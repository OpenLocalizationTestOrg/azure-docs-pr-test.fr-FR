---
title: "En savoir plus sur la limitation dans BizTalk Services | Microsoft Docs"
description: "En savoir plus sur les seuils de limitation et les comportements qui s'ensuivent lors de l'exécution pour BizTalk Services. La limitation est basée sur l'utilisation de la mémoire et le nombre de messages. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 145e7470bbc01c676a1fb5856c0f9a8726e667fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="2e4b2-105">Limitation BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="2e4b2-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="2e4b2-106">Azure BizTalk Services met en place un service de limitation basé sur deux conditions : l’utilisation de la mémoire et le nombre de messages traités simultanément.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and the number of simultaneous messages processing.</span></span> <span data-ttu-id="2e4b2-107">Cette rubrique répertorie les seuils de limitation et décrit le comportement d’exécution lorsque les conditions de limitation sont réunies.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-107">This topic lists the throttling thresholds and describes the Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="2e4b2-108">Seuils de limitation</span><span class="sxs-lookup"><span data-stu-id="2e4b2-108">Throttling Thresholds</span></span>
<span data-ttu-id="2e4b2-109">Le tableau suivant répertorie les sources et seuils de limitation :</span><span class="sxs-lookup"><span data-stu-id="2e4b2-109">The following table lists the throttling source and thresholds:</span></span>

|  | <span data-ttu-id="2e4b2-110">Description</span><span class="sxs-lookup"><span data-stu-id="2e4b2-110">Description</span></span> | <span data-ttu-id="2e4b2-111">Seuil minimum</span><span class="sxs-lookup"><span data-stu-id="2e4b2-111">Low Threshold</span></span> | <span data-ttu-id="2e4b2-112">Seuil maximum</span><span class="sxs-lookup"><span data-stu-id="2e4b2-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2e4b2-113">Mémoire</span><span class="sxs-lookup"><span data-stu-id="2e4b2-113">Memory</span></span> |<span data-ttu-id="2e4b2-114">Pourcentage de la mémoire système totale disponible/PageFileBytes (octets de fichier de page).</span><span class="sxs-lookup"><span data-stu-id="2e4b2-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="2e4b2-115">Le total de PageFileBytes disponible correspond environ à 2 fois la mémoire RAM du système.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-115">Total available PageFileBytes is approximately 2 times the RAM of the system.</span></span> |<span data-ttu-id="2e4b2-116">60 %</span><span class="sxs-lookup"><span data-stu-id="2e4b2-116">60%</span></span> |<span data-ttu-id="2e4b2-117">70 %</span><span class="sxs-lookup"><span data-stu-id="2e4b2-117">70%</span></span> |
| <span data-ttu-id="2e4b2-118">Traitement de message</span><span class="sxs-lookup"><span data-stu-id="2e4b2-118">Message Processing</span></span> |<span data-ttu-id="2e4b2-119">Nombre de messages traités simultanément</span><span class="sxs-lookup"><span data-stu-id="2e4b2-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="2e4b2-120">40 * nombre de cœurs</span><span class="sxs-lookup"><span data-stu-id="2e4b2-120">40 * number of cores</span></span> |<span data-ttu-id="2e4b2-121">100 * nombre de cœurs</span><span class="sxs-lookup"><span data-stu-id="2e4b2-121">100 * number of cores</span></span> |

<span data-ttu-id="2e4b2-122">Lorsqu'un seuil maximal est atteint, Azure BizTalk Services active les limitations.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-122">When a high threshold is reached, Azure BizTalk Services starts to throttle.</span></span> <span data-ttu-id="2e4b2-123">La limitation s'arrête une fois le seuil minimal atteint.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-123">Throttling stops when the low threshold is reached.</span></span> <span data-ttu-id="2e4b2-124">Par exemple, votre service utilise 65 % de la mémoire système.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="2e4b2-125">Dans ce cas, le service n'utilise pas de limitation.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-125">In this situation, the service does not throttle.</span></span> <span data-ttu-id="2e4b2-126">Votre service monte à 70 % d'utilisation de mémoire système.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="2e4b2-127">Dans ce cas, le service lance une limitation et continue de l'appliquer jusqu'à ce que le service utilise 60 % (seuil minimal) de la mémoire système.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-127">In this situation, the service throttles and continues to throttle until the service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="2e4b2-128">Azure BizTalk Services assure le suivi du statut de la limitation (état normal contre état limité) et de la durée de la limitation.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-128">Azure BizTalk Services tracks the throttling status (normal state vs. throttled state) and the throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="2e4b2-129">Comportement d'exécution</span><span class="sxs-lookup"><span data-stu-id="2e4b2-129">Runtime Behavior</span></span>
<span data-ttu-id="2e4b2-130">Lorsque Azure BizTalk Services passe en mode limitation, les actions suivantes se produisent :</span><span class="sxs-lookup"><span data-stu-id="2e4b2-130">When Azure BizTalk Services enters a throttling state, the following occurs:</span></span>

