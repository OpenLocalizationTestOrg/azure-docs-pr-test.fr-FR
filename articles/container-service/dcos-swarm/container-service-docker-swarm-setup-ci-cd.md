---
title: aaaCI/CD avec le Service de conteneur Azure et essaim | Documents Microsoft
description: Utiliser le Service de conteneur Azure avec Docker Swarm un Registre de conteneur Azure et Visual Studio Team Services toodeliver en permanence une application de .NET Core multi conteneur
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Swarm, Azure, Visual Studio Team Services, DevOps
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a><span data-ttu-id="7489a-104">/ CD complète de l’élément de configuration de pipeline toodeploy une application conteneur multi Azure Service de conteneur avec Docker Swarm à l’aide de Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="7489a-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span></span>

<span data-ttu-id="7489a-105">Un des hello plus grands défis lors de développement d’applications modernes pour le cloud de hello toodeliver en mesure de ces applications en continu.</span><span class="sxs-lookup"><span data-stu-id="7489a-105">One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="7489a-106">Dans cet article, vous découvrez comment tooimplement une intégration complète continue et le pipeline de déploiement (élément de configuration/CD) à l’aide du Service de conteneur Azure avec Docker Swarm, Registre de conteneur Azure et Visual Studio Team Services de génération et gestion des versions.</span><span class="sxs-lookup"><span data-stu-id="7489a-106">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span></span>

<span data-ttu-id="7489a-107">Cet article est basé sur une application simple, disponible sur [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), développée avec ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="7489a-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="7489a-108">application Hello est composée de quatre services différents : trois web API et un site web frontal :</span><span class="sxs-lookup"><span data-stu-id="7489a-108">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![Exemple d’application MyShop](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="7489a-110">objectif de Hello est toodeliver cette application en continu dans un cluster de Docker Swarm, à l’aide de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="7489a-110">hello objective is toodeliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="7489a-111">la figure suivant de Hello détails ce pipeline de livraison continue :</span><span class="sxs-lookup"><span data-stu-id="7489a-111">hello following figure details this continuous delivery pipeline:</span></span>

