---
title: "Bien démarrer avec l’audit de bases de données SQL Azure | Microsoft Docs"
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
ms.openlocfilehash: f4324a59b5fa4c2e1ab5b1d7fc7e5fe986ea80f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-auditing"></a><span data-ttu-id="58a2c-103">Bien démarrer avec l’audit de bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="58a2c-103">Get started with SQL database auditing</span></span>
<span data-ttu-id="58a2c-104">L’audit de bases de données SQL Azure suit les événements de base de données et les écrit dans un journal d’audit dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="58a2c-104">Azure SQL database auditing tracks database events and writes them to an audit log in your Azure storage account.</span></span> <span data-ttu-id="58a2c-105">Par ailleurs, l’audit :</span><span class="sxs-lookup"><span data-stu-id="58a2c-105">Auditing also:</span></span>

* <span data-ttu-id="58a2c-106">peut vous aider à respecter une conformité réglementaire, à comprendre l’activité de la base de données ainsi qu’à découvrir des discordances et anomalies susceptibles d’indiquer des problèmes pour l’entreprise ou des violations de la sécurité ;</span><span class="sxs-lookup"><span data-stu-id="58a2c-106">Helps you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

* <span data-ttu-id="58a2c-107">permet et facilite le respect de normes de conformité, même s’il ne garantit pas cette conformité.</span><span class="sxs-lookup"><span data-stu-id="58a2c-107">Enables and facilitates adherence to compliance standards, although it doesn't guarantee compliance.</span></span> <span data-ttu-id="58a2c-108">Pour plus d’informations sur les programmes Azure prenant en charge la conformité aux normes, voir le [Centre de confidentialité Azure](https://azure.microsoft.com/support/trust-center/compliance/).</span><span class="sxs-lookup"><span data-stu-id="58a2c-108">For more information about Azure programs that support standards compliance, see the [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).</span></span>


## <span data-ttu-id="58a2c-109"><a id="subheading-1"></a>Vue d’ensemble de l’audit be bases de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="58a2c-109"><a id="subheading-1"></a>Azure SQL database auditing overview</span></span>
<span data-ttu-id="58a2c-110">Vous pouvez utiliser l’audit de bases de données SQL pour :</span><span class="sxs-lookup"><span data-stu-id="58a2c-110">You can use SQL database auditing to:</span></span>


* <span data-ttu-id="58a2c-111">**La rétention** d’une piste d’audit d’événements sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="58a2c-111">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="58a2c-112">Définissez les catégories d'actions et d'événements de base de données à auditer.</span><span class="sxs-lookup"><span data-stu-id="58a2c-112">You can define categories of database actions to be audited.</span></span>
* <span data-ttu-id="58a2c-113">**La génération de rapports** sur les activités de la base de données.</span><span class="sxs-lookup"><span data-stu-id="58a2c-113">**Report** on database activity.</span></span> <span data-ttu-id="58a2c-114">Vous pouvez utiliser des rapports préconfigurés et un tableau de bord pour une prise en main rapide de la génération de rapports d'activités et d'événements.</span><span class="sxs-lookup"><span data-stu-id="58a2c-114">You can use preconfigured reports and a dashboard to get started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="58a2c-115">**L'analyse** des rapports.</span><span class="sxs-lookup"><span data-stu-id="58a2c-115">**Analyze** reports.</span></span> <span data-ttu-id="58a2c-116">Vous pouvez repérer les événements suspects, les activités inhabituelles et les tendances.</span><span class="sxs-lookup"><span data-stu-id="58a2c-116">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="58a2c-117">Vous pouvez configurer l’audit pour différents types de catégories d’événements, comme expliqué dans la section [Configuration de l’audit de votre base de données](#subheading-2).</span><span class="sxs-lookup"><span data-stu-id="58a2c-117">You can configure auditing for different types of event categories, as explained in the [Set up auditing for your database](#subheading-2) section.</span></span>

<span data-ttu-id="58a2c-118">Les journaux d’audit sont écrits dans le stockage Blob Azure avec votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="58a2c-118">Audit logs are written to Azure Blob storage on your Azure subscription.</span></span>


## <span data-ttu-id="58a2c-119"><a id="subheading-8"></a>Définir une stratégie d’audit au niveau du serveur ou au niveau de la base de données</span><span class="sxs-lookup"><span data-stu-id="58a2c-119"><a id="subheading-8"></a>Define server-level vs. database-level auditing policy</span></span>

