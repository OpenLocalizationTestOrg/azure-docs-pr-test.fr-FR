---
title: "aaaGet a démarré avec des concentrateurs de Notification pour les applications de Xamarin.Android | Documents Microsoft"
description: "Dans ce didacticiel, vous découvrez comment toouse Azure Notification Hubs toosend push notifications tooa les applications Xamarin Android."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="0dbc9-103">Prendre en main Notification Hubs avec Xamarin pour Android</span><span class="sxs-lookup"><span data-stu-id="0dbc9-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="0dbc9-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0dbc9-104">Overview</span></span>
<span data-ttu-id="0dbc9-105">Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push application de notifications de Xamarin.Android tooa.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Xamarin.Android application.</span></span>
<span data-ttu-id="0dbc9-106">Vous allez créer une application Xamarin.Android vide recevant des notifications Push via Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="0dbc9-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="0dbc9-107">Lorsque vous avez terminé, vous serez en mesure de toouse votre toobroadcast de concentrateur de notification push des appareils de hello notifications tooall votre application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="0dbc9-108">Hello code terminé est disponible dans hello [NotificationHubs application] [ GitHub] exemple.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-108">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="0dbc9-109">Ce didacticiel présente un scénario de diffusion simple hello dans à l’aide de concentrateurs de Notification.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-109">This tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0dbc9-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="0dbc9-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="0dbc9-111">code Hello terminée pour ce didacticiel se trouve sur GitHub [ici](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span><span class="sxs-lookup"><span data-stu-id="0dbc9-111">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dbc9-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0dbc9-112">Prerequisites</span></span>
<span data-ttu-id="0dbc9-113">Ce didacticiel requiert hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-113">This tutorial requires hello following:</span></span>

* <span data-ttu-id="0dbc9-114">Visual Studio avec Xamarin sur Windows ou Xamarin Studio sur Mac OS X. Des instructions d’installation complètes sont disponibles dans [Configurer et installer Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="0dbc9-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="0dbc9-115">Un compte Google actif</span><span class="sxs-lookup"><span data-stu-id="0dbc9-115">Active Google account</span></span>
* <span data-ttu-id="0dbc9-116">[Composant Azure Messaging]</span><span class="sxs-lookup"><span data-stu-id="0dbc9-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="0dbc9-117">[Composant Client Google Cloud Messaging]</span><span class="sxs-lookup"><span data-stu-id="0dbc9-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="0dbc9-118">Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels de Notification Hubs pour les applications Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0dbc9-119">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-119">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="0dbc9-120">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0dbc9-121">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="0dbc9-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="0dbc9-122">Activation de Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="0dbc9-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="0dbc9-123">Configuration de votre hub de notification</span><span class="sxs-lookup"><span data-stu-id="0dbc9-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="0dbc9-124">Cliquez sur hello <b>configurer</b> haut hello, entrez hello <b>clé API</b> valeur vous avez obtenu dans la section précédente de hello, puis cliquez sur <b>enregistrer</b>.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-124">Click hello <b>Configure</b> tab at hello top, enter hello <b>API Key</b> value you obtained in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="0dbc9-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="0dbc9-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="0dbc9-126">Votre concentrateur de notification est maintenant configuré toowork avec GCM, et vous disposez tooboth de chaînes de connexion hello enregistrer vos notifications tooreceive de l’application et les notifications de push toosend.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-126">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive notifications and toosend push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="0dbc9-127">Se connecter à votre hub de notification d’application toohello</span><span class="sxs-lookup"><span data-stu-id="0dbc9-127">Connect your app toohello notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="0dbc9-128">Création d'un projet</span><span class="sxs-lookup"><span data-stu-id="0dbc9-128">Create a new project</span></span>
1. <span data-ttu-id="0dbc9-129">Dans Xamarin Studio, cliquez sur **Nouvelle solution**, cliquez sur **Application Android**, puis sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="0dbc9-130">Saisissez le **Nom** et l’**Identificateur** de l’application.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="0dbc9-131">Cliquez sur hello **les plateformes cibles** toosupport et puis cliquez sur **suivant** et **créer**.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-131">Click hello **Target Plaforms** you want toosupport and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="0dbc9-132">Un projet Android est créé.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="0dbc9-133">Ouvrez les propriétés du projet hello en double-cliquant sur votre nouveau projet Bonjour affichage de solutions et en choisissant **Options**.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-133">Open hello project properties by right-clicking your new project in hello Solution view and choosing **Options**.</span></span> <span data-ttu-id="0dbc9-134">Sélectionnez hello **Application Android** élément Bonjour **générer** section.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-134">Select hello **Android Application** item in hello **Build** section.</span></span>
   
    <span data-ttu-id="0dbc9-135">Vérifiez cette première lettre de hello de votre **nom du Package** est en minuscules.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-135">Ensure that hello first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="0dbc9-136">Hello première lettre du nom du package hello doit être en minuscule.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-136">hello first letter of hello package name must be lowercase.</span></span> <span data-ttu-id="0dbc9-137">Sinon, vous recevrez des erreurs du manifeste d’application lors de l’inscription de vos **BroadcastReceiver** et **IntentFilter** pour les notifications Push ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="0dbc9-138">Si vous le souhaitez, jeu hello **version minimale Android** tooanother niveau de l’API.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-138">Optionally, set hello **Minimum Android version** tooanother API Level.</span></span>
3. <span data-ttu-id="0dbc9-139">Si vous le souhaitez, jeu hello **cible Android version** toohello une autre version de l’API que vous souhaitez tootarget (doit être au niveau d’API 8 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="0dbc9-139">Optionally, set hello **Target Android version** toohello another API version that you want tootarget (must be API level 8 or higher).</span></span>

<span data-ttu-id="0dbc9-140">Cliquez sur **OK** et boîte de dialogue Options du projet hello fermer.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-140">Click **OK** and close hello Project Options dialog.</span></span>

### <a name="add-hello-required-components-tooyour-project"></a><span data-ttu-id="0dbc9-141">Ajouter un projet de tooyour hello composants requis</span><span class="sxs-lookup"><span data-stu-id="0dbc9-141">Add hello required components tooyour project</span></span>
<span data-ttu-id="0dbc9-142">Hello Google Cloud Messaging Client disponible sur hello magasin de composants Xamarin simplifie hello prise en charge des notifications push dans Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-142">hello Google Cloud Messaging Client available on hello Xamarin Component Store simplifies hello process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="0dbc9-143">Cliquez sur le dossier composants hello Xamarin.Android application et choisissez **obtenir plusieurs composants**.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-143">Right-click hello Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="0dbc9-144">Recherchez hello **messagerie Azure** composant et l’ajouter toohello projet.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-144">Search for hello **Azure Messaging** component and add it toohello project.</span></span>
3. <span data-ttu-id="0dbc9-145">Recherchez hello **Client de messagerie Cloud Google** composant et l’ajouter toohello projet.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-145">Search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="0dbc9-146">Configuration de hubs de notification dans votre projet</span><span class="sxs-lookup"><span data-stu-id="0dbc9-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="0dbc9-147">Collectez hello informations pour votre application et notification votre hub Android suivantes :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-147">Gather hello following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="0dbc9-148">**GoogleProjectNumber**: obtenir cette valeur de numéro de projet à partir de la vue d’ensemble de hello de votre application sur hello portail des développeurs Google.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-148">**GoogleProjectNumber**:  Get this Project Number value from hello overview of your app on hello Google Developer Portal.</span></span> <span data-ttu-id="0dbc9-149">Vous avez notée précédemment cette valeur lorsque vous avez créé l’application hello sur le portail hello.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-149">You made a note of this value earlier when you created hello app on hello portal.</span></span>
   * <span data-ttu-id="0dbc9-150">**Écouter la chaîne de connexion**: tableau de bord hello Bonjour [portail classique Azure], cliquez sur **afficher les chaînes de connexion**.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-150">**Listen connection string**: On hello dashboard in hello [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="0dbc9-151">Hello de copie *DefaultListenSharedAccessSignature* chaîne de connexion pour cette valeur.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-151">Copy hello *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="0dbc9-152">**Nom du Hub**: nom de hello de votre concentrateur hello [portail classique Azure].</span><span class="sxs-lookup"><span data-stu-id="0dbc9-152">**Hub name**: This is hello name of your hub from hello [Azure Classic Portal].</span></span> <span data-ttu-id="0dbc9-153">Par exemple, *mynotificationhub2*.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="0dbc9-154">Créer un **Constants.cs** classe pour votre projet Xamarin et définir hello suivant de valeurs constantes dans la classe hello.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-154">Create a **Constants.cs** class for your Xamarin project and define hello following constant values in hello class.</span></span> <span data-ttu-id="0dbc9-155">Remplacez les espaces réservés de hello avec vos valeurs.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-155">Replace hello placeholders with your values.</span></span>
     
       <span data-ttu-id="0dbc9-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="0dbc9-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="0dbc9-157">}</span><span class="sxs-lookup"><span data-stu-id="0dbc9-157">}</span></span>
2. <span data-ttu-id="0dbc9-158">Ajoutez hello qui suit à l’aide d’instructions trop**MainActivity.cs**:</span><span class="sxs-lookup"><span data-stu-id="0dbc9-158">Add hello following using statements too**MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="0dbc9-159">Ajouter un toohello de variable d’instance `MainActivity` classe qui sera utilisé tooshow une boîte de dialogue alerte lors de l’application hello est en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-159">Add an instance variable toohello `MainActivity` class that will be used tooshow an alert dialog when hello app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="0dbc9-160">Créer hello méthode Bonjour **MainActivity** classe :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-160">Create hello following method in hello **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="0dbc9-161">Bonjour `OnCreate` méthode **MainActivity.cs**, initialiser hello `instance` variable et ajoutez un appel trop`RegisterWithGCM`:</span><span class="sxs-lookup"><span data-stu-id="0dbc9-161">In hello `OnCreate` method of **MainActivity.cs**, initialize hello `instance` variable and add a call too`RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="0dbc9-162">Créez la classe **MyBroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0dbc9-163">Nous allons décrire la procédure à suivre pour créer une classe **BroadcastReceiver** de toutes pièces.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="0dbc9-164">Toutefois, une création rapide toomanually autre **MyBroadcastReceiver.cs** est toorefer toohello **GcmService.cs** fichier trouvé dans hello exemple de projet Xamarin.Android inclus avec hello [NotificationHubs exemples][GitHub].</span><span class="sxs-lookup"><span data-stu-id="0dbc9-164">However, a quick alternative toomanually creating **MyBroadcastReceiver.cs** is toorefer toohello **GcmService.cs** file found in hello sample Xamarin.Android project included with hello [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="0dbc9-165">Duplication de **GcmService.cs** et la modification des noms de classe peut être un toostart idéal également.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-165">Duplicating **GcmService.cs** and changing class names can be a great place toostart as well.</span></span>
   > 
   > 
7. <span data-ttu-id="0dbc9-166">Ajoutez hello qui suit à l’aide d’instructions trop**MyBroadcastReceiver.cs** (référence toohello composant et l’assembly que vous avez ajouté précédemment) :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-166">Add hello following using statements too**MyBroadcastReceiver.cs** (referring toohello component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="0dbc9-167">Dans **MyBroadcastReceiver.cs**, ajouter hello suivant des demandes d’autorisations entre hello **à l’aide de** instructions et hello **espace de noms** déclaration :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-167">In **MyBroadcastReceiver.cs**, add hello following permission requests between hello **using** statements and hello **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="0dbc9-168">Dans **MyBroadcastReceiver.cs**, modifiez hello **MyBroadcastReceiver** suivant de hello toomatch de classe :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-168">In **MyBroadcastReceiver.cs**, change hello **MyBroadcastReceiver** class toomatch hello following:</span></span>
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. <span data-ttu-id="0dbc9-169">Dans **MyBroadcastReceiver.cs**, ajoutez une classe nommée **PushHandlerService** dérivée de **GcmServiceBase**.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="0dbc9-170">Assurez-vous que tooapply hello **Service** toohello classe d’attributs :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-170">Make sure tooapply hello **Service** attribute toohello class:</span></span>
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="0dbc9-171">**GcmServiceBase** implémente les méthodes **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** et **OnError()**.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="0dbc9-172">Notre **PushHandlerService** classe d’implémentation doit substituer ces méthodes et ces méthodes déclenchent dans toointeracting de réponse avec un concentrateur de notification hello.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response toointeracting with hello notification hub.</span></span>
12. <span data-ttu-id="0dbc9-173">Remplacer hello **OnRegistered()** méthode dans **PushHandlerService** à l’aide de hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-173">Override hello **OnRegistered()** method in **PushHandlerService** by using hello following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > <span data-ttu-id="0dbc9-174">Bonjour **OnRegistered()** de code ci-dessus, vous devez noter hello capacité toospecify balises tooregister pour les canaux de messagerie spécifiques.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-174">In hello **OnRegistered()** code above, you should note hello ability toospecify tags tooregister for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="0dbc9-175">Remplacer hello **OnMessage** méthode dans **PushHandlerService** à l’aide de hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-175">Override hello **OnMessage** method in **PushHandlerService** by using hello following code:</span></span>
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. <span data-ttu-id="0dbc9-176">Ajoutez hello suivant **createNotification** et **dialogNotify** méthodes trop**PushHandlerService** pour avertir les utilisateurs lorsqu’une notification est reçue.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-176">Add hello following **createNotification** and **dialogNotify** methods too**PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="0dbc9-177">La conception des notifications dans Android version 5.0 et ultérieure est radicalement différente de celle des versions précédentes.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="0dbc9-178">Si vous testez cette sur Android 5.0 ou version ultérieure, application hello devez toobe notification de hello tooreceive en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-178">If you test this on Android 5.0 or later, hello app will need toobe running tooreceive hello notification.</span></span> <span data-ttu-id="0dbc9-179">Pour plus d’informations, consultez [Notifications Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="0dbc9-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. <span data-ttu-id="0dbc9-180">Remplacez les membres abstraits **OnUnRegistered()**, **OnRecoverableError()** et **OnError()** pour pouvoir compiler votre code :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a><span data-ttu-id="0dbc9-181">Exécuter votre application dans l’émulateur de hello</span><span class="sxs-lookup"><span data-stu-id="0dbc9-181">Run your app in hello emulator</span></span>
<span data-ttu-id="0dbc9-182">Si vous exécutez cette application dans l’émulateur de hello, assurez-vous que vous utilisez un virtuel appareil (Android) qui prend en charge APIs de Google.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-182">If you run this app in hello emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0dbc9-183">Dans les notifications de push de tooreceive de commande, vous devez configurer un compte Google sur votre appareil virtuel Android.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-183">In order tooreceive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="0dbc9-184">(Dans l’émulateur de hello, accédez trop**paramètres** et cliquez sur **ajouter un compte**.) En outre, assurez-vous qu’émulateur hello est connecté toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-184">(In hello emulator, navigate too**Settings** and click **Add Account**.) Also, make sure that hello emulator is connected toohello Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="0dbc9-185">La conception des notifications dans Android version 5.0 et ultérieure est radicalement différente de celle des versions précédentes.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="0dbc9-186">Pour plus d’informations, consultez [Notifications Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="0dbc9-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="0dbc9-187">Dans **Outils**, cliquez sur **Open Android Emulator Manager**, sélectionnez votre appareil, puis cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="0dbc9-188">Sélectionnez **API Google** dans **Cible**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="0dbc9-189">Dans la barre d’outils supérieure hello, cliquez sur **exécuter**, puis sélectionnez votre application.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-189">On hello top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="0dbc9-190">Cela démarre l’émulateur hello et exécute l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-190">This starts hello emulator and runs hello app.</span></span>
   
   <span data-ttu-id="0dbc9-191">application Hello récupère hello *registrationId* GCM et inscrit avec le hub de notification hello.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-191">hello app retrieves hello *registrationId* from GCM and registers with hello notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="0dbc9-192">Envoi de notifications à partir de votre serveur principal</span><span class="sxs-lookup"><span data-stu-id="0dbc9-192">Send notifications from your backend</span></span>
<span data-ttu-id="0dbc9-193">Vous pouvez tester la réception de notifications dans votre application en envoyant des notifications Bonjour [portail classique Azure] via hello debug onglet concentrateur de notification hello, comme indiqué dans l’écran hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-193">You can test receiving notifications in your app by sending notifications in hello [Azure Classic Portal] via hello debug tab on hello notification hub, as shown in hello screen below.</span></span>

![][30]

<span data-ttu-id="0dbc9-194">Les notifications Push sont normalement envoyées dans un service principal tel que Mobile Services ou ASP.NET par le biais d’une bibliothèque compatible.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="0dbc9-195">Vous pouvez également utiliser les API REST de hello directement les messages de notification de toosend si une bibliothèque n’est pas disponible pour votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-195">You can also use hello REST API directly toosend notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="0dbc9-196">Voici une liste de certains autres didacticiels que vous pourriez vouloir tooreview pour envoyer des notifications :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-196">Here is a list of some other tutorials that you may want tooreview for sending notifications:</span></span>

* <span data-ttu-id="0dbc9-197">ASP.NET : Consultez [utiliser Notification Hubs toopush notifications toousers].</span><span class="sxs-lookup"><span data-stu-id="0dbc9-197">ASP.NET: See [Use Notification Hubs toopush notifications toousers].</span></span>
* <span data-ttu-id="0dbc9-198">Java de concentrateurs de Notification Azure SDK : consultez [comment toouse concentrateurs de Notification à partir de Java](notification-hubs-java-push-notification-tutorial.md) pour envoyer des notifications à partir de Java.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-198">Azure Notification Hubs Java SDK: See [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="0dbc9-199">Il a été testé dans Eclipse pour le développement Android.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="0dbc9-200">PHP : Consultez [comment toouse concentrateurs de Notification à partir de PHP](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="0dbc9-200">PHP: See [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="0dbc9-201">Dans hello suivant sous-sections suivantes du didacticiel de hello, vous envoyez des notifications à l’aide d’une application de console .NET et à l’aide d’un service mobile via un script de nœud.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-201">In hello next subsections of hello tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="0dbc9-202">(Facultatif) Pour envoyer des notifications en utilisant une application .NET :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="0dbc9-203">Dans cette section, nous allons envoyer des notifications à l’aide d’une application de console .NET.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="0dbc9-204">Créez une application console Visual C# :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="0dbc9-205">Dans Visual Studio, cliquez successivement sur **Outils**, **Gestionnaire de package NuGet** et **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="0dbc9-206">Cela affiche hello Package Manager Console dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-206">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="0dbc9-207">Dans la fenêtre de Console du Gestionnaire de Package de hello, définissez hello **projet par défaut** tooyour nouveau projet d’application console et puis, dans la fenêtre de console hello, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-207">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="0dbc9-208">Cette opération ajoute une référence de toohello Azure Notification Hubs SDK à l’aide de hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet de concentrateurs Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-208">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="0dbc9-209">Ouvrez le fichier Program.cs de hello et ajoutez hello suit `using` instruction :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-209">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="0dbc9-210">Dans votre `Program` de classe, ajoutez hello suivant de méthode.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-210">In your `Program` class, add hello following method.</span></span> <span data-ttu-id="0dbc9-211">Mettre à jour le texte d’espace réservé hello avec votre *DefaultFullSharedAccessSignature* nom de hub et la chaîne de connexion à partir de hello [portail classique Azure].</span><span class="sxs-lookup"><span data-stu-id="0dbc9-211">Update hello placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from hello [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="0dbc9-212">Ajouter hello suivant des lignes dans votre **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="0dbc9-212">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="0dbc9-213">Appuyez sur la touche application de hello toorun clé hello F5.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-213">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="0dbc9-214">Vous devriez recevoir une notification dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-214">You should receive a notification in hello app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="0dbc9-215">(Facultatif) Envoyer une notification à l’aide d’un service mobile</span><span class="sxs-lookup"><span data-stu-id="0dbc9-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="0dbc9-216">Suivez les procédures [Prise en main de Mobile Services].</span><span class="sxs-lookup"><span data-stu-id="0dbc9-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="0dbc9-217">Connectez-vous à toohello [portail classique Azure], puis sélectionnez votre service mobile.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-217">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="0dbc9-218">Sélectionnez hello **planificateur** onglet en haut de hello.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-218">Select hello **Scheduler** tab on hello top.</span></span>
   
      ![][22]
4. <span data-ttu-id="0dbc9-219">Créez un travail planifié, insérez un nom, puis sélectionnez **On demand**.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="0dbc9-220">Lorsque le travail de hello est créé, cliquez sur le nom de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-220">When hello job is created, click hello job name.</span></span> <span data-ttu-id="0dbc9-221">Puis cliquez sur hello **Script** onglet sur la barre supérieure de hello.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-221">Then click hello **Script** tab on hello top bar.</span></span>
6. <span data-ttu-id="0dbc9-222">Insérez hello script à l’intérieur de votre fonction Planificateur suivant.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-222">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="0dbc9-223">Rendre des espaces réservés de hello tooreplace vraiment avec votre notification hub hello et nom de chaîne de connexion pour *DefaultFullSharedAccessSignature* que vous avez obtenu précédemment.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-223">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="0dbc9-224">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-224">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. <span data-ttu-id="0dbc9-225">Cliquez sur **exécuter une fois** sur la barre inférieure de hello.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-225">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="0dbc9-226">Vous devez recevoir une notification toast.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dbc9-227">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0dbc9-227">Next steps</span></span>
<span data-ttu-id="0dbc9-228">Dans cet exemple simple, diffusées notifications tooall vos appareils Android.</span><span class="sxs-lookup"><span data-stu-id="0dbc9-228">In this simple example, you broadcasted notifications tooall your Android devices.</span></span> <span data-ttu-id="0dbc9-229">Dans l’ordre tootarget des utilisateurs spécifiques, consultez le didacticiel de toohello [utiliser Notification Hubs toopush notifications toousers].</span><span class="sxs-lookup"><span data-stu-id="0dbc9-229">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="0dbc9-230">Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, vous pouvez lire [toosend utiliser Notification Hubs actualités].</span><span class="sxs-lookup"><span data-stu-id="0dbc9-230">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="0dbc9-231">En savoir plus sur la façon toouse Notification Hubs dans [des conseils de concentrateurs de Notification] et Bonjour [concentrateurs de Notification toofor de façon Android].</span><span class="sxs-lookup"><span data-stu-id="0dbc9-231">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Prise en main de Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[portail classique Azure]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[des conseils de concentrateurs de Notification]: http://msdn.microsoft.com/library/jj927170.aspx
[concentrateurs de Notification toofor de façon Android]: http://msdn.microsoft.com/library/dn282661.aspx

[utiliser Notification Hubs toopush notifications toousers]: /manage/services/notification-hubs/notify-users-aspnet
[toosend utiliser Notification Hubs actualités]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Composant Client Google Cloud Messaging]: http://components.xamarin.com/view/GCMClient/
[Composant Azure Messaging]: http://components.xamarin.com/view/azure-messaging
