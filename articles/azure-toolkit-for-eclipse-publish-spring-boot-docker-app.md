---
title: Publier une application Spring Boot en tant que conteneur Docker avec le kit de ressources Azure pour Eclipse | Microsoft Docs
description: "Découvrez comment publier une application web sur Microsoft Azure en tant que conteneur Docker à l’aide du kit de ressources Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: fcb60fcfbda26f5f37bfb0edcb01f8737188b6bc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="0967f-103">Publier une application Spring Boot en tant que conteneur Docker avec le kit de ressources Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="0967f-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="0967f-104">L’[infrastructure Spring] est une solution open source qui aide les développeurs Java à créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="0967f-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="0967f-105">Un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="0967f-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="0967f-106">[Docker] est une solution open source qui aide les développeurs à automatiser le déploiement, la mise à l’échelle et la gestion de leurs applications qui s’exécutent dans des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="0967f-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="0967f-107">Ce didacticiel détaille la marche à suivre pour déployer une application Spring Boot en tant que conteneur Docker vers Microsoft Azure à l’aide du kit de ressources Azure pour Eclipse.</span><span class="sxs-lookup"><span data-stu-id="0967f-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a><span data-ttu-id="0967f-108">Cloner le référentiel Docker Spring Boot par défaut</span><span class="sxs-lookup"><span data-stu-id="0967f-108">Clone the default Spring Boot Docker repository</span></span>

### <a name="import-the-public-repository"></a><span data-ttu-id="0967f-109">Importer le référentiel public</span><span class="sxs-lookup"><span data-stu-id="0967f-109">Import the public repository</span></span>

<span data-ttu-id="0967f-110">Les étapes suivantes détaillent les étapes du clonage du référentiel Spring Boot Docker sur votre ordinateur local à l’aide d’IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0967f-110">The following steps walk you through cloning the Spring Boot Docker repository to your local computer by using IntelliJ.</span></span> <span data-ttu-id="0967f-111">Si vous voulez utiliser une ligne de commande, voir [Déployer une application Spring Boot sur Linux dans Azure Container Service][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="0967f-111">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="0967f-112">Ouvrez Eclipse.</span><span class="sxs-lookup"><span data-stu-id="0967f-112">Open Eclipse.</span></span>

1. <span data-ttu-id="0967f-113">Cliquez sur **Fichier** > **Importer**.</span><span class="sxs-lookup"><span data-stu-id="0967f-113">Click **File** > **Import**.</span></span>

   ![Menu Importer fichier][CL01]

1. <span data-ttu-id="0967f-115">Lorsque la boîte de dialogue **Importer** s’ouvre :</span><span class="sxs-lookup"><span data-stu-id="0967f-115">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="0967f-116">a.</span><span class="sxs-lookup"><span data-stu-id="0967f-116">a.</span></span> <span data-ttu-id="0967f-117">Développez **Git**.</span><span class="sxs-lookup"><span data-stu-id="0967f-117">Expand **Git**.</span></span>

   <span data-ttu-id="0967f-118">b.</span><span class="sxs-lookup"><span data-stu-id="0967f-118">b.</span></span> <span data-ttu-id="0967f-119">Sélectionnez **Projets de Git**.</span><span class="sxs-lookup"><span data-stu-id="0967f-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="0967f-120">c.</span><span class="sxs-lookup"><span data-stu-id="0967f-120">c.</span></span> <span data-ttu-id="0967f-121">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="0967f-121">Click **Next**.</span></span>

   ![Boîte de dialogue Importer][CL02]

1. <span data-ttu-id="0967f-123">Sur la page **Sélectionner une source de référentiel** :</span><span class="sxs-lookup"><span data-stu-id="0967f-123">On the **Select Repository Source** page:</span></span>

   <span data-ttu-id="0967f-124">a.</span><span class="sxs-lookup"><span data-stu-id="0967f-124">a.</span></span> <span data-ttu-id="0967f-125">Sélectionnez **Cloner l’URI**.</span><span class="sxs-lookup"><span data-stu-id="0967f-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="0967f-126">b.</span><span class="sxs-lookup"><span data-stu-id="0967f-126">b.</span></span> <span data-ttu-id="0967f-127">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="0967f-127">Click **Next**.</span></span>

   ![Sélectionner la page source du référentiel][CL03]

