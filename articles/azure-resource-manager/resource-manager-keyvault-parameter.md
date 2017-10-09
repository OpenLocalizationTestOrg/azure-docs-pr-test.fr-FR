---
title: "le secret de coffre aaaKey avec modèle Resource Manager | Documents Microsoft"
description: "Montre comment toopass une clé secrète à partir d’une clé de coffre en tant que paramètre pendant le déploiement."
services: azure-resource-manager,key-vault
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c582c144-4760-49d3-b793-a3e1e89128e2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 0bb7760c95b3b4ef34c9e5cc2e3421be56b5e5e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a>Utiliser la valeur de paramètre secure toopass le coffre de clés pendant le déploiement

Lorsque vous devez toopass une valeur sûre (par exemple, un mot de passe) en tant que paramètre pendant le déploiement, vous pouvez récupérer la valeur hello un [Azure Key Vault](../key-vault/key-vault-whatis.md). Vous récupérez la valeur de hello en référençant le coffre de clés hello et secret dans votre fichier de paramètres. valeur de Hello n’est jamais exposée parce que vous référencez uniquement son ID de coffre de clés. Vous n’avez pas besoin toomanually Entrez la valeur de hello pour secret de hello chaque fois que vous déployez des ressources de hello. coffre de clés Hello peut exister dans un autre abonnement à un groupe de ressources hello que vous effectuez le déploiement. Lorsque vous référencez un coffre de clés hello, vous incluez l’ID d’abonnement hello.

Lorsque vous créez un coffre de clés hello, définissez hello *enabledForTemplateDeployment* propriété trop*true*. En définissant cette valeur tootrue, vous autorisez l’accès à partir de modèles de gestionnaire de ressources pendant le déploiement.  

## <a name="deploy-a-key-vault-and-secret"></a>Déploiement d'un coffre de clés et d’une clé secrète

toocreate un coffre de clés et la clé secrète, utilisez CLI d’Azure ou de PowerShell. Notez que ce coffre de clés hello est activé pour le déploiement d’un modèle. 

Pour l’interface de ligne de commande Azure, consultez :

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

Pour PowerShell, utilisez la commande suivante :

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a>Activer le secret d’accès toohello

