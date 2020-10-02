# Kusto Graph Explorer Queries
The Resource Graph queries can be done through PowerShell or via the Azure Portal under "Resource Graph Explorer".


### LIST ALL SUBSCRIPTIONS ###
```
ResourceContainers
| where type =~ 'microsoft.resources/subscriptions'
| project SubName=name, subscriptionId
```

### LIST ALL VMs (simple) ###
```
Resources 
| where type =~ 'Microsoft.Compute/virtualMachines' 
| project subscriptionId, name, resourceGroup, location, properties.hardwareProfile.vmSize, 
		properties.storageProfile.osDisk.osType, properties.host.id, tags
| limit 25
```

### LIST ALL NICs with Public and Private IP addresses along with their associated VM and subscription
```
Resources
| where type =~ "microsoft.network/networkinterfaces"
and properties.ipConfigurations[0[.properties.privateIPAddress =~ "10.71.2.2"
| extend privateIPType = tostring(properties.ipCOnfigurations[0].properties["privateIPAllocationMethod2])
| extend privateIP = tostring(properties.ipConfigurations[0].properties["privateIPAddress"])
| extend publicIP = tostring(properties.ipConfigurations[0].properties["publicIPAddress"])
| extend subnet = tostring(properties.ipConfigurations[0].properties.subnet["id"])
```

### List all devices with 2 or more IP addresses
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
| extend ipCount = array_length(properties.ipConfigurations)
| extend privateIPType = tostring(properties.ipConfigurations[0].properties["privateIPAllocationMethod"])
| extend privateIP = tostring(properties.ipConfigurations[0].properties["privateIPAddress"])
| extend publicIP = tostring(properties.ipConfigurations[0].properties["publicIPAddress"])
| extend subnet = tostring(properties.ipConfigurations[0].properties.subnet["id"])
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



### Find by IP address
```
Resources
| where type =~ "microsoft.network/networkinterfaces" and isnotempty(properties.ipConfigurations)
| mv-expand ipConfiguration = properties.ipConfigurations
| where ipConfiguration.properties.privateIPAddress =~ "10.64.193.86"
| extend privateIPType = tostring(ipConfiguration.properties.privateIPAllocationMethod)
| extend privateIP = tostring(ipConfiguration.properties.privateIPAddress)
| extend publicIPid = tostring(ipConfiguration.properties.publicIPAddress.id)
| join kind=leftouter (Resources | where type =~ "microsoft.network/publicipaddresses"
    | extend publicIPaddr = tostring(properties.ipAddress)
    | project publicIPid=id, publicIPaddr) on publicIPid
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


### List Virtuan Networks (VNets) with IP addresses
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
