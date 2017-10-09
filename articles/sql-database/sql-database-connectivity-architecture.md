---
title: "architecture de connectivité de base de données SQL d’aaaAzure | Documents Microsoft"
description: "Ce document explique hello Azure SQLDB connectivité architecture d’Azure ou d’en dehors d’Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="285c2-103">Architecture de connectivité Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="285c2-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="285c2-104">Cet article explique l’architecture de connectivité de base de données SQL Azure hello et explique le fonctionnement des différents composants de hello instance de tooyour toodirect le trafic de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="285c2-104">This article explains hello Azure SQL Database connectivity architecture and explains how hello different components function toodirect traffic tooyour instance of Azure SQL Database.</span></span> <span data-ttu-id="285c2-105">Ces composants de connectivité de base de données SQL Azure fonctionnent toohello de trafic réseau toodirect de la base de données Azure avec les clients se connectant à partir d’Azure et avec les clients se connectant depuis l’extérieur d’Azure.</span><span class="sxs-lookup"><span data-stu-id="285c2-105">These Azure SQL Database connectivity components function toodirect network traffic toohello Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="285c2-106">Cet article fournit également des toochange d’exemples de script comment connectivité se produit, et les considérations hello liées paramètres de connectivité toochanging hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="285c2-106">This article also provides script samples toochange how connectivity occurs, and hello considerations related toochanging hello default connectivity settings.</span></span> <span data-ttu-id="285c2-107">Si vous avez des questions suite à la lecture de cet article, veuillez contacter Dhruv à l’adresse suivante : dmalik@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="285c2-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="285c2-108">Architecture de connectivité</span><span class="sxs-lookup"><span data-stu-id="285c2-108">Connectivity architecture</span></span>

<span data-ttu-id="285c2-109">Hello suivant schéma fournit une vue d’ensemble de hello architecture de connectivité de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="285c2-109">hello following diagram provides a high-level overview of hello Azure SQL Database connectivity architecture.</span></span> 

