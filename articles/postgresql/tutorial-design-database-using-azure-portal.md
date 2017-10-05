---
title: "Concevoir votre première base de données Azure pour PostgreSQL avec le portail Azure | Microsoft Docs"
description: "Ce didacticiel montre comment concevoir votre première base de données Azure pour PostgreSQL à l’aide du portail Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: tutorial, mvc
ms.topic: tutorial
ms.date: 05/10/2017
ms.openlocfilehash: 2aa9d10749b54537495ad3e09566c43718f67a9e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-the-azure-portal"></a><span data-ttu-id="2c2ff-103">Concevoir votre première base de données Azure pour PostgreSQL avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="2c2ff-103">Design your first Azure Database for PostgreSQL using the Azure portal</span></span>

<span data-ttu-id="2c2ff-104">Base de données Azure pour PostgreSQL est un service géré qui vous permet d’exécuter, de gérer et de mettre à l’échelle des bases de données PostgreSQL hautement disponibles dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-104">Azure Database for PostgreSQL is a managed service that enables you to run, manage, and scale highly available PostgreSQL databases in the cloud.</span></span> <span data-ttu-id="2c2ff-105">À l’aide du portail Azure, vous pouvez facilement gérer votre serveur et concevoir une base de données.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-105">Using the Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="2c2ff-106">Ce didacticiel vous montre comment utiliser le portail Azure pour :</span><span class="sxs-lookup"><span data-stu-id="2c2ff-106">In this tutorial, you use the Azure portal to learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="2c2ff-107">Créer une base de données Azure pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="2c2ff-107">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="2c2ff-108">Configurer le pare-feu du serveur</span><span class="sxs-lookup"><span data-stu-id="2c2ff-108">Configure the server firewall</span></span>
> * <span data-ttu-id="2c2ff-109">Utiliser l’utilitaire [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) pour créer une base de données</span><span class="sxs-lookup"><span data-stu-id="2c2ff-109">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="2c2ff-110">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="2c2ff-110">Load sample data</span></span>
> * <span data-ttu-id="2c2ff-111">Données de requête</span><span class="sxs-lookup"><span data-stu-id="2c2ff-111">Query data</span></span>
> * <span data-ttu-id="2c2ff-112">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="2c2ff-112">Update data</span></span>
> * <span data-ttu-id="2c2ff-113">Restaurer des données</span><span class="sxs-lookup"><span data-stu-id="2c2ff-113">Restore data</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c2ff-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2c2ff-114">Prerequisites</span></span>
<span data-ttu-id="2c2ff-115">Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-115">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="2c2ff-116">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-116">Log in to the Azure portal</span></span>
<span data-ttu-id="2c2ff-117">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2c2ff-117">Log in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-postgresql"></a><span data-ttu-id="2c2ff-118">Créer une base de données Azure pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="2c2ff-118">Create an Azure Database for PostgreSQL</span></span>

