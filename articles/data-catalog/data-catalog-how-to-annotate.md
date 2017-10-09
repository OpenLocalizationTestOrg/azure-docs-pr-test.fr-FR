---
title: "sources de données aaaHow tooannotate | Documents Microsoft"
description: "Mise en surbrillance de la procédure-tooarticle comment tooannotate les ressources de données dans Azure Data Catalog, y compris les noms conviviaux, les balises, les descriptions et les experts."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5a7e6bb2-863c-4eca-b614-1c814920d9ed
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 1d1ef34e3f1ef73cdc65129209d938abe1e36c01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooannotate-data-sources"></a>Comment tooannotate des sources de données
## <a name="introduction"></a>Introduction
**Microsoft Azure Data Catalog** est un service cloud entièrement géré qui sert de système d'inscription et de détection des sources de données d'entreprise. En d’autres termes, le catalogue de données concerne toutes les personnes découvrir, comprendre et utiliser des sources de données et de contribuer aux organisations tooget plus de valeur à partir de leurs données. Lorsqu’une source de données est enregistrée avec le catalogue de données, ses métadonnées sont copiée et est indexée par le service de hello, mais un récit hello ne se termine pas il. Catalogue de données permet les utilisateurs tooprovide leurs propres métadonnées de hello toosupplement métadonnées descriptives – tels que des descriptions et des balises – extraites à partir de la source de données hello et plus compréhensible toomore personnes de source de données de hello toomake.

## <a name="annotation-and-crowdsourcing"></a>Annotation et crowdsourcing
Tout le monde possède un avis. Et c’est une bonne chose.
Avec Data Catalog, les perspectives de chaque utilisateur à l’égard des sources de données d’entreprise sont prises en compte et valorisées. Tenez compte des hello scénario :

* administrateur du système Hello sait contrat de niveau de service hello pour hello serveurs ou services de cette source de données hôte hello.
* administrateur de base de données Hello sait sauvegarde de hello planifier pour chaque base de données et hello autorisée ETL pour windows.
* propriétaire du système Hello sait processus hello pour la source de données toohello utilisateurs toorequest accès.
* Gestionnaire de données Hello sait comment les ressources hello et les attributs dans la source de données hello mappent le modèle de données d’entreprise toohello.
* analyste de Hello sait comment les données de hello sont utilisées dans le contexte de hello hello des processus d’entreprise qu’il prend en charge.

Chacune de ces perspectives est un outil précieux, et le catalogue de données utilise un toometadata approche marketing participatif qui permet de chaque un toobe capturée et utilisé tooprovide une image complète des sources de données enregistrées. À l’aide du portail de catalogue de données hello, chaque utilisateur peut ajouter et modifier son propre annotations, tout en étant en mesure de tooview les annotations fournies par d’autres utilisateurs.

## <a name="different-types-of-annotations"></a>Différents types d’annotations
Données catalogue hello de prend en charge les types d’annotations suivants :

| Annotation | Remarques |
| --- | --- |
| Nom convivial |Les noms conviviaux peuvent être fournies au niveau de ressource de données hello, ressources de données toomake hello plus compréhensible. Les noms conviviaux sont particulièrement utiles quand un nom objet sous-jacent hello toousers difficiles à déchiffrer, abrégé ou sinon pas significatif. |
| Description |Descriptions peuvent être fournies à la ressource de données hello et d’attribut / niveaux de colonne. Les descriptions sont des annotations de texte courte de forme libre qui décrivent hello utilisateur sur la ressource de données hello ou son utilisation. |
| Balises (balises utilisateur) |Les balises peuvent être fournies à la ressource de données hello et d’attribut / niveaux de colonne. Balises de l’utilisateur sont des étiquettes définies par l’utilisateur qui peuvent être utilisés toocategorize les ressources de données ou d’attributs. |
| Balises (balises glossaire) |Les balises peuvent être fournies à la ressource de données hello et d’attribut / niveaux de colonne. Les balises de glossaire sont définies de manière centralisée glossaire qui peut être utilisé toocategorize les ressources de données ou des attributs à l’aide d’une taxonomie commune de business. Pour plus d’informations, consultez [comment tooset des hello glossaire métier pour baliser les régie](data-catalog-how-to-business-glossary.md) |
| Experts |Experts peuvent être fournies au niveau de hello données actif. Experts identifient des utilisateurs ou des groupes à des experts perspectives sur les données de salutation et peuvent servir de points de contact pour les utilisateurs de découvrir hello inscrit des sources de données et ont des questions qui ne sont pas traitées par les annotations existantes hello. |
| Demander l'accès |Accéder aux informations de demande peut être fournie au niveau de hello données actif. Ces informations sont pour les utilisateurs de découvrir une source de données qu’ils n’ont pas encore tooaccess d’autorisations. Les utilisateurs peuvent entrer l’adresse de messagerie hello de hello utilisateur ou un groupe qui accorde l’accès, hello URL du processus de hello ou outil que nécessaire aux utilisateurs l’accès toogain pouvez entrer des processus hello lui-même en tant que texte. |
| Documentation |Documentation peut être fournie au niveau de hello données actif. La documentation des ressources présente des informations complètes pouvant inclure des liens et des images et pouvant fournir des données non véhiculées par les descriptions et les balises. |

## <a name="annotating-multiple-assets"></a>Annotation de plusieurs ressources
Lorsque vous sélectionnez plusieurs ressources de données dans le portail du catalogue de données hello, les utilisateurs peuvent annoter toutes les ressources sélectionnées en une seule opération. Annotations applique actifs tooall sélectionné, rendant tooselect facile et fournir une description cohérente et les jeux de balises et les experts pour les ressources de données associées.

> [!NOTE]
> Les balises et les experts peuvent également être fournis lors de l’outil d’inscription de source de l’enregistrement des ressources de données à l’aide de données du catalogue de données hello.
>
>

Lorsque la sélection de plusieurs tables et vues, seules les colonnes que toutes les sélectionnées actifs ont en commun des données apparaîtront dans portail hello du catalogue de données. Ainsi, les balises tooprovide les utilisateurs et les descriptions de toutes les colonnes avec le même nom que celui de hello pour toutes les ressources sélectionnées.

## <a name="annotations-and-discovery"></a>Annotations et détection
Tout comme hello métadonnées extraites de la source de données hello lors de l’enregistrement sont ajoutée des index de recherche de catalogue de données toohello, fourni par l’utilisateur de métadonnées sont également indexée. Cela signifie que non seulement font annotations facilement pour les données de salutation toounderstand utilisateurs qu'il découvre, annotations facilitent également pour les ressources de données utilisateurs toodiscover hello annotée en effectuant une recherche à l’aide de conditions hello rendent toothem de sens.

## <a name="summary"></a>Résumé
L’inscription d’une source de données avec le catalogue de données identifiables que les données en copiant les métadonnées structurelles et descriptive à partir de la source de données hello dans hello service du catalogue. Une fois qu’une source de données a été enregistrée, les utilisateurs peuvent fournir toodiscover plus facile de toomake annotations et comprendre de portail du catalogue de données hello.

## <a name="see-also"></a>Voir aussi
* [Prise en main Azure Data Catalog](data-catalog-get-started.md) didacticiel pour plus d’informations détaillées sur la façon tooannotate des sources de données.
