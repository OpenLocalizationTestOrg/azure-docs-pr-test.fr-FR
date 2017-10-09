---
title: "modèles d’aaaLink pour le déploiement d’Azure | Documents Microsoft"
description: "Décrit comment toouse lié modèles dans un toocreate de modèle Azure Resource Manager, une solution de modèle modulaire. Montre comment les valeurs de paramètres toopass, spécifier un fichier de paramètres et créés de façon dynamique les URL."
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
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a><span data-ttu-id="00cb0-104">Utilisation de modèles liés lors du déploiement des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="00cb0-104">Using linked templates when deploying Azure resources</span></span>
<span data-ttu-id="00cb0-105">Dans un modèle Azure Resource Manager, vous pouvez lier de tooanother modèle, ce qui vous permet de toodecompose votre déploiement dans un ensemble de modèles ciblés, usage particulier.</span><span class="sxs-lookup"><span data-stu-id="00cb0-105">From within one Azure Resource Manager template, you can link tooanother template, which enables you toodecompose your deployment into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="00cb0-106">Tout comme la décomposition d’une application en plusieurs classes de codes, cette décomposition procure des avantages en matière de test, de réutilisation et de lisibilité.</span><span class="sxs-lookup"><span data-stu-id="00cb0-106">As with decomposing an application into several code classes, decomposition provides benefits in terms of testing, reuse, and readability.</span></span>  

<span data-ttu-id="00cb0-107">Vous pouvez passer des paramètres d’un modèle lié tooa de modèle principal, et ces paramètres capable de mapper directement tooparameters ou variables exposées par hello appelant le modèle.</span><span class="sxs-lookup"><span data-stu-id="00cb0-107">You can pass parameters from a main template tooa linked template, and those parameters can directly map tooparameters or variables exposed by hello calling template.</span></span> <span data-ttu-id="00cb0-108">modèle lié de Hello peut également passer un modèle de source de toohello précédent variable de sortie, l’activation d’un échange de données bidirectionnelle entre les modèles.</span><span class="sxs-lookup"><span data-stu-id="00cb0-108">hello linked template can also pass an output variable back toohello source template, enabling a two-way data exchange between templates.</span></span>

## <a name="linking-tooa-template"></a><span data-ttu-id="00cb0-109">Liaison de modèle de tooa</span><span class="sxs-lookup"><span data-stu-id="00cb0-109">Linking tooa template</span></span>
<span data-ttu-id="00cb0-110">Vous créez un lien entre les deux modèles en ajoutant une ressource de déploiement dans le modèle principal de hello points toohello modèle lié.</span><span class="sxs-lookup"><span data-stu-id="00cb0-110">You create a link between two templates by adding a deployment resource within hello main template that points toohello linked template.</span></span> <span data-ttu-id="00cb0-111">Vous définissez hello **templateLink** toohello de propriété URI de modèle lié de hello.</span><span class="sxs-lookup"><span data-stu-id="00cb0-111">You set hello **templateLink** property toohello URI of hello linked template.</span></span> <span data-ttu-id="00cb0-112">Vous pouvez fournir des valeurs de paramètre de modèle lié de hello directement dans votre modèle ou dans un fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="00cb0-112">You can provide parameter values for hello linked template directly in your template or in a parameter file.</span></span> <span data-ttu-id="00cb0-113">exemple Hello utilise hello **paramètres** propriété toospecify directement une valeur de paramètre.</span><span class="sxs-lookup"><span data-stu-id="00cb0-113">hello following example uses hello **parameters** property toospecify a parameter value directly.</span></span>

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

