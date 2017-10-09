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
# <a name="use-key-vault-toopass-secure-parameter-value-during-deployment"></a><span data-ttu-id="bfe3a-103">Utiliser la valeur de paramètre secure toopass le coffre de clés pendant le déploiement</span><span class="sxs-lookup"><span data-stu-id="bfe3a-103">Use Key Vault toopass secure parameter value during deployment</span></span>

<span data-ttu-id="bfe3a-104">Lorsque vous devez toopass une valeur sûre (par exemple, un mot de passe) en tant que paramètre pendant le déploiement, vous pouvez récupérer la valeur hello un [Azure Key Vault](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bfe3a-104">When you need toopass a secure value (like a password) as a parameter during deployment, you can retrieve hello value from an [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="bfe3a-105">Vous récupérez la valeur de hello en référençant le coffre de clés hello et secret dans votre fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-105">You retrieve hello value by referencing hello key vault and secret in your parameter file.</span></span> <span data-ttu-id="bfe3a-106">valeur de Hello n’est jamais exposée parce que vous référencez uniquement son ID de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-106">hello value is never exposed because you only reference its key vault ID.</span></span> <span data-ttu-id="bfe3a-107">Vous n’avez pas besoin toomanually Entrez la valeur de hello pour secret de hello chaque fois que vous déployez des ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-107">You do not need toomanually enter hello value for hello secret each time you deploy hello resources.</span></span> <span data-ttu-id="bfe3a-108">coffre de clés Hello peut exister dans un autre abonnement à un groupe de ressources hello que vous effectuez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-108">hello key vault can exist in a different subscription than hello resource group you are deploying to.</span></span> <span data-ttu-id="bfe3a-109">Lorsque vous référencez un coffre de clés hello, vous incluez l’ID d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-109">When referencing hello key vault, you include hello subscription ID.</span></span>

<span data-ttu-id="bfe3a-110">Lorsque vous créez un coffre de clés hello, définissez hello *enabledForTemplateDeployment* propriété trop*true*.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-110">When creating hello key vault, set hello *enabledForTemplateDeployment* property too*true*.</span></span> <span data-ttu-id="bfe3a-111">En définissant cette valeur tootrue, vous autorisez l’accès à partir de modèles de gestionnaire de ressources pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-111">By setting this value tootrue, you permit access from Resource Manager templates during deployment.</span></span>  

## <a name="deploy-a-key-vault-and-secret"></a><span data-ttu-id="bfe3a-112">Déploiement d'un coffre de clés et d’une clé secrète</span><span class="sxs-lookup"><span data-stu-id="bfe3a-112">Deploy a key vault and secret</span></span>

<span data-ttu-id="bfe3a-113">toocreate un coffre de clés et la clé secrète, utilisez CLI d’Azure ou de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-113">toocreate a key vault and secret, use either Azure CLI or PowerShell.</span></span> <span data-ttu-id="bfe3a-114">Notez que ce coffre de clés hello est activé pour le déploiement d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-114">Notice that hello key vault is enabled for template deployment.</span></span> 

<span data-ttu-id="bfe3a-115">Pour l’interface de ligne de commande Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="bfe3a-115">For Azure CLI, use:</span></span>

```azurecli
vaultname={your-unique-vault-name}
password={password-value}

az group create --name examplegroup --location 'South Central US'
az keyvault create --name $vaultname --resource-group examplegroup --location 'South Central US' --enabled-for-template-deployment true
az keyvault secret set --vault-name $vaultname --name examplesecret --value $password
```

<span data-ttu-id="bfe3a-116">Pour PowerShell, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bfe3a-116">For PowerShell, use:</span></span>

```powershell
$vaultname = "{your-unique-vault-name}"
$password = "{password-value}"

New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
New-AzureRmKeyVault -VaultName $vaultname -ResourceGroupName examplegroup -Location "South Central US" -EnabledForTemplateDeployment
$secretvalue = ConvertTo-SecureString $password -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName $vaultname -Name "examplesecret" -SecretValue $secretvalue
```

## <a name="enable-access-toohello-secret"></a><span data-ttu-id="bfe3a-117">Activer le secret d’accès toohello</span><span class="sxs-lookup"><span data-stu-id="bfe3a-117">Enable access toohello secret</span></span>

<span data-ttu-id="bfe3a-118">Si vous utilisez un coffre de clés nouveau ou existant, assurez-vous que l’utilisateur hello déploiement hello modèle accès hello secret.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-118">Whether you are using a new key vault or an existing one, ensure that hello user deploying hello template can access hello secret.</span></span> <span data-ttu-id="bfe3a-119">utilisateur Hello déploiement d’un modèle qui fait référence à une clé secrète doit avoir hello `Microsoft.KeyVault/vaults/deploy/action` l’autorisation de coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-119">hello user deploying a template that references a secret must have hello `Microsoft.KeyVault/vaults/deploy/action` permission for hello key vault.</span></span> <span data-ttu-id="bfe3a-120">Hello [propriétaire](../active-directory/role-based-access-built-in-roles.md#owner) et [collaborateur](../active-directory/role-based-access-built-in-roles.md#contributor) rôles à la fois accordent cet accès.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-120">hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) and [Contributor](../active-directory/role-based-access-built-in-roles.md#contributor) roles both grant this access.</span></span> <span data-ttu-id="bfe3a-121">Vous pouvez également créer un [rôle personnalisé](../active-directory/role-based-access-control-custom-roles.md) qui accorde cette autorisation et ajouter le rôle toothat hello.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-121">You can also create a [custom role](../active-directory/role-based-access-control-custom-roles.md) that grants this permission and add hello user toothat role.</span></span> <span data-ttu-id="bfe3a-122">Pour plus d’informations sur l’ajout d’un rôle d’utilisateur tooa, consultez [affecter un utilisateur tooadministrator des rôles dans Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bfe3a-122">For information about adding a user tooa role, see [Assign a user tooadministrator roles in Azure Active Directory](../active-directory/active-directory-users-assign-role-azure-portal.md).</span></span>


## <a name="reference-a-secret-with-static-id"></a><span data-ttu-id="bfe3a-123">Référencement d’un secret avec un ID statique</span><span class="sxs-lookup"><span data-stu-id="bfe3a-123">Reference a secret with static ID</span></span>

<span data-ttu-id="bfe3a-124">modèle Hello reçoit un secret de coffre de clés est comme tout autre modèle.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-124">hello template that receives a key vault secret is like any other template.</span></span> <span data-ttu-id="bfe3a-125">C’est parce que **vous référencez le coffre de clés hello dans fichier de paramètres hello, pas les modèles hello.**</span><span class="sxs-lookup"><span data-stu-id="bfe3a-125">That's because **you reference hello key vault in hello parameter file, not hello template.**</span></span> <span data-ttu-id="bfe3a-126">Par exemple, hello suivant le modèle déploie une base de données SQL qui inclut un mot de passe administrateur.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-126">For example, hello following template deploys a SQL database that includes an administrator password.</span></span> <span data-ttu-id="bfe3a-127">paramètre de mot de passe Hello a la valeur chaîne sécurisée de tooa.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-127">hello password parameter is set tooa secure string.</span></span> <span data-ttu-id="bfe3a-128">Toutefois, modèle de hello ne spécifie pas d'où vient cette valeur.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-128">But, hello template does not specify where that value comes from.</span></span>

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

<span data-ttu-id="bfe3a-129">À présent, créez un fichier de paramètres pour hello précédant le modèle.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-129">Now, create a parameter file for hello preceding template.</span></span> <span data-ttu-id="bfe3a-130">Dans le fichier de paramètres hello, spécifier un paramètre qui correspond au nom hello du paramètre hello dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-130">In hello parameter file, specify a parameter that matches hello name of hello parameter in hello template.</span></span> <span data-ttu-id="bfe3a-131">Pour la valeur du paramètre hello, référencer hello secrète hello coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-131">For hello parameter value, reference hello secret from hello key vault.</span></span> <span data-ttu-id="bfe3a-132">Vous référencez le secret de hello en passant l’identificateur de ressource de hello du coffre de clés hello et nom hello du secret de hello.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-132">You reference hello secret by passing hello resource identifier of hello key vault and hello name of hello secret.</span></span> <span data-ttu-id="bfe3a-133">Dans l’exemple suivant de hello, secret de coffre de clés hello doit déjà exister, et vous fournir une valeur statique pour son ID de ressource.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-133">In hello following example, hello key vault secret must already exist, and you provide a static value for its resource ID.</span></span>

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

## <a name="reference-a-secret-with-dynamic-id"></a><span data-ttu-id="bfe3a-134">Référencement d’un secret avec un ID dynamique</span><span class="sxs-lookup"><span data-stu-id="bfe3a-134">Reference a secret with dynamic ID</span></span>

<span data-ttu-id="bfe3a-135">section précédente de Hello a montré comment toopass un ID de ressource statique pour la clé de hello secret de coffre.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-135">hello previous section showed how toopass a static resource ID for hello key vault secret.</span></span> <span data-ttu-id="bfe3a-136">Toutefois, dans certains scénarios, vous devez tooreference un secret de coffre de clés qui varie en fonction de déploiement en cours hello.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-136">However, in some scenarios, you need tooreference a key vault secret that varies based on hello current deployment.</span></span> <span data-ttu-id="bfe3a-137">Dans ce cas, vous ne pouvez pas coder en dur hello les ID de ressource dans le fichier de paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-137">In that case, you cannot hard-code hello resource ID in hello parameters file.</span></span> <span data-ttu-id="bfe3a-138">Malheureusement, vous ne peut pas générer dynamiquement des ID de ressource hello dans le fichier de paramètres hello car les expressions de modèle ne sont pas autorisées dans le fichier de paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-138">Unfortunately, you cannot dynamically generate hello resource ID in hello parameters file because template expressions are not permitted in hello parameters file.</span></span>

<span data-ttu-id="bfe3a-139">toodynamically générer ID de ressource de hello pour un secret de coffre de clés, vous devez déplacer les ressources hello dont a besoin de la clé secrète de hello dans un modèle imbriqué.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-139">toodynamically generate hello resource ID for a key vault secret, you must move hello resource that needs hello secret into a nested template.</span></span> <span data-ttu-id="bfe3a-140">Dans votre modèle principal, vous ajoutez les modèles imbriqués hello et passez dans un paramètre qui contient l’ID de ressource hello générée de façon dynamique.</span><span class="sxs-lookup"><span data-stu-id="bfe3a-140">In your master template, you add hello nested template and pass in a parameter that contains hello dynamically generated resource ID.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bfe3a-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bfe3a-141">Next steps</span></span>
* <span data-ttu-id="bfe3a-142">Pour obtenir des informations générales sur les coffres de clés, consultez [Prise en main d’Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bfe3a-142">For general information about key vaults, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>
* <span data-ttu-id="bfe3a-143">Pour obtenir des exemples complets de référencement de clés secrètes, consultez [Exemples de coffres de clés](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span><span class="sxs-lookup"><span data-stu-id="bfe3a-143">For complete examples of referencing key secrets, see [Key Vault examples](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).</span></span>

