---
title: "Analyse des modèles d’utilisation CDN Azure | Microsoft Docs"
description: "Vous pouvez afficher les modèles d'utilisation pour votre CDN via les rapports suivants : la bande passante, les données transférées, les correspondances, les statuts de cache, le taux d'accès au cache, les données transférées IPV4/IPV6."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 5a0d9018-8bdb-48ff-84df-23648ebcf763
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: aadbe872dd3384c8d337b432fb3be69422ca322b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>Analyse des modèles d’utilisation CDN Azure

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Le guide ci-dessous suit la procédure permettant d’afficher les rapports de base via le portail de gestion des profils Verizon. Vous pouvez également exporter les données d’analyse de base vers le stockage, un concentrateur d’événements, ou Log Analytics (OMS) pour les profils Verizon et Akamai [via le portail Azure](cdn-log-analysis.md).

Vous pouvez afficher les modèles d'utilisation pour votre contenu via les rapports suivants :

* Bande passante
* Données transférées
* Correspondances
* États du cache
* Taux d'accès au cache
* Données IPV4/IPV6 transférées

## <a name="accessing-core-reports"></a>Accès aux rapports de base
1. Dans le panneau de profil CDN, cliquez sur le bouton **Gérer** .
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-reports/cdn-manage-btn.png)
   
    Le portail de gestion CDN s'ouvre.
