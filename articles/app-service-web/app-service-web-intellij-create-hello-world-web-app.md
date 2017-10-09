---
title: aaaCreate une application web Azure de base dans IntelliJ | Documents Microsoft
description: "Ce didacticiel vous montre comment toouse hello boîte à outils Azure pour IntelliJ toocreate, une application de Web Hello World pour Azure."
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
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="b8adb-103">Créer une application web Azure de base à l’aide dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b8adb-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="b8adb-104">Ce didacticiel montre comment toocreate et déployer une base tooAzure d’application Hello World comme une application Web à l’aide de hello [Azure Toolkit pour IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="b8adb-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="b8adb-105">Un exemple JSP de base est présenté par souci de simplicité, mais des étapes similaires conviennent également pour un servlet Java en ce qui concerne le déploiement d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b8adb-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="b8adb-106">Lorsque vous avez terminé ce didacticiel, votre application doit ressembler similaire toohello suivant illustration lorsque vous l’affichez dans un navigateur web :</span><span class="sxs-lookup"><span data-stu-id="b8adb-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Exemple de page web][01]

## <a name="prerequisites"></a><span data-ttu-id="b8adb-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b8adb-108">Prerequisites</span></span>
* <span data-ttu-id="b8adb-109">JDK (Java Development Kit) version 1.8 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b8adb-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="b8adb-110">IntelliJ IDEA édition Ultimate.</span><span class="sxs-lookup"><span data-stu-id="b8adb-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="b8adb-111">Il peut être téléchargé à partir du site <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="b8adb-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="b8adb-112">Une distribution d’un serveur web ou d’un serveur d’applications basé sur Java, comme [Apache Tomcat] ou [Jetty].</span><span class="sxs-lookup"><span data-stu-id="b8adb-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="b8adb-113">Un abonnement Azure, qui peut être obtenu à l’adresse <https://azure.microsoft.com/free/> ou <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="b8adb-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="b8adb-114">Hello [Azure Toolkit pour IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="b8adb-114">hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="b8adb-115">Pour plus d’informations sur l’installation hello boîte à outils Azure, consultez [installation Bonjour Azure Toolkit pour IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="b8adb-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="b8adb-116">toocreate une application Hello World</span><span class="sxs-lookup"><span data-stu-id="b8adb-116">toocreate a Hello World application</span></span>
<span data-ttu-id="b8adb-117">Tout d’abord, nous allons commencer par créer un projet Java.</span><span class="sxs-lookup"><span data-stu-id="b8adb-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="b8adb-118">Démarrer IntelliJ et cliquez sur hello **fichier** menu, puis cliquez sur **nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-118">Start IntelliJ and click hello **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![Fichier Nouveau Projet][02]
2. <span data-ttu-id="b8adb-120">Dans la boîte de dialogue Nouveau projet hello, sélectionnez **Java**, puis **Application Web**, puis cliquez sur **nouveau** tooadd un kit de développement du projet.</span><span class="sxs-lookup"><span data-stu-id="b8adb-120">In hello New Project dialog box, select **Java**, then **Web Application**, and then click **New** tooadd a Project SDK.</span></span>
   
    ![Boîte de dialogue Nouveau projet][03a]
   
3. <span data-ttu-id="b8adb-122">Bonjour sélectionner le répertoire de base pour la boîte de dialogue JDK, sélectionnez hello dossier où votre JDK est installé, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-122">In hello Select Home Directory for JDK dialog box, select hello folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="b8adb-123">Cliquez sur **suivant** dans toocontinue de boîte de dialogue de nouveau projet hello.</span><span class="sxs-lookup"><span data-stu-id="b8adb-123">Click **Next** in hello New Project dialog box toocontinue.</span></span>
   
    ![Spécifiez le répertoire de base du JDK][03b]
4. <span data-ttu-id="b8adb-125">Pour des raisons de ce didacticiel, nommez le projet de hello **Java application Web sur Azure**, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-125">For purposes of this tutorial, name hello project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Boîte de dialogue Nouveau projet][04]
5. <span data-ttu-id="b8adb-127">Dans l’affichage de l’explorateur de projets d’IntelliJ, développez **Java-Web-App-On-Azure**, puis développez **web** et double-cliquez sur **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Page Ouvrir l’index][05c]
6. <span data-ttu-id="b8adb-129">Lorsque votre fichier index.jsp s’ouvre dans IntelliJ, ajoutez dans l’affichage du texte toodynamically **Hello World !**</span><span class="sxs-lookup"><span data-stu-id="b8adb-129">When your index.jsp file opens in IntelliJ, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="b8adb-130">dans hello existant `<body>` élément.</span><span class="sxs-lookup"><span data-stu-id="b8adb-130">within hello existing `<body>` element.</span></span> <span data-ttu-id="b8adb-131">Votre mise à jour `<body>` contenu doit ressembler à hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b8adb-131">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="b8adb-132">Enregistrez index.jsp.</span><span class="sxs-lookup"><span data-stu-id="b8adb-132">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="b8adb-133">toodeploy votre tooan application conteneur d’application Web Azure</span><span class="sxs-lookup"><span data-stu-id="b8adb-133">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="b8adb-134">Il existe plusieurs façons par lequel vous pouvez déployer un tooAzure d’application web Java.</span><span class="sxs-lookup"><span data-stu-id="b8adb-134">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="b8adb-135">Ce didacticiel décrit l’une de hello plus simple : votre application sera déployée tooan conteneur d’application Web Azure - aucun type de projet spécial ni les outils supplémentaires ne sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="b8adb-135">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="b8adb-136">Hello JDK et hello web conteneur logiciel sera fourni pour vous par Azure, il est donc aucune tooupload besoin de votre propre ; Il vous suffit de votre application de Web Java.</span><span class="sxs-lookup"><span data-stu-id="b8adb-136">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="b8adb-137">Par conséquent, les processus de publication hello pour votre application prendra secondes, pas les minutes.</span><span class="sxs-lookup"><span data-stu-id="b8adb-137">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="b8adb-138">Avant de publier votre application, vous devez tout d’abord tooconfigure vos paramètres de module.</span><span class="sxs-lookup"><span data-stu-id="b8adb-138">Before you publish your application, you first need tooconfigure your module settings.</span></span> <span data-ttu-id="b8adb-139">toodo utilisez donc hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8adb-139">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="b8adb-140">Dans l’Explorateur de projet de IntelliJ, avec le bouton droit hello **Java application Web sur Azure** projet.</span><span class="sxs-lookup"><span data-stu-id="b8adb-140">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="b8adb-141">Lorsque le menu contextuel de hello s’affiche, cliquez sur **ouvrir les paramètres du Module**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-141">When hello context menu appears, click **Open Module Settings**.</span></span>

    ![Ouvrir les paramètres du module][05a]
2. <span data-ttu-id="b8adb-143">Lorsque la boîte de dialogue hello Structure de projet s’affiche :</span><span class="sxs-lookup"><span data-stu-id="b8adb-143">When hello Project Structure dialog box appears:</span></span>

   <span data-ttu-id="b8adb-144">a.</span><span class="sxs-lookup"><span data-stu-id="b8adb-144">a.</span></span> <span data-ttu-id="b8adb-145">Cliquez sur **artefacts** dans la liste des hello **les paramètres de projet**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-145">Click **Artifacts** in hello list of **Project Settings**.</span></span>
   <span data-ttu-id="b8adb-146">b.</span><span class="sxs-lookup"><span data-stu-id="b8adb-146">b.</span></span> <span data-ttu-id="b8adb-147">Modifier le nom hello artefact Bonjour **nom** zone afin qu’il ne contient pas un espace blanc ou des caractères spéciaux ; cela est nécessaire car hello nom sera utilisé dans hello identificateur de ressource uniforme (URI).</span><span class="sxs-lookup"><span data-stu-id="b8adb-147">Change hello artifact name in hello **Name** box so that it doesn't contain whitespace or special characters; this is necessary since hello name will be used in hello Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="b8adb-148">c.</span><span class="sxs-lookup"><span data-stu-id="b8adb-148">c.</span></span> <span data-ttu-id="b8adb-149">Hello de modification **Type** trop**Application Web : Archive**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-149">Change hello **Type** too**Web Application: Archive**.</span></span>
   <span data-ttu-id="b8adb-150">d.</span><span class="sxs-lookup"><span data-stu-id="b8adb-150">d.</span></span> <span data-ttu-id="b8adb-151">Cliquez sur **OK** boîte de dialogue tooclose hello Structure de projet.</span><span class="sxs-lookup"><span data-stu-id="b8adb-151">Click **OK** tooclose hello Project Structure dialog box.</span></span>

    ![Ouvrir les paramètres du module][05b]

<span data-ttu-id="b8adb-153">Lorsque vous avez configuré vos paramètres de module, vous pouvez publier votre tooAzure d’application à l’aide de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8adb-153">When you have configured your module settings, you can publish your application tooAzure by using hello following steps:</span></span>

1. <span data-ttu-id="b8adb-154">Dans l’Explorateur de projet de IntelliJ, avec le bouton droit hello **Java application Web sur Azure** projet.</span><span class="sxs-lookup"><span data-stu-id="b8adb-154">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="b8adb-155">Menu contextuel de hello, sélectionnez **Azure**, puis cliquez sur **publier en tant qu’application Web Azure...**</span><span class="sxs-lookup"><span data-stu-id="b8adb-155">When hello context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Menu contextuel de publication Azure][06]
2. <span data-ttu-id="b8adb-157">Si vous n’êtes pas déjà inscrit dans Azure à partir de IntelliJ, vous serez invité à toosign à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="b8adb-157">If you have not already signed into Azure from IntelliJ, you will be prompted toosign into your Azure account.</span></span> <span data-ttu-id="b8adb-158">(Si vous avez plusieurs comptes Azure, certaines des invites hello pendant le processus de connexion hello peuvent s’afficher plusieurs fois, même si elles apparaissent toobe hello identiques.</span><span class="sxs-lookup"><span data-stu-id="b8adb-158">(If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="b8adb-159">Dans ce cas, continuer toofollow hello signe dans les instructions.)</span><span class="sxs-lookup"><span data-stu-id="b8adb-159">When this happens, continue toofollow hello sign in instructions.)</span></span>
   
    ![Boîte de dialogue de connexion à Azure][07]
