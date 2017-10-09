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
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="75587-104">Fonctions JavaScript définies par l’utilisateur Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="75587-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="75587-105">Azure Stream Analytics prend en charge les fonctions définies par l’utilisateur écrites en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="75587-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="75587-106">Série de hello **chaîne**, **RegExp**, **mathématiques**, **tableau**, et **Date** méthodes qui JavaScript fournit, les transformations de données complexes avec des tâches de flux de données Analytique deviennent toocreate plus facile.</span><span class="sxs-lookup"><span data-stu-id="75587-106">With hello rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier toocreate.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="75587-107">Fonctions JavaScript définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="75587-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="75587-108">Les fonctions JavaScript définies par l’utilisateur prennent en charge les fonctions scalaires de calcul pur sans état qui ne nécessitent pas de connectivité externe.</span><span class="sxs-lookup"><span data-stu-id="75587-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="75587-109">Hello retournent la valeur d’une fonction peut uniquement être une valeur scalaire (unique).</span><span class="sxs-lookup"><span data-stu-id="75587-109">hello return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="75587-110">Après avoir ajouté un travail de tooa de fonction définie par l’utilisateur de JavaScript, vous pouvez utiliser fonction hello n’importe où dans la requête de hello, comme une fonction scalaire intégrée.</span><span class="sxs-lookup"><span data-stu-id="75587-110">After you add a JavaScript user-defined function tooa job, you can use hello function anywhere in hello query, like a built-in scalar function.</span></span>

<span data-ttu-id="75587-111">Voici quelques scénarios dans lesquels les fonctions JavaScript définies par l’utilisateur vous seront utiles :</span><span class="sxs-lookup"><span data-stu-id="75587-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="75587-112">Analyse et manipulation de chaînes avec des fonctions d’expressions régulières, par exemple **Regexp_Replace()** et **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="75587-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="75587-113">Décodage de données encodées, par exemple la conversion de binaire en hexadécimal</span><span class="sxs-lookup"><span data-stu-id="75587-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="75587-114">Calculs mathématiques avec les fonctions **Math** de JavaScript</span><span class="sxs-lookup"><span data-stu-id="75587-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="75587-115">Opérations de tableaux comme le tri, la jointure, la recherche et le remplissage</span><span class="sxs-lookup"><span data-stu-id="75587-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="75587-116">Voici quelques actions que vous ne pouvez pas effectuer avec une fonction JavaScript définie par l’utilisateur dans Stream Analytics :</span><span class="sxs-lookup"><span data-stu-id="75587-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="75587-117">Appel de points de terminaison REST externes, par exemple la recherche inversée d’une adresse IP ou l’extraction de données de référence à partir d’une source externe</span><span class="sxs-lookup"><span data-stu-id="75587-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="75587-118">Sérialisation ou désérialisation à un format d’événement personnalisé sur les entrées/sorties</span><span class="sxs-lookup"><span data-stu-id="75587-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="75587-119">Création d’agrégats personnalisés</span><span class="sxs-lookup"><span data-stu-id="75587-119">Create custom aggregates</span></span>

