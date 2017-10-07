---
title: architecture de moteur (Lucene) de recherche de texte aaaFull dans Azure Search | Documents Microsoft
description: "Explication des concepts récupération Lucene requête document et de traitement pour la recherche en texte intégral, comme tooAzure associé recherche."
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: c6d1bea8d40154fd9237b9e44584cdfcd193cbd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a>Fonctionnement de la recherche en texte intégral dans la recherche Azure

Cet article est destiné aux développeurs qui ont besoin d’une compréhension approfondie du fonctionnement de la recherche en texte intégral Lucene dans la recherche Azure. Pour les requêtes de texte, la recherche Azure. fournit en toute transparence les résultats attendus dans la plupart des scénarios, mais il se peut que vous obteniez un résultat « étrange » dans certains cas. Dans ce cas, la présence d’un arrière-plan dans hello quatre phases d’exécution de requêtes Lucene (requête analyse analyse lexicale, mise en correspondance, calculer les scores de document) peut vous aider à identifier les modifications spécifiques tooquery paramètres ou de configuration qui remet hello d’index résultat souhaité. 

> [!Note] 
> La recherche Azure utilise Lucene pour la recherche en texte intégral, mais l’intégration Lucene n’est pas exhaustive. Nous exposer et étendre Lucene fonctionnalité tooenable hello scénarios important tooAzure recherche sélective. 

## <a name="architecture-overview-and-diagram"></a>Présentation et diagramme de l’architecture

Le traitement d’une requête de recherche de texte intégral commence par analyser les termes de recherche tooextract hello requête texte. moteur de recherche Hello utilise un tooretrieve indexer des documents avec les termes du contrat de correspondance. Les termes de requête individuels sont parfois divisés et reconstitué dans nouveaux formulaires toocast un réseau plus large sur ce qui peut être considéré comme une correspondance potentielle. Un jeu de résultats est ensuite trié par un pertinence score attribué tooeach correspondant document individuel. Celles haut hello hello liste de classement sont retournées toohello application d’appel.

Après retraitement, l’exécution des requêtes comporte quatre étapes : 

1. Analyse des requêtes 
2. Analyse lexicale 
3. Extraction de documents 
4. Notation 

diagramme de Hello ci-dessous illustre hello composants utilisés tooprocess une demande de recherche. 

 ![Diagramme d’architecture de requête Lucene dans la recherche Azure][1]


| Composants clés | Description fonctionnelle | 
|----------------|------------------------|
|**Analyseurs de requêtes** | Séparer les termes de requête d’opérateurs de requête et créer le moteur de recherche hello requête structure (une arborescence de requête) toobe envoyé toohello. |
|**Analyseurs** | Effectuez une analyse lexicale sur les termes de requête. Ce processus peut impliquer la transformation, la suppression ou le développement des termes de requête. |
|**Index** | Une structure de données efficace utilisé toostore et organiser interrogeables termes extraits à partir de documents indexés. |
|**Moteur de recherche** | Récupère et des scores de correspondance des documents basés sur le contenu de hello Hello des index inversé. |

## <a name="anatomy-of-a-search-request"></a>Anatomie d’une requête de recherche

Une requête de recherche est une spécification complète de ce qui doit être renvoyé dans un jeu de résultats. Dans sa forme la plus simple, il s’agit d’une requête vide sans aucun critère. Un exemple plus réaliste inclut des paramètres, plusieurs termes, les champs toocertain peut-être avec étendue, avec les règles de tri et éventuellement une expression de filtre de requête.  

