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
# <a name="manage-nsgs-using-hello-portal"></a>Gérer des groupes de sécurité réseau à l’aide du portail de hello

> [!div class="op_single_selector"]
> * [Portail](virtual-network-manage-nsg-arm-portal.md)
> * [PowerShell](virtual-network-manage-nsg-arm-ps.md)
> * [interface de ligne de commande Azure](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu du modèle de déploiement classique hello.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a>Récupérer des informations
Vous pouvez afficher vos groupes de sécurité réseau existants, récupérer des règles pour un groupe de sécurité réseau existant et découvrir quelles sont les ressources associées à un groupe de sécurité réseau.

### <a name="view-existing-nsgs"></a>Afficher les groupes de sécurité réseau existants

tooview tous les existante des groupes de sécurité réseau dans un abonnement, hello complète comme suit :

1. À partir d’un navigateur, accédez à toohttp://portal.azure.com et, si nécessaire, connectez-vous avec votre compte Azure.

2. Cliquez sur **Parcourir >** > **Groupes de sécurité réseau**.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. Vérifier la liste hello de groupes de sécurité réseau Bonjour **groupes de sécurité réseau** panneau.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a>Afficher les groupes de sécurité réseau d’un groupe de ressources

liste de hello tooview de groupes de sécurité réseau Bonjour **RG-NSG** groupe de ressources, hello complète comme suit :

1. Cliquez sur **Groupes de ressources >** > **RG-NSG** > **...**.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. Dans la liste de hello des ressources, rechercher les éléments affichant hello icône de groupe de sécurité réseau, comme indiqué dans hello **ressources** panneau ci-dessous.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a>Répertorier toutes les règles pour un groupe de sécurité réseau

règles de hello tooview d’un groupe de sécurité réseau nommé **NSG-FrontEnd**complète hello comme suit :

1. À partir de hello **groupes de sécurité réseau** panneau ou hello **ressources** panneau illustrée ci-dessus, cliquez sur **NSG-FrontEnd**.

2. Bonjour **paramètres** , cliquez sur **les règles de sécurité de trafic entrant**.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. Hello **les règles de sécurité de trafic entrant** panneau s’affiche comme illustré ci-dessous.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. Bonjour **paramètres** , cliquez sur **les règles de sécurité sortante** toosee hello des règles de trafic sortant.

    > [!NOTE]
    > tooview les règles par défaut, cliquez sur hello **règles par défaut** icône haut hello du panneau hello qui affiche les règles de hello.
    >

### <a name="view-nsgs-associations"></a>Afficher les associations de groupes de sécurité réseau

tooview hello de quelles ressources **NSG-FrontEnd** NSG est hello associez, complète comme suit :

1. À partir de hello **groupes de sécurité réseau** panneau ou hello **ressources** panneau illustrée ci-dessus, cliquez sur **NSG-FrontEnd**.

2. Bonjour **paramètres** , cliquez sur **sous-réseaux** tooview quels sous-réseaux est associés toohello groupe de sécurité réseau.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. Bonjour **paramètres** , cliquez sur **interfaces réseau** tooview quelles cartes réseau est associées toohello groupe de sécurité réseau.

## <a name="manage-rules"></a>Gérer les règles
Vous pouvez ajouter tooan règles existants du groupe de sécurité réseau, modifier les règles existantes et supprimer des règles.

### <a name="add-a-rule"></a>Ajouter une règle
tooadd une règle autorisant **entrant** trafic tooport **443** à partir de n’importe quel ordinateur toohello **NSG-FrontEnd** NSG, hello complète comme suit :

1. À partir de hello **groupes de sécurité réseau** panneau ou hello **ressources** panneau illustrée ci-dessus, cliquez sur **NSG-FrontEnd**.
2. Bonjour **paramètres** , cliquez sur **les règles de sécurité de trafic entrant**.
3. Bonjour **les règles de sécurité de trafic entrant** panneau, cliquez sur **ajouter**. Ensuite, dans hello **ajouter une règle entrante sécurité** panneau, remplir les valeurs hello, comme illustré ci-dessous, puis cliquez sur **OK**.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    Après quelques secondes, notez la nouvelle règle de hello Bonjour **les règles de sécurité de trafic entrant** panneau.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a>Modifier une règle
règle de hello toochange créé ci-dessus tooallow le trafic entrant provenance hello **Internet** hello uniquement, complète comme suit :

1. À partir de hello **groupes de sécurité réseau** panneau ou hello **ressources** panneau illustrée ci-dessus, cliquez sur **NSG-FrontEnd**.
2. Bonjour **paramètres** , cliquez sur règle hello créé ci-dessus.
3. Bonjour **https autoriser** panneau, modification hello **Source** propriété comme indiqué ci-dessous, puis cliquez sur **enregistrer**.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a>Supprimer une règle

toodelete hello règle créée ci-dessus, effectuez hello comme suit :

1. À partir de hello **groupes de sécurité réseau** panneau ou hello **ressources** panneau illustrée ci-dessus, cliquez sur **NSG-FrontEnd**.
2. Bonjour **paramètres** , cliquez sur règle hello créé ci-dessus.
3. Bonjour **https autoriser** panneau, cliquez sur **supprimer**, puis cliquez sur **Oui**.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a>Gérer les associations
Vous pouvez associer un toosubnets du groupe de sécurité réseau et les cartes réseau. Vous pouvez également dissocier un groupe de sécurité réseau de n’importe quelle ressource à laquelle il est associé.

### <a name="associate-an-nsg-tooa-nic"></a>Associer un groupe de sécurité réseau de tooa carte réseau
tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, hello complète comme suit :

1. À partir de hello **groupes de sécurité réseau** panneau ou hello **ressources** panneau illustrée ci-dessus, cliquez sur **NSG-FrontEnd**.
2. Bonjour **paramètres** , cliquez sur **interfaces réseau** > **associer** > **TestNICWeb1**.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a>Dissocier un groupe de sécurité réseau d’une carte réseau

toodissociate hello **NSG-FrontEnd** groupe de sécurité réseau à partir de hello **TestNICWeb1** NIC, hello complète comme suit :

1. À partir de hello portail Azure, cliquez sur **groupes de ressources >** > **RG-NSG** > **...**   >  **TestNICWeb1**.

2. Bonjour **TestNICWeb1** panneau, cliquez sur **modifier la sécurité...**   >  **Aucun**.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> Vous pouvez également utiliser cette tooany de carte réseau panneau tooassociate hello existants du groupe de sécurité réseau.
>

### <a name="dissociate-an-nsg-from-a-subnet"></a>Dissocier un groupe de sécurité réseau d’un sous-réseau

toodissociate hello **NSG-FrontEnd** groupe de sécurité réseau à partir de hello **frontal** sous-réseau, hello complète comme suit :

1. À partir de hello portail Azure, cliquez sur **groupes de ressources >** > **RG-NSG** > **...**   >  **TestVNet**.

2. Bonjour **paramètres** panneau, cliquez sur **sous-réseaux** > **frontal** > **groupe de sécurité réseau**  >  **Aucun**.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. Bonjour **frontal** panneau, cliquez sur **enregistrer**.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a>Associez un sous-réseau de tooa du groupe de sécurité réseau

tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** à nouveau le sous-réseau, hello complète comme suit :

1. À partir de hello portail Azure, cliquez sur **groupes de ressources >** > **RG-NSG** > **...**   >  **TestVNet**.
2. Bonjour **paramètres** panneau, cliquez sur **sous-réseaux** > **frontal** > **groupe de sécurité réseau**  >  **NSG-FrontEnd**.
3. Bonjour **frontal** panneau, cliquez sur **enregistrer**.

> [!NOTE]
> Vous pouvez également associer un sous-réseau tooa de groupe de sécurité réseau à partir de thh NSG **paramètres** panneau.
>

## <a name="delete-an-nsg"></a>Suppression d'un groupe de sécurité réseau
Vous ne pouvez supprimer un groupe de sécurité réseau si elle n’est pas associé à tooany ressource. toodelete un groupe de sécurité réseau, hello complète comme suit :.

1. À partir de hello portail Azure, cliquez sur **groupes de ressources >** > **RG-NSG** > **...**   >  **NSG-FrontEnd**.
2. Bonjour **paramètres** panneau, cliquez sur **interfaces réseau**.
3. S’il existe des cartes réseau répertoriées, cliquez sur hello NIC et suivez l’étape 2 de [dissocier un groupe de sécurité réseau à partir d’une carte réseau](#Dissociate-an-NSG-from-a-NIC).
4. Répétez l’étape 3 pour chaque carte réseau.
5. Bonjour **paramètres** panneau, cliquez sur **sous-réseaux**.
6. S’il existe des sous-réseaux répertoriés, cliquez sur le sous-réseau de hello et suivez les étapes 2 et 3 dans [dissocier un groupe de sécurité réseau à partir d’un sous-réseau](#Dissociate-an-NSG-from-a-subnet).
7. Fait défiler vers la gauche toohello **NSG-FrontEnd** panneau, puis cliquez sur **supprimer** > **Oui**.

    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a>Étapes suivantes
* [Activez la journalisation](virtual-network-nsg-manage-log.md) des groupes de sécurité réseau.
