---
title: "aaaCreate un index Azure Search | Microsoft Azure | Service de recherche de cloud hébergé"
description: "Qu’est-ce qu’un index dans Azure Search et comment l’utiliser ?"
services: search
documentationcenter: 
author: ashmaka
ms.assetid: a395e166-bf2e-4fca-8bfc-116a46c5f7b1
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: c01cc654ff91427c8f1569b2f5b060a0a0f044c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index"></a>Création d'un index Azure Search
> [!div class="op_single_selector"]
> * [Vue d'ensemble](search-what-is-an-index.md)
> * [Portail](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

## <a name="what-is-an-index"></a>Qu’est-ce qu’un index ?
Un *index* est une banque permanente de *documents* et d’autres éléments utilisés par un service Azure Search. Un document correspond à une unité de données pouvant faire l’objet d’une recherche dans votre index. Par exemple, un détaillant de commerce électronique peut posséder un document pour chaque article qu’il vend, un organisme d’information peut posséder un document par article, etc. Ces équivalents de base de données familière toomore concepts de mappage : un *index* est conceptuellement semblable tooa *table*, et *documents* sont à peu près équivalente trop*lignes* dans une table.

Lorsque vous ajoutez/téléchargement des documents et soumettre des requêtes de recherche tooAzure recherche, vous envoyez votre index spécifique de demandes tooa dans votre service de recherche.

## <a name="field-types-and-attributes-in-an-azure-search-index"></a>Types et attributs de champ dans un index Azure Search
Lorsque vous définissez votre schéma, vous devez spécifier hello nom, type et les attributs de chaque champ dans votre index. type de champ Hello répartit les données hello qui sont stockées dans le champ. Les attributs sont définis sur des champs individuels toospecify utilisation hello champ. Hello tableaux suivants énumérer les types hello et vous pouvez spécifier des attributs.

### <a name="field-types"></a>Types de champ
| Type | Description |
| --- | --- |
| *Edm.String* |Texte pouvant éventuellement être tokenisé pour la recherche en texte intégral (césure de mots, recherche de radical, etc). |
| *Collection(Edm.String)* |Liste de chaînes pouvant être éventuellement tokenisées pour la recherche en texte intégral. Il n’existe aucune limite théorique supérieure sur nombre hello d’éléments dans une collection, mais limite supérieure de 16 Mo hello sur la taille de la charge s’applique toocollections. |
| *Edm.Boolean* |Contient des valeurs true/false. |
| *Edm.Int32* |Valeurs entières 32 bits. |
| *Edm.Int64* |Valeurs entières 64 bits. |
| *Edm.Double* |Données numériques à double précision. |
| *Edm.DateTimeOffset* |Les valeurs d’heure représentées dans le format hello OData V4 de date (par exemple, `yyyy-MM-ddTHH:mm:ss.fffZ` ou `yyyy-MM-ddTHH:mm:ss.fff[+/-]HH:mm`). |
| *Edm.GeographyPoint* |Un point qui représente un emplacement géographique globe de hello. |

Pour plus d’informations sur les types de données pris en charge par le service Recherche Azure, consultez [cet article](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types).

### <a name="field-attributes"></a>Attributs de champ
| Attribut | Description |
| --- | --- |
| *Clé* |Chaîne qui fournit l’ID unique de hello de chaque document, utilisé pour rechercher des documents. Chaque index doit avoir une clé. Qu’un seul champ valeur peut être hello clé et son type doit être défini à tooEdm.String. |
| *Affichable dans les résultats d’une recherche* |Définit si un champ peut être retourné dans un résultat de recherche. |
| *Filtrable* |Permet de hello toobe de champ utilisé dans les requêtes de filtre. |
| *Triable* |Permet à une requête toosort les résultats de recherche à l’aide de ce champ. |
| *À choix multiple* |Permet à un toobe champ utilisé dans un [une navigation par facettes](search-faceted-navigation.md) structure pour le filtrage automatique orienté utilisateur. En général, les champs contenant des valeurs répétitives que vous pouvez utiliser toogroup plusieurs documents ensemble (par exemple, plusieurs documents qui répondent à une seule marque ou d’une catégorie de service) fonctionnent mieux en tant que facettes. |
| *Possibilité de recherche* |Marques hello champ en tant que recherches de texte intégral. |

Pour plus d’informations sur les attributs d’index du service Recherche Azure, consultez [cet article](https://docs.microsoft.com/rest/api/searchservice/Create-Index).

## <a name="guidance-for-defining-an-index-schema"></a>Instructions de définition d’un schéma d’index
Lorsque vous concevez votre index, prenez votre temps Bonjour toothink phase via chaque décision de planification. Il est important de conserver votre recherche utilisateur expérience et des besoins à l’esprit lorsque vous concevez votre index en tant que chaque champ doit être attribuée hello [attributs corrects](https://docs.microsoft.com/rest/api/searchservice/Create-Index). La modification d’un index après son déploiement implique la reconstruction et de recharger les données de salutation.

Si vos besoins en stockage de données changent au fil du temps, vous pouvez augmenter ou diminuer la capacité en ajoutant ou en supprimant des partitions. Pour plus d’informations, consultez [Gérer votre service de recherche dans Azure](search-manage.md) ou [Limites de service](search-limits-quotas-capacity.md).

