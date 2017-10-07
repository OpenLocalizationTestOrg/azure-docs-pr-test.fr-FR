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
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="1326f-104">Exemples de requête pour les modes d’utilisation courants dans Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1326f-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="1326f-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="1326f-105">Introduction</span></span>
<span data-ttu-id="1326f-106">Les requêtes dans Azure Stream Analytics sont exprimées dans un langage de requête de type SQL.</span><span class="sxs-lookup"><span data-stu-id="1326f-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="1326f-107">Ces requêtes sont documentées dans hello [Analytique de flux de données de référence du langage de requête](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span><span class="sxs-lookup"><span data-stu-id="1326f-107">These queries are documented in hello [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="1326f-108">Ce article décrit les solutions tooseveral requête des modèles courants, les selon des scénarios concrets.</span><span class="sxs-lookup"><span data-stu-id="1326f-108">This article outlines solutions tooseveral common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="1326f-109">Il est un travail en cours et continue toobe mis à jour avec les nouveaux modèles de manière continue.</span><span class="sxs-lookup"><span data-stu-id="1326f-109">It is a work in progress and continues toobe updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="1326f-110">Exemple de requête : Convertir des types de données</span><span class="sxs-lookup"><span data-stu-id="1326f-110">Query example: Convert data types</span></span>
<span data-ttu-id="1326f-111">**Description**: définir des types de hello de propriétés sur les flux d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="1326f-111">**Description**: Define hello types of properties on hello input stream.</span></span>
<span data-ttu-id="1326f-112">Par exemple, le poids de voiture hello sera disponible sur les flux d’entrée hello sous forme de chaînes et doit toobe converti trop**INT** tooperform **somme** , configurez-le.</span><span class="sxs-lookup"><span data-stu-id="1326f-112">For example, hello car weight is coming on hello input stream as strings and needs toobe converted too**INT** tooperform **SUM** it up.</span></span>

<span data-ttu-id="1326f-113">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="1326f-113">**Input**:</span></span>

| <span data-ttu-id="1326f-114">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-114">Make</span></span> | <span data-ttu-id="1326f-115">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-115">Time</span></span> | <span data-ttu-id="1326f-116">Poids</span><span class="sxs-lookup"><span data-stu-id="1326f-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1326f-117">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-117">Honda</span></span> |<span data-ttu-id="1326f-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="1326f-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="1326f-119">"1000"</span></span> |
| <span data-ttu-id="1326f-120">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-120">Honda</span></span> |<span data-ttu-id="1326f-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="1326f-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="1326f-122">"2000"</span></span> |

<span data-ttu-id="1326f-123">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="1326f-123">**Output**:</span></span>

| <span data-ttu-id="1326f-124">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-124">Make</span></span> | <span data-ttu-id="1326f-125">Poids</span><span class="sxs-lookup"><span data-stu-id="1326f-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="1326f-126">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-126">Honda</span></span> |<span data-ttu-id="1326f-127">3000</span><span class="sxs-lookup"><span data-stu-id="1326f-127">3000</span></span> |

<span data-ttu-id="1326f-128">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="1326f-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="1326f-129">**Explication**: utilisez un **CAST** instruction Bonjour **poids** champ toospecify son type de données.</span><span class="sxs-lookup"><span data-stu-id="1326f-129">**Explanation**: Use a **CAST** statement in hello **Weight** field toospecify its data type.</span></span> <span data-ttu-id="1326f-130">Consultez la liste hello des types de données pris en charge dans [des types de données (Analytique de flux de données Azure)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span><span class="sxs-lookup"><span data-stu-id="1326f-130">See hello list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a><span data-ttu-id="1326f-131">Exemple de requête : utilisation non Like comme toodo critères spéciaux</span><span class="sxs-lookup"><span data-stu-id="1326f-131">Query example: Use Like/Not like toodo pattern matching</span></span>
<span data-ttu-id="1326f-132">**Description**: Vérifiez qu’une valeur de champ d’événement de hello correspond à un certain modèle.</span><span class="sxs-lookup"><span data-stu-id="1326f-132">**Description**: Check that a field value on hello event matches a certain pattern.</span></span>
<span data-ttu-id="1326f-133">Par exemple, vérifiez que les résultats hello retourne plaques d’immatriculation qui commence par A et se terminer par 9.</span><span class="sxs-lookup"><span data-stu-id="1326f-133">For example, check that hello result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="1326f-134">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="1326f-134">**Input**:</span></span>

| <span data-ttu-id="1326f-135">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-135">Make</span></span> | <span data-ttu-id="1326f-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="1326f-136">LicensePlate</span></span> | <span data-ttu-id="1326f-137">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1326f-138">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-138">Honda</span></span> |<span data-ttu-id="1326f-139">ABC-123</span><span class="sxs-lookup"><span data-stu-id="1326f-139">ABC-123</span></span> |<span data-ttu-id="1326f-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="1326f-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-141">Toyota</span></span> |<span data-ttu-id="1326f-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="1326f-142">AAA-999</span></span> |<span data-ttu-id="1326f-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="1326f-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="1326f-144">Nissan</span></span> |<span data-ttu-id="1326f-145">ABC-369</span><span class="sxs-lookup"><span data-stu-id="1326f-145">ABC-369</span></span> |<span data-ttu-id="1326f-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="1326f-147">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="1326f-147">**Output**:</span></span>

