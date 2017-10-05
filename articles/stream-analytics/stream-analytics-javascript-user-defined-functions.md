---
title: "Fonctions JavaScript définies par l’utilisateur Azure Stream Analytics | Microsoft Docs"
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
ms.openlocfilehash: e4a9e6c7078031240c22a51378c0459426b7f626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a><span data-ttu-id="1865d-104">Fonctions JavaScript définies par l’utilisateur Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1865d-104">Azure Stream Analytics JavaScript user-defined functions</span></span>
<span data-ttu-id="1865d-105">Azure Stream Analytics prend en charge les fonctions définies par l’utilisateur écrites en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1865d-105">Azure Stream Analytics supports user-defined functions written in JavaScript.</span></span> <span data-ttu-id="1865d-106">Avec le large éventail de méthodes **String**, **RegExp**, **Math**, **Array** et **Date** que fournit JavaScript, les transformations complexes de données des travaux Stream Analytics sont plus faciles à créer.</span><span class="sxs-lookup"><span data-stu-id="1865d-106">With the rich set of **String**, **RegExp**, **Math**, **Array**, and **Date** methods that JavaScript provides, complex data transformations with Stream Analytics jobs become easier to create.</span></span>

## <a name="javascript-user-defined-functions"></a><span data-ttu-id="1865d-107">Fonctions JavaScript définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="1865d-107">JavaScript user-defined functions</span></span>
<span data-ttu-id="1865d-108">Les fonctions JavaScript définies par l’utilisateur prennent en charge les fonctions scalaires de calcul pur sans état qui ne nécessitent pas de connectivité externe.</span><span class="sxs-lookup"><span data-stu-id="1865d-108">JavaScript user-defined functions support stateless, compute-only scalar functions that do not require external connectivity.</span></span> <span data-ttu-id="1865d-109">La valeur renvoyée par une fonction ne peut être qu’une valeur (unique) scalaire.</span><span class="sxs-lookup"><span data-stu-id="1865d-109">The return value of a function can only be a scalar (single) value.</span></span> <span data-ttu-id="1865d-110">Une fois que vous avez ajouté une fonction JavaScript définie par l’utilisateur à un travail, vous pouvez utiliser la fonction n’importe où dans la requête, comme une fonction scalaire intégrée.</span><span class="sxs-lookup"><span data-stu-id="1865d-110">After you add a JavaScript user-defined function to a job, you can use the function anywhere in the query, like a built-in scalar function.</span></span>

<span data-ttu-id="1865d-111">Voici quelques scénarios dans lesquels les fonctions JavaScript définies par l’utilisateur vous seront utiles :</span><span class="sxs-lookup"><span data-stu-id="1865d-111">Here are some scenarios where you might find JavaScript user-defined functions useful:</span></span>
* <span data-ttu-id="1865d-112">Analyse et manipulation de chaînes avec des fonctions d’expressions régulières, par exemple **Regexp_Replace()** et **Regexp_Extract()**</span><span class="sxs-lookup"><span data-stu-id="1865d-112">Parsing and manipulating strings that have regular expression functions, for example, **Regexp_Replace()** and **Regexp_Extract()**</span></span>
* <span data-ttu-id="1865d-113">Décodage de données encodées, par exemple la conversion de binaire en hexadécimal</span><span class="sxs-lookup"><span data-stu-id="1865d-113">Decoding and encoding data, for example, binary-to-hex conversion</span></span>
* <span data-ttu-id="1865d-114">Calculs mathématiques avec les fonctions **Math** de JavaScript</span><span class="sxs-lookup"><span data-stu-id="1865d-114">Performing mathematic computations with JavaScript **Math** functions</span></span>
* <span data-ttu-id="1865d-115">Opérations de tableaux comme le tri, la jointure, la recherche et le remplissage</span><span class="sxs-lookup"><span data-stu-id="1865d-115">Performing array operations like sort, join, find, and fill</span></span>

