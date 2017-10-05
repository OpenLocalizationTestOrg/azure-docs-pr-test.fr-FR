---
title: "Comportement des alertes SMS dans les groupes d’actions | Microsoft Docs"
description: "Format de message SMS et réponse aux messages SMS pour annuler un abonnement, vous réinscrire ou demander de l’aide."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 3e4eca174209eeb9cbce1d45111d1e5cc30af8b0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="1341d-103">Comportement des alertes SMS dans les groupes d’actions</span><span class="sxs-lookup"><span data-stu-id="1341d-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="1341d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1341d-104">Overview</span></span> ##
<span data-ttu-id="1341d-105">Les groupes d’actions vous permettent de configurer une liste de destinataires.</span><span class="sxs-lookup"><span data-stu-id="1341d-105">Action groups enable you to configure a list of receivers.</span></span> <span data-ttu-id="1341d-106">Ces groupes peuvent être utilisés lors de la définition des alertes de journal d’activité, en veillant à ce qu’un groupe d’actions particulier soit notifié au déclenchement de l’alerte de journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="1341d-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when the activity log alert is triggered.</span></span> <span data-ttu-id="1341d-107">Un des mécanismes d’alerte pris en charge est le SMS ; les alertes prennent en charge la communication bidirectionnelle.</span><span class="sxs-lookup"><span data-stu-id="1341d-107">One of the alerting mechanisms supported is SMS; the alerts support bi-directional communication.</span></span> <span data-ttu-id="1341d-108">Un utilisateur peut répondre à une alerte pour :</span><span class="sxs-lookup"><span data-stu-id="1341d-108">A user can respond to an alert to:</span></span>

- <span data-ttu-id="1341d-109">**Se désabonner des alertes :** Un utilisateur peut annuler l’abonnement pour toutes les alertes SMS pour tous les groupes d’actions, ou un groupe d’actions particulier.</span><span class="sxs-lookup"><span data-stu-id="1341d-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="1341d-110">**Se réinscrire aux alertes :** Un utilisateur peut se réinscrire à toutes les alertes SMS pour tous les groupes d’actions, ou à groupe d’actions particulier.</span><span class="sxs-lookup"><span data-stu-id="1341d-110">**Resubscribe to alerts:** A user can resubscribe to all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="1341d-111">**Demander de l’aide :** Un utilisateur peut demander plus d’informations sur le SMS.</span><span class="sxs-lookup"><span data-stu-id="1341d-111">**Request help:** A user can ask for more information on the SMS.</span></span> <span data-ttu-id="1341d-112">Ils seront redirigés vers cet article</span><span class="sxs-lookup"><span data-stu-id="1341d-112">They will be redirected to this article</span></span>

<span data-ttu-id="1341d-113">Cet article traite du comportement des alertes SMS et des actions de réponse que l’utilisateur peut entreprendre en fonction des paramètres régionaux de l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="1341d-113">This article covers the behavior of the SMS alerts and the response actions the user can take based on the locale of the user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="1341d-114">Comportement SMS États-Unis/Canada</span><span class="sxs-lookup"><span data-stu-id="1341d-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="1341d-115">Réception d’une alerte SMS</span><span class="sxs-lookup"><span data-stu-id="1341d-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="1341d-116">Un destinataire SMS, qui est configuré comme faisant partie d’un groupe d’actions, recevra un SMS lorsqu’une alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="1341d-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="1341d-117">Le SMS contiendra les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1341d-117">The SMS will carry the following information:</span></span>
* <span data-ttu-id="1341d-118">Le nom court du groupe d’actions auquel cette alerte a été envoyée</span><span class="sxs-lookup"><span data-stu-id="1341d-118">Shortname of the action group this alert was sent to</span></span>
- <span data-ttu-id="1341d-119">Titre de l’alerte</span><span class="sxs-lookup"><span data-stu-id="1341d-119">Title of the alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="1341d-120">Désabonnement d’alertes SMS pour un groupe d’actions</span><span class="sxs-lookup"><span data-stu-id="1341d-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="1341d-121">Un utilisateur peut se désabonner de SMS pour les alertes pour un groupe d’actions en répondant avec le code 20873 avec les mots-clés « Stop » avec les mots clés : « DISABLE &lt;Nom court du groupe d’actions&gt; ».</span><span class="sxs-lookup"><span data-stu-id="1341d-121">A user can unsubscribe from SMS for alerts for one action group by responding to the shortcode 20873 with the keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="1341d-122">P.</span><span class="sxs-lookup"><span data-stu-id="1341d-122">Ex.</span></span> <span data-ttu-id="1341d-123">Un utilisateur souhaitant se désabonner des alertes pour un groupe d’actions avec le nom court « Azure », enverrait ainsi un SMS avec le code 20873 indiquant « DISABLE Azure »</span><span class="sxs-lookup"><span data-stu-id="1341d-123">A user wishing to unsubscribe from alerts for an action group with the shortname “Azure”, would send an SMS to the shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="1341d-124">Annulation d’alertes SMS pour tous les groupes d’actions</span><span class="sxs-lookup"><span data-stu-id="1341d-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="1341d-125">Un utilisateur peut se désabonner de toutes les alertes SMS pour tous les groupes d’actions en répondant avec le code 20873 accompagné d’un des mots-clés suivants :</span><span class="sxs-lookup"><span data-stu-id="1341d-125">A user can unsubscribe from all SMS alerts for all action groups by responding to the shortcode 20873 with any of the following keywords:</span></span>
* <span data-ttu-id="1341d-126">STOP</span><span class="sxs-lookup"><span data-stu-id="1341d-126">STOP</span></span>

