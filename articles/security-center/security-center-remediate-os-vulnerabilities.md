---
title: "Corriger les vulnérabilités du système d’exploitation dans Azure Security Center | Microsoft Docs"
description: "Ce document vous montre comment implémenter la recommandation Azure Security Center **Remediate OS vulnerabilities** (Corriger les vulnérabilités du système d’exploitation)."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: e6b251d5b97c57b3b6f79d14e53fbed5ca37ecb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="50904-103">Corriger les vulnérabilités du système d’exploitation dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="50904-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="50904-104">Azure Security Center analyse quotidiennement le système d’exploitation de votre machine virtuelle afin d’identifier les configurations susceptibles de rendre la machine virtuelle plus vulnérable aux attaques, et recommande des changements de configuration visant à résoudre ces problèmes.</span><span class="sxs-lookup"><span data-stu-id="50904-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make the VM more vulnerable to attack and recommends configuration changes to address these vulnerabilities.</span></span> <span data-ttu-id="50904-105">Security Center vous recommande de résoudre les vulnérabilités lorsque la configuration du système d’exploitation de votre machine virtuelle ne correspond pas aux règles de configuration recommandées.</span><span class="sxs-lookup"><span data-stu-id="50904-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match the recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="50904-106">Consultez la [liste des règles de configuration recommandées](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335) pour plus d’informations sur les configurations surveillées.</span><span class="sxs-lookup"><span data-stu-id="50904-106">For more information on the specific configurations being monitored, see the [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="50904-107">Implémenter la recommandation</span><span class="sxs-lookup"><span data-stu-id="50904-107">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="50904-108">Ce document présente le service à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="50904-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="50904-109">Ce document n’est pas un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="50904-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="50904-110">Dans le panneau **Recommandations**, sélectionnez **Corriger les vulnérabilités du système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="50904-110">In the **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="50904-111">![Corriger des vulnérabilités du système d’exploitation][1]</span><span class="sxs-lookup"><span data-stu-id="50904-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="50904-112">Le panneau **Corriger des vulnérabilités du système d’exploitation** s’ouvre et répertorie vos machines virtuelles dont les configurations de système d’exploitation ne correspondent pas aux règles de configuration recommandées.</span><span class="sxs-lookup"><span data-stu-id="50904-112">The **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match the recommended configuration rules.</span></span>  <span data-ttu-id="50904-113">Pour chaque machine virtuelle, le panneau identifie les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="50904-113">For each VM, the blade identifies:</span></span>

   * <span data-ttu-id="50904-114">**RÈGLES AYANT ÉCHOUÉ** : nombre de règles non respectées par la configuration du système d’exploitation de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="50904-114">**FAILED RULES** -- The number of rules that the VM's OS configuration failed.</span></span>
   * <span data-ttu-id="50904-115">**HEURE DE LA DERNIÈRE ANALYSE** : date et heure de la dernière analyse de la configuration du système d’exploitation de la machine virtuelle par Security Center.</span><span class="sxs-lookup"><span data-stu-id="50904-115">**LAST SCAN TIME** -- The date and time that Security Center last scanned the VM’s OS configuration.</span></span>
   * <span data-ttu-id="50904-116">**ÉTAT** : état actuel de la vulnérabilité :</span><span class="sxs-lookup"><span data-stu-id="50904-116">**STATE** -- The current state of the vulnerability:</span></span>

     * <span data-ttu-id="50904-117">Ouverte : la recommandation n’a pas encore été corrigée</span><span class="sxs-lookup"><span data-stu-id="50904-117">Open: The vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="50904-118">En cours : la vulnérabilité est en cours de résolution, aucune action de votre part n’est nécessaire</span><span class="sxs-lookup"><span data-stu-id="50904-118">In Progress: The vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="50904-119">Résolue : l’application a déjà été corrigée (une fois le problème résolu, la ligne est grisée)</span><span class="sxs-lookup"><span data-stu-id="50904-119">Resolved: The vulnerability was already addressed (when the issue has been resolved, the entry is grayed out)</span></span>
   * <span data-ttu-id="50904-120">**GRAVITÉ** : toutes les vulnérabilités sont définies à un niveau de gravité faible, ce qui signifie qu’une vulnérabilité doit être traitée, mais qu’elle ne nécessite pas une attention immédiate.</span><span class="sxs-lookup"><span data-stu-id="50904-120">**SEVERITY** -- All vulnerabilities are set to a severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="50904-121">Sélectionnez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="50904-121">Select a VM.</span></span> <span data-ttu-id="50904-122">Un panneau de cette machine virtuelle s’ouvre et affiche les règles qui ont échoué.</span><span class="sxs-lookup"><span data-stu-id="50904-122">A blade for that VM opens and displays the rules that have failed.</span></span>
   <span data-ttu-id="50904-123">![Règles de configuration ayant échoué][2]</span><span class="sxs-lookup"><span data-stu-id="50904-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="50904-124">Sélectionnez une règle.</span><span class="sxs-lookup"><span data-stu-id="50904-124">Select a rule.</span></span> <span data-ttu-id="50904-125">Dans cet exemple, nous allons sélectionner **Le mot de passe doit respecter des exigences de complexité**.</span><span class="sxs-lookup"><span data-stu-id="50904-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="50904-126">La règle ayant échoué ainsi que son impact s’affichent alors dans un nouveau panneau.</span><span class="sxs-lookup"><span data-stu-id="50904-126">A blade opens describing the failed rule and the impact.</span></span> <span data-ttu-id="50904-127">Passez en revue les informations du panneau et déterminez comment les configurations de système d’exploitation sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="50904-127">Review the details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="50904-128">![Description de la règle ayant échoué][3]</span><span class="sxs-lookup"><span data-stu-id="50904-128">![Description for the failed rule][3]</span></span>

  <span data-ttu-id="50904-129">Security Center utilise CCE (Common Configuration Enumeration) pour affecter des identificateurs uniques pour les règles de configuration.</span><span class="sxs-lookup"><span data-stu-id="50904-129">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="50904-130">Ce panneau contient les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="50904-130">The following information is provided on this blade:</span></span>

  - <span data-ttu-id="50904-131">NOM : nom de règle</span><span class="sxs-lookup"><span data-stu-id="50904-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="50904-132">GRAVITÉ : valeur de gravité CCE (critique, important ou avertissement)</span><span class="sxs-lookup"><span data-stu-id="50904-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="50904-133">CCIED : identificateur unique CCE pour la règle</span><span class="sxs-lookup"><span data-stu-id="50904-133">CCIED -- CCE unique identifier for the rule</span></span>
  - <span data-ttu-id="50904-134">DESCRIPTION : description de la règle</span><span class="sxs-lookup"><span data-stu-id="50904-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="50904-135">VULNÉRABILITÉ : explication de la vulnérabilité ou du risque si la règle n’est pas appliquée</span><span class="sxs-lookup"><span data-stu-id="50904-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="50904-136">IMPACT : impact sur l’activité lorsque la règle est appliquée</span><span class="sxs-lookup"><span data-stu-id="50904-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="50904-137">VALEUR ATTENDUE : valeur attendue lorsque Security Center analyse la configuration du système d’exploitation de votre machine virtuelle par rapport à la règle</span><span class="sxs-lookup"><span data-stu-id="50904-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="50904-138">OPÉRATION DE LA RÈGLE : opération de règle utilisée par Security Center lors de l’analyse de la configuration du système d’exploitation de votre machine virtuelle par rapport à la règle</span><span class="sxs-lookup"><span data-stu-id="50904-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="50904-139">VALEUR RÉELLE : valeur retournée après analyse de la configuration du système d’exploitation de votre machine virtuelle par rapport à la règle</span><span class="sxs-lookup"><span data-stu-id="50904-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="50904-140">RÉSULTAT DE L’ÉVALUATION : résultat de l’analyse : réussite ou échec</span><span class="sxs-lookup"><span data-stu-id="50904-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="50904-141">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="50904-141">See also</span></span>
