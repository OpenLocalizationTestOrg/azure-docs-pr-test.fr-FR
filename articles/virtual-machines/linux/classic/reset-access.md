---
title: touche hello CLI aaaReset mot de passe Linux VM et SSH | Documents Microsoft
description: "Comment toouse hello extension VMAccess à partir de hello Azure Interface de ligne de commande (CLI) tooreset un mot de passe Linux VM ou clé SSH, corrigez la configuration SSH de hello et vérifier la cohérence du disque"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a>Comment tooreset un mot de passe Linux VM ou clé SSH, corrigez la configuration SSH de hello et vérifier la cohérence des disques à l’aide de l’extension VMAccess hello
Impossible de se connecter virtuels tooa Linux sur Azure en raison d’un mot de passe oublié, une clé SSH (Secure Shell) incorrecte ou un problème de configuration de SSH hello, utilisez hello extension VMAccessForLinux avec un mot de passe hello CLI d’Azure tooreset hello ou clé SSH, corriger Hello configuration SSH et vérifier la cohérence des disques. 

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).

Avec hello CLI d’Azure, vous utilisez hello **ensemble d’extension de machine virtuelle azure** commande à partir de vos commandes tooaccess de l’interface de ligne de commande (interpréteur de commandes, Terminal Server, invite de commandes). Exécutez **azure help vm extension set** pour utiliser l’extension détaillée.

Avec hello CLI d’Azure, vous pouvez effectuer hello tâche suivantes :

