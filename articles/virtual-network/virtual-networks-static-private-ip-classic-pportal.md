---
title: "les adresses IP privées aaaConfigure pour les machines virtuelles (classiques) - portail Azure | Documents Microsoft"
description: "Découvrez comment les adresses IP privées tooconfigure pour les machines virtuelles (classiques) à l’aide de hello portail Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a><span data-ttu-id="1d0a9-103">Configurer des adresses IP privées pour une machine virtuelle (classique) à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="1d0a9-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="1d0a9-104">Cet article décrit le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="1d0a9-105">Vous pouvez également [gérer une adresse IP privée statique dans le modèle de déploiement du Gestionnaire de ressources hello](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="1d0a9-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="1d0a9-106">étapes d’exemple Hello ci-dessous s’attendre à un environnement simple déjà créé.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-106">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="1d0a9-107">Si vous souhaitez que les étapes de hello toorun car elles sont affichées dans ce document, tout d’abord créer d’environnement de test hello décrit dans [créer un réseau virtuel](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="1d0a9-107">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="1d0a9-108">Comment toospecify une adresse IP privée statique d’adresses lorsque vous créez une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1d0a9-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="1d0a9-109">toocreate un ordinateur virtuel nommé *DNS01* Bonjour *frontal* sous-réseau d’un réseau virtuel nommé *TestVNet* avec une adresse IP privée statique de *192.168.1.101*, Suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1d0a9-109">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="1d0a9-110">À partir d’un navigateur, accédez à toohttp://portal.azure.com et, si nécessaire, connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-110">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="1d0a9-111">Cliquez sur **nouveau** > **de calcul** > **Windows Server 2012 R2 Datacenter**, notez que hello **sélectionner un modèle de déploiement** liste déjà indique **classique**, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="1d0a9-113">Bonjour **créer un ordinateur virtuel** panneau, entrez le nom hello de hello toobe de machine virtuelle créée (*DNS01* dans notre scénario), hello compte d’administrateur local et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-113">In hello **Create VM** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="1d0a9-115">Cliquez sur **Configuration facultative** > **Réseau** > **Réseau virtuel**, puis sur **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="1d0a9-116">Si **TestVNet** n’est pas disponible, assurez-vous que vous utilisez hello *du centre des États-Unis* emplacement et vous avez créé l’environnement de test de hello décrit au début de hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-116">If **TestVNet** is not available, make sure you are using hello *Central US* location and have created hello test environment described at hello beginning of this article.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="1d0a9-118">Bonjour **réseau** panneau, vérifiez le sous-réseau hello qu’actuellement sélectionné est *frontal*, puis cliquez sur **des adresses IP**, sous **l’attributiond’adressesIP** cliquez sur **statique**, puis entrez *192.168.1.101* pour **adresse IP** comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-118">In hello **Network** blade, make sure hello subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="1d0a9-120">Cliquez sur **OK** Bonjour **des adresses IP** panneau, puis cliquez sur **OK** Bonjour **réseau** panneau, puis cliquez sur **OK**Bonjour **configuration facultative** panneau.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-120">Click **OK** in hello **IP addresses** blade, then click **OK** in hello **Network** blade, and click **OK** in hello **Optional config** blade.</span></span>
7. <span data-ttu-id="1d0a9-121">Bonjour **créer un ordinateur virtuel** panneau, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-121">In hello **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="1d0a9-122">Avis hello vignette ci-dessous affichée dans votre tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-122">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="1d0a9-124">Comment informations pour une machine virtuelle d’adresse IP privée statique de tooretrieve</span><span class="sxs-lookup"><span data-stu-id="1d0a9-124">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="1d0a9-125">tooview hello statique privées informations d’adresse IP pour hello machine virtuelle créée avec les étapes de hello ci-dessus, exécutez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-125">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="1d0a9-126">À partir du portail d’Azure Azure hello, cliquez sur **parcourir tous les** > **machines virtuelles (classiques)** > **DNS01**  >   **Tous les paramètres** > **des adresses IP** et notez hello attribution d’adresses IP et l’adresse IP, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-126">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice hello IP address assignment and IP address as seen below.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="1d0a9-128">Comment tooremove une privée d’adresses IP statiques à partir d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1d0a9-128">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="1d0a9-129">tooremove hello adresse IP privée statique à partir de hello machine virtuelle créée ci-dessus, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-129">tooremove hello static private IP address from hello VM created above, follow hello steps below.</span></span>

1. <span data-ttu-id="1d0a9-130">À partir de hello **des adresses IP** panneau illustrée ci-dessus, cliquez sur **dynamique** toohello à droite de **attribution d’adresses IP**, puis cliquez sur **enregistrer**, puis Cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-130">From hello **IP addresses** blade shown above, click **Dynamic** toohello right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="1d0a9-132">Comment tooadd une adresse IP privée statique d’adresses tooan existant de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1d0a9-132">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="1d0a9-133">tooadd un toohello d’adresse IP privée statique machine virtuelle créée à l’aide des étapes de hello ci-dessus, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1d0a9-133">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="1d0a9-134">À partir de hello **des adresses IP** panneau illustrée ci-dessus, cliquez sur **statique** toohello à droite de **l’attribution d’adresses IP**.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-134">From hello **IP addresses** blade shown above, click **Static** toohello right of **IP address assignment**.</span></span>
2. <span data-ttu-id="1d0a9-135">Tapez *192.168.1.101* pour **Adresse IP**, puis cliquez sur **Enregistrer** et sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="1d0a9-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d0a9-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1d0a9-136">Next steps</span></span>
* <span data-ttu-id="1d0a9-137">En savoir plus sur les [adresses IP publiques réservées](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="1d0a9-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="1d0a9-138">En savoir plus sur les [adresses IP publiques de niveau d’instance](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="1d0a9-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="1d0a9-139">Consultez hello [API REST de IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d0a9-139">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