3. <span data-ttu-id="b8adb-161">Une fois que vous êtes connecté à votre compte Azure, hello **gérer les abonnements** boîte de dialogue affiche une liste des abonnements qui sont associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="b8adb-161">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="b8adb-162">(S’il existe plusieurs abonnements répertoriés et vous souhaitez toowork avec seulement un sous-ensemble spécifique, vous pouvez désactiver éventuellement abonnements hello vous ne souhaitez pas toouse.) Quand vous avez sélectionné vos abonnements, cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-162">(If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello subscriptions you don't want toouse.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Gérer les abonnements][08]
4. <span data-ttu-id="b8adb-164">Hello lorsque **tooAzure conteneur d’application Web de déployer** boîte de dialogue s’affiche, elle affiche tous les conteneurs de l’application Web que vous avez créé précédemment ; si vous n’avez pas créé tous les conteneurs, liste de hello sera vide.</span><span class="sxs-lookup"><span data-stu-id="b8adb-164">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![Conteneurs d’applications][09]
5. <span data-ttu-id="b8adb-166">Si vous n’avez créé un conteneur d’application Web Azure avant ou si vous souhaitez que toopublish votre conteneur tooa application, utilisez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="b8adb-166">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="b8adb-167">Sinon, sélectionnez un conteneur d’application Web existant et ignorer toostep 6 ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b8adb-167">Otherwise, select an existing Web App Container and skip toostep 6 below.</span></span>
   
   1. <span data-ttu-id="b8adb-168">Cliquez sur **+**</span><span class="sxs-lookup"><span data-stu-id="b8adb-168">Click **+**</span></span>
      
       ![Ajouter un conteneur d’application][10]
   2. <span data-ttu-id="b8adb-170">Hello **nouveau conteneur d’application Web** boîte de dialogue s’affiche, qui sera utilisé pour hello ensuite plusieurs étapes.</span><span class="sxs-lookup"><span data-stu-id="b8adb-170">hello **New Web App Container** dialog box will be displayed, which will be used for hello next several steps.</span></span>
      
       ![Nouveau conteneur d’application][11a]
   3. <span data-ttu-id="b8adb-172">Entrez un **nom DNS** pour votre conteneur d’application Web ; Ceci va former le nom DNS hello feuille de l’URL de l’hôte hello pour votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b8adb-172">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="b8adb-173">Notez ce nom hello doit être disponible et se conformer exigences d’affectation de noms de l’application Web tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b8adb-173">Note that hello name must be available and conform tooAzure Web App naming requirements.</span></span>
   4. <span data-ttu-id="b8adb-174">Bonjour **Web conteneur** menu déroulant, logiciel approprié de hello Sélectionnez pour votre application.</span><span class="sxs-lookup"><span data-stu-id="b8adb-174">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="b8adb-175">Pour le moment, vous pouvez choisir entre Tomcat 8, Tomcat 7 ou Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="b8adb-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="b8adb-176">Une distribution récente du logiciel de hello sélectionné sera fournie par Azure, et elle s’exécute sur une distribution récente de JDK 8 créée par Oracle et fournie par Azure.</span><span class="sxs-lookup"><span data-stu-id="b8adb-176">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="b8adb-177">Bonjour **abonnement** menu déroulant, sélectionnez hello abonnement toouse pour ce déploiement.</span><span class="sxs-lookup"><span data-stu-id="b8adb-177">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="b8adb-178">Bonjour **groupe de ressources** menu déroulant, sélectionnez hello groupe de ressources avec laquelle vous souhaitez tooassociate votre application Web.</span><span class="sxs-lookup"><span data-stu-id="b8adb-178">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="b8adb-179">(Les groupes de Ressources azure permet de vous toogroup les ressources associées ensemble afin que, par exemple, ils peuvent être supprimés ensemble.)</span><span class="sxs-lookup"><span data-stu-id="b8adb-179">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="b8adb-180">Vous pouvez sélectionner un groupe de ressources existant (si vous en avez) et g toostep de skip ci-dessous ou utilisez hello suite étapes toocreate un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="b8adb-180">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="b8adb-181">Sélectionnez  **&lt; &lt; créer le nouveau groupe de ressources &gt; &gt;**  Bonjour **groupe de ressources** menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="b8adb-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in hello **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="b8adb-182">Hello **nouveau groupe de ressources** boîte de dialogue s’affiche :</span><span class="sxs-lookup"><span data-stu-id="b8adb-182">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Nouveau groupe de ressources][12]
      * <span data-ttu-id="b8adb-184">Bonjour de hello **nom** zone de texte, spécifiez un nom pour votre nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b8adb-184">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="b8adb-185">Bonjour de hello **région** menu déroulant, emplacement pour votre groupe de ressources de centre de données Azure approprié de hello select.</span><span class="sxs-lookup"><span data-stu-id="b8adb-185">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="b8adb-186">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-186">Click **OK**.</span></span>
   7. <span data-ttu-id="b8adb-187">Hello **du Plan App Service** menu déroulant répertorie les plans de service d’application hello associés hello groupe de ressources que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="b8adb-187">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="b8adb-188">(Un Plan App Service spécifie les informations comme emplacement de hello de votre application Web, hello niveau tarifaire et taille d’instance de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="b8adb-188">(An App Service Plan specifies information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="b8adb-189">Un seul plan App Service peut être utilisé pour plusieurs Web Apps. Pour cette raison, il est stocké séparément d’un déploiement d’application web spécifique.)</span><span class="sxs-lookup"><span data-stu-id="b8adb-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="b8adb-190">Vous pouvez sélectionner un Plan de Service application existant (si vous en avez) et ignorer h toostep ci-dessous ou utilisez hello suivant toocreate étapes un nouveau Plan App Service :</span><span class="sxs-lookup"><span data-stu-id="b8adb-190">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="b8adb-191">Sélectionnez  **&lt; &lt; créer à nouveau un Plan App Service &gt; &gt;**  Bonjour **du Plan App Service** menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="b8adb-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in hello **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="b8adb-192">Hello **nouveau du Plan App Service** boîte de dialogue s’affiche :</span><span class="sxs-lookup"><span data-stu-id="b8adb-192">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Nouveau plan App Service][13]
      * <span data-ttu-id="b8adb-194">Bonjour de hello **nom** zone de texte, spécifiez un nom pour votre nouveau Plan App Service.</span><span class="sxs-lookup"><span data-stu-id="b8adb-194">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="b8adb-195">Bonjour de hello **emplacement** menu déroulant, emplacement pour le plan de hello centre de données Azure approprié de hello select.</span><span class="sxs-lookup"><span data-stu-id="b8adb-195">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="b8adb-196">Bonjour de hello **niveau tarifaire** menu déroulant, sélectionnez hello approprié de tarification pour le plan de hello.</span><span class="sxs-lookup"><span data-stu-id="b8adb-196">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="b8adb-197">À des fins de test, vous pouvez choisir **Free**(Gratuit).</span><span class="sxs-lookup"><span data-stu-id="b8adb-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="b8adb-198">Bonjour de hello **taille de l’Instance** menu déroulant, taille de l’instance appropriée sélectionnez hello pour le plan de hello.</span><span class="sxs-lookup"><span data-stu-id="b8adb-198">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="b8adb-199">À des fins de test, vous pouvez choisir **Small**(Petite).</span><span class="sxs-lookup"><span data-stu-id="b8adb-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="b8adb-200">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-200">Click **OK**.</span></span>
   8. <span data-ttu-id="b8adb-201">(Facultatif) Par défaut, une distribution récente de Java 8 sera déployée automatiquement en tant que votre machine virtuelle Java par conteneur d’application web Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="b8adb-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure tooyour web app container.</span></span> <span data-ttu-id="b8adb-202">Toutefois, vous pouvez sélectionner une version différente et la distribution de hello JVM.</span><span class="sxs-lookup"><span data-stu-id="b8adb-202">However, you can select a different version and distribution of hello JVM.</span></span> <span data-ttu-id="b8adb-203">toodo utilisez donc hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8adb-203">toodo so, use hello following steps:</span></span>
      
      * <span data-ttu-id="b8adb-204">Cliquez sur hello **JDK** onglet Bonjour **nouveau conteneur d’application Web** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b8adb-204">Click hello **JDK** tab in hello **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="b8adb-205">Vous pouvez choisir une des options suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="b8adb-205">You can choose from one of hello following options:</span></span>
        
        * <span data-ttu-id="b8adb-206">Déployer la valeur par défaut de hello JDK qui est offert par Azure</span><span class="sxs-lookup"><span data-stu-id="b8adb-206">Deploy hello default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="b8adb-207">Déployer un JDK tiers à partir d’une liste déroulante de JDK supplémentaires disponibles sur Azure</span><span class="sxs-lookup"><span data-stu-id="b8adb-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="b8adb-208">Déployer un JDK personnalisé, qui doit être empaqueté dans un fichier ZIP et accessible au public ou dans votre compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="b8adb-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Onglet JDK du nouveau conteneur d’application][11b]
   9. <span data-ttu-id="b8adb-210">Une fois que vous avez effectué toutes les hello étapes ci-dessus, boîte de dialogue nouveau conteneur d’application Web hello doit ressembler à hello après l’illustration :</span><span class="sxs-lookup"><span data-stu-id="b8adb-210">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![Nouveau conteneur d’application][14]
   10. <span data-ttu-id="b8adb-212">Cliquez sur **OK** création de hello toocomplete de votre conteneur d’application Web.</span><span class="sxs-lookup"><span data-stu-id="b8adb-212">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="b8adb-213">Attendez quelques secondes pour la liste de hello Web App conteneurs toobe hello actualisé, et votre conteneur d’application web de nouvellement créé doit maintenant être sélectionné dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="b8adb-213">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
