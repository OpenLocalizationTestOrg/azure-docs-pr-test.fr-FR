---
title: "mises à jour du système d’aaaApply dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandations du centre de sécurité Azure ** appliquer les mises à jour du système ** et ** redémarrer après l’application de mises à jour du système **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="47501-103">Appliquer les mises à jour système dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="47501-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="47501-104">Azure Security Center recherche quotidiennement les mises à jour manquantes du système d’exploitation sur les machines virtuelles Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="47501-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="47501-105">Security Center récupère une liste des mises à jour de sécurité et critiques disponibles dans Windows Update ou WSUS (Windows Server Update Services), selon le service configuré sur les machines virtuelles Windows.</span><span class="sxs-lookup"><span data-stu-id="47501-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="47501-106">Centre de sécurité vérifie également pour les dernières mises à jour de hello dans les systèmes Linux.</span><span class="sxs-lookup"><span data-stu-id="47501-106">Security Center also checks for hello latest updates in Linux systems.</span></span> <span data-ttu-id="47501-107">S’il manque une mise à jour système sur votre machine virtuelle, Security Center vous recommande de l’appliquer.</span><span class="sxs-lookup"><span data-stu-id="47501-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="47501-108">Ce document présente le service de hello à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="47501-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="47501-109">Il ne s’agit pas d’un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="47501-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="47501-110">Implémenter la recommandation de hello</span><span class="sxs-lookup"><span data-stu-id="47501-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="47501-111">Bonjour **recommandations** panneau, sélectionnez **appliquer les mises à jour système**.</span><span class="sxs-lookup"><span data-stu-id="47501-111">In hello **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Appliquer des mises à jour système][1]
2. <span data-ttu-id="47501-113">Hello **appliquer les mises à jour système** panneau s’ouvre en affichant une liste de mises à jour système manquantes de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="47501-113">hello **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="47501-114">Sélectionnez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="47501-114">Select a VM.</span></span>

   ![Sélectionner une machine virtuelle][2]
3. <span data-ttu-id="47501-116">Un panneau s’ouvre et affiche une liste des mises à jour manquantes sur cette machine.</span><span class="sxs-lookup"><span data-stu-id="47501-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="47501-117">Sélectionnez une mise à jour système.</span><span class="sxs-lookup"><span data-stu-id="47501-117">Select a system update.</span></span> <span data-ttu-id="47501-118">Dans cet exemple, sélectionnons KB3156016.</span><span class="sxs-lookup"><span data-stu-id="47501-118">In this example, let’s select KB3156016.</span></span>

   ![Mises à jour de sécurité manquantes][3]

4. <span data-ttu-id="47501-120">Suivez les étapes de hello Bonjour **mise à jour de sécurité** panneau tooapply hello mise à jour manquante.</span><span class="sxs-lookup"><span data-stu-id="47501-120">Follow hello steps in hello **Security Update** blade tooapply hello missing update.</span></span>

   ![Mise à jour de sécurité][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="47501-122">Redémarrer après l’application des mises à jour système</span><span class="sxs-lookup"><span data-stu-id="47501-122">Reboot after system updates</span></span>
1. <span data-ttu-id="47501-123">Retourner toohello **recommandations** panneau.</span><span class="sxs-lookup"><span data-stu-id="47501-123">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="47501-124">Une fois que vous avez appliqué les mises à jour système, une nouvelle entrée est générée, appelée **Redémarrer après l’application des mises à jour système**.</span><span class="sxs-lookup"><span data-stu-id="47501-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="47501-125">Cette entrée permet de savoir que vous avez besoin de processus de hello toocomplete tooreboot hello machine virtuelle de l’application de mises à jour du système.</span><span class="sxs-lookup"><span data-stu-id="47501-125">This entry lets you know that you need tooreboot hello VM toocomplete hello process of applying system updates.</span></span>

   ![Redémarrer après l’application des mises à jour système][5]
2. <span data-ttu-id="47501-127">Sélectionnez **Redémarrer après l’application des mises à jour système**.</span><span class="sxs-lookup"><span data-stu-id="47501-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="47501-128">Cette opération ouvre **un redémarrage est en attente toocomplete les mises à jour système** panneau affiche la liste des ordinateurs virtuels que vous avez besoin de toorestart toocomplete hello applique le processus de mises à jour du système.</span><span class="sxs-lookup"><span data-stu-id="47501-128">This opens **A restart is pending toocomplete system updates** blade displaying a list of VMs that you need toorestart toocomplete hello apply system updates process.</span></span>

   ![Redémarrage en attente][6]

<span data-ttu-id="47501-130">Redémarrez hello machine virtuelle à partir de processus de hello toocomplete Azure.</span><span class="sxs-lookup"><span data-stu-id="47501-130">Restart hello VM from Azure toocomplete hello process.</span></span>

## <a name="see-also"></a><span data-ttu-id="47501-131">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="47501-131">See also</span></span>
<span data-ttu-id="47501-132">toolearn en savoir plus sur le centre de sécurité, voir hello :</span><span class="sxs-lookup"><span data-stu-id="47501-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="47501-133">[Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="47501-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="47501-134">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="47501-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="47501-135">[Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="47501-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="47501-136">[Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="47501-136">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="47501-137">[Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.</span><span class="sxs-lookup"><span data-stu-id="47501-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="47501-138">[Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.</span><span class="sxs-lookup"><span data-stu-id="47501-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="47501-139">[Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : recherchez des billets de blog sur la sécurité et la conformité Azure.</span><span class="sxs-lookup"><span data-stu-id="47501-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
