---
title: Afficher le trafic par Traffic View dans Azure Traffic Manager | Microsoft Docs
description: "Introduction à la fonctionnalité d’affichage de trafic Traffic View et à Traffic Manager"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 11/11/2017
ms.author: kumud
ms.custom: 
ms.openlocfilehash: 6b4378cb293824702dd52dcdeb86619f957b83ea
ms.sourcegitcommit: afc78e4fdef08e4ef75e3456fdfe3709d3c3680b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/16/2017
---
# <a name="traffic-manager-traffic-view"></a>Traffic View de Traffic Manager

>[!NOTE]
>La fonctionnalité d’affichage de trafic Traffic View dans Traffic Manager est en préversion publique. Il se peut qu’elle n’offre pas les mêmes niveaux de disponibilité et de fiabilité que les fonctions de la version mise à la disposition générale. Cette fonctionnalité n’est pas prise en charge, est susceptible de disposer de possibilités limitées et peut ne pas être disponible à certains emplacements Azure. Pour les notifications les plus récentes sur la disponibilité et l’état de cette fonctionnalité, consultez la page relative aux [mises à jour d’Azure Traffic Manager](https://azure.microsoft.com/updates/?product=traffic-manager).

Traffic Manager vous offre un routage au niveau DNS, afin que vos utilisateurs finals soient dirigés vers les points de terminaison sains, en fonction de la méthode de routage spécifiée au moment de la création du profil. La Vue du trafic permet à Microsoft Azure Traffic Manager d’afficher vos bases d’utilisateurs (avec une granularité au niveau de la résolution DNS) et de leur schéma de trafic. Lorsque vous activez Traffic View, ces informations sont traitées pour vous fournir des renseignements exploitables. 

Grâce à Traffic View, vous pouvez :
- comprendre où se trouvent vos bases d’utilisateurs (jusqu’à une granularité fixée au niveau de la résolution DNS locale)
- voir le volume de trafic (observé pour les requêtes DNS gérées par Azure Traffic Manager) provenant de ces régions.
- obtenir des insights sur la latence représentative expérimentée par ces utilisateurs.
- explorez en profondeur les modèles de trafic spécifiques à partir de chacune de ces bases d’utilisateurs vers les régions Azure où vous avez des points de terminaison. 

Par exemple, vous pouvez utiliser Traffic View pour comprendre quelles régions enregistrent des volumes de trafic importants, mais pâtissent de latences supérieures. Vous pouvez ensuite utiliser ces informations pour planifier votre phase d’expansion sur de nouvelles régions Azure, afin que ces utilisateurs puissent bénéficier d’une latence plus faible.

## <a name="how-traffic-view-works"></a>Fonctionnement de Traffic View

Le fonctionnement de Traffic View est alimenté par l’observation que Traffic Manager effectue sur les requêtes entrantes, reçues au cours des sept derniers jours sur un profil pour lequel cette fonctionnalité a été activée. À partir des informations sur les requêtes entrantes, la Vue du trafic extrait l’adresse IP source est extraite de la résolution DNS, qui est alors utilisée comme représentation de l’emplacement des utilisateurs. Ceux-ci sont alors regroupés ensemble, selon une granularité fixée au niveau de la résolution DNS, afin de créer des régions de bases d’utilisateurs en utilisant les informations géographiques des adresses IP gérées par Traffic Manager. Traffic Manager examine ensuite les régions Azure vers lesquelles la requête a été routée, et constitue une carte des flux de trafic pour les utilisateurs à partir de ces régions.  
À l’étape suivante, Traffic Manager met en corrélation la région des bases d’utilisateurs avec le mappage des régions Azure au moyen des tables de latence de l’intelligence réseau qu’il tient à jour, pour que les différents réseaux d’utilisateurs finals comprennent la latence moyenne rencontrée par les utilisateurs de ces régions lorsqu’ils se connectent à des régions Azure. Tous ces calculs sont ensuite regroupés sous forme de tableaux au niveau de l’adresse IP de la résolution DNS locale avant de vous être présentés. Vous pouvez utiliser les informations de différentes manières.

>[!NOTE]
>La latence décrite dans la Vue du trafic correspond à la latence représentative entre l’utilisateur final et les régions Azure auxquelles il est connecté. Il ne s’agit pas de la latence des recherches DNS.

## <a name="visual-overview"></a>Présentation visuelle

Lorsque vous accédez à la section **Vue du trafic** de votre page Microsoft Azure Traffic Manager, vous voyez apparaître une carte géographique incluant une superposition des aperçus de la Vue du trafic. Cette carte fournit des informations sur la base d’utilisateurs et les points de terminaison de votre profil Traffic Manager.

### <a name="user-base-information"></a>Informations de la base d’utilisateurs

Les informations sur l’emplacement disponibles pour les résolutions DNS locales sont affichées sur cette carte. La couleur du programme de résolution DNS indique la latence moyenne rencontrée par les utilisateurs finaux ayant utilisé ce programme de résolution DNS pour les requêtes Traffic Manager.

Si vous pointez sur un emplacement du programme de résolution DNS dans le mappage, il affiche les informations suivantes :
- l’adresse IP du programme de résolution DNS ;
- la quantité de trafic de requête DNS affichée par Traffic Manager à partir de celui-ci ;
- les points de terminaison pour lesquels le trafic à partir du programme de résolution DNS a été routé, sous forme de ligne entre le point de terminaison et le programme de résolution DNS ; 
- la latence moyenne entre cet emplacement et le point de terminaison, représentée par la couleur de la ligne qui les relie.

### <a name="endpoint-information"></a>Informations sur le point de terminaison

Les régions Azure dans lesquelles résident les points de terminaison sont affichées sous la forme de points bleus dans la carte. Cliquez sur n’importe quel point de terminaison pour afficher les différents emplacements (basés sur le programme de résolution DNS utilisé) depuis lesquels le trafic a été dirigé vers ce point de terminaison. Les connexions sont affichées sous la forme d’une ligne entre le point de terminaison et l’emplacement du programme de résolution DNS. Leur couleur correspond à la latence représentative entre ces deux éléments. En outre, vous pouvez voir le nom du point de terminaison, la région Azure dans lequel elle s’exécute et le volume total de demandes dirigées vers cette dernière par ce profil Traffic Manager.


## <a name="tabular-listing-and-raw-data-download"></a>Téléchargement de données brutes et liste de tableaux

Vous pouvez afficher les données relatives à la Vue du trafic sous la forme d’un tableau, dans le portail Azure. Il existe une entrée pour chaque paire adresse IP du programme de résolution DNS/point de terminaison qui indique l’emplacement géographique du programme de résolution DNS (le cas échéant), le nom de la région Azure dans laquelle se trouve le point de terminaison, le volume de requêtes associé à ce programme de résolution DNS et la latence représentative associée aux utilisateurs finaux à l’aide de ce programme DNS (le cas échéant). Vous pouvez également télécharger les données de la Vue du trafic dans un fichier CSV, qui peut être utilisé dans le cadre du flux de travail analytique de votre choix.

## <a name="billing"></a>Facturation

Lorsque vous utilisez Traffic View, vous êtes facturé en fonction du nombre de points de données utilisés pour créer les insights présentés. Actuellement, le seul type de point de données utilisé correspond aux requêtes reçues par rapport à votre profil Traffic Manager. Pour plus d’informations sur les prix, visitez la page [Tarifs Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager/).


## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur le [fonctionnement de Traffic Manager](traffic-manager-overview.md)
- En savoir plus sur les [méthodes de routage du trafic](traffic-manager-routing-methods.md) prises en charge par Traffic Manager
- En savoir plus sur la [création d’un profil Traffic Manager](traffic-manager-create-profile.md)

