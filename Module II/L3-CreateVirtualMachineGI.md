# AzureLearning
My Azure Learning and Tutorial


## Create a Windows VM using Resource Manager and PowerShell

# Original Article : [Click Here](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-ps-create/)


```
Get-AzureRmLocation | sort Location | Select Location
```

```
$locName = "centralus"
```
# Setup ResourceGroup
```
$rgName = "mygroup2"

New-AzureRmResourceGroup -Name $rgName -Location $locName
```
# Setup Storage Account
```
$stName = "mystorageaccountft"

Get-AzureRmStorageAccountNameAvailability $stName

$storageAcc = New-AzureRmStorageAccount -ResourceGroupName $rgName -Name $stName -SkuName "Standard_LRS" -Kind "Storage" -Location $locName
```
# Setup Networking
```
$subnetName = "mysubnet1"
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24


$vnetName = "myvnet1"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $locName -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet

$ipName = "myIPaddress1"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic


$nicName = "mynic1"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
```

#Setup Availibity Set
```
New-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name "AvailabilitySet01" -Location $locName
$AvailabilitySet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name "AvailabilitySet01"
```
#--------------------
# Setup Credentials 
```
$user = "youaretheadmin"
$password = 'Pa$$word$1'
$securePassword = ConvertTo-SecureString $password -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ($user, $securePassword)
```
#Using prompt

#$cred = Get-Credential -Message "Type the name and password of the local administrator account."
#--------------------

#TO get VM Sizes Available in the region
#Get-AzureRmVMSize -Location $locName|FT


#setup VM Configutation
```
$vmName = "myvm1"
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1" -AvailabilitySetID $AvailabilitySet.Id


$compName = "myvm1"
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $compName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
```
# Make sure you have validated the availability of the image [More Details](https://github.com/abhishekanand/AzureLearning/blob/master/Module%20II/FindAPublishedImage.md)
```
$vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"

```

```
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```
```
$blobPath = "vhds/"+$vmname+"_os.vhd"
$osDiskUri = $storageAcc.PrimaryEndpoints.Blob.ToString() + $blobPath
```
```
$osdiskName = $vmname+'_osDisk'
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osdiskName -VhdUri $osDiskUri -CreateOption fromImage
```
```
New-AzureRmVM -ResourceGroupName $rgName -Location $locName -VM $vm -Verbose -Debug
```