| <span data-ttu-id="1326f-148">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-148">Make</span></span> | <span data-ttu-id="1326f-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="1326f-149">LicensePlate</span></span> | <span data-ttu-id="1326f-150">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1326f-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-151">Toyota</span></span> |<span data-ttu-id="1326f-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="1326f-152">AAA-999</span></span> |<span data-ttu-id="1326f-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="1326f-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="1326f-154">Nissan</span></span> |<span data-ttu-id="1326f-155">ABC-369</span><span class="sxs-lookup"><span data-stu-id="1326f-155">ABC-369</span></span> |<span data-ttu-id="1326f-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="1326f-157">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="1326f-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="1326f-158">**Explication**: hello d’utilisation **comme** hello de toocheck instruction **LicensePlate** valeur du champ.</span><span class="sxs-lookup"><span data-stu-id="1326f-158">**Explanation**: Use hello **LIKE** statement toocheck hello **LicensePlate** field value.</span></span> <span data-ttu-id="1326f-159">Il doit commencer par un A, puis avoir une chaîne de zéro, un ou plusieurs caractères, puis se terminer par un 9.</span><span class="sxs-lookup"><span data-stu-id="1326f-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="1326f-160">Exemple de requête : Spécifier la logique pour différentes casses/valeurs (instructions CASE)</span><span class="sxs-lookup"><span data-stu-id="1326f-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="1326f-161">**Description** : Fournir un calcul différent pour un champ en fonction de certains critères.</span><span class="sxs-lookup"><span data-stu-id="1326f-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="1326f-162">Par exemple, fournir une description de chaîne pour le nombre de voitures Hello même rendre passé, avec une casse spéciale pour 1.</span><span class="sxs-lookup"><span data-stu-id="1326f-162">For example, provide a string description for how many cars of hello same make passed, with a special case for 1.</span></span>

<span data-ttu-id="1326f-163">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="1326f-163">**Input**:</span></span>

| <span data-ttu-id="1326f-164">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-164">Make</span></span> | <span data-ttu-id="1326f-165">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="1326f-166">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-166">Honda</span></span> |<span data-ttu-id="1326f-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="1326f-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-168">Toyota</span></span> |<span data-ttu-id="1326f-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="1326f-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-170">Toyota</span></span> |<span data-ttu-id="1326f-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="1326f-172">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="1326f-172">**Output**:</span></span>

| <span data-ttu-id="1326f-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="1326f-173">CarsPassed</span></span> | <span data-ttu-id="1326f-174">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1326f-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-175">1 Honda</span></span> |<span data-ttu-id="1326f-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="1326f-177">2 Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-177">2 Toyotas</span></span> |<span data-ttu-id="1326f-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="1326f-179">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="1326f-179">**Solution**:</span></span>

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

<span data-ttu-id="1326f-180">**Explication**: hello **cas** clause nous permet de tooprovide un calcul différent, en fonction de certains critères (dans notre cas, le nombre de hello de voitures hello dans la fenêtre d’agrégation hello).</span><span class="sxs-lookup"><span data-stu-id="1326f-180">**Explanation**: hello **CASE** clause allows us tooprovide a different computation, based on some criteria (in our case, hello count of hello cars in hello aggregate window).</span></span>

## <a name="query-example-send-data-toomultiple-outputs"></a><span data-ttu-id="1326f-181">Exemple de requête : envoyer des données toomultiple fournit en sortie</span><span class="sxs-lookup"><span data-stu-id="1326f-181">Query example: Send data toomultiple outputs</span></span>
<span data-ttu-id="1326f-182">**Description**: toomultiple de données d’envoi de sortie cibles à partir d’une seule tâche.</span><span class="sxs-lookup"><span data-stu-id="1326f-182">**Description**: Send data toomultiple output targets from a single job.</span></span>
<span data-ttu-id="1326f-183">Par exemple, analyser des données pour une alerte de seuil et stockage de tooblob tous les événements d’archivage.</span><span class="sxs-lookup"><span data-stu-id="1326f-183">For example, analyze data for a threshold-based alert and archive all events tooblob storage.</span></span>

<span data-ttu-id="1326f-184">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="1326f-184">**Input**:</span></span>

| <span data-ttu-id="1326f-185">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-185">Make</span></span> | <span data-ttu-id="1326f-186">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="1326f-187">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-187">Honda</span></span> |<span data-ttu-id="1326f-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="1326f-189">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-189">Honda</span></span> |<span data-ttu-id="1326f-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="1326f-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-191">Toyota</span></span> |<span data-ttu-id="1326f-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="1326f-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-193">Toyota</span></span> |<span data-ttu-id="1326f-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="1326f-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-195">Toyota</span></span> |<span data-ttu-id="1326f-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="1326f-197">**Output1**:</span><span class="sxs-lookup"><span data-stu-id="1326f-197">**Output1**:</span></span>