2. Pointez sur l’onglet **Analytics**, puis sur le menu volant **Core Reports** (Rapports principaux).  Cliquez sur le rapport souhaité dans le menu.
   
    ![Portail de gestion CDN - Menu des rapports principaux](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a>Bande passante
Le rapport relatif à la bande passante consiste en un graphique et un tableau de données indiquant l'utilisation de la bande passante pour HTTP et HTTPS sur une période donnée. Vous pouvez afficher l'utilisation de la bande passante sur tous les POP CDN ou un POP particulier. Cela vous permet d'afficher les pics de trafic et la distribution sur les POP CDN en Mbits/s.

* Sélectionnez Tous les nœuds Edge pour afficher le trafic à partir de tous les nœuds ou choisissez une région/un nœud spécifique dans la liste déroulante.
* Sélectionnez la plage de dates pour afficher les données par jour/semaine/mois, etc. ou entrez des dates personnalisées, puis cliquez sur « go » pour vous assurer que votre sélection est mise à jour.
* Vous pouvez exporter et télécharger les données en cliquant sur l'icône de feuille Excel située en regard de « go ».

Le rapport est mis à jour toutes les 5 minutes.

![Rapport de la bande passante](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a>Données transférées
Ce rapport consiste en un graphique et un tableau de données indiquant l'utilisation de trafic pour HTTP et HTTPS sur une période donnée. Vous pouvez afficher le trafic de la bande passante sur tous les POP CDN ou un POP particulier. Cela vous permet d'afficher les pics de trafic et la distribution sur les POP CDN en Go.

* Sélectionnez Tous les nœuds Edge pour afficher le trafic à partir de tous les nœuds ou choisissez une région/un nœud spécifique dans la liste déroulante.
* Sélectionnez la plage de dates pour afficher les données par jour/semaine/mois, etc. ou entrez des dates personnalisées, puis cliquez sur « go » pour vous assurer que votre sélection est mise à jour.
* Vous pouvez exporter et télécharger les données en cliquant sur l'icône de feuille Excel située en regard de « go ».

Le rapport est mis à jour toutes les 5 minutes.

![Rapport des données transférées](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a>Correspondances (codes d'état)
Ce rapport décrit la distribution des codes d'état de demande pour votre contenu. Chaque demande de contenu génère un code d'état HTTP. Le code d'état décrit comment les POP Edge ont géré la demande. Par exemple, les codes d'état 2xx indiquent que la demande a été correctement servie à un client, tandis qu'un code d'état 4xx indique une erreur. Pour plus d'informations sur les codes d'état HTTP, consultez [codes d'état](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

* Sélectionnez la plage de dates pour afficher les données par jour/semaine/mois, etc. ou entrez des dates personnalisées, puis cliquez sur « go » pour vous assurer que votre sélection est mise à jour.
* Vous pouvez exporter et télécharger les données en cliquant sur la feuille Excel située en regard de « go ».

![Rapport de correspondances](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a>États du cache
Ce rapport décrit la distribution des correspondances et des absences dans le cache pour la requête du client. Étant donné que les meilleures performances proviennent de correspondances dans le cache, vous pouvez optimiser les vitesses de remise de données en réduisant les absences dans le cache et les correspondances dans le cache expirées. Les absences dans le cache peuvent être réduites en configurant votre serveur d'origine pour éviter d'affecter des en-têtes de réponse « no-cache », en évitant la mise en cache de la chaîne de requête, sauf lorsque cela est strictement nécessaire et en évitant les codes de réponse non mis en cache. Les correspondances dans le cache expirées peuvent être évitées en augmentant au maximum la propriété max-age d’une ressource, afin de réduire le nombre de requêtes au serveur d'origine.

![Rapport des états du cache](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a>Les états de cache principaux sont les suivants :
* TCP_HIT : traités à partir d’Edge. L'objet était en cache et n'avait pas dépassé son max-age.
* TCP_HIT : traité à partir de l’origine. L'objet n'était pas dans le cache et la réponse a été renvoyée à l'origine.
* TCP_EXPIRED _MISS : traités à partir de l'origine après la revalidation avec l'origine. L'objet était en cache mais avait dépassé son max-age. Une revalidation avec l’origine a entraîné un remplacement de l'objet de cache par une nouvelle réponse de l'origine.
* TCP_EXPIRED _HIT : traités à partir de Edge après la revalidation avec l'origine. L'objet était en cache mais avait dépassé son max-age. Une revalidation avec le serveur d'origine n’a entraîné aucune modification de l’objet de cache.
* Sélectionnez la plage de dates pour afficher les données par jour/semaine/mois, etc. ou entrez des dates personnalisées, puis cliquez sur « go » pour vous assurer que votre sélection est mise à jour.
* Vous pouvez exporter et télécharger les données en cliquant sur l'icône de feuille Excel située en regard de « go ».

### <a name="full-list-of-cache-statuses"></a>Liste complète des états de cache
* TCP_HIT : cet état est signalé lorsqu'une requête est traitée directement du POP au client. Une ressource est immédiatement traitée à partir d'un POP lorsqu'il est mis en cache sur le serveur POP le plus proche du client et que sa durée de vie (TTL) est valide. La durée de vie est déterminée par les en-têtes de réponse suivants :
  
  * Cache-Control: s-maxage
  * Cache-Control: max-age
  * Expires
* TCP_MISS : cet état indique qu'une version mise en cache de la ressource demandée est introuvable sur le serveur POP le plus proche du client. La ressource est demandée à partir d'un serveur d'origine ou d’un serveur de protection d'origine. Si le serveur d'origine ou le serveur de protection d'origine renvoie une ressource, elle est envoyée au client et mise en cache sur le client et le serveur Edge. Dans le cas contraire, un code d'état autre que -200 (par exemple, 403 interdit, 404 introuvable, etc.) est retourné.
* TCP_EXPIRED _HIT : cet état est signalé lorsqu’une requête ciblant une ressource avec une durée de vie (TTL) expirée, par exemple lorsque la propriété max-age de la ressource est arrivée à expiration, a été envoyée directement du POP au client.
  
    Une requête expirée entraîne généralement une demande de revalidation au serveur d'origine. Pour qu’un _HIT TCP_EXPIRED se produise, le serveur d'origine doit indiquer qu'il n’existe pas de version plus récente de la ressource. Ce type de situation met généralement à jour les en-têtes Cache-Control et Expires de la ressource.
* TCP_EXPIRED _MISS : cet état est signalé lorsqu'une version plus récente d'une ressource mise en cache expirée est envoyée du POP au client. Cela se produit lorsque la durée de vie d’une ressource mise en cache a expiré (par exemple, la propriété max-age a expiré) et que le serveur d'origine retourne une version plus récente de la ressource. Cette nouvelle version de la ressource est envoyée au client, plutôt que la version mise en cache. En outre, elle est mise en cache sur le serveur Edge et le client.
* CONFIG_NOCACHE : cet état indique qu'une configuration spécifique au client sur le POP Edge a empêché la mise en cache de la ressource.
* NONE : cet état indique qu'une vérification de la fraîcheur du contenu du cache n'a pas été effectuée.
* TCP_ CLIENT_REFRESH _MISS : cet état est signalé lorsqu'un client HTTP (par exemple, le navigateur) force un POP Edge à récupérer une nouvelle version d'une ressource obsolète à partir du serveur d'origine.
  
    Par défaut, nos serveurs empêchent un client HTTP de forcer nos serveurs Edge à récupérer une nouvelle version de la ressource à partir du serveur d'origine.
* TCP_ PARTIAL_HIT : cet état est signalé lorsqu'une demande de plage d'octets entraîne un accès à une ressource partiellement en cache. La plage d'octets demandée est immédiatement envoyée du serveur POP au client.
* UNCACHEABLE : cet état est signalé lorsque les en-têtes Cache-Control et Expires d'une ressource indiquent qu'elle ne doit pas être mise en cache sur un POP ou par le client HTTP. Ces types de requêtes sont traités à partir du serveur d'origine

## <a name="cache-hit-ratio"></a>Taux d'accès au cache
Ce rapport indique le pourcentage de requêtes mises en cache traitées directement à partir de la mémoire cache.

Le rapport fournit les informations suivantes :

* Le contenu demandé a été mis en cache sur le serveur POP le plus proche du demandeur.
* La requête a été traitée directement à partir du Edge de notre réseau.
* La demande ne nécessitait pas de revalidation avec le serveur d'origine.

Le rapport n'inclut pas :

* Les requêtes refusées en raison des options de filtrage par pays.
* Les demandes de ressources dont les en-têtes indiquent qu'elles ne doivent pas être mises en cache. Par exemple, les en-têtes Cache-Control: private, Cache-Control: no-cache, ou Pragma: no-cache empêchent la mise en cache d’une ressource.
* Les demandes de plage d'octets pour le contenu partiellement mis en cache.

La formule est : (TCP_ HIT/(TCP_ HIT+TCP_MISS))*100

* Sélectionnez la plage de dates pour afficher les données par jour/semaine/mois, etc. ou entrez des dates personnalisées, puis cliquez sur « go » pour vous assurer que votre sélection est mise à jour.
* Vous pouvez exporter et télécharger les données en cliquant sur l'icône de feuille Excel située en regard de « go ».

![Rapport des taux d'accès au cache](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a>Données IPV4/IPV6 transférées
Ce rapport affiche la distribution de l'utilisation du trafic entre IPV4 et IPV6.

![Données IPV4/IPV6 transférées](./media/cdn-reports/cdn-ipv4-ipv6.png)

* Sélectionnez la plage de dates pour afficher les données par jour/semaine/mois, etc. ou entrez des dates personnalisées.
* Puis, cliquez sur « go » pour vous assurer que votre sélection est mise à jour.

## <a name="considerations"></a>Considérations
Les rapports peuvent uniquement être générés pour les 18 derniers mois.

