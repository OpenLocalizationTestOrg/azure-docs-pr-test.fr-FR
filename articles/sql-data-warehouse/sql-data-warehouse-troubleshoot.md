---
title: aaaTroubleshooting Azure SQL Data Warehouse | Documents Microsoft
description: "Résolution des problèmes d’Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 51f1e444-9ef7-4e30-9a88-598946c45196
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/30/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3c53a39f77057fe0bcc053a0b896555abf397515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-sql-data-warehouse"></a>Résolution des problèmes d’Azure SQL Data Warehouse
Cette rubrique répertorie certaines des hello nous attendons de nos clients des questions de dépannage plus courantes.

## <a name="connecting"></a>Connexion
| Problème | Résolution : |
|:--- |:--- |
| Échec de connexion pour l’utilisateur 'NT AUTHORITY\ANONYMOUS LOGON'. (Microsoft SQL Server, erreur : 18456) |Cette erreur se produit lorsqu’un utilisateur d’AAD tente de base de données master tooconnect toohello, mais ne dispose pas d’un utilisateur dans master.  toocorrect ce problème, spécifiez hello SQL Data Warehouse, vous souhaitez le moment de la connexion tooconnect tooat ou ajoutez de la base de données master de toohello utilisateur hello.  Consultez l’article [Présentation de la sécurité][Security overview] pour plus de détails. |
| serveur Hello MyUserName « principal » n’est pas en mesure de tooaccess hello de base de données « master » sous le contexte de sécurité actuel hello. La base de données utilisateur par défaut ne peut pas être ouverte. La connexion a échoué. Échec de la connexion pour l'utilisateur 'MyUserName'. (Microsoft SQL Server, erreur : 916) |Cette erreur se produit lorsqu’un utilisateur d’AAD tente de base de données master tooconnect toohello, mais ne dispose pas d’un utilisateur dans master.  toocorrect ce problème, spécifiez hello SQL Data Warehouse, vous souhaitez le moment de la connexion tooconnect tooat ou ajoutez de la base de données master de toohello utilisateur hello.  Consultez l’article [Présentation de la sécurité][Security overview] pour plus de détails. |
| Erreur CTAIP |Cette erreur peut se produire lorsqu’une connexion a été créée sur la base de données master hello SQL server, mais pas dans la base de données SQL Data Warehouse hello.  Si vous rencontrez cette erreur, examinez hello [vue d’ensemble de la sécurité] [ Security overview] l’article.  Cet article explique comment toocreate créer une connexion et utilisateur dans master, puis comment toocreate un utilisateur dans hello de base de données SQL Data Warehouse. |
| Bloqué par le pare-feu |Bases de données SQL Azure sont protégés par tooensure de pare-feu de niveau serveur et base de données connue uniquement des adresses IP ont la base de données access tooa. les pare-feu Hello sont sécurisées par défaut, ce qui signifie que vous devez activer explicitement et adresse IP ou plage d’adresses avant de vous connecter.  tooconfigure votre pare-feu pour l’accès, suivez les étapes hello dans [configurer l’accès de pare-feu de serveur pour votre adresse IP du client] [ Configure server firewall access for your client IP] Bonjour [des instructions de configuration] [Provisioning instructions]. |
| Connexion impossible avec l’outil ou le pilote |SQL Data Warehouse recommande l’utilisation de [SSMS][SSMS], [SSDT pour Visual Studio][SSDT for Visual Studio], ou [sqlcmd] [ sqlcmd] tooquery vos données. Pour plus d’informations sur la connexion tooSQL l’entrepôt de données et des pilotes, consultez [pilotes pour Azure SQL Data Warehouse] [ Drivers for Azure SQL Data Warehouse] et [connecter tooAzure SQL Data Warehouse] [ Connect tooAzure SQL Data Warehouse] articles. |