| <span data-ttu-id="1326f-198">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-198">Make</span></span> | <span data-ttu-id="1326f-199">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="1326f-200">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-200">Honda</span></span> |<span data-ttu-id="1326f-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="1326f-202">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-202">Honda</span></span> |<span data-ttu-id="1326f-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="1326f-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-204">Toyota</span></span> |<span data-ttu-id="1326f-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="1326f-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-206">Toyota</span></span> |<span data-ttu-id="1326f-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="1326f-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-208">Toyota</span></span> |<span data-ttu-id="1326f-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="1326f-210">**Output2**:</span><span class="sxs-lookup"><span data-stu-id="1326f-210">**Output2**:</span></span>

| <span data-ttu-id="1326f-211">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-211">Make</span></span> | <span data-ttu-id="1326f-212">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-212">Time</span></span> | <span data-ttu-id="1326f-213">Nombre</span><span class="sxs-lookup"><span data-stu-id="1326f-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1326f-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-214">Toyota</span></span> |<span data-ttu-id="1326f-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="1326f-216">3</span><span class="sxs-lookup"><span data-stu-id="1326f-216">3</span></span> |

<span data-ttu-id="1326f-217">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="1326f-217">**Solution**:</span></span>

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

<span data-ttu-id="1326f-218">**Explication**: hello **INTO** clause indique Analytique de flux de données qui génère des toowrite hello données toofrom Hello cette instruction.</span><span class="sxs-lookup"><span data-stu-id="1326f-218">**Explanation**: hello **INTO** clause tells Stream Analytics which of hello outputs toowrite hello data toofrom this statement.</span></span>
<span data-ttu-id="1326f-219">Hello première requête est une passerelle de données hello nous avons reçu sortie tooan que nous avons nommé **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="1326f-219">hello first query is a pass-through of hello data we received tooan output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="1326f-220">fait une requête de deuxième Hello certains d’agrégation simple et le filtrage et envoie les résultats de hello tooa de système d’alerte en aval.</span><span class="sxs-lookup"><span data-stu-id="1326f-220">hello second query does some simple aggregation and filtering, and it sends hello results tooa downstream alerting system.</span></span>

<span data-ttu-id="1326f-221">Notez que vous pouvez également réutiliser des résultats d’expressions de table communes (CTE) hello hello (tel que **WITH** instructions) dans plusieurs instructions de sortie.</span><span class="sxs-lookup"><span data-stu-id="1326f-221">Note that you can also reuse hello results of hello common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="1326f-222">Cette option a hello avantage de l’ouverture de source d’entrée de toohello des lecteurs moins.</span><span class="sxs-lookup"><span data-stu-id="1326f-222">This option has hello added benefit of opening fewer readers toohello input source.</span></span>
<span data-ttu-id="1326f-223">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="1326f-223">For example:</span></span> 

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

## <a name="query-example-count-unique-values"></a><span data-ttu-id="1326f-224">Exemple de requête : Compter des valeurs uniques</span><span class="sxs-lookup"><span data-stu-id="1326f-224">Query example: Count unique values</span></span>
<span data-ttu-id="1326f-225">**Description**: hello dénombrer les valeurs de champ unique qui s’affichent dans le flux hello dans une fenêtre de temps.</span><span class="sxs-lookup"><span data-stu-id="1326f-225">**Description**: Count hello number of unique field values that appear in hello stream within a time window.</span></span>
<span data-ttu-id="1326f-226">Par exemple, le nombre unique fait de voitures passées gare de péage hello dans une fenêtre de 2 secondes ?</span><span class="sxs-lookup"><span data-stu-id="1326f-226">For example, how many unique makes of cars passed through hello toll booth in a 2-second window?</span></span>

<span data-ttu-id="1326f-227">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="1326f-227">**Input**:</span></span>

| <span data-ttu-id="1326f-228">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-228">Make</span></span> | <span data-ttu-id="1326f-229">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="1326f-230">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-230">Honda</span></span> |<span data-ttu-id="1326f-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="1326f-232">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-232">Honda</span></span> |<span data-ttu-id="1326f-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="1326f-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-234">Toyota</span></span> |<span data-ttu-id="1326f-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="1326f-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-236">Toyota</span></span> |<span data-ttu-id="1326f-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="1326f-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-238">Toyota</span></span> |<span data-ttu-id="1326f-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="1326f-240">**Output:**</span><span class="sxs-lookup"><span data-stu-id="1326f-240">**Output:**</span></span>

| <span data-ttu-id="1326f-241">Nombre</span><span class="sxs-lookup"><span data-stu-id="1326f-241">Count</span></span> | <span data-ttu-id="1326f-242">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="1326f-243">2</span><span class="sxs-lookup"><span data-stu-id="1326f-243">2</span></span> |<span data-ttu-id="1326f-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="1326f-245">1</span><span class="sxs-lookup"><span data-stu-id="1326f-245">1</span></span> |<span data-ttu-id="1326f-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="1326f-247">**Solution :**</span><span class="sxs-lookup"><span data-stu-id="1326f-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="1326f-248">**Explication :**
**COUNT (DISTINCT Vérifiez)** renvoie hello le nombre de valeurs distinctes dans hello **rendre** colonne dans une fenêtre de temps.</span><span class="sxs-lookup"><span data-stu-id="1326f-248">**Explanation:**
**COUNT(DISTINCT Make)** returns hello number of distinct values in hello **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="1326f-249">Exemple de requête : Déterminer si une valeur a changé</span><span class="sxs-lookup"><span data-stu-id="1326f-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="1326f-250">**Description**: examinez un toodetermine valeur précédente si elle est différente de la valeur actuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="1326f-250">**Description**: Look at a previous value toodetermine if it is different than hello current value.</span></span>
<span data-ttu-id="1326f-251">Par exemple, est voiture précédente de hello sur hello de route de péage hello que même rendre aussi voiture en cours de hello ?</span><span class="sxs-lookup"><span data-stu-id="1326f-251">For example, is hello previous car on hello toll road hello same make as hello current car?</span></span>

