---
title: "les données personnelles aaaProtect avec Azure Security Center | Documents Microsoft"
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
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="db1b1-103">Protéger les données personnelles contre les violations et attaques : Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="db1b1-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="db1b1-104">Cet article vous aidera à comprendre comment toouse Azure Security Center tooprotect les données personnelles d’atteinte et les attaques.</span><span class="sxs-lookup"><span data-stu-id="db1b1-104">This article will help you understand how toouse Azure Security Center tooprotect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="db1b1-105">Scénario</span><span class="sxs-lookup"><span data-stu-id="db1b1-105">Scenario</span></span> 

<span data-ttu-id="db1b1-106">Une société de croisière volumineux en hello États-Unis, étend ses itinéraires de toooffer d’opérations dans hello Méditerranée et mer Baltique, ainsi que hello britanniques.</span><span class="sxs-lookup"><span data-stu-id="db1b1-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="db1b1-107">toohelp à cet égard, elle a acquis plusieurs lignes croisière plus petits dans Italie, Allemagne, Danemark et hello Royaume-Uni.</span><span class="sxs-lookup"><span data-stu-id="db1b1-107">toohelp in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="db1b1-108">la société de Hello utilise des données d’entreprise de Microsoft Azure toostore dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="db1b1-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="db1b1-109">Ces dernières incluent des informations d’identification personnelle telles que les noms, les adresses, les numéros de téléphone et les informations de carte de crédit.</span><span class="sxs-lookup"><span data-stu-id="db1b1-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="db1b1-110">Des informations de ressources humaines sont également inclues comme :</span><span class="sxs-lookup"><span data-stu-id="db1b1-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="db1b1-111">Adresses</span><span class="sxs-lookup"><span data-stu-id="db1b1-111">Addresses</span></span>
- <span data-ttu-id="db1b1-112">Numéros de téléphone</span><span class="sxs-lookup"><span data-stu-id="db1b1-112">Phone numbers</span></span>
- <span data-ttu-id="db1b1-113">Numéros d’identification fiscale</span><span class="sxs-lookup"><span data-stu-id="db1b1-113">Tax identification numbers</span></span>
- <span data-ttu-id="db1b1-114">Informations médicales</span><span class="sxs-lookup"><span data-stu-id="db1b1-114">Medical information</span></span>

<span data-ttu-id="db1b1-115">ligne de croisière Hello gère également les bases de données volumineuses de membres du programme de récompense et fidélité.</span><span class="sxs-lookup"><span data-stu-id="db1b1-115">hello cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="db1b1-116">Réseau de hello accès employés de l’entreprise à partir de sites distants et les agents de voyage société hello situés dans Bonjour tout le monde ont accès aux ressources de l’entreprise toosome.</span><span class="sxs-lookup"><span data-stu-id="db1b1-116">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>
<span data-ttu-id="db1b1-117">Données personnelles parcourent le réseau de hello entre ces bureaux et le centre de données Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="db1b1-117">Personal data travels across hello network between these locations and hello Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="db1b1-118">Définition du problème</span><span class="sxs-lookup"><span data-stu-id="db1b1-118">Problem statement</span></span>

<span data-ttu-id="db1b1-119">Hello société est préoccupée menace hello d’attaques sur leurs ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="db1b1-119">hello company is concerned about hello threat of attacks on their Azure resources.</span></span> <span data-ttu-id="db1b1-120">Ils veulent exposition tooprevent de personnes de toounauthorized données personnelles des employés et clients.</span><span class="sxs-lookup"><span data-stu-id="db1b1-120">They want tooprevent exposure of customers’ and employees’ personal data toounauthorized persons.</span></span> <span data-ttu-id="db1b1-121">Ils veulent quant à la fois prévention et correction/réponse, mais aussi un moyen efficace toomonitor hello en continu la sécurité de leurs ressources de cloud.</span><span class="sxs-lookup"><span data-stu-id="db1b1-121">They want guidance on both prevention and response/remediation, as well as an effective way toomonitor hello ongoing security of their cloud resources.</span></span>
<span data-ttu-id="db1b1-122">Elle nécessite une solide ligne de défense contre les attaques complexes et organisées d’aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="db1b1-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="db1b1-123">Objectif de l’entreprise</span><span class="sxs-lookup"><span data-stu-id="db1b1-123">Company goal</span></span>

