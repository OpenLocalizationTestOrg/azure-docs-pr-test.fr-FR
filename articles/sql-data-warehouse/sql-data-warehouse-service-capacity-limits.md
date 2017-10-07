---
title: "limites de capacité de l’entrepôt de données aaaSQL | Documents Microsoft"
description: "Valeurs maximales pour les connexions, les bases de données, les tables et les requêtes pour SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: e1eac122-baee-4200-a2ed-f38bfa0f67ce
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 8619cb997f0955d649d447cb8ca15cd742cc70b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-capacity-limits"></a>Limites de la capacité de SQL Data Warehouse
Hello tableaux suivants contiennent les valeurs maximales hello autorisés pour les différents composants de l’entrepôt de données SQL Azure.

## <a name="workload-management"></a>Gestion des charges de travail
| Catégorie | Description | Maximale |
|:--- |:--- |:--- |
| [Data Warehouse Units (DWU)][Data Warehouse Units (DWU)] |DWU max pour un SQL Data Warehouse unique |6000 |
| [Data Warehouse Units (DWU)][Data Warehouse Units (DWU)] |DWU max pour un serveur SQL unique |6 000 par défaut<br/><br/> Par défaut, chaque serveur SQL server (par exemple, myserver.database.windows.net) a un Quota de DTU de 45 000, qui permet de too6000 DWU. Ce quota constitue simplement une limite de sécurité. Vous pouvez augmenter votre quota par [création d’un ticket de support] [ creating a support ticket] et en sélectionnant *Quota* en tant que type de demande hello.  toocalculate votre DTU a besoin, multipliez hello 7.5 par total hello DWU si nécessaire. Vous pouvez afficher votre consommation DTU actuelle à partir du panneau hello SQL server dans le portail de hello. Interruption et reprises des bases de données s’inscrivent du quota UDBD hello. |
| Connexion de base de données |Sessions simultanées ouvertes |1 024<br/><br/>Nous prenons en charge un maximum de connexions actives de 1024, chacune d’elles peut envoyer des demandes tooa SQL Data Warehouse base de données hello même temps. Notez qu’il existe des limites de nombre hello des requêtes qui peuvent effectivement s’exécuter simultanément. Hello d’accès concurrentiel limite est dépassée, demande de hello est affiché en file d’attente interne où il attend toobe traité. |
| Connexion de base de données |Mémoire maximale pour les instructions préparées |20 Mo |
| [Gestion des charges de travail][Workload management] |Nombre maximal de requêtes concurrentes |32<br/><br/> Par défaut, SQL Data Warehouse peut exécuter un maximum de 32 requêtes et files d’attente simultanées.<br/><br/>niveau de concurrence Hello peut-être diminuer lorsque des utilisateurs sont affectés de classe de ressource supérieur tooa ou lorsque l’entrepôt de données SQL est configuré avec DWU basse. Certaines requêtes, comme les requêtes de la vue de gestion dynamique, sont toujours autorisés toorun. |
| [Tempdb][Tempdb] |Taille maximale de Tempdb |399 Go par DW100. Par conséquent, est dimensionnée too3.99 to DWU1000 Tempdb |

## <a name="database-objects"></a>Objets de base de données
| Catégorie | Description | Maximale |
|:--- |:--- |:--- |
| Base de données |Taille maximale |240 To compressés sur disque<br/><br/>Cet espace est indépendant de l’espace tempdb ou de journal, et par conséquent, cet espace est dédié toopermanent tables.  La compression du cluster columnstore est estimée à 5 X.  Cette compression permet hello de base de données toogrow tooapproximately 1 po lorsque toutes les tables sont columnstore en cluster (type de table hello par défaut). |
| Table |Taille maximale |60 To compressés sur disque |
| Table |Tables par base de données |2 milliards |
| Table |Colonnes par table |1 024 colonnes |
| Table |Octets par colonne |Dépend de la colonne [type de données][data type].  La limite est de 8 000 pour les types de données Char, de 4 000 pour nvarchar ou 2 Go pour les types de données MAX. |
| Table |Octets par ligne, taille définie |8060 octets<br/><br/>nombre de Hello d’octets par ligne est calculée Bonjour exactement telle qu’elle est pour SQL Server avec la compression de page. Tel que SQL Server, SQL Data Warehouse prend en charge le stockage de dépassement de ligne qui permet **des colonnes de longueur variable** toobe envoyées hors ligne. Lorsque des lignes de longueur variable sont envoyées hors ligne, seule racine de 24 octets est stocké dans l’enregistrement principal des hello. Pour plus d’informations, consultez hello [dépassement de ligne de données supérieure à 8 Ko] [ Row-Overflow Data Exceeding 8 KB] article MSDN. |
| Table |Partitions par table |15 000<br/><br/>Pour des performances élevées, nous vous recommandons de réduire le nombre de hello de partitions, vous avez besoin tout en prenant en charge des besoins de votre entreprise. En tant que hello augmente le nombre de partitions, surcharge de hello pour langage DDL (Data Definition) et se développe et entraîne la baisse des performances des opérations de langage de Manipulation de données (DML). |
| Table |Caractères par valeur limite de partition. |4000 |
| Index |Index non-cluster par table. |999<br/><br/>S’applique uniquement les tables toorowstore. |
| Index |Index cluster par table. |1<br><br/>Applique les tables rowstore et columnstore tooboth. |
| Index |Taille de la clé d’index. |900 octets.<br/><br/>S’applique uniquement les index toorowstore.<br/><br/>Index sur des colonnes varchar d’une taille maximale de plus de 900 octets peuvent être créés si les données existantes hello dans les colonnes hello n’excède pas 900 octets lors de la création d’index de hello. Toutefois, d’insérer ou des actions de mise à jour sur les colonnes hello qui provoquent la taille totale de hello tooexceed 900 octets échouera. |
| Index |Colonnes clés par index. |16<br/><br/>S’applique uniquement les index toorowstore. Les index de stockage de colonnes cluster incluent toutes les colonnes. |
| Statistiques |Taille de hello combinés des valeurs de colonne. |900 octets. |
| Statistiques |Colonnes par objet de statistiques. |32 |
| Statistiques |Statistiques créées sur les colonnes par table. |30 000 |
| Procédures stockées |Nombre maximal de niveaux d’imbrication. |8 |
| Affichage |Colonnes par vue |1 024 |