<span data-ttu-id="1326f-252">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="1326f-252">**Input**:</span></span>

| <span data-ttu-id="1326f-253">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-253">Make</span></span> | <span data-ttu-id="1326f-254">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="1326f-255">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-255">Honda</span></span> |<span data-ttu-id="1326f-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="1326f-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-257">Toyota</span></span> |<span data-ttu-id="1326f-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="1326f-259">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="1326f-259">**Output**:</span></span>

| <span data-ttu-id="1326f-260">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-260">Make</span></span> | <span data-ttu-id="1326f-261">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="1326f-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-262">Toyota</span></span> |<span data-ttu-id="1326f-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="1326f-264">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="1326f-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="1326f-265">**Explication**: utilisez **LAG** toopeek dans hello d’entrée d’un événement nouveau flux de données et obtenir hello **rendre** valeur.</span><span class="sxs-lookup"><span data-stu-id="1326f-265">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="1326f-266">Comparez-le toohello **rendre** valeur sur les événements en cours hello et sortie hello si elles sont différentes.</span><span class="sxs-lookup"><span data-stu-id="1326f-266">Then compare it toohello **Make** value on hello current event and output hello event if they are different.</span></span>

## <a name="query-example-find-hello-first-event-in-a-window"></a><span data-ttu-id="1326f-267">Exemple de requête : rechercher hello premier événement dans une fenêtre</span><span class="sxs-lookup"><span data-stu-id="1326f-267">Query example: Find hello first event in a window</span></span>
<span data-ttu-id="1326f-268">**Description**: rechercher hello première voiture dans chaque intervalle de 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="1326f-268">**Description**: Find hello first car in every 10-minute interval.</span></span>

<span data-ttu-id="1326f-269">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="1326f-269">**Input**:</span></span>

| <span data-ttu-id="1326f-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="1326f-270">LicensePlate</span></span> | <span data-ttu-id="1326f-271">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-271">Make</span></span> | <span data-ttu-id="1326f-272">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1326f-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="1326f-273">DXE 5291</span></span> |<span data-ttu-id="1326f-274">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-274">Honda</span></span> |<span data-ttu-id="1326f-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="1326f-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="1326f-276">YZK 5704</span></span> |<span data-ttu-id="1326f-277">Ford</span><span class="sxs-lookup"><span data-stu-id="1326f-277">Ford</span></span> |<span data-ttu-id="1326f-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="1326f-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="1326f-279">RMV 8282</span></span> |<span data-ttu-id="1326f-280">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-280">Honda</span></span> |<span data-ttu-id="1326f-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="1326f-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="1326f-282">YHN 6970</span></span> |<span data-ttu-id="1326f-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-283">Toyota</span></span> |<span data-ttu-id="1326f-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="1326f-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="1326f-285">VFE 1616</span></span> |<span data-ttu-id="1326f-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-286">Toyota</span></span> |<span data-ttu-id="1326f-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="1326f-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="1326f-288">QYF 9358</span></span> |<span data-ttu-id="1326f-289">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-289">Honda</span></span> |<span data-ttu-id="1326f-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="1326f-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="1326f-291">MDR 6128</span></span> |<span data-ttu-id="1326f-292">BMW</span><span class="sxs-lookup"><span data-stu-id="1326f-292">BMW</span></span> |<span data-ttu-id="1326f-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="1326f-294">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="1326f-294">**Output**:</span></span>

