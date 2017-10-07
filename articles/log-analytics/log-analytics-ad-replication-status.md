---
title: "état de réplication d’Active Directory avec Azure journal Analytique d’aaaMonitor | Documents Microsoft"
description: "Hello pack de solution d’état de réplication Active Directory régulièrement surveille votre environnement Active Directory pour les échecs de réplication et signale les résultats hello sur votre tableau de bord OMS."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 1b988972-8e01-4f83-a7f4-87f62778f91d
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 235e4f7a066ea50b79f681398182b22c91fb6d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-active-directory-replication-status-with-log-analytics"></a><span data-ttu-id="03a14-103">Surveiller l’état de la réplication Active Directory avec Log Analytics</span><span class="sxs-lookup"><span data-stu-id="03a14-103">Monitor Active Directory replication status with Log Analytics</span></span>

![Symbole de l’état de la réplication AD](./media/log-analytics-ad-replication-status/ad-replication-status-symbol.png)

<span data-ttu-id="03a14-105">Active Directory est un composant clé de l’environnement informatique d’une entreprise.</span><span class="sxs-lookup"><span data-stu-id="03a14-105">Active Directory is a key component of an enterprise IT environment.</span></span> <span data-ttu-id="03a14-106">tooensure haute disponibilité et hautes performances, chaque contrôleur de domaine possède sa propre copie de base de données Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="03a14-106">tooensure high availability and high performance, each domain controller has its own copy of hello Active Directory database.</span></span> <span data-ttu-id="03a14-107">Contrôleurs de domaine répliquent entre eux dans classer les modifications de toopropagate dans toute entreprise de hello.</span><span class="sxs-lookup"><span data-stu-id="03a14-107">Domain controllers replicate with each other in order toopropagate changes across hello enterprise.</span></span> <span data-ttu-id="03a14-108">Échecs de ce processus de réplication peuvent provoquer de nombreux problèmes dans toute entreprise de hello.</span><span class="sxs-lookup"><span data-stu-id="03a14-108">Failures in this replication process can cause a variety of problems across hello enterprise.</span></span>

<span data-ttu-id="03a14-109">Hello pack de solution d’état de la réplication AD surveille votre environnement Active Directory pour les échecs de réplication régulièrement et signale les résultats hello sur votre tableau de bord OMS.</span><span class="sxs-lookup"><span data-stu-id="03a14-109">hello AD Replication Status solution pack regularly monitors your Active Directory environment for any replication failures and reports hello results on your OMS dashboard.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="03a14-110">L’installation et la configuration de solution de hello</span><span class="sxs-lookup"><span data-stu-id="03a14-110">Installing and configuring hello solution</span></span>
<span data-ttu-id="03a14-111">Utilisez hello suivant tooinstall des informations et configurer une solution de hello.</span><span class="sxs-lookup"><span data-stu-id="03a14-111">Use hello following information tooinstall and configure hello solution.</span></span>