![Présentation de l’architecture](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="285c2-111">Hello étapes suivantes décrivent comment une connexion est établie tooan base de données SQL Azure via hello Azure SQL Database-équilibrage de charge logiciel (SLB) et la passerelle de base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="285c2-111">hello following steps describe how a connection is established tooan Azure SQL database through hello Azure SQL Database software load-balancer (SLB) and hello Azure SQL Database gateway.</span></span>

- <span data-ttu-id="285c2-112">Les clients dans Azure ou en dehors de Azure connecteront toohello SLB, ce qui a une adresse IP publique et écoute le port 1433.</span><span class="sxs-lookup"><span data-stu-id="285c2-112">Clients within Azure or outside of Azure connect toohello SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="285c2-113">Hello SLB dirige la passerelle de base de données SQL Azure toohello le trafic.</span><span class="sxs-lookup"><span data-stu-id="285c2-113">hello SLB directs traffic toohello Azure SQL Database gateway.</span></span>
- <span data-ttu-id="285c2-114">passerelle de Hello redirige intergiciel (middleware) de hello trafic toohello proxy approprié.</span><span class="sxs-lookup"><span data-stu-id="285c2-114">hello gateway redirects hello traffic toohello correct proxy middleware.</span></span>
- <span data-ttu-id="285c2-115">intergiciel (middleware) de Hello proxy redirige hello trafic toohello approprié SQL Azure de base de données.</span><span class="sxs-lookup"><span data-stu-id="285c2-115">hello proxy middleware redirects hello traffic toohello appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="285c2-116">Chacun de ces composants a distribué de refus de la protection de service (distribué DDoS) intégrée au réseau de hello et à la couche d’application hello.</span><span class="sxs-lookup"><span data-stu-id="285c2-116">Each of these components has distributed denial of service (DDoS) protection built-in at hello network and hello app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="285c2-117">Connectivité dans Azure</span><span class="sxs-lookup"><span data-stu-id="285c2-117">Connectivity from within Azure</span></span>

<span data-ttu-id="285c2-118">Si vous vous connectez à partir d’Azure, vos connexions ont une stratégie de connexion par **redirection** par défaut.</span><span class="sxs-lookup"><span data-stu-id="285c2-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="285c2-119">Une stratégie de **rediriger** signifie que les connexions une fois la session TCP de hello est la base de données SQL Azure toohello établie, la session de client hello est alors redirigé toohello intergiciel (middleware) pour le proxy avec une modification toohello destination adresse IP virtuelle à partir de celle de toothat de passerelle de base de données SQL Azure hello d’intergiciel (middleware) de hello proxy.</span><span class="sxs-lookup"><span data-stu-id="285c2-119">A policy of **Redirect** means that connections after hello TCP session is established toohello Azure SQL database, hello client session is then redirected toohello proxy middleware with a change toohello destination virtual IP from that of hello Azure SQL Database gateway toothat of hello proxy middleware.</span></span> <span data-ttu-id="285c2-120">Par la suite, tous les paquets suivants de flux directement via l’intergiciel proxy hello, en ignorant la passerelle de base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="285c2-120">Thereafter, all subsequent packets flow directly via hello proxy middleware, bypassing hello Azure SQL Database gateway.</span></span> <span data-ttu-id="285c2-121">Hello suivant le diagramme illustre le flux de trafic.</span><span class="sxs-lookup"><span data-stu-id="285c2-121">hello following diagram illustrates this traffic flow.</span></span>

![Présentation de l’architecture](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="285c2-123">Connectivité en dehors d’Azure</span><span class="sxs-lookup"><span data-stu-id="285c2-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="285c2-124">Si vous vous connectez en dehors d’Azure, vos connexions disposent d’une stratégie de connexion de **proxy** par défaut.</span><span class="sxs-lookup"><span data-stu-id="285c2-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="285c2-125">Une stratégie de **Proxy** signifie que hello TCP est établie via une passerelle de base de données SQL Azure hello et flux de tous les paquets suivants hello passerelle.</span><span class="sxs-lookup"><span data-stu-id="285c2-125">A policy of **Proxy** means that hello TCP session is established via hello Azure SQL Database gateway and all subsequent packets flow via hello gateway.</span></span> <span data-ttu-id="285c2-126">Hello suivant le diagramme illustre le flux de trafic.</span><span class="sxs-lookup"><span data-stu-id="285c2-126">hello following diagram illustrates this traffic flow.</span></span>

![Présentation de l’architecture](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="285c2-128">Adresses IP de la passerelle Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="285c2-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="285c2-129">tooconnect tooan Azure base de données SQL à partir des ressources locales, vous devez passerelle de base de données SQL Azure toohello tooallow réseau sortant du trafic de votre région Azure.</span><span class="sxs-lookup"><span data-stu-id="285c2-129">tooconnect tooan Azure SQL database from on-premises resources, you need tooallow outbound network traffic toohello Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="285c2-130">Les connexions uniquement accéder via une passerelle de hello lors de la connexion en mode de Proxy, qui est la valeur par défaut hello lors de la connexion à partir des ressources locales.</span><span class="sxs-lookup"><span data-stu-id="285c2-130">Your connections only go via hello gateway when connecting in Proxy mode, which is hello default when connecting from on-premises resources.</span></span>

<span data-ttu-id="285c2-131">Hello tableau ci-dessous répertorie hello principaux et secondaire des adresses IP de passerelle de base de données SQL Azure hello pour toutes les régions de données.</span><span class="sxs-lookup"><span data-stu-id="285c2-131">hello following table lists hello primary and secondary IPs of hello Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="285c2-132">Pour certaines régions, il existe deux adresses IP.</span><span class="sxs-lookup"><span data-stu-id="285c2-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="285c2-133">Dans ces régions, l’adresse IP principale hello est hello adresse IP actuelle de passerelle de hello et adresse IP de la deuxième hello est une adresse IP de basculement.</span><span class="sxs-lookup"><span data-stu-id="285c2-133">In these regions, hello primary IP address is hello current IP address of hello gateway and hello second IP address is a failover IP address.</span></span> <span data-ttu-id="285c2-134">adresse de basculement Hello est toowhich d’adresse hello nous pouvons déplacer votre disponibilité du service serveur tookeep hello haute.</span><span class="sxs-lookup"><span data-stu-id="285c2-134">hello failover address is hello address toowhich we might move your server tookeep hello service availability high.</span></span> <span data-ttu-id="285c2-135">Pour ces régions, nous vous recommandons d’autoriser des adresses IP hello tooboth sortant.</span><span class="sxs-lookup"><span data-stu-id="285c2-135">For these regions, we recommend that you allow outbound tooboth hello IP addresses.</span></span> <span data-ttu-id="285c2-136">adresse IP de la deuxième Hello est détenu par Microsoft et n’écoute pas tous les services jusqu'à ce qu’il est activé par des connexions de tooaccept de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="285c2-136">hello second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database tooaccept connections.</span></span>

| <span data-ttu-id="285c2-137">Nom de la région</span><span class="sxs-lookup"><span data-stu-id="285c2-137">Region Name</span></span> | <span data-ttu-id="285c2-138">Adresse IP principale</span><span class="sxs-lookup"><span data-stu-id="285c2-138">Primary IP address</span></span> | <span data-ttu-id="285c2-139">Adresse IP secondaire</span><span class="sxs-lookup"><span data-stu-id="285c2-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="285c2-140">Est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="285c2-140">Australia East</span></span> | <span data-ttu-id="285c2-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="285c2-141">191.238.66.109</span></span> | <span data-ttu-id="285c2-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="285c2-142">13.75.149.87</span></span> |
| <span data-ttu-id="285c2-143">Sud-Est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="285c2-143">Australia South East</span></span> | <span data-ttu-id="285c2-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="285c2-144">191.239.192.109</span></span> | <span data-ttu-id="285c2-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="285c2-145">13.73.109.251</span></span> |
| <span data-ttu-id="285c2-146">Sud du Brésil</span><span class="sxs-lookup"><span data-stu-id="285c2-146">Brazil South</span></span> | <span data-ttu-id="285c2-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="285c2-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="285c2-148">Centre du Canada</span><span class="sxs-lookup"><span data-stu-id="285c2-148">Canada Central</span></span> | <span data-ttu-id="285c2-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="285c2-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="285c2-150">Est du Canada</span><span class="sxs-lookup"><span data-stu-id="285c2-150">Canada East</span></span> | <span data-ttu-id="285c2-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="285c2-151">40.86.226.166</span></span> | |
| <span data-ttu-id="285c2-152">Centre des États-Unis</span><span class="sxs-lookup"><span data-stu-id="285c2-152">Central US</span></span> | <span data-ttu-id="285c2-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="285c2-153">23.99.160.139</span></span> | <span data-ttu-id="285c2-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="285c2-154">13.67.215.62</span></span> |
| <span data-ttu-id="285c2-155">Est de l'Asie</span><span class="sxs-lookup"><span data-stu-id="285c2-155">East Asia</span></span> | <span data-ttu-id="285c2-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="285c2-156">191.234.2.139</span></span> | <span data-ttu-id="285c2-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="285c2-157">52.175.33.150</span></span> |
| <span data-ttu-id="285c2-158">Est des États-Unis 1</span><span class="sxs-lookup"><span data-stu-id="285c2-158">East US 1</span></span> | <span data-ttu-id="285c2-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="285c2-159">191.238.6.43</span></span> | <span data-ttu-id="285c2-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="285c2-160">40.121.158.30</span></span> |
| <span data-ttu-id="285c2-161">Est des États-Unis 2</span><span class="sxs-lookup"><span data-stu-id="285c2-161">East US 2</span></span> | <span data-ttu-id="285c2-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="285c2-162">191.239.224.107</span></span> | <span data-ttu-id="285c2-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="285c2-163">40.79.84.180</span></span> |
| <span data-ttu-id="285c2-164">Inde-Centre</span><span class="sxs-lookup"><span data-stu-id="285c2-164">India Central</span></span> | <span data-ttu-id="285c2-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="285c2-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="285c2-166">Sud de l'Inde</span><span class="sxs-lookup"><span data-stu-id="285c2-166">India South</span></span> | <span data-ttu-id="285c2-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="285c2-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="285c2-168">Inde-Ouest</span><span class="sxs-lookup"><span data-stu-id="285c2-168">India West</span></span> | <span data-ttu-id="285c2-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="285c2-169">104.211.160.80</span></span> | |
| <span data-ttu-id="285c2-170">Est du Japon</span><span class="sxs-lookup"><span data-stu-id="285c2-170">Japan East</span></span> | <span data-ttu-id="285c2-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="285c2-171">191.237.240.43</span></span> | <span data-ttu-id="285c2-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="285c2-172">13.78.61.196</span></span> |
| <span data-ttu-id="285c2-173">Ouest du Japon</span><span class="sxs-lookup"><span data-stu-id="285c2-173">Japan West</span></span> | <span data-ttu-id="285c2-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="285c2-174">191.238.68.11</span></span> | <span data-ttu-id="285c2-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="285c2-175">104.214.148.156</span></span> |
| <span data-ttu-id="285c2-176">Centre de la Corée</span><span class="sxs-lookup"><span data-stu-id="285c2-176">Korea Central</span></span> | <span data-ttu-id="285c2-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="285c2-177">52.231.32.42</span></span> | |
| <span data-ttu-id="285c2-178">Corée du Sud</span><span class="sxs-lookup"><span data-stu-id="285c2-178">Korea South</span></span> | <span data-ttu-id="285c2-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="285c2-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="285c2-180">États-Unis - partie centrale septentrionale</span><span class="sxs-lookup"><span data-stu-id="285c2-180">North Central US</span></span> | <span data-ttu-id="285c2-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="285c2-181">23.98.55.75</span></span> | <span data-ttu-id="285c2-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="285c2-182">23.96.178.199</span></span> |
| <span data-ttu-id="285c2-183">Europe du Nord</span><span class="sxs-lookup"><span data-stu-id="285c2-183">North Europe</span></span> | <span data-ttu-id="285c2-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="285c2-184">191.235.193.75</span></span> | <span data-ttu-id="285c2-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="285c2-185">40.113.93.91</span></span> |
| <span data-ttu-id="285c2-186">Centre-Sud des États-Unis</span><span class="sxs-lookup"><span data-stu-id="285c2-186">South Central US</span></span> | <span data-ttu-id="285c2-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="285c2-187">23.98.162.75</span></span> | <span data-ttu-id="285c2-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="285c2-188">13.66.62.124</span></span> |
| <span data-ttu-id="285c2-189">Asie du Sud-Est</span><span class="sxs-lookup"><span data-stu-id="285c2-189">South East Asia</span></span> | <span data-ttu-id="285c2-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="285c2-190">23.100.117.95</span></span> | <span data-ttu-id="285c2-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="285c2-191">104.43.15.0</span></span> |
| <span data-ttu-id="285c2-192">Nord du Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="285c2-192">UK North</span></span> | <span data-ttu-id="285c2-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="285c2-193">13.87.97.210</span></span> | |
| <span data-ttu-id="285c2-194">Sud du Royaume-Uni 1</span><span class="sxs-lookup"><span data-stu-id="285c2-194">UK South 1</span></span> | <span data-ttu-id="285c2-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="285c2-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="285c2-196">Sud du Royaume-Uni 2</span><span class="sxs-lookup"><span data-stu-id="285c2-196">UK South 2</span></span> | <span data-ttu-id="285c2-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="285c2-197">13.87.34.7</span></span> | |
| <span data-ttu-id="285c2-198">Ouest du Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="285c2-198">UK West</span></span> | <span data-ttu-id="285c2-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="285c2-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="285c2-200">Centre-Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="285c2-200">West Central US</span></span> | <span data-ttu-id="285c2-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="285c2-201">13.78.145.25</span></span> | |
| <span data-ttu-id="285c2-202">Europe de l'Ouest</span><span class="sxs-lookup"><span data-stu-id="285c2-202">West Europe</span></span> | <span data-ttu-id="285c2-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="285c2-203">191.237.232.75</span></span> | <span data-ttu-id="285c2-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="285c2-204">40.68.37.158</span></span> |
| <span data-ttu-id="285c2-205">Ouest des États-Unis 1</span><span class="sxs-lookup"><span data-stu-id="285c2-205">West US 1</span></span> | <span data-ttu-id="285c2-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="285c2-206">23.99.34.75</span></span> | <span data-ttu-id="285c2-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="285c2-207">104.42.238.205</span></span> |
| <span data-ttu-id="285c2-208">Ouest des États-Unis 2</span><span class="sxs-lookup"><span data-stu-id="285c2-208">West US 2</span></span> | <span data-ttu-id="285c2-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="285c2-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="285c2-210">Modifier la stratégie de connexion Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="285c2-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="285c2-211">toochange hello stratégie de connexion de base de données SQL Azure pour un serveur de base de données SQL Azure, utilisez hello [API REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="285c2-211">toochange hello Azure SQL Database connection policy for an Azure SQL Database server, use hello [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="285c2-212">Si votre stratégie de connexion est défini trop**Proxy**, tous les flux de paquets via une passerelle de base de données SQL Azure hello du réseau.</span><span class="sxs-lookup"><span data-stu-id="285c2-212">If your connection policy is set too**Proxy**, all network packets flow via hello Azure SQL Database gateway.</span></span> <span data-ttu-id="285c2-213">Pour ce paramètre, vous devez IP de passerelle de base de données SQL Azure tooallow tooonly sortant hello.</span><span class="sxs-lookup"><span data-stu-id="285c2-213">For this setting, you need tooallow outbound tooonly hello Azure SQL Database gateway IP.</span></span> <span data-ttu-id="285c2-214">L’utilisation d’un paramètre de **Proxy** offre plus de latence qu’un paramètre de **redirection**.</span><span class="sxs-lookup"><span data-stu-id="285c2-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="285c2-215">Si la définition de votre stratégie de connexion **rediriger**, tous les paquets réseau flux directement toohello intergiciel (middleware) proxy.</span><span class="sxs-lookup"><span data-stu-id="285c2-215">If your connection policy is setting **Redirect**, all network packets flow directly toohello middleware proxy.</span></span> <span data-ttu-id="285c2-216">Pour ce paramètre, vous devez toomultiple sortant de tooallow des adresses IP.</span><span class="sxs-lookup"><span data-stu-id="285c2-216">For this setting, you need tooallow outbound toomultiple IPs.</span></span> 

## <a name="script-toochange-connection-settings"></a><span data-ttu-id="285c2-217">Paramètres de script de connexion toochange</span><span class="sxs-lookup"><span data-stu-id="285c2-217">Script toochange connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="285c2-218">Ce script nécessite hello [module Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="285c2-218">This script requires hello [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="285c2-219">Hello PowerShell script suivant montre comment toochange hello stratégie de connexion.</span><span class="sxs-lookup"><span data-stu-id="285c2-219">hello following PowerShell script shows how toochange hello connection policy.</span></span>

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="285c2-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="285c2-220">Next steps</span></span>

- <span data-ttu-id="285c2-221">Pour plus d’informations sur la façon dont toochange hello stratégie de connexion de base de données SQL Azure pour un serveur de base de données SQL Azure, consultez [à l’aide de Create ou de la stratégie de mise à jour de connexion serveur hello API REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="285c2-221">For information on how toochange hello Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using hello REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="285c2-222">Pour plus d’informations sur le comportement de connexion d’Azure SQL Database pour les clients qui utilisent ADO.NET version 4.5 ou ultérieure, consultez [Ports au-delà de 1433 pour ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="285c2-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="285c2-223">Pour en savoir plus sur la vue d’ensemble du développement d’applications générales, consultez [Vue d’ensemble du développement de base de données SQL](sql-database-develop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="285c2-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
