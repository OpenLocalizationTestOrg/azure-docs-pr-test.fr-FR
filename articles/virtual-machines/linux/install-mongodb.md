---
title: "aaaInstall MongoDB sur un VM Linux avec hello CLI d’Azure | Documents Microsoft"
description: "Découvrez comment tooinstall et configurer MongoDB sur un ordinateur Linux machine virtuelle iusing Bonjour Azure CLI 2.0"
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
ms.openlocfilehash: 97a4d9913f0eeaf7b8bf15d7fc81befe538cdc8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="4fee2-103">Comment tooinstall et configurer MongoDB sur un VM Linux</span><span class="sxs-lookup"><span data-stu-id="4fee2-103">How tooinstall and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="4fee2-104">[MongoDB](http://www.mongodb.org) est une base de données NoSQL open-source qui offre des performances élevées.</span><span class="sxs-lookup"><span data-stu-id="4fee2-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="4fee2-105">Cet article vous montre comment tooinstall et configurer MongoDB sur un VM Linux avec hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="4fee2-105">This article shows you how tooinstall and configure MongoDB on a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="4fee2-106">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4fee2-106">You can also perform these steps with hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="4fee2-107">Présentations d’exemples détaillant comment :</span><span class="sxs-lookup"><span data-stu-id="4fee2-107">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="4fee2-108">Installer et configurer une instance MongoDB de base manuellement</span><span class="sxs-lookup"><span data-stu-id="4fee2-108">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="4fee2-109">Création d'une instance MongoDB de base à l'aide d'un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4fee2-109">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="4fee2-110">Créer un cluster partitionné MongoDB complexe avec jeux de réplicas à l’aide d’un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4fee2-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="4fee2-111">Installer et configurer MongoDB manuellement sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4fee2-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="4fee2-112">MongoDB [propose des instructions d’installation](https://docs.mongodb.com/manual/administration/install-on-linux/) pour les distributions Linux, notamment Red Hat / CentOS, SUSE, Ubuntu et Debian.</span><span class="sxs-lookup"><span data-stu-id="4fee2-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="4fee2-113">Hello exemple suivant crée un *CentOS* machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4fee2-113">hello following example creates a *CentOS* VM.</span></span> <span data-ttu-id="4fee2-114">toocreate cet environnement, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="4fee2-114">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="4fee2-115">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4fee2-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4fee2-116">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="4fee2-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="4fee2-117">Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="4fee2-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="4fee2-118">Hello exemple suivant crée un ordinateur virtuel nommé *myVM* avec un utilisateur nommé *azureuser* à l’aide de l’authentification par clé publique SSH</span><span class="sxs-lookup"><span data-stu-id="4fee2-118">hello following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="4fee2-119">SSH toohello machine virtuelle à l’aide de votre propre nom d’utilisateur et le hello `publicIpAddress` répertorié dans la sortie de hello à partir de l’étape précédente de hello :</span><span class="sxs-lookup"><span data-stu-id="4fee2-119">SSH toohello VM using your own username and hello `publicIpAddress` listed in hello output from hello previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="4fee2-120">sources d’installation tooadd hello pour MongoDB, créer un **yum** fichier référentiel comme suit :</span><span class="sxs-lookup"><span data-stu-id="4fee2-120">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="4fee2-121">Ouvrir le fichier de référentiel de MongoDB hello pour la modification.</span><span class="sxs-lookup"><span data-stu-id="4fee2-121">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="4fee2-122">Ajoutez hello lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4fee2-122">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="4fee2-123">Installez MongoDB à l’aide de **yum** comme suit :</span><span class="sxs-lookup"><span data-stu-id="4fee2-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="4fee2-124">Par défaut, SELinux est appliqué sur les images CentOS, ce qui vous empêche d’accéder à MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4fee2-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="4fee2-125">Installer les outils de gestion de stratégie et configurez SELinux tooallow MongoDB toooperate sur son 27017 le port TCP par défaut comme suit :</span><span class="sxs-lookup"><span data-stu-id="4fee2-125">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="4fee2-126">Démarrez le service de MongoDB hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4fee2-126">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="4fee2-127">Vérifier l’installation de MongoDB hello en vous connectant à l’aide de hello local `mongo` client :</span><span class="sxs-lookup"><span data-stu-id="4fee2-127">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="4fee2-128">Instance de MongoDB hello à présent tester en ajoutant des données et de recherche puis :</span><span class="sxs-lookup"><span data-stu-id="4fee2-128">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="4fee2-129">Si vous le souhaitez, configurer automatiquement MongoDB toostart lors d’un redémarrage du système :</span><span class="sxs-lookup"><span data-stu-id="4fee2-129">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="4fee2-130">Créeation d’une instance MongoDB de base sur CentOS à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="4fee2-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="4fee2-131">Vous pouvez créer une instance de MongoDB base sur une machine virtuelle CentOS unique à l’aide de hello suivant le modèle de démarrage rapide Azure à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="4fee2-131">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="4fee2-132">Ce modèle utilise l’extension de Script personnalisé hello pour Linux tooadd un **yum** référentiel tooyour nouveau CentOS VM et installez-les MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4fee2-132">This template uses hello Custom Script extension for Linux tooadd a **yum** repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="4fee2-133">[Instance MongoDB de base sur CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="4fee2-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="4fee2-134">toocreate cet environnement, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="4fee2-134">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="4fee2-135">Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4fee2-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4fee2-136">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="4fee2-136">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="4fee2-137">Ensuite, déployez le modèle de MongoDB hello avec [créer de déploiement de groupe az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="4fee2-137">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="4fee2-138">Définissez vos propres noms de ressources et tailles si nécessaire, comme par exemple pour *newStorageAccountName*, *virtualNetworkName* et *vmSize* :</span><span class="sxs-lookup"><span data-stu-id="4fee2-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

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

<span data-ttu-id="4fee2-139">Session toohello machine virtuelle à l’aide de hello DNS adresse publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4fee2-139">Log on toohello VM using hello public DNS address of your VM.</span></span> <span data-ttu-id="4fee2-140">Vous pouvez afficher les adresses DNS publique hello avec [afficher de machine virtuelle az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="4fee2-140">You can view hello public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="4fee2-141">SSH tooyour machine virtuelle à l’aide de votre propre nom d’utilisateur et l’adresse DNS publique :</span><span class="sxs-lookup"><span data-stu-id="4fee2-141">SSH tooyour VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="4fee2-142">Vérifier l’installation de MongoDB hello en vous connectant à l’aide de hello local `mongo` client comme suit :</span><span class="sxs-lookup"><span data-stu-id="4fee2-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="4fee2-143">Maintenant hello instance de test en ajoutant des données et de recherche comme suit :</span><span class="sxs-lookup"><span data-stu-id="4fee2-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="4fee2-144">Création d’un cluster partitionné MongoDB complexe sur CentOS à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="4fee2-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="4fee2-145">Vous pouvez créer un cluster partitionné MongoDB complex à l’aide de hello suivant le modèle de démarrage rapide Azure à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="4fee2-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="4fee2-146">Ce modèle suit hello [meilleures pratiques de cluster partitionnée MongoDB](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redondance et haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="4fee2-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="4fee2-147">modèle de Hello crée deux partitions, avec trois nœuds dans chaque jeu de réplicas.</span><span class="sxs-lookup"><span data-stu-id="4fee2-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="4fee2-148">Un réplica de serveur de configuration définie avec trois nœuds est également créé, plus deux **mongos** routeur serveurs tooprovide cohérence tooapplications d’entre les partitions de hello.</span><span class="sxs-lookup"><span data-stu-id="4fee2-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="4fee2-149">[Cluster de partitionnement MongoDB sur CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="4fee2-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="4fee2-150">Déploiement de ce cluster partitionné MongoDB complex nécessite plus de 20 cœurs, qui est généralement hello nombre de cœurs par défaut par région pour un abonnement.</span><span class="sxs-lookup"><span data-stu-id="4fee2-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="4fee2-151">Ouvrez un tooincrease de demande de support Azure votre nombre de cœurs.</span><span class="sxs-lookup"><span data-stu-id="4fee2-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="4fee2-152">toocreate cet environnement, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="4fee2-152">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="4fee2-153">Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4fee2-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4fee2-154">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="4fee2-154">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="4fee2-155">Ensuite, déployez le modèle de MongoDB hello avec [créer de déploiement de groupe az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="4fee2-155">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="4fee2-156">Définissez vos propres noms de ressources et tailles si nécessaire, comme par exemple pour *mongoAdminUsername*, *sizeOfDataDiskInGB* et *configNodeVmSize* :</span><span class="sxs-lookup"><span data-stu-id="4fee2-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

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

<span data-ttu-id="4fee2-157">Ce déploiement peut prendre une heure toodeploy et configurer toutes les instances de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="4fee2-157">This deployment can take over an hour toodeploy and configure all hello VM instances.</span></span> <span data-ttu-id="4fee2-158">Hello `--no-wait` indicateur est utilisé à fin hello Hello précédant l’invite de commande tooreturn contrôle toohello une fois le déploiement d’un modèle hello a été acceptée par hello plateforme Azure.</span><span class="sxs-lookup"><span data-stu-id="4fee2-158">hello `--no-wait` flag is used at hello end of hello preceding command tooreturn control toohello command prompt once hello template deployment has been accepted by hello Azure platform.</span></span> <span data-ttu-id="4fee2-159">Vous pouvez ensuite afficher le statut du déploiement hello avec [afficher de déploiement de groupe az](/cli/azure/group/deployment#show).</span><span class="sxs-lookup"><span data-stu-id="4fee2-159">You can then view hello deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="4fee2-160">état de hello hello Hello vues exemple suivantes *myMongoDBCluster* déploiement Bonjour *myResourceGroup* groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="4fee2-160">hello following example views hello status for hello *myMongoDBCluster* deployment in hello *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="4fee2-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4fee2-161">Next steps</span></span>
<span data-ttu-id="4fee2-162">Dans ces exemples, vous vous connectez toohello MongoDB instance localement à partir de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="4fee2-162">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="4fee2-163">Si vous souhaitez tooconnect toohello MongoDB instance à partir d’une autre machine virtuelle ou réseau, assurez-vous de hello approprié [règles du groupe de sécurité réseau sont créées](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="4fee2-163">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="4fee2-164">Ces exemples déploiement un environnement de MongoDB hello central à des fins de développement.</span><span class="sxs-lookup"><span data-stu-id="4fee2-164">These examples deploy hello core MongoDB environment for development purposes.</span></span> <span data-ttu-id="4fee2-165">Appliquer les options de configuration de sécurité hello requis pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="4fee2-165">Apply hello required security configuration options for your environment.</span></span> <span data-ttu-id="4fee2-166">Pour plus d’informations, consultez hello [docs de sécurité MongoDB](https://docs.mongodb.com/manual/security/).</span><span class="sxs-lookup"><span data-stu-id="4fee2-166">For more information, see hello [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="4fee2-167">Pour plus d’informations sur la création de l’aide de modèles, consultez hello [vue d’ensemble du Gestionnaire de ressources Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4fee2-167">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="4fee2-168">les modèles Azure Resource Manager Hello utilisent toodownload d’Extension de Script personnalisé hello et exécutent des scripts sur vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="4fee2-168">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="4fee2-169">Pour plus d’informations, consultez [Using hello Extension de Script personnalisé Azure avec des Machines virtuelles Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="4fee2-169">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

