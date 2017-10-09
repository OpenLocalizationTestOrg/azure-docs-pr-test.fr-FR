---
title: "codes d’erreur aaaSQL - erreur de connexion de base de données | Documents Microsoft"
description: "En savoir plus sur les codes d’erreur SQL pour les applications clientes SQL Database, tels que les erreurs de connexion de base de données courantes, les problèmes de copie de base de données et les erreurs générales. "
keywords: "code d’erreur sql, accès sql, erreur de connexion de base de données, codes d’erreur sql"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 2a23e4ca-ea93-4990-855a-1f9f05548202
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 683a7d72c935742f3f9f9a0c683e5d8161167d6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-error-codes-for-sql-database-client-applications-database-connection-error-and-other-issues"></a>Codes d’erreur SQL pour les applications clientes SQL Database : erreur de connexion à la base de données et autres problèmes
<!--
Old Title on MSDN:  Error Messages (Azure SQL Database)
ShortId on MSDN:  ff394106.aspx
Dx 4cff491e-9359-4454-bd7c-fb72c4c452ca
-->


Cet article répertorie les codes d’erreur SQL pour les applications clientes SQL Database, y compris les erreurs de connexion de base de données, les erreurs temporaires, les erreurs de gouvernance des ressources, les problèmes de copie de base de données, le pool élastique et d’autres erreurs. La plupart des catégories sont tooAzure particulier de la base de données SQL et ne s’appliquent pas tooMicrosoft SQL Server.

## <a name="database-connection-errors-transient-errors-and-other-temporary-errors"></a>Erreurs de connexion de base de données et erreurs temporaires
Hello tableau suivant couvre les codes d’erreur SQL hello pour les erreurs de perte de connexion et d’autres erreurs temporaires que vous pouvez rencontrer lorsque votre application tente de tooaccess base de données SQL. Pour obtenir des didacticiels sur la procédure tooconnect tooAzure base de données SQL, consultez [connexion tooAzure base de données SQL](sql-database-libraries.md).

### <a name="most-common-database-connection-errors-and-transient-fault-errors"></a>Erreurs de connexion de base de données et erreurs temporaires les plus courantes
Hello infrastructure Azure a hello capacité toodynamically reconfigurer les serveurs de cas de charges de travail Bonjour service de base de données SQL.  Ce comportement dynamique peut provoquer de votre client programme toolose son tooSQL de connexion de base de données. Ce type d’erreur état est connu sous le nom d’ *erreur temporaire*.

Il est fortement recommandé que votre programme client possède une logique afin qu’il peut rétablir une connexion après avoir donné toocorrect de temps d’erreurs transitoires hello lui-même.  Nous vous recommandons de patienter 5 secondes avant votre première tentative. Une nouvelle tentative après un délai inférieur à 5 secondes risque de service de cloud hello insurmontable. Pour chaque nouvelle tentative ultérieure délai de hello doit croître de manière exponentielle, jusqu'à tooa maximale de 60 secondes.

Les erreurs temporaires se manifeste généralement comme l’un des hello messages d’erreur suivants à partir de votre programme client :

* La base de données &lt;db_name&gt; sur le serveur &lt;Azure_instance&gt; n’est pas disponible actuellement. Veuillez réessayer plus tard les connexion hello. Si hello problème persiste, contactez le support technique et fournir les ID de suivi de session hello &lt;session_id&gt;
* La base de données &lt;db_name&gt; sur le serveur &lt;Azure_instance&gt; n’est pas disponible actuellement. Veuillez réessayer plus tard les connexion hello. Si hello problème persiste, contactez le support technique et fournir les ID de suivi de session hello &lt;session_id&gt;. (Microsoft SQL Server, erreur : 40613)
* Une connexion existante a dû être fermée par l’hôte distant de hello.
* System.Data.Entity.Core.EntityCommandExecutionException : Une erreur s’est produite lors de l’exécution d’une définition de commande hello. Consultez l’exception interne pour plus d’informations hello. ---> System.Data.SqlClient.SqlException : une erreur de niveau transport s’est produite lors de la réception des résultats à partir du serveur de hello. (fournisseur : fournisseur de session, erreur : 19 - connexion physique non utilisable)
* Une base de données secondaire tooa connexion tentative a échoué, car la base de données hello est en cours de hello de reconfguration et qu’il est occupé à appliquer les nouvelles pages lors de l’intercepteur hello d’une transation active sur la base de données primaire hello. 