<span data-ttu-id="db1b1-124">Un des objectifs de l’entreprise hello est confidentialité de hello tooensure des employés et les clients des données personnelles à protéger contre les menaces.</span><span class="sxs-lookup"><span data-stu-id="db1b1-124">One of hello company’s goals is tooensure hello privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="db1b1-125">Un des objectifs est toorespond immédiatement toosigns de violation toomitigate hello impact.</span><span class="sxs-lookup"><span data-stu-id="db1b1-125">One of their goals is toorespond immediately toosigns of breach toomitigate hello impact.</span></span> <span data-ttu-id="db1b1-126">Il nécessite un moyen tooassess hello l’état actuel de la sécurité, identifier les configurations vulnérables et les corriger.</span><span class="sxs-lookup"><span data-stu-id="db1b1-126">It requires a way tooassess hello current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="db1b1-127">Solutions</span><span class="sxs-lookup"><span data-stu-id="db1b1-127">Solutions</span></span>

<span data-ttu-id="db1b1-128">Microsoft Azure Security Center (ASC) fournit une solution de surveillance de sécurité et de gestion de stratégie intégrée.</span><span class="sxs-lookup"><span data-stu-id="db1b1-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="db1b1-129">Il offre des fonctionnalités de prévention, de détection et de réponse aux menaces efficaces et faciles à utiliser.</span><span class="sxs-lookup"><span data-stu-id="db1b1-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="db1b1-130">Prévention</span><span class="sxs-lookup"><span data-stu-id="db1b1-130">Prevention</span></span>

<span data-ttu-id="db1b1-131">ASC vous aide à empêcher les violations vous tooset des stratégies de sécurité, fournir un accès juste-à-temps et mettre en œuvre des recommandations de sécurité.</span><span class="sxs-lookup"><span data-stu-id="db1b1-131">ASC helps you prevent breaches by enabling you tooset security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="db1b1-132">Une stratégie de sécurité définit ensemble hello de contrôles recommandé pour les ressources hello spécifié abonnement.</span><span class="sxs-lookup"><span data-stu-id="db1b1-132">A security policy defines hello set of controls recommended for resources within hello specified subscription.</span></span> <span data-ttu-id="db1b1-133">Juste-à-temps accès peut être utilisé toolock vers le bas le trafic entrant tooyour les machines virtuelles Azure, ce qui réduit les risques tooattacks.</span><span class="sxs-lookup"><span data-stu-id="db1b1-133">Just in time access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks.</span></span> <span data-ttu-id="db1b1-134">Recommandations de sécurité sont créées par ASC après l’analyse d’état de la sécurité de vos ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="db1b1-134">Security recommendations are created by ASC after analyzing hello security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="db1b1-135">Comment définir des stratégies de sécurité dans ASC ?</span><span class="sxs-lookup"><span data-stu-id="db1b1-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="db1b1-136">Vous pouvez configurer des stratégies de sécurité pour chaque abonnement.</span><span class="sxs-lookup"><span data-stu-id="db1b1-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="db1b1-137">toomodify une stratégie de sécurité, vous devez être propriétaire ou contributeur de cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="db1b1-137">toomodify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="db1b1-138">Bonjour portail Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="db1b1-138">In hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="db1b1-139">Sélectionnez **stratégie** dans le tableau de bord hello ASC.</span><span class="sxs-lookup"><span data-stu-id="db1b1-139">Select **Policy** in hello ASC dashboard.</span></span>

2. <span data-ttu-id="db1b1-140">Sélectionnez l’abonnement hello sur lequel vous souhaitez que la stratégie de hello de tooenable.</span><span class="sxs-lookup"><span data-stu-id="db1b1-140">Select hello subscription on which you want tooenable hello policy.</span></span>

3. <span data-ttu-id="db1b1-141">Choisissez **stratégie de prévention de** stratégies tooconfigure par abonnement.</span><span class="sxs-lookup"><span data-stu-id="db1b1-141">Choose **Prevention policy** tooconfigure policies per subscription.</span></span> <span data-ttu-id="db1b1-142">**Collecter des données à partir d’ordinateurs virtuels** doit être défini trop**sur.**</span><span class="sxs-lookup"><span data-stu-id="db1b1-142">**Collect data from virtual machines** should be set too**On.**</span></span>

