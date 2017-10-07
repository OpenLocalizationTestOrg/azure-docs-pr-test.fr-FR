---
title: "aaaGet main d’Azure Mobile Engagement pour Cordova/Phonegap"
description: "Découvrez comment toouse Azure Mobile Engagement avec Analytique et les Notifications Push pour les applications Cordova/Phonegap."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a>Prise en main d'Azure Mobile Engagement pour Cordova/Phonegap
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Cette rubrique vous montre comment toounderstand d’Azure Mobile Engagement toouse développées par votre application d’utilisation et d’envoi push notifications toosegmented les utilisateurs d’une application mobile avec Cordova.

Dans ce didacticiel, nous allons créer une application Cordova vide à l'aide de Mac et intégrer le Kit de développement logiciel (SDK) Mobile Engagement. Elle collectera des données d'analyse de base et recevra des notifications push à l'aide du système de notifications push Apple (APNS) pour iOS et de Google Cloud Messaging (GCM) pour Android. Nous déploiera ce tooan appareil iOS ou Android pour le test. 

> [!NOTE]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).
> 
> 

Ce didacticiel requiert hello qui suit :

* XCode, que vous pouvez installer à partir de Mac App Store (pour le déploiement tooiOS)
* [Android SDK & émulateur](http://developer.android.com/sdk/installing/index.html) (pour le déploiement tooAndroid)
* Certificat de notification Push (.p12) que vous pouvez obtenir dans votre centre de développement Apple pour l’APNS
* Numéro du projet GCM que vous pouvez obtenir à partir de votre Console de développement Google pour GCM
* [Plug-in Mobile Engagement Cordova](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> Vous pouvez trouver le code source de hello et hello fichier Lisezmoi pour le plug-in de hello Cordova sur [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)
> 
> 

## <a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Connexion de votre serveur principal d’application toohello Mobile Engagement
Ce didacticiel présente une « intégration de base « hello minimale définie les données de toocollect requis et envoyer une notification push. 

Nous allons créer une application de base avec l’intégration de hello toodemonstrate Cordova :

### <a name="create-a-new-cordova-project"></a>Création d’un nouveau projet Cordova
1. Lancez *Terminal* fenêtre sur votre hello Mac machine et le type suivant qui créera un nouveau projet Cordova à partir du modèle par défaut de hello. Assurez-vous que la publication hello profil vous finalement toodeploy d’utiliser votre application iOS est à l’aide de 'com.mycompany.myapp' comme hello identifiant d’application. 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. Exécutez hello suivant tooconfigure votre projet pour **iOS** et exécutez-la dans hello, iOS Simulator :
   
        $ cordova platform add ios 
        $ cordova run ios
3. Exécutez hello suivant tooconfigure votre projet pour **Android** et l’exécuter dans l’émulateur Android de hello. Vérifiez vos paramètres de l’émulateur Kit de développement logiciel Android que sa cible en tant que Google APIs (Google Inc.) avec hello CPU / ABI sous forme de Google APIs ARM.  
   
        $ cordova platform add android
        $ cordova run android
4. Ajoutez hello plug-in Cordova Console. 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Se connecter à votre serveur principal d’application tooMobile Engagement
1. Installez le plug-in de hello Azure Mobile Engagement Cordova tout en offrant hello valeurs des variables tooconfigure hello plug-in :
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

*Icône d’atteindre Android* : doit être nom hello de ressource hello sans toute extension ni le préfixe drawable (ex : mynotificationicon), et le fichier d’icône hello doit être copié dans votre projet android (plateformes/android/res/drawable)

*iOS atteindre une icône* : doit être nom hello de ressource hello avec l’extension (ex : mynotificationicon.png), et le fichier d’icône hello doit être ajouté à votre projet iOS avec XCode (à l’aide de hello Ajouter fichiers Menu)

## <a id="monitor"></a>Activation de la surveillance en temps réel
1. Dans le projet de Cordova hello - modifier **www/js/index.js** appel de hello tooadd tooMobile Engagement toodeclare une nouvelle activité une fois hello *deviceReady* événement est reçu.
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. Exécutez l’application hello :
   
   * **Pour iOS**
     
       Dans `Terminal` fenêtre lancez votre application dans une nouvelle instance de simulateur en exécutant hello qui suit :
     
           cordova run ios
   * **Pour Android**
     
       Dans `Terminal` fenêtre lancez votre application dans une nouvelle instance de l’émulateur en exécutant hello qui suit :
     
           cordova run android
3. Vous pouvez voir suivant hello dans les journaux de la console hello :
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <a id="monitor"></a>Connexion d’application avec l’analyse en temps réel
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Activation des notifications Push et de la messagerie intégrée à l’application
Mobile Engagement vous permet de toointeract avec vos utilisateurs à l’aide de Notifications Push et les messages dans le contexte de hello de campagnes dans l’application. Ce module est appelé portée dans le portail Mobile Engagement de hello.
Hello sections suivantes va installer votre application tooreceive les.

### <a name="configure-push-credentials-for-mobile-engagement"></a>Configuration des informations d'identification Push pour Mobile Engagement
tooallow Mobile Engagement toosend des Notifications Push à votre place, vous devez toogrant il accéder au certificat de tooyour Apple iOS ou de la clé d’API GCM serveur. 

1. Accédez portail Mobile Engagement de tooyour. Vérifiez dans l’application hello que nous utilisons pour ce projet et que vous cliquez ensuite sur hello **Engage** bouton bas hello :
   
    ![][1]
2. Vous allez arriver dans la page des paramètres hello dans votre portail d’Engagement. À partir de là, cliquez sur hello **le Push natif** section :
   
    ![][2]
3. Configuration du certificat iOS/de la clé d’API serveur GCM
   
    **[iOS]**
   
    a. Sélectionnez votre .p12, téléchargez-le et tapez votre mot de passe :
   
    ![][3]
   
    **[Android]**
   
    a. Cliquez sur icône d’édition hello devant **clé API** Bonjour section GCM paramètres et dans la fenêtre contextuelle hello qui s’affiche, collez hello GCM clé du serveur, puis cliquez sur **OK**. 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a>Activer les notifications push dans l’application de Cordova hello
Modifier **www/js/index.js** tooadd hello appel tooMobile Engagement toorequest des notifications push et déclarer un gestionnaire :

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a>Exécutez l’application hello
**[iOS]**

1. Nous utilise XCode toobuild et déploiement d’une application de hello sur des notifications push de hello appareil tootest comme iOS permet uniquement le périphérique réel du tooan des notifications push. Atteindre l’emplacement toohello où votre projet Cordova est créé et accédez trop**...\platforms\ios** emplacement. Ouvrez le fichier .xcodeproj natif de hello dans XCode. 
2. Générez et déployez hello Cordova application toohello l’appareil iOS à l’aide du compte hello hello contenant le certificat hello que vous venez de télécharger portail Mobile Engagement de toohello et hello Id d’application qui correspond à hello vous fourni lors de la création de profil de configuration Hello d’application Cordova. Vous pouvez extraire hello *identificateur de lot* dans votre **ressources\*-info.plist** fichier dans XCode toomatch haut. 
3. Vous verrez la fenêtre contextuelle des e/s standard hello sur votre appareil indiquant que cette application hello demande notifications toosend d’autorisation. Accordez l’autorisation de hello. 

**[Android]**

Vous pouvez simplement utiliser hello émulateur toorun hello application Android comme émulateur Android de hello prennent en charge les notifications GCM. 

    cordova run android

## <a id="send"></a>Envoi d’une application tooyour de notification
Nous allons maintenant créer une campagne de Notification Push simple qui envoie une application de tooyour par émission de données en cours d’exécution sur l’appareil de hello :

1. Accédez toohello **atteindre** onglet dans votre portail Mobile Engagement
2. Cliquez sur **nouvelle annonce** toocreate votre campagne push
   
    ![][6]
3. Fournir des entrées toocreate votre campagne **[Android]**
   
   * Entrez un **nom** pour votre campagne. 
   * Sélectionnez hello **Type de remise** en tant que *notification système* *Simple*
   * Sélectionnez hello **heure de remise** comme *« Any Time »*
   * Fournir un **titre** pour votre notification qui sera hello première ligne de commande de hello.
   * Fournir un **Message** pour votre notification qui servira de corps du message hello. 
     
     ![][11]
4. Fournir des entrées toocreate votre campagne **[e]**
   
   * Entrez un **nom** pour votre campagne. 
   * Sélectionnez hello **heure de remise** comme *« hors de l’application »*
   * Fournir un **titre** pour votre notification qui sera hello première ligne de commande de hello.
   * Fournir un **Message** pour votre notification qui servira de corps du message hello. 
     
     ![][12]
5. Faites défiler et Bonjour section de contenu, sélectionnez **Notification uniquement**
   
    ![][8]
6. [Facultatif] Vous pouvez également fournir une URL d’action. Assurez-vous qu’il utilise un modèle d’URL fourni lors de la configuration du plug-in de hello **AZME\_rediriger\_URL** variable, par exemple *myapp://test*.  
7. Vous avez terminé possible de campagne paramètre hello plus simple. Maintenant défiler à nouveau vers le bas et cliquez sur hello **créer** bouton toosave votre campagne.
8. Enfin, dernière étape, **activez** votre campagne.
   
    ![][10]
9. Vous devriez maintenant voir une notification Push sur votre appareil ou votre émulateur dans le cadre de cette campagne. 

## <a id="next-steps"></a>Étapes suivantes
[Vue d'ensemble de toutes les méthodes disponibles avec le Kit de développement logiciel (SDK) Cordova Mobile Engagement](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

