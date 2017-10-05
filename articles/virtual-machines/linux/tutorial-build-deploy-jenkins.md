---
title: "Intégration continue/déploiement continu de Jenkins vers des machines virtuelles Azure avec Team Services | Microsoft Docs"
description: "Configurer l’intégration continue (CI) et le déploiement continu (CD) d’une application Node.js à l’aide de Jenkins vers des machines virtuelles Azure à partir de Release Management dans Visual Studio Team Services (VSTS) ou Microsoft Team Foundation Server (TFS)"
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
ms.openlocfilehash: a40e26a8681df31fad664e4d1df4c1513311900d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-app-to-linux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="8a10e-103">Déployer votre application sur des machines virtuelles Linux à l’aide de Jenkins et Team Services</span><span class="sxs-lookup"><span data-stu-id="8a10e-103">Deploy your app to Linux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="8a10e-104">L’intégration continue (CI) et le déploiement continu (CD) constituent un pipeline via lequel vous pouvez générer, mettre en production et déployer votre code.</span><span class="sxs-lookup"><span data-stu-id="8a10e-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="8a10e-105">Team Services fournit un ensemble complet d’outils d’automatisation CI/CD pour le déploiement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="8a10e-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment to Azure.</span></span> <span data-ttu-id="8a10e-106">Jenkins est un outil serveur CI/CD tiers populaire qui propose également l’automatisation CI/CD.</span><span class="sxs-lookup"><span data-stu-id="8a10e-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="8a10e-107">Vous pouvez les utiliser ensemble pour personnaliser la façon dont vous proposez votre service ou application cloud.</span><span class="sxs-lookup"><span data-stu-id="8a10e-107">You can use both together to customize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="8a10e-108">Dans ce didacticiel, vous utilisez Jenkins pour générer une **application web Node.js** et Visual Studio Team Services pour la déployer sur un [groupe de déploiement](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) contenant des machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="8a10e-108">In this tutorial, you use Jenkins to build a **Node.js web app**, and Visual Studio Team Services to deploy it to a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="8a10e-109">Vous allez :</span><span class="sxs-lookup"><span data-stu-id="8a10e-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a10e-110">Générer votre application dans Jenkins</span><span class="sxs-lookup"><span data-stu-id="8a10e-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="8a10e-111">Configurer Jenkins pour l’intégration Team Services</span><span class="sxs-lookup"><span data-stu-id="8a10e-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="8a10e-112">Créer un groupe de déploiement pour les machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="8a10e-112">Create a deployment group for the Azure virtual machines</span></span>
> * <span data-ttu-id="8a10e-113">Créer une définition de mise en production qui configure les machines virtuelles et déploie l’application</span><span class="sxs-lookup"><span data-stu-id="8a10e-113">Create a release definition that configures the VMs and deploys the app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8a10e-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="8a10e-114">Before you begin</span></span>

