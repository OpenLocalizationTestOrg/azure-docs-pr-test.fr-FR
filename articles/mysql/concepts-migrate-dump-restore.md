---
title: "aaaMigrate votre base de données MySQL à l’aide de vidage et la restauration dans la base de données Azure pour MySQL | Documents Microsoft"
description: "Cet article explique les deux tooback de façons courantes d’et de restauration des bases de données dans votre base de données Azure pour MySQL, à l’aide des outils tels que mysqldump, banc d’essai MySQL et PHPMyAdmin."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: d05d483ff53483df8e005eae2d9a4f8190e8f663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-tooazure-database-for-mysql-using-dump-and-restore"></a>Migrer votre tooAzure de base de données de base de données MySQL pour MySQL à l’aide de vidage et restauration
Cet article explique deux tooback façons courantes d’et restaurer des bases de données dans votre base de données Azure pour MySQL
- Vidage et la restauration à partir de hello de ligne de commande (à l’aide de mysqldump) 
- Sauvegarder et restaurer à l’aide de PHPMyAdmin 

## <a name="before-you-begin"></a>Avant de commencer
toostep via ce tooguide de procédure, vous devez toohave :
- [Créer un serveur de base de données Azure pour MySQL - Portail Azure](quickstart-create-mysql-server-database-using-azure-portal.md)
- Utilitaire de ligne de commande [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html) installé sur une machine
- Banc d’essai MySQL [télécharger MySQL le banc d’essai](https://dev.mysql.com/downloads/workbench/), adresse :, Navicat ou autres toodo d’outil tiers MySQL dump et restaurer les commandes.

## <a name="use-common-tools"></a>Utiliser des outils courants
Utilisez les utilitaires communs et des outils tels que tooremotely banc d’essai MySQL, mysqldump, adresse : ou Navicat se connecter et restaurer des données dans la base de données Azure pour MySQL. Utilisez ces outils sur votre ordinateur client avec un toohello de tooconnect de connexion internet de la base de données Azure pour MySQL. Utilisez une connexion chiffrée SSL pour appliquer les meilleures pratiques de sécurité ; consultez également la page [Configurer la connectivité SSL dans la base de données Azure pour MySQL](concepts-ssl-connection-security.md). Vous n’avez besoin d’emplacement cloud spéciaux tooany des fichiers de vidage toomove hello lors de la migration tooAzure de base de données de MySQL. 

## <a name="common-uses-for-dump-and-restore"></a>Utilisations courantes de la sauvegarde et de la restauration
Vous pouvez utiliser les utilitaires de MySQL telles que mysqldump mysqlpump toodump et charge bases de données et dans une base de données MySQL de Azure dans plusieurs scénarios courants. Dans d’autres scénarios, vous pouvez utiliser hello [importer et exporter](concepts-migrate-import-export.md) approche à la place.

- Base de données utiliser vide lors de la migration de base de données entière hello. Cette recommandation conserve lors du déplacement d’une grande quantité de données MySQL, ou lorsque vous souhaitez toominimize interruption du service pour les applications ou sites actifs. 
-  Assurez-vous que toutes les tables de base de données hello utilisent le moteur de stockage InnoDB hello lors du chargement de données dans la base de données Azure pour MySQL. La base de données Azure pour MySQL prend en charge le moteur de stockage InnoDB uniquement. Par conséquent, elle ne prend pas en charge les autres moteurs de stockage. Si vos tables sont configurés avec les autres moteurs de stockage, les convertir en un format de moteur hello InnoDB avant d’être tooAzure de migration de base de données de MySQL.
   Par exemple, si vous avez un WordPress ou une application Web à l’aide des tables de MyISAM hello, d’abord convertir ces tables en effectuant une migration dans le format de InnoDB avant la restauration de base de données de tooAzure pour MySQL. Clause de hello utilisation `ENGINE=InnoDB` tooset hello moteur utilisé lors de la création d’une nouvelle table, puis transférer les données de hello dans table compatible de hello avant la restauration de hello. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```
- problèmes de n’importe quel compatibilité tooavoid, vérifiez que hello même version de MySQL est utilisée sur les systèmes source et de destination hello lors du vidage de bases de données. Par exemple, si votre serveur MySQL existant est la version 5.7, vous devez migrer tooAzure de base de données MySQL configuré toorun version 5.7. Hello `mysql_upgrade` commande ne fonctionne pas dans une base de données Azure pour MySQL server et n’est pas pris en charge. Si vous devez tooupgrade entre les versions de MySQL, tout d’abord dump ou exporter votre base de données de version inférieur dans une version ultérieure de MySQL dans votre propre environnement. Ensuite, exécutez `mysql_upgrade` avant de tenter une migration vers une base de données Azure pour MySQL.

## <a name="performance-considerations"></a>Considérations relatives aux performances
toooptimize performances, prenez les avis de ces considérations lors du vidage de grandes bases de données :
-   Hello d’utilisation `exclude-triggers` option mysqldump lors du vidage de bases de données. Exclure déclenche à partir des fichiers de vidage des commandes de déclencheur de hello tooavoid déclencher pendant la restauration des données hello. 
-   Éviter hello `single-transaction` option mysqldump lors du vidage de bases de données très volumineuses. Le vidage de tables dans une seule transaction provoque l’espace de stockage supplémentaire et toobe des ressources de mémoire consommée pendant la restauration et peut entraîner des retards de performances ou des contraintes de ressources.
-   Insertions de valeurs multiples utilisation lors du chargement d’une charge de SQL toominimize instruction d’exécution lors du vidage de bases de données. Lorsque vous utilisez des fichiers de sauvegarde générés par l’utilitaire mysqldump, les insertions à valeurs multiples sont activées par défaut. 
-  Hello d’utilisation `order-by-primary` option mysqldump lors du vidage de bases de données, afin que les données de salutation sont écrit dans l’ordre des clés primaire.
-   Hello d’utilisation `disable-keys` option mysqldump lors du vidage des données, contraintes de clé étrangère toodisable avant le chargement. La désactivation des vérifications de clé étrangère offre des gains de performances. Activer les contraintes de hello et vérifier les données de hello après l’intégrité référentielle hello charge tooensure.
-   Utilisez des tables partitionnées le cas échéant.
-   Chargez les données en parallèle. Éviter de trop de parallélisme serait vous entraîner toohit une limite de ressource et de surveillance des ressources à l’aide de mesures hello disponibles dans hello portail Azure. 
-   Hello d’utilisation `defer-table-indexes` option mysqlpump lors du vidage de bases de données, afin que la création d’index se produit après le chargement de données de tables.

## <a name="create-a-backup-file-from-hello-command-line-using-mysqldump"></a>Créer un fichier de sauvegarde à partir de hello de ligne de commande à l’aide de mysqldump
tooback une base de données MySQL existante sur le serveur de site local hello ou dans une machine virtuelle, exécutez hello de commande suivante : 
```bash
$ mysqldump --opt -u [uname] -p[pass] [dbname] > [backupfile.sql]
```

Hello paramètres tooprovide sont les suivantes :
- [uname] le nom d’utilisateur de votre base de données ; 
- [réussite] hello mot de passe pour votre base de données (Notez il n’existe aucun espace entre-p et le mot de passe hello) 
- nom de hello [dbname] de votre base de données 
- nom de fichier [backupfile.sql] hello pour sauvegarder votre base de données 
- [--opt] hello mysqldump option 

Par exemple, tooback une base de données nommé « testdb » sur votre serveur MySQL avec nom d’utilisateur de hello « testuser » et aucun testdb_backup.sql de fichier de mot de passe tooa, utilisez hello commande suivante. Hello commande sauvegarde hello `testdb` base de données dans un fichier appelé `testdb_backup.sql`, qui contient toutes les instructions SQL de hello nécessaire toore-créer hello de base de données. 

```bash
$ mysqldump -u root -p testdb > testdb_backup.sql
```
tooselect des tables spécifiques dans votre tooback de base de données des, Lister les noms de table hello séparant par des espaces. Par exemple, tooback des tables de table1 et table2 uniquement à partir de hello « testdb », suivre cet exemple : 
```bash
$ mysqldump -u root -p testdb table1 table2 > testdb_tables_backup.sql
```

tooback plus d’une base de données en une seule fois, utilisez hello--basculer de base de données et les noms de base de données de liste hello séparant par des espaces. 
```bash
$ mysqldump -u root -p --databases testdb1 testdb3 testdb5 > testdb135_backup.sql 
```
tooback toutes les bases de données hello dans server hello en même temps, vous devez utiliser hello : option de toutes les bases de données.
```
$ mysqldump -u root -p --all-databases > alldb_backup.sql 
```

## <a name="create-a-database-on-hello-target-azure-database-for-mysql-server"></a>Créer une base de données sur la cible de hello Azure de base de données du serveur MySQL
Créer une base de données vide sur la cible de hello de base de données Azure pour MySQL server où vous souhaitez toomigrate hello données. Utilisez un outil tel que MySQL banc d’essai, adresse : Navicat toocreate hello base de données ou. base de données Hello peut avoir hello comme hello base de données des données de relation contenant-contenu hello exportée du même nom, ou vous pouvez créer une base de données avec un nom différent.

tooget connecté, recherchez des informations de connexion hello sur la page de propriétés hello dans votre base de données Azure pour MySQL.
![Rechercher des informations de connexion hello Bonjour portail Azure](./media/concepts-migrate-dump-restore/1_server-properties-name-login.png)

Ajouter des informations de connexion de hello dans votre atelier de MySQL.
![Chaîne de connexion MySQL Workbench](./media/concepts-migrate-dump-restore/2_setup-new-connection.png)


## <a name="restore-your-mysql-database-using-command-line-or-mysql-workbench"></a>Restaurer votre base de données MySQL à l’aide d’une ligne de commande ou de MySQL Workbench
Une fois que vous avez créé la base de données cible hello, vous pouvez utiliser la commande de mysql hello ou MySQL banc d’essai toorestore hello données hello spécifique qui vient d’être créé de base de données à partir du fichier de vidage hello.
```bash
mysql -h [hostname] -u [uname] -p[pass] [db_to_restore] < [backupfile.sql]
```
Dans cet exemple, restaurer les données de hello en hello nouvellement créé de base de données sur la cible de hello Azure de base de données du serveur MySQL.
```bash
$ mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p testdb < testdb_backup.sql
```

## <a name="export-using-phpmyadmin"></a>Exporter avec PHPMyAdmin
tooexport, vous pouvez utiliser phpMyAdmin outil commun hello, qui peuvent déjà avoir installé localement dans votre environnement. tooexport votre base de données MySQL à l’aide de PHPMyAdmin :
- Ouvrez phpMyAdmin.
- Sélectionnez votre base de données. Cliquez sur le nom de base de données hello dans liste hello hello gauche. 
- Cliquez sur hello **exporter** lien. Une nouvelle page s’affiche de vidage de hello tooview de base de données.
- Bonjour zone d’exportation, cliquez sur hello **sélectionner tout** liez des tables de hello toochoose dans votre base de données. 
- Dans la zone des options SQL de hello, cliquez sur les options appropriées hello. 
- Cliquez sur hello **enregistrer en tant que fichier** option compression correspondante de hello option, puis cliquez sur hello **accédez** bouton. Une boîte de dialogue doit apparaître invite vous toosave hello fichier localement.

## <a name="import-using-phpmyadmin"></a>Importer avec PHPMyAdmin
L’importation de votre base de données est tooexporting similaire. Hello comme suit :
- Ouvrez phpMyAdmin. 
- Dans la page de hello phpMyAdmin le programme d’installation, cliquez sur **ajouter** tooadd votre Azure de base de données du serveur MySQL. Fournissez les détails de la connexion hello et les informations de connexion.
- Créer une base de données nommée de façon appropriée et sélectionnez-le dans l’écran hello gauche hello. toorewrite hello de base de données existante, cliquez sur le nom de base de données hello, activez toutes les cases à cocher hello en regard des noms de table hello et sélectionnez **supprimer** toodelete hello des tables existantes. 
- Cliquez sur hello **SQL** lien tooshow hello la page où vous pouvez taper dans les commandes SQL, ou télécharger votre fichier SQL. 
- Hello d’utilisation **Parcourir** fichier de base de données de bouton toofind hello. 
- Cliquez sur hello **accédez** bouton sauvegarde de hello tooexport, exécuter des commandes SQL hello et recréer votre base de données.

## <a name="next-steps"></a>Étapes suivantes
[Se connecter tooAzure d’applications de base de données pour MySQL](./howto-connection-string.md)
