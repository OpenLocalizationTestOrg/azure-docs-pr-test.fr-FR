---
title: Prise en charge de HTTP/2 dans Azure CDN | Microsoft Docs
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
ms.openlocfilehash: 4f8dd685c3ae89535217d7a17a01c5129ca7e6e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="http2-support-in-azure-cdn"></a><span data-ttu-id="8d4fd-103">Prise en charge de HTTP/2 dans Azure CDN</span><span class="sxs-lookup"><span data-stu-id="8d4fd-103">HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="8d4fd-104">HTTP/2 est une révision majeure au HTTP/1.1\.</span><span class="sxs-lookup"><span data-stu-id="8d4fd-104">HTTP/2 is a major revision to HTTP/1.1\.</span></span> <span data-ttu-id="8d4fd-105">Il fournit plus rapide d’expérience utilisateur améliorée, temps de réponse réduit et performances de site web, tout en conservant les méthodes HTTP familières, les codes d’état et sémantique.</span><span class="sxs-lookup"><span data-stu-id="8d4fd-105">It provides faster web performance, reduced response time, and improved user experience, while maintaining the familiar HTTP methods, status codes, and semantics.</span></span> <span data-ttu-id="8d4fd-106">Bien que HTTP/2 soit conçu pour fonctionner avec HTTP et HTTPS, de nombreux navigateurs web clients prennent en charge seulement HTTP/2 sur TLS.</span><span class="sxs-lookup"><span data-stu-id="8d4fd-106">Though HTTP/2 is designed to work with HTTP and HTTPS, many client web browsers only support HTTP/2 over TLS.</span></span>

###<a name="http2-benefits"></a><span data-ttu-id="8d4fd-107">Avantages de HTTP/2</span><span class="sxs-lookup"><span data-stu-id="8d4fd-107">HTTP/2 Benefits</span></span>

<span data-ttu-id="8d4fd-108">Les avantages de HTTP/2 sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="8d4fd-108">The benefits of HTTP/2 include:</span></span>

*   <span data-ttu-id="8d4fd-109">**Multiplexage et accès concurrentiel**</span><span class="sxs-lookup"><span data-stu-id="8d4fd-109">**Multiplexing and concurrency**</span></span>

    <span data-ttu-id="8d4fd-110">Avec HTTP 1.1, effectuer plusieurs demandes de ressources nécessite plusieurs connexions TCP, et chaque connexion représente une surcharge qui a un impact sur les performances.</span><span class="sxs-lookup"><span data-stu-id="8d4fd-110">Using HTTP 1.1, multiple making multiple resource requests requires multiple TCP connections, and each connection has performance overhead associated with it.</span></span> <span data-ttu-id="8d4fd-111">HTTP/2 permet de demander plusieurs ressources sur une même connexion TCP.</span><span class="sxs-lookup"><span data-stu-id="8d4fd-111">HTTP/2 allows multiple resources to be requested on a single TCP connection.</span></span>

*   <span data-ttu-id="8d4fd-112">**Compression des en-têtes**</span><span class="sxs-lookup"><span data-stu-id="8d4fd-112">**Header compression**</span></span>

    <span data-ttu-id="8d4fd-113">Grâce à la compression des en-têtes HTTP pour les ressources traitées, le temps passé sur le réseau est sensiblement réduit.</span><span class="sxs-lookup"><span data-stu-id="8d4fd-113">By compressing the HTTP headers for served resources, time on the wire is reduced significantly.</span></span>

*   <span data-ttu-id="8d4fd-114">**Dépendances de flux**</span><span class="sxs-lookup"><span data-stu-id="8d4fd-114">**Stream dependencies**</span></span>

    <span data-ttu-id="8d4fd-115">Les dépendances de flux permettent au client indiquer au serveur quelles ressources ont la priorité.</span><span class="sxs-lookup"><span data-stu-id="8d4fd-115">Stream dependencies allow the client to indicate to the server which of resources have priority.</span></span>


##<a name="http2-browser-support"></a><span data-ttu-id="8d4fd-116">Prise en charge de HTTP/2 par les navigateurs</span><span class="sxs-lookup"><span data-stu-id="8d4fd-116">HTTP/2 Browser Support</span></span>

<span data-ttu-id="8d4fd-117">Tous les principaux navigateurs ont implémenté la prise en charge de HTTP/2 dans leur version actuelle.</span><span class="sxs-lookup"><span data-stu-id="8d4fd-117">All of the major browsers have implemented HTTP/2 support in their current versions.</span></span> <span data-ttu-id="8d4fd-118">Les navigateurs non pris en charge passent automatiquement à HTTP/1.1.</span><span class="sxs-lookup"><span data-stu-id="8d4fd-118">Non-supported browsers will automatically fallback to HTTP/1.1.</span></span>

