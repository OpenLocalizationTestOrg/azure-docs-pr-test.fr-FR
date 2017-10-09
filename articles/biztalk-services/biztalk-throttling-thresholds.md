---
title: aaaLearn sur la limitation dans BizTalk Services | Documents Microsoft
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
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="21afa-105">Limitation BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="21afa-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="21afa-106">Les Services BizTalk Azure implémente la basée sur les deux conditions de limitation de service : numéro hello et l’utilisation de mémoire de traitement de messages simultanés.</span><span class="sxs-lookup"><span data-stu-id="21afa-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and hello number of simultaneous messages processing.</span></span> <span data-ttu-id="21afa-107">Cette rubrique répertorie les seuils de limitation de hello et décrit le comportement d’exécution hello lorsqu’une condition de limitation se produit.</span><span class="sxs-lookup"><span data-stu-id="21afa-107">This topic lists hello throttling thresholds and describes hello Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="21afa-108">Seuils de limitation</span><span class="sxs-lookup"><span data-stu-id="21afa-108">Throttling Thresholds</span></span>
<span data-ttu-id="21afa-109">Hello tableau ci-dessous répertorie hello limitation source et les seuils :</span><span class="sxs-lookup"><span data-stu-id="21afa-109">hello following table lists hello throttling source and thresholds:</span></span>

|  | <span data-ttu-id="21afa-110">Description</span><span class="sxs-lookup"><span data-stu-id="21afa-110">Description</span></span> | <span data-ttu-id="21afa-111">Seuil minimum</span><span class="sxs-lookup"><span data-stu-id="21afa-111">Low Threshold</span></span> | <span data-ttu-id="21afa-112">Seuil maximum</span><span class="sxs-lookup"><span data-stu-id="21afa-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21afa-113">Mémoire</span><span class="sxs-lookup"><span data-stu-id="21afa-113">Memory</span></span> |<span data-ttu-id="21afa-114">Pourcentage de la mémoire système totale disponible/PageFileBytes (octets de fichier de page).</span><span class="sxs-lookup"><span data-stu-id="21afa-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="21afa-115">PageFileBytes disponible totale est d’environ 2 fois hello RAM du système de hello.</span><span class="sxs-lookup"><span data-stu-id="21afa-115">Total available PageFileBytes is approximately 2 times hello RAM of hello system.</span></span> |<span data-ttu-id="21afa-116">60 %</span><span class="sxs-lookup"><span data-stu-id="21afa-116">60%</span></span> |<span data-ttu-id="21afa-117">70 %</span><span class="sxs-lookup"><span data-stu-id="21afa-117">70%</span></span> |
| <span data-ttu-id="21afa-118">Traitement de message</span><span class="sxs-lookup"><span data-stu-id="21afa-118">Message Processing</span></span> |<span data-ttu-id="21afa-119">Nombre de messages traités simultanément</span><span class="sxs-lookup"><span data-stu-id="21afa-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="21afa-120">40 * nombre de cœurs</span><span class="sxs-lookup"><span data-stu-id="21afa-120">40 * number of cores</span></span> |<span data-ttu-id="21afa-121">100 * nombre de cœurs</span><span class="sxs-lookup"><span data-stu-id="21afa-121">100 * number of cores</span></span> |

<span data-ttu-id="21afa-122">Lorsqu’un seuil élevé est atteint, Azure BizTalk Services démarre toothrottle.</span><span class="sxs-lookup"><span data-stu-id="21afa-122">When a high threshold is reached, Azure BizTalk Services starts toothrottle.</span></span> <span data-ttu-id="21afa-123">La limitation s’arrête lorsque hello faible est atteint.</span><span class="sxs-lookup"><span data-stu-id="21afa-123">Throttling stops when hello low threshold is reached.</span></span> <span data-ttu-id="21afa-124">Par exemple, votre service utilise 65 % de la mémoire système.</span><span class="sxs-lookup"><span data-stu-id="21afa-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="21afa-125">Dans ce cas, le service de hello ne limite pas.</span><span class="sxs-lookup"><span data-stu-id="21afa-125">In this situation, hello service does not throttle.</span></span> <span data-ttu-id="21afa-126">Votre service monte à 70 % d'utilisation de mémoire système.</span><span class="sxs-lookup"><span data-stu-id="21afa-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="21afa-127">Dans ce cas, service de hello limite et continue toothrottle jusqu'à ce que le service de hello utilise la mémoire de système de 60 % (seuil faible).</span><span class="sxs-lookup"><span data-stu-id="21afa-127">In this situation, hello service throttles and continues toothrottle until hello service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="21afa-128">Azure BizTalk Services effectue le suivi hello (état normal et l’état d’accélérée) d’état de limitation et hello durée de limitation.</span><span class="sxs-lookup"><span data-stu-id="21afa-128">Azure BizTalk Services tracks hello throttling status (normal state vs. throttled state) and hello throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="21afa-129">Comportement d'exécution</span><span class="sxs-lookup"><span data-stu-id="21afa-129">Runtime Behavior</span></span>
<span data-ttu-id="21afa-130">Quand Azure BizTalk Services entre dans un état de limitation, hello événements suivants se produisent :</span><span class="sxs-lookup"><span data-stu-id="21afa-130">When Azure BizTalk Services enters a throttling state, hello following occurs:</span></span>

