---
title: "Démarrage rapide : création d’un serveur Azure Database pour MySQL - CLI Azure | Microsoft Docs"
description: "Ce guide de démarrage rapide explique comment utiliser l’interface CLI Azure pour créer un serveur Azure Database pour MySQL dans un groupe de ressources Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 11/29/2017
ms.custom: mvc
ms.openlocfilehash: aca5d33adda703f3cd50e940ee43bb0624e179a1
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/08/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a>Création d’un serveur Azure Database pour MySQL à l’aide de la CLI Azure
Ce guide de démarrage rapide explique comment utiliser l’interface CLI Azure pour créer un serveur Azure Database pour MySQL dans un groupe de ressources Azure en environ cinq minutes. L’interface de ligne de commande (CLI) Azure permet de créer et gérer des ressources Azure à partir de la ligne de commande ou dans les scripts.

Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article. Exécutez `az --version` pour trouver la version. Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Si vous possédez plusieurs abonnements, sélectionnez l’abonnement approprié dans lequel la ressource existe ou est facturée. Sélectionnez un ID d’abonnement spécifique sous votre compte à l’aide de la commande [az account set](/cli/azure/account#az_account_set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Créer un groupe de ressources
Créez un [groupe de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) avec la commande [az group create](/cli/azure/group#az_group_create). Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.

L’exemple suivant crée un groupe de ressources nommé `myresourcegroup` à l’emplacement `westus`.

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Créer un serveur de base de données Azure pour MySQL
Créez un serveur Azure Database pour MySQL avec la commande **[az mysql server create](/cli/azure/mysql/server#az_mysql_server_create)**. Un serveur peut gérer plusieurs bases de données. En règle générale, une base de données distincte est utilisée pour chaque projet ou pour chaque utilisateur.

L’exemple suivant crée un serveur Azure Database pour MySQL situé dans `westus` dans le groupe de ressources `myresourcegroup` avec le nom `myserver4demo`. Le serveur dispose d’une connexion administrateur avec le nom `myadmin` et le mot de passe `Password01!`. Le serveur est créé avec le niveau de performance **De base** et **50** unités de calcul partagées entre toutes les bases de données dans le serveur. Vous pouvez faire augmenter ou diminuer le calcul et le stockage selon les besoins de l’application.

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Configurer une règle de pare-feu
Créez une règle de pare-feu au niveau du serveur Azure Database pour MySQL avec la commande **[az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#az_mysql_server_firewall_rule_create)**. Une règle de pare-feu au niveau du serveur permet à une application externe, comme l’outil de ligne de commande **mysql.exe** ou MySQL Workbench de se connecter à votre serveur via le pare-feu du service Azure MySQL. 

L’exemple suivant illustre la création d’une règle de pare-feu pour une plage d’adresses prédéfinie qui, ici, est l’intégralité de la plage d’adresses IP possible.

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a>Configurer les paramètres SSL
Par défaut, des connexions SSL entre votre serveur et les applications clientes sont appliquées. Ce paramètre par défaut garantit la sécurité des données « en mouvement » en chiffrant le flux de données sur Internet. Pour faciliter ce démarrage rapide, désactivez les connexions SSL pour votre serveur. La désactivation des connexions SSL n’est pas recommandée pour les serveurs de production. Pour plus d’informations, consultez l’article [Configuration de la connectivité SSL dans votre application pour se connecter en toute sécurité à la base de données Azure pour MySQL](./howto-configure-ssl.md).

L’exemple suivant désactive l’application de SSL sur votre serveur MySQL.
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo --ssl-enforcement Disabled
 ```

## <a name="get-the-connection-information"></a>Obtenir les informations de connexion

Pour vous connecter à votre serveur, vous devez fournir des informations sur l’hôte et des informations d’identification pour l’accès.

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

Le résultat est au format JSON. Prenez note du **fullyQualifiedDomainName** et du **administratorLogin**.
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
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

## <a name="connect-to-the-server-using-the-mysqlexe-command-line-tool"></a>Connectez-vous au serveur avec l’outil de ligne de commande mysql.exe
Connectez-vous à votre serveur avec l’outil en ligne de commande **mysql.exe**. Vous pouvez télécharger MySQL [ici](https://dev.mysql.com/downloads/) et l’installer sur votre ordinateur. Une autre possibilité consiste à cliquer sur le bouton **Essayer** des exemples de code ou sur le bouton `>_` de la barre d’outils supérieure droite du Portail Azure et à lancer **Azure Cloud Shell**.

Tapez les commandes suivantes : 

1. Connectez-vous au serveur avec l’outil de ligne de commande **mysql** :
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. Afficher l’état du serveur :
```sql
 mysql> status
```
Si tout se déroule correctement, l’outil en ligne de commande doit générer le texte suivant :

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> Pour les autres commandes, consultez le [Manuel de référence de MySQL 5.7 - Chapitre 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).

## <a name="connect-to-the-server-using-the-mysql-workbench-gui-tool"></a>Connectez-vous au serveur à l’aide de l’outil MySQL Workbench GUI
1.  Lancez l’application MySQL Workbench sur votre ordinateur client. Vous pouvez télécharger et installer MySQL Workbench à partir [d’ici](https://dev.mysql.com/downloads/workbench/).

2.  Dans la boîte de dialogue **Configurer une nouvelle connexion**, entrez les informations suivantes dans l’onglet **Paramètres** :

   ![configurer une nouvelle connexion](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| **Paramètre** | **Valeur suggérée** | **Description** |
|---|---|---|
|   Nom de connexion | Ma connexion | Spécifiez une étiquette pour cette connexion (il peut s’agir de n’importe quoi) |
| Méthode de connexion | choisissez Standard (TCP/IP) | Utilisez le protocole TCP/IP pour vous connecter à la base de données Azure pour MySQL> |
| Nom d’hôte | myserver4demo.mysql.database.azure.com | Nom du serveur que vous avez noté précédemment |
| Port | 3306 | Le port par défaut pour MySQL est utilisé |
| Nom d’utilisateur | myadmin@myserver4demo | Connexion d’administrateur serveur que vous avez notée précédemment |
| Mot de passe | **** | Utilisez le mot de passe du compte Administrateur que vous avez configuré précédemment |

Cliquez sur **Tester la connexion** pour tester si tous les paramètres sont correctement configurés.
À présent, vous pouvez cliquer sur la connexion pour vous connecter au serveur.

## <a name="clean-up-resources"></a>Supprimer des ressources
Si vous n’avez pas besoin de ces ressources pour un autre guide de démarrage rapide ou didacticiel, vous pouvez les supprimer en exécutant la commande suivante : 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Conception d’une base de données MySQL avec Azure CLI](./tutorial-design-database-using-cli.md)
