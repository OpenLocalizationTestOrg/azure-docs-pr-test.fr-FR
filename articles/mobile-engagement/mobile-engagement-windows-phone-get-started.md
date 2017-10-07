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
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="50a64-103">Prise en main d'Azure Mobile Engagement pour les applications Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="50a64-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="50a64-104">Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et l’envoi push aux utilisateurs de toosegmented de notifications d’une application Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="50a64-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="50a64-105">Ce didacticiel illustre un scénario simple diffusion hello à l’aide de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="50a64-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="50a64-106">Il vous apprend à créer une application Windows Phone Silverlight vide qui collecte des données de base et reçoit des notifications push au moyen du service de notifications push Microsoft (MPNS).</span><span class="sxs-lookup"><span data-stu-id="50a64-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="50a64-107">Hello Azure Mobile Engagement service mars 2018 est retirée et est actuellement que les clients tooexisting disponibles.</span><span class="sxs-lookup"><span data-stu-id="50a64-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="50a64-108">Pour plus d’informations, consultez [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="50a64-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="50a64-109">Les projets du Windows Phone 8.1 et des versions antérieures ne sont pas pris en charge dans Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="50a64-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="50a64-110">Pour en savoir plus, consultez [Plateforme cible et compatibilité dans Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="50a64-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="50a64-111">Si vous ciblez Windows Phone 8.1 (non Silverlight), consultez toohello [didacticiel Windows universel](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="50a64-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer toohello [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="50a64-112">Ce didacticiel requiert hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="50a64-112">This tutorial requires hello following:</span></span>

