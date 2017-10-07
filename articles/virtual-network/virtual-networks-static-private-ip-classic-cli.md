---
title: "les adresses IP privées aaaConfigure pour les machines virtuelles (classiques) - Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment les adresses IP privées tooconfigure pour les machines virtuelles (classiques) à l’aide de hello Azure interface de ligne de commande (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a><span data-ttu-id="5a108-103">Configurer des adresses IP privées pour une machine virtuelle (classique) à l’aide de hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5a108-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="5a108-104">Cet article décrit le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="5a108-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="5a108-105">Vous pouvez également [gérer une adresse IP privée statique dans le modèle de déploiement du Gestionnaire de ressources hello](virtual-networks-static-private-ip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5a108-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span></span>

<span data-ttu-id="5a108-106">commandes CLI d’Azure d’exemple Hello ci-dessous s’attendre à un environnement simple déjà créé.</span><span class="sxs-lookup"><span data-stu-id="5a108-106">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="5a108-107">Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer d’environnement de test hello décrit dans [créer un réseau virtuel](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5a108-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="5a108-108">Comment toospecify une adresse IP privée statique d’adresses lorsque vous créez une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5a108-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="5a108-109">toocreate un nouvel ordinateur virtuel nommé *DNS01* dans un nouveau service cloud nommé *TestService* selon le scénario hello ci-dessus, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5a108-109">toocreate a new VM named *DNS01* in a new cloud service named *TestService* based on hello scenario above, follow these steps:</span></span>

1. <span data-ttu-id="5a108-110">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="5a108-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="5a108-111">Exécutez hello **de création du service azure** commande du service de cloud toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="5a108-111">Run hello **azure service create** command toocreate hello cloud service.</span></span>
   
        azure service create TestService --location uscentral
   
    <span data-ttu-id="5a108-112">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="5a108-112">Expected output:</span></span>
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. <span data-ttu-id="5a108-113">Exécutez hello **créer une machine virtuelle azure** commande toocreate hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5a108-113">Run hello **azure create vm** command toocreate hello VM.</span></span> <span data-ttu-id="5a108-114">Notez la valeur hello pour une adresse IP privée statique.</span><span class="sxs-lookup"><span data-stu-id="5a108-114">Notice hello value for a static private IP address.</span></span> <span data-ttu-id="5a108-115">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="5a108-115">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    <span data-ttu-id="5a108-116">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="5a108-116">Expected output:</span></span>
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * <span data-ttu-id="5a108-117">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="5a108-117">**-l (or --location)**.</span></span> <span data-ttu-id="5a108-118">Région Azure où hello machine virtuelle doit être créé.</span><span class="sxs-lookup"><span data-stu-id="5a108-118">Azure region where hello VM will be created.</span></span> <span data-ttu-id="5a108-119">Pour notre scénario, *centralus*.</span><span class="sxs-lookup"><span data-stu-id="5a108-119">For our scenario, *centralus*.</span></span>
   * <span data-ttu-id="5a108-120">**-n (ou--vm-name)**.</span><span class="sxs-lookup"><span data-stu-id="5a108-120">**-n (or --vm-name)**.</span></span> <span data-ttu-id="5a108-121">Nom de hello toobe de machine virtuelle créée.</span><span class="sxs-lookup"><span data-stu-id="5a108-121">Name of hello VM toobe created.</span></span>
   * <span data-ttu-id="5a108-122">**-w (ou --virtual-network-name)**.</span><span class="sxs-lookup"><span data-stu-id="5a108-122">**-w (or --virtual-network-name)**.</span></span> <span data-ttu-id="5a108-123">Nom de hello réseau virtuel où hello machine virtuelle doit être créé.</span><span class="sxs-lookup"><span data-stu-id="5a108-123">Name of hello VNet where hello VM will be created.</span></span> 
   * <span data-ttu-id="5a108-124">**-S (ou --static-ip)**.</span><span class="sxs-lookup"><span data-stu-id="5a108-124">**-S (or --static-ip)**.</span></span> <span data-ttu-id="5a108-125">Valeur adresse IP privée statique pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5a108-125">Static private IP address for hello VM.</span></span>
   * <span data-ttu-id="5a108-126">**TestService**.</span><span class="sxs-lookup"><span data-stu-id="5a108-126">**TestService**.</span></span> <span data-ttu-id="5a108-127">Nom du service de cloud hello où hello machine virtuelle doit être créé.</span><span class="sxs-lookup"><span data-stu-id="5a108-127">Name of hello cloud service where hello VM will be created.</span></span>
   * <span data-ttu-id="5a108-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span><span class="sxs-lookup"><span data-stu-id="5a108-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span></span> <span data-ttu-id="5a108-129">Image utilisée toocreate hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5a108-129">Image used toocreate hello VM.</span></span>
   * <span data-ttu-id="5a108-130">**adminuser**.</span><span class="sxs-lookup"><span data-stu-id="5a108-130">**adminuser**.</span></span> <span data-ttu-id="5a108-131">Administrateur local pour hello machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="5a108-131">Local administrator for hello Windows VM.</span></span>
   * <span data-ttu-id="5a108-132">**AdminP@ssw0rd**.</span><span class="sxs-lookup"><span data-stu-id="5a108-132">**AdminP@ssw0rd**.</span></span> <span data-ttu-id="5a108-133">Mot de passe administrateur local pour hello machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="5a108-133">Local administrator password for hello Windows VM.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="5a108-134">Comment informations pour une machine virtuelle d’adresse IP privée statique de tooretrieve</span><span class="sxs-lookup"><span data-stu-id="5a108-134">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="5a108-135">adresse IP privée statique de tooview hello adresse hello pour les ordinateurs virtuels créés avec script hello ci-dessus, exécutez hello suivant commande CLI d’Azure et observez la valeur hello pour *réseau StaticIP*:</span><span class="sxs-lookup"><span data-stu-id="5a108-135">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello value for *Network StaticIP*:</span></span>

    azure vm static-ip show DNS01

<span data-ttu-id="5a108-136">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="5a108-136">Expected output:</span></span>

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="5a108-137">Comment tooremove une privée d’adresses IP statiques à partir d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5a108-137">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="5a108-138">tooremove hello adresse IP privée statique ajouté toohello machine virtuelle dans le script hello ci-dessus, hello exécution suivant la commande CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="5a108-138">tooremove hello static private IP address added toohello VM in hello script above, run hello following Azure CLI command:</span></span>

    azure vm static-ip remove DNS01

<span data-ttu-id="5a108-139">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="5a108-139">Expected output:</span></span>

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a><span data-ttu-id="5a108-140">Comment tooadd un tooan d’IP privée statique machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="5a108-140">How tooadd a static private IP tooan existing VM</span></span>
<span data-ttu-id="5a108-141">tooadd un toohello d’adresse IP privée statique machine virtuelle créée à l’aide de script hello ci-dessus, exécutez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5a108-141">tooadd a static private IP address toohello VM created using hello script above, runt he following command:</span></span>

    azure vm static-ip set DNS01 192.168.1.101

<span data-ttu-id="5a108-142">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="5a108-142">Expected output:</span></span>

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a><span data-ttu-id="5a108-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5a108-143">Next steps</span></span>
* <span data-ttu-id="5a108-144">En savoir plus sur les [adresses IP publiques réservées](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="5a108-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="5a108-145">En savoir plus sur les [adresses IP publiques de niveau d’instance](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="5a108-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="5a108-146">Consultez hello [API REST de IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a108-146">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

