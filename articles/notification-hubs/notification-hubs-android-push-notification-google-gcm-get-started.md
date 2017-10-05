---
title: Envoi de notifications Push vers Android avec Azure Notification Hubs | Microsoft Docs
description: "Dans ce didacticiel, vous découvrirez comment utiliser Azure Notification Hubs pour envoyer des notifications Push à une application Android."
services: notification-hubs
documentationcenter: android
keywords: notifications push,notification push,notification push android
author: ysxu
manager: erikre
editor: 
ms.assetid: 8268c6ef-af63-433c-b14e-a20b04a0342a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/05/2016
ms.author: yuaxu
ms.openlocfilehash: 808fc10ef1ebb3288facbdf2e9e817b27d4fc6bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-android-with-azure-notification-hubs"></a><span data-ttu-id="a1a0e-104">Envoi de notifications Push vers Android avec Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="a1a0e-104">Sending push notifications to Android with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="a1a0e-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a1a0e-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a1a0e-106">Cette rubrique explique les notifications Push avec Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-106">This topic demonstrates push notifications with Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="a1a0e-107">Si vous utilisez encore Firebase Cloud Messaging (FCM) de Google, consultez [Sending push notifications to Android with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md)(Envoi de notifications Push vers Android avec Azure Notification Hubs et FCM).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-107">If you are using Google's Firebase Cloud Messaging (FCM), see [Sending push notifications to Android with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="a1a0e-108">Ce didacticiel montre comment utiliser Azure Notification Hubs pour envoyer des notifications Push vers une application Android.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-108">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an Android application.</span></span>
<span data-ttu-id="a1a0e-109">Vous allez créer une application Android vide qui reçoit des notifications Push à l’aide de Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-109">You'll create a blank Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="a1a0e-110">Le code complet de ce didacticiel peut être téléchargé depuis GitHub [ici](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-110">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1a0e-111">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="a1a0e-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a1a0e-112">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a1a0e-113">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a1a0e-114">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

