---
title: "aaaExample procédure pas à pas de Azure Infrastructure | Documents Microsoft"
description: "Découvrez hello clé conception et implémentation des recommandations pour le déploiement d’une infrastructure d’exemple dans Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd6b6e904404bea0b5be37dfce6d60039daae636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a><span data-ttu-id="a40fb-103">Procédure pas à pas d’exemple d’infrastructure Azure pour les machines virtuelles Windows</span><span class="sxs-lookup"><span data-stu-id="a40fb-103">Example Azure infrastructure walkthrough for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="a40fb-104">Cet article vous guide à travers la création d’un exemple d’infrastructure d’application.</span><span class="sxs-lookup"><span data-stu-id="a40fb-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="a40fb-105">Nous avons décrit en détail la conception d’une infrastructure pour un magasin en ligne simple qui réunit toutes les décisions concernant les conventions d’affectation de noms, des groupes à haute disponibilité, des réseaux virtuels et des équilibreurs de charge et les recommandations de hello et déployer vos machines virtuelles (VM).</span><span class="sxs-lookup"><span data-stu-id="a40fb-105">We detail designing an infrastructure for a simple on-line store that brings together all hello guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="a40fb-106">Exemple de charge de travail</span><span class="sxs-lookup"><span data-stu-id="a40fb-106">Example workload</span></span>
<span data-ttu-id="a40fb-107">Adventure Works Cycles veut toobuild une application de magasin en ligne dans Azure se compose de :</span><span class="sxs-lookup"><span data-stu-id="a40fb-107">Adventure Works Cycles wants toobuild an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="a40fb-108">Deux serveurs IIS exécutant client hello frontal dans une couche web</span><span class="sxs-lookup"><span data-stu-id="a40fb-108">Two IIS servers running hello client front-end in a web tier</span></span>
* <span data-ttu-id="a40fb-109">Deux serveurs IIS pour le traitement des données et des commandes dans une couche d’application</span><span class="sxs-lookup"><span data-stu-id="a40fb-109">Two IIS servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="a40fb-110">Deux instances Microsoft SQL Server avec des groupes de disponibilité AlwaysOn (deux serveurs SQL et un témoin de nœud majoritaire) pour le stockage des données sur les produits et des commandes dans une couche de base de données</span><span class="sxs-lookup"><span data-stu-id="a40fb-110">Two Microsoft SQL Server instances with AlwaysOn availability groups (two SQL Servers and a majority node witness) for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="a40fb-111">Deux contrôleurs de domaine Active Directory pour les comptes clients et les fournisseurs dans une couche d’authentification</span><span class="sxs-lookup"><span data-stu-id="a40fb-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="a40fb-112">Tous les serveurs hello se trouvent dans deux sous-réseaux :</span><span class="sxs-lookup"><span data-stu-id="a40fb-112">All hello servers are located in two subnets:</span></span>
  * <span data-ttu-id="a40fb-113">un sous-réseau frontal pour les serveurs web de hello</span><span class="sxs-lookup"><span data-stu-id="a40fb-113">a front-end subnet for hello web servers</span></span> 
  * <span data-ttu-id="a40fb-114">un sous-réseau principal pour les serveurs d’applications hello, cluster SQL et les contrôleurs de domaine</span><span class="sxs-lookup"><span data-stu-id="a40fb-114">a back-end subnet for hello application servers, SQL cluster, and domain controllers</span></span>

