---
title: "aaaUsing Analytique - hello puissant outil de recherche de l’Application Azure Insights | Documents Microsoft"
description: "À l’aide de hello Analytique, hello diagnostic outil puissant d’Application Insights. "
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a>Utilisation d’Analytics dans Application Insights
[Analytique](app-insights-analytics.md) fonctionnalité de recherche puissant de hello de [Application Insights](app-insights-overview.md). Ces pages décrivent le langage de requête Log Analytics.

* **[Regardez la vidéo de présentation hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Testez l’Analytique sur nos données simulées](https://analytics.applicationinsights.io/demo)**  si votre application n’envoie pas de données tooApplication Insights encore.

## <a name="open-analytics"></a>Ouverture de la fonctionnalité Analytics
À partir de la ressource de base de votre application dans Application Insights, cliquez sur Analytics.

![Ouvrez portal.azure.com, ouvrez votre ressource Application Insights, puis cliquez sur Analyse.](./media/app-insights-analytics-using/001.png)

didacticiel d’inline Hello vous donne quelques idées sur ce que vous pouvez faire.

Vous pouvez cependant consulter [ici une présentation approfondie](app-insights-analytics-tour.md).

## <a name="query-your-telemetry"></a>Interrogation de votre télémétrie
### <a name="write-a-query"></a>Écrivez votre requête.
![Affichage du schéma](./media/app-insights-analytics-using/150.png)

Commencer avec des noms de toutes les tables hello figurant sur la gauche de hello hello (ou hello [plage](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) ou [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) opérateurs). Utilisez `|` toocreate un pipeline de [opérateurs](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html). 

IntelliSense affiche les opérateurs hello et éléments d’expression hello que vous pouvez utiliser. Cliquez sur icône d’information hello (ou appuyez sur CTRL + espace) tooget une description plus détaillée et des exemples de toouse chaque élément.

Consultez hello [visite guidée du langage Analytique](app-insights-analytics-tour.md) et [référence du langage](app-insights-analytics-reference.md).

### <a name="run-a-query"></a>Exécution d’une requête
![Exécution d’une requête](./media/app-insights-analytics-using/130.png)

1. Vous pouvez utiliser des sauts de ligne uniques dans une requête.
2. Placez le curseur hello à l’intérieur ou à fin hello de requête hello toorun.
3. Vérifiez la plage de temps hello de votre requête. (Vous pouvez le modifier ou le remplacer en incluant votre propre clause [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) dans la requête.)
3. Cliquez sur OK toorun hello la requête.
4. N’insérez pas de lignes vides dans votre requête. Vous pouvez conserver plusieurs requêtes séparées dans un onglet de requête en les séparant par des lignes vides. Uniquement les requêtes de hello dont le curseur de hello s’exécute.

### <a name="save-a-query"></a>Enregistrement d’une requête
![Enregistrement d’une requête](./media/app-insights-analytics-using/140.png)

1. Enregistrer le fichier de requête en cours hello.
2. Ouvrez un fichier de requête enregistré.
3. Créez un fichier de requête.

## <a name="see-hello-details"></a>Afficher les détails de hello
Développez toute ligne dans hello résultats toosee sa liste complète des propriétés. Vous pouvez développer davantage de toute propriété qui est une valeur structurée - par exemple, des dimensions personnalisées ou pile hello dans une exception.

![Extension d’une ligne](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a>Organiser les résultats de hello
Vous pouvez trier, filtrer, paginer et regrouper les résultats hello retournés à partir de votre requête.

> [!NOTE]
> Tri, regroupement et filtrage dans le navigateur de hello ne réexécutez votre requête. Ils réorganiser uniquement les résultats de hello qui ont été renvoyés par votre dernière requête. 
> 
> tooperform ces tâches dans le serveur hello hello résultats sont retournés, avant d’écrire votre requête avec hello [tri](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [résumer](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) et [où](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) opérateurs.
> 
> 

Choisir des colonnes hello vous le feriez pour tout comme toosee, faire glisser toorearrange des en-têtes de colonne, ainsi que les colonnes de redimensionnement en faisant glisser ses bordures.

![Réorganisation de colonnes](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a>Tri et filtrage d’éléments
Trier les résultats en cliquant sur head hello d’une colonne. Cliquez de nouveau sur toosort hello autre façon, et cliquez une troisième fois toorevert toohello tri d’origine retourné par la requête.

Utilisez hello filtre icône toonarrow votre recherche.

![Tri et filtrage de colonnes](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a>Regroupement d’éléments
toosort par plusieurs colonnes, utilisez le regroupement. Tout d’abord l’activer, puis faites glisser les en-têtes de colonne dans l’espace hello au-dessus de table de hello.

![Groupe](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a>Certains résultats manquent ?

Si vous pensez que vous ne voyez pas tous les résultats hello prévu, il existe plusieurs raisons possibles.

* **Filtre d'intervalle de temps**. Par défaut, vous verrez seulement les résultats à partir de hello des dernières 24 heures. Il existe un filtre automatique qui limite la plage hello de résultats qui sont récupérés à partir des tables de source de hello. 

    Toutefois, vous pouvez modifier l’intervalle de temps hello filtre à l’aide du menu déroulant de hello.

    Ou vous pouvez remplacer la plage d’automatique hello en incluant votre propre [ `where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) dans votre requête. Par exemple :

    `requests | where timestamp > ago('2d')`

* **Limite de résultats**. Il existe une limite de lignes environ 10 k hello de résultats à partir du portail de hello. Un avertissement apparaît si vous passez la limite hello. Si cela se produit, vos résultats dans la table de hello de tri ne sont pas toujours afficher vous tous les hello réel premier ou derniers résultats. 

    Il s’agit de limite de bonnes pratiques tooavoid atteinte hello. Utilisez le filtre d’intervalle de temps hello, ou utiliser des opérateurs tels que :

  * [top 100 by timestamp](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [take 100](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [summarize ](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [where timestamp &gt; ago(3d)](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

(Vous voulez plus de 10 000 lignes ? Utilisez plutôt l'[exportation continue](app-insights-export-telemetry.md). Analytics est conçu pour l'analyse plutôt que pour la récupération de données brutes.)

## <a name="diagrams"></a>Diagrammes
Sélectionnez le type hello du diagramme que vous souhaitez :

![Sélectionnez un type de diagramme](./media/app-insights-analytics-using/230.png)

Si vous avez plusieurs colonnes de types de droite hello, vous pouvez choisir hello x et y axes et une colonne de résultats de hello toosplit dimensions par.

Par défaut, les résultats sont initialement affichés sous forme de table, et sélectionne diagramme de hello. Mais vous pouvez utiliser hello [restituer la directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) à fin hello d’une requête de tooselect un diagramme.

### <a name="analytics-diagnostics"></a>Diagnostic analytique


Sur un timechart, s’il existe un pic soudain ou une étape dans vos données, vous pouvez voir un point de mise en surbrillance sur la ligne de hello. Cela indique que les Diagnostics Analytique a identifié une combinaison des propriétés qui filtrent les modifications soudaines hello. Cliquez sur hello point tooget plus de détails sur le filtrage de hello et version filtrée de toosee hello. Cela peut vous aider à identifier le changement de hello dû. 

[En savoir plus sur le diagnostic analytique](app-insights-analytics-diagnostics.md)


![Diagnostic analytique](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a>Code confidentiel toodashboard
Vous pouvez épingler un tooone de schéma ou une table de votre [partagé des tableaux de bord](app-insights-dashboards.md) -cliquez simplement le code confidentiel de hello. (Vous devrez peut-être trop[mise d’à niveau votre application de tarification du package](app-insights-pricing.md) tooturn sur cette fonctionnalité.) 

![Cliquez sur le code confidentiel de hello](./media/app-insights-analytics-using/pin-01.png)

Cela signifie que, lorsque vous placez ensemble un toohelp de tableau de bord que vous surveillez les performances hello ou l’utilisation de vos services web, vous pouvez inclure une analyse complexe en même temps que hello autres métriques. 

Vous pouvez épingler un tableau de bord toohello de table, si elle a moins de quatre colonnes. Uniquement hello sept premières lignes sont affichés.

### <a name="dashboard-refresh"></a>Actualisation du tableau de bord
tableau de bord toohello Hello graphique épinglé est actualisé automatiquement par la nouvelle exécution de requête de hello environ toutes les heures. Vous pouvez également cliquer sur le bouton d’actualisation hello.

### <a name="automatic-simplifications"></a>Simplifications automatiques

Certaines simplifications sont appliqués tooa graphique quand vous l’épinglez tooa le tableau de bord.

**Restriction de temps :** requêtes sont automatiquement limité toohello cours des 14 derniers jours. Hello effet est hello identique comme si votre requête inclut `where timestamp > ago(14d)`.

**Restriction relative au nombre de compartimenter :** si vous affichez un graphique qui possède un grand nombre d’emplacements discrets (en général, un graphique à barres), hello moins remplis emplacements sont automatiquement regroupés en un seul « d’autres » bin. Par exemple, cette requête :

    requests | summarize count_search = count() by client_CountryOrRegion

se présente sous la forme suivante dans Analytics :

![Graphique à longue traîne](./media/app-insights-analytics-using/pin-07.png)

mais lorsque vous l’épinglez tooa le tableau de bord, il ressemble à ceci :

![Graphique comportant des emplacements limités](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a>Exportation tooExcel
Une fois votre requête exécutée, vous pouvez télécharger un fichier .csv. Cliquez sur **Exporter, Excel**.

## <a name="export-toopower-bi"></a>Exportation tooPower BI
Placez le curseur à hello dans une requête et choisissez **exporter, Power BI**.

![Exporter à partir de l’Analytique tooPower BI](./media/app-insights-analytics-using/240.png)

Exécution de requête de hello dans Power BI. Vous pouvez définir toorefresh selon une planification.

Avec Power BI, vous pouvez créer des tableaux de bord qui rassemblent les données issues d’un large éventail de sources.

[En savoir plus sur l’exportation tooPower BI](app-insights-export-power-bi.md)

## <a name="deep-link"></a>Lien ciblé

Obtenez un lien sous **exportation, liaison de partage** que vous pouvez envoyer tooanother utilisateur. Condition hello utilisateur a [groupe de ressources accès tooyour](app-insights-resources-roles-access-control.md), requête de hello s’ouvre dans hello l’interface utilisateur de l’Analytique.

(Dans le lien de hello, le texte de requête hello apparaît après « ? q = », compressés gzip et codé en base 64. Vous pouvez écrire des liens profonds toogenerate de code que vous fournissez toousers. Toutefois, hello recommandé est de façon toorun Analytique à partir du code à l’aide de hello [API REST](https://dev.applicationinsights.io/).)


## <a name="automation"></a>Automatisation

Hello d’utilisation [données accès REST API](https://dev.applicationinsights.io/) toorun des requêtes Analytique. [Par exemple](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (à l’aide de PowerShell) :

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

Contrairement à l’interface utilisateur de l’Analytique de hello, hello API REST n’ajoute pas automatiquement les requêtes tooyour de limitation timestamp. N’oubliez pas de tooadd votre propre clause where, tooavoid obtenir des réponses énormes.



## <a name="import-data"></a>Importer des données

Vous pouvez importer des données à partir d’un fichier CSV. Une utilisation classique est tooimport les données statiques que vous pouvez joindre des tables à partir de votre télémétrie. 

Par exemple, si les utilisateurs authentifiés sont identifiées dans vos données de télémétrie à un id obscurci ou un alias, vous pouvez importer une table qui mappe les noms d’alias tooreal. En effectuant une jointure sur la télémétrie des requêtes hello, vous pouvez identifier les utilisateurs par leur nom réel dans les rapports d’Analytique hello.

### <a name="define-your-data-schema"></a>Définir votre schéma de données

1. Cliquez sur **Paramètres** (en haut à gauche), puis sur **Sources de données**. 
2. Ajouter une source de données, en suivant les instructions hello. Vous êtes invité à toosupply un échantillon de données hello, qui doivent inclure au moins dix lignes. Vous corrigez ensuite le schéma de hello.

Définit une source de données, vous pouvez ensuite utiliser tooimport des tables individuelles.

### <a name="import-a-table"></a>Importer une table

1. Ouvrez votre définition de source de données à partir de la liste de hello.
2. Cliquez sur « Télécharger » et suivre la table de hello instructions tooupload hello. Cela implique un tooa appel API REST, et il est donc facile tooautomate. 

Votre table est désormais disponible pour une utilisation dans des requêtes Analytics. Elle apparaîtra dans Analytics 

### <a name="use-hello-table"></a>Utilisez la table de hello

Supposons que votre définition de source de données s'appelle `usermap` et comporte deux champs, `realName` et `user_AuthenticatedId`. Hello `requests` table possède également un champ nommé `user_AuthenticatedId`, par conséquent, il est facile toojoin les :

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
la table résultante de demandes Hello a une colonne supplémentaire, `realName`.

### <a name="import-from-logstash"></a>Importer à partir de LogStash

Si vous utilisez [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), vous pouvez utiliser Analytique tooquery vos journaux. Hello d’utilisation [plug-in qui envoie des données dans Analytique](https://github.com/Microsoft/logstash-output-application-insights). 

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

