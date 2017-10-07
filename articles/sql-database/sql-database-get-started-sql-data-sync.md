---
title: "aaaGetting main de la synchronisation des données SQL Azure (version préliminaire) | Documents Microsoft"
description: "Ce didacticiel décrit la prise en main d’Azure SQL Data Sync (version préliminaire)."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="2a795-103">Prise en main d’Azure SQL Data Sync (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="2a795-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="2a795-104">Dans ce didacticiel, vous découvrez comment tooset de synchronisation des données SQL Azure en créant un groupe de synchronisation hybride qui contient des instances de base de données SQL Azure et SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2a795-104">In this tutorial, you learn how tooset up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="2a795-105">nouveau groupe de synchronisation Hello est entièrement configuré et synchronise sur Planification hello définie.</span><span class="sxs-lookup"><span data-stu-id="2a795-105">hello new sync group is fully configured and synchronizes on hello schedule you set.</span></span>

<span data-ttu-id="2a795-106">Ce didacticiel suppose que vous ayez déjà utilisé SQL Database et SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2a795-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="2a795-107">Pour une vue d’ensemble de SQL Data Sync, consultez la section [Synchronisation des données](sql-database-sync-data.md).</span><span class="sxs-lookup"><span data-stu-id="2a795-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="2a795-108">Pour obtenir des exemples PowerShell complets qui montrent comment tooconfigure synchronisation des données SQL, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="2a795-108">For complete PowerShell examples that show how tooconfigure SQL Data Sync, see hello following articles:</span></span>
-   [<span data-ttu-id="2a795-109">Utilisez toosync PowerShell entre plusieurs bases de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="2a795-109">Use PowerShell toosync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="2a795-110">Utilisez toosync PowerShell entre une base de données SQL Azure et une base de données locale SQL Server</span><span class="sxs-lookup"><span data-stu-id="2a795-110">Use PowerShell toosync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="2a795-111">Hello technique documentation complète pour la synchronisation des données SQL Azure, anciennement situé sur le site MSDN, est disponible en tant qu’un. Document PDF.</span><span class="sxs-lookup"><span data-stu-id="2a795-111">hello complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="2a795-112">Téléchargez-le [ici](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span><span class="sxs-lookup"><span data-stu-id="2a795-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="2a795-113">Étape 1 : créer un groupe de synchronisation</span><span class="sxs-lookup"><span data-stu-id="2a795-113">Step 1 - Create sync group</span></span>

### <a name="locate-hello-data-sync-settings"></a><span data-ttu-id="2a795-114">Localiser les paramètres de synchronisation des données hello</span><span class="sxs-lookup"><span data-stu-id="2a795-114">Locate hello Data Sync settings</span></span>

1.  <span data-ttu-id="2a795-115">Dans votre navigateur, accédez à toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2a795-115">In your browser, navigate toohello Azure portal.</span></span>

2.  <span data-ttu-id="2a795-116">Dans le portail hello, localisez vos bases de données SQL à partir de votre tableau de bord ou à partir de l’icône de bases de données SQL hello sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-116">In hello portal, locate your SQL databases from your Dashboard or from hello SQL Databases icon on hello toolbar.</span></span>

    ![Liste des bases de données SQL Azure](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="2a795-118">Sur hello **bases de données SQL** panneau, sélectionnez hello base de données SQL que vous souhaitez toouse comme base de données concentrateur hello pour synchronisation de données. Panneau de base de données SQL hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="2a795-118">On hello **SQL databases** blade, select hello existing SQL database that you want toouse as hello hub database for Data Sync. hello SQL database blade opens.</span></span>

4.  <span data-ttu-id="2a795-119">Dans le panneau de base de données hello SQL pour la base de données sélectionnée hello, sélectionnez **synchroniser les bases de données tooother**.</span><span class="sxs-lookup"><span data-stu-id="2a795-119">On hello SQL database blade for hello selected database, select **Sync tooother databases**.</span></span> <span data-ttu-id="2a795-120">Panneau de synchronisation des données Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="2a795-120">hello Data Sync blade opens.</span></span>

    ![Option de bases de données de synchronisation tooother](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="2a795-122">Créer un groupe de synchronisation</span><span class="sxs-lookup"><span data-stu-id="2a795-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="2a795-123">Dans le panneau de la synchronisation des données hello, sélectionnez **nouveau groupe de synchronisation**.</span><span class="sxs-lookup"><span data-stu-id="2a795-123">On hello Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="2a795-124">Hello **nouveau groupe de synchronisation** panneau s’ouvre à l’étape 1, **créer un groupe de synchronisation**, mise en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="2a795-124">hello **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="2a795-125">Hello **créer un groupe de synchronisation de données** panneau s’ouvre également.</span><span class="sxs-lookup"><span data-stu-id="2a795-125">hello **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="2a795-126">Sur hello **créer un groupe de synchronisation de données** panneau, hello suivants choses :</span><span class="sxs-lookup"><span data-stu-id="2a795-126">On hello **Create Data Sync Group** blade, do hello following things:</span></span>

    1.  <span data-ttu-id="2a795-127">Bonjour **nom du groupe de synchronisation** , entrez un nom pour le nouveau groupe de synchronisation hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-127">In hello **Sync Group Name** field, enter a name for hello new sync group.</span></span>

    2.  <span data-ttu-id="2a795-128">Bonjour **base de données de métadonnées de synchronisation** , choisissez si toocreate une base de données (recommandé) ou toouse une base de données existant.</span><span class="sxs-lookup"><span data-stu-id="2a795-128">In hello **Sync Metadata Database** section, choose whether toocreate a new database (recommended) or toouse an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="2a795-129">Microsoft recommande de créer un toouse de base de données vide comme hello de base de données de métadonnées de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="2a795-129">Microsoft recommends that you create a new, empty database toouse as hello Sync Metadata Database.</span></span> <span data-ttu-id="2a795-130">SQL Data Sync crée les tables dans cette base de données et exécute une charge de travail fréquente.</span><span class="sxs-lookup"><span data-stu-id="2a795-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="2a795-131">Cette base de données est automatiquement partagé en tant que hello de base de données de synchronisation des métadonnées pour tous vos groupes de synchronisation dans une région de hello sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="2a795-131">This database is automatically shared as hello Sync Metadata Database for all of your Sync groups in hello selected region.</span></span> <span data-ttu-id="2a795-132">Vous ne pouvez pas modifier hello de base de données de synchronisation des métadonnées, son nom ou son niveau de service sans le déposer.</span><span class="sxs-lookup"><span data-stu-id="2a795-132">You can't change hello Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="2a795-133">Si vous avez choisi **Nouvelle base de données**, sélectionnez **Créer une nouvelle base de données.**</span><span class="sxs-lookup"><span data-stu-id="2a795-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="2a795-134">Hello **base de données SQL** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="2a795-134">hello **SQL Database** blade opens.</span></span> <span data-ttu-id="2a795-135">Sur hello **base de données SQL** panneau, nommez et configurer la nouvelle base de données hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-135">On hello **SQL Database** blade, name and configure hello new database.</span></span> <span data-ttu-id="2a795-136">Sélectionnez ensuite **OK**.</span><span class="sxs-lookup"><span data-stu-id="2a795-136">Then select **OK**.</span></span>

        <span data-ttu-id="2a795-137">Si vous avez choisi **utiliser la base de données existante**, sélectionnez base de données hello à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-137">If you chose **Use existing database**, select hello database from hello list.</span></span>

    3.  <span data-ttu-id="2a795-138">Bonjour **Sync automatique** , sélectionnez tout d’abord **sur** ou **hors**.</span><span class="sxs-lookup"><span data-stu-id="2a795-138">In hello **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="2a795-139">Si vous avez choisi **sur**, Bonjour **fréquence de synchronisation** section, entrez un nombre et sélectionnez secondes, Minutes, heures ou jours.</span><span class="sxs-lookup"><span data-stu-id="2a795-139">If you chose **On**, in hello **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![Spécifier la fréquence de synchronisation](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="2a795-141">Bonjour **la résolution des conflits** , sélectionnez le « wins Hub » ou « Wins de membre ».</span><span class="sxs-lookup"><span data-stu-id="2a795-141">In hello **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![Spécifier le mode de résolution des conflits](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="2a795-143">Sélectionnez **OK** et attendez hello nouvelle synchronisation groupe toobe créés et déployés.</span><span class="sxs-lookup"><span data-stu-id="2a795-143">Select **OK** and wait for hello new sync group toobe created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="2a795-144">Étape 2 : ajouter des membres de synchronisation</span><span class="sxs-lookup"><span data-stu-id="2a795-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="2a795-145">Une fois le nouveau groupe de synchronisation hello est créé et déployé, l’étape 2, **ajouter des membres de la synchronisation**, est mis en surbrillance dans hello **nouveau groupe de synchronisation** panneau.</span><span class="sxs-lookup"><span data-stu-id="2a795-145">After hello new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in hello **New sync group** blade.</span></span>

<span data-ttu-id="2a795-146">Bonjour **base de données concentrateur** section, entrez les informations d’identification existantes hello hello de base de données SQL server sur le hello hub base de données.</span><span class="sxs-lookup"><span data-stu-id="2a795-146">In hello **Hub Database** section, enter hello existing credentials for hello SQL Database server on which hello hub database is located.</span></span> <span data-ttu-id="2a795-147">N’entrez pas de *nouvelles* informations d’identification dans cette section.</span><span class="sxs-lookup"><span data-stu-id="2a795-147">Don't enter *new* credentials in this section.</span></span>

![Base de données concentrateur a été ajouté toosync groupe](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="2a795-149">Ajouter une base de données SQL Azure Database</span><span class="sxs-lookup"><span data-stu-id="2a795-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="2a795-150">Bonjour **base de données membre** section, vous pouvez également ajouter un groupe de synchronisation de base de données SQL Azure toohello en sélectionnant **ajouter une base de données Azure**.</span><span class="sxs-lookup"><span data-stu-id="2a795-150">In hello **Member Database** section, optionally add an Azure SQL Database toohello sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="2a795-151">Hello **configurer la base de données Azure** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="2a795-151">hello **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="2a795-152">Sur hello **configurer la base de données Azure** panneau, hello suivants choses :</span><span class="sxs-lookup"><span data-stu-id="2a795-152">On hello **Configure Azure Database** blade, do hello following things:</span></span>

1.  <span data-ttu-id="2a795-153">Bonjour **nom du membre de synchronisation** champ, fournissez un nom pour le nouveau membre de synchronisation hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-153">In hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="2a795-154">Ce nom est différent de nom hello de base de données hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="2a795-154">This name is distinct from hello name of hello database itself.</span></span>

2.  <span data-ttu-id="2a795-155">Bonjour **abonnement** hello, sélectionnez associés à un abonnement Azure à des fins de facturation.</span><span class="sxs-lookup"><span data-stu-id="2a795-155">In hello **Subscription** field, select hello associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="2a795-156">Bonjour **Azure SQL Server** serveur de base de données SQL existante, sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-156">In hello **Azure SQL Server** field, select hello existing SQL database server.</span></span>

4.  <span data-ttu-id="2a795-157">Bonjour **base de données SQL Azure** hello, sélectionnez base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="2a795-157">In hello **Azure SQL Database** field, select hello existing SQL database.</span></span>

5.  <span data-ttu-id="2a795-158">Bonjour **Directions de synchronisation** , sélectionnez la synchronisation bidirectionnelle, toohello concentrateur, ou à partir de hello Hub.</span><span class="sxs-lookup"><span data-stu-id="2a795-158">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

    ![Ajout d’un nouveau membre de synchronisation SQL Database](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="2a795-160">Bonjour **nom d’utilisateur** et **mot de passe** , saisissez les informations d’identification existantes hello pour hello de base de données SQL server sur le hello membre base de données.</span><span class="sxs-lookup"><span data-stu-id="2a795-160">In hello **Username** and **Password** fields, enter hello existing credentials for hello SQL Database server on which hello member database is located.</span></span> <span data-ttu-id="2a795-161">N’entrez pas de *nouvelles* informations d’identification dans cette section.</span><span class="sxs-lookup"><span data-stu-id="2a795-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="2a795-162">Sélectionnez **OK** et attendez hello nouvelle synchronisation membre toobe créés et déployés.</span><span class="sxs-lookup"><span data-stu-id="2a795-162">Select **OK** and wait for hello new sync member toobe created and deployed.</span></span>

    ![Nouveau membre de synchronisation SQL Database ajouté](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="2a795-164">Ajouter une base de données SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="2a795-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="2a795-165">Bonjour **base de données membre** section éventuellement ajouter un groupe de synchronisation toohello SQL Server local en sélectionnant **ajouter une base de données local**.</span><span class="sxs-lookup"><span data-stu-id="2a795-165">In hello **Member Database** section, optionally add an on-premises SQL Server toohello sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="2a795-166">Hello **configurer On-Premises** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="2a795-166">hello **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="2a795-167">Sur hello **configurer On-Premises** panneau, hello suivants choses :</span><span class="sxs-lookup"><span data-stu-id="2a795-167">On hello **Configure On-Premises** blade, do hello following things:</span></span>

1.  <span data-ttu-id="2a795-168">Sélectionnez **choisir hello passerelle de l’Agent de synchronisation**.</span><span class="sxs-lookup"><span data-stu-id="2a795-168">Select **Choose hello Sync Agent Gateway**.</span></span> <span data-ttu-id="2a795-169">Hello **sélectionnez l’Agent de synchronisation** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="2a795-169">hello **Select Sync Agent** blade opens.</span></span>

    ![Choisissez la passerelle de l’agent de synchronisation hello](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="2a795-171">Sur hello **choisir hello passerelle de l’Agent de synchronisation** panneau, choisissez si toouse un agent existant ou créer un nouvel agent.</span><span class="sxs-lookup"><span data-stu-id="2a795-171">On hello **Choose hello Sync Agent Gateway** blade, choose whether toouse an existing agent or create a new agent.</span></span>

    <span data-ttu-id="2a795-172">Si vous avez choisi **les agents existants**, sélectionnez hello agent existant à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-172">If you chose **Existing agents**, select hello existing agent from hello list.</span></span>

    <span data-ttu-id="2a795-173">Si vous avez choisi **créer un nouvel agent**, hello suivants choses :</span><span class="sxs-lookup"><span data-stu-id="2a795-173">If you chose **Create a new agent**, do hello following things:</span></span>

    1.  <span data-ttu-id="2a795-174">Télécharger le logiciel de l’agent de synchronisation hello client à partir du lien hello fourni et l’installer sur l’ordinateur hello où se trouve hello SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2a795-174">Download hello client sync agent software from hello link provided and install it on hello computer where hello SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="2a795-175">Vous avez tooopen sortant le port TCP 1433 dans l’agent client hello hello pare-feu toolet de communiquer avec le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-175">You have tooopen outbound TCP port 1433 in hello firewall toolet hello client agent communicate with hello server.</span></span>


    2.  <span data-ttu-id="2a795-176">Entrez un nom pour l’agent de hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-176">Enter a name for hello agent.</span></span>

    3.  <span data-ttu-id="2a795-177">Sélectionnez **Créer et générer une clé**.</span><span class="sxs-lookup"><span data-stu-id="2a795-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="2a795-178">Copiez le Presse-papiers toohello clé de l’agent hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-178">Copy hello agent key toohello clipboard.</span></span>
        
        ![Création d’un agent de synchronisation](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="2a795-180">Sélectionnez **OK** tooclose hello **sélectionnez l’Agent de synchronisation** panneau.</span><span class="sxs-lookup"><span data-stu-id="2a795-180">Select **OK** tooclose hello **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="2a795-181">Sur l’ordinateur SQL Server de hello, recherchez et exécuter l’application de l’Agent de synchronisation Client hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-181">On hello SQL Server computer, locate and run hello Client Sync Agent app.</span></span>

        ![application de l’agent client de synchronisation des données de Hello](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="2a795-183">Dans l’application de l’agent de synchronisation hello, sélectionnez **envoyer la clé de l’Agent**.</span><span class="sxs-lookup"><span data-stu-id="2a795-183">In hello sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="2a795-184">Hello **Configuration de base de données de métadonnées de synchronisation** boîte de dialogue s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="2a795-184">hello **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="2a795-185">Bonjour **Configuration de base de données de métadonnées de synchronisation** boîte de dialogue, coller dans la clé d’agent hello copié à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2a795-185">In hello **Sync Metadata Database Configuration** dialog box, paste in hello agent key copied from hello Azure portal.</span></span> <span data-ttu-id="2a795-186">Fournissent également des informations d’identification existantes de hello pour le serveur de base de données SQL Azure hello sur quel hello les métadonnées de base de données se trouve.</span><span class="sxs-lookup"><span data-stu-id="2a795-186">Also provide hello existing credentials for hello Azure SQL Database server on which hello metadata database is located.</span></span> <span data-ttu-id="2a795-187">(Si vous avez créé une nouvelle base de données de métadonnées, cette base de données est sur hello même serveur que la base de données concentrateur hello.) Sélectionnez **OK** et attendez hello configuration toofinish.</span><span class="sxs-lookup"><span data-stu-id="2a795-187">(If you created a new metadata database, this database is on hello same server as hello hub database.) Select **OK** and wait for hello configuration toofinish.</span></span>

        ![Entrez hello des informations d’identification clé et le serveur de l’agent](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="2a795-189">Si vous obtenez une erreur de pare-feu à ce stade, vous devez toocreate une règle de pare-feu sur le trafic entrant à partir de l’ordinateur SQL Server de hello tooallow Azure.</span><span class="sxs-lookup"><span data-stu-id="2a795-189">If you get a firewall error at this point, you have toocreate a firewall rule on Azure tooallow incoming traffic from hello SQL Server computer.</span></span> <span data-ttu-id="2a795-190">Vous pouvez créer des règles de hello manuellement dans le portail de hello, mais il peut s’avérer plus facile toocreate il dans SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="2a795-190">You can create hello rule manually in hello portal, but you may find it easier toocreate it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="2a795-191">Dans SSMS, essayez de base de données du concentrateur tooconnect toohello sur Azure.</span><span class="sxs-lookup"><span data-stu-id="2a795-191">In SSMS, try tooconnect toohello hub database on Azure.</span></span> <span data-ttu-id="2a795-192">Entrez son nom sous la forme \<nom_base_données_hub\>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="2a795-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="2a795-193">Suivez les étapes de hello de règle de pare-feu Azure hello boîte de dialogue zone tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-193">Follow hello steps in hello dialog box tooconfigure hello Azure firewall rule.</span></span> <span data-ttu-id="2a795-194">Application de l’Agent de synchronisation Client toohello est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="2a795-194">Then return toohello Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="2a795-195">Dans l’application de l’Agent de synchronisation Client hello, cliquez sur **inscrire** tooregister une base de données SQL Server avec l’agent de hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-195">In hello Client Sync Agent app, click **Register** tooregister a SQL Server database with hello agent.</span></span> <span data-ttu-id="2a795-196">Hello **de Configuration SQL Server** boîte de dialogue s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="2a795-196">hello **SQL Server Configuration** dialog box opens.</span></span>

        ![Ajouter et configurer une base de données SQL Server](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="2a795-198">Bonjour **de Configuration SQL Server** boîte de dialogue, choisissez si tooconnect à l’aide de SQL Server ou l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="2a795-198">In hello **SQL Server Configuration** dialog box, choose whether tooconnect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="2a795-199">Si vous choisissez l’authentification SQL Server, entrez les informations d’identification existantes hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-199">If you chose SQL Server authentication, enter hello existing credentials.</span></span> <span data-ttu-id="2a795-200">Indiquez des noms de SQL Server de hello et hello de base de données hello que vous souhaitez toosync.</span><span class="sxs-lookup"><span data-stu-id="2a795-200">Provide hello SQL Server name and hello name of hello database that you want toosync.</span></span> <span data-ttu-id="2a795-201">Sélectionnez **tester la connexion** tootest vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="2a795-201">Select **Test connection** tootest your settings.</span></span> <span data-ttu-id="2a795-202">Ensuite, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2a795-202">Then select **Save**.</span></span> <span data-ttu-id="2a795-203">base de données inscrite Hello s’affiche dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-203">hello registered database appears in hello list.</span></span>

        ![La base de données SQL Server est maintenant inscrite.](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="2a795-205">Vous pouvez fermer une application de l’Agent de synchronisation Client hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-205">You can now close hello Client Sync Agent app.</span></span>

    12. <span data-ttu-id="2a795-206">Dans le portail hello, sur hello **configurer On-Premises** panneau, sélectionnez **sélectionnez hello de base de données.**</span><span class="sxs-lookup"><span data-stu-id="2a795-206">In hello portal, on hello **Configure On-Premises** blade, select **Select hello Database.**</span></span> <span data-ttu-id="2a795-207">Hello **sélectionner une base de données** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="2a795-207">hello **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="2a795-208">Sur hello **sélectionner une base de données** panneau, Bonjour **nom du membre de synchronisation** champ, fournissez un nom pour le nouveau membre de synchronisation hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-208">On hello **Select Database** blade, in hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="2a795-209">Ce nom est différent de nom hello de base de données hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="2a795-209">This name is distinct from hello name of hello database itself.</span></span> <span data-ttu-id="2a795-210">Sélectionnez la base de données de hello à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-210">Select hello database from hello list.</span></span> <span data-ttu-id="2a795-211">Bonjour **Directions de synchronisation** , sélectionnez la synchronisation bidirectionnelle, toohello concentrateur, ou à partir de hello Hub.</span><span class="sxs-lookup"><span data-stu-id="2a795-211">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

        ![Sélectionnez hello sur la base de données de site](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="2a795-213">Sélectionnez **OK** tooclose hello **sélectionner une base de données** panneau.</span><span class="sxs-lookup"><span data-stu-id="2a795-213">Select **OK** tooclose hello **Select Database** blade.</span></span> <span data-ttu-id="2a795-214">Puis sélectionnez **OK** tooclose hello **configurer On-Premises** lame et attendez hello nouveau synchroniser toobe membre créé et déployé.</span><span class="sxs-lookup"><span data-stu-id="2a795-214">Then select **OK** tooclose hello **Configure On-Premises** blade and wait for hello new sync member toobe created and deployed.</span></span> <span data-ttu-id="2a795-215">Enfin, cliquez sur **OK** tooclose hello **sélectionner les membres de la synchronisation** panneau.</span><span class="sxs-lookup"><span data-stu-id="2a795-215">Finally, click **OK** tooclose hello **Select sync members** blade.</span></span>

        ![Sur la base de données local ajouté toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="2a795-217">tooconnect tooSQL synchronisation des données et l’agent local de hello, ajoutez votre rôle d’utilisateur nom toohello `DataSync_Executor`.</span><span class="sxs-lookup"><span data-stu-id="2a795-217">tooconnect tooSQL Data Sync and hello local agent, add your user name toohello role `DataSync_Executor`.</span></span> <span data-ttu-id="2a795-218">Synchronisation des données crée ce rôle sur l’instance de SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-218">Data Sync creates this role on hello SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="2a795-219">Étape 3 : configurer le groupe de synchronisation</span><span class="sxs-lookup"><span data-stu-id="2a795-219">Step 3 - Configure sync group</span></span>

<span data-ttu-id="2a795-220">Une fois les nouveaux membres de groupe de synchronisation hello sont créés et déployés, étape 3, **groupe de synchronisation configurer**, est mis en surbrillance dans hello **nouveau groupe de synchronisation** panneau.</span><span class="sxs-lookup"><span data-stu-id="2a795-220">After hello new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in hello **New sync group** blade.</span></span>

1.  <span data-ttu-id="2a795-221">Sur hello **Tables** panneau, sélectionnez une base de données à partir de la liste de hello de synchronisation des membres du groupe, puis sélectionnez **actualisation du schéma**.</span><span class="sxs-lookup"><span data-stu-id="2a795-221">On hello **Tables** blade, select a database from hello list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="2a795-222">Dans la liste hello des tables disponibles, sélectionnez les tables de hello que vous souhaitez toosync.</span><span class="sxs-lookup"><span data-stu-id="2a795-222">From hello list of available tables, select hello tables that you want toosync.</span></span>

    ![Sélectionner les tables toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="2a795-224">Par défaut, toutes les colonnes de table de hello sont sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="2a795-224">By default, all columns in hello table are selected.</span></span> <span data-ttu-id="2a795-225">Si vous ne souhaitez pas toutes les colonnes hello toosync, désactivez la case à cocher hello pour les colonnes hello que vous ne souhaitez pas toosync.</span><span class="sxs-lookup"><span data-stu-id="2a795-225">If you don't want toosync all hello columns, disable hello checkbox for hello columns that you don't want toosync.</span></span> <span data-ttu-id="2a795-226">N’oubliez pas sélectionné de la colonne de clé primaire tooleave hello.</span><span class="sxs-lookup"><span data-stu-id="2a795-226">Be sure tooleave hello primary key column selected.</span></span>

    ![Sélectionner les champs toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="2a795-228">Enfin, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2a795-228">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a795-229">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2a795-229">Next steps</span></span>
<span data-ttu-id="2a795-230">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="2a795-230">Congratulations.</span></span> <span data-ttu-id="2a795-231">Vous avez créé un groupe de synchronisation incluant une instance de base de données SQL et une base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2a795-231">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="2a795-232">Pour plus d’informations sur SQL Database et SQL Data Sync, consultez :</span><span class="sxs-lookup"><span data-stu-id="2a795-232">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="2a795-233">Téléchargez la documentation technique hello complète synchronisation des données SQL</span><span class="sxs-lookup"><span data-stu-id="2a795-233">Download hello complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="2a795-234">Télécharger la documentation des API REST de SQL Data Sync hello</span><span class="sxs-lookup"><span data-stu-id="2a795-234">Download hello SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="2a795-235">Vue d’ensemble des bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="2a795-235">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="2a795-236">Gestion du cycle de vie des bases de données</span><span class="sxs-lookup"><span data-stu-id="2a795-236">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
