---
title: "données aaaFind avec des recherches de journaux dans Azure journal Analytique | Documents Microsoft"
description: "Recherches de journal vous toocombine et mettre en corrélation des données machine de plusieurs sources dans votre environnement."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a>Trouver des données avec les recherches de journaux dans Log Analytics

>[!NOTE]
> Cet article décrit les recherches de journal à l’aide du langage de requête en cours hello dans Analytique de journal.  Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis vous devez faire référence trop[Understanding log recherche Analytique de journal (nouveau)](log-analytics-log-search-new.md).


Au cœur de hello d’Analytique de journal est fonction de recherche de journal hello qui vous permet de toocombine et mettre en corrélation des données machine de plusieurs sources dans votre environnement. Les solutions sont également alimentées par toobring de recherche de journal vous mesures cernant un domaine problématique en particulier.

Sur la page de recherche de hello, vous pouvez créer une requête, puis lorsque vous recherchez, vous pouvez filtrer les résultats de hello à l’aide de contrôles de facette. Vous pouvez également créer des rapports, le filtrage et des requêtes avancées tootransform sur vos résultats.

Les requêtes de recherche de journal courantes apparaissent dans la plupart des pages de solutions. Dans l’ensemble de la console OMS hello, vous pouvez cliquer sur les vignettes ou Explorer les éléments tooother tooview plus d’informations sur l’élément de hello par à l’aide de la recherche de journal.

Dans ce didacticiel, nous examinerons exemples toocover toutes les notions de base hello lorsque vous utilisez la recherche de journal.

Nous allons commencer par des exemples simples et pratiques, puis générez sur les afin que vous pouvez obtenir une compréhension pratique de cas d’utilisation sur le mode insights de hello toouse hello syntaxe tooextract à partir des données de hello.

Une fois que vous êtes familiarisé avec les techniques de recherche, vous pouvez passer en revue hello [Analytique de journal journal référence de recherche](log-analytics-search-reference.md).

## <a name="use-basic-filters"></a>Utilisation de filtres de base
Hello première tooknow est que hello première partie d’une requête de recherche, avant tout » | « caractère de barre verticale est toujours un *filtre*. Vous pouvez la considérer comme une clause WHERE dans TSQL : elle détermine *que* sous-ensemble de toopull de données en dehors de la banque de données OMS hello. La recherche dans le magasin de données hello consiste principalement à préciser les caractéristiques hello de hello données tooextract, par conséquent, il est naturel qu’une requête commence avec la clause WHERE de hello.

Hello filtres les plus simples que vous pouvez utiliser sont *mots clés*, tels que « error » ou « timeout » ou un nom d’ordinateur. Ces types de requêtes simples retournent généralement différentes formes de données au sein de hello même jeu de résultats. Il s’agit, car le journal Analytique dispose de différents *types* des données dans le système de hello.

### <a name="tooconduct-a-simple-search"></a>tooconduct une recherche simple
1. Dans le portail OMS : hello, cliquez sur **recherche de journal**.  
    ![Vignette Rechercher](./media/log-analytics-log-searches/oms-overview-log-search.png)
2. Dans le champ de requête hello, tapez `error` puis cliquez sur **recherche**.  
    ![Recherche d’erreur](./media/log-analytics-log-searches/oms-search-error.png)  
    Par exemple, les requêtes hello pour `error` Bonjour image suivante a retourné 100 000 **événement** enregistrements (collectés par la gestion du journal), 18 **ConfigurationAlert** (générés par la Configuration des enregistrements Évaluation) et 12 **ConfigurationChange** enregistrements (capturés par le suivi des modifications de hello).   
    ![Recherche de résultats](./media/log-analytics-log-searches/oms-search-results01.png)  

Ces filtres ne sont pas vraiment des classes/types d'objet. *Type* est simplement une balise ou une propriété ou une chaîne/nom/une catégorie, qui est attaché tooa donnée. Certains documents dans hello système sont marqués en tant que **Type : ConfigurationAlert** et certaines sont marqués en tant que **Type : Perf**, ou **Type : Event**, et ainsi de suite. Chaque résultat de recherche, document, enregistrement ou entrée affiche toutes les propriétés brutes hello et leurs valeurs pour chacun de ces éléments de données, et vous pouvez utiliser ces toospecify de noms de champ de filtre de hello lorsque vous souhaitez que seuls les enregistrements hello tooretrieve dont le champ de hello a cette donnée valeur.

Le *type* est simplement un champ que tous les enregistrements ont. Il n'est pas différent des autres champs. Cela a été établi en fonction de valeur hello du champ de Type hello. Cet enregistrement aura une autre forme. Par ailleurs, **Type = Perf**, ou **Type = Event** est également hello syntaxe que vous avez besoin de toolearn tooquery pour les données de performances ou des événements.

