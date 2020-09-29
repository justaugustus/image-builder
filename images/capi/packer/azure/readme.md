# Use the VHD

There are two options:

1. Publish the image to the Azure Market Place.  See the steps in [stages.yaml](./.pipelines/stages.yaml)
2. Create an image and use the disk for provising a VM.

## Provision a VM with VHD

After creating a VHD, create a managed image using the url output from `make make build-azure-vhd-<image>` and use it to [create the VM](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/build-image-with-packer#create-a-vm-from-the-packer-image): 

```bash
az image create -n testvmimage -g cluster-api-images --os-type <Windows/Linux> --source <storage url for vhd file>
az vm create -n testvm --image testvmimage -g cluster-api-images
```

## Debugging packer scripts
There are several ways to debug packer scripts: https://www.packer.io/docs/other/debugging.html