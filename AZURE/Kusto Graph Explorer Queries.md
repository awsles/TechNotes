# Kusto Graph Explorer Queries
The Resource Graph queries can be done through PowerShell or via the Azure Portal under "Resource Graph Explorer".
See also: https://docs.microsoft.com/en-us/azure/governance/resource-graph/samples/starter?tabs=azure-cli and
https://docs.microsoft.com/en-us/azure/governance/resource-graph/samples/advanced?tabs=azure-cli.

These queries may be pasted into the Azure Resource Graph Explorer or used via **Search-AzGraph -Query $Query**.
Note that when using Resource Graph Explorer, you will ONLY be able to see the subscriptions for which:
(a) you have permission; and (b) which are selected in your global subscriptions filter.

To invoke a Kusto Query in PowerShell:

```Search-AzGraph -First 1000 -Query $Query```

#### Important Tenant Limitations
Microsoft imposes a tenant-wide Kusto JOIN and mv-expand limits of 3. 
These can be increased to 5 joins and 4 mv-expands for your tenant, in order to support more complex resource graph queries
(which are needed for some of the examples below). The quota change applies to the underlying REST API,
which is used by everything EXCEPT for the Azure Resource Graph Explorer, which has an anomalous limit of 4 joins and 3 mv-expands.
However, you can build and save the query in the portal, and run it under Azure Resource Graph queries (which does use the REST API).

To test for the query limits on your tenant, try the following in a PowerShell window (after doing Login-AzAccount):
```
$q = 'Resources
| where type =~ "microsoft.network/networkinterfaces"
| mv-expand ipConfigurations = properties.ipConfigurations
| extend ipCount = array_length(properties.ipConfigurations)
| extend privateIPType = tostring(ipConfigurations.properties["privateIPAllocationMethod"])
| extend privateIP = tostring(ipConfigurations.properties["privateIPAddress"])
| extend subnetId = tostring(ipConfigurations.properties.subnet["id"])
| extend publicIPid = tostring(ipConfigurations.properties["publicIPAddress"].id)
| extend nicId = tostring(id)
| join kind=leftouter (ResourceContainers | where type=~ "microsoft.resources/subscriptions" 
       | project subscriptionName=name, subscriptionId) on subscriptionId 
| join kind=leftouter (Resources  
       | where type contains "publicIPAddresses" and isnotempty(properties.ipAddress)
       | extend publicIP = tostring(properties.ipAddress),
              publicIPid = tostring(id)) on publicIPid
| join kind=leftouter (Resources | where type =~ "microsoft.network/networksecuritygroups"
       | mv-expand nics = properties.networkInterfaces
       | extend nicId = tostring (nics.id),
              nicNSG = name,
              nicNSGgroup = resourceGroup  ) on nicId
| join kind=leftouter (Resources
       | where type =~ "microsoft.compute/virtualmachines" and isnotempty(properties.networkProfile.networkInterfaces)
       | extend vmName = name
       | extend vmSize = tostring(properties.hardwareProfile.vmSize)
       | extend osType = tostring(properties.storageProfile.osDisk.osType)
       | mv-expand nics = properties.networkProfile.networkInterfaces
       | extend nicId = tostring (nics.id) ) on nicId
| join kind=leftouter (Resources | where type =~ "microsoft.network/networksecuritygroups"
       | mv-expand subnets = properties.subnets
       | extend subnetId = tostring(subnets.id),
              vnetName = split(tostring(subnets.id),"/")[8],
              subnetName = split(tostring(subnets.id),"/")[10],
              subnetNSG = name,
              subnetNSGgroup = resourceGroup
       ) on subnetId
| project subscriptionId, subscriptionName, nicName=name, resourceGroup, vmName, vmSize, osType, vnetName, subnetName, nicNSG, subnetNSG, location, ipCount, privateIPType, privateIP, publicIP, tags, subnetId, nicId'

Search-AzGraph -First 1000 -Query $Q | ft
```
If you get an error, then there is a quota limit in place.

