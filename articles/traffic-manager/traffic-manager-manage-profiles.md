---
title: "Gérer des profils Azure Traffic Manager | Microsoft Docs"
description: "Cet article vous aide à créer, désactiver, activer et supprimer un profil Azure Traffic Manager."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f06e0365-0a20-4d08-b7e1-e56025e64f66
ms.service: traffic-manager
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: kumud
ms.openlocfilehash: a5164282264124835692bc72a4ab61891aa7af9d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a>Gestion d’un profil Azure Traffic Manager

Les profils Traffic Manager permettent de contrôler la distribution du trafic vers les points de terminaison de votre site Web ou de vos services cloud selon des méthodes de routage du trafic. Cet article explique comment créer et gérer ces profils.

## <a name="create-a-traffic-manager-profile"></a>Créer un profil Traffic Manager

Vous pouvez créer un profil Traffic Manager à l’aide du portail Azure. Après avoir créé votre profil, vous pouvez configurer des points de terminaison, des analyses ainsi que d’autres paramètres dans le portail Azure. Traffic Manager prend en charge jusqu’à 200 points de terminaison par profil. Toutefois, la plupart des scénarios d’utilisation ne requièrent que peu de points de terminaison.

### <a name="to-create-a-traffic-manager-profile"></a>Pour créer un profil Traffic Manager

1. Dans un navigateur, connectez-vous au [portail Azure](http://portal.azure.com). Si vous ne possédez pas encore de compte, vous pouvez [vous inscrire pour bénéficier d’un essai gratuit d’un mois](https://azure.microsoft.com/free/). 
2. Dans le menu **Hub**, cliquez sur **Nouveau** > **Mise en réseau** > **Afficher tout**, cliquez sur le profil **Traffic Manager** pour ouvrir le panneau **Créer un profil Traffic Manager**, puis cliquez sur **Créer**.
3. Dans le panneau **Créer un profil Traffic Manager**, procédez comme suit :
    1. Sous **Nom**, entrez un nom pour votre profil. Ce nom doit être unique au sein de la zone trafficmanager.net et affiche le nom DNS <name>, trafficmanager.net, qui est utilisé pour accéder à votre profil Traffic Manager.
    2. Sous **Méthode de routage**, sélectionnez la méthode de routage **Priorité**.
    3. Sous **Abonnement**, sélectionnez l’abonnement pour lequel vous souhaitez créer ce profil.
    4. Sous **Groupe de ressources**, créez un groupe de ressources où placer ce profil.
    5. Sous **Emplacement du groupe de ressources**, sélectionnez l’emplacement du groupe de ressources. Ce paramètre fait référence à l’emplacement du groupe de ressources et n’a pas d’impact sur le profil Traffic Manager qui sera déployé globalement.
    6. Cliquez sur **Create**.
    7. Lorsque le déploiement global de votre profil Traffic Manager est terminé, il est répertorié comme l’une des ressources dans le groupe de ressources respectif.

## <a name="disable-enable-or-delete-a-profile"></a>Désactiver, activer ou supprimer un profil

Vous pouvez désactiver un profil existant afin que Traffic Manager ne renvoie pas les demandes utilisateur vers les points de terminaison configurés. Lorsque vous désactivez un profil Traffic Manager, le profil et les informations qu’il contient demeurent intacts et peuvent être modifiés via l’interface de Traffic Manager.  Les références sont rétablies lorsque vous réactivez le profil. Lorsque vous créez un profil Traffic Manager dans le portail Azure, il est automatiquement activé. Si un profil ne vous semble plus nécessaire, vous pouvez le supprimer.

### <a name="to-disable-a-profile"></a>Désactivation d’un profil

1. Si vous utilisez un nom de domaine personnalisé, modifiez l’enregistrement CNAME sur votre serveur DNS Internet afin qu’il ne pointe plus sur votre profil Traffic Manager.
2. Le trafic n’est alors plus dirigé vers les points de terminaison via les paramètres du profil Traffic Manager.
3. Dans un navigateur, connectez-vous au [portail Azure](http://portal.azure.com).
2. Dans la barre de recherche du portail, recherchez le nom du **profil Traffic Manager** que vous souhaitez modifier et cliquez sur le profil Traffic Manager dans les résultats affichés.
3. Dans le panneau du **profil Traffic Manager**, cliquez sur **Vue d’ensemble**, dans le panneau Vue d’ensemble, cliquez sur **Désactiver**, puis confirmez pour désactiver le profil Traffic Manager.

### <a name="to-enable-a-profile"></a>Activation d’un profil

1. Dans un navigateur, connectez-vous au [portail Azure](http://portal.azure.com).
2. Dans la barre de recherche du portail, recherchez le nom du **profil Traffic Manager** que vous souhaitez modifier et cliquez sur le profil Traffic Manager dans les résultats affichés.
3. Dans le panneau du **profil Traffic Manager**, cliquez sur **Vue d’ensemble**, puis dans le panneau Vue d’ensemble, cliquez sur **Activer**.
5. Si vous utilisez un nom de domaine personnalisé, créez un enregistrement de ressource CNAME sur votre serveur DNS Internet qui pointe sur le nom de domaine de votre profil Traffic Manager.
6. Le trafic est de nouveau dirigé vers les points de terminaison.

### <a name="to-delete-a-profile"></a>Suppression d’un profil

1. Assurez-vous que l’enregistrement de ressource DNS sur votre serveur DNS Internet n’utilise plus un enregistrement de ressource CNAME pointant vers le nom de domaine de votre profil Traffic Manager.
2. Dans la barre de recherche du portail, recherchez le nom du **profil Traffic Manager** que vous souhaitez modifier et cliquez sur le profil Traffic Manager dans les résultats affichés.
3. Dans le panneau du **profil Traffic Manager**, cliquez sur **Vue d’ensemble**, dans le panneau Vue d’ensemble, cliquez sur **Supprimer**, puis confirmez pour supprimer le profil Traffic Manager.

## <a name="next-steps"></a>Étapes suivantes

* [Ajout d’un point de terminaison](traffic-manager-endpoints.md)
* [Configurer la méthode de routage en fonction de la priorité](traffic-manager-configure-priority-routing-method.md)
* [Configurer la méthode de routage géographique](traffic-manager-configure-geographic-routing-method.md) 
* [Configurer la méthode de routage en fonction de la pondération](traffic-manager-configure-weighted-routing-method.md)
* [Configurer la méthode de routage basé sur les performances](traffic-manager-configure-performance-routing-method.md)
