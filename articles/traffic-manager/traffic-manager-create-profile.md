---
title: aaaCreate un profil Traffic Manager dans Azure | Documents Microsoft
description: "Cet article décrit comment toocreate un profil Traffic Manager"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: kumud
ms.openlocfilehash: 5cd3d2903552c9a0427da41a73f6f38f6b0afc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-traffic-manager-profile"></a>Créer un profil Traffic Manager

Cet article décrit comment un profil avec **priorité** type de routage peut être créé de points de terminaison Azure Web Apps tooroute utilisateurs tootwo. À l’aide de hello **priorité** type de routage, tout le trafic est routé toohello le premier point de terminaison pendant hello est ensuite conserver sous la forme d’une sauvegarde. Par conséquent, les utilisateurs peuvent être routés toohello le deuxième point de terminaison si le premier point de terminaison hello devient non intègre.

Dans cet article, deux points de terminaison de l’application Web Azure créés précédemment sont le profil Traffic Manager toothis associé qui vient d’être créé. toolearn plus sur la façon de points de terminaison toocreate application Web Azure, visitez hello [page de documentation Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/). Vous pouvez ajouter n’importe quel point de terminaison a un nom DNS et est accessible via hello internet public et que nous utilisons des points de terminaison Azure Web Apps comme exemple.

### <a name="create-a-traffic-manager-profile"></a>Créer un profil Traffic Manager
1. À partir d’un navigateur, connectez-vous toohello [portail Azure](http://portal.azure.com). Si vous ne possédez pas encore de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit d’un mois](https://azure.microsoft.com/free/). 
2. Sur hello **Hub** menu, cliquez sur **nouveau** > **réseau** > **afficher tous les**, cliquez sur **le trafic Gestionnaire de** hello tooopen de profil **profil créer Traffic Manager** panneau, puis cliquez sur **créer**.
3. Sur hello **profil créer Traffic Manager** panneau, terminée, comme suit :
    1. Sous **Nom**, entrez un nom pour votre profil. Ce nom doit toobe unique au sein de la zone de trafficmanager.net hello et entraîne le nom DNS de hello <name>, trafficmanager.net qui est utilisé tooaccess votre profil Traffic Manager.
    2. Dans **méthode de routage**, sélectionnez hello **priorité** méthode de routage.
    3. Dans **abonnement**, sélectionnez hello abonnement toocreate ce profil sous
    4. Dans **groupe de ressources**, créez un nouveau tooplace de groupe de ressources ce profil sous.
    5. Dans **emplacement du groupe de ressources**, sélectionnez l’emplacement hello hello du groupe de ressources. Ce paramètre fait référence emplacement toohello hello du groupe de ressources et n’a aucun impact sur hello profil Traffic Manager qui sera déployé globalement.
    6. Cliquez sur **Créer**.
    7. Lorsque le déploiement global de hello de votre profil Traffic Manager est terminée, il est répertorié dans le groupe de ressources respectives comme l’une des ressources de hello.

    ![Créer un profil Traffic Manager](./media/traffic-manager-create-profile/Create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a>Ajouter des points de terminaison Traffic Manager

1. Dans la barre de recherche du portail hello, recherchez hello **profil Traffic Manager** nom que vous avez créé dans hello précédant la section et cliquez sur hello du profil traffic manager Bonjour que hello affichée des résultats.
2. Bonjour **profil Traffic Manager** panneau, Bonjour **paramètres** , cliquez sur **points de terminaison**.
3. Bonjour **points de terminaison** panneau s’affiche, cliquez sur **ajouter**.
4. Bonjour **ajouter le point de terminaison** panneau, terminée, comme suit :
    1. Sous **Type**, cliquez sur **Point de terminaison Azure**.
    2. Fournir un **nom** en fonction duquel vous voulez toorecognize ce point de terminaison.
    3. Sous **Type de ressource cible**, cliquez sur **App Service**.
    4. Pour **ressource cible**, cliquez sur **choisir un service d’application** tooshow la liste hello Hello Web Apps sous hello même abonnement. Bonjour **ressource** panneau s’affiche, hello de choix que vous souhaitez tooadd comme hello du premier point de terminaison du service d’applications.
    5. Pour **Priorité**, sélectionnez **1**. Ainsi, tout le trafic entrant de point de terminaison toothis si elle est sain.
    6. Vérifiez que la case **Ajouter comme désactivé** est désélectionnée.
    7. Cliquez sur **OK**
5.  Répétez les étapes 3 et 4 pour le point de terminaison Azure Web Apps suivant hello. Assurez-vous que tooadd avec sa **priorité** à la valeur **2**.
6.  Lors de l’ajout de hello de deux points de terminaison est terminée, ils sont affichés dans hello **profil Traffic Manager** panneau, ainsi que leur état d’analyse en tant que **Online**.

    ![Ajouter un point de terminaison Traffic Manager](./media/traffic-manager-create-profile/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Utiliser le profil Traffic Manager hello
1.  Dans la barre de recherche du portail hello, recherchez hello **profil Traffic Manager** nom que vous avez créé dans la précédente section de hello. Dans les résultats de hello qui sont affichés, cliquez sur le profil traffic manager hello.
2. Bonjour **profil Traffic Manager** panneau, cliquez sur **vue d’ensemble**.
3. Hello **profil Traffic Manager** panneau affiche le nom DNS de hello de votre profil Traffic Manager nouvellement créé. Cela peut servir par les clients (par exemple, en accédant à l’aide d’un navigateur web de tooit) tooget routé toohello droite point de terminaison tel que déterminé par le type de routage hello. Dans ce cas, toutes les demandes sont routés toohello le premier point de terminaison et si Traffic Manager détecte pas intègre, le trafic de hello bascule automatiquement toohello le prochain point de terminaison.

## <a name="delete-hello-traffic-manager-profile"></a>Supprimer le profil Traffic Manager hello
Lorsque n’est plus nécessaire, supprimer le groupe de ressources hello et profil Traffic Manager hello que vous avez créés. toodo, sélectionnez groupe de ressources hello hello **profil Traffic Manager** panneau, cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur les [types de routage](traffic-manager-routing-methods.md).
- En savoir plus sur les [types de point de terminaison](traffic-manager-endpoint-types.md).
- En savoir plus sur la [surveillance du point de terminaison](traffic-manager-monitoring.md).



