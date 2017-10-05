---
title: "Prise en main d'Azure Mobile Engagement pour les applications Windows Phone Silverlight"
description: "Découvrez comment utiliser Azure Mobile Engagement avec les analyses et les notifications push pour les applications Windows Phone Silverlight."
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
ms.openlocfilehash: d2334a59d83c90bdd02c4fa29261d36aad292892
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="a43c6-103">Prise en main d'Azure Mobile Engagement pour les applications Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="a43c6-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="a43c6-104">Cette rubrique vous explique comment utiliser Azure Mobile Engagement pour comprendre l'utilisation de votre application et envoyer des notifications Push à des utilisateurs segmentés d'une application Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="a43c6-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="a43c6-105">Ce didacticiel montre un scénario de diffusion simple à l'aide de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a43c6-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="a43c6-106">Il vous apprend à créer une application Windows Phone Silverlight vide qui collecte des données de base et reçoit des notifications push au moyen du service de notifications push Microsoft (MPNS).</span><span class="sxs-lookup"><span data-stu-id="a43c6-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="a43c6-107">Le service Azure Mobile Engagement ne sera plus disponible à partir de mars 2018. Actuellement, il reste uniquement accessible aux clients déjà abonnés à ce service.</span><span class="sxs-lookup"><span data-stu-id="a43c6-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="a43c6-108">Pour plus d’informations, consultez la page [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="a43c6-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="a43c6-109">Les projets du Windows Phone 8.1 et des versions antérieures ne sont pas pris en charge dans Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="a43c6-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="a43c6-110">Pour en savoir plus, consultez [Plateforme cible et compatibilité dans Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="a43c6-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="a43c6-111">Si vous ciblez Windows Phone 8.1 (non-Silverlight), consultez le [didacticiel Windows Universal](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a43c6-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer to the [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="a43c6-112">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a43c6-112">This tutorial requires the following:</span></span>

* <span data-ttu-id="a43c6-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="a43c6-113">Visual Studio 2013</span></span>
* <span data-ttu-id="a43c6-114">[MicrosoftAzure.MobileEngagement] </span><span class="sxs-lookup"><span data-stu-id="a43c6-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="a43c6-115">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="a43c6-115">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a43c6-116">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="a43c6-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a43c6-117">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span><span class="sxs-lookup"><span data-stu-id="a43c6-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="a43c6-118"><a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application Windows Phone</span><span class="sxs-lookup"><span data-stu-id="a43c6-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="a43c6-119"><a id="connecting-app"></a>Connexion de votre application au serveur principal Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a43c6-119"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="a43c6-120">Ce didacticiel aborde l'intégration de base qui correspond aux éléments nécessaires à la collection de données et à l'envoi de notifications push.</span><span class="sxs-lookup"><span data-stu-id="a43c6-120">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="a43c6-121">La documentation complète d’intégration peut être consultée dans [Intégration du Kit de développement logiciel (SDK) Windows Phone pour Azure Mobile Engagement.](mobile-engagement-windows-phone-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a43c6-121">The complete integration documentation can be found in the [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="a43c6-122">Nous allons créer une application basique à l'aide de Visual Studio pour la démonstration de l'intégration.</span><span class="sxs-lookup"><span data-stu-id="a43c6-122">We will create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="a43c6-123">Création d'un nouveau projet Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="a43c6-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="a43c6-124">Les étapes suivantes supposent l’utilisation de Visual Studio 2015, même si elles sont similaires dans les versions antérieures de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a43c6-124">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="a43c6-125">Démarrez Visual Studio, puis, dans l’écran **Accueil**, sélectionnez **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="a43c6-125">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="a43c6-126">Dans le menu contextuel, sélectionnez **Windows 8** -> **Windows Phone** -> **Application vide (Silverlight Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="a43c6-126">In the pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="a43c6-127">Dans les champs **Nom** et **Nom de la solution**, indiquez les nom et nom de solution de l’application, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a43c6-127">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="a43c6-128">Vous pouvez choisir de cibler **Windows Phone 8.0** ou **Windows Phone 8.1**.</span><span class="sxs-lookup"><span data-stu-id="a43c6-128">You can choose to target either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="a43c6-129">Vous avez maintenant créé une nouvelle application Windows Phone Silverlight dans laquelle nous allons intégrer le Kit de développement logiciel Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a43c6-129">You have now created a new Windows Phone Silverlight app into which we will integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="a43c6-130">Connexion de votre application au serveur principal Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a43c6-130">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="a43c6-131">Installez le package NuGet [MicrosoftAzure.MobileEngagement] dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="a43c6-131">Install the [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="a43c6-132">Ouvrez `WMAppManifest.xml` (dans le dossier Propriétés) et assurez-vous que les éléments suivants sont déclarés (dans le cas contraire, ajoutez-les) dans la balise `<Capabilities />`  :</span><span class="sxs-lookup"><span data-stu-id="a43c6-132">Open `WMAppManifest.xml` (under the Properties folder) and make sure the following are declared (add them if they are not) in the `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="a43c6-133">Collez maintenant la chaîne de connexion que vous avez copiée précédemment pour votre application Mobile Engagement dans le fichier `Resources\EngagementConfiguration.xml`, entre les balises `<connectionString>` et `</connectionString>` :</span><span class="sxs-lookup"><span data-stu-id="a43c6-133">Now paste the connection string that you copied earlier for your Mobile Engagement app and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="a43c6-134">Dans le fichier `App.xaml.cs` :</span><span class="sxs-lookup"><span data-stu-id="a43c6-134">In the `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="a43c6-135">a.</span><span class="sxs-lookup"><span data-stu-id="a43c6-135">a.</span></span> <span data-ttu-id="a43c6-136">Ajoutez l'instruction `using` :</span><span class="sxs-lookup"><span data-stu-id="a43c6-136">Add the `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="a43c6-137">b.</span><span class="sxs-lookup"><span data-stu-id="a43c6-137">b.</span></span> <span data-ttu-id="a43c6-138">Initialisez le Kit de développement logiciel (SDK) dans la méthode `Application_Launching` :</span><span class="sxs-lookup"><span data-stu-id="a43c6-138">Initialize the SDK in the `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="a43c6-139">c.</span><span class="sxs-lookup"><span data-stu-id="a43c6-139">c.</span></span> <span data-ttu-id="a43c6-140">Insérez les instructions suivantes dans le code `Application_Activated` :</span><span class="sxs-lookup"><span data-stu-id="a43c6-140">Insert the following in the `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="a43c6-141"><a id="monitor"></a>Activation de l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="a43c6-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="a43c6-142">Pour commencer à envoyer des données et vous assurer que les utilisateurs sont actifs, vous devez envoyer au moins un écran (activité) au serveur principal Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a43c6-142">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="a43c6-143">Dans le fichier MainPage.xaml.cs, ajoutez l’instruction `using` :</span><span class="sxs-lookup"><span data-stu-id="a43c6-143">In the MainPage.xaml.cs, add the `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="a43c6-144">Remplacez la classe de base de **MainPage**, qui se trouve devant **PhoneApplicationPage**, par **EngagementPage**.</span><span class="sxs-lookup"><span data-stu-id="a43c6-144">Replace the base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="a43c6-145">Dans votre fichier `MainPage.xml` :</span><span class="sxs-lookup"><span data-stu-id="a43c6-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="a43c6-146">a.</span><span class="sxs-lookup"><span data-stu-id="a43c6-146">a.</span></span> <span data-ttu-id="a43c6-147">Ajoutez une déclaration d'espace de noms :</span><span class="sxs-lookup"><span data-stu-id="a43c6-147">Add to your namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="a43c6-148">b.</span><span class="sxs-lookup"><span data-stu-id="a43c6-148">b.</span></span> <span data-ttu-id="a43c6-149">Remplacez `phone:PhoneApplicationPage` dans le nom de la balise XML par `engagement:EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="a43c6-149">Replace `phone:PhoneApplicationPage` in the XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="a43c6-150"><a id="monitor"></a>Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="a43c6-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="a43c6-151"><a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app</span><span class="sxs-lookup"><span data-stu-id="a43c6-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="a43c6-152">Mobile Engagement vous permet d'interagir et d'atteindre vos utilisateurs à l'aide de notifications push et de la messagerie dans l'application, dans le cadre d'une campagne.</span><span class="sxs-lookup"><span data-stu-id="a43c6-152">Mobile Engagement allows you to interact and reach your users with Push Notifications and in-app Messaging in the context of campaigns.</span></span> <span data-ttu-id="a43c6-153">Ce module s'appelle Couverture dans le portail Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a43c6-153">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="a43c6-154">Les sections suivantes vous permettent de configurer votre application pour la réception.</span><span class="sxs-lookup"><span data-stu-id="a43c6-154">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-mpns-push-notifications"></a><span data-ttu-id="a43c6-155">Permettre à votre application de recevoir les notifications push MPNS</span><span class="sxs-lookup"><span data-stu-id="a43c6-155">Enable your app to receive MPNS Push Notifications</span></span>
<span data-ttu-id="a43c6-156">Ajoutez de nouvelles capacités à votre fichier `WMAppManifest.xml` :</span><span class="sxs-lookup"><span data-stu-id="a43c6-156">Add new Capabilities to your `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="a43c6-157">Initialiser le SDK du module Couverture</span><span class="sxs-lookup"><span data-stu-id="a43c6-157">Initialize the REACH SDK</span></span>
1. <span data-ttu-id="a43c6-158">Dans `App.xaml.cs`, appelez `EngagementReach.Instance.Init();` dans la fonction **Application_Launching**, juste après l’initialisation de l’agent :</span><span class="sxs-lookup"><span data-stu-id="a43c6-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in the **Application_Launching** function, right after the agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="a43c6-159">Dans `App.xaml.cs`, appelez `EngagementReach.Instance.OnActivated(e);` dans la fonction **Application_Activated**, juste après l’initialisation de l’agent :</span><span class="sxs-lookup"><span data-stu-id="a43c6-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in the **Application_Activated** function, right after the agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="a43c6-160">Vous êtes prêt.</span><span class="sxs-lookup"><span data-stu-id="a43c6-160">You're all set.</span></span> <span data-ttu-id="a43c6-161">Nous allons maintenant vérifier que vous avez correctement effectué cette intégration de base.</span><span class="sxs-lookup"><span data-stu-id="a43c6-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="a43c6-162"><a id="send"></a>Envoi d’une notification vers votre application</span><span class="sxs-lookup"><span data-stu-id="a43c6-162"><a id="send"></a>Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="a43c6-163">Vous devez maintenant voir une notification sur votre appareil, s’affichant en tant que notification d’application si l’application est ouverte, ou sinon en tant que notification toast comme suit :</span><span class="sxs-lookup"><span data-stu-id="a43c6-163">You should now see a notification on your device which will show up as an in-app notification if the app is open otherwise as a toast notification like the following:</span></span> 

![][6]

<!-- URLs. -->
<span data-ttu-id="a43c6-164">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664</span><span class="sxs-lookup"><span data-stu-id="a43c6-164">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664</span></span>
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
