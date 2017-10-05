---
title: "Procédure pas à pas d’exemple d’infrastructure Azure | Microsoft Docs"
description: "Découvrez-en plus sur les principales instructions de conception et d’implémentation pour le déploiement d’un exemple d’infrastructure dans Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 281fc2c0-b533-45fa-81a3-728c0049c73d
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b18be0d81d6fad7328edb47c9b69af4eecd3b971
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a><span data-ttu-id="2f3ce-103">Procédure pas à pas d’exemple d’infrastructure Azure pour les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="2f3ce-103">Example Azure infrastructure walkthrough for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="2f3ce-104">Cet article vous guide à travers la création d’un exemple d’infrastructure d’application.</span><span class="sxs-lookup"><span data-stu-id="2f3ce-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="2f3ce-105">Nous détaillons la conception d’une infrastructure pour un magasin en ligne simple qui réunit toutes les instructions et les décisions concernant les conventions de dénomination, les groupes à haute disponibilité, les réseaux virtuels et équilibreurs de charge, ainsi que le déploiement de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2f3ce-105">We detail designing an infrastructure for a simple on-line store that brings together all the guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="2f3ce-106">Exemple de charge de travail</span><span class="sxs-lookup"><span data-stu-id="2f3ce-106">Example workload</span></span>
<span data-ttu-id="2f3ce-107">Adventure Works Cycles souhaite créer une application de magasin en ligne dans Azure, avec :</span><span class="sxs-lookup"><span data-stu-id="2f3ce-107">Adventure Works Cycles wants to build an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="2f3ce-108">Deux serveurs nginx exécutant le client frontal dans une couche web</span><span class="sxs-lookup"><span data-stu-id="2f3ce-108">Two nginx servers running the client front-end in a web tier</span></span>
* <span data-ttu-id="2f3ce-109">Deux serveurs nginx pour le traitement des données et des commandes dans une couche d’application</span><span class="sxs-lookup"><span data-stu-id="2f3ce-109">Two nginx servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="2f3ce-110">Deux serveurs MongoDB faisant partie d’un cluster partitionné pour le stockage des données sur les produits et des commandes dans une couche de base de données</span><span class="sxs-lookup"><span data-stu-id="2f3ce-110">Two MongoDB servers part of a sharded cluster for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="2f3ce-111">Deux contrôleurs de domaine Active Directory pour les comptes clients et les fournisseurs dans une couche d’authentification</span><span class="sxs-lookup"><span data-stu-id="2f3ce-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="2f3ce-112">Tous les serveurs se trouvent dans deux sous-réseaux :</span><span class="sxs-lookup"><span data-stu-id="2f3ce-112">All the servers are located in two subnets:</span></span>
  * <span data-ttu-id="2f3ce-113">un sous-réseau frontal pour les serveurs web</span><span class="sxs-lookup"><span data-stu-id="2f3ce-113">a front-end subnet for the web servers</span></span> 
  * <span data-ttu-id="2f3ce-114">un sous-réseau principal pour les serveurs d’applications, le cluster MongoDB et les contrôleurs de domaine</span><span class="sxs-lookup"><span data-stu-id="2f3ce-114">a back-end subnet for the application servers, MongoDB cluster, and domain controllers</span></span>

