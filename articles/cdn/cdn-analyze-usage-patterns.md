---
title: "modèles d’utilisation CDN Azure aaaAnalyze | Documents Microsoft"
description: "Vous pouvez afficher des modèles d’utilisation de votre CDN à l’aide de hello suivant de rapports : la bande passante, les données transférées, présences dans le, les États de Cache, le taux d’accès au Cache, IPV4/IPV6 données transférées."
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
ms.openlocfilehash: d27e6f60acaed66abb27d860c3a3e2e81c9f60cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>Analyse des modèles d’utilisation CDN Azure

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

guide de Hello ci-dessous traverse hello étapes tooview hello core rapports via le portail de gestion hello pour les profils de Verizon. Vous pouvez également exporter toostorage de données analytique core, concentrateur d’événements ou analytique de journal (oms) pour les profils Verizon et Akamai [via le portail de hello azure](cdn-log-analysis.md).

Vous pouvez afficher les modèles d’utilisation de votre CDN hello suivant des rapports à l’aide de :

* Bande passante
* Données transférées
* Correspondances
* États du cache
* Taux d'accès au cache
* Données IPV4/IPV6 transférées

## <a name="accessing-core-reports"></a>Accès aux rapports de base
1. À partir du Panneau de profil hello CDN, cliquez sur hello **gérer** bouton.
   
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-reports/cdn-manage-btn.png)
   
    portail de gestion CDN Hello s’ouvre.
