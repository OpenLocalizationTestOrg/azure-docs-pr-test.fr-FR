---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Documentation préliminaire concernant hello synonymes (version préliminaire), exposée dans hello API REST Azure Search."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a>Synonymes dans Azure Search (version préliminaire)

Synonymes dans les moteurs de recherche associent un terme équivalent implicitement développez étendue hello d’une requête, sans hello utilisateur tooactually fournissent les termes hello. Par exemple, le terme donné hello « dog » et les associations de synonymes de « canine » et « chien », tous les documents contenant « dog », « canine » ou « chien » appartiennent relevant de requête de hello hello.

Dans Azure Search, l’expansion des synonymes est effectuée au moment de la requête. Vous pouvez ajouter le synonyme maps tooa service sans aucune opération de tooexisting d’interruption de service. Vous pouvez ajouter un **synonymMaps** définition de champ de propriété tooa sans avoir d’index de hello toorebuild. Pour plus d’informations, consultez [Mise à jour d’index](https://docs.microsoft.com/rest/api/searchservice/update-index).

## <a name="feature-availability"></a>Disponibilité des fonctionnalités

afficher un aperçu de synonymes Hello fonctionnalité n’est en cours et uniquement pris en charge dans hello dernière api-version d’évaluation (api-version = 2016-09-01-Preview). Il n’existe aucune prise en charge sur le portail Azure pour l’instant. Étant donné que la version de l’API de hello est spécifiée sur la demande de hello, il est possible toocombine disposition générale (GA) et les API préliminaires Bonjour même application. Cependant, les API de versions préliminaires ne sont pas soumises à un contrat SLA, et les fonctionnalités peuvent changer ; par conséquent, nous ne recommandons pas de les utiliser dans des applications de production.

## <a name="how-toouse-synonyms-in-azure-search"></a>Comment rechercher les synonymes toouse dans Azure

Dans Azure Search, prise en charge de synonyme est basée sur des cartes de synonyme que vous définissez et téléchargez tooyour service. Ces cartes constituent des ressources indépendantes (telles que des index ou des sources de données) et peuvent être utilisées par n’importe quel champ de recherche dans un index de votre service de recherche.

Les cartes de synonymes et les index sont gérés de manière indépendante. Une fois que vous définissez un mappage de synonyme et téléchargez tooyour service, vous pouvez activer la fonctionnalité de synonyme hello sur un champ en ajoutant une nouvelle propriété nommée **synonymMaps** dans la définition de champ hello. Création, mise à jour et suppression de qu'un mappage de synonyme est toujours une opération du document dans son ensemble, ce qui signifie que que vous ne pouvez pas créer, mettre à jour ou supprimer des éléments de mappage de synonyme hello de façon incrémentielle. Même la mise à jour d’une seule entrée nécessite un rechargement.

L’incorporation de synonymes dans votre application de recherche est un processus en deux étapes :

1.  Ajouter un service de recherche de synonyme carte tooyour via hello API ci-dessous.  

2.  Configurer un mappage de champ interrogeable toouse hello synonyme dans la définition de l’index hello.

### <a name="synonymmaps-resource-apis"></a>API de ressources SynonymMaps

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a>Ajoutez ou mettez à jour une carte de synonymes dans votre service à l’aide d’une requête POST ou PUT.

Mappages de synonyme sont téléchargés service toohello via POST ou PUT. Chaque règle doit être délimité par hello caractère de nouvelle ligne ('\n'). Vous pouvez définir des too5, des règles 000 par mappage de synonyme dans un service gratuit et 10 000 règles dans tous les autres références (SKU). Chaque règle peut avoir des expansions de too20.

Dans cette version préliminaire, synonyme maps doivent respecter le format hello Apache Solr qui est expliquée ci-dessous. Si vous disposez d’un dictionnaire de synonyme existant dans un format différent et que vous souhaitez toouse il directement, faites-le nous savoir sur [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

Vous pouvez créer un nouveau mappage de synonyme à l’aide de la requête HTTP POST, comme dans hello l’exemple suivant :

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

Vous pouvez également utiliser une requête PUT et spécifiez le nom de mappage de synonyme de hello sur hello URI. Si le mappage de synonyme hello n’existe pas, il sera créé.

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a>Format de synonymes Apache Solr

format de Solr Hello prend en charge les mappages de synonyme équivalent et explicite. Règles de mappage de respectent la spécification de filtre du synonyme toohello open source d’Apache Solr, décrites dans ce document : [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter). Voici un exemple de règle pour des synonymes équivalents.
```
              USA, United States, United States of America
```

Règle de hello ci-dessus, une requête de recherche « USA » se développe trop « USA » ou « United States » ou « États-Unis ».

Un mappage explicite est indiqué par une flèche « => ». Si spécifié, une séquence de terme d’une requête de recherche qui correspond à la partie gauche de hello de « = > » sera remplacé par alternatives hello sur le côté droit hello. Compte tenu de règle hello ci-dessous, les requêtes de recherche « Washington », « Washington » ou « WA » tous copiera trop « WA ». Seul le mappage explicite s’applique dans le sens hello spécifié et ne réécrit pas trop de requête hello « WA » « Washington » dans ce cas.
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a>Répertorier les cartes de synonymes de votre service.

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a>Obtenir une carte de synonymes pour votre service.

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a>Supprimer une carte de synonymes de votre service.

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a>Configurer un mappage de champ interrogeable toouse hello synonyme dans la définition de l’index hello.

Une nouvelle propriété de champ **synonymMaps** peut être utilisé toospecify un toouse de carte de synonyme pour un champ de recherche. Mappages de synonyme sont des ressources de niveau de service et peuvent être référencées par n’importe quel champ d’un index sous le service hello.

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

**synonymMaps** peut être spécifié pour les champs de recherche de type de hello 'Edm.String' ou 'Collection (EDM.String)'.

> [!NOTE]
> Dans cette version préliminaire, vous pouvez uniquement utiliser une carte de synonymes par champ. Si vous souhaitez toouse plusieurs mappages de synonyme, faites-le nous savoir sur [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

## <a name="impact-of-synonyms-on-other-search-features"></a>Impact des synonymes sur les autres fonctionnalités de recherche

fonctionnalité de synonymes Hello réécrit requête d’origine de hello avec des synonymes par hello opérateur OR. Pour cette raison, mise en surbrillance et les profils d’accès traitent des terme d’origine de hello et synonymes comme équivalents.

Fonctionnalité de synonyme s’applique toosearch requêtes et ne s’applique pas toofilters ou facettes. De même, les suggestions sont basées uniquement sur le terme d’origine de hello ; correspondances de synonyme n’apparaissent pas dans la réponse de hello.

Les expansions de synonyme ne s’appliquent pas les termes de recherche toowildcard ; préfixe, floue et les termes du contrat de l’expression régulière ne sont pas développées.

## <a name="tips-for-building-a-synonym-map"></a>Conseils pour créer une carte de synonymes

- Une carte de synonymes claire et précise est plus efficace qu’une liste exhaustive des correspondances possibles. Dictionnaires très volumineux ou complexes prennent plus de temps tooparse et affectent la latence requête hello si la requête de hello développe les synonymes de réduire. Au lieu d’estimation à laquelle les termes du contrat peut être utilisé, vous pouvez obtenir des termes du contrat de réel hello via un [rechercher le rapport d’analyse du trafic](search-traffic-analytics.md).

- En version préliminaire et la validation d’exercice, activer et ensuite utiliser cette tooprecisely rapport déterminent le termes du contrat de bénéficier d’une correspondance de synonyme et puis continuer toouse en tant que validation que votre mappage synonyme produit les meilleurs résultats. Dans les rapports hello prédéfini, hello vignettes « requêtes de recherche les plus courantes » et « requêtes de recherche de résultat zéro » vous donnera hello les informations nécessaires.

- Vous pouvez créer plusieurs cartes de synonymes pour votre application de recherche (par exemple, par langue si votre application prend en charge une base de clients multilingue). Actuellement, un champ peut uniquement utiliser une de ces deux méthodes. Vous pouvez mettre à jour la propriété synonymMaps d’un champ à tout moment.

## <a name="next-steps"></a>Étapes suivantes

- Si vous avez un index existant dans un environnement de (hors production) de développement, faites des essais avec un petit dictionnaire toosee comment addition hello de synonymes change hello expérience de recherche, notamment l’impact sur les profils d’accès mise en surbrillance et des suggestions.

- [Activer la recherche du trafic analytique](search-traffic-analytics.md) et utilisez hello prédéfinies rapport Power BI toolearn les termes utilisés la plupart des et les types retour hello zéro documents. Grâce à ces aperçus, modifiez les synonymes de tooinclude dictionnaire hello pour les requêtes non productives qui doivent être résolution toodocuments dans votre index.
