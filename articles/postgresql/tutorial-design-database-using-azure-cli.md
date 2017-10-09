---
title: "Concevoir votre première base de données Azure pour PostgreSQL avec Azure CLI | Microsoft Docs"
description: "Ce didacticiel montre comment tooDesign votre première Azure de base de données PostgreSQL à l’aide de CLI d’Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a>Concevoir votre première base de données Azure pour PostgreSQL avec Azure CLI 
Dans ce didacticiel, vous utilisez Azure CLI (interface de ligne de commande) et autres toolearn utilitaires comment à :
> [!div class="checklist"]
> * Créer une base de données Azure pour PostgreSQL
> * Configurer le pare-feu du serveur hello
> * Utilisez [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilitaire toocreate une base de données
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
Créer un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) à l’aide de hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe. Hello exemple suivant crée un groupe de ressources nommé `myresourcegroup` Bonjour `westus` emplacement.
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a>Créer un serveur Azure Database pour PostgreSQL
Créer un [Azure de base de données PostgreSQL serveur](overview.md) à l’aide de hello [az postgres serveur créer](/cli/azure/postgres/server#create) commande. Un serveur contient un groupe de bases de données gérées en tant que groupe. 

Hello exemple suivant crée un serveur appelé `mypgserver-20170401` dans votre groupe de ressources `myresourcegroup` avec ouverture de session de serveur admin `mylogin`. Nom d’un serveur mappe le nom de tooDNS et est donc requis toobe globalement unique dans Azure. Hello de substitution `<server_admin_password>` avec votre propre valeur.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> connexion administrateur de serveur Hello et un mot de passe que vous spécifiez ici sont requis toolog dans toohello server et ses bases de données plus loin dans ce guide de démarrage rapide. Retenez ou enregistrez ces informations pour une utilisation ultérieure.

Par défaut, la création de la base de données **postgres** intervient sous votre serveur. Hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) base de données est une base de données par défaut destinée à une utilisation par les utilisateurs, les utilitaires et les applications tierces. 


## <a name="configure-a-server-level-firewall-rule"></a>Configurer une règle de pare-feu au niveau du serveur

