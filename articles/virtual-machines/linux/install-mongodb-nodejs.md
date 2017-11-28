---
title: "aaaInstall MongoDB sur un VM Linux à l’aide de hello Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment tooinstall et configurer MongoDB sur un ordinateur virtuel de Linux dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources hello."
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
ms.openlocfilehash: 4ce21a2c63da7d00a4422e0a6766e2103e7f12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="bcbef-103">Comment tooinstall et configurer MongoDB sur un VM Linux à l’aide de hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bcbef-103">How tooinstall and configure MongoDB on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="bcbef-104">[MongoDB](http://www.mongodb.org) est une base de données NoSQL open-source qui offre des performances élevées.</span><span class="sxs-lookup"><span data-stu-id="bcbef-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="bcbef-105">Cet article vous montre comment tooinstall et configurer MongoDB sur un VM Linux dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="bcbef-105">This article shows you how tooinstall and configure MongoDB on a Linux VM in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="bcbef-106">Présentations d’exemples détaillant comment :</span><span class="sxs-lookup"><span data-stu-id="bcbef-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="bcbef-107">Installer et configurer une instance MongoDB de base manuellement</span><span class="sxs-lookup"><span data-stu-id="bcbef-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="bcbef-108">Création d'une instance MongoDB de base à l'aide d'un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bcbef-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="bcbef-109">Créer un cluster partitionné MongoDB complexe avec jeux de réplicas à l’aide d’un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bcbef-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="bcbef-110">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="bcbef-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="bcbef-111">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="bcbef-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="bcbef-112">CLI Azure 1.0 – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="bcbef-112">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="bcbef-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="bcbef-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="bcbef-114">Installer et configurer MongoDB manuellement sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bcbef-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="bcbef-115">MongoDB [propose des instructions d’installation](https://docs.mongodb.com/manual/administration/install-on-linux/) pour les distributions Linux, notamment Red Hat / CentOS, SUSE, Ubuntu et Debian.</span><span class="sxs-lookup"><span data-stu-id="bcbef-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="bcbef-116">Hello exemple suivant crée un *CentOS* machine virtuelle à l’aide d’une clé SSH stockée sur *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="bcbef-116">hello following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="bcbef-117">Hello de réponse vous invite à entrer de nom de compte de stockage, nom DNS et informations d’identification d’administrateur :</span><span class="sxs-lookup"><span data-stu-id="bcbef-117">Answer hello prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="bcbef-118">Session toohello machine virtuelle à l’aide d’adresse IP publique hello à fin hello Hello précédant l’étape de création de la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="bcbef-118">Log on toohello VM using hello public IP address displayed at hello end of hello preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="bcbef-119">sources d’installation tooadd hello pour MongoDB, créer un **yum** fichier référentiel comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcbef-119">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="bcbef-120">Ouvrir le fichier de référentiel de MongoDB hello pour la modification.</span><span class="sxs-lookup"><span data-stu-id="bcbef-120">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="bcbef-121">Ajoutez hello lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="bcbef-121">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="bcbef-122">Installez MongoDB à l’aide de **yum** comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcbef-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="bcbef-123">Par défaut, SELinux est appliqué sur les images CentOS, ce qui vous empêche d’accéder à MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bcbef-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="bcbef-124">Installer les outils de gestion de stratégie et configurez SELinux tooallow MongoDB toooperate sur son 27017 le port TCP par défaut comme suit.</span><span class="sxs-lookup"><span data-stu-id="bcbef-124">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="bcbef-125">Démarrez le service de MongoDB hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcbef-125">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="bcbef-126">Vérifier l’installation de MongoDB hello en vous connectant à l’aide de hello local `mongo` client :</span><span class="sxs-lookup"><span data-stu-id="bcbef-126">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="bcbef-127">Instance de MongoDB hello à présent tester en ajoutant des données et de recherche puis :</span><span class="sxs-lookup"><span data-stu-id="bcbef-127">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="bcbef-128">Si vous le souhaitez, configurer automatiquement MongoDB toostart lors d’un redémarrage du système :</span><span class="sxs-lookup"><span data-stu-id="bcbef-128">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="bcbef-129">Créeation d’une instance MongoDB de base sur CentOS à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="bcbef-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="bcbef-130">Vous pouvez créer une instance de MongoDB base sur une machine virtuelle CentOS unique à l’aide de hello suivant le modèle de démarrage rapide Azure à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="bcbef-130">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="bcbef-131">Ce modèle utilise l’extension de Script personnalisé hello pour Linux tooadd un `yum` référentiel tooyour nouveau CentOS VM et installez-les MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bcbef-131">This template uses hello Custom Script extension for Linux tooadd a `yum` repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="bcbef-132">[Instance MongoDB de base sur CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="bcbef-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="bcbef-133">Hello exemple suivant crée un groupe de ressources avec le nom de hello `myResourceGroup` Bonjour `eastus` région.</span><span class="sxs-lookup"><span data-stu-id="bcbef-133">hello following example creates a resource group with hello name `myResourceGroup` in hello `eastus` region.</span></span> <span data-ttu-id="bcbef-134">Saisissez vos propres valeurs, comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcbef-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="bcbef-135">Hello CLI d’Azure vous renvoie tooa invite quelques secondes de la création du déploiement de hello, mais les installation hello et configuration prend quelques minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="bcbef-135">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration takes a few minutes toocomplete.</span></span> <span data-ttu-id="bcbef-136">Vérifier l’état de hello de déploiement hello avec `azure group deployment show myResourceGroup`, entrez le nom hello de votre groupe de ressources en conséquence.</span><span class="sxs-lookup"><span data-stu-id="bcbef-136">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, entering hello name of your resource group accordingly.</span></span> <span data-ttu-id="bcbef-137">Attendez que hello **ProvisioningState** montre *Succeeded* avant toohello tooSSH lors de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bcbef-137">Wait until hello **ProvisioningState** shows *Succeeded* before trying tooSSH toohello VM.</span></span>

