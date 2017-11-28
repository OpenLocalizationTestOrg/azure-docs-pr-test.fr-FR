---
title: "Configurer des adresses IP privées pour des machines virtuelles (Classic) - Portail Azure | Microsoft Docs"
description: "Découvrez comment configurer des adresses IP privées pour des machines virtuelles (Classic) à l’aide du portail Azure."
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
ms.openlocfilehash: bde6de3495c2909b63b1f85e420a4ff5e7ac2c1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-the-azure-portal"></a><span data-ttu-id="91912-103">Configurer des adresses IP privées pour une machine virtuelle (Classic) à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="91912-103">Configure private IP addresses for a virtual machine (Classic) using the Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="91912-104">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="91912-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="91912-105">Vous pouvez également [gérer une adresse IP privée statique dans le modèle de déploiement Resource Manager](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="91912-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="91912-106">Les étapes de l’exemple ci-dessous supposent qu’un environnement simple a déjà été créé.</span><span class="sxs-lookup"><span data-stu-id="91912-106">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="91912-107">Si vous souhaitez exécuter les étapes telles qu’elles sont présentées dans ce document, commencez par créer l’environnement de test décrit dans [Créer un réseau virtuel](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="91912-107">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="91912-108">Comment spécifier une adresse IP privée statique lors de la création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="91912-108">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="91912-109">Pour créer une machine virtuelle nommée *DNS01* dans le sous-réseau *FrontEnd* d’un réseau virtuel nommé *TestVNet* avec l’adresse IP privée statique *192.168.1.101*, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="91912-109">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="91912-110">Dans un navigateur, accédez à http://portal.azure.com et, si nécessaire, connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="91912-110">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="91912-111">Cliquez sur **Nouveau** > **Compute** > **Windows Server 2012 R2 Datacenter** (notez que la liste **Sélectionner un modèle de déploiement** contient déjà **Classique**), puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="91912-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="91912-113">Dans le panneau **Créer une machine virtuelle** , entrez le nom de la machine virtuelle à créer (*DNS01* dans notre scénario), le compte d’administrateur local et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="91912-113">In the **Create VM** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="91912-115">Cliquez sur **Configuration facultative** > **Réseau** > **Réseau virtuel**, puis sur **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="91912-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="91912-116">Si l’option **TestVNet** n’est pas disponible, assurez-vous que vous utilisez l’emplacement *Centre des États-Unis* et avez créé l’environnement de test décrit au début de cet article.</span><span class="sxs-lookup"><span data-stu-id="91912-116">If **TestVNet** is not available, make sure you are using the *Central US* location and have created the test environment described at the beginning of this article.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="91912-118">Dans le panneau **Réseau**, vérifiez que le sous-réseau actuellement sélectionné est *FrontEnd*, puis cliquez sur **Adresses IP**. Sous **Affectation d’adresses IP**, cliquez sur **Statique**, puis entrez *192.168.1.101* pour **Adresse IP**, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="91912-118">In the **Network** blade, make sure the subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="91912-120">Cliquez successivement sur **OK** dans le panneau **Adresses IP**, sur **OK** dans le panneau **Réseau**, puis sur **OK** dans le panneau **Configuration facultative**.</span><span class="sxs-lookup"><span data-stu-id="91912-120">Click **OK** in the **IP addresses** blade, then click **OK** in the **Network** blade, and click **OK** in the **Optional config** blade.</span></span>
7. <span data-ttu-id="91912-121">Dans le panneau **Créer une machine virtuelle**, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="91912-121">In the **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="91912-122">Notez la vignette ci-dessous affichée dans votre tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="91912-122">Notice the tile below displayed in your dashboard.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="91912-124">Récupération d’informations d’adresse IP privée statique pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="91912-124">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="91912-125">Pour afficher les informations d’adresse IP privée statique de la machine virtuelle créée lors des étapes ci-dessus, exécutez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="91912-125">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="91912-126">Dans le portail Azure, cliquez sur **Parcourir tout** > **Machines virtuelles (Classic)** > **DNS01** > **Tous les paramètres** > **Adresses IP**, puis examinez l’affectation d’adresses IP et l’adresse IP, telles qu’illustrées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="91912-126">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice the IP address assignment and IP address as seen below.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="91912-128">Suppression d’une adresse IP privée statique d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="91912-128">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="91912-129">Pour supprimer l’adresse IP privée statique de la machine virtuelle créée ci-dessus, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="91912-129">To remove the static private IP address from the VM created above, follow the steps below.</span></span>

1. <span data-ttu-id="91912-130">Dans le panneau **Adresses IP** illustré ci-dessus, cliquez sur **Dynamique** à droite de **Affectation d’adresses IP**, puis cliquez sur **Enregistrer** et sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="91912-130">From the **IP addresses** blade shown above, click **Dynamic** to the right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="91912-132">Ajout d’une adresse IP privée statique à une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="91912-132">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="91912-133">Pour ajouter une adresse IP privée statique à la machine virtuelle créée lors des étapes ci-dessus, exécutez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="91912-133">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="91912-134">Dans le panneau **Adresses IP** illustré ci-dessus, à droite de **Affectations d’adresses IP**, cliquez sur **Statique**.</span><span class="sxs-lookup"><span data-stu-id="91912-134">From the **IP addresses** blade shown above, click **Static** to the right of **IP address assignment**.</span></span>
2. <span data-ttu-id="91912-135">Tapez *192.168.1.101* pour **Adresse IP**, puis cliquez sur **Enregistrer** et sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="91912-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91912-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="91912-136">Next steps</span></span>
* <span data-ttu-id="91912-137">En savoir plus sur les [adresses IP publiques réservées](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="91912-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="91912-138">En savoir plus sur les [adresses IP publiques de niveau d’instance](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="91912-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="91912-139">Consulter les [API REST d’adresse IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="91912-139">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

