---
title: "groupes de sécurité réseau aaaManage à l’aide de hello portail Azure | Documents Microsoft"
description: "Découvrez comment toomanage existante des groupes de sécurité réseau à l’aide de hello portail Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a><span data-ttu-id="7332f-103">Gérer des groupes de sécurité réseau à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="7332f-103">Manage NSGs using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7332f-104">Portail</span><span class="sxs-lookup"><span data-stu-id="7332f-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="7332f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7332f-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="7332f-106">interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="7332f-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="7332f-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7332f-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7332f-108">Cet article décrit à l’aide du modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="7332f-108">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="7332f-109">Récupérer des informations</span><span class="sxs-lookup"><span data-stu-id="7332f-109">Retrieve Information</span></span>
<span data-ttu-id="7332f-110">Vous pouvez afficher vos groupes de sécurité réseau existants, récupérer des règles pour un groupe de sécurité réseau existant et découvrir quelles sont les ressources associées à un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="7332f-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="7332f-111">Afficher les groupes de sécurité réseau existants</span><span class="sxs-lookup"><span data-stu-id="7332f-111">View existing NSGs</span></span>

<span data-ttu-id="7332f-112">tooview tous les existante des groupes de sécurité réseau dans un abonnement, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="7332f-112">tooview all existing NSGs in a subscription, complete hello following steps:</span></span>

1. <span data-ttu-id="7332f-113">À partir d’un navigateur, accédez à toohttp://portal.azure.com et, si nécessaire, connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="7332f-113">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="7332f-114">Cliquez sur **Parcourir >** > **Groupes de sécurité réseau**.</span><span class="sxs-lookup"><span data-stu-id="7332f-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="7332f-116">Vérifier la liste hello de groupes de sécurité réseau Bonjour **groupes de sécurité réseau** panneau.</span><span class="sxs-lookup"><span data-stu-id="7332f-116">Check hello list of NSGs in hello **Network security groups** blade.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="7332f-118">Afficher les groupes de sécurité réseau d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="7332f-118">View NSGs in a resource group</span></span>

<span data-ttu-id="7332f-119">liste de hello tooview de groupes de sécurité réseau Bonjour **RG-NSG** groupe de ressources, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="7332f-119">tooview hello list of NSGs in hello **RG-NSG** resource group, complete hello following steps:</span></span>

1. <span data-ttu-id="7332f-120">Cliquez sur **Groupes de ressources >** > **RG-NSG** > **...**.</span><span class="sxs-lookup"><span data-stu-id="7332f-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="7332f-122">Dans la liste de hello des ressources, rechercher les éléments affichant hello icône de groupe de sécurité réseau, comme indiqué dans hello **ressources** panneau ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7332f-122">In hello list of resources, look for items displaying hello NSG icon, as shown in hello **Resources** blade below.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="7332f-124">Répertorier toutes les règles pour un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="7332f-124">List all rules for an NSG</span></span>

<span data-ttu-id="7332f-125">règles de hello tooview d’un groupe de sécurité réseau nommé **NSG-FrontEnd**complète hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7332f-125">tooview hello rules of an NSG named **NSG-FrontEnd**, complete hello following steps:</span></span>

1. <span data-ttu-id="7332f-126">À partir de hello **groupes de sécurité réseau** panneau ou hello **ressources** panneau illustrée ci-dessus, cliquez sur **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7332f-126">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="7332f-127">Bonjour **paramètres** , cliquez sur **les règles de sécurité de trafic entrant**.</span><span class="sxs-lookup"><span data-stu-id="7332f-127">In hello **Settings** tab, click **Inbound security rules**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="7332f-129">Hello **les règles de sécurité de trafic entrant** panneau s’affiche comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7332f-129">hello **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="7332f-131">Bonjour **paramètres** , cliquez sur **les règles de sécurité sortante** toosee hello des règles de trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="7332f-131">In hello **Settings** tab, click **Outbound security rules** toosee hello outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7332f-132">tooview les règles par défaut, cliquez sur hello **règles par défaut** icône haut hello du panneau hello qui affiche les règles de hello.</span><span class="sxs-lookup"><span data-stu-id="7332f-132">tooview default rules, click hello **Default rules** icon at hello top of hello blade that displays hello rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="7332f-133">Afficher les associations de groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="7332f-133">View NSGs associations</span></span>

<span data-ttu-id="7332f-134">tooview hello de quelles ressources **NSG-FrontEnd** NSG est hello associez, complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="7332f-134">tooview what resources hello **NSG-FrontEnd** NSG is associate with, complete hello following steps:</span></span>

