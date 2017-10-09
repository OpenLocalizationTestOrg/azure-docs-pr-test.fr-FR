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
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="0d423-103">Création d’un serveur Azure Database pour MySQL à l’aide de la CLI Azure</span><span class="sxs-lookup"><span data-stu-id="0d423-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="0d423-104">Ce démarrage rapide explique comment toouse hello CLI d’Azure toocreate une base de données Azure du serveur MySQL dans un groupe de ressources Azure dans environ cinq minutes.</span><span class="sxs-lookup"><span data-stu-id="0d423-104">This quickstart describes how toouse hello Azure CLI toocreate an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="0d423-105">Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="0d423-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span>

<span data-ttu-id="0d423-106">Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="0d423-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0d423-107">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0d423-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0d423-108">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="0d423-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0d423-109">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0d423-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="0d423-110">Si vous avez plusieurs abonnements, choisir l’abonnement approprié de hello dans lequel les ressources hello existent ou sont facturé pour.</span><span class="sxs-lookup"><span data-stu-id="0d423-110">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="0d423-111">Sélectionnez un ID d’abonnement spécifique sous votre compte à l’aide de la commande [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="0d423-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="0d423-112">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="0d423-112">Create a resource group</span></span>
<span data-ttu-id="0d423-113">Créer un [groupe de ressources Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) à l’aide de hello [création de groupe de az](https://docs.microsoft.com/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="0d423-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="0d423-114">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées en tant que groupe.</span><span class="sxs-lookup"><span data-stu-id="0d423-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="0d423-115">Hello exemple suivant crée un groupe de ressources nommé `myresourcegroup` Bonjour `westus` emplacement.</span><span class="sxs-lookup"><span data-stu-id="0d423-115">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="0d423-116">Créer un serveur de base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="0d423-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="0d423-117">Créer une base de données Azure pour le serveur MySQL avec hello **az mysql server créer** commande.</span><span class="sxs-lookup"><span data-stu-id="0d423-117">Create an Azure Database for MySQL server with hello **az mysql server create** command.</span></span> <span data-ttu-id="0d423-118">Un serveur peut gérer plusieurs bases de données.</span><span class="sxs-lookup"><span data-stu-id="0d423-118">A server can manage multiple databases.</span></span> <span data-ttu-id="0d423-119">En règle générale, une base de données distincte est utilisée pour chaque projet ou pour chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0d423-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="0d423-120">Hello exemple suivant crée une base de données Azure pour le serveur MySQL situé dans `westus` dans le groupe de ressources hello `myresourcegroup` avec le nom `myserver4demo`.</span><span class="sxs-lookup"><span data-stu-id="0d423-120">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="0d423-121">serveur de Hello possède un journal de l’administrateur dans nommé `myadmin` et le mot de passe `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="0d423-121">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="0d423-122">Hello serveur est créé avec **base** niveau de performances et **50** unités partagées entre toutes les bases de données hello dans le serveur de hello de calcul.</span><span class="sxs-lookup"><span data-stu-id="0d423-122">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="0d423-123">Vous pouvez faire évoluer calcul et stockage vers le haut ou vers le bas en fonction des besoins de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0d423-123">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="0d423-124">Configurer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="0d423-124">Configure firewall rule</span></span>
<span data-ttu-id="0d423-125">Créer une base de données Azure pour la règle de pare-feu de niveau serveur MySQL à l’aide de hello **az mysql server-règle de pare-feu créer** commande.</span><span class="sxs-lookup"><span data-stu-id="0d423-125">Create an Azure Database for MySQL server-level firewall rule using hello **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="0d423-126">Une règle de pare-feu de niveau serveur permet à une application externe, par exemple hello **mysql.exe** outil de ligne de commande ou serveur de tooyour tooconnect de banc d’essai MySQL via le pare-feu de service Azure MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="0d423-126">A server-level firewall rule allows an external application, such as hello **mysql.exe** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="0d423-127">Hello exemple suivant crée une règle de pare-feu pour une plage d’adresses prédéfinies qui, dans cet exemple, est hello ensemble possible de plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="0d423-127">hello following example creates a firewall rule for a predefined address range, which in this example is hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="0d423-128">Configurer les paramètres SSL</span><span class="sxs-lookup"><span data-stu-id="0d423-128">Configure SSL settings</span></span>
<span data-ttu-id="0d423-129">Par défaut, des connexions SSL entre votre serveur et les applications clientes sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="0d423-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="0d423-130">Cela garantit la sécurité de « en mouvement » données en chiffrant les flux de données hello sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="0d423-130">This ensures security of "in-motion" data by encrypting hello data stream over hello internet.</span></span>  <span data-ttu-id="0d423-131">toomake cette prise en main plus facilement, nous désactivons les connexions SSL pour votre serveur.</span><span class="sxs-lookup"><span data-stu-id="0d423-131">toomake this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="0d423-132">Cette opération n’est pas recommandée pour les serveurs de production.</span><span class="sxs-lookup"><span data-stu-id="0d423-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="0d423-133">Pour plus d’informations, consultez [tooAzure base de données de connexion de connectivité configurez SSL dans votre application de toosecurely pour MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="0d423-133">For more information, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="0d423-134">Hello exemple suivant désactive la mise en œuvre de SSL sur votre serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="0d423-134">hello following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a><span data-ttu-id="0d423-135">Obtenir des informations de connexion hello</span><span class="sxs-lookup"><span data-stu-id="0d423-135">Get hello connection information</span></span>

<span data-ttu-id="0d423-136">tooconnect tooyour server, vous devez tooprovide hôte accéder aux informations et informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="0d423-136">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="0d423-137">résultat de Hello est au format JSON.</span><span class="sxs-lookup"><span data-stu-id="0d423-137">hello result is in JSON format.</span></span> <span data-ttu-id="0d423-138">Prenez note de hello **fullyQualifiedDomainName** et **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="0d423-138">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a><span data-ttu-id="0d423-139">Connexion serveur toohello à l’aide d’outil de ligne de commande hello mysql.exe</span><span class="sxs-lookup"><span data-stu-id="0d423-139">Connect toohello server using hello mysql.exe command-line tool</span></span>
<span data-ttu-id="0d423-140">Connexion serveur tooyour à l’aide de hello **mysql.exe** outil de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="0d423-140">Connect tooyour server using hello **mysql.exe** command-line tool.</span></span> <span data-ttu-id="0d423-141">Vous pouvez télécharger MySQL [ici](https://dev.mysql.com/downloads/) et l’installer sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0d423-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="0d423-142">Au lieu de cela, vous pouvez également cliquer hello **essayer** bouton sur les exemples de code ou hello `>_` bouton hello supérieure droite barre d’outils hello portail Azure et lancement hello **Azure Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="0d423-142">Instead you may also click hello **Try It** button on code samples, or hello  `>_` button from hello upper right toolbar in hello Azure portal, and launch hello **Azure Cloud Shell**.</span></span>

<span data-ttu-id="0d423-143">Tapez les commandes suivants hello :</span><span class="sxs-lookup"><span data-stu-id="0d423-143">Type hello next commands:</span></span> 

1. <span data-ttu-id="0d423-144">Connectez-vous à l’aide du serveur toohello **mysql** outil de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="0d423-144">Connect toohello server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="0d423-145">Afficher l’état du serveur :</span><span class="sxs-lookup"><span data-stu-id="0d423-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="0d423-146">Si tout se passe bien, outil de ligne de commande hello doit générer hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="0d423-146">If everything goes well, hello command-line tool should output hello following text:</span></span>

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
> <span data-ttu-id="0d423-147">Pour les autres commandes, consultez le [Manuel de référence de MySQL 5.7 - Chapitre 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span><span class="sxs-lookup"><span data-stu-id="0d423-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a><span data-ttu-id="0d423-148">Connexion serveur toohello à l’aide d’outil d’interface utilisateur graphique de banc d’essai MySQL hello</span><span class="sxs-lookup"><span data-stu-id="0d423-148">Connect toohello server using hello MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="0d423-149">Lancez hello application banc d’essai MySQL sur votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="0d423-149">Launch hello MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="0d423-150">Vous pouvez télécharger et installer MySQL Workbench à partir [d’ici](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="0d423-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="0d423-151">Bonjour **le programme d’installation nouvelle connexion** boîte de dialogue, entrez hello suivant des informations sur la zone **paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="0d423-151">In hello **Setup New Connection** dialog box, enter hello following information on **Parameters** tab:</span></span>

   ![configurer une nouvelle connexion](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="0d423-153">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="0d423-153">**Setting**</span></span> | <span data-ttu-id="0d423-154">**Valeur suggérée**</span><span class="sxs-lookup"><span data-stu-id="0d423-154">**Suggested Value**</span></span> | <span data-ttu-id="0d423-155">**Description**</span><span class="sxs-lookup"><span data-stu-id="0d423-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="0d423-156">Nom de connexion</span><span class="sxs-lookup"><span data-stu-id="0d423-156">Connection Name</span></span> | <span data-ttu-id="0d423-157">Ma connexion</span><span class="sxs-lookup"><span data-stu-id="0d423-157">My Connection</span></span> | <span data-ttu-id="0d423-158">Spécifiez une étiquette pour cette connexion (il peut s’agir de n’importe quoi)</span><span class="sxs-lookup"><span data-stu-id="0d423-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="0d423-159">Méthode de connexion</span><span class="sxs-lookup"><span data-stu-id="0d423-159">Connection Method</span></span> | <span data-ttu-id="0d423-160">choisissez Standard (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="0d423-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="0d423-161">Utilisez tooAzure tooconnect de protocole TCP/IP de base de données de MySQL ></span><span class="sxs-lookup"><span data-stu-id="0d423-161">Use TCP/IP protocol tooconnect tooAzure Database for MySQL></span></span> |
| <span data-ttu-id="0d423-162">Nom d’hôte</span><span class="sxs-lookup"><span data-stu-id="0d423-162">Hostname</span></span> | <span data-ttu-id="0d423-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="0d423-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="0d423-164">Nom du serveur que vous avez noté précédemment</span><span class="sxs-lookup"><span data-stu-id="0d423-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="0d423-165">Port</span><span class="sxs-lookup"><span data-stu-id="0d423-165">Port</span></span> | <span data-ttu-id="0d423-166">3306</span><span class="sxs-lookup"><span data-stu-id="0d423-166">3306</span></span> | <span data-ttu-id="0d423-167">port par défaut Hello MySQL est utilisé.</span><span class="sxs-lookup"><span data-stu-id="0d423-167">hello default port for MySQL is used.</span></span> |
| <span data-ttu-id="0d423-168">Nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="0d423-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="0d423-169">connexion d’administration de serveur Hello noté précédemment.</span><span class="sxs-lookup"><span data-stu-id="0d423-169">hello server admin login you previously noted.</span></span> |
| <span data-ttu-id="0d423-170">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="0d423-170">Password</span></span> | **** | <span data-ttu-id="0d423-171">Utilisez hello compte mot de passe administrateur que vous avez configurée précédemment.</span><span class="sxs-lookup"><span data-stu-id="0d423-171">Use hello admin account password you configured earlier.</span></span> |

<span data-ttu-id="0d423-172">Cliquez sur **tester la connexion** tootest si tous les paramètres sont configurés correctement.</span><span class="sxs-lookup"><span data-stu-id="0d423-172">Click **Test Connection** tootest if all parameters are correctly configured.</span></span>
<span data-ttu-id="0d423-173">Maintenant, vous pouvez cliquer sur les connexions hello toosuccessfully connecter toohello server.</span><span class="sxs-lookup"><span data-stu-id="0d423-173">Now, you can click hello connection toosuccessfully connect toohello server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="0d423-174">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="0d423-174">Clean up resources</span></span>
<span data-ttu-id="0d423-175">Si vous n’avez pas besoin ces ressources pour un autre/didacticiel de démarrage rapide, vous pouvez les supprimer en procédant comme hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0d423-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing hello following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="0d423-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0d423-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0d423-177">Conception d’une base de données MySQL avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0d423-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