![Diagramme de différentes couches pour l’infrastructure d’applications](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="2f3ce-116">La charge du trafic web entrant sécurisé doit être répartie sur les serveurs web lorsque les clients parcourent le magasin en ligne.</span><span class="sxs-lookup"><span data-stu-id="2f3ce-116">Incoming secure web traffic must be load-balanced among the web servers as customers browse the on-line store.</span></span> <span data-ttu-id="2f3ce-117">Le trafic de traitement des commandes sous la forme de requêtes HTTP provenant des serveurs web doit être à charge équilibrée sur les serveurs d’applications.</span><span class="sxs-lookup"><span data-stu-id="2f3ce-117">Order processing traffic in the form of HTTP requests from the web servers must be load-balanced among the application servers.</span></span> <span data-ttu-id="2f3ce-118">En outre, l’infrastructure doit être conçue pour la haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="2f3ce-118">Additionally, the infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="2f3ce-119">La conception qui en résulte doit comprendre :</span><span class="sxs-lookup"><span data-stu-id="2f3ce-119">The resulting design must incorporate:</span></span>

* <span data-ttu-id="2f3ce-120">Un compte et un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="2f3ce-120">An Azure subscription and account</span></span>
* <span data-ttu-id="2f3ce-121">un seul groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="2f3ce-121">A single resource group</span></span>
* <span data-ttu-id="2f3ce-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="2f3ce-122">Azure Managed Disks</span></span>
* <span data-ttu-id="2f3ce-123">un réseau virtuel avec deux sous-réseaux ;</span><span class="sxs-lookup"><span data-stu-id="2f3ce-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="2f3ce-124">Des groupes à haute disponibilité pour machines virtuelles avec un rôle similaire</span><span class="sxs-lookup"><span data-stu-id="2f3ce-124">Availability sets for the VMs with a similar role</span></span>
* <span data-ttu-id="2f3ce-125">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="2f3ce-125">Virtual machines</span></span>

<span data-ttu-id="2f3ce-126">Tous les éléments ci-dessus sont conformes aux conventions de dénomination :</span><span class="sxs-lookup"><span data-stu-id="2f3ce-126">All the above follow these naming conventions:</span></span>

* <span data-ttu-id="2f3ce-127">Adventure Works Cycles utilise **[Charge de travail informatique]-[Emplacement]-[Ressources Azure]** comme préfixe</span><span class="sxs-lookup"><span data-stu-id="2f3ce-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="2f3ce-128">Pour cet exemple, « **azos** » (Azure On-line Store) est le nom de la charge de travail informatique et « **use** » (États-Unis de l’Est 2) est l’emplacement</span><span class="sxs-lookup"><span data-stu-id="2f3ce-128">For this example, "**azos**" (Azure On-line Store) is the IT workload name and "**use**" (East US 2) is the location</span></span>
* <span data-ttu-id="2f3ce-129">Les réseaux virtuels utilisent AZOS-USE-VN**[numéro]**</span><span class="sxs-lookup"><span data-stu-id="2f3ce-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="2f3ce-130">Les groupes à haute disponibilité utilisent azos-use-as-**[rôle]**</span><span class="sxs-lookup"><span data-stu-id="2f3ce-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="2f3ce-131">Les noms de machine virtuelle utilisent azos-use-vm-**[nom de machine virtuelle]**</span><span class="sxs-lookup"><span data-stu-id="2f3ce-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="2f3ce-132">Abonnements et comptes Azure</span><span class="sxs-lookup"><span data-stu-id="2f3ce-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="2f3ce-133">Adventure Works Cycles utilise son abonnement d’entreprise, nommé Adventure Works Enterprise Subscription, pour fournir des informations de facturation pour cette charge de travail informatique.</span><span class="sxs-lookup"><span data-stu-id="2f3ce-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, to provide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="2f3ce-134">Storage</span><span class="sxs-lookup"><span data-stu-id="2f3ce-134">Storage</span></span>
<span data-ttu-id="2f3ce-135">Adventure Works Cycles a déterminé que des disques managés Azure doivent être utilisés.</span><span class="sxs-lookup"><span data-stu-id="2f3ce-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="2f3ce-136">Lors de la création de machines virtuelles, les deux niveaux de stockage disponibles sont utilisés :</span><span class="sxs-lookup"><span data-stu-id="2f3ce-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="2f3ce-137">**Stockage standard** pour les serveurs web, les serveurs d’applications et les contrôleurs de domaine et leurs disques de données.</span><span class="sxs-lookup"><span data-stu-id="2f3ce-137">**Standard storage** for the web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="2f3ce-138">**Stockage Premium** pour les serveurs de cluster partitionné MongoDB et leurs disques de données.</span><span class="sxs-lookup"><span data-stu-id="2f3ce-138">**Premium storage** for the MongoDB sharded cluster servers and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="2f3ce-139">Réseau virtuel et sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="2f3ce-139">Virtual network and subnets</span></span>
<span data-ttu-id="2f3ce-140">Étant donné que le réseau virtuel n’a pas besoin d’une connectivité continue au réseau Adventure Work Cycles local, il a été décidé d’adopter un réseau virtuel cloud.</span><span class="sxs-lookup"><span data-stu-id="2f3ce-140">Because the virtual network does not need ongoing connectivity to the Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="2f3ce-141">Un réseau virtuel cloud a été créé avec les paramètres suivants via le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="2f3ce-141">They created a cloud-only virtual network with the following settings using the Azure portal:</span></span>

* <span data-ttu-id="2f3ce-142">Nom : AZOS-USE-VN01</span><span class="sxs-lookup"><span data-stu-id="2f3ce-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="2f3ce-143">Emplacement : East US 2</span><span class="sxs-lookup"><span data-stu-id="2f3ce-143">Location: East US 2</span></span>
* <span data-ttu-id="2f3ce-144">Espace d’adressage du réseau virtuel : 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="2f3ce-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="2f3ce-145">Premier sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="2f3ce-145">First subnet:</span></span>
  * <span data-ttu-id="2f3ce-146">Nom : FrontEnd</span><span class="sxs-lookup"><span data-stu-id="2f3ce-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="2f3ce-147">Espace d’adressage : 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="2f3ce-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="2f3ce-148">Second sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="2f3ce-148">Second subnet:</span></span>
  * <span data-ttu-id="2f3ce-149">Nom : BackEnd</span><span class="sxs-lookup"><span data-stu-id="2f3ce-149">Name: BackEnd</span></span>
  * <span data-ttu-id="2f3ce-150">Espace d’adressage : 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="2f3ce-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="2f3ce-151">Groupes à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="2f3ce-151">Availability sets</span></span>
<span data-ttu-id="2f3ce-152">Pour assurer une haute disponibilité sur les quatre couches de son magasin en ligne, Adventure Work Cycles a adopté quatre groupes à haute disponibilité :</span><span class="sxs-lookup"><span data-stu-id="2f3ce-152">To maintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="2f3ce-153">**azos-use-as-web** pour les serveurs web</span><span class="sxs-lookup"><span data-stu-id="2f3ce-153">**azos-use-as-web** for the web servers</span></span>
* <span data-ttu-id="2f3ce-154">**azos-use-as-app** pour les serveurs d’application</span><span class="sxs-lookup"><span data-stu-id="2f3ce-154">**azos-use-as-app** for the application servers</span></span>
* <span data-ttu-id="2f3ce-155">**azos-use-as-db** pour les serveurs du cluster partitionné MongoDB</span><span class="sxs-lookup"><span data-stu-id="2f3ce-155">**azos-use-as-db** for the servers in the MongoDB sharded cluster</span></span>
* <span data-ttu-id="2f3ce-156">**azos-use-as-dc** pour les contrôleurs de domaine</span><span class="sxs-lookup"><span data-stu-id="2f3ce-156">**azos-use-as-dc** for the domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="2f3ce-157">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="2f3ce-157">Virtual machines</span></span>
<span data-ttu-id="2f3ce-158">Adventure Works Cycles a donné les noms suivants à ses machines virtuelles Azure :</span><span class="sxs-lookup"><span data-stu-id="2f3ce-158">Adventure Works Cycles decided on the following names for their Azure VMs:</span></span>

* <span data-ttu-id="2f3ce-159">**azos-use-vm-web01** pour le premier serveur web</span><span class="sxs-lookup"><span data-stu-id="2f3ce-159">**azos-use-vm-web01** for the first web server</span></span>
* <span data-ttu-id="2f3ce-160">**azfae-vm-vm-web02** pour le second serveur web</span><span class="sxs-lookup"><span data-stu-id="2f3ce-160">**azos-use-vm-web02** for the second web server</span></span>
* <span data-ttu-id="2f3ce-161">**azos-use-vm-app01** pour le premier serveur d’applications</span><span class="sxs-lookup"><span data-stu-id="2f3ce-161">**azos-use-vm-app01** for the first application server</span></span>
* <span data-ttu-id="2f3ce-162">**azos-use-vm-app02** pour le second serveur d’applications</span><span class="sxs-lookup"><span data-stu-id="2f3ce-162">**azos-use-vm-app02** for the second application server</span></span>
* <span data-ttu-id="2f3ce-163">**azos-use-vm-db01** pour le premier serveur MongoDB dans le cluster</span><span class="sxs-lookup"><span data-stu-id="2f3ce-163">**azos-use-vm-db01** for the first MongoDB server in the cluster</span></span>
* <span data-ttu-id="2f3ce-164">**azos-use-vm-db02** pour le second serveur MongoDB dans le cluster</span><span class="sxs-lookup"><span data-stu-id="2f3ce-164">**azos-use-vm-db02** for the second MongoDB server in the cluster</span></span>
* <span data-ttu-id="2f3ce-165">**azos-use-vm-dc01** pour le premier contrôleur de domaine</span><span class="sxs-lookup"><span data-stu-id="2f3ce-165">**azos-use-vm-dc01** for the first domain controller</span></span>
* <span data-ttu-id="2f3ce-166">**azos-use-vm-dc02** pour le second contrôleur de domaine</span><span class="sxs-lookup"><span data-stu-id="2f3ce-166">**azos-use-vm-dc02** for the second domain controller</span></span>

<span data-ttu-id="2f3ce-167">Voici la configuration obtenue.</span><span class="sxs-lookup"><span data-stu-id="2f3ce-167">Here is the resulting configuration.</span></span>

![Infrastructure d’applications finale déployée dans Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="2f3ce-169">Cette configuration comprend :</span><span class="sxs-lookup"><span data-stu-id="2f3ce-169">This configuration incorporates:</span></span>

* <span data-ttu-id="2f3ce-170">un réseau virtuel cloud avec deux sous-réseaux (FrontEnd et BackEnd) ;</span><span class="sxs-lookup"><span data-stu-id="2f3ce-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="2f3ce-171">des disques managés Azure utilisant à la fois des disques Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="2f3ce-171">Azure Managed Disks using both Standard and Premium disks</span></span>
* <span data-ttu-id="2f3ce-172">quatre groupes à haute disponibilité, un pour chaque niveau du magasin en ligne</span><span class="sxs-lookup"><span data-stu-id="2f3ce-172">Four availability sets, one for each tier of the on-line store</span></span>
* <span data-ttu-id="2f3ce-173">les machines virtuelles pour les quatre niveaux ;</span><span class="sxs-lookup"><span data-stu-id="2f3ce-173">The virtual machines for the four tiers</span></span>
* <span data-ttu-id="2f3ce-174">un jeu d’équilibrage de charge externe pour le trafic Web basé sur HTTPS depuis Internet vers les serveurs web ;</span><span class="sxs-lookup"><span data-stu-id="2f3ce-174">An external load balanced set for HTTPS-based web traffic from the Internet to the web servers</span></span>
* <span data-ttu-id="2f3ce-175">un jeu d’équilibrage de charge interne pour le trafic Web non crypté depuis les serveurs Web vers les serveurs d’applications.</span><span class="sxs-lookup"><span data-stu-id="2f3ce-175">An internal load balanced set for unencrypted web traffic from the web servers to the application servers</span></span>
* <span data-ttu-id="2f3ce-176">un seul groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="2f3ce-176">A single resource group</span></span>
