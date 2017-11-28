---
title: "Créer une application web Azure de base à l’aide dans IntelliJ | Microsoft Docs"
description: "Ce didacticiel vous montre comment utiliser le Kit de ressources Azure pour IntelliJ pour créer une application web Hello World pour Azure."
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 20b2c3d86f5bde9302647f345aa99b030d78613a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="180a9-103">Créer une application web Azure de base à l’aide dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="180a9-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="180a9-104">Ce didacticiel explique comment créer une application Hello World de base et la déployer sur Azure en tant qu’application web à l’aide du [kit de ressources Azure pour IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="180a9-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="180a9-105">Un exemple JSP de base est présenté par souci de simplicité, mais des étapes similaires conviennent également pour un servlet Java en ce qui concerne le déploiement d’Azure.</span><span class="sxs-lookup"><span data-stu-id="180a9-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="180a9-106">À la fin de ce didacticiel, votre application ressemble à l’illustration suivante quand vous l’affichez dans un navigateur web :</span><span class="sxs-lookup"><span data-stu-id="180a9-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Exemple de page web][01]

## <a name="prerequisites"></a><span data-ttu-id="180a9-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="180a9-108">Prerequisites</span></span>
* <span data-ttu-id="180a9-109">JDK (Java Development Kit) version 1.8 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="180a9-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="180a9-110">IntelliJ IDEA édition Ultimate.</span><span class="sxs-lookup"><span data-stu-id="180a9-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="180a9-111">Il peut être téléchargé à partir du site <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="180a9-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="180a9-112">Une distribution d’un serveur web ou d’un serveur d’applications basé sur Java, comme [Apache Tomcat] ou [Jetty].</span><span class="sxs-lookup"><span data-stu-id="180a9-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="180a9-113">Un abonnement Azure, qui peut être obtenu à l’adresse <https://azure.microsoft.com/free/> ou <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="180a9-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="180a9-114">Le [kit de ressources Azure pour IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="180a9-114">The [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="180a9-115">Pour plus d’informations sur l’installation du kit de ressources Azure, consultez [Installation du kit de ressources Azure pour IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="180a9-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ].</span></span>

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="180a9-116">Pour créer une application Hello World</span><span class="sxs-lookup"><span data-stu-id="180a9-116">To create a Hello World application</span></span>
<span data-ttu-id="180a9-117">Tout d’abord, nous allons commencer par créer un projet Java.</span><span class="sxs-lookup"><span data-stu-id="180a9-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="180a9-118">Démarrez IntelliJ, puis dans la barre de menus, cliquez sur **Fichier**, **Nouveau**, puis cliquez sur **Project** (Projet).</span><span class="sxs-lookup"><span data-stu-id="180a9-118">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![Fichier Nouveau Projet][02]
2. <span data-ttu-id="180a9-120">Dans la boîte de dialogue New Project (Nouveau projet), sélectionnez **Java**, puis **Web Application** (Application web), puis cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="180a9-120">In the New Project dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
    ![Boîte de dialogue Nouveau projet][03a]
   
3. <span data-ttu-id="180a9-122">Dans Sélection du répertoire de base pour la boîte de dialogue JDK, sélectionnez le dossier où est installé votre JDK, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="180a9-122">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="180a9-123">Cliquez sur **Suivant** dans la boîte de dialogue Nouveau projet pour continuer.</span><span class="sxs-lookup"><span data-stu-id="180a9-123">Click **Next** in the New Project dialog box to continue.</span></span>
   
    ![Spécifiez le répertoire de base du JDK][03b]
