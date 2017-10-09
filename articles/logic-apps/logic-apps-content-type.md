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
# <a name="handle-content-types-in-logic-apps"></a><span data-ttu-id="46c91-103">Gérer les types de contenu dans les applications logiques</span><span class="sxs-lookup"><span data-stu-id="46c91-103">Handle content types in logic apps</span></span>

<span data-ttu-id="46c91-104">De nombreux types de contenu peuvent transiter par une application logique, notamment les données binaires, les fichiers plats, ainsi que les contenus XML et JSON.</span><span class="sxs-lookup"><span data-stu-id="46c91-104">Many different types of content can flow through a logic app, including JSON, XML, flat files, and binary data.</span></span> <span data-ttu-id="46c91-105">Hello logique applications moteur prend en charge tous les types de contenu, certaines sont compris en mode natif par hello logique applications moteur.</span><span class="sxs-lookup"><span data-stu-id="46c91-105">While hello Logic Apps Engine supports all content types, some are natively understood by hello Logic Apps Engine.</span></span> <span data-ttu-id="46c91-106">D’autres peuvent nécessiter un transtypage ou des conversions en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="46c91-106">Others might require casting or conversions as necessary.</span></span> <span data-ttu-id="46c91-107">Cet article décrit comment le moteur de hello gère les différents types de contenu et comment toocorrectly gérer ces types lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="46c91-107">This article describes how hello engine handles different content types and how toocorrectly handle these types when necessary.</span></span>

## <a name="content-type-header"></a><span data-ttu-id="46c91-108">Entête Content-Type</span><span class="sxs-lookup"><span data-stu-id="46c91-108">Content-Type Header</span></span>

