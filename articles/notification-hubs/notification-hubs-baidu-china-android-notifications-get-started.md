---
title: "Prendre en main Azure Notification Hubs à l’aide de Baidu | Microsoft Docs"
description: "Dans ce didacticiel, vous découvrirez comment utiliser Azure Notification Hubs pour envoyer des notifications Push à un appareil Android à l’aide de Baidu."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: df3bbda15e1245b6068c2b8290d0c96856051f1f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a>Prendre en main Notification Hubs à l’aide de Baidu
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
Le service de transmission Push dans le cloud de Baidu est un service cloud chinois que vous pouvez utiliser pour envoyer des notifications Push à des appareils mobiles. Ce service est utile en Chine, où la remise de notifications Push à Android est complexe en raison de la présence de différents magasins d’applications et de services de transmission de type push, outre la disponibilité d’appareils Android qui ne sont généralement pas connectés à Google Cloud Messaging (GCM).

## <a name="prerequisites"></a>Composants requis
Ce didacticiel requiert les éléments suivants :

* Kit de développement logiciel Android SDK (nous supposons que vous utilisez Eclipse), que vous pouvez télécharger à partir du <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site Android</a>
* [Kit de développement logiciel (SDK) Mobile Services pour Android]
* [Kit de développement logiciel (SDK) Android pour transmissions push Baidu]

> [!NOTE]
> Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).
> 
> 

## <a name="create-a-baidu-account"></a>Création d’un compte Baidu
Pour utiliser Baidu, vous devez disposer d’un compte Baidu. Si vous en avez déjà un, connectez-vous au [portail Baidu] et passez à l’étape suivante. Dans le cas contraire, consultez les instructions ci-après pour créer un compte Baidu.  

1. Accédez au [portail Baidu] et cliquez sur le lien **登录** (**Connexion**). Cliquez sur **立即注册** pour démarrer le processus d’inscription d’un compte.
   
   ![][1]
2. Entrez les informations requises (téléphone/adresse de messagerie, mot de passe et code de vérification), puis cliquez sur **Inscription**.
   
   ![][2]
3. Vous allez recevoir un courrier électronique à l’adresse e-mail que vous avez entrée avec un lien permettant d’activer votre compte Baidu.
   
   ![][3]
4. Connectez-vous à votre compte de messagerie, ouvrez le courrier électronique d’activation Baidu, puis cliquez sur le lien d’activation pour activer votre compte Baidu.
   
   ![][4]

Une fois que vous possédez un compte Baidu activé, connectez-vous au [portail Baidu].

## <a name="register-as-a-baidu-developer"></a>Inscription en tant que développeur Baidu
1. Une fois que êtes connecté au [portail Baidu], cliquez sur **更多>>** (**plus**).
   
      ![][5]
2. Faites défiler la section **站长与开发者服务 (Administrateur Web et Services de développement)** et cliquez sur **百度开放云平台** (**Plateforme cloud ouverte Baidu**).
   
      ![][6]
3. Sur la page suivante, cliquez sur **开发者服务** (**Services de développement**) dans le coin supérieur droit.
   
      ![][7]
4. Sur la page suivante, cliquez sur **注册开发者** (**Développeurs inscrits**) dans le menu dans le coin supérieur droit.
   
      ![][8]
5. Entrez votre nom, une description et un numéro de téléphone portable pour la réception d’un message texte de vérification, puis cliquez sur **送验证码** (**Envoyer un code de vérification**). Pour les numéros de téléphone internationaux, vous devez placer l’indicatif téléphonique du pays entre parenthèses. Voici un exemple de numéro en France : **(33)123456789**.
   
      ![][9]
6. Vous recevrez ensuite un message texte comportant un numéro de vérification, comme illustré dans l’exemple suivant :
   
      ![][10]
7. Entrez le numéro de vérification à partir du message dans **验证码** (**Code de confirmation**).
8. Enfin, terminez l’inscription du développeur en acceptant le contrat Baidu et en cliquant sur **提交** (**Envoyer**). Une fois l’inscription effectuée, la page ci-après s’affiche :
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a>Créer un projet Baidu de transmission Push dans le cloud
Quand vous créez un projet Baidu de transmission Push dans le cloud, vous recevez un ID d’application, une clé API et une clé secrète.

1. Une fois que êtes connecté au [portail Baidu], cliquez sur **更多>>** (**plus**).
   
      ![][5]
2. Faites défiler la section **站长与开发者服** (**Administrateur Web et Services de développement**) et cliquez sur **百度开放云平台** (**Plateforme cloud ouverte Baidu**).
   
      ![][6]
3. Sur la page suivante, cliquez sur **开发者服务** (**Services de développement**) dans le coin supérieur droit.
   
      ![][7]
4. Sur la page suivante, cliquez sur **云推送** (**Cloud Push**) à partir de la section **云服务** (**Services cloud**).
   
      ![][12]
