---
title: "Exporter tooSQL à partir de l’Application Azure Insights | Documents Microsoft"
description: "En continu exporter tooSQL de données d’Application Insights à l’aide de flux de données Analytique."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="91156-103">Procédure pas à pas : Exportation tooSQL à partir de l’Application Insights à l’aide de flux de données Analytique</span><span class="sxs-lookup"><span data-stu-id="91156-103">Walkthrough: Export tooSQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="91156-104">Cet article explique comment toomove vos données de télémétrie de [Azure Application Insights] [ start] dans une base de données SQL Azure à l’aide de [de l’exportation continue] [ export] et [Azure Stream Analytique](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="91156-104">This article shows how toomove your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="91156-105">L’exportation continue déplace vos données de télémétrie vers le stockage Azure au format JSON.</span><span class="sxs-lookup"><span data-stu-id="91156-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="91156-106">Nous analyser hello des objets JSON à l’aide d’Analytique de flux de données Azure et créer des lignes dans une table de base de données.</span><span class="sxs-lookup"><span data-stu-id="91156-106">We'll parse hello JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="91156-107">(Plus généralement, l’exportation continue est hello moyen toodo votre propre analyse des données de télémétrie hello tooApplication Insights d’envoi de vos applications.</span><span class="sxs-lookup"><span data-stu-id="91156-107">(More generally, Continuous Export is hello way toodo your own analysis of hello telemetry your apps send tooApplication Insights.</span></span> <span data-ttu-id="91156-108">Vous pourriez adapter cette toodo exemple de code autres choses avec les données de télémétrie hello exportée, telles que l’agrégation de données.)</span><span class="sxs-lookup"><span data-stu-id="91156-108">You could adapt this code sample toodo other things with hello exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="91156-109">Nous allons commencer par hypothèse hello que vous avez déjà application hello toomonitor.</span><span class="sxs-lookup"><span data-stu-id="91156-109">We'll start with hello assumption that you already have hello app you want toomonitor.</span></span>

<span data-ttu-id="91156-110">Dans cet exemple, nous allons utiliser des données d’affichage page hello, mais hello même modèle peut facilement être étendu tooother des types de données tels que les événements personnalisés et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="91156-110">In this example, we will be using hello page view data, but hello same pattern can easily be extended tooother data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-tooyour-application"></a><span data-ttu-id="91156-111">Ajouter Application Insights tooyour application</span><span class="sxs-lookup"><span data-stu-id="91156-111">Add Application Insights tooyour application</span></span>
<span data-ttu-id="91156-112">tooget démarré :</span><span class="sxs-lookup"><span data-stu-id="91156-112">tooget started:</span></span>

1. <span data-ttu-id="91156-113">[Configurer Application Insights pour vos pages web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="91156-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="91156-114">(Dans cet exemple, nous allons nous concentrer sur le traitement des données d’affichage de page dans les navigateurs clients hello, mais vous pouvez également configurer Application Insights pour côté serveur hello votre [Java](app-insights-java-get-started.md) ou [ASP.NET](app-insights-asp-net.md) application et le processus de demande dépendances et autres données de télémétrie du serveur.)</span><span class="sxs-lookup"><span data-stu-id="91156-114">(In this example, we'll focus on processing page view data from hello client browsers, but you could also set up Application Insights for hello server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="91156-115">Publiez votre application et surveillez les données de télémétrie apparaissant dans votre ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="91156-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="91156-116">Création d’un stockage dans Azure</span><span class="sxs-lookup"><span data-stu-id="91156-116">Create storage in Azure</span></span>
<span data-ttu-id="91156-117">Exportation continue retourne toujours le compte de stockage Azure données tooan, donc vous devez tout d’abord le stockage de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="91156-117">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="91156-118">Créer un compte de stockage dans votre abonnement Bonjour [portail Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="91156-118">Create a storage account in your subscription in hello [Azure portal][portal].</span></span>
   
    ![Sur le portail Azure, choisissez Nouveau, Données, Stockage.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="91156-122">Créez un conteneur.</span><span class="sxs-lookup"><span data-stu-id="91156-122">Create a container</span></span>
   
    ![Dans un nouveau stockage hello, sélectionnez les conteneurs, cliquez sur la vignette de conteneurs hello, puis sur Ajouter](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="91156-124">Copiez la clé d’accès de stockage de hello</span><span class="sxs-lookup"><span data-stu-id="91156-124">Copy hello storage access key</span></span>
   
    <span data-ttu-id="91156-125">Vous en aurez besoin dès tooset hello toohello d’entrée flux analytique service.</span><span class="sxs-lookup"><span data-stu-id="91156-125">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![Dans le stockage de hello, ouvrez les paramètres, clés et effectuer une copie de hello clé d’accès primaire](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="91156-127">Démarrer l’exportation continue tooAzure stockage</span><span class="sxs-lookup"><span data-stu-id="91156-127">Start continuous export tooAzure storage</span></span>
1. <span data-ttu-id="91156-128">Bonjour portail Azure, parcourir les ressources d’Application Insights toohello que vous avez créé pour votre application.</span><span class="sxs-lookup"><span data-stu-id="91156-128">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Sélectionnez Parcourir, Application Insights, puis votre application.](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="91156-130">Créez une exportation continue.</span><span class="sxs-lookup"><span data-stu-id="91156-130">Create a continuous export.</span></span>
   
    ![Choisissez Paramètres, Exportation continue, Ajouter.](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="91156-132">Sélectionnez le compte de stockage hello que vous avez créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="91156-132">Select hello storage account you created earlier:</span></span>

    ![Définir la destination de l’exportation hello](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="91156-134">Définir les types d’événement hello toosee :</span><span class="sxs-lookup"><span data-stu-id="91156-134">Set hello event types you want toosee:</span></span>

    ![Choisissez les types d’événements.](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="91156-136">Laissez les données s'accumuler.</span><span class="sxs-lookup"><span data-stu-id="91156-136">Let some data accumulate.</span></span> <span data-ttu-id="91156-137">Installez-vous confortablement et laissez les utilisateurs utiliser votre application pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="91156-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="91156-138">Les données de télémétrie vont vous être transmises et vous permettre d’afficher des graphiques statistiques dans [Metrics explorer](app-insights-metrics-explorer.md) et des événements dans [Recherche de diagnostic](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="91156-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="91156-139">Et, en outre, les données de salutation exportera tooyour stockage.</span><span class="sxs-lookup"><span data-stu-id="91156-139">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="91156-140">Inspecter les données hello exportée, soit dans le portail de hello - choisir **Parcourir**, sélectionnez votre compte de stockage, puis **conteneurs** - ou dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="91156-140">Inspect hello exported data, either in hello portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="91156-141">Dans Visual Studio, sélectionnez **Afficher / Cloud Explorer**, puis ouvrez Azure / Stockage.</span><span class="sxs-lookup"><span data-stu-id="91156-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="91156-142">(Si vous n’avez pas cette option de menu, vous devez tooinstall hello Azure SDK : ouvrir la boîte de dialogue Nouveau projet hello et ouvrez Visual C# / Cloud / obtenir Microsoft Azure SDK pour .NET.)</span><span class="sxs-lookup"><span data-stu-id="91156-142">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![Dans Visual Studio, ouvrez Explorateur de serveurs, Azure, Stockage](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="91156-144">Prenez note de la partie commune de hello du nom de chemin d’accès de hello, qui est dérivé de la clé de nom et d’instrumentation application hello.</span><span class="sxs-lookup"><span data-stu-id="91156-144">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="91156-145">événements de Hello sont écrits les fichiers de tooblob au format JSON.</span><span class="sxs-lookup"><span data-stu-id="91156-145">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="91156-146">Chaque fichier peut contenir un ou plusieurs événements.</span><span class="sxs-lookup"><span data-stu-id="91156-146">Each file may contain one or more events.</span></span> <span data-ttu-id="91156-147">Par conséquent, nous souhaitons les données d’événement tooread hello et filtrer les champs hello.</span><span class="sxs-lookup"><span data-stu-id="91156-147">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="91156-148">Il existe toutes sortes de choses que nous pouvons faire avec les données de hello, mais notre plan aujourd'hui est toouse flux Analytique toomove hello données tooa base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="91156-148">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toomove hello data tooa SQL database.</span></span> <span data-ttu-id="91156-149">Qui rend un grand nombre de toorun facile de requêtes intéressantes.</span><span class="sxs-lookup"><span data-stu-id="91156-149">That will make it easy toorun lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="91156-150">Création d’une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="91156-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="91156-151">À nouveau à partir de votre abonnement dans [portail Azure][portal], créer la base de données hello (et un nouveau serveur, sauf si vous avez déjà une) toowhich, vous allez écrire les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="91156-151">Once again starting from your subscription in [Azure portal][portal], create hello database (and a new server, unless you've already got one) toowhich you'll write hello data.</span></span>

![Nouveau, Données, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="91156-153">Assurez-vous que ce serveur de base de données hello autorise l’accès tooAzure services :</span><span class="sxs-lookup"><span data-stu-id="91156-153">Make sure that hello database server allows access tooAzure services:</span></span>

![Parcourir, des serveurs, votre serveur, les paramètres, les pare-feu, autoriser l’accès à tooAzure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="91156-155">Créer une table dans la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="91156-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="91156-156">Se connecter toohello de base de données créée dans la section précédente, hello à votre outil de gestion préférés.</span><span class="sxs-lookup"><span data-stu-id="91156-156">Connect toohello database created in hello previous section with your preferred management tool.</span></span> <span data-ttu-id="91156-157">Dans cette procédure pas à pas, nous utiliserons [Outils d’administration SQL Server](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="91156-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="91156-158">Créer une requête et exécutez hello T-SQL suivant :</span><span class="sxs-lookup"><span data-stu-id="91156-158">Create a new query, and execute hello following T-SQL:</span></span>

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

<span data-ttu-id="91156-159">Dans cet exemple, nous utilisons les données issues des affichages de pages.</span><span class="sxs-lookup"><span data-stu-id="91156-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="91156-160">toosee hello d’autres données disponibles, examinez la sortie JSON et voir hello [exporter le modèle de données](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="91156-160">toosee hello other data available, inspect your JSON output, and see hello [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="91156-161">Création d’une instance Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="91156-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="91156-162">À partir de hello [portail Azure Classic](https://manage.windowsazure.com/), sélectionnez le service d’Analytique de flux de données Azure hello et créer une nouvelle tâche de flux de données Analytique :</span><span class="sxs-lookup"><span data-stu-id="91156-162">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="91156-163">Lors de la création de tâche hello, développer ses détails :</span><span class="sxs-lookup"><span data-stu-id="91156-163">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="91156-164">Définition de l’emplacement des objets blob</span><span class="sxs-lookup"><span data-stu-id="91156-164">Set blob location</span></span>
<span data-ttu-id="91156-165">Définissez-le entrée tootake à partir de votre objet blob de l’exportation continue :</span><span class="sxs-lookup"><span data-stu-id="91156-165">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="91156-166">Vous devez maintenant hello clé d’accès primaire à partir de votre compte de stockage que vous avez notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="91156-166">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="91156-167">Définir en tant que clé de compte de stockage de hello.</span><span class="sxs-lookup"><span data-stu-id="91156-167">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="91156-168">Définition de la séquence d’octets préfixe du chemin d’accès</span><span class="sxs-lookup"><span data-stu-id="91156-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="91156-169">Être hello tooset que Format de Date trop**AAAA-MM-jj** (avec **tirets**).</span><span class="sxs-lookup"><span data-stu-id="91156-169">Be sure tooset hello Date Format too**YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="91156-170">Hello modèle du préfixe de chemin d’accès spécifie comment Analytique de flux de données recherche les fichiers d’entrée hello dans le stockage hello.</span><span class="sxs-lookup"><span data-stu-id="91156-170">hello Path Prefix Pattern specifies how Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="91156-171">Vous devez tooset il toohow toocorrespond de l’exportation continue stocke les données de hello.</span><span class="sxs-lookup"><span data-stu-id="91156-171">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="91156-172">Définissez-la comme suit :</span><span class="sxs-lookup"><span data-stu-id="91156-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="91156-173">Dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="91156-173">In this example:</span></span>

* <span data-ttu-id="91156-174">`webapplication27`est le nom hello Hello ressource Application Insights, **tout en minuscules**.</span><span class="sxs-lookup"><span data-stu-id="91156-174">`webapplication27` is hello name of hello Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="91156-175">`1234...`est la clé d’instrumentation hello Hello ressource Application Insights **et tirets supprimés**.</span><span class="sxs-lookup"><span data-stu-id="91156-175">`1234...` is hello instrumentation key of hello Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="91156-176">`PageViews`est hello type de données, nous souhaitons tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="91156-176">`PageViews` is hello type of data we want tooanalyze.</span></span> <span data-ttu-id="91156-177">les types disponibles Hello dépendent de filtre hello que vous définissez dans l’exportation continue.</span><span class="sxs-lookup"><span data-stu-id="91156-177">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="91156-178">Examiner les autres types disponibles hello de toosee données exportées hello et consultez hello [exporter le modèle de données](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="91156-178">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="91156-179">`/{date}/{time}` est une séquence écrite de manière littérale.</span><span class="sxs-lookup"><span data-stu-id="91156-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="91156-180">nom de hello tooget iKey de votre ressource Application Insights, ouvrez Essentials dans sa page de présentation et ouvrir les paramètres.</span><span class="sxs-lookup"><span data-stu-id="91156-180">tooget hello name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="91156-181">Fin de l’installation initiale</span><span class="sxs-lookup"><span data-stu-id="91156-181">Finish initial setup</span></span>
<span data-ttu-id="91156-182">Vérifiez le format de sérialisation hello :</span><span class="sxs-lookup"><span data-stu-id="91156-182">Confirm hello serialization format:</span></span>

![Confirmez et fermez l’assistant.](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="91156-184">Fermez l’Assistant de hello et attendez hello le programme d’installation toocomplete.</span><span class="sxs-lookup"><span data-stu-id="91156-184">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="91156-185">Utilisez hello exemple fonction toocheck que vous avez défini un chemin d’accès d’entrée de hello correctement.</span><span class="sxs-lookup"><span data-stu-id="91156-185">Use hello Sample function toocheck that you have set hello input path correctly.</span></span> <span data-ttu-id="91156-186">En cas d’échec : Vérifiez qu’il existe des données dans le stockage hello pour la plage de temps exemple hello choisis.</span><span class="sxs-lookup"><span data-stu-id="91156-186">If it fails: Check that there is data in hello storage for hello sample time range you chose.</span></span> <span data-ttu-id="91156-187">Modifier la définition d’entrée de hello et définir le compte de stockage hello, préfixe de chemin d’accès et de format de date correctement.</span><span class="sxs-lookup"><span data-stu-id="91156-187">Edit hello input definition and check you set hello storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="91156-188">Définition d’une requête</span><span class="sxs-lookup"><span data-stu-id="91156-188">Set query</span></span>
<span data-ttu-id="91156-189">Ouvrez la section de requête hello :</span><span class="sxs-lookup"><span data-stu-id="91156-189">Open hello query section:</span></span>

![Dans Stream analytics, sélectionnez Requête.](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="91156-191">Remplacez la requête par défaut de hello avec :</span><span class="sxs-lookup"><span data-stu-id="91156-191">Replace hello default query with:</span></span>

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

<span data-ttu-id="91156-192">Notez que hello tout d’abord certaines propriétés sont spécifiques de toopage afficher les données.</span><span class="sxs-lookup"><span data-stu-id="91156-192">Notice that hello first few properties are specific toopage view data.</span></span> <span data-ttu-id="91156-193">Les exportations d’autres types de télémétrie disposent de propriétés différentes.</span><span class="sxs-lookup"><span data-stu-id="91156-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="91156-194">Consultez hello [détaillées de référence de modèle de données pour les valeurs et les types de propriété hello.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="91156-194">See hello [detailed data model reference for hello property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-toodatabase"></a><span data-ttu-id="91156-195">Configurer la sortie toodatabase</span><span class="sxs-lookup"><span data-stu-id="91156-195">Set up output toodatabase</span></span>
<span data-ttu-id="91156-196">Sélectionnez SQL en tant que sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="91156-196">Select SQL as hello output.</span></span>

![Dans Stream analytics, sélectionnez Sorties.](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="91156-198">Spécifiez la base de données SQL hello.</span><span class="sxs-lookup"><span data-stu-id="91156-198">Specify hello SQL database.</span></span>

![Renseignez les détails de hello de votre base de données](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="91156-200">Fermez l’Assistant de hello et attendre une notification de sortie de hello a été configuré.</span><span class="sxs-lookup"><span data-stu-id="91156-200">Close hello wizard and wait for a notification that hello output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="91156-201">Démarrage du traitement</span><span class="sxs-lookup"><span data-stu-id="91156-201">Start processing</span></span>
<span data-ttu-id="91156-202">Démarrer le travail de hello à partir de la barre d’action hello :</span><span class="sxs-lookup"><span data-stu-id="91156-202">Start hello job from hello action bar:</span></span>

![Dans Stream Analytics, cliquez sur Démarrer.](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="91156-204">Vous pouvez choisir si le traitement de toostart hello des données à partir de maintenant, ou toostart avec des données antérieures.</span><span class="sxs-lookup"><span data-stu-id="91156-204">You can choose whether toostart processing hello data starting from now, or toostart with earlier data.</span></span> <span data-ttu-id="91156-205">Hello ce dernier est utile si vous avez eu l’exportation continue déjà en cours d’exécution pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="91156-205">hello latter is useful if you have had Continuous Export already running for a while.</span></span>

![Dans Stream Analytics, cliquez sur Démarrer.](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="91156-207">Après quelques minutes, outils de gestion de serveur tooSQL revenir en arrière et regarder la hello données circulent dans.</span><span class="sxs-lookup"><span data-stu-id="91156-207">After a few minutes, go back tooSQL Server Management Tools and watch hello data flowing in.</span></span> <span data-ttu-id="91156-208">Utilisez, par exemple, le type de requête suivant :</span><span class="sxs-lookup"><span data-stu-id="91156-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="91156-209">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="91156-209">Related articles</span></span>
* [<span data-ttu-id="91156-210">TooPowerBI d’exportation à l’aide de flux de données Analytique</span><span class="sxs-lookup"><span data-stu-id="91156-210">Export tooPowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="91156-211">Informations de référence pour les types de propriété hello et les valeurs de modèle de données détaillées.</span><span class="sxs-lookup"><span data-stu-id="91156-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="91156-212">Exportation continue dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="91156-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="91156-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="91156-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