<span data-ttu-id="46c91-109">toostart en fait, nous allons voir hello deux `Content-Types` ne nécessitant une conversion de que vous pouvez utiliser dans une application de logique : `application/json` et `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="46c91-109">toostart basically, let's look at hello two `Content-Types` that don't require conversion or casting that you can use in a logic app: `application/json` and `text/plain`.</span></span>

## <a name="applicationjson"></a><span data-ttu-id="46c91-110">Application/JSON</span><span class="sxs-lookup"><span data-stu-id="46c91-110">Application/JSON</span></span>

<span data-ttu-id="46c91-111">moteur de flux de travail Hello s’appuie sur hello `Content-Type` en-tête HTTP appelle la gestion appropriée toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="46c91-111">hello workflow engine relies on hello `Content-Type` header from HTTP calls toodetermine hello appropriate handling.</span></span> <span data-ttu-id="46c91-112">Une demande dont le type de contenu hello `application/json` est stocké et géré en tant qu’objet JSON.</span><span class="sxs-lookup"><span data-stu-id="46c91-112">Any request with hello content type `application/json` is stored and handled as a JSON Object.</span></span> <span data-ttu-id="46c91-113">Le contenu JSON peut également être analysé par défaut sans subir de transtypage.</span><span class="sxs-lookup"><span data-stu-id="46c91-113">Also, JSON content can be parsed by default without needing any casting.</span></span> 

<span data-ttu-id="46c91-114">Par exemple, Impossible d’analyser une requête comportant un en-tête de type de contenu hello `application/json ` dans un flux de travail à l’aide d’une expression telle que `@body('myAction')['foo'][0]` valeur hello de tooget `bar` dans ce cas :</span><span class="sxs-lookup"><span data-stu-id="46c91-114">For example, you could parse a request that has hello content type header `application/json ` in a workflow by using an expression like `@body('myAction')['foo'][0]` tooget hello value `bar` in this case:</span></span>

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

<span data-ttu-id="46c91-115">Aucun transtypage supplémentaire n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="46c91-115">No additional casting is needed.</span></span> <span data-ttu-id="46c91-116">Si vous travaillez avec des données qui sont JSON mais ne comportait un en-tête spécifié, vous pouvez manuellement convertir tooJSON à l’aide de hello `@json()` de fonction, par exemple : `@json(triggerBody())['foo']`.</span><span class="sxs-lookup"><span data-stu-id="46c91-116">If you are working with data that is JSON but didn't have a header specified, you can manually cast it tooJSON using hello `@json()` function, for example: `@json(triggerBody())['foo']`.</span></span>

### <a name="schema-and-schema-generator"></a><span data-ttu-id="46c91-117">Schéma et générateur de schéma</span><span class="sxs-lookup"><span data-stu-id="46c91-117">Schema and schema generator</span></span>

<span data-ttu-id="46c91-118">Hello déclencheur de la demande vous permet de tooenter un schéma JSON pour la charge utile de hello souhaitées tooreceive.</span><span class="sxs-lookup"><span data-stu-id="46c91-118">hello Request trigger lets you tooenter a JSON schema for hello payload you expect tooreceive.</span></span> <span data-ttu-id="46c91-119">Ce schéma permet de générer des jetons donc vous pouvez consommer du contenu hello de demande de hello Concepteur de hello.</span><span class="sxs-lookup"><span data-stu-id="46c91-119">This schema lets hello designer generate tokens so you can consume hello content of hello request.</span></span> <span data-ttu-id="46c91-120">Si vous n’avez pas un schéma prêt, sélectionnez **utilisez exemple charge utile toogenerate de schéma**, de sorte que vous pouvez générer un schéma JSON à partir d’une charge utile d’exemple.</span><span class="sxs-lookup"><span data-stu-id="46c91-120">If you don't have a schema ready, select **Use sample payload toogenerate schema**, so you can generate a JSON schema from a sample payload.</span></span>

![Schéma](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a><span data-ttu-id="46c91-122">Action d’analyse JSON</span><span class="sxs-lookup"><span data-stu-id="46c91-122">'Parse JSON' action</span></span>

<span data-ttu-id="46c91-123">Hello `Parse JSON` action vous permet d’analyser le contenu JSON en jetons conviviales pour la consommation d’application logique.</span><span class="sxs-lookup"><span data-stu-id="46c91-123">hello `Parse JSON` action lets you parse JSON content into friendly tokens for logic app consumption.</span></span> <span data-ttu-id="46c91-124">Déclencheur de demande toohello similaire, cette action vous permet d’entrer ou de générer un schéma JSON pour hello contenu que vous souhaitez tooparse.</span><span class="sxs-lookup"><span data-stu-id="46c91-124">Similar toohello Request trigger, this action lets you enter or generate a JSON schema for hello content you want tooparse.</span></span> <span data-ttu-id="46c91-125">Cet outil facilite l’utilisation des données de Service Bus, Azure Cosmos DB, etc.</span><span class="sxs-lookup"><span data-stu-id="46c91-125">This tool makes consuming data from Service Bus, Azure Cosmos DB, and so on, much easier.</span></span>

![Analyse JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a><span data-ttu-id="46c91-127">Text/plain</span><span class="sxs-lookup"><span data-stu-id="46c91-127">Text/plain</span></span>

<span data-ttu-id="46c91-128">Similaire trop`application/json`, les messages HTTP reçus par hello `Content-Type` en-tête de `text/plain` sont stockées dans sous la forme brute.</span><span class="sxs-lookup"><span data-stu-id="46c91-128">Similar too`application/json`, HTTP messages received with hello `Content-Type` header of `text/plain` are stored in raw form.</span></span> <span data-ttu-id="46c91-129">En outre, si ces messages sont inclus dans les actions suivantes sans transtypage, ces demandes sortent avec l’en-tête`Content-Type` : `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="46c91-129">Also, if those messages are included in subsequent actions without casting, those requests go out with  `Content-Type`: `text/plain` header.</span></span> <span data-ttu-id="46c91-130">Par exemple, lorsque vous travaillez avec un fichier plat, vous pouvez obtenir ce contenu HTTP en tant que `text/plain` :</span><span class="sxs-lookup"><span data-stu-id="46c91-130">For example, when working with a flat file, you might get this HTTP content as `text/plain`:</span></span>

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