<span data-ttu-id="00cb0-114">Comme d’autres types de ressources, vous pouvez définir des dépendances entre les modèles liés hello et d’autres ressources.</span><span class="sxs-lookup"><span data-stu-id="00cb0-114">Like other resource types, you can set dependencies between hello linked template and other resources.</span></span> <span data-ttu-id="00cb0-115">Par conséquent, lorsque les autres ressources requièrent une valeur de sortie de modèle lié de hello, faire en sorte modèle lié de hello est déployé avant eux.</span><span class="sxs-lookup"><span data-stu-id="00cb0-115">Therefore, when other resources require an output value from hello linked template, you can make sure hello linked template is deployed before them.</span></span> <span data-ttu-id="00cb0-116">Ou, lorsque le modèle lié de hello s’appuie sur d’autres ressources, vous pouvez vous assurer qu'autres ressources sont déployées avant de modèle lié de hello.</span><span class="sxs-lookup"><span data-stu-id="00cb0-116">Or, when hello linked template relies on other resources, you can make sure other resources are deployed before hello linked template.</span></span> <span data-ttu-id="00cb0-117">Vous pouvez récupérer une valeur à partir d’un modèle lié avec hello selon la syntaxe :</span><span class="sxs-lookup"><span data-stu-id="00cb0-117">You can retrieve a value from a linked template with hello following syntax:</span></span>

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

<span data-ttu-id="00cb0-118">Hello service Gestionnaire de ressources doit être un modèle lié de tooaccess en mesure de hello.</span><span class="sxs-lookup"><span data-stu-id="00cb0-118">hello Resource Manager service must be able tooaccess hello linked template.</span></span> <span data-ttu-id="00cb0-119">Vous ne pouvez pas spécifier un fichier local ou un fichier qui est uniquement disponible sur votre réseau local pour le modèle lié de hello.</span><span class="sxs-lookup"><span data-stu-id="00cb0-119">You cannot specify a local file or a file that is only available on your local network for hello linked template.</span></span> <span data-ttu-id="00cb0-120">Vous pouvez seulement fournir une valeur URI qui inclut soit **http** soit **https**.</span><span class="sxs-lookup"><span data-stu-id="00cb0-120">You can only provide a URI value that includes either **http** or **https**.</span></span> <span data-ttu-id="00cb0-121">Une option consiste à tooplace votre modèle lié dans un compte de stockage et utilisez hello URI de cet élément, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="00cb0-121">One option is tooplace your linked template in a storage account, and use hello URI for that item, such as shown in hello following example:</span></span>

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

