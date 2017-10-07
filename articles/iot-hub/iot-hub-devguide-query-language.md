---
title: "aaaUnderstand hello langage de requête Azure IoT Hub | Documents Microsoft"
description: "Guide du développeur - description du langage de requête de type SQL IoT Hub hello utilisée tooretrieve informations jumeaux de périphérique et les travaux à partir de votre hub IoT."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a>Référence - Langage de requête IoT Hub pour les jumeaux d’appareil, les travaux et le routage des messages

IoT Hub fournit un puissant langage de type SQL des informations de tooretrieve concernant [jumeaux de périphérique] [ lnk-twins] et [travaux][lnk-jobs]et [routage des messages][lnk-devguide-messaging-routes]. Cet article présente les éléments suivants :

* Une introduction toohello principales fonctionnalités de langage de requête IoT Hub, de hello et
* Hello description détaillée du langage de hello.

## <a name="get-started-with-device-twin-queries"></a>Bien démarrer avec les requêtes de jumeau d’appareil
Des [jumeaux d’appareil][lnk-twins] peuvent contenir des objets JSON arbitraires tels que des balises (tags) et des propriétés. IoT Hub vous permet de jumeaux de périphérique tooquery en tant qu’un seul document JSON contenant toutes les informations de périphérique double.
Supposons, par exemple, que vos jumeaux de périphérique de hub IoT ont hello suivant la structure :

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

IoT Hub expose jumeaux de périphérique hello en tant que document collection appelée **périphériques**.
Par conséquent, hello suivant la requête récupère définition hello de jumeaux du périphérique :

```sql
SELECT * FROM devices
```

> [!NOTE]
> Les kits [Azure IoT SDK][lnk-hub-sdks] prennent en charge la pagination des résultats volumineux.

IoT Hub permet jumeaux de périphérique tooretrieve filtrage avec des conditions arbitraires. Par exemple,

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

Récupère hello jumeaux de périphérique avec hello **location.region** ensemble trop de balises**US**.
Les opérateurs booléens et les comparaisons arithmétiques sont également pris en charge, par exemple,

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

Récupère tous les jumeaux périphérique situé dans hello nous configuré toosend télémétrie moins souvent que toutes les minutes. Pour des raisons pratiques, il est également possible toouse les constantes de matrice avec hello **IN** et **NDANS** (pas dans) les opérateurs. Par exemple,

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

récupère tous les jumeaux d’appareil ayant signalé une connectivité Wi-Fi ou câblée. Il est souvent nécessaire tooidentify tous les jumeaux de périphérique qui contiennent une propriété spécifique. IoT Hub prend en charge la fonction hello `is_defined()` à cet effet. Par exemple,

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

récupérer tous les jumeaux de périphérique qui définissent hello `connectivity` a signalé de propriété. Consultez toohello [clause WHERE] [ lnk-query-where] section de référence complète de hello Hello des fonctionnalités de filtre.

Le regroupement et les agrégations sont également pris en charge. Par exemple,

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

Retourne le nombre hello de périphériques de hello dans chaque état de configuration de télémétrie.

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

Hello exemple précédent illustre une situation où trois unités signalé configuration réussie, deux sont toujours l’application configuration de hello, et un a signalé une erreur.

