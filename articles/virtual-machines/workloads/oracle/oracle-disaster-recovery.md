---
title: "aaaOverview d’un scénario de récupération d’urgence Oracle dans votre environnement Azure | Documents Microsoft"
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
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="fb66c-103">Récupération d’urgence pour une base de données Oracle Database 12c dans votre environnement Azure</span><span class="sxs-lookup"><span data-stu-id="fb66c-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="fb66c-104">Hypothèses</span><span class="sxs-lookup"><span data-stu-id="fb66c-104">Assumptions</span></span>

- <span data-ttu-id="fb66c-105">Vous disposez d’une connaissance de la conception d’Oracle Data Guard et des environnements Azure.</span><span class="sxs-lookup"><span data-stu-id="fb66c-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="fb66c-106">Objectifs</span><span class="sxs-lookup"><span data-stu-id="fb66c-106">Goals</span></span>
- <span data-ttu-id="fb66c-107">Concevoir une topologie de hello et de configuration qui répondent à vos besoins de reprise après sinistre.</span><span class="sxs-lookup"><span data-stu-id="fb66c-107">Design hello topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="fb66c-108">Scénario 1 : site principal et site de récupération d’urgence sur Azure</span><span class="sxs-lookup"><span data-stu-id="fb66c-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="fb66c-109">Un client dispose d’Oracle des bases de données de site principal de hello.</span><span class="sxs-lookup"><span data-stu-id="fb66c-109">A customer has an Oracle database set up on hello primary site.</span></span> <span data-ttu-id="fb66c-110">Un site de récupération d’urgence se trouve dans une autre région.</span><span class="sxs-lookup"><span data-stu-id="fb66c-110">A DR site is in a different region.</span></span> <span data-ttu-id="fb66c-111">client de Hello utilise Oracle Data Guard pour une récupération rapide entre ces sites.</span><span class="sxs-lookup"><span data-stu-id="fb66c-111">hello customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="fb66c-112">site principal de Hello possède également une base de données secondaire pour la création de rapports et d’autres utilisations.</span><span class="sxs-lookup"><span data-stu-id="fb66c-112">hello primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="fb66c-113">Topologie</span><span class="sxs-lookup"><span data-stu-id="fb66c-113">Topology</span></span>

<span data-ttu-id="fb66c-114">Voici un résumé de hello le programme d’installation Azure :</span><span class="sxs-lookup"><span data-stu-id="fb66c-114">Here is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="fb66c-115">Deux sites (un site principal et un site de récupération d’urgence)</span><span class="sxs-lookup"><span data-stu-id="fb66c-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="fb66c-116">Deux réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="fb66c-116">Two virtual networks</span></span>
- <span data-ttu-id="fb66c-117">Deux bases de données Oracle avec Data Guard (primaire et secondaire)</span><span class="sxs-lookup"><span data-stu-id="fb66c-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="fb66c-118">Deux bases de données Oracle avec Golden Gate ou Data Guard (site principal uniquement)</span><span class="sxs-lookup"><span data-stu-id="fb66c-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="fb66c-119">Les deux services d’application, un serveur principal et sur le site de récupération d’urgence de hello</span><span class="sxs-lookup"><span data-stu-id="fb66c-119">Two application services, one primary and one on hello DR site</span></span>
- <span data-ttu-id="fb66c-120">Un *à haute disponibilité,* qui est utilisé pour la base de données et application de service sur le site principal de hello</span><span class="sxs-lookup"><span data-stu-id="fb66c-120">An *availability set,* which is used for database and application service on hello primary site</span></span>
- <span data-ttu-id="fb66c-121">Un jumpbox sur chaque site, ce qui restreint le réseau privé de l’accès toohello et autorise uniquement l’authentification dans par un administrateur</span><span class="sxs-lookup"><span data-stu-id="fb66c-121">One jumpbox on each site, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="fb66c-122">Jumpbox, service d’application, base de données et passerelle VPN sur des sous-réseaux distincts</span><span class="sxs-lookup"><span data-stu-id="fb66c-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="fb66c-123">Le groupe de sécurité réseau est appliqué sur les sous-réseaux d’application et de base de données</span><span class="sxs-lookup"><span data-stu-id="fb66c-123">NSG enforced on application and database subnets</span></span>

