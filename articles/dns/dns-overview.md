---
title: "Vue d’ensemble d’Azure DNS | Microsoft Docs"
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
ms.openlocfilehash: 3705457e4c90f8869496f7f5177531bd128d1057
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="1bb6d-104">Vue d’ensemble d’Azure DNS</span><span class="sxs-lookup"><span data-stu-id="1bb6d-104">Azure DNS overview</span></span>

<span data-ttu-id="1bb6d-105">Le DNS (Domain Name System) se charge de traduire (ou résoudre) un nom de site web ou de service en une adresse IP.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-105">The Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name to its IP address.</span></span> <span data-ttu-id="1bb6d-106">Azure DNS est un service d'hébergement pour les domaines DNS et qui offre une résolution de noms à l'aide de l'infrastructure Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="1bb6d-107">En hébergeant vos domaines dans Azure, vous pouvez gérer vos enregistrements DNS avec les mêmes informations d’identification, les mêmes API, les mêmes outils et la même facturation que vos autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-107">By hosting your domains in Azure, you can manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![Vue d’ensemble de DNS](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="1bb6d-109">Caractéristiques</span><span class="sxs-lookup"><span data-stu-id="1bb6d-109">Features</span></span>

* <span data-ttu-id="1bb6d-110">**Fiabilité et performances** : les domaines DNS dans Azure DNS sont hébergés sur un réseau global de serveurs de noms DNS.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="1bb6d-111">Nous utilisons la mise en réseau Anycast, afin que chaque requête DNS obtienne une réponse du serveur DNS disponible le plus proche.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-111">We use Anycast networking so that each DNS query is answered by the closest available DNS server.</span></span> <span data-ttu-id="1bb6d-112">Cette technique offre des performances élevées et une haute disponibilité pour votre domaine.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="1bb6d-113">**Intégration transparente** : le service Azure DNS peut être utilisé pour gérer les enregistrements DNS pour vos services Azure et pour fournir également un DNS pour vos ressources externes.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-113">**Seamless integration** - The Azure DNS service can be used to manage DNS records for your Azure services and can be used to provide DNS for your external resources as well.</span></span> <span data-ttu-id="1bb6d-114">Azure DNS est intégré au portail Azure et utilise les mêmes informations d’identification, facturation et contrat de support que vos autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-114">Azure DNS is integrated in the Azure portal and uses the same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="1bb6d-115">**Sécurité** : le service Azure DNS est basé sur Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-115">**Security** - The Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="1bb6d-116">Ainsi, il tire parti de fonctionnalités de Resource Manager telles que le contrôle d’accès en fonction du rôle, les journaux d’audit et le verrouillage de ressources.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="1bb6d-117">Vos domaines et enregistrements peuvent être gérés via le portail Azure, des applets de commande Azure PowerShell et l’interface CLI Azure multiplateforme.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-117">Your domains and records can be managed via the Azure portal, Azure PowerShell cmdlets, and the cross-platform Azure CLI.</span></span> <span data-ttu-id="1bb6d-118">Les applications nécessitant une gestion automatique de DNS peuvent s’intégrer au service par le biais de l’API REST et des Kits de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="1bb6d-118">Applications requiring automatic DNS management can integrate with the service via the REST API and SDKs.</span></span>

<span data-ttu-id="1bb6d-119">Azure DNS ne prend actuellement pas en charge l'achat de noms de domaine.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="1bb6d-120">Si vous voulez acheter des domaines, vous devez utiliser un bureau d’enregistrement de noms de domaine tiers.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-120">If you want to purchase domains, you need to use a third-party domain name registrar.</span></span> <span data-ttu-id="1bb6d-121">Le bureau d’enregistrement facture généralement des frais annuels peu élevés.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-121">The registrar typically charges a small annual fee.</span></span> <span data-ttu-id="1bb6d-122">Les domaines peuvent être hébergés dans Azure DNS pour la gestion des enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-122">The domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="1bb6d-123">Pour plus d’informations, consultez [Déléguer un domaine à Azure DNS](dns-domain-delegation.md) .</span><span class="sxs-lookup"><span data-stu-id="1bb6d-123">See [Delegate a Domain to Azure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="1bb6d-124">Tarification</span><span class="sxs-lookup"><span data-stu-id="1bb6d-124">Pricing</span></span>

<span data-ttu-id="1bb6d-125">La facturation DNS est basée sur le nombre de zones DNS hébergées dans Azure et le nombre de requêtes DNS.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-125">DNS billing is based on the number of DNS zones hosted in Azure and by the number of DNS queries.</span></span> <span data-ttu-id="1bb6d-126">Pour en savoir plus sur la tarification, consultez [Tarification d’Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="1bb6d-126">To learn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="1bb6d-127">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="1bb6d-127">FAQ</span></span>

<span data-ttu-id="1bb6d-128">Pour les questions fréquemment posées sur Azure DNS, consultez le [FAQ sur Azure DNS](dns-faq.md).</span><span class="sxs-lookup"><span data-stu-id="1bb6d-128">For frequently asked questions about Azure DNS, see the [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bb6d-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1bb6d-129">Next steps</span></span>

<span data-ttu-id="1bb6d-130">Obteniez plus d’informations sur les zones et enregistrements DNS en consultant : [Vue d’ensemble des enregistrements et zones DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="1bb6d-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="1bb6d-131">Découvrez comment [créer une zone DNS](./dns-getstarted-create-dnszone-portal.md) dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-131">Learn how to [create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="1bb6d-132">Découvrez certaines des autres [fonctionnalités de réseau](../networking/networking-overview.md) clés d’Azure.</span><span class="sxs-lookup"><span data-stu-id="1bb6d-132">Learn about some of the other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

