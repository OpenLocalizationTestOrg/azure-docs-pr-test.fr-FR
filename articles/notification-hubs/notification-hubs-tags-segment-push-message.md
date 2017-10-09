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
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="2d3f5-103">Routage et expressions de balise</span><span class="sxs-lookup"><span data-stu-id="2d3f5-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="2d3f5-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="2d3f5-104">Overview</span></span>
<span data-ttu-id="2d3f5-105">Les expressions de balises permettent de tootarget des ensembles spécifiques d’appareils ou plus particulièrement d’inscriptions, lors de l’envoi d’une notification push via des concentrateurs de Notification.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-105">Tag expressions enable you tootarget specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="2d3f5-106">Ciblage d'inscriptions spécifiques</span><span class="sxs-lookup"><span data-stu-id="2d3f5-106">Targeting specific registrations</span></span>
<span data-ttu-id="2d3f5-107">Hello uniquement moyen tootarget notification spécifique des enregistrements est balises tooassociate avec eux, puis cibler ces balises.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-107">hello only way tootarget specific notification registrations is tooassociate tags with them, then target those tags.</span></span> <span data-ttu-id="2d3f5-108">Comme indiqué dans [gestion de l’inscription](notification-hubs-push-notification-registration-management.md), de push de tooreceive d’ordre notifications d’une application a tooregister un appareil gérer sur un concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order tooreceive push notifications an app has tooregister a device handle on a notification hub.</span></span> <span data-ttu-id="2d3f5-109">Une fois qu’un enregistrement est créé sur un concentrateur de notification, hello principale peut envoyer tooit de notifications push.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-109">Once a registration is created on a notification hub, hello application backend can send push notifications tooit.</span></span>
<span data-ttu-id="2d3f5-110">principal d’application Hello peut choisir tootarget d’inscriptions hello avec une notification spécifique Bonjour suivant façons :</span><span class="sxs-lookup"><span data-stu-id="2d3f5-110">hello application backend can choose hello registrations tootarget with a specific notification in hello following ways:</span></span>

1. <span data-ttu-id="2d3f5-111">**Diffusion**: tous les enregistrements dans le hub de notification hello recevoir une notification de hello.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-111">**Broadcast**: all registrations in hello notification hub receive hello notification.</span></span>
2. <span data-ttu-id="2d3f5-112">**Balise**: tous les enregistrements qui contiennent des hello spécifié balise recevoir une notification de hello.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-112">**Tag**: all registrations that contain hello specified tag receive hello notification.</span></span>
3. <span data-ttu-id="2d3f5-113">**Expression de balise**: toutes les inscriptions dont l’ensemble de balises correspondance hello expression spécifiée reçoivent notification de hello.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-113">**Tag expression**: all registrations whose set of tags match hello specified expression receive hello notification.</span></span>

## <a name="tags"></a><span data-ttu-id="2d3f5-114">Tags</span><span class="sxs-lookup"><span data-stu-id="2d3f5-114">Tags</span></span>
<span data-ttu-id="2d3f5-115">Une balise peut être n’importe quelle chaîne, des too120, contenant des caractères alphanumériques et hello les caractères non alphanumériques suivants : '_', ' @', '#', '. ',' :', '-'.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-115">A tag can be any string, up too120 characters, containing alphanumeric and hello following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="2d3f5-116">Hello suivant montre une application à partir de laquelle vous pouvez recevoir des notifications toast concernant des groupes musicaux spécifiques.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-116">hello following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="2d3f5-117">Dans ce scénario, une notification de tooroute moyen simple est inscriptions toolabel avec balises qui représentent des bandes différentes hello, comme dans hello illustration suivante.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-117">In this scenario, a simple way tooroute notifications is toolabel registrations with tags that represent hello different bands, as in hello following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="2d3f5-118">Dans cette illustration, le message de type hello marquées **Beatles** atteint uniquement hello tablette enregistrée avec la balise de hello **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-118">In this picture, hello message tagged **Beatles** reaches only hello tablet that registered with hello tag **Beatles**.</span></span>

