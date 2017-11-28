---
title: aaaUnderstanding DNS dans la pile de Azure | Documents Microsoft
description: "Présentation des fonctionnalités DNS dans Azure Stack"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 60f5ac85-be19-49ac-a7c1-f290d682b5de
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: scottnap
ms.openlocfilehash: f60128cf98af8e98ac2bc87172b54132ed06cd8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-idns-for-azure-stack"></a><span data-ttu-id="d42cd-103">Présentation d’iDNS pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="d42cd-103">Introducing iDNS for Azure Stack</span></span>
================================

<span data-ttu-id="d42cd-104">noms de domaines internationaux est une fonctionnalité de pile Azure qui vous permet de tooresolve des noms DNS externes (par exemple, http://www.bing.com).</span><span class="sxs-lookup"><span data-stu-id="d42cd-104">iDNS is a feature in Azure Stack that allows you tooresolve external DNS names (such as http://www.bing.com).</span></span>
<span data-ttu-id="d42cd-105">Il vous permet également les noms de réseau virtuel interne tooregister.</span><span class="sxs-lookup"><span data-stu-id="d42cd-105">It also allows you tooregister internal virtual network names.</span></span> <span data-ttu-id="d42cd-106">En procédant ainsi, vous pouvez résoudre des machines virtuelles sur le même réseau virtuel par nom plutôt que par IP adresse, sans avoir tooprovide entrées de serveur DNS personnalisées de hello.</span><span class="sxs-lookup"><span data-stu-id="d42cd-106">By doing so, you can resolve VMs on hello same virtual network by name rather than IP address, without having tooprovide custom DNS server entries.</span></span>

<span data-ttu-id="d42cd-107">Cette fonctionnalité a toujours été présente dans Azure, mais elle est également disponible dans Windows Server 2016 et Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d42cd-107">It’s something that’s always been there in Azure, but it's available in Windows Server 2016 and Azure Stack too.</span></span>

## <a name="what-does-idns-do"></a><span data-ttu-id="d42cd-108">Que fait iDNS ?</span><span class="sxs-lookup"><span data-stu-id="d42cd-108">What does iDNS do?</span></span>
<span data-ttu-id="d42cd-109">Avec les noms de domaines internationaux dans la pile d’Azure, vous obtenez hello suivant des fonctions, sans avoir toospecify entrées de serveur DNS personnalisées.</span><span class="sxs-lookup"><span data-stu-id="d42cd-109">With iDNS in Azure Stack, you get hello following capabilities, without having toospecify custom DNS server entries.</span></span>

* <span data-ttu-id="d42cd-110">Services de résolution de noms DNS partagés pour les charges de travail de locataire.</span><span class="sxs-lookup"><span data-stu-id="d42cd-110">Shared DNS name resolution services for tenant workloads.</span></span>
* <span data-ttu-id="d42cd-111">Service DNS faisant autorité pour la résolution de noms et d’inscription DNS dans le réseau virtuel hello du client.</span><span class="sxs-lookup"><span data-stu-id="d42cd-111">Authoritative DNS service for name resolution and DNS registration within hello tenant virtual network.</span></span>
* <span data-ttu-id="d42cd-112">Service DNS récursif pour la résolution de noms Internet à partir de machines virtuelles de locataire.</span><span class="sxs-lookup"><span data-stu-id="d42cd-112">Recursive DNS service for resolution of Internet names from tenant VMs.</span></span> <span data-ttu-id="d42cd-113">Les clients n’ont plus toospecify DNS entrées tooresolve Internet des noms personnalisés (par exemple, www.bing.com).</span><span class="sxs-lookup"><span data-stu-id="d42cd-113">Tenants no longer need toospecify custom DNS entries tooresolve Internet names (for example, www.bing.com).</span></span>

<span data-ttu-id="d42cd-114">Vous pouvez toujours configurer votre propre DNS et utiliser des serveurs DNS personnalisés si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d42cd-114">You can still bring your own DNS and use custom DNS servers if you want.</span></span> <span data-ttu-id="d42cd-115">Mais maintenant, si vous souhaitez que les noms DNS Internet toobe tooresolve en mesure de simplement et que vous être en mesure de tooconnect tooother machines virtuelles hello même réseau virtuel, vous n’avez pas besoin toospecify quoi que ce soit, et qu’il fonctionnera.</span><span class="sxs-lookup"><span data-stu-id="d42cd-115">But now, if you just want toobe able tooresolve Internet DNS names and be able tooconnect tooother virtual machines in hello same virtual network, you don’t need toospecify anything and it will just work.</span></span>

## <a name="what-does-idns-not-do"></a><span data-ttu-id="d42cd-116">Que ne fait pas iDNS ?</span><span class="sxs-lookup"><span data-stu-id="d42cd-116">What does iDNS not do?</span></span>
<span data-ttu-id="d42cd-117">Les noms de domaines internationaux ne vous autorise pas toodo est de créer un enregistrement DNS pour un nom qui peut être résolu à partir du réseau virtuel de hello en dehors.</span><span class="sxs-lookup"><span data-stu-id="d42cd-117">What iDNS does not allow you toodo is create a DNS record for a name that can be resolved from outside hello virtual network.</span></span>

<span data-ttu-id="d42cd-118">Dans Azure, vous pouvez hello en spécifiant une étiquette de nom DNS qui peut être associée à une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="d42cd-118">In Azure, you have hello option of specifying a DNS name label that can be associated with a public IP address.</span></span> <span data-ttu-id="d42cd-119">Vous pouvez choisir l’étiquette hello (préfixe), mais Azure choisit suffixe hello, qui est basée sur la région de hello dans lequel vous créez l’adresse IP publique de hello.</span><span class="sxs-lookup"><span data-stu-id="d42cd-119">You can choose hello label (prefix), but Azure chooses hello suffix, which is based on hello region in which you create hello public IP address.</span></span>

![Capture d’écran de l’étiquette de nom DNS](media/azure-stack-understanding-dns-in-tp2/image3.png)

<span data-ttu-id="d42cd-121">Dans l’image hello ci-dessus, Azure créera un « A » enregistrement dans DNS pour l’étiquette de nom DNS hello spécifié sous la zone de hello **westus.cloudapp.azure.com**. Le suffixe de préfixe et hello un domaine nom complet (FQDN) pouvant être résolu à partir de n’importe où sur l’ensemble de forme hello Internet public.</span><span class="sxs-lookup"><span data-stu-id="d42cd-121">In hello image above, Azure will create an “A” record in DNS for hello DNS name label specified under hello zone **westus.cloudapp.azure.com**. The prefix and hello suffix together compose a Fully Qualified Domain Name (FQDN) that can be resolved from anywhere on hello public Internet.</span></span>

<span data-ttu-id="d42cd-122">Azure pile uniquement prend en charge noms de domaines internationaux pour l’inscription du nom interne, donc il ne peut pas hello suivant.</span><span class="sxs-lookup"><span data-stu-id="d42cd-122">Azure Stack only supports iDNS for internal name registration, so it cannot do hello following.</span></span>

* <span data-ttu-id="d42cd-123">Créer un enregistrement DNS dans une zone DNS existante hébergée (par exemple, local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="d42cd-123">Create a DNS record under an existing hosted DNS zone (for example, local.azurestack.external).</span></span>
* <span data-ttu-id="d42cd-124">Créer une zone DNS (par exemple, Contoso.com).</span><span class="sxs-lookup"><span data-stu-id="d42cd-124">Create a DNS zone (such as Contoso.com).</span></span>
* <span data-ttu-id="d42cd-125">Créer un enregistrement dans votre propre zone DNS personnalisée.</span><span class="sxs-lookup"><span data-stu-id="d42cd-125">Create a record under your own custom DNS zone.</span></span>
* <span data-ttu-id="d42cd-126">Prend en charge bon hello des noms de domaine.</span><span class="sxs-lookup"><span data-stu-id="d42cd-126">Support hello purchase of domain names.</span></span>

