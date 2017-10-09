---
title: aaaSet des PostgreSQL sur un VM Linux | Documents Microsoft
description: "Découvrez comment tooinstall et configurer PostgreSQL sur un ordinateur virtuel de Linux dans Azure"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 1a747363-0cc5-4ba3-9be7-084dfeb04651
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 40209647924dffce11500705eb2d9f41c14df6ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="afc6e-103">Installer et configurer PostgreSQL sur Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="afc6e-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="afc6e-104">PostgreSQL est tooOracle similaire d’avancée de la base de données open source et DB2.</span><span class="sxs-lookup"><span data-stu-id="afc6e-104">PostgreSQL is an advanced open-source database similar tooOracle and DB2.</span></span> <span data-ttu-id="afc6e-105">Il inclut des fonctionnalités destinées aux entreprises, comme la conformité complète à ACID, un traitement transactionnel fiable et un contrôle d’accès concurrentiel multiversion.</span><span class="sxs-lookup"><span data-stu-id="afc6e-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="afc6e-106">Il prend également en charge des normes comme ANSI SQL et SQL/MED (y compris les wrappers de données externes pour Oracle, MySQL, MongoDB et beaucoup d’autres).</span><span class="sxs-lookup"><span data-stu-id="afc6e-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="afc6e-107">Il est hautement extensible, avec la prise en charge de 12 langages procéduraux, les index GIN et GIST, la prise en charge des données spatiales et plusieurs fonctionnalités de type NoSQL pour les applications JSON ou basées sur les paires clé-valeur.</span><span class="sxs-lookup"><span data-stu-id="afc6e-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="afc6e-108">Dans cet article, vous allez apprendre comment tooinstall et configurer PostgreSQL sur une machine virtuelle Azure exécutant Linux.</span><span class="sxs-lookup"><span data-stu-id="afc6e-108">In this article, you will learn how tooinstall and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="afc6e-109">Installation de PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="afc6e-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="afc6e-110">Vous devez déjà disposer d’une machine virtuelle Azure exécutant Linux dans l’ordre toocomplete ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="afc6e-110">You must already have an Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="afc6e-111">toocreate et configurer un VM Linux avant de procéder, consultez la [didacticiel de la machine virtuelle de Azure Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="afc6e-111">toocreate and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="afc6e-112">Dans ce cas, utilisez le port 1999 comme hello PostgreSQL port.</span><span class="sxs-lookup"><span data-stu-id="afc6e-112">In this case, use port 1999 as hello PostgreSQL port.</span></span>  