exemple Hello est une demande de recherche que vous pouvez envoyer tooAzure recherche à l’aide de hello [API REST](https://docs.microsoft.com/rest/api/searchservice/search-documents).  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

Pour cette requête, moteur de recherche hello hello suivant :

1. Filtre les documents où le prix de hello est au moins 60 et moins de 300 $.
2. Exécute la requête de hello. Dans cet exemple, la requête de recherche hello se compose de phrases et les termes du contrat : `"Spacious, air-condition* +\"Ocean view\""` (en général, les utilisateurs n’entrent pas signes de ponctuation, mais inclure dans l’exemple de hello permet tooexplain comment des analyseurs de gérer). Pour cette requête, moteur de recherche hello analyse description de hello et champs de titre spécifié dans `searchFields` pour les documents qui contiennent « Vue océan » et en outre sur terme hello « spacieux » ou sur les termes qui commencent par Bonjour préfixe « air-condition ». Hello `searchMode` paramètre est toomatch utilisée sur tout terme (valeur par défaut) ou l’ensemble d'entre elles, pour les cas où un terme n’est pas explicitement requis (`+`).
3. Commandes hello obtenu des hôtels à proximité tooa l’emplacement géographique et retournées toohello application d’appel. 

Hello plus grande partie de cet article est sur le traitement de hello *recherche*: `"Spacious, air-condition* +\"Ocean view\""`. Le filtrage et le tri ne sont pas abordés. Pour plus d’informations, consultez hello [documentation de référence des API de recherche](https://docs.microsoft.com/rest/api/searchservice/search-documents).

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a>Étape 1 : Analyse des requêtes 

Comme indiqué, la chaîne de requête hello est hello première ligne de hello demande : 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

requête Hello analyseur sépare les opérateurs (tels que `*` et `+` dans l’exemple de hello) à partir de la recherche des termes du contrat et décompose les requêtes de recherche hello dans *sous-requêtes* d’un type pris en charge : 

+ *requête de terme* pour les termes autonomes (comme spacieux)
+ *requête d’expression* pour les termes entre guillemets (comme vue mer)
+ *requête de préfixe* pour les termes suivis d’un opérateur de préfixe `*` (comme air condition)

Pour obtenir la liste complète des types de requêtes pris en charge, voir [Syntaxe de requête Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

Opérateurs associés à une sous-requête déterminent si la requête de hello « doit être » ou « doit être » satisfait par ordre d’un document toobe considérée comme une correspondance. Par exemple, `+"Ocean view"` en « doit » toohello échéance `+` opérateur. 

Analyseur de requêtes Hello restructure des sous-requêtes hello un *arborescence de requête* (une structure interne représentant hello requête), il passe sur le moteur de recherche toohello. Dans hello première étape de l’analyse de requête, l’arbre de requête hello ressemble à ceci.  

 ![Mode de recherche de requête booléenne : quelconque][2]

### <a name="supported-parsers-simple-and-full-lucene"></a>Analyseurs pris en charge : simple et complet (Lucene) 

 La recherche Azure expose deux langages de requête différents, `simple` (valeur par défaut) et `full`. En définissant un hello `queryType` paramètre avec votre demande de recherche, vous indiquez à Analyseur de requêtes hello langage de requête vous choisissez afin qu’il sache comment toointerpret hello la syntaxe et les opérateurs. Hello [langue de requête Simple](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) est intuitive et robuste, souvent approprié toointerpret l’entrée d’utilisateur en tant que-sans traitement côté client. Il prend en charge les opérateurs de requête courants des moteurs de recherche web. Hello [langage de requête complète Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), que vous obtenez en définissant `queryType=full`, étend le langage de requête Simple hello par défaut en ajoutant la prise en charge pour plus d’opérateurs et des types de requêtes comme caractère générique, floue, regex et les requêtes de portée d’un champ. Par exemple, une expression régulière envoyée en syntaxe de requête simple serait interprétée en tant que chaîne de requête et pas en tant qu’expression. demande d’exemple Hello dans cet article utilise un langage de requête complète Lucene hello.

### <a name="impact-of-searchmode-on-hello-parser"></a>Impact de searchMode sur l’Analyseur de hello 

Un autre paramètre de requête de recherche qui affecte l’analyse est hello `searchMode` paramètre. Il contrôle l’opérateur par défaut de hello pour les requêtes booléennes : n’importe quel (par défaut) ou l’ensemble.  

Lorsque `searchMode=any`, qui est par défaut hello, délimiteur d’espace hello entre spacieux et air-condition est ou (`||`), en le texte de requête d’exemple hello équivalent à : 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

Opérateurs explicites, tels que `+` dans `+"Ocean view"`, ne sont pas ambiguës dans la construction de requête booléenne (terme de hello *doit* correspondent). Est moins évidente comment hello toointerpret restants du contrat : spacieux et air-condition. Moteur de recherche hello doit rechercher des correspondances dans la vue de l’océan *et* spacieux *et* air-condition ? Ou il doit trouver océan plus *le des deux* Hello restant des termes du contrat ? 

Par défaut (`searchMode=any`), moteur de recherche hello suppose d’interprétation plus large de hello. N’importe quel champ *doit* être mis en correspondance, reflétant la sémantique du « ou ». arborescence de la requête initiale Hello illustré précédemment, par hello deux opérations « doit », présente, hello par défaut.  

Supposons que nous avons maintenant défini `searchMode=all`. Dans ce cas, espace de hello est interprété comme une opération « et ». Chacun des termes de restantes hello doit être présent dans hello document tooqualify comme une correspondance. Hello résultant exemple de requête est interprétée comme suit : 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

Une arborescence de la requête modifiée pour cette requête se présente comme suit, où un document correspondant est intersection hello de toutes les sous-requêtes de trois : 

 ![Mode de recherche de requête booléenne : tout][3]

> [!Note] 
> Choisir `searchMode=any` plutôt que `searchMode=all` est le meilleur moyen d’exécuter des requêtes représentatives. Les utilisateurs qui sont susceptibles de tooinclude opérateurs (commun lors de la recherche de document stocke) peut rechercher les résultats plus intuitive si `searchMode=all` informe les constructions de requête booléenne. Pour plus d’informations sur l’interaction entre les hello entre `searchMode` et opérateurs, consultez [syntaxe de requête Simple](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a>Étape 2 : Analyse lexicale 

Processus d’analyseurs lexicaux *terme requêtes* et *une phrase requêtes* une fois que l’arborescence de requête hello est structurée. Un analyseur accepte hello texte intrants tooit par l’Analyseur de hello et processus hello texte puis termes envoie de nouveau sous forme de jetons toobe intégrés hello arborescence de requête. 

forme la plus commune de l’analyse lexicale Hello est *analyse linguistique* qui transforme les termes de requête en fonction de tooa spécifique de règles donné de langage : 

* Réduction d’une requête terme toohello racine d’un mot forme 
* Supprimer les mots non essentiels (mots vides, tels que « le », « la », « les » ou « et » en français) 
* Diviser un mot composite en composants 
* Convertir en minuscules un mot en majuscules 

Toutes ces opérations ont tendance tooerase les différences entre l’entrée de texte hello fournies par les termes hello hello et utilisateur stockées dans les index hello. Les opérations aller au-delà du traitement de texte et nécessitent une connaissance approfondie du langage hello lui-même. tooadd cette couche de sensibilisation linguistique, Azure Search prend en charge une longue liste de [analyseurs de langage](https://docs.microsoft.com/rest/api/searchservice/language-support) de Lucene et Microsoft.

> [!Note]
> Besoins d’analyse peuvent s’échelonner de tooelaborate minimale en fonction de votre scénario. Vous pouvez contrôler la complexité de l’analyse lexicale par hello en sélectionnant un des analyseurs de hello prédéfini ou en créant votre propre [analyseur personnalisé](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search). Analyseurs sont des champs de toosearchable étendue et sont spécifiés dans le cadre d’une définition de champ. Ainsi, vous analyse lexicale de toovary sur une base de chaque champ. N’est pas spécifié, hello *standard* Lucene analyseur est utilisée.

Dans notre exemple, tooanalysis préalable, requête initiale hello possède le terme hello « Spacious » par un majuscule « S » et une virgule qui hello Analyseur de requêtes interprète comme une partie du terme de requête hello (une virgule n'est pas considéré comme un opérateur de langage de requête).  

Lorsque l’Analyseur de hello par défaut traite le terme de hello, il minuscules « vue océan » et « spacieux » et supprimez le caractère de virgule hello. arborescence de la requête modifiée Hello se présentera comme suit : 

 ![Requête booléenne avec termes analysés][4]

### <a name="testing-analyzer-behaviors"></a>Test des comportements de l’analyseur 

comportement de Hello d’un analyseur peut être testé à l’aide de hello [analyser les API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer). Entrez le texte hello souhaité tooanalyze toosee le termes du contrat de donnée d’analyseur génère. Par exemple, toosee comment l’analyseur standard de hello traiterait hello air-condition « texte », vous pouvez émettre hello demande :

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

analyseur standard de Hello s’interrompt de texte d’entrée hello en hello suivant deux jetons, les annoter avec des attributs tels que Démarrer et les offsets de fin (utilisés pour la mise en surbrillance), ainsi que leur position (utilisé pour la correspondance d’expression) :

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-toolexical-analysis"></a>Analyse de toolexical d’exceptions 

Analyse lexicale s’applique uniquement les types de tooquery qui nécessitent des conditions complètes – une requête terme ou une requête d’expression. Il ne s’applique pas tooquery les types incomplets termes : requête de préfixe, les requêtes génériques, regex requête – ou requête approximative de tooa. Les types, y compris la requête de préfixe hello avec un terme de requête *air-condition\**  dans notre exemple, sont ajoutés directement toohello arbre de requêtes, en ignorant la phase d’analyse hello. Hello que transformation effectuée sur les termes de requête de ces types est minuscules.

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a>Étape 3 : Extraction de documents 

Récupération de document fait référence à des documents avec les termes correspondants dans les index de hello toofinding. Vous comprendrez mieux cette étape à l’aide d’un exemple. Commençons par un index hôtels ayant hello suivant schéma simple : 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

Supposons également que cet index contient hello suivant quatre documents : 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance toohello beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on hello north shore of hello island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

**Comment les termes sont indexés**

récupération de toounderstand, il permet de tooknow quelques notions de base sur l’indexation. unité de stockage de Hello est un index inversé, un pour chaque champ de recherche. Un index inversé comprend la liste triée de tous les termes issus de tous les documents. Chaque terme mappe toohello la liste des documents dans laquelle elle se produit, comme évident dans l’exemple hello ci-dessous.

termes du contrat de hello tooproduce dans un index inversé, moteur de recherche hello effectue des analyse lexicale sur le contenu des documents, hello toowhat similaire se produit pendant le traitement des requêtes. Entrées de texte sont passées analyseur tooan, en minuscules, débarrassé des signes de ponctuation et ainsi de suite, en fonction de la configuration d’analyseur hello. Il est commun, mais n’est pas obligatoire, toouse hello des analyseurs de mêmes pour la recherche et les opérations d’indexation afin que les termes de requête plus ressembler à des termes du contrat à l’intérieur de hello index.

> [!Note]
> La recherche Azure vous permet de spécifier différents analyseurs pour l’indexation et la recherche via les paramètres de champ supplémentaires `indexAnalyzer` et `searchAnalyzer`. Si non spécifié, hello analyzer avec hello `analyzer` propriété est utilisée pour l’indexation et de recherche.  

**Index inversé pour les documents d’exemple**

Retour de tooour exemple, pour hello **titre** champ, les index hello inversé ressemble à ceci :

| Terme | Liste de documents |
|------|---------------|
| atman | 1 |
| plage | 2 |
| hôtel | 1, 3 |
| mer | 4  |
| playa | 3 |
| complexe | 3 |
| retraite | 4 |

Dans le champ de titre hello, uniquement *hôtel* s’affiche dans deux documents : 1, 3.

Pourquoi **description** champ, hello index est comme suit :

| Terme | Liste de documents |
|------|---------------|
| air | 3
| and | 4
| plage | 1
| conditionné | 3
| confortable | 3
| distance | 1
| île | 2
| kauaʻi | 2
| situé | 2
| Nord | 2
| mer | 1, 2, 3
| sur | 2
| sur |2
| calme | 4
| chambres  | 1, 3
| isolé | 4
| rive | 2
| spacieux | 1
| Salut | 1, 2
| trop| 1
| view | 1, 2, 3
| marche | 1
| par | 3


**Termes de requête correspondant aux termes indexés**

Étant donné les indices hello inversé ci-dessus, nous allons retourner toohello exemple de requête et voir comment la correspondance des documents sont trouvés pour notre exemple de requête. Rappelez-vous que cette arborescence de la dernière requête hello ressemble à ceci : 

 ![Requête booléenne avec termes analysés][4]

Pendant l’exécution de requête, les requêtes sont exécutées sur les champs interrogeables hello indépendamment. 

+ Hello TermQuery, « spacieux » correspond au document 1 (hôtel Atman). 

+ Hello PrefixQuery, « air-condition * », ne correspond pas à tous les documents. 

  Ce comportement déroute parfois les développeurs. Bien que le terme hello climatisée existe dans le document de hello, il est fractionné en deux termes par l’Analyseur de hello par défaut. N’oubliez pas que les requêtes de préfixe, qui contiennent des termes partiels, ne sont pas analysées. Par conséquent, les termes du contrat avec le préfixe « air-condition » est recherchés dans hello index inversé et introuvable.

+ Hello PhraseQuery « vue océan », consulte les termes du contrat de hello « océan » et « vue » et vérifie la proximité hello de termes hello document d’origine. Documents 1, 2 et 3 correspond à cette requête dans le champ de description hello. Document d’avis 4 a océan de terme hello dans le titre de hello mais n’est pas considéré comme une correspondance, nous recherchons une expression de hello « vue océan » plutôt que des mots individuels. 

> [!Note]
> Une requête de recherche est exécutée indépendamment par rapport à tous les champs interrogeables Bonjour Azure recherche d’index, sauf si vous limitez les champs hello avec hello `searchFields` paramètre, comme illustré dans la demande de recherche d’exemple hello. Les documents qui correspondent dans un des champs de hello sélectionné sont retournés. 

Sur hello entier de requête hello en question, documents hello correspondant sont 1, 2, 3. 

## <a name="stage-4-scoring"></a>Étape 4 : Notation  

Un score de pertinence est attribué à chaque document d’un jeu de résultats de recherche. fonction Hello du score de pertinence hello est toorank plus élevé de ces documents que mieux répondre à un utilisateur de question exprimé par une requête de recherche hello. score de Hello est calculé en fonction des propriétés statistiques des termes du contrat de mise en correspondance. Hello core Hello formule de calcul de score est [TF/IDF (fréquence inverse de la fréquence de document de terme)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf). Dans les requêtes contenant les termes rares et communes, TF/IDF promeut les résultats contenant le terme de rares hello. Par exemple, dans un index hypothétique avec tous les articles de Wikipedia, à partir de documents cette requête de mise en correspondance hello *directeur de hello*, des documents spéciaux sur *directeur* sont considérés comme plus pertinents que documents correspondant sur *le*.


### <a name="scoring-example"></a>Exemple de notation

Rappel hello trois documents correspondant à notre exemple de requête :
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance toohello beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on hello north shore of hello island of Kauai. Ocean view."
    }
  ]
}
~~~~

Document 1 requête de mise en correspondance hello mieux, car les deux hello terme *spacieux* et d’une expression de requis hello *océan* se produisent dans le champ de description hello. documents de deux Hello correspondent uniquement l’expression hello *océan*. Il peut étonnante ce score de pertinence hello pour document 2 et 3 est différent, même si elles mises en correspondance la requête hello Bonjour identique. Cela signifie que la formule de calcul de score de hello a de composants plus que simplement TF/IDF. Dans ce cas, un score légèrement plus élevé a été affecté au document 3, car sa description est plus courte. En savoir plus sur [formule de calcul de score pratique Lucene](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) toounderstand la longueur de champ et d’autres facteurs peuvent influencer hello note.

Certains types (caractère générique, préfixe, regex) de la requête contribue toujours à un score de constant toohello globale score de document. Ainsi, les correspondances trouvées par le biais toobe d’extension de requête inclus dans les résultats de hello, mais sans affecter le classement de hello. 

L’exemple suivant illustre l’importance de ce facteur. Recherches par caractères génériques, y compris les recherches de préfixes sont ambiguës par définition, car hello entrée est une chaîne partielle avec des correspondances potentielles sur un très grand nombre de termes disparates (prendre en compte une entrée de « visite * », avec des correspondances trouvées sur « présentations », « tourettes », et » TOURMALINE »). Compte tenu de nature hello de ces résultats, il est impossible tooreasonably déduire le termes du contrat est plus utile que d’autres. Pour cette raison, nous ignorons les fréquences de terme lors de la notation des résultats dans les requêtes de types génériques, de préfixe et d’expression régulière. Dans une demande de recherche de plusieurs parties qui comprend les termes partielles et totales, les résultats à partir de l’entrée partielle de hello sont intégrés avec une constante score décalage tooavoid vers correspondances potentiellement inattendus.

### <a name="score-tuning"></a>Paramétrage du score

Il existe deux façons les scores de pertinence tootune dans Azure Search :

1. **Profils de calcul de score** promouvoir des documents dans la liste hello classé de résultats en fonction d’un ensemble de règles. Dans notre exemple, nous avons prendre en compte les documents mis en correspondance dans le champ de titre hello plus pertinent que les documents mis en correspondance dans le champ de description hello. En outre, si notre index comporte un champ Prix pour chaque hôtel, nous aurions pu promouvoir les documents avec un prix inférieur. En savoir plus comment trop[ajouter des index de recherche de profils de calcul de score tooa.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)
2. **Renforcement de terme** (disponible uniquement dans la syntaxe de requête complète Lucene hello) fournit un opérateur de renforcement `^` qui peut être appliqué partie tooany d’arborescence de requête hello. Dans notre exemple, au lieu de rechercher le préfixe du hello *air-condition*\*, un pourriez rechercher un terme exact hello *air-condition* ou préfixe de hello, mais les documents qui correspondent sur hello exacte terme de rang supérieur en appliquant la requête de renforcement toohello terme : *air condition ^ 2 || air-condition**. En savoir plus sur la [promotion de termes](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).


### <a name="scoring-in-a-distributed-index"></a>Notation dans un index distribué

Tous les index de recherche de Azure sont automatiquement Fractionner en plusieurs partitions, ce qui nous permet de tooquickly distribuer index hello entre plusieurs nœuds pendant la mise à l’échelle du service vers le haut ou à l’échelle. Lorsqu’une requête de recherche est émise, elle est émise sur chaque partition indépendamment. Hello résultats de chaque partition sont ensuite fusionnées et classées par score (si aucun autre classement n’est défini). Il est important tooknow qui hello score fonction poids terme fréquence des requêtes par rapport à sa fréquence inverse de document dans tous les documents de la partition de hello, pas sur toutes les partitions !

Cela signifie qu’un score de pertinence *peut* être différent pour des documents identiques s’ils résident sur différentes partitions. Heureusement, ces différences ont tendance toodisappear comme nombre de hello de documents dans l’index de hello augmente en raison de la distribution du même terme toomore. Il n’est pas possible tooassume sur quelle partition sera placé n’importe quel document donné. Toutefois, en supposant qu’une clé de document ne change pas, il sera toujours être affecté toohello même ID de partition.

En général, le score du document n’est pas attribut de meilleures hello pour le classement des documents si la stabilité de l’ordre est importante. Par exemple, étant donné deux documents ont un score identique, il n’existe aucune garantie que celui qui apparaît en premier dans les exécutions suivantes de hello même requête. Score du document doit uniquement donner une idée générale de la pertinence du document relatif tooother documents dans le jeu de résultats hello.

## <a name="conclusion"></a>Conclusion

réussite Hello de moteurs de recherche internet a généré les attentes en matière de recherche en texte intégral sur des données privées. Pour presque n’importe quel type d’expérience de recherche, nous avons maintenant vous attendre hello moteur toounderstand notre intention, même quand les conditions sont mal orthographiées ou incomplète. Nous allons même jusqu’à attendre des correspondances en fonction de termes équivalents ou synonymes jamais spécifiés.

À partir d’un point de vue technique, la recherche en texte intégral est très complexe, nécessitant une analyse linguistique sophistiquée et une approche systématique tooprocessing de manière à distiller, développez et transformer des termes de requête toodeliver un résultat correspondant. Étant donné les complexités inhérentes hello, il existe un grand nombre de facteurs peuvent affecter les résultats hello d’une requête. Pour cette raison, faisant l’acquisition de mécanismes de hello toounderstand hello heure de recherche en texte intégral offre des avantages tangibles lors de la tentative de toowork par le biais des résultats inattendus.  

Cet article a traité la recherche en texte intégral dans le contexte de hello d’Azure Search. Nous espérons qu’il vous donne suffisamment arrière-plan toorecognize potentiels causes et solutions pour résoudre les problèmes courants de requête. 

## <a name="next-steps"></a>Étapes suivantes

+ Générer l’exemple d’index de hello, essayez différentes requêtes et passez en revue les résultats. Pour obtenir des instructions, consultez [construire et interroger un index dans le portail de hello](search-get-started-portal.md#query-index).

+ Essayez de syntaxe de requête supplémentaires à partir de hello [recherche de Documents](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) section exemple ou à partir de [syntaxe de requête Simple](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) dans l’Explorateur de recherche dans le portail de hello.

+ Révision [profils](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) si vous souhaitez tootune dans votre application de recherche de classement.

+ Découvrez comment tooapply [les analyseurs lexicaux spécifiques au langage](https://docs.microsoft.com/rest/api/searchservice/language-support).

+ [Configurez des analyseurs personnalisés](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) pour un traitement minimal ou pour un traitement spécialisé sur des champs spécifiques.

+ [Comparez les analyseurs standards et les analyseurs anglais](http://alice.unearth.ai/) côte à côte sur ce site web de démonstration. 

## <a name="see-also"></a>Voir aussi

[API REST de recherche de documents](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[Syntaxe de requête simple](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[Syntaxe de requête complète Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[Traiter les résultats de recherche](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
