---
title: "Démarrage rapide : création d’un serveur Azure Database pour MySQL - CLI Azure | Microsoft Docs"
description: "Ce démarrage rapide explique comment toouse hello CLI d’Azure toocreate une base de données Azure du serveur MySQL dans un groupe de ressources Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a>Création d’un serveur Azure Database pour MySQL à l’aide de la CLI Azure
Ce démarrage rapide explique comment toouse hello CLI d’Azure toocreate une base de données Azure du serveur MySQL dans un groupe de ressources Azure dans environ cinq minutes. Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts.

Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Si vous avez plusieurs abonnements, choisir l’abonnement approprié de hello dans lequel les ressources hello existent ou sont facturé pour. Sélectionnez un ID d’abonnement spécifique sous votre compte à l’aide de la commande [az account set](/cli/azure/account#set).
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a>Créer un groupe de ressources
Créer un [groupe de ressources Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) à l’aide de hello [création de groupe de az](https://docs.microsoft.com/cli/azure/group#create) commande. Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.

Hello exemple suivant crée un groupe de ressources nommé `myresourcegroup` Bonjour `westus` emplacement.

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a>Créer un serveur de base de données Azure pour MySQL
Créer une base de données Azure pour le serveur MySQL avec hello **az mysql server créer** commande. Un serveur peut gérer plusieurs bases de données. En règle générale, une base de données distincte est utilisée pour chaque projet ou pour chaque utilisateur.

Hello exemple suivant crée une base de données Azure pour le serveur MySQL situé dans `westus` dans le groupe de ressources hello `myresourcegroup` avec le nom `myserver4demo`. serveur de Hello possède un journal de l’administrateur dans nommé `myadmin` et le mot de passe `Password01!`. Hello serveur est créé avec **base** niveau de performances et **50** unités partagées entre toutes les bases de données hello dans le serveur de hello de calcul. Vous pouvez faire évoluer calcul et stockage vers le haut ou vers le bas en fonction des besoins de l’application hello.

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a>Configurer une règle de pare-feu
Créer une base de données Azure pour la règle de pare-feu de niveau serveur MySQL à l’aide de hello **az mysql server-règle de pare-feu créer** commande. Une règle de pare-feu de niveau serveur permet à une application externe, par exemple hello **mysql.exe** outil de ligne de commande ou serveur de tooyour tooconnect de banc d’essai MySQL via le pare-feu de service Azure MySQL hello. 

Hello exemple suivant crée une règle de pare-feu pour une plage d’adresses prédéfinies qui, dans cet exemple, est hello ensemble possible de plage d’adresses IP.

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a>Configurer les paramètres SSL
Par défaut, des connexions SSL entre votre serveur et les applications clientes sont appliquées.  Cela garantit la sécurité de « en mouvement » données en chiffrant les flux de données hello sur hello internet.  toomake cette prise en main plus facilement, nous désactivons les connexions SSL pour votre serveur.  Cette opération n’est pas recommandée pour les serveurs de production.  Pour plus d’informations, consultez [tooAzure base de données de connexion de connectivité configurez SSL dans votre application de toosecurely pour MySQL](./howto-configure-ssl.md).

Hello exemple suivant désactive la mise en œuvre de SSL sur votre serveur MySQL.
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a>Obtenir des informations de connexion hello

tooconnect tooyour server, vous devez tooprovide hôte accéder aux informations et informations d’identification.

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

résultat de Hello est au format JSON. Prenez note de hello **fullyQualifiedDomainName** et **administratorLogin**.
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a>Connexion serveur toohello à l’aide d’outil de ligne de commande hello mysql.exe
Connexion serveur tooyour à l’aide de hello **mysql.exe** outil de ligne de commande. Vous pouvez télécharger MySQL [ici](https://dev.mysql.com/downloads/) et l’installer sur votre ordinateur. Au lieu de cela, vous pouvez également cliquer hello **essayer** bouton sur les exemples de code ou hello `>_` bouton hello supérieure droite barre d’outils hello portail Azure et lancement hello **Azure Cloud Shell**.

Tapez les commandes suivants hello : 

1. Connectez-vous à l’aide du serveur toohello **mysql** outil de ligne de commande :
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. Afficher l’état du serveur :
```sql
 mysql> status
```
Si tout se passe bien, outil de ligne de commande hello doit générer hello suivant du texte :

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

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
> Pour les autres commandes, consultez le [Manuel de référence de MySQL 5.7 - Chapitre 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Connexion serveur toohello à l’aide d’outil d’interface utilisateur graphique de banc d’essai MySQL hello
1.  Lancez hello application banc d’essai MySQL sur votre ordinateur client. Vous pouvez télécharger et installer MySQL Workbench à partir [d’ici](https://dev.mysql.com/downloads/workbench/).

2.  Bonjour **le programme d’installation nouvelle connexion** boîte de dialogue, entrez hello suivant des informations sur la zone **paramètres** onglet :

   ![configurer une nouvelle connexion](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| **Paramètre** | **Valeur suggérée** | **Description** |
|---|---|---|
|   Nom de connexion | Ma connexion | Spécifiez une étiquette pour cette connexion (il peut s’agir de n’importe quoi) |
| Méthode de connexion | choisissez Standard (TCP/IP) | Utilisez tooAzure tooconnect de protocole TCP/IP de base de données de MySQL > |
| Nom d’hôte | myserver4demo.mysql.database.azure.com | Nom du serveur que vous avez noté précédemment |
| Port | 3306 | port par défaut Hello MySQL est utilisé. |
| Nom d’utilisateur | myadmin@myserver4demo | connexion d’administration de serveur Hello noté précédemment. |
| Mot de passe | **** | Utilisez hello compte mot de passe administrateur que vous avez configurée précédemment. |

Cliquez sur **tester la connexion** tootest si tous les paramètres sont configurés correctement.
Maintenant, vous pouvez cliquer sur les connexions hello toosuccessfully connecter toohello server.

## <a name="clean-up-resources"></a>Supprimer des ressources
Si vous n’avez pas besoin ces ressources pour un autre/didacticiel de démarrage rapide, vous pouvez les supprimer en procédant comme hello de commande suivante : 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Conception d’une base de données MySQL avec Azure CLI](./tutorial-design-database-using-cli.md)
