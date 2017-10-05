---
title: "Déployer des ressources avec le modèle et PowerShell | Microsoft Docs"
description: "Utilisez Azure Resource Manager et Azure PowerShell pour déployer des ressources sur Azure. Les ressources sont définies dans un modèle Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 5f395abf8ebdfbac18fd17d8183b392673e280ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="288e9-104">Déployer des ressources à l’aide de modèles Resource Manager et d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="288e9-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="288e9-105">Cette rubrique explique comment utiliser Azure PowerShell avec les modèles Resource Manager pour déployer vos ressources dans Azure.</span><span class="sxs-lookup"><span data-stu-id="288e9-105">This topic explains how to use Azure PowerShell with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="288e9-106">Si vous n’avez pas une bonne connaissance des concepts de déploiement et de gestion de solutions Azure, consultez [Vue d’ensemble d’Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="288e9-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="288e9-107">Le modèle Resource Manager que vous déployez peut être un fichier local sur votre ordinateur ou un fichier externe qui se trouve dans un dépôt comme GitHub.</span><span class="sxs-lookup"><span data-stu-id="288e9-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="288e9-108">Le modèle que vous déployez dans cet article est disponible dans la section [Exemple de modèle](#sample-template) ou en tant que [modèle de compte de stockage dans GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="288e9-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="288e9-109">Déployer un modèle à partir de votre ordinateur local</span><span class="sxs-lookup"><span data-stu-id="288e9-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="288e9-110">Au moment de déployer des ressources dans Azure, vous effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="288e9-110">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="288e9-111">Connexion à votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="288e9-111">Log in to your Azure account</span></span>
2. <span data-ttu-id="288e9-112">Créez un groupe de ressources qui sert de conteneur pour les ressources déployées.</span><span class="sxs-lookup"><span data-stu-id="288e9-112">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="288e9-113">Le nom du groupe de ressources ne peut contenir que des caractères alphanumériques, des points, des traits de soulignement, des traits d'union et des parenthèses.</span><span class="sxs-lookup"><span data-stu-id="288e9-113">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="288e9-114">Il peut comprendre jusqu’à 90 caractères.</span><span class="sxs-lookup"><span data-stu-id="288e9-114">It can be up to 90 characters.</span></span> <span data-ttu-id="288e9-115">Il ne peut pas se terminer par un point.</span><span class="sxs-lookup"><span data-stu-id="288e9-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="288e9-116">Déploiement dans le groupe de ressources du modèle qui définit les ressources à créer</span><span class="sxs-lookup"><span data-stu-id="288e9-116">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="288e9-117">Un modèle peut inclure des paramètres qui permettent de personnaliser le déploiement.</span><span class="sxs-lookup"><span data-stu-id="288e9-117">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="288e9-118">Par exemple, vous pouvez indiquer des valeurs qui sont adaptées à un environnement particulier (par exemple, de développement, de test ou de production).</span><span class="sxs-lookup"><span data-stu-id="288e9-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="288e9-119">L’exemple de modèle définit un paramètre pour la référence (SKU) de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="288e9-119">The sample template defines a parameter for the storage account SKU.</span></span>

<span data-ttu-id="288e9-120">L’exemple suivant crée un groupe de ressources et déploie un modèle à partir de votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="288e9-120">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="288e9-121">Le déploiement peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="288e9-121">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="288e9-122">Au terme, vous voyez un message qui inclut le résultat :</span><span class="sxs-lookup"><span data-stu-id="288e9-122">When it finishes, you see a message that includes the result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="288e9-123">Déployer un modèle à partir d’une source externe</span><span class="sxs-lookup"><span data-stu-id="288e9-123">Deploy a template from an external source</span></span>

<span data-ttu-id="288e9-124">Au lieu de stocker les modèles Resource Manager sur votre ordinateur local, vous pouvez les stocker dans un emplacement externe.</span><span class="sxs-lookup"><span data-stu-id="288e9-124">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="288e9-125">Vous pouvez stocker des modèles dans un dépôt de contrôle de code source (par exemple, GitHub).</span><span class="sxs-lookup"><span data-stu-id="288e9-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="288e9-126">Vous pouvez aussi les stocker dans un compte de stockage Azure pour mettre en place un accès partagé dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="288e9-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="288e9-127">Pour déployer un modèle externe, utilisez le paramètre **TemplateUri**.</span><span class="sxs-lookup"><span data-stu-id="288e9-127">To deploy an external template, use the **TemplateUri** parameter.</span></span> <span data-ttu-id="288e9-128">Pour déployer l’exemple de modèle à partir de GitHub, utilisez l’URI figurant dans l’exemple.</span><span class="sxs-lookup"><span data-stu-id="288e9-128">Use the URI in the example to deploy the sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="288e9-129">L’exemple précédent nécessite un URI accessible publiquement pour le modèle, ce qui convient pour la plupart des scénarios, sachant que votre modèle ne doit pas inclure de données sensibles.</span><span class="sxs-lookup"><span data-stu-id="288e9-129">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="288e9-130">Si vous avez besoin de spécifier des données sensibles (par exemple, un mot de passe d’administrateur), passez cette valeur en tant que paramètre sécurisé.</span><span class="sxs-lookup"><span data-stu-id="288e9-130">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="288e9-131">Toutefois, si vous ne souhaitez pas que votre modèle soit accessible au public, vous pouvez le protéger en le stockant dans un conteneur de stockage privé.</span><span class="sxs-lookup"><span data-stu-id="288e9-131">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="288e9-132">Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton de signature d’accès partagé (SAS), consultez [Déployer un modèle privé avec un jeton SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="288e9-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="288e9-133">Fichiers de paramètres</span><span class="sxs-lookup"><span data-stu-id="288e9-133">Parameter files</span></span>

<span data-ttu-id="288e9-134">Au lieu de passer des paramètres en tant que valeurs inline dans votre script, il peut s’avérer plus facile d’utiliser un fichier JSON qui contient les valeurs des paramètres.</span><span class="sxs-lookup"><span data-stu-id="288e9-134">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="288e9-135">Le fichier de paramètres doit être au format suivant :</span><span class="sxs-lookup"><span data-stu-id="288e9-135">The parameter file must be in the following format:</span></span>

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

<span data-ttu-id="288e9-136">Notez que la section des paramètres comprend un nom de paramètre qui correspond au paramètre défini dans votre modèle (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="288e9-136">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="288e9-137">Le fichier de paramètres contient une valeur pour le paramètre.</span><span class="sxs-lookup"><span data-stu-id="288e9-137">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="288e9-138">Cette valeur est transmise automatiquement au modèle pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="288e9-138">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="288e9-139">Vous pouvez créer plusieurs fichiers de paramètres pour différents scénarios de déploiement, puis transmettre le fichier de paramètres approprié.</span><span class="sxs-lookup"><span data-stu-id="288e9-139">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="288e9-140">Copiez l’exemple précédent et enregistrez-le dans un fichier nommé `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="288e9-140">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="288e9-141">Pour transmettre un fichier de paramètres local, utilisez le paramètre **TemplateParameterFile** :</span><span class="sxs-lookup"><span data-stu-id="288e9-141">To pass a local parameter file, use the **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="288e9-142">Pour transmettre un fichier de paramètres externe, utilisez le paramètre **TemplateParameterUri** :</span><span class="sxs-lookup"><span data-stu-id="288e9-142">To pass an external parameter file, use the **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="288e9-143">Vous pouvez utiliser des paramètres inline et un fichier de paramètres local pendant la même opération de déploiement.</span><span class="sxs-lookup"><span data-stu-id="288e9-143">You can use inline parameters and a local parameter file in the same deployment operation.</span></span> <span data-ttu-id="288e9-144">Par exemple, vous pouvez spécifier certaines valeurs dans le fichier de paramètres local et ajouter d’autres valeurs inline pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="288e9-144">For example, you can specify some values in the local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="288e9-145">Si vous fournissez des valeurs pour un paramètre à la fois dans le fichier de paramètres local et inline, la valeur inline est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="288e9-145">If you provide values for a parameter in both the local parameter file and inline, the inline value takes precedence.</span></span>

<span data-ttu-id="288e9-146">Cependant, lorsque vous utilisez un fichier de paramètres externe, vous ne pouvez pas passer d’autres valeurs inline ou tirées d’un fichier local.</span><span class="sxs-lookup"><span data-stu-id="288e9-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="288e9-147">Lorsque vous spécifiez un fichier de paramètres dans le paramètre **TemplateParameterUri**, tous les paramètres inline sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="288e9-147">When you specify a parameter file in the **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="288e9-148">Fournissez toutes les valeurs de paramètre dans le fichier externe.</span><span class="sxs-lookup"><span data-stu-id="288e9-148">Provide all parameter values in the external file.</span></span> <span data-ttu-id="288e9-149">Si votre modèle inclut une valeur sensible que vous ne pouvez pas inclure dans le fichier de paramètres, ajoutez cette valeur dans un coffre de clés, ou fournissez de manière dynamique toutes des valeurs de paramètre inline.</span><span class="sxs-lookup"><span data-stu-id="288e9-149">If your template includes a sensitive value that you cannot include in the parameter file, either add that value to a key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="288e9-150">Si votre modèle inclut un paramètre utilisant le même nom que l’un des paramètres dans la commande PowerShell, PowerShell présente le paramètre de votre modèle avec le suffixe **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="288e9-150">If your template includes a parameter with the same name as one of the parameters in the PowerShell command, PowerShell presents the parameter from your template with the postfix **FromTemplate**.</span></span> <span data-ttu-id="288e9-151">Par exemple, un paramètre nommé **ResourceGroupName** dans votre modèle est en conflit avec le paramètre **ResourceGroupName** dans l’applet de commande [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="288e9-151">For example, a parameter named **ResourceGroupName** in your template conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="288e9-152">Vous êtes invité à fournir une valeur pour **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="288e9-152">You are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="288e9-153">En général, vous devez éviter cette confusion en ne nommant pas les paramètres avec un nom identique à celui des paramètres utilisés pour les opérations de déploiement.</span><span class="sxs-lookup"><span data-stu-id="288e9-153">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="288e9-154">Tester le déploiement d’un modèle</span><span class="sxs-lookup"><span data-stu-id="288e9-154">Test a template deployment</span></span>

<span data-ttu-id="288e9-155">Pour tester votre modèle et vos valeur de paramètre sans réellement déployer toutes les ressources, utilisez [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="288e9-155">To test your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="288e9-156">Si aucune erreur n’est détectée, la commande se termine sans réponse.</span><span class="sxs-lookup"><span data-stu-id="288e9-156">If no errors are detected, the command finishes without a response.</span></span> <span data-ttu-id="288e9-157">Si une erreur est détectée, la commande retourne un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="288e9-157">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="288e9-158">Par exemple, la tentative de transmission d’une valeur incorrecte pour la référence (SKU) du compte de stockage retourne l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="288e9-158">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'The provided value 'badSku' for the template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. The parameter value is not part of the allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="288e9-159">Si votre modèle comporte une erreur de syntaxe, la commande retourne une erreur indiquant qu’il n’a pas pu analyser le modèle.</span><span class="sxs-lookup"><span data-stu-id="288e9-159">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="288e9-160">Le message indique le numéro de ligne et la position de l’erreur d’analyse.</span><span class="sxs-lookup"><span data-stu-id="288e9-160">The message indicates the line number and position of the parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="288e9-161">Pour utiliser le mode complet, utilisez le paramètre `Mode` :</span><span class="sxs-lookup"><span data-stu-id="288e9-161">To use complete mode, use the `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="288e9-162">Exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="288e9-162">Sample template</span></span>

<span data-ttu-id="288e9-163">Le modèle suivant est utilisé pour les exemples de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="288e9-163">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="288e9-164">Copiez et enregistrez-le dans un fichier nommé storage.json.</span><span class="sxs-lookup"><span data-stu-id="288e9-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="288e9-165">Pour comprendre comment ce modèle est créé, consultez [Créer votre premier modèle Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="288e9-165">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="288e9-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="288e9-166">Next steps</span></span>
* <span data-ttu-id="288e9-167">Les exemples de cet article permettent de déployer des ressources dans un groupe de ressources pour votre abonnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="288e9-167">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="288e9-168">Pour utiliser un autre abonnement, consultez [Gérer plusieurs abonnements Azure](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="288e9-168">To use a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="288e9-169">Pour accéder à un exemple de script complet qui déploie un modèle, consultez la page [Déploiement d’un modèle Azure Resource Manager](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="288e9-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="288e9-170">Pour comprendre comment définir des paramètres dans votre modèle, consultez [Comprendre la structure et la syntaxe des modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="288e9-170">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="288e9-171">Pour obtenir des conseils sur la résolution des erreurs courantes de déploiement, consultez la page [Résolution des erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="288e9-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="288e9-172">Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton SAP, consultez [Déploiement d’un modèle privé avec un jeton SAP](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="288e9-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="288e9-173">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="288e9-173">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

