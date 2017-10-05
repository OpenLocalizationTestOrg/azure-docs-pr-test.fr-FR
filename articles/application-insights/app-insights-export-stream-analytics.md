---
title: "Exporter à l’aide de Stream Analytics à partir d’Azure Application Insights | Microsoft Docs"
description: "Stream Analytics peut transformer, filtrer et acheminer en continu les données que vous exportez depuis Application Insights."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6a84d8ff67c420ce712de905ab1172632502a863
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-stream-analytics-to-process-exported-data-from-application-insights"></a><span data-ttu-id="c9182-103">Utiliser Stream Analytics pour traiter des données exportées depuis Application Insights</span><span class="sxs-lookup"><span data-stu-id="c9182-103">Use Stream Analytics to process exported data from Application Insights</span></span>
<span data-ttu-id="c9182-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) est l’outil idéal pour traiter des données [exportées depuis Application Insights](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="c9182-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is the ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="c9182-105">Stream Analytics peut extraire des données de diverses sources.</span><span class="sxs-lookup"><span data-stu-id="c9182-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="c9182-106">Il peut transformer et filtrer les données, puis les acheminer vers plusieurs récepteurs.</span><span class="sxs-lookup"><span data-stu-id="c9182-106">It can transform and filter the data, and then route it to a variety of sinks.</span></span>

<span data-ttu-id="c9182-107">Dans cet exemple, nous allons créer une carte qui récupère des données d’Application Insights, renomme et traite certains champs, puis les dirige vers Power BI.</span><span class="sxs-lookup"><span data-stu-id="c9182-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of the fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="c9182-108">Il existe des [méthodes recommandées bien meilleures et plus simples pour afficher les données d’Application Insights dans Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="c9182-108">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="c9182-109">Le chemin d’accès illustré ici est un exemple pour illustrer comment traiter les données exportées.</span><span class="sxs-lookup"><span data-stu-id="c9182-109">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