6. <span data-ttu-id="b8adb-214">Vous êtes maintenant déploiement initial de hello prêt toocomplete de tooAzure de votre application Web ; Cliquez sur **OK** toodeploy votre toohello d’application Java sélectionné conteneur de l’application Web.</span><span class="sxs-lookup"><span data-stu-id="b8adb-214">You are now ready toocomplete hello initial deployment of your Web App tooAzure; click **OK** toodeploy your Java application toohello selected Web App container.</span></span> <span data-ttu-id="b8adb-215">Par défaut, votre application sera déployée en tant que sous-répertoire hello du serveur d’applications.</span><span class="sxs-lookup"><span data-stu-id="b8adb-215">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="b8adb-216">Si vous voulez qu’elle toobe déployé en tant qu’application de racine hello, vérifiez hello **déployer tooroot** case à cocher avant de cliquer sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-216">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
   
    ![Déployer tooAzure][15]
7. <span data-ttu-id="b8adb-218">Ensuite, vous devez voir hello **journal des activités Azure** vue, ce qui indique l’état du déploiement de votre application Web hello.</span><span class="sxs-lookup"><span data-stu-id="b8adb-218">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Indicateur de progression][16]
   
    <span data-ttu-id="b8adb-220">Hello du déploiement de votre application Web de tooAzure doit durer quelques secondes seulement toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b8adb-220">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="b8adb-221">Lorsque vous êtes prêt application, vous verrez un lien nommé **publié** Bonjour **état** colonne.</span><span class="sxs-lookup"><span data-stu-id="b8adb-221">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="b8adb-222">Lorsque vous cliquez sur le lien de hello, il vous faudra page d’accueil de l’application Web de tooyour déployé, ou vous pouvez utiliser les étapes de hello Bonjour suivant la section toobrowse tooyour l’application web.</span><span class="sxs-lookup"><span data-stu-id="b8adb-222">When you click hello link, it will take you tooyour deployed Web App's home page, or you can use hello steps in hello following section toobrowse tooyour web app.</span></span>

