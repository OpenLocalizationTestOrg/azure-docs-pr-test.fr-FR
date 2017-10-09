---
title: "aaaCI/CD avec moteur du Service de conteneur d’Azure et de Swarm | Documents Microsoft"
description: Utiliser le moteur du Service de conteneur Azure avec le Mode de Docker Swarm un Registre de conteneur Azure et Visual Studio Team Services toodeliver en permanence une application de .NET Core conteneur multi
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: Docker, conteneurs, micro-services, Swarm, Azure, Visual Studio Team Services, DevOps, moteur ACS
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a><span data-ttu-id="a1c71-104">L’élément de configuration complet/CD pipeline toodeploy une application conteneur multiples sur un Service de conteneur Azure avec le moteur d’ACS et le Mode Docker Swarm à l’aide de Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a1c71-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Visual Studio Team Services</span></span>

<span data-ttu-id="a1c71-105">*Cet article est basé sur [/CD complète de l’élément de configuration de pipeline toodeploy une application conteneur multi Azure Service de conteneur avec Docker Swarm à l’aide de Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span><span class="sxs-lookup"><span data-stu-id="a1c71-105">*This article is based on [Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="a1c71-106">Aujourd'hui, un des hello plus grands défis lors de développement d’applications modernes pour le cloud de hello toodeliver en mesure de ces applications en continu.</span><span class="sxs-lookup"><span data-stu-id="a1c71-106">Nowadays, One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="a1c71-107">Dans cet article, vous découvrez comment tooimplement une intégration complète continue et déploiement (élément de configuration/CD) pipeline à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="a1c71-107">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="a1c71-108">Moteur Azure Container Service avec le mode Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="a1c71-108">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="a1c71-109">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a1c71-109">Azure Container Registry</span></span>
* <span data-ttu-id="a1c71-110">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a1c71-110">Visual Studio Team Services</span></span>

<span data-ttu-id="a1c71-111">Cet article est basé sur une application simple, disponible sur [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), développée avec ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="a1c71-111">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="a1c71-112">application Hello est composée de quatre services différents : trois web API et un site web frontal :</span><span class="sxs-lookup"><span data-stu-id="a1c71-112">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![Exemple d’application MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="a1c71-114">objectif de Hello est toodeliver cette application en continu dans un cluster de Mode de Docker Swarm, à l’aide de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a1c71-114">hello objective is toodeliver this application continuously in a Docker Swarm Mode cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="a1c71-115">la figure suivant de Hello détails ce pipeline de livraison continue :</span><span class="sxs-lookup"><span data-stu-id="a1c71-115">hello following figure details this continuous delivery pipeline:</span></span>

![Exemple d’application MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="a1c71-117">Voici une brève explication des étapes de hello :</span><span class="sxs-lookup"><span data-stu-id="a1c71-117">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="a1c71-118">Modifications du code sont validées toohello référentiel de code source (ici, GitHub)</span><span class="sxs-lookup"><span data-stu-id="a1c71-118">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="a1c71-119">GitHub déclenche une build dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a1c71-119">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="a1c71-120">Obtient la version la plus récente de sources de hello hello de Visual Studio Team Services et génère toutes les images hello qui composent l’application hello</span><span class="sxs-lookup"><span data-stu-id="a1c71-120">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="a1c71-121">Visual Studio Team Services transmet chaque registre Docker de tooa image créé à l’aide du service de Registre de conteneur Azure hello</span><span class="sxs-lookup"><span data-stu-id="a1c71-121">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="a1c71-122">Visual Studio Team Services déclenche une nouvelle mise en production.</span><span class="sxs-lookup"><span data-stu-id="a1c71-122">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="a1c71-123">version de Hello exécute des commandes à l’aide de SSH sur le nœud principal du cluster service conteneur Azure hello</span><span class="sxs-lookup"><span data-stu-id="a1c71-123">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="a1c71-124">Docker Swarm Mode sur le cluster de hello extrait la version la plus récente des images de hello hello</span><span class="sxs-lookup"><span data-stu-id="a1c71-124">Docker Swarm Mode on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="a1c71-125">Hello nouvelle version d’application hello est déployée à l’aide de la pile de Docker</span><span class="sxs-lookup"><span data-stu-id="a1c71-125">hello new version of hello application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a1c71-126">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a1c71-126">Prerequisites</span></span>

<span data-ttu-id="a1c71-127">Avant de commencer ce didacticiel, vous devez hello toocomplete tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="a1c71-127">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="a1c71-128">Création d’un cluster du Mode Swarm dans Azure Container Service avec le moteur ACS</span><span class="sxs-lookup"><span data-stu-id="a1c71-128">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="a1c71-129">Se connecter à un cluster d’essaim hello dans le conteneur de Service Azure</span><span class="sxs-lookup"><span data-stu-id="a1c71-129">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="a1c71-130">Utilisation d’un Registre de conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="a1c71-130">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="a1c71-131">Création d’un compte et d’un projet d’équipe Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a1c71-131">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="a1c71-132">Effectuer un branchement tooyour de référentiel GitHub hello compte GitHub</span><span class="sxs-lookup"><span data-stu-id="a1c71-132">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="a1c71-133">orchestrator de Docker Swarm Hello dans le Service de conteneur Azure utilise autonome hérité essaim.</span><span class="sxs-lookup"><span data-stu-id="a1c71-133">hello Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="a1c71-134">Actuellement, hello intégré [essaim mode](https://docs.docker.com/engine/swarm/) (dans Docker 1.12 et versions ultérieures) n’est pas un orchestrateur de prise en charge dans le Service de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="a1c71-134">Currently, hello integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="a1c71-135">Pour cette raison, nous utilisons [ACS moteur](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), une communauté [modèle de démarrage rapide](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), ou une solution de Docker Bonjour [Azure Marketplace](https://azuremarketplace.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a1c71-135">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in hello [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="a1c71-136">Étape 1 : configuration de votre compte Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a1c71-136">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="a1c71-137">Dans cette section, vous allez configurer votre compte Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a1c71-137">In this section, you configure your Visual Studio Team Services account.</span></span> <span data-ttu-id="a1c71-138">points de terminaison des Services de VSTS de tooconfigure, dans votre projet Visual Studio Team Services, cliquez sur hello **paramètres** icône dans la barre d’outils hello, puis sélectionnez **Services**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-138">tooconfigure VSTS Services Endpoints, in your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

![Ouvrez Point de terminaison de services](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a><span data-ttu-id="a1c71-140">Connectez Visual Studio Team Services avec votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="a1c71-140">Connect Visual Studio Team Services and Azure account</span></span>

<span data-ttu-id="a1c71-141">Configurez une connexion entre votre projet VSTS et votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="a1c71-141">Set up a connection between your VSTS project and your Azure account.</span></span>

1. <span data-ttu-id="a1c71-142">Sur hello gauche, cliquez sur **nouveau point de terminaison de Service** > **Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-142">On hello left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="a1c71-143">toowork VSTS tooauthorize avec votre compte Azure, sélectionnez votre **abonnement** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-143">tooauthorize VSTS toowork with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Visual Studio Team Services - Autoriser Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="a1c71-145">Connexion entre Visual Studio Team Services et GitHub</span><span class="sxs-lookup"><span data-stu-id="a1c71-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="a1c71-146">Configurez une connexion entre votre projet VSTS et votre compte GitHub.</span><span class="sxs-lookup"><span data-stu-id="a1c71-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="a1c71-147">Sur hello gauche, cliquez sur **nouveau point de terminaison de Service** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-147">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="a1c71-148">toowork VSTS tooauthorize avec votre compte GitHub, cliquez sur **Authorize** et suivez la procédure hello dans la fenêtre hello qui s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="a1c71-148">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services - Autoriser GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a><span data-ttu-id="a1c71-150">Connecter le cluster de Service de conteneur Azure tooyour VSTS</span><span class="sxs-lookup"><span data-stu-id="a1c71-150">Connect VSTS tooyour Azure Container Service cluster</span></span>

<span data-ttu-id="a1c71-151">dernières étapes de Hello avant d’entrer dans le pipeline de l’élément de configuration/CD hello sont tooconfigure connexions externes tooyour Docker Swarm un cluster dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a1c71-151">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="a1c71-152">Pour le cluster de Docker Swarm hello, ajoutez un point de terminaison de type **SSH**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-152">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="a1c71-153">Puis entrez les informations de connexion SSH hello de votre cluster essaim (nœud principal).</span><span class="sxs-lookup"><span data-stu-id="a1c71-153">Then enter hello SSH connection information of your Swarm cluster (master node).</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="a1c71-155">La configuration hello est effectuée maintenant.</span><span class="sxs-lookup"><span data-stu-id="a1c71-155">All hello configuration is done now.</span></span> <span data-ttu-id="a1c71-156">Dans les étapes suivantes hello, créer pipeline de l’élément de configuration/CD hello qui génère et déploie hello application toohello Docker Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="a1c71-156">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="a1c71-157">Étape 2 : Créer la définition de build hello</span><span class="sxs-lookup"><span data-stu-id="a1c71-157">Step 2: Create hello build definition</span></span>

<span data-ttu-id="a1c71-158">Dans cette étape, vous configurez une définition de build pour votre projet VSTS et définissez le flux de travail de build hello pour vos images de conteneur</span><span class="sxs-lookup"><span data-stu-id="a1c71-158">In this step, you set up a build definition for your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="a1c71-159">Configuration de la définition initiale</span><span class="sxs-lookup"><span data-stu-id="a1c71-159">Initial definition setup</span></span>

1. <span data-ttu-id="a1c71-160">toocreate une définition de build, connecter tooyour Visual Studio Team Services projet, puis cliquez sur **générer & version**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-160">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> <span data-ttu-id="a1c71-161">Bonjour **des définitions de Build** , cliquez sur **+ nouveau**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-161">In hello **Build definitions** section, click **+ New**.</span></span> 

    ![Visual Studio Team Services - Nouvelle définition de build](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="a1c71-163">Sélectionnez hello **processus vide**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-163">Select hello **Empty process**.</span></span>

    ![Visual Studio Team Services - Nouvelle définition de build vide](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="a1c71-165">Ensuite, cliquez sur hello **Variables** onglet et créez deux nouvelles variables : **RegistryURL** et **AgentURL**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-165">Then, click hello **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="a1c71-166">Collez les valeurs hello de votre Registre et le Cluster Agents DNS.</span><span class="sxs-lookup"><span data-stu-id="a1c71-166">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - Configuration des variables de la build](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="a1c71-168">Sur hello **définitions de Build** page, ouvrez hello **déclencheurs** onglet et configurer l’intégration continue hello build toouse avec branchement hello du projet MyShop hello que vous avez créé dans les conditions préalables de hello.</span><span class="sxs-lookup"><span data-stu-id="a1c71-168">On hello **Build Definitions** page, open hello **Triggers** tab and configure hello build toouse continuous integration with hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="a1c71-169">Sélectionnez ensuite **Modifications de lot**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-169">Then, select **Batch changes**.</span></span> <span data-ttu-id="a1c71-170">Assurez-vous que vous sélectionnez *docker-linux* comme hello **branche spécification**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-170">Make sure that you select *docker-linux* as hello **Branch specification**.</span></span>

    ![Visual Studio Team Services - Configuration du référentiel de la build](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="a1c71-172">Enfin, cliquez sur hello **Options** onglet et configurer trop de file d’attente de l’agent de valeur par défaut hello**aperçu de Linux hébergés**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-172">Finally, click hello **Options** tab and configure hello Default agent queue too**Hosted Linux Preview**.</span></span>

    ![Visual Studio Team Services - Configuration de l’agent hébergé](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="a1c71-174">Définir le flux de travail de build hello</span><span class="sxs-lookup"><span data-stu-id="a1c71-174">Define hello build workflow</span></span>
<span data-ttu-id="a1c71-175">les étapes suivantes Hello définissent des flux de travail de build hello.</span><span class="sxs-lookup"><span data-stu-id="a1c71-175">hello next steps define hello build workflow.</span></span> <span data-ttu-id="a1c71-176">Tout d’abord, vous devez source hello tooconfigure code de hello.</span><span class="sxs-lookup"><span data-stu-id="a1c71-176">First, you need tooconfigure hello source of hello code.</span></span> <span data-ttu-id="a1c71-177">toodo il, sélectionnez **GitHub** et votre **référentiel** et **branche** (docker linux).</span><span class="sxs-lookup"><span data-stu-id="a1c71-177">toodo it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Visual Studio Team Services - Configurer la source du code](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="a1c71-179">Il existe cinq toobuild d’images de conteneur pour hello *MyShop* application.</span><span class="sxs-lookup"><span data-stu-id="a1c71-179">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="a1c71-180">Chaque image est générée à l’aide de hello que dockerfile situé dans des dossiers du projet hello :</span><span class="sxs-lookup"><span data-stu-id="a1c71-180">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="a1c71-181">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="a1c71-181">ProductsApi</span></span>
* <span data-ttu-id="a1c71-182">Proxy</span><span class="sxs-lookup"><span data-stu-id="a1c71-182">Proxy</span></span>
* <span data-ttu-id="a1c71-183">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="a1c71-183">RatingsApi</span></span>
* <span data-ttu-id="a1c71-184">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="a1c71-184">RecommandationsApi</span></span>
* <span data-ttu-id="a1c71-185">ShopFront</span><span class="sxs-lookup"><span data-stu-id="a1c71-185">ShopFront</span></span>

<span data-ttu-id="a1c71-186">Vous avez besoin de deux étapes de Docker pour chaque image, une image de hello toobuild et une image de hello toopush dans le Registre de conteneur Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a1c71-186">You need two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="a1c71-187">tooadd une étape dans le flux de travail hello, cliquez sur **+ ajouter une étape build** et sélectionnez **Docker**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-187">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - Ajout d’étapes de build](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="a1c71-189">Pour chaque image, configurez une seule étape qui utilise hello `docker build` commande.</span><span class="sxs-lookup"><span data-stu-id="a1c71-189">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services - Build Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="a1c71-191">Opération de génération pour hello, sélectionnez votre Registre de conteneur Azure, hello **générer une image** action et hello Dockerfile qui définit chaque image.</span><span class="sxs-lookup"><span data-stu-id="a1c71-191">For hello build operation, select your Azure Container Registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="a1c71-192">Ensemble hello **du répertoire de travail** dans le répertoire racine du fichier Dockerfile hello, définir hello **nom de l’Image**, puis sélectionnez **inclure une balise Latest**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-192">Set hello **Working Directory** as hello Dockerfile root directory, define hello **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="a1c71-193">Hello, nom de l’Image a toobe dans ce format : ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span><span class="sxs-lookup"><span data-stu-id="a1c71-193">hello Image Name has toobe in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="a1c71-194">Remplacez **[nom]** avec le nom de l’image hello :</span><span class="sxs-lookup"><span data-stu-id="a1c71-194">Replace **[NAME]** with hello image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="a1c71-195">Pour chaque image, configurer une deuxième étape qui utilise hello `docker push` commande.</span><span class="sxs-lookup"><span data-stu-id="a1c71-195">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services - Envoi du fichier Docker](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="a1c71-197">Pour une opération de diffusion hello, sélectionnez votre Registre conteneur Azure, hello **de pousser une image** action, entrez hello **nom de l’Image** qui est intégré dans l’étape précédente de hello et sélectionnez **inclure une balise Latest** .</span><span class="sxs-lookup"><span data-stu-id="a1c71-197">For hello push operation, select your Azure container registry, hello **Push an image** action, enter hello **Image Name** that is built in hello previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="a1c71-198">Après avoir configuré la génération de hello et distribuer les étapes pour chacune des images de cinq hello, ajouter que trois étapes plus Bonjour générer des flux de travail.</span><span class="sxs-lookup"><span data-stu-id="a1c71-198">After you configure hello build and push steps for each of hello five images, add three more steps in hello build workflow.</span></span>

   ![Visual Studio Team Services - Ajout d’une tâche de ligne de commande](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="a1c71-200">Une tâche de ligne de commande qui utilise un Bonjour tooreplace du script bash *RegistryURL* occurrence dans le fichier de docker-compose.yml hello avec la variable de RegistryURL hello.</span><span class="sxs-lookup"><span data-stu-id="a1c71-200">A command-line task that uses a bash script tooreplace hello *RegistryURL* occurrence in hello docker-compose.yml file with hello RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio Team Services - Mise à jour du fichier Compose avec l’URL du Registre](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="a1c71-202">Une tâche de ligne de commande qui utilise un Bonjour tooreplace du script bash *AgentURL* occurrence dans le fichier de docker-compose.yml hello avec la variable de AgentURL hello.</span><span class="sxs-lookup"><span data-stu-id="a1c71-202">A command-line task that uses a bash script tooreplace hello *AgentURL* occurrence in hello docker-compose.yml file with hello AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="a1c71-203">Une tâche qui supprime hello mis à jour le fichier de message en tant qu’un artefact de build il peut être utilisé dans la version de hello.</span><span class="sxs-lookup"><span data-stu-id="a1c71-203">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="a1c71-204">Hello suivant l’écran pour plus d’informations, consultez.</span><span class="sxs-lookup"><span data-stu-id="a1c71-204">See hello following screen for details.</span></span>

         ![Visual Studio Team Services - Publication de l’artefact](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - Publication du fichier Compose](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="a1c71-207">Cliquez sur **enregistrer et de file d’attente** tootest votre définition de build.</span><span class="sxs-lookup"><span data-stu-id="a1c71-207">Click **Save & queue** tootest your build definition.</span></span>

   ![Visual Studio Team Services - Enregistrer et mettre en file d’attente](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio Team Services - Nouvelle file d’attente](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="a1c71-210">Si hello **générer** est correct, vous avez toosee cet écran :</span><span class="sxs-lookup"><span data-stu-id="a1c71-210">If hello **Build** is correct, you have toosee this screen:</span></span>

  ![Visual Studio Team Services - Build réussie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="a1c71-212">Étape 3 : Créer la définition de la version hello</span><span class="sxs-lookup"><span data-stu-id="a1c71-212">Step 3: Create hello release definition</span></span>

<span data-ttu-id="a1c71-213">Visual Studio Team Services vous permet de trop[gérer les versions dans des environnements](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="a1c71-213">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="a1c71-214">Vous pouvez activer toomake déploiement continu sûr que votre application est déployée sur vos environnements différents (par exemple, le développement, test, préproduction et production) de façon fluide.</span><span class="sxs-lookup"><span data-stu-id="a1c71-214">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="a1c71-215">Vous pouvez créer un environnement qui représente votre cluster Docker Swarm Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="a1c71-215">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Visual Studio Team Services - version tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="a1c71-217">Configuration de la mise en production initiale</span><span class="sxs-lookup"><span data-stu-id="a1c71-217">Initial release setup</span></span>

1. <span data-ttu-id="a1c71-218">toocreate une définition de la mise en production, cliquez sur **versions** > **+ Release**</span><span class="sxs-lookup"><span data-stu-id="a1c71-218">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="a1c71-219">source d’artefact tooconfigure hello, cliquez sur **artefacts** > **lier une source d’artefact**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-219">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="a1c71-220">Ici, lier cette nouvelle définition toohello version Release que vous avez définie à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="a1c71-220">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="a1c71-221">Après cela, le fichier de docker-compose.yml de hello est disponible dans le processus de mise en production hello.</span><span class="sxs-lookup"><span data-stu-id="a1c71-221">After that, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services - Artefacts de mise en production](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="a1c71-223">déclencheur hello tooconfigure, cliquez sur **déclencheurs** et sélectionnez **déploiement continu**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-223">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="a1c71-224">Définir un déclencheur hello sur hello même source d’artefact.</span><span class="sxs-lookup"><span data-stu-id="a1c71-224">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="a1c71-225">Ce paramètre s’assure qu’une nouvelle version démarre lorsque hello build s’effectue correctement.</span><span class="sxs-lookup"><span data-stu-id="a1c71-225">This setting ensures that a new release starts when hello build completes successfully.</span></span>

    ![Visual Studio Team Services - Déclencheurs de mise en production](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="a1c71-227">Cliquez sur les variables de version tooconfigure hello, **Variables** et sélectionnez **+ Variable** toocreate trois nouvelles variables avec des informations du Registre de hello hello : **docker.username**, **docker.password**, et **docker.registry**.</span><span class="sxs-lookup"><span data-stu-id="a1c71-227">tooconfigure hello release variables, click **Variables** and select **+Variable** toocreate three new variables with hello info of hello registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="a1c71-228">Collez les valeurs hello de votre Registre et le Cluster Agents DNS.</span><span class="sxs-lookup"><span data-stu-id="a1c71-228">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio Team Services - Configuration du référentiel de la build](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="a1c71-230">Comme indiqué à l’écran précédent de hello, cliquez sur hello **verrou** case à cocher dans docker.password.</span><span class="sxs-lookup"><span data-stu-id="a1c71-230">As shown on hello previous screen, click hello **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="a1c71-231">Ce paramètre est un mot de passe hello toorestrict important.</span><span class="sxs-lookup"><span data-stu-id="a1c71-231">This setting is important toorestrict hello password.</span></span>
    >

### <a name="define-hello-release-workflow"></a><span data-ttu-id="a1c71-232">Définir le flux de travail de mise en production hello</span><span class="sxs-lookup"><span data-stu-id="a1c71-232">Define hello release workflow</span></span>

<span data-ttu-id="a1c71-233">flux de travail de mise en production Hello est composé de deux tâches que vous ajoutez.</span><span class="sxs-lookup"><span data-stu-id="a1c71-233">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="a1c71-234">Configurer un Bonjour de copie toosecurely tâche composer fichier tooa *déployer* dossier hello Docker Swarm nœud maître, à l’aide de la connexion SSH hello configurées précédemment.</span><span class="sxs-lookup"><span data-stu-id="a1c71-234">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="a1c71-235">Hello suivant l’écran pour plus d’informations, consultez.</span><span class="sxs-lookup"><span data-stu-id="a1c71-235">See hello following screen for details.</span></span>
    
    <span data-ttu-id="a1c71-236">Dossier source : ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="a1c71-236">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Visual Studio Team Services - SCP mise en production](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="a1c71-238">Configurer une deuxième tooexecute de tâche un toorun de commande d’interpréteur de commandes `docker` et `docker stack deploy` commandes sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="a1c71-238">Configure a second task tooexecute a bash command toorun `docker` and `docker stack deploy` commands on hello master node.</span></span> <span data-ttu-id="a1c71-239">Hello suivant l’écran pour plus d’informations, consultez.</span><span class="sxs-lookup"><span data-stu-id="a1c71-239">See hello following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio Team Services - Bash mise en production](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="a1c71-241">commande Hello exécutée sur le contrôleur de hello utilise hello Docker CLI et hello de toodo CLI de Docker Compose hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="a1c71-241">hello command executed on hello master uses hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="a1c71-242">Ouvrez une session dans le Registre de conteneur Azure toohello (il utilise trois variables de génération qui sont définis dans hello **Variables** onglet)</span><span class="sxs-lookup"><span data-stu-id="a1c71-242">Log in toohello Azure container registry (it uses three build variables that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="a1c71-243">Définir hello **DOCKER_HOST** toowork variable avec le point de terminaison hello essaim ( : 2375)</span><span class="sxs-lookup"><span data-stu-id="a1c71-243">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="a1c71-244">Accédez toohello *déployer* dossier qui a été créé par hello précédant la tâche de copie sécurisée et qui contient le fichier de docker-compose.yml hello</span><span class="sxs-lookup"><span data-stu-id="a1c71-244">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="a1c71-245">Exécutez `docker stack deploy` commandes qui extrait les nouvelles images de hello et créer des conteneurs de hello.</span><span class="sxs-lookup"><span data-stu-id="a1c71-245">Execute `docker stack deploy` commands that pull hello new images and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="a1c71-246">Comme indiqué à l’écran précédent de hello, laissez hello **échouer dans STDERR** case à cocher est désactivée.</span><span class="sxs-lookup"><span data-stu-id="a1c71-246">As shown on hello previous screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="a1c71-247">Ce paramètre permet de processus de mise en production toocomplete hello échéance trop`docker-compose` imprime plusieurs messages de diagnostic, tels que les conteneurs sont en cours de suppression sur la sortie d’erreur standard hello ou d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="a1c71-247">This setting allows us toocomplete hello release process due too`docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="a1c71-248">Si vous activez la case à cocher hello, Visual Studio Team Services signale que les erreurs se sont produites au cours de la version de hello, même si tout se passe bien.</span><span class="sxs-lookup"><span data-stu-id="a1c71-248">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="a1c71-249">Enregistrez cette nouvelle définition de mise en production.</span><span class="sxs-lookup"><span data-stu-id="a1c71-249">Save this new release definition.</span></span>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="a1c71-250">Étape 4 : Tester le pipeline de l’élément de configuration/CD hello</span><span class="sxs-lookup"><span data-stu-id="a1c71-250">Step 4: Test hello CI/CD pipeline</span></span>

<span data-ttu-id="a1c71-251">Maintenant que vous avez terminé avec la configuration de hello, il est temps tootest de ce nouveau pipeline de l’élément de configuration/CD.</span><span class="sxs-lookup"><span data-stu-id="a1c71-251">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="a1c71-252">tootest moyen plus simple de Hello, il est tooupdate Bonjour source code puis de valider Bonjour change dans votre référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="a1c71-252">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="a1c71-253">Quelques secondes après le push de code de hello, vous verrez une nouvelle build en cours d’exécution dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a1c71-253">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="a1c71-254">Une fois terminé, une nouvelle version est déclenchée et déployé hello nouvelle version d’application hello sur le cluster du Service de conteneur Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a1c71-254">Once completed successfully, a new release is triggered and deployed hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1c71-255">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a1c71-255">Next steps</span></span>

* <span data-ttu-id="a1c71-256">Pour plus d’informations sur l’élément de configuration/CD avec Visual Studio Team Services, consultez hello [VSTS générer une vue d’ensemble](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="a1c71-256">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="a1c71-257">Pour plus d’informations sur le moteur d’ACS, consultez hello [référentiel GitHub de moteur ACS](https://github.com/Azure/acs-engine).</span><span class="sxs-lookup"><span data-stu-id="a1c71-257">For more information about ACS Engine, see hello [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="a1c71-258">Pour plus d’informations sur le mode de Docker Swarm, consultez hello [Docker Swarm une vue d’ensemble du mode](https://docs.docker.com/engine/swarm/).</span><span class="sxs-lookup"><span data-stu-id="a1c71-258">For more information about Docker Swarm mode, see hello [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
