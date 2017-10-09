---
title: aaaGet en main de Windows universel applications Azure Mobile Engagement
description: "Découvrez comment toouse Azure Mobile Engagement avec analytique et des notifications push pour les applications Windows universelles."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a>Prise en main d’Azure Mobile Engagement pour les applications universelles Windows
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et l’envoi push aux utilisateurs de toosegmented de notifications d’une application Windows universelle.
Ce didacticiel illustre un scénario simple diffusion hello à l’aide de Mobile Engagement. Vous allez créer une application universelle Windows vide, qui collecte des données de base sur l’utilisation des applications et reçoit des notifications Push à l’aide du service de notification Windows.

> [!NOTE]
> Hello Azure Mobile Engagement service mars 2018 est retirée et est actuellement que les clients tooexisting disponibles. Pour plus d’informations, consultez [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

## <a name="prerequisites"></a>Composants requis
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a>Configuration de Mobile Engagement pour votre application universelle Windows
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement
Ce didacticiel présente une « intégration de base, « hello minimale définie les données de toocollect requis et envoyer une notification push. Vous trouverez la documentation sur l’intégration complète Hello dans hello [intégration Mobile Engagement Windows universel SDK](mobile-engagement-windows-store-sdk-overview.md).

Vous créez une application de base avec l’intégration de Visual Studio toodemonstrate hello.

### <a name="create-a-windows-universal-app-project"></a>Création d’un projet d’application universelle Windows
Hello étapes suivantes supposent hello utilisation de Visual Studio 2015 bien que les étapes de hello sont similaires dans les versions antérieures de Visual Studio.

1. Démarrez Visual Studio et Bonjour **accueil** écran, sélectionnez **nouveau projet**.
2. Dans la fenêtre contextuelle hello, sélectionnez **Windows** -> **universel** -> **application vide (Windows universel)**. Renseignez application hello **nom** et **nom de la Solution**, puis cliquez sur **OK**.

    ![][1]

Vous venez de créer un projet d’application universelle de Windows dans lequel vous intégrez ensuite hello Kit de développement logiciel Azure Mobile Engagement.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Se connecter à votre serveur principal d’application tooMobile Engagement
1. Installer hello [MicrosoftAzure.MobileEngagement] package Nuget dans votre projet. Si vous ciblez les plateformes Windows et Windows Phone, vous devez toodo cela pour les deux projets. Pour Windows 8.x et Windows Phone 8.1, hello même Nuget package emplacements hello correct spécifique à la plateforme binaires dans chaque projet.
2. Ouvrez **Package.appxmanifest** et assurez-vous que hello suivant la fonctionnalité est ajoutée :

        Internet (Client)

    ![][2]
3. Copier la chaîne de connexion hello que vous avez copiée précédemment pour votre application d’Engagement Mobile et le coller dans hello maintenant `Resources\EngagementConfiguration.xml` fichier, entre hello `<connectionString>` et `</connectionString>` balises :

    ![][3]

    > [!TIP]
    > Si votre application cible les plateformes Windows et Windows Phone, vous devez quand même créer deux applications Mobile Engagement, une par plateforme prise en charge. Deux applications permet de garantir que vous pouvez créer une segmentation correcte de l’audience de hello et pouvez envoyer des notifications ciblées de façon appropriée pour chaque plateforme.

    > [!IMPORTANT]
    > NuGet ne copie pas automatiquement les ressources du Kit de développement logiciel hello dans votre application Windows 10 UWP. Vous l’avez toodo manuellement comme suit hello qui afficheront (readme.txt) lors de l’installation du package Nuget hello.  

1. Bonjour `App.xaml.cs` fichier :

    a. Ajouter hello `using` instruction :

            using Microsoft.Azure.Engagement;

    b. Ajoutez une méthode qui initialise hello Engagement :

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    c. Initialiser hello SDK Bonjour **OnLaunched** méthode :

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    c. Insérer les suivant hello Bonjour **OnActivated** (méthode) et ajoutez la méthode hello si elle n’est pas déjà présent :

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <a id="monitor"></a>Activation de l’analyse en temps réel
toostart envoi de données et de s’assurer que les utilisateurs hello sont actifs, vous devez envoyer au moins un principal de Mobile Engagement toohello écran (activité).

1. Bonjour **MainPage.xaml.cs**, ajoutez hello suit `using` instruction :

    using Microsoft.Azure.Engagement.Overlay;
2. Modifier la classe de base hello de **MainPage** de **Page** trop**EngagementPageOverlay**:

        class MainPage : EngagementPageOverlay
3. Bonjour `MainPage.xaml` fichier :

    a. Ajoutez les déclarations d’espaces de noms tooyour :

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    b. Remplacez hello **Page** dans le nom de la balise XML hello avec **engagement : EngagementPageOverlay**

> [!IMPORTANT]
> Si votre page substitue hello `OnNavigatedTo` (méthode), être toocall vraiment `base.OnNavigatedTo(e)`. Dans le cas contraire, activité hello n’est pas signalée `EngagementPage` appelle `StartActivity` à l’intérieur de son `OnNavigatedTo` méthode). Cela est particulièrement important dans un projet Windows Phone, où le modèle par défaut de hello a un `OnNavigatedTo` (méthode).
>
> Pour **d’applications Windows 10 universelles**, utiliser la méthode hello recommandé Bonjour » méthode recommandée : surcharger vos classes de Page « section de [avancé Reporting par hello universel applications Engagement Kit de développement](mobile-engagement-windows-store-advanced-reporting.md) , plutôt que de hello une mentionnés ci-dessus.