## <a name="tools"></a>Outils
| Problème | Résolution : |
|:--- |:--- |
| Des utilisateurs Azure Active Directory sont manquants dans l’explorateur d’objets Visual Studio |Il s'agit d'un problème connu.  Pour résoudre ce problème, afficher les utilisateurs de hello dans [sys.database_principals][sys.database_principals].  Consultez [tooAzure de l’authentification SQL Data Warehouse] [ Authentication tooAzure SQL Data Warehouse] toolearn plus en détail à l’aide d’Azure Active Directory avec l’entrepôt de données SQL. |
|Manuel de scripts, à l’aide d’Assistant de script hello ou qui se connectent via SSMS est lents, bloqués ou produire des erreurs| Assurez-vous que les utilisateurs ont été créés dans la base de données master hello. Dans les options de script, assurez-vous également que cette édition de moteur hello est définie en tant que « Édition Microsoft Azure SQL Data Warehouse » et type de moteur est « Microsoft Azure SQL Database ».|

## <a name="performance"></a>Performances
| Problème | Résolution : |
|:--- |:--- |
| Résolution des problèmes de performances des requêtes |Si vous essayez de tootroubleshoot une requête particulière, commencez par [apprendre comment toomonitor vos requêtes][Learning how toomonitor your queries]. |
| Des performances des requêtes et des plans médiocres sont souvent le résultat de statistiques manquantes |cause la plus courante de performances médiocres Hello est le manque de statistiques sur les tables.  Consultez [gestion de statistiques de table] [ Statistics] pour plus d’informations sur la façon de statistiques de toocreate et pourquoi ils sont critiques tooyour performances. |
| Concurrence faible / requêtes en file d’attente |Présentation de [gestion de la charge de travail] [ Workload management] est important dans l’ordre toounderstand comment toobalance l’allocation de mémoire avec l’accès concurrentiel. |
| Comment tooimplement meilleures pratiques |Bonjour place toostart toolearn façons tooimprove meilleurs résultats est [SQL Data Warehouse meilleures pratiques] [ SQL Data Warehouse best practices] l’article. |
| Comment tooimprove les performances avec la mise à l’échelle |Performances de tooimproving la solution hello est parfois toosimply ajouter plusieurs requêtes tooyour puissance de calcul [mise à l’échelle de votre entrepôt de données SQL][Scaling your SQL Data Warehouse]. |
| Performances de requêtes médiocres en raison de la qualité médiocre de l’index |Parfois, les requêtes peuvent ralentir en raison de la [qualité médiocre des index columnstore][Poor columnstore index quality].  Consultez cet article pour plus d’informations et comment trop[reconstruction d’index qualité de segment tooimprove][Rebuild indexes tooimprove segment quality]. |

## <a name="system-management"></a>Gestion de systèmes
| Problème | Résolution : |
|:--- |:--- |
| Msg 40847 : Impossible d’effectuer les opération hello, car le serveur dépasserait hello autorisé quota d’unité de Transaction de base de données de 45000. |Vous pouvez soit réduire hello [DWU] [ DWU] de base de données hello vous essayez de toocreate ou [demander une augmentation du quota][request a quota increase]. |
| Examen de l’utilisation de l’espace |Consultez [Table tailles] [ Table sizes] utilisation de l’espace de hello toounderstand de votre système. |
| Aide concernant la gestion des tables |Consultez hello [vue d’ensemble de la Table] [ Overview] l’article d’aide sur la gestion de vos tables.  Cet article inclut également des liens vers des rubriques plus détaillées, notamment [Types de données de table][Data types], [Distribution d’une table][Distribute], [Indexation d’une table][Index], [Partitionnement d’une table][Partition], [Maintenance des statistiques de table][Statistics] et [Tables temporaires][Temporary]. |
|Barre de progression (TDE) le chiffrement transparent des données n’est pas mise à jour Bonjour portail Azure|Vous pouvez afficher état hello du chiffrement transparent des données via [powershell](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption).|

## <a name="polybase"></a>Polybase
| Problème | Résolution : |
|:--- |:--- |
| Échec du chargement en raison des grandes lignes |Actuellement, la prise en charge des grandes lignes n’est pas disponible pour Polybase.  Cela signifie que si votre table contient varchar (max), nvarchar (max) ou varbinary (max), les tables externes ne peuvent pas être utilisé tooload vos données.  Charges pour les lignes de grande taille est actuellement prise en charge uniquement via Azure Data Factory (avec BCP), Azure flux Analytique, SSIS, BCP ou hello classe .NET SQLBulkCopy. La prise en charge de PolyBase pour les grandes lignes sera ajoutée dans une version ultérieure. |
| Échec de chargement BCP d’une table avec le type de données MAX |Il existe un problème connu qui nécessite que varchar (max), nvarchar (max) ou varbinary (max) soient placés à fin hello de table hello dans certains scénarios.  Essayez de déplacer votre principal de toohello MAX colonnes de table de hello. |

