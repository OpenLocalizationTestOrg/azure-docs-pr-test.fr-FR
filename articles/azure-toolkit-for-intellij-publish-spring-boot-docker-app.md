---
title: "une application de démarrage du ressort comme un conteneur Docker à l’aide d’aaaPublish hello boîte à outils Azure pour IntelliJ | Documents Microsoft"
description: "Découvrez comment toopublish un tooMicrosoft d’application web Azure comme un conteneur Docker à l’aide de hello boîte à outils Azure pour IntelliJ."
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
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="859e1-103">Publier une application de démarrage du ressort comme un conteneur Docker à l’aide de hello boîte à outils Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="859e1-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="859e1-104">Hello [Spring Framework] est une solution open source qui permet aux développeurs Java de créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="859e1-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="859e1-105">Un des projets plus-populaires hello qui est créé de plateforme est [ressort démarrage], qui fournit une approche simplifiée pour la création d’applications Java autonome.</span><span class="sxs-lookup"><span data-stu-id="859e1-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="859e1-106">[Docker] est une solution open source qui permet aux développeurs d’automatiser hello déploiement, mise à l’échelle et la gestion de leurs applications qui s’exécutent dans des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="859e1-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="859e1-107">Ce didacticiel vous guide hello étapes toodeploy une application de démarrage du ressort comme un tooMicrosoft du conteneur Docker Azure à l’aide de hello boîte à outils Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="859e1-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a><span data-ttu-id="859e1-108">Cloner hello par défaut ressort démarrage Docker référentiel</span><span class="sxs-lookup"><span data-stu-id="859e1-108">Clone hello default Spring Boot Docker repo</span></span>

