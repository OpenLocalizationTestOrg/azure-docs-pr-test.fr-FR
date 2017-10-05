---
title: "Ajouter des notifications Push à votre application iOS à l'aide d'Azure Mobile Apps"
description: "Découvrez comment utiliser Azure Mobile Apps pour envoyer des notifications Push à votre application iOS."
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
ms.openlocfilehash: 08a8c35b89386bd0dbe7bba406a6985a5a0d7eb8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="63c41-103">Ajout de notifications Push à votre application iOS</span><span class="sxs-lookup"><span data-stu-id="63c41-103">Add Push Notifications to your iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="63c41-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="63c41-104">Overview</span></span>
<span data-ttu-id="63c41-105">Dans ce didacticiel, vous ajoutez des notifications Push au projet [Démarrage rapide iOS] afin qu'une notification Push soit envoyée chaque fois qu'un enregistrement est inséré.</span><span class="sxs-lookup"><span data-stu-id="63c41-105">In this tutorial, you add push notifications to the [iOS quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="63c41-106">Si vous n’utilisez pas le projet de serveur du démarrage rapide téléchargé, vous devrez ajouter le package d’extension de notification Push.</span><span class="sxs-lookup"><span data-stu-id="63c41-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="63c41-107">Consultez [Fonctionnement avec le Kit de développement logiciel (SDK) du serveur principal .NET pour Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="63c41-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="63c41-108">Les [notifications Push ne sont pas prises en charge par le simulateur iOS](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="63c41-108">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="63c41-109">Vous avez besoin d’un appareil iOS physique et d’une [appartenance au programme pour développeurs Apple](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="63c41-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="63c41-110"><a name="configure-hub"></a>Configurer un hub de notification</span><span class="sxs-lookup"><span data-stu-id="63c41-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="63c41-111"><a id="register"></a>Inscrire une application pour les notifications Push</span><span class="sxs-lookup"><span data-stu-id="63c41-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="63c41-112">Configurer Azure pour l’envoi de notifications Push</span><span class="sxs-lookup"><span data-stu-id="63c41-112">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="63c41-113"><a id="update-server"></a>Mettre à jour le serveur principal pour l'envoi de notifications push</span><span class="sxs-lookup"><span data-stu-id="63c41-113"><a id="update-server"></a>Update backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="63c41-114"><a id="add-push"></a>Ajouter des notifications Push à l’application</span><span class="sxs-lookup"><span data-stu-id="63c41-114"><a id="add-push"></a>Add push notifications to app</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="63c41-115"><a id="test"></a>Tester les notifications Push</span><span class="sxs-lookup"><span data-stu-id="63c41-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="63c41-116"><a id="more"></a>En savoir plus</span><span class="sxs-lookup"><span data-stu-id="63c41-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="63c41-117">Les modèles vous apportent la souplesse nécessaire pour envoyer des notifications push multiplateformes et localisées.</span><span class="sxs-lookup"><span data-stu-id="63c41-117">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="63c41-118">[Utilisation de la bibliothèque cliente iOS pour Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) vous montre comment enregistrer des modèles.</span><span class="sxs-lookup"><span data-stu-id="63c41-118">[How to Use iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how to register templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="63c41-119">[Démarrage rapide iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="63c41-119">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>
