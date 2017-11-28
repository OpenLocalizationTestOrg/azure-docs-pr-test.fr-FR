---
title: "les adresses IP privées aaaConfigure pour les machines virtuelles - portail Azure | Documents Microsoft"
description: "Découvrez comment les adresses IP privées tooconfigure pour les ordinateurs virtuels à l’aide de hello portail Azure."
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
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="7bae7-103">Configurer des adresses IP privées pour un ordinateur virtuel à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="7bae7-103">Configure private IP addresses for a virtual machine using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7bae7-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="7bae7-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="7bae7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7bae7-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="7bae7-106">interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="7bae7-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="7bae7-107">Portail Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="7bae7-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="7bae7-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="7bae7-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="7bae7-109">Interface de ligne de commande Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="7bae7-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="7bae7-110">Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="7bae7-110">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="7bae7-111">Vous pouvez également [gérer une adresse IP privée statique dans le modèle de déploiement classique hello](virtual-networks-static-private-ip-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="7bae7-111">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="7bae7-112">étapes d’exemple Hello ci-dessous s’attendre à un environnement simple déjà créé.</span><span class="sxs-lookup"><span data-stu-id="7bae7-112">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="7bae7-113">Si vous souhaitez que les étapes de hello toorun car elles sont affichées dans ce document, tout d’abord créer d’environnement de test hello décrit dans [créer un réseau virtuel](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="7bae7-113">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="7bae7-114">Comment les adresses toocreate une machine virtuelle pour tester l’adresse IP privée statique</span><span class="sxs-lookup"><span data-stu-id="7bae7-114">How toocreate a VM for testing static private IP addresses</span></span>
<span data-ttu-id="7bae7-115">Impossible de définir une adresse IP privée statique lors de la création de hello d’une machine virtuelle en mode de déploiement du Gestionnaire de ressources hello à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7bae7-115">You cannot set a static private IP address during hello creation of a VM in hello Resource Manager deployment mode by using hello Azure portal.</span></span> <span data-ttu-id="7bae7-116">Vous devez d’abord créer hello VM, quantité définie son toobe IP privée statique.</span><span class="sxs-lookup"><span data-stu-id="7bae7-116">You must create hello VM first, tehn set its private IP toobe static.</span></span>

<span data-ttu-id="7bae7-117">toocreate un ordinateur virtuel nommé *DNS01* Bonjour *frontal* sous-réseau d’un réseau virtuel nommé *TestVNet*, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7bae7-117">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet*, follow hello steps below.</span></span>

