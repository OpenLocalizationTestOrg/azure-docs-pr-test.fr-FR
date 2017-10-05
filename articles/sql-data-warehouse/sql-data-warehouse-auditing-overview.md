---
title: "Audit dans Azure SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: f851c82ebeaa647f663d499a4d327c3479e36121
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="ee815-103">Audit dans Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ee815-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee815-104">Audit</span><span class="sxs-lookup"><span data-stu-id="ee815-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="ee815-105">Détection de menaces</span><span class="sxs-lookup"><span data-stu-id="ee815-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="ee815-106">La fonction d’audit de SQL Data Warehouse vous permet d’enregistrer les événements survenus dans votre base de données dans un journal d’audit au sein de votre compte Microsoft Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ee815-106">SQL Data Warehouse auditing allows you to record events in your database to an audit log in your Azure Storage account.</span></span> <span data-ttu-id="ee815-107">L’audit peut vous aider à respecter une conformité réglementaire, à comprendre l’activité de la base de données, et à découvrir des discordances et des anomalies susceptibles d’indiquer des problèmes pour l’entreprise ou des violations de la sécurité.</span><span class="sxs-lookup"><span data-stu-id="ee815-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="ee815-108">Cette fonction s’intègre également dans Microsoft Power BI, afin de faciliter la création d’analyses et de rapports approfondis.</span><span class="sxs-lookup"><span data-stu-id="ee815-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="ee815-109">Les outils d'audit permettent et facilitent le respect des normes liées à la conformité, mais ne garantissent pas cette dernière.</span><span class="sxs-lookup"><span data-stu-id="ee815-109">Auditing tools enable and facilitate adherence to compliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="ee815-110">Pour plus d'informations sur les programmes Azure prenant en charge la conformité aux normes, consultez le <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Centre de gestion de la confidentialité Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="ee815-110">For more information about Azure programs that support standards compliance, see the <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="ee815-111">[Principes fondamentaux de l’audit de base de données]</span><span class="sxs-lookup"><span data-stu-id="ee815-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="ee815-112">[Configuration de l'audit pour votre base de données]</span><span class="sxs-lookup"><span data-stu-id="ee815-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="ee815-113">[Analyse des journaux et des rapports d’audit]</span><span class="sxs-lookup"><span data-stu-id="ee815-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="ee815-114"><a id="subheading-1"></a>Principes fondamentaux de l’audit de base de données Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ee815-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="ee815-115">Éléments rendus possibles par l’audit de bases de données SQL Data Warehouse :</span><span class="sxs-lookup"><span data-stu-id="ee815-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="ee815-116">**La rétention** d’une piste d’audit d’événements sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="ee815-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="ee815-117">Vous pouvez définir des catégories d’actions de base de données à auditer.</span><span class="sxs-lookup"><span data-stu-id="ee815-117">You can define categories of database actions  to be audited.</span></span>
* <span data-ttu-id="ee815-118">**La génération de rapports** sur les activités de la base de données.</span><span class="sxs-lookup"><span data-stu-id="ee815-118">**Report** on database activity.</span></span> <span data-ttu-id="ee815-119">Vous pouvez utiliser des rapports préconfigurés et un tableau de bord pour une prise en main rapide de la génération de rapports d'activités et d'événements.</span><span class="sxs-lookup"><span data-stu-id="ee815-119">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="ee815-120">**L'analyse** des rapports.</span><span class="sxs-lookup"><span data-stu-id="ee815-120">**Analyze** reports.</span></span> <span data-ttu-id="ee815-121">Vous pouvez repérer les événements suspects, les activités inhabituelles et les tendances.</span><span class="sxs-lookup"><span data-stu-id="ee815-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="ee815-122">Vous pouvez configurer l’audit pour les catégories d’événements suivantes :</span><span class="sxs-lookup"><span data-stu-id="ee815-122">You can configure auditing for the following event categories:</span></span>

<span data-ttu-id="ee815-123">**SQL brut** et **SQL paramétré** pour lesquels les journaux d’audit collectés sont classés comme</span><span class="sxs-lookup"><span data-stu-id="ee815-123">**Plain SQL** and **Parameterized SQL** for which the collected audit logs are classified as</span></span>  

