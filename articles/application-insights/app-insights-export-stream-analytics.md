---
title: "aaaExport à l’aide d’Analytique de flux de données à partir de l’Application Azure Insights | Documents Microsoft"
description: "Flux de données Analytique peut se transformer en permanence, filtrer et acheminer les données de salutation que vous exportez à partir de l’Application Insights."
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
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a><span data-ttu-id="ff92e-103">Tooprocess de flux de données Analytique d’utilisation des données exportées à partir de l’Application Insights</span><span class="sxs-lookup"><span data-stu-id="ff92e-103">Use Stream Analytics tooprocess exported data from Application Insights</span></span>
<span data-ttu-id="ff92e-104">[Analytique de flux de données Azure](https://azure.microsoft.com/services/stream-analytics/) est l’outil idéal de hello pour le traitement des données [exporté à partir de l’Application Insights](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="ff92e-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is hello ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="ff92e-105">Stream Analytics peut extraire des données de diverses sources.</span><span class="sxs-lookup"><span data-stu-id="ff92e-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="ff92e-106">Il peut transformer et filtrer les données de hello et router tooa diverses récepteurs.</span><span class="sxs-lookup"><span data-stu-id="ff92e-106">It can transform and filter hello data, and then route it tooa variety of sinks.</span></span>

<span data-ttu-id="ff92e-107">Dans cet exemple, nous allons créer un adaptateur qui Récupère des données d’Application Insights, changements de noms et traite certains des champs de hello et dirige dans Power BI.</span><span class="sxs-lookup"><span data-stu-id="ff92e-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of hello fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="ff92e-108">Il existe beaucoup plus facile et [méthodes recommandées pour données d’Application Insights toodisplay dans Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="ff92e-108">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="ff92e-109">Hello chemin illustrée ici est simplement un tooillustrate exemple tooprocess comment les données exportées.</span><span class="sxs-lookup"><span data-stu-id="ff92e-109">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

![Diagramme de blocs pour une exportation via SA tooPBI](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="ff92e-111">Création d’un stockage dans Azure</span><span class="sxs-lookup"><span data-stu-id="ff92e-111">Create storage in Azure</span></span>
<span data-ttu-id="ff92e-112">Exportation continue retourne toujours le compte de stockage Azure données tooan, donc vous devez tout d’abord le stockage de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ff92e-112">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="ff92e-113">Créer un compte de stockage « classiques » dans votre abonnement Bonjour [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ff92e-113">Create a "classic" storage account in your subscription in hello [Azure portal](https://portal.azure.com).</span></span>
   
   ![Sur le portail Azure, choisissez Nouveau, Données, Stockage.](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="ff92e-115">Créez un conteneur.</span><span class="sxs-lookup"><span data-stu-id="ff92e-115">Create a container</span></span>
   
    ![Dans un nouveau stockage hello, sélectionnez les conteneurs, cliquez sur la vignette de conteneurs hello, puis sur Ajouter](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="ff92e-117">Copiez la clé d’accès de stockage de hello</span><span class="sxs-lookup"><span data-stu-id="ff92e-117">Copy hello storage access key</span></span>
   
    <span data-ttu-id="ff92e-118">Vous en aurez besoin dès tooset hello toohello d’entrée flux analytique service.</span><span class="sxs-lookup"><span data-stu-id="ff92e-118">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![Dans le stockage de hello, ouvrez les paramètres, clés et effectuer une copie de hello clé d’accès primaire](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="ff92e-120">Démarrer l’exportation continue tooAzure stockage</span><span class="sxs-lookup"><span data-stu-id="ff92e-120">Start continuous export tooAzure storage</span></span>
<span data-ttu-id="ff92e-121">[exportation continue](app-insights-export-telemetry.md) déplace des données d'Application Insights vers le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ff92e-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="ff92e-122">Bonjour portail Azure, parcourir les ressources d’Application Insights toohello que vous avez créé pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ff92e-122">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Sélectionnez Parcourir, Application Insights, puis votre application.](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="ff92e-124">Créez une exportation continue.</span><span class="sxs-lookup"><span data-stu-id="ff92e-124">Create a continuous export.</span></span>
   
    ![Choisissez Paramètres, Exportation continue, Ajouter.](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="ff92e-126">Sélectionnez le compte de stockage hello que vous avez créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="ff92e-126">Select hello storage account you created earlier:</span></span>

    ![Définir la destination de l’exportation hello](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="ff92e-128">Définir les types d’événement hello toosee :</span><span class="sxs-lookup"><span data-stu-id="ff92e-128">Set hello event types you want toosee:</span></span>

    ![Choisissez les types d’événements.](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="ff92e-130">Laissez les données s'accumuler.</span><span class="sxs-lookup"><span data-stu-id="ff92e-130">Let some data accumulate.</span></span> <span data-ttu-id="ff92e-131">Installez-vous confortablement et laissez les utilisateurs utiliser votre application pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="ff92e-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="ff92e-132">Les données de télémétrie vont vous être transmises et vous permettre d’afficher des graphiques statistiques dans [Metrics explorer](app-insights-metrics-explorer.md) et des événements dans [Recherche de diagnostic](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="ff92e-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="ff92e-133">Et, en outre, les données de salutation exportera tooyour stockage.</span><span class="sxs-lookup"><span data-stu-id="ff92e-133">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="ff92e-134">Inspecter les données hello exportée.</span><span class="sxs-lookup"><span data-stu-id="ff92e-134">Inspect hello exported data.</span></span> <span data-ttu-id="ff92e-135">Dans Visual Studio, sélectionnez **Afficher / Cloud Explorer**, puis ouvrez Azure / Stockage.</span><span class="sxs-lookup"><span data-stu-id="ff92e-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="ff92e-136">(Si vous n’avez pas cette option de menu, vous devez tooinstall hello Azure SDK : ouvrir la boîte de dialogue Nouveau projet hello et ouvrez Visual C# / Cloud / obtenir Microsoft Azure SDK pour .NET.)</span><span class="sxs-lookup"><span data-stu-id="ff92e-136">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="ff92e-137">Prenez note de la partie commune de hello du nom de chemin d’accès de hello, qui est dérivé de la clé de nom et d’instrumentation application hello.</span><span class="sxs-lookup"><span data-stu-id="ff92e-137">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="ff92e-138">événements de Hello sont écrits les fichiers de tooblob au format JSON.</span><span class="sxs-lookup"><span data-stu-id="ff92e-138">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="ff92e-139">Chaque fichier peut contenir un ou plusieurs événements.</span><span class="sxs-lookup"><span data-stu-id="ff92e-139">Each file may contain one or more events.</span></span> <span data-ttu-id="ff92e-140">Par conséquent, nous souhaitons les données d’événement tooread hello et filtrer les champs hello.</span><span class="sxs-lookup"><span data-stu-id="ff92e-140">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="ff92e-141">Il existe toutes sortes de choses que nous pouvons faire avec les données de hello, mais notre plan est aujourd'hui toouse flux Analytique toopipe hello données tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="ff92e-141">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toopipe hello data tooPower BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="ff92e-142">Création d’une instance Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ff92e-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="ff92e-143">À partir de hello [portail Azure Classic](https://manage.windowsazure.com/), sélectionnez le service d’Analytique de flux de données Azure hello et créer une nouvelle tâche de flux de données Analytique :</span><span class="sxs-lookup"><span data-stu-id="ff92e-143">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="ff92e-144">Lors de la création de tâche hello, développer ses détails :</span><span class="sxs-lookup"><span data-stu-id="ff92e-144">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="ff92e-145">Définition de l’emplacement des objets blob</span><span class="sxs-lookup"><span data-stu-id="ff92e-145">Set blob location</span></span>
<span data-ttu-id="ff92e-146">Définissez-le entrée tootake à partir de votre objet blob de l’exportation continue :</span><span class="sxs-lookup"><span data-stu-id="ff92e-146">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="ff92e-147">Vous devez maintenant hello clé d’accès primaire à partir de votre compte de stockage que vous avez notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="ff92e-147">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="ff92e-148">Définir en tant que clé de compte de stockage de hello.</span><span class="sxs-lookup"><span data-stu-id="ff92e-148">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="ff92e-149">Définition de la séquence d’octets préfixe du chemin d’accès</span><span class="sxs-lookup"><span data-stu-id="ff92e-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="ff92e-150">**Être vraiment tooset hello Format de Date tooYYYY-MM-JJ (avec les tirets).**</span><span class="sxs-lookup"><span data-stu-id="ff92e-150">**Be sure tooset hello Date Format tooYYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="ff92e-151">Hello modèle du préfixe de chemin d’accès spécifie où Analytique de flux de données recherche les fichiers d’entrée hello dans le stockage hello.</span><span class="sxs-lookup"><span data-stu-id="ff92e-151">hello Path Prefix Pattern specifies where Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="ff92e-152">Vous devez tooset il toohow toocorrespond de l’exportation continue stocke les données de hello.</span><span class="sxs-lookup"><span data-stu-id="ff92e-152">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="ff92e-153">Définissez-la comme suit :</span><span class="sxs-lookup"><span data-stu-id="ff92e-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="ff92e-154">Dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="ff92e-154">In this example:</span></span>

* <span data-ttu-id="ff92e-155">`webapplication27`est le nom hello Hello ressource Application Insights **toutes les minuscules**.</span><span class="sxs-lookup"><span data-stu-id="ff92e-155">`webapplication27` is hello name of hello Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="ff92e-156">`1234...`est la clé d’instrumentation hello Hello ressource Application Insights, **l’omission de tirets**.</span><span class="sxs-lookup"><span data-stu-id="ff92e-156">`1234...` is hello instrumentation key of hello Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="ff92e-157">`PageViews`est de type de hello de données vous souhaitez tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="ff92e-157">`PageViews` is hello type of data you want tooanalyze.</span></span> <span data-ttu-id="ff92e-158">les types disponibles Hello dépendent de filtre hello que vous définissez dans l’exportation continue.</span><span class="sxs-lookup"><span data-stu-id="ff92e-158">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="ff92e-159">Examiner les autres types disponibles hello de toosee données exportées hello et consultez hello [exporter le modèle de données](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="ff92e-159">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="ff92e-160">`/{date}/{time}` est une séquence écrite de manière littérale.</span><span class="sxs-lookup"><span data-stu-id="ff92e-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="ff92e-161">Vérifiez que hello toomake de stockage que vous obtenez le chemin d’accès hello droite.</span><span class="sxs-lookup"><span data-stu-id="ff92e-161">Inspect hello storage toomake sure you get hello path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="ff92e-162">Fin de l’installation initiale</span><span class="sxs-lookup"><span data-stu-id="ff92e-162">Finish initial setup</span></span>
<span data-ttu-id="ff92e-163">Vérifiez le format de sérialisation hello :</span><span class="sxs-lookup"><span data-stu-id="ff92e-163">Confirm hello serialization format:</span></span>

![Confirmez et fermez l’assistant.](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="ff92e-165">Fermez l’Assistant de hello et attendez hello le programme d’installation toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ff92e-165">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="ff92e-166">Utilisez toodownload de commande exemple hello certaines données.</span><span class="sxs-lookup"><span data-stu-id="ff92e-166">Use hello Sample command toodownload some data.</span></span> <span data-ttu-id="ff92e-167">Conserver en un toodebug d’exemple de test de votre requête.</span><span class="sxs-lookup"><span data-stu-id="ff92e-167">Keep it as a test sample toodebug your query.</span></span>
> 
> 

## <a name="set-hello-output"></a><span data-ttu-id="ff92e-168">Sortie hello</span><span class="sxs-lookup"><span data-stu-id="ff92e-168">Set hello output</span></span>
<span data-ttu-id="ff92e-169">Sélectionnez votre projet et définissez hello sortie.</span><span class="sxs-lookup"><span data-stu-id="ff92e-169">Now select your job and set hello output.</span></span>

![Sélectionnez le nouveau canal de hello, cliquez sur les sorties, ajouter, Power BI](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="ff92e-171">Fournissez votre **compte professionnel ou scolaire** tooauthorize tooaccess de flux de données Analytique votre ressource Power BI.</span><span class="sxs-lookup"><span data-stu-id="ff92e-171">Provide your **work or school account** tooauthorize Stream Analytics tooaccess your Power BI resource.</span></span> <span data-ttu-id="ff92e-172">Puis inventer un nom pour la sortie de hello et pour la table et le jeu de données Power BI hello cible.</span><span class="sxs-lookup"><span data-stu-id="ff92e-172">Then invent a name for hello output, and for hello target Power BI dataset and table.</span></span>

![Inventer trois noms](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a><span data-ttu-id="ff92e-174">Requête hello de jeu</span><span class="sxs-lookup"><span data-stu-id="ff92e-174">Set hello query</span></span>
<span data-ttu-id="ff92e-175">requête de Hello détermine la traduction hello toooutput d’entrée.</span><span class="sxs-lookup"><span data-stu-id="ff92e-175">hello query governs hello translation from input toooutput.</span></span>

![Sélectionnez le travail de hello et cliquez sur la requête.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="ff92e-178">Utilisez hello Test fonction toocheck que vous obtenez une sortie de droite hello.</span><span class="sxs-lookup"><span data-stu-id="ff92e-178">Use hello Test function toocheck that you get hello right output.</span></span> <span data-ttu-id="ff92e-179">Lui donner des exemples de données hello que vous avez suivies à partir de la page d’entrées hello.</span><span class="sxs-lookup"><span data-stu-id="ff92e-179">Give it hello sample data that you took from hello inputs page.</span></span> 

### <a name="query-toodisplay-counts-of-events"></a><span data-ttu-id="ff92e-180">Toodisplay les décomptes d’événements de requête</span><span class="sxs-lookup"><span data-stu-id="ff92e-180">Query toodisplay counts of events</span></span>
<span data-ttu-id="ff92e-181">Collez cette requête :</span><span class="sxs-lookup"><span data-stu-id="ff92e-181">Paste this query:</span></span>

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

* <span data-ttu-id="ff92e-182">entrée de l’exportation est alias hello nous a donné d’entrée de flux toohello</span><span class="sxs-lookup"><span data-stu-id="ff92e-182">export-input is hello alias we gave toohello stream input</span></span>
* <span data-ttu-id="ff92e-183">pbi-sortie est l’alias de sortie hello nous avons défini</span><span class="sxs-lookup"><span data-stu-id="ff92e-183">pbi-output is hello output alias we defined</span></span>
* <span data-ttu-id="ff92e-184">Nous utilisons [externe GetElements appliquer](https://msdn.microsoft.com/library/azure/dn706229.aspx) , car le nom de l’événement hello est dans un arrray JSON imbriquée.</span><span class="sxs-lookup"><span data-stu-id="ff92e-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because hello event name is in a nested JSON arrray.</span></span> <span data-ttu-id="ff92e-185">Puis récupère de Select hello hello nom d’événement, ainsi que de nombre hello d’instances de ce nom dans hello laps de temps.</span><span class="sxs-lookup"><span data-stu-id="ff92e-185">Then hello Select picks hello event name, together with a count of hello number of instances with that name in hello time period.</span></span> <span data-ttu-id="ff92e-186">Hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause regroupe les éléments hello dans des périodes de 1 minute.</span><span class="sxs-lookup"><span data-stu-id="ff92e-186">hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups hello elements into time periods of 1 minute.</span></span>

### <a name="query-toodisplay-metric-values"></a><span data-ttu-id="ff92e-187">Les valeurs de mesure toodisplay de requête</span><span class="sxs-lookup"><span data-stu-id="ff92e-187">Query toodisplay metric values</span></span>
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

* <span data-ttu-id="ff92e-188">Cette requête explore heure de l’événement hello métriques télémétrie tooget hello et la valeur de métrique hello.</span><span class="sxs-lookup"><span data-stu-id="ff92e-188">This query drills into hello metrics telemetry tooget hello event time and hello metric value.</span></span> <span data-ttu-id="ff92e-189">les valeurs de mesure Hello étant à l’intérieur d’un tableau, nous utilisent les hello externe GetElements Appliquer modèle tooextract hello lignes.</span><span class="sxs-lookup"><span data-stu-id="ff92e-189">hello metric values are inside an array, so we use hello OUTER APPLY GetElements pattern tooextract hello rows.</span></span> <span data-ttu-id="ff92e-190">« myMetric » désigne hello métrique de hello dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="ff92e-190">"myMetric" is hello name of hello metric in this case.</span></span> 

### <a name="query-tooinclude-values-of-dimension-properties"></a><span data-ttu-id="ff92e-191">Requête tooinclude les valeurs de propriétés de dimension</span><span class="sxs-lookup"><span data-stu-id="ff92e-191">Query tooinclude values of dimension properties</span></span>
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

* <span data-ttu-id="ff92e-192">Cette requête inclut les valeurs des propriétés de dimension hello sans en fonction d’une dimension particulière en cours à l’index de tableau à une dimension hello fixe.</span><span class="sxs-lookup"><span data-stu-id="ff92e-192">This query includes values of hello dimension properties without depending on a particular dimension being at a fixed index in hello dimension array.</span></span>

## <a name="run-hello-job"></a><span data-ttu-id="ff92e-193">Exécuter la tâche de hello</span><span class="sxs-lookup"><span data-stu-id="ff92e-193">Run hello job</span></span>
<span data-ttu-id="ff92e-194">Vous pouvez sélectionner une date dans hello au-delà de travail de hello toostart à partir de.</span><span class="sxs-lookup"><span data-stu-id="ff92e-194">You can select a date in hello past toostart hello job from.</span></span> 

![Sélectionnez le travail de hello et cliquez sur la requête.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="ff92e-197">Attendez que l’exécution du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="ff92e-197">Wait until hello job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="ff92e-198">Afficher les résultats dans Power BI</span><span class="sxs-lookup"><span data-stu-id="ff92e-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="ff92e-199">Il existe beaucoup plus facile et [méthodes recommandées pour données d’Application Insights toodisplay dans Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="ff92e-199">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="ff92e-200">Hello chemin illustrée ici est simplement un tooillustrate exemple tooprocess comment les données exportées.</span><span class="sxs-lookup"><span data-stu-id="ff92e-200">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

<span data-ttu-id="ff92e-201">Ouvrez Power BI avec votre travail ou le compte scolaire et la hello sélectionnez le jeu de données et la table que vous avez défini en tant que sortie hello de tâche de flux de données Analytique hello.</span><span class="sxs-lookup"><span data-stu-id="ff92e-201">Open Power BI with your work or school account, and select hello dataset and table that you defined as hello output of hello Stream Analytics job.</span></span>

![Dans Power BI, sélectionnez votre dataset et vos champs.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="ff92e-203">Vous pouvez maintenant utiliser ce jeu de données dans des rapports et des tableaux de bord dans [Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ff92e-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![Dans Power BI, sélectionnez votre dataset et vos champs.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="ff92e-205">Pas de données ?</span><span class="sxs-lookup"><span data-stu-id="ff92e-205">No data?</span></span>
* <span data-ttu-id="ff92e-206">Vérifiez que vous avez [format de date set hello](#set-path-prefix-pattern) correctement tooYYYY-MM-JJ (avec les tirets).</span><span class="sxs-lookup"><span data-stu-id="ff92e-206">Check that you [set hello date format](#set-path-prefix-pattern) correctly tooYYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="ff92e-207">Vidéo</span><span class="sxs-lookup"><span data-stu-id="ff92e-207">Video</span></span>
<span data-ttu-id="ff92e-208">Noam Ben Zeev montre le mode d’exportation des données à l’aide de flux de données Analytique tooprocess.</span><span class="sxs-lookup"><span data-stu-id="ff92e-208">Noam Ben Zeev shows how tooprocess exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ff92e-209">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ff92e-209">Next steps</span></span>
* [<span data-ttu-id="ff92e-210">Exportation continue</span><span class="sxs-lookup"><span data-stu-id="ff92e-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="ff92e-211">Informations de référence pour les types de propriété hello et les valeurs de modèle de données détaillées.</span><span class="sxs-lookup"><span data-stu-id="ff92e-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="ff92e-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="ff92e-212">Application Insights</span></span>](app-insights-overview.md)

