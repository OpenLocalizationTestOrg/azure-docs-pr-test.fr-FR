---
title: tooApache de Notifications Push aaaAdd application Cordova avec les applications mobiles Azure | Documents Microsoft
description: "Découvrez comment toouse Azure Mobile Apps toosend push notifications tooyour Apache Cordova application."
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a>Ajouter une application de push notifications tooyour Apache Cordova
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Vue d'ensemble
Dans ce didacticiel, vous ajoutez le projet toohello [démarrage rapide de Apache Cordova] de notifications push afin qu’une notification push est envoyée toohello périphérique chaque fois qu’un enregistrement est inséré.

Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez hello package d’extension de notification push. Pour plus d’informations, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure][1].

## <a name="prerequisites"></a>Configuration requise
Ce didacticiel décrit une application Apache Cordova développée avec Visual Studio 2015 qui s’exécute sur hello émulateur Android de Google, un appareil Android, un périphérique Windows et un appareil iOS.

toocomplete ce didacticiel, vous devez :

* Un PC avec [Visual Studio Community 2015][2] ou version ultérieure.
* [Visual Studio Tools pour Apache Cordova][4].
* Un [compte Azure actif][3].
* Un projet [Démarrage rapide Apache Cordova][5] .
* Un [compte Google][6] avec une adresse électronique vérifiée.
* (iOS) Un [abonnement au programme pour développeurs Apple][7] et un appareil iOS (le simulateur iOS ne prend pas en charge les notifications Push).
* (Windows) Un [compte de développeur Windows Store][8] et un appareil Windows 10.

## <a name="configure-hub"></a>Configurer un hub de notification
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

[Regarder une vidéo illustrant les étapes de cette section][9]

## <a name="update-hello-server-project"></a>Mettre à jour le projet de serveur hello
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="add-push-to-app"></a>Modification de votre application Cordova
Assurez-vous que votre projet d’application Apache Cordova est prêt toohandle des notifications de push par plug-in du push de Cordova hello lors de l’installation ainsi que tous les services par émission de données spécifiques à la plateforme.

#### <a name="update-hello-cordova-version-in-your-project"></a>Mettre à jour la version de Cordova hello dans votre projet.
Si votre projet utilise une version antérieure à v6.1.1 d’Apache Cordova, mettre à jour le projet de client hello. projet de hello tooupdate :

* Avec le bouton droit `config.xml` Concepteur de configuration tooopen hello.
* Sélectionnez l’onglet de plateformes hello.
* Choisissez 6.1.1 Bonjour **Cordova CLI** zone de texte.
* Choisissez **générer**, puis **générer la Solution** projet hello de tooupdate.

#### <a name="install-hello-push-plugin"></a>Installez le plug-in de hello push
En mode natif, les applications Apache Cordova ne gèrent pas les fonctionnalités de réseau ou d’appareils.  Ces fonctionnalités sont fournies par des plug-ins publiés sur [npm][10] ou sur GitHub.  Hello `phonegap-plugin-push` plug-in est toohandle utilisé réseau les notifications push.

Vous pouvez installer le plug-in de hello par émission de données dans une des manières suivantes :

**À partir de hello d’invite de commandes :**

Exécutez hello de commande suivante :

    cordova plugin add phonegap-plugin-push

**À partir de Visual Studio :**

1. Dans l’Explorateur de solutions, ouvrez hello `config.xml` fichier, cliquez sur **plug-ins** > **personnalisé**, sélectionnez **Git** comme source d’installation, puis entrez `https://github.com/phonegap/phonegap-plugin-push`en tant que source de hello.

   ![][img1]

2. Cliquez sur source d’installation toohello suivant hello flèche.
3. Dans **SENDER_ID**, si vous avez déjà un ID numérique de projet pour le projet de Console des développeurs Google hello, vous pouvez l’ajouter ici. Entrez temporairement une valeur d’espace réservé, par exemple, 777777.  Si vous ciblez Android, vous pourrez modifier cette valeur dans le fichier config.xml ultérieurement.
4. Cliquez sur **Add**.

le plug-in de Hello push est maintenant installé.