<span data-ttu-id="1865d-116">Voici quelques actions que vous ne pouvez pas effectuer avec une fonction JavaScript définie par l’utilisateur dans Stream Analytics :</span><span class="sxs-lookup"><span data-stu-id="1865d-116">Here are some things that you cannot do with a JavaScript user-defined function in Stream Analytics:</span></span>
* <span data-ttu-id="1865d-117">Appel de points de terminaison REST externes, par exemple la recherche inversée d’une adresse IP ou l’extraction de données de référence à partir d’une source externe</span><span class="sxs-lookup"><span data-stu-id="1865d-117">Call out external REST endpoints, for example, performing reverse IP lookup or pulling reference data from an external source</span></span>
* <span data-ttu-id="1865d-118">Sérialisation ou désérialisation à un format d’événement personnalisé sur les entrées/sorties</span><span class="sxs-lookup"><span data-stu-id="1865d-118">Perform custom event format serialization or deserialization on inputs/outputs</span></span>
* <span data-ttu-id="1865d-119">Création d’agrégats personnalisés</span><span class="sxs-lookup"><span data-stu-id="1865d-119">Create custom aggregates</span></span>

<span data-ttu-id="1865d-120">Bien qu’elles ne soient pas bloquées dans la définition des fonctions, évitez d’utiliser des fonctions telles que **Date.GetDate()** ou **Math.random()**.</span><span class="sxs-lookup"><span data-stu-id="1865d-120">Although functions like **Date.GetDate()** or **Math.random()** are not blocked in the functions definition, you should avoid using them.</span></span> <span data-ttu-id="1865d-121">Ces fonctions ne retournent **pas** le même résultat à chaque fois que vous les appelez et le service Azure Stream Analytics ne conserve pas de journal des appels de fonction et des résultats retournés.</span><span class="sxs-lookup"><span data-stu-id="1865d-121">These functions **do not** return the same result every time you call them, and the Azure Stream Analytics service does not keep a journal of function invocations and returned results.</span></span> <span data-ttu-id="1865d-122">Si une fonction retourne un résultat différent sur les mêmes événements, la reproductibilité n’est pas garantie lorsqu’un travail est relancé par vos soins ou par le service Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="1865d-122">If a function returns different result on the same events, repeatability is not guaranteed when a job is restarted by you or by the Stream Analytics service.</span></span>

## <a name="add-a-javascript-user-defined-function-in-the-azure-portal"></a><span data-ttu-id="1865d-123">Ajouter une fonction JavaScript définie par l’utilisateur dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1865d-123">Add a JavaScript user-defined function in the Azure portal</span></span>
<span data-ttu-id="1865d-124">Pour créer une simple fonction JavaScript définie par l’utilisateur dans un travail Stream Analytics existant, suivez ces étapes :</span><span class="sxs-lookup"><span data-stu-id="1865d-124">To create a simple JavaScript user-defined function under an existing Stream Analytics job, do these steps:</span></span>

