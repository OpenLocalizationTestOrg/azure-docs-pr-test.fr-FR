---
title: "Gérer les groupes de sécurité réseau - Portail Azure | Microsoft Docs"
description: "Découvrez comment gérer les groupes de sécurité réseau à l’aide du portail Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: faee5ac8-f4c4-4f97-ade5-197a37aad496
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ecb4fb4608628f5a1bd54fac6af19fecfa4508f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-the-azure-portal"></a><span data-ttu-id="3dfa4-103">Gérer les groupes de sécurité réseau à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="3dfa4-103">Manage network security groups using the Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="3dfa4-104">Cet article traite du modèle de déploiement de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-104">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="3dfa4-105">Vous pouvez également [créer des groupes de sécurité réseau dans le modèle de déploiement classique](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3dfa4-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="3dfa4-106">Les exemples de commandes PowerShell ci-dessous supposent qu’un environnement simple a déjà été créé conformément au scénario décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-106">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="3dfa4-107">Si vous souhaitez exécuter les commandes telles qu’elles sont présentées dans ce document, commencez par créer l’environnement de test en déployant [ce modèle](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), cliquez sur **Déployer dans Azure**, remplacez les valeurs des paramètres par défaut si nécessaire, puis suivez les instructions dans le portail.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-107">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span> <span data-ttu-id="3dfa4-108">Les étapes ci-dessous utilisent **RG-NSG** comme nom du groupe de ressources vers lequel le modèle a été déployé.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-108">The steps below use **RG-NSG** as the name of the resource group the template was deployed to.</span></span>

## <a name="create-the-nsg-frontend-nsg"></a><span data-ttu-id="3dfa4-109">Créer le groupe de sécurité réseau NSG-FrontEnd</span><span class="sxs-lookup"><span data-stu-id="3dfa4-109">Create the NSG-FrontEnd NSG</span></span>
<span data-ttu-id="3dfa4-110">Pour créer le groupe de sécurité réseau **NSG-FrontEnd** selon le scénario ci-dessus, suivez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-110">To create the **NSG-FrontEnd** NSG as shown in the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="3dfa4-111">Dans un navigateur, accédez à http://portal.azure.com et, si nécessaire, connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-111">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="3dfa4-112">Cliquez sur **Parcourir >** > **Groupes de sécurité réseau**.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="3dfa4-114">Dans le panneau **Groupes de sécurité réseau**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-114">In the **Network security groups** blade, click **Add**.</span></span>
   
    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="3dfa4-116">Dans le panneau **Créer un groupe de sécurité réseau**, créez un groupe de sécurité réseau nommé *NSG-FrontEnd* dans le groupe de ressources *RG-NSG*, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-116">In the **Create network security group** blade, create an NSG named *NSG-FrontEnd* in the *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="3dfa4-118">Création de règles dans un NSG existant</span><span class="sxs-lookup"><span data-stu-id="3dfa4-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="3dfa4-119">Pour créer des règles dans un groupe de sécurité réseau existant à partir du portail Azure, suivez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-119">To create rules in an existing NSG from the Azure portal, follow the steps below.</span></span>

1. <span data-ttu-id="3dfa4-120">Cliquez sur **Parcourir >** > **Groupes de sécurité réseau**.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="3dfa4-121">Dans la liste des NSGs, cliquez sur **NSG-FrontEnd** > **Règles de sécurité de trafic entrant**</span><span class="sxs-lookup"><span data-stu-id="3dfa4-121">In the list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Portail Azure - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="3dfa4-123">Dans la liste **Règles de sécurité de trafic entrant**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-123">In the list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Portail Azure - Ajouter une règle](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="3dfa4-125">Dans le panneau **Ajouter une règle de sécurité de trafic entrant**, créez une règle nommée *web-rule* avec une priorité de *200* autorisant l’accès via *TCP* sur le port *80* à une machine virtuelle de n’importe quelle source, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-125">In the **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* to port *80* to any VM from any source, and then click **OK**.</span></span> <span data-ttu-id="3dfa4-126">Notez que la plupart de ces paramètres sont déjà des valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-126">Notice that most of these settings are default values already.</span></span>
   
    ![Portail Azure - Paramètres des règles](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="3dfa4-128">Après quelques secondes, vous voyez la nouvelle règle dans le NSG.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-128">After a few seconds you will see the new rule in the NSG.</span></span>
   
    ![Portail Azure - Nouvelle règle](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="3dfa4-130">Répétez les étapes 1 à 6 pour créer une règle de trafic entrant nommée *rdp-rule* avec la priorité *250* autorisant l’accès via *TCP* sur le port *3389* à une machine virtuelle de n’importe quelle source.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-130">Repeat steps  to 6 to create an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* to port *3389* to any VM from any source.</span></span>

## <a name="associate-the-nsg-to-the-frontend-subnet"></a><span data-ttu-id="3dfa4-131">Associer le groupe de sécurité réseau au sous-réseau FrontEnd</span><span class="sxs-lookup"><span data-stu-id="3dfa4-131">Associate the NSG to the FrontEnd subnet</span></span>
1. <span data-ttu-id="3dfa4-132">Cliquez sur **Parcourir >** > **Groupes de ressources** > **RG-NSG**.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="3dfa4-133">Dans le panneau **RG-NSG**, cliquez sur **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-133">In the **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Portail Azure - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="3dfa4-135">Dans le panneau **Paramètres**, cliquez sur **Sous-réseaux** > **FrontEnd** > **Groupe de sécurité réseau** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-135">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Portail Azure - Paramètres de sous-réseau](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="3dfa4-137">Dans le panneau **FrontEnd**, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-137">In the **FrontEnd** blade, click **Save**.</span></span>
   
    ![Portail Azure - Paramètres de sous-réseau](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-the-nsg-backend-nsg"></a><span data-ttu-id="3dfa4-139">Créer le groupe de sécurité réseau NSG-BackEnd</span><span class="sxs-lookup"><span data-stu-id="3dfa4-139">Create the NSG-BackEnd NSG</span></span>
<span data-ttu-id="3dfa4-140">Pour créer le groupe de sécurité réseau **NSG-BackEnd** et l’associer au sous-réseau **BackEnd**, suivez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-140">To create the **NSG-BackEnd** NSG and associate it to the **BackEnd** subnet, follow the steps below.</span></span>

1. <span data-ttu-id="3dfa4-141">Répétez les étapes de la section [Créer le groupe de sécurité réseau NSG-FrontEnd](#Create-the-NSG-FrontEnd-NSG) pour créer un groupe de sécurité réseau nommé *NSG-BackEnd*</span><span class="sxs-lookup"><span data-stu-id="3dfa4-141">Repeat the steps in [Create the NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) to create an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="3dfa4-142">Répétez les étapes de la section [Créer des règles dans un groupe de sécurité réseau existant](#Create-rules-in-an-existing-NSG) pour créer les règles **entrantes** dans le tableau ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-142">Repeat the steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) to create the **inbound** rules in the table below.</span></span>
   
   | <span data-ttu-id="3dfa4-143">Règle de trafic entrant</span><span class="sxs-lookup"><span data-stu-id="3dfa4-143">Inbound rule</span></span> | <span data-ttu-id="3dfa4-144">Règle de trafic sortant</span><span class="sxs-lookup"><span data-stu-id="3dfa4-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Portail Azure - Règle entrante](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portail Azure - Règle entrante](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="3dfa4-147">Répétez les étapes de la section [Associer le groupe de sécurité réseau au sous-réseau FrontEnd](#Associate-the-NSG-to-the-FrontEnd-subnet) pour associer le groupe de sécurité réseau **NSG-Backend** au sous-réseau **BackEnd**.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-147">Repeat the steps in [Associate the NSG to the FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) to associate the **NSG-Backend** NSG to the **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dfa4-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3dfa4-148">Next Steps</span></span>
* <span data-ttu-id="3dfa4-149">Découvrez comment [gérer des groupes de sécurité réseau existants](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3dfa4-149">Learn how to [manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="3dfa4-150">[Activez la journalisation](virtual-network-nsg-manage-log.md) des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="3dfa4-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