![Diagramme de différentes couches pour l’infrastructure d’applications](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="a40fb-116">Entrant sécuriser le trafic web doit être équilibrée entre les serveurs web de hello clients parcourir la Boutique en ligne hello.</span><span class="sxs-lookup"><span data-stu-id="a40fb-116">Incoming secure web traffic must be load-balanced among hello web servers as customers browse hello on-line store.</span></span> <span data-ttu-id="a40fb-117">Le trafic à l’écran hello du serveur proxy de traitement de la commande demande à partir du web hello serveurs doivent être équilibrées entre les serveurs d’application hello.</span><span class="sxs-lookup"><span data-stu-id="a40fb-117">Order processing traffic in hello form of HTTP requests from hello web servers must be balanced among hello application servers.</span></span> <span data-ttu-id="a40fb-118">En outre, l’infrastructure de hello doit être conçue pour la haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="a40fb-118">Additionally, hello infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="a40fb-119">conception de résultant Hello doit intégrer :</span><span class="sxs-lookup"><span data-stu-id="a40fb-119">hello resulting design must incorporate:</span></span>

* <span data-ttu-id="a40fb-120">Un compte et un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="a40fb-120">An Azure subscription and account</span></span>
* <span data-ttu-id="a40fb-121">un seul groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a40fb-121">A single resource group</span></span>
* <span data-ttu-id="a40fb-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="a40fb-122">Azure Managed Disks</span></span>
* <span data-ttu-id="a40fb-123">un réseau virtuel avec deux sous-réseaux ;</span><span class="sxs-lookup"><span data-stu-id="a40fb-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="a40fb-124">Haute disponibilité pour hello machines virtuelles avec un rôle similaire</span><span class="sxs-lookup"><span data-stu-id="a40fb-124">Availability sets for hello VMs with a similar role</span></span>
* <span data-ttu-id="a40fb-125">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="a40fb-125">Virtual machines</span></span>

<span data-ttu-id="a40fb-126">Tous les hello ci-dessus suivre les conventions d’affectation de noms :</span><span class="sxs-lookup"><span data-stu-id="a40fb-126">All hello above follow these naming conventions:</span></span>

* <span data-ttu-id="a40fb-127">Adventure Works Cycles utilise **[Charge de travail informatique]-[Emplacement]-[Ressources Azure]** comme préfixe</span><span class="sxs-lookup"><span data-stu-id="a40fb-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="a40fb-128">Pour cet exemple, «**azos**» (magasin d’Azure en ligne) est hello nom de la charge de travail informatique et «**utiliser**» (est des États-Unis 2) est l’emplacement de hello</span><span class="sxs-lookup"><span data-stu-id="a40fb-128">For this example, "**azos**" (Azure On-line Store) is hello IT workload name and "**use**" (East US 2) is hello location</span></span>
* <span data-ttu-id="a40fb-129">Les réseaux virtuels utilisent AZOS-USE-VN**[numéro]**</span><span class="sxs-lookup"><span data-stu-id="a40fb-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="a40fb-130">Les groupes à haute disponibilité utilisent azos-use-as-**[rôle]**</span><span class="sxs-lookup"><span data-stu-id="a40fb-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="a40fb-131">Les noms de machine virtuelle utilisent azos-use-vm-**[nom de machine virtuelle]**</span><span class="sxs-lookup"><span data-stu-id="a40fb-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="a40fb-132">Abonnements et comptes Azure</span><span class="sxs-lookup"><span data-stu-id="a40fb-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="a40fb-133">Adventure Works Cycles est à l’aide de leur abonnement Enterprise, nommé abonnement d’entreprise Adventure Works, tooprovide de facturation pour cette charge de travail informatique.</span><span class="sxs-lookup"><span data-stu-id="a40fb-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, tooprovide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="a40fb-134">Storage</span><span class="sxs-lookup"><span data-stu-id="a40fb-134">Storage</span></span>
<span data-ttu-id="a40fb-135">Adventure Works Cycles a déterminé que des disques managés Azure doivent être utilisés.</span><span class="sxs-lookup"><span data-stu-id="a40fb-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="a40fb-136">Lors de la création de machines virtuelles, les deux niveaux de stockage disponibles sont utilisés :</span><span class="sxs-lookup"><span data-stu-id="a40fb-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="a40fb-137">**Stockage standard** pour les serveurs web de hello, les serveurs d’applications et les contrôleurs de domaine et leurs disques de données.</span><span class="sxs-lookup"><span data-stu-id="a40fb-137">**Standard storage** for hello web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="a40fb-138">**Stockage Premium** pour les machines virtuelles hello SQL Server disques et de leurs données.</span><span class="sxs-lookup"><span data-stu-id="a40fb-138">**Premium storage** for hello SQL Server VMs and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="a40fb-139">Réseau virtuel et sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="a40fb-139">Virtual network and subnets</span></span>
<span data-ttu-id="a40fb-140">Car le réseau virtuel de hello ne doit pas de réseau local de connectivité en cours toohello Cycles de travail Adventure, ils ont choisi un réseau virtuel cloud uniquement.</span><span class="sxs-lookup"><span data-stu-id="a40fb-140">Because hello virtual network does not need ongoing connectivity toohello Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="a40fb-141">Ils créé un réseau virtuel cloud uniquement avec hello suivant les paramètres à l’aide de hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="a40fb-141">They created a cloud-only virtual network with hello following settings using hello Azure portal:</span></span>

* <span data-ttu-id="a40fb-142">Nom : AZOS-USE-VN01</span><span class="sxs-lookup"><span data-stu-id="a40fb-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="a40fb-143">Emplacement : East US 2</span><span class="sxs-lookup"><span data-stu-id="a40fb-143">Location: East US 2</span></span>
* <span data-ttu-id="a40fb-144">Espace d’adressage du réseau virtuel : 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="a40fb-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="a40fb-145">Premier sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="a40fb-145">First subnet:</span></span>
  * <span data-ttu-id="a40fb-146">Nom : FrontEnd</span><span class="sxs-lookup"><span data-stu-id="a40fb-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="a40fb-147">Espace d’adressage : 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="a40fb-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="a40fb-148">Second sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="a40fb-148">Second subnet:</span></span>
  * <span data-ttu-id="a40fb-149">Nom : BackEnd</span><span class="sxs-lookup"><span data-stu-id="a40fb-149">Name: BackEnd</span></span>
  * <span data-ttu-id="a40fb-150">Espace d’adressage : 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="a40fb-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="a40fb-151">Groupes à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="a40fb-151">Availability sets</span></span>
<span data-ttu-id="a40fb-152">toomaintain haute disponibilité de toutes les quatre niveaux de leur magasin en ligne, Adventure Works Cycles décidé sur quatre groupes à haute disponibilité :</span><span class="sxs-lookup"><span data-stu-id="a40fb-152">toomaintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="a40fb-153">**Utilisez azos comme web** pour les serveurs web de hello</span><span class="sxs-lookup"><span data-stu-id="a40fb-153">**azos-use-as-web** for hello web servers</span></span>
* <span data-ttu-id="a40fb-154">**Utilisez azos en tant qu’application** des serveurs d’applications hello</span><span class="sxs-lookup"><span data-stu-id="a40fb-154">**azos-use-as-app** for hello application servers</span></span>
* <span data-ttu-id="a40fb-155">**Utilisez azos comme sql** pour hello serveurs SQL</span><span class="sxs-lookup"><span data-stu-id="a40fb-155">**azos-use-as-sql** for hello SQL Servers</span></span>
* <span data-ttu-id="a40fb-156">**Utilisez azos comme dc** hello des contrôleurs de domaine</span><span class="sxs-lookup"><span data-stu-id="a40fb-156">**azos-use-as-dc** for hello domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="a40fb-157">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="a40fb-157">Virtual machines</span></span>
<span data-ttu-id="a40fb-158">Adventure Works Cycles choisi hello suivant des noms pour leurs machines virtuelles Azure :</span><span class="sxs-lookup"><span data-stu-id="a40fb-158">Adventure Works Cycles decided on hello following names for their Azure VMs:</span></span>

* <span data-ttu-id="a40fb-159">**azos-utilisation-vm-web01** pour le premier serveur web de hello</span><span class="sxs-lookup"><span data-stu-id="a40fb-159">**azos-use-vm-web01** for hello first web server</span></span>
* <span data-ttu-id="a40fb-160">**azos-utilisation-vm-web02** pour le second serveur web de hello</span><span class="sxs-lookup"><span data-stu-id="a40fb-160">**azos-use-vm-web02** for hello second web server</span></span>
* <span data-ttu-id="a40fb-161">**azos-utilisation-vm-app01** hello premier serveur d’applications</span><span class="sxs-lookup"><span data-stu-id="a40fb-161">**azos-use-vm-app01** for hello first application server</span></span>
* <span data-ttu-id="a40fb-162">**azos-utilisation-vm-app02** hello deuxième serveur d’applications</span><span class="sxs-lookup"><span data-stu-id="a40fb-162">**azos-use-vm-app02** for hello second application server</span></span>
* <span data-ttu-id="a40fb-163">**azos-utilisation-vm-sql01** pour hello premier serveur SQL Server en cluster de hello</span><span class="sxs-lookup"><span data-stu-id="a40fb-163">**azos-use-vm-sql01** for hello first SQL Server server in hello cluster</span></span>
* <span data-ttu-id="a40fb-164">**azos-utilisation-vm-sql02** pour hello deuxième serveur SQL Server en cluster de hello</span><span class="sxs-lookup"><span data-stu-id="a40fb-164">**azos-use-vm-sql02** for hello second SQL Server server in hello cluster</span></span>
* <span data-ttu-id="a40fb-165">**azos-utilisation-vm-dc01** hello premier contrôleur de domaine</span><span class="sxs-lookup"><span data-stu-id="a40fb-165">**azos-use-vm-dc01** for hello first domain controller</span></span>
* <span data-ttu-id="a40fb-166">**azos-utilisation-vm-dc02** hello deuxième contrôleur de domaine</span><span class="sxs-lookup"><span data-stu-id="a40fb-166">**azos-use-vm-dc02** for hello second domain controller</span></span>

<span data-ttu-id="a40fb-167">Voici la configuration obtenue de hello.</span><span class="sxs-lookup"><span data-stu-id="a40fb-167">Here is hello resulting configuration.</span></span>

![Infrastructure d’applications finale déployée dans Azure](./media/infrastructure-example/example-config.png)

<span data-ttu-id="a40fb-169">Cette configuration comprend :</span><span class="sxs-lookup"><span data-stu-id="a40fb-169">This configuration incorporates:</span></span>

* <span data-ttu-id="a40fb-170">un réseau virtuel cloud avec deux sous-réseaux (FrontEnd et BackEnd) ;</span><span class="sxs-lookup"><span data-stu-id="a40fb-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="a40fb-171">des disques managés Azure avec des disques Standard et Premium ;</span><span class="sxs-lookup"><span data-stu-id="a40fb-171">Azure Managed Disks with both Standard and Premium disks</span></span>
* <span data-ttu-id="a40fb-172">Quatre groupes à haute disponibilité, une pour chaque niveau de la Boutique en ligne hello</span><span class="sxs-lookup"><span data-stu-id="a40fb-172">Four availability sets, one for each tier of hello on-line store</span></span>
* <span data-ttu-id="a40fb-173">machines virtuelles de Hello pour les couches de hello quatre</span><span class="sxs-lookup"><span data-stu-id="a40fb-173">hello virtual machines for hello four tiers</span></span>
* <span data-ttu-id="a40fb-174">Un jeu d’équilibrage de charge externe pour le trafic web basé sur HTTPS à partir de serveurs web de hello Internet toohello</span><span class="sxs-lookup"><span data-stu-id="a40fb-174">An external load balanced set for HTTPS-based web traffic from hello Internet toohello web servers</span></span>
* <span data-ttu-id="a40fb-175">Un jeu pour le trafic non chiffré web à partir de serveurs d’applications toohello hello web serveurs d’équilibrage interne</span><span class="sxs-lookup"><span data-stu-id="a40fb-175">An internal load balanced set for unencrypted web traffic from hello web servers toohello application servers</span></span>
* <span data-ttu-id="a40fb-176">un seul groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a40fb-176">A single resource group</span></span>