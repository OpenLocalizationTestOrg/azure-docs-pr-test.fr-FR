---
title: "comportement des alertes dans les groupes d’actions aaaSMS | Documents Microsoft"
description: "Format de message SMS et toounsubscribe de messages tooSMS répond, vous réinscrire vos disponible ou demander de l’aide."
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
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="9a4e1-103">Comportement des alertes SMS dans les groupes d’actions</span><span class="sxs-lookup"><span data-stu-id="9a4e1-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="9a4e1-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9a4e1-104">Overview</span></span> ##
<span data-ttu-id="9a4e1-105">Groupes d’actions Activer tooconfigure une liste de destinataires.</span><span class="sxs-lookup"><span data-stu-id="9a4e1-105">Action groups enable you tooconfigure a list of receivers.</span></span> <span data-ttu-id="9a4e1-106">Ces groupes peuvent être utilisées lors de la définition des alertes de journal d’activité ; s’assurer qu’un groupe d’actions particulier est averti hello activité journal alerte est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="9a4e1-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when hello activity log alert is triggered.</span></span> <span data-ttu-id="9a4e1-107">Un de génération d’alertes de la prise en charge des mécanismes de hello est SMS ; alertes de Hello prend en charge la communication bidirectionnelle.</span><span class="sxs-lookup"><span data-stu-id="9a4e1-107">One of hello alerting mechanisms supported is SMS; hello alerts support bi-directional communication.</span></span> <span data-ttu-id="9a4e1-108">Un utilisateur peut répondre alerte tooan à :</span><span class="sxs-lookup"><span data-stu-id="9a4e1-108">A user can respond tooan alert to:</span></span>

- <span data-ttu-id="9a4e1-109">**Se désabonner des alertes :** Un utilisateur peut annuler l’abonnement pour toutes les alertes SMS pour tous les groupes d’actions, ou un groupe d’actions particulier.</span><span class="sxs-lookup"><span data-stu-id="9a4e1-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="9a4e1-110">**Vous réinscrire vos disponible tooalerts :** un utilisateur peut vous réinscrire vos disponible tooall des alertes SMS pour tous les groupes d’actions ou un groupe d’actions au singulier.</span><span class="sxs-lookup"><span data-stu-id="9a4e1-110">**Resubscribe tooalerts:** A user can resubscribe tooall SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="9a4e1-111">**Demander de l’aide :** un utilisateur peut demander pour plus d’informations sur hello SMS.</span><span class="sxs-lookup"><span data-stu-id="9a4e1-111">**Request help:** A user can ask for more information on hello SMS.</span></span> <span data-ttu-id="9a4e1-112">Il sera redirigé toothis article</span><span class="sxs-lookup"><span data-stu-id="9a4e1-112">They will be redirected toothis article</span></span>

<span data-ttu-id="9a4e1-113">Cet article traite du comportement de hello d’alertes SMS hello et hello utilisateur de hello actions de réponse peut entreprendre en fonction des paramètres régionaux de hello d’utilisateur de hello :</span><span class="sxs-lookup"><span data-stu-id="9a4e1-113">This article covers hello behavior of hello SMS alerts and hello response actions hello user can take based on hello locale of hello user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="9a4e1-114">Comportement SMS États-Unis/Canada</span><span class="sxs-lookup"><span data-stu-id="9a4e1-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="9a4e1-115">Réception d’une alerte SMS</span><span class="sxs-lookup"><span data-stu-id="9a4e1-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="9a4e1-116">Un destinataire SMS, qui est configuré comme faisant partie d’un groupe d’actions, recevra un SMS lorsqu’une alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="9a4e1-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="9a4e1-117">Hello SMS transitent hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="9a4e1-117">hello SMS will carry hello following information:</span></span>
* <span data-ttu-id="9a4e1-118">Nom court du groupe d’actions hello cette alerte a été envoyée à</span><span class="sxs-lookup"><span data-stu-id="9a4e1-118">Shortname of hello action group this alert was sent to</span></span>
- <span data-ttu-id="9a4e1-119">Titre de l’alerte de hello</span><span class="sxs-lookup"><span data-stu-id="9a4e1-119">Title of hello alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="9a4e1-120">Désabonnement d’alertes SMS pour un groupe d’actions</span><span class="sxs-lookup"><span data-stu-id="9a4e1-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="9a4e1-121">Un utilisateur peut annuler l’abonnement à partir de SMS pour les alertes pour le groupe d’une action en répond toohello « Stop » au 20873 avec les mots clés de hello : « désactiver &lt;nom court du groupe d’actions&gt;».</span><span class="sxs-lookup"><span data-stu-id="9a4e1-121">A user can unsubscribe from SMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="9a4e1-122">P.</span><span class="sxs-lookup"><span data-stu-id="9a4e1-122">Ex.</span></span> <span data-ttu-id="9a4e1-123">Un utilisateur souhaitant toounsubscribe à partir d’alertes pour un groupe d’actions avec le nom court de hello « Azure », envoyez un « Stop » au toohello SMS 20873 indiquant que « Désactiver Azure »</span><span class="sxs-lookup"><span data-stu-id="9a4e1-123">A user wishing toounsubscribe from alerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="9a4e1-124">Annulation d’alertes SMS pour tous les groupes d’actions</span><span class="sxs-lookup"><span data-stu-id="9a4e1-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="9a4e1-125">Un utilisateur peut annuler l’abonnement à partir de toutes les alertes SMS pour tous les groupes d’actions en réponse toohello « Stop » au 20873 avec n’importe quelle Hello après les mots clés :</span><span class="sxs-lookup"><span data-stu-id="9a4e1-125">A user can unsubscribe from all SMS alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="9a4e1-126">STOP</span><span class="sxs-lookup"><span data-stu-id="9a4e1-126">STOP</span></span>

