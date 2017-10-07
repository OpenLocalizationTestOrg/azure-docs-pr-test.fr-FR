---
title: "des vulnérabilités d’aaaRemediate du système d’exploitation dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** corriger le système d’exploitation des vulnérabilités **."
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
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="45e66-103">Corriger les vulnérabilités du système d’exploitation dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="45e66-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="45e66-104">Centre de sécurité Azure analyse tous les jours de votre système d’exploitation de l’ordinateur virtuel (VM) (système d’exploitation) pour les configurations qui pourrait rendre hello VM plus vulnérables tooattack et recommande la configuration change tooaddress ces vulnérabilités.</span><span class="sxs-lookup"><span data-stu-id="45e66-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make hello VM more vulnerable tooattack and recommends configuration changes tooaddress these vulnerabilities.</span></span> <span data-ttu-id="45e66-105">Centre de sécurité vous recommande de résoudre les vulnérabilités lors de la configuration du système d’exploitation de votre machine virtuelle ne correspond pas à des règles de configuration recommandée de hello.</span><span class="sxs-lookup"><span data-stu-id="45e66-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match hello recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="45e66-106">Pour plus d’informations sur les configurations spécifiques hello en cours d’analyse, consultez hello [liste des règles de configuration recommandée](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="45e66-106">For more information on hello specific configurations being monitored, see hello [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="45e66-107">Implémenter la recommandation de hello</span><span class="sxs-lookup"><span data-stu-id="45e66-107">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="45e66-108">Ce document présente le service de hello à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="45e66-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="45e66-109">Ce document n'est pas un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="45e66-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="45e66-110">Bonjour **recommandations** panneau, sélectionnez **les vulnérabilités du système d’exploitation corriger**.</span><span class="sxs-lookup"><span data-stu-id="45e66-110">In hello **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="45e66-111">![Remediate OS vulnerabilities][1]</span><span class="sxs-lookup"><span data-stu-id="45e66-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="45e66-112">Hello **les vulnérabilités du système d’exploitation corriger** panneau s’ouvre et répertorie vos machines virtuelles avec des configurations de système d’exploitation qui ne correspondent pas hello les règles de configuration recommandée.</span><span class="sxs-lookup"><span data-stu-id="45e66-112">hello **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match hello recommended configuration rules.</span></span>  <span data-ttu-id="45e66-113">Pour chaque machine virtuelle, panneau de hello identifie :</span><span class="sxs-lookup"><span data-stu-id="45e66-113">For each VM, hello blade identifies:</span></span>

   * <span data-ttu-id="45e66-114">**Échec de règles** --nombre hello de règles hello configuration de système d’exploitation de l’ordinateur virtuel a échoué.</span><span class="sxs-lookup"><span data-stu-id="45e66-114">**FAILED RULES** -- hello number of rules that hello VM's OS configuration failed.</span></span>
   * <span data-ttu-id="45e66-115">**DERNIÈRE analyse** --hello date et heure que le centre de sécurité analysés dernière configuration de système d’exploitation de la machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="45e66-115">**LAST SCAN TIME** -- hello date and time that Security Center last scanned hello VM’s OS configuration.</span></span>
   * <span data-ttu-id="45e66-116">**ÉTAT** --hello l’état actuel de la vulnérabilité de hello :</span><span class="sxs-lookup"><span data-stu-id="45e66-116">**STATE** -- hello current state of hello vulnerability:</span></span>

     * <span data-ttu-id="45e66-117">Ouvrez : hello vulnérabilité n'a pas été traitée encore</span><span class="sxs-lookup"><span data-stu-id="45e66-117">Open: hello vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="45e66-118">En cours d’exécution : Une vulnérabilité de hello est actuellement appliquée, aucune action n’est requise par vous</span><span class="sxs-lookup"><span data-stu-id="45e66-118">In Progress: hello vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="45e66-119">Résolu : une vulnérabilité de hello a déjà été traitée (lorsque hello a été résolu, entrée de hello est grisée)</span><span class="sxs-lookup"><span data-stu-id="45e66-119">Resolved: hello vulnerability was already addressed (when hello issue has been resolved, hello entry is grayed out)</span></span>
   * <span data-ttu-id="45e66-120">**GRAVITÉ** --toutes les vulnérabilités sont définies à gravité tooa basse, ce qui signifie une vulnérabilité doit être traitée, mais ne nécessite pas une attention immédiate.</span><span class="sxs-lookup"><span data-stu-id="45e66-120">**SEVERITY** -- All vulnerabilities are set tooa severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="45e66-121">Sélectionnez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="45e66-121">Select a VM.</span></span> <span data-ttu-id="45e66-122">Un panneau pour cette machine virtuelle s’ouvre et affiche les règles hello qui ont échoué.</span><span class="sxs-lookup"><span data-stu-id="45e66-122">A blade for that VM opens and displays hello rules that have failed.</span></span>
   <span data-ttu-id="45e66-123">![Règles de configuration ayant échoué][2]</span><span class="sxs-lookup"><span data-stu-id="45e66-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="45e66-124">Sélectionnez une règle.</span><span class="sxs-lookup"><span data-stu-id="45e66-124">Select a rule.</span></span> <span data-ttu-id="45e66-125">Dans cet exemple, nous allons sélectionner **Le mot de passe doit respecter des exigences de complexité**.</span><span class="sxs-lookup"><span data-stu-id="45e66-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="45e66-126">Un panneau s’ouvre décrivant impact de règle et hello hello a échoué.</span><span class="sxs-lookup"><span data-stu-id="45e66-126">A blade opens describing hello failed rule and hello impact.</span></span> <span data-ttu-id="45e66-127">Passez en revue les détails de hello et prendre en compte la façon dont les configurations de système d’exploitation sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="45e66-127">Review hello details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="45e66-128">![Description de la règle d’échec hello][3]</span><span class="sxs-lookup"><span data-stu-id="45e66-128">![Description for hello failed rule][3]</span></span>

  <span data-ttu-id="45e66-129">Centre de sécurité utilise des identificateurs uniques de tooassign énumération CCE (Common Configuration) pour les règles de configuration.</span><span class="sxs-lookup"><span data-stu-id="45e66-129">Security Center uses Common Configuration Enumeration (CCE) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="45e66-130">Hello informations suivantes est fournie sur ce panneau :</span><span class="sxs-lookup"><span data-stu-id="45e66-130">hello following information is provided on this blade:</span></span>

  - <span data-ttu-id="45e66-131">NOM : nom de règle</span><span class="sxs-lookup"><span data-stu-id="45e66-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="45e66-132">GRAVITÉ : valeur de gravité CCE (critique, important ou avertissement)</span><span class="sxs-lookup"><span data-stu-id="45e66-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="45e66-133">CCIED--Identificateur unique de CCE pour la règle de hello</span><span class="sxs-lookup"><span data-stu-id="45e66-133">CCIED -- CCE unique identifier for hello rule</span></span>
  - <span data-ttu-id="45e66-134">DESCRIPTION : description de la règle</span><span class="sxs-lookup"><span data-stu-id="45e66-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="45e66-135">VULNÉRABILITÉ : explication de la vulnérabilité ou du risque si la règle n’est pas appliquée</span><span class="sxs-lookup"><span data-stu-id="45e66-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="45e66-136">IMPACT : impact sur l’activité lorsque la règle est appliquée</span><span class="sxs-lookup"><span data-stu-id="45e66-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="45e66-137">VALEUR attendue : Valeur de prévu lorsque le centre de sécurité analyse la configuration de votre système d’exploitation de la machine virtuelle par rapport à la règle de hello</span><span class="sxs-lookup"><span data-stu-id="45e66-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="45e66-138">OPÉRATION de règle : Des règles utilisées par le centre de sécurité lors de l’analyse de configuration de votre système d’exploitation de la machine virtuelle par rapport à la règle de hello</span><span class="sxs-lookup"><span data-stu-id="45e66-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="45e66-139">VALEUR réelle : La valeur retournée après l’analyse de configuration de votre système d’exploitation de la machine virtuelle par rapport à la règle de hello</span><span class="sxs-lookup"><span data-stu-id="45e66-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="45e66-140">RÉSULTAT DE L’ÉVALUATION : résultat de l’analyse : réussite ou échec</span><span class="sxs-lookup"><span data-stu-id="45e66-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="45e66-141">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="45e66-141">See also</span></span>
