---
title: "Analyser les journaux des sites web à l’aide d’Azure Data Lake Analytics | Microsoft Docs"
description: "Apprendre à analyser les journaux des sites web à l'aide de Data Lake Analytics. "
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
ms.openlocfilehash: 25fbbe97d26491fc421f4821315761c18e523ec8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="b3cd8-103">Analyser les journaux des sites web à l’aide d’Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b3cd8-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="b3cd8-104">Découvrez comment analyser les journaux des sites web à l'aide de Data Lake Analytics, en particulier pour découvrir quels points d'accès ont rencontré des erreurs lorsqu'ils ont essayé de visiter le site web.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-104">Learn how to analyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried to visit the website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3cd8-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b3cd8-105">Prerequisites</span></span>
* <span data-ttu-id="b3cd8-106">**Visual Studio 2015 ou Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="b3cd8-107">**[Data Lake Tools pour Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="b3cd8-108">Une fois Data Lake Tools pour Visual Studio installé, un élément **Data Lake** figure dans le menu **Outils** de Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="b3cd8-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in the **Tools** menu in Visual Studio:</span></span>

    ![Menu U-SQL Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="b3cd8-110">**Connaissances de base de Data Lake Analytics et de Data Lake Tools pour Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-110">**Basic knowledge of Data Lake Analytics and the Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="b3cd8-111">Pour commencer, consultez :</span><span class="sxs-lookup"><span data-stu-id="b3cd8-111">To get started, see:</span></span>

  * <span data-ttu-id="b3cd8-112">[Développer des scripts U-SQL à l'aide de Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b3cd8-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="b3cd8-113">**Un compte Data Lake Analytics.**</span><span class="sxs-lookup"><span data-stu-id="b3cd8-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="b3cd8-114">Consultez [Créer un compte Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b3cd8-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="b3cd8-115">**Télécharger les exemples de données sur le compte Data Lake Analytics.**</span><span class="sxs-lookup"><span data-stu-id="b3cd8-115">**Upload the sample data to the Data Lake Analytics account.**</span></span> <span data-ttu-id="b3cd8-116">Consultez [Pour copier des fichiers de données d’exemple](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b3cd8-116">See [To copy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="b3cd8-117">Pour lancer une tâche Data Lake Analytics, vous aurez besoin de données.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-117">To run a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="b3cd8-118">Bien que Data Lake Tools prenne en charge le téléchargement de données, vous allez utiliser le portail pour télécharger les exemples de données, ce qui facilitera la progression dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-118">Even though the Data Lake Tools supports uploading data, you will use the portal to upload the sample data to make this tutorial easier to follow.</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="b3cd8-119">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="b3cd8-119">Connect to Azure</span></span>
<span data-ttu-id="b3cd8-120">Avant de pouvoir générer et tester des scripts U-SQL, vous devez d'abord vous connecter à Azure.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-120">Before you can build and test any U-SQL scripts, you must first connect to Azure.</span></span>

<span data-ttu-id="b3cd8-121">**Se connecter à Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="b3cd8-121">**To connect to Data Lake Analytics**</span></span>

1. <span data-ttu-id="b3cd8-122">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="b3cd8-123">Cliquez sur **Data Lake > Options et paramètres**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="b3cd8-124">Cliquez sur **Connexion** ou sur **Changer d’utilisateur** si un autre utilisateur est connecté et suivez les instructions.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-124">Click **Sign In**, or **Change User** if someone has signed in, and follow the instructions.</span></span>
4. <span data-ttu-id="b3cd8-125">Cliquez sur **OK** pour fermer la boîte de dialogue Options et paramètres.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-125">Click **OK** to close the Options and Settings dialog.</span></span>

<span data-ttu-id="b3cd8-126">**Pour parcourir vos comptes Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="b3cd8-126">**To browse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="b3cd8-127">Dans Visual Studio, ouvrez **l’Explorateur de serveurs** en appuyant sur **CTRL+ALT+S**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="b3cd8-128">Dans l’**Explorateur de serveurs**, développez **Azure**, puis **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="b3cd8-129">Le cas échéant, la liste de vos comptes Data Lake Analytics s'affiche.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="b3cd8-130">Vous ne pouvez pas créer de comptes Data Lake Analytics à partir du studio.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-130">You cannot create Data Lake Analytics accounts from the studio.</span></span> <span data-ttu-id="b3cd8-131">Pour créer un compte, consultez [Prise en main d’Azure Data Lake Analytics à l’aide du Portail Azure](data-lake-analytics-get-started-portal.md) ou [Prise en main d’Azure Data Lake Analytics avec Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b3cd8-131">To create an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="b3cd8-132">Développement d'application U-SQL</span><span class="sxs-lookup"><span data-stu-id="b3cd8-132">Develop U-SQL application</span></span>
<span data-ttu-id="b3cd8-133">Une application U-SQL est essentiellement un script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="b3cd8-134">Pour en savoir plus sur U-SQL, consultez [Prise en main de U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b3cd8-134">To learn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="b3cd8-135">Vous pouvez ajouter des opérateurs définis par l'utilisateur à l'application.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-135">You can add addition user-defined operators to the application.</span></span>  <span data-ttu-id="b3cd8-136">Pour plus d'informations, consultez [Développer des opérateurs définis par l'utilisateur U-SQL pour des travaux Data Lake Analytics](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="b3cd8-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="b3cd8-137">**Pour créer et soumettre une tâche Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="b3cd8-137">**To create and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="b3cd8-138">Cliquez sur **Fichier > Nouveau > Projet**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-138">Click the **File > New > Project**.</span></span>
2. <span data-ttu-id="b3cd8-139">Sélectionnez le type de projet U-SQL.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-139">Select the U-SQL Project type.</span></span>

    ![nouveau projet U-SQL Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="b3cd8-141">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-141">Click **OK**.</span></span> <span data-ttu-id="b3cd8-142">Visual Studio crée une solution avec un fichier Script.usql.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="b3cd8-143">Insérez le script suivant dans le fichier Script.usql :</span><span class="sxs-lookup"><span data-stu-id="b3cd8-143">Enter the following script into the Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need to read from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from the weblog file with the correct schema.
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

    <span data-ttu-id="b3cd8-144">Pour comprendre U-SQL, voir [Prise en main du langage U-SQL Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b3cd8-144">To understand the U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="b3cd8-145">Ajoutez un nouveau script U-SQL dans votre projet et entrez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="b3cd8-145">Add a new U-SQL script to your project and enter the following:</span></span>

        // Query the referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        TO @"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="b3cd8-146">Revenez au premier script U-SQL, puis, à côté du bouton **Soumettre** , spécifiez votre compte Analytics.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-146">Switch back to the first U-SQL script and next to the **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="b3cd8-147">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur **Script.usql**, puis cliquez sur **Générer le script**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="b3cd8-148">Vérifiez les résultats dans le volet Sortie.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-148">Verify the results in the Output pane.</span></span>
8. <span data-ttu-id="b3cd8-149">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur **Script.usql**, puis cliquez sur **Soumettre le script**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="b3cd8-150">Vérifiez que le **compte Analytics** est celui où vous souhaitez exécuter la tâche, puis cliquez sur **Soumettre**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-150">Verify the **Analytics Account** is the one where you want to run the job, and then click **Submit**.</span></span> <span data-ttu-id="b3cd8-151">Les résultats de la soumission et le lien vers la tâche sont disponibles dans la fenêtre Résultats de Data Lake Tools pour Visual Studio à l'issue de la soumission.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-151">Submission results and job link are available in the Data Lake Tools for Visual Studio Results window when the submission is completed.</span></span>
10. <span data-ttu-id="b3cd8-152">Attendez que la tâche soit terminée avec succès.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-152">Wait until the job is completed successfully.</span></span>  <span data-ttu-id="b3cd8-153">Si la tâche a échoué, le fichier source est probablement manquant.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-153">If the job failed, it is most likely missing the source file.</span></span>  <span data-ttu-id="b3cd8-154">Consultez la section Configuration requise de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-154">Please see the Prerequisite section of this tutorial.</span></span> <span data-ttu-id="b3cd8-155">Pour plus d'informations de dépannage, consultez [Analyser et résoudre les problèmes des tâches Azure Data Lake Analytics](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="b3cd8-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="b3cd8-156">Une fois la tâche terminée, l'écran suivant s'affiche :</span><span class="sxs-lookup"><span data-stu-id="b3cd8-156">When the job is completed, you shall see the following screen:</span></span>

    ![data lake analytics analyser les journaux des sites web](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="b3cd8-158">Répétez les étapes 7 à 10 pour **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="b3cd8-159">**Pour voir la sortie du travail**</span><span class="sxs-lookup"><span data-stu-id="b3cd8-159">**To see the job output**</span></span>

1. <span data-ttu-id="b3cd8-160">Dans l’**Explorateur de serveurs**, développez **Azure**, **Data Lake Analytics**, puis votre compte Data Lake Analytics et **Comptes de stockage**. Cliquez avec le bouton droit sur le compte de stockage Data Lake par défaut, puis sur **Explorateur**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="b3cd8-161">Double-cliquez sur **Exemples** pour ouvrir le dossier, puis double-cliquez sur **Sorties**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-161">Double-click **Samples** to open the folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="b3cd8-162">Double-cliquez sur **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="b3cd8-163">Vous pouvez également double-cliquer sur le fichier de sortie dans l'affichage graphique de la tâche afin d'accéder directement à la sortie.</span><span class="sxs-lookup"><span data-stu-id="b3cd8-163">You can also double-click the output file inside the graph view of the job in order to navigate directly to the output.</span></span>

## <a name="see-also"></a><span data-ttu-id="b3cd8-164">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b3cd8-164">See also</span></span>
<span data-ttu-id="b3cd8-165">Pour commencer à utiliser Data Lake Analytics à l'aide de différents outils, consultez :</span><span class="sxs-lookup"><span data-stu-id="b3cd8-165">To get started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="b3cd8-166">Prendre en main Data Lake Analytics à l'aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="b3cd8-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="b3cd8-167">Prise en main de Data Lake Analytics à l'aide d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3cd8-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="b3cd8-168">Prise en main de Data Lake Analytics à l'aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="b3cd8-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
