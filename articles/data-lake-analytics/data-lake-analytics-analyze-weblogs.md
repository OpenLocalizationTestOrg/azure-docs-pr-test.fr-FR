---
title: "les journaux du site Web aaaAnalyze à l’aide d’Analytique de LAC de données Azure | Documents Microsoft"
description: "Découvrez comment tooanalyze site connecte à l’aide des données de LAC Analytique. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: d27aaca95ed2b643cfed7a17b0066bf7fa4a1bf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="15616-103">Analyser les journaux des sites web à l’aide d’Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="15616-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="15616-104">Découvrez comment tooanalyze journaux de site Web à l’aide d’Analytique de LAC de données, en particulier sur découvrir les points d’accès s’est produite erreurs quand il a tenté de site Web de toovisit hello.</span><span class="sxs-lookup"><span data-stu-id="15616-104">Learn how tooanalyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried toovisit hello website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15616-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="15616-105">Prerequisites</span></span>
* <span data-ttu-id="15616-106">**Visual Studio 2015 ou Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="15616-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="15616-107">**[Data Lake Tools pour Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="15616-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="15616-108">Une fois que Data Lake Tools pour Visual Studio est installé, vous verrez un **Data Lake** élément Bonjour **outils** menu dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="15616-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in hello **Tools** menu in Visual Studio:</span></span>

    ![Menu U-SQL Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="15616-110">**Connaissances de base de données de LAC Analytique et hello Data Lake Tools pour Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="15616-110">**Basic knowledge of Data Lake Analytics and hello Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="15616-111">tooget démarré, consultez :</span><span class="sxs-lookup"><span data-stu-id="15616-111">tooget started, see:</span></span>

  * <span data-ttu-id="15616-112">[Développer des scripts U-SQL à l'aide des Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="15616-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="15616-113">**Un compte Data Lake Analytics.**</span><span class="sxs-lookup"><span data-stu-id="15616-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="15616-114">Consultez [Créer un compte Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15616-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="15616-115">**Téléchargez le compte de hello exemple données toohello Analytique lac de données.**</span><span class="sxs-lookup"><span data-stu-id="15616-115">**Upload hello sample data toohello Data Lake Analytics account.**</span></span> <span data-ttu-id="15616-116">Consultez [toocopy des fichiers de données](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15616-116">See [toocopy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="15616-117">toorun une tâche Analytique lac de données, vous aurez besoin de certaines données.</span><span class="sxs-lookup"><span data-stu-id="15616-117">toorun a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="15616-118">Bien que hello Data Lake Tools prend en charge le téléchargement de données, vous allez utiliser toomake de données exemple hello tooupload portail hello ce didacticiel toofollow plus facile.</span><span class="sxs-lookup"><span data-stu-id="15616-118">Even though hello Data Lake Tools supports uploading data, you will use hello portal tooupload hello sample data toomake this tutorial easier toofollow.</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="15616-119">Se connecter tooAzure</span><span class="sxs-lookup"><span data-stu-id="15616-119">Connect tooAzure</span></span>
<span data-ttu-id="15616-120">Avant de pouvoir générer et tester des scripts U-SQL, vous devez d’abord connecter tooAzure.</span><span class="sxs-lookup"><span data-stu-id="15616-120">Before you can build and test any U-SQL scripts, you must first connect tooAzure.</span></span>

<span data-ttu-id="15616-121">**tooconnect tooData Lake Analytique**</span><span class="sxs-lookup"><span data-stu-id="15616-121">**tooconnect tooData Lake Analytics**</span></span>

1. <span data-ttu-id="15616-122">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15616-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="15616-123">Cliquez sur **Data Lake > Options et paramètres**.</span><span class="sxs-lookup"><span data-stu-id="15616-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="15616-124">Cliquez sur **connexion**, ou **changer d’utilisateur** si quelqu'un s’est connecté et suivez les instructions de hello.</span><span class="sxs-lookup"><span data-stu-id="15616-124">Click **Sign In**, or **Change User** if someone has signed in, and follow hello instructions.</span></span>
4. <span data-ttu-id="15616-125">Cliquez sur **OK** boîte de dialogue tooclose hello Options et paramètres.</span><span class="sxs-lookup"><span data-stu-id="15616-125">Click **OK** tooclose hello Options and Settings dialog.</span></span>

<span data-ttu-id="15616-126">**toobrowse vos comptes Analytique lac de données**</span><span class="sxs-lookup"><span data-stu-id="15616-126">**toobrowse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="15616-127">Dans Visual Studio, ouvrez **l’Explorateur de serveurs** en appuyant sur **CTRL+ALT+S**.</span><span class="sxs-lookup"><span data-stu-id="15616-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="15616-128">Dans l’**Explorateur de serveurs**, développez **Azure**, puis **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="15616-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="15616-129">Le cas échéant, la liste de vos comptes Data Lake Analytics s'affiche.</span><span class="sxs-lookup"><span data-stu-id="15616-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="15616-130">Impossible de créer des comptes d’Analytique lac de données à partir de studio de hello.</span><span class="sxs-lookup"><span data-stu-id="15616-130">You cannot create Data Lake Analytics accounts from hello studio.</span></span> <span data-ttu-id="15616-131">toocreate un compte, consultez [prise en main Analytique de LAC de données Azure à l’aide du portail Azure](data-lake-analytics-get-started-portal.md) ou [prise en main Analytique de LAC de données Azure à l’aide d’Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="15616-131">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="15616-132">Développement d'application U-SQL</span><span class="sxs-lookup"><span data-stu-id="15616-132">Develop U-SQL application</span></span>
<span data-ttu-id="15616-133">Une application U-SQL est essentiellement un script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="15616-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="15616-134">toolearn en savoir plus sur U-SQL, consultez [prise en main U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="15616-134">toolearn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="15616-135">Vous pouvez ajouter l’application de toohello Ajout opérateurs définis par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="15616-135">You can add addition user-defined operators toohello application.</span></span>  <span data-ttu-id="15616-136">Pour plus d'informations, consultez [Développer des opérateurs définis par l'utilisateur U-SQL pour des travaux Data Lake Analytics](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="15616-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="15616-137">**toocreate et soumettez une tâche Analytique lac de données**</span><span class="sxs-lookup"><span data-stu-id="15616-137">**toocreate and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="15616-138">Cliquez sur hello **fichier > Nouveau > projet**.</span><span class="sxs-lookup"><span data-stu-id="15616-138">Click hello **File > New > Project**.</span></span>
2. <span data-ttu-id="15616-139">Sélectionnez le type de projet U-SQL hello.</span><span class="sxs-lookup"><span data-stu-id="15616-139">Select hello U-SQL Project type.</span></span>

    ![nouveau projet U-SQL Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="15616-141">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="15616-141">Click **OK**.</span></span> <span data-ttu-id="15616-142">Visual Studio crée une solution avec un fichier Script.usql.</span><span class="sxs-lookup"><span data-stu-id="15616-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="15616-143">Entrez hello script suivant dans le fichier de Script.usql hello :</span><span class="sxs-lookup"><span data-stu-id="15616-143">Enter hello following script into hello Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need tooread from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from hello weblog file with hello correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            DISTRIBUTED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    <span data-ttu-id="15616-144">toounderstand hello U-SQL, consultez [prise en main langage données Lake Analytique U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="15616-144">toounderstand hello U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="15616-145">Ajoutez un nouveau projet de tooyour script U-SQL et tapez Bonjour suivante :</span><span class="sxs-lookup"><span data-stu-id="15616-145">Add a new U-SQL script tooyour project and enter hello following:</span></span>

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="15616-146">Basculer le script U-SQL de la première toohello précédent et suivant toohello **envoyer** et spécifier votre compte Analytique.</span><span class="sxs-lookup"><span data-stu-id="15616-146">Switch back toohello first U-SQL script and next toohello **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="15616-147">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur **Script.usql**, puis cliquez sur **Générer le script**.</span><span class="sxs-lookup"><span data-stu-id="15616-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="15616-148">Vérifier les résultats de hello dans le volet de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="15616-148">Verify hello results in hello Output pane.</span></span>
8. <span data-ttu-id="15616-149">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur **Script.usql**, puis cliquez sur **Soumettre le script**.</span><span class="sxs-lookup"><span data-stu-id="15616-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="15616-150">Vérifiez que hello **Analytique compte** est hello une où vous voulez toorun hello travail, puis cliquez sur **Submit**.</span><span class="sxs-lookup"><span data-stu-id="15616-150">Verify hello **Analytics Account** is hello one where you want toorun hello job, and then click **Submit**.</span></span> <span data-ttu-id="15616-151">Résultats de l’envoi et de lien de tâche sont disponibles dans hello Data Lake Tools pour la fenêtre Résultats Visual Studio lors de la soumission de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="15616-151">Submission results and job link are available in hello Data Lake Tools for Visual Studio Results window when hello submission is completed.</span></span>
10. <span data-ttu-id="15616-152">Attendez que hello tâche terminée avec succès.</span><span class="sxs-lookup"><span data-stu-id="15616-152">Wait until hello job is completed successfully.</span></span>  <span data-ttu-id="15616-153">En cas d’échec de la tâche de hello, il est très probablement hello source fichier manquant.</span><span class="sxs-lookup"><span data-stu-id="15616-153">If hello job failed, it is most likely missing hello source file.</span></span>  <span data-ttu-id="15616-154">Consultez la section Configuration requise de hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="15616-154">Please see hello Prerequisite section of this tutorial.</span></span> <span data-ttu-id="15616-155">Pour plus d'informations de dépannage, consultez [Analyser et résoudre les problèmes des tâches Azure Data Lake Analytics](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="15616-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="15616-156">À la fin du travail hello, vous allez voir hello suivant d’écran :</span><span class="sxs-lookup"><span data-stu-id="15616-156">When hello job is completed, you shall see hello following screen:</span></span>

    ![data lake analytics analyser les journaux des sites web](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="15616-158">Répétez les étapes 7 à 10 pour **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="15616-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="15616-159">**sortie de tâche hello toosee**</span><span class="sxs-lookup"><span data-stu-id="15616-159">**toosee hello job output**</span></span>

1. <span data-ttu-id="15616-160">À partir de **l’Explorateur de serveurs**, développez **Azure**, développez **Analytique lac de données**, développez votre compte Analytique lac de données, puis **lescomptesdestockage**, cliquez sur le compte de stockage des données Lake hello par défaut, puis cliquez sur **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="15616-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="15616-161">Double-cliquez sur **exemples** tooopen hello du dossier, puis double-cliquez sur **sorties**.</span><span class="sxs-lookup"><span data-stu-id="15616-161">Double-click **Samples** tooopen hello folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="15616-162">Double-cliquez sur **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="15616-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="15616-163">Vous pouvez également double-cliquer sur hello fichier de sortie à l’intérieur de vue du graphique hello du travail hello dans l’ordre toonavigate directement toohello de sortie.</span><span class="sxs-lookup"><span data-stu-id="15616-163">You can also double-click hello output file inside hello graph view of hello job in order toonavigate directly toohello output.</span></span>

## <a name="see-also"></a><span data-ttu-id="15616-164">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="15616-164">See also</span></span>
<span data-ttu-id="15616-165">tooget main Analytique lac de données à l’aide de différents outils, consultez :</span><span class="sxs-lookup"><span data-stu-id="15616-165">tooget started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="15616-166">Prendre en main Data Lake Analytics à l'aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="15616-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="15616-167">Prise en main de Data Lake Analytics à l'aide d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="15616-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="15616-168">Prise en main de Data Lake Analytics à l'aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="15616-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