<span data-ttu-id="2c2ff-119">Un serveur de base de données Azure pour PostgreSQL est créé. Il contient un ensemble défini de [ressources de calcul et de stockage](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="2c2ff-119">An Azure Database for PostgreSQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="2c2ff-120">Ce serveur est créé dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2c2ff-120">The server is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="2c2ff-121">Pour créer un serveur de base de données Azure pour PostgreSQL, suivez les étapes ci-après :</span><span class="sxs-lookup"><span data-stu-id="2c2ff-121">Follow these steps to create an Azure Database for PostgreSQL server:</span></span>
1.  <span data-ttu-id="2c2ff-122">Cliquez sur le bouton **+ Nouveau** dans l’angle supérieur gauche du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-122">Click the **+ New**  button found on the upper left-hand corner of the Azure portal.</span></span>
2.  <span data-ttu-id="2c2ff-123">Sélectionnez **Bases de données** dans la page **Nouveau**, puis **Base de données Azure pour PostgreSQL** dans la page **Bases de données**.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-123">Select **Databases** from the **New** page, and select **Azure Database for PostgreSQL** from the **Databases** page.</span></span>
 <span data-ttu-id="2c2ff-124">![Base de données Azure pour PostgreSQL - Créer la base de données](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span><span class="sxs-lookup"><span data-stu-id="2c2ff-124">![Azure Database for PostgreSQL - Create the database](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span></span>

3.  <span data-ttu-id="2c2ff-125">Renseignez le formulaire du nouveau serveur avec les informations suivantes, comme indiqué dans l’illustration précédente :</span><span class="sxs-lookup"><span data-stu-id="2c2ff-125">Fill out the new server details form with the following information, as shown on the preceding image:</span></span>
    - <span data-ttu-id="2c2ff-126">Nom du serveur : **mypgserver-20170401** (le nom du serveur correspond au nom DNS et doit ainsi être globalement unique).</span><span class="sxs-lookup"><span data-stu-id="2c2ff-126">Server name: **mypgserver-20170401** (name of a server maps to DNS name and is thus required to be globally unique)</span></span> 
    - <span data-ttu-id="2c2ff-127">Abonnement : si vous avez plusieurs abonnements, sélectionnez l’abonnement approprié dans lequel la ressource existe ou est facturée.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-127">Subscription: If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span>
    - <span data-ttu-id="2c2ff-128">Groupe de ressources : **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-128">Resource group: **myresourcegroup**</span></span>
    - <span data-ttu-id="2c2ff-129">Connexion d’administrateur du serveur et mot de passe de votre choix.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-129">Server admin login and password of your choice</span></span>
    - <span data-ttu-id="2c2ff-130">Lieu</span><span class="sxs-lookup"><span data-stu-id="2c2ff-130">Location</span></span>
    - <span data-ttu-id="2c2ff-131">Version de PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-131">PostgreSQL Version</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="2c2ff-132">La connexion d’administrateur serveur et le mot de passe que vous spécifiez ici seront requis plus loin dans ce guide de démarrage rapide pour la connexion au serveur et à ses bases de données.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-132">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="2c2ff-133">Retenez ou enregistrez ces informations pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-133">Remember or record this information for later use.</span></span>

4.  <span data-ttu-id="2c2ff-134">Cliquez sur **Niveau tarifaire** pour spécifier le niveau de service et le niveau de performances pour votre nouvelle base de données.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-134">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="2c2ff-135">Pour ce guide de démarrage rapide, choisissez le niveau **De base**, **50 unités de calcul** et **50 Go** de stockage inclus.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-135">For this quick start, select **Basic** Tier, **50 Compute Units** and **50 GB** of included storage.</span></span>
 <span data-ttu-id="2c2ff-136">![Base de données Azure pour PostgreSQL - Choisir le niveau de service](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span><span class="sxs-lookup"><span data-stu-id="2c2ff-136">![Azure Database for PostgreSQL - pick the service tier](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span></span>
5.  <span data-ttu-id="2c2ff-137">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-137">Click **Ok**.</span></span>
6.  <span data-ttu-id="2c2ff-138">Cliquez sur **Créer** pour approvisionner le serveur.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-138">Click **Create** to provision the server.</span></span> <span data-ttu-id="2c2ff-139">L’approvisionnement prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-139">Provisioning takes a few minutes.</span></span>

  > [!TIP]
  > <span data-ttu-id="2c2ff-140">Cochez l’option **Épingler au tableau de bord** pour faciliter le suivi de vos déploiements.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-140">Check the **Pin to dashboard** option to allow easy tracking of your deployments.</span></span>

7.  <span data-ttu-id="2c2ff-141">Dans la barre d’outils, cliquez sur **Notifications** pour surveiller le processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-141">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>
 <span data-ttu-id="2c2ff-142">![Base de données Azure pour PostgreSQL - Consulter les notifications](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span><span class="sxs-lookup"><span data-stu-id="2c2ff-142">![Azure Database for PostgreSQL - See notifications](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span></span>
   
  <span data-ttu-id="2c2ff-143">Par défaut, la création de la base de données **postgres** intervient sous votre serveur.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-143">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="2c2ff-144">La base de données [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) est une base de données par défaut destinée aux utilisateurs, utilitaires et applications tierces.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-144">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 

## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="2c2ff-145">Configurer une règle de pare-feu au niveau du serveur</span><span class="sxs-lookup"><span data-stu-id="2c2ff-145">Configure a server-level firewall rule</span></span>

<span data-ttu-id="2c2ff-146">Le service Base de données Azure pour PostgreSQL crée un pare-feu au niveau du serveur.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-146">The Azure Database for PostgreSQL service creates a firewall at the server-level.</span></span> <span data-ttu-id="2c2ff-147">Le pare-feu empêche les applications et les outils externes de se connecter au serveur et à toute base de données sur le serveur, sauf si une règle de pare-feu est créée pour ouvrir le pare-feu à des adresses IP spécifiques.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-147">This firewall prevents external applications and tools from connecting to the server and any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> 

1.  <span data-ttu-id="2c2ff-148">Une fois le déploiement terminé, cliquez sur **Toutes les ressources** dans le menu de gauche et saisissez le nom **mypgserver-20170401** pour rechercher le serveur qui vient d’être créé.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-148">After the deployment completes, click **All Resources** from the left-hand menu and type in the name **mypgserver-20170401** to search for your newly created server.</span></span> <span data-ttu-id="2c2ff-149">Cliquez sur le nom du serveur figurant dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-149">Click the server name listed in the search result.</span></span> <span data-ttu-id="2c2ff-150">La page **Présentation** correspondant à votre serveur s’ouvre et propose des options pour poursuivre la configuration de la page.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-150">The **Overview** page for your server opens and provides options for further configuration.</span></span>
 
 ![<span data-ttu-id="2c2ff-151">Base de données Azure pour PostgreSQL - Rechercher le serveur</span><span class="sxs-lookup"><span data-stu-id="2c2ff-151">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

2.  <span data-ttu-id="2c2ff-152">Dans le panneau du serveur, sélectionnez **Sécurité de la connexion**.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-152">In the server blade, select **Connection Security**.</span></span> 
3.  <span data-ttu-id="2c2ff-153">Cliquez dans la zone de texte sous **Nom de la règle**, puis ajoutez une nouvelle règle de pare-feu pour placer la plage IP pour la connectivité en liste verte.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-153">Click in the text box under **Rule Name,** and add a new firewall rule to whitelist the IP range for connectivity.</span></span> <span data-ttu-id="2c2ff-154">Pour ce didacticiel, nous allons autoriser toutes les adresses IP. Pour cela, tapez **Nom de la règle = AllowAllIps** ,  **= 0.0.0.0** et **= 255.255.255.255** , puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-154">For this tutorial, let's allow all IPs by typing in **Rule Name = AllowAllIps**, **Start IP = 0.0.0.0** and **End IP = 255.255.255.255** and then click **Save**.</span></span> <span data-ttu-id="2c2ff-155">Vous pouvez définir une règle de pare-feu qui couvre une plage IP afin de vous connecter à partir de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-155">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span>
 
 ![Base de données Azure pour PostgreSQL - Créer une règle de pare-feu](./media/tutorial-design-database-using-azure-portal/5-firewall-2.png)

4.  <span data-ttu-id="2c2ff-157">Cliquez sur **Enregistrer**, puis sur **X** pour fermer la page **Sécurité de la connexion**.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-157">Click **Save** and then click the **X** to close the **Connections Security** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="2c2ff-158">Le serveur Azure PostgreSQL communique sur le port 5432.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-158">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="2c2ff-159">Si vous essayez de vous connecter à partir d’un réseau d’entreprise, le trafic sortant sur le port 5432 peut être bloqué par le pare-feu de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-159">If you are trying to connect from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="2c2ff-160">Dans ce cas, vous ne pouvez pas vous connecter à votre serveur Azure SQL Database, sauf si votre service informatique ouvre le port 5432.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-160">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 5432.</span></span>
  >


## <a name="get-the-connection-information"></a><span data-ttu-id="2c2ff-161">Obtenir les informations de connexion</span><span class="sxs-lookup"><span data-stu-id="2c2ff-161">Get the connection information</span></span>

<span data-ttu-id="2c2ff-162">Lorsque nous avons créé notre serveur de base de données Azure pour PostgreSQL, la base de données **postgres** par défaut a également été créée.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-162">When we created our Azure Database for PostgreSQL server, the default **postgres** database also gets created.</span></span> <span data-ttu-id="2c2ff-163">Pour vous connecter à votre serveur de base de données, vous devez fournir des informations sur l’hôte et des informations d’identification pour l’accès.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-163">To connect to your database server, you need to provide host information and access credentials.</span></span>

1. <span data-ttu-id="2c2ff-164">Dans le menu de gauche du portail Azure, cliquez sur **Toutes les ressources**, puis recherchez le serveur **mypgserver-20170401** que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-164">From the left-hand menu in Azure portal, click **All resources** and search for the server you just created **mypgserver-20170401**.</span></span>

  ![<span data-ttu-id="2c2ff-165">Base de données Azure pour PostgreSQL - Rechercher le serveur</span><span class="sxs-lookup"><span data-stu-id="2c2ff-165">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

3. <span data-ttu-id="2c2ff-166">Cliquez sur le nom du serveur **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-166">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="2c2ff-167">Sélectionnez la page **Présentation** du serveur.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-167">Select the server's **Overview** page.</span></span> <span data-ttu-id="2c2ff-168">Prenez note du **nom du serveur** et du **nom de connexion d’administrateur du serveur**.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-168">Make a note of the **Server name** and **Server admin login name**.</span></span>

 ![Base de données Azure pour PostgreSQL - Connexion d’administrateur du serveur](./media/tutorial-design-database-using-azure-portal/6-server-name.png)


## <a name="connect-to-postgresql-database-using-psql-in-cloud-shell"></a><span data-ttu-id="2c2ff-170">Se connecter à la base de données PostgreSQL à l’aide de psql dans Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="2c2ff-170">Connect to PostgreSQL database using psql in Cloud Shell</span></span>

<span data-ttu-id="2c2ff-171">Nous allons maintenant utiliser l’utilitaire de ligne de commande psql pour nous connecter au serveur de base de données Azure pour PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-171">Let's now use the psql command-line utility to connect to the Azure Database for PostgreSQL server.</span></span> 
1. <span data-ttu-id="2c2ff-172">Exécutez Azure Cloud Shell via l’icône de la console dans le volet de navigation supérieur.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-172">Launch the Azure Cloud Shell via the terminal icon on the top navigation pane.</span></span>

   ![Base de données Azure pour PostgreSQL - Icône de la console Azure Cloud Shell](./media/tutorial-design-database-using-azure-portal/7-cloud-shell.png)

2. <span data-ttu-id="2c2ff-174">Azure Cloud Shell s’ouvre dans votre navigateur, ce qui vous permet de saisir des commande bash.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-174">The Azure Cloud Shell opens in your browser, enabling you to type bash commands.</span></span>

   ![Base de données Azure pour PostgreSQL - Invite bash Azure Shell](./media/tutorial-design-database-using-azure-portal/8-bash.png)

3. <span data-ttu-id="2c2ff-176">À l’invite Cloud Shell, connectez-vous à votre serveur de base de données Azure pour PostgreSQL en utilisant les commandes psql.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-176">At the Cloud Shell prompt, connect to your Azure Database for PostgreSQL server using the psql commands.</span></span> <span data-ttu-id="2c2ff-177">Le format suivant est utilisé pour se connecter à un serveur de base de données Azure pour PostgreSQL avec l’utilitaire [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) :</span><span class="sxs-lookup"><span data-stu-id="2c2ff-177">The following format is used to connect to an Azure Database for PostgreSQL server with the [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility:</span></span>
   ```bash
   psql --host=<myserver> --port=<port> --username=<server admin login> --dbname=<database name>
   ```

   <span data-ttu-id="2c2ff-178">Par exemple, la commande suivante permet de se connecter à la base de données par défaut appelée **postgres** sur votre serveur PostgreSQL **mypgserver-20170401.postgres.database.azure.com** à l’aide des informations d’identification d’accès.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-178">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="2c2ff-179">À l’invite, entrez votre mot de passe d’administrateur du serveur.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-179">Enter your server admin password when prompted.</span></span>

   ```bash
   psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
   ```

## <a name="create-a-new-database"></a><span data-ttu-id="2c2ff-180">Créer une base de données</span><span class="sxs-lookup"><span data-stu-id="2c2ff-180">Create a New Database</span></span>
<span data-ttu-id="2c2ff-181">Une fois que vous êtes connecté au serveur, créez une base de données vide à l’invite.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-181">Once you're connected to the server, create a blank database at the prompt.</span></span>
```bash
CREATE DATABASE mypgsqldb;
```

<span data-ttu-id="2c2ff-182">À l’invite, exécutez la commande suivante pour basculer la connexion sur la base de données nouvellement créée **mypgsqldb**.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-182">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**.</span></span>
```bash
\c mypgsqldb
```
## <a name="create-tables-in-the-database"></a><span data-ttu-id="2c2ff-183">Créer des tables dans la base de données</span><span class="sxs-lookup"><span data-stu-id="2c2ff-183">Create tables in the database</span></span>
<span data-ttu-id="2c2ff-184">Maintenant que vous savez comment vous connecter à la base de données Azure pour PostgreSQL, nous pouvons aborder certaines tâches de base.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-184">Now that you know how to connect to the Azure Database for PostgreSQL, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="2c2ff-185">Tout d’abord, nous pouvons créer une table et la charger avec des données.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-185">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="2c2ff-186">Nous allons créer une table qui assure le suivi des informations d’inventaire.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-186">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="2c2ff-187">Vous pouvez localiser cette nouvelle table dans la liste des tables en tapant :</span><span class="sxs-lookup"><span data-stu-id="2c2ff-187">You can see the newly created table in the list of tabvles now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="2c2ff-188">Charger des données dans les tables</span><span class="sxs-lookup"><span data-stu-id="2c2ff-188">Load data into the tables</span></span>
<span data-ttu-id="2c2ff-189">Maintenant que nous disposons d’une table, nous pouvons y insérer des données.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-189">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="2c2ff-190">Dans la fenêtre d’invite de commandes ouverte, exécutez la requête suivante pour insérer des lignes de données.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-190">At the open command prompt window, run the following query to insert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="2c2ff-191">Vous avez maintenant chargé deux lignes de données dans la table que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-191">You have now two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="2c2ff-192">Interroger et mettre à jour les données des tables</span><span class="sxs-lookup"><span data-stu-id="2c2ff-192">Query and update the data in the tables</span></span>
<span data-ttu-id="2c2ff-193">Exécutez la requête suivante pour récupérer des informations à partir de la table de base de données.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-193">Execute the following query to retrieve information from the database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="2c2ff-194">Vous pouvez également mettre à jour les données des tables.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-194">You can also update the data in the tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="2c2ff-195">La ligne est mise à jour en conséquence lorsque vous récupérez les données.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-195">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-data-to-a-previous-point-in-time"></a><span data-ttu-id="2c2ff-196">Restaurer les données à un point antérieur dans le temps</span><span class="sxs-lookup"><span data-stu-id="2c2ff-196">Restore data to a previous point in time</span></span>
<span data-ttu-id="2c2ff-197">Imaginez que vous avez supprimé cette table par erreur.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-197">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="2c2ff-198">La récupération dans ce cas n’est pas simple.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-198">This situation is something you cannot easily recover from.</span></span> <span data-ttu-id="2c2ff-199">La base de données Azure pour PostgreSQL vous permet de revenir à n’importe quel point dans le temps (dans la limite de 7 jours (De base) et de 35 jours (Standard)), puis d’effectuer une restauration vers un nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-199">Azure Database for PostgreSQL allows you to go back to any point-in-time (in the last up to 7 days (Basic) and 35 days (Standard)) and restore this point-in-time to a new server.</span></span> <span data-ttu-id="2c2ff-200">Vous pouvez alors utiliser ce nouveau serveur pour récupérer les données supprimées.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-200">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="2c2ff-201">Les étapes suivantes restaurent le serveur dans l’état dans lequel il était avant l’ajout de la table.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-201">The following steps restore the sample server to a point before the table was added.</span></span>

1.  <span data-ttu-id="2c2ff-202">Dans la page de la base de données Azure pour PostgreSQL pour votre serveur, cliquez sur **Restaurer** dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-202">On the Azure Database for PostgreSQL page for your server, click **Restore** on the toolbar.</span></span> <span data-ttu-id="2c2ff-203">La page **Restauration** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-203">The **Restore** page opens.</span></span>
  <span data-ttu-id="2c2ff-204">![Portail Azure - Options du formulaire de restauration](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span><span class="sxs-lookup"><span data-stu-id="2c2ff-204">![Azure portal - Restore form options](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span></span>
2.  <span data-ttu-id="2c2ff-205">Remplissez le formulaire **Restaurer** avec les informations requises :</span><span class="sxs-lookup"><span data-stu-id="2c2ff-205">Fill out the **Restore** form with the required information:</span></span>

  ![Portail Azure - Options du formulaire de restauration](./media/tutorial-design-database-using-azure-portal/10-azure-portal-restore.png)
  - <span data-ttu-id="2c2ff-207">**Point de restauration** : sélectionnez un point dans le temps avant la modification du serveur.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-207">**Restore point**: Select a point-in-time that occurs before the server was changed</span></span>
  - <span data-ttu-id="2c2ff-208">**Serveur cible** : fournissez un nouveau nom de serveur sur lequel vous souhaitez effectuer la restauration.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-208">**Target server**: Provide a new server name you want to restore to</span></span>
  - <span data-ttu-id="2c2ff-209">**Emplacement** : vous ne pouvez pas sélectionner la région. Par défaut, elle est identique à celle du serveur source.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-209">**Location**: You cannot select the region, by default it is same as the source server</span></span>
  - <span data-ttu-id="2c2ff-210">**Niveau tarifaire** : vous ne pouvez pas modifier cette valeur lors de la restauration d’un serveur.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-210">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="2c2ff-211">Elle est identique à celle du serveur source.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-211">It is same as the source server.</span></span> 
3.  <span data-ttu-id="2c2ff-212">Cliquez sur **OK** pour restaurer le serveur [à un point dans le temps](./howto-restore-server-portal.md) avant la suppression des tables.</span><span class="sxs-lookup"><span data-stu-id="2c2ff-212">Click **OK** to restore the server to [restore to a point-in-time](./howto-restore-server-portal.md) before the tables was deleted.</span></span> <span data-ttu-id="2c2ff-213">La restauration d’un serveur à un autre point dans le temps crée un serveur en double par rapport au serveur d’origine, à condition qu’il se trouve au sein de la période de rétention de votre [niveau de service](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="2c2ff-213">Restoring a server to a different point in time creates a duplicate new server as the original server as of the point in time you specify, provided that it is within the retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c2ff-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2c2ff-214">Next Steps</span></span>
<span data-ttu-id="2c2ff-215">Ce didacticiel vous montre comment utiliser le portail Azure et d’autres utilitaires pour :</span><span class="sxs-lookup"><span data-stu-id="2c2ff-215">In this tutorial, you learned how to use the Azure portal and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="2c2ff-216">Créer une base de données Azure pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="2c2ff-216">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="2c2ff-217">Configurer le pare-feu du serveur</span><span class="sxs-lookup"><span data-stu-id="2c2ff-217">Configure the server firewall</span></span>
> * <span data-ttu-id="2c2ff-218">Utiliser l’utilitaire [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) pour créer une base de données</span><span class="sxs-lookup"><span data-stu-id="2c2ff-218">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="2c2ff-219">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="2c2ff-219">Load sample data</span></span>
> * <span data-ttu-id="2c2ff-220">Données de requête</span><span class="sxs-lookup"><span data-stu-id="2c2ff-220">Query data</span></span>
> * <span data-ttu-id="2c2ff-221">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="2c2ff-221">Update data</span></span>
> * <span data-ttu-id="2c2ff-222">Restaurer des données</span><span class="sxs-lookup"><span data-stu-id="2c2ff-222">Restore data</span></span>

<span data-ttu-id="2c2ff-223">Ensuite, découvrez comment utiliser l’interface de ligne de commande Azure pour effectuer des tâches similaires. Lisez le didacticiel [Concevoir votre première base de données Azure pour PostgreSQL à l’aide de l’interface de ligne de commande Azure](tutorial-design-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2c2ff-223">Next, learn how to use Azure CLI to do similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using Azure CLI](tutorial-design-database-using-azure-cli.md)</span></span>
