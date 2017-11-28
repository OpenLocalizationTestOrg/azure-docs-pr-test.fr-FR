---
title: Routage et expressions de balise
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
ms.openlocfilehash: 18faa88641623e1248d6a33bc2d87099e1c9f624
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="70651-103">Routage et expressions de balise</span><span class="sxs-lookup"><span data-stu-id="70651-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="70651-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="70651-104">Overview</span></span>
<span data-ttu-id="70651-105">Les expressions de balise vous permettent de cibler des ensembles spécifiques d'appareils, ou plus précisément d'inscriptions, lors de l'envoi d'une notification push via Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="70651-105">Tag expressions enable you to target specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="70651-106">Ciblage d'inscriptions spécifiques</span><span class="sxs-lookup"><span data-stu-id="70651-106">Targeting specific registrations</span></span>
<span data-ttu-id="70651-107">La seule façon de cibler des inscriptions de notification spécifiques consiste à les associer à des balises, puis à cibler ces balises.</span><span class="sxs-lookup"><span data-stu-id="70651-107">The only way to target specific notification registrations is to associate tags with them, then target those tags.</span></span> <span data-ttu-id="70651-108">Comme indiqué dans la rubrique [Gestion des inscriptions](notification-hubs-push-notification-registration-management.md), pour recevoir des notifications push, une application doit inscrire un appareil sur un concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="70651-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order to receive push notifications an app has to register a device handle on a notification hub.</span></span> <span data-ttu-id="70651-109">Lorsqu’une inscription est créée sur un concentrateur de notification, le serveur principal d'application peut envoyer des notifications push.</span><span class="sxs-lookup"><span data-stu-id="70651-109">Once a registration is created on a notification hub, the application backend can send push notifications to it.</span></span>
<span data-ttu-id="70651-110">Le serveur principal d'application peut choisir les inscriptions à cibler avec une notification spécifique en procédant ainsi :</span><span class="sxs-lookup"><span data-stu-id="70651-110">The application backend can choose the registrations to target with a specific notification in the following ways:</span></span>

1. <span data-ttu-id="70651-111">**Diffusion**: toutes les inscriptions dans le concentrateur de notification reçoivent la notification.</span><span class="sxs-lookup"><span data-stu-id="70651-111">**Broadcast**: all registrations in the notification hub receive the notification.</span></span>
2. <span data-ttu-id="70651-112">**Balise**: toutes les inscriptions qui contiennent la balise spécifiée reçoivent la notification.</span><span class="sxs-lookup"><span data-stu-id="70651-112">**Tag**: all registrations that contain the specified tag receive the notification.</span></span>
3. <span data-ttu-id="70651-113">**Expression de balise**: toutes les inscriptions dont le jeu de balises correspond à l'expression spécifiée reçoivent la notification.</span><span class="sxs-lookup"><span data-stu-id="70651-113">**Tag expression**: all registrations whose set of tags match the specified expression receive the notification.</span></span>

## <a name="tags"></a><span data-ttu-id="70651-114">Tags</span><span class="sxs-lookup"><span data-stu-id="70651-114">Tags</span></span>
<span data-ttu-id="70651-115">Une balise peut être n’importe quelle chaîne, jusqu'à 120 caractères alphanumériques et les caractères non alphanumériques suivants : '_', ' @', '#', '. ',' :', '-'.</span><span class="sxs-lookup"><span data-stu-id="70651-115">A tag can be any string, up to 120 characters, containing alphanumeric and the following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="70651-116">L'exemple suivant montre une application à partir de laquelle vous pouvez recevoir des notifications toast concernant des groupes musicaux spécifiques.</span><span class="sxs-lookup"><span data-stu-id="70651-116">The following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="70651-117">Dans ce scénario, une méthode simple pour acheminer des notifications consiste à étiqueter les inscriptions avec des balises représentant les différents groupes de musique, comme dans l'image suivante.</span><span class="sxs-lookup"><span data-stu-id="70651-117">In this scenario, a simple way to route notifications is to label registrations with tags that represent the different bands, as in the following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="70651-118">Dans cette illustration, le message étiqueté **Beatles** est uniquement envoyé à la tablette inscrite avec la balise **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="70651-118">In this picture, the message tagged **Beatles** reaches only the tablet that registered with the tag **Beatles**.</span></span>