Vous pouvez utiliser un signe deux-points ( :) ou un signe égal (=) après le nom du champ hello et avant la valeur de hello. **Type : Event** et **Type = Event** sont équivalentes dans un sens, vous pouvez choisir hello style qui vous convient.

Par conséquent, si hello Type = Perf enregistrements ont un champ appelé « CounterName », puis vous pouvez écrire une requête qui ressemble à `Type=Perf CounterName="% Processor Time"`.

Cela vous donnera des données de performances hello uniquement où le nom de compteur de performance hello est « % temps processeur ».

### <a name="toosearch-for-processor-time-performance-data"></a>toosearch pour les données de performance du temps processeur
* Dans le champ de requête de recherche hello, tapez`Type=Perf CounterName="% Processor Time"`

Vous pouvez également être plus précis et utiliser **InstanceName = _ 'Total'** dans la requête de hello, qui est un compteur de performance Windows. Vous pouvez également sélectionner une facette et une autre valeur **field:value**. Hello filtre est automatiquement ajouté tooyour filtre dans la barre de requête hello. Vous pouvez le voir dans hello suivant l’image. Il vous montre où tooclick tooadd **InstanceName : '_Total'** requête toohello sans avoir à taper quoi que ce soit.

![Recherche de facette](./media/log-analytics-log-searches/oms-search-facet.png)

Votre requête devient alors `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`

Dans cet exemple, vous n’avez pas toospecify **Type = Perf** tooget toothis résultat. Étant donné que hello champs CounterName et InstanceName existent uniquement pour les enregistrements de Type = Perf, requête de hello est suffisamment spécifique tooreturn hello mêmes résultats que hello une plus longue, précédente :

```
CounterName="% Processor Time" InstanceName="_Total"
```

C’est parce que tous les filtres de hello dans la requête de hello sont évalués comme étant dans *AND* entre eux. En réalité, hello plusieurs champs que vous ajoutez toohello critères, moins vous obtenez des résultats plus spécifiques et affinés.

Par exemple, les requêtes hello `Type=Event EventLog="Windows PowerShell"` est identique trop`Type=Event AND EventLog="Windows PowerShell"`. Il retourne tous les événements qui ont été enregistrés dans et collectés à partir du journal des événements Windows PowerShell hello. Si vous ajoutez un filtre à plusieurs fois et en sélectionnant de manière répétée hello même facette, puis d’émettre hello est alors purement esthétique : il peut surcharger la barre de recherche hello, mais elle retourne toujours hello mêmes résultats, car l’opérateur AND implicite de hello est toujours.

Vous pouvez facilement inverser l’opérateur AND implicite de hello à l’aide d’un opérateur NOT explicite. Par exemple :

`Type:Event NOT(EventLog:"Windows PowerShell")`ou son équivalent `Type=Event EventLog!="Windows PowerShell"` retourne tous les événements de tous les autres journaux qui ne sont pas hello Windows PowerShell.

Vous pouvez également utiliser un autre opérateur booléen tel que « OR ». Renvoie les enregistrements pour le hello le journal des événements est une Application ou un système de requête de suivante de Hello.

```
EventLog=Application OR EventLog=System
```

À l’aide de hello au-dessus de requête, vous obtiendrez les entrées pour les journaux Bonjour même jeu de résultats.

Toutefois, si vous supprimez hello ou en le laissant hello implicite AND en place, puis hello requête suivante ne produira pas de résultats, car il n’est pas une entrée de journal des événements qui appartient tooBOTH journaux. Chaque entrée de journal des événements a été écrite tooonly un des deux journaux de hello.

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a>Utilisation de filtres supplémentaires
Hello requête suivante retourne les entrées pour les journaux d’événements 2 pour tous les ordinateurs hello qui ont envoyé des données.

```
EventLog=Application OR EventLog=System
```

![Recherche de résultats](./media/log-analytics-log-searches/oms-search-results03.png)

La sélection d’un des champs de hello ou des filtres restreindra hello requête tooa ordinateur spécifique, en excluant tous les autres. requête obtenue de Hello peut se présenter comme suit de hello.

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

Qui est équivalent toohello suivantes, en raison de hello opérateur and implicite.

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

Chaque requête est évaluée dans hello suivant l’ordre explicite. Parenthèse de hello Remarque.

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

Comme champ hello du journal des événements, vous pouvez récupérer des données uniquement pour un ensemble d’ordinateurs spécifiques en ajoutant ou. Par exemple :

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

De même, cette hello après le retour de la requête **% temps processeur** pour hello sélectionné uniquement de deux ordinateurs.

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a>Types de champ
Lors de la création de filtres, vous devez comprendre les différences de hello à l’utilisation des différents types de champs retournés par les recherches de journal.

Les **champs interrogeables** s’affichent en bleu dans les résultats de la recherche.  Vous pouvez utiliser les champs de recherche dans le champ de toohello spécifique de conditions de recherche tels que les suivants hello :

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

