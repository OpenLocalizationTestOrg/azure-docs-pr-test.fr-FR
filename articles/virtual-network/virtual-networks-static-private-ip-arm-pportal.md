---
title: "Configurer des adresses IP privées pour des machines virtuelles - Portail Azure | Microsoft Docs"
description: "Découvrez comment configurer des adresses IP privées pour des machines virtuelles à l’aide du portail Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 672462fad715758e50680fa5bade4b1f9d50e6e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="36b2d-103">Configurer des adresses IP privées pour une machine virtuelle à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="36b2d-103">Configure private IP addresses for a virtual machine using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="36b2d-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="36b2d-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="36b2d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="36b2d-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="36b2d-106">interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="36b2d-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="36b2d-107">Portail Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="36b2d-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="36b2d-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="36b2d-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="36b2d-109">Interface de ligne de commande Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="36b2d-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="36b2d-110">Cet article traite du modèle de déploiement de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="36b2d-110">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="36b2d-111">Vous pouvez également [gérer une adresse IP privée statique dans le modèle de déploiement classique](virtual-networks-static-private-ip-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="36b2d-111">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="36b2d-112">Les étapes de l’exemple ci-dessous supposent qu’un environnement simple a déjà été créé.</span><span class="sxs-lookup"><span data-stu-id="36b2d-112">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="36b2d-113">Si vous souhaitez exécuter les étapes telles qu’elles sont présentées dans ce document, commencez par créer l’environnement de test décrit dans [Créer un réseau virtuel](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="36b2d-113">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-to-create-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="36b2d-114">Création d’une machine virtuelle pour tester des adresses IP privées statiques</span><span class="sxs-lookup"><span data-stu-id="36b2d-114">How to create a VM for testing static private IP addresses</span></span>
<span data-ttu-id="36b2d-115">Vous ne pouvez pas définir une adresse IP privée statique lors de la création d'une machine virtuelle dans le mode de déploiement Resource Manager à l'aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="36b2d-115">You cannot set a static private IP address during the creation of a VM in the Resource Manager deployment mode by using the Azure portal.</span></span> <span data-ttu-id="36b2d-116">Vous devez d’abord créer la machine virtuelle, puis définir son adresse IP privée de façon à ce qu’elle soit statique.</span><span class="sxs-lookup"><span data-stu-id="36b2d-116">You must create the VM first, tehn set its private IP to be static.</span></span>

<span data-ttu-id="36b2d-117">Pour créer une machine virtuelle nommée *DNS01* dans le sous-réseau *FrontEnd* d’un réseau virtuel nommé *TestVNet*, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="36b2d-117">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet*, follow the steps below.</span></span>

1. <span data-ttu-id="36b2d-118">Dans un navigateur, accédez à http://portal.azure.com et, si nécessaire, connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="36b2d-118">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="36b2d-119">Cliquez sur **Nouveau** > **Compute** > **Windows Server 2012 R2 Datacenter** (notez que la liste **Sélectionner un modèle de déploiement** contient déjà **Resource Manager**), puis cliquez sur **Créer**, comme le montre la figure ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="36b2d-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in the figure below.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="36b2d-121">Dans le panneau **Informations de base** , entrez le nom de la machine virtuelle à créer (*DNS01* dans notre scénario), le compte d’administrateur local et un mot de passe, comme illustré dans la figure ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="36b2d-121">In the **Basics** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password, as seen in the figure below.</span></span>
   
    ![Panneau Informations de base](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="36b2d-123">Vérifiez que l’**emplacement** sélectionné est *Centre des États-Unis*. Ensuite, sous **Groupe de ressources**, cliquez sur **Sélectionner un groupe existant**, cliquez de nouveau sur **Groupe de ressources**, sur *TestRG* et enfin sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="36b2d-123">Make sure the **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![Panneau Informations de base](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="36b2d-125">Dans le panneau **Choisir une taille**, sélectionnez **A1 Standard**, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="36b2d-125">In the **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![Panneau Choisir une taille](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="36b2d-127">Dans le panneau **Paramètres**, vérifiez que les propriétés suivantes sont définies avec les valeurs ci-dessous, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="36b2d-127">In teh **Settings** blade, make sure the following properties are set are set with the values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="36b2d-128">-**Compte de stockage**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="36b2d-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="36b2d-129">**Réseau**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="36b2d-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="36b2d-130">**Sous-réseau**: *FrontEnd*</span><span class="sxs-lookup"><span data-stu-id="36b2d-130">**Subnet**: *FrontEnd*</span></span>
     
     ![Panneau Choisir une taille](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="36b2d-132">Dans le panneau **Résumé**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="36b2d-132">In the **Summary** blade, click **OK**.</span></span> <span data-ttu-id="36b2d-133">Notez la vignette ci-dessous affichée dans votre tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="36b2d-133">Notice the tile below displayed in your dashboard.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="36b2d-135">Récupération d’informations d’adresse IP privée statique pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="36b2d-135">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="36b2d-136">Pour afficher les informations d’adresse IP privée statique de la machine virtuelle créée lors des étapes ci-dessus, exécutez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="36b2d-136">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="36b2d-137">Dans le portail Azure, cliquez sur **Parcourir tout** > **Machines virtuelles** > **DNS01** > **Tous les paramètres** > **Interfaces réseau**, puis cliquez sur la seule interface réseau répertoriée.</span><span class="sxs-lookup"><span data-stu-id="36b2d-137">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on the only network interface listed.</span></span>
   
    ![Déploiement d’une vignette de machine virtuelle](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="36b2d-139">Dans le panneau **Interface réseau**, cliquez sur **Tous les paramètres** > **Adresses IP**, puis notez les valeurs des paramètres **Affectation** et **Adresse IP**.</span><span class="sxs-lookup"><span data-stu-id="36b2d-139">In the **Network interface** blade, click **All settings** > **IP addresses** and notice the **Assignment** and **IP address** values.</span></span>
   
    ![Déploiement d’une vignette de machine virtuelle](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="36b2d-141">Ajout d’une adresse IP privée statique à une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="36b2d-141">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="36b2d-142">Pour ajouter une adresse IP privée statique à la machine virtuelle créée lors des étapes ci-dessus, exécutez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="36b2d-142">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="36b2d-143">Dans le panneau **Adresses IP** illustré ci-dessus, sous **Affectation**, cliquez sur **Statique**.</span><span class="sxs-lookup"><span data-stu-id="36b2d-143">From the **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="36b2d-144">Tapez *192.168.1.101* dans **Adresse IP**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="36b2d-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="36b2d-146">Si, après avoir cliqué sur **Enregistrer**, vous remarquez que l’affectation est toujours définie sur **Dynamique**, cela signifie que l’adresse IP que vous avez tapée est déjà utilisée.</span><span class="sxs-lookup"><span data-stu-id="36b2d-146">If after clicking **Save** you notice that the assignment is still set to **Dynamic**, it means that the IP address you typed is already in use.</span></span> <span data-ttu-id="36b2d-147">Essayez une autre adresse IP.</span><span class="sxs-lookup"><span data-stu-id="36b2d-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="36b2d-148">Comment supprimer une adresse IP privée statique d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="36b2d-148">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="36b2d-149">Pour supprimer l’adresse IP privée statique de la machine virtuelle créée ci-dessus, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="36b2d-149">To remove the static private IP address from the VM created above, complete the following step:</span></span>

<span data-ttu-id="36b2d-150">Dans le panneau **Adresses IP** illustré ci-dessus, sous **Affectation**, cliquez sur **Dynamique**, puis sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="36b2d-150">From the **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36b2d-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36b2d-151">Next steps</span></span>
* <span data-ttu-id="36b2d-152">En savoir plus sur les [adresses IP publiques réservées](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="36b2d-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="36b2d-153">En savoir plus sur les [adresses IP publiques de niveau d’instance](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="36b2d-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="36b2d-154">Consulter les [API REST d’adresse IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="36b2d-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

