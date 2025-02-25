# Azure CLI commands
```
 az login
```
```
 az account show --output jsonc
```

  - **If you have multiple subscriptions then the following commands may be used to switch context.**
```
     az account list --output table
```
```
     az account set --subscription <subscriptionId> #set context of subscription
```
```
     az account show
```

  - **Register providers, some subscriptions do not have necessary resource provider enabled to use varios features, below example is for Microsoft.Insights provider**
  - Syntax [az provider register --namespace "provider_name"]
    ```
       az provider register --namespace Microsoft.Insights
    ```
    - to check registrationstion use:
      ```
       az provider show --namespace Microsoft.Insights --query registrationState --output tsv
      ```
     

## Create resource group using for loop 
### (In the below example 5 RGs are created named Hub,Spoke1,Spoke2,OnPrem and NVA)

    for rg in Hub Spoke1 Spoke2 OnPrem NVA 
    do az group create --location westeurope --name VDC-$rg
    done

## 3rd party services may need terms to accepted before creation, portal has the option for same, however, when deploying resources via code, this may need tobe done seperately.
### (Below example Cisco CSR 1000v EULA is accepted using CLI)

    for urn in $(az vm image list --all --publisher cisco --offer cisco-csr-1000v --sku 16_6 --query '[].urn' --output tsv)
    do az vm image accept-terms --urn $urn
    done
