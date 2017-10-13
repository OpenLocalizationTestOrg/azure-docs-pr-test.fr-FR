---
title: "Présentation de DNS dans Azure Stack | Microsoft Docs"
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
ms.date: 9/25/2017
ms.author: scottnap
ms.openlocfilehash: 8c023eda179ace41a082bf4a4fadc281c14db7ba
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="introducing-idns-for-azure-stack"></a><span data-ttu-id="c504a-103">Présentation d’iDNS pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c504a-103">Introducing iDNS for Azure Stack</span></span>

<span data-ttu-id="c504a-104">*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*</span><span class="sxs-lookup"><span data-stu-id="c504a-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="c504a-105">iDNS est une fonctionnalité d’Azure Stack qui vous permet de résoudre les noms DNS externes (par exemple, http://www.bing.com).</span><span class="sxs-lookup"><span data-stu-id="c504a-105">iDNS is a feature in Azure Stack that allows you to resolve external DNS names (such as http://www.bing.com).</span></span>
<span data-ttu-id="c504a-106">Elle vous permet également d’enregistrer des noms de réseau virtuel interne.</span><span class="sxs-lookup"><span data-stu-id="c504a-106">It also allows you to register internal virtual network names.</span></span> <span data-ttu-id="c504a-107">De cette façon, vous pouvez résoudre des machines virtuelles sur le même réseau virtuel par nom plutôt que par adresse IP, sans avoir à fournir des entrées de serveur DNS personnalisées.</span><span class="sxs-lookup"><span data-stu-id="c504a-107">By doing so, you can resolve VMs on the same virtual network by name rather than IP address, without having to provide custom DNS server entries.</span></span>

<span data-ttu-id="c504a-108">Cette fonctionnalité a toujours été présente dans Azure, mais elle est également disponible dans Windows Server 2016 et Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c504a-108">It’s something that’s always been there in Azure, but it's available in Windows Server 2016 and Azure Stack too.</span></span>

## <a name="what-does-idns-do"></a><span data-ttu-id="c504a-109">Que fait iDNS ?</span><span class="sxs-lookup"><span data-stu-id="c504a-109">What does iDNS do?</span></span>
<span data-ttu-id="c504a-110">Avec iDNS dans Azure Stack, vous obtenez les fonctionnalités suivantes, sans avoir à spécifier d’entrées de serveur DNS personnalisées.</span><span class="sxs-lookup"><span data-stu-id="c504a-110">With iDNS in Azure Stack, you get the following capabilities, without having to specify custom DNS server entries.</span></span>

* <span data-ttu-id="c504a-111">Services de résolution de noms DNS partagés pour les charges de travail de locataire.</span><span class="sxs-lookup"><span data-stu-id="c504a-111">Shared DNS name resolution services for tenant workloads.</span></span>
* <span data-ttu-id="c504a-112">Service DNS faisant autorité pour la résolution de noms et l’enregistrement DNS dans le réseau virtuel du locataire.</span><span class="sxs-lookup"><span data-stu-id="c504a-112">Authoritative DNS service for name resolution and DNS registration within the tenant virtual network.</span></span>
* <span data-ttu-id="c504a-113">Service DNS récursif pour la résolution de noms Internet à partir de machines virtuelles de locataire.</span><span class="sxs-lookup"><span data-stu-id="c504a-113">Recursive DNS service for resolution of Internet names from tenant VMs.</span></span> <span data-ttu-id="c504a-114">Les locataires n’ont plus besoin de spécifier des entrées DNS personnalisées pour résoudre les noms Internet (par exemple, www.bing.com).</span><span class="sxs-lookup"><span data-stu-id="c504a-114">Tenants no longer need to specify custom DNS entries to resolve Internet names (for example, www.bing.com).</span></span>

<span data-ttu-id="c504a-115">Vous pouvez toujours configurer votre propre DNS et utiliser des serveurs DNS personnalisés si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="c504a-115">You can still bring your own DNS and use custom DNS servers if you want.</span></span> <span data-ttu-id="c504a-116">Toutefois, à présent, si vous voulez simplement résoudre les noms DNS Internet et vous connecter à d’autres machines virtuelles dans le même réseau virtuel, vous n’avez besoin de spécifier aucun paramètre pour pouvoir le faire.</span><span class="sxs-lookup"><span data-stu-id="c504a-116">But now, if you just want to be able to resolve Internet DNS names and be able to connect to other virtual machines in the same virtual network, you don’t need to specify anything and it will just work.</span></span>

## <a name="what-does-idns-not-do"></a><span data-ttu-id="c504a-117">Que ne fait pas iDNS ?</span><span class="sxs-lookup"><span data-stu-id="c504a-117">What does iDNS not do?</span></span>
<span data-ttu-id="c504a-118">iDNS ne vous permet pas de créer un enregistrement DNS pour un nom qui peut être résolu en dehors du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="c504a-118">What iDNS does not allow you to do is create a DNS record for a name that can be resolved from outside the virtual network.</span></span>

<span data-ttu-id="c504a-119">Dans Azure, vous avez la possibilité de spécifier une étiquette de nom DNS pouvant être associée à une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="c504a-119">In Azure, you have the option of specifying a DNS name label that can be associated with a public IP address.</span></span> <span data-ttu-id="c504a-120">Vous pouvez choisir l’étiquette (préfixe), mais Azure choisit le suffixe, qui est basé sur la région dans laquelle vous créez l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="c504a-120">You can choose the label (prefix), but Azure chooses the suffix, which is based on the region in which you create the public IP address.</span></span>

![Capture d’écran de l’étiquette de nom DNS](media/azure-stack-understanding-dns-in-tp2/image3.png)

<span data-ttu-id="c504a-122">Dans l’image ci-dessus, Azure crée un enregistrement « A » dans DNS pour l’étiquette du nom DNS spécifiée dans la zone **westus.cloudapp.azure.com**. Le préfixe et le suffixe ensemble représentent un nom de domaine complet (FQDN) pouvant être résolu n’importe où sur le réseau Internet public.</span><span class="sxs-lookup"><span data-stu-id="c504a-122">In the image above, Azure will create an “A” record in DNS for the DNS name label specified under the zone **westus.cloudapp.azure.com**. The prefix and the suffix together compose a Fully Qualified Domain Name (FQDN) that can be resolved from anywhere on the public Internet.</span></span>

<span data-ttu-id="c504a-123">Azure Stack prend en charge iDNS uniquement pour l’enregistrement de noms internes. Dans ce sens, il ne peut pas effectuer les opérations suivantes.</span><span class="sxs-lookup"><span data-stu-id="c504a-123">Azure Stack only supports iDNS for internal name registration, so it cannot do the following.</span></span>

* <span data-ttu-id="c504a-124">Créer un enregistrement DNS dans une zone DNS existante hébergée (par exemple, local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="c504a-124">Create a DNS record under an existing hosted DNS zone (for example, local.azurestack.external).</span></span>
* <span data-ttu-id="c504a-125">Créer une zone DNS (par exemple, Contoso.com).</span><span class="sxs-lookup"><span data-stu-id="c504a-125">Create a DNS zone (such as Contoso.com).</span></span>
* <span data-ttu-id="c504a-126">Créer un enregistrement dans votre propre zone DNS personnalisée.</span><span class="sxs-lookup"><span data-stu-id="c504a-126">Create a record under your own custom DNS zone.</span></span>
* <span data-ttu-id="c504a-127">Prendre en charge l’achat de noms de domaine.</span><span class="sxs-lookup"><span data-stu-id="c504a-127">Support the purchase of domain names.</span></span>