1. <span data-ttu-id="0967f-129">Sur la page **Référentiel Git source** :</span><span class="sxs-lookup"><span data-stu-id="0967f-129">On the **Source Git Repository** page:</span></span>

   <span data-ttu-id="0967f-130">a.</span><span class="sxs-lookup"><span data-stu-id="0967f-130">a.</span></span> <span data-ttu-id="0967f-131">Pour **URI**, entrez `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span><span class="sxs-lookup"><span data-stu-id="0967f-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="0967f-132">Cette étape devrait compléter automatiquement les champs **Hôte** et **Chemin d’accès du référentiel** avec les valeurs appropriées.</span><span class="sxs-lookup"><span data-stu-id="0967f-132">This step should automatically populate the **Host** and **Repository path** fields with the correct values.</span></span>
   
   <span data-ttu-id="0967f-133">b.</span><span class="sxs-lookup"><span data-stu-id="0967f-133">b.</span></span> <span data-ttu-id="0967f-134">Le référentiel Spring Boot est public. Vous n’avez donc pas à entrer vos identifiants Git.</span><span class="sxs-lookup"><span data-stu-id="0967f-134">The Spring Boot repository is public, so you should not have to enter your Git username and password.</span></span>
   
   <span data-ttu-id="0967f-135">c.</span><span class="sxs-lookup"><span data-stu-id="0967f-135">c.</span></span> <span data-ttu-id="0967f-136">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="0967f-136">Click **Next**.</span></span>

   ![Page du référentiel Git source][CL04]

1. <span data-ttu-id="0967f-138">Dans la page **Sélection de la branche**, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="0967f-138">On the **Branch Selection** page, click **Next**.</span></span>

   ![Page Sélection de la branche][CL05]

1. <span data-ttu-id="0967f-140">Sur la page **Destination locale** :</span><span class="sxs-lookup"><span data-stu-id="0967f-140">On the **Local Destination** page:</span></span>

   <span data-ttu-id="0967f-141">a.</span><span class="sxs-lookup"><span data-stu-id="0967f-141">a.</span></span> <span data-ttu-id="0967f-142">Spécifiez le dossier local où vous souhaitez placer votre référentiel local.</span><span class="sxs-lookup"><span data-stu-id="0967f-142">Specify the local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="0967f-143">b.</span><span class="sxs-lookup"><span data-stu-id="0967f-143">b.</span></span> <span data-ttu-id="0967f-144">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="0967f-144">Click **Next**.</span></span>

   ![Page Destination locale][CL06]

1. <span data-ttu-id="0967f-146">Sur la page **Sélectionner un assistant pour l’importation de projets** :</span><span class="sxs-lookup"><span data-stu-id="0967f-146">On the **Select a wizard to use for importing projects** page:</span></span>

   <span data-ttu-id="0967f-147">a.</span><span class="sxs-lookup"><span data-stu-id="0967f-147">a.</span></span> <span data-ttu-id="0967f-148">Sélectionnez **Importer en tant que projet général**.</span><span class="sxs-lookup"><span data-stu-id="0967f-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="0967f-149">b.</span><span class="sxs-lookup"><span data-stu-id="0967f-149">b.</span></span> <span data-ttu-id="0967f-150">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="0967f-150">Click **Next**.</span></span>

   ![Page « Sélectionner un assistant pour l’importation de projets »][CL07]

1. <span data-ttu-id="0967f-152">Sur la page **Importer des projets** :</span><span class="sxs-lookup"><span data-stu-id="0967f-152">On the **Import Projects** page:</span></span>

   <span data-ttu-id="0967f-153">a.</span><span class="sxs-lookup"><span data-stu-id="0967f-153">a.</span></span> <span data-ttu-id="0967f-154">Spécifiez le nom de votre projet.</span><span class="sxs-lookup"><span data-stu-id="0967f-154">Specify your project name.</span></span>
   
   <span data-ttu-id="0967f-155">b.</span><span class="sxs-lookup"><span data-stu-id="0967f-155">b.</span></span> <span data-ttu-id="0967f-156">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="0967f-156">Click **Finish**.</span></span>

   ![Page Importer des projets][CL08]

1. <span data-ttu-id="0967f-158">Une fois le référentiel cloné avec succès, tous les fichiers répertoriés dans Eclipse sont visibles.</span><span class="sxs-lookup"><span data-stu-id="0967f-158">When the repository is cloned successfully, you see all the files listed in Eclipse.</span></span>

   ![Référentiel local][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="0967f-160">Créer un projet Maven à partir de votre référentiel local</span><span class="sxs-lookup"><span data-stu-id="0967f-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="0967f-161">Le référentiel Spring Boot Docker contient un projet Maven terminé à utiliser pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0967f-161">The Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="0967f-162">Cliquez sur **Fichier** > **Importer**.</span><span class="sxs-lookup"><span data-stu-id="0967f-162">Click **File** > **Import**.</span></span>

   ![Commande Importer du menu Fichier][CL01]

1. <span data-ttu-id="0967f-164">Lorsque la boîte de dialogue **Importer** s’ouvre :</span><span class="sxs-lookup"><span data-stu-id="0967f-164">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="0967f-165">a.</span><span class="sxs-lookup"><span data-stu-id="0967f-165">a.</span></span> <span data-ttu-id="0967f-166">Développez **Maven**.</span><span class="sxs-lookup"><span data-stu-id="0967f-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="0967f-167">b.</span><span class="sxs-lookup"><span data-stu-id="0967f-167">b.</span></span> <span data-ttu-id="0967f-168">Sélectionnez **Projets Maven existants**.</span><span class="sxs-lookup"><span data-stu-id="0967f-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="0967f-169">c.</span><span class="sxs-lookup"><span data-stu-id="0967f-169">c.</span></span> <span data-ttu-id="0967f-170">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="0967f-170">Click **Next**.</span></span>

   ![Boîte de dialogue Importer][MV01]

1. <span data-ttu-id="0967f-172">Sur la page **Projets Maven** :</span><span class="sxs-lookup"><span data-stu-id="0967f-172">On the **Maven Projects** page:</span></span>

   <span data-ttu-id="0967f-173">a.</span><span class="sxs-lookup"><span data-stu-id="0967f-173">a.</span></span> <span data-ttu-id="0967f-174">Pour **Répertoire racine**, spécifiez le dossier **complete** dans votre référentiel local.</span><span class="sxs-lookup"><span data-stu-id="0967f-174">For **Root Directory**, specify the **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="0967f-175">b.</span><span class="sxs-lookup"><span data-stu-id="0967f-175">b.</span></span> <span data-ttu-id="0967f-176">Développez la section **Avancé**, puis entrez un nom personnalisé dans le champ **Modèle de nom**.</span><span class="sxs-lookup"><span data-stu-id="0967f-176">Expand the **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="0967f-177">c.</span><span class="sxs-lookup"><span data-stu-id="0967f-177">c.</span></span> <span data-ttu-id="0967f-178">Activez la case à cocher pour le fichier **pom.xml** dans le projet.</span><span class="sxs-lookup"><span data-stu-id="0967f-178">Select the box for the **pom.xml** file in the project.</span></span>
   
   <span data-ttu-id="0967f-179">d.</span><span class="sxs-lookup"><span data-stu-id="0967f-179">d.</span></span> <span data-ttu-id="0967f-180">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="0967f-180">Click **Finish**.</span></span>

   ![Page Projets Maven][MV02]

1. <span data-ttu-id="0967f-182">Une fois le projet Maven ouvert, vous pouvez voir un deuxième projet répertorié dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="0967f-182">When the Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Projet Maven local][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="0967f-184">Générer votre application Spring Boot à l’aide de Maven</span><span class="sxs-lookup"><span data-stu-id="0967f-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="0967f-185">Dans l’explorateur de projets d’Eclipse, sélectionnez le projet Maven.</span><span class="sxs-lookup"><span data-stu-id="0967f-185">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="0967f-186">Cliquez sur **Exécuter** > **Exécuter en tant que** > **build Maven**.</span><span class="sxs-lookup"><span data-stu-id="0967f-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Commandes pour exécuter en tant que build Maven][BU01]

1. <span data-ttu-id="0967f-188">Une fois votre application générée, la fenêtre de console affiche l’état.</span><span class="sxs-lookup"><span data-stu-id="0967f-188">When your application is successfully built, the console window shows the status.</span></span>

   ![Build Maven réussie][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="0967f-190">Publier votre application web sur Azure en utilisant un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="0967f-190">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="0967f-191">Dans l’explorateur de projets d’Eclipse, sélectionnez le projet Maven.</span><span class="sxs-lookup"><span data-stu-id="0967f-191">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="0967f-192">Cliquez sur le menu Azure **Publier**, puis sur **Publier en tant que conteneur Docker**.</span><span class="sxs-lookup"><span data-stu-id="0967f-192">Click the Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Commande Publier en tant que conteneur Docker][PU01]

1. <span data-ttu-id="0967f-194">Lorsque la boîte de dialogue **Déploiement de conteneur Docker sur Azure** s’affiche :</span><span class="sxs-lookup"><span data-stu-id="0967f-194">When the **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="0967f-195">a.</span><span class="sxs-lookup"><span data-stu-id="0967f-195">a.</span></span> <span data-ttu-id="0967f-196">Entrez un nom d’image Docker personnalisé.</span><span class="sxs-lookup"><span data-stu-id="0967f-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="0967f-197">b.</span><span class="sxs-lookup"><span data-stu-id="0967f-197">b.</span></span> <span data-ttu-id="0967f-198">Pour **Artefact à déployer**, spécifiez le chemin d’accès au fichier **gs-spring-boot-docker-0.1.0.jar** que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="0967f-198">For **Artifact to deploy**, specify the path to the **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Spécifiez les options Docker][PU02]

   <span data-ttu-id="0967f-200">Tous les hôtes Docker existants s’affichent.</span><span class="sxs-lookup"><span data-stu-id="0967f-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="0967f-201">Si vous choisissez d’effectuer le déploiement sur un hôte existant, vous pouvez passer à l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="0967f-201">If you choose to deploy to an existing host, you can skip to step 5.</span></span> <span data-ttu-id="0967f-202">Autrement, procédez comme suit pour créer un hôte :</span><span class="sxs-lookup"><span data-stu-id="0967f-202">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="0967f-203">a.</span><span class="sxs-lookup"><span data-stu-id="0967f-203">a.</span></span> <span data-ttu-id="0967f-204">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="0967f-204">Click **Add**.</span></span>

      ![Ajouter un nouvel hôte Docker][PU03]

   <span data-ttu-id="0967f-206">b.</span><span class="sxs-lookup"><span data-stu-id="0967f-206">b.</span></span> <span data-ttu-id="0967f-207">Quand la boîte de dialogue **Create Docker Host** (Créer un hôte Docker) apparaît, vous pouvez accepter les valeurs par défaut ou spécifier divers paramètres personnalisés pour votre nouvel hôte Docker</span><span class="sxs-lookup"><span data-stu-id="0967f-207">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="0967f-208">(pour des descriptions détaillées des différents paramètres, voir [Publier une application web en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ][Publish Container with Azure Toolkit]). Cliquez sur **Next** une fois que vous avez spécifié les paramètres à utiliser.</span><span class="sxs-lookup"><span data-stu-id="0967f-208">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Spécifier les options de l’hôte Docker][PU04]

   <span data-ttu-id="0967f-210">c.</span><span class="sxs-lookup"><span data-stu-id="0967f-210">c.</span></span> <span data-ttu-id="0967f-211">Vous pouvez utiliser des identifiants de connexion existants d’un coffre de clés Azure, ou entrer de nouveaux identifiants de connexion Docker.</span><span class="sxs-lookup"><span data-stu-id="0967f-211">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="0967f-212">Cliquez sur **Finish** une fois que vous avez spécifié vos options.</span><span class="sxs-lookup"><span data-stu-id="0967f-212">Click **Finish** when you have specified your options.</span></span>

      ![Spécifier les identifiants de connexion à l’hôte Docker][PU05]

1. <span data-ttu-id="0967f-214">Sélectionnez votre hôte Docker, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="0967f-214">Select your Docker host, and then click **Next**.</span></span>

   ![Sélectionner l’hôte Docker à utiliser][PU06]

1. <span data-ttu-id="0967f-216">Dans la dernière page de la boîte de dialogue **Déploiement de conteneur Docker sur Azure**, vous devez spécifier les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="0967f-216">On the last page of the **Deploying Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="0967f-217">a.</span><span class="sxs-lookup"><span data-stu-id="0967f-217">a.</span></span> <span data-ttu-id="0967f-218">Vous pouvez spécifier un nom personnalisé pour le conteneur qui doit héberger votre conteneur Docker, ou accepter le nom par défaut.</span><span class="sxs-lookup"><span data-stu-id="0967f-218">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="0967f-219">b.</span><span class="sxs-lookup"><span data-stu-id="0967f-219">b.</span></span> <span data-ttu-id="0967f-220">Entrez les ports TCP de votre hôte Docker en utilisant la syntaxe suivante : « *[port externe]*:*[port interne]*.</span><span class="sxs-lookup"><span data-stu-id="0967f-220">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="0967f-221">Par exemple, dans **80:8080**, 80 est un port externe et 8080 le port interne par défaut de Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="0967f-221">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="0967f-222">Si vous avez personnalisé le port interne (par exemple, en modifiant le fichier application.yml), vous devez spécifier le numéro de port pour que le routage dans Azure soit correct.</span><span class="sxs-lookup"><span data-stu-id="0967f-222">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="0967f-223">c.</span><span class="sxs-lookup"><span data-stu-id="0967f-223">c.</span></span> <span data-ttu-id="0967f-224">Après avoir configuré ces options, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="0967f-224">After you configure these options, click **Finish**.</span></span>

   ![Déployer un conteneur Docker dans Azure][PU07]

1. <span data-ttu-id="0967f-226">Une fois que le kit de ressources Azure a terminé la publication, le journal d’activité d’Azure affiche le statut **Publié**.</span><span class="sxs-lookup"><span data-stu-id="0967f-226">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Déploiement réussi de l’hôte Docker][PU08]

## <a name="next-steps"></a><span data-ttu-id="0967f-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0967f-228">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
<span data-ttu-id="0967f-229">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="0967f-229">[Docker]: https://www.docker.com/</span></span>
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
<span data-ttu-id="0967f-230">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="0967f-230">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="0967f-231">[infrastructure Spring]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="0967f-231">[Spring Framework]: https://spring.io/</span></span>

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
