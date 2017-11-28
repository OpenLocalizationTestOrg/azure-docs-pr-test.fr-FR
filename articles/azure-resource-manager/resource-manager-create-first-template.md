---
title: "modèle Azure Resource Manager de la première aaaCreate | Documents Microsoft"
description: "Un guide pas à pas de toocreating votre premier modèle Azure Resource Manager. Il vous montre comment toouse hello référence de modèle pour un modèle de stockage compte toocreate hello."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="8bba0-104">Créer et déployer votre premier modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8bba0-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="8bba0-105">Cette rubrique vous guide tout au long des étapes de hello de création de votre premier modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8bba0-105">This topic walks you through hello steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="8bba0-106">Modèles du Gestionnaire de ressources sont des fichiers JSON qui définissent les ressources hello nécessaires toodeploy pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="8bba0-106">Resource Manager templates are JSON files that define hello resources you need toodeploy for your solution.</span></span> <span data-ttu-id="8bba0-107">concepts de hello toounderstand associés au déploiement et la gestion de vos solutions Azure, consultez [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8bba0-107">toounderstand hello concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="8bba0-108">Si vous disposez de ressources et que vous souhaitez tooget un modèle pour ces ressources, consultez [exporter un modèle Azure Resource Manager à partir de ressources existants](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="8bba0-108">If you have existing resources and want tooget a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="8bba0-109">toocreate et modifier des modèles, vous avez besoin d’éditeur JSON.</span><span class="sxs-lookup"><span data-stu-id="8bba0-109">toocreate and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="8bba0-110">[Visual Studio Code](https://code.visualstudio.com/) est un éditeur de code multiplateforme, open source et léger.</span><span class="sxs-lookup"><span data-stu-id="8bba0-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="8bba0-111">Nous vous recommandons vivement d’utiliser Visual Studio Code pour créer des modèles Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8bba0-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="8bba0-112">Cette rubrique suppose que vous utilisez VS Code ; toutefois, si vous disposez d’un autre éditeur JSON (tel que Visual Studio), vous pouvez utiliser cet éditeur.</span><span class="sxs-lookup"><span data-stu-id="8bba0-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bba0-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8bba0-113">Prerequisites</span></span>

* <span data-ttu-id="8bba0-114">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8bba0-114">Visual Studio Code.</span></span> <span data-ttu-id="8bba0-115">Si nécessaire, installez-le à partir de [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="8bba0-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="8bba0-116">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8bba0-116">An Azure subscription.</span></span> <span data-ttu-id="8bba0-117">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="8bba0-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="8bba0-118">Créer un modèle</span><span class="sxs-lookup"><span data-stu-id="8bba0-118">Create template</span></span>

<span data-ttu-id="8bba0-119">Commençons par un modèle simple qui déploie un abonnement de tooyour de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8bba0-119">Let's start with a simple template that deploys a storage account tooyour subscription.</span></span>

1. <span data-ttu-id="8bba0-120">Sélectionnez **Fichier** > **Nouveau fichier**.</span><span class="sxs-lookup"><span data-stu-id="8bba0-120">Select **File** > **New File**.</span></span> 

   ![Nouveau fichier](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="8bba0-122">Copiez et collez hello suivant la syntaxe JSON dans votre fichier :</span><span class="sxs-lookup"><span data-stu-id="8bba0-122">Copy and paste hello following JSON syntax into your file:</span></span>

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   <span data-ttu-id="8bba0-123">Les noms de compte de stockage ont plusieurs restrictions qui les rendent difficile tooset.</span><span class="sxs-lookup"><span data-stu-id="8bba0-123">Storage account names have several restrictions that make them difficult tooset.</span></span> <span data-ttu-id="8bba0-124">nom de Hello doit être comprise entre 3 et 24 caractères de longueur, utiliser uniquement des nombres et des lettres minuscules et doit être unique.</span><span class="sxs-lookup"><span data-stu-id="8bba0-124">hello name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="8bba0-125">le modèle précédent Hello utilise hello [uniqueString](resource-group-template-functions-string.md#uniquestring) toogenerate une valeur de hachage de la fonction.</span><span class="sxs-lookup"><span data-stu-id="8bba0-125">hello preceding template uses hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function toogenerate a hash value.</span></span> <span data-ttu-id="8bba0-126">valeur de ce hachage toogive plus ce qui signifie que, il ajoute le préfixe de hello *stockage*.</span><span class="sxs-lookup"><span data-stu-id="8bba0-126">toogive this hash value more meaning, it adds hello prefix *storage*.</span></span> 

3. <span data-ttu-id="8bba0-127">Enregistrez ce fichier sous **azuredeploy.json** tooa les dossier local.</span><span class="sxs-lookup"><span data-stu-id="8bba0-127">Save this file as **azuredeploy.json** tooa local folder.</span></span>

   ![Enregistrer un modèle](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="8bba0-129">Déployer un modèle</span><span class="sxs-lookup"><span data-stu-id="8bba0-129">Deploy template</span></span>

<span data-ttu-id="8bba0-130">Vous est prêt toodeploy ce modèle.</span><span class="sxs-lookup"><span data-stu-id="8bba0-130">You are ready toodeploy this template.</span></span> <span data-ttu-id="8bba0-131">Vous utilisez PowerShell ou CLI d’Azure toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8bba0-131">You use either PowerShell or Azure CLI toocreate a resource group.</span></span> <span data-ttu-id="8bba0-132">Ensuite, vous déployez un groupe de ressources de stockage compte toothat.</span><span class="sxs-lookup"><span data-stu-id="8bba0-132">Then, you deploy a storage account toothat resource group.</span></span>

* <span data-ttu-id="8bba0-133">Pour PowerShell, utilisez hello suivant les commandes à partir du dossier hello contenant hello modèle :</span><span class="sxs-lookup"><span data-stu-id="8bba0-133">For PowerShell, use hello following commands from hello folder containing hello template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="8bba0-134">Pour une installation locale de CLI d’Azure, utilisez hello suivant les commandes à partir du dossier hello contenant hello modèle :</span><span class="sxs-lookup"><span data-stu-id="8bba0-134">For a local installation of Azure CLI, use hello following commands from hello folder containing hello template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="8bba0-135">Lorsque le déploiement terminé, votre compte de stockage existe dans le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="8bba0-135">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="8bba0-136">Déployer le modèle à partir de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="8bba0-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="8bba0-137">Vous pouvez utiliser [Cloud Shell](../cloud-shell/overview.md) toorun hello CLI d’Azure des commandes pour le déploiement de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="8bba0-137">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="8bba0-138">Toutefois, vous devez d’abord charger votre modèle dans le partage de fichiers hello pour votre environnement Cloud.</span><span class="sxs-lookup"><span data-stu-id="8bba0-138">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="8bba0-139">Si vous n’avez pas utilisé Cloud Shell, consultez [Vue d’ensemble d’Azure Cloud Shell](../cloud-shell/overview.md) pour obtenir plus d’informations sur sa configuration.</span><span class="sxs-lookup"><span data-stu-id="8bba0-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="8bba0-140">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8bba0-140">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="8bba0-141">Sélectionnez votre groupe de ressources Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="8bba0-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="8bba0-142">modèle de nom Hello est `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="8bba0-142">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Sélection du groupe de ressources](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="8bba0-144">Sélectionnez le compte de stockage hello pour votre environnement Cloud.</span><span class="sxs-lookup"><span data-stu-id="8bba0-144">Select hello storage account for your Cloud Shell.</span></span>

   ![Sélectionner le compte de stockage](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="8bba0-146">Sélectionnez **Fichiers**.</span><span class="sxs-lookup"><span data-stu-id="8bba0-146">Select **Files**.</span></span>

   ![Sélectionner des fichiers](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="8bba0-148">Sélectionnez le partage de fichiers de hello pour Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="8bba0-148">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="8bba0-149">modèle de nom Hello est `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="8bba0-149">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Sélectionner le partage de fichiers](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="8bba0-151">Sélectionnez **Ajouter un répertoire**.</span><span class="sxs-lookup"><span data-stu-id="8bba0-151">Select **Add directory**.</span></span>

   ![Ajouter un répertoire](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="8bba0-153">Nommez-le **modèles** puis sélectionnez **Ok**.</span><span class="sxs-lookup"><span data-stu-id="8bba0-153">Name it **templates**, and select **Okay**.</span></span>

   ![Nommer le répertoire](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="8bba0-155">Sélectionnez votre nouveau répertoire.</span><span class="sxs-lookup"><span data-stu-id="8bba0-155">Select your new directory.</span></span>

   ![Sélectionner le répertoire](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="8bba0-157">Sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="8bba0-157">Select **Upload**.</span></span>

   ![Sélectionner Télécharger](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="8bba0-159">Recherchez et chargez votre modèle.</span><span class="sxs-lookup"><span data-stu-id="8bba0-159">Find and upload your template.</span></span>

   ![Charger le fichier](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="8bba0-161">Invite de commandes ouverte hello.</span><span class="sxs-lookup"><span data-stu-id="8bba0-161">Open hello prompt.</span></span>

   ![Ouvrir Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="8bba0-163">Entrez hello suivant les commandes Bonjour Cloud Shell :</span><span class="sxs-lookup"><span data-stu-id="8bba0-163">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="8bba0-164">Lorsque le déploiement terminé, votre compte de stockage existe dans le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="8bba0-164">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="customize-hello-template"></a><span data-ttu-id="8bba0-165">Personnaliser le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="8bba0-165">Customize hello template</span></span>

<span data-ttu-id="8bba0-166">modèle de Hello fonctionne correctement, mais il n’est pas flexible.</span><span class="sxs-lookup"><span data-stu-id="8bba0-166">hello template works fine, but it is not flexible.</span></span> <span data-ttu-id="8bba0-167">Il déploie toujours un tooSouth stockage localement redondant du centre des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="8bba0-167">It always deploys a locally redundant storage tooSouth Central US.</span></span> <span data-ttu-id="8bba0-168">nom de Hello est toujours *stockage* suivie d’une valeur de hachage.</span><span class="sxs-lookup"><span data-stu-id="8bba0-168">hello name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="8bba0-169">tooenable à l’aide du modèle de hello pour différents scénarios, ajouter un modèle de toohello de paramètres.</span><span class="sxs-lookup"><span data-stu-id="8bba0-169">tooenable using hello template for different scenarios, add parameters toohello template.</span></span>

<span data-ttu-id="8bba0-170">Hello suivant montre section de paramètres hello avec deux paramètres.</span><span class="sxs-lookup"><span data-stu-id="8bba0-170">hello following example shows hello parameters section with two parameters.</span></span> <span data-ttu-id="8bba0-171">premier paramètre de Hello `storageSKU` vous permet de type hello de toospecify de redondance.</span><span class="sxs-lookup"><span data-stu-id="8bba0-171">hello first parameter `storageSKU` enables you toospecify hello type of redundancy.</span></span> <span data-ttu-id="8bba0-172">Elle limite les valeurs hello que toovalues qui sont valides pour un compte de stockage, vous pouvez passer.</span><span class="sxs-lookup"><span data-stu-id="8bba0-172">It limits hello values you can pass in toovalues that are valid for a storage account.</span></span> <span data-ttu-id="8bba0-173">Il spécifie également une valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="8bba0-173">It also specifies a default value.</span></span> <span data-ttu-id="8bba0-174">Hello du deuxième paramètre `storageNamePrefix` est ensemble tooallow un maximum de 11 caractères.</span><span class="sxs-lookup"><span data-stu-id="8bba0-174">hello second parameter `storageNamePrefix` is set tooallow a maximum of 11 characters.</span></span> <span data-ttu-id="8bba0-175">Il spécifie une valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="8bba0-175">It specifies a default value.</span></span>

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="8bba0-176">Dans la section de variables hello, ajoutez une variable nommée `storageName`.</span><span class="sxs-lookup"><span data-stu-id="8bba0-176">In hello variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="8bba0-177">Il combine la valeur de préfixe hello à partir des paramètres de hello et une valeur de hachage à partir de hello [uniqueString](resource-group-template-functions-string.md#uniquestring) (fonction).</span><span class="sxs-lookup"><span data-stu-id="8bba0-177">It combines hello prefix value from hello parameters and a hash value from hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="8bba0-178">Il utilise hello [toLower](resource-group-template-functions-string.md#tolower) fonction tooconvert tous les caractères toolowercase.</span><span class="sxs-lookup"><span data-stu-id="8bba0-178">It uses hello [toLower](resource-group-template-functions-string.md#tolower) function tooconvert all characters toolowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="8bba0-179">toouse ces nouvelles valeurs pour votre compte de stockage, modifiez la définition de ressource hello :</span><span class="sxs-lookup"><span data-stu-id="8bba0-179">toouse these new values for your storage account, change hello resource definition:</span></span>

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

<span data-ttu-id="8bba0-180">Notez que hello nom du compte de stockage hello a maintenant la valeur variable toohello que vous avez ajouté.</span><span class="sxs-lookup"><span data-stu-id="8bba0-180">Notice that hello name of hello storage account is now set toohello variable that you added.</span></span> <span data-ttu-id="8bba0-181">nom de référence (SKU) Hello est valeur toohello paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="8bba0-181">hello SKU name is set toohello value of hello parameter.</span></span> <span data-ttu-id="8bba0-182">emplacement de Hello a la valeur hello même emplacement que le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="8bba0-182">hello location is set hello same location as hello resource group.</span></span>

<span data-ttu-id="8bba0-183">Enregistrez votre fichier.</span><span class="sxs-lookup"><span data-stu-id="8bba0-183">Save your file.</span></span> 

<span data-ttu-id="8bba0-184">Après avoir effectué les étapes de hello dans cet article, votre modèle ressemble à :</span><span class="sxs-lookup"><span data-stu-id="8bba0-184">After completing hello steps in this article, your template now looks like:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a><span data-ttu-id="8bba0-185">Redéployer le modèle</span><span class="sxs-lookup"><span data-stu-id="8bba0-185">Redeploy template</span></span>

<span data-ttu-id="8bba0-186">Redéployez le modèle hello avec des valeurs différentes.</span><span class="sxs-lookup"><span data-stu-id="8bba0-186">Redeploy hello template with different values.</span></span>

<span data-ttu-id="8bba0-187">Pour PowerShell, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8bba0-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="8bba0-188">Pour l’interface de ligne de commande Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="8bba0-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="8bba0-189">Pour hello Cloud Shell, téléchargez votre partage de fichiers de modèle modifié toohello.</span><span class="sxs-lookup"><span data-stu-id="8bba0-189">For hello Cloud Shell, upload your changed template toohello file share.</span></span> <span data-ttu-id="8bba0-190">Remplacer le fichier existant de hello.</span><span class="sxs-lookup"><span data-stu-id="8bba0-190">Overwrite hello existing file.</span></span> <span data-ttu-id="8bba0-191">Ensuite, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8bba0-191">Then, use hello following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="8bba0-192">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="8bba0-192">Clean up resources</span></span>

<span data-ttu-id="8bba0-193">Lorsque vous n’est plus nécessaire, nettoyer les ressources hello que vous avez déployé par la suppression du groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="8bba0-193">When no longer needed, clean up hello resources you deployed by deleting hello resource group.</span></span>

<span data-ttu-id="8bba0-194">Pour PowerShell, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8bba0-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="8bba0-195">Pour l’interface de ligne de commande Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="8bba0-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="8bba0-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8bba0-196">Next steps</span></span>
* <span data-ttu-id="8bba0-197">toolearn en savoir plus sur la structure de hello d’un modèle, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8bba0-197">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="8bba0-198">toolearn sur les propriétés hello pour un compte de stockage, consultez [référence du modèle des comptes de stockage](/azure/templates/microsoft.storage/storageaccounts).</span><span class="sxs-lookup"><span data-stu-id="8bba0-198">toolearn about hello properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="8bba0-199">tooview des modèles complète pour divers types de solutions, consultez hello [modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="8bba0-199">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
