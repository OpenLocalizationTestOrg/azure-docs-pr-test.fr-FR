---
title: "Déployer une application Web liée à un référentiel GitHub | Microsoft Docs"
description: "Utiliser un modèle Azure Resource Manager pour déployer une application Web qui contient un projet issu d'un référentiel GitHub."
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
ms.openlocfilehash: 77064802814296d0c21f004534e4264d2f97252e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-web-app-linked-to-a-github-repository"></a><span data-ttu-id="3bd30-103">Déployer une application Web liée à un référentiel GitHub</span><span class="sxs-lookup"><span data-stu-id="3bd30-103">Deploy a web app linked to a GitHub repository</span></span>
<span data-ttu-id="3bd30-104">Dans cette rubrique, vous allez apprendre à créer un modèle Azure Resource Manager qui déploie une application Web liée à un projet dans un référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="3bd30-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys a web app that is linked to a project in a GitHub repository.</span></span> <span data-ttu-id="3bd30-105">Vous allez apprendre comment définir les ressources à déployer et configurer les paramètres qui sont spécifiés lors de l’exécution du déploiement.</span><span class="sxs-lookup"><span data-stu-id="3bd30-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="3bd30-106">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou le personnaliser afin qu’il réponde à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="3bd30-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="3bd30-107">Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3bd30-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="3bd30-108">Pour le modèle complet, consultez [Application Web liée au modèle GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="3bd30-108">For the complete template, see [Web App Linked to GitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="3bd30-109">Ce que vous allez déployer</span><span class="sxs-lookup"><span data-stu-id="3bd30-109">What you will deploy</span></span>
<span data-ttu-id="3bd30-110">Avec ce modèle, vous allez déployer une application Web qui contient le code d'un projet dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="3bd30-110">With this template, you will deploy a web app that contains the code from a project in GitHub.</span></span>

<span data-ttu-id="3bd30-111">Pour exécuter automatiquement le déploiement, cliquez sur le bouton ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3bd30-111">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="3bd30-112">[![Déploiement sur Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="3bd30-112">[![Deploy to Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="3bd30-113">Paramètres</span><span class="sxs-lookup"><span data-stu-id="3bd30-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="3bd30-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="3bd30-114">repoURL</span></span>
<span data-ttu-id="3bd30-115">L'URL du référentiel GitHub qui contient le projet à déployer.</span><span class="sxs-lookup"><span data-stu-id="3bd30-115">The URL for GitHub repository that contains the project to deploy.</span></span> <span data-ttu-id="3bd30-116">Ce paramètre contient une valeur par défaut, mais cette valeur est uniquement destinée à vous montrer comment fournir l'URL du référentiel.</span><span class="sxs-lookup"><span data-stu-id="3bd30-116">This parameter contains a default value but this value is only intended to show you how to provide the URL for repository.</span></span> <span data-ttu-id="3bd30-117">Vous pouvez utiliser cette valeur lorsque vous testez le modèle, mais vous devrez fournir l'URL de votre propre référentiel lors de l'utilisation du modèle.</span><span class="sxs-lookup"><span data-stu-id="3bd30-117">You can use this value when testing the template but you will want to provide the URL your own repository when working with the template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="3bd30-118">branche</span><span class="sxs-lookup"><span data-stu-id="3bd30-118">branch</span></span>
<span data-ttu-id="3bd30-119">La branche du référentiel à utiliser lors du déploiement de l'application.</span><span class="sxs-lookup"><span data-stu-id="3bd30-119">The branch of the repository to use when deploying the application.</span></span> <span data-ttu-id="3bd30-120">La valeur par défaut est master, mais vous pouvez fournir le nom de n'importe quelle branche dans le référentiel que vous souhaitez déployer.</span><span class="sxs-lookup"><span data-stu-id="3bd30-120">The default value is master, but you can provide the name of any branch in the repository that you wish to deploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="3bd30-121">Ressources à déployer</span><span class="sxs-lookup"><span data-stu-id="3bd30-121">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="3bd30-122">Application web</span><span class="sxs-lookup"><span data-stu-id="3bd30-122">Web app</span></span>
<span data-ttu-id="3bd30-123">Crée l'application Web qui est liée au projet dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="3bd30-123">Creates the web app that is linked to the project in GitHub.</span></span> 