![Exemple d’application MyShop](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="7489a-113">Voici une brève explication des étapes de hello :</span><span class="sxs-lookup"><span data-stu-id="7489a-113">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="7489a-114">Modifications du code sont validées toohello référentiel de code source (ici, GitHub)</span><span class="sxs-lookup"><span data-stu-id="7489a-114">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="7489a-115">GitHub déclenche une build dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="7489a-115">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="7489a-116">Obtient la version la plus récente de sources de hello hello de Visual Studio Team Services et génère toutes les images hello qui composent l’application hello</span><span class="sxs-lookup"><span data-stu-id="7489a-116">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="7489a-117">Visual Studio Team Services transmet chaque registre Docker de tooa image créé à l’aide du service de Registre de conteneur Azure hello</span><span class="sxs-lookup"><span data-stu-id="7489a-117">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="7489a-118">Visual Studio Team Services déclenche une nouvelle mise en production.</span><span class="sxs-lookup"><span data-stu-id="7489a-118">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="7489a-119">version de Hello exécute des commandes à l’aide de SSH sur le nœud principal du cluster service conteneur Azure hello</span><span class="sxs-lookup"><span data-stu-id="7489a-119">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="7489a-120">Essaim docker sur hello cluster extrait hello version la plus récente des images de hello</span><span class="sxs-lookup"><span data-stu-id="7489a-120">Docker Swarm on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="7489a-121">Hello nouvelle version d’application hello est déployée à l’aide de Docker Compose</span><span class="sxs-lookup"><span data-stu-id="7489a-121">hello new version of hello application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7489a-122">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7489a-122">Prerequisites</span></span>

<span data-ttu-id="7489a-123">Avant de commencer ce didacticiel, vous devez hello toocomplete tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="7489a-123">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="7489a-124">Création d’un cluster Swarm dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="7489a-124">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="7489a-125">Se connecter à un cluster d’essaim hello dans le conteneur de Service Azure</span><span class="sxs-lookup"><span data-stu-id="7489a-125">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="7489a-126">Utilisation d’un Registre de conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="7489a-126">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="7489a-127">Création d’un compte et d’un projet d’équipe Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="7489a-127">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="7489a-128">Effectuer un branchement tooyour de référentiel GitHub hello compte GitHub</span><span class="sxs-lookup"><span data-stu-id="7489a-128">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="7489a-129">Vous devez également posséder un ordinateur Ubuntu (14.04 ou 16.04) avec Docker installé.</span><span class="sxs-lookup"><span data-stu-id="7489a-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="7489a-130">Cet ordinateur est utilisé par Visual Studio Team Services pendant hello générer et lancer le processus.</span><span class="sxs-lookup"><span data-stu-id="7489a-130">This machine is used by Visual Studio Team Services during hello build and release processes.</span></span> <span data-ttu-id="7489a-131">Une façon toocreate cet ordinateur est l’image de hello toouse disponible dans hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span><span class="sxs-lookup"><span data-stu-id="7489a-131">One way toocreate this machine is toouse hello image available in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="7489a-132">Étape 1 : configuration de votre compte Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="7489a-132">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="7489a-133">Dans cette section, vous allez configurer votre compte Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="7489a-133">In this section, you configure your Visual Studio Team Services account.</span></span>

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a><span data-ttu-id="7489a-134">Configuration d’un agent de build Linux Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="7489a-134">Configure a Visual Studio Team Services Linux build agent</span></span>

<span data-ttu-id="7489a-135">toocreate Docker images et push que générer de ces images dans un Registre de conteneur Azure à partir d’un Visual Studio Team Services, vous devez tooregister un agent Linux.</span><span class="sxs-lookup"><span data-stu-id="7489a-135">toocreate Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need tooregister a Linux agent.</span></span> <span data-ttu-id="7489a-136">Vous avez le choix entre les options d’installation suivantes :</span><span class="sxs-lookup"><span data-stu-id="7489a-136">You have these installation options:</span></span>

* [<span data-ttu-id="7489a-137">Déploiement d’un agent sur Linux</span><span class="sxs-lookup"><span data-stu-id="7489a-137">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="7489a-138">Utilisez l’agent de Docker toorun hello VSTS</span><span class="sxs-lookup"><span data-stu-id="7489a-138">Use Docker toorun hello VSTS agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a><span data-ttu-id="7489a-139">Installation de l’extension de Docker intégration VSTS hello</span><span class="sxs-lookup"><span data-stu-id="7489a-139">Install hello Docker Integration VSTS extension</span></span>

<span data-ttu-id="7489a-140">Microsoft fournit une extension VSTS toowork avec Docker dans la build et libérer des processus.</span><span class="sxs-lookup"><span data-stu-id="7489a-140">Microsoft provides a VSTS extension toowork with Docker in build and release processes.</span></span> <span data-ttu-id="7489a-141">Cette extension est disponible dans hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span><span class="sxs-lookup"><span data-stu-id="7489a-141">This extension is available in hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="7489a-142">Cliquez sur **installer** tooadd ce compte VSTS tooyour extension :</span><span class="sxs-lookup"><span data-stu-id="7489a-142">Click **Install** tooadd this extension tooyour VSTS account:</span></span>

![Installer hello intégration de Docker](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="7489a-144">Vous êtes invité compte VSTS tooyour tooconnect à l’aide de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7489a-144">You are asked tooconnect tooyour VSTS account using your credentials.</span></span> 

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="7489a-145">Connexion entre Visual Studio Team Services et GitHub</span><span class="sxs-lookup"><span data-stu-id="7489a-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="7489a-146">Configurez une connexion entre votre projet VSTS et votre compte GitHub.</span><span class="sxs-lookup"><span data-stu-id="7489a-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="7489a-147">Dans votre projet Visual Studio Team Services, cliquez sur hello **paramètres** icône dans la barre d’outils hello, puis sélectionnez **Services**.</span><span class="sxs-lookup"><span data-stu-id="7489a-147">In your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

    ![Visual Studio Team Services - Connexion externe](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. <span data-ttu-id="7489a-149">Sur hello gauche, cliquez sur **nouveau point de terminaison de Service** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="7489a-149">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Visual Studio Team Services - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. <span data-ttu-id="7489a-151">toowork VSTS tooauthorize avec votre compte GitHub, cliquez sur **Authorize** et suivez la procédure hello dans la fenêtre hello qui s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="7489a-151">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio Team Services - Autoriser GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="7489a-153">Se connecter du Registre de conteneur Azure VSTS tooyour et cluster du Service de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="7489a-153">Connect VSTS tooyour Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="7489a-154">dernières étapes de Hello avant d’entrer dans le pipeline de l’élément de configuration/CD hello sont Registre de conteneur tooyour tooconfigure connexions externes et de votre cluster Docker Swarm dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7489a-154">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="7489a-155">Bonjour **Services** paramètres de votre projet Visual Studio Team Services, ajouter un point de terminaison de type **Docker Registre**.</span><span class="sxs-lookup"><span data-stu-id="7489a-155">In hello **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span></span> 

2. <span data-ttu-id="7489a-156">Dans le menu contextuel hello qui s’ouvre, entrez l’URL de la hello et les informations d’identification hello du Registre de votre conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="7489a-156">In hello popup that opens, enter hello URL and hello credentials of your Azure container registry.</span></span>

    ![Visual Studio Team Services - Registre Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. <span data-ttu-id="7489a-158">Pour le cluster de Docker Swarm hello, ajoutez un point de terminaison de type **SSH**.</span><span class="sxs-lookup"><span data-stu-id="7489a-158">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="7489a-159">Puis entrez les informations de connexion SSH hello de votre cluster essaim.</span><span class="sxs-lookup"><span data-stu-id="7489a-159">Then enter hello SSH connection information of your Swarm cluster.</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="7489a-161">La configuration hello est effectuée maintenant.</span><span class="sxs-lookup"><span data-stu-id="7489a-161">All hello configuration is done now.</span></span> <span data-ttu-id="7489a-162">Dans les étapes suivantes hello, créer pipeline de l’élément de configuration/CD hello qui génère et déploie hello application toohello Docker Swarm cluster.</span><span class="sxs-lookup"><span data-stu-id="7489a-162">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="7489a-163">Étape 2 : Créer la définition de build hello</span><span class="sxs-lookup"><span data-stu-id="7489a-163">Step 2: Create hello build definition</span></span>

<span data-ttu-id="7489a-164">Dans cette étape, vous configurer un definitionfor de génération de votre projet VSTS et définissez le flux de travail de build hello pour vos images de conteneur</span><span class="sxs-lookup"><span data-stu-id="7489a-164">In this step, you set up a build definitionfor your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="7489a-165">Configuration de la définition initiale</span><span class="sxs-lookup"><span data-stu-id="7489a-165">Initial definition setup</span></span>

1. <span data-ttu-id="7489a-166">toocreate une définition de build, connecter tooyour Visual Studio Team Services projet, puis cliquez sur **générer & version**.</span><span class="sxs-lookup"><span data-stu-id="7489a-166">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> 

2. <span data-ttu-id="7489a-167">Bonjour **des définitions de Build** , cliquez sur **+ nouveau**.</span><span class="sxs-lookup"><span data-stu-id="7489a-167">In hello **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="7489a-168">Sélectionnez hello **vide** modèle.</span><span class="sxs-lookup"><span data-stu-id="7489a-168">Select hello **Empty** template.</span></span>

    ![Visual Studio Team Services - Nouvelle définition de build](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. <span data-ttu-id="7489a-170">Configurer la nouvelle version de hello avec une source de référentiel GitHub, vérification **intégration continue**et la file d’attente de l’agent hello sélectionnez où vous avez inscrit votre agent Linux.</span><span class="sxs-lookup"><span data-stu-id="7489a-170">Configure hello new build with a GitHub repository source, check **Continuous integration**, and select hello agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="7489a-171">Cliquez sur **créer** toocreate hello la définition de build.</span><span class="sxs-lookup"><span data-stu-id="7489a-171">Click **Create** toocreate hello build definition.</span></span>

    ![Visual Studio Team Services - Création de la définition de build](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. <span data-ttu-id="7489a-173">Sur hello **définitions de Build** page, ouvrez d’abord hello **référentiel** onglet et configurer le branchement de hello toouse hello build de projet MyShop hello que vous avez créé dans les conditions préalables de hello.</span><span class="sxs-lookup"><span data-stu-id="7489a-173">On hello **Build Definitions** page, first open hello **Repository** tab and configure hello build toouse hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="7489a-174">Assurez-vous que vous sélectionnez *acs-documents* comme hello **branche par défaut**.</span><span class="sxs-lookup"><span data-stu-id="7489a-174">Make sure that you select *acs-docs* as hello **Default branch**.</span></span>

    ![Visual Studio Team Services - Configuration du référentiel de la build](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. <span data-ttu-id="7489a-176">Sur hello **déclencheurs** , onglet de la configurer hello build toobe est déclenchée après chaque validation.</span><span class="sxs-lookup"><span data-stu-id="7489a-176">On hello **Triggers** tab, configure hello build toobe triggered after each commit.</span></span> <span data-ttu-id="7489a-177">Sélectionnez **Intégration continue** et **Modifications par lots**.</span><span class="sxs-lookup"><span data-stu-id="7489a-177">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Visual Studio Team Services - Configuration du déclencheur de la build](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="7489a-179">Définir le flux de travail de build hello</span><span class="sxs-lookup"><span data-stu-id="7489a-179">Define hello build workflow</span></span>
<span data-ttu-id="7489a-180">les étapes suivantes Hello définissent des flux de travail de build hello.</span><span class="sxs-lookup"><span data-stu-id="7489a-180">hello next steps define hello build workflow.</span></span> <span data-ttu-id="7489a-181">Il existe cinq toobuild d’images de conteneur pour hello *MyShop* application.</span><span class="sxs-lookup"><span data-stu-id="7489a-181">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="7489a-182">Chaque image est générée à l’aide de hello que dockerfile situé dans des dossiers du projet hello :</span><span class="sxs-lookup"><span data-stu-id="7489a-182">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="7489a-183">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="7489a-183">ProductsApi</span></span>
* <span data-ttu-id="7489a-184">Proxy</span><span class="sxs-lookup"><span data-stu-id="7489a-184">Proxy</span></span>
* <span data-ttu-id="7489a-185">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="7489a-185">RatingsApi</span></span>
* <span data-ttu-id="7489a-186">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="7489a-186">RecommandationsApi</span></span>
* <span data-ttu-id="7489a-187">ShopFront</span><span class="sxs-lookup"><span data-stu-id="7489a-187">ShopFront</span></span>

<span data-ttu-id="7489a-188">Vous devez tooadd deux étapes de Docker pour chaque image, une image de hello toobuild et une image de hello toopush dans le Registre de conteneur Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7489a-188">You need tooadd two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="7489a-189">tooadd une étape dans le flux de travail hello, cliquez sur **+ ajouter une étape build** et sélectionnez **Docker**.</span><span class="sxs-lookup"><span data-stu-id="7489a-189">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio Team Services - Ajout d’étapes de build](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. <span data-ttu-id="7489a-191">Pour chaque image, configurez une seule étape qui utilise hello `docker build` commande.</span><span class="sxs-lookup"><span data-stu-id="7489a-191">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio Team Services - Build Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="7489a-193">Opération de génération pour hello, sélectionnez votre Registre conteneur Azure, hello **générer une image** action et hello Dockerfile qui définit chaque image.</span><span class="sxs-lookup"><span data-stu-id="7489a-193">For hello build operation, select your Azure container registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="7489a-194">Ensemble hello **contexte de génération** comme hello Dockerfile répertoire racine et définir hello **nom de l’Image**.</span><span class="sxs-lookup"><span data-stu-id="7489a-194">Set hello **Build context** as hello Dockerfile root directory, and define hello **Image Name**.</span></span> 
    
    <span data-ttu-id="7489a-195">Comme indiqué dans le hello précédant l’écran, démarrez nom de l’image hello avec hello URI de votre Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="7489a-195">As shown on hello preceding screen, start hello image name with hello URI of your Azure container registry.</span></span> <span data-ttu-id="7489a-196">(Vous pouvez également utiliser une balise de hello tooparameterize variable génération d’image hello, comme l’identificateur de build hello dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="7489a-196">(You can also use a build variable tooparameterize hello tag of hello image, such as hello build identifier in this example.)</span></span>

3. <span data-ttu-id="7489a-197">Pour chaque image, configurer une deuxième étape qui utilise hello `docker push` commande.</span><span class="sxs-lookup"><span data-stu-id="7489a-197">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio Team Services - Envoi du fichier Docker](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="7489a-199">Pour une opération de diffusion hello, sélectionnez votre Registre conteneur Azure, hello **de pousser une image** action, puis entrez hello **nom de l’Image** qui est généré à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="7489a-199">For hello push operation, select your Azure container registry, hello **Push an image** action, and enter hello **Image Name** that is built in hello previous step.</span></span>

4. <span data-ttu-id="7489a-200">Après avoir configuré la génération de hello et distribuer les étapes pour chacune des images de cinq hello, ajoutez que deux étapes plus Bonjour générer des flux de travail.</span><span class="sxs-lookup"><span data-stu-id="7489a-200">After you configure hello build and push steps for each of hello five images, add two more steps in hello build workflow.</span></span>

    <span data-ttu-id="7489a-201">a.</span><span class="sxs-lookup"><span data-stu-id="7489a-201">a.</span></span> <span data-ttu-id="7489a-202">Une tâche de ligne de commande qui utilise un Bonjour tooreplace du script bash *BuildNumber* occurrence dans le fichier docker-compose.yml hello hello actuel générer ID. Hello suivant l’écran pour plus d’informations, consultez.</span><span class="sxs-lookup"><span data-stu-id="7489a-202">A command-line task that uses a bash script tooreplace hello *BuildNumber* occurrence in hello docker-compose.yml file with hello current build Id. See hello following screen for details.</span></span>

    ![Visual Studio Team Services - Mise à jour du fichier Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="7489a-204">b.</span><span class="sxs-lookup"><span data-stu-id="7489a-204">b.</span></span> <span data-ttu-id="7489a-205">Une tâche qui supprime hello mis à jour le fichier de message en tant qu’un artefact de build il peut être utilisé dans la version de hello.</span><span class="sxs-lookup"><span data-stu-id="7489a-205">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="7489a-206">Hello suivant l’écran pour plus d’informations, consultez.</span><span class="sxs-lookup"><span data-stu-id="7489a-206">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - Publication du fichier Compose](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. <span data-ttu-id="7489a-208">Cliquez sur **Enregistrer** et affectez un nom à votre définition de build.</span><span class="sxs-lookup"><span data-stu-id="7489a-208">Click **Save** and name your build definition.</span></span>

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="7489a-209">Étape 3 : Créer la définition de la version hello</span><span class="sxs-lookup"><span data-stu-id="7489a-209">Step 3: Create hello release definition</span></span>

<span data-ttu-id="7489a-210">Visual Studio Team Services vous permet de trop[gérer les versions dans des environnements](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="7489a-210">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="7489a-211">Vous pouvez activer toomake déploiement continu sûr que votre application est déployée sur vos environnements différents (par exemple, le développement, test, préproduction et production) de façon fluide.</span><span class="sxs-lookup"><span data-stu-id="7489a-211">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="7489a-212">Vous pouvez créer un nouvel environnement qui représente votre cluster Docker Swarm Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="7489a-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Visual Studio Team Services - version tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="7489a-214">Configuration de la mise en production initiale</span><span class="sxs-lookup"><span data-stu-id="7489a-214">Initial release setup</span></span>

1. <span data-ttu-id="7489a-215">toocreate une définition de la mise en production, cliquez sur **versions** > **+ Release**</span><span class="sxs-lookup"><span data-stu-id="7489a-215">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="7489a-216">source d’artefact tooconfigure hello, cliquez sur **artefacts** > **lier une source d’artefact**.</span><span class="sxs-lookup"><span data-stu-id="7489a-216">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="7489a-217">Ici, lier cette nouvelle définition toohello version Release que vous avez définie à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="7489a-217">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="7489a-218">Ce faisant, fichier de docker-compose.yml hello est disponible dans le processus de mise en production hello.</span><span class="sxs-lookup"><span data-stu-id="7489a-218">By doing this, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio Team Services - Artefacts de mise en production](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. <span data-ttu-id="7489a-220">déclencheur hello tooconfigure, cliquez sur **déclencheurs** et sélectionnez **déploiement continu**.</span><span class="sxs-lookup"><span data-stu-id="7489a-220">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="7489a-221">Définir un déclencheur hello sur hello même source d’artefact.</span><span class="sxs-lookup"><span data-stu-id="7489a-221">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="7489a-222">Ce paramètre s’assure qu’une nouvelle version démarre dès qu’hello build s’effectue correctement.</span><span class="sxs-lookup"><span data-stu-id="7489a-222">This setting ensures that a new release starts as soon as hello build completes successfully.</span></span>

    ![Visual Studio Team Services - Déclencheurs de mise en production](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a><span data-ttu-id="7489a-224">Définir le flux de travail de mise en production hello</span><span class="sxs-lookup"><span data-stu-id="7489a-224">Define hello release workflow</span></span>

<span data-ttu-id="7489a-225">flux de travail de mise en production Hello est composé de deux tâches que vous ajoutez.</span><span class="sxs-lookup"><span data-stu-id="7489a-225">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="7489a-226">Configurer un Bonjour de copie toosecurely tâche composer fichier tooa *déployer* dossier hello Docker Swarm nœud maître, à l’aide de la connexion SSH hello configurées précédemment.</span><span class="sxs-lookup"><span data-stu-id="7489a-226">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="7489a-227">Hello suivant l’écran pour plus d’informations, consultez.</span><span class="sxs-lookup"><span data-stu-id="7489a-227">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - SCP mise en production](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. <span data-ttu-id="7489a-229">Configurer une deuxième tooexecute de tâche un toorun de commande d’interpréteur de commandes `docker` et `docker-compose` commandes sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="7489a-229">Configure a second task tooexecute a bash command toorun `docker` and `docker-compose` commands on hello master node.</span></span> <span data-ttu-id="7489a-230">Hello suivant l’écran pour plus d’informations, consultez.</span><span class="sxs-lookup"><span data-stu-id="7489a-230">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - Bash mise en production](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="7489a-232">commande Hello exécutée sur Bonjour utilisez master Bonjour Docker CLI et hello de toodo CLI de Docker Compose hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="7489a-232">hello command executed on hello master use hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="7489a-233">Registre de conteneur Azure connexion toohello (il utilise trois variab'les de génération qui sont définis dans hello **Variables** onglet)</span><span class="sxs-lookup"><span data-stu-id="7489a-233">Login toohello Azure container registry (it uses three build variab\`les that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="7489a-234">Définir hello **DOCKER_HOST** toowork variable avec le point de terminaison hello essaim ( : 2375)</span><span class="sxs-lookup"><span data-stu-id="7489a-234">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="7489a-235">Accédez toohello *déployer* dossier qui a été créé par hello précédant la tâche de copie sécurisée et qui contient le fichier de docker-compose.yml hello</span><span class="sxs-lookup"><span data-stu-id="7489a-235">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="7489a-236">Exécutez `docker-compose` commandes qui extrait les nouvelles images de hello, arrêter les services de hello, supprimez les services hello et créer des conteneurs de hello.</span><span class="sxs-lookup"><span data-stu-id="7489a-236">Execute `docker-compose` commands that pull hello new images, stop hello services, remove hello services, and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="7489a-237">Comme indiqué dans le hello précédant l’écran, laissez hello **échouer dans STDERR** case à cocher est désactivée.</span><span class="sxs-lookup"><span data-stu-id="7489a-237">As shown on hello preceding screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="7489a-238">Ceci est un paramètre important, car `docker-compose` imprime plusieurs messages de diagnostic, tels que les conteneurs sont en cours de suppression sur la sortie d’erreur standard hello ou d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="7489a-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="7489a-239">Si vous activez la case à cocher hello, Visual Studio Team Services signale que les erreurs se sont produites au cours de la version de hello, même si tout se passe bien.</span><span class="sxs-lookup"><span data-stu-id="7489a-239">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="7489a-240">Enregistrez cette nouvelle définition de mise en production.</span><span class="sxs-lookup"><span data-stu-id="7489a-240">Save this new release definition.</span></span>


>[!NOTE]
><span data-ttu-id="7489a-241">Ce déploiement inclut un temps d’arrêt, car nous sommes l’arrêt des services d’ancien hello et en cours d’exécution hello nouveau.</span><span class="sxs-lookup"><span data-stu-id="7489a-241">This deployment includes some downtime because we are stopping hello old services and running hello new one.</span></span> <span data-ttu-id="7489a-242">Il est possible de tooavoid cela en effectuant un déploiement bleu-vert.</span><span class="sxs-lookup"><span data-stu-id="7489a-242">It is possible tooavoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="7489a-243">Étape 4.</span><span class="sxs-lookup"><span data-stu-id="7489a-243">Step 4.</span></span> <span data-ttu-id="7489a-244">Tester le pipeline de l’élément de configuration/CD hello</span><span class="sxs-lookup"><span data-stu-id="7489a-244">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="7489a-245">Maintenant que vous avez terminé avec la configuration de hello, il est temps tootest de ce nouveau pipeline de l’élément de configuration/CD.</span><span class="sxs-lookup"><span data-stu-id="7489a-245">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="7489a-246">tootest moyen plus simple de Hello, il est tooupdate Bonjour source code puis de valider Bonjour change dans votre référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="7489a-246">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="7489a-247">Quelques secondes après le push de code de hello, vous verrez une nouvelle build en cours d’exécution dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="7489a-247">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="7489a-248">Une fois terminé, une nouvelle version est déclenchée et déploiera hello nouvelle version d’application hello sur le cluster du Service de conteneur Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7489a-248">Once completed successfully, a new release will be triggered and will deploy hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7489a-249">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7489a-249">Next Steps</span></span>

* <span data-ttu-id="7489a-250">Pour plus d’informations sur l’élément de configuration/CD avec Visual Studio Team Services, consultez hello [VSTS générer une vue d’ensemble](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="7489a-250">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
