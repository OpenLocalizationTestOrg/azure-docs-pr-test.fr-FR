---
title: "Vue d’ensemble du scénario de récupération d’urgence Oracle dans votre environnement Azure | Documents Microsoft"
description: "Scénario de récupération d’urgence pour une base de données Oracle Database 12c dans votre environnement Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: f17ebb2b74cd7ad872f88483ed7cdb4f239ee069
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="6131a-103">Récupération d’urgence pour une base de données Oracle Database 12c dans votre environnement Azure</span><span class="sxs-lookup"><span data-stu-id="6131a-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="6131a-104">Hypothèses</span><span class="sxs-lookup"><span data-stu-id="6131a-104">Assumptions</span></span>

- <span data-ttu-id="6131a-105">Vous disposez d’une connaissance de la conception d’Oracle Data Guard et des environnements Azure.</span><span class="sxs-lookup"><span data-stu-id="6131a-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="6131a-106">Objectifs</span><span class="sxs-lookup"><span data-stu-id="6131a-106">Goals</span></span>
- <span data-ttu-id="6131a-107">Concevoir la topologie et la configuration adaptées à vos besoins de récupération d’urgence (DR).</span><span class="sxs-lookup"><span data-stu-id="6131a-107">Design the topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="6131a-108">Scénario 1 : site principal et site de récupération d’urgence sur Azure</span><span class="sxs-lookup"><span data-stu-id="6131a-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="6131a-109">Un client dispose d’une configuration de base de données Oracle sur le site principal.</span><span class="sxs-lookup"><span data-stu-id="6131a-109">A customer has an Oracle database set up on the primary site.</span></span> <span data-ttu-id="6131a-110">Un site de récupération d’urgence se trouve dans une autre région.</span><span class="sxs-lookup"><span data-stu-id="6131a-110">A DR site is in a different region.</span></span> <span data-ttu-id="6131a-111">Le client utilise Oracle Data Guard pour une récupération rapide entre ces sites.</span><span class="sxs-lookup"><span data-stu-id="6131a-111">The customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="6131a-112">Le site principal possède également une base de données secondaire pour la création de rapports et d’autres utilisations.</span><span class="sxs-lookup"><span data-stu-id="6131a-112">The primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="6131a-113">Topologie</span><span class="sxs-lookup"><span data-stu-id="6131a-113">Topology</span></span>

<span data-ttu-id="6131a-114">Voici un résumé de la configuration Azure :</span><span class="sxs-lookup"><span data-stu-id="6131a-114">Here is a summary of the Azure setup:</span></span>

- <span data-ttu-id="6131a-115">Deux sites (un site principal et un site de récupération d’urgence)</span><span class="sxs-lookup"><span data-stu-id="6131a-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="6131a-116">Deux réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="6131a-116">Two virtual networks</span></span>
- <span data-ttu-id="6131a-117">Deux bases de données Oracle avec Data Guard (primaire et secondaire)</span><span class="sxs-lookup"><span data-stu-id="6131a-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="6131a-118">Deux bases de données Oracle avec Golden Gate ou Data Guard (site principal uniquement)</span><span class="sxs-lookup"><span data-stu-id="6131a-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="6131a-119">Deux services d’application sur le site principal et un sur le site de récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="6131a-119">Two application services, one primary and one on the DR site</span></span>
- <span data-ttu-id="6131a-120">Un *groupe à haute disponibilité,* utilisé pour la base de données et le service d’application sur le site principal</span><span class="sxs-lookup"><span data-stu-id="6131a-120">An *availability set,* which is used for database and application service on the primary site</span></span>
- <span data-ttu-id="6131a-121">Une jumpbox sur chaque site, qui limite l’accès au réseau privé et autorise uniquement l’administrateur à se connecter</span><span class="sxs-lookup"><span data-stu-id="6131a-121">One jumpbox on each site, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="6131a-122">Jumpbox, service d’application, base de données et passerelle VPN sur des sous-réseaux distincts</span><span class="sxs-lookup"><span data-stu-id="6131a-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="6131a-123">Le groupe de sécurité réseau est appliqué sur les sous-réseaux d’application et de base de données</span><span class="sxs-lookup"><span data-stu-id="6131a-123">NSG enforced on application and database subnets</span></span>

