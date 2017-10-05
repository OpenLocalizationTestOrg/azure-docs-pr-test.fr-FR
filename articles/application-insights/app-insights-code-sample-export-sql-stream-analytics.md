---
title: "Exporter vers SQL à partir d’Application Insights | Microsoft Docs"
description: "Exportez de façon continue les données Application Insights vers SQL à l’aide de Stream Analytics."
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
ms.openlocfilehash: d51e80509ffb63cef0d01133a2295d58757d5b1a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-export-to-sql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="cdefb-103">Procédure pas à pas : exporter vers SQL à partir d’Application Insights à l’aide de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cdefb-103">Walkthrough: Export to SQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="cdefb-104">Cet article explique comment déplacer vos données de télémétrie à partir d’[Azure Application Insights][start] vers une base de données SQL Azure à l’aide de l’[Exportation continue][export] et d’[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="cdefb-104">This article shows how to move your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="cdefb-105">L’exportation continue déplace vos données de télémétrie vers le stockage Azure au format JSON.</span><span class="sxs-lookup"><span data-stu-id="cdefb-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="cdefb-106">Nous analyserons les objets JSON à l’aide d’Azure Stream Analytics et créerons des lignes dans une table de base de données.</span><span class="sxs-lookup"><span data-stu-id="cdefb-106">We'll parse the JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="cdefb-107">(Plus généralement, l’exportation continue est la méthode qui vous permet de réaliser votre propre analyse des données de télémétrie que vos applications transmettent à Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cdefb-107">(More generally, Continuous Export is the way to do your own analysis of the telemetry your apps send to Application Insights.</span></span> <span data-ttu-id="cdefb-108">Vous pourriez adapter cet exemple de code pour effectuer d’autres actions à l’aide des données de télémétrie exportées, comme agréger les données.)</span><span class="sxs-lookup"><span data-stu-id="cdefb-108">You could adapt this code sample to do other things with the exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="cdefb-109">Nous allons partir du principe que vous disposez déjà de l’application que vous voulez analyser.</span><span class="sxs-lookup"><span data-stu-id="cdefb-109">We'll start with the assumption that you already have the app you want to monitor.</span></span>

<span data-ttu-id="cdefb-110">Dans cet exemple, nous allons utiliser les données d’affichage de page. Toutefois, le même modèle peut facilement être étendu à d’autres types de données, tels que des événements et des exceptions personnalisés.</span><span class="sxs-lookup"><span data-stu-id="cdefb-110">In this example, we will be using the page view data, but the same pattern can easily be extended to other data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-to-your-application"></a><span data-ttu-id="cdefb-111">Ajouter Application Insights à votre application</span><span class="sxs-lookup"><span data-stu-id="cdefb-111">Add Application Insights to your application</span></span>
<span data-ttu-id="cdefb-112">Pour commencer :</span><span class="sxs-lookup"><span data-stu-id="cdefb-112">To get started:</span></span>

