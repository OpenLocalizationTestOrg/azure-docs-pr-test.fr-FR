---
title: "Configurer des filtres de routage pour l’homologation d’Azure ExpressRoute Microsoft : Portail | Microsoft Docs"
description: "Cet article décrit la façon dont les filtres de routage tooconfigure pour l’utilisation de Microsoft Peering hello portail Azure"
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
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a>Configurer des filtres de routage pour l’homologation Microsoft

Filtres de routage sont un moyen de tooconsume un sous-ensemble de services pris en charge via l’homologation Microsoft. les étapes dans cette article vous aident à configurez et gérez des filtres de routage pour les circuits ExpressRoute Hello.

Dynamics 365 services et les services Office 365 comme Exchange Online, SharePoint Online et Skype pour entreprises, sont accessibles via l’homologation de Microsoft hello. Lors de l’homologation Microsoft est configuré dans un circuit ExpressRoute, tous les services connexes toothese de préfixes sont publiés via des sessions BGP hello établies. Une BGP Communauté valeur est attaché tooevery préfixe tooidentify hello du service qui vous est proposé via le préfixe de hello. Pour obtenir la liste des valeurs de communauté BGP hello et services hello auxquels elles sont mappées à, consultez [les Communautés BGP](expressroute-routing.md#bgp).

Si vous avez besoin des services de connectivité de tooall, un grand nombre de préfixes est publié via BGP. Cela augmente considérablement la taille de hello hello de tables d’itinéraires gérées par les routeurs au sein de votre réseau. Si vous envisagez tooconsume uniquement un sous-ensemble des services offerts via l’homologation Microsoft, vous pouvez réduire la taille hello de vos tables d’itinéraires de deux manières. Vous pouvez :

- Filtrer les préfixes indésirables en appliquant des filtres de routage sur les communautés BGP. Ceci est une pratique standard et très courante de mise en réseau.

- Définir des filtres de routage et de les appliquer de circuit ExpressRoute de tooyour. Un filtre d’itinéraire est une ressource que vous permet de sélectionner la liste hello des services que vous prévoyez tooconsume via l’homologation Microsoft. ExpressRoute les routeurs n’envoient liste hello de préfixes qui font partie des services de toohello identifiés dans le filtre de routage hello.

### <a name="about"></a>À propos des filtres de routage

Lors de l’homologation Microsoft est configuré sur votre circuit ExpressRoute, routeurs de bord Microsoft hello établissent une paire de sessions BGP avec les routeurs de périphérie hello (la vôtre ou votre fournisseur de connectivité). Aucun itinéraire n’est publiés tooyour réseau. réseau de tooyour tooenable itinéraire publications, vous devez associer un filtre de routage.

Un filtre de routage vous permet d’identifier les services auxquels vous souhaitez tooconsume via votre circuit ExpressRoute homologation de Microsoft. Il est essentiellement une liste blanche de toutes les valeurs de communauté hello BGP. Une fois qu’une ressource de filtre d’itinéraire est définie et attaché tooan circuit ExpressRoute, tous les préfixes qui mappent les valeurs de communauté toohello BGP sont publiés tooyour réseau.

toobe tooattach en mesure des filtres de routage avec les services Office 365, vous devez disposer de services d’Office 365 tooconsume d’autorisation via ExpressRoute. Si vous n’êtes pas autorisé tooconsume Office 365 des services via ExpressRoute, filtres de routage tooattach hello opération échoue. Pour plus d’informations sur le processus d’autorisation de hello, consultez [Azure ExpressRoute pour Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd). Services de connectivité de 365 tooDynamics ne nécessite pas l’autorisation préalable.

> [!IMPORTANT]
> Homologation Microsoft des circuits ExpressRoute qui ont été configurés préalable tooAugust 1, 2017 aura tous les préfixes de service publiés via l’homologation Microsoft, même si les filtres de routage ne sont pas définis. Homologation Microsoft des circuits ExpressRoute qui sont configurés sur ou après le 1er août 2017 n’aura pas de préfixes publiés jusqu'à ce qu’un filtre de routage est attaché toohello circuit.
> 
> 

### <a name="workflow"></a>Flux de travail

toobe les toosuccessfully en mesure de se connecter à tooservices via l’homologation Microsoft, vous devez effectuer les hello configuration comme suit :

- Vous devez disposer d’un circuit ExpressRoute actif où l’homologation Microsoft est approvisionnée. Vous pouvez utiliser hello suivant les instructions tooaccomplish ces tâches :
  - [Créer un circuit ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) et circuit hello activé par votre fournisseur de connectivité avant de continuer. Hello circuit ExpressRoute doit être dans un état configuré et activé.
  - [Créer l’homologation Microsoft](expressroute-howto-routing-portal-resource-manager.md) si vous gérez la session BGP hello directement. Sinon, demandez à votre fournisseur de connectivité de configurer l’homologation Microsoft pour votre circuit.

-  Vous devez créer et configurer un filtre de routage.
    - Identifier hello services vous avec tooconsume via l’homologation Microsoft
    - Identifier la liste des valeurs de communauté BGP associés aux services de hello de hello
    - Créer une règle tooallow hello préfixe liste correspondance hello valeurs de communauté BGP

-  Vous devez joindre le circuit ExpressRoute toohello hello itinéraire filtre.

## <a name="before-you-begin"></a>Avant de commencer

Avant de commencer la configuration, assurez-vous que vous remplissez hello suivant des critères :

 - Hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.

 - Vous devez disposer d’un circuit ExpressRoute actif. Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) et circuit hello activé par votre fournisseur de connectivité avant de continuer. Hello circuit ExpressRoute doit être dans un état configuré et activé.

 - Vous devez disposer d’une homologation Microsoft active. Suivez les instructions de [création et modification de la configuration d’homologation](expressroute-howto-routing-portal-resource-manager.md).


