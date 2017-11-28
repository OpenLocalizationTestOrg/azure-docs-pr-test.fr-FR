---
title: "les déploiements PaaS aaaSecuring | Documents Microsoft"
description: " Découvrir les avantages de sécurité hello de PaaS et autres modèles de service cloud et des pratiques recommandées pour la sécurisation de votre déploiement PaaS Azure. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: techlake
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: terrylan
ms.openlocfilehash: b94fe03b6f3a43d82e1e6e834f10a423e4c1db95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-deployments"></a><span data-ttu-id="aeaaf-103">Sécurisation des déploiements PaaS</span><span class="sxs-lookup"><span data-stu-id="aeaaf-103">Securing PaaS deployments</span></span>

<span data-ttu-id="aeaaf-104">Cet article fournit des informations qui vous permettent :</span><span class="sxs-lookup"><span data-stu-id="aeaaf-104">This article provides information that helps you:</span></span>

- <span data-ttu-id="aeaaf-105">Comprendre les avantages de sécurité hello d’hébergement d’applications dans le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="aeaaf-105">Understand hello security advantages of hosting applications in hello cloud</span></span>
- <span data-ttu-id="aeaaf-106">Évaluer les avantages de sécurité hello de plateforme en tant que service (PaaS) et autres modèles de service cloud</span><span class="sxs-lookup"><span data-stu-id="aeaaf-106">Evaluate hello security advantages of platform as a service (PaaS) versus other cloud service models</span></span>
- <span data-ttu-id="aeaaf-107">Modifier le focus de la sécurité d’une approche de sécurité de périmètre centré sur l’identité tooan centrée sur le réseau</span><span class="sxs-lookup"><span data-stu-id="aeaaf-107">Change your security focus from a network-centric tooan identity-centric perimeter security approach</span></span>
- <span data-ttu-id="aeaaf-108">d'implémenter les bonnes pratiques recommandées de la sécurité de la PaaS.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-108">Implement general PaaS security best practices recommendations</span></span>

## <a name="cloud-security-advantages"></a><span data-ttu-id="aeaaf-109">Avantages du cloud en matière de sécurité</span><span class="sxs-lookup"><span data-stu-id="aeaaf-109">Cloud security advantages</span></span>
<span data-ttu-id="aeaaf-110">Il existe toobeing des avantages de sécurité dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-110">There are security advantages toobeing in hello cloud.</span></span> <span data-ttu-id="aeaaf-111">Dans un environnement sur site, les organisations disposent probablement non remplies responsabilités et des ressources limitées de tooinvest disponible dans la sécurité, ce qui crée un environnement où les attaquants tooexploit en mesure des vulnérabilités à tous les niveaux.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-111">In an on-premises environment, organizations likely have unmet responsibilities and limited resources available tooinvest in security, which creates an environment where attackers are able tooexploit vulnerabilities at all layers.</span></span>

![Les avantages de l’ère du cloud en matière de sécurité][1]

<span data-ttu-id="aeaaf-113">Les organisations est en mesure de tooimprove leur détection des menaces et les temps de réponse à l’aide des fonctionnalités de sécurité basée sur le cloud et l’intelligence de cloud d’un fournisseur.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-113">Organizations are able tooimprove their threat detection and response times by using a provider’s cloud-based security capabilities and cloud intelligence.</span></span>  <span data-ttu-id="aeaaf-114">En utilisant le fournisseur de cloud de responsabilités toohello, organisations peuvent obtenir plus garantie de sécurité, ce qui leur permet tooreallocate les ressources de sécurité et les priorités de l’entreprise tooother budget.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-114">By shifting responsibilities toohello cloud provider, organizations can get more security coverage, which enables them tooreallocate security resources and budget tooother business priorities.</span></span>