Les **champs interrogeables en texte libre** s’affichent en gris dans les résultats de la recherche.  Ils ne peuvent pas être utilisés avec le champ de toohello spécifique de conditions de recherche telles que des champs de recherche.  Recherche uniquement lors d’une requête pour tous les champs tels que les suivants hello.

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a>Opérateurs booléens
Avec les champs numériques et DateHeure, vous pouvez rechercher des valeurs à l’aide d’opérateurs *supérieur à*, *inférieur à* et *inférieur ou égal à*. Vous pouvez utiliser des opérateurs simples tels que >, <>, =, < =, ! = dans la barre de recherche de requête hello.

Vous pouvez interroger un journal des événements spécifique pour une période spécifique. Par exemple, hello des dernières 24 heures est exprimé par hello expression mnémonique suivante.

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a>toosearch à l’aide d’un opérateur booléen
* Dans le champ de requête de recherche hello, tapez`EventLog=System TimeGenerated>NOW-24HOURS`  
    ![Recherche avec des opérateurs boléens](./media/log-analytics-log-searches/oms-search-boolean.png)

Vous pouvez contrôler hello intervalle de temps sous forme graphique et la plupart du temps, vous pourriez toodo que, il n’y avantages tooincluding un filtre de temps directement dans la requête de hello. Par exemple, cela fonctionne très bien avec les tableaux de bord où vous pouvez remplacer le temps de hello pour chaque vignette, quel que soit hello *global* sélecteur d’heure sur la page du tableau de bord hello. Pour plus d'informations, consultez [Questions relatives au temps dans le tableau de bord](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).

Lorsque le filtrage par heure, gardez à l’esprit que vous obtenez des résultats pour hello *intersection* Hello deux périodes : celle spécifiée dans le portail OMS (S1) est hello hello et hello celui spécifié dans la requête de hello (S2).

![intersection](./media/log-analytics-log-searches/oms-search-intersection.png)

Cela signifie que, si hello deux périodes ne se chevauchent, par exemple dans le portail OMS de hello où vous choisissez **cette semaine** et dans la requête hello où vous définissez **semaine dernière**, il n’existe aucune intersection et vous ne serez pas réception des résultats.

Opérateurs de comparaison utilisés pour le champ TimeGenerated de hello sont également utiles dans d’autres situations. Par exemple, avec des champs numériques.

Par exemple, étant donné que les alertes d’évaluation de la Configuration ont hello des valeurs de gravité suivantes :

* 0 = Information
* 1 = Avertissement
* 2 = Critique

Vous pouvez interroger pour les alertes d’avertissement et critiques et exclure également les alertes d’information avec hello suivant la requête :

```
Type=ConfigurationAlert  Severity>=1
```


Vous pouvez aussi utiliser des requêtes de plage de données. Cela signifie que vous pouvez fournir la plage de début et de fin de hello de valeurs dans une séquence. Par exemple, si vous souhaitez que les événements du journal des événements Operations Manager hello où hello EventID est too2100 supérieur ou égal mais non supérieur à 2199, puis hello suivant la requête va alors les retourner.

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> syntaxe de plage de Hello vous devez utiliser est le séparateur field : value de deux-points ( :)) hello et *pas* hello égal signe (=). Placez l’extrémité supérieure et inférieure de hello de plage de hello crochets et séparez-les par deux points (..).
>
>

## <a name="manipulate-search-results"></a>Manipulation des résultats de la recherche
Lorsque vous recherchez des données, vous souhaitez toorefine votre requête de recherche et avoir un bon niveau de contrôle sur les résultats hello. Lorsque les résultats sont récupérés, vous pouvez appliquer des commandes tootransform les.

Commandes dans les recherches de journal Analytique *doit* suivre après hello barre verticale (|). Un filtre doit toujours être la première partie de hello de chaîne de requête. Il définit le jeu de données hello avec lequel vous travaillez et « dirige ensuite « ces résultats dans une ligne de commande. Vous pouvez ensuite utiliser des commandes supplémentaires hello canal tooadd. Il s’agit de pipeline de Windows PowerShell toohello relativement similaire.

En règle générale, hello langage de recherche Analytique de journal tente de toomake de style et les instructions de PowerShell toofollow toohello similaire d’informatique informatique les avantages et courbe d’apprentissage tooease hello.

Le nom des commandes est un verbe, ce qui vous permet de connaître facilement leur fonction.  

### <a name="sort"></a>Trier
commande de tri Hello vous permet de hello toodefine ordre par un ou plusieurs champs de tri. Même si vous ne l'utilisez pas, un ordre de temps décroissant est appliqué par défaut. les résultats les plus récents Hello sont toujours en haut de hello des résultats de recherche. Cela signifie que lorsque vous exécutez une recherche avec `Type=Event EventID=1234` , ce qui est réellement exécuté pour vous est :

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

