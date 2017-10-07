---
title: "groupes de sécurité réseau aaaCreate - portail Azure | Documents Microsoft"
description: "Découvrez comment toocreate et déployer des groupes de sécurité réseau à l’aide de hello portail Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5bc8fc2e-1e81-40e2-8231-0484cd5605cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74ecc7db06bb69f2041aa64d7b38b63eb379a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-portal"></a>Créer des groupes de sécurité à l’aide de hello portail Azure réseau

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello. Vous pouvez également [créer des groupes de sécurité réseau dans le modèle de déploiement classique hello](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

l’exemple Hello PowerShell commandes ci-dessous attendent un simple environnement déjà créé en fonction de scénario hello ci-dessus. Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer des environnement de test hello en déployant [ce modèle](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), cliquez sur **déployer tooAzure**, remplacez les valeurs de paramètre par défaut hello Si nécessaire et suivez les instructions hello dans hello portal. les étapes ci-dessous utilisent Hello **RG-NSG** comme nom de hello du modèle hello de groupe de ressources hello a été déployé sur.

## <a name="create-hello-nsg-frontend-nsg"></a>Créer hello NSG de serveur frontal du groupe de sécurité réseau
toocreate hello **NSG-FrontEnd** NSG comme indiqué dans le scénario de hello ci-dessus, procédez comme suit hello.

1. À partir d’un navigateur, accédez à toohttp://portal.azure.com et, si nécessaire, connectez-vous avec votre compte Azure.
2. Cliquez sur **Parcourir >** > **Groupes de sécurité réseau**.
   
    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. Bonjour **groupes de sécurité réseau** panneau, cliquez sur **ajouter**.
   
    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. Bonjour **créer un groupe de sécurité réseau** panneau, créer un groupe de sécurité réseau nommé *NSG-FrontEnd* Bonjour *RG-NSG* groupe de ressources, puis cliquez sur **créer**.
   
    ![Portail Azure - Groupes de sécurité réseau](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a>Création de règles dans un NSG existant
règles de toocreate dans un groupe de sécurité réseau existant à partir de hello portail Azure, suivez les étapes de hello ci-dessous.

1. Cliquez sur **Parcourir >** > **Groupes de sécurité réseau**.
2. Dans la liste de hello des groupes de sécurité réseau, cliquez sur **NSG-FrontEnd** > **les règles de sécurité de trafic entrant**
   
    ![Portail Azure - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. Dans la liste des hello **les règles de sécurité de trafic entrant**, cliquez sur **ajouter**.
   
    ![Portail Azure - Ajouter une règle](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. Bonjour **ajouter une règle entrante sécurité** panneau, créer une règle nommée *web-règle* avec une priorité de *200* autorisant l’accès via *TCP* tooport *80* tooany machine virtuelle à partir d’une source, puis cliquez sur **OK**. Notez que la plupart de ces paramètres sont déjà des valeurs par défaut.
   
    ![Portail Azure - Paramètres des règles](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. Après quelques secondes, vous verrez hello nouvelle règle dans hello groupe de sécurité réseau.
   
    ![Portail Azure - Nouvelle règle](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. Répétez les étapes too6 toocreate une règle de trafic entrant nommée *rdp-règle* avec une priorité de *250* autorisant l’accès via *TCP* tooport *3389* tooany machine virtuelle à partir de n’importe quelle source.

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a>Associer le sous-réseau frontal de hello NSG toohello
1. Cliquez sur **Parcourir >** > **Groupes de ressources** > **RG-NSG**.
2. Bonjour **RG-NSG** panneau, cliquez sur **...**   >  **TestVNet**.
   
    ![Portail Azure - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. Bonjour **paramètres** panneau, cliquez sur **sous-réseaux** > **frontal** > **groupe de sécurité réseau**  >  **NSG-FrontEnd**.
   
    ![Portail Azure - Paramètres de sous-réseau](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. Bonjour **frontal** panneau, cliquez sur **enregistrer**.
   
    ![Portail Azure - Paramètres de sous-réseau](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a>Créer hello NSG du serveur principal du groupe de sécurité réseau
toocreate hello **principal de groupe de sécurité réseau** NSG et associez-le toohello **principal** sous-réseau, suivez les étapes hello ci-dessous.

1. Hello Répétez les étapes [créer hello NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) toocreate un groupe de sécurité réseau nommé *principal de groupe de sécurité réseau*
2. Hello Répétez les étapes [créer des règles dans un groupe de sécurité réseau existant](#Create-rules-in-an-existing-NSG) toocreate hello **entrant** règles dans la table hello ci-dessous.
   
   | Règle de trafic entrant | Règle de trafic sortant |
   | --- | --- |
   | ![Portail Azure - Règle entrante](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portail Azure - Règle entrante](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. Hello Répétez les étapes [associer le sous-réseau frontal de hello NSG toohello](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **principal de groupe de sécurité réseau** NSG toohello **principal** sous-réseau.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[gérer les groupes de sécurité réseau existants](virtual-network-manage-nsg-arm-portal.md)
* [Activez la journalisation](virtual-network-nsg-manage-log.md) des groupes de sécurité réseau.