* [Réinitialiser le mot de passe hello](#pwresetcli)
* [Réinitialiser la clé SSH hello](#sshkeyresetcli)
* [Réinitialisation de la clé hello hello et le mot de passe SSH](#resetbothcli)
* [Création d’un nouveau compte utilisateur sudo](#createnewsudocli)
* [Réinitialiser la configuration SSH de hello](#sshconfigresetcli)
* [Suppression d’un utilisateur](#deletecli)
* [Afficher l’état de hello Hello extension VMAccess](#statuscli)
* [Vérification de la cohérence des disques ajoutés](#checkdisk)
* [Réparation des disques ajoutées sur votre VM Linux](#repairdisk)

## <a name="prerequisites"></a>Composants requis
Vous devez suivant de hello toodo :

* Vous devez trop[installer hello CLI d’Azure](../../../cli-install-nodejs.md) et [connecter tooyour abonnement](../../../xplat-cli-connect.md) toouse Azure ressources associées à votre compte.
* Ensemble hello mode approprié pour le modèle de déploiement classique hello en tapant hello à l’invite de commandes hello :
    ``` 
        azure config mode asm
    ```
* Disposer d’un nouveau mot de passe ou d’un jeu de clés SSH, tooreset le des deux. Vous n’avez pas besoin ces si vous souhaitez que la configuration de SSH tooreset hello.

## <a name="pwresetcli"></a>Réinitialiser le mot de passe hello
1. Sur votre ordinateur local, créez un fichier appelé PrivateConf.json avec ces lignes. Remplacez **myUserName** et **myP@ssW0rd** par vos propres nom d’utilisateur et mot de passe, et définissez votre propre date d’expiration.

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. Exécutez cette commande, en remplaçant le nom hello de votre machine virtuelle pour **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <a name="sshkeyresetcli"></a>Réinitialiser la clé SSH hello
1. Créez un fichier appelé PrivateConf.json avec ces éléments. Remplacez hello **myUserName** et **mySSHKey** valeurs avec vos propres informations.

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. Exécutez cette commande, en remplaçant le nom hello de votre machine virtuelle pour **myVM**.
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="resetbothcli"></a>Réinitialiser le mot de passe hello et la clé SSH hello
1. Créez un fichier appelé PrivateConf.json avec ces éléments. Remplacez hello **myUserName**, **mySSHKey** et  **myP@ssW0rd**  valeurs avec vos propres informations.

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. Exécutez cette commande, en remplaçant le nom hello de votre machine virtuelle pour **myVM**.

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="createnewsudocli"></a>Création d’un nouveau compte utilisateur sudo

Si vous oubliez votre nom d’utilisateur, vous pouvez utiliser une autorité de sudo hello toocreate de VMAccess. Dans ce cas, hello nom d’utilisateur existant et un mot de passe ne sera pas modifié.

toocreate un nouvel utilisateur de sudo avec un accès de mot de passe, utiliser un script hello dans [le mot de passe réinitialisé hello](#pwresetcli) et spécifiez le nouveau nom d’utilisateur hello.

toocreate un nouvel utilisateur de sudo avec accès de la clé SSH, utiliser un script hello dans [réinitialiser la clé SSH hello](#sshkeyresetcli) et spécifiez le nouveau nom d’utilisateur hello.

Vous pouvez également utiliser [réinitialiser le mot de passe hello et la clé SSH hello](#resetbothcli) toocreate un nouvel utilisateur avec mot de passe et accès de la clé SSH.

## <a name="sshconfigresetcli"></a>Réinitialiser la configuration SSH de hello
Si la configuration de SSH hello est dans un état indésirable, vous risquez de perdre également accès toohello machine virtuelle. Vous pouvez utiliser l’état par défaut des tooits configuration hello hello VMAccess extension tooreset. toodo par conséquent, vous devez simplement clé de « reset_ssh » tooset hello trop « True ». extension de Hello sera redémarrer hello SSH serveur, ouvrez le port SSH hello sur votre machine virtuelle et réinitialiser les valeurs de toodefault configuration hello SSH. compte d’utilisateur Hello (nom, un mot de passe ou les clés SSH) n’est pas remplacé.

> [!NOTE]
> fichier de configuration Hello SSH réinitialisée se trouve dans /etc/ssh/sshd_config.
> 
> 

1. Créez un fichier appelé PrivateConf.json avec ces éléments.

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. Exécutez cette commande, en remplaçant le nom hello de votre machine virtuelle pour **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="deletecli"></a>Suppression d’un utilisateur
Si vous voulez toodelete un compte d’utilisateur sans se connecter à toohello machine virtuelle directement, vous pouvez utiliser ce script.

1. Créez un fichier nommé PrivateConf.json avec ce contenu, en remplaçant tooremove de nom d’utilisateur hello pour **removeUserName**. 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. Exécutez cette commande, en remplaçant le nom hello de votre machine virtuelle pour **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="statuscli"></a>Afficher l’état de hello Hello extension VMAccess
état de hello toodisplay Hello extension VMAccess, exécutez la commande.

```
        azure vm extension get
```

## <a name='checkdisk'></a>Vérification de la cohérence des disques ajoutés
fsck toorun sur tous les disques de votre machine virtuelle de Linux, vous devez suivant de hello toodo :

1. Créez un fichier nommé PublicConf.json avec ces éléments. Vérifier le disque prend une valeur booléenne pour si toocheck disques attaché à un ordinateur virtuel de tooyour ou non. 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. Exécutez cette commande tooexecute, en remplaçant le nom hello de votre machine virtuelle pour **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <a name='repairdisk'></a>Réparation de disques
toorepair les disques qui ne sont pas monter ou comportent des erreurs de configuration de montage, utilisent la configuration de monter l’extension tooreset hello hello VMAccess sur votre machine virtuelle de Linux. Puis remplacez nom hello du disque **myDisk**.

1. Créez un fichier nommé PublicConf.json avec ces éléments. 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. Exécutez cette commande tooexecute, en remplaçant le nom hello de votre machine virtuelle pour **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a>Étapes suivantes
* Si vous souhaitez que les applets de commande Azure PowerShell toouse ou un mot de passe Azure Resource Manager modèles tooreset hello ou clé SSH, corrigez la configuration SSH de hello et vérifier la cohérence des disques, consultez hello [documentation d’extension VMAccess sur GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess). 
* Vous pouvez également utiliser hello [portail Azure](https://portal.azure.com) mot de passe tooreset hello ou clé SSH d’un VM Linux déployés dans le modèle de déploiement classique hello. Vous ne pouvez pas utiliser actuellement hello portail toothis un VM Linux déployés dans le modèle de déploiement du Gestionnaire de ressources hello.
* Consultez la page [À propos des extensions et des fonctionnalités des machines virtuelles](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour plus d’informations sur l’utilisation des extensions de machine virtuelle pour les machines virtuelles Azure.