## <a name="division-of-responsibility"></a><span data-ttu-id="aeaaf-115">Répartition de la responsabilité</span><span class="sxs-lookup"><span data-stu-id="aeaaf-115">Division of responsibility</span></span>
<span data-ttu-id="aeaaf-116">Il s’agit de division de hello toounderstand important de responsabilité entre vous et Microsoft.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-116">It’s important toounderstand hello division of responsibility between you and Microsoft.</span></span> <span data-ttu-id="aeaaf-117">En local, vous possédez l’ensemble de la pile hello mais que vous vous déplacez toohello cloud certaines responsabilités de transfert tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-117">On-premises, you own hello whole stack but as you move toohello cloud some responsibilities transfer tooMicrosoft.</span></span> <span data-ttu-id="aeaaf-118">Hello responsabilité tableau ci-dessous indique les zones hello de pile de hello dans un déploiement IaaS, PaaS et SaaS dont vous êtes responsable et Microsoft est responsable.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-118">hello following responsibility matrix shows hello areas of hello stack in a SaaS, PaaS, and IaaS deployment that you are responsible for and Microsoft is responsible for.</span></span>

![Zones de responsabilité][2]

<span data-ttu-id="aeaaf-120">Vous avez vos données et les identités pour tous les types de déploiement dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-120">For all cloud deployment types, you own your data and identities.</span></span> <span data-ttu-id="aeaaf-121">Vous êtes responsable de la protection de sécurité hello de vos données et les identités, des ressources locales et hello composants cloud que vous contrôlez (qui varie selon le type de service).</span><span class="sxs-lookup"><span data-stu-id="aeaaf-121">You are responsible for protecting hello security of your data and identities, on-premises resources, and hello cloud components you control (which varies by service type).</span></span>

<span data-ttu-id="aeaaf-122">Les responsabilités sont toujours conservées par vous, quel que soit le type de hello de déploiement, sont :</span><span class="sxs-lookup"><span data-stu-id="aeaaf-122">Responsibilities that are always retained by you, regardless of hello type of deployment, are:</span></span>

- <span data-ttu-id="aeaaf-123">Données</span><span class="sxs-lookup"><span data-stu-id="aeaaf-123">Data</span></span>
- <span data-ttu-id="aeaaf-124">Endpoints</span><span class="sxs-lookup"><span data-stu-id="aeaaf-124">Endpoints</span></span>
- <span data-ttu-id="aeaaf-125">Compte</span><span class="sxs-lookup"><span data-stu-id="aeaaf-125">Account</span></span>
- <span data-ttu-id="aeaaf-126">gestion de l’accès</span><span class="sxs-lookup"><span data-stu-id="aeaaf-126">Access management</span></span>

## <a name="security-advantages-of-a-paas-cloud-service-model"></a><span data-ttu-id="aeaaf-127">Avantages d'un modèle de service cloud PaaS en matière de sécurité</span><span class="sxs-lookup"><span data-stu-id="aeaaf-127">Security advantages of a PaaS cloud service model</span></span>
<span data-ttu-id="aeaaf-128">À l’aide de hello même matrice de responsabilité, nous allons examiner les avantages de sécurité hello d’un déploiement PaaS Azure et locaux.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-128">Using hello same responsibility matrix, let’s look at hello security advantages of an Azure PaaS deployment versus on-premises.</span></span>

