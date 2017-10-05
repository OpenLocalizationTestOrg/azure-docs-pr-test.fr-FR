---
title: "Création d’un pipeline CI/CD dans Azure avec Team Services | Microsoft Docs"
description: "Découvrez comment créer un pipeline Visual Studio Team Services pour une intégration continue et une fourniture qui déploie une application web vers IIS sur une machine virtuelle Windows"
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
ms.openlocfilehash: a587f58fad2ec74c7633823c4d34f900e7c01f7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-continuous-integration-pipeline-with-visual-studio-team-services-and-iis"></a><span data-ttu-id="26787-103">Création d’un pipeline d’intégration continue avec Visual Studio Team Services et IIS</span><span class="sxs-lookup"><span data-stu-id="26787-103">Create a continuous integration pipeline with Visual Studio Team Services and IIS</span></span>
<span data-ttu-id="26787-104">Pour automatiser les phases de création, de test et de déploiement du développement de l’application, vous pouvez utiliser un pipeline d’intégration et de déploiement continus (CI/CD).</span><span class="sxs-lookup"><span data-stu-id="26787-104">To automate the build, test, and deployment phases of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="26787-105">Dans ce didacticiel, vous créez un pipeline CI/CD à l’aide de Visual Studio Team Services et d’une machine virtuelle Windows (VM) dans Azure qui exécute IIS.</span><span class="sxs-lookup"><span data-stu-id="26787-105">In this tutorial, you create a CI/CD pipeline using Visual Studio Team Services and a Windows virtual machine (VM) in Azure that runs IIS.</span></span> <span data-ttu-id="26787-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="26787-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="26787-107">Publier une application web ASP.NET dans un projet Team Services</span><span class="sxs-lookup"><span data-stu-id="26787-107">Publish an ASP.NET web application to a Team Services project</span></span>
> * <span data-ttu-id="26787-108">Créer une définition de build qui est déclenchée par les validations de code</span><span class="sxs-lookup"><span data-stu-id="26787-108">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="26787-109">Installer et configurer IIS sur une machine virtuelle dans Azure</span><span class="sxs-lookup"><span data-stu-id="26787-109">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="26787-110">Ajouter l’instance IIS à un groupe de déploiement dans Team Services</span><span class="sxs-lookup"><span data-stu-id="26787-110">Add the IIS instance to a deployment group in Team Services</span></span>
> * <span data-ttu-id="26787-111">Créer une définition de version pour publier les nouveaux packages de déploiement web sur IIS</span><span class="sxs-lookup"><span data-stu-id="26787-111">Create a release definition to publish new web deploy packages to IIS</span></span>
> * <span data-ttu-id="26787-112">test du pipeline CI/CD</span><span class="sxs-lookup"><span data-stu-id="26787-112">Test the CI/CD pipeline</span></span>

