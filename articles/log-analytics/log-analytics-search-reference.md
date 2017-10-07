---
title: "référence de recherche Analytique de journal d’aaaAzure | Documents Microsoft"
description: "référence de recherche Analytique de journal Hello décrit le langage de recherche hello et fournit des options de syntaxe de requête générale hello que vous pouvez utiliser lorsque vous recherchez des données et le filtrage des expressions toohelp affiner votre recherche."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 402615a2-bed0-4831-ba69-53be49059718
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7478a1139b88a1ce76ebb7b76027a6ccd66f4f27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-search-reference"></a>Référence de recherche Log Analytics

>[!NOTE]
> Cet article décrit les recherches de journal à l’aide du langage de requête en cours hello dans Analytique de journal.  Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis vous devez faire référence trop[hello référence du langage pour le nouveau langage de hello](https://go.microsoft.com/fwlink/?linkid=856079).

Hello section de référence suivante sur le langage de recherche décrit les options de syntaxe de requête générale hello que vous pouvez utiliser lorsque vous recherchez des données et le filtrage des expressions toohelp affiner votre recherche. Il décrit également les commandes que vous pouvez utiliser l’action de tootake sur hello les données récupérées.

Vous pouvez lire sur les champs hello retournés dans les recherches et les facettes hello qui vous aident à en savoir plus sur les catégories de données, Bonjour similaires [section de référence de champ de recherche et de facette](#search-field-and-facet-reference).

## <a name="general-query-syntax"></a>Syntaxe de requête générale
syntaxe de Hello pour l’interrogation générale est la suivante :

```
filterExpression | command1 | command2 …
```

expression de filtre de Hello (`filterExpression`) définit hello « where » une condition pour hello la requête. commandes Hello s’appliquent toohello les résultats retournés par la requête de hello. Plusieurs commandes doivent être séparés par une barre verticale hello (|).

### <a name="general-syntax-examples"></a>Exemples de syntaxe générale
Exemples :

```
system
```

Cette requête retourne des résultats qui contiennent les mot hello *système* dans un champ qui a été indexé pour la recherche en texte intégral ou de conditions de recherche.

> [!NOTE]
> Tous les champs sont indexés de cette façon, mais sont de hello plus courante des champs texte (par exemple, les noms et les descriptions) généralement.
>
>

```
system error
```

Cette requête renvoie les résultats qui contiennent les mots hello *système* et *erreur*.

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

Cette requête renvoie les résultats qui contiennent les mots hello *système* et *erreur*. Elle trie ensuite les résultats de hello en hello *ManagementGroupName* champ (dans l’ordre croissant), puis par hello *TimeGenerated* champ (dans l’ordre décroissant). Il prend uniquement hello 10 premiers résultats.

> [!IMPORTANT]
> Tous les hello des noms de champs et valeurs hello pour les champs de texte et la chaîne hello respectent la casse.
>
>

## <a name="filter-expressions"></a>Expressions de filtre
Hello suivant sous-sections explique les expressions de filtre hello.

### <a name="string-literals"></a>Littéraux de chaîne
Un littéral de chaîne est une chaîne qui n’est pas reconnue par l’Analyseur de hello comme un mot clé ou un type de données prédéfini (par exemple, un nombre ou une date).

Exemples :

```
These all are string literals
```

Cette requête recherche des résultats qui contiennent les occurrences des cinq mots. tooperform une recherche de chaîne complexe, placez hello littéral de chaîne dans des guillemets doubles. Par exemple :

```
"Windows Server"
```

Cela renvoie uniquement les résultats avec des correspondances exactes pour *Windows Server*.

### <a name="numbers"></a>Nombres
Analyseur de Hello prend en charge le nombre entier décimal hello et syntaxe de nombre à virgule flottante pour les champs numériques.

Exemples :

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a>Dates et heures
Chaque élément de données dans le système de hello a un *TimeGenerated* propriété, qui représente la date d’origine de hello et l’heure d’enregistrement de hello. Certains types de données peuvent avoir davantage de champs Date/Heure (par exemple, *LastModified*).

Hello chronologie **graphique/heure** sélecteur dans Azure journal Analytique montre une répartition des résultats au fil du temps (en fonction toohello requête actuelle en cours d’exécution). Il est basé sur hello *TimeGenerated* champ. Les champs de date et l’heure ont un format de chaîne spécifique qui peut être utilisé dans les requêtes toorestrict hello requête tooa période particulière. Vous pouvez également utiliser la syntaxe toorefer toorelative intervalles de temps (par exemple, « entre il y a 3 jours et il y a 2 heures »).

les Voici Hello valides formes de syntaxe pour les dates et heures :

```
yyyy-mm-ddThh:mm:ss.dddZ
```

```
yyyy-mm-ddThh:mm:ss.ddd
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm
```

```
yyyy-mm-dd
```


Par exemple :

```
TimeGenerated:2013-10-01T12:20
```

commande précédente Hello retourne uniquement les enregistrements avec un *TimeGenerated* valeur exactement 12:20 le 1er octobre 2013.

Hello prend également en valeur Date/heure mnémonique hello maintenant. (Il est peu probable que cela génère des résultats, car les données ne traversent pas hello système si rapidement.)

Ces exemples sont des blocs de construction toouse de dates relatives et absolues. Dans hello trois sous-sections suivantes, vous verrez comment toouse les plus avancés filtres, avec des exemples qui utilisent des plages de dates relatives.

### <a name="datetime-math"></a>Mathématique de Date/Heure
Utilisez toooffset d’opérateurs mathématiques hello Date/heure ou arrondir la valeur de Date/heure hello, à l’aide de simples calculs de Date/heure.

Syntaxe :

```
datetime/unit
```

```
datetime[+|-]count unit
```

| Opérateur  | Description |
| --- | --- |
| / |Arrondit Date/heure toohello spécifié d’unité. Par exemple, désormais / DAY arrondit hello toomidnight de Date/heure actuelle de hello jour actuel. |
| + ou - |Les décalages de Date/heure par hello spécifié le nombre d’unités. Par exemple, NOW + 1HOUR décale hello actuel Date/heure en une heure en avant. 2013-10-01T12:00-10 jours décale la valeur de Date de hello 10 jours en arrière. |

Vous pouvez chaîner les opérateurs mathématiques Date/heure hello. Par exemple :

```
NOW+1HOUR-10MONTHS/MINUTE
```

Hello tableau suivant répertorie les unités de Date/heure hello pris en charge.

| Unité Date/Heure | Description |
| --- | --- |
| YEAR, YEARS |Arrondit toocurrent année ou les décalages de par Bonjour spécifié le nombre d’années. |
| MONTH, MONTHS |Arrondit toocurrent mois ou les décalages de par Bonjour nombre spécifié de mois. |
| DAY, DAYS, DATE |Jour de toocurrent essais de hello mois ou les décalages de par Bonjour spécifié le nombre de jours. |
| HOUR, HOURS |Arrondit toocurrent heure ou les décalages de par Bonjour spécifié le nombre d’heures. |
| MINUTE, MINUTES |Arrondit toocurrent minute ou les décalages de par Bonjour nombre spécifié de minutes. |
| SECOND, SECONDS |Arrondit la seconde toocurrent, ou décale hello spécifié nombre de secondes. |
| MILLISECOND, MILLISECONDS, MILLI, MILLIS |Millisecondes de toocurrent arrondit ou décalages par hello spécifié en millisecondes. |

### <a name="field-facets"></a>Facettes de champ
À l’aide de facettes de champ, vous pouvez spécifier la condition de recherche de hello pour des champs spécifiques et leurs valeurs exactes. Cela diffère de l’écriture de requêtes de « texte libre » pour différents termes dans l’index de hello. Vous avez déjà vu cette technique dans plusieurs des exemples précédents. Hello Voici des exemples plus complexes.

**Syntaxe**

```
field:value
```

```
field=value
```

**Description**

Recherches hello champ de valeur spécifique de hello. valeur de Hello peut être un littéral de chaîne, la numéro, ou la date et l’heure.

Par exemple :

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

**Syntaxe**

*champ&gt;valeur*

*champ&lt;valeur*

*champ&gt;=valeur*

*champ&lt;=valeur*

*champ!=valeur*

**Description**

Fournit des comparaisons.

Par exemple :

```
TimeGenerated>NOW+2HOURS
```

**Syntaxe**

```
field:[from..to]
```

**Description**

Fournit des facettes de plage.

Par exemple :

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a>IN
Hello **IN** (mot clé) vous permet de tooselect à partir d’une liste de valeurs. Selon la syntaxe hello que vous utilisez, cela peut être une simple liste de valeurs que vous fournissez, ou une liste de valeurs à partir d’une agrégation.

Syntaxe 1 :

```
field IN {value1,value2,value3,...}
```

Cette syntaxe vous permet de tooinclude toutes les valeurs dans une liste simple.



Exemples :

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

Syntaxe 2 :

```
(Outer query) (Field toouse with inner query results) IN {Inner query | measure count() by (Field toosend tooouter query)} (rest  of outer query)  
```

Cette syntaxe vous permet de toocreate une agrégation. Vous pouvez ensuite alimenter la liste des valeurs hello à partir de cette agrégation dans une autre recherche externe (principale) permettant de rechercher des événements avec cette valeur. Pour cela, vous devez hello, recherche interne entre accolades et alimentez ses résultats sous forme de valeurs possibles pour un champ de recherche externe de hello en utilisant l’opérateur IN de hello.

Exemple de requête interne : *ordinateurs auxquels il manque des mises à jour de sécurité* avec hello suivant la requête d’agrégation :

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

Hello dernière requête qui recherche *tous les événements de Windows pour les ordinateurs auxquels il manque des mises à jour de sécurité* similaire hello suivant :

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a>Contient
Hello **contient** (mot clé) vous permet de toofilter des enregistrements avec un champ qui contient une chaîne spécifiée. Il respecte la casse, fonctionne uniquement avec des champs de type chaîne et ne peut inclure de caractère d’échappement.

Syntaxe :

```
field:contains("string")
```

Exemple :

```
Type:contains("Event")
```

Cela retourne les enregistrements avec un type qui contient la chaîne de hello « Événement ». Les exemples incluent **Event**, **SecurityEvent** et **ServiceFabricOperationEvent**.



### <a name="regular-expressions"></a>Expressions régulières
Vous pouvez spécifier une condition de recherche pour un champ avec une expression régulière, à l’aide de hello **Regex** (mot clé). Pour obtenir une description complète de la syntaxe hello que vous pouvez utiliser dans les expressions régulières, consultez [à l’aide de recherches de journal toofilter des expressions régulières dans le journal Analytique](log-analytics-log-searches-regex.md).

Syntaxe :

```
field:Regex("Regular Expression")
```

Exemple :

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a>Opérateurs logiques
requête Hello langages prennent en charge les opérateurs logiques hello (*AND*, *ou*, et *pas*) et de leurs alias C-style (*&&*,  *||* , et *!*, respectivement). Vous pouvez utiliser des parenthèses toogroup ces opérateurs.

Exemples :

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

Vous pouvez omettre l’opérateur logique de hello pour les arguments de filtre de niveau supérieur hello. Dans ce cas, hello opérateur AND est supposé.

| Expression de filtre | Équivalent trop|
| --- | --- |
| erreur système |système AND erreur |
| système « Windows Server » OR Gravité:1 |système AND (« Windows Server » OR Gravité:1) |

### <a name="wildcarding"></a>Utilisation des caractères génériques
langage de requête Hello prend en charge à l’aide de hello ( \* ) caractères représentent trop un ou plusieurs caractères pour une valeur dans une requête.

Exemple :

 Rechercher tous les ordinateurs par « SQL » nom hello, tels que « Redmond-SQL ».

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> Pour l’instant, les caractères génériques ne peuvent pas être utilisés entre guillemets. Par exemple, message de type hello `"*This text*"` considère hello (\*) utilisé comme littéral (\*) caractères.


## <a name="commands"></a>Commandes


commandes Hello s’appliquent toohello les résultats retournés par la requête de hello. Utilisez hello canal caractère (|) tooapply un toohello de commande récupérer les résultats. Plusieurs commandes doivent être séparés par une barre verticale hello.

> [!NOTE]
> Les noms de commande peuvent être écrits en majuscules ou minuscules, contrairement aux noms de champs hello et les données de salutation.
>
>

### <a name="sort"></a>Trier
Syntaxe :

    sort field1 asc|desc, field2 asc|desc, …

Trie les résultats de hello champs particuliers. résultats de hello Hello asc/desc suffixe toosort dans l’ordre croissant ou décroissant est facultative. S’il est omis, hello *asc* ordre de tri est supposé. Pourquoi **TimeGenerated** champ, *desc* est donné par ordre de tri, elle retourne les résultats les plus récents hello tout d’abord par défaut.

### <a name="toplimit"></a>Top/Limit
Syntaxe :

    top number


    limit number
Limites hello réponse toohello top N des résultats.

Exemple :

    Type:Alert errors detected | top 10

Retourne hello 10 premiers résultats correspondants.

### <a name="skip"></a>Skip
Syntaxe :

    skip number

Ignore la hello nombre de résultats répertoriés.

Exemple :

    Type:Alert errors detected | top 10 | skip 200

Retourne les 10 premiers résultats correspondants en commençant au résultat 200.

### <a name="select"></a>Sélectionnez
Syntaxe :

    select field1, field2, ...

Limite les champs de toohello de résultats que vous choisissez.

Exemple :

    Type:Alert errors detected | select Name, Severity

Limites hello des champs de résultats retournés trop*nom* et *gravité*.

### <a name="measure"></a>Measure
Hello *mesure* commande est les résultats de recherche bruts toohello tooapply utilisé des fonctions statistiques. Cela est très utile tooget *group by* vues sur les données de salutation. Lorsque vous utilisez la commande de mesure hello, la recherche de journal Analytique affiche une table avec des résultats agrégés.

**Syntaxe :**

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



Regroupe les résultats hello en *groupField*et calcule les valeurs de mesure hello agrégée à l’aide de *aggregatedField*.

| Fonction statistique de mesure | Description |
| --- | --- |
| *aggregateFunction* |nom de Hello de fonction d’agrégation hello (sensible à la casse). Hello suivant des fonctions d’agrégation est prises en charge : COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, centile ## ou PCT ## (## est un nombre compris entre 1 et 99). |
| *aggregatedField* |champ de Hello est en cours d’agrégation. Ce champ est facultatif pour hello fonction d’agrégation COUNT, mais a toobe un champ numérique existant pour SUM, MAX, MIN, AVG, STDDEV, centile ## ou PCT ## (## est un nombre compris entre 1 et 99). Hello aggregatedField peut également s’agir de hello **étendre** fonctions prises en charge. |
| *fieldAlias* |alias (facultatif) Hello hello calculée valeur agrégée. Si non spécifié, le nom du champ hello est **AggregatedValue**. |
| *groupField* |nom Hello du champ de hello du jeu de résultats de hello de regroupement. |
| *Intervalle* |intervalle de temps Hello, dans le format de hello :**Nnnnom**. **nnn**est un nombre entier positif de hello. **NOM** est le nom de l’intervalle hello. Les noms d’intervalle pris en charge sont sensibles à la casse et incluent : MILLISECOND[S], SECOND[S], MINUTE[S], HOUR[S], DAY[S], MONTH[S] et YEAR[S]. |

option d’intervalle Hello utilisable uniquement dans les champs de groupe Date/heure (tels que *TimeGenerated* et *TimeCreated*). Actuellement, il n’est pas appliquée par le service de hello, mais un champ sans la Date/heure qui est passé toohello back-end provoque une erreur d’exécution. Lors de la validation de schéma hello est implémenté, hello service API rejette les requêtes qui utilisent des champs sans la Date/heure pour l’agrégation d’intervalle. Hello actuel *mesure* implémentation prend en charge le regroupement de l’intervalle pour une fonction d’agrégation.

Si la clause de hello BY est omise, mais un intervalle est spécifié (comme seconde syntaxe), hello *TimeGenerated* champ est supposé par défaut.

Exemples :

**Exemple 1**

    Type:Alert | measure count() as Count by ObjectId

Groupes hello alertes par *ObjectID*et calcule le nombre de hello d’alertes pour chaque groupe. valeur d’agrégation Hello est retournée en tant que hello *nombre* champ (alias).

**Exemple 2**

    Type:Alert | measure count() interval 1HOUR

Groupes hello alertes par intervalles de 1 heure à l’aide de hello *TimeGenerated* champ et le numéro de hello retourne des alertes dans chaque intervalle.

**Exemple 3**

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

Comme hello l’exemple précédent, mais avec un alias de champ agrégé (*AlertsPerHour*).

**Exemple 4**

    * | measure count() by TimeCreated interval 5DAYS

Regroupe les résultats de hello par intervalles de 5 jours à l’aide de hello *TimeCreated* champ et le numéro de hello retourne des résultats dans chaque intervalle.

**Exemple 5**

    Type:Alert | measure max(Severity) by WorkflowName

Groupes hello alertes par nom de la charge de travail et retourne hello valeur de gravité d’alerte maximum pour chaque flux de travail.

**Exemple 6**

    Type:Alert | measure min(Severity) by WorkflowName

Comme hello l’exemple précédent, mais avec hello *min* fonction agrégée.

**Exemple 7**

    Type:Perf | measure avg(CounterValue) by Computer

Regroupe les performances par ordinateur et calcule la moyenne de hello (moyenne).

**Exemple 8**

    Type:Perf | measure sum(CounterValue) by Computer

Comme l’exemple précédent de hello, mais utilise *somme*.

**Exemple 9**

    Type:Perf | measure stddev(CounterValue) by Computer

Comme l’exemple précédent de hello, mais utilise *stddev*.

**Exemple 10**

    Type:Perf | measure percentile70(CounterValue) by Computer

Comme l’exemple précédent de hello, mais utilise *percentile70*.

**Exemple 11**

    Type:Perf | measure pct70(CounterValue) by Computer

Comme l’exemple précédent de hello, mais utilise *pct70*. Notez que *PCT##* est uniquement un alias de la fonction *PERCENTILE##*.

**Exemple 12**

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

Regroupe d’abord les performances par ordinateur, puis CounterName et calcule hello moyenne (moyenne).

**Exemple 13**

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

Obtient des premiers cinq flux de travail avec un nombre maximal d’alertes hello hello.

**Exemple 14**

    * | measure countdistinct(Computer) by Type

Hello nombre d’ordinateurs uniques pour chaque Type.

**Exemple 15**

    * | measure countdistinct(Computer) Interval 1HOUR

Hello nombre d’ordinateurs uniques pour toutes les heures.

**Exemple 16**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

% Temps processeur par ordinateur de groupe et renvoie la moyenne de hello pour toutes les heures.

**Exemple 17**

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

Groupe W3CIISLog par la méthode et retourne hello maximale pour toutes les 5 minutes.

**Exemple 18**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

Groupes % temps processeur par ordinateur et retourne hello minimum, moyenne, 75e centile et maximal pour toutes les heures.

**Exemple 19**

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

Groupes % temps processeur tout d’abord par ordinateur, puis par Instance nom et retourne hello minimum, moyenne, 75e centile et maximal pour toutes les heures.

**Exemple 20**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

Calcule le maximum de hello d’écritures sur disque par minute pour chaque disque sur votre ordinateur.

### <a name="where"></a>Where
Syntaxe :

```
**where** AggregatedValue>20
```

Peut être utilisée uniquement après un *mesure* commande hello de filtre toofurther agrégée des résultats que hello *mesure* fonction d’agrégation a généré.

Exemples :

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a>Dedup
Syntaxe :

    Dedup FieldName

Retourne hello premier document trouvé pour chaque valeur unique du champ de hello.

Exemple :

    Type=Event | Dedup EventID | sort TimeGenerated DESC

Cet exemple retourne un événement (événement de dernière hello) par ID d’événement.

### <a name="join"></a>Join
Jointures hello les résultats de deux requêtes tooform un seul jeu de résultats.  Prend en charge plusieurs types de jointures décrites dans hello suivre la table.

| Type de jointure | Description |
|:--|:--|
| interne | Renvoie uniquement les enregistrements comportant une valeur correspondante dans les deux requêtes. |
| externe | Renvoie tous les enregistrements des deux requêtes.  |
| gauche  | Renvoie tous les enregistrements de la requête de gauche et les enregistrements correspondants de la requête de droite. |


- Jointures ne prennent pas en charge les requêtes qui incluent hello **IN** (mot clé), hello **mesure** commande ou hello **étendre** commande si elle cible un champ de requête à droite de hello.
- Vous ne pouvez inclure qu’un seul champ dans une jointure.
- Une recherche unique ne doit pas comporter plus d’une jointure.

**Syntaxe**

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

**Exemples**

types de jointure différent tooillustrate hello, envisagez de rejoindre un type de données collectées à partir d’un journal personnalisé appelé MyBackup_CL pulsation de hello pour chaque ordinateur.  Ces types de données ont hello données suivantes.

`Type = MyBackup_CL`

| TimeGenerated | Ordinateur | LastBackupStatus |
|:---|:---|:---|
| 20/04/2017 01:26:32.137 | srv01.contoso.com | Succès |
| 20/04/2017 02:13:12.381 | srv02.contoso.com | Succès |
| 20/04/2017 02:13:12.381 | srv03.contoso.com | Échec |

`Type = Hearbeat` (un seul sous-ensemble de champs présenté)

| TimeGenerated | Ordinateur | ComputerIP |
|:---|:---|:---|
| 21/04/2017 12:01:34.482 | srv01.contoso.com | 10.10.100.1 |
| 21/04/2017 12:02:21.916 | srv02.contoso.com | 10.10.100.2 |
| 21/04/2017 12:01:47.373 | srv04.contoso.com | 10.10.100.4 |

#### <a name="inner-join"></a>jointure interne

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

Hello retourne les enregistrements suivants, où le champ de l’ordinateur hello correspond à pour les deux types de données.

| Ordinateur| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 20/04/2017 01:26:32.137 | Succès | 21/04/2017 12:01:34.482 | 10.10.100.1 | Heartbeat |
| srv02.contoso.com | 20/04/2017 02:13:12.381 | Succès | 21/04/2017 12:02:21.916 | 10.10.100.2 | Heartbeat |


#### <a name="outer-join"></a>jointure externe

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

Hello retourne les enregistrements pour les deux types de données suivants.

| Ordinateur| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 20/04/2017 01:26:32.137 | Succès  | 21/04/2017 12:01:34.482 | 10.10.100.1 | Heartbeat |
| srv02.contoso.com | 20/04/2017 14:14:12.381 | Succès  | 21/04/2017 12:02:21.916 | 10.10.100.2 | Heartbeat |
| srv03.contoso.com | 20/04/2017 01:33:35.974 | Échec  | 21/04/2017 12:01:47.373 | | |
| srv04.contoso.com |                           |          | 21/04/2017 12:01:47.373 | 10.10.100.2 | Heartbeat |



#### <a name="left-join"></a>jointure gauche

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

Retourne les enregistrements suivants MyBackup_CL avec tous les champs de correspondance à partir de la pulsation de hello.

| Ordinateur| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| srv01.contoso.com | 20/04/2017 01:26:32.137 | Succès | 21/04/2017 12:01:34.482 | 10.10.100.1 | Heartbeat |
| srv02.contoso.com | 20/04/2017 02:13:12.381 | Succès | 21/04/2017 12:02:21.916 | 10.10.100.2 | Heartbeat |
| srv03.contoso.com | 20/04/2017 02:13:12.381 | Échec | | | |


### <a name="extend"></a>Extend
Vous permet de toocreate les champs d’exécution dans les requêtes. Notez que les champs d’exécution ne peut pas être utilisés avec l’agrégation de tooperform commande hello mesure.

**Exemple 1**

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
Affiche le score de recommandation pondéré pour les recommandations d’évaluation SQL.

**Exemple 2**

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
Affiche la valeur de compteur en Ko au lieu d’octets.

**Exemple 3**

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
Échelles hello valeur de WireData TotalBytes, de telle sorte que tous les résultats sont compris entre 0 et 100.

**Exemple 4**

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
Les valeurs Tag Perf Counter inférieures à 50 % sont définies comme LOW, et les autres comme HIGH.

**Exemple 5**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
Calcule le maximum de hello d’écritures sur disque par minute pour chaque disque sur votre ordinateur.

**Fonctions prises en charge**

| Fonction | Description | Exemples de syntaxe |
| --- | --- | --- |
| abs |Retourne la valeur absolue hello Hello spécifié la valeur ou une fonction. |`abs(x)` <br> `abs(-5)` |
| acos |Retourne l’arc cosinus d’une valeur ou d’une fonction. |`acos(x)` |
| and |Retourne la valeur true si et seulement si tous les opérandes ont la tootrue. |`and(not(exists(popularity)),exists(price))` |
| asin |Retourne l’arc sinus d’une valeur ou d’une fonction. |`asin(x)` |
| atan |Retourne l’arc tangente d’une valeur ou d’une fonction. |`atan(x)` |
| atan2 |Retourne l’angle hello résultant de conversion hello des coordonnées rectangulaires de hello coordonnées x et y toopolar. |`atan2(x,y)` |
| cbrt |Racine cubique. |`cbrt(x)` |
| ceil |Arrondit tooan entier. |`ceil(x)`  <br> `ceil(5.6)` Retourne 6 |
| cos |Retourne le cosinus d’un angle. |`cos(x)` |
| cosh |Retourne le cosinus hyperbolique d’un angle. |`cosh(x)` |
| def |Abréviation de valeur par défaut. Retourne hello la valeur du champ « field ». Si le champ de hello n’existe pas, renvoie la valeur par défaut hello et génère hello première valeur où : `exists()==true`. |`def(rating,5)`. Cette fonction def() renvoie hello évaluation ou, si aucun classement n’est spécifié dans le document de hello, 5. <br> `def(myfield, 1.0)`est équivalent trop`if(exists(myfield),myfield,1.0)`. |
| deg |Convertit des radians toodegrees. |`deg(x)` |
| div |`div(x,y)` divise x par y. |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| dist |Retourne la distance hello entre deux vecteurs (points) dans un espace à n dimensions. Prend la puissance de hello, ainsi que les instances de ValueSource deux ou plus et calcule les distances hello entre deux vecteurs de hello. Chaque ValueSource doit être un nombre. Il doit être un nombre pair d’instances de ValueSource passées dans, et méthode hello part du principe que hello première moitié représente premier vecteur de hello et deuxième moitié de hello représente hello second vecteur. |`dist(2, x, y, 0, 0)`Calcule la distance EUCLIDIENNE hello entre (0,0) et (x, y) pour chaque document. <br> `dist(1, x, y, 0, 0)`Calcule la distance de Manhattan (taxi) hello entre (0,0) et (x, y) pour chaque document. <br> `dist(2,,x,y,z,0,0,0)` Calcule la distance euclidienne entre (0,0,0) et (x,y,z) pour chaque document.<br>`dist(1,x,y,z,e,f,g)` Calcule la distance de Manhattan entre (x,y,z) et (e,f,g), où chaque lettre est un nom de champ. |
| exists |Retourne TRUE si les membres du champ de hello existe. |`exists(author)`Retourne TRUE pour tout document qui a une valeur dans le champ « author » de hello.<br>`exists(query(price:5.00))` Retourne TRUE si la valeur de « price » est égale à « 5.00 ». |
| exp |Nombre d’Euler retourne déclenché toopower x. |`exp(x)` |
| floor |Arrondit vers le bas tooan entier. |`floor(x)`  <br> `floor(5.6)` Retourne 5 |
| hypo |Retourne Sqrt(sum(pow(x,2),pow(y,2))) sans dépassement positif ou négatif intermédiaire. |`hypo(x,y)`  <br> ` |
| if |Autorise les requêtes de fonction conditionnelle. Dans `if(test,value1,value2)`, le test est ou fait référence la valeur logique de tooa ou une expression qui retourne une valeur logique (TRUE ou FALSE). `value1`est hello valeur retournée par la fonction hello si test renvoie la valeur TRUE. `value2`est hello valeur retournée par la fonction hello si le test retourne FALSE. Une expression peut être n’importe quelle fonction qui génère des valeurs booléennes. Elle peut également être une fonction qui retourne des valeurs numériques, auquel cas la valeur 0 est interprétée comme false, ou qui retourne des chaînes, auquel cas une chaîne vide est interprétée comme false. |`if(termfreq(cat,'electronics'),popularity,42)`Cette fonction vérifie chaque toosee document s’il contient le terme hello « electronics » dans le champ cat de hello. Si elle existe, puis hello la valeur du champ de popularité hello est retourné. Sinon, valeur hello 42 est retournée. |
| linear |Implémente `m*x+c`, où m et c sont des constantes et x est une fonction arbitraire. Cela est équivalent`sum(product(m,x),c)`, mais légèrement plus efficace car elle est implémentée comme une fonction unique. |`linear(x,m,c) linear(x,2,4)` retourne `2*x+4` |
| ln |Logarithme naturel de hello retourne Hello spécifié (fonction). |`ln(x)` |
| log |Retourne hello journal base 10 de hello spécifié (fonction). |`log(x)   log(sum(x,100))` |
| map |Mappe toute valeur d’une fonction d’entrée x comprise entre min et cible spécifié de toohello max (inclus). hello arguments min et max doivent être des constantes. par défaut et la cible d’arguments hello peuvent être des constantes ou des fonctions. Si la valeur hello de x n’est pas comprise entre min et max, puis une valeur hello x est retournée ou une valeur par défaut est retournée s’il est spécifié comme argument de 5. |`map(x,min,max,target) map(x,0,0,1)`Remplace toute valeur too1 0. Cela peut être utile pour le traitement des valeurs par défaut 0.<br> `map(x,min,max,target,default)    map(x,0,100,1,-1)`Remplace toute valeur entre 0 et 100 too1 et toutes les autres valeurs trop-1.<br>  `map(x,0,100,sum(x,599),docfreq(text,solr))`Modifie les valeurs comprises entre 0 et 100 toox + 599 et tous les autres toofrequency de valeurs de durée de hello « solr » dans le texte du champ hello. |
| max |Retourne hello valeur numérique maximale de plusieurs fonctions ou constantes imbriquées, qui sont spécifiées en tant qu’arguments : `max(x,y,...)`. fonction max Hello peut également être utile pour « limiter par le bas » une autre fonction ou champ à une constante spécifiée.  Hello d’utilisation `field(myfield,max)` syntaxe pour sélectionner hello la valeur maximale d’un champ à valeurs multiples. |`max(myfield,myotherfield,0)` |
| Min |Retourne hello valeur numérique minimale de plusieurs fonctions imbriquées, des constantes, qui sont spécifiés en tant qu’arguments : `min(x,y,...)`. Hello fonction min peut également être utile pour fournir une « limite supérieure » sur une fonction à l’aide d’une constante. Hello d’utilisation `field(myfield,min)` syntaxe pour sélectionner hello la valeur minimale d’un champ à valeurs multiples. |`min(myfield,myotherfield,0)` |
| mod |Calcule le modulo hello de fonction hello x par y de fonction hello. |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| ms |Retourne la différence en millisecondes entre ses arguments. Les dates sont relative toohello Unix ou POSIX époque, minuit le 1er janvier 1970 UTC. Les arguments peuvent être nom hello d’un TrieDateField indexé, ou mathématique de date basée sur une date constante ou NOW. `ms()`est équivalent trop`ms(NOW)`, nombre de millisecondes depuis l’époque de hello. `ms(a)`Retourne le nombre hello de millisecondes depuis l’époque de hello hello argument représente. `ms(a,b)`Retourne hello les nombre de millisecondes que b se produit avant a, qui est `a - b`. |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| not |valeur Hello logiquement niée hello encapsulé (fonction). |`not(exists(author))` TRUE uniquement lorsque `exists(author)` a la valeur false. |
| ou |Une disjonction logique. |`or(value1,value2)` TRUE si value1 ou value2 a la valeur true. |
| pow |Déclenche hello spécifié toohello base spécifié power. `pow(x,y)`déclenche x toohello puissance y. |`pow(x,y)`<br>`pow(x,log(y))`<br>`pow(x,0.5)`Bonjour même en tant que racine. |
| product |Retourne hello produit de plusieurs valeurs ou fonctions qui sont spécifiées dans une liste séparée par des virgules. `mul(...)` peut également être utilisé comme alias pour cette fonction. |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| recip |Exécute une fonction réciproque avec `recip(x,m,a,b)` implémentant `a/(m*x+b)`, où m, a et b sont des constantes, et x toute fonction arbitrairement complexe. Lorsque a et b sont égaux et que x>=0, cette fonction a une valeur maximale de 1 qui diminue à mesure que x augmente. Augmenter la valeur hello un et b entraîne un déplacement de hello fonction entière tooa plate partie de la courbe de hello. Ces propriétés peuvent en faire une fonction idéale pour améliorer les documents plus récents lorsque x est `rord(datefield)`. |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| rad |Convertit de degrés tooradians. |`rad(x)` |
| rint |Toohello arrondit entière la plus proche. |`rint(x)`  <br> `rint(5.6)` Retourne 6 |
| sin |Retourne le sinus d’un angle. |`sin(x)` |
| sinh |Retourne le sinus hyperbolique d’un angle. |`sinh(x)` |
| scale |Les valeurs d’échelles de fonction de hello x, tel qu’elles soient comprises entre hello spécifié, valeurs et maxTarget. mise en œuvre actuelle Hello parcourt toutes les de hello fonction valeurs tooobtain hello min et max, afin de choisir la mise à l’échelle correcte hello. mise en œuvre actuelle Hello ne peut pas distinguer quand les documents ont été supprimés, ou les documents qui n’ont aucune valeur. Elle utilise les valeurs 0.0 dans ces cas. Cela signifie que si les valeurs sont normalement toutes supérieures à 0.0, vous pouvez toujours 0.0 comme hello toomap de valeur min à partir de. Dans ce cas, un `map()` fonction peut être utilisée en tant que solution de contournement toochange 0.0 tooa valeur dans la plage réelle de hello, comme illustré ici :`scale(map(x,0,0,5),1,2)` |`scale(x,minTarget,maxTarget)`<br>`scale(x,1,2)`Échelles hello des valeurs de x, tel que toutes les valeurs sont compris entre 1 et 2 inclus. |
| sqrt |Racine carrée retourne hello hello spécifié de valeur ou une fonction. |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| strdist |Calcule la distance entre deux chaînes hello. Utilise l’interface StringDistance de hello Lucene orthographe vérificateur et prend en charge toutes les implémentations de hello disponibles dans ce package. Autorise également les applications tooplug dans leurs propres ressources de Solr capacités de chargement. strdist prend les valeurs `(string1, string2, distance measure)`. Les valeurs possibles pour la mesure de distance sont les suivantes :<ul><li>jw : Jaro-Winkler</li><li>edit : distance de Levenstein ou d’édition</li><li>ngram : hello NGramDistance, si spécifié, peut éventuellement aussi passer la taille ngram hello trop. La valeur par défaut est 2.</li><li>FQN : Nom d’une implémentation de l’interface StringDistance de hello de classe de complet. Doit avoir un constructeur non arg.</li></ul> |`strdist("SOLR",id,edit)` |
| sub |Retourne x-y à partir de `sub(x,y)`. |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| Sum |Retourne hello somme de plusieurs valeurs ou fonctions qui sont spécifiées dans une liste séparée par des virgules. `add(...)` peut également être utilisé comme alias pour cette fonction. |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| termfreq |Retourne le nombre de hello de terme de hello s’affiche dans le champ hello pour ce document. |termfreq(text,’memory’) |
| tan |Retourne la tangente d’un angle. |`tan(x)` |
| tanh |Retourne la tangente hyperbolique d’un angle. |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a>Référence de champ et de facette de recherche
Lorsque vous utilisez des données toofind de recherche de journal, les résultats affichent différents champs et facettes. Certaines des informations de hello ne sont pas très descriptives. Utilisez hello suivant toohelp informations vous comprenez les résultats hello.

| Champ | Type de recherche | Description |
| --- | --- | --- |
| TenantId |Tout |Toopartition les données utilisées. |
| TimeGenerated |Tout |Utilisé toodrive hello chronologie, il est (dans la recherche et dans d’autres écrans). Il représente lors de l’élément de hello de données a été généré (en général sur l’agent de hello). Hello heure est exprimée au format ISO et toujours en UTC. Dans les cas de hello des types qui sont basées sur une instrumentation existante (autrement dit, les événements dans un journal), il s’agit généralement de hello temps que hello entrée/ligne/enregistrement du journal a été enregistré. Pour certaines des hello autres types produits via des packs d’administration ou dans le cloud hello (par exemple, les recommandations ou les alertes), hello représente temps quelque chose d’autre. Il s’agit de heure hello lorsque ce nouvel élément de données avec un instantané d’une configuration quelconque a été collecté, ou une recommandation/alerte a été générée en fonction de celui-ci. |
| EventID |Événement |ID d’événement dans le journal des événements Windows hello. |
| EventLog |Événement |Journal des événements où l’événement de hello a été enregistré par Windows. |
| EventLevelName |Événement |Critique, avertissement, information ou réussite |
| EventLevel |Événement |Valeur numérique indiquant le niveau d’événement : critique, avertissement, information ou réussite (utilisez la valeur EventLevelName pour des requêtes plus faciles et mieux lisibles). |
| SourceSystem |Tout |D'où proviennent les données hello (en termes de joindre le service de toohello en mode). Entre autres, on peut citer Microsoft System Center Operations Manager et le stockage Azure. |
| ObjectName |PerfHourly |Nom d’objet de performances Windows. |
| InstanceName |PerfHourly |Nom d’instance du compteur de performances Windows. |
| CounteName |PerfHourly |Nom du compteur de performances Windows. |
| ObjectDisplayName |PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty |Nom complet de l’objet de hello ciblé par une règle de collecte des performances dans Operations Manager. Peut également être le nom d’affichage hello d’objet hello découvert par Operational Insights, ou contre le hello alerte a été générée. |
| RootObjectName |PerfHourly, ConfigurationAlert, ConfigurationObject, ConfigurationObjectProperty |Nom d’affichage du parent hello parent de hello (dans une relation d’hébergement double) d’objet hello ciblé par une règle de collecte des performances dans Operations Manager. Peut également être le nom d’affichage hello d’objet hello découvert par Operational Insights, ou contre le hello alerte a été générée. |
| Ordinateur |La plupart des types |Nom de l’ordinateur auquel appartiennent les données hello. |
| DeviceName |ProtectionStatus |Les données des ordinateurs nom hello appartient trop (identique à « Computer »). |
| DetectionId |ProtectionStatus | |
| ThreatStatusRank |ProtectionStatus |Classement d’état de menace est une représentation numérique de l’état de la menace hello. Codes de réponse tooHTTP similaire, classement de hello a des écarts entre les nombres hello (c’est pourquoi aucune menace est 150 et non 100 ou 0), ne laissant place tooadd nouveaux États. Pour un cumul d’état de la menace et l’état de protection, l’intention hello est tooshow hello pire état hello ordinateur a été durant hello période sélectionnée. nombres de Hello classent les différents États, hello afin que vous pouvez rechercher hello enregistrement avec un nombre plus élevé de hello. |
| ThreatStatus |ProtectionStatus |Description de ThreatStatus, mappe 1:1 avec ThreatStatusRank. |
| TypeofProtection |ProtectionStatus |Produit anti-programme malveillant détecté sur l’ordinateur de hello : aucun, outil de suppression de logiciels malveillants de Microsoft, Forefront et ainsi de suite. |
| ScanDate |ProtectionStatus | |
| SourceHealthServiceId |ProtectionStatus, RequiredUpdate |ID du service de contrôle d’intégrité de l’agent de cet ordinateur. |
| HealthServiceId |La plupart des types |ID du service de contrôle d’intégrité de l’agent de cet ordinateur. |
| ManagementGroupName |La plupart des types |Nom du groupe d’administration pour les agents liés à Operations Manager. Dans le cas contraire, il sera Null/vide. |
| ObjectType |ConfigurationObject |Type (comme « type » ou « classe » dans le pack d’administration d’Operations Manager) pour cet objet découvert par l’évaluation de configuration Log Analytics. |
| UpdateTitle |RequiredUpdate |Nom de la mise à jour de hello est pas installée. |
| PublishDate |RequiredUpdate |Lorsque la mise à jour hello a été publiée sur Microsoft Update. |
| Serveur |RequiredUpdate |Les données des ordinateurs nom hello appartient trop (identique à « Computer »). |
| Produit |RequiredUpdate |Produit hello mise à jour s’applique à. |
| UpdateClassification |RequiredUpdate |Type de mise à jour (par exemple, correctif cumulatif ou service pack). |
| KBID |RequiredUpdate |ID d’article de la base de connaissances qui décrit cette meilleure pratique ou cette mise à jour. |
| WorkflowName |ConfigurationAlert |Nom de la règle de hello ou l’analyse qui a produit l’alerte de hello. |
| Severity |ConfigurationAlert |Niveau de gravité d’alerte de hello. |
| Priorité |ConfigurationAlert |Priorité d’alerte de hello. |
| IsMonitorAlert |ConfigurationAlert |Cette alerte est-elle générée par une analyse (true) ou une règle (false) ? |
| AlertParameters |ConfigurationAlert |XML avec des paramètres d’alerte de journal Analytique hello hello. |
| Context |ConfigurationAlert |XML avec le contexte hello d’alerte d’Analytique de journal hello. |
| Charge de travail |ConfigurationAlert |Technologie ou une charge de travail hello alerte fait référence à. |
| AdvisorWorkload |Recommandation |Technologie ou la charge de travail hello recommandation fait référence à. |
| Description |ConfigurationAlert |Description de l’alerte (en bref). |
| DaysSinceLastUpdate |UpdateAgent |Combien de jours (tooTimeGenerated relative de cet enregistrement) cet agent installation de mise à jour à partir de Windows Server Update Services (WSUS) ou Microsoft Update ? |
| DaysSinceLastUpdateBucket |UpdateAgent |Catégorisation, basée sur la valeur DaysSinceLastUpdate, en intervalles de planification du temps écoulé depuis qu’un ordinateur a installé pour la dernière fois une mise à jour quelconque provenant de WSUS ou de Microsoft Update. |
| AutomaticUpdateEnabled |UpdateAgent |Activation ou désactivation de la vérification de mise à jour automatique sur cet agent. |
| AutomaticUpdateValue |UpdateAgent |Téléchargement tooautomatically ensemble la vérification de mise à jour automatique n’est et installer, téléchargement uniquement ou vérification uniquement ? |
| WindowsUpdateAgentVersion |UpdateAgent |Numéro de version de l’agent de Microsoft Update hello. |
| WSUSServer |UpdateAgent |Quel serveur WSUS cet agent de mise à jour cible-t-il ? |
| OSVersion: |UpdateAgent |Version du système d’exploitation de hello que cet agent de mise à jour est en cours d’exécution. |
| Nom |Recommendation, ConfigurationObjectProperty |Nom ou titre de recommandation de hello, ou nom de propriété hello à partir de l’évaluation de la configuration Analytique de journal. |
| Valeur |ConfigurationObjectProperty |Valeur d’une propriété de l’évaluation de configuration de Log Analytics. |
| KBLink |Recommandation |Article toohello Ko URL qui décrit cette meilleure pratique ou la mise à jour. |
| RecommendationStatus |Recommandation |Recommandations font partie des hello quelques types dont les enregistrements obtenir l’index de recherche toohello mis à jour, pas vient d’être ajoutée. Cet état change si la recommandation de hello est active/ouverte ou si le journal Analytique détecte qu’elle a été résolu. |
| RenderedDescription |Événement |Description rendue (texte réutilisé avec des paramètres remplis) d’un événement Windows. |
| ParameterXml |Événement |XML avec les paramètres de hello dans la section de données hello d’un événement Windows (tel qu’affiché dans l’Observateur d’événements). |
| EventData |Événement |XML avec hello toute section données d’un événement Windows (tel qu’affiché dans l’Observateur d’événements). |
| Source |Événement |Source de journal des événements qui a généré l’événement de hello. |
| EventCategory |Événement |Catégorie d’événement hello, directement à partir de journal des événements Windows hello. |
| Nom d’utilisateur |Événement |Nom d’utilisateur de l’événement de Windows hello (en général, NT AUTHORITY\LOCALSYSTEM). |
| SampleValue |PerfHourly |Valeur moyenne pour l’agrégation de toutes les heures hello d’un compteur de performances. |
| Min |PerfHourly |Valeur minimale dans l’intervalle horaire de hello d’un agrégat horaire de compteur de performances. |
| max |PerfHourly |Valeur maximale dans l’intervalle horaire de hello d’un agrégat horaire de compteur de performances. |
| Percentile95 |PerfHourly |Hello 95e centile pour l’intervalle horaire de hello d’un agrégat horaire de compteur de performances. |
| SampleCount |PerfHourly |Enregistrement d’agrégation échantillons de compteur de performances brutes combien ont été tooproduce utilisé ce toutes les heures. |
| Menace |ProtectionStatus |Nom du programme malveillant trouvé. |
| StorageAccount |W3CIISLog |Journal hello de compte de stockage Azure a été lu à partir de. |
| AzureDeploymentID |W3CIISLog |ID de déploiement Azure du journal de hello hello cloud service appartient. |
| Rôle |W3CIISLog |Propriétaire du rôle du journal de hello hello Azure cloud service. |
| RoleInstance |W3CIISLog |Instance du hello rôle Azure hello journal appartient. |
| sSiteName |W3CIISLog |Site Web IIS qui hello journal appartient too(metabase notation) ; champ s-sitename Hello journal d’origine de hello. |
| sComputerName |W3CIISLog |champ s-computername Hello journal d’origine de hello. |
| sIP |W3CIISLog |Serveur IP adresse hello HTTP requête a été envoyée. champ s-ip Hello journal d’origine de hello. |
| csMethod |W3CIISLog |Méthode HTTP (par exemple, GET/POST) utilisée par le client hello dans la demande HTTP de hello. Hello cs-method dans le journal d’origine de hello. |
| cIP |W3CIISLog |Requête HTTP de client IP adresse hello provenait. champ c-ip Hello journal d’origine de hello. |
| csUserAgent |W3CIISLog |Agent utilisateur HTTP déclaré par le client de hello (navigateur ou autre). Bonjour cs-user-agent dans le journal d’origine de hello. |
| scStatus |W3CIISLog |Code d’état HTTP (par exemple, 200/403/500) retourné par le client de toohello server hello. Hello cs-METHODE dans le journal d’origine de hello. |
| TimeTaken |W3CIISLog |Combien de temps (en millisecondes), cette demande hello a duré toocomplete. champ timetaken Hello journal d’origine de hello. |
| csUriStem |W3CIISLog |URI relatif (sans adresse d’hôte, c’est-à-dire /search) qui a été demandé. champ cs-uristem Hello journal d’origine de hello. |
| csUriQuery |W3CIISLog |Requête d’URI. Les requêtes d’URI sont nécessaires uniquement pour les pages dynamiques, telles que des pages ASP. Par conséquent, ce champ contient souvent un trait d’union pour les pages statiques. |
| sPort |W3CIISLog |Port du serveur qui hello demande HTTP a été envoyée trop (et qu’IIS écoute, puisqu’il l’a récupéré). |
| csUserName |W3CIISLog |Nom d’utilisateur, authentifié si la demande de hello est authentifiée et non anonyme. |
| csVersion |W3CIISLog |Version du protocole HTTP utilisée dans la demande de hello (par exemple, HTTP/1.1). |
| csCookie |W3CIISLog |Informations sur le cookie. |
| csReferer |W3CIISLog |Cet utilisateur hello dernière visité du site. Ce site a fourni un lien toohello le site actuel. |
| csHost |W3CIISLog |En-tête d’hôte (par exemple, www.mysite.com) qui a été demandé. |
| scSubStatus |W3CIISLog |Code d'erreur du sous-état. |
| scWin32Status |W3CIISLog |Code d’état Windows. |
| csBytes |W3CIISLog |Octets envoyés dans la demande de hello hello client toohello serveur. |
| scBytes |W3CIISLog |Octets retourné en réponse hello du client de toohello serveur hello. |
| ConfigChangeType |ConfigurationChange |Type de modification (par exemple, services Windows et logiciels). |
| ChangeCategory |ConfigurationChange |Catégorie de la modification de hello (modifiées, ajoutées/supprimées). |
| SoftwareType |ConfigurationChange |Type de logiciel (mise à jour, application). |
| SoftwareName |ConfigurationChange |Nom du logiciel de hello (seules les modifications toosoftware applicable). |
| Éditeur |ConfigurationChange |Fournisseur qui publie le logiciel hello (seules les modifications toosoftware applicable). |
| SvcChangeType |ConfigurationChange |Type de modification appliquée à un service Windows (état, type d’état, chemin d’accès, compte de service). Il s’agit de tooWindows applicables uniquement les modifications de service. |
| SvcDisplayName |ConfigurationChange |Nom complet du service hello qui a été modifié. |
| SvcName |ConfigurationChange |Nom du service hello qui a été modifié. |
| SvcState |ConfigurationChange |Nouvel état (actuel) du service de hello. |
| SvcPreviousState |ConfigurationChange |Précédent état connu du service hello (applicable uniquement si l’état du service a changé). |
| SvcStartupType |ConfigurationChange |Type de démarrage du service. |
| SvcPreviousStartupType |ConfigurationChange |Dernier type de démarrage du service (applicable uniquement si le type de démarrage du service a été modifié). |
| SvcAccount |ConfigurationChange |Compte de service. |
| SvcPreviousAccount |ConfigurationChange |Compte de service précédent (applicable uniquement si le compte de service a été modifié). |
| SvcPath |ConfigurationChange |Chemin d’accès toohello fichier exécutable du service de Windows hello. |
| SvcPreviousPath |ConfigurationChange |Chemin d’accès précédent hello exécutable pour hello service Windows (applicable uniquement si elle a changé). |
| SvcDescription |ConfigurationChange |Description du service de hello. |
| Précédent |ConfigurationChange |État précédent de ce logiciel (installé, non installé, version précédente). |
| Current |ConfigurationChange |Dernier état de ce logiciel (installé, non installé, version actuelle). |

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les recherches de journal :

* Se familiariser avec [recherche de journal](log-analytics-log-searches.md) tooview détaillées des informations collectées par les solutions.
* Utilisez [des champs personnalisés dans le journal Analytique](log-analytics-custom-fields.md) tooextend des recherches de journaux.
