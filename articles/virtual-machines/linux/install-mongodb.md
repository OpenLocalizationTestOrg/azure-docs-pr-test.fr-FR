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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a>Comment tooinstall et configurer MongoDB sur un VM Linux
[MongoDB](http://www.mongodb.org) est une base de données NoSQL open-source qui offre des performances élevées. Cet article vous montre comment tooinstall et configurer MongoDB sur un VM Linux avec hello Azure CLI 2.0. Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](install-mongodb-nodejs.md). Présentations d’exemples détaillant comment :

* [Installer et configurer une instance MongoDB de base manuellement](#manually-install-and-configure-mongodb-on-a-vm)
* [Création d'une instance MongoDB de base à l'aide d'un modèle Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Créer un cluster partitionné MongoDB complexe avec jeux de réplicas à l’aide d’un modèle Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Installer et configurer MongoDB manuellement sur une machine virtuelle
MongoDB [propose des instructions d’installation](https://docs.mongodb.com/manual/administration/install-on-linux/) pour les distributions Linux, notamment Red Hat / CentOS, SUSE, Ubuntu et Debian. Hello exemple suivant crée un *CentOS* machine virtuelle. toocreate cet environnement, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :

```azurecli
az group create --name myResourceGroup --location eastus
```

Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create). Hello exemple suivant crée un ordinateur virtuel nommé *myVM* avec un utilisateur nommé *azureuser* à l’aide de l’authentification par clé publique SSH

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH toohello machine virtuelle à l’aide de votre propre nom d’utilisateur et le hello `publicIpAddress` répertorié dans la sortie de hello à partir de l’étape précédente de hello :

```bash
ssh azureuser@<publicIpAddress>
```

sources d’installation tooadd hello pour MongoDB, créer un **yum** fichier référentiel comme suit :

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

Ouvrir le fichier de référentiel de MongoDB hello pour la modification. Ajoutez hello lignes suivantes :

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

Installez MongoDB à l’aide de **yum** comme suit :

```bash
sudo yum install -y mongodb-org
```

Par défaut, SELinux est appliqué sur les images CentOS, ce qui vous empêche d’accéder à MongoDB. Installer les outils de gestion de stratégie et configurez SELinux tooallow MongoDB toooperate sur son 27017 le port TCP par défaut comme suit :

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

Démarrez le service de MongoDB hello comme suit :

```bash
sudo service mongod start
```

Vérifier l’installation de MongoDB hello en vous connectant à l’aide de hello local `mongo` client :

```bash
mongo
```

Instance de MongoDB hello à présent tester en ajoutant des données et de recherche puis :

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

Si vous le souhaitez, configurer automatiquement MongoDB toostart lors d’un redémarrage du système :

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a>Créeation d’une instance MongoDB de base sur CentOS à l’aide d’un modèle
Vous pouvez créer une instance de MongoDB base sur une machine virtuelle CentOS unique à l’aide de hello suivant le modèle de démarrage rapide Azure à partir de GitHub. Ce modèle utilise l’extension de Script personnalisé hello pour Linux tooadd un **yum** référentiel tooyour nouveau CentOS VM et installez-les MongoDB.

* [Instance MongoDB de base sur CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

toocreate cet environnement, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login). Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :

```azurecli
az group create --name myResourceGroup --location eastus
```

Ensuite, déployez le modèle de MongoDB hello avec [créer de déploiement de groupe az](/cli/azure/group/deployment#create). Définissez vos propres noms de ressources et tailles si nécessaire, comme par exemple pour *newStorageAccountName*, *virtualNetworkName* et *vmSize* :

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

Session toohello machine virtuelle à l’aide de hello DNS adresse publique de votre machine virtuelle. Vous pouvez afficher les adresses DNS publique hello avec [afficher de machine virtuelle az](/cli/azure/vm#show):

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

SSH tooyour machine virtuelle à l’aide de votre propre nom d’utilisateur et l’adresse DNS publique :

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

Vérifier l’installation de MongoDB hello en vous connectant à l’aide de hello local `mongo` client comme suit :

```bash
mongo
```

Maintenant hello instance de test en ajoutant des données et de recherche comme suit :

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a>Création d’un cluster partitionné MongoDB complexe sur CentOS à l’aide d’un modèle
Vous pouvez créer un cluster partitionné MongoDB complex à l’aide de hello suivant le modèle de démarrage rapide Azure à partir de GitHub. Ce modèle suit hello [meilleures pratiques de cluster partitionnée MongoDB](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redondance et haute disponibilité. modèle de Hello crée deux partitions, avec trois nœuds dans chaque jeu de réplicas. Un réplica de serveur de configuration définie avec trois nœuds est également créé, plus deux **mongos** routeur serveurs tooprovide cohérence tooapplications d’entre les partitions de hello.

* [Cluster de partitionnement MongoDB sur CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json

> [!WARNING]
> Déploiement de ce cluster partitionné MongoDB complex nécessite plus de 20 cœurs, qui est généralement hello nombre de cœurs par défaut par région pour un abonnement. Ouvrez un tooincrease de demande de support Azure votre nombre de cœurs.

toocreate cet environnement, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login). Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :

```azurecli
az group create --name myResourceGroup --location eastus
```

Ensuite, déployez le modèle de MongoDB hello avec [créer de déploiement de groupe az](/cli/azure/group/deployment#create). Définissez vos propres noms de ressources et tailles si nécessaire, comme par exemple pour *mongoAdminUsername*, *sizeOfDataDiskInGB* et *configNodeVmSize* :

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

Ce déploiement peut prendre une heure toodeploy et configurer toutes les instances de machine virtuelle hello. Hello `--no-wait` indicateur est utilisé à fin hello Hello précédant l’invite de commande tooreturn contrôle toohello une fois le déploiement d’un modèle hello a été acceptée par hello plateforme Azure. Vous pouvez ensuite afficher le statut du déploiement hello avec [afficher de déploiement de groupe az](/cli/azure/group/deployment#show). état de hello hello Hello vues exemple suivantes *myMongoDBCluster* déploiement Bonjour *myResourceGroup* groupe de ressources :

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a>Étapes suivantes
Dans ces exemples, vous vous connectez toohello MongoDB instance localement à partir de la machine virtuelle de hello. Si vous souhaitez tooconnect toohello MongoDB instance à partir d’une autre machine virtuelle ou réseau, assurez-vous de hello approprié [règles du groupe de sécurité réseau sont créées](nsg-quickstart.md).

Ces exemples déploiement un environnement de MongoDB hello central à des fins de développement. Appliquer les options de configuration de sécurité hello requis pour votre environnement. Pour plus d’informations, consultez hello [docs de sécurité MongoDB](https://docs.mongodb.com/manual/security/).

Pour plus d’informations sur la création de l’aide de modèles, consultez hello [vue d’ensemble du Gestionnaire de ressources Azure](../../azure-resource-manager/resource-group-overview.md).

les modèles Azure Resource Manager Hello utilisent toodownload d’Extension de Script personnalisé hello et exécutent des scripts sur vos machines virtuelles. Pour plus d’informations, consultez [Using hello Extension de Script personnalisé Azure avec des Machines virtuelles Linux](extensions-customscript.md).