<span data-ttu-id="26787-113">Ce didacticiel requiert le module Azure PowerShell version 3.6 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="26787-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="26787-114">Exécutez `Get-Module -ListAvailable AzureRM` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="26787-114">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="26787-115">Si vous devez effectuer une mise à niveau, consultez [Installer le module Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="26787-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="create-project-in-team-services"></a><span data-ttu-id="26787-116">Création d’un projet dans Team Services</span><span class="sxs-lookup"><span data-stu-id="26787-116">Create project in Team Services</span></span>
<span data-ttu-id="26787-117">Visual Studio Team Services simplifie la collaboration et permet le développement sans recours à une solution de gestion de code en local.</span><span class="sxs-lookup"><span data-stu-id="26787-117">Visual Studio Team Services allows for easy collaboration and development without maintaining an on-premises code management solution.</span></span> <span data-ttu-id="26787-118">Team Services offre des fonctionnalités de test de code, de création et d’analyse de l’application dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="26787-118">Team Services provides cloud code testing, build, and application insights.</span></span> <span data-ttu-id="26787-119">Vous pouvez choisir le référentiel de contrôle de version et l’IDE qui conviennent le mieux au développement de votre code.</span><span class="sxs-lookup"><span data-stu-id="26787-119">You can choose a version control repo and IDE that best fits your code development.</span></span> <span data-ttu-id="26787-120">Pour ce didacticiel, vous pouvez utiliser un compte gratuit pour créer une application web ASP.NET de base et un pipeline CI/CD.</span><span class="sxs-lookup"><span data-stu-id="26787-120">For this tutorial, you can use a free account to create a basic ASP.NET web app and CI/CD pipeline.</span></span> <span data-ttu-id="26787-121">Si vous n’avez pas encore de compte Team Services, [créez-en un](http://go.microsoft.com/fwlink/?LinkId=307137).</span><span class="sxs-lookup"><span data-stu-id="26787-121">If you do not already have a Team Services account, [create one](http://go.microsoft.com/fwlink/?LinkId=307137).</span></span>

<span data-ttu-id="26787-122">Pour gérer le processus de validation de code, de définition de build et de définition de version, créez un projet dans Team Services en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="26787-122">To manage the code commit process, build definitions, and release definitions, create a project in Team Services as follows:</span></span>

1. <span data-ttu-id="26787-123">Ouvrez votre tableau de bord Team Services dans un navigateur web et choisissez **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="26787-123">Open your Team Services dashboard in a web browser and choose **New project**.</span></span>
2. <span data-ttu-id="26787-124">Entrez *myWebApp* comme **nom de projet**.</span><span class="sxs-lookup"><span data-stu-id="26787-124">Enter *myWebApp* for the **Project name**.</span></span> <span data-ttu-id="26787-125">Laissez toutes les autres valeurs par défaut pour utiliser le contrôle de version *Git* et le processus d’élément de travail *Agile*.</span><span class="sxs-lookup"><span data-stu-id="26787-125">Leave all other default values to use *Git* version control and *Agile* work item process.</span></span>
3. <span data-ttu-id="26787-126">Choisissez l’option **Partager avec** *Membres de l’équipe*, puis sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="26787-126">Choose the option to **Share with** *Team Members*, then select **Create**.</span></span>
5. <span data-ttu-id="26787-127">Une fois votre projet créé, sélectionnez l’option **Initialize with a README or gitignore** (Initialiser avec un fichier README ou gitignore), puis **Initialiser**.</span><span class="sxs-lookup"><span data-stu-id="26787-127">Once your project has been created, choose the option to **Initialize with a README or gitignore**, then **Initialize**.</span></span>
6. <span data-ttu-id="26787-128">À l’intérieur de votre nouveau projet, choisissez **Tableaux de bord** en haut, puis sélectionnez **Ouvrir dans Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="26787-128">Inside your new project, choose **Dashboards** across the top, then select **Open in Visual Studio**.</span></span>


## <a name="create-aspnet-web-application"></a><span data-ttu-id="26787-129">Création d’une application web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="26787-129">Create ASP.NET web application</span></span>
<span data-ttu-id="26787-130">À l’étape précédente, vous avez créé un projet dans Team Services.</span><span class="sxs-lookup"><span data-stu-id="26787-130">In the previous step, you created a project in Team Services.</span></span> <span data-ttu-id="26787-131">La dernière étape ouvre votre nouveau projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26787-131">The final step opens your new project in Visual Studio.</span></span> <span data-ttu-id="26787-132">Vous gérez vos validations de code dans la fenêtre **Team Explorer**.</span><span class="sxs-lookup"><span data-stu-id="26787-132">You manage your code commits in the **Team Explorer** window.</span></span> <span data-ttu-id="26787-133">Créez une copie locale de votre nouveau projet, puis créez une application web ASP.NET à partir d’un modèle comme suit :</span><span class="sxs-lookup"><span data-stu-id="26787-133">Create a local copy of your new project, then create an ASP.NET web application from a template as follows:</span></span>

1. <span data-ttu-id="26787-134">Sélectionnez **Cloner** pour créer un référentiel git local de votre projet Team Services.</span><span class="sxs-lookup"><span data-stu-id="26787-134">Select **Clone** to create a local git repo of your Team Services project.</span></span>
    
    ![Clonage du référentiel à partir du projet Team Services](media/tutorial-vsts-iis-cicd/clone_repo.png)

2. <span data-ttu-id="26787-136">Sous **Solutions**, sélectionnez **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="26787-136">Under **Solutions**, select **New**.</span></span>

    ![Création de la solution d’application web](media/tutorial-vsts-iis-cicd/new_solution.png)

3. <span data-ttu-id="26787-138">Sélectionnez les modèles **web**, puis choisissez le modèle **Application web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="26787-138">Select **Web** templates, and then choose the **ASP.NET Web Application** template.</span></span>
    1. <span data-ttu-id="26787-139">Entrez un nom pour votre application, tel que *myWebApp*, et décochez la case **Créer un répertoire pour la solution**.</span><span class="sxs-lookup"><span data-stu-id="26787-139">Enter a name for your application, such as *myWebApp*, and uncheck the box for **Create directory for solution**.</span></span>
    2. <span data-ttu-id="26787-140">Si l’option est disponible, décochez la case **Add Application Insights to project** (Ajouter Application Insights au projet).</span><span class="sxs-lookup"><span data-stu-id="26787-140">If the option is available, uncheck the box to **Add Application Insights to project**.</span></span> <span data-ttu-id="26787-141">Application Insights nécessite que vous autorisiez votre application web dans Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="26787-141">Application Insights requires you to authorize your web application with Azure Application Insights.</span></span> <span data-ttu-id="26787-142">Pour faire simple, dans ce didacticiel, ignorez cette procédure.</span><span class="sxs-lookup"><span data-stu-id="26787-142">To keep it simple in this tutorial, skip this process.</span></span>
    3. <span data-ttu-id="26787-143">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="26787-143">Select **OK**.</span></span>
4. <span data-ttu-id="26787-144">Dans la liste des modèles, choisissez **MVC**.</span><span class="sxs-lookup"><span data-stu-id="26787-144">Choose **MVC** from the template list.</span></span>
    1. <span data-ttu-id="26787-145">Pour **Modifier l’authentification**, sélectionnez **Aucune authentification**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="26787-145">Select **Change Authentication**, choose **No Authentication**, then select **OK**.</span></span>
    2. <span data-ttu-id="26787-146">Sélectionnez **OK** pour créer votre solution.</span><span class="sxs-lookup"><span data-stu-id="26787-146">Select **OK** to create your solution.</span></span>
5. <span data-ttu-id="26787-147">Dans la fenêtre **Team Explorer**, choisissez **Modifications**.</span><span class="sxs-lookup"><span data-stu-id="26787-147">In the **Team Explorer** window, choose **Changes**.</span></span>

    ![Validation des modifications locales dans le référentiel git Team Services](media/tutorial-vsts-iis-cicd/commit_changes.png)

6. <span data-ttu-id="26787-149">Dans la zone de texte de validation, entrez un message tel que *Validation initiale*.</span><span class="sxs-lookup"><span data-stu-id="26787-149">In the commit text box, enter a message such as *Initial commit*.</span></span> <span data-ttu-id="26787-150">Dans le menu déroulant, choisissez **Commit All and Sync** (Tout valider et synchroniser).</span><span class="sxs-lookup"><span data-stu-id="26787-150">Choose **Commit All and Sync** from the drop-down menu.</span></span>


## <a name="create-build-definition"></a><span data-ttu-id="26787-151">Création d’une définition de build</span><span class="sxs-lookup"><span data-stu-id="26787-151">Create build definition</span></span>
<span data-ttu-id="26787-152">Dans Team Services, vous utilisez une définition de build pour montrer la manière dont votre application doit être conçue.</span><span class="sxs-lookup"><span data-stu-id="26787-152">In Team Services, you use a build definition to outline how your application should be built.</span></span> <span data-ttu-id="26787-153">Dans ce didacticiel, nous créons une définition de base qui prend notre code source, génère la solution, puis crée le package de déploiement web que nous pouvons utiliser pour exécuter l’application web sur un serveur IIS.</span><span class="sxs-lookup"><span data-stu-id="26787-153">In this tutorial, we create a basic definition that takes our source code, builds the solution, then creates web deploy package we can use to run the web app on an IIS server.</span></span>

1. <span data-ttu-id="26787-154">Dans votre projet Team Services, choisissez l’option **Build & Release** (Générer et publier) en haut, puis sélectionnez **Builds**.</span><span class="sxs-lookup"><span data-stu-id="26787-154">In your Team Services project, choose **Build & Release** across the top, then select **Builds**.</span></span>
3. <span data-ttu-id="26787-155">Sélectionnez **+ Nouvelle définition**.</span><span class="sxs-lookup"><span data-stu-id="26787-155">Select **+ New definition**.</span></span>
4. <span data-ttu-id="26787-156">Choisissez le modèle **ASP.NET (préversion)** et sélectionnez **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="26787-156">Choose the **ASP.NET (PREVIEW)** template and select **Apply**.</span></span>
5. <span data-ttu-id="26787-157">Laissez les valeurs par défaut pour les tâches.</span><span class="sxs-lookup"><span data-stu-id="26787-157">Leave all the default task values.</span></span> <span data-ttu-id="26787-158">Sous **Obtenir les sources**, assurez-vous que le référentiel *myWebApp* et la branche *master* sont sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="26787-158">Under **Get sources**, ensure that the *myWebApp* repository and *master* branch are selected.</span></span>

    ![Création d’une définition de build dans le projet Team Services](media/tutorial-vsts-iis-cicd/create_build_definition.png)

6. <span data-ttu-id="26787-160">Sur l’onglet **Déclencheurs**, déplacez le curseur **Enable this trigger** (Activer ce déclencheur) sur *Activé*.</span><span class="sxs-lookup"><span data-stu-id="26787-160">On the **Triggers** tab, move the slider for **Enable this trigger** to *Enabled*.</span></span>
7. <span data-ttu-id="26787-161">Enregistrez la définition de build et mettez en file d’attente une nouvelle build en sélectionnant **Save & queue** (Enregistrer et mettre en file d’attente), puis de nouveau **Save & queue** (Enregistrer et mettre en file d’attente).</span><span class="sxs-lookup"><span data-stu-id="26787-161">Save the build definition and queue a new build by selecting **Save & queue** , then **Save & queue** again.</span></span> <span data-ttu-id="26787-162">Conservez les valeurs par défaut et sélectionnez **File d’attente**.</span><span class="sxs-lookup"><span data-stu-id="26787-162">Leave the defaults and select **Queue**.</span></span>

<span data-ttu-id="26787-163">Vérifiez que la build est planifiée sur un agent hébergé, puis commencez la génération.</span><span class="sxs-lookup"><span data-stu-id="26787-163">Watch as the build is scheduled on a hosted agent, then begins to build.</span></span> <span data-ttu-id="26787-164">Le résultat ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="26787-164">The output is similar to the following example:</span></span>

![Génération réussie du projet Team Services](media/tutorial-vsts-iis-cicd/successful_build.png)


## <a name="create-virtual-machine"></a><span data-ttu-id="26787-166">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="26787-166">Create virtual machine</span></span>
<span data-ttu-id="26787-167">Pour fournir une plateforme sur laquelle exécuter votre application web ASP.NET, vous avez besoin d’une machine virtuelle Windows qui exécute IIS.</span><span class="sxs-lookup"><span data-stu-id="26787-167">To provide a platform to run your ASP.NET web app, you need a Windows virtual machine that runs IIS.</span></span> <span data-ttu-id="26787-168">Team Services utilise un agent pour interagir avec l’instance IIS lorsque vous validez le code et que les builds sont déclenchées.</span><span class="sxs-lookup"><span data-stu-id="26787-168">Team Services uses an agent to interact with the IIS instance as you commit code and builds are triggered.</span></span>

<span data-ttu-id="26787-169">Créez une machine virtuelle Windows Server 2016 à l’aide de [cet exemple de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="26787-169">Create a Windows Server 2016 VM using [this script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md?toc=%2fpowershell%2fmodule%2ftoc.json).</span></span> <span data-ttu-id="26787-170">Il faut quelques minutes pour que le script s’exécute et crée la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="26787-170">It takes a few minutes for the script to run and create the VM.</span></span> <span data-ttu-id="26787-171">Une fois la machine virtuelle créée, ouvrez le port 80 pour le trafic web avec [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) comme suit :</span><span class="sxs-lookup"><span data-stu-id="26787-171">Once the VM has been created, open port 80 for web traffic with [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermresourcegroup) as follows:</span></span>

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

<span data-ttu-id="26787-172">Pour vous connecter à votre machine virtuelle, obtenez l’adresse IP publique avec [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) comme suit :</span><span class="sxs-lookup"><span data-stu-id="26787-172">To connect to your VM, obtain the public IP address with [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) as follows:</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup | Select IpAddress
```

<span data-ttu-id="26787-173">Créez une session Bureau à distance vers votre machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="26787-173">Create a remote desktop session to your VM:</span></span>

```cmd
mstsc /v:<publicIpAddress>
```

<span data-ttu-id="26787-174">Sur la machine virtuelle, ouvrez une invite de commande **Administrateur PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="26787-174">On the VM, open an **Administrator PowerShell** command prompt.</span></span> <span data-ttu-id="26787-175">Installez IIS et les fonctionnalités .NET requises comme suit :</span><span class="sxs-lookup"><span data-stu-id="26787-175">Install IIS and required .NET features as follows:</span></span>

```powershell
Install-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features
```


## <a name="create-deployment-group"></a><span data-ttu-id="26787-176">Créer un groupe de déploiement</span><span class="sxs-lookup"><span data-stu-id="26787-176">Create deployment group</span></span>
<span data-ttu-id="26787-177">Pour diffuser le package de déploiement web vers le serveur IIS, vous définissez un groupe de déploiement dans Team Services.</span><span class="sxs-lookup"><span data-stu-id="26787-177">To push out the web deploy package to the IIS server, you define a deployment group in Team Services.</span></span> <span data-ttu-id="26787-178">Ce groupe vous permet de spécifier quels serveurs sont la cible de nouvelles builds lorsque vous validez du code dans Team Services et que les builds sont terminées.</span><span class="sxs-lookup"><span data-stu-id="26787-178">This group allows you to specify which servers are the target of new builds as you commit code to Team Services and builds are completed.</span></span>

1. <span data-ttu-id="26787-179">Dans Team Services, choisissez **Build & Release** (Générer et publier), puis sélectionnez **Groupes de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="26787-179">In Team Services, choose **Build & Release** and then select **Deployment groups**.</span></span>
2. <span data-ttu-id="26787-180">Choisissez **Add Deployment group** (Ajouter un groupe de déploiement).</span><span class="sxs-lookup"><span data-stu-id="26787-180">Choose **Add Deployment group**.</span></span>
3. <span data-ttu-id="26787-181">Entrez un nom pour le groupe, tel que *myIIS*, puis sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="26787-181">Enter a name for the group, such as *myIIS*, then select **Create**.</span></span>
4. <span data-ttu-id="26787-182">Dans la section **Register machines** (Enregistrer des ordinateurs), assurez-vous que l’option *Windows* est sélectionnée, puis cochez la case **Use a personal access token in the script for authentication** (Utiliser un jeton d’accès personnel dans le script pour l’authentification).</span><span class="sxs-lookup"><span data-stu-id="26787-182">In the **Register machines** section, ensure *Windows* is selected, then check the box to **Use a personal access token in the script for authentication**.</span></span>
5. <span data-ttu-id="26787-183">Sélectionnez **Copy script to clipboard** (Copier le script dans le Presse-papiers).</span><span class="sxs-lookup"><span data-stu-id="26787-183">Select **Copy script to clipboard**.</span></span>


### <a name="add-iis-vm-to-the-deployment-group"></a><span data-ttu-id="26787-184">Ajouter une machine virtuelle IIS au groupe de déploiement</span><span class="sxs-lookup"><span data-stu-id="26787-184">Add IIS VM to the deployment group</span></span>
<span data-ttu-id="26787-185">Une fois le groupe de déploiement créé, ajoutez-y chaque instance IIS.</span><span class="sxs-lookup"><span data-stu-id="26787-185">With the deployment group created, add each IIS instance to the group.</span></span> <span data-ttu-id="26787-186">Team Services génère un script qui télécharge et configure un agent sur la machine virtuelle qui reçoit les nouveaux packages de déploiement web, puis l’applique à IIS.</span><span class="sxs-lookup"><span data-stu-id="26787-186">Team Services generates a script that downloads and configures an agent on the VM that receives new web deploy packages then applies it to IIS.</span></span>

1. <span data-ttu-id="26787-187">Dans la session **Administrateur PowerShell** sur votre machine virtuelle, collez le script copié à partir de Team Services et exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="26787-187">Back in the **Administrator PowerShell** session on your VM, paste and run the script copied from Team Services.</span></span>
2. <span data-ttu-id="26787-188">Lorsque vous êtes invité à configurer les balises pour l’agent, choisissez *Y* et entrez *web*.</span><span class="sxs-lookup"><span data-stu-id="26787-188">When prompted to configure tags for the agent, choose *Y* and enter *web*.</span></span>
3. <span data-ttu-id="26787-189">Lorsque vous êtes invité à indiquer le compte d’utilisateur, appuyez sur *Retour* pour accepter les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="26787-189">When prompted for the user account, press *Return* to accept the defaults.</span></span>
4. <span data-ttu-id="26787-190">Attendez que le script se termine avec un message de type *Service vstsagent.account.computername démarré correctement*.</span><span class="sxs-lookup"><span data-stu-id="26787-190">Wait for the script to finish with a message *Service vstsagent.account.computername started successfully*.</span></span>
5. <span data-ttu-id="26787-191">Dans la page **Groupes de déploiement** du menu **Build & Release** (Générer et publier), ouvrez le groupe de déploiement *myIIS*.</span><span class="sxs-lookup"><span data-stu-id="26787-191">In the **Deployment groups** page of the **Build & Release** menu, open the *myIIS* deployment group.</span></span> <span data-ttu-id="26787-192">Sur l’onglet **Machines**, vérifiez que votre machine virtuelle est répertoriée.</span><span class="sxs-lookup"><span data-stu-id="26787-192">On the **Machines** tab, verify that your VM is listed.</span></span>

    ![Machine virtuelle ajoutée au groupe de déploiement Team Services](media/tutorial-vsts-iis-cicd/deployment_group.png)


## <a name="create-release-definition"></a><span data-ttu-id="26787-194">Création d’une définition de mise en production</span><span class="sxs-lookup"><span data-stu-id="26787-194">Create release definition</span></span>
<span data-ttu-id="26787-195">Pour publier vos builds, vous créez une définition de mise en production dans Team Services.</span><span class="sxs-lookup"><span data-stu-id="26787-195">To publish your builds, you create a release definition in Team Services.</span></span> <span data-ttu-id="26787-196">Cette définition est déclenchée automatiquement en cas de réussite de la génération de votre application.</span><span class="sxs-lookup"><span data-stu-id="26787-196">This definition is triggered automatically by a successful build of your application.</span></span> <span data-ttu-id="26787-197">Vous choisissez le groupe de déploiement dans lequel distribuer votre application web et définissez les paramètres IIS appropriés.</span><span class="sxs-lookup"><span data-stu-id="26787-197">You choose the deployment group to push your web deploy package to, and define the appropriate IIS settings.</span></span>

1. <span data-ttu-id="26787-198">Choisissez **Build & Release** (Générer et publier), puis sélectionnez **Builds**.</span><span class="sxs-lookup"><span data-stu-id="26787-198">Choose **Build & Release**, then select **Builds**.</span></span> <span data-ttu-id="26787-199">Sélectionnez la définition de build créée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="26787-199">Choose the build definition created in a previous step.</span></span>
2. <span data-ttu-id="26787-200">Sous **Effectuées récemment**, choisissez la build la plus récente, puis sélectionnez **Mise en production**.</span><span class="sxs-lookup"><span data-stu-id="26787-200">Under **Recently completed**, choose the most recent build, then select **Release**.</span></span>
3. <span data-ttu-id="26787-201">Choisissez **Oui** pour créer une définition de mise en production.</span><span class="sxs-lookup"><span data-stu-id="26787-201">Choose **Yes** to create a release definition.</span></span>
4. <span data-ttu-id="26787-202">Choisissez le modèle **vide**, puis sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="26787-202">Choose the **Empty** template, then select **Next**.</span></span>
5. <span data-ttu-id="26787-203">Vérifiez que le projet et la définition de build source sont renseignés avec votre projet.</span><span class="sxs-lookup"><span data-stu-id="26787-203">Verify the project and source build definition are populated with your project.</span></span>
6. <span data-ttu-id="26787-204">Cochez la case **Déploiement continu**, puis sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="26787-204">Select the **Continuous deployment** check box, then select **Create**.</span></span>
7. <span data-ttu-id="26787-205">Sélectionnez la liste déroulante en regard de **+ Ajouter des tâches** et choisissez *Add a deployment group phase* (Ajouter une phase de déploiement de groupe).</span><span class="sxs-lookup"><span data-stu-id="26787-205">Select the drop-down box next to **+ Add tasks** and choose *Add a deployment group phase*.</span></span>
    
    ![Ajouter une tâche à la définition de mise en production dans Team Services](media/tutorial-vsts-iis-cicd/add_release_task.png)

8. <span data-ttu-id="26787-207">Choisissez **Ajouter** en regard de **IIS Web App Deploy (Preview)** (Déploiement d’application web IIS (préversion)), puis sélectionnez **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="26787-207">Choose **Add** next to **IIS Web App Deploy(Preview)**, then select **Close**.</span></span>
9. <span data-ttu-id="26787-208">Sélectionnez la tâche parente **Run on deployment group** (Exécuter sur le groupe de déploiement).</span><span class="sxs-lookup"><span data-stu-id="26787-208">Select the **Run on deployment group** parent task.</span></span>
    1. <span data-ttu-id="26787-209">Pour **Groupe de déploiement**, sélectionnez le groupe de déploiement que vous avez créé précédemment, par exemple *myIIS*.</span><span class="sxs-lookup"><span data-stu-id="26787-209">For **Deployment Group**, select the deployment group you created earlier, such as *myIIS*.</span></span>
    2. <span data-ttu-id="26787-210">Dans la zone **Machine tags** (Balises de machine), sélectionnez **Ajouter** et choisissez la balise *web*.</span><span class="sxs-lookup"><span data-stu-id="26787-210">In the **Machine tags** box, select **Add** and choose the *web* tag.</span></span>
    
    ![Tâche de groupe de déploiement de définition de mise en production pour IIS](media/tutorial-vsts-iis-cicd/release_definition_iis.png)
 
11. <span data-ttu-id="26787-212">Sélectionnez la tâche **Déployer : déploiement de l’application web IIS** pour configurer les paramètres de votre instance IIS comme suit :</span><span class="sxs-lookup"><span data-stu-id="26787-212">Select the **Deploy: IIS Web App Deploy** task to configure your IIS instance settings as follows:</span></span>
    1. <span data-ttu-id="26787-213">Pour **Nom du site web**, entrez *Site web par défaut*.</span><span class="sxs-lookup"><span data-stu-id="26787-213">For **Website Name**, enter *Default Web Site*.</span></span>
    2. <span data-ttu-id="26787-214">Laissez tous les autres paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="26787-214">Leave all the other default settings.</span></span>
12. <span data-ttu-id="26787-215">Choisissez **Enregistrer**, puis sélectionnez **OK** deux fois.</span><span class="sxs-lookup"><span data-stu-id="26787-215">Choose **Save**, then select **OK** twice.</span></span>


## <a name="create-a-release-and-publish"></a><span data-ttu-id="26787-216">Création d’une version et publication</span><span class="sxs-lookup"><span data-stu-id="26787-216">Create a release and publish</span></span>
<span data-ttu-id="26787-217">Vous pouvez désormais distribuer votre package de déploiement web en tant que nouvelle version.</span><span class="sxs-lookup"><span data-stu-id="26787-217">You can now push your web deploy package as a new release.</span></span> <span data-ttu-id="26787-218">Cette étape communique avec l’agent sur chaque instance qui fait partie du groupe de déploiement, distribue le package de déploiement web, puis configure IIS pour exécuter l’application web mise à jour.</span><span class="sxs-lookup"><span data-stu-id="26787-218">This step communicates with the agent on each instance that is part of the deployment group, pushes the web deploy package, then configures IIS to run the updated web application.</span></span>

1. <span data-ttu-id="26787-219">Dans votre définition de mise en production, sélectionnez **+ Mise en production**, puis choisissez **Créer une mise en production**.</span><span class="sxs-lookup"><span data-stu-id="26787-219">In your release definition, select **+ Release**, then choose **Create Release**.</span></span>
2. <span data-ttu-id="26787-220">Vérifiez que la build la plus récente est sélectionnée dans la liste déroulante, ainsi que **Déploiement automatisé : après la création de la mise en production**.</span><span class="sxs-lookup"><span data-stu-id="26787-220">Verify that the latest build is selected in the drop-down list, along with **Automated deployment: After release creation**.</span></span> <span data-ttu-id="26787-221">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="26787-221">Select **Create**.</span></span>
3. <span data-ttu-id="26787-222">Une petite bannière apparaît en haut de votre définition de mise en production, par exemple *La mise en production 'Mise en production-1' a été créée*.</span><span class="sxs-lookup"><span data-stu-id="26787-222">A small banner appears across the top of your release definition, such as *Release 'Release-1' has been created*.</span></span> <span data-ttu-id="26787-223">Sélectionnez le lien de la mise en production.</span><span class="sxs-lookup"><span data-stu-id="26787-223">Select the release link.</span></span>
4. <span data-ttu-id="26787-224">Ouvrez l’onglet **Journaux** pour surveiller la progression de la mise en production.</span><span class="sxs-lookup"><span data-stu-id="26787-224">Open the **Logs** tab to watch the release progress.</span></span>
    
    ![Réussite de la mise en production Team Services et de la distribution du package de déploiement web](media/tutorial-vsts-iis-cicd/successful_release.png)

5. <span data-ttu-id="26787-226">Une fois la mise en production terminée, ouvrez un navigateur web et entrez l’adresse IP publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="26787-226">After the release is complete, open a web browser and enter the public IIP address of your VM.</span></span> <span data-ttu-id="26787-227">Votre application web ASP.NET est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="26787-227">Your ASP.NET web application is running.</span></span>

    ![Application web ASP.NET s’exécutant sur une machine virtuelle IIS](media/tutorial-vsts-iis-cicd/running_web_app.png)


## <a name="test-the-whole-cicd-pipeline"></a><span data-ttu-id="26787-229">Test de l’ensemble du pipeline CI/CD</span><span class="sxs-lookup"><span data-stu-id="26787-229">Test the whole CI/CD pipeline</span></span>
<span data-ttu-id="26787-230">Votre application web s’exécutant sur IIS, testez à présent l’ensemble du pipeline CI/CD.</span><span class="sxs-lookup"><span data-stu-id="26787-230">With your web application running on IIS, now try the whole CI/CD pipeline.</span></span> <span data-ttu-id="26787-231">Lorsque vous apportez une modification dans Visual Studio et validez votre code, une build est déclenchée, qui déclenche ensuite une mise en production de votre package de déploiement web mis à jour sur IIS :</span><span class="sxs-lookup"><span data-stu-id="26787-231">After you make a change in Visual Studio and commit your code, a build is triggered which then triggers a release of your updated web deploy package to IIS:</span></span>

1. <span data-ttu-id="26787-232">Dans Visual Studio, ouvrez la fenêtre **Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="26787-232">In Visual Studio, open the **Solution Explorer** window.</span></span>
2. <span data-ttu-id="26787-233">Recherchez et ouvrez *myWebApp | Vues | Accueil | Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="26787-233">Navigate to and open *myWebApp | Views | Home | Index.cshtml*</span></span>
3. <span data-ttu-id="26787-234">Modifiez la ligne 6 en :</span><span class="sxs-lookup"><span data-stu-id="26787-234">Edit line 6 to read:</span></span>

    `<h1>ASP.NET with VSTS and CI/CD!</h1>`

4. <span data-ttu-id="26787-235">Enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="26787-235">Save the file.</span></span>
5. <span data-ttu-id="26787-236">Ouvrez la fenêtre **Team Explorer**, sélectionnez le projet *myWebApp*, puis choisissez **Modifications**.</span><span class="sxs-lookup"><span data-stu-id="26787-236">Open the **Team Explorer** window, select the *myWebApp* project, then choose **Changes**.</span></span>
6. <span data-ttu-id="26787-237">Entrez un message de validation, tel que *Test du pipeline CI/CD*, puis choisissez **Commit All and Sync** (Tout valider et synchroniser) dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="26787-237">Enter a commit message, such as *Testing CI/CD pipeline*, then choose **Commit All and Sync** from the drop-down menu.</span></span>
7. <span data-ttu-id="26787-238">Dans l’espace de travail de Team Services, une nouvelle build est déclenchée à partir de la validation du code.</span><span class="sxs-lookup"><span data-stu-id="26787-238">In Team Services workspace, a new build is triggered from the code commit.</span></span> 
    - <span data-ttu-id="26787-239">Choisissez **Build & Release** (Générer et publier), puis sélectionnez **Builds**.</span><span class="sxs-lookup"><span data-stu-id="26787-239">Choose **Build & Release**, then select **Builds**.</span></span> 
    - <span data-ttu-id="26787-240">Choisissez votre définition de build, puis sélectionnez la build **en file d’attente et en cours d’exécution** pour afficher la progression.</span><span class="sxs-lookup"><span data-stu-id="26787-240">Choose your build definition, then select the **Queued & running** build to watch as the build progresses.</span></span>
9. <span data-ttu-id="26787-241">Une fois la génération réussie, une nouvelle mise en production est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="26787-241">Once the build is successful, a new release is triggered.</span></span>
    - <span data-ttu-id="26787-242">Choisissez **Build & Release** (Générer et publier), puis **Mises en production**, pour voir le package de déploiement web distribué sur votre machine virtuelle IIS.</span><span class="sxs-lookup"><span data-stu-id="26787-242">Choose **Build & Release**, then **Releases** to see the web deploy package pushed to your IIS VM.</span></span> 
    - <span data-ttu-id="26787-243">Sélectionnez l’icône **Actualiser** pour mettre à jour l’état.</span><span class="sxs-lookup"><span data-stu-id="26787-243">Select the **Refresh** icon to update the status.</span></span> <span data-ttu-id="26787-244">Lorsque la colonne *Environnements* affiche une coche verte, cela signifie que la mise en production a bien été déployée sur IIS.</span><span class="sxs-lookup"><span data-stu-id="26787-244">When the *Environments* column shows a green check mark, the release has successfully deployed to IIS.</span></span>
11. <span data-ttu-id="26787-245">Pour afficher les modifications que vous avez appliquées, actualisez votre site web IIS dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="26787-245">To see your changes applied, refresh your IIS website in a browser.</span></span>

    ![Application web ASP.NET s’exécutant sur une machine virtuelle IIS à partir d’un pipeline CI/CD](media/tutorial-vsts-iis-cicd/running_web_app_cicd.png)


## <a name="next-steps"></a><span data-ttu-id="26787-247">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="26787-247">Next steps</span></span>

<span data-ttu-id="26787-248">Dans ce didacticiel, vous avez créé une application web ASP.NET dans Team Services et configuré des définitions de build et de mise en production pour déployer de nouveaux packages de déploiement web sur IIS lors de la validation de chaque code.</span><span class="sxs-lookup"><span data-stu-id="26787-248">In this tutorial, you created an ASP.NET web application in Team Services and configured build and release definitions to deploy new web deploy packages to IIS on each code commit.</span></span> <span data-ttu-id="26787-249">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="26787-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="26787-250">Publier une application web ASP.NET dans un projet Team Services</span><span class="sxs-lookup"><span data-stu-id="26787-250">Publish an ASP.NET web application to a Team Services project</span></span>
> * <span data-ttu-id="26787-251">Créer une définition de build qui est déclenchée par les validations de code</span><span class="sxs-lookup"><span data-stu-id="26787-251">Create a build definition that is triggered by code commits</span></span>
> * <span data-ttu-id="26787-252">Installer et configurer IIS sur une machine virtuelle dans Azure</span><span class="sxs-lookup"><span data-stu-id="26787-252">Install and configure IIS on a virtual machine in Azure</span></span>
> * <span data-ttu-id="26787-253">Ajouter l’instance IIS à un groupe de déploiement dans Team Services</span><span class="sxs-lookup"><span data-stu-id="26787-253">Add the IIS instance to a deployment group in Team Services</span></span>
> * <span data-ttu-id="26787-254">Créer une définition de version pour publier les nouveaux packages de déploiement web sur IIS</span><span class="sxs-lookup"><span data-stu-id="26787-254">Create a release definition to publish new web deploy packages to IIS</span></span>
> * <span data-ttu-id="26787-255">test du pipeline CI/CD</span><span class="sxs-lookup"><span data-stu-id="26787-255">Test the CI/CD pipeline</span></span>

<span data-ttu-id="26787-256">Passez au didacticiel suivant pour savoir comment mieux protéger les serveurs SSL à l’aide des certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="26787-256">Advance to the next tutorial to learn how to secure a web server with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="26787-257">Sécuriser un serveur web avec SSL</span><span class="sxs-lookup"><span data-stu-id="26787-257">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)