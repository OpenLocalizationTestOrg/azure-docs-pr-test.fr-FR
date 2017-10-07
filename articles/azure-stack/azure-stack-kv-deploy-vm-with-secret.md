---
title: "aaaDeploy une machine virtuelle avec un mot de passe stockée en toute sécurité sur la pile de Azure | Documents Microsoft"
description: "Découvrez comment toodeploy une machine virtuelle à l’aide d’un mot de passe stockés dans la pile d’Azure Key Vault"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 23322a49-fb7e-4dc2-8d0e-43de8cd41f80
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: sngun
ms.openlocfilehash: 368addc1dfc5b7adadd2151fbd6d354f7892eea5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-by-retrieving-hello-password-stored-in-a-key-vault"></a>Créer un ordinateur virtuel par la récupération de mot de passe hello stocké dans un coffre de clés

Lorsque vous avez besoin d’une valeur sûre comme un mot de passe de toopass durant le déploiement, vous pouvez stocker cette valeur en tant que secret dans un coffre de clés Azure pile et référencez-la dans les modèles Azure Resource Manager hello. Vous n’avez pas besoin de toomanually Entrez code secret hello chaque fois que vous déployez des ressources de hello, vous pouvez également spécifier les utilisateurs ou les principaux du service accès hello secret. 

Dans cet article, nous vous guident toodeploy requis de hello suit une machine virtuelle de Windows dans la pile de Azure par la récupération de mot de passe hello est stocké dans un coffre de clés. Par conséquent, un mot de passe hello n’est jamais placée en texte brut dans le fichier de paramètres de modèle hello. Vous pouvez utiliser ces étapes hello Kit de développement Azure pile ou d’un client externe si vous êtes connecté via VPN.

## <a name="prerequisites"></a>Composants requis

* Les administrateurs de cloud Azure pile doivent avoir [créé une offre](azure-stack-create-offer.md) qui inclut le service de coffre de clés Azure hello.  
* Les utilisateurs doivent [s’abonner tooan offre](azure-stack-subscribe-plan-provision-vm.md) qui inclut le service de coffre de clés hello.  
* [Installer PowerShell pour Azure Stack.](azure-stack-powershell-install.md)  
* [Configurer hello pile d’Azure PowerShell environnement utilisateur.](azure-stack-powershell-configure-user.md)

Hello étapes suivantes décrivent hello processus requis toocreate un ordinateur virtuel par la récupération de mot de passe hello stocké dans un coffre de clés :

1. Créer un secret Key Vault.
2. Fichier de mise à jour hello azuredeploy.parameters.json.
3. Déployer le modèle de hello.

## <a name="create-a-key-vault-secret"></a>Créer un secret Key Vault

Hello script suivant crée un coffre de clés et stocke un mot de passe dans le coffre de clés hello en tant que secret. Hello d’utilisation `-EnabledForDeployment` paramètre quand vous créez un coffre de clés hello. Ce paramètre permet de s’assurer de que ce coffre de clés hello peut être référencé à partir de modèles Azure Resource Manager.

```powershell

$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "MySecret"

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location
  -EnabledForTemplateDeployment

$secretValue = ConvertTo-SecureString -String '<Password for your virtual machine>' -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
  -SecretValue $secretValue

```

Lorsque vous exécutez le script précédent de hello, sortie de hello inclut le secret hello URI. Notez cet URI. Vous avez tooreference dans hello [machine virtuelle Windows de déployer avec mot de passe dans le modèle de coffre de clés](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password). Télécharger hello [101-vm--mot de passe sécurisé](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) dossier sur votre ordinateur de développement. Ce dossier contient hello `azuredeploy.json` et `azuredeploy.parameters.json` fichiers dont vous aurez besoin dans les étapes suivantes hello.

Modifier hello `azuredeploy.parameters.json` fichier selon des valeurs d’environnement tooyour. paramètres de Hello un intérêt particulier sont le nom de coffre hello, groupe de ressources de coffre hello et le secret de hello URI (tel que généré par le script précédent de hello). Hello, le fichier suivant est un exemple d’un fichier de paramètres :

## <a name="update-hello-azuredeployparametersjson-file"></a>Fichier de mise à jour hello azuredeploy.parameters.json

Mettre à jour les fichiers de azuredeploy.parameters.json hello avec hello KeyVault URI, secretName, adminUsername de valeurs de machine virtuelle hello conformément à votre environnement. Hello fichier JSON suivant illustre un exemple de fichier de paramètres de modèle hello : 

```json
{
    "$schema":  "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion":  "1.0.0.0",
    "parameters":  {
       "adminUsername":  {
         "value":  "demouser"
          },
         "adminPassword":  {
           "reference":  {
              "keyVault":  {
                "id":  "/subscriptions/xxxxxx/resourceGroups/RgKvPwd/providers/Microsoft.KeyVault/vaults/KvPwd"
                },
              "secretName":  "MySecret"
           }
         },
       "dnsLabelPrefix":  {
          "value":  "mydns123456"
        },
        "windowsOSVersion":  {
          "value":  "2016-Datacenter"
        }
    }
}

```

## <a name="template-deployment"></a>Déploiement de modèle

Maintenant déployer le modèle de hello en utilisant hello PowerShell script suivant :

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```
Lorsque le modèle de hello est déployée avec succès, il en résulte hello suivant de sortie :

![Sortie du déploiement](media\azure-stack-kv-deploy-vm-with-secret/deployment-output.png)


## <a name="next-steps"></a>Étapes suivantes
[Déployer un exemple d’application avec Key Vault](azure-stack-kv-sample-app.md)

[Déployer une machine virtuelle avec un certificat Key Vault](azure-stack-kv-push-secret-into-vm.md)

