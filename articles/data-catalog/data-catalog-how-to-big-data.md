---
title: "toowork aaaHow des sources de données de « données volumineuses » | Documents Microsoft"
description: "Modèles de mise en surbrillance tooarticle de procédure pour l’utilisation d’Azure Data Catalog des sources de données de « données volumineuses », y compris le stockage d’objets Blob Azure, Azure Data Lake et Hadoop HDFS."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a>Comment toowork avec les données sources dans Azure Data Catalog
## <a name="introduction"></a>Introduction
**Microsoft Azure Data Catalog** est un service cloud entièrement géré qui sert de système d'inscription et de détection des sources de données d'entreprise. Il concerne toutes les personnes découvrir, comprendre et utiliser des sources de données et de contribuer aux organisations tooget plus de valeur à partir de leurs sources de données existantes, y compris les données volumineuses.

**Azure Data Catalog** prend en charge hello d’enregistrement des objets BLOB de stockage d’objets BLOB Azure et des répertoires ainsi que des fichiers de Hadoop HDFS et des répertoires. nature de semi-structurées Hello de ces sources de données offre une grande souplesse. Toutefois, tooget hello le meilleur parti de l’inscription avec **Azure Data Catalog**, les utilisateurs doivent envisager la façon dont les sources de données hello sont organisés.

## <a name="directories-as-logical-data-sets"></a>Répertoires sous forme de jeux de données logiques
Il est courant pour organiser les sources de données volumineuses tootreat répertoires en tant que jeux de données logique. Répertoires de niveau supérieur sont toodefine utilisé un jeu de données, tandis que les sous-dossiers définissent des partitions et des fichiers hello qu’ils contiennent stockent des données de hello lui-même.

Voici quelques exemples de ce modèle :

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

Dans cet exemple, vehicle_maintenance_events et location_tracking_events représentent les jeux de données logiques. Chacun de ces dossiers contient des fichiers de données organisés par année et par mois en sous-dossiers. Chacun de ces dossiers peut contenir des centaines ou des milliers de fichiers.

Dans ce modèle, l’enregistrement des fichiers individuels auprès d’ **Azure Data Catalog** ne sert sans doute à rien. Au lieu de cela, inscrivez les répertoires hello qui représentent des jeux de données hello être significatif toohello aux utilisateurs qui travaillent avec des données hello.

## <a name="reference-data-files"></a>Référence de fichiers de données
Un modèle complémentaire est jeux de données de référence toostore en tant que fichiers individuels. Ces jeux de données peut être considéré comme le côté « small » de hello de données volumineuses et sont souvent toodimensions similaires dans un modèle de données analytiques. Les fichiers de données de référence contiennent des enregistrements contexte tooprovide utilisées en bloc de hello hello des fichiers de données stockés ailleurs dans le magasin de données volumineuses hello.

Voici quelques exemples de ce modèle :

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

Quand un chercheur analyste ou données collabore avec données hello contenues dans les grandes structures de répertoire hello, données hello dans ces fichiers de référence peuvent être utilisé tooprovide des informations plus détaillées pour les entités qui sont visés tooonly par nom ou ID dans les données plus grandes hello ensemble.

Dans ce modèle, il est logique des fichiers de données de référence de hello tooregister avec **Azure Data Catalog**. Chaque fichier représente un jeu de données, et chacun d’eux peut être annoté et découvert individuellement.

## <a name="alternate-patterns"></a>Modèles alternatifs
Hello modèles décrits dans la précédente section de hello deux méthodes sont possibles qu'un magasin de données volumineuses peut être organisé, mais chaque implémentation est différente. Quelle que soit la façon dont vos sources de données sont structurées, lors de l’inscription des sources de données volumineuses avec **Azure Data Catalog**, se concentrer sur l’enregistrement des fichiers de hello et de répertoires qui représentent des jeux de données hello de tooothers valeur au sein de votre organisation. L’inscription de tous les fichiers et répertoires permettre encombrer catalogue hello, rend plus difficile pour les utilisateurs toofind dont ils ont besoin.

## <a name="summary"></a>Résumé
L’inscription des sources de données avec **Azure Data Catalog** rend plus facile toodiscover et à comprendre. En enregistrant et annoter les fichiers de données volumineuses hello et de répertoires qui représentent des jeux de données logiques, les utilisateurs peuvent aider à trouver et utiliser des sources de données volumineuses hello que dont ils ont besoin.
