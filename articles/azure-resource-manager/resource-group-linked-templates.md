---
title: "Lier des modèles pour un déploiement Azure | Microsoft Docs"
description: "Décrit comment utiliser des modèles liés dans un modèle Azure Resource Manager afin de créer une solution de modèle modulaire. Indique comment transmettre des valeurs de paramètres, spécifier un fichier de paramètres et créer dynamiquement des URL."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: 8b58a83ffd473500dd3f76c09e251f9208527d4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="8074b-104">Utilisation de modèles liés lors du déploiement des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="8074b-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="8074b-105">À partir d’un modèle Azure Resource Manager, vous pouvez établir un lien avec un autre modèle, ce qui vous permet le cas échéant de décomposer votre déploiement en un ensemble de modèles ciblés, dédiés.</span><span class="sxs-lookup"><span data-stu-id="8074b-105">From within one Azure Resource Manager template, you can link to another template, which enables you to decompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="8074b-106">Tout comme la décomposition d’une application en plusieurs classes de codes, cette décomposition procure des avantages en matière de test, de réutilisation et de lisibilité.</span><span class="sxs-lookup"><span data-stu-id="8074b-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="8074b-107">Vous pouvez déplacer des paramètres d’un modèle principal à un modèle lié. Ces paramètres peuvent être directement mappés sur des paramètres ou des variables exposés par le modèle d’appel.</span><span class="sxs-lookup"><span data-stu-id="8074b-107">You can pass parameters from a main template to a linked template, and those parameters can directly map to parameters or variables exposed by the calling template.</span></span> <span data-ttu-id="8074b-108">Le modèle lié peut également retransmettre une variable de sortie vers le modèle source, permettant ainsi un échange bidirectionnel de données entre les modèles.</span><span class="sxs-lookup"><span data-stu-id="8074b-108">The linked template can also pass an output variable back to the source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-to-a-template"></a><span data-ttu-id="8074b-109">Liaison à un modèle</span><span class="sxs-lookup"><span data-stu-id="8074b-109">Linking to a template</span></span>
<span data-ttu-id="8074b-110">Pour créer un lien entre deux modèles, ajoutez une ressource de déploiement dans le modèle principal pointant vers le modèle lié.</span><span class="sxs-lookup"><span data-stu-id="8074b-110">You create a link between two templates by adding a deployment resource within the main template that points to the linked template.</span></span> <span data-ttu-id="8074b-111">Vous définissez la propriété **templateLink** à l’URI du modèle lié.</span><span class="sxs-lookup"><span data-stu-id="8074b-111">You set the **templateLink** property to the URI of the linked template.</span></span> <span data-ttu-id="8074b-112">Vous pouvez fournir des valeurs de paramètres pour le modèle lié directement dans votre modèle ou dans un fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="8074b-112">You can provide parameter values for the linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="8074b-113">L’exemple suivant utilise la propriété **parameters** afin de spécifier directement une valeur de paramètre.</span><span class="sxs-lookup"><span data-stu-id="8074b-113">The following example uses the **parameters** property to specify a parameter value directly.</span></span>

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

