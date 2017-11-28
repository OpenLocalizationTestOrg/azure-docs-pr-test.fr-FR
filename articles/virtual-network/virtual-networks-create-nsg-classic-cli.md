---
title: "Guide pratique pour créer des groupes de sécurité réseau en mode classique à l’aide d’Azure CLI | Microsoft Docs"
description: "Découvrez comment créer et déployer des groupes de sécurité réseau en mode classique à l'aide de l’interface de ligne de commande Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 115a1937a4c88ba2b986a40c84b1b759ed5e03b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-nsgs-classic-in-the-azure-cli"></a><span data-ttu-id="99ecd-103">Création de NSG (classiques) dans l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="99ecd-103">How to create NSGs (classic) in the Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="99ecd-104">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="99ecd-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="99ecd-105">Vous pouvez également [créer un groupe de sécurité réseau dans le modèle de déploiement Resource Manager](virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="99ecd-105">You can also [create NSGs in the Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="99ecd-106">Les exemples de commandes d’interface de ligne de commande PowerShell ci-dessous supposent qu’un environnement simple a déjà été créé conformément au scénario décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="99ecd-106">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="99ecd-107">Si vous souhaitez exécuter les commandes telles qu’elles sont présentées dans ce document, commencez par créer l’environnement de test décrit dans [Création d’un réseau virtuel](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="99ecd-107">If you want to run the commands as they are displayed in this document, first build the test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="99ecd-108">Création du groupe de sécurité réseau pour le sous-réseau frontal</span><span class="sxs-lookup"><span data-stu-id="99ecd-108">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="99ecd-109">Pour créer un groupe de sécurité réseau nommé **NSG-FrontEnd** selon le scénario ci-dessus, suivez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="99ecd-109">To create an NSG named named **NSG-FrontEnd** based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="99ecd-110">Si vous n’avez jamais utilisé l’interface de ligne de commande Azure, consultez [Installer et configurer l’interface de ligne de commande Azure](../cli-install-nodejs.md) et suivez les instructions jusqu’à l’étape où vous sélectionnez votre compte et votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="99ecd-110">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="99ecd-111">Exécutez la commande **`azure config mode`** pour passer en mode classique, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="99ecd-111">Run the **`azure config mode`** command to switch to classic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="99ecd-112">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="99ecd-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="99ecd-113">Exécutez la commande **`azure network nsg create`** pour créer un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="99ecd-113">Run the **`azure network nsg create`** command to create an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="99ecd-114">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="99ecd-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="99ecd-115">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="99ecd-115">Parameters:</span></span>
   
   * <span data-ttu-id="99ecd-116">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="99ecd-116">**-l (or --location)**.</span></span> <span data-ttu-id="99ecd-117">Région Azure où le groupe de sécurité réseau sera créé.</span><span class="sxs-lookup"><span data-stu-id="99ecd-117">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="99ecd-118">Pour notre scénario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="99ecd-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="99ecd-119">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="99ecd-119">**-n (or --name)**.</span></span> <span data-ttu-id="99ecd-120">Nom du nouveau groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="99ecd-120">Name for the new NSG.</span></span> <span data-ttu-id="99ecd-121">Pour notre scénario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="99ecd-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="99ecd-122">Exécutez la commande **`azure network nsg rule create`** pour créer une règle qui autorise l'accès au port 3389 (RDP) à partir d'Internet.</span><span class="sxs-lookup"><span data-stu-id="99ecd-122">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="99ecd-123">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="99ecd-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="99ecd-124">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="99ecd-124">Parameters:</span></span>
   
   * <span data-ttu-id="99ecd-125">**-a (ou --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="99ecd-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="99ecd-126">Nom du groupe de sécurité réseau dans lequel la règle sera créée.</span><span class="sxs-lookup"><span data-stu-id="99ecd-126">Name of the NSG in which the rule will be created.</span></span> <span data-ttu-id="99ecd-127">Pour notre scénario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="99ecd-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="99ecd-128">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="99ecd-128">**-n (or --name)**.</span></span> <span data-ttu-id="99ecd-129">Nom de la nouvelle règle.</span><span class="sxs-lookup"><span data-stu-id="99ecd-129">Name for the new rule.</span></span> <span data-ttu-id="99ecd-130">Pour notre scénario, *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="99ecd-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="99ecd-131">**-c (ou--action)**.</span><span class="sxs-lookup"><span data-stu-id="99ecd-131">**-c (or --action)**.</span></span> <span data-ttu-id="99ecd-132">Niveau d’accès de la règle (Deny ou Allow).</span><span class="sxs-lookup"><span data-stu-id="99ecd-132">Access level for the rule (Deny or Allow).</span></span>
   * <span data-ttu-id="99ecd-133">**-p (ou --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="99ecd-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="99ecd-134">Protocole (TCP, UDP ou *) de la règle.</span><span class="sxs-lookup"><span data-stu-id="99ecd-134">Protocol (Tcp, Udp, or *) for the rule.</span></span>
   * <span data-ttu-id="99ecd-135">**-r (ou --type)**.</span><span class="sxs-lookup"><span data-stu-id="99ecd-135">**-r (or --type)**.</span></span> <span data-ttu-id="99ecd-136">Direction de la connexion (Inbound ou Outbound).</span><span class="sxs-lookup"><span data-stu-id="99ecd-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="99ecd-137">**-y (ou --priority)**.</span><span class="sxs-lookup"><span data-stu-id="99ecd-137">**-y (or --priority)**.</span></span> <span data-ttu-id="99ecd-138">Priorité de la règle.</span><span class="sxs-lookup"><span data-stu-id="99ecd-138">Priority for the rule.</span></span>
   * <span data-ttu-id="99ecd-139">**-f (ou --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="99ecd-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="99ecd-140">Préfixe de l’adresse source dans CIDR ou à l’aide de balises par défaut.</span><span class="sxs-lookup"><span data-stu-id="99ecd-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="99ecd-141">**-o (ou --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="99ecd-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="99ecd-142">Port source ou plage de ports.</span><span class="sxs-lookup"><span data-stu-id="99ecd-142">Source port, or port range.</span></span>
   * <span data-ttu-id="99ecd-143">**-e (ou --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="99ecd-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="99ecd-144">Préfixe de l’adresse de destination dans CIDR ou à l’aide de balises par défaut.</span><span class="sxs-lookup"><span data-stu-id="99ecd-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="99ecd-145">**-u (ou --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="99ecd-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="99ecd-146">Port de destination ou plage de ports.</span><span class="sxs-lookup"><span data-stu-id="99ecd-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="99ecd-147">Exécutez la commande **`azure network nsg rule create`** pour créer une règle qui autorise l'accès au port 80 (HTTP) à partir d'Internet.</span><span class="sxs-lookup"><span data-stu-id="99ecd-147">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="99ecd-148">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="99ecd-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="99ecd-149">Exécutez la commande **`azure network nsg subnet add`** pour lier le groupe de sécurité réseau au sous-réseau frontal.</span><span class="sxs-lookup"><span data-stu-id="99ecd-149">Run the **`azure network nsg subnet add`** command to link the NSG to the front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="99ecd-150">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="99ecd-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="99ecd-151">Création du groupe de sécurité réseau pour le sous-réseau principal</span><span class="sxs-lookup"><span data-stu-id="99ecd-151">How to create the NSG for the back end subnet</span></span>
<span data-ttu-id="99ecd-152">Pour créer un groupe de sécurité réseau nommé *NSG-BackEnd* selon le scénario ci-dessus, suivez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="99ecd-152">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="99ecd-153">Exécutez la commande **`azure network nsg create`** pour créer un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="99ecd-153">Run the **`azure network nsg create`** command to create an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="99ecd-154">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="99ecd-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="99ecd-155">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="99ecd-155">Parameters:</span></span>
   
   * <span data-ttu-id="99ecd-156">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="99ecd-156">**-l (or --location)**.</span></span> <span data-ttu-id="99ecd-157">Région Azure où le groupe de sécurité réseau sera créé.</span><span class="sxs-lookup"><span data-stu-id="99ecd-157">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="99ecd-158">Pour notre scénario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="99ecd-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="99ecd-159">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="99ecd-159">**-n (or --name)**.</span></span> <span data-ttu-id="99ecd-160">Nom du nouveau groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="99ecd-160">Name for the new NSG.</span></span> <span data-ttu-id="99ecd-161">Pour notre scénario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="99ecd-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="99ecd-162">Exécutez la commande **`azure network nsg rule create`** pour créer une règle qui autorise l'accès au port 1433 (SQL) à partir du sous-réseau frontal.</span><span class="sxs-lookup"><span data-stu-id="99ecd-162">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="99ecd-163">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="99ecd-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="99ecd-164">Exécutez la commande **`azure network nsg rule create`** pour créer une règle qui refuse l'accès à Internet.</span><span class="sxs-lookup"><span data-stu-id="99ecd-164">Run the **`azure network nsg rule create`** command to create a rule that denies access to the Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="99ecd-165">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="99ecd-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="99ecd-166">Exécutez la commande **`azure network nsg subnet add`** pour lier le groupe de sécurité réseau au sous-réseau back-end.</span><span class="sxs-lookup"><span data-stu-id="99ecd-166">Run the **`azure network nsg subnet add`** command to link the NSG to the back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="99ecd-167">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="99ecd-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up the network security group "NSG-BackEndX"
        info:    Looking up the subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