1.  <span data-ttu-id="1865d-125">Dans le portail Azure, recherchez votre travail Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="1865d-125">In the Azure portal, find your Stream Analytics job.</span></span>
2.  <span data-ttu-id="1865d-126">Sous **TOPOLOGIE DE LA TÂCHE**, sélectionnez votre fonction.</span><span class="sxs-lookup"><span data-stu-id="1865d-126">Under **JOB TOPOLOGY**, select your function.</span></span> <span data-ttu-id="1865d-127">Une liste vide de fonctions apparaît.</span><span class="sxs-lookup"><span data-stu-id="1865d-127">An empty list of functions appears.</span></span>
3.  <span data-ttu-id="1865d-128">Pour créer une fonction définie par l’utilisateur, sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1865d-128">To create a new user-defined function, select **Add**.</span></span>
4.  <span data-ttu-id="1865d-129">Dans le panneau **Nouvelle fonction**, pour **Type de fonction**, sélectionnez **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="1865d-129">On the **New Function** blade, for **Function Type**, select **JavaScript**.</span></span> <span data-ttu-id="1865d-130">Un modèle de fonction par défaut apparaît dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="1865d-130">A default function template appears in the editor.</span></span>
5.  <span data-ttu-id="1865d-131">Pour l’**alias de fonction définie par l’utilisateur**, entrez **hex2Int**, puis modifiez l’implémentation de la fonction de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="1865d-131">For the **UDF alias**, enter **hex2Int**, and change the function implementation as follows:</span></span>

    ```
    // Convert Hex value to integer.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  <span data-ttu-id="1865d-132">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1865d-132">Select **Save**.</span></span> <span data-ttu-id="1865d-133">La fonction apparaît dans la liste des fonctions.</span><span class="sxs-lookup"><span data-stu-id="1865d-133">Your function appears in the list of functions.</span></span>
7.  <span data-ttu-id="1865d-134">Sélectionnez la nouvelle fonction **hex2Int** pour vérifier sa définition.</span><span class="sxs-lookup"><span data-stu-id="1865d-134">Select the new **hex2Int** function, and check the function definition.</span></span> <span data-ttu-id="1865d-135">Toutes les fonctions ont un préfixe **UDF** ajouté à l’alias de la fonction.</span><span class="sxs-lookup"><span data-stu-id="1865d-135">All functions have a **UDF** prefix added to the function alias.</span></span> <span data-ttu-id="1865d-136">Vous devez *inclure le préfixe* quand vous appelez la fonction dans votre requête Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="1865d-136">You need to *include the prefix* when you call the function in your Stream Analytics query.</span></span> <span data-ttu-id="1865d-137">Dans ce cas, vous appelez **UDF.hex2Int**.</span><span class="sxs-lookup"><span data-stu-id="1865d-137">In this case, you call **UDF.hex2Int**.</span></span>

## <a name="call-a-javascript-user-defined-function-in-a-query"></a><span data-ttu-id="1865d-138">Appeler une fonction JavaScript définie par l’utilisateur dans une requête</span><span class="sxs-lookup"><span data-stu-id="1865d-138">Call a JavaScript user-defined function in a query</span></span>

1. <span data-ttu-id="1865d-139">Dans l’éditeur de requêtes, sous **TOPOLOGIE DE LA TÂCHE**, sélectionnez **Requête**.</span><span class="sxs-lookup"><span data-stu-id="1865d-139">In the query editor, under **JOB TOPOLOGY**, select **Query**.</span></span>
2.  <span data-ttu-id="1865d-140">Modifiez votre requête, puis appelez la fonction définie par l’utilisateur comme suit :</span><span class="sxs-lookup"><span data-stu-id="1865d-140">Edit your query, and then call the user-defined function, like this:</span></span>

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  <span data-ttu-id="1865d-141">Pour charger l’exemple de fichier de données, cliquez avec le bouton droit sur l’entrée du travail.</span><span class="sxs-lookup"><span data-stu-id="1865d-141">To upload the sample data file, right-click the job input.</span></span>
4.  <span data-ttu-id="1865d-142">Pour tester votre requête, sélectionnez **Test**.</span><span class="sxs-lookup"><span data-stu-id="1865d-142">To test your query, select **Test**.</span></span>


## <a name="supported-javascript-objects"></a><span data-ttu-id="1865d-143">Objets JavaScript pris en charge</span><span class="sxs-lookup"><span data-stu-id="1865d-143">Supported JavaScript objects</span></span>
<span data-ttu-id="1865d-144">Les fonctions JavaScript définies par l’utilisateur Azure Stream Analytics prennent en charge les objets prédéfinis standard du langage JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1865d-144">Azure Stream Analytics JavaScript user-defined functions support standard, built-in JavaScript objects.</span></span> <span data-ttu-id="1865d-145">Pour obtenir la liste de ces objets, consultez [Objets globaux](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span><span class="sxs-lookup"><span data-stu-id="1865d-145">For a list of these objects, see [Global Objects](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects).</span></span>

### <a name="stream-analytics-and-javascript-type-conversion"></a><span data-ttu-id="1865d-146">Conversion de type Stream Analytics et JavaScript</span><span class="sxs-lookup"><span data-stu-id="1865d-146">Stream Analytics and JavaScript type conversion</span></span>

<span data-ttu-id="1865d-147">Il existe des différences entre les types pris en charge dans le langage de requête Stream Analytics et JavaScript.</span><span class="sxs-lookup"><span data-stu-id="1865d-147">There are differences in the types that the Stream Analytics query language and JavaScript support.</span></span> <span data-ttu-id="1865d-148">Le tableau suivant répertorie les mappages de conversion entre les deux :</span><span class="sxs-lookup"><span data-stu-id="1865d-148">This table lists the conversion mappings between the two:</span></span>

<span data-ttu-id="1865d-149">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1865d-149">Stream Analytics</span></span> | <span data-ttu-id="1865d-150">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1865d-150">JavaScript</span></span>
--- | ---
<span data-ttu-id="1865d-151">bigint</span><span class="sxs-lookup"><span data-stu-id="1865d-151">bigint</span></span> | <span data-ttu-id="1865d-152">Number (JavaScript ne peut représenter les entiers que jusqu’à 2^53 précisément)</span><span class="sxs-lookup"><span data-stu-id="1865d-152">Number (JavaScript can only represent integers up to precisely 2^53)</span></span>
<span data-ttu-id="1865d-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="1865d-153">DateTime</span></span> | <span data-ttu-id="1865d-154">Date (JavaScript ne prend en charge que les millisecondes)</span><span class="sxs-lookup"><span data-stu-id="1865d-154">Date (JavaScript only supports milliseconds)</span></span>
<span data-ttu-id="1865d-155">double</span><span class="sxs-lookup"><span data-stu-id="1865d-155">double</span></span> | <span data-ttu-id="1865d-156">Number</span><span class="sxs-lookup"><span data-stu-id="1865d-156">Number</span></span>
<span data-ttu-id="1865d-157">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="1865d-157">nvarchar(MAX)</span></span> | <span data-ttu-id="1865d-158">String</span><span class="sxs-lookup"><span data-stu-id="1865d-158">String</span></span>
<span data-ttu-id="1865d-159">Enregistrement</span><span class="sxs-lookup"><span data-stu-id="1865d-159">Record</span></span> | <span data-ttu-id="1865d-160">Object</span><span class="sxs-lookup"><span data-stu-id="1865d-160">Object</span></span>
<span data-ttu-id="1865d-161">Tableau</span><span class="sxs-lookup"><span data-stu-id="1865d-161">Array</span></span> | <span data-ttu-id="1865d-162">Tableau</span><span class="sxs-lookup"><span data-stu-id="1865d-162">Array</span></span>
<span data-ttu-id="1865d-163">NULL</span><span class="sxs-lookup"><span data-stu-id="1865d-163">NULL</span></span> | <span data-ttu-id="1865d-164">Null</span><span class="sxs-lookup"><span data-stu-id="1865d-164">Null</span></span>


<span data-ttu-id="1865d-165">Voici les conversions de JavaScript à Stream Analytics :</span><span class="sxs-lookup"><span data-stu-id="1865d-165">Here are JavaScript-to-Stream Analytics conversions:</span></span>


<span data-ttu-id="1865d-166">JavaScript</span><span class="sxs-lookup"><span data-stu-id="1865d-166">JavaScript</span></span> | <span data-ttu-id="1865d-167">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1865d-167">Stream Analytics</span></span>
--- | ---
<span data-ttu-id="1865d-168">Number</span><span class="sxs-lookup"><span data-stu-id="1865d-168">Number</span></span> | <span data-ttu-id="1865d-169">Bigint (si le nombre est rond et entre long.MinValue et long.MaxValue, sinon, double)</span><span class="sxs-lookup"><span data-stu-id="1865d-169">Bigint (if the number is round and between long.MinValue and long.MaxValue; otherwise, it's double)</span></span>
<span data-ttu-id="1865d-170">Date</span><span class="sxs-lookup"><span data-stu-id="1865d-170">Date</span></span> | <span data-ttu-id="1865d-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="1865d-171">DateTime</span></span>
<span data-ttu-id="1865d-172">String</span><span class="sxs-lookup"><span data-stu-id="1865d-172">String</span></span> | <span data-ttu-id="1865d-173">nvarchar(MAX)</span><span class="sxs-lookup"><span data-stu-id="1865d-173">nvarchar(MAX)</span></span>
<span data-ttu-id="1865d-174">Object</span><span class="sxs-lookup"><span data-stu-id="1865d-174">Object</span></span> | <span data-ttu-id="1865d-175">Enregistrement</span><span class="sxs-lookup"><span data-stu-id="1865d-175">Record</span></span>
<span data-ttu-id="1865d-176">Tableau</span><span class="sxs-lookup"><span data-stu-id="1865d-176">Array</span></span> | <span data-ttu-id="1865d-177">Tableau</span><span class="sxs-lookup"><span data-stu-id="1865d-177">Array</span></span>
<span data-ttu-id="1865d-178">Null, Undefined</span><span class="sxs-lookup"><span data-stu-id="1865d-178">Null, Undefined</span></span> | <span data-ttu-id="1865d-179">NULL</span><span class="sxs-lookup"><span data-stu-id="1865d-179">NULL</span></span>
<span data-ttu-id="1865d-180">Un autre type (par exemple une fonction ou une erreur)</span><span class="sxs-lookup"><span data-stu-id="1865d-180">Any other type (for example, a function or error)</span></span> | <span data-ttu-id="1865d-181">Non pris en charge (entraîne une erreur d’exécution)</span><span class="sxs-lookup"><span data-stu-id="1865d-181">Not supported (results in runtime error)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1865d-182">résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="1865d-182">Troubleshooting</span></span>
<span data-ttu-id="1865d-183">Les erreurs d’exécution JavaScript sont considérées comme irrécupérables et remontées par le biais du journal d’activité.</span><span class="sxs-lookup"><span data-stu-id="1865d-183">JavaScript runtime errors are considered fatal, and are surfaced through the Activity log.</span></span> <span data-ttu-id="1865d-184">Pour récupérer le journal, dans le portail Azure, accédez à votre travail et sélectionnez **Journal d’activité**.</span><span class="sxs-lookup"><span data-stu-id="1865d-184">To retrieve the log, in the Azure portal, go to your job and select **Activity log**.</span></span>


## <a name="other-javascript-user-defined-function-patterns"></a><span data-ttu-id="1865d-185">Autres modèles de fonctions JavaScript définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="1865d-185">Other JavaScript user-defined function patterns</span></span>

### <a name="write-nested-json-to-output"></a><span data-ttu-id="1865d-186">Écrire du code JSON imbriqué en sortie</span><span class="sxs-lookup"><span data-stu-id="1865d-186">Write nested JSON to output</span></span>
<span data-ttu-id="1865d-187">Si vous avez une étape de traitement de suivi qui prend la sortie du travail Stream Analytics en entrée et qu’un format JSON est requis, vous pouvez écrire une chaîne JSON comme sortie.</span><span class="sxs-lookup"><span data-stu-id="1865d-187">If you have a follow-up processing step that uses a Stream Analytics job output as input, and it requires a JSON format, you can write a JSON string to output.</span></span> <span data-ttu-id="1865d-188">L’exemple suivant appelle la fonction **JSON.stringify()** pour compresser toutes les paires nom/valeur de l’entrée, puis les écrire sous la forme d’une valeur de chaîne unique en sortie.</span><span class="sxs-lookup"><span data-stu-id="1865d-188">The next example calls the **JSON.stringify()** function to pack all name/value pairs of the input, and then write them as a single string value in output.</span></span>

<span data-ttu-id="1865d-189">**Définition de la fonction JavaScript définie par l’utilisateur :**</span><span class="sxs-lookup"><span data-stu-id="1865d-189">**JavaScript user-defined function definition:**</span></span>

```
function main(x) {
return JSON.stringify(x);
}
```

<span data-ttu-id="1865d-190">**Exemple de requête :**</span><span class="sxs-lookup"><span data-stu-id="1865d-190">**Sample query:**</span></span>
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

## <a name="get-help"></a><span data-ttu-id="1865d-191">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="1865d-191">Get help</span></span>
<span data-ttu-id="1865d-192">Pour obtenir de l’aide supplémentaire, essayez notre [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="1865d-192">For additional help, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1865d-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1865d-193">Next steps</span></span>
* [<span data-ttu-id="1865d-194">Présentation d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1865d-194">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="1865d-195">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1865d-195">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="1865d-196">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1865d-196">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="1865d-197">Références sur le langage des requêtes Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1865d-197">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="1865d-198">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1865d-198">Azure Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
