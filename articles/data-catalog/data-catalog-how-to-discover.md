---
title: "sources de données aaaHow toodiscover dans Azure Data Catalog | Documents Microsoft"
description: "Cet article présente comment toodiscover ressources de données référencées dans Azure Data Catalog, y compris la recherche et le filtrage et à l’aide de hello atteint des fonctionnalités de mise en surbrillance du portail d’Azure Data Catalog hello."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: f72ae3a3-6573-4710-89a7-f13555e1968c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 624834b8895dd50c8931c9d3e6f8dc217927c617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodiscover-data-sources-in-azure-data-catalog"></a>Comment des sources de données de toodiscover dans Azure Data Catalog
## <a name="introduction"></a>Introduction
Azure Data Catalog est un service cloud entièrement géré qui permet d’inscrire et de détecter les sources de données d’entreprise. En d’autres termes, Data Catalog aide les utilisateurs à détecter, comprendre et utiliser les sources de données, et permet aux organisations de mieux exploiter leurs données existantes. Après avoir enregistré une source de données avec le catalogue de données, ses métadonnées sont indexée par le service de hello, afin que vous pouvez rechercher facilement les données de salutation toodiscover que vous avez besoin.

## <a name="searching-and-filtering"></a>Recherche et filtrage
Dans Data Catalog, la détection utilise deux mécanismes principaux : la recherche et le filtrage.

La recherche est conçue toobe intuitif et puissant. Par défaut, les termes de recherche sont mises en correspondance par rapport à n’importe quelle propriété dans le catalogue de hello, y compris les annotations fourni par l’utilisateur.

Le filtrage est conçu toocomplement recherche. Vous pouvez sélectionner des caractéristiques telles que les experts, le type de source de données, le type d’objet ou les balises. Vous pouvez afficher uniquement les ressources de données correspondants et limiter les ressources de toomatching de résultats de recherche.

En utilisant une combinaison de recherche et de filtrage, vous pouvez naviguer rapidement les sources de données hello qui ont été enregistrés avec le catalogue de données toodiscover hello des sources de données que vous avez besoin.

## <a name="search-syntax"></a>Syntaxe de recherche
Bien que la recherche en texte libre hello par défaut est simple et intuitive, vous pouvez également utiliser la syntaxe de recherche de catalogue de données pour mieux contrôler les résultats de la recherche hello. Données catalogue recherche prend en charge hello suivant techniques :

| Technique | Utilisation | Exemple |
| --- | --- | --- |
| Recherche de base |Recherche de base à l’aide d’un ou plusieurs termes de recherche. Les résultats sont les actifs qui correspond à n’importe quelle propriété avec un ou plusieurs des termes hello spécifiés. |`sales data` |
| Étendue de la propriété |Retour uniquement des sources de données où le terme de recherche hello est mis en correspondance avec hello de propriété spécifiée. |`name:finance` |
| Opérateurs booléens |Les opérations booléennes permettent d’étendre et de limiter une recherche. |`finance NOT corporate` |
| Parenthèses de regroupement |Utilisez les parties toogroup de parenthèses de hello requête tooachieve d’isolation logique, en particulier en association avec des opérateurs booléens. |`name:finance AND (tags:Q1 OR tags:Q2)` |
| Opérateurs de comparaison |Utilisez des comparaisons autres que l’égalité pour les propriétés comportant des types de données numériques et de date. |`modifiedTime > "11/05/2014"` |

Pour plus d’informations sur la recherche dans le catalogue de données, consultez hello [Azure Data Catalog](https://msdn.microsoft.com/library/azure/mt267594.aspx) l’article.

## <a name="hit-highlighting"></a>Mise en surbrillance des correspondances
Lorsque vous affichez les résultats de la recherche, afficher les propriétés qui correspondent aux hello spécifié des termes de recherche (par exemple, le nom de la ressource données hello, description et les balises) sont mis en surbrillance toomake il plus facile tooidentify pourquoi une ressource donnée a été retournée par une recherche donnée.

> [!NOTE]
> tooturn hors d’atteinte de la mise en surbrillance, utilisez hello **mettre en surbrillance** basculer dans le portail du catalogue de données hello.
>
>

Lorsque vous affichez les résultats de la recherche, il n’est pas toujours évident de comprendre pourquoi une ressource de données a été retournée, même lorsque la mise en surbrillance des correspondances est activée. Étant donné que, par défaut, toutes les propriétés font l’objet de la recherche, une ressource de données peut être retournée si une correspondance avec une propriété de colonne est détectée. Et, étant donné que plusieurs utilisateurs peuvent annoter des ressources de données inscrits avec leurs balises et leurs descriptions, pas toutes les métadonnées peuvent être affichées dans la liste hello des résultats de la recherche.

Dans l’affichage en mosaïque hello par défaut, chaque mosaïque affiché dans les résultats de recherche hello inclut un **terme de recherche vue correspond à** icône, afin que vous pouvez rapidement afficher hello nombre de correspondances et leur emplacement et toojump toothem si vous le souhaitez.

 ![Atteindre la mise en surbrillance et les occurrences trouvées dans le portail d’Azure Data Catalog hello](./media/data-catalog-how-to-discover/search-matches.png)

## <a name="summary"></a>Résumé
Étant donné que l’inscription d’une source de données avec des copies de données catalogue structurelles et descriptifs toohello service du catalogue de source de métadonnées à partir des données de hello, devient plus facile toodiscover hello source de données et comprendre. Après avoir enregistré une source de données, vous pouvez identifier par l’utilisation du filtrage et Explorer à partir de portail du catalogue de données hello.

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations détaillées sur la façon toodiscover des sources de données, consultez [prise en main Azure Data Catalog](data-catalog-get-started.md).