<span data-ttu-id="3bd30-124">Vous spécifiez le nom de l’application web par le biais du paramètre **siteName** et l’emplacement de l’application web par le biais du paramètre **siteLocation**.</span><span class="sxs-lookup"><span data-stu-id="3bd30-124">You specify the name of the web app through the **siteName** parameter, and the location of the web app through the **siteLocation** parameter.</span></span> <span data-ttu-id="3bd30-125">Dans l'élément **dependsOn** , le modèle définit l'application Web comme dépendante du plan d'hébergement de service.</span><span class="sxs-lookup"><span data-stu-id="3bd30-125">In the **dependsOn** element, the template defines the web app as dependent on the service hosting plan.</span></span> <span data-ttu-id="3bd30-126">Étant donné qu'elle dépend du plan d'hébergement, l'application Web n'est pas créée tant que le plan d'hébergement est en cours de création.</span><span class="sxs-lookup"><span data-stu-id="3bd30-126">Because it is dependent on the hosting plan, the web app is not created until the hosting plan has finished being created.</span></span> <span data-ttu-id="3bd30-127">L'élément **dependsOn** est uniquement utilisé pour spécifier l'ordre de déploiement.</span><span class="sxs-lookup"><span data-stu-id="3bd30-127">The **dependsOn** element is only used to specify deployment order.</span></span> <span data-ttu-id="3bd30-128">Si vous ne marquez pas l'application Web comme dépendante du plan d'hébergement, Azure Resource Manager tentera de créer les deux ressources en même temps et vous pourriez recevoir une erreur si l'application Web est créée avant le plan d'hébergement.</span><span class="sxs-lookup"><span data-stu-id="3bd30-128">If you do not mark the web app as dependent on the hosting plan, Azure Resource Mananger will attempt to create both resources at the same time and you may receive an error if the web app is created before the hosting plan.</span></span>

<span data-ttu-id="3bd30-129">L'application Web a également une ressource enfant qui est définie dans la section des **ressources** ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3bd30-129">The web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="3bd30-130">Cette ressource enfant définit le contrôle de code source pour le projet déployé avec l'application Web.</span><span class="sxs-lookup"><span data-stu-id="3bd30-130">This child resource defines source control for the project deployed with the web app.</span></span> <span data-ttu-id="3bd30-131">Dans ce modèle, le contrôle de code source est lié à un référentiel GitHub particulier.</span><span class="sxs-lookup"><span data-stu-id="3bd30-131">In this template, the source control is linked to a particular GitHub repository.</span></span> <span data-ttu-id="3bd30-132">Le référentiel GitHub est défini avec le code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** Vous pouvez coder en dur l'URL du référentiel lorsque vous souhaitez créer un modèle qui déploie de façon répétée un projet unique tout en nécessitant le nombre minimal de paramètres.</span><span class="sxs-lookup"><span data-stu-id="3bd30-132">The GitHub repository is defined with the code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code the repository URL when you want to create a template that repeatedly deploys a single project while requiring the minimum number of parameters.</span></span>
<span data-ttu-id="3bd30-133">Au lieu de coder en dur l'URL du référentiel, vous pouvez ajouter un paramètre pour l'URL du référentiel et utiliser cette valeur pour la propriété **RepoUrl** .</span><span class="sxs-lookup"><span data-stu-id="3bd30-133">Instead of hard-coding the repository URL, you can add a parameter for the repository URL and use that value for the **RepoUrl** property.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="3bd30-134">Commandes pour l’exécution du déploiement</span><span class="sxs-lookup"><span data-stu-id="3bd30-134">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="3bd30-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3bd30-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="3bd30-136">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="3bd30-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="3bd30-137">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3bd30-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="3bd30-138">Pour le contenu du fichier de paramètres JSON, consultez [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="3bd30-138">For content of the parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

