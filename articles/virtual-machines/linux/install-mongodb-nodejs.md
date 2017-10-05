---
title: "Installer MongoDB sur une machine virtuelle Linux à l’aide d’Azure CLI 1.0 | Microsoft Docs"
description: "Découvrez comment installer et configurer MongoDB sur une machine virtuelle Linux dans Azure à l’aide du modèle de déploiement de Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: c97ade0a3d95824f723aad55776de861fe49441f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="0799d-103">Guide pratique d’installation et de configuration de MongoDB sur une machine virtuelle Linux avec Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0799d-103">How to install and configure MongoDB on a Linux VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="0799d-104">[MongoDB](http://www.mongodb.org) est une base de données NoSQL open-source qui offre des performances élevées.</span><span class="sxs-lookup"><span data-stu-id="0799d-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="0799d-105">Cet article vous montre comment installer et configurer MongoDB sur une machine virtuelle Linux dans Azure à l’aide du modèle de déploiement de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0799d-105">This article shows you how to install and configure MongoDB on a Linux VM in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="0799d-106">Présentations d’exemples détaillant comment :</span><span class="sxs-lookup"><span data-stu-id="0799d-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="0799d-107">Installer et configurer une instance MongoDB de base manuellement</span><span class="sxs-lookup"><span data-stu-id="0799d-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="0799d-108">Création d'une instance MongoDB de base à l'aide d'un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0799d-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="0799d-109">Créer un cluster partitionné MongoDB complexe avec jeux de réplicas à l’aide d’un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0799d-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="0799d-110">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="0799d-110">CLI versions to complete the task</span></span>
<span data-ttu-id="0799d-111">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="0799d-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="0799d-112">Azure CLI 1.0 : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="0799d-112">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="0799d-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) : notre interface de ligne de commande nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0799d-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="0799d-114">Installer et configurer MongoDB manuellement sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="0799d-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="0799d-115">MongoDB [propose des instructions d’installation](https://docs.mongodb.com/manual/administration/install-on-linux/) pour les distributions Linux, notamment Red Hat / CentOS, SUSE, Ubuntu et Debian.</span><span class="sxs-lookup"><span data-stu-id="0799d-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="0799d-116">L’exemple suivant crée une machine virtuelle *CentOS* à l’aide d’une clé SSH stockée sur *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="0799d-116">The following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="0799d-117">Répondez aux invites pour le nom de compte de stockage, le nom DNS et les informations d’identification d’administrateur :</span><span class="sxs-lookup"><span data-stu-id="0799d-117">Answer the prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="0799d-118">Connectez-vous à la machine virtuelle à l’aide de l’adresse IP publique affichée à la fin de l’étape de création de machine virtuelle précédente :</span><span class="sxs-lookup"><span data-stu-id="0799d-118">Log on to the VM using the public IP address displayed at the end of the preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="0799d-119">Pour ajouter les sources d’installation pour MongoDB, créez un fichier de référentiel **yum** comme suit :</span><span class="sxs-lookup"><span data-stu-id="0799d-119">To add the installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="0799d-120">Ouvrez le fichier de référentiel MongoDB à modifier.</span><span class="sxs-lookup"><span data-stu-id="0799d-120">Open the MongoDB repo file for editing.</span></span> <span data-ttu-id="0799d-121">Ajoutez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0799d-121">Add the following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="0799d-122">Installez MongoDB à l’aide de **yum** comme suit :</span><span class="sxs-lookup"><span data-stu-id="0799d-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="0799d-123">Par défaut, SELinux est appliqué sur les images CentOS, ce qui vous empêche d’accéder à MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0799d-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="0799d-124">Installez les outils de gestion de stratégie et configurez SELinux afin d’autoriser MongoDB fonctionner sur le port TCP 27017 par défaut, comme suit.</span><span class="sxs-lookup"><span data-stu-id="0799d-124">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="0799d-125">Démarrez le service MongoDB comme suit :</span><span class="sxs-lookup"><span data-stu-id="0799d-125">Start the MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="0799d-126">Vérifiez l’installation de MongoDB en vous connectant à l’aide du client `mongo` local :</span><span class="sxs-lookup"><span data-stu-id="0799d-126">Verify the MongoDB installation by connecting using the local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="0799d-127">Testez maintenant l’instance MongoDB en ajoutant des données, puis en recherchant :</span><span class="sxs-lookup"><span data-stu-id="0799d-127">Now test the MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="0799d-128">Si vous le souhaitez, configurez MongoDB pour démarrer automatiquement lors du redémarrage du système :</span><span class="sxs-lookup"><span data-stu-id="0799d-128">If desired, configure MongoDB to start automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="0799d-129">Créeation d’une instance MongoDB de base sur CentOS à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="0799d-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="0799d-130">Vous pouvez créer une instance MongoDB de base sur une machine virtuelle CentOS unique en utilisant le modèle de démarrage rapide Azure suivant à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="0799d-130">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="0799d-131">Ce modèle utilise l’extension de script personnalisé pour Linux pour ajouter un référentiel `yum` à votre nouvelle machine virtuelle CentOS, puis installer MongoDB.</span><span class="sxs-lookup"><span data-stu-id="0799d-131">This template uses the Custom Script extension for Linux to add a `yum` repository to your newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="0799d-132">[Instance MongoDB de base sur CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="0799d-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="0799d-133">L’exemple suivant crée un groupe de ressources nommé `myResourceGroup` dans la région `eastus`.</span><span class="sxs-lookup"><span data-stu-id="0799d-133">The following example creates a resource group with the name `myResourceGroup` in the `eastus` region.</span></span> <span data-ttu-id="0799d-134">Saisissez vos propres valeurs, comme suit :</span><span class="sxs-lookup"><span data-stu-id="0799d-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="0799d-135">L’interface de ligne de commande Azure vous renvoie à une invite quelques secondes après la création du déploiement, mais l’installation et la configuration prennent quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="0799d-135">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration takes a few minutes to complete.</span></span> <span data-ttu-id="0799d-136">Vérifiez l’état du déploiement avec `azure group deployment show myResourceGroup`, en saisissant le nom de votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0799d-136">Check the status of the deployment with `azure group deployment show myResourceGroup`, entering the name of your resource group accordingly.</span></span> <span data-ttu-id="0799d-137">Attendez que **ProvisioningState** (État d’approvisionnement) indique *Succeeded* (Opération réussie) avant d’essayer d’utiliser SSH pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0799d-137">Wait until the **ProvisioningState** shows *Succeeded* before trying to SSH to the VM.</span></span>