<span data-ttu-id="859e1-109">Hello étapes suivantes vous guident le clonage du référentiel du ressort démarrage Docker hello à l’aide de IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="859e1-109">hello following steps walk you through cloning hello Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="859e1-110">Si vous souhaitez toouse une ligne de commande, consultez [déployer une application de démarrage du ressort sur Linux dans le Service de conteneur Azure][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="859e1-110">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="859e1-111">Ouvrez IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="859e1-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="859e1-112">Sur l’écran d’accueil hello, sélectionnez hello **GitHub** option Bonjour **extraire du contrôle de Version** liste.</span><span class="sxs-lookup"><span data-stu-id="859e1-112">On hello welcome screen, select hello **GitHub** option in hello **Check out from Version Control** list.</span></span>

   ![Option GitHub pour le contrôle de version][CL01]

1. <span data-ttu-id="859e1-114">Entrez vos informations d’identification si vous êtes invité à toolog dans.</span><span class="sxs-lookup"><span data-stu-id="859e1-114">Enter your credentials if you are prompted toolog in.</span></span>

   * <span data-ttu-id="859e1-115">Si vous utilisez un nom d’utilisateur/mot de passe toolog dans tooGitHub :</span><span class="sxs-lookup"><span data-stu-id="859e1-115">If you are using a username/password toolog in tooGitHub:</span></span>

      ![Boîte de dialogue pour la saisie du nom d’utilisateur et du mot de passe GitHub][CL02a]

   * <span data-ttu-id="859e1-117">Si vous utilisez un jeton toolog dans tooGitHub :</span><span class="sxs-lookup"><span data-stu-id="859e1-117">If you are using a token toolog in tooGitHub:</span></span>

      ![Boîte de dialogue pour la saisie d’un jeton GitHub][CL02b]

1. <span data-ttu-id="859e1-119">Entrez **https://github.com/spring-guides/gs-spring-boot-docker.git** pour l’URL de référentiel hello, spécifiez le chemin d’accès local et les informations de dossier, puis cliquez sur **Clone**.</span><span class="sxs-lookup"><span data-stu-id="859e1-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for hello repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Boîte de dialogue Cloner le référentiel][CL03]

1. <span data-ttu-id="859e1-121">Lorsque vous êtes invité à entrer toocreate un projet IntelliJ, sélectionnez **non**.</span><span class="sxs-lookup"><span data-stu-id="859e1-121">When you're prompted toocreate an IntelliJ project, select **No**.</span></span>

   ![Refus toocreate un projet IntelliJ][CL04]

1. <span data-ttu-id="859e1-123">Dans la page d’accueil hello, cliquez sur **projet d’importation**.</span><span class="sxs-lookup"><span data-stu-id="859e1-123">On hello welcome page, click **Import Project**.</span></span>

   ![Choix d’importer un projet][CL05]

1. <span data-ttu-id="859e1-125">Localiser hello le chemin où vous avez cloné le dépôt de démarrage du ressort hello, sélectionnez hello **complète** dossier sous la racine de hello, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="859e1-125">Locate hello path where you cloned hello Spring Boot repo, select hello **complete** folder under hello root, and then click **OK**.</span></span>

   ![Sélectionner un dossier pour l’importation][CL06]

1. <span data-ttu-id="859e1-127">Lorsque vous y êtes invité, sélectionnez **Create project from existing sources** (Créer un projet à partir de sources existantes).</span><span class="sxs-lookup"><span data-stu-id="859e1-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Option toocreate un projet à partir de sources existantes][CL07]

1. <span data-ttu-id="859e1-129">Spécifiez le nom de votre projet ou accepter la valeur par défaut de hello, vérifiez toohello de chemin d’accès correct hello **complète** dossier, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="859e1-129">Specify your project name or accept hello default, verify hello correct path toohello **complete** folder, and then click **Next**.</span></span>

   ![Spécifiez le nom du projet hello][CL08]

1. <span data-ttu-id="859e1-131">Personnalisez les répertoires pour l’importation, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="859e1-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Choisir des répertoires][CL09]

1. <span data-ttu-id="859e1-133">Passez en revue les hello bibliothèques tooimport, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="859e1-133">Review hello libraries tooimport, and then click **Next**.</span></span>

   ![Passer en revue les bibliothèques de projet][CL10]

1. <span data-ttu-id="859e1-135">Passez en revue la structure de module hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="859e1-135">Review hello module structure, and then click **Next**.</span></span>

   ![Passer en revue la structure des modules][CL11]

1. <span data-ttu-id="859e1-137">Spécifiez votre JDK, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="859e1-137">Specify your JDK, and then click **Next**.</span></span>

   ![Spécifier un JDK][CL12]

1. <span data-ttu-id="859e1-139">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="859e1-139">Click **Finish**.</span></span>

   ![Bouton Terminer][CL13]

<span data-ttu-id="859e1-141">IntelliJ importe l’application de démarrage du ressort hello en tant que projet et affiche la structure de hello lors de l’importation du hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="859e1-141">IntelliJ imports hello Spring Boot app as a project and displays hello structure when hello import has finished.</span></span>

![Application Spring Boot dans IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="859e1-143">Générer votre application Spring Boot</span><span class="sxs-lookup"><span data-stu-id="859e1-143">Build your Spring Boot app</span></span>

### <a name="build-hello-app-by-using-hello-maven-pom"></a><span data-ttu-id="859e1-144">Générer l’application hello à l’aide de hello POM Maven</span><span class="sxs-lookup"><span data-stu-id="859e1-144">Build hello app by using hello Maven POM</span></span>

1. <span data-ttu-id="859e1-145">Ouvrez la fenêtre d’outil hello Maven s’il n’est pas déjà ouvert.</span><span class="sxs-lookup"><span data-stu-id="859e1-145">Open hello Maven tool window if it is not already opened.</span></span> <span data-ttu-id="859e1-146">Cliquez sur **View (Affichage)** > **Tool Windows (Fenêtre Outil)** > **Maven Projects (Projets Maven)**.</span><span class="sxs-lookup"><span data-stu-id="859e1-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Commandes Fenêtres Outil et Projets Maven][BU01]

1. <span data-ttu-id="859e1-148">Dans la fenêtre outil de Maven hello, cliquez sur **package** et sélectionnez **exécuter la Build Maven**.</span><span class="sxs-lookup"><span data-stu-id="859e1-148">In hello Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="859e1-149">(Si votre projet Maven ne s’affiche pas automatiquement, cliquez sur hello **réimporter** icône sur la barre d’outils de Maven hello.)</span><span class="sxs-lookup"><span data-stu-id="859e1-149">(If your Maven project does not show up automatically, click hello **Reimport** icon on hello Maven toolbar.)</span></span>

   ![Commande Run Maven Build][BU02]

1. <span data-ttu-id="859e1-151">Une fois votre application Spring Boot créée, IntelliJ doit afficher le message **BUILD SUCCESS** (GÉNÉRATION RÉUSSIE).</span><span class="sxs-lookup"><span data-stu-id="859e1-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![Message BUILD SUCCESS][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="859e1-153">Créer un artefact prêt pour le déploiement</span><span class="sxs-lookup"><span data-stu-id="859e1-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="859e1-154">toopublish votre application de démarrage du ressort, vous devez toocreate un artefact prêts pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="859e1-154">toopublish your Spring Boot app, you need toocreate a deployment-ready artifact.</span></span> <span data-ttu-id="859e1-155">Utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="859e1-155">Use hello following steps:</span></span>

1. <span data-ttu-id="859e1-156">Ouvrez votre projet d’application web dans IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="859e1-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="859e1-157">Cliquez sur **File (Fichier)**, puis sur **Project Structure (Structure de projet)**.</span><span class="sxs-lookup"><span data-stu-id="859e1-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Commande Project Structure][ART01]

1. <span data-ttu-id="859e1-159">Cliquez sur hello vert plus (**+**) tooadd un artefact de symboles, cliquez sur **JAR**, puis cliquez sur **vide**.</span><span class="sxs-lookup"><span data-stu-id="859e1-159">Click hello green plus (**+**) symbol tooadd an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Ajouter un artefact][ART02]

