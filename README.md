# New-Tattoo
Script to collect Task Sequence Variables within an OSD Task Sequence, and tattoo said information into various locations during deployment so that it persists to the deployed machine.  This is a fork of [Stephanevg/New-Tattoo](/Stephanevg/New-Tattoo) intended to resolve some specific issues.  Do not consider this production code, and no warranty is implied.

## Usage
Information on how to use the original script can be found here --> [PowerShellDistrict/OSDTattoo](http://powershelldistrict.com/osd-tattoo-powershell/)

## SYNTAX

```powershell
  New-OSDTattoo.ps1 [-WMI] [-Registry] [-EnvironmentVariable] [-All] [-Root <string>] [-Prefix <string>] [-Variables <string\[]>]
```

## PARAMETERS
**-WMI** <SwitchParameter>
Creates and populates a WMI Class with the collected information.  Creates a WMI Class `root\wimv2\[$root]`.  If $root is undefined, defaults to OSDBuildInfo, eg:
> root\wimv2\OSDBuildInfo

**-Registry** <SwitchParameter>
Creates and populates a Registry key with the collected information.  Creates a Registry key `HKLM:\Software\[$root]`.  If $root is undefined, defaults to OSDBuildInfo, eg:
> HKLM:\Software\OSDBuildInfo

**-EnvironmentVariable** <SwitchParameter>
Creates and populates system environment variables with the collected information.  Creates system-level Environment variables, one for each collected Task Sequence variable.  Ignores $root.

**-All** <SwitchParameter>
Shorthand for `-WMI` `-Registry` `-Environmentvariable`, ie: will create all three tattoo types.

**-Root** <String>
Specifies the $root variable to be used for the `-WMI` and `-Registry` options.  Default value: `OSBuildInfo`.

**-Prefix** <String>
Specifies the prefix which will be used to select Task Sequence variables for collection.  For example, `-prefix "Foo"` will match (and return) the variables `Foo_OSDVariable` and `FooOSDVariable` but not `Bar_OSDVariable`.  Default value: `PSDistrict`

**-Variables** <String[]>
Defines extra variables which will be matched along with those found by `-prefix`.  For example, `-prefix "Foo" -variables @("Bar_OSDVariable")` would match (and return) the variables `Foo_OSDVariable` and `FooOSDVariable` as well as `Bar_OSDVariable`.  Default value: empty.


## Getting help

User the following command to get help:

```powershell

get-help New-OSDTattoo.ps1

```
