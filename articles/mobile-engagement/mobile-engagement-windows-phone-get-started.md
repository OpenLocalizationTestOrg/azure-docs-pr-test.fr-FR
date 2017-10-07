---
title: "aaaGet main d’applications Azure Mobile Engagement pour Windows Phone Silverlight"
description: "Découvrez comment toouse Azure Mobile Engagement avec analytique et des notifications push pour les applications Windows Phone Silverlight."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a>Prise en main d'Azure Mobile Engagement pour les applications Windows Phone Silverlight
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et l’envoi push aux utilisateurs de toosegmented de notifications d’une application Windows Phone Silverlight.
Ce didacticiel illustre un scénario simple diffusion hello à l’aide de Mobile Engagement. Il vous apprend à créer une application Windows Phone Silverlight vide qui collecte des données de base et reçoit des notifications push au moyen du service de notifications push Microsoft (MPNS).

> [!NOTE]
> Hello Azure Mobile Engagement service mars 2018 est retirée et est actuellement que les clients tooexisting disponibles. Pour plus d’informations, consultez [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

> [!NOTE]
> Les projets du Windows Phone 8.1 et des versions antérieures ne sont pas pris en charge dans Visual Studio 2017.  Pour en savoir plus, consultez [Plateforme cible et compatibilité dans Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Si vous ciblez Windows Phone 8.1 (non Silverlight), consultez toohello [didacticiel Windows universel](mobile-engagement-windows-store-dotnet-get-started.md).
> 
> 

Ce didacticiel requiert hello qui suit :

* Visual Studio 2013
* [MicrosoftAzure.MobileEngagement]

> [!NOTE]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).
> 
> 

## <a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application Windows Phone
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement
Ce didacticiel présente une « intégration de base », qui est hello minimal requis toocollect données et envoyer une notification push. Vous trouverez la documentation sur l’intégration complète Hello dans hello [intégration du Kit de développement logiciel Windows Phone Mobile Engagement](mobile-engagement-windows-phone-sdk-overview.md)

Nous allons créer une application de base avec l’intégration de Visual Studio toodemonstrate hello.

### <a name="create-a-new-windows-phone-silverlight-project"></a>Création d'un nouveau projet Windows Phone Silverlight
Hello étapes suivantes supposent hello utilisation de Visual Studio 2015 bien que les étapes de hello sont similaires dans les versions antérieures de Visual Studio. 

1. Démarrez Visual Studio et Bonjour **accueil** écran, sélectionnez **nouveau projet**.
2. Dans la fenêtre contextuelle hello, sélectionnez **Windows 8** -> **Windows Phone** -> **application vide (Silverlight de Windows Phone)**. Renseignez application hello **nom** et **nom de la Solution**, puis cliquez sur **OK**.
   
    ![][1]
3. Vous pouvez choisir soit tootarget **Windows Phone 8.0** ou **Windows Phone 8.1**.

Vous venez de créer une nouvelle application Windows Phone Silverlight dans laquelle nous intégrera hello Kit de développement logiciel Azure Mobile Engagement.

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement
1. Installer hello [MicrosoftAzure.MobileEngagement] package nuget dans votre projet.
2. Ouvrez `WMAppManifest.xml` (sous le dossier Propriétés de hello) et assurez-vous que suivant de hello est déclarées (ajoutez-les si elles ne sont pas) Bonjour `<Capabilities />` balise :
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. Collez la chaîne de connexion hello que vous avez copiée précédemment pour votre application Mobile Engagement maintenant et le coller dans hello `Resources\EngagementConfiguration.xml` fichier, entre hello `<connectionString>` et `</connectionString>` balises :
   
    ![][3]
4. Bonjour `App.xaml.cs` fichier :
   
    a. Ajouter hello `using` instruction :
   
            using Microsoft.Azure.Engagement;
   
    b. Initialiser hello SDK Bonjour `Application_Launching` méthode :
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    c. Insérer les suivant hello Bonjour `Application_Activated`:
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <a id="monitor"></a>Activation de l’analyse en temps réel
Dans l’ordre toostart envoi de données et en garantissant que les utilisateurs de hello sont actifs, vous devez envoyer au moins un principal de Mobile Engagement toohello écran (activité).

1. Bonjour MainPage.xaml.cs, ajouter hello `using` instruction :
   
        using Microsoft.Azure.Engagement;
2. Remplacez la classe de base hello de **MainPage**, c'est-à-dire avant **PhoneApplicationPage**, avec **EngagementPage**.
   
        class MainPage : EngagementPage 
3. Dans votre fichier `MainPage.xml` :
   
    a. Ajoutez les déclarations d’espaces de noms tooyour :
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    b. Remplacez `phone:PhoneApplicationPage` dans le nom de la balise XML hello avec `engagement:EngagementPage`.

## <a id="monitor"></a>Connexion d’application avec l’analyse en temps réel
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app
Mobile Engagement vous permet de toointeract et atteindre vos utilisateurs avec des Notifications Push et de messagerie dans l’application dans le contexte de hello de campagnes. Ce module est appelé portée dans le portail Mobile Engagement de hello.
Hello sections suivantes configurer votre application tooreceive les.

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a>Activer votre tooreceive application Notifications de Push de MPNS
Ajouter de nouvelles fonctionnalités tooyour `WMAppManifest.xml` fichier :

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a>Initialiser hello SDK REACH
1. Dans `App.xaml.cs`, appelez `EngagementReach.Instance.Init();` Bonjour **Application_Launching** fonction, juste après l’initialisation de l’agent hello :
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. Dans `App.xaml.cs`, appelez `EngagementReach.Instance.OnActivated(e);` Bonjour **Application_Activated** fonction, juste après l’initialisation de l’agent hello :
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

Vous êtes prêt. Nous allons maintenant vérifier que vous avez correctement effectué cette intégration de base.

## <a id="send"></a>Envoi d’une application tooyour de notification
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Vous devez maintenant voir une notification sur votre appareil qui s’afficheront en tant qu’une notification dans l’application si l’application hello est ouverte en tant que notification toast hello suivante : 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
