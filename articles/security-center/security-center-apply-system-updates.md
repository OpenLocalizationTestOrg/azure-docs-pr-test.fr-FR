---
title: "Appliquer les mises à jour système dans Azure Security Center | Microsoft Docs"
description: "Ce document vous montre comment implémenter les recommandations d’Azure Security Center **Appliquer les mises à jour système** et **Redémarrer après l’application des mises à jour système**."
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
ms.openlocfilehash: 50cdea437db5387813c6a3905d14b6904d2aba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="9eed2-103">Appliquer les mises à jour système dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9eed2-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="9eed2-104">Azure Security Center recherche quotidiennement les mises à jour manquantes du système d’exploitation sur les machines virtuelles Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="9eed2-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="9eed2-105">Security Center récupère une liste des mises à jour de sécurité et critiques disponibles dans Windows Update ou WSUS (Windows Server Update Services), selon le service configuré sur les machines virtuelles Windows.</span><span class="sxs-lookup"><span data-stu-id="9eed2-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="9eed2-106">Security Center recherche également les dernières mises à jour dans les systèmes Linux.</span><span class="sxs-lookup"><span data-stu-id="9eed2-106">Security Center also checks for the latest updates in Linux systems.</span></span> <span data-ttu-id="9eed2-107">S’il manque une mise à jour système sur votre machine virtuelle, Security Center vous recommande de l’appliquer.</span><span class="sxs-lookup"><span data-stu-id="9eed2-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="9eed2-108">Ce document présente le service à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="9eed2-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="9eed2-109">Il ne s’agit pas d’un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="9eed2-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="9eed2-110">Implémenter la recommandation</span><span class="sxs-lookup"><span data-stu-id="9eed2-110">Implement the recommendation</span></span>
1. <span data-ttu-id="9eed2-111">Dans le panneau **Recommandations**, sélectionnez **Appliquer les mises à jour système**.</span><span class="sxs-lookup"><span data-stu-id="9eed2-111">In the **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Appliquer des mises à jour système][1]
2. <span data-ttu-id="9eed2-113">Le panneau **Appliquer les mises à jour système** s’ouvre en affichant une liste des mises à jour système manquantes sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9eed2-113">The **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="9eed2-114">Sélectionnez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9eed2-114">Select a VM.</span></span>

   ![Sélectionner une machine virtuelle][2]
3. <span data-ttu-id="9eed2-116">Un panneau s’ouvre et affiche une liste des mises à jour manquantes sur cette machine.</span><span class="sxs-lookup"><span data-stu-id="9eed2-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="9eed2-117">Sélectionnez une mise à jour système.</span><span class="sxs-lookup"><span data-stu-id="9eed2-117">Select a system update.</span></span> <span data-ttu-id="9eed2-118">Dans cet exemple, sélectionnons KB3156016.</span><span class="sxs-lookup"><span data-stu-id="9eed2-118">In this example, let’s select KB3156016.</span></span>

   ![Mises à jour de sécurité manquantes][3]

4. <span data-ttu-id="9eed2-120">Suivez les étapes du panneau **Mise à jour de sécurité** pour appliquer la mise à jour manquante.</span><span class="sxs-lookup"><span data-stu-id="9eed2-120">Follow the steps in the **Security Update** blade to apply the missing update.</span></span>

   ![Mise à jour de sécurité][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="9eed2-122">Redémarrer après l’application des mises à jour système</span><span class="sxs-lookup"><span data-stu-id="9eed2-122">Reboot after system updates</span></span>
1. <span data-ttu-id="9eed2-123">Retournons au panneau **Recommandations** .</span><span class="sxs-lookup"><span data-stu-id="9eed2-123">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="9eed2-124">Une fois que vous avez appliqué les mises à jour système, une nouvelle entrée est générée, appelée **Redémarrer après l’application des mises à jour système**.</span><span class="sxs-lookup"><span data-stu-id="9eed2-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="9eed2-125">Cette entrée vous permet de savoir que vous devez redémarrer la machine virtuelle pour terminer le processus d’application des mises à jour système.</span><span class="sxs-lookup"><span data-stu-id="9eed2-125">This entry lets you know that you need to reboot the VM to complete the process of applying system updates.</span></span>

   ![Redémarrer après l’application des mises à jour système][5]
2. <span data-ttu-id="9eed2-127">Sélectionnez **Redémarrer après l’application des mises à jour système**.</span><span class="sxs-lookup"><span data-stu-id="9eed2-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="9eed2-128">Cette opération ouvre le panneau **Un redémarrage est en attente pour terminer les mises à jour système** qui affiche une liste de machines virtuelles que vous devez redémarrer pour terminer le processus d’application des mises à jour système.</span><span class="sxs-lookup"><span data-stu-id="9eed2-128">This opens **A restart is pending to complete system updates** blade displaying a list of VMs that you need to restart to complete the apply system updates process.</span></span>

   ![Redémarrage en attente][6]

<span data-ttu-id="9eed2-130">Redémarrez la machine virtuelle à partir d’Azure pour terminer le processus.</span><span class="sxs-lookup"><span data-stu-id="9eed2-130">Restart the VM from Azure to complete the process.</span></span>

## <a name="see-also"></a><span data-ttu-id="9eed2-131">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9eed2-131">See also</span></span>
<span data-ttu-id="9eed2-132">Pour plus d’informations sur le Centre de sécurité, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="9eed2-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="9eed2-133">[Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md) : découvrez comment configurer des stratégies de sécurité pour vos groupes de ressources et abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="9eed2-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="9eed2-134">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9eed2-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="9eed2-135">[Surveillance de l’intégrité de la sécurité dans Azure Security Center](security-center-monitoring.md) : découvrez comment surveiller l’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9eed2-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="9eed2-136">[Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="9eed2-136">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="9eed2-137">[Surveillance des solutions partenaires avec Azure Security Center](security-center-partner-solutions.md) : découvrez comment surveiller l’état d’intégrité de vos solutions partenaires.</span><span class="sxs-lookup"><span data-stu-id="9eed2-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="9eed2-138">[FAQ Azure Security Center](security-center-faq.md) : forum aux questions concernant l’utilisation de ce service.</span><span class="sxs-lookup"><span data-stu-id="9eed2-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="9eed2-139">[Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : recherchez des billets de blog sur la sécurité et la conformité Azure.</span><span class="sxs-lookup"><span data-stu-id="9eed2-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