<span data-ttu-id="45e66-142">Cet article vous a montré comment tooimplement hello centre de sécurité « vulnérabilités de correction du système d’exploitation » de recommandation.</span><span class="sxs-lookup"><span data-stu-id="45e66-142">This article showed you how tooimplement hello Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="45e66-143">Vous pouvez consulter le jeu de hello des règles de configuration [ici](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="45e66-143">You can review hello set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="45e66-144">Centre de sécurité utilise des identificateurs uniques de tooassign CCE (Common Configuration Enumeration) pour les règles de configuration.</span><span class="sxs-lookup"><span data-stu-id="45e66-144">Security Center uses CCE (Common Configuration Enumeration) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="45e66-145">Visitez hello [CCE](https://nvd.nist.gov/cce/index.cfm) site pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="45e66-145">Visit hello [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="45e66-146">toolearn en savoir plus sur le centre de sécurité, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="45e66-146">toolearn more about Security Center, see hello following resources:</span></span>

* <span data-ttu-id="45e66-147">[Plateformes prises en charge dans Azure Security Center](security-center-os-coverage.md) : répertorie les machines virtuelles Windows et Linux prises en charge.</span><span class="sxs-lookup"><span data-stu-id="45e66-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="45e66-148">[Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) -en savoir comment les stratégies de sécurité tooconfigure pour vos abonnements Azure et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="45e66-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="45e66-149">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="45e66-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="45e66-150">[Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) -en savoir comment toomonitor hello d’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="45e66-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="45e66-151">[Gestion et répond toosecurity alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) -en savoir comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="45e66-151">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="45e66-152">[Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) -en savoir comment toomonitor hello état d’intégrité de vos solutions de partenaire.</span><span class="sxs-lookup"><span data-stu-id="45e66-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="45e66-153">[Forum aux questions sur Azure Security Center](security-center-faq.md) -Forum aux questions sur l’utilisation hello service de recherche.</span><span class="sxs-lookup"><span data-stu-id="45e66-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="45e66-154">[Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.</span><span class="sxs-lookup"><span data-stu-id="45e66-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