<span data-ttu-id="2d3f5-119">Pour plus d'informations sur la création d’inscriptions pour des balises, consultez [Gestion des inscriptions](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="2d3f5-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="2d3f5-120">Vous pouvez envoyer des tootags des notifications à l’aide de hello d’envoi des méthodes de notifications de hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` classe Bonjour [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-120">You can send notifications tootags using hello send notifications methods of hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in hello [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="2d3f5-121">Vous pouvez également utiliser Node.js ou hello API REST de Notifications Push.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-121">You can also use Node.js, or hello Push Notifications REST APIs.</span></span>  <span data-ttu-id="2d3f5-122">Voici un exemple d’utilisation hello SDK.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-122">Here's an example using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="2d3f5-123">Balises n’ont pas de toobe pré-configurés et peuvent faire référence les concepts de toomultiple spécifique à l’application.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-123">Tags do not have toobe pre-provisioned and can refer toomultiple app-specific concepts.</span></span> <span data-ttu-id="2d3f5-124">Par exemple, les utilisateurs de cet exemple d’application peuvent commenter les bandes et souhaitez tooreceive toasts, non seulement pour les commentaires de hello sur leurs groupes favoris, mais aussi pour tous les commentaires de leurs amis, quel que soit la bande hello sur lequel ils entrent des commentaires.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-124">For example, users of this example application can comment on bands and want tooreceive toasts, not only for hello comments on their favorite bands, but also for all comments from their friends, regardless of hello band on which they are commenting.</span></span> <span data-ttu-id="2d3f5-125">Hello illustration suivante montre un exemple de ce scénario :</span><span class="sxs-lookup"><span data-stu-id="2d3f5-125">hello following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="2d3f5-126">Dans cette image, Alice s’intéresse aux mises à jour pour hello Beatles, et Bob s’intéresse aux mises à jour pour hello aux Wailers.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-126">In this picture, Alice is interested in updates for hello Beatles, and Bob is interested in updates for hello Wailers.</span></span> <span data-ttu-id="2d3f5-127">Bob est également intéressée par commentaires de Charlie, et Charlie s’intéresse aux Wailers de hello.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in hello Wailers.</span></span> <span data-ttu-id="2d3f5-128">Lorsqu’une notification est envoyée pour le commentaire de Charlie sur hello Beatles, Alice et Bob reçoit.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-128">When a notification is sent for Charlie’s comment on hello Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="2d3f5-129">Même s’il est possible d’encoder plusieurs paramètres (par exemple, « band_Beatles » ou « follows_Charlie »), les balises sont des chaînes simples et non des propriétés avec des valeurs.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="2d3f5-130">Un enregistrement est mis en correspondance uniquement sur la présence de hello ou l’absence d’une balise spécifique.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-130">A registration is matched only on hello presence or absence of a specific tag.</span></span>

<span data-ttu-id="2d3f5-131">Pour obtenir un didacticiel complet et détaillé sur comment toouse les balises pour l’envoi de groupes de toointerest, consultez [dernières nouvelles](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="2d3f5-131">For a full step-by-step tutorial on how toouse tags for sending toointerest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-tootarget-users"></a><span data-ttu-id="2d3f5-132">À l’aide de balises tootarget utilisateurs</span><span class="sxs-lookup"><span data-stu-id="2d3f5-132">Using tags tootarget users</span></span>
<span data-ttu-id="2d3f5-133">Une autre façon toouse balises est tooidentify tous les appareils hello d’un utilisateur particulier.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-133">Another way toouse tags is tooidentify all hello devices of a particular user.</span></span> <span data-ttu-id="2d3f5-134">Les enregistrements peuvent être identifiés avec une balise qui contient un id d’utilisateur, comme dans hello illustration suivante :</span><span class="sxs-lookup"><span data-stu-id="2d3f5-134">Registrations can be tagged with a tag that contains a user id, as in hello following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="2d3f5-135">Dans cette image, UID : Alice de message marquée hello atteint tous les enregistrements marqués UID : Alice ; Par conséquent, tous les appareils d’Alice.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-135">In this picture, hello message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="2d3f5-136">Expressions de balise</span><span class="sxs-lookup"><span data-stu-id="2d3f5-136">Tag expressions</span></span>
<span data-ttu-id="2d3f5-137">Il existe des cas dans lesquels une notification a tootarget un jeu d’enregistrements identifié pas par une balise unique, mais par une expression booléenne sur les balises.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-137">There are cases in which a notification has tootarget a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="2d3f5-138">Considérez une application de sports qui envoie un rappel tooeveryone à Boston concernant un match entre hello Red Sox et les Cardinals.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-138">Consider a sports application that sends a reminder tooeveryone in Boston about a game between hello Red Sox and Cardinals.</span></span> <span data-ttu-id="2d3f5-139">Si hello client application inscrit des balises sur l’intérêt dans les équipes et l’emplacement, puis hello notification doit être ciblée tooeveryone à Boston qui souhaitent hello Red Sox ou de hello Cardinals.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-139">If hello client app registers tags about interest in teams and location, then hello notification should be targeted tooeveryone in Boston who is interested in either hello Red Sox or hello Cardinals.</span></span> <span data-ttu-id="2d3f5-140">Cette condition peut être exprimée par hello expression booléenne suivante :</span><span class="sxs-lookup"><span data-stu-id="2d3f5-140">This condition can be expressed with hello following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="2d3f5-141">Les expressions de balise peuvent contenir tous les opérateurs booléens, notamment AND (&&), OR (||) et NOT (!).</span><span class="sxs-lookup"><span data-stu-id="2d3f5-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="2d3f5-142">Elles peuvent également contenir des parenthèses.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-142">They can also contain parentheses.</span></span> <span data-ttu-id="2d3f5-143">Expressions de balises sont limitées too20 balises si elles contiennent uniquement des opérateurs OR ; Sinon, elles sont limitées too6 balises.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-143">Tag expressions are limited too20 tags if they contain only ORs; otherwise they are limited too6 tags.</span></span>

<span data-ttu-id="2d3f5-144">Voici un exemple pour envoyer des notifications avec des expressions de balise à l’aide du Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="2d3f5-144">Here's an example for sending notifications with tag expressions using hello SDK.</span></span>

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
