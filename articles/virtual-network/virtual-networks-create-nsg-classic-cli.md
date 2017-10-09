---
title: "aaaHow toocreate groupes de sécurité réseau à l’aide du mode classique hello CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toocreate et déployer des groupes de sécurité réseau en mode classique, à l’aide de hello CLI d’Azure"
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
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a><span data-ttu-id="97a4c-103">Comment (classiques), de groupes de sécurité réseau toocreate hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="97a4c-103">How toocreate NSGs (classic) in hello Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="97a4c-104">Cet article décrit le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="97a4c-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="97a4c-105">Vous pouvez également [créer des groupes de sécurité réseau dans le modèle de déploiement du Gestionnaire de ressources hello](virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="97a4c-105">You can also [create NSGs in hello Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="97a4c-106">commandes de CLI d’Azure Hello exemple ci-dessous s’attendre à un environnement simple déjà créé en fonction de scénario hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="97a4c-106">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="97a4c-107">Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer d’environnement de test hello [créer un réseau virtuel](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="97a4c-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="97a4c-108">Comment toocreate hello le groupe de sécurité réseau pour le sous-réseau frontal de hello</span><span class="sxs-lookup"><span data-stu-id="97a4c-108">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="97a4c-109">toocreate nommé d’un groupe de sécurité réseau nommé **NSG-FrontEnd** selon le scénario hello ci-dessus, suivez les étapes hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="97a4c-109">toocreate an NSG named named **NSG-FrontEnd** based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="97a4c-110">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="97a4c-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="97a4c-111">Exécutez hello  **`azure config mode`**  mode commande tooswitch tooclassic, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="97a4c-111">Run hello **`azure config mode`** command tooswitch tooclassic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="97a4c-112">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="97a4c-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="97a4c-113">Exécutez hello  **`azure network nsg create`**  commande toocreate un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="97a4c-113">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="97a4c-114">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="97a4c-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="97a4c-115">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="97a4c-115">Parameters:</span></span>
   
   * <span data-ttu-id="97a4c-116">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="97a4c-116">**-l (or --location)**.</span></span> <span data-ttu-id="97a4c-117">Région Azure où hello nouveau groupe de sécurité réseau doit être créé.</span><span class="sxs-lookup"><span data-stu-id="97a4c-117">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="97a4c-118">Pour notre scénario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="97a4c-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="97a4c-119">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="97a4c-119">**-n (or --name)**.</span></span> <span data-ttu-id="97a4c-120">Nom de hello nouveau groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="97a4c-120">Name for hello new NSG.</span></span> <span data-ttu-id="97a4c-121">Pour notre scénario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="97a4c-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="97a4c-122">Exécutez hello  **`azure network nsg rule create`**  commande toocreate une règle qui autorise l’accès tooport 3389 (RDP) à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="97a4c-122">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="97a4c-123">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="97a4c-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="97a4c-124">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="97a4c-124">Parameters:</span></span>
   
   * <span data-ttu-id="97a4c-125">**-a (ou --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="97a4c-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="97a4c-126">Nom du NSG hello dans le hello règle sera créée.</span><span class="sxs-lookup"><span data-stu-id="97a4c-126">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="97a4c-127">Pour notre scénario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="97a4c-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="97a4c-128">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="97a4c-128">**-n (or --name)**.</span></span> <span data-ttu-id="97a4c-129">Nom de la nouvelle règle de hello.</span><span class="sxs-lookup"><span data-stu-id="97a4c-129">Name for hello new rule.</span></span> <span data-ttu-id="97a4c-130">Pour notre scénario, *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="97a4c-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="97a4c-131">**-c (ou--action)**.</span><span class="sxs-lookup"><span data-stu-id="97a4c-131">**-c (or --action)**.</span></span> <span data-ttu-id="97a4c-132">Niveau d’accès pour la règle hello (Deny ou autoriser).</span><span class="sxs-lookup"><span data-stu-id="97a4c-132">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="97a4c-133">**-p (ou --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="97a4c-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="97a4c-134">Protocole (Tcp, Udp ou *) pour la règle de hello.</span><span class="sxs-lookup"><span data-stu-id="97a4c-134">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="97a4c-135">**-r (ou --type)**.</span><span class="sxs-lookup"><span data-stu-id="97a4c-135">**-r (or --type)**.</span></span> <span data-ttu-id="97a4c-136">Direction de la connexion (Inbound ou Outbound).</span><span class="sxs-lookup"><span data-stu-id="97a4c-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="97a4c-137">**-y (ou --priority)**.</span><span class="sxs-lookup"><span data-stu-id="97a4c-137">**-y (or --priority)**.</span></span> <span data-ttu-id="97a4c-138">Priorité de la règle de hello.</span><span class="sxs-lookup"><span data-stu-id="97a4c-138">Priority for hello rule.</span></span>
   * <span data-ttu-id="97a4c-139">**-f (ou --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="97a4c-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="97a4c-140">Préfixe de l’adresse source dans CIDR ou à l’aide de balises par défaut.</span><span class="sxs-lookup"><span data-stu-id="97a4c-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="97a4c-141">**-o (ou --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="97a4c-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="97a4c-142">Port source ou plage de ports.</span><span class="sxs-lookup"><span data-stu-id="97a4c-142">Source port, or port range.</span></span>
   * <span data-ttu-id="97a4c-143">**-e (ou --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="97a4c-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="97a4c-144">Préfixe de l’adresse de destination dans CIDR ou à l’aide de balises par défaut.</span><span class="sxs-lookup"><span data-stu-id="97a4c-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="97a4c-145">**-u (ou --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="97a4c-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="97a4c-146">Port de destination ou plage de ports.</span><span class="sxs-lookup"><span data-stu-id="97a4c-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="97a4c-147">Exécutez hello  **`azure network nsg rule create`**  commande toocreate une règle qui autorise l’accès tooport 80 (HTTP) à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="97a4c-147">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="97a4c-148">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="97a4c-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
6. <span data-ttu-id="97a4c-149">Exécutez hello  **`azure network nsg subnet add`**  sous-réseau frontal de commande toolink hello NSG toohello.</span><span class="sxs-lookup"><span data-stu-id="97a4c-149">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="97a4c-150">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="97a4c-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="97a4c-151">Comment mettre fin sous-réseau à toocreate hello NSG pour hello précédent</span><span class="sxs-lookup"><span data-stu-id="97a4c-151">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="97a4c-152">toocreate nommé d’un groupe de sécurité réseau nommé *principal de groupe de sécurité réseau* selon le scénario hello ci-dessus, suivez les étapes hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="97a4c-152">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="97a4c-153">Exécutez hello  **`azure network nsg create`**  commande toocreate un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="97a4c-153">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="97a4c-154">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="97a4c-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
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
   
    <span data-ttu-id="97a4c-155">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="97a4c-155">Parameters:</span></span>
   
   * <span data-ttu-id="97a4c-156">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="97a4c-156">**-l (or --location)**.</span></span> <span data-ttu-id="97a4c-157">Région Azure où hello nouveau groupe de sécurité réseau doit être créé.</span><span class="sxs-lookup"><span data-stu-id="97a4c-157">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="97a4c-158">Pour notre scénario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="97a4c-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="97a4c-159">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="97a4c-159">**-n (or --name)**.</span></span> <span data-ttu-id="97a4c-160">Nom de hello nouveau groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="97a4c-160">Name for hello new NSG.</span></span> <span data-ttu-id="97a4c-161">Pour notre scénario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="97a4c-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="97a4c-162">Exécutez hello  **`azure network nsg rule create`**  commande toocreate une règle qui autorise l’accès tooport 1433 (SQL) à partir du sous-réseau frontal de hello.</span><span class="sxs-lookup"><span data-stu-id="97a4c-162">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="97a4c-163">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="97a4c-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
3. <span data-ttu-id="97a4c-164">Exécutez hello  **`azure network nsg rule create`**  commande toocreate une règle qui refuse l’accès toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="97a4c-164">Run hello **`azure network nsg rule create`** command toocreate a rule that denies access toohello Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="97a4c-165">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="97a4c-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
4. <span data-ttu-id="97a4c-166">Exécutez hello  **`azure network nsg subnet add`**  toolink hello NSG toohello nouveau sous-réseau de fin de commande.</span><span class="sxs-lookup"><span data-stu-id="97a4c-166">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="97a4c-167">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="97a4c-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

