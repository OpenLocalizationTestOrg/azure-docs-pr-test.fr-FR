---
title: Prise en main de Notification Hubs pour les applications Xamarin.Android | Microsoft Docs
description: "Ce didacticiel vous apprend à utiliser Azure Notification Hubs pour envoyer des notifications Push vers une application Xamarin Android."
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
ms.openlocfilehash: e0ef1b006a2b202c08a71caaff4ef4d763d50d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a><span data-ttu-id="808e9-103">Prendre en main Notification Hubs avec Xamarin pour Android</span><span class="sxs-lookup"><span data-stu-id="808e9-103">Get started with Notification Hubs with Xamarin for Android</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="808e9-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="808e9-104">Overview</span></span>
<span data-ttu-id="808e9-105">Ce didacticiel vous montre comment utiliser Azure Notification Hubs pour envoyer des notifications Push vers une application Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="808e9-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Xamarin.Android application.</span></span>
<span data-ttu-id="808e9-106">Vous allez créer une application Xamarin.Android vide recevant des notifications Push via Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="808e9-106">You'll create a blank Xamarin.Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="808e9-107">Une fois l’opération terminée, vous pouvez utiliser votre hub de notification pour diffuser des notifications Push sur tous les appareils exécutant votre application.</span><span class="sxs-lookup"><span data-stu-id="808e9-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="808e9-108">Le code finalisé est disponible dans l’exemple [Application NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="808e9-108">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="808e9-109">Ce didacticiel présente un scénario de diffusion simple utilisant les Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="808e9-109">This tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="808e9-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="808e9-110">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="808e9-111">Le code complet de ce didacticiel est disponible sur GitHub [ici](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span><span class="sxs-lookup"><span data-stu-id="808e9-111">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="808e9-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="808e9-112">Prerequisites</span></span>
<span data-ttu-id="808e9-113">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="808e9-113">This tutorial requires the following:</span></span>

