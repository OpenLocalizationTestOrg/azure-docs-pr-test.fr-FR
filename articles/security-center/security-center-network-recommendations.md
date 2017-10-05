---
title: "Protection de votre réseau dans Azure Security Center | Microsoft Docs"
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
ms.openlocfilehash: 00b715507a7c3a4d784b800e7bf0c700f6ea6ff1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="f3694-103">Protection de votre réseau dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f3694-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="f3694-104">Le Centre de sécurité Azure analyse l’état de sécurité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="f3694-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="f3694-105">Lorsque Security Center identifie des failles de sécurité potentielles, il crée des recommandations qui vous guident tout au long du processus de configuration des contrôles nécessaires.</span><span class="sxs-lookup"><span data-stu-id="f3694-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="f3694-106">Ces recommandations s’appliquent aux types de ressources Azure : machines virtuelles, mise en réseau, applications et SQL.</span><span class="sxs-lookup"><span data-stu-id="f3694-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="f3694-107">Cet article traite des recommandations qui s’appliquent à votre réseau.</span><span class="sxs-lookup"><span data-stu-id="f3694-107">This article addresses recommendations that apply to your network.</span></span>  <span data-ttu-id="f3694-108">Les recommandations relatives au réseau se concentrent autour des pare-feu nouvelle génération, des groupes de sécurité réseau, de la configuration des règles de trafic entrant, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="f3694-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="f3694-109">Utilisez le tableau ci-dessous pour mieux comprendre les recommandations disponibles pour le réseau et leurs effets.</span><span class="sxs-lookup"><span data-stu-id="f3694-109">Use the table below as a reference to help you understand the available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="f3694-110">Recommandations disponibles pour le réseau</span><span class="sxs-lookup"><span data-stu-id="f3694-110">Available network recommendations</span></span>
| <span data-ttu-id="f3694-111">Recommandation</span><span class="sxs-lookup"><span data-stu-id="f3694-111">Recommendation</span></span> | <span data-ttu-id="f3694-112">Description</span><span class="sxs-lookup"><span data-stu-id="f3694-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="f3694-113">Ajouter un pare-feu de nouvelle génération</span><span class="sxs-lookup"><span data-stu-id="f3694-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="f3694-114">Recommande l’ajout d’un pare-feu de nouvelle génération d’un partenaire Microsoft afin de renforcer vos protections de sécurité.</span><span class="sxs-lookup"><span data-stu-id="f3694-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> |
| [<span data-ttu-id="f3694-115">Acheminer le trafic uniquement via un pare-feu de nouvelle génération</span><span class="sxs-lookup"><span data-stu-id="f3694-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="f3694-116">Recommande la configuration de règles de groupe de sécurité réseau qui forcent le trafic entrant de votre machine virtuelle via votre pare-feu de nouvelle génération.</span><span class="sxs-lookup"><span data-stu-id="f3694-116">Recommends that you configure network security group (NSG) rules that force inbound traffic to your VM through your NGFW.</span></span> |
| [<span data-ttu-id="f3694-117">Activer des groupes de sécurité réseau sur les sous-réseaux et ou les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="f3694-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="f3694-118">Recommande l’activation des groupes de sécurité réseau sur les sous-réseaux ou les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="f3694-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="f3694-119">Restreindre l’accès via un point de terminaison accessible sur Internet</span><span class="sxs-lookup"><span data-stu-id="f3694-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="f3694-120">Recommande la configuration de règles de trafic entrant pour les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="f3694-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="f3694-121">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f3694-121">See also</span></span>
<span data-ttu-id="f3694-122">Pour en savoir plus sur les recommandations qui s’appliquent à d’autres types de ressources Azure, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="f3694-122">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="f3694-123">Protection de vos machines virtuelles dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f3694-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="f3694-124">Protection de vos applications dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f3694-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="f3694-125">Protection de votre service SQL Azure dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f3694-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="f3694-126">Pour plus d’informations sur le Centre de sécurité, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="f3694-126">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="f3694-127">[Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md) : découvrez comment configurer des stratégies de sécurité pour vos groupes de ressources et abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="f3694-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="f3694-128">[Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="f3694-128">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="f3694-129">[FAQ Azure Security Center](security-center-faq.md) : forum aux questions concernant l’utilisation de ce service.</span><span class="sxs-lookup"><span data-stu-id="f3694-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
