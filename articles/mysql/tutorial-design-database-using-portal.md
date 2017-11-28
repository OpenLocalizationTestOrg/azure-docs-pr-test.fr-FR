---
title: "Concevoir votre première base de données Azure pour MySQL - Portail Azure | Microsoft Docs"
description: "Ce didacticiel explique comment créer et gérer un serveur de base de données Azure pour MySQL à l’aide du portail Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: c7b76cacbdc4e483353f64cc4e50c974867bb5b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="8145f-103">Concevoir votre première base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="8145f-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="8145f-104">Base de données Azure pour MySQL est un service géré qui vous permet d’exécuter, de gérer et de mettre à l’échelle des bases de données MySQL hautement disponibles dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="8145f-104">Azure Database for MySQL is a managed service that enables you to run, manage, and scale highly available MySQL databases in the cloud.</span></span> <span data-ttu-id="8145f-105">À l’aide du portail Azure, vous pouvez facilement gérer votre serveur et concevoir une base de données.</span><span class="sxs-lookup"><span data-stu-id="8145f-105">Using the Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="8145f-106">Ce didacticiel vous montre comment utiliser le portail Azure pour :</span><span class="sxs-lookup"><span data-stu-id="8145f-106">In this tutorial, you use the Azure portal to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8145f-107">Créer une base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="8145f-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="8145f-108">Configurer le pare-feu du serveur</span><span class="sxs-lookup"><span data-stu-id="8145f-108">Configure the server firewall</span></span>
> * <span data-ttu-id="8145f-109">Utiliser l’outil en ligne de commande mysql pour créer une base de données</span><span class="sxs-lookup"><span data-stu-id="8145f-109">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="8145f-110">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="8145f-110">Load sample data</span></span>
> * <span data-ttu-id="8145f-111">Données de requête</span><span class="sxs-lookup"><span data-stu-id="8145f-111">Query data</span></span>
> * <span data-ttu-id="8145f-112">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="8145f-112">Update data</span></span>
> * <span data-ttu-id="8145f-113">Restaurer des données</span><span class="sxs-lookup"><span data-stu-id="8145f-113">Restore data</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="8145f-114">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8145f-114">Sign in to the Azure portal</span></span>
<span data-ttu-id="8145f-115">Ouvrez votre navigateur web préféré et rendez-vous sur le [portail Microsoft Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8145f-115">Open your favorite web browser, and visit the [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="8145f-116">Entrez vos informations d’identification pour vous connecter au portail.</span><span class="sxs-lookup"><span data-stu-id="8145f-116">Enter your credentials to sign in to the portal.</span></span> <span data-ttu-id="8145f-117">Il s’ouvre par défaut sur le tableau de bord des services.</span><span class="sxs-lookup"><span data-stu-id="8145f-117">The default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="8145f-118">Créer un serveur de base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="8145f-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="8145f-119">Un serveur de base de données Azure pour MySQL est créé avec un ensemble défini de [ressources de calcul et de stockage](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="8145f-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="8145f-120">Ce serveur est créé dans un [groupe de ressources Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="8145f-120">The server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="8145f-121">Accédez à **Bases de données** > **Base de données Azure pour MySQL**.</span><span class="sxs-lookup"><span data-stu-id="8145f-121">Navigate to **Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="8145f-122">Si vous ne trouvez pas MySQL Server sous **Bases de données**, cliquez sur **Tout afficher** pour afficher tous les services de base de données disponibles.</span><span class="sxs-lookup"><span data-stu-id="8145f-122">If you cannot find MySQL Server under **Databases** category, click **See all** to show all available database services.</span></span> <span data-ttu-id="8145f-123">Vous pouvez également taper **Base de données Azure pour MySQL** dans la zone de recherche pour localiser rapidement le service.</span><span class="sxs-lookup"><span data-stu-id="8145f-123">You can also type **Azure Database for MySQL** in the search box to quickly find the service.</span></span>
<span data-ttu-id="8145f-124">![2-1 Accéder à MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="8145f-124">![2-1 Navigate to MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="8145f-125">Cliquez sur la vignette **Base de données Azure pour MySQL**, puis sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8145f-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="8145f-126">Dans notre exemple, vous renseignez le formulaire de base de données Azure pour MySQL avec les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8145f-126">In our example, fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="8145f-127">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="8145f-127">**Setting**</span></span> | <span data-ttu-id="8145f-128">**Valeur suggérée**</span><span class="sxs-lookup"><span data-stu-id="8145f-128">**Suggested value**</span></span> | <span data-ttu-id="8145f-129">**Description du champ**</span><span class="sxs-lookup"><span data-stu-id="8145f-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="8145f-130">*Nom du serveur*</span><span class="sxs-lookup"><span data-stu-id="8145f-130">*Server name*</span></span> | <span data-ttu-id="8145f-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="8145f-131">myserver4demo</span></span>  | <span data-ttu-id="8145f-132">Le nom du serveur doit être unique au niveau global.</span><span class="sxs-lookup"><span data-stu-id="8145f-132">Server name has to be globally unique.</span></span> |
| <span data-ttu-id="8145f-133">*Abonnement*</span><span class="sxs-lookup"><span data-stu-id="8145f-133">*Subscription*</span></span> | <span data-ttu-id="8145f-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="8145f-134">mysubscription</span></span> | <span data-ttu-id="8145f-135">Sélectionnez votre abonnement dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="8145f-135">Select your subscription from the drop-down.</span></span> |
| <span data-ttu-id="8145f-136">*Groupe de ressources*</span><span class="sxs-lookup"><span data-stu-id="8145f-136">*Resource group*</span></span> | <span data-ttu-id="8145f-137">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8145f-137">myresourcegroup</span></span> | <span data-ttu-id="8145f-138">Créez un groupe de ressources ou utilisez un groupe existant.</span><span class="sxs-lookup"><span data-stu-id="8145f-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="8145f-139">*Connexion d’administrateur du serveur*</span><span class="sxs-lookup"><span data-stu-id="8145f-139">*Server admin login*</span></span> | <span data-ttu-id="8145f-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="8145f-140">myadmin</span></span> | <span data-ttu-id="8145f-141">Configurez le nom du compte Administrateur.</span><span class="sxs-lookup"><span data-stu-id="8145f-141">Setup admin account name.</span></span> |
| <span data-ttu-id="8145f-142">*Mot de passe*</span><span class="sxs-lookup"><span data-stu-id="8145f-142">*Password*</span></span> |  | <span data-ttu-id="8145f-143">Définissez un mot de passe complexe pour le compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8145f-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="8145f-144">*Confirmer le mot de passe*</span><span class="sxs-lookup"><span data-stu-id="8145f-144">*Confirm password*</span></span> |  | <span data-ttu-id="8145f-145">Confirmez le mot de passe du compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8145f-145">Confirm the admin account password.</span></span> |
| <span data-ttu-id="8145f-146">*Emplacement*</span><span class="sxs-lookup"><span data-stu-id="8145f-146">*Location*</span></span> |  | <span data-ttu-id="8145f-147">Sélectionnez une région disponible.</span><span class="sxs-lookup"><span data-stu-id="8145f-147">Select an available region.</span></span> |
| <span data-ttu-id="8145f-148">*Version*</span><span class="sxs-lookup"><span data-stu-id="8145f-148">*Version*</span></span> | <span data-ttu-id="8145f-149">5.7</span><span class="sxs-lookup"><span data-stu-id="8145f-149">5.7</span></span> | <span data-ttu-id="8145f-150">Choisissez la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="8145f-150">Choose the latest version.</span></span> |
| <span data-ttu-id="8145f-151">*Configurer les performances*</span><span class="sxs-lookup"><span data-stu-id="8145f-151">*Configure performance*</span></span> | <span data-ttu-id="8145f-152">De base, 50 unités de calcul, 50 Go</span><span class="sxs-lookup"><span data-stu-id="8145f-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="8145f-153">Choisissez le **niveau de performance**, les **unités de calcul** et le **stockage**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8145f-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="8145f-154">*Épingler au tableau de bord*</span><span class="sxs-lookup"><span data-stu-id="8145f-154">*Pin to Dashboard*</span></span> | <span data-ttu-id="8145f-155">Vérification</span><span class="sxs-lookup"><span data-stu-id="8145f-155">Check</span></span> | <span data-ttu-id="8145f-156">Il est recommandé de cocher cette case pour trouver facilement le serveur plus tard.</span><span class="sxs-lookup"><span data-stu-id="8145f-156">Recommended to check this box so you may find the server easily later on</span></span> |
<span data-ttu-id="8145f-157">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8145f-157">Then, click **Create**.</span></span> <span data-ttu-id="8145f-158">En une minute ou deux, un nouveau serveur de base de données Azure pour MySQL s’exécute dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="8145f-158">In a minute or two, a new Azure Database for MySQL server is running in the cloud.</span></span> <span data-ttu-id="8145f-159">Dans la barre d’outils, cliquez sur le bouton **Notifications** pour surveiller le processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="8145f-159">You can click **Notifications** button on the toolbar to monitor the deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="8145f-160">Configurer le pare-feu</span><span class="sxs-lookup"><span data-stu-id="8145f-160">Configure firewall</span></span>
<span data-ttu-id="8145f-161">Les bases de données Azure pour MySQL sont protégées par un pare-feu.</span><span class="sxs-lookup"><span data-stu-id="8145f-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="8145f-162">Par défaut, toutes les connexions au serveur et aux bases de données du serveur sont rejetées.</span><span class="sxs-lookup"><span data-stu-id="8145f-162">By default, all connections to the server and the databases inside the server are rejected.</span></span> <span data-ttu-id="8145f-163">Avant de vous connecter pour la première fois à la base de données Azure pour MySQL, configurez le pare-feu pour ajouter l’adresse IP du réseau public de l’ordinateur client (ou une plage d’adresses IP).</span><span class="sxs-lookup"><span data-stu-id="8145f-163">Before connecting to Azure Database for MySQL for the first time, configure the firewall to add the client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="8145f-164">Cliquez sur le serveur qui vient d’être créé, puis sur **Sécurité de la connexion**.</span><span class="sxs-lookup"><span data-stu-id="8145f-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="8145f-165">![3-1 Sécurité de la connexion](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="8145f-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="8145f-166">Vous pouvez choisir **Ajouter mon adresse IP** ou configurer les règles de pare-feu ici.</span><span class="sxs-lookup"><span data-stu-id="8145f-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="8145f-167">N’oubliez pas de cliquer sur **Enregistrer** après avoir créé les règles.</span><span class="sxs-lookup"><span data-stu-id="8145f-167">Remember to click **Save** after you have created the rules.</span></span>
<span data-ttu-id="8145f-168">Vous pouvez maintenant vous connecter au serveur en utilisant l’outil en ligne de commande mysql ou l’interface graphique utilisateur MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="8145f-168">You can now connect to the server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="8145f-169">Le serveur de base de données Azure pour MySQL communique sur le port 3306.</span><span class="sxs-lookup"><span data-stu-id="8145f-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="8145f-170">Si vous essayez de vous connecter à partir d’un réseau d’entreprise, le trafic sortant sur le port 3306 peut ne pas être autorisé par le pare-feu de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="8145f-170">If you are trying to connect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="8145f-171">Dans ce cas, vous ne pouvez pas vous connecter à votre serveur Azure MySQL, sauf si votre service informatique ouvre le port 3306.</span><span class="sxs-lookup"><span data-stu-id="8145f-171">If so, you cannot connect to Azure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="8145f-172">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="8145f-172">Get connection information</span></span>
<span data-ttu-id="8145f-173">Obtenez le **nom du serveur** et le **nom de connexion d’administrateur du serveur** complets pour votre serveur de base de données Azure pour MySQL à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8145f-173">Get the fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from the Azure portal.</span></span> <span data-ttu-id="8145f-174">Vous utilisez le nom de serveur complet pour vous connecter à votre serveur avec l’outil en ligne de commande mysql.</span><span class="sxs-lookup"><span data-stu-id="8145f-174">You use the fully qualified server name to connect to your server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="8145f-175">Dans le [portail Azure](https://portal.azure.com/), cliquez sur **Toutes les ressources** dans le menu de gauche, tapez le nom et recherchez votre serveur de base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="8145f-175">In [Azure portal](https://portal.azure.com/), click **All resources** from the left-hand menu, type the name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="8145f-176">Sélectionnez le nom du serveur pour afficher les détails.</span><span class="sxs-lookup"><span data-stu-id="8145f-176">Select the server name to view the details.</span></span>

2. <span data-ttu-id="8145f-177">Sous le titre Paramètres, cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="8145f-177">Under the Settings heading, click **Properties**.</span></span> <span data-ttu-id="8145f-178">Notez les valeurs de **NOM DU SERVEUR** et de **NOM DE CONNEXION D’ADMINISTRATEUR DU SERVEUR**.</span><span class="sxs-lookup"><span data-stu-id="8145f-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="8145f-179">Vous pouvez cliquer sur le bouton de copie en regard de chaque champ pour les copier dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="8145f-179">You may click the copy button next to each field to copy to the clipboard.</span></span>
   <span data-ttu-id="8145f-180">![4-2 Propriétés de serveur](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="8145f-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="8145f-181">Dans cet exemple, le nom du serveur est *myserver4demo.mysql.database.azure.com*, et la connexion d’administrateur du serveur est *myadmin@myserver4demo*.</span><span class="sxs-lookup"><span data-stu-id="8145f-181">In this example, the server name is *myserver4demo.mysql.database.azure.com*, and the server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="8145f-182">Se connecter au serveur à l’aide de mysql</span><span class="sxs-lookup"><span data-stu-id="8145f-182">Connect to the server using mysql</span></span>
<span data-ttu-id="8145f-183">Utilisez [l’outil de ligne de commande mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) pour établir une connexion à votre serveur de base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="8145f-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="8145f-184">Vous pouvez exécuter l’outil en ligne de commande mysql depuis Azure Cloud Shell dans le navigateur ou depuis votre propre ordinateur à l’aide des outils mysql installés localement.</span><span class="sxs-lookup"><span data-stu-id="8145f-184">You can run the mysql command-line tool from the Azure Cloud Shell in the browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="8145f-185">Pour lancer Azure Cloud Shell, cliquez sur le bouton `Try It` dans un bloc de code de cet article, ou visitez le portail Azure et cliquez sur l’icône `>_` dans la barre d’outils en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="8145f-185">To launch the Azure Cloud Shell, click the `Try It` button on a code block in this article, or visit the Azure portal and click the `>_` icon in the top right toolbar.</span></span> 

<span data-ttu-id="8145f-186">Saisissez cette commande pour vous connecter :</span><span class="sxs-lookup"><span data-stu-id="8145f-186">Type the command to connect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="8145f-187">Créer une base de données vide</span><span class="sxs-lookup"><span data-stu-id="8145f-187">Create a blank database</span></span>
<span data-ttu-id="8145f-188">Une fois que vous êtes connecté au serveur, créez une base de données vide sur laquelle travailler.</span><span class="sxs-lookup"><span data-stu-id="8145f-188">Once you’re connected to the server, create a blank database to work with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="8145f-189">À l’invite, exécutez la commande suivante pour basculer la connexion sur la base de données nouvellement créée :</span><span class="sxs-lookup"><span data-stu-id="8145f-189">At the prompt, run the following command to switch connection to this newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="8145f-190">Créer des tables dans la base de données</span><span class="sxs-lookup"><span data-stu-id="8145f-190">Create tables in the database</span></span>
<span data-ttu-id="8145f-191">Maintenant que vous savez comment vous connecter à la base de données Azure pour MySQL, nous pouvons aborder certaines tâches de base.</span><span class="sxs-lookup"><span data-stu-id="8145f-191">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="8145f-192">Tout d’abord, nous pouvons créer une table et y charger des données.</span><span class="sxs-lookup"><span data-stu-id="8145f-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="8145f-193">Nous allons créer une table qui stocke des données d’inventaire.</span><span class="sxs-lookup"><span data-stu-id="8145f-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="8145f-194">Charger des données dans les tables</span><span class="sxs-lookup"><span data-stu-id="8145f-194">Load data into the tables</span></span>
<span data-ttu-id="8145f-195">Maintenant que nous disposons d’une table, nous pouvons y insérer des données.</span><span class="sxs-lookup"><span data-stu-id="8145f-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="8145f-196">Dans la fenêtre d’invite de commandes ouverte, exécutez la requête suivante pour insérer des lignes de données.</span><span class="sxs-lookup"><span data-stu-id="8145f-196">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="8145f-197">Vous avez maintenant chargé deux lignes de données dans la table que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="8145f-197">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="8145f-198">Interroger et mettre à jour les données des tables</span><span class="sxs-lookup"><span data-stu-id="8145f-198">Query and update the data in the tables</span></span>
<span data-ttu-id="8145f-199">Exécutez la requête suivante pour récupérer des informations à partir de la table de base de données.</span><span class="sxs-lookup"><span data-stu-id="8145f-199">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="8145f-200">Vous pouvez également mettre à jour les données des tables.</span><span class="sxs-lookup"><span data-stu-id="8145f-200">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="8145f-201">La ligne est mise à jour en conséquence lorsque vous récupérez les données.</span><span class="sxs-lookup"><span data-stu-id="8145f-201">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="8145f-202">Restaurer une version antérieure d’une base de données</span><span class="sxs-lookup"><span data-stu-id="8145f-202">Restore a database to a previous point in time</span></span>
<span data-ttu-id="8145f-203">Imaginez que vous avez accidentellement supprimé une table de base de données importante et que vous ne pouvez pas récupérer les données facilement.</span><span class="sxs-lookup"><span data-stu-id="8145f-203">Imagine you have accidentally deleted an important database table, and cannot recover the data easily.</span></span> <span data-ttu-id="8145f-204">La base de données Azure pour MySQL vous permet de restaurer le serveur à un point dans le temps, créant une copie des bases de données dans le nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="8145f-204">Azure Database for MySQL allows you to restore the server to a point in time, creating a copy of the databases into new server.</span></span> <span data-ttu-id="8145f-205">Vous pouvez alors utiliser ce nouveau serveur pour récupérer les données supprimées.</span><span class="sxs-lookup"><span data-stu-id="8145f-205">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="8145f-206">Les étapes suivantes restaurent le serveur à l’état dans lequel il était avant l’ajout de la table.</span><span class="sxs-lookup"><span data-stu-id="8145f-206">The following steps restore the sample server to a point before the table was added.</span></span>

1. <span data-ttu-id="8145f-207">Dans le portail Azure, recherchez votre base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="8145f-207">In the Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="8145f-208">Sur la page **Vue d’ensemble**, cliquez sur **Restaurer** dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="8145f-208">On the **Overview** page, click **Restore** on the toolbar.</span></span> <span data-ttu-id="8145f-209">La page Restaurer s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="8145f-209">The Restore page opens.</span></span>

   ![10-1 Restaurer une base de données](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="8145f-211">Remplissez le formulaire **Restaurer** avec les informations requises.</span><span class="sxs-lookup"><span data-stu-id="8145f-211">Fill out the **Restore** form with the required information.</span></span>
   
   ![10-2 Formulaire de restauration](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="8145f-213">**Point de restauration** : sélectionnez un point dans le temps vers lequel vous souhaitez effectuer une restauration, pendant la période répertoriée.</span><span class="sxs-lookup"><span data-stu-id="8145f-213">**Restore point**: Select a point-in-time that you want to restore to, within the timeframe listed.</span></span> <span data-ttu-id="8145f-214">Veillez à convertir votre fuseau horaire local vers le fuseau horaire UTC.</span><span class="sxs-lookup"><span data-stu-id="8145f-214">Make sure to convert your local timezone to UTC.</span></span>
   - <span data-ttu-id="8145f-215">**Restaurer sur un nouveau serveur** : spécifiez un nouveau nom de serveur sur lequel vous souhaitez effectuer la restauration.</span><span class="sxs-lookup"><span data-stu-id="8145f-215">**Restore to new server**: Provide a new server name you want to restore to.</span></span>
   - <span data-ttu-id="8145f-216">**Emplacement** : la région est identique à celle du serveur source et ne peut pas être modifiée.</span><span class="sxs-lookup"><span data-stu-id="8145f-216">**Location**: The region is same as the source server, and cannot be changed.</span></span>
   - <span data-ttu-id="8145f-217">**Niveau tarifaire** : le niveau tarifaire est identique à celui du serveur source et ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="8145f-217">**Pricing tier**: The pricing tier is the same as the source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="8145f-218">Cliquez sur **OK** pour restaurer le serveur [à un point dans le temps](./howto-restore-server-portal.md) avant la suppression de la table.</span><span class="sxs-lookup"><span data-stu-id="8145f-218">Click **OK** to restore the server to [restore to a point in time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="8145f-219">La restauration d’un serveur crée une copie du serveur à partir du point dans le temps que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="8145f-219">Restoring a server creates a new copy of the server, as of the point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8145f-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8145f-220">Next steps</span></span>
<span data-ttu-id="8145f-221">Ce didacticiel vous montre comment utiliser le portail Azure pour :</span><span class="sxs-lookup"><span data-stu-id="8145f-221">In this tutorial, you use the Azure portal to learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8145f-222">Créer une base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="8145f-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="8145f-223">Configurer le pare-feu du serveur</span><span class="sxs-lookup"><span data-stu-id="8145f-223">Configure the server firewall</span></span>
> * <span data-ttu-id="8145f-224">Utiliser l’outil en ligne de commande mysql pour créer une base de données</span><span class="sxs-lookup"><span data-stu-id="8145f-224">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="8145f-225">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="8145f-225">Load sample data</span></span>
> * <span data-ttu-id="8145f-226">Données de requête</span><span class="sxs-lookup"><span data-stu-id="8145f-226">Query data</span></span>
> * <span data-ttu-id="8145f-227">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="8145f-227">Update data</span></span>
> * <span data-ttu-id="8145f-228">Restaurer des données</span><span class="sxs-lookup"><span data-stu-id="8145f-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8145f-229">Connexion d’applications à la base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="8145f-229">How to connect applications to Azure Database for MySQL</span></span>](./howto-connection-string.md)
