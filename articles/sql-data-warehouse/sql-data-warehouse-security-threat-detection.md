---
title: "aaaGet main de la détection des menaces de l’entrepôt de données SQL"
description: "Comment tooget démarrer avec la détection des menaces"
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
ms.openlocfilehash: dec0b734849e7f52434e099db0b38fbf0bf6ad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="1fa30-103">Prise en main de la détection de menaces</span><span class="sxs-lookup"><span data-stu-id="1fa30-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1fa30-104">Audit</span><span class="sxs-lookup"><span data-stu-id="1fa30-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="1fa30-105">Détection de menaces</span><span class="sxs-lookup"><span data-stu-id="1fa30-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="1fa30-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1fa30-106">Overview</span></span>
<span data-ttu-id="1fa30-107">La détection des menaces détecte des activités de base de données anormales indiquant de base de données des toohello des menaces de sécurité potentielles.</span><span class="sxs-lookup"><span data-stu-id="1fa30-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="1fa30-108">Threat Detection est disponible en version préliminaire et est pris en charge pour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1fa30-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="1fa30-109">La détection des menaces fournit une nouvelle couche de sécurité, ce qui permet aux clients toodetect et de répond toopotential menaces qu’ils se produisent en fournissant des alertes de sécurité sur les activités anormales.</span><span class="sxs-lookup"><span data-stu-id="1fa30-109">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="1fa30-110">Les utilisateurs peuvent Explorer à l’aide d’événements suspects hello [audit de l’entrepôt de données SQL Azure](sql-data-warehouse-auditing-overview.md) toodetermine s’ils résultent d’une tentative de tooaccess, violation ou exploiter les données dans l’entrepôt de données hello.</span><span class="sxs-lookup"><span data-stu-id="1fa30-110">Users can explore hello suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) toodetermine if they result from an attempt tooaccess, breach or exploit data in hello data warehouse.</span></span>
<span data-ttu-id="1fa30-111">La détection des menaces rend les menaces potentielles tooaddress simple toohello données de l’entrepôt sans hello besoin toobe un expert en sécurité ou gérer des systèmes de surveillance de la sécurité avancée.</span><span class="sxs-lookup"><span data-stu-id="1fa30-111">Threat Detection makes it simple tooaddress potential threats toohello data warehouse without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="1fa30-112">Par exemple, il détecte certaines activités de base de données anormales indiquant des tentatives d’injection SQL potentielles.</span><span class="sxs-lookup"><span data-stu-id="1fa30-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="1fa30-113">Injection SQL est un des hello Web application problèmes de sécurité courants sur hello Internet, les applications utilisées tooattack piloté par les données.</span><span class="sxs-lookup"><span data-stu-id="1fa30-113">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="1fa30-114">Les attaquants profiter d’application vulnérabilités tooinject des instructions SQL malveillantes dans les champs de saisie d’application, de violation ou de modification des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="1fa30-114">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="1fa30-115">Configurer Threat Detection pour votre base de données</span><span class="sxs-lookup"><span data-stu-id="1fa30-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="1fa30-116">Lancement hello portail Azure à l’adresse [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1fa30-116">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1fa30-117">Accédez à panneau de configuration toohello Hello souhaité toomonitor SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1fa30-117">Navigate toohello configuration blade of hello SQL Data Warehouse you want toomonitor.</span></span> <span data-ttu-id="1fa30-118">Dans le panneau des paramètres de hello, sélectionnez **audit et la détection des menaces**.</span><span class="sxs-lookup"><span data-stu-id="1fa30-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Volet de navigation][1]
3. <span data-ttu-id="1fa30-120">Bonjour **audit et la détection des menaces** activer Panneau de configuration **ON** l’audit, qui affiche les paramètres de détection de menace hello.</span><span class="sxs-lookup"><span data-stu-id="1fa30-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello Threat detection settings.</span></span>
   
    ![Volet de navigation][2]
