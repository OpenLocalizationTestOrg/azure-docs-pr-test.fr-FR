---
title: aaaAuditing dans Azure SQL Data Warehouse | Documents Microsoft
description: "Prise en main de l’audit dans Azure SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="e35c2-103">Audit dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e35c2-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e35c2-104">Audit</span><span class="sxs-lookup"><span data-stu-id="e35c2-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="e35c2-105">Détection de menaces</span><span class="sxs-lookup"><span data-stu-id="e35c2-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="e35c2-106">L’audit de l’entrepôt de données SQL vous permet de toorecord événements dans votre journal d’audit de base de données tooan dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e35c2-106">SQL Data Warehouse auditing allows you toorecord events in your database tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="e35c2-107">L’audit peut vous aider à respecter une conformité réglementaire, à comprendre l’activité de la base de données, et à découvrir des discordances et des anomalies susceptibles d’indiquer des problèmes pour l’entreprise ou des violations de la sécurité.</span><span class="sxs-lookup"><span data-stu-id="e35c2-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="e35c2-108">Cette fonction s’intègre également dans Microsoft Power BI, afin de faciliter la création d’analyses et de rapports approfondis.</span><span class="sxs-lookup"><span data-stu-id="e35c2-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="e35c2-109">Les outils d’audit activent et facilitent les normes de conformité toocompliance mais ne garantissent pas la conformité.</span><span class="sxs-lookup"><span data-stu-id="e35c2-109">Auditing tools enable and facilitate adherence toocompliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="e35c2-110">Pour plus d’informations sur Azure programmes que la conformité aux normes de prise en charge, consultez hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span><span class="sxs-lookup"><span data-stu-id="e35c2-110">For more information about Azure programs that support standards compliance, see hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="e35c2-111">[Principes fondamentaux de l’audit de base de données]</span><span class="sxs-lookup"><span data-stu-id="e35c2-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="e35c2-112">[Configuration de l'audit pour votre base de données]</span><span class="sxs-lookup"><span data-stu-id="e35c2-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="e35c2-113">[Analyse des journaux et des rapports d’audit]</span><span class="sxs-lookup"><span data-stu-id="e35c2-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="e35c2-114"><a id="subheading-1"></a>Principes fondamentaux de l’audit de base de données Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e35c2-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="e35c2-115">Éléments rendus possibles par l’audit de bases de données SQL Data Warehouse :</span><span class="sxs-lookup"><span data-stu-id="e35c2-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="e35c2-116">**La rétention** d’une piste d’audit d’événements sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="e35c2-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="e35c2-117">Vous pouvez définir des catégories de base de données actions toobe est auditée.</span><span class="sxs-lookup"><span data-stu-id="e35c2-117">You can define categories of database actions  toobe audited.</span></span>
* <span data-ttu-id="e35c2-118">**La génération de rapports** sur les activités de la base de données.</span><span class="sxs-lookup"><span data-stu-id="e35c2-118">**Report** on database activity.</span></span> <span data-ttu-id="e35c2-119">Vous pouvez utiliser les rapports préconfigurés et un tooget de tableau de bord rapidement opérationnel avec activité et les rapports d’événements.</span><span class="sxs-lookup"><span data-stu-id="e35c2-119">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="e35c2-120">**L'analyse** des rapports.</span><span class="sxs-lookup"><span data-stu-id="e35c2-120">**Analyze** reports.</span></span> <span data-ttu-id="e35c2-121">Vous pouvez repérer les événements suspects, les activités inhabituelles et les tendances.</span><span class="sxs-lookup"><span data-stu-id="e35c2-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="e35c2-122">Vous pouvez configurer l’audit pour hello suivant des catégories d’événements :</span><span class="sxs-lookup"><span data-stu-id="e35c2-122">You can configure auditing for hello following event categories:</span></span>

<span data-ttu-id="e35c2-123">**SQL brut** et **SQL paramétrées** pour le hello les journaux d’audit collectées sont classés comme</span><span class="sxs-lookup"><span data-stu-id="e35c2-123">**Plain SQL** and **Parameterized SQL** for which hello collected audit logs are classified as</span></span>  

* <span data-ttu-id="e35c2-124">**Accès toodata**</span><span class="sxs-lookup"><span data-stu-id="e35c2-124">**Access toodata**</span></span>
* <span data-ttu-id="e35c2-125">**modifications de schéma (DDL) ;**</span><span class="sxs-lookup"><span data-stu-id="e35c2-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="e35c2-126">**modifications de données (DML) ;**</span><span class="sxs-lookup"><span data-stu-id="e35c2-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="e35c2-127">**comptes, rôles et autorisations (DCL) ;**</span><span class="sxs-lookup"><span data-stu-id="e35c2-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="e35c2-128">**Procédure stockée**, **Connexion** et **Gestion des transactions**.</span><span class="sxs-lookup"><span data-stu-id="e35c2-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="e35c2-129">Pour chaque catégorie d’événements, les audits des opérations **Succès** et **Échec** sont configurées séparément.</span><span class="sxs-lookup"><span data-stu-id="e35c2-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="e35c2-130">Pour plus d’informations sur les activités hello et les événements audités, consultez hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">référence de Format de journal d’Audit (téléchargement de fichier doc)</a>.</span><span class="sxs-lookup"><span data-stu-id="e35c2-130">For more information about hello activities and events audited, see hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="e35c2-131">Les journaux d'audit sont stockés dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e35c2-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="e35c2-132">Vous pouvez définir une période de rétention des journaux d'audit.</span><span class="sxs-lookup"><span data-stu-id="e35c2-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="e35c2-133">Une stratégie d’audit peut être définie pour une base de données spécifique ou en tant que stratégie de serveur par défaut.</span><span class="sxs-lookup"><span data-stu-id="e35c2-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="e35c2-134">Une stratégie d’audit de serveur par défaut s’applique tooall de bases de données sur un serveur, ce qui n’ont pas d’une substitution de base de données stratégie d’audit spécifique définie.</span><span class="sxs-lookup"><span data-stu-id="e35c2-134">A default server auditing policy applies tooall databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="e35c2-135">Avant de configurer l’audit, vérifiez que vous utilisez bien un [« Client de niveau inférieur »](sql-data-warehouse-auditing-downlevel-clients.md).</span><span class="sxs-lookup"><span data-stu-id="e35c2-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="e35c2-136"><a id="subheading-2"></a>Configuration de l’audit pour votre base de données</span><span class="sxs-lookup"><span data-stu-id="e35c2-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="e35c2-137">Lancez hello <a href="https://portal.azure.com" target="_blank">portail Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="e35c2-137">Launch hello <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="e35c2-138">Accédez toohello **paramètres** Panneau de hello souhaité tooaudit SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e35c2-138">Go toohello **Settings** blade of hello SQL Data Warehouse you want tooaudit.</span></span> <span data-ttu-id="e35c2-139">Bonjour **paramètres** panneau, sélectionnez **détection d’audit et de menaces**.</span><span class="sxs-lookup"><span data-stu-id="e35c2-139">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="e35c2-140">Ensuite, activez l’audit en cliquant sur hello **ON** bouton.</span><span class="sxs-lookup"><span data-stu-id="e35c2-140">Next, enable auditing by clicking hello **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="e35c2-141">Bonjour l’audit du Panneau de configuration, sélectionnez **détails de stockage** Panneau de stockage des journaux d’Audit tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="e35c2-141">In hello auditing configuration blade, select **STORAGE DETAILS** tooopen hello Audit Logs Storage blade.</span></span> <span data-ttu-id="e35c2-142">Sélectionnez hello compte de stockage Azure dans lequel les journaux sont enregistrés et hello période de rétention.</span><span class="sxs-lookup"><span data-stu-id="e35c2-142">Select hello Azure storage account where logs will be saved and, hello retention period.</span></span> 
>[!TIP]
><span data-ttu-id="e35c2-143">Hello utilisez même compte de stockage pour tous les hello tooget de bases de données audités parti hello préconfiguré signale des modèles.</span><span class="sxs-lookup"><span data-stu-id="e35c2-143">Use hello same storage account for all audited databases tooget hello most out of hello pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="e35c2-144">Cliquez sur hello **OK** configuration des détails stockage bouton toosave hello.</span><span class="sxs-lookup"><span data-stu-id="e35c2-144">Click hello **OK** button toosave hello storage details configuration.</span></span>
6. <span data-ttu-id="e35c2-145">Sous **journalisation par événement**, cliquez sur **réussite** et **échec** toolog tous les événements, ou choisir des catégories d’événements.</span><span class="sxs-lookup"><span data-stu-id="e35c2-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** toolog all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="e35c2-146">Si vous configurez l’audit pour une base de données, vous devrez peut-être la chaîne de connexion tooalter hello de votre tooensure client audit de données est capturée correctement.</span><span class="sxs-lookup"><span data-stu-id="e35c2-146">If you are configuring Auditing for a database, you may need tooalter hello connection string of your client tooensure data auditing is correctly captured.</span></span> <span data-ttu-id="e35c2-147">Vérifiez hello [modifier les FQDN de serveur dans la chaîne de connexion hello](sql-data-warehouse-auditing-downlevel-clients.md) rubrique pour les connexions de client de niveau inférieur.</span><span class="sxs-lookup"><span data-stu-id="e35c2-147">Check hello [Modify Server FDQN in hello connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="e35c2-148">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e35c2-148">Click **OK**.</span></span>

## <span data-ttu-id="e35c2-149"><a id="subheading-3"></a>Analyse des journaux et des rapports d’audit</span><span class="sxs-lookup"><span data-stu-id="e35c2-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="e35c2-150">Journaux d’audit sont regroupées dans une collection de Tables de magasin avec un **SQLDBAuditLogs** préfixe Bonjour compte de stockage Azure que vous avez choisi lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="e35c2-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="e35c2-151">Vous pouvez afficher les fichiers journaux à l'aide d'un outil tel que l'<a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Explorateur de stockage Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="e35c2-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="e35c2-152">Un modèle de rapport de tableau de bord préconfigurés est disponible en tant qu’un <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">feuille de calcul Excel téléchargeable</a> toohelp analyser rapidement les données du journal.</span><span class="sxs-lookup"><span data-stu-id="e35c2-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> toohelp you quickly analyze log data.</span></span> <span data-ttu-id="e35c2-153">modèle de hello toouse sur vos journaux d’audit, vous devez Excel 2013 ou version ultérieure et Power Query, que vous pouvez télécharger <a href="http://www.microsoft.com/download/details.aspx?id=39379">ici</a>.</span><span class="sxs-lookup"><span data-stu-id="e35c2-153">toouse hello template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="e35c2-154">modèle de Hello comporte des données d’exemple fictif, et vous pouvez configurer Power Query tooimport votre journal d’audit directement à partir de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e35c2-154">hello template has fictional sample data in it, and you can set up Power Query tooimport your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="e35c2-155"><a id="subheading-4"></a>Régénération des clés de stockage</span><span class="sxs-lookup"><span data-stu-id="e35c2-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="e35c2-156">En production, vous êtes probablement toorefresh votre stockage de clés périodiquement.</span><span class="sxs-lookup"><span data-stu-id="e35c2-156">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="e35c2-157">Lors de l’actualisation de vos clés, vous devez la stratégie de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="e35c2-157">When refreshing your keys, you need toosave hello policy.</span></span> <span data-ttu-id="e35c2-158">processus de Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="e35c2-158">hello process is as follows:</span></span>

1. <span data-ttu-id="e35c2-159">Bonjour à l’audit du Panneau de configuration (comme décrit ci-dessus dans le programme d’installation hello section d’audit) Basculer hello **clé d’accès de stockage** de *principal* trop*secondaire* et  **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e35c2-159">In hello auditing configuration blade (described above in hello setup auditing section) switch hello **Storage Access Key** from *Primary* too*Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="e35c2-160">Panneau de configuration de stockage accédez toohello et **régénérer** hello *clé d’accès primaire*.</span><span class="sxs-lookup"><span data-stu-id="e35c2-160">Go toohello storage configuration blade and **regenerate** hello *Primary Access Key*.</span></span>
3. <span data-ttu-id="e35c2-161">Revenir en arrière toohello l’audit du Panneau de configuration, commutateur hello **clé d’accès de stockage** de *secondaire* trop*principal* et appuyez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e35c2-161">Go back toohello auditing configuration blade, switch hello **Storage Access Key** from *Secondary* too*Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="e35c2-162">Revenir en arrière toohello stockage UI et **régénérer** hello *clé d’accès secondaire* (dans la préparation de hello clés prochains cycle d’actualisation.</span><span class="sxs-lookup"><span data-stu-id="e35c2-162">Go back toohello storage UI and **regenerate** hello *Secondary Access Key* (as preparation for hello next keys refresh cycle.</span></span>

## <span data-ttu-id="e35c2-163"><a id="subheading-5"></a>Automation (PowerShell / API REST)</span><span class="sxs-lookup"><span data-stu-id="e35c2-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="e35c2-164">Vous pouvez également configurer l’audit dans l’entrepôt de données SQL Azure à l’aide de hello suivant des outils d’automatisation :</span><span class="sxs-lookup"><span data-stu-id="e35c2-164">You can also configure auditing in Azure SQL Data Warehouse by using hello following automation tools:</span></span>

* <span data-ttu-id="e35c2-165">**Applets de commande PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="e35c2-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="e35c2-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="e35c2-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="e35c2-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="e35c2-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="e35c2-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="e35c2-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="e35c2-169">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="e35c2-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="e35c2-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="e35c2-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="e35c2-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="e35c2-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="e35c2-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="e35c2-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

<!--Anchors-->
[Principes fondamentaux de l’audit de base de données]: #subheading-1
[Configuration de l'audit pour votre base de données]: #subheading-2
[Analyse des journaux et des rapports d’audit]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy