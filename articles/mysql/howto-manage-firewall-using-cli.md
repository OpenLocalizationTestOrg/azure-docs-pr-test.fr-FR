---
title: "aaaCreate et gérer la base de données Azure MySQL aux règles de pare-feu à l’aide d’Azure CLI | Documents Microsoft"
description: "Cet article décrit comment toocreate et gérer la base de données Azure MySQL aux règles de pare-feu à l’aide de la ligne de commande CLI d’Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="4e05a-103">Création et gestion des règles de pare-feu Azure Database pour MySQL à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="4e05a-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="4e05a-104">Les règles de pare-feu de niveau serveur activer administrateurs toomanage accès tooan base de données Azure pour MySQL Server à partir d’une adresse IP spécifique ou de la plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="4e05a-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="4e05a-105">À l’aide des commandes CLI d’Azure pratiques, vous pouvez créer, mettre à jour, supprimer, répertorier et afficher toomanage de règles de pare-feu de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="4e05a-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="4e05a-106">Pour une vue d’ensemble des pare-feu Azure Database pour MySQL, consultez la rubrique [Règles de pare-feu d’Azure Database pour MySQL](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="4e05a-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e05a-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4e05a-107">Prerequisites</span></span>
* [<span data-ttu-id="4e05a-108">Installation d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4e05a-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="4e05a-109">Installation du Kit de développement logiciel (SDK) Python pour les services PostgreSQL et MySQL</span><span class="sxs-lookup"><span data-stu-id="4e05a-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="4e05a-110">Installer le composant de CLI d’Azure hello pour les services PostgreSQL et MySQL</span><span class="sxs-lookup"><span data-stu-id="4e05a-110">Install hello Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="4e05a-111">Créer un serveur de base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4e05a-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="4e05a-112">Commandes des règles de pare-feu :</span><span class="sxs-lookup"><span data-stu-id="4e05a-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="4e05a-113">Hello **az mysql server-règle de pare-feu** commande est utilisée à partir d’Azure CLI toocreate, supprimer, répertorier, afficher et mettre à jour les règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="4e05a-113">hello **az mysql server firewall-rule** command is used from Azure CLI toocreate, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="4e05a-114">Commandes :</span><span class="sxs-lookup"><span data-stu-id="4e05a-114">Commands:</span></span>
- <span data-ttu-id="4e05a-115">**create** : créez une règle de pare-feu du serveur Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="4e05a-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="4e05a-116">**delete** : supprimez une règle de pare-feu du serveur Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="4e05a-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="4e05a-117">**liste** : liste des règles de pare-feu de serveur MySQL de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4e05a-117">**list** : List hello Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="4e05a-118">**afficher** : afficher les détails de hello d’un serveur MySQL de Azure règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="4e05a-118">**show** : Show hello details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="4e05a-119">**update**: mettez à jour une règle de pare-feu du serveur Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="4e05a-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="4e05a-120">Connexion tooAzure liste et votre base de données Azure pour serveurs MySQL</span><span class="sxs-lookup"><span data-stu-id="4e05a-120">Login tooAzure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="4e05a-121">Connectez-vous en toute sécurité à votre compte Azure à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="4e05a-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="4e05a-122">Hello d’utilisation **ouverture de session az** commande toodo cela.</span><span class="sxs-lookup"><span data-stu-id="4e05a-122">Use hello **az login** command toodo this.</span></span>

1. <span data-ttu-id="4e05a-123">Exécutez hello de commande suivante à partir de la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="4e05a-123">Run hello following command from hello command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="4e05a-124">Cette commande génère un code toouse à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="4e05a-124">This command will output a code toouse in hello next step.</span></span>

2. <span data-ttu-id="4e05a-125">Utiliser une page hello navigateur tooopen [https://aka.ms/devicelogin](https://aka.ms/devicelogin) et entrez le code de hello.</span><span class="sxs-lookup"><span data-stu-id="4e05a-125">Use a web browser tooopen hello page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter hello code.</span></span>

3. <span data-ttu-id="4e05a-126">À l’invite de hello, connectez-vous en utilisant vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="4e05a-126">At hello prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="4e05a-127">Une fois que votre connexion est autorisée, une liste des abonnements est imprimée dans la console hello.</span><span class="sxs-lookup"><span data-stu-id="4e05a-127">Once your login is authorized, a list of subscriptions will be printed in hello console.</span></span> <span data-ttu-id="4e05a-128">Id du hello Hello souhaité abonnement tooset hello actuel abonnement toobe utilisé progresser.</span><span class="sxs-lookup"><span data-stu-id="4e05a-128">Copy hello id of hello desired subscription tooset hello current subscription toobe used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="4e05a-129">Si vous ne connaissez pas les noms de hello de liste hello bases de données Azure pour les serveurs MySQL pour votre groupe d’abonnement et de ressources.</span><span class="sxs-lookup"><span data-stu-id="4e05a-129">List hello Azure Databases for MySQL servers for your subscription and resource group if you are unsure of hello names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="4e05a-130">Notez attribut nom hello Bonjour répertoriant, qui sera utilisé toospecify le toowork de serveur MySQL sur.</span><span class="sxs-lookup"><span data-stu-id="4e05a-130">Note hello name attribute in hello listing, which will be used toospecify which MySQL server toowork on.</span></span> <span data-ttu-id="4e05a-131">Si nécessaire, vérifiez les détails de hello pour ce serveur toousing hello attribut tooconfirm nom est correct :</span><span class="sxs-lookup"><span data-stu-id="4e05a-131">If needed, confirm hello details for that server toousing hello name attribute tooconfirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="4e05a-132">Répertorier les règles de pare-feu d’un serveur Azure Database pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4e05a-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="4e05a-133">À l’aide du nom du serveur hello et nom du groupe de ressources de hello, liste hello serveur règles de pare-feu existantes sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="4e05a-133">Using hello server name and hello resource group name, list hello existing server firewall rules on hello server.</span></span> <span data-ttu-id="4e05a-134">Notez cet attribut de nom de serveur hello est spécifié dans hello **--serveur** basculer et pas hello **--nom** basculer.</span><span class="sxs-lookup"><span data-stu-id="4e05a-134">Notice that hello server name attribute is specified in hello **--server** switch and not hello **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="4e05a-135">sortie de Hello répertorie les règles hello si elle existe, par défaut au format JSON de format.</span><span class="sxs-lookup"><span data-stu-id="4e05a-135">hello output will list hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="4e05a-136">Vous pouvez utiliser le commutateur de hello **--table de sortie** pour un format plus lisible de la table en tant que sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="4e05a-136">You may use hello switch **--output table** for a more readable table format as hello output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="4e05a-137">Création d’une règle de pare-feu d’un serveur Azure Database pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4e05a-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="4e05a-138">Nom du serveur MySQL de Azure hello et nom de groupe de ressources hello, créez une règle de pare-feu sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="4e05a-138">Using hello Azure MySQL server name and hello resource group name, create a new firewall rule on hello server.</span></span> <span data-ttu-id="4e05a-139">Fournissez un nom pour la règle hello, adresse IP de début hello et IP de fin pour hello règle toocover un accès de tooallow adresses plage IP.</span><span class="sxs-lookup"><span data-stu-id="4e05a-139">Provide a name for hello rule, hello start IP, and end IP for hello rule toocover a range of IP addresses tooallow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="4e05a-140">Pour une adresse IP au singulier d’adresses toobe autorisé à accéder, fournissez hello la même adresse que hello IP de début et l’adresse IP de fin, comme dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="4e05a-140">For a singular IP address toobe allowed access, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="4e05a-141">En cas de réussite, sortie de la commande hello répertorie les détails de hello hello de règle de pare-feu que vous avez créé, par défaut au format JSON.</span><span class="sxs-lookup"><span data-stu-id="4e05a-141">Upon success, hello command output will list hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="4e05a-142">En cas de panne, sortie de hello afficher texte du message d’erreur à la place.</span><span class="sxs-lookup"><span data-stu-id="4e05a-142">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="4e05a-143">Mise à jour d’une règle de pare-feu d’un serveur Azure Database pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4e05a-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="4e05a-144">À l’aide du nom du serveur MySQL de Azure hello et le nom de groupe de ressources hello, mettre à jour une règle de pare-feu existante sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="4e05a-144">Using hello Azure MySQL server name and hello resource group name, update an existing firewall rule on hello server.</span></span> <span data-ttu-id="4e05a-145">Fournir le nom hello de règle de pare-feu existante hello comme entrée et tooupdate par démarrer hello IP et de fin attributs IP.</span><span class="sxs-lookup"><span data-stu-id="4e05a-145">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="4e05a-146">En cas de réussite, sortie de la commande hello répertorie les détails de hello hello de règle de pare-feu que vous avez mis à jour, par défaut au format JSON.</span><span class="sxs-lookup"><span data-stu-id="4e05a-146">Upon success, hello command output will list hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="4e05a-147">En cas de panne, sortie de hello afficher texte du message d’erreur à la place.</span><span class="sxs-lookup"><span data-stu-id="4e05a-147">If there is a failure, hello output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="4e05a-148">Si la règle de pare-feu hello n’existe pas, il sera créé par la commande de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="4e05a-148">If hello firewall rule does not exist, it will be created by hello update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="4e05a-149">Affichage des détails d’une règle de pare-feu d’un serveur Azure Database pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4e05a-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="4e05a-150">À l’aide du nom du serveur MySQL de Azure hello et le nom de groupe de ressources hello, afficher les détails de règle de pare-feu existante hello du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="4e05a-150">Using hello Azure MySQL server name and hello resource group name, show hello existing firewall rule details from hello server.</span></span> <span data-ttu-id="4e05a-151">Fournissez le nom hello de règle de pare-feu existante hello comme entrée.</span><span class="sxs-lookup"><span data-stu-id="4e05a-151">Provide hello name of hello existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="4e05a-152">En cas de réussite, sortie de la commande hello répertorie les détails de hello hello de règle de pare-feu que vous avez spécifié, par défaut au format JSON.</span><span class="sxs-lookup"><span data-stu-id="4e05a-152">Upon success, hello command output will list hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="4e05a-153">En cas de panne, sortie de hello afficher texte du message d’erreur à la place.</span><span class="sxs-lookup"><span data-stu-id="4e05a-153">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="4e05a-154">Suppression d’une règle de pare-feu d’un serveur Azure Database pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4e05a-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="4e05a-155">À l’aide du nom du serveur MySQL de Azure hello et le nom de groupe de ressources hello, supprimez une règle de pare-feu existante du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="4e05a-155">Using hello Azure MySQL server name and hello resource group name, remove an existing firewall rule from hello server.</span></span> <span data-ttu-id="4e05a-156">Fournir le nom hello hello existant de règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="4e05a-156">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="4e05a-157">En cas de réussite, aucun résultat ne s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4e05a-157">Upon success, there is no output.</span></span> <span data-ttu-id="4e05a-158">En cas d’échec, le texte de message d’erreur hello est retourné.</span><span class="sxs-lookup"><span data-stu-id="4e05a-158">Upon failure, hello error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e05a-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e05a-159">Next steps</span></span>
- <span data-ttu-id="4e05a-160">En savoir plus sur les [règles de pare-feu du serveur Azure Database pour MySQL](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="4e05a-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="4e05a-161">Créer et gérer la base de données Azure MySQL aux règles de pare-feu à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4e05a-161">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
