---
title: "aaaInstall Endpoint Protection dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** installer Endpoint Protection **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="c29e7-103">Installer Endpoint Protection dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="c29e7-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="c29e7-104">Azure Security Center recommande d’installer Endpoint Protection sur vos machines virtuelles Azure si cette dernière n’est pas déjà activée.</span><span class="sxs-lookup"><span data-stu-id="c29e7-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="c29e7-105">Cette recommandation s’applique tooWindows machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c29e7-105">This recommendation applies tooWindows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="c29e7-106">Cet exemple de déploiement utilise Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="c29e7-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="c29e7-107">Consultez [Intégration des partenaires dans Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) pour obtenir la liste des partenaires intégrés dans Security Center.</span><span class="sxs-lookup"><span data-stu-id="c29e7-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="c29e7-108">Implémenter la recommandation de hello</span><span class="sxs-lookup"><span data-stu-id="c29e7-108">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="c29e7-109">Ce document présente le service de hello à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c29e7-109">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="c29e7-110">Ce document n'est pas un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="c29e7-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="c29e7-111">Bonjour **recommandations** panneau, sélectionnez **installer Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="c29e7-111">In hello **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="c29e7-112">![Sélectionner Installer Endpoint Protection][1]</span><span class="sxs-lookup"><span data-stu-id="c29e7-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="c29e7-113">Hello **installer Endpoint Protection** panneau s’ouvre en affichant une liste d’ordinateurs virtuels sans protection de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="c29e7-113">hello **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="c29e7-114">Sélectionnez hello de liste hello machines virtuelles que vous souhaitez une protection de point de terminaison tooinstall sur et cliquez sur **installer sur des machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="c29e7-114">Select from hello list hello VMs that you want tooinstall endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="c29e7-115">![Sélectionnez les machines virtuelles tooinstall Endpoint Protection sur][2]</span><span class="sxs-lookup"><span data-stu-id="c29e7-115">![Select VMs tooinstall Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="c29e7-116">Hello **sélectionner une Protection de point de terminaison** panneau s’ouvre tooallow vous tooselect hello endpoint protection solution souhaitée toouse.</span><span class="sxs-lookup"><span data-stu-id="c29e7-116">hello **Select Endpoint Protection** blade opens tooallow you tooselect hello endpoint protection solution you want toouse.</span></span> <span data-ttu-id="c29e7-117">Dans cet exemple, nous allons sélectionner **Microsoft Antimalware**.</span><span class="sxs-lookup"><span data-stu-id="c29e7-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="c29e7-118">![Sélectionner Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="c29e7-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="c29e7-119">Des informations supplémentaires sur la solution de protection de point de terminaison hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c29e7-119">Additional information about hello endpoint protection solution is displayed.</span></span> <span data-ttu-id="c29e7-120">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c29e7-120">Select **Create**.</span></span>
   <span data-ttu-id="c29e7-121">![Créer une solution anti-programme malveillant][4]</span><span class="sxs-lookup"><span data-stu-id="c29e7-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="c29e7-122">Entrez les paramètres de configuration hello requis sur hello **Ajout d’une Extension** panneau, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="c29e7-122">Enter hello required configuration settings on hello **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="c29e7-123">toolearn savoir plus sur les paramètres de configuration de hello, consultez [par défaut et la Configuration du logiciel anti-programme malveillant personnalisée](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="c29e7-123">toolearn more about hello configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="c29e7-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) est maintenant actif sur hello sélectionné des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c29e7-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on hello selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="c29e7-125">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c29e7-125">See also</span></span>
<span data-ttu-id="c29e7-126">Cet article vous a montré comment tooimplement hello recommandation du centre de sécurité « Installer Endpoint Protection ».</span><span class="sxs-lookup"><span data-stu-id="c29e7-126">This article showed you how tooimplement hello Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="c29e7-127">toolearn savoir plus sur l’activation de Microsoft Antimalware dans Azure, consultez hello suivant du document :</span><span class="sxs-lookup"><span data-stu-id="c29e7-127">toolearn more about enabling Microsoft Antimalware in Azure, see hello following document:</span></span>

* <span data-ttu-id="c29e7-128">[Microsoft Antimalware pour Services de cloud computing et Machines virtuelles](../security/azure-security-antimalware.md) --Découvrez comment toodeploy Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="c29e7-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how toodeploy Microsoft Antimalware.</span></span>

<span data-ttu-id="c29e7-129">toolearn en savoir plus sur le centre de sécurité, consultez hello suivant des documents :</span><span class="sxs-lookup"><span data-stu-id="c29e7-129">toolearn more about Security Center, see hello following documents:</span></span>

* <span data-ttu-id="c29e7-130">[Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité.</span><span class="sxs-lookup"><span data-stu-id="c29e7-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="c29e7-131">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="c29e7-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c29e7-132">[Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="c29e7-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="c29e7-133">[Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="c29e7-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="c29e7-134">[Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.</span><span class="sxs-lookup"><span data-stu-id="c29e7-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="c29e7-135">[Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.</span><span class="sxs-lookup"><span data-stu-id="c29e7-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="c29e7-136">[Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : recherchez des billets de blog sur la sécurité et la conformité Azure.</span><span class="sxs-lookup"><span data-stu-id="c29e7-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
