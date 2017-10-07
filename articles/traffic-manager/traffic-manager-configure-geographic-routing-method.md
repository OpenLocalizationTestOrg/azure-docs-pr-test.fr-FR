---
title: "méthode de routage à l’aide de Azure Traffic Manager du trafic aaaConfigure géographique | Documents Microsoft"
description: "Cet article explique comment tooconfigure hello méthode de routage du trafic géographique à l’aide de Azure Traffic Manager"
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
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 4142389211ae54e7feea6564641e01e4477491e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-geographic-traffic-routing-method-using-traffic-manager"></a>Configurer la méthode de routage de trafic géographique hello à l’aide de Traffic Manager

méthode de routage du trafic géographique de Hello autorise le trafic toodirect vous toospecific les points de terminaison en fonction de l’emplacement géographique hello d'où proviennent les demandes de hello. Ce didacticiel vous montre comment toocreate un gestionnaire de trafic profil associé à cette méthode de routage et configurer le trafic tooreceive de points de terminaison hello à partir des zones géographiques spécifiques.

## <a name="create-a-traffic-manager-profile"></a>Créer un profil Traffic Manager

1. À partir d’un navigateur, connectez-vous toohello [portail Azure](http://portal.azure.com). Si vous ne possédez pas encore de compte, vous pouvez [vous inscrire pour bénéficier d’un essai gratuit d’un mois](https://azure.microsoft.com/free/).
2. Dans le menu du Hub hello, cliquez sur **nouveau** > **mise en réseau** > **voir toutes les**, puis cliquez sur **le profil Traffic Manager**tooopen hello **profil créer Traffic Manager** panneau.
3. Sur hello **profil créer Traffic Manager** panneau :
    1. Entrez un nom pour votre profil. Ce nom doit toobe unique au sein de la zone de trafficmanager.net hello et se produit dans le nom DNS de hello <profilename>, trafficmanager.net qui sera être tooaccess utilisé votre profil Traffic Manager.
    2. Sélectionnez hello **géographique** méthode de routage.
    3. Sélectionnez hello abonnement toocreate ce profil.
    4. Utiliser un groupe de ressources existant ou créer un nouveau tooplace de groupe de ressources de ce profil sous. Si vous choisissez toocreate un groupe de ressources, utilisez hello **emplacement du groupe de ressources** liste déroulante emplacement de hello toospecify hello du groupe de ressources. Ce paramètre fait référence emplacement toohello hello du groupe de ressources et n’a aucun impact sur hello profil Traffic Manager qui sera déployé globalement.
    5. Après avoir cliqué sur **Créer**, votre profil Traffic Manager est créé et déployé globalement.

![Créer un profil Traffic Manager](./media/traffic-manager-geographic-routing-method/create-traffic-manager-profile.png)

## <a name="add-endpoints"></a>Ajouter des points de terminaison

1. Recherchez le nom du profil Traffic Manager hello que vous venez de créer dans la barre de recherche du portail hello et cliquez sur le résultat de hello lorsqu’il est affiché.
2. Accédez trop**paramètres** -> **points de terminaison** dans le panneau de Traffic Manager hello.
3. Cliquez sur **ajouter** tooshow hello **ajouter le point de terminaison** panneau.
3. Bonjour **points de terminaison** panneau, cliquez sur **ajouter** et Bonjour **ajouter le point de terminaison** panneau s’affiche, complétez comme suit :
4. Sélectionnez **Type** en fonction de type hello du point de terminaison que vous ajoutez. Pour les profils de routage géographique utilisés en production, nous vous recommandons d’utiliser des types de point de terminaison imbriqués contenant un profil enfant avec plus d’un point de terminaison. Pour plus d’informations, consultez [FAQ sur les méthodes de routage du trafic géographique](traffic-manager-FAQs.md).
5. Fournir un **nom** en fonction duquel vous voulez toorecognize ce point de terminaison.
6. Certains champs de ce panneau dépendent de type hello du point de terminaison que vous ajoutez :
    1. Si vous ajoutez un point de terminaison Azure, sélectionnez hello **cibler un type de ressource** et hello **cible** basé sur les ressources hello vous voulez que le trafic toodirect
    2. Si vous ajoutez un **externe** point de terminaison, fournir hello **le nom de domaine complet (FQDN)** pour votre point de terminaison.
    3. Si vous ajoutez un **imbriqués de point de terminaison**, sélectionnez hello **ressource cible** qui correspond le profil enfant toohello vous souhaitez toouse et que vous spécifiez hello **dunombredepointsdeterminaisonenfantMinimum**.
7. Dans la section de la localisation géographique de hello, utilisez hello déroulante régions hello tooadd où vous souhaitez toothis point de terminaison toobe envoyé le trafic. Vous devez ajouter au moins une région et vous pouvez avoir plusieurs régions mappées.
8. Répétez cette étape pour tous les points de terminaison souhaité tooadd sous ce profil

![Ajouter un point de terminaison Traffic Manager](./media/traffic-manager-geographic-routing-method/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Utiliser le profil Traffic Manager hello
1.  Dans la barre de recherche du portail hello, recherchez hello **profil Traffic Manager** nom que vous avez créé dans hello précédant la section et cette hello affichée des résultats, cliquez sur le profil hello traffic manager Bonjour.
2. Bonjour **profil Traffic Manager** panneau, cliquez sur **vue d’ensemble**.
3. Hello **profil Traffic Manager** panneau affiche le nom DNS de hello de votre profil Traffic Manager nouvellement créé. Cela peut servir par les clients (par exemple, en accédant à l’aide d’un navigateur web de tooit) tooget routé toohello droite point de terminaison tel que déterminé par le type de routage hello.  Dans les cas de hello du routage géographique, Traffic Manager recherche à adresse IP source de hello de demande entrante de hello et détermine la région de hello à partir de laquelle il est d’origine. Si cette région est mappé tooan le point de terminaison, le trafic est routé toothere. Si cette région n’est pas mappé tooan le point de terminaison, Traffic Manager renvoie une réponse de requête NODATA.

## <a name="next-steps"></a>Étapes suivantes

- Découvrez-en davantage sur la [méthode de routage du trafic géographique](traffic-manager-routing-methods.md#geographic).
- Découvrez comment trop[tester les paramètres de Traffic Manager](traffic-manager-testing-settings.md).
