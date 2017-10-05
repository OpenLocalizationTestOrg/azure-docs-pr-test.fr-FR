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
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 04fc441aee7a4c8adc4f02d5e51b2d9e64400f55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="2e366-103">Création d’un serveur Azure Database pour MySQL à l’aide de la CLI Azure</span><span class="sxs-lookup"><span data-stu-id="2e366-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="2e366-104">Ce guide de démarrage rapide explique comment utiliser l’interface CLI Azure pour créer un serveur Azure Database pour MySQL dans un groupe de ressources Azure en environ cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="2e366-104">This quickstart describes how to use the Azure CLI to create an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="2e366-105">L’interface de ligne de commande (CLI) Azure permet de créer et gérer des ressources Azure à partir de la ligne de commande ou dans les scripts.</span><span class="sxs-lookup"><span data-stu-id="2e366-105">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span>

<span data-ttu-id="2e366-106">Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="2e366-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2e366-107">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="2e366-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2e366-108">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="2e366-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="2e366-109">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2e366-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="2e366-110">Si vous possédez plusieurs abonnements, sélectionnez l’abonnement approprié dans lequel la ressource existe ou est facturée.</span><span class="sxs-lookup"><span data-stu-id="2e366-110">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="2e366-111">Sélectionnez un ID d’abonnement spécifique sous votre compte à l’aide de la commande [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="2e366-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="2e366-112">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="2e366-112">Create a resource group</span></span>
<span data-ttu-id="2e366-113">Créez un [groupe de ressources Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) avec la commande [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="2e366-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="2e366-114">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="2e366-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="2e366-115">L’exemple suivant crée un groupe de ressources nommé `myresourcegroup` à l’emplacement `westus`.</span><span class="sxs-lookup"><span data-stu-id="2e366-115">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="2e366-116">Créer un serveur de base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="2e366-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="2e366-117">Créez un serveur Azure Database pour MySQL avec la commande **az sql server create**.</span><span class="sxs-lookup"><span data-stu-id="2e366-117">Create an Azure Database for MySQL server with the **az mysql server create** command.</span></span> <span data-ttu-id="2e366-118">Un serveur peut gérer plusieurs bases de données.</span><span class="sxs-lookup"><span data-stu-id="2e366-118">A server can manage multiple databases.</span></span> <span data-ttu-id="2e366-119">En règle générale, une base de données distincte est utilisée pour chaque projet ou pour chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2e366-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="2e366-120">L’exemple suivant crée un serveur Azure Database pour MySQL situé dans `westus` dans le groupe de ressources `myresourcegroup` avec le nom `myserver4demo`.</span><span class="sxs-lookup"><span data-stu-id="2e366-120">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="2e366-121">Le serveur dispose d’une connexion administrateur avec le nom `myadmin` et le mot de passe `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="2e366-121">The server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="2e366-122">Le serveur est créé avec le niveau de performance **De base** et **50** unités de calcul partagées entre toutes les bases de données dans le serveur.</span><span class="sxs-lookup"><span data-stu-id="2e366-122">The server is created with **Basic** performance tier and **50** compute units shared between all the databases in the server.</span></span> <span data-ttu-id="2e366-123">Vous pouvez faire augmenter ou diminuer le calcul et le stockage selon les besoins de l’application.</span><span class="sxs-lookup"><span data-stu-id="2e366-123">You can scale compute and storage up or down depending on the application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="2e366-124">Configurer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="2e366-124">Configure firewall rule</span></span>
<span data-ttu-id="2e366-125">Créez une règle de pare-feu au niveau du serveur Azure Database pour MySQL avec la commande **az mysql server firewall-rule create**.</span><span class="sxs-lookup"><span data-stu-id="2e366-125">Create an Azure Database for MySQL server-level firewall rule using the **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="2e366-126">Une règle de pare-feu au niveau du serveur permet à une application externe, comme l’outil de ligne de commande **mysql.exe** ou MySQL Workbench de se connecter à votre serveur via le pare-feu du service Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="2e366-126">A server-level firewall rule allows an external application, such as the **mysql.exe** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="2e366-127">L’exemple suivant illustre la création d’une règle de pare-feu pour une plage d’adresses prédéfinie qui, ici, est l’intégralité de la plage d’adresses IP possible.</span><span class="sxs-lookup"><span data-stu-id="2e366-127">The following example creates a firewall rule for a predefined address range, which in this example is the entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="2e366-128">Configurer les paramètres SSL</span><span class="sxs-lookup"><span data-stu-id="2e366-128">Configure SSL settings</span></span>
<span data-ttu-id="2e366-129">Par défaut, des connexions SSL entre votre serveur et les applications clientes sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="2e366-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="2e366-130">Cela garantit la sécurité des données « en mouvement » en chiffrant le flux de données sur Internet.</span><span class="sxs-lookup"><span data-stu-id="2e366-130">This ensures security of "in-motion" data by encrypting the data stream over the internet.</span></span>  <span data-ttu-id="2e366-131">Pour faciliter ce démarrage rapide, nous désactivons les connexions SSL pour votre serveur.</span><span class="sxs-lookup"><span data-stu-id="2e366-131">To make this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="2e366-132">Cette opération n’est pas recommandée pour les serveurs de production.</span><span class="sxs-lookup"><span data-stu-id="2e366-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="2e366-133">Pour plus d’informations, consultez l’article [Configuration de la connectivité SSL dans votre application pour se connecter en toute sécurité à la base de données Azure pour MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="2e366-133">For more information, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="2e366-134">L’exemple suivant désactive l’application de SSL sur votre serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="2e366-134">The following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-the-connection-information"></a><span data-ttu-id="2e366-135">Obtenir les informations de connexion</span><span class="sxs-lookup"><span data-stu-id="2e366-135">Get the connection information</span></span>

<span data-ttu-id="2e366-136">Pour vous connecter à votre serveur, vous devez fournir des informations sur l’hôte et des informations d’identification pour l’accès.</span><span class="sxs-lookup"><span data-stu-id="2e366-136">To connect to your server, you need to provide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="2e366-137">Le résultat est au format JSON.</span><span class="sxs-lookup"><span data-stu-id="2e366-137">The result is in JSON format.</span></span> <span data-ttu-id="2e366-138">Prenez note du **fullyQualifiedDomainName** et du **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="2e366-138">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-to-the-server-using-the-mysqlexe-command-line-tool"></a><span data-ttu-id="2e366-139">Connectez-vous au serveur avec l’outil de ligne de commande mysql.exe</span><span class="sxs-lookup"><span data-stu-id="2e366-139">Connect to the server using the mysql.exe command-line tool</span></span>
<span data-ttu-id="2e366-140">Connectez-vous à votre serveur avec l’outil en ligne de commande **mysql.exe**.</span><span class="sxs-lookup"><span data-stu-id="2e366-140">Connect to your server using the **mysql.exe** command-line tool.</span></span> <span data-ttu-id="2e366-141">Vous pouvez télécharger MySQL [ici](https://dev.mysql.com/downloads/) et l’installer sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2e366-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="2e366-142">Une autre possibilité consiste à cliquer sur le bouton **Essayer** des exemples de code ou sur le bouton `>_` de la barre d’outils supérieure droite du Portail Azure et à lancer **Azure Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="2e366-142">Instead you may also click the **Try It** button on code samples, or the  `>_` button from the upper right toolbar in the Azure portal, and launch the **Azure Cloud Shell**.</span></span>

<span data-ttu-id="2e366-143">Tapez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2e366-143">Type the next commands:</span></span> 

1. <span data-ttu-id="2e366-144">Connectez-vous au serveur avec l’outil de ligne de commande **mysql** :</span><span class="sxs-lookup"><span data-stu-id="2e366-144">Connect to the server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="2e366-145">Afficher l’état du serveur :</span><span class="sxs-lookup"><span data-stu-id="2e366-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="2e366-146">Si tout se déroule correctement, l’outil en ligne de commande doit générer le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="2e366-146">If everything goes well, the command-line tool should output the following text:</span></span>

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
> <span data-ttu-id="2e366-147">Pour les autres commandes, consultez le [Manuel de référence de MySQL 5.7 - Chapitre 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span><span class="sxs-lookup"><span data-stu-id="2e366-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-to-the-server-using-the-mysql-workbench-gui-tool"></a><span data-ttu-id="2e366-148">Connectez-vous au serveur à l’aide de l’outil MySQL Workbench GUI</span><span class="sxs-lookup"><span data-stu-id="2e366-148">Connect to the server using the MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="2e366-149">Lancez l’application MySQL Workbench sur votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="2e366-149">Launch the MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="2e366-150">Vous pouvez télécharger et installer MySQL Workbench à partir [d’ici](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="2e366-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="2e366-151">Dans la boîte de dialogue **Configurer une nouvelle connexion**, entrez les informations suivantes dans l’onglet **Paramètres** :</span><span class="sxs-lookup"><span data-stu-id="2e366-151">In the **Setup New Connection** dialog box, enter the following information on **Parameters** tab:</span></span>

   ![configurer une nouvelle connexion](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="2e366-153">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="2e366-153">**Setting**</span></span> | <span data-ttu-id="2e366-154">**Valeur suggérée**</span><span class="sxs-lookup"><span data-stu-id="2e366-154">**Suggested Value**</span></span> | <span data-ttu-id="2e366-155">**Description**</span><span class="sxs-lookup"><span data-stu-id="2e366-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="2e366-156">Nom de connexion</span><span class="sxs-lookup"><span data-stu-id="2e366-156">Connection Name</span></span> | <span data-ttu-id="2e366-157">Ma connexion</span><span class="sxs-lookup"><span data-stu-id="2e366-157">My Connection</span></span> | <span data-ttu-id="2e366-158">Spécifiez une étiquette pour cette connexion (il peut s’agir de n’importe quoi)</span><span class="sxs-lookup"><span data-stu-id="2e366-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="2e366-159">Méthode de connexion</span><span class="sxs-lookup"><span data-stu-id="2e366-159">Connection Method</span></span> | <span data-ttu-id="2e366-160">choisissez Standard (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="2e366-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="2e366-161">Utilisez le protocole TCP/IP pour vous connecter à la base de données Azure pour MySQL></span><span class="sxs-lookup"><span data-stu-id="2e366-161">Use TCP/IP protocol to connect to Azure Database for MySQL></span></span> |
| <span data-ttu-id="2e366-162">Nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="2e366-162">Hostname</span></span> | <span data-ttu-id="2e366-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="2e366-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="2e366-164">Nom du serveur que vous avez noté précédemment</span><span class="sxs-lookup"><span data-stu-id="2e366-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="2e366-165">Port</span><span class="sxs-lookup"><span data-stu-id="2e366-165">Port</span></span> | <span data-ttu-id="2e366-166">3306</span><span class="sxs-lookup"><span data-stu-id="2e366-166">3306</span></span> | <span data-ttu-id="2e366-167">Le port par défaut pour MySQL est utilisé</span><span class="sxs-lookup"><span data-stu-id="2e366-167">The default port for MySQL is used.</span></span> |
| <span data-ttu-id="2e366-168">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2e366-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="2e366-169">Connexion d’administrateur serveur que vous avez notée précédemment</span><span class="sxs-lookup"><span data-stu-id="2e366-169">The server admin login you previously noted.</span></span> |
| <span data-ttu-id="2e366-170">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="2e366-170">Password</span></span> | **** | <span data-ttu-id="2e366-171">Utilisez le mot de passe du compte Administrateur que vous avez configuré précédemment</span><span class="sxs-lookup"><span data-stu-id="2e366-171">Use the admin account password you configured earlier.</span></span> |

<span data-ttu-id="2e366-172">Cliquez sur **Tester la connexion** pour tester si tous les paramètres sont correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="2e366-172">Click **Test Connection** to test if all parameters are correctly configured.</span></span>
<span data-ttu-id="2e366-173">À présent, vous pouvez cliquer sur la connexion pour vous connecter au serveur.</span><span class="sxs-lookup"><span data-stu-id="2e366-173">Now, you can click the connection to successfully connect to the server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="2e366-174">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="2e366-174">Clean up resources</span></span>
<span data-ttu-id="2e366-175">Si vous n’avez pas besoin de ces ressources pour un autre guide de démarrage rapide ou didacticiel, vous pouvez les supprimer en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2e366-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing the following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="2e366-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e366-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2e366-177">Conception d’une base de données MySQL avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2e366-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