## <a name="differences-from-sql-database"></a>Différences par rapport à la base de données SQL
| Problème | Résolution : |
|:--- |:--- |
| Fonctionnalités de base de données SQL non prises en charge |Voir [Fonctionnalités de tables non prises en charge][Unsupported table features]. |
| Types de données de base de données SQL non pris en charge |Voir [Types de données non pris en charge][Unsupported data types]. |
| Limitations DELETE et UPDATE |Consultez [solutions de contournement de mise à jour][UPDATE workarounds], [solutions de contournement DELETE] [ DELETE workarounds] et [toowork à l’aide de SACT autour d’une mise à jour non pris en charge et Syntaxe de suppression][Using CTAS toowork around unsupported UPDATE and DELETE syntax]. |
| Instruction MERGE non prise en charge |Consultez la rubrique [Solutions de contournement MERGE][MERGE workarounds]. |
| Limitations des procédures stockées |Consultez [stockées les limitations de la procédure] [ Stored procedure limitations] toounderstand certaines des limitations de hello des procédures stockées. |
| Les fonctions définies par l’utilisateur ne prennent pas en charge les instructions SELECT |Il s’agit d’une limitation actuelle de nos fonctions définies par l’utilisateur.  Consultez [CREATE FUNCTION] [ CREATE FUNCTION] pour connaître la syntaxe hello nous prenons en charge. |

## <a name="next-steps"></a>Étapes suivantes
Si vous êtes ont été toofind Impossible d’un problème de tooyour solution ci-dessus, voici quelques autres ressources que vous pouvez essayer.

* [Blogs]
* [Demandes de fonctionnalités]
* [Vidéos]
* [Blogs de l’équipe CAT (Customer Advisory Team)]
* [Création d’un ticket de support]
* [Forum MSDN]
* [Forum Stack Overflow]
* [Twitter]

<!--Image references-->

<!--Article references-->
[Security overview]: ./sql-data-warehouse-overview-manage-security.md
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx
[SSDT for Visual Studio]: ./sql-data-warehouse-install-visual-studio.md
[Drivers for Azure SQL Data Warehouse]: ./sql-data-warehouse-connection-strings.md
[Connect tooAzure SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Création d’un ticket de support]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Scaling your SQL Data Warehouse]: ./sql-data-warehouse-manage-compute-overview.md
[DWU]: ./sql-data-warehouse-overview-what-is.md
[request a quota increase]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Learning how toomonitor your queries]: ./sql-data-warehouse-manage-monitor.md
[Provisioning instructions]: ./sql-data-warehouse-get-started-provision.md
[Configure server firewall access for your client IP]: ./sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[Table sizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries
[Unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuild indexes tooimprove segment quality]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Using CTAS toowork around unsupported UPDATE and DELETE syntax]: ./sql-data-warehouse-develop-ctas.md#using-ctas-to-work-around-unsupported-features
[UPDATE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[DELETE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[MERGE workarounds]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[Stored procedure limitations]: ./sql-data-warehouse-develop-stored-procedures.md#limitations
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md
[Working around hello PolyBase UTF-8 requirement]: ./sql-data-warehouse-load-polybase-guide.md#working-around-the-polybase-utf-8-requirement

<!--MSDN references-->
[sys.database_principals]: https://msdn.microsoft.com/library/ms187328.aspx
[CREATE FUNCTION]: https://msdn.microsoft.com/library/mt203952.aspx
[sqlcmd]: https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-get-started-connect-sqlcmd/

<!--Other Web references-->
[Blogs]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Blogs de l’équipe CAT (Customer Advisory Team)]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Demandes de fonctionnalités]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Forum MSDN]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse
[Forum Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Vidéos]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
