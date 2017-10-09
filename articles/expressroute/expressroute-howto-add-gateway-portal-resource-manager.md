---
title: "Ajouter un tooa de passerelle de réseau virtuel réseau virtuel pour ExpressRoute : portail : Azure | Documents Microsoft"
description: "Cet article vous explique comment ajouter un tooan de passerelle de réseau virtuel déjà créé VNet Gestionnaire de ressources pour ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: cherylmc
ms.openlocfilehash: 9e922af1f3676eeebc569b57c3ae3a22d4e0b395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-hello-azure-portal"></a>Configurer une passerelle de réseau virtuel pour ExpressRoute à l’aide de hello portail Azure
> [!div class="op_single_selector"]
> * [Resource Manager - Portail Azure](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Classic - PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Vidéo - portail Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

Cet article vous guide dans les étapes de hello tooadd une passerelle de réseau virtuel pour un réseau virtuel existant. Cet article vous guide tout au long des hello étapes tooadd, redimensionner et supprimer une passerelle de réseau virtuel (VNet) pour un réseau virtuel existant. étapes de Hello pour cette configuration sont spécifiquement pour les réseaux virtuels qui ont été créés à l’aide du modèle de déploiement de gestionnaire de ressources hello qui sera utilisé dans une configuration ExpressRoute. Pour plus d’informations sur les passerelles de réseau virtuel et les paramètres de configuration de passerelle pour ExpressRoute, consultez [À propos des passerelles de réseau virtuel pour ExpressRoute](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Avant tout chose

étapes Hello pour cette tâche, utilisez un réseau virtuel en fonction des valeurs hello hello suivant liste de référence de configuration. Nous utilisons cette liste dans notre exemple de procédure. Vous pouvez copier hello liste toouse en tant que référence, en remplaçant les valeurs hello par les vôtres.

**Liste de référence de configuration**

* Nom du réseau virtuel : « TestVNet »
* Espace d’adressage du réseau virtuel : 192.168.0.0/16
* Nom du sous-réseau : « FrontEnd » 
    * Espace d’adressage du sous-réseau : « 192.168.1.0/24 »
* Groupe de ressources : « TestRG »
* Emplacement = « Est des États-Unis »
* Nom de sous-réseau de passerelle : « GatewaySubnet » Vous devez toujours nommer un sous-réseau de passerelle *GatewaySubnet*.
    * Espace d'adressage du sous-réseau de passerelle : « 192.168.200.0/26 »
* Nom de la passerelle : « ERGW »
* Nom d’adresse IP de la passerelle : « MyERGWVIP »
* Type de passerelle : « ExpressRoute ». Ce type est requis pour une configuration ExpressRoute.
* Nom d’adresse IP publique de passerelle = « MyERGWVIP »

Vous pouvez afficher une [vidéo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network) de ces étapes avant de commencer votre configuration.

## <a name="create-hello-gateway-subnet"></a>Créez le sous-réseau de passerelle hello

1. Bonjour [portal](http://portal.azure.com), parcourir le réseau virtuel du Gestionnaire de ressources toohello pour lequel vous souhaitez toocreate une passerelle de réseau virtuel.
2. Bonjour **paramètres** section du Panneau de votre réseau virtuel, cliquez sur **sous-réseaux** Panneau de sous-réseaux tooexpand hello.
3. Sur hello **sous-réseaux** panneau, cliquez sur **+ sous-réseau de passerelle** tooopen hello **ajouter un sous-réseau** panneau. 
   
    ![Ajouter un sous-réseau de passerelle hello](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "ajouter un sous-réseau de passerelle hello")


4. Hello **nom** pour votre sous-réseau est automatiquement renseigné avec hello valeur « GatewaySubnet ». Cette valeur est requise dans l’ordre pour le sous-réseau de hello toorecognize Azure que le sous-réseau de passerelle hello. Ajuster hello automatiquement renseigné **plage d’adresses** valeurs toomatch la configuration requise. Nous vous recommandons de créer un sous-réseau de passerelle avec /27 ou plus (/26, /25, etc.). Ensuite, cliquez sur **OK** toosave hello valeurs et créer le sous-réseau de passerelle hello.

    ![Ajout du sous-réseau de hello](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "Ajout hello sous-réseau")

## <a name="create-hello-virtual-network-gateway"></a>Créer une passerelle de réseau virtuel hello

1. Dans le portail hello, sur le côté gauche de hello, cliquez sur  **+**  et type de passerelle de réseau virtuel dans la recherche. Recherchez **passerelle de réseau virtuel** dans la recherche de hello retourner et cliquez sur entrée de hello. Sur hello **passerelle de réseau virtuel** panneau, cliquez sur **créer** bas hello du Panneau de hello. Cette opération ouvre hello **créer une passerelle réseau virtuelle** panneau.
2. Sur hello **créer une passerelle réseau virtuelle** panneau, renseignez les valeurs hello pour votre passerelle de réseau virtuel.

    ![Champs du panneau Créer une passerelle de réseau virtuel](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "Champs du panneau Créer une passerelle de réseau virtuel")
3. **Nom** : nommez votre passerelle. Cela n’est pas hello identique à un sous-réseau de passerelle d’affectation de noms. Il s’agit de nom hello d’objet hello passerelle que vous créez.
4. **Type de passerelle** : sélectionnez **ExpressRoute**.
5. **Référence (SKU)**: passerelle hello sélectionnez référence (SKU) à partir de la liste déroulante de hello.
6. **Emplacement**: ajuster hello **emplacement** champ toopoint toohello emplacement de votre réseau virtuel. Si l’emplacement de hello ne pointe pas toohello la région où se trouve votre réseau virtuel, réseau virtuel de hello n’apparaît pas dans la liste déroulante de hello 'Sélectionner un réseau virtuel'.
7. Choisissez toowhich de réseau virtuel hello vous voulez tooadd cette passerelle. Cliquez sur **réseau virtuel** tooopen hello **choisir un réseau virtuel** panneau. Sélectionnez hello réseau virtuel. Si vous ne voyez pas votre réseau virtuel, vérifiez que hello **emplacement** champ pointe toohello la région dans lequel se trouve votre réseau virtuel.
9. Définissez une adresse IP publique. Cliquez sur **adresse IP publique** tooopen hello **choisir une adresse IP publique** panneau. Cliquez sur **+ créer de nouveaux** tooopen hello **lame adresse IP publique de créer**. Donnez à un nom à votre adresse IP publique. Ce panneau crée un public toowhich d’objet d’adresse IP qu'une adresse IP publique sera affectée dynamiquement. Cliquez sur **OK** toosave votre panneau toothis de modifications.
10. **Abonnement**: Vérifiez que hello correct d’abonnement est sélectionné.
11. **Groupe de ressources**: ce paramètre est déterminé par hello réseau virtuel que vous sélectionnez.
12. Ne pas ajuster hello **emplacement** après avoir spécifié les paramètres précédents hello.
13. Vérifiez les paramètres de hello. Si vous souhaitez que votre tooappear passerelle sur le tableau de bord hello, vous pouvez sélectionner **toodashboard du code confidentiel** bas hello du Panneau de hello.
14. Cliquez sur **créer** toobegin création hello passerelle. paramètres de Hello sont validés et déploie de passerelle de hello. Création de passerelle de réseau virtuel peut prendre jusqu'à too45 minutes toocomplete.

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous avez créé la passerelle de réseau virtuel hello, vous pouvez lier votre réseau virtuel de tooan circuit ExpressRoute. Consultez [lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-portal-resource-manager.md).
