---
title: "aaaGet main d’Azure Notification Hubs pour les applications Kindle | Documents Microsoft"
description: "Dans ce didacticiel, vous découvrez comment toouse Azure Notification Hubs toosend push application de notifications de Kindle tooa."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a>Prendre en main Notification Hubs pour les applications Kindle
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push application de notifications de Kindle tooa.
Dans ce didacticiel, vous allez créer une application Kindle vierge recevant des notifications Push à l’aide d’Amazon Device Messaging (ADM).

## <a name="prerequisites"></a>Composants requis
Ce didacticiel requiert hello qui suit :

* Obtenir hello Android SDK (nous supposons que vous allez utiliser Eclipse) à partir de hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site Android</a>.
* Suivez les étapes de hello dans <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">paramètre votre environnement de développement</a> tooset de votre environnement de développement pour Kindle.

## <a name="add-a-new-app-toohello-developer-portal"></a>Ajouter un nouveau portail des développeurs toohello application
1. Tout d’abord, créez une application dans hello [portail des développeurs Amazon].
   
    ![][0]
2. Hello de copie **clé d’Application**.
   
    ![][1]
3. Dans le portail hello, cliquez sur le nom hello de votre application, puis cliquez sur hello **Device Messaging** onglet.
   
    ![][2]
4. Cliquez sur **Create a New Security Profile** (Créer un profil de sécurité), puis créez un profil de sécurité (par exemple, le **profil de sécurité TestAdm**). Cliquez ensuite sur **Enregistrer**.
   
    ![][3]
5. Cliquez sur **profils de sécurité** tooview hello sécurité profil que vous venez de créer. Hello de copie **ID Client** et **clé secrète Client** valeurs pour une utilisation ultérieure.
   
    ![][4]

## <a name="create-an-api-key"></a>Création d'une clé API
1. Ouvrez une invite de commandes avec les privilèges Administrateur.
2. Parcourir le dossier du Kit de développement logiciel Android toohello.
3. Entrez hello de commande suivante :
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. Pourquoi **keystore** mot de passe, tapez **android**.
5. Hello de copie **MD5** empreintes digitales.
6. Dans le portail des développeurs hello, sur hello **messagerie** , cliquez sur **Android/Kindle** et entrez le nom hello du package de hello pour votre application (par exemple, **com.sample.notificationhubtest**) et hello **MD5** valeur, puis cliquez sur **générer une clé API**.

## <a name="add-credentials-toohello-hub"></a>Ajouter le concentrateur toohello d’informations d’identification
Dans le portail hello, ajouter hello client secret et le client ID toohello **configurer** onglet de votre concentrateur de notification.

## <a name="set-up-your-application"></a>Configuration de votre application
> [!NOTE]
> Lors de la création d’une application, utilisez au moins l’API de niveau 17.
> 
> 

Ajouter le projet Eclipse tooyour hello ADM bibliothèques :

1. bibliothèque de tooobtain hello ADM, [télécharger hello SDK]. Extrayez le fichier zip du SDK hello.
2. Dans Eclipse, cliquez avec le bouton droit sur votre projet, puis cliquez sur **Propriétés**. Sélectionnez **chemin d’accès de Build Java** sur hello gauche, puis sélectionnez hello ** bibliothèques ** onglet en haut de hello. Cliquez sur **ajouter le Jar externe**et sélectionnez hello fichier `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` à partir du répertoire hello dans lequel vous avez extrait hello Amazon SDK.
3. Téléchargez hello NotificationHubs Android SDK (lien).
4. Décompressez le package de hello, puis faites glisser le fichier de hello `notification-hubs-sdk.jar` dans hello `libs` dossier dans Eclipse.

Modifiez votre toosupport de manifeste d’application ADM :

1. Ajoutez hello Amazon espace de noms dans l’élément de manifeste hello racine :

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. Ajouter des autorisations en tant que premier élément de hello sous l’élément manifeste hello. Substitution **[votre nom de PACKAGE]** avec package hello que vous avez utilisé toocreate votre application.
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. Insérez hello suit l’élément en tant que premier enfant de hello hello d’élément d’application. N’oubliez pas de toosubstitute **[votre nom de SERVICE]** avec nom hello de votre gestionnaire de messages ADM qui vous créez dans la section suivante de hello (package de hello, y compris), puis remplacez **[votre nom de PACKAGE]** avec hello nom du package avec lequel vous avez créé votre application.
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a>Création de votre gestionnaire de messages ADM
1. Créez une classe qui hérite de `com.amazon.device.messaging.ADMMessageHandlerBase` et nommez-le `MyADMMessageHandler`, comme illustré dans la figure suivante de hello :
   
    ![][6]
2. Ajoutez hello suit `import` instructions :
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. Ajoutez hello suivant le code de classe hello que vous avez créé. N’oubliez pas de toosubstitute hello hub nom et une connexion chaîne (écoute) :
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. Ajouter hello suivant code toohello `OnMessage()` méthode :
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. Ajouter hello suivant code toohello `OnRegistered` méthode :
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. Ajouter hello suivant code toohello `OnUnregistered` méthode :
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. Bonjour `MainActivity` (méthode), ajouter hello après l’instruction d’importation :
   
        import com.amazon.device.messaging.ADM;
8. Ajouter hello suivant du code à la fin de hello de hello `OnCreate` méthode :
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-tooyour-app"></a>Ajouter votre application de tooyour clé API
1. Dans Eclipse, créez un nouveau fichier nommé **api_key.txt** dans les ressources de répertoire hello de votre projet.
2. Ouvrez hello fichier et copiez hello clé d’API que vous avez généré dans le portail des développeurs Amazon hello.

## <a name="run-hello-app"></a>Exécutez l’application hello
1. Démarrer l’émulateur de hello.
2. Dans l’émulateur de hello, faites glisser à partir du haut de hello et cliquez sur **paramètres**, puis cliquez sur **mon compte** et l’inscrire avec un compte Amazon valide.
3. Dans Eclipse, exécutez l’application hello.

> [!NOTE]
> Si un problème se produit, vérifie hello d’émulateur de hello (ou périphérique). valeur d’heure Hello doit être exact. temps de hello toochange de l’émulateur de Kindle hello, vous pouvez exécuter hello commande à partir de votre répertoire d’outils de plateforme du SDK Android suivante :
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a>Envoyer un message
toosend un message à l’aide de .NET :

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[portail des développeurs Amazon]: https://developer.amazon.com/home.html
[télécharger hello SDK]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