#### <a name="install-hello-device-plugin"></a>Installez le plug-in de hello appareil
Suivez hello même procédure que vous avez utilisé le plug-in de tooinstall hello par émission de données.  Ajouter le plug-in de hello appareil à partir de la liste de plug-ins hello Core (cliquez sur **plug-ins** > **Core** toofind il). Vous avez besoin de ce nom de la plateforme plug-in tooobtain hello.

#### <a name="register-your-device-on-application-start-up"></a>Inscription de votre appareil au démarrage de l’application
Initialement, nous proposons un code minimal pour Android. Par la suite, modifiez toorun d’application hello sur iOS ou Windows 10.

1. Ajoutez un appel trop**registerForPushNotifications** pendant le rappel hello pour le processus de connexion hello ou bas hello hello **onDeviceReady** méthode :

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    Cet exemple montre l’appel de **registerForPushNotifications** après une authentification réussie.  Vous pouvez appeler `registerForPushNotifications()` aussi souvent que nécessaire.

2. Ajouter hello nouvelle **registerForPushNotifications** méthode comme suit :

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. (Android) Bonjour précédant le code, remplacez `Your_Project_ID` avec numérique de hello ID du projet pour votre application à partir de la [Console des développeurs Google][18].

## <a name="optional-configure-and-run-hello-app-on-android"></a>(Facultatif) Configurer et exécuter l’application hello sur Android
Effectuez cette section tooenable push les notifications pour Android.

#### <a name="enable-gcm"></a>Activation de Firebase Cloud Messaging
Étant donné que nous prévoyons initialement hello plateforme de Google Android, vous devez activer Firebase de messagerie Cloud.

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <a name="configure-backend"></a>Configurer hello à l’aide de FCM des demandes par l’application Mobile back-end toosend par émission de données
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a>Configuration de votre application Cordova pour Android
Dans votre application Cordova, ouvrez le fichier config.xml et remplacez `Your_Project_ID` avec numérique de hello ID du projet pour votre application à partir de hello [Console des développeurs Google][18].

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

Ouvrez index.js et mettre à jour toouse de code hello votre ID de projet numérique.

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <a name="configure-device"></a>Configuration de votre appareil Android pour le débogage USB
Avant de déployer votre application de tooyour appareil Android, vous devez tooenable débogage USB.  Sur votre téléphone Android, procédez comme suit :

1. Accédez trop**paramètres** > **propos du téléphone**, puis appuyez sur hello **numéro de Build** jusqu'à ce que le mode développeur est activé (environ sept fois).
2. Dans les **paramètres** > **Developer Options** activer **débogage USB**, puis connectez votre PC de développement tooyour téléphone Android avec un câble USB.

Nous avons testé cette procédure à l’aide d’un appareil Google Nexus 5 X exécutant Android 6.0 (Marshmallow).  Toutefois, les techniques de hello sont communs à n’importe quelle version d’Android moderne.

#### <a name="install-google-play-services"></a>Installation des services Google Play
le plug-in de Hello push s’appuie sur Android Services Google Play pour des notifications push.

1. Dans Visual Studio, cliquez sur **outils** > **Android** > **Android SDK Manager**, développez hello **Extras** dossier et vérifiez hello boîte toomake que chacun des hello suivant des kits de développement logiciel est installé.

   * Android 2.3 ou version ultérieure
   * Révision du référentiel Google 27 ou version ultérieure
   * Google Play Services 9.0.2 ou version ultérieure

2. Cliquez sur **installer les Packages** et attendez hello installation toocomplete.

Hello actuel requis bibliothèques sont répertoriées dans hello [la documentation d’installation du plug-in-push phonegap][19].

#### <a name="test-push-notifications-in-hello-app-on-android"></a>Notifications push de test dans une application hello sur Android
Vous pouvez à présent des notifications push de test en exécutant hello application et l’insertion d’éléments dans la table TodoItem de hello. Vous pouvez tester de hello même appareil ou à partir d’un deuxième appareil, tant que vous utilisez hello même principal. Tester votre application Cordova sur la plateforme Android de hello dans un des hello suivant façons :