4. <span data-ttu-id="1fa30-122">**Activez** la détection des menaces.</span><span class="sxs-lookup"><span data-stu-id="1fa30-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="1fa30-123">Configurez la liste hello d’adresses de messagerie qui recevront les alertes de sécurité lors de la détection des activités de l’entrepôt de données anormales.</span><span class="sxs-lookup"><span data-stu-id="1fa30-123">Configure hello list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="1fa30-124">Cliquez sur **enregistrer** Bonjour **détection d’audit et de menaces** toosave Panneau de configuration hello nouvelle ou mis à jour stratégie de détection des menaces et de l’audit.</span><span class="sxs-lookup"><span data-stu-id="1fa30-124">Click **Save** in hello **Auditing & Threat detection** configuration blade toosave hello new or updated auditing and threat detection policy.</span></span>
   
    ![Volet de navigation][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="1fa30-126">Explorer les activités anormales sur l'entrepôt de données en cas de détection d'un événement suspect</span><span class="sxs-lookup"><span data-stu-id="1fa30-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="1fa30-127">Vous recevrez une notification par courrier électronique lorsque des activités anormales sont détectées au niveau de la base de données.</span><span class="sxs-lookup"><span data-stu-id="1fa30-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="1fa30-128">messagerie de Hello fournit des informations sur les événements de sécurité anormaux hello, y compris la nature hello d’activités anormales de hello, nom de la base de données, heure de serveur hello et de nom de l’événement.</span><span class="sxs-lookup"><span data-stu-id="1fa30-128">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="1fa30-129">En outre, il fournit des informations sur les causes possibles et recommandé actions tooinvestigate et atténuer la base de données du toohello de menaces potentielles hello.</span><span class="sxs-lookup"><span data-stu-id="1fa30-129">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
   
    ![Volet de navigation][4]
2. <span data-ttu-id="1fa30-131">Dans le message électronique de hello, cliquez sur hello **le journal d’audit Azure SQL** lien lance hello portail classique Azure et afficher les enregistrements de l’audit pertinentes hello en temps hello d’événement de suspectes hello.</span><span class="sxs-lookup"><span data-stu-id="1fa30-131">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure Classic Portal and show hello relevant Auditing records around hello time of hello suspicious event.</span></span>
   
    ![Volet de navigation][5]
3. <span data-ttu-id="1fa30-133">Cliquez sur hello audit enregistrements tooview plus de détails sur les activités de base de données suspecte hello comme instruction SQL, IP raison et le client d’échec.</span><span class="sxs-lookup"><span data-stu-id="1fa30-133">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Volet de navigation][6]
4. <span data-ttu-id="1fa30-135">Dans le panneau des enregistrements d’audit hello, cliquez sur **ouvrir dans Excel** tooopen un préconfiguré excel tooimport de modèle et d’exécuter une analyse plus approfondie du journal d’audit de hello en temps hello d’événement de suspectes hello.</span><span class="sxs-lookup"><span data-stu-id="1fa30-135">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span><br/><span data-ttu-id="1fa30-136">
   **Remarque :** dans Excel 2010 ou version ultérieure, Power Query et hello **combinaison rapide** paramètre est requis</span><span class="sxs-lookup"><span data-stu-id="1fa30-136">
**Note:** In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required</span></span>
   
    ![Volet de navigation][7]
5. <span data-ttu-id="1fa30-138">tooconfigure hello **combinaison rapide** le paramètre - Bonjour **POWER QUERY** onglet de ruban, sélectionnez **Options** boîte de dialogue Options toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="1fa30-138">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="1fa30-139">Sélectionnez la section de confidentialité hello et choisissez hello deuxième option - « Ignorer les niveaux de confidentialité hello et potentiellement améliorer les performances » :</span><span class="sxs-lookup"><span data-stu-id="1fa30-139">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>
   
    ![Volet de navigation][8]
6. <span data-ttu-id="1fa30-141">les journaux d’audit tooload SQL, assurez-vous que hello les paramètres dans l’onglet Paramètres de hello sont correctement définies et puis sélectionnez hello 'Data' ruban et cliquez sur le bouton Actualiser tout de hello.</span><span class="sxs-lookup"><span data-stu-id="1fa30-141">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>
   
    ![Volet de navigation][9]
7. <span data-ttu-id="1fa30-143">résultats de Hello s’affichent dans hello **les journaux d’Audit SQL** feuille qui vous permet d’effectuer une analyse toorun des activités anormales de hello qui ont été détectés et d’atténuer l’impact hello d’événement de sécurité hello dans votre application.</span><span class="sxs-lookup"><span data-stu-id="1fa30-143">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>

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