## <a name="loads"></a>Charges
| Catégorie | Description | Maximale |
|:--- |:--- |:--- |
| Charges Polybase |60 Mo par ligne |1<br/><br/>Polybase charges sont inférieures à 1 Mo de tooloading limité de lignes à la fois et ne peut pas charger tooVARCHR(MAX), nvarchar (max) ou varbinary (max).<br/><br/> |

## <a name="queries"></a>Requêtes
| Catégorie | Description | Maximale |
|:--- |:--- |:--- |
| Interroger |Requêtes mises en file d’attente sur les tables utilisateur. |1 000 |
| Interroger |Requêtes simultanées sur les vues système. |100 |
| Interroger |Requêtes mises en file d’attente sur les vues système |1 000 |
| Interroger |Nombre maximal de paramètres |2 098 |
| Batch |Taille maximale |65 536*4 096 |
| Résultats SELECT |Colonnes par ligne |4096<br/><br/>Vous ne pouvez jamais avoir plus de 4096 de colonnes par ligne Bonjour sélectionnez résultat. Le nombre de 4 096 colonnes n’est pas toujours garanti. Si le plan de requête hello requiert une table temporaire, hello 1024 colonnes par table maximale peuvent s’appliquer. |
| SELECT |Sous-requêtes imbriquées |32<br/><br/>Un instruction SELECT ne peut pas contenir plus de 32 sous-requêtes imbriquées. Le nombre de 32 sous-requêtes n’est pas toujours garanti. Par exemple, une jointure peut introduire une sous-requête dans le plan de requête hello. nombre de Hello de sous-requêtes peut aussi être limité par la mémoire disponible. |
| SELECT |Colonnes par JOIN |1 024 colonnes<br/><br/>Vous ne pouvez jamais avoir plus de 1 024 colonnes Bonjour jointure. Le nombre de 1024 colonnes n’est pas toujours garanti. Si le plan de jointure hello requiert une table temporaire avec plus de colonnes que le résultat de la jointure hello, limite de 1024 hello applique la table temporaire de toohello. |
| SELECT |Octets par colonnes GROUP BY. |8 060<br/><br/>les colonnes dans la clause GROUP BY hello Hello peuvent avoir un maximum de 8 060 octets. |
| SELECT |Octets par colonnes ORDER BY |8 060 octets.<br/><br/>les colonnes dans la clause ORDER BY hello Hello peuvent avoir un maximum de 8 060 octets. |
| Identificateurs et constantes par instruction |Nombre d’identificateurs et constantes référencés. |65 535<br/><br/>Entrepôt de données SQL limite le nombre hello d’identificateurs et les constantes qui peuvent être contenus dans une seule expression d’une requête. Cette limite s’élève à 65 535. Le dépassement de ce nombre génère l’erreur SQL Server 8632. Pour plus d’informations, consultez [Erreur interne : une limite des services d’expression est dépassée][Internal error: An expression services limit has been reached]. |

## <a name="metadata"></a>Métadonnées
| Vue système | Nombre maximal de lignes |
|:--- |:--- |
| Sys.dm_pdw_component_health_alerts |10 000 |
| sys.dm_pdw_dms_cores |100 |
| sys.dm_pdw_dms_workers |Nombre total de travailleurs DMS pour hello plus récent 1000 les requêtes SQL. |
| sys.dm_pdw_errors |10 000 |
| sys.dm_pdw_exec_requests |10 000 |
| sys.dm_pdw_exec_sessions |10 000 |
| sys.dm_pdw_request_steps |Nombre total d’étapes pour les demandes SQL hello 1000 la plus récente sont stockées dans sys.dm_pdw_exec_requests. |
| sys.dm_pdw_os_event_logs |10 000 |
| sys.dm_pdw_sql_requests |Hello 1000 SQL demandes les plus récentes qui sont stockées dans sys.dm_pdw_exec_requests. |

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez la rubrique [Vue d’ensemble de référence de SQL Data Warehouse][SQL Data Warehouse reference overview].

<!--Image references-->

<!--Article references-->
[Data Warehouse Units (DWU)]: ./sql-data-warehouse-overview-what-is.md
[SQL Data Warehouse reference overview]: ./sql-data-warehouse-overview-reference.md
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Tempdb]: ./sql-data-warehouse-tables-temporary.md
[data type]: ./sql-data-warehouse-tables-data-types.md
[creating a support ticket]: /sql-data-warehouse-get-started-create-support-ticket.md

<!--MSDN references-->
[Row-Overflow Data Exceeding 8 KB]: https://msdn.microsoft.com/library/ms186981.aspx
[Internal error: An expression services limit has been reached]: https://support.microsoft.com/kb/913050
