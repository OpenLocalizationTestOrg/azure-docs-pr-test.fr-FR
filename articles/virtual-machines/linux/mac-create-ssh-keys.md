---
title: "paire de clés aaaCreate et utilisez un SSH pour les machines virtuelles Linux dans Azure | Documents Microsoft"
description: "Comment toocreate et utilisez une paire de clés SSH publique et privée pour les machines virtuelles Linux dans Azure tooimprove hello sécurité hello processus d’authentification."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a>Comment toocreate et utiliser une clé publique et privée de SSH paire pour les machines virtuelles Linux dans Azure
Avec une paire de clés SSH (secure shell), vous pouvez créer des machines virtuelles (VM) dans Azure qui utilisent des clés SSH pour l’authentification, hello inutile toolog des mots de passe dans. Cet article vous explique comment tooquickly générer et utiliser une paire de fichier de clé publique et privée RSA de SSH protocol version 2 pour les machines virtuelles Linux. Pour plus d’étapes et des exemples supplémentaires, consultez [détaillée des paires de clés SSH toocreate étapes et les certificats](create-ssh-keys-detailed.md).

## <a name="create-an-ssh-key-pair"></a>Création d’une paire de clés SSH
Hello d’utilisation `ssh-keygen` fichiers de commandes toocreate SSH publiques et privées clés par défaut créé dans hello `~/.ssh` active, mais vous pouvez spécifier un autre emplacement et le mot de passe supplémentaire (un mot de passe tooaccess hello fichier de clé privée) lors de la vous y êtes invité. Exécutez hello commande suivante à partir d’un interpréteur de commandes Bash, répondre aux invites hello avec vos propres informations.

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a>Utilisez la paire de clés SSH hello
clé publique Hello que vous placez sur votre VM Linux dans Azure est stocké par défaut dans `~/.ssh/id_rsa.pub`, sauf si vous avez modifié les emplacement hello lorsque vous les avez créés. Si vous utilisez hello [Azure CLI 2.0](/cli/azure) toocreate votre machine virtuelle, spécifiez l’emplacement hello de cette clé publique lorsque vous utilisez hello [az vm créer](/cli/azure/vm#create) avec hello `--ssh-key-path` option. Si vous copiez et collez contenu hello de toouse du fichier de clé publique hello hello portail Azure ou d’un modèle de gestionnaire de ressources, assurez-vous que vous ne copiez pas les espaces blancs supplémentaires. Par exemple, si vous utilisez OS X, vous pouvez diriger le fichier de clé publique hello (par défaut, **~/.ssh/id_rsa.pub**) trop**pbcopy** toocopy contenu de hello (des autres programmes Linux hello même chose, tel que `xclip`).

Si vous n’êtes pas familiarisé avec les clés publiques SSH, vous pouvez voir votre clé publique en exécutant `cat` comme suit, en remplaçant `~/.ssh/id_rsa.pub` par l’emplacement de votre propre fichier de clé publique :

```bash
cat ~/.ssh/id_rsa.pub
```

Avec la clé publique de hello sur votre machine virtuelle Azure, à l’aide de SSH tooyour VM hello adresse IP ou nom DNS de votre machine virtuelle (n’oubliez pas de tooreplace `azureuser` et `myvm.westus.cloudapp.azure.com` ci-dessous avec le nom d’utilisateur de hello administrateur ou une adresse IP et nom de domaine complet de hello--adresse) :

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Si vous avez fourni un mot de passe lorsque vous avez créé votre paire de clés, entrez la phrase secrète de hello lorsque vous y êtes invité au cours du processus de connexion hello. (serveur de hello est ajouté tooyour `~/.ssh/known_hosts` dossier et que vous ne vous demandera tooconnect à nouveau jusqu'à ce que la clé publique de hello sur vos modifications de la machine virtuelle Azure ou le nom du serveur hello est supprimé de `~/.ssh/known_hosts`.)

## <a name="next-steps"></a>Étapes suivantes

Machines virtuelles créées à l’aide de clés SSH sont par défaut configuré avec des mots de passe désactivés, toomake cassée estimation tente considérablement plus coûteux et par conséquent difficile. Cette rubrique décrit la création d’une simple paire de clés SSH dans le cadre d’une utilisation rapide. Si vous avez besoin d’assistance pour la création de votre paire de clés SSH ou exiger des certificats supplémentaires, consultez [détaillée des paires de clés SSH toocreate étapes et les certificats](create-ssh-keys-detailed.md).

Vous pouvez créer des ordinateurs virtuels qui utilisent votre paire de clés SSH à l’aide de hello portail Azure, CLI et les modèles :

* [Créer une VM Linux sécurisé à l’aide de hello portail Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Créer une VM Linux sécurisé à l’aide de hello Azure CLI 2.0)](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Créer une machine virtuelle Linux sécurisée à l’aide d’un modèle Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