* <span data-ttu-id="808e9-114">Visual Studio avec Xamarin sur Windows ou Xamarin Studio sur Mac OS X. Des instructions d’installation complètes sont disponibles dans [Configurer et installer Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="808e9-114">Visual Studio with Xamarin on Windows or Xamarin Studio on Mac OS X. Complete installation instructions are on [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* <span data-ttu-id="808e9-115">Un compte Google actif</span><span class="sxs-lookup"><span data-stu-id="808e9-115">Active Google account</span></span>
* <span data-ttu-id="808e9-116">[Composant Azure Messaging]</span><span class="sxs-lookup"><span data-stu-id="808e9-116">[Azure Messaging Component]</span></span>
* <span data-ttu-id="808e9-117">[Composant Client Google Cloud Messaging]</span><span class="sxs-lookup"><span data-stu-id="808e9-117">[Google Cloud Messaging Client Component]</span></span>

<span data-ttu-id="808e9-118">Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels de Notification Hubs pour les applications Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="808e9-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin.Android apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="808e9-119">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="808e9-119">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="808e9-120">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="808e9-120">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="808e9-121">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="808e9-121">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).</span></span>
> 
> 

## <a name="enable-google-cloud-messaging"></a><span data-ttu-id="808e9-122">Activation de Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="808e9-122">Enable Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="808e9-123">Configuration de votre hub de notification</span><span class="sxs-lookup"><span data-stu-id="808e9-123">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p><span data-ttu-id="808e9-124">Cliquez sur l’onglet <b>Configurer</b> dans la partie supérieure, saisissez la valeur de <b>clé API</b> obtenue à la section précédente, puis cliquez sur <b>Enregistrer</b>.</span><span class="sxs-lookup"><span data-stu-id="808e9-124">Click the <b>Configure</b> tab at the top, enter the <b>API Key</b> value you obtained in the previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>
<span data-ttu-id="808e9-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span><span class="sxs-lookup"><span data-stu-id="808e9-125">&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)</span></span>

<span data-ttu-id="808e9-126">Votre concentrateur de notification est à présent configuré pour GCM, et vous disposez des chaînes de connexion vous permettant d’inscrire votre application pour la réception de notifications et l’envoi de notifications Push.</span><span class="sxs-lookup"><span data-stu-id="808e9-126">Your notification hub is now configured to work with GCM, and you have the connection strings to both register your app to receive notifications and to send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="808e9-127">Connexion de votre application au hub de notification</span><span class="sxs-lookup"><span data-stu-id="808e9-127">Connect your app to the notification hub</span></span>
### <a name="create-a-new-project"></a><span data-ttu-id="808e9-128">Création d'un projet</span><span class="sxs-lookup"><span data-stu-id="808e9-128">Create a new project</span></span>
1. <span data-ttu-id="808e9-129">Dans Xamarin Studio, cliquez sur **Nouvelle solution**, cliquez sur **Application Android**, puis sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="808e9-129">In Xamarin Studio, click **New Solution**, click **Android App**, and click **Next**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. <span data-ttu-id="808e9-130">Saisissez le **Nom** et l’**Identificateur** de l’application.</span><span class="sxs-lookup"><span data-stu-id="808e9-130">Enter your **App Name** and **Identifier**.</span></span> <span data-ttu-id="808e9-131">Cliquez sur les **plateformes cibles** que vous souhaitez prendre en charge, puis cliquez sur **Suivant** et sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="808e9-131">Click the **Target Plaforms** you want to support and then click **Next** and **Create**.</span></span>
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    <span data-ttu-id="808e9-132">Un projet Android est créé.</span><span class="sxs-lookup"><span data-stu-id="808e9-132">This creates a new Android project.</span></span>

1. <span data-ttu-id="808e9-133">Ouvrez les propriétés du projet en cliquant avec le bouton droit sur votre nouveau projet dans la vue Solution et en choisissant **Options**.</span><span class="sxs-lookup"><span data-stu-id="808e9-133">Open the project properties by right-clicking your new project in the Solution view and choosing **Options**.</span></span> <span data-ttu-id="808e9-134">Sélectionnez l'élément **Android Application** dans la section **Build**.</span><span class="sxs-lookup"><span data-stu-id="808e9-134">Select the **Android Application** item in the **Build** section.</span></span>
   
    <span data-ttu-id="808e9-135">Assurez-vous que la première lettre de votre nom de package ( **Package name** ) est en minuscule.</span><span class="sxs-lookup"><span data-stu-id="808e9-135">Ensure that the first letter of your **Package name** is lowercase.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="808e9-136">La première lettre du nom du package doit être une minuscule.</span><span class="sxs-lookup"><span data-stu-id="808e9-136">The first letter of the package name must be lowercase.</span></span> <span data-ttu-id="808e9-137">Sinon, vous recevrez des erreurs du manifeste d’application lors de l’inscription de vos **BroadcastReceiver** et **IntentFilter** pour les notifications Push ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="808e9-137">Otherwise, you will receive application manifest errors when you register your **BroadcastReceiver** and **IntentFilter** for push notifications below.</span></span>
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. <span data-ttu-id="808e9-138">Définissez optionnellement la **version minimale d’Android** sur un autre niveau d’API.</span><span class="sxs-lookup"><span data-stu-id="808e9-138">Optionally, set the **Minimum Android version** to another API Level.</span></span>
3. <span data-ttu-id="808e9-139">Le cas échéant, définissez la **version Android cible** sur une autre version d’API que vous souhaitez cibler (API de niveau 8 ou supérieur).</span><span class="sxs-lookup"><span data-stu-id="808e9-139">Optionally, set the **Target Android version** to the another API version that you want to target (must be API level 8 or higher).</span></span>

<span data-ttu-id="808e9-140">Cliquez sur **OK** et fermez la boîte de dialogue Options du projet.</span><span class="sxs-lookup"><span data-stu-id="808e9-140">Click **OK** and close the Project Options dialog.</span></span>

### <a name="add-the-required-components-to-your-project"></a><span data-ttu-id="808e9-141">Ajout des composants requis à votre projet</span><span class="sxs-lookup"><span data-stu-id="808e9-141">Add the required components to your project</span></span>
<span data-ttu-id="808e9-142">Le client Google Cloud Messaging, disponible dans le magasin de composants Xamarin, simplifie la prise en charge des notifications Push dans les applications Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="808e9-142">The Google Cloud Messaging Client available on the Xamarin Component Store simplifies the process of supporting push notifications in Xamarin.Android.</span></span>

1. <span data-ttu-id="808e9-143">Cliquez avec le bouton droit sur le dossier Components de l’application Xamarin.Android et choisissez **Get More Components...**.</span><span class="sxs-lookup"><span data-stu-id="808e9-143">Right-click the Components folder in Xamarin.Android app and choose **Get More Components**.</span></span>
2. <span data-ttu-id="808e9-144">Recherchez le composant **Azure Messaging** et ajoutez-le au projet.</span><span class="sxs-lookup"><span data-stu-id="808e9-144">Search for the **Azure Messaging** component and add it to the project.</span></span>
3. <span data-ttu-id="808e9-145">Recherchez le composant **Client Google Cloud Messaging** et ajoutez-le au projet.</span><span class="sxs-lookup"><span data-stu-id="808e9-145">Search for the **Google Cloud Messaging Client** component and add it to the project.</span></span>

### <a name="set-up-notification-hubs-in-your-project"></a><span data-ttu-id="808e9-146">Configuration de hubs de notification dans votre projet</span><span class="sxs-lookup"><span data-stu-id="808e9-146">Set up notification hubs in your project</span></span>
1. <span data-ttu-id="808e9-147">Collectez les informations suivantes pour votre application Android et votre concentrateur de notifications :</span><span class="sxs-lookup"><span data-stu-id="808e9-147">Gather the following information for your Android app and notification hub:</span></span>
   
   * <span data-ttu-id="808e9-148">**GoogleProjectNumber** : obtenez cette valeur de numéro de projet dans la vue d’ensemble de votre application sur le portail de développement Google.</span><span class="sxs-lookup"><span data-stu-id="808e9-148">**GoogleProjectNumber**:  Get this Project Number value from the overview of your app on the Google Developer Portal.</span></span> <span data-ttu-id="808e9-149">Vous l’avez notée précédemment lorsque vous avez créé l’application sur le portail.</span><span class="sxs-lookup"><span data-stu-id="808e9-149">You made a note of this value earlier when you created the app on the portal.</span></span>
   * <span data-ttu-id="808e9-150">**Chaîne de connexion d’écoute** : dans le tableau de bord du [portail Azure Classic], cliquez sur **Afficher les chaînes de connexion**.</span><span class="sxs-lookup"><span data-stu-id="808e9-150">**Listen connection string**: On the dashboard in the [Azure Classic Portal], click **View connection strings**.</span></span> <span data-ttu-id="808e9-151">Copiez la chaîne de connexion *DefaultListenSharedAccessSignature* pour cette valeur.</span><span class="sxs-lookup"><span data-stu-id="808e9-151">Copy the *DefaultListenSharedAccessSignature* connection string for this value.</span></span>
   * <span data-ttu-id="808e9-152">**Nom du concentrateur**: c’est le nom de votre concentrateur sur le [portail Azure Classic].</span><span class="sxs-lookup"><span data-stu-id="808e9-152">**Hub name**: This is the name of your hub from the [Azure Classic Portal].</span></span> <span data-ttu-id="808e9-153">Par exemple, *mynotificationhub2*.</span><span class="sxs-lookup"><span data-stu-id="808e9-153">For example, *mynotificationhub2*.</span></span>
     
     <span data-ttu-id="808e9-154">Créez une classe **Constants.cs** pour votre projet Xamarin et définissez les valeurs constantes suivantes dans la classe.</span><span class="sxs-lookup"><span data-stu-id="808e9-154">Create a **Constants.cs** class for your Xamarin project and define the following constant values in the class.</span></span> <span data-ttu-id="808e9-155">Remplacez les espaces réservés par vos valeurs.</span><span class="sxs-lookup"><span data-stu-id="808e9-155">Replace the placeholders with your values.</span></span>
     
       <span data-ttu-id="808e9-156">public static class Constants   {</span><span class="sxs-lookup"><span data-stu-id="808e9-156">public static class Constants   {</span></span>
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       <span data-ttu-id="808e9-157">}</span><span class="sxs-lookup"><span data-stu-id="808e9-157">}</span></span>
2. <span data-ttu-id="808e9-158">Ajoutez les instructions using suivantes à **MainActivity.cs**:</span><span class="sxs-lookup"><span data-stu-id="808e9-158">Add the following using statements to **MainActivity.cs**:</span></span>
   
        using Android.Util;
        using Gcm.Client;
3. <span data-ttu-id="808e9-159">Ajoutez une variable d’instance à la classe `MainActivity` , qui sera utilisée pour afficher une boîte de dialogue d’alerte lors de l’exécution de l’application :</span><span class="sxs-lookup"><span data-stu-id="808e9-159">Add an instance variable to the `MainActivity` class that will be used to show an alert dialog when the app is running:</span></span>
   
        public static MainActivity instance;
4. <span data-ttu-id="808e9-160">Ajoutez la méthode suivante dans la classe **MainActivity** :</span><span class="sxs-lookup"><span data-stu-id="808e9-160">Create the following method in the **MainActivity** class:</span></span>
   
        private void RegisterWithGCM()
        {
            // Check to ensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. <span data-ttu-id="808e9-161">Dans la méthode `OnCreate` de **MainActivity.cs**, initialisez la variable `instance` et ajoutez un appel à `RegisterWithGCM` :</span><span class="sxs-lookup"><span data-stu-id="808e9-161">In the `OnCreate` method of **MainActivity.cs**, initialize the `instance` variable and add a call to `RegisterWithGCM`:</span></span>
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from the "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from the layout resource,
            // and attach an event to it
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. <span data-ttu-id="808e9-162">Créez la classe **MyBroadcastReceiver**.</span><span class="sxs-lookup"><span data-stu-id="808e9-162">Create a new class, **MyBroadcastReceiver**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="808e9-163">Nous allons décrire la procédure à suivre pour créer une classe **BroadcastReceiver** de toutes pièces.</span><span class="sxs-lookup"><span data-stu-id="808e9-163">We will walk through creating a **BroadcastReceiver** class from scratch below.</span></span> <span data-ttu-id="808e9-164">Il existe toutefois une alternative rapide à la création manuelle de **MyBroadcastReceiver.cs**, qui consiste à se reporter au fichier **GcmService.cs** de l’exemple de projet Xamarin.Android fourni avec les [exemples NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="808e9-164">However, a quick alternative to manually creating **MyBroadcastReceiver.cs** is to refer to the **GcmService.cs** file found in the sample Xamarin.Android project included with the [NotificationHubs samples][GitHub].</span></span> <span data-ttu-id="808e9-165">La duplication de **GcmService.cs** et le changement des noms de classe peuvent également constituer un excellent point de départ.</span><span class="sxs-lookup"><span data-stu-id="808e9-165">Duplicating **GcmService.cs** and changing class names can be a great place to start as well.</span></span>
   > 
   > 
7. <span data-ttu-id="808e9-166">Ajoutez les instructions using suivantes à **MyBroadcastReceiver.cs** (faisant référence au composant et à l’assembly ajoutés plus tôt) :</span><span class="sxs-lookup"><span data-stu-id="808e9-166">Add the following using statements to **MyBroadcastReceiver.cs** (referring to the component and assembly that you added earlier):</span></span>
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. <span data-ttu-id="808e9-167">Dans **MyBroadcastReceiver.cs**, ajoutez les demandes d’autorisation suivantes entre les instructions **using** et la déclaration **namespace** :</span><span class="sxs-lookup"><span data-stu-id="808e9-167">In **MyBroadcastReceiver.cs**, add the following permission requests between the **using** statements and the **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. <span data-ttu-id="808e9-168">Dans **MyBroadcastReceiver.cs**, changez la classe **MyBroadcastReceiver** comme suit :</span><span class="sxs-lookup"><span data-stu-id="808e9-168">In **MyBroadcastReceiver.cs**, change the **MyBroadcastReceiver** class to match the following:</span></span>
   
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
10. <span data-ttu-id="808e9-169">Dans **MyBroadcastReceiver.cs**, ajoutez une classe nommée **PushHandlerService** dérivée de **GcmServiceBase**.</span><span class="sxs-lookup"><span data-stu-id="808e9-169">Add another class in **MyBroadcastReceiver.cs** named **PushHandlerService**, which derives from **GcmServiceBase**.</span></span> <span data-ttu-id="808e9-170">Veillez à appliquer l’attribut **Service** à la classe :</span><span class="sxs-lookup"><span data-stu-id="808e9-170">Make sure to apply the **Service** attribute to the class:</span></span>
    
         [Service] // Must use the service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. <span data-ttu-id="808e9-171">**GcmServiceBase** implémente les méthodes **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** et **OnError()**.</span><span class="sxs-lookup"><span data-stu-id="808e9-171">**GcmServiceBase** implements methods **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()**, and **OnError()**.</span></span> <span data-ttu-id="808e9-172">Notre classe d’implémentation **PushHandlerService** doit remplacer ces méthodes, qui à leur tour seront déclenchées en réponse à l’interaction avec le concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="808e9-172">Our **PushHandlerService** implementation class must override these methods, and these methods will fire in response to interacting with the notification hub.</span></span>
12. <span data-ttu-id="808e9-173">Remplacez la méthode **OnRegistered()** dans **PushHandlerService** par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="808e9-173">Override the **OnRegistered()** method in **PushHandlerService** by using the following code:</span></span>
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "The device has been Registered!");
    
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
    > <span data-ttu-id="808e9-174">Dans le code **OnRegistered()** ci-dessus, notez qu’il est possible de spécifier des balises pour enregistrer des canaux de messagerie spécifiques.</span><span class="sxs-lookup"><span data-stu-id="808e9-174">In the **OnRegistered()** code above, you should note the ability to specify tags to register for specific messaging channels.</span></span>
    > 
    > 
13. <span data-ttu-id="808e9-175">Remplacez la méthode **OnMessage** dans **PushHandlerService** par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="808e9-175">Override the **OnMessage** method in **PushHandlerService** by using the following code:</span></span>
    
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
14. <span data-ttu-id="808e9-176">Ajoutez les méthodes **createNotification** et **dialogNotify** à **PushHandlerService** pour avertir les utilisateurs lorsqu’une notification est reçue.</span><span class="sxs-lookup"><span data-stu-id="808e9-176">Add the following **createNotification** and **dialogNotify** methods to **PushHandlerService** for notifying users when a notification is received.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="808e9-177">La conception des notifications dans Android version 5.0 et ultérieure est radicalement différente de celle des versions précédentes.</span><span class="sxs-lookup"><span data-stu-id="808e9-177">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="808e9-178">Si vous testez cette fonction sur Android 5.0 ou version ultérieure, l’application doit être en cours d’exécution pour recevoir la notification.</span><span class="sxs-lookup"><span data-stu-id="808e9-178">If you test this on Android 5.0 or later, the app will need to be running to receive the notification.</span></span> <span data-ttu-id="808e9-179">Pour plus d’informations, consultez [Notifications Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="808e9-179">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent to show UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create the notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove the notification once the user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set the notification info
            //we use the pending intent, passing our ui intent over, which will get called
            //when the notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show the notification
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
15. <span data-ttu-id="808e9-180">Remplacez les membres abstraits **OnUnRegistered()**, **OnRecoverableError()** et **OnError()** pour pouvoir compiler votre code :</span><span class="sxs-lookup"><span data-stu-id="808e9-180">Override abstract members **OnUnRegistered()**, **OnRecoverableError()**, and **OnError()** so that your code compiles:</span></span>
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "The device has been unregistered!");
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

## <a name="run-your-app-in-the-emulator"></a><span data-ttu-id="808e9-181">Exécution de votre application dans l'émulateur</span><span class="sxs-lookup"><span data-stu-id="808e9-181">Run your app in the emulator</span></span>
<span data-ttu-id="808e9-182">Si vous exécutez cette application dans l’émulateur, veillez à utiliser un appareil virtuel Android (AVD) qui prend en charge les API Google.</span><span class="sxs-lookup"><span data-stu-id="808e9-182">If you run this app in the emulator, make sure that you use an Android Virtual Device (AVD) that supports Google APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="808e9-183">Pour recevoir des notifications Push, vous devez configurer un compte Google sur votre appareil virtuel Android.</span><span class="sxs-lookup"><span data-stu-id="808e9-183">In order to receive push notifications, you must set up a Google account on your Android Virtual Device.</span></span> <span data-ttu-id="808e9-184">(Dans l’émulateur, accédez à **Paramètres**, puis cliquez sur **Ajouter un compte**.) Assurez-vous également que l’émulateur est connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="808e9-184">(In the emulator, navigate to **Settings** and click **Add Account**.) Also, make sure that the emulator is connected to the Internet.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="808e9-185">La conception des notifications dans Android version 5.0 et ultérieure est radicalement différente de celle des versions précédentes.</span><span class="sxs-lookup"><span data-stu-id="808e9-185">Notification design in Android version 5.0 and later represents a significant departure from that of previous versions.</span></span> <span data-ttu-id="808e9-186">Pour plus d’informations, consultez [Notifications Android](http://go.microsoft.com/fwlink/?LinkId=615880).</span><span class="sxs-lookup"><span data-stu-id="808e9-186">For more information, see [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880).</span></span>
> 
> 

1. <span data-ttu-id="808e9-187">Dans **Outils**, cliquez sur **Open Android Emulator Manager**, sélectionnez votre appareil, puis cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="808e9-187">From **Tools**, click **Open Android Emulator Manager**, select your device, and then click **Edit**.</span></span>
   
      ![][18]
2. <span data-ttu-id="808e9-188">Sélectionnez **API Google** dans **Cible**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="808e9-188">Select **Google APIs** in **Target**, and then click **OK**.</span></span>
   
      ![][19]
3. <span data-ttu-id="808e9-189">Dans la barre d'outils supérieure, cliquez sur **Exécuter**, puis sélectionnez votre application.</span><span class="sxs-lookup"><span data-stu-id="808e9-189">On the top toolbar, click **Run**, and then select your app.</span></span> <span data-ttu-id="808e9-190">L’émulateur démarre et l’application est exécutée.</span><span class="sxs-lookup"><span data-stu-id="808e9-190">This starts the emulator and runs the app.</span></span>
   
   <span data-ttu-id="808e9-191">L'application extrait le *registrationId* de GCM et s'inscrit auprès du notification hub.</span><span class="sxs-lookup"><span data-stu-id="808e9-191">The app retrieves the *registrationId* from GCM and registers with the notification hub.</span></span>

## <a name="send-notifications-from-your-backend"></a><span data-ttu-id="808e9-192">Envoi de notifications à partir de votre serveur principal</span><span class="sxs-lookup"><span data-stu-id="808e9-192">Send notifications from your backend</span></span>
<span data-ttu-id="808e9-193">Vous pouvez tester la réception de notifications dans votre application en envoyant des notifications dans le [portail Azure Classic] via l’onglet Déboguer du hub de notification, comme indiqué dans l’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="808e9-193">You can test receiving notifications in your app by sending notifications in the [Azure Classic Portal] via the debug tab on the notification hub, as shown in the screen below.</span></span>

![][30]

<span data-ttu-id="808e9-194">Les notifications Push sont normalement envoyées dans un service principal tel que Mobile Services ou ASP.NET par le biais d’une bibliothèque compatible.</span><span class="sxs-lookup"><span data-stu-id="808e9-194">Push notifications are normally sent in a backend service like Mobile Services or ASP.NET through a compatible library.</span></span> <span data-ttu-id="808e9-195">Vous pouvez également utiliser l’API REST directement pour envoyer des messages de notification si aucune bibliothèque n’est disponible pour votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="808e9-195">You can also use the REST API directly to send notification messages if a library is not available for your backend.</span></span>

<span data-ttu-id="808e9-196">La liste ci-dessous répertorie certains autres didacticiels que vous pouvez consulter pour envoyer des notifications :</span><span class="sxs-lookup"><span data-stu-id="808e9-196">Here is a list of some other tutorials that you may want to review for sending notifications:</span></span>

* <span data-ttu-id="808e9-197">ASP.NET : consultez [Utilisation des Notification Hubs pour envoyer des notifications Push aux utilisateurs].</span><span class="sxs-lookup"><span data-stu-id="808e9-197">ASP.NET: See [Use Notification Hubs to push notifications to users].</span></span>
* <span data-ttu-id="808e9-198">Kit de développement logiciel (SDK) Java pour Azure Notification Hubs : consultez [Utilisation de Notification Hubs à partir de Java](notification-hubs-java-push-notification-tutorial.md) pour envoyer des notifications depuis Java.</span><span class="sxs-lookup"><span data-stu-id="808e9-198">Azure Notification Hubs Java SDK: See [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) for sending notifications from Java.</span></span> <span data-ttu-id="808e9-199">Il a été testé dans Eclipse pour le développement Android.</span><span class="sxs-lookup"><span data-stu-id="808e9-199">This has been tested in Eclipse for Android Development.</span></span>
* <span data-ttu-id="808e9-200">PHP : [Utilisation de Notification Hubs à partir de PHP](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="808e9-200">PHP: See [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

<span data-ttu-id="808e9-201">Dans les prochaines sous-sections de ce didacticiel, vous envoyez des notifications avec une application console .NET et en utilisant un service mobile avec un script de noeud.</span><span class="sxs-lookup"><span data-stu-id="808e9-201">In the next subsections of the tutorial, you send notifications by using a .NET console app, and by using a mobile service through a node script.</span></span>

#### <a name="optional-send-notifications-by-using-a-net-app"></a><span data-ttu-id="808e9-202">(Facultatif) Pour envoyer des notifications en utilisant une application .NET :</span><span class="sxs-lookup"><span data-stu-id="808e9-202">(Optional) Send notifications by using a .NET app</span></span>
<span data-ttu-id="808e9-203">Dans cette section, nous allons envoyer des notifications à l’aide d’une application de console .NET.</span><span class="sxs-lookup"><span data-stu-id="808e9-203">In this section, we will send notifications by using a .NET console app</span></span>

1. <span data-ttu-id="808e9-204">Créez une application console Visual C# :</span><span class="sxs-lookup"><span data-stu-id="808e9-204">Create a new Visual C# console application:</span></span>
   
      ![][20]
2. <span data-ttu-id="808e9-205">Dans Visual Studio, cliquez successivement sur **Outils**, **Gestionnaire de package NuGet** et **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="808e9-205">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="808e9-206">La console du gestionnaire de package s’affiche dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="808e9-206">This displays the Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="808e9-207">Dans la fenêtre Console du gestionnaire de package, choisissez **Projet par défaut** comme nouveau projet d’application console, puis exécutez la commande suivante dans la fenêtre de console :</span><span class="sxs-lookup"><span data-stu-id="808e9-207">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="808e9-208">Cette opération ajoute une référence au Kit de développement logiciel (SDK) Azure Notification Hubs à l’aide du <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="808e9-208">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="808e9-209">Ouvrez le fichier Program.cs et ajoutez l’instruction `using` suivante :</span><span class="sxs-lookup"><span data-stu-id="808e9-209">Open the Program.cs file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="808e9-210">Dans votre classe `Program` , ajoutez la méthode suivante.</span><span class="sxs-lookup"><span data-stu-id="808e9-210">In your `Program` class, add the following method.</span></span> <span data-ttu-id="808e9-211">Mettez à jour le texte d’espace réservé avec la chaîne de connexion *DefaultFullSharedAccessSignature* et le nom de votre concentrateur du [portail Azure Classic].</span><span class="sxs-lookup"><span data-stu-id="808e9-211">Update the placeholder text with your *DefaultFullSharedAccessSignature* connection string and hub name from the [Azure Classic Portal].</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. <span data-ttu-id="808e9-212">Ajoutez les lignes suivantes dans votre méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="808e9-212">Add the following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="808e9-213">Appuyez sur la touche F5 pour exécuter l'application.</span><span class="sxs-lookup"><span data-stu-id="808e9-213">Press the F5 key to run the app.</span></span> <span data-ttu-id="808e9-214">Vous devez recevoir une notification dans l’application.</span><span class="sxs-lookup"><span data-stu-id="808e9-214">You should receive a notification in the app.</span></span>
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a><span data-ttu-id="808e9-215">(Facultatif) Envoyer une notification à l’aide d’un service mobile</span><span class="sxs-lookup"><span data-stu-id="808e9-215">(Optional) Send notifications by using a mobile service</span></span>
1. <span data-ttu-id="808e9-216">Suivez les procédures [Prise en main de Mobile Services].</span><span class="sxs-lookup"><span data-stu-id="808e9-216">Follow [Get started with Mobile Services].</span></span>
2. <span data-ttu-id="808e9-217">Connectez-vous au [portail Azure Classic], puis sélectionnez votre service mobile.</span><span class="sxs-lookup"><span data-stu-id="808e9-217">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
3. <span data-ttu-id="808e9-218">Sélectionnez l’onglet **Scheduler** dans la partie supérieure.</span><span class="sxs-lookup"><span data-stu-id="808e9-218">Select the **Scheduler** tab on the top.</span></span>
   
      ![][22]
4. <span data-ttu-id="808e9-219">Créez un travail planifié, insérez un nom, puis sélectionnez **On demand**.</span><span class="sxs-lookup"><span data-stu-id="808e9-219">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
      ![][23]
5. <span data-ttu-id="808e9-220">Lorsque le travail est créé, cliquez sur son nom.</span><span class="sxs-lookup"><span data-stu-id="808e9-220">When the job is created, click the job name.</span></span> <span data-ttu-id="808e9-221">Cliquez ensuite sur l’onglet **Script** dans la barre supérieure.</span><span class="sxs-lookup"><span data-stu-id="808e9-221">Then click the **Script** tab on the top bar.</span></span>
6. <span data-ttu-id="808e9-222">Insérez le script suivant dans votre fonction Scheduler.</span><span class="sxs-lookup"><span data-stu-id="808e9-222">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="808e9-223">Remplacez les espaces réservés par le nom de votre concentrateur de notification et la chaîne de connexion pour *DefaultFullSharedAccessSignature* obtenue précédemment.</span><span class="sxs-lookup"><span data-stu-id="808e9-223">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="808e9-224">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="808e9-224">Click **Save**.</span></span>
   
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
7. <span data-ttu-id="808e9-225">Cliquez sur **Exécuter une fois** sur la barre inférieure.</span><span class="sxs-lookup"><span data-stu-id="808e9-225">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="808e9-226">Vous devez recevoir une notification toast.</span><span class="sxs-lookup"><span data-stu-id="808e9-226">You should receive a toast notification.</span></span>

## <a name="next-steps"></a><span data-ttu-id="808e9-227">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="808e9-227">Next steps</span></span>
<span data-ttu-id="808e9-228">Dans cet exemple simple, vous avez diffusé des notifications à tous vos appareils Android.</span><span class="sxs-lookup"><span data-stu-id="808e9-228">In this simple example, you broadcasted notifications to all your Android devices.</span></span> <span data-ttu-id="808e9-229">Pour cibler certains utilisateurs, reportez-vous au didacticiel [Utilisation des Notification Hubs pour envoyer des notifications Push aux utilisateurs].</span><span class="sxs-lookup"><span data-stu-id="808e9-229">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="808e9-230">Pour segmenter vos utilisateurs par groupes d'intérêt, consultez la page [Utilisation des Notification Hubs pour diffuser les dernières nouvelles].</span><span class="sxs-lookup"><span data-stu-id="808e9-230">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="808e9-231">Pour plus d’informations sur l’utilisation de Notification Hubs, consultez [Recommandations relatives à Notification Hubs] et [Procédures Notification Hubs pour Android].</span><span class="sxs-lookup"><span data-stu-id="808e9-231">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for Android].</span></span>

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app to the Notification Hub]: #connecting-app
[Run your app with the emulator]: #run-app
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
<span data-ttu-id="808e9-232">[Prise en main de Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service</span><span class="sxs-lookup"><span data-stu-id="808e9-232">[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service</span></span>
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

<span data-ttu-id="808e9-233">[portail Azure Classic]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="808e9-233">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
<span data-ttu-id="808e9-234">[Recommandations relatives à Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="808e9-234">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="808e9-235">[Procédures Notification Hubs pour Android]: http://msdn.microsoft.com/library/dn282661.aspx</span><span class="sxs-lookup"><span data-stu-id="808e9-235">[Notification Hubs How-To for Android]: http://msdn.microsoft.com/library/dn282661.aspx</span></span>

<span data-ttu-id="808e9-236">[Utilisation des Notification Hubs pour envoyer des notifications Push aux utilisateurs]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="808e9-236">[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="808e9-237">[Utilisation des Notification Hubs pour diffuser les dernières nouvelles]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="808e9-237">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
<span data-ttu-id="808e9-238">[Composant Client Google Cloud Messaging]: http://components.xamarin.com/view/GCMClient/</span><span class="sxs-lookup"><span data-stu-id="808e9-238">[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/</span></span>
<span data-ttu-id="808e9-239">[Composant Azure Messaging]: http://components.xamarin.com/view/azure-messaging</span><span class="sxs-lookup"><span data-stu-id="808e9-239">[Azure Messaging Component]: http://components.xamarin.com/view/azure-messaging</span></span>
