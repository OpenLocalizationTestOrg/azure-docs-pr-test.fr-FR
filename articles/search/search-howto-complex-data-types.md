---
title: "types de données complexes aaaHow toomodel dans Azure Search | Documents Microsoft"
description: "Les structures de données imbriquées ou hiérarchiques peuvent être modélisées dans un index Recherche Azure à l’aide d’un ensemble de lignes aplati et du type de données Collection."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a>Comment des types de données complexes de toomodel dans Azure Search
Jeux de données externes utilisées toopopulate un index Azure Search incluent parfois sous-structures hiérarchiques ou imbriquées qui ne désactiver parfaitement dans un ensemble de lignes tabulaire. Des exemples de telles structures incluent les emplacements et les numéros de téléphone multiples pour un même client, les couleurs et les tailles multiples pour une même référence, les auteurs multiples pour un même livre, etc. En termes de modélisation, vous pouvez voir ces structures visés tooas *types de données complexes*, *composée des types de données*, *types de données composites*, ou *d’agrégation types de données*, tooname quelques.

Types de données complexes ne sont pas pris en charge en mode natif dans Azure Search, mais une excellente solution de contournement inclut un processus en deux étapes de mise à plat de la structure de hello, puis en utilisant un **Collection** structure intérieurs de hello tooreconstitute de type de données. Technique de hello décrite dans cet article permet toobe de contenu hello recherchée, à facettes, filtrées et triées.

## <a name="example-of-a-complex-data-structure"></a>Exemple d’une structure de données complexe
En règle générale, les données de salutation en question résident en tant qu’ensemble de documents JSON ou XML, ou en tant qu’éléments dans une banque NoSQL comme base de données Azure Cosmos. Point de vue structurel, défi de hello provient d’avoir plusieurs éléments enfants qui doivent toobe recherché et filtré.  Comme point de départ pour illustrer la solution de contournement hello, prenez hello suivant du document JSON qui répertorie un ensemble de contacts, par exemple :

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

Alors que les champs hello nommée « id », « name » et « société » peuvent facilement être mappés un à un en tant que champs dans un index Azure Search, champ de « emplacements » hello contient un tableau d’emplacements, les deux un ensemble d’identificateurs de localisation, ainsi que des descriptions de l’emplacement. Étant donné que Azure Search n’a pas un type de données qui prend en charge, nous avons besoin un toomodel de manière différente dans Azure Search. 

> [!NOTE]
> Cette technique est également décrit par Kirk Evans dans un billet de blog [l’indexation de DocumentDB avec Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), qui montre une technique appelée « aplatissement hello données », dans laquelle vous aurait un champ appelé `locationsID` et `locationsDescription` qui sont tous deux [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (ou un tableau de chaînes).   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a>Partie 1 : Aplanir un tableau de hello dans des champs individuels
toocreate un index Azure Search adapté à ce jeu de données, créer des champs individuels de sous-structure imbriqués de hello : `locationsID` et `locationsDescription` avec un type de données [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (ou un tableau de chaînes). Dans ces champs vous serez valeurs d’index hello '1' et '2' dans hello `locationsID` champ pour les valeurs de John Smith et hello '3' & '4' dans hello `locationsID` champ Jen Campbell.  

Vos données dans Recherche Azure présentent l’aspect suivant : 

![Exemple de données, 2 lignes](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a>Partie 2 : Ajouter un champ de regroupement dans la définition d’index hello
Dans le schéma d’index hello, les définitions de champ hello peut se présenter exemple toothis similaire.

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a>Valider les comportements de recherche et d’éventuellement étendre les index hello
Si vous indexez hello créé et les données de hello chargé, vous pouvez maintenant tester hello solution tooverify recherche l’exécution des requêtes sur hello le jeu de données. Chaque champ **collection** doit **pouvoir faire l’objet de recherches**, être **filtrable** et **à choix multiples**. Vous devez être en mesure de toorun des requêtes comme :

* Trouver toutes les personnes qui travaillent à hello « Siège social de Adventureworks ».
* Obtention d’un nombre du nombre de hello de personnes qui travaillent dans un bureau « accueil ».  
* De hello personnes travaillant dans un bureau d’accueil, afficher les autres bureaux elles fonctionnent en même temps que le nombre de personnes hello dans chaque emplacement.  

Où cette technique réduit à néant est lorsque vous devez toodo une recherche qui combine des id d’emplacement hello ainsi que description de l’emplacement hello. Par exemple :

* Trouver toutes les personnes qui font du télétravail et dont l’ID d’emplacement est 4.  

Si vous vous souvenez de contenu d’origine de hello présentait ainsi :

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

Toutefois, maintenant que nous avons séparées par des données de salutation dans des champs distincts, nous n’avons aucun moyen de savoir si hello particuliers pour Jen Campbell concerne trop`locationsID 3` ou `locationsID 4`.  

toohandle ce cas, définissez un autre champ dans l’index hello qui combine toutes les données de hello en une collection unique.  Dans notre exemple, nous appellerons ce champ `locationsCombined` et nous allons séparer contenu hello avec un `||` bien que vous pouvez choisir n’importe quel séparateur que vous pensez serait un jeu unique de caractères pour votre contenu. Par exemple : 

![Exemple de données, 2 lignes avec séparateur](./media/search-howto-complex-data-types/sample-data-2.png)

À l’aide de ce champ `locationsCombined` , nous pouvons maintenant effectuer davantage de requêtes, telles que :

* Afficher le nombre de personnes qui font du télétravail et dont l’ID d’emplacement est 4.  
* Rechercher les personnes qui font du télétravail et dont l’ID d’emplacement est 4. 

## <a name="limitations"></a>Limitations
Cette technique est utile pour un certain nombre de scénarios, mais elle n’est pas applicable dans tous les cas.  Par exemple :

1. Si vous n’avez pas d’un ensemble statique de champs dans votre type de données complexe et il n’a aucun toomap de façon possible de hello tous les types de champ tooa. 
2. Mise à jour des objets de hello imbriqué requiert certains toodetermine travail supplémentaire à exactement ce qui doit toobe mis à jour dans l’index de recherche de Azure hello

## <a name="sample-code"></a>Exemple de code
Vous pouvez afficher un exemple de comment tooindex un complexes JSON jeu de données dans Azure Search et effectuer un nombre de requêtes sur ce jeu de données sur ce [référentiel GitHub](https://github.com/liamca/AzureSearchComplexTypes).

## <a name="next-step"></a>Étape suivante
[Vote pour la prise en charge native pour les types de données complexes](https://feedback.azure.com/forums/263029-azure-search) sur hello Azure recherche UserVoice page et fournir une entrée supplémentaire que vous souhaitez que nous tooconsider concernant l’implémentation des fonctionnalités. Vous pouvez également contacter toome directement sur Twitter à @liamca.