1. <span data-ttu-id="cdefb-113">[Configurer Application Insights pour vos pages web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="cdefb-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="cdefb-114">(Dans cet exemple, nous allons nous concentrer sur le traitement des données d’affichage de page dans les navigateurs clients, mais vous pouvez également configurer Application Insights pour le côté serveur de votre application [Java](app-insights-java-get-started.md) ou [ASP.NET](app-insights-asp-net.md) et traiter la demande, les dépendances et d’autres données de télémétrie du serveur.)</span><span class="sxs-lookup"><span data-stu-id="cdefb-114">(In this example, we'll focus on processing page view data from the client browsers, but you could also set up Application Insights for the server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="cdefb-115">Publiez votre application et surveillez les données de télémétrie apparaissant dans votre ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cdefb-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="cdefb-116">Création d’un stockage dans Azure</span><span class="sxs-lookup"><span data-stu-id="cdefb-116">Create storage in Azure</span></span>
<span data-ttu-id="cdefb-117">Comme l’exportation continue génère toujours des données vers un compte de stockage Azure, vous devez commencer par créer ce stockage.</span><span class="sxs-lookup"><span data-stu-id="cdefb-117">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="cdefb-118">Créez un compte de stockage dans votre abonnement sur le [portail Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="cdefb-118">Create a storage account in your subscription in the [Azure portal][portal].</span></span>
   
    ![Sur le portail Azure, choisissez Nouveau, Données, Stockage.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="cdefb-122">Créez un conteneur.</span><span class="sxs-lookup"><span data-stu-id="cdefb-122">Create a container</span></span>
   
    ![Dans le nouvel emplacement de stockage, sélectionnez Conteneurs, cliquez sur la mosaïque Conteneurs puis sur Ajouter.](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="cdefb-124">Copiez la clé d’accès au stockage.</span><span class="sxs-lookup"><span data-stu-id="cdefb-124">Copy the storage access key</span></span>
   
    <span data-ttu-id="cdefb-125">Vous en aurez bientôt besoin pour configurer l’entrée dans le service Stream analytics.</span><span class="sxs-lookup"><span data-stu-id="cdefb-125">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![Dans le stockage, ouvrez Paramètres, Clés et copiez la clé d’accès principale.](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="cdefb-127">Démarrer l’exportation continue vers le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="cdefb-127">Start continuous export to Azure storage</span></span>
1. <span data-ttu-id="cdefb-128">Sur le portail Azure, accédez à la ressource Application Insights que vous avez créée pour votre application.</span><span class="sxs-lookup"><span data-stu-id="cdefb-128">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Sélectionnez Parcourir, Application Insights, puis votre application.](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="cdefb-130">Créez une exportation continue.</span><span class="sxs-lookup"><span data-stu-id="cdefb-130">Create a continuous export.</span></span>
   
    ![Choisissez Paramètres, Exportation continue, Ajouter.](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="cdefb-132">Sélectionnez le compte de stockage que vous avez préalablement créé.</span><span class="sxs-lookup"><span data-stu-id="cdefb-132">Select the storage account you created earlier:</span></span>

    ![Définissez la destination de l’exportation.](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="cdefb-134">Définissez les types d’événements que vous souhaitez afficher :</span><span class="sxs-lookup"><span data-stu-id="cdefb-134">Set the event types you want to see:</span></span>

    ![Choisissez les types d’événements.](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="cdefb-136">Laissez les données s'accumuler.</span><span class="sxs-lookup"><span data-stu-id="cdefb-136">Let some data accumulate.</span></span> <span data-ttu-id="cdefb-137">Installez-vous confortablement et laissez les utilisateurs utiliser votre application pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="cdefb-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="cdefb-138">Les données de télémétrie vont vous être transmises et vous permettre d’afficher des graphiques statistiques dans [Metrics explorer](app-insights-metrics-explorer.md) et des événements dans [Recherche de diagnostic](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="cdefb-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="cdefb-139">Les données seront également exportées vers votre stockage.</span><span class="sxs-lookup"><span data-stu-id="cdefb-139">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="cdefb-140">Inspectez les données exportées, soit dans le portail (choisissez **Parcourir**, sélectionnez votre compte de stockage, puis **Conteneurs**), soit dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cdefb-140">Inspect the exported data, either in the portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="cdefb-141">Dans Visual Studio, sélectionnez **Afficher / Cloud Explorer**, puis ouvrez Azure / Stockage.</span><span class="sxs-lookup"><span data-stu-id="cdefb-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="cdefb-142">(Si vous n'avez pas cette option, vous devez installer le SDK Azure : Ouvrez la boîte de dialogue Nouveau projet et ouvrez Visual C# / Cloud / Obtenir Microsoft Azure SDK pour .NET.)</span><span class="sxs-lookup"><span data-stu-id="cdefb-142">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![Dans Visual Studio, ouvrez Explorateur de serveurs, Azure, Stockage](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="cdefb-144">Prenez note de la partie commune du nom du chemin d'accès, qui est dérivée du nom de l'application et de la clé d'instrumentation.</span><span class="sxs-lookup"><span data-stu-id="cdefb-144">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="cdefb-145">Les événements sont écrits dans des fichiers blob au format JSON.</span><span class="sxs-lookup"><span data-stu-id="cdefb-145">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="cdefb-146">Chaque fichier peut contenir un ou plusieurs événements.</span><span class="sxs-lookup"><span data-stu-id="cdefb-146">Each file may contain one or more events.</span></span> <span data-ttu-id="cdefb-147">Donc, nous devons lire les données d’événement et filtrer les champs voulus.</span><span class="sxs-lookup"><span data-stu-id="cdefb-147">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="cdefb-148">Nous pourrions effectuer toutes sortes d’opérations avec les données, mais notre objectif aujourd’hui est d’utiliser Stream Analytics pour déplacer les données vers une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="cdefb-148">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to move the data to a SQL database.</span></span> <span data-ttu-id="cdefb-149">Cette action va simplifier l’exécution d’un grand nombre de requêtes intéressantes.</span><span class="sxs-lookup"><span data-stu-id="cdefb-149">That will make it easy to run lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="cdefb-150">Création d’une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="cdefb-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="cdefb-151">Là encore, à partir de votre abonnement dans le [portail Azure][portal], créez la base de données (et un serveur si ce n’est déjà fait) dans laquelle vous allez écrire les données.</span><span class="sxs-lookup"><span data-stu-id="cdefb-151">Once again starting from your subscription in [Azure portal][portal], create the database (and a new server, unless you've already got one) to which you'll write the data.</span></span>

![Nouveau, Données, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="cdefb-153">Assurez-vous que le serveur de base de données permet d’accéder aux services Azure :</span><span class="sxs-lookup"><span data-stu-id="cdefb-153">Make sure that the database server allows access to Azure services:</span></span>

![Parcourir, Serveurs, votre serveur, Paramètres, Pare-feu, Autoriser l’accès à Azure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="cdefb-155">Créer une table dans la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="cdefb-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="cdefb-156">Connectez-vous à la base de données créée dans la section précédente à l’aide de votre outil de gestion préféré.</span><span class="sxs-lookup"><span data-stu-id="cdefb-156">Connect to the database created in the previous section with your preferred management tool.</span></span> <span data-ttu-id="cdefb-157">Dans cette procédure pas à pas, nous utiliserons [Outils d’administration SQL Server](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="cdefb-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="cdefb-158">Créez une nouvelle requête et exécutez le T-SQL suivant :</span><span class="sxs-lookup"><span data-stu-id="cdefb-158">Create a new query, and execute the following T-SQL:</span></span>

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

<span data-ttu-id="cdefb-159">Dans cet exemple, nous utilisons les données issues des affichages de pages.</span><span class="sxs-lookup"><span data-stu-id="cdefb-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="cdefb-160">Pour voir les autres données disponibles, examinez la sortie JSON et consultez le [modèle d’exportation de données](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="cdefb-160">To see the other data available, inspect your JSON output, and see the [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="cdefb-161">Création d’une instance Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cdefb-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="cdefb-162">À partir du [portail classique Azure](https://manage.windowsazure.com/), sélectionnez le service Azure Stream Analytics et créez une nouvelle tâche Stream Analytics :</span><span class="sxs-lookup"><span data-stu-id="cdefb-162">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="cdefb-163">Une fois la tâche créée, développez les informations qui s’y rapportent :</span><span class="sxs-lookup"><span data-stu-id="cdefb-163">When the new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="cdefb-164">Définition de l’emplacement des objets blob</span><span class="sxs-lookup"><span data-stu-id="cdefb-164">Set blob location</span></span>
<span data-ttu-id="cdefb-165">Définissez-le pour qu’il tienne compte des données de votre objet blob d’exportation continue :</span><span class="sxs-lookup"><span data-stu-id="cdefb-165">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="cdefb-166">Vous devez maintenant disposer de la clé d’accès principale issue de votre compte de stockage, que vous avez notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="cdefb-166">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="cdefb-167">Définissez-la comme clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="cdefb-167">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="cdefb-168">Définition de la séquence d’octets préfixe du chemin d’accès</span><span class="sxs-lookup"><span data-stu-id="cdefb-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="cdefb-169">Veillez à définir le format de date sur **AAAA-MM-JJ** (avec des **tirets**).</span><span class="sxs-lookup"><span data-stu-id="cdefb-169">Be sure to set the Date Format to **YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="cdefb-170">La séquence d’octets préfixe du chemin d’accès spécifie la manière dont Stream Analytics recherche les fichiers d’entrée dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="cdefb-170">The Path Prefix Pattern specifies how Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="cdefb-171">Vous devez la configurer pour correspondre au mode de stockage des données de l'exportation continue.</span><span class="sxs-lookup"><span data-stu-id="cdefb-171">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="cdefb-172">Définissez-la comme suit :</span><span class="sxs-lookup"><span data-stu-id="cdefb-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="cdefb-173">Dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="cdefb-173">In this example:</span></span>

* <span data-ttu-id="cdefb-174">`webapplication27` est le nom de la ressource Application Insights, **tout en minuscules**.</span><span class="sxs-lookup"><span data-stu-id="cdefb-174">`webapplication27` is the name of the Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="cdefb-175">`1234...` est la clé d’instrumentation de la ressource Application Insights **avec les tirets supprimés**.</span><span class="sxs-lookup"><span data-stu-id="cdefb-175">`1234...` is the instrumentation key of the Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="cdefb-176">`PageViews` est le type de données que nous souhaitons analyser.</span><span class="sxs-lookup"><span data-stu-id="cdefb-176">`PageViews` is the type of data we want to analyze.</span></span> <span data-ttu-id="cdefb-177">Les types disponibles varient selon le filtre que vous définissez dans l’exportation continue.</span><span class="sxs-lookup"><span data-stu-id="cdefb-177">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="cdefb-178">Examinez les données exportées pour voir les autres types disponibles et consultez le [modèle d’exportation de données](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="cdefb-178">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="cdefb-179">`/{date}/{time}` est une séquence écrite de manière littérale.</span><span class="sxs-lookup"><span data-stu-id="cdefb-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="cdefb-180">Pour obtenir le nom et l’iKey de votre ressource Application Insights, ouvrez Essentials sur sa page de présentation ou ouvrez Paramètres.</span><span class="sxs-lookup"><span data-stu-id="cdefb-180">To get the name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="cdefb-181">Fin de l’installation initiale</span><span class="sxs-lookup"><span data-stu-id="cdefb-181">Finish initial setup</span></span>
<span data-ttu-id="cdefb-182">Confirmez le format de sérialisation :</span><span class="sxs-lookup"><span data-stu-id="cdefb-182">Confirm the serialization format:</span></span>

![Confirmez et fermez l’assistant.](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="cdefb-184">Fermez l’assistant et attendez la fin de l’installation.</span><span class="sxs-lookup"><span data-stu-id="cdefb-184">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="cdefb-185">Utilisez l’exemple de fonction pour vérifier que vous avez correctement défini le chemin d’accès d’entrée.</span><span class="sxs-lookup"><span data-stu-id="cdefb-185">Use the Sample function to check that you have set the input path correctly.</span></span> <span data-ttu-id="cdefb-186">En cas d’échec, vérifiez qu’il y a des données dans le stockage pour l’exemple de période que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="cdefb-186">If it fails: Check that there is data in the storage for the sample time range you chose.</span></span> <span data-ttu-id="cdefb-187">Modifiez la définition de l’entrée et vérifiez que vous avez correctement défini le compte de stockage, le préfixe de chemin d’accès et le format de date.</span><span class="sxs-lookup"><span data-stu-id="cdefb-187">Edit the input definition and check you set the storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="cdefb-188">Définition d’une requête</span><span class="sxs-lookup"><span data-stu-id="cdefb-188">Set query</span></span>
<span data-ttu-id="cdefb-189">Ouvrez la section de la requête :</span><span class="sxs-lookup"><span data-stu-id="cdefb-189">Open the query section:</span></span>

![Dans Stream analytics, sélectionnez Requête.](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="cdefb-191">Remplacez la requête par défaut par :</span><span class="sxs-lookup"><span data-stu-id="cdefb-191">Replace the default query with:</span></span>

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

<span data-ttu-id="cdefb-192">Notez que les premières propriétés sont spécifiques aux données d’affichage de page.</span><span class="sxs-lookup"><span data-stu-id="cdefb-192">Notice that the first few properties are specific to page view data.</span></span> <span data-ttu-id="cdefb-193">Les exportations d’autres types de télémétrie disposent de propriétés différentes.</span><span class="sxs-lookup"><span data-stu-id="cdefb-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="cdefb-194">Consultez la [référence de modèle de données détaillé pour les valeurs et types de propriétés.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="cdefb-194">See the [detailed data model reference for the property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-to-database"></a><span data-ttu-id="cdefb-195">Configuration de la sortie vers la base de données</span><span class="sxs-lookup"><span data-stu-id="cdefb-195">Set up output to database</span></span>
<span data-ttu-id="cdefb-196">Sélectionnez SQL comme sortie.</span><span class="sxs-lookup"><span data-stu-id="cdefb-196">Select SQL as the output.</span></span>

![Dans Stream analytics, sélectionnez Sorties.](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="cdefb-198">Spécifiez la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="cdefb-198">Specify the SQL database.</span></span>

![Remplissez les détails de votre base de données.](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="cdefb-200">Fermez l’assistant et attendez une notification indiquant que la sortie a été configurée.</span><span class="sxs-lookup"><span data-stu-id="cdefb-200">Close the wizard and wait for a notification that the output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="cdefb-201">Démarrage du traitement</span><span class="sxs-lookup"><span data-stu-id="cdefb-201">Start processing</span></span>
<span data-ttu-id="cdefb-202">Démarrez la tâche à partir de la barre d’action :</span><span class="sxs-lookup"><span data-stu-id="cdefb-202">Start the job from the action bar:</span></span>

![Dans Stream Analytics, cliquez sur Démarrer.](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="cdefb-204">Vous pouvez choisir de démarrer le traitement à partir de données actuelles ou de données antérieures.</span><span class="sxs-lookup"><span data-stu-id="cdefb-204">You can choose whether to start processing the data starting from now, or to start with earlier data.</span></span> <span data-ttu-id="cdefb-205">La dernière possibilité est utile si l’exportation continue fonctionne déjà depuis un certain temps.</span><span class="sxs-lookup"><span data-stu-id="cdefb-205">The latter is useful if you have had Continuous Export already running for a while.</span></span>

![Dans Stream Analytics, cliquez sur Démarrer.](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="cdefb-207">Après quelques minutes, revenez aux Outils d’administration SQL Server et observez les données qui y circulent.</span><span class="sxs-lookup"><span data-stu-id="cdefb-207">After a few minutes, go back to SQL Server Management Tools and watch the data flowing in.</span></span> <span data-ttu-id="cdefb-208">Utilisez, par exemple, le type de requête suivant :</span><span class="sxs-lookup"><span data-stu-id="cdefb-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="cdefb-209">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="cdefb-209">Related articles</span></span>
* [<span data-ttu-id="cdefb-210">Exporter vers PowerBI à l’aide de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="cdefb-210">Export to PowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="cdefb-211">Référence de modèle de données détaillé pour les valeurs et types de propriétés.</span><span class="sxs-lookup"><span data-stu-id="cdefb-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="cdefb-212">Exportation continue dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="cdefb-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="cdefb-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="cdefb-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