Pour obtenir des exemples de code de logique de nouvelle tentative, voir :

* [Bibliothèques de connexions pour SQL Database et SQL Server](sql-database-libraries.md) 
* [Erreurs de connexion toofix actions et des erreurs temporaires dans la base de données SQL](sql-database-connectivity-issues.md)

En savoir plus sur hello *la période de blocage* pour les clients qui utilisent ADO.NET est disponible dans [le regroupement de connexion SQL Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

### <a name="transient-fault-error-codes"></a>Codes d’erreur pour les erreurs temporaires
Hello erreurs suivantes sont transitoires et doivent être retentées dans la logique d’application 

| Code d'erreur | Niveau de gravité | Description |
| ---:| ---:|:--- |
| 4060 |16 |Impossible d’ouvrir de base de données « % & #x2a ; %.*ls » demandée par connexion de hello. Échec de la connexion de Hello. |
| 40197 |17 |service de Hello a rencontré une erreur lors du traitement de votre demande. Réessayez. Code d'erreur % d.<br/><br/>Vous recevez cette erreur, lorsque le service de hello est arrêté en raison de toosoftware ou mises à niveau matérielles, défaillances matérielles ou d’autres problèmes de basculement. code d’erreur Hello (%d) incorporé dans le message de type hello d’erreur 40197 fournit des informations supplémentaires sur le type de hello de défaillance ou de basculement qui s’est produite. Quelques exemples d’erreur hello codes sont incorporées dans le message d’erreur 40197 de type hello sont 40020, 40143, 40166 et 40540.<br/><br/>Serveur de base de données SQL se reconnectant tooyour se connecte automatiquement tooa la copie saine de votre base de données. Votre application doit intercepter l’erreur 40197, journal hello incorporé code d’erreur (%d) dans le message de type hello pour le dépannage et essayez de vous reconnecter tooSQL de base de données jusqu'à ce que les ressources hello sont disponibles, votre connexion est rétablie. |
| 40501 |20 |service de Hello est actuellement occupé. Renvoyez la demande de hello après 10 secondes. ID de l'incident : %ls. Code : %d.<br/><br/>*Remarque :* pour en savoir plus, consultez :<br/>• [Limites de ressources de base de données SQL Azure](sql-database-resource-limits.md). |
| 40613 |17 |La base de données ’%.&#x2a;ls’ sur le serveur ’%.&#x2a;ls’ n’est pas disponible actuellement. Veuillez réessayer plus tard les connexion hello. Si hello problème persiste, contactez le support technique et fournir les ID de suivi de session hello '% & #x2a ; %.*ls'. |
| 49918 |16 |Impossible de traiter la requête. La demande n’est pas suffisant tooprocess de ressources.<br/><br/>service de Hello est actuellement occupé. Réessayez plus tard la demande de hello. |
| 49919 |16 |Processus ne peut pas créer ou mettre à jour de la demande. Opérations de mise à jour ou de création en cours pour l'abonnement « % ld » trop nombreuses.<br/><br/>service de Hello est occupé à traiter plusieurs créer ou mettre à jour les demandes de votre abonnement ou le serveur. Les requêtes sont actuellement bloquées pour l’optimisation des ressources. Requête [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx) pour les opérations en attente. Patientez jusqu’à ce que les demandes de création ou de mise à jour soient terminées ou supprimez l’une de vos requêtes en cours et réessayez votre requête ultérieurement. |
| 49920 |16 |Impossible de traiter la requête. Opérations en cours pour l'abonnement « % ld » trop nombreuses.<br/><br/>service de Hello est occupé à traiter plusieurs demandes pour cet abonnement. Les requêtes sont actuellement bloquées pour l’optimisation des ressources. Requête [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx) pour l'état de l'opération. Patientez jusqu’à ce que les requêtes soient terminées ou supprimez l’une de vos requêtes en cours et réessayez votre requête ultérieurement. |
| 4221 |16 |Connexion tooread-secondaire a échoué en raison de l’attente toolong sur 'HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING'. réplica de Hello n’est pas disponible pour la connexion, car les versions de ligne sont manquantes pour les transactions qui étaient en cours lorsque le réplica de hello a été recyclé. Hello peut être résolu par la restauration ou de valider des transactions actives de hello sur le réplica principal de hello. Occurrences de cette condition peuvent être réduites en évitant les transactions d’écriture long sur hello principal. |

## <a name="database-copy-errors"></a>Erreurs de copie de base de données
Hello les erreurs suivantes permettre se produire lors de la copie d’une base de données dans la base de données SQL Azure. Pour en savoir plus, consultez [Copie d’une base de données SQL Azure](sql-database-copy.md).

| Code d'erreur | Niveau de gravité | Description |
| ---:| ---:|:--- |
| 40635 |16 |Le client avec l'adresse IP’%.&#x2a;ls’ est temporairement désactivé. |
| 40637 |16 |La copie de base de données est actuellement désactivée. |
| 40561 |16 |La copie de base de données a échoué. Une base de données source ou cible hello n’existe pas. |
| 40562 |16 |La copie de base de données a échoué. base de données source Hello a été supprimé. |
| 40563 |16 |La copie de base de données a échoué. base de données cible Hello a été supprimé. |
| 40564 |16 |Copie de base de données a échoué en raison de l’erreur interne de tooan. Supprimez la base de données cible et réessayez. |
| 40565 |16 |La copie de base de données a échoué. Copie de base de données simultanées pas plus de 1 à partir de la même source est autorisé de hello. Supprimez la base de données cible et réessayez ultérieurement. |
| 40566 |16 |Copie de base de données a échoué en raison de l’erreur interne de tooan. Supprimez la base de données cible et réessayez. |
| 40567 |16 |Copie de base de données a échoué en raison de l’erreur interne de tooan. Supprimez la base de données cible et réessayez. |
| 40568 |16 |La copie de base de données a échoué. La base de données source n'est plus disponible. Supprimez la base de données cible et réessayez. |
| 40569 |16 |La copie de base de données a échoué. La base de données cible n'est plus disponible. Supprimez la base de données cible et réessayez. |
| 40570 |16 |Copie de base de données a échoué en raison de l’erreur interne de tooan. Supprimez la base de données cible et réessayez ultérieurement. |
| 40571 |16 |Copie de base de données a échoué en raison de l’erreur interne de tooan. Supprimez la base de données cible et réessayez ultérieurement. |

## <a name="resource-governance-errors"></a>Erreurs de gouvernance des ressources
Hello, les erreurs suivantes est dus à une utilisation excessive des ressources lorsque vous travaillez avec la base de données SQL Azure. Par exemple :

* Votre transaction a été ouverte trop longtemps.
* Votre transaction comporte trop de verrous.
* Une application consomme trop de mémoire.
* Une application consomme trop de ressources d’espace `TempDb` .

Rubriques connexes :

* Des informations plus détaillées sont disponibles ici : [Limites de ressources de base de données SQL Azure](sql-database-resource-limits.md)

| Code d'erreur | Niveau de gravité | Description |
| ---:| ---:|:--- |
| 10928 |20 |ID de la ressource : %d. limite de %s Hello pour la base de données hello est %d et a été atteint. Pour plus d’informations, consultez [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637).<br/><br/>Hello ID de ressource indique les ressources hello qui a atteint la limite de hello. Pour les threads de travail, hello ID de ressource = 1. Pour les sessions, hello ID de ressource = 2.<br/><br/>*Remarque :* pour plus d’informations sur cette erreur et comment tooresolve, consultez :<br/>• [Limites de ressources de base de données SQL Azure](sql-database-resource-limits.md). |
| 10929 |20 |ID de la ressource : %d. garantie minimale de %s Hello est %d, le nombre maximal est %d et l’utilisation actuelle de hello pour la base de données hello est %d. Toutefois, hello serveur est actuellement trop occupé toosupport les demandes supérieures à %d pour cette base de données. Pour plus d’informations, consultez [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637). Sinon, réessayez plus tard.<br/><br/>Hello ID de ressource indique les ressources hello qui a atteint la limite de hello. Pour les threads de travail, hello ID de ressource = 1. Pour les sessions, hello ID de ressource = 2.<br/><br/>*Remarque :* pour plus d’informations sur cette erreur et comment tooresolve, consultez :<br/>• [Limites de ressources de base de données SQL Azure](sql-database-resource-limits.md). |
| 40544 |20 |base de données Hello a atteint son quota de taille. Partitionnez ou supprimez des données, drop index ou consultez la documentation de hello pour les résolutions possibles. |
| 40549 |16 |La session est arrêtée, car l’une des transactions est de longue durée. Essayez de la raccourcir. |
| 40550 |16 |session de Hello a été arrêtée car elle a acquis trop de verrous. Essayez de lire ou de modifier moins de lignes dans une transaction unique. |
| 40551 |16 |session de Hello a été arrêtée en raison d’excessive `TEMPDB` utilisation. Essayez de modifier votre requête tooreduce hello table temporaire utilisation de l’espace.<br/><br/>*Conseil :* si vous utilisez des objets temporaires, conservez l’espace dans hello `TEMPDB` base de données en supprimant des objets temporaires une fois qu’ils ne sont plus nécessaires par session de hello. |
| 40552 |16 |session de Hello a été arrêtée en raison de l’utilisation de l’espace de journal des transactions excessive. Essayez de modifier moins de lignes dans une transaction unique.<br/><br/>*Conseil :* si vous effectuez des insertions en bloc à l’aide de hello `bcp.exe` utilitaire ou hello `System.Data.SqlClient.SqlBulkCopy` de classe, essayez d’utiliser hello `-b batchsize` ou `BatchSize` nombre de hello toolimit options de lignes copiées toohello serveur lors de chaque transaction. Si vous reconstruisez un index avec hello `ALTER INDEX` instruction, essayez d’utiliser hello `REBUILD WITH ONLINE = ON` option. |
| 40553 |16 |session de Hello a été arrêtée en raison de l’utilisation de mémoire excessive. Essayez de modifier votre requête tooprocess moins de lignes.<br/><br/>*Conseil :* en réduisant le nombre hello de `ORDER BY` et `GROUP BY` opérations dans votre code Transact-SQL réduit les besoins en mémoire hello de votre requête. |

## <a name="elastic-pool-errors"></a>Erreurs relatives au pool élastique
Hello, les erreurs suivantes est associée toocreating et l’utilisation de Pools d’ELASTIQUES.

| ErrorNumber | ErrorSeverity | ErrorFormat | ErrorInserts | ErrorCause | ErrorCorrectiveAction |
|:--- |:--- |:--- |:--- |:--- |:--- |
| 1132 |EX_RESOURCE |pool élastique de Hello a atteint sa limite de stockage. l’utilisation du stockage pour le pool élastique de hello Hello ne peut pas dépasser le nombre de Mo (%d). |Limite de l’espace du pool élastique, en Mo. |Tentative de toowrite données tooa base de données lors de la limite de stockage hello du pool élastique de hello a été atteinte. |Veuillez prendre en compte les dtu hello croissante de hello pool élastique si possible dans l’ordre tooincrease sa limite de stockage, réduire le stockage hello utilisé par les bases de données individuelles au sein du pool élastique de hello ou supprimer des bases de données à partir du pool élastique de hello. |
| 10929 |EX_USER |garantie minimale de %s Hello est %d, le nombre maximal est %d et l’utilisation actuelle de hello pour la base de données hello est %d. Toutefois, hello serveur est actuellement trop occupé toosupport les demandes supérieures à %d pour cette base de données. Voir [https://msdn.microsoft.com/library/azure/dn338078.aspx](http://go.microsoft.com/fwlink/?LinkId=267637) pour obtenir de l’aide. Sinon, réessayez plus tard. |Nombre minimal de DTU par base de données ; nombre maximal de DTU par base de données. |Bonjour nombre total de threads de travail simultanés (demandes) sur toutes les bases de données dans la limite du pool hello pool élastique tooexceed tentative hello. |Veuillez augmentez hello dtu de hello pool élastique si possible dans l’ordre tooincrease sa limite de processus de travail, ou supprimer des bases de données à partir du pool élastique de hello. |
| 40844 |EX_USER |La base de données '%ls' sur le serveur '%ls' est une base de données présentant l’édition '%ls' dans un pool élastique. Elle ne peut pas présenter de relation de copie continue. |Nom de la base de données, édition de la base de données, nom du serveur |Une commande StartDatabaseCopy est émise pour une base de données non-Premium dans un pool élastique. |Bientôt disponible |
| 40857 |EX_USER |Pool élastique introuvable pour le serveur : '%ls'. Nom du pool élastique: '%ls'. |Nom du serveur, nom du pool élastique |Un pool élastique spécifié n’existe pas dans le serveur spécifié de hello. |Saisissez un nom de pool élastique valide. |
| 40858 |EX_USER |Le pool élastique '%ls' existe déjà sur le serveur : '%ls'. |Nom du pool élastique, nom du serveur |Un pool élastique spécifié existe déjà dans le serveur logique de hello spécifié. |Saisissez un nouveau nom pour le pool élastique. |
| 40859 |EX_USER |Le pool élastique ne prend pas en charge le niveau de service '%ls'. |Niveau de service du pool élastique |Le niveau de service spécifié n’est pas pris en charge pour le provisioning du pool élastique. |Fournir l’édition appropriée de hello ou laissez le niveau de service par défaut service couche vide toouse hello. |
| 40860 |EX_USER |La combinaison du pool élastique '%ls' et de l’objectif de service '%ls' n’est pas valide. |Nom du pool élastique, nom de l’objectif de niveau de service |L’objectif de service et le pool élastique peuvent être spécifiés ensemble uniquement si le premier est indiqué en tant que « ElasticPool ». |Spécifiez la combinaison de pool élastique et d’objectif de service adéquate. |
| 40861 |EX_USER |Édition de base de données Hello ' %. *%.*ls ne peut pas être différents de celui de niveau de service de pool élastique hello qui est ' %.* %.*ls. |Édition de base de données, niveau de service du pool élastique |Édition de base de données Hello est différente de celui de niveau de service du pool élastique hello. |Ne spécifiez pas une édition de base de données qui est différente de celui de niveau de service du pool élastique hello.  Notez que cette édition de base de données hello n’a pas besoin toobe spécifié. |
| 40862 |EX_USER |Nom du pool élastique doit être spécifié si l’objectif de service du pool élastique hello est spécifié. |Aucun |L’objectif de service du pool élastique n’identifie pas de manière unique un pool élastique. |Spécifiez le nom du pool élastique hello si l’objectif de service du pool élastique hello. |
| 40864 |EX_USER |Hello dtu pour le pool élastique de hello doit contenir au moins (%d) dtu pour le niveau de service ' %. * ls'. |Nombre de DTU du pool élastique, niveau de service du pool élastique |Tentative de hello tooset dtu pour le pool élastique de hello sous la limite minimale de hello. |Veuillez réessayer définissant dtu hello pour hello pool élastique tooat moins limite minimale de hello. |
| 40865 |EX_USER |Hello dtu pour le pool élastique de hello ne peut pas dépasser (%d) dtu pour le niveau de service ' %. * ls'. |Nombre de DTU du pool élastique, niveau de service du pool élastique |Tentative de hello tooset dtu pour le pool élastique de hello au-dessus de limite maximale de hello. |Veuillez réessayer de paramètre dtu hello pour hello pool élastique toono supérieure à la limite maximale de hello. |
| 40867 |EX_USER |Hello maximum de DTU par base de données doit être d’au moins (%d) pour le niveau de service ' %. * ls'. |Nombre maximal de DTU par base de données, niveau de service du pool élastique |Tentative tooset hello maximum de DTU par base de données ci-dessous hello la limite autorisée. |Envisagez d’utiliser le niveau de service de pool élastique hello qui prend en charge les paramètre hello souhaité. |
| 40868 |EX_USER |Hello maximum de DTU par base de données ne peut pas dépasser (%d) pour le niveau de service ' %. * ls'. |Nombre maximal de DTU par base de données, niveau de service du pool élastique |Tentative tooset hello maximum de DTU par base de données au-delà de hello la limite autorisée. |Envisagez d’utiliser le niveau de service de pool élastique hello qui prend en charge les paramètre hello souhaité. |
| 40870 |EX_USER |Hello nombre minimal de DTU par base de données ne peut pas dépasser (%d) pour le niveau de service ' %. * ls'. |Nombre minimal de DTU par base de données, niveau de service du pool élastique |Tentative tooset hello nombre minimal de DTU par base de données au-delà de hello la limite autorisée. |Envisagez d’utiliser le niveau de service de pool élastique hello qui prend en charge les paramètre hello souhaité. |
| 40873 |EX_USER |nombre de Hello de bases de données (%d) et le nombre minimal de DTU par base de données (%d) ne peut pas dépasser la dtu hello du pool élastique de hello (%d). |Nombre de bases de données dans le pool élastique ; nombre minimal de DTU par base de données ; DTU du pool élastique |Tentative de nombre minimal de DTU toospecify pour les bases de données dans le pool élastique hello qui dépasse hello dtu du pool élastique de hello. |Envisagez d’augmenter hello dtu du pool élastique de hello, ou diminuer hello nombre minimal de DTU par base de données ou diminuer le nombre de hello de bases de données dans le pool élastique de hello. |
| 40877 |EX_USER |Impossible de supprimer un pool élastique, sauf s’il ne contient aucune base de données. |Aucun |pool élastique de Hello contient une ou plusieurs bases de données et ne peut donc pas être supprimé. |Veuillez supprimer les bases de données à partir du pool élastique de hello dans l’ordre toodelete il. |
| 40881 |EX_USER |Hello pool élastique ' %. * ls' a atteint sa limite de nombre de base de données.  limite du nombre de base de données pour le pool élastique de hello Hello ne peut pas dépasser (%d) pour un pool élastique dtu (%d). |Nom du pool élastique ; nombre limite de bases de données du pool élastique ; DTU du pool de ressources. |Tentative toocreate ou ajouter un pool de tooelastic de base de données lors de la limite du nombre de base de données du pool élastique de hello hello a été atteint. |Veuillez augmentez hello dtu de hello pool élastique si possible dans l’ordre tooincrease sa limite de base de données, ou supprimer des bases de données à partir du pool élastique de hello. |
| 40889 |EX_USER |Hello dtu ou la limite de stockage pour le pool élastique de hello ' %. * ls' ne peut être diminués depuis qui ne fournirait pas d’espace de stockage pour ses bases de données. |Nom du pool élastique. |Tentative de limite de stockage toodecrease hello du pool élastique de hello sous son utilisation du stockage. |Pensez à réduire l’utilisation du stockage des bases de données dans le pool élastique de hello hello ou supprimer des bases de données à partir du pool hello dans l’ordre tooreduce sa dtu ou le stockage limite. |
| 40891 |EX_USER |Hello nombre minimal de DTU par base de données (%d) ne peut pas dépasser hello DTU maximale par base de données (%d). |Nombre minimal de DTU par base de données ; nombre maximal de DTU par base de données |Tentative de tooset hello nombre minimal de DTU par base de données supérieure à hello maximum de DTU par base de données. |Vérifiez que le nombre minimal de DTU hello par les bases de données ne dépasse pas hello maximum de DTU par base de données. |
| TBD |EX_USER |taille du stockage Hello pour une base de données individuel dans un pool élastique ne peut pas dépasser la taille maximale de hello autorisée par ' %. * ls' pool élastique de niveau de service. |Niveau de service du pool élastique |taille maximale de Hello pour la base de données hello dépasse la taille de max de hello autorisée par niveau de service du pool élastique hello. |Définissez la taille maximale de hello de base de données hello dans les limites de hello la taille maximale autorisée par le niveau de service du pool élastique hello hello. |

Rubriques connexes :

* [Créer un pool élastique (C#)](sql-database-elastic-pool-manage-csharp.md) 
* [Gérer un pool élastique (C#)](sql-database-elastic-pool-manage-csharp.md). 
* [Créer un pool élastique (PowerShell)](sql-database-elastic-pool-manage-powershell.md) 
* [Surveiller et gérer un pool élastique (PowerShell)](sql-database-elastic-pool-manage-powershell.md).

## <a name="general-errors"></a>Erreurs générales.
Hello les erreurs suivantes n’est pas toutes les catégories précédentes.

| Code d'erreur | Niveau de gravité | Description |
| ---:| ---:|:--- |
| 15006 |16 |<AdministratorLogin> n’est pas un nom valide, car il contient des caractères non valides. |
| 18452 |14 |La connexion a échoué. Hello connexion provient d’un domaine non approuvé et ne peut pas être utilisée avec Windows authentication.%. & #x2a ; %.*ls (les connexions Windows ne sont pas pris en charge dans cette version de SQL Server.) |
| 18456 |14 |Échec de la connexion pour l’utilisateur ' % #x2a;ls'.%. & #x2a ; % ls. & #x2a ; %.*ls (Échec de la connexion de hello pour l’utilisateur « % & #x2a ; %.*ls ». Échec du changement de mot de passe Hello. La modification du mot de passe lors de la connexion n'est pas prise en charge dans cette version de SQL Server.) |
| 18470 |14 |Échec de la connexion pour l'utilisateur '%.&#x2a;ls'. Raison : le compte de hello est disabled.%. & #x2a ; %.*ls |
| 40014 |16 |Plusieurs bases de données ne peut pas être utilisés dans hello même transaction. |
| 40054 |16 |Les tables sans index de cluster ne sont pas prises en charge dans cette version de SQL Server. Créez un index de cluster et réessayez. |
| 40133 |15 |Cette opération n'est pas prise en charge dans cette version de SQL Server. |
| 40506 |16 |Le SID spécifié n'est pas valide pour cette version de SQL Server. |
| 40507 |16 |'%.&#x2a;ls' ne peut pas être appelé avec des paramètres dans cette version de SQL Server. |
| 40508 |16 |L’instruction USE n’est pas pris en charge tooswitch entre bases de données. Utiliser une connexion tooconnect tooa autre base de données. |
| 40510 |16 |L'instruction '%.&#x2a;ls' n'est pas prise en charge dans cette version de SQL Server |
| 40511 |16 |La fonction intégrée '%.&#x2a;ls' n'est pas prise en charge dans cette version de SQL Server. |
| 40512 |16 |La fonctionnalité déconseillée '%ls' n'est pas prise en charge dans cette version de SQL Server. |
| 40513 |16 |La variable de serveur '%.&#x2a;ls' n'est pas prise en charge dans cette version de SQL Server. |
| 40514 |16 |'%.ls' n'est pas pris en charge dans cette version de SQL Server. |
| 40515 |16 |Nom de référence toodatabase et/ou au serveur en '%. & #x2a ; %.*ls' n’est pas pris en charge dans cette version de SQL Server. |
| 40516 |16 |Les objets temporaires globaux ne sont pas pris en charge dans cette version de SQL Server. |
| 40517 |16 |Le mot clé ou l'option d'instruction '%.&#x2a;ls' n'est pas pris en charge dans cette version de SQL Server. |
| 40518 |16 |La commande DBCC '%.&#x2a;ls' n'est pas prise en charge dans cette version de SQL Server. |
| 40520 |16 |La classe sécurisable '%S_MSG' n'est pas prise en charge dans cette version de SQL Server. |
| 40521 |16 |Classe sécurisable '% S_MSG' est pas pris en charge dans l’étendue du serveur hello dans cette version de SQL Server. |
| 40522 |16 |Le type de base de données principal '%.&#x2a;ls' n'est pas pris en charge dans cette version de SQL Server. |
| 40523 |16 |La création de l'utilisateur implicite '%.&#x2a;ls' n'est pas prise en charge dans cette version de SQL Server. Créer explicitement l’utilisateur de hello avant de l’utiliser. |
| 40524 |16 |Le type de données '%.&#x2a;ls' n'est pas pris en charge dans cette version de SQL Server. |
| 40525 |16 |WITH '%.ls' n'est pas en charge cette version de SQL Server. |
| 40526 |16 |Le fournisseur d'ensemble de lignes '%.&#x2a;ls' n'est pris en charge dans cette version de SQL Server. |
| 40527 |16 |Les serveurs liés ne sont pas pris en charge dans cette version de SQL Server. |
| 40528 |16 |Les utilisateurs ne peuvent pas être mappé toocertificates, clés asymétriques ou des connexions Windows dans cette version de SQL Server. |
| 40529 |16 |La fonction intégrée '%.&#x2a;ls' dans le contexte d'emprunt d'identité n'est pas prise en charge dans cette version de SQL Server. |
| 40532 |11 |Impossible d’ouvrir le serveur « % & #x2a ; %.*ls » demandée par connexion de hello. Échec de la connexion de Hello. |
| 40553 |16 |session de Hello a été arrêtée en raison de l’utilisation de mémoire excessive. Essayez de modifier votre requête tooprocess moins de lignes.<br/><br/>*Remarque :* en réduisant le nombre hello de `ORDER BY` et `GROUP BY` opérations dans votre code Transact-SQL permet de réduire les besoins en mémoire hello de votre requête. |
| 40604 |16 |Impossible de CREATE/ALTER pas la base de données, car il dépasserait le quota hello du serveur de hello. |
| 40606 |16 |L'association de bases de données n'est pas prise en charge dans cette version de SQL Server. |
| 40607 |16 |Les connexions Windows ne sont pas prises en charge dans cette version de SQL Server. |
| 40611 |16 |Les serveurs peuvent avoir au maximum 128 règles de pare-feu définies. |
| 40614 |16 |L'adresse IP de début de la règle de pare-feu ne peut pas dépasser l'adresse IP de fin. |
| 40615 |16 |Impossible d’ouvrir le serveur '{0}' demandé par connexion de hello. Client avec l’adresse IP « {{1} » n’est pas autorisé serveur hello de tooaccess.  tooenable accès, utilisez hello portail de base de données SQL ou exécutez sp_set_firewall_rule sur la base de données master de hello toocreate une règle de pare-feu pour cette adresse IP ou une plage d’adresses.  Cela peut prendre jusqu'à minutes toofive pour cette modification tootake effet. |
| 40617 |16 |nom de règle de pare-feu Hello qui commence par <rule name> est trop long. La longueur maximale est 128. |
| 40618 |16 |nom de règle de pare-feu Hello ne peut pas être vide. |
| 40620 |16 |Échec de la connexion de Hello pour l’utilisateur « % & #x2a ; %.*ls ». Échec du changement de mot de passe Hello. La modification du mot de passe lors de la connexion n'est pas prise en charge dans cette version de SQL Server. |
| 40627 |20 |L'opération sur le serveur '{0}' et la base de données '{1}' est en cours. Veuillez patienter quelques minutes avant de réessayer. |
| 40630 |16 |Échec de la validation de mot de passe. mot de passe Hello ne respecte pas les exigences de la stratégie, car il est trop court. |
| 40631 |16 |mot de passe Hello que vous avez spécifié est trop long. mot de passe Hello doit avoir pas plus de 128 caractères. |
| 40632 |16 |Échec de la validation de mot de passe. mot de passe Hello ne respecte pas les exigences de la stratégie, car il n’est pas assez complexe. |
| 40636 |16 |Impossible d'utiliser un nom de base de données réservé '%.&#x2a;ls' dans cette opération. |
| 40638 |16 |ID d’abonnement <subscription-id> non valide. L'abonnement n'existe pas. |
| 40639 |16 |Demande n’est pas conforme tooschema : <schema error>. |
| 40640 |20 |serveur de Hello a rencontré une exception inattendue. |
| 40641 |16 |Hello spécifié l’emplacement n’est pas valide. |
| 40642 |17 |Hello serveur est actuellement trop occupé. Veuillez réessayer plus tard. |
| 40643 |16 |Hello spécifié la valeur de l’en-tête x-ms-version n’est pas valide. |
| 40644 |14 |Échec tooauthorize accès toohello spécifié abonnement. |
| 40645 |16 |Le nom de serveur <servername> ne peut pas être vide ou nul. Il peut uniquement être constitué de lettres minuscules 'a'-'z', les numéros de hello 0-9 et trait d’union hello. trait d’union Hello ne peut pas aboutir ou fin hello nom. |
| 40646 |16 |L'ID d'abonnement ne peut pas être vide. |
| 40647 |16 |L'abonnement <subscription-id ne contient pas de nom de serveur. |
| 40648 |17 |Trop de demandes ont été effectuées. Veuillez réessayer ultérieurement. |
| 40649 |16 |Un type de contenu non valide est spécifié. Seul application/xml est pris en charge. |
| 40650 |16 |Abonnement < ID_ABONNEMENT > n’existe pas ou n’est pas prêt pour l’opération de hello. |
| 40651 |16 |Échec de toocreate serveur, car l’abonnement < ID_ABONNEMENT > hello est désactivé. |
| 40652 |16 |Impossible de déplacer ou de créer le serveur. L'abonnement <subscription-id> va dépasser le quota du serveur. |
| 40671 |17 |Échec de communication entre la passerelle de hello et le service de gestion hello. Veuillez réessayer ultérieurement. |
| 40852 |16 |Impossible d’ouvrir de base de données ' %. *! sur le serveur ' %.* %.*ls demandé par connexion de hello. Base de données Access toohello est autorisée uniquement à l’aide d’une chaîne de connexion à sécurité activée. tooaccess cette base de données, modifiez votre toocontain de chaînes de connexion sécurisée dans le serveur de hello FQDN - nom du serveur.database.windows .net doit être modifié too'server nom '.database. `secure`. windows.net. |
| 45168 |16 |Hello système SQL Azure est sous charge et spécifie une limite supérieure sur les opérations CRUD de base de données simultanées pour un serveur unique (par exemple, créer la base de données). serveur Hello spécifié dans le message d’erreur hello a dépassé le nombre maximal de hello de connexions simultanées. Réessayez ultérieurement. |
| 45169 |16 |Hello système SQL azure est sous charge et place une limite supérieure sur le nombre de hello d’opérations CRUD simultanées sur un seul abonnement (par exemple, créer le serveur). abonnement de Hello spécifié dans l’erreur de hello message a dépassé le nombre maximal de hello de connexions simultanées et hello demande a été refusée. Réessayez ultérieurement. |

## <a name="related-links"></a>Liens connexes
* [Fonctionnalités d’Azure SQL Database](sql-database-features.md)
* [Limites de ressources de base de données SQL Azure](sql-database-resource-limits.md)