| <span data-ttu-id="1326f-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="1326f-295">LicensePlate</span></span> | <span data-ttu-id="1326f-296">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-296">Make</span></span> | <span data-ttu-id="1326f-297">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1326f-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="1326f-298">DXE 5291</span></span> |<span data-ttu-id="1326f-299">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-299">Honda</span></span> |<span data-ttu-id="1326f-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="1326f-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="1326f-301">QYF 9358</span></span> |<span data-ttu-id="1326f-302">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-302">Honda</span></span> |<span data-ttu-id="1326f-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="1326f-304">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="1326f-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="1326f-305">Maintenant assurons-nous modification hello problème et rechercher hello première voiture d’un particulier dans chaque intervalle de 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="1326f-305">Now let’s change hello problem and find hello first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="1326f-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="1326f-306">LicensePlate</span></span> | <span data-ttu-id="1326f-307">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-307">Make</span></span> | <span data-ttu-id="1326f-308">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1326f-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="1326f-309">DXE 5291</span></span> |<span data-ttu-id="1326f-310">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-310">Honda</span></span> |<span data-ttu-id="1326f-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="1326f-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="1326f-312">YZK 5704</span></span> |<span data-ttu-id="1326f-313">Ford</span><span class="sxs-lookup"><span data-stu-id="1326f-313">Ford</span></span> |<span data-ttu-id="1326f-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="1326f-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="1326f-315">YHN 6970</span></span> |<span data-ttu-id="1326f-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-316">Toyota</span></span> |<span data-ttu-id="1326f-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="1326f-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="1326f-318">QYF 9358</span></span> |<span data-ttu-id="1326f-319">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-319">Honda</span></span> |<span data-ttu-id="1326f-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="1326f-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="1326f-321">MDR 6128</span></span> |<span data-ttu-id="1326f-322">BMW</span><span class="sxs-lookup"><span data-stu-id="1326f-322">BMW</span></span> |<span data-ttu-id="1326f-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="1326f-324">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="1326f-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a><span data-ttu-id="1326f-325">Exemple de requête : rechercher hello du dernier événement dans une fenêtre</span><span class="sxs-lookup"><span data-stu-id="1326f-325">Query example: Find hello last event in a window</span></span>
<span data-ttu-id="1326f-326">**Description**: voiture de dernière hello rechercher dans chaque intervalle de 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="1326f-326">**Description**: Find hello last car in every 10-minute interval.</span></span>

<span data-ttu-id="1326f-327">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="1326f-327">**Input**:</span></span>

| <span data-ttu-id="1326f-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="1326f-328">LicensePlate</span></span> | <span data-ttu-id="1326f-329">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-329">Make</span></span> | <span data-ttu-id="1326f-330">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1326f-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="1326f-331">DXE 5291</span></span> |<span data-ttu-id="1326f-332">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-332">Honda</span></span> |<span data-ttu-id="1326f-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="1326f-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="1326f-334">YZK 5704</span></span> |<span data-ttu-id="1326f-335">Ford</span><span class="sxs-lookup"><span data-stu-id="1326f-335">Ford</span></span> |<span data-ttu-id="1326f-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="1326f-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="1326f-337">RMV 8282</span></span> |<span data-ttu-id="1326f-338">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-338">Honda</span></span> |<span data-ttu-id="1326f-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="1326f-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="1326f-340">YHN 6970</span></span> |<span data-ttu-id="1326f-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-341">Toyota</span></span> |<span data-ttu-id="1326f-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="1326f-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="1326f-343">VFE 1616</span></span> |<span data-ttu-id="1326f-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-344">Toyota</span></span> |<span data-ttu-id="1326f-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="1326f-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="1326f-346">QYF 9358</span></span> |<span data-ttu-id="1326f-347">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-347">Honda</span></span> |<span data-ttu-id="1326f-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="1326f-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="1326f-349">MDR 6128</span></span> |<span data-ttu-id="1326f-350">BMW</span><span class="sxs-lookup"><span data-stu-id="1326f-350">BMW</span></span> |<span data-ttu-id="1326f-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="1326f-352">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="1326f-352">**Output**:</span></span>

| <span data-ttu-id="1326f-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="1326f-353">LicensePlate</span></span> | <span data-ttu-id="1326f-354">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-354">Make</span></span> | <span data-ttu-id="1326f-355">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1326f-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="1326f-356">VFE 1616</span></span> |<span data-ttu-id="1326f-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-357">Toyota</span></span> |<span data-ttu-id="1326f-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="1326f-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="1326f-359">MDR 6128</span></span> |<span data-ttu-id="1326f-360">BMW</span><span class="sxs-lookup"><span data-stu-id="1326f-360">BMW</span></span> |<span data-ttu-id="1326f-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="1326f-362">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="1326f-362">**Solution**:</span></span>

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

<span data-ttu-id="1326f-363">**Explication**: il existe deux étapes de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="1326f-363">**Explanation**: There are two steps in hello query.</span></span> <span data-ttu-id="1326f-364">Hello première recherche un hello dernière horodatage dans les fenêtres de 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="1326f-364">hello first one finds hello latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="1326f-365">les jointures Hello deuxième étape hello des résultats de requête de première hello avec hello d’origine flux toofind hello les événements qui correspondent aux hello derniers horodatages dans chaque fenêtre.</span><span class="sxs-lookup"><span data-stu-id="1326f-365">hello second step joins hello results of hello first query with hello original stream toofind hello events that match hello last time stamps in each window.</span></span> 

## <a name="query-example-detect-hello-absence-of-events"></a><span data-ttu-id="1326f-366">Exemple de requête : détecte l’absence de hello d’événements</span><span class="sxs-lookup"><span data-stu-id="1326f-366">Query example: Detect hello absence of events</span></span>
<span data-ttu-id="1326f-367">**Description** : Vérifier qu’un flux ne contient aucune valeur correspondant à certains critères.</span><span class="sxs-lookup"><span data-stu-id="1326f-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="1326f-368">Par exemple, 2 voitures consécutifs de hello que même rendre saisi route de péage hello dans hello dernière 90 secondes ?</span><span class="sxs-lookup"><span data-stu-id="1326f-368">For example, have 2 consecutive cars from hello same make entered hello toll road within hello last 90 seconds?</span></span>

