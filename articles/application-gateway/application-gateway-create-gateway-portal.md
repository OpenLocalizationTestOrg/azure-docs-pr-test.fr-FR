---
title: "aaaCreate une passerelle d’Application - portail Azure | Documents Microsoft"
description: "Découvrez comment toocreate une passerelle d’Application à l’aide de hello portail"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 54dffe95-d802-4f86-9e2e-293f49bd1e06
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 24c1d5701eae372cd233162ceb58dea36a3b6a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-hello-portal"></a>Créer une passerelle d’application avec le portail de hello

[Application Gateway](application-gateway-introduction.md) est une appliance virtuelle dédiée qui intègre Application Delivery Controller (ADC) en tant que service, offrant diverses fonctionnalités d’équilibrage de charge de couche 7 pour votre application. Cet article passe en revue hello étapes toocreate une passerelle d’Application hello portail Azure et en ajoutant un serveur existant en tant que membre principal.

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Connectez-vous toohello portail Azure à l’adresse [http://portal.azure.com](http://portal.azure.com)

## <a name="create-application-gateway"></a>Créer une passerelle Application Gateway

toocreate une passerelle d’application, hello terminé les étapes qui suivent. La passerelle Application Gateway Azure requiert son propre sous-réseau. Lorsque vous créez un réseau virtuel, assurez-vous que vous laissez suffisamment toohave d’espace adresse plusieurs sous-réseaux. Une fois déployée tooa sous-réseau, passerelle d’application hello uniquement autres passerelles d’application peuvent être ajoutés tooit.

1. Dans le volet de favoris hello du portail de hello, cliquez sur **nouveau**
1. Bonjour **nouveau** panneau, cliquez sur **réseau**. Bonjour **réseau** panneau, cliquez sur **Application Gateway**, comme indiqué dans hello suivant image :

    ![Création d’une passerelle Application Gateway][1]

1. Bonjour **notions de base** panneau qui s’affiche, entrez hello valeurs suivantes, puis cliquez sur **OK**:

   | **Paramètre** | **Valeur** | **Détails**|
   |---|---|---|
   |**Nom**|AdatumAppGateway|nom de Hello de passerelle d’application hello|
   |**Niveau**|Standard|Les valeurs disponibles sont Standard et WAF. Visitez [pare-feu d’applications web](application-gateway-web-application-firewall-overview.md) toolearn plus WAF.|
   |**Taille de la référence (SKU)**|Moyenne|Si vous sélectionnez le niveau Standard, vous avez le choix entre Petite, Moyenne et Grande. Si vous choisissez le niveau WAF, les options sont limitées à Moyenne et Grande.|
   |**Nombre d’instances**|2|Nombre d’instances de la passerelle d’application hello pour la haute disponibilité. Un nombre d’instances de 1 doit être utilisé uniquement à des fins de test.|
   |**Abonnement**|[Votre abonnement]|Sélectionnez une passerelle d’application abonnement toocreate hello dans.|
   |**Groupe de ressources**|**Créer un nouveau :** AdatumAppGatewayRG|Créez un groupe de ressources. nom de groupe de ressources Hello doit être unique au sein de l’abonnement hello sélectionné. toolearn plus d’informations sur les groupes de ressources, lire hello [le Gestionnaire de ressources](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) l’article de vue d’ensemble.|
   |**Emplacement**|Ouest des États-Unis||

1. Bonjour **paramètres** panneau s’affiche sous **réseau virtuel**, cliquez sur **choisir un réseau virtuel**. Hello **réseau virtuel de choisir** panneau s’ouvre.  Cliquez sur **nouvel** tooopen hello **créer un réseau virtuel** panneau.

   ![choisir un réseau virtuel][2]

1. Sur hello **Panneau de réseau virtuel créer** , puis entrez les valeurs suivantes de hello **OK**. Hello **créer un réseau virtuel** et **réseau virtuel de choisir** panneaux ferme. Cette étape remplit hello **sous-réseau** champ hello **paramètres** panneau avec sous-réseau hello choisi.

   | **Paramètre** | **Valeur** | **Détails**|
   |---|---|---|
   |**Nom**|AdatumAppGatewayVNET|Nom de la passerelle d’application hello|
   |**Espace d’adressage**|10.0.0.0/16|Il s’agit d’espace d’adressage hello pour le réseau virtuel de hello|
   |**Nom du sous-réseau**|AppGatewaySubnet|Nom du sous-réseau de hello pour la passerelle d’application hello|
   |**Plage d’adresses de sous-réseau**|10.0.0.0/28|Ce sous-réseau permet à d’autres sous-réseaux supplémentaires dans le réseau virtuel de hello pour les membres du pool principal|

1. Sur hello **paramètres** panneau sous **configuration Frontend IP**, choisissez **Public** comme hello **type d’adresse IP**

1. Sur hello **paramètres** panneau sous **adresse IP publique** cliquez sur **choisir une adresse IP publique**, hello **choisir une adresse IP publique** panneau s’ouvre. , cliquez sur **nouvel**.

   ![choisir une adresse ip publique][3]

1. Sur hello **créer une adresse IP publique** panneau, acceptez la valeur par défaut de hello, puis cliquez sur **OK**. Panneau de Hello se ferme et remplit hello **adresse IP publique** avec l’adresse IP publique hello choisi.

1. Sur hello **paramètres** panneau sous **configuration de l’écouteur**, cliquez sur **HTTP** sous **protocole**. Entrez hello port toouse Bonjour **Port** champ.

2. Cliquez sur **OK** sur hello **paramètres** toocontinue du panneau.

1. Passez en revue les paramètres hello sur hello **Résumé** panneau, cliquez sur **OK** toostart la création de la passerelle d’application hello. Création d’une passerelle d’application est une tâche de longue durée et prend du temps toocomplete.

## <a name="add-servers-toobackend-pools"></a>Ajouter des serveurs toobackend pools

Une fois que vous créez la passerelle d’application hello, les systèmes de hello qui hébergent hello application toobe équilibrée doivent toujours passerelle d’application toobe toohello ajouté. les adresses IP Hello, nom de domaine complet, ou deux cartes réseau de ces serveurs sont ajoutés toohello principaux des pools d’adresses.

### <a name="ip-address-or-fqdn"></a>Adresse IP ou nom de domaine complet

1. Avec la passerelle d’application hello créée, Bonjour Azure portal **favoris** volet, cliquez sur **toutes les ressources**. Cliquez sur hello **AdatumAppGateway** passerelle d’application dans hello toutes les lames de ressources. Si l’abonnement hello déjà sélectionné comporte plusieurs ressources, vous pouvez entrer **AdatumAppGateway** Bonjour **filtrer par nom...** passerelle d’application hello boîte tooeasily accès.

1. passerelle d’application Hello que vous avez créé s’affiche. Cliquez sur **pools principaux**, puis sélectionnez le pool principal en cours de hello **appGatewayBackendPool**, hello **appGatewayBackendPool** panneau s’ouvre.

   ![Pools principaux Application Gateway][4]

1. Cliquez sur **ajouter une cible** tooadd les adresses IP des valeurs de nom de domaine complet. Choisissez **IP adresse ou le nom de domaine complet** comme hello **Type** et entrez votre adresse IP ou le nom de domaine complet dans le champ de hello. Répétez cette étape pour les autres membres du pool principal. Une fois que vous avez terminé, cliquez sur **Enregistrer**.

### <a name="virtual-machine-and-nic"></a>Machine virtuelle et carte d’interface réseau

Vous pouvez également ajouter des cartes d’interface réseau de machine virtuelle en tant que membres de pool principal. Seuls les ordinateurs virtuels au sein du même réseau virtuel que hello passerelle d’Application sont disponibles par le biais de hello hello la liste déroulante.

1. Avec la passerelle d’application hello créée, Bonjour Azure portal **favoris** volet, cliquez sur **toutes les ressources**. Cliquez sur hello **AdatumAppGateway** passerelle d’application dans hello toutes les lames de ressources. Si l’abonnement hello déjà sélectionné comporte plusieurs ressources, vous pouvez entrer **AdatumAppGateway** Bonjour **filtrer par nom...** passerelle d’application hello boîte tooeasily accès.

1. passerelle d’application Hello que vous avez créé s’affiche. Cliquez sur **pools principaux**, puis sélectionnez le pool principal en cours de hello **appGatewayBackendPool**, hello **appGatewayBackendPool** panneau s’ouvre.

   ![Pools principaux Application Gateway][5]

1. Cliquez sur **ajouter une cible** tooadd les adresses IP des valeurs de nom de domaine complet. Choisissez **virtuels** comme hello **Type** et sélectionnez virtuels hello et toouse de carte réseau. Une fois que vous avez terminé, cliquez sur **Enregistrer**.

   > [!NOTE]
   > Seuls les ordinateurs virtuels dans hello même réseau virtuel comme passerelle d’application hello sont disponibles dans la zone déroulante hello.

## <a name="clean-up-resources"></a>Supprimer des ressources

Si n’est plus nécessaire, supprimer le groupe de ressources hello, la passerelle d’application et toutes les ressources associées. toodo, sélectionnez groupe de ressources hello dans Panneau de passerelle d’application hello et cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Dans ce scénario, vous déployé une passerelle d’application et ajouté un serveur toohello de serveur principal. les étapes suivantes Hello sont la passerelle d’application hello tooconfigure par modification des paramètres et des règles d’ajustements dans la passerelle de hello. Vous trouverez ces étapes en visitant hello suivant des articles :

Découvrez comment des sondes toocreate d’état personnalisé en vous rendant sur [créer une sonde d’intégrité personnalisé](application-gateway-create-probe-portal.md)

Découvrez comment tooconfigure déchargement SSL et le déchiffrement SSL coûteux take hello désactivé vos serveurs web en vous rendant sur [configurer le déchargement SSL](application-gateway-ssl-portal.md)

Découvrez comment tooprotect vos applications avec [pare-feu d’applications Web](application-gateway-webapplicationfirewall-overview.md) une fonctionnalité de passerelle d’application.

<!--Image references-->
[1]: ./media/application-gateway-create-gateway-portal/figure1.png
[2]: ./media/application-gateway-create-gateway-portal/figure2.png
[3]: ./media/application-gateway-create-gateway-portal/figure3.png
[4]: ./media/application-gateway-create-gateway-portal/figure4.png
[5]: ./media/application-gateway-create-gateway-portal/figure5.png
[scenario]: ./media/application-gateway-create-gateway-portal/scenario.png
