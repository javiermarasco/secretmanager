Implementation

- [x] Create a keyvault
- [x] Create an SPN to handle the secrets of the keyvault
- [x] Grant permissions on the keyvault for the SPN
- [x] Create a GO package/module
- [x] Use environment variables to provide configuration to the CLI
  - [x] ClientID
  - [x] Secret
  - [x] TenantID
  - [x] VaultName
- [x] Inputs
  - [x] Path: "/infra/dev/cluster"
  - [x] SecretName: "Port"
  - [x] Value: "80"
- [ ] Tasks:
  - [x] Split path by "/" 
  - [x] Create tags depending on the path provided
    - [x] A: infra
    - [x] B: dev
    - [x] C: cluster
    - [x] SecretName: port
    - [x] Secret value --> Value(80)
  - [x] The name of the secret is a hash made by the combination of: (This will allow us to keep multiple versions of the same secret)
    - [x] all the tags + SecretName
  - [x] Write secrets
    - [x] Using arguments and flags from command line
  - [x] Read secrets
    - [x] Using arguments and flags from command line
  
AWS secrets manager
  - [x] Create IAM user
  - [ ] Assign the correct permissions to IAM User to handle secrets
    - [ ] secretsmanager:Name
    - [ ] secretsmanager:Description
    - [ ] secretsmanager:KmsKeyId
    - [ ] aws:RequestTag/${TagKey}
    - [ ] aws:ResourceTag/${TagKey}
    - [ ] aws:TagKeys
    - [ ] secretsmanager:ResourceTag/tag-key
    - [ ] secretsmanager:AddReplicaRegions
    - [ ] secretsmanager:ForceOverwriteReplicaSecret
    - [ ] resourcetypes: Secret*
    - [ ] secretsmanager:TagResource
    - [ ] secretsmanager:UntagResource
  - [ ] Learn how to create and delete secrets using GO SDK
  - [ ] Add support for tagging of secrets
    - Should I use tagresource? (https://docs.aws.amazon.com/secretsmanager/latest/apireference/API_TagResource.html)
    - Should I use untagresource? (https://docs.aws.amazon.com/secretsmanager/latest/apireference/API_UntagResource.html)
  - Information on what is returned as a secret from the SDK: (https://github.com/aws/aws-sdk-go-v2/blob/main/service/secretsmanager/types/types.go)
  - Repo with the SDK implementation (https://github.com/aws/aws-sdk-go-v2/tree/main/service/secretsmanager)

Add management for cloud providers:
 - Ideally the CLI should also be able to configure the needed "stuff" in the cloud provider to be used
   - In Azure create the SPN, assign it to the keyvault, grant permissions and retrieve the SPN clientid, secret, tenant (Also create a keyvault???)
   - In AWS Create the IAM, policy, assign the policy and retrieve the IAM id and secret (Also create the secrets manager?)

GCP secretmanager
  - [ ] TODO

EXTRAS:

- [ ] Ability to copy a secret from one platform to another (AWS to Azure, Azure to GCP, GCP to Azure, etc.)
- [ ] Ability to MIGRATE a secret from one platform to another (copy first then remove from origin)
- [ ] Add extra argument in the cli to specify which cloud provider to use (implement all the flags)
  - [ ] secretcli az read (to read a secret from azure)
  - [ ] secretcli aws read (to read a secret from aws)
  - [ ] secretcli gcp read (to read a secret from gcp)
- [ ] Help message 
  - [ ] Include all the flags and how to use them
  - [ ] Include an example of write and read a secret for each cloud provider
  - [ ] Include an explanation of the needed environment variables