* <span data-ttu-id="8a10e-115">Vous devez avoir accès à un compte de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="8a10e-115">You need access to a Jenkins account.</span></span> <span data-ttu-id="8a10e-116">Si vous n’avez pas encore créé de serveur Jenkins, consultez la [documentation Jenkins](https://jenkins.io/doc/).</span><span class="sxs-lookup"><span data-stu-id="8a10e-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="8a10e-117">Connectez-vous à votre compte Team Services (`https://{youraccount}.visualstudio.com`).</span><span class="sxs-lookup"><span data-stu-id="8a10e-117">Sign in to your Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="8a10e-118">Vous pouvez obtenir un [compte Team Services gratuit](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span><span class="sxs-lookup"><span data-stu-id="8a10e-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="8a10e-119">Pour plus d’informations, consultez [Connect to Visual Studio Team Services from Eclipse, Xcode, Visual Studio, and more](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services) (Se connecter à Visual Studio Team Services depuis Eclipse, Xcode, Visual Studio, etc.).</span><span class="sxs-lookup"><span data-stu-id="8a10e-119">For more information, see [Connect to Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="8a10e-120">Créez un jeton d’accès personnel (PAT) dans votre compte Team Services si vous n’en avez pas encore.</span><span class="sxs-lookup"><span data-stu-id="8a10e-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="8a10e-121">Jenkins requiert ces informations pour accéder à votre compte Team Services.</span><span class="sxs-lookup"><span data-stu-id="8a10e-121">Jenkins requires this information to access your Team Services account.</span></span>
  <span data-ttu-id="8a10e-122">Consultez [Authenticate access with personal access tokens for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) (Authentifier l’accès avec des jetons d’accès personnel pour Team Services et TFS) pour savoir comment en générer un.</span><span class="sxs-lookup"><span data-stu-id="8a10e-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) to learn how to generate one.</span></span>

## <a name="get-the-sample-app"></a><span data-ttu-id="8a10e-123">Obtenir l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="8a10e-123">Get the sample app</span></span>

<span data-ttu-id="8a10e-124">Vous devez déployer une application stockée dans un référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="8a10e-124">You need an app to deploy stored in a Git repository.</span></span>
<span data-ttu-id="8a10e-125">Pour ce didacticiel, nous vous recommandons d’utiliser [cet exemple d’application disponible sur GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span><span class="sxs-lookup"><span data-stu-id="8a10e-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="8a10e-126">Dupliquez cette application et notez son emplacement (URL) pour pouvoir l’utiliser ultérieurement dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="8a10e-126">Create a fork of this app and take note of the location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="8a10e-127">La duplication de l’application doit être **publique** pour simplifier la connexion à GitHub plus tard.</span><span class="sxs-lookup"><span data-stu-id="8a10e-127">Make the fork **public** to simplify connecting to GitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="8a10e-128">Pour plus d’informations, consultez [Fork A Repo](https://help.github.com/articles/fork-a-repo/) (Dupliquer un référentiel)et [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/) (Rendre public un référentiel privé).</span><span class="sxs-lookup"><span data-stu-id="8a10e-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="8a10e-129">L’application a été générée à l’aide de [Yeoman](http://yeoman.io/learning/index.html) ; elle utilise **Express**, **bower** et **grunt** et comprend certains packages **npm** en tant que dépendances.</span><span class="sxs-lookup"><span data-stu-id="8a10e-129">The app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="8a10e-130">L’exemple d’application contient un ensemble de [modèles Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) qui sont utilisés pour créer dynamiquement les machines virtuelles pour le déploiement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="8a10e-130">The sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used to dynamically create the virtual machines for deployment on Azure.</span></span> <span data-ttu-id="8a10e-131">Ces modèles sont utilisés par des tâches de la [définition de mise en production Team Services](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span><span class="sxs-lookup"><span data-stu-id="8a10e-131">These templates are used by tasks in the [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="8a10e-132">Le modèle principal crée un groupe de sécurité réseau, une machine virtuelle et un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8a10e-132">The main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="8a10e-133">Il attribue une adresse IP publique et ouvre le port 80 entrant.</span><span class="sxs-lookup"><span data-stu-id="8a10e-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="8a10e-134">Il ajoute également une balise qui est utilisée par le groupe de déploiement pour sélectionner les machines devant recevoir le déploiement.</span><span class="sxs-lookup"><span data-stu-id="8a10e-134">It also adds a tag that is used by the deployment group to select the machines to receive the deployment.</span></span>
>
> <span data-ttu-id="8a10e-135">L’exemple contient également un script qui configure Nginx et déploie l’application.</span><span class="sxs-lookup"><span data-stu-id="8a10e-135">The sample also contains a script that sets up Nginx and deploys the app.</span></span> <span data-ttu-id="8a10e-136">Il est exécuté sur chacune des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8a10e-136">It is executed on each of the virtual machines.</span></span> <span data-ttu-id="8a10e-137">Plus précisément, le script installe Node, Nginx et PM2. Il configure Nginx et PM2, puis démarre l’application Node.</span><span class="sxs-lookup"><span data-stu-id="8a10e-137">Specifically, the script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts the Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="8a10e-138">Configurer les plug-ins Jenkins</span><span class="sxs-lookup"><span data-stu-id="8a10e-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="8a10e-139">Tout d’abord, vous devez configurer deux plug-ins Jenkins pour **NodeJS** et **l’intégration avec Team Services**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="8a10e-140">Ouvrez votre compte Jenkins et choisissez **Manage Jenkins** (Gérer Jenkins).</span><span class="sxs-lookup"><span data-stu-id="8a10e-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="8a10e-141">Sur la page **Manage Jenkins** (Gérer Jenkins), choisissez **Manage Plugins** (Gérer les plug-ins).</span><span class="sxs-lookup"><span data-stu-id="8a10e-141">In the **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="8a10e-142">Filtrez la liste pour localiser le plug-in **NodeJS** et l’installer sans redémarrage.</span><span class="sxs-lookup"><span data-stu-id="8a10e-142">Filter the list to locate the **NodeJS** plugin and install it without restart.</span></span>

   ![Ajout du plug-in NodeJS à Jenkins](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="8a10e-144">Filtrez la liste pour rechercher le plug-in **Team Foundation Server** et installez-le.</span><span class="sxs-lookup"><span data-stu-id="8a10e-144">Filter the list to find the **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="8a10e-145">(Ce plug-in fonctionne pour Team Services et Team Foundation Server.) Le redémarrage de Jenkins n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8a10e-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="8a10e-146">Configurer la génération Jenkins pour Node.js</span><span class="sxs-lookup"><span data-stu-id="8a10e-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="8a10e-147">Dans Jenkins, créez un projet de génération et configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a10e-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="8a10e-148">Dans l’onglet **Général**, entrez un nom pour votre projet de génération.</span><span class="sxs-lookup"><span data-stu-id="8a10e-148">In the **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="8a10e-149">Dans l’onglet **Gestion du code source**, sélectionnez **Git** et entrez les détails du référentiel et la branche qui contient le code de votre application.</span><span class="sxs-lookup"><span data-stu-id="8a10e-149">In the **Source Code Management** tab, select **Git** and enter the details of the repository and the branch containing your app code.</span></span>

   ![Ajouter un référentiel à votre génération](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="8a10e-151">Si votre référentiel n’est pas public, choisissez **Ajouter** et fournissez des informations d’identification pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="8a10e-151">If your repository is not public, choose **Add** and provide credentials to connect to it.</span></span>

1. <span data-ttu-id="8a10e-152">Dans l’onglet **Build Triggers** (Générer des déclencheurs), sélectionnez **Poll SCM** (Interroger SCM) et entrez la planification `H/03 * * * *` pour interroger le référentiel Git pour les modifications toutes les trois minutes.</span><span class="sxs-lookup"><span data-stu-id="8a10e-152">In the **Build Triggers** tab, select **Poll SCM** and enter the schedule `H/03 * * * *` to poll the Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="8a10e-153">Dans l’onglet **Build Environment** (Générer un environnement), sélectionnez **Provide Node &amp; npm bin/ folder PATH** (Fournir le CHEMIN D’ACCÈS au dossier npm bin/ et à Node) et saisissez `NodeJS` pour la valeur d’installation de Node JS.</span><span class="sxs-lookup"><span data-stu-id="8a10e-153">In the **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for the Node JS Installation value.</span></span> <span data-ttu-id="8a10e-154">Laissez **npmrc file** (fichier npmrc) défini sur « utiliser les valeurs par défaut du système ».</span><span class="sxs-lookup"><span data-stu-id="8a10e-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="8a10e-155">Dans l’onglet **Générer**, entrez la commande `npm install` pour vous assurer que toutes les dépendances sont mises à jour.</span><span class="sxs-lookup"><span data-stu-id="8a10e-155">In the **Build** tab, enter the command `npm install` to ensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="8a10e-156">Configurer Jenkins pour l’intégration Team Services</span><span class="sxs-lookup"><span data-stu-id="8a10e-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="8a10e-157">Dans l’onglet **Post-build Actions** (Actions post-génération), pour **Files to archive** (Fichiers à archiver), entrez `**/*` pour inclure tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="8a10e-157">In the **Post-build Actions** tab, for **Files to archive**, enter `**/*` to include all files.</span></span>

1. <span data-ttu-id="8a10e-158">Pour **Trigger release in TFS/Team Services** (Déclencher la mise en production dans TFS/Team Services), entrez l’URL complète de votre compte (tel que `https://your-account-name.visualstudio.com`), le nom du projet, un nom pour la définition de mise en production (créée ultérieurement) et les informations d’identification pour vous connecter à votre compte.</span><span class="sxs-lookup"><span data-stu-id="8a10e-158">For **Trigger release in TFS/Team Services**, enter the full URL of your account (such as `https://your-account-name.visualstudio.com`), the project name, a name for the release definition (created later), and the credentials to connect to your account.</span></span>
   <span data-ttu-id="8a10e-159">Vous avez besoin de votre nom d’utilisateur et du jeton d’accès personnel créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="8a10e-159">You need your user name and the PAT you created earlier.</span></span> 

   ![Configuration des actions post-génération Jenkins](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="8a10e-161">Enregistrez le projet de génération.</span><span class="sxs-lookup"><span data-stu-id="8a10e-161">Save the build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="8a10e-162">Créer un point de terminaison de service Jenkins</span><span class="sxs-lookup"><span data-stu-id="8a10e-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="8a10e-163">Un point de terminaison de service permet à Team Services de se connecter à Jenkins.</span><span class="sxs-lookup"><span data-stu-id="8a10e-163">A service endpoint allows Team Services to connect to Jenkins.</span></span>

1. <span data-ttu-id="8a10e-164">Ouvrez la page **Services** dans Team Services, ouvrez la liste **Nouveau point de terminaison de service** et choisissez **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-164">Open the **Services** page in Team Services, open the **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![Ajouter un point de terminaison Jenkins](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="8a10e-166">Entrez un nom à utiliser pour faire référence à cette connexion.</span><span class="sxs-lookup"><span data-stu-id="8a10e-166">Enter a name you will use to refer to this connection.</span></span>

1. <span data-ttu-id="8a10e-167">Entrez l’URL de votre serveur Jenkins et cochez l’option **Accepter les certificats SSL non fiables**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-167">Enter the URL of your Jenkins server, and tick the **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="8a10e-168">Entrez le nom d’utilisateur et le mot de passe de votre compte Jenkins.</span><span class="sxs-lookup"><span data-stu-id="8a10e-168">Enter the user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="8a10e-169">Choisissez **Vérifier la connexion** pour vérifier que les informations sont correctes.</span><span class="sxs-lookup"><span data-stu-id="8a10e-169">Choose **Verify connection** to check that the information is correct.</span></span>

1. <span data-ttu-id="8a10e-170">Sélectionnez **OK** pour créer le point de terminaison de service.</span><span class="sxs-lookup"><span data-stu-id="8a10e-170">Choose **OK** to create the service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="8a10e-171">Créer un groupe de déploiement</span><span class="sxs-lookup"><span data-stu-id="8a10e-171">Create a deployment group</span></span>

<span data-ttu-id="8a10e-172">Vous avez besoin d’un [groupe de déploiement](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) pour héberger les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8a10e-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) to  contain the virtual machines.</span></span>

1. <span data-ttu-id="8a10e-173">Ouvrez l’onglet **Mises en production** du hub **Build et mise en production**, puis ouvrez l’onglet **Groupes de déploiement**, puis choisissez **+ Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-173">Open the **Releases** tab of the **Build &amp; Release** hub, then open the **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="8a10e-174">Entrez un nom pour le groupe de déploiement, et éventuellement une description.</span><span class="sxs-lookup"><span data-stu-id="8a10e-174">Enter a name for the deployment group, and an optional description.</span></span>
   <span data-ttu-id="8a10e-175">Sélectionnez ensuite **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-175">Then choose **Create**.</span></span>

<span data-ttu-id="8a10e-176">La tâche Déploiement de groupe de ressources Azure crée et inscrit les machines virtuelles lorsqu’elle s’exécute à l’aide du modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8a10e-176">The Azure Resource Group Deployment task creates and registers the VMs when it runs using the Azure Resource Manager template.</span></span>
<span data-ttu-id="8a10e-177">Vous n’avez pas besoin de créer, ni d’inscrire les machines virtuelles vous-même.</span><span class="sxs-lookup"><span data-stu-id="8a10e-177">You don't need to create and register the virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="8a10e-178">Création d’une définition de version</span><span class="sxs-lookup"><span data-stu-id="8a10e-178">Create a release definition</span></span>

<span data-ttu-id="8a10e-179">Une définition de mise en production spécifie le processus que Team Services exécutera pour déployer l’application.</span><span class="sxs-lookup"><span data-stu-id="8a10e-179">A release definition specifies the process Team Services will execute to deploy the app.</span></span>
<span data-ttu-id="8a10e-180">Pour créer la définition de mise en production dans Team Services :</span><span class="sxs-lookup"><span data-stu-id="8a10e-180">To create the release definition in Team Services:</span></span>

1. <span data-ttu-id="8a10e-181">Ouvrez l’onglet **Mises en production** du hub **Build et mise en production**, ouvrez le menu déroulant **+** dans la liste des définitions de mise en production et choisissez **Créer une définition de mise en production**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-181">Open the **Releases** tab of the **Build &amp; Release** hub, open the **+** drop-down in the list of release definitions, and choose the **Create release definition**.</span></span> 

1. <span data-ttu-id="8a10e-182">Choisissez le modèle **Vide** et sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-182">Select the **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="8a10e-183">Dans la section **Artefacts**, cliquez sur **Lier une source d’artefact** et choisissez **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-183">In the **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="8a10e-184">Sélectionnez votre connexion de point de terminaison de service Jenkins.</span><span class="sxs-lookup"><span data-stu-id="8a10e-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="8a10e-185">Sélectionnez ensuite le travail de source Jenkins, puis choisissez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-185">Then select the Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="8a10e-186">Dans la nouvelle définition de mise en production, choisissez **+ Ajouter des tâches** et ajoutez une tâche **Déploiement de groupe de ressources Azure** à l’environnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="8a10e-186">In the new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task to the default environment.</span></span>

1. <span data-ttu-id="8a10e-187">Choisissez la flèche déroulante en regard du lien **+ Ajouter des tâches** et ajoutez une phase de groupe de déploiement à la définition.</span><span class="sxs-lookup"><span data-stu-id="8a10e-187">Choose the drop down arrow next to the **+ Add tasks** link and add a deployment group phase to the definition.</span></span>

   ![Ajout d’une phase de groupe de déploiement](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="8a10e-189">Dans le catalogue Tâche, ouvrez la section **Utilitaire** et ajoutez une instance de la tâche **Script Shell**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-189">In the Task catalog, open the **Utility** section and add an instance of the **Shell Script** task.</span></span>

1. <span data-ttu-id="8a10e-190">Le modèle de paramètres utilisé dans la tâche Déploiement de groupe de ressources Azure définit le mot de passe administrateur servant à se connecter aux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8a10e-190">The parameters template used in the Azure Resource Group Deployment task sets the admin password used to connect to the VMs.</span></span>
   <span data-ttu-id="8a10e-191">Vous fournissez ce mot de passe avec la variable **$(adminpassword)** :</span><span class="sxs-lookup"><span data-stu-id="8a10e-191">You provide this password with the variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="8a10e-192">Ouvrez l’onglet **Variables**et, dans la section **Variables**, entrez le nom `adminpassword`.</span><span class="sxs-lookup"><span data-stu-id="8a10e-192">Open the **Variables** tab and, in the **Variables** section, enter the name `adminpassword`.</span></span>

   - <span data-ttu-id="8a10e-193">Entrez le mot de passe d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8a10e-193">Enter the administrator password.</span></span>

   - <span data-ttu-id="8a10e-194">Cliquez sur l’icône de cadenas en regard de la zone de texte de valeur pour protéger le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8a10e-194">Choose the "padlock" icon next to the value textbox to protect the password.</span></span> 

## <a name="configure-the-azure-resource-group-deployment-task"></a><span data-ttu-id="8a10e-195">Configurer la tâche Déploiement de groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="8a10e-195">Configure the Azure Resource Group Deployment task</span></span>

<span data-ttu-id="8a10e-196">La tâche **Déploiement de groupe de ressources Azure** est utilisée pour créer le groupe de déploiement.</span><span class="sxs-lookup"><span data-stu-id="8a10e-196">The **Azure Resource Group Deployment** task is used to create the deployment group.</span></span> <span data-ttu-id="8a10e-197">Configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a10e-197">Configure it as follows:</span></span>

* <span data-ttu-id="8a10e-198">**Abonnement Azure :** sélectionnez une connexion dans la liste sous **Connexions au service Azure disponibles**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-198">**Azure Subscription:** Select a connection from the list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="8a10e-199">Si aucune connexion n’apparaît, choisissez **Gérer**, sélectionnez **Nouveau point de terminaison de service**, puis **Azure Resource Manager** et suivez les invites.</span><span class="sxs-lookup"><span data-stu-id="8a10e-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow the prompts.</span></span>
  <span data-ttu-id="8a10e-200">Revenez à votre définition de mise en production, actualisez la liste **Abonnement AzureRM** et sélectionnez la connexion que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="8a10e-200">Return to your release definition, refresh the **AzureRM Subscription** list, and select the connection you created.</span></span>

* <span data-ttu-id="8a10e-201">**Groupe de ressources** : entrez un nom pour le groupe de ressources que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="8a10e-201">**Resource group**: Enter a name of the resource group you created earlier.</span></span>

* <span data-ttu-id="8a10e-202">**Emplacement** : sélectionnez une région pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="8a10e-202">**Location**: Select a region for the deployment.</span></span>

  ![Création d’un groupe de ressources](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="8a10e-204">**Emplacement du modèle** : `URL of the file`</span><span class="sxs-lookup"><span data-stu-id="8a10e-204">**Template location**: `URL of the file`</span></span>

* <span data-ttu-id="8a10e-205">**Lien du modèle** : `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="8a10e-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="8a10e-206">**Lien des paramètres de modèle** : `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="8a10e-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="8a10e-207">**Remplacer les paramètres du modèle** : une liste des valeurs de remplacement, par exemple : `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span><span class="sxs-lookup"><span data-stu-id="8a10e-207">**Override template parameters**: A list of the override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="8a10e-208">Insérez vos propres valeurs spécifiques pour les {espaces réservés}.</span><span class="sxs-lookup"><span data-stu-id="8a10e-208">Insert your own specific values for the {placeholders}.</span></span> 

* <span data-ttu-id="8a10e-209">**Activer les prérequis** : `Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="8a10e-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="8a10e-210">**Point de terminaison TFS/VSTS** : choisissez **Ajouter** et, dans la boîte de dialogue « Add new Team Foundation Server/Team Services Connection » (Ajouter une connexion Team Foundation Server/Team Services), sélectionnez **Authentification basée sur un jeton**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-210">**TFS/VSTS endpoint**: Choose **Add** and, in the "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="8a10e-211">Entrez un nom pour la connexion et l’URL de votre projet d’équipe.</span><span class="sxs-lookup"><span data-stu-id="8a10e-211">Enter a name of the connection and the URL of your team project.</span></span> <span data-ttu-id="8a10e-212">Ensuite, générez et saisissez un [jeton d’accès personnel (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) pour authentifier la connexion à votre projet d’équipe.</span><span class="sxs-lookup"><span data-stu-id="8a10e-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) to authenticate the connection to your team project.</span></span>

  ![Créer un jeton d’accès personnel](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="8a10e-214">**Projet d’équipe** : sélectionnez votre projet actuel.</span><span class="sxs-lookup"><span data-stu-id="8a10e-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="8a10e-215">**Groupe de déploiement** : entrez le même nom de groupe de déploiement que celui que vous avez utilisé pour le paramètre **Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-215">**Deployment Group**: Enter the same deployment group name as you used for the **Resource group** parameter.</span></span>

<span data-ttu-id="8a10e-216">Les paramètres par défaut de la tâche Déploiement de groupe de ressources Azure servent à créer ou mettre à jour une ressource de façon incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="8a10e-216">The default settings for the Azure Resource Group Deployment task are to create or update a resource, and to do so incrementally.</span></span> <span data-ttu-id="8a10e-217">La tâche crée les machines virtuelles la première fois qu’elle est exécutée, puis les met simplement à jour.</span><span class="sxs-lookup"><span data-stu-id="8a10e-217">The task creates the VMs the first time it runs, and subsequently just update them.</span></span>

## <a name="configure-the-shell-script-task"></a><span data-ttu-id="8a10e-218">Configurer la tâche Shell Script</span><span class="sxs-lookup"><span data-stu-id="8a10e-218">Configure the Shell Script task</span></span>

<span data-ttu-id="8a10e-219">La tâche **Script Shell** est utilisée pour fournir la configuration d’un script à exécuter sur chaque serveur, afin d’installer Node.js et de démarrer l’application.</span><span class="sxs-lookup"><span data-stu-id="8a10e-219">The **Shell Script** task is used to provide the configuration for a script to run on each server to install Node.js and start the app.</span></span> <span data-ttu-id="8a10e-220">Configurez-le comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a10e-220">Configure it as follows:</span></span>

* <span data-ttu-id="8a10e-221">**Chemin d’accès au script** : `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="8a10e-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="8a10e-222">**Spécifier le répertoire de travail** : `Checked`</span><span class="sxs-lookup"><span data-stu-id="8a10e-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="8a10e-223">**Répertoire de travail** : `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="8a10e-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-the-release-definition"></a><span data-ttu-id="8a10e-224">Renommer et enregistrer la définition de mise en production</span><span class="sxs-lookup"><span data-stu-id="8a10e-224">Rename and save the release definition</span></span>

1. <span data-ttu-id="8a10e-225">Modifiez le nom de la définition de mise en production pour le remplacer par le nom que vous avez spécifié dans l’onglet **Actions post-génération** de la build dans Jenkins.</span><span class="sxs-lookup"><span data-stu-id="8a10e-225">Edit the name of the release definition to the name you specified in the **Post-build Actions** tab of the build in Jenkins.</span></span> <span data-ttu-id="8a10e-226">Jenkins exige que ce nom soit en mesure de déclencher une nouvelle mise en production lorsque les artefacts source sont mis à jour.</span><span class="sxs-lookup"><span data-stu-id="8a10e-226">Jenkins requires this name to be able to trigger a new release when the source artifacts are updated.</span></span>

1. <span data-ttu-id="8a10e-227">Si vous le souhaitez, modifiez le nom de l’environnement en cliquant sur dessus.</span><span class="sxs-lookup"><span data-stu-id="8a10e-227">Optionally, change the name of the environment by clicking on the name.</span></span> 

1. <span data-ttu-id="8a10e-228">Choisissez **Enregistrer**, puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="8a10e-229">Démarrer un déploiement manuel</span><span class="sxs-lookup"><span data-stu-id="8a10e-229">Start a manual deployment</span></span>

1. <span data-ttu-id="8a10e-230">Choisissez **+ Mise en production** et sélectionnez **Créer une mise en production**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="8a10e-231">Sélectionnez la génération que vous avez effectuée dans la liste déroulante en surbrillance et choisissez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8a10e-231">Select the build you completed in the highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="8a10e-232">Dans le message qui s’affiche, sélectionnez le lien de la mise en production.</span><span class="sxs-lookup"><span data-stu-id="8a10e-232">Choose the release link in the popup message.</span></span> <span data-ttu-id="8a10e-233">Par exemple : « Mise en production **Mise en production-1** a été créé. ».</span><span class="sxs-lookup"><span data-stu-id="8a10e-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="8a10e-234">Ouvrez l’onglet **Journaux** pour surveiller la sortie de console de mise en production.</span><span class="sxs-lookup"><span data-stu-id="8a10e-234">Open the **Logs** tab to watch the release console output.</span></span>

1. <span data-ttu-id="8a10e-235">Dans votre navigateur, ouvrez l’URL de l’un des serveurs que vous avez ajoutés à votre groupe de déploiement.</span><span class="sxs-lookup"><span data-stu-id="8a10e-235">In your browser, open the URL of one of the servers you added to your deployment group.</span></span> <span data-ttu-id="8a10e-236">Par exemple, entrez `http://{your-server-ip-address}`.</span><span class="sxs-lookup"><span data-stu-id="8a10e-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="8a10e-237">Démarrer un déploiement CI/CD</span><span class="sxs-lookup"><span data-stu-id="8a10e-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="8a10e-238">Dans la définition de mise en production, décochez la case **Activé** dans la section **Options de contrôle** des paramètres de la tâche Déploiement de groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="8a10e-238">In the release definition, uncheck the **Enabled** checkbox in the **Control Options** section of the settings for the Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="8a10e-239">Pour les futurs déploiements sur le groupe de déploiement existant, vous n’avez pas besoin de réexécuter cette tâche.</span><span class="sxs-lookup"><span data-stu-id="8a10e-239">For future deployments to the existing deployment group, you do not need to re-execute this task.</span></span>

1. <span data-ttu-id="8a10e-240">Accédez au référentiel Git source et modifiez le contenu du titre **h1** dans le fichier [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span><span class="sxs-lookup"><span data-stu-id="8a10e-240">Go to the source Git repository and modify the contents of the **h1** heading in the file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="8a10e-241">Validez votre modification.</span><span class="sxs-lookup"><span data-stu-id="8a10e-241">Commit your change.</span></span>

1. <span data-ttu-id="8a10e-242">Après quelques minutes, vous verrez une nouvelle mise en production sur la page **Mises en production** de Team Services ou TFS.</span><span class="sxs-lookup"><span data-stu-id="8a10e-242">After a few minutes, you will see a new release created in the **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="8a10e-243">Ouvrez la mise en production pour voir le déploiement en action.</span><span class="sxs-lookup"><span data-stu-id="8a10e-243">Open the release to see the deployment taking place.</span></span> <span data-ttu-id="8a10e-244">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="8a10e-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a10e-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8a10e-245">Next Steps</span></span>

<span data-ttu-id="8a10e-246">Dans ce didacticiel, vous avez automatisé le déploiement d’une application Azure à l’aide d’une build Jenkins et de Team Services pour la mise en production.</span><span class="sxs-lookup"><span data-stu-id="8a10e-246">In this tutorial, you automated the deployment of an app to Azure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="8a10e-247">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="8a10e-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a10e-248">Générer votre application dans Jenkins</span><span class="sxs-lookup"><span data-stu-id="8a10e-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="8a10e-249">Configurer Jenkins pour l’intégration Team Services</span><span class="sxs-lookup"><span data-stu-id="8a10e-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="8a10e-250">Créer un groupe de déploiement pour les machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="8a10e-250">Create a deployment group for the Azure virtual machines</span></span>
> * <span data-ttu-id="8a10e-251">Créer une définition de mise en production qui configure les machines virtuelles et déploie l’application</span><span class="sxs-lookup"><span data-stu-id="8a10e-251">Create a release definition that configures the VMs and deploys the app</span></span>

<span data-ttu-id="8a10e-252">Passez au didacticiel suivant pour en savoir plus sur le déploiement d’une pile LAMP (Linux, Apache, MySQL et PHP).</span><span class="sxs-lookup"><span data-stu-id="8a10e-252">Advance to the next tutorial to learn more about how to deploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8a10e-253">Déploiement d’une pile LAMP dans Azure</span><span class="sxs-lookup"><span data-stu-id="8a10e-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)