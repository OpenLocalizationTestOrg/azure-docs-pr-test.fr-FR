---
title: "aaaImport tooAnalytics de vos données dans Azure Application Insights | Documents Microsoft"
description: "Importer des toojoin de données statiques avec les données de télémétrie application, ou importer une tooquery de flux de données distinct avec Analytique."
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
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a><span data-ttu-id="0a029-104">Importer des données dans Analytics</span><span class="sxs-lookup"><span data-stu-id="0a029-104">Import data into Analytics</span></span>

<span data-ttu-id="0a029-105">Importer des données tabulaires dans [Analytique](app-insights-analytics.md), soit toojoin avec [Application Insights](app-insights-overview.md) télémétrie à partir de votre application, ou que vous pouvez les analyser comme un flux séparé.</span><span class="sxs-lookup"><span data-stu-id="0a029-105">Import any tabular data into [Analytics](app-insights-analytics.md), either toojoin it with [Application Insights](app-insights-overview.md) telemetry from your app, or so that you can analyze it as a separate stream.</span></span> <span data-ttu-id="0a029-106">Analytique est un flux de haut volume horodaté de requête puissantes language tooanalyzing convient parfaitement de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="0a029-106">Analytics is a powerful query language well-suited tooanalyzing high-volume timestamped streams of telemetry.</span></span>

<span data-ttu-id="0a029-107">Vous pouvez importer des données dans Analytics à l’aide de votre propre schéma.</span><span class="sxs-lookup"><span data-stu-id="0a029-107">You can import data into Analytics using your own schema.</span></span> <span data-ttu-id="0a029-108">Il n’a pas toouse hello Application Insights des schémas standard telles que la demande ou de trace.</span><span class="sxs-lookup"><span data-stu-id="0a029-108">It doesn't have toouse hello standard Application Insights schemas such as request or trace.</span></span>

<span data-ttu-id="0a029-109">Vous pouvez importer des fichiers JSON ou DSV (valeurs séparées par des délimiteurs : virgule, point-virgule ou tabulation).</span><span class="sxs-lookup"><span data-stu-id="0a029-109">You can import JSON or DSV (delimiter-separated values - comma, semicolon or tab) files.</span></span>

<span data-ttu-id="0a029-110">Il existe trois situations où il est utile de l’importation tooAnalytics :</span><span class="sxs-lookup"><span data-stu-id="0a029-110">There are three situations where importing tooAnalytics is useful:</span></span>

* <span data-ttu-id="0a029-111">**Association avec la télémétrie de l’application.**</span><span class="sxs-lookup"><span data-stu-id="0a029-111">**Join with app telemetry.**</span></span> <span data-ttu-id="0a029-112">Par exemple, vous pouvez importer une table qui mappe des URL à partir de vos titres de page lisible toomore site Web.</span><span class="sxs-lookup"><span data-stu-id="0a029-112">For example, you could import a table that maps URLs from your website toomore readable page titles.</span></span> <span data-ttu-id="0a029-113">Dans Analytique, vous pouvez créer un rapport de graphique du tableau de bord qui affiche des pages les plus populaires dix hello dans votre site Web.</span><span class="sxs-lookup"><span data-stu-id="0a029-113">In Analytics, you can create a dashboard chart report that shows hello ten most popular pages in your website.</span></span> <span data-ttu-id="0a029-114">Il peut désormais afficher hello titres des pages au lieu de l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="0a029-114">Now it can show hello page titles instead of hello URLs.</span></span>
* <span data-ttu-id="0a029-115">**Mettre en corrélation la télémétrie de votre application** avec d’autres sources telles que le trafic réseau, les données de serveur ou les fichiers journaux CDN.</span><span class="sxs-lookup"><span data-stu-id="0a029-115">**Correlate your application telemetry** with other sources such as network traffic, server data, or CDN log files.</span></span>
* <span data-ttu-id="0a029-116">**Appliquer le flux de données distinct tooa Analytique.**</span><span class="sxs-lookup"><span data-stu-id="0a029-116">**Apply Analytics tooa separate data stream.**</span></span> <span data-ttu-id="0a029-117">Application Insights Analytics est un outil puissant, qui fonctionne bien avec les flux horodatés partiellement alloués, et même beaucoup mieux que SQL dans la plupart des cas.</span><span class="sxs-lookup"><span data-stu-id="0a029-117">Application Insights Analytics is a powerful tool, that works well with sparse, timestamped streams - much better than SQL in many cases.</span></span> <span data-ttu-id="0a029-118">Si vous avez un flux de ce type issu d’une autre source, vous pouvez l’analyser avec Analytics.</span><span class="sxs-lookup"><span data-stu-id="0a029-118">If you have such a stream from some other source, you can analyze it with Analytics.</span></span>

