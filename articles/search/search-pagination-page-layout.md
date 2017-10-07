---
title: "résultats de la recherche de toopage aaaHow dans Azure Search | Documents Microsoft"
description: "Pagination dans Azure Search, un service de recherche cloud hébergé sur Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a>Affichage des résultats de recherche de toopage dans Azure Search
Cet article fournit des conseils sur l’affichage des résultats de page, tels que le total des nombres, récupération de document, ordres de tri et la navigation toouse hello API REST de Service Azure Search tooimplement éléments standard d’une recherche.

Dans tous les cas mentionnés ci-dessous, les options de page qui contribuent des données ou des informations tooyour page de résultats sont spécifiées via hello [recherche dans le Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) tooyour de demandes envoyées Service Azure Search. Les demandes incluent une commande GET, chemin d’accès et les paramètres de requête qui informent le service hello ce qui est demandé et comment tooformulate hello réponse.

> [!NOTE]
> Une demande valide inclut plusieurs éléments, parmi lesquels une URL de service et un chemin d’accès, un verbe HTTP, `api-version`, etc. Par souci de concision, nous tronquées hello exemples toohighlight hello simplement la syntaxe toopagination pertinentes. Consultez hello [API REST de Service Azure Search](http://msdn.microsoft.com/library/azure/dn798935.aspx) pour plus d’informations sur la syntaxe de requête.
> 
> 

## <a name="total-hits-and-page-counts"></a>Nombre total de résultats et nombre de pages
Affichage hello total nombre de résultats retournés à partir d’une requête, puis de retourner les résultats en segments plus petits, n’est fondamental toovirtually toutes les pages de recherche.

![][1]

Dans Azure Search, vous utilisez hello `$count`, `$top`, et `$skip` paramètres tooreturn ces valeurs. Hello suivant montre un exemple de demande pour le nombre total d’accès, retourné sous la forme `@OData.count`:

        GET /indexes/onlineCatalog/docs?$count=true

Récupérer des documents dans des groupes de 15 et indiquent également le nombre total d’accès hello, en commençant à la première page de hello :

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

Pagination des résultats requiert deux `$top` et `$skip`, où `$top` spécifie combien tooreturn d’éléments dans un lot, et `$skip` spécifie combien tooskip d’éléments. Bonjour, l’exemple suivant chaque page affiche hello ensuite 15 d’éléments, indiquée par sauts incrémentielle de hello Bonjour `$skip` paramètre.

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a>Disposition
Sur une page de résultats, vous pourriez tooshow une image miniature, un sous-ensemble des champs et une page de produit complet tooa lien.

 ![][2]

Dans Azure Search, vous utiliseriez `$select` et une recherche des commandes tooimplement cette expérience.

tooreturn un sous-ensemble des champs d’une disposition en mosaïque :

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

Images et fichiers multimédias ne sont pas directement interrogeables et doivent être stockées dans une autre plate-forme de stockage, telles que le stockage Blob Azure, les coûts de tooreduce. Dans les index hello et des documents, définissez un champ qui stocke l’adresse URL de hello du contenu externe de hello. Vous pouvez ensuite utiliser le champ de hello comme une référence d’image. URL d’image de toohello Hello doit être dans le document de hello.

tooretrieve page d’une description de produit pour un **onClick** événement, utilisez [recherche de Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass dans la clé de hello de hello document tooretrieve. type de données Hello de clé de hello est `Edm.String`. Dans cet exemple, il s’agit de *246810*. 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a>Tri par pertinence, évaluation ou prix
Les ordres de tri souvent par défaut toorelevance, mais il est commun toomake autre les ordres de tri disponibles afin que les clients peuvent remanier rapidement les résultats existants dans un ordre de classement différent.

 ![][3]

Dans Azure Search, le tri est basé sur hello `$orderby` expression pour tous les champs qui sont indexés en tant que`"Sortable": true.`

La pertinence est clairement liée aux profils de score. Vous pouvez utiliser hello score par défaut, qui repose sur l’ordre de toorank statistiques et d’analyse de texte tous les résultats, avec des scores élevés va toodocuments avec des correspondances plus ou plus forts sur un terme à rechercher.

Ordres de tri de remplacement sont généralement associés **onClick** événements rappeler tooa méthode qui génère l’ordre de tri hello. Par exemple, avec cet élément de page :

 ![][4]

Vous devez créer une méthode qui accepte une option de tri hello sélectionné en tant qu’entrée et retourne une liste ordonnée de critères hello associés à cette option.

 ![][5]

> [!NOTE]
> Hello de calcul de score par défaut est suffisant pour de nombreux scénarios, nous vous recommandons de baser pertinence sur un profil de score personnalisé à la place. Un profil de score personnalisé vous donne un tooboost de façon dont les éléments qui sont les plus avantageux tooyour business. Consultez [Ajout de profils de calcul de score](http://msdn.microsoft.com/library/azure/dn798928.aspx) pour en savoir plus. 
> 
> 

## <a name="faceted-navigation"></a>Navigation à facettes
Navigation de la recherche est courante dans une page de résultats, souvent située à côté de hello ou en haut d’une page. Dans Azure Search, la navigation à facettes permet une recherche autonome en fonction de filtres prédéfinis. Consultez [Navigation à facettes dans Azure Search](search-faceted-navigation.md) pour en savoir plus.

## <a name="filters-at-hello-page-level"></a>Filtres au niveau de la page hello
Si votre conception de solution inclus des pages de recherche dédié pour certains types de contenu (par exemple, une application de vente au détail en ligne qui a les services répertoriés en hello haut hello), vous pouvez insérer une expression de filtre avec une **onClick** événement tooopen une page dans un état pré-filtrée. 

Vous pouvez envoyer un filtre avec ou sans expression de recherche. Par exemple, hello de demande suivant filtre sur le nom de marque, ne retourner que les documents qui lui correspondent.

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

Consultez [Recherche de documents (API Recherche Azure)](http://msdn.microsoft.com/library/azure/dn798927.aspx) pour en savoir plus sur les expressions `$filter`.

## <a name="see-also"></a>Voir aussi
* [API REST de service Azure Search](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [Opérations d’index](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [Opérations de document](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [Vidéos et didacticiels relatifs à Azure Search](search-video-demo-tutorial-list.md)
* [Navigation à facettes dans Azure Search](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