## <a id="monitor"></a>Connexion d’application avec l’analyse en temps réel
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app
Mobile Engagement vous permet de toointeract et atteindre vos utilisateurs avec des notifications push et les messages dans le contexte de hello de campagnes dans l’application. Ce module est appelé portée dans le portail Mobile Engagement de hello.
Hello sections suivantes configurer votre application tooreceive les.

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a>Activer votre tooreceive application WNS Push Notifications
1. Bonjour `Package.appxmanifest` fichier, Bonjour **Application** sous l’onglet sous **Notifications**, définissez **compatibilité avec les toasts :** trop**Oui**

    ![][5]

### <a name="initialize-hello-reach-sdk"></a>Initialiser hello SDK REACH
Dans `App.xaml.cs`, appelez **EngagementReach.Instance.Init(e) ;** Bonjour **InitEngagement** fonction juste après l’initialisation de l’agent hello :

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

Vous êtes prêt toosend un toast. Ensuite, nous vérifions que l’intégration de base est correcte.

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a>Accorder l’accès tooMobile Engagement toosend notifications
1. Ouvrez le [Centre de développement Windows Store] dans votre navigateur web, connectez-vous et créez un compte si nécessaire.
2. Cliquez sur **tableau de bord** à hello en haut à droite d’angle, puis cliquez sur **créer une application** à partir du menu de gauche du Panneau de configuration hello.

    ![][9]
3. Créez votre application en réservant son nom.

    ![][10]
4. Une fois que l’application hello a été créée, accédez trop**Services -> notifications Push** à partir du menu de gauche hello.

    ![][11]
5. Bonjour Push section notifications, cliquez sur hello **site des Services Live** lien.

    ![][12]
6. Vous accédez section d’informations d’identification toohello par émission de données. Vérifiez que vous êtes dans hello **paramètres de l’application** section, puis copiez votre **SID du Package** et **question secrète du Client**

    ![][13]
7. Accédez toohello **paramètres** de votre portail Mobile Engagement, puis cliquez sur hello **le Push natif** section hello gauche. Ensuite, cliquez sur hello **modifier** bouton tooenter votre **Package SID (security identifier)** et votre **clé secrète** comme indiqué :

    ![][6]
8. Enfin, assurez-vous que vous avez associé votre application Visual Studio avec cette application créée dans le magasin d’applications hello. Cliquez sur **Associer l’application au Windows Store** dans Visual Studio.

    ![][7]

## <a id="send"></a>Envoi d’une application tooyour de notification
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Si l’application hello est en cours d’exécution, vous consultez une notification dans l’application. Sinon, si l’application hello est fermée, vous voyez une notification de toast.
Si vous voyez une notification dans l’application, mais pas une notification toast, et que vous exécutez application hello en mode débogage dans Visual Studio, puis recommencez **cycle de vie des événements -> interrompre** dans tooensure de barre d’outils hello cette application hello est interrompue. Si vous avez cliqué sur bouton d’accueil hello lors du débogage d’application hello dans Visual Studio, puis il ne toujours suspendu et pendant que vous voyez la notification de hello en tant que dans l’application, il n’apparaît pas comme une notification toast.  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Centre de développement Windows Store]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
