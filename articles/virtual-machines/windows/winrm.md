---
title: "aaaSet d’accès WinRM pour une machine virtuelle Azure | Documents Microsoft"
description: "Configurer l’accès de WinRM pour une utilisation avec une machine virtuelle Azure créée dans le modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a>Configuration de l’accès WinRM pour les machines virtuelles dans Azure Resource Manager
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a>WinRM dans Azure Service Management par rapport à Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* Pour une vue d’ensemble de hello Azure Resource Manager, consultez ce [article](../../azure-resource-manager/resource-group-overview.md)
* Pour connaître les différences entre Azure Service Management et Azure Resource Manager, consultez cet [article](../../resource-manager-deployment-model.md)

Hello principale différence dans la définition de la configuration de WinRM entre deux piles de hello est ainsi les certificats hello obtient installées sur hello machine virtuelle. Dans la pile du Gestionnaire de ressources Azure hello, certificats de hello sont modélisées comme des ressources gérées par hello fournisseur de ressources de coffre de clé. Par conséquent, utilisateur de hello doit tooprovide leur propre certificat et téléchargez-le tooa le coffre de clés avant son utilisation dans une machine virtuelle.

Voici les étapes hello tooset tootake d’un ordinateur virtuel avec connectivité de WinRM

1. Créer un coffre de clés
2. Créer un certificat auto-signé
3. Télécharger votre coffre de tooKey un certificat auto-signé
4. Obtenir l’URL de hello pour votre certificat auto-signé dans le coffre de clés de hello
5. Référencer les URL de vos certificats auto-signés lors de la création d’une machine virtuelle

## <a name="step-1-create-a-key-vault"></a>Étape 1 : créer un coffre de clés
Vous pouvez utiliser hello ci-dessous commande toocreate hello coffre de clés

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a>Étape 2 : créer un certificat auto-signé
Vous pouvez créer un certificat auto-signé à l’aide de ce script PowerShell

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a>Étape 3 : Téléchargez votre coffre de clés de toohello un certificat auto-signé
Avant de télécharger hello certificat toohello le coffre de clés créé à l’étape 1, doit tooconverted dans un Bonjour format Microsoft.Compute comprendre de fournisseur de ressources. Hello PowerShell script ci-dessous permettra de que vous faire

```
$fileName = "<Path toohello .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a>Étape 4 : Obtenir l’URL de hello pour votre certificat auto-signé dans le coffre de clés de hello
fournisseur de ressources Microsoft.Compute Hello a besoin d’un secret de toohello URL à l’intérieur de hello coffre de clés lors de la configuration de machine virtuelle de hello. Cela permet la clé secrète fournisseur toodownload hello hello Microsoft.Compute ressource et que vous créez des certificat équivalent de hello sur hello machine virtuelle.

> [!NOTE]
> URL de Hello du secret de hello doit tooinclude hello version. Un exemple d’URL se présente comme suit https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve
> 
> 

#### <a name="templates"></a>Modèles
Vous pouvez obtenir l’URL de toohello de lien de hello dans le modèle hello à l’aide de hello code ci-dessous

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a>PowerShell
Vous pouvez obtenir cette URL à l’aide de hello ci-dessous la commande PowerShell

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a>Étape 5 : référencer les URL de vos certificats auto-signés lors de la création d’une machine virtuelle
#### <a name="azure-resource-manager-templates"></a>Modèles Azure Resource Manager
Lors de la création d’une machine virtuelle via des modèles, le certificat de hello est référencée dans les sections de secrets hello et hello winRM comme indiqué ci-dessous :

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

Un exemple de modèle pour hello ci-dessus trouverez ici [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)

Pour obtenir le code source pour ce modèle, consultez [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)

#### <a name="powershell"></a>PowerShell
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a>Étape 6 : Connexion toohello machine virtuelle
Avant de pouvoir connecter toohello machine virtuelle, vous devez toomake que votre ordinateur est configuré pour l’administration à distance via WinRM. Démarrer PowerShell en tant qu’administrateur et exécutez hello ci-dessous toomake de commande que vous êtes prêt.

    Enable-PSRemoting -Force

> [!NOTE]
> Vous devrez peut-être toomake que hello service WinRM est en cours d’exécution si hello ci-dessus ne fonctionne pas. Vous pouvez le faire à l’aide de `Get-Service WinRM`
> 
> 

Une fois que le programme d’installation hello est terminé, vous pouvez vous connecter à toohello machine virtuelle à l’aide de hello commande ci-dessous

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
