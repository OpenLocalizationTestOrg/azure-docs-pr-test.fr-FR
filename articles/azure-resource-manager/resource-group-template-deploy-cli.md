---
title: "Déployer des ressources avec Azure CLI et un modèle | Microsoft Docs"
description: "Utilisez Azure Resource Manager et Azure CLI pour déployer des ressources sur Azure. Les ressources sont définies dans un modèle Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 4f1d5f4cc48470f8906edb28628006dd1996bd3a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="bafa4-104">Déployer des ressources à l’aide de modèles Resource Manager et dAzure CLI</span><span class="sxs-lookup"><span data-stu-id="bafa4-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="bafa4-105">Cette rubrique explique comment utiliser Azure CLI 2.0 avec les modèles Resource Manager pour déployer vos ressources dans Azure.</span><span class="sxs-lookup"><span data-stu-id="bafa4-105">This topic explains how to use Azure CLI 2.0 with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="bafa4-106">Si vous n’avez pas une bonne connaissance des concepts de déploiement et de gestion de solutions Azure, consultez [Vue d’ensemble d’Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bafa4-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="bafa4-107">Le modèle Resource Manager que vous déployez peut être un fichier local sur votre ordinateur ou un fichier externe qui se trouve dans un dépôt comme GitHub.</span><span class="sxs-lookup"><span data-stu-id="bafa4-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="bafa4-108">Le modèle que vous déployez dans le cadre de cet article est disponible dans la section [Exemple de modèle](#sample-template) ou en tant que [modèle de compte de stockage dans GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="bafa4-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="bafa4-109">Si Azure CLI n’est pas installé, vous pouvez utiliser le [Cloud Shell](#deploy-template-from-cloud-shell).</span><span class="sxs-lookup"><span data-stu-id="bafa4-109">If you do not have Azure CLI installed, you can use the [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="bafa4-110">Déployer un modèle local</span><span class="sxs-lookup"><span data-stu-id="bafa4-110">Deploy local template</span></span>

<span data-ttu-id="bafa4-111">Au moment de déployer des ressources dans Azure, vous effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="bafa4-111">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="bafa4-112">Connexion à votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="bafa4-112">Log in to your Azure account</span></span>
2. <span data-ttu-id="bafa4-113">Créez un groupe de ressources qui sert de conteneur pour les ressources déployées.</span><span class="sxs-lookup"><span data-stu-id="bafa4-113">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="bafa4-114">Le nom du groupe de ressources ne peut contenir que des caractères alphanumériques, des points, des traits de soulignement, des traits d'union et des parenthèses.</span><span class="sxs-lookup"><span data-stu-id="bafa4-114">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="bafa4-115">Il peut comprendre jusqu’à 90 caractères.</span><span class="sxs-lookup"><span data-stu-id="bafa4-115">It can be up to 90 characters.</span></span> <span data-ttu-id="bafa4-116">Il ne peut pas se terminer par un point.</span><span class="sxs-lookup"><span data-stu-id="bafa4-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="bafa4-117">Déploiement dans le groupe de ressources du modèle qui définit les ressources à créer</span><span class="sxs-lookup"><span data-stu-id="bafa4-117">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="bafa4-118">Un modèle peut inclure des paramètres qui permettent de personnaliser le déploiement.</span><span class="sxs-lookup"><span data-stu-id="bafa4-118">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="bafa4-119">Par exemple, vous pouvez indiquer des valeurs qui sont adaptées à un environnement particulier (par exemple, de développement, de test ou de production).</span><span class="sxs-lookup"><span data-stu-id="bafa4-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="bafa4-120">L’exemple de modèle définit un paramètre pour la référence (SKU) de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="bafa4-120">The sample template defines a parameter for the storage account SKU.</span></span> 

<span data-ttu-id="bafa4-121">L’exemple suivant crée un groupe de ressources et déploie un modèle à partir de votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="bafa4-121">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="bafa4-122">Le déploiement peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="bafa4-122">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="bafa4-123">Au terme, vous voyez un message qui inclut le résultat :</span><span class="sxs-lookup"><span data-stu-id="bafa4-123">When it finishes, you see a message that includes the result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="bafa4-124">Déployer un modèle externe</span><span class="sxs-lookup"><span data-stu-id="bafa4-124">Deploy external template</span></span>

<span data-ttu-id="bafa4-125">Au lieu de stocker les modèles Resource Manager sur votre ordinateur local, vous pouvez les stocker dans un emplacement externe.</span><span class="sxs-lookup"><span data-stu-id="bafa4-125">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="bafa4-126">Vous pouvez stocker des modèles dans un dépôt de contrôle de code source (par exemple, GitHub).</span><span class="sxs-lookup"><span data-stu-id="bafa4-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="bafa4-127">Vous pouvez aussi les stocker dans un compte de stockage Azure pour mettre en place un accès partagé dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="bafa4-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="bafa4-128">Pour déployer un modèle externe, utilisez le paramètre **template-uri**.</span><span class="sxs-lookup"><span data-stu-id="bafa4-128">To deploy an external template, use the **template-uri** parameter.</span></span> <span data-ttu-id="bafa4-129">Pour déployer l’exemple de modèle à partir de GitHub, utilisez l’URI figurant dans l’exemple.</span><span class="sxs-lookup"><span data-stu-id="bafa4-129">Use the URI in the example to deploy the sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="bafa4-130">L’exemple précédent nécessite un URI accessible publiquement pour le modèle, ce qui convient pour la plupart des scénarios, sachant que votre modèle ne doit pas inclure de données sensibles.</span><span class="sxs-lookup"><span data-stu-id="bafa4-130">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="bafa4-131">Si vous avez besoin de spécifier des données sensibles (par exemple, un mot de passe d’administrateur), passez cette valeur en tant que paramètre sécurisé.</span><span class="sxs-lookup"><span data-stu-id="bafa4-131">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="bafa4-132">Toutefois, si vous ne souhaitez pas que votre modèle soit accessible au public, vous pouvez le protéger en le stockant dans un conteneur de stockage privé.</span><span class="sxs-lookup"><span data-stu-id="bafa4-132">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="bafa4-133">Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton de signature d’accès partagé (SAS), consultez [Déployer un modèle privé avec un jeton SAS](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="bafa4-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="bafa4-134">Déployer le modèle à partir de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="bafa4-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="bafa4-135">Vous pouvez utiliser [Cloud Shell](../cloud-shell/overview.md) pour exécuter les commandes Azure CLI pour le déploiement de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="bafa4-135">You can use [Cloud Shell](../cloud-shell/overview.md) to run the Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="bafa4-136">Toutefois, vous devez d’abord charger votre modèle dans le partage de fichiers de votre Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="bafa4-136">However, you must first load your template into the file share for your Cloud Shell.</span></span> <span data-ttu-id="bafa4-137">Si vous n’avez pas utilisé Cloud Shell, consultez [Vue d’ensemble d’Azure Cloud Shell](../cloud-shell/overview.md) pour obtenir plus d’informations sur sa configuration.</span><span class="sxs-lookup"><span data-stu-id="bafa4-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="bafa4-138">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bafa4-138">Log in to the [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="bafa4-139">Sélectionnez votre groupe de ressources Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="bafa4-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="bafa4-140">Le modèle de nom est `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="bafa4-140">The name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Sélection du groupe de ressources](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="bafa4-142">Sélectionnez le compte de stockage de votre Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="bafa4-142">Select the storage account for your Cloud Shell.</span></span>

   ![Sélectionner le compte de stockage](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="bafa4-144">Sélectionnez **Fichiers**.</span><span class="sxs-lookup"><span data-stu-id="bafa4-144">Select **Files**.</span></span>

   ![Sélectionner des fichiers](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="bafa4-146">Sélectionnez le partage de fichiers pour Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="bafa4-146">Select the file share for Cloud Shell.</span></span> <span data-ttu-id="bafa4-147">Le modèle de nom est `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="bafa4-147">The name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Sélectionner le partage de fichiers](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="bafa4-149">Sélectionnez **Ajouter un répertoire**.</span><span class="sxs-lookup"><span data-stu-id="bafa4-149">Select **Add directory**.</span></span>

   ![Ajouter un répertoire](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="bafa4-151">Nommez-le **modèles** puis sélectionnez **Ok**.</span><span class="sxs-lookup"><span data-stu-id="bafa4-151">Name it **templates**, and select **Okay**.</span></span>

   ![Nommer le répertoire](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="bafa4-153">Sélectionnez votre nouveau répertoire.</span><span class="sxs-lookup"><span data-stu-id="bafa4-153">Select your new directory.</span></span>

   ![Sélectionner le répertoire](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="bafa4-155">Sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="bafa4-155">Select **Upload**.</span></span>

   ![Sélectionner Télécharger](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="bafa4-157">Recherchez et chargez votre modèle.</span><span class="sxs-lookup"><span data-stu-id="bafa4-157">Find and upload your template.</span></span>

   ![Charger le fichier](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="bafa4-159">Ouvrez l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="bafa4-159">Open the prompt.</span></span>

   ![Ouvrir Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="bafa4-161">Entrez les commandes suivantes dans Cloud Shell :</span><span class="sxs-lookup"><span data-stu-id="bafa4-161">Enter the following commands in the Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="bafa4-162">Fichiers de paramètres</span><span class="sxs-lookup"><span data-stu-id="bafa4-162">Parameter files</span></span>

<span data-ttu-id="bafa4-163">Au lieu de passer des paramètres en tant que valeurs inline dans votre script, il peut s’avérer plus facile d’utiliser un fichier JSON qui contient les valeurs des paramètres.</span><span class="sxs-lookup"><span data-stu-id="bafa4-163">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="bafa4-164">Le fichier de paramètres doit être au format suivant :</span><span class="sxs-lookup"><span data-stu-id="bafa4-164">The parameter file must be in the following format:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

<span data-ttu-id="bafa4-165">Notez que la section des paramètres comprend un nom de paramètre qui correspond au paramètre défini dans votre modèle (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="bafa4-165">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="bafa4-166">Le fichier de paramètres contient une valeur pour le paramètre.</span><span class="sxs-lookup"><span data-stu-id="bafa4-166">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="bafa4-167">Cette valeur est transmise automatiquement au modèle pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="bafa4-167">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="bafa4-168">Vous pouvez créer plusieurs fichiers de paramètres pour différents scénarios de déploiement, puis transmettre le fichier de paramètres approprié.</span><span class="sxs-lookup"><span data-stu-id="bafa4-168">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="bafa4-169">Copiez l’exemple précédent et enregistrez-le dans un fichier nommé `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="bafa4-169">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="bafa4-170">Pour transmettre un fichier de paramètres local, utilisez `@` pour spécifier un fichier local nommé storage.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="bafa4-170">To pass a local parameter file, use `@` to specify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="bafa4-171">Tester le déploiement d’un modèle</span><span class="sxs-lookup"><span data-stu-id="bafa4-171">Test a template deployment</span></span>

<span data-ttu-id="bafa4-172">Pour tester votre modèle et vos valeurs de paramètres sans réellement déployer toutes les ressources, utilisez [az group deployment validate](/cli/azure/group/deployment#validate).</span><span class="sxs-lookup"><span data-stu-id="bafa4-172">To test your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="bafa4-173">Si aucune erreur n’est détectée, la commande retourne des informations sur le déploiement de test.</span><span class="sxs-lookup"><span data-stu-id="bafa4-173">If no errors are detected, the command returns information about the test deployment.</span></span> <span data-ttu-id="bafa4-174">En particulier, notez que **error** a la valeur Null.</span><span class="sxs-lookup"><span data-stu-id="bafa4-174">In particular, notice that the **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="bafa4-175">Si une erreur est détectée, la commande retourne un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="bafa4-175">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="bafa4-176">Par exemple, la tentative de transmission d’une valeur incorrecte pour la référence (SKU) du compte de stockage retourne l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="bafa4-176">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'The provided value 'badSKU' for the template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. The parameter value is not part of the allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

<span data-ttu-id="bafa4-177">Si votre modèle comporte une erreur de syntaxe, la commande retourne une erreur indiquant qu’il n’a pas pu analyser le modèle.</span><span class="sxs-lookup"><span data-stu-id="bafa4-177">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="bafa4-178">Le message indique le numéro de ligne et la position de l’erreur d’analyse.</span><span class="sxs-lookup"><span data-stu-id="bafa4-178">The message indicates the line number and position of the parsing error.</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="bafa4-179">Pour utiliser le mode complet, utilisez le paramètre `mode` :</span><span class="sxs-lookup"><span data-stu-id="bafa4-179">To use complete mode, use the `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="bafa4-180">Exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="bafa4-180">Sample template</span></span>

<span data-ttu-id="bafa4-181">Le modèle suivant est utilisé pour les exemples de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="bafa4-181">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="bafa4-182">Copiez et enregistrez-le dans un fichier nommé storage.json.</span><span class="sxs-lookup"><span data-stu-id="bafa4-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="bafa4-183">Pour comprendre comment ce modèle est créé, consultez [Créer votre premier modèle Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="bafa4-183">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="bafa4-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bafa4-184">Next steps</span></span>
* <span data-ttu-id="bafa4-185">Les exemples de cet article permettent de déployer des ressources dans un groupe de ressources pour votre abonnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="bafa4-185">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="bafa4-186">Pour utiliser un autre abonnement, consultez [Gérer plusieurs abonnements Azure](/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bafa4-186">To use a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="bafa4-187">Pour accéder à un exemple de script complet qui déploie un modèle, consultez la page [Déploiement d’un modèle Azure Resource Manager](resource-manager-samples-cli-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="bafa4-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="bafa4-188">Pour comprendre comment définir des paramètres dans votre modèle, consultez [Comprendre la structure et la syntaxe des modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bafa4-188">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="bafa4-189">Pour obtenir des conseils sur la résolution des erreurs courantes de déploiement, consultez la page [Résolution des erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="bafa4-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="bafa4-190">Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton SAP, consultez [Déploiement d’un modèle privé avec un jeton SAP](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="bafa4-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="bafa4-191">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="bafa4-191">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