<span data-ttu-id="9a4e1-127">P.</span><span class="sxs-lookup"><span data-stu-id="9a4e1-127">Ex.</span></span> <span data-ttu-id="9a4e1-128">Un utilisateur souhaitant toounsubscribe à partir de toutes les alertes SMS pour tous les groupes d’actions, envoyez un « Stop » au toohello SMS 20873 indiquant que « Arrêter »</span><span class="sxs-lookup"><span data-stu-id="9a4e1-128">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="9a4e1-129">Si un utilisateur a annulé son abonnement à partir de SMS des alertes, mais il est ensuite ajouté le nouveau groupe d’actions tooa ; ils seront recevoir des alertes SMS pour ce nouveau groupe d’actions, mais restent non inscrits à partir de tous les groupes d’actions précédent.</span><span class="sxs-lookup"><span data-stu-id="9a4e1-129">If a user has unsubscribed from SMS alerts, but is then added tooa new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a><span data-ttu-id="9a4e1-130">Resubscribing tooSMS des alertes pour un groupe d’actions</span><span class="sxs-lookup"><span data-stu-id="9a4e1-130">Resubscribing tooSMS alerts for one action group</span></span>
<span data-ttu-id="9a4e1-131">Un utilisateur peut vous réinscrire vos disponible tooSMS pour les alertes pour le groupe d’une action en réponse toohello « Stop » au 20873 avec les mots clés de hello : « activer &lt;nom court du groupe d’actions&gt;».</span><span class="sxs-lookup"><span data-stu-id="9a4e1-131">A user can resubscribe tooSMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="9a4e1-132">P.</span><span class="sxs-lookup"><span data-stu-id="9a4e1-132">Ex.</span></span> <span data-ttu-id="9a4e1-133">Un utilisateur souhaitant tooalerts tooresubscribe pour un groupe d’actions avec le nom court de hello « Azure », envoyez un « Stop » au toohello SMS 20873 indiquant que « Activer Azure »</span><span class="sxs-lookup"><span data-stu-id="9a4e1-133">A user wishing tooresubscribe tooalerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a><span data-ttu-id="9a4e1-134">Resubscribing tooSMS des alertes pour tous les groupes d’actions</span><span class="sxs-lookup"><span data-stu-id="9a4e1-134">Resubscribing tooSMS alerts for all action groups</span></span>
<span data-ttu-id="9a4e1-135">Un utilisateur peut réabonner tooall SMS pour les alertes pour tous les groupes d’actions en réponse toohello « Stop » au 20873 avec n’importe quelle Hello après les mots clés :</span><span class="sxs-lookup"><span data-stu-id="9a4e1-135">A user can resubscribe tooall SMS for alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>

* <span data-ttu-id="9a4e1-136">START</span><span class="sxs-lookup"><span data-stu-id="9a4e1-136">START</span></span>

<span data-ttu-id="9a4e1-137">P.</span><span class="sxs-lookup"><span data-stu-id="9a4e1-137">Ex.</span></span> <span data-ttu-id="9a4e1-138">Un utilisateur souhaitant toounsubscribe à partir de toutes les alertes SMS pour tous les groupes d’actions, envoyez un « Stop » au toohello SMS 20873 indiquant que « Démarrer »</span><span class="sxs-lookup"><span data-stu-id="9a4e1-138">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="9a4e1-139">Demande d’aide via SMS</span><span class="sxs-lookup"><span data-stu-id="9a4e1-139">Requesting help via SMS</span></span>
<span data-ttu-id="9a4e1-140">Un utilisateur peut demander pour plus d’informations sur hello SMS qu’ils ont reçu par toohello répond « Stop » au 20873 avec les hello après les mots clés :</span><span class="sxs-lookup"><span data-stu-id="9a4e1-140">A user can ask for more information about hello SMS they have received by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="9a4e1-141">HELP</span><span class="sxs-lookup"><span data-stu-id="9a4e1-141">HELP</span></span>

<span data-ttu-id="9a4e1-142">Une réponse est envoyée utilisateur toohello avec un article de toothis du lien.</span><span class="sxs-lookup"><span data-stu-id="9a4e1-142">A response will be sent toohello user with a link toothis article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a4e1-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9a4e1-143">Next Steps</span></span>
<span data-ttu-id="9a4e1-144">Obtenir un [vue d’ensemble des alertes de journal d’activité](monitoring-overview-alerts.md) et découvrez comment tooget alerté</span><span class="sxs-lookup"><span data-stu-id="9a4e1-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how tooget alerted</span></span>  
<span data-ttu-id="9a4e1-145">En savoir plus sur la [restriction des SMS](monitoring-alerts-rate-limiting.md)</span><span class="sxs-lookup"><span data-stu-id="9a4e1-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="9a4e1-146">En savoir plus sur les [groupes de ressources](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="9a4e1-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>
