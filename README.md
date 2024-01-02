# ContentLibrary

## Module Install Instructions:
Get module directories with:
- $Env:PSModulePath

Create folder "ContentLibrary" in correct path - i.e. "C:\Users\Administrator\Documents\WindowsPowerShell\Modules\ContentLibrary"

- Copy file ContentLibrary.psm1 to folder you just created
- Verify module is available: Get-Module -ListAvailable
- Install module: Import-module-name ContentLibrary


## Creating the OVF and Copying to Content Library
Before running a module, connect to API server and vCenter server:

```
Connect-VIServer -Server vc-l-01a.corp.local -User administrator@vsphere.local -Password XYZ
Connect-CISServer -Server vc-l-01a.corp.local -User administrator@vsphere.local -Password XYZ
```

Then to convert VM to OVF and put it in a Content Library:

```
New-OVF -SourceVMName "testVMsmall" -OVFName "testVMsmall-OVF-Template" -Description "test VM template" -LibraryName "template-master"
```

Then to copy the template from one Content Library to another:
```
Copy-ContentLibrary -SourceLibraryName "template-master" -DestinationLibraryName "template-regional" -DeleteSourceFile $false
```