<span data-ttu-id="46c91-131">Si dans l’action suivante de hello, vous envoyez la demande de hello en tant que corps hello d’une autre demande (`@body('flatfile')`), demande de hello aurait un `text/plain` en-tête Content-Type.</span><span class="sxs-lookup"><span data-stu-id="46c91-131">If in hello next action, you send hello request as hello body of another request (`@body('flatfile')`), hello request would have a `text/plain` Content-Type header.</span></span> <span data-ttu-id="46c91-132">Si vous travaillez avec des données qui sont du texte brut mais ne comportait un en-tête spécifié, vous pouvez manuellement effectuer un cast hello tootext de données à l’aide de hello `@string()` de fonction, par exemple : `@string(triggerBody())`.</span><span class="sxs-lookup"><span data-stu-id="46c91-132">If you are working with data that is plain text but didn't have a header specified, you can manually cast hello data tootext using hello `@string()` function, for example: `@string(triggerBody())`.</span></span>

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a><span data-ttu-id="46c91-133">Application/xml, Application/octet-stream et fonctions de conversion</span><span class="sxs-lookup"><span data-stu-id="46c91-133">Application/xml and Application/octet-stream and converter functions</span></span>

<span data-ttu-id="46c91-134">Hello logique applications moteur conserve toujours hello `Content-Type` qui a été reçu sur hello HTTP demande ou réponse.</span><span class="sxs-lookup"><span data-stu-id="46c91-134">hello Logic Apps Engine always preserves hello `Content-Type` that was received on hello HTTP request or response.</span></span> <span data-ttu-id="46c91-135">Par conséquent, si le moteur de hello reçoit du contenu avec hello `Content-Type` de `application/octet-stream`, et que vous incluez le contenu dans des actions suivantes sans cast, la demande sortante hello que `Content-Type`: `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="46c91-135">So if hello engine receives content with hello `Content-Type` of `application/octet-stream`, and you include that content in a subsequent action without casting, hello outgoing request has `Content-Type`: `application/octet-stream`.</span></span> <span data-ttu-id="46c91-136">De cette manière, le moteur de hello peut garantir données ne sont pas perdues lors du déplacement de flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="46c91-136">This way, hello engine can guarantee data isn't lost while moving through hello workflow.</span></span> <span data-ttu-id="46c91-137">Toutefois, l’état d’action hello (entrées et sorties) est stockée dans un objet JSON comme hello état parcourt les flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="46c91-137">However, hello action state (inputs and outputs) is stored in a JSON object as hello state moves through hello workflow.</span></span> <span data-ttu-id="46c91-138">Par conséquent, toopreserve certains types de données, le moteur de hello convertit hello chaîne binary base64 encodé de contenu tooa avec les métadonnées appropriées qui conserve les deux `$content` et `$content-type`, qui sont automatiquement être convertis.</span><span class="sxs-lookup"><span data-stu-id="46c91-138">So toopreserve some data types, hello engine converts hello content tooa binary base64 encoded string with appropriate metadata that preserves both `$content` and `$content-type`, which are automatically be converted.</span></span> 

* <span data-ttu-id="46c91-139">`@json()`-Convertit trop de données`application/json`</span><span class="sxs-lookup"><span data-stu-id="46c91-139">`@json()` - casts data too`application/json`</span></span>
* <span data-ttu-id="46c91-140">`@xml()`-Convertit trop de données`application/xml`</span><span class="sxs-lookup"><span data-stu-id="46c91-140">`@xml()` - casts data too`application/xml`</span></span>
* <span data-ttu-id="46c91-141">`@binary()`-Convertit trop de données`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="46c91-141">`@binary()` - casts data too`application/octet-stream`</span></span>
* <span data-ttu-id="46c91-142">`@string()`-Convertit trop de données`text/plain`</span><span class="sxs-lookup"><span data-stu-id="46c91-142">`@string()` - casts data too`text/plain`</span></span>
* <span data-ttu-id="46c91-143">`@base64()`-Convertit la chaîne en base64 tooa contenu</span><span class="sxs-lookup"><span data-stu-id="46c91-143">`@base64()` - converts content tooa base64 string</span></span>
* <span data-ttu-id="46c91-144">`@base64toString()`-Convertit une chaîne codée en base64 trop`text/plain`</span><span class="sxs-lookup"><span data-stu-id="46c91-144">`@base64toString()` - converts a base64 encoded string too`text/plain`</span></span>
* <span data-ttu-id="46c91-145">`@base64toBinary()`-Convertit une chaîne codée en base64 trop`application/octet-stream`</span><span class="sxs-lookup"><span data-stu-id="46c91-145">`@base64toBinary()` - converts a base64 encoded string too`application/octet-stream`</span></span>
* <span data-ttu-id="46c91-146">`@encodeDataUri()` : encode une chaîne en tableau d’octets dataUri</span><span class="sxs-lookup"><span data-stu-id="46c91-146">`@encodeDataUri()` - encodes a string as a dataUri byte array</span></span>
* <span data-ttu-id="46c91-147">`@decodeDataUri()` : décode un dataUri en tableau d’octets</span><span class="sxs-lookup"><span data-stu-id="46c91-147">`@decodeDataUri()` - decodes a dataUri into a byte array</span></span>

