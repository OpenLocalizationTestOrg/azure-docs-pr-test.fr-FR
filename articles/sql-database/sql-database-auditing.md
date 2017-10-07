---
title: "aaaGet en main de l’audit de base de données SQL Azure | Documents Microsoft"
description: "Bien démarrer avec l’audit de bases de données SQL Azure"
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="67e15-103">Bien démarrer avec l’audit de bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="67e15-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="67e15-104">Audit de base de données SQL Azure effectue le suivi des événements de base de données et les écrit le journal d’audit de tooan dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="67e15-104">Azure SQL database auditing tracks database events and writes them tooan audit log in your Azure storage account.</span></span> <span data-ttu-id="67e15-105">Par ailleurs, l’audit :</span><span class="sxs-lookup"><span data-stu-id="67e15-105">Auditing also:</span></span>

* <span data-ttu-id="67e15-106">peut vous aider à respecter une conformité réglementaire, à comprendre l’activité de la base de données ainsi qu’à découvrir des discordances et anomalies susceptibles d’indiquer des problèmes pour l’entreprise ou des violations de la sécurité ;</span><span class="sxs-lookup"><span data-stu-id="67e15-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="67e15-107">Permet et facilite les normes de toocompliance d’adhésion, bien qu’il ne garantit pas la conformité.</span><span class="sxs-lookup"><span data-stu-id="67e15-107">Enables and facilitates adherence toocompliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="67e15-108">Pour plus d’informations sur Azure programmes que la conformité aux normes de prise en charge, consultez hello [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="67e15-108">For more information about Azure programs that support standards compliance, see hello [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="67e15-109"><a id="subheading-1"></a>Vue d’ensemble de l’audit be bases de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="67e15-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="67e15-110">Vous pouvez utiliser l’audit de bases de données SQL pour :</span><span class="sxs-lookup"><span data-stu-id="67e15-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="67e15-111">**La rétention** d’une piste d’audit d’événements sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="67e15-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="67e15-112">Vous pouvez définir des catégories de base de données actions toobe est auditée.</span><span class="sxs-lookup"><span data-stu-id="67e15-112">You can define categories of database actions toobe audited.</span></span>
* <span data-ttu-id="67e15-113">**La génération de rapports** sur les activités de la base de données.</span><span class="sxs-lookup"><span data-stu-id="67e15-113">**Report** on database activity.</span></span> <span data-ttu-id="67e15-114">Vous pouvez utiliser les rapports préconfigurés et un tooget de tableau de bord rapidement opérationnel avec activité et les rapports d’événements.</span><span class="sxs-lookup"><span data-stu-id="67e15-114">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="67e15-115">**L'analyse** des rapports.</span><span class="sxs-lookup"><span data-stu-id="67e15-115">**Analyze** reports.</span></span> <span data-ttu-id="67e15-116">Vous pouvez repérer les événements suspects, les activités inhabituelles et les tendances.</span><span class="sxs-lookup"><span data-stu-id="67e15-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="67e15-117">Vous pouvez configurer l’audit pour les différents types de catégories d’événements, comme expliqué dans hello [configurer l’audit pour votre base de données](#subheading-2) section.</span><span class="sxs-lookup"><span data-stu-id="67e15-117">You can configure auditing for different types of event categories, as explained in hello [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="67e15-118">Journaux d’audit sont écrites de stockage d’objets Blob tooAzure sur votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="67e15-118">Audit logs are written tooAzure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="67e15-119"><a id="subheading-8"></a>Définir une stratégie d’audit au niveau du serveur ou au niveau de la base de données</span><span class="sxs-lookup"><span data-stu-id="67e15-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="67e15-120">Une stratégie d’audit peut être définie pour une base de données spécifique ou en tant que stratégie de serveur par défaut :</span><span class="sxs-lookup"><span data-stu-id="67e15-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="67e15-121">Une stratégie de serveur s’applique tooall existantes et nouvelles bases de données sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="67e15-121">A server policy applies tooall existing and newly created databases on hello server.</span></span>