5. Une fois que vous êtes un développeur enregistré, vous voyez **管理控制台** (**Console de gestion**) dans le menu supérieur. Cliquez sur **开发者服务管理** (**Gestion des services des développeurs**).
   
      ![][13]
6. Sur la page suivante, cliquez sur **创建工程** (**Créer un projet**).
   
      ![][14]
7. Entrez un nom d’application et cliquez sur **创建** (**Créer**).
   
      ![][15]
8. Une fois qu’un projet push cloud Baidu a été créé, vous voyez apparaître une page présentant **l’ID d’application**, la **clé API** et la **clé secrète**. Prenez note de la clé API et de la clé secrète que nous utiliserons ultérieurement.
   
      ![][16]
9. Configurez le projet pour les notifications push en cliquant sur **云推送** (**Cloud Push**) dans le volet gauche.
   
      ![][31]
10. Sur la page suivante, cliquez sur le bouton **推送设置** (**Paramètres Push**).
    
    ![][32]  
11. Sur la page de configuration, ajoutez le nom du package que vous utiliserez dans votre projet Android dans le champ **应用包名** (**Package d’application**), puis cliquez sur **保存设置** (**Enregistrer**).  
    
    ![][33]

Vous voyez apparaître le message **保存成功！** (**Enregistrement réussi !**).

## <a name="configure-your-notification-hub"></a>Configuration de votre hub de notification
1. Connectez-vous au [Portail Azure Classic], puis cliquez sur **+NOUVEAU** en bas de l’écran.
2. Cliquez sur **Services d’application**, sur **Service Bus**, sur **Hub de notification**, puis cliquez sur **Création rapide**.
3. Fournissez un nom dans le champ **Hub de notification**, renseignez les champs **Région** et **Espace de noms** pour indiquer où ce hub de notification sera créé, puis cliquez sur **Créer un hub de notification**.  
   
      ![][17]
4. Cliquez sur l’espace de noms dans lequel vous avez créé votre hub de notification, puis cliquez sur **Notification Hubs** dans la partie supérieure.
   
      ![][18]
5. Sélectionnez le hub de notification que vous avez créé, puis cliquez sur **Configurer** dans le menu supérieur.
   
      ![][19]
6. Faites défiler l’écran vers le bas jusqu’à la section **Paramètres de notification Baidu** et entrez la clé API et la clé secrète que vous avez obtenues précédemment à partir de la console Baidu pour votre projet Baidu de transmission push dans le cloud. Cliquez sur **Enregistrer**.
   
      ![][20]
7. Cliquez sur l’onglet **Tableau de bord** dans la partie supérieure du hub de notification, puis cliquez sur **Afficher la chaîne de connexion**.
   
      ![][21]
8. Prenez note des valeurs **DefaultListenSharedAccessSignature** et **DefaultFullSharedAccessSignature** dans la fenêtre **Accès aux informations de connexion**.
   
    ![][22]

## <a name="connect-your-app-to-the-notification-hub"></a>Connexion de votre application au hub de notification
1. Dans Eclipse ADT, créez un projet Android (**File** > **New** > **Android Application Project**).
   
    ![][23]
2. Entrez un **nom d’application** et vérifiez que la version de **Kit de développement logiciel (SDK) minimum obligatoire** est définie sur **API 16 : Android 4.1**.
   
    ![][24]
3. Cliquez sur **Next** et continuez à suivre l’Assistant jusqu’à ce que la fenêtre **Create Activity** s’affiche. Assurez-vous que l’option **Blank Activity** est sélectionnée, puis cliquez sur **Finish** pour créer une application Android.
   
    ![][25]
4. Assurez-vous que la **cible de génération du projet** est définie correctement.
   
    ![][26]
5. Téléchargez le fichier notification-hubs-0.4.jar à partir de l’onglet **Fichiers** du [Notification-Hubs-Android-SDK sur Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4). Ajoutez le fichier au dossier **libs** de votre projet Eclipse, puis actualisez le dossier *libs* .
6. Téléchargez et décompressez le [Kit de développement logiciel (SDK) Android pour transmissions push Baidu], ouvrez le dossier **libs**, puis copiez le fichier jar **pushservice-x.y.z** et les dossiers **armeabi** & **mips** dans le dossier **libs** de votre application Android.
7. Ouvrez le fichier **AndroidManifest.xml** de votre projet Android et ajoutez les autorisations requises par le Kit de développement logiciel (SDK) Baidu.
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. Ajoutez la propriété **android:name** à votre élément **application** dans le fichier **AndroidManifest.xml** en remplaçant *yourprojectname* par votre nom de projet (par exemple, **com.example.BaiduTest**). Assurez-vous que ce nom de projet correspond à celui que vous avez configuré dans la console Baidu.
   
        <application android:name="yourprojectname.DemoApplication"
9. Ajoutez la configuration ci-après dans l’élément application après l’élément d’activité **.MainActivity** en remplaçant *yourprojectname* par votre nom de projet (par exemple, **com.example.BaiduTest**) :
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. Ajoutez une nouvelle classe appelée **ConfigurationSettings.java** au projet.
    
     ![][28]
    
     ![][29]
