---
title: "Importer vos données dans Analytics dans Azure Application Insights | Microsoft Docs"
description: "Importez des données statiques à associer à la télémétrie de l’application ou importez un flux de données distinct à interroger avec Analytics."
services: application-insights
keywords: "schéma ouvert, importation de données"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: aa855a9050ec4e5e7c5db88b7209b8bb48bdba51
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="607b5-104">Importer des données dans Analytics</span><span class="sxs-lookup"><span data-stu-id="607b5-104">Import data into Analytics</span></span>

<span data-ttu-id="607b5-105">Importez des données tabulaires dans [Analytics](app-insights-analytics.md) pour les associer à la télémétrie [Application Insights](app-insights-overview.md) à partir de votre application ou pour les analyser comme un flux distinct.</span><span class="sxs-lookup"><span data-stu-id="607b5-105">Import any tabular data into [Analytics](app-insights-analytics.md), either to join it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="607b5-106">Analytics est un langage de requête puissant et bien adapté à l’analyse de gros volumes de flux horodatés de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="607b5-106">Analytics is a powerful query language well-suited to analyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="607b5-107">Vous pouvez importer des données dans Analytics à l’aide de votre propre schéma.</span><span class="sxs-lookup"><span data-stu-id="607b5-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="607b5-108">Il n’est pas nécessaire d’utiliser les schémas Application Insights standard tels qu’une requête ou une trace.</span><span class="sxs-lookup"><span data-stu-id="607b5-108">It doesn't have to use the standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="607b5-109">Vous pouvez importer des fichiers JSON ou DSV (valeurs séparées par des délimiteurs : virgule, point-virgule ou tabulation).</span><span class="sxs-lookup"><span data-stu-id="607b5-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="607b5-110">L’importation de données dans Analytics peut être utile dans les trois situations suivantes :</span><span class="sxs-lookup"><span data-stu-id="607b5-110">There are three situations where importing to Analytics is useful:</span></span>

* <span data-ttu-id="607b5-111">**Association avec la télémétrie de l’application.**</span><span class="sxs-lookup"><span data-stu-id="607b5-111">**Join with app telemetry.**</span></span> <span data-ttu-id="607b5-112">Par exemple, vous pouvez importer une table qui mappe des URL de votre site Web à des titres de page plus lisibles.</span><span class="sxs-lookup"><span data-stu-id="607b5-112">For example, you could import a table that maps URLs from your website to more readable page titles.</span></span> <span data-ttu-id="607b5-113">Dans Analytics, vous pouvez créer un rapport graphique de tableau de bord qui affiche les dix pages les plus consultées de votre site Web.</span><span class="sxs-lookup"><span data-stu-id="607b5-113">In Analytics, you can create a dashboard chart report that shows the ten most popular pages in your website.</span></span> <span data-ttu-id="607b5-114">Maintenant, il peut afficher les titres des pages plutôt que les URL.</span><span class="sxs-lookup"><span data-stu-id="607b5-114">Now it can show the page titles instead of the URLs.</span></span>
* <span data-ttu-id="607b5-115">**Mettre en corrélation la télémétrie de votre application** avec d’autres sources telles que le trafic réseau, les données de serveur ou les fichiers journaux CDN.</span><span class="sxs-lookup"><span data-stu-id="607b5-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="607b5-116">**Appliquer Analytics à un flux de données distinct.**</span><span class="sxs-lookup"><span data-stu-id="607b5-116">**Apply Analytics to a separate data stream.**</span></span> <span data-ttu-id="607b5-117">Application Insights Analytics est un outil puissant, qui fonctionne bien avec les flux horodatés partiellement alloués, et même beaucoup mieux que SQL dans la plupart des cas.</span><span class="sxs-lookup"><span data-stu-id="607b5-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="607b5-118">Si vous avez un flux de ce type issu d’une autre source, vous pouvez l’analyser avec Analytics.</span><span class="sxs-lookup"><span data-stu-id="607b5-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="607b5-119">Il est facile d’envoyer des données à votre source de données.</span><span class="sxs-lookup"><span data-stu-id="607b5-119">Sending data to your data source is easy.</span></span> 