Si vous utilisez un coffre de clés nouveau ou existant, assurez-vous que l’utilisateur hello déploiement hello modèle accès hello secret. utilisateur Hello déploiement d’un modèle qui fait référence à une clé secrète doit avoir hello `Microsoft.KeyVault/vaults/deploy/action` l’autorisation de coffre de clés hello. Hello [propriétaire](../active-directory/role-based-access-built-in-roles.md#owner) et [collaborateur](../active-directory/role-based-access-built-in-roles.md#contributor) rôles à la fois accordent cet accès. Vous pouvez également créer un [rôle personnalisé](../active-directory/role-based-access-control-custom-roles.md) qui accorde cette autorisation et ajouter le rôle toothat hello. Pour plus d’informations sur l’ajout d’un rôle d’utilisateur tooa, consultez [affecter un utilisateur tooadministrator des rôles dans Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).


## <a name="reference-a-secret-with-static-id"></a>Référencement d’un secret avec un ID statique

modèle Hello reçoit un secret de coffre de clés est comme tout autre modèle. C’est parce que **vous référencez le coffre de clés hello dans fichier de paramètres hello, pas les modèles hello.** Par exemple, hello suivant le modèle déploie une base de données SQL qui inclut un mot de passe administrateur. paramètre de mot de passe Hello a la valeur chaîne sécurisée de tooa. Toutefois, modèle de hello ne spécifie pas d'où vient cette valeur.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "type": "string"
        },
        "administratorLoginPassword": {
            "type": "securestring"
        },
        "collation": {
            "type": "string"
        },
        "databaseName": {
            "type": "string"
        },
        "edition": {
            "type": "string"
        },
        "requestedServiceObjectiveId": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "maxSizeBytes": {
            "type": "string"
        },
        "serverName": {
            "type": "string"
        },
        "sampleName": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
        {
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "name": "[parameters('serverName')]",
            "properties": {
                "administratorLogin": "[parameters('administratorLogin')]",
                "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
                "version": "12.0"
            },
            "resources": [
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "[parameters('databaseName')]",
                    "properties": {
                        "collation": "[parameters('collation')]",
                        "edition": "[parameters('edition')]",
                        "maxSizeBytes": "[parameters('maxSizeBytes')]",
                        "requestedServiceObjectiveId": "[parameters('requestedServiceObjectiveId')]",
                        "sampleName": "[parameters('sampleName')]"
                    },
                    "type": "databases"
                },
                {
                    "apiVersion": "2014-04-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Sql/servers/', parameters('serverName'))]"
                    ],
                    "location": "[parameters('location')]",
                    "name": "AllowAllWindowsAzureIps",
                    "properties": {
                        "endIpAddress": "0.0.0.0",
                        "startIpAddress": "0.0.0.0"
                    },
                    "type": "firewallrules"
                }
            ],
            "type": "Microsoft.Sql/servers"
        }
    ]
}
```

À présent, créez un fichier de paramètres pour hello précédant le modèle. Dans le fichier de paramètres hello, spécifier un paramètre qui correspond au nom hello du paramètre hello dans le modèle de hello. Pour la valeur du paramètre hello, référencer hello secrète hello coffre de clés. Vous référencez le secret de hello en passant l’identificateur de ressource de hello du coffre de clés hello et nom hello du secret de hello. Dans l’exemple suivant de hello, secret de coffre de clés hello doit déjà exister, et vous fournir une valeur statique pour son ID de ressource.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "administratorLogin": {
            "value": "exampleadmin"
        },
        "administratorLoginPassword": {
            "reference": {
              "keyVault": {
                "id": "/subscriptions/{guid}/resourceGroups/examplegroup/providers/Microsoft.KeyVault/vaults/{vault-name}"
              },
              "secretName": "examplesecret"
            }
        },
        "collation": {
            "value": "SQL_Latin1_General_CP1_CI_AS"
        },
        "databaseName": {
            "value": "exampledb"
        },
        "edition": {
            "value": "Standard"
        },
        "location": {
            "value": "southcentralus"
        },
        "maxSizeBytes": {
            "value": "268435456000"
        },
        "requestedServiceObjectiveId": {
            "value": "455330e1-00cd-488b-b5fa-177c226f28b7"
        },
        "sampleName": {
            "value": ""
        },
        "serverName": {
            "value": "exampleserver"
        }
    }
}
```

## <a name="reference-a-secret-with-dynamic-id"></a>Référencement d’un secret avec un ID dynamique

section précédente de Hello a montré comment toopass un ID de ressource statique pour la clé de hello secret de coffre. Toutefois, dans certains scénarios, vous devez tooreference un secret de coffre de clés qui varie en fonction de déploiement en cours hello. Dans ce cas, vous ne pouvez pas coder en dur hello les ID de ressource dans le fichier de paramètres hello. Malheureusement, vous ne peut pas générer dynamiquement des ID de ressource hello dans le fichier de paramètres hello car les expressions de modèle ne sont pas autorisées dans le fichier de paramètres hello.

toodynamically générer ID de ressource de hello pour un secret de coffre de clés, vous devez déplacer les ressources hello dont a besoin de la clé secrète de hello dans un modèle imbriqué. Dans votre modèle principal, vous ajoutez les modèles imbriqués hello et passez dans un paramètre qui contient l’ID de ressource hello générée de façon dynamique.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "vaultName": {
        "type": "string"
      },
      "secretName": {
        "type": "string"
      }
    },
    "resources": [
    {
      "apiVersion": "2015-01-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newVM.json",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "reference": {
              "keyVault": {
                "id": "[concat(resourceGroup().id, '/providers/Microsoft.KeyVault/vaults/', parameters('vaultName'))]"
              },
              "secretName": "[parameters('secretName')]"
            }
          }
        }
      }
    }],
    "outputs": {}
}
```

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir des informations générales sur les coffres de clés, consultez [Prise en main d’Azure Key Vault](../key-vault/key-vault-get-started.md).
* Pour obtenir des exemples complets de référencement de clés secrètes, consultez [Exemples de coffres de clés](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).