* <span data-ttu-id="67e15-122">Si *l’audit de blob serveur est activé*, il *applique toujours la base de données toohello* (autrement dit, base de données hello est audité), quelle que soit la base de données hello paramètres d’audit.</span><span class="sxs-lookup"><span data-stu-id="67e15-122">If *server blob auditing is enabled*, it *always applies toohello database* (that is, hello database will be audited), regardless of hello database auditing settings.</span></span>

* <span data-ttu-id="67e15-123">L’activation d’objet blob de l’audit sur base de données hello dans Ajout tooenabling sur le serveur de hello, sera *pas* remplacer ou modifier les paramètres d’audit d’objets blob hello serveur hello.</span><span class="sxs-lookup"><span data-stu-id="67e15-123">Enabling blob auditing on hello database, in addition tooenabling it on hello server, will *not* override or change any of hello settings of hello server blob auditing.</span></span> <span data-ttu-id="67e15-124">Les deux audits coexistent.</span><span class="sxs-lookup"><span data-stu-id="67e15-124">Both audits will exist side by side.</span></span> <span data-ttu-id="67e15-125">En d’autres termes, la base de données hello est audité deux fois en parallèle (une fois par la stratégie de serveur hello et qu’une seule fois par la stratégie de base de données hello).</span><span class="sxs-lookup"><span data-stu-id="67e15-125">In other words, hello database will be audited twice in parallel (once by hello server policy and once by hello database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="67e15-126">Vous devez éviter d’activer à la fois l’audit d’objets blob du serveur et l’audit d’objets blob de la base de données, sauf si :</span><span class="sxs-lookup"><span data-stu-id="67e15-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="67e15-127">Vous voulez toouse un autre *compte de stockage* ou *période de rétention* pour une base de données spécifique.</span><span class="sxs-lookup"><span data-stu-id="67e15-127">You want toouse a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="67e15-128">Vous souhaitez les catégories ou les types d’événements tooaudit pour une base de données spécifique qui diffèrent des types d’événements ou des catégories qui sont en cours d’audit pour les autres hello hello bases de données hello serveur.</span><span class="sxs-lookup"><span data-stu-id="67e15-128">You want tooaudit event types or categories for a specific database that differ from event types or categories that are being audited for hello rest of hello databases on hello server.</span></span> <span data-ttu-id="67e15-129">Par exemple, peut avoir des insertions de table qui doivent toobe auditer uniquement pour une base de données spécifique.</span><span class="sxs-lookup"><span data-stu-id="67e15-129">For example, you might have table inserts that need toobe audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="67e15-130">Dans le cas contraire, nous vous recommandons d’activer l’audit des objets blob d’uniquement au niveau du serveur et laissez hello au niveau de la base de données d’audit désactivé pour toutes les bases de données.</span><span class="sxs-lookup"><span data-stu-id="67e15-130">Otherwise, we recommended that you enable only server-level blob auditing and leave hello database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="67e15-131"><a id="subheading-2"></a>Configuration de l’audit pour votre base de données</span><span class="sxs-lookup"><span data-stu-id="67e15-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="67e15-132">Hello section suivante décrit la configuration hello d’audit à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="67e15-132">hello following section describes hello configuration of auditing using hello Azure portal.</span></span>

1. <span data-ttu-id="67e15-133">Accédez toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67e15-133">Go toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="67e15-134">Accédez toohello **paramètres** Panneau de hello SQL de base de données/serveur SQL server tooaudit.</span><span class="sxs-lookup"><span data-stu-id="67e15-134">Go toohello **Settings** blade of hello SQL database/SQL server you want tooaudit.</span></span> <span data-ttu-id="67e15-135">Bonjour **paramètres** panneau, sélectionnez **détection d’audit et de menaces**.</span><span class="sxs-lookup"><span data-stu-id="67e15-135">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="67e15-136"><a id="auditing-screenshot"></a>![Volet de navigation][1]</span><span class="sxs-lookup"><span data-stu-id="67e15-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="67e15-137">Si vous préférez tooset d’une stratégie d’audit de serveur (qui doit s’appliquer tooall existant et bases de données nouvellement créées sur ce serveur), vous pouvez sélectionner hello **afficher les paramètres du serveur** lien dans le panneau de l’audit de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="67e15-137">If you prefer tooset up a server auditing policy (which will apply tooall existing and newly created databases on this server), you can select hello **View server settings** link in hello database auditing blade.</span></span> <span data-ttu-id="67e15-138">Vous pouvez afficher ou modifier les paramètres d’audit de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="67e15-138">You can then view or modify hello server auditing settings.</span></span>

    ![Volet de navigation][2]
4. <span data-ttu-id="67e15-140">Si vous préférez tooenable blob l’audit de niveau de base de données de hello (dans tooor ajout au lieu de l’audit au niveau du serveur), **audit**, sélectionnez **ON**et pour **l’audit de type** , sélectionnez **Blob**.</span><span class="sxs-lookup"><span data-stu-id="67e15-140">If you prefer tooenable blob auditing on hello database level (in addition tooor instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="67e15-141">Si l’audit des objets blob de serveur est activé, audit de base de données configurée hello existe côte à côte avec l’audit du blob serveur hello.</span><span class="sxs-lookup"><span data-stu-id="67e15-141">If server blob auditing is enabled, hello database-configured audit will exist side by side with hello server blob audit.</span></span>  

    ![Volet de navigation][3]
5. <span data-ttu-id="67e15-143">tooopen hello **stockage des journaux d’Audit** panneau, sélectionnez **détails de stockage**.</span><span class="sxs-lookup"><span data-stu-id="67e15-143">tooopen hello **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="67e15-144">Sélectionnez le compte de stockage Azure hello où seront enregistrés les journaux et puis sélectionnez la période de rétention hello, après le hello anciens journaux seront supprimés.</span><span class="sxs-lookup"><span data-stu-id="67e15-144">Select hello Azure storage account where logs will be saved, and then select hello retention period, after which hello old logs will be deleted.</span></span> <span data-ttu-id="67e15-145">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="67e15-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="67e15-146">hello tooget parti hello audit des modèles de rapports, utilisez hello même compte de stockage pour toutes les bases de données audités.</span><span class="sxs-lookup"><span data-stu-id="67e15-146">tooget hello most out of hello auditing reports templates, use hello same storage account for all audited databases.</span></span> 

    <span data-ttu-id="67e15-147"><a id="storage-screenshot"></a>![Volet de navigation][4]</span><span class="sxs-lookup"><span data-stu-id="67e15-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="67e15-148">Si vous souhaitez que les événements audité de hello toocustomize, vous pouvez le faire via PowerShell ou hello API REST.</span><span class="sxs-lookup"><span data-stu-id="67e15-148">If you want toocustomize hello audited events, you can do this via PowerShell or hello REST API.</span></span> <span data-ttu-id="67e15-149">Pour plus d’informations, consultez hello [Automation (API PowerShell/REST)](#subheading-7) section.</span><span class="sxs-lookup"><span data-stu-id="67e15-149">For more details, see hello [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="67e15-150">Une fois que vous avez configuré vos paramètres d’audit, vous pouvez activer la nouvelle fonctionnalité de détection de menaces hello et configurer des alertes de sécurité des messages électroniques tooreceive.</span><span class="sxs-lookup"><span data-stu-id="67e15-150">After you've configured your auditing settings, you can turn on hello new threat detection feature and configure emails tooreceive security alerts.</span></span> <span data-ttu-id="67e15-151">La détection des menaces vous permet de recevoir des alertes proactives sur des activités anormales de la base de données qui peuvent indiquer des menaces de sécurité potentielles.</span><span class="sxs-lookup"><span data-stu-id="67e15-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="67e15-152">Pour plus d’informations, consultez [Bien démarrer avec la détection des menaces](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="67e15-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="67e15-153">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="67e15-153">Click **Save**.</span></span>





## <span data-ttu-id="67e15-154"><a id="subheading-3"></a>Analyse des journaux et des rapports d’audit</span><span class="sxs-lookup"><span data-stu-id="67e15-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="67e15-155">Journaux d’audit sont regroupées dans hello compte de stockage Azure que vous avez choisi lors de l’installation.</span><span class="sxs-lookup"><span data-stu-id="67e15-155">Audit logs are aggregated in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="67e15-156">Vous pouvez explorer les journaux d’audit avec un outil comme [l’Explorateur de stockage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="67e15-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="67e15-157">Les journaux d’audit d’objets blob sont enregistrés sous la forme d’une collection de fichiers d’objets blob dans un conteneur nommé **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="67e15-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="67e15-158">Pour plus d’informations sur la hiérarchie hello du dossier de stockage des journaux hello blob d’audit, conventions d’affectation de noms d’objet blob et le format de journal, consultez hello [référence de la Format de journal d’Audit Blob (téléchargement de fichier .docx)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="67e15-158">For further details about hello hierarchy of hello blob audit logs storage folder, blob naming conventions, and log format, see hello [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="67e15-159">Il existe plusieurs méthodes que vous pouvez utiliser blob tooview les journaux d’audit :</span><span class="sxs-lookup"><span data-stu-id="67e15-159">There are several methods you can use tooview blob auditing logs:</span></span>

* <span data-ttu-id="67e15-160">Hello d’utilisation [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67e15-160">Use hello [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="67e15-161">Base de données appropriée hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="67e15-161">Open hello relevant database.</span></span> <span data-ttu-id="67e15-162">Haut de hello AT de la base de données hello **détection d’audit et de menaces** panneau, cliquez sur **afficher les journaux d’audit**.</span><span class="sxs-lookup"><span data-stu-id="67e15-162">At hello top of hello database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Volet de navigation][7]

    <span data-ttu-id="67e15-164">Un **enregistrements d’Audit** s’ouvre le panneau, à partir de laquelle vous serez en mesure de tooview hello journaux.</span><span class="sxs-lookup"><span data-stu-id="67e15-164">An **Audit records** blade opens, from which you'll be able tooview hello logs.</span></span>

    - <span data-ttu-id="67e15-165">Vous pouvez afficher des dates spécifiques en cliquant sur **filtre** haut hello hello **enregistrements d’Audit** panneau.</span><span class="sxs-lookup"><span data-stu-id="67e15-165">You can view specific dates by clicking **Filter** at hello top of hello **Audit records** blade.</span></span>
    - <span data-ttu-id="67e15-166">Vous pouvez basculer entre les enregistrements d’audit qui ont été créés par un audit de stratégie de base de données ou de stratégie de serveur.</span><span class="sxs-lookup"><span data-stu-id="67e15-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Volet de navigation][8]

* <span data-ttu-id="67e15-168">Utilisez la fonction du système hello **sys.fn_get_audit_file** données du journal d’audit (T-SQL) tooreturn hello sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="67e15-168">Use hello system function **sys.fn_get_audit_file** (T-SQL) tooreturn hello audit log data in tabular format.</span></span> <span data-ttu-id="67e15-169">Pour plus d’informations sur l’utilisation de cette fonction, consultez hello [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="67e15-169">For more information on using this function, see hello [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="67e15-170">Utilisez **Fusionner les fichiers d’audit** dans SQL Server Management Studio (à partir de SSMS 17) :</span><span class="sxs-lookup"><span data-stu-id="67e15-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="67e15-171">Dans le menu SSMS hello, sélectionnez **fichier** > **ouvrir** > **fusionner les fichiers d’Audit**.</span><span class="sxs-lookup"><span data-stu-id="67e15-171">From hello SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Volet de navigation][9]
    2. <span data-ttu-id="67e15-173">Hello **ajouter des fichiers d’Audit** boîte de dialogue s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="67e15-173">hello **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="67e15-174">Sélectionnez une des hello **ajouter** options pour choisir si des fichiers d’audit de toomerge à partir d’une variable locale du disque ou les importer depuis le stockage Azure (vous sera nécessaire tooprovide vos informations de stockage Azure et de la clé de compte).</span><span class="sxs-lookup"><span data-stu-id="67e15-174">Select one of hello **Add** options to choose whether toomerge audit files from a local disk or import them from Azure Storage (you will be required tooprovide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="67e15-175">Une fois tous les fichiers toomerge ont été ajoutés, cliquez sur **OK** opération de fusion toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="67e15-175">After all files toomerge have been added, click **OK** toocomplete hello merge operation.</span></span>

    4. <span data-ttu-id="67e15-176">Hello fusionné s’ouvre dans SSMS, où vous pouvez afficher et analyser, ainsi que des exportation il tooan XEL ou CSV tooa ou fichier de la table.</span><span class="sxs-lookup"><span data-stu-id="67e15-176">hello merged file opens in SSMS, where you can view and analyze it, as well as export it tooan XEL or CSV file or tooa table.</span></span>

* <span data-ttu-id="67e15-177">Hello d’utilisation [synchronisation application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) que nous avons créés.</span><span class="sxs-lookup"><span data-stu-id="67e15-177">Use hello [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="67e15-178">Il s’exécute dans Azure et utilise l’Analytique des journaux Operations Management Suite (OMS) publique API toopush SQL des journaux d’audit dans OMS.</span><span class="sxs-lookup"><span data-stu-id="67e15-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs toopush SQL audit logs into OMS.</span></span> <span data-ttu-id="67e15-179">synchroniser l’application Hello transmet les journaux d’audit SQL dans l’Analytique des journaux OMS pour la consommation via le tableau de bord hello Analytique des journaux OMS.</span><span class="sxs-lookup"><span data-stu-id="67e15-179">hello sync application pushes SQL audit logs into OMS Log Analytics for consumption via hello OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="67e15-180">Utilisez Power BI.</span><span class="sxs-lookup"><span data-stu-id="67e15-180">Use Power BI.</span></span> <span data-ttu-id="67e15-181">Vous pouvez afficher et analyser les données du journal d’audit dans Power BI.</span><span class="sxs-lookup"><span data-stu-id="67e15-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="67e15-182">Explorez [Power BI et accédez à un modèle téléchargeable](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="67e15-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="67e15-183">Téléchargez les fichiers journaux à partir de votre conteneur d’objets blob de stockage Azure via le portail de hello ou à l’aide d’un outil tel que [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="67e15-183">Download log files from your Azure Storage blob container via hello portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="67e15-184">Après avoir téléchargé un fichier journal localement, vous pouvez double-cliquer sur hello tooopen de fichier, afficher et analyser les journaux hello dans SSMS.</span><span class="sxs-lookup"><span data-stu-id="67e15-184">After you have downloaded a log file locally, you can double-click hello file tooopen, view, and analyze hello logs in SSMS.</span></span>
    * <span data-ttu-id="67e15-185">Vous pouvez également télécharger plusieurs fichiers simultanément avec l’Explorateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="67e15-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="67e15-186">Cliquez sur un sous-dossier spécifique (par exemple, un sous-dossier qui inclut tous les fichiers journaux pour une date spécifique) et sélectionnez **enregistrer en tant que** toosave dans un dossier local.</span><span class="sxs-lookup"><span data-stu-id="67e15-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** toosave in a local folder.</span></span>

* <span data-ttu-id="67e15-187">Autres méthodes :</span><span class="sxs-lookup"><span data-stu-id="67e15-187">Additional methods:</span></span>
   * <span data-ttu-id="67e15-188">Après le téléchargement de plusieurs fichiers (ou un sous-dossier qui comprend des fichiers journaux pour une journée entière, comme indiqué dans l’élément précédent de hello dans cette liste), vous pouvez les fusionner localement comme décrit dans les instructions de fichiers d’Audit de fusion SSMS hello décrites précédemment.</span><span class="sxs-lookup"><span data-stu-id="67e15-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in hello previous item in this list), you can merge them locally as described in hello SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="67e15-189">Affichez des journaux d’audit d’objets blob par programmation :</span><span class="sxs-lookup"><span data-stu-id="67e15-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="67e15-190">Hello d’utilisation [lecteur d’événements étendus](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) bibliothèque c#.</span><span class="sxs-lookup"><span data-stu-id="67e15-190">Use hello [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="67e15-191">[Interrogez des fichiers d’événements étendus](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="67e15-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="67e15-192"><a id="subheading-5"></a>Pratiques de production</span><span class="sxs-lookup"><span data-stu-id="67e15-192"><a id="subheading-5"></a>Production practices</span></span>
<!--hello description in this section refers toopreceding screen captures.-->

### <span data-ttu-id="67e15-193"><a id="subheading-6">Audit des bases de données géorépliquées</a></span><span class="sxs-lookup"><span data-stu-id="67e15-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="67e15-194">Lorsque vous utilisez des bases de données répliquées, il est possible tooset l’audit sur la base de données primaire hello, base de données secondaire hello ou les deux, selon le type de l’audit hello.</span><span class="sxs-lookup"><span data-stu-id="67e15-194">When you use geo-replicated databases, it is possible tooset up auditing on either hello primary database, hello secondary database, or both, depending on hello audit type.</span></span>

<span data-ttu-id="67e15-195">Suivez ces instructions (n’oubliez pas que l’audit des objets blob peut être activée ou désactivée uniquement à partir des paramètres d’audit de la base de données hello principale) :</span><span class="sxs-lookup"><span data-stu-id="67e15-195">Follow these instructions (remember that blob auditing can be turned on or off only from hello primary database auditing settings):</span></span>

* <span data-ttu-id="67e15-196">**Base de données primaire**.</span><span class="sxs-lookup"><span data-stu-id="67e15-196">**Primary database**.</span></span> <span data-ttu-id="67e15-197">Activer le blob l’audit sur le serveur de hello ou sur une base de données hello lui-même, comme décrit dans hello [configurer l’audit pour votre base de données](#subheading-2) section.</span><span class="sxs-lookup"><span data-stu-id="67e15-197">Turn on blob auditing, either on hello server or on hello database itself, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="67e15-198">**Base de données secondaire**.</span><span class="sxs-lookup"><span data-stu-id="67e15-198">**Secondary database**.</span></span> <span data-ttu-id="67e15-199">Activer l’audit de l’objet blob sur la base de données primaire hello, comme décrit dans hello [configurer l’audit pour votre base de données](#subheading-2) section.</span><span class="sxs-lookup"><span data-stu-id="67e15-199">Turn on blob auditing on hello primary database, as described in hello [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="67e15-200">Audit de l’objet BLOB doit être activée sur hello *base de données primaire elle-même*, non par serveur hello.</span><span class="sxs-lookup"><span data-stu-id="67e15-200">Blob auditing must be enabled on hello *primary database itself*, not hello server.</span></span>
   * <span data-ttu-id="67e15-201">Une fois que l’objet blob l’audit est activé sur la base de données primaire hello, il est également activé sur la base de données secondaire hello.</span><span class="sxs-lookup"><span data-stu-id="67e15-201">After blob auditing is enabled on hello primary database, it will also become enabled on hello secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="67e15-202">Par défaut, les paramètres de stockage hello pour la base de données secondaire hello sera identique toothose de base de données primaire hello, à l’origine du trafic entre-régionale.</span><span class="sxs-lookup"><span data-stu-id="67e15-202">By default, hello storage settings for hello secondary database will be identical toothose of hello primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="67e15-203">Vous pouvez éviter cela en activant l’audit des objets blob sur le serveur secondaire de hello et la configuration du stockage local dans les paramètres de stockage de serveur secondaire hello.</span><span class="sxs-lookup"><span data-stu-id="67e15-203">You can avoid this by enabling blob auditing on hello secondary server and configuring local storage in hello secondary server storage settings.</span></span> <span data-ttu-id="67e15-204">Cela remplacera l’emplacement de stockage hello pour la base de données secondaire hello et résultats dans chaque base de données de l’enregistrement de son stockage toolocal de journaux d’audit.</span><span class="sxs-lookup"><span data-stu-id="67e15-204">This will override hello storage location for hello secondary database and result in each database saving its audit logs toolocal storage.</span></span>  
<br>

### <span data-ttu-id="67e15-205"><a id="subheading-6">Régénération des clés de stockage</a></span><span class="sxs-lookup"><span data-stu-id="67e15-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="67e15-206">En production, vous êtes probablement toorefresh votre stockage de clés périodiquement.</span><span class="sxs-lookup"><span data-stu-id="67e15-206">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="67e15-207">Lors de l’actualisation de vos clés, vous devez la stratégie d’audit tooresave hello.</span><span class="sxs-lookup"><span data-stu-id="67e15-207">When refreshing your keys, you need tooresave hello auditing policy.</span></span> <span data-ttu-id="67e15-208">processus de Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="67e15-208">hello process is as follows:</span></span>

1. <span data-ttu-id="67e15-209">Ouvrez hello **détails de stockage** panneau.</span><span class="sxs-lookup"><span data-stu-id="67e15-209">Open hello **Storage Details** blade.</span></span> <span data-ttu-id="67e15-210">Bonjour **clé d’accès de stockage** boîte, sélectionnez **secondaire**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="67e15-210">In hello **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="67e15-211">Puis cliquez sur **enregistrer** haut hello hello l’audit du Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="67e15-211">Then click **Save** at hello top of hello auditing configuration blade.</span></span>

    ![Volet de navigation][5]
2. <span data-ttu-id="67e15-213">Atteindre le panneau de configuration de stockage toohello et régénérer la clé d’accès primaire hello.</span><span class="sxs-lookup"><span data-stu-id="67e15-213">Go toohello storage configuration blade and regenerate hello primary access key.</span></span>

    ![Volet de navigation][6]
3. <span data-ttu-id="67e15-215">Revenir en arrière toohello l’audit du Panneau de configuration, basculez de clé d’accès de stockage hello de tooprimary secondaire, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="67e15-215">Go back toohello auditing configuration blade, switch hello storage access key from secondary tooprimary, and then click **OK**.</span></span> <span data-ttu-id="67e15-216">Puis cliquez sur **enregistrer** haut hello hello l’audit du Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="67e15-216">Then click **Save** at hello top of hello auditing configuration blade.</span></span>
4. <span data-ttu-id="67e15-217">Retournez dans Panneau de configuration de stockage toohello et la clé d’accès secondaire hello régénérer (en vue de cycle d’actualisation de la clé suivante hello).</span><span class="sxs-lookup"><span data-stu-id="67e15-217">Go back toohello storage configuration blade and regenerate hello secondary access key (in preparation for hello next key's refresh cycle).</span></span>

## <span data-ttu-id="67e15-218"><a id="subheading-7"></a>Automation (PowerShell / API REST)</span><span class="sxs-lookup"><span data-stu-id="67e15-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="67e15-219">Vous pouvez également configurer l’audit dans la base de données SQL Azure à l’aide de hello suivant des outils d’automatisation :</span><span class="sxs-lookup"><span data-stu-id="67e15-219">You can also configure auditing in Azure SQL Database by using hello following automation tools:</span></span>

* <span data-ttu-id="67e15-220">**Applets de commande PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="67e15-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="67e15-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="67e15-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="67e15-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="67e15-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="67e15-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="67e15-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="67e15-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="67e15-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="67e15-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="67e15-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="67e15-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="67e15-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="67e15-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="67e15-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="67e15-228">Pour obtenir un exemple de script, consultez [Configurer l’audit et la détection des menaces avec PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="67e15-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="67e15-229">**API REST - Audit d’objets blob** :</span><span class="sxs-lookup"><span data-stu-id="67e15-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="67e15-230">Create or Update Database Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="67e15-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="67e15-231">Create or Update Server Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="67e15-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="67e15-232">Get Database Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="67e15-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="67e15-233">Get Server Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="67e15-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="67e15-234">Get Server Blob Auditing Operation Result</span><span class="sxs-lookup"><span data-stu-id="67e15-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