1. <span data-ttu-id="7bae7-118">À partir d’un navigateur, accédez à toohttp://portal.azure.com et, si nécessaire, connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="7bae7-118">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="7bae7-119">Cliquez sur **nouveau** > **de calcul** > **Windows Server 2012 R2 Datacenter**, notez que hello **sélectionner un modèle de déploiement** liste déjà indique **le Gestionnaire de ressources**, puis cliquez sur **créer**, comme indiqué dans la figure ci-dessous hello.</span><span class="sxs-lookup"><span data-stu-id="7bae7-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in hello figure below.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="7bae7-121">Bonjour **notions de base** panneau, entrez le nom hello de hello toobe de machine virtuelle créée (*DNS01* dans notre scénario), hello compte d’administrateur local et le mot de passe, comme indiqué dans la figure ci-dessous hello.</span><span class="sxs-lookup"><span data-stu-id="7bae7-121">In hello **Basics** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password, as seen in hello figure below.</span></span>
   
    ![Panneau Informations de base](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="7bae7-123">Vérifiez que hello **emplacement** sélectionné est *du centre des États-Unis*, puis cliquez sur **sélectionnez existante** sous **groupe de ressources**, puis cliquez sur **Groupe de ressources** , puis cliquez sur *TestRG*, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7bae7-123">Make sure hello **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![Panneau Informations de base](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="7bae7-125">Bonjour **choisir une taille** panneau, sélectionnez **A1 Standard**, puis cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="7bae7-125">In hello **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![Panneau Choisir une taille](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="7bae7-127">Dans le **paramètres** panneau, assurez-vous de hello que propriétés suivantes sont définies sont définis avec des valeurs hello ci-dessous, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7bae7-127">In teh **Settings** blade, make sure hello following properties are set are set with hello values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="7bae7-128">-**Compte de stockage**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="7bae7-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="7bae7-129">**Réseau**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="7bae7-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="7bae7-130">**Sous-réseau**: *FrontEnd*</span><span class="sxs-lookup"><span data-stu-id="7bae7-130">**Subnet**: *FrontEnd*</span></span>
     
     ![Panneau Choisir une taille](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="7bae7-132">Bonjour **Résumé** panneau, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7bae7-132">In hello **Summary** blade, click **OK**.</span></span> <span data-ttu-id="7bae7-133">Avis hello vignette ci-dessous affichée dans votre tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="7bae7-133">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="7bae7-135">Comment informations pour une machine virtuelle d’adresse IP privée statique de tooretrieve</span><span class="sxs-lookup"><span data-stu-id="7bae7-135">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="7bae7-136">tooview hello statique privées informations d’adresse IP pour hello machine virtuelle créée avec les étapes de hello ci-dessus, exécutez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7bae7-136">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="7bae7-137">À partir du portail d’Azure Azure hello, cliquez sur **parcourir tous les** > **virtuels** > **DNS01** > **toutes les paramètres** > **interfaces réseau** , puis cliquez sur l’interface réseau uniquement hello répertorié.</span><span class="sxs-lookup"><span data-stu-id="7bae7-137">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on hello only network interface listed.</span></span>
   
    ![Déploiement d’une vignette de machine virtuelle](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="7bae7-139">Bonjour **interface réseau** panneau, cliquez sur **tous les paramètres** > **des adresses IP** et avis hello **affectation** et **Adresse IP** valeurs.</span><span class="sxs-lookup"><span data-stu-id="7bae7-139">In hello **Network interface** blade, click **All settings** > **IP addresses** and notice hello **Assignment** and **IP address** values.</span></span>
   
    ![Déploiement d’une vignette de machine virtuelle](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="7bae7-141">Comment tooadd une adresse IP privée statique d’adresses tooan existant de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7bae7-141">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="7bae7-142">tooadd un toohello d’adresse IP privée statique machine virtuelle créée à l’aide des étapes de hello ci-dessus, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7bae7-142">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="7bae7-143">À partir de hello **des adresses IP** panneau illustrée ci-dessus, cliquez sur **statique** sous **affectation**.</span><span class="sxs-lookup"><span data-stu-id="7bae7-143">From hello **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="7bae7-144">Tapez *192.168.1.101* dans **Adresse IP**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7bae7-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="7bae7-146">Si, après avoir en cliquant sur **enregistrer** vous remarquez que l’attribution hello est toujours définie trop**dynamique**, cela signifie qu’adresse hello vous avez tapé est déjà en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="7bae7-146">If after clicking **Save** you notice that hello assignment is still set too**Dynamic**, it means that hello IP address you typed is already in use.</span></span> <span data-ttu-id="7bae7-147">Essayez une autre adresse IP.</span><span class="sxs-lookup"><span data-stu-id="7bae7-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="7bae7-148">Comment tooremove une privée d’adresses IP statiques à partir d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7bae7-148">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="7bae7-149">tooremove hello adresse IP privée statique à partir de hello machine virtuelle créée ci-dessus, effectuez hello suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="7bae7-149">tooremove hello static private IP address from hello VM created above, complete hello following step:</span></span>

<span data-ttu-id="7bae7-150">À partir de hello **des adresses IP** panneau illustrée ci-dessus, cliquez sur **dynamique** sous **affectation**, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7bae7-150">From hello **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bae7-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7bae7-151">Next steps</span></span>
* <span data-ttu-id="7bae7-152">En savoir plus sur les [adresses IP publiques réservées](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="7bae7-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="7bae7-153">En savoir plus sur les [adresses IP publiques de niveau d’instance](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="7bae7-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="7bae7-154">Consultez hello [API REST de IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="7bae7-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

