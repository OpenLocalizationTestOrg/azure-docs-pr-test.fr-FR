---
title: "aaaDesign votre première Azure de base de données pour la base de données MySQL - portail Azure | Documents Microsoft"
description: "Ce didacticiel explique comment toocreate et gérer la base de données Azure pour MySQL server et la base de données à l’aide du portail Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="4248e-103">Concevoir votre première base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4248e-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="4248e-104">Base de données Azure pour MySQL est un service géré qui vous permet de toorun, gérer et mettre à l’échelle des bases de données MySQL hautement disponibles dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="4248e-104">Azure Database for MySQL is a managed service that enables you toorun, manage, and scale highly available MySQL databases in hello cloud.</span></span> <span data-ttu-id="4248e-105">À l’aide de hello portail Azure, vous pouvez facilement gérer votre serveur et concevoir une base de données.</span><span class="sxs-lookup"><span data-stu-id="4248e-105">Using hello Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="4248e-106">Dans ce didacticiel, vous utilisez comment hello toolearn portail Azure pour :</span><span class="sxs-lookup"><span data-stu-id="4248e-106">In this tutorial, you use hello Azure portal toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4248e-107">Créer une base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4248e-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="4248e-108">Configurer le pare-feu du serveur hello</span><span class="sxs-lookup"><span data-stu-id="4248e-108">Configure hello server firewall</span></span>
> * <span data-ttu-id="4248e-109">Utiliser l’outil de ligne de commande de mysql toocreate une base de données</span><span class="sxs-lookup"><span data-stu-id="4248e-109">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="4248e-110">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="4248e-110">Load sample data</span></span>
> * <span data-ttu-id="4248e-111">Données de requête</span><span class="sxs-lookup"><span data-stu-id="4248e-111">Query data</span></span>
> * <span data-ttu-id="4248e-112">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="4248e-112">Update data</span></span>
> * <span data-ttu-id="4248e-113">Restaurer des données</span><span class="sxs-lookup"><span data-stu-id="4248e-113">Restore data</span></span>

## <a name="sign-in-toohello-azure-portal"></a><span data-ttu-id="4248e-114">Se connecter toohello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4248e-114">Sign in toohello Azure portal</span></span>
<span data-ttu-id="4248e-115">Ouvrez votre navigateur web favoris et visitez hello [portail Microsoft Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4248e-115">Open your favorite web browser, and visit hello [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="4248e-116">Entrez vos informations d’identification toosign dans toohello portal.</span><span class="sxs-lookup"><span data-stu-id="4248e-116">Enter your credentials toosign in toohello portal.</span></span> <span data-ttu-id="4248e-117">affichage par défaut de Hello est votre tableau de bord de service.</span><span class="sxs-lookup"><span data-stu-id="4248e-117">hello default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="4248e-118">Créer un serveur de base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4248e-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="4248e-119">Un serveur de base de données Azure pour MySQL est créé avec un ensemble défini de [ressources de calcul et de stockage](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="4248e-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="4248e-120">serveur de Hello est créé dans un [groupe de ressources Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="4248e-120">hello server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="4248e-121">Accédez trop**bases de données** > **base de données Azure pour MySQL**.</span><span class="sxs-lookup"><span data-stu-id="4248e-121">Navigate too**Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="4248e-122">Si vous ne trouvez pas MySQL Server sous **bases de données** catégorie, cliquez sur **afficher tous les** tooshow tous les services de base de données.</span><span class="sxs-lookup"><span data-stu-id="4248e-122">If you cannot find MySQL Server under **Databases** category, click **See all** tooshow all available database services.</span></span> <span data-ttu-id="4248e-123">Vous pouvez également taper **base de données Azure pour MySQL** dans tooquickly de zone de recherche hello trouver le service de hello.</span><span class="sxs-lookup"><span data-stu-id="4248e-123">You can also type **Azure Database for MySQL** in hello search box tooquickly find hello service.</span></span>
<span data-ttu-id="4248e-124">![2-1 naviguer tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="4248e-124">![2-1 Navigate tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="4248e-125">Cliquez sur la vignette **Base de données Azure pour MySQL**, puis sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="4248e-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="4248e-126">Dans notre exemple, renseignez hello Azure de base de données MySQL formulaire avec hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4248e-126">In our example, fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="4248e-127">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="4248e-127">**Setting**</span></span> | <span data-ttu-id="4248e-128">**Valeur suggérée**</span><span class="sxs-lookup"><span data-stu-id="4248e-128">**Suggested value**</span></span> | <span data-ttu-id="4248e-129">**Description du champ**</span><span class="sxs-lookup"><span data-stu-id="4248e-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="4248e-130">*Nom du serveur*</span><span class="sxs-lookup"><span data-stu-id="4248e-130">*Server name*</span></span> | <span data-ttu-id="4248e-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="4248e-131">myserver4demo</span></span>  | <span data-ttu-id="4248e-132">Nom du serveur a toobe global unique.</span><span class="sxs-lookup"><span data-stu-id="4248e-132">Server name has toobe globally unique.</span></span> |
| <span data-ttu-id="4248e-133">*Abonnement*</span><span class="sxs-lookup"><span data-stu-id="4248e-133">*Subscription*</span></span> | <span data-ttu-id="4248e-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="4248e-134">mysubscription</span></span> | <span data-ttu-id="4248e-135">Sélectionnez votre abonnement dans hello de liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="4248e-135">Select your subscription from hello drop-down.</span></span> |
| <span data-ttu-id="4248e-136">*Groupe de ressources*</span><span class="sxs-lookup"><span data-stu-id="4248e-136">*Resource group*</span></span> | <span data-ttu-id="4248e-137">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4248e-137">myresourcegroup</span></span> | <span data-ttu-id="4248e-138">Créez un groupe de ressources ou utilisez un groupe existant.</span><span class="sxs-lookup"><span data-stu-id="4248e-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="4248e-139">*Connexion d’administrateur du serveur*</span><span class="sxs-lookup"><span data-stu-id="4248e-139">*Server admin login*</span></span> | <span data-ttu-id="4248e-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="4248e-140">myadmin</span></span> | <span data-ttu-id="4248e-141">Configurez le nom du compte Administrateur.</span><span class="sxs-lookup"><span data-stu-id="4248e-141">Setup admin account name.</span></span> |
| <span data-ttu-id="4248e-142">*Mot de passe*</span><span class="sxs-lookup"><span data-stu-id="4248e-142">*Password*</span></span> |  | <span data-ttu-id="4248e-143">Définissez un mot de passe complexe pour le compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4248e-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="4248e-144">*Confirmer le mot de passe*</span><span class="sxs-lookup"><span data-stu-id="4248e-144">*Confirm password*</span></span> |  | <span data-ttu-id="4248e-145">Confirmer le mot de passe administrateur hello.</span><span class="sxs-lookup"><span data-stu-id="4248e-145">Confirm hello admin account password.</span></span> |
| <span data-ttu-id="4248e-146">*Emplacement*</span><span class="sxs-lookup"><span data-stu-id="4248e-146">*Location*</span></span> |  | <span data-ttu-id="4248e-147">Sélectionnez une région disponible.</span><span class="sxs-lookup"><span data-stu-id="4248e-147">Select an available region.</span></span> |
| <span data-ttu-id="4248e-148">*Version*</span><span class="sxs-lookup"><span data-stu-id="4248e-148">*Version*</span></span> | <span data-ttu-id="4248e-149">5.7</span><span class="sxs-lookup"><span data-stu-id="4248e-149">5.7</span></span> | <span data-ttu-id="4248e-150">Choisissez la version la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="4248e-150">Choose hello latest version.</span></span> |
| <span data-ttu-id="4248e-151">*Configurer les performances*</span><span class="sxs-lookup"><span data-stu-id="4248e-151">*Configure performance*</span></span> | <span data-ttu-id="4248e-152">De base, 50 unités de calcul, 50 Go</span><span class="sxs-lookup"><span data-stu-id="4248e-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="4248e-153">Choisissez le **niveau de performance**, les **unités de calcul** et le **stockage**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4248e-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="4248e-154">*Code confidentiel tooDashboard*</span><span class="sxs-lookup"><span data-stu-id="4248e-154">*Pin tooDashboard*</span></span> | <span data-ttu-id="4248e-155">Vérification</span><span class="sxs-lookup"><span data-stu-id="4248e-155">Check</span></span> | <span data-ttu-id="4248e-156">Recommandé toocheck cette case, afin que vous pouvez rechercher facilement ultérieurement sur le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="4248e-156">Recommended toocheck this box so you may find hello server easily later on</span></span> |
<span data-ttu-id="4248e-157">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="4248e-157">Then, click **Create**.</span></span> <span data-ttu-id="4248e-158">Dans une ou deux minutes, une nouvelle base de données Azure pour MySQL server est en cours d’exécution dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="4248e-158">In a minute or two, a new Azure Database for MySQL server is running in hello cloud.</span></span> <span data-ttu-id="4248e-159">Vous pouvez cliquer sur **Notifications** bouton sur le processus de déploiement hello barre d’outils toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="4248e-159">You can click **Notifications** button on hello toolbar toomonitor hello deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="4248e-160">Configurer le pare-feu</span><span class="sxs-lookup"><span data-stu-id="4248e-160">Configure firewall</span></span>
<span data-ttu-id="4248e-161">Les bases de données Azure pour MySQL sont protégées par un pare-feu.</span><span class="sxs-lookup"><span data-stu-id="4248e-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="4248e-162">Par défaut, toutes les connexions toohello serveur hello bases de données et à l’intérieur du serveur de hello sont rejetées.</span><span class="sxs-lookup"><span data-stu-id="4248e-162">By default, all connections toohello server and hello databases inside hello server are rejected.</span></span> <span data-ttu-id="4248e-163">Avant de tooAzure de base de données de connexion MySQL pour hello première fois, configurer l’adresse IP du réseau public de hello pare-feu tooadd hello l’ordinateur client (ou plage d’adresses IP).</span><span class="sxs-lookup"><span data-stu-id="4248e-163">Before connecting tooAzure Database for MySQL for hello first time, configure hello firewall tooadd hello client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="4248e-164">Cliquez sur le serveur qui vient d’être créé, puis sur **Sécurité de la connexion**.</span><span class="sxs-lookup"><span data-stu-id="4248e-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="4248e-165">![3-1 Sécurité de la connexion](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="4248e-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="4248e-166">Vous pouvez choisir **Ajouter mon adresse IP** ou configurer les règles de pare-feu ici.</span><span class="sxs-lookup"><span data-stu-id="4248e-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="4248e-167">N’oubliez pas de tooclick **enregistrer** après avoir créé des règles hello.</span><span class="sxs-lookup"><span data-stu-id="4248e-167">Remember tooclick **Save** after you have created hello rules.</span></span>
<span data-ttu-id="4248e-168">Vous pouvez désormais connecter serveur toohello à l’aide d’outil de ligne de commande mysql ou d’outil d’interface utilisateur graphique de banc d’essai de MySQL.</span><span class="sxs-lookup"><span data-stu-id="4248e-168">You can now connect toohello server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="4248e-169">Le serveur de base de données Azure pour MySQL communique sur le port 3306.</span><span class="sxs-lookup"><span data-stu-id="4248e-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="4248e-170">Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 3306 ne peut pas être autorisé par le pare-feu de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="4248e-170">If you are trying tooconnect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="4248e-171">Dans ce cas, tooAzure MySQL server ne peut pas se connecter à moins que votre service informatique ouvre le port 3306.</span><span class="sxs-lookup"><span data-stu-id="4248e-171">If so, you cannot connect tooAzure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="4248e-172">Obtenir des informations de connexion</span><span class="sxs-lookup"><span data-stu-id="4248e-172">Get connection information</span></span>
<span data-ttu-id="4248e-173">Hello Get complet **nom du serveur** et **nom de connexion de serveur admin** pour votre base de données Azure pour le serveur MySQL de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4248e-173">Get hello fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from hello Azure portal.</span></span> <span data-ttu-id="4248e-174">Vous utilisez hello complet nom tooconnect tooyour serveur à l’aide d’outil de ligne de commande mysql.</span><span class="sxs-lookup"><span data-stu-id="4248e-174">You use hello fully qualified server name tooconnect tooyour server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="4248e-175">Dans [portail Azure](https://portal.azure.com/), cliquez sur **toutes les ressources** de menu à gauche hello, nom de type hello et recherchez votre base de données Azure pour le serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="4248e-175">In [Azure portal](https://portal.azure.com/), click **All resources** from hello left-hand menu, type hello name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="4248e-176">Sélectionner les détails de hello hello serveur nom tooview.</span><span class="sxs-lookup"><span data-stu-id="4248e-176">Select hello server name tooview hello details.</span></span>

2. <span data-ttu-id="4248e-177">Sous paramètres de hello titre, cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="4248e-177">Under hello Settings heading, click **Properties**.</span></span> <span data-ttu-id="4248e-178">Notez les valeurs de **NOM DU SERVEUR** et de **NOM DE CONNEXION D’ADMINISTRATEUR DU SERVEUR**.</span><span class="sxs-lookup"><span data-stu-id="4248e-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="4248e-179">Vous pouvez cliquer hello copier bouton suivant tooeach champ toocopy toohello le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="4248e-179">You may click hello copy button next tooeach field toocopy toohello clipboard.</span></span>
   <span data-ttu-id="4248e-180">![4-2 Propriétés de serveur](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="4248e-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="4248e-181">Dans cet exemple, le nom du serveur hello est *myserver4demo.mysql.database.azure.com*, et de la connexion administrateur de serveur hello est  *myadmin@myserver4demo* .</span><span class="sxs-lookup"><span data-stu-id="4248e-181">In this example, hello server name is *myserver4demo.mysql.database.azure.com*, and hello server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="4248e-182">Connexion serveur toohello à l’aide de mysql</span><span class="sxs-lookup"><span data-stu-id="4248e-182">Connect toohello server using mysql</span></span>
<span data-ttu-id="4248e-183">Utilisez [outil de ligne de commande mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish un tooyour de connexion de base de données Azure pour le serveur MySQL.</span><span class="sxs-lookup"><span data-stu-id="4248e-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="4248e-184">Vous pouvez exécuter outil de ligne de commande mysql hello de hello Azure Cloud Shell dans le navigateur de hello ou à partir de votre propre ordinateur à l’aide des outils de mysql sont installés localement.</span><span class="sxs-lookup"><span data-stu-id="4248e-184">You can run hello mysql command-line tool from hello Azure Cloud Shell in hello browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="4248e-185">toolaunch hello Azure Cloud interpréteur de commandes, cliquez sur hello `Try It` bouton sur un bloc de code dans cet article, ou visitez hello portail Azure, puis cliquez sur hello `>_` icône dans la barre d’outils droite supérieure hello.</span><span class="sxs-lookup"><span data-stu-id="4248e-185">toolaunch hello Azure Cloud Shell, click hello `Try It` button on a code block in this article, or visit hello Azure portal and click hello `>_` icon in hello top right toolbar.</span></span> 

<span data-ttu-id="4248e-186">Tapez hello commande tooconnect :</span><span class="sxs-lookup"><span data-stu-id="4248e-186">Type hello command tooconnect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="4248e-187">Créer une base de données vide</span><span class="sxs-lookup"><span data-stu-id="4248e-187">Create a blank database</span></span>
<span data-ttu-id="4248e-188">Une fois que vous êtes connecté toohello server, créez un toowork de base de données vide avec.</span><span class="sxs-lookup"><span data-stu-id="4248e-188">Once you’re connected toohello server, create a blank database toowork with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="4248e-189">À l’invite de hello, exécutez hello suivant de base de données de commande tooswitch connexion toothis nouvellement créé :</span><span class="sxs-lookup"><span data-stu-id="4248e-189">At hello prompt, run hello following command tooswitch connection toothis newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="4248e-190">Créer des tables dans la base de données hello</span><span class="sxs-lookup"><span data-stu-id="4248e-190">Create tables in hello database</span></span>
<span data-ttu-id="4248e-191">Maintenant que vous savez comment tooconnect toohello base de données Azure pour la base de données MySQL, nous pouvons sur la façon toocomplete certaines tâches de base.</span><span class="sxs-lookup"><span data-stu-id="4248e-191">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="4248e-192">Tout d’abord, nous pouvons créer une table et y charger des données.</span><span class="sxs-lookup"><span data-stu-id="4248e-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="4248e-193">Nous allons créer une table qui stocke des données d’inventaire.</span><span class="sxs-lookup"><span data-stu-id="4248e-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="4248e-194">Charger des données dans les tables de hello</span><span class="sxs-lookup"><span data-stu-id="4248e-194">Load data into hello tables</span></span>
<span data-ttu-id="4248e-195">Maintenant que nous disposons d’une table, nous pouvons y insérer des données.</span><span class="sxs-lookup"><span data-stu-id="4248e-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="4248e-196">Fenêtre d’invite de commandes ouverte hello, puis exécutez hello suivant requête tooinsert certaines lignes de données.</span><span class="sxs-lookup"><span data-stu-id="4248e-196">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="4248e-197">Vous avez maintenant deux lignes d’exemples de données dans la table hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="4248e-197">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="4248e-198">Interroger et mettre à jour les données hello dans les tables de hello</span><span class="sxs-lookup"><span data-stu-id="4248e-198">Query and update hello data in hello tables</span></span>
<span data-ttu-id="4248e-199">Exécutez hello suivant tooretrieve les informations de requête à partir de la table de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="4248e-199">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="4248e-200">Vous pouvez également mettre à jour les données hello dans les tables de hello.</span><span class="sxs-lookup"><span data-stu-id="4248e-200">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="4248e-201">ligne de Hello est mise à jour en conséquence lorsque vous récupérez des données.</span><span class="sxs-lookup"><span data-stu-id="4248e-201">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="4248e-202">Restaurer un état antérieur de tooa de base de données dans le temps</span><span class="sxs-lookup"><span data-stu-id="4248e-202">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="4248e-203">Imaginez que vous avez accidentellement supprimé une table de base de données importants et ne peut pas récupérer les données de salutation facilement.</span><span class="sxs-lookup"><span data-stu-id="4248e-203">Imagine you have accidentally deleted an important database table, and cannot recover hello data easily.</span></span> <span data-ttu-id="4248e-204">Base de données Azure pour MySQL vous permet de toorestore hello server tooa point dans le temps, créez une copie de bases de données hello dans du nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="4248e-204">Azure Database for MySQL allows you toorestore hello server tooa point in time, creating a copy of hello databases into new server.</span></span> <span data-ttu-id="4248e-205">Les données supprimées, vous pouvez utiliser cette nouvelle toorecover de serveur.</span><span class="sxs-lookup"><span data-stu-id="4248e-205">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="4248e-206">Hello suivant étapes restauration hello exemple server tooa point avant hello table a été ajoutée.</span><span class="sxs-lookup"><span data-stu-id="4248e-206">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

1. <span data-ttu-id="4248e-207">Bonjour portail Azure, recherchez votre base de données Azure pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="4248e-207">In hello Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="4248e-208">Sur hello **vue d’ensemble** , cliquez sur **restaurer** sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="4248e-208">On hello **Overview** page, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="4248e-209">page de restauration Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="4248e-209">hello Restore page opens.</span></span>

   ![10-1 Restaurer une base de données](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="4248e-211">Remplir hello **restaurer** formulaire avec les informations de hello requis.</span><span class="sxs-lookup"><span data-stu-id="4248e-211">Fill out hello **Restore** form with hello required information.</span></span>
   
   ![10-2 Formulaire de restauration](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="4248e-213">**Point de restauration**: sélectionnez un point dans le temps que vous souhaitez toorestore, pendant les laps de temps hello répertoriés.</span><span class="sxs-lookup"><span data-stu-id="4248e-213">**Restore point**: Select a point-in-time that you want toorestore to, within hello timeframe listed.</span></span> <span data-ttu-id="4248e-214">Assurez-vous que tooconvert tooUTC de votre fuseau horaire local.</span><span class="sxs-lookup"><span data-stu-id="4248e-214">Make sure tooconvert your local timezone tooUTC.</span></span>
   - <span data-ttu-id="4248e-215">**Restaurer le serveur de toonew**: fournir un nouveau nom du serveur toorestore à.</span><span class="sxs-lookup"><span data-stu-id="4248e-215">**Restore toonew server**: Provide a new server name you want toorestore to.</span></span>
   - <span data-ttu-id="4248e-216">**Emplacement**: région de hello est identique au serveur de source de hello et ne peut pas être modifiée.</span><span class="sxs-lookup"><span data-stu-id="4248e-216">**Location**: hello region is same as hello source server, and cannot be changed.</span></span>
   - <span data-ttu-id="4248e-217">**Niveau de tarification**: hello niveau tarifaire est hello identique hello serveur source et ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="4248e-217">**Pricing tier**: hello pricing tier is hello same as hello source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="4248e-218">Cliquez sur **OK** toorestore hello server trop[restaurer tooa point dans le temps](./howto-restore-server-portal.md) avant hello table a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="4248e-218">Click **OK** toorestore hello server too[restore tooa point in time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="4248e-219">Restauration d’un serveur crée une copie du serveur hello, as of point hello dans le temps que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="4248e-219">Restoring a server creates a new copy of hello server, as of hello point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4248e-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4248e-220">Next steps</span></span>
<span data-ttu-id="4248e-221">Dans ce didacticiel, vous utilisez comment hello toolearned portail Azure pour :</span><span class="sxs-lookup"><span data-stu-id="4248e-221">In this tutorial, you use hello Azure portal toolearned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4248e-222">Créer une base de données Azure pour MySQL</span><span class="sxs-lookup"><span data-stu-id="4248e-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="4248e-223">Configurer le pare-feu du serveur hello</span><span class="sxs-lookup"><span data-stu-id="4248e-223">Configure hello server firewall</span></span>
> * <span data-ttu-id="4248e-224">Utiliser l’outil de ligne de commande de mysql toocreate une base de données</span><span class="sxs-lookup"><span data-stu-id="4248e-224">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="4248e-225">Charger les exemples de données</span><span class="sxs-lookup"><span data-stu-id="4248e-225">Load sample data</span></span>
> * <span data-ttu-id="4248e-226">Données de requête</span><span class="sxs-lookup"><span data-stu-id="4248e-226">Query data</span></span>
> * <span data-ttu-id="4248e-227">Mettre à jour des données</span><span class="sxs-lookup"><span data-stu-id="4248e-227">Update data</span></span>
> * <span data-ttu-id="4248e-228">Restaurer des données</span><span class="sxs-lookup"><span data-stu-id="4248e-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4248e-229">Comment tooconnect applications tooAzure de base de données MySQL</span><span class="sxs-lookup"><span data-stu-id="4248e-229">How tooconnect applications tooAzure Database for MySQL</span></span>](./howto-connection-string.md)
