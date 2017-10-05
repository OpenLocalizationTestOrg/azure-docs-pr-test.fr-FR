---
title: "Architecture de connectivité Azure SQL Database | Microsoft Docs"
description: "Ce document décrit l’architecture de connectivité Azure SQLDB dans et en dehors d’Azure."
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
ms.openlocfilehash: 8a1dd89c9e82483184ceb5d767190a5a5044265d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a><span data-ttu-id="60c0c-103">Architecture de connectivité Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="60c0c-103">Azure SQL Database Connectivity Architecture</span></span> 

<span data-ttu-id="60c0c-104">Cet article explique l’architecture de connectivité Azure SQL Database et comment les différents composants fonctionnent pour diriger le trafic vers votre instance Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="60c0c-104">This article explains the Azure SQL Database connectivity architecture and explains how the different components function to direct traffic to your instance of Azure SQL Database.</span></span> <span data-ttu-id="60c0c-105">Ces composants de connectivité Azure SQL Database permettent de diriger le trafic réseau vers la base de données Azure avec des clients se connectant à partir d’Azure et d’autres se connectant en dehors d’Azure.</span><span class="sxs-lookup"><span data-stu-id="60c0c-105">These Azure SQL Database connectivity components function to direct network traffic to the Azure database with clients connecting from within Azure and with clients connecting from outside of Azure.</span></span> <span data-ttu-id="60c0c-106">Cet article comporte également des exemples de script permettant de modifier la façon dont la connectivité se produit et des considérations liées à la modification des paramètres de connectivité par défaut.</span><span class="sxs-lookup"><span data-stu-id="60c0c-106">This article also provides script samples to change how connectivity occurs, and the considerations related to changing the default connectivity settings.</span></span> <span data-ttu-id="60c0c-107">Si vous avez des questions suite à la lecture de cet article, veuillez contacter Dhruv à l’adresse suivante : dmalik@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="60c0c-107">If there are any questions after reading this article, please contact Dhruv at dmalik@microsoft.com.</span></span> 

## <a name="connectivity-architecture"></a><span data-ttu-id="60c0c-108">Architecture de connectivité</span><span class="sxs-lookup"><span data-stu-id="60c0c-108">Connectivity architecture</span></span>

<span data-ttu-id="60c0c-109">Le diagramme suivant donne une vue d’ensemble détaillée de l’architecture de connectivité Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="60c0c-109">The following diagram provides a high-level overview of the Azure SQL Database connectivity architecture.</span></span> 

![Présentation de l’architecture](./media/sql-database-connectivity-architecture/architecture-overview.png)


<span data-ttu-id="60c0c-111">Les étapes suivantes décrivent la manière dont une connexion est établie vers une base de données SQL Azure via l’équilibreur de charge logiciel et la passerelle Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="60c0c-111">The following steps describe how a connection is established to an Azure SQL database through the Azure SQL Database software load-balancer (SLB) and the Azure SQL Database gateway.</span></span>

- <span data-ttu-id="60c0c-112">Les clients dans Azure ou en dehors d’Azure se connectent à l’équilibreur de charge logiciel, qui détient une adresse IP publique et écoute le port 1433.</span><span class="sxs-lookup"><span data-stu-id="60c0c-112">Clients within Azure or outside of Azure connect to the SLB, which has a public IP address and listens on port 1433.</span></span>
- <span data-ttu-id="60c0c-113">L’équilibreur de charge logiciel dirige le trafic vers la passerelle Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="60c0c-113">The SLB directs traffic to the Azure SQL Database gateway.</span></span>
- <span data-ttu-id="60c0c-114">La passerelle redirige le trafic vers l’intergiciel de proxy approprié.</span><span class="sxs-lookup"><span data-stu-id="60c0c-114">The gateway redirects the traffic to the correct proxy middleware.</span></span>
- <span data-ttu-id="60c0c-115">Ce dernier redirige le trafic vers la base de données SQL Azure appropriée.</span><span class="sxs-lookup"><span data-stu-id="60c0c-115">The proxy middleware redirects the traffic to the appropriate Azure SQL database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60c0c-116">Chacun de ces composants dispose d’une protection contre les attaques par déni de service distribué (DDoS) intégrée au niveau du réseau et de la couche d’application.</span><span class="sxs-lookup"><span data-stu-id="60c0c-116">Each of these components has distributed denial of service (DDoS) protection built-in at the network and the app layer.</span></span>
>