<span data-ttu-id="1326f-369">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="1326f-369">**Input**:</span></span>

| <span data-ttu-id="1326f-370">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-370">Make</span></span> | <span data-ttu-id="1326f-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="1326f-371">LicensePlate</span></span> | <span data-ttu-id="1326f-372">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1326f-373">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-373">Honda</span></span> |<span data-ttu-id="1326f-374">ABC-123</span><span class="sxs-lookup"><span data-stu-id="1326f-374">ABC-123</span></span> |<span data-ttu-id="1326f-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="1326f-376">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-376">Honda</span></span> |<span data-ttu-id="1326f-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="1326f-377">AAA-999</span></span> |<span data-ttu-id="1326f-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="1326f-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-379">Toyota</span></span> |<span data-ttu-id="1326f-380">DEF-987</span><span class="sxs-lookup"><span data-stu-id="1326f-380">DEF-987</span></span> |<span data-ttu-id="1326f-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="1326f-382">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-382">Honda</span></span> |<span data-ttu-id="1326f-383">GHI-345</span><span class="sxs-lookup"><span data-stu-id="1326f-383">GHI-345</span></span> |<span data-ttu-id="1326f-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="1326f-385">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="1326f-385">**Output**:</span></span>

| <span data-ttu-id="1326f-386">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-386">Make</span></span> | <span data-ttu-id="1326f-387">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-387">Time</span></span> | <span data-ttu-id="1326f-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="1326f-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="1326f-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="1326f-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="1326f-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="1326f-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="1326f-391">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-391">Honda</span></span> |<span data-ttu-id="1326f-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="1326f-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="1326f-393">AAA-999</span></span> |<span data-ttu-id="1326f-394">ABC-123</span><span class="sxs-lookup"><span data-stu-id="1326f-394">ABC-123</span></span> |<span data-ttu-id="1326f-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="1326f-396">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="1326f-396">**Solution**:</span></span>

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

<span data-ttu-id="1326f-397">**Explication**: utilisez **LAG** toopeek dans hello d’entrée d’un événement nouveau flux de données et obtenir hello **rendre** valeur.</span><span class="sxs-lookup"><span data-stu-id="1326f-397">**Explanation**: Use **LAG** toopeek into hello input stream one event back and get hello **Make** value.</span></span> <span data-ttu-id="1326f-398">Comparer toohello **rendre** valeur dans l’événement hello en cours, puis sur les événements de hello sortie si elles sont hello identiques.</span><span class="sxs-lookup"><span data-stu-id="1326f-398">Compare it toohello **MAKE** value in hello current event, and then output hello event if they are hello same.</span></span> <span data-ttu-id="1326f-399">Vous pouvez également utiliser **LAG** tooget des données sur les voitures précédente hello.</span><span class="sxs-lookup"><span data-stu-id="1326f-399">You can also use **LAG** tooget data about hello previous car.</span></span>

## <a name="query-example-detect-hello-duration-between-events"></a><span data-ttu-id="1326f-400">Exemple de requête : détecter la durée hello entre les événements</span><span class="sxs-lookup"><span data-stu-id="1326f-400">Query example: Detect hello duration between events</span></span>
<span data-ttu-id="1326f-401">**Description**: trouver durée hello d’un événement donné.</span><span class="sxs-lookup"><span data-stu-id="1326f-401">**Description**: Find hello duration of a given event.</span></span> <span data-ttu-id="1326f-402">Par exemple, étant donné un parcours de web, déterminer temps hello sur une fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1326f-402">For example, given a web clickstream, determine hello time spent on a feature.</span></span>

<span data-ttu-id="1326f-403">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="1326f-403">**Input**:</span></span>  

| <span data-ttu-id="1326f-404">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="1326f-404">User</span></span> | <span data-ttu-id="1326f-405">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="1326f-405">Feature</span></span> | <span data-ttu-id="1326f-406">Événement</span><span class="sxs-lookup"><span data-stu-id="1326f-406">Event</span></span> | <span data-ttu-id="1326f-407">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="1326f-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="1326f-408">RightMenu</span></span> |<span data-ttu-id="1326f-409">Démarrer</span><span class="sxs-lookup"><span data-stu-id="1326f-409">Start</span></span> |<span data-ttu-id="1326f-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="1326f-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="1326f-411">RightMenu</span></span> |<span data-ttu-id="1326f-412">Terminer</span><span class="sxs-lookup"><span data-stu-id="1326f-412">End</span></span> |<span data-ttu-id="1326f-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="1326f-414">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="1326f-414">**Output**:</span></span>  

| <span data-ttu-id="1326f-415">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="1326f-415">User</span></span> | <span data-ttu-id="1326f-416">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="1326f-416">Feature</span></span> | <span data-ttu-id="1326f-417">Durée</span><span class="sxs-lookup"><span data-stu-id="1326f-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="1326f-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="1326f-418">RightMenu</span></span> |<span data-ttu-id="1326f-419">7</span><span class="sxs-lookup"><span data-stu-id="1326f-419">7</span></span> |