1. <span data-ttu-id="7332f-135">À partir de hello **groupes de sécurité réseau** panneau ou hello **ressources** panneau illustrée ci-dessus, cliquez sur **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7332f-135">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="7332f-136">Bonjour **paramètres** , cliquez sur **sous-réseaux** tooview quels sous-réseaux est associés toohello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="7332f-136">In hello **Settings** tab, click **Subnets** tooview what subnets are associated toohello NSG.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="7332f-138">Bonjour **paramètres** , cliquez sur **interfaces réseau** tooview quelles cartes réseau est associées toohello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="7332f-138">In hello **Settings** tab, click **Network interfaces** tooview what NICs are associated toohello NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="7332f-139">Gérer les règles</span><span class="sxs-lookup"><span data-stu-id="7332f-139">Manage rules</span></span>
<span data-ttu-id="7332f-140">Vous pouvez ajouter tooan règles existants du groupe de sécurité réseau, modifier les règles existantes et supprimer des règles.</span><span class="sxs-lookup"><span data-stu-id="7332f-140">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="7332f-141">Ajouter une règle</span><span class="sxs-lookup"><span data-stu-id="7332f-141">Add a rule</span></span>
<span data-ttu-id="7332f-142">tooadd une règle autorisant **entrant** trafic tooport **443** à partir de n’importe quel ordinateur toohello **NSG-FrontEnd** NSG, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="7332f-142">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="7332f-143">À partir de hello **groupes de sécurité réseau** panneau ou hello **ressources** panneau illustrée ci-dessus, cliquez sur **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7332f-143">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="7332f-144">Bonjour **paramètres** , cliquez sur **les règles de sécurité de trafic entrant**.</span><span class="sxs-lookup"><span data-stu-id="7332f-144">In hello **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="7332f-145">Bonjour **les règles de sécurité de trafic entrant** panneau, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7332f-145">In hello **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="7332f-146">Ensuite, dans hello **ajouter une règle entrante sécurité** panneau, remplir les valeurs hello, comme illustré ci-dessous, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7332f-146">Then, in hello **Add inbound security rule** blade, fill hello values as shown below, and then click **OK**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="7332f-148">Après quelques secondes, notez la nouvelle règle de hello Bonjour **les règles de sécurité de trafic entrant** panneau.</span><span class="sxs-lookup"><span data-stu-id="7332f-148">After a few seconds, notice hello new rule in hello **Inbound security rules** blade.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="7332f-150">Modifier une règle</span><span class="sxs-lookup"><span data-stu-id="7332f-150">Change a rule</span></span>
<span data-ttu-id="7332f-151">règle de hello toochange créé ci-dessus tooallow le trafic entrant provenance hello **Internet** hello uniquement, complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="7332f-151">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, complete hello following steps:</span></span>

1. <span data-ttu-id="7332f-152">À partir de hello **groupes de sécurité réseau** panneau ou hello **ressources** panneau illustrée ci-dessus, cliquez sur **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7332f-152">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="7332f-153">Bonjour **paramètres** , cliquez sur règle hello créé ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7332f-153">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="7332f-154">Bonjour **https autoriser** panneau, modification hello **Source** propriété comme indiqué ci-dessous, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7332f-154">In hello **allow-https** blade, change hello **Source** property as shown below, and then click **Save**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="7332f-156">Supprimer une règle</span><span class="sxs-lookup"><span data-stu-id="7332f-156">Delete a rule</span></span>

<span data-ttu-id="7332f-157">toodelete hello règle créée ci-dessus, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7332f-157">toodelete hello rule created above, complete hello following steps:</span></span>

