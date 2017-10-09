---
title: "aaaGet main à l’aide de Baidu Azure Notification Hubs | Documents Microsoft"
description: "Dans ce didacticiel, vous apprendrez comment appareils tooAndroid toouse Azure Notification Hubs toopush des notifications à l’aide de Baidu."
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
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a>Prendre en main Notification Hubs à l’aide de Baidu
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
Push de cloud Baidu est un service de cloud chinois que vous pouvez utiliser des périphériques de toomobile toosend push notifications. Ce service est utile en Chine, où remettre des notifications push tooAndroid est complexe en raison de la présence de hello de magasins d’applications différents et par émission de données des services, en outre disponibilité toohello des appareils Android qui ne sont pas généralement connecté tooGCM (Google Le cloud de messagerie).

## <a name="prerequisites"></a>Composants requis
Ce didacticiel requiert les éléments suivants :

* SDK Android (nous supposons que vous utilisez Eclipse), que vous pouvez télécharger à partir de hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site Android</a>
* [Kit de développement logiciel (SDK) Mobile Services pour Android]
* [Push Baidu Android SDK]

> [!NOTE]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).
> 
> 

## <a name="create-a-baidu-account"></a>Création d’un compte Baidu
toouse Baidu, vous devez disposer d’un compte Baidu. Si vous avez déjà un, ouvrez une session dans toohello [Baidu portail] et ignorer l’étape suivante de toohello. Dans le cas contraire, consultez hello suivant les instructions sur la façon de toocreate un compte Baidu.  

1. Accédez toohello [Baidu portail] et cliquez sur hello**登录**(**connexion**) lien. Cliquez sur**立即注册**toostart processus d’inscription hello.
   
   ![][1]
2. Entrez les détails de hello requis : code adresse, un mot de passe et la vérification de téléphone/messagerie, puis cliquez sur **inscription**.
   
   ![][2]
3. Vous recevrez une adresse de messagerie toohello par courrier électronique que vous avez entré avec un tooactivate lien votre compte Baidu.
   
   ![][3]
4. Connectez-vous au compte de messagerie tooyour, ouvrir la messagerie de l’activation de Baidu hello, cliquez sur tooactivate de lien d’activation hello votre compte Baidu.
   
   ![][4]

Une fois que vous avez un compte Baidu activé, connectez-vous à toohello [Baidu portail].

## <a name="register-as-a-baidu-developer"></a>Inscription en tant que développeur Baidu
1. Une fois que vous avez ouvert une session dans toohello [Baidu portail], cliquez sur**更多 >>** (**plus**).
   
      ![][5]
2. Faites défiler hello**站长与开发者服务 (administrateur Web et Services de développement)** et cliquez sur**百度开放云平台**(**Baidu ouvrir plateforme cloud**).
   
      ![][6]
3. Dans la page suivante de hello, cliquez sur**开发者服务**(**Services de développement**) dans l’angle supérieur droit de hello.
   
      ![][7]
4. Dans la page suivante de hello, cliquez sur**注册开发者**(**inscrit les développeurs**) à partir du menu hello dans l’angle supérieur droit de hello.
   
      ![][8]
5. Entrez votre nom, une description et un numéro de téléphone portable pour la réception d’un message texte de vérification, puis cliquez sur **送验证码** (**Envoyer un code de vérification**). Pour les numéros de téléphone international, vous devez tooenclose indicatif du pays hello entre parenthèses. Voici un exemple de numéro en France : **(33)123456789**.
   
      ![][9]
6. Vous recevrez ensuite un message texte avec un code de vérification, comme indiqué dans hello l’exemple suivant :
   
      ![][10]
7. Entrez le numéro de vérification hello à partir du message de type hello dans**验证码**(**code de Confirmation**).
8. Pour finir, terminez l’inscription de développeur hello en cliquant sur Accepter hello Baidu contrat**提交**(**Submit**). Vous verrez hello suivant page sur la réussite de l’inscription :
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a>Créer un projet Baidu de transmission Push dans le cloud
Quand vous créez un projet Baidu de transmission Push dans le cloud, vous recevez un ID d’application, une clé API et une clé secrète.

1. Une fois que vous avez ouvert une session dans toohello [Baidu portail], cliquez sur**更多 >>** (**plus**).
   
      ![][5]
2. Faites défiler hello**站长与开发者服务**(**administrateur Web et des Services de développement**) et cliquez sur**百度开放云平台**(**Baidu ouvrir plateforme cloud**).
   
      ![][6]
3. Dans la page suivante de hello, cliquez sur**开发者服务**(**Services de développement**) dans l’angle supérieur droit de hello.
   
      ![][7]
4. Dans la page suivante de hello, cliquez sur**云推送**(**Cloud Push**) à partir de hello**云服务**(**Services de cloud computing**) section.
   
      ![][12]
