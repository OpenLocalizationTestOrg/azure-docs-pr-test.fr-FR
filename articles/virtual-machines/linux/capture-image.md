---
title: "aaaCapture une image d’un VM Linux dans Azure à l’aide de CLI 2.0 | Documents Microsoft"
description: "Capturer une image d’un toouse de machine virtuelle Azure pour les déploiements de mass à l’aide de hello Azure CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a>Comment toocreate une image d’un ordinateur virtuel ou un disque dur virtuel

<!-- generalize, image - extended version of hello tutorial-->

toocreate plusieurs copies d’un ordinateur virtuel (VM) toouse dans Azure, capturer une image de machine virtuelle de hello ou hello du disque dur virtuel du système d’exploitation. toocreate une image, vous devez supprimer les informations de compte personnel qui le rend plus sûre toodeploy plusieurs fois. Bonjour vous annuler le déploiement d’un ordinateur virtuel existant comme suit, désallouer et créer une image. Vous pouvez utiliser cette image de toocreate machines virtuelles sur n’importe quel groupe de ressources au sein de votre abonnement.

Si vous souhaitez toocreate une copie de votre VM Linux existante pour la sauvegarde ou de débogage, ou téléchargez un VHD Linux spécialisées à partir d’une machine virtuelle locale, consultez [télécharger et créer un VM Linux à partir de l’image de disque personnalisé](upload-vhd.md).  

Vous pouvez également utiliser **GARNITURE** toocreate votre configuration personnalisée. Pour plus d’informations sur l’utilisation du programme de compression, consultez [comment une machine virtuelle Linux toouse GARNITURE toocreate images dans Azure](build-image-with-packer.md).


## <a name="before-you-begin"></a>Avant de commencer
Vérifiez que vous remplissez hello suivant des conditions préalables :

* Vous avez besoin d’une machine virtuelle de Azure créé dans le modèle de déploiement hello Gestionnaire de ressources à l’aide de disques gérés. Si vous n’avez pas créé un VM Linux, vous pouvez utiliser hello [portal](quick-create-portal.md), hello [CLI d’Azure](quick-create-cli.md), ou [modèles Resource Manager](create-ssh-secured-vm-from-template.md). Configurer hello machine virtuelle en fonction des besoins. Par exemple, [ajoutez des disques de données](add-disk.md), appliquez des mises à jour et installez des applications. 

* Vous devez également toohave hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et être connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

## <a name="quick-commands"></a>Commandes rapides

Pour une version simplifiée de cette rubrique, pour les tests, l’évaluation ou en savoir plus sur les machines virtuelles dans Azure, consultez [créer une image personnalisée d’une machine virtuelle de Azure à l’aide de hello CLI](tutorial-custom-images.md).


## <a name="step-1-deprovision-hello-vm"></a>Étape 1 : Annuler le déploiement hello machine virtuelle
Vous annulez le déploiement hello machine virtuelle, à l’aide des données de l’agent de machine virtuelle Azure hello et toodelete les fichiers d’ordinateur spécifique. Hello d’utilisation `waagent` avec hello *-deprovision + utilisateur* paramètre sur votre source de Linux VM. Pour plus d’informations, consultez hello [guide de l’utilisateur Linux Agent Azure](../windows/agent-user-guide.md).

1. Se connecter tooyour VM Linux à l’aide d’un client SSH.
2. Dans la fenêtre SSH hello, tapez hello de commande suivante :
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > Uniquement, exécutez cette commande sur une machine virtuelle que vous avez l’intention de toocapture en tant qu’image. Il ne garantit pas cette image hello est effacée de toutes les informations sensibles ou appropriée pour la redistribution. Hello *+ utilisateur* paramètre supprime également le dernier compte d’utilisateur configuré hello. Si vous souhaitez que les informations d’identification de compte tookeep Bonjour machine virtuelle, utilisez simplement *-deprovision* compte d’utilisateur tooleave hello en place.
 
