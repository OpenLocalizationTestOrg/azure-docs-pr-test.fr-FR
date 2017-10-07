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
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a>Analyser les journaux des sites web à l’aide d’Azure Data Lake Analytics
Découvrez comment tooanalyze journaux de site Web à l’aide d’Analytique de LAC de données, en particulier sur découvrir les points d’accès s’est produite erreurs quand il a tenté de site Web de toovisit hello.

## <a name="prerequisites"></a>Composants requis
* **Visual Studio 2015 ou Visual Studio 2013**.
* **[Data Lake Tools pour Visual Studio](http://aka.ms/adltoolsvs)**.

    Une fois que Data Lake Tools pour Visual Studio est installé, vous verrez un **Data Lake** élément Bonjour **outils** menu dans Visual Studio :

    ![Menu U-SQL Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* **Connaissances de base de données de LAC Analytique et hello Data Lake Tools pour Visual Studio**. tooget démarré, consultez :

  * [Développer des scripts U-SQL à l'aide des Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* **Un compte Data Lake Analytics.**  Consultez [Créer un compte Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
* **Téléchargez le compte de hello exemple données toohello Analytique lac de données.** Consultez [toocopy des fichiers de données](data-lake-analytics-get-started-portal.md).

    toorun une tâche Analytique lac de données, vous aurez besoin de certaines données. Bien que hello Data Lake Tools prend en charge le téléchargement de données, vous allez utiliser toomake de données exemple hello tooupload portail hello ce didacticiel toofollow plus facile.

## <a name="connect-tooazure"></a>Se connecter tooAzure
Avant de pouvoir générer et tester des scripts U-SQL, vous devez d’abord connecter tooAzure.

**tooconnect tooData Lake Analytique**

1. Ouvrez Visual Studio.
2. Cliquez sur **Data Lake > Options et paramètres**.
3. Cliquez sur **connexion**, ou **changer d’utilisateur** si quelqu'un s’est connecté et suivez les instructions de hello.
4. Cliquez sur **OK** boîte de dialogue tooclose hello Options et paramètres.

**toobrowse vos comptes Analytique lac de données**

1. Dans Visual Studio, ouvrez **l’Explorateur de serveurs** en appuyant sur **CTRL+ALT+S**.
2. Dans l’**Explorateur de serveurs**, développez **Azure**, puis **Data Lake Analytics**. Le cas échéant, la liste de vos comptes Data Lake Analytics s'affiche. Impossible de créer des comptes d’Analytique lac de données à partir de studio de hello. toocreate un compte, consultez [prise en main Analytique de LAC de données Azure à l’aide du portail Azure](data-lake-analytics-get-started-portal.md) ou [prise en main Analytique de LAC de données Azure à l’aide d’Azure PowerShell](data-lake-analytics-get-started-powershell.md).

## <a name="develop-u-sql-application"></a>Développement d'application U-SQL
Une application U-SQL est essentiellement un script U-SQL. toolearn en savoir plus sur U-SQL, consultez [prise en main U-SQL](data-lake-analytics-u-sql-get-started.md).

Vous pouvez ajouter l’application de toohello Ajout opérateurs définis par l’utilisateur.  Pour plus d'informations, consultez [Développer des opérateurs définis par l'utilisateur U-SQL pour des travaux Data Lake Analytics](data-lake-analytics-u-sql-develop-user-defined-operators.md).

**toocreate et soumettez une tâche Analytique lac de données**

1. Cliquez sur hello **fichier > Nouveau > projet**.
2. Sélectionnez le type de projet U-SQL hello.

    ![nouveau projet U-SQL Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. Cliquez sur **OK**. Visual Studio crée une solution avec un fichier Script.usql.
4. Entrez hello script suivant dans le fichier de Script.usql hello :

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

    toounderstand hello U-SQL, consultez [prise en main langage données Lake Analytique U-SQL](data-lake-analytics-u-sql-get-started.md).    
5. Ajoutez un nouveau projet de tooyour script U-SQL et tapez Bonjour suivante :

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. Basculer le script U-SQL de la première toohello précédent et suivant toohello **envoyer** et spécifier votre compte Analytique.
7. Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur **Script.usql**, puis cliquez sur **Générer le script**. Vérifier les résultats de hello dans le volet de sortie hello.
8. Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur **Script.usql**, puis cliquez sur **Soumettre le script**.
9. Vérifiez que hello **Analytique compte** est hello une où vous voulez toorun hello travail, puis cliquez sur **Submit**. Résultats de l’envoi et de lien de tâche sont disponibles dans hello Data Lake Tools pour la fenêtre Résultats Visual Studio lors de la soumission de hello est terminée.
10. Attendez que hello tâche terminée avec succès.  En cas d’échec de la tâche de hello, il est très probablement hello source fichier manquant.  Consultez la section Configuration requise de hello de ce didacticiel. Pour plus d'informations de dépannage, consultez [Analyser et résoudre les problèmes des tâches Azure Data Lake Analytics](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).

    À la fin du travail hello, vous allez voir hello suivant d’écran :

    ![data lake analytics analyser les journaux des sites web](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. Répétez les étapes 7 à 10 pour **Script1.usql**.

**sortie de tâche hello toosee**

1. À partir de **l’Explorateur de serveurs**, développez **Azure**, développez **Analytique lac de données**, développez votre compte Analytique lac de données, puis **lescomptesdestockage**, cliquez sur le compte de stockage des données Lake hello par défaut, puis cliquez sur **Explorer**.
2. Double-cliquez sur **exemples** tooopen hello du dossier, puis double-cliquez sur **sorties**.
3. Double-cliquez sur **UnsuccessfulResponsees.log**.
4. Vous pouvez également double-cliquer sur hello fichier de sortie à l’intérieur de vue du graphique hello du travail hello dans l’ordre toonavigate directement toohello de sortie.

## <a name="see-also"></a>Voir aussi
tooget main Analytique lac de données à l’aide de différents outils, consultez :

* [Prendre en main Data Lake Analytics à l'aide du portail Azure](data-lake-analytics-get-started-portal.md)
* [Prise en main de Data Lake Analytics à l'aide d'Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Prise en main de Data Lake Analytics à l'aide du Kit de développement logiciel (SDK) .NET](data-lake-analytics-get-started-net-sdk.md)
