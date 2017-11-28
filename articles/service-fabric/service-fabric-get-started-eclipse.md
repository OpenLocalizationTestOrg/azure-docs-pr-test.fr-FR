---
title: aaaAzure Service Fabric plug-in Eclipse | Documents Microsoft
description: "Prise en main hello Service Fabric plug-in d’Eclipse."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="bdfb8-103">Plug-in Service Fabric pour le développement d’applications Java sous Eclipse</span><span class="sxs-lookup"><span data-stu-id="bdfb8-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="bdfb8-104">Eclipse est un des hello plus largement utilisé intégré (IDE) des environnements de développement pour les développeurs Java.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-104">Eclipse is one of hello most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="bdfb8-105">Dans cet article, nous décrivons comment tooset de votre toowork d’environnement de développement Eclipse avec Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-105">In this article, we describe how tooset up your Eclipse development environment toowork with Azure Service Fabric.</span></span> <span data-ttu-id="bdfb8-106">Découvrez comment créer une application Service Fabric tooinstall hello plug-in, l’infrastructure de Service et déployer votre cluster Service Fabric application tooa local ou distant Service Fabric dans Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-106">Learn how tooinstall hello Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application tooa local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="bdfb8-107">Installer ou mettre à jour hello Service Fabric plug-in Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="bdfb8-107">Install or update hello Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="bdfb8-108">Vous pouvez installer un plug-in Service Fabric sur Eclipse.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="bdfb8-109">Hello plug-in vous permet de simplifier les processus hello de génération et de déploiement des services de Java.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-109">hello plug-in can help simplify hello process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="bdfb8-110">Assurez-vous d’avoir hello dernière version d’Eclipse Neon et la version la plus récente de Buildship hello (1.0.17 ou une version ultérieure) installé :</span><span class="sxs-lookup"><span data-stu-id="bdfb8-110">Ensure that you have hello latest version of Eclipse Neon and hello latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="bdfb8-111">versions de hello toocheck des composants installés, dans Eclipse Neon, accédez trop**aide** > **détails de l’Installation**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-111">toocheck hello versions of installed components, in Eclipse Neon, go too**Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="bdfb8-112">tooupdate Buildship, consultez [Eclipse Buildship : Eclipse Plug-ins pour Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="bdfb8-112">tooupdate Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="bdfb8-113">toocheck pour et installer les mises à jour pour Eclipse Neon, sont trop**aide** > **mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-113">toocheck for and install updates for Eclipse Neon, go too**Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="bdfb8-114">tooinstall hello Service Fabric plug-in dans Eclipse Neon, accédez trop**aide** > **installer le nouveau logiciel**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-114">tooinstall hello Service Fabric plug-in, in Eclipse Neon, go too**Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="bdfb8-115">Bonjour **travailler avec** , entrez **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-115">In hello **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="bdfb8-116">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-116">Click **Add**.</span></span>

         ![Plug-in Service Fabric pour Eclipse Neon][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="bdfb8-118">Sélectionnez hello Service Fabric plug-in, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-118">Select hello Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="bdfb8-119">Complétez les étapes d’installation hello et puis acceptez le contrat de licence logiciel Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-119">Complete hello installation steps, and then accept hello Microsoft Software License Terms.</span></span>

<span data-ttu-id="bdfb8-120">Si vous avez déjà hello Service Fabric plug-in installé, assurez-vous que vous avez la version la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-120">If you already have hello Service Fabric plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="bdfb8-121">toocheck pour les mises à jour disponibles, accédez trop**aide** > **détails de l’Installation**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-121">toocheck for available updates, go too**Help** > **Installation Details**.</span></span> <span data-ttu-id="bdfb8-122">Dans la liste de hello des plug-ins installés, sélectionnez le Service Fabric, puis cliquez sur **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-122">In hello list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="bdfb8-123">Les mises à jour disponibles seront installées.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="bdfb8-124">Si l’installation ou la mise à jour de hello Service Fabric plug-in est lente, il peut être en raison du paramètre d’Eclipse tooan.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-124">If installing or updating hello Service Fabric plug-in is slow, it might be due tooan Eclipse setting.</span></span> <span data-ttu-id="bdfb8-125">Eclipse collecte des métadonnées sur tous les sites de tooupdate de modifications qui sont inscrits avec votre instance d’Eclipse.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-125">Eclipse collects metadata on all changes tooupdate sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="bdfb8-126">toospeed processus hello de vérification et l’installation d’une mise à jour du plug-in de l’infrastructure de Service, accédez trop**Sites logiciels disponibles**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-126">toospeed up hello process of checking for and installing a Service Fabric plug-in update, go too**Available Software Sites**.</span></span> <span data-ttu-id="bdfb8-127">Désactivez les cases à cocher hello pour tous les sites à l’exception de hello celle qui pointe l’emplacement du plug-in du Service Fabric toohello (http://dl.microsoft.com/eclipse/azure/servicefabric).</span><span class="sxs-lookup"><span data-stu-id="bdfb8-127">Clear hello check boxes for all sites except for hello one that points toohello Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="bdfb8-128">Créer une application Service Fabric dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="bdfb8-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="bdfb8-129">Dans Eclipse Neon, accédez trop**fichier** > **nouveau** > **autres**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-129">In Eclipse Neon, go too**File** > **New** > **Other**.</span></span> <span data-ttu-id="bdfb8-130">Sélectionnez **Projet Service Fabric**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Nouveau projet Service Fabric, page 1][create-application/p1]

2.  <span data-ttu-id="bdfb8-132">Saisissez un nom pour votre projet, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Nouveau projet Service Fabric, page 2][create-application/p2]

3.  <span data-ttu-id="bdfb8-134">Dans la liste hello des modèles, sélectionnez **modèle de Service**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-134">In hello list of templates, select **Service Template**.</span></span> <span data-ttu-id="bdfb8-135">Sélectionnez votre type de modèle de service (acteur, sans état, conteneur ou binaire invité), puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Nouveau projet Service Fabric, page 3][create-application/p3]

4.  <span data-ttu-id="bdfb8-137">Entrez le nom du service hello et les détails du service, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-137">Enter hello service name and service details, and then click **Finish**.</span></span>

    ![Nouveau projet Service Fabric, page 4][create-application/p4]

5. <span data-ttu-id="bdfb8-139">Lorsque vous créez votre premier projet de Service Fabric Bonjour **ouvrir une Perspective associés** boîte de dialogue, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-139">When you create your first Service Fabric project, in hello **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Nouveau projet Service Fabric, page 5][create-application/p5]

6.  <span data-ttu-id="bdfb8-141">Votre nouveau projet ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="bdfb8-141">Your new project looks like this:</span></span>

    ![Nouveau projet Service Fabric, page 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="bdfb8-143">Créer et déployer une application Service Fabric dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="bdfb8-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="bdfb8-144">Cliquez avec le bouton droit de la souris sur votre nouvelle application Service Fabric, puis sélectionnez **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Menu contextuel Service Fabric][publish/RightClick]

2. <span data-ttu-id="bdfb8-146">Dans le sous-menu de hello, activez l’option hello :</span><span class="sxs-lookup"><span data-stu-id="bdfb8-146">In hello submenu, select hello option you want:</span></span>
    -   <span data-ttu-id="bdfb8-147">application de hello toobuild sans nettoyage, cliquez sur **Application Build**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-147">toobuild hello application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="bdfb8-148">toodo une génération complète de l’application hello, cliquez sur **régénérer l’Application**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-148">toodo a clean build of hello application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="bdfb8-149">application de hello tooclean d’artefacts générés, cliquez sur **propre Application**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-149">tooclean hello application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="bdfb8-150">Dans ce menu, vous pouvez également déployer, annuler le déploiement et publier votre application :</span><span class="sxs-lookup"><span data-stu-id="bdfb8-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="bdfb8-151">cluster local de tooyour toodeploy, cliquez sur **déployer l’Application**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-151">toodeploy tooyour local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="bdfb8-152">Bonjour **publier l’Application** boîte de dialogue, sélectionnez un profil de publication :</span><span class="sxs-lookup"><span data-stu-id="bdfb8-152">In hello **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="bdfb8-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="bdfb8-153">**Local.json**</span></span>
        -  <span data-ttu-id="bdfb8-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="bdfb8-154">**Cloud.json**</span></span>

     <span data-ttu-id="bdfb8-155">Ces fichiers JavaScript Objet Notation (JSON) stockent des informations (par exemple, les points de terminaison de connexion et les informations de sécurité) qui est tooyour tooconnect requis local ou cloud (Azure).</span><span class="sxs-lookup"><span data-stu-id="bdfb8-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required tooconnect tooyour local or cloud (Azure) cluster.</span></span>

  ![Menu Publier de Service Fabric][publish/Publish]

<span data-ttu-id="bdfb8-157">Une autre façon toodeploy votre application de Service Fabric est à l’aide d’Eclipse exécutée les configurations.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-157">An alternate way toodeploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="bdfb8-158">Accédez trop**exécuter** > **les Configurations de série**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-158">Go too**Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="bdfb8-159">Sous **Gradle projet**, sélectionnez hello **ServiceFabricDeployer** exécuter la configuration.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-159">Under **Gradle Project**, select hello **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="bdfb8-160">Dans le volet de droite de hello sur hello **Arguments** onglet, pour **publishProfile**, sélectionnez **local** ou **cloud**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-160">In hello right pane, on hello **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="bdfb8-161">valeur par défaut Hello est **local**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-161">hello default is **local**.</span></span> <span data-ttu-id="bdfb8-162">tooa toodeploy à distance ou le cluster du cloud, sélectionnez **cloud**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-162">toodeploy tooa remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="bdfb8-163">tooensure que les informations correctes hello sont remplies Bonjour des profils de publication, modifiez **Local.json** ou **Cloud.json** en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-163">tooensure that hello proper information is populated in hello publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="bdfb8-164">Vous pouvez ajouter ou mettre à jour les détails du point de terminaison et les informations d’identification de sécurité.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="bdfb8-165">Vérifiez que **du répertoire de travail** pointe application toohello vous souhaitez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-165">Ensure that **Working Directory** points toohello application you want toodeploy.</span></span> <span data-ttu-id="bdfb8-166">toochange hello application, cliquez sur hello **espace de travail** bouton, puis sélectionnez application hello.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-166">toochange hello application, click hello **Workspace** button, and then select hello application you want.</span></span>
  6.    <span data-ttu-id="bdfb8-167">Cliquez sur **Appliquer**, puis sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="bdfb8-168">Votre application est générée et déployée en quelques instants.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="bdfb8-169">Vous pouvez surveiller l’état du déploiement hello dans Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-169">You can monitor hello deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a><span data-ttu-id="bdfb8-170">Ajouter un tooyour de service Service Fabric application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bdfb8-170">Add a Service Fabric service tooyour Service Fabric application</span></span>

<span data-ttu-id="bdfb8-171">tooadd une application Service Fabric Service Fabric service tooan existante, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bdfb8-171">tooadd a Service Fabric service tooan existing Service Fabric application, do hello following steps:</span></span>

1.  <span data-ttu-id="bdfb8-172">Projet de hello contextuel vous voulez tooadd un service, puis cliquez sur **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-172">Right-click hello project you want tooadd a service to, and then click **Service Fabric**.</span></span>

    ![Ajouter un service Service Fabric, page 1][add-service/p1]

2.  <span data-ttu-id="bdfb8-174">Cliquez sur **ajouter un Service Service Fabric**, et hello complète des étapes tooadd un projet toohello de service.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-174">Click **Add Service Fabric Service**, and complete hello set of steps tooadd a service toohello project.</span></span>
3.  <span data-ttu-id="bdfb8-175">Modèle de service hello Sélectionnez votre choix tooadd tooyour projet, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-175">Select hello service template you want tooadd tooyour project, and then click **Next**.</span></span>

    ![Ajouter un service Service Fabric, page 2][add-service/p2]

4.  <span data-ttu-id="bdfb8-177">Entrez le nom du service hello (et autres détails, si nécessaire), puis cliquez sur hello **ajouter un Service** bouton.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-177">Enter hello service name (and other details, as needed), and then click hello **Add Service** button.</span></span>  

    ![Ajouter un service Service Fabric, page 3][add-service/p3]

5.  <span data-ttu-id="bdfb8-179">Une fois que le service de hello est ajouté, structure globale de votre projet recherche similaire toohello suivant du projet :</span><span class="sxs-lookup"><span data-stu-id="bdfb8-179">After hello service is added, your overall project structure looks similar toohello following project:</span></span>

    ![Ajouter un service Service Fabric, page 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="bdfb8-181">Modifier les versions de manifeste de votre application Java Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bdfb8-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="bdfb8-182">versions de manifeste tooedit, cliquez avec le bouton droit sur le projet de hello, accédez trop**Service Fabric** et sélectionnez **modifier les Versions de manifeste...**  à partir de la liste déroulante du menu hello.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-182">tooedit manifest versions, right click on hello project, go too**Service Fabric** and select **Edit Manifest Versions...** from hello menu dropdown.</span></span> <span data-ttu-id="bdfb8-183">Dans l’Assistant de hello, vous pouvez mettre à jour hello des versions manifeste manifeste d’application manifeste, service et hello pour **Code**, **Config** et **données** packages.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-183">In hello wizard, you can update hello manifest versions for application manifest, service manifest and hello versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="bdfb8-184">Si vous activez l’option de hello **mettre à jour automatiquement les applications et les versions de service** et ensuite mettre à jour une version, les versions de manifeste hello puis seront automatiquement mis à jour.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-184">If you check hello option **Automatically update application and service versions** and then update a version, then hello manifest versions will be automatically updated.</span></span> <span data-ttu-id="bdfb8-185">toogive, par exemple, vous tout d’abord sélectionnez hello de la case à cocher, puis version hello de mise à jour de **Code** version 0.0.0 too0.0.1 et cliquez sur **Terminer**, puis de version du manifeste et manifeste d’application de service version sera automatiquement mis à jour too0.0.1.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-185">toogive an example, you first select hello check-box, then update hello version of **Code** version from 0.0.0 too0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated too0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="bdfb8-186">Mettre à niveau votre application Java Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bdfb8-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="bdfb8-187">Pour un scénario de mise à niveau, par exemple vous avez créé hello **App1** projet à l’aide de hello Service Fabric plug-in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-187">For an upgrade scenario, say you created hello **App1** project by using hello Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="bdfb8-188">Avoir déployé à l’aide de toocreate de plug-in hello une application nommée **fabric : / App1Application**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-188">You deployed it by using hello plug-in toocreate an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="bdfb8-189">type d’application Hello est **App1AppicationType**, et la version de l’application hello est 1.0.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-189">hello application type is **App1AppicationType**, and hello application version is 1.0.</span></span> <span data-ttu-id="bdfb8-190">Maintenant, vous souhaitez que tooupgrade votre application sans interrompre la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-190">Now, you want tooupgrade your application without interrupting availability.</span></span>

<span data-ttu-id="bdfb8-191">Tout d’abord, apporter des modifications tooyour application, puis reconstruire hello modifié service.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-191">First, make any changes tooyour application, and then rebuild hello modified service.</span></span> <span data-ttu-id="bdfb8-192">Hello de mise à jour modifié le fichier manifeste du service (ServiceManifest.xml) avec les versions hello mis à jour pour hello service (et de Code, configuration ou données, selon le cas).</span><span class="sxs-lookup"><span data-stu-id="bdfb8-192">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="bdfb8-193">En outre, modifier le manifeste de l’application hello (ApplicationManifest.xml) avec le numéro de version hello mis à jour pour l’application hello et hello service modifié.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-193">Also, modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application and hello modified service.</span></span>  

<span data-ttu-id="bdfb8-194">tooupgrade votre application à l’aide d’Eclipse Neon, vous pouvez créer un profil de configuration d’exécution en double.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-194">tooupgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="bdfb8-195">Ensuite, utilisez tooupgrade votre application en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-195">Then, use it tooupgrade your application as needed.</span></span>

1.  <span data-ttu-id="bdfb8-196">Accédez trop**exécuter** > **les Configurations de série**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-196">Go too**Run** > **Run Configurations**.</span></span> <span data-ttu-id="bdfb8-197">Dans le volet gauche de hello, cliquez sur hello petite flèche toohello gauche **Gradle projet**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-197">In hello left pane, click hello small arrow toohello left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="bdfb8-198">Cliquez avec le bouton droit de la souris sur **ServiceFabricDeployer**, puis sélectionnez **Dupliquer**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="bdfb8-199">Entrez un nouveau nom pour cette configuration, par exemple, **ServiceFabricUpgrader**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="bdfb8-200">Dans le panneau droit hello, sur hello **Arguments** , modifiez **- ipconfig /release = 'déployer'** trop**- ipconfig /release = 'mise à niveau'**, puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-200">In hello right panel, on hello **Arguments** tab, change **-Pconfig='deploy'** too**-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="bdfb8-201">Ce processus crée et enregistre un profil de configuration d’exécution vous pouvez utiliser à n’importe quel tooupgrade de temps à votre application.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-201">This process creates and saves a run configuration profile you can use at any time tooupgrade your application.</span></span> <span data-ttu-id="bdfb8-202">Il obtient également la dernière version de type application mis à jour hello à partir du fichier manifeste d’application hello.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-202">It also gets hello latest updated application type version from hello application manifest file.</span></span>

<span data-ttu-id="bdfb8-203">mise à niveau des applications Hello prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-203">hello application upgrade takes a few minutes.</span></span> <span data-ttu-id="bdfb8-204">Vous pouvez surveiller la mise à niveau des applications de hello dans Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-204">You can monitor hello application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="bdfb8-205">Migration d’ancien toobe d’applications Java de l’infrastructure de Service utilisé avec Maven</span><span class="sxs-lookup"><span data-stu-id="bdfb8-205">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="bdfb8-206">Nous avons déplacé récemment bibliothèques Service Fabric Java à partir du référentiel de tooMaven Service Fabric Java SDK.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="bdfb8-207">Alors que hello nouvelles applications générer à l’aide d’Eclipse, génère les plus récentes des projets mis à jour (qui seront en mesure de toowork avec Maven), vous pouvez mettre à jour votre Service Fabric existant sans état ou les applications Java acteur, qui utilisaient l’hello Service Fabric Java SDK versions antérieures, toouse hello Service Fabric dépendances Java à partir de Maven.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-207">While hello new applications you generate using Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="bdfb8-208">Suivez les étapes de hello mentionnés [ici](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure votre ancienne application fonctionne avec Maven.</span><span class="sxs-lookup"><span data-stu-id="bdfb8-208">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
