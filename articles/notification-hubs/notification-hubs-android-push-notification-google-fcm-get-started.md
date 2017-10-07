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
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a>Envoi de tooAndroid de notifications push avec Azure Notification Hubs
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
> [!IMPORTANT]
> Cette rubrique explique les notifications Push avec Google Firebase Cloud Messaging (FCM). Si vous utilisez encore Google Cloud Messaging (GCM), consultez [envoi tooAndroid de notifications push avec Azure Notification Hubs et GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).
> 
> 

Ce didacticiel vous montre comment toouse Azure Notification Hubs et toosend de messagerie de Cloud Firebase push application Android tooan de notifications.
Vous allez créer une application Android vide qui reçoit des notifications Push à l’aide de Firebase Cloud Messaging (FCM).

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

code Hello terminée pour ce didacticiel peut être téléchargé à partir de GitHub [ici](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).

## <a name="prerequisites"></a>Composants requis
> [!IMPORTANT]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).
> 
> 

* En outre tooan de compte Azure active mentionnés ci-dessus, ce didacticiel requiert la version la plus récente de hello [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).
* Android 2.3 ou ultérieure pour Firebase Cloud Messaging.
* La révision 27 ou ultérieure du référentiel Google est requise pour Firebase Cloud Messaging.
* Services Google Play 9.0.2 ou version ultérieure pour Firebase Cloud Messaging.
* Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels Notification Hubs pour les applications Android.

