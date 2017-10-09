---
title: "aaaData cas d’utilisation en usine - recommandations de produits"
description: "Découvrez un cas d'utilisation implémenté à l'aide d’Azure Data Factory et d'autres services."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6f1523c7-46c3-4b8d-9ed6-b847ae5ec4ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: d7912965fe4762d64e8ca3c28381ea6187f36631
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---product-recommendations"></a>Cas d’utilisation - Recommandations de produits
Azure Data Factory est un des nombreux services utilisés de tooimplement hello Cortana Intelligence Suite d’accélérateurs de solutions.  Consultez la page [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics) pour plus de détails. Dans ce document, nous décrivons un cas d’utilisation courant que les utilisateurs Azure ont déjà résolu et implémenté à l’aide d’Azure Data Factory et d’autres services Cortana Intelligence.

## <a name="scenario"></a>Scénario
Magasins en ligne choix couramment tooentice leurs produits toopurchase de clients en leur présentation avec les produits qu’ils sont probablement toobe intéressé et toobuy donc plus probable. tooaccomplish, magasins en ligne doivent toocustomize expérience en ligne des utilisateurs à l’aide personnalisée de produits recommandés pour un utilisateur spécifique. Ces recommandations personnalisées sont toobe prise en fonction de leurs données actuelles et historiques d’achat comportement, informations de produit, a récemment introduits marques et les données de segmentation du client et du produit.  En outre, qu’ils puissent fournir des recommandations de produits hello utilisateur basées sur l’analyse du comportement de l’utilisation globale de tous les utilisateurs de leurs combinées.

objectif Hello de ces détaillants est toooptimize pour les conversions de clic à la vente d’utilisateur et gagnez des affaires plus élevé.  Ils parviennent à effectuer cette conversion en proposant des recommandations de produits contextuelles basées sur les habitudes, les centres d’intérêt et les actions du client. Pour ce cas de figure, nous utilisons des magasins en ligne par exemple, pour les entreprises qui souhaitent toooptimize pour leurs clients. Toutefois, ces principes s’appliquent tooany entreprise qui veut tooengage ses clients autour de ses produits et les services et amélioreront l’expérience d’achat leurs clients des recommandations de produits personnalisés.

## <a name="challenges"></a>Défis
De nombreux défis sont auxquelles sont confrontées les magasins en ligne lors de la tentative de tooimplement ce type de cas d’usage. 

Tout d’abord, les données de différentes tailles et de formes doivent être transférées vers plusieurs sources de données à la fois localement et dans le cloud de hello. Ces données incluent les données de produit, les données de comportement d’historique et les données utilisateur comme utilisateur de hello navigue sur le site de vente au détail en ligne hello. 

Deuxièmement, les recommandations de produits personnalisées doivent être anticipées et évaluées de manière raisonnable et précise. En outre tooproduct, de marque et de données de comportement et le navigateur client, magasins en ligne doivent également tooinclude commentaires des clients sur les dernières toofactor achats dans la détermination de hello de meilleures recommandations de produits hello pour l’utilisateur de hello. 

Enfin, les recommandations hello doivent être immédiatement livrable toohello utilisateur tooprovide une navigation transparente et une expérience d’achat et fournissent des recommandations les plus récents et pertinentes hello. 

Enfin, détaillants doivent efficacité de hello toomeasure de l’approche en effectuant le suivi de la vente incitative globale croiséesent réussites de ventes de conversion en un clic et ajuster les recommandations futures tootheir.

