---
title: "aaaImport et d’exportation dans la base de données Azure pour MySQL | Documents Microsoft"
description: "Cet article explique les moyens tooimport et l’exportation bases de données courantes dans la base de données Azure pour MySQL, à l’aide des outils tels que MySQL banc d’essai."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: e2c036773d975df2eea2a59d166ea10567218a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-by-using-import-and-export"></a>Migration d’une base de données MySQL à l’aide de l’importation et de l’exportation
Cet article explique deux courantes approches tooimporting et tooan exportation des données de la base de données Azure pour MySQL server à l’aide de banc d’essai MySQL. 

## <a name="before-you-begin"></a>Avant de commencer
toostep via ce tooguide de procédure, vous devez :
- Un serveur de base de données Azure pour MySQL (voir [Créer un serveur de base de données Azure pour MySQL à l’aide du Portail Azure](quickstart-create-mysql-server-database-using-azure-portal.md))
- Banc d’essai MySQL [téléchargé](https://dev.mysql.com/downloads/workbench/), ou un autre MySQL outil tooimport et exportation.

## <a name="use-common-tools"></a>Utiliser des outils courants
Utiliser les outils courants tels que MySQL banc d’essai, adresse : ou Navicat tooremotely vous connecter et importer ou exporter des données dans la base de données Azure pour MySQL. 

Utilisez ces outils sur votre ordinateur client avec un tooAzure de tooconnect de connexion Internet de base de données de MySQL. Utilisez une connexion chiffrée SSL pour appliquer les meilleures pratiques de sécurité, comme décrit dans la page [Configurer la connectivité SSL dans la base de données Azure pour MySQL](concepts-ssl-connection-security.md).

Vous ne devez toomove l’importation et exporter l’emplacement des fichiers de cloud spéciaux tooany lors de la migration tooAzure de base de données de MySQL. 

## <a name="create-a-database-on-hello-azure-database-for-mysql-server"></a>Créer une base de données sur hello Azure de base de données du serveur MySQL
Créer une base de données vide sur hello Azure de base de données du serveur MySQL où vous souhaitez toomigrate hello données. Utilisez un outil tel que MySQL banc d’essai, adresse : Navicat toocreate hello base de données ou. base de données Hello peut avoir hello même nom que la base de données hello qui contient les données de hello exportée, ou vous pouvez créer une base de données avec un nom différent.

tooget connecté, recherchez les informations de connexion hello sur hello **propriétés** volet dans la base de données Azure pour MySQL.

![Rechercher des informations de connexion hello Bonjour portail Azure](./media/concepts-migrate-import-export/1_server-properties-name-login.png)

Ajoutez tooMySQL informations de connexion hello banc d’essai.

![Chaîne de connexion MySQL Workbench](./media/concepts-migrate-import-export/2_setup-new-connection.png)

## <a name="determine-when-toouse-import-and-export-techniques-instead-of-a-dump-and-restore"></a>Déterminer quand toouse importer et exporter des techniques au lieu d’un vidage et de restauration
Utilisez MySQL outils tooimport et exporter des bases de données dans la base de données MySQL Azure Bonjour les scénarios suivants. Dans d’autres scénarios, vous pouvez bénéficier de l’utilisation de hello [de vidage et de restauration](concepts-migrate-dump-restore.md) approche à la place. 

- Lorsque vous avez besoin tooselectively choisissez plusieurs tables tooimport à partir d’une base de données MySQL existante dans la base de données MySQL de Azure, ses meilleures toouse hello importation et exportation technique.  En procédant ainsi, vous pouvez omettre les tables inutiles de hello migration toosave temps et des ressources. Par exemple, utiliser hello `--include-tables` ou `--exclude-tables` basculer [mysqlpump](https://dev.mysql.com/doc/refman/5.7/en/mysqlpump.html#option_mysqlpump_include-tables) et hello `--tables` basculer [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html#option_mysqldump_tables).
- Lorsque vous déplacez des objets de base de données hello autres que les tables, créez explicitement celles. Inclure les contraintes (clé primaire, clé étrangère, index), vues, fonctions, procédures, déclencheurs et toute autre base de données des objets que vous souhaitez toomigrate.
- Lorsque vous effectuez la migration de données à partir de sources de données externes autres qu’une base de données MySQL, créez des fichiers plats et importez-les à l’aide de [mysqlimport](https://dev.mysql.com/doc/refman/5.7/en/mysqlimport.html).

Assurez-vous que toutes les tables de base de données hello utiliseront moteur de stockage InnoDB hello lorsque vous vous chargez des données dans la base de données Azure pour MySQL. Une base de données Azure pour MySQL prend en charge uniquement hello InnoDB moteur de stockage, il ne prend pas en charge les moteurs de stockage de remplacement. Si vos tables nécessitent des moteurs de stockage secondaire, être tooconvert que leur format du moteur toouse hello InnoDB avant hello tooAzure de migration de base de données de MySQL. 

Par exemple, si vous avez une WordPress ou une application web qui utilise le moteur de MyISAM hello, tout d’abord convertir les tables hello en migrant les données hello InnoDB tables. Puis restaurer tooAzure de base de données de MySQL. Clause de hello utilisation `ENGINE=INNODB` tooset hello moteur pour la création d’une table, puis transférer les données de hello dans table compatible de hello avant la migration de hello. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```

## <a name="performance-recommendations-for-import-and-export"></a>Recommandations en matière de performances pour l’importation et l’exportation
-   Créez des index cluster et des clés primaires avant le chargement des données. Chargez les données dans l’ordre des clés primaires. 
-   Reportez la création des index secondaires après le chargement des données. Créez tous les index secondaires après le chargement. 
-   Désactivez les contraintes de clé étrangère avant le chargement. La désactivation des vérifications de clé étrangère offre d’importants gains de performances. Activer les contraintes de hello et vérifier les données de hello après l’intégrité référentielle hello charge tooensure.
-   Chargez les données en parallèle. Éviter de trop de parallélisme serait vous entraîner toohit une limite de ressource et de surveillance des ressources à l’aide de mesures hello disponibles dans hello portail Azure. 
-   Utilisez des tables partitionnées le cas échéant.

## <a name="import-and-export-by-using-mysql-workbench"></a>Importer et exporter des données à l’aide de MySQL Workbench
Il existe deux façons tooexport et l’importation des données dans le banc d’essai MySQL. Chacune répond à un objectif différent. 

### <a name="table-data-export-and-import-wizards-from-hello-object-browsers-context-menu"></a>Données de la table exporter et importer des Assistants à partir du menu contextuel de l’Explorateur d’objets hello
![Assistants de banc d’essai MySQL dans le menu contextuel de l’Explorateur d’objets hello](./media/concepts-migrate-import-export/p1.png)

Assistants Hello pour les données de table prend en charge d’importation et d’exportation à l’aide de fichiers CSV et JSON. Ils offrent plusieurs options de configuration, notamment les séparateurs, la sélection de colonne et la sélection du codage. Vous pouvez exécuter chaque Assistant sur des serveurs MySQL locaux ou connectés à distance. action d’importation Hello inclut le mappage de type table et colonne. 

Vous pouvez accéder ces Assistants à partir du menu contextuel de l’Explorateur d’objets hello en double-cliquant sur une table. Choisissez ensuite **Table Data Export Wizard** (Assistant Exportation de données de table) ou **Table Data Import Wizard** (Assistant Importation de données de table). 

#### <a name="table-data-export-wizard"></a>Assistant Exportation de données de table
Hello exemple exporte fichier CSV de hello table tooa : 
1. Cliquez sur table hello de hello toobe de base de données exportée. 
2. Sélectionnez **Assistant Exportation de données de table**. Sélectionnez toobe colonnes hello exportée, décalage de lignes (le cas échéant) et count (le cas échéant). 
3. Sur hello **sélectionner des données pour l’exportation** , cliquez sur **suivant**. Sélectionnez le chemin d’accès du fichier hello, CSV ou JSON type de fichier. Sélectionnez également le séparateur de ligne hello, méthode de placer des chaînes et le séparateur de champs. 
4. Sur hello **emplacement de fichier de sortie sélectionnez** , cliquez sur **suivant**. 
5. Sur hello **exporter des données** , cliquez sur **suivant**.

#### <a name="table-data-import-wizard"></a>Assistant Importation de données de table
Hello exemple suivant importe hello table à partir d’un fichier CSV :
1. Cliquez sur table hello de hello toobe de base de données importée. 
2. Parcourir tooand sélectionnez hello toobe de fichier CSV importé, puis cliquez sur **suivant**. 
3. Sélectionnez la table de destination hello (nouveau ou existant) et activez ou désactivez hello **troncature de table avant l’importation** case à cocher. Cliquez sur **Suivant**.
4. Sélectionnez le codage et hello toobe colonnes importée, puis cliquez sur **suivant**. 
5. Sur hello **importer des données** , cliquez sur **suivant**. Assistant de Hello importe les données de salutation en conséquence.

### <a name="sql-data-export-and-import-wizards-from-hello-navigator-pane"></a>Les données SQL exporter et importer des Assistants à partir du volet de navigation hello
Utiliser un Assistant tooexport ou importer SQL généré à partir de banc d’essai MySQL ou généré à partir de la commande de mysqldump hello. Accéder à ces Assistants de hello **Navigator** volet ou en sélectionnant **Server** à partir du menu principal de hello. Puis, sélectionnez **Data Export** (Exportation des données) ou **Data Import** (Importation de données). 

#### <a name="data-export"></a>Exportation de données
![Exportation des données de banc d’essai MySQL à l’aide du volet de navigation hello](./media/concepts-migrate-import-export/p2.png)

Vous pouvez utiliser hello **d’exportation des données** onglet tooexport vos données de MySQL. 
1. Sélectionnez chaque schéma que vous souhaitez tooexport, si vous le souhaitez choisissez des objets de schéma spécifique et les tables à partir de chaque schéma et générez l’exportation de hello. Options de configuration incluent le dossier d’exportation tooa projet ou fichier SQL autonome, dump des événements et les routines stockées ou ignorer les données de la table. 
 
   Vous pouvez également utiliser **exporter un jeu de résultats** tooexport un résultat spécifique défini dans le format tooanother éditeur hello SQL, tels que CSV, JSON, HTML et XML. 
3. Sélectionnez tooexport d’objets hello de base de données, puis configurez hello des options liées.
4. Cliquez sur **Actualiser** objets en cours de tooload hello.
5. Si vous le souhaitez, ouvrez hello **Options avancées** onglet toorefine l’opération d’exportation hello. Par exemple, ajoutez des verrous de table, utilisez des instructions replace à la place des instructions insert et placez les identificateurs entre accents graves.
6. Cliquez sur **démarrer exporter** processus d’exportation toobegin hello.


#### <a name="data-import"></a>Importation de données
![Importation de données MySQL Workbench à l’aide du navigateur de gestion](./media/concepts-migrate-import-export/p3.png)

Vous pouvez utiliser hello **importation des données** onglet tooimport ou restaurer des données exportées à partir de l’opération d’exportation de données de hello ou à partir de la commande de mysqldump hello. 
1. Choisissez le dossier du projet hello ou fichiers autonome de SQL, choisissez tooimport de schéma hello dans ou choisissez **nouveau** toodefine un nouveau schéma. 
2. Cliquez sur **démarrer importer** processus d’importation toobegin hello.

## <a name="next-steps"></a>Étapes suivantes
Pour découvrir une autre approche de migration, consultez [Migrer une base de données MySQL à l’aide des images mémoire et de la restauration dans la base de données Azure pour MySQL](concepts-migrate-dump-restore.md). 