## <a name="create-a-new-android-studio-project"></a>Créer un nouveau projet Android Studio
1. Dans Android Studio, démarrez un nouveau projet Android Studio.
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. Choisissez hello **téléphone et tablette** forment le facteur et hello **Minimum SDK** que vous souhaitez toosupport. Cliquez ensuite sur **Suivant**.
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. Choisissez **activité vide** pour l’activité principale de hello, cliquez sur **suivant**, puis cliquez sur **Terminer**.

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>Créer un projet qui prend en charge Firebase Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a>Configurer un nouveau hub de notification
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6. Bonjour **paramètres** Panneau de votre concentrateur de notification, sélectionnez **Notification Services** , puis **Google (GCM)**. Touche hello FCM server vous avez copiée précédemment à partir de hello [console de Firebase](https://firebase.google.com/console/) et cliquez sur **enregistrer**.

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

Votre concentrateur de notification est maintenant configuré toowork avec Firebase Cloud Messagin, et vous disposez tooboth de chaînes de connexion hello inscrire tooreceive de votre application et d’envoyer des notifications push.

## <a id="connecting-app"></a>Se connecter à votre hub de notification d’application toohello
### <a name="add-google-play-services-toohello-project"></a>Ajouter un projet de toohello services Google Play
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a>Ajout de bibliothèques de concentrateurs de notification Azure
1. Bonjour `Build.Gradle` fichier hello **application**, ajouter hello lignes Bonjour suivantes **dépendances** section.
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. Ajouter hello suivant référentiel après hello **dépendances** section.
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a>Mise à jour hello AndroidManifest.xml.
1. toosupport FCM, nous devons implémenter un service d’écoute ID d’Instance dans notre code utilisé trop[obtenir des jetons d’inscription](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) à l’aide de [FirebaseInstanceId API de Google](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId). Dans ce didacticiel, nous allons appeler classe hello `MyInstanceIDService`. 
   
    Ajouter hello service définition toohello AndroidManifest.xml le fichier suivant, à l’intérieur de hello `<application>` balise. 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. Une fois que nous avons reçu notre jeton d’inscription FCM de hello FirebaseInstanceId API, nous l’utiliserons trop[enregistrer avec hello Hub de Notification Azure](notification-hubs-push-notification-registration-management.md). Nous prendrons en charge cette inscription à l’aide d’arrière-plan hello un `IntentService` nommé `RegistrationIntentService`. Ce service gère également l’actualisation de notre jeton d’inscription FCM.
   
    Ajouter hello service définition toohello AndroidManifest.xml le fichier suivant, à l’intérieur de hello `<application>` balise. 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. Nous allons également définir une notification de tooreceive récepteur. Ajouter hello récepteur définition toohello AndroidManifest.xml le fichier suivant, à l’intérieur de hello `<application>` balise. Remplacez hello `<your package>` espace réservé avec hello votre nom de package réel indiqué en haut de hello Hello `AndroidManifest.xml` fichier.
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. Ajouter hello suivant nécessaire FCM liées autorisations ci-dessous hello `</application>` balise. Assurez-vous que tooreplace `<your package>` avec le nom du package hello indiqué en haut de hello Hello `AndroidManifest.xml` fichier.
   
    Pour plus d’informations sur ces autorisations, consultez [le programme d’installation d’une application cliente de GCM pour Android](https://developers.google.com/cloud-messaging/android/client#manifest) et [migrer une application cliente de GCM pour Android tooFirebase messagerie Cloud](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a>Ajout de code
1. Bonjour vue du projet, développez **application** > **src** > **principal** > **java**. Cliquez avec le bouton droit sur le dossier de votre package sous **java**, cliquez sur **Nouveau**, puis sur **Classe Java**. Ajoutez une nouvelle classe nommée `NotificationSettings`. 
   
    ![Android Studio - nouvelle classe Java](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    Assurez-vous que tooupdate hello ces trois espaces réservés dans hello suivant code hello `NotificationSettings` classe :
   
   * **ID d’expéditeur**: hello Id de l’expéditeur que vous avez obtenu précédemment dans hello **messagerie Cloud** onglet des paramètres de votre projet dans hello [console de Firebase](https://firebase.google.com/console/).
   * **HubListenConnectionString**: hello **DefaultListenAccessSignature** chaîne de connexion pour votre concentrateur. Vous pouvez copier cette chaîne de connexion en cliquant sur **des stratégies d’accès** sur hello **paramètres** Panneau de votre concentrateur sur hello [Azure Portal].
   * **HubName**: utiliser le nom de votre concentrateur de notification qui s’affiche dans le panneau de concentrateur hello Bonjour hello [Azure Portal].
     
     `NotificationSettings` code :
     
       public class NotificationSettings {
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       }
2. À l’aide des étapes hello ci-dessus, ajoutez une autre classe nommée `MyInstanceIDService`. Il s'agira de notre implémentation de service d'écouteur d'ID d'instance.
   
    code Hello pour cette classe appellera notre `IntentService` trop[jeton d’actualisation hello FCM](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) en arrière-plan de hello.
   
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


1. Ajouter une autre classe tooyour projet nommé, `RegistrationIntentService`. Il s’agit d’implémentation hello pour notre `IntentService` qui gérera [actualisation jeton FCM de hello](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) et [l’inscription auprès de hub de notification hello](notification-hubs-push-notification-registration-management.md).
   
    Utilisez hello suivant de code de cette classe.
   
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
2. Dans votre `MainActivity` de classe, ajoutez hello `import` instructions ci-dessus hello déclaration de classe.
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. Ajoutez hello suivant des membres privés haut hello de classe hello. Nous allons utiliser ces [vérifier la disponibilité de hello de Services Google Play comme recommandé par Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. Dans votre `MainActivity` de classe, ajoutez hello après disponibilité toohello de méthode de Services Google Play. 
   
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
5. Dans votre `MainActivity` de classe, ajoutez hello suivant code recherchera les Services Google Play avant d’appeler votre `IntentService` tooget votre jeton d’inscription FCM et l’inscrire auprès de votre concentrateur de notification.
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. Bonjour `OnCreate` méthode Hello `MainActivity` de classe, ajoutez hello suivant le processus d’inscription de code toostart hello lorsque l’activité est créée.
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. Ajouter ces méthodes supplémentaires de toohello `MainActivity` tooverify état et les rapports état des applications dans votre application.
   
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
8. Hello `ToastNotify` méthode utilise hello *« Hello World »* `TextView` contrôler tooreport état et les notifications de manière permanente dans l’application hello. Dans la mise en page activity_main.xml, ajoutez hello id pour ce contrôle suivant.
   
       android:id="@+id/text_hello"
9. Ensuite, nous allons ajouter une sous-classe pour notre récepteur que nous avons défini Bonjour AndroidManifest.xml. Ajouter une autre classe tooyour projet nommé `MyHandler`.
10. Ajouter hello suivant les instructions d’importation haut hello `MyHandler.java`:
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. Ajouter hello suivant code hello `MyHandler` classe rendant une sous-classe de `com.microsoft.windowsazure.notifications.NotificationsHandler`.
    
    Ce code substitue hello `OnReceive` méthode gestionnaire de hello signalera notifications qui ont été reçues. Gestionnaire de Hello envoie également un gestionnaire de notification Android hello push notifications toohello à l’aide de hello `sendNotification()` (méthode). Hello `sendNotification()` méthode doit être exécutée lors de l’application hello n’est pas en cours d’exécution et une notification est reçue.
    
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
12. Dans Android Studio sur la barre de menus hello, cliquez sur **générer** > **régénérer le projet** toomake sûr qu’aucune erreur n’est présent dans votre code.
13. Exécutez l’application hello sur votre appareil et vérifier qu’il s’enregistre correctement avec le hub de notification hello. 
    
    > [!NOTE]
    > L’inscription peut échouer au démarrage initial de hello jusqu'à hello `onTokenRefresh()` méthode de service de l’Id d’instance est appelée. actualisation de Hello doit initier une inscription réussie avec le hub de notification hello.
    > 
    > 

## <a name="sending-push-notifications"></a>Envoi de notifications Push
Vous pouvez tester de recevoir des notifications push dans votre application en les envoyant via hello [Azure Portal] -recherchez hello **dépannage** Section dans le panneau de concentrateur hello, comme indiqué ci-dessous.

![Azure Notification Hubs - Test d’envoi](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a>(Facultatif) Envoyer des notifications push directement à partir de l’application hello
> [!IMPORTANT]
> Cet exemple montre comment envoyer des notifications à partir de l’application cliente de hello est fourni uniquement à des fins pédagogiques. Étant donné que vous devrez hello `DefaultFullSharedAccessSignature` toobe présent sur l’application cliente de hello, il expose les risques de toohello de concentrateur de notification qu’un utilisateur peut obtenir les notifications d’accès non autorisé de toosend tooyour clients.
> 
> 

En règle générale, vous devez envoyer des notifications à l'aide d'un serveur principal. Dans certains cas, vous pouvez choisir des notifications push de toosend en mesure de toobe directement à partir de l’application cliente de hello. Cette section explique comment les notifications toosend client hello à l’aide de hello [API REST de Azure Notification Hub](https://msdn.microsoft.com/library/azure/dn223264.aspx).

1. Dans la vue de projet Android Studio, développez **App** > **src** > **main** > **res** > **layout**. Ouvrez hello `activity_main.xml` mise en page, cliquez sur hello **texte** onglet tooupdate hello contenus de texte hello fichier. Mettre à jour avec le code hello ci-dessous, qui ajoute de nouvelles `Button` et `EditText` contrôles pour l’envoi de poussée du hub de notification toohello notification messages. Ajoutez ce code au bas de hello, juste avant `</RelativeLayout>`.
   
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
2. Dans la vue de projet Android Studio, développez **App** > **src** > **main** > **res** > **values**. Ouvrez hello `strings.xml` et ajoutez les valeurs de chaîne hello qui sont référencés par hello nouvelle `Button` et `EditText` contrôles. Ajoutez ces bas hello du fichier de hello, juste avant `</resources>`.
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. Dans votre `NotificationSetting.java` , ajoutez hello suivant paramètre toohello `NotificationSettings` classe.
   
    Mise à jour `HubFullAccess` avec hello **DefaultFullSharedAccessSignature** chaîne de connexion pour votre concentrateur. Cette chaîne de connexion peut être copiée à partir de hello [Azure Portal] en cliquant sur **des stratégies d’accès** sur hello **paramètres** panneau pour votre concentrateur de notification.
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. Dans votre `MainActivity.java` , ajoutez les éléments suivants de hello `import` instructions ci-dessus hello `MainActivity` classe.
   
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
5. Dans votre `MainActivity.java` , ajoutez hello suivant membres haut hello hello `MainActivity` classe.    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. Un concentrateur de notification POST demande toosend messages tooyour, vous devez créer un tooauthenticate de jeton de Signature d’accès (SaS) du logiciel. Pour cela, l’analyse des données de clé hello à partir de la chaîne de connexion hello et puis en créant hello jeton SAP, comme indiqué dans hello [Concepts communs](http://msdn.microsoft.com/library/azure/dn495627.aspx) référence d’API REST. Hello suivant de code est un exemple d’implémentation.
   
    Dans `MainActivity.java`, ajouter hello suivant de méthode toohello `MainActivity` classe tooparse votre chaîne de connexion.
   
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
7. Dans `MainActivity.java`, ajouter hello suivant de méthode toohello `MainActivity` classe toocreate un jeton d’authentification SAP.
   
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
8. Dans `MainActivity.java`, ajouter hello suivant de méthode toohello `MainActivity` hello toohandle de classe **envoyer une Notification** clic de bouton et envoyer une notification de push de hello concentrateur toohello de messages à l’aide de hello intégrés API REST.
   
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

## <a name="testing-your-app"></a>Test de votre application
#### <a name="push-notifications-in-hello-emulator"></a>Notifications push dans l’émulateur de hello
Si vous souhaitez que les notifications push tootest à l’intérieur d’un émulateur, assurez-vous que votre image de l’émulateur prend en charge le niveau d’API Google hello que vous avez choisie pour votre application. Si votre image ne prend pas en charge native APIs Google, vous obtiendrez des hello **SERVICE\_pas\_disponible** exception.

En outre toohello ci-dessus, assurez-vous que vous avez ajouté votre tooyour de compte Google en cours d’exécution émulateur sous **paramètres** > **comptes**. Dans le cas contraire, votre tooregister tentatives avec GCM peut entraîner hello **authentification\_n’a pas pu** exception.

#### <a name="running-hello-application"></a>Exécution de l’application hello
1. Exécutez l’application hello et notez que l’ID d’inscription hello est signalé pour une inscription réussie.
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. Entrez un toobe de message de notification envoyé tooall les appareils Android qui ont été inscrits auprès de concentrateur de hello.
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. Appuyez sur **Envoyer une notification**. Affichent tous les périphériques qui ont en cours d’exécution application hello un `AlertDialog` instance avec un message de notification push hello. Les appareils qui n’ont pas en cours d’exécution application hello mais précédemment inscrits pour les notifications push recevra une notification Bonjour Gestionnaire de notifications Android. Celles peuvent être affichées par le glissement vers le bas à partir de l’angle supérieur gauche de hello.
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a>Étapes suivantes
Nous vous recommandons de hello [utiliser Notification Hubs toopush notifications toousers] didacticiel en tant qu’étape suivante de hello. Il va vous montrer comment les notifications toosend à partir d’un serveur principal ASP.NET à l’aide de balises tootarget des utilisateurs spécifiques.

Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, consultez hello [toosend utiliser Notification Hubs actualités] didacticiel.

toolearn plus d’informations sur les concentrateurs de Notification, consultez notre [des conseils de concentrateurs de Notification].

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
