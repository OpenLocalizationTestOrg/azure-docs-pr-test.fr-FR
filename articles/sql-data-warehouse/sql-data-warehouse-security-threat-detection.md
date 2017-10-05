---
title: Prise en main de Threat Detection pour SQL Data Warehouse
description: "Prise en main de la détection de menaces"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: c9073dd9-6c62-4735-8457-dfb9f859c900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: f4a2376fe4fb710d031c35ca7fdbf4c7bb0f3caa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="54122-103">Prise en main de la détection de menaces</span><span class="sxs-lookup"><span data-stu-id="54122-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="54122-104">Audit</span><span class="sxs-lookup"><span data-stu-id="54122-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="54122-105">Détection de menaces</span><span class="sxs-lookup"><span data-stu-id="54122-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="54122-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="54122-106">Overview</span></span>
<span data-ttu-id="54122-107">Threat Detection permet de détecter les activités base de données anormales indiquant la présence potentielle de menaces de sécurité pour la base de données.</span><span class="sxs-lookup"><span data-stu-id="54122-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="54122-108">Threat Detection est disponible en version préliminaire et est pris en charge pour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="54122-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="54122-109">Threat Detection fournit une nouvelle couche de sécurité qui permet aux clients de détecter les menaces potentielles et d’y répondre à mesure qu’elles se présentent en générant des alertes de sécurité sur les activités anormales.</span><span class="sxs-lookup"><span data-stu-id="54122-109">Threat Detection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="54122-110">Les utilisateurs peuvent explorer les événements suspects à l’aide de l’ [audit d’Azure SQL Data Warehouse](sql-data-warehouse-auditing-overview.md) pour déterminer s’ils sont le résultat d’une tentative d’accès, d’une violation ou d’une exploitation des données dans l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="54122-110">Users can explore the suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) to determine if they result from an attempt to access, breach or exploit data in the data warehouse.</span></span>
<span data-ttu-id="54122-111">Threat Detection vous permet de réagir facilement aux menaces potentielles envers l'entrepôt de données sans avoir à acquérir une expertise de la sécurité ou à gérer des systèmes de surveillance de la sécurité avancés.</span><span class="sxs-lookup"><span data-stu-id="54122-111">Threat Detection makes it simple to address potential threats to the data warehouse without the need to be a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="54122-112">Par exemple, il détecte certaines activités de base de données anormales indiquant des tentatives d’injection SQL potentielles.</span><span class="sxs-lookup"><span data-stu-id="54122-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="54122-113">L’injection SQL représente l’un des problèmes de sécurité auxquels sont le plus exposées les applications web, et est utilisée pour cibler les applications pilotées par des données.</span><span class="sxs-lookup"><span data-stu-id="54122-113">SQL injection is one of the common Web application security issues on the Internet, used to attack data-driven applications.</span></span> <span data-ttu-id="54122-114">Les pirates exploitent les vulnérabilités des applications pour injecter des instructions SQL nuisibles dans les champs de saisie d’application afin de violer ou modifier les données contenues dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="54122-114">Attackers take advantage of application vulnerabilities to inject malicious SQL statements into application entry fields, for breaching or modifying data in the database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="54122-115">Configurer Threat Detection pour votre base de données</span><span class="sxs-lookup"><span data-stu-id="54122-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="54122-116">Accédez à l’adresse [https://portal.azure.com](https://portal.azure.com)et exécutez le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="54122-116">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="54122-117">Accédez au volet de configuration de l'entrepôt SQL Data Warehouse que voulez surveiller.</span><span class="sxs-lookup"><span data-stu-id="54122-117">Navigate to the configuration blade of the SQL Data Warehouse you want to monitor.</span></span> <span data-ttu-id="54122-118">Dans le panneau Paramètres, sélectionnez **Audit et détection des menaces**.</span><span class="sxs-lookup"><span data-stu-id="54122-118">In the Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Volet de navigation][1]
3. <span data-ttu-id="54122-120">Dans le panneau de configuration **Audit et détection des menaces**, **activez** l’audit pour afficher les paramètres Détection des menaces.</span><span class="sxs-lookup"><span data-stu-id="54122-120">In the **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display the Threat detection settings.</span></span>
   
    ![Volet de navigation][2]
