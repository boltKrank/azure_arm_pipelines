# azure_arm_pipelines

Testing of deploying ARM templates via Azure pipelines

## Goals

1. Deploy PE master via ARM and Azure pipelines
2. Deploy an agent to a Windows machine
3. Be able to see the STDOUT / status of the agent - to check if it's running, logs, etc.

## Command for deploying PE master

```shell
az group create --name "simonpuppet" --location "Australia East"
az deployment group create --resource-group "simonpuppet" --template-file azure_pe_master_deploy.json
az vm show --resource-group "simonpuppet" --name "simon-pe-puppet-vm" --show-details --query publicIps --output tsv
ssh -i id_rsa puppet@<ipaddress>
```

## Powershell for deploying PE master

```shell
New-AzResourceGroup -Name "simonpuppet" -Location "Australia East"
New-AzResourceGroupDeployment -Name ExampleDeployment `
  -ResourceGroupName "simonpuppet" `
  -TemplateFile azure_pe_master_deploy.json
```

## Command for cleaning up PE master (destroy!)

```shell
az group delete --name "simonpuppet"
```

## Powershell for cleaning up PE master (destroy!)

```shell
Remove-AzResourceGroup -Name ExampleResourceGroup
```