![Diagramme de blocs pour l’exportation via SA vers PBI](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="c9182-111">Création d’un stockage dans Azure</span><span class="sxs-lookup"><span data-stu-id="c9182-111">Create storage in Azure</span></span>
<span data-ttu-id="c9182-112">Comme l’exportation continue génère toujours des données vers un compte de stockage Azure, vous devez commencer par créer ce stockage.</span><span class="sxs-lookup"><span data-stu-id="c9182-112">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="c9182-113">Créez un compte de stockage « classique » dans votre abonnement sur le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c9182-113">Create a "classic" storage account in your subscription in the [Azure portal](https://portal.azure.com).</span></span>
   
   ![Sur le portail Azure, choisissez Nouveau, Données, Stockage.](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="c9182-115">Créez un conteneur.</span><span class="sxs-lookup"><span data-stu-id="c9182-115">Create a container</span></span>
   
    ![Dans le nouvel emplacement de stockage, sélectionnez Conteneurs, cliquez sur la mosaïque Conteneurs puis sur Ajouter.](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="c9182-117">Copiez la clé d’accès au stockage.</span><span class="sxs-lookup"><span data-stu-id="c9182-117">Copy the storage access key</span></span>
   
    <span data-ttu-id="c9182-118">Vous en aurez bientôt besoin pour configurer l’entrée dans le service Stream analytics.</span><span class="sxs-lookup"><span data-stu-id="c9182-118">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![Dans le stockage, ouvrez Paramètres, Clés et copiez la clé d’accès principale.](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="c9182-120">Démarrer l’exportation continue vers le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="c9182-120">Start continuous export to Azure storage</span></span>
<span data-ttu-id="c9182-121">[exportation continue](app-insights-export-telemetry.md) déplace des données d'Application Insights vers le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c9182-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="c9182-122">Sur le portail Azure, accédez à la ressource Application Insights que vous avez créée pour votre application.</span><span class="sxs-lookup"><span data-stu-id="c9182-122">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Sélectionnez Parcourir, Application Insights, puis votre application.](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="c9182-124">Créez une exportation continue.</span><span class="sxs-lookup"><span data-stu-id="c9182-124">Create a continuous export.</span></span>
   
    ![Choisissez Paramètres, Exportation continue, Ajouter.](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="c9182-126">Sélectionnez le compte de stockage que vous avez préalablement créé.</span><span class="sxs-lookup"><span data-stu-id="c9182-126">Select the storage account you created earlier:</span></span>

    ![Définissez la destination de l’exportation.](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="c9182-128">Définissez les types d’événements que vous souhaitez afficher :</span><span class="sxs-lookup"><span data-stu-id="c9182-128">Set the event types you want to see:</span></span>

    ![Choisissez les types d’événements.](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="c9182-130">Laissez les données s'accumuler.</span><span class="sxs-lookup"><span data-stu-id="c9182-130">Let some data accumulate.</span></span> <span data-ttu-id="c9182-131">Installez-vous confortablement et laissez les utilisateurs utiliser votre application pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="c9182-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="c9182-132">Les données de télémétrie vont vous être transmises et vous permettre d’afficher des graphiques statistiques dans [Metrics explorer](app-insights-metrics-explorer.md) et des événements dans [Recherche de diagnostic](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="c9182-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="c9182-133">Les données seront également exportées vers votre stockage.</span><span class="sxs-lookup"><span data-stu-id="c9182-133">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="c9182-134">Inspectez les données exportées.</span><span class="sxs-lookup"><span data-stu-id="c9182-134">Inspect the exported data.</span></span> <span data-ttu-id="c9182-135">Dans Visual Studio, sélectionnez **Afficher / Cloud Explorer**, puis ouvrez Azure / Stockage.</span><span class="sxs-lookup"><span data-stu-id="c9182-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="c9182-136">(Si vous n'avez pas cette option, vous devez installer le SDK Azure : Ouvrez la boîte de dialogue Nouveau projet et ouvrez Visual C# / Cloud / Obtenir Microsoft Azure SDK pour .NET.)</span><span class="sxs-lookup"><span data-stu-id="c9182-136">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="c9182-137">Prenez note de la partie commune du nom du chemin d'accès, qui est dérivée du nom de l'application et de la clé d'instrumentation.</span><span class="sxs-lookup"><span data-stu-id="c9182-137">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="c9182-138">Les événements sont écrits dans des fichiers blob au format JSON.</span><span class="sxs-lookup"><span data-stu-id="c9182-138">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="c9182-139">Chaque fichier peut contenir un ou plusieurs événements.</span><span class="sxs-lookup"><span data-stu-id="c9182-139">Each file may contain one or more events.</span></span> <span data-ttu-id="c9182-140">Donc, nous devons lire les données d’événement et filtrer les champs voulus.</span><span class="sxs-lookup"><span data-stu-id="c9182-140">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="c9182-141">Nous pourrions effectuer toutes sortes d'opérations avec les données, mais notre objectif aujourd'hui est d'utiliser Stream Analytics pour transmettre les données vers Power BI.</span><span class="sxs-lookup"><span data-stu-id="c9182-141">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to pipe the data to Power BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="c9182-142">Création d’une instance Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c9182-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="c9182-143">À partir du [portail classique Azure](https://manage.windowsazure.com/), sélectionnez le service Azure Stream Analytics et créez une nouvelle tâche Stream Analytics :</span><span class="sxs-lookup"><span data-stu-id="c9182-143">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="c9182-144">Une fois la tâche créée, développez les informations qui s’y rapportent :</span><span class="sxs-lookup"><span data-stu-id="c9182-144">When the new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="c9182-145">Définition de l’emplacement des objets blob</span><span class="sxs-lookup"><span data-stu-id="c9182-145">Set blob location</span></span>
<span data-ttu-id="c9182-146">Définissez-le pour qu’il tienne compte des données de votre objet blob d’exportation continue :</span><span class="sxs-lookup"><span data-stu-id="c9182-146">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="c9182-147">Vous devez maintenant disposer de la clé d’accès principale issue de votre compte de stockage, que vous avez notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="c9182-147">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="c9182-148">Définissez-la comme clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c9182-148">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="c9182-149">Définition de la séquence d’octets préfixe du chemin d’accès</span><span class="sxs-lookup"><span data-stu-id="c9182-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="c9182-150">**Veillez à définir le format de date sur AAAA-MM-JJ (avec des tirets).**</span><span class="sxs-lookup"><span data-stu-id="c9182-150">**Be sure to set the Date Format to YYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="c9182-151">La séquence d'octets préfixe du chemin d'accès spécifie où Stream Analytics recherche les fichiers d'entrée dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="c9182-151">The Path Prefix Pattern specifies where Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="c9182-152">Vous devez la configurer pour correspondre au mode de stockage des données de l'exportation continue.</span><span class="sxs-lookup"><span data-stu-id="c9182-152">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="c9182-153">Définissez-la comme suit :</span><span class="sxs-lookup"><span data-stu-id="c9182-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="c9182-154">Dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="c9182-154">In this example:</span></span>

* <span data-ttu-id="c9182-155">`webapplication27` est le nom de la ressource Application Insights, **tout en minuscules**.</span><span class="sxs-lookup"><span data-stu-id="c9182-155">`webapplication27` is the name of the Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="c9182-156">`1234...` est la clé d'instrumentation de la ressource Application Insights, **sans les tirets**.</span><span class="sxs-lookup"><span data-stu-id="c9182-156">`1234...` is the instrumentation key of the Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="c9182-157">`PageViews` est le type de données que vous souhaitez analyser.</span><span class="sxs-lookup"><span data-stu-id="c9182-157">`PageViews` is the type of data you want to analyze.</span></span> <span data-ttu-id="c9182-158">Les types disponibles varient selon le filtre que vous définissez dans l’exportation continue.</span><span class="sxs-lookup"><span data-stu-id="c9182-158">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="c9182-159">Examinez les données exportées pour voir les autres types disponibles et consultez le [modèle d’exportation de données](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="c9182-159">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="c9182-160">`/{date}/{time}` est une séquence écrite de manière littérale.</span><span class="sxs-lookup"><span data-stu-id="c9182-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="c9182-161">Vérifiez le stockage pour être sûr d'avoir le chemin d'accès approprié.</span><span class="sxs-lookup"><span data-stu-id="c9182-161">Inspect the storage to make sure you get the path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="c9182-162">Fin de l’installation initiale</span><span class="sxs-lookup"><span data-stu-id="c9182-162">Finish initial setup</span></span>
<span data-ttu-id="c9182-163">Confirmez le format de sérialisation :</span><span class="sxs-lookup"><span data-stu-id="c9182-163">Confirm the serialization format:</span></span>

![Confirmez et fermez l’assistant.](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="c9182-165">Fermez l’assistant et attendez la fin de l’installation.</span><span class="sxs-lookup"><span data-stu-id="c9182-165">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="c9182-166">Utilisez l'exemple de commande pour télécharger des données.</span><span class="sxs-lookup"><span data-stu-id="c9182-166">Use the Sample command to download some data.</span></span> <span data-ttu-id="c9182-167">Gardez-le comme exemple de test pour déboguer votre requête.</span><span class="sxs-lookup"><span data-stu-id="c9182-167">Keep it as a test sample to debug your query.</span></span>
> 
> 

## <a name="set-the-output"></a><span data-ttu-id="c9182-168">Définir la sortie</span><span class="sxs-lookup"><span data-stu-id="c9182-168">Set the output</span></span>
<span data-ttu-id="c9182-169">Sélectionnez maintenant votre tâche et définissez la sortie.</span><span class="sxs-lookup"><span data-stu-id="c9182-169">Now select your job and set the output.</span></span>

![Sélectionnez le nouveau canal, cliquez sur Sorties, Ajouter, Power BI](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="c9182-171">Indiquez votre **compte professionnel ou scolaire** pour autoriser Stream Analytics à accéder à votre ressource Power BI.</span><span class="sxs-lookup"><span data-stu-id="c9182-171">Provide your **work or school account** to authorize Stream Analytics to access your Power BI resource.</span></span> <span data-ttu-id="c9182-172">Inventez ensuite un nom pour la sortie et le jeu de données et la table Power BI cibles.</span><span class="sxs-lookup"><span data-stu-id="c9182-172">Then invent a name for the output, and for the target Power BI dataset and table.</span></span>

![Inventer trois noms](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-the-query"></a><span data-ttu-id="c9182-174">Définir la requête</span><span class="sxs-lookup"><span data-stu-id="c9182-174">Set the query</span></span>
<span data-ttu-id="c9182-175">La requête régit la traduction de l’entrée vers la sortie.</span><span class="sxs-lookup"><span data-stu-id="c9182-175">The query governs the translation from input to output.</span></span>

![Sélectionnez la tâche et cliquez sur Interroger.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="c9182-178">Utilisez la fonction de Test pour vérifier que vous obtenez le résultat approprié.</span><span class="sxs-lookup"><span data-stu-id="c9182-178">Use the Test function to check that you get the right output.</span></span> <span data-ttu-id="c9182-179">Indiquez les exemples de données que vous avez copiés de la page d'entrées.</span><span class="sxs-lookup"><span data-stu-id="c9182-179">Give it the sample data that you took from the inputs page.</span></span> 

### <a name="query-to-display-counts-of-events"></a><span data-ttu-id="c9182-180">Requête d'affichage du nombre d'événements</span><span class="sxs-lookup"><span data-stu-id="c9182-180">Query to display counts of events</span></span>
<span data-ttu-id="c9182-181">Collez cette requête :</span><span class="sxs-lookup"><span data-stu-id="c9182-181">Paste this query:</span></span>

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* <span data-ttu-id="c9182-182">export-input est l’alias que nous avons donné au flux d’entrée</span><span class="sxs-lookup"><span data-stu-id="c9182-182">export-input is the alias we gave to the stream input</span></span>
* <span data-ttu-id="c9182-183">pbi-output est l’alias de sortie que nous avons défini</span><span class="sxs-lookup"><span data-stu-id="c9182-183">pbi-output is the output alias we defined</span></span>
* <span data-ttu-id="c9182-184">Nous utilisons [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) , car le nom de l'événement se trouve dans un tableau JSON imbriqué.</span><span class="sxs-lookup"><span data-stu-id="c9182-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because the event name is in a nested JSON arrray.</span></span> <span data-ttu-id="c9182-185">Ensuite, l’instruction Select récupère le nom de l’événement, ainsi que le nombre d’instances portant ce nom dans la période donnée.</span><span class="sxs-lookup"><span data-stu-id="c9182-185">Then the Select picks the event name, together with a count of the number of instances with that name in the time period.</span></span> <span data-ttu-id="c9182-186">La clause [Regrouper par](https://msdn.microsoft.com/library/azure/dn835023.aspx) regroupe les éléments en intervalles d'1 minute.</span><span class="sxs-lookup"><span data-stu-id="c9182-186">The [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups the elements into time periods of 1 minute.</span></span>

### <a name="query-to-display-metric-values"></a><span data-ttu-id="c9182-187">Requête d'affichage des valeurs de mesure</span><span class="sxs-lookup"><span data-stu-id="c9182-187">Query to display metric values</span></span>
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* <span data-ttu-id="c9182-188">Cette requête explore la télémétrie des mesures pour obtenir l'heure de l'événement et la valeur de mesure.</span><span class="sxs-lookup"><span data-stu-id="c9182-188">This query drills into the metrics telemetry to get the event time and the metric value.</span></span> <span data-ttu-id="c9182-189">Les valeurs de mesure se trouvent dans un tableau, donc nous utilisons le modèle OUTER APPLY GetElements pour extraire les lignes.</span><span class="sxs-lookup"><span data-stu-id="c9182-189">The metric values are inside an array, so we use the OUTER APPLY GetElements pattern to extract the rows.</span></span> <span data-ttu-id="c9182-190">Dans ce cas, « myMetric » est le nom de la mesure.</span><span class="sxs-lookup"><span data-stu-id="c9182-190">"myMetric" is the name of the metric in this case.</span></span> 

### <a name="query-to-include-values-of-dimension-properties"></a><span data-ttu-id="c9182-191">Requête d’inclusion de valeurs de propriétés de dimension</span><span class="sxs-lookup"><span data-stu-id="c9182-191">Query to include values of dimension properties</span></span>
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* <span data-ttu-id="c9182-192">Cette requête inclut les valeurs des propriétés de dimension, indépendamment d’une dimension particulière se trouvant à un index fixe dans le tableau de dimension.</span><span class="sxs-lookup"><span data-stu-id="c9182-192">This query includes values of the dimension properties without depending on a particular dimension being at a fixed index in the dimension array.</span></span>

## <a name="run-the-job"></a><span data-ttu-id="c9182-193">Exécution de la tâche</span><span class="sxs-lookup"><span data-stu-id="c9182-193">Run the job</span></span>
<span data-ttu-id="c9182-194">Vous pouvez sélectionner une date dans le passé à partir de laquelle démarrer la tâche.</span><span class="sxs-lookup"><span data-stu-id="c9182-194">You can select a date in the past to start the job from.</span></span> 

![Sélectionnez la tâche et cliquez sur Interroger.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="c9182-197">Attendez que le travail s’exécute.</span><span class="sxs-lookup"><span data-stu-id="c9182-197">Wait until the job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="c9182-198">Afficher les résultats dans Power BI</span><span class="sxs-lookup"><span data-stu-id="c9182-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="c9182-199">Il existe des [méthodes recommandées bien meilleures et plus simples pour afficher les données d’Application Insights dans Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="c9182-199">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="c9182-200">Le chemin d’accès illustré ici est un exemple pour illustrer comment traiter les données exportées.</span><span class="sxs-lookup"><span data-stu-id="c9182-200">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

<span data-ttu-id="c9182-201">Ouvrez Power BI avec votre compte professionnel ou scolaire, puis sélectionnez le jeu de données et la table que vous avez définis comme sortie de la tâche Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="c9182-201">Open Power BI with your work or school account, and select the dataset and table that you defined as the output of the Stream Analytics job.</span></span>

![Dans Power BI, sélectionnez votre dataset et vos champs.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="c9182-203">Vous pouvez maintenant utiliser ce jeu de données dans des rapports et des tableaux de bord dans [Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c9182-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![Dans Power BI, sélectionnez votre dataset et vos champs.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="c9182-205">Pas de données ?</span><span class="sxs-lookup"><span data-stu-id="c9182-205">No data?</span></span>
* <span data-ttu-id="c9182-206">Vérifiez que vous avez [défini le format de date](#set-path-prefix-pattern) correctement sur AAAA-MM-JJ (avec des tirets).</span><span class="sxs-lookup"><span data-stu-id="c9182-206">Check that you [set the date format](#set-path-prefix-pattern) correctly to YYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="c9182-207">Vidéo</span><span class="sxs-lookup"><span data-stu-id="c9182-207">Video</span></span>
<span data-ttu-id="c9182-208">Noam Ben Zeev montre comment traiter des données exportées à l’aide de Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="c9182-208">Noam Ben Zeev shows how to process exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c9182-209">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c9182-209">Next steps</span></span>
* [<span data-ttu-id="c9182-210">Exportation continue</span><span class="sxs-lookup"><span data-stu-id="c9182-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="c9182-211">Référence de modèle de données détaillé pour les valeurs et types de propriétés.</span><span class="sxs-lookup"><span data-stu-id="c9182-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="c9182-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="c9182-212">Application Insights</span></span>](app-insights-overview.md)

