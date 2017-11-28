---
title: Installer MongoDB sur une machine virtuelle Linux avec Azure CLI | Microsoft Docs
description: "Découvrez comment installer et configurer MongoDB sur une machine virtuelle Linux avec Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: e19c09558285497f29eb78b4f4ae5b15d7f1a191
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="fff30-103">Guide pratique d’installation et de configuration de MongoDB sur une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="fff30-103">How to install and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="fff30-104">[MongoDB](http://www.mongodb.org) est une base de données NoSQL open-source qui offre des performances élevées.</span><span class="sxs-lookup"><span data-stu-id="fff30-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="fff30-105">Cet article montre comment installer et configurer MongoDB sur une machine virtuelle Linux avec Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="fff30-105">This article shows you how to install and configure MongoDB on a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="fff30-106">Vous pouvez également suivre ces étapes avec [Azure CLI 1.0](install-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="fff30-106">You can also perform these steps with the [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="fff30-107">Présentations d’exemples détaillant comment :</span><span class="sxs-lookup"><span data-stu-id="fff30-107">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="fff30-108">Installer et configurer une instance MongoDB de base manuellement</span><span class="sxs-lookup"><span data-stu-id="fff30-108">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="fff30-109">Création d'une instance MongoDB de base à l'aide d'un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fff30-109">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="fff30-110">Créer un cluster partitionné MongoDB complexe avec jeux de réplicas à l’aide d’un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fff30-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="fff30-111">Installer et configurer MongoDB manuellement sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="fff30-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="fff30-112">MongoDB [propose des instructions d’installation](https://docs.mongodb.com/manual/administration/install-on-linux/) pour les distributions Linux, notamment Red Hat / CentOS, SUSE, Ubuntu et Debian.</span><span class="sxs-lookup"><span data-stu-id="fff30-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="fff30-113">L’exemple suivant permet de créer une machine virtuelle nommée *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="fff30-113">The following example creates a *CentOS* VM.</span></span> <span data-ttu-id="fff30-114">Pour créer cet environnement, la dernière version de l’interface [Azure CLI 2.0](/cli/azure/install-az-cli2) doit être installée et connectée à un compte Azure à l’aide de la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="fff30-114">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="fff30-115">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fff30-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fff30-116">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *eastus* :</span><span class="sxs-lookup"><span data-stu-id="fff30-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="fff30-117">Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fff30-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="fff30-118">L’exemple suivant crée une machine virtuelle nommée *myVM* avec un utilisateur nommé *azureuser* utilisant l’authentification par clé publique SSH</span><span class="sxs-lookup"><span data-stu-id="fff30-118">The following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="fff30-119">SSH à la machine virtuelle à l’aide de votre propre nom d’utilisateur et de l’`publicIpAddress` indiquée dans la sortie de l’étape précédente :</span><span class="sxs-lookup"><span data-stu-id="fff30-119">SSH to the VM using your own username and the `publicIpAddress` listed in the output from the previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="fff30-120">Pour ajouter les sources d’installation pour MongoDB, créez un fichier de référentiel **yum** comme suit :</span><span class="sxs-lookup"><span data-stu-id="fff30-120">To add the installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="fff30-121">Ouvrez le fichier de référentiel MongoDB à modifier.</span><span class="sxs-lookup"><span data-stu-id="fff30-121">Open the MongoDB repo file for editing.</span></span> <span data-ttu-id="fff30-122">Ajoutez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="fff30-122">Add the following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="fff30-123">Installez MongoDB à l’aide de **yum** comme suit :</span><span class="sxs-lookup"><span data-stu-id="fff30-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="fff30-124">Par défaut, SELinux est appliqué sur les images CentOS, ce qui vous empêche d’accéder à MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fff30-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="fff30-125">Installez les outils de gestion de stratégie et configurez SELinux afin d’autoriser MongoDB fonctionner sur le port TCP 27017 par défaut, comme suit :</span><span class="sxs-lookup"><span data-stu-id="fff30-125">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="fff30-126">Démarrez le service MongoDB comme suit :</span><span class="sxs-lookup"><span data-stu-id="fff30-126">Start the MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="fff30-127">Vérifiez l’installation de MongoDB en vous connectant à l’aide du client `mongo` local :</span><span class="sxs-lookup"><span data-stu-id="fff30-127">Verify the MongoDB installation by connecting using the local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="fff30-128">Testez maintenant l’instance MongoDB en ajoutant des données, puis en recherchant :</span><span class="sxs-lookup"><span data-stu-id="fff30-128">Now test the MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="fff30-129">Si vous le souhaitez, configurez MongoDB pour démarrer automatiquement lors du redémarrage du système :</span><span class="sxs-lookup"><span data-stu-id="fff30-129">If desired, configure MongoDB to start automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="fff30-130">Créeation d’une instance MongoDB de base sur CentOS à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="fff30-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="fff30-131">Vous pouvez créer une instance MongoDB de base sur une machine virtuelle CentOS unique en utilisant le modèle de démarrage rapide Azure suivant à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="fff30-131">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="fff30-132">Ce gabarit utilise l’extension de script personnalisé pour Linux pour ajouter un référentiel **yum** à votre nouvelle machine virtuelle CentOS, puis installer MongoDB.</span><span class="sxs-lookup"><span data-stu-id="fff30-132">This template uses the Custom Script extension for Linux to add a **yum** repository to your newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="fff30-133">[Instance MongoDB de base sur CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="fff30-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="fff30-134">Pour créer cet environnement, la dernière version de l’interface [Azure CLI 2.0](/cli/azure/install-az-cli2) doit être installée et connectée à un compte Azure à l’aide de la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="fff30-134">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="fff30-135">Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fff30-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fff30-136">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *eastus* :</span><span class="sxs-lookup"><span data-stu-id="fff30-136">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="fff30-137">Ensuite, déployez le modèle MongoDB avec [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="fff30-137">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="fff30-138">Définissez vos propres noms de ressources et tailles si nécessaire, comme par exemple pour *newStorageAccountName*, *virtualNetworkName* et *vmSize* :</span><span class="sxs-lookup"><span data-stu-id="fff30-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS2_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

<span data-ttu-id="fff30-139">Connectez-vous à la machine virtuelle avec l’adresse DNS publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fff30-139">Log on to the VM using the public DNS address of your VM.</span></span> <span data-ttu-id="fff30-140">Vous pouvez afficher l’adresse DNS publique avec [az vm show](/cli/azure/vm#show) :</span><span class="sxs-lookup"><span data-stu-id="fff30-140">You can view the public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="fff30-141">SSH vers votre machine virtuelle avec votre propre nom d’utilisateur et votre adresse DNS publique :</span><span class="sxs-lookup"><span data-stu-id="fff30-141">SSH to your VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="fff30-142">Vérifiez l’installation de MongoDB en vous connectant à l’aide du client `mongo` local, comme suit :</span><span class="sxs-lookup"><span data-stu-id="fff30-142">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="fff30-143">Testez maintenant l’instance en ajoutant des données, puis en recherchant comme suit :</span><span class="sxs-lookup"><span data-stu-id="fff30-143">Now test the instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="fff30-144">Création d’un cluster partitionné MongoDB complexe sur CentOS à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="fff30-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="fff30-145">Vous pouvez créer une instance MongoDB complexe sur un cluster partitionné en utilisant le modèle de démarrage rapide Azure suivant à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="fff30-145">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="fff30-146">Ce modèle suit les [meilleures pratiques pour les clusters partitionnés MongoDB](https://docs.mongodb.com/manual/core/sharded-cluster-components/) pour fournir la redondance et la haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="fff30-146">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span></span> <span data-ttu-id="fff30-147">Le modèle crée deux partitions, avec trois nœuds dans chaque jeu de réplicas.</span><span class="sxs-lookup"><span data-stu-id="fff30-147">The template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="fff30-148">Un jeu de réplicas de serveur de configuration avec trois nœuds est également créé, ainsi que deux serveurs de routeur **mongos** pour assurer la cohérence des applications au sein des partitions.</span><span class="sxs-lookup"><span data-stu-id="fff30-148">One config server replica set with three nodes is also created, plus two **mongos** router servers to provide consistency to applications from across the shards.</span></span>

* <span data-ttu-id="fff30-149">[Cluster de partitionnement MongoDB sur CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="fff30-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="fff30-150">Le déploiement de ce cluster partitionné MongoDB complexe requiert plus de 20 cœurs, ce qui est généralement le nombre de cœurs par défaut par région pour un abonnement.</span><span class="sxs-lookup"><span data-stu-id="fff30-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span></span> <span data-ttu-id="fff30-151">Ouvrez une demande de support Azure pour augmenter votre nombre de cœurs.</span><span class="sxs-lookup"><span data-stu-id="fff30-151">Open an Azure support request to increase your core count.</span></span>

<span data-ttu-id="fff30-152">Pour créer cet environnement, la dernière version de l’interface [Azure CLI 2.0](/cli/azure/install-az-cli2) doit être installée et connectée à un compte Azure à l’aide de la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="fff30-152">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="fff30-153">Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fff30-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fff30-154">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *eastus* :</span><span class="sxs-lookup"><span data-stu-id="fff30-154">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="fff30-155">Ensuite, déployez le modèle MongoDB avec [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="fff30-155">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="fff30-156">Définissez vos propres noms de ressources et tailles si nécessaire, comme par exemple pour *mongoAdminUsername*, *sizeOfDataDiskInGB* et *configNodeVmSize* :</span><span class="sxs-lookup"><span data-stu-id="fff30-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster \
  --no-wait
```

<span data-ttu-id="fff30-157">Ce déploiement peut nécessiter plus d’une heure pour déployer et configurer toutes les instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fff30-157">This deployment can take over an hour to deploy and configure all the VM instances.</span></span> <span data-ttu-id="fff30-158">L’indicateur `--no-wait` est utilisé à la fin de la commande précédente pour renvoyer le contrôle à l’invite de commandes une fois le déploiement du modèle accepté par la plateforme Azure.</span><span class="sxs-lookup"><span data-stu-id="fff30-158">The `--no-wait` flag is used at the end of the preceding command to return control to the command prompt once the template deployment has been accepted by the Azure platform.</span></span> <span data-ttu-id="fff30-159">Vous pouvez ensuite afficher l’état du déploiement avec [az group deployment show](/cli/azure/group/deployment#show).</span><span class="sxs-lookup"><span data-stu-id="fff30-159">You can then view the deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="fff30-160">L’exemple suivant vérifie l’état du déploiement de *myMongoDBCluster* dans le groupe de ressources *myResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="fff30-160">The following example views the status for the *myMongoDBCluster* deployment in the *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="fff30-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fff30-161">Next steps</span></span>
<span data-ttu-id="fff30-162">Dans ces exemples, vous vous connectez à l’instance MongoDB localement à partir de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fff30-162">In these examples, you connect to the MongoDB instance locally from the VM.</span></span> <span data-ttu-id="fff30-163">Si vous souhaitez vous connecter à l’instance MongoDB à partir d’une autre machine virtuelle ou d’un autre réseau, vérifiez que les bonnes [règles de groupe de sécurité réseau sont créées](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="fff30-163">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="fff30-164">Ces exemples montrent le déploiement de l’environnement MongoDB central à des fins de développement.</span><span class="sxs-lookup"><span data-stu-id="fff30-164">These examples deploy the core MongoDB environment for development purposes.</span></span> <span data-ttu-id="fff30-165">Appliquez les options de configuration de sécurité requises pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="fff30-165">Apply the required security configuration options for your environment.</span></span> <span data-ttu-id="fff30-166">Pour plus d’informations, voir les [documents relatifs à la sécurité de MongoDB](https://docs.mongodb.com/manual/security/).</span><span class="sxs-lookup"><span data-stu-id="fff30-166">For more information, see the [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="fff30-167">Pour en savoir plus sur la création avec des modèles, voir [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fff30-167">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="fff30-168">Les modèles Azure Resource Manager utilisent l’extension de script personnalisé pour télécharger et exécuter des scripts sur vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="fff30-168">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span></span> <span data-ttu-id="fff30-169">Pour plus d’informations, consultez [Utilisation de l’extension de script personnalisé Azure avec des machines virtuelles Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="fff30-169">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

