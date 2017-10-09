---
title: "les fonctions aaaAzure JavaScript Analytique de flux de données définis par l’utilisateur | Documents Microsoft"
description: "Effectuer des requêtes avancées avec les fonctions JavaScript définies par l’utilisateur"
keywords: "JavaScript, fonctions définies par l’utilisateur"
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a>Fonctions JavaScript définies par l’utilisateur Azure Stream Analytics
Azure Stream Analytics prend en charge les fonctions définies par l’utilisateur écrites en JavaScript. Série de hello **chaîne**, **RegExp**, **mathématiques**, **tableau**, et **Date** méthodes qui JavaScript fournit, les transformations de données complexes avec des tâches de flux de données Analytique deviennent toocreate plus facile.

## <a name="javascript-user-defined-functions"></a>Fonctions JavaScript définies par l’utilisateur
Les fonctions JavaScript définies par l’utilisateur prennent en charge les fonctions scalaires de calcul pur sans état qui ne nécessitent pas de connectivité externe. Hello retournent la valeur d’une fonction peut uniquement être une valeur scalaire (unique). Après avoir ajouté un travail de tooa de fonction définie par l’utilisateur de JavaScript, vous pouvez utiliser fonction hello n’importe où dans la requête de hello, comme une fonction scalaire intégrée.

Voici quelques scénarios dans lesquels les fonctions JavaScript définies par l’utilisateur vous seront utiles :
* Analyse et manipulation de chaînes avec des fonctions d’expressions régulières, par exemple **Regexp_Replace()** et **Regexp_Extract()**
* Décodage de données encodées, par exemple la conversion de binaire en hexadécimal
* Calculs mathématiques avec les fonctions **Math** de JavaScript
* Opérations de tableaux comme le tri, la jointure, la recherche et le remplissage

Voici quelques actions que vous ne pouvez pas effectuer avec une fonction JavaScript définie par l’utilisateur dans Stream Analytics :
* Appel de points de terminaison REST externes, par exemple la recherche inversée d’une adresse IP ou l’extraction de données de référence à partir d’une source externe
* Sérialisation ou désérialisation à un format d’événement personnalisé sur les entrées/sorties
* Création d’agrégats personnalisés

Bien que les fonctions comme **Date.GetDate()** ou **Math.Random ()** ne sont pas bloqués dans la définition de fonctions hello, vous devez éviter leur utilisation. Ces fonctions **pas** retour hello même résultat chaque fois que vous les appelez et hello service d’Analytique de flux de données Azure ne conserve pas un journal d’appels de fonction et a renvoyé des résultats. Si une fonction retourne un résultat différent sur hello événements mêmes, la répétabilité n’est pas garantie lorsqu’un travail est redémarré par vous ou par le service de flux de données Analytique hello.

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a>Ajouter une fonction définie par l’utilisateur de JavaScript dans hello portail Azure
toocreate une fonction définie par l’utilisateur JavaScript simple sous une tâche de flux de données Analytique existante, procédez comme suit :

1.  Bonjour portail Azure, recherchez votre tâche de flux de données Analytique.
2.  Sous **TOPOLOGIE DE LA TÂCHE**, sélectionnez votre fonction. Une liste vide de fonctions apparaît.
3.  toocreate une nouvelle fonction définie par l’utilisateur, sélectionnez **ajouter**.
4.  Sur hello **nouvelle fonction** panneau, pour **Type de fonction**, sélectionnez **JavaScript**. Un modèle de fonction par défaut s’affiche dans l’éditeur de hello.
5.  Pourquoi **alias des UDF**, entrez **hex2Int**, modifiez l’implémentation de fonction hello comme suit :

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  Sélectionnez **Enregistrer**. Votre fonction apparaît dans la liste des fonctions hello.
7.  Sélectionnez hello nouvelle **hex2Int** la fonction et vérifiez la définition de fonction hello. Toutes les fonctions ont un **UDF** alias de préfixe de fonction toohello ajouté. Vous devez trop*inclure hello préfixe* lorsque vous appelez la fonction hello dans votre requête Analytique de flux de données. Dans ce cas, vous appelez **UDF.hex2Int**.

## <a name="call-a-javascript-user-defined-function-in-a-query"></a>Appeler une fonction JavaScript définie par l’utilisateur dans une requête

1. Bonjour éditeur de requête, sous **travail topologie**, sélectionnez **requête**.
2.  Modifier votre requête, puis appelez la fonction hello défini par l’utilisateur, comme suit :

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  fichier de données exemple hello tooupload, entrée de tâche avec le bouton hello.
4.  tootest votre requête, sélectionnez **Test**.


## <a name="supported-javascript-objects"></a>Objets JavaScript pris en charge
Les fonctions JavaScript définies par l’utilisateur Azure Stream Analytics prennent en charge les objets prédéfinis standard du langage JavaScript. Pour obtenir la liste de ces objets, consultez [Objets globaux](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).

### <a name="stream-analytics-and-javascript-type-conversion"></a>Conversion de type Stream Analytics et JavaScript

Il existe des différences entre les types hello qui prennent en charge de langage de requête de flux de données Analytique hello et JavaScript. Ce tableau répertorie les mappages de conversion hello entre hello deux :

Stream Analytics | JavaScript
--- | ---
bigint | Nombre (JavaScript peut représenter uniquement des entiers des tooprecisely 2 ^ 53)
DateTime | Date (JavaScript ne prend en charge que les millisecondes)
double | Number
nvarchar(MAX) | String
Enregistrement | Object
Tableau | Tableau
NULL | Null


Voici les conversions de JavaScript à Stream Analytics :


JavaScript | Stream Analytics
--- | ---
Number | Bigint (si le nombre de hello est arrondi et entre long. MinValue et long. MaxValue ; dans le cas contraire, il est double)
Date | DateTime
String | nvarchar(MAX)
Object | Enregistrement
Tableau | Tableau
Null, Undefined | NULL
Un autre type (par exemple une fonction ou une erreur) | Non pris en charge (entraîne une erreur d’exécution)

## <a name="troubleshooting"></a>Résolution des problèmes
Erreurs d’exécution JavaScript sont considérées comme irrécupérables et sont exposés via le journal d’activité hello. tooretrieve hello journal, hello portail Azure, accédez tooyour travail et sélectionnez **le journal d’activité**.


## <a name="other-javascript-user-defined-function-patterns"></a>Autres modèles de fonctions JavaScript définies par l’utilisateur

### <a name="write-nested-json-toooutput"></a>Écrire des toooutput JSON imbriquée
Si vous disposez d’une étape de traitement suivi qui utilise une tâche de flux de données Analytique de sortie en tant qu’entrée, et il requiert un format JSON, vous pouvez écrire un toooutput de chaîne JSON. Hello l’exemple suivant appelle hello **JSON.stringify()** toopack toutes les paires nom/valeur de hello d’entrée et de les écrivent en tant que valeur de chaîne unique dans la sortie de fonction.

**Définition de la fonction JavaScript définie par l’utilisateur :**

```
function main(x) {
return JSON.stringify(x);
}
```

**Exemple de requête :**
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir de l’aide supplémentaire, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Mise à l'échelle des travaux Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Références sur le langage des requêtes Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
