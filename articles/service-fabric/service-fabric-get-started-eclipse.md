---
title: Plug-in Azure Service Fabric pour Eclipse | Documents Microsoft
description: Prise en main du plug-in Service Fabric pour Eclipse
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
ms.openlocfilehash: 98c1b99972b9ad7a396d72b98e727286f6822e42
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="a599f-103">Plug-in Service Fabric pour le développement d’applications Java sous Eclipse</span><span class="sxs-lookup"><span data-stu-id="a599f-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="a599f-104">Eclipse est l’un des environnements de développement intégrés (IDE) les plus largement utilisés par les développeurs Java.</span><span class="sxs-lookup"><span data-stu-id="a599f-104">Eclipse is one of the most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="a599f-105">Dans cet article, nous décrivons comment configurer votre environnement de développement Eclipse pour utiliser Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a599f-105">In this article, we describe how to set up your Eclipse development environment to work with Azure Service Fabric.</span></span> <span data-ttu-id="a599f-106">Découvrez comment installer le plug-in Service Fabric, créer une application Service Fabric et déployer votre application Service Fabric dans un cluster Service Fabric local ou distant sur Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="a599f-106">Learn how to install the Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application to a local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-the-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="a599f-107">Installer ou mettre à jour le plug-in Service Fabric sur Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="a599f-107">Install or update the Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="a599f-108">Vous pouvez installer un plug-in Service Fabric sur Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a599f-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="a599f-109">Ce plug-in peut aider à simplifier le processus de génération et le déploiement des services Java.</span><span class="sxs-lookup"><span data-stu-id="a599f-109">The plug-in can help simplify the process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="a599f-110">Assurez-vous que la dernière version d’Eclipse Neon et la dernière version de Buildship (1.0.17 ou une version ultérieure) sont installées :</span><span class="sxs-lookup"><span data-stu-id="a599f-110">Ensure that you have the latest version of Eclipse Neon and the latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="a599f-111">Pour vérifier les versions des composants installés, dans Eclipse Neon, accédez à **Aide** > **Détails de l’installation**.</span><span class="sxs-lookup"><span data-stu-id="a599f-111">To check the versions of installed components, in Eclipse Neon, go to **Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="a599f-112">Pour mettre à jour Buildship, consultez [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update] (Eclipse Buildship : plug-in Eclipse pour Gradle).</span><span class="sxs-lookup"><span data-stu-id="a599f-112">To update Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="a599f-113">Pour vérifier et installer les mises à jour pour Eclipse Neon, accédez à **Aide** > **Rechercher les mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="a599f-113">To check for and install updates for Eclipse Neon, go to **Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="a599f-114">Pour installer le plug-in Service Fabric, dans Eclipse Neon, accédez à **Aide** > **Installer un nouveau logiciel**.</span><span class="sxs-lookup"><span data-stu-id="a599f-114">To install the Service Fabric plug-in, in Eclipse Neon, go to **Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="a599f-115">Dans la zone **Work with** (Utiliser avec), entrez : **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="a599f-115">In the **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="a599f-116">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="a599f-116">Click **Add**.</span></span>

         ![Plug-in Service Fabric pour Eclipse Neon][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="a599f-118">Sélectionnez le plug-in Service Fabric, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="a599f-118">Select the Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="a599f-119">Terminez les étapes d’installation, puis acceptez les termes du contrat de licence du logiciel Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a599f-119">Complete the installation steps, and then accept the Microsoft Software License Terms.</span></span>

<span data-ttu-id="a599f-120">Si le plug-in Service Fabric est déjà installé, assurez-vous que vous disposez de la dernière version.</span><span class="sxs-lookup"><span data-stu-id="a599f-120">If you already have the Service Fabric plug-in installed, make sure that you have the latest version.</span></span> <span data-ttu-id="a599f-121">Pour vérifier les mises à jour disponibles, accédez à **Aide** > **Détails de l’installation**.</span><span class="sxs-lookup"><span data-stu-id="a599f-121">To check for available updates, go to **Help** > **Installation Details**.</span></span> <span data-ttu-id="a599f-122">Dans la liste des plug-ins installés, sélectionnez Service Fabric, puis cliquez sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="a599f-122">In the list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="a599f-123">Les mises à jour disponibles seront installées.</span><span class="sxs-lookup"><span data-stu-id="a599f-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="a599f-124">La lenteur de l’installation ou de la mise à jour du plug-in Service Fabric peut être due à un paramètre d’Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a599f-124">If installing or updating the Service Fabric plug-in is slow, it might be due to an Eclipse setting.</span></span> <span data-ttu-id="a599f-125">Eclipse collecte des métadonnées sur toutes les modifications pour mettre à jour les sites enregistrés avec votre instance d’Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a599f-125">Eclipse collects metadata on all changes to update sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="a599f-126">Pour accélérer le processus de vérification et l’installation d’une mise à jour du plug-in Service Fabric, accédez à **Sites logiciels disponibles**.</span><span class="sxs-lookup"><span data-stu-id="a599f-126">To speed up the process of checking for and installing a Service Fabric plug-in update, go to **Available Software Sites**.</span></span> <span data-ttu-id="a599f-127">Désactivez les cases à cocher pour tous les sites, sauf pour celui qui pointe vers l’emplacement du plug-in Service Fabric (http://dl.microsoft.com/eclipse/azure/servicefabric).</span><span class="sxs-lookup"><span data-stu-id="a599f-127">Clear the check boxes for all sites except for the one that points to the Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="a599f-128">Créer une application Service Fabric dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="a599f-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="a599f-129">Dans Eclipse Neon, accédez à **Fichier** > **Nouveau** > **Autre**.</span><span class="sxs-lookup"><span data-stu-id="a599f-129">In Eclipse Neon, go to **File** > **New** > **Other**.</span></span> <span data-ttu-id="a599f-130">Sélectionnez **Projet Service Fabric**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="a599f-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Nouveau projet Service Fabric, page 1][create-application/p1]

2.  <span data-ttu-id="a599f-132">Saisissez un nom pour votre projet, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="a599f-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Nouveau projet Service Fabric, page 2][create-application/p2]

3.  <span data-ttu-id="a599f-134">Dans la liste des modèles, sélectionnez **Modèle de service**.</span><span class="sxs-lookup"><span data-stu-id="a599f-134">In the list of templates, select **Service Template**.</span></span> <span data-ttu-id="a599f-135">Sélectionnez votre type de modèle de service (acteur, sans état, conteneur ou binaire invité), puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="a599f-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Nouveau projet Service Fabric, page 3][create-application/p3]

4.  <span data-ttu-id="a599f-137">Saisissez le nom du service et les détails du service, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="a599f-137">Enter the service name and service details, and then click **Finish**.</span></span>

    ![Nouveau projet Service Fabric, page 4][create-application/p4]

5. <span data-ttu-id="a599f-139">Lorsque vous créez votre premier projet Service Fabric, dans la boîte de dialogue **Ouvrir la perspective associée**, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="a599f-139">When you create your first Service Fabric project, in the **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Nouveau projet Service Fabric, page 5][create-application/p5]

