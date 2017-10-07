---
title: "Ajouter plusieurs tooa connexions de passerelle Site-à-Site VPN réseau virtuel : portail Azure : le Gestionnaire de ressources | Documents Microsoft"
description: "Ajouter plusieurs S2S connexions tooa passerelle VPN de site qui dispose d’une connexion existante"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a>Ajouter un tooa de connexion de Site à Site réseau virtuel avec une connexion de passerelle VPN existante

> [!div class="op_single_selector"]
> * [Portail Azure](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (classique)](vpn-gateway-multi-site.md)
>
> 

Cet article vous guide tout au long de l’aide de hello tooadd portail Azure Site à Site (S2S) connexions tooa passerelle VPN qui dispose d’une connexion existante. Ce type de connexion est souvent tooas auxquels une configuration de « multisite ». Vous pouvez ajouter un tooa de connexion réseau virtuel qui possède déjà un S2S connexion, une connexion Point à Site ou un réseau à connexion S2S. L’ajout de connexions est soumis à certaines limitations. Vérifiez hello [avant de commencer](#before) section dans cette tooverify article avant de commencer votre configuration. 

Cet article s’applique tooVNets créé à l’aide du modèle de déploiement du Gestionnaire de ressources hello qui ont une passerelle VPN de RouteBased. Ces étapes ne s’appliquent pas à la configuration des connexions coexistence tooExpressRoute/Site à Site. Consultez l’article [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) (Connexions coexistantes ExpressRoute/S2S) pour en savoir plus sur les connexions coexistantes.

### <a name="deployment-models-and-methods"></a>Outils et modèles de déploiement
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Nous mettons à jour ce tableau à mesure que de nouveaux articles et des outils supplémentaires sont disponibles pour cette configuration. Quand un article est disponible, nous lier directement tooit à partir de cette table.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="before"></a>Avant de commencer
Vérifiez que hello éléments suivants :

* Vous ne créez pas de connexion coexistante ExpressRoute/S2S.
* Vous avez un réseau virtuel qui a été créé à l’aide du modèle de déploiement du Gestionnaire de ressources hello avec une connexion existante.
* passerelle de réseau virtuel Hello pour votre réseau virtuel est RouteBased. Si vous avez une passerelle VPN de PolicyBased, vous devez supprimer la passerelle de réseau virtuel hello et créer une passerelle VPN en tant que RouteBased.
* Aucune des plages d’adresses hello se chevauchent pour une des hello ce réseau virtuel se connecte à des réseaux virtuels.
* Vous avez le périphérique VPN compatible et une personne qui est en mesure de tooconfigure il. Consultez [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md). Si vous n’êtes pas familiarisé avec la configuration de votre périphérique VPN, ou vous n’êtes pas familiarisé avec les plages d’adresses IP hello situés dans la configuration de votre réseau local, vous devez toocoordinate avec une personne qui peut fournir ces informations pour vous.
* Vous disposez d’une adresse IP publique exposée en externe pour votre périphérique VPN. Cette adresse IP ne peut pas se trouver derrière un NAT.

## <a name="part1"></a>Partie 1 - Configuration d’une connexion
1. À partir d’un navigateur, accédez à toohello [portail Azure](http://portal.azure.com) et, si nécessaire, connectez-vous à votre compte Azure.
2. Cliquez sur **toutes les ressources** et recherchez votre **passerelle de réseau virtuel** à partir de la liste de hello des ressources, cliquez dessus.
3. Sur hello **passerelle de réseau virtuel** panneau, cliquez sur **connexions**.
   
    ![Panneau Connexions](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Panneau Connexions")<br>
4. Sur hello **connexions** panneau, cliquez sur **+ ajouter**.
   
    ![Bouton de connexion ajouter](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "bouton Ajouter la connexion")<br>
5. Sur hello **ajouter une connexion** panneau, remplissez hello champs qui suivent :
   
   * **Nom :** nom hello toogive toohello site que vous créez connexion hello.
   * **Type de connexion** : sélectionnez **Site à site (IPSec)**.
     
     ![Panneau de connexion ajouter](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Panneau de connexion ajouter")<br>

## <a name="part2"></a>Partie 2 - Ajout d’une passerelle de réseau local
1. Cliquez sur **Passerelle de réseau local** ***Choisir une passerelle de réseau local***. Cela ouvre hello **passerelle de réseau local choisir** panneau.
   
    ![Passerelle de réseau local choisir](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "passerelle de réseau local choisir")<br>
2. Cliquez sur **nouvel** tooopen hello **créer une passerelle réseau local** panneau.
   
    ![Panneau de passerelle de réseau local de créer](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "créer une passerelle réseau local")<br>
3. Sur hello **créer une passerelle réseau local** panneau, remplissez hello champs qui suivent :
   
   * **Nom :** hello nom de ressource de la passerelle toogive toohello réseau local.
   * **Adresse IP :** hello adresse IP publique du périphérique VPN de hello sur site hello que vous souhaitez tooconnect à.
   * **L’espace d’adressage :** l’espace d’adressage que vous souhaitez toobe hello routé toohello nouveau site de réseau local.
4. Cliquez sur **OK** sur hello **créer une passerelle réseau local** modifications de panneau toosave hello.

## <a name="part3"></a>Partie 3 : ajouter la clé partagée de hello et créer la connexion de hello
1. Sur hello **ajouter une connexion** panneau, ajouter la clé partagée de hello que vous souhaitez toouse toocreate votre connexion. Vous pouvez soit obtenir la clé partagée de hello à partir de votre périphérique VPN, ou créer un ici, puis configurer votre hello toouse du périphérique VPN même clé partagée. Hello important est que les clés de hello sont exactement hello identiques.
   
    ![Clé partagée](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Clé partagée")<br>
2. Au bas de hello du Panneau de hello, cliquez sur **OK** connexion de hello toocreate.

## <a name="part4"></a>Partie 4 : vérifier la connexion VPN hello


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a>Étapes suivantes

Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels. Consultez les machines virtuelles de hello [cursus](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) pour plus d’informations.
