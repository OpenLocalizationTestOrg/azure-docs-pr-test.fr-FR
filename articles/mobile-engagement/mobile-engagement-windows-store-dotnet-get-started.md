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
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="61a31-103">Prise en main d’Azure Mobile Engagement pour les applications universelles Windows</span><span class="sxs-lookup"><span data-stu-id="61a31-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="61a31-104">Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et l’envoi push aux utilisateurs de toosegmented de notifications d’une application Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="61a31-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Universal application.</span></span>
<span data-ttu-id="61a31-105">Ce didacticiel illustre un scénario simple diffusion hello à l’aide de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="61a31-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="61a31-106">Vous allez créer une application universelle Windows vide, qui collecte des données de base sur l’utilisation des applications et reçoit des notifications Push à l’aide du service de notification Windows.</span><span class="sxs-lookup"><span data-stu-id="61a31-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="61a31-107">Hello Azure Mobile Engagement service mars 2018 est retirée et est actuellement que les clients tooexisting disponibles.</span><span class="sxs-lookup"><span data-stu-id="61a31-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="61a31-108">Pour plus d’informations, consultez [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="61a31-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61a31-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="61a31-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="61a31-110">Configuration de Mobile Engagement pour votre application universelle Windows</span><span class="sxs-lookup"><span data-stu-id="61a31-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="61a31-111"><a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="61a31-111"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="61a31-112">Ce didacticiel présente une « intégration de base, « hello minimale définie les données de toocollect requis et envoyer une notification push.</span><span class="sxs-lookup"><span data-stu-id="61a31-112">This tutorial presents a "basic integration," which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="61a31-113">Vous trouverez la documentation sur l’intégration complète Hello dans hello [intégration Mobile Engagement Windows universel SDK](mobile-engagement-windows-store-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61a31-113">hello complete integration documentation can be found in hello [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="61a31-114">Vous créez une application de base avec l’intégration de Visual Studio toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="61a31-114">You create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="61a31-115">Création d’un projet d’application universelle Windows</span><span class="sxs-lookup"><span data-stu-id="61a31-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="61a31-116">Hello étapes suivantes supposent hello utilisation de Visual Studio 2015 bien que les étapes de hello sont similaires dans les versions antérieures de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="61a31-116">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="61a31-117">Démarrez Visual Studio et Bonjour **accueil** écran, sélectionnez **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="61a31-117">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="61a31-118">Dans la fenêtre contextuelle hello, sélectionnez **Windows** -> **universel** -> **application vide (Windows universel)**.</span><span class="sxs-lookup"><span data-stu-id="61a31-118">In hello pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="61a31-119">Renseignez application hello **nom** et **nom de la Solution**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="61a31-119">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="61a31-120">Vous venez de créer un projet d’application universelle de Windows dans lequel vous intégrez ensuite hello Kit de développement logiciel Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="61a31-120">You have now created a Windows Universal App project into which you next integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="61a31-121">Se connecter à votre serveur principal d’application tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="61a31-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="61a31-122">Installer hello [MicrosoftAzure.MobileEngagement] package Nuget dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="61a31-122">Install hello [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="61a31-123">Si vous ciblez les plateformes Windows et Windows Phone, vous devez toodo cela pour les deux projets.</span><span class="sxs-lookup"><span data-stu-id="61a31-123">If you are targeting both Windows and Windows Phone platforms, you need toodo this for both projects.</span></span> <span data-ttu-id="61a31-124">Pour Windows 8.x et Windows Phone 8.1, hello même Nuget package emplacements hello correct spécifique à la plateforme binaires dans chaque projet.</span><span class="sxs-lookup"><span data-stu-id="61a31-124">For Windows 8.x and Windows Phone 8.1, hello same Nuget package places hello correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="61a31-125">Ouvrez **Package.appxmanifest** et assurez-vous que hello suivant la fonctionnalité est ajoutée :</span><span class="sxs-lookup"><span data-stu-id="61a31-125">Open **Package.appxmanifest** and make sure that hello following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="61a31-126">Copier la chaîne de connexion hello que vous avez copiée précédemment pour votre application d’Engagement Mobile et le coller dans hello maintenant `Resources\EngagementConfiguration.xml` fichier, entre hello `<connectionString>` et `</connectionString>` balises :</span><span class="sxs-lookup"><span data-stu-id="61a31-126">Now copy hello connection string that you copied earlier for your Mobile Engagement App and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="61a31-127">Si votre application cible les plateformes Windows et Windows Phone, vous devez quand même créer deux applications Mobile Engagement, une par plateforme prise en charge.</span><span class="sxs-lookup"><span data-stu-id="61a31-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="61a31-128">Deux applications permet de garantir que vous pouvez créer une segmentation correcte de l’audience de hello et pouvez envoyer des notifications ciblées de façon appropriée pour chaque plateforme.</span><span class="sxs-lookup"><span data-stu-id="61a31-128">Having two apps ensures that you can create correct segmentation of hello audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="61a31-129">NuGet ne copie pas automatiquement les ressources du Kit de développement logiciel hello dans votre application Windows 10 UWP.</span><span class="sxs-lookup"><span data-stu-id="61a31-129">NuGet does not automatically copy hello SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="61a31-130">Vous l’avez toodo manuellement comme suit hello qui afficheront (readme.txt) lors de l’installation du package Nuget hello.</span><span class="sxs-lookup"><span data-stu-id="61a31-130">You have toodo it manually following hello steps which show up (readme.txt) when hello Nuget package is installed.</span></span>  

1. <span data-ttu-id="61a31-131">Bonjour `App.xaml.cs` fichier :</span><span class="sxs-lookup"><span data-stu-id="61a31-131">In hello `App.xaml.cs` file:</span></span>

    <span data-ttu-id="61a31-132">a.</span><span class="sxs-lookup"><span data-stu-id="61a31-132">a.</span></span> <span data-ttu-id="61a31-133">Ajouter hello `using` instruction :</span><span class="sxs-lookup"><span data-stu-id="61a31-133">Add hello `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="61a31-134">b.</span><span class="sxs-lookup"><span data-stu-id="61a31-134">b.</span></span> <span data-ttu-id="61a31-135">Ajoutez une méthode qui initialise hello Engagement :</span><span class="sxs-lookup"><span data-stu-id="61a31-135">Add a method that initializes hello Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    <span data-ttu-id="61a31-136">c.</span><span class="sxs-lookup"><span data-stu-id="61a31-136">c.</span></span> <span data-ttu-id="61a31-137">Initialiser hello SDK Bonjour **OnLaunched** méthode :</span><span class="sxs-lookup"><span data-stu-id="61a31-137">Initialize hello SDK in hello **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    <span data-ttu-id="61a31-138">c.</span><span class="sxs-lookup"><span data-stu-id="61a31-138">c.</span></span> <span data-ttu-id="61a31-139">Insérer les suivant hello Bonjour **OnActivated** (méthode) et ajoutez la méthode hello si elle n’est pas déjà présent :</span><span class="sxs-lookup"><span data-stu-id="61a31-139">Insert hello following in hello **OnActivated** method and add hello method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <span data-ttu-id="61a31-140"><a id="monitor"></a>Activation de l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="61a31-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="61a31-141">toostart envoi de données et de s’assurer que les utilisateurs hello sont actifs, vous devez envoyer au moins un principal de Mobile Engagement toohello écran (activité).</span><span class="sxs-lookup"><span data-stu-id="61a31-141">toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="61a31-142">Bonjour **MainPage.xaml.cs**, ajoutez hello suit `using` instruction :</span><span class="sxs-lookup"><span data-stu-id="61a31-142">In hello **MainPage.xaml.cs**, add hello following `using` statement:</span></span>

    <span data-ttu-id="61a31-143">using Microsoft.Azure.Engagement.Overlay;</span><span class="sxs-lookup"><span data-stu-id="61a31-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="61a31-144">Modifier la classe de base hello de **MainPage** de **Page** trop**EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="61a31-144">Change hello base class of **MainPage** from **Page** too**EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="61a31-145">Bonjour `MainPage.xaml` fichier :</span><span class="sxs-lookup"><span data-stu-id="61a31-145">In hello `MainPage.xaml` file:</span></span>

    <span data-ttu-id="61a31-146">a.</span><span class="sxs-lookup"><span data-stu-id="61a31-146">a.</span></span> <span data-ttu-id="61a31-147">Ajoutez les déclarations d’espaces de noms tooyour :</span><span class="sxs-lookup"><span data-stu-id="61a31-147">Add tooyour namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="61a31-148">b.</span><span class="sxs-lookup"><span data-stu-id="61a31-148">b.</span></span> <span data-ttu-id="61a31-149">Remplacez hello **Page** dans le nom de la balise XML hello avec **engagement : EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="61a31-149">Replace hello **Page** in hello XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61a31-150">Si votre page substitue hello `OnNavigatedTo` (méthode), être toocall vraiment `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="61a31-150">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="61a31-151">Dans le cas contraire, activité hello n’est pas signalée `EngagementPage` appelle `StartActivity` à l’intérieur de son `OnNavigatedTo` méthode).</span><span class="sxs-lookup"><span data-stu-id="61a31-151">Otherwise, hello activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="61a31-152">Cela est particulièrement important dans un projet Windows Phone, où le modèle par défaut de hello a un `OnNavigatedTo` (méthode).</span><span class="sxs-lookup"><span data-stu-id="61a31-152">This is especially important in a Windows Phone project where hello default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="61a31-153">Pour **d’applications Windows 10 universelles**, utiliser la méthode hello recommandé Bonjour » méthode recommandée : surcharger vos classes de Page « section de [avancé Reporting par hello universel applications Engagement Kit de développement](mobile-engagement-windows-store-advanced-reporting.md) , plutôt que de hello une mentionnés ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="61a31-153">For **Windows 10 Universal apps**, use hello method recommended in hello "Recommended method: overload your Page classes" section of [Advanced Reporting with hello Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than hello one mentioned above.</span></span>

## <span data-ttu-id="61a31-154"><a id="monitor"></a>Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="61a31-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="61a31-155"><a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app</span><span class="sxs-lookup"><span data-stu-id="61a31-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="61a31-156">Mobile Engagement vous permet de toointeract et atteindre vos utilisateurs avec des notifications push et les messages dans le contexte de hello de campagnes dans l’application.</span><span class="sxs-lookup"><span data-stu-id="61a31-156">Mobile Engagement allows you toointeract and reach your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="61a31-157">Ce module est appelé portée dans le portail Mobile Engagement de hello.</span><span class="sxs-lookup"><span data-stu-id="61a31-157">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="61a31-158">Hello sections suivantes configurer votre application tooreceive les.</span><span class="sxs-lookup"><span data-stu-id="61a31-158">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a><span data-ttu-id="61a31-159">Activer votre tooreceive application WNS Push Notifications</span><span class="sxs-lookup"><span data-stu-id="61a31-159">Enable your app tooreceive WNS Push Notifications</span></span>
1. <span data-ttu-id="61a31-160">Bonjour `Package.appxmanifest` fichier, Bonjour **Application** sous l’onglet sous **Notifications**, définissez **compatibilité avec les toasts :** trop**Oui**</span><span class="sxs-lookup"><span data-stu-id="61a31-160">In hello `Package.appxmanifest` file, in hello **Application** tab, under **Notifications**, set **Toast capable:** too**Yes**</span></span>

    ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="61a31-161">Initialiser hello SDK REACH</span><span class="sxs-lookup"><span data-stu-id="61a31-161">Initialize hello REACH SDK</span></span>
<span data-ttu-id="61a31-162">Dans `App.xaml.cs`, appelez **EngagementReach.Instance.Init(e) ;** Bonjour **InitEngagement** fonction juste après l’initialisation de l’agent hello :</span><span class="sxs-lookup"><span data-stu-id="61a31-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in hello **InitEngagement** function right after hello agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="61a31-163">Vous êtes prêt toosend un toast.</span><span class="sxs-lookup"><span data-stu-id="61a31-163">You're ready toosend a toast.</span></span> <span data-ttu-id="61a31-164">Ensuite, nous vérifions que l’intégration de base est correcte.</span><span class="sxs-lookup"><span data-stu-id="61a31-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a><span data-ttu-id="61a31-165">Accorder l’accès tooMobile Engagement toosend notifications</span><span class="sxs-lookup"><span data-stu-id="61a31-165">Grant access tooMobile Engagement toosend notifications</span></span>
1. <span data-ttu-id="61a31-166">Ouvrez le [Centre de développement Windows Store] dans votre navigateur web, connectez-vous et créez un compte si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="61a31-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="61a31-167">Cliquez sur **tableau de bord** à hello en haut à droite d’angle, puis cliquez sur **créer une application** à partir du menu de gauche du Panneau de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="61a31-167">Click **Dashboard** at hello top right corner and then click **Create a new app** from hello left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="61a31-168">Créez votre application en réservant son nom.</span><span class="sxs-lookup"><span data-stu-id="61a31-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="61a31-169">Une fois que l’application hello a été créée, accédez trop**Services -> notifications Push** à partir du menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="61a31-169">Once hello app has been created, navigate too**Services -> Push notifications** from hello left menu.</span></span>

    ![][11]
5. <span data-ttu-id="61a31-170">Bonjour Push section notifications, cliquez sur hello **site des Services Live** lien.</span><span class="sxs-lookup"><span data-stu-id="61a31-170">In hello Push notifications section, click hello **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="61a31-171">Vous accédez section d’informations d’identification toohello par émission de données.</span><span class="sxs-lookup"><span data-stu-id="61a31-171">You navigate toohello Push credentials section.</span></span> <span data-ttu-id="61a31-172">Vérifiez que vous êtes dans hello **paramètres de l’application** section, puis copiez votre **SID du Package** et **question secrète du Client**</span><span class="sxs-lookup"><span data-stu-id="61a31-172">Make sure you are in hello **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="61a31-173">Accédez toohello **paramètres** de votre portail Mobile Engagement, puis cliquez sur hello **le Push natif** section hello gauche.</span><span class="sxs-lookup"><span data-stu-id="61a31-173">Navigate toohello **Settings** of your Mobile Engagement portal, and click hello **Native Push** section on hello left.</span></span> <span data-ttu-id="61a31-174">Ensuite, cliquez sur hello **modifier** bouton tooenter votre **Package SID (security identifier)** et votre **clé secrète** comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="61a31-174">Then, click hello **Edit** button tooenter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="61a31-175">Enfin, assurez-vous que vous avez associé votre application Visual Studio avec cette application créée dans le magasin d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="61a31-175">Finally make sure that you have associated your Visual Studio app with this created app in hello App store.</span></span> <span data-ttu-id="61a31-176">Cliquez sur **Associer l’application au Windows Store** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="61a31-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="61a31-177"><a id="send"></a>Envoi d’une application tooyour de notification</span><span class="sxs-lookup"><span data-stu-id="61a31-177"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="61a31-178">Si l’application hello est en cours d’exécution, vous consultez une notification dans l’application.</span><span class="sxs-lookup"><span data-stu-id="61a31-178">If hello app is running, you see an in-app notification.</span></span> <span data-ttu-id="61a31-179">Sinon, si l’application hello est fermée, vous voyez une notification de toast.</span><span class="sxs-lookup"><span data-stu-id="61a31-179">otherwise if hello app is closed, you see a toast notification.</span></span>
<span data-ttu-id="61a31-180">Si vous voyez une notification dans l’application, mais pas une notification toast, et que vous exécutez application hello en mode débogage dans Visual Studio, puis recommencez **cycle de vie des événements -> interrompre** dans tooensure de barre d’outils hello cette application hello est interrompue.</span><span class="sxs-lookup"><span data-stu-id="61a31-180">If you see an in-app notification but not a toast notification, and you are running hello app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in hello toolbar tooensure that hello app is suspended.</span></span> <span data-ttu-id="61a31-181">Si vous avez cliqué sur bouton d’accueil hello lors du débogage d’application hello dans Visual Studio, puis il ne toujours suspendu et pendant que vous voyez la notification de hello en tant que dans l’application, il n’apparaît pas comme une notification toast.</span><span class="sxs-lookup"><span data-stu-id="61a31-181">If you clicked hello Home button while debugging hello application in Visual Studio, then it doesn't always get suspended and while you see hello notification as in-app, it doesn't show up as a toast notification.</span></span>  

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