<span data-ttu-id="58a2c-120">Une stratégie d’audit peut être définie pour une base de données spécifique ou en tant que stratégie de serveur par défaut :</span><span class="sxs-lookup"><span data-stu-id="58a2c-120">An auditing policy can be defined for a specific database or as a default server policy:</span></span>

* <span data-ttu-id="58a2c-121">Une stratégie de serveur s’applique aux bases de données existantes et à celles qui sont nouvellement créées sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="58a2c-121">A server policy applies to all existing and newly created databases on the server.</span></span>

* <span data-ttu-id="58a2c-122">Si *l’audit d’objets blob du serveur est activé*, il *s’applique toujours à la base de données* (autrement dit, la base de données sera auditée), indépendamment des paramètres d’audit de la base de données.</span><span class="sxs-lookup"><span data-stu-id="58a2c-122">If *server blob auditing is enabled*, it *always applies to the database* (that is, the database will be audited), regardless of the database auditing settings.</span></span>

* <span data-ttu-id="58a2c-123">L’activation de l’audit d’objets blob sur la base de données, en plus de son activation sur le serveur, *ne* remplace ni ne modifie aucun des paramètres de l’audit d’objets blob du serveur.</span><span class="sxs-lookup"><span data-stu-id="58a2c-123">Enabling blob auditing on the database, in addition to enabling it on the server, will *not* override or change any of the settings of the server blob auditing.</span></span> <span data-ttu-id="58a2c-124">Les deux audits coexistent.</span><span class="sxs-lookup"><span data-stu-id="58a2c-124">Both audits will exist side by side.</span></span> <span data-ttu-id="58a2c-125">En d’autres termes, la base de données est auditée deux fois en parallèle (une fois par la stratégie du serveur et une autre fois par la stratégie de la base de données).</span><span class="sxs-lookup"><span data-stu-id="58a2c-125">In other words, the database will be audited twice in parallel (once by the server policy and once by the database policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="58a2c-126">Vous devez éviter d’activer à la fois l’audit d’objets blob du serveur et l’audit d’objets blob de la base de données, sauf si :</span><span class="sxs-lookup"><span data-stu-id="58a2c-126">You should avoid enabling both server blob auditing and database blob auditing together, unless:</span></span>
    > * <span data-ttu-id="58a2c-127">Vous voulez utiliser un autre *compte de stockage* ou une autre *période de rétention* pour une base de données spécifique.</span><span class="sxs-lookup"><span data-stu-id="58a2c-127">You want to use a different *storage account* or *retention period* for a specific database.</span></span>
    > * <span data-ttu-id="58a2c-128">Vous souhaitez auditer des types ou catégories d’événements pour une base de données spécifique différents des types ou catégories d’événements qui sont audités pour les autres bases de données sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="58a2c-128">You want to audit event types or categories for a specific database that differ from event types or categories that are being audited for the rest of the databases on the server.</span></span> <span data-ttu-id="58a2c-129">Par exemple, il est possible que des insertions de table doivent être auditées uniquement pour une base de données spécifique.</span><span class="sxs-lookup"><span data-stu-id="58a2c-129">For example, you might have table inserts that need to be audited only for a specific database.</span></span>
   > 
   > <span data-ttu-id="58a2c-130">Sinon, nous vous recommandons d’activer uniquement l’audit d’objets blob au niveau du serveur et de laisser l’audit au niveau de la base de données désactivé pour toutes les bases de données.</span><span class="sxs-lookup"><span data-stu-id="58a2c-130">Otherwise, we recommended that you enable only server-level blob auditing and leave the database-level auditing disabled for all databases.</span></span>


## <span data-ttu-id="58a2c-131"><a id="subheading-2"></a>Configuration de l’audit pour votre base de données</span><span class="sxs-lookup"><span data-stu-id="58a2c-131"><a id="subheading-2"></a>Set up auditing for your database</span></span>
<span data-ttu-id="58a2c-132">La section suivante décrit la configuration de l’audit à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="58a2c-132">The following section describes the configuration of auditing using the Azure portal.</span></span>

1. <span data-ttu-id="58a2c-133">Accédez au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="58a2c-133">Go to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="58a2c-134">Accédez au panneau **Paramètres** de la base de données/du serveur SQL que vous voulez auditer.</span><span class="sxs-lookup"><span data-stu-id="58a2c-134">Go to the **Settings** blade of the SQL database/SQL server you want to audit.</span></span> <span data-ttu-id="58a2c-135">Dans le panneau **Paramètres**, sélectionnez **Audit et détection des menaces**.</span><span class="sxs-lookup"><span data-stu-id="58a2c-135">In the **Settings** blade, select **Auditing & Threat detection**.</span></span>

    <span data-ttu-id="58a2c-136"><a id="auditing-screenshot"></a> ![Volet de navigation][1]</span><span class="sxs-lookup"><span data-stu-id="58a2c-136"><a id="auditing-screenshot"></a> ![Navigation pane][1]</span></span>
3. <span data-ttu-id="58a2c-137">Si vous préférez configurer une stratégie d’audit de serveur (qui s’appliquera aux bases de données existantes et nouvellement créées sur ce serveur), vous pouvez sélectionner le lien **Afficher les paramètres du serveur** dans le panneau d’audit de la base de données.</span><span class="sxs-lookup"><span data-stu-id="58a2c-137">If you prefer to set up a server auditing policy (which will apply to all existing and newly created databases on this server), you can select the **View server settings** link in the database auditing blade.</span></span> <span data-ttu-id="58a2c-138">Vous pouvez alors afficher ou modifier les paramètres d’audit du serveur.</span><span class="sxs-lookup"><span data-stu-id="58a2c-138">You can then view or modify the server auditing settings.</span></span>

    ![Volet de navigation][2]
4. <span data-ttu-id="58a2c-140">Si vous préférez activer l’audit d’objets blob au niveau de la base de données (en plus ou à la place de l’audit au niveau du serveur) : pour **Audit**, sélectionnez **ACTIVÉ** et pour **Type d’audit**, sélectionnez **Objet blob**.</span><span class="sxs-lookup"><span data-stu-id="58a2c-140">If you prefer to enable blob auditing on the database level (in addition to or instead of server-level auditing), for **Auditing**, select **ON**, and for **Auditing type**, select  **Blob**.</span></span>

    <span data-ttu-id="58a2c-141">Si l’audit d’objets blob du serveur est activé, l’audit configuré pour la base de données coexiste avec celui-ci.</span><span class="sxs-lookup"><span data-stu-id="58a2c-141">If server blob auditing is enabled, the database-configured audit will exist side by side with the server blob audit.</span></span>  

    ![Volet de navigation][3]
5. <span data-ttu-id="58a2c-143">Pour ouvrir le panneau **Stockage des journaux d’audit**, sélectionnez **Détails du stockage**.</span><span class="sxs-lookup"><span data-stu-id="58a2c-143">To open the **Audit Logs Storage** blade, select **Storage Details**.</span></span> <span data-ttu-id="58a2c-144">Sélectionnez le compte de stockage Azure où les journaux sont enregistrés, puis la période de rétention après laquelle les anciens journaux sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="58a2c-144">Select the Azure storage account where logs will be saved, and then select the retention period, after which the old logs will be deleted.</span></span> <span data-ttu-id="58a2c-145">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="58a2c-145">Then click **OK**.</span></span> 
   >[!TIP] 
   ><span data-ttu-id="58a2c-146">Pour tirer le meilleur parti des modèles des rapports d’audit, utilisez le même compte de stockage pour toutes les bases de données auditées.</span><span class="sxs-lookup"><span data-stu-id="58a2c-146">To get the most out of the auditing reports templates, use the same storage account for all audited databases.</span></span> 

    <span data-ttu-id="58a2c-147"><a id="storage-screenshot"></a> ![Volet de navigation][4]</span><span class="sxs-lookup"><span data-stu-id="58a2c-147"><a id="storage-screenshot"></a> ![Navigation pane][4]</span></span>
6. <span data-ttu-id="58a2c-148">Si vous souhaitez personnaliser les événements audités, vous pouvez le faire avec PowerShell ou l’API REST.</span><span class="sxs-lookup"><span data-stu-id="58a2c-148">If you want to customize the audited events, you can do this via PowerShell or the REST API.</span></span> <span data-ttu-id="58a2c-149">Pour plus d’informations, consultez la section [Automation (PowerShell / API REST)](#subheading-7).</span><span class="sxs-lookup"><span data-stu-id="58a2c-149">For more details, see the [Automation (PowerShell/REST API)](#subheading-7) section.</span></span>
7. <span data-ttu-id="58a2c-150">Une fois que vous avez configuré vos paramètres d’audit, vous pouvez activer la nouvelle fonctionnalité de détection des menaces et configurer les adresses e-mail de réception des alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="58a2c-150">After you've configured your auditing settings, you can turn on the new threat detection feature and configure emails to receive security alerts.</span></span> <span data-ttu-id="58a2c-151">La détection des menaces vous permet de recevoir des alertes proactives sur des activités anormales de la base de données qui peuvent indiquer des menaces de sécurité potentielles.</span><span class="sxs-lookup"><span data-stu-id="58a2c-151">When you use threat detection, you receive proactive alerts on anomalous database activities that can indicate potential security threats.</span></span> <span data-ttu-id="58a2c-152">Pour plus d’informations, consultez [Bien démarrer avec la détection des menaces](sql-database-threat-detection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="58a2c-152">For more details, see [Getting started with threat detection](sql-database-threat-detection-get-started.md).</span></span>
8. <span data-ttu-id="58a2c-153">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="58a2c-153">Click **Save**.</span></span>





## <span data-ttu-id="58a2c-154"><a id="subheading-3"></a>Analyse des journaux et des rapports d’audit</span><span class="sxs-lookup"><span data-stu-id="58a2c-154"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="58a2c-155">Les journaux d’audit sont agrégés dans le compte de stockage Azure choisi lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="58a2c-155">Audit logs are aggregated in the Azure storage account you chose during setup.</span></span> <span data-ttu-id="58a2c-156">Vous pouvez explorer les journaux d’audit avec un outil comme [l’Explorateur de stockage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="58a2c-156">You can explore audit logs by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="58a2c-157">Les journaux d’audit d’objets blob sont enregistrés sous la forme d’une collection de fichiers d’objets blob dans un conteneur nommé **sqldbauditlogs**.</span><span class="sxs-lookup"><span data-stu-id="58a2c-157">Blob auditing logs are saved as a collection of blob files within a container named **sqldbauditlogs**.</span></span>

<span data-ttu-id="58a2c-158">Pour plus d’informations sur la hiérarchie des dossiers de stockage des journaux d’audit d’objets blob, sur les conventions de noms des objets blob et sur le format des journaux, consultez les [informations de référence sur le format des journaux d’audit d’objets blob (téléchargement de fichier .docx)](https://go.microsoft.com/fwlink/?linkid=829599).</span><span class="sxs-lookup"><span data-stu-id="58a2c-158">For further details about the hierarchy of the blob audit logs storage folder, blob naming conventions, and log format, see the [Blob Audit Log Format Reference (.docx file download)](https://go.microsoft.com/fwlink/?linkid=829599).</span></span>

<span data-ttu-id="58a2c-159">Plusieurs méthodes vous permettent d’afficher des journaux d’audit d’objets blob :</span><span class="sxs-lookup"><span data-stu-id="58a2c-159">There are several methods you can use to view blob auditing logs:</span></span>

* <span data-ttu-id="58a2c-160">Utilisez le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="58a2c-160">Use the [Azure portal](https://portal.azure.com).</span></span>  <span data-ttu-id="58a2c-161">Ouvrez la base de données appropriée.</span><span class="sxs-lookup"><span data-stu-id="58a2c-161">Open the relevant database.</span></span> <span data-ttu-id="58a2c-162">En haut du panneau **Audit et détection des menaces** de la base de données, cliquez sur **Afficher les journaux d’audit**.</span><span class="sxs-lookup"><span data-stu-id="58a2c-162">At the top of the database's **Auditing & Threat detection** blade, click **View audit logs**.</span></span>

    ![Volet de navigation][7]

    <span data-ttu-id="58a2c-164">Un panneau **Enregistrements d’audit** s’ouvre, dans lequel s’affichent les journaux.</span><span class="sxs-lookup"><span data-stu-id="58a2c-164">An **Audit records** blade opens, from which you'll be able to view the logs.</span></span>

    - <span data-ttu-id="58a2c-165">Vous pouvez afficher des dates spécifiques en cliquant sur **Filtrer** en haut du panneau **Enregistrements d’audit**.</span><span class="sxs-lookup"><span data-stu-id="58a2c-165">You can view specific dates by clicking **Filter** at the top of the **Audit records** blade.</span></span>
    - <span data-ttu-id="58a2c-166">Vous pouvez basculer entre les enregistrements d’audit qui ont été créés par un audit de stratégie de base de données ou de stratégie de serveur.</span><span class="sxs-lookup"><span data-stu-id="58a2c-166">You can switch between audit records that were created by a server policy or database policy audit.</span></span>

       ![Volet de navigation][8]

* <span data-ttu-id="58a2c-168">Utilisez la fonction système **sys.fn_get_audit_file** (T-SQL) pour retourner les données du journal d’audit sous un format tabulaire.</span><span class="sxs-lookup"><span data-stu-id="58a2c-168">Use the system function **sys.fn_get_audit_file** (T-SQL) to return the audit log data in tabular format.</span></span> <span data-ttu-id="58a2c-169">Pour plus d’informations sur l’utilisation de cette fonction, consultez la [documentation sys.fn_get_audit_file](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="58a2c-169">For more information on using this function, see the [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).</span></span>


* <span data-ttu-id="58a2c-170">Utilisez **Fusionner les fichiers d’audit** dans SQL Server Management Studio (à partir de SSMS 17) :</span><span class="sxs-lookup"><span data-stu-id="58a2c-170">Use **Merge Audit Files** in SQL Server Management Studio (starting with SSMS 17):</span></span>  
    1. <span data-ttu-id="58a2c-171">Dans le menu SSMS, sélectionnez **Fichier** > **Ouvrir** > **Fusionner les fichiers d’audit**.</span><span class="sxs-lookup"><span data-stu-id="58a2c-171">From the SSMS menu, select **File** > **Open** > **Merge Audit Files**.</span></span>

        ![Volet de navigation][9]
    2. <span data-ttu-id="58a2c-173">La boîte de dialogue **Ajouter des fichiers d’audit** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="58a2c-173">The **Add Audit Files** dialog box opens.</span></span> <span data-ttu-id="58a2c-174">Sélectionnez l’une des options **Ajouter** pour choisir de fusionner les fichiers d’audit à partir d’un disque local ou de les importer à partir du stockage Azure (vous devrez fournir vos informations de stockage Azure et la clé de compte).</span><span class="sxs-lookup"><span data-stu-id="58a2c-174">Select one of the **Add** options to choose whether to merge audit files from a local disk or import them from Azure Storage (you will be required to provide your Azure Storage details and account key).</span></span>

    3. <span data-ttu-id="58a2c-175">Une fois que tous les fichiers à fusionner ont été ajoutés, cliquez sur **OK** pour terminer l’opération de fusion.</span><span class="sxs-lookup"><span data-stu-id="58a2c-175">After all files to merge have been added, click **OK** to complete the merge operation.</span></span>

    4. <span data-ttu-id="58a2c-176">Le fichier fusionné s’ouvre dans SSMS, où vous pouvez l’afficher et l’analyser, ainsi que l’exporter vers un fichier XEL ou CSV, ou une table.</span><span class="sxs-lookup"><span data-stu-id="58a2c-176">The merged file opens in SSMS, where you can view and analyze it, as well as export it to an XEL or CSV file or to a table.</span></span>

* <span data-ttu-id="58a2c-177">Utilisez l’[application de synchronisation](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) que nous avons créée.</span><span class="sxs-lookup"><span data-stu-id="58a2c-177">Use the [sync application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) that we have created.</span></span> <span data-ttu-id="58a2c-178">Elle s’exécute dans Azure et utilise les API publiques OMS (Operations Management Suite) Log Analytics pour effectuer un push des journaux d’audit SQL vers OMS.</span><span class="sxs-lookup"><span data-stu-id="58a2c-178">It runs in Azure and utilizes Operations Management Suite (OMS) Log Analytics public APIs to push SQL audit logs into OMS.</span></span> <span data-ttu-id="58a2c-179">L’application de synchronisation effectue un push des journaux d’audit SQL vers OMS Log Analytics pour les utiliser dans le tableau de bord OMS Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="58a2c-179">The sync application pushes SQL audit logs into OMS Log Analytics for consumption via the OMS Log Analytics dashboard.</span></span> 

* <span data-ttu-id="58a2c-180">Utilisez Power BI.</span><span class="sxs-lookup"><span data-stu-id="58a2c-180">Use Power BI.</span></span> <span data-ttu-id="58a2c-181">Vous pouvez afficher et analyser les données du journal d’audit dans Power BI.</span><span class="sxs-lookup"><span data-stu-id="58a2c-181">You can view and analyze audit log data in Power BI.</span></span> <span data-ttu-id="58a2c-182">Explorez [Power BI et accédez à un modèle téléchargeable](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span><span class="sxs-lookup"><span data-stu-id="58a2c-182">Learn more about [Power BI, and access a downloadable template](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).</span></span>

* <span data-ttu-id="58a2c-183">Téléchargez les fichiers journaux à partir de votre conteneur Azure Storage Blob via le portail ou avec un outil comme [l’Explorateur de stockage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="58a2c-183">Download log files from your Azure Storage blob container via the portal or by using a tool such as [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
    * <span data-ttu-id="58a2c-184">Une fois que vous avez téléchargé localement un fichier journal, vous pouvez double-cliquer sur le fichier pour ouvrir, afficher et analyser les journaux dans SSMS.</span><span class="sxs-lookup"><span data-stu-id="58a2c-184">After you have downloaded a log file locally, you can double-click the file to open, view, and analyze the logs in SSMS.</span></span>
    * <span data-ttu-id="58a2c-185">Vous pouvez également télécharger plusieurs fichiers simultanément avec l’Explorateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="58a2c-185">You can also download multiple files simultaneously via Azure Storage Explorer.</span></span> <span data-ttu-id="58a2c-186">Cliquez avec le bouton droit sur un sous-dossier spécifique (par exemple, un sous-dossier qui inclut tous les fichiers journaux pour une date spécifique) et sélectionnez **Enregistrer sous** pour l’enregistrer dans un dossier local.</span><span class="sxs-lookup"><span data-stu-id="58a2c-186">Right-click a specific subfolder (for example, a subfolder that includes all log files for a specific date) and select **Save as** to save in a local folder.</span></span>

* <span data-ttu-id="58a2c-187">Autres méthodes :</span><span class="sxs-lookup"><span data-stu-id="58a2c-187">Additional methods:</span></span>
   * <span data-ttu-id="58a2c-188">Après avoir téléchargé plusieurs fichiers (ou un sous-dossier qui comprend les fichiers journaux pour une journée entière, comme indiqué dans l’élément précédent de cette liste), vous pouvez les fusionner localement comme illustré dans les instructions relatives à l’option Fusionner les fichiers d’audit dans SSMS décrites précédemment.</span><span class="sxs-lookup"><span data-stu-id="58a2c-188">After downloading several files (or a subfolder that includes log files for an entire day, as described in the previous item in this list), you can merge them locally as described in the SSMS Merge Audit Files instructions described earlier.</span></span>

   * <span data-ttu-id="58a2c-189">Affichez des journaux d’audit d’objets blob par programmation :</span><span class="sxs-lookup"><span data-stu-id="58a2c-189">View blob auditing logs programmatically:</span></span>

     * <span data-ttu-id="58a2c-190">Utilisez la bibliothèque C# [Lecteur des événements étendus](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/).</span><span class="sxs-lookup"><span data-stu-id="58a2c-190">Use the [Extended Events Reader](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) C# library.</span></span>
     * <span data-ttu-id="58a2c-191">[Interrogez des fichiers d’événements étendus](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="58a2c-191">[Query Extended Events Files](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) by using PowerShell.</span></span>




## <span data-ttu-id="58a2c-192"><a id="subheading-5"></a>Pratiques de production</span><span class="sxs-lookup"><span data-stu-id="58a2c-192"><a id="subheading-5"></a>Production practices</span></span>
<!--The description in this section refers to preceding screen captures.-->

### <span data-ttu-id="58a2c-193"><a id="subheading-6">Audit des bases de données géorépliquées</a></span><span class="sxs-lookup"><span data-stu-id="58a2c-193"><a id="subheading-6">Auditing geo-replicated databases</a></span></span>
<span data-ttu-id="58a2c-194">Quand vous utilisez des bases de données géorépliquées, il est possible de configurer l’audit sur la base de données primaire, sur la base de données secondaire ou sur les deux, selon le type d’audit.</span><span class="sxs-lookup"><span data-stu-id="58a2c-194">When you use geo-replicated databases, it is possible to set up auditing on either the primary database, the secondary database, or both, depending on the audit type.</span></span>

<span data-ttu-id="58a2c-195">Suivez ces instructions (gardez à l’esprit que l’audit d’objets blob peut être activé ou désactivé uniquement à partir des paramètres d’audit de la base de données primaire) :</span><span class="sxs-lookup"><span data-stu-id="58a2c-195">Follow these instructions (remember that blob auditing can be turned on or off only from the primary database auditing settings):</span></span>

* <span data-ttu-id="58a2c-196">**Base de données primaire**.</span><span class="sxs-lookup"><span data-stu-id="58a2c-196">**Primary database**.</span></span> <span data-ttu-id="58a2c-197">Activez l’audit d’objets blob sur le serveur ou sur la base de données elle-même, comme décrit dans la section [Configuration de l’audit pour votre base de données](#subheading-2).</span><span class="sxs-lookup"><span data-stu-id="58a2c-197">Turn on blob auditing, either on the server or on the database itself, as described in the [Set up auditing for your database](#subheading-2) section.</span></span>
* <span data-ttu-id="58a2c-198">**Base de données secondaire**.</span><span class="sxs-lookup"><span data-stu-id="58a2c-198">**Secondary database**.</span></span> <span data-ttu-id="58a2c-199">Activez l’audit d’objets blob sur la base de données primaire, comme décrit dans la section [Configuration de l’audit pour votre base de données](#subheading-2).</span><span class="sxs-lookup"><span data-stu-id="58a2c-199">Turn on blob auditing on the primary database, as described in the [Set up auditing for your database](#subheading-2) section.</span></span> 
   * <span data-ttu-id="58a2c-200">L’audit Objet blob doit être activé sur la *base de données primaire elle-même*, et non pas sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="58a2c-200">Blob auditing must be enabled on the *primary database itself*, not the server.</span></span>
   * <span data-ttu-id="58a2c-201">Une fois que l’audit d’objets blob est activé sur la base de données primaire, il est également activé sur la base de données secondaire.</span><span class="sxs-lookup"><span data-stu-id="58a2c-201">After blob auditing is enabled on the primary database, it will also become enabled on the secondary database.</span></span>

     >[!IMPORTANT]
     ><span data-ttu-id="58a2c-202">Par défaut, les paramètres de stockage pour la base de données secondaire sont identiques à ceux de la base de données primaire, ce qui provoque un trafic entre régions.</span><span class="sxs-lookup"><span data-stu-id="58a2c-202">By default, the storage settings for the secondary database will be identical to those of the primary database, causing cross-regional traffic.</span></span> <span data-ttu-id="58a2c-203">Vous pouvez éviter cela en activant l’audit d’objets blob sur le serveur secondaire et en configurant le stockage local dans les paramètres de stockage du serveur secondaire.</span><span class="sxs-lookup"><span data-stu-id="58a2c-203">You can avoid this by enabling blob auditing on the secondary server and configuring local storage in the secondary server storage settings.</span></span> <span data-ttu-id="58a2c-204">Cela remplace l’emplacement de stockage pour la base de données secondaire et, par conséquent, chaque base de données enregistre ses journaux d’audit dans le stockage local.</span><span class="sxs-lookup"><span data-stu-id="58a2c-204">This will override the storage location for the secondary database and result in each database saving its audit logs to local storage.</span></span>  
<br>

### <span data-ttu-id="58a2c-205"><a id="subheading-6">Régénération des clés de stockage</a></span><span class="sxs-lookup"><span data-stu-id="58a2c-205"><a id="subheading-6">Storage key regeneration</a></span></span>
<span data-ttu-id="58a2c-206">Dans un environnement de production, vous allez probablement actualiser périodiquement vos clés de stockage.</span><span class="sxs-lookup"><span data-stu-id="58a2c-206">In production, you are likely to refresh your storage keys periodically.</span></span> <span data-ttu-id="58a2c-207">Lors de l’actualisation de vos clés, vous devez réenregistrer la stratégie d’audit.</span><span class="sxs-lookup"><span data-stu-id="58a2c-207">When refreshing your keys, you need to resave the auditing policy.</span></span> <span data-ttu-id="58a2c-208">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="58a2c-208">The process is as follows:</span></span>

1. <span data-ttu-id="58a2c-209">Ouvrez le panneau **Détails du stockage**.</span><span class="sxs-lookup"><span data-stu-id="58a2c-209">Open the **Storage Details** blade.</span></span> <span data-ttu-id="58a2c-210">Dans la zone **Clé d’accès de stockage**, sélectionnez **Secondaire**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="58a2c-210">In the **Storage Access Key** box, select **Secondary**, and click **OK**.</span></span> <span data-ttu-id="58a2c-211">Cliquez ensuite sur **Enregistrer** en haut du panneau de configuration de l’audit.</span><span class="sxs-lookup"><span data-stu-id="58a2c-211">Then click **Save** at the top of the auditing configuration blade.</span></span>

    ![Volet de navigation][5]
2. <span data-ttu-id="58a2c-213">Accédez au panneau de configuration du stockage, puis régénérez la clé d’accès primaire.</span><span class="sxs-lookup"><span data-stu-id="58a2c-213">Go to the storage configuration blade and regenerate the primary access key.</span></span>

    ![Volet de navigation][6]
3. <span data-ttu-id="58a2c-215">Revenez au panneau de configuration de l’audit, remplacez la clé d’accès de stockage secondaire par la clé primaire, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="58a2c-215">Go back to the auditing configuration blade, switch the storage access key from secondary to primary, and then click **OK**.</span></span> <span data-ttu-id="58a2c-216">Cliquez ensuite sur **Enregistrer** en haut du panneau de configuration de l’audit.</span><span class="sxs-lookup"><span data-stu-id="58a2c-216">Then click **Save** at the top of the auditing configuration blade.</span></span>
4. <span data-ttu-id="58a2c-217">Revenez au panneau de configuration du stockage, puis régénérez la clé d’accès secondaire (en préparation du cycle suivant d’actualisation des clés).</span><span class="sxs-lookup"><span data-stu-id="58a2c-217">Go back to the storage configuration blade and regenerate the secondary access key (in preparation for the next key's refresh cycle).</span></span>

## <span data-ttu-id="58a2c-218"><a id="subheading-7"></a>Automation (PowerShell / API REST)</span><span class="sxs-lookup"><span data-stu-id="58a2c-218"><a id="subheading-7"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="58a2c-219">Vous pouvez également configurer l’audit dans Azure SQL Database en utilisant les outils d’automation suivants :</span><span class="sxs-lookup"><span data-stu-id="58a2c-219">You can also configure auditing in Azure SQL Database by using the following automation tools:</span></span>

* <span data-ttu-id="58a2c-220">**Applets de commande PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="58a2c-220">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="58a2c-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="58a2c-221">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="58a2c-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="58a2c-222">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="58a2c-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="58a2c-223">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="58a2c-224">[Remove-AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="58a2c-224">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="58a2c-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="58a2c-225">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="58a2c-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="58a2c-226">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="58a2c-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="58a2c-227">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

   <span data-ttu-id="58a2c-228">Pour obtenir un exemple de script, consultez [Configurer l’audit et la détection des menaces avec PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="58a2c-228">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

* <span data-ttu-id="58a2c-229">**API REST - Audit d’objets blob** :</span><span class="sxs-lookup"><span data-stu-id="58a2c-229">**REST API - Blob auditing**:</span></span>

   * [<span data-ttu-id="58a2c-230">Create or Update Database Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="58a2c-230">Create or Update Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [<span data-ttu-id="58a2c-231">Create or Update Server Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="58a2c-231">Create or Update Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [<span data-ttu-id="58a2c-232">Get Database Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="58a2c-232">Get Database Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [<span data-ttu-id="58a2c-233">Get Server Blob Auditing Policy</span><span class="sxs-lookup"><span data-stu-id="58a2c-233">Get Server Blob Auditing Policy</span></span>](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [<span data-ttu-id="58a2c-234">Get Server Blob Auditing Operation Result</span><span class="sxs-lookup"><span data-stu-id="58a2c-234">Get Server Blob Auditing Operation Result</span></span>](https://msdn.microsoft.com/library/azure/mt771862.aspx)


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