4. <span data-ttu-id="db1b1-143">Bonjour **stratégie de prévention de** options, sélectionnez **sur** tooenable les recommandations de sécurité hello qui sont pertinentes pour l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="db1b1-143">In hello **Prevention policy** options, select **On** tooenable hello security recommendations that are relevant for hello subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="db1b1-144">Pour plus d’instructions et une explication de chacune des recommandations pour la stratégie hello qui peuvent être activées, consultez [définir des stratégies de sécurité dans le centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span><span class="sxs-lookup"><span data-stu-id="db1b1-144">For more detailed instructions and an explanation of each of hello policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="db1b1-145">Comment configurer l’accès juste-à-temps (JIT) ?</span><span class="sxs-lookup"><span data-stu-id="db1b1-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="db1b1-146">Lorsque le JIT est activé, le centre de sécurité bloque le trafic entrant tooyour machines virtuelles Azure en créant une règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="db1b1-146">When JIT is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="db1b1-147">Vous sélectionnez les ports hello sur hello VM toowhich le trafic entrant sera verrouillé.</span><span class="sxs-lookup"><span data-stu-id="db1b1-147">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="db1b1-148">toouse JIT accéder, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="db1b1-148">toouse JIT access, do hello following:</span></span>

1. <span data-ttu-id="db1b1-149">Sélectionnez hello **juste dans la vignette de temps machine virtuelle accès** sur le panneau ASC hello.</span><span class="sxs-lookup"><span data-stu-id="db1b1-149">Select hello **Just in time VM access tile** on hello ASC blade.</span></span>

2. <span data-ttu-id="db1b1-150">Sélectionnez hello **recommandé** onglet.</span><span class="sxs-lookup"><span data-stu-id="db1b1-150">Select hello **Recommended** tab.</span></span>

3. <span data-ttu-id="db1b1-151">Sous **machines virtuelles**, sélectionnez les machines virtuelles de hello que vous souhaitez tooenable.</span><span class="sxs-lookup"><span data-stu-id="db1b1-151">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="db1b1-152">Cela permet de placer un ordinateur virtuel de tooa suivant coche.</span><span class="sxs-lookup"><span data-stu-id="db1b1-152">This puts a checkmark next tooa VM.</span></span> 
4. <span data-ttu-id="db1b1-153">Sélectionnez **Activer JIT** sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="db1b1-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="db1b1-154">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="db1b1-154">Select **Save**.</span></span>

<span data-ttu-id="db1b1-155">Ensuite, vous pouvez voir des ports par défaut hello ASC recommandées doivent être activés pour JIT.</span><span class="sxs-lookup"><span data-stu-id="db1b1-155">Then you can see hello default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="db1b1-156">Vous pouvez également ajouter et configurer un nouveau port sur lequel vous souhaitez hello tooenable juste-à-solution de temps.</span><span class="sxs-lookup"><span data-stu-id="db1b1-156">You can also add and configure a new port on which you want tooenable hello just in time solution.</span></span> <span data-ttu-id="db1b1-157">Hello **juste à l’accès des ordinateurs virtuels de temps** vignette Bonjour centre de sécurité affiche nombre hello d’ordinateurs virtuels configurés pour l’accès JIT.</span><span class="sxs-lookup"><span data-stu-id="db1b1-157">hello **Just in time VM access** tile in hello Security Center shows hello number of VMs configured for JIT access.</span></span> <span data-ttu-id="db1b1-158">Il montre également le nombre hello approuvées de demandes d’accès effectuées Bonjour la semaine dernière.</span><span class="sxs-lookup"><span data-stu-id="db1b1-158">It also shows hello number of approved access requests made in hello last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="db1b1-159">Pour obtenir des instructions sur la façon de toodo, et des informations supplémentaires sur juste dans access de temps, consultez [gérer l’accès d’ordinateur virtuel à l’aide de juste-à-temps.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span><span class="sxs-lookup"><span data-stu-id="db1b1-159">For instructions on how toodo this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="db1b1-160">Comment implémenter les recommandations de sécurité ASC ?</span><span class="sxs-lookup"><span data-stu-id="db1b1-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="db1b1-161">Lorsqu’il identifie des failles de sécurité potentielles, il crée des recommandations.</span><span class="sxs-lookup"><span data-stu-id="db1b1-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="db1b1-162">recommandations de Hello vous guident tout au long des processus de hello de configuration de contrôles de hello si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="db1b1-162">hello recommendations guide you through hello process of configuring hello needed controls.</span></span> 
1. <span data-ttu-id="db1b1-163">Sélectionnez hello **recommandations** vignette sur le tableau de bord hello ASC.</span><span class="sxs-lookup"><span data-stu-id="db1b1-163">Select hello **Recommendations** tile on hello ASC dashboard.</span></span>

2. <span data-ttu-id="db1b1-164">Afficher les recommandations de hello, qui sont affichées sous forme de tableau, où chaque ligne représente une recommandation.</span><span class="sxs-lookup"><span data-stu-id="db1b1-164">View hello recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="db1b1-165">recommandations de toofilter, sélectionnez **filtre** et sélectionnez valeurs hello gravité et son état toosee vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="db1b1-165">toofilter recommendations, select **Filter** and select hello severity and state values you wish toosee.</span></span>

4. <span data-ttu-id="db1b1-166">toodismiss une recommandation qui n’est pas applicable, vous pouvez cliquez droit et sélectionnez **faire disparaître.**</span><span class="sxs-lookup"><span data-stu-id="db1b1-166">toodismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="db1b1-167">Évaluez les recommandations à appliquer en premier.</span><span class="sxs-lookup"><span data-stu-id="db1b1-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="db1b1-168">Appliquer les recommandations de hello dans l’ordre de priorité.</span><span class="sxs-lookup"><span data-stu-id="db1b1-168">Apply hello recommendations in order of priority.</span></span>

<span data-ttu-id="db1b1-169">Pour obtenir la liste des recommandations possibles et des procédures détaillées sur la façon de tooapply chaque, consultez [gestion des recommandations de sécurité dans le centre de sécurité Azure.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span><span class="sxs-lookup"><span data-stu-id="db1b1-169">For a list of possible recommendations and walk-throughs on how tooapply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="db1b1-170">Détection et réponse</span><span class="sxs-lookup"><span data-stu-id="db1b1-170">Detection and Response</span></span>

<span data-ttu-id="db1b1-171">Détection et réponse allient ensemble, comme vous le voulez toorespond aussi rapidement que possible après qu’une menace est détectée.</span><span class="sxs-lookup"><span data-stu-id="db1b1-171">Detection and response go together, as you want toorespond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="db1b1-172">Détection des menaces ASC fonctionne en collectant automatiquement des informations de sécurité à partir de vos ressources Azure, hello réseau et les solutions de partenaire connecté.</span><span class="sxs-lookup"><span data-stu-id="db1b1-172">ASC threat detection works by automatically collecting security information from your Azure resources, hello network, and connected partner solutions.</span></span> <span data-ttu-id="db1b1-173">ASC peut donc rapidement mettre à jour ses algorithmes de détection, puisque les pirates sont à l’origine d’attaques innovantes de plus en plus sophistiquées.</span><span class="sxs-lookup"><span data-stu-id="db1b1-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="db1b1-174">Pour plus d’informations sur le fonctionnement de la détection des menaces par ASC, consultez [Fonctionnalités de détection d’Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span><span class="sxs-lookup"><span data-stu-id="db1b1-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a><span data-ttu-id="db1b1-175">Comment gérer et répondre toosecurity alertes ?</span><span class="sxs-lookup"><span data-stu-id="db1b1-175">How do I manage and respond toosecurity alerts?</span></span>

<span data-ttu-id="db1b1-176">Une liste des alertes de sécurité hiérarchisée est indiquée dans le centre de sécurité, ainsi que de hello informations dont vous avez besoin tooquickly examiner le problème de hello.</span><span class="sxs-lookup"><span data-stu-id="db1b1-176">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem.</span></span> <span data-ttu-id="db1b1-177">Centre de sécurité inclut également des recommandations sur la manière tooremediate une attaque.</span><span class="sxs-lookup"><span data-stu-id="db1b1-177">Security Center also includes recommendations for how tooremediate an attack.</span></span> <span data-ttu-id="db1b1-178">toomanage votre sécurité des alertes, faire hello suivant :</span><span class="sxs-lookup"><span data-stu-id="db1b1-178">toomanage your security alerts, do hello following:</span></span>

1. <span data-ttu-id="db1b1-179">Sélectionnez hello **alertes de sécurité** vignette dans le tableau de bord hello ASC.</span><span class="sxs-lookup"><span data-stu-id="db1b1-179">Select hello **Security alerts** tile in hello ASC dashboard.</span></span> <span data-ttu-id="db1b1-180">Celle-ci permet d’afficher les détails de chaque alerte.</span><span class="sxs-lookup"><span data-stu-id="db1b1-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="db1b1-181">alertes toofilter en fonction de date, d’état et de gravité, sélectionnez **filtre** , puis sélectionnez les valeurs hello toosee.</span><span class="sxs-lookup"><span data-stu-id="db1b1-181">toofilter alerts based on date, state, and severity, select **Filter** and then select hello values you want toosee.</span></span>

3. <span data-ttu-id="db1b1-182">toorespond tooan alerte, sélectionnez-la et passez en revue les informations de hello, puis sélectionnez hello ressource qui a été attaqué.</span><span class="sxs-lookup"><span data-stu-id="db1b1-182">toorespond tooan alert, select it and review hello information, then select hello resource that was attacked.</span></span>

4. <span data-ttu-id="db1b1-183">Bonjour **Description** champ, vous verrez plus d’informations, y compris la résolution recommandée.</span><span class="sxs-lookup"><span data-stu-id="db1b1-183">In hello **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="db1b1-184">Pour des instructions sur les alertes toosecurity ne répond plus détaillées, consultez [toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span><span class="sxs-lookup"><span data-stu-id="db1b1-184">For more detailed instructions on responding toosecurity alerts, see [Managing and responding toosecurity alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="db1b1-185">Pour obtenir de l’aide de l’examen des alertes de sécurité, société de hello peut intégrer les alertes ASC sa propre solution SIEM, à l’aide de [Azure journal intégration](https://aka.ms/AzLog).</span><span class="sxs-lookup"><span data-stu-id="db1b1-185">For further help in investigating security alerts, hello company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="db1b1-186">Comment gérer les incidents de sécurité ?</span><span class="sxs-lookup"><span data-stu-id="db1b1-186">How do I manage security incidents?</span></span>

<span data-ttu-id="db1b1-187">Dans ASC, un incident de sécurité est un regroupement de toutes les alertes d’une ressource correspondant à des modèles de chaîne de destruction.</span><span class="sxs-lookup"><span data-stu-id="db1b1-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="db1b1-188">Un Incident indiquent liste hello d’alertes associées, ce qui permet de vous tooobtain plus d’informations sur chaque occurrence.</span><span class="sxs-lookup"><span data-stu-id="db1b1-188">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span> <span data-ttu-id="db1b1-189">Incidents apparaissent dans hello vignette alertes de sécurité et de panneau.</span><span class="sxs-lookup"><span data-stu-id="db1b1-189">Incidents appear in hello Security Alerts tile and blade.</span></span>

<span data-ttu-id="db1b1-190">tooreview et la gestion des incidents de sécurité, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="db1b1-190">tooreview and manage security incidents, do hello following:</span></span>

1. <span data-ttu-id="db1b1-191">Sélectionnez hello **alertes de sécurité** vignette.</span><span class="sxs-lookup"><span data-stu-id="db1b1-191">Select hello **Security alerts** tile.</span></span> <span data-ttu-id="db1b1-192">Si un incident de sécurité est détecté, elle s’affiche sous le graphique d’alertes de sécurité de hello.</span><span class="sxs-lookup"><span data-stu-id="db1b1-192">if a security incident is detected, it will appear under hello security alerts graph.</span></span> <span data-ttu-id="db1b1-193">Son icône diffère de celles des autres alertes.</span><span class="sxs-lookup"><span data-stu-id="db1b1-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="db1b1-194">Sélectionnez toosee d’incident hello plus de détails sur cet incident de sécurité.</span><span class="sxs-lookup"><span data-stu-id="db1b1-194">Select hello incident toosee more details about this security incident.</span></span> <span data-ttu-id="db1b1-195">Des détails supplémentaires comprennent sa description complète, sa gravité, son état actuel, hello attaqué ressource, les étapes de conversion hello pour les incidents hello et hello alertes qui ont été inclus dans cet incident.</span><span class="sxs-lookup"><span data-stu-id="db1b1-195">Additional details include its full description, its severity, its current state, hello attacked resource, hello remediation steps for hello incident, and hello alerts that were included in this incident.</span></span>

<span data-ttu-id="db1b1-196">Vous pouvez filtrer toosee **uniquement les incidents**, **alertes uniquement**, ou **les deux**.</span><span class="sxs-lookup"><span data-stu-id="db1b1-196">You can filter toosee **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a><span data-ttu-id="db1b1-197">Comment accéder à hello Threat Intelligence rapport ?</span><span class="sxs-lookup"><span data-stu-id="db1b1-197">How do I access hello Threat Intelligence Report?</span></span>

<span data-ttu-id="db1b1-198">ASC analyse les informations contre les menaces de tooidentify plusieurs sources.</span><span class="sxs-lookup"><span data-stu-id="db1b1-198">ASC analyzes information from multiple sources tooidentify threats.</span></span> <span data-ttu-id="db1b1-199">les équipes de réponse aux incidents tooassist examiner et corriger les menaces, centre de sécurité inclut un rapport de menace qui contient des informations sur les menaces hello qui a été détectée.</span><span class="sxs-lookup"><span data-stu-id="db1b1-199">tooassist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about hello threat that was detected.</span></span>

<span data-ttu-id="db1b1-200">Azure Security Center propose trois types de rapports sur les menaces, qui peuvent varier en fonction de l’attaque.</span><span class="sxs-lookup"><span data-stu-id="db1b1-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="db1b1-201">rapports Hello disponibles sont :</span><span class="sxs-lookup"><span data-stu-id="db1b1-201">hello reports available are:</span></span>

- <span data-ttu-id="db1b1-202">Rapport sur le groupe d’activités : fournit des informations détaillées sur les attaquants, leurs objectifs et leurs tactiques.</span><span class="sxs-lookup"><span data-stu-id="db1b1-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="db1b1-203">Rapport sur la campagne : se concentre sur les détails des campagnes d’attaque spécifiques.</span><span class="sxs-lookup"><span data-stu-id="db1b1-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="db1b1-204">Rapport de synthèse de menace : couvre tous les éléments dans les rapports de deux précédente hello.</span><span class="sxs-lookup"><span data-stu-id="db1b1-204">Threat Summary Report: covers all items in hello previous two reports.</span></span>

<span data-ttu-id="db1b1-205">Ce type d’information est très utile au cours du processus de réponse aux incidents hello, s’il existe une source de hello toounderstand enquête en cours d’attaque de hello, hello la personne malveillante, et des motivations le toomitigate toodo ce problème passer.</span><span class="sxs-lookup"><span data-stu-id="db1b1-205">This type of information is very useful during hello incident response process, where there is an ongoing investigation toounderstand hello source of hello attack, hello attacker’s motivations, and what toodo toomitigate this issue moving forward.</span></span>

1. <span data-ttu-id="db1b1-206">tooaccess hello sur les menaces de rapports, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="db1b1-206">tooaccess hello threat intelligence report, do hello following:</span></span>

2. <span data-ttu-id="db1b1-207">Sélectionnez hello **alertes de sécurité** vignette sur le tableau de bord hello ASC.</span><span class="sxs-lookup"><span data-stu-id="db1b1-207">Select hello **Security alerts** tile on hello ASC dashboard.</span></span>

3. <span data-ttu-id="db1b1-208">Sélectionnez alerte de sécurité hello pour lequel vous souhaitez tooobtain plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="db1b1-208">Select hello security alert for which you want tooobtain more information.</span></span>

4. <span data-ttu-id="db1b1-209">Bonjour **rapports** , cliquez sur hello lien toohello threat intelligence du rapport.</span><span class="sxs-lookup"><span data-stu-id="db1b1-209">In hello **Reports** field, click hello link toohello threat intelligence report.</span></span>

5. <span data-ttu-id="db1b1-210">Fichier PDF hello, que vous pouvez télécharger s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="db1b1-210">This will open hello PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="db1b1-211">Pour plus d’informations sur hello rapport ASC menace, consultez [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="db1b1-211">For additional information about hello ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="db1b1-212">Évaluation</span><span class="sxs-lookup"><span data-stu-id="db1b1-212">Assessment</span></span>

<span data-ttu-id="db1b1-213">toohelp avec des tests, l’évaluation et d’évaluation de vos défenses, ASC fournit pour l’évaluation des vulnérabilités intégré avec Qualys agents du cloud, dans le cadre de son composant de recommandations de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="db1b1-213">toohelp with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="db1b1-214">agent de Qualys Hello signale une vulnérabilité données toohello Qualys plateforme de gestion, qui envoie ensuite la vulnérabilité et l’intégrité de l’analyse des données de sauvegarde tooASC.</span><span class="sxs-lookup"><span data-stu-id="db1b1-214">hello Qualys agent reports vulnerability data toohello Qualys management platform, which then sends vulnerability and health monitoring data back tooASC.</span></span> <span data-ttu-id="db1b1-215">Hello tooadd recommandation une solution d’évaluation de la vulnérabilité est affichée dans hello **recommandations** panneau dans le tableau de bord hello ASC.</span><span class="sxs-lookup"><span data-stu-id="db1b1-215">hello recommendation tooadd a vulnerability assessment solution is displayed in hello **Recommendations** blade on hello ASC dashboard.</span></span>

<span data-ttu-id="db1b1-216">Une fois la solution d’évaluation des risques de vulnérabilité hello est installée sur la cible de hello machine virtuelle, les analyses de centre de sécurité hello toodetect de machine virtuelle et identifient les vulnérabilités des applications et système.</span><span class="sxs-lookup"><span data-stu-id="db1b1-216">After hello vulnerability assessment solution is installed on hello target VM, Security Center scans hello VM toodetect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="db1b1-217">A détecté les problèmes sont affichent sous hello **recommandations de Machines virtuelles** option.</span><span class="sxs-lookup"><span data-stu-id="db1b1-217">Detected issues are shown under hello **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="db1b1-218">Comment mettre en œuvre une solution d’évaluation des vulnérabilités ?</span><span class="sxs-lookup"><span data-stu-id="db1b1-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="db1b1-219">Si une machine virtuelle n’a pas déjà une solution d’évaluation des vulnérabilités intégrée déployée, Security Center recommande d’en installer une.</span><span class="sxs-lookup"><span data-stu-id="db1b1-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="db1b1-220">De hello ASC tableau de bord sur hello **recommandations** panneau, sélectionnez **ajouter une solution d’évaluation de la vulnérabilité.**</span><span class="sxs-lookup"><span data-stu-id="db1b1-220">In hello ASC dashboard, on hello **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="db1b1-221">Sélectionnez les machines virtuelles de hello où vous souhaitez la solution d’évaluation des risques de vulnérabilité tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="db1b1-221">Select hello VMs where you want tooinstall hello vulnerability assessment solution.</span></span>

3. <span data-ttu-id="db1b1-222">Cliquez sur **Installer sur [nombre] machines virtuelles.**</span><span class="sxs-lookup"><span data-stu-id="db1b1-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="db1b1-223">Sélectionnez une solution partenaire Bonjour Azure Marketplace ou sous **utiliser une solution existante,** sélectionnez **Qualys.**</span><span class="sxs-lookup"><span data-stu-id="db1b1-223">Select a partner solution in hello Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="db1b1-224">Vous pouvez activer hello automatiquement mise à jour ou désactiver les paramètres de hello **Solutions de partenaire** panneau.</span><span class="sxs-lookup"><span data-stu-id="db1b1-224">You can turn hello auto update settings on or off in hello **Partner Solutions** blade.</span></span>

<span data-ttu-id="db1b1-225">Pour plus d’informations sur la façon de tooimplement une solution d’évaluation de la vulnérabilité, consultez [évaluation des vulnérabilités dans le centre de sécurité Azure.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span><span class="sxs-lookup"><span data-stu-id="db1b1-225">For further instructions on how tooimplement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="db1b1-226">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="db1b1-226">Next steps</span></span>

- [<span data-ttu-id="db1b1-227">Guide de démarrage rapide d’Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="db1b1-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="db1b1-228">Introduction tooAzure centre de sécurité</span><span class="sxs-lookup"><span data-stu-id="db1b1-228">Introduction tooAzure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="db1b1-229">Intégration des alertes Azure Security Center aux journaux Azure</span><span class="sxs-lookup"><span data-stu-id="db1b1-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- [<span data-ttu-id="db1b1-230">Renforcer Azure Security Center avec l’évaluation des vulnérabilités intégrée</span><span class="sxs-lookup"><span data-stu-id="db1b1-230">Boost Azure Security Center with Integrated Vulnerability Assessment</span></span>](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)