<span data-ttu-id="0a029-119">Envoi source de données tooyour est facile.</span><span class="sxs-lookup"><span data-stu-id="0a029-119">Sending data tooyour data source is easy.</span></span> 

1. <span data-ttu-id="0a029-120">(Une fois) Définir le schéma hello de vos données dans une source de données.</span><span class="sxs-lookup"><span data-stu-id="0a029-120">(One time) Define hello schema of your data in a 'data source'.</span></span>
2. <span data-ttu-id="0a029-121">(Périodiquement) Télécharger des tooAzure de stockage de données, puis appelez hello API REST toonotify nouvelles données en attente pour l’ingestion.</span><span class="sxs-lookup"><span data-stu-id="0a029-121">(Periodically) Upload your data tooAzure storage, and call hello REST API toonotify us that new data is waiting for ingestion.</span></span> <span data-ttu-id="0a029-122">Dans quelques minutes, les données de salutation soient disponibles pour la requête Analytique.</span><span class="sxs-lookup"><span data-stu-id="0a029-122">Within a few minutes, hello data is available for query in Analytics.</span></span>

<span data-ttu-id="0a029-123">fréquence de téléchargement de hello Hello est définie par vous et la vitesse à laquelle vous souhaitez que votre toobe de données disponible pour les requêtes.</span><span class="sxs-lookup"><span data-stu-id="0a029-123">hello frequency of hello upload is defined by you and how fast would you like your data toobe available for queries.</span></span> <span data-ttu-id="0a029-124">Il est plus efficace des données tooupload en blocs plus volumineux, mais pas supérieure à 1 Go.</span><span class="sxs-lookup"><span data-stu-id="0a029-124">It is more efficient tooupload data in larger chunks, but not larger than 1GB.</span></span>

