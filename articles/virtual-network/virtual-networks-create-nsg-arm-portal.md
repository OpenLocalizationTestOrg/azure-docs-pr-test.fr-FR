---
title: "groupes de sécurité réseau aaaManage - portail Azure | Documents Microsoft"
description: "Découvrez comment les groupes de sécurité réseau toomanage à l’aide de hello portail Azure."
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
ms.openlocfilehash: 53fb29e60cbc2a535f6cf03e430d9e703e97b216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-portal"></a><span data-ttu-id="b559d-103">Gérer les groupes de sécurité réseau à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b559d-103">Manage network security groups using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="b559d-104">Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="b559d-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="b559d-105">Vous pouvez également [créer des groupes de sécurité réseau dans le modèle de déploiement classique hello](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b559d-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="b559d-106">l’exemple Hello PowerShell commandes ci-dessous attendent un simple environnement déjà créé en fonction de scénario hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b559d-106">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="b559d-107">Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer des environnement de test hello en déployant [ce modèle](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), cliquez sur **déployer tooAzure**, remplacez les valeurs de paramètre par défaut hello Si nécessaire et suivez les instructions hello dans hello portal.</span><span class="sxs-lookup"><span data-stu-id="b559d-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span> <span data-ttu-id="b559d-108">les étapes ci-dessous utilisent Hello **RG-NSG** comme nom de hello du modèle hello de groupe de ressources hello a été déployé sur.</span><span class="sxs-lookup"><span data-stu-id="b559d-108">hello steps below use **RG-NSG** as hello name of hello resource group hello template was deployed to.</span></span>

## <a name="create-hello-nsg-frontend-nsg"></a><span data-ttu-id="b559d-109">Créer hello NSG de serveur frontal du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="b559d-109">Create hello NSG-FrontEnd NSG</span></span>
<span data-ttu-id="b559d-110">toocreate hello **NSG-FrontEnd** NSG comme indiqué dans le scénario de hello ci-dessus, procédez comme suit hello.</span><span class="sxs-lookup"><span data-stu-id="b559d-110">toocreate hello **NSG-FrontEnd** NSG as shown in hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="b559d-111">À partir d’un navigateur, accédez à toohttp://portal.azure.com et, si nécessaire, connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="b559d-111">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="b559d-112">Cliquez sur **Parcourir >** > **Groupes de sécurité réseau**.</span><span class="sxs-lookup"><span data-stu-id="b559d-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="b559d-114">Bonjour **groupes de sécurité réseau** panneau, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b559d-114">In hello **Network security groups** blade, click **Add**.</span></span>
   
    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="b559d-116">Bonjour **créer un groupe de sécurité réseau** panneau, créer un groupe de sécurité réseau nommé *NSG-FrontEnd* Bonjour *RG-NSG* groupe de ressources, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="b559d-116">In hello **Create network security group** blade, create an NSG named *NSG-FrontEnd* in hello *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="b559d-118">Création de règles dans un NSG existant</span><span class="sxs-lookup"><span data-stu-id="b559d-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="b559d-119">règles de toocreate dans un groupe de sécurité réseau existant à partir de hello portail Azure, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b559d-119">toocreate rules in an existing NSG from hello Azure portal, follow hello steps below.</span></span>