<span data-ttu-id="0799d-138">Une fois le déploiement terminé, connectez-vous par SSH à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0799d-138">Once the deployment is complete, SSH to the VM.</span></span> <span data-ttu-id="0799d-139">Obtenez l’adresse IP de votre machine virtuelle à l’aide de la commande `azure vm show` comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0799d-139">Obtain the IP address of your VM using the `azure vm show` command as in the following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="0799d-140">Vers la fin de la sortie, l’adresse IP publique s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0799d-140">Near the end of the output, the public IP address is displayed.</span></span> <span data-ttu-id="0799d-141">Connectez-vous par SSH à votre machine virtuelle avec l’adresse IP de votre machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="0799d-141">SSH to your VM with the IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="0799d-142">Vérifiez l’installation de MongoDB en vous connectant à l’aide du client `mongo` local, comme suit :</span><span class="sxs-lookup"><span data-stu-id="0799d-142">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="0799d-143">Testez maintenant l’instance en ajoutant des données, puis en recherchant comme suit :</span><span class="sxs-lookup"><span data-stu-id="0799d-143">Now test the instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="0799d-144">Création d’un cluster partitionné MongoDB complexe sur CentOS à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="0799d-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="0799d-145">Vous pouvez créer une instance MongoDB complexe sur un cluster partitionné en utilisant le modèle de démarrage rapide Azure suivant à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="0799d-145">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="0799d-146">Ce modèle suit les [meilleures pratiques pour les clusters partitionnés MongoDB](https://docs.mongodb.com/manual/core/sharded-cluster-components/) pour fournir la redondance et la haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="0799d-146">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span></span> <span data-ttu-id="0799d-147">Le modèle crée deux partitions, avec trois nœuds dans chaque jeu de réplicas.</span><span class="sxs-lookup"><span data-stu-id="0799d-147">The template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="0799d-148">Un jeu de réplicas de serveur de configuration avec trois nœuds est également créé, ainsi que deux serveurs de routeur **mongos** pour assurer la cohérence des applications au sein des partitions.</span><span class="sxs-lookup"><span data-stu-id="0799d-148">One config server replica set with three nodes is also created, plus two **mongos** router servers to provide consistency to applications from across the shards.</span></span>

* <span data-ttu-id="0799d-149">[Cluster de partitionnement MongoDB sur CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="0799d-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="0799d-150">Le déploiement de ce cluster partitionné MongoDB complexe requiert plus de 20 cœurs, ce qui est généralement le nombre de cœurs par défaut par région pour un abonnement.</span><span class="sxs-lookup"><span data-stu-id="0799d-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span></span> <span data-ttu-id="0799d-151">Ouvrez une demande de support Azure pour augmenter votre nombre de cœurs.</span><span class="sxs-lookup"><span data-stu-id="0799d-151">Open an Azure support request to increase your core count.</span></span>

<span data-ttu-id="0799d-152">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* dans la région *eastus*.</span><span class="sxs-lookup"><span data-stu-id="0799d-152">The following example creates a resource group with the name *myResourceGroup* in the *eastus* region.</span></span> <span data-ttu-id="0799d-153">Saisissez vos propres valeurs, comme suit :</span><span class="sxs-lookup"><span data-stu-id="0799d-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="0799d-154">L’interface de ligne de commande Azure vous renvoie à une invite quelques secondes après la création du déploiement, mais l’installation et la configuration peuvent prendre plus d’une heure.</span><span class="sxs-lookup"><span data-stu-id="0799d-154">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration can take over an hour to complete.</span></span> <span data-ttu-id="0799d-155">Vérifiez l’état du déploiement avec `azure group deployment show myResourceGroup`, en ajustant le nom de votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0799d-155">Check the status of the deployment with `azure group deployment show myResourceGroup`, adjusting the name of your resource group accordingly.</span></span> <span data-ttu-id="0799d-156">Attendez que **ProvisioningState** (État d’approvisionnement) indique *Succeeded* (Opération réussie) avant de vous connecter aux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="0799d-156">Wait until the **ProvisioningState** shows *Succeeded* before connecting to the VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0799d-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0799d-157">Next steps</span></span>
<span data-ttu-id="0799d-158">Dans ces exemples, vous vous connectez à l’instance MongoDB localement à partir de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0799d-158">In these examples, you connect to the MongoDB instance locally from the VM.</span></span> <span data-ttu-id="0799d-159">Si vous souhaitez vous connecter à l’instance MongoDB à partir d’une autre machine virtuelle ou d’un autre réseau, vérifiez que les bonnes [règles de groupe de sécurité réseau sont créées](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="0799d-159">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="0799d-160">Pour en savoir plus sur la création avec des modèles, voir [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0799d-160">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="0799d-161">Les modèles Azure Resource Manager utilisent l’extension de script personnalisé pour télécharger et exécuter des scripts sur vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="0799d-161">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span></span> <span data-ttu-id="0799d-162">Pour plus d’informations, consultez [Utilisation de l’extension de script personnalisé Azure avec des machines virtuelles Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="0799d-162">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