* <span data-ttu-id="21afa-131">La limitation s'effectue par instance de rôle.</span><span class="sxs-lookup"><span data-stu-id="21afa-131">Throttling is per role instance.</span></span> <span data-ttu-id="21afa-132">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="21afa-132">For example:</span></span><br/>
  <span data-ttu-id="21afa-133">L'instance RoleInstanceA est limitée.</span><span class="sxs-lookup"><span data-stu-id="21afa-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="21afa-134">L'instance RoleInstanceB ne l'est pas.</span><span class="sxs-lookup"><span data-stu-id="21afa-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="21afa-135">Dans ce cas, les messages dans RoleInstanceB sont traités normalement.</span><span class="sxs-lookup"><span data-stu-id="21afa-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="21afa-136">Messages dans RoleInstanceA sont ignorés et échouent avec hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="21afa-136">Messages in RoleInstanceA are discarded and fail with hello following error:</span></span><br/><br/><span data-ttu-id="21afa-137">
  **Le serveur est occupé. Réessayez.**</span><span class="sxs-lookup"><span data-stu-id="21afa-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="21afa-138">Les sources d'extraction cessent d'interroger et de télécharger les messages.</span><span class="sxs-lookup"><span data-stu-id="21afa-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="21afa-139">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="21afa-139">For example:</span></span><br/>
  <span data-ttu-id="21afa-140">Un pipeline extrait les messages depuis une source FTP externe.</span><span class="sxs-lookup"><span data-stu-id="21afa-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="21afa-141">instance de rôle Hello effectuant l’extraction de hello Obtient dans un état de limitation.</span><span class="sxs-lookup"><span data-stu-id="21afa-141">hello role instance doing hello pull gets into a throttling state.</span></span> <span data-ttu-id="21afa-142">Dans ce cas, le pipeline de hello arrête le téléchargement des messages supplémentaires jusqu'à ce que l’instance de rôle hello arrête la limitation.</span><span class="sxs-lookup"><span data-stu-id="21afa-142">In this situation, hello pipeline stops downloading additional messages until hello role instance stops throttling.</span></span>
* <span data-ttu-id="21afa-143">Une réponse est envoyée toohello client pour le client de hello peut renvoyer le message de type hello.</span><span class="sxs-lookup"><span data-stu-id="21afa-143">A response is sent toohello client so hello client can resubmit hello message.</span></span>
* <span data-ttu-id="21afa-144">Vous devez attendre jusqu'à ce que la limitation de hello est résolue.</span><span class="sxs-lookup"><span data-stu-id="21afa-144">You must wait until hello throttling is resolved.</span></span> <span data-ttu-id="21afa-145">Plus précisément, vous devez attendre jusqu'à ce que hello faible est atteint.</span><span class="sxs-lookup"><span data-stu-id="21afa-145">Specifically, you must wait until hello low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="21afa-146">Remarques importantes</span><span class="sxs-lookup"><span data-stu-id="21afa-146">Important notes</span></span>
* <span data-ttu-id="21afa-147">Il n'est pas possible de désactiver la limitation.</span><span class="sxs-lookup"><span data-stu-id="21afa-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="21afa-148">Il n'est pas possible de modifier les seuils de limitation.</span><span class="sxs-lookup"><span data-stu-id="21afa-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="21afa-149">La limitation est déployée sur l'ensemble du système.</span><span class="sxs-lookup"><span data-stu-id="21afa-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="21afa-150">Hello, serveur de base de données SQL Azure a également la limitation intégrés.</span><span class="sxs-lookup"><span data-stu-id="21afa-150">hello Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="21afa-151">Autres rubriques Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="21afa-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="21afa-152">Lors de l’installation Bonjour Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="21afa-152">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="21afa-153">Didacticiels : Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="21afa-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="21afa-154">Comment puis-je démarrer à l’aide de hello SDK des Services BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="21afa-154">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="21afa-155">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="21afa-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="21afa-156">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="21afa-156">See Also</span></span>
* [<span data-ttu-id="21afa-157">Tableau comparatif des éditions Développeur, De base, Standard et Premium de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="21afa-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="21afa-158">BizTalk Services : approvisionnement à l’aide du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="21afa-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="21afa-159">Tableau comparatif des états d'approvisionnement BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="21afa-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="21afa-160">Onglets Tableau de bord, Surveiller et Mettre à l'échelle dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="21afa-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="21afa-161">Sauvegarde et restauration de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="21afa-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="21afa-162">Nom et clé de l'émetteur dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="21afa-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

