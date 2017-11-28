---
title: "aaaDeploy une application web qui est lié le référentiel GitHub de tooa | Documents Microsoft"
description: "Utilisez un toodeploy de modèle Azure Resource Manager une application web qui contient un projet à partir d’un référentiel GitHub."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a><span data-ttu-id="bee73-103">Déployer un référentiel GitHub de web application lié tooa</span><span class="sxs-lookup"><span data-stu-id="bee73-103">Deploy a web app linked tooa GitHub repository</span></span>
<span data-ttu-id="bee73-104">Dans cette rubrique, vous allez apprendre comment toocreate un modèle Azure Resource Manager qui déploie une application web qui est lié à project tooa dans un référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="bee73-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys a web app that is linked tooa project in a GitHub repository.</span></span> <span data-ttu-id="bee73-105">Vous allez apprendre comment toodefine les ressources qui sont déployés et comment les paramètres toodefine sont spécifiés lorsque le déploiement de hello est exécutée.</span><span class="sxs-lookup"><span data-stu-id="bee73-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="bee73-106">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins.</span><span class="sxs-lookup"><span data-stu-id="bee73-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="bee73-107">Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="bee73-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="bee73-108">Pour le modèle complète de hello, consultez [Web application lié tooGitHub modèle](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="bee73-108">For hello complete template, see [Web App Linked tooGitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="bee73-109">Ce que vous allez déployer</span><span class="sxs-lookup"><span data-stu-id="bee73-109">What you will deploy</span></span>
<span data-ttu-id="bee73-110">Avec ce modèle, vous allez déployer une application web qui contient le code hello à partir d’un projet dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="bee73-110">With this template, you will deploy a web app that contains hello code from a project in GitHub.</span></span>

<span data-ttu-id="bee73-111">toorun hello déploiement automatiquement, cliquez sur hello suivant bouton :</span><span class="sxs-lookup"><span data-stu-id="bee73-111">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="bee73-112">[![Déployer tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="bee73-112">[![Deploy tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="bee73-113">Paramètres</span><span class="sxs-lookup"><span data-stu-id="bee73-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="bee73-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="bee73-114">repoURL</span></span>
<span data-ttu-id="bee73-115">URL de Hello pour le référentiel GitHub qui contient les hello projet toodeploy.</span><span class="sxs-lookup"><span data-stu-id="bee73-115">hello URL for GitHub repository that contains hello project toodeploy.</span></span> <span data-ttu-id="bee73-116">Ce paramètre contient une valeur par défaut, mais cette valeur est uniquement prévue tooshow vous comment tooprovide hello URL du référentiel.</span><span class="sxs-lookup"><span data-stu-id="bee73-116">This parameter contains a default value but this value is only intended tooshow you how tooprovide hello URL for repository.</span></span> <span data-ttu-id="bee73-117">Vous pouvez utiliser cette valeur lorsque le test de modèle de hello, mais vous pouvez tooprovide hello URL votre propre référentiel lorsque vous travaillez avec un modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="bee73-117">You can use this value when testing hello template but you will want tooprovide hello URL your own repository when working with hello template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="bee73-118">branche</span><span class="sxs-lookup"><span data-stu-id="bee73-118">branch</span></span>
<span data-ttu-id="bee73-119">branche Hello de hello référentiel toouse lors du déploiement d’application hello.</span><span class="sxs-lookup"><span data-stu-id="bee73-119">hello branch of hello repository toouse when deploying hello application.</span></span> <span data-ttu-id="bee73-120">la valeur par défaut Hello est master, mais vous pouvez fournir nom hello de n’importe quelle branche dans le référentiel de hello que vous souhaitez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="bee73-120">hello default value is master, but you can provide hello name of any branch in hello repository that you wish toodeploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="bee73-121">Ressources toodeploy</span><span class="sxs-lookup"><span data-stu-id="bee73-121">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="bee73-122">Application web</span><span class="sxs-lookup"><span data-stu-id="bee73-122">Web app</span></span>
<span data-ttu-id="bee73-123">Crée l’application hello web qui est le projet toohello lié dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="bee73-123">Creates hello web app that is linked toohello project in GitHub.</span></span> 

<span data-ttu-id="bee73-124">Vous spécifiez le nom hello de l’application web via hello hello **siteName** paramètre et l’emplacement de hello de l’application web via hello hello **sitelocation correspond** paramètre.</span><span class="sxs-lookup"><span data-stu-id="bee73-124">You specify hello name of hello web app through hello **siteName** parameter, and hello location of hello web app through hello **siteLocation** parameter.</span></span> <span data-ttu-id="bee73-125">Bonjour **dependsOn** élément, modèle de hello définit hello web application en tant que dépendant du service hello plan d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="bee73-125">In hello **dependsOn** element, hello template defines hello web app as dependent on hello service hosting plan.</span></span> <span data-ttu-id="bee73-126">Comme il est dépendant de hello plan d’hébergement, hello web app n’est pas créé tant que plan d’hébergement de hello est en cours de création.</span><span class="sxs-lookup"><span data-stu-id="bee73-126">Because it is dependent on hello hosting plan, hello web app is not created until hello hosting plan has finished being created.</span></span> <span data-ttu-id="bee73-127">Hello **dependsOn** élément est uniquement un ordre de déploiement toospecify utilisé.</span><span class="sxs-lookup"><span data-stu-id="bee73-127">hello **dependsOn** element is only used toospecify deployment order.</span></span> <span data-ttu-id="bee73-128">Si vous ne marquez pas une application web hello comme dépendant de plan d’hébergement hello, Azure Resource Manager va tenter de toocreate les ressources à hello même temps et que vous receviez une erreur si l’application web hello est créée avant hello plan d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="bee73-128">If you do not mark hello web app as dependent on hello hosting plan, Azure Resource Mananger will attempt toocreate both resources at hello same time and you may receive an error if hello web app is created before hello hosting plan.</span></span>

<span data-ttu-id="bee73-129">l’application Hello web a également une ressource enfant qui est définie dans **ressources** section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bee73-129">hello web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="bee73-130">Cette ressource enfant définit le contrôle de code source pour le projet hello déployé avec l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="bee73-130">This child resource defines source control for hello project deployed with hello web app.</span></span> <span data-ttu-id="bee73-131">Dans ce modèle, contrôle de code source hello est le référentiel GitHub particulier de tooa lié.</span><span class="sxs-lookup"><span data-stu-id="bee73-131">In this template, hello source control is linked tooa particular GitHub repository.</span></span> <span data-ttu-id="bee73-132">référentiel GitHub de Hello est défini avec le code de hello **« RepoUrl » : « https://github.com/davidebbo-test/Mvc52Application.git »** vous pouvez coder en dur hello URL du référentiel lorsque vous souhaitez toocreate un modèle à plusieurs reprises déploie un projet unique tout en exigeant le nombre minimal de hello de paramètres.</span><span class="sxs-lookup"><span data-stu-id="bee73-132">hello GitHub repository is defined with hello code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code hello repository URL when you want toocreate a template that repeatedly deploys a single project while requiring hello minimum number of parameters.</span></span>
<span data-ttu-id="bee73-133">Au lieu de coder en dur hello URL du référentiel, vous pouvez ajouter un paramètre d’URL du référentiel hello et utilisez cette valeur pour hello **RepoUrl** propriété.</span><span class="sxs-lookup"><span data-stu-id="bee73-133">Instead of hard-coding hello repository URL, you can add a parameter for hello repository URL and use that value for hello **RepoUrl** property.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a><span data-ttu-id="bee73-134">Déploiement de toorun de commandes</span><span class="sxs-lookup"><span data-stu-id="bee73-134">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="bee73-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bee73-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="bee73-136">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="bee73-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="bee73-137">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bee73-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="bee73-138">Pour le contenu du fichier JSON de paramètres hello, consultez [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="bee73-138">For content of hello parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