## <a name="browsing-tooyour-web-app-on-azure"></a><span data-ttu-id="b8adb-223">Navigation tooyour application Web sur Azure</span><span class="sxs-lookup"><span data-stu-id="b8adb-223">Browsing tooyour Web App on Azure</span></span>
<span data-ttu-id="b8adb-224">toobrowse tooyour application Web sur Azure, vous pouvez utiliser hello **Explorateur Azure** vue.</span><span class="sxs-lookup"><span data-stu-id="b8adb-224">toobrowse tooyour Web App on Azure, you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="b8adb-225">Si hello **Explorateur Azure** affichage n’est pas déjà ouvert, vous pouvez l’ouvrir en cliquant sur ensuite **vue** menu IntelliJ, puis cliquez sur **fenêtres Outil**, puis cliquez sur  **Service Explorateur**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-225">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="b8adb-226">Si vous n’avez pas précédemment connecté, il vous invite toodo donc.</span><span class="sxs-lookup"><span data-stu-id="b8adb-226">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="b8adb-227">Hello lorsque **Explorateur Azure** s’affiche, utilisez suivez ces tooyour de toobrowse comme application Web :</span><span class="sxs-lookup"><span data-stu-id="b8adb-227">When hello **Azure Explorer** view is displayed, use follow these steps toobrowse tooyour Web App:</span></span> 

