# Azure_Key_Vault_Secrets
Use this task to download secrets, such as authentication keys, storage account keys, data encryption keys, .PFX files, and passwords from an Azure Key Vault instance. 

## Pipeline Requirements

This task requires the following parameters to be defined:

Parameters:

| Name  | Displayname | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | :-------------: | :-------------: | :-------------: | :-------------: | ------------- |
| azureSubscription | Azure subscription | String |  |  | Required | Select the service connection for the Azure subscription containing the Azure Key Vault instance, or create a new connection |
| KeyVaultName | Key vault | String |  |  | Required | The name of the Azure Key Vault that contains the secrets to download |
| SecretsFilter | Secrets filter | String | '*' |  | Required | Downloads secret names according to the entered value. The value can be the default value to download all secrets from the selected key vault, or a comma-separated list of secret names |
| RunAsPreJob | Make secrets available to whole job | boolean | false |  | Optional | Runs the task before the job execution begins. Exposes secrets to all tasks in the job, not just tasks that follow this one |

These parameters provide multiple use case options for the template, enable/disable flags for the utilization of different templates as per the requirements.


## Use Cases

You can directly call a particular template as per the requirement. for example: 

  ```yaml
  # azure-pipeline.yml
  resources:
  repositories:
    - repository: Template
      type: github
      name: your_username/Azure_Key_Vault_Secrets
      ref: <respective branch name>
      endpoint: 'githubServiceConnectioNname'

  steps:
  # passing the parameters
  - template: Azure_Key_Vault_Secrets.yml
    parameters:
      azureSubscription: ${{ parameters.azureSubscription }}
      KeyVaultName: ${{ parameters.KeyVaultName }}
      SecretsFilter: ${{ parameters.SecretsFilter }}
      RunAsPreJob: ${{ parameters.RunAsPreJob }}
        
  
Make sure to adjust the repository name, branch name, and parameter values according to your project's requirements.

  ```
