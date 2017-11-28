---
title: "Installation d’Endpoint Protection dans Azure Security Center | Microsoft Docs"
description: "Ce document vous montre comment implémenter la recommandation d’Azure Security Center **Installer Endpoint Protection**."
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
ms.openlocfilehash: efb86a0ae362c30a6772c391a499154b7ae2a697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="d47c7-103">Installer Endpoint Protection dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="d47c7-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="d47c7-104">Azure Security Center recommande d’installer Endpoint Protection sur vos machines virtuelles Azure si cette dernière n’est pas déjà activée.</span><span class="sxs-lookup"><span data-stu-id="d47c7-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="d47c7-105">Cette recommandation s'applique uniquement aux machines virtuelles Windows.</span><span class="sxs-lookup"><span data-stu-id="d47c7-105">This recommendation applies to Windows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="d47c7-106">Cet exemple de déploiement utilise Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="d47c7-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="d47c7-107">Consultez [Intégration des partenaires dans Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) pour obtenir la liste des partenaires intégrés dans Security Center.</span><span class="sxs-lookup"><span data-stu-id="d47c7-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="d47c7-108">Implémenter la recommandation</span><span class="sxs-lookup"><span data-stu-id="d47c7-108">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="d47c7-109">Ce document présente le service à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="d47c7-109">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="d47c7-110">Ce document n’est pas un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="d47c7-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="d47c7-111">Dans le panneau **Recommandations**, sélectionnez **Installer Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="d47c7-111">In the **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="d47c7-112">![Sélectionner Installer Endpoint Protection][1]</span><span class="sxs-lookup"><span data-stu-id="d47c7-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="d47c7-113">Le panneau **Installer Endpoint Protection** s’ouvre en affichant une liste de machines virtuelles dépourvues de protection des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d47c7-113">The **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="d47c7-114">Dans cette liste, sélectionnez les machines virtuelles sur lesquelles vous souhaitez installer Endpoint Protection et cliquez sur **Installer sur les machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="d47c7-114">Select from the list the VMs that you want to install endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="d47c7-115">![Sélectionner les machines virtuelles sur lesquelles installer Endpoint Protection][2]</span><span class="sxs-lookup"><span data-stu-id="d47c7-115">![Select VMs to install Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="d47c7-116">Le panneau **Sélectionner Endpoint Protection** s’ouvre et vous permet de sélectionner la solution Endpoint Protection de votre choix.</span><span class="sxs-lookup"><span data-stu-id="d47c7-116">The **Select Endpoint Protection** blade opens to allow you to select the endpoint protection solution you want to use.</span></span> <span data-ttu-id="d47c7-117">Dans cet exemple, nous allons sélectionner **Microsoft Antimalware**.</span><span class="sxs-lookup"><span data-stu-id="d47c7-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="d47c7-118">![Sélectionner Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="d47c7-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="d47c7-119">Des informations supplémentaires sur la solution Endpoint Protection s’affichent.</span><span class="sxs-lookup"><span data-stu-id="d47c7-119">Additional information about the endpoint protection solution is displayed.</span></span> <span data-ttu-id="d47c7-120">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d47c7-120">Select **Create**.</span></span>
   <span data-ttu-id="d47c7-121">![Créer une solution anti-programme malveillant][4]</span><span class="sxs-lookup"><span data-stu-id="d47c7-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="d47c7-122">Entrez les paramètres de configuration nécessaires dans le panneau **Ajouter une extension**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="d47c7-122">Enter the required configuration settings on the **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="d47c7-123">Pour en savoir plus sur les paramètres de configuration, consultez [Configuration d’un logiciel anti-programme malveillant par défaut et personnalisée](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="d47c7-123">To learn more about the configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="d47c7-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) est maintenant activé sur les machines virtuelles sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="d47c7-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on the selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="d47c7-125">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d47c7-125">See also</span></span>
<span data-ttu-id="d47c7-126">Cet article vous a montré comment implémenter la recommandation de Security Center « Installer Endpoint Protection ».</span><span class="sxs-lookup"><span data-stu-id="d47c7-126">This article showed you how to implement the Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="d47c7-127">Pour en savoir plus sur l’activation de Microsoft Antimalware dans Azure, consultez le document suivant :</span><span class="sxs-lookup"><span data-stu-id="d47c7-127">To learn more about enabling Microsoft Antimalware in Azure, see the following document:</span></span>

* <span data-ttu-id="d47c7-128">[Microsoft Antimalware pour Azure Cloud Services et les machines virtuelles](../security/azure-security-antimalware.md) : découvrez comment déployer Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="d47c7-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how to deploy Microsoft Antimalware.</span></span>

<span data-ttu-id="d47c7-129">Pour plus d’informations sur Security Center, consultez les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="d47c7-129">To learn more about Security Center, see the following documents:</span></span>

* <span data-ttu-id="d47c7-130">[Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md) : découvrez comment configurer des stratégies de sécurité.</span><span class="sxs-lookup"><span data-stu-id="d47c7-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="d47c7-131">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d47c7-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="d47c7-132">[Surveillance de l’intégrité de la sécurité dans Azure Security Center](security-center-monitoring.md) : découvrez comment surveiller l’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d47c7-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="d47c7-133">[Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="d47c7-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="d47c7-134">[Surveillance des solutions partenaires avec Azure Security Center](security-center-partner-solutions.md) : découvrez comment surveiller l’état d’intégrité de vos solutions partenaires.</span><span class="sxs-lookup"><span data-stu-id="d47c7-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="d47c7-135">[FAQ Azure Security Center](security-center-faq.md) : forum aux questions concernant l’utilisation de ce service.</span><span class="sxs-lookup"><span data-stu-id="d47c7-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="d47c7-136">[Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : recherchez des billets de blog sur la sécurité et la conformité Azure.</span><span class="sxs-lookup"><span data-stu-id="d47c7-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