6.  <span data-ttu-id="a599f-141">Votre nouveau projet ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="a599f-141">Your new project looks like this:</span></span>

    ![Nouveau projet Service Fabric, page 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="a599f-143">Créer et déployer une application Service Fabric dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="a599f-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="a599f-144">Cliquez avec le bouton droit de la souris sur votre nouvelle application Service Fabric, puis sélectionnez **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="a599f-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Menu contextuel Service Fabric][publish/RightClick]

2. <span data-ttu-id="a599f-146">Dans le sous-menu, sélectionnez l’option souhaitée :</span><span class="sxs-lookup"><span data-stu-id="a599f-146">In the submenu, select the option you want:</span></span>
    -   <span data-ttu-id="a599f-147">Pour créer l’application sans suppression, cliquez sur **Créer l’application**.</span><span class="sxs-lookup"><span data-stu-id="a599f-147">To build the application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="a599f-148">Pour supprimer, puis générer l’application, cliquez sur **Régénérer l’application**.</span><span class="sxs-lookup"><span data-stu-id="a599f-148">To do a clean build of the application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="a599f-149">Pour supprimer l’application des artefacts générés, cliquez sur **Nettoyer l’application**.</span><span class="sxs-lookup"><span data-stu-id="a599f-149">To clean the application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="a599f-150">Dans ce menu, vous pouvez également déployer, annuler le déploiement et publier votre application :</span><span class="sxs-lookup"><span data-stu-id="a599f-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="a599f-151">Pour effectuer le déploiement dans votre cluster local, cliquez sur **Déployer l’application**.</span><span class="sxs-lookup"><span data-stu-id="a599f-151">To deploy to your local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="a599f-152">Dans la boîte de dialogue **Publication de l’application**, sélectionnez un profil de publication :</span><span class="sxs-lookup"><span data-stu-id="a599f-152">In the **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="a599f-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="a599f-153">**Local.json**</span></span>
        -  <span data-ttu-id="a599f-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="a599f-154">**Cloud.json**</span></span>

     <span data-ttu-id="a599f-155">Ces fichiers JavaScript Object Notation (JSON) stockent des informations (par exemple, les points de terminaison de connexion et les informations de sécurité) requises pour se connecter à votre cluster local ou cloud (Azure).</span><span class="sxs-lookup"><span data-stu-id="a599f-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required to connect to your local or cloud (Azure) cluster.</span></span>

  ![Menu Publier de Service Fabric][publish/Publish]

