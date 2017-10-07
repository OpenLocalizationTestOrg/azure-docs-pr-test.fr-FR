---
title: "aaaA guidée Analytique dans Azure Application Insights | Documents Microsoft"
description: "Exemples courts de toutes les requêtes principales hello Analytique, hello puissant outil de recherche de l’Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: bddf4a6d-ea8d-4607-8531-1fe197cc57ad
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/06/2017
ms.author: bwren
ms.openlocfilehash: c268e26c6bf93ac2ee2a9d5e83613150dcf90b04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a>Visite guidée d’Analytics dans Application Insights
[Analytique](app-insights-analytics.md) fonctionnalité de recherche puissant de hello de [Application Insights](app-insights-overview.md). Ces pages décrivent le langage de requête Log Analytics.

* **[Regardez la vidéo de présentation hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Testez l’Analytique sur nos données simulées](https://analytics.applicationinsights.io/demo)**  si votre application n’envoie pas de données tooApplication Insights encore.
* **[Feuille de graphique SQL utilisateurs](https://aka.ms/sql-analytics)**  traduit idiomes courants de hello.

Nous allons vous guide dans certaines tooget de requêtes de base que vous avez démarré.

## <a name="connect-tooyour-application-insights-data"></a>Connecter des données d’Application Insights tooyour
Ouvrez Analytics à partir du [panneau Vue d’ensemble](app-insights-dashboards.md) de votre application dans Application Insights :

![Ouvrez portal.azure.com, ouvrez votre ressource Application Insights, puis cliquez sur Analyse.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a>[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): afficher n lignes
Les points de données qui consignent les opérations des utilisateurs (généralement des requêtes HTTP reçues par votre application web) sont stockés dans une table appelée `requests`. Chaque ligne est un point de données de télémétrie reçu de hello Application Insights SDK dans votre application.

Nous pouvons commencer en examinant quelques exemples de lignes de table de hello :

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> Placez curseur à hello quelque part dans l’instruction de hello avant de cliquer sur OK. Vous pouvez répartir une instruction sur plusieurs lignes, mais ne placez pas de lignes vides dans une instruction. Lignes vides sont un moyen pratique de tookeep plusieurs séparer les requêtes dans la fenêtre hello.
>
>

Choisissez les colonnes, faites-les glisser, groupez-les par colonnes et filtrez :

![Cliquez sur le sélecteur de colonnes en haut à droite des résultats](./media/app-insights-analytics-tour/030.png)

Développez les détails toosee hello :

![Choisissez la vue de table et utilisez Configurer les colonnes](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> Cliquez sur en-tête hello d’une colonne toore-trier hello les résultats disponibles dans le navigateur web de hello. Mais gardez à l’esprit que, pour un grand jeu de résultats, nombre de hello du navigateur toohello téléchargé de lignes est limité. Tri de cette manière n’affiche toujours pas vous hello réel le plus élevé ou les éléments de la plus basse. les éléments toosort utilisent de manière fiable, hello `top` ou `sort` opérateur.
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a>[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) et [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)
`take`est utile tooget un exemple rapide d’un résultat, mais il affiche des lignes de table de hello dans aucun ordre particulier. tooget un affichage ordonné, utilisez `top` (pour obtenir un exemple) ou `sort` (sur la table entière de hello).

Afficher hello n premières lignes, classés par une colonne particulière :

```AIQL

    requests | top 10 by timestamp desc
```

* *Syntaxe :* la plupart des opérateurs ont des paramètres de mot clé comme `by`.
* `desc` = ordre décroissant, `asc` = ordre croissant.

![](./media/app-insights-analytics-tour/260.png)

`top...` est une manière plus performante d’exprimer `sort ... | take...`. Nous aurions pu écrire :

```AIQL

    requests | sort by timestamp desc | take 10
```

résultat de Hello serait hello identiques, mais elle sera exécutée un peu plus lentement. (Vous pouvez également écrire `order`, qui est un alias de `sort`.)

les en-têtes de colonne Hello dans la vue de table hello peuvent également être utilisé toosort les résultats de hello sur l’écran hello. Mais bien entendu, si vous avez utilisé `take` ou `top` tooretrieve une partie seulement d’une table, vous allez uniquement réorganiser hello les enregistrements que vous avez récupéré.

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a>[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtrage sur une condition

Concentrons-nous sur les requêtes qui ont renvoyé un code de résultat particulier :

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

Hello `where` l’opérateur accepte une expression booléenne. Voici quelques points clés les concernant :

* `and`, `or` : opérateurs booléens
* `==`, `<>`, `!=` : égal à et différent de
* `=~`, `!~` : chaîne ne respectant pas la casse (égal à et différent de). Il existe de nombreux autres opérateurs de comparaison de chaîne.

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a>Mise en route du type approprié de hello
Rechercher les requêtes ayant échoué :

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a>Temps

Par défaut, vos requêtes sont restreinte toohello des dernières 24 heures. Mais vous pouvez modifier cette plage :

![](./media/app-insights-analytics-tour/change-time-range.png)

Remplacer l’intervalle de temps hello en écrivant une requête qui mentionne `timestamp` dans une clause where. Par exemple :

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

fonction de plage de temps Hello est équivalent tooa 'where' clause inséré après chaque mention d’une des tables de source de hello.

`ago(3d)` signifie « il y a trois jours ». Il existe d’autres unités de temps, par exemple les heures (`2h`, `2.5h`), les minutes (`25m`) et les secondes (`10s`).

Autres exemples :

```AIQL

    // Last calendar week:
    requests
    | where timestamp > startofweek(now()-7d)
        and timestamp < startofweek(now())
    | top 5 by duration

    // First hour of every day in past seven days:
    requests
    | where timestamp > ago(7d) and timestamp % 1d < 1h
    | top 5 by duration

    // Specific dates:
    requests
    | where timestamp > datetime(2016-11-19) and timestamp < datetime(2016-11-21)
    | top 5 by duration

```

[Référence sur les dates et les heures](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a>[Projet](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) : sélectionnez, renommez et calculez des colonnes
Utilisez [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick simplement les colonnes hello souhaité :

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

Vous pouvez également renommer des colonnes et en définir de nouvelles :

```AIQL

    requests
    | top 10 by timestamp desc
    | project  
            name,
            response = resultCode,
            timestamp,
            ['time of day'] = floor(timestamp % 1d, 1s)
```

![result](./media/app-insights-analytics-tour/270.png)

* Les noms de colonnes peuvent contenir des espaces ou des symboles s’ils sont placés entre crochets comme suit : `['...']` ou `["..."]`
* `%`est hello habituel opérateur modulo.
* `1d` (le chiffre un, suivi de la lettre d) est un littéral d’intervalle de temps qui signifie un jour. Voici d’autres littéraux d’intervalle de temps : `12h`, `30m`, `10s`, `0.01s`.
* `floor`(alias `bin`) Arrondit une valeur vers le bas toohello multiple de valeur de base hello vous fournissez le plus proche. Par conséquent, `floor(aTime, 1s)` Arrondit vers le bas toohello plus proche de la seconde fois.

Les expressions peuvent inclure tous les opérateurs habituels hello (`+`, `-`,...), et il existe une gamme de fonctions utiles.

## <a name="extend"></a>Extend
Si vous souhaitez simplement tooadd toohello de colonnes des groupes existants, utilisez [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

À l’aide de [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) est moins détaillé que [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) si vous souhaitez tookeep tous hello colonnes existantes.

### <a name="convert-toolocal-time"></a>Convertir l’heure de toolocal

Les timestamps sont toujours exprimés en UTC. Par conséquent, si vous êtes sur hello nous Nord, et il s’agit d’hiver, vous pouvez comme ceci :

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a>[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): agréger des groupes de lignes
`Summarize` applique une *fonction d’agrégation* spécifiée sur des groupes de lignes.

Par exemple, le temps de hello votre application web prend toorespond tooa demande est indiqué dans le champ de hello `duration`. Voyons de réponse moyen de hello tooall demandes de temps :

![](./media/app-insights-analytics-tour/410.png)

Ou bien, nous avons séparer le résultat de hello dans des demandes de noms différents :

![](./media/app-insights-analytics-tour/420.png)

`Summarize`collecte hello des points de données dans le flux de hello en groupes pour le hello `by` clause évalue également. Chaque valeur Bonjour `by` expression - chaque nom de l’opération Bonjour exemple ci-dessus - génère une ligne dans la table de résultats hello.

Nous pouvons également regrouper les résultats par heure :

![](./media/app-insights-analytics-tour/430.png)

Notez la façon dont nous utilisons hello `bin` (fonction) (également appelé `floor`). Si nous avions simplement utilisé `by timestamp`, chaque ligne d’entrée apparaîtrait dans un groupe individuel. Pour n’importe quel scalaire continue like heures ou des nombres, nous avons plage continue de toobreak hello dans un nombre raisonnable de valeurs discrètes. `bin`-qui est simplement hello familiers arrondi vers le bas `floor` fonction - est toodo de façon plus simple de hello qui.

Nous pouvons utiliser hello même plages de tooreduce technique de chaînes :

![](./media/app-insights-analytics-tour/440.png)

Notez que vous pouvez utiliser `name=` nom de hello tooset d’une colonne de résultats, dans les expressions d’agrégation hello ou la clause by hello.

## <a name="counting-sampled-data"></a>Décompte des données échantillonnées
`sum(itemCount)`est hello recommandée toocount événements d’agrégation. Dans de nombreux cas, itemCount == 1, afin de la fonction hello compte simplement nombre de hello de lignes dans le groupe de hello. Mais lorsque [échantillonnage](app-insights-sampling.md) est dans l’opération, seule une fraction d’événements d’origine de hello sont conservées en tant que points de données d’Application Insights, de sorte que pour chaque point de données que vous voyez, `itemCount` événements.

Par exemple, si l’échantillonnage ignore 75 % des événements d’origine de hello, puis itemCount == 4 dans les enregistrements hello conservée - autrement dit, pour chaque enregistrement de retenue, il existait quatre enregistrements d’origine.

Échantillonnage Adaptive entraîne toobe itemCount plus élevé pendant les périodes lorsque votre application est utilisée de manière intensive.

Cumulant itemCount donne donc une bonne estimation du nombre d’origine de hello d’événements.

![](./media/app-insights-analytics-tour/510.png)

Il existe également un `count()` d’agrégation (et une opération count), pour les cas où vous vraiment voulez nombre de hello toocount de lignes dans un groupe.

Il existe toute une gamme de [fonctions d’agrégation](https://docs.loganalytics.io/learn/tutorials/aggregations.html).

## <a name="charting-hello-results"></a>Graphique des résultats de hello
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

Par défaut, les résultats sont affichés sous forme de table :

![](./media/app-insights-analytics-tour/225.png)

Nous pouvons faire de meilleures performances que la vue de table hello. Examinons les résultats hello dans la vue du graphique hello avec l’option de barre verticale hello :

![Cliquez sur la vue graphique, puis choisissez le graphique à barres verticales et affectez les axes x et y](./media/app-insights-analytics-tour/230.png)

Notez que bien que nous n’avez pas trier les résultats de hello par heure (comme vous pouvez le voir dans l’affichage de la table hello), affichage du graphique hello affiche toujours les dates/heures dans le bon ordre.


## <a name="timecharts"></a>Graphiques temporels
Afficher le nombre d’événements qui se produisent chaque heure :

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

Sélectionnez l’option d’affichage graphique hello :

![Graphique temporel](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a>Séries multiples
Plusieurs expressions Bonjour `summarize` clause crée plusieurs colonnes.

Plusieurs expressions Bonjour `by` clause crée plusieurs lignes, une pour chaque combinaison de valeurs.

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tableau de demandes par heure et par emplacement](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a>Segmentez un graphique par dimensions
Si graphique sur une table qui comporte une colonne de chaîne et une colonne numérique, chaîne de hello peut être utilisé toosplit hello des données numériques en séries distinctes de points. S’il existe plusieurs colonnes de chaîne, vous pouvez choisir quels toouse de colonne en tant que discriminateur de hello.

![Segmenter un tableau d’analyse](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a>Taux de rebond

Convertir un toouse de chaîne booléenne tooa comme un discriminateur :

```AIQL

    // Bounce rate: sessions with only one page view
    requests
    | where notempty(session_Id)
    | where tostring(operation_SyntheticSource) == "" // real users
    | summarize pagesInSession=sum(itemCount), sessionEnd=max(timestamp)
               by session_Id
    | extend isbounce= pagesInSession == 1
    | summarize count()
               by tostring(isbounce), bin (sessionEnd, 1h)
    | render timechart
```

### <a name="display-multiple-metrics"></a>Afficher plusieurs mesures
Si vous représenter une table qui comporte plus d’une colonne numérique, dans Ajout toohello timestamp, vous pouvez afficher n’importe quelle combinaison d’eux.

![Segmenter un tableau d’analyse](./media/app-insights-analytics-tour/110.png)

Vous devez sélectionner **Ne pas fractionner** avant de pouvoir sélectionner plusieurs colonnes numériques. Vous ne peut pas fractionner en une colonne de chaîne à hello même temps en tant que l’affichage de plusieurs colonnes numériques.

## <a name="daily-average-cycle"></a>Cycle moyen quotidien
Dans quelle mesure l’utilisation de fonction sur une journée moyenne et hello ?

Demandes de nombre par heure hello modulo une journée, placées dans heures :

```AIQL

    requests
    | where timestamp > ago(30d)  // Override "Last 24h"
    | where tostring(operation_SyntheticSource) == "" // real users
    | extend hour = bin(timestamp % 1d , 1h)
          + datetime("2016-01-01") // Allow render on line chart
    | summarize event_count=sum(itemCount) by hour
```

![Graphique en courbes des heures dans une journée moyenne](./media/app-insights-analytics-tour/120.png)

> [!NOTE]
> Notez que nous disposons tooconvert temps durées toodatetimes dans l’ordre toodisplay sur un graphique en courbes.
>
>

## <a name="compare-multiple-daily-series"></a>Comparer plusieurs séries quotidiennes
Comment l’utilisation de varier au fil du temps hello du jour dans différents pays ?

```AIQL

     requests  
     | where timestamp > ago(30d)  // Override "Last 24h"
     | where tostring(operation_SyntheticSource) == "" // real users
     | extend hour= floor( timestamp % 1d , 1h)
           + datetime("2001-01-01")
     | summarize event_count=sum(itemCount)
       by hour, client_CountryOrRegion
     | render timechart
```

![Fractionner par client_CountryOrRegion](./media/app-insights-analytics-tour/130.png)

## <a name="plot-a-distribution"></a>Tracer une distribution
Combien existe-t-il de sessions de différentes longueurs ?

```AIQL

    requests
    | where timestamp > ago(30d) // override "Last 24h"
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sessionDuration = max_timestamp - min_timestamp
    | where sessionDuration > 1s and sessionDuration < 3m
    | summarize count() by floor(sessionDuration, 3s)
    | project d = sessionDuration + datetime("2016-01-01"), count_
```

Hello dernière ligne est requis tooconvert toodatetime. Axe hello x d’un graphique est actuellement affiché en tant qu’une valeur scalaire uniquement s’il est une valeur datetime.

Hello `where` clause exclut les sessions Shot (Durée_de_la_session == 0) et jeux hello longueur de l’axe des abscisses hello.

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[Centiles](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
Quelles sont les plages de durées qui couvrent différents pourcentages de sessions ?

Utilisez hello au-dessus de requête, mais remplacez hello dernière ligne :

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s)
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
```

Nous avons supprimé également limite supérieure de hello Bonjour où clause, dans l’ordre tooget corriger des chiffres, y compris toutes les sessions avec plusieurs demandes :

![result](./media/app-insights-analytics-tour/180.png)

Nous pouvons voir que :

* 5 % des sessions durent moins de 3 minutes 34 s ;
* 50 % des sessions durent moins de 36 minutes ;
* 5 % des sessions durent plus de 7 jours.

tooget une répartition distincte pour chaque pays, nous avons simplement avoir toobring hello client_CountryOrRegion colonne séparément à la fois résumer les opérateurs :

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id, client_CountryOrRegion
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s), client_CountryOrRegion
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
      by client_CountryOrRegion
```

![](./media/app-insights-analytics-tour/190.png)

## <a name="join"></a>Join
Nous avons accès tooseveral tables, y compris les demandes et les exceptions.

Nous pouvons toofind hello exceptions connexes tooa demande a renvoyé une réponse d’échec, joindre des tables de hello sur `session_Id`:

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


Il est conseillé toouse `project` tooselect les colonnes hello simplement nous avons besoin avant d’effectuer hello jointure.
Bonjour les clauses de mêmes, nous renommer la colonne de type timestamp hello.

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a>[Laisser](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): assignez une variable tooa de résultat

Utilisez `let` tooseparate parties hello de l’expression précédente de hello. résultats de Hello sont identiques :

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> Dans le client d’Analytique hello, ne placez pas de lignes vides entre les parties hello de requête de hello. Vérifiez que tooexecute tous les de celui-ci.
>

Utilisez `toscalar` tooconvert une valeur de tooa de cellule de table unique :

```AIQL
let topCities =  toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City));
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```


### <a name="functions"></a>Fonctions

Utilisez *permettent* toodefine une fonction :

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a>Accès à des objets imbriqués
Les objets imbriqués sont faciles d’accès. Par exemple, dans le flux d’exceptions hello, vous pouvez voir des objets structurés comme suit :

![result](./media/app-insights-analytics-tour/520.png)

Vous pouvez aplatir en choisissant Propriétés hello que vous intéresse :

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

Notez que vous devez toocast hello résultat toohello approprié de type.


## <a name="custom-properties-and-measurements"></a>Mesures et propriétés personnalisées
Si votre application se connecte [dimensions personnalisées (propriétés) et des mesures personnalisées](app-insights-api-custom-events-metrics.md#properties) tooevents, puis vous les voyez dans hello `customDimensions` et `customMeasurements` objets.

Par exemple, si votre application inclut :

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

tooextract ces valeurs dans Analytique :

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

tooverify si une dimension personnalisée est d’un type particulier :

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a>Tableaux de bord
Vous pouvez épingler votre tableau de bord de tooa de résultats dans l’ordre toobring ensemble toutes vos tables et graphiques plus importantes.

* [Tableau de bord partagé Azure](app-insights-dashboards.md#share-dashboards): cliquez sur l’icône d’épingle hello. Avant cela, vous devez disposer d’un tableau de bord partagé. Bonjour portail Azure, ouvrez ou créez un tableau de bord, puis cliquez sur Partager.
* [Tableau de bord Power BI](app-insights-export-power-bi.md) : cliquez sur Exporter, Requête Power BI. L’avantage de cette solution est que vous pouvez afficher votre requête avec d’autres résultats issus d’un large éventail de sources.

## <a name="combine-with-imported-data"></a>Combiner avec des données importées

Analytique rapports superbes sur tableau de bord hello, mais vous pouvez souhaiter tootranslate hello données tooa formulaire digestibles plus. Par exemple, supposons que vos utilisateurs authentifiés sont identifiés dans les données de télémétrie hello par un alias. Vous aimeriez tooshow leur réel des noms dans les résultats. toodo, vous avez besoin d’un fichier CSV qui mappe les noms réels des toohello alias hello.

Vous pouvez importer un fichier de données et l’utiliser comme une des tables standard de hello (demandes, exceptions et ainsi de suite). Interrogez-la individuellement ou joignez-la à d’autres tables. Par exemple, si vous disposez d’une table nommée usermap, et il a des colonnes `realName` et `userId`, vous pouvez utiliser tootranslate hello `user_AuthenticatedId` de télémétrie des requêtes hello :

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

tooimport une table, dans le panneau de schéma hello, sous **autres Sources de données**, suivez hello instructions tooadd une nouvelle source de données, en téléchargeant un échantillon de vos données. Ensuite, vous pouvez utiliser les tables de tooupload de cette définition.

fonctionnalité d’importation Hello étant actuellement en version préliminaire, vous verrez initialement un lien « Contactez-nous » sous « Autres sources de données ». Utilisez cette toosign de programme d’évaluation toohello et lien de hello est alors remplacé par un bouton « Ajouter une nouvelle source de données ».


## <a name="tables"></a>Tables
flux Hello de télémétrie reçu à partir de votre application est accessible par plusieurs tables. schéma Hello des propriétés disponibles pour chaque table est visible à gauche de hello de fenêtre hello.

### <a name="requests-table"></a>Table de requêtes
Nombre de requêtes HTTP tooyour web app et le segment par nom de page :

![Compter les requêtes segmentées par nom](./media/app-insights-analytics-tour/analytics-count-requests.png)

Recherche les demandes de hello qui échouent le plus :

![Compter les requêtes segmentées par nom](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a>Table des événements personnalisés
Si vous utilisez [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend vos propres événements, vous pouvez les lire à partir de cette table.

Prenons un exemple dans lequel le code de votre application contient les lignes suivantes :

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

Affichage de la fréquence de hello de ces événements :

![Afficher la fréquence des événements personnalisés](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

Extraire les événements hello mesures et dimensions :

![Afficher la fréquence des événements personnalisés](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a>Table des mesures personnalisées
Si vous utilisez [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend vos propres valeurs de mesure, vous trouverez ses résultats dans hello **customMetrics** flux. Par exemple :  

![Mesures personnalisées dans Application Insights Analytics](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> Dans [Metrics Explorer](app-insights-metrics-explorer.md), toutes les mesures personnalisées type tooany joint de télémétrie apparaissent ensemble dans Panneau de métriques hello avec envoyé à l’aide de mesures `TrackMetric()`. Mais, dans Analytique, des mesures personnalisées sont toujours attachés type toowhichever de télémétrie qu’ils ont été effectuées sur les événements ou les demandes et ainsi de suite - tandis que les métriques envoyés par TrackMetric s’affichent dans leur propre flux de données.
>
>

### <a name="performance-counters-table"></a>Table des compteurs de performances
[Les compteurs de performances](app-insights-performance-counters.md) vous indiquent les métriques système de base pour votre application, notamment le processeur, la mémoire et l’utilisation du réseau. Vous pouvez configurer hello SDK toosend compteurs supplémentaires, y compris vos propres compteurs personnalisés.

Hello **performanceCounters** schéma expose hello `category`, `counter` nom, et `instance` nom de chaque compteur de performance. Noms d’instance de compteur toosome applicables uniquement les compteurs de performances et indiquent généralement le nom hello de hello processus toowhich hello count est lié. Télémétrie hello pour chaque application, vous voyez uniquement les compteurs de hello pour cette application. Par exemple, toosee les compteurs sont disponibles :

![Compteurs de performances dans Application Insights Analytics](./media/app-insights-analytics-tour/analytics-performance-counters.png)

tooget un graphique de mémoire disponible sur hello sélectionné période :

![Graphique temporel dans Application Insights Analytics](./media/app-insights-analytics-tour/analytics-available-memory.png)

Comme les autres données de télémétrie, **performanceCounters** possède également une colonne `cloud_RoleInstance` qui indique l’identité hello de l’ordinateur hôte de hello sur lequel votre application est en cours d’exécution. Par exemple, toocompare hello des performances de votre application sur des ordinateurs différents hello :

![Performances segmentées par instances de rôle d’Application Insights Analytics](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a>Table des exceptions
[Les exceptions signalées par votre application](app-insights-asp-net-exceptions.md) sont disponibles dans cette table.

toofind hello demande HTTP qui gère votre application lorsque hello exception a été levée, joindre sur identifiant_opération :

![Ajoutez des exceptions avec des requêtes operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a>Table des délais de chargement dans le navigateur
`browserTimings` affiche les données de chargement de pages collectées dans les navigateurs de vos utilisateurs.

[Configurer votre application pour les données de télémétrie côté client](app-insights-javascript.md) commander toosee ces mesures.

schéma de Hello inclut [métriques indiquant les longueurs de hello des différentes étapes du processus de chargement de la page hello](app-insights-javascript.md#page-load-performance). (Ils n’indiquent pas la durée hello que vos utilisateurs lire une page.)  

Afficher popularities hello de différentes pages et temps pour chaque page de chargement :

![Délai de chargement de page dans Analytics](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a>Tableau de résultats de la disponibilité
`availabilityResults`affiche hello les résultats de votre [tests web](app-insights-monitor-web-app-availability.md). Chaque exécution de vos tests à partir de chaque emplacement est déclarée séparément.

![Délai de chargement de page dans Analytics](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a>Table des dépendances
Contient les résultats des appels de que votre application effectue des toodatabases et API REST appelle tooTrackDependency(). Inclut également les appels AJAX effectuées à partir du navigateur de hello.

Appels AJAX à partir du navigateur de hello :

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

Appels de dépendance à partir du serveur de hello :

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

Toujours affichent les résultats de la dépendance du côté serveur `success==False` si hello Application Insights Agent n’est pas installé. Toutefois, hello autres données sont correctes.

### <a name="traces-table"></a>Table des traces
Contient les données de télémétrie hello envoyées par votre application à l’aide de TrackTrace(), ou [autres infrastructures de journalisation](app-insights-asp-net-trace-logs.md).

## <a name="video"></a>Vidéo 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

Requêtes avancées :

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a>Étapes suivantes
* [Référence sur le langage Analytics](app-insights-analytics-reference.md)
* [Feuille de graphique SQL utilisateurs](https://aka.ms/sql-analytics) traduit idiomes courants de hello.

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
