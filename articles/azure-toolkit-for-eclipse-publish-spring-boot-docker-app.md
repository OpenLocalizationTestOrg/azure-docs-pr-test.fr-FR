---
title: "une application de démarrage du ressort comme un conteneur Docker à l’aide d’aaaPublish hello boîte à outils Azure pour Eclipse | Documents Microsoft"
description: "Découvrez comment toopublish un tooMicrosoft d’application web Azure comme un conteneur Docker à l’aide de hello boîte à outils Azure pour Eclipse."
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
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="eaa30-103">Publier une application de démarrage du ressort comme un conteneur Docker à l’aide de hello boîte à outils Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="eaa30-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="eaa30-104">Hello [Spring Framework] est une solution open source qui permet aux développeurs Java de créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="eaa30-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="eaa30-105">Un des projets plus-populaires hello qui est créé de plateforme est [ressort démarrage], qui fournit une approche simplifiée pour la création d’applications Java autonome.</span><span class="sxs-lookup"><span data-stu-id="eaa30-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="eaa30-106">[Docker] est une solution open source qui permet aux développeurs d’automatiser hello déploiement, mise à l’échelle et la gestion de leurs applications qui s’exécutent dans des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="eaa30-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="eaa30-107">Ce didacticiel vous guide hello étapes toodeploy une application de démarrage du ressort comme un tooMicrosoft du conteneur Docker Azure à l’aide de hello boîte à outils Azure pour Eclipse.</span><span class="sxs-lookup"><span data-stu-id="eaa30-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a><span data-ttu-id="eaa30-108">Cloner le référentiel de Docker de démarrage ressort hello par défaut</span><span class="sxs-lookup"><span data-stu-id="eaa30-108">Clone hello default Spring Boot Docker repository</span></span>

### <a name="import-hello-public-repository"></a><span data-ttu-id="eaa30-109">Importer un référentiel public hello</span><span class="sxs-lookup"><span data-stu-id="eaa30-109">Import hello public repository</span></span>