1. <span data-ttu-id="b8adb-228">Développez hello **Azure** nœud.</span><span class="sxs-lookup"><span data-stu-id="b8adb-228">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="b8adb-229">Développez hello **Web Apps** nœud.</span><span class="sxs-lookup"><span data-stu-id="b8adb-229">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="b8adb-230">Avec le bouton hello souhaité application Web.</span><span class="sxs-lookup"><span data-stu-id="b8adb-230">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="b8adb-231">Lorsque le menu contextuel de hello s’affiche, cliquez sur **ouvrir dans le navigateur**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-231">When hello context menu appears, click **Open in Browser**.</span></span>
   
    ![Parcourir l’application web][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="b8adb-233">Mise à jour de votre application web</span><span class="sxs-lookup"><span data-stu-id="b8adb-233">Updating your web app</span></span>
<span data-ttu-id="b8adb-234">La mise à jour d’une application web Azure existante en cours d’exécution est un processus simple et rapide, que vous pouvez effectuer de deux façons :</span><span class="sxs-lookup"><span data-stu-id="b8adb-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="b8adb-235">Vous pouvez mettre à jour le déploiement hello d’une application de Web Java existante.</span><span class="sxs-lookup"><span data-stu-id="b8adb-235">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="b8adb-236">Vous pouvez publier un toohello d’application Java supplémentaire même conteneur d’application Web.</span><span class="sxs-lookup"><span data-stu-id="b8adb-236">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="b8adb-237">Dans les deux cas, les processus hello sont identique et ne prend que quelques secondes :</span><span class="sxs-lookup"><span data-stu-id="b8adb-237">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="b8adb-238">Dans l’Explorateur de projets hello IntelliJ, cliquez sur application Java hello que vous souhaitez tooupdate ou que vous ajoutez tooan existant de conteneur d’application Web.</span><span class="sxs-lookup"><span data-stu-id="b8adb-238">In hello IntelliJ project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="b8adb-239">Menu contextuel de hello, sélectionnez **Azure** , puis **publier en tant qu’application Web Azure...**</span><span class="sxs-lookup"><span data-stu-id="b8adb-239">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="b8adb-240">Comme vous vous êtes déjà connecté, la liste de vos conteneurs d’application web existants apparaît.</span><span class="sxs-lookup"><span data-stu-id="b8adb-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="b8adb-241">Sélectionnez hello un choix toopublish ou de publier votre Java application tooand, cliquez à nouveau **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-241">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="b8adb-242">Quelques secondes plus tard, hello **journal des activités Azure** vue affiche votre déploiement de mises à jour en tant que **publié** et vous sera en mesure de tooverify votre application mis à jour dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="b8adb-242">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="b8adb-243">Démarrage, arrêt ou redémarrage d’une application web existante</span><span class="sxs-lookup"><span data-stu-id="b8adb-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="b8adb-244">toostart ou arrêter un conteneur d’application Web Azure existant, (y compris toutes les applications de Java hello déployé qu’elle contient), vous pouvez utiliser des hello **Explorateur Azure** vue.</span><span class="sxs-lookup"><span data-stu-id="b8adb-244">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="b8adb-245">Si hello **Explorateur Azure** affichage n’est pas déjà ouvert, vous pouvez l’ouvrir en cliquant sur ensuite **vue** menu IntelliJ, puis cliquez sur **fenêtres Outil**, puis cliquez sur  **Service Explorateur**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-245">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="b8adb-246">Si vous n’avez pas précédemment connecté, il vous invite toodo donc.</span><span class="sxs-lookup"><span data-stu-id="b8adb-246">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="b8adb-247">Hello lorsque **Explorateur Azure** s’affiche, utilisez, suivez ces étapes toostart ou arrêter votre application Web :</span><span class="sxs-lookup"><span data-stu-id="b8adb-247">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="b8adb-248">Développez hello **Azure** nœud.</span><span class="sxs-lookup"><span data-stu-id="b8adb-248">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="b8adb-249">Développez hello **Web Apps** nœud.</span><span class="sxs-lookup"><span data-stu-id="b8adb-249">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="b8adb-250">Avec le bouton hello souhaité application Web.</span><span class="sxs-lookup"><span data-stu-id="b8adb-250">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="b8adb-251">Lorsque le menu contextuel de hello s’affiche, cliquez sur **Démarrer**, **arrêter**, ou **redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="b8adb-251">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="b8adb-252">Notez que les options de menu hello sont sensibles au contexte, donc vous pouvez uniquement arrêter une application web en cours d’exécution ou démarrer une application web qui n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b8adb-252">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Arrêter l’application Web][18]

