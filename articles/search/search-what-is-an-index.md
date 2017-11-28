---
title: "Création d’un index Azure Search | Microsoft Azure | Service de recherche cloud hébergé"
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
ms.openlocfilehash: 7fc45273c0f71c727b7087949cc63bbb4111f866
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
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
Un *index* est une banque permanente de *documents* et d’autres éléments utilisés par un service Azure Search. Un document correspond à une unité de données pouvant faire l’objet d’une recherche dans votre index. Par exemple, un détaillant de commerce électronique peut posséder un document pour chaque article qu’il vend, un organisme d’information peut posséder un document par article, etc. Pour comparer avec des éléments de base de données plus familiers, d’un point de vue conceptuel, un *index* est similaire à une *table*, et les *documents* équivalent plus ou moins aux *lignes* d’une table.

Lorsque vous ajoutez/chargez des documents et soumettez des requêtes de recherche à Azure Search, vous envoyez vos demandes à un index spécifique dans votre service de recherche.

## <a name="field-types-and-attributes-in-an-azure-search-index"></a>Types et attributs de champ dans un index Azure Search
Lorsque vous définissez votre schéma, vous devez spécifier le nom, le type et les attributs de chaque champ de votre index. Le type de champ classifie les données stockées dans ce champ. Les attributs sont définis sur des champs individuels pour spécifier la façon dont le champ est utilisé. Les tableaux ci-après énumèrent les types et les attributs que vous pouvez spécifier.

### <a name="field-types"></a>Types de champ
| Type | Description |
| --- | --- |
| *Edm.String* |Texte pouvant éventuellement être tokenisé pour la recherche en texte intégral (césure de mots, recherche de radical, etc). |
| *Collection(Edm.String)* |Liste de chaînes pouvant être éventuellement tokenisées pour la recherche en texte intégral. En théorie, il n’existe pas de limite supérieure quant au nombre d’éléments d’une collection, mais la limite supérieure de 16 Mo sur la taille de charge utile s’applique aux collections. |
| *Edm.Boolean* |Contient des valeurs true/false. |
| *Edm.Int32* |Valeurs entières 32 bits. |
| *Edm.Int64* |Valeurs entières 64 bits. |
| *Edm.Double* |Données numériques à double précision. |
| *Edm.DateTimeOffset* |Dates et heures représentées au format OData V4 (par exemple, `yyyy-MM-ddTHH:mm:ss.fffZ` ou `yyyy-MM-ddTHH:mm:ss.fff[+/-]HH:mm`). |
| *Edm.GeographyPoint* |Point représentant un emplacement géographique de la planète. |

Pour plus d’informations sur les types de données pris en charge par le service Recherche Azure, consultez [cet article](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types).

### <a name="field-attributes"></a>Attributs de champ
| Attribut | Description |
| --- | --- |
| *Clé* |Chaîne fournissant un ID unique à chaque document utilisé pour rechercher des documents. Chaque index doit avoir une clé. Un seul champ peut être la clé, et son type doit être défini sur Edm.String. |
| *Affichable dans les résultats d’une recherche* |Définit si un champ peut être retourné dans un résultat de recherche. |
| *Filtrable* |Permet d’utiliser le champ dans des requêtes de filtre. |
| *Triable* |Permet à une requête de trier les résultats de recherche à l’aide de ce champ. |
| *À choix multiple* |Permet d’utiliser un champ pour le filtrage autonome dans une structure de [navigation par facettes](search-faceted-navigation.md) par un utilisateur. En général, les champs contenant des valeurs répétitives que vous pouvez utiliser pour regrouper plusieurs documents (par exemple, plusieurs documents appartenant à une seule marque ou catégorie de service) sont les mieux adaptés en tant que facettes. |
| *Possibilité de recherche* |Indique que le champ peut faire l’objet d’une recherche en texte intégral. |

Pour plus d’informations sur les attributs d’index du service Recherche Azure, consultez [cet article](https://docs.microsoft.com/rest/api/searchservice/Create-Index).

## <a name="guidance-for-defining-an-index-schema"></a>Instructions de définition d’un schéma d’index
Lorsque vous concevez votre index, prenez le temps lors de la phase de planification de réfléchir chaque décision. Il est important de ne perdre de vue ni votre expérience de recherche ni vos besoins métiers lorsque vous concevez votre index, chaque champ devant être associé à des [attributs corrects](https://docs.microsoft.com/rest/api/searchservice/Create-Index). La modification d’un index une fois déployé implique la reconstruction et le rechargement des données.

Si vos besoins en stockage de données changent au fil du temps, vous pouvez augmenter ou diminuer la capacité en ajoutant ou en supprimant des partitions. Pour plus d’informations, consultez [Gérer votre service de recherche dans Azure](search-manage.md) ou [Limites de service](search-limits-quotas-capacity.md).

