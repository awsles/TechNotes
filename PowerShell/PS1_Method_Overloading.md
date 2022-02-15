$method = @{ param([int32] $t) if ($t -ge 0) { return $this.substring($t)) } else { return $this.substring(($this.Length + $t)) } }	

$mymethod = @{
  MemberName = 'splice';
  MemberType = 'ScriptMethod';
  # Note the use of param() to define the method parameter and
  # the use of $this to access the instance at hand.
  Value      = { param([int32] $t) if ($t -ge 0) { return $this.substring($t)) } else { return $this.substring(($this.Length + $t)) } }	
  Force      = $true
}

#
# The following example defines a new .myLower() method and attaches it to strings
#
$mymethod = @{
  MemberName = 'myLower';
  MemberType = 'ScriptMethod';
  # Note the use of param() to define the method parameter and
  # the use of $this to access the instance at hand.
  Value      = { param([int32] $t) $this.toLower() }	
  Force      = $true
}

Update-TypeData -TypeName 'string' @mymethod



#
# Slice() https://github.com/PowerShell/PowerShell/issues/14533
#
# String slice()
$stringMethod = @{
  MemberName = 'slice';
  MemberType = 'ScriptMethod';
  Value      = { param([int32] $t) $( if ($t -ge 0) {$this.substring($t)} else {$this.substring(($this.Length + $t))}) }	
  Force      = $true
}
Update-TypeData -TypeName 'string' @stringMethod

# System.Array slice()
$arrayMethod = @{
  MemberName = 'slice';
  MemberType = 'ScriptMethod';
  Value      = { param($t) $this[$t] }	
  Force      = $true
}
Update-TypeData -TypeName 'System.Array' @arrayMethod