<span data-ttu-id="00cb0-122">Bien que le modèle lié de hello doit être disponible en externe, elle ne doit pas toobe toohello généralement disponible public.</span><span class="sxs-lookup"><span data-stu-id="00cb0-122">Although hello linked template must be externally available, it does not need toobe generally available toohello public.</span></span> <span data-ttu-id="00cb0-123">Vous pouvez ajouter votre compte de stockage privé tooa modèle qui est propriétaire du compte de stockage accessible tooonly hello.</span><span class="sxs-lookup"><span data-stu-id="00cb0-123">You can add your template tooa private storage account that is accessible tooonly hello storage account owner.</span></span> <span data-ttu-id="00cb0-124">Ensuite, vous créez un accès partagé (SAS) de signature jeton tooenable d’accéder au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="00cb0-124">Then, you create a shared access signature (SAS) token tooenable access during deployment.</span></span> <span data-ttu-id="00cb0-125">Vous ajoutez ce toohello jeton SAS URI pour le modèle lié de hello.</span><span class="sxs-lookup"><span data-stu-id="00cb0-125">You add that SAS token toohello URI for hello linked template.</span></span> <span data-ttu-id="00cb0-126">Pour connaître les étapes de configuration d’un modèle dans un compte de stockage et de génération d’un jeton SAP, consultez [Déployer des ressources avec des modèles Resource Manager et Azure PowerShell](resource-group-template-deploy.md) ou [Déployer des ressources avec des modèles Resource Manager et l’interface de ligne de commande Azure](resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="00cb0-126">For steps on setting up a template in a storage account and generating a SAS token, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) or [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> 

<span data-ttu-id="00cb0-127">Hello l’exemple suivant montre un modèle parent ce modèle tooanother de liens.</span><span class="sxs-lookup"><span data-stu-id="00cb0-127">hello following example shows a parent template that links tooanother template.</span></span> <span data-ttu-id="00cb0-128">modèle de lié Hello est accessible avec un jeton SAP qui est passé en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="00cb0-128">hello linked template is accessed with a SAS token that is passed in as a parameter.</span></span>

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

<span data-ttu-id="00cb0-129">Même si le jeton de hello est passé dans sous forme de chaîne sécurisée, hello URI de modèle lié hello, y compris le jeton SAS de hello, est enregistré dans les opérations de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="00cb0-129">Even though hello token is passed in as a secure string, hello URI of hello linked template, including hello SAS token, is logged in hello deployment operations.</span></span> <span data-ttu-id="00cb0-130">exposition de toolimit, définir un délai d’expiration pour le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="00cb0-130">toolimit exposure, set an expiration for hello token.</span></span>

<span data-ttu-id="00cb0-131">Resource Manager gère chaque modèle lié comme un déploiement séparé.</span><span class="sxs-lookup"><span data-stu-id="00cb0-131">Resource Manager handles each linked template as a separate deployment.</span></span> <span data-ttu-id="00cb0-132">Dans l’historique de déploiement hello pour le groupe de ressources hello, vous voyez des déploiements distincts pour le parent de hello et les modèles imbriqués.</span><span class="sxs-lookup"><span data-stu-id="00cb0-132">In hello deployment history for hello resource group, you see separate deployments for hello parent and nested templates.</span></span>

![historique des déploiements](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a><span data-ttu-id="00cb0-134">Fichier de paramètres de liaison tooa</span><span class="sxs-lookup"><span data-stu-id="00cb0-134">Linking tooa parameter file</span></span>
<span data-ttu-id="00cb0-135">Hello l’exemple suivant utilise hello **parametersLink** fichier de paramètres de propriété toolink tooa.</span><span class="sxs-lookup"><span data-stu-id="00cb0-135">hello next example uses hello **parametersLink** property toolink tooa parameter file.</span></span>

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

<span data-ttu-id="00cb0-136">Hello URI valeur pour le fichier de paramètres liés de hello ne peut pas être un fichier local et doit inclure **http** ou **https**.</span><span class="sxs-lookup"><span data-stu-id="00cb0-136">hello URI value for hello linked parameter file cannot be a local file, and must include either **http** or **https**.</span></span> <span data-ttu-id="00cb0-137">fichier de paramètres Hello peut également être limité tooaccess via un jeton SAP.</span><span class="sxs-lookup"><span data-stu-id="00cb0-137">hello parameter file can also be limited tooaccess through a SAS token.</span></span>

## <a name="using-variables-toolink-templates"></a><span data-ttu-id="00cb0-138">À l’aide de modèles de toolink de variables</span><span class="sxs-lookup"><span data-stu-id="00cb0-138">Using variables toolink templates</span></span>
<span data-ttu-id="00cb0-139">Hello les exemples précédents ont montré les valeurs d’URL codées en dur pour les liens de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="00cb0-139">hello previous examples showed hard-coded URL values for hello template links.</span></span> <span data-ttu-id="00cb0-140">Cette approche peut s’avérer efficace avec un modèle isolé, mais elle est incompatible avec le traitement d’un large ensemble des modèles modulaires.</span><span class="sxs-lookup"><span data-stu-id="00cb0-140">This approach might work for a simple template but it does not work well when working with a large set of modular templates.</span></span> <span data-ttu-id="00cb0-141">Au lieu de cela, vous pouvez créer une variable statique qui stocke une URL de base pour les modèles principal hello et créer dynamiquement des URL pour les modèles de hello lié à partir de cette URL de base.</span><span class="sxs-lookup"><span data-stu-id="00cb0-141">Instead, you can create a static variable that stores a base URL for hello main template and then dynamically create URLs for hello linked templates from that base URL.</span></span> <span data-ttu-id="00cb0-142">avantage Hello de cette approche est, vous pouvez facilement déplacer ou branchement de modèle de hello, car vous devez seulement variable statique de toochange hello dans les modèles principal hello.</span><span class="sxs-lookup"><span data-stu-id="00cb0-142">hello benefit of this approach is you can easily move or fork hello template because you only need toochange hello static variable in hello main template.</span></span> <span data-ttu-id="00cb0-143">les modèles principal Hello passe hello correct Qu'uri dans l’ensemble de hello décomposé de modèle.</span><span class="sxs-lookup"><span data-stu-id="00cb0-143">hello main template passes hello correct URIs throughout hello decomposed template.</span></span>

<span data-ttu-id="00cb0-144">Hello suivant montre comment toouse un toocreate URL base lié deux URL pour les modèles (**sharedTemplateUrl** et **vmTemplate**).</span><span class="sxs-lookup"><span data-stu-id="00cb0-144">hello following example shows how toouse a base URL toocreate two URLs for linked templates (**sharedTemplateUrl** and **vmTemplate**).</span></span> 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

<span data-ttu-id="00cb0-145">Vous pouvez également utiliser [le déploiement()](resource-group-template-functions-deployment.md#deployment) tooget hello URL de base pour le modèle actuel de hello et utiliser cette URL de hello tooget des autres modèles dans hello même emplacement.</span><span class="sxs-lookup"><span data-stu-id="00cb0-145">You can also use [deployment()](resource-group-template-functions-deployment.md#deployment) tooget hello base URL for hello current template, and use that tooget hello URL for other templates in hello same location.</span></span> <span data-ttu-id="00cb0-146">Cette approche est utile si votre emplacement de modèle change (peut-être due tooversioning) ou que vous souhaitiez tooavoid dur codage URL dans le fichier de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="00cb0-146">This approach is useful if your template location changes (maybe due tooversioning) or you want tooavoid hard coding URLs in hello template file.</span></span> 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a><span data-ttu-id="00cb0-147">Exemple complet</span><span class="sxs-lookup"><span data-stu-id="00cb0-147">Complete example</span></span>
<span data-ttu-id="00cb0-148">Hello suivant des exemples de modèles affiche une disposition simplifiée des modèles liés tooillustrate de plusieurs des concepts de hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="00cb0-148">hello following example templates show a simplified arrangement of linked templates tooillustrate several of hello concepts in this article.</span></span> <span data-ttu-id="00cb0-149">Il suppose que les modèles hello ont été ajoutées toohello même conteneur dans un compte de stockage avec un accès public désactivé.</span><span class="sxs-lookup"><span data-stu-id="00cb0-149">It assumes hello templates have been added toohello same container in a storage account with public access turned off.</span></span> <span data-ttu-id="00cb0-150">modèle lié de Hello transmet un modèle principal toohello arrière de valeur Bonjour **génère** section.</span><span class="sxs-lookup"><span data-stu-id="00cb0-150">hello linked template passes a value back toohello main template in hello **outputs** section.</span></span>

<span data-ttu-id="00cb0-151">Hello **parent.json** se compose de :</span><span class="sxs-lookup"><span data-stu-id="00cb0-151">hello **parent.json** file consists of:</span></span>

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

<span data-ttu-id="00cb0-152">Hello **helloworld.json** se compose de :</span><span class="sxs-lookup"><span data-stu-id="00cb0-152">hello **helloworld.json** file consists of:</span></span>

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

<span data-ttu-id="00cb0-153">Dans PowerShell, vous obtenez un jeton pour le conteneur de hello et déployez des modèles de hello avec :</span><span class="sxs-lookup"><span data-stu-id="00cb0-153">In PowerShell, you get a token for hello container and deploy hello templates with:</span></span>

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

<span data-ttu-id="00cb0-154">Dans Azure CLI 2.0, vous obtenez un jeton pour le conteneur de hello et déployez des modèles de hello avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="00cb0-154">In Azure CLI 2.0, you get a token for hello container and deploy hello templates with hello following code:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="00cb0-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="00cb0-155">Next steps</span></span>
* <span data-ttu-id="00cb0-156">toolearn sur hello définissant l’ordre de déploiement hello pour vos ressources, consultez [définition des dépendances dans les modèles Azure Resource Manager](resource-group-define-dependencies.md)</span><span class="sxs-lookup"><span data-stu-id="00cb0-156">toolearn about hello defining hello deployment order for your resources, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md)</span></span>
* <span data-ttu-id="00cb0-157">toolearn toodefine qu’une seule ressource créer mais de nombreuses instances de celui-ci, voir [créer plusieurs instances de ressources dans le Gestionnaire de ressources Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="00cb0-157">toolearn how toodefine one resource but create many instances of it, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>

