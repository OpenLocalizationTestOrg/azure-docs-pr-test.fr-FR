---
title: Installation de MongoDB sur une machine virtuelle Windows | Microsoft Docs
description: "Apprenez à installer MongoDB sur une machine virtuelle Azure fonctionnant sous Windows Server 2012 R2 créée avec le modèle de déploiement Resource Manager."
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
ms.openlocfilehash: db1a550b9273925b304fe4280f2a1b0e115f856d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="047b8-103">Installation et configuration de MongoDB sur une machine virtuelle Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="047b8-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="047b8-104">[MongoDB](http://www.mongodb.org) est une base de données NoSQL open-source qui offre des performances élevées.</span><span class="sxs-lookup"><span data-stu-id="047b8-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="047b8-105">Cet article vous guide lors de l’installation et de la configuration de MongoDB sur une machine virtuelle Windows Server 2012 R2 (VM) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="047b8-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="047b8-106">Vous pouvez également [installer MongoDB sur une machine virtuelle Linux dans Azure](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="047b8-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="047b8-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="047b8-107">Prerequisites</span></span>
<span data-ttu-id="047b8-108">Avant d’installer et configurer MongoDB, vous devez créer une machine virtuelle et, dans l’idéal, ajouter un disque de données à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="047b8-108">Before you install and configure MongoDB, you need to create a VM and, ideally, add a data disk to it.</span></span> <span data-ttu-id="047b8-109">Consultez les articles suivants pour créer une machine Virtuelle et ajouter un disque de données :</span><span class="sxs-lookup"><span data-stu-id="047b8-109">See the following articles to create a VM and add a data disk:</span></span>