* **Sur un appareil physique :** attacher votre ordinateur de développement tooyour appareil Android avec un câble USB.  Au lieu de **l’Émulateur Google Android**, sélectionnez **Appareil**. Visual Studio déploie l’appareil de toohello application hello, puis exécute application hello.  Ensuite, vous pouvez interagir avec l’application hello sur l’appareil de hello.

  Améliorez votre expérience du développement.  Les applications de partage d’écran telles que [Mobizen] [20] peuvent vous aider à développer une application Android.  Mobizen projette votre navigateur web de tooa écran Android sur votre PC.

* **Sur un émulateur Android :** des étapes de configuration supplémentaires sont requises lors de l’exécution sur un émulateur.

    Assurez-vous que vous déployez un périphérique virtuel tooa disposant APIs Google défini en tant que cible de hello, comme indiqué dans le Gestionnaire de périphériques virtuels Android (AVD) hello.

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    Si vous souhaitez un x86 plus rapide que toouse émulateur, vous [installer le pilote HAXM à hello] [ 11] et configurer hello émulateur toouse il.

    Ajouter un appareil Android de Google compte toohello en cliquant sur **applications** > **paramètres** > **Ajouter compte**, puis suivez les invites hello.

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    Exécutez hello d’application todolist comme avant et insérer un nouvel élément de tâche. Cette fois-ci, une icône de notification s’affiche dans la zone de notification hello. Vous pouvez ouvrir hello notification tiroir tooview hello texte intégral de la notification de hello.

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a>(Facultatif) Configurer et exécuter sur iOS
Cette section est de projet Cordova de hello en cours d’exécution sur les appareils iOS. Vous pouvez ignorer cette section si vous n'utilisez pas d'appareils iOS.

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a>Installer et iOS hello exécution à distance de l’agent de build sur un Mac ou un service cloud
Avant de pouvoir exécuter une application Cordova sur iOS à l’aide de Visual Studio, ouvrez hello de hello [Guide d’installation iOS] [ 12] tooinstall et hello exécution à distance de l’agent de build.

Assurez-vous que vous pouvez créer des application hello pour iOS. Hello étapes hello guide d’installation sont requis toobuild pour iOS depuis Visual Studio. Si vous n’avez pas d’un Mac, vous pouvez générer pour iOS à l’aide de l’agent de build distante hello sur un service comme MacInCloud. Pour plus d’informations, consultez [exécuter votre application iOS dans le cloud de hello][21].

> [!NOTE]
> XCode 7 ou version ultérieure est plug-in de push de hello toouse requis sur iOS.

#### <a name="find-hello-id-toouse-as-your-app-id"></a>Trouver hello ID toouse en tant que votre ID d’application
Avant d’inscrire votre application pour les notifications push, ouvrez le fichier config.xml dans votre application Cordova, recherche hello `id` valeur dans l’élément de widget hello d’attribut et le copier pour une utilisation ultérieure. Bonjour XML suivant, ID de hello est `io.cordova.myapp7777777`.

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