<span data-ttu-id="70651-119">Pour plus d'informations sur la création d’inscriptions pour des balises, consultez [Gestion des inscriptions](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="70651-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="70651-120">Vous pouvez envoyer des notifications à des balises à l'aide des méthodes d’envoi de notifications de la classe `Microsoft.Azure.NotificationHubs.NotificationHubClient` dans le Kit de développement logiciel (SDK) [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) .</span><span class="sxs-lookup"><span data-stu-id="70651-120">You can send notifications to tags using the send notifications methods of the `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in the [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="70651-121">Vous pouvez également utiliser Node.js ou les API REST Notifications Push.</span><span class="sxs-lookup"><span data-stu-id="70651-121">You can also use Node.js, or the Push Notifications REST APIs.</span></span>  <span data-ttu-id="70651-122">Voici un exemple utilisant le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="70651-122">Here's an example using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="70651-123">Les balises n'ont pas besoin d'être provisionnées et peuvent référencer plusieurs concepts propres à l'application.</span><span class="sxs-lookup"><span data-stu-id="70651-123">Tags do not have to be pre-provisioned and can refer to multiple app-specific concepts.</span></span> <span data-ttu-id="70651-124">Par exemple, les utilisateurs de cet exemple d'application peuvent publier des commentaires sur les groupes et recevoir des notifications toast non seulement concernant les commentaires sur leurs groupes favoris, mais également pour tous les commentaires de leurs amis, quel que soit le groupe qu’ils commentent.</span><span class="sxs-lookup"><span data-stu-id="70651-124">For example, users of this example application can comment on bands and want to receive toasts, not only for the comments on their favorite bands, but also for all comments from their friends, regardless of the band on which they are commenting.</span></span> <span data-ttu-id="70651-125">L'illustration suivante montre un exemple de ce scénario :</span><span class="sxs-lookup"><span data-stu-id="70651-125">The following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="70651-126">Dans cette image, Alice s'intéresse à l’actualité des Beatles, et Bob à celle des Wailers.</span><span class="sxs-lookup"><span data-stu-id="70651-126">In this picture, Alice is interested in updates for the Beatles, and Bob is interested in updates for the Wailers.</span></span> <span data-ttu-id="70651-127">Bob est également intéressée par les commentaires de Charlie, et Charlie s'intéresse aux Wailers.</span><span class="sxs-lookup"><span data-stu-id="70651-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in the Wailers.</span></span> <span data-ttu-id="70651-128">Lorsqu'une notification est envoyée concernant un commentaire de Charlie sur les Beatles, Alice et Bob la reçoivent.</span><span class="sxs-lookup"><span data-stu-id="70651-128">When a notification is sent for Charlie’s comment on the Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="70651-129">Même s’il est possible d’encoder plusieurs paramètres (par exemple, « band_Beatles » ou « follows_Charlie »), les balises sont des chaînes simples et non des propriétés avec des valeurs.</span><span class="sxs-lookup"><span data-stu-id="70651-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="70651-130">Un enregistrement est mis en correspondance uniquement en présence ou en absence d'une balise spécifique.</span><span class="sxs-lookup"><span data-stu-id="70651-130">A registration is matched only on the presence or absence of a specific tag.</span></span>

<span data-ttu-id="70651-131">Pour obtenir un didacticiel complet et détaillé sur la façon d'utiliser des balises pour l'envoi à des groupes d'intérêt, consultez la rubrique [Dernières nouvelles](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="70651-131">For a full step-by-step tutorial on how to use tags for sending to interest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-to-target-users"></a><span data-ttu-id="70651-132">Utilisation de balises pour cibler des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="70651-132">Using tags to target users</span></span>
<span data-ttu-id="70651-133">Une autre façon d'utiliser des balises consiste à identifier tous les appareils d'un utilisateur particulier.</span><span class="sxs-lookup"><span data-stu-id="70651-133">Another way to use tags is to identify all the devices of a particular user.</span></span> <span data-ttu-id="70651-134">Les inscriptions peuvent être étiquetées avec une balise contenant un ID utilisateur, comme dans l'illustration suivante :</span><span class="sxs-lookup"><span data-stu-id="70651-134">Registrations can be tagged with a tag that contains a user id, as in the following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="70651-135">Dans cette illustration, le message étiqueté uid:Alice atteint toutes les inscriptions marquées uid:Alice et, par conséquent, tous les appareils d'Alice.</span><span class="sxs-lookup"><span data-stu-id="70651-135">In this picture, the message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="70651-136">Expressions de balise</span><span class="sxs-lookup"><span data-stu-id="70651-136">Tag expressions</span></span>
<span data-ttu-id="70651-137">Dans certains cas, une notification doit cibler un jeu d'inscriptions identifié non pas par une balise unique, mais par une expression booléenne sur des balises.</span><span class="sxs-lookup"><span data-stu-id="70651-137">There are cases in which a notification has to target a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="70651-138">Examinons une application de sports qui envoie un rappel à tous les abonnés habitant Boston qu’un match opposera les Red Sox aux Cardinals.</span><span class="sxs-lookup"><span data-stu-id="70651-138">Consider a sports application that sends a reminder to everyone in Boston about a game between the Red Sox and Cardinals.</span></span> <span data-ttu-id="70651-139">Si l'application cliente inscrit des balises spécifiques à ces équipes et à ce lieu, la notification doit être ciblée pour tous les abonnés de Boston qui s’intéressent aux Red Sox ou aux Cardinals.</span><span class="sxs-lookup"><span data-stu-id="70651-139">If the client app registers tags about interest in teams and location, then the notification should be targeted to everyone in Boston who is interested in either the Red Sox or the Cardinals.</span></span> <span data-ttu-id="70651-140">Cette condition peut être exprimée avec l'expression booléenne suivante :</span><span class="sxs-lookup"><span data-stu-id="70651-140">This condition can be expressed with the following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="70651-141">Les expressions de balise peuvent contenir tous les opérateurs booléens, notamment AND (&&), OR (||) et NOT (!).</span><span class="sxs-lookup"><span data-stu-id="70651-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="70651-142">Elles peuvent également contenir des parenthèses.</span><span class="sxs-lookup"><span data-stu-id="70651-142">They can also contain parentheses.</span></span> <span data-ttu-id="70651-143">Les expressions de balise sont limitées à 20 balises si elles contiennent uniquement des opérateurs OR ; sinon, elles sont limitées à 6 balises.</span><span class="sxs-lookup"><span data-stu-id="70651-143">Tag expressions are limited to 20 tags if they contain only ORs; otherwise they are limited to 6 tags.</span></span>

<span data-ttu-id="70651-144">Voici un exemple d’envoi de notifications effectué avec des expressions de balise et le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="70651-144">Here's an example for sending notifications with tag expressions using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