## <a name="solution-overview"></a>Vue d’ensemble de la solution
Cet exemple de cas d’utilisation a été résolu et implémenté par de vrais utilisateurs Azure avec Azure Data Factory et d’autres services Cortana Intelligence, notamment [HDInsight](https://azure.microsoft.com/services/hdinsight/) et [Power BI](https://powerbi.microsoft.com/).

site de vente en ligne Hello utilise un magasin d’objets Blob Azure, un local SQL server, base de données SQL Azure et un Datamart relationnelle en tant que leurs options de stockage de données dans l’ensemble de flux de travail hello.  magasin d’objets blob Hello contient des informations sur les clients, les données de comportement client et les données des informations de produit. informations sur les produits Hello données incluent des informations de marque de produit et un catalogue de produits stockés localement dans un entrepôt de données SQL. 

Toutes les données de hello sont combinées et chargées dans un produit recommandation système toodeliver personnalisée basées sur intérêts du client et les actions, tandis que l’utilisateur de hello parcourt les produits dans le catalogue hello sur le site Web de hello. les clients Hello également voient que les produits associés produit toohello qu’ils cherchent à basé sur des modèles d’utilisation du site Web global qui ne sont pas associée tooany un utilisateur.

![diagramme de cas d'utilisation](./media/data-factory-product-reco-usecase/diagram-1.png)

Gigaoctets de fichiers journaux web brutes sont générés tous les jours à partir du site Web du détaillant hello en ligne en tant que fichiers semi-structurées. Hello des fichiers journaux web brut et informations du catalogue customer et product hello sont régulièrement intégrées dans un stockage d’objets Blob Azure à l’aide du mouvement de données globalement déployées de la fabrique de données en tant que service. les fichiers journaux brutes Hello pour le jour de hello sont partitionnés (par année et mois) dans le stockage d’objets blob pour le stockage à long terme.  [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) sont fichiers de journal brut hello toopartition utilisé dans l’objet blob de hello magasin et processus de journaux hello ingéré à grande échelle à l’aide de scripts Hive et Pig. Hello journaux web partitionné les données sont ensuite traité tooextract hello nécessaires entrées pour un apprentissage des recommandations de produits recommandation système toogenerate hello personnalisé.

système de recommandation utilisé pour l’apprentissage hello dans cet exemple Hello est une plate-forme de recommandation d’apprentissage open source [Apache Mahout](http://mahout.apache.org/).  N’importe quel [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) ou le modèle personnalisé peut être appliqué toohello scénario.  modèle de Mahout Hello est utilisé toopredict hello similitude des éléments sur le site Web de hello basé sur des modèles d’utilisation générale et toogenerate hello personnalisée basées sur les utilisateurs individuels hello.

Enfin, le jeu de résultats de hello des recommandations de produits personnalisé est déplacé tooa relationnelle Datamart pour la consommation par le site Web du site de vente hello.  jeu de résultats Hello est également accessible directement à partir de stockage d’objets blob par une autre application ou déplacé tooadditional magasins pour d’autres consommateurs et les cas d’usage.

## <a name="benefits"></a>Avantages
En optimisant leur stratégie de recommandation de produit et les aligner avec les objectifs, la solution de hello remplie merchandising détaillant hello en ligne et commercialisation des objectifs. En outre, ils ont été en mesure de toooperationalize et gérer des flux de travail de recommandation hello produit de manière efficace, fiable et économique. approche de Hello facilite leur tooupdate leur modèle et à affiner son efficacité basée sur les mesures hello de ventes réussites de conversion en un clic. À l’aide de Azure Data Factory, ils ont été tooabandon en mesure de leur gestion des ressources fastidieux et onéreux cloud manuelle et déplacement la gestion des ressources de cloud tooon à la demande. Par conséquent, ils ont été toosave en mesure de temps et d’argent et réduisent les temps de déploiement toosolution. Vues lignage des données et l’intégrité du service opérationnel est devenue toovisualize facile et résoudre les problèmes avec hello intuitive Data Factory analyse et gestion de l’interface utilisateur disponible à partir de hello portail Azure. Leur solution peut maintenant être planifiée et gérée afin que les données terminées sont fiable générées et remises toousers et données et les dépendances de traitement sont gérées automatiquement sans intervention humaine.

En fournissant cette expérience d’achat personnalisée, hello en ligne détaillant créé un client plus de concurrence, mobilisation rencontrer et par conséquent augmenter la satisfaction des clients de ventes et globale.