## <a name="next-steps"></a><span data-ttu-id="b8adb-254">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b8adb-254">Next Steps</span></span>
<span data-ttu-id="b8adb-255">Pour plus d’informations sur hello boîtes à outils Azure pour Java IDE, consultez hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="b8adb-255">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="b8adb-256">[boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b8adb-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b8adb-257">[Lors de l’installation hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b8adb-257">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b8adb-258">[Créer une application web « Hello World » pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b8adb-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="b8adb-259">[Nouveautés dans hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b8adb-259">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="b8adb-260">[Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b8adb-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b8adb-261">[installation Bonjour Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b8adb-261">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b8adb-262">*Créer une application web « Hello World » pour Azure dans IntelliJ (cet article)*</span><span class="sxs-lookup"><span data-stu-id="b8adb-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="b8adb-263">[Nouveautés dans hello Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b8adb-263">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="b8adb-264">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b8adb-264">See Also</span></span>
<span data-ttu-id="b8adb-265">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure].</span><span class="sxs-lookup"><span data-stu-id="b8adb-265">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="b8adb-266">Pour plus d’informations sur la création d’applications Web Azure, consultez hello [vue d’ensemble des applications Web].</span><span class="sxs-lookup"><span data-stu-id="b8adb-266">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit pour IntelliJ]: ../azure-toolkit-for-intellij.md
[Créer une application web « Hello World » pour Azure dans Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Lors de l’installation hello boîte à outils Azure pour Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[installation Bonjour Azure Toolkit pour IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Nouveautés dans hello boîte à outils Azure pour Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Nouveautés dans hello Azure Toolkit pour IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[centre de développement Java Azure]: https://azure.microsoft.com/develop/java/
[vue d’ensemble des applications Web]: ./app-service-web-overview.md
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
