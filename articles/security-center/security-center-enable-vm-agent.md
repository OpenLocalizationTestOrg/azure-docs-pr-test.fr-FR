---
title: "Activer l’agent de machine virtuelle dans Azure Security Center | Microsoft Docs"
description: "Ce document vous montre comment implémenter la recommandation du Centre de sécurité Azure **Activer l’agent de machine virtuelle**."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 337a7adfd93c76882a749685702bea6d1524c96a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="9c59b-103">Activer l’agent de machine virtuelle dans le Centre de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="9c59b-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="9c59b-104">L’agent de machine virtuelle doit être installé sur les machines virtuelles pour [activer la collecte des données](security-center-enable-data-collection.md).</span><span class="sxs-lookup"><span data-stu-id="9c59b-104">The VM Agent must be installed on virtual machines (VMs) in order to [enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="9c59b-105">Le Centre de sécurité Azure vous permet de voir quelles machines virtuelles nécessitent l’agent de machine virtuelle et vous recommandera d’activer l’agent sur ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9c59b-105">Azure Security Center enables you to see which VMs require the VM Agent and will recommend that you enable the VM Agent on those VMs.</span></span>

<span data-ttu-id="9c59b-106">L’agent de machine virtuelle est installé par défaut sur les machines virtuelles déployées depuis Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="9c59b-106">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span></span> <span data-ttu-id="9c59b-107">L’article [Installer l’agent de machine virtuelle – Deuxième partie](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) fournit des informations sur l’installation de l’agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9c59b-107">The article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="9c59b-108">Ce document présente le service à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="9c59b-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="9c59b-109">Il ne s’agit pas d’un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="9c59b-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="9c59b-110">Implémenter la recommandation</span><span class="sxs-lookup"><span data-stu-id="9c59b-110">Implement the recommendation</span></span>
1. <span data-ttu-id="9c59b-111">Dans le panneau **Recommandations** , sélectionnez **Activer l’agent de machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="9c59b-111">In the **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="9c59b-112">![Activer l’agent de machine virtuelle][1]</span><span class="sxs-lookup"><span data-stu-id="9c59b-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="9c59b-113">Cette opération ouvre le panneau **L’agent de machine virtuelle est manquant ou ne répond pas**.</span><span class="sxs-lookup"><span data-stu-id="9c59b-113">This opens the blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="9c59b-114">Ce panneau répertorie les machines virtuelles qui nécessitent l’agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9c59b-114">This blade lists the VMs that require the VM Agent.</span></span> <span data-ttu-id="9c59b-115">Suivez les instructions dans le panneau pour installer l’agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9c59b-115">Follow the instructions on the blade to install the VM agent.</span></span>
   <span data-ttu-id="9c59b-116">![L’agent de machine virtuelle est manquant][2]</span><span class="sxs-lookup"><span data-stu-id="9c59b-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="9c59b-117">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9c59b-117">See also</span></span>
<span data-ttu-id="9c59b-118">Pour plus d’informations sur Security Center, consultez :</span><span class="sxs-lookup"><span data-stu-id="9c59b-118">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="9c59b-119">[Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md): découvrez comment configurer des stratégies de sécurité pour vos groupes de ressources et abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="9c59b-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="9c59b-120">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md): découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9c59b-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="9c59b-121">[Surveillance de l’intégrité de la sécurité dans le Centre de sécurité Azure](security-center-monitoring.md): découvrez comment surveiller l’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9c59b-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="9c59b-122">[Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md): découvrez comment gérer et résoudre les alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="9c59b-122">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="9c59b-123">[Surveillance des solutions de partenaires avec Azure Security Center](security-center-partner-solutions.md) : découvrez comment surveiller l’état d’intégrité de vos solutions de partenaires.</span><span class="sxs-lookup"><span data-stu-id="9c59b-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="9c59b-124">[FAQ du Centre de sécurité Azure](security-center-faq.md): forum aux questions concernant l’utilisation de ce service.</span><span class="sxs-lookup"><span data-stu-id="9c59b-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="9c59b-125">[Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/): découvrez les dernières nouvelles et informations sur la sécurité Azure.</span><span class="sxs-lookup"><span data-stu-id="9c59b-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
