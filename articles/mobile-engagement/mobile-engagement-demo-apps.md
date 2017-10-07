---
title: "application de démonstration de Mobile Engagement aaaAzure | Documents Microsoft"
description: "Explique où toodownload, comment toouse et hello les avantages de l’utilisation d’Azure Mobile Engagement démonstration application"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: f624d5aa-254b-4ad0-96a3-f00e6c3a2c97
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2016
ms.author: piyushjo
ms.openlocfilehash: 9ff0df0d21e1bad6aff573db49304a55593df1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-demo-app"></a>Application de démonstration d’Azure Mobile Engagement
Nous avons publié une application de démonstration d’Azure Mobile Engagement pour **iOS**, **Android**, et **Windows** plateformes toohelp vous toofind des ressources utiles et en savoir plus sur Mobile Engagement.

application Hello vous aide à :

* Rechercher facilement les ressources d’Engagement tooMobile comme les vidéos, documentation, forum de support hello, liens utiles et où la fonctionnalité de tooraise toogo demande.
* Notifications d’exemple expérience qui sont pris en charge par les idées de tooget Mobile Engagement pour vos propres applications mobiles.
* Utiliser un toostudy d’implémentation de référence comment tooimplement Mobile Engagement dans votre propre application. Vous découvrirez comment :
  
  * Recueillir des données d’analyse.
  * Implémenter des scénarios de notification avancés de type *Plein écran interstitiel* ou *Fenêtre contextuelle*.
  * Implémenter des enquêtes et des sondages.
  * Implémenter des scénarios push et push données sans assistance.   

## <a name="app-installation"></a>Installation de l’application
Cette application est disponible dans hello suivant des magasins d’applications :

* **Application de démonstration universelle Windows**:
  
  * Télécharger l’application hello en hello [Windows App store](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).
  * application Hello a été développée une application Windows 10 universelles. code source de Hello est disponible sur [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).
* **Application de démonstration iOS**:
  
  * Télécharger l’application hello en hello [Apple store](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).
  * application Hello a été développée dans iOS Swift. code source de Hello est disponible sur [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).
* **Application de démonstration Android**:
  
  * Télécharger l’application hello en hello [Google Play store](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).
  * code source de Hello est disponible sur [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).

![Application de démonstration universelle Windows][1]

![Application de démonstration iOS][2]
![Application de démonstration Android][3]

## <a name="usage"></a>Usage
Vous pouvez utiliser cette application Bonjour suivant façons :

**Télécharger l’application hello sur votre appareil à partir des liens du magasin au niveau application hello (fournis plus haut) :**

> [!IMPORTANT]
> Vous n’avez pas besoin d’un compte Azure ou devez tooconnect hello application tooa principaux. application Hello fonctionne indépendamment.
> 
> 

