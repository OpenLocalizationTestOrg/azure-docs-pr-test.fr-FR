---
title: "Créer une base de données Azure PostgreSQL à l’aide de hello CLI d’Azure | Documents Microsoft"
description: "Rapide toocreate du guide de démarrage et gérer la base de données Azure pour le serveur de PostgreSQL à l’aide d’Azure CLI (interface de ligne de commande)."
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: 946aa3cbf5ff9f5ac4e51248412d3da5d718141e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a>Créer une base de données Azure PostgreSQL à l’aide de hello CLI d’Azure
Base de données Azure pour PostgreSQL est un service géré qui vous permet de toorun, gérer et mettre à l’échelle des bases de données PostgreSQL hautement disponibles dans le cloud de hello. Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts. Ce démarrage rapide vous montre comment toocreate Azure de base de données pour le serveur PostgreSQL dans un [groupe de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) à l’aide de hello CLI d’Azure.

Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

Si vous avez plusieurs abonnements, choisir l’abonnement approprié de hello dans lequel les ressources hello seront facturé. Sélectionnez un ID d’abonnement spécifique sous votre compte à l’aide de la commande [az account set](/cli/azure/account#set).
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

Hello exemple suivant crée un serveur nommé `mypgserver-20170401` dans votre groupe de ressources `myresourcegroup` avec ouverture de session de serveur admin `mylogin`. Hello nom d’un serveur mappe le nom de tooDNS et est donc requis toobe globalement unique dans Azure. Hello de substitution `<server_admin_password>` avec votre propre valeur.
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
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

## <a name="connect-toopostgresql-database-using-psql"></a>Se connecter à l’aide de psql de la base de données tooPostgreSQL

Si votre ordinateur client a PostgreSQL installé, vous pouvez utiliser une instance locale de [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL serveur. Nous allons maintenant utiliser server de hello psql utilitaire de ligne de commande tooconnect toohello Azure PostgreSQL.

1. Exécutez hello suivant psql commande tooconnect tooan Azure de base de données PostgreSQL serveur
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  Par exemple, hello commande suivante connecte à base de données de la valeur par défaut toohello appelée **postgres** sur votre serveur PostgreSQL **mypgserver-20170401.postgres.database.azure.com** à l’aide des informations d’identification d’accès. Entrez hello `<server_admin_password>` vous avez choisi à l’invite de mot de passe.
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  Une fois que vous êtes connecté toohello server, créez une base de données vide à l’invite de hello.
```sql
CREATE DATABASE mypgsqldb;
```

3.  À l’invite de hello, exécutez hello suivant de base de données de commande tooswitch connexion toohello nouvellement créé **mypgsqldb**:
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a>Se connecter à l’aide de pgAdmin de la base de données tooPostgreSQL

tooconnect tooAzure PostgreSQL serveur à l’aide d’outil d’interface utilisateur graphique de hello _pgAdmin_
1.  Lancez hello _pgAdmin_ application sur votre ordinateur client. Vous pouvez installer _pgAdmin_ à partir de http://www.pgadmin.org/.
2.  Choisissez **ajouter un nouveau serveur** de hello **liens rapides** menu.
3.  Bonjour **Create - Server** boîte de dialogue **général** , entrez un nom convivial unique pour le serveur de hello. Par exemple **Serveur Azure PostgreSQL**.
 ![Outil pgAdmin - Créer - Serveur](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)
4.  Bonjour **Create - Server** boîte de dialogue, **connexion** onglet :
    - Entrez le nom du serveur complet hello (par exemple, **mypgserver-20170401.postgres.database.azure.com**) Bonjour **nom d’hôte / adresse** boîte. 
    - Entrez le port 5432 dans hello **Port** boîte. 
    - Entrez hello **connexion d’administration de serveur (user@mypgserver)** obtenu précédemment dans ce démarrage rapide et un mot de passe entré lors de la création d’un serveur de hello en hello **nom d’utilisateur** et **mot de passe** zones, respectivement.
    - Sélectionnez **Requis** pour **Mode SSL**. Par défaut, tous les serveurs Azure PostgreSQL sont créés avec l’application du SSL activée. tooturn hors tension de l’application de SSL, consultez les détails dans [SSL de l’application](./concepts-ssl-connection-security.md).

    ![pgAdmin - Créer - Serveur](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  Cliquez sur **Enregistrer**.
6.  Dans le volet gauche du navigateur hello, développez hello **groupes de serveurs**. Choisissez votre serveur **Serveur Azure PostgreSQL**.
7.  Choisissez hello **Server** vous connecté à, puis choisissez **bases de données** sous celle-ci. 
8.  Avec le bouton droit sur **bases de données** tooCreate une base de données.
9.  Choisissez un nom de base de données **mypgsqldb** et propriétaire hello pour qu’il en tant que compte de connexion admin server **mylogin**.
10. Cliquez sur **enregistrer** toocreate une base de données vide.
11. Bonjour **navigateur**, développez hello **serveurs** groupe. Développez serveur hello vous avez créé et la base de données hello **mypgsqldb** sous celle-ci.
 ![pgAdmin - Créer - Base de données](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)


## <a name="clean-up-resources"></a>Supprimer des ressources

Nettoyer toutes les ressources que vous avez créé dans démarrage rapide de hello en supprimant hello [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md).

> [!TIP]
> Les autres démarrages rapides de cette collection reposent sur ce démarrage rapide. Si vous prévoyez toocontinue toowork avec ultérieures Démarrages rapides, effectuez pas nettoyer les hello ressources créées dans ce démarrage rapide. Si vous n’envisagez pas de toocontinue, utilisez hello suivant les étapes toodelete toutes les ressources créées par ce démarrage rapide Bonjour CLI d’Azure.

```azurecli-interactive
az group delete --name myresourcegroup
```

Si vous souhaitez simplement que toodelete hello un nouveau serveur, vous pouvez exécuter [suppression du serveur az postgres](/cli/azure/postgres/server#delete) commande.
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Migration de votre base de données PostgreSQL par exportation et importation](./howto-migrate-using-export-and-import.md)