![Les avantages d'une PaaS en matière de sécurité][3]

<span data-ttu-id="aeaaf-130">Bas hello pile hello, infrastructure physique hello Microsoft atténue responsabilités et les risques courants.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-130">Starting at hello bottom of hello stack, hello physical infrastructure, Microsoft mitigates common risks and responsibilities.</span></span> <span data-ttu-id="aeaaf-131">Hello cloud de Microsoft est surveillée en permanence par Microsoft, il est difficile tooattack.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-131">Because hello Microsoft cloud is continually monitored by Microsoft, it is hard tooattack.</span></span> <span data-ttu-id="aeaaf-132">Il n’a aucune signification pour un hello de toopursue attaquant cloud de Microsoft en tant que cible.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-132">It doesn’t make sense for an attacker toopursue hello Microsoft cloud as a target.</span></span> <span data-ttu-id="aeaaf-133">À moins que les intrus hello possède un grand nombre d’argent et de ressources, les intrus hello est probablement toomove sur tooanother cible.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-133">Unless hello attacker has lots of money and resources, hello attacker is likely toomove on tooanother target.</span></span>  

<span data-ttu-id="aeaaf-134">Milieu hello de pile de hello, il n’existe aucune différence entre un déploiement PaaS et sur site.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-134">In hello middle of hello stack, there is no difference between a PaaS deployment and on-premises.</span></span> <span data-ttu-id="aeaaf-135">Couche d’application hello et la couche de gestion de compte et un accès hello, vous disposez des risques similaires.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-135">At hello application layer and hello account and access management layer, you have similar risks.</span></span> <span data-ttu-id="aeaaf-136">Dans la section hello suivante étapes de cet article, nous vous guide pratiques toobest pour éliminer ou réduire ces risques.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-136">In hello next steps section of this article, we will guide you toobest practices for eliminating or minimizing these risks.</span></span>

<span data-ttu-id="aeaaf-137">Haut hello de pile de hello, gouvernance des données et la gestion des droits, vous prenez un risque qui peut être atténué par la gestion de clés.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-137">At hello top of hello stack, data governance and rights management, you take on one risk that can be mitigated by key management.</span></span> <span data-ttu-id="aeaaf-138">(la gestion des clés est traitée dans les bonnes pratiques). Lors de la gestion de clés est une responsabilité supplémentaire, vous avez des zones dans un déploiement PaaS que vous n’avez plus toomanage donc vous pouvez décaler la gestion des ressources tookey.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-138">(Key management is covered in best practices.) While key management is an additional responsibility, you have areas in a PaaS deployment that you no longer have toomanage so you can shift resources tookey management.</span></span>

<span data-ttu-id="aeaaf-139">Hello plateforme Azure fournit également une protection DDoS renforcée à l’aide de différentes technologies de réseau.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-139">hello Azure platform also provides you strong DDoS protection by using various network-based technologies.</span></span> <span data-ttu-id="aeaaf-140">Toutefois, tous les types de méthodes de protection contre le déni de service distribué (DDoS) basée sur le réseau ont leurs limites par lien et par centre de données.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-140">However, all types of network-based DDoS protection methods have their limits on a per-link and per-datacenter basis.</span></span> <span data-ttu-id="aeaaf-141">toohelp éviter impact hello de grandes attaques DDoS, vous pouvez tirer parti de la fonctionnalité cloud d’Azure core destinée à vous tooquickly et automatiquement montée en puissance parallèle toodefend contre des attaques DDoS.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-141">toohelp avoid hello impact of large DDoS attacks, you can take advantage of Azure’s core cloud capability of enabling you tooquickly and automatically scale out toodefend against DDoS attacks.</span></span> <span data-ttu-id="aeaaf-142">Nous aborderons plus en détail sur comment vous pouvez faire cela dans hello recommandé pratiques articles.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-142">We'll go into more detail on how you can do this in hello recommended practices articles.</span></span>

## <a name="modernizing-hello-defenders-mindset"></a><span data-ttu-id="aeaaf-143">État d’esprit du modernisation defender hello</span><span class="sxs-lookup"><span data-stu-id="aeaaf-143">Modernizing hello defender’s mindset</span></span>
<span data-ttu-id="aeaaf-144">Les déploiements PaaS accompagnent une équipe dans votre toosecurity approche globale.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-144">With PaaS deployments come a shift in your overall approach toosecurity.</span></span> <span data-ttu-id="aeaaf-145">Vous déplacez d’avoir toocontrol tout vous-même responsabilité toosharing avec Microsoft.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-145">You shift from needing toocontrol everything yourself toosharing responsibility with Microsoft.</span></span>

<span data-ttu-id="aeaaf-146">Une autre différence importante entre PaaS et des déploiements sur site traditionnelle, est une nouvelle vue de ce que définit le périmètre de sécurité principal hello.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-146">Another significant difference between PaaS and traditional on-premises deployments, is a new view of what defines hello primary security perimeter.</span></span> <span data-ttu-id="aeaaf-147">Historiquement, périmètre de sécurité locale principale hello était votre réseau et plus local sécurité conceptions utilisez hello réseau comme son pivot principal de sécurité.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-147">Historically, hello primary on-premises security perimeter was your network and most on-premises security designs use hello network as its primary security pivot.</span></span> <span data-ttu-id="aeaaf-148">Pour les déploiements PaaS, il est préférable en tenant compte du périmètre de sécurité principal identité toobe hello.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-148">For PaaS deployments, you are better served by considering identity toobe hello primary security perimeter.</span></span>

## <a name="identity-as-hello-primary-security-perimeter"></a><span data-ttu-id="aeaaf-149">Identité que le périmètre de sécurité principal hello</span><span class="sxs-lookup"><span data-stu-id="aeaaf-149">Identity as hello primary security perimeter</span></span>
<span data-ttu-id="aeaaf-150">Une des cinq caractéristiques essentielles hello du cloud computing est un large accès réseau, ce qui rend centrée sur le réseau considérant moins pertinentes.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-150">One of hello five essential characteristics of cloud computing is broad network access, which makes network-centric thinking less relevant.</span></span> <span data-ttu-id="aeaaf-151">objectif Hello d’une grande partie du cloud computing est tooallow utilisateurs tooaccess des ressources, quelle que soit l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-151">hello goal of much of cloud computing is tooallow users tooaccess resources regardless of location.</span></span> <span data-ttu-id="aeaaf-152">Pour la plupart des utilisateurs, leur emplacement va toobe quelque part sur hello Internet.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-152">For most users, their location is going toobe somewhere on hello Internet.</span></span>

<span data-ttu-id="aeaaf-153">Hello figure suivante montre comment le périmètre de sécurité hello a évolué à partir d’un réseau de périmètre d’identité périmètre tooan.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-153">hello following figure shows how hello security perimeter has evolved from a network perimeter tooan identity perimeter.</span></span> <span data-ttu-id="aeaaf-154">La sécurité devient plus ou moins sur la protection de votre réseau sur la protection de vos données, ainsi que gestion de la sécurité hello de vos applications et les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-154">Security becomes less about defending your network and more about defending your data, as well as managing hello security of your apps and users.</span></span> <span data-ttu-id="aeaaf-155">Hello principale différence est que vous souhaitez société d’importantes tooyour de toopush sécurité proche toowhat.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-155">hello key difference is that you want toopush security closer toowhat’s important tooyour company.</span></span>

![L'identité en tant que nouveau périmètre de sécurité][4]

<span data-ttu-id="aeaaf-157">Initialement, les services PaaS Azure (par exemple, les rôles web et Azure SQL) fournissaient peu ou pas de défenses du périmètre de réseau traditionnelles.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-157">Initially, Azure PaaS services (for example, web roles and Azure SQL) provided little or no traditional network perimeter defenses.</span></span> <span data-ttu-id="aeaaf-158">Il a été entendu qu’objectif de l’élément hello est toobe exposée toohello Internet (rôle web) et que l’authentification hello nouveau périmètre (par exemple, un objet BLOB ou SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="aeaaf-158">It was understood that hello element’s purpose was toobe exposed toohello Internet (web role) and that authentication provides hello new perimeter (for example, BLOB or Azure SQL).</span></span>

<span data-ttu-id="aeaaf-159">Pratiques de sécurité modernes partent du principe qu’adversaire hello a enfreint le périmètre du réseau hello.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-159">Modern security practices assume that hello adversary has breached hello network perimeter.</span></span> <span data-ttu-id="aeaaf-160">Par conséquent, les pratiques de défense modernes ont déplacés tooidentity.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-160">Therefore, modern defense practices have moved tooidentity.</span></span> <span data-ttu-id="aeaaf-161">Les organisations doivent établir un périmètre de sécurité basé sur les identités avec forte hygiène d’authentification et d’autorisation (bonnes pratiques).</span><span class="sxs-lookup"><span data-stu-id="aeaaf-161">Organizations must establish an identity-based security perimeter with strong authentication and authorization hygiene (best practices).</span></span>

## <a name="recommendations-for-managing-hello-identity-perimeter"></a><span data-ttu-id="aeaaf-162">Recommandations pour la gestion du périmètre d’identité hello</span><span class="sxs-lookup"><span data-stu-id="aeaaf-162">Recommendations for managing hello identity perimeter</span></span>

<span data-ttu-id="aeaaf-163">Principes et des modèles pour le réseau de périmètre hello ont été disponibles des dizaines d’années.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-163">Principles and patterns for hello network perimeter have been available for decades.</span></span> <span data-ttu-id="aeaaf-164">En revanche, secteur d’activité hello possède relativement moins expérience à l’aide d’identité en tant que le périmètre de sécurité principal hello.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-164">In contrast, hello industry has relatively less experience with using identity as hello primary security perimeter.</span></span> <span data-ttu-id="aeaaf-165">Cela étant dit, nous ont accumulé suffisamment tooprovide expérience quelques recommandations générales qui sont prouvées dans le champ de hello et appliquer tooalmost tous les services PaaS.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-165">With that said, we have accumulated enough experience tooprovide some general recommendations that are proven in hello field and apply tooalmost all PaaS services.</span></span>

<span data-ttu-id="aeaaf-166">Hello Voici une toomanaging d’approche meilleures pratiques générales du périmètre de votre identité.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-166">hello following summarizes a general best practices approach toomanaging your identity perimeter.</span></span>

- <span data-ttu-id="aeaaf-167">**Ne perdez pas vos clés ou les informations d’identification** sécurisation des clés et les informations d’identification est essentielle toosecure les déploiements PaaS.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-167">**Don’t lose your keys or credentials** Securing keys and credentials is essential toosecure PaaS deployments.</span></span> <span data-ttu-id="aeaaf-168">La perte de clés ou d'informations d’identification est un problème courant.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-168">Losing keys and credentials is a common problem.</span></span> <span data-ttu-id="aeaaf-169">Toouse une solution centralisée est une bonne solution dans laquelle les clés et les secrets peuvent être stockées dans des modules de sécurité matériel (HSM).</span><span class="sxs-lookup"><span data-stu-id="aeaaf-169">One good solution is toouse a centralized solution where keys and secrets can be stored in hardware security modules (HSM).</span></span> <span data-ttu-id="aeaaf-170">Azure fournit un module HSM dans le cloud hello avec [Azure Key Vault](../key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aeaaf-170">Azure provides you an HSM in hello cloud with [Azure Key Vault](../key-vault/key-vault-whatis.md).</span></span>
- <span data-ttu-id="aeaaf-171">**Ne placez les informations d’identification et d’autres secrets dans le code source ou GitHub** hello uniquement pire que perdre vos clés et les informations d’identification rencontre une partie non autorisée obtenir accès toothem.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-171">**Don’t put credentials and other secrets into source code or GitHub** hello only thing worse than losing your keys and credentials is having an unauthorized party gain access toothem.</span></span> <span data-ttu-id="aeaaf-172">Les personnes malveillantes sont parti tootake en mesure de clés de toofind bot technologies et des clés secrètes stockées dans des référentiels de code, tels que GitHub.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-172">Attackers are able tootake advantage of bot technologies toofind keys and secrets stored in code repositories such as GitHub.</span></span> <span data-ttu-id="aeaaf-173">Ne placez pas de clé et de secrets dans ces référentiels de code source publics.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-173">Do not put key and secrets in these public source code repositories.</span></span>
- <span data-ttu-id="aeaaf-174">**Protégez vos interfaces de gestion de machine virtuelle sur des services PaaS et IaaS hybrides** Les services IaaS et PaaS s’exécutent sur des machines virtuelles (VM).</span><span class="sxs-lookup"><span data-stu-id="aeaaf-174">**Protect your VM management interfaces on hybrid PaaS and IaaS services** IaaS and PaaS services run on virtual machines (VMs).</span></span> <span data-ttu-id="aeaaf-175">En fonction de type hello de service, plusieurs interfaces de gestion sont disponibles qui permettent de tooremote gérer ces ordinateurs virtuels directement.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-175">Depending on hello type of service, several management interfaces are available that enable you tooremote manage these VMs directly.</span></span> <span data-ttu-id="aeaaf-176">Vous pouvez utiliser les protocoles de gestion à distance tels que [le protocole SSH (Secure Shell)](https://en.wikipedia.org/wiki/Secure_Shell), [le protocole RDP (Remote Desktop)](https://support.microsoft.com/kb/186607) et [PowerShell distant](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enable-psremoting).</span><span class="sxs-lookup"><span data-stu-id="aeaaf-176">Remote management protocols such as [Secure Shell Protocol (SSH)](https://en.wikipedia.org/wiki/Secure_Shell), [Remote Desktop Protocol (RDP)](https://support.microsoft.com/kb/186607), and [Remote PowerShell](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enable-psremoting) can be used.</span></span> <span data-ttu-id="aeaaf-177">En règle générale, nous vous recommandons de ne pas activer tooVMs d’accès à distance directe à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-177">In general, we recommend that you do not enable direct remote access tooVMs from hello Internet.</span></span> <span data-ttu-id="aeaaf-178">S’il est disponible, vous devez utiliser d'autres approches, telles que l’utilisation d’un réseau privé virtuel dans un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-178">If available, you should use alternate approaches such as using virtual private networking into an Azure virtual network.</span></span> <span data-ttu-id="aeaaf-179">Si aucune autre approche n'est disponible, assurez-vous que vous utilisez des phrases secrètes complexes et, si d'autres options sont disponibles, l’authentification à deux facteurs (notamment [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)).</span><span class="sxs-lookup"><span data-stu-id="aeaaf-179">If alternative approaches are not available, then ensure that you use complex passphrases, and when available, two-factor authentication (such as [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)).</span></span>
- <span data-ttu-id="aeaaf-180">**Utilisez une authentification forte et des plateformes d’autorisation**</span><span class="sxs-lookup"><span data-stu-id="aeaaf-180">**Use strong authentication and authorization platforms**</span></span>

  - <span data-ttu-id="aeaaf-181">Utilisez des identités fédérées dans Azure AD au lieu des magasins d’utilisateurs personnalisés.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-181">Use federated identities in Azure AD instead of custom user stores.</span></span> <span data-ttu-id="aeaaf-182">Lorsque vous utilisez des identités fédérées, vous tirer parti d’une approche basée sur la plateforme et vous déléguer la gestion de hello de partenaires de tooyour identités autorisés.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-182">When you use federated identities, you take advantage of a platform-based approach and you delegate hello management of authorized identities tooyour partners.</span></span> <span data-ttu-id="aeaaf-183">Une approche d’identité fédérée est particulièrement importante dans les scénarios lorsque les employés sont terminées et que les informations doivent toobe réfléchie par l’intermédiaire de plusieurs identités et d’autorisation systèmes.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-183">A federated identity approach is especially important in scenarios when employees are terminated and that information needs toobe reflected through multiple identity and authorization systems.</span></span>
  - <span data-ttu-id="aeaaf-184">Utilisez des mécanismes d'authentification et d'autorisation basés sur des plateformes au lieu d'un code personnalisé.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-184">Use platform supplied authentication and authorization mechanisms instead of custom code.</span></span> <span data-ttu-id="aeaaf-185">Hello parce que le développement de code d’authentification personnalisé peut être sujette aux erreurs.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-185">hello reason is that developing custom authentication code can be error prone.</span></span> <span data-ttu-id="aeaaf-186">La plupart de vos développeurs n’est pas des experts en sécurité et est peu probable toobe connaître les subtilités hello et hello derniers développements de l’authentification et l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-186">Most of your developers are not security experts and are unlikely toobe aware of hello subtleties and hello latest developments in authentication and authorization.</span></span> <span data-ttu-id="aeaaf-187">Le code commercial (par exemple par Microsoft) est souvent contrôlé en ce qui concerne la sécurité.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-187">Commercial code (for example from Microsoft) is often extensively security reviewed.</span></span>
  - <span data-ttu-id="aeaaf-188">Utilisez l'authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-188">Use multi-factor authentication.</span></span> <span data-ttu-id="aeaaf-189">L’authentification multifacteur est en cours de hello standard pour l’authentification et l’autorisation car elle évite les failles de sécurité hello inhérents aux types de nom d’utilisateur et mot de passe d’authentification.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-189">Multi-factor authentication is hello current standard for authentication and authorization because it avoids hello security weaknesses inherent in username and password types of authentication.</span></span> <span data-ttu-id="aeaaf-190">Interfaces d’accès aux tooboth hello Azure management (portal remote PowerShell) et toocustomer services exposés au doit être conçus et configuré toouse [Azure multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="aeaaf-190">Access tooboth hello Azure management (portal/remote PowerShell) interfaces and toocustomer facing services should be designed and configured toouse [Azure Multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md).</span></span>
  - <span data-ttu-id="aeaaf-191">Utilisez des protocoles d’authentification standard, tels qu'OAuth2 et Kerberos.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-191">Use standard authentication protocols, such as OAuth2 and Kerberos.</span></span> <span data-ttu-id="aeaaf-192">Ces protocoles ont été largement contrôlés et sont probablement implémentés dans le cadre de vos bibliothèques de plateforme pour l’authentification et l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-192">These protocols have been extensively peer reviewed and are likely implemented as part of your platform libraries for authentication and authorization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aeaaf-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aeaaf-193">Next steps</span></span>
<span data-ttu-id="aeaaf-194">Dans cet article, nous avons vu les avantages d’un déploiement PaaS Azure en matière de sécurité.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-194">In this article, we focused on security advantages of an Azure PaaS deployment.</span></span> <span data-ttu-id="aeaaf-195">Découvrez ensuite les pratiques recommandées pour sécuriser solutions PaaS web et mobiles.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-195">Next, learn recommended practices for securing your PaaS web and mobile solutions.</span></span> <span data-ttu-id="aeaaf-196">Nous allons commencer par Azure App Service, Azure SQL Database et Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="aeaaf-196">We’ll start with Azure App Service, Azure SQL Database, and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="aeaaf-197">Lorsque des articles sur les pratiques recommandées pour les autres services Azure sont disponibles, des liens seront fournies dans hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="aeaaf-197">As articles on recommended practices for other Azure services become available, links will be provided in hello following list:</span></span>

- [<span data-ttu-id="aeaaf-198">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="aeaaf-198">Azure App Service</span></span>](security-paas-applications-using-app-services.md)
- [<span data-ttu-id="aeaaf-199">Azure SQL Database et Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="aeaaf-199">Azure SQL Database and Azure SQL Data Warehouse</span></span>](security-paas-applications-using-sql.md)
- <span data-ttu-id="aeaaf-200">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="aeaaf-200">Azure Storage</span></span>
- <span data-ttu-id="aeaaf-201">Cache REDIS Azure</span><span class="sxs-lookup"><span data-stu-id="aeaaf-201">Azure REDIS Cache</span></span>
- <span data-ttu-id="aeaaf-202">Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="aeaaf-202">Azure Service Bus</span></span>
- <span data-ttu-id="aeaaf-203">Pare-feu d’applications web</span><span class="sxs-lookup"><span data-stu-id="aeaaf-203">Web Application Firewalls</span></span>

<!--Image references-->
[1]: ./media/security-paas-deployments/advantages-of-cloud.png
[2]: ./media/security-paas-deployments/responsibility-zones.png
[3]: ./media/security-paas-deployments/advantages-of-paas.png
[4]: ./media/security-paas-deployments/identity-perimeter.png