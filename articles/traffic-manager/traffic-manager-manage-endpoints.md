---
title: points de terminaison aaaManage dans Azure Traffic Manager | Documents Microsoft
description: "Cet article vous aide à ajouter, supprimer, activer et désactiver des points de terminaison d’Azure Traffic Manager."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: ade2bbc2-35a7-43c5-8001-4698f7254526
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kumud
ms.openlocfilehash: fc65874ae2eaeb6fca5d8c4f33403c258307bdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-disable-enable-or-delete-endpoints"></a>Ajouter, désactiver, activer ou supprimer des points de terminaison

fonctionnalité des applications Web Hello dans Azure App Service fournit déjà le basculement et les fonctionnalités de routage du trafic de tourniquet pour les sites Web au sein d’un centre de données, quel que soit le mode de site Web hello. Azure Traffic Manager vous permet de toospecify basculement et le routage du trafic de tourniquet pour les services de cloud et sites Web dans différents centres de données. Hello première étape nécessaire tooprovide fonctionne tooadd hello cloud service ou le site Web du point de terminaison tooTraffic Manager.

Vous pouvez également désactiver des points de terminaison individuels qui font partie d'un profil Traffic Manager. Points de terminaison restent dans le cadre du profil de hello, mais le profil de hello se comporte comme si le point de terminaison hello n’est pas inclus dans il. Cette action s’avère utile pour supprimer temporairement un point de terminaison en mode de maintenance ou redéployé. Une fois le point de terminaison hello à nouveau opérationnel, il peut être activé.

> [!NOTE]
> La désactivation d’un point de terminaison est indépendante toodo état de son déploiement dans Azure. Un point de terminaison intègre reste opérationnel et en mesure de trafic tooreceive même s’il est désactivé dans Traffic Manager. En outre, le fait de désactiver un point de terminaison dans un profil n'affecte pas son statut dans un autre profil.

## <a name="tooadd-a-cloud-service-or-an-app-service-endpoint-tooa-traffic-manager-profile"></a>tooadd un service cloud ou un tooa de point de terminaison de service application profil Traffic Manager

