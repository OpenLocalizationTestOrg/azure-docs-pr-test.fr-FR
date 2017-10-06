---
title: "aaaData fabrique de fonctions et Variables système | Documents Microsoft"
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
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a><span data-ttu-id="08067-103">Azure Data Factory - Variables système et fonctions</span><span class="sxs-lookup"><span data-stu-id="08067-103">Azure Data Factory - Functions and System Variables</span></span>
<span data-ttu-id="08067-104">Cet article fournit des informations sur les fonctions et variables prises en charge par Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="08067-104">This article provides information about functions and variables supported by Azure Data Factory.</span></span>

## <a name="data-factory-system-variables"></a><span data-ttu-id="08067-105">Variables système Data Factory</span><span class="sxs-lookup"><span data-stu-id="08067-105">Data Factory system variables</span></span>
| <span data-ttu-id="08067-106">Nom de la variable</span><span class="sxs-lookup"><span data-stu-id="08067-106">Variable Name</span></span> | <span data-ttu-id="08067-107">Description</span><span class="sxs-lookup"><span data-stu-id="08067-107">Description</span></span> | <span data-ttu-id="08067-108">Portée de l’objet</span><span class="sxs-lookup"><span data-stu-id="08067-108">Object Scope</span></span> | <span data-ttu-id="08067-109">Étendue JSON et cas d’utilisation</span><span class="sxs-lookup"><span data-stu-id="08067-109">JSON Scope and Use Cases</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08067-110">WindowStart</span><span class="sxs-lookup"><span data-stu-id="08067-110">WindowStart</span></span> |<span data-ttu-id="08067-111">Début de l’intervalle de temps pour l’intervalle d’exécution d’activité en cours</span><span class="sxs-lookup"><span data-stu-id="08067-111">Start of time interval for current activity run window</span></span> |<span data-ttu-id="08067-112">activité</span><span class="sxs-lookup"><span data-stu-id="08067-112">activity</span></span> |<ol><li><span data-ttu-id="08067-113">Spécifier des requêtes de sélection de données.</span><span class="sxs-lookup"><span data-stu-id="08067-113">Specify data selection queries.</span></span> <span data-ttu-id="08067-114">Consultez les articles de connecteur référencés dans hello [les activités de déplacement des données](data-factory-data-movement-activities.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="08067-114">See connector articles referenced in hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span></li> |
| <span data-ttu-id="08067-115">WindowEnd</span><span class="sxs-lookup"><span data-stu-id="08067-115">WindowEnd</span></span> |<span data-ttu-id="08067-116">Fin de l’intervalle de temps de l’intervalle d’exécution d’activité en cours</span><span class="sxs-lookup"><span data-stu-id="08067-116">End of time interval for current activity run window</span></span> |<span data-ttu-id="08067-117">activité</span><span class="sxs-lookup"><span data-stu-id="08067-117">activity</span></span> |<span data-ttu-id="08067-118">identique à WindowStart.</span><span class="sxs-lookup"><span data-stu-id="08067-118">same as WindowStart.</span></span> |
| <span data-ttu-id="08067-119">SliceStart</span><span class="sxs-lookup"><span data-stu-id="08067-119">SliceStart</span></span> |<span data-ttu-id="08067-120">Début de l’intervalle de temps pour une tranche de données en cours de génération</span><span class="sxs-lookup"><span data-stu-id="08067-120">Start of time interval for data  slice being produced</span></span> |<span data-ttu-id="08067-121">activité</span><span class="sxs-lookup"><span data-stu-id="08067-121">activity</span></span><br/><span data-ttu-id="08067-122">jeu de données</span><span class="sxs-lookup"><span data-stu-id="08067-122">dataset</span></span> |<ol><li><span data-ttu-id="08067-123">Spécifier les chemins d’accès et les noms de fichiers dynamiques tout en travaillant avec [Blob Azure](data-factory-azure-blob-connector.md) et [Jeux de données du système de fichiers](data-factory-onprem-file-system-connector.md).</span><span class="sxs-lookup"><span data-stu-id="08067-123">Specify dynamic folder paths and file names while working with [Azure Blob](data-factory-azure-blob-connector.md) and [File System datasets](data-factory-onprem-file-system-connector.md).</span></span></li><li><span data-ttu-id="08067-124">Spécifier les dépendances d’entrée avec les fonctions Data Factory dans la collecte d’activité.</span><span class="sxs-lookup"><span data-stu-id="08067-124">Specify input dependencies with data factory functions in activity inputs collection.</span></span></li></ol> |
| <span data-ttu-id="08067-125">SliceEnd</span><span class="sxs-lookup"><span data-stu-id="08067-125">SliceEnd</span></span> |<span data-ttu-id="08067-126">Fin de l’intervalle de temps pour la tranche de données en cours.</span><span class="sxs-lookup"><span data-stu-id="08067-126">End of time interval for current data slice.</span></span> |<span data-ttu-id="08067-127">activité</span><span class="sxs-lookup"><span data-stu-id="08067-127">activity</span></span><br/><span data-ttu-id="08067-128">dataset</span><span class="sxs-lookup"><span data-stu-id="08067-128">dataset</span></span> |<span data-ttu-id="08067-129">identique à SliceStart.</span><span class="sxs-lookup"><span data-stu-id="08067-129">same as SliceStart.</span></span> |