4. <span data-ttu-id="180a9-125">Pour les besoins de ce didacticiel, nommez le projet **Java-Web-App-On-Azure**, puis cliquez sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="180a9-125">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Boîte de dialogue Nouveau projet][04]
5. <span data-ttu-id="180a9-127">Dans l’affichage de l’explorateur de projets d’IntelliJ, développez **Java-Web-App-On-Azure**, puis développez **web** et double-cliquez sur **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="180a9-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Page Ouvrir l’index][05c]
6. <span data-ttu-id="180a9-129">Quand votre fichier index.jsp s’ouvre dans IntelliJ, ajoutez un texte pour afficher dynamiquement **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="180a9-129">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="180a9-130">dans l’élément `<body>` existant.</span><span class="sxs-lookup"><span data-stu-id="180a9-130">within the existing `<body>` element.</span></span> <span data-ttu-id="180a9-131">Le contenu `<body>` mis à jour doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="180a9-131">Your updated `<body>` content should resemble the following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="180a9-132">Enregistrez index.jsp.</span><span class="sxs-lookup"><span data-stu-id="180a9-132">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="180a9-133">Pour déployer votre application sur un conteneur d’application web Azure</span><span class="sxs-lookup"><span data-stu-id="180a9-133">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="180a9-134">Vous pouvez déployer une application web Java sur Azure de plusieurs façons.</span><span class="sxs-lookup"><span data-stu-id="180a9-134">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="180a9-135">Ce didacticiel décrit l’une des plus simples : votre application est déployée sur un conteneur d’application web Azure ; ainsi, aucun type de projet spécifique ni outil supplémentaire n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="180a9-135">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="180a9-136">Le JDK et le logiciel du conteneur web vous étant fournis par Azure, vous n’avez pas besoin de charger les vôtres ; vous devez uniquement être en possession de votre application web Java.</span><span class="sxs-lookup"><span data-stu-id="180a9-136">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="180a9-137">Ainsi, le processus de publication de votre application ne prend que quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="180a9-137">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="180a9-138">Avant de publier votre application, vous devez d’abord configurer vos paramètres de module.</span><span class="sxs-lookup"><span data-stu-id="180a9-138">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="180a9-139">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="180a9-139">To do so, use the following steps:</span></span>

1. <span data-ttu-id="180a9-140">Dans l’explorateur de projets d’IntelliJ, cliquez avec le bouton droit sur le projet **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="180a9-140">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="180a9-141">Quand le menu contextuel s’affiche, cliquez sur **Open Module Settings**(Ouvrir les paramètres du module).</span><span class="sxs-lookup"><span data-stu-id="180a9-141">When the context menu appears, click **Open Module Settings**.</span></span>

    ![Ouvrir les paramètres du module][05a]
2. <span data-ttu-id="180a9-143">Lorsque la boîte de dialogue Structure de projet s’affiche :</span><span class="sxs-lookup"><span data-stu-id="180a9-143">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="180a9-144">a.</span><span class="sxs-lookup"><span data-stu-id="180a9-144">a.</span></span> <span data-ttu-id="180a9-145">Cliquez sur **Artefacts** dans la liste des **Paramètres du projet**.</span><span class="sxs-lookup"><span data-stu-id="180a9-145">Click **Artifacts** in the list of **Project Settings**.</span></span>
   <span data-ttu-id="180a9-146">b.</span><span class="sxs-lookup"><span data-stu-id="180a9-146">b.</span></span> <span data-ttu-id="180a9-147">Modifiez le nom de l’artefact dans la zone **Nom** pour qu’il ne contienne pas d’espaces blancs ou des caractères spéciaux. Cela est nécessaire dans la mesure où le nom est utilisé dans l’URI.</span><span class="sxs-lookup"><span data-stu-id="180a9-147">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="180a9-148">c.</span><span class="sxs-lookup"><span data-stu-id="180a9-148">c.</span></span> <span data-ttu-id="180a9-149">Définissez le **Type** sur **Web Application: Archive** (Application Web : Archive).</span><span class="sxs-lookup"><span data-stu-id="180a9-149">Change the **Type** to **Web Application: Archive**.</span></span>
   <span data-ttu-id="180a9-150">d.</span><span class="sxs-lookup"><span data-stu-id="180a9-150">d.</span></span> <span data-ttu-id="180a9-151">Cliquez sur **OK** pour fermer la boîte de dialogue Structure de projet.</span><span class="sxs-lookup"><span data-stu-id="180a9-151">Click **OK** to close the Project Structure dialog box.</span></span>

    ![Ouvrir les paramètres du module][05b]

