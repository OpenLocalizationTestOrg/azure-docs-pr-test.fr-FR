---
title: aaaEnable Agent de machine virtuelle dans Azure Security Center | Documents Microsoft
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** activer VM Agent **."
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
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="cc5a9-103">Activer l’agent de machine virtuelle dans le Centre de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="cc5a9-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="cc5a9-104">Hello Agent de machine virtuelle doit être installé sur les machines virtuelles (VM) dans l’ordre trop[activer la collecte des données](security-center-enable-data-collection.md).</span><span class="sxs-lookup"><span data-stu-id="cc5a9-104">hello VM Agent must be installed on virtual machines (VMs) in order too[enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="cc5a9-105">Permet de centre de sécurité Azure toosee qui nécessitent des machines virtuelles hello Agent de machine virtuelle et recommande que vous activez hello Agent de machine virtuelle sur ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-105">Azure Security Center enables you toosee which VMs require hello VM Agent and will recommend that you enable hello VM Agent on those VMs.</span></span>

<span data-ttu-id="cc5a9-106">Hello Agent de machine virtuelle est installé par défaut pour les ordinateurs virtuels qui sont déployés à partir de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-106">hello VM Agent is installed by default for VMs that are deployed from hello Azure Marketplace.</span></span> <span data-ttu-id="cc5a9-107">article de Hello [Agent de machine virtuelle et Extensions-partie 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) fournit des informations sur la façon dont tooinstall hello Agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-107">hello article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how tooinstall hello VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="cc5a9-108">Ce document présente le service de hello à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="cc5a9-109">Il ne s’agit pas d’un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="cc5a9-110">Implémenter la recommandation de hello</span><span class="sxs-lookup"><span data-stu-id="cc5a9-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="cc5a9-111">Bonjour **Panneau de recommandations**, sélectionnez **activer l’Agent de machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-111">In hello **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="cc5a9-112">![Activer l’agent de machine virtuelle][1]</span><span class="sxs-lookup"><span data-stu-id="cc5a9-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="cc5a9-113">Cela ouvre le panneau de hello **VM Agent manquant ou ne répond pas**.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-113">This opens hello blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="cc5a9-114">Ce panneau répertorie les machines virtuelles hello nécessitant hello Agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-114">This blade lists hello VMs that require hello VM Agent.</span></span> <span data-ttu-id="cc5a9-115">Suivez les instructions de hello sur l’agent de machine virtuelle hello panneau tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-115">Follow hello instructions on hello blade tooinstall hello VM agent.</span></span>
   <span data-ttu-id="cc5a9-116">![L’agent de machine virtuelle est manquant][2]</span><span class="sxs-lookup"><span data-stu-id="cc5a9-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="cc5a9-117">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="cc5a9-117">See also</span></span>
<span data-ttu-id="cc5a9-118">toolearn en savoir plus sur le centre de sécurité, voir hello :</span><span class="sxs-lookup"><span data-stu-id="cc5a9-118">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="cc5a9-119">[Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md)--Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="cc5a9-120">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md): découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="cc5a9-121">[Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md)--Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="cc5a9-122">[Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md)--Découvrez comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-122">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="cc5a9-123">[Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="cc5a9-124">[Forum aux questions sur Azure Security Center](security-center-faq.md)--rechercher Forum aux questions sur l’utilisation du service de hello.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="cc5a9-125">[Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/)--obtenir les dernières informations de sécurité Azure hello et informations.</span><span class="sxs-lookup"><span data-stu-id="cc5a9-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
