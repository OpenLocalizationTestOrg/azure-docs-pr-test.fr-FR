---
title: "prise en charge d’aaaHTTP/2 dans Azure CDN | Documents Microsoft"
description: En savoir plus sur la prise en charge de HTTP/2 et de CDN.
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="f317d-103">Prise en charge de HTTP/2 dans Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f317d-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="f317d-104">HTTP/2 est un tooHTTP/1.1\ révision majeure.</span><span class="sxs-lookup"><span data-stu-id="f317d-104">HTTP/2 is a major revision tooHTTP/1.1\.</span></span> <span data-ttu-id="f317d-105">Il fournit plus rapide d’expérience utilisateur améliorée, temps de réponse réduit et performances de site web, tout en conservant les méthodes HTTP familières hello, les codes d’état et sémantique.</span><span class="sxs-lookup"><span data-stu-id="f317d-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining hello familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="f317d-106">Bien que HTTP/2 est conçue toowork HTTP et HTTPS, de nombreux navigateurs web de client prennent uniquement en charge HTTP/2 sur TLS.</span><span class="sxs-lookup"><span data-stu-id="f317d-106">Though HTTP/2 is designed toowork with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="f317d-107">Avantages de HTTP/2</span><span class="sxs-lookup"><span data-stu-id="f317d-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="f317d-108">avantages de Hello de HTTP/2 :</span><span class="sxs-lookup"><span data-stu-id="f317d-108">hello benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="f317d-109">**Multiplexage et accès concurrentiel**</span><span class="sxs-lookup"><span data-stu-id="f317d-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="f317d-110">Avec HTTP 1.1, effectuer plusieurs demandes de ressources nécessite plusieurs connexions TCP, et chaque connexion représente une surcharge qui a un impact sur les performances.</span><span class="sxs-lookup"><span data-stu-id="f317d-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="f317d-111">HTTP/2 permet à plusieurs ressources toobe demandé sur une connexion TCP unique.</span><span class="sxs-lookup"><span data-stu-id="f317d-111">HTTP/2 allows multiple resources toobe requested on a single TCP connection.</span></span>

*   <span data-ttu-id="f317d-112">**Compression des en-têtes**</span><span class="sxs-lookup"><span data-stu-id="f317d-112">**Header compression**</span></span>

    <span data-ttu-id="f317d-113">Par la compression des en-têtes hello HTTP pour les ressources traitées, l’heure sur le câble de hello est sensiblement réduit.</span><span class="sxs-lookup"><span data-stu-id="f317d-113">By compressing hello HTTP headers for served resources, time on hello wire is reduced significantly.</span></span>

*   <span data-ttu-id="f317d-114">**Dépendances de flux**</span><span class="sxs-lookup"><span data-stu-id="f317d-114">**Stream dependencies**</span></span>

    <span data-ttu-id="f317d-115">Dépendances de flux de données permettent de client de hello tooindicate toohello server, qui ont la priorité des ressources.</span><span class="sxs-lookup"><span data-stu-id="f317d-115">Stream dependencies allow hello client tooindicate toohello server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="f317d-116">Prise en charge de HTTP/2 par les navigateurs</span><span class="sxs-lookup"><span data-stu-id="f317d-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="f317d-117">Tous les navigateurs principaux hello ont implémenté la prise en charge HTTP/2 dans leur version actuelle.</span><span class="sxs-lookup"><span data-stu-id="f317d-117">All of hello major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="f317d-118">Non pris en charge des navigateurs seront automatiquement secours tooHTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="f317d-118">Non-supported browsers will automatically fallback tooHTTP/1.1.</span></span>

|<span data-ttu-id="f317d-119">Browser</span><span class="sxs-lookup"><span data-stu-id="f317d-119">Browser</span></span>|<span data-ttu-id="f317d-120">Version minimale</span><span class="sxs-lookup"><span data-stu-id="f317d-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="f317d-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="f317d-121">Microsoft Edge</span></span>| <span data-ttu-id="f317d-122">12</span><span class="sxs-lookup"><span data-stu-id="f317d-122">12</span></span>|
|<span data-ttu-id="f317d-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="f317d-123">Google Chrome</span></span>| <span data-ttu-id="f317d-124">43</span><span class="sxs-lookup"><span data-stu-id="f317d-124">43</span></span>|
|<span data-ttu-id="f317d-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="f317d-125">Mozilla Firefox</span></span>| <span data-ttu-id="f317d-126">38</span><span class="sxs-lookup"><span data-stu-id="f317d-126">38</span></span>|
|<span data-ttu-id="f317d-127">Opera</span><span class="sxs-lookup"><span data-stu-id="f317d-127">Opera</span></span>| <span data-ttu-id="f317d-128">32</span><span class="sxs-lookup"><span data-stu-id="f317d-128">32</span></span>|
|<span data-ttu-id="f317d-129">Safari</span><span class="sxs-lookup"><span data-stu-id="f317d-129">Safari</span></span>| <span data-ttu-id="f317d-130">9</span><span class="sxs-lookup"><span data-stu-id="f317d-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="f317d-131">Activation de la prise en charge de HTTP/2 dans Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f317d-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="f317d-132">La prise en charge HTTP/2 est actuellement active pour les profils **Azure CDN d’Akamai** et **Azure CDN de Verizon**.</span><span class="sxs-lookup"><span data-stu-id="f317d-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="f317d-133">Aucune action supplémentaire n’est nécessaire de la part des clients.</span><span class="sxs-lookup"><span data-stu-id="f317d-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="f317d-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f317d-134">Next Steps</span></span>

<span data-ttu-id="f317d-135">avantages de hello toosee de HTTP/2 en action, consultez [cette démonstration d’Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="f317d-135">toosee hello benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="f317d-136">toolearn plus de HTTP/2, visitez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="f317d-136">toolearn more about HTTP/2, visit hello following resources:</span></span>

*   [<span data-ttu-id="f317d-137">Page d’accueil de la spécification HTTP/2</span><span class="sxs-lookup"><span data-stu-id="f317d-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="f317d-138">Forum Aux Questions officiel de HTTP/2</span><span class="sxs-lookup"><span data-stu-id="f317d-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="f317d-139">Informations sur HTTP/2 d’Akamai</span><span class="sxs-lookup"><span data-stu-id="f317d-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="f317d-140">toolearn savoir plus sur les fonctionnalités disponibles du CDN Azure, consultez hello [vue d’ensemble du CDN Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="f317d-140">toolearn more about Azure CDN's available features, see hello [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>
