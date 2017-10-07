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
# <a name="get-started-with-sql-database-auditing"></a>Bien démarrer avec l’audit de bases de données SQL
Audit de base de données SQL Azure effectue le suivi des événements de base de données et les écrit le journal d’audit de tooan dans votre compte de stockage Azure. Par ailleurs, l’audit :

* peut vous aider à respecter une conformité réglementaire, à comprendre l’activité de la base de données ainsi qu’à découvrir des discordances et anomalies susceptibles d’indiquer des problèmes pour l’entreprise ou des violations de la sécurité ;

* Permet et facilite les normes de toocompliance d’adhésion, bien qu’il ne garantit pas la conformité. Pour plus d’informations sur Azure programmes que la conformité aux normes de prise en charge, consultez hello [Azure Trust Center](https://azure.microsoft.com/support/trust-center/compliance/).


## <a id="subheading-1"></a>Vue d’ensemble de l’audit be bases de données SQL Azure
Vous pouvez utiliser l’audit de bases de données SQL pour :


* **La rétention** d’une piste d’audit d’événements sélectionnés. Vous pouvez définir des catégories de base de données actions toobe est auditée.
* **La génération de rapports** sur les activités de la base de données. Vous pouvez utiliser les rapports préconfigurés et un tooget de tableau de bord rapidement opérationnel avec activité et les rapports d’événements.
* **L'analyse** des rapports. Vous pouvez repérer les événements suspects, les activités inhabituelles et les tendances.

Vous pouvez configurer l’audit pour les différents types de catégories d’événements, comme expliqué dans hello [configurer l’audit pour votre base de données](#subheading-2) section.

Journaux d’audit sont écrites de stockage d’objets Blob tooAzure sur votre abonnement Azure.


## <a id="subheading-8"></a>Définir une stratégie d’audit au niveau du serveur ou au niveau de la base de données

Une stratégie d’audit peut être définie pour une base de données spécifique ou en tant que stratégie de serveur par défaut :

* Une stratégie de serveur s’applique tooall existantes et nouvelles bases de données sur le serveur de hello.

* Si *l’audit de blob serveur est activé*, il *applique toujours la base de données toohello* (autrement dit, base de données hello est audité), quelle que soit la base de données hello paramètres d’audit.

* L’activation d’objet blob de l’audit sur base de données hello dans Ajout tooenabling sur le serveur de hello, sera *pas* remplacer ou modifier les paramètres d’audit d’objets blob hello serveur hello. Les deux audits coexistent. En d’autres termes, la base de données hello est audité deux fois en parallèle (une fois par la stratégie de serveur hello et qu’une seule fois par la stratégie de base de données hello).

   > [!NOTE]
   > Vous devez éviter d’activer à la fois l’audit d’objets blob du serveur et l’audit d’objets blob de la base de données, sauf si :
    > * Vous voulez toouse un autre *compte de stockage* ou *période de rétention* pour une base de données spécifique.
    > * Vous souhaitez les catégories ou les types d’événements tooaudit pour une base de données spécifique qui diffèrent des types d’événements ou des catégories qui sont en cours d’audit pour les autres hello hello bases de données hello serveur. Par exemple, peut avoir des insertions de table qui doivent toobe auditer uniquement pour une base de données spécifique.
   > 
   > Dans le cas contraire, nous vous recommandons d’activer l’audit des objets blob d’uniquement au niveau du serveur et laissez hello au niveau de la base de données d’audit désactivé pour toutes les bases de données.


## <a id="subheading-2"></a>Configuration de l’audit pour votre base de données
Hello section suivante décrit la configuration hello d’audit à l’aide de hello portail Azure.

1. Accédez toohello [portail Azure](https://portal.azure.com).
2. Accédez toohello **paramètres** Panneau de hello SQL de base de données/serveur SQL server tooaudit. Bonjour **paramètres** panneau, sélectionnez **détection d’audit et de menaces**.

    <a id="auditing-screenshot"></a>![Volet de navigation][1]
3. Si vous préférez tooset d’une stratégie d’audit de serveur (qui doit s’appliquer tooall existant et bases de données nouvellement créées sur ce serveur), vous pouvez sélectionner hello **afficher les paramètres du serveur** lien dans le panneau de l’audit de base de données hello. Vous pouvez afficher ou modifier les paramètres d’audit de serveur hello.

    ![Volet de navigation][2]
4. Si vous préférez tooenable blob l’audit de niveau de base de données de hello (dans tooor ajout au lieu de l’audit au niveau du serveur), **audit**, sélectionnez **ON**et pour **l’audit de type** , sélectionnez **Blob**.

    Si l’audit des objets blob de serveur est activé, audit de base de données configurée hello existe côte à côte avec l’audit du blob serveur hello.  

    ![Volet de navigation][3]
5. tooopen hello **stockage des journaux d’Audit** panneau, sélectionnez **détails de stockage**. Sélectionnez le compte de stockage Azure hello où seront enregistrés les journaux et puis sélectionnez la période de rétention hello, après le hello anciens journaux seront supprimés. Cliquez ensuite sur **OK**. 
   >[!TIP] 
   >hello tooget parti hello audit des modèles de rapports, utilisez hello même compte de stockage pour toutes les bases de données audités. 

    <a id="storage-screenshot"></a>![Volet de navigation][4]
6. Si vous souhaitez que les événements audité de hello toocustomize, vous pouvez le faire via PowerShell ou hello API REST. Pour plus d’informations, consultez hello [Automation (API PowerShell/REST)](#subheading-7) section.
7. Une fois que vous avez configuré vos paramètres d’audit, vous pouvez activer la nouvelle fonctionnalité de détection de menaces hello et configurer des alertes de sécurité des messages électroniques tooreceive. La détection des menaces vous permet de recevoir des alertes proactives sur des activités anormales de la base de données qui peuvent indiquer des menaces de sécurité potentielles. Pour plus d’informations, consultez [Bien démarrer avec la détection des menaces](sql-database-threat-detection-get-started.md).
8. Cliquez sur **Enregistrer**.





## <a id="subheading-3"></a>Analyse des journaux et des rapports d’audit
Journaux d’audit sont regroupées dans hello compte de stockage Azure que vous avez choisi lors de l’installation. Vous pouvez explorer les journaux d’audit avec un outil comme [l’Explorateur de stockage Azure](http://storageexplorer.com/).

Les journaux d’audit d’objets blob sont enregistrés sous la forme d’une collection de fichiers d’objets blob dans un conteneur nommé **sqldbauditlogs**.

Pour plus d’informations sur la hiérarchie hello du dossier de stockage des journaux hello blob d’audit, conventions d’affectation de noms d’objet blob et le format de journal, consultez hello [référence de la Format de journal d’Audit Blob (téléchargement de fichier .docx)](https://go.microsoft.com/fwlink/?linkid=829599).

Il existe plusieurs méthodes que vous pouvez utiliser blob tooview les journaux d’audit :

* Hello d’utilisation [portail Azure](https://portal.azure.com).  Base de données appropriée hello ouvert. Haut de hello AT de la base de données hello **détection d’audit et de menaces** panneau, cliquez sur **afficher les journaux d’audit**.

    ![Volet de navigation][7]

    Un **enregistrements d’Audit** s’ouvre le panneau, à partir de laquelle vous serez en mesure de tooview hello journaux.

    - Vous pouvez afficher des dates spécifiques en cliquant sur **filtre** haut hello hello **enregistrements d’Audit** panneau.
    - Vous pouvez basculer entre les enregistrements d’audit qui ont été créés par un audit de stratégie de base de données ou de stratégie de serveur.

       ![Volet de navigation][8]

* Utilisez la fonction du système hello **sys.fn_get_audit_file** données du journal d’audit (T-SQL) tooreturn hello sous forme de tableau. Pour plus d’informations sur l’utilisation de cette fonction, consultez hello [sys.fn_get_audit_file documentation](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).


* Utilisez **Fusionner les fichiers d’audit** dans SQL Server Management Studio (à partir de SSMS 17) :  
    1. Dans le menu SSMS hello, sélectionnez **fichier** > **ouvrir** > **fusionner les fichiers d’Audit**.

        ![Volet de navigation][9]
    2. Hello **ajouter des fichiers d’Audit** boîte de dialogue s’ouvre. Sélectionnez une des hello **ajouter** options pour choisir si des fichiers d’audit de toomerge à partir d’une variable locale du disque ou les importer depuis le stockage Azure (vous sera nécessaire tooprovide vos informations de stockage Azure et de la clé de compte).

    3. Une fois tous les fichiers toomerge ont été ajoutés, cliquez sur **OK** opération de fusion toocomplete hello.

    4. Hello fusionné s’ouvre dans SSMS, où vous pouvez afficher et analyser, ainsi que des exportation il tooan XEL ou CSV tooa ou fichier de la table.

* Hello d’utilisation [synchronisation application](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) que nous avons créés. Il s’exécute dans Azure et utilise l’Analytique des journaux Operations Management Suite (OMS) publique API toopush SQL des journaux d’audit dans OMS. synchroniser l’application Hello transmet les journaux d’audit SQL dans l’Analytique des journaux OMS pour la consommation via le tableau de bord hello Analytique des journaux OMS. 

* Utilisez Power BI. Vous pouvez afficher et analyser les données du journal d’audit dans Power BI. Explorez [Power BI et accédez à un modèle téléchargeable](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).

* Téléchargez les fichiers journaux à partir de votre conteneur d’objets blob de stockage Azure via le portail de hello ou à l’aide d’un outil tel que [Azure Storage Explorer](http://storageexplorer.com/).
    * Après avoir téléchargé un fichier journal localement, vous pouvez double-cliquer sur hello tooopen de fichier, afficher et analyser les journaux hello dans SSMS.
    * Vous pouvez également télécharger plusieurs fichiers simultanément avec l’Explorateur de stockage Azure. Cliquez sur un sous-dossier spécifique (par exemple, un sous-dossier qui inclut tous les fichiers journaux pour une date spécifique) et sélectionnez **enregistrer en tant que** toosave dans un dossier local.

* Autres méthodes :
   * Après le téléchargement de plusieurs fichiers (ou un sous-dossier qui comprend des fichiers journaux pour une journée entière, comme indiqué dans l’élément précédent de hello dans cette liste), vous pouvez les fusionner localement comme décrit dans les instructions de fichiers d’Audit de fusion SSMS hello décrites précédemment.

   * Affichez des journaux d’audit d’objets blob par programmation :

     * Hello d’utilisation [lecteur d’événements étendus](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) bibliothèque c#.
     * [Interrogez des fichiers d’événements étendus](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) avec PowerShell.




## <a id="subheading-5"></a>Pratiques de production
<!--hello description in this section refers toopreceding screen captures.-->

### <a id="subheading-6">Audit des bases de données géorépliquées</a>
Lorsque vous utilisez des bases de données répliquées, il est possible tooset l’audit sur la base de données primaire hello, base de données secondaire hello ou les deux, selon le type de l’audit hello.

Suivez ces instructions (n’oubliez pas que l’audit des objets blob peut être activée ou désactivée uniquement à partir des paramètres d’audit de la base de données hello principale) :

* **Base de données primaire**. Activer le blob l’audit sur le serveur de hello ou sur une base de données hello lui-même, comme décrit dans hello [configurer l’audit pour votre base de données](#subheading-2) section.
* **Base de données secondaire**. Activer l’audit de l’objet blob sur la base de données primaire hello, comme décrit dans hello [configurer l’audit pour votre base de données](#subheading-2) section. 
   * Audit de l’objet BLOB doit être activée sur hello *base de données primaire elle-même*, non par serveur hello.
   * Une fois que l’objet blob l’audit est activé sur la base de données primaire hello, il est également activé sur la base de données secondaire hello.

     >[!IMPORTANT]
     >Par défaut, les paramètres de stockage hello pour la base de données secondaire hello sera identique toothose de base de données primaire hello, à l’origine du trafic entre-régionale. Vous pouvez éviter cela en activant l’audit des objets blob sur le serveur secondaire de hello et la configuration du stockage local dans les paramètres de stockage de serveur secondaire hello. Cela remplacera l’emplacement de stockage hello pour la base de données secondaire hello et résultats dans chaque base de données de l’enregistrement de son stockage toolocal de journaux d’audit.  
<br>

### <a id="subheading-6">Régénération des clés de stockage</a>
En production, vous êtes probablement toorefresh votre stockage de clés périodiquement. Lors de l’actualisation de vos clés, vous devez la stratégie d’audit tooresave hello. processus de Hello est comme suit :

1. Ouvrez hello **détails de stockage** panneau. Bonjour **clé d’accès de stockage** boîte, sélectionnez **secondaire**, puis cliquez sur **OK**. Puis cliquez sur **enregistrer** haut hello hello l’audit du Panneau de configuration.

    ![Volet de navigation][5]
2. Atteindre le panneau de configuration de stockage toohello et régénérer la clé d’accès primaire hello.

    ![Volet de navigation][6]
3. Revenir en arrière toohello l’audit du Panneau de configuration, basculez de clé d’accès de stockage hello de tooprimary secondaire, puis cliquez sur **OK**. Puis cliquez sur **enregistrer** haut hello hello l’audit du Panneau de configuration.
4. Retournez dans Panneau de configuration de stockage toohello et la clé d’accès secondaire hello régénérer (en vue de cycle d’actualisation de la clé suivante hello).

## <a id="subheading-7"></a>Automation (PowerShell / API REST)
Vous pouvez également configurer l’audit dans la base de données SQL Azure à l’aide de hello suivant des outils d’automatisation :

* **Applets de commande PowerShell**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Use-AzureRMSqlServerAuditingPolicy][107]

   Pour obtenir un exemple de script, consultez [Configurer l’audit et la détection des menaces avec PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

* **API REST - Audit d’objets blob** :

   * [Create or Update Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [Create or Update Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [Get Database Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [Get Server Blob Auditing Policy](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [Get Server Blob Auditing Operation Result](https://msdn.microsoft.com/library/azure/mt771862.aspx)


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
