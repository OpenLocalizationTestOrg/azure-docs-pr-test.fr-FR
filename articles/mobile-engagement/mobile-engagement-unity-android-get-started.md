---
title: "aaaGet main d’Azure Mobile Engagement pour Android Unity déploiement"
description: "Découvrez comment toouse Azure Mobile Engagement avec Analytique et les Notifications Push pour les applications Unity tooiOS périphériques de déploiement."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a>Prise en main d’Azure Mobile Engagement pour le déploiement de l’application Unity pour Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et comment toosend push utilisateurs toosegmented de notifications d’une application Unity lors du déploiement tooan des appareils Android.
Ce didacticiel utilise hello restaurer de Unity classique un didacticiel boule en tant que point de départ de hello. Vous devez suivre des étapes hello dans ce [didacticiel](mobile-engagement-unity-roll-a-ball.md) avant de poursuivre hello intégration de Mobile Engagement nous exposer dans le didacticiel hello ci-dessous. 

Ce didacticiel requiert hello qui suit :

* [Unity Editor](http://unity3d.com/get-unity)
* [Kit de développement logiciel (SDK) Mobile Engagement pour Unity](https://aka.ms/azmeunitysdk)
* Kit de développement logiciel (SDK) pour Google Android

> [!NOTE]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Essai gratuit d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).
> 
> 

## <a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application Android
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
1. Ouvrez hello **EngagementConfiguration** fichier de script à partir de hello dossier et de mise à jour du Kit de développement logiciel hello **ANDROID\_connexion\_chaîne** avec la chaîne de connexion hello vous avez obtenu version antérieure de hello portail Azure.  
   
    ![][73]
2. Enregistrez le fichier de hello 
3. Exécutez **File -> Engagement -> Generate Android Manifest** (Fichier -> Engagement -> Générer le manifeste Android). Il s’agit plug-in hello ajoutée par hello Kit de développement logiciel de Mobile Engagement et en cliquant sur elle met automatiquement à jour les paramètres du projet. 
   
    ![][74]

> [!IMPORTANT]
> Transformer en tooexecute que chaque fois que vous mettez à jour hello **EngagementConfiguration** fichier dans le cas contraire, vos modifications n’apparaîtront pas dans l’application hello. 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a>Configurer l’application hello pour le suivi de base
1. Ouvrez hello **PlayerController** script joint toohello d’objet lecteur pour la modification. 
2. Ajoutez hello qui suit à l’aide d’instruction :
   
        using Microsoft.Azure.Engagement.Unity;
3. Ajouter hello suivant toohello `Start()` (méthode)
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Déployer et exécuter l’application hello
Assurez-vous que vous disposez du SDK Android installés sur votre ordinateur avant de tenter de toodeploy ce périphérique tooyour d’application Unity. 

1. Connectez un ordinateur de tooyour appareil Android. 
2. Accédez à **File -> Build Settings** (Fichier -> Paramètres de build). 
   
    ![][40]
3. Sélectionnez **Android** (Android), puis cliquez sur **Switch Platform** (Changer de plateforme).
   
    ![][51]
   
    ![][52]
4. Cliquez sur **Player settings** et indiquez un identificateur Bundle Identifier valide. 
   
    ![][53]
5. Pour finir, cliquez sur **Build And Run**
   
    ![][54]
6. Vous pouvez être invité tooprovide un package dossier nom toostore hello Android. 
7. Si tout se passe bien, package de hello sera déployé tooyour connecté appareil et vous devez voir votre jeu Unity sur votre téléphone ! 

## <a id="monitor"></a>Connexion d’application avec l’analyse en temps réel
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a>Mettre à jour hello EngagementConfiguration
1. Ouvrez hello **EngagementConfiguration** fichier de script à partir de hello dossier et de mise à jour du Kit de développement logiciel hello **ANDROID\_GOOGLE\_nombre** avec hello **projet Google Nombre** obtenu précédemment à partir du portail des développeurs de Cloud de Google hello. Il s’agit d’une chaîne de valeur donc pas vraiment tooenclose dans des guillemets doubles. 
   
    ![][75]
2. Enregistrez le fichier de hello. 
3. Exécutez **File -> Engagement -> Generate Android Manifest** (Fichier -> Engagement -> Générer le manifeste Android). Il s’agit plug-in hello ajoutée par hello Kit de développement logiciel de Mobile Engagement et en cliquant sur elle met automatiquement à jour les paramètres du projet. 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a>Configurer des notifications de tooreceive l’application hello
1. Ouvrez hello **PlayerController** script joint toohello d’objet lecteur pour la modification. 
2. Ajouter hello suivant toohello `Start()` (méthode)
   
        EngagementReachAgent.Initialize();
3. Maintenant que hello application est mise à jour, déployer et exécuter l’application hello sur un appareil par les instructions ci-dessous hello. 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