### <a name="c-example"></a>Exemple en code C#
fonctionnalités de requête Hello sont exposée par hello [SDK du service C#] [ lnk-hub-sdks] Bonjour **RegistryManager** classe.
Voici un exemple de requête simple :

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

Notez comment hello **requête** objet est instancié avec une taille de page (haut too1000), et puis plusieurs pages peuvent être récupérés en appelant hello **GetNextAsTwinAsync** méthodes plusieurs fois.
Notez que cet objet de requête hello expose plusieurs **suivant\***, selon l’option de la désérialisation de hello requis par la requête hello, tels que les objets périphériques double ou de travail, ou brut JSON toobe utilisé lors de l’utilisation de projections.

### <a name="nodejs-example"></a>Exemple de Node.js
fonctionnalités de requête Hello sont exposée par hello [Azure IoT service SDK pour Node.js] [ lnk-hub-sdks] Bonjour **Registre** objet.
Voici un exemple de requête simple :

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

Notez comment hello **requête** objet est instancié avec une taille de page (haut too1000), et puis plusieurs pages peuvent être récupérés en appelant hello **nextAsTwin** méthodes plusieurs fois.
Notez que cet objet de requête hello expose plusieurs **suivant\***, selon l’option de la désérialisation de hello requis par la requête hello, tels que les objets périphériques double ou de travail, ou brut JSON toobe utilisé lors de l’utilisation de projections.

### <a name="limitations"></a>Limites
> [!IMPORTANT]
> Résultats de la requête peuvent contenir quelques minutes de retard avec les valeurs les plus récentes en ce qui concerne toohello jumeaux de périphérique. Si vous interrogez jumeaux de périphérique par id, il est toujours préférable toouse hello récupérer les API de double de l’appareil, qui contient les valeurs les plus récentes hello et a plus la limitation limites toujours.

Actuellement, les comparaisons ne sont prises en charge qu’entre types primitifs (aucun objet), par exemple `... WHERE properties.desired.config = properties.reported.config` est pris en charge uniquement si ces propriétés ont des valeurs primitives.

## <a name="get-started-with-jobs-queries"></a>Bien démarrer avec les requêtes de travaux
[Travaux] [ lnk-jobs] fournissent un moyen tooexecute des opérations sur des ensembles de périphériques. Chaque double périphérique contient des informations de hello de travaux hello dont il fait partie d’une collection appelée **travaux**.
Sous forme logique,

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

Actuellement, cette collection ne peut être interrogée comme **devices.jobs** Bonjour langage de requête IoT Hub.

> [!IMPORTANT]
> Actuellement, propriété des travaux hello n’est jamais retournée lors de l’interrogation jumeaux d’appareil (autrement dit, les requêtes qui contient « à partir d’appareils »). Elle est uniquement accessible directement avec des requêtes utilisant `FROM devices.jobs`.
>
>

Par exemple, tooget tous les travaux (passées et planifiées) qui affectent un seul appareil, vous pouvez utiliser hello suivant la requête :

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

Notez comment cette requête fournit l’état de spécifique au périphérique hello (et éventuellement réponse de la méthode directe hello) de chaque tâche retournée.
Il est également possible de toofilter avec des conditions booléennes arbitraires sur toutes les propriétés de l’objet Bonjour **devices.jobs** collection.
Par exemple, hello requête suivante :

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

récupère tous les travaux de mise à jour du jumeau de l’appareil **myDeviceId**, qui ont été créés après le mois de septembre 2016.

Il est également des résultats de chaque appareil hello tooretrieve possibles d’une tâche unique.

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a>Limites
Actuellement, les requêtes sur **devices.jobs** ne prennent pas en charge :

* Les projections, par conséquent seul `SELECT *` est possible.
* Conditions qui font référence à double d’appareil toohello dans les propriétés de toojob d’addition (voir hello précédant la section).
* L’exécution d’agrégations, par exemple, count, avg, group by.

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a>Bien démarrer avec les expressions de requête d’itinéraires de messages appareil-à-cloud

À l’aide de [appareil-à-cloud itinéraires][lnk-devguide-messaging-routes], vous pouvez configurer IoT Hub toodispatch appareil-à-cloud messages toodifferent de points de terminaison basé sur des expressions évaluées par rapport à des messages individuels.

itinéraire de Hello [condition] [ lnk-query-expressions] utilise hello même langage de requête IoT Hub en tant que les conditions dans les requêtes double et de travail. Conditions de routage sont évaluées sur le corps et en-têtes de message hello. Votre expression de requête de routage peut impliquer seulement des en-têtes de message, uniquement hello corps du message, ou les deux en-têtes de message et le corps du message. IoT Hub suppose un schéma spécifique pour les en-têtes de hello et de corps du message dans les messages d’ordre tooroute et hello les sections suivantes décrire ce qui est obligatoire pour l’itinéraire de tooproperly IoT Hub :

### <a name="routing-on-message-headers"></a>Routage sur les en-têtes de message

IoT Hub suppose hello suivant la représentation JSON d’en-têtes de message pour le routage des messages :

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

Propriétés des messages système sont précédées de hello `'$'` symbole.
Les propriétés de l’utilisateur sont toujours accessibles par leur nom. Si un nom de propriété utilisateur produit toocoincide avec une propriété système (tel que `$to`), propriété hello de l’utilisateur est récupérée avec hello `$to` expression.
Vous pouvez toujours accéder à l’aide de crochets de la propriété du système hello `{}`: par exemple, vous pouvez utiliser l’expression de hello `{$to}` tooaccess hello propriété système `to`. Noms de propriété entre crochets récupèrent toujours le propriété système correspondante de hello.

N’oubliez pas que les noms de propriété respectent la casse.

> [!NOTE]
> Toutes les propriétés de message sont des chaînes. Propriétés du système, comme décrit dans hello [guide du développeur][lnk-devguide-messaging-format], ne sont pas actuellement disponible toouse dans les requêtes.
>

Par exemple, si vous utilisez un `messageType` propriété, vous pourriez tooroute le point de terminaison de tooone toutes les données de télémétrie et le point de terminaison de tooanother toutes les alertes. Vous pouvez écrire hello suivant de télémétrie de hello tooroute expression :

```sql
messageType = 'telemetry'
```

Et hello suivant des messages d’alerte hello tooroute expression :

```sql
messageType = 'alert'
```

Les fonctions et expressions booléennes sont également prises en charge. Cette fonctionnalité permet de vous toodistinguish entre le niveau de gravité, par exemple :

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

Consultez toohello [Expression et conditions] [ lnk-query-expressions] section pour la liste complète hello des fonctions et opérateurs pris en charge.

### <a name="routing-on-message-bodies"></a>Routage sur les corps de message

IoT Hub peut uniquement acheminer basé sur le corps du message contenu si le corps du message hello est correctement formé JSON encodé en UTF-8, UTF-16 ou UTF-32. Vous devez définir les type de contenu hello de message de type hello trop`application/json` et tooone de codage contenu hello Hello pris en charge les encodages UTF dans tooallow d’en-têtes de message hello message de type hello IoT Hub tooroute basé sur le contenu du corps de hello. Si un des en-têtes de hello n’est pas spécifié, IoT Hub tentera pas tooevaluate toute expression de requête impliquant des corps hello contre le message de type hello. Si votre message n’est pas un message JSON, ou si le message de type hello ne spécifie pas de type de contenu hello et l’encodage du contenu, vous pouvez toujours utiliser le message de type hello tooroute basée sur les en-têtes de message hello de routage des messages.

Vous pouvez utiliser `$body` dans le message de type hello tooroute expression requête hello. Vous pouvez utiliser une référence simple corps, référence de tableau de corps ou plusieurs références de corps dans l’expression de requête hello. Votre expression de requête peut également combiner une référence de corps avec une référence d’en-tête de message. Par exemple, hello Voici toutes les expressions de requête valide :

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a>Principes de base d’une requête IoT Hub
Chaque requête IoT Hub se compose de clauses SELECT et FROM et, en option, de clauses WHERE et GROUP BY. Chaque requête est exécutée sur un regroupement de documents JSON, par exemple des jumeaux d’appareil. clause FROM de Hello indique hello document collection toobe itéré sur (**périphériques** ou **devices.jobs**). Ensuite, hello filtre Bonjour où clause est appliquée. Avec des agrégations, les résultats de hello de cette étape sont regroupés comme spécifié dans hello clause GROUP BY et, pour chaque groupe, une ligne est générée comme spécifié dans la clause SELECT de hello.

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a>Clause FROM
Hello **à partir de < from_specification >** clause peut supposer que deux valeurs : **à partir d’appareils**, tooquery jumeaux de périphérique, ou **de devices.jobs**, par périphérique du travail tooquery Détails.

## <a name="where-clause"></a>Clause WHERE
Hello **où < filter_condition >** clause est facultative. Elle spécifie une ou plusieurs des conditions que les documents JSON hello dans la collection de FROM hello doivent satisfaire toobe inclus en tant que partie du résultat de hello. N’importe quel document JSON doit évaluer hello spécifié conditions trop « true » toobe inclus dans le résultat de hello.

Hello autorisés sont décrites dans la section [Expressions et les conditions][lnk-query-expressions].

## <a name="select-clause"></a>Clause SELECT
clause SELECT de Hello (**sélectionnez < select_list >**) est obligatoire et spécifie que les valeurs sont récupérées à partir de la requête de hello. Il spécifie toobe de valeurs JSON hello utilisé toogenerate de nouveaux objets JSON.
Pour chaque élément de hello sous-ensemble filtré (et éventuellement groupée) de collection de FROM hello, la phase de projection hello génère un nouvel objet JSON, construit avec les valeurs hello spécifiés dans la clause SELECT de hello.

Voici la grammaire hello de la clause SELECT de hello :

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

où **attribute_name** fait référence de propriété tooany document JSON de hello dans la collection de FROM hello. Vous trouverez des exemples de clauses SELECT Bonjour [mise en route avec les requêtes de double périphérique] [ lnk-query-getstarted] section.

Actuellement, les clauses de sélection autres que **SELECT\*** sont prises en charge uniquement dans les requêtes d’agrégation sur des jumeaux d’appareil.

## <a name="group-by-clause"></a>Clause GROUP BY
Hello **GROUP BY < group_specification >** clause est une étape facultative qui peut être exécutée une fois que le filtre de hello spécifié Bonjour clause WHERE et avant de projection hello spécifiée dans hello sélectionner. Il regroupe des documents en fonction de la valeur hello d’un attribut. Ces groupes sont utilisés toogenerate agrégée des valeurs comme spécifié dans la clause SELECT de hello.

Voici un exemple de requête utilisant la clause GROUP BY :

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

une syntaxe de Hello pour GROUP BY est la suivante :

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

où **attribute_name** fait référence de propriété tooany document JSON de hello dans la collection de FROM hello.

Actuellement, clause GROUP BY hello est uniquement pris en charge lors de l’interrogation jumeaux de périphérique.

## <a name="expressions-and-conditions"></a>Expressions et conditions
À un niveau élevé, une *expression* :

* Évalue l’instance tooan d’un type JSON (par exemple, les booléen, nombre, chaîne, tableau ou objet), et
* Est défini par la manipulation de données provenant d’un document JSON de périphérique hello et constantes à l’aide des fonctions et opérateurs intégrés.

*Conditions* sont des expressions qui évaluent tooa booléen. N’importe quelle autre qu’une valeur booléenne de constante **true** est considéré comme **false** (y compris **null**, **non défini**, n’importe quelle instance d’objet ou un tableau, toute chaîne et clairement hello booléen **false**).

syntaxe des expressions de Hello est la suivante :

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

où :

| Symbole | Définition |
| --- | --- |
| attribute_name | N’importe quelle propriété de document JSON de hello Bonjour **FROM** collection. |
| binary_operator | Tout opérateur binaire répertoriés dans hello [opérateurs](#operators) section. |
| function_name| Toutes les fonctions répertoriées dans hello [fonctions](#functions) section. |
| decimal_literal |Variable exprimée en notation décimale. |
| hexadecimal_literal |Un nombre exprimé par la chaîne de hello '0 x' suivi d’une chaîne de chiffres hexadécimaux. |
| string_literal |Les littéraux de chaîne sont des chaînes Unicode représentées par une séquence de zéro ou plusieurs caractères Unicode ou séquences d’échappement. Les littéraux de chaîne sont placés entre guillemets simples (apostrophes, ’) ou guillemets doubles ("). Échappements autorisés : `\'`, `\"`, `\\`, `\uXXXX` pour les caractères Unicode définis par 4 chiffres hexadécimaux. |

### <a name="operators"></a>Operators
Hello après les opérateurs est pris en charge :

| Famille | Opérateurs |
| --- | --- |
| Opérateurs arithmétiques |+,-,*,/,% |
| Opérateurs logiques |AND, OR, NOT |
| Opérateurs de comparaison |=, !=, <, >, <=, >=, <> |

### <a name="functions"></a>Fonctions
Lors de l’interrogation hello jumeaux et tâches de prise en charge uniquement la fonction est :

| Fonction | Description |
| -------- | ----------- |
| IS_DEFINED(property) | Retourne une valeur booléenne indiquant si une valeur a été assignée à la propriété de hello (y compris `null`). |

Dans les conditions d’itinéraires, hello suivant des fonctions mathématiques est prises en charge :

| Fonction | Description |
| -------- | ----------- |
| ABS(x) | Retourne hello valeur absolue (positive) de hello de l’expression numérique spécifiée. |
| EXP(x) | Retourne la valeur exponentielle hello Hello de l’expression numérique spécifiée (e ^ x). |
| POWER(x,y) | Retourne hello valeur Hello spécifié toohello de l’expression spécifiée d’alimentation (x ^ y).|
| SQUARE(x) | Hello retourne carrée hello la valeur numérique spécifiée. |
| CEILING(x) | Retourne hello plus petit entier supérieur à, ou être égal, hello expression numérique spécifiée. |
| FLOOR(x) | Retourne des hello plus grand entier inférieur ou égal toohello l’expression numérique spécifiée. |
| SIGN(x) | Retourne hello positif (+ 1), zéro (0), ou un signe négatif (-1) de hello de l’expression numérique spécifiée.|
| SQRT(x) | Hello retourne carrée hello la valeur numérique spécifiée. |

Dans les conditions d’itinéraires, hello suivant le type de vérification et de la conversion des fonctions est prises en charge :

| Fonction | Description |
| -------- | ----------- |
| AS_NUMBER | Convertit le nombre de tooa hello chaîne d’entrée. `noop` si l’entrée est un nombre ; `Undefined` si la chaîne ne représente pas un nombre.|
| IS_ARRAY | Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est un tableau. |
| IS_BOOL | Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est une valeur booléenne. |
| IS_DEFINED | Retourne une valeur booléenne indiquant si une valeur a été assignée à la propriété de hello. |
| IS_NULL | Retourne une valeur booléenne indiquant si le type hello Hello spécifié expression est null. |
| IS_NUMBER | Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est un nombre. |
| IS_OBJECT | Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est un objet JSON. |
| IS_PRIMITIVE | Retourne une valeur booléenne indiquant si le type hello Hello spécifié expression est un type primitif (chaîne, booléen, numérique ou `null`). |
| IS_STRING | Retourne une valeur booléenne indiquant si type hello Hello l’expression spécifiée est une chaîne. |

Dans les conditions d’itinéraires, hello suivant des fonctions de chaîne est pris en charge :

| Fonction | Description |
| -------- | ----------- |
| CONCAT(x, …) | Retourne une chaîne qui est le résultat de hello de la concaténation de deux ou plusieurs valeurs de chaîne. |
| LENGTH(x) | Retourne hello nombre de caractères de hello spécifié l’expression de chaîne.|
| LOWER(x) | Retourne une expression de chaîne après la conversion de toolowercase de données de caractères majuscules en caractères. |
| UPPER(x) | Retourne une expression de chaîne après la conversion de toouppercase de données de caractères en minuscules. |
| SUBSTRING(string, start [, length]) | Retourne dans une expression de chaîne commençant à hello spécifié le caractère de base zéro et continue toohello spécifié longueur, ou à la fin de toohello de chaîne de hello. |
| INDEX_OF(string, fragment) | Retourne hello position de départ des hello première occurrence de hello deuxième expression de chaîne hello première expression de chaîne spécifiée, ou -1 si la chaîne de hello est introuvable.|
| STARTS_WITH(x, y) | Retourne une valeur booléenne indiquant si les première expression de chaîne hello commence par hello ensuite. |
| ENDS_WITH(x, y) | Retourne une valeur booléenne indiquant si les première expression de chaîne hello se termine ensuite par hello. |
| CONTAINS(x,y) | Retourne une valeur booléenne qui indique si le première expression de chaîne hello contient hello ensuite. |

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment tooexecute les requêtes dans vos applications à l’aide de [kits de développement logiciel Azure IoT][lnk-hub-sdks].

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
