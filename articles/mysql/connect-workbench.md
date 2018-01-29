---
title: "Se connecter à la base de données Azure pour MySQL depuis MySQL Workbench | Microsoft Docs"
description: "Ce guide de démarrage rapide indique les étapes à suivre pour utiliser MySQL Workbench pour vous connecter et interroger des données de la base de données Azure pour MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql
ms.custom: mvc
ms.topic: quickstart
ms.date: 09/22/2017
ms.openlocfilehash: 4214b80dc4c5db644d5a05f942907c86f292fe18
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2018
---
# <a name="azure-database-for-mysql-use-mysql-workbench-to-connect-and-query-data"></a>Base de données Azure pour MySQL : Utilisation de MySQL Workbench pour vous connecter et interroger des données
Ce guide de démarrage rapide vous explique comment vous connecter à une base de données Azure pour MySQL en utilisant une application MySQL Workbench. 

## <a name="prerequisites"></a>configuration requise
Ce guide de démarrage rapide s’appuie sur les ressources créées dans l’un de ces guides :
- [Créer un serveur de base de données Azure pour MySQL à l’aide du Portail Azure](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [Création d’un serveur de base de données Azure pour MySQL à l’aide d’Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a>Installer MySQL Workbench
Téléchargez et installez MySQL Workbench sur votre ordinateur depuis le [site web MySQL](https://dev.mysql.com/downloads/workbench/).

## <a name="get-connection-information"></a>Obtenir des informations de connexion
Obtenez les informations requises pour vous connecter à la base de données Azure pour MySQL. Vous devez disposer du nom de serveur complet et des informations d’identification.

1. Connectez-vous au [portail Azure](https://portal.azure.com/).

2. Dans le menu de gauche du portail Azure, cliquez sur **Toutes les ressources**, puis recherchez le serveur que vous venez de créer, par exemple **myserver4demo**.

3. Cliquez sur le nom du serveur.

4. Sélectionnez la page **Propriétés** du serveur, puis notez le **nom du serveur** et le **nom de connexion de l’administrateur du serveur**.

 ![Nom du serveur de base de données Azure pour MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. Si vous avez oublié vos informations de connexion au serveur, accédez à la page **Vue d’ensemble** pour afficher le nom de connexion de l’administrateur du serveur et, si nécessaire, réinitialiser le mot de passe.

## <a name="connect-to-the-server-by-using-mysql-workbench"></a>Se connecter au serveur à l’aide de MySQL Workbench 
Pour vous connecter au serveur Azure MySQL à l’aide de l’outil d’interface graphique MySQL Workbench :

1.  Lancez l’application MySQL Workbench sur votre ordinateur. 

2.  Dans la boîte de dialogue **Configurer une nouvelle connexion**, entrez les informations suivantes dans l’onglet **Paramètres** :

    ![configurer une nouvelle connexion](./media/connect-workbench/2-setup-new-connection.png)

    | **Paramètre** | **Valeur suggérée** | **Description du champ** |
    |---|---|---|
    |   Nom de connexion | Connexion démo | Spécifiez une étiquette pour cette connexion. |
    | Méthode de connexion | Standard (TCP/IP) | Standard (TCP/IP) est suffisant. |
    | Nom d’hôte | *nom du serveur* | Spécifiez la valeur de nom de serveur utilisée lorsque vous avez créé la base de données Azure pour MySQL. Le serveur que nous utilisons dans notre exemple est myserver4demo.mysql.database.azure.com. Utilisez le nom de domaine complet (\*.mysql.database.azure.com), comme indiqué dans l’exemple. Si vous ne vous souvenez pas du nom de votre serveur, suivez les instructions de la section précédente pour obtenir les informations de connexion.  |
    | Port | 3306 | Utilisez toujours le port 3306 lorsque vous vous connectez au service Base de données Azure pour MySQL. |
    | Nom d’utilisateur |  *nom de connexion d’administrateur du serveur* | Tapez le nom d’utilisateur de connexion d’administrateur du serveur fourni lorsque vous avez créé la base de données Azure pour MySQL. Le nom d’utilisateur dans notre exemple est myadmin@myserver4demo. Si vous ne vous souvenez pas du nom d’utilisateur, suivez les instructions de la section précédente pour obtenir les informations de connexion. Le format correct est *username@servername*.
    | Mot de passe | votre mot de passe | Cliquez sur le bouton **Stocker dans le coffre-fort…** pour enregistrer le mot de passe. |

3.   Cliquez sur **Tester la connexion** pour tester si tous les paramètres sont correctement configurés. 

4.   Cliquez sur **OK** pour enregistrer la connexion. 

5.   Dans la liste de **connexions MySQL**, cliquez sur le nom correspondant à votre serveur puis patientez jusqu’à ce que la connexion soit établie.

        Un nouvel onglet SQL s’ouvre avec un éditeur vide où vous pouvez saisir vos requêtes.
    
        > [!NOTE]
        > Par défaut, la sécurité de la connexion SSL est requise et appliquée sur votre serveur Azure Database pour MySQL. Habituellement, bien qu’aucune configuration supplémentaire avec certificats SSL ne soit requise pour MySQL Workbench afin de vous connecter à votre serveur, nous recommandons de lier la certification d’autorité de certification SSL à MySQL Workbench. Pour plus d’informations sur la façon de télécharger et de lier cette certification, consultez l’article [Configurer la connectivité SSL dans votre application pour vous connecter en toute sécurité à Azure Database pour MySQL](./howto-configure-ssl.md).  Si vous souhaitez désactiver le protocole SSL, visitez le portail Azure et cliquez sur la page Sécurité de la connexion pour désactiver le bouton bascule Appliquer une connexion SSL.

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a>Créer une table, insérer des données, lire les données, mettre à jour des données et supprimer des données
1. Copiez et collez l’exemple de code SQL dans un onglet SQL vide pour illustrer des exemples de données.

    Ce code crée une base de données vide nommée quickstartdb, puis crée un exemple de table nommée inventory. Il insère des lignes, puis lit les lignes. Il modifie les données avec une instruction de mise à jour et lit de nouveau les lignes. Enfin, il supprime une ligne puis lit de nouveau les lignes.
    
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

    La capture d’écran montre un exemple de code SQL dans SQL Workbench et la sortie obtenue après son exécution.
    
    ![Onglet Workbench MySQL de SQL pour exécuter l’exemple de code SQL](media/connect-workbench/3-workbench-sql-tab.png)

2. Pour exécuter l’exemple de Code SQL, cliquez sur l’icône d’éclair dans la barre d’outils de l’onglet**Fichier SQL**.
3. Vous observerez trois onglets de résultats dans la section **Grille de résultats** au milieu de la page. 
4. La liste **Sortie** apparaît en bas de la page. L’état de chaque commande s’affiche. 

Vous êtes à présent connecté à la base de données Azure pour MySQL à l’aide de MySQL Workbench et avez interrogé des données à l’aide du langage SQL.

## <a name="next-steps"></a>étapes suivantes
> [!div class="nextstepaction"]
> [Migration de votre base de données PostgreSQL par exportation et importation](./concepts-migrate-import-export.md)