11. Ajoutez-lui le code suivant :
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    Définissez **API_KEY** sur la valeur que vous avez récupérée précédemment du projet cloud Baidu, **NotificationHubName** sur le nom de votre hub de notification issu du portail Azure Classic et **NotificationHubConnectionString** sur la valeur DefaultListenSharedAccessSignature issue du portail Azure Classic.
12. Ajoutez une nouvelle classe appelée **DemoApplication.java**et ajoutez-lui le code suivant :
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. Ajoutez une autre nouvelle classe appelée **MyPushMessageReceiver.java**et ajoutez-lui le code suivant. Il s’agit de la classe qui gère les notifications Push reçues à partir du serveur push Baidu.
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG to Log */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. Ouvrez **MainActivity.java** et ajoutez le code suivant à la méthode **onCreate** :
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. Ouvrez les instructions d’importation suivantes en haut :
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-to-your-app"></a>Envoi de notifications à votre application
Vous pouvez tester rapidement la réception de notifications dans votre application en envoyant des notifications dans le [Portail Azure](https://portal.azure.com/) à l’aide du bouton **Envoyer** sur le hub de notification, comme illustré ci-dessous :

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

Les notifications Push sont normalement envoyées dans un service principal tel que Mobile Services ou ASP.NET à l’aide d’une bibliothèque compatible. Si une bibliothèque n’est pas disponible pour votre serveur principal, vous pouvez utiliser l’API REST directement pour envoyer des messages de notification.

Dans ce didacticiel, nous nous contentons pour plus de simplicité de tester votre application cliente en envoyant des notifications à l’aide du Kit de développement logiciel (SDK) .NET pour Notification Hubs dans une application console au lieu d’un service principal. Nous vous recommandons de consulter le didacticiel [Utiliser Notification Hubs pour envoyer des notifications Push aux utilisateurs](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) comme prochaine étape pour envoyer des notifications à partir d’un serveur principal ASP.NET. Toutefois, les approches suivantes peuvent servir à envoyer des notifications :

* **Interface REST** : vous pouvez prendre en charge les notifications sur n’importe quel serveur principal à l’aide de [l’interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **SDK .NET Microsoft Azure Notification Hubs**: dans le Gestionnaire de package Nuget pour Visual Studio, exécutez [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [Utilisation de Notification Hubs à partir de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).
* **Applications mobiles Azure**: pour découvrir un exemple de la procédure d’envoi de notifications à partir d’une application mobile Azure intégrée à Notification Hubs, consultez l’article [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) (Ajouter des notifications Push pour Mobile Apps).
* **Java/PHP** : pour voir un exemple d’envoi de notifications au moyen des API REST, consultez « Utilisation de Notification Hubs depuis Java/PHP » ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-net-console-app"></a>(Facultatif) Envoi de notifications à partir d’une application de console .NET.
Dans cette section, nous montrons comment envoyer une notification à l’aide d’une application console .NET.

1. Créez une application console Visual C# :
   
    ![][30]
2. Dans la fenêtre Console du gestionnaire de package, choisissez **Projet par défaut** comme nouveau projet d’application console, puis exécutez la commande suivante dans la fenêtre de console :
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Cette instruction ajoute une référence au Kit de développement logiciel (SDK) Azure Notification Hubs à l’aide du <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet Microsoft.Azure.Notification Hubs</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. Ouvrez le fichier **Program.cs** et ajoutez l’instruction using suivante :
   
        using Microsoft.Azure.NotificationHubs;
4. Dans votre classe `Program`, ajoutez la méthode ci-après et remplacez *DefaultFullSharedAccessSignatureSASConnectionString* et *NotificationHubName* par les valeurs dont vous disposez.
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. Ajoutez les lignes suivantes dans votre méthode **Main** :
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a>Test de l'application
Pour tester cette application avec un téléphone réel, connectez simplement le téléphone à votre ordinateur à l’aide d’un câble USB. Cette action charge votre application sur le téléphone attaché.

Pour tester cette application avec l’émulateur, dans la barre d’outils supérieure d’Eclipse, cliquez sur **Run**, puis sélectionnez votre application : elle démarre l’émulateur, puis charge et exécute l’application.

L’application récupère les paramètres userId et channelId à partir du service de notification push Baidu et s’inscrit auprès du hub de notification.

Pour envoyer une notification de test, vous pouvez utiliser l’onglet de débogage du Portail Azure Classic. Si vous avez intégré l’application de console .NET, appuyez sur la touche F5 dans Visual Studio pour exécuter l’application. L’application envoie une notification qui s’affiche dans la zone de notification supérieure de votre appareil ou de l’émulateur.

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[Kit de développement logiciel (SDK) Mobile Services pour Android]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Kit de développement logiciel (SDK) Android pour transmissions push Baidu]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[Portail Azure Classic]: https://manage.windowsazure.com/
[portail Baidu]: http://www.baidu.com/
