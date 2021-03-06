How to install and configure Azure PowerShell:-

[ Microsoft Official Article](https://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/)

My Version  :
-------------------
Sanity Checks :- Brand New Machine - First Time installation  

```
# Check Basic Machine Info :-

Get-CimInstance Win32_OperatingSystem | Select-Object  Caption, InstallDate, ServicePackMajorVersion, OSArchitecture, BootDevice,  BuildNumber, LocalDateTime| FL

Caption                 : Microsoft Windows 10 Pro
InstallDate             : 4/4/2016 4:08:53 PM
ServicePackMajorVersion : 0
OSArchitecture          : 64-bit
BootDevice              : \Device\HarddiskVolume1
BuildNumber             : 10586
LocalDateTime           : 6/20/2016 3:26:53 PM

```



```
# Check Environment Path Variable : -

$env:Path
C:\Windows\system32;C:\Windows;C:\Windows\System32\Wbem;C:\Windows\System32\WindowsPowerShell\v1.0\

$env:PSModulePath
C:\Users\test\Documents\WindowsPowerShell\Modules;C:\Program Files\WindowsPowerShell\Modules;C:\Windows\system32\WindowsPowerShell\v1.0\Modules
```

To check is Azure PowerShell is already installed

```
 C:\Windows\system32> Get-Module -ListAvailable Azure*
```

### Installing Azure PowerShell from the PowerShell Gallery (ARM)

Install Azure PowerShell 1.3.0 or greater from the PowerShell Gallery using an elevated Windows PowerShell or PowerShell Integrated Scripting Environment (ISE) prompt using the following commands:

```
# Install the Azure Resource Manager modules from the PowerShell Gallery

PS C:\Windows\system32> Install-Module AzureRM

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet provider must be available in 'C:\Program
Files\PackageManagement\ProviderAssemblies' or 'C:\Users\aanan\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running 'Install-PackageProvider
 -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y

Untrusted repository
You are installing the modules from an untrusted repository. If you trust this repository, change its InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to
 install the modules from 'PSGallery'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): A
PS C:\Windows\system32>

```


To check is Azure PowerShell if Azure PowerShell is installed correctly.

In Windows Explorer
```
C:\Program Files\WindowsPowerShell\Modules
```
In PowerShell

```

PS C:\Windows\system32> Get-Module -ListAvailable Azure*


    Directory: C:\Program Files\WindowsPowerShell\Modules


ModuleType Version    Name
---------- -------    ----
Manifest   1.1.3      Azure.Storage
Script     1.5.0      AzureRM
Manifest   1.1.1      AzureRM.ApiManagement
Manifest   1.0.9      AzureRM.Automation
Manifest   1.0.9      AzureRM.Backup
Manifest   1.1.1      AzureRM.Batch
Manifest   1.0.3      AzureRM.Cdn
Manifest   1.3.1      AzureRM.Compute
Manifest   1.0.9      AzureRM.DataFactories
Manifest   1.1.1      AzureRM.DataLakeAnalytics
Manifest   1.0.9      AzureRM.DataLakeStore
Manifest   1.0.0      AzureRM.DevTestLabs
Manifest   1.0.9      AzureRM.Dns
Manifest   1.1.1      AzureRM.HDInsight
Manifest   1.0.9      AzureRM.Insights
Manifest   1.1.8      AzureRM.KeyVault
Manifest   1.0.5      AzureRM.LogicApp
Manifest   0.9.0      AzureRM.MachineLearning
Manifest   1.0.10     AzureRM.Network
Manifest   1.0.9      AzureRM.NotificationHubs
Manifest   1.0.9      AzureRM.OperationalInsights
Manifest   1.0.9      AzureRM.profile
Manifest   1.1.1      AzureRM.RecoveryServices
Manifest   1.0.1      AzureRM.RecoveryServices.Backup
Manifest   1.1.7      AzureRM.RedisCache
Manifest   2.0.0      AzureRM.Resources
Manifest   1.0.0      AzureRM.ServerManagement
Manifest   1.1.8      AzureRM.SiteRecovery
Manifest   1.0.9      AzureRM.Sql
Manifest   1.1.1      AzureRM.Storage
Manifest   1.0.9      AzureRM.StreamAnalytics
Manifest   1.0.9      AzureRM.Tags
Manifest   1.0.9      AzureRM.TrafficManager
Manifest   1.0.9      AzureRM.UsageAggregates
Manifest   1.1.1      AzureRM.Websites

```

#### Tips
* Installed AzureRM version is same as Azure PowerShell version.(In this case : 1.5.0)
* To check latest Released PowerShell Command : [Click Here](https://github.com/Azure/azure-powershell/blob/dev/ChangeLog.md)
