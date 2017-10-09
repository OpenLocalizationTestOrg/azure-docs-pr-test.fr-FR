---
title: types de contenu aaaHandle - Azure Logic Apps | Documents Microsoft
description: "Découvrir comment les applications logiques gèrent les types de contenu au moment de la conception et de l’exécution"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: cd1f08fd-8cde-4afc-86ff-2e5738cc8288
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a823249c5388b15ae0aae450b40499b420ea005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="handle-content-types-in-logic-apps"></a>Gérer les types de contenu dans les applications logiques

De nombreux types de contenu peuvent transiter par une application logique, notamment les données binaires, les fichiers plats, ainsi que les contenus XML et JSON. Hello logique applications moteur prend en charge tous les types de contenu, certaines sont compris en mode natif par hello logique applications moteur. D’autres peuvent nécessiter un transtypage ou des conversions en fonction des besoins. Cet article décrit comment le moteur de hello gère les différents types de contenu et comment toocorrectly gérer ces types lorsque cela est nécessaire.

## <a name="content-type-header"></a>Entête Content-Type

toostart en fait, nous allons voir hello deux `Content-Types` ne nécessitant une conversion de que vous pouvez utiliser dans une application de logique : `application/json` et `text/plain`.

## <a name="applicationjson"></a>Application/JSON

moteur de flux de travail Hello s’appuie sur hello `Content-Type` en-tête HTTP appelle la gestion appropriée toodetermine hello. Une demande dont le type de contenu hello `application/json` est stocké et géré en tant qu’objet JSON. Le contenu JSON peut également être analysé par défaut sans subir de transtypage. 

Par exemple, Impossible d’analyser une requête comportant un en-tête de type de contenu hello `application/json ` dans un flux de travail à l’aide d’une expression telle que `@body('myAction')['foo'][0]` valeur hello de tooget `bar` dans ce cas :

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

Aucun transtypage supplémentaire n’est nécessaire. Si vous travaillez avec des données qui sont JSON mais ne comportait un en-tête spécifié, vous pouvez manuellement convertir tooJSON à l’aide de hello `@json()` de fonction, par exemple : `@json(triggerBody())['foo']`.

### <a name="schema-and-schema-generator"></a>Schéma et générateur de schéma

Hello déclencheur de la demande vous permet de tooenter un schéma JSON pour la charge utile de hello souhaitées tooreceive. Ce schéma permet de générer des jetons donc vous pouvez consommer du contenu hello de demande de hello Concepteur de hello. Si vous n’avez pas un schéma prêt, sélectionnez **utilisez exemple charge utile toogenerate de schéma**, de sorte que vous pouvez générer un schéma JSON à partir d’une charge utile d’exemple.

![Schéma](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a>Action d’analyse JSON

Hello `Parse JSON` action vous permet d’analyser le contenu JSON en jetons conviviales pour la consommation d’application logique. Déclencheur de demande toohello similaire, cette action vous permet d’entrer ou de générer un schéma JSON pour hello contenu que vous souhaitez tooparse. Cet outil facilite l’utilisation des données de Service Bus, Azure Cosmos DB, etc.

![Analyse JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a>Text/plain

Similaire trop`application/json`, les messages HTTP reçus par hello `Content-Type` en-tête de `text/plain` sont stockées dans sous la forme brute. En outre, si ces messages sont inclus dans les actions suivantes sans transtypage, ces demandes sortent avec l’en-tête`Content-Type` : `text/plain`. Par exemple, lorsque vous travaillez avec un fichier plat, vous pouvez obtenir ce contenu HTTP en tant que `text/plain` :

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

Si dans l’action suivante de hello, vous envoyez la demande de hello en tant que corps hello d’une autre demande (`@body('flatfile')`), demande de hello aurait un `text/plain` en-tête Content-Type. Si vous travaillez avec des données qui sont du texte brut mais ne comportait un en-tête spécifié, vous pouvez manuellement effectuer un cast hello tootext de données à l’aide de hello `@string()` de fonction, par exemple : `@string(triggerBody())`.

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a>Application/xml, Application/octet-stream et fonctions de conversion

Hello logique applications moteur conserve toujours hello `Content-Type` qui a été reçu sur hello HTTP demande ou réponse. Par conséquent, si le moteur de hello reçoit du contenu avec hello `Content-Type` de `application/octet-stream`, et que vous incluez le contenu dans des actions suivantes sans cast, la demande sortante hello que `Content-Type`: `application/octet-stream`. De cette manière, le moteur de hello peut garantir données ne sont pas perdues lors du déplacement de flux de travail hello. Toutefois, l’état d’action hello (entrées et sorties) est stockée dans un objet JSON comme hello état parcourt les flux de travail hello. Par conséquent, toopreserve certains types de données, le moteur de hello convertit hello chaîne binary base64 encodé de contenu tooa avec les métadonnées appropriées qui conserve les deux `$content` et `$content-type`, qui sont automatiquement être convertis. 

* `@json()`-Convertit trop de données`application/json`
* `@xml()`-Convertit trop de données`application/xml`
* `@binary()`-Convertit trop de données`application/octet-stream`
* `@string()`-Convertit trop de données`text/plain`
* `@base64()`-Convertit la chaîne en base64 tooa contenu
* `@base64toString()`-Convertit une chaîne codée en base64 trop`text/plain`
* `@base64toBinary()`-Convertit une chaîne codée en base64 trop`application/octet-stream`
* `@encodeDataUri()` : encode une chaîne en tableau d’octets dataUri
* `@decodeDataUri()` : décode un dataUri en tableau d’octets

Par exemple, si vous recevez une demande HTTP avec `Content-Type` : `application/xml` :

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

Vous pouvez appliquer un transtypage et utiliser le résultat ultérieurement avec, par exemple, `@xml(triggerBody())` ou dans une fonction comme `@xpath(xml(triggerBody()), '/CustomerName')`.

## <a name="other-content-types"></a>Autres types de contenu

Autres types de contenu sont pris en charge et fonctionne avec les applications de la logique, mais peut nécessiter le corps du message hello manuellement lors de la récupération par le décodage hello `$content`. Par exemple, supposons que vous déclenchez une `application/x-www-url-formencoded` demander où `$content` est la charge utile de hello encodé sous la forme d’un toopreserve de chaîne base64 toutes les données :

```
CustomerName=Frank&Address=123+Avenue
```

Étant donné que la demande de hello n’est pas en texte brut ou JSON, demande de hello est stockée dans l’action de hello comme suit :

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Actuellement, il n’est pas une fonction native pour les données de formulaire, donc vous pouvez toujours utiliser ces données dans un flux de travail par manuellement l’accès aux données de hello avec une fonction comme `@string(body('formdataAction'))`. Si vous souhaitiez hello demande sortante tooalso ont hello `application/x-www-url-formencoded` en-tête du type de contenu, vous pouvez ajouter des corps d’action hello demande toohello sans conversion comme `@body('formdataAction')`. Toutefois, cette méthode fonctionne uniquement si les corps hello sont hello seul paramètre dans hello `body` d’entrée. Si vous essayez de toouse `@body('formdataAction')` dans un `application/json` demande, vous obtenez une erreur d’exécution, car le corps de hello encodé est envoyé.