4. <span data-ttu-id="54122-122">**Activez** la détection des menaces.</span><span class="sxs-lookup"><span data-stu-id="54122-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="54122-123">Configurez la liste des adresses électroniques qui recevront les alertes de sécurité en cas de détection d'activités anormales sur l'entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="54122-123">Configure the list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="54122-124">Cliquez sur **Enregistrer** dans le panneau de configuration **Audit et détection des menaces** pour enregistrer la stratégie d’audit et de détection des menaces que vous avez créée ou modifiée.</span><span class="sxs-lookup"><span data-stu-id="54122-124">Click **Save** in the **Auditing & Threat detection** configuration blade to save the new or updated auditing and threat detection policy.</span></span>
   
    ![Volet de navigation][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="54122-126">Explorer les activités anormales sur l'entrepôt de données en cas de détection d'un événement suspect</span><span class="sxs-lookup"><span data-stu-id="54122-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="54122-127">Vous recevrez une notification par courrier électronique lorsque des activités anormales sont détectées au niveau de la base de données.</span><span class="sxs-lookup"><span data-stu-id="54122-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="54122-128">Le courrier électronique contiendra des informations sur l’événement de sécurité suspect, notamment la nature des activités anormales, le nom de la base de données, le nom du serveur et l’heure de l’événement.</span><span class="sxs-lookup"><span data-stu-id="54122-128">The email will provide information on the suspicious security event including the nature of the anomalous activities, database name, server name and the event time.</span></span> <span data-ttu-id="54122-129">Il fournit également des informations sur les causes possibles et les mesures recommandées afin d’examiner et atténuer la menace potentielle pesant sur la base de données.</span><span class="sxs-lookup"><span data-stu-id="54122-129">In addition, it will provide information on possible causes and recommended actions to investigate and mitigate the potential threat to the database.</span></span><br/>
   
    ![Volet de navigation][4]
2. <span data-ttu-id="54122-131">Dans le courrier électronique, cliquez sur le lien **Azure SQL Auditing Log** pour ouvrir le portail Azure Classic et afficher les enregistrements d’audit pertinents au moment de l’événement suspect.</span><span class="sxs-lookup"><span data-stu-id="54122-131">In the email, click on the **Azure SQL Auditing Log** link, which will launch the Azure Classic Portal and show the relevant Auditing records around the time of the suspicious event.</span></span>
   
    ![Volet de navigation][5]
3. <span data-ttu-id="54122-133">Cliquez sur les enregistrements d’audit pour afficher plus de détails sur les activités de base de données suspects, comme l’instruction SQL, la cause de l’échec et l’adresse IP client.</span><span class="sxs-lookup"><span data-stu-id="54122-133">Click on the audit records to view more details on the suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Volet de navigation][6]
4. <span data-ttu-id="54122-135">Dans le panneau des enregistrements d’audit, cliquez sur **Ouvrir dans Excel** pour ouvrir un modèle Excel préconfiguré à importer et exécuter une analyse plus approfondie du journal d’audit au moment de l’événement suspect.</span><span class="sxs-lookup"><span data-stu-id="54122-135">In the Auditing Records blade, click  **Open in Excel** to open a pre-configured excel template to import and run deeper analysis of the audit log around the time of the suspicious event.</span></span><br/><span data-ttu-id="54122-136">
   **Remarque :** dans Excel 2010 ou version ultérieure, les paramètres Power Query et **Combinaison rapide** sont requis</span><span class="sxs-lookup"><span data-stu-id="54122-136">
**Note:** In Excel 2010 or later, Power Query and the **Fast Combine** setting is required</span></span>
   
    ![Volet de navigation][7]
5. <span data-ttu-id="54122-138">Pour configurer le paramètre **Combinaison rapide** : sous l’onglet du ruban **POWER QUERY**, sélectionnez **Options** pour afficher la boîte de dialogue correspondante.</span><span class="sxs-lookup"><span data-stu-id="54122-138">To configure the **Fast Combine** setting - In the **POWER QUERY** ribbon tab, select **Options** to display the Options dialog.</span></span> <span data-ttu-id="54122-139">Sélectionnez la section Confidentialité et choisissez la deuxième option « gnore the Privacy Levels and potentially improve performance » :</span><span class="sxs-lookup"><span data-stu-id="54122-139">Select the Privacy section and choose the second option - 'Ignore the Privacy Levels and potentially improve performance':</span></span>
   
    ![Volet de navigation][8]
6. <span data-ttu-id="54122-141">Pour charger les journaux d’audit SQL, vérifiez que les paramètres de l’onglet Paramètres sont correctement définis, puis sélectionnez le ruban « Données » et cliquez sur le bouton « Actualiser tout ».</span><span class="sxs-lookup"><span data-stu-id="54122-141">To load SQL audit logs, ensure that the parameters in the settings tab are set correctly and then select the 'Data' ribbon and click the 'Refresh All' button.</span></span>
   
    ![Volet de navigation][9]
7. <span data-ttu-id="54122-143">Les résultats s’affichent dans la feuille **SQL Audit Logs** , qui vous permet d’analyser de manière plus approfondie les activités anormales détectées et de limiter l’impact de l’événement de sécurité sur votre application.</span><span class="sxs-lookup"><span data-stu-id="54122-143">The results appear in the **SQL Audit Logs** sheet which enables you to run deeper analysis of the anomalous activities that were detected, and mitigate the impact of the security event in your application.</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-data-warehouse-security-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-data-warehouse-security-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-data-warehouse-security-threat-detection/4_td_email.png
[5]: ./media/sql-data-warehouse-security-threat-detection/5_td_audit_records.png
[6]: ./media/sql-data-warehouse-security-threat-detection/6_td_audit_record_details.png
[7]: ./media/sql-data-warehouse-security-threat-detection/7_td_audit_records_open_excel.png
[8]: ./media/sql-data-warehouse-security-threat-detection/8_td_excel_fast_combine.png
[9]: ./media/sql-data-warehouse-security-threat-detection/9_td_excel_parameters.png
