---
title: "aaaRate limitée pour SMS, des messages électroniques et de webhooks | Documents Microsoft"
description: "Comprendre comment Azure limite le nombre de hello des notifications de SMS, par courrier électronique ou webhook possibles à partir d’un groupe d’actions."
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
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="93ee6-103">Limitation de la fréquence des SMS, e-mails et publications Webhook</span><span class="sxs-lookup"><span data-stu-id="93ee6-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="93ee6-104">Limitation du débit est une suspension de notifications qui se produit quand trop de notifications sont envoyées tooa téléphone particulier numéro ou adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="93ee6-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent tooa particular phone number or email address.</span></span> <span data-ttu-id="93ee6-105">Elle garantit que les alertes sont faciles à gérer et exploitables.</span><span class="sxs-lookup"><span data-stu-id="93ee6-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="93ee6-106">règles de Hello pour SMS et par courrier électronique sont hello identiques.</span><span class="sxs-lookup"><span data-stu-id="93ee6-106">hello rules for SMS and email are hello same.</span></span> <span data-ttu-id="93ee6-107">limite de seuil de taux Hello est la suivante :</span><span class="sxs-lookup"><span data-stu-id="93ee6-107">hello rate limit threshold is:</span></span>

 - <span data-ttu-id="93ee6-108">**SMS** : 10 messages en une heure ;</span><span class="sxs-lookup"><span data-stu-id="93ee6-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="93ee6-109">**E-mail** : 100 messages en une heure.</span><span class="sxs-lookup"><span data-stu-id="93ee6-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="93ee6-110">Règles de limitation de la fréquence</span><span class="sxs-lookup"><span data-stu-id="93ee6-110">Rate limit rules</span></span>
- <span data-ttu-id="93ee6-111">Un numéro de téléphone particulier ou un e-mail est limitée lorsqu’il reçoit plus de messages que le seuil de hello permet de taux.</span><span class="sxs-lookup"><span data-stu-id="93ee6-111">A particular phone number or email is rate limited when it receives more messages than hello threshold allows.</span></span>
- <span data-ttu-id="93ee6-112">Un numéro de téléphone ou une adresse de messagerie peut faire partie de groupes d’actions sur plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="93ee6-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="93ee6-113">La limitation de la fréquence s’applique à tous les abonnements,</span><span class="sxs-lookup"><span data-stu-id="93ee6-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="93ee6-114">Il s’applique dès que hello est atteint, même si les messages sont envoyés à partir de plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="93ee6-114">It applies as soon as hello threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="93ee6-115">Quand un numéro de téléphone ou un e-mail taux limitée, une notification supplémentaire est envoyée toocommunicate hello limitation du débit.</span><span class="sxs-lookup"><span data-stu-id="93ee6-115">When a phone number or email is rate limited, an additional notification is sent toocommunicate hello rate limiting.</span></span> <span data-ttu-id="93ee6-116">Hello États lorsque hello limitation du débit de notification d’expiration.</span><span class="sxs-lookup"><span data-stu-id="93ee6-116">hello notification states when hello rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="93ee6-117">Limite de fréquence des Webhooks</span><span class="sxs-lookup"><span data-stu-id="93ee6-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="93ee6-118">Aucune limitation de la fréquence n’est appliquée aux Webhooks.</span><span class="sxs-lookup"><span data-stu-id="93ee6-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93ee6-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="93ee6-119">Next steps</span></span> ##
* <span data-ttu-id="93ee6-120">En savoir plus sur le [comportement des alertes SMS](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="93ee6-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="93ee6-121">Obtenir un [vue d’ensemble des alertes de journal d’activité](monitoring-overview-alerts.md)et découvrez comment tooreceive alertes.</span><span class="sxs-lookup"><span data-stu-id="93ee6-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="93ee6-122">Découvrez comment trop[configurer des alertes lors de la validation d’une notification de contrôle d’intégrité du service](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="93ee6-122">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
