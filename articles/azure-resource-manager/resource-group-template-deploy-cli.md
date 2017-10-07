---
title: "ressources aaaDeploy avec CLI d’Azure et modèle | Documents Microsoft"
description: "Utilisez le Gestionnaire de ressources Azure et Azure CLI toodeploy un tooAzure de ressources. ressources de Hello sont définies dans un modèle de gestionnaire de ressources."
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
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="e1601-104">Déployer des ressources à l’aide de modèles Resource Manager et dAzure CLI</span><span class="sxs-lookup"><span data-stu-id="e1601-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="e1601-105">Cette rubrique explique comment toouse Azure CLI 2.0 avec le Gestionnaire de ressources modèles toodeploy tooAzure de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="e1601-105">This topic explains how toouse Azure CLI 2.0 with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="e1601-106">Si vous n’êtes pas familiarisé avec les concepts de hello du déploiement et la gestion de vos solutions Azure, consultez [vue d’ensemble du Gestionnaire de ressources Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e1601-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="e1601-107">modèle de gestionnaire de ressources Hello que vous déployez peut être un fichier local sur votre ordinateur, ou un fichier externe qui se trouve dans un référentiel comme GitHub.</span><span class="sxs-lookup"><span data-stu-id="e1601-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="e1601-108">modèle Hello que vous déployez dans cet article est disponible dans hello [exemple de modèle](#sample-template) section, ou comme un [modèle de compte de stockage dans GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e1601-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="e1601-109">Si vous n’avez pas installé CLI d’Azure, vous pouvez utiliser hello [Cloud Shell](#deploy-template-from-cloud-shell).</span><span class="sxs-lookup"><span data-stu-id="e1601-109">If you do not have Azure CLI installed, you can use hello [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="e1601-110">Déployer un modèle local</span><span class="sxs-lookup"><span data-stu-id="e1601-110">Deploy local template</span></span>

<span data-ttu-id="e1601-111">Lors du déploiement de ressources tooAzure, vous :</span><span class="sxs-lookup"><span data-stu-id="e1601-111">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="e1601-112">Ouvrez une session dans tooyour compte Azure</span><span class="sxs-lookup"><span data-stu-id="e1601-112">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="e1601-113">Créer un groupe de ressources qui sert de conteneur hello pour les ressources de hello déployé.</span><span class="sxs-lookup"><span data-stu-id="e1601-113">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="e1601-114">nom Hello hello du groupe de ressources peut inclure uniquement les parenthèses, des points, des traits de soulignement, des traits d’union et des caractères alphanumériques.</span><span class="sxs-lookup"><span data-stu-id="e1601-114">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="e1601-115">Il peut être too90 caractères.</span><span class="sxs-lookup"><span data-stu-id="e1601-115">It can be up too90 characters.</span></span> <span data-ttu-id="e1601-116">Il ne peut pas se terminer par un point.</span><span class="sxs-lookup"><span data-stu-id="e1601-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="e1601-117">Déployer toohello ressource groupe hello modèle qui définit hello ressources toocreate</span><span class="sxs-lookup"><span data-stu-id="e1601-117">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="e1601-118">Un modèle peut inclure des paramètres qui vous permettent de déploiement de hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="e1601-118">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="e1601-119">Par exemple, vous pouvez indiquer des valeurs qui sont adaptées à un environnement particulier (par exemple, de développement, de test ou de production).</span><span class="sxs-lookup"><span data-stu-id="e1601-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="e1601-120">exemple de modèle de Hello définit un paramètre pour le compte de stockage hello référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="e1601-120">hello sample template defines a parameter for hello storage account SKU.</span></span> 

<span data-ttu-id="e1601-121">Bonjour à l’exemple suivant crée un groupe de ressources et déploie un modèle à partir de votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="e1601-121">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="e1601-122">déploiement de Hello peut prendre quelques minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e1601-122">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="e1601-123">Lorsqu’elle est terminée, vous voyez un message qui inclut le résultat de hello :</span><span class="sxs-lookup"><span data-stu-id="e1601-123">When it finishes, you see a message that includes hello result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="e1601-124">Déployer un modèle externe</span><span class="sxs-lookup"><span data-stu-id="e1601-124">Deploy external template</span></span>

<span data-ttu-id="e1601-125">Au lieu de stocker les modèles de gestionnaire de ressources sur votre ordinateur local, vous souhaiterez peut-être toostore dans un emplacement externe.</span><span class="sxs-lookup"><span data-stu-id="e1601-125">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="e1601-126">Vous pouvez stocker des modèles dans un dépôt de contrôle de code source (par exemple, GitHub).</span><span class="sxs-lookup"><span data-stu-id="e1601-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="e1601-127">Vous pouvez aussi les stocker dans un compte de stockage Azure pour mettre en place un accès partagé dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="e1601-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="e1601-128">toodeploy un modèle externe, utilisez hello **-l’uri du modèle** paramètre.</span><span class="sxs-lookup"><span data-stu-id="e1601-128">toodeploy an external template, use hello **template-uri** parameter.</span></span> <span data-ttu-id="e1601-129">Utilisez hello URI dans hello exemple toodeploy hello exemple de modèle à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="e1601-129">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="e1601-130">Hello exemple précédent requiert un URI accessible publiquement pour modèle hello, qui fonctionne pour la plupart des scénarios, car votre modèle ne doit pas inclure les données sensibles.</span><span class="sxs-lookup"><span data-stu-id="e1601-130">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="e1601-131">Si vous avez besoin de toospecify des données sensibles (par exemple, un mot de passe administrateur), passez cette valeur comme paramètre sécurisé.</span><span class="sxs-lookup"><span data-stu-id="e1601-131">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="e1601-132">Toutefois, si vous ne souhaitez pas votre toobe modèle accessible publiquement, vous pouvez le protéger en les stockant dans un conteneur de stockage privé.</span><span class="sxs-lookup"><span data-stu-id="e1601-132">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="e1601-133">Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton de signature d’accès partagé (SAS), consultez [Déployer un modèle privé avec un jeton SAS](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="e1601-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="e1601-134">Déployer le modèle à partir de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="e1601-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="e1601-135">Vous pouvez utiliser [Cloud Shell](../cloud-shell/overview.md) toorun hello CLI d’Azure des commandes pour le déploiement de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="e1601-135">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="e1601-136">Toutefois, vous devez d’abord charger votre modèle dans le partage de fichiers hello pour votre environnement Cloud.</span><span class="sxs-lookup"><span data-stu-id="e1601-136">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="e1601-137">Si vous n’avez pas utilisé Cloud Shell, consultez [Vue d’ensemble d’Azure Cloud Shell](../cloud-shell/overview.md) pour obtenir plus d’informations sur sa configuration.</span><span class="sxs-lookup"><span data-stu-id="e1601-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="e1601-138">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1601-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="e1601-139">Sélectionnez votre groupe de ressources Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="e1601-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="e1601-140">modèle de nom Hello est `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="e1601-140">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Sélection du groupe de ressources](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="e1601-142">Sélectionnez le compte de stockage hello pour votre environnement Cloud.</span><span class="sxs-lookup"><span data-stu-id="e1601-142">Select hello storage account for your Cloud Shell.</span></span>

   ![Sélectionner le compte de stockage](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="e1601-144">Sélectionnez **Fichiers**.</span><span class="sxs-lookup"><span data-stu-id="e1601-144">Select **Files**.</span></span>

   ![Sélectionner des fichiers](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="e1601-146">Sélectionnez le partage de fichiers de hello pour Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="e1601-146">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="e1601-147">modèle de nom Hello est `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="e1601-147">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Sélectionner le partage de fichiers](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="e1601-149">Sélectionnez **Ajouter un répertoire**.</span><span class="sxs-lookup"><span data-stu-id="e1601-149">Select **Add directory**.</span></span>

   ![Ajouter un répertoire](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="e1601-151">Nommez-le **modèles** puis sélectionnez **Ok**.</span><span class="sxs-lookup"><span data-stu-id="e1601-151">Name it **templates**, and select **Okay**.</span></span>

   ![Nommer le répertoire](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="e1601-153">Sélectionnez votre nouveau répertoire.</span><span class="sxs-lookup"><span data-stu-id="e1601-153">Select your new directory.</span></span>

   ![Sélectionner le répertoire](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="e1601-155">Sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="e1601-155">Select **Upload**.</span></span>

   ![Sélectionner Télécharger](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="e1601-157">Recherchez et chargez votre modèle.</span><span class="sxs-lookup"><span data-stu-id="e1601-157">Find and upload your template.</span></span>

   ![Charger le fichier](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="e1601-159">Invite de commandes ouverte hello.</span><span class="sxs-lookup"><span data-stu-id="e1601-159">Open hello prompt.</span></span>

   ![Ouvrir Cloud Shell](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="e1601-161">Entrez hello suivant les commandes Bonjour Cloud Shell :</span><span class="sxs-lookup"><span data-stu-id="e1601-161">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="e1601-162">Fichiers de paramètres</span><span class="sxs-lookup"><span data-stu-id="e1601-162">Parameter files</span></span>

<span data-ttu-id="e1601-163">Au lieu de passer des paramètres en tant que valeurs inline dans votre script, il peut s’avérer plus facile toouse un fichier JSON qui contient des valeurs de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="e1601-163">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="e1601-164">fichier de paramètres Hello doit être Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="e1601-164">hello parameter file must be in hello following format:</span></span>

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

<span data-ttu-id="e1601-165">Notez que hello paramètres comprend un nom de paramètre qui correspond au paramètre hello défini dans votre modèle (storageAccountType).</span><span class="sxs-lookup"><span data-stu-id="e1601-165">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="e1601-166">fichier de paramètres Hello contient une valeur pour le paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="e1601-166">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="e1601-167">Cette valeur est automatiquement passée toohello modèle durant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="e1601-167">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="e1601-168">Vous pouvez créer plusieurs fichiers de paramètres pour différents scénarios de déploiement et passez dans un fichier de paramètres appropriés de hello.</span><span class="sxs-lookup"><span data-stu-id="e1601-168">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="e1601-169">Copier hello précédent exemple et l’enregistrer en tant qu’un fichier nommé `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="e1601-169">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="e1601-170">toopass un fichier local de paramètre, utilisez `@` toospecify un fichier local nommé storage.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="e1601-170">toopass a local parameter file, use `@` toospecify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="e1601-171">Tester le déploiement d’un modèle</span><span class="sxs-lookup"><span data-stu-id="e1601-171">Test a template deployment</span></span>

<span data-ttu-id="e1601-172">utilisation de vos valeurs de paramètres et de modèle sans réellement déployer des ressources, tootest [valider du déploiement d’un groupe az](/cli/azure/group/deployment#validate).</span><span class="sxs-lookup"><span data-stu-id="e1601-172">tootest your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="e1601-173">Si aucune erreur n’est détectée, commande hello retourne des informations sur le déploiement de test hello.</span><span class="sxs-lookup"><span data-stu-id="e1601-173">If no errors are detected, hello command returns information about hello test deployment.</span></span> <span data-ttu-id="e1601-174">En particulier, notez que hello **erreur** la valeur est null.</span><span class="sxs-lookup"><span data-stu-id="e1601-174">In particular, notice that hello **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="e1601-175">Si une erreur est détectée, la commande hello renvoie un message d’erreur.</span><span class="sxs-lookup"><span data-stu-id="e1601-175">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="e1601-176">Par exemple, la tentative de toopass une valeur incorrecte pour le compte de stockage hello référence (SKU), retourne hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="e1601-176">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

<span data-ttu-id="e1601-177">Si votre modèle comporte une erreur de syntaxe, commande hello renvoie une erreur indiquant qu’il a pas pu analyser le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="e1601-177">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="e1601-178">message de type Hello indique le numéro de ligne hello et la position de l’erreur d’analyse de hello.</span><span class="sxs-lookup"><span data-stu-id="e1601-178">hello message indicates hello line number and position of hello parsing error.</span></span>

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

<span data-ttu-id="e1601-179">en mode toouse terminée, utilisez hello `mode` paramètre :</span><span class="sxs-lookup"><span data-stu-id="e1601-179">toouse complete mode, use hello `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="e1601-180">Exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="e1601-180">Sample template</span></span>

<span data-ttu-id="e1601-181">Hello modèle suivant est utilisé pour obtenir des exemples hello dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="e1601-181">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="e1601-182">Copiez et enregistrez-le dans un fichier nommé storage.json.</span><span class="sxs-lookup"><span data-stu-id="e1601-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="e1601-183">toounderstand comment toocreate ce modèle, consultez [créer votre premier modèle Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="e1601-183">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="e1601-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e1601-184">Next steps</span></span>
* <span data-ttu-id="e1601-185">exemples de Hello dans cet article déploiement un groupe de ressources tooa ressources dans votre abonnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="e1601-185">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="e1601-186">toouse un autre abonnement, consultez [gérer plusieurs abonnements Azure](/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e1601-186">toouse a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="e1601-187">Pour accéder à un exemple de script complet qui déploie un modèle, consultez la page [Déploiement d’un modèle Azure Resource Manager](resource-manager-samples-cli-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e1601-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="e1601-188">toounderstand toodefine des paramètres dans votre modèle, voir [comprendre la structure de hello et syntaxe des modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e1601-188">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e1601-189">Pour obtenir des conseils sur la résolution des erreurs courantes de déploiement, consultez la page [Résolution des erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="e1601-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="e1601-190">Pour plus d’informations sur le déploiement d’un modèle qui nécessite un jeton SAP, consultez [Déploiement d’un modèle privé avec un jeton SAP](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="e1601-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="e1601-191">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="e1601-191">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
