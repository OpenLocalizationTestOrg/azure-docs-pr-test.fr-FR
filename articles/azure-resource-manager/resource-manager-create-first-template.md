---
title: "Créer le premier modèle Azure Resource Manager | Microsoft Docs"
description: "Guide pas à pas pour la création de votre premier modèle Azure Resource Manager. Ce guide montre comment utiliser la référence de modèle pour un compte de stockage afin de créer un modèle."
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
ms.openlocfilehash: 49086b51e2db1aebed45746306ae14b6f1feb631
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="36d9f-104">Créer et déployer votre premier modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="36d9f-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="36d9f-105">Cette rubrique vous guide tout au long des étapes de création de votre premier modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="36d9f-105">This topic walks you through the steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="36d9f-106">Les modèles Azure Resource Manager sont des fichiers JSON qui définissent les ressources nécessaires au déploiement de votre solution.</span><span class="sxs-lookup"><span data-stu-id="36d9f-106">Resource Manager templates are JSON files that define the resources you need to deploy for your solution.</span></span> <span data-ttu-id="36d9f-107">Pour comprendre les concepts associés au déploiement et à la gestion de vos solutions Azure, voir [Présentation d’Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="36d9f-107">To understand the concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="36d9f-108">Si vous disposez de ressources existantes et que vous souhaitez créer un modèle pour ces ressources, voir [Exporter un modèle Azure Resource Manager à partir de ressources existantes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="36d9f-108">If you have existing resources and want to get a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="36d9f-109">Pour créer et réviser des modèles, vous avez besoin d’un éditeur JSON.</span><span class="sxs-lookup"><span data-stu-id="36d9f-109">To create and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="36d9f-110">[Visual Studio Code](https://code.visualstudio.com/) est un éditeur de code multiplateforme, open source et léger.</span><span class="sxs-lookup"><span data-stu-id="36d9f-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="36d9f-111">Nous vous recommandons vivement d’utiliser Visual Studio Code pour créer des modèles Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="36d9f-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="36d9f-112">Cette rubrique suppose que vous utilisez VS Code ; toutefois, si vous disposez d’un autre éditeur JSON (tel que Visual Studio), vous pouvez utiliser cet éditeur.</span><span class="sxs-lookup"><span data-stu-id="36d9f-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36d9f-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="36d9f-113">Prerequisites</span></span>

