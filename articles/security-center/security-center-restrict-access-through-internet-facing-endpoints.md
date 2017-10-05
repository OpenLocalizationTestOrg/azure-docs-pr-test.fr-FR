---
title: "Limiter l’accès par le biais d’un point de terminaison accessible sur Internet dans Azure Security Center | Microsoft Docs"
description: "Ce document vous montre comment implémenter la recommandation du Centre de sécurité Azure **Restreindre l’accès via un point de terminaison accessible sur Internet**."
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
ms.openlocfilehash: f7309c617f1705205e2c9f1b1b48d141391d45da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="9dbdb-103">Restreindre l’accès via des points de terminaison accessibles sur Internet dans le Centre de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="9dbdb-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="9dbdb-104">Le Centre de sécurité Azure vous recommande de restreindre l’accès via les points de terminaison accessibles sur Internet si l’un de vos groupes de sécurité réseau (NSG) possède une ou plusieurs règles de trafic entrant autorisant l’accès à partir de « n’importe quelle » adresse IP source.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="9dbdb-105">Un accès « total » peut permettre aux pirates d’accéder à vos ressources.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-105">Opening access to “any” may enable attackers to access your resources.</span></span> <span data-ttu-id="9dbdb-106">Le Centre de sécurité vous recommande de modifier ces règles de trafic entrant afin de restreindre l’accès aux adresses IP source qui en ont réellement besoin.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-106">Security Center will recommend that you edit these inbound rules to restrict access to source IP addresses that actually need access.</span></span>

<span data-ttu-id="9dbdb-107">Cette recommandation est générée pour n’importe quel port non web avec une « quelconque » source.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="9dbdb-108">Ce document présente le service à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="9dbdb-109">Il ne s’agit pas d’un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="9dbdb-110">Implémenter la recommandation</span><span class="sxs-lookup"><span data-stu-id="9dbdb-110">Implement the recommendation</span></span>
1. <span data-ttu-id="9dbdb-111">Dans le panneau **Recommandations**, sélectionnez **Limiter l'accès par le biais d'un point de terminaison accessible sur Internet**.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-111">In the **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![Restreindre l’accès via un point de terminaison accessible sur Internet][1]
2. <span data-ttu-id="9dbdb-113">Le panneau **Restreindre l’accès via un point de terminaison accessible sur Internet**s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-113">This opens the blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="9dbdb-114">Ce panneau répertorie les machines virtuelles dont les règles de trafic entrant créent un problème de sécurité potentiel.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-114">This blade lists the virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="9dbdb-115">Sélectionnez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-115">Select a VM.</span></span>

   ![Sélectionner une machine virtuelle][2]
3. <span data-ttu-id="9dbdb-117">Le panneau **NSG** affiche des informations sur le groupe de sécurité réseau (NSG), les règles de trafic entrant associées ainsi que la machine virtuelle associée.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-117">The **NSG** blade displays Network Security Group information, related inbound rules, and the associated VM.</span></span> <span data-ttu-id="9dbdb-118">Sélectionnez **Modifier les règles de trafic entrant** pour poursuivre la modification d’une règle de trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-118">Select **Edit inbound rules** to proceed with editing an inbound rule.</span></span>

   ![Panneau Groupe de sécurité réseau][3]
4. <span data-ttu-id="9dbdb-120">Dans le panneau **Règles de sécurité entrantes** , sélectionnez la règle de trafic entrant à modifier.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-120">On the **Inbound security rules** blade select the inbound rule to edit.</span></span> <span data-ttu-id="9dbdb-121">Dans cet exemple, sélectionnons **AllowWeb**.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Règles de sécurité de trafic entrant][4]

   <span data-ttu-id="9dbdb-123">Notez que vous pouvez également sélectionner **Règles par défaut** pour afficher l’ensemble de règles par défaut de tous les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-123">Note, you can also select **Default rules** to see the set of default rules contained by all NSGs.</span></span> <span data-ttu-id="9dbdb-124">Les règles par défaut ne peuvent pas être supprimées, mais comme une priorité plus basse leur est attribuée, elles peuvent être remplacées par les règles que vous créez.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-124">The default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by the rules that you create.</span></span> <span data-ttu-id="9dbdb-125">En savoir plus sur les [règles par défaut](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="9dbdb-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Règles par défaut][5]
5. <span data-ttu-id="9dbdb-127">Dans le panneau **AllowWeb**, modifiez les propriétés de la règle de trafic entrant pour que la valeur **Source** affiche une adresse IP ou un bloc d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-127">On the **AllowWeb** blade, edit the properties of the inbound rule so that the **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="9dbdb-128">Pour en savoir plus sur les propriétés de la règle de trafic entrant, consultez [Règles de groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="9dbdb-128">To learn more about the properties of the inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Modifier une règle de trafic entrant][6]

## <a name="see-also"></a><span data-ttu-id="9dbdb-130">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9dbdb-130">See also</span></span>
<span data-ttu-id="9dbdb-131">Cet article vous a montré comment implémenter la recommandation du Centre de sécurité Azure « Restreindre l’accès via un point de terminaison accessible sur Internet ».</span><span class="sxs-lookup"><span data-stu-id="9dbdb-131">This article showed you how to implement the Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="9dbdb-132">Pour plus d’informations sur l’activation de groupes de sécurité et de règles, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="9dbdb-132">To learn more about enabling NSGs and rules, see the following:</span></span>

* [<span data-ttu-id="9dbdb-133">Présentation du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="9dbdb-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="9dbdb-134">Gestion des groupes de sécurité réseau à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="9dbdb-134">How to manage NSGs using the Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="9dbdb-135">Pour plus d’informations sur Security Center, consultez :</span><span class="sxs-lookup"><span data-stu-id="9dbdb-135">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="9dbdb-136">[Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md): découvrez comment configurer des stratégies de sécurité pour vos groupes de ressources et abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="9dbdb-137">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md): découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="9dbdb-138">[Surveillance de l’intégrité de la sécurité dans le Centre de sécurité Azure](security-center-monitoring.md): découvrez comment surveiller l’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="9dbdb-139">[Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md): découvrez comment gérer et résoudre les alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-139">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="9dbdb-140">[Surveillance des solutions de partenaires avec Azure Security Center](security-center-partner-solutions.md) : découvrez comment surveiller l’état d’intégrité de vos solutions de partenaires.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="9dbdb-141">[FAQ du Centre de sécurité Azure](security-center-faq.md): forum aux questions concernant l’utilisation de ce service.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="9dbdb-142">[Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/): découvrez les dernières nouvelles et informations sur la sécurité Azure.</span><span class="sxs-lookup"><span data-stu-id="9dbdb-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
