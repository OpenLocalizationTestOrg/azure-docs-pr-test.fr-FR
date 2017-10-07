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
# <a name="add-push-notifications-tooyour-ios-app"></a>Ajouter des Notifications Push tooyour les applications iOS
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Vue d'ensemble
Dans ce didacticiel, vous allez ajouter toohello de notifications push [iOS rapides Démarrer] projet afin qu’une notification push est envoyée toohello périphérique chaque fois qu’un enregistrement est inséré.

Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez serez hello package d’extension de notification push. Consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour plus d’informations.

Hello [simulateur iOS ne prend pas en charge des notifications push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html). Vous avez besoin d’un appareil iOS physique et d’une [appartenance au programme pour développeurs Apple](https://developer.apple.com/programs/ios/).

## <a name="configure-hub"></a>Configurer un hub de notification
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Inscrire une application pour les notifications Push
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-toosend-push-notifications"></a>Configurer des notifications push de toosend Azure
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a id="update-server"></a>Mettre à jour des notifications push de toosend principal
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <a id="add-push"></a>Ajouter tooapp de notifications push
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <a id="test"></a>Tester les notifications Push
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <a id="more"></a>En savoir plus
* Les modèles vous permettent de push de flexibilité toosend inter-plateformes et push localisée. [Comment tooUse iOS bibliothèque cliente pour les applications mobiles Azure](app-service-mobile-ios-how-to-use-client-library.md#templates) vous montre comment les modèles tooregister.

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[iOS rapides Démarrer]: app-service-mobile-ios-get-started.md