## <a name="prefixes"></a>Étape 1. Obtenir la liste des préfixes et des valeurs de communauté BGP

### <a name="1-get-a-list-of-bgp-community-values"></a>1. Obtenir la liste des valeurs de communauté BGP

Les valeurs de communauté BGP associés aux services accessibles via l’homologation Microsoft n’est disponible dans hello [conditions de routage ExpressRoute](expressroute-routing.md) page.

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2. Dressez la liste des valeurs de hello que vous souhaitez toouse

Dressez la liste des valeurs de communauté BGP souhaité toouse dans un filtre d’itinéraire hello. Par exemple, hello valeur communautaire BGP pour les services de Dynamics 365 est 12076:5040.

## <a name="filter"></a>Étape 2. Créer un filtre de routage et une règle de filtre

Un filtre de routage peut avoir qu’une seule règle, et la règle de hello doit être de type « Autoriser ». Cette règle peut être associée à une liste des valeurs de communauté BGP.

### <a name="1-create-a-route-filter"></a>1. Créer un filtre de routage
Vous pouvez créer un filtre de routage en sélectionnant hello option toocreate une nouvelle ressource. Cliquez sur **nouveau** > **réseau** > **RouteFilter**, comme indiqué dans hello suivant image :

![Créer un filtre de routage](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

Vous devez placer le filtre de routage hello dans un groupe de ressources. 

![Créer un filtre de routage](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a>2. Créer une règle de filtre

Vous pouvez ajouter et gérer les règles de mise à jour en sélectionnant hello onglet règle votre filtre de routage.

![Créer un filtre de routage](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


Vous pouvez sélectionner hello services souhaités tooconnect toofrom hello liste déroulant et enregistrement la règle hello lorsqu’il est terminé.

![Créer un filtre de routage](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <a name="attach"></a>Étape 3. Attacher le circuit ExpressRoute tooan hello itinéraire filtre

Vous pouvez attacher le circuit de tooa hello route filtre en sélectionnant le bouton « Ajouter un Circuit » de hello, circuit ExpressRoute de hello à partir de la liste déroulante hello.

![Créer un filtre de routage](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <a name="getproperties"></a>propriétés de hello tooget d’un filtre de routage

Vous pouvez afficher les propriétés d’un filtre de routage lorsque vous ouvrez des ressources de hello dans le portail de hello.

![Créer un filtre de routage](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <a name="updateproperties"></a>propriétés de hello tooupdate d’un filtre de routage

Vous pouvez mettre à jour liste hello du circuit BGP Communauté valeurs tooa attaché en sélectionnant le bouton de hello « gérer les règles ».


![Créer un filtre de routage](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Créer un filtre de routage](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <a name="detach"></a>toodetach un filtre d’itinéraire à partir d’un circuit ExpressRoute

toodetach un circuit de filtre de routage hello, cliquez avec le bouton droit sur le circuit de hello et cliquez sur « Dissocier ».

![Créer un filtre de routage](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <a name="delete"></a>toodelete un filtre de routage

Vous pouvez supprimer un filtre de routage en sélectionnant le bouton de suppression hello. 

![Créer un filtre de routage](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).
