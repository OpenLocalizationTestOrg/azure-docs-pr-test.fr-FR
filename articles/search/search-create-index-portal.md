---
title: "AAA « créer un index (portail - Azure Search) | Documents Microsoft »"
description: "Créer un index à l’aide de hello portail Azure."
services: search
manager: jhubbard
author: heidisteen
documentationcenter: 
ms.assetid: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/20/2017
ms.author: heidist
ms.openlocfilehash: 4c5d663499bf73a8883690aa9482b6ba59d1ddf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-azure-portal"></a>Créer un index Azure Search à l’aide de hello portail Azure
> [!div class="op_single_selector"]
> * [Vue d'ensemble](search-what-is-an-index.md)
> * [Portail](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

Utiliser le Concepteur d’index intégrés hello dans tooprototype portail Azure ou créer un [index de recherche](search-what-is-an-index.md) toorun sur votre service Azure Search. 

## <a name="prerequisites"></a>Composants requis

Cet article repose sur le principe que vous disposez [d’un abonnement Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) et du [service Recherche Azure](search-create-service-portal.md).  

## <a name="find-your-search-service"></a>Rechercher votre service de recherche
1. Connectez-vous à toohello page du portail Azure et passez en revue les hello [rechercher dans les services de votre abonnement](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)
2. Sélectionnez votre service Recherche Azure.

## <a name="name-hello-index"></a>Index du nom hello

1. Cliquez sur hello **ajouter un index** bouton dans la barre de commandes hello en hello haut hello.
2. Nommez votre index Azure Search. 
   * Le nom doit commencer par une lettre.
   * N’utilisez que des lettres minuscules, chiffres ou tirets (« - »).
   * Limiter les caractères too60 hello.

  nom de l’index Hello devient partie intégrante de hello URL de point de terminaison utilisé sur les index toohello de connexions et pour envoyer des requêtes HTTP Bonjour API REST Azure Search.

## <a name="define-hello-fields-of-your-index"></a>Définir des champs de l’index de hello

Composition de l’index inclut un *collection de champs* qui définit les données interrogeables hello dans votre index. Plus spécifiquement, il spécifie la structure hello de documents que vous téléchargez séparément. collection de champs Hello inclut les champs obligatoires et facultatifs, nommé et typé, toodetermine d’attributs index comment hello champ utilisable.

1. Bonjour **Add Index** panneau, cliquez sur **champs >** tooslide ouvrir le panneau de définition de champ hello. 

2. Accepter hello généré *clé* champ de type Edm.String. Par défaut, le champ de hello est nommé *id* mais vous pouvez le renommer tant que chaîne de hello satisfait [les règles d’affectation de noms](https://docs.microsoft.com/rest/api/searchservice/Naming-rules). Chaque index Azure Search doit obligatoirement comporter un champ clé de type chaîne.

3. Ajouter des champs toofully spécifier que vous allez télécharger des documents hello. Si les documents se composent d’un *id*, *nom d’hôtel*, *adresse*, *Ville*, et *région*, créer un champ correspondant pour chacun d’eux dans les index hello. Hello de révision [concevoir des instructions dans la section ci-dessous sur hello](#design) pour vous aider à définir les attributs.

4. Si vous le souhaitez, ajoutez tous les champs qui sont utilisés en interne dans les expressions de filtre. Dans le champ de hello peuvent définir des attributs tooexclude champs à partir d’opérations de recherche.

5. Lorsque vous avez terminé, cliquez sur **OK** toosave et créer des index de hello.

## <a name="tips-for-adding-fields"></a>Conseils sur l’ajout de champs

Création d’un index dans le portail de hello est intensif du clavier. Allégez les différentes étapes en suivant ce processus :

1. Générer en premier lieu, liste de champs hello en entrant les noms et en définissant des types de données.

2. Ensuite, les cases à cocher Utiliser hello haut hello toobulk de chaque attribut activer le paramètre hello pour tous les champs et puis sélectivement les cases pour hello assez de champs qui ne nécessite pas. Par exemple, il est généralement possible d’effectuer des recherches sur les champs de type chaîne. Par conséquent, vous pouvez cliquer sur **Retrievable** et **Searchable** tooboth les valeurs de retour hello Hello champ dans les résultats de la recherche, ainsient qu’Autoriser la recherche en texte intégral sur le champ de hello. 

<a name="design"></a>
## <a name="design-guidance-for-setting-attributes"></a>Conseils de conception pour la définition des attributs

Bien que vous pouvez ajouter de nouveaux champs à tout moment, les définitions de champ existant sont verrouillées dans pour la durée de vie hello d’index de hello. Pour cette raison, les développeurs utilisent en général le portail de hello pour la création d’index simples, idées de test ou à l’aide de toolook de pages du portail hello un paramètre. Itération fréquente sur la création d’un index est plus efficace si vous suivez une approche basée sur le code afin que vous pouvez reconstruire les index hello facilement.

Analyseurs et générateurs de suggestions sont associés avec des champs avant de l’index de hello est enregistré. Être tooclick vraiment à chaque page à onglets tooadd langage analyseurs ou générateurs de suggestions tooyour définition d’index.

Les champs de type chaîne sont souvent marqués avec les attributs **Possibilité de recherche** et **Récupérable**.

Résultats de recherche de champs utilisés toonarrow incluent **triable**, **Filterable**, et **Facetable**.

Les attributs d’un champ déterminent son utilisation, par exemple s’il est utilisé dans la recherche en texte intégral, la navigation par facettes, les opérations de tri et ainsi de suite. Hello tableau suivant décrit chaque attribut.

|Attribut|Description|  
|---------------|-----------------|  
|**searchable**|Analyse de recherche en texte intégral interrogeables, objet toolexical telles que l’analyse lexicale lors de l’indexation. Si vous définissez une valeur de tooa de champ de recherche telles que « journée ensoleillée », en interne il doit être fractionné en jetons individuels de hello « ensoleillée » et « jour ». Pour en savoir plus, consultez la rubrique [Fonctionnement de la recherche en texte intégral](search-lucene-query-architecture.md).|  
|**filterable**|Référencé dans les requêtes **$filter**. Les champs filtrables de type `Edm.String` ou `Collection(Edm.String)` ne font pas l’objet d’une analyse lexicale, les comparaisons ne concernent donc que les correspondances exactes. Par exemple, si vous définissez un tel champ trop « journée ensoleillée », `$filter=f eq 'sunny'` ne trouve aucune correspondance, mais `$filter=f eq 'sunny day'` sera. |  
|**sortable**|Par défaut système de hello trie les résultats par score, mais vous pouvez configurer le tri en fonction des champs dans les documents de hello. Les champs de type `Collection(Edm.String)` ne sont pas **triables**. |  
|**facetable**|Généralement utilisé dans une présentation des résultats de recherche qui inclut un nombre de correspondances par catégorie (par exemple, les hôtels dans une ville spécifique). Cette option ne peut pas être utilisée avec des champs de type `Edm.GeographyPoint`. Les champs de type `Edm.String` qui sont **filtrables**, **triables** ou **à choix multiples** ne peuvent pas dépasser 32 Ko de longueur. Pour plus d’informations, consultez l’article [Créer un index (API REST)](https://docs.microsoft.com/rest/api/searchservice/create-index).|  
|**key**|Identificateur unique pour les documents dans l’index de hello. Un seul champ doit être choisi comme champ de clé hello et il doit être de type `Edm.String`.|  
|**retrievable**|Détermine si le champ de hello peut être retournée dans un résultat de recherche. Cela est utile lorsque vous souhaitez toouse un champ (tel que *marge*) en tant que filtre, de tri ou de calcul du score du mécanisme, mais ne pas que vous souhaitez hello champ toobe toohello visible utilisateurs finaux. Il doit être `true` for `key` .|  

## <a name="create-hello-hotels-index-used-in-example-api-sections"></a>Création d’index de hôtels hello utilisé dans les sections exemple API

La documentation de l’API Azure Search inclut des exemples de code utilisant un index *hotels* simple. Dans hello captures d’écran ci-dessous, vous pouvez voir définition d’index hello, y compris d’analyseur de langue Français de hello spécifié lors de la définition d’index, ce qui vous pouvez recréer comme un exercice pratique dans le portail de hello.

![](./media/search-create-index-portal/field-definitions.png)

![](./media/search-create-index-portal/set-analyzer.png)

## <a name="next-steps"></a>Étapes suivantes

Après avoir créé un index Azure Search, vous pouvez déplacer maintenant toohello : [charger les données de recherche dans les index hello](search-what-is-data-import.md).

Sinon, vous pouvez étudier les index de manière plus approfondie. En outre toohello collection de champs, index spécifie également des analyseurs, générateurs de suggestions, profils et les paramètres CORS de calcul de score. Hello portail fournit des pages à onglets permettant de définir les éléments les plus courants hello : champs, des analyseurs et générateurs de suggestions. toocreate ou modifier d’autres éléments, vous pouvez utiliser des hello API REST ou .NET SDK.

## <a name="see-also"></a>Voir aussi

 [Fonctionnement de la recherche en texte intégral](search-lucene-query-architecture.md)  
 [API REST du service de recherche](https://docs.microsoft.com/rest/api/searchservice/)[SDK .NET](https://docs.microsoft.com/dotnet/api/overview/azure/search?view=azure-dotnet)