* <span data-ttu-id="2e4b2-131">La limitation s'effectue par instance de rôle.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-131">Throttling is per role instance.</span></span> <span data-ttu-id="2e4b2-132">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2e4b2-132">For example:</span></span><br/>
  <span data-ttu-id="2e4b2-133">L'instance RoleInstanceA est limitée.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="2e4b2-134">L'instance RoleInstanceB ne l'est pas.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="2e4b2-135">Dans ce cas, les messages dans RoleInstanceB sont traités normalement.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="2e4b2-136">Les messages dans RoleInstanceA sont ignorés et le message d'erreur suivant est affiché :</span><span class="sxs-lookup"><span data-stu-id="2e4b2-136">Messages in RoleInstanceA are discarded and fail with the following error:</span></span><br/><br/><span data-ttu-id="2e4b2-137">
  **Le serveur est occupé. Réessayez.**</span><span class="sxs-lookup"><span data-stu-id="2e4b2-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="2e4b2-138">Les sources d'extraction cessent d'interroger et de télécharger les messages.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="2e4b2-139">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="2e4b2-139">For example:</span></span><br/>
  <span data-ttu-id="2e4b2-140">Un pipeline extrait les messages depuis une source FTP externe.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="2e4b2-141">L'instance de rôle responsable de l'extraction passe en mode limité.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-141">The role instance doing the pull gets into a throttling state.</span></span> <span data-ttu-id="2e4b2-142">Dans cette situation, le pipeline cesse de télécharger de nouveaux messages tant que l'instance de rôle est limitée.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-142">In this situation, the pipeline stops downloading additional messages until the role instance stops throttling.</span></span>
* <span data-ttu-id="2e4b2-143">Une réponse est envoyée au client afin qu'il puisse soumettre le message de nouveau.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-143">A response is sent to the client so the client can resubmit the message.</span></span>
* <span data-ttu-id="2e4b2-144">Vous devez patienter jusqu'à la fin de la limitation.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-144">You must wait until the throttling is resolved.</span></span> <span data-ttu-id="2e4b2-145">Plus précisément, vous devez attendre que le seuil minimal soit atteint.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-145">Specifically, you must wait until the low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="2e4b2-146">Remarques importantes</span><span class="sxs-lookup"><span data-stu-id="2e4b2-146">Important notes</span></span>
* <span data-ttu-id="2e4b2-147">Il n'est pas possible de désactiver la limitation.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="2e4b2-148">Il n'est pas possible de modifier les seuils de limitation.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="2e4b2-149">La limitation est déployée sur l'ensemble du système.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="2e4b2-150">Le serveur de base de données SQL d'Azure comporte également un dispositif de limitation intégré.</span><span class="sxs-lookup"><span data-stu-id="2e4b2-150">The Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="2e4b2-151">Autres rubriques Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="2e4b2-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="2e4b2-152">Installation du Kit de développement logiciel (SDK) Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="2e4b2-152">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="2e4b2-153">Didacticiels : Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="2e4b2-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="2e4b2-154">Utilisation du Kit de développement logiciel (SDK) Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="2e4b2-154">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="2e4b2-155">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="2e4b2-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="2e4b2-156">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="2e4b2-156">See Also</span></span>
* [<span data-ttu-id="2e4b2-157">Tableau comparatif des éditions Développeur, De base, Standard et Premium de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="2e4b2-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="2e4b2-158">BizTalk Services : approvisionnement à l’aide du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="2e4b2-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="2e4b2-159">Tableau comparatif des états d'approvisionnement BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="2e4b2-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="2e4b2-160">Onglets Tableau de bord, Surveiller et Mettre à l'échelle dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="2e4b2-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="2e4b2-161">Sauvegarde et restauration de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="2e4b2-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="2e4b2-162">Nom et clé de l'émetteur dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="2e4b2-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