<span data-ttu-id="75587-120">Bien que les fonctions comme **Date.GetDate()** ou **Math.Random ()** ne sont pas bloqués dans la définition de fonctions hello, vous devez éviter leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="75587-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in hello functions definition, you should avoid using them.</span></span> <span data-ttu-id="75587-121">Ces fonctions **pas** retour hello même résultat chaque fois que vous les appelez et hello service d’Analytique de flux de données Azure ne conserve pas un journal d’appels de fonction et a renvoyé des résultats.</span><span class="sxs-lookup"><span data-stu-id="75587-121">These functions **do not** return hello same result every time you call them, and hello Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="75587-122">Si une fonction retourne un résultat différent sur hello événements mêmes, la répétabilité n’est pas garantie lorsqu’un travail est redémarré par vous ou par le service de flux de données Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="75587-122">If a function returns different result on hello same events, repeatability is not guaranteed when a job is restarted by you or by hello Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a><span data-ttu-id="75587-123">Ajouter une fonction définie par l’utilisateur de JavaScript dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="75587-123">Add a JavaScript user-defined function in hello Azure portal</span></span>
<span data-ttu-id="75587-124">toocreate une fonction définie par l’utilisateur JavaScript simple sous une tâche de flux de données Analytique existante, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="75587-124">toocreate a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="75587-125">Bonjour portail Azure, recherchez votre tâche de flux de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="75587-125">In hello Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="75587-126">Sous **TOPOLOGIE DE LA TÂCHE**, sélectionnez votre fonction.</span><span class="sxs-lookup"><span data-stu-id="75587-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="75587-127">Une liste vide de fonctions apparaît.</span><span class="sxs-lookup"><span data-stu-id="75587-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="75587-128">toocreate une nouvelle fonction définie par l’utilisateur, sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="75587-128">toocreate a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="75587-129">Sur hello **nouvelle fonction** panneau, pour **Type de fonction**, sélectionnez **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="75587-129">On hello **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="75587-130">Un modèle de fonction par défaut s’affiche dans l’éditeur de hello.</span><span class="sxs-lookup"><span data-stu-id="75587-130">A default function template appears in hello editor.</span></span>
5.  <span data-ttu-id="75587-131">Pourquoi **alias des UDF**, entrez **hex2Int**, modifiez l’implémentation de fonction hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="75587-131">For hello **UDF alias**, enter **hex2Int**, and change hello function implementation as follows:</span></span>

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="75587-132">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="75587-132">Select **Save**.</span></span> <span data-ttu-id="75587-133">Votre fonction apparaît dans la liste des fonctions hello.</span><span class="sxs-lookup"><span data-stu-id="75587-133">Your function appears in hello list of functions.</span></span>
7.  <span data-ttu-id="75587-134">Sélectionnez hello nouvelle **hex2Int** la fonction et vérifiez la définition de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="75587-134">Select hello new **hex2Int** function, and check hello function definition.</span></span> <span data-ttu-id="75587-135">Toutes les fonctions ont un **UDF** alias de préfixe de fonction toohello ajouté.</span><span class="sxs-lookup"><span data-stu-id="75587-135">All functions have a **UDF** prefix added toohello function alias.</span></span> <span data-ttu-id="75587-136">Vous devez trop*inclure hello préfixe* lorsque vous appelez la fonction hello dans votre requête Analytique de flux de données.</span><span class="sxs-lookup"><span data-stu-id="75587-136">You need too*include hello prefix* when you call hello function in your Stream Analytics query.</span></span> <span data-ttu-id="75587-137">Dans ce cas, vous appelez **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="75587-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="75587-138">Appeler une fonction JavaScript définie par l’utilisateur dans une requête</span><span class="sxs-lookup"><span data-stu-id="75587-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="75587-139">Bonjour éditeur de requête, sous **travail topologie**, sélectionnez **requête**.</span><span class="sxs-lookup"><span data-stu-id="75587-139">In hello query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="75587-140">Modifier votre requête, puis appelez la fonction hello défini par l’utilisateur, comme suit :</span><span class="sxs-lookup"><span data-stu-id="75587-140">Edit your query, and then call hello user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="75587-141">fichier de données exemple hello tooupload, entrée de tâche avec le bouton hello.</span><span class="sxs-lookup"><span data-stu-id="75587-141">tooupload hello sample data file, right-click hello job input.</span></span>
4.  <span data-ttu-id="75587-142">tootest votre requête, sélectionnez **Test**.</span><span class="sxs-lookup"><span data-stu-id="75587-142">tootest your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="75587-143">Objets JavaScript pris en charge</span><span class="sxs-lookup"><span data-stu-id="75587-143">Supported JavaScript objects</span></span>
<span data-ttu-id="75587-144">Les fonctions JavaScript définies par l’utilisateur Azure Stream Analytics prennent en charge les objets prédéfinis standard du langage JavaScript.</span><span class="sxs-lookup"><span data-stu-id="75587-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="75587-145">Pour obtenir la liste de ces objets, consultez [Objets globaux](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="75587-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="75587-146">Conversion de type Stream Analytics et JavaScript</span><span class="sxs-lookup"><span data-stu-id="75587-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="75587-147">Il existe des différences entre les types hello qui prennent en charge de langage de requête de flux de données Analytique hello et JavaScript.</span><span class="sxs-lookup"><span data-stu-id="75587-147">There are differences in hello types that hello Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="75587-148">Ce tableau répertorie les mappages de conversion hello entre hello deux :</span><span class="sxs-lookup"><span data-stu-id="75587-148">This table lists hello conversion mappings between hello two:</span></span>

<span data-ttu-id="75587-149">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="75587-149">Stream Analytics</span></span> | <span data-ttu-id="75587-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="75587-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="75587-151">bigint</span><span class="sxs-lookup"><span data-stu-id="75587-151">bigint</span></span> | <span data-ttu-id="75587-152">Nombre (JavaScript peut représenter uniquement des entiers des tooprecisely 2 ^ 53)</span><span class="sxs-lookup"><span data-stu-id="75587-152">Number (JavaScript can only represent integers up tooprecisely 2^53)</span></span>
<span data-ttu-id="75587-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="75587-153">DateTime</span></span> | <span data-ttu-id="75587-154">Date (JavaScript ne prend en charge que les millisecondes)</span><span class="sxs-lookup"><span data-stu-id="75587-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="75587-155">double</span><span class="sxs-lookup"><span data-stu-id="75587-155">double</span></span> | <span data-ttu-id="75587-156">Number</span><span class="sxs-lookup"><span data-stu-id="75587-156">Number</span></span>
<span data-ttu-id="75587-157">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="75587-157">nvarchar(MAX)</span></span> | <span data-ttu-id="75587-158">String</span><span class="sxs-lookup"><span data-stu-id="75587-158">String</span></span>
<span data-ttu-id="75587-159">Enregistrement</span><span class="sxs-lookup"><span data-stu-id="75587-159">Record</span></span> | <span data-ttu-id="75587-160">Object</span><span class="sxs-lookup"><span data-stu-id="75587-160">Object</span></span>
<span data-ttu-id="75587-161">Tableau</span><span class="sxs-lookup"><span data-stu-id="75587-161">Array</span></span> | <span data-ttu-id="75587-162">Tableau</span><span class="sxs-lookup"><span data-stu-id="75587-162">Array</span></span>
<span data-ttu-id="75587-163">NULL</span><span class="sxs-lookup"><span data-stu-id="75587-163">NULL</span></span> | <span data-ttu-id="75587-164">Null</span><span class="sxs-lookup"><span data-stu-id="75587-164">Null</span></span>


