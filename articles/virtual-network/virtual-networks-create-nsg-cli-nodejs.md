---
title: "aaaCreate réseau des groupes de sécurité - Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment toocreate et déployer des groupes de sécurité réseau à l’aide de hello Azure CLI 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eeb7feedab959d92659e03c5c46d93fdfc08faea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="26149-103">Créer des groupes de sécurité à l’aide de hello Azure CLI 1.0 réseau</span><span class="sxs-lookup"><span data-stu-id="26149-103">Create network security groups using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="26149-104">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="26149-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="26149-105">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="26149-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="26149-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="26149-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="26149-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) -CLI de notre nouvelle génération pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="26149-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="26149-108">Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="26149-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="26149-109">Vous pouvez également [créer des groupes de sécurité réseau dans le modèle de déploiement classique hello](virtual-networks-create-nsg-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="26149-109">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="26149-110">commandes de CLI d’Azure Hello exemple ci-dessous s’attendre à un environnement simple déjà créé en fonction de scénario hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="26149-110">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> 

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="26149-111">Comment toocreate hello le groupe de sécurité réseau pour le sous-réseau frontal de hello</span><span class="sxs-lookup"><span data-stu-id="26149-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="26149-112">toocreate nommé d’un groupe de sécurité réseau nommé *NSG-FrontEnd* selon le scénario hello ci-dessus, suivez les étapes hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="26149-112">toocreate an NSG named named *NSG-FrontEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="26149-113">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="26149-113">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="26149-114">Exécutez hello **configuration azure mode** mode Manager tooResource commande tooswitch, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="26149-114">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="26149-115">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="26149-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="26149-116">Exécutez hello **réseau azure nsg créer** commande toocreate un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="26149-116">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="26149-117">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="26149-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
        data:    Name                            : NSG-FrontEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
   
    <span data-ttu-id="26149-118">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="26149-118">Parameters:</span></span>
   
   * <span data-ttu-id="26149-119">**-g (ou --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="26149-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="26149-120">Nom du groupe de ressources hello où hello NSG sera créé.</span><span class="sxs-lookup"><span data-stu-id="26149-120">Name of hello resource group where hello NSG will be created.</span></span> <span data-ttu-id="26149-121">Pour notre scénario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="26149-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="26149-122">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="26149-122">**-l (or --location)**.</span></span> <span data-ttu-id="26149-123">Région Azure où hello nouveau groupe de sécurité réseau doit être créé.</span><span class="sxs-lookup"><span data-stu-id="26149-123">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="26149-124">Pour notre scénario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="26149-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="26149-125">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="26149-125">**-n (or --name)**.</span></span> <span data-ttu-id="26149-126">Nom de hello nouveau groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="26149-126">Name for hello new NSG.</span></span> <span data-ttu-id="26149-127">Pour notre scénario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="26149-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="26149-128">Exécutez hello **créer de règle de groupe de sécurité réseau du réseau azure** commande toocreate une règle qui autorise l’accès tooport 3389 (RDP) à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="26149-128">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="26149-129">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="26149-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up hello network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp
        -rule
        data:    Name                            : rdp-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 3389
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="26149-130">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="26149-130">Parameters:</span></span>
   
   * <span data-ttu-id="26149-131">**-a (ou --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="26149-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="26149-132">Nom du NSG hello dans le hello règle sera créée.</span><span class="sxs-lookup"><span data-stu-id="26149-132">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="26149-133">Pour notre scénario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="26149-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="26149-134">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="26149-134">**-n (or --name)**.</span></span> <span data-ttu-id="26149-135">Nom de la nouvelle règle de hello.</span><span class="sxs-lookup"><span data-stu-id="26149-135">Name for hello new rule.</span></span> <span data-ttu-id="26149-136">Pour notre scénario, *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="26149-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="26149-137">**-c (ou --access)**.</span><span class="sxs-lookup"><span data-stu-id="26149-137">**-c (or --access)**.</span></span> <span data-ttu-id="26149-138">Niveau d’accès pour la règle hello (Deny ou autoriser).</span><span class="sxs-lookup"><span data-stu-id="26149-138">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="26149-139">**-p (ou --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="26149-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="26149-140">Protocole (Tcp, Udp ou *) pour la règle de hello.</span><span class="sxs-lookup"><span data-stu-id="26149-140">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="26149-141">**-r (ou --direction)**.</span><span class="sxs-lookup"><span data-stu-id="26149-141">**-r (or --direction)**.</span></span> <span data-ttu-id="26149-142">Direction de la connexion (Inbound ou Outbound).</span><span class="sxs-lookup"><span data-stu-id="26149-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="26149-143">**-y (ou --priority)**.</span><span class="sxs-lookup"><span data-stu-id="26149-143">**-y (or --priority)**.</span></span> <span data-ttu-id="26149-144">Priorité de la règle de hello.</span><span class="sxs-lookup"><span data-stu-id="26149-144">Priority for hello rule.</span></span>
   * <span data-ttu-id="26149-145">**-f (ou --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="26149-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="26149-146">Préfixe de l’adresse source dans CIDR ou à l’aide de balises par défaut.</span><span class="sxs-lookup"><span data-stu-id="26149-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="26149-147">**-o (ou --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="26149-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="26149-148">Port source ou plage de ports.</span><span class="sxs-lookup"><span data-stu-id="26149-148">Source port, or port range.</span></span>
   * <span data-ttu-id="26149-149">**-e (ou --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="26149-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="26149-150">Préfixe de l’adresse de destination dans CIDR ou à l’aide de balises par défaut.</span><span class="sxs-lookup"><span data-stu-id="26149-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="26149-151">**-u (ou --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="26149-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="26149-152">Port de destination ou plage de ports.</span><span class="sxs-lookup"><span data-stu-id="26149-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="26149-153">Exécutez hello **créer de règle de groupe de sécurité réseau du réseau azure** commande toocreate une règle qui autorise l’accès tooport 80 (HTTP) à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="26149-153">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="26149-154">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="26149-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 80
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="26149-155">Exécutez hello **ensemble de sous-réseau de réseau virtuel azure réseau** sous-réseau frontal de commande toolink hello NSG toohello.</span><span class="sxs-lookup"><span data-stu-id="26149-155">Run hello **azure network vnet subnet set** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="26149-156">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="26149-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="26149-157">Comment mettre fin sous-réseau à toocreate hello NSG pour hello précédent</span><span class="sxs-lookup"><span data-stu-id="26149-157">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="26149-158">toocreate nommé d’un groupe de sécurité réseau nommé *principal de groupe de sécurité réseau* selon le scénario hello ci-dessus, suivez les étapes hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="26149-158">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="26149-159">Exécutez hello **réseau azure nsg créer** commande toocreate un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="26149-159">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="26149-160">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="26149-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd
        data:    Name                            : NSG-BackEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
2. <span data-ttu-id="26149-161">Exécutez hello **créer de règle de groupe de sécurité réseau du réseau azure** commande toocreate une règle qui autorise l’accès tooport 1433 (SQL) à partir du sous-réseau frontal de hello.</span><span class="sxs-lookup"><span data-stu-id="26149-161">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="26149-162">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="26149-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule
        data:    Name                            : sql-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 1433
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="26149-163">Exécutez hello **créer de règle de groupe de sécurité réseau du réseau azure** commande toocreate une règle qui refuse l’accès toohello Internet à partir de.</span><span class="sxs-lookup"><span data-stu-id="26149-163">Run hello **azure network nsg rule create** command toocreate a rule that denies access toohello Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="26149-164">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="26149-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : *
        data:    Source Port                     : *
        data:    Destination IP                  : Internet
        data:    Destination Port                : *
        data:    Protocol                        : *
        data:    Direction                       : Outbound
        data:    Access                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="26149-165">Exécutez hello **ensemble de sous-réseau de réseau virtuel azure réseau** toolink hello NSG toohello nouveau sous-réseau de fin de commande.</span><span class="sxs-lookup"><span data-stu-id="26149-165">Run hello **azure network vnet subnet set** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="26149-166">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="26149-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up hello subnet "BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/BackEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : BackEnd
        data:    Address prefix                  : 192.168.2.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL1/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL2/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

