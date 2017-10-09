---
title: "aaaDeploy une machine virtuelle avec un certificat stocké en toute sécurité sur la pile de Azure | Documents Microsoft"
description: "Découvrez comment toodeploy une machine virtuelle et envoyé un certificat sur celui-ci à l’aide d’une clé de coffre dans la pile de Azure"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 46590eb1-1746-4ecf-a9e5-41609fde8e89
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/03/2017
ms.author: sngun
ms.openlocfilehash: b5fa0a502ba582e10ff59b8af0568bf134d3d189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-and-include-certificate-retrieved-from-a-key-vault"></a>Créer une machine virtuelle et inclure un certificat récupéré à partir d’un coffre de clés

Cet article vous aide à toocreate une machine virtuelle dans la pile d’Azure et les certificats de push sur lui. 

## <a name="prerequisites"></a>Composants requis

* Les administrateurs de cloud Azure pile doivent avoir [créé une offre](azure-stack-create-offer.md) qui inclut le service de coffre de clés Azure hello.  
* Les utilisateurs doivent [s’abonner tooan offre](azure-stack-subscribe-plan-provision-vm.md) qui inclut le service de coffre de clés hello.  
* [Installer PowerShell pour Azure Stack.](azure-stack-powershell-install.md)  
* [Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell](azure-stack-powershell-configure-user.md)

Un coffre de clés dans la pile de Azure est utilisé toostore certificats. Les certificats sont utiles dans de nombreux scénarios différents. Prenons l’exemple d’un scénario selon lequel une machine virtuelle dans Azure Stack exécute une application qui a besoin d’un certificat. Ce certificat peut être utilisé pour le chiffrement, pour l’authentification tooActive Active ou SSL sur un site Web. Des certificats hello dans un coffre de clés vous permet de vous assurer qu’il est sécurisé.

Dans cet article, nous vous guident hello étapes toopush requis un certificat sur un ordinateur virtuel de Windows dans la pile de Azure. Vous pouvez utiliser ces étapes hello Kit de développement Azure pile ou à partir d’un client externe Windows si vous êtes connecté via VPN.

hello processus requis toopush un certificat sur l’ordinateur virtuel de hello décrire les Hello comme suit :

1. Créer un secret Key Vault.
2. Fichier de mise à jour hello azuredeploy.parameters.json.
3. Déployer le modèle de hello

## <a name="create-a-key-vault-secret"></a>Créer un secret Key Vault

Hello script suivant crée un certificat au format .pfx de hello, crée un coffre de clés et stocke le certificat de hello dans le coffre de clés hello en tant que secret. Vous devez utiliser hello `-EnabledForDeployment` paramètre quand vous créez un coffre de clés hello. Ce paramètre permet de s’assurer de que ce coffre de clés hello peut être référencé à partir de modèles Azure Resource Manager.

```powershell

# Create a certificate in hello .pfx format
New-SelfSignedCertificate `
  -certstorelocation cert:\LocalMachine\My `
  -dnsname contoso.microsoft.com

$pwd = ConvertTo-SecureString `
  -String "<Password used tooexport hello certificate>" `
  -Force `
  -AsPlainText

Export-PfxCertificate `
  -cert "cert:\localMachine\my\<Certificate Thumbprint that was created in hello previous step>" `
  -FilePath "<Fully qualified path where hello exported certificate can be stored>" `
  -Password $pwd

# Create a key vault and upload hello certificate into hello key vault as a secret
$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "servicecert"
$fileName = "<Fully qualified path where hello exported certificate can be stored>"
$certPassword = "<Password used tooexport hello certificate>"

$fileContentBytes = get-content $fileName `
  -Encoding Byte

$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
$jsonObject = @"
{
"data": "$filecontentencoded",
"dataType" :"pfx",
"password": "$certPassword"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location `
  -sku standard `
  -EnabledForDeployment

$secret = ConvertTo-SecureString `
  -String $jsonEncoded `
  -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
   -SecretValue $secret

```

Lorsque vous exécutez le script précédent de hello, sortie de hello inclut le secret hello URI. Notez cet URI. Vous avez tooreference dans hello [Push certificat tooWindows modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows). Télécharger hello [modèle de machine virtuelle push certificat windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) dossier sur votre ordinateur de développement. Ce dossier contient hello `azuredeploy.json` et `azuredeploy.parameters.json` fichiers dont vous aurez besoin dans les étapes suivantes hello.

Modifier hello `azuredeploy.parameters.json` fichier selon des valeurs d’environnement tooyour. paramètres de Hello un intérêt particulier sont le nom de coffre hello, groupe de ressources de coffre hello et le secret de hello URI (tel que généré par le script précédent de hello). Hello, le fichier suivant est un exemple d’un fichier de paramètres :

## <a name="update-hello-azuredeployparametersjson-file"></a>Fichier de mise à jour hello azuredeploy.parameters.json

Mettre à jour fichier azuredeploy.parameters.json de hello hello coffre, URI secret, VmName et autres valeurs en fonction de votre environnement. Hello fichier JSON suivant illustre un exemple de fichier de paramètres de modèle hello : 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "newStorageAccountName": {
      "value": "kvstorage01"
    },
    "vmName": {
      "value": "VM1"
    },
    "vmSize": {
      "value": "Standard_D1_v2"
    },
    "adminUserName": {
      "value": "demouser"
    },
    "adminPassword": {
      "value": "demouser@123"
    },
    "vaultName": {
      "value": "contosovault"
    },
    "vaultResourceGroup": {
      "value": "contosovaultrg"
    },
    "secretUrlWithVersion": {
      "value": "https://testkv001.vault.local.azurestack.external/secrets/testcert002/82afeeb84f4442329ce06593502e7840"
    }
  }
}
```

## <a name="deploy-hello-template"></a>Déployer le modèle de hello

Maintenant déployer le modèle de hello en utilisant hello PowerShell script suivant :

```powershell
# Deploy a Resource Manager template toocreate a VM and push hello secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```

Lorsque le modèle de hello est déployée avec succès, il en résulte hello suivant de sortie :

![Sortie du déploiement](media\azure-stack-kv-push-secret-into-vm/deployment-output.png)

Lorsque cet ordinateur virtuel est déployé, la pile de Azure exécute un push de certificat hello sur l’ordinateur virtuel de hello. Dans Windows, les certificats hello sont ajouté toohello LocalMachine emplacement de certificat, avec le certificat de hello stocker cet utilisateur hello fourni. Sous Linux, certificat de hello est placé sous le répertoire de /var/lib/waagent hello, avec le nom de fichier hello &lt;UppercaseThumbprint&gt;.crt hello X509 fichier de certificat et &lt;UppercaseThumbprint&gt;.prv pour hello clé privée.

## <a name="retire-certificates"></a>Mettre hors service des certificats

Bonjour précédant la section, nous vous a montré comment toopush un nouveau certificat sur un ordinateur virtuel. Votre ancien certificat est toujours sur l’ordinateur virtuel de hello, et il ne peut pas être supprimé. Toutefois, vous pouvez désactiver hello ancienne version de code secret hello à l’aide de hello `Set-AzureKeyVaultSecretAttribute` applet de commande. Hello Voici un exemple d’utilisation de cette applet de commande. Créer un nom du coffre que tooreplace hello, nom secret et selon l’environnement de tooyour les valeurs de version :

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a>Étapes suivantes

* [Déployer une machine virtuelle avec un mot de passe Key Vault](azure-stack-kv-deploy-vm-with-secret.md)
* [Autoriser un tooaccess application coffre de clés](azure-stack-kv-sample-app.md)