<span data-ttu-id="50904-142">Cet article vous a montré comment implémenter la recommandation de Security Center « Corriger les vulnérabilités du système d’exploitation ».</span><span class="sxs-lookup"><span data-stu-id="50904-142">This article showed you how to implement the Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="50904-143">Vous pouvez consulter l’ensemble des règles de configuration [ici](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="50904-143">You can review the set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="50904-144">Security Center utilise CCE (Common Configuration Enumeration) pour affecter des identificateurs uniques pour les règles de configuration.</span><span class="sxs-lookup"><span data-stu-id="50904-144">Security Center uses CCE (Common Configuration Enumeration) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="50904-145">Visitez le site [CCE](https://nvd.nist.gov/cce/index.cfm) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="50904-145">Visit the [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="50904-146">Pour plus d’informations sur Security Center, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="50904-146">To learn more about Security Center, see the following resources:</span></span>

* <span data-ttu-id="50904-147">[Plateformes prises en charge dans Azure Security Center](security-center-os-coverage.md) : répertorie les machines virtuelles Windows et Linux prises en charge.</span><span class="sxs-lookup"><span data-stu-id="50904-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="50904-148">[Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md) : découvrez comment configurer des stratégies de sécurité pour vos groupes de ressources et abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="50904-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="50904-149">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="50904-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="50904-150">[Surveillance de l’intégrité de la sécurité dans Azure Security Center](security-center-monitoring.md) : découvrez comment surveiller l’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="50904-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="50904-151">[Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="50904-151">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="50904-152">[Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) : découvrez comment surveiller l’état d’intégrité de vos solutions de partenaire.</span><span class="sxs-lookup"><span data-stu-id="50904-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="50904-153">[FAQ Azure Security Center](security-center-faq.md) : forum aux questions concernant l’utilisation de ce service.</span><span class="sxs-lookup"><span data-stu-id="50904-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="50904-154">[Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.</span><span class="sxs-lookup"><span data-stu-id="50904-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
