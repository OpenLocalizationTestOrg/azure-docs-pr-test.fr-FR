---
title: "aaaDesign votre première Azure de base de données pour la base de données MySQL - portail Azure | Documents Microsoft"
description: "Ce didacticiel explique comment toocreate et gérer la base de données Azure pour MySQL server et la base de données à l’aide du portail Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>Concevoir votre première base de données Azure pour MySQL
Base de données Azure pour MySQL est un service géré qui vous permet de toorun, gérer et mettre à l’échelle des bases de données MySQL hautement disponibles dans le cloud de hello. À l’aide de hello portail Azure, vous pouvez facilement gérer votre serveur et concevoir une base de données.

Dans ce didacticiel, vous utilisez comment hello toolearn portail Azure pour :

> [!div class="checklist"]
> * Créer une base de données Azure pour MySQL
> * Configurer le pare-feu du serveur hello
> * Utiliser l’outil de ligne de commande de mysql toocreate une base de données
> * Charger les exemples de données
> * Données de requête
> * Mettre à jour des données
> * Restaurer des données

## <a name="sign-in-toohello-azure-portal"></a>Se connecter toohello portail Azure
Ouvrez votre navigateur web favoris et visitez hello [portail Microsoft Azure](https://portal.azure.com/). Entrez vos informations d’identification toosign dans toohello portal. affichage par défaut de Hello est votre tableau de bord de service.

## <a name="create-an-azure-database-for-mysql-server"></a>Créer un serveur de base de données Azure pour MySQL
Un serveur de base de données Azure pour MySQL est créé avec un ensemble défini de [ressources de calcul et de stockage](./concepts-compute-unit-and-storage.md). serveur de Hello est créé dans un [groupe de ressources Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).

1. Accédez trop**bases de données** > **base de données Azure pour MySQL**. Si vous ne trouvez pas MySQL Server sous **bases de données** catégorie, cliquez sur **afficher tous les** tooshow tous les services de base de données. Vous pouvez également taper **base de données Azure pour MySQL** dans tooquickly de zone de recherche hello trouver le service de hello.
![2-1 naviguer tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)

2. Cliquez sur la vignette **Base de données Azure pour MySQL**, puis sur **Créer**.

Dans notre exemple, renseignez hello Azure de base de données MySQL formulaire avec hello informations suivantes :

| **Paramètre** | **Valeur suggérée** | **Description du champ** |
|---|---|---|
| *Nom du serveur* | myserver4demo  | Nom du serveur a toobe global unique. |
| *Abonnement* | mysubscription | Sélectionnez votre abonnement dans hello de liste déroulante. |
| *Groupe de ressources* | myResourceGroup | Créez un groupe de ressources ou utilisez un groupe existant. |
| *Connexion d’administrateur du serveur* | myadmin | Configurez le nom du compte Administrateur. |
| *Mot de passe* |  | Définissez un mot de passe complexe pour le compte d’administrateur. |
| *Confirmer le mot de passe* |  | Confirmer le mot de passe administrateur hello. |
| *Emplacement* |  | Sélectionnez une région disponible. |
| *Version* | 5.7 | Choisissez la version la plus récente hello. |
| *Configurer les performances* | De base, 50 unités de calcul, 50 Go  | Choisissez le **niveau de performance**, les **unités de calcul** et le **stockage**, puis cliquez sur **OK**. |
| *Code confidentiel tooDashboard* | Vérification | Recommandé toocheck cette case, afin que vous pouvez rechercher facilement ultérieurement sur le serveur de hello |
Cliquez sur **Créer**. Dans une ou deux minutes, une nouvelle base de données Azure pour MySQL server est en cours d’exécution dans le cloud de hello. Vous pouvez cliquer sur **Notifications** bouton sur le processus de déploiement hello barre d’outils toomonitor hello.

## <a name="configure-firewall"></a>Configurer le pare-feu
Les bases de données Azure pour MySQL sont protégées par un pare-feu. Par défaut, toutes les connexions toohello serveur hello bases de données et à l’intérieur du serveur de hello sont rejetées. Avant de tooAzure de base de données de connexion MySQL pour hello première fois, configurer l’adresse IP du réseau public de hello pare-feu tooadd hello l’ordinateur client (ou plage d’adresses IP).

1. Cliquez sur le serveur qui vient d’être créé, puis sur **Sécurité de la connexion**.
   ![3-1 Sécurité de la connexion](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)
2. Vous pouvez choisir **Ajouter mon adresse IP** ou configurer les règles de pare-feu ici. N’oubliez pas de tooclick **enregistrer** après avoir créé des règles hello.
Vous pouvez désormais connecter serveur toohello à l’aide d’outil de ligne de commande mysql ou d’outil d’interface utilisateur graphique de banc d’essai de MySQL.

> [!TIP]
> Le serveur de base de données Azure pour MySQL communique sur le port 3306. Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 3306 ne peut pas être autorisé par le pare-feu de votre réseau. Dans ce cas, tooAzure MySQL server ne peut pas se connecter à moins que votre service informatique ouvre le port 3306.

## <a name="get-connection-information"></a>Obtenir des informations de connexion
Hello Get complet **nom du serveur** et **nom de connexion de serveur admin** pour votre base de données Azure pour le serveur MySQL de hello portail Azure. Vous utilisez hello complet nom tooconnect tooyour serveur à l’aide d’outil de ligne de commande mysql. 

1. Dans [portail Azure](https://portal.azure.com/), cliquez sur **toutes les ressources** de menu à gauche hello, nom de type hello et recherchez votre base de données Azure pour le serveur MySQL. Sélectionner les détails de hello hello serveur nom tooview.

2. Sous paramètres de hello titre, cliquez sur **propriétés**. Notez les valeurs de **NOM DU SERVEUR** et de **NOM DE CONNEXION D’ADMINISTRATEUR DU SERVEUR**. Vous pouvez cliquer hello copier bouton suivant tooeach champ toocopy toohello le Presse-papiers.
   ![4-2 Propriétés de serveur](./media/tutorial-design-database-using-portal/4_2-server-properties.png)

Dans cet exemple, le nom du serveur hello est *myserver4demo.mysql.database.azure.com*, et de la connexion administrateur de serveur hello est  *myadmin@myserver4demo* .

## <a name="connect-toohello-server-using-mysql"></a>Connexion serveur toohello à l’aide de mysql
Utilisez [outil de ligne de commande mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish un tooyour de connexion de base de données Azure pour le serveur MySQL. Vous pouvez exécuter outil de ligne de commande mysql hello de hello Azure Cloud Shell dans le navigateur de hello ou à partir de votre propre ordinateur à l’aide des outils de mysql sont installés localement. toolaunch hello Azure Cloud interpréteur de commandes, cliquez sur hello `Try It` bouton sur un bloc de code dans cet article, ou visitez hello portail Azure, puis cliquez sur hello `>_` icône dans la barre d’outils droite supérieure hello. 

Tapez hello commande tooconnect :
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a>Créer une base de données vide
Une fois que vous êtes connecté toohello server, créez un toowork de base de données vide avec.
```sql
CREATE DATABASE mysampledb;
```

À l’invite de hello, exécutez hello suivant de base de données de commande tooswitch connexion toothis nouvellement créé :
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Créer des tables dans la base de données hello
Maintenant que vous savez comment tooconnect toohello base de données Azure pour la base de données MySQL, nous pouvons sur la façon toocomplete certaines tâches de base.

Tout d’abord, nous pouvons créer une table et y charger des données. Nous allons créer une table qui stocke des données d’inventaire.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Charger des données dans les tables de hello
Maintenant que nous disposons d’une table, nous pouvons y insérer des données. Fenêtre d’invite de commandes ouverte hello, puis exécutez hello suivant requête tooinsert certaines lignes de données.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Vous avez maintenant deux lignes d’exemples de données dans la table hello que vous avez créé précédemment.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Interroger et mettre à jour les données hello dans les tables de hello
Exécutez hello suivant tooretrieve les informations de requête à partir de la table de base de données hello.
```sql
SELECT * FROM inventory;
```

Vous pouvez également mettre à jour les données hello dans les tables de hello.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

ligne de Hello est mise à jour en conséquence lorsque vous récupérez des données.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Restaurer un état antérieur de tooa de base de données dans le temps
Imaginez que vous avez accidentellement supprimé une table de base de données importants et ne peut pas récupérer les données de salutation facilement. Base de données Azure pour MySQL vous permet de toorestore hello server tooa point dans le temps, créez une copie de bases de données hello dans du nouveau serveur. Les données supprimées, vous pouvez utiliser cette nouvelle toorecover de serveur. Hello suivant étapes restauration hello exemple server tooa point avant hello table a été ajoutée.

1. Bonjour portail Azure, recherchez votre base de données Azure pour MySQL. Sur hello **vue d’ensemble** , cliquez sur **restaurer** sur la barre d’outils hello. page de restauration Hello s’ouvre.

   ![10-1 Restaurer une base de données](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. Remplir hello **restaurer** formulaire avec les informations de hello requis.
   
   ![10-2 Formulaire de restauration](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - **Point de restauration**: sélectionnez un point dans le temps que vous souhaitez toorestore, pendant les laps de temps hello répertoriés. Assurez-vous que tooconvert tooUTC de votre fuseau horaire local.
   - **Restaurer le serveur de toonew**: fournir un nouveau nom du serveur toorestore à.
   - **Emplacement**: région de hello est identique au serveur de source de hello et ne peut pas être modifiée.
   - **Niveau de tarification**: hello niveau tarifaire est hello identique hello serveur source et ne peut pas être modifié.
   
3. Cliquez sur **OK** toorestore hello server trop[restaurer tooa point dans le temps](./howto-restore-server-portal.md) avant hello table a été supprimée. Restauration d’un serveur crée une copie du serveur hello, as of point hello dans le temps que vous spécifiez. 

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous utilisez comment hello toolearned portail Azure pour :

> [!div class="checklist"]
> * Créer une base de données Azure pour MySQL
> * Configurer le pare-feu du serveur hello
> * Utiliser l’outil de ligne de commande de mysql toocreate une base de données
> * Charger les exemples de données
> * Données de requête
> * Mettre à jour des données
> * Restaurer des données

> [!div class="nextstepaction"]
> [Comment tooconnect applications tooAzure de base de données MySQL](./howto-connection-string.md)
