---
title: "aaaGet main d’Azure Mobile Engagement pour Xamarin.iOS"
description: "Découvrez comment toouse Azure Mobile Engagement avec Analytique et les Notifications Push pour les applications de Xamarin.iOS."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a><span data-ttu-id="66c18-103">Prise en main d’Azure Mobile Engagement pour les applications Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="66c18-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="66c18-104">Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et l’envoi push notifications toosegmented les utilisateurs dans une application Xamarin.iOS.</span><span class="sxs-lookup"><span data-stu-id="66c18-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users in a Xamarin.iOS application.</span></span>
<span data-ttu-id="66c18-105">Dans ce didacticiel, vous allez créer une application Xamarin.iOS vide qui collecte des données de base et reçoit des notifications Push à l’aide du service APN (Apple Push Notification).</span><span class="sxs-lookup"><span data-stu-id="66c18-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

> [!NOTE]
> <span data-ttu-id="66c18-106">Hello Azure Mobile Engagement service mars 2018 est retirée et est actuellement que les clients tooexisting disponibles.</span><span class="sxs-lookup"><span data-stu-id="66c18-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="66c18-107">Pour plus d’informations, consultez [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="66c18-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="66c18-108">Ce didacticiel requiert hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="66c18-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="66c18-109">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="66c18-109">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="66c18-110">Vous pouvez également utiliser Visual Studio avec Xamarin, mais ce didacticiel utilise Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="66c18-110">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="66c18-111">Pour obtenir des instructions sur l’installation, consultez la page [Configuration et installation pour Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="66c18-111">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span> 
* [<span data-ttu-id="66c18-112">Kit de développement logiciel (SDK) Mobile Engagement pour Xamarin</span><span class="sxs-lookup"><span data-stu-id="66c18-112">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="66c18-113">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="66c18-113">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="66c18-114">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="66c18-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="66c18-115">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="66c18-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="66c18-116"><a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application iOS</span><span class="sxs-lookup"><span data-stu-id="66c18-116"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="66c18-117"><a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="66c18-117"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="66c18-118">Ce didacticiel présente une « intégration de base « hello minimale définie les données de toocollect requis et envoyer une notification push.</span><span class="sxs-lookup"><span data-stu-id="66c18-118">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span>

<span data-ttu-id="66c18-119">Nous allons créer une application de base avec l’intégration de hello toodemonstrate Xamarin :</span><span class="sxs-lookup"><span data-stu-id="66c18-119">We will create a basic app with Xamarin toodemonstrate hello integration:</span></span>

### <a name="create-a-new-xamarinios-project"></a><span data-ttu-id="66c18-120">Créer un projet Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="66c18-120">Create a new Xamarin.iOS project</span></span>
1. <span data-ttu-id="66c18-121">Démarrez Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="66c18-121">Launch Xamarin Studio.</span></span> <span data-ttu-id="66c18-122">Accédez trop**fichier** -> **nouveau** -> **Solution**</span><span class="sxs-lookup"><span data-stu-id="66c18-122">Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="66c18-123">Sélectionnez **application vue unique**, assurez-vous que la langue hello sélectionné est **c#** puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="66c18-123">Select **Single View App**, make sure hello selected language is **C#** and then click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="66c18-124">Renseignez hello **nom de l’application** et hello **identifiant d’organisation** puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="66c18-124">Fill in hello **App Name** and hello **Organization Identifier** and then click **Next**.</span></span> 
   
    ![][3]
   
   > [!IMPORTANT]
   > <span data-ttu-id="66c18-125">Vérifiez que hello publication que vous utilisez finalement toodeploy que votre application iOS utilise un ID d’application qui correspond à exactement avec hello identificateur de lot que vous avez ici.</span><span class="sxs-lookup"><span data-stu-id="66c18-125">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using an App ID which matches exactly with hello Bundle Identifier you have here.</span></span> 
   > 
   > 
4. <span data-ttu-id="66c18-126">Hello de mise à jour **nom du projet**, **nom de la Solution** et **emplacement** si nécessaire et cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="66c18-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="66c18-127">Xamarin Studio créera une application de démonstration hello dans lequel nous intégrera Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="66c18-127">Xamarin Studio will create hello demo app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="66c18-128">Se connecter à votre serveur principal d’application tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="66c18-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="66c18-129">Cliquez avec le bouton droit sur hello **Packages** dossier dans windows de Solution hello et sélectionnez **ajouter des Packages en cours...**</span><span class="sxs-lookup"><span data-stu-id="66c18-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="66c18-130">Recherchez hello **Microsoft Azure Mobile Engagement Xamarin SDK** et ajoutez-le tooyour solution.</span><span class="sxs-lookup"><span data-stu-id="66c18-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="66c18-131">Ouvrez **AppDelegate.cs** et ajoutez hello qui suit à l’aide d’instruction :</span><span class="sxs-lookup"><span data-stu-id="66c18-131">Open **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
4. <span data-ttu-id="66c18-132">Bonjour **FinishedLaunching** (méthode), ajouter hello après la connexion de hello tooinitialize avec le serveur principal Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="66c18-132">In hello **FinishedLaunching** method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="66c18-133">Assurez-vous que tooadd votre **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="66c18-133">Make sure tooadd your **ConnectionString**.</span></span> <span data-ttu-id="66c18-134">Ce code utilise également un fantôme **NotificationIcon** qui est ajouté par hello Mobile Engagement Kit de développement logiciel que vous pouvez tooreplace.</span><span class="sxs-lookup"><span data-stu-id="66c18-134">This code also uses a dummy **NotificationIcon** which is added by hello Mobile Engagement SDK which you may want tooreplace.</span></span> 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <span data-ttu-id="66c18-135"><a id="monitor"></a>Activation de la surveillance en temps réel</span><span class="sxs-lookup"><span data-stu-id="66c18-135"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="66c18-136">Dans l’ordre toostart envoi de données et en garantissant hello utilisateurs sont actifs, vous devez envoyer au moins un écran toohello Mobile Engagement principal.</span><span class="sxs-lookup"><span data-stu-id="66c18-136">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="66c18-137">Ouvrez **ViewController.cs** et ajoutez hello qui suit à l’aide d’instruction :</span><span class="sxs-lookup"><span data-stu-id="66c18-137">Open **ViewController.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
2. <span data-ttu-id="66c18-138">Remplacez la classe hello à partir de laquelle `ViewController` hérite `UIViewController` trop`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="66c18-138">Replace hello class from which `ViewController` inherits from `UIViewController` too`EngagementViewController`.</span></span> 

## <span data-ttu-id="66c18-139"><a id="monitor"></a>Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="66c18-139"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="66c18-140"><a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app</span><span class="sxs-lookup"><span data-stu-id="66c18-140"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="66c18-141">Mobile Engagement vous permet de toointeract avec vos utilisateurs et portée avec des notifications push et les messages dans le contexte de hello de campagnes dans l’application.</span><span class="sxs-lookup"><span data-stu-id="66c18-141">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="66c18-142">Ce module est appelé portée dans le portail Mobile Engagement de hello.</span><span class="sxs-lookup"><span data-stu-id="66c18-142">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="66c18-143">Hello sections suivantes configurer votre application tooreceive les.</span><span class="sxs-lookup"><span data-stu-id="66c18-143">hello following sections set up your app tooreceive them.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="66c18-144">Modifier votre délégué d'Application</span><span class="sxs-lookup"><span data-stu-id="66c18-144">Modify your Application Delegate</span></span>
1. <span data-ttu-id="66c18-145">Ouvrez hello **AppDelegate.cs** et ajoutez hello qui suit à l’aide d’instruction :</span><span class="sxs-lookup"><span data-stu-id="66c18-145">Open hello **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using System; 
2. <span data-ttu-id="66c18-146">Maintenant, à l’intérieur hello `FinishedLaunching` (méthode), ajouter hello suivant tooregister pour les messages envoyés après`EngagementAgent.init(...)`</span><span class="sxs-lookup"><span data-stu-id="66c18-146">Now inside hello `FinishedLaunching` method, add hello following tooregister for push messages after `EngagementAgent.init(...)`</span></span>
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. <span data-ttu-id="66c18-147">Enfin - mettre à jour ou ajouter hello méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="66c18-147">Finally - update or add hello following methods:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. <span data-ttu-id="66c18-148">Dans votre **Info.plist** de fichiers dans la solution de hello, vérifiez que hello **identificateur de lot** correspond au hello **ID d’application** vous avez dans votre profil de configuration Bonjour Apple Dev Centre.</span><span class="sxs-lookup"><span data-stu-id="66c18-148">In your **Info.plist** file in hello solution, confirm that hello **Bundle Identifier** matches with hello **App ID** you have in your provisioning profile in hello Apple Dev Center.</span></span> 
   
    ![][7]
5. <span data-ttu-id="66c18-149">Dans hello même **Info.plist** de fichiers, assurez-vous que vous avez vérifié hello **activer les Modes d’arrière-plan** et **des Notifications à distance**.</span><span class="sxs-lookup"><span data-stu-id="66c18-149">In hello same **Info.plist** file, make sure that you have checked hello **Enable Background Modes** and **Remote Notifications**.</span></span> 
   
     ![][8]
6. <span data-ttu-id="66c18-150">Exécutez l’application hello sur périphérique hello que vous avez associé à ce profil de publication.</span><span class="sxs-lookup"><span data-stu-id="66c18-150">Run hello app on hello device you have associated with this publishing profile.</span></span> 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
