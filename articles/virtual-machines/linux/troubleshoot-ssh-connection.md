---
title: "la connexion SSH aaaTroubleshoot émet tooan machine virtuelle Azure | Documents Microsoft"
description: "Comment tootroubleshoot problèmes tels que « Échoué de la connexion SSH » ou « A refusé la connexion SSH » pour une machine virtuelle Azure exécutant Linux."
keywords: "connexion ssh refusée, erreur ssh, ssh azure, échec de connexion SSH"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a>Résoudre les problèmes de tooan des connexions SSH Azure Linux VM qui échoue, les erreurs, ou est refusée
Il existe différentes raisons que vous rencontrez des erreurs de SSH (Secure Shell), les échecs de connexion SSH ou SSH est refusée lorsque vous essayez de tooconnect tooa Linux virtual machine (VM). Cet article vous permet de rechercher et problèmes de hello correct. Vous pouvez utiliser hello portail Azure, Azure CLI ou Extension d’accès aux ordinateurs virtuels pour Linux tootroubleshoot et résoudre les problèmes de connexion.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello forums MSDN Azure et le débordement de pile](http://azure.microsoft.com/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de support technique Azure](http://azure.microsoft.com/support/options/) et sélectionnez **obtenir un support technique**. Pour plus d’informations sur l’utilisation de Azure prend en charge, lire hello [prise en charge de Microsoft Azure FAQ](http://azure.microsoft.com/support/faq/).

## <a name="quick-troubleshooting-steps"></a>Étapes de dépannage rapide
Après chaque étape de résolution des problèmes, essayez de vous reconnecter toohello machine virtuelle.

1. Réinitialiser la configuration SSH de hello.
2. Réinitialiser les informations d’identification de hello pour l’utilisateur de hello.
3. Vérifiez que hello [groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md) règles autorisent le trafic SSH.
   * Assurez-vous qu’une règle de groupe de sécurité réseau existe toopermit SSH trafic (par défaut, le port TCP 22).
   * Vous ne pouvez pas utiliser la redirection / mappage de port sans utiliser un équilibreur de charge Azure.
4. Vérifiez hello [contrôle d’intégrité de machine virtuelle](../../resource-health/resource-health-overview.md). 
   * Vérifiez que hello VM rapports comme étant sain.
   * Si vous avez activés les diagnostics de démarrage, vérifiez hello VM ne signale pas d’erreurs de démarrage dans les journaux hello.
5. Redémarrez hello machine virtuelle.
6. Redéployez hello machine virtuelle.

Si vous cherchez des procédures de dépannage plus détaillées et des explications, poursuivez la lecture.

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a>Problèmes de connexion SSH méthodes disponibles tootroubleshoot
Vous pouvez réinitialiser les informations d’identification ou la configuration SSH à l’aide d’une des méthodes suivantes de hello :

* [Portail Azure](#use-the-azure-portal) - great si vous avez besoin de tooquickly réinitialiser la configuration SSH de hello ou clé SSH et que vous n’avez hello Windows Azure tools installés.
* [Azure CLI 2.0](#use-the-azure-cli-20) : Si vous êtes déjà sur la ligne de commande hello rapidement réinitialisation hello SSH configuration ou les informations d’identification. Vous pouvez également utiliser hello [Azure CLI 1.0](#use-the-azure-cli-10)
* [L’extension VMAccessForLinux Azure](#use-the-vmaccess-extension) - création et la réutilisation de json définition fichiers tooreset hello SSH configuration ou références utilisateur.

Après chaque étape de dépannage, réessayez de vous connecter tooyour machine virtuelle. Si vous ne pouvez toujours pas vous connecter, essayez l’étape suivante de hello.

## <a name="use-hello-azure-portal"></a>Utilisez hello portail Azure
Hello portail Azure fournit un Bonjour de tooreset rapidement des informations d’identification utilisateur ou de la configuration SSH sans installer les outils sur votre ordinateur local.

Bonjour portail Azure, sélectionnez votre machine virtuelle. Défiler toohello **prise en charge + dépannage** section et sélectionnez **réinitialisation de mot de passe** comme hello l’exemple suivant :

![Réinitialiser la configuration SSH ou les informations d’identification dans hello portail Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a>Réinitialiser la configuration SSH de hello
Dans un premier temps, sélectionnez `Reset configuration only` de hello **Mode** menu déroulant comme dans hello précédant la capture d’écran, puis cliquez sur hello **réinitialiser** bouton. Une fois cette opération terminée, réessayez tooaccess votre machine virtuelle.

### <a name="reset-ssh-credentials-for-a-user"></a>Réinitialisation des informations d’identification SSH d’un utilisateur
informations d’identification de hello tooreset d’un utilisateur existant, sélectionnez `Reset SSH public key` ou `Reset password` de hello **Mode** menu déroulant comme hello précédant la capture d’écran. Spécifiez le nom d’utilisateur hello et une clé SSH ou un nouveau mot de passe, puis cliquez sur hello **réinitialiser** bouton.

Vous pouvez également créer un utilisateur avec des privilèges sudo sur hello machine virtuelle à partir de ce menu. Entrez un nouveau nom d’utilisateur et le mot de passe associé ou la clé SSH, puis cliquez sur hello **réinitialiser** bouton.

## <a name="use-hello-azure-cli-20"></a>Utilisez hello Azure CLI 2.0
Si vous n’avez pas encore, installez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Si vous avez créé et téléchargé une image de disque Linux personnalisée, vérifiez que hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 ou version ultérieure est installé. Pour les machines virtuelles créées à l’aide d’images de la galerie, cette extension de l’accès est déjà installée et configurée.

### <a name="reset-ssh-configuration"></a>Réinitialisation de la configuration SSH
Vous pouvez initialement try réinitialisation hello SSH toodefault les valeurs de configuration et en cours de redémarrage serveur SSH hello hello machine virtuelle. Notez que cela ne modifie pas le nom de compte d’utilisateur hello, mot de passe ou des clés SSH.
Hello exemple suivant utilise [réinitialisation de l’utilisateur az vm-ssh](/cli/azure/vm/user#reset-ssh) configuration SSH tooreset hello hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`. Utilisez vos propres valeurs comme suit :

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a>Réinitialisation des informations d’identification SSH d’un utilisateur
Hello exemple suivant utilise [mise à jour des utilisateur de machine virtuelle az](/cli/azure/vm/user#update) tooreset hello informations d’identification pour `myUsername` valeur toohello spécifiée dans `myPassword`, sur hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`. Utilisez vos propres valeurs comme suit :

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

Si vous utilisez l’authentification par clé SSH, vous pouvez réinitialiser la clé SSH hello pour un utilisateur donné. Hello exemple suivant utilise **az vm accéder set-linux-user** tooupdate hello SSH clé stockée dans `~/.ssh/id_rsa.pub` d’utilisateur hello nommé `myUsername`, sur hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`. Utilisez vos propres valeurs comme suit :

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a>Utilisez l’extension VMAccess hello
Hello Extension d’accès aux ordinateurs virtuels pour Linux lit dans un fichier json qui définit toocarry actions out. Ces actions incluent la réinitialisation SSHD, la réinitialisation d’une clé SSH ou l’ajout d’un utilisateur. Vous utilisez toujours toocall hello extension VMAccess de hello CLI d’Azure, mais vous pouvez réutiliser des fichiers au format json hello dans plusieurs machines virtuelles, si vous le souhaitez. Cette approche vous permet de toocreate un référentiel de fichiers json qui peut ensuite être appelée pour compte tenu des scénarios.

### <a name="reset-sshd"></a>Réinitialiser SSHD
Créez un fichier nommé `settings.json` avec hello suivant le contenu :

```json
{  
    "reset_ssh":"True"
}
```

À l’aide de hello CLI d’Azure, puis appelez hello `VMAccessForLinux` extension tooreset votre connexion SSHD en spécifiant votre fichier json. Hello exemple suivant utilise [az vm extension ensemble](/cli/azure/vm/extension#set) tooreset SSHD sur hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`. Utilisez vos propres valeurs comme suit :

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a>Réinitialisation des informations d’identification SSH d’un utilisateur
Se SSHD toofunction correctement, vous pouvez réinitialiser les informations d’identification de hello pour un utilisateur lui-même. mot de passe tooreset hello pour un utilisateur, créez un fichier nommé `settings.json`. Hello exemple suivant réinitialise les informations d’identification de hello pour `myUsername` valeur toohello spécifiée dans `myPassword`. Entrez hello suivant des lignes dans votre `settings.json` fichier, à l’aide de vos propres valeurs :

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

Ou tooreset hello clé SSH pour un utilisateur, commencez par créer un fichier nommé `settings.json`. Hello exemple suivant réinitialise les informations d’identification de hello pour `myUsername` valeur toohello spécifiée dans `myPassword`, sur hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`. Entrez hello suivant des lignes dans votre `settings.json` fichier, à l’aide de vos propres valeurs :

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

Après avoir créé votre fichier json, utilisez hello de toocall CLI d’Azure hello `VMAccessForLinux` tooreset d’extension d’informations d’identification de votre utilisateur SSH en spécifiant votre fichier json. Hello exemple suivant réinitialise les informations d’identification sur hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`. Utilisez vos propres valeurs comme suit :

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a>Utilisez hello Azure CLI 1.0
Si vous n’avez pas déjà fait, [installer hello Azure CLI 1.0 et se connecter tooyour abonnement Azure](../../cli-install-nodejs.md). Assurez-vous d’utiliser le mode Resource Manager comme indiqué ci-après :

```azurecli
azure config mode arm
```

Si vous avez créé et téléchargé une image de disque Linux personnalisée, vérifiez que hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 ou version ultérieure est installé. Pour les machines virtuelles créées à l’aide d’images de la galerie, cette extension de l’accès est déjà installée et configurée.

### <a name="reset-ssh-configuration"></a>Réinitialisation de la configuration SSH
configuration de SSHD Hello lui-même peut être mal configurée ou service de hello a rencontré une erreur. Vous pouvez réinitialiser toomake SSHD que la configuration SSH hello lui-même est valide. La réinitialisation SSHD doit être hello première étape de dépannage que vous prenez.

Hello exemple suivant réinitialise SSHD sur un ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`. Utilisez vos propres noms de machine virtuelle et de groupe de ressources comme suit :

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a>Réinitialisation des informations d’identification SSH d’un utilisateur
Se SSHD toofunction correctement, vous pouvez réinitialiser le mot de passe hello pour un utilisateur lui-même. Hello exemple suivant réinitialise les informations d’identification de hello pour `myUsername` valeur toohello spécifiée dans `myPassword`, sur hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`. Utilisez vos propres valeurs comme suit :

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

Si vous utilisez l’authentification par clé SSH, vous pouvez réinitialiser la clé SSH hello pour un utilisateur donné. Hello après les mises à jour de l’exemple hello stockée dans la clé SSH `~/.ssh/id_rsa.pub` d’utilisateur hello nommé `myUsername`, sur hello ordinateur virtuel nommé `myVM` dans `myResourceGroup`. Utilisez vos propres valeurs comme suit :

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a>Redémarrer une machine virtuelle
Si vous avez réinitialisé les informations d’identification utilisateur et de configuration de SSH hello ou a rencontré une erreur en faisant cela, vous pouvez essayer de redémarrer tooaddress de machine virtuelle hello sous-jacente des problèmes de calcul.

### <a name="azure-portal"></a>Portail Azure
une machine virtuelle à l’aide de toorestart hello sélectionnez portail, Azure hello de votre machine virtuelle et cliquez sur **redémarrer** bouton comme hello l’exemple suivant :

![Redémarrer une machine virtuelle Bonjour portail Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a>Azure CLI 1.0
Hello après le redémarrage de l’exemple hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`. Utilisez vos propres valeurs comme suit :

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Azure CLI 2.0
Hello exemple suivant utilise [redémarrage de machine virtuelle az](/cli/azure/vm#restart) toorestart hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`. Utilisez vos propres valeurs comme suit :

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a>Redéploiement d’une machine virtuelle
Vous pouvez redéployer un nœud de tooanother de machine virtuelle dans Azure, ce qui peut résoudre les problèmes de mise en réseau sous-jacent. Pour plus d’informations sur la redéployer une machine virtuelle, consultez [redéployer la machine virtuelle toonew nœud Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> Une fois cette opération terminée, disque éphémère, les données seront perdues et les adresses IP dynamiques associés à la machine virtuelle de hello seront mise à jour.
> 
> 

### <a name="azure-portal"></a>Portail Azure
une machine virtuelle à l’aide de tooredeploy hello Azure sélectionnez portail, votre machine virtuelle et faites défiler toohello **prise en charge + dépannage** section. Cliquez sur hello **redéployer** bouton comme hello l’exemple suivant :

![Redéployer une machine virtuelle dans hello portail Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a>Azure CLI 1.0
Hello suivant redéploiements ultérieurs d’exemple hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`. Utilisez vos propres valeurs comme suit :

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Azure CLI 2.0
Hello après utilisation de l’exemple [redéploiement de machine virtuelle az](/cli/azure/vm#redeploy) tooredeploy hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`. Utilisez vos propres valeurs comme suit :

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a>Machines virtuelles créées à l’aide du modèle de déploiement classique de hello
Essayez ces étapes tooresolve hello courants SSH échecs de connexion pour les ordinateurs virtuels qui ont été créés à l’aide du modèle de déploiement classique hello. Après chaque étape, essayez de vous reconnecter toohello machine virtuelle.

* Réinitialisez l’accès à distance à partir de hello [portail Azure](https://portal.azure.com). Sur hello portail Azure, votre machine virtuelle puis cliquez sur hello **réinitialiser à distance...**  bouton.
* Redémarrez hello machine virtuelle. Sur hello [portail Azure](https://portal.azure.com), sélectionnez votre machine virtuelle et cliquez sur hello **redémarrer** bouton.
    
* Redéployez le nœud Azure nouvelle machine virtuelle tooa hello. Pour plus d’informations sur la façon tooredeploy une machine virtuelle, consultez [redéployer la machine virtuelle toonew nœud Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
    Une fois cette opération terminée, disque éphémère, les données seront perdues et les adresses IP dynamiques associés à la machine virtuelle de hello seront mise à jour.
* Suivez les instructions de hello dans [comment tooreset un mot de passe ou de SSH pour les ordinateurs virtuels basés sur Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) à :
  
  * Réinitialiser le mot de passe hello ou clé SSH.
  * créer un nouveau compte utilisateur *sudo* ;
  * Réinitialiser la configuration SSH de hello.
* Vérifiez l’intégrité des ressources de machine virtuelle hello pour les problèmes de plateforme.<br>
     Sélectionnez votre machine virtuelle et faites défiler jusqu’à **Paramètres** > **Vérifier l’intégrité**.

## <a name="additional-resources"></a>Ressources supplémentaires
* Si vous ne parvenez toujours pas tooSSH tooyour machine virtuelle après suivant hello après les étapes, consultez [plus d’étapes de dépannage](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview supplémentaire étapes tooresolve votre problème.
* Pour plus d’informations sur la résolution des problèmes d’accès aux applications, consultez [application tooan de résoudre les accès en cours d’exécution sur une machine virtuelle Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Pour plus d’informations sur le dépannage des ordinateurs virtuels qui ont été créés à l’aide du modèle de déploiement classique de hello, consultez [comment tooreset un mot de passe ou de SSH pour les ordinateurs virtuels basés sur Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