![Capture d’écran de la page de la topologie hello récupération d’urgence](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="fb66c-125">Scénario 2 : site principal local et site de récupération d’urgence sur Azure</span><span class="sxs-lookup"><span data-stu-id="fb66c-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="fb66c-126">Un client dispose d’une configuration de base de données Oracle locale (site principal).</span><span class="sxs-lookup"><span data-stu-id="fb66c-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="fb66c-127">Le site de récupération d’urgence est sur Azure.</span><span class="sxs-lookup"><span data-stu-id="fb66c-127">A DR site is on Azure.</span></span> <span data-ttu-id="fb66c-128">Oracle Data Guard permet une récupération rapide entre ces sites.</span><span class="sxs-lookup"><span data-stu-id="fb66c-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="fb66c-129">site principal de Hello possède également une base de données secondaire pour la création de rapports et d’autres utilisations.</span><span class="sxs-lookup"><span data-stu-id="fb66c-129">hello primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="fb66c-130">Deux approches sont possibles pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="fb66c-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a><span data-ttu-id="fb66c-131">Méthode 1 : Les connexions directes entre locaux et Azure, nécessitant des ports TCP ouverts sur les pare-feu hello</span><span class="sxs-lookup"><span data-stu-id="fb66c-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on hello firewall</span></span> 

<span data-ttu-id="fb66c-132">Nous ne recommandons des connexions directes, car ils exposent toohello de ports TCP hello world à l’extérieur.</span><span class="sxs-lookup"><span data-stu-id="fb66c-132">We don't recommend direct connections because they expose hello TCP ports toohello outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="fb66c-133">Topologie</span><span class="sxs-lookup"><span data-stu-id="fb66c-133">Topology</span></span>

<span data-ttu-id="fb66c-134">Voici un résumé de hello le programme d’installation Azure :</span><span class="sxs-lookup"><span data-stu-id="fb66c-134">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="fb66c-135">Un site de récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="fb66c-135">One DR site</span></span> 
- <span data-ttu-id="fb66c-136">Un seul réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="fb66c-136">One virtual network</span></span>
- <span data-ttu-id="fb66c-137">Une base de données Oracle avec Data Guard (active)</span><span class="sxs-lookup"><span data-stu-id="fb66c-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="fb66c-138">Service d’une application sur le site de récupération d’urgence de hello</span><span class="sxs-lookup"><span data-stu-id="fb66c-138">One application service on hello DR site</span></span>
- <span data-ttu-id="fb66c-139">Un jumpbox, ce qui restreint le réseau privé de l’accès toohello et autorise uniquement l’authentification dans par un administrateur</span><span class="sxs-lookup"><span data-stu-id="fb66c-139">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="fb66c-140">Jumpbox, service d’application, base de données et passerelle VPN sur des sous-réseaux distincts</span><span class="sxs-lookup"><span data-stu-id="fb66c-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="fb66c-141">Le groupe de sécurité réseau est appliqué sur les sous-réseaux d’application et de base de données</span><span class="sxs-lookup"><span data-stu-id="fb66c-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="fb66c-142">Un tooallow/règle de stratégie de groupe de sécurité réseau entrants le port 1521 TCP (ou un port défini par l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="fb66c-142">An NSG policy/rule tooallow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="fb66c-143">Un groupe de sécurité réseau/règle de stratégie toorestrict uniquement hello IP adresse/adresses locales (base de données ou application) tooaccess hello réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="fb66c-143">An NSG policy/rule toorestrict only hello IP address/addresses on-premises (DB or application) tooaccess hello virtual network</span></span>

![Capture d’écran de la page de la topologie hello récupération d’urgence](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="fb66c-145">Approche 2 : VPN de site à site</span><span class="sxs-lookup"><span data-stu-id="fb66c-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="fb66c-146">La meilleure approche consiste à utiliser des VPN de site à site.</span><span class="sxs-lookup"><span data-stu-id="fb66c-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="fb66c-147">Pour plus d’informations sur la configuration d’un VPN, consultez [Créer un réseau virtuel avec une connexion VPN de Site à Site à l’aide de CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="fb66c-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="fb66c-148">Topologie</span><span class="sxs-lookup"><span data-stu-id="fb66c-148">Topology</span></span>

<span data-ttu-id="fb66c-149">Voici un résumé de hello le programme d’installation Azure :</span><span class="sxs-lookup"><span data-stu-id="fb66c-149">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="fb66c-150">Un site de récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="fb66c-150">One DR site</span></span> 
- <span data-ttu-id="fb66c-151">Un seul réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="fb66c-151">One virtual network</span></span> 
- <span data-ttu-id="fb66c-152">Une base de données Oracle avec Data Guard (active)</span><span class="sxs-lookup"><span data-stu-id="fb66c-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="fb66c-153">Service d’une application sur le site de récupération d’urgence de hello</span><span class="sxs-lookup"><span data-stu-id="fb66c-153">One application service on hello DR site</span></span>
- <span data-ttu-id="fb66c-154">Un jumpbox, ce qui restreint le réseau privé de l’accès toohello et autorise uniquement l’authentification dans par un administrateur</span><span class="sxs-lookup"><span data-stu-id="fb66c-154">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="fb66c-155">Une jumpbox, un service d’application, une base de données et une passerelle VPN se trouvent sur des sous-réseaux distincts</span><span class="sxs-lookup"><span data-stu-id="fb66c-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="fb66c-156">Le groupe de sécurité réseau est appliqué sur les sous-réseaux d’application et de base de données</span><span class="sxs-lookup"><span data-stu-id="fb66c-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="fb66c-157">Connexion VPN de site à site entre un site local et un site sur Azure</span><span class="sxs-lookup"><span data-stu-id="fb66c-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Capture d’écran de la page de la topologie hello récupération d’urgence](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="fb66c-159">Documentation supplémentaire</span><span class="sxs-lookup"><span data-stu-id="fb66c-159">Additional reading</span></span>

- [<span data-ttu-id="fb66c-160">Concevoir et mettre en œuvre une base de données Oracle sur Azure</span><span class="sxs-lookup"><span data-stu-id="fb66c-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="fb66c-161">Implémenter Oracle Data Guard sur une machine virtuelle Linux Azure</span><span class="sxs-lookup"><span data-stu-id="fb66c-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="fb66c-162">Implémenter Oracle Golden Gate sur une machine virtuelle Linux Azure</span><span class="sxs-lookup"><span data-stu-id="fb66c-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="fb66c-163">Sauvegarde et récupération Oracle</span><span class="sxs-lookup"><span data-stu-id="fb66c-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="fb66c-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fb66c-164">Next steps</span></span>

- [<span data-ttu-id="fb66c-165">Didacticiel : créer des machines virtuelles hautement disponibles</span><span class="sxs-lookup"><span data-stu-id="fb66c-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="fb66c-166">Explorer des exemples Azure CLI de déploiement de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="fb66c-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