3. Type **y** toocontinue. Vous pouvez ajouter hello **-force** paramètre tooavoid cette étape de confirmation.
4. Une fois la commande hello terminée, tapez **quitter**. Cette étape ferme le client SSH de hello.

## <a name="step-2-create-vm-image"></a>Étape 2 : Créer une image de machine virtuelle
Utilisez Bonjour Azure CLI 2.0 toomark Bonjour machine virtuelle comme généralisé et capturer l’image de hello. Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les noms de paramètre sont par exemple *myResourceGroup*, *myVnet* et *myVM*.

1. Désallouer hello machine virtuelle qui vous a été annulé avec [az vm désallouer](/cli//azure/vm#deallocate). exemple Hello désalloue hello ordinateur virtuel nommé *myVM* dans le groupe de ressources hello nommé *myResourceGroup*:
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. Hello de marque machine virtuelle comme généralisée avec [az vm généraliser](/cli//azure/vm#generalize). Hello suivants exemple marques hello hello VM nommée *myVM* dans le groupe de ressources hello nommé *myResourceGroup* comme généralisé :
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. Créez une image de la ressource d’ordinateur virtuel hello avec [az image création](/cli//azure/image#create). Hello exemple suivant crée une image nommée *myImage* dans le groupe de ressources hello nommé *myResourceGroup* à l’aide de la ressource de machine virtuelle hello nommé *myVM*:
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > Hello image est créée dans hello même groupe de ressources que votre ordinateur virtuel source. Vous pouvez créer des machines virtuelles dans n’importe quel groupe de ressources de votre abonnement à partir de cette image. À partir d’un point de vue de gestion, vous pouvez toocreate un groupe de ressources spécifique pour vos ressources d’ordinateurs virtuels et des images.

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Étape 3 : Créer une machine virtuelle à partir de l’image de hello capturée
Créer une machine virtuelle à l’aide d’image hello vous avez créé avec [az vm créer](/cli/azure/vm#create). Hello exemple suivant crée un ordinateur virtuel nommé *myVMDeployed* à partir de l’image hello nommée *myImage*:

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a>Création de hello machine virtuelle dans un autre groupe de ressources 

Vous pouvez créer des machines virtuelles à partir d’une image dans n’importe quel groupe de ressources de votre abonnement. toocreate une machine virtuelle dans un autre groupe de ressources à l’image de hello, spécifiez l’ID tooyour image hello ressource complète. Utilisez [liste d’images az](/cli/azure/image#list) tooview une liste d’images. Hello la sortie est similaire toohello l’exemple suivant :

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

Hello exemple suivant utilise [az vm créer](/cli/azure/vm#create) toocreate une machine virtuelle dans un autre groupe de ressources à l’image source de hello en spécifiant l’ID de ressource d’image hello :

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a>Étape 4 : Vérifier le déploiement de hello

Maintenant SSH toohello machine virtuelle vous avez créé le déploiement de hello tooverify et commencer à utiliser hello nouvelle machine virtuelle. tooconnect via SSH, rechercher l’adresse IP de hello ou nom de domaine complet de votre machine virtuelle avec [afficher de machine virtuelle az](/cli/azure/vm#show):

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez créer plusieurs machines virtuelles à partir de votre image de machine virtuelle source. Si vous avez besoin d’image de tooyour toomake des modifications : 

- Créez une machine virtuelle à partir de votre image.
- Apportez les mises à jour ou modifications de configuration requises.
- Suivez hello les étapes à nouveau toodeprovision, désallouer, généraliser et créer une image.
- Utilisez cette nouvelle image pour les déploiements futurs. Si vous le souhaitez, supprimez l’image d’origine de hello.

Pour plus d’informations sur la gestion de vos machines virtuelles avec hello CLI, consultez [Azure CLI 2.0](/cli/azure/overview).
