---
title: aaaOverview de DNS Azure | Documents Microsoft
description: "Vue d’ensemble des services d’hébergement DNS sur Microsoft Azure. Héberger votre domaine sur Microsoft Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="389f3-104">Vue d’ensemble d’Azure DNS</span><span class="sxs-lookup"><span data-stu-id="389f3-104">Azure DNS overview</span></span>

<span data-ttu-id="389f3-105">Hello système de nom de domaine, ou DNS, est responsable de la traduction (ou la résolution de) un site Web ou un service name tooits adresse IP.</span><span class="sxs-lookup"><span data-stu-id="389f3-105">hello Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name tooits IP address.</span></span> <span data-ttu-id="389f3-106">Azure DNS est un service d'hébergement pour les domaines DNS et qui offre une résolution de noms à l'aide de l'infrastructure Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="389f3-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="389f3-107">En hébergeant vos domaines dans Azure, vous pouvez gérer votre serveur DNS les enregistrements à l’aide de hello même des informations d’identification, les API, outils et facturation en tant que vos autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="389f3-107">By hosting your domains in Azure, you can manage your DNS records using hello same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![Vue d’ensemble de DNS](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="389f3-109">Caractéristiques</span><span class="sxs-lookup"><span data-stu-id="389f3-109">Features</span></span>

* <span data-ttu-id="389f3-110">**Fiabilité et performances** : les domaines DNS dans Azure DNS sont hébergés sur un réseau global de serveurs de noms DNS.</span><span class="sxs-lookup"><span data-stu-id="389f3-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="389f3-111">Nous utilisons Anycast mise en réseau afin que chaque requête DNS est reçu par le serveur DNS le plus proche disponible hello.</span><span class="sxs-lookup"><span data-stu-id="389f3-111">We use Anycast networking so that each DNS query is answered by hello closest available DNS server.</span></span> <span data-ttu-id="389f3-112">Cette technique offre des performances élevées et une haute disponibilité pour votre domaine.</span><span class="sxs-lookup"><span data-stu-id="389f3-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="389f3-113">**Intégration transparente** -service DNS Azure de hello peut être utilisé toomanage enregistrements DNS pour vos services Azure et peut être utilisé tooprovide DNS pour vos ressources externes ainsi.</span><span class="sxs-lookup"><span data-stu-id="389f3-113">**Seamless integration** - hello Azure DNS service can be used toomanage DNS records for your Azure services and can be used tooprovide DNS for your external resources as well.</span></span> <span data-ttu-id="389f3-114">Azure DNS est intégré dans hello portail Azure et utilise hello les mêmes informations d’identification, la facturation et le contrat de prise en charge en tant que vos autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="389f3-114">Azure DNS is integrated in hello Azure portal and uses hello same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="389f3-115">**Sécurité** -hello service DNS Azure est basé sur le Gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="389f3-115">**Security** - hello Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="389f3-116">Ainsi, il tire parti de fonctionnalités de Resource Manager telles que le contrôle d’accès en fonction du rôle, les journaux d’audit et le verrouillage de ressources.</span><span class="sxs-lookup"><span data-stu-id="389f3-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="389f3-117">Vos domaines et les enregistrements peuvent être gérés via hello portail Azure, les applets de commande PowerShell de Azure et hello CLI d’Azure inter-plateformes.</span><span class="sxs-lookup"><span data-stu-id="389f3-117">Your domains and records can be managed via hello Azure portal, Azure PowerShell cmdlets, and hello cross-platform Azure CLI.</span></span> <span data-ttu-id="389f3-118">Applications qui requièrent la gestion DNS automatique peuvent intégrer service hello via hello API REST et les kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="389f3-118">Applications requiring automatic DNS management can integrate with hello service via hello REST API and SDKs.</span></span>

<span data-ttu-id="389f3-119">Azure DNS ne prend actuellement pas en charge l'achat de noms de domaine.</span><span class="sxs-lookup"><span data-stu-id="389f3-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="389f3-120">Si vous souhaitez toopurchase domaines, vous devez toouse un bureau d’enregistrement du nom de domaine de l’application tierce.</span><span class="sxs-lookup"><span data-stu-id="389f3-120">If you want toopurchase domains, you need toouse a third-party domain name registrar.</span></span> <span data-ttu-id="389f3-121">bureau d’enregistrement Hello généralement des frais une petite annuel.</span><span class="sxs-lookup"><span data-stu-id="389f3-121">hello registrar typically charges a small annual fee.</span></span> <span data-ttu-id="389f3-122">les domaines Hello peuvent ensuite être hébergés dans Azure DNS pour la gestion des enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="389f3-122">hello domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="389f3-123">Consultez [déléguer un tooAzure de domaine DNS](dns-domain-delegation.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="389f3-123">See [Delegate a Domain tooAzure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="389f3-124">Tarification</span><span class="sxs-lookup"><span data-stu-id="389f3-124">Pricing</span></span>

<span data-ttu-id="389f3-125">Facturation de DNS est basée sur le nombre de hello de zones DNS hébergées dans Azure et en nombre hello de requêtes DNS.</span><span class="sxs-lookup"><span data-stu-id="389f3-125">DNS billing is based on hello number of DNS zones hosted in Azure and by hello number of DNS queries.</span></span> <span data-ttu-id="389f3-126">toolearn plus d’informations sur la tarification visite [de la tarification Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="389f3-126">toolearn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="389f3-127">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="389f3-127">FAQ</span></span>

<span data-ttu-id="389f3-128">Pour les questions fréquemment posées sur le système DNS d’Azure, consultez hello [le Forum aux questions sur Azure DNS](dns-faq.md).</span><span class="sxs-lookup"><span data-stu-id="389f3-128">For frequently asked questions about Azure DNS, see hello [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="389f3-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="389f3-129">Next steps</span></span>

<span data-ttu-id="389f3-130">Obteniez plus d’informations sur les zones et enregistrements DNS en consultant : [Vue d’ensemble des enregistrements et zones DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="389f3-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="389f3-131">Découvrez comment trop[créer une zone DNS](./dns-getstarted-create-dnszone-portal.md) dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="389f3-131">Learn how too[create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="389f3-132">En savoir plus sur certaines des hello autre clé [fonctionnalités de réseau](../networking/networking-overview.md) de Azure.</span><span class="sxs-lookup"><span data-stu-id="389f3-132">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