1. <span data-ttu-id="859e1-161">Nommez votre artefact en veillant pas tooadd hello extension « .jar », puis spécifiez le dossier cible hello hello Maven de sortie.</span><span class="sxs-lookup"><span data-stu-id="859e1-161">Name your artifact while making sure not tooadd hello ".jar" extension, and then specify hello target folder for hello Maven output.</span></span>

   ![Spécifier les propriétés de l’artefact][ART03]

1. <span data-ttu-id="859e1-163">Créez un manifeste pour votre artefact (facultatif) :</span><span class="sxs-lookup"><span data-stu-id="859e1-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="859e1-164">a.</span><span class="sxs-lookup"><span data-stu-id="859e1-164">a.</span></span> <span data-ttu-id="859e1-165">Cliquez sur **Create Manifest** (Créer un manifeste).</span><span class="sxs-lookup"><span data-stu-id="859e1-165">Click **Create Manifest**.</span></span>

      ![Cliquez sur le bouton de créer un manifeste de hello][ART04a]

   <span data-ttu-id="859e1-167">b.</span><span class="sxs-lookup"><span data-stu-id="859e1-167">b.</span></span> <span data-ttu-id="859e1-168">Choisissez le chemin d’accès par défaut de hello pour l’artefact de hello, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="859e1-168">Choose hello default path for hello artifact, and then click **OK**.</span></span>

      ![Spécifier le chemin de l’artefact][ART04b]

   <span data-ttu-id="859e1-170">c.</span><span class="sxs-lookup"><span data-stu-id="859e1-170">c.</span></span> <span data-ttu-id="859e1-171">Cliquez sur les points de suspension hello (**...** ) classe principale de toolocate hello.</span><span class="sxs-lookup"><span data-stu-id="859e1-171">Click hello ellipsis (**...**) toolocate hello main class.</span></span>

      ![Localiser la classe principale][ART04c]

   <span data-ttu-id="859e1-173">d.</span><span class="sxs-lookup"><span data-stu-id="859e1-173">d.</span></span> <span data-ttu-id="859e1-174">Choisissez votre classe principale, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="859e1-174">Choose your main class, and then click **OK**.</span></span>

      ![Spécifier la classe principale][ART04d]