5. Une fois que vous êtes un développeur inscrit, vous voyez**管理控制台**(**Console de gestion**) au menu du haut hello. Cliquez sur **开发者服务管理** (**Gestion des services des développeurs**).
   
      ![][13]
6. Dans la page suivante de hello, cliquez sur**创建工程**(**créer un projet**).
   
      ![][14]
7. Entrez un nom d’application et cliquez sur **创建** (**Créer**).
   
      ![][15]
8. Une fois qu’un projet push cloud Baidu a été créé, vous voyez apparaître une page présentant **l’ID d’application**, la **clé API** et la **clé secrète**. Prenez note de la clé d’API hello et une clé secrète, que nous utiliserons plus tard.
   
      ![][16]
9. Configurez le projet hello pour les notifications push en cliquant sur**云推送**(**Cloud Push**) dans le volet gauche de hello.
   
      ![][31]
10. Sur la page suivante de hello, cliquez sur hello**推送设置**(**Push paramètres**) bouton.
    
    ![][32]  
11. Sur la page de configuration hello, ajouter le nom du package hello que vous utiliserez dans votre projet Android dans hello**应用包名**(**package d’Application**) champ, puis cliquez sur**保存设置**() **Enregistrer**).  
    
    ![][33]

Vous consultez hello**保存成功 !** (**Enregistrement réussi !**).

## <a name="configure-your-notification-hub"></a>Configuration de votre hub de notification
1. Connectez-vous à toohello [portail classique Azure], puis cliquez sur **+ nouveau** bas hello écran hello.
2. Cliquez sur **Services d’application**, sur **Service Bus**, sur **Hub de notification**, puis cliquez sur **Création rapide**.
3. Fournissez un nom pour votre **Hub de Notification**, sélectionnez hello **région** et hello **Namespace** où ce hub de notification est créé, puis cliquez sur  **Créer un Hub de Notification**.  
   
      ![][17]
4. Espace de noms hello dans lequel vous avez créé votre hub de notification, puis **concentrateurs de Notification** haut hello.
   
      ![][18]
5. Concentrateur de notification Sélectionnez hello créé, puis cliquez sur **configurer** à partir du menu du haut hello.
   
      ![][19]
6. Faites défiler vers le bas toohello **les paramètres de notification baidu** section et entrez la clé d’API de hello et une clé secrète que vous avez obtenue à partir de la console de Baidu hello précédemment pour votre projet Baidu cloud push. Cliquez sur **Enregistrer**.
   
      ![][20]
7. Cliquez sur hello **tableau de bord** onglet en haut de hello hello hub de notification, puis cliquez sur **afficher la chaîne de connexion**.
   
      ![][21]
8. Prenez note de hello **DefaultListenSharedAccessSignature** et **DefaultFullSharedAccessSignature** de hello **d’accéder aux informations de connexion** fenêtre.
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a>Se connecter à votre hub de notification d’application toohello
1. Dans Eclipse ADT, créez un projet Android (**File** > **New** > **Android Application Project**).
   
    ![][23]
2. Entrez un **nom de l’Application** et assurez-vous que hello **Minimum nécessaire le Kit de développement** version est définie trop**API 16 : Android 4.1**.
   
    ![][24]
3. Cliquez sur **suivant** et continuer après l’Assistant de hello jusqu'à hello **créer une activité** fenêtre s’affiche. Assurez-vous que **activité vide** est sélectionné et enfin sélectionnez **Terminer** toocreate une Application Android.
   
    ![][25]
4. Vérifiez que hello **cible de Build de projet** est défini correctement.
   
    ![][26]
5. Téléchargez hello concentrateurs-notification-0.4.jar fichier hello **fichiers** onglet Hello [Notification-Hubs-Android-SDK sur Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4). Ajouter hello fichier toohello **libs** dossier de votre projet Eclipse et actualisation hello *libs* dossier.
6. Téléchargez et décompressez hello [Push Baidu Android SDK], ouvrez hello **libs** dossier, puis hello de copie **pushservice-x.y.z** jar de fichiers et de hello **armeabi**  &  **mips** dossiers Bonjour **libs** dossier de votre application Android.
7. Ouvrez hello **AndroidManifest.xml** fichier de votre Android de projet et ajouter des autorisations hello requis par hello Baidu SDK.
   
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
8. Ajouter hello **android : name** propriété tooyour **application** élément **AndroidManifest.xml**, en remplaçant *votre_nom_de_projet* (pour exemple, **com.example.BaiduTest**). Assurez-vous que ce nom de projet correspond à hello une que vous avez configuré dans la console hello Baidu.
   
        <application android:name="yourprojectname.DemoApplication"
9. Ajouter hello configuration au sein de l’élément de l’application hello après hello suivante **. MainActivity** élément d’activité, en remplaçant *votre_nom_de_projet* (par exemple, **com.example.BaiduTest**) :
   
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
10. Ajouter une nouvelle classe nommée **ConfigurationSettings.java** toohello projet.
    
     ![][28]
    
     ![][29]