Vous utiliserez cet identifiant ultérieurement lors de la création d’un ID d’application sur le portail des développeurs d’Apple. Si vous créez un autre ID d’application sur le portail des développeurs hello, vous devez prendre quelques étapes supplémentaires plus loin dans ce didacticiel. ID de Hello dans l’élément widget doit correspondre à hello ID d’application sur le portail des développeurs hello.

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Inscrire l’application hello pour les notifications push sur le portail des développeurs d’Apple
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[Regarder une vidéo montrant des étapes similaires](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a>Configurer des notifications push de toosend Azure
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a>Vérifier que votre ID d’application correspond à votre application Cordova
Si hello déjà créés dans votre compte de développeur Apple ID d’application correspond à hello des ID d’élément de widget hello dans le fichier config.xml, vous pouvez ignorer cette étape. Toutefois, si les identificateurs hello ne correspondent pas, prendre hello comme suit :

1. Supprimer le dossier de plateformes hello de votre projet.
2. Supprimer le dossier de plug-ins hello de votre projet.
3. Supprimez le dossier node_modules hello votre projet.
4. Mettre à jour d’attribut d’id hello d’élément de widget hello dans config.xml toouse hello ID d’application que vous avez créé dans votre compte de développeur Apple.
5. Régénérez votre projet.

##### <a name="test-push-notifications-in-your-ios-app"></a>Tester les notifications Push dans votre application iOS
1. Dans Visual Studio, assurez-vous que **iOS** est sélectionné comme cible de déploiement hello, puis choisissez **périphérique** toorun sur votre appareil iOS connecté.

    Vous pouvez exécuter sur un tooyour de périphérique connecté iOS PC à l’aide d’iTunes. Hello, iOS Simulator ne prend pas en charge des notifications push.

2. Hello de presse **exécuter** bouton ou **F5** dans Visual Studio toobuild projet de hello début hello application dans un appareil iOS, puis cliquez sur **OK** tooaccept les notifications push.

   > [!NOTE]
   > application Hello demande confirmation pour les notifications push pendant hello première exécution.

3. Dans l’application hello, une tâche, puis tapez hello plus (+) icône.
4. Vérifiez qu’une notification est reçue, puis cliquez sur OK toodismiss hello notification.

## <a name="optional-configure-and-run-on-windows"></a>(Facultatif) Configurer et exécuter sur Windows
Cette section est pour l’exécution du projet d’application hello Apache Cordova sur les appareils Windows 10 (plug-in de hello PhoneGap push est pris en charge sur Windows 10). Vous pouvez ignorer cette section si vous n'utilisez pas d'appareils Windows.

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a>Inscrire votre application Windows pour les notifications Push avec WNS
options du magasin toouse hello dans Visual Studio, sélectionnez une cible de Windows à partir de la liste des plateformes de Solution hello, tel que **Windows-x64** ou **Windows-x86** (éviter **Windows-AnyCPU** pour les notifications push).

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

[Regarder une vidéo montrant des étapes similaires][13]

#### <a name="configure-hello-notification-hub-for-wns"></a>Configuration d’un concentrateur de notification hello pour WNS
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a>Configurer votre application Cordova toosupport Windows push notifications
Concepteur de configuration Open hello (avec le bouton droit sur le fichier config.xml et sélectionnez **Concepteur de vue**), sélectionnez hello **Windows** onglet, puis choisissez **Windows 10** sous **Windows ciblent la Version**.

toosupport des notifications de push de la valeur par défaut (debug) génère, ouvrez build.json fichier. Copier la configuration de débogage de tooyour de configuration « release ».

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

Après la mise à jour de hello, hello build.json doit contenir hello suivant de code :

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

Générez l’application hello et vérifiez que vous ne disposez d’aucune erreur. Votre application cliente doit désormais s’inscrire aux notifications de hello à partir de la principal de l’application Mobile hello. Répétez cette section pour chaque projet Windows dans votre solution.

#### <a name="test-push-notifications-in-your-windows-app"></a>Tester les notifications Push dans votre application Windows
Dans Visual Studio, assurez-vous qu’une plateforme Windows est sélectionnée comme cible de déploiement hello, tel que **Windows-x64** ou **Windows-x86**. application de hello toorun sur un PC Windows 10 qui héberge Visual Studio, choisissez **ordinateur Local**.

Hello de presse exécuter bouton toobuild hello projet et démarrer l’application hello.

Dans l’application hello, tapez un nom pour un nouveau todoitem, puis cliquez sur hello plus (+) icône tooadd il.

Vérifiez qu’une notification est reçue lors de l’élément de hello est ajouté.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [concentrateurs de Notification] [ 17] toolearn à propos des notifications push.
* Si vous ne le n'avez pas déjà fait, continuer le didacticiel hello par [Ajout de l’authentification] [ 14] tooyour Apache Cordova application.

Découvrez comment toouse hello kits de développement logiciel.

* [Kit de développement logiciel (SDK) Apache Cordova][15]
* [Kit de développement logiciel du serveur ASP.NET][1]
* [Kit de développement logiciel du serveur Node.js][16]

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/