* <span data-ttu-id="03a14-112">Vous devez installer des agents sur les contrôleurs de domaine qui sont membres de hello domaine toobe est évaluée.</span><span class="sxs-lookup"><span data-stu-id="03a14-112">You must install agents on domain controllers that are members of hello domain toobe evaluated.</span></span> <span data-ttu-id="03a14-113">Ou bien, vous devez installer des agents sur les serveurs membres et configurer hello agents toosend AD réplication données tooOMS.</span><span class="sxs-lookup"><span data-stu-id="03a14-113">Or, you must install agents on member servers and configure hello agents toosend AD replication data tooOMS.</span></span> <span data-ttu-id="03a14-114">toounderstand tooconnect tooOMS d’ordinateurs Windows, voir [tooLog d’ordinateurs Windows de se connecter Analytique](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="03a14-114">toounderstand how tooconnect Windows computers tooOMS, see [Connect Windows computers tooLog Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="03a14-115">Si votre contrôleur de domaine fait déjà partie d’un environnement System Center Operations Manager existant que vous souhaitez tooconnect tooOMS, consultez [connecter Operations Manager tooLog Analytique](log-analytics-om-agents.md).</span><span class="sxs-lookup"><span data-stu-id="03a14-115">If your domain controller is already part of an existing System Center Operations Manager environment that you want tooconnect tooOMS, see [Connect Operations Manager tooLog Analytics](log-analytics-om-agents.md).</span></span>
* <span data-ttu-id="03a14-116">Ajouter hello état de réplication Active Directory solution tooyour espace de travail OMS à l’aide du processus de hello décrit dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="03a14-116">Add hello Active Directory Replication Status solution tooyour OMS workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>  <span data-ttu-id="03a14-117">Aucune configuration supplémentaire n’est requise.</span><span class="sxs-lookup"><span data-stu-id="03a14-117">There is no further configuration required.</span></span>

## <a name="ad-replication-status-data-collection-details"></a><span data-ttu-id="03a14-118">Détails de la collecte des données pour la solution État de la réplication AD</span><span class="sxs-lookup"><span data-stu-id="03a14-118">AD Replication Status data collection details</span></span>
<span data-ttu-id="03a14-119">Hello tableau suivant présente les méthodes de collecte de données et d’autres détails sur la façon dont les données sont collectées pour l’état de la réplication AD.</span><span class="sxs-lookup"><span data-stu-id="03a14-119">hello following table shows data collection methods and other details about how data is collected for AD Replication Status.</span></span>

| <span data-ttu-id="03a14-120">plateforme</span><span class="sxs-lookup"><span data-stu-id="03a14-120">platform</span></span> | <span data-ttu-id="03a14-121">Agent direct</span><span class="sxs-lookup"><span data-stu-id="03a14-121">Direct Agent</span></span> | <span data-ttu-id="03a14-122">Agent SCOM</span><span class="sxs-lookup"><span data-stu-id="03a14-122">SCOM agent</span></span> | <span data-ttu-id="03a14-123">Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="03a14-123">Azure Storage</span></span> | <span data-ttu-id="03a14-124">SCOM requis ?</span><span class="sxs-lookup"><span data-stu-id="03a14-124">SCOM required?</span></span> | <span data-ttu-id="03a14-125">Données de l’agent SCOM envoyées via un groupe d’administration</span><span class="sxs-lookup"><span data-stu-id="03a14-125">SCOM agent data sent via management group</span></span> | <span data-ttu-id="03a14-126">fréquence de collecte</span><span class="sxs-lookup"><span data-stu-id="03a14-126">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="03a14-127">Windows</span><span class="sxs-lookup"><span data-stu-id="03a14-127">Windows</span></span> |<span data-ttu-id="03a14-128">&#8226;</span><span class="sxs-lookup"><span data-stu-id="03a14-128">&#8226;</span></span> |<span data-ttu-id="03a14-129">&#8226;</span><span class="sxs-lookup"><span data-stu-id="03a14-129">&#8226;</span></span> |  |  |<span data-ttu-id="03a14-130">&#8226;</span><span class="sxs-lookup"><span data-stu-id="03a14-130">&#8226;</span></span> |<span data-ttu-id="03a14-131">tous les cinq jours</span><span class="sxs-lookup"><span data-stu-id="03a14-131">every five days</span></span> |

## <a name="optionally-enable-a-non-domain-controller-toosend-ad-data-toooms"></a><span data-ttu-id="03a14-132">Si vous le souhaitez, activer un tooOMS de données toosend AD non-contrôleurs de domaine</span><span class="sxs-lookup"><span data-stu-id="03a14-132">Optionally, enable a non-domain controller toosend AD data tooOMS</span></span>
<span data-ttu-id="03a14-133">Si vous ne souhaitez tooconnect un de vos contrôleurs de domaine directement tooOMS, vous pouvez utiliser n’importe quel autre ordinateur connecté à OMS dans votre toocollect de domaine, les données pour hello solution de l’état de la réplication AD pack et qu’il envoie des données de salutation.</span><span class="sxs-lookup"><span data-stu-id="03a14-133">If you don't want tooconnect any of your domain controllers directly tooOMS, you can use any other OMS-connected computer in your domain toocollect data for hello AD Replication Status solution pack and have it send hello data.</span></span>

### <a name="tooenable-a-non-domain-controller-toosend-ad-data-toooms"></a><span data-ttu-id="03a14-134">tooenable un tooOMS de données toosend AD non-contrôleurs de domaine</span><span class="sxs-lookup"><span data-stu-id="03a14-134">tooenable a non-domain controller toosend AD data tooOMS</span></span>
1. <span data-ttu-id="03a14-135">Vérifiez que hello de l’ordinateur est membre du domaine hello que vous souhaitez toomonitor à l’aide de la solution d’état de réplication hello AD.</span><span class="sxs-lookup"><span data-stu-id="03a14-135">Verify that hello computer is a member of hello domain that you wish toomonitor using hello AD Replication Status solution.</span></span>
2. <span data-ttu-id="03a14-136">[Se connecter hello Windows ordinateur tooOMS](log-analytics-windows-agents.md) ou [se connecter à l’aide de votre tooOMS d’environnement Operations Manager existant](log-analytics-om-agents.md), s’il n’est pas déjà connecté.</span><span class="sxs-lookup"><span data-stu-id="03a14-136">[Connect hello Windows computer tooOMS](log-analytics-windows-agents.md) or [connect it using your existing Operations Manager environment tooOMS](log-analytics-om-agents.md), if it is not already connected.</span></span>
3. <span data-ttu-id="03a14-137">Sur cet ordinateur, définissez hello clé de Registre suivante :</span><span class="sxs-lookup"><span data-stu-id="03a14-137">On that computer, set hello following registry key:</span></span>

   * <span data-ttu-id="03a14-138">Clé : **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**</span><span class="sxs-lookup"><span data-stu-id="03a14-138">Key: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**</span></span>
   * <span data-ttu-id="03a14-139">Valeur : **IsTarget**</span><span class="sxs-lookup"><span data-stu-id="03a14-139">Value: **IsTarget**</span></span>
   * <span data-ttu-id="03a14-140">Données de la valeur : **true**</span><span class="sxs-lookup"><span data-stu-id="03a14-140">Value Data: **true**</span></span>

   > [!NOTE]
   > <span data-ttu-id="03a14-141">Ces modifications ne prennent pas d’effet jusqu'à ce que votre hello de redémarrer le service Microsoft Monitoring Agent (HealthService.exe).</span><span class="sxs-lookup"><span data-stu-id="03a14-141">These changes do not take effect until your restart hello Microsoft Monitoring Agent service (HealthService.exe).</span></span>
   >
   >

## <a name="understanding-replication-errors"></a><span data-ttu-id="03a14-142">Présentation des erreurs de réplication</span><span class="sxs-lookup"><span data-stu-id="03a14-142">Understanding replication errors</span></span>
<span data-ttu-id="03a14-143">Une fois que vous avez des données d’état de réplication AD envoyées tooOMS, vous voyez un toohello similaire vignette suivant d’image de tableau de bord OMS hello indiquant combien vous avez actuellement des erreurs de réplication.</span><span class="sxs-lookup"><span data-stu-id="03a14-143">Once you have AD replication status data sent tooOMS, you see a tile similar toohello following image on hello OMS dashboard indicating how many replication errors you currently have.</span></span>  
![Vignette de l’état de la réplication AD](./media/log-analytics-ad-replication-status/oms-ad-replication-tile.png)

<span data-ttu-id="03a14-145">**Erreurs de réplication critique** sont des erreurs qui se trouvent dans ou supérieure à 75 % de hello [durée de vie de temporisation](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) pour votre forêt Active Directory.</span><span class="sxs-lookup"><span data-stu-id="03a14-145">**Critical Replication Errors** are errors that are at or above 75% of hello [tombstone lifetime](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) for your Active Directory forest.</span></span>

<span data-ttu-id="03a14-146">Lorsque vous cliquez sur la vignette de hello, vous pouvez afficher plus d’informations sur les erreurs de hello.</span><span class="sxs-lookup"><span data-stu-id="03a14-146">When you click hello tile, you can view more information about hello errors.</span></span>
<span data-ttu-id="03a14-147">![Tableau de bord de l’état de la réplication AD](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)</span><span class="sxs-lookup"><span data-stu-id="03a14-147">![AD Replication Status dashboard](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)</span></span>

### <a name="destination-server-status-and-source-server-status"></a><span data-ttu-id="03a14-148">Destination Server Status (État du serveur de destination) et Source Server Status (État du serveur source)</span><span class="sxs-lookup"><span data-stu-id="03a14-148">Destination Server Status and Source Server Status</span></span>
<span data-ttu-id="03a14-149">Ces colonnes indiquent l’état hello de serveurs de destination et les serveurs sources qui rencontrent des erreurs de réplication.</span><span class="sxs-lookup"><span data-stu-id="03a14-149">These columns show hello status of destination servers and source servers that are experiencing replication errors.</span></span> <span data-ttu-id="03a14-150">nombre de Hello après que chaque nom de contrôleur de domaine indique le nombre de hello d’erreurs de réplication sur ce contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="03a14-150">hello number after each domain controller name indicates hello number of replication errors on that domain controller.</span></span>

<span data-ttu-id="03a14-151">erreurs de Hello pour les serveurs de destination et source sont affichés, car certains problèmes sont tootroubleshoot plus facile à partir de la perspective de serveur hello source et autres utilisateurs du point de vue serveur de destination hello.</span><span class="sxs-lookup"><span data-stu-id="03a14-151">hello errors for both destination servers and source servers are shown because some problems are easier tootroubleshoot from hello source server perspective and others from hello destination server perspective.</span></span>

<span data-ttu-id="03a14-152">Dans cet exemple, vous pouvez voir que le nombre de serveurs de destination ont à peu près hello même nombre d’erreurs, mais il existe un serveur source (ADDC35) qui a beaucoup d’erreurs plus que hello tous les autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="03a14-152">In this example, you can see that many destination servers have roughly hello same number of errors, but there's one source server (ADDC35) that has many more errors than all hello others.</span></span> <span data-ttu-id="03a14-153">Il est probable qu’il existe un problème sur ADDC35 qui provoque le partenaires de réplication tooits toofail toosend données.</span><span class="sxs-lookup"><span data-stu-id="03a14-153">It's likely that there is some problem on ADDC35 that is causing it toofail toosend data tooits replication partners.</span></span> <span data-ttu-id="03a14-154">Résoudre les problèmes de hello sur ADDC35 peut résoudre la plupart des erreurs de hello qui s’affichent dans la zone de serveur de destination hello.</span><span class="sxs-lookup"><span data-stu-id="03a14-154">Fixing hello problems on ADDC35 might resolve many of hello errors that appear in hello destination server area.</span></span>

### <a name="replication-error-types"></a><span data-ttu-id="03a14-155">Replication Error Types (Types d’erreurs de réplication)</span><span class="sxs-lookup"><span data-stu-id="03a14-155">Replication Error Types</span></span>
<span data-ttu-id="03a14-156">Cette zone fournit des informations sur les types hello d’erreurs détectées au sein de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="03a14-156">This area gives you information about hello types of errors detected throughout your enterprise.</span></span> <span data-ttu-id="03a14-157">Chaque erreur possède un code numérique unique et un message qui peut vous aider à déterminer la cause première hello d’erreur de hello.</span><span class="sxs-lookup"><span data-stu-id="03a14-157">Each error has a unique numerical code and a message that can help you determine hello root cause of hello error.</span></span>

<span data-ttu-id="03a14-158">anneau Hello haut hello vous donne une idée des erreurs s’affichent plus et moins souvent dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="03a14-158">hello donut at hello top gives you an idea of which errors appear more and less frequently in your environment.</span></span>

<span data-ttu-id="03a14-159">Il vous indique lorsque plusieurs contrôleurs de domaine expérience hello même erreur de réplication.</span><span class="sxs-lookup"><span data-stu-id="03a14-159">It shows you when multiple domain controllers experience hello same replication error.</span></span> <span data-ttu-id="03a14-160">Dans ce cas, vous pouvez être en mesure de toodiscover ou identifier une solution sur un contrôleur de domaine, puis répétez sur d’autres contrôleurs de domaine faisant l’objet hello même erreur.</span><span class="sxs-lookup"><span data-stu-id="03a14-160">In this case, you may be able toodiscover or identify a solution on one domain controller, then repeat it on other domain controllers affected by hello same error.</span></span>

### <a name="tombstone-lifetime"></a><span data-ttu-id="03a14-161">durée de vie des objets tombstone (TSL)</span><span class="sxs-lookup"><span data-stu-id="03a14-161">Tombstone Lifetime</span></span>
<span data-ttu-id="03a14-162">durée de vie de désactivation Hello détermine la durée pendant laquelle un objet supprimé, appelée tooas un objet tombstone, est conservée dans la base de données Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="03a14-162">hello tombstone lifetime determines how long a deleted object, referred tooas a tombstone, is retained in hello Active Directory database.</span></span> <span data-ttu-id="03a14-163">Lorsqu’une durée de vie des objets supprimés passe hello désactivé (tombstone), un processus de garbage collection supprime automatiquement à partir de la base de données Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="03a14-163">When a deleted object passes hello tombstone lifetime, a garbage collection process automatically removes it from hello Active Directory database.</span></span>

<span data-ttu-id="03a14-164">durée de vie de désactivation Hello par défaut est de 180 jours pour les versions les plus récentes de Windows, mais il était 60 jours sur des versions antérieures, et il peut être modifié explicitement par un administrateur Active Directory.</span><span class="sxs-lookup"><span data-stu-id="03a14-164">hello default tombstone lifetime is 180 days for most recent versions of Windows, but it was 60 days on older versions, and it can be changed explicitly by an Active Directory administrator.</span></span>

<span data-ttu-id="03a14-165">Il est important tooknow si vous rencontrez des erreurs de réplication qui sont presque atteintes ou ont dépassé la durée de vie de désactivation hello.</span><span class="sxs-lookup"><span data-stu-id="03a14-165">It's important tooknow if you're having replication errors that are approaching or are past hello tombstone lifetime.</span></span> <span data-ttu-id="03a14-166">Si les deux contrôleurs de domaine de rencontrer une erreur de réplication qui persiste au-delà de durée de vie de désactivation hello, est désactiver la réplication entre les deux contrôleurs de domaine, même si hello réplication erreur sous-jacent est fixe.</span><span class="sxs-lookup"><span data-stu-id="03a14-166">If two domain controllers experience a replication error that persists past hello tombstone lifetime, replication is disabled between those two domain controllers, even if hello underlying replication error is fixed.</span></span>

<span data-ttu-id="03a14-167">zone de durée de vie de désactivation de Hello vous aide à identifier les endroits où la réplication a été désactivée est risque de se produire.</span><span class="sxs-lookup"><span data-stu-id="03a14-167">hello Tombstone Lifetime area helps you identify places where disabled replication is in danger of happening.</span></span> <span data-ttu-id="03a14-168">Chaque erreur Bonjour **plus de 100 % TSL** catégorie représente une partition qui n’a pas répliqué entre son serveur source et de destination pour au moins durée de vie de désactivation hello pour la forêt hello.</span><span class="sxs-lookup"><span data-stu-id="03a14-168">Each error in hello **Over 100% TSL** category represents a partition that has not replicated between its source and destination server for at least hello tombstone lifetime for hello forest.</span></span>

<span data-ttu-id="03a14-169">Dans ce cas, le simplement résolution d’erreur de réplication hello sera pas suffisante.</span><span class="sxs-lookup"><span data-stu-id="03a14-169">In this situation, simply fixing hello replication error will not be enough.</span></span> <span data-ttu-id="03a14-170">Au minimum, vous devez toomanually examiner tooidentify et nettoyer des objets en attente avant de pouvoir redémarrer la réplication.</span><span class="sxs-lookup"><span data-stu-id="03a14-170">At a minimum, you need toomanually investigate tooidentify and clean up lingering objects before you can restart replication.</span></span> <span data-ttu-id="03a14-171">Vous devrez peut-être même de toodecommission un contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="03a14-171">You may even need toodecommission a domain controller.</span></span>

<span data-ttu-id="03a14-172">Dans Ajout tooidentifying toutes les erreurs de réplication qui ont conservées au-delà de durée de vie de désactivation hello vous également erreurs de tooany toopay attention relèvent hello **50 à 75 % TSL** ou **75-100 % TSL** catégories.</span><span class="sxs-lookup"><span data-stu-id="03a14-172">In addition tooidentifying any replication errors that have persisted past hello tombstone lifetime, you also want toopay attention tooany errors falling into hello **50-75% TSL** or **75-100% TSL** categories.</span></span>

<span data-ttu-id="03a14-173">Ce sont des erreurs qui sont clairement en attente, non temporaire, afin qu’ils probablement besoin de votre tooresolve intervention.</span><span class="sxs-lookup"><span data-stu-id="03a14-173">These are errors that are clearly lingering, not transient, so they likely need your intervention tooresolve.</span></span> <span data-ttu-id="03a14-174">excellente Hello est qu’ils n’ont pas encore atteint durée de vie de désactivation hello.</span><span class="sxs-lookup"><span data-stu-id="03a14-174">hello good news is that they have not yet reached hello tombstone lifetime.</span></span> <span data-ttu-id="03a14-175">Si vous corrigez ces problèmes rapidement et *avant* qu’ils atteignent la durée de vie de désactivation hello, la réplication peut redémarrer avec une intervention manuelle minimale.</span><span class="sxs-lookup"><span data-stu-id="03a14-175">If you fix these problems promptly and *before* they reach hello tombstone lifetime, replication can restart with minimal manual intervention.</span></span>

<span data-ttu-id="03a14-176">Comme indiqué précédemment, vignette de tableau de bord hello pour la solution d’état de réplication hello AD montre le nombre hello de *critique* dans votre environnement, qui est défini en tant qu’erreurs sont plus de 75 % de la durée de vie de désactivation (y compris des erreurs de réplication erreurs sont plus de 100 % de TSL).</span><span class="sxs-lookup"><span data-stu-id="03a14-176">As noted earlier, hello dashboard tile for hello AD Replication Status solution shows hello number of *critical* replication errors in your environment, which is defined as errors that are over 75% of tombstone lifetime (including errors that are over 100% of TSL).</span></span> <span data-ttu-id="03a14-177">S’efforcent tookeep ce nombre à 0.</span><span class="sxs-lookup"><span data-stu-id="03a14-177">Strive tookeep this number at 0.</span></span>

> [!NOTE]
> <span data-ttu-id="03a14-178">Tous les calculs de pourcentage de durée de vie hello tombstone reposent sur la durée de vie hello tombstone réelle de votre forêt Active Directory, donc vous pouvez approuver que les pourcentages sont précis, même si vous disposez d’une valeur de durée de vie de temporisation personnalisée définie.</span><span class="sxs-lookup"><span data-stu-id="03a14-178">All hello tombstone lifetime percentage calculations are based on hello actual tombstone lifetime for your Active Directory forest, so you can trust that those percentages are accurate, even if you have a custom tombstone lifetime value set.</span></span>
>
>

### <a name="ad-replication-status-details"></a><span data-ttu-id="03a14-179">Détails de l’état de la réplication AD</span><span class="sxs-lookup"><span data-stu-id="03a14-179">AD Replication status details</span></span>
<span data-ttu-id="03a14-180">Lorsque vous cliquez sur n’importe quel élément dans une des listes de hello, vous consultez des informations supplémentaires à l’aide de la recherche de journal.</span><span class="sxs-lookup"><span data-stu-id="03a14-180">When you click any item in one of hello lists, you see additional details about it using Log Search.</span></span> <span data-ttu-id="03a14-181">les résultats de Hello sont filtrées tooshow seul hello erreurs connexes toothat élément.</span><span class="sxs-lookup"><span data-stu-id="03a14-181">hello results are filtered tooshow only hello errors related toothat item.</span></span> <span data-ttu-id="03a14-182">Par exemple, si vous cliquez sur premier contrôleur de domaine hello répertoriés sous **état du serveur de Destination (ADDC02)**, vous voyez les résultats de recherche filtrés tooshow erreurs avec ce contrôleur de domaine répertorié comme serveur de destination hello :</span><span class="sxs-lookup"><span data-stu-id="03a14-182">For example, if you click on hello first domain controller listed under **Destination Server Status (ADDC02)**, you see search results filtered tooshow errors with that domain controller listed as hello destination server:</span></span>

![Erreurs de l’état de la réplication AD dans les résultats de la recherche](./media/log-analytics-ad-replication-status/oms-ad-replication-search-details.png)

<span data-ttu-id="03a14-184">À ce stade, vous pouvez filtrer davantage, modifiez la requête de recherche hello et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="03a14-184">From here, you can filter further, modify hello search query, and so on.</span></span> <span data-ttu-id="03a14-185">Pour plus d’informations sur l’utilisation de hello recherche de journal, consultez [recherche de journal](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="03a14-185">For more information about using hello Log Search, see [Log searches](log-analytics-log-searches.md).</span></span>

<span data-ttu-id="03a14-186">Hello **HelpLink** champ affiche l’URL de hello d’une page TechNet avec des détails supplémentaires sur cette erreur spécifique.</span><span class="sxs-lookup"><span data-stu-id="03a14-186">hello **HelpLink** field shows hello URL of a TechNet page with additional details about that specific error.</span></span> <span data-ttu-id="03a14-187">Vous pouvez copier et coller ce lien dans votre navigateur fenêtre toosee d’informations sur la résolution des problèmes et de résolution d’erreur de hello.</span><span class="sxs-lookup"><span data-stu-id="03a14-187">You can copy and paste this link into your browser window toosee information about troubleshooting and fixing hello error.</span></span>

<span data-ttu-id="03a14-188">Vous pouvez également cliquer sur **exporter** tooexport hello tooExcel des résultats.</span><span class="sxs-lookup"><span data-stu-id="03a14-188">You can also click **Export** tooexport hello results tooExcel.</span></span> <span data-ttu-id="03a14-189">Exportation de données de hello peut vous aider à visualiser les données d’erreur de réplication de quelque manière que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="03a14-189">Exporting hello data can help you visualize replication error data in any way you'd like.</span></span>

![Erreurs de l’état de réplication AD exportées dans Excel](./media/log-analytics-ad-replication-status/oms-ad-replication-export.png)

## <a name="ad-replication-status-faq"></a><span data-ttu-id="03a14-191">FAQ sur l’état de la réplication AD</span><span class="sxs-lookup"><span data-stu-id="03a14-191">AD Replication Status FAQ</span></span>
<span data-ttu-id="03a14-192">**Q : Quelle est la fréquence de la mise à jour de l’état de la réplication AD ?**</span><span class="sxs-lookup"><span data-stu-id="03a14-192">**Q: How often is AD replication status data updated?**</span></span>
<span data-ttu-id="03a14-193">R : informations de hello sont mise à jour tous les cinq jours.</span><span class="sxs-lookup"><span data-stu-id="03a14-193">A: hello information is updated every five days.</span></span>

<span data-ttu-id="03a14-194">**Q : existe-t-il un tooconfigure de façon que la fréquence à laquelle ces données sont mise à jour ?**</span><span class="sxs-lookup"><span data-stu-id="03a14-194">**Q: Is there a way tooconfigure how often this data is updated?**</span></span>
<span data-ttu-id="03a14-195">R : Pas pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="03a14-195">A: Not at this time.</span></span>

<span data-ttu-id="03a14-196">**Q : dois-je tooadd tous de mon domaine contrôleurs toomy OMS espace de travail dans l’état de la réplication toosee ordre ?**</span><span class="sxs-lookup"><span data-stu-id="03a14-196">**Q: Do I need tooadd all of my domain controllers toomy OMS workspace in order toosee replication status?**</span></span>
<span data-ttu-id="03a14-197">R : Non, un seul contrôleur de domaine doit être ajouté.</span><span class="sxs-lookup"><span data-stu-id="03a14-197">A: No, only a single domain controller must be added.</span></span> <span data-ttu-id="03a14-198">Si vous avez plusieurs contrôleurs de domaine dans votre espace de travail OMS, toutes les données sont envoyées à tooOMS.</span><span class="sxs-lookup"><span data-stu-id="03a14-198">If you have multiple domain controllers in your OMS workspace, data from all of them is sent tooOMS.</span></span>

<span data-ttu-id="03a14-199">**Q : je ne souhaite pas tooadd n’importe quel espace de travail de domaine contrôleurs toomy OMS. Puis-je continuer à utiliser hello solution de l’état de la réplication Active Directory ?**</span><span class="sxs-lookup"><span data-stu-id="03a14-199">**Q: I don't want tooadd any domain controllers toomy OMS workspace. Can I still use hello AD Replication Status solution?**</span></span>
<span data-ttu-id="03a14-200">R. : Oui.</span><span class="sxs-lookup"><span data-stu-id="03a14-200">A: Yes.</span></span> <span data-ttu-id="03a14-201">Vous pouvez définir la valeur hello un tooenable de clé de Registre il.</span><span class="sxs-lookup"><span data-stu-id="03a14-201">You can set hello value of a registry key tooenable it.</span></span> <span data-ttu-id="03a14-202">Consultez [tooenable un tooOMS de données non contrôleur de domaine toosend AD](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).</span><span class="sxs-lookup"><span data-stu-id="03a14-202">See [tooenable a non-domain controller toosend AD data tooOMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).</span></span>

<span data-ttu-id="03a14-203">**Q : qu’est nom hello du processus hello qui hello collecte de données ?**</span><span class="sxs-lookup"><span data-stu-id="03a14-203">**Q: What is hello name of hello process that does hello data collection?**</span></span>
<span data-ttu-id="03a14-204">R : AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="03a14-204">A: AdvisorAssessment.exe</span></span>

<span data-ttu-id="03a14-205">**Q : combien de temps faut-il pour toobe des données collectée ?**</span><span class="sxs-lookup"><span data-stu-id="03a14-205">**Q: How long does it take for data toobe collected?**</span></span>
<span data-ttu-id="03a14-206">R : heure de collecte de données de dépend de taille hello d’environnement Active Directory de hello, mais prend généralement moins de 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="03a14-206">A: Data collection time depends on hello size of hello Active Directory environment, but usually takes less than 15 minutes.</span></span>

<span data-ttu-id="03a14-207">**Q : Quels types de données sont collectés ?**</span><span class="sxs-lookup"><span data-stu-id="03a14-207">**Q: What type of data is collected?**</span></span>
<span data-ttu-id="03a14-208">R : Les informations de réplication sont recueillies par le biais de LDAP.</span><span class="sxs-lookup"><span data-stu-id="03a14-208">A: Replication information is collected via LDAP.</span></span>

<span data-ttu-id="03a14-209">**Q : existe-t-il un moyen tooconfigure lorsque les données sont collectées ?**</span><span class="sxs-lookup"><span data-stu-id="03a14-209">**Q: Is there a way tooconfigure when data is collected?**</span></span>
<span data-ttu-id="03a14-210">R : Pas pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="03a14-210">A: Not at this time.</span></span>

<span data-ttu-id="03a14-211">**Q : que faire autorisations ai-je besoin toocollect données ?**</span><span class="sxs-lookup"><span data-stu-id="03a14-211">**Q: What permissions do I need toocollect data?**</span></span>
<span data-ttu-id="03a14-212">A: tooActive d’autorisations utilisateur normal active sont suffisants.</span><span class="sxs-lookup"><span data-stu-id="03a14-212">A: Normal user permissions tooActive Directory are sufficient.</span></span>

## <a name="troubleshoot-data-collection-problems"></a><span data-ttu-id="03a14-213">Résoudre les problèmes de collecte de données</span><span class="sxs-lookup"><span data-stu-id="03a14-213">Troubleshoot data collection problems</span></span>
<span data-ttu-id="03a14-214">Dans les données de la commande toocollect pack de solution d’état de réplication hello AD requiert au moins un domaine contrôleur toobe connecté tooyour espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="03a14-214">In order toocollect data, hello AD Replication Status solution pack requires at least one domain controller toobe connected tooyour OMS workspace.</span></span> <span data-ttu-id="03a14-215">Un message indiquant que **les données sont toujours en cours de collecte** s’affiche tant que vous n’avez pas connecté de contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="03a14-215">Until you connect a domain controller, a message appears indicating that **data is still being collected**.</span></span>

<span data-ttu-id="03a14-216">Si vous avez besoin d’assistance de connexion d’un de vos contrôleurs de domaine, vous pouvez afficher la documentation à l’adresse [tooLog d’ordinateurs Windows de se connecter Analytique](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="03a14-216">If you need assistance connecting one of your domain controllers, you can view documentation at [Connect Windows computers tooLog Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="03a14-217">Vous pouvez également, si votre contrôleur de domaine est déjà connecté tooan d’environnement System Center Operations Manager, vous pouvez afficher la documentation à [connecter System Center Operations Manager tooLog Analytique](log-analytics-om-agents.md).</span><span class="sxs-lookup"><span data-stu-id="03a14-217">Alternatively, if your domain controller is already connected tooan existing System Center Operations Manager environment, you can view documentation at [Connect System Center Operations Manager tooLog Analytics](log-analytics-om-agents.md).</span></span>

<span data-ttu-id="03a14-218">Si vous ne souhaitez tooconnect un de vos contrôleurs de domaine directement tooOMS ou tooSCOM, consultez [tooenable un tooOMS de données non contrôleur de domaine toosend AD](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).</span><span class="sxs-lookup"><span data-stu-id="03a14-218">If you don't want tooconnect any of your domain controllers directly tooOMS or tooSCOM, see [tooenable a non-domain controller toosend AD data tooOMS](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="03a14-219">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="03a14-219">Next steps</span></span>
* <span data-ttu-id="03a14-220">Utilisez [connecter recherche Analytique de journal](log-analytics-log-searches.md) tooview détaillé les données d’état de réplication Active Directory.</span><span class="sxs-lookup"><span data-stu-id="03a14-220">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Active Directory Replication status data.</span></span>