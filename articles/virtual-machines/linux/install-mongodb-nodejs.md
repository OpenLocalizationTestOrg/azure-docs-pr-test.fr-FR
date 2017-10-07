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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a>Comment tooinstall et configurer MongoDB sur un VM Linux à l’aide de hello Azure CLI 1.0
[MongoDB](http://www.mongodb.org) est une base de données NoSQL open-source qui offre des performances élevées. Cet article vous montre comment tooinstall et configurer MongoDB sur un VM Linux dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources hello. Présentations d’exemples détaillant comment :

* [Installer et configurer une instance MongoDB de base manuellement](#manually-install-and-configure-mongodb-on-a-vm)
* [Création d'une instance MongoDB de base à l'aide d'un modèle Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Créer un cluster partitionné MongoDB complexe avec jeux de réplicas à l’aide d’un modèle Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- CLI Azure 1.0 – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](create-cli-complete-nodejs.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>Installer et configurer MongoDB manuellement sur une machine virtuelle
MongoDB [propose des instructions d’installation](https://docs.mongodb.com/manual/administration/install-on-linux/) pour les distributions Linux, notamment Red Hat / CentOS, SUSE, Ubuntu et Debian. Hello exemple suivant crée un *CentOS* machine virtuelle à l’aide d’une clé SSH stockée sur *~/.ssh/id_rsa.pub*. Hello de réponse vous invite à entrer de nom de compte de stockage, nom DNS et informations d’identification d’administrateur :

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

Session toohello machine virtuelle à l’aide d’adresse IP publique hello à fin hello Hello précédant l’étape de création de la machine virtuelle :

```bash
ssh azureuser@40.78.23.145
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

Par défaut, SELinux est appliqué sur les images CentOS, ce qui vous empêche d’accéder à MongoDB. Installer les outils de gestion de stratégie et configurez SELinux tooallow MongoDB toooperate sur son 27017 le port TCP par défaut comme suit. 

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
Vous pouvez créer une instance de MongoDB base sur une machine virtuelle CentOS unique à l’aide de hello suivant le modèle de démarrage rapide Azure à partir de GitHub. Ce modèle utilise l’extension de Script personnalisé hello pour Linux tooadd un `yum` référentiel tooyour nouveau CentOS VM et installez-les MongoDB.

* [Instance MongoDB de base sur CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

Hello exemple suivant crée un groupe de ressources avec le nom de hello `myResourceGroup` Bonjour `eastus` région. Saisissez vos propres valeurs, comme suit :

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> Hello CLI d’Azure vous renvoie tooa invite quelques secondes de la création du déploiement de hello, mais les installation hello et configuration prend quelques minutes toocomplete. Vérifier l’état de hello de déploiement hello avec `azure group deployment show myResourceGroup`, entrez le nom hello de votre groupe de ressources en conséquence. Attendez que hello **ProvisioningState** montre *Succeeded* avant toohello tooSSH lors de la machine virtuelle.

Une fois le déploiement de hello terminée, SSH toohello machine virtuelle. Obtenir une adresse IP de hello de votre machine virtuelle à l’aide de hello `azure vm show` commande comme hello l’exemple suivant :

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

Près de fin hello de sortie de hello, adresse IP publique de hello s’affiche. SSH tooyour machine virtuelle avec l’adresse IP de hello de votre machine virtuelle :

```bash
ssh azureuser@138.91.149.74
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

Hello exemple suivant crée un groupe de ressources avec le nom de hello *myResourceGroup* Bonjour *eastus* région. Saisissez vos propres valeurs, comme suit :

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> Hello CLI d’Azure vous renvoie tooa invite quelques secondes de la création du déploiement de hello, mais hello installation et la configuration peuvent reprendre un toocomplete heure. Vérifier l’état de hello de déploiement hello avec `azure group deployment show myResourceGroup`, ajustant nom hello de votre groupe de ressources. Attendez que hello **ProvisioningState** montre *Succeeded* avant de connecter des machines virtuelles de toohello.


## <a name="next-steps"></a>Étapes suivantes
Dans ces exemples, vous vous connectez toohello MongoDB instance localement à partir de la machine virtuelle de hello. Si vous souhaitez tooconnect toohello MongoDB instance à partir d’une autre machine virtuelle ou réseau, assurez-vous de hello approprié [règles du groupe de sécurité réseau sont créées](nsg-quickstart.md).

Pour plus d’informations sur la création de l’aide de modèles, consultez hello [vue d’ensemble du Gestionnaire de ressources Azure](../../azure-resource-manager/resource-group-overview.md).

les modèles Azure Resource Manager Hello utilisent toodownload d’Extension de Script personnalisé hello et exécutent des scripts sur vos machines virtuelles. Pour plus d’informations, consultez [Using hello Extension de Script personnalisé Azure avec des Machines virtuelles Linux](extensions-customscript.md).

