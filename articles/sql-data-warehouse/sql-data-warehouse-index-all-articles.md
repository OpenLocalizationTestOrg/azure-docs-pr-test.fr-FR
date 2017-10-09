---
title: "les rubriques aaaAll pour le service de l’entrepôt de données SQL | Documents Microsoft"
description: "Tableau de toutes les rubriques pour hello service Azure nommé SQL Data Warehouse qui existent sur http://azure.microsoft.com/documentation/articles/, Title et description."
services: sql-data-warehouse
documentationcenter: 
author: barbkess
manager: jhubbard
editor: 
ms.assetid: a26a6dec-9c08-4415-8f58-4ee1dd41f718
ms.service: sql-data-warehouse
ms.workload: sql-data-warehouse
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: reference
ms.date: 03/30/2017
ms.author: barbkess
ms.openlocfilehash: 6f71d35b76b50764a5904525445675dafaa56b85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="all-topics-for-azure-sql-data-warehouse-service"></a>Toutes les rubriques pour le service SQL Data Warehouse
Cette rubrique répertorie toutes les rubriques qui s’applique directement toohello **SQL Data Warehouse** service de Azure. Vous pouvez rechercher cette page Web pour les mots clés à l’aide de **Ctrl + F**, rubriques de hello toofind d’intérêt en cours.

## <a name="new"></a>Nouveau
| &nbsp; | Intitulé | Description |
| ---:|:--- |:--- |
| 1 |[Sauvegardes SQL Data Warehouse](sql-data-warehouse-backups.md) |En savoir plus sur les sauvegardes de base de données intégrée SQL Data Warehouse qui vous permettent de toorestore un point de restauration tooa Azure SQL Data Warehouse ou une autre région géographique. |

## <a name="updated-articles-sql-data-warehouse"></a>Articles mis à jour, SQL Data Warehouse
Cette section répertorie les articles qui ont été récemment mis à jour, où hello mettre à jour est grande ou importante. Pour chaque article de mise à jour, un extrait de code approximative de hello ajouté markdown texte est affiché. les articles Hello ont été mis à jour au sein de la plage de dates de hello **2016-08-22** trop**2016-10-05**.

