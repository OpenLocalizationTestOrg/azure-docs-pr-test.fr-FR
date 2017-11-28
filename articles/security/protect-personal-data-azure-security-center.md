---
title: "Protéger les données personnelles avec Azure Security Center | Microsoft Docs"
description: "protéger les données personnelles à l’aide d’Azure Security Center"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3a941389713a4d3dbffbbfe8a717409927d85c6d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="27eda-103">Protéger les données personnelles contre les violations et attaques : Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="27eda-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="27eda-104">Cet article va vous aider à comprendre comment utiliser Azure Security Center pour protéger les données personnelles contre les violations et attaques.</span><span class="sxs-lookup"><span data-stu-id="27eda-104">This article will help you understand how to use Azure Security Center to protect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="27eda-105">Scénario</span><span class="sxs-lookup"><span data-stu-id="27eda-105">Scenario</span></span> 

<span data-ttu-id="27eda-106">Une importante compagnie de croisière, dont le siège se situe aux États-Unis, étend ses opérations afin de proposer des circuits dans les Mers Méditerranée et Baltique, ainsi que dans les îles Britanniques.</span><span class="sxs-lookup"><span data-stu-id="27eda-106">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="27eda-107">Pour soutenir cet effort, elle a fait l’acquisition de plusieurs lignes de croisière plus petites basées en Italie, en Allemagne, au Danemark et au Royaume-Uni.</span><span class="sxs-lookup"><span data-stu-id="27eda-107">To help in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and the U.K.</span></span>

<span data-ttu-id="27eda-108">La compagnie utilise Microsoft Azure pour stocker les données d’entreprise dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="27eda-108">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="27eda-109">Ces dernières incluent des informations d’identification personnelle telles que les noms, les adresses, les numéros de téléphone et les informations de carte de crédit.</span><span class="sxs-lookup"><span data-stu-id="27eda-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="27eda-110">Des informations de ressources humaines sont également inclues comme :</span><span class="sxs-lookup"><span data-stu-id="27eda-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="27eda-111">Adresses</span><span class="sxs-lookup"><span data-stu-id="27eda-111">Addresses</span></span>
- <span data-ttu-id="27eda-112">Numéros de téléphone</span><span class="sxs-lookup"><span data-stu-id="27eda-112">Phone numbers</span></span>
- <span data-ttu-id="27eda-113">Numéros d’identification fiscale</span><span class="sxs-lookup"><span data-stu-id="27eda-113">Tax identification numbers</span></span>
- <span data-ttu-id="27eda-114">Informations médicales</span><span class="sxs-lookup"><span data-stu-id="27eda-114">Medical information</span></span>

<span data-ttu-id="27eda-115">La ligne de croisière gère également une volumineuse base de données des membres du programme de fidélité et de récompense.</span><span class="sxs-lookup"><span data-stu-id="27eda-115">The cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="27eda-116">Les employés de la compagnie accèdent au réseau à partir de ses agences distantes et les agents de voyage répartis dans le monde entier ont accès à certaines ressources de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="27eda-116">Corporate employees access the network from the company’s remote offices and travel agents located around the world have access to some company resources.</span></span>
<span data-ttu-id="27eda-117">Les données personnelles transitent sur le réseau entre ces emplacements et le centre de données Microsoft.</span><span class="sxs-lookup"><span data-stu-id="27eda-117">Personal data travels across the network between these locations and the Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="27eda-118">Définition du problème</span><span class="sxs-lookup"><span data-stu-id="27eda-118">Problem statement</span></span>

<span data-ttu-id="27eda-119">La compagnie s’inquiète de la menace que constituent les attaques sur ses ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="27eda-119">The company is concerned about the threat of attacks on their Azure resources.</span></span> <span data-ttu-id="27eda-120">Elle souhaite empêcher l’exposition des données personnelles de ses clients et employés à des personnes non autorisées.</span><span class="sxs-lookup"><span data-stu-id="27eda-120">They want to prevent exposure of customers’ and employees’ personal data to unauthorized persons.</span></span> <span data-ttu-id="27eda-121">Elle a besoin de conseils en matière de prévention et de réponse/correction, ainsi que d’un moyen efficace de surveiller en continu la sécurité de ses ressources cloud.</span><span class="sxs-lookup"><span data-stu-id="27eda-121">They want guidance on both prevention and response/remediation, as well as an effective way to monitor the ongoing security of their cloud resources.</span></span>
<span data-ttu-id="27eda-122">Elle nécessite une solide ligne de défense contre les attaques complexes et organisées d’aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="27eda-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="27eda-123">Objectif de l’entreprise</span><span class="sxs-lookup"><span data-stu-id="27eda-123">Company goal</span></span>

