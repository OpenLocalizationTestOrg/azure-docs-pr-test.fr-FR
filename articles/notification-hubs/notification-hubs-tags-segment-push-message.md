---
title: aaaRouting et les Expressions de balise
description: Cette rubrique explique les expressions de balise et de routage pour Azure Notification Hubs.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 0fffb3bb-8ed8-4e0f-89e8-0de24a47f644
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c2c60500f7469f1cb1a73a5cf63c221a9ad6cbb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="routing-and-tag-expressions"></a>Routage et expressions de balise
## <a name="overview"></a>Vue d'ensemble
Les expressions de balises permettent de tootarget des ensembles spécifiques d’appareils ou plus particulièrement d’inscriptions, lors de l’envoi d’une notification push via des concentrateurs de Notification.

## <a name="targeting-specific-registrations"></a>Ciblage d'inscriptions spécifiques
Hello uniquement moyen tootarget notification spécifique des enregistrements est balises tooassociate avec eux, puis cibler ces balises. Comme indiqué dans [gestion de l’inscription](notification-hubs-push-notification-registration-management.md), de push de tooreceive d’ordre notifications d’une application a tooregister un appareil gérer sur un concentrateur de notification. Une fois qu’un enregistrement est créé sur un concentrateur de notification, hello principale peut envoyer tooit de notifications push.
principal d’application Hello peut choisir tootarget d’inscriptions hello avec une notification spécifique Bonjour suivant façons :

1. **Diffusion**: tous les enregistrements dans le hub de notification hello recevoir une notification de hello.
2. **Balise**: tous les enregistrements qui contiennent des hello spécifié balise recevoir une notification de hello.
3. **Expression de balise**: toutes les inscriptions dont l’ensemble de balises correspondance hello expression spécifiée reçoivent notification de hello.

## <a name="tags"></a>Tags
Une balise peut être n’importe quelle chaîne, des too120, contenant des caractères alphanumériques et hello les caractères non alphanumériques suivants : '_', ' @', '#', '. ',' :', '-'. Hello suivant montre une application à partir de laquelle vous pouvez recevoir des notifications toast concernant des groupes musicaux spécifiques. Dans ce scénario, une notification de tooroute moyen simple est inscriptions toolabel avec balises qui représentent des bandes différentes hello, comme dans hello illustration suivante.

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

Dans cette illustration, le message de type hello marquées **Beatles** atteint uniquement hello tablette enregistrée avec la balise de hello **Beatles**.

Pour plus d'informations sur la création d’inscriptions pour des balises, consultez [Gestion des inscriptions](notification-hubs-push-notification-registration-management.md).

Vous pouvez envoyer des tootags des notifications à l’aide de hello d’envoi des méthodes de notifications de hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` classe Bonjour [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) Kit de développement logiciel. Vous pouvez également utiliser Node.js ou hello API REST de Notifications Push.  Voici un exemple d’utilisation hello SDK.

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




Balises n’ont pas de toobe pré-configurés et peuvent faire référence les concepts de toomultiple spécifique à l’application. Par exemple, les utilisateurs de cet exemple d’application peuvent commenter les bandes et souhaitez tooreceive toasts, non seulement pour les commentaires de hello sur leurs groupes favoris, mais aussi pour tous les commentaires de leurs amis, quel que soit la bande hello sur lequel ils entrent des commentaires. Hello illustration suivante montre un exemple de ce scénario :

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

Dans cette image, Alice s’intéresse aux mises à jour pour hello Beatles, et Bob s’intéresse aux mises à jour pour hello aux Wailers. Bob est également intéressée par commentaires de Charlie, et Charlie s’intéresse aux Wailers de hello. Lorsqu’une notification est envoyée pour le commentaire de Charlie sur hello Beatles, Alice et Bob reçoit.

Même s’il est possible d’encoder plusieurs paramètres (par exemple, « band_Beatles » ou « follows_Charlie »), les balises sont des chaînes simples et non des propriétés avec des valeurs. Un enregistrement est mis en correspondance uniquement sur la présence de hello ou l’absence d’une balise spécifique.

Pour obtenir un didacticiel complet et détaillé sur comment toouse les balises pour l’envoi de groupes de toointerest, consultez [dernières nouvelles](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).

## <a name="using-tags-tootarget-users"></a>À l’aide de balises tootarget utilisateurs
Une autre façon toouse balises est tooidentify tous les appareils hello d’un utilisateur particulier. Les enregistrements peuvent être identifiés avec une balise qui contient un id d’utilisateur, comme dans hello illustration suivante :

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

Dans cette image, UID : Alice de message marquée hello atteint tous les enregistrements marqués UID : Alice ; Par conséquent, tous les appareils d’Alice.

## <a name="tag-expressions"></a>Expressions de balise
Il existe des cas dans lesquels une notification a tootarget un jeu d’enregistrements identifié pas par une balise unique, mais par une expression booléenne sur les balises.

Considérez une application de sports qui envoie un rappel tooeveryone à Boston concernant un match entre hello Red Sox et les Cardinals. Si hello client application inscrit des balises sur l’intérêt dans les équipes et l’emplacement, puis hello notification doit être ciblée tooeveryone à Boston qui souhaitent hello Red Sox ou de hello Cardinals. Cette condition peut être exprimée par hello expression booléenne suivante :

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

Les expressions de balise peuvent contenir tous les opérateurs booléens, notamment AND (&&), OR (||) et NOT (!). Elles peuvent également contenir des parenthèses. Expressions de balises sont limitées too20 balises si elles contiennent uniquement des opérateurs OR ; Sinon, elles sont limitées too6 balises.

Voici un exemple pour envoyer des notifications avec des expressions de balise à l’aide du Kit de développement logiciel de hello.

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