2. Placez votre curseur sur hello **Analytique** tab, puis pointez sur hello **Core rapports** menu volant.  Cliquez sur rapport hello souhaité dans le menu de hello.
   
    ![Portail de gestion CDN - Menu des rapports principaux](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a>Bande passante
état de la bande passante Hello consiste en un tableau de graphique et les données indiquant l’utilisation de la bande passante hello pour HTTP et HTTPS sur une période particulière. Vous pouvez afficher l’utilisation de la bande passante hello entre tous les CDN POP ou d’un POP particulier. Ainsi, vous tooview hello pics de trafic et la distribution sur CDN POP en Mbits/s.

* Sélectionnez le trafic toosee de tous les noeuds de tous les nœuds ou choisissez un région/nœud spécifique à partir de la liste déroulante de hello.
* Sélectionnez des données Date plage tooview par jour/semaine/mois, etc. ou entrer des dates personnalisées, puis toomake que votre sélection est mis à jour de « go ».
* Vous pouvez exporter et téléchargement des données en cliquant sur hello hello excel icône feuille située en regard de trop « go ».

rapport de Hello est mise à jour toutes les 5 minutes.

![Rapport de la bande passante](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a>Données transférées
Ce rapport se compose d’une table de graphique et les données indiquant l’utilisation du trafic de hello pour HTTP et HTTPS sur une période particulière. Vous pouvez afficher l’utilisation de hello du trafic entre tous les CDN POP ou d’un POP particulier. Ainsi, vous tooview hello pics de trafic et la distribution sur CDN POP en Go.

* Sélectionnez le trafic de tous les noeuds toosee de toutes les remarques ou choisissez un région/nœud spécifique à partir de la liste déroulante de hello.
* Sélectionnez des données Date plage tooview par jour/semaine/mois, etc. ou entrer des dates personnalisées, puis toomake que votre sélection est mis à jour de « go ».
* Vous pouvez exporter et téléchargement des données en cliquant sur hello hello excel icône feuille située en regard de trop « go ».

rapport de Hello est mise à jour toutes les 5 minutes.

![Rapport des données transférées](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a>Correspondances (codes d'état)
Ce rapport décrit la distribution hello demande des codes d’état pour votre contenu. Chaque demande de contenu génère un code d'état HTTP. code d’état Hello décrit les modalités de bord POP sur demande de hello. Par exemple, les codes d’état de 2xx indiquent que demande hello a été traitée correctement tooa client, tandis qu’un code d’état 4xx indique une erreur s’est produite. Pour plus d'informations sur les codes d'état HTTP, consultez [codes d'état](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

* Sélectionnez des données Date plage tooview par jour/semaine/mois, etc. ou entrer des dates personnalisées, puis toomake que votre sélection est mis à jour de « go ».
* Vous pouvez exporter et téléchargement des données en cliquant sur hello hello excel feuille située en regard de trop « go ».

![Rapport de correspondances](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a>États du cache
Ce rapport décrit la distribution hello de présences dans le cache et absences dans le cache pour la demande du client. Étant donné que les performances les meilleures hello proviennent de présences dans le cache, vous pouvez optimiser les vitesses de remise de données par la réduction des absences dans le cache et de présences dans le cache a expiré. Absences dans le cache peuvent être réduits en configurant votre tooavoid de serveur d’origine attribution des en-têtes de réponse de « no-cache », en évitant la chaîne de requête mise en cache, sauf lorsque cela est strictement nécessaire et en évitant les codes de réponse non mise en cache. Expiration du cache de l’accès peuvent être évités en effectuant max-age d’un élément multimédia tant que possible toominimize hello nombre de serveur d’origine toohello demandes.

![Rapport des états du cache](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a>Les états de cache principaux sont les suivants :
* TCP_HIT : traités à partir d’Edge. objet de Hello était en cache et n’a pas dépassé son max-age.
* TCP_HIT : traité à partir de l’origine. l’objet Hello n’était pas dans le cache et réponse de hello était tooorigin précédent.
* TCP_EXPIRED _MISS : traités à partir de l'origine après la revalidation avec l'origine. objet de Hello était en cache, mais a dépassé son max-age. Revalidation avec origine a généré un objet dans le cache hello qui est remplacée par une nouvelle réponse à partir de l’origine.
* TCP_EXPIRED _HIT : traités à partir de Edge après la revalidation avec l'origine. objet de Hello était en cache, mais a dépassé son max-age. Revalidation avec le serveur d’origine hello a généré un objet hello dans le cache en cours sans modification.
* Sélectionnez des données Date plage tooview par jour/semaine/mois, etc. ou entrer des dates personnalisées, puis toomake que votre sélection est mis à jour de « go ».
* Vous pouvez exporter et téléchargement des données en cliquant sur hello hello excel icône feuille située en regard de trop « go ».

### <a name="full-list-of-cache-statuses"></a>Liste complète des états de cache
* TCP_HIT - cet état est signalé lorsqu’une demande est pris en charge directement à partir de clients de toohello hello POP. Un élément multimédia est immédiatement pris en charge à partir d’un POP lorsqu’elle est mise en cache sur le client de toohello le plus proche hello POP et durée de vie est valide, ou durée de vie. Durée de vie est déterminée par hello suivant les en-têtes de réponse :
  
  * Cache-Control: s-maxage
  * Cache-Control: max-age
  * Expires
* TCP_MISS - cet état indique qu’une version mise en cache de ressource demandée de hello est introuvable sur le client de toohello hello POP le plus proche. ressource de Hello sera demandé à partir d’un serveur d’origine ou sur un serveur de protection d’origine. Si le serveur d’origine hello ou le serveur de protection d’origine hello retourne un élément multimédia, il sera pris en charge toohello client et mis en cache sur hello client et le serveur de périphérie hello. Dans le cas contraire, un code d'état autre que -200 (par exemple, 403 interdit, 404 introuvable, etc.) est retourné.
* TCP_EXPIRED _HIT - cet état est signalé lorsqu’une demande ciblant un élément multimédia avec une durée de vie a expiré, telles que lorsque max-age l’élément multimédia hello a expiré, a été pris en charge directement à partir de clients de toohello hello POP.
  
    Un serveur d’origine toohello revalidation demande entraîne généralement une demande a expiré. Dans l’ordre pour un toooccur _HIT TCP_EXPIRED, serveur d’origine hello doit indiquer qu’une version plus récente de l’élément multimédia de hello n’existe pas. Ce type de situation met généralement à jour les en-têtes Cache-Control et Expires de la ressource.
* TCP_EXPIRED _MISS - cet état est signalé lorsqu’une version plus récente d’un actif de mise en cache ayant expiré est pris en charge à partir du client de toohello hello POP. Cela se produit lorsque hello durée de vie d’un composant mis en cache a expiré (par exemple, expiré max-age) et le serveur d’origine hello retourne une version plus récente de cet élément multimédia. Cette nouvelle version de l’élément multimédia de hello sera pris en charge client de toohello au lieu de la version de mise en cache hello. En outre, elle est mises en cache sur le serveur de périphérie hello et client de hello.
* CONFIG_NOCACHE - cet état indique qu’une configuration spécifique au client sur notre bord POP empêché asset de hello mis en cache.
* NONE : cet état indique qu'une vérification de la fraîcheur du contenu du cache n'a pas été effectuée.
* TCP_ CLIENT_REFRESH _MISS - cet état est signalé lorsqu’un client HTTP (par exemple, un navigateur) force une tooretrieve bord POP une nouvelle version d’un élément multimédia obsolète à partir du serveur d’origine hello.
  
    Par défaut, nos serveurs empêchent un client HTTP de forcer notre tooretrieve de serveurs edge une nouvelle version de l’élément multimédia de hello hello serveur d’origine.
* TCP_ PARTIAL_HIT : cet état est signalé lorsqu'une demande de plage d'octets entraîne un accès à une ressource partiellement en cache. Hello a demandé une plage d’octets est immédiatement pris en charge à partir du client de toohello POP hello.
* UNCACHEABLE - cet état est signalé lorsque Cache-Control et des en-têtes de la date d’expiration d’un élément multimédia indiquent qu’il ne doit pas être mis en cache sur un POP ou hello HTTP client. Ces types de demandes sont servies à partir du serveur d’origine hello

## <a name="cache-hit-ratio"></a>Taux d'accès au cache
Ce rapport indique le pourcentage de hello de demandes mises en cache qui ont été traitées directement à partir du cache.

rapport de Hello fournit hello les détails suivants :

* Hello demandé de contenu a été mis en cache sur le demandeur de toohello hello POP le plus proche.
* traitement de demande de Hello directement à partir de l’extrémité de hello de notre réseau.
* demande de Hello n’avait pas besoin de revalidation avec le serveur d’origine hello.

rapport de Hello n’inclut pas :

* Requêtes refusées en raison des options de filtrage toocountry.
* Les demandes de ressources dont les en-têtes indiquent qu'elles ne doivent pas être mises en cache. Par exemple, les en-têtes Cache-Control: private, Cache-Control: no-cache, ou Pragma: no-cache empêchent la mise en cache d’une ressource.
* Les demandes de plage d'octets pour le contenu partiellement mis en cache.

Hello formule est : (TCP_ positionnement / (positionnement TCP_ + TCP_MISS)) * 100

* Sélectionnez des données Date plage tooview par jour/semaine/mois, etc. ou entrer des dates personnalisées, puis toomake que votre sélection est mis à jour de « go ».
* Vous pouvez exporter et téléchargement des données en cliquant sur hello hello excel icône feuille située en regard de trop « go ».

![Rapport des taux d'accès au cache](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a>Données IPV4/IPV6 transférées
Ce rapport affiche la distribution de l’utilisation trafic hello dans IPV4 et IPV6.

![Données IPV4/IPV6 transférées](./media/cdn-reports/cdn-ipv4-ipv6.png)

* Sélectionnez les données de tooview plage Date par jour/semaine/mois, etc. ou entrer des dates personnalisées.
* Ensuite, cliquez sur toomake que votre sélection est mis à jour de « go ».

## <a name="considerations"></a>Considérations
Les rapports ne peuvent être générés dans hello 18 derniers mois.

