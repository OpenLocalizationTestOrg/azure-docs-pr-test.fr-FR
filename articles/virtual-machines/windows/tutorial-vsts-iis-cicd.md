---
title: "aaaCreate un pipeline de l’élément de configuration/CD dans Azure avec Team Services | Documents Microsoft"
description: "Découvrez comment toocreate un Visual Studio Team Services pipeline pour l’intégration continue et de remise qui déploie un tooIIS d’application web sur une machine virtuelle Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b758a124c4742854dd3b543f747fd8700f954414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="d583e-103">Création d’un pipeline d’intégration continue avec Visual Studio Team Services et IIS</span><span class="sxs-lookup"><span data-stu-id="d583e-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="d583e-104">génération de hello tooautomate, de test et des phases de déploiement du développement d’applications, vous pouvez utiliser une intégration continue et le pipeline de déploiement de (l’élément de configuration/CD).</span><span class="sxs-lookup"><span data-stu-id="d583e-104">tooautomate hello build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="d583e-105">Dans ce didacticiel, vous créez un pipeline CI/CD à l’aide de Visual Studio Team Services et d’une machine virtuelle Windows (VM) dans Azure qui exécute IIS.</span><span class="sxs-lookup"><span data-stu-id="d583e-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="d583e-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="d583e-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d583e-107">Publier un projet d’équipe Services ASP.NET web application tooa</span><span class="sxs-lookup"><span data-stu-id="d583e-107">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="d583e-108">Créer une définition de build qui est déclenchée par les validations de code</span><span class="sxs-lookup"><span data-stu-id="d583e-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="d583e-109">Installer et configurer IIS sur une machine virtuelle dans Azure</span><span class="sxs-lookup"><span data-stu-id="d583e-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="d583e-110">Ajouter un groupe de déploiement hello tooa de l’instance IIS dans Team Services</span><span class="sxs-lookup"><span data-stu-id="d583e-110">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="d583e-111">Créez une version définition toopublish web tooIIS de packages de déploiement</span><span class="sxs-lookup"><span data-stu-id="d583e-111">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="d583e-112">Tester le pipeline de l’élément de configuration/CD hello</span><span class="sxs-lookup"><span data-stu-id="d583e-112">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="d583e-113">Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module.</span><span class="sxs-lookup"><span data-stu-id="d583e-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="d583e-114">Exécutez `Get-Module -ListAvailable AzureRM` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="d583e-114">Run `Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="d583e-115">Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="d583e-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="d583e-116">Création d’un projet dans Team Services</span><span class="sxs-lookup"><span data-stu-id="d583e-116">Create project in Team Services</span></span>
<span data-ttu-id="d583e-117">Visual Studio Team Services simplifie la collaboration et permet le développement sans recours à une solution de gestion de code en local.</span><span class="sxs-lookup"><span data-stu-id="d583e-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="d583e-118">Team Services offre des fonctionnalités de test de code, de création et d’analyse de l’application dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="d583e-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="d583e-119">Vous pouvez choisir le référentiel de contrôle de version et l’IDE qui conviennent le mieux au développement de votre code.</span><span class="sxs-lookup"><span data-stu-id="d583e-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="d583e-120">Pour ce didacticiel, vous pouvez utiliser un compte gratuit toocreate une base d’application web ASP.NET et le pipeline de l’élément de configuration/CD.</span><span class="sxs-lookup"><span data-stu-id="d583e-120">For this tutorial, you can use a free account toocreate a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="d583e-121">Si vous n’avez pas encore de compte Team Services, [créez-en un](http://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="d583e-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="d583e-122">processus de validation code toomanage hello, définitions de build et définitions de version, créez un projet dans Team Services, comme suit :</span><span class="sxs-lookup"><span data-stu-id="d583e-122">toomanage hello code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="d583e-123">Ouvrez votre tableau de bord Team Services dans un navigateur web et choisissez **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="d583e-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="d583e-124">Entrez *myWebApp* pour hello **nom du projet**.</span><span class="sxs-lookup"><span data-stu-id="d583e-124">Enter *myWebApp* for hello **Project name**.</span></span> <span data-ttu-id="d583e-125">Laissez toutes les autres toouse de valeurs par défaut *Git* contrôle de version et *Agile* processus de l’élément de travail.</span><span class="sxs-lookup"><span data-stu-id="d583e-125">Leave all other default values toouse *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="d583e-126">Choisir hello trop**partager avec** *membres de l’équipe*, puis sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="d583e-126">Choose hello option too**Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="d583e-127">Une fois que votre projet a été créé, choisir hello trop**initialiser avec un fichier Lisez-moi ou la gitignore**, puis **initialiser**.</span><span class="sxs-lookup"><span data-stu-id="d583e-127">Once your project has been created, choose hello option too**Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="d583e-128">À l’intérieur de votre nouveau projet, choisissez **tableaux de bord** haut de hello, puis sélectionnez **ouvert dans Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="d583e-128">Inside your new project, choose **Dashboards** across hello top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="d583e-129">Création d’une application web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d583e-129">Create ASP.NET web application</span></span>
<span data-ttu-id="d583e-130">Dans l’étape précédente de hello, vous avez créé un projet dans Team Services.</span><span class="sxs-lookup"><span data-stu-id="d583e-130">In hello previous step, you created a project in Team Services.</span></span> <span data-ttu-id="d583e-131">étape finale de Hello ouvre votre nouveau projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d583e-131">hello final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="d583e-132">Vous gérez vos validations code Bonjour **Team Explorer** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d583e-132">You manage your code commits in hello **Team Explorer** window.</span></span> <span data-ttu-id="d583e-133">Créez une copie locale de votre nouveau projet, puis créez une application web ASP.NET à partir d’un modèle comme suit :</span><span class="sxs-lookup"><span data-stu-id="d583e-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="d583e-134">Sélectionnez **Clone** toocreate un référentiel git local de votre projet Team Services.</span><span class="sxs-lookup"><span data-stu-id="d583e-134">Select **Clone** toocreate a local git repo of your Team Services project.</span></span>
    
    ![Clonage du référentiel à partir du projet Team Services](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="d583e-136">Sous **Solutions**, sélectionnez **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="d583e-136">Under **Solutions**, select **New**.</span></span>

    ![Création de la solution d’application web](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="d583e-138">Sélectionnez **Web** modèles, puis choisissez hello **Application Web ASP.NET** modèle.</span><span class="sxs-lookup"><span data-stu-id="d583e-138">Select **Web** templates, and then choose hello **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="d583e-139">Entrez un nom pour votre application, tel que *myWebApp*, puis décochez la case hello pour **créer le répertoire pour la solution**.</span><span class="sxs-lookup"><span data-stu-id="d583e-139">Enter a name for your application, such as *myWebApp*, and uncheck hello box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="d583e-140">Si l’option de hello est disponible, hello désactivez case à cocher trop**ajouter Application Insights tooproject**.</span><span class="sxs-lookup"><span data-stu-id="d583e-140">If hello option is available, uncheck hello box too**Add Application Insights tooproject**.</span></span> <span data-ttu-id="d583e-141">Application Insights a besoin votre application web avec Azure Application Insights vous tooauthorize.</span><span class="sxs-lookup"><span data-stu-id="d583e-141">Application Insights requires you tooauthorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="d583e-142">tookeep il simple dans ce didacticiel, ignorez ce processus.</span><span class="sxs-lookup"><span data-stu-id="d583e-142">tookeep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="d583e-143">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="d583e-143">Select **OK**.</span></span>
4. <span data-ttu-id="d583e-144">Choisissez **MVC** à partir de la liste des modèles hello.</span><span class="sxs-lookup"><span data-stu-id="d583e-144">Choose **MVC** from hello template list.</span></span>
    1. <span data-ttu-id="d583e-145">Pour **Modifier l’authentification**, sélectionnez **Aucune authentification**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="d583e-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="d583e-146">Sélectionnez **OK** toocreate votre solution.</span><span class="sxs-lookup"><span data-stu-id="d583e-146">Select **OK** toocreate your solution.</span></span>
5. <span data-ttu-id="d583e-147">Bonjour **Team Explorer** fenêtre, choisissez **modifications**.</span><span class="sxs-lookup"><span data-stu-id="d583e-147">In hello **Team Explorer** window, choose **Changes**.</span></span>

    ![Valider le référentiel git de modifications locales tooTeam Services](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="d583e-149">Dans la zone de texte de validation hello, entrez un message tel que *la validation initiale*.</span><span class="sxs-lookup"><span data-stu-id="d583e-149">In hello commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="d583e-150">Choisissez **valider tous les et synchronisation** à partir du menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="d583e-150">Choose **Commit All and Sync** from hello drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="d583e-151">Création d’une définition de build</span><span class="sxs-lookup"><span data-stu-id="d583e-151">Create build definition</span></span>
<span data-ttu-id="d583e-152">Dans les Services d’équipe, vous utilisez un toooutline de définition de build comment votre application doit être créée.</span><span class="sxs-lookup"><span data-stu-id="d583e-152">In Team Services, you use a build definition toooutline how your application should be built.</span></span> <span data-ttu-id="d583e-153">Dans ce didacticiel, nous créer une définition de base que prend notre code source, génère hello solution, puis crée web déployer le package, nous pouvons utiliser toorun hello web application sur un serveur IIS.</span><span class="sxs-lookup"><span data-stu-id="d583e-153">In this tutorial, we create a basic definition that takes our source code, builds hello solution, then creates web deploy package we can use toorun hello web app on an IIS server.</span></span>

1. <span data-ttu-id="d583e-154">Dans votre projet de Services d’équipe, choisissez **générer & version** haut de hello, puis sélectionnez **génère**.</span><span class="sxs-lookup"><span data-stu-id="d583e-154">In your Team Services project, choose **Build & Release** across hello top, then select **Builds**.</span></span>
3. <span data-ttu-id="d583e-155">Sélectionnez **+ Nouvelle définition**.</span><span class="sxs-lookup"><span data-stu-id="d583e-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="d583e-156">Choisissez hello **ASP.NET (version préliminaire)** modèle et sélectionnez **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="d583e-156">Choose hello **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="d583e-157">Laissez par défaut de hello toutes les valeurs de la tâche.</span><span class="sxs-lookup"><span data-stu-id="d583e-157">Leave all hello default task values.</span></span> <span data-ttu-id="d583e-158">Sous **obtenir les sources**, vérifiez que hello *myWebApp* référentiel et *master* branche sont sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="d583e-158">Under **Get sources**, ensure that hello *myWebApp* repository and *master* branch are selected.</span></span>

    ![Création d’une définition de build dans le projet Team Services](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="d583e-160">Sur hello **déclencheurs** onglet, déplacez le curseur hello pour **activer ce déclencheur** trop*activé*.</span><span class="sxs-lookup"><span data-stu-id="d583e-160">On hello **Triggers** tab, move hello slider for **Enable this trigger** too*Enabled*.</span></span>
7. <span data-ttu-id="d583e-161">Enregistrer la définition de build hello et file d’attente une nouvelle build en sélectionnant **enregistrer et de file d’attente** , puis **enregistrer et de file d’attente** à nouveau.</span><span class="sxs-lookup"><span data-stu-id="d583e-161">Save hello build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="d583e-162">Laissez les valeurs par défaut hello et sélectionnez **file d’attente**.</span><span class="sxs-lookup"><span data-stu-id="d583e-162">Leave hello defaults and select **Queue**.</span></span>

<span data-ttu-id="d583e-163">Espion que build de hello est planifiée sur un agent hébergé, puis commence à toobuild.</span><span class="sxs-lookup"><span data-stu-id="d583e-163">Watch as hello build is scheduled on a hosted agent, then begins toobuild.</span></span> <span data-ttu-id="d583e-164">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d583e-164">hello output is similar toohello following example:</span></span>

![Génération réussie du projet Team Services](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="d583e-166">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="d583e-166">Create virtual machine</span></span>
<span data-ttu-id="d583e-167">tooprovide un toorun plateforme votre application web ASP.NET, vous avez besoin d’une machine virtuelle Windows qui exécute IIS.</span><span class="sxs-lookup"><span data-stu-id="d583e-167">tooprovide a platform toorun your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="d583e-168">Team Services utilise une toointeract de l’agent avec une instance IIS hello que vous validez le code et les builds sont déclenchées.</span><span class="sxs-lookup"><span data-stu-id="d583e-168">Team Services uses an agent toointeract with hello IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="d583e-169">Créez une machine virtuelle Windows Server 2016 à l’aide de [cet exemple de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d583e-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="d583e-170">Il prend quelques minutes pour hello script toorun et créer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d583e-170">It takes a few minutes for hello script toorun and create hello VM.</span></span> <span data-ttu-id="d583e-171">Une fois que hello machine virtuelle a été créé, ouvrez le port 80 pour le trafic web avec [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) comme suit :</span><span class="sxs-lookup"><span data-stu-id="d583e-171">Once hello VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $resourceGroup `
  -Name "myNetworkSecurityGroup" | `
Add-AzureRmNetworkSecurityRuleConfig `
  -Name "myNetworkSecurityGroupRuleWeb" `
  -Protocol "Tcp" `
  -Direction "Inbound" `
  -Priority "1001" `
  -SourceAddressPrefix "*" `
  -SourcePortRange "*" `
  -DestinationAddressPrefix "*" `
  -DestinationPortRange "80" `
  -Access "Allow" | `
Set-AzureRmNetworkSecurityGroup
```

<span data-ttu-id="d583e-172">tooconnect tooyour machine virtuelle, obtenir l’adresse IP publique de hello avec [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) comme suit :</span><span class="sxs-lookup"><span data-stu-id="d583e-172">tooconnect tooyour VM, obtain hello public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="d583e-173">Créer une machine virtuelle de tooyour session Bureau à distance :</span><span class="sxs-lookup"><span data-stu-id="d583e-173">Create a remote desktop session tooyour VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="d583e-174">Sur la machine virtuelle de hello, ouvrez un **administrateur PowerShell** invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="d583e-174">On hello VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="d583e-175">Installez IIS et les fonctionnalités .NET requises comme suit :</span><span class="sxs-lookup"><span data-stu-id="d583e-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="d583e-176">Créer un groupe de déploiement</span><span class="sxs-lookup"><span data-stu-id="d583e-176">Create deployment group</span></span>
<span data-ttu-id="d583e-177">serveur IIS toohello du package de déploiement de toopush out web de hello, vous définissez un groupe de déploiement dans les Services d’équipe.</span><span class="sxs-lookup"><span data-stu-id="d583e-177">toopush out hello web deploy package toohello IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="d583e-178">Ce groupe vous permet de toospecify quels serveurs sont cible hello de nouvelles builds que vous validez tooTeam code Services et les builds sont terminées.</span><span class="sxs-lookup"><span data-stu-id="d583e-178">This group allows you toospecify which servers are hello target of new builds as you commit code tooTeam Services and builds are completed.</span></span>

1. <span data-ttu-id="d583e-179">Dans Team Services, choisissez **Build & Release** (Générer et publier), puis sélectionnez **Groupes de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="d583e-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="d583e-180">Choisissez **Add Deployment group** (Ajouter un groupe de déploiement).</span><span class="sxs-lookup"><span data-stu-id="d583e-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="d583e-181">Entrez un nom pour le groupe de hello, tel que *myIIS*, puis sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="d583e-181">Enter a name for hello group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="d583e-182">Bonjour **enregistrer des ordinateurs** section, vérifiez que *Windows* est sélectionné, puis la case hello trop**utiliser un jeton d’accès personnel dans le script de hello pour l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="d583e-182">In hello **Register machines** section, ensure *Windows* is selected, then check hello box too**Use a personal access token in hello script for authentication**.</span></span>
5. <span data-ttu-id="d583e-183">Sélectionnez **copier le script tooclipboard**.</span><span class="sxs-lookup"><span data-stu-id="d583e-183">Select **Copy script tooclipboard**.</span></span>


### <a name="add-iis-vm-toohello-deployment-group"></a><span data-ttu-id="d583e-184">Ajouter le groupe de déploiement IIS VM toohello</span><span class="sxs-lookup"><span data-stu-id="d583e-184">Add IIS VM toohello deployment group</span></span>
<span data-ttu-id="d583e-185">Avec le groupe de déploiement hello créé, ajoutez chaque groupe toohello d’instances IIS.</span><span class="sxs-lookup"><span data-stu-id="d583e-185">With hello deployment group created, add each IIS instance toohello group.</span></span> <span data-ttu-id="d583e-186">Team Services génère un script qui télécharge et configure un agent sur hello machine virtuelle qui reçoit le nouveau site web déploiement de packages, puis applique tooIIS.</span><span class="sxs-lookup"><span data-stu-id="d583e-186">Team Services generates a script that downloads and configures an agent on hello VM that receives new web deploy packages then applies it tooIIS.</span></span>

1. <span data-ttu-id="d583e-187">Dans hello **administrateur PowerShell** session sur votre machine virtuelle, coller et exécuter le script hello copié à partir de Team Services.</span><span class="sxs-lookup"><span data-stu-id="d583e-187">Back in hello **Administrator PowerShell** session on your VM, paste and run hello script copied from Team Services.</span></span>
2. <span data-ttu-id="d583e-188">Lorsque les balises tooconfigure demandées pour l’agent hello, choisissez *Y* et entrez *web*.</span><span class="sxs-lookup"><span data-stu-id="d583e-188">When prompted tooconfigure tags for hello agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="d583e-189">Lorsque vous y êtes invité pour le compte d’utilisateur hello, appuyez sur *retourner* tooaccept, hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="d583e-189">When prompted for hello user account, press *Return* tooaccept hello defaults.</span></span>
4. <span data-ttu-id="d583e-190">Attendez que toofinish de script hello avec un message *vstsagent.account.computername de Service a démarré correctement*.</span><span class="sxs-lookup"><span data-stu-id="d583e-190">Wait for hello script toofinish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="d583e-191">Bonjour **groupes de déploiement** page Hello **générer & version** menu, ouvrez hello *myIIS* groupe de déploiement.</span><span class="sxs-lookup"><span data-stu-id="d583e-191">In hello **Deployment groups** page of hello **Build & Release** menu, open hello *myIIS* deployment group.</span></span> <span data-ttu-id="d583e-192">Sur hello **Machines** , vérifiez que votre machine virtuelle est répertorié.</span><span class="sxs-lookup"><span data-stu-id="d583e-192">On hello **Machines** tab, verify that your VM is listed.</span></span>

    ![Machine virtuelle correctement ajouté le groupe de déploiement de Services tooTeam](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="d583e-194">Création d’une définition de mise en production</span><span class="sxs-lookup"><span data-stu-id="d583e-194">Create release definition</span></span>
<span data-ttu-id="d583e-195">toopublish vos builds, vous créez une définition de version dans Team Services.</span><span class="sxs-lookup"><span data-stu-id="d583e-195">toopublish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="d583e-196">Cette définition est déclenchée automatiquement en cas de réussite de la génération de votre application.</span><span class="sxs-lookup"><span data-stu-id="d583e-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="d583e-197">Vous choisissez toopush de groupe de déploiement hello votre site web déployer le package à et définissez les paramètres IIS appropriés hello.</span><span class="sxs-lookup"><span data-stu-id="d583e-197">You choose hello deployment group toopush your web deploy package to, and define hello appropriate IIS settings.</span></span>

1. <span data-ttu-id="d583e-198">Choisissez **Build & Release** (Générer et publier), puis sélectionnez **Builds**.</span><span class="sxs-lookup"><span data-stu-id="d583e-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="d583e-199">Choisissez la définition de build hello créée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="d583e-199">Choose hello build definition created in a previous step.</span></span>
2. <span data-ttu-id="d583e-200">Sous **récemment terminé**, choisissez la build la plus récente hello, puis sélectionnez **version**.</span><span class="sxs-lookup"><span data-stu-id="d583e-200">Under **Recently completed**, choose hello most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="d583e-201">Choisissez **Oui** toocreate une définition de mise en production.</span><span class="sxs-lookup"><span data-stu-id="d583e-201">Choose **Yes** toocreate a release definition.</span></span>
4. <span data-ttu-id="d583e-202">Choisissez hello **vide** modèle, puis sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d583e-202">Choose hello **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="d583e-203">Vérifiez la définition de build de projet et source hello sont renseignées avec votre projet.</span><span class="sxs-lookup"><span data-stu-id="d583e-203">Verify hello project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="d583e-204">Sélectionnez hello **déploiement continu** case à cocher, puis sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="d583e-204">Select hello **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="d583e-205">Sélectionnez zone de liste déroulante hello suivant trop**+ ajouter des tâches** et choisissez *ajouter une phase de déploiement de groupe*.</span><span class="sxs-lookup"><span data-stu-id="d583e-205">Select hello drop-down box next too**+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![Ajouter la définition de tâche toorelease Team Services](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="d583e-207">Choisissez **ajouter** suivant trop**IIS Web application Deploy(Preview)**, puis sélectionnez **fermer**.</span><span class="sxs-lookup"><span data-stu-id="d583e-207">Choose **Add** next too**IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="d583e-208">Sélectionnez hello **s’exécutent sur le groupe de déploiement** tâche parente.</span><span class="sxs-lookup"><span data-stu-id="d583e-208">Select hello **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="d583e-209">Pour **groupe de déploiement**, sélectionnez le déploiement de hello groupe que vous avez créé précédemment, comme *myIIS*.</span><span class="sxs-lookup"><span data-stu-id="d583e-209">For **Deployment Group**, select hello deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="d583e-210">Bonjour **balises d’ordinateurs** boîte, sélectionnez **ajouter** et choisissez hello *web* balise.</span><span class="sxs-lookup"><span data-stu-id="d583e-210">In hello **Machine tags** box, select **Add** and choose hello *web* tag.</span></span>
    
    ![Tâche de groupe de déploiement de définition de mise en production pour IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="d583e-212">Sélectionnez hello **déploiement : déploiement de l’application Web de IIS** tâche tooconfigure votre IIS instance des paramètres comme suit :</span><span class="sxs-lookup"><span data-stu-id="d583e-212">Select hello **Deploy: IIS Web App Deploy** task tooconfigure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="d583e-213">Pour **Nom du site web**, entrez *Site web par défaut*.</span><span class="sxs-lookup"><span data-stu-id="d583e-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="d583e-214">Laissez hello tous les autres paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="d583e-214">Leave all hello other default settings.</span></span>
12. <span data-ttu-id="d583e-215">Choisissez **Enregistrer**, puis sélectionnez **OK** deux fois.</span><span class="sxs-lookup"><span data-stu-id="d583e-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="d583e-216">Création d’une version et publication</span><span class="sxs-lookup"><span data-stu-id="d583e-216">Create a release and publish</span></span>
<span data-ttu-id="d583e-217">Vous pouvez désormais distribuer votre package de déploiement web en tant que nouvelle version.</span><span class="sxs-lookup"><span data-stu-id="d583e-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="d583e-218">Cette étape communique avec l’agent de hello sur chaque instance qui fait partie du groupe de déploiement hello, exécute un push de web de hello déployer le package, puis configure l’application web IIS toorun hello mis à jour.</span><span class="sxs-lookup"><span data-stu-id="d583e-218">This step communicates with hello agent on each instance that is part of hello deployment group, pushes hello web deploy package, then configures IIS toorun hello updated web application.</span></span>

1. <span data-ttu-id="d583e-219">Dans votre définition de mise en production, sélectionnez **+ Mise en production**, puis choisissez **Créer une mise en production**.</span><span class="sxs-lookup"><span data-stu-id="d583e-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="d583e-220">Vérifiez que la build la plus récente hello est sélectionné dans la liste déroulante hello, avec **déploiement automatisé : après la création de la version**.</span><span class="sxs-lookup"><span data-stu-id="d583e-220">Verify that hello latest build is selected in hello drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="d583e-221">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d583e-221">Select **Create**.</span></span>
3. <span data-ttu-id="d583e-222">Une petite bannière apparaît comme haut hello de votre définition de la mise en production, *version 'Version 1' a été créée*.</span><span class="sxs-lookup"><span data-stu-id="d583e-222">A small banner appears across hello top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="d583e-223">Sélectionnez hello version lien.</span><span class="sxs-lookup"><span data-stu-id="d583e-223">Select hello release link.</span></span>
4. <span data-ttu-id="d583e-224">Ouvrez hello **journaux** onglet progression de la version toowatch hello.</span><span class="sxs-lookup"><span data-stu-id="d583e-224">Open hello **Logs** tab toowatch hello release progress.</span></span>
    
    ![Réussite de la mise en production Team Services et de la distribution du package de déploiement web](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="d583e-226">Une fois la mise en production hello est terminée, ouvrez un navigateur web et entrez hello IIP adresse publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d583e-226">After hello release is complete, open a web browser and enter hello public IIP address of your VM.</span></span> <span data-ttu-id="d583e-227">Votre application web ASP.NET est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d583e-227">Your ASP.NET web application is running.</span></span>

    ![Application web ASP.NET s’exécutant sur une machine virtuelle IIS](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-hello-whole-cicd-pipeline"></a><span data-ttu-id="d583e-229">Pipeline de l’élément de configuration/CD ensemble test hello</span><span class="sxs-lookup"><span data-stu-id="d583e-229">Test hello whole CI/CD pipeline</span></span>
<span data-ttu-id="d583e-230">Votre application web s’exécutant sur IIS, essayez à présent pipeline de l’élément de configuration/CD hello ensemble.</span><span class="sxs-lookup"><span data-stu-id="d583e-230">With your web application running on IIS, now try hello whole CI/CD pipeline.</span></span> <span data-ttu-id="d583e-231">Une fois que vous apportez une modification dans Visual Studio et de validation, que votre code, une build est déclenchée, qui déclenche ensuite une version de votre site web mis à jour déployer le package tooIIS :</span><span class="sxs-lookup"><span data-stu-id="d583e-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package tooIIS:</span></span>

1. <span data-ttu-id="d583e-232">Dans Visual Studio, ouvrez hello **l’Explorateur de solutions** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d583e-232">In Visual Studio, open hello **Solution Explorer** window.</span></span>
2. <span data-ttu-id="d583e-233">Accédez tooand ouvrir *myWebApp | Vues | Accueil | Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="d583e-233">Navigate tooand open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="d583e-234">Modifiez la ligne 6 tooread :</span><span class="sxs-lookup"><span data-stu-id="d583e-234">Edit line 6 tooread:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="d583e-235">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="d583e-235">Save hello file.</span></span>
5. <span data-ttu-id="d583e-236">Ouvrez hello **Team Explorer** fenêtre, sélectionnez hello *myWebApp* de projet, puis choisissez **modifications**.</span><span class="sxs-lookup"><span data-stu-id="d583e-236">Open hello **Team Explorer** window, select hello *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="d583e-237">Entrez un message de validation, tel que *l’élément de configuration de test/CD pipeline*, puis choisissez **tous de la validation et la synchronisation** à partir du menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="d583e-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from hello drop-down menu.</span></span>
7. <span data-ttu-id="d583e-238">Dans l’espace de travail de Team Services, une nouvelle build est déclenchée à partir de la validation de code hello.</span><span class="sxs-lookup"><span data-stu-id="d583e-238">In Team Services workspace, a new build is triggered from hello code commit.</span></span> 
    - <span data-ttu-id="d583e-239">Choisissez **Build & Release** (Générer et publier), puis sélectionnez **Builds**.</span><span class="sxs-lookup"><span data-stu-id="d583e-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="d583e-240">Choisissez votre définition de build, puis sélectionnez hello **en file d’attente et en cours d’exécution** toowatch build comme hello build progresse.</span><span class="sxs-lookup"><span data-stu-id="d583e-240">Choose your build definition, then select hello **Queued & running** build toowatch as hello build progresses.</span></span>
9. <span data-ttu-id="d583e-241">Une fois la génération de hello est réussie, une nouvelle version est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="d583e-241">Once hello build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="d583e-242">Choisissez **générer & version**, puis **versions** envoyée tooyour IIS VM de package de déploiement web de hello de toosee.</span><span class="sxs-lookup"><span data-stu-id="d583e-242">Choose **Build & Release**, then **Releases** toosee hello web deploy package pushed tooyour IIS VM.</span></span> 
    - <span data-ttu-id="d583e-243">Sélectionnez hello **Actualiser** état de l’icône tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="d583e-243">Select hello **Refresh** icon tooupdate hello status.</span></span> <span data-ttu-id="d583e-244">Hello lorsque *environnements* colonne affiche une coche verte, mise en production hello a été déployée tooIIS.</span><span class="sxs-lookup"><span data-stu-id="d583e-244">When hello *Environments* column shows a green check mark, hello release has successfully deployed tooIIS.</span></span>
11. <span data-ttu-id="d583e-245">appliquer les modifications toosee, actualiser votre site Web d’IIS dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="d583e-245">toosee your changes applied, refresh your IIS website in a browser.</span></span>

    ![Application web ASP.NET s’exécutant sur une machine virtuelle IIS à partir d’un pipeline CI/CD](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="d583e-247">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d583e-247">Next steps</span></span>

<span data-ttu-id="d583e-248">Dans ce didacticiel, vous avez créé une application web ASP.NET dans les Services d’équipe et tooIIS packages lors de la validation de chaque code de déployer de build configuré et définitions version toodeploy un site web.</span><span class="sxs-lookup"><span data-stu-id="d583e-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions toodeploy new web deploy packages tooIIS on each code commit.</span></span> <span data-ttu-id="d583e-249">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="d583e-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d583e-250">Publier un projet d’équipe Services ASP.NET web application tooa</span><span class="sxs-lookup"><span data-stu-id="d583e-250">Publish an ASP.NET web application tooa Team Services project</span></span>
> * <span data-ttu-id="d583e-251">Créer une définition de build qui est déclenchée par les validations de code</span><span class="sxs-lookup"><span data-stu-id="d583e-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="d583e-252">Installer et configurer IIS sur une machine virtuelle dans Azure</span><span class="sxs-lookup"><span data-stu-id="d583e-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="d583e-253">Ajouter un groupe de déploiement hello tooa de l’instance IIS dans Team Services</span><span class="sxs-lookup"><span data-stu-id="d583e-253">Add hello IIS instance tooa deployment group in Team Services</span></span>
> * <span data-ttu-id="d583e-254">Créez une version définition toopublish web tooIIS de packages de déploiement</span><span class="sxs-lookup"><span data-stu-id="d583e-254">Create a release definition toopublish new web deploy packages tooIIS</span></span>
> * <span data-ttu-id="d583e-255">Tester le pipeline de l’élément de configuration/CD hello</span><span class="sxs-lookup"><span data-stu-id="d583e-255">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="d583e-256">Avancer toolearn de didacticiel suivant toohello comment toosecure un serveur web avec les certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="d583e-256">Advance toohello next tutorial toolearn how toosecure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d583e-257">Sécuriser un serveur web avec SSL</span><span class="sxs-lookup"><span data-stu-id="d583e-257">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)