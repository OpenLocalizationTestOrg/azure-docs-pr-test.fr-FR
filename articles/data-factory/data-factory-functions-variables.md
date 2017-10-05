---
title: "Variables système et fonctions Data Factory | Microsoft Docs"
description: "Fournit la liste des variables système et fonctions Azure Data Factory"
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 72a966bdc271f86b9568d3310d2e22d83b447594
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="31eb3-103">Azure Data Factory - Variables système et fonctions</span><span class="sxs-lookup"><span data-stu-id="31eb3-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="31eb3-104">Cet article fournit des informations sur les fonctions et variables prises en charge par Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="31eb3-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="31eb3-105">Variables système Data Factory</span><span class="sxs-lookup"><span data-stu-id="31eb3-105">Data Factory system variables</span></span>
| <span data-ttu-id="31eb3-106">Nom de la variable</span><span class="sxs-lookup"><span data-stu-id="31eb3-106">Variable Name</span></span> | <span data-ttu-id="31eb3-107">Description</span><span class="sxs-lookup"><span data-stu-id="31eb3-107">Description</span></span> | <span data-ttu-id="31eb3-108">Portée de l’objet</span><span class="sxs-lookup"><span data-stu-id="31eb3-108">Object Scope</span></span> | <span data-ttu-id="31eb3-109">Étendue JSON et cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="31eb3-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="31eb3-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="31eb3-110">WindowStart</span></span> |<span data-ttu-id="31eb3-111">Début de l’intervalle de temps pour l’intervalle d’exécution d’activité en cours</span><span class="sxs-lookup"><span data-stu-id="31eb3-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="31eb3-112">activité</span><span class="sxs-lookup"><span data-stu-id="31eb3-112">activity</span></span> |<ol><li><span data-ttu-id="31eb3-113">Spécifier des requêtes de sélection de données.</span><span class="sxs-lookup"><span data-stu-id="31eb3-113">Specify data selection queries.</span></span> <span data-ttu-id="31eb3-114">Consultez les articles connexes référencés par l’article [Activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="31eb3-114">See connector articles referenced in the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="31eb3-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="31eb3-115">WindowEnd</span></span> |<span data-ttu-id="31eb3-116">Fin de l’intervalle de temps de l’intervalle d’exécution d’activité en cours</span><span class="sxs-lookup"><span data-stu-id="31eb3-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="31eb3-117">activité</span><span class="sxs-lookup"><span data-stu-id="31eb3-117">activity</span></span> |<span data-ttu-id="31eb3-118">identique à WindowStart.</span><span class="sxs-lookup"><span data-stu-id="31eb3-118">same as WindowStart.</span></span> |
| <span data-ttu-id="31eb3-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="31eb3-119">SliceStart</span></span> |<span data-ttu-id="31eb3-120">Début de l’intervalle de temps pour une tranche de données en cours de génération</span><span class="sxs-lookup"><span data-stu-id="31eb3-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="31eb3-121">activité</span><span class="sxs-lookup"><span data-stu-id="31eb3-121">activity</span></span><br/><span data-ttu-id="31eb3-122">jeu de données</span><span class="sxs-lookup"><span data-stu-id="31eb3-122">dataset</span></span> |<ol><li><span data-ttu-id="31eb3-123">Spécifier les chemins d’accès et les noms de fichiers dynamiques tout en travaillant avec [Blob Azure](data-factory-azure-blob-connector.md) et [Jeux de données du système de fichiers](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="31eb3-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="31eb3-124">Spécifier les dépendances d’entrée avec les fonctions Data Factory dans la collecte d’activité.</span><span class="sxs-lookup"><span data-stu-id="31eb3-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="31eb3-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="31eb3-125">SliceEnd</span></span> |<span data-ttu-id="31eb3-126">Fin de l’intervalle de temps pour la tranche de données en cours.</span><span class="sxs-lookup"><span data-stu-id="31eb3-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="31eb3-127">activité</span><span class="sxs-lookup"><span data-stu-id="31eb3-127">activity</span></span><br/><span data-ttu-id="31eb3-128">dataset</span><span class="sxs-lookup"><span data-stu-id="31eb3-128">dataset</span></span> |<span data-ttu-id="31eb3-129">identique à SliceStart.</span><span class="sxs-lookup"><span data-stu-id="31eb3-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="31eb3-130">Actuellement, la fabrique de données exige que le calendrier spécifié dans l’activité corresponde exactement à la planification spécifiée dans la disponibilité du jeu de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="31eb3-130">Currently data factory requires that the schedule specified in the activity exactly matches the schedule specified in availability of the output dataset.</span></span> <span data-ttu-id="31eb3-131">Ainsi, WindowStart, WindowEnd, SliceStart et SliceEnd font toujours correspondre la même période de temps et une tranche de sortie unique.</span><span class="sxs-lookup"><span data-stu-id="31eb3-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map to the same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="31eb3-132">Exemple d’utilisation d’une variable système</span><span class="sxs-lookup"><span data-stu-id="31eb3-132">Example for using a system variable</span></span>
<span data-ttu-id="31eb3-133">Dans l’exemple suivant, l’année, le mois, le jour et l’heure de **SliceStart** sont extraits dans des variables distinctes qui sont utilisées par les propriétés **folderPath** et **fileName**.</span><span class="sxs-lookup"><span data-stu-id="31eb3-133">In the following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a><span data-ttu-id="31eb3-134">Fonctions Data Factory</span><span class="sxs-lookup"><span data-stu-id="31eb3-134">Data Factory functions</span></span>
<span data-ttu-id="31eb3-135">Vous pouvez utiliser des fonctions dans Data Factory avec les variables système aux fins suivantes :</span><span class="sxs-lookup"><span data-stu-id="31eb3-135">You can use functions in data factory along with system variables for the following purposes:</span></span>

1. <span data-ttu-id="31eb3-136">Spécification de requêtes de sélection de données (consultez les articles connexes référencés par l’article [Activités de déplacement des données](data-factory-data-movement-activities.md) ).</span><span class="sxs-lookup"><span data-stu-id="31eb3-136">Specifying data selection queries (see connector articles referenced by the [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="31eb3-137">La syntaxe pour appeler une fonction Data Factory est : **$$<function>** pour les requêtes de sélection de données et d’autres propriétés de l’activité et des jeux de données.</span><span class="sxs-lookup"><span data-stu-id="31eb3-137">The syntax to invoke a data factory function is: **$$<function>** for data selection queries and other properties in the activity and datasets.</span></span>  
2. <span data-ttu-id="31eb3-138">Spécifier les dépendances d’entrée avec les fonctions Data Factory dans la collecte d’entrées d’activité.</span><span class="sxs-lookup"><span data-stu-id="31eb3-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="31eb3-139">$$ n’est pas nécessaire pour spécifier des expressions de dépendance d’entrée.</span><span class="sxs-lookup"><span data-stu-id="31eb3-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="31eb3-140">Dans l’exemple suivant, la propriété **sqlReaderQuery** d’un fichier JSON est affectée à une valeur renvoyée par la fonction `Text.Format`.</span><span class="sxs-lookup"><span data-stu-id="31eb3-140">In the following sample, **sqlReaderQuery** property in a JSON file is assigned to a value returned by the `Text.Format` function.</span></span> <span data-ttu-id="31eb3-141">Cet exemple utilise également une variable système nommée **WindowStart**, qui représente l’heure de début de la fenêtre d’activité à exécuter.</span><span class="sxs-lookup"><span data-stu-id="31eb3-141">This sample also uses a system variable named **WindowStart**, which represents the start time of the activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="31eb3-142">Consultez la rubrique [Chaînes de format de date et d’heure personnalisées](https://msdn.microsoft.com/library/8kb3ddd4.aspx) , qui décrit les différentes options de formatage que vous pouvez utiliser (par exemple : aa et aaaa).</span><span class="sxs-lookup"><span data-stu-id="31eb3-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="31eb3-143">Fonctions</span><span class="sxs-lookup"><span data-stu-id="31eb3-143">Functions</span></span>
<span data-ttu-id="31eb3-144">Les tables qui suivent répertorient toutes les fonctions dans Azure Data Factory :</span><span class="sxs-lookup"><span data-stu-id="31eb3-144">The following tables list all the functions in Azure Data Factory:</span></span>

| <span data-ttu-id="31eb3-145">Catégorie</span><span class="sxs-lookup"><span data-stu-id="31eb3-145">Category</span></span> | <span data-ttu-id="31eb3-146">Fonction</span><span class="sxs-lookup"><span data-stu-id="31eb3-146">Function</span></span> | <span data-ttu-id="31eb3-147">Paramètres</span><span class="sxs-lookup"><span data-stu-id="31eb3-147">Parameters</span></span> | <span data-ttu-id="31eb3-148">Description</span><span class="sxs-lookup"><span data-stu-id="31eb3-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="31eb3-149">Time</span><span class="sxs-lookup"><span data-stu-id="31eb3-149">Time</span></span> |<span data-ttu-id="31eb3-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="31eb3-150">AddHours(X,Y)</span></span> |<span data-ttu-id="31eb3-151">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="31eb3-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="31eb3-152">Y: int</span></span> |<span data-ttu-id="31eb3-153">Ajoute Y heures à l’heure donnée X.</span><span class="sxs-lookup"><span data-stu-id="31eb3-153">Adds Y hours to the given time X.</span></span> <br/><br/><span data-ttu-id="31eb3-154">Exemple : `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="31eb3-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="31eb3-155">Temps</span><span class="sxs-lookup"><span data-stu-id="31eb3-155">Time</span></span> |<span data-ttu-id="31eb3-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="31eb3-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="31eb3-157">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="31eb3-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="31eb3-158">Y: int</span></span> |<span data-ttu-id="31eb3-159">Ajoute Y minutes à X.</span><span class="sxs-lookup"><span data-stu-id="31eb3-159">Adds Y minutes to X.</span></span><br/><br/><span data-ttu-id="31eb3-160">Exemple : `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="31eb3-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="31eb3-161">Temps</span><span class="sxs-lookup"><span data-stu-id="31eb3-161">Time</span></span> |<span data-ttu-id="31eb3-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="31eb3-162">StartOfHour(X)</span></span> |<span data-ttu-id="31eb3-163">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-163">X: Datetime</span></span> |<span data-ttu-id="31eb3-164">Obtient l’heure de début de l’heure représentée par le composant heure de X.</span><span class="sxs-lookup"><span data-stu-id="31eb3-164">Gets the starting time for the hour represented by the hour component of X.</span></span> <br/><br/><span data-ttu-id="31eb3-165">Exemple : `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="31eb3-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="31eb3-166">Date</span><span class="sxs-lookup"><span data-stu-id="31eb3-166">Date</span></span> |<span data-ttu-id="31eb3-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="31eb3-167">AddDays(X,Y)</span></span> |<span data-ttu-id="31eb3-168">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-168">X: DateTime</span></span><br/><br/><span data-ttu-id="31eb3-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="31eb3-169">Y: int</span></span> |<span data-ttu-id="31eb3-170">Ajoute Y jours à X.</span><span class="sxs-lookup"><span data-stu-id="31eb3-170">Adds Y days to X.</span></span> <br/><br/><span data-ttu-id="31eb3-171">Exemple : 9/15/2013 12:00:00 PM + 2 jours = 9/17/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="31eb3-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="31eb3-172">Vous pouvez également soustraire les jours en spécifiant Y en tant que nombre négatif.</span><span class="sxs-lookup"><span data-stu-id="31eb3-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="31eb3-173">Exemple : `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="31eb3-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="31eb3-174">Date</span><span class="sxs-lookup"><span data-stu-id="31eb3-174">Date</span></span> |<span data-ttu-id="31eb3-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="31eb3-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="31eb3-176">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-176">X: DateTime</span></span><br/><br/><span data-ttu-id="31eb3-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="31eb3-177">Y: int</span></span> |<span data-ttu-id="31eb3-178">Ajoute Y mois à X.</span><span class="sxs-lookup"><span data-stu-id="31eb3-178">Adds Y months to X.</span></span><br/><br/><span data-ttu-id="31eb3-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="31eb3-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="31eb3-180">Vous pouvez également soustraire les mois en spécifiant Y en tant que nombre négatif.</span><span class="sxs-lookup"><span data-stu-id="31eb3-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="31eb3-181">Exemple : `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="31eb3-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="31eb3-182">Date</span><span class="sxs-lookup"><span data-stu-id="31eb3-182">Date</span></span> |<span data-ttu-id="31eb3-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="31eb3-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="31eb3-184">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="31eb3-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="31eb3-185">Y: int</span></span> |<span data-ttu-id="31eb3-186">Ajoute Y * 3 mois à X.</span><span class="sxs-lookup"><span data-stu-id="31eb3-186">Adds Y * 3 months to X.</span></span><br/><br/><span data-ttu-id="31eb3-187">Exemple : `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="31eb3-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="31eb3-188">Date</span><span class="sxs-lookup"><span data-stu-id="31eb3-188">Date</span></span> |<span data-ttu-id="31eb3-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="31eb3-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="31eb3-190">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-190">X: DateTime</span></span><br/><br/><span data-ttu-id="31eb3-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="31eb3-191">Y: int</span></span> |<span data-ttu-id="31eb3-192">Ajoute Y * 7 jours à X</span><span class="sxs-lookup"><span data-stu-id="31eb3-192">Adds Y * 7 days to X</span></span><br/><br/><span data-ttu-id="31eb3-193">Exemple : 15/9/2013 12:00:00 PM + 1 semaine = 22/9/2013 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="31eb3-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="31eb3-194">Vous pouvez également soustraire les semaines en spécifiant Y en tant que nombre négatif.</span><span class="sxs-lookup"><span data-stu-id="31eb3-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="31eb3-195">Exemple : `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="31eb3-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="31eb3-196">Date</span><span class="sxs-lookup"><span data-stu-id="31eb3-196">Date</span></span> |<span data-ttu-id="31eb3-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="31eb3-197">AddYears(X,Y)</span></span> |<span data-ttu-id="31eb3-198">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-198">X: DateTime</span></span><br/><br/><span data-ttu-id="31eb3-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="31eb3-199">Y: int</span></span> |<span data-ttu-id="31eb3-200">Ajoute Y années à X.</span><span class="sxs-lookup"><span data-stu-id="31eb3-200">Adds Y years to X.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="31eb3-201">Vous pouvez également soustraire les années en spécifiant Y en tant que nombre négatif.</span><span class="sxs-lookup"><span data-stu-id="31eb3-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="31eb3-202">Exemple : `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="31eb3-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="31eb3-203">Date</span><span class="sxs-lookup"><span data-stu-id="31eb3-203">Date</span></span> |<span data-ttu-id="31eb3-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="31eb3-204">Day(X)</span></span> |<span data-ttu-id="31eb3-205">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-205">X: DateTime</span></span> |<span data-ttu-id="31eb3-206">Obtient le composant jour de X.</span><span class="sxs-lookup"><span data-stu-id="31eb3-206">Gets the day component of X.</span></span><br/><br/><span data-ttu-id="31eb3-207">Exemple : `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="31eb3-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="31eb3-208">Date</span><span class="sxs-lookup"><span data-stu-id="31eb3-208">Date</span></span> |<span data-ttu-id="31eb3-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="31eb3-209">DayOfWeek(X)</span></span> |<span data-ttu-id="31eb3-210">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-210">X: DateTime</span></span> |<span data-ttu-id="31eb3-211">Obtient le composant semaine de X.</span><span class="sxs-lookup"><span data-stu-id="31eb3-211">Gets the day of week component of X.</span></span><br/><br/><span data-ttu-id="31eb3-212">Exemple : `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="31eb3-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="31eb3-213">Date</span><span class="sxs-lookup"><span data-stu-id="31eb3-213">Date</span></span> |<span data-ttu-id="31eb3-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="31eb3-214">DayOfYear(X)</span></span> |<span data-ttu-id="31eb3-215">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-215">X: DateTime</span></span> |<span data-ttu-id="31eb3-216">Permet d’obtenir le jour de l’année représenté par le composant année de X.</span><span class="sxs-lookup"><span data-stu-id="31eb3-216">Gets the day in the year represented by the year component of X.</span></span><br/><br/><span data-ttu-id="31eb3-217">Exemples :</span><span class="sxs-lookup"><span data-stu-id="31eb3-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="31eb3-218">Date</span><span class="sxs-lookup"><span data-stu-id="31eb3-218">Date</span></span> |<span data-ttu-id="31eb3-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="31eb3-219">DaysInMonth(X)</span></span> |<span data-ttu-id="31eb3-220">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-220">X: DateTime</span></span> |<span data-ttu-id="31eb3-221">Permet d’obtenir les jours du mois représentés par le composant mois du paramètre X.</span><span class="sxs-lookup"><span data-stu-id="31eb3-221">Gets the days in the month represented by the month component of parameter X.</span></span><br/><br/><span data-ttu-id="31eb3-222">Exemple : `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span><span class="sxs-lookup"><span data-stu-id="31eb3-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in the September month`.</span></span> |
| <span data-ttu-id="31eb3-223">Date</span><span class="sxs-lookup"><span data-stu-id="31eb3-223">Date</span></span> |<span data-ttu-id="31eb3-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="31eb3-224">EndOfDay(X)</span></span> |<span data-ttu-id="31eb3-225">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-225">X: DateTime</span></span> |<span data-ttu-id="31eb3-226">Obtient la valeur date-heure qui représente la fin de la journée (composant jour) de X.</span><span class="sxs-lookup"><span data-stu-id="31eb3-226">Gets the date-time that represents the end of the day (day component) of X.</span></span><br/><br/><span data-ttu-id="31eb3-227">Exemple : `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="31eb3-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="31eb3-228">Date</span><span class="sxs-lookup"><span data-stu-id="31eb3-228">Date</span></span> |<span data-ttu-id="31eb3-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="31eb3-229">EndOfMonth(X)</span></span> |<span data-ttu-id="31eb3-230">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-230">X: DateTime</span></span> |<span data-ttu-id="31eb3-231">Permet d’obtenir la fin du mois représentée par le composant mois du paramètre X.</span><span class="sxs-lookup"><span data-stu-id="31eb3-231">Gets the end of the month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="31eb3-232">Exemple : `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date-heure qui représente la fin du mois de septembre)</span><span class="sxs-lookup"><span data-stu-id="31eb3-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents the end of September month)</span></span> |
| <span data-ttu-id="31eb3-233">Date</span><span class="sxs-lookup"><span data-stu-id="31eb3-233">Date</span></span> |<span data-ttu-id="31eb3-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="31eb3-234">StartOfDay(X)</span></span> |<span data-ttu-id="31eb3-235">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-235">X: DateTime</span></span> |<span data-ttu-id="31eb3-236">Permet d’obtenir le début de la journée représenté par le composant jour du paramètre X.</span><span class="sxs-lookup"><span data-stu-id="31eb3-236">Gets the start of the day represented by the day component of parameter X.</span></span><br/><br/><span data-ttu-id="31eb3-237">Exemple : `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="31eb3-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="31eb3-238">DateTime</span><span class="sxs-lookup"><span data-stu-id="31eb3-238">DateTime</span></span> |<span data-ttu-id="31eb3-239">From(X)</span><span class="sxs-lookup"><span data-stu-id="31eb3-239">From(X)</span></span> |<span data-ttu-id="31eb3-240">X: String</span><span class="sxs-lookup"><span data-stu-id="31eb3-240">X: String</span></span> |<span data-ttu-id="31eb3-241">Analyser la chaîne X à une heure de date.</span><span class="sxs-lookup"><span data-stu-id="31eb3-241">Parse string X to a date time.</span></span> |
| <span data-ttu-id="31eb3-242">DateTime</span><span class="sxs-lookup"><span data-stu-id="31eb3-242">DateTime</span></span> |<span data-ttu-id="31eb3-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="31eb3-243">Ticks(X)</span></span> |<span data-ttu-id="31eb3-244">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="31eb3-244">X: DateTime</span></span> |<span data-ttu-id="31eb3-245">Permet d’obtenir la propriété de graduation du paramètre X. Un cycle est égal à 100 nanosecondes.</span><span class="sxs-lookup"><span data-stu-id="31eb3-245">Gets the ticks property of the parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="31eb3-246">La valeur de cette propriété représente le nombre de graduations écoulées depuis 12:00:00 minuit, le 1er janvier 0001.</span><span class="sxs-lookup"><span data-stu-id="31eb3-246">The value of this property represents the number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="31eb3-247">Texte</span><span class="sxs-lookup"><span data-stu-id="31eb3-247">Text</span></span> |<span data-ttu-id="31eb3-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="31eb3-248">Format(X)</span></span> |<span data-ttu-id="31eb3-249">X : variable de chaîne</span><span class="sxs-lookup"><span data-stu-id="31eb3-249">X: String variable</span></span> |<span data-ttu-id="31eb3-250">Met en forme le texte (utilisez la combinaison `\\'` pour échapper le caractère `'`).</span><span class="sxs-lookup"><span data-stu-id="31eb3-250">Formats the text (use `\\'` combination to escape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="31eb3-251">Lorsque vous utilisez une fonction au sein d’une autre fonction, vous n’avez pas besoin d’utiliser le préfixe **$$** de la fonction interne.</span><span class="sxs-lookup"><span data-stu-id="31eb3-251">When using a function within another function, you do not need to use **$$** prefix for the inner function.</span></span> <span data-ttu-id="31eb3-252">Par exemple : $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' et RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="31eb3-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="31eb3-253">Dans cet exemple, notez que le préfixe **$$** n’est pas utilisé pour la fonction **Time.AddHours**.</span><span class="sxs-lookup"><span data-stu-id="31eb3-253">In this example, notice that **$$** prefix is not used for the **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="31eb3-254">Exemple</span><span class="sxs-lookup"><span data-stu-id="31eb3-254">Example</span></span>
<span data-ttu-id="31eb3-255">Dans l’exemple suivant, les paramètres d’entrée et de sortie de l’activité Hive sont déterminés à l’aide de la fonction `Text.Format` et de la variable système SliceStart.</span><span class="sxs-lookup"><span data-stu-id="31eb3-255">In the following example, input and output parameters for the Hive activity are determined by using the `Text.Format` function and SliceStart system variable.</span></span> 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a><span data-ttu-id="31eb3-256">Exemple 2</span><span class="sxs-lookup"><span data-stu-id="31eb3-256">Example 2</span></span>

<span data-ttu-id="31eb3-257">Dans l’exemple suivant, le paramètre DateTime de l’activité de procédure stockée est déterminé à l’aide de la fonction Text.</span><span class="sxs-lookup"><span data-stu-id="31eb3-257">In the following example, the DateTime parameter for the Stored Procedure Activity is determined by using the Text.</span></span> <span data-ttu-id="31eb3-258">Format et de la variable SliceStart.</span><span class="sxs-lookup"><span data-stu-id="31eb3-258">Format function and the SliceStart variable.</span></span> 

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a><span data-ttu-id="31eb3-259">Exemple 3</span><span class="sxs-lookup"><span data-stu-id="31eb3-259">Example 3</span></span>
<span data-ttu-id="31eb3-260">Pour lire les données de la veille au lieu du jour représenté par SliceStart, utilisez la fonction AddDays, comme illustré dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="31eb3-260">To read data from previous day instead of day represented by the SliceStart, use the AddDays function as shown in the following example:</span></span> 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
                        "Month": "$$Text.Format('{0:MM}',WindowStart)",
                        "Day": "$$Text.Format('{0:dd}',WindowStart)"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 2,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```

<span data-ttu-id="31eb3-261">Consultez la rubrique [Chaînes de format de date et d’heure personnalisées](https://msdn.microsoft.com/library/8kb3ddd4.aspx) , qui décrit les différentes options de formatage que vous pouvez utiliser (par exemple : aa et aaaa).</span><span class="sxs-lookup"><span data-stu-id="31eb3-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