* <span data-ttu-id="50a64-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="50a64-113">Visual Studio 2013</span></span>
* <span data-ttu-id="50a64-114">[MicrosoftAzure.MobileEngagement]</span><span class="sxs-lookup"><span data-stu-id="50a64-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="50a64-115">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="50a64-115">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="50a64-116">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="50a64-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="50a64-117">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span><span class="sxs-lookup"><span data-stu-id="50a64-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="50a64-118"><a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application Windows Phone</span><span class="sxs-lookup"><span data-stu-id="50a64-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="50a64-119"><a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="50a64-119"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="50a64-120">Ce didacticiel présente une « intégration de base », qui est hello minimal requis toocollect données et envoyer une notification push.</span><span class="sxs-lookup"><span data-stu-id="50a64-120">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="50a64-121">Vous trouverez la documentation sur l’intégration complète Hello dans hello [intégration du Kit de développement logiciel Windows Phone Mobile Engagement](mobile-engagement-windows-phone-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="50a64-121">hello complete integration documentation can be found in hello [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="50a64-122">Nous allons créer une application de base avec l’intégration de Visual Studio toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="50a64-122">We will create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="50a64-123">Création d'un nouveau projet Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="50a64-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="50a64-124">Hello étapes suivantes supposent hello utilisation de Visual Studio 2015 bien que les étapes de hello sont similaires dans les versions antérieures de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="50a64-124">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="50a64-125">Démarrez Visual Studio et Bonjour **accueil** écran, sélectionnez **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="50a64-125">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="50a64-126">Dans la fenêtre contextuelle hello, sélectionnez **Windows 8** -> **Windows Phone** -> **application vide (Silverlight de Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="50a64-126">In hello pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="50a64-127">Renseignez application hello **nom** et **nom de la Solution**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="50a64-127">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="50a64-128">Vous pouvez choisir soit tootarget **Windows Phone 8.0** ou **Windows Phone 8.1**.</span><span class="sxs-lookup"><span data-stu-id="50a64-128">You can choose tootarget either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="50a64-129">Vous venez de créer une nouvelle application Windows Phone Silverlight dans laquelle nous intégrera hello Kit de développement logiciel Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="50a64-129">You have now created a new Windows Phone Silverlight app into which we will integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="50a64-130">Se connecter à votre serveur principal d’application toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="50a64-130">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="50a64-131">Installer hello [MicrosoftAzure.MobileEngagement] package nuget dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="50a64-131">Install hello [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="50a64-132">Ouvrez `WMAppManifest.xml` (sous le dossier Propriétés de hello) et assurez-vous que suivant de hello est déclarées (ajoutez-les si elles ne sont pas) Bonjour `<Capabilities />` balise :</span><span class="sxs-lookup"><span data-stu-id="50a64-132">Open `WMAppManifest.xml` (under hello Properties folder) and make sure hello following are declared (add them if they are not) in hello `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="50a64-133">Collez la chaîne de connexion hello que vous avez copiée précédemment pour votre application Mobile Engagement maintenant et le coller dans hello `Resources\EngagementConfiguration.xml` fichier, entre hello `<connectionString>` et `</connectionString>` balises :</span><span class="sxs-lookup"><span data-stu-id="50a64-133">Now paste hello connection string that you copied earlier for your Mobile Engagement app and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="50a64-134">Bonjour `App.xaml.cs` fichier :</span><span class="sxs-lookup"><span data-stu-id="50a64-134">In hello `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="50a64-135">a.</span><span class="sxs-lookup"><span data-stu-id="50a64-135">a.</span></span> <span data-ttu-id="50a64-136">Ajouter hello `using` instruction :</span><span class="sxs-lookup"><span data-stu-id="50a64-136">Add hello `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="50a64-137">b.</span><span class="sxs-lookup"><span data-stu-id="50a64-137">b.</span></span> <span data-ttu-id="50a64-138">Initialiser hello SDK Bonjour `Application_Launching` méthode :</span><span class="sxs-lookup"><span data-stu-id="50a64-138">Initialize hello SDK in hello `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="50a64-139">c.</span><span class="sxs-lookup"><span data-stu-id="50a64-139">c.</span></span> <span data-ttu-id="50a64-140">Insérer les suivant hello Bonjour `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="50a64-140">Insert hello following in hello `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="50a64-141"><a id="monitor"></a>Activation de l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="50a64-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="50a64-142">Dans l’ordre toostart envoi de données et en garantissant que les utilisateurs de hello sont actifs, vous devez envoyer au moins un principal de Mobile Engagement toohello écran (activité).</span><span class="sxs-lookup"><span data-stu-id="50a64-142">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="50a64-143">Bonjour MainPage.xaml.cs, ajouter hello `using` instruction :</span><span class="sxs-lookup"><span data-stu-id="50a64-143">In hello MainPage.xaml.cs, add hello `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="50a64-144">Remplacez la classe de base hello de **MainPage**, c'est-à-dire avant **PhoneApplicationPage**, avec **EngagementPage**.</span><span class="sxs-lookup"><span data-stu-id="50a64-144">Replace hello base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="50a64-145">Dans votre fichier `MainPage.xml` :</span><span class="sxs-lookup"><span data-stu-id="50a64-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="50a64-146">a.</span><span class="sxs-lookup"><span data-stu-id="50a64-146">a.</span></span> <span data-ttu-id="50a64-147">Ajoutez les déclarations d’espaces de noms tooyour :</span><span class="sxs-lookup"><span data-stu-id="50a64-147">Add tooyour namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="50a64-148">b.</span><span class="sxs-lookup"><span data-stu-id="50a64-148">b.</span></span> <span data-ttu-id="50a64-149">Remplacez `phone:PhoneApplicationPage` dans le nom de la balise XML hello avec `engagement:EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="50a64-149">Replace `phone:PhoneApplicationPage` in hello XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="50a64-150"><a id="monitor"></a>Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="50a64-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="50a64-151"><a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app</span><span class="sxs-lookup"><span data-stu-id="50a64-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="50a64-152">Mobile Engagement vous permet de toointeract et atteindre vos utilisateurs avec des Notifications Push et de messagerie dans l’application dans le contexte de hello de campagnes.</span><span class="sxs-lookup"><span data-stu-id="50a64-152">Mobile Engagement allows you toointeract and reach your users with Push Notifications and in-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="50a64-153">Ce module est appelé portée dans le portail Mobile Engagement de hello.</span><span class="sxs-lookup"><span data-stu-id="50a64-153">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="50a64-154">Hello sections suivantes configurer votre application tooreceive les.</span><span class="sxs-lookup"><span data-stu-id="50a64-154">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a><span data-ttu-id="50a64-155">Activer votre tooreceive application Notifications de Push de MPNS</span><span class="sxs-lookup"><span data-stu-id="50a64-155">Enable your app tooreceive MPNS Push Notifications</span></span>
<span data-ttu-id="50a64-156">Ajouter de nouvelles fonctionnalités tooyour `WMAppManifest.xml` fichier :</span><span class="sxs-lookup"><span data-stu-id="50a64-156">Add new Capabilities tooyour `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="50a64-157">Initialiser hello SDK REACH</span><span class="sxs-lookup"><span data-stu-id="50a64-157">Initialize hello REACH SDK</span></span>
1. <span data-ttu-id="50a64-158">Dans `App.xaml.cs`, appelez `EngagementReach.Instance.Init();` Bonjour **Application_Launching** fonction, juste après l’initialisation de l’agent hello :</span><span class="sxs-lookup"><span data-stu-id="50a64-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in hello **Application_Launching** function, right after hello agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="50a64-159">Dans `App.xaml.cs`, appelez `EngagementReach.Instance.OnActivated(e);` Bonjour **Application_Activated** fonction, juste après l’initialisation de l’agent hello :</span><span class="sxs-lookup"><span data-stu-id="50a64-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in hello **Application_Activated** function, right after hello agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="50a64-160">Vous êtes prêt.</span><span class="sxs-lookup"><span data-stu-id="50a64-160">You're all set.</span></span> <span data-ttu-id="50a64-161">Nous allons maintenant vérifier que vous avez correctement effectué cette intégration de base.</span><span class="sxs-lookup"><span data-stu-id="50a64-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="50a64-162"><a id="send"></a>Envoi d’une application tooyour de notification</span><span class="sxs-lookup"><span data-stu-id="50a64-162"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="50a64-163">Vous devez maintenant voir une notification sur votre appareil qui s’afficheront en tant qu’une notification dans l’application si l’application hello est ouverte en tant que notification toast hello suivante :</span><span class="sxs-lookup"><span data-stu-id="50a64-163">You should now see a notification on your device which will show up as an in-app notification if hello app is open otherwise as a toast notification like hello following:</span></span> 

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