|<span data-ttu-id="8d4fd-119">Browser</span><span class="sxs-lookup"><span data-stu-id="8d4fd-119">Browser</span></span>|<span data-ttu-id="8d4fd-120">Version minimale</span><span class="sxs-lookup"><span data-stu-id="8d4fd-120">Minimum Version</span></span>|
|-------------|------------|
|<span data-ttu-id="8d4fd-121">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="8d4fd-121">Microsoft Edge</span></span>| <span data-ttu-id="8d4fd-122">12</span><span class="sxs-lookup"><span data-stu-id="8d4fd-122">12</span></span>|
|<span data-ttu-id="8d4fd-123">Google Chrome</span><span class="sxs-lookup"><span data-stu-id="8d4fd-123">Google Chrome</span></span>| <span data-ttu-id="8d4fd-124">43</span><span class="sxs-lookup"><span data-stu-id="8d4fd-124">43</span></span>|
|<span data-ttu-id="8d4fd-125">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="8d4fd-125">Mozilla Firefox</span></span>| <span data-ttu-id="8d4fd-126">38</span><span class="sxs-lookup"><span data-stu-id="8d4fd-126">38</span></span>|
|<span data-ttu-id="8d4fd-127">Opera</span><span class="sxs-lookup"><span data-stu-id="8d4fd-127">Opera</span></span>| <span data-ttu-id="8d4fd-128">32</span><span class="sxs-lookup"><span data-stu-id="8d4fd-128">32</span></span>|
|<span data-ttu-id="8d4fd-129">Safari</span><span class="sxs-lookup"><span data-stu-id="8d4fd-129">Safari</span></span>| <span data-ttu-id="8d4fd-130">9</span><span class="sxs-lookup"><span data-stu-id="8d4fd-130">9</span></span>|

##<a name="enabling-http2-support-in-azure-cdn"></a><span data-ttu-id="8d4fd-131">Activation de la prise en charge de HTTP/2 dans Azure CDN</span><span class="sxs-lookup"><span data-stu-id="8d4fd-131">Enabling HTTP/2 Support in Azure CDN</span></span>

<span data-ttu-id="8d4fd-132">La prise en charge HTTP/2 est actuellement active pour les profils **Azure CDN d’Akamai** et **Azure CDN de Verizon**.</span><span class="sxs-lookup"><span data-stu-id="8d4fd-132">Currently HTTP/2 support is active for **Azure CDN from Akamai** and **Azure CDN from Verizon** profiles.</span></span> <span data-ttu-id="8d4fd-133">Aucune action supplémentaire n’est nécessaire de la part des clients.</span><span class="sxs-lookup"><span data-stu-id="8d4fd-133">No further action is required from customers.</span></span>

##<a name="next-steps"></a><span data-ttu-id="8d4fd-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8d4fd-134">Next Steps</span></span>

<span data-ttu-id="8d4fd-135">Pour voir les avantages de HTTP/2 en situation, consultez [cette démonstration d’Akamai](https://http2.akamai.com/demo).</span><span class="sxs-lookup"><span data-stu-id="8d4fd-135">To see the benefits of HTTP/2 in action, see [this demo from Akamai](https://http2.akamai.com/demo).</span></span>

<span data-ttu-id="8d4fd-136">Pour en savoir plus sur les HTTP/2, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="8d4fd-136">To learn more about HTTP/2, visit the following resources:</span></span>

*   [<span data-ttu-id="8d4fd-137">Page d’accueil de la spécification HTTP/2</span><span class="sxs-lookup"><span data-stu-id="8d4fd-137">HTTP/2 specification homepage</span></span>](https://http2.github.io/)
*   [<span data-ttu-id="8d4fd-138">Forum Aux Questions officiel de HTTP/2</span><span class="sxs-lookup"><span data-stu-id="8d4fd-138">Official HTTP/2 FAQ</span></span>](https://http2.github.io/faq/)
*   [<span data-ttu-id="8d4fd-139">Informations sur HTTP/2 d’Akamai</span><span class="sxs-lookup"><span data-stu-id="8d4fd-139">Akamai HTTP/2 information</span></span>](https://http2.akamai.com/)

<span data-ttu-id="8d4fd-140">Pour plus d’informations sur les fonctionnalités disponibles dans Azure CDN, consultez [Vue d’ensemble du réseau de distribution de contenu (CDN) Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span><span class="sxs-lookup"><span data-stu-id="8d4fd-140">To learn more about Azure CDN's available features, see the [Azure CDN Overview](https://azure.microsoft.com/documentation/articles/cdn-overview/).</span></span>