The document (https://docs.microsoft.com/en-us/azure/governance/resource-graph/concepts/query-language#supported-tabulartop-level-operators)
does state the max joins allowed is 3, however, production team overrides the limit to 4 for queries used in Azure Portal.

#### Additional Resources

* https://github.com/kobusd/Azure-Resource-Graph

# Queries
These queries are in no particular order as this list often serves as a notepad for
tracking useful queries and variations thereof.  Contributions are welcome!

### LIST ALL SUBSCRIPTIONS ###
```
ResourceContainers
| where type =~ 'microsoft.resources/subscriptions'
| project subscriptionName=name, subscriptionId
```

### LIST ALL VMs (simple) ###
```
Resources 
| where type =~ 'Microsoft.Compute/virtualMachines' 
| project subscriptionId, name, resourceGroup, location, properties.hardwareProfile.vmSize, 
		properties.storageProfile.osDisk.osType, properties.host.id, tags
| limit 25
```

### List all VMs with names that might indicate a database is present
```
resources
| where type == "microsoft.compute/virtualmachines"
	and (name contains "sql"
	or name contains "db"
	or name contains "database")
| join kind=leftouter (ResourceContainers | where type=~ 'microsoft.resources/subscriptions' 
       | project subscriptionName=name, subscriptionId) on subscriptionId
| project subscriptionId, subscriptionName, name, resourceGroup, location, properties, tags, id
```

### List VMs with detail (excluding IP info)
```
Resources
| where type == "microsoft.compute/virtualmachines" and isnotempty(properties.networkProfile.networkInterfaces)
| extend vmSize = tostring(properties.hardwareProfile.vmSize)
| extend osType = tostring(properties.storageProfile.osDisk.osType)
| extend nicId = properties.networkProfile.networkInterfaces[0].id
| join kind=leftouter (ResourceContainers | where type=~'microsoft.resources/subscriptions' 
	| project subscriptionName=name, subscriptionId) on subscriptionId 
| project name, resourceGroup, subscriptionName, location, osType, privateIP, publicIP, vmSize, tags, id
```

### List VMs with detail (including IP info)
Note that resource graph is NOT always up to date with dynamically assigned public IP addresses.
A VM can be running for quite a long time before the public IP address displays in resource graph.

```
Resources
| where type == "microsoft.compute/virtualmachines" and isnotempty(properties.networkProfile.networkInterfaces)
| extend vmSize = tostring(properties.hardwareProfile.vmSize)
| extend osType = tostring(properties.storageProfile.osDisk.osType)
| extend vmProperties = tostring(properties)
| mv-expand nics = properties.networkProfile.networkInterfaces
| extend nicId = tostring(nics.id)
| join kind=leftouter (Resources
	| where type =~ "microsoft.network/networkinterfaces"
	| extend privateIP = tostring(properties.ipConfigurations[0].properties["privateIPAddress"])
	| extend pubId = tostring(properties.ipConfigurations[0].properties.publicIPAddress.id)
	| extend subnetId = tostring(properties.ipConfigurations[0].properties.subnet.id)
	| join kind=leftouter (Resources | where type =~ "microsoft.network/publicipaddresses"
		| extend fqdn = properties.dnsSettings.fqdn
		| extend publicIP = tostring(properties.ipAddress) // May not be up to date...
		| project pubId=id, publicIP, fqdn, pubIpProperties=properties) on pubId
	| project nicId=id, nicName=name, privateIP, publicIP, fqdn, pubId, nicProperties=properties, pubIpProperties) on nicId
| join kind=leftouter (ResourceContainers | where type=~'microsoft.resources/subscriptions' 
	| project subscriptionName=name, subscriptionId) on subscriptionId 
| project name, resourceGroup, subscriptionName, location, osType, vmSize, nicName, privateIP, publicIP, fqdn, nicProperties, pubIpProperties, vmProperties, nicId, id
```

### List NSGs by Inbound Destinations and Ports
Excludes defaultSecurityRules.

```
resources
| where type =~ "microsoft.network/networksecuritygroups"
| mv-expand rule = properties.securityRules
| where rule.properties.access =~ "Allow" and rule.properties.direction =~ "Inbound" 
| extend ruleName = rule.name,
	priority = rule.properties.priority,
	dstAddressPrefix = rule.properties.destinationAddressPrefix,
	dstAddresses = rule.properties.destinationAddressPrefixes,
	dstPortRange = rule.properties.destinationPortRange,
	dstPortRanges = rule.properties.destinationPortRanges
| project name, resourceGroup, location, subscriptionId, priority, dstAddressPrefix, dstAddresses, dstPortRange, dstPortRanges, rule, properties, tags
```

### List all NICS and the associated VM in a given subnet name
To Do: Output the VNET and subnet and privateIP as well.

```
Resources 
| where type =~ "microsoft.network/networkinterfaces" and (tostring(properties) contains 'azsu-subn-devtest-h-web-bsmart-001')
| extend subnets = tostring(properties["subnets"])
| extend prefixCount = array_length(properties.subnets)
| extend nicName = name
| extend nicId = id
| join kind=leftouter (Resources
	| where type =~ "microsoft.compute/virtualmachines" 
	| extend nicId = tostring(properties.networkProfile.networkInterfaces[0].id)
	| project VmName=name, vmId=id, vmProperties=properties, nicId) on nicId
| join kind=leftouter (ResourceContainers | where type=~'microsoft.resources/subscriptions' 
	| project subscriptionName=name, subscriptionId) on subscriptionId 
| project VmName, resourceGroup, subscriptionName, location, nicName, properties

```

### LIST ALL NICs with Public and Private IP addresses abd FQDNs
Note that resource graph is NOT always up to date with dynamically assigned public IP addresses.
A VM can be running for quite a long time before the public IP address displays in resource graph.

```
Resources
| where type =~ "microsoft.network/networkinterfaces" 
| extend privateIP = tostring(properties.ipConfigurations[0].properties["privateIPAddress"])
| extend pubId = tostring(properties.ipConfigurations[0].properties.publicIPAddress.id)
| extend subnetId = tostring(properties.ipConfigurations[0].properties.subnet.id)
| join kind=leftouter (Resources | where type =~ "microsoft.network/publicipaddresses"
	| extend fqdn = properties.dnsSettings.fqdn
	| extend publicIP = tostring(properties.ipAddress) // May be out of date...
	| project pubId=id, publicIP, fqdn, pubIpProperties=properties) on pubId
| project nicId=id, nicName=name, privateIP, publicIP, fqdn, pubId, pubIpProperties
```

### List all NICs with the associated VMs
TO DO.


### List all devices with 2 or more IP addresses
THIS IS TERRIBLE. Use mv-expand
```
Resources  
| where type startswith 'microsoft.network' and isnotempty(properties.ipConfigurations[1])
| extend ipCount = array_length(properties.ipConfigurations)
| extend privateIPType = tostring(properties.ipConfigurations[0].properties["privateIPAllocationMethod"])
| extend privateIP = tostring(properties.ipConfigurations[0].properties["privateIPAddress"])
| extend privateIPType2 = tostring(properties.ipConfigurations[1].properties["privateIPAllocationMethod"])
| extend privateIP2 = tostring(properties.ipConfigurations[1].properties["privateIPAddress"])
| extend privateIPType3 = tostring(properties.ipConfigurations[2].properties["privateIPAllocationMethod"])
| extend privateIP3 = tostring(properties.ipConfigurations[2].properties["privateIPAddress"])
```


### List Network Interfaces
```
Resources
| where type =~ "microsoft.network/networkinterfaces"
| mv-expand ipConfigurations = properties.ipConfigurations
| extend ipCount = array_length(properties.ipConfigurations)
| extend privateIPType = tostring(ipConfigurations.properties["privateIPAllocationMethod"])
| extend privateIP = tostring(ipConfigurations.properties["privateIPAddress"])
| extend publicIP = tostring(ipConfigurations.properties["publicIPAddress"])
| extend subnet = tostring(ipConfigurations.properties.subnet["id"])
```


### List all Network Interfaces (NICs) 
This lists both their public and private IP addresses and associated subnet ID.
```
Resources
| where type =~ "microsoft.network/networkinterfaces"
| mv-expand ipConfigurations = properties.ipConfigurations
| extend ipCount = array_length(properties.ipConfigurations)
| extend privateIPType = tostring(ipConfigurations.properties["privateIPAllocationMethod"])
| extend privateIP = tostring(ipConfigurations.properties["privateIPAddress"])
| extend subnetId = tostring(ipConfigurations.properties.subnet["id"])
| extend publicIPid = tostring(ipConfigurations.properties["publicIPAddress"].id)
| extend nicId = tostring(id)
| join kind=leftouter (ResourceContainers | where type=~'microsoft.resources/subscriptions' 
	| project subscriptionName=name, subscriptionId) on subscriptionId 
| join kind=leftouter (Resources  
	| where type contains 'publicIPAddresses' and isnotempty(properties.ipAddress)
	| extend publicIP = tostring(properties.ipAddress),
		publicIPid = tostring(id)) on publicIPid
| join kind=leftouter (Resources | where type == "microsoft.network/networksecuritygroups"
	| mv-expand nics = properties.networkInterfaces
	| extend nicId = tostring (nics.id),
		nicNSG = name,
		resourceGroupNSG = resourceGroup  ) on nicId
| project subscriptionName, name, resourceGroup, location, ipCount, privateIPType, privateIP, publicIP, nicNSG, resourceGroupNSG, tags, subnetId, nicId
```


### List all Network Interfaces (NICs) with NSG detail
This lists all NICs with the associated NSG, subnet, subnet NSG, 
and their public and private IP addresses.  Very use for seeing which VMs
are protected by an NSG and which are not.

NOTE: This only works in the Azure ARM Portal. To use in PowerShell, you MUST ask Microsoft
to increase your mv-expand and join limits!


```
Resources
| where type =~ "microsoft.network/networkinterfaces"
| mv-expand ipConfigurations = properties.ipConfigurations
| extend ipCount = array_length(properties.ipConfigurations)
| extend privateIPType = tostring(ipConfigurations.properties["privateIPAllocationMethod"])
| extend privateIP = tostring(ipConfigurations.properties["privateIPAddress"])
| extend subnetId = tostring(ipConfigurations.properties.subnet["id"])
| extend publicIPid = tostring(ipConfigurations.properties["publicIPAddress"].id)
| extend nicId = tostring(id)
| join kind=leftouter (ResourceContainers | where type=~ "microsoft.resources/subscriptions" 
	| project subscriptionName=name, subscriptionId) on subscriptionId 
| join kind=leftouter (Resources  
	| where type contains "publicIPAddresses" and isnotempty(properties.ipAddress)
	| extend publicIP = tostring(properties.ipAddress),
		publicIPid = tostring(id)) on publicIPid
| join kind=leftouter (Resources | where type =~ "microsoft.network/networksecuritygroups"
	| mv-expand nics = properties.networkInterfaces
	| extend nicId = tostring (nics.id),
		nicNSG = name,
		nicNSGgroup = resourceGroup  ) on nicId
| join kind=leftouter (Resources | where type =~ "microsoft.network/networksecuritygroups"
	| mv-expand subnets = properties.subnets
	| extend subnetId = tostring(subnets.id),
		vnetName = split(tostring(subnets.id),"/")[8],
		subnetName = split(tostring(subnets.id),"/")[10],
		subnetNSG = name,
		subnetNSGgroup = resourceGroup
	) on subnetId
| project subscriptionName, nicName=name, resourceGroup, vnetName, subnetName, nicNSG, subnetNSG, location, ipCount, privateIPType, privateIP, publicIP, tags, subnetId, nicId
```

The query below lists all with VM name with subscription name.
This query requires a quota increase from Microsoft.

```
Resources
| where type =~ "microsoft.network/networkinterfaces"
| mv-expand ipConfigurations = properties.ipConfigurations
| extend ipCount = array_length(properties.ipConfigurations)
| extend privateIPType = tostring(ipConfigurations.properties["privateIPAllocationMethod"])
| extend privateIP = tostring(ipConfigurations.properties["privateIPAddress"])
| extend subnetId = tostring(ipConfigurations.properties.subnet["id"])
| extend publicIPid = tostring(ipConfigurations.properties["publicIPAddress"].id)
| extend nicId = tostring(id)
| join kind=leftouter (ResourceContainers | where type=~ "microsoft.resources/subscriptions" 
	| project subscriptionName=name, subscriptionId) on subscriptionId 
| join kind=leftouter (Resources  
	| where type contains "publicIPAddresses" and isnotempty(properties.ipAddress)
	| extend publicIP = tostring(properties.ipAddress),
		publicIPid = tostring(id)) on publicIPid
| join kind=leftouter (Resources | where type =~ "microsoft.network/networksecuritygroups"
	| mv-expand nics = properties.networkInterfaces
	| extend nicId = tostring (nics.id),
		nicNSG = name,
		nicNSGgroup = resourceGroup  ) on nicId
| join kind=leftouter (Resources
	| where type =~ "microsoft.compute/virtualmachines" and isnotempty(properties.networkProfile.networkInterfaces)
	| extend vmName = name
	| extend vmSize = tostring(properties.hardwareProfile.vmSize)
	| extend osType = tostring(properties.storageProfile.osDisk.osType)
	| mv-expand nics = properties.networkProfile.networkInterfaces
	| extend nicId = tostring (nics.id) ) on nicId
| join kind=leftouter (Resources | where type =~ "microsoft.network/networksecuritygroups"
	| mv-expand subnets = properties.subnets
	| extend subnetId = tostring(subnets.id),
		vnetName = split(tostring(subnets.id),"/")[8],
		subnetName = split(tostring(subnets.id),"/")[10],
		subnetNSG = name,
		subnetNSGgroup = resourceGroup
	) on subnetId
| project subscriptionId, subscriptionName, nicName=name, resourceGroup, vmName, vmSize, osType, vnetName, subnetName, nicNSG, subnetNSG, location, ipCount, privateIPType, privateIP, publicIP, tags, subnetId, nicId
```



### List FQDNs
This is usually just database servers.
```
Resources
| where isnotempty(properties.fullyQualifiedDomainName)
| extend FQDN = tostring(properties.fullyQualifiedDomainName)
```

### List Public IP Addresses
```
Resources  
| where type contains 'publicIPAddresses' and isnotempty(properties.ipAddress)
| extend publicIP = tostring(properties.ipAddress)
```


### Splits IP configurations into a single row per entry
```
Resources
| where type =~ "microsoft.network/networkinterfaces" and isnotempty(properties.ipConfigurations[1])
| mv-expand x = properties.ipConfigurations
```



### Find NIC by private IP address
This outputs the vmName, resourceGroup, subscriptionName, location, privateIP, privateIPType, publicIP, vnetName, subnetName, vmId, and subnetId.

```
Resources
| where type =~ "microsoft.network/networkinterfaces" and isnotempty(properties.ipConfigurations)
| mv-expand ipConfiguration = properties.ipConfigurations
| where ipConfiguration.properties.privateIPAddress == "10.65.96.6" or ipConfiguration.properties.privateIPAddress == "10.65.105.100"
| extend
	privateIPType = tostring(ipConfiguration.properties.privateIPAllocationMethod),
	privateIP = tostring(ipConfiguration.properties.privateIPAddress),
	publicIPid = tostring(ipConfiguration.properties.publicIPAddress.id),
	subnetId = tostring(ipConfiguration.properties.subnet.id),
	vnetName = tostring(split(ipConfiguration.properties.subnet.id,'/',8)[0]),
	subnetName = tostring(split(ipConfiguration.properties.subnet.id,'/',10)[0]),
	nicId = id
| join kind=leftouter (Resources | where type =~ "microsoft.network/publicipaddresses"
    | extend publicIP = tostring(properties.ipAddress)
    | project publicIPid=id, publicIP) on publicIPid
| join kind=leftouter (Resources
	| where type =~ "microsoft.compute/virtualmachines"
	| extend
		networkProfile = tostring(properties.networkProfile),
		computerName = properties.osProfile.computerName
	| mv-expand networkInterfaces = properties.networkProfile.networkInterfaces
	| extend
		nicId = tostring(networkInterfaces.id),
		vmName = name,
		vmId = id
	| project vmName, nicId, vmId) on nicId
| join kind=leftouter (ResourceContainers | where type=~"microsoft.resources/subscriptions" 
	| project subscriptionName=name, subscriptionId) on subscriptionId
| project vmName, resourceGroup, subscriptionName, location, privateIP, privateIPType, publicIP, vnetName, subnetName, vmId, subnetId
```

### Find VM given its network interface ID

```
Resources
| where type =~ "microsoft.compute/virtualmachines"
| extend networkProfile = tostring(properties.networkProfile)
| extend computerName = properties.osProfile.computerName
| mv-expand networkInterfaces = properties.networkProfile.networkInterfaces
| where networkInterfaces.id =~ "%%ID%%"
| join kind=leftouter (ResourceContainers | where type=~"microsoft.resources/subscriptions" 
	| project subscriptionName=name, subscriptionId) on subscriptionId 
```

### List all Resources (or ResourceContainers) without a given tag

```
resources
| where properties.provisioningState =~ "Succeeded" and tostring(tags) !contains '"CreatedBy"'
| join kind=leftouter (ResourceContainers | where type =~ 'microsoft.resources/subscriptions'
    | project subscriptionName=name, subscriptionId) on subscriptionId
```


### List Azure Bastion Hosts with IP Addresses

```
Resources
| where type =~ "microsoft.network/networkinterfaces" and isnotempty(properties.ipConfigurations)
| mv-expand ipConfiguration = properties.ipConfigurations
| where ipConfiguration.properties.privateIPAddress startswith "10.68.193."
| extend privateIPType = tostring(ipConfiguration.properties.privateIPAllocationMethod)
| extend privateIP = tostring(ipConfiguration.properties.privateIPAddress)
| extend publicIPid = tostring(ipConfiguration.properties.publicIPAddress.id)
| join kind=leftouter (ResourceContainers | where type =~ 'microsoft.resources/subscriptions'
    | project SubscriptionName=name, subscriptionId) on subscriptionId
| join kind=leftouter (Resources | where type =~ "microsoft.network/publicipaddresses"
    | extend publicIPaddr = tostring(properties.ipAddress)
    | project publicIPid=id, publicIPaddr) on publicIPid
| project privateIP, privateIPType,publicIPaddr,name,type,location,resourceGroup,tags,id,publicIPid
| sort by privateIP asc
```

### List all vNets and subnets 
This lists them all with associated IP addresses (public and private) and NSGs

```
resources
| where type == "microsoft.network/virtualnetworks"
| mv-expand subnets = properties.subnets
| extend subnetName = subnets.name,
	addressPrefix = subnets.properties.addressPrefix,
	p = subnets.properties,
	subnetId = strcat(id,'/subnets/',subnets.name)
| join kind=leftouter (ResourceContainers | where type =~ 'microsoft.resources/subscriptions'
    | project subscriptionName=name, subscriptionId) on subscriptionId
| join kind=leftouter (Resources | where type == "microsoft.network/networksecuritygroups"
	| mv-expand subnets = properties.subnets
	| extend subnetId = tostring(subnets.id),
		subnetNSG = name,
		resourceGroupNSG = resourceGroup
	) on subnetId
| project subscriptionName, vnetName=name, subnetName, addressPrefix, resourceGroup, location, subnetNSG, resourceGroupNSG, tags, subnetId, id
```


### List all NSGs with associated NICs

```
Resources
| where type == "microsoft.network/networksecuritygroups"
| mv-expand networkInterfaces = properties.networkInterfaces

Resources
| where type == "microsoft.network/networksecuritygroups"
| mv-expand subnets = properties.subnets
| extend subnetId = subnets.id
```


### List Virtual Networks (VNets) with IP addresses
This is crude as I need to way to count and join all instances

```
Resources
| where type =~ "microsoft.network/virtualnetworks"
| extend subnets = tostring(properties["subnets"])
| extend prefixCount = array_length(properties.subnets)
| extend ip1 = tostring(properties.subnets[0].properties.addressPrefix)
| extend ip2 = tostring(properties.subnets[1].properties.addressPrefix)
| extend ip3 = tostring(properties.subnets[2].properties.addressPrefix)
| extend ip4 = tostring(properties.subnets[3].properties.addressPrefix)
| extend ip5 = tostring(properties.subnets[4].properties.addressPrefix)
```

### List all resources by Public IP Address
A shame there isn't a private IP address equivalent...
```
Resources
| where type =~ "microsoft.network/publicipaddresses"
| extend ipAddress = tostring(properties.ipAddress)
```

### LIST ALL VMs (joined with subscription name) ###
```
Resources 
| where type =~ 'Microsoft.Compute/virtualMachines' 
| extend ServiceOwner = tostring(tags['Service Owner'])
| extend ServiceName = tostring(tags['Service Name'])
| extend CostCodeID = tostring(tags['Cost Code ID'])
| join kind=leftouter (ResourceContainers | where type=~'microsoft.resources/subscriptions' 
	| project SubName=name, subscriptionId) on subscriptionId 
| project subscriptionId, name, resourceGroup, location,
	vmSize = tostring(properties.hardwareProfile.vmSize), 
	osType = tostring(properties.storageProfile.osDisk.osType),
	hostId = tostring(properties.host.id), tags, id,
	ServiceOwner,ServiceName,CostCodeID
```

	
### LIST ALL VMs WHICH HAVE OMS EXTENSIONS (with workspace ID mapped to details) ###
```
Resources
| where type =~ 'microsoft.compute/virtualmachines/extensions'
and properties.publisher =~ 'Microsoft.EnterpriseCloud.Monitoring'
| extend workspaceId = tostring(properties.settings.workspaceId)
| extend vmName = tostring(split(id,'/',8)[0])
| join kind=leftouter (Resources | where type=~ 'microsoft.operationalinsights/workspaces' 
    | project workspaceId=tostring(properties.customerId),
		sku = tostring(properties.sku.name), tags, id,
        retentionInDays = tostring(properties.retentionInDays),
        dailyQuotaGb = tostring(properties.workspaceCapping.dailyQuotaGb)) on workspaceId
| project subscriptionId, vmName, id, tags, sku, name, kind, plan, location, resourceGroup,
	managedBy, identity, tenantId, workspaceId, retentionInDays
```


### LIST ALL VMs WHICH HAVE OMS EXTENSIONS (with subscription name and named details) ###
```
Resources
| where type =~ 'microsoft.compute/virtualmachines/extensions'
	and properties.publisher =~ 'Microsoft.EnterpriseCloud.Monitoring'
| extend ExtensionName = tostring(name)
| extend workspaceId = tostring(properties.settings.workspaceId)
| extend vmName = tostring(split(id,'/',8)[0])
| join kind=leftouter (ResourceContainers | where type=~'microsoft.resources/subscriptions' 
	| project SubName=name, subscriptionId) on subscriptionId 
| join kind=leftouter (Resources | where type=~ 'microsoft.operationalinsights/workspaces' 
    | project workspaceId=tostring(properties.customerId),
		sku1 = tostring(properties.sku.name), tags, id,
        retentionInDays = tostring(properties.retentionInDays),
        dailyQuotaGb = tostring(properties.workspaceCapping.dailyQuotaGb)) on workspaceId
| project subscriptionId, SubName, vmName, resourceGroup, sku1, ExtensionName, kind, plan, location,
	managedBy, identity, tenantId, workspaceId, retentionInDays, tags, properties, id
```


### LIST ALL VMs AND THIER OMS EXTENSIONS (with subscription name and named details) ###
```
Resources
| where type =~ 'microsoft.compute/virtualmachines/extensions'
	and properties.publisher =~ 'Microsoft.EnterpriseCloud.Monitoring'
| extend ExtensionName = tostring(name)
| extend workspaceId = tostring(properties.settings.workspaceId)
| extend vmName = tostring(split(id,'/',8)[0])
| join kind=leftouter (ResourceContainers | where type=~'microsoft.resources/subscriptions' 
	| project SubName=name, subscriptionId) on subscriptionId 
| join kind=leftouter (Resources | where type=~ 'microsoft.operationalinsights/workspaces' 
    | project workspaceId=tostring(properties.customerId),
		sku1 = tostring(properties.sku.name), tags, id,
        retentionInDays = tostring(properties.retentionInDays),
        dailyQuotaGb = tostring(properties.workspaceCapping.dailyQuotaGb)) on workspaceId
| project subscriptionId, SubName, vmName, resourceGroup, sku1, ExtensionName, kind, plan, location,
	managedBy, identity, tenantId, workspaceId, retentionInDays, tags, properties, id
```


	
ALTERNATE:
```
Resources
| where type =~ 'Microsoft.Compute/virtualMachines' 
| project subscriptionId, name, resourceGroup, location,
	vmSize = tostring(properties.hardwareProfile.vmSize), 
	osType = tostring(properties.storageProfile.osDisk.osType),
	hostId = tostring(properties.host.id), tags, id
| join kind=leftouter (ResourceContainers | where type=~'microsoft.resources/subscriptions' 
	| project SubName=name, subscriptionId) on subscriptionId 
| join kind=leftouter (Resources
	| where type =~ 'microsoft.compute/virtualmachines/extensions'
		and properties.publisher =~ 'Microsoft.EnterpriseCloud.Monitoring'
	| extend ExtensionName = tostring(name)
	| extend workspaceId = tostring(properties.settings.workspaceId)
	| extend id1 = tostring(split(tostring(id),'/extensions')[0])
	| extend vmName = tostring(split(id,'/',8)[0])
	| project-away id, tags, type, subscriptionId, name, resourceGroup, location) on $left.id == $right.id1
| join kind=leftouter (Resources | where type=~ 'microsoft.operationalinsights/workspaces' 
    | project workspaceId=tostring(properties.customerId),
		sku1 = tostring(properties.sku.name), tags, id,
        retentionInDays = tostring(properties.retentionInDays),
        dailyQuotaGb = tostring(properties.workspaceCapping.dailyQuotaGb)) on workspaceId

| project subscriptionId, SubName, vmName, resourceGroup, ExtensionName, sku1, kind, plan, location,
	managedBy, identity, tenantId, workspaceId, retentionInDays, dailyQuotaGb, tags, properties, id
```


### LIST ALL VIRTUAL MACHINES WITH EXTENSIONS
This may not be working...
```
Resources
| where type =~ 'microsoft.compute/virtualmachines/extensions'
	and properties.publisher =~ 'Microsoft.EnterpriseCloud.Monitoring'
| extend ExtensionName = tostring(name)
| extend workspaceId = tostring(properties.settings.workspaceId)
| extend vmName = tostring(split(id,'/',8)[0])
| extend vmId = tolower(tostring(split(tostring(id),'/extensions')[0]))
| join kind=leftouter (ResourceContainers | where type=~'microsoft.resources/subscriptions' 
	| project SubName=name, subscriptionId) on subscriptionId 
| join kind=leftouter (Resources | where type=~ 'microsoft.operationalinsights/workspaces' 
    | project workspaceId=tostring(properties.customerId),
		sku1 = tostring(properties.sku.name), tags, id,
        retentionInDays = tostring(properties.retentionInDays),
        dailyQuotaGb = tostring(properties.workspaceCapping.dailyQuotaGb)) on workspaceId
| project subscriptionId, SubName, vmName, resourceGroup, sku1, ExtensionName, kind, plan, location,
	managedBy, identity, tenantId, workspaceId, retentionInDays, tags, properties, id, vmId

| join kind=rightouter (Resources | where type =~ 'Microsoft.Compute/virtualMachines' 
	| extend vmId = tolower(tostring(id))
	| project subscriptionId, name, resourceGroup, location,
		vmSize = tostring(properties.hardwareProfile.vmSize), 
		osType = tostring(properties.storageProfile.osDisk.osType),
		hostId = tostring(properties.host.id), tags, vmId) on vmId


	
	
| join kind=fullouter (Resources | where type =~ 'Microsoft.Compute/virtualMachines' 
	| extend vmId = tolower(tostring(id))
	| project subscriptionId, name, resourceGroup, location,
		vmSize = tostring(properties.hardwareProfile.vmSize), 
		osType = tostring(properties.storageProfile.osDisk.osType),
		hostId = tostring(properties.host.id), tags, id) on vmId
```
	
	
### LIST ALL VIRTUAL MACHINES WITH DETAIL 1
```
Resources
| where type =~ 'Microsoft.Compute/virtualMachines' 
| project subscriptionId, name, resourceGroup, location, properties.hardwareProfile.vmSize, 
		properties.storageProfile.osDisk.osType, properties.host.id, tags, id
| join kind=leftouter (Resources
	| where type =~ 'microsoft.compute/virtualmachines/extensions'
		and properties.publisher =~ 'Microsoft.EnterpriseCloud.Monitoring'
	| extend ExtensionName = tostring(name)
	| extend workspaceId = tostring(properties.settings.workspaceId)
	| extend id1 = tostring(split(tostring(id),'/extensions'))
	| extend vmName = tostring(split(id,'/',8)[0])) on $left.id == $right.id1
```


### LIST ALL VIRTUAL MACHINES WITH DETAIL 2
```
Resources 
| where type =~ 'Microsoft.Compute/virtualMachines' 
| join kind=leftouter (ResourceContainers | where type=~'microsoft.resources/subscriptions' 
	| project SubName=name, subscriptionId) on subscriptionId 
| project subscriptionId, name, resourceGroup, location, properties.hardwareProfile.vmSize, 
		properties.storageProfile.osDisk.osType, properties.host.id, tags
```


### LIST RESOURCE COUNTS BY SUBSCRIPTION
```
Resources
| summarize resourceCount=count() by subscriptionId
| join kind=leftouter (ResourceContainers | where type=='microsoft.resources/subscriptions' | project SubName=name, subscriptionId) on subscriptionId
| project-away subscriptionId, subscriptionId1
```

### LIST ALL KEY VAULTS
```
Resources
| where type == 'microsoft.keyvault/vaults'
| join (ResourceContainers | where type=='microsoft.resources/subscriptions' | project SubName=name, subscriptionId) on subscriptionId
| project type, name, SubName
| limit 1
```

### LIST ALL VIRTUAL MACHINES
```
Resources
| where type =~ 'Microsoft.Compute/virtualMachines'
| join (ResourceContainers | where type =~ 'microsoft.resources/subscriptions' | project SubName=name, subscriptionId) on subscriptionId
| project type, name, SubName
| limit 25
```

---


### LIST ALL DATA SERVICES ###

```
Resources 
| where (type contains 'microsoft.azuredata'
       or type contains 'microsoft.data'
       or type contains 'microsoft.db'
       or type contains 'microsoft.documentdb'
       or type contains 'microsoft.sql'
       or type contains 'microsoft.storage')
| extend fullyQualifiedDomainName = tostring(properties.fullyQualifiedDomainName)
| extend size = tostring(properties.currentServiceObjectiveName)
| join kind=leftouter (ResourceContainers | where type=~ 'microsoft.resources/subscriptions' 
       | project SubName=name, subscriptionId) on subscriptionId
| project type, subscriptionId, SubName, name, resourceGroup, fullyQualifiedDomainName, size, location, tags, properties, managedBy, id


PS C:\PS1> Import-Module Az.ResourceGraph
PS C:\PS1> $q = "Resources 
| where (type contains 'microsoft.azuredata'
       or type contains 'microsoft.data'
       or type contains 'microsoft.db'
       or type contains 'microsoft.documentdb'
       or type contains 'microsoft.sql'
       or type contains 'microsoft.storage')
| extend fullyQualifiedDomainName = tostring(properties.fullyQualifiedDomainName)
| extend size = tostring(properties.currentServiceObjectiveName)
| join kind=leftouter (ResourceContainers | where type=~ 'microsoft.resources/subscriptions' 
       | project SubName=name, subscriptionId) on subscriptionId
| project type, subscriptionId, SubName, name, resourceGroup, fullyQualifiedDomainName, size, location, tags, properties, managedBy, id"



PS C:\PS1> $Results = Search-AzGraph -query $q -First 5000 ; write-host "$($Results.Count) entries"

PS C:\PS1> $Results | Out-GridView
```


```
resources
| join kind=leftouter (ResourceContainers | where type=~'microsoft.resources/subscriptions' 
	| project SubName=name, subscriptionId) on subscriptionId
	
| project subscriptionId, SubName, resourceGroup
```


# List all resource groups, tags, and VM counts

```
ResourceContainers
| where type=~ 'microsoft.resources/subscriptions/resourcegroups' 
| extend ServiceOwner = tostring(tags["Service Owner"])
| extend ServiceName = tostring(tags["Service Name"])
| extend CostCodeID = tostring(tags["Cost Code ID"])
| join kind=leftouter (Resources | where type=~ 'microsoft.compute/virtualmachines' 
	| summarize count() by tostring(resourceGroup)
	| project resourceGroup, VMcount = count_) on resourceGroup
| join kind=leftouter (Resources | where type contains 'microsoft.classic' 
	| summarize count() by tostring(resourceGroup)
	| project resourceGroup, ClassicCount = count_) on resourceGroup
| project subscriptionId, name, location, VMcount, ClassicCount, ServiceOwner, ServiceName, CostCodeID, tenantId
```

# List all Resource Groups with tags
This also pulls out a few key tags...
```
$KustoQuery = "resourcecontainers
 | where type == 'microsoft.resources/subscriptions/resourcegroups'
 | extend ServiceOwner = tostring(tags['Service Owner'])
 | extend ServiceName = tostring(tags['Service Name'])
 | extend CostCodeID = tostring(tags['Cost Code ID'])
 | join kind=leftouter (ResourceContainers | where type=~'microsoft.resources/subscriptions' 
 | project SubName=name, subscriptionId) on subscriptionId
 | project id, subscriptionId, SubName, type, resourceGroup, location, tags, ServiceOwner, ServiceName, CostCodeID, tenantId, properties"
$ResourceGroups = @()
$SkipCount = 0
Do 
{	# Search-AzGraph doesn't like a -SkipCount of zero
	if ($SkipCount -eq 0)
		{ $r = Search-AzGraph -query $KustoQuery -First 1000 } # -ErrorAction SilentlyContinue
	else
		{ $r = Search-AzGraph -query $KustoQuery -First 1000 -Skip $SkipCount } # -ErrorAction SilentlyContinue
	$ResourceGroups += $r
	$SkipCount += 1000
}
Until ($r.Count -lt 1000)
```

## List all Resource Groups with Subordinate Cost Code ID
```
resourcecontainers
 | where type == "microsoft.resources/subscriptions/resourcegroups"
 | extend ServiceOwner = tostring(tags["Service Owner"])
 | extend ServiceName = tostring(tags["Service Name"])
 | extend CostCodeID = tostring(tags["Cost Code ID"])
| join kind=inner (Resources | where tags contains "Cost Code ID" | extend SubCostCodeID = tostring(tags["Cost Code ID"]) | project resourceGroup,SubordinateTags=tags,SubCostCodeID) on resourceGroup 
| join kind=leftouter (ResourceContainers | where type=~'microsoft.resources/subscriptions' 
	| project SubName=name, subscriptionId) on subscriptionId
| project subscriptionId, SubName, resourceGroup, location, CostCodeID, ServiceOwner, ServiceName, tags,SubordinateTags, SubCostCodeID
```

## List all Resources WITHOUT 'Cost Code ID' tag
```
Resources
  | where tags !contains "Cost Code ID" 
| join kind=leftouter (ResourceContainers | where type=~'microsoft.resources/subscriptions' 
	| project SubName=name, subscriptionId) on subscriptionId
| project subscriptionId, SubName, name, resourceGroup, location, tags, type
```

## mv-expand

https://stackoverflow.com/questions/56159424/how-do-i-iterate-through-array-in-kusto

https://docs.microsoft.com/en-us/azure/data-explorer/kusto/query/mvexpandoperator

```
 where type =~ "microsoft.network/networksecuritygroups"
| mv-expand rules = properties.defaultSecurityRules
| where rules.properties.destinationAddressPrefix =~ "*"
```


---
## Using PowerShell

```
$q = "YOUR_KUSTO_QUERY"
$Results = Search-AzGraph -query $q -First 5000 ; write-host "$($Results.Count) entries"
$Results | Out-GridView  # Or Export-CSV
```

---
## References

https://docs.microsoft.com/en-us/azure/kusto/query/
https://docs.microsoft.com/en-us/azure/governance/resource-graph/concepts/query-language
https://docs.microsoft.com/en-us/azure/governance/resource-graph/samples/starter?tabs=azure-cli
https://docs.microsoft.com/en-us/azure/kusto/query/joinoperator
https://docs.microsoft.com/en-us/azure/firewall/log-analytics-samples