| &nbsp; | Article | Texte mis à jour, extrait de code | Mis à jour quand |
| ---:|:--- |:--- |:--- |
| 2 |[Charger les données de stockage d’objets blob Azure dans SQL Data Warehouse (PolyBase)](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |/ tootrack octets et sélectionnez r.command, s.request_id, r.status, count (distinct input_name) en tant que nbr_files, sum (s.bytes_processed) / 1024/1024 en tant que gb_processed de sys.dm_pdw_exec_requests r jointure interne sys.dm_pdw_dms_external_work s sur r.request_id de fichiers = s.request_id où r. label  = ’CTAS : Load  cso . DimProduct  ’  OR r. label  = ’CTAS : Load  cso . FactOnlineSales  ’ GROUP BY  r.command,  s.request_id,  r.status ORDER BY  nbr_files desc,  gb_processed desc; |2016-09-07 |
| 3 |[Restauration SQL Data Warehouse](sql-data-warehouse-restore-database-overview.md) |** Puis-je restaurer un entrepôt de données en pause ? ** toorestore un entrepôt de données est suspendu, vous devez toofirst le remettre en ligne. Une fois que l’entrepôt de données hello est remis en ligne, vous avez des toochoose de points de restauration à partir de sept jours. ** Restaurer tooa géo-redondant région ** si vous utilisez un stockage géo-redondant hello, vous pouvez restaurer hello données entrepôt tooyour appariés centre de données dans une autre région géographique. entrepôt de données Hello est restauré à partir de la dernière sauvegarde quotidienne la hello. ** Restaurez chronologie ** vous pouvez restaurer un point de restauration de base de données tooany dans hello sept derniers jours. Instantanés de toutes les quatre heures tooeight et sont disponibles pour les sept jours. Quand une capture instantanée a une ancienneté supérieure à sept jours, elle expire et son point de restauration n’est plus disponible. ** Restore coûts ** frais de stockage hello pour hello restauré l’entrepôt de données est facturée au tarif de stockage Azure Premium hello. Si vous suspendez un entrepôt de données restaurées, vous êtes facturé pour le stockage au tarif de stockage Azure Premium hello. Hello de la suspension d’avantage que vous n’êtes pas gratuits |2016-09-29 |

## <a name="get-started"></a>Prise en main
| &nbsp; | Intitulé | Description |
| ---:|:--- |:--- |
| 4 |[Authentification tooAzure SQL Data Warehouse](sql-data-warehouse-authentication.md) |Azure Active Directory (AAD) et SQL Server authentication tooAzure SQL Data Warehouse. |
| 5 |[Meilleures pratiques pour Azure SQL Data Warehouse](sql-data-warehouse-best-practices.md) |Recommandations et meilleures pratiques que vous devez connaître pour développer des solutions pour Azure SQL Data Warehouse. Elles vous aideront à réussir. |
| 6 |[Pilotes pour Azure SQL Data Warehouse](sql-data-warehouse-connection-strings.md) |Chaînes de connexion et pilotes pour SQL Data Warehouse |
| 7 |[Se connecter tooAzure SQL Data Warehouse](sql-data-warehouse-connect-overview.md) |Comment chaîne de connexion et le nom du serveur toofind hello pour votre tooAzure SQL Data Warehouse |
| 8 |[Analyse des données avec Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md) |Utilisez toobuild d’Azure Machine Learning un modèle basé sur les données stockées dans Azure SQL Data Warehouse prédictive d’apprentissage. |
| 9 |[Interroger Azure SQL Data Warehouse (sqlcmd)](sql-data-warehouse-get-started-connect-sqlcmd.md) |Interrogation d’Azure SQL Data Warehouse avec sqlcmd hello utilitaire de ligne de commande. |
| 10 |[Créer une base de données SQL Data Warehouse à l’aide de Transact-SQL (TSQL).](sql-data-warehouse-get-started-create-database-tsql.md) |Découvrez comment toocreate une données SQL Azure de l’entrepôt de TSQL |
| 11 |[Comment toocreate une prise en charge de ticket pour SQL Data Warehouse](sql-data-warehouse-get-started-create-support-ticket.md) |Comment toocreate une prise en charge de ticket dans Azure SQL Data Warehouse. |
| 12 |[Téléchargement de données avec Azure Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md) |En savoir plus les données tooload avec Azure Data Factory |
| 13. |[Télécharger des données avec PolyBase dans SQL Data Warehouse](sql-data-warehouse-get-started-load-with-polybase.md) |Découvrez les nouveautés de PolyBase et comment toouse pour les scénarios d’entreposage de données. |
| 14 |[Créer un Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md) |Découvrez comment toocreate un entrepôt de données SQL Azure dans hello portail Azure |
| 15 |[Création de SQL Data Warehouse à l’aide de PowerShell](sql-data-warehouse-get-started-provision-powershell.md) |Création de SQL Data Warehouse à l’aide de PowerShell |
| 16 |[Visualiser des données avec Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md) |Visualiser les données SQL Data Warehouse avec Power BI |
| 17 |[Interroger Azure SQL Data Warehouse (sqlcmd) (Visual Studio)](sql-data-warehouse-query-visual-studio.md) |Interrogez SQL Data Warehouse avec Visual Studio. |

## <a name="develop"></a>Développement
| &nbsp; | Intitulé | Description |
| ---:|:--- |:--- |
| 18 |[Optimisation des transactions pour SQL Data Warehouse](sql-data-warehouse-develop-best-practices-transactions.md) |Meilleures pratiques sur l’écriture de mises à jour efficaces de transactions dans Azure SQL Data Warehouse |
| 19 |[Gestion de la concurrence et des charges de travail dans SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md) |Décrit la gestion de la concurrence et des charges de travail dans Azure SQL Data Warehouse pour le développement de solutions. |
| 20 |[Instruction Create Table As Select (CTAS) dans SQL Data Warehouse](sql-data-warehouse-develop-ctas.md) |Conseils pour le codage par hello créer la table que vous sélectionnez l’instruction de (SACT) dans l’entrepôt de données SQL Azure pour développer des solutions. |
| 21 |[Code SQL dynamique dans SQL Data Warehouse](sql-data-warehouse-develop-dynamic-sql.md) |Conseils relatifs à l’utilisation de code SQL dynamique dans Azure SQL Data Warehouse pour le développement de solutions. |
| 22 |[Options de regroupement dans SQL Data Warehouse](sql-data-warehouse-develop-group-by-options.md) |Conseils relatifs à l’implémentation d’options de regroupement dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions. |
| 23 |[Utiliser les requêtes de tooinstrument d’étiquettes dans l’entrepôt de données SQL](sql-data-warehouse-develop-label.md) |Conseils pour l’utilisation de requêtes de tooinstrument étiquettes dans l’entrepôt de données SQL Azure pour développer des solutions. |
| 24 |[Boucles dans SQL Data Warehouse](sql-data-warehouse-develop-loops.md) |Conseils relatifs à l’utilisation de boucles Transact-SQL et au remplacement de curseurs dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions. |
| 25 |[Procédures stockées dans SQL Data Warehouse](sql-data-warehouse-develop-stored-procedures.md) |Conseils relatifs à l’implémentation de procédures stockées dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions. |
| 26 |[Transactions dans SQL Data Warehouse](sql-data-warehouse-develop-transactions.md) |Conseils relatifs à l’implémentation de transactions dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions. |
| 27 |[Schémas définis par l’utilisateur dans SQL Data Warehouse](sql-data-warehouse-develop-user-defined-schemas.md) |Conseils relatifs à l’utilisation de schémas Transact-SQL dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions. |
| 28 |[Affecter des variables dans SQL Data Warehouse](sql-data-warehouse-develop-variable-assignment.md) |Conseils relatifs à l’affectation de variables Transact-SQL dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions. |
| 29 |[Vues proposées par SQL Data Warehouse](sql-data-warehouse-develop-views.md) |Conseils relatifs à l’utilisation de vues Transact-SQL dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions. |
| 30 |[Choix de conception et techniques de codage pour SQL Data Warehouse](sql-data-warehouse-overview-develop.md) |Concepts de développement, choix de conception, recommandations et des techniques de codage pour SQL Data Warehouse. |

## <a name="manage"></a>Gérer
| &nbsp; | Intitulé | Description |
| ---:|:--- |:--- |
| 31 |[Gestion de la puissance de calcul dans Azure SQL Data Warehouse (Vue d’ensemble)](sql-data-warehouse-manage-compute-overview.md) |Capacités de montée en puissance des performances dans Azure SQL Data Warehouse. Montée en puissance parallèle en ajustant les Dwu ou suspendre et reprendre les coûts toosave de ressources de calcul. |
| 32 |[Gestion de la puissance de calcul dans Azure SQL Data Warehouse (portail Azure)](sql-data-warehouse-manage-compute-portal.md) |Tâches du portail Azure toomanage une puissance de calcul. Mettez à l’échelle les ressources de calcul en ajustant les unités DWU. Ou bien, suspendre et reprendre des coûts toosave des ressources de calcul. |
| 33 |[Gestion de la puissance de calcul dans Azure SQL Data Warehouse (PowerShell)](sql-data-warehouse-manage-compute-powershell.md) |PowerShell tâches toomanage une puissance de calcul. Mettez à l’échelle les ressources de calcul en ajustant les unités DWU. Ou bien, suspendre et reprendre des coûts toosave des ressources de calcul. |
| 34 |[Gestion de la puissance de calcul dans Azure SQL Data Warehouse (REST)](sql-data-warehouse-manage-compute-rest-api.md) |PowerShell tâches toomanage une puissance de calcul. Mettez à l’échelle les ressources de calcul en ajustant les unités DWU. Ou bien, suspendre et reprendre des coûts toosave des ressources de calcul. |
| 35 |[Gestion de la puissance de calcul dans Azure SQL Data Warehouse (T-SQL)](sql-data-warehouse-manage-compute-tsql.md) |Transact-SQL (T-SQL) tâches tooscale performances en ajustant les Dwu. Réalisez des économies en réduisant vos ressources pendant les heures creuses. |
| 36 |[Surveiller votre charge de travail à l'aide de vues de gestion dynamique](sql-data-warehouse-manage-monitor.md) |Découvrez comment toomonitor votre charge de travail à l’aide de vues de gestion dynamique. |
| 37 |[Gestion de bases de données dans Azure SQL Data Warehouse](sql-data-warehouse-overview-manage.md) |Vue d’ensemble de la gestion des bases de données SQL Data Warehouse. Inclut des outils de gestion, des unités DWU et une montée en puissance des performances, une résolution des problèmes de performances des requêtes, la mise en œuvre de stratégies de sécurité adaptées et la restauration d’une base de données en cas d’altération des données ou de panne au niveau régional. |
| 38 |[Surveillance des requêtes d’utilisateur dans Azure SQL Data Warehouse](sql-data-warehouse-overview-manage-user-queries.md) |Vue d’ensemble des considérations de hello, les meilleures pratiques et les tâches de surveillance des requêtes utilisateur dans Azure SQL Data Warehouse |
| 39 |[Restauration SQL Data Warehouse](sql-data-warehouse-restore-database-overview.md) |Vue d’ensemble des options de restauration de base de données hello pour récupérer une base de données dans l’entrepôt de données SQL Azure. |
| 40 |[Restauration d’un Azure SQL Data Warehouse (Portail)](sql-data-warehouse-restore-database-portal.md) |Tâches du portail Azure permettant de restaurer un Azure SQL Data Warehouse. |
| 41 |[Restauration d’un Azure SQL Data Warehouse (PowerShell)](sql-data-warehouse-restore-database-powershell.md) |Tâches PowerShell permettant de restaurer un Azure SQL Data Warehouse. |
| 42 |[Restauration d’un Azure SQL Data Warehouse (API REST)](sql-data-warehouse-restore-database-rest-api.md) |Tâches d’API REST permettant de restaurer un Azure SQL Data Warehouse. |

## <a name="tables-and-indexes"></a>Tables et index
| &nbsp; | Intitulé | Description |
| ---:|:--- |:--- |
| 43 |[Types de données pour tables dans SQL Data Warehouse](sql-data-warehouse-tables-data-types.md) |Prise en main des types de données pour les tables Azure SQL Data Warehouse. |
| 44 |[Distribution de tables dans SQL Data Warehouse](sql-data-warehouse-tables-distribute.md) |Prise en main de la distribution de tables dans Azure SQL Data Warehouse. |
| 45 |[Indexation de tables dans SQL Data Warehouse](sql-data-warehouse-tables-index.md) |Prise en main de l’indexation de tables dans Azure SQL Data Warehouse. |
| 46 |[Vue d’ensemble des tables dans SQL Data Warehouse](sql-data-warehouse-tables-overview.md) |Prise en main des tables Azure SQL Data Warehouse. |
| 47 |[Partitionnement de tables dans SQL Data Warehouse](sql-data-warehouse-tables-partition.md) |Prise en main du partitionnement de tables dans Azure SQL Data Warehouse. |
| 48 |[Gestion des statistiques sur les tables dans SQL Data Warehouse](sql-data-warehouse-tables-statistics.md) |Prise en main des statistiques sur les tables dans Azure SQL Data Warehouse. |
| 49 |[Tables temporaires dans SQL Data Warehouse](sql-data-warehouse-tables-temporary.md) |Prise en main des tables temporaires dans Azure SQL Data Warehouse. |

## <a name="integrate"></a>Integrate
| &nbsp; | Intitulé | Description |
| ---:|:--- |:--- |
| 50 |[Utiliser Azure Data Factory avec SQL Data Warehouse](sql-data-warehouse-integrate-azure-data-factory.md) |Conseils sur l’utilisation de Microsoft Azure Data Factory avec Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions. |
| 51 |[Utilisation de Microsoft Azure Machine Learning avec SQL Data Warehouse](sql-data-warehouse-integrate-azure-machine-learning.md) |Didacticiel sur l’utilisation de Microsoft Azure Machine Learning avec Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions. |
| 52 |[Utiliser Azure Stream Analytics avec SQL Data Warehouse](sql-data-warehouse-integrate-azure-stream-analytics.md) |Conseils sur l’utilisation d’Azure Stream Analytics avec Azure SQL Data Warehouse pour le développement de solutions. |
| 53 |[Utiliser Power BI avec SQL Data Warehouse](sql-data-warehouse-integrate-power-bi.md) |Conseils relatifs à l’utilisation de Power BI avec Azure SQL Data Warehouse pour le développement de solutions. |
| 54 |[Tirer parti d’autres services avec SQL Data Warehouse](sql-data-warehouse-overview-integrate.md) |Outils et partenaires proposant des solutions s’intégrant avec SQL Data Warehouse. |

## <a name="load"></a>charger
| &nbsp; | Intitulé | Description |
| ---:|:--- |:--- |
| 55 |[Charger les données conservées dans un stockage d’objets blob Azure dans Azure SQL Data Warehouse. (Azure Data Factory)](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md) |En savoir plus les données tooload avec Azure Data Factory |
| 56 |[Charger les données de stockage d’objets blob Azure dans SQL Data Warehouse (PolyBase)](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |Découvrez comment les données tooload Azure toouse PolyBase stockage d’objets blob dans SQL Data Warehouse. Charger plusieurs tables à partir de données publics dans le schéma d’entrepôt de données Contoso Retail hello. |
| 57 |[Charger des données à partir de SQL Server dans Azure SQL Data Warehouse (AZCopy)](sql-data-warehouse-load-from-sql-server-with-azcopy.md) |Utilise les données de tooexport bcp à partir de fichiers tooflat de SQL Server, le stockage blob tooAzure AZCopy tooimport données et les données de salutation tooingest PolyBase dans Azure SQL Data Warehouse. |
| 58 |[Charger des données à partir de SQL Server dans Azure SQL Data Warehouse (fichiers plats)](sql-data-warehouse-load-from-sql-server-with-bcp.md) |Pour une taille de données de petite taille, utilise les données tooexport de bcp à partir de fichiers tooflat de SQL Server et importer des données hello directement dans l’entrepôt de données SQL Azure. |
| 59 |[Charger des données à partir de SQL Server dans Azure SQL Data Warehouse (SSIS)](sql-data-warehouse-load-from-sql-server-with-integration-services.md) |Montre comment toocreate un SQL Server Integration Services (SSIS) package toomove des données d’une grande variété de données sources tooSQL l’entrepôt de données. |
| 60 |[Télécharger des données avec PolyBase dans SQL Data Warehouse](sql-data-warehouse-load-from-sql-server-with-polybase.md) |Utilise les données de tooexport bcp à partir de fichiers tooflat de SQL Server, le stockage blob tooAzure AZCopy tooimport données et les données de salutation tooingest PolyBase dans Azure SQL Data Warehouse. |
| 61 |[Guide d'utilisation de PolyBase dans SQL Data Warehouse](sql-data-warehouse-load-polybase-guide.md) |Instructions et recommandations relatives à l'utilisation de PolyBase dans les scénarios SQL Data Warehouse. |
| 62 |[Charger des exemples de données dans SQL Data Warehouse](sql-data-warehouse-load-sample-databases.md) |Charger des exemples de données dans SQL Data Warehouse |
| 63 |[Charger des données avec bcp](sql-data-warehouse-load-with-bcp.md) |Découvrez quels bcp est et comment toouse pour les scénarios d’entreposage de données. |
| 64 |[Chargement de données dans Azure SQL Data Warehouse](sql-data-warehouse-overview-load.md) |Découvrez les scénarios courants de hello pour les données à charger dans l’entrepôt de données SQL. Ceux-ci incluent l’utilisation de PolyBase, d’Azure Blob Storage et de fichiers plats ainsi que l’envoi de disques. Vous pouvez également utiliser des outils tiers. |

## <a name="migrate"></a>Migrer
| &nbsp; | Intitulé | Description |
| ---:|:--- |:--- |
| 65 |[Migrer votre tooSQL de code SQL Data Warehouse](sql-data-warehouse-migrate-code.md) |Conseils pour migrer votre tooAzure de code SQL SQL Data Warehouse pour développer des solutions. |
| 66 |[Migration de vos données](sql-data-warehouse-migrate-data.md) |Conseils pour migrer votre tooAzure de données SQL Data Warehouse pour développer des solutions. |
| 67 |[Utilitaire de migration de l’entrepôt de données (version préliminaire)](sql-data-warehouse-migrate-migration-utility.md) |Migrer tooSQL l’entrepôt de données. |
| 68 |[Migrer votre tooSQL schéma l’entrepôt de données](sql-data-warehouse-migrate-schema.md) |Conseils pour migrer votre tooAzure de schéma SQL Data Warehouse pour développer des solutions. |
| 69 |[Migrer votre tooSQL solution entrepôt de données](sql-data-warehouse-overview-migrate.md) |Conseils de migration pour mettre votre plateforme de SQL Data Warehouse tooAzure la solution. |

## <a name="partners"></a>Partenaires
| &nbsp; | Intitulé | Description |
| ---:|:--- |:--- |
| 70 |[Partenaires décisionnels de SQL Data Warehouse](sql-data-warehouse-partner-business-intelligence.md) |Répertorie les partenaires tiers en matière d’aide à la décision proposant des solutions qui prennent en charge SQL Data Warehouse. |
| 71 |[Partenaires de SQL Data Warehouse en matière d’intégration de données](sql-data-warehouse-partner-data-integration.md) |Répertorie les partenaires tiers proposant des solutions d’intégration de données prenant en charge SQL Data Warehouse. |
| 72 |[Partenaires de SQL Data Warehouse en matière de gestion de données](sql-data-warehouse-partner-data-management.md) |Répertorie les partenaires de gestion des données tiers proposant des solutions qui prennent en charge SQL Data Warehouse. |

## <a name="reference"></a>Référence
| &nbsp; | Intitulé | Description |
| ---:|:--- |:--- |
| 73 |[Rubriques de référence pour SQL Data Warehouse](sql-data-warehouse-overview-reference.md) |Liens vers du contenu de référence pour SQL Data Warehouse. |
| 74 |[Applets de commande PowerShell et API REST pour SQL Data Warehouse](sql-data-warehouse-reference-powershell-cmdlets.md) |Rechercher les applets de commande PowerShell supérieur hello pour Azure SQL Data Warehouse notamment toopause et reprendre une base de données. |
| 75 |[Éléments de langage](sql-data-warehouse-reference-tsql-language-elements.md) |Liste du contenu tooreference de liens pour les éléments de langage hello Transact-SQL utilisée pour l’entrepôt de données SQL. |
| 76 |[Rubriques Transact-SQL](sql-data-warehouse-reference-tsql-statements.md) |Contenu de tooreference liens des rubriques de Transact-SQL hello utilisé par SQL Data Warehouse. |
| 77 |[Vues système](sql-data-warehouse-reference-tsql-system-views.md) |Liens toosystem affiche du contenu pour l’entrepôt de données SQL. |

## <a name="security"></a>Sécurité
| &nbsp; | Intitulé | Description |
| ---:|:--- |:--- |
| 78 |[SQL Data Warehouse : prise en charge des clients de niveau inférieur pour l’audit et le masquage dynamique des données (Dynamic Data Masking)](sql-data-warehouse-auditing-downlevel-clients.md) |En savoir plus sur la prise en charge des clients de niveau inférieur de SQL Data Warehouse pour l’audit des données |
| 79 |[Audit dans Azure SQL Data Warehouse](sql-data-warehouse-auditing-overview.md) |Prise en main de l’audit dans Azure SQL Data Warehouse |
| 80 |[Mise en route avec le chiffrement transparent des données (TDE) dans SQL Data Warehouse](sql-data-warehouse-encryption-tde.md) |Chiffrement transparent des données (TDE) dans SQL Data Warehouse |
| 81 |[Prise en main du chiffrement transparent des données (TDE)](sql-data-warehouse-encryption-tde-tsql.md) |Chiffrement transparent des données (TDE) dans SQL Data Warehouse (T-SQL) |
| 82 |[Sécuriser une base de données dans SQL Data Warehouse](sql-data-warehouse-overview-manage-security.md) |Conseils relatifs à la sécurisation d’une base de données dans Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions. |

## <a name="miscellaneous"></a>Divers
| &nbsp; | Intitulé | Description |
| ---:|:--- |:--- |
| 83 |[Installer Visual Studio et SSDT pour SQL Data Warehouse](sql-data-warehouse-install-visual-studio.md) |Installer les outils de développement Visual Studio et SSDT pour Azure SQL Data Warehouse |
| 84 |[Migration tooPremium détails de stockage](sql-data-warehouse-migrate-to-premium-storage.md) |Instructions pour la migration d’un stockage de toopremium de l’entrepôt de données SQL existant |
| 85 |[Prise en main de la détection de menaces](sql-data-warehouse-security-threat-detection.md) |Comment tooget démarrer avec la détection des menaces |
| 86 |[Limites de la capacité de SQL Data Warehouse](sql-data-warehouse-service-capacity-limits.md) |Valeurs maximales pour les connexions, les bases de données, les tables et les requêtes pour SQL Data Warehouse. |
| 87 |[Résolution des problèmes d’Azure SQL Data Warehouse](sql-data-warehouse-troubleshoot.md) |Résolution des problèmes d’Azure SQL Data Warehouse. |