* <span data-ttu-id="36d9f-114">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="36d9f-114">Visual Studio Code.</span></span> <span data-ttu-id="36d9f-115">Si nécessaire, installez-le à partir de [https://code.visualstudio.com/](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="36d9f-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="36d9f-116">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="36d9f-116">An Azure subscription.</span></span> <span data-ttu-id="36d9f-117">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="36d9f-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="36d9f-118">Créer un modèle</span><span class="sxs-lookup"><span data-stu-id="36d9f-118">Create template</span></span>

<span data-ttu-id="36d9f-119">Commençons avec un modèle simple qui déploie un compte de stockage sur votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="36d9f-119">Let's start with a simple template that deploys a storage account to your subscription.</span></span>

1. <span data-ttu-id="36d9f-120">Sélectionnez **Fichier** > **Nouveau fichier**.</span><span class="sxs-lookup"><span data-stu-id="36d9f-120">Select **File** > **New File**.</span></span> 

   ![Nouveau fichier](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="36d9f-122">Copiez et collez la syntaxe JSON suivante dans votre fichier :</span><span class="sxs-lookup"><span data-stu-id="36d9f-122">Copy and paste the following JSON syntax into your file:</span></span>

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

   <span data-ttu-id="36d9f-123">Les noms de compte de stockage ont de nombreuses restrictions qui rendent leur définition plus difficile.</span><span class="sxs-lookup"><span data-stu-id="36d9f-123">Storage account names have several restrictions that make them difficult to set.</span></span> <span data-ttu-id="36d9f-124">Le nom doit comprendre entre 3 et 24 caractères, comporter uniquement des lettres en minuscules et des nombres, et être unique.</span><span class="sxs-lookup"><span data-stu-id="36d9f-124">The name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="36d9f-125">Le modèle précédent utilise la fonction [uniqueString](resource-group-template-functions-string.md#uniquestring) pour générer une valeur de hachage.</span><span class="sxs-lookup"><span data-stu-id="36d9f-125">The preceding template uses the [uniqueString](resource-group-template-functions-string.md#uniquestring) function to generate a hash value.</span></span> <span data-ttu-id="36d9f-126">Pour donner plus de sens à cette valeur de hachage, il ajoute le préfixe *stockage*.</span><span class="sxs-lookup"><span data-stu-id="36d9f-126">To give this hash value more meaning, it adds the prefix *storage*.</span></span> 

3. <span data-ttu-id="36d9f-127">Enregistrez ce fichier sous **azuredeploy.json** dans un dossier local.</span><span class="sxs-lookup"><span data-stu-id="36d9f-127">Save this file as **azuredeploy.json** to a local folder.</span></span>

   ![Enregistrer un modèle](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="36d9f-129">Déployer un modèle</span><span class="sxs-lookup"><span data-stu-id="36d9f-129">Deploy template</span></span>

<span data-ttu-id="36d9f-130">Vous êtes prêt à déployer ce modèle.</span><span class="sxs-lookup"><span data-stu-id="36d9f-130">You are ready to deploy this template.</span></span> <span data-ttu-id="36d9f-131">Vous utilisez soit PowerShell, soit Azure CLI pour créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="36d9f-131">You use either PowerShell or Azure CLI to create a resource group.</span></span> <span data-ttu-id="36d9f-132">Vous déployez ensuite un compte de stockage dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="36d9f-132">Then, you deploy a storage account to that resource group.</span></span>

* <span data-ttu-id="36d9f-133">Pour PowerShell, utilisez les commandes suivantes à partir du dossier qui contient le modèle :</span><span class="sxs-lookup"><span data-stu-id="36d9f-133">For PowerShell, use the following commands from the folder containing the template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="36d9f-134">Pour une installation locale d’Azure CLI, utilisez les commandes suivantes à partir du dossier qui contient le modèle :</span><span class="sxs-lookup"><span data-stu-id="36d9f-134">For a local installation of Azure CLI, use the following commands from the folder containing the template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="36d9f-135">Une fois le déploiement terminé, votre compte de stockage existe dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="36d9f-135">When deployment finishes, your storage account exists in the resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="36d9f-136">Déployer le modèle à partir de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="36d9f-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="36d9f-137">Vous pouvez utiliser [Cloud Shell](../cloud-shell/overview.md) pour exécuter les commandes Azure CLI pour le déploiement de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="36d9f-137">You can use [Cloud Shell](../cloud-shell/overview.md) to run the Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="36d9f-138">Toutefois, vous devez d’abord charger votre modèle dans le partage de fichiers de votre Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="36d9f-138">However, you must first load your template into the file share for your Cloud Shell.</span></span> <span data-ttu-id="36d9f-139">Si vous n’avez pas utilisé Cloud Shell, consultez [Vue d’ensemble d’Azure Cloud Shell](../cloud-shell/overview.md) pour obtenir plus d’informations sur sa configuration.</span><span class="sxs-lookup"><span data-stu-id="36d9f-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="36d9f-140">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36d9f-140">Log in to the [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="36d9f-141">Sélectionnez votre groupe de ressources Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="36d9f-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="36d9f-142">Le modèle de nom est `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="36d9f-142">The name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Sélection du groupe de ressources](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="36d9f-144">Sélectionnez le compte de stockage de votre Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="36d9f-144">Select the storage account for your Cloud Shell.</span></span>

   ![Sélectionner le compte de stockage](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="36d9f-146">Sélectionnez **Fichiers**.</span><span class="sxs-lookup"><span data-stu-id="36d9f-146">Select **Files**.</span></span>

   ![Sélectionner des fichiers](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="36d9f-148">Sélectionnez le partage de fichiers pour Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="36d9f-148">Select the file share for Cloud Shell.</span></span> <span data-ttu-id="36d9f-149">Le modèle de nom est `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="36d9f-149">The name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Sélectionner le partage de fichiers](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="36d9f-151">Sélectionnez **Ajouter un répertoire**.</span><span class="sxs-lookup"><span data-stu-id="36d9f-151">Select **Add directory**.</span></span>

   ![Ajouter un répertoire](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="36d9f-153">Nommez-le **modèles** puis sélectionnez **Ok**.</span><span class="sxs-lookup"><span data-stu-id="36d9f-153">Name it **templates**, and select **Okay**.</span></span>

   ![Nommer le répertoire](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="36d9f-155">Sélectionnez votre nouveau répertoire.</span><span class="sxs-lookup"><span data-stu-id="36d9f-155">Select your new directory.</span></span>

   ![Sélectionner le répertoire](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="36d9f-157">Sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="36d9f-157">Select **Upload**.</span></span>

   ![Sélectionner Télécharger](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="36d9f-159">Recherchez et chargez votre modèle.</span><span class="sxs-lookup"><span data-stu-id="36d9f-159">Find and upload your template.</span></span>

   ![Charger le fichier](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="36d9f-161">Ouvrez l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="36d9f-161">Open the prompt.</span></span>

   ![Ouvrir Cloud Shell](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="36d9f-163">Entrez les commandes suivantes dans Cloud Shell :</span><span class="sxs-lookup"><span data-stu-id="36d9f-163">Enter the following commands in the Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="36d9f-164">Une fois le déploiement terminé, votre compte de stockage existe dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="36d9f-164">When deployment finishes, your storage account exists in the resource group.</span></span>

## <a name="customize-the-template"></a><span data-ttu-id="36d9f-165">Personnaliser le modèle</span><span class="sxs-lookup"><span data-stu-id="36d9f-165">Customize the template</span></span>

<span data-ttu-id="36d9f-166">Le modèle fonctionne correctement, mais il n’est pas flexible.</span><span class="sxs-lookup"><span data-stu-id="36d9f-166">The template works fine, but it is not flexible.</span></span> <span data-ttu-id="36d9f-167">Il déploie toujours un stockage localement redondant pour la région Sud-Centre des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="36d9f-167">It always deploys a locally redundant storage to South Central US.</span></span> <span data-ttu-id="36d9f-168">Le nom est toujours *stockage* suivi d’une valeur de hachage.</span><span class="sxs-lookup"><span data-stu-id="36d9f-168">The name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="36d9f-169">Pour permettre l’utilisation du modèle dans différents scénarios, ajoutez des paramètres au modèle.</span><span class="sxs-lookup"><span data-stu-id="36d9f-169">To enable using the template for different scenarios, add parameters to the template.</span></span>

<span data-ttu-id="36d9f-170">L’exemple suivant montre la section des paramètres avec deux paramètres.</span><span class="sxs-lookup"><span data-stu-id="36d9f-170">The following example shows the parameters section with two parameters.</span></span> <span data-ttu-id="36d9f-171">Le premier paramètre `storageSKU` vous permet de spécifier le type de redondance.</span><span class="sxs-lookup"><span data-stu-id="36d9f-171">The first parameter `storageSKU` enables you to specify the type of redundancy.</span></span> <span data-ttu-id="36d9f-172">Il limite les valeurs que vous pouvez transmettre aux valeurs valides pour un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="36d9f-172">It limits the values you can pass in to values that are valid for a storage account.</span></span> <span data-ttu-id="36d9f-173">Il spécifie également une valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="36d9f-173">It also specifies a default value.</span></span> <span data-ttu-id="36d9f-174">Le deuxième paramètre `storageNamePrefix` est défini de façon à autoriser un maximum de 11 caractères.</span><span class="sxs-lookup"><span data-stu-id="36d9f-174">The second parameter `storageNamePrefix` is set to allow a maximum of 11 characters.</span></span> <span data-ttu-id="36d9f-175">Il spécifie une valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="36d9f-175">It specifies a default value.</span></span>

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
      "description": "The type of replication to use for the storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="36d9f-176">Dans la section des variables, ajoutez une variable nommée `storageName`.</span><span class="sxs-lookup"><span data-stu-id="36d9f-176">In the variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="36d9f-177">Elle associe la valeur de préfixe des paramètres à une valeur de hachage de la fonction [uniqueString](resource-group-template-functions-string.md#uniquestring).</span><span class="sxs-lookup"><span data-stu-id="36d9f-177">It combines the prefix value from the parameters and a hash value from the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="36d9f-178">Elle utilise la fonction [toLower](resource-group-template-functions-string.md#tolower) pour convertir tous les caractères en minuscules.</span><span class="sxs-lookup"><span data-stu-id="36d9f-178">It uses the [toLower](resource-group-template-functions-string.md#tolower) function to convert all characters to lowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="36d9f-179">Pour utiliser ces nouvelles valeurs pour votre compte de stockage, modifiez la définition de ressource :</span><span class="sxs-lookup"><span data-stu-id="36d9f-179">To use these new values for your storage account, change the resource definition:</span></span>

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

<span data-ttu-id="36d9f-180">Notez que le nom du compte de stockage est maintenant défini sur la variable que vous avez ajoutée.</span><span class="sxs-lookup"><span data-stu-id="36d9f-180">Notice that the name of the storage account is now set to the variable that you added.</span></span> <span data-ttu-id="36d9f-181">Le nom de référence SKU est défini sur la valeur du paramètre.</span><span class="sxs-lookup"><span data-stu-id="36d9f-181">The SKU name is set to the value of the parameter.</span></span> <span data-ttu-id="36d9f-182">L’emplacement est défini sur celui du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="36d9f-182">The location is set the same location as the resource group.</span></span>

<span data-ttu-id="36d9f-183">Enregistrez votre fichier.</span><span class="sxs-lookup"><span data-stu-id="36d9f-183">Save your file.</span></span> 

<span data-ttu-id="36d9f-184">Après avoir effectué les étapes de cet article, votre modèle doit maintenant ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="36d9f-184">After completing the steps in this article, your template now looks like:</span></span>

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
        "description": "The type of replication to use for the storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
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

## <a name="redeploy-template"></a><span data-ttu-id="36d9f-185">Redéployer le modèle</span><span class="sxs-lookup"><span data-stu-id="36d9f-185">Redeploy template</span></span>

<span data-ttu-id="36d9f-186">Redéployez le modèle avec des valeurs différentes.</span><span class="sxs-lookup"><span data-stu-id="36d9f-186">Redeploy the template with different values.</span></span>

<span data-ttu-id="36d9f-187">Pour PowerShell, utilisez :</span><span class="sxs-lookup"><span data-stu-id="36d9f-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="36d9f-188">Pour l’interface de ligne de commande Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="36d9f-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="36d9f-189">Pour Cloud Shell, chargez votre modèle modifié vers le partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="36d9f-189">For the Cloud Shell, upload your changed template to the file share.</span></span> <span data-ttu-id="36d9f-190">Remplacez le fichier existant.</span><span class="sxs-lookup"><span data-stu-id="36d9f-190">Overwrite the existing file.</span></span> <span data-ttu-id="36d9f-191">Utilisez ensuite la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="36d9f-191">Then, use the following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="36d9f-192">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="36d9f-192">Clean up resources</span></span>

<span data-ttu-id="36d9f-193">Lorsque vous n’en avez plus besoin, nettoyez les ressources que vous avez déployées en supprimant le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="36d9f-193">When no longer needed, clean up the resources you deployed by deleting the resource group.</span></span>

<span data-ttu-id="36d9f-194">Pour PowerShell, utilisez :</span><span class="sxs-lookup"><span data-stu-id="36d9f-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="36d9f-195">Pour l’interface de ligne de commande Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="36d9f-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="36d9f-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36d9f-196">Next steps</span></span>
* <span data-ttu-id="36d9f-197">Pour plus d’informations sur la structure du modèle, consultez [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="36d9f-197">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="36d9f-198">Pour en savoir plus sur les propriétés d’un compte de stockage, consultez la [référence sur le modèle des comptes de stockage](/azure/templates/microsoft.storage/storageaccounts).</span><span class="sxs-lookup"><span data-stu-id="36d9f-198">To learn about the properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="36d9f-199">Pour afficher des modèles complets pour de nombreux types de solutions, consultez [Modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="36d9f-199">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