> [!NOTE]
> <span data-ttu-id="0a029-125">*Vous avez un grand nombre de tooanalyze des sources de données ?*</span><span class="sxs-lookup"><span data-stu-id="0a029-125">*Got lots of data sources tooanalyze?*</span></span> [<span data-ttu-id="0a029-126">*Envisagez d’utiliser* logstash *tooship vos données dans Application Insights.*</span><span class="sxs-lookup"><span data-stu-id="0a029-126">*Consider using* logstash *tooship your data into Application Insights.*</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a><span data-ttu-id="0a029-127">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="0a029-127">Before you start</span></span>

<span data-ttu-id="0a029-128">Ce dont vous avez besoin :</span><span class="sxs-lookup"><span data-stu-id="0a029-128">You need:</span></span>

1. <span data-ttu-id="0a029-129">Une ressource Application Insights dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0a029-129">An Application Insights resource in Microsoft Azure.</span></span>

 * <span data-ttu-id="0a029-130">Si vous souhaitez tooanalyze vos données séparément à partir de toutes les autres données de télémétrie, [créer une ressource Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="0a029-130">If you want tooanalyze your data separately from any other telemetry, [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span>
 * <span data-ttu-id="0a029-131">Si vous utilisez jointure ou la comparaison de vos données avec les données de télémétrie à partir d’une application qui est déjà configurée avec Application Insights, vous pouvez utiliser les ressources hello pour cette application.</span><span class="sxs-lookup"><span data-stu-id="0a029-131">If you're joining or comparing your data with telemetry from an app that is already set up with Application Insights, then you can use hello resource for that app.</span></span>
 * <span data-ttu-id="0a029-132">Ressource de toothat accès contributeur ou propriétaire.</span><span class="sxs-lookup"><span data-stu-id="0a029-132">Contributor or owner access toothat resource.</span></span>
 
2. <span data-ttu-id="0a029-133">stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0a029-133">Azure storage.</span></span> <span data-ttu-id="0a029-134">Vous téléchargez tooAzure stockage et Analytique obtienne de vos données à partir de là.</span><span class="sxs-lookup"><span data-stu-id="0a029-134">You upload tooAzure storage, and Analytics gets your data from there.</span></span> 

 * <span data-ttu-id="0a029-135">Nous vous recommandons de créer un compte de stockage dédié pour vos blobs.</span><span class="sxs-lookup"><span data-stu-id="0a029-135">We recommend you create a dedicated storage account for your blobs.</span></span> <span data-ttu-id="0a029-136">Si vos objets BLOB est partagés avec d’autres processus, il est plus long pour notre tooread processus vos objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="0a029-136">If your blobs are shared with other processes, it takes longer for our processes tooread your blobs.</span></span>


## <a name="define-your-schema"></a><span data-ttu-id="0a029-137">Définir votre schéma</span><span class="sxs-lookup"><span data-stu-id="0a029-137">Define your schema</span></span>

<span data-ttu-id="0a029-138">Vous pouvez importer des données, vous devez au préalable définir une *source de données,* qui spécifie le schéma hello de vos données.</span><span class="sxs-lookup"><span data-stu-id="0a029-138">Before you can import data, you must define a *data source,* which specifies hello schema of your data.</span></span>
<span data-ttu-id="0a029-139">Vous pouvez avoir des sources de données too50 dans une seule ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="0a029-139">You can have up too50 data sources in a single Application Insights resource</span></span>

1. <span data-ttu-id="0a029-140">Démarrer l’Assistant source de données hello.</span><span class="sxs-lookup"><span data-stu-id="0a029-140">Start hello data source wizard.</span></span> <span data-ttu-id="0a029-141">Utilisez le bouton Ajouter une nouvelle source de données.</span><span class="sxs-lookup"><span data-stu-id="0a029-141">Use "Add new data source" button.</span></span> <span data-ttu-id="0a029-142">Vous pouvez également cliquer sur le bouton Paramètres en haut à droite, puis choisir Sources de données dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="0a029-142">Alternatively - click on settings button in right upper corner and choose "Data Sources" in dropdown menu.</span></span>

    ![Ajouter une source de données](./media/app-insights-analytics-import/add-new-data-source.png)

    <span data-ttu-id="0a029-144">Entrez un nom pour votre nouvelle source de données.</span><span class="sxs-lookup"><span data-stu-id="0a029-144">Provide a name for your new data source.</span></span>

2. <span data-ttu-id="0a029-145">Définir le format des fichiers hello que vous allez télécharger.</span><span class="sxs-lookup"><span data-stu-id="0a029-145">Define format of hello files that you will upload.</span></span>

    <span data-ttu-id="0a029-146">Vous pouvez définir le format de hello manuellement, ou télécharger un exemple de fichier.</span><span class="sxs-lookup"><span data-stu-id="0a029-146">You can either define hello format manually, or upload a sample file.</span></span>

    <span data-ttu-id="0a029-147">Si les données de salutation sont au format CSV, hello de première ligne d’exemple hello permettre être des en-têtes de colonne.</span><span class="sxs-lookup"><span data-stu-id="0a029-147">If hello data is in CSV format, hello first row of hello sample can be column headers.</span></span> <span data-ttu-id="0a029-148">Vous pouvez modifier les noms de champs hello dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="0a029-148">You can change hello field names in hello next step.</span></span>

    <span data-ttu-id="0a029-149">exemple Hello doit inclure au moins 10 lignes ou des enregistrements de données.</span><span class="sxs-lookup"><span data-stu-id="0a029-149">hello sample should include at least 10 rows or records of data.</span></span>

    <span data-ttu-id="0a029-150">Les noms de colonnes ou de champs doivent avoir des noms alphanumériques (sans espaces ni ponctuation).</span><span class="sxs-lookup"><span data-stu-id="0a029-150">Column or field names should have alphanumeric names (without spaces or punctuation).</span></span>

    ![Charger un exemple de fichier](./media/app-insights-analytics-import/sample-data-file.png)


3. <span data-ttu-id="0a029-152">Schéma hello révision hello Assistant a.</span><span class="sxs-lookup"><span data-stu-id="0a029-152">Review hello schema that hello wizard has got.</span></span> <span data-ttu-id="0a029-153">Si il déduit les types hello à partir d’un échantillon, vous devrez peut-être tooadjust des types de hello déduit des colonnes de hello.</span><span class="sxs-lookup"><span data-stu-id="0a029-153">If it inferred hello types from a sample, you might need tooadjust hello inferred types of hello columns.</span></span>

    ![Schéma de hello déduit de révision](./media/app-insights-analytics-import/data-source-review-schema.png)

 * <span data-ttu-id="0a029-155">(Facultatif.) Téléchargez une définition de schéma.</span><span class="sxs-lookup"><span data-stu-id="0a029-155">(Optional.) Upload a schema definition.</span></span> <span data-ttu-id="0a029-156">Voir format hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0a029-156">See hello format below.</span></span>

 * <span data-ttu-id="0a029-157">Sélectionnez un horodatage.</span><span class="sxs-lookup"><span data-stu-id="0a029-157">Select a Timestamp.</span></span> <span data-ttu-id="0a029-158">Toutes les données dans Analytics doivent avoir un champ d’horodatage.</span><span class="sxs-lookup"><span data-stu-id="0a029-158">All data in Analytics must have a timestamp field.</span></span> <span data-ttu-id="0a029-159">Elle doit être de type `datetime`, mais il n’est pas toobe nommé « timestamp ».</span><span class="sxs-lookup"><span data-stu-id="0a029-159">It must have type `datetime`, but it doesn't have toobe named 'timestamp'.</span></span> <span data-ttu-id="0a029-160">Si vos données possèdent une colonne contenant une date et une heure au format ISO, choisissez cette option en tant que colonne de type timestamp hello.</span><span class="sxs-lookup"><span data-stu-id="0a029-160">If your data has a column containing a date and time in ISO format, choose this as hello timestamp column.</span></span> <span data-ttu-id="0a029-161">Sinon, choisissez « en tant que données arrivé » et les processus d’importation hello ajoute un champ d’horodatage.</span><span class="sxs-lookup"><span data-stu-id="0a029-161">Otherwise, choose "as data arrived", and hello import process will add a timestamp field.</span></span>

5. <span data-ttu-id="0a029-162">Créer la source de données hello.</span><span class="sxs-lookup"><span data-stu-id="0a029-162">Create hello data source.</span></span>

### <a name="schema-definition-file-format"></a><span data-ttu-id="0a029-163">Format de fichier de définition de schéma</span><span class="sxs-lookup"><span data-stu-id="0a029-163">Schema definition file format</span></span>

<span data-ttu-id="0a029-164">Plutôt que de modifier le schéma de hello dans l’interface utilisateur, vous pouvez charger la définition de schéma hello à partir d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="0a029-164">Instead of editing hello schema in UI, you can load hello schema definition from a file.</span></span> <span data-ttu-id="0a029-165">format de définition de schéma Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="0a029-165">hello schema definition format is as follows:</span></span> 

<span data-ttu-id="0a029-166">Format délimité</span><span class="sxs-lookup"><span data-stu-id="0a029-166">Delimited format</span></span> 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

<span data-ttu-id="0a029-167">Format JSON</span><span class="sxs-lookup"><span data-stu-id="0a029-167">JSON format</span></span> 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
<span data-ttu-id="0a029-168">Chaque colonne est identifié par type, nom et l’emplacement de hello.</span><span class="sxs-lookup"><span data-stu-id="0a029-168">Each column is identified by hello location, name and type.</span></span> 

* <span data-ttu-id="0a029-169">Emplacement – pour le format de fichier délimité, il est position hello de valeur de hello mappé.</span><span class="sxs-lookup"><span data-stu-id="0a029-169">Location – For delimited file format it is hello position of hello mapped value.</span></span> <span data-ttu-id="0a029-170">Pour le format JSON, il est jpath hello de clé de hello mappé.</span><span class="sxs-lookup"><span data-stu-id="0a029-170">For JSON format, it is hello jpath of hello mapped key.</span></span>
* <span data-ttu-id="0a029-171">Nom : hello affiche le nom de colonne de hello.</span><span class="sxs-lookup"><span data-stu-id="0a029-171">Name – hello displayed name of hello column.</span></span>
* <span data-ttu-id="0a029-172">Type : type de données hello de cette colonne.</span><span class="sxs-lookup"><span data-stu-id="0a029-172">Type – hello data type of that column.</span></span>
 
<span data-ttu-id="0a029-173">Au cas où un exemple de données a été utilisé et format de fichier est délimité, définition de schéma hello doit mapper toutes les colonnes et ajouter de nouvelles colonnes à la fin de hello.</span><span class="sxs-lookup"><span data-stu-id="0a029-173">In case a sample data was used and file format is delimited, hello schema definition must map all columns and add new columns at hello end.</span></span> 

<span data-ttu-id="0a029-174">JSON permet un mappage partiel des données de hello, par conséquent hello définition de schéma du format JSON ne dispose pas toomap toutes les clés qui se trouve dans les exemples de données.</span><span class="sxs-lookup"><span data-stu-id="0a029-174">JSON allows partial mapping of hello data, therefore hello schema definition of JSON format doesn’t have toomap every key which is found in a sample data.</span></span> <span data-ttu-id="0a029-175">Il peut également mapper des colonnes qui ne font pas partie des données d’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="0a029-175">It can also map columns which are not part of hello sample data.</span></span> 

## <a name="import-data"></a><span data-ttu-id="0a029-176">Importer des données</span><span class="sxs-lookup"><span data-stu-id="0a029-176">Import data</span></span>

<span data-ttu-id="0a029-177">tooimport des données, vous téléchargez-le tooAzure stockage, créer une clé d’accès pour celle-ci et appeler une API REST.</span><span class="sxs-lookup"><span data-stu-id="0a029-177">tooimport data, you upload it tooAzure storage, create an access key for it, and then make a REST API call.</span></span>

![Ajouter une source de données](./media/app-insights-analytics-import/analytics-upload-process.png)

<span data-ttu-id="0a029-179">Vous pouvez effectuer hello suivant le processus manuellement, ou définir d’une toodo automatique du système à intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="0a029-179">You can perform hello following process manually, or set up an automated system toodo it at regular intervals.</span></span> <span data-ttu-id="0a029-180">Vous devez toofollow ces étapes pour chaque bloc de données que vous souhaitez tooimport.</span><span class="sxs-lookup"><span data-stu-id="0a029-180">You need toofollow these steps for each block of data you want tooimport.</span></span>

1. <span data-ttu-id="0a029-181">Télécharger les données de salutation trop[stockage d’objets blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="0a029-181">Upload hello data too[Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> 

 * <span data-ttu-id="0a029-182">Objets BLOB peuvent être n’importe quelle taille des too1GB non compressé.</span><span class="sxs-lookup"><span data-stu-id="0a029-182">Blobs can be any size up too1GB uncompressed.</span></span> <span data-ttu-id="0a029-183">Les blobs d’une centaine de Mo sont parfaits, du point de vue des performances.</span><span class="sxs-lookup"><span data-stu-id="0a029-183">Large blobs of hundreds of MB are ideal from a performance perspective.</span></span>
 * <span data-ttu-id="0a029-184">Vous pouvez les compresser avec le temps de téléchargement tooimprove Gzip et la latence pour hello toobe de données disponible pour la requête.</span><span class="sxs-lookup"><span data-stu-id="0a029-184">You can compress it with Gzip tooimprove upload time and latency for hello data toobe available for query.</span></span> <span data-ttu-id="0a029-185">Hello d’utilisation `.gz` extension de nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="0a029-185">Use hello `.gz` filename extension.</span></span>
 * <span data-ttu-id="0a029-186">Il est meilleure toouse un compte de stockage distinct à cet effet, les appels de tooavoid à partir de différents services ralentit les performances.</span><span class="sxs-lookup"><span data-stu-id="0a029-186">It's best toouse a separate storage account for this purpose, tooavoid calls from different services slowing performance.</span></span>
 * <span data-ttu-id="0a029-187">Lors de l’envoi des données de haute fréquence, après quelques secondes, il est recommandé de toouse plus que d’un compte de stockage, pour des raisons de performances.</span><span class="sxs-lookup"><span data-stu-id="0a029-187">When sending data in high frequency, every few seconds, it is recommended toouse more than one storage account, for performance reasons.</span></span>

 
2. <span data-ttu-id="0a029-188">[Créer une clé de Signature d’accès partagé pour l’objet blob de hello](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="0a029-188">[Create a Shared Access Signature key for hello blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span> <span data-ttu-id="0a029-189">clé de Hello doit disposer d’un délai d’expiration d’un jour et fournir un accès en lecture.</span><span class="sxs-lookup"><span data-stu-id="0a029-189">hello key should have an expiration period of one day and provide read access.</span></span>
3. <span data-ttu-id="0a029-190">Rendre un toonotify d’appel REST Application Insights qui attendant des données.</span><span class="sxs-lookup"><span data-stu-id="0a029-190">Make a REST call toonotify Application Insights that data is waiting.</span></span>

 * <span data-ttu-id="0a029-191">Point de terminaison : `https://dc.services.visualstudio.com/v2/track`</span><span class="sxs-lookup"><span data-stu-id="0a029-191">Endpoint: `https://dc.services.visualstudio.com/v2/track`</span></span>
 * <span data-ttu-id="0a029-192">Méthode HTTP : POST</span><span class="sxs-lookup"><span data-stu-id="0a029-192">HTTP method: POST</span></span>
 * <span data-ttu-id="0a029-193">Charge utile :</span><span class="sxs-lookup"><span data-stu-id="0a029-193">Payload:</span></span>

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

<span data-ttu-id="0a029-194">espaces réservés de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="0a029-194">hello placeholders are:</span></span>

* <span data-ttu-id="0a029-195">`Blob URI with Shared Access Key`: Vous obtenez cette procédure de hello pour la création d’une clé.</span><span class="sxs-lookup"><span data-stu-id="0a029-195">`Blob URI with Shared Access Key`: You get this from hello procedure for creating a key.</span></span> <span data-ttu-id="0a029-196">Il s’agit d’objet blob de toohello spécifique.</span><span class="sxs-lookup"><span data-stu-id="0a029-196">It is specific toohello blob.</span></span>
* <span data-ttu-id="0a029-197">`Schema ID`: hello ID schéma généré pour votre schéma défini.</span><span class="sxs-lookup"><span data-stu-id="0a029-197">`Schema ID`: hello schema ID generated for your defined schema.</span></span> <span data-ttu-id="0a029-198">données Hello dans cet objet blob doivent être conforme toohello schéma.</span><span class="sxs-lookup"><span data-stu-id="0a029-198">hello data in this blob should conform toohello schema.</span></span>
* <span data-ttu-id="0a029-199">`DateTime`: heure de hello à quels hello demande est soumise, UTC.</span><span class="sxs-lookup"><span data-stu-id="0a029-199">`DateTime`: hello time at which hello request is submitted, UTC.</span></span> <span data-ttu-id="0a029-200">Nous acceptons les formats suivants : ISO8601 (comme « 2016-01-01 13:45:01 ») ; RFC822 (« Mer, 14 déc 16 14:57:01 +0000 ») ; RFC850 (« Mercredi, 14-déc-16 14:57:00 UTC ») ; RFC1123 (« Mer, 14 déc 2016 14:57:00 +0000 »).</span><span class="sxs-lookup"><span data-stu-id="0a029-200">We accept these formats: ISO8601 (like "2016-01-01 13:45:01"); RFC822 ("Wed, 14 Dec 16 14:57:01 +0000"); RFC850 ("Wednesday, 14-Dec-16 14:57:00 UTC"); RFC1123 ("Wed, 14 Dec 2016 14:57:00 +0000").</span></span>
* <span data-ttu-id="0a029-201">`Instrumentation key` de votre ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0a029-201">`Instrumentation key` of your Application Insights resource.</span></span>

<span data-ttu-id="0a029-202">les données de salutation sont disponibles dans Analytique après quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="0a029-202">hello data is available in Analytics after a few minutes.</span></span>

## <a name="error-responses"></a><span data-ttu-id="0a029-203">Réponses d’erreur</span><span class="sxs-lookup"><span data-stu-id="0a029-203">Error responses</span></span>

* <span data-ttu-id="0a029-204">**400 demande incorrecte**: indique cette charge utile de demande hello n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="0a029-204">**400 bad request**: indicates that hello request payload is invalid.</span></span> <span data-ttu-id="0a029-205">Vérifiez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="0a029-205">Check:</span></span>
 * <span data-ttu-id="0a029-206">Clé d’instrumentation correcte.</span><span class="sxs-lookup"><span data-stu-id="0a029-206">Correct instrumentation key.</span></span>
 * <span data-ttu-id="0a029-207">Valeur de temps valide.</span><span class="sxs-lookup"><span data-stu-id="0a029-207">Valid time value.</span></span> <span data-ttu-id="0a029-208">Il doit être hello maintenant en heure UTC.</span><span class="sxs-lookup"><span data-stu-id="0a029-208">It should be hello time now in UTC.</span></span>
 * <span data-ttu-id="0a029-209">JSON d’événement de hello est conforme toohello schéma.</span><span class="sxs-lookup"><span data-stu-id="0a029-209">JSON of hello event conforms toohello schema.</span></span>
* <span data-ttu-id="0a029-210">**403 Interdit**: blob hello que vous avez envoyé n’est pas accessible.</span><span class="sxs-lookup"><span data-stu-id="0a029-210">**403 Forbidden**: hello blob you've sent is not accessible.</span></span> <span data-ttu-id="0a029-211">Assurez-vous que cette clé d’accès partagé hello est valide et n’a pas expiré.</span><span class="sxs-lookup"><span data-stu-id="0a029-211">Make sure that hello shared access key is valid and has not expired.</span></span>
* <span data-ttu-id="0a029-212">**404 Introuvable** :</span><span class="sxs-lookup"><span data-stu-id="0a029-212">**404 Not Found**:</span></span>
 * <span data-ttu-id="0a029-213">objet blob de Hello n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="0a029-213">hello blob doesn't exist.</span></span>
 * <span data-ttu-id="0a029-214">Hello sourceId est incorrecte.</span><span class="sxs-lookup"><span data-stu-id="0a029-214">hello sourceId is wrong.</span></span>

<span data-ttu-id="0a029-215">Des informations plus détaillées sont disponibles dans le message d’erreur de réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="0a029-215">More detailed information is available in hello response error message.</span></span>


## <a name="sample-code"></a><span data-ttu-id="0a029-216">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="0a029-216">Sample code</span></span>

<span data-ttu-id="0a029-217">Ce code utilise hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) package NuGet.</span><span class="sxs-lookup"><span data-stu-id="0a029-217">This code uses hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) NuGet package.</span></span>

### <a name="classes"></a><span data-ttu-id="0a029-218">Classes</span><span class="sxs-lookup"><span data-stu-id="0a029-218">Classes</span></span>

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

### <a name="ingest-data"></a><span data-ttu-id="0a029-219">Réception de données</span><span class="sxs-lookup"><span data-stu-id="0a029-219">Ingest data</span></span>

<span data-ttu-id="0a029-220">Utilisez ce code pour chaque blob.</span><span class="sxs-lookup"><span data-stu-id="0a029-220">Use this code for each blob.</span></span> 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a><span data-ttu-id="0a029-221">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0a029-221">Next steps</span></span>

* [<span data-ttu-id="0a029-222">Visite guidée de hello langage de requête Analytique de journal</span><span class="sxs-lookup"><span data-stu-id="0a029-222">Tour of hello Log Analytics query language</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="0a029-223">Utilisez *Logstash* toosend données tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="0a029-223">Use *Logstash* toosend data tooApplication Insights</span></span>](https://github.com/Microsoft/logstash-output-application-insights)