## <a name="connectivity-from-within-azure"></a><span data-ttu-id="60c0c-117">Connectivité dans Azure</span><span class="sxs-lookup"><span data-stu-id="60c0c-117">Connectivity from within Azure</span></span>

<span data-ttu-id="60c0c-118">Si vous vous connectez à partir d’Azure, vos connexions ont une stratégie de connexion par **redirection** par défaut.</span><span class="sxs-lookup"><span data-stu-id="60c0c-118">If you are connecting from within Azure, your connections have a connection policy of **Redirect** by default.</span></span> <span data-ttu-id="60c0c-119">Une stratégie de **redirection** signifie qu’une fois les connexions établies après la session TCP vers la base de données SQL Azure, la session du client est redirigée vers l’intergiciel de proxy en modifiant l’adresse (en la faisant passer de celle de la passerelle de base de données SQL Azure à celle de l’intergiciel de proxy).</span><span class="sxs-lookup"><span data-stu-id="60c0c-119">A policy of **Redirect** means that connections after the TCP session is established to the Azure SQL database, the client session is then redirected to the proxy middleware with a change to the destination virtual IP from that of the Azure SQL Database gateway to that of the proxy middleware.</span></span> <span data-ttu-id="60c0c-120">Ainsi, tous les paquets suivants flux se dirigent directement vers l’intergiciel de proxy en ignorant la passerelle Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="60c0c-120">Thereafter, all subsequent packets flow directly via the proxy middleware, bypassing the Azure SQL Database gateway.</span></span> <span data-ttu-id="60c0c-121">Le schéma suivant illustre ce flux de trafic :</span><span class="sxs-lookup"><span data-stu-id="60c0c-121">The following diagram illustrates this traffic flow.</span></span>

