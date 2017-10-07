---
title: "aaaMove fichiers tooand à partir d’ordinateurs virtuels Linux de Azure avec SCP | Documents Microsoft"
description: "Déplacer en toute sécurité les fichiers tooand à partir d’un VM Linux dans Azure en utilisant le SCP et une paire de clés SSH."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a>Déplacer les fichiers tooand à partir d’un VM Linux à l’aide de SCP

Cet article explique comment toomove des fichiers à partir de votre station de travail des tooan machine virtuelle Linux de Azure, ou à partir d’un Azure machine virtuelle Linux vers le bas tooyour station de travail, à l’aide de la copie sécurisé (SCP). Le déplacement de fichiers entre votre poste de travail et une machine virtuelle Linux, de manière rapide et sécurisée, constitue une partie essentielle de la gestion de votre infrastructure Azure. 

Pour cet article, vous avez besoin d’une machine virtuelle Linux déployée dans Azure à l’aide de [fichiers de clés publiques et privées SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Vous avez également besoin d’un client SCP pour votre ordinateur local. Il est construit par-dessus SSH et inclus dans l’interpréteur de commandes Bash hello par défaut de la plupart des ordinateurs Mac et Linux et certains interpréteurs de commandes Windows.

## <a name="quick-commands"></a>Commandes rapides

Copier un fichier de configuration toohello Linux VM

```bash
scp file azureuser@azurehost:directory/targetfile
```

Copier un fichier vers le bas à partir de hello Linux VM

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a>Procédure pas à pas

Par exemple, nous déplacer un fichier de configuration Azure des tooa Linux VM et par extraction vers le bas un répertoire du fichier journal, à la fois à l’aide de clés CSP et SSH.   

## <a name="ssh-key-pair-authentication"></a>Authentification avec une paire de clés SSH

SCP utilise SSH pour la couche de transport hello. L’authentification sur l’hôte de destination hello hello SSH handles, et il transfère des fichiers hello dans un tunnel chiffré fourni par défaut avec SSH. Pour l’authentification SSH, des noms d’utilisateur et des mots de passe peuvent être utilisés. Toutefois, l’authentification par clé publique et privée SSH est recommandée en tant que meilleure pratique de sécurité. Une fois que SSH a authentifié les connexion hello, SCP commence alors la copie du fichier de hello. À l’aide d’un correctement configuré `~/.ssh/config` et SSH clés publiques et privées, connexion de hello SCP peuvent être établies en utilisant un nom de serveur (ou adresse IP). Si vous avez uniquement une clé SSH, SCP cherche dans hello `~/.ssh/` active et l’utilise en toolog par défaut dans toohello machine virtuelle.

Pour plus d’informations sur la configuration de votre `~/.ssh/config` et les clés publiques et privées SSH, consultez [Créer des clés SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="scp-a-file-tooa-linux-vm"></a>SCP un tooa fichier Linux VM

Pour le premier exemple de hello, nous copions un fichier de configuration Azure des tooa VM Linux qui est utilisé toodeploy automation. Étant donné que ce fichier contient des informations d’identification d’API Azure, notamment des secrets, sa sécurité est importante. tunnel chiffré de Hello fournie par SSH protège le contenu hello du fichier de hello.

Hello après la commande copies hello local *.azure/config* tooan machine virtuelle Azure avec le nom de domaine complet du fichier *myserver.eastus.cloudapp.azure.com*. nom d’utilisateur admin hello sur hello machine virtuelle Azure est *azureuser* . fichier Hello est ciblé toohello */home/azureuser/* active. Substituez vos propres valeurs dans cette commande.

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a>Copie sécurisée (SCP) d’un répertoire à partir d’une machine virtuelle Linux

Pour cet exemple, nous copions un répertoire de fichiers journaux à partir de hello Linux VM tooyour la station de travail vers le bas. Un fichier journal est susceptible de contenir des données sensibles ou secrètes. Toutefois, à l’aide de SCP garantit le contenu des fichiers de journaux hello hello est crypté. L’utilisation de fichiers de SCP tootransfer hello est tooget de façon plus simple de hello hello du répertoire des journaux et des fichiers vers le bas de station de travail tooyour tout en étant sécurisée.

Hello commande suivante copie les fichiers Bonjour */home/azureuser/journaux/* répertoire répertoire /tmp local de hello Azure VM toohello :

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

Hello `-r` cli indicateur indique SCP toorecursively copier hello les fichiers et répertoires à partir du point de hello du répertoire hello répertorié dans la commande hello.  Notez que la syntaxe de ligne de commande de hello est également semblable tooa `cp` copier la commande.

## <a name="next-steps"></a>Étapes suivantes

* [Gérer les utilisateurs, SSH et vérification ou de réparation des disques sur les machines virtuelles Azure Linux à l’aide de bienvenue de le VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