1. <span data-ttu-id="7332f-158">À partir de hello **groupes de sécurité réseau** panneau ou hello **ressources** panneau illustrée ci-dessus, cliquez sur **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7332f-158">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="7332f-159">Bonjour **paramètres** , cliquez sur règle hello créé ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7332f-159">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="7332f-160">Bonjour **https autoriser** panneau, cliquez sur **supprimer**, puis cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="7332f-160">In hello **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="7332f-162">Gérer les associations</span><span class="sxs-lookup"><span data-stu-id="7332f-162">Manage associations</span></span>
<span data-ttu-id="7332f-163">Vous pouvez associer un toosubnets du groupe de sécurité réseau et les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="7332f-163">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="7332f-164">Vous pouvez également dissocier un groupe de sécurité réseau de n’importe quelle ressource à laquelle il est associé.</span><span class="sxs-lookup"><span data-stu-id="7332f-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="7332f-165">Associer un groupe de sécurité réseau de tooa carte réseau</span><span class="sxs-lookup"><span data-stu-id="7332f-165">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="7332f-166">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="7332f-166">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="7332f-167">À partir de hello **groupes de sécurité réseau** panneau ou hello **ressources** panneau illustrée ci-dessus, cliquez sur **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7332f-167">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="7332f-168">Bonjour **paramètres** , cliquez sur **interfaces réseau** > **associer** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="7332f-168">In hello **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="7332f-170">Dissocier un groupe de sécurité réseau d’une carte réseau</span><span class="sxs-lookup"><span data-stu-id="7332f-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="7332f-171">toodissociate hello **NSG-FrontEnd** groupe de sécurité réseau à partir de hello **TestNICWeb1** NIC, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="7332f-171">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="7332f-172">À partir de hello portail Azure, cliquez sur **groupes de ressources >** > **RG-NSG** > **...**   >  **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="7332f-172">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="7332f-173">Bonjour **TestNICWeb1** panneau, cliquez sur **modifier la sécurité...**   >  **Aucun**.</span><span class="sxs-lookup"><span data-stu-id="7332f-173">In hello **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="7332f-175">Vous pouvez également utiliser cette tooany de carte réseau panneau tooassociate hello existants du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="7332f-175">You can also use this blade tooassociate hello NIC tooany existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="7332f-176">Dissocier un groupe de sécurité réseau d’un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="7332f-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="7332f-177">toodissociate hello **NSG-FrontEnd** groupe de sécurité réseau à partir de hello **frontal** sous-réseau, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="7332f-177">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="7332f-178">À partir de hello portail Azure, cliquez sur **groupes de ressources >** > **RG-NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="7332f-178">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="7332f-179">Bonjour **paramètres** panneau, cliquez sur **sous-réseaux** > **frontal** > **groupe de sécurité réseau**  >  **Aucun**.</span><span class="sxs-lookup"><span data-stu-id="7332f-179">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="7332f-181">Bonjour **frontal** panneau, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7332f-181">In hello **FrontEnd** blade, click **Save**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="7332f-183">Associez un sous-réseau de tooa du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="7332f-183">Associate an NSG tooa subnet</span></span>

<span data-ttu-id="7332f-184">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** à nouveau le sous-réseau, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="7332f-184">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="7332f-185">À partir de hello portail Azure, cliquez sur **groupes de ressources >** > **RG-NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="7332f-185">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="7332f-186">Bonjour **paramètres** panneau, cliquez sur **sous-réseaux** > **frontal** > **groupe de sécurité réseau**  >  **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7332f-186">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="7332f-187">Bonjour **frontal** panneau, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7332f-187">In hello **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="7332f-188">Vous pouvez également associer un sous-réseau tooa de groupe de sécurité réseau à partir de thh NSG **paramètres** panneau.</span><span class="sxs-lookup"><span data-stu-id="7332f-188">You can also associate an NSG tooa subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="7332f-189">Suppression d'un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="7332f-189">Delete an NSG</span></span>
<span data-ttu-id="7332f-190">Vous ne pouvez supprimer un groupe de sécurité réseau si elle n’est pas associé à tooany ressource.</span><span class="sxs-lookup"><span data-stu-id="7332f-190">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="7332f-191">toodelete un groupe de sécurité réseau, hello complète comme suit :.</span><span class="sxs-lookup"><span data-stu-id="7332f-191">toodelete an NSG, complete hello following steps:.</span></span>

1. <span data-ttu-id="7332f-192">À partir de hello portail Azure, cliquez sur **groupes de ressources >** > **RG-NSG** > **...**   >  **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7332f-192">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="7332f-193">Bonjour **paramètres** panneau, cliquez sur **interfaces réseau**.</span><span class="sxs-lookup"><span data-stu-id="7332f-193">In hello **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="7332f-194">S’il existe des cartes réseau répertoriées, cliquez sur hello NIC et suivez l’étape 2 de [dissocier un groupe de sécurité réseau à partir d’une carte réseau](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="7332f-194">If there are any NICs listed, click hello NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="7332f-195">Répétez l’étape 3 pour chaque carte réseau.</span><span class="sxs-lookup"><span data-stu-id="7332f-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="7332f-196">Bonjour **paramètres** panneau, cliquez sur **sous-réseaux**.</span><span class="sxs-lookup"><span data-stu-id="7332f-196">In hello **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="7332f-197">S’il existe des sous-réseaux répertoriés, cliquez sur le sous-réseau de hello et suivez les étapes 2 et 3 dans [dissocier un groupe de sécurité réseau à partir d’un sous-réseau](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="7332f-197">If there are any subnets listed, click hello subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="7332f-198">Fait défiler vers la gauche toohello **NSG-FrontEnd** panneau, puis cliquez sur **supprimer** > **Oui**.</span><span class="sxs-lookup"><span data-stu-id="7332f-198">Scrolls left toohello **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="7332f-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7332f-200">Next steps</span></span>
* <span data-ttu-id="7332f-201">[Activez la journalisation](virtual-network-nsg-manage-log.md) des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="7332f-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
