---
title: "aaaGet démarrée avec des applications mobiles à l’aide de Xamarin.Forms"
description: "Suivez ce didacticiel toostart à l’aide des applications mobiles pour le développement de Xamarin.Forms"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="43f8f-103">Créer une application Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="43f8f-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="43f8f-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="43f8f-104">Overview</span></span>
<span data-ttu-id="43f8f-105">Ce didacticiel vous montre comment une application mobile principaux services de cloud computing tooa Xamarin.Forms à l’aide de tooadd hello fonctionnalité des applications mobiles de Service d’applications Azure en tant que serveur principal de hello.</span><span class="sxs-lookup"><span data-stu-id="43f8f-105">This tutorial shows you how tooadd a cloud-based back-end service tooa Xamarin.Forms mobile app by using hello Mobile Apps feature of Azure App Service as hello back end.</span></span> <span data-ttu-id="43f8f-106">Vous allez créer un serveur principal d’applications mobiles et une simple application Xamarin.Forms de liste de tâches qui stocke les données d’application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="43f8f-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="43f8f-107">Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels Mobile Apps pour les applications Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="43f8f-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43f8f-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="43f8f-108">Prerequisites</span></span>
<span data-ttu-id="43f8f-109">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="43f8f-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="43f8f-110">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="43f8f-110">An active Azure account.</span></span> <span data-ttu-id="43f8f-111">Si vous n’avez pas un compte, vous pouvez souscrire à la période d’évaluation d’Azure et obtenir des too10 libre les applications mobiles que vous pouvez continuer à utiliser même après la fin de votre version d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="43f8f-111">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="43f8f-112">Pour plus d’informations, consultez la page [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43f8f-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="43f8f-113">Visual Studio avec Xamarin.</span><span class="sxs-lookup"><span data-stu-id="43f8f-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="43f8f-114">Pour plus d’informations, consultez hello [définir configurer et installer Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="43f8f-114">For information, see hello [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="43f8f-115">Un Mac sur lequel sont installés Xcode v7.0 ou version ultérieure et Xamarin Studio Community.</span><span class="sxs-lookup"><span data-stu-id="43f8f-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="43f8f-116">Pour plus d’informations, consultez les articles [Configurer et installer Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) et [Configurer, installer et vérifier pour les utilisateurs de Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="43f8f-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="43f8f-117">Créer un back end Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="43f8f-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="43f8f-118">toocreate mettre fin à un nouveau Mobile Apps précédent, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="43f8f-118">toocreate a new Mobile Apps back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="43f8f-119">Vous avez maintenant configuré un back end Mobile Apps que vos applications client mobiles peuvent utiliser.</span><span class="sxs-lookup"><span data-stu-id="43f8f-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="43f8f-120">Ensuite, télécharger un projet de serveur pour des tâches simples liste principale et publiez-le tooAzure.</span><span class="sxs-lookup"><span data-stu-id="43f8f-120">Next, you download a server project for a simple to-do list back end and then publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="43f8f-121">Configurer le projet de serveur hello</span><span class="sxs-lookup"><span data-stu-id="43f8f-121">Configure hello server project</span></span>

<span data-ttu-id="43f8f-122">toouse de project server tooconfigure hello hello back-end Node.js ou .NET, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="43f8f-122">tooconfigure hello server project toouse either hello Node.js or .NET back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a><span data-ttu-id="43f8f-123">Téléchargez et exécutez la solution de Xamarin.Forms hello</span><span class="sxs-lookup"><span data-stu-id="43f8f-123">Download and run hello Xamarin.Forms solution</span></span>

<span data-ttu-id="43f8f-124">Vous pouvez télécharger la solution hello de deux manières.</span><span class="sxs-lookup"><span data-stu-id="43f8f-124">You can download hello solution in either of two ways.</span></span> <span data-ttu-id="43f8f-125">Téléchargez-le tooa Mac et ouvrez-le dans Xamarin Studio, ou téléchargez-le tooa l’ordinateur Windows et ouvrez-le dans Visual Studio à l’aide d’un Mac en réseau pour la création d’application iOS de hello.</span><span class="sxs-lookup"><span data-stu-id="43f8f-125">Download it tooa Mac and open it in Xamarin Studio, or download it tooa Windows computer and open it in Visual Studio by using a networked Mac for building hello iOS app.</span></span> <span data-ttu-id="43f8f-126">Pour plus d’informations, consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="43f8f-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="43f8f-127">Sur un ordinateur Mac ou Windows, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="43f8f-127">On a Mac or Windows computer, do hello following:</span></span>

1. <span data-ttu-id="43f8f-128">Accédez toohello [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="43f8f-128">Go toohello [Azure portal].</span></span>

2. <span data-ttu-id="43f8f-129">Sur hello **paramètres** panneau pour votre application mobile, sous **Mobile**, sélectionnez **prise en main** > **Xamarin.Forms**.</span><span class="sxs-lookup"><span data-stu-id="43f8f-129">On hello **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="43f8f-130">À l’**étape 3**, sélectionnez **Créer une application**, puis sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="43f8f-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="43f8f-131">Cette action télécharge un projet qui contient une application cliente qui est connecté tooyour des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="43f8f-131">This action downloads a project that contains a client application that's connected tooyour mobile app.</span></span> <span data-ttu-id="43f8f-132">Enregistrer l’ordinateur local du tooyour fichier projet compressée hello et prenez note d’où vous l’enregistrez.</span><span class="sxs-lookup"><span data-stu-id="43f8f-132">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="43f8f-133">Extraire le projet hello que vous avez téléchargé, puis ouvrez-le dans Visual Studio (Windows) ou de Xamarin Studio (Mac).</span><span class="sxs-lookup"><span data-stu-id="43f8f-133">Extract hello project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![Projet extrait dans Xamarin Studio][9]

   ![Projet extrait dans Visual Studio][8]

## <a name="optional-run-hello-ios-project"></a><span data-ttu-id="43f8f-136">(Facultatif) Exécutez le projet iOS de hello</span><span class="sxs-lookup"><span data-stu-id="43f8f-136">(Optional) Run hello iOS project</span></span>
<span data-ttu-id="43f8f-137">Dans cette section, vous exécutez projet d’iOS Xamarin hello pour les appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="43f8f-137">In this section, you run hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="43f8f-138">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="43f8f-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="43f8f-139">Dans Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="43f8f-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="43f8f-140">Projet d’iOS hello d’avec le bouton droit et sélectionnez **définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="43f8f-140">Right-click hello iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="43f8f-141">Sur hello **exécuter** menu, sélectionnez **démarrer le débogage** toobuild hello du projet et démarrer l’application hello dans l’émulateur d’iPhone hello.</span><span class="sxs-lookup"><span data-stu-id="43f8f-141">On hello **Run** menu, select **Start Debugging** toobuild hello project and start hello app in hello iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="43f8f-142">Dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43f8f-142">In Visual Studio</span></span>
1. <span data-ttu-id="43f8f-143">Projet d’iOS hello d’avec le bouton droit et sélectionnez **définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="43f8f-143">Right-click hello iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="43f8f-144">Sur hello **générer** menu, sélectionnez **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="43f8f-144">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="43f8f-145">Bonjour **Configuration Manager** boîte de dialogue, sélectionnez hello **générer** et **déployer** projet iOS toohello suivant de cases à cocher.</span><span class="sxs-lookup"><span data-stu-id="43f8f-145">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello iOS project.</span></span>

4. <span data-ttu-id="43f8f-146">toobuild hello du projet et démarrer l’application hello dans l’émulateur de hello iPhone, sélectionnez hello **F5** clé.</span><span class="sxs-lookup"><span data-stu-id="43f8f-146">toobuild hello project and start hello app in hello iPhone emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="43f8f-147">Si vous avez des problèmes de génération de projet de hello, exécutez hello NuGet package manager et mise à jour toohello version la plus récente des packages de prise en charge de Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="43f8f-147">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="43f8f-148">Projets de démarrage rapide peuvent être lente tooupdate toohello versions les plus récentes.</span><span class="sxs-lookup"><span data-stu-id="43f8f-148">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="43f8f-149">Dans l’application hello, tapez un texte explicite, tel que *Xamarin d’en savoir plus*, et puis sélectionnez hello signe plus (**+**).</span><span class="sxs-lookup"><span data-stu-id="43f8f-149">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="43f8f-150">Cette action envoie un toohello de demande post que nouvelles applications mobiles back-end qui est hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="43f8f-150">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="43f8f-151">Les données à partir de la demande de hello sont insérées dans la table TodoItem de hello.</span><span class="sxs-lookup"><span data-stu-id="43f8f-151">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="43f8f-152">Les éléments qui sont stockés dans la table de hello sont retournés par hello dans les applications mobiles se termine et hello données sont affichées dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="43f8f-152">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="43f8f-153">Vous trouverez le code hello qui accède à vos applications mobiles back-end Bonjour c# TodoItemManager.cs le fichier de projet de bibliothèque de classes portable hello de votre solution.</span><span class="sxs-lookup"><span data-stu-id="43f8f-153">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-android-project"></a><span data-ttu-id="43f8f-154">(Facultatif) Exécutez le projet Android de hello</span><span class="sxs-lookup"><span data-stu-id="43f8f-154">(Optional) Run hello Android project</span></span>
<span data-ttu-id="43f8f-155">Dans cette section, vous exécutez le projet de droid Xamarin hello pour Android.</span><span class="sxs-lookup"><span data-stu-id="43f8f-155">In this section, you run hello Xamarin droid project for Android.</span></span> <span data-ttu-id="43f8f-156">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Android.</span><span class="sxs-lookup"><span data-stu-id="43f8f-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="43f8f-157">Dans Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="43f8f-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="43f8f-158">Les projets Android hello d’avec le bouton droit et sélectionnez **définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="43f8f-158">Right-click hello Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="43f8f-159">toobuild hello du projet et démarrer l’application hello dans un émulateur Android, sur hello **exécuter** menu, sélectionnez **démarrer le débogage**.</span><span class="sxs-lookup"><span data-stu-id="43f8f-159">toobuild hello project and start hello app in an Android emulator, on hello **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="43f8f-160">Dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43f8f-160">In Visual Studio</span></span>

1. <span data-ttu-id="43f8f-161">Projet Android (Droid) de hello d’avec le bouton droit et sélectionnez **définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="43f8f-161">Right-click hello Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="43f8f-162">Sur hello **générer** menu, sélectionnez **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="43f8f-162">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="43f8f-163">Bonjour **Configuration Manager** boîte de dialogue, sélectionnez hello **générer** et **déployer** prochain projet de Android toohello cases à cocher.</span><span class="sxs-lookup"><span data-stu-id="43f8f-163">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Android project.</span></span>

4. <span data-ttu-id="43f8f-164">toobuild hello du projet et démarrer l’application hello dans un émulateur Android, sélectionnez hello **F5** clé.</span><span class="sxs-lookup"><span data-stu-id="43f8f-164">toobuild hello project and start hello app in an Android emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="43f8f-165">Si vous avez des problèmes de génération de projet de hello, exécutez hello NuGet package manager et mise à jour toohello version la plus récente des packages de prise en charge de Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="43f8f-165">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="43f8f-166">Projets de démarrage rapide peuvent être lente tooupdate toohello versions les plus récentes.</span><span class="sxs-lookup"><span data-stu-id="43f8f-166">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="43f8f-167">Dans l’application hello, tapez un texte explicite, tel que *Xamarin d’en savoir plus*, et puis sélectionnez hello signe plus (**+**).</span><span class="sxs-lookup"><span data-stu-id="43f8f-167">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="43f8f-168">Cette action envoie un toohello de demande post que nouvelles applications mobiles back-end qui est hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="43f8f-168">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="43f8f-169">Les données à partir de la demande de hello sont insérées dans la table TodoItem de hello.</span><span class="sxs-lookup"><span data-stu-id="43f8f-169">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="43f8f-170">Les éléments qui sont stockés dans la table de hello sont retournés par hello dans les applications mobiles se termine et hello données sont affichées dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="43f8f-170">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="43f8f-171">Vous trouverez le code hello qui accède à vos applications mobiles back-end Bonjour c# TodoItemManager.cs le fichier de projet de bibliothèque de classes portable hello de votre solution.</span><span class="sxs-lookup"><span data-stu-id="43f8f-171">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-windows-project"></a><span data-ttu-id="43f8f-172">(Facultatif) Exécutez le projet d’application Windows hello</span><span class="sxs-lookup"><span data-stu-id="43f8f-172">(Optional) Run hello Windows project</span></span>

<span data-ttu-id="43f8f-173">Dans cette section, vous exécutez hello projet Xamarin WinApp pour les appareils Windows.</span><span class="sxs-lookup"><span data-stu-id="43f8f-173">In this section, you run hello Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="43f8f-174">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Windows.</span><span class="sxs-lookup"><span data-stu-id="43f8f-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="43f8f-175">Dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43f8f-175">In Visual Studio</span></span>

1. <span data-ttu-id="43f8f-176">Cliquez sur un des projets d’application Windows hello et sélectionnez **définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="43f8f-176">Right-click any of hello Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="43f8f-177">Sur hello **générer** menu, sélectionnez **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="43f8f-177">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="43f8f-178">Bonjour **Configuration Manager** boîte de dialogue, sélectionnez hello **générer** et **déployer** cases à cocher prochain toohello Windows projet que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="43f8f-178">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Windows project that you chose.</span></span>

4. <span data-ttu-id="43f8f-179">toobuild hello du projet et démarrer l’application hello dans un émulateur de Windows, sélectionnez hello **F5** clé.</span><span class="sxs-lookup"><span data-stu-id="43f8f-179">toobuild hello project and start hello app in a Windows emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="43f8f-180">Si vous avez des problèmes de génération de projet de hello, exécutez hello NuGet package manager et mise à jour toohello version la plus récente des packages de prise en charge de Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="43f8f-180">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="43f8f-181">Projets de démarrage rapide peuvent être lente tooupdate toohello versions les plus récentes.</span><span class="sxs-lookup"><span data-stu-id="43f8f-181">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="43f8f-182">Dans l’application hello, tapez un texte explicite, tel que *Xamarin d’en savoir plus*, et puis sélectionnez hello signe plus (**+**).</span><span class="sxs-lookup"><span data-stu-id="43f8f-182">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    <span data-ttu-id="43f8f-183">Cette action envoie un toohello de demande post que nouvelles applications mobiles back-end qui est hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="43f8f-183">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="43f8f-184">Les données à partir de la demande de hello sont insérées dans la table TodoItem de hello.</span><span class="sxs-lookup"><span data-stu-id="43f8f-184">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="43f8f-185">Les éléments qui sont stockés dans la table de hello sont retournés par hello dans les applications mobiles se termine et hello données sont affichées dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="43f8f-185">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="43f8f-186">Vous trouverez le code hello qui accède à vos applications mobiles back-end Bonjour c# TodoItemManager.cs le fichier de projet de bibliothèque de classes portable hello de votre solution.</span><span class="sxs-lookup"><span data-stu-id="43f8f-186">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="43f8f-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="43f8f-187">Next steps</span></span>

* [<span data-ttu-id="43f8f-188">Ajouter une application de tooyour d’authentification</span><span class="sxs-lookup"><span data-stu-id="43f8f-188">Add authentication tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="43f8f-189">Découvrez comment tooauthenticate les utilisateurs de votre application avec un fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="43f8f-189">Learn how tooauthenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="43f8f-190">Ajouter une application de tooyour de notifications push</span><span class="sxs-lookup"><span data-stu-id="43f8f-190">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="43f8f-191">Découvrez comment les notifications push tooadd prennent en charge tooyour application et configurer vos applications mobiles back-end toouse Azure Notification Hubs toosend hello des notifications push.</span><span class="sxs-lookup"><span data-stu-id="43f8f-191">Learn how tooadd push notifications support tooyour app and configure your Mobile Apps back end toouse Azure Notification Hubs toosend hello push notifications.</span></span>

* [<span data-ttu-id="43f8f-192">Activer la synchronisation hors connexion pour votre application</span><span class="sxs-lookup"><span data-stu-id="43f8f-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="43f8f-193">Découvrez comment tooadd la prise en charge en mode hors connexion pour votre application à l’aide d’un Mobile Apps back-end.</span><span class="sxs-lookup"><span data-stu-id="43f8f-193">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="43f8f-194">La synchronisation hors connexion permet d’afficher, d’ajouter ou de modifier les données d’une application mobile même en l’absence de connexion au réseau.</span><span class="sxs-lookup"><span data-stu-id="43f8f-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="43f8f-195">Utiliser les clients gérés hello pour les applications mobiles</span><span class="sxs-lookup"><span data-stu-id="43f8f-195">Use hello managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="43f8f-196">Découvrez comment toowork avec hello gérées client SDK dans votre application Xamarin.</span><span class="sxs-lookup"><span data-stu-id="43f8f-196">Learn how toowork with hello managed client SDK in your Xamarin app.</span></span>

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[portail Azure]: https://portal.azure.com/