C'est-à-dire, car il est de type hello d’expérience que vous connaissez avec les journaux. Par exemple, dans hello Observateur d’événements Windows.

Vous pouvez utiliser le tri toochange hello moyen résultats sont retournés. Hello exemples suivants montrent comment cela fonctionne.

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


Hello simples exemples ci-dessus vous montrent comment des commandes : elles modifient forme hello de résultats hello hello filtre retourné.

### <a name="limit-and-top"></a>Limit et Top
Une autre commande moins connue est LIMIT. Limit est un verbe similaire à PowerShell. Limite est de commande TOP toohello fonctionnellement identique. Hello requêtes suivantes retournent hello mêmes résultats.

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a>toosearch à l’aide de top
* Dans le champ de requête de recherche hello, tapez`Type=Event EventID=600 | Top 1`   
    ![Recherche top](./media/log-analytics-log-searches/oms-search-top.png)

Dans l’image hello ci-dessus, il existe 358 mille enregistrements avec EventID = 600. Hello des champs, les facettes et les filtres sur hello gauche toujours des informations sur les résultats de hello *par partie du filtre hello* de requête de hello, qui fait partie de hello avant une barre verticale. Hello **résultats** volet retourne uniquement le résultat de hello 1 plus récente, parce que l’exemple de commande hello a formé et transformé les résultats hello.

### <a name="select"></a>Sélectionnez
commande SELECT Hello se comporte comme Select-Object dans PowerShell. Elle retourne des résultats filtrés qui n'ont pas toutes leurs propriétés d'origine. Au lieu de cela, elle sélectionne uniquement les propriétés de hello que vous spécifiez.

#### <a name="toorun-a-search-using-hello-select-command"></a>toorun une recherche à l’aide de la commande select hello
1. Dans Rechercher, tapez `Type=Event` puis cliquez sur **Rechercher**.
2. Cliquez sur **+ afficher plus** dans un des tooview de résultats hello toutes les propriétés de hello qui hello des résultats.
3. Sélectionnez certains d'entre eux explicitement et hello modifications de la requête trop`Type=Event | Select Computer,EventID,RenderedDescription`.  
    ![Recherche select](./media/log-analytics-log-searches/oms-search-select.png)

Cette commande est particulièrement utile lorsque vous souhaitez que les résultats de recherche toocontrol et choisissez uniquement les parties de hello des données qui importent vraiment pour votre exploration et qui n’est pas souvent d’enregistrement complet de hello. Elle est également utile lorsque des enregistrements de différents types présentent *certaines* propriétés communes, mais que leurs propriétés ne sont pas *toutes* communes. Base de données, vous pouvez générer des résultats qui ressemblent plus naturellement à une table ou fonctionnent bien lorsqu’exporté tooa un fichier CSV puis envoyés dans Excel.

## <a name="use-hello-measure-command"></a>Utilisez la commande de mesure hello
MESURE est une des commandes plus polyvalentes hello dans les recherches de journal Analytique. Il vous permet de tooapply statistique *fonctions* tooyour données et agréger les résultats sont regroupés par champ donné. Il existe plusieurs fonctions statistiques qui prennent en charge Measure.

### <a name="measure-count"></a>La fonction count() de Measure
Hello la première fonction statistique toowork, avec un des toounderstand la plus simple de hello est donc hello *count()* (fonction).

Les résultats d’une requête de recherche telle que `Type=Event`, affichent des filtres, également appelés facettes, sur hello gauche des résultats de recherche. Hello filtres montrent une distribution de valeurs pour les résultats hello un champ donné dans hello recherche exécutée.

![Recherche measure count](./media/log-analytics-log-searches/oms-search-measure-count01.png)

Par exemple, Bonjour image ci-dessus, vous verrez hello **ordinateur** champ qui montre que dans les événements de presque 739 mille hello dans les résultats de hello, sont des valeurs uniques et distinctes 68 pour hello **ordinateur** champ dans ces enregistrements. vignette de Hello affiche uniquement hello top 5, qui sont hello 5 valeurs les plus courantes écrites dans hello **ordinateur** champs), triées par nombre hello de documents contenant cette valeur spécifique dans ce champ. Dans l’image de hello vous pouvez voir que, parmi ces événements presque 369 mille, 90 mille proviennent hello OpsInsights04.contoso.com ordinateur, des milliers de 83 à partir de l’ordinateur de DB03.contoso.com hello et ainsi de suite.

Que se passe-t-il si vous souhaitez toosee toutes les valeurs, étant donné que les mosaïques hello montre uniquement hello uniquement les 5 premières ?

Qui est quelle mesure hello commande permet de faire avec la fonction count() de hello. Cette fonction n'utilise aucun paramètre. Vous spécifiez simplement le champ hello en fonction duquel vous voulez toogroup par : hello **ordinateur** champ dans ce cas :

`Type=Event | Measure count() by Computer`