![Présentation de l’architecture](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a><span data-ttu-id="60c0c-123">Connectivité en dehors d’Azure</span><span class="sxs-lookup"><span data-stu-id="60c0c-123">Connectivity from outside of Azure</span></span>

<span data-ttu-id="60c0c-124">Si vous vous connectez en dehors d’Azure, vos connexions disposent d’une stratégie de connexion de **proxy** par défaut.</span><span class="sxs-lookup"><span data-stu-id="60c0c-124">If you are connecting from outside Azure, your connections have a connection policy of **Proxy** by default.</span></span> <span data-ttu-id="60c0c-125">Une stratégie de **Proxy** signifie que la session TCP est établie via la passerelle Azure SQL Database et que tous les paquets suivants transitent via la passerelle.</span><span class="sxs-lookup"><span data-stu-id="60c0c-125">A policy of **Proxy** means that the TCP session is established via the Azure SQL Database gateway and all subsequent packets flow via the gateway.</span></span> <span data-ttu-id="60c0c-126">Le schéma suivant illustre ce flux de trafic :</span><span class="sxs-lookup"><span data-stu-id="60c0c-126">The following diagram illustrates this traffic flow.</span></span>

![Présentation de l’architecture](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a><span data-ttu-id="60c0c-128">Adresses IP de la passerelle Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="60c0c-128">Azure SQL Database gateway IP addresses</span></span>

<span data-ttu-id="60c0c-129">Pour vous connecter à une base de données SQL Azure à partir de ressources locales, vous devez autoriser le trafic réseau sortant vers la passerelle Azure SQL Database pour votre région Azure.</span><span class="sxs-lookup"><span data-stu-id="60c0c-129">To connect to an Azure SQL database from on-premises resources, you need to allow outbound network traffic to the Azure SQL Database gateway for your Azure region.</span></span> <span data-ttu-id="60c0c-130">Les connexions transitent uniquement via la passerelle lors de la connexion en mode Proxy, qui est le mode par défaut lors de la connexion à partir de ressources locales.</span><span class="sxs-lookup"><span data-stu-id="60c0c-130">Your connections only go via the gateway when connecting in Proxy mode, which is the default when connecting from on-premises resources.</span></span>

<span data-ttu-id="60c0c-131">Le tableau suivant répertorie les adresses IP principales et secondaires de la passerelle Azure SQL Database pour toutes les régions de données.</span><span class="sxs-lookup"><span data-stu-id="60c0c-131">The following table lists the primary and secondary IPs of the Azure SQL Database gateway for all data regions.</span></span> <span data-ttu-id="60c0c-132">Pour certaines régions, il existe deux adresses IP.</span><span class="sxs-lookup"><span data-stu-id="60c0c-132">For some regions, there are two IP addresses.</span></span> <span data-ttu-id="60c0c-133">Dans ces régions, l’adresse IP principale est l’adresse IP actuelle de la passerelle et la deuxième adresse IP est une adresse IP de basculement.</span><span class="sxs-lookup"><span data-stu-id="60c0c-133">In these regions, the primary IP address is the current IP address of the gateway and the second IP address is a failover IP address.</span></span> <span data-ttu-id="60c0c-134">L’adresse de basculement est l’adresse vers laquelle nous pouvons déplacer votre serveur pour maintenir la haute disponibilité du service.</span><span class="sxs-lookup"><span data-stu-id="60c0c-134">The failover address is the address to which we might move your server to keep the service availability high.</span></span> <span data-ttu-id="60c0c-135">Pour ces régions, nous vous conseillons d’autoriser le trafic sortant vers les deux adresses IP.</span><span class="sxs-lookup"><span data-stu-id="60c0c-135">For these regions, we recommend that you allow outbound to both the IP addresses.</span></span> <span data-ttu-id="60c0c-136">La deuxième adresse IP est détenue par Microsoft et n’écoute pas les services tant qu’elle n’est pas activée par Azure SQL Database de manière à accepter les connexions.</span><span class="sxs-lookup"><span data-stu-id="60c0c-136">The second IP address is owned by Microsoft and does not listen in on any services until it is activated by Azure SQL Database to accept connections.</span></span>

| <span data-ttu-id="60c0c-137">Nom de la région</span><span class="sxs-lookup"><span data-stu-id="60c0c-137">Region Name</span></span> | <span data-ttu-id="60c0c-138">Adresse IP principale</span><span class="sxs-lookup"><span data-stu-id="60c0c-138">Primary IP address</span></span> | <span data-ttu-id="60c0c-139">Adresse IP secondaire</span><span class="sxs-lookup"><span data-stu-id="60c0c-139">Secondary IP address</span></span> |
| --- | --- |--- |
| <span data-ttu-id="60c0c-140">Est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="60c0c-140">Australia East</span></span> | <span data-ttu-id="60c0c-141">191.238.66.109</span><span class="sxs-lookup"><span data-stu-id="60c0c-141">191.238.66.109</span></span> | <span data-ttu-id="60c0c-142">13.75.149.87</span><span class="sxs-lookup"><span data-stu-id="60c0c-142">13.75.149.87</span></span> |
| <span data-ttu-id="60c0c-143">Sud-Est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="60c0c-143">Australia South East</span></span> | <span data-ttu-id="60c0c-144">191.239.192.109</span><span class="sxs-lookup"><span data-stu-id="60c0c-144">191.239.192.109</span></span> | <span data-ttu-id="60c0c-145">13.73.109.251</span><span class="sxs-lookup"><span data-stu-id="60c0c-145">13.73.109.251</span></span> |
| <span data-ttu-id="60c0c-146">Sud du Brésil</span><span class="sxs-lookup"><span data-stu-id="60c0c-146">Brazil South</span></span> | <span data-ttu-id="60c0c-147">104.41.11.5</span><span class="sxs-lookup"><span data-stu-id="60c0c-147">104.41.11.5</span></span> | |    
| <span data-ttu-id="60c0c-148">Centre du Canada</span><span class="sxs-lookup"><span data-stu-id="60c0c-148">Canada Central</span></span> | <span data-ttu-id="60c0c-149">40.85.224.249</span><span class="sxs-lookup"><span data-stu-id="60c0c-149">40.85.224.249</span></span> | |    
| <span data-ttu-id="60c0c-150">Est du Canada</span><span class="sxs-lookup"><span data-stu-id="60c0c-150">Canada East</span></span> | <span data-ttu-id="60c0c-151">40.86.226.166</span><span class="sxs-lookup"><span data-stu-id="60c0c-151">40.86.226.166</span></span> | |
| <span data-ttu-id="60c0c-152">Centre des États-Unis</span><span class="sxs-lookup"><span data-stu-id="60c0c-152">Central US</span></span> | <span data-ttu-id="60c0c-153">23.99.160.139</span><span class="sxs-lookup"><span data-stu-id="60c0c-153">23.99.160.139</span></span> | <span data-ttu-id="60c0c-154">13.67.215.62</span><span class="sxs-lookup"><span data-stu-id="60c0c-154">13.67.215.62</span></span> |
| <span data-ttu-id="60c0c-155">Est de l'Asie</span><span class="sxs-lookup"><span data-stu-id="60c0c-155">East Asia</span></span> | <span data-ttu-id="60c0c-156">191.234.2.139</span><span class="sxs-lookup"><span data-stu-id="60c0c-156">191.234.2.139</span></span> | <span data-ttu-id="60c0c-157">52.175.33.150</span><span class="sxs-lookup"><span data-stu-id="60c0c-157">52.175.33.150</span></span> |
| <span data-ttu-id="60c0c-158">Est des États-Unis 1</span><span class="sxs-lookup"><span data-stu-id="60c0c-158">East US 1</span></span> | <span data-ttu-id="60c0c-159">191.238.6.43</span><span class="sxs-lookup"><span data-stu-id="60c0c-159">191.238.6.43</span></span> | <span data-ttu-id="60c0c-160">40.121.158.30</span><span class="sxs-lookup"><span data-stu-id="60c0c-160">40.121.158.30</span></span> |
| <span data-ttu-id="60c0c-161">Est des États-Unis 2</span><span class="sxs-lookup"><span data-stu-id="60c0c-161">East US 2</span></span> | <span data-ttu-id="60c0c-162">191.239.224.107</span><span class="sxs-lookup"><span data-stu-id="60c0c-162">191.239.224.107</span></span> | <span data-ttu-id="60c0c-163">40.79.84.180</span><span class="sxs-lookup"><span data-stu-id="60c0c-163">40.79.84.180</span></span> |
| <span data-ttu-id="60c0c-164">Inde-Centre</span><span class="sxs-lookup"><span data-stu-id="60c0c-164">India Central</span></span> | <span data-ttu-id="60c0c-165">104.211.96.159</span><span class="sxs-lookup"><span data-stu-id="60c0c-165">104.211.96.159</span></span>  | |   
| <span data-ttu-id="60c0c-166">Sud de l'Inde</span><span class="sxs-lookup"><span data-stu-id="60c0c-166">India South</span></span> | <span data-ttu-id="60c0c-167">104.211.224.146</span><span class="sxs-lookup"><span data-stu-id="60c0c-167">104.211.224.146</span></span>  | |
| <span data-ttu-id="60c0c-168">Inde-Ouest</span><span class="sxs-lookup"><span data-stu-id="60c0c-168">India West</span></span> | <span data-ttu-id="60c0c-169">104.211.160.80</span><span class="sxs-lookup"><span data-stu-id="60c0c-169">104.211.160.80</span></span> | |
| <span data-ttu-id="60c0c-170">Est du Japon</span><span class="sxs-lookup"><span data-stu-id="60c0c-170">Japan East</span></span> | <span data-ttu-id="60c0c-171">191.237.240.43</span><span class="sxs-lookup"><span data-stu-id="60c0c-171">191.237.240.43</span></span> | <span data-ttu-id="60c0c-172">13.78.61.196</span><span class="sxs-lookup"><span data-stu-id="60c0c-172">13.78.61.196</span></span> |
| <span data-ttu-id="60c0c-173">Ouest du Japon</span><span class="sxs-lookup"><span data-stu-id="60c0c-173">Japan West</span></span> | <span data-ttu-id="60c0c-174">191.238.68.11</span><span class="sxs-lookup"><span data-stu-id="60c0c-174">191.238.68.11</span></span> | <span data-ttu-id="60c0c-175">104.214.148.156</span><span class="sxs-lookup"><span data-stu-id="60c0c-175">104.214.148.156</span></span> |
| <span data-ttu-id="60c0c-176">Centre de la Corée</span><span class="sxs-lookup"><span data-stu-id="60c0c-176">Korea Central</span></span> | <span data-ttu-id="60c0c-177">52.231.32.42</span><span class="sxs-lookup"><span data-stu-id="60c0c-177">52.231.32.42</span></span> | |
| <span data-ttu-id="60c0c-178">Corée du Sud</span><span class="sxs-lookup"><span data-stu-id="60c0c-178">Korea South</span></span> | <span data-ttu-id="60c0c-179">52.231.200.86</span><span class="sxs-lookup"><span data-stu-id="60c0c-179">52.231.200.86</span></span> |  |
| <span data-ttu-id="60c0c-180">États-Unis - partie centrale septentrionale</span><span class="sxs-lookup"><span data-stu-id="60c0c-180">North Central US</span></span> | <span data-ttu-id="60c0c-181">23.98.55.75</span><span class="sxs-lookup"><span data-stu-id="60c0c-181">23.98.55.75</span></span> | <span data-ttu-id="60c0c-182">23.96.178.199</span><span class="sxs-lookup"><span data-stu-id="60c0c-182">23.96.178.199</span></span> |
| <span data-ttu-id="60c0c-183">Europe du Nord</span><span class="sxs-lookup"><span data-stu-id="60c0c-183">North Europe</span></span> | <span data-ttu-id="60c0c-184">191.235.193.75</span><span class="sxs-lookup"><span data-stu-id="60c0c-184">191.235.193.75</span></span> | <span data-ttu-id="60c0c-185">40.113.93.91</span><span class="sxs-lookup"><span data-stu-id="60c0c-185">40.113.93.91</span></span> |
| <span data-ttu-id="60c0c-186">Centre-Sud des États-Unis</span><span class="sxs-lookup"><span data-stu-id="60c0c-186">South Central US</span></span> | <span data-ttu-id="60c0c-187">23.98.162.75</span><span class="sxs-lookup"><span data-stu-id="60c0c-187">23.98.162.75</span></span> | <span data-ttu-id="60c0c-188">13.66.62.124</span><span class="sxs-lookup"><span data-stu-id="60c0c-188">13.66.62.124</span></span> |
| <span data-ttu-id="60c0c-189">Asie du Sud-Est</span><span class="sxs-lookup"><span data-stu-id="60c0c-189">South East Asia</span></span> | <span data-ttu-id="60c0c-190">23.100.117.95</span><span class="sxs-lookup"><span data-stu-id="60c0c-190">23.100.117.95</span></span> | <span data-ttu-id="60c0c-191">104.43.15.0</span><span class="sxs-lookup"><span data-stu-id="60c0c-191">104.43.15.0</span></span> |
| <span data-ttu-id="60c0c-192">Nord du Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="60c0c-192">UK North</span></span> | <span data-ttu-id="60c0c-193">13.87.97.210</span><span class="sxs-lookup"><span data-stu-id="60c0c-193">13.87.97.210</span></span> | |
| <span data-ttu-id="60c0c-194">Sud du Royaume-Uni 1</span><span class="sxs-lookup"><span data-stu-id="60c0c-194">UK South 1</span></span> | <span data-ttu-id="60c0c-195">51.140.184.11</span><span class="sxs-lookup"><span data-stu-id="60c0c-195">51.140.184.11</span></span> | |    
| <span data-ttu-id="60c0c-196">Sud du Royaume-Uni 2</span><span class="sxs-lookup"><span data-stu-id="60c0c-196">UK South 2</span></span> | <span data-ttu-id="60c0c-197">13.87.34.7</span><span class="sxs-lookup"><span data-stu-id="60c0c-197">13.87.34.7</span></span> | |
| <span data-ttu-id="60c0c-198">Ouest du Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="60c0c-198">UK West</span></span> | <span data-ttu-id="60c0c-199">51.141.8.11</span><span class="sxs-lookup"><span data-stu-id="60c0c-199">51.141.8.11</span></span>  | |
| <span data-ttu-id="60c0c-200">Centre-Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="60c0c-200">West Central US</span></span> | <span data-ttu-id="60c0c-201">13.78.145.25</span><span class="sxs-lookup"><span data-stu-id="60c0c-201">13.78.145.25</span></span> | |
| <span data-ttu-id="60c0c-202">Europe de l'Ouest</span><span class="sxs-lookup"><span data-stu-id="60c0c-202">West Europe</span></span> | <span data-ttu-id="60c0c-203">191.237.232.75</span><span class="sxs-lookup"><span data-stu-id="60c0c-203">191.237.232.75</span></span> | <span data-ttu-id="60c0c-204">40.68.37.158</span><span class="sxs-lookup"><span data-stu-id="60c0c-204">40.68.37.158</span></span> |
| <span data-ttu-id="60c0c-205">Ouest des États-Unis 1</span><span class="sxs-lookup"><span data-stu-id="60c0c-205">West US 1</span></span> | <span data-ttu-id="60c0c-206">23.99.34.75</span><span class="sxs-lookup"><span data-stu-id="60c0c-206">23.99.34.75</span></span> | <span data-ttu-id="60c0c-207">104.42.238.205</span><span class="sxs-lookup"><span data-stu-id="60c0c-207">104.42.238.205</span></span> |
| <span data-ttu-id="60c0c-208">Ouest des États-Unis 2</span><span class="sxs-lookup"><span data-stu-id="60c0c-208">West US 2</span></span> | <span data-ttu-id="60c0c-209">13.66.226.202</span><span class="sxs-lookup"><span data-stu-id="60c0c-209">13.66.226.202</span></span>  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a><span data-ttu-id="60c0c-210">Modifier la stratégie de connexion Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="60c0c-210">Change Azure SQL Database connection policy</span></span>

<span data-ttu-id="60c0c-211">Pour modifier la stratégie de connexion Azure SQL Database d’un serveur Azure SQL Database, utilisez l’[API REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span><span class="sxs-lookup"><span data-stu-id="60c0c-211">To change the Azure SQL Database connection policy for an Azure SQL Database server, use the [REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span> 

- <span data-ttu-id="60c0c-212">Si votre stratégie de connexion est définie sur **Proxy**, tous les paquets réseau transitent via la passerelle Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="60c0c-212">If your connection policy is set to **Proxy**, all network packets flow via the Azure SQL Database gateway.</span></span> <span data-ttu-id="60c0c-213">Pour ce paramètre, vous devez autoriser le trafic sortant uniquement vers l’IP de la passerelle Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="60c0c-213">For this setting, you need to allow outbound to only the Azure SQL Database gateway IP.</span></span> <span data-ttu-id="60c0c-214">L’utilisation d’un paramètre de **Proxy** offre plus de latence qu’un paramètre de **redirection**.</span><span class="sxs-lookup"><span data-stu-id="60c0c-214">Using a setting of **Proxy** has more latency than a setting of **Redirect**.</span></span> 
- <span data-ttu-id="60c0c-215">Si votre stratégie de connexion repose sur le paramètre de **redirection**, tous les paquets réseau se dirigent directement vers le proxy de l’intergiciel.</span><span class="sxs-lookup"><span data-stu-id="60c0c-215">If your connection policy is setting **Redirect**, all network packets flow directly to the middleware proxy.</span></span> <span data-ttu-id="60c0c-216">Pour ce paramètre, vous devez autoriser le trafic sortant vers plusieurs adresses IP.</span><span class="sxs-lookup"><span data-stu-id="60c0c-216">For this setting, you need to allow outbound to multiple IPs.</span></span> 

## <a name="script-to-change-connection-settings"></a><span data-ttu-id="60c0c-217">Script permettant de modifier les paramètres de connexion</span><span class="sxs-lookup"><span data-stu-id="60c0c-217">Script to change connection settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60c0c-218">Ce script nécessite le [module Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="60c0c-218">This script requires the [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
>

<span data-ttu-id="60c0c-219">Le script PowerShell suivant montre comment modifier la stratégie de connexion.</span><span class="sxs-lookup"><span data-stu-id="60c0c-219">The following PowerShell script shows how to change the connection policy.</span></span>

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

#getting the current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting the property to ‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a><span data-ttu-id="60c0c-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="60c0c-220">Next steps</span></span>

- <span data-ttu-id="60c0c-221">Pour plus d’informations sur la façon de modifier la stratégie de connexion Azure SQL Database d’un serveur Azure SQL Database, consultez [Create or Update Server Connection Policy using the REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx) (Créer ou mettre à jour la stratégie de connexion au serveur à l’aide de l’API REST).</span><span class="sxs-lookup"><span data-stu-id="60c0c-221">For information on how to change the Azure SQL Database connection policy for an Azure SQL Database server, see [Create or Update Server Connection Policy using the REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx).</span></span>
- <span data-ttu-id="60c0c-222">Pour plus d’informations sur le comportement de connexion d’Azure SQL Database pour les clients qui utilisent ADO.NET version 4.5 ou ultérieure, consultez [Ports au-delà de 1433 pour ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="60c0c-222">For information about Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version, see [Ports beyond 1433 for ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
- <span data-ttu-id="60c0c-223">Pour en savoir plus sur la vue d’ensemble du développement d’applications générales, consultez [Vue d’ensemble du développement de base de données SQL](sql-database-develop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="60c0c-223">For general application development overview information, see [SQL Database Application Development Overview](sql-database-develop-overview.md).</span></span>