<span data-ttu-id="180a9-153">Lorsque vous avez configuré vos paramètres de module, vous pouvez publier votre application dans Azure à l’aide de la procédure suivante :</span><span class="sxs-lookup"><span data-stu-id="180a9-153">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="180a9-154">Dans l’explorateur de projets d’IntelliJ, cliquez avec le bouton droit sur le projet **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="180a9-154">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="180a9-155">Quand le menu contextuel apparaît, sélectionnez **Azure**, puis cliquez sur **Publish as Azure Web App...** (Publier comme application web Azure...).</span><span class="sxs-lookup"><span data-stu-id="180a9-155">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Menu contextuel de publication Azure][06]
2. <span data-ttu-id="180a9-157">Si vous n’êtes pas encore connecté à Azure à partir d’IntelliJ, vous êtes invité à vous connecter à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="180a9-157">If you have not already signed into Azure from IntelliJ, you will be prompted to sign into your Azure account.</span></span> <span data-ttu-id="180a9-158">Si vous avez plusieurs comptes Azure, certaines des invites du processus de connexion peuvent s’afficher plusieurs fois, même si elles semblent être identiques.</span><span class="sxs-lookup"><span data-stu-id="180a9-158">(If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="180a9-159">Dans ce cas, continuez à suivre les instructions de connexion.</span><span class="sxs-lookup"><span data-stu-id="180a9-159">When this happens, continue to follow the sign in instructions.)</span></span>
   
    ![Boîte de dialogue de connexion à Azure][07]
3. <span data-ttu-id="180a9-161">Une fois que vous êtes connecté à votre compte Azure, la boîte de dialogue **Gérer les abonnements** affiche la liste des abonnements associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="180a9-161">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="180a9-162">Si plusieurs abonnements sont répertoriés et que vous ne souhaitez utiliser qu’une partie d’entre eux, vous pouvez éventuellement désélectionner ceux qui ne vous intéressent pas. Quand vous avez sélectionné vos abonnements, cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="180a9-162">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Gérer les abonnements][08]
4. <span data-ttu-id="180a9-164">Quand la boîte de dialogue **Deploy to Azure Web App Container** (Déployer sur le conteneur d’application web Azure) s’affiche, elle présente tous les conteneurs d’application web déjà créés ; si vous n’avez pas créé de conteneur, la liste est vide.</span><span class="sxs-lookup"><span data-stu-id="180a9-164">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
    ![Conteneurs d’applications][09]
