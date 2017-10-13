---
title: "Contrôle du trafic des applications web Azure avec Azure Traffic Manager"
description: Cet article fournit des informations globales sur Azure Traffic Manager et son rapport aux applications web Azure.
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
ms.openlocfilehash: fb7d391e3118a9dccde5501c3f30c6f580932a30
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a>Contrôle du trafic des applications web Azure avec Azure Traffic Manager
> [!NOTE]
> Cet article présente des informations résumées sur Microsoft Azure Traffic Manager, qui est associé aux applications web Azure App Service. Vous trouverez d'autres informations sur Azure Traffic Manager en suivant les liens fournis à la fin de cet article.
> 
> 

## <a name="introduction"></a>Introduction
Vous pouvez utiliser Azure Traffic Manager pour contrôler la façon dont les requêtes des clients web sont distribuées aux applications web dans Azure App Service. Lorsque des points de terminaison d’applications web sont ajoutés à un profil Azure Traffic Manager, ce dernier conserve une trace du statut de vos applications web (en cours d’exécution, arrêtées ou supprimées) pour pouvoir décider du point de terminaison qui doit recevoir le trafic.

## <a name="load-balancing-methods"></a>Méthodes d'équilibrage de charge
Azure Traffic Manager utilise trois méthodes d'équilibrage de charge. Elles sont décrites dans la liste suivante, car elles se rapportent aux applications web Azure.

* **Basculement**: si vous avez des clones d’application web dans différentes régions, utilisez cette méthode pour configurer une application web qui traite l’ensemble du trafic des clients web, et en configurer une autre d’une région différente qui traite ce trafic en cas de défaillance de la première.
* **Tourniquet**: si vous avez des clones d’application web dans différentes régions, utilisez cette méthode pour répartir le trafic équitablement entre les applications web des différentes régions.
* **Performance**: cette méthode répartit le trafic en fonction du trajet aller-retour le plus court avec les clients. Cette méthode peut être utilisée pour les applications web d’une même région ou de régions différentes.

## <a name="web-apps-and-traffic-manager-profiles"></a>Applications web et profils dans Traffic Manager
Pour configurer le contrôle du trafic des applications web, vous pouvez créer un profil dans Azure Traffic Manager, qui utilise l’une des trois méthodes d’équilibrage de charge décrites précédemment, puis ajouter au profil les points de terminaison (ici, des applications web) dont vous souhaitez contrôler le trafic. Le statut de votre application web (en cours d’exécution, arrêtée ou supprimée) est régulièrement communiqué au profil, ce qui permet à Azure Traffic Manager de diriger le trafic.

Lorsque vous utilisez Azure Traffic Manager avec Azure, tenez compte des points suivants :

* Pour les déploiements des applications web dans une même région uniquement, Web Apps fournit déjà les fonctionnalités de basculement et de tourniquet (round-robin) et ce, quel que soit le mode des applications web.
* Pour les déploiements dans une même région qui utilisent Web Apps conjointement avec un autre service cloud Azure, vous pouvez combiner les deux types de point de terminaison pour autoriser les scénarios hybrides.
* Vous pouvez spécifier un seul point de terminaison d’application web par région dans un profil. Lorsque vous sélectionnez une application web comme point de terminaison pour une région, les autres applications web de cette région ne peuvent plus être sélectionnées pour ce profil.
* Les points de terminaison d’applications web, que vous spécifiez dans un profil Azure Traffic Manager, s’affichent dans la section **Noms de domaine** de la page Configurer de l’application web du profil, mais ils ne sont pas configurables ici.
* Lorsque vous avez ajouté une application web à un profil, l’ **URL du site** dans le tableau de bord de l’application web sur le portail affiche l’URL du domaine personnalisé de l’application web (s’il est défini). Sinon, elle affiche l’URL du profil Traffic Manager (par exemple, `contoso.trafficmgr.com`). Le nom de domaine direct de l’application web et l’URL de Traffic Manager sont tous deux affichés dans la page Configurer de l’application web dans la section **Noms de domaine** .
* Vos noms de domaines personnalisés fonctionnent comme prévu, mais en plus de les ajouter à vos applications web, vous devez configurer votre carte DNS pour qu’elle pointe vers l’URL de Traffic Manager. Pour plus d’informations sur la configuration d’un domaine personnalisé pour une application web Azure, consultez la page [Configuration d’un nom de domaine personnalisé pour un site web Azure](app-service-web-tutorial-custom-domain.md).
* Vous ne pouvez ajouter que des applications web en mode standard ou Premium à un profil Azure Traffic Manager.

## <a name="next-steps"></a>Étapes suivantes
Pour une vue d'ensemble conceptuelle et technique d'Azure Traffic Manager, consultez la rubrique [Vue d'ensemble de Traffic Manager](../traffic-manager/traffic-manager-overview.md).

Pour plus d’informations sur l’utilisation de Traffic Manager avec Web Apps, consultez les billets de blog [Utilisation de Microsoft Azure Traffic Manager avec WAWS](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) et [Azure Traffic Manager peut désormais s’intégrer dans les sites web Azure](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/).

