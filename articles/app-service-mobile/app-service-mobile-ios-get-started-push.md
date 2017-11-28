---
title: aaaAdd des Notifications Push tooiOS application avec les applications mobiles Azure
description: "Découvrez comment toouse Azure Mobile Apps toosend push notifications tooyour iOS application."
services: app-service\mobile
documentationcenter: ios
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: fa503833-d23e-4925-8d93-341bb3fbab7d
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/10/2016
ms.author: glenga
ms.openlocfilehash: 11588c56bc8987a71257dbad4fcdebf1b3209b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="3fce0-103">Ajouter des Notifications Push tooyour les applications iOS</span><span class="sxs-lookup"><span data-stu-id="3fce0-103">Add Push Notifications tooyour iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="3fce0-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3fce0-104">Overview</span></span>
<span data-ttu-id="3fce0-105">Dans ce didacticiel, vous allez ajouter toohello de notifications push [iOS rapides Démarrer] projet afin qu’une notification push est envoyée toohello périphérique chaque fois qu’un enregistrement est inséré.</span><span class="sxs-lookup"><span data-stu-id="3fce0-105">In this tutorial, you add push notifications toohello [iOS quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="3fce0-106">Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez serez hello package d’extension de notification push.</span><span class="sxs-lookup"><span data-stu-id="3fce0-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="3fce0-107">Consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="3fce0-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="3fce0-108">Hello [simulateur iOS ne prend pas en charge des notifications push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="3fce0-108">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="3fce0-109">Vous avez besoin d’un appareil iOS physique et d’une [appartenance au programme pour développeurs Apple](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="3fce0-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="3fce0-110"><a name="configure-hub"></a>Configurer un hub de notification</span><span class="sxs-lookup"><span data-stu-id="3fce0-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="3fce0-111"><a id="register"></a>Inscrire une application pour les notifications Push</span><span class="sxs-lookup"><span data-stu-id="3fce0-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="3fce0-112">Configurer des notifications push de toosend Azure</span><span class="sxs-lookup"><span data-stu-id="3fce0-112">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="3fce0-113"><a id="update-server"></a>Mettre à jour des notifications push de toosend principal</span><span class="sxs-lookup"><span data-stu-id="3fce0-113"><a id="update-server"></a>Update backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="3fce0-114"><a id="add-push"></a>Ajouter tooapp de notifications push</span><span class="sxs-lookup"><span data-stu-id="3fce0-114"><a id="add-push"></a>Add push notifications tooapp</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="3fce0-115"><a id="test"></a>Tester les notifications Push</span><span class="sxs-lookup"><span data-stu-id="3fce0-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="3fce0-116"><a id="more"></a>En savoir plus</span><span class="sxs-lookup"><span data-stu-id="3fce0-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="3fce0-117">Les modèles vous permettent de push de flexibilité toosend inter-plateformes et push localisée.</span><span class="sxs-lookup"><span data-stu-id="3fce0-117">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="3fce0-118">[Comment tooUse iOS bibliothèque cliente pour les applications mobiles Azure](app-service-mobile-ios-how-to-use-client-library.md#templates) vous montre comment les modèles tooregister.</span><span class="sxs-lookup"><span data-stu-id="3fce0-118">[How tooUse iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how tooregister templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[iOS rapides Démarrer]: app-service-mobile-ios-get-started.md