1. <span data-ttu-id="859e1-176">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="859e1-176">Click **OK**.</span></span>

   ![Fermez la boîte de dialogue de Structure de projet hello][ART05]

> [!NOTE]
> <span data-ttu-id="859e1-178">Pour plus d’informations sur la création des artefacts dans IntelliJ, consultez [configuration des artefacts] sur le site Web de JetBrains hello.</span><span class="sxs-lookup"><span data-stu-id="859e1-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on hello JetBrains website.</span></span>
>

### <a name="build-hello-artifact-for-deployment"></a><span data-ttu-id="859e1-179">Artefact hello pour le déploiement de build</span><span class="sxs-lookup"><span data-stu-id="859e1-179">Build hello artifact for deployment</span></span>

1. <span data-ttu-id="859e1-180">Cliquez sur **Build** (Générer), puis sur **Artifacts** (Artefacts).</span><span class="sxs-lookup"><span data-stu-id="859e1-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Commande Build Artifacts][BU04]

1. <span data-ttu-id="859e1-182">Hello lorsque **générer un artefact** menu contextuel s’affiche, cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="859e1-182">When hello **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Menu contextuel Build Artifact][BU05]

<span data-ttu-id="859e1-184">IntelliJ doit s’afficher artefact hello terminée pour votre application de démarrage du ressort dans la fenêtre outil du projet hello.</span><span class="sxs-lookup"><span data-stu-id="859e1-184">IntelliJ should display hello completed artifact for your Spring Boot app in hello project tool window.</span></span>

   ![Artefact créé][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="859e1-186">Publier votre tooAzure d’application web à l’aide d’un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="859e1-186">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="859e1-187">Si vous n’êtes pas inscrit dans tooyour compte Azure, suivez les étapes de hello dans [instructions d’authentification pour hello boîte à outils Azure pour IntelliJ][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="859e1-187">If you have not signed in tooyour Azure account, follow hello steps in [Sign-in instructions for hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="859e1-188">Dans la fenêtre outil de l’Explorateur de projets hello, cliquez sur le projet de hello et sélectionnez **Azure** > **publier en tant que conteneur Docker**.</span><span class="sxs-lookup"><span data-stu-id="859e1-188">In hello Project Explorer tool window, right-click hello project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Commande Publier en tant que conteneur Docker][PU01]

1. <span data-ttu-id="859e1-190">Hello lorsque **déployer le conteneur Docker sur Azure** boîte de dialogue s’affiche, tous les hôtes Docker existantes sont affichées.</span><span class="sxs-lookup"><span data-stu-id="859e1-190">When hello **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="859e1-191">Si vous choisissez d’hôte de toodeploy tooan existant, vous pouvez ignorer toostep 4.</span><span class="sxs-lookup"><span data-stu-id="859e1-191">If you choose toodeploy tooan existing host, you can skip toostep 4.</span></span> <span data-ttu-id="859e1-192">Sinon, utilisez hello suivant les étapes toocreate un ordinateur hôte :</span><span class="sxs-lookup"><span data-stu-id="859e1-192">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="859e1-193">a.</span><span class="sxs-lookup"><span data-stu-id="859e1-193">a.</span></span> <span data-ttu-id="859e1-194">Cliquez sur hello vert plus (**+**) symbole.</span><span class="sxs-lookup"><span data-stu-id="859e1-194">Click hello green plus (**+**) symbol.</span></span>

      ![Ajouter un nouvel hôte Docker][PU02]

   <span data-ttu-id="859e1-196">b.</span><span class="sxs-lookup"><span data-stu-id="859e1-196">b.</span></span> <span data-ttu-id="859e1-197">Hello lorsque **créer un hôte Docker** boîte de dialogue s’affiche, vous pouvez choisir les valeurs par défaut de tooaccept hello, ou vous pouvez spécifier tous les paramètres personnalisés pour votre nouvel hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="859e1-197">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="859e1-198">(Pour une description détaillée de hello divers paramètres, consultez [publier une application web comme un conteneur Docker à l’aide de hello boîte à outils Azure pour IntelliJ][Publish Container with Azure Toolkit].) Cliquez sur **suivant** lorsque vous avez spécifié le paramètres toouse.</span><span class="sxs-lookup"><span data-stu-id="859e1-198">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Spécifier les options de l’hôte Docker][PU03a]

   <span data-ttu-id="859e1-200">c.</span><span class="sxs-lookup"><span data-stu-id="859e1-200">c.</span></span> <span data-ttu-id="859e1-201">Vous pouvez choisir les informations d’identification de connexion existantes toouse dans un coffre de clés Azure, ou vous pouvez choisir de tooenter de nouvelles informations d’identification de connexion Docker.</span><span class="sxs-lookup"><span data-stu-id="859e1-201">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="859e1-202">Cliquez sur **Finish** une fois que vous avez spécifié vos options.</span><span class="sxs-lookup"><span data-stu-id="859e1-202">Click **Finish** when you have specified your options.</span></span>

      ![Spécifier les identifiants de connexion à l’hôte Docker][PU03b]

1. <span data-ttu-id="859e1-204">Sélectionnez votre hôte Docker, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="859e1-204">Select your Docker host, and then click **Next**.</span></span>

   ![Sélectionnez hello Docker hôte toouse][PU04]

1. <span data-ttu-id="859e1-206">Sur la dernière page de hello Hello **déployer le conteneur Docker sur Azure** boîte de dialogue, spécifiez hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="859e1-206">On hello last page of hello **Deploy Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="859e1-207">a.</span><span class="sxs-lookup"><span data-stu-id="859e1-207">a.</span></span> <span data-ttu-id="859e1-208">Vous pouvez choisir toospecify un nom personnalisé pour le conteneur hello qui hébergera votre conteneur Docker, ou vous pouvez accepter la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="859e1-208">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="859e1-209">b.</span><span class="sxs-lookup"><span data-stu-id="859e1-209">b.</span></span> <span data-ttu-id="859e1-210">Entrez les ports TCP hello pour l’hôte docker à l’aide de la syntaxe de hello : *[port externe]*:*[port interne]*.</span><span class="sxs-lookup"><span data-stu-id="859e1-210">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="859e1-211">Par exemple, **80:8080** spécifie un port externe 80 et le port interne ressort démarrage hello par défaut 8080.</span><span class="sxs-lookup"><span data-stu-id="859e1-211">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="859e1-212">Si vous avez personnalisé votre port interne (par exemple, en modifiant le fichier de application.yml hello), vous devez numéro de port toospecify hello pour hello toooccur de routage correct dans Azure.</span><span class="sxs-lookup"><span data-stu-id="859e1-212">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="859e1-213">c.</span><span class="sxs-lookup"><span data-stu-id="859e1-213">c.</span></span> <span data-ttu-id="859e1-214">Après avoir configuré ces options, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="859e1-214">After you have configured these options, click **Finish**.</span></span>

   ![Déployer un conteneur Docker dans Azure][PU05]

1. <span data-ttu-id="859e1-216">Une fois hello boîte à outils Azure publication, hello affiche du journal des activités Azure **publié** pour l’état de hello.</span><span class="sxs-lookup"><span data-stu-id="859e1-216">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Déploiement réussi de l’hôte Docker][PU06]

## <a name="next-steps"></a><span data-ttu-id="859e1-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="859e1-218">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="859e1-219">toolearn des méthodes supplémentaires pour la création d’applications de démarrage du ressort à l’aide de IntelliJ, consultez [création de projets de démarrage ressort](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) sur le site Web de JetBrains hello.</span><span class="sxs-lookup"><span data-stu-id="859e1-219">toolearn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on hello JetBrains website.</span></span>

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[configuration des artefacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Configuration des artefacts)
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[ressort démarrage]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