* <span data-ttu-id="047b8-110">Création d’une machine virtuelle Windows Server à l’aide du [portail Azure](quick-create-portal.md) ou [d’Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="047b8-110">Create a Windows Server VM using [the Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="047b8-111">Association d’un disque de données à une machine virtuelle Windows Server à l’aide du [portail Azure](attach-managed-disk-portal.md) ou [d’Azure PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="047b8-111">Attach a data disk to a Windows Server VM using [the Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="047b8-112">Pour commencer à installer et à configurer MongoDB, [connectez-vous à votre machine virtuelle Windows Server](connect-logon.md) à l’aide du Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="047b8-112">To begin installing and configuring MongoDB, [log on to your Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="047b8-113">Installation de MongoDB</span><span class="sxs-lookup"><span data-stu-id="047b8-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="047b8-114">Les fonctionnalités de sécurité MongoDB, comme l’authentification et la liaison d’adresse IP, ne sont pas activées par défaut.</span><span class="sxs-lookup"><span data-stu-id="047b8-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="047b8-115">Elles doivent être activées avant le déploiement de MongoDB dans un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="047b8-115">Security features should be enabled before deploying MongoDB to a production environment.</span></span> <span data-ttu-id="047b8-116">Pour en savoir plus, consultez la page [Sécurité et authentification pour MongoDB](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="047b8-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="047b8-117">Une fois que vous êtes connecté à la machine virtuelle à l’aide du Bureau à distance, ouvrez Internet Explorer à partir du menu **Démarrer** sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="047b8-117">After you've connected to your VM using Remote Desktop, open Internet Explorer from the **Start** menu on the VM.</span></span>
2. <span data-ttu-id="047b8-118">Sélectionnez **Utiliser les paramètres de sécurité, de confidentialité et de compatibilité recommandés** lorsque s’ouvre pour la première fois, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="047b8-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="047b8-119">La configuration de la sécurité renforcée d’Internet Explorer est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="047b8-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="047b8-120">Ajoutez le site Web MongoDB à la liste des sites autorisés :</span><span class="sxs-lookup"><span data-stu-id="047b8-120">Add the MongoDB website to the list of allowed sites:</span></span>
   
   * <span data-ttu-id="047b8-121">Sélectionnez l’icône **Outils** dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="047b8-121">Select the **Tools** icon in the upper-right corner.</span></span>
   * <span data-ttu-id="047b8-122">Dans **Options Internet**, sélectionnez l’onglet **Sécurité**, puis l’icône **Sites de confiance**.</span><span class="sxs-lookup"><span data-stu-id="047b8-122">In **Internet Options**, select the **Security** tab, and then select the **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="047b8-123">Cliquez sur le bouton **Sites**.</span><span class="sxs-lookup"><span data-stu-id="047b8-123">Click the **Sites** button.</span></span> <span data-ttu-id="047b8-124">Ajoutez le site *https://\*.mongodb.org* à la liste des sites de confiance, et fermez la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="047b8-124">Add *https://\*.mongodb.org* to the list of trusted sites, and then close the dialog box.</span></span>
     
     ![Configuration des paramètres de sécurité Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="047b8-126">Accédez à la page [MongoDB - Téléchargements](http://www.mongodb.org/downloads) (http://www.mongodb.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="047b8-126">Browse to the [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="047b8-127">Si nécessaire, sélectionnez l’édition **Community Server** et la dernière version stable mise à jour pour Windows Server 2008 R2 64 bits et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="047b8-127">If needed, select the **Community Server** edition and then select the latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="047b8-128">Pour télécharger le programme d’installation, cliquez sur **TÉLÉCHARGER (msi)**.</span><span class="sxs-lookup"><span data-stu-id="047b8-128">To download the installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![Téléchargez le programme d’installation de MongoDB](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="047b8-130">Exécutez le programme d’installation une fois le téléchargement terminé.</span><span class="sxs-lookup"><span data-stu-id="047b8-130">Run the installer after the download is complete.</span></span>
6. <span data-ttu-id="047b8-131">Lisez et acceptez le contrat de licence.</span><span class="sxs-lookup"><span data-stu-id="047b8-131">Read and accept the license agreement.</span></span> <span data-ttu-id="047b8-132">Lorsqu’une invite s’affiche, sélectionnez **Terminer** le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="047b8-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="047b8-133">Sur le dernier écran, cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="047b8-133">On the final screen, click **Install**.</span></span>

## <a name="configure-the-vm-and-mongodb"></a><span data-ttu-id="047b8-134">Configuration de la machine virtuelle et de MongoDB</span><span class="sxs-lookup"><span data-stu-id="047b8-134">Configure the VM and MongoDB</span></span>
1. <span data-ttu-id="047b8-135">Les variables de chemin d’accès ne sont pas mises à jour par le programme d’installation de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="047b8-135">The path variables are not updated by the MongoDB installer.</span></span> <span data-ttu-id="047b8-136">Sans l’emplacement `bin` de MongoDB dans votre variable PATH, vous devez spécifier le chemin d’accès complet à chaque fois que vous utilisez un fichier exécutable MongoDB.</span><span class="sxs-lookup"><span data-stu-id="047b8-136">Without the MongoDB `bin` location in your path variable, you need to specify the full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="047b8-137">Pour ajouter l’emplacement à votre variable PATH :</span><span class="sxs-lookup"><span data-stu-id="047b8-137">To add the location to your path variable:</span></span>
   
   * <span data-ttu-id="047b8-138">Avec le bouton droit, cliquez sur le menu **Démarrer** et sélectionnez **Système**.</span><span class="sxs-lookup"><span data-stu-id="047b8-138">Right-click the **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="047b8-139">Cliquez sur **Paramètres système avancés**, puis cliquez sur **Variables d’environnement**.</span><span class="sxs-lookup"><span data-stu-id="047b8-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="047b8-140">Sous **Variables système**, sélectionnez **Chemin d’accès**, puis cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="047b8-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Configurez les variables PATH](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="047b8-142">Ajoutez le chemin d’accès vers le dossier `bin` de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="047b8-142">Add the path to your MongoDB `bin` folder.</span></span> <span data-ttu-id="047b8-143">MongoDB est généralement installé sur *C:\Program Files\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="047b8-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="047b8-144">Vérifiez le chemin d’installation sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="047b8-144">Verify the installation path on your VM.</span></span> <span data-ttu-id="047b8-145">L’exemple suivant ajoute la valeur par défaut d’emplacement d’installation de MongoDB la variable `PATH` :</span><span class="sxs-lookup"><span data-stu-id="047b8-145">The following example adds the default MongoDB install location to the `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="047b8-146">Veillez à ajouter le point-virgule en premier (`;`) pour indiquer que vous ajoutez un emplacement pour votre variable `PATH`.</span><span class="sxs-lookup"><span data-stu-id="047b8-146">Be sure to add the leading semicolon (`;`) to indicate that you are adding a location to your `PATH` variable.</span></span>

2. <span data-ttu-id="047b8-147">Créez les répertoires de journaux et de données MongoDB sur votre disque dur.</span><span class="sxs-lookup"><span data-stu-id="047b8-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="047b8-148">Dans le menu **Démarrer**, sélectionnez **Invite de commande**.</span><span class="sxs-lookup"><span data-stu-id="047b8-148">From the **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="047b8-149">L’exemple suivant crée les répertoires sur le lecteur F:</span><span class="sxs-lookup"><span data-stu-id="047b8-149">The following examples create the directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="047b8-150">Démarrez une instance MongoDB avec la commande suivante, en adaptant le chemin d’accès à vos données et journaux :</span><span class="sxs-lookup"><span data-stu-id="047b8-150">Start a MongoDB instance with the following command, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="047b8-151">Il se peut que plusieurs minutes soient nécessaires pour que MongaDB alloue les fichiers journaux et commence à écouter les connexions.</span><span class="sxs-lookup"><span data-stu-id="047b8-151">It may take several minutes for MongoDB to allocate the journal files and start listening for connections.</span></span> <span data-ttu-id="047b8-152">Tous les messages du journal sont dirigés vers le fichier *F:\MongoLogs\mongolog.log* lorsque le serveur `mongod.exe` démarre et alloue les fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="047b8-152">All log messages are directed to the *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="047b8-153">L’invite de commandes reste axée sur cette tâche pendant que votre instance MongoDB est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="047b8-153">The command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="047b8-154">Laissez la fenêtre d’invite de commandes ouverte pour poursuivre l’exécution de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="047b8-154">Leave the command prompt window open to continue running MongoDB.</span></span> <span data-ttu-id="047b8-155">Vous pouvez aussi installer MongoDB en tant que service, comme indiqué dans l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="047b8-155">Or, install MongoDB as service, as detailed in the next step.</span></span>

4. <span data-ttu-id="047b8-156">Pour une expérience plus robuste avec MongoDB, installez `mongod.exe` en tant que service.</span><span class="sxs-lookup"><span data-stu-id="047b8-156">For a more robust MongoDB experience, install the `mongod.exe` as a service.</span></span> <span data-ttu-id="047b8-157">La création d’un service signifie que vous n’avez pas besoin de laisser une invite de commande s’exécuter chaque fois que vous souhaitez utiliser MongoDB.</span><span class="sxs-lookup"><span data-stu-id="047b8-157">Creating a service means you don't need to leave a command prompt running each time you want to use MongoDB.</span></span> <span data-ttu-id="047b8-158">Créez le service en procédant comme suit, en adaptant le chemin d’accès à vos répertoires de données et de journaux :</span><span class="sxs-lookup"><span data-stu-id="047b8-158">Create the service as follows, adjusting the path to your data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="047b8-159">La commande précédente crée un service nommé « MongoDB » avec « Mongo DB » comme description.</span><span class="sxs-lookup"><span data-stu-id="047b8-159">The preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="047b8-160">Les paramètres suivants sont également spécifiés :</span><span class="sxs-lookup"><span data-stu-id="047b8-160">The following parameters are also specified:</span></span>
   
   * <span data-ttu-id="047b8-161">L’option `--dbpath` spécifie l’emplacement du répertoire de données.</span><span class="sxs-lookup"><span data-stu-id="047b8-161">The `--dbpath` option specifies the location of the data directory.</span></span>
   * <span data-ttu-id="047b8-162">L’option `--logpath` permet de spécifier un fichier journal puisque le service en cours d’exécution n’a pas de fenêtre de commande pour afficher la sortie.</span><span class="sxs-lookup"><span data-stu-id="047b8-162">The `--logpath` option must be used to specify a log file, because the running service does not have a command window to display output.</span></span>
   * <span data-ttu-id="047b8-163">L’option `--logappend` spécifie qu’au redémarrage du service, la sortie est ajoutée au fichier journal existant.</span><span class="sxs-lookup"><span data-stu-id="047b8-163">The `--logappend` option specifies that a restart of the service causes output to append to the existing log file.</span></span>
   
   <span data-ttu-id="047b8-164">Pour démarrer le service MongoDB, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="047b8-164">To start the MongoDB service, run the following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="047b8-165">Pour plus d’informations sur la création du service MongoDB, consultez [Configuration d’un service Windows pour MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="047b8-165">For more information about creating the MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-the-mongodb-instance"></a><span data-ttu-id="047b8-166">Testez l’instance de MongoDB</span><span class="sxs-lookup"><span data-stu-id="047b8-166">Test the MongoDB instance</span></span>
<span data-ttu-id="047b8-167">Avec MongoDB lancé en tant qu’instance unique ou installé en tant que service, vous pouvez maintenant commencer la création et l’utilisation de vos bases de données.</span><span class="sxs-lookup"><span data-stu-id="047b8-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="047b8-168">Pour lancer l’interpréteur de commandes d’administration de MongoDB, ouvrez une autre fenêtre d’invite de commande à partir du menu **Démarrer** et entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="047b8-168">To start the MongoDB administrative shell, open another command prompt window from the **Start** menu, and enter the following command:</span></span>

```
mongo  
```

<span data-ttu-id="047b8-169">Vous pouvez répertorier les bases de données avec la commande `db`.</span><span class="sxs-lookup"><span data-stu-id="047b8-169">You can list the databases with the `db` command.</span></span> <span data-ttu-id="047b8-170">Insérez des données comme suit :</span><span class="sxs-lookup"><span data-stu-id="047b8-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="047b8-171">Recherchez des données comme suit :</span><span class="sxs-lookup"><span data-stu-id="047b8-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="047b8-172">Le résultat ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="047b8-172">The output is similar to the following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="047b8-173">Quittez la console `mongo` comme suit :</span><span class="sxs-lookup"><span data-stu-id="047b8-173">Exit the `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="047b8-174">Configuration des règles de pare-feu et de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="047b8-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="047b8-175">Maintenant que MongoDB est installé et en cours d’exécution, ouvrez un port dans le Pare-feu Windows pour vous connecter à distance à MongoDB.</span><span class="sxs-lookup"><span data-stu-id="047b8-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect to MongoDB.</span></span> <span data-ttu-id="047b8-176">Pour créer une nouvelle règle de trafic entrant pour autoriser le port TCP 27017, ouvrez une invite PowerShell administrative et saisissez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="047b8-176">To create a new inbound rule to allow TCP port 27017, open an administrative PowerShell prompt and enter the following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="047b8-177">Vous pouvez également créer la règle à l’aide de l’outil de gestion graphique **Pare-feu Windows avec fonctions de sécurité avancées**.</span><span class="sxs-lookup"><span data-stu-id="047b8-177">You can also create the rule by using the **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="047b8-178">Créez une nouvelle règle de trafic entrant pour autoriser le port TCP 27017.</span><span class="sxs-lookup"><span data-stu-id="047b8-178">Create a new inbound rule to allow TCP port 27017.</span></span>

<span data-ttu-id="047b8-179">Si nécessaire, créez une règle de groupe de sécurité réseau pour autoriser l’accès à MongoDB en dehors du sous-réseau du réseau virtuel Azure existant.</span><span class="sxs-lookup"><span data-stu-id="047b8-179">If needed, create a Network Security Group rule to allow access to MongoDB from outside of the existing Azure virtual network subnet.</span></span> <span data-ttu-id="047b8-180">Vous pouvez créer les règles du groupe de sécurité réseau à l’aide du [portail Azure](nsg-quickstart-portal.md) ou [d’Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="047b8-180">You can create the Network Security Group rules by using the [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="047b8-181">Comme avec les règles de pare-feu Windows, autorisez le port TCP 27017 pour l’interface réseau virtuelle de votre machine virtuelle MongoDB.</span><span class="sxs-lookup"><span data-stu-id="047b8-181">As with the Windows Firewall rules, allow TCP port 27017 to the virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="047b8-182">Le port TCP 27017 est le port par défaut utilisé par MongoDB.</span><span class="sxs-lookup"><span data-stu-id="047b8-182">TCP port 27017 is the default port used by MongoDB.</span></span> <span data-ttu-id="047b8-183">Vous pouvez modifier ce port à l’aide du paramètre `--port` lors du démarrage de `mongod.exe`, manuellement ou à partir d’un service.</span><span class="sxs-lookup"><span data-stu-id="047b8-183">You can change this port by using the `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="047b8-184">Si vous modifiez le port, veillez à mettre à jour les règles de pare-feu Windows et le groupe de sécurité réseau dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="047b8-184">If you change the port, make sure to update the Windows Firewall and Network Security Group rules in the preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="047b8-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="047b8-185">Next steps</span></span>
<span data-ttu-id="047b8-186">Dans ce didacticiel, vous avez appris à installer et à configurer MongoDB sur votre machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="047b8-186">In this tutorial, you learned how to install and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="047b8-187">Vous pouvez maintenant accéder à MongoDB sur votre machine virtuelle Windows en suivant les rubriques avancées dans la [Documentation MongoDB](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="047b8-187">You can now access MongoDB on your Windows VM, by following the advanced topics in the [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