<span data-ttu-id="8074b-114">Comme pour d’autres types de ressources, vous pouvez définir des dépendances entre le modèle lié et d’autres ressources.</span><span class="sxs-lookup"><span data-stu-id="8074b-114">Like other resource types, you can set dependencies between the linked template and other resources.</span></span> <span data-ttu-id="8074b-115">Par conséquent, lorsque d’autres ressources requièrent une valeur de sortie à partir du modèle lié, vous pouvez vous assurer que le modèle lié est déployé avant celles-ci.</span><span class="sxs-lookup"><span data-stu-id="8074b-115">Therefore, when other resources require an output value from the linked template, you can make sure the linked template is deployed before them.</span></span> <span data-ttu-id="8074b-116">Sinon, lorsque le modèle lié s’appuie sur d’autres ressources, vous pouvez vous assurer que d’autres ressources sont déployées avant le modèle lié.</span><span class="sxs-lookup"><span data-stu-id="8074b-116">Or, when the linked template relies on other resources, you can make sure other resources are deployed before the linked template.</span></span> <span data-ttu-id="8074b-117">Vous pouvez récupérer une valeur à partir d’un modèle lié avec la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="8074b-117">You can retrieve a value from a linked template with the following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="8074b-118">Le service Resource Manager doit être en mesure d’accéder au modèle lié.</span><span class="sxs-lookup"><span data-stu-id="8074b-118">The Resource Manager service must be able to access the linked template.</span></span> <span data-ttu-id="8074b-119">Vous ne pouvez pas spécifier un fichier local ou un fichier uniquement disponible sur votre réseau local pour le modèle lié.</span><span class="sxs-lookup"><span data-stu-id="8074b-119">You cannot specify a local file or a file that is only available on your local network for the linked template.</span></span> <span data-ttu-id="8074b-120">Vous pouvez seulement fournir une valeur URI qui inclut soit **http** soit **https**.</span><span class="sxs-lookup"><span data-stu-id="8074b-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="8074b-121">Une possibilité consiste à placer votre modèle lié dans un compte de stockage et à utiliser l’URI de cet élément, comme illustré ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8074b-121">One option is to place your linked template in a storage account, and use the URI for that item, such as shown in the following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="8074b-122">Bien que le modèle lié doive être disponible en externe, il n’a pas besoin d’être accessible au public.</span><span class="sxs-lookup"><span data-stu-id="8074b-122">Although the linked template must be externally available, it does not need to be generally available to the public.</span></span> <span data-ttu-id="8074b-123">Vous pouvez ajouter votre modèle dans un compte de stockage privé, uniquement accessible au propriétaire du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8074b-123">You can add your template to a private storage account that is accessible to only the storage account owner.</span></span> <span data-ttu-id="8074b-124">Ensuite, vous créez un jeton de signature d’accès partagé (SAP) pour autoriser l’accès en cours de déploiement.</span><span class="sxs-lookup"><span data-stu-id="8074b-124">Then, you create a shared access signature (SAS) token to enable access during deployment.</span></span> <span data-ttu-id="8074b-125">Vous ajoutez ce jeton SAP à l’URI pour le modèle lié.</span><span class="sxs-lookup"><span data-stu-id="8074b-125">You add that SAS token to the URI for the linked template.</span></span> <span data-ttu-id="8074b-126">Pour connaître les étapes de configuration d’un modèle dans un compte de stockage et de génération d’un jeton SAP, consultez [Déployer des ressources avec des modèles Resource Manager et Azure PowerShell](resource-group-template-deploy.md) ou [Déployer des ressources avec des modèles Resource Manager et l’interface de ligne de commande Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8074b-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="8074b-127">L’exemple suivant montre un modèle parent lié à un autre modèle.</span><span class="sxs-lookup"><span data-stu-id="8074b-127">The following example shows a parent template that links to another template.</span></span> <span data-ttu-id="8074b-128">Le modèle lié est accessible avec un jeton SAP qui est transmis en tant paramètre.</span><span class="sxs-lookup"><span data-stu-id="8074b-128">The linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

<span data-ttu-id="8074b-129">Même si le jeton est transmis sous forme de chaîne sécurisée, l’URI du modèle lié, y compris le jeton SAP, est enregistré dans les opérations de déploiement.</span><span class="sxs-lookup"><span data-stu-id="8074b-129">Even though the token is passed in as a secure string, the URI of the linked template, including the SAS token, is logged in the deployment operations.</span></span> <span data-ttu-id="8074b-130">Pour limiter l’exposition, définissez un délai d’expiration pour le jeton.</span><span class="sxs-lookup"><span data-stu-id="8074b-130">To limit exposure, set an expiration for the token.</span></span>

<span data-ttu-id="8074b-131">Resource Manager gère chaque modèle lié comme un déploiement séparé.</span><span class="sxs-lookup"><span data-stu-id="8074b-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="8074b-132">Dans l’historique de déploiement du groupe de ressources, vous voyez des déploiements distincts pour les modèles parents et imbriqués.</span><span class="sxs-lookup"><span data-stu-id="8074b-132">In the deployment history for the resource group, you see separate deployments for the parent and nested templates.</span></span>