<span data-ttu-id="a599f-157">Une autre méthode pour déployer votre application Service Fabric consiste à utiliser des configurations d’exécution Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a599f-157">An alternate way to deploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="a599f-158">Accédez à **Exécuter** > **Configurations d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="a599f-158">Go to **Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="a599f-159">Sous **Projet Gradle**, sélectionnez la configuration d’exécution **ServiceFabricDeployer**.</span><span class="sxs-lookup"><span data-stu-id="a599f-159">Under **Gradle Project**, select the **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="a599f-160">Dans le volet de droite, sous l’onglet **Arguments**, pour **publishProfile**, sélectionnez **local** ou **cloud**.</span><span class="sxs-lookup"><span data-stu-id="a599f-160">In the right pane, on the **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="a599f-161">La valeur par défaut est **local**.</span><span class="sxs-lookup"><span data-stu-id="a599f-161">The default is **local**.</span></span> <span data-ttu-id="a599f-162">Pour effectuer un déploiement dans un cluster cloud ou distant, sélectionnez **cloud**.</span><span class="sxs-lookup"><span data-stu-id="a599f-162">To deploy to a remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="a599f-163">Pour vous assurer que les informations appropriées sont renseignées dans les profils de publication, modifiez **Local.json** ou **Cloud.json** selon les besoins.</span><span class="sxs-lookup"><span data-stu-id="a599f-163">To ensure that the proper information is populated in the publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="a599f-164">Vous pouvez ajouter ou mettre à jour les détails du point de terminaison et les informations d’identification de sécurité.</span><span class="sxs-lookup"><span data-stu-id="a599f-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="a599f-165">Vérifiez que **Répertoire de travail** pointe vers l’application que vous souhaitez déployer.</span><span class="sxs-lookup"><span data-stu-id="a599f-165">Ensure that **Working Directory** points to the application you want to deploy.</span></span> <span data-ttu-id="a599f-166">Pour modifier l’application, cliquez sur le bouton **Espace de travail**, puis sélectionnez l’application souhaitée.</span><span class="sxs-lookup"><span data-stu-id="a599f-166">To change the application, click the **Workspace** button, and then select the application you want.</span></span>
  6.    <span data-ttu-id="a599f-167">Cliquez sur **Appliquer**, puis sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="a599f-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="a599f-168">Votre application est générée et déployée en quelques instants.</span><span class="sxs-lookup"><span data-stu-id="a599f-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="a599f-169">Vous pouvez contrôler le statut de déploiement dans Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="a599f-169">You can monitor the deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-to-your-service-fabric-application"></a><span data-ttu-id="a599f-170">Ajouter un service Service Fabric à votre application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a599f-170">Add a Service Fabric service to your Service Fabric application</span></span>

<span data-ttu-id="a599f-171">Pour ajouter un service Service Fabric à une application Service Fabric existante, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a599f-171">To add a Service Fabric service to an existing Service Fabric application, do the following steps:</span></span>

1.  <span data-ttu-id="a599f-172">Cliquez avec le bouton droit de la souris sur le projet auquel vous souhaitez ajouter un service, puis cliquez sur **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="a599f-172">Right-click the project you want to add a service to, and then click **Service Fabric**.</span></span>

    ![Ajouter un service Service Fabric, page 1][add-service/p1]

