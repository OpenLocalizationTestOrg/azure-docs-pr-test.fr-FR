---
title: "Exemples de requête pour les modes d’utilisation courants dans Stream Analytics | Microsoft Docs"
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
ms.openlocfilehash: a00855c200b3fb365073bad4c5773b02c4c2c7fe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a><span data-ttu-id="bc83e-104">Exemples de requête pour les modes d’utilisation courants dans Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bc83e-104">Query examples for common Stream Analytics usage patterns</span></span>
## <a name="introduction"></a><span data-ttu-id="bc83e-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="bc83e-105">Introduction</span></span>
<span data-ttu-id="bc83e-106">Les requêtes dans Azure Stream Analytics sont exprimées dans un langage de requête de type SQL.</span><span class="sxs-lookup"><span data-stu-id="bc83e-106">Queries in Azure Stream Analytics are expressed in a SQL-like query language.</span></span> <span data-ttu-id="bc83e-107">Ces requêtes sont documentées dans le guide [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) (Informations de référence sur le langage de requête Stream Analytics).</span><span class="sxs-lookup"><span data-stu-id="bc83e-107">These queries are documented in the [Stream Analytics query language reference](https://msdn.microsoft.com/library/azure/dn834998.aspx) guide.</span></span> <span data-ttu-id="bc83e-108">Cet article décrit les solutions à plusieurs modèles de requête habituels, inspirés de scénarios réels.</span><span class="sxs-lookup"><span data-stu-id="bc83e-108">This article outlines solutions to several common query patterns, based on real-world scenarios.</span></span> <span data-ttu-id="bc83e-109">Il est en cours et mis à jour avec de nouveaux modèles de manière continue.</span><span class="sxs-lookup"><span data-stu-id="bc83e-109">It is a work in progress and continues to be updated with new patterns on an ongoing basis.</span></span>

## <a name="query-example-convert-data-types"></a><span data-ttu-id="bc83e-110">Exemple de requête : Convertir des types de données</span><span class="sxs-lookup"><span data-stu-id="bc83e-110">Query example: Convert data types</span></span>
<span data-ttu-id="bc83e-111">**Description** : Définir les types des propriétés sur le flux d’entrée.</span><span class="sxs-lookup"><span data-stu-id="bc83e-111">**Description**: Define the types of properties on the input stream.</span></span>
<span data-ttu-id="bc83e-112">Par exemple, le poids de la voiture arrive sur le flux d’entrée sous forme de chaîne, et doit être converti en **INT** pour exécuter la fonction **SUM**.</span><span class="sxs-lookup"><span data-stu-id="bc83e-112">For example, the car weight is coming on the input stream as strings and needs to be converted to **INT** to perform **SUM** it up.</span></span>

<span data-ttu-id="bc83e-113">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-113">**Input**:</span></span>

| <span data-ttu-id="bc83e-114">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-114">Make</span></span> | <span data-ttu-id="bc83e-115">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-115">Time</span></span> | <span data-ttu-id="bc83e-116">Poids</span><span class="sxs-lookup"><span data-stu-id="bc83e-116">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc83e-117">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-117">Honda</span></span> |<span data-ttu-id="bc83e-118">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-118">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="bc83e-119">"1000"</span><span class="sxs-lookup"><span data-stu-id="bc83e-119">"1000"</span></span> |
| <span data-ttu-id="bc83e-120">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-120">Honda</span></span> |<span data-ttu-id="bc83e-121">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-121">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="bc83e-122">"2000"</span><span class="sxs-lookup"><span data-stu-id="bc83e-122">"2000"</span></span> |

<span data-ttu-id="bc83e-123">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-123">**Output**:</span></span>

| <span data-ttu-id="bc83e-124">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-124">Make</span></span> | <span data-ttu-id="bc83e-125">Poids</span><span class="sxs-lookup"><span data-stu-id="bc83e-125">Weight</span></span> |
| --- | --- |
| <span data-ttu-id="bc83e-126">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-126">Honda</span></span> |<span data-ttu-id="bc83e-127">3000</span><span class="sxs-lookup"><span data-stu-id="bc83e-127">3000</span></span> |

<span data-ttu-id="bc83e-128">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-128">**Solution**:</span></span>

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

<span data-ttu-id="bc83e-129">**Explication** : Utilisez une instruction **CAST** dans le champ **Poids** pour spécifier son type de données.</span><span class="sxs-lookup"><span data-stu-id="bc83e-129">**Explanation**: Use a **CAST** statement in the **Weight** field to specify its data type.</span></span> <span data-ttu-id="bc83e-130">Voir la liste des types de données pris en charge dans [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx) (Types de données (Azure Stream Analytics)).</span><span class="sxs-lookup"><span data-stu-id="bc83e-130">See the list of supported data types in [Data types (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).</span></span>

## <a name="query-example-use-likenot-like-to-do-pattern-matching"></a><span data-ttu-id="bc83e-131">Exemple de requête : Utiliser Like/Not like pour les critères spéciaux</span><span class="sxs-lookup"><span data-stu-id="bc83e-131">Query example: Use Like/Not like to do pattern matching</span></span>
<span data-ttu-id="bc83e-132">**Description**: Vérifier qu’une valeur de champ sur l’événement correspond à un certain modèle.</span><span class="sxs-lookup"><span data-stu-id="bc83e-132">**Description**: Check that a field value on the event matches a certain pattern.</span></span>
<span data-ttu-id="bc83e-133">Par exemple, vérifier que le résultat retourne des plaques d’immatriculation qui commencent par A et se terminent par 9.</span><span class="sxs-lookup"><span data-stu-id="bc83e-133">For example, check that the result returns license plates that start with A and end with 9.</span></span>

<span data-ttu-id="bc83e-134">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-134">**Input**:</span></span>

| <span data-ttu-id="bc83e-135">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-135">Make</span></span> | <span data-ttu-id="bc83e-136">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="bc83e-136">LicensePlate</span></span> | <span data-ttu-id="bc83e-137">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-137">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc83e-138">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-138">Honda</span></span> |<span data-ttu-id="bc83e-139">ABC-123</span><span class="sxs-lookup"><span data-stu-id="bc83e-139">ABC-123</span></span> |<span data-ttu-id="bc83e-140">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-140">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="bc83e-141">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-141">Toyota</span></span> |<span data-ttu-id="bc83e-142">AAA-999</span><span class="sxs-lookup"><span data-stu-id="bc83e-142">AAA-999</span></span> |<span data-ttu-id="bc83e-143">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-143">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="bc83e-144">Nissan</span><span class="sxs-lookup"><span data-stu-id="bc83e-144">Nissan</span></span> |<span data-ttu-id="bc83e-145">ABC-369</span><span class="sxs-lookup"><span data-stu-id="bc83e-145">ABC-369</span></span> |<span data-ttu-id="bc83e-146">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-146">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="bc83e-147">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-147">**Output**:</span></span>

| <span data-ttu-id="bc83e-148">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-148">Make</span></span> | <span data-ttu-id="bc83e-149">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="bc83e-149">LicensePlate</span></span> | <span data-ttu-id="bc83e-150">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-150">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc83e-151">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-151">Toyota</span></span> |<span data-ttu-id="bc83e-152">AAA-999</span><span class="sxs-lookup"><span data-stu-id="bc83e-152">AAA-999</span></span> |<span data-ttu-id="bc83e-153">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-153">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="bc83e-154">Nissan</span><span class="sxs-lookup"><span data-stu-id="bc83e-154">Nissan</span></span> |<span data-ttu-id="bc83e-155">ABC-369</span><span class="sxs-lookup"><span data-stu-id="bc83e-155">ABC-369</span></span> |<span data-ttu-id="bc83e-156">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-156">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="bc83e-157">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-157">**Solution**:</span></span>

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

<span data-ttu-id="bc83e-158">**Explication** : Utilisez l’instruction **LIKE** pour vérifier la valeur du champ **LicensePlate**.</span><span class="sxs-lookup"><span data-stu-id="bc83e-158">**Explanation**: Use the **LIKE** statement to check the **LicensePlate** field value.</span></span> <span data-ttu-id="bc83e-159">Il doit commencer par un A, puis avoir une chaîne de zéro, un ou plusieurs caractères, puis se terminer par un 9.</span><span class="sxs-lookup"><span data-stu-id="bc83e-159">It should start with an A, then have any string of zero or more characters, and then end with a 9.</span></span> 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a><span data-ttu-id="bc83e-160">Exemple de requête : Spécifier la logique pour différentes casses/valeurs (instructions CASE)</span><span class="sxs-lookup"><span data-stu-id="bc83e-160">Query example: Specify logic for different cases/values (CASE statements)</span></span>
<span data-ttu-id="bc83e-161">**Description** : Fournir un calcul différent pour un champ en fonction de certains critères.</span><span class="sxs-lookup"><span data-stu-id="bc83e-161">**Description**: Provide a different computation for a field, based on a particular criterion.</span></span>
<span data-ttu-id="bc83e-162">Par exemple, fournir une description de chaîne pour le nombre de voitures de la même marque avec une casse spéciale pour 1.</span><span class="sxs-lookup"><span data-stu-id="bc83e-162">For example, provide a string description for how many cars of the same make passed, with a special case for 1.</span></span>

<span data-ttu-id="bc83e-163">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-163">**Input**:</span></span>

| <span data-ttu-id="bc83e-164">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-164">Make</span></span> | <span data-ttu-id="bc83e-165">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-165">Time</span></span> |
| --- | --- |
| <span data-ttu-id="bc83e-166">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-166">Honda</span></span> |<span data-ttu-id="bc83e-167">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-167">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="bc83e-168">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-168">Toyota</span></span> |<span data-ttu-id="bc83e-169">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-169">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="bc83e-170">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-170">Toyota</span></span> |<span data-ttu-id="bc83e-171">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-171">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="bc83e-172">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-172">**Output**:</span></span>

| <span data-ttu-id="bc83e-173">CarsPassed</span><span class="sxs-lookup"><span data-stu-id="bc83e-173">CarsPassed</span></span> | <span data-ttu-id="bc83e-174">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-174">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc83e-175">1 Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-175">1 Honda</span></span> |<span data-ttu-id="bc83e-176">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-176">2015-01-01T00:00:10.0000000Z</span></span> |
| <span data-ttu-id="bc83e-177">2 Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-177">2 Toyotas</span></span> |<span data-ttu-id="bc83e-178">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-178">2015-01-01T00:00:10.0000000Z</span></span> |

<span data-ttu-id="bc83e-179">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-179">**Solution**:</span></span>

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

<span data-ttu-id="bc83e-180">**Explication** : La clause **CASE** permet de fournir un calcul différent en fonction de certains critères (ici, le nombre de voitures dans la fenêtre d’agrégation).</span><span class="sxs-lookup"><span data-stu-id="bc83e-180">**Explanation**: The **CASE** clause allows us to provide a different computation, based on some criteria (in our case, the count of the cars in the aggregate window).</span></span>

## <a name="query-example-send-data-to-multiple-outputs"></a><span data-ttu-id="bc83e-181">Exemple de requête : envoi de données vers plusieurs sorties</span><span class="sxs-lookup"><span data-stu-id="bc83e-181">Query example: Send data to multiple outputs</span></span>
<span data-ttu-id="bc83e-182">**Description** : Envoyer des données à plusieurs cibles de sortie à partir d’un travail unique.</span><span class="sxs-lookup"><span data-stu-id="bc83e-182">**Description**: Send data to multiple output targets from a single job.</span></span>
<span data-ttu-id="bc83e-183">Par exemple, analyser des données relatives à une alerte basée sur un seuil et archiver tous les événements dans le Stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="bc83e-183">For example, analyze data for a threshold-based alert and archive all events to blob storage.</span></span>

<span data-ttu-id="bc83e-184">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-184">**Input**:</span></span>

| <span data-ttu-id="bc83e-185">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-185">Make</span></span> | <span data-ttu-id="bc83e-186">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-186">Time</span></span> |
| --- | --- |
| <span data-ttu-id="bc83e-187">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-187">Honda</span></span> |<span data-ttu-id="bc83e-188">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-188">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="bc83e-189">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-189">Honda</span></span> |<span data-ttu-id="bc83e-190">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-190">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="bc83e-191">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-191">Toyota</span></span> |<span data-ttu-id="bc83e-192">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-192">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="bc83e-193">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-193">Toyota</span></span> |<span data-ttu-id="bc83e-194">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-194">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="bc83e-195">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-195">Toyota</span></span> |<span data-ttu-id="bc83e-196">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-196">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="bc83e-197">**Output1**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-197">**Output1**:</span></span>

| <span data-ttu-id="bc83e-198">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-198">Make</span></span> | <span data-ttu-id="bc83e-199">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-199">Time</span></span> |
| --- | --- |
| <span data-ttu-id="bc83e-200">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-200">Honda</span></span> |<span data-ttu-id="bc83e-201">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-201">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="bc83e-202">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-202">Honda</span></span> |<span data-ttu-id="bc83e-203">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-203">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="bc83e-204">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-204">Toyota</span></span> |<span data-ttu-id="bc83e-205">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-205">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="bc83e-206">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-206">Toyota</span></span> |<span data-ttu-id="bc83e-207">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-207">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="bc83e-208">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-208">Toyota</span></span> |<span data-ttu-id="bc83e-209">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-209">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="bc83e-210">**Output2**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-210">**Output2**:</span></span>

| <span data-ttu-id="bc83e-211">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-211">Make</span></span> | <span data-ttu-id="bc83e-212">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-212">Time</span></span> | <span data-ttu-id="bc83e-213">Nombre</span><span class="sxs-lookup"><span data-stu-id="bc83e-213">Count</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc83e-214">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-214">Toyota</span></span> |<span data-ttu-id="bc83e-215">2015-01-01T00:00:10.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-215">2015-01-01T00:00:10.0000000Z</span></span> |<span data-ttu-id="bc83e-216">3</span><span class="sxs-lookup"><span data-stu-id="bc83e-216">3</span></span> |

<span data-ttu-id="bc83e-217">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-217">**Solution**:</span></span>

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

<span data-ttu-id="bc83e-218">**Explication** : La clause **INTO** indique à Stream Analytics la sortie sur laquelle écrire les données à partir de cette instruction.</span><span class="sxs-lookup"><span data-stu-id="bc83e-218">**Explanation**: The **INTO** clause tells Stream Analytics which of the outputs to write the data to from this statement.</span></span>
<span data-ttu-id="bc83e-219">La première requête est un transfert des données que nous avons reçues vers une sortie nommée **ArchiveOutput**.</span><span class="sxs-lookup"><span data-stu-id="bc83e-219">The first query is a pass-through of the data we received to an output that we named **ArchiveOutput**.</span></span>
<span data-ttu-id="bc83e-220">La deuxième requête effectue une agrégation et un filtrage simples, et envoie les résultats vers un système d’alerte en aval.</span><span class="sxs-lookup"><span data-stu-id="bc83e-220">The second query does some simple aggregation and filtering, and it sends the results to a downstream alerting system.</span></span>

<span data-ttu-id="bc83e-221">Notez que vous pouvez également réutiliser les résultats d’expressions de table communes (par exemple avec des instructions **WITH**) dans plusieurs instructions de sortie.</span><span class="sxs-lookup"><span data-stu-id="bc83e-221">Note that you can also reuse the results of the common table expressions (CTEs) (such as **WITH** statements) in multiple output statements.</span></span> <span data-ttu-id="bc83e-222">Cette option a l’avantage d’ouvrir moins de lecteurs vers la source d’entrée.</span><span class="sxs-lookup"><span data-stu-id="bc83e-222">This option has the added benefit of opening fewer readers to the input source.</span></span>
<span data-ttu-id="bc83e-223">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="bc83e-223">For example:</span></span> 

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

## <a name="query-example-count-unique-values"></a><span data-ttu-id="bc83e-224">Exemple de requête : Compter des valeurs uniques</span><span class="sxs-lookup"><span data-stu-id="bc83e-224">Query example: Count unique values</span></span>
<span data-ttu-id="bc83e-225">**Description** : Compter le nombre de valeurs de champ uniques qui apparaissent dans le flux au cours d’une fenêtre de temps.</span><span class="sxs-lookup"><span data-stu-id="bc83e-225">**Description**: Count the number of unique field values that appear in the stream within a time window.</span></span>
<span data-ttu-id="bc83e-226">Par exemple, combien de voitures d’une même marque ont franchi le péage dans une fenêtre de temps de deux secondes ?</span><span class="sxs-lookup"><span data-stu-id="bc83e-226">For example, how many unique makes of cars passed through the toll booth in a 2-second window?</span></span>

<span data-ttu-id="bc83e-227">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-227">**Input**:</span></span>

| <span data-ttu-id="bc83e-228">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-228">Make</span></span> | <span data-ttu-id="bc83e-229">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-229">Time</span></span> |
| --- | --- |
| <span data-ttu-id="bc83e-230">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-230">Honda</span></span> |<span data-ttu-id="bc83e-231">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-231">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="bc83e-232">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-232">Honda</span></span> |<span data-ttu-id="bc83e-233">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-233">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="bc83e-234">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-234">Toyota</span></span> |<span data-ttu-id="bc83e-235">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-235">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="bc83e-236">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-236">Toyota</span></span> |<span data-ttu-id="bc83e-237">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-237">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="bc83e-238">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-238">Toyota</span></span> |<span data-ttu-id="bc83e-239">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-239">2015-01-01T00:00:03.0000000Z</span></span> |

<span data-ttu-id="bc83e-240">**Output:**</span><span class="sxs-lookup"><span data-stu-id="bc83e-240">**Output:**</span></span>

| <span data-ttu-id="bc83e-241">Nombre</span><span class="sxs-lookup"><span data-stu-id="bc83e-241">Count</span></span> | <span data-ttu-id="bc83e-242">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-242">Time</span></span> |
| --- | --- |
| <span data-ttu-id="bc83e-243">2</span><span class="sxs-lookup"><span data-stu-id="bc83e-243">2</span></span> |<span data-ttu-id="bc83e-244">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-244">2015-01-01T00:00:02.000Z</span></span> |
| <span data-ttu-id="bc83e-245">1</span><span class="sxs-lookup"><span data-stu-id="bc83e-245">1</span></span> |<span data-ttu-id="bc83e-246">2015-01-01T00:00:04.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-246">2015-01-01T00:00:04.000Z</span></span> |

<span data-ttu-id="bc83e-247">**Solution :**</span><span class="sxs-lookup"><span data-stu-id="bc83e-247">**Solution:**</span></span>

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


<span data-ttu-id="bc83e-248">**Explication :**
**COUNT(DISTINCT Make)** retourne le nombre de valeurs distinctes de la colonne **Marque** dans une fenêtre de temps.</span><span class="sxs-lookup"><span data-stu-id="bc83e-248">**Explanation:**
**COUNT(DISTINCT Make)** returns the number of distinct values in the **Make** column within a time window.</span></span>

## <a name="query-example-determine-if-a-value-has-changed"></a><span data-ttu-id="bc83e-249">Exemple de requête : Déterminer si une valeur a changé</span><span class="sxs-lookup"><span data-stu-id="bc83e-249">Query example: Determine if a value has changed</span></span>
<span data-ttu-id="bc83e-250">**Description** : Examiner une valeur précédente pour déterminer si elle est différente de la valeur actuelle.</span><span class="sxs-lookup"><span data-stu-id="bc83e-250">**Description**: Look at a previous value to determine if it is different than the current value.</span></span>
<span data-ttu-id="bc83e-251">Par exemple, la voiture précédente sur la route à péage est-elle de la même marque que la voiture actuelle ?</span><span class="sxs-lookup"><span data-stu-id="bc83e-251">For example, is the previous car on the toll road the same make as the current car?</span></span>

<span data-ttu-id="bc83e-252">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-252">**Input**:</span></span>

| <span data-ttu-id="bc83e-253">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-253">Make</span></span> | <span data-ttu-id="bc83e-254">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-254">Time</span></span> |
| --- | --- |
| <span data-ttu-id="bc83e-255">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-255">Honda</span></span> |<span data-ttu-id="bc83e-256">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-256">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="bc83e-257">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-257">Toyota</span></span> |<span data-ttu-id="bc83e-258">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-258">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="bc83e-259">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-259">**Output**:</span></span>

| <span data-ttu-id="bc83e-260">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-260">Make</span></span> | <span data-ttu-id="bc83e-261">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-261">Time</span></span> |
| --- | --- |
| <span data-ttu-id="bc83e-262">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-262">Toyota</span></span> |<span data-ttu-id="bc83e-263">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-263">2015-01-01T00:00:02.0000000Z</span></span> |

<span data-ttu-id="bc83e-264">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-264">**Solution**:</span></span>

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

<span data-ttu-id="bc83e-265">**Explication** : Utilisez **LAG** pour lire le flux d’entrée de l’événement précédent et obtenir la valeur de **Marque**.</span><span class="sxs-lookup"><span data-stu-id="bc83e-265">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="bc83e-266">Ensuite, la comparer à la valeur **Marque** de l’événement en cours, puis générer l’événement si elles sont différentes.</span><span class="sxs-lookup"><span data-stu-id="bc83e-266">Then compare it to the **Make** value on the current event and output the event if they are different.</span></span>

## <a name="query-example-find-the-first-event-in-a-window"></a><span data-ttu-id="bc83e-267">Exemple de requête : Rechercher le premier événement dans une fenêtre</span><span class="sxs-lookup"><span data-stu-id="bc83e-267">Query example: Find the first event in a window</span></span>
<span data-ttu-id="bc83e-268">**Description** : Rechercher la première voiture dans chaque intervalle de 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="bc83e-268">**Description**: Find the first car in every 10-minute interval.</span></span>

<span data-ttu-id="bc83e-269">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-269">**Input**:</span></span>

| <span data-ttu-id="bc83e-270">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="bc83e-270">LicensePlate</span></span> | <span data-ttu-id="bc83e-271">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-271">Make</span></span> | <span data-ttu-id="bc83e-272">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-272">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc83e-273">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="bc83e-273">DXE 5291</span></span> |<span data-ttu-id="bc83e-274">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-274">Honda</span></span> |<span data-ttu-id="bc83e-275">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-275">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="bc83e-276">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="bc83e-276">YZK 5704</span></span> |<span data-ttu-id="bc83e-277">Ford</span><span class="sxs-lookup"><span data-stu-id="bc83e-277">Ford</span></span> |<span data-ttu-id="bc83e-278">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-278">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="bc83e-279">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="bc83e-279">RMV 8282</span></span> |<span data-ttu-id="bc83e-280">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-280">Honda</span></span> |<span data-ttu-id="bc83e-281">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-281">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="bc83e-282">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="bc83e-282">YHN 6970</span></span> |<span data-ttu-id="bc83e-283">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-283">Toyota</span></span> |<span data-ttu-id="bc83e-284">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-284">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="bc83e-285">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="bc83e-285">VFE 1616</span></span> |<span data-ttu-id="bc83e-286">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-286">Toyota</span></span> |<span data-ttu-id="bc83e-287">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-287">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="bc83e-288">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="bc83e-288">QYF 9358</span></span> |<span data-ttu-id="bc83e-289">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-289">Honda</span></span> |<span data-ttu-id="bc83e-290">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-290">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="bc83e-291">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="bc83e-291">MDR 6128</span></span> |<span data-ttu-id="bc83e-292">BMW</span><span class="sxs-lookup"><span data-stu-id="bc83e-292">BMW</span></span> |<span data-ttu-id="bc83e-293">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-293">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="bc83e-294">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-294">**Output**:</span></span>

| <span data-ttu-id="bc83e-295">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="bc83e-295">LicensePlate</span></span> | <span data-ttu-id="bc83e-296">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-296">Make</span></span> | <span data-ttu-id="bc83e-297">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-297">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc83e-298">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="bc83e-298">DXE 5291</span></span> |<span data-ttu-id="bc83e-299">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-299">Honda</span></span> |<span data-ttu-id="bc83e-300">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-300">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="bc83e-301">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="bc83e-301">QYF 9358</span></span> |<span data-ttu-id="bc83e-302">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-302">Honda</span></span> |<span data-ttu-id="bc83e-303">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-303">2015-07-27T00:12:02.0000000Z</span></span> |

<span data-ttu-id="bc83e-304">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-304">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

<span data-ttu-id="bc83e-305">À présent, nous allons changer le problème et rechercher la première voiture d’une marque donnée dans chaque intervalle de 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="bc83e-305">Now let’s change the problem and find the first car of a particular make in every 10-minute interval.</span></span>

| <span data-ttu-id="bc83e-306">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="bc83e-306">LicensePlate</span></span> | <span data-ttu-id="bc83e-307">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-307">Make</span></span> | <span data-ttu-id="bc83e-308">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-308">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc83e-309">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="bc83e-309">DXE 5291</span></span> |<span data-ttu-id="bc83e-310">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-310">Honda</span></span> |<span data-ttu-id="bc83e-311">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-311">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="bc83e-312">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="bc83e-312">YZK 5704</span></span> |<span data-ttu-id="bc83e-313">Ford</span><span class="sxs-lookup"><span data-stu-id="bc83e-313">Ford</span></span> |<span data-ttu-id="bc83e-314">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-314">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="bc83e-315">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="bc83e-315">YHN 6970</span></span> |<span data-ttu-id="bc83e-316">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-316">Toyota</span></span> |<span data-ttu-id="bc83e-317">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-317">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="bc83e-318">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="bc83e-318">QYF 9358</span></span> |<span data-ttu-id="bc83e-319">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-319">Honda</span></span> |<span data-ttu-id="bc83e-320">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-320">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="bc83e-321">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="bc83e-321">MDR 6128</span></span> |<span data-ttu-id="bc83e-322">BMW</span><span class="sxs-lookup"><span data-stu-id="bc83e-322">BMW</span></span> |<span data-ttu-id="bc83e-323">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-323">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="bc83e-324">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-324">**Solution**:</span></span>

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-the-last-event-in-a-window"></a><span data-ttu-id="bc83e-325">Exemple de requête : Rechercher le dernier événement dans une fenêtre</span><span class="sxs-lookup"><span data-stu-id="bc83e-325">Query example: Find the last event in a window</span></span>
<span data-ttu-id="bc83e-326">**Description** : Rechercher la dernière voiture dans chaque intervalle de 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="bc83e-326">**Description**: Find the last car in every 10-minute interval.</span></span>

<span data-ttu-id="bc83e-327">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-327">**Input**:</span></span>

| <span data-ttu-id="bc83e-328">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="bc83e-328">LicensePlate</span></span> | <span data-ttu-id="bc83e-329">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-329">Make</span></span> | <span data-ttu-id="bc83e-330">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-330">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc83e-331">DXE 5291</span><span class="sxs-lookup"><span data-stu-id="bc83e-331">DXE 5291</span></span> |<span data-ttu-id="bc83e-332">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-332">Honda</span></span> |<span data-ttu-id="bc83e-333">2015-07-27T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-333">2015-07-27T00:00:05.0000000Z</span></span> |
| <span data-ttu-id="bc83e-334">YZK 5704</span><span class="sxs-lookup"><span data-stu-id="bc83e-334">YZK 5704</span></span> |<span data-ttu-id="bc83e-335">Ford</span><span class="sxs-lookup"><span data-stu-id="bc83e-335">Ford</span></span> |<span data-ttu-id="bc83e-336">2015-07-27T00:02:17.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-336">2015-07-27T00:02:17.0000000Z</span></span> |
| <span data-ttu-id="bc83e-337">RMV 8282</span><span class="sxs-lookup"><span data-stu-id="bc83e-337">RMV 8282</span></span> |<span data-ttu-id="bc83e-338">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-338">Honda</span></span> |<span data-ttu-id="bc83e-339">2015-07-27T00:05:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-339">2015-07-27T00:05:01.0000000Z</span></span> |
| <span data-ttu-id="bc83e-340">YHN 6970</span><span class="sxs-lookup"><span data-stu-id="bc83e-340">YHN 6970</span></span> |<span data-ttu-id="bc83e-341">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-341">Toyota</span></span> |<span data-ttu-id="bc83e-342">2015-07-27T00:06:00.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-342">2015-07-27T00:06:00.0000000Z</span></span> |
| <span data-ttu-id="bc83e-343">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="bc83e-343">VFE 1616</span></span> |<span data-ttu-id="bc83e-344">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-344">Toyota</span></span> |<span data-ttu-id="bc83e-345">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-345">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="bc83e-346">QYF 9358</span><span class="sxs-lookup"><span data-stu-id="bc83e-346">QYF 9358</span></span> |<span data-ttu-id="bc83e-347">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-347">Honda</span></span> |<span data-ttu-id="bc83e-348">2015-07-27T00:12:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-348">2015-07-27T00:12:02.0000000Z</span></span> |
| <span data-ttu-id="bc83e-349">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="bc83e-349">MDR 6128</span></span> |<span data-ttu-id="bc83e-350">BMW</span><span class="sxs-lookup"><span data-stu-id="bc83e-350">BMW</span></span> |<span data-ttu-id="bc83e-351">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-351">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="bc83e-352">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-352">**Output**:</span></span>

| <span data-ttu-id="bc83e-353">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="bc83e-353">LicensePlate</span></span> | <span data-ttu-id="bc83e-354">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-354">Make</span></span> | <span data-ttu-id="bc83e-355">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-355">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc83e-356">VFE 1616</span><span class="sxs-lookup"><span data-stu-id="bc83e-356">VFE 1616</span></span> |<span data-ttu-id="bc83e-357">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-357">Toyota</span></span> |<span data-ttu-id="bc83e-358">2015-07-27T00:09:31.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-358">2015-07-27T00:09:31.0000000Z</span></span> |
| <span data-ttu-id="bc83e-359">MDR 6128</span><span class="sxs-lookup"><span data-stu-id="bc83e-359">MDR 6128</span></span> |<span data-ttu-id="bc83e-360">BMW</span><span class="sxs-lookup"><span data-stu-id="bc83e-360">BMW</span></span> |<span data-ttu-id="bc83e-361">2015-07-27T00:13:45.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-361">2015-07-27T00:13:45.0000000Z</span></span> |

<span data-ttu-id="bc83e-362">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-362">**Solution**:</span></span>

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

<span data-ttu-id="bc83e-363">**Explication** : La requête comporte deux étapes.</span><span class="sxs-lookup"><span data-stu-id="bc83e-363">**Explanation**: There are two steps in the query.</span></span> <span data-ttu-id="bc83e-364">La première recherche l’horodatage le plus récent dans les fenêtres de 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="bc83e-364">The first one finds the latest time stamp in 10-minute windows.</span></span> <span data-ttu-id="bc83e-365">La deuxième joint les résultats de la première requête avec le flux d’origine pour rechercher les événements qui correspondent aux derniers horodatages dans chaque fenêtre.</span><span class="sxs-lookup"><span data-stu-id="bc83e-365">The second step joins the results of the first query with the original stream to find the events that match the last time stamps in each window.</span></span> 

## <a name="query-example-detect-the-absence-of-events"></a><span data-ttu-id="bc83e-366">Exemple de requête : Détecter l’absence d’événements</span><span class="sxs-lookup"><span data-stu-id="bc83e-366">Query example: Detect the absence of events</span></span>
<span data-ttu-id="bc83e-367">**Description** : Vérifier qu’un flux ne contient aucune valeur correspondant à certains critères.</span><span class="sxs-lookup"><span data-stu-id="bc83e-367">**Description**: Check that a stream has no value that matches a certain criterion.</span></span>
<span data-ttu-id="bc83e-368">Par exemple, deux voitures consécutives de la même marque se sont-elles engagées dans la route à péage durant les 90 dernières secondes ?</span><span class="sxs-lookup"><span data-stu-id="bc83e-368">For example, have 2 consecutive cars from the same make entered the toll road within the last 90 seconds?</span></span>

<span data-ttu-id="bc83e-369">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-369">**Input**:</span></span>

| <span data-ttu-id="bc83e-370">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-370">Make</span></span> | <span data-ttu-id="bc83e-371">LicensePlate</span><span class="sxs-lookup"><span data-stu-id="bc83e-371">LicensePlate</span></span> | <span data-ttu-id="bc83e-372">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-372">Time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc83e-373">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-373">Honda</span></span> |<span data-ttu-id="bc83e-374">ABC-123</span><span class="sxs-lookup"><span data-stu-id="bc83e-374">ABC-123</span></span> |<span data-ttu-id="bc83e-375">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-375">2015-01-01T00:00:01.0000000Z</span></span> |
| <span data-ttu-id="bc83e-376">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-376">Honda</span></span> |<span data-ttu-id="bc83e-377">AAA-999</span><span class="sxs-lookup"><span data-stu-id="bc83e-377">AAA-999</span></span> |<span data-ttu-id="bc83e-378">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-378">2015-01-01T00:00:02.0000000Z</span></span> |
| <span data-ttu-id="bc83e-379">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-379">Toyota</span></span> |<span data-ttu-id="bc83e-380">DEF-987</span><span class="sxs-lookup"><span data-stu-id="bc83e-380">DEF-987</span></span> |<span data-ttu-id="bc83e-381">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-381">2015-01-01T00:00:03.0000000Z</span></span> |
| <span data-ttu-id="bc83e-382">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-382">Honda</span></span> |<span data-ttu-id="bc83e-383">GHI-345</span><span class="sxs-lookup"><span data-stu-id="bc83e-383">GHI-345</span></span> |<span data-ttu-id="bc83e-384">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-384">2015-01-01T00:00:04.0000000Z</span></span> |

<span data-ttu-id="bc83e-385">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-385">**Output**:</span></span>

| <span data-ttu-id="bc83e-386">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-386">Make</span></span> | <span data-ttu-id="bc83e-387">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-387">Time</span></span> | <span data-ttu-id="bc83e-388">CurrentCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="bc83e-388">CurrentCarLicensePlate</span></span> | <span data-ttu-id="bc83e-389">FirstCarLicensePlate</span><span class="sxs-lookup"><span data-stu-id="bc83e-389">FirstCarLicensePlate</span></span> | <span data-ttu-id="bc83e-390">FirstCarTime</span><span class="sxs-lookup"><span data-stu-id="bc83e-390">FirstCarTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="bc83e-391">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-391">Honda</span></span> |<span data-ttu-id="bc83e-392">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-392">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="bc83e-393">AAA-999</span><span class="sxs-lookup"><span data-stu-id="bc83e-393">AAA-999</span></span> |<span data-ttu-id="bc83e-394">ABC-123</span><span class="sxs-lookup"><span data-stu-id="bc83e-394">ABC-123</span></span> |<span data-ttu-id="bc83e-395">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-395">2015-01-01T00:00:01.0000000Z</span></span> |

<span data-ttu-id="bc83e-396">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-396">**Solution**:</span></span>

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

<span data-ttu-id="bc83e-397">**Explication** : Utilisez **LAG** pour lire le flux d’entrée de l’événement précédent et obtenir la valeur de **Marque**.</span><span class="sxs-lookup"><span data-stu-id="bc83e-397">**Explanation**: Use **LAG** to peek into the input stream one event back and get the **Make** value.</span></span> <span data-ttu-id="bc83e-398">La comparer à la valeur **Marque** de l’événement en cours, puis générer l’événement si elles sont identiques.</span><span class="sxs-lookup"><span data-stu-id="bc83e-398">Compare it to the **MAKE** value in the current event, and then output the event if they are the same.</span></span> <span data-ttu-id="bc83e-399">Vous pouvez également utiliser **LAG** pour obtenir des données relatives à la voiture précédente.</span><span class="sxs-lookup"><span data-stu-id="bc83e-399">You can also use **LAG** to get data about the previous car.</span></span>

## <a name="query-example-detect-the-duration-between-events"></a><span data-ttu-id="bc83e-400">Exemple de requête : Détecter la durée entre des événements</span><span class="sxs-lookup"><span data-stu-id="bc83e-400">Query example: Detect the duration between events</span></span>
<span data-ttu-id="bc83e-401">**Description** : Rechercher la durée d’un événement donné.</span><span class="sxs-lookup"><span data-stu-id="bc83e-401">**Description**: Find the duration of a given event.</span></span> <span data-ttu-id="bc83e-402">Par exemple, sur la base d’un parcours web, déterminer le temps passé sur une fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bc83e-402">For example, given a web clickstream, determine the time spent on a feature.</span></span>

<span data-ttu-id="bc83e-403">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-403">**Input**:</span></span>  

| <span data-ttu-id="bc83e-404">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="bc83e-404">User</span></span> | <span data-ttu-id="bc83e-405">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="bc83e-405">Feature</span></span> | <span data-ttu-id="bc83e-406">Événement</span><span class="sxs-lookup"><span data-stu-id="bc83e-406">Event</span></span> | <span data-ttu-id="bc83e-407">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-407">Time</span></span> |
| --- | --- | --- | --- |
| user@location.com |<span data-ttu-id="bc83e-408">RightMenu</span><span class="sxs-lookup"><span data-stu-id="bc83e-408">RightMenu</span></span> |<span data-ttu-id="bc83e-409">Démarrer</span><span class="sxs-lookup"><span data-stu-id="bc83e-409">Start</span></span> |<span data-ttu-id="bc83e-410">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-410">2015-01-01T00:00:01.0000000Z</span></span> |
| user@location.com |<span data-ttu-id="bc83e-411">RightMenu</span><span class="sxs-lookup"><span data-stu-id="bc83e-411">RightMenu</span></span> |<span data-ttu-id="bc83e-412">Terminer</span><span class="sxs-lookup"><span data-stu-id="bc83e-412">End</span></span> |<span data-ttu-id="bc83e-413">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-413">2015-01-01T00:00:08.0000000Z</span></span> |

<span data-ttu-id="bc83e-414">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-414">**Output**:</span></span>  

| <span data-ttu-id="bc83e-415">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="bc83e-415">User</span></span> | <span data-ttu-id="bc83e-416">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="bc83e-416">Feature</span></span> | <span data-ttu-id="bc83e-417">Durée</span><span class="sxs-lookup"><span data-stu-id="bc83e-417">Duration</span></span> |
| --- | --- | --- |
| user@location.com |<span data-ttu-id="bc83e-418">RightMenu</span><span class="sxs-lookup"><span data-stu-id="bc83e-418">RightMenu</span></span> |<span data-ttu-id="bc83e-419">7</span><span class="sxs-lookup"><span data-stu-id="bc83e-419">7</span></span> |

<span data-ttu-id="bc83e-420">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-420">**Solution**:</span></span>

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

<span data-ttu-id="bc83e-421">**Explication** : Utilisez la fonction **LAST** pour récupérer la dernière valeur **TEMPS** quand le type d’événement était **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="bc83e-421">**Explanation**: Use the **LAST** function to retrieve the last **TIME** value when the event type was **Start**.</span></span> <span data-ttu-id="bc83e-422">Notez que la fonction **LAST** utilise **PARTITION BY [user]** pour indiquer que le résultat est calculé par utilisateur unique.</span><span class="sxs-lookup"><span data-stu-id="bc83e-422">The **LAST** function uses **PARTITION BY [user]** to indicate that the result is computed per unique user.</span></span> <span data-ttu-id="bc83e-423">La requête a un seuil maximal d’une heure pour la différence de temps entre les événements **Démarrer** et **Terminer** **(LIMIT DURATION(hour, 1)**, mais ce seuil est configurable en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="bc83e-423">The query has a 1-hour maximum threshold for the time difference between **Start** and **Stop** events, but is configurable as needed **(LIMIT DURATION(hour, 1)**.</span></span>

## <a name="query-example-detect-the-duration-of-a-condition"></a><span data-ttu-id="bc83e-424">Exemple de requête : Détecter la durée d’une condition</span><span class="sxs-lookup"><span data-stu-id="bc83e-424">Query example: Detect the duration of a condition</span></span>
<span data-ttu-id="bc83e-425">**Description** : Rechercher la durée pendant laquelle une condition s’est produite.</span><span class="sxs-lookup"><span data-stu-id="bc83e-425">**Description**: Find out how long a condition occurred.</span></span>
<span data-ttu-id="bc83e-426">Par exemple, supposez qu’à la suite d’un bogue, le poids de toutes les voitures est incorrect (supérieur à 20 000 livres).</span><span class="sxs-lookup"><span data-stu-id="bc83e-426">For example, suppose that a bug resulted in all cars having an incorrect weight (above 20,000 pounds).</span></span> <span data-ttu-id="bc83e-427">Nous voulons calculer la durée du bogue.</span><span class="sxs-lookup"><span data-stu-id="bc83e-427">We want to compute the duration of the bug.</span></span>

<span data-ttu-id="bc83e-428">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-428">**Input**:</span></span>

| <span data-ttu-id="bc83e-429">Marque</span><span class="sxs-lookup"><span data-stu-id="bc83e-429">Make</span></span> | <span data-ttu-id="bc83e-430">Temps</span><span class="sxs-lookup"><span data-stu-id="bc83e-430">Time</span></span> | <span data-ttu-id="bc83e-431">Poids</span><span class="sxs-lookup"><span data-stu-id="bc83e-431">Weight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc83e-432">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-432">Honda</span></span> |<span data-ttu-id="bc83e-433">2015-01-01T00:00:01.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-433">2015-01-01T00:00:01.0000000Z</span></span> |<span data-ttu-id="bc83e-434">2000</span><span class="sxs-lookup"><span data-stu-id="bc83e-434">2000</span></span> |
| <span data-ttu-id="bc83e-435">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-435">Toyota</span></span> |<span data-ttu-id="bc83e-436">2015-01-01T00:00:02.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-436">2015-01-01T00:00:02.0000000Z</span></span> |<span data-ttu-id="bc83e-437">25000</span><span class="sxs-lookup"><span data-stu-id="bc83e-437">25000</span></span> |
| <span data-ttu-id="bc83e-438">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-438">Honda</span></span> |<span data-ttu-id="bc83e-439">2015-01-01T00:00:03.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-439">2015-01-01T00:00:03.0000000Z</span></span> |<span data-ttu-id="bc83e-440">26000</span><span class="sxs-lookup"><span data-stu-id="bc83e-440">26000</span></span> |
| <span data-ttu-id="bc83e-441">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-441">Toyota</span></span> |<span data-ttu-id="bc83e-442">2015-01-01T00:00:04.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-442">2015-01-01T00:00:04.0000000Z</span></span> |<span data-ttu-id="bc83e-443">25000</span><span class="sxs-lookup"><span data-stu-id="bc83e-443">25000</span></span> |
| <span data-ttu-id="bc83e-444">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-444">Honda</span></span> |<span data-ttu-id="bc83e-445">2015-01-01T00:00:05.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-445">2015-01-01T00:00:05.0000000Z</span></span> |<span data-ttu-id="bc83e-446">26000</span><span class="sxs-lookup"><span data-stu-id="bc83e-446">26000</span></span> |
| <span data-ttu-id="bc83e-447">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-447">Toyota</span></span> |<span data-ttu-id="bc83e-448">2015-01-01T00:00:06.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-448">2015-01-01T00:00:06.0000000Z</span></span> |<span data-ttu-id="bc83e-449">25000</span><span class="sxs-lookup"><span data-stu-id="bc83e-449">25000</span></span> |
| <span data-ttu-id="bc83e-450">Honda</span><span class="sxs-lookup"><span data-stu-id="bc83e-450">Honda</span></span> |<span data-ttu-id="bc83e-451">2015-01-01T00:00:07.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-451">2015-01-01T00:00:07.0000000Z</span></span> |<span data-ttu-id="bc83e-452">26000</span><span class="sxs-lookup"><span data-stu-id="bc83e-452">26000</span></span> |
| <span data-ttu-id="bc83e-453">Toyota</span><span class="sxs-lookup"><span data-stu-id="bc83e-453">Toyota</span></span> |<span data-ttu-id="bc83e-454">2015-01-01T00:00:08.0000000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-454">2015-01-01T00:00:08.0000000Z</span></span> |<span data-ttu-id="bc83e-455">2000</span><span class="sxs-lookup"><span data-stu-id="bc83e-455">2000</span></span> |

<span data-ttu-id="bc83e-456">**Sortie**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-456">**Output**:</span></span>

| <span data-ttu-id="bc83e-457">StartFault</span><span class="sxs-lookup"><span data-stu-id="bc83e-457">StartFault</span></span> | <span data-ttu-id="bc83e-458">EndFault</span><span class="sxs-lookup"><span data-stu-id="bc83e-458">EndFault</span></span> |
| --- | --- |
| <span data-ttu-id="bc83e-459">2015-01-01T00:00:02.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-459">2015-01-01T00:00:02.000Z</span></span> |<span data-ttu-id="bc83e-460">2015-01-01T00:00:07.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-460">2015-01-01T00:00:07.000Z</span></span> |

<span data-ttu-id="bc83e-461">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-461">**Solution**:</span></span>

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

<span data-ttu-id="bc83e-462">**Explication** : Utilisez **LAG** pour afficher le flux d’entrée sur 24 heures et recherchez les instances dans lesquelles **StartFault** et **StopFault** sont couvertes par la condition « weight < 20000 » (poids inférieur à 20 000 livres).</span><span class="sxs-lookup"><span data-stu-id="bc83e-462">**Explanation**: Use **LAG** to view the input stream for 24 hours and look for instances where **StartFault** and **StopFault** are spanned by the weight < 20000.</span></span>

## <a name="query-example-fill-missing-values"></a><span data-ttu-id="bc83e-463">Exemple de requête : Remplir les valeurs manquantes</span><span class="sxs-lookup"><span data-stu-id="bc83e-463">Query example: Fill missing values</span></span>
<span data-ttu-id="bc83e-464">**Description** : Pour le flux des événements qui ont des valeurs manquantes, produire un flux d’événements à intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="bc83e-464">**Description**: For the stream of events that have missing values, produce a stream of events with regular intervals.</span></span>
<span data-ttu-id="bc83e-465">Par exemple, générer toutes les cinq secondes un événement qui indique le point de données le plus récemment observé.</span><span class="sxs-lookup"><span data-stu-id="bc83e-465">For example, generate an event every 5 seconds that reports the most recently seen data point.</span></span>

<span data-ttu-id="bc83e-466">**Entrée**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-466">**Input**:</span></span>

| <span data-ttu-id="bc83e-467">t</span><span class="sxs-lookup"><span data-stu-id="bc83e-467">t</span></span> | <span data-ttu-id="bc83e-468">value</span><span class="sxs-lookup"><span data-stu-id="bc83e-468">value</span></span> |
| --- | --- |
| <span data-ttu-id="bc83e-469">"2014-01-01T06:01:00"</span><span class="sxs-lookup"><span data-stu-id="bc83e-469">"2014-01-01T06:01:00"</span></span> |<span data-ttu-id="bc83e-470">1</span><span class="sxs-lookup"><span data-stu-id="bc83e-470">1</span></span> |
| <span data-ttu-id="bc83e-471">"2014-01-01T06:01:05"</span><span class="sxs-lookup"><span data-stu-id="bc83e-471">"2014-01-01T06:01:05"</span></span> |<span data-ttu-id="bc83e-472">2</span><span class="sxs-lookup"><span data-stu-id="bc83e-472">2</span></span> |
| <span data-ttu-id="bc83e-473">"2014-01-01T06:01:10"</span><span class="sxs-lookup"><span data-stu-id="bc83e-473">"2014-01-01T06:01:10"</span></span> |<span data-ttu-id="bc83e-474">3</span><span class="sxs-lookup"><span data-stu-id="bc83e-474">3</span></span> |
| <span data-ttu-id="bc83e-475">"2014-01-01T06:01:15"</span><span class="sxs-lookup"><span data-stu-id="bc83e-475">"2014-01-01T06:01:15"</span></span> |<span data-ttu-id="bc83e-476">4</span><span class="sxs-lookup"><span data-stu-id="bc83e-476">4</span></span> |
| <span data-ttu-id="bc83e-477">"2014-01-01T06:01:30"</span><span class="sxs-lookup"><span data-stu-id="bc83e-477">"2014-01-01T06:01:30"</span></span> |<span data-ttu-id="bc83e-478">5</span><span class="sxs-lookup"><span data-stu-id="bc83e-478">5</span></span> |
| <span data-ttu-id="bc83e-479">"2014-01-01T06:01:35"</span><span class="sxs-lookup"><span data-stu-id="bc83e-479">"2014-01-01T06:01:35"</span></span> |<span data-ttu-id="bc83e-480">6</span><span class="sxs-lookup"><span data-stu-id="bc83e-480">6</span></span> |

<span data-ttu-id="bc83e-481">**Sortie (10 premières lignes)**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-481">**Output (first 10 rows)**:</span></span>

| <span data-ttu-id="bc83e-482">windowend</span><span class="sxs-lookup"><span data-stu-id="bc83e-482">windowend</span></span> | <span data-ttu-id="bc83e-483">lastevent.t</span><span class="sxs-lookup"><span data-stu-id="bc83e-483">lastevent.t</span></span> | <span data-ttu-id="bc83e-484">lastevent.value</span><span class="sxs-lookup"><span data-stu-id="bc83e-484">lastevent.value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc83e-485">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-485">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="bc83e-486">2014-01-01T14:01:00.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-486">2014-01-01T14:01:00.000Z</span></span> |<span data-ttu-id="bc83e-487">1</span><span class="sxs-lookup"><span data-stu-id="bc83e-487">1</span></span> |
| <span data-ttu-id="bc83e-488">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-488">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="bc83e-489">2014-01-01T14:01:05.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-489">2014-01-01T14:01:05.000Z</span></span> |<span data-ttu-id="bc83e-490">2</span><span class="sxs-lookup"><span data-stu-id="bc83e-490">2</span></span> |
| <span data-ttu-id="bc83e-491">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-491">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="bc83e-492">2014-01-01T14:01:10.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-492">2014-01-01T14:01:10.000Z</span></span> |<span data-ttu-id="bc83e-493">3</span><span class="sxs-lookup"><span data-stu-id="bc83e-493">3</span></span> |
| <span data-ttu-id="bc83e-494">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-494">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="bc83e-495">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-495">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="bc83e-496">4</span><span class="sxs-lookup"><span data-stu-id="bc83e-496">4</span></span> |
| <span data-ttu-id="bc83e-497">2014-01-01T14:01:20.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-497">2014-01-01T14:01:20.000Z</span></span> |<span data-ttu-id="bc83e-498">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-498">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="bc83e-499">4</span><span class="sxs-lookup"><span data-stu-id="bc83e-499">4</span></span> |
| <span data-ttu-id="bc83e-500">2014-01-01T14:01:25.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-500">2014-01-01T14:01:25.000Z</span></span> |<span data-ttu-id="bc83e-501">2014-01-01T14:01:15.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-501">2014-01-01T14:01:15.000Z</span></span> |<span data-ttu-id="bc83e-502">4</span><span class="sxs-lookup"><span data-stu-id="bc83e-502">4</span></span> |
| <span data-ttu-id="bc83e-503">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-503">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="bc83e-504">2014-01-01T14:01:30.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-504">2014-01-01T14:01:30.000Z</span></span> |<span data-ttu-id="bc83e-505">5</span><span class="sxs-lookup"><span data-stu-id="bc83e-505">5</span></span> |
| <span data-ttu-id="bc83e-506">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-506">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="bc83e-507">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-507">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="bc83e-508">6</span><span class="sxs-lookup"><span data-stu-id="bc83e-508">6</span></span> |
| <span data-ttu-id="bc83e-509">2014-01-01T14:01:40.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-509">2014-01-01T14:01:40.000Z</span></span> |<span data-ttu-id="bc83e-510">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-510">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="bc83e-511">6</span><span class="sxs-lookup"><span data-stu-id="bc83e-511">6</span></span> |
| <span data-ttu-id="bc83e-512">2014-01-01T14:01:45.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-512">2014-01-01T14:01:45.000Z</span></span> |<span data-ttu-id="bc83e-513">2014-01-01T14:01:35.000Z</span><span class="sxs-lookup"><span data-stu-id="bc83e-513">2014-01-01T14:01:35.000Z</span></span> |<span data-ttu-id="bc83e-514">6</span><span class="sxs-lookup"><span data-stu-id="bc83e-514">6</span></span> |

<span data-ttu-id="bc83e-515">**Solution**:</span><span class="sxs-lookup"><span data-stu-id="bc83e-515">**Solution**:</span></span>

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


<span data-ttu-id="bc83e-516">**Explication** : Cette requête génère des événements toutes les cinq secondes et indique le dernier événement précédemment reçu.</span><span class="sxs-lookup"><span data-stu-id="bc83e-516">**Explanation**: This query generates events every 5 seconds and outputs the last event that was received previously.</span></span> <span data-ttu-id="bc83e-517">La [Fenêtre récurrente](https://msdn.microsoft.com/library/dn835041.aspx "Fenêtre récurrente - Azure Stream Analytics") détermine la période que la requête remonte pour rechercher le dernier événement (300 secondes, dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="bc83e-517">The [Hopping window](https://msdn.microsoft.com/library/dn835041.aspx "Hopping window--Azure Stream Analytics") duration determines how far back the query looks to find the latest event (300 seconds in this example).</span></span>

## <a name="get-help"></a><span data-ttu-id="bc83e-518">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="bc83e-518">Get help</span></span>
<span data-ttu-id="bc83e-519">Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="bc83e-519">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc83e-520">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bc83e-520">Next steps</span></span>
* [<span data-ttu-id="bc83e-521">Présentation d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bc83e-521">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="bc83e-522">Prise en main d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bc83e-522">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="bc83e-523">Mise à l'échelle des travaux Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bc83e-523">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="bc83e-524">Références sur le langage des requêtes d'Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bc83e-524">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="bc83e-525">Références sur l’API REST de gestion d’Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bc83e-525">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