* <span data-ttu-id="ee815-124">**accès aux données ;**</span><span class="sxs-lookup"><span data-stu-id="ee815-124">**Access to data**</span></span>
* <span data-ttu-id="ee815-125">**modifications de schéma (DDL) ;**</span><span class="sxs-lookup"><span data-stu-id="ee815-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="ee815-126">**modifications de données (DML) ;**</span><span class="sxs-lookup"><span data-stu-id="ee815-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="ee815-127">**comptes, rôles et autorisations (DCL) ;**</span><span class="sxs-lookup"><span data-stu-id="ee815-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="ee815-128">**Procédure stockée**, **Connexion** et **Gestion des transactions**.</span><span class="sxs-lookup"><span data-stu-id="ee815-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="ee815-129">Pour chaque catégorie d’événements, les audits des opérations **Succès** et **Échec** sont configurées séparément.</span><span class="sxs-lookup"><span data-stu-id="ee815-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="ee815-130">Pour plus d’informations sur les activités et les événements audités, consultez <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Informations de référence sur le format des journaux d’audit (téléchargement d’un fichier doc)</a>.</span><span class="sxs-lookup"><span data-stu-id="ee815-130">For more information about the activities and events audited, see the <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="ee815-131">Les journaux d'audit sont stockés dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ee815-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="ee815-132">Vous pouvez définir une période de rétention des journaux d'audit.</span><span class="sxs-lookup"><span data-stu-id="ee815-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="ee815-133">Une stratégie d’audit peut être définie pour une base de données spécifique ou en tant que stratégie de serveur par défaut.</span><span class="sxs-lookup"><span data-stu-id="ee815-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="ee815-134">Une stratégie d’audit de serveur par défaut s’applique à toutes les bases de données d’un serveur sur lequel aucune stratégie d’audit de base de données de substitution spécifique n’est définie.</span><span class="sxs-lookup"><span data-stu-id="ee815-134">A default server auditing policy applies to all databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="ee815-135">Avant de configurer l’audit, vérifiez que vous utilisez bien un [« Client de niveau inférieur »](sql-data-warehouse-auditing-downlevel-clients.md).</span><span class="sxs-lookup"><span data-stu-id="ee815-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="ee815-136"><a id="subheading-2"></a>Configuration de l’audit pour votre base de données</span><span class="sxs-lookup"><span data-stu-id="ee815-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="ee815-137">Lancez le <a href="https://portal.azure.com" target="_blank">portail Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="ee815-137">Launch the <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="ee815-138">Accédez au panneau **Paramètres** de l’instance SQL Data Warehouse que vous voulez auditer.</span><span class="sxs-lookup"><span data-stu-id="ee815-138">Go to the **Settings** blade of the SQL Data Warehouse you want to audit.</span></span> <span data-ttu-id="ee815-139">Dans le panneau **Paramètres**, sélectionnez **Audit et détection des menaces**.</span><span class="sxs-lookup"><span data-stu-id="ee815-139">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="ee815-140">Ensuite, activez la fonction d’audit en cliquant sur le bouton **ACTIVÉ** .</span><span class="sxs-lookup"><span data-stu-id="ee815-140">Next, enable auditing by clicking the **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="ee815-141">Dans le panneau de configuration de l’audit, sélectionnez **DÉTAILS DU STOCKAGE** pour ouvrir le panneau Stockage des journaux d’audit.</span><span class="sxs-lookup"><span data-stu-id="ee815-141">In the auditing configuration blade, select **STORAGE DETAILS** to open the Audit Logs Storage blade.</span></span> <span data-ttu-id="ee815-142">Sélectionnez le compte de stockage Azure dans lequel les journaux seront enregistrés, ainsi que la période de rétention.</span><span class="sxs-lookup"><span data-stu-id="ee815-142">Select the Azure storage account where logs will be saved and, the retention period.</span></span> 
>[!TIP]
><span data-ttu-id="ee815-143">Utilisez le même compte de stockage pour toutes les bases de données auditées afin de profiter au mieux des modèles de rapport préconfigurés.</span><span class="sxs-lookup"><span data-stu-id="ee815-143">Use the same storage account for all audited databases to get the most out of the pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="ee815-144">Cliquez sur le bouton **OK** pour enregistrer la configuration des détails du stockage.</span><span class="sxs-lookup"><span data-stu-id="ee815-144">Click the **OK** button to save the storage details configuration.</span></span>
6. <span data-ttu-id="ee815-145">Sous **JOURNALISATION PAR ÉVÈNEMENT**, cliquez sur **SUCCÈS** et sur **ÉCHEC**pour enregistrer tous les événements, ou choisissez des catégories d’événements individuelles.</span><span class="sxs-lookup"><span data-stu-id="ee815-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** to log all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="ee815-146">Si vous configurez l’audit pour une base de données, vous pouvez être amené à modifier la chaîne de connexion de votre client pour garantir que l’audit des données est correctement capturé.</span><span class="sxs-lookup"><span data-stu-id="ee815-146">If you are configuring Auditing for a database, you may need to alter the connection string of your client to ensure data auditing is correctly captured.</span></span> <span data-ttu-id="ee815-147">Consultez la rubrique [Modifier le nom de domaine complet du serveur dans la chaîne de connexion](sql-data-warehouse-auditing-downlevel-clients.md) , qui traite des connexions de client de niveau inférieur.</span><span class="sxs-lookup"><span data-stu-id="ee815-147">Check the [Modify Server FDQN in the connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="ee815-148">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee815-148">Click **OK**.</span></span>

