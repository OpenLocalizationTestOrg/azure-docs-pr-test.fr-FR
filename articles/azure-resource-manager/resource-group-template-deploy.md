---
title: "ressources aaaDeploy avec PowerShell et modèle | Documents Microsoft"
description: "Utilisez le Gestionnaire de ressources Azure et d’Azure PowerShell toodeploy un tooAzure de ressources. ressources de Hello sont définies dans un modèle de gestionnaire de ressources."
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
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="913b9-104">Déployer des ressources à l’aide de modèles Resource Manager et d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="913b9-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="913b9-105">Cette rubrique explique comment toouse Azure PowerShell avec le Gestionnaire de ressources modèles toodeploy tooAzure de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="913b9-105">This topic explains how toouse Azure PowerShell with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="913b9-106">Si vous n’êtes pas familiarisé avec les concepts de hello du déploiement et la gestion de vos solutions Azure, consultez [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="913b9-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="913b9-107">modèle de gestionnaire de ressources Hello que vous déployez peut être un fichier local sur votre ordinateur, ou un fichier externe qui se trouve dans un référentiel comme GitHub.</span><span class="sxs-lookup"><span data-stu-id="913b9-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="913b9-108">modèle de Hello vous déployez dans cet article est disponible dans hello [exemple de modèle](#sample-template) section, ou en tant que [modèle de compte de stockage dans GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="913b9-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="913b9-109">Déployer un modèle à partir de votre ordinateur local</span><span class="sxs-lookup"><span data-stu-id="913b9-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="913b9-110">Lors du déploiement de ressources tooAzure, vous :</span><span class="sxs-lookup"><span data-stu-id="913b9-110">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="913b9-111">Ouvrez une session dans tooyour compte Azure</span><span class="sxs-lookup"><span data-stu-id="913b9-111">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="913b9-112">Créer un groupe de ressources qui sert de conteneur hello pour les ressources de hello déployé.</span><span class="sxs-lookup"><span data-stu-id="913b9-112">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="913b9-113">nom Hello hello du groupe de ressources peut inclure uniquement les parenthèses, des points, des traits de soulignement, des traits d’union et des caractères alphanumériques.</span><span class="sxs-lookup"><span data-stu-id="913b9-113">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="913b9-114">Il peut être too90 caractères.</span><span class="sxs-lookup"><span data-stu-id="913b9-114">It can be up too90 characters.</span></span> <span data-ttu-id="913b9-115">Il ne peut pas se terminer par un point.</span><span class="sxs-lookup"><span data-stu-id="913b9-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="913b9-116">Déployer toohello ressource groupe hello modèle qui définit hello ressources toocreate</span><span class="sxs-lookup"><span data-stu-id="913b9-116">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="913b9-117">Un modèle peut inclure des paramètres qui vous permettent de déploiement de hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="913b9-117">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="913b9-118">Par exemple, vous pouvez indiquer des valeurs qui sont adaptées à un environnement particulier (par exemple, de développement, de test ou de production).</span><span class="sxs-lookup"><span data-stu-id="913b9-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="913b9-119">exemple de modèle de Hello définit un paramètre pour le compte de stockage hello référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="913b9-119">hello sample template defines a parameter for hello storage account SKU.</span></span>

<span data-ttu-id="913b9-120">Bonjour à l’exemple suivant crée un groupe de ressources et déploie un modèle à partir de votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="913b9-120">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="913b9-121">déploiement de Hello peut prendre quelques minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="913b9-121">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="913b9-122">Lorsqu’elle est terminée, vous voyez un message qui inclut le résultat de hello :</span><span class="sxs-lookup"><span data-stu-id="913b9-122">When it finishes, you see a message that includes hello result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="913b9-123">Déployer un modèle à partir d’une source externe</span><span class="sxs-lookup"><span data-stu-id="913b9-123">Deploy a template from an external source</span></span>