1. <span data-ttu-id="607b5-120">(Une fois) Définissez le schéma de vos données dans une « source de données ».</span><span class="sxs-lookup"><span data-stu-id="607b5-120">(One time) Define the schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="607b5-121">(Régulièrement) Chargez vos données dans le stockage Azure et appelez l’API REST pour nous informer que de nouvelles données sont en attente d’ingestion.</span><span class="sxs-lookup"><span data-stu-id="607b5-121">(Periodically) Upload your data to Azure storage, and call the REST API to notify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="607b5-122">Après quelques minutes, les données sont disponibles pour être interrogées dans Analytics.</span><span class="sxs-lookup"><span data-stu-id="607b5-122">Within a few minutes, the data is available for query in Analytics.</span></span>

<span data-ttu-id="607b5-123">Vous définissez la fréquence du chargement et la rapidité à laquelle vous souhaitez que vos données soient disponibles pour les requêtes.</span><span class="sxs-lookup"><span data-stu-id="607b5-123">The frequency of the upload is defined by you and how fast would you like your data to be available for queries.</span></span> <span data-ttu-id="607b5-124">Nous vous recommandons de charger des données dans des segments plus grands, mais d’une taille inférieure à 1 Go.</span><span class="sxs-lookup"><span data-stu-id="607b5-124">It is more efficient to upload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="607b5-125">*Vous avez un grand nombre de sources de données à analyser ?*</span><span class="sxs-lookup"><span data-stu-id="607b5-125">*Got lots of data sources to analyze?*</span></span> [<span data-ttu-id="607b5-126">*Envisagez d’utiliser* logstash *pour envoyer vos données dans Application Insights.*</span><span class="sxs-lookup"><span data-stu-id="607b5-126">*Consider using* logstash *to ship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="607b5-127">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="607b5-127">Before you start</span></span>

<span data-ttu-id="607b5-128">Ce dont vous avez besoin :</span><span class="sxs-lookup"><span data-stu-id="607b5-128">You need:</span></span>

1. <span data-ttu-id="607b5-129">Une ressource Application Insights dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="607b5-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="607b5-130">Si vous voulez analyser vos données séparément de la télémétrie, [créez une ressource Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="607b5-130">If you want to analyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="607b5-131">Si vous associez ou comparez vos données à la télémétrie d’une application qui est déjà configurée avec Application Insights, vous pouvez utiliser la ressource pour cette application.</span><span class="sxs-lookup"><span data-stu-id="607b5-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use the resource for that app.</span></span>
 * <span data-ttu-id="607b5-132">Accès du propriétaire ou du contributeur à cette ressource.</span><span class="sxs-lookup"><span data-stu-id="607b5-132">Contributor or owner access to that resource.</span></span>
 
2. <span data-ttu-id="607b5-133">stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="607b5-133">Azure storage.</span></span> <span data-ttu-id="607b5-134">Vous chargez les données dans le stockage Azure et Analytics les récupère.</span><span class="sxs-lookup"><span data-stu-id="607b5-134">You upload to Azure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="607b5-135">Nous vous recommandons de créer un compte de stockage dédié pour vos blobs.</span><span class="sxs-lookup"><span data-stu-id="607b5-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="607b5-136">Si vos blobs sont partagés avec d’autres processus, nos processus prendront plus de temps pour lire vos blobs.</span><span class="sxs-lookup"><span data-stu-id="607b5-136">If your blobs are shared with other processes, it takes longer for our processes to read your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="607b5-137">Définir votre schéma</span><span class="sxs-lookup"><span data-stu-id="607b5-137">Define your schema</span></span>

<span data-ttu-id="607b5-138">Avant de pouvoir importer des données, vous devez définir une *source de données,* qui spécifie le schéma de vos données.</span><span class="sxs-lookup"><span data-stu-id="607b5-138">Before you can import data, you must define a *data source,* which specifies the schema of your data.</span></span>
<span data-ttu-id="607b5-139">Vous pouvez avoir jusqu'à 50 sources de données dans une seule ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="607b5-139">You can have up to 50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="607b5-140">Démarrez l’Assistant Source de données.</span><span class="sxs-lookup"><span data-stu-id="607b5-140">Start the data source wizard.</span></span> <span data-ttu-id="607b5-141">Utilisez le bouton Ajouter une nouvelle source de données.</span><span class="sxs-lookup"><span data-stu-id="607b5-141">Use "Add new data source" button.</span></span> <span data-ttu-id="607b5-142">Vous pouvez également cliquer sur le bouton Paramètres en haut à droite, puis choisir Sources de données dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="607b5-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Ajouter une source de données](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="607b5-144">Entrez un nom pour votre nouvelle source de données.</span><span class="sxs-lookup"><span data-stu-id="607b5-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="607b5-145">Définissez le format des fichiers que vous allez charger.</span><span class="sxs-lookup"><span data-stu-id="607b5-145">Define format of the files that you will upload.</span></span>

    <span data-ttu-id="607b5-146">Vous pouvez définir le format manuellement, ou télécharger un exemple de fichier.</span><span class="sxs-lookup"><span data-stu-id="607b5-146">You can either define the format manually, or upload a sample file.</span></span>

    <span data-ttu-id="607b5-147">Si les données sont au format CSV, la première ligne de l’exemple peut être des en-têtes de colonne.</span><span class="sxs-lookup"><span data-stu-id="607b5-147">If the data is in CSV format, the first row of the sample can be column headers.</span></span> <span data-ttu-id="607b5-148">Vous pouvez modifier le nom des champs à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="607b5-148">You can change the field names in the next step.</span></span>

    <span data-ttu-id="607b5-149">L’exemple doit inclure au moins 10 lignes ou enregistrements de données.</span><span class="sxs-lookup"><span data-stu-id="607b5-149">The sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="607b5-150">Les noms de colonnes ou de champs doivent avoir des noms alphanumériques (sans espaces ni ponctuation).</span><span class="sxs-lookup"><span data-stu-id="607b5-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Charger un exemple de fichier](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="607b5-152">Examinez le schéma de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="607b5-152">Review the schema that the wizard has got.</span></span> <span data-ttu-id="607b5-153">S’il a déduit les types à partir d’un exemple, vous devrez probablement modifier les types déduits des colonnes.</span><span class="sxs-lookup"><span data-stu-id="607b5-153">If it inferred the types from a sample, you might need to adjust the inferred types of the columns.</span></span>

    ![Examiner le schéma déduit](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="607b5-155">(Facultatif.) Téléchargez une définition de schéma.</span><span class="sxs-lookup"><span data-stu-id="607b5-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="607b5-156">Consultez le format ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="607b5-156">See the format below.</span></span>

 * <span data-ttu-id="607b5-157">Sélectionnez un horodatage.</span><span class="sxs-lookup"><span data-stu-id="607b5-157">Select a Timestamp.</span></span> <span data-ttu-id="607b5-158">Toutes les données dans Analytics doivent avoir un champ d’horodatage.</span><span class="sxs-lookup"><span data-stu-id="607b5-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="607b5-159">Il doit être de type `datetime`, mais il ne doit pas forcément être nommé « Horodatage ».</span><span class="sxs-lookup"><span data-stu-id="607b5-159">It must have type `datetime`, but it doesn't have to be named 'timestamp'.</span></span> <span data-ttu-id="607b5-160">Si vos données comportent une colonne contenant une date et une heure au format ISO, choisissez celle-ci en tant que colonne d’horodatage.</span><span class="sxs-lookup"><span data-stu-id="607b5-160">If your data has a column containing a date and time in ISO format, choose this as the timestamp column.</span></span> <span data-ttu-id="607b5-161">Sinon, choisissez « à mesure que les données sont arrivées », et le processus d’importation ajoutera un champ d’horodatage.</span><span class="sxs-lookup"><span data-stu-id="607b5-161">Otherwise, choose "as data arrived", and the import process will add a timestamp field.</span></span>

5. <span data-ttu-id="607b5-162">Créez la source de données.</span><span class="sxs-lookup"><span data-stu-id="607b5-162">Create the data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="607b5-163">Format de fichier de définition de schéma</span><span class="sxs-lookup"><span data-stu-id="607b5-163">Schema definition file format</span></span>

<span data-ttu-id="607b5-164">Au lieu de modifier le schéma dans l’interface utilisateur, vous pouvez charger la définition de schéma à partir d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="607b5-164">Instead of editing the schema in UI, you can load the schema definition from a file.</span></span> <span data-ttu-id="607b5-165">Le format de définition de schéma est le suivant :</span><span class="sxs-lookup"><span data-stu-id="607b5-165">The schema definition format is as follows:</span></span> 

<span data-ttu-id="607b5-166">Format délimité</span><span class="sxs-lookup"><span data-stu-id="607b5-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="607b5-167">Format JSON</span><span class="sxs-lookup"><span data-stu-id="607b5-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="607b5-168">Chaque colonne est identifiée par l’emplacement, le nom et le type.</span><span class="sxs-lookup"><span data-stu-id="607b5-168">Each column is identified by the location, name and type.</span></span> 

* <span data-ttu-id="607b5-169">Emplacement : pour le format de fichier délimité, il s’agit de la position de la valeur mappée.</span><span class="sxs-lookup"><span data-stu-id="607b5-169">Location – For delimited file format it is the position of the mapped value.</span></span> <span data-ttu-id="607b5-170">Pour le format JSON, il s’agit du jpath de la clé mappée.</span><span class="sxs-lookup"><span data-stu-id="607b5-170">For JSON format, it is the jpath of the mapped key.</span></span>
* <span data-ttu-id="607b5-171">Nom : nom affiché de la colonne.</span><span class="sxs-lookup"><span data-stu-id="607b5-171">Name – the displayed name of the column.</span></span>
* <span data-ttu-id="607b5-172">Type : type de données de cette colonne.</span><span class="sxs-lookup"><span data-stu-id="607b5-172">Type – the data type of that column.</span></span>
 
<span data-ttu-id="607b5-173">Si un exemple de données a été utilisé et que le format de fichier est délimité, la définition de schéma doit mapper toutes les colonnes et ajouter de nouvelles colonnes à la fin.</span><span class="sxs-lookup"><span data-stu-id="607b5-173">In case a sample data was used and file format is delimited, the schema definition must map all columns and add new columns at the end.</span></span> 

<span data-ttu-id="607b5-174">JSON permet un mappage partiel des données, par conséquent la définition de schéma du format JSON n’a pas besoin de mapper toutes les clés trouvées dans un exemple de données.</span><span class="sxs-lookup"><span data-stu-id="607b5-174">JSON allows partial mapping of the data, therefore the schema definition of JSON format doesn’t have to map every key which is found in a sample data.</span></span> <span data-ttu-id="607b5-175">Il peut également mapper les colonnes qui ne font pas partie de l’exemple de données.</span><span class="sxs-lookup"><span data-stu-id="607b5-175">It can also map columns which are not part of the sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="607b5-176">Importer des données</span><span class="sxs-lookup"><span data-stu-id="607b5-176">Import data</span></span>

<span data-ttu-id="607b5-177">Pour importer des données, chargez-les dans le stockage Azure, créez une clé d’accès qui leur est associée, puis appelez une API REST.</span><span class="sxs-lookup"><span data-stu-id="607b5-177">To import data, you upload it to Azure storage, create an access key for it, and then make a REST API call.</span></span>

![Ajouter une source de données](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="607b5-179">Vous pouvez effectuer l’opération suivante manuellement ou configurer un système automatisé pour qu’il le fasse à intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="607b5-179">You can perform the following process manually, or set up an automated system to do it at regular intervals.</span></span> <span data-ttu-id="607b5-180">Vous devez suivre ces étapes pour chaque bloc de données à importer.</span><span class="sxs-lookup"><span data-stu-id="607b5-180">You need to follow these steps for each block of data you want to import.</span></span>

1. <span data-ttu-id="607b5-181">Chargez les données dans le [stockage Blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="607b5-181">Upload the data to [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="607b5-182">La taille maximum des blobs est de 1 Go (sans compression).</span><span class="sxs-lookup"><span data-stu-id="607b5-182">Blobs can be any size up to 1GB uncompressed.</span></span> <span data-ttu-id="607b5-183">Les blobs d’une centaine de Mo sont parfaits, du point de vue des performances.</span><span class="sxs-lookup"><span data-stu-id="607b5-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="607b5-184">Vous pouvez les compresser avec Gzip pour améliorer le temps de chargement et la latence de disponibilité des données pour interrogation.</span><span class="sxs-lookup"><span data-stu-id="607b5-184">You can compress it with Gzip to improve upload time and latency for the data to be available for query.</span></span> <span data-ttu-id="607b5-185">Utilisez l’extension de nom de fichier `.gz`.</span><span class="sxs-lookup"><span data-stu-id="607b5-185">Use the `.gz` filename extension.</span></span>
 * <span data-ttu-id="607b5-186">Il est préférable d’utiliser un compte de stockage distinct à cet effet, afin d’éviter que les appels provenant de différents services ralentissent les performances.</span><span class="sxs-lookup"><span data-stu-id="607b5-186">It's best to use a separate storage account for this purpose, to avoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="607b5-187">Lors de l’envoi de données à des fréquences élevées, toutes les quelques secondes, il est recommandé d’utiliser plusieurs comptes de stockage, pour des raisons de performances.</span><span class="sxs-lookup"><span data-stu-id="607b5-187">When sending data in high frequency, every few seconds, it is recommended to use more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="607b5-188">[Créez une clé de signature d’accès partagé pour le blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="607b5-188">[Create a Shared Access Signature key for the blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="607b5-189">Le délai d’expiration de la clé doit être d’un jour et celle-ci doit fournir un accès en lecture.</span><span class="sxs-lookup"><span data-stu-id="607b5-189">The key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="607b5-190">Effectuez un appel REST pour indiquer à Application Insights que les données sont en attente.</span><span class="sxs-lookup"><span data-stu-id="607b5-190">Make a REST call to notify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="607b5-191">Point de terminaison : `https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="607b5-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="607b5-192">Méthode HTTP : POST</span><span class="sxs-lookup"><span data-stu-id="607b5-192">HTTP method: POST</span></span>
 * <span data-ttu-id="607b5-193">Charge utile :</span><span class="sxs-lookup"><span data-stu-id="607b5-193">Payload:</span></span>

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

<span data-ttu-id="607b5-194">Les espaces réservés sont :</span><span class="sxs-lookup"><span data-stu-id="607b5-194">The placeholders are:</span></span>

* <span data-ttu-id="607b5-195">`Blob URI with Shared Access Key` : cet élément est obtenu à partir de la procédure de création d’une clé.</span><span class="sxs-lookup"><span data-stu-id="607b5-195">`Blob URI with Shared Access Key`: You get this from the procedure for creating a key.</span></span> <span data-ttu-id="607b5-196">Il est spécifique au blob.</span><span class="sxs-lookup"><span data-stu-id="607b5-196">It is specific to the blob.</span></span>
* <span data-ttu-id="607b5-197">`Schema ID` : l’ID de schéma généré pour votre schéma défini.</span><span class="sxs-lookup"><span data-stu-id="607b5-197">`Schema ID`: The schema ID generated for your defined schema.</span></span> <span data-ttu-id="607b5-198">Les données de ce blob doivent respecter le schéma que vous avez défini pour cette source.</span><span class="sxs-lookup"><span data-stu-id="607b5-198">The data in this blob should conform to the schema.</span></span>
* <span data-ttu-id="607b5-199">`DateTime` : l’heure à laquelle la demande est soumise, UTC.</span><span class="sxs-lookup"><span data-stu-id="607b5-199">`DateTime`: The time at which the request is submitted, UTC.</span></span> <span data-ttu-id="607b5-200">Nous acceptons les formats suivants : ISO8601 (comme « 2016-01-01 13:45:01 ») ; RFC822 (« Mer, 14 déc 16 14:57:01 +0000 ») ; RFC850 (« Mercredi, 14-déc-16 14:57:00 UTC ») ; RFC1123 (« Mer, 14 déc 2016 14:57:00 +0000 »).</span><span class="sxs-lookup"><span data-stu-id="607b5-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="607b5-201">`Instrumentation key` de votre ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="607b5-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="607b5-202">Les données sont disponibles dans Analytics après quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="607b5-202">The data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="607b5-203">Réponses d’erreur</span><span class="sxs-lookup"><span data-stu-id="607b5-203">Error responses</span></span>

* <span data-ttu-id="607b5-204">**400 Demande incorrecte** : indique que la charge utile de la demande n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="607b5-204">**400 bad request**: indicates that the request payload is invalid.</span></span> <span data-ttu-id="607b5-205">Vérifiez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="607b5-205">Check:</span></span>
 * <span data-ttu-id="607b5-206">Clé d’instrumentation correcte.</span><span class="sxs-lookup"><span data-stu-id="607b5-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="607b5-207">Valeur de temps valide.</span><span class="sxs-lookup"><span data-stu-id="607b5-207">Valid time value.</span></span> <span data-ttu-id="607b5-208">Il s’agit de l’heure actuelle au format UTC.</span><span class="sxs-lookup"><span data-stu-id="607b5-208">It should be the time now in UTC.</span></span>
 * <span data-ttu-id="607b5-209">Le format JSON de l’événement est conforme au schéma.</span><span class="sxs-lookup"><span data-stu-id="607b5-209">JSON of the event conforms to the schema.</span></span>
* <span data-ttu-id="607b5-210">**403 Interdit** : le blob que vous avez envoyé n’est pas accessible.</span><span class="sxs-lookup"><span data-stu-id="607b5-210">**403 Forbidden**: The blob you've sent is not accessible.</span></span> <span data-ttu-id="607b5-211">Assurez-vous que la clé d’accès partagé est valide et n’a pas expiré.</span><span class="sxs-lookup"><span data-stu-id="607b5-211">Make sure that the shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="607b5-212">**404 Introuvable** :</span><span class="sxs-lookup"><span data-stu-id="607b5-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="607b5-213">Le blob n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="607b5-213">The blob doesn't exist.</span></span>
 * <span data-ttu-id="607b5-214">L’ID source est incorrect.</span><span class="sxs-lookup"><span data-stu-id="607b5-214">The sourceId is wrong.</span></span>

<span data-ttu-id="607b5-215">Des informations plus détaillées sont disponibles dans le message d’erreur de réponse.</span><span class="sxs-lookup"><span data-stu-id="607b5-215">More detailed information is available in the response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="607b5-216">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="607b5-216">Sample code</span></span>

<span data-ttu-id="607b5-217">Ce code utilise le package NuGet [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1).</span><span class="sxs-lookup"><span data-stu-id="607b5-217">This code uses the [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="607b5-218">Classes</span><span class="sxs-lookup"><span data-stu-id="607b5-218">Classes</span></span>

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a><span data-ttu-id="607b5-219">Réception de données</span><span class="sxs-lookup"><span data-stu-id="607b5-219">Ingest data</span></span>

<span data-ttu-id="607b5-220">Utilisez ce code pour chaque blob.</span><span class="sxs-lookup"><span data-stu-id="607b5-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="607b5-221">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="607b5-221">Next steps</span></span>

* [<span data-ttu-id="607b5-222">Présentation du langage de requête Log Analytics</span><span class="sxs-lookup"><span data-stu-id="607b5-222">Tour of the Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="607b5-223">Use *Logstash* to send data to Application Insights (Utiliser Logstash pour envoyer des données à Application Insights)</span><span class="sxs-lookup"><span data-stu-id="607b5-223">Use *Logstash* to send data to Application Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
