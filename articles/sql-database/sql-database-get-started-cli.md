---
title: "Interface de ligne de commande Azure : Créer une base de données SQL | Microsoft Docs"
description: "Découvrez comment toocreate un serveur logique de base de données SQL, la règle de pare-feu de niveau serveur et bases de données à l’aide de hello CLI d’Azure."
keywords: "didacticiel sur la base de données sql, créer une base de données sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a>Créer une seule base de données SQL Azure à l’aide de hello CLI d’Azure

Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts. Ce guide hello CLI d’Azure toodeploy en utilisant une base de données SQL Azure dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) dans un [serveur logique de base de données SQL Azure](sql-database-features.md).

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="define-variables"></a>Définir des variables

Définir des variables pour une utilisation dans les scripts hello dans ce démarrage rapide.

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md) à l’aide de hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe. Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westeurope` emplacement.

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a>Création d'un serveur logique

Créer un [serveur logique de base de données SQL Azure](sql-database-features.md) à l’aide de hello [az sql server créer](/cli/azure/sql/server#create) commande. Un serveur logique contient un groupe de bases de données gérées en tant que groupe. Hello exemple suivant crée un serveur nommé de façon aléatoire dans votre groupe de ressources avec une connexion d’administration nommée `ServerAdmin` et un mot de passe de `ChangeYourAdminPassword1`. Remplacez les valeurs prédéfinies par ce que vous souhaitez.

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a>Configurer une règle de pare-feu du serveur

Créer un [règle de pare-feu de niveau serveur de base de données SQL Azure](sql-database-firewall-configure.md) à l’aide de hello [créer de pare-feu du serveur sql az](/cli/azure/sql/server/firewall-rule#create) commande. Une règle de pare-feu de niveau serveur permet à une application externe, telles que SQL Server Management Studio ou hello SQLCMD utilitaire tooconnect tooa base de données SQL via le pare-feu de service de base de données SQL hello. Dans l’exemple suivant de hello, hello pare-feu est uniquement ouvert pour d’autres ressources Azure. connectivité externe tooenable, modification hello adresse tooan appropriée d’adresses IP pour votre environnement. tooopen toutes les adresses IP, utilisez 0.0.0.0 comme hello à partir d’adresse IP et 255.255.255.255 comme adresse de fin de hello.  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> SQL Database communique par le biais du port 1433. Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 1433 ne peut pas être autorisé par le pare-feu de votre réseau. Dans ce cas, vous ne serez pas de serveur de base de données SQL Azure en mesure de tooconnect tooyour, sauf si votre service informatique s’ouvre le port 1433.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>Créer une base de données de serveur hello avec des exemples de données

Créer une base de données avec un [niveau de performance S0](sql-database-service-tiers.md) dans server hello à l’aide de hello [créer de base de données sql az](/cli/azure/sql/db#create) commande. Hello exemple suivant crée une base de données appelée `mySampleDatabase` et charges hello des exemples de données AdventureWorksLT dans cette base de données. Remplacer ces prédéfinis des valeurs comme vous le souhaitez (autres Démarrages rapides dans cette version de la collection des valeurs hello dans ce démarrage rapide).

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a>Supprimer des ressources

Les autres démarrages rapides de cette collection reposent sur ce démarrage rapide. 

> [!TIP]
> Si vous prévoyez toocontinue toowork avec les Démarrages rapides suivants, ne pas nettoyer les ressources hello créés dans cette rapide démarrent. Si vous n’envisagez pas de toocontinue, utilisez hello suivant toodelete suit toutes les ressources créées par ce guide de démarrage rapide Bonjour portail Azure.
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous disposez d’une base de données, vous pouvez vous connecter et interroger à l’aide de vos outils préférés. En savoir plus en choisissant votre outil ci-dessous :

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.JS](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

