---
title: "aaaDesign votre première Azure de base de données pour la base de données MySQL - CLI d’Azure | Documents Microsoft"
description: "Ce didacticiel explique comment toocreate de base de données à l’aide d’Azure CLI 2.0 à partir de la ligne de commande hello et gérer la base de données Azure pour le serveur MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>Concevoir votre première base de données Azure pour MySQL

Base de données Azure pour MySQL est un service de base de données relationnelle Bonjour cloud de Microsoft en fonction du moteur de base de données MySQL Community Edition. Dans ce didacticiel, vous utilisez Azure CLI (interface de ligne de commande) et autres toolearn utilitaires comment à :

> [!div class="checklist"]
> * Créer une base de données Azure pour MySQL
> * Configurer le pare-feu du serveur hello
> * Utilisez [outil de ligne de commande mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate une base de données
> * Charger les exemples de données
> * Données de requête
> * Mettre à jour des données
> * Restaurer des données

Vous pouvez utiliser hello Azure Cloud Shell dans le navigateur de hello, ou [installer Azure CLI 2.0]( /cli/azure/install-azure-cli) sur votre propre ordinateur toorun hello les blocs de code dans ce didacticiel.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Si vous avez plusieurs abonnements, choisir l’abonnement approprié de hello dans lequel les ressources hello existent ou sont facturé pour. Sélectionnez un ID d’abonnement spécifique sous votre compte à l’aide de la commande [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Créer un groupe de ressources
Créez un [groupe de ressources Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) avec la commande [az group create](https://docs.microsoft.com/cli/azure/group#create). Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.

Hello exemple suivant crée un groupe de ressources nommé `mycliresource` Bonjour `westus` emplacement.

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Créer un serveur de base de données Azure pour MySQL
Créer une base de données Azure pour commande Création d’un serveur MySQL avec le serveur mysql de az hello. Un serveur peut gérer plusieurs bases de données. En règle générale, une base de données distincte est utilisée pour chaque projet ou pour chaque utilisateur.

Hello exemple suivant crée une base de données Azure pour le serveur MySQL situé dans `westus` dans le groupe de ressources hello `mycliresource` avec le nom `mycliserver`. serveur de Hello possède un journal de l’administrateur dans nommé `myadmin` et le mot de passe `Password01!`. Hello serveur est créé avec **base** niveau de performances et **50** unités partagées entre toutes les bases de données hello dans le serveur de hello de calcul. Vous pouvez faire évoluer calcul et stockage vers le haut ou vers le bas en fonction des besoins de l’application hello.

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Configurer une règle de pare-feu
Créer une base de données Azure pour commande de création de règle de pare-feu de niveau serveur MySQL avec hello az mysql server-règle de pare-feu. Une règle de pare-feu de niveau serveur permet à une application externe, tel que **mysql** outil de ligne de commande ou serveur de tooyour tooconnect de banc d’essai MySQL via le pare-feu de service Azure MySQL hello. 

Hello exemple suivant crée une règle de pare-feu pour une plage d’adresses prédéfinie. Cet exemple montre hello ensemble possible de plage d’adresses IP.

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a>Obtenir des informations de connexion hello

tooconnect tooyour server, vous devez tooprovide hôte accéder aux informations et informations d’identification.
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

résultat de Hello est au format JSON. Prenez note de hello **fullyQualifiedDomainName** et **administratorLogin**.
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-mysql"></a>Connexion serveur toohello à l’aide de mysql
Utilisez [outil de ligne de commande mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish un tooyour de connexion de base de données Azure pour le serveur MySQL. Dans cet exemple, commande hello est :
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a>Créer une base de données vide
Une fois que vous êtes connecté toohello server, créez une base de données vide.
```sql
mysql> CREATE DATABASE mysampledb;
```

À l’invite de hello, exécutez hello suivant de base de données de commande tooswitch hello connexion toothis nouvellement créé :
```sql
mysql> USE mysampledb;
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
Imaginez que vous avez supprimé cette table par erreur. Il s’agit de quelque chose que vous ne pouvez pas récupérer facilement. Base de données Azure pour MySQL vous permet de toogo tooany précédent point dans le temps dans hello dernière too35 jours et de restauration ce point dans le nouveau serveur de temps tooa. Les données supprimées, vous pouvez utiliser cette nouvelle toorecover de serveur. Hello suivant étapes restauration hello exemple server tooa point avant hello table a été ajoutée.

Pourquoi restauration vous devez hello informations suivantes :

- Point de restauration : sélectionnez un point dans le temps qui se produit avant que le serveur de hello a été modifié. Doit être supérieure ou égale à valeur de sauvegarde plus ancienne toohello source de base de données.
- Serveur cible : fournir un nouveau nom du serveur toorestore à
- Serveur source : fournir nom hello du serveur hello toorestore à partir de
- Emplacement : Vous ne pouvez pas sélectionner la région de hello, par défaut, il est identique au serveur de source de hello

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

serveur de hello toorestore et [tooa point-à-temps de restauration](./howto-restore-server-portal.md) avant hello table a été supprimée. Restauration d’un point différent de tooa de serveur dans le temps crée un nouveau serveur en double en tant que serveur d’origine de hello en tant que point hello dans le temps, vous spécifiez, autant qu’il soit dans la période de rétention hello pour votre [niveau de service](./concepts-service-tiers.md).

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :
> [!div class="checklist"]
> * Créer une base de données Azure pour MySQL
> * Configurer le pare-feu du serveur hello
> * Utilisez [outil de ligne de commande mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate une base de données
> * Charger les exemples de données
> * Données de requête
> * Mettre à jour des données
> * Restaurer des données

> [!div class="nextstepaction"]
> [Azure Database for MySQL - Azure CLI samples](./sample-scripts-azure-cli.md) (Base de données Azure pour MySQL - Exemples avec Azure CLI)
