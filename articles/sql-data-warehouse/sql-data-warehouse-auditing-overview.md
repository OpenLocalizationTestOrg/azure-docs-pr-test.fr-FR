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
# <a name="auditing-in-azure-sql-data-warehouse"></a>Audit dans Azure SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Audit](sql-data-warehouse-auditing-overview.md)
> * [Détection de menaces](sql-data-warehouse-security-threat-detection.md)
> 
> 

L’audit de l’entrepôt de données SQL vous permet de toorecord événements dans votre journal d’audit de base de données tooan dans votre compte de stockage Azure. L’audit peut vous aider à respecter une conformité réglementaire, à comprendre l’activité de la base de données, et à découvrir des discordances et des anomalies susceptibles d’indiquer des problèmes pour l’entreprise ou des violations de la sécurité. Cette fonction s’intègre également dans Microsoft Power BI, afin de faciliter la création d’analyses et de rapports approfondis.

Les outils d’audit activent et facilitent les normes de conformité toocompliance mais ne garantissent pas la conformité. Pour plus d’informations sur Azure programmes que la conformité aux normes de prise en charge, consultez hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.

* [Principes fondamentaux de l’audit de base de données]
* [Configuration de l'audit pour votre base de données]
* [Analyse des journaux et des rapports d’audit]

## <a id="subheading-1"></a>Principes fondamentaux de l’audit de base de données Azure SQL Data Warehouse
Éléments rendus possibles par l’audit de bases de données SQL Data Warehouse :

* **La rétention** d’une piste d’audit d’événements sélectionnés. Vous pouvez définir des catégories de base de données actions toobe est auditée.
* **La génération de rapports** sur les activités de la base de données. Vous pouvez utiliser les rapports préconfigurés et un tooget de tableau de bord rapidement opérationnel avec activité et les rapports d’événements.
* **L'analyse** des rapports. Vous pouvez repérer les événements suspects, les activités inhabituelles et les tendances.

Vous pouvez configurer l’audit pour hello suivant des catégories d’événements :

**SQL brut** et **SQL paramétrées** pour le hello les journaux d’audit collectées sont classés comme  

* **Accès toodata**
* **modifications de schéma (DDL) ;**
* **modifications de données (DML) ;**
* **comptes, rôles et autorisations (DCL) ;**
* **Procédure stockée**, **Connexion** et **Gestion des transactions**.

Pour chaque catégorie d’événements, les audits des opérations **Succès** et **Échec** sont configurées séparément.

Pour plus d’informations sur les activités hello et les événements audités, consultez hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">référence de Format de journal d’Audit (téléchargement de fichier doc)</a>.

Les journaux d'audit sont stockés dans votre compte de stockage Azure. Vous pouvez définir une période de rétention des journaux d'audit.

Une stratégie d’audit peut être définie pour une base de données spécifique ou en tant que stratégie de serveur par défaut. Une stratégie d’audit de serveur par défaut s’applique tooall de bases de données sur un serveur, ce qui n’ont pas d’une substitution de base de données stratégie d’audit spécifique définie.

Avant de configurer l’audit, vérifiez que vous utilisez bien un [« Client de niveau inférieur »](sql-data-warehouse-auditing-downlevel-clients.md).

## <a id="subheading-2"></a>Configuration de l’audit pour votre base de données
1. Lancez hello <a href="https://portal.azure.com" target="_blank">portail Azure</a>.
2. Accédez toohello **paramètres** Panneau de hello souhaité tooaudit SQL Data Warehouse. Bonjour **paramètres** panneau, sélectionnez **détection d’audit et de menaces**.
   
    ![][1]
3. Ensuite, activez l’audit en cliquant sur hello **ON** bouton.
   
    ![][3]
4. Bonjour l’audit du Panneau de configuration, sélectionnez **détails de stockage** Panneau de stockage des journaux d’Audit tooopen hello. Sélectionnez hello compte de stockage Azure dans lequel les journaux sont enregistrés et hello période de rétention. 
>[!TIP]
>Hello utilisez même compte de stockage pour tous les hello tooget de bases de données audités parti hello préconfiguré signale des modèles.
   
    ![][4]
5. Cliquez sur hello **OK** configuration des détails stockage bouton toosave hello.
6. Sous **journalisation par événement**, cliquez sur **réussite** et **échec** toolog tous les événements, ou choisir des catégories d’événements.
7. Si vous configurez l’audit pour une base de données, vous devrez peut-être la chaîne de connexion tooalter hello de votre tooensure client audit de données est capturée correctement. Vérifiez hello [modifier les FQDN de serveur dans la chaîne de connexion hello](sql-data-warehouse-auditing-downlevel-clients.md) rubrique pour les connexions de client de niveau inférieur.
8. Cliquez sur **OK**.

## <a id="subheading-3"></a>Analyse des journaux et des rapports d’audit
Journaux d’audit sont regroupées dans une collection de Tables de magasin avec un **SQLDBAuditLogs** préfixe Bonjour compte de stockage Azure que vous avez choisi lors de l’installation. Vous pouvez afficher les fichiers journaux à l'aide d'un outil tel que l'<a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Explorateur de stockage Azure</a>.

Un modèle de rapport de tableau de bord préconfigurés est disponible en tant qu’un <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">feuille de calcul Excel téléchargeable</a> toohelp analyser rapidement les données du journal. modèle de hello toouse sur vos journaux d’audit, vous devez Excel 2013 ou version ultérieure et Power Query, que vous pouvez télécharger <a href="http://www.microsoft.com/download/details.aspx?id=39379">ici</a>.

modèle de Hello comporte des données d’exemple fictif, et vous pouvez configurer Power Query tooimport votre journal d’audit directement à partir de votre compte de stockage Azure.

## <a id="subheading-4"></a>Régénération des clés de stockage
En production, vous êtes probablement toorefresh votre stockage de clés périodiquement. Lors de l’actualisation de vos clés, vous devez la stratégie de hello toosave. processus de Hello est comme suit :

1. Bonjour à l’audit du Panneau de configuration (comme décrit ci-dessus dans le programme d’installation hello section d’audit) Basculer hello **clé d’accès de stockage** de *principal* trop*secondaire* et  **Enregistrer**.

   ![][4]
2. Panneau de configuration de stockage accédez toohello et **régénérer** hello *clé d’accès primaire*.
3. Revenir en arrière toohello l’audit du Panneau de configuration, commutateur hello **clé d’accès de stockage** de *secondaire* trop*principal* et appuyez sur **enregistrer**.
4. Revenir en arrière toohello stockage UI et **régénérer** hello *clé d’accès secondaire* (dans la préparation de hello clés prochains cycle d’actualisation.

## <a id="subheading-5"></a>Automation (PowerShell / API REST)
Vous pouvez également configurer l’audit dans l’entrepôt de données SQL Azure à l’aide de hello suivant des outils d’automatisation :

* **Applets de commande PowerShell**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Use-AzureRMSqlServerAuditingPolicy][107]

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