5. <span data-ttu-id="180a9-166">Si vous n’avez pas déjà créé de conteneur d’application web Azure ou que vous souhaitez publier votre application dans un nouveau conteneur, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="180a9-166">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="180a9-167">Sinon, sélectionnez un conteneur d’application web existant et passez à l’étape 6 ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="180a9-167">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   1. <span data-ttu-id="180a9-168">Cliquez sur **+**</span><span class="sxs-lookup"><span data-stu-id="180a9-168">Click **+**</span></span>
      
       ![Ajouter un conteneur d’application][10]
   2. <span data-ttu-id="180a9-170">La boîte de dialogue **New Web App Container** (Nouveau conteneur d’application web) s’affiche, que nous allons utiliser au cours des prochaines étapes.</span><span class="sxs-lookup"><span data-stu-id="180a9-170">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
       ![Nouveau conteneur d’application][11a]
   3. <span data-ttu-id="180a9-172">Entrez un **nom DNS** pour votre conteneur d’application web ; celui-ci constitue le nom DNS feuille de l’URL hôte de votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="180a9-172">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="180a9-173">Le nom doit être disponible et conforme aux exigences d’affectation de noms pour les applications web Azure.</span><span class="sxs-lookup"><span data-stu-id="180a9-173">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>
   4. <span data-ttu-id="180a9-174">Dans le menu déroulant **Web Container** (Conteneur d’application), sélectionnez le logiciel approprié pour votre application.</span><span class="sxs-lookup"><span data-stu-id="180a9-174">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
       <span data-ttu-id="180a9-175">Pour le moment, vous pouvez choisir entre Tomcat 8, Tomcat 7 ou Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="180a9-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="180a9-176">Une distribution récente du logiciel sélectionné sera fournie par Azure, et il s’exécutera sur une distribution récente de JDK 8 créée par Oracle et fournie par Azure.</span><span class="sxs-lookup"><span data-stu-id="180a9-176">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="180a9-177">Dans le menu déroulant **Subscription** (Abonnement), sélectionnez l’abonnement à utiliser pour ce déploiement.</span><span class="sxs-lookup"><span data-stu-id="180a9-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>
   6. <span data-ttu-id="180a9-178">Dans le menu déroulant **Resource Group** (Groupe de ressources), sélectionnez le groupe de ressources auquel vous souhaitez associer votre application web.</span><span class="sxs-lookup"><span data-stu-id="180a9-178">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="180a9-179">(Les groupes de ressources Azure permettent de regrouper les ressources associées afin de pouvoir, par exemple, les supprimer simultanément.)</span><span class="sxs-lookup"><span data-stu-id="180a9-179">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="180a9-180">Vous pouvez sélectionner un groupe de ressources existant (le cas échéant) et passer directement à l’étape G ou suivre les étapes ci-dessous pour créer un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="180a9-180">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="180a9-181">Sélectionnez **&lt;&lt; Créer un groupe de ressources &gt;&gt;** dans le menu déroulant **Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="180a9-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="180a9-182">La boîte de dialogue **New Resource Group** (Nouveau groupe de ressources) s’affiche :</span><span class="sxs-lookup"><span data-stu-id="180a9-182">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Nouveau groupe de ressources][12]
      * <span data-ttu-id="180a9-184">Dans la zone de texte **Name** (Nom), spécifiez un nom pour votre nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="180a9-184">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="180a9-185">Dans le menu déroulant **Region** (Région), sélectionnez l’emplacement de centre de données Azure approprié pour votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="180a9-185">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="180a9-186">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="180a9-186">Click **OK**.</span></span>
   7. <span data-ttu-id="180a9-187">Le menu déroulant **App Service Plan** (Plan de Service d’application) répertorie les plans de service d’application qui sont associés au groupe de ressources que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="180a9-187">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="180a9-188">(Un plan App Service spécifie des informations telles que l’emplacement de votre application web, le niveau tarifaire et la taille d’instance de calcul.)</span><span class="sxs-lookup"><span data-stu-id="180a9-188">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="180a9-189">Un seul plan App Service peut être utilisé pour plusieurs Web Apps. Pour cette raison, il est stocké séparément d’un déploiement d’application web spécifique.)</span><span class="sxs-lookup"><span data-stu-id="180a9-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="180a9-190">Vous pouvez sélectionner un plan App Services existant (le cas échéant) et passer directement à l’étape H ou suivre les étapes ci-dessous pour créer un plan App Service :</span><span class="sxs-lookup"><span data-stu-id="180a9-190">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="180a9-191">Sélectionnez **&lt;&lt; Créer un plan App Service&gt;&gt;** dans le menu déroulant **Plan App Service**.</span><span class="sxs-lookup"><span data-stu-id="180a9-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="180a9-192">La boîte de dialogue **New App Service Plan** (Nouveau plan de Service d’application) s’affiche :</span><span class="sxs-lookup"><span data-stu-id="180a9-192">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Nouveau plan App Service][13]
      * <span data-ttu-id="180a9-194">Dans la zone de texte **Name** (Nom), spécifiez un nom pour votre nouveau plan de service d’application.</span><span class="sxs-lookup"><span data-stu-id="180a9-194">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="180a9-195">Dans le menu déroulant **Location** (Emplacement), sélectionnez l’emplacement de centre de données Azure approprié pour le plan.</span><span class="sxs-lookup"><span data-stu-id="180a9-195">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="180a9-196">Dans le menu déroulant **Pricing Tier** (Niveau de tarification), sélectionnez la tarification appropriée pour le plan.</span><span class="sxs-lookup"><span data-stu-id="180a9-196">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="180a9-197">À des fins de test, vous pouvez choisir **Free**(Gratuit).</span><span class="sxs-lookup"><span data-stu-id="180a9-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="180a9-198">Dans le menu déroulant **Instance Size** (Taille de l’instance), sélectionnez la taille d’instance appropriée pour le plan.</span><span class="sxs-lookup"><span data-stu-id="180a9-198">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="180a9-199">À des fins de test, vous pouvez choisir **Small**(Petite).</span><span class="sxs-lookup"><span data-stu-id="180a9-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="180a9-200">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="180a9-200">Click **OK**.</span></span>
   8. <span data-ttu-id="180a9-201">(Facultatif) Par défaut, une distribution récente de Java 8 sera déployée automatiquement par Azure sur votre conteneur d’application web en tant que machine virtuelle Java.</span><span class="sxs-lookup"><span data-stu-id="180a9-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="180a9-202">Vous pouvez cependant sélectionner une version et une distribution de machine virtuelle Java différentes.</span><span class="sxs-lookup"><span data-stu-id="180a9-202">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="180a9-203">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="180a9-203">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="180a9-204">Cliquez sur l’onglet **JDK** dans la boîte de dialogue **New Web App Container** (Nouveau conteneur d’application web).</span><span class="sxs-lookup"><span data-stu-id="180a9-204">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="180a9-205">Vous pouvez choisir l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="180a9-205">You can choose from one of the following options:</span></span>
        
        * <span data-ttu-id="180a9-206">Déployer le JDK proposé par défaut par Azure</span><span class="sxs-lookup"><span data-stu-id="180a9-206">Deploy the default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="180a9-207">Déployer un JDK tiers à partir d’une liste déroulante de JDK supplémentaires disponibles sur Azure</span><span class="sxs-lookup"><span data-stu-id="180a9-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="180a9-208">Déployer un JDK personnalisé, qui doit être empaqueté dans un fichier ZIP et accessible au public ou dans votre compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="180a9-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Onglet JDK du nouveau conteneur d’application][11b]
   9. <span data-ttu-id="180a9-210">Une fois effectuées toutes les étapes ci-dessus, la boîte de dialogue New Web App Container doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="180a9-210">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
       ![Nouveau conteneur d’application][14]
   10. <span data-ttu-id="180a9-212">Cliquez sur **OK** pour terminer la création de votre conteneur d’application web.</span><span class="sxs-lookup"><span data-stu-id="180a9-212">Click **OK** to complete the creation of your new Web App container.</span></span>
       
        <span data-ttu-id="180a9-213">Attendez quelques secondes pour que la liste des conteneurs d’application web s’actualise. Votre conteneur d’application web nouvellement créée doit maintenant être sélectionné dans la liste.</span><span class="sxs-lookup"><span data-stu-id="180a9-213">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>
