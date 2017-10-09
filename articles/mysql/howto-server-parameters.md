---
title: "aaaHow tooConfigure paramètres du serveur dans la base de données Azure pour MySQL | Documents Microsoft"
description: "Cet article décrit comment tooconfigure les paramètres de serveur disponible dans la base de données Azure pour l’utilisation de MySQL hello portail Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/19/2017
ms.openlocfilehash: 8292c8eda605854a06b6a9c82185c857bd353cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-server-parameters-in-azure-database-for-mysql-using-hello-azure-portal"></a>Comment tooconfigure les paramètres de serveur dans la base de données Azure pour l’utilisation de MySQL hello portail Azure

Azure Database pour MySQL prend en charge la configuration de certains paramètres de serveur. Cet article décrit comment tooconfigure ces paramètres à l’aide de hello portail Azure et les listes hello prises en charge les paramètres, les valeurs par défaut hello et hello plage de valeurs valides. Les paramètres du serveur ne sont pas tous modifiables. Uniquement hello répertoriés ici sont pris en charge.

## <a name="navigate-tooserver-parameters-blade-on-azure-portal"></a>Accédez tooServer panneau des paramètres sur le portail Azure

Connectez-vous à toohello portail Azure, puis cliquez sur votre base de données Azure pour le nom du serveur MySQL. Sous hello **paramètres** , cliquez sur **paramètres serveur** Panneau de paramètres serveur tooopen hello pour hello Azure de base de données de MySQL.

![Panneau Paramètres du serveur du portail Azure](./media/howto-server-parameters/auzre-portal-server-parameters.png)

## <a name="list-of-configurable-server-parameters"></a>Liste des paramètres de serveur configurables

Hello tableau suivant répertorie les paramètres de serveur hello actuellement pris en charge. paramètres de Hello peuvent être configurés en fonction des exigences de l’application tooyour.

> [!div class="mx-tableFixed"]
|Nom du paramètre|Valeur par défaut|Plage|Description|
|---|---|---|---|
|binlog_group_commit_sync_delay|1 000|0, 11-1000000|Contrôle le nombre de microsecondes hello journal binaire des attentes de validation avant la synchronisation toodisk de fichier journal binaire hello.|
|binlog_group_commit_sync_no_delay_count|0|0-1000000|nombre maximal de Hello de toowait de transactions pour avant d’abandonner le délai de hello actuel tel que spécifié par binlog-groupe-validation-sync-delay.|
|character_set_server|LATIN1|BIG5, UTF8MB4, etc.|Utilisez nom_jeu_caractères comme jeu de caractères du serveur hello par défaut.|
|div_precision_increment|4|0-30|Nombre de chiffres par quelle échelle de hello tooincrease du résultat de hello d’opérations de division.|
|group_concat_max_len|1 024|4-16777216|Longueur du résultat autorisée maximale en octets pour hello GROUP_CONCAT().|
|innodb_adaptive_hash_index|ACTIVÉ|ON, OFF|Indique si les index de hachage adaptatifs innodb sont activés ou désactivés.|
|innodb_lock_wait_timeout|50|1-3600|Durée Hello en secondes une transaction InnoDB attend un verrou de ligne avant d’abandonner.|
|interactive_timeout|1 800|10-1800|Numéro du serveur de hello secondes attend que l’activité sur une connexion interactive avant sa fermeture.|
|log_bin_trust_function_creators|ÉTEINT|ON, OFF|Cette variable s’applique lorsque la journalisation binaire est activée. Elle contrôle si des fonctions stockées créateurs peuvent être approuvée toocreate stockée pas les fonctions qui permettent aux toobe événements unsafe écrite toohello journal binaire des événements.|
|log_queries_not_using_indexes|ÉTEINT|ON, OFF|Requêtes de journaux qui sont attendus tooretrieve toutes les lignes tooslow du journal.|
|log_slow_admin_statements|ÉTEINT|ON, OFF|Inclut des instructions d’administration lentes dans les instructions de hello écrites le journal des requêtes lentes toohello.|
|log_throttle_queries_not_using_indexes|0|0-4294967295|Limites hello nombre de telles requêtes par minute qui peuvent être écrites toohello journal des requêtes lentes.|
|long_query_time|10|1-1E+100|Si une requête dure plus longtemps que ce nombre de secondes, serveur de hello incrémente la variable d’état Slow_queries hello.|
|max_allowed_packet|536870912|1024-1073741824|taille maximale de Hello de n’importe quel paramètre envoyé par hello mysql_stmt_send_long_data() fonction d’API C, un seul paquet ou n’importe quelle chaîne/intermédiaire généré.|
|min_examined_row_limit|0|0-18446744073709551615|Journalise les requêtes qui ont supérieur au nombre de hello configuré de lignes dans le journal des requêtes lentes hello. |
|server_id|3293747068|1000-4294967295|ID du serveur Hello, utilisée dans la réplication toogive chaque maître et esclave une identité unique.|
|slave_net_timeout|60|30-3600|nombre de Hello de toowait secondes plus de données à partir du maître hello avant que les esclave hello considère comme connexion hello résiliée, abandonne hello lire et tente de tooreconnect.|
|slow_query_log|ÉTEINT|ON, OFF|Activer ou désactiver le journal des requêtes lentes hello.|
|sql_mode|0 sélectionné|ALLOW_INVALID_DATES, IGNORE_SPACE, etc.|mode SQL server actuel Hello.|
|time_zone|SYSTEM|exemples : -8:00, +05:30|fuseau horaire du serveur Hello.|
|wait_timeout|120|60-240|nombre de Hello du serveur de hello secondes attend que l’activité sur une connexion non interactive avant sa fermeture.|

## <a name="next-steps"></a>Étapes suivantes
- [Bibliothèques de connexions de la base de données Azure pour MySQL](concepts-connection-libraries.md)
