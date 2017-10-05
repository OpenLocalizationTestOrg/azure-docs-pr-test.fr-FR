---
title: "Prise en main de Mobile Apps à l’aide de Xamarin.Forms"
description: "Suivez ce didacticiel pour commencer à utiliser Azure Mobile Apps pour le développement Xamarin.Forms"
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
ms.openlocfilehash: ee12caaad4095cff6dae3282f747ae804f93db81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="0be78-103">Créer une application Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="0be78-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="0be78-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0be78-104">Overview</span></span>
<span data-ttu-id="0be78-105">Ce didacticiel vous montre comment ajouter un service principal cloud à une application Xamarin.Forms en utilisant la fonctionnalité Azure Mobile Apps d’Azure App Service en tant que back end.</span><span class="sxs-lookup"><span data-stu-id="0be78-105">This tutorial shows you how to add a cloud-based back-end service to a Xamarin.Forms mobile app by using the Mobile Apps feature of Azure App Service as the back end.</span></span> <span data-ttu-id="0be78-106">Vous allez créer un serveur principal d’applications mobiles et une simple application Xamarin.Forms de liste de tâches qui stocke les données d’application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0be78-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="0be78-107">Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels Mobile Apps pour les applications Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="0be78-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0be78-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0be78-108">Prerequisites</span></span>
<span data-ttu-id="0be78-109">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0be78-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="0be78-110">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="0be78-110">An active Azure account.</span></span> <span data-ttu-id="0be78-111">Si vous n'avez pas de compte, vous pouvez vous inscrire pour une évaluation d'Azure et obtenir jusqu'à 10 applications mobiles gratuites que vous pourrez conserver après l'expiration de votre période d'évaluation.</span><span class="sxs-lookup"><span data-stu-id="0be78-111">If you don't have an account, you can sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="0be78-112">Pour plus d’informations, consultez la page [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0be78-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="0be78-113">Visual Studio avec Xamarin.</span><span class="sxs-lookup"><span data-stu-id="0be78-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="0be78-114">Pour plus d’informations, consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="0be78-114">For information, see the [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="0be78-115">Un Mac sur lequel sont installés Xcode v7.0 ou version ultérieure et Xamarin Studio Community.</span><span class="sxs-lookup"><span data-stu-id="0be78-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="0be78-116">Pour plus d’informations, consultez les articles [Configurer et installer Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) et [Configurer, installer et vérifier pour les utilisateurs de Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="0be78-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="0be78-117">Créer un back end Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="0be78-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="0be78-118">Pour créer un nouveau back end Mobile Apps, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0be78-118">To create a new Mobile Apps back end, do the following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="0be78-119">Vous avez maintenant configuré un back end Mobile Apps que vos applications client mobiles peuvent utiliser.</span><span class="sxs-lookup"><span data-stu-id="0be78-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="0be78-120">Vous allez ensuite télécharger un projet de serveur pour un simple back end de liste de tâches et le publier dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0be78-120">Next, you download a server project for a simple to-do list back end and then publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="0be78-121">Configurer le projet de serveur</span><span class="sxs-lookup"><span data-stu-id="0be78-121">Configure the server project</span></span>

<span data-ttu-id="0be78-122">Pour configurer le projet de serveur de sorte qu’il utilise le back end Node.js ou .NET, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0be78-122">To configure the server project to use either the Node.js or .NET back end, do the following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinforms-solution"></a><span data-ttu-id="0be78-123">Télécharger et exécuter la solution Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="0be78-123">Download and run the Xamarin.Forms solution</span></span>

<span data-ttu-id="0be78-124">Vous pouvez télécharger la solution de la manière de votre choix.</span><span class="sxs-lookup"><span data-stu-id="0be78-124">You can download the solution in either of two ways.</span></span> <span data-ttu-id="0be78-125">Téléchargez la solution sur un Mac et ouvrez-la dans Xamarin Studio, ou bien téléchargez la solution sur un ordinateur Windows et ouvrez-la dans Visual Studio à l’aide d’un ordinateur Mac connecté au réseau pour la création de l’application iOS.</span><span class="sxs-lookup"><span data-stu-id="0be78-125">Download it to a Mac and open it in Xamarin Studio, or download it to a Windows computer and open it in Visual Studio by using a networked Mac for building the iOS app.</span></span> <span data-ttu-id="0be78-126">Pour plus d’informations, consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="0be78-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="0be78-127">Sur un ordinateur Mac ou Windows, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0be78-127">On a Mac or Windows computer, do the following:</span></span>

1. <span data-ttu-id="0be78-128">Accédez au [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="0be78-128">Go to the [Azure portal].</span></span>

2. <span data-ttu-id="0be78-129">Dans le panneau **Paramètres** de votre application mobile, dans **Mobile**, cliquez sur **Commencer** > **Xamarin.Forms**.</span><span class="sxs-lookup"><span data-stu-id="0be78-129">On the **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="0be78-130">À l’**étape 3**, sélectionnez **Créer une application**, puis sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="0be78-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="0be78-131">Cette action télécharge un projet qui contient une application cliente connectée à votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="0be78-131">This action downloads a project that contains a client application that's connected to your mobile app.</span></span> <span data-ttu-id="0be78-132">Enregistrez le fichier projet compressé sur votre ordinateur local et notez l'emplacement où vous l'avez enregistré.</span><span class="sxs-lookup"><span data-stu-id="0be78-132">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="0be78-133">Extrayez le projet que vous avez téléchargé, puis ouvrez-le dans Xamarin Studio (Mac) ou Visual Studio (Windows).</span><span class="sxs-lookup"><span data-stu-id="0be78-133">Extract the project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![Projet extrait dans Xamarin Studio][9]

   ![Projet extrait dans Visual Studio][8]

## <a name="optional-run-the-ios-project"></a><span data-ttu-id="0be78-136">(Facultatif) Exécuter le projet iOS</span><span class="sxs-lookup"><span data-stu-id="0be78-136">(Optional) Run the iOS project</span></span>
<span data-ttu-id="0be78-137">Dans cette section, vous exécutez le projet iOS Xamarin pour les appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="0be78-137">In this section, you run the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="0be78-138">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="0be78-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="0be78-139">Dans Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="0be78-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="0be78-140">Cliquez avec le bouton droit sur le projet iOS, puis cliquez sur **Définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="0be78-140">Right-click the iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="0be78-141">Dans le menu **Exécuter**, cliquez sur **Démarrer le débogage** pour créer le projet et démarrer l’application dans l’émulateur iPhone.</span><span class="sxs-lookup"><span data-stu-id="0be78-141">On the **Run** menu, select **Start Debugging** to build the project and start the app in the iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="0be78-142">Dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0be78-142">In Visual Studio</span></span>
1. <span data-ttu-id="0be78-143">Cliquez avec le bouton droit sur le projet iOS, puis cliquez sur **Définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="0be78-143">Right-click the iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="0be78-144">Dans le menu **Générer**, cliquez sur **Gestionnaire de configuration**.</span><span class="sxs-lookup"><span data-stu-id="0be78-144">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="0be78-145">Dans la boîte de dialogue **Gestionnaire de configuration**, cochez les cases **Générer** et **Déployer** situées à côté du projet iOS.</span><span class="sxs-lookup"><span data-stu-id="0be78-145">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the iOS project.</span></span>

4. <span data-ttu-id="0be78-146">Pour générer le projet et démarrer l’application dans l’émulateur iPhone, appuyez sur la touche **F5**.</span><span class="sxs-lookup"><span data-stu-id="0be78-146">To build the project and start the app in the iPhone emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0be78-147">Si vous avez des problèmes pour générer le projet, exécutez le gestionnaire de package NuGet et mettez à jour vers la dernière version des packages de support Xamarin.</span><span class="sxs-lookup"><span data-stu-id="0be78-147">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="0be78-148">La mise à jour des dernières versions des projets de démarrage rapide peut être lente.</span><span class="sxs-lookup"><span data-stu-id="0be78-148">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="0be78-149">Dans l’application, tapez un texte explicite, tel que *Découvrir Xamarin*, puis cliquez sur le bouton « + » (**+**).</span><span class="sxs-lookup"><span data-stu-id="0be78-149">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="0be78-150">Cette action envoie une demande post vers le back end Mobile Apps qui est hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0be78-150">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="0be78-151">Les données de la requête sont insérées dans la table TodoItem.</span><span class="sxs-lookup"><span data-stu-id="0be78-151">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="0be78-152">Les éléments stockés dans cette table sont renvoyés par le backend Mobile Apps et les données sont affichées dans la liste.</span><span class="sxs-lookup"><span data-stu-id="0be78-152">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0be78-153">Vous trouverez le code qui vous permet d’accéder à votre back end Mobile Apps dans le fichier C# TodoItemManager.cs du projet de bibliothèque de classes portables de votre solution.</span><span class="sxs-lookup"><span data-stu-id="0be78-153">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-the-android-project"></a><span data-ttu-id="0be78-154">(Facultatif) Exécuter le projet Android</span><span class="sxs-lookup"><span data-stu-id="0be78-154">(Optional) Run the Android project</span></span>
<span data-ttu-id="0be78-155">Dans cette section, vous exécutez le projet droïde Xamarin pour Android.</span><span class="sxs-lookup"><span data-stu-id="0be78-155">In this section, you run the Xamarin droid project for Android.</span></span> <span data-ttu-id="0be78-156">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Android.</span><span class="sxs-lookup"><span data-stu-id="0be78-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="0be78-157">Dans Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="0be78-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="0be78-158">Cliquez avec le bouton droit sur le projet Android, puis cliquez sur **Définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="0be78-158">Right-click the Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="0be78-159">Pour générer le projet et démarrer l’application dans l’émulateur Android, dans le menu **Exécuter**, cliquez sur **Démarrer le débogage**.</span><span class="sxs-lookup"><span data-stu-id="0be78-159">To build the project and start the app in an Android emulator, on the **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="0be78-160">Dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0be78-160">In Visual Studio</span></span>

1. <span data-ttu-id="0be78-161">Cliquez avec le bouton droit sur le projet Android (Droid), puis cliquez sur **Définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="0be78-161">Right-click the Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="0be78-162">Dans le menu **Générer**, cliquez sur **Gestionnaire de configuration**.</span><span class="sxs-lookup"><span data-stu-id="0be78-162">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="0be78-163">Dans la boîte de dialogue **Gestionnaire de configuration**, cochez les cases **Générer** et **Déployer** situées à côté du projet Android.</span><span class="sxs-lookup"><span data-stu-id="0be78-163">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the Android project.</span></span>

4. <span data-ttu-id="0be78-164">Pour générer le projet et démarrer l’application dans l’émulateur Android, appuyez sur la touche **F5**.</span><span class="sxs-lookup"><span data-stu-id="0be78-164">To build the project and start the app in an Android emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0be78-165">Si vous avez des problèmes pour générer le projet, exécutez le gestionnaire de package NuGet et mettez à jour vers la dernière version des packages de support Xamarin.</span><span class="sxs-lookup"><span data-stu-id="0be78-165">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="0be78-166">La mise à jour des dernières versions des projets de démarrage rapide peut être lente.</span><span class="sxs-lookup"><span data-stu-id="0be78-166">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="0be78-167">Dans l’application, tapez un texte explicite, tel que *Découvrir Xamarin*, puis cliquez sur le bouton « + » (**+**).</span><span class="sxs-lookup"><span data-stu-id="0be78-167">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="0be78-168">Cette action envoie une demande post vers le back end Mobile Apps qui est hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0be78-168">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="0be78-169">Les données de la requête sont insérées dans la table TodoItem.</span><span class="sxs-lookup"><span data-stu-id="0be78-169">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="0be78-170">Les éléments stockés dans cette table sont renvoyés par le backend Mobile Apps et les données sont affichées dans la liste.</span><span class="sxs-lookup"><span data-stu-id="0be78-170">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="0be78-171">Vous trouverez le code qui vous permet d’accéder à votre back end Mobile Apps dans le fichier C# TodoItemManager.cs du projet de bibliothèque de classes portables de votre solution.</span><span class="sxs-lookup"><span data-stu-id="0be78-171">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-the-windows-project"></a><span data-ttu-id="0be78-172">(Facultatif) Exécuter le projet Windows</span><span class="sxs-lookup"><span data-stu-id="0be78-172">(Optional) Run the Windows project</span></span>

<span data-ttu-id="0be78-173">Dans cette section, vous exécutez le projet WinApp Xamarin pour les appareils Windows.</span><span class="sxs-lookup"><span data-stu-id="0be78-173">In this section, you run the Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="0be78-174">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Windows.</span><span class="sxs-lookup"><span data-stu-id="0be78-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="0be78-175">Dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0be78-175">In Visual Studio</span></span>

1. <span data-ttu-id="0be78-176">Cliquez avec le bouton droit sur les projets Windows, puis cliquez sur **Définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="0be78-176">Right-click any of the Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="0be78-177">Dans le menu **Générer**, cliquez sur **Gestionnaire de configuration**.</span><span class="sxs-lookup"><span data-stu-id="0be78-177">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="0be78-178">Dans la boîte de dialogue **Gestionnaire de configuration**, cochez les cases **Générer** et **Déployer** situées à côté du projet Windows que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="0be78-178">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the Windows project that you chose.</span></span>

4. <span data-ttu-id="0be78-179">Pour générer le projet et démarrer l’application dans un émulateur Windows, appuyez sur la touche **F5**.</span><span class="sxs-lookup"><span data-stu-id="0be78-179">To build the project and start the app in a Windows emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0be78-180">Si vous avez des problèmes pour générer le projet, exécutez le gestionnaire de package NuGet et mettez à jour vers la dernière version des packages de support Xamarin.</span><span class="sxs-lookup"><span data-stu-id="0be78-180">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="0be78-181">La mise à jour des dernières versions des projets de démarrage rapide peut être lente.</span><span class="sxs-lookup"><span data-stu-id="0be78-181">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="0be78-182">Dans l’application, tapez un texte explicite, tel que *Découvrir Xamarin*, puis cliquez sur le bouton « + » (**+**).</span><span class="sxs-lookup"><span data-stu-id="0be78-182">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    <span data-ttu-id="0be78-183">Cette action envoie une demande post vers le back end Mobile Apps qui est hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0be78-183">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="0be78-184">Les données de la requête sont insérées dans la table TodoItem.</span><span class="sxs-lookup"><span data-stu-id="0be78-184">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="0be78-185">Les éléments stockés dans cette table sont renvoyés par le backend Mobile Apps et les données sont affichées dans la liste.</span><span class="sxs-lookup"><span data-stu-id="0be78-185">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="0be78-186">Vous trouverez le code qui vous permet d’accéder à votre back end Mobile Apps dans le fichier C# TodoItemManager.cs du projet de bibliothèque de classes portables de votre solution.</span><span class="sxs-lookup"><span data-stu-id="0be78-186">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="0be78-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0be78-187">Next steps</span></span>

* [<span data-ttu-id="0be78-188">Ajout de l’authentification à votre application</span><span class="sxs-lookup"><span data-stu-id="0be78-188">Add authentication to your app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="0be78-189">Découvrez comment authentifier les utilisateurs de votre application avec un fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="0be78-189">Learn how to authenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="0be78-190">Ajouter des notifications Push à votre application Android</span><span class="sxs-lookup"><span data-stu-id="0be78-190">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="0be78-191">Découvrez comment ajouter la prise en charge des notifications Push à votre application et configurer le back end Mobile Apps pour utiliser Azure Notification Hubs afin d’envoyer les notifications Push.</span><span class="sxs-lookup"><span data-stu-id="0be78-191">Learn how to add push notifications support to your app and configure your Mobile Apps back end to use Azure Notification Hubs to send the push notifications.</span></span>

* [<span data-ttu-id="0be78-192">Activer la synchronisation hors connexion pour votre application</span><span class="sxs-lookup"><span data-stu-id="0be78-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="0be78-193">Découvrez comment ajouter une prise en charge hors connexion à votre application à l’aide d’un serveur principal Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="0be78-193">Learn how to add offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="0be78-194">La synchronisation hors connexion permet d’afficher, d’ajouter ou de modifier les données d’une application mobile même en l’absence de connexion au réseau.</span><span class="sxs-lookup"><span data-stu-id="0be78-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="0be78-195">Utilisation du client géré pour Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="0be78-195">Use the managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="0be78-196">Découvrez comment utiliser le Kit de développement logiciel (SDK) dans votre application Xamarin.</span><span class="sxs-lookup"><span data-stu-id="0be78-196">Learn how to work with the managed client SDK in your Xamarin app.</span></span>

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