<span data-ttu-id="1326f-420">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="1326f-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="1326f-421">**Explication**: hello d’utilisation **dernière** fonction tooretrieve hello dernière **temps** valeur lorsque le type d’événement hello a été **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="1326f-421">**Explanation**: Use hello **LAST** function tooretrieve hello last **TIME** value when hello event type was **Start**.</span></span> <span data-ttu-id="1326f-422">Hello **dernière** fonction utilise **PARTITION BY [user]** tooindicate qui hello le résultat est calculé par l’utilisateur unique.</span><span class="sxs-lookup"><span data-stu-id="1326f-422">hello **LAST** function uses **PARTITION BY [user]** tooindicate that hello result is computed per unique user.</span></span> <span data-ttu-id="1326f-423">requête de Hello a un seuil maximal de 1 heure pour la différence de temps hello entre **Démarrer** et **arrêter** événements, mais peut être configuré en fonction des besoins **(limite DURATION(hour, 1)**.</span><span class="sxs-lookup"><span data-stu-id="1326f-423">hello query has a 1-hour maximum threshold for hello time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-hello-duration-of-a-condition"></a><span data-ttu-id="1326f-424">Exemple de requête : détecter la durée hello d’une condition</span><span class="sxs-lookup"><span data-stu-id="1326f-424">Query example: Detect hello duration of a condition</span></span>
<span data-ttu-id="1326f-425">**Description** : Rechercher la durée pendant laquelle une condition s’est produite.</span><span class="sxs-lookup"><span data-stu-id="1326f-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="1326f-426">Par exemple, supposez qu’à la suite d’un bogue, le poids de toutes les voitures est incorrect (supérieur à 20 000 livres).</span><span class="sxs-lookup"><span data-stu-id="1326f-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="1326f-427">Nous voulons que la durée de hello toocompute de bogue de hello.</span><span class="sxs-lookup"><span data-stu-id="1326f-427">We want toocompute hello duration of hello bug.</span></span>

<span data-ttu-id="1326f-428">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="1326f-428">**Input**:</span></span>

| <span data-ttu-id="1326f-429">Marque</span><span class="sxs-lookup"><span data-stu-id="1326f-429">Make</span></span> | <span data-ttu-id="1326f-430">Temps</span><span class="sxs-lookup"><span data-stu-id="1326f-430">Time</span></span> | <span data-ttu-id="1326f-431">Poids</span><span class="sxs-lookup"><span data-stu-id="1326f-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1326f-432">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-432">Honda</span></span> |<span data-ttu-id="1326f-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="1326f-434">2000</span><span class="sxs-lookup"><span data-stu-id="1326f-434">2000</span></span> |
| <span data-ttu-id="1326f-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-435">Toyota</span></span> |<span data-ttu-id="1326f-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="1326f-437">25000</span><span class="sxs-lookup"><span data-stu-id="1326f-437">25000</span></span> |
| <span data-ttu-id="1326f-438">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-438">Honda</span></span> |<span data-ttu-id="1326f-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="1326f-440">26000</span><span class="sxs-lookup"><span data-stu-id="1326f-440">26000</span></span> |
| <span data-ttu-id="1326f-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-441">Toyota</span></span> |<span data-ttu-id="1326f-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="1326f-443">25000</span><span class="sxs-lookup"><span data-stu-id="1326f-443">25000</span></span> |
| <span data-ttu-id="1326f-444">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-444">Honda</span></span> |<span data-ttu-id="1326f-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="1326f-446">26000</span><span class="sxs-lookup"><span data-stu-id="1326f-446">26000</span></span> |
| <span data-ttu-id="1326f-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-447">Toyota</span></span> |<span data-ttu-id="1326f-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="1326f-449">25000</span><span class="sxs-lookup"><span data-stu-id="1326f-449">25000</span></span> |
| <span data-ttu-id="1326f-450">Honda</span><span class="sxs-lookup"><span data-stu-id="1326f-450">Honda</span></span> |<span data-ttu-id="1326f-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="1326f-452">26000</span><span class="sxs-lookup"><span data-stu-id="1326f-452">26000</span></span> |
| <span data-ttu-id="1326f-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="1326f-453">Toyota</span></span> |<span data-ttu-id="1326f-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="1326f-455">2000</span><span class="sxs-lookup"><span data-stu-id="1326f-455">2000</span></span> |

<span data-ttu-id="1326f-456">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="1326f-456">**Output**:</span></span>

| <span data-ttu-id="1326f-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="1326f-457">StartFault</span></span> | <span data-ttu-id="1326f-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="1326f-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="1326f-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="1326f-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="1326f-461">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="1326f-461">**Solution**:</span></span>

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

<span data-ttu-id="1326f-462">**Explication**: utilisez **LAG** tooview hello flux d’entrée des dernières 24 heures, puis recherchez les instances où **StartFault** et **StopFault** sont couvertes par hello poids < 20000.</span><span class="sxs-lookup"><span data-stu-id="1326f-462">**Explanation**: Use **LAG** tooview hello input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by hello weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="1326f-463">Exemple de requête : Remplir les valeurs manquantes</span><span class="sxs-lookup"><span data-stu-id="1326f-463">Query example: Fill missing values</span></span>
<span data-ttu-id="1326f-464">**Description**: pour les flux de hello d’événements qui ont des valeurs manquantes, produisent un flux d’événements à intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="1326f-464">**Description**: For hello stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="1326f-465">Par exemple, génère un événement toutes les 5 secondes qui indique le point de données hello plus récemment affichée.</span><span class="sxs-lookup"><span data-stu-id="1326f-465">For example, generate an event every 5 seconds that reports hello most recently seen data point.</span></span>

