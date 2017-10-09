---
title: application aaaAdd push notifications tooyour Xamarin.iOS avec Azure App Service
description: "Découvrez comment toouse Azure App Service toosend push notifications tooyour Xamarin.iOS application"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a><span data-ttu-id="a91a3-103">Ajouter des notifications de push tooyour application Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="a91a3-103">Add push notifications tooyour Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="a91a3-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a91a3-104">Overview</span></span>
<span data-ttu-id="a91a3-105">Dans ce didacticiel, vous allez ajouter toohello de notifications push [Xamarin.iOS de démarrage rapide](app-service-mobile-xamarin-ios-get-started.md) projet afin qu’une notification push est envoyée toohello périphérique chaque fois qu’un enregistrement est inséré.</span><span class="sxs-lookup"><span data-stu-id="a91a3-105">In this tutorial, you add push notifications toohello [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="a91a3-106">Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez serez hello package d’extension de notification push.</span><span class="sxs-lookup"><span data-stu-id="a91a3-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="a91a3-107">Consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a91a3-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a91a3-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a91a3-108">Prerequisites</span></span>
* <span data-ttu-id="a91a3-109">Hello complète [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a91a3-109">Complete hello [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="a91a3-110">Un appareil iOS physique.</span><span class="sxs-lookup"><span data-stu-id="a91a3-110">A physical iOS device.</span></span> <span data-ttu-id="a91a3-111">Notifications push ne sont pas pris en charge par le simulateur iOS de hello.</span><span class="sxs-lookup"><span data-stu-id="a91a3-111">Push notifications are not supported by hello iOS simulator.</span></span>

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="a91a3-112">Inscrire l’application hello pour les notifications push sur le portail des développeurs d’Apple</span><span class="sxs-lookup"><span data-stu-id="a91a3-112">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a><span data-ttu-id="a91a3-113">Configurer les notifications de push de l’application Mobile toosend</span><span class="sxs-lookup"><span data-stu-id="a91a3-113">Configure your Mobile App toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="a91a3-114">Mettre à jour des notifications push de hello serveur projet toosend</span><span class="sxs-lookup"><span data-stu-id="a91a3-114">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="a91a3-115">Configurer votre projet Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="a91a3-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="a91a3-116">Ajouter une application de tooyour de notifications push</span><span class="sxs-lookup"><span data-stu-id="a91a3-116">Add push notifications tooyour app</span></span>
1. <span data-ttu-id="a91a3-117">Dans **QSTodoService**, ajouter hello suivant propriété afin que **AppDelegate** peut acquérir les clients mobiles hello :</span><span class="sxs-lookup"><span data-stu-id="a91a3-117">In **QSTodoService**, add hello following property so that **AppDelegate** can acquire hello mobile client:</span></span>
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. <span data-ttu-id="a91a3-118">Ajoutez hello suivant `using` haut de toohello d’instruction de hello **AppDelegate.cs** fichier.</span><span class="sxs-lookup"><span data-stu-id="a91a3-118">Add hello following `using` statement toohello top of hello **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="a91a3-119">Dans **AppDelegate**, substituez hello **FinishedLaunching** événement :</span><span class="sxs-lookup"><span data-stu-id="a91a3-119">In **AppDelegate**, override hello **FinishedLaunching** event:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. <span data-ttu-id="a91a3-120">Dans hello du même fichier, remplacer hello **RegisteredForRemoteNotifications** événement.</span><span class="sxs-lookup"><span data-stu-id="a91a3-120">In hello same file, override hello **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="a91a3-121">Dans ce code, vous vous inscrivez pour une notification de modèle simple qui est envoyée sur toutes les plateformes prises en charge par le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="a91a3-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by hello server.</span></span>
   
    <span data-ttu-id="a91a3-122">Pour plus d’informations sur les modèles avec Notification Hubs, consultez [Modèles](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="a91a3-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. <span data-ttu-id="a91a3-123">Substituez ensuite hello **DidReceivedRemoteNotification** événement :</span><span class="sxs-lookup"><span data-stu-id="a91a3-123">Then, override hello **DidReceivedRemoteNotification** event:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

<span data-ttu-id="a91a3-124">Votre application est maintenant des notifications push de toosupport mis à jour.</span><span class="sxs-lookup"><span data-stu-id="a91a3-124">Your app is now updated toosupport push notifications.</span></span>

## <span data-ttu-id="a91a3-125"><a name="test"></a>Tester les notifications push dans votre application</span><span class="sxs-lookup"><span data-stu-id="a91a3-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="a91a3-126">Hello de presse **exécuter** projet de hello toobuild et démarrer l’application hello dans un appareil iOS, puis cliquez sur **OK** tooaccept les notifications push.</span><span class="sxs-lookup"><span data-stu-id="a91a3-126">Press hello **Run** button toobuild hello project and start hello app in an iOS capable device, then click **OK** tooaccept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a91a3-127">Vous devez accepter explicitement les notifications Push de votre application.</span><span class="sxs-lookup"><span data-stu-id="a91a3-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="a91a3-128">Cette demande produit uniquement hello première fois que hello application s’exécute.</span><span class="sxs-lookup"><span data-stu-id="a91a3-128">This request only occurs hello first time that hello app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="a91a3-129">Dans l’application hello, une tâche, puis tapez Bonjour signe plu (**+**) icône.</span><span class="sxs-lookup"><span data-stu-id="a91a3-129">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
3. <span data-ttu-id="a91a3-130">Vérifiez qu’une notification est reçue, puis cliquez sur **OK** toodismiss hello notification.</span><span class="sxs-lookup"><span data-stu-id="a91a3-130">Verify that a notification is received, then click **OK** toodismiss hello notification.</span></span>
4. <span data-ttu-id="a91a3-131">Répétez l’étape 2 et fermer immédiatement hello app, puis vérifiez qu’une notification s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a91a3-131">Repeat step 2 and immediately close hello app, then verify that a notification is shown.</span></span>

<span data-ttu-id="a91a3-132">Vous avez terminé ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a91a3-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