![Recherche measure count](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

Le champ **Computer** est toutefois simplement un champ utilisé *dans* chaque élément de données : aucune base de données relationnelle n’est impliquée, et il n’existe aucun objet **Computer**distinct nulle part. Hello simplement les valeurs *dans* hello données peuvent décrire quelle entité a générées, ainsi que plusieurs autres caractéristiques et aspects des données de hello : hello donc terme *facette*. Toutefois, vous pouvez également les regrouper par d'autres champs. Étant donné que les résultats d’origine de hello de presque 739 milliers d’événements transmis dans la commande de mesure hello ont également un champ appelé **EventID**, vous pouvez appliquer hello même toogroup technique par ce champ et obtenir le nombre d’événements par ID d’événement :

```
Type=Event | Measure count() by EventID
```

Si vous n’êtes pas intéressé par nombre d’enregistrements réels hello qui contiennent une valeur spécifique, mais à la place si vous souhaitez seulement une liste de hello valeurs elles-mêmes, vous pouvez ajouter un *sélectionnez* à la fin de hello d’elle et sélectionnez simplement hello première colonne :

```
Type=Event | Measure count() by EventID | Select EventID
```

Puis vous pouvez obtenir plus complexes et des résultats de tri hello dans requête de hello, ou vous pouvez aussi simplement cliquer sur les colonnes dans la grille de hello, hello.

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a>toosearch à l’aide de la mesure nombre
* Dans le champ de requête de recherche hello, tapez`Type=Event | Measure count() by EventID`
* Ajouter `| Select EventID` fin toohello de requête de hello.
* Enfin, ajoutez `| Sort EventID asc` fin toohello de requête de hello.

Il existe quelques points importants toonotice et mettre en évidence :

Tout d’abord, les résultats hello que vous voyez ne sont pas résultats bruts d’origine de hello plus. Il s’agit en fait de résultats agrégés : autrement dit, des groupes de résultats. Ce n’est pas un problème, mais vous devez comprendre que vous interagissez avec une toute autre forme de données qui diffère de hello forme brute d’origine créée en volée hello en raison de la fonction d’agrégation ou statistique est utilisée hello.

Ensuite, **mesurer le nombre** actuellement retourne hello uniquement les premiers résultats distincts 100. Cette limite ne s’applique pas toohello autres fonctions statistiques. Par conséquent, vous devez généralement toouse un toosearch premier filtre plus précis pour des éléments spécifiques avant d’appliquer measure count().

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a>Utilisez les fonctions min et max hello avec la commande de mesure hello
Il existe plusieurs situations où les commandes **Measure Max()** et **Measure Min()** sont utiles. Toutefois, étant donné que chaque fonction est l'opposé de l'autre, nous démontrerons la fonction Max() et vous pourrez ensuite tester vous-même la fonction Min().

Si vous interrogez des événements de sécurité, ceux-ci ont une propriété **Level** qui peut varier. Par exemple :

```
Type=SecurityEvent
```

![Recherche du début de la fonction measure count](./media/log-analytics-log-searches/oms-search-measure-max01.png)

Si vous souhaitez que la valeur plus élevée tooview hello pour tous les de sécurité de hello événements à un même ordinateur, groupe hello par champ, vous pouvez utiliser

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![Recherche l’ordinateur de la fonction measure max](./media/log-analytics-log-searches/oms-search-measure-max02.png)

Il affichera que pour les ordinateurs hello ayant **niveau** enregistrements, la plupart d'entre eux ont au moins 8, le niveau nombreuses avaient un niveau de 16.

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![Recherche l’ordinateur qui génère la valeur horaire measure max](./media/log-analytics-log-searches/oms-search-measure-max03.png)

Cette fonction fonctionne bien avec les nombres, mais elle fonctionne également avec les champs DateHeure. C’est le dernier toocheck utile pour hello ou plus récent horodatage pour tout type de données indexé pour chaque ordinateur. Par exemple : lorsque l’événement sécurité hello plus récent a été signalée pour chaque machine ?

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a>Utilisez avg, fonction hello avec la commande de mesure hello
Hello fonction statistique Avg() utilisée avec measure vous permet de valeur moyenne de toocalculate hello pour un champ et groupe les résultats par hello même ou un autre champ. Cela est utile dans de nombreux cas, pour les données de performances par exemple.

Nous allons commencer par les données de performances. Remarque : OMS collecte actuellement les compteurs de performance pour les ordinateurs Windows et Linux.

toosearch pour *tous les* est de requête la plus simple hello des données de performances :

```
Type=Perf
```

![Recherche du début de la fonction avg](./media/log-analytics-log-searches/oms-search-avg01.png)

Hello première chose que vous remarquerez est qu’Analytique de journal vous montre trois perspectives : liste, qui vous montre ce qui montre les enregistrements réels hello derrière les graphiques hello ; Table, qui affiche une vue tabulaire des données de compteur de performance ; et les mesures, qui affiche des compteurs de performance de graphiques pour hello.

Dans l’image hello ci-dessus, il existe deux ensembles de champs marqués qui indiquent les éléments suivants de hello :

* Hello premier jeu identifie le nom de compteur de Performance Windows, nom de l’objet et nom de l’Instance dans le filtre de requête hello. Il s’agit des champs hello que vous utiliserez probablement le plus souvent en tant que facettes ou filtres.
* **CounterValue** est hello la valeur réelle du compteur de hello. Dans cet exemple, la valeur de hello est *75*.
* **TimeGenerated** a la valeur 12:51, au format 24 heures.

Voici une vue des mesures hello dans un graphique.

![Recherche du début de la fonction avg](./media/log-analytics-log-searches/oms-search-avg02.png)

Après la lecture sur la forme d’enregistrement hello des performances et après avoir lu sur d’autres techniques de recherche, vous pouvez utiliser measure Avg() tooaggregate ce type de données numériques.

Voici un exemple simple :

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![Recherche de l’exemple de valeur de la fonction avg](./media/log-analytics-log-searches/oms-search-avg03.png)

Dans cet exemple, vous sélectionnez le compteur de performance du temps processeur Total hello et moyenne par ordinateur. Si vous souhaitez toonarrow vers le bas votre hello tooonly de résultats 6 dernières heures, vous pouvez utiliser le contrôle de filtre de temps hello ou spécifiez dans votre requête, comme suit :

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a>toosearch à l’aide de la fonction avg de hello avec la commande de mesure hello
* Dans la zone de requête de recherche hello, tapez `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.

Vous pouvez agréger et corréler les données *entre* plusieurs ordinateurs. Par exemple, imaginez que vous avez un ensemble d’ordinateurs hôtes dans une sorte de batterie de serveurs où chaque nœud est égal tooany autre et il suffit de faire hello tous les même type de travail et le chargement doit être à peu près équilibrée. Vous pouvez obtenir leurs compteurs qu'en une seule fois par hello suivante, interroge et obtenir des moyennes pour l’ensemble de la batterie hello. Vous pouvez commencer en choisissant les ordinateurs hello avec hello l’exemple suivant :

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Maintenant que vous avez des ordinateurs de hello, vous ne devez que tooselect deux indicateurs de performance clés (KPI) : l’utilisation du processeur et % d’espace disque libre. Par conséquent, cette partie de hello requête devient :

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

Vous pouvez maintenant ajouter les compteurs et les ordinateurs avec hello l’exemple suivant :

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Étant donné que vous avez une sélection très spécifique, hello **mesurer Avg()** commande peut retourner hello moyenne non par ordinateur, mais dans la batterie de serveurs hello, simplement en effectuant un regroupement par CounterName. Par exemple :

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

Cela vous donne une vue compacte utile de quelques indicateurs de performance clés de votre environnement.

![Recherche du groupement de la fonction avg](./media/log-analytics-log-searches/oms-search-avg04.png)

Vous pouvez facilement utiliser la requête de recherche hello dans un tableau de bord. Par exemple, vous Impossible d’enregistrer la requête de recherche hello et créer un tableau de bord à partir de celui-ci nommé *KPI de batterie de serveurs Web*. toolearn plus sur l’utilisation de tableaux de bord, consultez [créer un tableau de bord personnalisé dans le journal Analytique](log-analytics-dashboards.md).

![Tableau de bord de recherche avg](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a>Utilisez la fonction sum hello avec la commande de mesure hello
la fonction sum Hello est fonctions tooother similaires de la commande de mesure hello. Vous pouvez voir un exemple sur la façon dont toouse hello fonction sum dans [recherche de journaux IIS W3C dans Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).

Vous pouvez utiliser les fonctions Max() et Min() avec des chaînes de nombres, de dates et heures, et de texte. Avec des chaînes de texte, elles sont triées par ordre alphabétique et vous pouvez obtenir la première et la dernière.

Toutefois, vous ne pouvez pas utiliser Sum() uniquement avec des champs numériques. Cela s’applique également tooAvg().

### <a name="use-hello-percentile-function-with-hello-measure-command"></a>Utilisez la fonction de centile de hello avec la commande de mesure hello
fonction de centile Hello est similaire tooAvg() et Sum() dans que vous pouvez l’utiliser uniquement pour les champs numériques. Vous pouvez utiliser n’importe quel centile entre 1 too99 sur un champ numérique. Vous pouvez également utiliser les deux commandes **percentile** et **pct**. Voici quelques exemples :  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a>Utiliser des commandes hello
Hello où commande fonctionne comme un filtre, mais elle peut être appliquée dans le filtre de hello pipeline toofurther agrégées des résultats qui ont été produits par une commande Measure – en tant que résultats tooraw opposés qui sont filtrés au début de hello d’une requête.

Par exemple :

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

Vous pouvez ajouter une autre barre verticale « | » caractères et hello où commande tooonly obtenir les ordinateurs dont l’UC moyenne est supérieure à 80 %, avec hello selon exemple :

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

Si vous êtes familiarisé avec Microsoft System Center - Operations Manager, vous pouvez considérer hello où command pack d’administration. Si hello exemple était une règle, hello première partie de la requête de hello serait hello et la source de données hello où commande serait la détection de condition hello.

Vous pouvez utiliser la requête de hello sous forme de vignette dans **mon tableau de bord**, comme un moniteur de tri, toosee lorsque les processeurs d’ordinateur sont surexploités. toolearn savoir plus sur les tableaux de bord, consultez [créer un tableau de bord personnalisé dans le journal Analytique](log-analytics-dashboards.md). Vous pouvez également créer et utiliser des tableaux de bord à l’aide d’application mobile hello. Pour plus d’informations, voir [Applications mobiles OMS](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865). Dans hello bas des deux vignettes de hello suivant l’image, vous pouvez voir le moniteur de hello a affiché une liste et un nombre. Fondamentalement, vous souhaitez hello, toobe nombre zéro et toujours hello toobe liste vide. Dans le cas contraire, il indique une condition d'alerte. Si nécessaire, vous pouvez l’utiliser tootake examiner quels ordinateurs sont sous pression.

![Tableau de bord mobile](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a>Utilisez hello in, opérateur
Hello *IN* (opérateur), avec *NOT IN* vous permet de toouse sous-recherches, c'est-à-dire des recherches qui incluent une autre recherche en tant qu’argument. Elles sont contenues entre accolades {} à l’intérieur d’une autre recherche *principale* ou *externe*. Hello résultat d’une sous-recherche, souvent une liste de résultats distincts est ensuite utilisé en tant qu’argument dans sa recherche principale.

Vous pouvez utiliser des sous-recherches toomatch des sous-ensembles de vos données que vous ne pouvez pas décrire directement dans une expression de recherche, mais qui peut être généré à partir d’une recherche. Par exemple, si vous voulez intéressez à l’aide d’une recherche toofind tous les événements à partir de *ordinateurs mises à jour de sécurité manquantes*, vous devez toodesign une sous-recherche qui identifie d’abord *ordinateurs mises à jour de sécurité manquantes*  avant de rechercher les événements appartenant toothose hôtes.

Ainsi, vous pouvez représenter *ordinateurs auxquels il manque requis des mises à jour de sécurité* avec hello suivant la requête :

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![Exemple de recherche avec l’opérateur IN](./media/log-analytics-log-searches/oms-search-in01-revised.png)

Une fois que vous avez hello liste, vous pouvez utiliser hello recherche comme une liste de hello toofeed recherche interne des ordinateurs d’une recherche externe (principale) qui recherche les événements liés à ces ordinateurs. Pour cela, vous devez hello, recherche interne entre accolades et alimentez ses résultats sous forme de valeurs possibles pour un filtre/champ de recherche externe à hello à l’aide d’opérateur de hello dans. Hello requête ressemble à :

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![Exemple de recherche avec l’opérateur IN](./media/log-analytics-log-searches/oms-search-in02-revised.png)

Temps de hello avis filtre utilisé dans la recherche interne de hello car hello évaluation des mises à jour du système prend également un instantané de tous les ordinateurs toutes les 24 heures. Faire en requête interne de hello plus léger et plus précise par recherche uniquement sur une journée. recherche externe de Hello utilise à la place sélection de temps hello dans l’interface utilisateur hello, récupérer les événements à partir de hello ces 7 derniers jours. Consultez la page [Opérateurs booléens](#boolean-operators) pour plus d’informations sur les opérateurs de temps.

Étant donné que vous vraiment à peine hello utiliser les résultats de recherche interne de hello comme valeur de filtre pour hello externe, vous pouvez toujours appliquer des commandes de recherche externe de hello. Par exemple, vous pouvez toujours hello groupe au-dessus événements avec une autre commande measure :

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![Exemple de recherche avec l’opérateur IN](./media/log-analytics-log-searches/oms-search-in03-revised.png)

En règle générale, vous souhaitez tooexecute de votre requête interne rapidement car Analytique de journal a des délais d’expiration côté service pour et également tooreturn une petite quantité de résultats. Si la requête interne de hello retourne plus de résultats, la liste des résultats hello est tronquée, ce qui peut amener hello recherche externe tooreturn des résultats incorrects.

Une autre règle est que la recherche interne hello doit tooprovide *agrégées* résultats. En d’autres termes, elle doit contenir une commande *measure* ; vous ne pouvez pour le moment pas alimenter les résultats bruts dans une recherche externe.

En outre, il peut y avoir qu’un seul opérateur IN, et il doit être hello dernier filtre de requête de hello. Plusieurs opérateurs IN ne peut pas être, ou cela essentiellement d’empêcher l’exécution de plusieurs sous-recherches : hello important point est que seule sub/recherche interne est possible pour chaque recherche externe.

Même avec ces limites, permet de nombreux types de recherche en corrélation et vous permet de toodefine toogroups quelque chose de similaire tels que les ordinateurs, les utilisateurs ou les fichiers, les champs hello dans vos données contiennent des. Voici des exemples supplémentaires :

**Toutes les mises à jour manquantes sur des ordinateurs sur lesquels le paramètre de mise à jour automatique est désactivé**

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

**Tous les événements d’erreur sur des ordinateurs exécutant SQL Server (où l’évaluation de SQL a été exécutée)**

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

**Tous les événements de sécurité des ordinateurs qui sont des contrôleurs de domaine (où l’évaluation d’Active Directory a été exécutée)**

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

**Qui autres comptes ont ouvert une session toohello mêmes ordinateurs où le compte BACONLAND\jochan a ouvert une session ?**

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a>Utilisez la commande distinctes hello
Comme le suggère le nom hello, cette commande fournit une liste de valeurs distinctes d’un champ. Son utilisation est étonnamment simple mais cette commande s’avère très utile. Hello que même résultat peut être obtenu avec la commande measure count() également, comme indiqué ci-dessous.

```
Type=Event | Measure count() by Computer
```

![Exemple de commande de recherche DISTINCT](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

Toutefois, si vous êtes intéressé il suffit qu’une liste de valeurs distinctes et non par nombre de documents qui ont des valeurs qui hello, puis DISTINCT peut fournir tooread plus claire et plus facile de sortie et une syntaxe plus courte, comme indiqué ci-dessous.

```
Type=Event | Distinct Computer
```
![Exemple de commande de recherche DISTINCT](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a>Utiliser la fonction countdistinct de hello avec la commande de mesure hello
fonction countdistinct de Hello de hello nombre de valeurs distinctes dans chaque groupe. Par exemple, il peut être utilisé numéro de hello toocount d’ordinateurs uniques pour chaque Type de création de rapports :

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a>Utiliser la commande d’intervalle hello measure
Grâce à la récupération des données de performance en quasi-temps réel, vous pouvez récupérer et visualiser des compteurs de performance dans Log Analytics. Requête de hello simplement entrer **Type : Perf** retournera des milliers de graphiques de métriques en fonction du nombre de hello des compteurs et les serveurs dans votre environnement Analytique de journal. Avec l’agrégation de mesure à la demande, vous pouvez examiner hello métriques globale dans votre environnement à un niveau élevé et une connaissance approfondie des données plus granulaires que nécessaire pour.

Supposons que vous voulez tooknow hello moyenne du processeur sur tous vos ordinateurs. Examinant hello des UC moyenne pour tous les ordinateurs ne serait pas utile, car les résultats peuvent obtenir nivelés. toolook en plus de détails, vous pouvez regrouper vos résultats fois plus petits segments de la fenêtre, puis ouvrez dans une série chronologique dans différentes dimensions. Par exemple, vous pouvez effectuer moyenne de toutes les heures hello d’utilisation du processeur sur tous vos ordinateurs comme suit :

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![intervalle moyen de mesure](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

Par défaut, ces résultats s’affichent dans un graphique interactif en courbes contenant plusieurs séries.  Ce graphique prend en charge le basculement entre séries (avec la remise à l’échelle de l’axe y), le zoom et le survol.  option d’affichage de tableau de Hello est toujours disponible pour l’affichage des données brutes de hello si nécessaire.

Vous pouvez également effectuer des regroupements sur d’autres champs. Dans cet exemple, je regarde tous les compteurs de % hello pour un ordinateur spécifique et vous voulez tooknow Nouveautés de centiles de toutes les heures 70 hello de chaque compteur :

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
Une chose toonote est que ces requêtes ne sont pas limités tooperformance compteurs. Vous pouvez les appliquer tooany métrique. Dans cet exemple, j’examine les journaux IIS W3C. Je veux tooknow quel est le temps maximal de hello que nécessaire sur un intervalle de 5 minutes pour le traitement de chaque demande :

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a>Utilisation de plusieurs agrégats dans une même requête
Vous pouvez spécifier plusieurs clauses d’agrégation dans une commande measure.  Un alias indépendant peut être attribué à chacune d’entre elles.  Si elle n’est pas fourni un hello alias qui résulte nom de champ sera fonction d’agrégation hello qui a été utilisée (par exemple, « avg(CounterValue) » pour avg(CounterValue)).

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

Voici un autre exemple :

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les recherches de journal, consultez les ressources suivantes :

* Utilisez [les champs personnalisés dans le journal Analytique](log-analytics-custom-fields.md) tooextend des recherches de journaux.
* Hello de révision [Analytique de journal journal référence de recherche](log-analytics-search-reference.md) tooview tous les Hello recherche des champs et facettes disponibles dans le journal Analytique.