<span data-ttu-id="1326f-466">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="1326f-466">**Input**:</span></span>

| <span data-ttu-id="1326f-467">t</span><span class="sxs-lookup"><span data-stu-id="1326f-467">t</span></span> | <span data-ttu-id="1326f-468">value</span><span class="sxs-lookup"><span data-stu-id="1326f-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="1326f-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="1326f-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="1326f-470">1</span><span class="sxs-lookup"><span data-stu-id="1326f-470">1</span></span> |
| <span data-ttu-id="1326f-471">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="1326f-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="1326f-472">2</span><span class="sxs-lookup"><span data-stu-id="1326f-472">2</span></span> |
| <span data-ttu-id="1326f-473">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="1326f-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="1326f-474">3</span><span class="sxs-lookup"><span data-stu-id="1326f-474">3</span></span> |
| <span data-ttu-id="1326f-475">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="1326f-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="1326f-476">4</span><span class="sxs-lookup"><span data-stu-id="1326f-476">4</span></span> |
| <span data-ttu-id="1326f-477">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="1326f-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="1326f-478">5</span><span class="sxs-lookup"><span data-stu-id="1326f-478">5</span></span> |
| <span data-ttu-id="1326f-479">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="1326f-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="1326f-480">6</span><span class="sxs-lookup"><span data-stu-id="1326f-480">6</span></span> |

<span data-ttu-id="1326f-481">**Sortie (10 premières lignes)**:</span><span class="sxs-lookup"><span data-stu-id="1326f-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="1326f-482">windowend</span><span class="sxs-lookup"><span data-stu-id="1326f-482">windowend</span></span> | <span data-ttu-id="1326f-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="1326f-483">lastevent.t</span></span> | <span data-ttu-id="1326f-484">lastevent.value</span><span class="sxs-lookup"><span data-stu-id="1326f-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1326f-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="1326f-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="1326f-487">1</span><span class="sxs-lookup"><span data-stu-id="1326f-487">1</span></span> |
| <span data-ttu-id="1326f-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="1326f-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="1326f-490">2</span><span class="sxs-lookup"><span data-stu-id="1326f-490">2</span></span> |
| <span data-ttu-id="1326f-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="1326f-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="1326f-493">3</span><span class="sxs-lookup"><span data-stu-id="1326f-493">3</span></span> |
| <span data-ttu-id="1326f-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="1326f-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="1326f-496">4</span><span class="sxs-lookup"><span data-stu-id="1326f-496">4</span></span> |
| <span data-ttu-id="1326f-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="1326f-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="1326f-499">4</span><span class="sxs-lookup"><span data-stu-id="1326f-499">4</span></span> |
| <span data-ttu-id="1326f-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="1326f-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="1326f-502">4</span><span class="sxs-lookup"><span data-stu-id="1326f-502">4</span></span> |
| <span data-ttu-id="1326f-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="1326f-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="1326f-505">5</span><span class="sxs-lookup"><span data-stu-id="1326f-505">5</span></span> |
| <span data-ttu-id="1326f-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="1326f-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="1326f-508">6</span><span class="sxs-lookup"><span data-stu-id="1326f-508">6</span></span> |
| <span data-ttu-id="1326f-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="1326f-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="1326f-511">6</span><span class="sxs-lookup"><span data-stu-id="1326f-511">6</span></span> |
| <span data-ttu-id="1326f-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="1326f-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="1326f-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="1326f-514">6</span><span class="sxs-lookup"><span data-stu-id="1326f-514">6</span></span> |

<span data-ttu-id="1326f-515">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="1326f-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="1326f-516">**Explication**: cette requête génère des événements toutes les 5 secondes et sorties hello du dernier événement reçu précédemment.</span><span class="sxs-lookup"><span data-stu-id="1326f-516">**Explanation**: This query generates events every 5 seconds and outputs hello last event that was received previously.</span></span> <span data-ttu-id="1326f-517">Hello [saut fenêtre](https://msdn.microsoft.com/library/dn835041.aspx "fenêtre saut--Analytique de flux de données Azure") durée détermine combien hello arrière requête se présente événement plus récente de hello toofind (300 secondes dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="1326f-517">hello [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back hello query looks toofind hello latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="1326f-518">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="1326f-518">Get help</span></span>
<span data-ttu-id="1326f-519">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="1326f-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1326f-520">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1326f-520">Next steps</span></span>
* [<span data-ttu-id="1326f-521">Introduction tooAzure Analytique de flux de données</span><span class="sxs-lookup"><span data-stu-id="1326f-521">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="1326f-522">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1326f-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="1326f-523">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1326f-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="1326f-524">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1326f-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="1326f-525">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1326f-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

