---
title: "équilibrage de charge aaaCreate une côté Internet - portail Azure | Documents Microsoft"
description: "Découvrez comment toocreate une côté Internet équilibrage de charge à l’aide du Gestionnaire de ressources hello portail Azure"
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: annahar
ms.openlocfilehash: 390ba8ec1474c54cf2c0022c4a3c219d21b1a659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-hello-azure-portal"></a>Création d’un équilibrage de charge connecté à Internet à l’aide de hello portail Azure

> [!div class="op_single_selector"]
> * [Portail](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Modèle](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello. Vous pouvez également [apprendre comment toocreate une côté Internet l’équilibrage de charge à l’aide de déploiement classique](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

Cette rubrique décrit les séquences hello des tâches individuelles et expliquent en détail ce qui est effectué l’objectif de hello tooaccomplish toobe fait toocreate un équilibreur de charge.

## <a name="what-is-required-toocreate-an-internet-facing-load-balancer"></a>Qu’est requis toocreate un équilibrage de charge connecté à Internet ?

Vous devez toocreate et que vous configurez hello suivant objets toodeploy un équilibreur de charge.

* Configuration d’adresses IP frontales : contient les adresses IP publiques pour le trafic réseau entrant.
* Pool d’adresses principal - contient des interfaces réseau (NIC) pour le trafic réseau tooreceive de hello machines virtuelles à partir de l’équilibrage de charge hello.
* Règles d’équilibrage de charge - contient des règles de mappage d’un port public sur tooport d’équilibrage de charge hello dans un pool d’adresses de serveur principal hello.
* Les règles NAT de trafic entrant - contient des règles de mappage d’un port public sur le port de tooa d’équilibrage de charge hello pour un ordinateur virtuel spécifique dans le pool d’adresses principal hello.
* Sondes - contient la disponibilité de toocheck les sondes utilisées de contrôle d’intégrité des instances de machines virtuelles dans un pool d’adresses de serveur principal hello.

Pour obtenir plus d’informations sur les composants de l’équilibreur de charge avec Azure Resource Manager, consultez la page [Support Azure Resource Manager pour l’équilibreur de charge](load-balancer-arm.md).

## <a name="set-up-a-load-balancer-in-azure-portal"></a>Configurer un équilibreur de charge dans le portail Azure

> [!IMPORTANT]
> Cet exemple suppose que vous disposez d’un réseau virtuel appelé **myVNet**. Consultez trop[créer le réseau virtuel](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) toodo cela. Il suppose également est un sous-réseau dans **myVNet** appelé **LB sous-réseau être** et deux machines virtuelles appelés **web1** et **web2** respectivement dans Hello du même groupe à haute disponibilité appelée **myAvailSet** dans **myVNet**. Consultez trop[ce lien](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocreate machines virtuelles.

1. À partir d’un navigateur, accédez toohello portail Azure : [http://portal.azure.com](http://portal.azure.com) et connectez-vous à votre compte Azure.
2. Hello haut à gauche de l’écran hello sur **nouveau** > **réseau** > **équilibrage de charge.**
3. Bonjour **équilibrage de charge créer** panneau, tapez un nom pour votre équilibreur de charge. Ici, il s’appelle **myLoadBalancer**.
4. Sous **Type**, sélectionnez **Public**.
5. Sous **Adresse IP publique**, créez une nouvelle adresse IP publique appelée **myPublicIP**.
6. Sous Groupe de ressources, sélectionnez **myRG**. Sélectionnez l’**emplacement** approprié, puis cliquez sur **OK**. équilibrage de charge Hello commence ensuite à toodeploy et prendra quelques minutes toosuccessfully complète de déploiement.

    ![Mise à jour du groupe de ressources de l’équilibreur de charge](./media/load-balancer-get-started-internet-portal/1-load-balancer.png)

## <a name="create-a-back-end-address-pool"></a>Créer un pool d’adresses principal

1. Une fois votre équilibreur de charge déployé avec succès, sélectionnez-le depuis vos ressources. Sous Paramètres, sélectionnez Pools principaux. Saisissez le nom de votre pool principal. Cliquez ensuite sur hello **ajouter** bouton vers le haut hello du panneau hello qui s’affiche.
2. Cliquez sur **ajouter une machine virtuelle** Bonjour **ajouter le pool principal** panneau.  Sélectionnez **Choisir un groupe à haute disponibilité** sous **Groupe à haute disponibilité**, puis choisissez **myAvailSet**. Ensuite, sélectionnez **choisissez hello virtuels** sous hello section de Machines virtuelles dans le panneau de hello et cliquez sur **web1** et **web2**, hello deux machines virtuelles créées pour l’équilibrage de charge. Assurez-vous que les deux ont toohello bleu coches gauche comme indiqué dans l’image hello ci-dessous. Ensuite, cliquez sur **sélectionnez** dans ce panneau suivi OK Bonjour **choisir des machines virtuelles** panneau, puis **OK** Bonjour **ajouter le pool principal** panneau.

    ![Ajout de pool d’adresses principales toohello- ](./media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. Vérifiez toomake que les notifications de liste déroulant dispose d’une mise à jour concernant l’enregistrement hello pool principal d’équilibreurs de charge dans l’interface de réseau plus tooupdating hello pour les deux hello machines virtuelles **web1** et **web2**.

## <a name="create-a-probe-lb-rule-and-nat-rules"></a>Créer une sonde, une règle d’équilibrage de charge et des règles NAT

1. Créer une sonde d’intégrité.

    Dans les paramètres de votre équilibreur de charge, sélectionnez Sondes. Puis cliquez sur **ajouter** situé en haut de hello du Panneau de hello.

    Il existe deux façons tooconfigure une sonde : HTTP ou TCP. Cet exemple montre HTTP, mais TCP peut être configuré de la même manière.
    Mettre à jour les informations nécessaires hello. Comme indiqué, **myLoadBalancer** équilibrera le trafic sur le port 80. chemin d’accès Hello sélectionné est HealthProbe.aspx, intervalle est de 15 secondes et seuil de fonctionnement anormal est 2. Une fois que vous avez terminé, cliquez sur **OK** sonde de hello toocreate.

    Placez votre pointeur sur toolearn d’icône hello 'i' plus d’informations sur ces configurations individuelles et comment ils peuvent être modifiées toocater tooyour exigences.

    ![Ajout d'une sonde](./media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

2. Créez une règle d’équilibreur de charge.

    Cliquez sur règles Bonjour d’équilibrage de charge le section Paramètres de votre équilibreur de charge. Dans le panneau de nouveau hello, cliquez sur **ajouter**. Nommez votre règle. Ici, HTTP. Choisissez le port de serveur frontal hello et le port principal. Ici, 80 est choisi pour les deux. Choisissez **principal de l’équilibrage de charge** comme pool principal et hello précédemment créé **HealthProbe** comme hello sonde. D’autres configurations peuvent être définies en fonction des exigences de tooyour. Cliquez ensuite sur la règle d’équilibrage de la charge de hello toosave OK.

    ![Ajout d’une règle d’équilibrage de charge](./media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

3. Créer des règles NAT entrantes

    Cliquez sur règles NAT entrantes sous la section de paramètres hello de votre équilibreur de charge. Dans hello nouveau panneau, cliquez sur **ajouter**. Nommez ensuite votre règle NAT entrante. Ici, elle s’appelle **inboundNATrule1**. destination de Hello doit être hello qu'adresse IP publique créée précédemment. Sélectionnez personnalisé sous le Service et sélectionnez le protocole hello toouse voulue. Ici, TCP est sélectionné. Entrez le port de hello, 3441 et hello port cible, dans ce cas, 3389. Cliquez sur OK toosave cette règle.

    Une fois que la première règle de hello est créé, répétez cette étape pour hello deuxième règle NAT entrante appelé inboundNATrule2 du port de tooTarget 3442 port 3389.

    ![Ajout d’une règle NAT entrante](./media/load-balancer-get-started-internet-portal/6-load-balancer-inbound-nat-rules.png)

## <a name="remove-a-load-balancer"></a>Supprimer un équilibreur de charge

toodelete un équilibreur de charge, sélectionnez hello équilibrage de charge tooremove. Bonjour *équilibrage de charge* panneau, cliquez sur **supprimer** situé en haut de hello du Panneau de hello. Puis sélectionnez **Oui** à l’invite.

## <a name="next-steps"></a>Étapes suivantes

[Prise en main de la configuration d’un équilibrage de charge interne](load-balancer-get-started-ilb-arm-cli.md)

[Configuration d'un mode de distribution d'équilibrage de charge](load-balancer-distribution-mode.md)

[Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)