6. <span data-ttu-id="180a9-214">Vous êtes maintenant prêt à effectuer le déploiement initial de votre application web dans Azure ; cliquez sur **OK** pour déployer votre application Java sur le conteneur d’application web sélectionné.</span><span class="sxs-lookup"><span data-stu-id="180a9-214">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="180a9-215">Par défaut, votre application est déployée en tant que sous-répertoire du serveur d’applications.</span><span class="sxs-lookup"><span data-stu-id="180a9-215">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="180a9-216">Si vous voulez qu’elle soit déployée en tant qu’application racine, cochez la case **Deploy to root** (Déployer sur la racine) avant de cliquer sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="180a9-216">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
    ![Déploiement sur Azure][15]
7. <span data-ttu-id="180a9-218">Ensuite, la vue **Journaux d’activité** doit apparaître et indiquer l’état du déploiement de votre application web.</span><span class="sxs-lookup"><span data-stu-id="180a9-218">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
    ![Indicateur de progression][16]
   
    <span data-ttu-id="180a9-220">Le processus de déploiement de votre application web sur Azure doit prendre seulement quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="180a9-220">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="180a9-221">Quand votre application est prête, un lien nommé **Publié** dans la colonne **État** .</span><span class="sxs-lookup"><span data-stu-id="180a9-221">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="180a9-222">Quand vous cliquez sur le lien, vous êtes redirigé vers la page d’accueil de votre application web déployée, à laquelle vous pouvez accéder en suivant les étapes de la section suivante.</span><span class="sxs-lookup"><span data-stu-id="180a9-222">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="180a9-223">Accès à votre application web sur Azure</span><span class="sxs-lookup"><span data-stu-id="180a9-223">Browsing to your Web App on Azure</span></span>