<span data-ttu-id="27eda-124">Un des objectifs de la compagnie consiste à assurer la confidentialité des données personnelles des clients et employés en les protégeant contre les menaces.</span><span class="sxs-lookup"><span data-stu-id="27eda-124">One of the company’s goals is to ensure the privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="27eda-125">Un de ses objectifs vise à répondre immédiatement aux signes de violation pour en atténuer l’impact.</span><span class="sxs-lookup"><span data-stu-id="27eda-125">One of their goals is to respond immediately to signs of breach to mitigate the impact.</span></span> <span data-ttu-id="27eda-126">Elle nécessite un moyen d’évaluer l’état actuel de la sécurité, d’identifier les configurations vulnérables et de les corriger.</span><span class="sxs-lookup"><span data-stu-id="27eda-126">It requires a way to assess the current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="27eda-127">Solutions</span><span class="sxs-lookup"><span data-stu-id="27eda-127">Solutions</span></span>

<span data-ttu-id="27eda-128">Microsoft Azure Security Center (ASC) fournit une solution de surveillance de sécurité et de gestion de stratégie intégrée.</span><span class="sxs-lookup"><span data-stu-id="27eda-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="27eda-129">Il offre des fonctionnalités de prévention, de détection et de réponse aux menaces efficaces et faciles à utiliser.</span><span class="sxs-lookup"><span data-stu-id="27eda-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="27eda-130">Prévention</span><span class="sxs-lookup"><span data-stu-id="27eda-130">Prevention</span></span>

<span data-ttu-id="27eda-131">ASC vous permet d’empêcher les violations en vous permettant de définir des stratégies de sécurité, de fournir un accès juste-à-temps et de mettre en œuvre des recommandations de sécurité.</span><span class="sxs-lookup"><span data-stu-id="27eda-131">ASC helps you prevent breaches by enabling you to set security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="27eda-132">Une stratégie de sécurité définit l’ensemble des contrôles recommandés pour les ressources d’un abonnement spécifique.</span><span class="sxs-lookup"><span data-stu-id="27eda-132">A security policy defines the set of controls recommended for resources within the specified subscription.</span></span> <span data-ttu-id="27eda-133">L’accès juste-à-temps permet de bloquer le trafic entrant sur vos machines virtuelles Azure, ce qui réduit l’exposition aux attaques.</span><span class="sxs-lookup"><span data-stu-id="27eda-133">Just in time access can be used to lock down inbound traffic to your Azure VMs, reducing exposure to attacks.</span></span> <span data-ttu-id="27eda-134">Des recommandations de sécurité sont créées par ASC après analyse de l’état de sécurité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="27eda-134">Security recommendations are created by ASC after analyzing the security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="27eda-135">Comment définir des stratégies de sécurité dans ASC ?</span><span class="sxs-lookup"><span data-stu-id="27eda-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="27eda-136">Vous pouvez configurer des stratégies de sécurité pour chaque abonnement.</span><span class="sxs-lookup"><span data-stu-id="27eda-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="27eda-137">Pour modifier une stratégie de sécurité, vous devez avoir le rôle de propriétaire ou de collaborateur pour l’abonnement concerné.</span><span class="sxs-lookup"><span data-stu-id="27eda-137">To modify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="27eda-138">Dans le portail Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="27eda-138">In the Azure portal, do the following:</span></span>

1. <span data-ttu-id="27eda-139">Sélectionnez **Stratégie** dans le tableau de bord ASC.</span><span class="sxs-lookup"><span data-stu-id="27eda-139">Select **Policy** in the ASC dashboard.</span></span>

2. <span data-ttu-id="27eda-140">Sélectionnez l’abonnement sur lequel activer la stratégie.</span><span class="sxs-lookup"><span data-stu-id="27eda-140">Select the subscription on which you want to enable the policy.</span></span>