<span data-ttu-id="afc6e-113">Se connecter toohello VM Linux vous avez créé via PuTTY.</span><span class="sxs-lookup"><span data-stu-id="afc6e-113">Connect toohello Linux VM you created via PuTTY.</span></span> <span data-ttu-id="afc6e-114">S’il s’agit hello première fois que vous utilisez une machine virtuelle Linux de Azure, consultez [comment tooUse SSH avec Linux sur Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn comment toouse PuTTY tooconnect tooa Linux VM.</span><span class="sxs-lookup"><span data-stu-id="afc6e-114">If this is hello first time you're using an Azure Linux VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn how toouse PuTTY tooconnect tooa Linux VM.</span></span>

1. <span data-ttu-id="afc6e-115">Exécutez hello suivant racine de toohello commande tooswitch (admin) :</span><span class="sxs-lookup"><span data-stu-id="afc6e-115">Run hello following command tooswitch toohello root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="afc6e-116">Certaines distributions ont des dépendances à installer avant d’installer PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="afc6e-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="afc6e-117">Vérifiez pour votre distribution dans cette liste et exécutez la commande appropriée hello :</span><span class="sxs-lookup"><span data-stu-id="afc6e-117">Check for your distro in this list and run hello appropriate command:</span></span>
   
   * <span data-ttu-id="afc6e-118">Red Hat Linux :</span><span class="sxs-lookup"><span data-stu-id="afc6e-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="afc6e-119">Debian Linux :</span><span class="sxs-lookup"><span data-stu-id="afc6e-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="afc6e-120">SUSE Linux :</span><span class="sxs-lookup"><span data-stu-id="afc6e-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="afc6e-121">Télécharger PostgreSQL dans le répertoire racine de hello et puis décompressez le package de hello :</span><span class="sxs-lookup"><span data-stu-id="afc6e-121">Download PostgreSQL into hello root directory, and then unzip hello package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="afc6e-122">Hello ci-dessus est un exemple.</span><span class="sxs-lookup"><span data-stu-id="afc6e-122">hello above is an example.</span></span> <span data-ttu-id="afc6e-123">Vous pouvez trouver hello plus détaillées téléchargement adresse Bonjour [Indexde/pub/source/](https://ftp.postgresql.org/pub/source/).</span><span class="sxs-lookup"><span data-stu-id="afc6e-123">You can find hello more detailed download address in hello [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="afc6e-124">génération de hello toostart, exécutez ces commandes :</span><span class="sxs-lookup"><span data-stu-id="afc6e-124">toostart hello build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="afc6e-125">Si vous souhaitez toobuild tout ce qui peut être générée, y compris la documentation de hello (pages HTML et man) et les modules complémentaires (cotisation), exécuter la commande suivante à la place de hello :</span><span class="sxs-lookup"><span data-stu-id="afc6e-125">If  you want toobuild everything that can be built, including hello documentation (HTML and man pages) and additional modules (contrib), run hello following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="afc6e-126">Vous devez recevoir hello message de confirmation suivant :</span><span class="sxs-lookup"><span data-stu-id="afc6e-126">You should receive hello following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a><span data-ttu-id="afc6e-127">Configurer PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="afc6e-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="afc6e-128">(Facultatif) Créer un hello tooshorten de lien symbolique PostgreSQL référence toonot inclure le numéro de version hello :</span><span class="sxs-lookup"><span data-stu-id="afc6e-128">(Optional) Create a symbolic link tooshorten hello PostgreSQL reference toonot include hello version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="afc6e-129">Créez un répertoire de base de données hello :</span><span class="sxs-lookup"><span data-stu-id="afc6e-129">Create a directory for hello database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="afc6e-130">Créez un utilisateur non-root et modifiez le profil de cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="afc6e-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="afc6e-131">Ensuite, basculez toothis nouvel utilisateur (appelé *postgres* dans notre exemple) :</span><span class="sxs-lookup"><span data-stu-id="afc6e-131">Then, switch toothis new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="afc6e-132">Pour des raisons de sécurité, PostgreSQL utilise un tooinitialize utilisateur non racine, démarrer ou arrêter la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="afc6e-132">For security reasons, PostgreSQL uses a non-root user tooinitialize, start, or shut down hello database.</span></span>
   > 
   > 
4. <span data-ttu-id="afc6e-133">Modifier hello *bash_profile* fichier en entrant les commandes hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="afc6e-133">Edit hello *bash_profile* file by entering hello commands below.</span></span> <span data-ttu-id="afc6e-134">Ces lignes seront ajoutées fin toohello Hello *bash_profile* fichier :</span><span class="sxs-lookup"><span data-stu-id="afc6e-134">These lines will be added toohello end of hello *bash_profile* file:</span></span>
   
        cat >> ~/.bash_profile <<EOF
        export PGPORT=1999
        export PGDATA=/opt/pgsql_data
        export LANG=en_US.utf8
        export PGHOME=/opt/pgsql
        export PATH=\$PATH:\$PGHOME/bin
        export MANPATH=\$MANPATH:\$PGHOME/share/man
        export DATA=`date +"%Y%m%d%H%M"`
        export PGUSER=postgres
        alias rm='rm -i'
        alias ll='ls -lh'
        EOF
5. <span data-ttu-id="afc6e-135">Exécutez hello *bash_profile* fichier :</span><span class="sxs-lookup"><span data-stu-id="afc6e-135">Execute hello *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="afc6e-136">Valider votre installation à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="afc6e-136">Validate your installation by using hello following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="afc6e-137">Si votre installation est réussie, vous verrez hello suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="afc6e-137">If your installation is successful, you will see hello following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="afc6e-138">Vous pouvez également vérifier la version de PostgreSQL hello :</span><span class="sxs-lookup"><span data-stu-id="afc6e-138">You can also check hello PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="afc6e-139">Initialiser la base de données hello :</span><span class="sxs-lookup"><span data-stu-id="afc6e-139">Initialize hello database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="afc6e-140">Vous devez recevoir hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="afc6e-140">You should receive hello following output:</span></span>

![image](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="afc6e-142">Configurer PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="afc6e-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="afc6e-143">Exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="afc6e-143">Run hello following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="afc6e-144">Modifiez les deux variables dans le fichier de /etc/init.d/postgresql hello.</span><span class="sxs-lookup"><span data-stu-id="afc6e-144">Modify two variables in hello /etc/init.d/postgresql file.</span></span> <span data-ttu-id="afc6e-145">Hello préfixe a la valeur chemin d’installation de toohello de PostgreSQL : **pgsql/opt/**.</span><span class="sxs-lookup"><span data-stu-id="afc6e-145">hello prefix is set toohello installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="afc6e-146">PGDATA est défini de chemin d’accès de stockage de données toohello de PostgreSQL : **pgsql_data/opt/**.</span><span class="sxs-lookup"><span data-stu-id="afc6e-146">PGDATA is set toohello data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![image](./media/postgresql-install/no2.png)

<span data-ttu-id="afc6e-148">Modifier hello fichier toomake il exécutable :</span><span class="sxs-lookup"><span data-stu-id="afc6e-148">Change hello file toomake it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="afc6e-149">Démarrez PostgreSQL :</span><span class="sxs-lookup"><span data-stu-id="afc6e-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="afc6e-150">Vérifiez si le point de terminaison hello de PostgreSQL se trouve sur :</span><span class="sxs-lookup"><span data-stu-id="afc6e-150">Check if hello endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="afc6e-151">Vous devez voir hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="afc6e-151">You should see hello following output:</span></span>

![image](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a><span data-ttu-id="afc6e-153">Connexion de base de données Postgres toohello</span><span class="sxs-lookup"><span data-stu-id="afc6e-153">Connect toohello Postgres database</span></span>
<span data-ttu-id="afc6e-154">Basculer de nouveau toohello postgres utilisateur :</span><span class="sxs-lookup"><span data-stu-id="afc6e-154">Switch toohello postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="afc6e-155">Créez une base de données Postgres :</span><span class="sxs-lookup"><span data-stu-id="afc6e-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="afc6e-156">Se connecter toohello événements de base de données que vous venez de créer :</span><span class="sxs-lookup"><span data-stu-id="afc6e-156">Connect toohello events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="afc6e-157">Créer et supprimer une table Postgres</span><span class="sxs-lookup"><span data-stu-id="afc6e-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="afc6e-158">Maintenant que vous êtes connecté toohello de base de données, vous pouvez créer les tables qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="afc6e-158">Now that you have connected toohello database, you can create tables in it.</span></span>

<span data-ttu-id="afc6e-159">Par exemple, créer une nouvelle table de Postgres exemple à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="afc6e-159">For example, create a new example Postgres table by using hello following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="afc6e-160">Vous avez défini un tableau de quatre colonnes avec hello suivant des noms de colonnes et restrictions :</span><span class="sxs-lookup"><span data-stu-id="afc6e-160">You have now set up a four-column table with hello following column names and restrictions:</span></span>

1. <span data-ttu-id="afc6e-161">Hello « name » une colonne a été limitée par hello VARCHAR commande toobe sous 20 caractères.</span><span class="sxs-lookup"><span data-stu-id="afc6e-161">hello “name” column has been limited by hello VARCHAR command toobe under 20 characters long.</span></span>
2. <span data-ttu-id="afc6e-162">colonne de « produits alimentaires » Hello indique aliment hello chaque personne s’affiche.</span><span class="sxs-lookup"><span data-stu-id="afc6e-162">hello “food” column indicates hello food item that each person will bring.</span></span> <span data-ttu-id="afc6e-163">VARCHAR limite ce toobe texte sous 30 caractères.</span><span class="sxs-lookup"><span data-stu-id="afc6e-163">VARCHAR limits this text toobe under 30 characters.</span></span>
3. <span data-ttu-id="afc6e-164">Hello « confirmé « enregistrements de la colonne si personne de hello a auxquels elle répondu toohello buffet.</span><span class="sxs-lookup"><span data-stu-id="afc6e-164">hello “confirmed” column records whether hello person has RSVP’d toohello potluck.</span></span> <span data-ttu-id="afc6e-165">les valeurs acceptables Hello sont « Y » et « N ».</span><span class="sxs-lookup"><span data-stu-id="afc6e-165">hello acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="afc6e-166">affiche de colonne « date » de Hello lors de leur inscription pour l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="afc6e-166">hello “date” column shows when they signed up for hello event.</span></span> <span data-ttu-id="afc6e-167">Postgres requiert que les dates soient écrites au format aaaa-mm-jj.</span><span class="sxs-lookup"><span data-stu-id="afc6e-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="afc6e-168">Vous devez voir s’afficher hello si votre table a été créée avec succès :</span><span class="sxs-lookup"><span data-stu-id="afc6e-168">You should see hello following if your table has been successfully created:</span></span>

![image](./media/postgresql-install/no4.png)

<span data-ttu-id="afc6e-170">Vous pouvez également vérifier la structure de la table hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="afc6e-170">You can also check hello table structure by using hello following command:</span></span>

![image](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a><span data-ttu-id="afc6e-172">Ajouter la table de données tooa</span><span class="sxs-lookup"><span data-stu-id="afc6e-172">Add data tooa table</span></span>
<span data-ttu-id="afc6e-173">Insérez d’abord des informations dans une ligne :</span><span class="sxs-lookup"><span data-stu-id="afc6e-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="afc6e-174">Cette sortie doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="afc6e-174">You should see this output:</span></span>

![image](./media/postgresql-install/no6.png)

<span data-ttu-id="afc6e-176">Vous pouvez ajouter quelques plusieurs personnes toohello table également.</span><span class="sxs-lookup"><span data-stu-id="afc6e-176">You can add a couple more people toohello table as well.</span></span> <span data-ttu-id="afc6e-177">Voici quelques propositions, mais vous pouvez créer vos propres informations :</span><span class="sxs-lookup"><span data-stu-id="afc6e-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="afc6e-178">Afficher les tables</span><span class="sxs-lookup"><span data-stu-id="afc6e-178">Show tables</span></span>
<span data-ttu-id="afc6e-179">Hello suivant commande tooshow une table, utilisez :</span><span class="sxs-lookup"><span data-stu-id="afc6e-179">Use hello following command tooshow a table:</span></span>

    select * from potluck;

<span data-ttu-id="afc6e-180">sortie de Hello est :</span><span class="sxs-lookup"><span data-stu-id="afc6e-180">hello output is:</span></span>

![image](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="afc6e-182">Supprimer des données dans une table</span><span class="sxs-lookup"><span data-stu-id="afc6e-182">Delete data in a table</span></span>
<span data-ttu-id="afc6e-183">Utilisez hello données toodelete de commande dans une table suivantes :</span><span class="sxs-lookup"><span data-stu-id="afc6e-183">Use hello following command toodelete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="afc6e-184">Cette opération supprime toutes les informations de hello Bonjour ligne de « John ».</span><span class="sxs-lookup"><span data-stu-id="afc6e-184">This deletes all hello information in hello "John" row.</span></span> <span data-ttu-id="afc6e-185">sortie de Hello est :</span><span class="sxs-lookup"><span data-stu-id="afc6e-185">hello output is:</span></span>

![image](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="afc6e-187">Mettre à jour des données dans une table</span><span class="sxs-lookup"><span data-stu-id="afc6e-187">Update data in a table</span></span>
<span data-ttu-id="afc6e-188">Utilisez hello suivant données tooupdate de commande dans une table.</span><span class="sxs-lookup"><span data-stu-id="afc6e-188">Use hello following command tooupdate data in a table.</span></span> <span data-ttu-id="afc6e-189">Dans cet exemple, Sandy a confirmé qu’elle participe, donc nous allons changer son RSVP à partir de « N » trop « Y » :</span><span class="sxs-lookup"><span data-stu-id="afc6e-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" too"Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="afc6e-190">Obtenez davantage d’informations sur PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="afc6e-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="afc6e-191">Maintenant que vous avez terminé l’installation Bonjour de PostgreSQL dans une machine virtuelle Linux de Azure, vous pouvez profiter de l’utiliser dans Azure.</span><span class="sxs-lookup"><span data-stu-id="afc6e-191">Now that you have completed hello installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="afc6e-192">toolearn en savoir plus sur PostgreSQL, visitez hello [site Web de PostgreSQL](http://www.postgresql.org/).</span><span class="sxs-lookup"><span data-stu-id="afc6e-192">toolearn more about PostgreSQL, visit hello [PostgreSQL website](http://www.postgresql.org/).</span></span>