<span data-ttu-id="bcbef-138">Une fois le déploiement de hello terminée, SSH toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bcbef-138">Once hello deployment is complete, SSH toohello VM.</span></span> <span data-ttu-id="bcbef-139">Obtenir une adresse IP de hello de votre machine virtuelle à l’aide de hello `azure vm show` commande comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="bcbef-139">Obtain hello IP address of your VM using hello `azure vm show` command as in hello following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="bcbef-140">Près de fin hello de sortie de hello, adresse IP publique de hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="bcbef-140">Near hello end of hello output, hello public IP address is displayed.</span></span> <span data-ttu-id="bcbef-141">SSH tooyour machine virtuelle avec l’adresse IP de hello de votre machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="bcbef-141">SSH tooyour VM with hello IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="bcbef-142">Vérifier l’installation de MongoDB hello en vous connectant à l’aide de hello local `mongo` client comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcbef-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="bcbef-143">Maintenant hello instance de test en ajoutant des données et de recherche comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcbef-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="bcbef-144">Création d’un cluster partitionné MongoDB complexe sur CentOS à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="bcbef-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="bcbef-145">Vous pouvez créer un cluster partitionné MongoDB complex à l’aide de hello suivant le modèle de démarrage rapide Azure à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="bcbef-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="bcbef-146">Ce modèle suit hello [meilleures pratiques de cluster partitionnée MongoDB](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redondance et haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="bcbef-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="bcbef-147">modèle de Hello crée deux partitions, avec trois nœuds dans chaque jeu de réplicas.</span><span class="sxs-lookup"><span data-stu-id="bcbef-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="bcbef-148">Un réplica de serveur de configuration définie avec trois nœuds est également créé, plus deux **mongos** routeur serveurs tooprovide cohérence tooapplications d’entre les partitions de hello.</span><span class="sxs-lookup"><span data-stu-id="bcbef-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="bcbef-149">[Cluster de partitionnement MongoDB sur CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="bcbef-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="bcbef-150">Déploiement de ce cluster partitionné MongoDB complex nécessite plus de 20 cœurs, qui est généralement hello nombre de cœurs par défaut par région pour un abonnement.</span><span class="sxs-lookup"><span data-stu-id="bcbef-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="bcbef-151">Ouvrez un tooincrease de demande de support Azure votre nombre de cœurs.</span><span class="sxs-lookup"><span data-stu-id="bcbef-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="bcbef-152">Hello exemple suivant crée un groupe de ressources avec le nom de hello *myResourceGroup* Bonjour *eastus* région.</span><span class="sxs-lookup"><span data-stu-id="bcbef-152">hello following example creates a resource group with hello name *myResourceGroup* in hello *eastus* region.</span></span> <span data-ttu-id="bcbef-153">Saisissez vos propres valeurs, comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcbef-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="bcbef-154">Hello CLI d’Azure vous renvoie tooa invite quelques secondes de la création du déploiement de hello, mais hello installation et la configuration peuvent reprendre un toocomplete heure.</span><span class="sxs-lookup"><span data-stu-id="bcbef-154">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration can take over an hour toocomplete.</span></span> <span data-ttu-id="bcbef-155">Vérifier l’état de hello de déploiement hello avec `azure group deployment show myResourceGroup`, ajustant nom hello de votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="bcbef-155">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, adjusting hello name of your resource group accordingly.</span></span> <span data-ttu-id="bcbef-156">Attendez que hello **ProvisioningState** montre *Succeeded* avant de connecter des machines virtuelles de toohello.</span><span class="sxs-lookup"><span data-stu-id="bcbef-156">Wait until hello **ProvisioningState** shows *Succeeded* before connecting toohello VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bcbef-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bcbef-157">Next steps</span></span>
<span data-ttu-id="bcbef-158">Dans ces exemples, vous vous connectez toohello MongoDB instance localement à partir de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="bcbef-158">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="bcbef-159">Si vous souhaitez tooconnect toohello MongoDB instance à partir d’une autre machine virtuelle ou réseau, assurez-vous de hello approprié [règles du groupe de sécurité réseau sont créées](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="bcbef-159">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="bcbef-160">Pour plus d’informations sur la création de l’aide de modèles, consultez hello [vue d’ensemble du Gestionnaire de ressources Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bcbef-160">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="bcbef-161">les modèles Azure Resource Manager Hello utilisent toodownload d’Extension de Script personnalisé hello et exécutent des scripts sur vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bcbef-161">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="bcbef-162">Pour plus d’informations, consultez [Using hello Extension de Script personnalisé Azure avec des Machines virtuelles Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="bcbef-162">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