* Après avoir configuré application hello sur votre appareil, vous pouvez accéder via des liens de hello dans hello menu de gauche toofind hello ressources utiles sur Mobile Engagement.
* Nous avons ajouté hello [flux RSS du service](https://aka.ms/azmerssfeed) à cette application afin que vous êtes toujours mis à jour sur hello dernières mises à jour.
* Vous pouvez également passer par hello notification scénarios tooexperience hello au type d’exemple de notifications qui sont pris en charge par Mobile Engagement pour chaque plateforme. Ces notifications peuvent être expérimentés localement : autrement dit, vous pouvez cliquer sur les boutons hello sur hello écrans tooshow vous hello expérience de notifications, ce qui est de notifications de hello toosending identique à partir de la plateforme Mobile Engagement de hello.

![Menu de l’application pour Windows][4]

![Menu de l’application pour iOS][5]
![Menu de l’application pour Android][6]

**Télécharger le code de source de hello de hello liens GitHub (fournis plus haut) :**

* Après avoir téléchargé le code source de hello, ouvrez-le dans l’environnement de développement respectifs hello XCode pour iOS, Android Studio pour Android et Visual Studio pour Windows.
* Vous devez ensuite suivre nos [base étapes d’intégration SDK](mobile-engagement-windows-store-dotnet-get-started.md) afin que vous êtes en mesure de tooconnect tooits de cette application propriétaire d’instance de serveur principal Mobile Engagement.
  * Vous devez tooconfigure une chaîne de connexion dans l’application hello.
  * Vous devez également la plate-forme de notification push tooconfigure hello pour votre application.
* Vous remarquerez que cette application hello lui-même est instrumentée avec Mobile Engagement. Par conséquent, lorsque vous ouvrez l’application hello après sa connexion toohello back-end, vous serez session d’utilisateur en mesure de toosee hello, activités, événements et ainsi de suite, sur hello **moniteur** onglet.
* Vous serez également en mesure de toosend notifications toothis application à partir de votre propre instance de Mobile Engagement, au lieu d’utiliser des notifications locales.
  
  * Ici vous pouvez ajouter votre appareil en tant qu’un appareil de test à l’aide de hello **Get hello ID de périphérique** élément de menu dans une application hello. Vous obtenez alors un ID d’appareil, que vous inscrivez ensuite comme appareil test avec l’instance de serveur principal de votre plateforme.
    
    ![ID d’appareil sur Windows][7]
    
    ![ID d’appareil sur iOS][8]
    ![ID d’appareil sur Android][9]

## <a name="key-features-of-hello-demo-app"></a>Principales fonctionnalités de l’application de démonstration hello
* Comme mentionné précédemment, avec cette application, vous avez toutes les ressources clés hello pour Mobile Engagement dans main. Vous pouvez accéder via des liens de hello sur le menu de gauche hello.
* Pour chaque plateforme, vous pouvez tester les notifications hors de l’application. Ces notifications peuvent être remises en tant que **Notification uniquement**, simplement en cliquant sur la notification de hello où ouvre un écran natif de l’application hello (à l’aide de **lien profond**)--ou comme un **Web annonce**, où vous pouvez remettre un contenu HTML supplémentaire de hello Mobile Engagement retour de fin toobe affiché lors de la notification de hello est activée.
  
    ![Notifications hors de l’application][29]
* Sur iOS, vous avez tooclose hello application toosee hello hors de l’application ou le système des notifications push. Vous pouvez examiner l’implémentation de hello ici pour ajouter **boutons d’Action**, telles que celles qui sont ajoutées toothis notification hors de l’application pour hello *commentaires* et *partage* (de sorte que Hello utilisateur peut effectuer directement d’action à partir de la notification hello elle-même).
  
    ![Notifications hors de l’application sur iOS][11] ![Affichage de notification hors de l’application sur iOS][14]
* Sur Android, les options de hello qui sont prises en charge sont Ajout de texte multiligne (**texte Big**) ou d’une notification (**présentation**) notification toohello, ainsi que de hello **desboutonsd’Action** (comme la prise en charge par iOS).
  
    ![Notifications hors de l’application sur Android][12] ![Affichage de notification hors de l’application sur Android][15]
* Sur Windows 10, vous pouvez voir l’aspect des notifications de hello sur hello PC. Cette notification s’affiche également dans hello Windows 10 **centre de notifications**. Il n’existe aucune prise en charge pour l’ajout de **boutons d’Action** au moment hello hello Kit de développement logiciel Windows.
  
    ![Notifications hors de l’application sur Windows][10] ![Affichage de notification hors de l’application sur Windows][13]
* Pour chaque plateforme, vous pouvez tester les notifications « dans l’application ». Il s’agit d’une expérience en deux étapes où une fenêtre **Notification** est affichée en premier. Lorsque vous cliquez dessus, il ouvre un plein écran **annonce**, comme indiqué dans hello suivant capture d’écran. le contenu de cette annonce Hello proviennent de votre instance de serveur principal Mobile Engagement. Hello SDK dispose de modèles de hello pour les notifications et annonces. Vous pouvez facilement personnaliser, comme indiqué dans cette application de démonstration avec ajout de hello de notre logo et la coloration de la syntaxe.  
  
    ![Notifications dans l’application sur Windows][16]
  
    ![Notifications dans l’application sur iOS][17]  ![Notifications dans l’application sur Android][18]
  
    **iOS**, **Android**
* Vous pouvez également utiliser hello **catégorie** fonctionnalité de Mobile Engagement toocustomize cette expérience par défaut. Dans l’application de démonstration hello, nous avons démontré de deux façons toochange hello expérience commune de notifications de hello. Notez que cette fonctionnalité de catégorie hello n’est pas encore pris en charge dans hello Kit de développement logiciel Windows.
  
    **Plein écran interstitiel :**
  
    ![Notification dans l’application - catégorie interstitielle][30]
  
    ![Catégorie interstitielle sur iOS][21]     ![Catégorie interstitielle sur Android][22]
  
    **Notification contextuelle :**
  
    ![Notification dans l’application - catégorie contextuelle][31]
  
    ![Notification contextuelle sur iOS][19]    ![Notification contextuelle sur Android][20]

**iOS**, **Android**

* Mobile Engagement prend également en charge un type spécialisé de notification dans l’application appelée **Sondages**. Cela vous permet de toosend les utilisateurs d’application rapide enquêtes tooyour segmenté. Vous pouvez ajouter des questions et les options de chaque question comme hello suivant capture d’écran. Cela sera ensuite s’affichent en tant qu’un utilisateur d’application de toohello notification dans l’application.   
  
    ![Notifications d’interrogation][32]
  
    ![Enquête sur Windows][26]
  
    ![Enquête sur iOS][27]   ![Enquête sur Android][28]

**iOS**, **Android**

* Mobile Engagement prend également en charge l’envoi en mode silencieux de notifications **Push de données** . Avec ces notifications, vous pouvez envoyer des données à partir de votre service (par exemple hello données JSON dans hello exemple suivant), que vous pouvez gérer dans votre application et prendre des mesures. Un exemple est comment nous passons prix hello d’un élément de manière sélective à l’aide des notifications push de données.
  
    ![Notification Push de données][33]
  
    ![Notification Push de données sur Windows][23]
  
    ![Notification Push de données sur iOS][24]  ![Notification Push de données sur Android][25]

**iOS**, **Android**

> [!NOTE]
> Vous pouvez afficher des instructions détaillées pour une de ces notifications en cliquant sur **cliquez ici pour obtenir des instructions sur la façon de toosend ces notifications à partir de la plateforme Mobile Engagement** sur n’importe quel écran : exemple de notification.
> 
> 

[1]: ./media/mobile-engagement-demo-apps/home-windows.png
[2]: ./media/mobile-engagement-demo-apps/home-ios.png
[3]: ./media/mobile-engagement-demo-apps/home-android.png
[4]: ./media/mobile-engagement-demo-apps/menu-windows.png
[5]: ./media/mobile-engagement-demo-apps/menu-ios.png
[6]: ./media/mobile-engagement-demo-apps/menu-android.png
[7]: ./media/mobile-engagement-demo-apps/device-id-windows.png
[8]: ./media/mobile-engagement-demo-apps/device-id-ios.png
[9]: ./media/mobile-engagement-demo-apps/device-id-android.png
[10]: ./media/mobile-engagement-demo-apps/out-of-app-windows.png
[11]: ./media/mobile-engagement-demo-apps/out-of-app-ios.png
[12]: ./media/mobile-engagement-demo-apps/out-of-app-android.png
[13]: ./media/mobile-engagement-demo-apps/out-of-app-display-windows.png
[14]: ./media/mobile-engagement-demo-apps/out-of-app-display-ios.png
[15]: ./media/mobile-engagement-demo-apps/out-of-app-display-android.png
[16]: ./media/mobile-engagement-demo-apps/in-app-windows.png
[17]: ./media/mobile-engagement-demo-apps/in-app-ios.png
[18]: ./media/mobile-engagement-demo-apps/in-app-android.png
[19]: ./media/mobile-engagement-demo-apps/pop-up-ios.png
[20]: ./media/mobile-engagement-demo-apps/pop-up-android.png
[21]: ./media/mobile-engagement-demo-apps/interstitial-ios.png
[22]: ./media/mobile-engagement-demo-apps/interstitial-android.png
[23]: ./media/mobile-engagement-demo-apps/data-push-windows.png
[24]: ./media/mobile-engagement-demo-apps/data-push-ios.png
[25]: ./media/mobile-engagement-demo-apps/data-push-android.png
[26]: ./media/mobile-engagement-demo-apps/survey-windows.png
[27]: ./media/mobile-engagement-demo-apps/survey-ios.png
[28]: ./media/mobile-engagement-demo-apps/survey-android.png
[29]: ./media/mobile-engagement-demo-apps/out-of-app.png
[30]: ./media/mobile-engagement-demo-apps/in-app-interstitial.png
[31]: ./media/mobile-engagement-demo-apps/in-app-pop-up.png
[32]: ./media/mobile-engagement-demo-apps/notification-poll.png
[33]: ./media/mobile-engagement-demo-apps/notification-data-push.png