<span data-ttu-id="a1a0e-115">En plus du compte Azure actif mentionné ci-dessus, ce didacticiel requiert uniquement la dernière version d’ [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-115">In addition to an active Azure account mentioned above, this tutorial only requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>

<span data-ttu-id="a1a0e-116">Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels Notification Hubs pour les applications Android.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-116">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a><span data-ttu-id="a1a0e-117">Création d’un projet prenant en charge Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="a1a0e-117">Creating a project that supports Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="a1a0e-118">Configurer un nouveau hub de notification</span><span class="sxs-lookup"><span data-stu-id="a1a0e-118">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="a1a0e-119">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-119">&emsp;&emsp;6.</span></span>   <span data-ttu-id="a1a0e-120">Dans le panneau **Paramètres**, sélectionnez **Notification Services**, puis **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-120">In the **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="a1a0e-121">Entrez la clé d’API et cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-121">Enter the API key and click **Save**.</span></span>

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="a1a0e-123">Votre hub de notification est à présent configuré pour GCM, et vous disposez des chaînes de connexion vous permettant d’inscrire votre application pour la réception et l’envoi de notifications Push.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-123">Your notification hub is now configured to work with GCM, and you have the connection strings to both register your app to receive and send push notifications.</span></span>

## <span data-ttu-id="a1a0e-124"><a id="connecting-app"></a>Connexion de votre application au hub de notification</span><span class="sxs-lookup"><span data-stu-id="a1a0e-124"><a id="connecting-app"></a>Connect your app to the notification hub</span></span>
### <a name="create-a-new-android-project"></a><span data-ttu-id="a1a0e-125">Créer un projet Android</span><span class="sxs-lookup"><span data-stu-id="a1a0e-125">Create a new Android project</span></span>
1. <span data-ttu-id="a1a0e-126">Dans Android Studio, démarrez un nouveau projet Android Studio.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-126">In Android Studio, start a new Android Studio project.</span></span>
   
   ![Android Studio - nouveau projet][13]
2. <span data-ttu-id="a1a0e-128">Choisissez le format **Phone and Tablet** (Téléphone et tablette) et le **Minimum SDK** (SDK minimal) que vous voulez prendre en charge.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-128">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span></span> <span data-ttu-id="a1a0e-129">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-129">Then click **Next**.</span></span>
   
   ![Android Studio - workflow de création de projet][14]
3. <span data-ttu-id="a1a0e-131">Choisissez **Empty Activity** (Activité vide) comme activité principale, cliquez sur **Next** (Suivant), puis sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-131">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span></span>

### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="a1a0e-132">Ajout de services Google Play au projet</span><span class="sxs-lookup"><span data-stu-id="a1a0e-132">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="a1a0e-133">Ajout de bibliothèques de concentrateurs de notification Azure</span><span class="sxs-lookup"><span data-stu-id="a1a0e-133">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="a1a0e-134">Dans le fichier `Build.Gradle` de **l’application**, dans la section **dépendances**, ajoutez les lignes suivantes.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-134">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="a1a0e-135">Ajoutez le référentiel suivant après la section **dépendances** .</span><span class="sxs-lookup"><span data-stu-id="a1a0e-135">Add the following repository after the **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-the-androidmanifestxml"></a><span data-ttu-id="a1a0e-136">Mise à jour du fichier AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-136">Updating the AndroidManifest.xml.</span></span>
1. <span data-ttu-id="a1a0e-137">Pour prendre en charge GCM, nous devons implémenter un service d’écoute d’ID d’instance dans notre code afin d’[obtenir des jetons d’inscription](https://developers.google.com/cloud-messaging/android/client#sample-register) à l’aide de l’[API d’ID d’instance Google](https://developers.google.com/instance-id/).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-137">To support GCM, we must implement a Instance ID listener service in our code which is used to [obtain registration tokens](https://developers.google.com/cloud-messaging/android/client#sample-register) using [Google's Instance ID API](https://developers.google.com/instance-id/).</span></span> <span data-ttu-id="a1a0e-138">Dans ce didacticiel, nous nommerons la classe `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-138">In this tutorial we will name the class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="a1a0e-139">Ajoutez la définition de service suivante au fichier AndroidManifest.xml, dans la balise `<application>` .</span><span class="sxs-lookup"><span data-stu-id="a1a0e-139">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="a1a0e-140">Remplacez l’espace réservé `<your package>` par le nom de votre package actuel, qui apparaît en haut du fichier `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-140">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="a1a0e-141">Une fois que nous avons reçu notre jeton d’inscription GCM de la part de l’API d’ID d’instance, nous l’utiliserons pour nous [inscrire auprès d’Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-141">Once we have received our GCM registration token from the Instance ID API, we will use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="a1a0e-142">Nous effectuerons cette inscription en arrière-plan à l'aide d'un élément `IntentService` nommé `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-142">We will support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="a1a0e-143">Ce service gère également [l'actualisation de notre jeton d'inscription GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-143">This service will also be responsible for [refreshing our GCM registration token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span></span>
   
    <span data-ttu-id="a1a0e-144">Ajoutez la définition de service suivante au fichier AndroidManifest.xml, dans la balise `<application>` .</span><span class="sxs-lookup"><span data-stu-id="a1a0e-144">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="a1a0e-145">Remplacez l’espace réservé `<your package>` par le nom de votre package actuel, qui apparaît en haut du fichier `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-145">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span> 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="a1a0e-146">Nous allons également définir le destinataire qui recevra les des notifications.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-146">We will also define a receiver to receive notifications.</span></span> <span data-ttu-id="a1a0e-147">Ajoutez la définition de destinataire suivante au fichier AndroidManifest.xml, dans la balise `<application>` .</span><span class="sxs-lookup"><span data-stu-id="a1a0e-147">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="a1a0e-148">Remplacez l’espace réservé `<your package>` par le nom de votre package actuel, qui apparaît en haut du fichier `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-148">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="a1a0e-149">Ajoutez les autorisations nécessaires liées à GCM sous la balise `</application>`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-149">Add the following necessary GCM related permissions below the  `</application>` tag.</span></span> <span data-ttu-id="a1a0e-150">Veillez à remplacer `<your package>` par le nom du package qui apparaît en haut du fichier `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-150">Make sure to replace `<your package>` with the package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="a1a0e-151">Pour plus d’informations sur ces autorisations, consultez la rubrique [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest)(Configuration d’une application cliente GCM pour Android).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-151">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a><span data-ttu-id="a1a0e-152">Ajout de code</span><span class="sxs-lookup"><span data-stu-id="a1a0e-152">Adding code</span></span>
1. <span data-ttu-id="a1a0e-153">Dans la vue du projet, développez **app** > **src** > **main** > **java**.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-153">In the Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="a1a0e-154">Cliquez avec le bouton droit sur le dossier de votre package sous **java**, cliquez sur **Nouveau**, puis sur **Classe Java**.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-154">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="a1a0e-155">Ajoutez une nouvelle classe nommée `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-155">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - nouvelle classe Java][6]
   
    <span data-ttu-id="a1a0e-157">Veillez à mettre à jour ces trois espaces réservés dans le code suivant pour la classe `NotificationSettings` :</span><span class="sxs-lookup"><span data-stu-id="a1a0e-157">Make sure to update the these three placeholders in the following code for the `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="a1a0e-158">**SenderId**: numéro de projet que vous avez obtenu précédemment dans la [Google Cloud Console](http://cloud.google.com/console).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-158">**SenderId**: The project number you obtained earlier in the [Google Cloud Console](http://cloud.google.com/console).</span></span>
   * <span data-ttu-id="a1a0e-159">**HubListenConnectionString** : chaîne de connexion **DefaultListenAccessSignature** de votre hub.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-159">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="a1a0e-160">Vous pouvez copier cette chaîne de connexion en cliquant sur **Stratégies d’accès** dans le panneau **Paramètres** de votre hub dans le [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="a1a0e-160">You can copy that connection string by clicking **Access Policies** on the **Settings** blade of your hub on the [Azure Portal].</span></span>
   * <span data-ttu-id="a1a0e-161">**HubName**: utilisez le nom de votre hub de notification qui s’affiche dans le panneau Hub sur le [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="a1a0e-161">**HubName**: Use the name of your notification hub that appears in the hub blade in the [Azure Portal].</span></span>
     
     <span data-ttu-id="a1a0e-162">`NotificationSettings` code :</span><span class="sxs-lookup"><span data-stu-id="a1a0e-162">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="a1a0e-163">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="a1a0e-163">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       <span data-ttu-id="a1a0e-164">}</span><span class="sxs-lookup"><span data-stu-id="a1a0e-164">}</span></span>
2. <span data-ttu-id="a1a0e-165">À l’aide de la procédure ci-dessus, ajoutez une autre nouvelle classe nommée `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-165">Using the steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="a1a0e-166">Il s'agira de notre implémentation de service d'écouteur d'ID d'instance.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-166">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="a1a0e-167">Le code de cette classe appellera notre `IntentService` pour [actualiser le jeton GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-167">The code for this class will call our `IntentService` to [refresh the GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.android.gms.iid.InstanceIDListenerService;

        public class MyInstanceIDService extends InstanceIDListenerService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.i(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="a1a0e-168">Ajoutez à votre projet une autre nouvelle classe nommée `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-168">Add another new class to your project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="a1a0e-169">Il s’agit de l’implémentation de notre `IntentService` qui gère l’[actualisation du jeton GCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) et l’[inscription auprès du hub de notification](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-169">This will be the implementation for our `IntentService` that will handle [refreshing the GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="a1a0e-170">Utilisez le code suivant pour cette classe.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-170">Use the following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.google.android.gms.iid.InstanceID;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {        
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
   
                try {
                    InstanceID instanceID = InstanceID.getInstance(this);
                    String token = instanceID.getToken(NotificationSettings.SenderId,
                            GoogleCloudMessaging.INSTANCE_ID_SCOPE);        
                    Log.i(TAG, "Got GCM Registration Token: " + token);
   
                    // Storing the registration id that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting to register with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed to complete token refresh", e);
                    // If an exception happens while fetching the new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt the update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="a1a0e-171">Dans votre classe `MainActivity`, ajoutez les instructions `import` suivantes au-dessus de la déclaration de la classe.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-171">In your `MainActivity` class, add the following `import` statements above the class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="a1a0e-172">Ajoutez les membres privés suivants dans la partie supérieure de la classe.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-172">Add the following private members at the top of the class.</span></span> <span data-ttu-id="a1a0e-173">Nous les utiliserons pour [vérifier la disponibilité des services Google Play comme recommandé par Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-173">We will use these [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="a1a0e-174">Dans votre classe `MainActivity` , ajoutez la méthode suivante à la disponibilité des services Google Play.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-174">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span></span> 
   
        /**
         * Check the device to make sure it has the Google Play Services APK. If
         * it doesn't, display a dialog that allows users to download the APK from
         * the Google Play Store or enable it in the device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. <span data-ttu-id="a1a0e-175">Dans votre classe `MainActivity`, ajoutez le code suivant pour rechercher les services Google Play avant d’appeler votre `IntentService` pour obtenir votre jeton d’inscription GCM et vous inscrire auprès de votre hub de notification.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-175">In your `MainActivity` class, add the following code that will check for Google Play Services before calling your `IntentService` to get your GCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService to register this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="a1a0e-176">Dans la méthode `OnCreate` de la classe `MainActivity`, ajoutez le code suivant pour lancer le processus d’inscription lorsque l’activité est créée.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-176">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="a1a0e-177">Ajoutez ces méthodes supplémentaires à `MainActivity` pour vérifier l’état de l’application et afficher un rapport dans votre application.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-177">Add these additional methods to the `MainActivity` to verify app state and report status in your app.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. <span data-ttu-id="a1a0e-178">La méthode `ToastNotify` utilise le contrôle *« Hello World »* `TextView` pour afficher en permanence un rapport d’état et des notifications dans l’application.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-178">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span></span> <span data-ttu-id="a1a0e-179">Dans votre disposition activity_main.xml, ajoutez l'ID suivant pour ce contrôle.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-179">In your activity_main.xml layout, add the following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="a1a0e-180">Nous allons maintenant ajouter une sous-classe pour le destinataire que nous avons défini dans le fichier AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-180">Next we will add a subclass for our receiver we defined in the AndroidManifest.xml.</span></span> <span data-ttu-id="a1a0e-181">Ajoutez à votre projet une autre nouvelle classe nommée `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-181">Add another new class to your project named `MyHandler`.</span></span>
10. <span data-ttu-id="a1a0e-182">Ajoutez les instructions d’importation suivantes au-dessus de `MyHandler.java` :</span><span class="sxs-lookup"><span data-stu-id="a1a0e-182">Add the following import statements at the top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="a1a0e-183">Ajoutez le code suivant pour la classe `MyHandler` afin d’en faire une sous-classe de `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-183">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="a1a0e-184">Comme ce code remplace la méthode `OnReceive` , le gestionnaire rapporte les notifications reçues.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-184">This code overrides the `OnReceive` method, so the handler will report notifications that are received.</span></span> <span data-ttu-id="a1a0e-185">Le gestionnaire envoie également la notification Push au gestionnaire de notifications Android en utilisant la méthode `sendNotification()` .</span><span class="sxs-lookup"><span data-stu-id="a1a0e-185">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span></span> <span data-ttu-id="a1a0e-186">La méthode `sendNotification()` doit être exécutée quand l’application n’est pas en cours d’exécution et qu’une notification est reçue.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-186">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span></span>
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. <span data-ttu-id="a1a0e-187">Dans Android Studio, sur la barre de menus, cliquez sur **Build** > **Rebuild Project** pour vérifier que votre code ne contient aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-187">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="a1a0e-188">Envoi de notifications Push</span><span class="sxs-lookup"><span data-stu-id="a1a0e-188">Sending push notifications</span></span>
<span data-ttu-id="a1a0e-189">Vous pouvez tester la réception de notifications dans votre application en les envoyant via le [portail Azure] (observez la section **Dépannage** dans le panneau Hub, comme illustré ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-189">You can test receiving push notifications in your app by sending them via the [Azure Portal] - look for the **Troubleshooting** Section in the hub blade, as shown below.</span></span>

![Azure Notification Hubs - Test d’envoi](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-the-app"></a><span data-ttu-id="a1a0e-191">(Facultatif) Envoyer des notifications Push directement depuis l’application</span><span class="sxs-lookup"><span data-stu-id="a1a0e-191">(Optional) Send push notifications directly from the app</span></span>
<span data-ttu-id="a1a0e-192">En règle générale, vous devez envoyer des notifications à l'aide d'un serveur principal.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-192">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="a1a0e-193">Dans la plupart des cas, vous chercherez peut-être à envoyer des notifications Push directement à partir de l’application cliente.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-193">For some cases, you might want to be able to send push notifications directly from the client application.</span></span> <span data-ttu-id="a1a0e-194">Cette section explique comment envoyer des notifications à partir du client avec [l’API REST d’Azure Notification Hub](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-194">This section explains how to send notifications from the client using the [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="a1a0e-195">Dans la vue de projet Android Studio, développez **App** > **src** > **main** > **res** > **layout**.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-195">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="a1a0e-196">Ouvrez le fichier de disposition `activity_main.xml` et cliquez sur l’onglet **Texte** pour mettre à jour le texte du fichier.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-196">Open the `activity_main.xml` layout file and click the **Text** tab to update the text contents of the file.</span></span> <span data-ttu-id="a1a0e-197">Mettez-le à jour avec le code suivant, qui ajoute de nouveaux contrôles `Button` et `EditText` pour l’envoi de messages de notification Push au hub de notification.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-197">Update it with the code below, which adds new `Button` and `EditText` controls for sending push notification messages to the notification hub.</span></span> <span data-ttu-id="a1a0e-198">Ajoutez ce code en bas, juste avant `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-198">Add this code at the bottom, just before `</RelativeLayout>`.</span></span>
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. <span data-ttu-id="a1a0e-199">Dans la vue de projet Android Studio, développez **App** > **src** > **main** > **res** > **values**.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="a1a0e-200">Ouvrez le fichier `strings.xml` et ajoutez les valeurs de chaîne référencées par les nouveaux contrôles `Button` et `EditText`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-200">Open the `strings.xml` file and add the string values that are referenced by the new `Button` and `EditText` controls.</span></span> <span data-ttu-id="a1a0e-201">Ajoutez-les en bas du fichier juste avant `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-201">Add these at the bottom of the file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="a1a0e-202">Dans votre fichier `NotificationSetting.java`, ajoutez le paramètre suivant à la classe `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-202">In your `NotificationSetting.java` file, add the following setting to the `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="a1a0e-203">Mettez à jour `HubFullAccess` avec la chaîne de connexion **DefaultFullSharedAccessSignature** correspondant à votre hub.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-203">Update `HubFullAccess` with the **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="a1a0e-204">Vous pouvez copier cette chaîne de connexion à partir du [portail Azure] en cliquant sur **Stratégies d’accès** dans le panneau **Paramètres** de votre hub de notification.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-204">This connection string can be copied from the [Azure Portal] by clicking **Access Policies** on the **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. <span data-ttu-id="a1a0e-205">Dans votre fichier `MainActivity.java`, ajoutez les instructions `import` suivantes au-dessus de la classe `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-205">In your `MainActivity.java` file, add the following `import` statements above the `MainActivity` class.</span></span>
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. <span data-ttu-id="a1a0e-206">Dans votre fichier `MainActivity.java`, ajoutez les membres suivants au-dessus de la classe `MainActivity`.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-206">In your `MainActivity.java` file, add the following members at the top of the `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="a1a0e-207">Vous devez créer un jeton SaS (Software Access Signature) pour authentifier une demande POST d'envoi de messages à votre hub de notification.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-207">You must create a Software Access Signature (SaS) token to authenticate a POST request to send messages to your notification hub.</span></span> <span data-ttu-id="a1a0e-208">Cette opération est effectuée grâce à l’analyse des données clés de la chaîne de connexion, puis en créant le jeton SaS, comme indiqué sur la page [Concepts courants](http://msdn.microsoft.com/library/azure/dn495627.aspx) des informations de référence sur l’API REST.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-208">This is done by parsing the key data from the connection string and then creating the SaS token, as mentioned in the [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="a1a0e-209">Le code suivant est un exemple d'implémentation.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-209">The following code is an example implementation.</span></span>
   
    <span data-ttu-id="a1a0e-210">Dans `MainActivity.java`, ajoutez la méthode suivante à la classe `MainActivity` pour analyser votre chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-210">In `MainActivity.java`, add the following method to the `MainActivity` class to parse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * to parse the connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be the DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. <span data-ttu-id="a1a0e-211">Dans `MainActivity.java`, ajoutez la méthode suivante à la classe `MainActivity` pour créer un jeton d’authentification SaS.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-211">In `MainActivity.java`, add the following method to the `MainActivity` class to create a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from the access key to authenticate a request.
         *
         * @param uri The unencoded resource URI string for this operation. The resource
         *            URI is the full URI of the Service Bus resource to which access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from the raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute the hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. <span data-ttu-id="a1a0e-212">Dans `MainActivity.java`, ajoutez la méthode suivante à la classe `MainActivity` pour gérer le clic sur le bouton **Envoyer une notification** et envoyer le message de notification Push au hub à l’aide de l’API REST intégrée.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-212">In `MainActivity.java`, add the following method to the `MainActivity` class to handle the **Send Notification** button click and send the push notification message to the hub by using the built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added to the Authorization header on the POST request to the
         * notification hub. The text in the editTextNotificationMessage control
         * is added as the JSON body for the request to add a GCM message to the hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate the POST request with the SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a><span data-ttu-id="a1a0e-213">Test de votre application</span><span class="sxs-lookup"><span data-stu-id="a1a0e-213">Testing your app</span></span>
#### <a name="push-notifications-in-the-emulator"></a><span data-ttu-id="a1a0e-214">Notifications Push dans l’émulateur</span><span class="sxs-lookup"><span data-stu-id="a1a0e-214">Push notifications in the emulator</span></span>
<span data-ttu-id="a1a0e-215">Si vous souhaitez effectuer les tests de notifications Push sur un émulateur, vérifiez que votre image d’émulateur prend en charge le niveau d’API Google que vous avez choisi pour votre application.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-215">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span></span> <span data-ttu-id="a1a0e-216">Si votre image ne prend pas en charge les API Google natives, l’exception **SERVICE\_NOT\_AVAILABLE** est levée.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-216">If your image doesn't support native Google APIs, you will end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="a1a0e-217">Parallèlement à cela, assurez-vous que vous avez ajouté votre compte Google à l’émulateur en cours d’exécution sous **Paramètres** > **Comptes**(Envoi de notifications Push vers Android avec Azure Notification Hubs et GCM).</span><span class="sxs-lookup"><span data-stu-id="a1a0e-217">In addition to the above, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="a1a0e-218">Sinon, vos tentatives d’inscription auprès de GCM peuvent entraîner la levée de l’exception **AUTHENTICATION\_FAILED**.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-218">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="a1a0e-219">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="a1a0e-219">Running the application</span></span>
1. <span data-ttu-id="a1a0e-220">Exécutez l’application et notez qu’un ID d’inscription apparaît quand l’inscription réussit.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-220">Run the app and notice that the registration ID is reported for a successful registration.</span></span>
   
      ![Tests sur Android - Inscription de canal][18]
2. <span data-ttu-id="a1a0e-222">Entrez le message de notification à envoyer à tous les appareils Android inscrits auprès du hub.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-222">Enter a notification message to be sent to all Android devices that have registered with the hub.</span></span>
   
      ![Tests sur Android - envoi d’un message][19]

3. <span data-ttu-id="a1a0e-224">Appuyez sur **Envoyer une notification**.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-224">Press **Send Notification**.</span></span> <span data-ttu-id="a1a0e-225">Tous les appareils sur lesquels l’application est en cours d’exécution affichent une instance `AlertDialog` comportant le message de notification Push.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-225">Any devices that have the app running will show an `AlertDialog` instance with the push notification message.</span></span> <span data-ttu-id="a1a0e-226">Les appareils sur lesquels l’application n’est pas en cours d’exécution, mais qui ont déjà été inscrits aux notifications Push, reçoivent une notification dans le gestionnaire de notifications Android.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-226">Devices that don't have the app running but were previously registered for push notifications will receive a notification in the Android Notification Manager.</span></span> <span data-ttu-id="a1a0e-227">Vous pouvez afficher ces notifications en effectuant un balayage vers le bas depuis l’angle supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-227">Those can be viewed by swiping down from the upper-left corner.</span></span>
   
      ![Tests sur Android - notifications][21]

## <a name="next-steps"></a><span data-ttu-id="a1a0e-229">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a1a0e-229">Next steps</span></span>
<span data-ttu-id="a1a0e-230">Nous vous recommandons de consulter le didacticiel [Utiliser Notification Hubs pour envoyer des notifications Push aux utilisateurs] comme prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-230">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="a1a0e-231">Il vous expliquera comment envoyer des notifications à partir d’un serveur principal ASP.NET en utilisant des balises pour cibler des utilisateurs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="a1a0e-231">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="a1a0e-232">Pour segmenter vos utilisateurs par groupes d’intérêt, consultez le didacticiel [Utilisation des Notification Hubs pour diffuser les dernières nouvelles] .</span><span class="sxs-lookup"><span data-stu-id="a1a0e-232">If you want to segment your users by interest groups, check out the [Use Notification Hubs to send breaking news] tutorial.</span></span>

<span data-ttu-id="a1a0e-233">Pour obtenir des informations générales sur Notification Hubs, consultez nos [Recommandations relatives à Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="a1a0e-233">To learn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-android-get-started/notification-hub-android-new-class.png

[12]: ./media/notification-hubs-android-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-new-project.png
[14]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-choose-form-factor.png
[15]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app4.png
[16]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app5.png
[17]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app6.png

[18]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-registered.png
[19]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-set-message.png

[20]: ./media/notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-received-message.png
[22]: ./media/notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/notification-hubs-android-get-started/notification-hub-scheduler2.png
[29]: ./media/mobile-services-android-get-started-push/mobile-eclipse-import-Play-library.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png

[31]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-add-ui.png


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="a1a0e-234">[Recommandations relatives à Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="a1a0e-234">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="a1a0e-235">[Utiliser Notification Hubs pour envoyer des notifications Push aux utilisateurs]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span><span class="sxs-lookup"><span data-stu-id="a1a0e-235">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span></span>
<span data-ttu-id="a1a0e-236">[Utilisation des Notification Hubs pour diffuser les dernières nouvelles]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="a1a0e-236">[Use Notification Hubs to send breaking news]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span></span>
<span data-ttu-id="a1a0e-237">[portail Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="a1a0e-237">[Azure Portal]: https://portal.azure.com</span></span>
