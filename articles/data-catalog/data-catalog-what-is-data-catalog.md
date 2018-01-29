---
title: "Introduction à Azure Data Catalog | Microsoft Docs"
description: "Cet article présente Microsoft Azure Data Catalog, notamment ses fonctionnalités et les problèmes qu’il résoud. Data Catalog permet à n’importe quel utilisateur de s’inscrire, de découvrir, de comprendre et d’utiliser des sources de données."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: cc733907-17ec-4153-9f0c-5b3754b2db19
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 01/18/2018
ms.author: maroche
ms.openlocfilehash: edf6e1d8b86d9773b54353bb70f000bcdf40e5ec
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="what-is-azure-data-catalog"></a>Qu’est-ce qu’Azure Data Catalog ?
Azure Data Catalog est un service cloud entièrement géré dont les utilisateurs peuvent détecter les sources de données, et comprendre les sources de données qu’ils recherchent. Dans le même temps, Data Catalog permet aux organisations de mieux exploiter leurs investissements existants. 

Avec Data Catalog, n’importe quel utilisateur (analyste, scientifique de données ou développeur) peut détecter, comprendre et utiliser des sources de données. Data Catalog inclut un modèle de crowdsourcing de métadonnées et des annotations. Il centralise l’ensemble des éléments qui permettent aux utilisateurs d’une organisation de partager leurs connaissances et de créer une communauté et une culture des données.

## <a name="discovery-challenges-for-data-consumers"></a>Défis des consommateurs de données en matière de découverte
La détection de sources de données d’entreprise est un processus organique basé sur des connaissances tribales. Cette approche présente de nombreux défis aux entreprises qui souhaitent tirer le meilleur parti de leurs informations :

* Les utilisateurs peuvent ne pas être conscients qu’une source de données existe, tant qu’ils ne sont pas en contact avec cette dernière dans le cadre d’un autre processus. Les sources de données ne sont pas enregistrées de manière centralisée.
* À moins que les utilisateurs connaissent l’emplacement d’une source de données, ils ne peuvent pas se connecter aux données à l’aide d’une application cliente. Les expériences d’utilisation de données requièrent de la part des utilisateurs de connaître la chaîne de connexion ou le chemin d’accès.
* À moins de connaître l’emplacement de la documentation d’une source données, les utilisateurs ne peuvent pas comprendre les utilisations prévues des données. La documentation et les sources de données peuvent se trouver à différents emplacements et être utilisées par le biais d’expériences diverses.
* Si les utilisateurs ont des questions sur une ressource d’informations, ils doivent localiser l’expert ou l’équipe responsable des données et les faire intervenir en mode hors connexion. Il n’existe aucune rapport explicite entre les données et celles auxquelles des perspectives d’experts sur leur utilisation sont associées.
* Sauf si un utilisateur comprend le processus de demande d’accès à la source de données, la détection de la source de données et de sa documentation ne lui permet toujours pas d’accéder aux données.

## <a name="discovery-challenges-for-data-producers"></a>Défis des producteurs de données en matière de découverte
Pendant que les consommateurs de données relèvent les défis mentionnés précédemment, les utilisateurs responsables de la production et de la gestion des ressources d’informations relèvent, quant à eux, des défis qui leur sont propres :

* L’annotation des sources de données avec des métadonnées descriptives est souvent peine perdue. En général, les applications clientes ignorent les descriptions stockées dans la source de données.
* La création de documentation pour les sources de données est souvent peine perdue. La synchronisation de la documentation avec des sources de données est une responsabilité permanente, et les utilisateurs pourraient ne plus avoir confiance en une documentation perçue comme étant obsolète.
* Créer et gérer une documentation pour des sources de données est une tâche plutôt longue et complexe. Rendre disponible cette documentation pour tous les utilisateurs de la source de données peut l’être plus encore.
* Restreindre l’accès à la source de données et veiller à ce que les utilisateurs de données sachent comment demander l’accès est un défi récurrent.

Lorsqu’ils sont combinés, ces défis représentent un obstacle majeur pour les entreprises qui souhaitent encourager et promouvoir l’utilisation et la compréhension des données d’entreprise.

## <a name="azure-data-catalog-can-help"></a>Azure Data Catalog peut être utile
Data Catalog est conçu pour résoudre ces problèmes et permettre aux entreprises de tirer le meilleur parti de leurs ressources d’informations existantes. Data Catalog rend les sources de données facilement détectables et compréhensibles par les utilisateurs qui gèrent les données.

Data Catalog fournit un service cloud dans lequel une source de données peut être inscrite. Les données restent à leur emplacement existant, mais une copie de leurs métadonnées, ainsi qu’une référence à l’emplacement de la source de données, sont ajoutées à Data Catalog. Les métadonnées sont également indexées de manière à ce que chaque source de données soit facilement détectable via la recherche, et compréhensible pour les utilisateurs qui la découvrent.

Une fois qu’une source de données a été inscrite, ses métadonnées peuvent ensuite être enrichies, par l’utilisateur qui a réalisé l’inscription ou par d’autres utilisateurs de l’entreprise. Tous les utilisateurs peuvent annoter une source de données en fournissant des descriptions, des balises ou d'autres métadonnées, telles que de la documentation, et traiter la demande d’accès à la source de données. Ces métadonnées descriptives complètent les métadonnées structurelles (telles que les noms de colonnes et les types de données) inscrites à partir de la source de données.

La détection, la compréhension et l’utilisation des sources de données sont le principal objectif de l’inscription des sources. Les utilisateurs professionnels peuvent avoir besoin de données pour le décisionnel, le développement d’applications, la science des données ou toute autre tâche nécessitant des données adéquates. Ils peuvent utiliser l’expérience de détection de Data Catalog pour rechercher rapidement des données qui correspondent à leurs besoins, comprendre les données pour évaluer leur pertinence par rapport à l’utilisation et utiliser les données en ouvrant la source de données dans l’outil de leur choix. 

Dans le même temps, les utilisateurs peuvent contribuer au catalogue en balisant, en documentant et en annotant les sources de données qui ont déjà été enregistrées. Ils peuvent également enregistrer de nouvelles sources de données, qui peuvent ensuite être détectées, comprises et utilisées par la communauté d’utilisateurs du catalogue.

![Fonctionnalités Data Catalog](./media/data-catalog-what-is-data-catalog/data-catalog-capabilities.png)

## <a name="learn-more-about-data-catalog"></a>En savoir plus sur Data Catalog
Pour en savoir plus sur les fonctions de Data Catalog, voir :

* [Inscription de sources de données](data-catalog-how-to-register.md)
* [Détection de sources de données](data-catalog-how-to-discover.md)
* [Annotation de sources de données](data-catalog-how-to-annotate.md)
* [Comment documenter des sources de données](data-catalog-how-to-documentation.md)
* [Connexion aux sources de données](data-catalog-how-to-connect.md)
* [Travail avec du Big Data](data-catalog-how-to-big-data.md)
* [Gestion des ressources de données](data-catalog-how-to-manage.md)
* [Configuration du glossaire métier](data-catalog-how-to-business-glossary.md)
* [Forum Aux Questions](data-catalog-frequently-asked-questions.md)

## <a name="next-steps"></a>étapes suivantes
Pour prendre en main Data Catalog, accédez à :
* [Microsoft Azure Data Catalog](https://www.azuredatacatalog.com)
* [Prise en main d’Azure Data Catalog](data-catalog-get-started.md)
