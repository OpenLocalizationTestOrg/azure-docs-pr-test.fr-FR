---
title: "aaaCapture une image d’un VM Linux | Documents Microsoft"
description: "Découvrez comment toocapture une image d’une basés sur Linux Azure virtual machine (VM) créé avec le modèle de déploiement classique hello."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a>Comment toocapture une machine virtuelle de Linux classique en tant qu’image
> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Cet article vous explique comment toocapture une classique Azure machine virtuelle (VM) exécutant Linux en tant qu’une image toocreate autres machines virtuelles. Cette image comprend le disque du système d’exploitation hello et des disques de données attachée toohello machine virtuelle. Il n’inclut pas la configuration réseau, vous devez tooconfigure que lorsque vous créez hello autre machine virtuelle à partir de l’image de hello.

Magasins Azure hello image sous **Images**, ainsi que toutes les images que vous avez téléchargé. Pour plus d’informations sur les images, consultez l’article [À propos des images de machine virtuelle dans Azure][About Virtual Machine Images in Azure].

## <a name="before-you-begin"></a>Avant de commencer
Ces étapes supposent que vous avez déjà créé une machine virtuelle de Azure à l’aide du modèle de déploiement classique hello et le système d’exploitation de hello configurés, y compris l’attachement des disques de données. Si vous avez besoin toocreate une machine virtuelle, lisez [comment tooCreate une Machine virtuelle Linux][How tooCreate a Linux Virtual Machine].

## <a name="capture-hello-virtual-machine"></a>Capture de machine virtuelle de hello
1. [Se connecter toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) à l’aide d’un client SSH de votre choix.
2. Dans la fenêtre SSH hello, tapez hello commande suivante. Hello de sortie à partir de `waagent` peut varier légèrement en fonction de la version de hello de cet utilitaire :

    ```bash
    sudo waagent -deprovision+user
    ```

    Hello précédente commande tente de système de hello tooclean et adapté à la préparation. Cette opération effectue hello tâches suivantes :

   * Supprime les clés d’hôte SSH (si Provisioning.RegenerateSshHostKeyPair est « y » dans le fichier de configuration hello)
   * efface la configuration de Nameserver dans /etc/resolv.conf ;
   * Supprime hello `root` mot de passe utilisateur à partir / etc/shadow (si Provisioning.DeleteRootPassword est « y » dans le fichier de configuration hello)
   * supprime les baux du client DHCP mis en cache ;
   * Réinitialise héberge nom toolocalhost.localdomain
   * Supprime hello dernier compte d’utilisateur configuré (obtenu à partir de /var/lib/waagent) **et les données associées**.

     > [!NOTE]
     > Mise hors service supprime les fichiers et données trop « généralisent » hello image. Uniquement, exécutez cette commande sur une machine virtuelle que vous avez l’intention toocapture comme un nouveau modèle d’image. Il ne garantit pas cette image hello est effacée de toutes les informations sensibles ou adaptée aux parties toothird de redistribution.

3. Type **y** toocontinue. Vous pouvez ajouter hello `-force` paramètre tooavoid cette étape de confirmation.
4. Type **Exit** client SSH de hello tooclose.

   > [!NOTE]
   > Hello restantes étapes supposent que vous avez déjà [installé hello CLI d’Azure](../../../cli-install-nodejs.md) sur votre ordinateur client. Tous les hello comme suit peut également être effectué dans hello [portail Azure](http://portal.azure.com).

5. À partir de votre ordinateur client, ouvrez CLI d’Azure et de connexion tooyour abonnement Azure. Pour plus d’informations, consultez [connecter tooan abonnement Azure à partir de hello CLI d’Azure](../../../xplat-cli-connect.md).

   > [!NOTE]
   > Bonjour portail Azure, ouvrez une session dans toohello portal.

6. Assurez-vous que vous êtes en mode de gestion des services :

    ```azurecli
    azure config mode asm
    ```

7. Arrêtez hello machine virtuelle qui est déjà annulé. Hello exemple suivant arrête hello ordinateur virtuel nommé `myVM`:

    ```azurecli
    azure vm shutdown myVM
    ```
   Si nécessaire, vous pouvez afficher une liste hello tous les ordinateurs virtuels créés dans votre abonnement à l’aide de`azure vm list`

   > [!NOTE]
   > Si vous utilisez hello portail Azure, sélectionnez hello machine virtuelle et cliquez sur **arrêter** arrêter hello machine virtuelle.

8. Lorsque hello machine virtuelle est arrêtée, capturez l’image du hello. Hello suivant capture de l’exemple hello ordinateur virtuel nommé `myVM` et crée une image généralisée nommée `myNewVM`:

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    Hello `-t` sous-commande suppressions hello ordinateur virtuel d’origine.

    > [!NOTE]
    > Bonjour portail Azure, vous pouvez capturer une image en sélectionnant **Image** à partir du menu du hub hello. Vous devez hello toosupply informations pour l’image de hello suivantes : nom, groupe de ressources, l’emplacement, le type de système d’exploitation et le chemin d’accès de stockage blob.

9. Hello nouvelle image est désormais disponible dans la liste de hello d’images qui peuvent être utilisées tooconfigure tout nouvel ordinateur virtuel. Vous pouvez l’afficher avec la commande hello :

   ```azurecli
   azure vm image list
   ```

   Sur hello [portail Azure](http://portal.azure.com), hello nouvelle image apparaît dans hello **images de machine virtuelle (classique)** qui appartient toohello **de calcul** services. Vous pouvez accéder aux **images de machine virtuelle (classique)** en cliquant sur _davantage de services_ bas hello hello Azure service liste, puis en consultant Bonjour **de calcul** services.   

   ![Capture d’image réussie](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Étapes suivantes
image de Hello est prêt toobe utilisé toocreate machines virtuelles. Vous pouvez utiliser la commande CLI d’Azure de hello `azure vm create` et nom de l’image hello approvisionnement vous avez créé. Pour plus d’informations, consultez [Using hello CLI d’Azure avec le modèle de déploiement classique](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

Vous pouvez également utiliser hello [portail Azure](http://portal.azure.com) toocreate une machine virtuelle personnalisé à l’aide de hello **Image** (méthode) et en sélectionnant hello de l’image que vous avez créé. Pour plus d’informations, consultez [comment tooCreate un ordinateur virtuel personnalisé][How tooCreate a Custom Virtual Machine].

**Consultez également :**[Guide d’utilisateur de l’agent Linux Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