<span data-ttu-id="75587-165">Voici les conversions de JavaScript à Stream Analytics :</span><span class="sxs-lookup"><span data-stu-id="75587-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="75587-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="75587-166">JavaScript</span></span> | <span data-ttu-id="75587-167">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="75587-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="75587-168">Number</span><span class="sxs-lookup"><span data-stu-id="75587-168">Number</span></span> | <span data-ttu-id="75587-169">Bigint (si le nombre de hello est arrondi et entre long. MinValue et long. MaxValue ; dans le cas contraire, il est double)</span><span class="sxs-lookup"><span data-stu-id="75587-169">Bigint (if hello number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="75587-170">Date</span><span class="sxs-lookup"><span data-stu-id="75587-170">Date</span></span> | <span data-ttu-id="75587-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="75587-171">DateTime</span></span>
<span data-ttu-id="75587-172">String</span><span class="sxs-lookup"><span data-stu-id="75587-172">String</span></span> | <span data-ttu-id="75587-173">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="75587-173">nvarchar(MAX)</span></span>
<span data-ttu-id="75587-174">Object</span><span class="sxs-lookup"><span data-stu-id="75587-174">Object</span></span> | <span data-ttu-id="75587-175">Enregistrement</span><span class="sxs-lookup"><span data-stu-id="75587-175">Record</span></span>
<span data-ttu-id="75587-176">Tableau</span><span class="sxs-lookup"><span data-stu-id="75587-176">Array</span></span> | <span data-ttu-id="75587-177">Tableau</span><span class="sxs-lookup"><span data-stu-id="75587-177">Array</span></span>
<span data-ttu-id="75587-178">Null, Undefined</span><span class="sxs-lookup"><span data-stu-id="75587-178">Null, Undefined</span></span> | <span data-ttu-id="75587-179">NULL</span><span class="sxs-lookup"><span data-stu-id="75587-179">NULL</span></span>
<span data-ttu-id="75587-180">Un autre type (par exemple une fonction ou une erreur)</span><span class="sxs-lookup"><span data-stu-id="75587-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="75587-181">Non pris en charge (entraîne une erreur d’exécution)</span><span class="sxs-lookup"><span data-stu-id="75587-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="75587-182">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="75587-182">Troubleshooting</span></span>
<span data-ttu-id="75587-183">Erreurs d’exécution JavaScript sont considérées comme irrécupérables et sont exposés via le journal d’activité hello.</span><span class="sxs-lookup"><span data-stu-id="75587-183">JavaScript runtime errors are considered fatal, and are surfaced through hello Activity log.</span></span> <span data-ttu-id="75587-184">tooretrieve hello journal, hello portail Azure, accédez tooyour travail et sélectionnez **le journal d’activité**.</span><span class="sxs-lookup"><span data-stu-id="75587-184">tooretrieve hello log, in hello Azure portal, go tooyour job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="75587-185">Autres modèles de fonctions JavaScript définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="75587-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-toooutput"></a><span data-ttu-id="75587-186">Écrire des toooutput JSON imbriquée</span><span class="sxs-lookup"><span data-stu-id="75587-186">Write nested JSON toooutput</span></span>
<span data-ttu-id="75587-187">Si vous disposez d’une étape de traitement suivi qui utilise une tâche de flux de données Analytique de sortie en tant qu’entrée, et il requiert un format JSON, vous pouvez écrire un toooutput de chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="75587-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string toooutput.</span></span> <span data-ttu-id="75587-188">Hello l’exemple suivant appelle hello **JSON.stringify()** toopack toutes les paires nom/valeur de hello d’entrée et de les écrivent en tant que valeur de chaîne unique dans la sortie de fonction.</span><span class="sxs-lookup"><span data-stu-id="75587-188">hello next example calls hello **JSON.stringify()** function toopack all name/value pairs of hello input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="75587-189">**Définition de la fonction JavaScript définie par l’utilisateur :**</span><span class="sxs-lookup"><span data-stu-id="75587-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="75587-190">**Exemple de requête :**</span><span class="sxs-lookup"><span data-stu-id="75587-190">**Sample query:**</span></span>
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

## <a name="get-help"></a><span data-ttu-id="75587-191">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="75587-191">Get help</span></span>
<span data-ttu-id="75587-192">Pour obtenir de l’aide supplémentaire, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="75587-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="75587-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="75587-193">Next steps</span></span>
* [<span data-ttu-id="75587-194">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="75587-194">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="75587-195">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="75587-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="75587-196">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="75587-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="75587-197">Références sur le langage des requêtes Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="75587-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="75587-198">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="75587-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
