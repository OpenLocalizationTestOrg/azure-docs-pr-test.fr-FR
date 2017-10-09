---
title: notifications push aaaSend tooChrome les applications avec Azure Notification Hubs | Documents Microsoft
description: "Découvrez comment toouse Azure Notification Hubs toosend push notifications tooa Chrome application."
services: notification-hubs
keywords: notifications push mobiles, notifications push, notification push, notifications push chrome
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 7dec8ab02622563bc3730a2e96820da8932d22f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a>Envoyer des notifications d’applications tooChrome avec Azure Notification Hubs push
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

Cette rubrique vous montre comment toouse Azure Notification Hubs toosend push notifications tooa application Chrome qui sera affiché dans le contexte de hello Hello navigateur Google Chrome. Dans ce didacticiel, nous allons créer une application Chrome qui reçoit des notifications push à l’aide de [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/). 

> [!NOTE]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).
> 
> 

didacticiel de Hello vous guide tout au long de ces notifications de push tooenable étapes de base :

* [Activation de Google Cloud Messaging](#register)
* [Configuration de votre hub de notification](#configure-hub)
* [Se connecter à votre hub de notification d’application de Chrome toohello](#connect-app)
* [Envoyer un tooyour de notification push Chrome application](#send)
* [Fonctionnalités et capacités supplémentaires](#next-steps)

> [!NOTE]
> Notifications push de l’application chrome ne sont pas des notifications dans un navigateur génériques - ils sont le modèle d’extensibilité de navigateur toohello spécifique (consultez [vue d’ensemble des applications de Chrome] pour plus d’informations). En outre toohello navigateur de bureau, Chrome applications s’exécutent sur mobile (Android et iOS) via Apache Cordova. Consultez [applications Chrome sur Mobile] toolearn plus.
> 
> 

Configuration GCM et Azure Notification Hubs est identiques tooconfiguring pour Android, car [de messagerie Cloud Google Chrome] a été déconseillée et hello GCM même prend désormais en charge les appareils Android et instances de Chrome.

## <a id="register"></a>Activer Google Cloud Messaging
1. Accédez toohello [Google Cloud Console] site Web, connectez-vous avec vos informations d’identification du compte Google, puis cliquez sur hello **créer un projet** bouton. Fournir un **nom du projet**, puis cliquez sur hello **créer** bouton.
   
       ![Google Cloud Console - Create Project][1]
2. Prenez note de hello **numéro de projet** sur hello **projets** page hello projet que vous venez de créer. Vous allez utiliser comme hello **ID de l’expéditeur GCM** dans tooregister de Chrome application hello avec GCM.
   
       ![Google Cloud Console - Project Number][2]
3. Dans le volet gauche de hello, cliquez sur **API & auth**et faites défiler vers le bas, puis cliquez sur hello bascule tooenable **Google Cloud Messaging pour Android**. Vous n’avez pas tooenable **de messagerie Cloud Google Chrome**.
   
       ![Google Cloud Console - Server Key][3]
4. Dans le volet gauche de hello, cliquez sur **informations d’identification** > **créer une nouvelle clé** > **clé serveur** > **créer**.
   
       ![Google Cloud Console - Credentials][4]
5. Prenez note du serveur de hello **clé API**. Vous allez configurer cela dans votre tooenable suivant, concentrateur de notification Il tooGCM de notifications push toosend.
   
       ![Google Cloud Console - API Key][5]

## <a id="configure-hub"></a>Configuration de votre hub de notification
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   Bonjour **paramètres** panneau, sélectionnez **Notification Services** , puis **Google (GCM)**. Entrez la clé d’API hello et enregistrer.

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <a id="connect-app"></a>Se connecter à votre hub de notification d’application de Chrome toohello
Votre concentrateur de notification est maintenant configuré toowork avec GCM, et vous avez tooregister de chaînes de connexion hello tooboth de votre application de réception et envoyer des notifications push. LK

### <a name="create-a-new-chrome-app"></a>Création d’une application Chrome
exemple Hello ci-dessous est basé sur hello [Chrome application GCM exemple] et utilise hello recommandé toocreate de la façon dont une application de Chrome. Il met en surbrillance hello étapes tooAzure concernant spécifiquement concentrateurs de Notification. 

> [!NOTE]
> Nous vous conseillons de télécharger la source de hello pour cette application de Chrome de [exemple Hub de Notification d’application Chrome].
> 
> 

Hello Chrome application est créé via JavaScript, et vous pouvez utiliser tous vos éditeurs word par défaut pour sa création. Voici à quoi ressemblera cette application Chrome.

![Application Google Chrome][15]

1. Créez un dossier et nommez-le `ChromePushApp`. Bien entendu, le nom de hello est arbitraire - si vous lui donner un nommez différent, assurez-vous que vous remplacez chemin hello dans les segments de code hello requis.
2. Télécharger hello [crypto-js bibliothèque] dans le dossier hello créé à l’étape de deuxième hello. Ce dossier contiendra deux sous-dossiers : `components` et `rollups`.
3. Créez un fichier `manifest.json` . Toutes les applications de Chrome sont soutenues par un fichier manifeste qui contient les métadonnées de l’application hello et, le plus important encore, toutes les autorisations accordées toohello application lorsque l’utilisateur de hello l’installe.
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    Hello d’avis `permissions` élément, ce qui indique que cette application Chrome sera en mesure de tooreceive notifications push GCM. Il doit également spécifier hello Azure Notification Hubs URI où hello Chrome application fera une tooregister d’appel REST.
    Notre exemple d’application utilise également un fichier icône, `gcm_128.png`, que vous trouverez sur source hello qui est réutilisé à partir de l’exemple GCM hello d’origine. Vous pouvez le remplacer pour toute image qui correspond à hello [critères d’icône](https://developer.chrome.com/apps/manifest/icons).
4. Créez un fichier appelé `background.js` avec hello suivant de code :
   
        // Returns a new notification ID used in hello notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs tooform a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification tooshow hello GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners tootrigger hello first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    Il s’agit des fichiers hello qui s’affiche la fenêtre d’application de Chrome hello HTML (**register.html**) et définit également le Gestionnaire de hello **messageReceived** toohandle hello entrants de notifications push.
5. Créez un fichier appelé `register.html` -définit hello l’interface utilisateur de hello Chrome application. 
   
   > [!NOTE]
   > Cet exemple utilise **CryptoJS v3.1.2**. Si vous avez téléchargé une autre version de la bibliothèque de hello, assurez-vous que vous remplacez correctement version hello Bonjour `src` chemin d’accès.
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. Créez un fichier appelé `register.js` avec le code hello ci-dessous. Ce fichier Spécifie le script hello derrière `register.html`. Applications de chrome n’autorisent pas l’exécution inline, afin que vous ayez toocreate un script de sauvegarde distinct pour votre interface utilisateur.
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before hello registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When hello registration fails, handle hello error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that hello first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update hello payload with hello registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    Hello au-dessus de script a hello paramètres clés suivants :
   
   * **Window.OnLoad** définit les événements de clic de bouton hello des boutons de hello deux sur hello l’interface utilisateur. Un inscrit avec GCM et hello autres utilise l’ID d’inscription hello qui est retournée après l’inscription avec tooregister GCM avec Azure Notification Hubs.
   * **updateLog** est fonction hello qui nous permet de toohandle des fonctions d’enregistrement simple.
   * **registerWithGCM** est le Gestionnaire de clic de bouton premier hello, ce qui rend hello `chrome.gcm.register` appel tooGCM tooregister hello Chrome application instance en cours.
   * **registerCallback** est fonction de rappel hello qui est appelée lorsque hello appel d’inscription GCM retourne.
   * **registerWithNH** est le Gestionnaire de clic de bouton deuxième hello, qui inscrit avec Notification Hubs. Il obtient `hubName` et `connectionString` (utilisateur hello a spécifié) et les travaux manuels hello appel d’API REST de Notification Hubs d’inscription.
   * **splitConnectionString** et **generateSaSToken** sont des programmes d’assistance qui représentent l’implémentation JavaScript de hello d’un processus de création d’un jeton SaS, qui doit être utilisé dans tous les appels d’API REST. Pour plus d’informations, consultez la page [Concepts courants](http://msdn.microsoft.com/library/dn495627.aspx).
   * **sendNHRegistrationRequest** appel de fonction hello qui rend un HTTP REST est tooAzure Notification Hubs.
   * **registrationPayload** définit la charge utile de hello d’enregistrement XML. Pour plus d’informations, voir [Création de l’API REST NH d’inscription]. Nous mettre à jour l’ID d’inscription hello qu’elle contient avec ce que nous avons reçu de GCM.
   * **client** est une instance de **XMLHttpRequest** que nous utilisons demande de requête HTTP POST toomake hello. Notez que nous mettre à jour hello `Authorization` en-tête avec `sasToken`. La réussite de cet appel enregistre cette instance de l’application Chrome auprès d’Azure Notification Hubs.

Hello globale structure de dossiers pour ce projet doit ressembler à ceci : ![Google Chrome application - Structure de dossiers][21]

### <a name="set-up-and-test-your-chrome-app"></a>Installation et test de votre application Chrome
1. Ouvrez votre navigateur Chrome. Ouvrez la page **Extensions** de Chrome et activez **Mode développeur**.
   
       ![Google Chrome - Enable Developer Mode][16]
2. Cliquez sur **de charger l’extension décompressée** et accédez dossier toohello où vous avez créé des fichiers de hello. Vous pouvez également utiliser hello **Chrome applications et outils de développement d’Extensions**. Cet outil est une application de Chrome en soi (installée à partir de hello Chrome Web Store) et fournit des fonctionnalités de débogage avancées pour le développement de vos applications de Chrome.
   
       ![Google Chrome - Load Unpacked Extension][17]
3. Si hello Chrome application est créé sans erreur, puis vous verrez votre application Chrome s’affichent.
   
       ![Google Chrome - Chrome App Display][18]
4. Entrez hello **numéro de projet** que vous avez obtenu précédemment hello **Google Cloud Console** en tant qu’ID d’expéditeur hello, puis cliquez sur **inscrire auprès de GCM**. Vous devez voir le message de type hello **inscription GCM a réussi.**
   
       ![Google Chrome - Chrome App Customization][19]
5. Entrez votre **nom du concentrateur de Notification** et hello **DefaultListenSharedAccessSignature** que vous avez obtenu de portail hello précédemment, puis cliquez sur **inscrire auprès d’Azure Notification Hub**. Vous devez voir le message de type hello **inscription de concentrateur de Notification réussie !** ID de détails hello de réponse d’inscription de hello, qui contient les hello d’inscription d’Azure Notification Hubs.
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <a name="send"></a>Envoyer une notification de tooyour Chrome application
À des fins de test, nous envoyons des notifications push Chrome à l’aide d’une application de console .NET. 

> [!NOTE]
> Vous pouvez envoyer des notifications push en utilisant Notification Hubs à partir d’un serveur principal utilisant notre <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interface REST</a> publique. Découvrez notre [portail de documentation](https://azure.microsoft.com/documentation/services/notification-hubs/) pour plus d’exemples interplateformes.
> 
> 

1. Dans Visual Studio, à partir de hello **fichier** menu, sélectionnez **nouveau** , puis **projet**. Sous **Visual C#**, cliquez sur **Windows** et **Application Console**, puis cliquez sur **OK**.  Un projet d'application console est créé.
2. À partir de hello **outils** menu, cliquez sur **Gestionnaire de Package de bibliothèque** , puis **Package Manager Console**. Cette opération affiche hello Console du Gestionnaire de Package.
3. Dans la fenêtre de console hello, exécutez hello de commande suivante :
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. Ouvrez `Program.cs` et ajoutez hello suit `using` instruction :
   
        using Microsoft.Azure.NotificationHubs;
5. Bonjour `Program` de classe, ajoutez hello suivant de méthode :
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > Assurez-vous que vous utilisez avec la chaîne de connexion de hello **complète** accéder, pas **écouter** accès. Hello **écouter** chaîne de connexion d’accès à ne pas accorde des autorisations des notifications push de toosend.
   > 
   > 
6. Ajouter hello suite à des appels Bonjour `Main` méthode :
   
         SendNotificationAsync();
         Console.ReadLine();
7. Vérifiez que Chrome est en cours d’exécution et exécuter l’application de console hello.
8. Vous devez voir s’afficher hello notification contextuelle sur votre bureau.
   
       ![Google Chrome - Notification][13]
9. Vous pouvez également voir toutes vos notifications (dans Windows) à l’aide de la fenêtre de Notifications de Chrome hello dans la barre des tâches hello lorsque Chrome est en cours d’exécution.
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> Vous n’avez pas besoin toohave hello Chrome application en cours d’exécution ou ouvrir dans le navigateur hello (même si le navigateur Chrome de hello lui-même doit être en cours d’exécution). Vous obtenez également une vue consolidée de toutes vos notifications dans la fenêtre de Notifications de Chrome hello.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur Notification Hubs dans la [Vue d’ensemble de Notification Hubs].

tootarget des utilisateurs spécifiques, consultez toohello [Azure Notification Hubs notifier utilisateurs] didacticiel. 

Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, vous pouvez suivre hello [Azure Notification Hubs actualités] didacticiel.

<!-- Images. -->
[1]: ./media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: ./media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: ./media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: ./media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: ./media/notification-hubs-chrome-get-started/ServerKey.png
[6]: ./media/notification-hubs-chrome-get-started/CreateNH.png
[7]: ./media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: ./media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: ./media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: ./media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: ./media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: ./media/notification-hubs-chrome-get-started/NHConnString.png
[13]: ./media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: ./media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: ./media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: ./media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: ./media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: ./media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: ./media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: ./media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: ./media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
[exemple Hub de Notification d’application Chrome]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[Google Cloud Console]: http://cloud.google.com/console
[Azure Classic Portal]: https://manage.windowsazure.com/
[Vue d’ensemble de Notification Hubs]: notification-hubs-push-notification-overview.md
[vue d’ensemble des applications de Chrome]: https://developer.chrome.com/apps/about_apps
[Chrome application GCM exemple]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[applications Chrome sur Mobile]: https://developer.chrome.com/apps/chrome_apps_on_mobile
[Création de l’API REST NH d’inscription]: http://msdn.microsoft.com/library/azure/dn223265.aspx
[crypto-js bibliothèque]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[de messagerie Cloud Google Chrome]: https://developer.chrome.com/apps/cloudMessagingV1
[Azure Notification Hubs notifier utilisateurs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Azure Notification Hubs actualités]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