![historique des déploiements](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-to-a-parameter-file"></a><span data-ttu-id="8074b-134">Liaison à un fichier de paramètres</span><span class="sxs-lookup"><span data-stu-id="8074b-134">Linking to a parameter file</span></span>
<span data-ttu-id="8074b-135">L’exemple suivant utilise la propriété **parametersLink** pour créer un lien vers un fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="8074b-135">The next example uses the **parametersLink** property to link to a parameter file.</span></span>

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

<span data-ttu-id="8074b-136">La valeur d’URI pour le fichier de paramètres liés ne peut pas être un fichier local et doit inclure **http** ou **https**.</span><span class="sxs-lookup"><span data-stu-id="8074b-136">The URI value for the linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="8074b-137">Le fichier de paramètres peut également être limité à l’accès avec un jeton SAP.</span><span class="sxs-lookup"><span data-stu-id="8074b-137">The parameter file can also be limited to access through a SAS token.</span></span>

## <a name="using-variables-to-link-templates"></a><span data-ttu-id="8074b-138">Utilisation de variables pour lier des modèles</span><span class="sxs-lookup"><span data-stu-id="8074b-138">Using variables to link templates</span></span>
<span data-ttu-id="8074b-139">Les exemples précédents représentaient des valeurs d’URL codées en dur pour les liens de modèle.</span><span class="sxs-lookup"><span data-stu-id="8074b-139">The previous examples showed hard-coded URL values for the template links.</span></span> <span data-ttu-id="8074b-140">Cette approche peut s’avérer efficace avec un modèle isolé, mais elle est incompatible avec le traitement d’un large ensemble des modèles modulaires.</span><span class="sxs-lookup"><span data-stu-id="8074b-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="8074b-141">Au lieu de cela, vous pouvez créer une variable statique qui stocke une URL de base pour le modèle principal, avant de créer dynamiquement les URL pour les modèles liés à partir de cette URL de base.</span><span class="sxs-lookup"><span data-stu-id="8074b-141">Instead, you can create a static variable that stores a base URL for the main template and then dynamically create URLs for the linked templates from that base URL.</span></span> <span data-ttu-id="8074b-142">Cette approche permet notamment de déplacer ou de répliquer facilement le modèle. En effet, il vous suffit de modifier la variable statique dans le modèle principal.</span><span class="sxs-lookup"><span data-stu-id="8074b-142">The benefit of this approach is you can easily move or fork the template because you only need to change the static variable in the main template.</span></span> <span data-ttu-id="8074b-143">Le modèle principal transmet les URI appropriés au modèle décomposé.</span><span class="sxs-lookup"><span data-stu-id="8074b-143">The main template passes the correct URIs throughout the decomposed template.</span></span>

<span data-ttu-id="8074b-144">L’exemple suivant indique comment utiliser une URL de base afin de créer deux URL pour des modèles liés (**sharedTemplateUrl** et **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="8074b-144">The following example shows how to use a base URL to create two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="8074b-145">Vous pouvez également utiliser [deployment()](resource-group-template-functions-deployment.md#deployment) pour obtenir l’URL de base pour le modèle actuel, qui permet d’obtenir l’URL d’autres modèles dans le même emplacement.</span><span class="sxs-lookup"><span data-stu-id="8074b-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) to get the base URL for the current template, and use that to get the URL for other templates in the same location.</span></span> <span data-ttu-id="8074b-146">Cette approche est utile si l’emplacement des modèles change (à cause des versions notamment) ou si vous voulez éviter de coder en dur les URL dans le fichier de modèle.</span><span class="sxs-lookup"><span data-stu-id="8074b-146">This approach is useful if your template location changes (maybe due to versioning) or you want to avoid hard coding URLs in the template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="8074b-147">Exemple complet</span><span class="sxs-lookup"><span data-stu-id="8074b-147">Complete example</span></span>
<span data-ttu-id="8074b-148">Les exemples de modèles suivants montrent une disposition simplifiée des modèles liés pour illustrer certains des concepts décrits dans cet article.</span><span class="sxs-lookup"><span data-stu-id="8074b-148">The following example templates show a simplified arrangement of linked templates to illustrate several of the concepts in this article.</span></span> <span data-ttu-id="8074b-149">Ils partent du principe que les modèles ont été ajoutés au même conteneur dans un compte de stockage dont l’accès public est désactivé.</span><span class="sxs-lookup"><span data-stu-id="8074b-149">It assumes the templates have been added to the same container in a storage account with public access turned off.</span></span> <span data-ttu-id="8074b-150">Le modèle lié retransmet une valeur au modèle principal dans la section **outputs** .</span><span class="sxs-lookup"><span data-stu-id="8074b-150">The linked template passes a value back to the main template in the **outputs** section.</span></span>

<span data-ttu-id="8074b-151">Le fichier **parent.json** est composé de :</span><span class="sxs-lookup"><span data-stu-id="8074b-151">The **parent.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

<span data-ttu-id="8074b-152">Le fichier **helloworld.json** est composé de :</span><span class="sxs-lookup"><span data-stu-id="8074b-152">The **helloworld.json** file consists of:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

<span data-ttu-id="8074b-153">Dans PowerShell, vous obtenez un jeton pour le conteneur et déployez les modèles avec :</span><span class="sxs-lookup"><span data-stu-id="8074b-153">In PowerShell, you get a token for the container and deploy the templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="8074b-154">Dans Azure CLI 2.0, vous obtenez un jeton pour le conteneur et déployez les modèles avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="8074b-154">In Azure CLI 2.0, you get a token for the container and deploy the templates with the following code:</span></span>

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a><span data-ttu-id="8074b-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8074b-155">Next steps</span></span>
* <span data-ttu-id="8074b-156">Pour obtenir des informations sur la définition de l’ordre de déploiement de vos ressources, consultez [Définition de dépendances dans les modèles Azure Resource Manager](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="8074b-156">To learn about the defining the deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="8074b-157">Pour savoir comment définir une seule ressource mais également créer de nombreuses instances de cette dernière, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="8074b-157">To learn how to define one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