Créer une règle de pare-feu de niveau serveur Azure PostgreSQL avec hello [az postgres server-règle de pare-feu créer](/cli/azure/postgres/server/firewall-rule#create) commande. Une règle de pare-feu de niveau serveur permet à une application externe, tel que [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) ou [PgAdmin](https://www.pgadmin.org/) server tooyour de tooconnect via le pare-feu de service Azure PostgreSQL hello. 

Vous pouvez définir une règle de pare-feu qui couvre une tooconnect IP plage toobe en mesure de votre réseau. Hello exemple suivant utilise [az postgres server-règle de pare-feu créer](/cli/azure/postgres/server/firewall-rule#create) toocreate une règle de pare-feu `AllowAllIps` plage d’adresses pour une adresse IP. tooopen toutes les adresses IP, utilisez 0.0.0.0 comme hello à partir d’adresse IP et 255.255.255.255 comme adresse de fin de hello.
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> Le serveur Azure PostgreSQL communique sur le port 5432. Lorsque vous vous connectez à partir d’un réseau d’entreprise, le trafic sortant sur le port 5432 peut être bloqué par le pare-feu de votre réseau. Avoir votre service informatique d’ouvrir le serveur de base de données SQL Azure port 5432 tooconnect tooyour.
>

## <a name="get-hello-connection-information"></a>Obtenir des informations de connexion hello

tooconnect tooyour server, vous devez tooprovide hôte accéder aux informations et informations d’identification.
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

résultat de Hello est au format JSON. Prenez note de hello **administratorLogin** et **fullyQualifiedDomainName**.
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a>Se connecter tooAzure de base de données pour la base de données PostgreSQL à l’aide de psql
Si votre ordinateur client a PostgreSQL installé, vous pouvez utiliser une instance locale de [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), ou le serveur Azure PostgreSQL tooan hello Azure Cloud Console tooconnect. Nous allons maintenant utiliser hello psql utilitaire de ligne de commande tooconnect toohello Azure de base de données PostgreSQL serveur.

1. Exécutez hello suivant psql commande tooconnect tooan Azure de base de données PostgreSQL serveur
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Par exemple, hello commande suivante connecte à base de données de la valeur par défaut toohello appelée **postgres** sur votre serveur PostgreSQL **mypgserver-20170401.postgres.database.azure.com** à l’aide des informations d’identification d’accès. Entrez hello `<server_admin_password>` vous avez choisi à l’invite de mot de passe.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  Une fois que vous êtes connecté toohello server, créez une base de données vide à l’invite de hello.
```sql
CREATE DATABASE mypgsqldb;
```

3.  À l’invite de hello, exécutez hello suivant de base de données de commande tooswitch connexion toohello nouvellement créé **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a>Créer des tables dans la base de données hello
Maintenant que vous savez comment tooconnect toohello base de données Azure pour PostgreSQL, nous pouvons sur la façon toocomplete certaines tâches de base.

Tout d’abord, nous pouvons créer une table et y charger des données. Nous allons créer une table qui assure le suivi des informations d’inventaire.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

Vous pouvez voir hello nouvellement créé table dans la liste hello des tables maintenant en tapant :
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a>Charger des données dans les tables de hello
Maintenant que nous disposons d’une table, nous pouvons y insérer des données. Au niveau de la fenêtre d’invite de commandes ouverte hello, exécutez hello suivant requête tooinsert certaines lignes de données
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

Vous pouvez également mettre à jour les données hello dans les tables de hello
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

ligne de Hello est mise à jour en conséquence lorsque vous récupérez des données.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Restaurer un état antérieur de tooa de base de données dans le temps
Imaginez que vous avez supprimé une table par inadvertance. Il s’agit de quelque chose que vous ne pouvez pas récupérer facilement. Base de données Azure pour PostgreSQL vous permet de toogo tooany arrière dans le temps (en hello dernière too7 jours (Basic) et de 35 jours (Standard)) et de restauration ce point-à-temps tooa nouveau serveur. Les données supprimées, vous pouvez utiliser cette nouvelle toorecover de serveur. Hello suivant étapes restauration hello exemple server tooa point avant hello table a été ajoutée.

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Hello `az postgres server restore` commande doit hello paramètres suivants :
| Paramètre | Valeur suggérée | Description  |
| --- | --- | --- |
| --resource-group |  myResourceGroup |  Le groupe de ressources dans le hello serveur source existe.  |
| --name | mypgserver-restored | nom Hello hello nouveau serveur qui est créé par la commande de restauration hello. |
| restore-point-in-time | 2017-04-13T13:59:00Z | Sélectionnez un toorestore point-à-temps pour. Cette date / heure doivent être au sein de la période de rétention de sauvegarde du serveur hello source. Utilisez le format de date et d’heure ISO8601. Par exemple, vous pouvez utiliser votre fuseau horaire local, comme `2017-04-13T05:59:00-08:00`, ou le format UTC Zulu `2017-04-13T13:59:00Z`. |
| --source-server | mypgserver-20170401 | nom de Hello ou ID de hello toorestore de serveur source à partir de. |

Restauration d’un serveur tooa point-à-temps crée un nouvelle copie d’un serveur, en tant que serveur d’origine de hello sous la forme hello point dans le temps que vous spécifiez. emplacement de Hello et la tarification des valeurs de niveau pour le serveur de hello restauré sont hello même en tant que serveur de source de hello.

commande Hello est synchrone et retourne une fois hello serveur est restauré. Une fois la restauration de hello terminée, recherchez hello nouveau serveur qui a été créé. Vérifiez que hello données ont été restaurées comme prévu.


## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment toouse Azure CLI (interface de ligne de commande) et d’autres utilitaires pour :
> [!div class="checklist"]
> * Créer une base de données Azure pour PostgreSQL
> * Configurer le pare-feu du serveur hello
> * Utilisez [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilitaire toocreate une base de données
> * Charger les exemples de données
> * Données de requête
> * Mettre à jour des données
> * Restaurer des données

Ensuite, découvrez comment toouse hello des tâches similaires toodo portail Azure, passez en revue ce didacticiel : [concevoir votre première base de données Azure pour à l’aide de PostgreSQL hello portail Azure](tutorial-design-database-using-azure-portal.md)
