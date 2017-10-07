---
title: "aaaProtecting votre réseau dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document traite des recommandations d’Azure Security Center qui peuvent vous aider à protéger votre réseau Azure et à rester en conformité avec les stratégies de sécurité."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="b798f-103">Protection de votre réseau dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="b798f-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="b798f-104">Centre de sécurité Azure analyse l’état de la sécurité de vos ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b798f-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="b798f-105">Lorsque le centre de sécurité identifie les éventuelles failles de sécurité, il crée des recommandations qui vous guident tout au long des processus de hello de configuration de contrôles de hello nécessité.</span><span class="sxs-lookup"><span data-stu-id="b798f-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="b798f-106">Recommandations s’appliquent à des types de ressources tooAzure : machines virtuelles (VM), mise en réseau, SQL et les applications.</span><span class="sxs-lookup"><span data-stu-id="b798f-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="b798f-107">Cet article traite des recommandations qui s’appliquent tooyour réseau.</span><span class="sxs-lookup"><span data-stu-id="b798f-107">This article addresses recommendations that apply tooyour network.</span></span>  <span data-ttu-id="b798f-108">Les recommandations relatives au réseau se concentrent autour des pare-feu nouvelle génération, des groupes de sécurité réseau, de la configuration des règles de trafic entrant, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="b798f-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="b798f-109">Tableau hello ci-dessous comme un toohelp de référence que vous comprenez les recommandations de réseau disponible hello et ce que fait chacun d’eux si vous l’appliquez.</span><span class="sxs-lookup"><span data-stu-id="b798f-109">Use hello table below as a reference toohelp you understand hello available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="b798f-110">Recommandations disponibles pour le réseau</span><span class="sxs-lookup"><span data-stu-id="b798f-110">Available network recommendations</span></span>
| <span data-ttu-id="b798f-111">Recommandation</span><span class="sxs-lookup"><span data-stu-id="b798f-111">Recommendation</span></span> | <span data-ttu-id="b798f-112">Description</span><span class="sxs-lookup"><span data-stu-id="b798f-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="b798f-113">Ajouter un pare-feu de nouvelle génération</span><span class="sxs-lookup"><span data-stu-id="b798f-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="b798f-114">Recommande d’ajouter un pare-feu de la génération suivante (Conviction) à partir d’un tooincrease de partenaire Microsoft votre protections de sécurité.</span><span class="sxs-lookup"><span data-stu-id="b798f-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> |
| [<span data-ttu-id="b798f-115">Acheminer le trafic uniquement via un pare-feu de nouvelle génération</span><span class="sxs-lookup"><span data-stu-id="b798f-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="b798f-116">Recommande de configurer les règles de groupe (NSG) de sécurité réseau qui force le trafic entrant tooyour machine virtuelle via votre Conviction.</span><span class="sxs-lookup"><span data-stu-id="b798f-116">Recommends that you configure network security group (NSG) rules that force inbound traffic tooyour VM through your NGFW.</span></span> |
| [<span data-ttu-id="b798f-117">Activer des groupes de sécurité réseau sur les sous-réseaux et ou les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="b798f-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="b798f-118">Recommande l’activation des groupes de sécurité réseau sur les sous-réseaux ou les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="b798f-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="b798f-119">Restreindre l’accès via un point de terminaison accessible sur Internet</span><span class="sxs-lookup"><span data-stu-id="b798f-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="b798f-120">Recommande la configuration de règles de trafic entrant pour les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="b798f-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="b798f-121">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b798f-121">See also</span></span>
<span data-ttu-id="b798f-122">toolearn en savoir plus sur les recommandations qui s’appliquent les types de ressources Azure tooother, voir hello :</span><span class="sxs-lookup"><span data-stu-id="b798f-122">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="b798f-123">Protection de vos machines virtuelles dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="b798f-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="b798f-124">Protection de vos applications dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="b798f-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="b798f-125">Protection de votre service SQL Azure dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="b798f-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="b798f-126">toolearn en savoir plus sur le centre de sécurité, voir hello :</span><span class="sxs-lookup"><span data-stu-id="b798f-126">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="b798f-127">[Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="b798f-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="b798f-128">[Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="b798f-128">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="b798f-129">[Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.</span><span class="sxs-lookup"><span data-stu-id="b798f-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
