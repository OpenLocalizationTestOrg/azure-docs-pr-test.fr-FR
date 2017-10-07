---
title: "aaaEnable des groupes de sécurité réseau dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** activer réseau sécurité groupes **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="d7ee7-103">Activation de groupes de sécurité réseau dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="d7ee7-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="d7ee7-104">Azure Security Center vous recommande d’activer un groupe de sécurité réseau si aucun n’est encore activé.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="d7ee7-105">Groupes de sécurité réseau contient une liste de règles de liste de contrôle d’accès (ACL) qui autorisent ou refusent le trafic réseau tooyour des instances de machine virtuelle dans un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic tooyour VM instances in a Virtual Network.</span></span> <span data-ttu-id="d7ee7-106">Des groupes de sécurité réseau peuvent être associés à des sous-réseaux ou à des instances de machine virtuelle au sein de ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="d7ee7-107">Lorsqu’un groupe de sécurité réseau est associé à un sous-réseau, listes de contrôle hello appliquent instances de machine virtuelle tooall hello dans ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-107">When an NSG is associated with a subnet, hello ACL rules apply tooall hello VM instances in that subnet.</span></span> <span data-ttu-id="d7ee7-108">En outre, le trafic tooan machine virtuelle individuelle peut être limité par l’association d’un groupe de sécurité réseau directement toothat machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-108">In addition, traffic tooan individual VM can be restricted further by associating an NSG directly toothat VM.</span></span> <span data-ttu-id="d7ee7-109">Voir toolearn [qu’est un groupe de sécurité réseau (NSG) ?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="d7ee7-109">toolearn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="d7ee7-110">Si vous n’avez pas de groupes de sécurité réseau activés, le centre de sécurité présente deux recommandations tooyou : activer les groupes de sécurité réseau sur les sous-réseaux et activer les groupes de sécurité réseau sur les ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-110">If you do not have NSGs enabled, Security Center presents two recommendations tooyou: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="d7ee7-111">Vous choisissez les niveau, le sous-réseau ou la machine virtuelle, tooapply groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-111">You choose which level, subnet or VM, tooapply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="d7ee7-112">Ce document présente le service de hello à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-112">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="d7ee7-113">Il ne s’agit pas d’un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="d7ee7-114">Implémenter la recommandation de hello</span><span class="sxs-lookup"><span data-stu-id="d7ee7-114">Implement hello recommendation</span></span>
1. <span data-ttu-id="d7ee7-115">Bonjour **recommandations** panneau, sélectionnez **activer les groupes de sécurité réseau** sur des sous-réseaux ou des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-115">In hello **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="d7ee7-116">![Activer des groupes de sécurité réseau][1]</span><span class="sxs-lookup"><span data-stu-id="d7ee7-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="d7ee7-117">Cela ouvre le panneau de hello **configurer des groupes de sécurité réseau manquant** des sous-réseaux ou pour les ordinateurs virtuels, selon la recommandation hello que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-117">This opens hello blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on hello recommendation that you selected.</span></span> <span data-ttu-id="d7ee7-118">Sélectionnez un sous-réseau ou un ordinateur virtuel de tooconfigure un groupe de sécurité réseau sur.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-118">Select a subnet or a virtual machine tooconfigure an NSG on.</span></span>

   ![Configurer un groupe de sécurité réseau pour un sous-réseau][2]

   ![Configurer un groupe de sécurité réseau pour une machine virtuelle][3]
3. <span data-ttu-id="d7ee7-121">Sur hello **choisir un groupe de sécurité réseau** panneau, sélectionnez un groupe de sécurité réseau existant ou **nouvel** toocreate un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-121">On hello **Choose network security group** blade, select an existing NSG or select **Create new** toocreate an NSG.</span></span>

   ![Choisir un groupe de sécurité réseau][4]

<span data-ttu-id="d7ee7-123">Si vous créez un groupe de sécurité réseau, suivez les étapes de hello dans [comment toomanage groupes de sécurité réseau à l’aide de hello portail Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate un groupe de sécurité réseau et de définir des règles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-123">If you create an NSG, follow hello steps in [How toomanage NSGs using hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="d7ee7-124">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d7ee7-124">See also</span></span>
<span data-ttu-id="d7ee7-125">Cet article vous a montré comment tooimplement hello centre de sécurité recommandation « activer les groupes de sécurité réseau » pour les sous-réseaux ou les ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-125">This article showed you how tooimplement hello Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="d7ee7-126">toolearn savoir plus sur l’activation des groupes de sécurité réseau, voir hello :</span><span class="sxs-lookup"><span data-stu-id="d7ee7-126">toolearn more about enabling NSGs, see hello following:</span></span>

* [<span data-ttu-id="d7ee7-127">Présentation du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="d7ee7-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="d7ee7-128">Comment les groupes de sécurité réseau toomanage à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d7ee7-128">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="d7ee7-129">toolearn en savoir plus sur le centre de sécurité, voir hello :</span><span class="sxs-lookup"><span data-stu-id="d7ee7-129">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="d7ee7-130">[Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="d7ee7-131">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="d7ee7-132">[Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="d7ee7-133">[Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="d7ee7-134">[Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="d7ee7-135">[Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="d7ee7-136">[Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) --obtenir les dernières informations de sécurité Azure hello et informations.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
