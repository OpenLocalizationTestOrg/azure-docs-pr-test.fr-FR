---
title: "Clé secrète de coffre de clés avec un modèle Resource Manager | Microsoft Docs"
description: "Montre comment passer une clé secrète à partir d’un coffre de clés en tant que paramètre lors du déploiement."
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
ms.openlocfilehash: 1ca72599e67e79d42a3d430dbb13e89ea7265334
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-key-vault-to-pass-secure-parameter-value-during-deployment"></a><span data-ttu-id="4709b-103">Utiliser Key Vault pour transmettre une valeur de paramètre sécurisée pendant le déploiement</span><span class="sxs-lookup"><span data-stu-id="4709b-103">Use Key Vault to pass secure parameter value during deployment</span></span>

<span data-ttu-id="4709b-104">Lorsque vous avez besoin de passer une valeur sécurisée (par exemple, un mot de passe) comme paramètre au cours du déploiement, vous pouvez récupérer la valeur à partir d’un coffre [Azure Key Vault](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4709b-104">When you need to pass a secure value (like a password) as a parameter during deployment, you can retrieve the value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="4709b-105">Vous récupérez la valeur en référençant le coffre de clés et la clé secrète dans votre fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="4709b-105">You retrieve the value by referencing the key vault and secret in your parameter file.</span></span> <span data-ttu-id="4709b-106">La valeur n’est jamais exposée, car vous référencez uniquement son ID de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="4709b-106">The value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="4709b-107">Il est inutile d’entrer manuellement la valeur de la clé secrète chaque fois que vous déployez les ressources.</span><span class="sxs-lookup"><span data-stu-id="4709b-107">You do not need to manually enter the value for the secret each time you deploy the resources.</span></span> <span data-ttu-id="4709b-108">Le coffre de clés peut exister dans un autre abonnement que le groupe de ressources sur lequel vous effectuez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="4709b-108">The key vault can exist in a different subscription than the resource group you are deploying to.</span></span> <span data-ttu-id="4709b-109">Lorsque vous référencez le coffre de clés, incluez l’ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="4709b-109">When referencing the key vault, you include the subscription ID.</span></span>

<span data-ttu-id="4709b-110">Lorsque vous créez le coffre de clés, définissez la propriété *enabledForTemplateDeployment* sur *true*.</span><span class="sxs-lookup"><span data-stu-id="4709b-110">When creating the key vault, set the *enabledForTemplateDeployment* property to *true*.</span></span> <span data-ttu-id="4709b-111">En définissant cette valeur sur true, vous autorisez l’accès depuis des modèles Resource Manager pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="4709b-111">By setting this value to true, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="4709b-112">Déploiement d'un coffre de clés et d’une clé secrète</span><span class="sxs-lookup"><span data-stu-id="4709b-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="4709b-113">Pour créer un coffre de clés et une clé secrète, utilisez l’interface de ligne de commande Azure CLI ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4709b-113">To create a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="4709b-114">Remarque : le coffre de clés est activé pour le déploiement du modèle.</span><span class="sxs-lookup"><span data-stu-id="4709b-114">Notice that the key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="4709b-115">Pour l’interface de ligne de commande Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="4709b-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="4709b-116">Pour PowerShell, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4709b-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-to-the-secret"></a><span data-ttu-id="4709b-117">Autoriser l’accès à la clé secrète</span><span class="sxs-lookup"><span data-stu-id="4709b-117">Enable access to the secret</span></span>

<span data-ttu-id="4709b-118">Que vous utilisiez un coffre de clés nouveau ou existant, vérifiez que l’utilisateur qui déploie le modèle peut accéder à la clé secrète.</span><span class="sxs-lookup"><span data-stu-id="4709b-118">Whether you are using a new key vault or an existing one, ensure that the user deploying the template can access the secret.</span></span> <span data-ttu-id="4709b-119">L’utilisateur déployant un modèle qui fait référence à une clé secrète doit avoir l’autorisation `Microsoft.KeyVault/vaults/deploy/action` pour le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="4709b-119">The user deploying a template that references a secret must have the `Microsoft.KeyVault/vaults/deploy/action` permission for the key vault.</span></span> <span data-ttu-id="4709b-120">Les rôles [propriétaire](../active-directory/role-based-access-built-in-roles.md#owner) et [contributeur](../active-directory/role-based-access-built-in-roles.md#contributor) accordent cet accès.</span><span class="sxs-lookup"><span data-stu-id="4709b-120">The [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="4709b-121">Vous pouvez également créer un [rôle personnalisé](../active-directory/role-based-access-control-custom-roles.md) qui accorde cette autorisation et ajouter l’utilisateur à ce rôle.</span><span class="sxs-lookup"><span data-stu-id="4709b-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add the user to that role.</span></span> <span data-ttu-id="4709b-122">Pour en savoir plus sur l’ajout d’un utilisateur à un rôle, voir [Affecter des rôles d’administrateur à un utilisateur dans Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4709b-122">For information about adding a user to a role, see [Assign a user to administrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="4709b-123">Référencement d’un secret avec un ID statique</span><span class="sxs-lookup"><span data-stu-id="4709b-123">Reference a secret with static ID</span></span>

<span data-ttu-id="4709b-124">Le modèle qui reçoit un secret de coffre de clés est similaire à n’importe quel modèle.</span><span class="sxs-lookup"><span data-stu-id="4709b-124">The template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="4709b-125">Ceci s’explique par le fait que **vous référencez le coffre de clés dans le fichier de paramètres, et non dans le modèle.**</span><span class="sxs-lookup"><span data-stu-id="4709b-125">That's because **you reference the key vault in the parameter file, not the template.**</span></span> <span data-ttu-id="4709b-126">Par exemple, le modèle suivant déploie une base de données SQL qui inclut un mot de passe administrateur.</span><span class="sxs-lookup"><span data-stu-id="4709b-126">For example, the following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="4709b-127">Le paramètre du mot de passe est défini sur une chaîne sécurisée.</span><span class="sxs-lookup"><span data-stu-id="4709b-127">The password parameter is set to a secure string.</span></span> <span data-ttu-id="4709b-128">Toutefois, le modèle ne spécifie pas d’où vient cette valeur.</span><span class="sxs-lookup"><span data-stu-id="4709b-128">But, the template does not specify where that value comes from.</span></span>

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

<span data-ttu-id="4709b-129">À présent, créez un fichier de paramètres pour le modèle précédent.</span><span class="sxs-lookup"><span data-stu-id="4709b-129">Now, create a parameter file for the preceding template.</span></span> <span data-ttu-id="4709b-130">Dans le fichier de paramètres, spécifiez un paramètre qui correspond au nom du paramètre dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="4709b-130">In the parameter file, specify a parameter that matches the name of the parameter in the template.</span></span> <span data-ttu-id="4709b-131">Pour la valeur du paramètre, référencez le secret du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="4709b-131">For the parameter value, reference the secret from the key vault.</span></span> <span data-ttu-id="4709b-132">Vous référencez la clé secrète en passant l'identificateur de ressource du coffre de clés et le nom de la clé secrète.</span><span class="sxs-lookup"><span data-stu-id="4709b-132">You reference the secret by passing the resource identifier of the key vault and the name of the secret.</span></span> <span data-ttu-id="4709b-133">Dans l’exemple suivant, la clé secrète du coffre de clés doit déjà exister, et vous définissez une valeur statique pour son ID de ressource.</span><span class="sxs-lookup"><span data-stu-id="4709b-133">In the following example, the key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

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

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="4709b-134">Référencement d’un secret avec un ID dynamique</span><span class="sxs-lookup"><span data-stu-id="4709b-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="4709b-135">La section précédente expliquait comment transmettre un ID de ressource statique pour la clé secrète du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="4709b-135">The previous section showed how to pass a static resource ID for the key vault secret.</span></span> <span data-ttu-id="4709b-136">Toutefois, dans certains scénarios, vous devez référencer une clé secrète de coffre de clés qui varie selon le déploiement actuel.</span><span class="sxs-lookup"><span data-stu-id="4709b-136">However, in some scenarios, you need to reference a key vault secret that varies based on the current deployment.</span></span> <span data-ttu-id="4709b-137">Dans ce cas, vous ne pouvez pas coder en dur l’ID de ressource dans le fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="4709b-137">In that case, you cannot hard-code the resource ID in the parameters file.</span></span> <span data-ttu-id="4709b-138">Malheureusement, vous ne pouvez pas générer dynamiquement l’ID de ressource dans le fichier de paramètres, car les expressions de modèle ne sont pas autorisées dans ce dernier.</span><span class="sxs-lookup"><span data-stu-id="4709b-138">Unfortunately, you cannot dynamically generate the resource ID in the parameters file because template expressions are not permitted in the parameters file.</span></span>

<span data-ttu-id="4709b-139">Pour générer dynamiquement l’ID de ressource pour une clé secrète de coffre de clés, vous devez déplacer la ressource qui a besoin de la clé secrète dans un modèle imbriqué.</span><span class="sxs-lookup"><span data-stu-id="4709b-139">To dynamically generate the resource ID for a key vault secret, you must move the resource that needs the secret into a nested template.</span></span> <span data-ttu-id="4709b-140">Dans votre modèle principal, vous ajoutez le modèle imbriqué et passez un paramètre qui contient l’ID de ressource généré dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="4709b-140">In your master template, you add the nested template and pass in a parameter that contains the dynamically generated resource ID.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4709b-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4709b-141">Next steps</span></span>
* <span data-ttu-id="4709b-142">Pour obtenir des informations générales sur les coffres de clés, consultez [Prise en main d’Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4709b-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="4709b-143">Pour obtenir des exemples complets de référencement de clés secrètes, consultez [Exemples de coffres de clés](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span><span class="sxs-lookup"><span data-stu-id="4709b-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