<span data-ttu-id="1341d-127">P.</span><span class="sxs-lookup"><span data-stu-id="1341d-127">Ex.</span></span> <span data-ttu-id="1341d-128">Un utilisateur souhaitant se désabonner de toutes les alertes SMS pour un groupe d’actions enverrait ainsi un SMS avec le code 20873 indiquant « STOP »</span><span class="sxs-lookup"><span data-stu-id="1341d-128">A user wishing to unsubscribe from all SMS alerts for all action groups, would send an SMS to the shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="1341d-129">Si un utilisateur a annulé son abonnement aux alertes SMS, mais est ensuite ajouté à un nouveau groupe d’actions ; il RECEVRA les alertes SMS pour ce nouveau groupe d’actions, mais restera désabonné de tous les groupes d’actions précédents.</span><span class="sxs-lookup"><span data-stu-id="1341d-129">If a user has unsubscribed from SMS alerts, but is then added to a new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-to-sms-alerts-for-one-action-group"></a><span data-ttu-id="1341d-130">Réabonnement aux alertes SMS pour un groupe d’actions</span><span class="sxs-lookup"><span data-stu-id="1341d-130">Resubscribing to SMS alerts for one action group</span></span>
<span data-ttu-id="1341d-131">Un utilisateur peut se réabonner aux SMS pour les alertes pour un groupe d’actions en répondant avec le code 20873 avec les mots-clés « Stop » avec les mots clés : « ENABLE &lt;Nom court du groupe d’actions&gt; ».</span><span class="sxs-lookup"><span data-stu-id="1341d-131">A user can resubscribe to SMS for alerts for one action group by responding to the shortcode 20873 with the keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="1341d-132">P.</span><span class="sxs-lookup"><span data-stu-id="1341d-132">Ex.</span></span> <span data-ttu-id="1341d-133">Un utilisateur souhaitant se réabonner aux alertes pour un groupe d’actions avec le nom court « Azure », enverrait ainsi un SMS avec le code 20873 indiquant « ENABLE Azure »</span><span class="sxs-lookup"><span data-stu-id="1341d-133">A user wishing to resubscribe to alerts for an action group with the shortname “Azure”, would send an SMS to the shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-to-sms-alerts-for-all-action-groups"></a><span data-ttu-id="1341d-134">Réabonnement aux alertes SMS pour tous les groupes d’actions</span><span class="sxs-lookup"><span data-stu-id="1341d-134">Resubscribing to SMS alerts for all action groups</span></span>
<span data-ttu-id="1341d-135">Un utilisateur peut se réabonner à toutes les alertes SMS pour tous les groupes d’actions en répondant avec le code 20873 accompagné d’un des mots-clés suivants :</span><span class="sxs-lookup"><span data-stu-id="1341d-135">A user can resubscribe to all SMS for alerts for all action groups by responding to the shortcode 20873 with any of the following keywords:</span></span>

* <span data-ttu-id="1341d-136">START</span><span class="sxs-lookup"><span data-stu-id="1341d-136">START</span></span>

<span data-ttu-id="1341d-137">P.</span><span class="sxs-lookup"><span data-stu-id="1341d-137">Ex.</span></span> <span data-ttu-id="1341d-138">Un utilisateur souhaitant se réabonner à toutes les alertes SMS pour un groupe d’actions enverrait ainsi un SMS avec le code 20873 indiquant « START »</span><span class="sxs-lookup"><span data-stu-id="1341d-138">A user wishing to unsubscribe from all SMS alerts for all action groups, would send an SMS to the shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="1341d-139">Demande d’aide via SMS</span><span class="sxs-lookup"><span data-stu-id="1341d-139">Requesting help via SMS</span></span>
<span data-ttu-id="1341d-140">Un utilisateur peut demander plus d’informations sur le SMS qu’ils ont reçu en répondant avec le code 20873 accompagné d’un des mots-clés suivants :</span><span class="sxs-lookup"><span data-stu-id="1341d-140">A user can ask for more information about the SMS they have received by responding to the shortcode 20873 with any of the following keywords:</span></span>
* <span data-ttu-id="1341d-141">HELP</span><span class="sxs-lookup"><span data-stu-id="1341d-141">HELP</span></span>

<span data-ttu-id="1341d-142">Une réponse est envoyée à l’utilisateur avec un lien vers cet article.</span><span class="sxs-lookup"><span data-stu-id="1341d-142">A response will be sent to the user with a link to this article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1341d-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1341d-143">Next Steps</span></span>
<span data-ttu-id="1341d-144">Obtenez une [Vue d’ensemble des alertes de journal d’activité](monitoring-overview-alerts.md) et découvrez comment recevoir des alertes</span><span class="sxs-lookup"><span data-stu-id="1341d-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted</span></span>  
<span data-ttu-id="1341d-145">En savoir plus sur la [restriction des SMS](monitoring-alerts-rate-limiting.md)</span><span class="sxs-lookup"><span data-stu-id="1341d-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="1341d-146">En savoir plus sur les [groupes de ressources](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="1341d-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>
