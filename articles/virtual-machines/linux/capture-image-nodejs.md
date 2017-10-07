---
title: "aaaCapture toouse d’une machine virtuelle de Azure Linux en tant que modèle | Documents Microsoft"
description: "Découvrez comment toocapture et généraliser une image d’une basés sur Linux Azure virtual machine (VM) créée avec le modèle de déploiement du Gestionnaire de ressources Azure hello."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a>Capturer une machine virtuelle Linux exécutée sur Azure
Suivez les étapes de hello dans cet article de toogeneralize et capturer votre machine virtuelle de Azure Linux (VM) dans le modèle de déploiement du Gestionnaire de ressources hello. Lorsque vous généralisez hello machine virtuelle, vous supprimez les informations de compte personnelles et préparez hello VM toobe est utilisé en tant qu’image. Vous puis capture un disque dur virtuel (VHD) généralisé l’image pour hello du système d’exploitation, les disques durs virtuels pour les disques de données attaché, et un [modèle Resource Manager](../../azure-resource-manager/resource-group-overview.md) pour les nouveaux déploiements d’ordinateurs virtuels. Cet article décrit en détail comment l’image avec hello Azure CLI 1.0 toocapture une machine virtuelle pour une machine virtuelle à l’aide de disques non managés. Vous pouvez également [capturer une machine virtuelle à l’aide de disques de Azure gérés par hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Disques gérés sont gérés par hello plateforme Azure et ne nécessitent pas de n’importe quel toostore préparation ou emplacement les. Pour plus d’informations, voir la page [Azure Managed Disks overview](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Vue d’ensemble d’Azure Managed Disks). 

toocreate machines virtuelles à l’aide de l’image hello, configurer des ressources réseau pour chaque nouvel ordinateur virtuel et utilisez hello toodeploy de modèle (un fichier JavaScript Object Notation ou JSON,) à partir de hello capture des images de disque dur virtuel. De cette façon, vous pouvez répliquer une machine virtuelle avec sa configuration logicielle actuel, toohello comme vous utilisez des images Bonjour Azure Marketplace.

> [!TIP]
> Si vous souhaitez toocreate une copie de votre VM Linux existant avec son état spécialisé pour la sauvegarde ou de débogage, consultez [créer une copie d’une machine virtuelle de Linux en cours d’exécution sur Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Et si vous souhaitez tooupload un VHD Linux à partir d’une machine virtuelle locale, consultez [télécharger et de créer un VM Linux à partir de l’image de disque personnalisé](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](#before-you-begin) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello

## <a name="before-you-begin"></a>Avant de commencer
Vérifiez que vous remplissez hello suivant des conditions préalables :

* **Machine virtuelle Azure créé dans le modèle de déploiement du Gestionnaire de ressources hello** -si vous n’avez pas créé un VM Linux, vous pouvez utiliser hello [portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [CLI d’Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ou [le Gestionnaire de ressources modèles](create-ssh-secured-vm-from-template.md). 
  
    Configurer hello machine virtuelle en fonction des besoins. Par exemple, [ajoutez des disques de données](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), appliquez des mises à jour et installez des applications. 
* **CLI Azure** -installation hello [CLI d’Azure](../../cli-install-nodejs.md) sur un ordinateur local.

## <a name="step-1-remove-hello-azure-linux-agent"></a>Étape 1 : Supprimer l’agent de hello Azure Linux
Tout d’abord, exécutez hello **waagent** avec hello **deprovision** paramètre sur hello Linux VM. Cette commande supprime les fichiers et les données toomake hello prêt pour la généralisation des ordinateurs virtuels. Pour plus d’informations, consultez hello [guide de l’utilisateur Linux Agent Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

1. Se connecter tooyour VM Linux à l’aide d’un client SSH.
2. Dans la fenêtre SSH hello, tapez hello de commande suivante :
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > Uniquement, exécutez cette commande sur une machine virtuelle que vous avez l’intention de toocapture en tant qu’image. Il ne garantit pas cette image hello est effacée de toutes les informations sensibles ou appropriée pour la redistribution.
 
3. Type **y** toocontinue. Vous pouvez ajouter hello **-force** paramètre tooavoid cette étape de confirmation.
4. Une fois la commande hello terminée, tapez **quitter**. Cette étape ferme le client SSH de hello.

## <a name="step-2-capture-hello-vm"></a>Étape 2 : Capturer hello machine virtuelle
Utilisez hello CLI d’Azure toogeneralize et capturer hello machine virtuelle. Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les noms de paramètre sont par exemple **myResourceGroup**, **myVnet** et **myVM**.

1. À partir de votre ordinateur local, ouvrez hello CLI d’Azure et [connexion tooyour abonnement Azure](../../xplat-cli-connect.md). 
2. Assurez-vous que vous êtes en mode Gestionnaire de ressources.
   
    ```azurecli
    azure config mode arm
    ```
3. Arrêtez hello machine virtuelle qui vous a déjà été annulé à l’aide de hello de commande suivante :
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. Généraliser hello VM par hello de commande suivante :
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. Exécutez maintenant hello **capture de machine virtuelle azure** commande, qui capture hello machine virtuelle. Dans l’exemple suivant de hello, image hello disques durs virtuels sont capturés avec des noms commençant par **MyVHDNamePrefix**et hello **-t** option spécifie un modèle de toohello de chemin d’accès **MyTemplate.json**. 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > fichiers de disque dur virtuel d’image Hello obtient créés par défaut dans hello même compte de stockage hello d’ordinateur virtuel d’origine est utilisée. Hello d’utilisation *même compte de stockage* toostore hello disques durs virtuels pour de nouvelles machines virtuelles que vous créez à partir de l’image de hello. 

6. emplacement de hello toofind d’une image capturée, modèle JSON hello ouvert dans un éditeur de texte. Bonjour **storageProfile**, recherche hello **uri** Hello **image** situé dans hello **système** conteneur. Par exemple, hello URI d’image de disque hello du système d’exploitation est similaire trop`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Étape 3 : Créer une machine virtuelle à partir de l’image de hello capturée
Maintenant utiliser hello image avec un modèle de toocreate un VM Linux. Ces étapes vous indiquent comment toouse hello CLI d’Azure et hello du modèle de fichier JSON capturés toocreate hello machine virtuelle dans un réseau virtuel.

### <a name="create-network-resources"></a>Créer des ressources réseau
modèle de hello toouse, vous devez tooset un réseau virtuel et une carte réseau pour votre nouvelle machine virtuelle. Nous vous recommandons de que vous créez un groupe de ressources pour ces ressources dans un emplacement hello où est stockée votre image de machine virtuelle. Exécuter des commandes similaires toohello suivant, en remplaçant les noms de vos ressources et un emplacement Azure approprié (« centralus » dans ces commandes) :

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a>Obtenir hello Id de carte réseau de hello
toodeploy une machine virtuelle à partir de l’image hello à l’aide de hello JSON que vous avez enregistré lors de la capture, vous devez hello Id Hello carte réseau. L’obtenir en exécutant hello de commande suivante :

```azurecli
azure network nic show myResourceGroup1 myNIC
```

Hello **Id** Bonjour sortie est similaire trop`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`

### <a name="create-a-vm"></a>Créer une machine virtuelle
Maintenant suivante d’exécution hello commande toocreate votre machine virtuelle à partir de hello capturées image de machine virtuelle. Hello d’utilisation **-f** JSON de modèle de toohello de chemin d’accès hello de paramètre toospecify fichier que vous avez enregistré.

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

Dans la sortie de la commande hello, vous sont demandée toosupply un nouveau nom d’ordinateur virtuel, nom d’utilisateur admin hello et un mot de passe et hello Id Hello carte réseau que vous avez créé précédemment.

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

Hello suivant l’exemple montre ce que vous voyez pour un déploiement réussi :

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a>Vérifier le déploiement de hello
Maintenant SSH toohello machine virtuelle vous avez créé le déploiement de hello tooverify et commencer à utiliser hello nouvelle machine virtuelle. tooconnect via SSH, Rechercher adresse IP hello hello machine virtuelle que vous avez créé en exécutant hello de commande suivante :

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

adresse IP publique de Hello est répertorié dans la sortie de la commande hello. Par défaut, vous vous connectez toohello VM Linux par SSH sur le port 22.

## <a name="create-additional-vms"></a>Créer des machines virtuelles supplémentaires
Hello d’utilisation capturées toodeploy image et le modèle à l’aide des étapes de hello Bonjour précédant la section des machines virtuelles supplémentaires. Autres options de toocreate machines virtuelles à partir de l’image de hello inclure à l’aide d’un modèle de démarrage rapide ou en cours d’exécution hello **créer de machine virtuelle azure** commande.

### <a name="use-hello-captured-template"></a>Utiliser le modèle capturé hello
toouse hello l’image capturée et modèle, suivez ces étapes (détaillés dans la précédente section de hello) :

* Assurez-vous que votre image de machine virtuelle est Bonjour même compte de stockage qui héberge votre disque dur virtuel.
* Copiez le fichier JSON de modèle hello et spécifiez un nom unique pour le disque de système d’exploitation hello de disque dur virtuel hello nouvelle la machine virtuelle (ou les disques durs virtuels). Par exemple, dans hello **storageProfile**, sous **vhd**, dans **uri**, spécifiez un nom unique pour hello **osDisk** disque dur virtuel similaire trop`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`
* Créez une carte réseau soit Bonjour même ou à un autre réseau virtuel.
* Fichier JSON de modèle hello modifié, créez un déploiement du groupe de ressources hello dans lequel vous configurez un réseau virtuel de hello.

### <a name="use-a-quickstart-template"></a>Utilisation d’un modèle de démarrage rapide
Si vous souhaitez réseau hello configuré automatiquement lorsque vous créez une machine virtuelle à partir de l’image de hello, vous pouvez spécifier ces ressources dans un modèle. Par exemple, consultez hello [101-vm-de-utilisateur-image modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) à partir de GitHub. Ce modèle crée une machine virtuelle à partir de votre image personnalisée et hello nécessaire réseau virtuel, adresse IP publique et ressources de la carte réseau. Pour une procédure pas à pas de l’utilisation du modèle de hello Bonjour portail Azure, consultez [comment toocreate un ordinateur virtuel à partir d’une image personnalisée à l’aide d’un modèle de gestionnaire de ressources](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).

### <a name="use-hello-azure-vm-create-command"></a>Utilisez hello azure vm Créer commande
Il est généralement plus simple toouse un toocreate de modèle de gestionnaire de ressources une machine virtuelle à partir de l’image de hello. Toutefois, vous pouvez créer hello VM *impérative* à l’aide de hello **créer de machine virtuelle azure** avec hello **-Q** (**--urn de l’image**) paramètre . Si vous utilisez cette méthode, vous passez également hello **-d** (**--système d’exploitation-disque-vhd**) emplacement de hello toospecify paramètre du fichier .vhd de hello du système d’exploitation pour hello nouvelle machine virtuelle. Ce fichier doit être dans le conteneur de disques durs virtuels hello hello du compte de stockage où se trouve le fichier de disque dur virtuel d’image hello. Hello commande copies hello de disque dur virtuel pour hello nouvelle machine virtuelle automatiquement toohello **disques durs virtuels** conteneur.

Avant d’exécuter **créer de machine virtuelle azure** avec l’image hello, procédez hello comme suit :

1. Créer un groupe de ressources, ou identifier un groupe de ressources pour le déploiement de hello.
2. Créer un public ressource d’adresse IP et une ressource de la carte réseau pour hello nouvelle machine virtuelle. Pour les étapes toocreate un réseau virtuel, adresse IP publique et les cartes réseau à l’aide de hello CLI, consultez plus haut dans cet article. (**créer de machine virtuelle azure** peut également créer une carte réseau, mais vous devez toopass des paramètres supplémentaires pour un réseau virtuel et le sous-réseau.)

Exécutez ensuite une commande qui transmet des URI le fichier de disque dur virtuel du système d’exploitation de tooboth hello et hello existant d’image. Dans cet exemple, une taille Standard_A1 VM est créé dans la région est des États-Unis hello.

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

Pour obtenir d’autres options de commande supplémentaires, exécutez `azure help vm create`.

## <a name="next-steps"></a>Étapes suivantes
toomanage vos machines virtuelles avec hello CLI, consultez tâches hello [déployer et gérer des ordinateurs virtuels à l’aide de modèles Azure Resource Manager et hello CLI d’Azure](create-ssh-secured-vm-from-template.md).