<span data-ttu-id="913b9-124">Au lieu de stocker les modèles de gestionnaire de ressources sur votre ordinateur local, vous souhaiterez peut-être toostore dans un emplacement externe.</span><span class="sxs-lookup"><span data-stu-id="913b9-124">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="913b9-125">Vous pouvez stocker des modèles dans un dépôt de contrôle de code source (par exemple, GitHub).</span><span class="sxs-lookup"><span data-stu-id="913b9-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="913b9-126">Vous pouvez aussi les stocker dans un compte de stockage Azure pour mettre en place un accès partagé dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="913b9-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="913b9-127">toodeploy un modèle externe, utilisez hello **TemplateUri** paramètre.</span><span class="sxs-lookup"><span data-stu-id="913b9-127">toodeploy an external template, use hello **TemplateUri** parameter.</span></span> <span data-ttu-id="913b9-128">Utilisez hello URI dans hello exemple toodeploy hello exemple de modèle à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="913b9-128">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="913b9-129">Hello exemple précédent requiert un URI accessible publiquement pour modèle hello, qui fonctionne pour la plupart des scénarios, car votre modèle ne doit pas inclure les données sensibles.</span><span class="sxs-lookup"><span data-stu-id="913b9-129">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="913b9-130">Si vous avez besoin de toospecify des données sensibles (par exemple, un mot de passe administrateur), passez cette valeur comme paramètre sécurisé.</span><span class="sxs-lookup"><span data-stu-id="913b9-130">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="913b9-131">Toutefois, si vous ne souhaitez pas votre toobe modèle accessible publiquement, vous pouvez le protéger en les stockant dans un conteneur de stockage privé.</span><span class="sxs-lookup"><span data-stu-id="913b9-131">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="913b9-132">Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton de signature d’accès partagé (SAS), consultez [Déployer un modèle privé avec un jeton SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="913b9-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="913b9-133">Fichiers de paramètres</span><span class="sxs-lookup"><span data-stu-id="913b9-133">Parameter files</span></span>

<span data-ttu-id="913b9-134">Au lieu de passer des paramètres en tant que valeurs inline dans votre script, il peut s’avérer plus facile toouse un fichier JSON qui contient des valeurs de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="913b9-134">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="913b9-135">fichier de paramètres Hello doit être Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="913b9-135">hello parameter file must be in hello following format:</span></span>

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

<span data-ttu-id="913b9-136">Notez que hello paramètres comprend un nom de paramètre qui correspond au paramètre hello défini dans votre modèle (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="913b9-136">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="913b9-137">fichier de paramètres Hello contient une valeur pour le paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="913b9-137">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="913b9-138">Cette valeur est automatiquement passée toohello modèle durant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="913b9-138">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="913b9-139">Vous pouvez créer plusieurs fichiers de paramètres pour différents scénarios de déploiement et passez dans un fichier de paramètres appropriés de hello.</span><span class="sxs-lookup"><span data-stu-id="913b9-139">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="913b9-140">Copier hello précédent exemple et l’enregistrer en tant qu’un fichier nommé `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="913b9-140">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="913b9-141">toopass un fichier local de paramètre, utilisez hello **TemplateParameterFile** paramètre :</span><span class="sxs-lookup"><span data-stu-id="913b9-141">toopass a local parameter file, use hello **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="913b9-142">toopass un fichier de paramètres externe, utilisez hello **TemplateParameterUri** paramètre :</span><span class="sxs-lookup"><span data-stu-id="913b9-142">toopass an external parameter file, use hello **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="913b9-143">Vous pouvez utiliser les paramètres inline et un paramètre local du fichier Bonjour même opération de déploiement.</span><span class="sxs-lookup"><span data-stu-id="913b9-143">You can use inline parameters and a local parameter file in hello same deployment operation.</span></span> <span data-ttu-id="913b9-144">Par exemple, vous pouvez spécifier certaines valeurs dans le fichier de paramètre local hello et ajouter d’autres en ligne des valeurs pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="913b9-144">For example, you can specify some values in hello local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="913b9-145">Si vous indiquez des valeurs pour un paramètre dans le fichier de paramètre local hello et inline, valeur de hello inline est prioritaire.</span><span class="sxs-lookup"><span data-stu-id="913b9-145">If you provide values for a parameter in both hello local parameter file and inline, hello inline value takes precedence.</span></span>

<span data-ttu-id="913b9-146">Cependant, lorsque vous utilisez un fichier de paramètres externe, vous ne pouvez pas passer d’autres valeurs inline ou tirées d’un fichier local.</span><span class="sxs-lookup"><span data-stu-id="913b9-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="913b9-147">Lorsque vous spécifiez un fichier de paramètres dans hello **TemplateParameterUri** paramètre, inline tous les paramètres sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="913b9-147">When you specify a parameter file in hello **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="913b9-148">Fournir toutes les valeurs de paramètre dans un fichier externe de hello.</span><span class="sxs-lookup"><span data-stu-id="913b9-148">Provide all parameter values in hello external file.</span></span> <span data-ttu-id="913b9-149">Si votre modèle inclut une valeur sensible que vous ne pouvez pas inclure dans le fichier de paramètres hello, ajoutez ce coffre de clés tooa valeur, ou fournir de manière dynamique en ligne toutes des valeurs de paramètre.</span><span class="sxs-lookup"><span data-stu-id="913b9-149">If your template includes a sensitive value that you cannot include in hello parameter file, either add that value tooa key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="913b9-150">Si votre modèle inclut un paramètre avec le même nom qu’un des paramètres hello Bonjour de commande PowerShell de hello, PowerShell présente le paramètre hello à partir de votre modèle avec le suffixe de hello **modèle**.</span><span class="sxs-lookup"><span data-stu-id="913b9-150">If your template includes a parameter with hello same name as one of hello parameters in hello PowerShell command, PowerShell presents hello parameter from your template with hello postfix **FromTemplate**.</span></span> <span data-ttu-id="913b9-151">Par exemple, un paramètre nommé **ResourceGroupName** dans votre modèle est en conflit avec hello **ResourceGroupName** paramètre Bonjour [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)applet de commande.</span><span class="sxs-lookup"><span data-stu-id="913b9-151">For example, a parameter named **ResourceGroupName** in your template conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="913b9-152">Vous êtes invité à tooprovide une valeur pour **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="913b9-152">You are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="913b9-153">En règle générale, vous devez éviter cette confusion en nommant ne pas de paramètres avec le même nom en tant que paramètres utilisés pour les opérations de déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="913b9-153">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="913b9-154">Tester le déploiement d’un modèle</span><span class="sxs-lookup"><span data-stu-id="913b9-154">Test a template deployment</span></span>

<span data-ttu-id="913b9-155">utilisation de vos valeurs de paramètres et de modèle sans réellement déployer des ressources, tootest [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="913b9-155">tootest your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="913b9-156">Si aucune erreur n’est détectée, la commande hello se termine sans réponse.</span><span class="sxs-lookup"><span data-stu-id="913b9-156">If no errors are detected, hello command finishes without a response.</span></span> <span data-ttu-id="913b9-157">Si une erreur est détectée, la commande hello renvoie un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="913b9-157">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="913b9-158">Par exemple, la tentative de toopass une valeur incorrecte pour le compte de stockage hello référence (SKU), retourne hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="913b9-158">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="913b9-159">Si votre modèle comporte une erreur de syntaxe, commande hello renvoie une erreur indiquant qu’il a pas pu analyser le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="913b9-159">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="913b9-160">message de type Hello indique le numéro de ligne hello et la position de l’erreur d’analyse de hello.</span><span class="sxs-lookup"><span data-stu-id="913b9-160">hello message indicates hello line number and position of hello parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="913b9-161">en mode toouse terminée, utilisez hello `Mode` paramètre :</span><span class="sxs-lookup"><span data-stu-id="913b9-161">toouse complete mode, use hello `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="913b9-162">Exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="913b9-162">Sample template</span></span>

<span data-ttu-id="913b9-163">Hello modèle suivant est utilisé pour obtenir des exemples hello dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="913b9-163">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="913b9-164">Copiez et enregistrez-le dans un fichier nommé storage.json.</span><span class="sxs-lookup"><span data-stu-id="913b9-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="913b9-165">toounderstand comment toocreate ce modèle, consultez [créer votre premier modèle Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="913b9-165">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="913b9-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="913b9-166">Next steps</span></span>
* <span data-ttu-id="913b9-167">exemples de Hello dans cet article déploiement un groupe de ressources tooa ressources dans votre abonnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="913b9-167">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="913b9-168">toouse un autre abonnement, consultez [gérer plusieurs abonnements Azure](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="913b9-168">toouse a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="913b9-169">Pour accéder à un exemple de script complet qui déploie un modèle, consultez la page [Déploiement d’un modèle Azure Resource Manager](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="913b9-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="913b9-170">toounderstand toodefine des paramètres dans votre modèle, voir [comprendre la structure de hello et syntaxe des modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="913b9-170">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="913b9-171">Pour obtenir des conseils sur la résolution des erreurs courantes de déploiement, consultez la page [Résolution des erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="913b9-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="913b9-172">Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton SAP, consultez [Déploiement d’un modèle privé avec un jeton SAP](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="913b9-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="913b9-173">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="913b9-173">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

