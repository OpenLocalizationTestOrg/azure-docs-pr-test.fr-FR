---
title: les profils Azure Traffic Manager aaaManage | Documents Microsoft
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
ms.openlocfilehash: 0c6ab0c451581d039514a9de0b525b3937e45a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a>Gestion d’un profil Azure Traffic Manager

Profils Traffic Manager utilisent le routage du trafic méthodes toocontrol hello distribution services de cloud computing tooyour trafic ou des points de terminaison de site Web. Cet article explique comment toocreate et gérer ces profils.

## <a name="create-a-traffic-manager-profile"></a>Créer un profil Traffic Manager

Vous pouvez créer un profil Traffic Manager à l’aide de hello portail Azure. Après avoir créé votre profil, vous pouvez configurer des points de terminaison, la surveillance et les autres paramètres Bonjour portail Azure. Traffic Manager prend en charge des points de terminaison too200 par profil. Toutefois, la plupart des scénarios d’utilisation ne requièrent que peu de points de terminaison.

### <a name="toocreate-a-traffic-manager-profile"></a>toocreate un profil Traffic Manager

1. À partir d’un navigateur, connectez-vous toohello [portail Azure](http://portal.azure.com). Si vous ne possédez pas encore de compte, vous pouvez [vous inscrire pour bénéficier d’un essai gratuit d’un mois](https://azure.microsoft.com/free/). 
2. Sur hello **Hub** menu, cliquez sur **nouveau** > **réseau** > **afficher tous les**, cliquez sur **le trafic Gestionnaire de** hello tooopen de profil **profil créer Traffic Manager** panneau, puis cliquez sur **créer**.
3. Sur hello **profil créer Traffic Manager** panneau, terminée, comme suit :
    1. Sous **Nom**, entrez un nom pour votre profil. Ce nom doit toobe unique au sein de la zone de trafficmanager.net hello et entraîne le nom DNS de hello <name>, trafficmanager.net, qui est utilisé tooaccess votre profil Traffic Manager.
    2. Dans **méthode de routage**, sélectionnez hello **priorité** méthode de routage.
    3. Dans **abonnement**, sélectionnez hello abonnement toocreate ce profil sous
    4. Dans **groupe de ressources**, créez un nouveau tooplace de groupe de ressources ce profil sous.
    5. Dans **emplacement du groupe de ressources**, sélectionnez l’emplacement hello hello du groupe de ressources. Ce paramètre fait référence emplacement toohello hello du groupe de ressources et n’a aucun impact sur hello profil Traffic Manager qui sera déployé globalement.
    6. Cliquez sur **Créer**.
    7. Lorsque le déploiement global de hello de votre profil Traffic Manager est terminée, il est répertorié dans le groupe de ressources respectives comme l’une des ressources de hello.

## <a name="disable-enable-or-delete-a-profile"></a>Désactiver, activer ou supprimer un profil

Vous pouvez désactiver un profil existant afin de Traffic Manager ne référence pas de points de terminaison toohello configuré de requêtes utilisateur. Lorsque vous désactivez un profil Traffic Manager, le profil de hello et informations hello contenue dans le profil de hello restent intacts et peuvent être modifiées dans l’interface de Traffic Manager hello.  Les redirections de reprendre lorsque vous réactivez le profil de hello. Lorsque vous créez un profil Traffic Manager Bonjour portail Azure, il est automatiquement activé. Si un profil ne vous semble plus nécessaire, vous pouvez le supprimer.

### <a name="toodisable-a-profile"></a>toodisable un profil

1. Si vous utilisez un nom de domaine personnalisé, modifiez enregistrement CNAME de hello sur votre serveur DNS Internet pour qu’il pointe ne sont plus tooyour du profil Traffic Manager.
2. En cours d’arrêt du trafic dirigé toohello de points de terminaison via les paramètres du profil Traffic Manager hello.
3. À partir d’un navigateur, connectez-vous toohello [portail Azure](http://portal.azure.com).
2. Dans la barre de recherche du portail hello, recherchez hello **profil Traffic Manager** nom que vous souhaitez toomodify, puis cliquez sur le profil Traffic Manager hello Bonjour que hello affichée des résultats.
3. Bonjour **profil Traffic Manager** panneau, cliquez sur **vue d’ensemble**, dans le panneau de vue d’ensemble de hello, cliquez sur **désactiver**, puis confirmez le profil Traffic Manager toodisable hello.

### <a name="tooenable-a-profile"></a>tooenable un profil

1. À partir d’un navigateur, connectez-vous toohello [portail Azure](http://portal.azure.com).
2. Dans la barre de recherche du portail hello, recherchez hello **profil Traffic Manager** nom que vous souhaitez toomodify, puis cliquez sur le profil Traffic Manager hello Bonjour que hello affichée des résultats.
3. Bonjour **profil Traffic Manager** panneau, cliquez sur **vue d’ensemble**, puis dans le panneau de vue d’ensemble de hello cliquez sur **activer**.
5. Si vous utilisez un nom de domaine personnalisé, créez un enregistrement de ressource CNAME sur votre nom de domaine DNS Internet server toopoint toohello de votre profil Traffic Manager.
6. Le trafic est dirigé toohello de points de terminaison à nouveau.

### <a name="toodelete-a-profile"></a>toodelete un profil

1. Assurez-vous qu’enregistrement de ressource DNS hello sur votre serveur DNS Internet n’utilise plus un enregistrement de ressource CNAME qui pointe le nom de domaine toohello de votre profil Traffic Manager.
2. Dans la barre de recherche du portail hello, recherchez hello **profil Traffic Manager** nom que vous souhaitez toomodify, puis cliquez sur le profil Traffic Manager hello Bonjour que hello affichée des résultats.
3. Bonjour **profil Traffic Manager** panneau, cliquez sur **vue d’ensemble**, dans le panneau de vue d’ensemble de hello, cliquez sur **supprimer**, puis confirmez le profil Traffic Manager toodelete hello.

## <a name="next-steps"></a>Étapes suivantes

* [Ajout d’un point de terminaison](traffic-manager-endpoints.md)
* [Configurer la méthode de routage en fonction de la priorité](traffic-manager-configure-priority-routing-method.md)
* [Configurer la méthode de routage géographique](traffic-manager-configure-geographic-routing-method.md) 
* [Configurer la méthode de routage en fonction de la pondération](traffic-manager-configure-weighted-routing-method.md)
* [Configurer la méthode de routage basé sur les performances](traffic-manager-configure-performance-routing-method.md)
