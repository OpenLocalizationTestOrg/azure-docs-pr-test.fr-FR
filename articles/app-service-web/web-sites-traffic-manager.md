---
title: "aaaControlling trafic d’application web Azure avec Azure Traffic Manager"
description: "Cet article fournit des informations récapitulatives pour Azure Traffic Manager en matière de tooAzure des applications web."
services: app-service\web
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: dabda633-e72f-4dd4-bf1c-6e945da456fd
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: a93d4c9370046d54e401e36e7b495af8b711a2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a>Contrôle du trafic des applications web Azure avec Azure Traffic Manager
> [!NOTE]
> Cet article fournit des informations récapitulatives de Microsoft Azure Traffic Manager en matière de tooAzure App Service Web Apps. Vous trouverez plus d’informations sur Azure Traffic Manager lui-même en consultant les liens hello à fin hello de cet article.
> 
> 

## <a name="introduction"></a>Introduction
Vous pouvez utiliser Azure Traffic Manager toocontrol comment les demandes des clients web sont des applications distribuées tooweb dans Azure App Service. Lorsque des points de terminaison web sont ajoutés tooa Azure Traffic Manager profil, Azure Traffic Manager conserve des informations état hello de vos applications web (en cours d’exécution, arrêté ou supprimé) afin qu’il peut décider de ces points de terminaison doit recevoir le trafic.

## <a name="load-balancing-methods"></a>Méthodes d'équilibrage de charge
Azure Traffic Manager utilise trois méthodes d'équilibrage de charge. Ceux-ci sont décrits dans hello suit la liste en ce qui concerne les applications web tooAzure.

* **Basculement**: Si vous avez des clones d’application web dans des régions différentes, vous pouvez utiliser cette tooservice d’application web à une méthode tooconfigure tout le trafic de client web et configurer une autre application web dans un tooservice autre région que le trafic dans une application web de la première case hello n’est plus disponible.
* **Tourniquet (Round Robin)**: Si vous avez des clones d’application web dans des régions différentes, vous pouvez utiliser ce trafic toodistribute de méthode tout aussi dans les applications web de hello dans des régions différentes.
* **Performances**: hello méthode Performance répartit le trafic de la selon hello tooclients du temps aller-retour plus court. Hello, méthode de Performance peut être utilisé pour les applications web au sein de hello même région ou dans des régions différentes.

## <a name="web-apps-and-traffic-manager-profiles"></a>Applications web et profils dans Traffic Manager
tooconfigure hello contrôle du trafic d’application web, vous créez un profil dans Azure Traffic Manager qui utilise l’une des méthodes décrites précédemment d’équilibrage de charge hello trois et puis ajoutez les points de terminaison hello (dans ce cas, les applications web) pour lequel vous souhaitez toocontrol trafic toohello profil. État de votre application web (en cours d’exécution, arrêté ou supprimé) est communiqué régulièrement toohello du profil afin que Azure Traffic Manager dirige le trafic en conséquence.

Lorsque vous utilisez Azure Traffic Manager avec Azure, gardez Bonjour l’esprit les points suivants :

* Pour les déploiements uniquement d’applications web au sein de hello même région, les applications Web déjà fournit des fonctionnalités de basculement et de tourniquet sans mode de l’application tooweb tenir compte.
* Pour les déploiements dans hello même région qui utilisent des applications Web en conjonction avec un autre service cloud Azure, vous pouvez combiner les deux types de scénarios de points de terminaison tooenable hybrides.
* Vous pouvez spécifier un seul point de terminaison d’application web par région dans un profil. Lorsque vous sélectionnez une application web en tant que point de terminaison d’une région, hello autres applications web dans cette région ne sont plus disponibles pour la sélection de ce profil.
* Hello web points de terminaison que vous spécifiez dans un profil Traffic Manager de Azure seront affiche sous hello **les noms de domaine** section sur la page Configurer de hello pour l’application web de hello dans le profil de hello, mais ne pourra pas être configuré il.
* Après avoir ajouté un profil de tooa d’application web, hello **URL du Site** sur hello du tableau de bord du site web hello page du portail de l’application affiche hello les URL de domaine personnalisé de l’application web de hello si vous avez défini une. Dans le cas contraire, il affichera les URL du profil Traffic Manager hello (par exemple, `contoso.trafficmgr.com`). Les deux hello nom de domaine directe de l’application web hello et hello URL du Gestionnaire de trafic seront visible sur la page de configuration de l’application hello web sous hello **les noms de domaine** section.
* Vos noms de domaine personnalisé fonctionne comme prévu, mais dans Ajout tooadding les tooyour des applications web, vous devez également configurer votre ordinateur DNS carte toopoint toohello URL du Gestionnaire de trafic. Pour plus d’informations sur la façon de tooset d’un domaine personnalisé pour une application web Azure, consultez [configuration d’un nom de domaine personnalisé pour un site web Azure](app-service-web-tutorial-custom-domain.md).
* Vous pouvez uniquement ajouter des applications web qui se trouvent dans le mode standard ou premium tooa profil Azure Traffic Manager.

## <a name="next-steps"></a>Étapes suivantes
Pour une vue d'ensemble conceptuelle et technique d'Azure Traffic Manager, consultez la rubrique [Vue d'ensemble de Traffic Manager](../traffic-manager/traffic-manager-overview.md).

Pour plus d’informations sur l’utilisation de Traffic Manager avec les applications Web, consultez les billets de blog hello [à l’aide de Azure Traffic Manager avec les Sites Web Azure](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) et [Azure Traffic Manager peut à présent intégrer avec les Sites Web Azure](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/).

