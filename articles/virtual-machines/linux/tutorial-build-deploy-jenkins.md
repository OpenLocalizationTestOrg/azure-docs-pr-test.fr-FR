---
title: aaaCI/CD de Jenkins tooAzure machines virtuelles avec Team Services | Documents Microsoft
description: "Configurer l’intégration continue (CI) et le déploiement continu (CD) d’une application Node.js à l’aide de machines virtuelles de tooAzure Jenkins à partir de la gestion des versions dans Visual Studio Team Services (VSTS) ou Microsoft Team Foundation Server (TFS)"
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="9c6a1-103">Déployer votre application de tooLinux machines virtuelles à l’aide de Jenkins et Team Services</span><span class="sxs-lookup"><span data-stu-id="9c6a1-103">Deploy your app tooLinux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="9c6a1-104">L’intégration continue (CI) et le déploiement continu (CD) constituent un pipeline via lequel vous pouvez générer, mettre en production et déployer votre code.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="9c6a1-105">Team Services fournit un ensemble de CD de l’élément de configuration/Outils d’automatisation complète et complet pour tooAzure de déploiement.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment tooAzure.</span></span> <span data-ttu-id="9c6a1-106">Jenkins est un outil serveur CI/CD tiers populaire qui propose également l’automatisation CI/CD.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="9c6a1-107">Vous pouvez utiliser les deux ensemble toocustomize comment livrer votre application cloud ou le service.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-107">You can use both together toocustomize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="9c6a1-108">Dans ce didacticiel, vous utilisez Jenkins toobuild un **application web Node.js**et Visual Studio Team Services toodeploy il tooa [groupe de déploiement](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) contenant des ordinateurs virtuels Linux.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-108">In this tutorial, you use Jenkins toobuild a **Node.js web app**, and Visual Studio Team Services toodeploy it tooa [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="9c6a1-109">Vous allez :</span><span class="sxs-lookup"><span data-stu-id="9c6a1-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9c6a1-110">Générer votre application dans Jenkins</span><span class="sxs-lookup"><span data-stu-id="9c6a1-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="9c6a1-111">Configurer Jenkins pour l’intégration Team Services</span><span class="sxs-lookup"><span data-stu-id="9c6a1-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="9c6a1-112">Créer un groupe de déploiement hello pour les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="9c6a1-112">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="9c6a1-113">Créer une définition de mise en production qui configure les ordinateurs virtuels de hello et déploie l’application hello</span><span class="sxs-lookup"><span data-stu-id="9c6a1-113">Create a release definition that configures hello VMs and deploys hello app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9c6a1-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="9c6a1-114">Before you begin</span></span>

* <span data-ttu-id="9c6a1-115">Vous devez le compte d’accès tooa Jenkins.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-115">You need access tooa Jenkins account.</span></span> <span data-ttu-id="9c6a1-116">Si vous n’avez pas encore créé de serveur Jenkins, consultez la [documentation Jenkins](https://jenkins.io/doc/).</span><span class="sxs-lookup"><span data-stu-id="9c6a1-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="9c6a1-117">Connectez-vous à tooyour compte Team Services (`https://{youraccount}.visualstudio.com`).</span><span class="sxs-lookup"><span data-stu-id="9c6a1-117">Sign in tooyour Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="9c6a1-118">Vous pouvez obtenir un [compte Team Services gratuit](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span><span class="sxs-lookup"><span data-stu-id="9c6a1-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="9c6a1-119">Pour plus d’informations, consultez [connecter les Services de tooTeam](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="9c6a1-119">For more information, see [Connect tooTeam Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="9c6a1-120">Créez un jeton d’accès personnel (PAT) dans votre compte Team Services si vous n’en avez pas encore.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="9c6a1-121">Jenkins requiert cette tooaccess informations de votre compte Team Services.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-121">Jenkins requires this information tooaccess your Team Services account.</span></span>
  <span data-ttu-id="9c6a1-122">Lecture [comment créer un jeton d’accès personnel pour Team Services et TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn comment toogenerate une.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn how toogenerate one.</span></span>

## <a name="get-hello-sample-app"></a><span data-ttu-id="9c6a1-123">Obtenir l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="9c6a1-123">Get hello sample app</span></span>

<span data-ttu-id="9c6a1-124">Vous avez besoin d’un toodeploy d’application stocké dans un référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-124">You need an app toodeploy stored in a Git repository.</span></span>
<span data-ttu-id="9c6a1-125">Pour ce didacticiel, nous vous recommandons d’utiliser [cet exemple d’application disponible sur GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span><span class="sxs-lookup"><span data-stu-id="9c6a1-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="9c6a1-126">Créer une branche de cette application et notez hello emplacement (URL) pour une utilisation dans les étapes ultérieures de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-126">Create a fork of this app and take note of hello location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="9c6a1-127">Vérifiez le branchement de hello **public** toosimplify vous tooGitHub plus tard.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-127">Make hello fork **public** toosimplify connecting tooGitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="9c6a1-128">Pour plus d’informations, consultez [Fork A Repo](https://help.github.com/articles/fork-a-repo/) (Dupliquer un référentiel)et [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/) (Rendre public un référentiel privé).</span><span class="sxs-lookup"><span data-stu-id="9c6a1-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="9c6a1-129">application Hello a été générée à l’aide de [Yeoman](http://yeoman.io/learning/index.html); elle utilise **Express**, **bower**, et **grunt**; et qu’il a certaines **npm**packages en tant que dépendances.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-129">hello app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="9c6a1-130">Hello, exemple d’application contient un ensemble de [modèles Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) que sont toodynamically utilisé créer des machines virtuelles de hello pour le déploiement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-130">hello sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used toodynamically create hello virtual machines for deployment on Azure.</span></span> <span data-ttu-id="9c6a1-131">Ces modèles sont utilisés par des tâches de hello [Team Services version définition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span><span class="sxs-lookup"><span data-stu-id="9c6a1-131">These templates are used by tasks in hello [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="9c6a1-132">les modèles principal Hello crée un groupe de sécurité réseau, un ordinateur virtuel et un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-132">hello main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="9c6a1-133">Il attribue une adresse IP publique et ouvre le port 80 entrant.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="9c6a1-134">Il ajoute également une balise qui est utilisée par hello groupe hello trop sélectionnez machines tooreceive hello un déploiement.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-134">It also adds a tag that is used by hello deployment group too select hello machines tooreceive hello deployment.</span></span>
>
> <span data-ttu-id="9c6a1-135">exemple Hello contient également un script qui configure Nginx et déploie l’application hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-135">hello sample also contains a script that sets up Nginx and deploys hello app.</span></span> <span data-ttu-id="9c6a1-136">Il est exécuté sur chacun des ordinateurs virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-136">It is executed on each of hello virtual machines.</span></span> <span data-ttu-id="9c6a1-137">Plus précisément, le script de hello installe nœud Nginx et PM2 ; Configure Nginx et PM2 ; démarre ensuite l’application de nœud hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-137">Specifically, hello script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts hello Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="9c6a1-138">Configurer les plug-ins Jenkins</span><span class="sxs-lookup"><span data-stu-id="9c6a1-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="9c6a1-139">Tout d’abord, vous devez configurer deux plug-ins Jenkins pour **NodeJS** et **l’intégration avec Team Services**.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="9c6a1-140">Ouvrez votre compte Jenkins et choisissez **Manage Jenkins** (Gérer Jenkins).</span><span class="sxs-lookup"><span data-stu-id="9c6a1-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="9c6a1-141">Bonjour **gérer les Jenkins** choisissez **gérer les plug-ins**.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-141">In hello **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="9c6a1-142">Filtre Bonjour liste toolocate Bonjour **NodeJS** plug-in et l’installer sans redémarrage.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-142">Filter hello list toolocate hello **NodeJS** plugin and install it without restart.</span></span>

   ![Ajout de hello NodeJS plug-in tooJenkins](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="9c6a1-144">Filtre Bonjour liste toofind Bonjour **Team Foundation Server** plug-in et l’installer.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-144">Filter hello list toofind hello **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="9c6a1-145">(Ce plug-in fonctionne pour Team Services et Team Foundation Server.) Le redémarrage de Jenkins n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="9c6a1-146">Configurer la génération Jenkins pour Node.js</span><span class="sxs-lookup"><span data-stu-id="9c6a1-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="9c6a1-147">Dans Jenkins, créez un projet de génération et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="9c6a1-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="9c6a1-148">Bonjour **général** , entrez un nom pour votre projet de build.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-148">In hello **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="9c6a1-149">Bonjour **gestion du Code Source** onglet, sélectionnez **Git** et entrez les détails de hello du référentiel de hello et de branche hello contenant le code de votre application.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-149">In hello **Source Code Management** tab, select **Git** and enter hello details of hello repository and hello branch containing your app code.</span></span>

   ![Ajouter une build tooyour de référentiel](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="9c6a1-151">Si votre référentiel n’est pas public, choisissez **ajouter** et fournir des informations d’identification tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-151">If your repository is not public, choose **Add** and provide credentials tooconnect tooit.</span></span>

1. <span data-ttu-id="9c6a1-152">Bonjour **déclencheurs de Build** onglet, sélectionnez **interrogation SCM** et entrez la planification de hello `H/03 * * * *` référentiel Git toopoll hello modifications toutes les trois minutes.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-152">In hello **Build Triggers** tab, select **Poll SCM** and enter hello schedule `H/03 * * * *` toopoll hello Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="9c6a1-153">Bonjour **environnement Build** onglet, sélectionnez **fournissent un nœud &amp; npm bin / chemin d’accès de dossier** et entrez `NodeJS` pour hello valeur du nœud JS Installation.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-153">In hello **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for hello Node JS Installation value.</span></span> <span data-ttu-id="9c6a1-154">Laissez **npmrc file** (fichier npmrc) défini sur « utiliser les valeurs par défaut du système ».</span><span class="sxs-lookup"><span data-stu-id="9c6a1-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="9c6a1-155">Bonjour **générer** , entrez la commande hello `npm install` tooensure toutes les dépendances sont mises à jour.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-155">In hello **Build** tab, enter hello command `npm install` tooensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="9c6a1-156">Configurer Jenkins pour l’intégration Team Services</span><span class="sxs-lookup"><span data-stu-id="9c6a1-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="9c6a1-157">Bonjour **post-build Actions** onglet, pour **tooarchive de fichiers**, entrez `**/*` tooinclude tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-157">In hello **Post-build Actions** tab, for **Files tooarchive**, enter `**/*` tooinclude all files.</span></span>

1. <span data-ttu-id="9c6a1-158">Pour **déclencher la mise en production dans TFS/Team Services**, entrer une URL complète de votre compte hello (tel que `https://your-account-name.visualstudio.com`), hello nom du projet, un nom pour la définition de la version hello (créé ultérieurement), et hello des informations d’identification tooconnect tooyour compte.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-158">For **Trigger release in TFS/Team Services**, enter hello full URL of your account (such as `https://your-account-name.visualstudio.com`), hello project name, a name for hello release definition (created later), and hello credentials tooconnect tooyour account.</span></span>
   <span data-ttu-id="9c6a1-159">Vous avez besoin de votre nom d’utilisateur et le hello PAT que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-159">You need your user name and hello PAT you created earlier.</span></span> 

   ![Configuration des actions post-génération Jenkins](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="9c6a1-161">Enregistrez le projet de build hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-161">Save hello build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="9c6a1-162">Créer un point de terminaison de service Jenkins</span><span class="sxs-lookup"><span data-stu-id="9c6a1-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="9c6a1-163">Un point de terminaison de service permet de tooJenkins de tooconnect Team Services.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-163">A service endpoint allows Team Services tooconnect tooJenkins.</span></span>

1. <span data-ttu-id="9c6a1-164">Ouvrez hello **Services** page Team Services, ouvrez hello **nouveau point de terminaison de Service** liste, puis choisissez **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-164">Open hello **Services** page in Team Services, open hello **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![Ajouter un point de terminaison Jenkins](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="9c6a1-166">Entrez un nom que vous utiliserez toorefer toothis connexion.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-166">Enter a name you will use toorefer toothis connection.</span></span>

1. <span data-ttu-id="9c6a1-167">Entrez l’URL de hello de votre serveur Jenkins et graduations hello **accepter les certificats SSL non fiables** option.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-167">Enter hello URL of your Jenkins server, and tick hello **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="9c6a1-168">Entrez le nom d’utilisateur hello et le mot de passe pour votre compte Jenkins.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-168">Enter hello user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="9c6a1-169">Choisissez **vérifier connexion** toocheck qui hello informations est correct.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-169">Choose **Verify connection** toocheck that hello information is correct.</span></span>

1. <span data-ttu-id="9c6a1-170">Choisissez **OK** point de terminaison de service toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-170">Choose **OK** toocreate hello service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="9c6a1-171">Créer un groupe de déploiement</span><span class="sxs-lookup"><span data-stu-id="9c6a1-171">Create a deployment group</span></span>

<span data-ttu-id="9c6a1-172">Vous avez besoin une [groupe de déploiement](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) contiennent trop de machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) too contain hello virtual machines.</span></span>

1. <span data-ttu-id="9c6a1-173">Ouvrez hello **versions** onglet Hello **générer &amp; version** concentrateur, puis ouvrez hello **groupes de déploiement** onglet, puis choisissez **+ nouveau**.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-173">Open hello **Releases** tab of hello **Build &amp; Release** hub, then open hello **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="9c6a1-174">Entrez un nom pour le groupe de déploiement hello et une description facultative.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-174">Enter a name for hello deployment group, and an optional description.</span></span>
   <span data-ttu-id="9c6a1-175">Sélectionnez ensuite **Créer**.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-175">Then choose **Create**.</span></span>

<span data-ttu-id="9c6a1-176">tâche de déploiement de groupe de ressources Azure Hello crée et enregistre les machines virtuelles de hello lorsqu’elle s’exécute à l’aide du modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-176">hello Azure Resource Group Deployment task creates and registers hello VMs when it runs using hello Azure Resource Manager template.</span></span>
<span data-ttu-id="9c6a1-177">Vous ne devez toocreate et inscrire des machines virtuelles de hello vous-même.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-177">You don't need toocreate and register hello virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="9c6a1-178">Création d’une définition de version</span><span class="sxs-lookup"><span data-stu-id="9c6a1-178">Create a release definition</span></span>

<span data-ttu-id="9c6a1-179">Une définition de mise en production Spécifie le processus hello Team Services exécutera toodeploy hello application.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-179">A release definition specifies hello process Team Services will execute toodeploy hello app.</span></span>
<span data-ttu-id="9c6a1-180">définition de mise en production toocreate hello dans Team Services :</span><span class="sxs-lookup"><span data-stu-id="9c6a1-180">toocreate hello release definition in Team Services:</span></span>

1. <span data-ttu-id="9c6a1-181">Ouvrez hello **versions** onglet Hello **générer &amp; Release** hub, ouvrez hello  **+**  liste déroulante dans la liste hello des définitions de version, puis choisissez Hello **définition de créer la version**.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-181">Open hello **Releases** tab of hello **Build &amp; Release** hub, open hello **+** drop-down in hello list of release definitions, and choose hello **Create release definition**.</span></span> 

1. <span data-ttu-id="9c6a1-182">Sélectionnez hello **vide** modèle et choisissez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-182">Select hello **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="9c6a1-183">Bonjour **artefacts** section, cliquez sur **lier un artefact** et choisissez **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-183">In hello **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="9c6a1-184">Sélectionnez votre connexion de point de terminaison de service Jenkins.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="9c6a1-185">Sélectionnez le projet source de Jenkins hello ensuite et choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-185">Then select hello Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="9c6a1-186">Bonjour nouvelles release définition, choisissez **+ ajouter des tâches** et ajoutez un **déploiement de groupe de ressources Azure** toohello de l’environnement par défaut de tâche.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-186">In hello new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task toohello default environment.</span></span>

1. <span data-ttu-id="9c6a1-187">Choisissez hello déroulante toohello suivant de flèche **+ ajouter des tâches** lier et ajoutez une définition de déploiement groupe phase toohello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-187">Choose hello drop down arrow next toohello **+ Add tasks** link and add a deployment group phase toohello definition.</span></span>

   ![Ajout d’une phase de groupe de déploiement](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="9c6a1-189">Dans le catalogue de tâche hello, ouvrez hello **utilitaire** section et ajoutez une instance de hello **Script Shell** tâche.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-189">In hello Task catalog, open hello **Utility** section and add an instance of hello **Shell Script** task.</span></span>

1. <span data-ttu-id="9c6a1-190">modèle de paramètres de Hello utilisé dans la tâche de déploiement de groupe de ressources Azure hello définit hello admin avec le mot de passe utilisé tooconnect toohello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-190">hello parameters template used in hello Azure Resource Group Deployment task sets hello admin password used tooconnect toohello VMs.</span></span>
   <span data-ttu-id="9c6a1-191">Vous fournissez ce mot de passe avec la variable de hello **$(adminpassword)**:</span><span class="sxs-lookup"><span data-stu-id="9c6a1-191">You provide this password with hello variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="9c6a1-192">Ouvrez hello **Variables** onglet et hello **Variables** section, entrez le nom de hello `adminpassword`.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-192">Open hello **Variables** tab and, in hello **Variables** section, enter hello name `adminpassword`.</span></span>

   - <span data-ttu-id="9c6a1-193">Entrez le mot de passe administrateur hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-193">Enter hello administrator password.</span></span>

   - <span data-ttu-id="9c6a1-194">Choisissez hello cadenas » en » icône suivant toohello valeur textbox tooprotect hello mot de passe.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-194">Choose hello "padlock" icon next toohello value textbox tooprotect hello password.</span></span> 

## <a name="configure-hello-azure-resource-group-deployment-task"></a><span data-ttu-id="9c6a1-195">Configurer la tâche de déploiement de groupe de ressources Azure hello</span><span class="sxs-lookup"><span data-stu-id="9c6a1-195">Configure hello Azure Resource Group Deployment task</span></span>

<span data-ttu-id="9c6a1-196">Hello **déploiement de groupe de ressources Azure** tâche est le groupe de déploiement hello toocreate utilisé.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-196">hello **Azure Resource Group Deployment** task is used toocreate hello deployment group.</span></span> <span data-ttu-id="9c6a1-197">Configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="9c6a1-197">Configure it as follows:</span></span>

* <span data-ttu-id="9c6a1-198">**Abonnement Azure :** sélectionner une connexion à partir de la liste de hello sous **des connexions de Service Azure disponibles**.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-198">**Azure Subscription:** Select a connection from hello list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="9c6a1-199">Si aucune connexion n’apparaît, choisissez **gérer**, sélectionnez **nouveau point de terminaison de Service** puis **Azure Resource Manager**et suivez les invites hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow hello prompts.</span></span>
  <span data-ttu-id="9c6a1-200">Retourner tooyour hello d’actualisation, définition de la version **AzureRM abonnement** liste et la connexion hello sélectionnez vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-200">Return tooyour release definition, refresh hello **AzureRM Subscription** list, and select hello connection you created.</span></span>

* <span data-ttu-id="9c6a1-201">**Groupe de ressources**: entrez un nom de groupe de ressources hello vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-201">**Resource group**: Enter a name of hello resource group you created earlier.</span></span>

* <span data-ttu-id="9c6a1-202">**Emplacement**: sélectionnez une région pour le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-202">**Location**: Select a region for hello deployment.</span></span>

  ![Création d’un groupe de ressources](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="9c6a1-204">**Emplacement du modèle** : `URL of hello file`</span><span class="sxs-lookup"><span data-stu-id="9c6a1-204">**Template location**: `URL of hello file`</span></span>

* <span data-ttu-id="9c6a1-205">**Lien du modèle** : `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="9c6a1-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="9c6a1-206">**Lien des paramètres de modèle** : `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="9c6a1-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="9c6a1-207">**Remplacer les paramètres de modèle**: une liste de hello remplacer des valeurs, par exemple : `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-207">**Override template parameters**: A list of hello override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="9c6a1-208">Insérez vos propres valeurs spécifiques pour hello {des espaces réservés}.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-208">Insert your own specific values for hello {placeholders}.</span></span> 

* <span data-ttu-id="9c6a1-209">**Activer les prérequis** : `Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="9c6a1-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="9c6a1-210">**Point de terminaison TFS/VSTS**: choisissez **ajouter** et, dans le dialogue de « Ajouter la nouvelle connexion de Services de serveur/équipe Team Foundation » hello, sélectionnez **authentification jeton**.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-210">**TFS/VSTS endpoint**: Choose **Add** and, in hello "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="9c6a1-211">Entrez un nom de connexion de hello et URL hello de votre projet d’équipe.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-211">Enter a name of hello connection and hello URL of your team project.</span></span> <span data-ttu-id="9c6a1-212">Générer, puis entrez un [personnel Access jeton (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) projet d’équipe tooyour tooauthenticate hello connexion.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello connection tooyour team project.</span></span>

  ![Créer un jeton d’accès personnel](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="9c6a1-214">**Projet d’équipe** : sélectionnez votre projet actuel.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="9c6a1-215">**Groupe de déploiement**: entrez hello le même nom de groupe de déploiement que vous avez utilisé pour hello **groupe de ressources** paramètre.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-215">**Deployment Group**: Enter hello same deployment group name as you used for hello **Resource group** parameter.</span></span>

<span data-ttu-id="9c6a1-216">paramètres par défaut de Hello pour la tâche de déploiement de groupe de ressources Azure hello sont toocreate ou mise à jour d’une ressource et toodo donc incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-216">hello default settings for hello Azure Resource Group Deployment task are toocreate or update a resource, and toodo so incrementally.</span></span> <span data-ttu-id="9c6a1-217">tâche Hello crée hello de machines virtuelles hello première fois qu’elle s’exécute, les mettre à jour par la suite uniquement.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-217">hello task creates hello VMs hello first time it runs, and subsequently just update them.</span></span>

## <a name="configure-hello-shell-script-task"></a><span data-ttu-id="9c6a1-218">Configurer la tâche de Script Shell hello</span><span class="sxs-lookup"><span data-stu-id="9c6a1-218">Configure hello Shell Script task</span></span>

<span data-ttu-id="9c6a1-219">Hello **Script Shell** tâche est configuration de hello tooprovide utilisés pour un toorun de script sur chaque serveur tooinstall Node.js et démarrer hello d’application.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-219">hello **Shell Script** task is used tooprovide hello configuration for a script toorun on each server tooinstall Node.js and start hello app.</span></span> <span data-ttu-id="9c6a1-220">Configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="9c6a1-220">Configure it as follows:</span></span>

* <span data-ttu-id="9c6a1-221">**Chemin d’accès au script** : `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="9c6a1-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="9c6a1-222">**Spécifier le répertoire de travail** : `Checked`</span><span class="sxs-lookup"><span data-stu-id="9c6a1-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="9c6a1-223">**Répertoire de travail** : `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="9c6a1-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-hello-release-definition"></a><span data-ttu-id="9c6a1-224">Renommer et enregistrer la définition de la version hello</span><span class="sxs-lookup"><span data-stu-id="9c6a1-224">Rename and save hello release definition</span></span>

1. <span data-ttu-id="9c6a1-225">Modifier le nom hello hello version de définition de toohello vous avez spécifié dans le **post-build Actions** onglet de build Jenkins hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-225">Edit hello name of hello release definition toohello name you specified in the **Post-build Actions** tab of hello build in Jenkins.</span></span> <span data-ttu-id="9c6a1-226">Jenkins requiert cette tootrigger en mesure de nom toobe une nouvelle version mise à jour des artefacts de code source hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-226">Jenkins requires this name toobe able tootrigger a new release when hello source artifacts are updated.</span></span>

1. <span data-ttu-id="9c6a1-227">Modifiez éventuellement le nom hello d’environnement de hello en cliquant sur le nom de hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-227">Optionally, change hello name of hello environment by clicking on hello name.</span></span> 

1. <span data-ttu-id="9c6a1-228">Choisissez **Enregistrer**, puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="9c6a1-229">Démarrer un déploiement manuel</span><span class="sxs-lookup"><span data-stu-id="9c6a1-229">Start a manual deployment</span></span>

1. <span data-ttu-id="9c6a1-230">Choisissez **+ Mise en production** et sélectionnez **Créer une mise en production**.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="9c6a1-231">Sélectionnez la build hello vous terminé dans la liste déroulante de la mise en surbrillance hello et choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-231">Select hello build you completed in hello highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="9c6a1-232">Choisissez le lien de mise en production de hello dans un message contextuel hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-232">Choose hello release link in hello popup message.</span></span> <span data-ttu-id="9c6a1-233">Par exemple : « Mise en production **Mise en production-1** a été créé. ».</span><span class="sxs-lookup"><span data-stu-id="9c6a1-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="9c6a1-234">Ouvrez hello **journaux** onglet sortie de la console toowatch hello mise en production.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-234">Open hello **Logs** tab toowatch hello release console output.</span></span>

1. <span data-ttu-id="9c6a1-235">Dans votre navigateur, ouvrez hello URL de l’un des serveurs de hello, vous avez ajouté le groupe de déploiement tooyour.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-235">In your browser, open hello URL of one of hello servers you added tooyour deployment group.</span></span> <span data-ttu-id="9c6a1-236">Par exemple, entrez `http://{your-server-ip-address}`.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="9c6a1-237">Démarrer un déploiement CI/CD</span><span class="sxs-lookup"><span data-stu-id="9c6a1-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="9c6a1-238">Bonjour, lancez définition, décochez la case hello **activé** case à cocher Bonjour **contrôler les Options de** section des paramètres de hello pour la tâche de déploiement de groupe de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-238">In hello release definition, uncheck hello **Enabled** checkbox in hello **Control Options** section of hello settings for hello Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="9c6a1-239">Pour les déploiements futurs toohello déploiement groupe existant, vous n’avez pas besoin de toore-exécuter cette tâche.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-239">For future deployments toohello existing deployment group, you do not need toore-execute this task.</span></span>

1. <span data-ttu-id="9c6a1-240">Référentiel Git de source toohello et modifiez le contenu de hello Hello **h1** en-tête dans le fichier de hello [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span><span class="sxs-lookup"><span data-stu-id="9c6a1-240">Go toohello source Git repository and modify hello contents of hello **h1** heading in hello file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="9c6a1-241">Validez votre modification.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-241">Commit your change.</span></span>

1. <span data-ttu-id="9c6a1-242">Après quelques minutes, vous verrez une nouvelle version créée Bonjour **versions** page des Services d’équipe TFS.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-242">After a few minutes, you will see a new release created in hello **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="9c6a1-243">Ouvrez hello toosee hello déploiement se produisent.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-243">Open hello release toosee hello deployment taking place.</span></span> <span data-ttu-id="9c6a1-244">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9c6a1-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c6a1-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9c6a1-245">Next Steps</span></span>

<span data-ttu-id="9c6a1-246">Dans ce didacticiel, vous avez automatisé déploiement hello d’un tooAzure d’application à l’aide de la build Jenkins et Team Services pour cette version.</span><span class="sxs-lookup"><span data-stu-id="9c6a1-246">In this tutorial, you automated hello deployment of an app tooAzure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="9c6a1-247">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="9c6a1-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9c6a1-248">Générer votre application dans Jenkins</span><span class="sxs-lookup"><span data-stu-id="9c6a1-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="9c6a1-249">Configurer Jenkins pour l’intégration Team Services</span><span class="sxs-lookup"><span data-stu-id="9c6a1-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="9c6a1-250">Créer un groupe de déploiement hello pour les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="9c6a1-250">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="9c6a1-251">Créer une définition de mise en production qui configure les ordinateurs virtuels de hello et déploie l’application hello</span><span class="sxs-lookup"><span data-stu-id="9c6a1-251">Create a release definition that configures hello VMs and deploys hello app</span></span>

<span data-ttu-id="9c6a1-252">Avance toolearn de didacticiel suivant toohello plus d’informations sur la façon dont la pile toodeploy un feu (Linux, Apache, MySQL et PHP).</span><span class="sxs-lookup"><span data-stu-id="9c6a1-252">Advance toohello next tutorial toolearn more about how toodeploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9c6a1-253">Déploiement d’une pile LAMP dans Azure</span><span class="sxs-lookup"><span data-stu-id="9c6a1-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)