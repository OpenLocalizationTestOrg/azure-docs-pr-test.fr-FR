---
title: "exemples d’aaaQuery pour les modèles d’utilisation courants dans le flux de données Analytique | Documents Microsoft"
description: "Modèles courants de requêtes Azure Stream Analytics"
keywords: "exemples de requête"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a>Exemples de requête pour les modes d’utilisation courants dans Stream Analytics
## <a name="introduction"></a>Introduction
Les requêtes dans Azure Stream Analytics sont exprimées dans un langage de requête de type SQL. Ces requêtes sont documentées dans hello [Analytique de flux de données de référence du langage de requête](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide. Ce article décrit les solutions tooseveral requête des modèles courants, les selon des scénarios concrets. Il est un travail en cours et continue toobe mis à jour avec les nouveaux modèles de manière continue.

## <a name="query-example-convert-data-types"></a>Exemple de requête : Convertir des types de données
**Description**: définir des types de hello de propriétés sur les flux d’entrée hello.
Par exemple, le poids de voiture hello sera disponible sur les flux d’entrée hello sous forme de chaînes et doit toobe converti trop**INT** tooperform **somme** , configurez-le.

**Entrée**:

| Marque | Temps | Poids |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |"1000" |
| Honda |2015-01-01T00:00:02.0000000Z |"2000" |

**Sortie**:

| Marque | Poids |
| --- | --- |
| Honda |3000 |

**Solution**:

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**Explication**: utilisez un **CAST** instruction Bonjour **poids** champ toospecify son type de données. Consultez la liste hello des types de données pris en charge dans [des types de données (Analytique de flux de données Azure)](https://msdn.microsoft.com/library/azure/dn835065.aspx).

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a>Exemple de requête : utilisation non Like comme toodo critères spéciaux
**Description**: Vérifiez qu’une valeur de champ d’événement de hello correspond à un certain modèle.
Par exemple, vérifiez que les résultats hello retourne plaques d’immatriculation qui commence par A et se terminer par 9.

**Entrée**:

| Marque | LicensePlate | Temps |
| --- | --- | --- |
| Honda |ABC-123 |2015-01-01T00:00:01.0000000Z |
| Toyota |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC-369 |2015-01-01T00:00:03.0000000Z |

**Sortie**:

| Marque | LicensePlate | Temps |
| --- | --- | --- |
| Toyota |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC-369 |2015-01-01T00:00:03.0000000Z |

**Solution**:

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

**Explication**: hello d’utilisation **comme** hello de toocheck instruction **LicensePlate** valeur du champ. Il doit commencer par un A, puis avoir une chaîne de zéro, un ou plusieurs caractères, puis se terminer par un 9. 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a>Exemple de requête : Spécifier la logique pour différentes casses/valeurs (instructions CASE)
**Description** : Fournir un calcul différent pour un champ en fonction de certains critères.
Par exemple, fournir une description de chaîne pour le nombre de voitures Hello même rendre passé, avec une casse spéciale pour 1.

**Entrée**:

| Marque | Temps |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Sortie**:

| CarsPassed | Temps |
| --- | --- | --- |
| 1 Honda |2015-01-01T00:00:10.0000000Z |
| 2 Toyota |2015-01-01T00:00:10.0000000Z |

**Solution**:

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**Explication**: hello **cas** clause nous permet de tooprovide un calcul différent, en fonction de certains critères (dans notre cas, le nombre de hello de voitures hello dans la fenêtre d’agrégation hello).

## <a name="query-example-send-data-toomultiple-outputs"></a>Exemple de requête : envoyer des données toomultiple fournit en sortie
**Description**: toomultiple de données d’envoi de sortie cibles à partir d’une seule tâche.
Par exemple, analyser des données pour une alerte de seuil et stockage de tooblob tous les événements d’archivage.

**Entrée**:

| Marque | Temps |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Output1**:

| Marque | Temps |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Output2**:

| Marque | Temps | Nombre |
| --- | --- | --- |
| Toyota |2015-01-01T00:00:10.0000000Z |3 |

**Solution**:

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

**Explication**: hello **INTO** clause indique Analytique de flux de données qui génère des toowrite hello données toofrom Hello cette instruction.
Hello première requête est une passerelle de données hello nous avons reçu sortie tooan que nous avons nommé **ArchiveOutput**.
fait une requête de deuxième Hello certains d’agrégation simple et le filtrage et envoie les résultats de hello tooa de système d’alerte en aval.

Notez que vous pouvez également réutiliser des résultats d’expressions de table communes (CTE) hello hello (tel que **WITH** instructions) dans plusieurs instructions de sortie. Cette option a hello avantage de l’ouverture de source d’entrée de toohello des lecteurs moins.
Par exemple : 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a>Exemple de requête : Compter des valeurs uniques
**Description**: hello dénombrer les valeurs de champ unique qui s’affichent dans le flux hello dans une fenêtre de temps.
Par exemple, le nombre unique fait de voitures passées gare de péage hello dans une fenêtre de 2 secondes ?

**Entrée**:

| Marque | Temps |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Output:**

| Nombre | Temps |
| --- | --- |
| 2 |2015-01-01T00:00:02.000Z |
| 1 |2015-01-01T00:00:04.000Z |

**Solution :**

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


**Explication :**
**COUNT (DISTINCT Vérifiez)** renvoie hello le nombre de valeurs distinctes dans hello **rendre** colonne dans une fenêtre de temps.

## <a name="query-example-determine-if-a-value-has-changed"></a>Exemple de requête : Déterminer si une valeur a changé
**Description**: examinez un toodetermine valeur précédente si elle est différente de la valeur actuelle de hello.
Par exemple, est voiture précédente de hello sur hello de route de péage hello que même rendre aussi voiture en cours de hello ?

**Entrée**:

| Marque | Temps |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |

**Sortie**:

| Marque | Temps |
| --- | --- |
| Toyota |2015-01-01T00:00:02.0000000Z |

**Solution**:

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

**Explication**: utilisez **LAG** toopeek dans hello d’entrée d’un événement nouveau flux de données et obtenir hello **rendre** valeur. Comparez-le toohello **rendre** valeur sur les événements en cours hello et sortie hello si elles sont différentes.

## <a name="query-example-find-hello-first-event-in-a-window"></a>Exemple de requête : rechercher hello premier événement dans une fenêtre
**Description**: rechercher hello première voiture dans chaque intervalle de 10 minutes.

**Entrée**:

| LicensePlate | Marque | Temps |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:05:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Sortie**:

| LicensePlate | Marque | Temps |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |

**Solution**:

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

Maintenant assurons-nous modification hello problème et rechercher hello première voiture d’un particulier dans chaque intervalle de 10 minutes.

| LicensePlate | Marque | Temps |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Solution**:

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a>Exemple de requête : rechercher hello du dernier événement dans une fenêtre
**Description**: voiture de dernière hello rechercher dans chaque intervalle de 10 minutes.

**Entrée**:

| LicensePlate | Marque | Temps |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:05:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Sortie**:

| LicensePlate | Marque | Temps |
| --- | --- | --- |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Solution**:

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

**Explication**: il existe deux étapes de requête de hello. Hello première recherche un hello dernière horodatage dans les fenêtres de 10 minutes. les jointures Hello deuxième étape hello des résultats de requête de première hello avec hello d’origine flux toofind hello les événements qui correspondent aux hello derniers horodatages dans chaque fenêtre. 

## <a name="query-example-detect-hello-absence-of-events"></a>Exemple de requête : détecte l’absence de hello d’événements
**Description** : Vérifier qu’un flux ne contient aucune valeur correspondant à certains critères.
Par exemple, 2 voitures consécutifs de hello que même rendre saisi route de péage hello dans hello dernière 90 secondes ?

**Entrée**:

| Marque | LicensePlate | Temps |
| --- | --- | --- |
| Honda |ABC-123 |2015-01-01T00:00:01.0000000Z |
| Honda |AAA-999 |2015-01-01T00:00:02.0000000Z |
| Toyota |DEF-987 |2015-01-01T00:00:03.0000000Z |
| Honda |GHI-345 |2015-01-01T00:00:04.0000000Z |

**Sortie**:

| Marque | Temps | CurrentCarLicensePlate | FirstCarLicensePlate | FirstCarTime |
| --- | --- | --- | --- | --- |
| Honda |2015-01-01T00:00:02.0000000Z |AAA-999 |ABC-123 |2015-01-01T00:00:01.0000000Z |

**Solution**:

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

**Explication**: utilisez **LAG** toopeek dans hello d’entrée d’un événement nouveau flux de données et obtenir hello **rendre** valeur. Comparer toohello **rendre** valeur dans l’événement hello en cours, puis sur les événements de hello sortie si elles sont hello identiques. Vous pouvez également utiliser **LAG** tooget des données sur les voitures précédente hello.

## <a name="query-example-detect-hello-duration-between-events"></a>Exemple de requête : détecter la durée hello entre les événements
**Description**: trouver durée hello d’un événement donné. Par exemple, étant donné un parcours de web, déterminer temps hello sur une fonctionnalité.

**Entrée**:  

| Utilisateur | Fonctionnalité | Événement | Temps |
| --- | --- | --- | --- |
| user@location.com |RightMenu |Démarrer |2015-01-01T00:00:01.0000000Z |
| user@location.com |RightMenu |Terminer |2015-01-01T00:00:08.0000000Z |

**Sortie**:  

| Utilisateur | Fonctionnalité | Durée |
| --- | --- | --- |
| user@location.com |RightMenu |7 |

**Solution**:

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

**Explication**: hello d’utilisation **dernière** fonction tooretrieve hello dernière **temps** valeur lorsque le type d’événement hello a été **Démarrer**. Hello **dernière** fonction utilise **PARTITION BY [user]** tooindicate qui hello le résultat est calculé par l’utilisateur unique. requête de Hello a un seuil maximal de 1 heure pour la différence de temps hello entre **Démarrer** et **arrêter** événements, mais peut être configuré en fonction des besoins **(limite DURATION(hour, 1)**.

## <a name="query-example-detect-hello-duration-of-a-condition"></a>Exemple de requête : détecter la durée hello d’une condition
**Description** : Rechercher la durée pendant laquelle une condition s’est produite.
Par exemple, supposez qu’à la suite d’un bogue, le poids de toutes les voitures est incorrect (supérieur à 20 000 livres). Nous voulons que la durée de hello toocompute de bogue de hello.

**Entrée**:

| Marque | Temps | Poids |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |2000 |
| Toyota |2015-01-01T00:00:02.0000000Z |25000 |
| Honda |2015-01-01T00:00:03.0000000Z |26000 |
| Toyota |2015-01-01T00:00:04.0000000Z |25000 |
| Honda |2015-01-01T00:00:05.0000000Z |26000 |
| Toyota |2015-01-01T00:00:06.0000000Z |25000 |
| Honda |2015-01-01T00:00:07.0000000Z |26000 |
| Toyota |2015-01-01T00:00:08.0000000Z |2000 |

**Sortie**:

| StartFault | EndFault |
| --- | --- |
| 2015-01-01T00:00:02.000Z |2015-01-01T00:00:07.000Z |

**Solution**:

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

**Explication**: utilisez **LAG** tooview hello flux d’entrée des dernières 24 heures, puis recherchez les instances où **StartFault** et **StopFault** sont couvertes par hello poids < 20000.

## <a name="query-example-fill-missing-values"></a>Exemple de requête : Remplir les valeurs manquantes
**Description**: pour les flux de hello d’événements qui ont des valeurs manquantes, produisent un flux d’événements à intervalles réguliers.
Par exemple, génère un événement toutes les 5 secondes qui indique le point de données hello plus récemment affichée.

**Entrée**:

| t | value |
| --- | --- |
| "2014-01-01T06:01:00" |1 |
| "2014-01-01T06:01:05" |2 |
| "2014-01-01T06:01:10" |3 |
| "2014-01-01T06:01:15" |4 |
| "2014-01-01T06:01:30" |5 |
| "2014-01-01T06:01:35" |6 |

**Sortie (10 premières lignes)**:

| windowend | lastevent.t | lastevent.value |
| --- | --- | --- |
| 2014-01-01T14:01:00.000Z |2014-01-01T14:01:00.000Z |1 |
| 2014-01-01T14:01:05.000Z |2014-01-01T14:01:05.000Z |2 |
| 2014-01-01T14:01:10.000Z |2014-01-01T14:01:10.000Z |3 |
| 2014-01-01T14:01:15.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:20.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:25.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:30.000Z |2014-01-01T14:01:30.000Z |5 |
| 2014-01-01T14:01:35.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:40.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:45.000Z |2014-01-01T14:01:35.000Z |6 |

**Solution**:

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


**Explication**: cette requête génère des événements toutes les 5 secondes et sorties hello du dernier événement reçu précédemment. Hello [saut fenêtre](https://msdn.microsoft.com/library/dn835041.aspx "fenêtre saut--Analytique de flux de données Azure") durée détermine combien hello arrière requête se présente événement plus récente de hello toofind (300 secondes dans cet exemple).

## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