> [!NOTE]
> <span data-ttu-id="08067-130">Actuellement la fabrique de données requiert que hello planifier hello spécifié dans activité correspond exactement à planification hello spécifiée dans la disponibilité du jeu de données de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="08067-130">Currently data factory requires that hello schedule specified in hello activity exactly matches hello schedule specified in availability of hello output dataset.</span></span> <span data-ttu-id="08067-131">Par conséquent, WindowStart, WindowEnd et SliceStart et SliceEnd toujours mappent toohello même moment période et une tranche de sortie unique.</span><span class="sxs-lookup"><span data-stu-id="08067-131">Therefore, WindowStart, WindowEnd, and SliceStart and SliceEnd always map toohello same time period and a single output slice.</span></span>
> 

### <a name="example-for-using-a-system-variable"></a><span data-ttu-id="08067-132">Exemple d’utilisation d’une variable système</span><span class="sxs-lookup"><span data-stu-id="08067-132">Example for using a system variable</span></span>
<span data-ttu-id="08067-133">Bonjour suivant l’exemple, année, mois, jour et l’heure de **SliceStart** sont extraits dans des variables distinctes qui sont utilisés par **folderPath** et **nom de fichier** propriétés.</span><span class="sxs-lookup"><span data-stu-id="08067-133">In hello following example, year, month, day, and time of **SliceStart** are extracted into separate variables that are used by **folderPath** and **fileName** properties.</span></span>

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

## <a name="data-factory-functions"></a><span data-ttu-id="08067-134">Fonctions Data Factory</span><span class="sxs-lookup"><span data-stu-id="08067-134">Data Factory functions</span></span>
<span data-ttu-id="08067-135">Vous pouvez utiliser des fonctions dans la fabrique de données, ainsi que des variables système pour hello suite à des fins :</span><span class="sxs-lookup"><span data-stu-id="08067-135">You can use functions in data factory along with system variables for hello following purposes:</span></span>