1. <span data-ttu-id="b559d-120">Cliquez sur **Parcourir >** > **Groupes de sécurité réseau**.</span><span class="sxs-lookup"><span data-stu-id="b559d-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="b559d-121">Dans la liste de hello des groupes de sécurité réseau, cliquez sur **NSG-FrontEnd** > **les règles de sécurité de trafic entrant**</span><span class="sxs-lookup"><span data-stu-id="b559d-121">In hello list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Portail Azure - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="b559d-123">Dans la liste des hello **les règles de sécurité de trafic entrant**, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b559d-123">In hello list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Portail Azure - Ajouter une règle](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="b559d-125">Bonjour **ajouter une règle entrante sécurité** panneau, créer une règle nommée *web-règle* avec une priorité de *200* autorisant l’accès via *TCP* tooport *80* tooany machine virtuelle à partir d’une source, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b559d-125">In hello **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* tooport *80* tooany VM from any source, and then click **OK**.</span></span> <span data-ttu-id="b559d-126">Notez que la plupart de ces paramètres sont déjà des valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="b559d-126">Notice that most of these settings are default values already.</span></span>
   
    ![Portail Azure - Paramètres des règles](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="b559d-128">Après quelques secondes, vous verrez hello nouvelle règle dans hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="b559d-128">After a few seconds you will see hello new rule in hello NSG.</span></span>
   
    ![Portail Azure - Nouvelle règle](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="b559d-130">Répétez les étapes too6 toocreate une règle de trafic entrant nommée *rdp-règle* avec une priorité de *250* autorisant l’accès via *TCP* tooport *3389* tooany machine virtuelle à partir de n’importe quelle source.</span><span class="sxs-lookup"><span data-stu-id="b559d-130">Repeat steps  too6 toocreate an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* tooport *3389* tooany VM from any source.</span></span>

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a><span data-ttu-id="b559d-131">Associer le sous-réseau frontal de hello NSG toohello</span><span class="sxs-lookup"><span data-stu-id="b559d-131">Associate hello NSG toohello FrontEnd subnet</span></span>
1. <span data-ttu-id="b559d-132">Cliquez sur **Parcourir >** > **Groupes de ressources** > **RG-NSG**.</span><span class="sxs-lookup"><span data-stu-id="b559d-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="b559d-133">Bonjour **RG-NSG** panneau, cliquez sur **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="b559d-133">In hello **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Portail Azure - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="b559d-135">Bonjour **paramètres** panneau, cliquez sur **sous-réseaux** > **frontal** > **groupe de sécurité réseau**  >  **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="b559d-135">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Portail Azure - Paramètres de sous-réseau](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="b559d-137">Bonjour **frontal** panneau, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b559d-137">In hello **FrontEnd** blade, click **Save**.</span></span>
   
    ![Portail Azure - Paramètres de sous-réseau](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a><span data-ttu-id="b559d-139">Créer hello NSG du serveur principal du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="b559d-139">Create hello NSG-BackEnd NSG</span></span>
<span data-ttu-id="b559d-140">toocreate hello **principal de groupe de sécurité réseau** NSG et associez-le toohello **principal** sous-réseau, suivez les étapes hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b559d-140">toocreate hello **NSG-BackEnd** NSG and associate it toohello **BackEnd** subnet, follow hello steps below.</span></span>

1. <span data-ttu-id="b559d-141">Hello Répétez les étapes [créer hello NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) toocreate un groupe de sécurité réseau nommé *principal de groupe de sécurité réseau*</span><span class="sxs-lookup"><span data-stu-id="b559d-141">Repeat hello steps in [Create hello NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) toocreate an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="b559d-142">Hello Répétez les étapes [créer des règles dans un groupe de sécurité réseau existant](#Create-rules-in-an-existing-NSG) toocreate hello **entrant** règles dans la table hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b559d-142">Repeat hello steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) toocreate hello **inbound** rules in hello table below.</span></span>
   
   | <span data-ttu-id="b559d-143">Règle de trafic entrant</span><span class="sxs-lookup"><span data-stu-id="b559d-143">Inbound rule</span></span> | <span data-ttu-id="b559d-144">Règle de trafic sortant</span><span class="sxs-lookup"><span data-stu-id="b559d-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Portail Azure - Règle entrante](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portail Azure - Règle entrante](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="b559d-147">Hello Répétez les étapes [associer le sous-réseau frontal de hello NSG toohello](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **principal de groupe de sécurité réseau** NSG toohello **principal** sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="b559d-147">Repeat hello steps in [Associate hello NSG toohello FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG-Backend** NSG toohello **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b559d-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b559d-148">Next Steps</span></span>
* <span data-ttu-id="b559d-149">Découvrez comment trop[gérer les groupes de sécurité réseau existants](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b559d-149">Learn how too[manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="b559d-150">[Activez la journalisation](virtual-network-nsg-manage-log.md) des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="b559d-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

