---
title: "sources de données de profil aaaHow tooData"
description: "Tooarticle de la mise en surbrillance comment les données de niveau table ou colonne tooinclude profils lors de l’inscription des sources de données dans Azure Data Catalog et comment les données toouse profils toounderstand des sources de données."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a>Profilage de données dans des sources de données
## <a name="introduction"></a>Introduction
**Microsoft Azure Data Catalog** est un service cloud entièrement géré qui sert de système d'inscription et de détection des sources de données d'entreprise. En d’autres termes, **Azure Data Catalog** est tout sur aidant les utilisateurs à découvrir, comprendre et utiliser des sources de données, et aider les organisations tooget plus la valeur à partir de leurs données. Quand une source de données est enregistrée avec **Azure Data Catalog**, ses métadonnées sont copiée et est indexée par le service de hello, mais un récit hello ne se termine pas il.

Hello **profilage des données** fonctionnalité de **Azure Data Catalog** examine hello des données à partir de sources de données pris en charge dans votre catalogue et collecte des statistiques et les informations relatives à ces données. Il est facile tooinclude un profil de vos ressources de données. Lorsque vous inscrivez une ressource de données, choisissez **inclure un profil de données** dans l’outil de l’enregistrement de source de données hello.

## <a name="what-is-data-profiling"></a>Qu’est-ce que le profilage de données ?
Profilage des données examine les données de hello dans la source de données hello en cours d’inscription et collecte des statistiques et les informations relatives à ces données. Pendant la découverte de source de données, ces statistiques peuvent vous aider à déterminer adéquation hello de hello données toosolve leur problème professionnel.

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

Hello sources de données suivantes prennent en charge le profilage des données :

* Vues et tables SQL Server (y compris la base de données SQL Azure et Azure SQL Data Warehouse)
* Tables et vues Oracle
* Tables et vues Teradata
* Tables Hive

L’inclusion de profils de données lors de l’inscription de ressources de données permet à l’utilisateur de répondre à certaines questions sur les sources de données, notamment :

* Il peut être utilisé toosolve mon problème d’entreprise ?
* Les données de salutation est conforme tooparticular normes ou modèles ?
* Quelles sont les anomalies hello hello de source de données ?
* Quelles sont les difficultés que je risque de rencontrer en intégrant ces données dans mon application ?

> [!NOTE]
> Vous pouvez également ajouter la documentation tooan asset toodescribe comment les données peuvent être intégrées dans une application. Consultez [comment toodocument des sources de données](data-catalog-how-to-documentation.md).
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a>Comment tooinclude une profil des données lorsque l’inscription d’une source de données
Il est facile tooinclude un profil de votre source de données. Lorsque vous enregistrez une source de données, Bonjour **toobe objets inscrits** Panneau de configuration de l’enregistrement de source de données hello d’outils, choisissez **inclure un profil de données**.

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

toolearn savoir plus sur les sources de données tooregister, voir [comment les sources de données tooregister](data-catalog-how-to-register.md) et [prise en main Azure Data Catalog](data-catalog-get-started.md).

## <a name="filtering-on-data-assets-that-include-data-profiles"></a>Filtrage sur des ressources de données comprenant des profils de données
toodiscover les ressources de données qui incluent un profil des données, vous pouvez inclure `has:tableDataProfiles` ou `has:columnsDataProfiles` comme l’un de vos termes de recherche.

> [!NOTE]
> En sélectionnant **inclure un profil de données** dans les données de salutation outil d’inscription source inclut table et les informations de profil au niveau de la colonne. Toutefois, hello API de catalogue de données permet de données actifs toobe inscrit avec un seul jeu d’informations de profil inclus.
>
>

## <a name="viewing-data-profile-information"></a>Affichage des informations de profil de données
Une fois que vous trouvez une source de données adapté à un profil, vous pouvez afficher les détails du profil de données hello. les données de salutation tooview de profil, sélectionnez une ressource de données et choisissez **profil des données** dans la fenêtre du portail hello catalogue de données.

![](media/data-catalog-data-profile/data-catalog-view.png)

Un profil de données dans **Azure Data Catalog** affiche les informations de profil au niveau de la table et au niveau de la colonne :

### <a name="object-data-profile"></a>Profil de données au niveau objet
* Nombre de lignes
* Taille de la table
* Lorsque les objets hello a été modifié

### <a name="column-data-profile"></a>Profil de données au niveau colonne
* Type de données de colonne
* Nombre de valeurs distinctes
* Nombre de lignes contenant des valeurs NULL
* Valeurs minimale, maximale, moyenne et d’écart type des colonnes

## <a name="summary"></a>Résumé
Fournit des statistiques de profilage des données et informations inscrit toohelp actifs de données vous déterminez la capacité d’adaptation hello hello données toosolve de problèmes d’entreprise. Outre l’annotation et la documentation de sources de données, les profils de données peuvent permettre aux utilisateurs de mieux comprendre vos données.

## <a name="see-also"></a>Voir aussi
* [Comment tooregister des sources de données](data-catalog-how-to-register.md)
* [Prise en main d’Azure Data Catalog](data-catalog-get-started.md)
