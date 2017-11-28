---
title: "accès aaaRestrict via des points de terminaison exposés à Internet dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** restreindre l’accès via Internet exposés au point de terminaison **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="d3ef4-103">Restreindre l’accès via des points de terminaison accessibles sur Internet dans le Centre de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="d3ef4-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="d3ef4-104">Le Centre de sécurité Azure vous recommande de restreindre l’accès via les points de terminaison accessibles sur Internet si l’un de vos groupes de sécurité réseau (NSG) possède une ou plusieurs règles de trafic entrant autorisant l’accès à partir de « n’importe quelle » adresse IP source.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="d3ef4-105">Ouverture d’accès trop « tout » peut activer des personnes malveillantes tooaccess vos ressources.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-105">Opening access too“any” may enable attackers tooaccess your resources.</span></span> <span data-ttu-id="d3ef4-106">Centre de sécurité seront vous recommandons de modifier ces règles de trafic entrant toorestrict accès toosource adresses qui ont réellement besoin d’accéder.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-106">Security Center will recommend that you edit these inbound rules toorestrict access toosource IP addresses that actually need access.</span></span>

<span data-ttu-id="d3ef4-107">Cette recommandation est générée pour n’importe quel port non web avec une « quelconque » source.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="d3ef4-108">Ce document présente le service de hello à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="d3ef4-109">Il ne s’agit pas d’un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="d3ef4-110">Implémenter la recommandation de hello</span><span class="sxs-lookup"><span data-stu-id="d3ef4-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="d3ef4-111">Bonjour **Panneau de recommandations**, sélectionnez **restreindre l’accès via Internet exposés au point de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-111">In hello **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![Restreindre l’accès via un point de terminaison accessible sur Internet][1]
2. <span data-ttu-id="d3ef4-113">Cela ouvre le panneau de hello **restreindre l’accès via Internet exposés au point de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-113">This opens hello blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="d3ef4-114">Ce panneau répertorie hello virtual machines virtuelles avec les règles de trafic entrant qui créent un problème de sécurité potentiel.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-114">This blade lists hello virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="d3ef4-115">Sélectionnez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-115">Select a VM.</span></span>

   ![Sélectionner une machine virtuelle][2]
3. <span data-ttu-id="d3ef4-117">Hello **NSG** panneau affiche des informations de groupe de sécurité réseau, les règles de trafic entrant connexes, et hello associé la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-117">hello **NSG** blade displays Network Security Group information, related inbound rules, and hello associated VM.</span></span> <span data-ttu-id="d3ef4-118">Sélectionnez **modifier les règles de trafic entrant** tooproceed avec la modification d’une règle de trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-118">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span>

   ![Panneau Groupe de sécurité réseau][3]
4. <span data-ttu-id="d3ef4-120">Sur hello **les règles de sécurité de trafic entrant** panneau Sélectionner hello tooedit de règle de trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-120">On hello **Inbound security rules** blade select hello inbound rule tooedit.</span></span> <span data-ttu-id="d3ef4-121">Dans cet exemple, sélectionnons **AllowWeb**.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Règles de sécurité de trafic entrant][4]

   <span data-ttu-id="d3ef4-123">Notez que vous pouvez également sélectionner **règles par défaut** ensemble de hello toosee de règles par défaut contenues dans tous les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-123">Note, you can also select **Default rules** toosee hello set of default rules contained by all NSGs.</span></span> <span data-ttu-id="d3ef4-124">Impossible de supprimer les règles par défaut de Hello mais, car ils sont affectés d’une priorité plus faible, elles peuvent être remplacées par les règles hello que vous créez.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-124">hello default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by hello rules that you create.</span></span> <span data-ttu-id="d3ef4-125">En savoir plus sur les [règles par défaut](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="d3ef4-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Règles par défaut][5]
5. <span data-ttu-id="d3ef4-127">Sur hello **AllowWeb** panneau, modifier des propriétés de règle de trafic entrant hello afin que hello hello **Source** est une adresse IP ou un bloc d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-127">On hello **AllowWeb** blade, edit hello properties of hello inbound rule so that hello **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="d3ef4-128">toolearn savoir plus sur les propriétés hello de règle de trafic entrant hello, consultez [règles du groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="d3ef4-128">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Modifier une règle de trafic entrant][6]

## <a name="see-also"></a><span data-ttu-id="d3ef4-130">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d3ef4-130">See also</span></span>
<span data-ttu-id="d3ef4-131">Cet article vous a montré comment tooimplement hello centre de sécurité recommandation « restreindre l’accès via Internet exposés au point de terminaison. »</span><span class="sxs-lookup"><span data-stu-id="d3ef4-131">This article showed you how tooimplement hello Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="d3ef4-132">toolearn savoir plus sur l’activation des groupes de sécurité réseau et les règles, voir hello :</span><span class="sxs-lookup"><span data-stu-id="d3ef4-132">toolearn more about enabling NSGs and rules, see hello following:</span></span>

* [<span data-ttu-id="d3ef4-133">Présentation du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="d3ef4-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="d3ef4-134">Comment les groupes de sécurité réseau toomanage à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d3ef4-134">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="d3ef4-135">toolearn en savoir plus sur le centre de sécurité, voir hello :</span><span class="sxs-lookup"><span data-stu-id="d3ef4-135">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="d3ef4-136">[Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md)--Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="d3ef4-137">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md): découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="d3ef4-138">[Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md)--Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="d3ef4-139">[Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md)--Découvrez comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-139">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="d3ef4-140">[Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="d3ef4-141">[Forum aux questions sur Azure Security Center](security-center-faq.md)--rechercher Forum aux questions sur l’utilisation du service de hello.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="d3ef4-142">[Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/)--obtenir les dernières informations de sécurité Azure hello et informations.</span><span class="sxs-lookup"><span data-stu-id="d3ef4-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