11. Ajoutez hello suivant tooit de code :
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    Valeur hello **API_KEY** avec ce que vous avez récupérés sous projet hello Baidu cloud précédemment, **NotificationHubName** avec votre nom de hub de notification à partir de hello portail classique Azure et  **NotificationHubConnectionString** avec DefaultListenSharedAccessSignature de hello portail classique Azure.
12. Ajouter une nouvelle classe nommée **DemoApplication.java**et ajoutez hello suivant tooit de code :
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. Ajoutez une autre classe nommée **MyPushMessageReceiver.java**et ajoutez hello suivant tooit de code. Il est la classe hello handles hello des notifications push reçus à partir du serveur de push Baidu hello.
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
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
14. Ouvrez **MainActivity.java**et ajoutez hello suivant toohello **onCreate** méthode :
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. Ouvrez hello suivant les instructions d’importation haut hello :
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a>Envoyer des notifications tooyour application
Vous pouvez tester rapidement la réception de notifications dans votre application en envoyant des notifications Bonjour [portail Azure](https://portal.azure.com/) à l’aide de hello **envoyer** bouton sur le concentrateur de notification hello, comme indiqué dans hello suivant d’écran :

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

Les notifications Push sont normalement envoyées dans un service principal tel que Mobile Services ou ASP.NET à l’aide d’une bibliothèque compatible. Si une bibliothèque n’est pas disponible pour votre serveur principal, vous pouvez utiliser les API REST de hello toosend directement les messages de notification.

Dans ce didacticiel, nous plus de simplicité et simplement montrent le test de votre application cliente en envoyant des notifications à l’aide de hello SDK .NET pour les concentrateurs de notification dans une application console à la place d’un service principal. Nous vous recommandons de hello [utiliser Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) didacticiel en tant qu’étape suivante de hello pour envoyer des notifications à partir d’un serveur principal d’ASP.NET. Toutefois, hello méthodes suivantes peut servir pour envoyer des notifications :

* **Interface REST**: peut prendre en charge notification sur toute plateforme principale à l’aide de hello [interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Kit de développement logiciel Microsoft Azure Notification Hubs .NET**: Bonjour Gestionnaire de Package Nuget pour Visual Studio, exécutez [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js**: [comment toouse concentrateurs de Notification à partir de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).
* **Applications mobiles**: pour obtenir un exemple de notifications toosend à partir d’un serveur principal Azure App Service Mobile Apps intégré avec Notification Hubs, consultez [ajouter push notifications tooyour application mobile](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: pour obtenir un exemple de comment toosend des notifications à l’aide de hello API REST, consultez « Comment toouse concentrateurs de Notification à partir de Java/PHP » ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-net-console-app"></a>(Facultatif) Envoi de notifications à partir d’une application de console .NET.
Dans cette section, nous montrons comment envoyer une notification à l’aide d’une application console .NET.

1. Créez une application console Visual C# :
   
    ![][30]
2. Dans la fenêtre de Console du Gestionnaire de Package de hello, définissez hello **projet par défaut** tooyour nouveau projet d’application console et puis, dans la fenêtre de console hello, exécutez hello de commande suivante :
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Cette instruction ajoute une référence de toohello Azure Notification Hubs SDK à l’aide de hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet de concentrateurs Microsoft.Azure.Notification</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. Les fichiers ouverts hello **Program.cs** et ajoutez hello qui suit à l’aide d’instruction :
   
        using Microsoft.Azure.NotificationHubs;
4. Dans votre `Program` de classe, ajoutez hello suivant de méthode et remplacer *DefaultFullSharedAccessSignatureSASConnectionString* et *NotificationHubName* avec les valeurs hello dont vous disposez.
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. Ajouter hello suivant des lignes dans votre **Main** méthode :
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a>Test de l'application
tootest cette application avec un téléphone réelle, seulement se connecter hello ordinateur tooyour de téléphone à l’aide d’un câble USB. Cette action charge votre application sur un téléphone de hello attaché.

Cliquez sur cette application avec l’émulateur hello, hello Eclipse haut la barre d’outils de tootest **exécuter**, puis sélectionnez votre application : il démarre hello émulateur, chargement, et s’exécute hello application.

application Hello récupère hello 'userId' et 'channelId' hello services de notifications Push de Baidu et inscrit avec le hub de notification hello.

toosend une notification de test, vous pouvez utiliser l’onglet débogage de hello Hello portail classique Azure. Si vous avez créé d’application de console .NET hello pour Visual Studio, appuyez sur touche F5 de hello dans l’application de Visual Studio toorun hello. application Hello envoie une notification qui s’affiche dans la zone de notification supérieur de hello de votre appareil ou l’émulateur.

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
[Push Baidu Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[portail classique Azure]: https://manage.windowsazure.com/
[Baidu portail]: http://www.baidu.com/
