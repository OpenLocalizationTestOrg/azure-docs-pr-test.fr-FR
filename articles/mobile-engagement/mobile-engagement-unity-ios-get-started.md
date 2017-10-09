---
title: "aaaGet main d’Azure Mobile Engagement pour le déploiement d’iOS Unity"
description: "Découvrez comment toouse Azure Mobile Engagement avec Analytique et les Notifications Push pour les applications Unity tooiOS périphériques de déploiement."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a>Prise en main d’Azure Mobile Engagement pour le déploiement de l’application Unity pour iOS
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et comment toosend push utilisateurs toosegmented de notifications d’une application Unity lors du déploiement de l’appareil iOS tooan.
Ce didacticiel utilise hello restaurer de Unity classique un didacticiel boule en tant que point de départ de hello. Vous devez suivre des étapes hello dans ce [didacticiel](mobile-engagement-unity-roll-a-ball.md) avant de poursuivre hello intégration de Mobile Engagement nous exposer dans le didacticiel hello ci-dessous. 

Ce didacticiel requiert hello qui suit :

* [Unity Editor](http://unity3d.com/get-unity)
* [Kit de développement logiciel (SDK) Mobile Engagement pour Unity](https://aka.ms/azmeunitysdk)
* Éditeur XCode

> [!NOTE]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).
> 
> 

## <a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement
### <a name="import-hello-unity-package"></a>Importer un package Unity hello
1. Télécharger hello [package Mobile Engagement Unity](https://aka.ms/azmeunitysdk) et enregistrez-le tooyour les ordinateur local. 
2. Accédez trop**ressources -> Importer un Package -> Package personnalisé** et sélectionnez hello vous avez téléchargé dans hello ci-dessus étape. 
   
    ![][70] 
3. Vérifiez que tous les fichiers sont sélectionnés, puis cliquez sur le bouton **Import** . 
   
    ![][71] 
4. Une fois l’importation a réussi, vous verrez les fichiers de kit de développement logiciel de hello importé dans votre projet.  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a>Mettre à jour hello EngagementConfiguration
1. Ouvrez hello **EngagementConfiguration** fichier de script à partir de hello dossier et de mise à jour du Kit de développement logiciel hello **IOS\_connexion\_chaîne** avec la chaîne de connexion hello obtenues précédemment à partir de hello portail Azure.  
   
    ![][73]
2. Enregistrez le fichier de hello. 

### <a name="configure-hello-app-for-basic-tracking"></a>Configurer l’application hello pour le suivi de base
1. Ouvrez hello **PlayerController** script joint toohello d’objet lecteur pour la modification. 
2. Ajoutez hello qui suit à l’aide d’instruction :
   
        using Microsoft.Azure.Engagement.Unity;
3. Ajouter hello suivant toohello `Start()` (méthode)
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Déployer et exécuter l’application hello
1. Connectez un ordinateur de tooyour périphérique iOS. 
2. Accédez à **File -> Build Settings** (Fichier -> Paramètres de build). 
   
    ![][40]
3. Sélectionnez **Android** (Android), puis cliquez sur **Switch Platform** (Changer de plateforme).
   
    ![][41]
   
    ![][42]
4. Cliquez sur **Player settings** et indiquez un identificateur Bundle Identifier valide. 
   
    ![][53]
5. Pour finir, cliquez sur **Build And Run**
   
    ![][54]
6. Vous pouvez être invité tooprovide un package de dossier nom toostore hello iOS. 
   
    ![][43]
7. Si tout se passe correctement, puis projet de hello sera compilé et vous devez ouvrir sur votre application XCode. 
8. Vérifiez que hello **identificateur de lot** est correct dans le projet de hello.  
   
    ![][75]
9. Exécutez maintenant application hello dans XCode, afin que le package de hello est un périphérique connecté tooyour déployé et vous devez voir votre jeu Unity sur votre téléphone ! 

## <a id="monitor"></a>Connexion d’application avec l’analyse en temps réel
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app
Mobile Engagement vous permet de toointeract avec vos utilisateurs et portée avec des notifications push et les messages dans le contexte de hello de campagnes dans l’application. Ce module est appelé portée dans le portail Mobile Engagement de hello.
Vous n’avez aucune configuration supplémentaire toodo dans vos notifications tooreceive de l’application et elle est déjà configurée pour celui-ci.

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