<span data-ttu-id="46c91-148">Par exemple, si vous recevez une demande HTTP avec `Content-Type` : `application/xml` :</span><span class="sxs-lookup"><span data-stu-id="46c91-148">For example, if you received an HTTP request with `Content-Type`: `application/xml`:</span></span>

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

<span data-ttu-id="46c91-149">Vous pouvez appliquer un transtypage et utiliser le résultat ultérieurement avec, par exemple, `@xml(triggerBody())` ou dans une fonction comme `@xpath(xml(triggerBody()), '/CustomerName')`.</span><span class="sxs-lookup"><span data-stu-id="46c91-149">You could cast and use later with something like `@xml(triggerBody())`, or in a function like `@xpath(xml(triggerBody()), '/CustomerName')`.</span></span>

## <a name="other-content-types"></a><span data-ttu-id="46c91-150">Autres types de contenu</span><span class="sxs-lookup"><span data-stu-id="46c91-150">Other content types</span></span>

<span data-ttu-id="46c91-151">Autres types de contenu sont pris en charge et fonctionne avec les applications de la logique, mais peut nécessiter le corps du message hello manuellement lors de la récupération par le décodage hello `$content`.</span><span class="sxs-lookup"><span data-stu-id="46c91-151">Other content types are supported and work with logic apps, but might require manually retrieving hello message body by decoding hello `$content`.</span></span> <span data-ttu-id="46c91-152">Par exemple, supposons que vous déclenchez une `application/x-www-url-formencoded` demander où `$content` est la charge utile de hello encodé sous la forme d’un toopreserve de chaîne base64 toutes les données :</span><span class="sxs-lookup"><span data-stu-id="46c91-152">For example, suppose you trigger an `application/x-www-url-formencoded` request where `$content` is hello payload encoded as a base64 string toopreserve all data:</span></span>

```
CustomerName=Frank&Address=123+Avenue
```

<span data-ttu-id="46c91-153">Étant donné que la demande de hello n’est pas en texte brut ou JSON, demande de hello est stockée dans l’action de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="46c91-153">Because hello request isn't plain text or JSON, hello request is stored in hello action as follows:</span></span>

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Actuellement, il n’est pas une fonction native pour les données de formulaire, donc vous pouvez toujours utiliser ces données dans un flux de travail par manuellement l’accès aux données de hello avec une fonction comme `@string(body('formdataAction'))`. Si vous souhaitiez hello demande sortante tooalso ont hello `application/x-www-url-formencoded` en-tête du type de contenu, vous pouvez ajouter des corps d’action hello demande toohello sans conversion comme `@body('formdataAction')`. Toutefois, cette méthode fonctionne uniquement si les corps hello sont hello seul paramètre dans hello `body` d’entrée. <span data-ttu-id="46c91-157">Si vous essayez de toouse `@body('formdataAction')` dans un `application/json` demande, vous obtenez une erreur d’exécution, car le corps de hello encodé est envoyé.</span><span class="sxs-lookup"><span data-stu-id="46c91-157">If you try toouse `@body('formdataAction')` in an `application/json` request, you get a runtime error because hello encoded body is sent.</span></span>