<span data-ttu-id="eaa30-110">Hello étapes suivantes vous guident le clonage d’ordinateur local de hello ressort démarrage Docker référentiel tooyour à l’aide de IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="eaa30-110">hello following steps walk you through cloning hello Spring Boot Docker repository tooyour local computer by using IntelliJ.</span></span> <span data-ttu-id="eaa30-111">Si vous souhaitez toouse une ligne de commande, consultez [déployer une application de démarrage du ressort sur Linux dans le Service de conteneur Azure][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="eaa30-111">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="eaa30-112">Ouvrez Eclipse.</span><span class="sxs-lookup"><span data-stu-id="eaa30-112">Open Eclipse.</span></span>

1. <span data-ttu-id="eaa30-113">Cliquez sur **Fichier** > **Importer**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-113">Click **File** > **Import**.</span></span>

   ![Menu Importer fichier][CL01]

1. <span data-ttu-id="eaa30-115">Hello lorsque **importation** ouvre la boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="eaa30-115">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="eaa30-116">a.</span><span class="sxs-lookup"><span data-stu-id="eaa30-116">a.</span></span> <span data-ttu-id="eaa30-117">Développez **Git**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-117">Expand **Git**.</span></span>

   <span data-ttu-id="eaa30-118">b.</span><span class="sxs-lookup"><span data-stu-id="eaa30-118">b.</span></span> <span data-ttu-id="eaa30-119">Sélectionnez **Projets de Git**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="eaa30-120">c.</span><span class="sxs-lookup"><span data-stu-id="eaa30-120">c.</span></span> <span data-ttu-id="eaa30-121">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-121">Click **Next**.</span></span>

   ![Boîte de dialogue Importer][CL02]

1. <span data-ttu-id="eaa30-123">Sur hello **sélectionner une Source de référentiel** page :</span><span class="sxs-lookup"><span data-stu-id="eaa30-123">On hello **Select Repository Source** page:</span></span>

   <span data-ttu-id="eaa30-124">a.</span><span class="sxs-lookup"><span data-stu-id="eaa30-124">a.</span></span> <span data-ttu-id="eaa30-125">Sélectionnez **Cloner l’URI**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="eaa30-126">b.</span><span class="sxs-lookup"><span data-stu-id="eaa30-126">b.</span></span> <span data-ttu-id="eaa30-127">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-127">Click **Next**.</span></span>

   ![Sélectionner la page source du référentiel][CL03]

1. <span data-ttu-id="eaa30-129">Sur hello **référentiel de code Source Git** page :</span><span class="sxs-lookup"><span data-stu-id="eaa30-129">On hello **Source Git Repository** page:</span></span>

   <span data-ttu-id="eaa30-130">a.</span><span class="sxs-lookup"><span data-stu-id="eaa30-130">a.</span></span> <span data-ttu-id="eaa30-131">Pour **URI**, entrez `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span><span class="sxs-lookup"><span data-stu-id="eaa30-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="eaa30-132">Cette étape doit remplir automatiquement hello **hôte** et **chemin d’accès du référentiel** champs avec hello corriger les valeurs.</span><span class="sxs-lookup"><span data-stu-id="eaa30-132">This step should automatically populate hello **Host** and **Repository path** fields with hello correct values.</span></span>
   
   <span data-ttu-id="eaa30-133">b.</span><span class="sxs-lookup"><span data-stu-id="eaa30-133">b.</span></span> <span data-ttu-id="eaa30-134">référentiel de démarrage du ressort Hello est publique, donc vous ne devez pas tooenter votre nom d’utilisateur Git et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="eaa30-134">hello Spring Boot repository is public, so you should not have tooenter your Git username and password.</span></span>
   
   <span data-ttu-id="eaa30-135">c.</span><span class="sxs-lookup"><span data-stu-id="eaa30-135">c.</span></span> <span data-ttu-id="eaa30-136">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-136">Click **Next**.</span></span>

   ![Page du référentiel Git source][CL04]

1. <span data-ttu-id="eaa30-138">Sur hello **sélection de la branche** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-138">On hello **Branch Selection** page, click **Next**.</span></span>

   ![Page Sélection de la branche][CL05]

1. <span data-ttu-id="eaa30-140">Sur hello **Local de Destination** page :</span><span class="sxs-lookup"><span data-stu-id="eaa30-140">On hello **Local Destination** page:</span></span>

   <span data-ttu-id="eaa30-141">a.</span><span class="sxs-lookup"><span data-stu-id="eaa30-141">a.</span></span> <span data-ttu-id="eaa30-142">Spécifiez hello de dossier local où vous souhaitez que votre référentiel local.</span><span class="sxs-lookup"><span data-stu-id="eaa30-142">Specify hello local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="eaa30-143">b.</span><span class="sxs-lookup"><span data-stu-id="eaa30-143">b.</span></span> <span data-ttu-id="eaa30-144">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-144">Click **Next**.</span></span>

   ![Page Destination locale][CL06]

1. <span data-ttu-id="eaa30-146">Sur hello **sélectionner un toouse de l’Assistant pour importer des projets** page :</span><span class="sxs-lookup"><span data-stu-id="eaa30-146">On hello **Select a wizard toouse for importing projects** page:</span></span>

   <span data-ttu-id="eaa30-147">a.</span><span class="sxs-lookup"><span data-stu-id="eaa30-147">a.</span></span> <span data-ttu-id="eaa30-148">Sélectionnez **Importer en tant que projet général**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="eaa30-149">b.</span><span class="sxs-lookup"><span data-stu-id="eaa30-149">b.</span></span> <span data-ttu-id="eaa30-150">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-150">Click **Next**.</span></span>

   ![Page « Sélectionner un toouse de l’Assistant pour importer des projets »][CL07]

1. <span data-ttu-id="eaa30-152">Sur hello **importation projets** page :</span><span class="sxs-lookup"><span data-stu-id="eaa30-152">On hello **Import Projects** page:</span></span>

   <span data-ttu-id="eaa30-153">a.</span><span class="sxs-lookup"><span data-stu-id="eaa30-153">a.</span></span> <span data-ttu-id="eaa30-154">Spécifiez le nom de votre projet.</span><span class="sxs-lookup"><span data-stu-id="eaa30-154">Specify your project name.</span></span>
   
   <span data-ttu-id="eaa30-155">b.</span><span class="sxs-lookup"><span data-stu-id="eaa30-155">b.</span></span> <span data-ttu-id="eaa30-156">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-156">Click **Finish**.</span></span>

   ![Page Importer des projets][CL08]

1. <span data-ttu-id="eaa30-158">Lorsque le référentiel de hello est cloné avec succès, vous voyez tous les fichiers hello répertoriés dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="eaa30-158">When hello repository is cloned successfully, you see all hello files listed in Eclipse.</span></span>

   ![Référentiel local][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="eaa30-160">Créer un projet Maven à partir de votre référentiel local</span><span class="sxs-lookup"><span data-stu-id="eaa30-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="eaa30-161">référentiel du ressort démarrage Docker Hello contient un projet de Maven terminé, vous allez utiliser pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="eaa30-161">hello Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="eaa30-162">Cliquez sur **Fichier** > **Importer**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-162">Click **File** > **Import**.</span></span>

   ![Importer la commande de menu de fichier hello][CL01]

1. <span data-ttu-id="eaa30-164">Hello lorsque **importation** ouvre la boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="eaa30-164">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="eaa30-165">a.</span><span class="sxs-lookup"><span data-stu-id="eaa30-165">a.</span></span> <span data-ttu-id="eaa30-166">Développez **Maven**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="eaa30-167">b.</span><span class="sxs-lookup"><span data-stu-id="eaa30-167">b.</span></span> <span data-ttu-id="eaa30-168">Sélectionnez **Projets Maven existants**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="eaa30-169">c.</span><span class="sxs-lookup"><span data-stu-id="eaa30-169">c.</span></span> <span data-ttu-id="eaa30-170">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-170">Click **Next**.</span></span>

   ![Boîte de dialogue Importer][MV01]

1. <span data-ttu-id="eaa30-172">Sur hello **projets Maven** page :</span><span class="sxs-lookup"><span data-stu-id="eaa30-172">On hello **Maven Projects** page:</span></span>

   <span data-ttu-id="eaa30-173">a.</span><span class="sxs-lookup"><span data-stu-id="eaa30-173">a.</span></span> <span data-ttu-id="eaa30-174">Pour **répertoire racine**, spécifiez hello **complète** dossier dans votre référentiel local.</span><span class="sxs-lookup"><span data-stu-id="eaa30-174">For **Root Directory**, specify hello **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="eaa30-175">b.</span><span class="sxs-lookup"><span data-stu-id="eaa30-175">b.</span></span> <span data-ttu-id="eaa30-176">Développez hello **avancé** section et entrez un nom personnalisé pour **modèle de nom**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-176">Expand hello **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="eaa30-177">c.</span><span class="sxs-lookup"><span data-stu-id="eaa30-177">c.</span></span> <span data-ttu-id="eaa30-178">Boîte de sélection hello hello **pom.xml** fichier de projet de hello.</span><span class="sxs-lookup"><span data-stu-id="eaa30-178">Select hello box for hello **pom.xml** file in hello project.</span></span>
   
   <span data-ttu-id="eaa30-179">d.</span><span class="sxs-lookup"><span data-stu-id="eaa30-179">d.</span></span> <span data-ttu-id="eaa30-180">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-180">Click **Finish**.</span></span>

   ![Page Projets Maven][MV02]

1. <span data-ttu-id="eaa30-182">Lorsque le projet de Maven hello est ouvert avec succès, vous consultez un deuxième projet répertorié dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="eaa30-182">When hello Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Projet Maven local][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="eaa30-184">Générer votre application Spring Boot à l’aide de Maven</span><span class="sxs-lookup"><span data-stu-id="eaa30-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="eaa30-185">Bonjour Explorateur de projets Eclipse, sélectionnez projet de Maven hello.</span><span class="sxs-lookup"><span data-stu-id="eaa30-185">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="eaa30-186">Cliquez sur **Exécuter** > **Exécuter en tant que** > **build Maven**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Toorun de commandes en tant que build Maven][BU01]

1. <span data-ttu-id="eaa30-188">Lorsque votre application est générée avec succès, fenêtre de console hello affiche état de hello.</span><span class="sxs-lookup"><span data-stu-id="eaa30-188">When your application is successfully built, hello console window shows hello status.</span></span>

   ![Build Maven réussie][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="eaa30-190">Publier votre tooAzure d’application web à l’aide d’un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="eaa30-190">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="eaa30-191">Bonjour Explorateur de projets Eclipse, sélectionnez projet de Maven hello.</span><span class="sxs-lookup"><span data-stu-id="eaa30-191">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="eaa30-192">Cliquez sur hello Azure **publier** menu, puis sur **publier en tant que conteneur Docker**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-192">Click hello Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Commande Publier en tant que conteneur Docker][PU01]

1. <span data-ttu-id="eaa30-194">Hello lorsque **déploiement de conteneur Docker sur Azure** boîte de dialogue s’affiche :</span><span class="sxs-lookup"><span data-stu-id="eaa30-194">When hello **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="eaa30-195">a.</span><span class="sxs-lookup"><span data-stu-id="eaa30-195">a.</span></span> <span data-ttu-id="eaa30-196">Entrez un nom d’image Docker personnalisé.</span><span class="sxs-lookup"><span data-stu-id="eaa30-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="eaa30-197">b.</span><span class="sxs-lookup"><span data-stu-id="eaa30-197">b.</span></span> <span data-ttu-id="eaa30-198">Pour **artefact toodeploy**, spécifiez hello chemin d’accès toohello **0.1.0.jar du docker démarrage gs ressort** fichier que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="eaa30-198">For **Artifact toodeploy**, specify hello path toohello **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Spécifiez les options Docker][PU02]

   <span data-ttu-id="eaa30-200">Tous les hôtes Docker existants s’affichent.</span><span class="sxs-lookup"><span data-stu-id="eaa30-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="eaa30-201">Si vous choisissez d’hôte de toodeploy tooan existant, vous pouvez ignorer toostep 5.</span><span class="sxs-lookup"><span data-stu-id="eaa30-201">If you choose toodeploy tooan existing host, you can skip toostep 5.</span></span> <span data-ttu-id="eaa30-202">Sinon, utilisez hello suivant les étapes toocreate un ordinateur hôte :</span><span class="sxs-lookup"><span data-stu-id="eaa30-202">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="eaa30-203">a.</span><span class="sxs-lookup"><span data-stu-id="eaa30-203">a.</span></span> <span data-ttu-id="eaa30-204">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-204">Click **Add**.</span></span>

      ![Ajouter un nouvel hôte Docker][PU03]

   <span data-ttu-id="eaa30-206">b.</span><span class="sxs-lookup"><span data-stu-id="eaa30-206">b.</span></span> <span data-ttu-id="eaa30-207">Hello lorsque **créer un hôte Docker** boîte de dialogue s’affiche, vous pouvez choisir les valeurs par défaut de tooaccept hello, ou vous pouvez spécifier tous les paramètres personnalisés pour votre nouvel hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="eaa30-207">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="eaa30-208">(Pour une description détaillée de hello divers paramètres, consultez [publier une application web comme un conteneur Docker à l’aide de hello boîte à outils Azure pour IntelliJ][Publish Container with Azure Toolkit].) Cliquez sur **suivant** lorsque vous avez spécifié le paramètres toouse.</span><span class="sxs-lookup"><span data-stu-id="eaa30-208">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Spécifier les options de l’hôte Docker][PU04]

   <span data-ttu-id="eaa30-210">c.</span><span class="sxs-lookup"><span data-stu-id="eaa30-210">c.</span></span> <span data-ttu-id="eaa30-211">Vous pouvez choisir les informations d’identification de connexion existantes toouse dans un coffre de clés Azure, ou vous pouvez choisir de tooenter de nouvelles informations d’identification de connexion Docker.</span><span class="sxs-lookup"><span data-stu-id="eaa30-211">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="eaa30-212">Cliquez sur **Finish** une fois que vous avez spécifié vos options.</span><span class="sxs-lookup"><span data-stu-id="eaa30-212">Click **Finish** when you have specified your options.</span></span>

      ![Spécifier les identifiants de connexion à l’hôte Docker][PU05]

1. <span data-ttu-id="eaa30-214">Sélectionnez votre hôte Docker, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-214">Select your Docker host, and then click **Next**.</span></span>

   ![Sélectionnez toouse d’hôte Docker][PU06]

1. <span data-ttu-id="eaa30-216">Sur la dernière page de hello Hello **déploiement de conteneur Docker sur Azure** boîte de dialogue, spécifiez hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="eaa30-216">On hello last page of hello **Deploying Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="eaa30-217">a.</span><span class="sxs-lookup"><span data-stu-id="eaa30-217">a.</span></span> <span data-ttu-id="eaa30-218">Vous pouvez choisir toospecify un nom personnalisé pour le conteneur hello qui hébergera votre conteneur Docker, ou vous pouvez accepter la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="eaa30-218">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="eaa30-219">b.</span><span class="sxs-lookup"><span data-stu-id="eaa30-219">b.</span></span> <span data-ttu-id="eaa30-220">Entrez les ports TCP hello pour l’hôte docker à l’aide de la syntaxe de hello : *[port externe]*:*[port interne]*.</span><span class="sxs-lookup"><span data-stu-id="eaa30-220">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="eaa30-221">Par exemple, **80:8080** spécifie un port externe 80 et le port interne ressort démarrage hello par défaut 8080.</span><span class="sxs-lookup"><span data-stu-id="eaa30-221">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="eaa30-222">Si vous avez personnalisé votre port interne (par exemple, en modifiant le fichier de application.yml hello), vous devez numéro de port toospecify hello pour hello toooccur de routage correct dans Azure.</span><span class="sxs-lookup"><span data-stu-id="eaa30-222">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="eaa30-223">c.</span><span class="sxs-lookup"><span data-stu-id="eaa30-223">c.</span></span> <span data-ttu-id="eaa30-224">Après avoir configuré ces options, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="eaa30-224">After you configure these options, click **Finish**.</span></span>

   ![Déployer un conteneur Docker dans Azure][PU07]

1. <span data-ttu-id="eaa30-226">Une fois hello boîte à outils Azure publication, hello affiche du journal des activités Azure **publié** pour l’état de hello.</span><span class="sxs-lookup"><span data-stu-id="eaa30-226">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Déploiement réussi de l’hôte Docker][PU08]

## <a name="next-steps"></a><span data-ttu-id="eaa30-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eaa30-228">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[ressort démarrage]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

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