3. <span data-ttu-id="27eda-141">Choisissez **Stratégie de prévention** pour configurer des stratégies par abonnement.</span><span class="sxs-lookup"><span data-stu-id="27eda-141">Choose **Prevention policy** to configure policies per subscription.</span></span> <span data-ttu-id="27eda-142">**Collecter les données des machines virtuelles** doit être défini sur **Activé.**</span><span class="sxs-lookup"><span data-stu-id="27eda-142">**Collect data from virtual machines** should be set to **On.**</span></span>

4. <span data-ttu-id="27eda-143">Dans les options **Stratégie de prévention**, sélectionnez **Activé** pour activer les recommandations de sécurité pertinentes pour l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="27eda-143">In the **Prevention policy** options, select **On** to enable the security recommendations that are relevant for the subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="27eda-144">Pour obtenir d’autres instructions et une explication de chacune de ces recommandations de stratégie pouvant être activées, consultez [Définir des stratégies de sécurité dans Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span><span class="sxs-lookup"><span data-stu-id="27eda-144">For more detailed instructions and an explanation of each of the policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="27eda-145">Comment configurer l’accès juste-à-temps (JIT) ?</span><span class="sxs-lookup"><span data-stu-id="27eda-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="27eda-146">Quand la fonctionnalité JIT est activée, Security Center verrouille le trafic entrant vers vos machines virtuelles Azure en créant une règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="27eda-146">When JIT is enabled, Security Center locks down inbound traffic to your Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="27eda-147">Vous sélectionnez les ports de la machine virtuelle pour lesquels le trafic entrant sera verrouillé.</span><span class="sxs-lookup"><span data-stu-id="27eda-147">You select the ports on the VM to which inbound traffic will be locked down.</span></span> <span data-ttu-id="27eda-148">Pour utiliser l’accès JIT, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="27eda-148">To use JIT access, do the following:</span></span>

1. <span data-ttu-id="27eda-149">Sélectionnez la **vignette Accès Juste à temps à la machine virtuelle** dans le panneau ASC.</span><span class="sxs-lookup"><span data-stu-id="27eda-149">Select the **Just in time VM access tile** on the ASC blade.</span></span>

2. <span data-ttu-id="27eda-150">Sélectionnez l’onglet **Recommandé**.</span><span class="sxs-lookup"><span data-stu-id="27eda-150">Select the **Recommended** tab.</span></span>

3. <span data-ttu-id="27eda-151">Sous **Machines virtuelles**, sélectionnez les machines virtuelles que vous souhaitez activer.</span><span class="sxs-lookup"><span data-stu-id="27eda-151">Under **VMs**, select the VMs that you want to enable.</span></span> <span data-ttu-id="27eda-152">Une coche est alors placée en regard des machines virtuelles concernées.</span><span class="sxs-lookup"><span data-stu-id="27eda-152">This puts a checkmark next to a VM.</span></span> 
4. <span data-ttu-id="27eda-153">Sélectionnez **Activer JIT** sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="27eda-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="27eda-154">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="27eda-154">Select **Save**.</span></span>

<span data-ttu-id="27eda-155">Ensuite, vous pouvez voir les ports par défaut qu’ASC recommande d’activer pour JIT.</span><span class="sxs-lookup"><span data-stu-id="27eda-155">Then you can see the default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="27eda-156">Vous pouvez également ajouter et configurer un nouveau port sur lequel activer la solution Juste-à-temps.</span><span class="sxs-lookup"><span data-stu-id="27eda-156">You can also add and configure a new port on which you want to enable the just in time solution.</span></span> <span data-ttu-id="27eda-157">La vignette **Accès Juste à temps à la machine virtuelle** de Security Center indique le nombre de machines virtuelles configurées pour l’accès JIT.</span><span class="sxs-lookup"><span data-stu-id="27eda-157">The **Just in time VM access** tile in the Security Center shows the number of VMs configured for JIT access.</span></span> <span data-ttu-id="27eda-158">Il montre également le nombre de demandes d’accès approuvées pendant la semaine passée.</span><span class="sxs-lookup"><span data-stu-id="27eda-158">It also shows the number of approved access requests made in the last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="27eda-159">Pour obtenir des instructions sur la procédure à suivre, et des informations supplémentaires sur l’accès Juste-à-temps, consultez [Gérer l’accès Juste à temps à la machine virtuelle.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span><span class="sxs-lookup"><span data-stu-id="27eda-159">For instructions on how to do this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="27eda-160">Comment implémenter les recommandations de sécurité ASC ?</span><span class="sxs-lookup"><span data-stu-id="27eda-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="27eda-161">Lorsqu’il identifie des failles de sécurité potentielles, il crée des recommandations.</span><span class="sxs-lookup"><span data-stu-id="27eda-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="27eda-162">Ces recommandations vous guident tout au long du processus de configuration des contrôles nécessaires.</span><span class="sxs-lookup"><span data-stu-id="27eda-162">The recommendations guide you through the process of configuring the needed controls.</span></span> 
1. <span data-ttu-id="27eda-163">Sélectionnez la vignette **Recommandations** dans le tableau de bord ASC.</span><span class="sxs-lookup"><span data-stu-id="27eda-163">Select the **Recommendations** tile on the ASC dashboard.</span></span>

2. <span data-ttu-id="27eda-164">Prenez connaissance des recommandations affichées sous forme de tableau où chaque ligne correspond à une recommandation.</span><span class="sxs-lookup"><span data-stu-id="27eda-164">View the recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="27eda-165">Pour filtrer les recommandations, sélectionnez **Filtre** et sélectionnez les valeurs de gravité et d’état à afficher.</span><span class="sxs-lookup"><span data-stu-id="27eda-165">To filter recommendations, select **Filter** and select the severity and state values you wish to see.</span></span>

4. <span data-ttu-id="27eda-166">Pour masquer une recommandation non applicable, vous pouvez cliquer avec le bouton droit et sélectionner **Faire disparaître.**</span><span class="sxs-lookup"><span data-stu-id="27eda-166">To dismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="27eda-167">Évaluez les recommandations à appliquer en premier.</span><span class="sxs-lookup"><span data-stu-id="27eda-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="27eda-168">Appliquez les recommandations dans leur ordre de priorité.</span><span class="sxs-lookup"><span data-stu-id="27eda-168">Apply the recommendations in order of priority.</span></span>

<span data-ttu-id="27eda-169">Pour obtenir la liste des recommandations possibles et des procédures pas à pas permettant de les appliquer, consultez [Gestion des recommandations de sécurité dans Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span><span class="sxs-lookup"><span data-stu-id="27eda-169">For a list of possible recommendations and walk-throughs on how to apply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="27eda-170">Détection et réponse</span><span class="sxs-lookup"><span data-stu-id="27eda-170">Detection and Response</span></span>

<span data-ttu-id="27eda-171">Détection et réponse vont de pair, car vous avez besoin de répondre aussi rapidement que possible une fois qu’une menace est détectée.</span><span class="sxs-lookup"><span data-stu-id="27eda-171">Detection and response go together, as you want to respond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="27eda-172">La détection des menaces par ASC fonctionne en collectant automatiquement les informations de sécurité à partir de vos ressources Azure, du réseau et des solutions de partenaires connectées.</span><span class="sxs-lookup"><span data-stu-id="27eda-172">ASC threat detection works by automatically collecting security information from your Azure resources, the network, and connected partner solutions.</span></span> <span data-ttu-id="27eda-173">ASC peut donc rapidement mettre à jour ses algorithmes de détection, puisque les pirates sont à l’origine d’attaques innovantes de plus en plus sophistiquées.</span><span class="sxs-lookup"><span data-stu-id="27eda-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="27eda-174">Pour plus d’informations sur le fonctionnement de la détection des menaces par ASC, consultez [Fonctionnalités de détection d’Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span><span class="sxs-lookup"><span data-stu-id="27eda-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-to-security-alerts"></a><span data-ttu-id="27eda-175">Comment gérer les alertes de sécurité et y répondre ?</span><span class="sxs-lookup"><span data-stu-id="27eda-175">How do I manage and respond to security alerts?</span></span>

<span data-ttu-id="27eda-176">La liste hiérarchisée des alertes de sécurité s’affiche dans Security Center, ainsi que les informations nécessaires pour trouver rapidement la cause d’une attaque.</span><span class="sxs-lookup"><span data-stu-id="27eda-176">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem.</span></span> <span data-ttu-id="27eda-177">Security Center inclut également des recommandations sur la manière de corriger les problèmes liés à une attaque.</span><span class="sxs-lookup"><span data-stu-id="27eda-177">Security Center also includes recommendations for how to remediate an attack.</span></span> <span data-ttu-id="27eda-178">Pour gérer vos alertes de sécurité, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="27eda-178">To manage your security alerts, do the following:</span></span>

1. <span data-ttu-id="27eda-179">Sélectionnez la vignette **Alertes de sécurité** dans le tableau de bord ASC.</span><span class="sxs-lookup"><span data-stu-id="27eda-179">Select the **Security alerts** tile in the ASC dashboard.</span></span> <span data-ttu-id="27eda-180">Celle-ci permet d’afficher les détails de chaque alerte.</span><span class="sxs-lookup"><span data-stu-id="27eda-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="27eda-181">Pour filtrer les alertes en fonction de leur date, état et gravité, sélectionnez **Filtre**, puis sélectionnez les valeurs à afficher.</span><span class="sxs-lookup"><span data-stu-id="27eda-181">To filter alerts based on date, state, and severity, select **Filter** and then select the values you want to see.</span></span>

3. <span data-ttu-id="27eda-182">Pour répondre à une alerte, sélectionnez-la, puis passez en revue les informations et sélectionnez la ressource attaquée.</span><span class="sxs-lookup"><span data-stu-id="27eda-182">To respond to an alert, select it and review the information, then select the resource that was attacked.</span></span>

4. <span data-ttu-id="27eda-183">Dans le champ **Description** figurent des détails, notamment la correction recommandée.</span><span class="sxs-lookup"><span data-stu-id="27eda-183">In the **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="27eda-184">Pour obtenir des instructions sur la réponse à donner à des alertes de sécurité, consultez [Gestion et résolution des alertes de sécurité dans Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span><span class="sxs-lookup"><span data-stu-id="27eda-184">For more detailed instructions on responding to security alerts, see [Managing and responding to security alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="27eda-185">Pour obtenir de l’aide dans l’examen des alertes de sécurité, la compagnie peut intégrer les alertes ASC à sa propre solution SIEM, à l’aide de l’[intégration des journaux Azure](https://aka.ms/AzLog).</span><span class="sxs-lookup"><span data-stu-id="27eda-185">For further help in investigating security alerts, the company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="27eda-186">Comment gérer les incidents de sécurité ?</span><span class="sxs-lookup"><span data-stu-id="27eda-186">How do I manage security incidents?</span></span>

<span data-ttu-id="27eda-187">Dans ASC, un incident de sécurité est un regroupement de toutes les alertes d’une ressource correspondant à des modèles de chaîne de destruction.</span><span class="sxs-lookup"><span data-stu-id="27eda-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="27eda-188">Un incident affiche la liste des alertes associées, qui vous permet d’en savoir plus sur chaque occurrence.</span><span class="sxs-lookup"><span data-stu-id="27eda-188">An Incident will reveal the list of related alerts, which enables you to obtain more information about each occurrence.</span></span> <span data-ttu-id="27eda-189">Les incidents apparaissent dans la vignette et le panneau Alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="27eda-189">Incidents appear in the Security Alerts tile and blade.</span></span>

<span data-ttu-id="27eda-190">Pour vérifier et gérer des incidents de sécurité, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="27eda-190">To review and manage security incidents, do the following:</span></span>

1. <span data-ttu-id="27eda-191">Sélectionnez la vignette **Alertes de sécurité**.</span><span class="sxs-lookup"><span data-stu-id="27eda-191">Select the **Security alerts** tile.</span></span> <span data-ttu-id="27eda-192">Si un incident de sécurité est détecté, il apparaît sous le graphe des alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="27eda-192">if a security incident is detected, it will appear under the security alerts graph.</span></span> <span data-ttu-id="27eda-193">Son icône diffère de celles des autres alertes.</span><span class="sxs-lookup"><span data-stu-id="27eda-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="27eda-194">Sélectionnez l’incident pour afficher d’autres détails sur cet incident de sécurité.</span><span class="sxs-lookup"><span data-stu-id="27eda-194">Select the incident to see more details about this security incident.</span></span> <span data-ttu-id="27eda-195">Les détails supplémentaires incluent sa description complète, sa gravité, son état actuel, la ressource attaquée, les étapes de correction de l’incident et les alertes qui étaient incluses dans cet incident.</span><span class="sxs-lookup"><span data-stu-id="27eda-195">Additional details include its full description, its severity, its current state, the attacked resource, the remediation steps for the incident, and the alerts that were included in this incident.</span></span>

<span data-ttu-id="27eda-196">Vous pouvez filtrer pour afficher **uniquement les incidents**, **uniquement les alertes** ou **les deux**.</span><span class="sxs-lookup"><span data-stu-id="27eda-196">You can filter to see **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-the-threat-intelligence-report"></a><span data-ttu-id="27eda-197">Comment accéder au rapport d’informations sur les menaces ?</span><span class="sxs-lookup"><span data-stu-id="27eda-197">How do I access the Threat Intelligence Report?</span></span>

<span data-ttu-id="27eda-198">ASC analyse les informations provenant de plusieurs sources pour identifier les menaces.</span><span class="sxs-lookup"><span data-stu-id="27eda-198">ASC analyzes information from multiple sources to identify threats.</span></span> <span data-ttu-id="27eda-199">Pour aider les équipes de réponse aux incidents à examiner et à corriger les menaces, Azure Security Center inclut un rapport qui contient des informations sur la menace détectée.</span><span class="sxs-lookup"><span data-stu-id="27eda-199">To assist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about the threat that was detected.</span></span>

<span data-ttu-id="27eda-200">Azure Security Center propose trois types de rapports sur les menaces, qui peuvent varier en fonction de l’attaque.</span><span class="sxs-lookup"><span data-stu-id="27eda-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="27eda-201">Les rapports disponibles sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="27eda-201">The reports available are:</span></span>

- <span data-ttu-id="27eda-202">Rapport sur le groupe d’activités : fournit des informations détaillées sur les attaquants, leurs objectifs et leurs tactiques.</span><span class="sxs-lookup"><span data-stu-id="27eda-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="27eda-203">Rapport sur la campagne : se concentre sur les détails des campagnes d’attaque spécifiques.</span><span class="sxs-lookup"><span data-stu-id="27eda-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="27eda-204">Rapport de synthèse sur la menace : couvre tous les éléments des deux rapports précédents.</span><span class="sxs-lookup"><span data-stu-id="27eda-204">Threat Summary Report: covers all items in the previous two reports.</span></span>

<span data-ttu-id="27eda-205">Ce type d’information est très utile pendant le processus de réponse aux incidents, au cours duquel des examens sont effectués en continu afin de comprendre la source de l’attaque, les motivations de l’attaquant et les solutions d’atténuation de ce problème à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="27eda-205">This type of information is very useful during the incident response process, where there is an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate this issue moving forward.</span></span>

1. <span data-ttu-id="27eda-206">Pour accéder au rapport d’informations sur les menaces, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="27eda-206">To access the threat intelligence report, do the following:</span></span>

2. <span data-ttu-id="27eda-207">Sélectionnez la vignette **Alertes de sécurité** dans le tableau de bord ASC.</span><span class="sxs-lookup"><span data-stu-id="27eda-207">Select the **Security alerts** tile on the ASC dashboard.</span></span>

3. <span data-ttu-id="27eda-208">Sélectionnez l’alerte de sécurité pour laquelle vous voulez obtenir plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="27eda-208">Select the security alert for which you want to obtain more information.</span></span>

4. <span data-ttu-id="27eda-209">Dans le champ **Rapports**, cliquez sur le lien vers le rapport d’informations sur les menaces.</span><span class="sxs-lookup"><span data-stu-id="27eda-209">In the **Reports** field, click the link to the threat intelligence report.</span></span>

5. <span data-ttu-id="27eda-210">Le fichier PDF, que vous pouvez télécharger, s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="27eda-210">This will open the PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="27eda-211">Pour plus d’informations sur le rapport d’informations sur les menaces d’ASC, consultez [Rapport d’informations sur les menaces d’Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="27eda-211">For additional information about the ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="27eda-212">Évaluation</span><span class="sxs-lookup"><span data-stu-id="27eda-212">Assessment</span></span>

<span data-ttu-id="27eda-213">Pour vous aider à tester, estimer et évaluer l’état de votre sécurité, ASC propose une des vulnérabilités intégrée aux agents cloud Qualys, dans le cadre de son composant de recommandations pour les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="27eda-213">To help with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="27eda-214">L’agent Qualys transmet des données de vulnérabilité à la plateforme de gestion Qualys, laquelle renvoie alors des données de surveillance des vulnérabilités et de l’intégrité à ASC.</span><span class="sxs-lookup"><span data-stu-id="27eda-214">The Qualys agent reports vulnerability data to the Qualys management platform, which then sends vulnerability and health monitoring data back to ASC.</span></span> <span data-ttu-id="27eda-215">La recommandation d’ajouter une solution d’évaluation des vulnérabilités s’affiche dans le panneau **Recommandations** du tableau de bord ASC.</span><span class="sxs-lookup"><span data-stu-id="27eda-215">The recommendation to add a vulnerability assessment solution is displayed in the **Recommendations** blade on the ASC dashboard.</span></span>

<span data-ttu-id="27eda-216">Une fois la solution d’évaluation des vulnérabilités installée sur la machine virtuelle cible, Azure Security Center analyse cette dernière pour détecter et identifier les vulnérabilités des applications et du système.</span><span class="sxs-lookup"><span data-stu-id="27eda-216">After the vulnerability assessment solution is installed on the target VM, Security Center scans the VM to detect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="27eda-217">Les problèmes détectés sont visibles sous l’option **Virtual Machines Recommendations (Recommandations relatives aux machines virtuelles)**.</span><span class="sxs-lookup"><span data-stu-id="27eda-217">Detected issues are shown under the **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="27eda-218">Comment mettre en œuvre une solution d’évaluation des vulnérabilités ?</span><span class="sxs-lookup"><span data-stu-id="27eda-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="27eda-219">Si une machine virtuelle n’a pas déjà une solution d’évaluation des vulnérabilités intégrée déployée, Security Center recommande d’en installer une.</span><span class="sxs-lookup"><span data-stu-id="27eda-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="27eda-220">Dans le tableau de bord ASC, dans le panneau **Recommandations**, sélectionnez **Ajouter une solution d’évaluation des vulnérabilités.**</span><span class="sxs-lookup"><span data-stu-id="27eda-220">In the ASC dashboard, on the **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="27eda-221">Sélectionnez les machines virtuelles sur lesquelles vous voulez installer la solution d’évaluation des vulnérabilités.</span><span class="sxs-lookup"><span data-stu-id="27eda-221">Select the VMs where you want to install the vulnerability assessment solution.</span></span>

3. <span data-ttu-id="27eda-222">Cliquez sur **Installer sur [nombre] machines virtuelles.**</span><span class="sxs-lookup"><span data-stu-id="27eda-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="27eda-223">Sélectionnez une solution de partenaire dans Place de marché Microsoft Azure ou sous **Utiliser une solution existante,** sélectionnez **Qualys.**</span><span class="sxs-lookup"><span data-stu-id="27eda-223">Select a partner solution in the Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="27eda-224">Vous pouvez activer ou désactiver les paramètres de mise à jour automatique dans le panneau **Solutions de partenaire**.</span><span class="sxs-lookup"><span data-stu-id="27eda-224">You can turn the auto update settings on or off in the **Partner Solutions** blade.</span></span>

<span data-ttu-id="27eda-225">Pour obtenir des instructions sur la façon d’implémenter une solution d’évaluation des vulnérabilités, consultez [Évaluation des vulnérabilités dans Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span><span class="sxs-lookup"><span data-stu-id="27eda-225">For further instructions on how to implement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="27eda-226">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="27eda-226">Next steps</span></span>

- [<span data-ttu-id="27eda-227">Guide de démarrage rapide d’Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="27eda-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="27eda-228">Présentation du Centre de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="27eda-228">Introduction to Azure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="27eda-229">Intégration des alertes Azure Security Center aux journaux Azure</span><span class="sxs-lookup"><span data-stu-id="27eda-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [<span data-ttu-id="27eda-230">Renforcer Azure Security Center avec l’évaluation des vulnérabilités intégrée</span><span class="sxs-lookup"><span data-stu-id="27eda-230">Boost Azure Security Center with Integrated Vulnerability Assessment</span></span>](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