## <span data-ttu-id="ee815-149"><a id="subheading-3"></a>Analyse des journaux et des rapports d’audit</span><span class="sxs-lookup"><span data-stu-id="ee815-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="ee815-150">Les journaux d’audit sont agrégés dans une collection de tables de stockage avec un préfixe **SQLDBAuditLogs** au sein du compte de stockage Azure que vous avez choisi lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="ee815-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="ee815-151">Vous pouvez afficher les fichiers journaux à l'aide d'un outil tel que l'<a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Explorateur de stockage Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="ee815-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="ee815-152">Un modèle de rapport de tableau de bord préconfiguré est disponible sous forme de <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">feuille de calcul Excel téléchargeable</a> afin de vous aider à analyser rapidement les données de journal.</span><span class="sxs-lookup"><span data-stu-id="ee815-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> to help you quickly analyze log data.</span></span> <span data-ttu-id="ee815-153">Pour utiliser le modèle sur vos journaux d'audit, il vous faut Excel 2013 ou une version ultérieure et Power Query, téléchargeable <a href="http://www.microsoft.com/download/details.aspx?id=39379">ici</a>.</span><span class="sxs-lookup"><span data-stu-id="ee815-153">To use the template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="ee815-154">Le modèle contient des données d'exemple fictives. Vous pouvez configurer Power Query de façon à ce qu'il importe votre journal d'audit directement à partir de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ee815-154">The template has fictional sample data in it, and you can set up Power Query to import your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="ee815-155"><a id="subheading-4"></a>Régénération des clés de stockage</span><span class="sxs-lookup"><span data-stu-id="ee815-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="ee815-156">Dans un environnement de production, vous allez probablement actualiser périodiquement vos clés de stockage.</span><span class="sxs-lookup"><span data-stu-id="ee815-156">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="ee815-157">Au moment d’actualiser vos clés, vous devez réenregistrer la stratégie.</span><span class="sxs-lookup"><span data-stu-id="ee815-157">When refreshing your keys, you need to save the policy.</span></span> <span data-ttu-id="ee815-158">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ee815-158">The process is as follows:</span></span>

1. <span data-ttu-id="ee815-159">Dans le panneau de configuration de l’audit (décrit plus haut dans la section de configuration de l’audit), faites passer la **clé d’accès du stockage** de *Principale* à *Secondaire*, puis choisissez **ENREGISTRER**.</span><span class="sxs-lookup"><span data-stu-id="ee815-159">In the auditing configuration blade (described above in the setup auditing section) switch the **Storage Access Key** from *Primary* to *Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="ee815-160">Revenez au volet de configuration du stockage, puis **régénérez** la *clé d’accès primaire*.</span><span class="sxs-lookup"><span data-stu-id="ee815-160">Go to the storage configuration blade and **regenerate** the *Primary Access Key*.</span></span>
3. <span data-ttu-id="ee815-161">Revenez au panneau de configuration de l’audit, faites passer la **clé d’accès du stockage** de *Secondaire* à *Principale*, puis cliquez sur **ENREGISTRER**.</span><span class="sxs-lookup"><span data-stu-id="ee815-161">Go back to the auditing configuration blade, switch the **Storage Access Key** from *Secondary* to *Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="ee815-162">Retournez dans l'interface utilisateur de stockage, puis **régénérez** la *clé d'accès secondaire* (en vue du prochain cycle d'actualisation des clés).</span><span class="sxs-lookup"><span data-stu-id="ee815-162">Go back to the storage UI and **regenerate** the *Secondary Access Key* (as preparation for the next keys refresh cycle.</span></span>

## <span data-ttu-id="ee815-163"><a id="subheading-5"></a>Automation (PowerShell / API REST)</span><span class="sxs-lookup"><span data-stu-id="ee815-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="ee815-164">Vous pouvez aussi configurer l’audit dans Azure SQL Data Warehouse en utilisant les outils d’automation suivants :</span><span class="sxs-lookup"><span data-stu-id="ee815-164">You can also configure auditing in Azure SQL Data Warehouse by using the following automation tools:</span></span>

* <span data-ttu-id="ee815-165">**Applets de commande PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="ee815-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="ee815-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="ee815-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="ee815-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="ee815-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="ee815-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="ee815-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="ee815-169">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="ee815-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="ee815-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="ee815-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="ee815-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="ee815-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="ee815-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="ee815-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

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