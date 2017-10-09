---
title: "Se connecter tooAzure de base de données de MySQL de banc d’essai MySQL | Documents Microsoft"
description: "Ce démarrage rapide fournit hello étapes toouse banc d’essai MySQL tooconnect et interroger des données à partir de la base de données Azure pour MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a>Base de données Azure pour MySQL : utilisez MySQL Workbench tooconnect et interroger des données
Ce démarrage rapide montre comment tooconnect tooan base de données Azure pour l’utilisation de MySQL hello application MySQL Workbench. 

## <a name="prerequisites"></a>Composants requis
Ce démarrage rapide utilise des ressources hello créés dans un de ces guides comme point de départ :
- [Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a>Installer MySQL Workbench
Télécharger et installer le banc d’essai MySQL sur votre ordinateur à partir de [site Web de MySQL hello](https://dev.mysql.com/downloads/workbench/).

## <a name="get-connection-information"></a>Obtenir des informations de connexion
Obtenir hello connexion informations nécessaires tooconnect toohello base de données Azure pour MySQL. Vous devez hello des informations d’identification de nom et la connexion serveur complet.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).

2. Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources** et recherchez le serveur hello vous avez créé, tel que **myserver4demo**.

3. Cliquez sur le nom du serveur hello.

4. Serveur hello sélectionnez **propriétés** page. Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**.

 ![Nom du serveur de base de données Azure pour MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. Si vous oubliez vos informations de connexion du serveur, accédez à toohello **vue d’ensemble** page Nom de connexion d’administrateur du serveur de hello tooview et, si nécessaire, réinitialiser un mot de passe hello.

## <a name="connect-toohello-server-using-mysql-workbench"></a>Connexion serveur toohello à l’aide de banc d’essai MySQL 
tooconnect tooAzure MySQL server à l’aide de l’outil hello GUI banc d’essai MySQL :

1.  Lancez hello application banc d’essai MySQL sur votre ordinateur. 

2.  Dans **le programme d’installation nouvelle connexion** boîte de dialogue, entrez hello suivant les informations de hello **paramètres** onglet :

    ![configurer une nouvelle connexion](./media/connect-workbench/2-setup-new-connection.png)

    | **Paramètre** | **Valeur suggérée** | **Description du champ** |
    |---|---|---|
    |   Nom de connexion | Connexion démo | Spécifiez une étiquette pour cette connexion. |
    | Méthode de connexion | Standard (TCP/IP) | Standard (TCP/IP) est suffisant. |
    | Nom d’hôte | *nom du serveur* | Spécifiez la valeur de nom de serveur hello utilisé lorsque vous avez créé précédemment des hello de base de données Azure pour MySQL. Le serveur que nous utilisons dans notre exemple est myserver4demo.mysql.database.azure.com. Utilisez le nom de domaine complet hello (\*. mysql.database.azure.com) comme indiqué dans l’exemple de hello. Suivez les étapes de hello dans les informations de connexion du hello tooget de la section précédente hello si vous ne vous souvenez pas de nom de votre serveur.  |
    | Port | 3306 | Utilisez toujours le port 3306 lors de la connexion de base de données de tooAzure pour MySQL. |
    | Nom d’utilisateur |  *nom de connexion d’administrateur du serveur* | Tapez hello server connexion nom d’utilisateur administrateur fourni lorsque vous avez créé précédemment des hello de base de données Azure pour MySQL. Le nom d’utilisateur dans notre exemple est myadmin@myserver4demo. Suivez les étapes de hello dans les informations de connexion du hello tooget de la section précédente hello si vous ne vous souvenez pas de nom d’utilisateur hello. format de Hello est  *username@servername* .
    | Mot de passe | votre mot de passe | Cliquez sur **magasin dans le coffre...**  mot de passe de bouton toosave hello. |

3.   Cliquez sur **tester la connexion** tootest si tous les paramètres sont configurés correctement. 

4.   Cliquez sur **OK** connexion de hello toosave. 

5.   Dans la liste des hello **connexion MySQL**, cliquez sur le serveur de tooyour correspondant hello vignette et attendez hello toobe de connexion établie.

6.   Un nouvel onglet SQL s’ouvre avec un éditeur vide où vous pouvez saisir vos requêtes.

    > [!NOTE]
    > Par défaut, la sécurité de la connexion SSL est requise et appliquée sur votre serveur Azure Database pour MySQL. En général, aucune configuration supplémentaire avec les certificats SSL n’est requise pour le serveur de banc d’essai MySQL tooconnect tooyour. Pour plus d’informations sur SSL, consultez [tooAzure base de données de connexion de connectivité configurez SSL dans votre application de toosecurely pour MySQL](./howto-configure-ssl.md).  Si vous avez besoin de toodisable SSL, visitez hello portail Azure et cliquez sur hello connexion sécurité page toodisable hello SSL d’appliquer la connexion bascule.

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a>Créer une table, insérer des données, lire les données, mettre à jour des données et supprimer des données
1. Copiez et collez les exemple de code SQL hello dans un tooillustrate d’onglet SQL vide quelques exemples de données.

    Ce code crée une base de données vide nommée quickstartdb, puis crée un exemple de table nommée inventory. Il insère des lignes, puis lit les lignes hello. Il modifie des données de hello avec une instruction de mise à jour et lectures hello à nouveau les lignes. Pour finir, il supprime une ligne et lit les lignes hello à nouveau.
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    capture d’écran de Hello montre un exemple de code SQL de hello dans la sortie de SQL Workbench et hello après que qu’il a été exécuté.
    
    ![Onglet de SQL Workbench MySQL toorun exemple de code SQL](media/connect-workbench/3-workbench-sql-tab.png)

2. hello toorun exemple de Code SQL, cliquez sur hello éclaircissement icône d’éclair dans la barre d’outils hello Hello **fichier SQL** onglet.
3. Notez hello trois résultats à onglets Bonjour **grille de résultats** section milieu de hello de page de hello. 
4. Hello d’avis **sortie** liste à la fin de hello de page de hello. Hello l’état de chaque commande est affiché. 

À présent, vous avez connecté tooAzure de base de données pour MySQL à l’aide de banc d’essai MySQL et interrogez les données à l’aide du langage SQL de hello.

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Migration de votre base de données PostgreSQL par exportation et importation](./concepts-migrate-import-export.md)