1. <span data-ttu-id="08067-136">Spécification de requêtes de sélection de données (voir les articles de connecteur référencés par hello [les activités de déplacement des données](data-factory-data-movement-activities.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="08067-136">Specifying data selection queries (see connector articles referenced by hello [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>
   
   <span data-ttu-id="08067-137">Hello tooinvoke syntaxe une fonction de fabrique de données est :  **$$ <function>**  pour les requêtes de sélection de données et d’autres propriétés dans l’activité hello et jeux de données.</span><span class="sxs-lookup"><span data-stu-id="08067-137">hello syntax tooinvoke a data factory function is: **$$<function>** for data selection queries and other properties in hello activity and datasets.</span></span>  
2. <span data-ttu-id="08067-138">Spécifier les dépendances d’entrée avec les fonctions Data Factory dans la collecte d’entrées d’activité.</span><span class="sxs-lookup"><span data-stu-id="08067-138">Specifying input dependencies with data factory functions in activity inputs collection.</span></span>
   
    <span data-ttu-id="08067-139">$$ n’est pas nécessaire pour spécifier des expressions de dépendance d’entrée.</span><span class="sxs-lookup"><span data-stu-id="08067-139">$$ is not needed for specifying input dependency expressions.</span></span>     

<span data-ttu-id="08067-140">Bonjour suivant l’exemple, **sqlReaderQuery** dans un fichier JSON est affectée à tooa retourné par hello `Text.Format` (fonction).</span><span class="sxs-lookup"><span data-stu-id="08067-140">In hello following sample, **sqlReaderQuery** property in a JSON file is assigned tooa value returned by hello `Text.Format` function.</span></span> <span data-ttu-id="08067-141">Cet exemple utilise également une variable système nommée **WindowStart**, qui représente l’heure de début de hello de fenêtre d’exécution de l’activité hello.</span><span class="sxs-lookup"><span data-stu-id="08067-141">This sample also uses a system variable named **WindowStart**, which represents hello start time of hello activity run window.</span></span>

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

<span data-ttu-id="08067-142">Consultez la rubrique [Chaînes de format de date et d’heure personnalisées](https://msdn.microsoft.com/library/8kb3ddd4.aspx) , qui décrit les différentes options de formatage que vous pouvez utiliser (par exemple : aa et aaaa).</span><span class="sxs-lookup"><span data-stu-id="08067-142">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: ay vs. yyyy).</span></span> 

### <a name="functions"></a><span data-ttu-id="08067-143">Fonctions</span><span class="sxs-lookup"><span data-stu-id="08067-143">Functions</span></span>
<span data-ttu-id="08067-144">Hello les tableaux suivants répertorie toutes les fonctions hello dans Azure Data Factory :</span><span class="sxs-lookup"><span data-stu-id="08067-144">hello following tables list all hello functions in Azure Data Factory:</span></span>

| <span data-ttu-id="08067-145">Catégorie</span><span class="sxs-lookup"><span data-stu-id="08067-145">Category</span></span> | <span data-ttu-id="08067-146">Fonction</span><span class="sxs-lookup"><span data-stu-id="08067-146">Function</span></span> | <span data-ttu-id="08067-147">Paramètres</span><span class="sxs-lookup"><span data-stu-id="08067-147">Parameters</span></span> | <span data-ttu-id="08067-148">Description</span><span class="sxs-lookup"><span data-stu-id="08067-148">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08067-149">Time</span><span class="sxs-lookup"><span data-stu-id="08067-149">Time</span></span> |<span data-ttu-id="08067-150">AddHours(X,Y)</span><span class="sxs-lookup"><span data-stu-id="08067-150">AddHours(X,Y)</span></span> |<span data-ttu-id="08067-151">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-151">X: DateTime</span></span> <br/><br/><span data-ttu-id="08067-152">Y: int</span><span class="sxs-lookup"><span data-stu-id="08067-152">Y: int</span></span> |<span data-ttu-id="08067-153">Ajoute Y heures toohello est heure X.</span><span class="sxs-lookup"><span data-stu-id="08067-153">Adds Y hours toohello given time X.</span></span> <br/><br/><span data-ttu-id="08067-154">Exemple : `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="08067-154">Example: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM`</span></span> |
| <span data-ttu-id="08067-155">Temps</span><span class="sxs-lookup"><span data-stu-id="08067-155">Time</span></span> |<span data-ttu-id="08067-156">AddMinutes(X,Y)</span><span class="sxs-lookup"><span data-stu-id="08067-156">AddMinutes(X,Y)</span></span> |<span data-ttu-id="08067-157">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-157">X: DateTime</span></span> <br/><br/><span data-ttu-id="08067-158">Y: int</span><span class="sxs-lookup"><span data-stu-id="08067-158">Y: int</span></span> |<span data-ttu-id="08067-159">Ajoute Y minutes tooX.</span><span class="sxs-lookup"><span data-stu-id="08067-159">Adds Y minutes tooX.</span></span><br/><br/><span data-ttu-id="08067-160">Exemple : `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span><span class="sxs-lookup"><span data-stu-id="08067-160">Example: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM`</span></span> |
| <span data-ttu-id="08067-161">Temps</span><span class="sxs-lookup"><span data-stu-id="08067-161">Time</span></span> |<span data-ttu-id="08067-162">StartOfHour(X)</span><span class="sxs-lookup"><span data-stu-id="08067-162">StartOfHour(X)</span></span> |<span data-ttu-id="08067-163">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-163">X: Datetime</span></span> |<span data-ttu-id="08067-164">Obtient hello heure de début de heure hello représenté par le composant « heure » hello de X.</span><span class="sxs-lookup"><span data-stu-id="08067-164">Gets hello starting time for hello hour represented by hello hour component of X.</span></span> <br/><br/><span data-ttu-id="08067-165">Exemple : `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="08067-165">Example: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM`</span></span> |
| <span data-ttu-id="08067-166">Date</span><span class="sxs-lookup"><span data-stu-id="08067-166">Date</span></span> |<span data-ttu-id="08067-167">AddDays(X,Y)</span><span class="sxs-lookup"><span data-stu-id="08067-167">AddDays(X,Y)</span></span> |<span data-ttu-id="08067-168">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-168">X: DateTime</span></span><br/><br/><span data-ttu-id="08067-169">Y: int</span><span class="sxs-lookup"><span data-stu-id="08067-169">Y: int</span></span> |<span data-ttu-id="08067-170">Ajoute Y jours tooX.</span><span class="sxs-lookup"><span data-stu-id="08067-170">Adds Y days tooX.</span></span> <br/><br/><span data-ttu-id="08067-171">Exemple : 9/15/2013 12:00:00 PM + 2 jours = 9/17/2013 12:00:00 PM.</span><span class="sxs-lookup"><span data-stu-id="08067-171">Example: 9/15/2013 12:00:00 PM + 2 days = 9/17/2013 12:00:00 PM.</span></span><br/><br/><span data-ttu-id="08067-172">Vous pouvez également soustraire les jours en spécifiant Y en tant que nombre négatif.</span><span class="sxs-lookup"><span data-stu-id="08067-172">You can subtract days too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="08067-173">Exemple : `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="08067-173">Example: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="08067-174">Date</span><span class="sxs-lookup"><span data-stu-id="08067-174">Date</span></span> |<span data-ttu-id="08067-175">AddMonths(X,Y)</span><span class="sxs-lookup"><span data-stu-id="08067-175">AddMonths(X,Y)</span></span> |<span data-ttu-id="08067-176">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-176">X: DateTime</span></span><br/><br/><span data-ttu-id="08067-177">Y: int</span><span class="sxs-lookup"><span data-stu-id="08067-177">Y: int</span></span> |<span data-ttu-id="08067-178">Ajoute Y mois tooX.</span><span class="sxs-lookup"><span data-stu-id="08067-178">Adds Y months tooX.</span></span><br/><br/><span data-ttu-id="08067-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="08067-179">`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.</span></span><br/><br/><span data-ttu-id="08067-180">Vous pouvez également soustraire les mois en spécifiant Y en tant que nombre négatif.</span><span class="sxs-lookup"><span data-stu-id="08067-180">You can subtract months too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="08067-181">Exemple : `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="08067-181">Example: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.</span></span>|
| <span data-ttu-id="08067-182">Date</span><span class="sxs-lookup"><span data-stu-id="08067-182">Date</span></span> |<span data-ttu-id="08067-183">AddQuarters(X,Y)</span><span class="sxs-lookup"><span data-stu-id="08067-183">AddQuarters(X,Y)</span></span> |<span data-ttu-id="08067-184">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-184">X: DateTime</span></span> <br/><br/><span data-ttu-id="08067-185">Y: int</span><span class="sxs-lookup"><span data-stu-id="08067-185">Y: int</span></span> |<span data-ttu-id="08067-186">Ajoute Y * 3 mois tooX.</span><span class="sxs-lookup"><span data-stu-id="08067-186">Adds Y * 3 months tooX.</span></span><br/><br/><span data-ttu-id="08067-187">Exemple : `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span><span class="sxs-lookup"><span data-stu-id="08067-187">Example: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM`</span></span> |
| <span data-ttu-id="08067-188">Date</span><span class="sxs-lookup"><span data-stu-id="08067-188">Date</span></span> |<span data-ttu-id="08067-189">AddWeeks(X,Y)</span><span class="sxs-lookup"><span data-stu-id="08067-189">AddWeeks(X,Y)</span></span> |<span data-ttu-id="08067-190">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-190">X: DateTime</span></span><br/><br/><span data-ttu-id="08067-191">Y: int</span><span class="sxs-lookup"><span data-stu-id="08067-191">Y: int</span></span> |<span data-ttu-id="08067-192">Ajoute Y * 7 jours tooX</span><span class="sxs-lookup"><span data-stu-id="08067-192">Adds Y * 7 days tooX</span></span><br/><br/><span data-ttu-id="08067-193">Exemple : 15/9/2013 12:00:00 PM + 1 semaine = 22/9/2013 12:00:00 PM</span><span class="sxs-lookup"><span data-stu-id="08067-193">Example: 9/15/2013 12:00:00 PM + 1 week = 9/22/2013 12:00:00 PM</span></span><br/><br/><span data-ttu-id="08067-194">Vous pouvez également soustraire les semaines en spécifiant Y en tant que nombre négatif.</span><span class="sxs-lookup"><span data-stu-id="08067-194">You can subtract weeks too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="08067-195">Exemple : `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="08067-195">Example: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`.</span></span> |
| <span data-ttu-id="08067-196">Date</span><span class="sxs-lookup"><span data-stu-id="08067-196">Date</span></span> |<span data-ttu-id="08067-197">AddYears(X,Y)</span><span class="sxs-lookup"><span data-stu-id="08067-197">AddYears(X,Y)</span></span> |<span data-ttu-id="08067-198">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-198">X: DateTime</span></span><br/><br/><span data-ttu-id="08067-199">Y: int</span><span class="sxs-lookup"><span data-stu-id="08067-199">Y: int</span></span> |<span data-ttu-id="08067-200">Ajoute Y années tooX.</span><span class="sxs-lookup"><span data-stu-id="08067-200">Adds Y years tooX.</span></span><br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/><span data-ttu-id="08067-201">Vous pouvez également soustraire les années en spécifiant Y en tant que nombre négatif.</span><span class="sxs-lookup"><span data-stu-id="08067-201">You can subtract years too by specifying Y as a negative number.</span></span><br/><br/><span data-ttu-id="08067-202">Exemple : `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span><span class="sxs-lookup"><span data-stu-id="08067-202">Example: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`.</span></span> |
| <span data-ttu-id="08067-203">Date</span><span class="sxs-lookup"><span data-stu-id="08067-203">Date</span></span> |<span data-ttu-id="08067-204">Day(X)</span><span class="sxs-lookup"><span data-stu-id="08067-204">Day(X)</span></span> |<span data-ttu-id="08067-205">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-205">X: DateTime</span></span> |<span data-ttu-id="08067-206">Obtient le composant « jour » hello de X.</span><span class="sxs-lookup"><span data-stu-id="08067-206">Gets hello day component of X.</span></span><br/><br/><span data-ttu-id="08067-207">Exemple : `Day of 9/15/2013 12:00:00 PM is 9`.</span><span class="sxs-lookup"><span data-stu-id="08067-207">Example: `Day of 9/15/2013 12:00:00 PM is 9`.</span></span> |
| <span data-ttu-id="08067-208">Date</span><span class="sxs-lookup"><span data-stu-id="08067-208">Date</span></span> |<span data-ttu-id="08067-209">DayOfWeek(X)</span><span class="sxs-lookup"><span data-stu-id="08067-209">DayOfWeek(X)</span></span> |<span data-ttu-id="08067-210">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-210">X: DateTime</span></span> |<span data-ttu-id="08067-211">Obtient le jour hello de composant semaine de X.</span><span class="sxs-lookup"><span data-stu-id="08067-211">Gets hello day of week component of X.</span></span><br/><br/><span data-ttu-id="08067-212">Exemple : `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span><span class="sxs-lookup"><span data-stu-id="08067-212">Example: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`.</span></span> |
| <span data-ttu-id="08067-213">Date</span><span class="sxs-lookup"><span data-stu-id="08067-213">Date</span></span> |<span data-ttu-id="08067-214">DayOfYear(X)</span><span class="sxs-lookup"><span data-stu-id="08067-214">DayOfYear(X)</span></span> |<span data-ttu-id="08067-215">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-215">X: DateTime</span></span> |<span data-ttu-id="08067-216">Obtient le jour hello année hello représenté par le composant « année » hello de X.</span><span class="sxs-lookup"><span data-stu-id="08067-216">Gets hello day in hello year represented by hello year component of X.</span></span><br/><br/><span data-ttu-id="08067-217">Exemples :</span><span class="sxs-lookup"><span data-stu-id="08067-217">Examples:</span></span><br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| <span data-ttu-id="08067-218">Date</span><span class="sxs-lookup"><span data-stu-id="08067-218">Date</span></span> |<span data-ttu-id="08067-219">DaysInMonth(X)</span><span class="sxs-lookup"><span data-stu-id="08067-219">DaysInMonth(X)</span></span> |<span data-ttu-id="08067-220">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-220">X: DateTime</span></span> |<span data-ttu-id="08067-221">Obtient les jours hello mois hello représenté par le composant de mois hello du paramètre X.</span><span class="sxs-lookup"><span data-stu-id="08067-221">Gets hello days in hello month represented by hello month component of parameter X.</span></span><br/><br/><span data-ttu-id="08067-222">Exemple : `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span><span class="sxs-lookup"><span data-stu-id="08067-222">Example: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`.</span></span> |
| <span data-ttu-id="08067-223">Date</span><span class="sxs-lookup"><span data-stu-id="08067-223">Date</span></span> |<span data-ttu-id="08067-224">EndOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="08067-224">EndOfDay(X)</span></span> |<span data-ttu-id="08067-225">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-225">X: DateTime</span></span> |<span data-ttu-id="08067-226">Obtient la date-heure hello qui représente la fin de hello du jour hello (composant day) de X.</span><span class="sxs-lookup"><span data-stu-id="08067-226">Gets hello date-time that represents hello end of hello day (day component) of X.</span></span><br/><br/><span data-ttu-id="08067-227">Exemple : `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span><span class="sxs-lookup"><span data-stu-id="08067-227">Example: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`.</span></span> |
| <span data-ttu-id="08067-228">Date</span><span class="sxs-lookup"><span data-stu-id="08067-228">Date</span></span> |<span data-ttu-id="08067-229">EndOfMonth(X)</span><span class="sxs-lookup"><span data-stu-id="08067-229">EndOfMonth(X)</span></span> |<span data-ttu-id="08067-230">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-230">X: DateTime</span></span> |<span data-ttu-id="08067-231">Obtient la fin de hello du mois de hello représenté par le composant month du paramètre X.</span><span class="sxs-lookup"><span data-stu-id="08067-231">Gets hello end of hello month represented by month component of parameter X.</span></span> <br/><br/><span data-ttu-id="08067-232">Exemple : `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date représentant une fin hello du mois de septembre)</span><span class="sxs-lookup"><span data-stu-id="08067-232">Example: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (date time that represents hello end of September month)</span></span> |
| <span data-ttu-id="08067-233">Date</span><span class="sxs-lookup"><span data-stu-id="08067-233">Date</span></span> |<span data-ttu-id="08067-234">StartOfDay(X)</span><span class="sxs-lookup"><span data-stu-id="08067-234">StartOfDay(X)</span></span> |<span data-ttu-id="08067-235">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-235">X: DateTime</span></span> |<span data-ttu-id="08067-236">Obtient le début hello du jour hello représenté par le composant de jour hello du paramètre X.</span><span class="sxs-lookup"><span data-stu-id="08067-236">Gets hello start of hello day represented by hello day component of parameter X.</span></span><br/><br/><span data-ttu-id="08067-237">Exemple : `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span><span class="sxs-lookup"><span data-stu-id="08067-237">Example: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`.</span></span> |
| <span data-ttu-id="08067-238">DateTime</span><span class="sxs-lookup"><span data-stu-id="08067-238">DateTime</span></span> |<span data-ttu-id="08067-239">From(X)</span><span class="sxs-lookup"><span data-stu-id="08067-239">From(X)</span></span> |<span data-ttu-id="08067-240">X: String</span><span class="sxs-lookup"><span data-stu-id="08067-240">X: String</span></span> |<span data-ttu-id="08067-241">Analyser la chaîne X tooa date heure.</span><span class="sxs-lookup"><span data-stu-id="08067-241">Parse string X tooa date time.</span></span> |
| <span data-ttu-id="08067-242">DateTime</span><span class="sxs-lookup"><span data-stu-id="08067-242">DateTime</span></span> |<span data-ttu-id="08067-243">Ticks(X)</span><span class="sxs-lookup"><span data-stu-id="08067-243">Ticks(X)</span></span> |<span data-ttu-id="08067-244">X: DateTime </span><span class="sxs-lookup"><span data-stu-id="08067-244">X: DateTime</span></span> |<span data-ttu-id="08067-245">Obtient les graduations hello propriété de paramètre de hello X. Un cycle est égal à 100 nanosecondes.</span><span class="sxs-lookup"><span data-stu-id="08067-245">Gets hello ticks property of hello parameter X. One tick equals 100 nanoseconds.</span></span> <span data-ttu-id="08067-246">valeur Hello de cette propriété représente le nombre de hello de graduations qui se sont écoulées depuis 12:00:00 minuit, le 1er janvier 0001.</span><span class="sxs-lookup"><span data-stu-id="08067-246">hello value of this property represents hello number of ticks that have elapsed since 12:00:00 midnight, January 1, 0001.</span></span> |
| <span data-ttu-id="08067-247">Texte</span><span class="sxs-lookup"><span data-stu-id="08067-247">Text</span></span> |<span data-ttu-id="08067-248">Format(X)</span><span class="sxs-lookup"><span data-stu-id="08067-248">Format(X)</span></span> |<span data-ttu-id="08067-249">X : variable de chaîne</span><span class="sxs-lookup"><span data-stu-id="08067-249">X: String variable</span></span> |<span data-ttu-id="08067-250">Formats hello texte (utilisez `\\'` combinaison tooescape `'` caractères).</span><span class="sxs-lookup"><span data-stu-id="08067-250">Formats hello text (use `\\'` combination tooescape `'` character).</span></span>|

> [!IMPORTANT]
> <span data-ttu-id="08067-251">Lorsque vous utilisez une fonction dans une autre fonction, vous n’avez pas besoin de toouse  **$$**  préfixe de fonction interne de hello.</span><span class="sxs-lookup"><span data-stu-id="08067-251">When using a function within another function, you do not need toouse **$$** prefix for hello inner function.</span></span> <span data-ttu-id="08067-252">Par exemple : $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' et RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span><span class="sxs-lookup"><span data-stu-id="08067-252">For example: $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0: yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)).</span></span> <span data-ttu-id="08067-253">Dans cet exemple, notez que  **$$**  préfixe n’est pas utilisé pour hello **Time.AddHours** (fonction).</span><span class="sxs-lookup"><span data-stu-id="08067-253">In this example, notice that **$$** prefix is not used for hello **Time.AddHours** function.</span></span> 

#### <a name="example"></a><span data-ttu-id="08067-254">Exemple</span><span class="sxs-lookup"><span data-stu-id="08067-254">Example</span></span>
<span data-ttu-id="08067-255">Bonjour, des paramètres d’exemple, les entrées et sorties suivants pour l’activité de ruche hello sont déterminées à l’aide de hello `Text.Format` fonction et la variable SliceStart du système.</span><span class="sxs-lookup"><span data-stu-id="08067-255">In hello following example, input and output parameters for hello Hive activity are determined by using hello `Text.Format` function and SliceStart system variable.</span></span> 

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

### <a name="example-2"></a><span data-ttu-id="08067-256">Exemple 2</span><span class="sxs-lookup"><span data-stu-id="08067-256">Example 2</span></span>

<span data-ttu-id="08067-257">Bonjour l’exemple suivant, le paramètre DateTime hello hello activité de procédure stockée est déterminée à l’aide de hello texte.</span><span class="sxs-lookup"><span data-stu-id="08067-257">In hello following example, hello DateTime parameter for hello Stored Procedure Activity is determined by using hello Text.</span></span> <span data-ttu-id="08067-258">Formatage de la fonction et hello SliceStart variable.</span><span class="sxs-lookup"><span data-stu-id="08067-258">Format function and hello SliceStart variable.</span></span> 

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

### <a name="example-3"></a><span data-ttu-id="08067-259">Exemple 3</span><span class="sxs-lookup"><span data-stu-id="08067-259">Example 3</span></span>
<span data-ttu-id="08067-260">tooread des données à partir de la journée précédente au lieu de jours représenté par hello SliceStart, utilisez la fonction AddDays de hello comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="08067-260">tooread data from previous day instead of day represented by hello SliceStart, use hello AddDays function as shown in hello following example:</span></span> 

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

<span data-ttu-id="08067-261">Consultez la rubrique [Chaînes de format de date et d’heure personnalisées](https://msdn.microsoft.com/library/8kb3ddd4.aspx) , qui décrit les différentes options de formatage que vous pouvez utiliser (par exemple : aa et aaaa).</span><span class="sxs-lookup"><span data-stu-id="08067-261">See [Custom Date and Time Format Strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx) topic that describes different formatting options you can use (for example: yy vs. yyyy).</span></span> 

