---
title: aaaSending tooAndroid de notifications push avec Azure Notification Hubs et de la messagerie de Cloud Firebase | Documents Microsoft
description: "Dans ce didacticiel, vous apprendrez comment toouse Azure Notification Hubs et la messagerie de Cloud Firebase toopush notifications tooAndroid périphériques."
services: notification-hubs
documentationcenter: android
keywords: notifications push,notification push,notification push android,fcm,firebase cloud messaging
author: ysxu
manager: erikre
editor: 
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/14/2016
ms.author: yuaxu
ms.openlocfilehash: d2e57437ac7b0ef77abf048f991043620621e58d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a><span data-ttu-id="61013-104">Envoi de tooAndroid de notifications push avec Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="61013-104">Sending push notifications tooAndroid with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="61013-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="61013-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="61013-106">Cette rubrique explique les notifications Push avec Google Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="61013-106">This topic demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span></span> <span data-ttu-id="61013-107">Si vous utilisez encore Google Cloud Messaging (GCM), consultez [envoi tooAndroid de notifications push avec Azure Notification Hubs et GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="61013-107">If you are still using Google Cloud Messaging (GCM), see [Sending push notifications tooAndroid with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="61013-108">Ce didacticiel vous montre comment toouse Azure Notification Hubs et toosend de messagerie de Cloud Firebase push application Android tooan de notifications.</span><span class="sxs-lookup"><span data-stu-id="61013-108">This tutorial shows you how toouse Azure Notification Hubs and Firebase Cloud Messaging toosend push notifications tooan Android application.</span></span>
<span data-ttu-id="61013-109">Vous allez créer une application Android vide qui reçoit des notifications Push à l’aide de Firebase Cloud Messaging (FCM).</span><span class="sxs-lookup"><span data-stu-id="61013-109">You'll create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="61013-110">code Hello terminée pour ce didacticiel peut être téléchargé à partir de GitHub [ici](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span><span class="sxs-lookup"><span data-stu-id="61013-110">hello completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61013-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="61013-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="61013-112">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="61013-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="61013-113">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="61013-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="61013-114">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="61013-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

* <span data-ttu-id="61013-115">En outre tooan de compte Azure active mentionnés ci-dessus, ce didacticiel requiert la version la plus récente de hello [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span><span class="sxs-lookup"><span data-stu-id="61013-115">In addition tooan active Azure account mentioned above, this tutorial requires hello latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>
* <span data-ttu-id="61013-116">Android 2.3 ou ultérieure pour Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="61013-116">Android 2.3 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="61013-117">La révision 27 ou ultérieure du référentiel Google est requise pour Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="61013-117">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="61013-118">Services Google Play 9.0.2 ou version ultérieure pour Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="61013-118">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="61013-119">Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels Notification Hubs pour les applications Android.</span><span class="sxs-lookup"><span data-stu-id="61013-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="create-a-new-android-studio-project"></a><span data-ttu-id="61013-120">Créer un nouveau projet Android Studio</span><span class="sxs-lookup"><span data-stu-id="61013-120">Create a new Android Studio Project</span></span>
1. <span data-ttu-id="61013-121">Dans Android Studio, démarrez un nouveau projet Android Studio.</span><span class="sxs-lookup"><span data-stu-id="61013-121">In Android Studio, start a new Android Studio project.</span></span>
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. <span data-ttu-id="61013-122">Choisissez hello **téléphone et tablette** forment le facteur et hello **Minimum SDK** que vous souhaitez toosupport.</span><span class="sxs-lookup"><span data-stu-id="61013-122">Choose hello **Phone and Tablet** form factor and hello **Minimum SDK** that you want toosupport.</span></span> <span data-ttu-id="61013-123">Cliquez ensuite sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="61013-123">Then click **Next**.</span></span>
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. <span data-ttu-id="61013-124">Choisissez **activité vide** pour l’activité principale de hello, cliquez sur **suivant**, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="61013-124">Choose **Empty Activity** for hello main activity, click **Next**, and then click **Finish**.</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="61013-125">Créer un projet qui prend en charge Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="61013-125">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="61013-126">Configurer un nouveau hub de notification</span><span class="sxs-lookup"><span data-stu-id="61013-126">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="61013-127">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="61013-127">&emsp;&emsp;6.</span></span> <span data-ttu-id="61013-128">Bonjour **paramètres** Panneau de votre concentrateur de notification, sélectionnez **Notification Services** , puis **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="61013-128">In hello **Settings** blade of your notification hub, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="61013-129">Touche hello FCM server vous avez copiée précédemment à partir de hello [console de Firebase](https://firebase.google.com/console/) et cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="61013-129">Enter hello FCM server key you copied earlier from hello [Firebase console](https://firebase.google.com/console/) and click **Save**.</span></span>

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="61013-131">Votre concentrateur de notification est maintenant configuré toowork avec Firebase Cloud Messagin, et vous disposez tooboth de chaînes de connexion hello inscrire tooreceive de votre application et d’envoyer des notifications push.</span><span class="sxs-lookup"><span data-stu-id="61013-131">Your notification hub is now configured toowork with Firebase Cloud Messagin, and you have hello connection strings tooboth register your app tooreceive and send push notifications.</span></span>

## <span data-ttu-id="61013-132"><a id="connecting-app"></a>Se connecter à votre hub de notification d’application toohello</span><span class="sxs-lookup"><span data-stu-id="61013-132"><a id="connecting-app"></a>Connect your app toohello notification hub</span></span>
### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="61013-133">Ajouter un projet de toohello services Google Play</span><span class="sxs-lookup"><span data-stu-id="61013-133">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="61013-134">Ajout de bibliothèques de concentrateurs de notification Azure</span><span class="sxs-lookup"><span data-stu-id="61013-134">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="61013-135">Bonjour `Build.Gradle` fichier hello **application**, ajouter hello lignes Bonjour suivantes **dépendances** section.</span><span class="sxs-lookup"><span data-stu-id="61013-135">In hello `Build.Gradle` file for hello **app**, add hello following lines in hello **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="61013-136">Ajouter hello suivant référentiel après hello **dépendances** section.</span><span class="sxs-lookup"><span data-stu-id="61013-136">Add hello following repository after hello **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a><span data-ttu-id="61013-137">Mise à jour hello AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="61013-137">Updating hello AndroidManifest.xml.</span></span>
1. <span data-ttu-id="61013-138">toosupport FCM, nous devons implémenter un service d’écoute ID d’Instance dans notre code utilisé trop[obtenir des jetons d’inscription](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) à l’aide de [FirebaseInstanceId API de Google](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span><span class="sxs-lookup"><span data-stu-id="61013-138">toosupport FCM, we must implement a Instance ID listener service in our code which is used too[obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span></span> <span data-ttu-id="61013-139">Dans ce didacticiel, nous allons appeler classe hello `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="61013-139">In this tutorial we will name hello class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="61013-140">Ajouter hello service définition toohello AndroidManifest.xml le fichier suivant, à l’intérieur de hello `<application>` balise.</span><span class="sxs-lookup"><span data-stu-id="61013-140">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="61013-141">Une fois que nous avons reçu notre jeton d’inscription FCM de hello FirebaseInstanceId API, nous l’utiliserons trop[enregistrer avec hello Hub de Notification Azure](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="61013-141">Once we have received our FCM registration token from hello FirebaseInstanceId API, we will use it too[register with hello Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="61013-142">Nous prendrons en charge cette inscription à l’aide d’arrière-plan hello un `IntentService` nommé `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="61013-142">We will support this registration in hello background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="61013-143">Ce service gère également l’actualisation de notre jeton d’inscription FCM.</span><span class="sxs-lookup"><span data-stu-id="61013-143">This service will also be responsible for refreshing our FCM registration token.</span></span>
   
    <span data-ttu-id="61013-144">Ajouter hello service définition toohello AndroidManifest.xml le fichier suivant, à l’intérieur de hello `<application>` balise.</span><span class="sxs-lookup"><span data-stu-id="61013-144">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="61013-145">Nous allons également définir une notification de tooreceive récepteur.</span><span class="sxs-lookup"><span data-stu-id="61013-145">We will also define a receiver tooreceive notifications.</span></span> <span data-ttu-id="61013-146">Ajouter hello récepteur définition toohello AndroidManifest.xml le fichier suivant, à l’intérieur de hello `<application>` balise.</span><span class="sxs-lookup"><span data-stu-id="61013-146">Add hello following receiver definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="61013-147">Remplacez hello `<your package>` espace réservé avec hello votre nom de package réel indiqué en haut de hello Hello `AndroidManifest.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="61013-147">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="61013-148">Ajouter hello suivant nécessaire FCM liées autorisations ci-dessous hello `</application>` balise.</span><span class="sxs-lookup"><span data-stu-id="61013-148">Add hello following necessary FCM related permissions below hello  `</application>` tag.</span></span> <span data-ttu-id="61013-149">Assurez-vous que tooreplace `<your package>` avec le nom du package hello indiqué en haut de hello Hello `AndroidManifest.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="61013-149">Make sure tooreplace `<your package>` with hello package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="61013-150">Pour plus d’informations sur ces autorisations, consultez [le programme d’installation d’une application cliente de GCM pour Android](https://developers.google.com/cloud-messaging/android/client#manifest) et [migrer une application cliente de GCM pour Android tooFirebase messagerie Cloud](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span><span class="sxs-lookup"><span data-stu-id="61013-150">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android tooFirebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a><span data-ttu-id="61013-151">Ajout de code</span><span class="sxs-lookup"><span data-stu-id="61013-151">Adding code</span></span>
1. <span data-ttu-id="61013-152">Bonjour vue du projet, développez **application** > **src** > **principal** > **java**.</span><span class="sxs-lookup"><span data-stu-id="61013-152">In hello Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="61013-153">Cliquez avec le bouton droit sur le dossier de votre package sous **java**, cliquez sur **Nouveau**, puis sur **Classe Java**.</span><span class="sxs-lookup"><span data-stu-id="61013-153">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="61013-154">Ajoutez une nouvelle classe nommée `NotificationSettings`.</span><span class="sxs-lookup"><span data-stu-id="61013-154">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - nouvelle classe Java](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    <span data-ttu-id="61013-156">Assurez-vous que tooupdate hello ces trois espaces réservés dans hello suivant code hello `NotificationSettings` classe :</span><span class="sxs-lookup"><span data-stu-id="61013-156">Make sure tooupdate hello these three placeholders in hello following code for hello `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="61013-157">**ID d’expéditeur**: hello Id de l’expéditeur que vous avez obtenu précédemment dans hello **messagerie Cloud** onglet des paramètres de votre projet dans hello [console de Firebase](https://firebase.google.com/console/).</span><span class="sxs-lookup"><span data-stu-id="61013-157">**SenderId**: hello Sender Id you obtained earlier in hello **Cloud Messaging** tab of your project settings in hello [Firebase console](https://firebase.google.com/console/).</span></span>
   * <span data-ttu-id="61013-158">**HubListenConnectionString**: hello **DefaultListenAccessSignature** chaîne de connexion pour votre concentrateur.</span><span class="sxs-lookup"><span data-stu-id="61013-158">**HubListenConnectionString**: hello **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="61013-159">Vous pouvez copier cette chaîne de connexion en cliquant sur **des stratégies d’accès** sur hello **paramètres** Panneau de votre concentrateur sur hello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="61013-159">You can copy that connection string by clicking **Access Policies** on hello **Settings** blade of your hub on hello [Azure Portal].</span></span>
   * <span data-ttu-id="61013-160">**HubName**: utiliser le nom de votre concentrateur de notification qui s’affiche dans le panneau de concentrateur hello Bonjour hello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="61013-160">**HubName**: Use hello name of your notification hub that appears in hello hub blade in hello [Azure Portal].</span></span>
     
     <span data-ttu-id="61013-161">`NotificationSettings` code :</span><span class="sxs-lookup"><span data-stu-id="61013-161">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="61013-162">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="61013-162">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       <span data-ttu-id="61013-163">}</span><span class="sxs-lookup"><span data-stu-id="61013-163">}</span></span>
2. <span data-ttu-id="61013-164">À l’aide des étapes hello ci-dessus, ajoutez une autre classe nommée `MyInstanceIDService`.</span><span class="sxs-lookup"><span data-stu-id="61013-164">Using hello steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="61013-165">Il s'agira de notre implémentation de service d'écouteur d'ID d'instance.</span><span class="sxs-lookup"><span data-stu-id="61013-165">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="61013-166">code Hello pour cette classe appellera notre `IntentService` trop[jeton d’actualisation hello FCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="61013-166">hello code for this class will call our `IntentService` too[refresh hello FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in hello background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.firebase.iid.FirebaseInstanceIdService;

        public class MyInstanceIDService extends FirebaseInstanceIdService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.d(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="61013-167">Ajouter une autre classe tooyour projet nommé, `RegistrationIntentService`.</span><span class="sxs-lookup"><span data-stu-id="61013-167">Add another new class tooyour project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="61013-168">Il s’agit d’implémentation hello pour notre `IntentService` qui gérera [actualisation jeton FCM de hello](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) et [l’inscription auprès de hub de notification hello](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="61013-168">This will be hello implementation for our `IntentService` that will handle [refreshing hello FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with hello notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="61013-169">Utilisez hello suivant de code de cette classe.</span><span class="sxs-lookup"><span data-stu-id="61013-169">Use hello following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;        
        import com.google.firebase.iid.FirebaseInstanceId;
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
                String storedToken = null;
   
                try {
                    String FCM_token = FirebaseInstanceId.getInstance().getToken();
                    Log.d(TAG, "FCM Registration Token: " + FCM_token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    // Check if hello token may have been compromised and needs refreshing.
                    else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete registration", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="61013-170">Dans votre `MainActivity` de classe, ajoutez hello `import` instructions ci-dessus hello déclaration de classe.</span><span class="sxs-lookup"><span data-stu-id="61013-170">In your `MainActivity` class, add hello following `import` statements above hello class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="61013-171">Ajoutez hello suivant des membres privés haut hello de classe hello.</span><span class="sxs-lookup"><span data-stu-id="61013-171">Add hello following private members at hello top of hello class.</span></span> <span data-ttu-id="61013-172">Nous allons utiliser ces [vérifier la disponibilité de hello de Services Google Play comme recommandé par Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span><span class="sxs-lookup"><span data-stu-id="61013-172">We will use these [check hello availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="61013-173">Dans votre `MainActivity` de classe, ajoutez hello après disponibilité toohello de méthode de Services Google Play.</span><span class="sxs-lookup"><span data-stu-id="61013-173">In your `MainActivity` class, add hello following method toohello availability of Google Play Services.</span></span> 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
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
5. <span data-ttu-id="61013-174">Dans votre `MainActivity` de classe, ajoutez hello suivant code recherchera les Services Google Play avant d’appeler votre `IntentService` tooget votre jeton d’inscription FCM et l’inscrire auprès de votre concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="61013-174">In your `MainActivity` class, add hello following code that will check for Google Play Services before calling your `IntentService` tooget your FCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="61013-175">Bonjour `OnCreate` méthode Hello `MainActivity` de classe, ajoutez hello suivant le processus d’inscription de code toostart hello lorsque l’activité est créée.</span><span class="sxs-lookup"><span data-stu-id="61013-175">In hello `OnCreate` method of hello `MainActivity` class, add hello following code toostart hello registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="61013-176">Ajouter ces méthodes supplémentaires de toohello `MainActivity` tooverify état et les rapports état des applications dans votre application.</span><span class="sxs-lookup"><span data-stu-id="61013-176">Add these additional methods toohello `MainActivity` tooverify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="61013-177">Hello `ToastNotify` méthode utilise hello *« Hello World »* `TextView` contrôler tooreport état et les notifications de manière permanente dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="61013-177">hello `ToastNotify` method uses hello *"Hello World"* `TextView` control tooreport status and notifications persistently in hello app.</span></span> <span data-ttu-id="61013-178">Dans la mise en page activity_main.xml, ajoutez hello id pour ce contrôle suivant.</span><span class="sxs-lookup"><span data-stu-id="61013-178">In your activity_main.xml layout, add hello following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="61013-179">Ensuite, nous allons ajouter une sous-classe pour notre récepteur que nous avons défini Bonjour AndroidManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="61013-179">Next we will add a subclass for our receiver we defined in hello AndroidManifest.xml.</span></span> <span data-ttu-id="61013-180">Ajouter une autre classe tooyour projet nommé `MyHandler`.</span><span class="sxs-lookup"><span data-stu-id="61013-180">Add another new class tooyour project named `MyHandler`.</span></span>
10. <span data-ttu-id="61013-181">Ajouter hello suivant les instructions d’importation haut hello `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="61013-181">Add hello following import statements at hello top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="61013-182">Ajouter hello suivant code hello `MyHandler` classe rendant une sous-classe de `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span><span class="sxs-lookup"><span data-stu-id="61013-182">Add hello following code for hello `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="61013-183">Ce code substitue hello `OnReceive` méthode gestionnaire de hello signalera notifications qui ont été reçues.</span><span class="sxs-lookup"><span data-stu-id="61013-183">This code overrides hello `OnReceive` method, so hello handler will report notifications that are received.</span></span> <span data-ttu-id="61013-184">Gestionnaire de Hello envoie également un gestionnaire de notification Android hello push notifications toohello à l’aide de hello `sendNotification()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="61013-184">hello handler also sends hello push notification toohello Android notification manager by using hello `sendNotification()` method.</span></span> <span data-ttu-id="61013-185">Hello `sendNotification()` méthode doit être exécutée lors de l’application hello n’est pas en cours d’exécution et une notification est reçue.</span><span class="sxs-lookup"><span data-stu-id="61013-185">hello `sendNotification()` method should be executed when hello app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="61013-186">Dans Android Studio sur la barre de menus hello, cliquez sur **générer** > **régénérer le projet** toomake sûr qu’aucune erreur n’est présent dans votre code.</span><span class="sxs-lookup"><span data-stu-id="61013-186">In Android Studio on hello menu bar, click **Build** > **Rebuild Project** toomake sure that no errors are present in your code.</span></span>
13. <span data-ttu-id="61013-187">Exécutez l’application hello sur votre appareil et vérifier qu’il s’enregistre correctement avec le hub de notification hello.</span><span class="sxs-lookup"><span data-stu-id="61013-187">Run hello app on your device and verify it registers successfully with hello notification hub.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="61013-188">L’inscription peut échouer au démarrage initial de hello jusqu'à hello `onTokenRefresh()` méthode de service de l’Id d’instance est appelée.</span><span class="sxs-lookup"><span data-stu-id="61013-188">Registration may fail on hello initial launch until hello `onTokenRefresh()` method of instance Id service is called.</span></span> <span data-ttu-id="61013-189">actualisation de Hello doit initier une inscription réussie avec le hub de notification hello.</span><span class="sxs-lookup"><span data-stu-id="61013-189">hello refresh should intiate a successful registration with hello notification hub.</span></span>
    > 
    > 

## <a name="sending-push-notifications"></a><span data-ttu-id="61013-190">Envoi de notifications Push</span><span class="sxs-lookup"><span data-stu-id="61013-190">Sending push notifications</span></span>
<span data-ttu-id="61013-191">Vous pouvez tester de recevoir des notifications push dans votre application en les envoyant via hello [Azure Portal] -recherchez hello **dépannage** Section dans le panneau de concentrateur hello, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="61013-191">You can test receiving push notifications in your app by sending them via hello [Azure Portal] - look for hello **Troubleshooting** Section in hello hub blade, as shown below.</span></span>

![Azure Notification Hubs - Test d’envoi](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a><span data-ttu-id="61013-193">(Facultatif) Envoyer des notifications push directement à partir de l’application hello</span><span class="sxs-lookup"><span data-stu-id="61013-193">(Optional) Send push notifications directly from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="61013-194">Cet exemple montre comment envoyer des notifications à partir de l’application cliente de hello est fourni uniquement à des fins pédagogiques.</span><span class="sxs-lookup"><span data-stu-id="61013-194">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="61013-195">Étant donné que vous devrez hello `DefaultFullSharedAccessSignature` toobe présent sur l’application cliente de hello, il expose les risques de toohello de concentrateur de notification qu’un utilisateur peut obtenir les notifications d’accès non autorisé de toosend tooyour clients.</span><span class="sxs-lookup"><span data-stu-id="61013-195">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="61013-196">En règle générale, vous devez envoyer des notifications à l'aide d'un serveur principal.</span><span class="sxs-lookup"><span data-stu-id="61013-196">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="61013-197">Dans certains cas, vous pouvez choisir des notifications push de toosend en mesure de toobe directement à partir de l’application cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="61013-197">For some cases, you might want toobe able toosend push notifications directly from hello client application.</span></span> <span data-ttu-id="61013-198">Cette section explique comment les notifications toosend client hello à l’aide de hello [API REST de Azure Notification Hub](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="61013-198">This section explains how toosend notifications from hello client using hello [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="61013-199">Dans la vue de projet Android Studio, développez **App** > **src** > **main** > **res** > **layout**.</span><span class="sxs-lookup"><span data-stu-id="61013-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="61013-200">Ouvrez hello `activity_main.xml` mise en page, cliquez sur hello **texte** onglet tooupdate hello contenus de texte hello fichier.</span><span class="sxs-lookup"><span data-stu-id="61013-200">Open hello `activity_main.xml` layout file and click hello **Text** tab tooupdate hello text contents of hello file.</span></span> <span data-ttu-id="61013-201">Mettre à jour avec le code hello ci-dessous, qui ajoute de nouvelles `Button` et `EditText` contrôles pour l’envoi de poussée du hub de notification toohello notification messages.</span><span class="sxs-lookup"><span data-stu-id="61013-201">Update it with hello code below, which adds new `Button` and `EditText` controls for sending push notification messages toohello notification hub.</span></span> <span data-ttu-id="61013-202">Ajoutez ce code au bas de hello, juste avant `</RelativeLayout>`.</span><span class="sxs-lookup"><span data-stu-id="61013-202">Add this code at hello bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="61013-203">Dans la vue de projet Android Studio, développez **App** > **src** > **main** > **res** > **values**.</span><span class="sxs-lookup"><span data-stu-id="61013-203">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="61013-204">Ouvrez hello `strings.xml` et ajoutez les valeurs de chaîne hello qui sont référencés par hello nouvelle `Button` et `EditText` contrôles.</span><span class="sxs-lookup"><span data-stu-id="61013-204">Open hello `strings.xml` file and add hello string values that are referenced by hello new `Button` and `EditText` controls.</span></span> <span data-ttu-id="61013-205">Ajoutez ces bas hello du fichier de hello, juste avant `</resources>`.</span><span class="sxs-lookup"><span data-stu-id="61013-205">Add these at hello bottom of hello file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="61013-206">Dans votre `NotificationSetting.java` , ajoutez hello suivant paramètre toohello `NotificationSettings` classe.</span><span class="sxs-lookup"><span data-stu-id="61013-206">In your `NotificationSetting.java` file, add hello following setting toohello `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="61013-207">Mise à jour `HubFullAccess` avec hello **DefaultFullSharedAccessSignature** chaîne de connexion pour votre concentrateur.</span><span class="sxs-lookup"><span data-stu-id="61013-207">Update `HubFullAccess` with hello **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="61013-208">Cette chaîne de connexion peut être copiée à partir de hello [Azure Portal] en cliquant sur **des stratégies d’accès** sur hello **paramètres** panneau pour votre concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="61013-208">This connection string can be copied from hello [Azure Portal] by clicking **Access Policies** on hello **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. <span data-ttu-id="61013-209">Dans votre `MainActivity.java` , ajoutez les éléments suivants de hello `import` instructions ci-dessus hello `MainActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="61013-209">In your `MainActivity.java` file, add hello following `import` statements above hello `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="61013-210">Dans votre `MainActivity.java` , ajoutez hello suivant membres haut hello hello `MainActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="61013-210">In your `MainActivity.java` file, add hello following members at hello top of hello `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="61013-211">Un concentrateur de notification POST demande toosend messages tooyour, vous devez créer un tooauthenticate de jeton de Signature d’accès (SaS) du logiciel.</span><span class="sxs-lookup"><span data-stu-id="61013-211">You must create a Software Access Signature (SaS) token tooauthenticate a POST request toosend messages tooyour notification hub.</span></span> <span data-ttu-id="61013-212">Pour cela, l’analyse des données de clé hello à partir de la chaîne de connexion hello et puis en créant hello jeton SAP, comme indiqué dans hello [Concepts communs](http://msdn.microsoft.com/library/azure/dn495627.aspx) référence d’API REST.</span><span class="sxs-lookup"><span data-stu-id="61013-212">This is done by parsing hello key data from hello connection string and then creating hello SaS token, as mentioned in hello [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="61013-213">Hello suivant de code est un exemple d’implémentation.</span><span class="sxs-lookup"><span data-stu-id="61013-213">hello following code is an example implementation.</span></span>
   
    <span data-ttu-id="61013-214">Dans `MainActivity.java`, ajouter hello suivant de méthode toohello `MainActivity` classe tooparse votre chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="61013-214">In `MainActivity.java`, add hello following method toohello `MainActivity` class tooparse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
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
7. <span data-ttu-id="61013-215">Dans `MainActivity.java`, ajouter hello suivant de méthode toohello `MainActivity` classe toocreate un jeton d’authentification SAP.</span><span class="sxs-lookup"><span data-stu-id="61013-215">In `MainActivity.java`, add hello following method toohello `MainActivity` class toocreate a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
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
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
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
8. <span data-ttu-id="61013-216">Dans `MainActivity.java`, ajouter hello suivant de méthode toohello `MainActivity` hello toohandle de classe **envoyer une Notification** clic de bouton et envoyer une notification de push de hello concentrateur toohello de messages à l’aide de hello intégrés API REST.</span><span class="sxs-lookup"><span data-stu-id="61013-216">In `MainActivity.java`, add hello following method toohello `MainActivity` class toohandle hello **Send Notification** button click and send hello push notification message toohello hub by using hello built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
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
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
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

## <a name="testing-your-app"></a><span data-ttu-id="61013-217">Test de votre application</span><span class="sxs-lookup"><span data-stu-id="61013-217">Testing your app</span></span>
#### <a name="push-notifications-in-hello-emulator"></a><span data-ttu-id="61013-218">Notifications push dans l’émulateur de hello</span><span class="sxs-lookup"><span data-stu-id="61013-218">Push notifications in hello emulator</span></span>
<span data-ttu-id="61013-219">Si vous souhaitez que les notifications push tootest à l’intérieur d’un émulateur, assurez-vous que votre image de l’émulateur prend en charge le niveau d’API Google hello que vous avez choisie pour votre application.</span><span class="sxs-lookup"><span data-stu-id="61013-219">If you want tootest push notifications inside an emulator, make sure that your emulator image supports hello Google API level that you chose for your app.</span></span> <span data-ttu-id="61013-220">Si votre image ne prend pas en charge native APIs Google, vous obtiendrez des hello **SERVICE\_pas\_disponible** exception.</span><span class="sxs-lookup"><span data-stu-id="61013-220">If your image doesn't support native Google APIs, you will end up with hello **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="61013-221">En outre toohello ci-dessus, assurez-vous que vous avez ajouté votre tooyour de compte Google en cours d’exécution émulateur sous **paramètres** > **comptes**.</span><span class="sxs-lookup"><span data-stu-id="61013-221">In addition toohello above, ensure that you have added your Google account tooyour running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="61013-222">Dans le cas contraire, votre tooregister tentatives avec GCM peut entraîner hello **authentification\_n’a pas pu** exception.</span><span class="sxs-lookup"><span data-stu-id="61013-222">Otherwise, your attempts tooregister with GCM may result in hello **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-hello-application"></a><span data-ttu-id="61013-223">Exécution de l’application hello</span><span class="sxs-lookup"><span data-stu-id="61013-223">Running hello application</span></span>
1. <span data-ttu-id="61013-224">Exécutez l’application hello et notez que l’ID d’inscription hello est signalé pour une inscription réussie.</span><span class="sxs-lookup"><span data-stu-id="61013-224">Run hello app and notice that hello registration ID is reported for a successful registration.</span></span>
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. <span data-ttu-id="61013-225">Entrez un toobe de message de notification envoyé tooall les appareils Android qui ont été inscrits auprès de concentrateur de hello.</span><span class="sxs-lookup"><span data-stu-id="61013-225">Enter a notification message toobe sent tooall Android devices that have registered with hello hub.</span></span>
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. <span data-ttu-id="61013-226">Appuyez sur **Envoyer une notification**.</span><span class="sxs-lookup"><span data-stu-id="61013-226">Press **Send Notification**.</span></span> <span data-ttu-id="61013-227">Affichent tous les périphériques qui ont en cours d’exécution application hello un `AlertDialog` instance avec un message de notification push hello.</span><span class="sxs-lookup"><span data-stu-id="61013-227">Any devices that have hello app running will show an `AlertDialog` instance with hello push notification message.</span></span> <span data-ttu-id="61013-228">Les appareils qui n’ont pas en cours d’exécution application hello mais précédemment inscrits pour les notifications push recevra une notification Bonjour Gestionnaire de notifications Android.</span><span class="sxs-lookup"><span data-stu-id="61013-228">Devices that don't have hello app running but were previously registered for push notifications will receive a notification in hello Android Notification Manager.</span></span> <span data-ttu-id="61013-229">Celles peuvent être affichées par le glissement vers le bas à partir de l’angle supérieur gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="61013-229">Those can be viewed by swiping down from hello upper-left corner.</span></span>
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a><span data-ttu-id="61013-230">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61013-230">Next steps</span></span>
<span data-ttu-id="61013-231">Nous vous recommandons de hello [utiliser Notification Hubs toopush notifications toousers] didacticiel en tant qu’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="61013-231">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="61013-232">Il va vous montrer comment les notifications toosend à partir d’un serveur principal ASP.NET à l’aide de balises tootarget des utilisateurs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="61013-232">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="61013-233">Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, consultez hello [toosend utiliser Notification Hubs actualités] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="61013-233">If you want toosegment your users by interest groups, check out hello [Use Notification Hubs toosend breaking news] tutorial.</span></span>

<span data-ttu-id="61013-234">toolearn plus d’informations sur les concentrateurs de Notification, consultez notre [des conseils de concentrateurs de Notification].</span><span class="sxs-lookup"><span data-stu-id="61013-234">toolearn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[des conseils de concentrateurs de Notification]: notification-hubs-push-notification-overview.md
[utiliser Notification Hubs toopush notifications toousers]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[toosend utiliser Notification Hubs actualités]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Azure Portal]: https://portal.azure.com
