---
title: aaaInstall MongoDB sur un ordinateur virtuel Windows Azure | Documents Microsoft
description: "Découvrez comment tooinstall MongoDB sur une machine virtuelle de Azure exécutant Windows Server 2012 R2 est créé avec le modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="d7aad-103">Installation et configuration de MongoDB sur une machine virtuelle Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="d7aad-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="d7aad-104">[MongoDB](http://www.mongodb.org) est une base de données NoSQL open-source qui offre des performances élevées.</span><span class="sxs-lookup"><span data-stu-id="d7aad-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="d7aad-105">Cet article vous guide lors de l’installation et de la configuration de MongoDB sur une machine virtuelle Windows Server 2012 R2 (VM) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d7aad-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="d7aad-106">Vous pouvez également [installer MongoDB sur une machine virtuelle Linux dans Azure](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="d7aad-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7aad-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d7aad-107">Prerequisites</span></span>
<span data-ttu-id="d7aad-108">Avant d’installer et configurer MongoDB, vous devez toocreate une machine virtuelle et, dans l’idéal, ajoutez un tooit de disque de données.</span><span class="sxs-lookup"><span data-stu-id="d7aad-108">Before you install and configure MongoDB, you need toocreate a VM and, ideally, add a data disk tooit.</span></span> <span data-ttu-id="d7aad-109">Consultez hello suivant articles toocreate une machine virtuelle et ajoutez un disque de données :</span><span class="sxs-lookup"><span data-stu-id="d7aad-109">See hello following articles toocreate a VM and add a data disk:</span></span>

* <span data-ttu-id="d7aad-110">Créer une machine virtuelle Windows Server à l’aide de [hello portail Azure](quick-create-portal.md) ou [Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d7aad-110">Create a Windows Server VM using [hello Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="d7aad-111">Joindre des données disque tooa machine virtuelle Windows Server avec [hello portail Azure](attach-managed-disk-portal.md) ou [Azure PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d7aad-111">Attach a data disk tooa Windows Server VM using [hello Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="d7aad-112">toobegin installation et configuration MongoDB, [session tooyour machine virtuelle Windows Server](connect-logon.md) à l’aide du Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="d7aad-112">toobegin installing and configuring MongoDB, [log on tooyour Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="d7aad-113">Installation de MongoDB</span><span class="sxs-lookup"><span data-stu-id="d7aad-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d7aad-114">Les fonctionnalités de sécurité MongoDB, comme l’authentification et la liaison d’adresse IP, ne sont pas activées par défaut.</span><span class="sxs-lookup"><span data-stu-id="d7aad-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="d7aad-115">Les fonctionnalités de sécurité doivent être activées avant de déployer l’environnement de production tooa MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d7aad-115">Security features should be enabled before deploying MongoDB tooa production environment.</span></span> <span data-ttu-id="d7aad-116">Pour en savoir plus, consultez la page [Sécurité et authentification pour MongoDB](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="d7aad-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="d7aad-117">Une fois que vous avez connecté tooyour machine virtuelle en utilisant Bureau à distance, ouvrez Internet Explorer à partir de hello **Démarrer** menu hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d7aad-117">After you've connected tooyour VM using Remote Desktop, open Internet Explorer from hello **Start** menu on hello VM.</span></span>
2. <span data-ttu-id="d7aad-118">Sélectionnez **Utiliser les paramètres de sécurité, de confidentialité et de compatibilité recommandés** lorsque s’ouvre pour la première fois, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7aad-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="d7aad-119">La configuration de la sécurité renforcée d’Internet Explorer est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="d7aad-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="d7aad-120">Ajoutez hello MongoDB site Web toohello liste des sites autorisés :</span><span class="sxs-lookup"><span data-stu-id="d7aad-120">Add hello MongoDB website toohello list of allowed sites:</span></span>
   
   * <span data-ttu-id="d7aad-121">Sélectionnez hello **outils** icône dans le coin supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="d7aad-121">Select hello **Tools** icon in hello upper-right corner.</span></span>
   * <span data-ttu-id="d7aad-122">Dans **Options Internet**, sélectionnez hello **sécurité** onglet et sélectionnez hello **Sites de confiance** icône.</span><span class="sxs-lookup"><span data-stu-id="d7aad-122">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="d7aad-123">Cliquez sur hello **Sites** bouton.</span><span class="sxs-lookup"><span data-stu-id="d7aad-123">Click hello **Sites** button.</span></span> <span data-ttu-id="d7aad-124">Ajouter *https://\*. mongodb.org* toohello liste des sites de confiance, boîte de dialogue Fermer puis hello.</span><span class="sxs-lookup"><span data-stu-id="d7aad-124">Add *https://\*.mongodb.org* toohello list of trusted sites, and then close hello dialog box.</span></span>
     
     ![Configuration des paramètres de sécurité Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="d7aad-126">Parcourir toohello [MongoDB - téléchargements](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="d7aad-126">Browse toohello [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="d7aad-127">Si nécessaire, sélectionnez hello **serveur de la Communauté** edition et hello puis sélectionnez dernière stable version actuelle de Windows Server 2008 R2 64 bits et les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="d7aad-127">If needed, select hello **Community Server** edition and then select hello latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="d7aad-128">toodownload hello du programme d’installation, cliquez sur **téléchargement (msi)**.</span><span class="sxs-lookup"><span data-stu-id="d7aad-128">toodownload hello installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![Téléchargez le programme d’installation de MongoDB](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="d7aad-130">Exécuter le programme d’installation hello après que hello téléchargement est terminé.</span><span class="sxs-lookup"><span data-stu-id="d7aad-130">Run hello installer after hello download is complete.</span></span>
6. <span data-ttu-id="d7aad-131">Lisez et acceptez le contrat de licence hello.</span><span class="sxs-lookup"><span data-stu-id="d7aad-131">Read and accept hello license agreement.</span></span> <span data-ttu-id="d7aad-132">Lorsqu’une invite s’affiche, sélectionnez **Terminer** le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="d7aad-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="d7aad-133">Dans l’écran final de hello, cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="d7aad-133">On hello final screen, click **Install**.</span></span>

## <a name="configure-hello-vm-and-mongodb"></a><span data-ttu-id="d7aad-134">Configurer hello VM et MongoDB</span><span class="sxs-lookup"><span data-stu-id="d7aad-134">Configure hello VM and MongoDB</span></span>
1. <span data-ttu-id="d7aad-135">variables de chemin d’accès Hello ne sont pas mis à jour par le programme d’installation de hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d7aad-135">hello path variables are not updated by hello MongoDB installer.</span></span> <span data-ttu-id="d7aad-136">Sans hello MongoDB `bin` emplacement dans votre variable de chemin d’accès, vous devez chemin d’accès complet de toospecify hello chaque fois que vous utilisez un fichier exécutable MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d7aad-136">Without hello MongoDB `bin` location in your path variable, you need toospecify hello full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="d7aad-137">variable de chemin d’accès tooyour tooadd hello emplacement :</span><span class="sxs-lookup"><span data-stu-id="d7aad-137">tooadd hello location tooyour path variable:</span></span>
   
   * <span data-ttu-id="d7aad-138">Avec le bouton hello **Démarrer** , puis sélectionnez **système**.</span><span class="sxs-lookup"><span data-stu-id="d7aad-138">Right-click hello **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="d7aad-139">Cliquez sur **Paramètres système avancés**, puis cliquez sur **Variables d’environnement**.</span><span class="sxs-lookup"><span data-stu-id="d7aad-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="d7aad-140">Sous **Variables système**, sélectionnez **Chemin d’accès**, puis cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="d7aad-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Configurez les variables PATH](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="d7aad-142">Ajouter le chemin d’accès de hello tooyour MongoDB `bin` dossier.</span><span class="sxs-lookup"><span data-stu-id="d7aad-142">Add hello path tooyour MongoDB `bin` folder.</span></span> <span data-ttu-id="d7aad-143">MongoDB est généralement installé sur *C:\Program Files\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="d7aad-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="d7aad-144">Vérifiez le chemin d’installation de hello sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d7aad-144">Verify hello installation path on your VM.</span></span> <span data-ttu-id="d7aad-145">exemple Hello ajoute hello par défaut MongoDB installation emplacement toohello `PATH` variable :</span><span class="sxs-lookup"><span data-stu-id="d7aad-145">hello following example adds hello default MongoDB install location toohello `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="d7aad-146">Être vraiment tooadd hello début point-virgule (`;`) tooindicate que vous ajoutez un emplacement tooyour `PATH` variable.</span><span class="sxs-lookup"><span data-stu-id="d7aad-146">Be sure tooadd hello leading semicolon (`;`) tooindicate that you are adding a location tooyour `PATH` variable.</span></span>

2. <span data-ttu-id="d7aad-147">Créez les répertoires de journaux et de données MongoDB sur votre disque dur.</span><span class="sxs-lookup"><span data-stu-id="d7aad-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="d7aad-148">À partir de hello **Démarrer** menu, sélectionnez **invite de commandes**.</span><span class="sxs-lookup"><span data-stu-id="d7aad-148">From hello **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="d7aad-149">Hello exemple suivant créer les répertoires hello sur le lecteur F:</span><span class="sxs-lookup"><span data-stu-id="d7aad-149">hello following examples create hello directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="d7aad-150">Démarrer une instance de MongoDB avec hello commande suivante, l’ajustement des données de tooyour hello chemin d’accès et des journaux en conséquence :</span><span class="sxs-lookup"><span data-stu-id="d7aad-150">Start a MongoDB instance with hello following command, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="d7aad-151">Il peut prendre plusieurs minutes MongoDB tooallocate les fichiers de journal hello et commence à écouter les connexions.</span><span class="sxs-lookup"><span data-stu-id="d7aad-151">It may take several minutes for MongoDB tooallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="d7aad-152">Tous les messages du journal sont suggéré toohello *F:\MongoLogs\mongolog.log* de fichiers `mongod.exe` serveur démarre et alloue des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="d7aad-152">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d7aad-153">invite de commandes Hello reste se concentrent sur cette tâche pendant l’exécution de votre instance de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d7aad-153">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="d7aad-154">Laissez ouverte toocontinue hello invite de commandes fenêtre MongoDB en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d7aad-154">Leave hello command prompt window open toocontinue running MongoDB.</span></span> <span data-ttu-id="d7aad-155">Ou bien, installez MongoDB en tant que service, comme indiqué dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d7aad-155">Or, install MongoDB as service, as detailed in hello next step.</span></span>

4. <span data-ttu-id="d7aad-156">Pour une expérience MongoDB plus robuste, installez hello `mongod.exe` en tant que service.</span><span class="sxs-lookup"><span data-stu-id="d7aad-156">For a more robust MongoDB experience, install hello `mongod.exe` as a service.</span></span> <span data-ttu-id="d7aad-157">Création d’un service signifie que vous n’avez pas besoin tooleave une invite de commandes en cours d’exécution chaque fois que vous toouse MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d7aad-157">Creating a service means you don't need tooleave a command prompt running each time you want toouse MongoDB.</span></span> <span data-ttu-id="d7aad-158">Créez le service de hello comme suit, ajustement hello données tooyour de chemin d’accès et des journaux en conséquence :</span><span class="sxs-lookup"><span data-stu-id="d7aad-158">Create hello service as follows, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="d7aad-159">Hello commande précédente crée un service nommé MongoDB, avec une description de « Mongodb ».</span><span class="sxs-lookup"><span data-stu-id="d7aad-159">hello preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="d7aad-160">Hello paramètres suivants est également spécifiée :</span><span class="sxs-lookup"><span data-stu-id="d7aad-160">hello following parameters are also specified:</span></span>
   
   * <span data-ttu-id="d7aad-161">Hello `--dbpath` option spécifie l’emplacement de hello hello du répertoire de données.</span><span class="sxs-lookup"><span data-stu-id="d7aad-161">hello `--dbpath` option specifies hello location of hello data directory.</span></span>
   * <span data-ttu-id="d7aad-162">Hello `--logpath` option doit être toospecify utilisé un fichier journal, car le service en cours d’exécution de hello n’a pas une sortie toodisplay de la fenêtre commande.</span><span class="sxs-lookup"><span data-stu-id="d7aad-162">hello `--logpath` option must be used toospecify a log file, because hello running service does not have a command window toodisplay output.</span></span>
   * <span data-ttu-id="d7aad-163">Hello `--logappend` option spécifie qu’un redémarrage du service de hello, le fichier journal existant de sortie tooappend toohello.</span><span class="sxs-lookup"><span data-stu-id="d7aad-163">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>
   
   <span data-ttu-id="d7aad-164">service de MongoDB hello toostart, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d7aad-164">toostart hello MongoDB service, run hello following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="d7aad-165">Pour plus d’informations sur la création du service de MongoDB hello, consultez [configurer un Service Windows pour MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="d7aad-165">For more information about creating hello MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-hello-mongodb-instance"></a><span data-ttu-id="d7aad-166">Instance de test hello MongoDB</span><span class="sxs-lookup"><span data-stu-id="d7aad-166">Test hello MongoDB instance</span></span>
<span data-ttu-id="d7aad-167">Avec MongoDB lancé en tant qu’instance unique ou installé en tant que service, vous pouvez maintenant commencer la création et l’utilisation de vos bases de données.</span><span class="sxs-lookup"><span data-stu-id="d7aad-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="d7aad-168">toostart hello MongoDB interpréteur de commandes d’administration, ouvrez une autre fenêtre d’invite de commandes à partir de hello **Démarrer** menu, puis entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d7aad-168">toostart hello MongoDB administrative shell, open another command prompt window from hello **Start** menu, and enter hello following command:</span></span>

```
mongo  
```

<span data-ttu-id="d7aad-169">Vous pouvez répertorier les bases de données hello hello `db` commande.</span><span class="sxs-lookup"><span data-stu-id="d7aad-169">You can list hello databases with hello `db` command.</span></span> <span data-ttu-id="d7aad-170">Insérez des données comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7aad-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="d7aad-171">Recherchez des données comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7aad-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="d7aad-172">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d7aad-172">hello output is similar toohello following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="d7aad-173">Hello de sortie `mongo` console comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7aad-173">Exit hello `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="d7aad-174">Configuration des règles de pare-feu et de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="d7aad-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="d7aad-175">Maintenant que MongoDB est installé et en cours d’exécution, ouvrir un port dans le pare-feu Windows pour vous connecter à distance tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="d7aad-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span> <span data-ttu-id="d7aad-176">toocreate un nouvelle règle de trafic entrant tooallow le port TCP 27017, ouvrez une invite PowerShell d’administration, puis entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d7aad-176">toocreate a new inbound rule tooallow TCP port 27017, open an administrative PowerShell prompt and enter hello following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="d7aad-177">Vous pouvez également créer des règles de hello à l’aide de hello **pare-feu Windows avec fonctions avancées de sécurité** outil de gestion graphique.</span><span class="sxs-lookup"><span data-stu-id="d7aad-177">You can also create hello rule by using hello **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="d7aad-178">Créer un nouvelle règle de trafic entrant tooallow le port TCP 27017.</span><span class="sxs-lookup"><span data-stu-id="d7aad-178">Create a new inbound rule tooallow TCP port 27017.</span></span>

<span data-ttu-id="d7aad-179">Si nécessaire, créez un groupe de sécurité réseau règle tooallow accès tooMongoDB d’en dehors du sous-réseau de réseau virtuel Azure existant hello.</span><span class="sxs-lookup"><span data-stu-id="d7aad-179">If needed, create a Network Security Group rule tooallow access tooMongoDB from outside of hello existing Azure virtual network subnet.</span></span> <span data-ttu-id="d7aad-180">Vous pouvez créer des règles du groupe de sécurité réseau de hello à l’aide de hello [portail Azure](nsg-quickstart-portal.md) ou [Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d7aad-180">You can create hello Network Security Group rules by using hello [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="d7aad-181">Comme avec les règles de pare-feu Windows hello, autoriser l’interface de réseau virtuel TCP port 27017 toohello de votre VM MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d7aad-181">As with hello Windows Firewall rules, allow TCP port 27017 toohello virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="d7aad-182">Le port TCP 27017 est le port par défaut de hello utilisé par MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d7aad-182">TCP port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="d7aad-183">Vous pouvez modifier ce port à l’aide de hello `--port` lors du démarrage de paramètre `mongod.exe` manuellement ou à partir d’un service.</span><span class="sxs-lookup"><span data-stu-id="d7aad-183">You can change this port by using hello `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="d7aad-184">Si vous modifiez le port de hello, rendre que tooupdate hello pare-feu Windows et le groupe de sécurité réseau règles Bonjour étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="d7aad-184">If you change hello port, make sure tooupdate hello Windows Firewall and Network Security Group rules in hello preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d7aad-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d7aad-185">Next steps</span></span>
<span data-ttu-id="d7aad-186">Dans ce didacticiel, vous avez appris comment tooinstall et configurer MongoDB sur votre machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="d7aad-186">In this tutorial, you learned how tooinstall and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="d7aad-187">Vous pouvez désormais accéder aux MongoDB sur votre machine virtuelle Windows, en suivant hello rubriques Bonjour avancées [documentation MongoDB](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="d7aad-187">You can now access MongoDB on your Windows VM, by following hello advanced topics in hello [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