<span data-ttu-id="180a9-224">Pour accéder à votre application web sur Azure, vous pouvez utiliser la vue **Explorateur Azure**.</span><span class="sxs-lookup"><span data-stu-id="180a9-224">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="180a9-225">Si la vue **Explorateur Azure** n’est pas déjà ouverte, procédez comme suit : dans IntelliJ, cliquez sur le menu **View** (Affichage), sur **Tool Windows** (Fenêtres des outils), puis sur **Service Explorer** (Explorateur de services).</span><span class="sxs-lookup"><span data-stu-id="180a9-225">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="180a9-226">Si vous ne vous êtes pas déjà connecté, vous êtes invité à le faire.</span><span class="sxs-lookup"><span data-stu-id="180a9-226">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="180a9-227">Quand l’**Explorateur Azure** s’affiche, procédez comme suit pour accéder à votre application web :</span><span class="sxs-lookup"><span data-stu-id="180a9-227">When the **Azure Explorer** view is displayed, use follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="180a9-228">Développez le nœud **Azure** .</span><span class="sxs-lookup"><span data-stu-id="180a9-228">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="180a9-229">Développez le nœud **Web Apps** (Applications web).</span><span class="sxs-lookup"><span data-stu-id="180a9-229">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="180a9-230">Cliquez avec le bouton droit sur l’application web souhaitée.</span><span class="sxs-lookup"><span data-stu-id="180a9-230">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="180a9-231">Quand le menu contextuel s’affiche, cliquez sur **Open in Browser**(Ouvrir dans un navigateur).</span><span class="sxs-lookup"><span data-stu-id="180a9-231">When the context menu appears, click **Open in Browser**.</span></span>
   
    ![Parcourir l’application web][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="180a9-233">Mise à jour de votre application web</span><span class="sxs-lookup"><span data-stu-id="180a9-233">Updating your web app</span></span>
<span data-ttu-id="180a9-234">La mise à jour d’une application web Azure existante en cours d’exécution est un processus simple et rapide, que vous pouvez effectuer de deux façons :</span><span class="sxs-lookup"><span data-stu-id="180a9-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="180a9-235">Vous pouvez mettre à jour le déploiement d’une application web Java existante.</span><span class="sxs-lookup"><span data-stu-id="180a9-235">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="180a9-236">Vous pouvez publier une application Java supplémentaire dans le même conteneur d’application web.</span><span class="sxs-lookup"><span data-stu-id="180a9-236">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="180a9-237">Dans les deux cas, le processus est identique et ne prend que quelques secondes :</span><span class="sxs-lookup"><span data-stu-id="180a9-237">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="180a9-238">Dans l’Explorateur de projets IntelliJ, cliquez avec le bouton droit sur l’application Java que vous souhaitez mettre à jour ou ajouter à un conteneur d’application web existant.</span><span class="sxs-lookup"><span data-stu-id="180a9-238">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="180a9-239">Lorsque le menu contextuel s’affiche, sélectionnez **Azure** puis **Publish as Azure Web App...** (Publier en tant qu’application Web Azure...).</span><span class="sxs-lookup"><span data-stu-id="180a9-239">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="180a9-240">Comme vous vous êtes déjà connecté, la liste de vos conteneurs d’application web existants apparaît.</span><span class="sxs-lookup"><span data-stu-id="180a9-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="180a9-241">Sélectionnez celui dans lequel vous souhaitez publier ou republier votre application Java, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="180a9-241">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="180a9-242">Quelques secondes plus tard, le **Journal des activités Azure** affiche votre déploiement mis à jour comme **publié** et êtes en mesure de vérifier votre application mise à jour dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="180a9-242">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="180a9-243">Démarrage, arrêt ou redémarrage d’une application web existante</span><span class="sxs-lookup"><span data-stu-id="180a9-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="180a9-244">Pour démarrer ou arrêter un conteneur d’application web Azure existant (y compris toutes les applications Java déployées dans celui-ci), vous pouvez utiliser la vue **Explorateur Azure** .</span><span class="sxs-lookup"><span data-stu-id="180a9-244">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="180a9-245">Si la vue **Explorateur Azure** n’est pas déjà ouverte, procédez comme suit : dans IntelliJ, cliquez sur le menu **View** (Affichage), sur **Tool Windows** (Fenêtres des outils), puis sur **Service Explorer** (Explorateur de services).</span><span class="sxs-lookup"><span data-stu-id="180a9-245">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="180a9-246">Si vous ne vous êtes pas déjà connecté, vous êtes invité à le faire.</span><span class="sxs-lookup"><span data-stu-id="180a9-246">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="180a9-247">Quand l’ **Explorateur Azure** s’affiche, procédez comme suit pour démarrer ou arrêter votre application web :</span><span class="sxs-lookup"><span data-stu-id="180a9-247">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="180a9-248">Développez le nœud **Azure** .</span><span class="sxs-lookup"><span data-stu-id="180a9-248">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="180a9-249">Développez le nœud **Web Apps** (Applications web).</span><span class="sxs-lookup"><span data-stu-id="180a9-249">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="180a9-250">Cliquez avec le bouton droit sur l’application web souhaitée.</span><span class="sxs-lookup"><span data-stu-id="180a9-250">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="180a9-251">Quand le menu contextuel s’affiche, cliquez sur **Démarrer**, **Arrêter** ou **Redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="180a9-251">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="180a9-252">Les options de menu étant sensibles au contexte, vous pouvez uniquement arrêter une application web en cours d’exécution ou démarrer une application web qui n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="180a9-252">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Arrêter l’application Web][18]

## <a name="next-steps"></a><span data-ttu-id="180a9-254">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="180a9-254">Next Steps</span></span>
<span data-ttu-id="180a9-255">Pour plus d’informations sur les boîtes à outils Azure pour les environnements de développement Java, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="180a9-255">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="180a9-256">[Kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="180a9-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="180a9-257">[Installation du kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="180a9-257">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="180a9-258">[Créer une application web « Hello World » pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="180a9-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="180a9-259">[Nouveautés du kit de ressources Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="180a9-259">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="180a9-260">[kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="180a9-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="180a9-261">[Installation du kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="180a9-261">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="180a9-262">*Créer une application web « Hello World » pour Azure dans IntelliJ (cet article)*</span><span class="sxs-lookup"><span data-stu-id="180a9-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="180a9-263">[Nouveautés du Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="180a9-263">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="180a9-264">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="180a9-264">See Also</span></span>
<span data-ttu-id="180a9-265">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure].</span><span class="sxs-lookup"><span data-stu-id="180a9-265">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="180a9-266">Pour plus d’informations sur la création d’Azure Web Apps, consultez la [Vue d’ensemble de Web Apps].</span><span class="sxs-lookup"><span data-stu-id="180a9-266">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Kit de ressources Azure pour Eclipse]: ../azure-toolkit-for-eclipse.md
[kit de ressources Azure pour IntelliJ]: ../azure-toolkit-for-intellij.md
[Créer une application web « Hello World » pour Azure dans Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Installation du kit de ressources Azure pour Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Installation du kit de ressources Azure pour IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Nouveautés du kit de ressources Azure pour Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Nouveautés du Kit de ressources Azure pour IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/
[Vue d’ensemble de Web Apps]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