![Capture d’écran de la page de topologie de récupération d’urgence](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="6131a-125">Scénario 2 : site principal local et site de récupération d’urgence sur Azure</span><span class="sxs-lookup"><span data-stu-id="6131a-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="6131a-126">Un client dispose d’une configuration de base de données Oracle locale (site principal).</span><span class="sxs-lookup"><span data-stu-id="6131a-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="6131a-127">Le site de récupération d’urgence est sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6131a-127">A DR site is on Azure.</span></span> <span data-ttu-id="6131a-128">Oracle Data Guard permet une récupération rapide entre ces sites.</span><span class="sxs-lookup"><span data-stu-id="6131a-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="6131a-129">Le site principal possède également une base de données secondaire pour la création de rapports et d’autres utilisations.</span><span class="sxs-lookup"><span data-stu-id="6131a-129">The primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="6131a-130">Deux approches sont possibles pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="6131a-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-the-firewall"></a><span data-ttu-id="6131a-131">Approche 1 : connexions directes entre un site local et un site sur Azure, nécessitant des ports TCP ouverts sur le pare-feu</span><span class="sxs-lookup"><span data-stu-id="6131a-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on the firewall</span></span> 

<span data-ttu-id="6131a-132">Nous ne recommandons pas des connexions directes, car ils exposent les ports TCP au monde extérieur.</span><span class="sxs-lookup"><span data-stu-id="6131a-132">We don't recommend direct connections because they expose the TCP ports to the outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="6131a-133">Topologie</span><span class="sxs-lookup"><span data-stu-id="6131a-133">Topology</span></span>

<span data-ttu-id="6131a-134">Voici un résumé de la configuration Azure :</span><span class="sxs-lookup"><span data-stu-id="6131a-134">Following is a summary of the Azure setup:</span></span>

- <span data-ttu-id="6131a-135">Un site de récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="6131a-135">One DR site</span></span> 
- <span data-ttu-id="6131a-136">Un seul réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="6131a-136">One virtual network</span></span>
- <span data-ttu-id="6131a-137">Une base de données Oracle avec Data Guard (active)</span><span class="sxs-lookup"><span data-stu-id="6131a-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="6131a-138">Un service d’application sur le site de récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="6131a-138">One application service on the DR site</span></span>
- <span data-ttu-id="6131a-139">Une jumpbox, qui limite l’accès au réseau privé et autorise uniquement l’administrateur à se connecter</span><span class="sxs-lookup"><span data-stu-id="6131a-139">One jumpbox, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="6131a-140">Jumpbox, service d’application, base de données et passerelle VPN sur des sous-réseaux distincts</span><span class="sxs-lookup"><span data-stu-id="6131a-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="6131a-141">Le groupe de sécurité réseau est appliqué sur les sous-réseaux d’application et de base de données</span><span class="sxs-lookup"><span data-stu-id="6131a-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="6131a-142">Une règle/stratégie de groupe de sécurité réseau pour autoriser le port TCP entrant 1521 (ou un port défini par l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="6131a-142">An NSG policy/rule to allow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="6131a-143">Une stratégie/règle de groupe de sécurité réseau pour limiter l’accès du réseau virtuel à l’adresse IP/aux adresses locales (base de données ou application) uniquement</span><span class="sxs-lookup"><span data-stu-id="6131a-143">An NSG policy/rule to restrict only the IP address/addresses on-premises (DB or application) to access the virtual network</span></span>

![Capture d’écran de la page de topologie de récupération d’urgence](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="6131a-145">Approche 2 : VPN de site à site</span><span class="sxs-lookup"><span data-stu-id="6131a-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="6131a-146">La meilleure approche consiste à utiliser des VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="6131a-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="6131a-147">Pour plus d’informations sur la configuration d’un VPN, consultez [Créer un réseau virtuel avec une connexion VPN de Site à Site à l’aide de CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="6131a-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="6131a-148">Topologie</span><span class="sxs-lookup"><span data-stu-id="6131a-148">Topology</span></span>

<span data-ttu-id="6131a-149">Voici un résumé de la configuration Azure :</span><span class="sxs-lookup"><span data-stu-id="6131a-149">Following is a summary of the Azure setup:</span></span>

- <span data-ttu-id="6131a-150">Un site de récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="6131a-150">One DR site</span></span> 
- <span data-ttu-id="6131a-151">Un seul réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="6131a-151">One virtual network</span></span> 
- <span data-ttu-id="6131a-152">Une base de données Oracle avec Data Guard (active)</span><span class="sxs-lookup"><span data-stu-id="6131a-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="6131a-153">Un service d’application sur le site de récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="6131a-153">One application service on the DR site</span></span>
- <span data-ttu-id="6131a-154">Une jumpbox, qui limite l’accès au réseau privé et autorise uniquement l’administrateur à se connecter</span><span class="sxs-lookup"><span data-stu-id="6131a-154">One jumpbox, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="6131a-155">Une jumpbox, un service d’application, une base de données et une passerelle VPN se trouvent sur des sous-réseaux distincts</span><span class="sxs-lookup"><span data-stu-id="6131a-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="6131a-156">Le groupe de sécurité réseau est appliqué sur les sous-réseaux d’application et de base de données</span><span class="sxs-lookup"><span data-stu-id="6131a-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="6131a-157">Connexion VPN de site à site entre un site local et un site sur Azure</span><span class="sxs-lookup"><span data-stu-id="6131a-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Capture d’écran de la page de topologie de récupération d’urgence](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="6131a-159">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="6131a-159">Additional reading</span></span>

- [<span data-ttu-id="6131a-160">Concevoir et mettre en œuvre une base de données Oracle sur Azure</span><span class="sxs-lookup"><span data-stu-id="6131a-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="6131a-161">Implémenter Oracle Data Guard sur une machine virtuelle Linux Azure</span><span class="sxs-lookup"><span data-stu-id="6131a-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="6131a-162">Implémenter Oracle Golden Gate sur une machine virtuelle Linux Azure</span><span class="sxs-lookup"><span data-stu-id="6131a-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="6131a-163">Sauvegarde et récupération Oracle</span><span class="sxs-lookup"><span data-stu-id="6131a-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="6131a-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6131a-164">Next steps</span></span>

- [<span data-ttu-id="6131a-165">Didacticiel : créer des machines virtuelles hautement disponibles</span><span class="sxs-lookup"><span data-stu-id="6131a-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="6131a-166">Explorer des exemples Azure CLI de déploiement de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="6131a-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