2.  <span data-ttu-id="a599f-174">Cliquez sur **Ajouter un service Service Fabric** et terminez les d’étapes pour ajouter un service au projet.</span><span class="sxs-lookup"><span data-stu-id="a599f-174">Click **Add Service Fabric Service**, and complete the set of steps to add a service to the project.</span></span>
3.  <span data-ttu-id="a599f-175">Sélectionnez le modèle de service que vous souhaitez ajouter à votre projet et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="a599f-175">Select the service template you want to add to your project, and then click **Next**.</span></span>

    ![Ajouter un service Service Fabric, page 2][add-service/p2]

4.  <span data-ttu-id="a599f-177">Entrez le nom du service (et autres détails, si nécessaire), puis cliquez sur le bouton **Ajouter un service**.</span><span class="sxs-lookup"><span data-stu-id="a599f-177">Enter the service name (and other details, as needed), and then click the **Add Service** button.</span></span>  

    ![Ajouter un service Service Fabric, page 3][add-service/p3]

5.  <span data-ttu-id="a599f-179">Une fois le service ajouté, la structure globale de votre projet ressemble au projet suivant :</span><span class="sxs-lookup"><span data-stu-id="a599f-179">After the service is added, your overall project structure looks similar to the following project:</span></span>

    ![Ajouter un service Service Fabric, page 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="a599f-181">Modifier les versions de manifeste de votre application Java Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a599f-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="a599f-182">Pour modifier les versions de manifeste, cliquez avec le bouton droit sur le projet, accédez à **Service Fabric** et sélectionnez **Modifier les versions de manifeste...**  à partir de la liste déroulante du menu.</span><span class="sxs-lookup"><span data-stu-id="a599f-182">To edit manifest versions, right click on the project, go to **Service Fabric** and select **Edit Manifest Versions...** from the menu dropdown.</span></span> <span data-ttu-id="a599f-183">Dans l’Assistant, vous pouvez mettre à jour les versions du manifeste d’application, du manifeste de service et des packages **Code**, **Config** et **Data**.</span><span class="sxs-lookup"><span data-stu-id="a599f-183">In the wizard, you can update the manifest versions for application manifest, service manifest and the versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="a599f-184">Si vous activez l’option **Mettre à jour automatiquement les versions des applications et des services**, puis que vous mettez à jour une version, les versions des manifestes seront automatiquement mises à jour.</span><span class="sxs-lookup"><span data-stu-id="a599f-184">If you check the option **Automatically update application and service versions** and then update a version, then the manifest versions will be automatically updated.</span></span> <span data-ttu-id="a599f-185">Par exemple, vous commencez par cocher la case, vous changez la version du **Code** de 0.0.0 à 0.0.1, puis vous cliquez sur **Terminer**. La version du manifeste de service et du manifeste d’application sera automatiquement mise à jour à 0.0.1.</span><span class="sxs-lookup"><span data-stu-id="a599f-185">To give an example, you first select the check-box, then update the version of **Code** version from 0.0.0 to 0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated to 0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="a599f-186">Mettre à niveau votre application Java Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a599f-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="a599f-187">Prenons l’exemple d’un scénario de mise à niveau. Admettons que vous avez créé le projet **App1** à l’aide du plug-in Service Fabric dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a599f-187">For an upgrade scenario, say you created the **App1** project by using the Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="a599f-188">Vous l’avez déployé à l’aide du plug-in pour créer une application nommée **fabric:/App1Application**.</span><span class="sxs-lookup"><span data-stu-id="a599f-188">You deployed it by using the plug-in to create an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="a599f-189">Le type d’application est **App1AppicationType**, et la version de l’application est 1.0.</span><span class="sxs-lookup"><span data-stu-id="a599f-189">The application type is **App1AppicationType**, and the application version is 1.0.</span></span> <span data-ttu-id="a599f-190">Vous souhaitez à présent mettre à niveau votre application sans interrompre la disponibilité.</span><span class="sxs-lookup"><span data-stu-id="a599f-190">Now, you want to upgrade your application without interrupting availability.</span></span>

<span data-ttu-id="a599f-191">Tout d’abord, apportez les éventuelles modifications à votre application, puis reconstruisez le service modifié.</span><span class="sxs-lookup"><span data-stu-id="a599f-191">First, make any changes to your application, and then rebuild the modified service.</span></span> <span data-ttu-id="a599f-192">Mettez à jour le fichier manifeste du service modifié (ServiceManifest.xml) avec les versions mises à jour du service (Code, Config ou Données, comme il convient).</span><span class="sxs-lookup"><span data-stu-id="a599f-192">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="a599f-193">Modifiez également le manifeste de l’application (ApplicationManifest.xml) avec le numéro de version mis à jour de l’application et le service modifié.</span><span class="sxs-lookup"><span data-stu-id="a599f-193">Also, modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application and the modified service.</span></span>  

<span data-ttu-id="a599f-194">Pour mettre à niveau votre application à l’aide d’Eclipse Neon, vous pouvez créer un profil de configuration d’exécution en double.</span><span class="sxs-lookup"><span data-stu-id="a599f-194">To upgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="a599f-195">Ensuite, utilisez-le pour mettre à niveau votre application selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="a599f-195">Then, use it to upgrade your application as needed.</span></span>

1.  <span data-ttu-id="a599f-196">Accédez à **Exécuter** > **Configurations d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="a599f-196">Go to **Run** > **Run Configurations**.</span></span> <span data-ttu-id="a599f-197">Dans le volet de gauche, cliquez sur la petite flèche à gauche de **Projet Gradle**.</span><span class="sxs-lookup"><span data-stu-id="a599f-197">In the left pane, click the small arrow to the left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="a599f-198">Cliquez avec le bouton droit de la souris sur **ServiceFabricDeployer**, puis sélectionnez **Dupliquer**.</span><span class="sxs-lookup"><span data-stu-id="a599f-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="a599f-199">Entrez un nouveau nom pour cette configuration, par exemple, **ServiceFabricUpgrader**.</span><span class="sxs-lookup"><span data-stu-id="a599f-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="a599f-200">Dans le volet de droite, sous l’onglet **Arguments**, remplacez **-Pconfig='deploy'** par **-Pconfig='upgrade'**, puis cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="a599f-200">In the right panel, on the **Arguments** tab, change **-Pconfig='deploy'** to **-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="a599f-201">Ce processus crée et enregistre un profil de configuration d’exécution que vous pouvez utiliser à tout moment pour mettre à niveau votre application.</span><span class="sxs-lookup"><span data-stu-id="a599f-201">This process creates and saves a run configuration profile you can use at any time to upgrade your application.</span></span> <span data-ttu-id="a599f-202">Il permet également d’obtenir la dernière version mise à jour du type d’application à partir du fichier de manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="a599f-202">It also gets the latest updated application type version from the application manifest file.</span></span>

<span data-ttu-id="a599f-203">La mise à niveau de l’application prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="a599f-203">The application upgrade takes a few minutes.</span></span> <span data-ttu-id="a599f-204">Vous pouvez contrôler la mise à niveau de l’application dans Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="a599f-204">You can monitor the application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-to-be-used-with-maven"></a><span data-ttu-id="a599f-205">Migration d’anciennes applications Java Service Fabric à utiliser avec Maven</span><span class="sxs-lookup"><span data-stu-id="a599f-205">Migrating old Service Fabric Java applications to be used with Maven</span></span>
<span data-ttu-id="a599f-206">Nous avons récemment déplacé les bibliothèques Java Service Fabric vers un référentiel Maven depuis le Kit de développement logiciel (SDK) Java Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a599f-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK to Maven repository.</span></span> <span data-ttu-id="a599f-207">Tandis que les nouvelles applications que vous générez à l’aide d’Eclipse génèrent les derniers projets mis à jour (en mesure de fonctionner avec Maven), vous pouvez mettre à jour vos services sans état Service Fabric existants ou vos applications Java d’acteur existantes ayant utilisé le Kit de développement logiciel (SDK) précédemment, afin d’utiliser les dépendances Java Service Fabric à partir de Maven.</span><span class="sxs-lookup"><span data-stu-id="a599f-207">While the new applications you generate using Eclipse, will generate latest updated projects (which will be able to work with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using the Service Fabric Java SDK earlier, to use the Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="a599f-208">Suivez les étapes mentionnées [ici](service-fabric-migrate-old-javaapp-to-use-maven.md) pour vous assurer qu’une version plus ancienne de votre application fonctionne avec Maven.</span><span class="sxs-lookup"><span data-stu-id="a599f-208">Please follow the steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) to ensure your older application works with Maven.</span></span>

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