1. À partir d’un navigateur, connectez-vous toohello [portail Azure](http://portal.azure.com).
2. Dans la barre de recherche du portail hello, recherchez hello **profil Traffic Manager** nom que vous souhaitez toomodify, puis cliquez sur le profil Traffic Manager hello Bonjour que hello affichée des résultats.
3. Bonjour **profil Traffic Manager** panneau, Bonjour **paramètres** , cliquez sur **points de terminaison**.
4. Bonjour **points de terminaison** panneau s’affiche, cliquez sur **ajouter**.
5. Bonjour **ajouter le point de terminaison** panneau, terminée, comme suit :
    1. Sous **Type**, cliquez sur **Point de terminaison Azure**.
    2. Fournir un **nom** en fonction duquel vous voulez toorecognize ce point de terminaison.
    3. Pour **cibler un type de ressource**, à partir de hello de liste déroulante, choisissez le type de ressource approprié hello.
    4. Pour **ressource cible**, à partir de hello de liste déroulante, sélectionnez une ressource cible appropriée hello tooshow hello liste ressources hello même abonnement Bonjour **panneau des ressources**. Bonjour **ressource** panneau s’affiche, service hello de choix que vous souhaitez tooadd comme hello du premier point de terminaison.
    5. Pour **Priorité**, sélectionnez **1**. Ainsi, tout le trafic entrant de point de terminaison toothis si elle est sain.
    6. Vérifiez que la case **Ajouter comme désactivé** est désélectionnée.
    7. Cliquez sur **OK**
6.  Répétez les étapes 4 et 5 tooadd hello prochain point de terminaison Azure. Assurez-vous que tooadd avec sa **priorité** à la valeur **2**.
7.  Lors de l’ajout de hello de deux points de terminaison est terminée, ils sont affichés dans hello **profil Traffic Manager** panneau, ainsi que leur état d’analyse en tant que **Online**.

> [!NOTE]
> Une fois que vous ajoutez ou supprimez un point de terminaison à partir d’un profil à l’aide de hello *basculement* méthode de routage de trafic, la liste prioritaire de basculement hello ils pas peuvent être classés comme vous le souhaitez. Vous pouvez ajuster l’ordre hello Hello liste prioritaire de basculement sur la page de Configuration hello. Pour plus d’informations, consultez la rubrique [Configurer le routage du trafic par basculement](traffic-manager-configure-failover-routing-method.md).

## <a name="toodisable-an-endpoint"></a>toodisable un point de terminaison

1. À partir d’un navigateur, connectez-vous toohello [portail Azure](http://portal.azure.com).
2. Dans la barre de recherche du portail hello, recherchez hello **profil Traffic Manager** nom que vous souhaitez toomodify, puis cliquez sur le profil Traffic Manager hello dans les résultats de hello sont affichés.
3. Bonjour **profil Traffic Manager** panneau, Bonjour **paramètres** , cliquez sur **points de terminaison**. 
4. Cliquez sur le point de terminaison hello que vous souhaitez toodisable, puis sous hello **point de terminaison** panneau s’affiche, cliquez sur **modifier**.
5. Bonjour **point de terminaison** panneau, changent d’état du point de terminaison hello**désactivé**, puis cliquez sur **enregistrer**.
6. Les clients continuent de point de terminaison toohello toosend le trafic pendant hello Time-to-Live (TTL). Vous pouvez modifier hello durée de vie de page de Configuration hello Hello profil Traffic Manager.

## <a name="tooenable-an-endpoint"></a>tooenable un point de terminaison

1. À partir d’un navigateur, connectez-vous toohello [portail Azure](http://portal.azure.com).
2. Dans la barre de recherche du portail hello, recherchez hello **profil Traffic Manager** nom que vous souhaitez toomodify, puis cliquez sur le profil Traffic Manager hello dans les résultats de hello sont affichés.
3. Bonjour **profil Traffic Manager** panneau, Bonjour **paramètres** , cliquez sur **points de terminaison**. 
4. Cliquez sur le point de terminaison hello que vous souhaitez toodisable, puis sous hello **point de terminaison** panneau s’affiche, cliquez sur **modifier**.
5. Bonjour **point de terminaison** panneau, changent d’état du point de terminaison hello**activé**, puis cliquez sur **enregistrer**.
6. Les clients continuent de point de terminaison toohello toosend le trafic pendant hello Time-to-Live (TTL). Vous pouvez modifier hello durée de vie de page de Configuration hello Hello profil Traffic Manager.

## <a name="toodelete-an-endpoint"></a>toodelete un point de terminaison

1. À partir d’un navigateur, connectez-vous toohello [portail Azure](http://portal.azure.com).
2. Dans la barre de recherche du portail hello, recherchez hello **profil Traffic Manager** nom que vous souhaitez toomodify, puis cliquez sur le profil Traffic Manager hello dans les résultats de hello sont affichés.
3. Bonjour **profil Traffic Manager** panneau, Bonjour **paramètres** , cliquez sur **points de terminaison**. 
4. Cliquez sur le point de terminaison hello que vous souhaitez toodisable, puis sous hello **point de terminaison** panneau s’affiche, cliquez sur **modifier**.
5. Bonjour **point de terminaison** panneau, changent d’état du point de terminaison hello**activé**, puis cliquez sur **enregistrer**.


## <a name="next-steps"></a>Étapes suivantes

* [Gérer des profils Traffic Manager](traffic-manager-manage-profiles.md)
* [Configurer des méthodes de routage](traffic-manager-configure-routing-method.md)
* [Résolution des problèmes liés à l’état Détérioré de Traffic Manager](traffic-manager-troubleshooting-degraded.md)
* [Considérations sur les performances de Traffic Manager](traffic-manager-performance-considerations.md)
* [Opérations sur Traffic Manager (Référence sur l’API REST)](http://go.microsoft.com/fwlink/p/?LinkID=313584)

