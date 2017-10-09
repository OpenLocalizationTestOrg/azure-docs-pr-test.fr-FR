---
title: "Bureau à distance d’aaaUse tooa VM Linux dans Azure | Documents Microsoft"
description: "Découvrez comment tooinstall et configurer le Bureau à distance (xrdp) tooconnect tooa Linux VM dans Azure à l’aide des outils graphiques"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a>Installer et configurer le Bureau à distance tooconnect tooa Linux VM dans Azure
Linux machines virtuelles (VM) dans Azure sont généralement gérées à partir de la ligne de commande hello à l’aide d’une connexion SSH (secure shell). Lors de la nouvelle tooLinux, ou pour des scénarios de dépannage rapides, utilisez hello du Bureau à distance peut être plus facile. Cet article détails comment tooinstall et configurer un environnement de bureau ([xfce](https://www.xfce.org)) et le Bureau à distance ([xrdp](http://www.xrdp.org)) pour votre VM Linux à l’aide du modèle de déploiement du Gestionnaire de ressources hello.


## <a name="prerequisites"></a>Composants requis
Cet article requiert une machine virtuelle Linux existante dans Azure. Si vous devez toocreate une machine virtuelle, utilisez une des méthodes suivantes de hello :

- Hello [Azure CLI 2.0](quick-create-cli.md)
- Hello [portail Azure](quick-create-portal.md)


## <a name="install-a-desktop-environment-on-your-linux-vm"></a>Installation d’un environnement de bureau sur votre machine virtuelle Linux
La plupart des machines virtuelles Linux dans Azure n’ont pas d’environnement de bureau installé par défaut. Les machines virtuelles Linux sont généralement gérées à l’aide des connexions SSH plutôt que d’un environnement de bureau. Il existe divers environnements de bureau sous Linux que vous pouvez choisir. Selon votre choix de l’environnement de bureau, il peut consommer un Go too2 d’espace disque et prendre tooinstall de minutes 5 too10 et configurer tous les packages hello requis.

exemple Hello installe légère de hello [xfce4](https://www.xfce.org/) environnement de bureau sur une VM Ubuntu. Pour les autres distributions varier légèrement en fonction des commandes (utilisez `yum` tooinstall sur Red Hat Enterprise Linux et configurer un approprié `selinux` des règles ou utilisez `zypper` tooinstall sur SUSE, par exemple).

Tout d’abord, SSH tooyour une machine virtuelle. Hello exemple suivant connecte toohello ordinateur virtuel nommé *myvm.westus.cloudapp.azure.com* avec le nom d’utilisateur hello de *azureuser*:

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Si vous utilisez des fenêtres et plus d’informations sur l’utilisation de SSH, consultez [comment toouse SSH clés avec Windows](ssh-from-windows.md).

Ensuite, installez xfce en utilisant `apt` comme suit :

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a>Installation et configuration d’un serveur de bureau à distance
Maintenant que vous avez un environnement de bureau installé, configurez un toolisten des services Bureau à distance pour les connexions entrantes. [xrdp](http://xrdp.org) est un serveur RDP (Remote Desktop Protocol) open source qui est disponible sur la plupart des distributions Linux et fonctionne bien avec xfce. Installez xrdp sur votre machine virtuelle Ubuntu comme suit :

```bash
sudo apt-get install xrdp
```

Indiquez xrdp le toouse de l’environnement de bureau lorsque vous démarrez votre session. Configurer xrdp toouse xfce en tant que votre environnement de bureau comme suit :

```bash
echo xfce4-session >~/.xsession
```

Redémarrez le service de xrdp de hello pour effet de tootake hello modifications comme suit :

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a>Définition d’un mot de passe de compte d’utilisateur
Si vous avez créé un mot de passe pour votre compte d’utilisateur lorsque vous avez créé votre machine virtuelle, ignorez cette étape. Si vous utilisez l’authentification par clé SSH et n’avez pas un mot de passe du compte local défini, spécifiez un mot de passe avant d’utiliser xrdp toolog dans tooyour machine virtuelle. xrdp ne peut pas accepter de clés SSH pour l’authentification. exemple Hello spécifie un mot de passe pour le compte d’utilisateur hello *azureuser*:

```bash
sudo passwd azureuser
```

> [!NOTE]
> En spécifiant un mot de passe ne pas mettre à jour vos connexions de mot de passe SSHD configuration toopermit si elle ne l’est pas. Du point de vue de la sécurité, vous pouvez souhaitez tooconnect tooyour machine virtuelle avec un tunnel SSH à l’aide de l’authentification basée sur la clé, puis connectez tooxrdp. Dans ce cas, ignorez hello suivant l’étape sur la création d’une sécurité groupe règle tooallow à distance bureau le trafic réseau.


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a>Création d’une règle de groupe de sécurité réseau pour le trafic du Bureau à distance
tooallow Bureau à distance le trafic tooreach votre VM Linux, une règle de groupe de sécurité réseau doit les toobe créé qui permet à TCP sur port les tooreach 3389 votre machine virtuelle. Pour plus d’informations sur les règles de groupe de sécurité réseau, consultez [Présentation du groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Vous pouvez également [utilisez hello toocreate portail Azure une règle de groupe de sécurité réseau](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello exemples suivants créent une règle de groupe de sécurité réseau avec [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create) nommé *myNetworkSecurityGroupRule* trop*autoriser* le trafic sur *tcp* port *3389*.

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a>Connexion de votre machine virtuelle Linux à un client Bureau à distance
Ouvrez votre client Bureau à distance local et connecter toohello adresse ou le nom DNS de votre VM Linux. Entrez le nom d’utilisateur de hello hello compte d’utilisateur sur votre machine virtuelle comme suit :

![Se connecter tooxrdp à l’aide de votre client Bureau à distance](./media/use-remote-desktop/remote-desktop-client.png)

Une fois l’authentification, l’environnement de bureau xfce hello est chargées et Rechercher similaire toohello l’exemple suivant :

![Environnement de bureau xfce via xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a>Résolution des problèmes
Si vous ne pouvez pas vous connecter tooyour VM Linux à l’aide d’un client Bureau à distance, utilisez `netstat` sur votre tooverify Linux VM que votre machine virtuelle écoute pour les connexions RDP comme suit :

```bash
sudo netstat -plnt | grep rdp
```

Hello suivant montre l’exemple hello machine virtuelle à l’écoute sur le port TCP 3389 comme prévu :

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

Si le service de xrdp hello n’est pas à l’écoute, sur un VM Ubuntu redémarrez hello service comme suit :

```bash
sudo service xrdp restart
```

Examen des journaux dans */var/log*Thug sur votre Ubuntu VM pour obtenir des indications en tant que service de hello toowhy ne répond pas. Vous pouvez également surveiller hello syslog pendant un tooview de la tentative de connexion Bureau à distance des erreurs :

```bash
tail -f /var/log/syslog
```

Autres distributions de Linux telles que Red Hat Enterprise Linux et SUSE peut-être tooreview d’emplacements de fichier journal et les services de toorestart de différentes façons.

Si vous ne recevez pas de réponse dans votre client Bureau à distance et que vous ne voyez pas tous les événements dans le journal système hello, cela indique que le trafic de bureau à distance ne peut pas atteindre hello machine virtuelle. Passez en revue votre tooensure règles du groupe de sécurité de réseau que vous disposez d’une règle de toopermit TCP sur le port 3389. Pour plus d’informations, consultez [Résoudre les problèmes de connectivité des applications sur une machine virtuelle Linux Azure](../windows/troubleshoot-app-connection.md).


## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la création et l’utilisation de clés SSH avec les machines virtuelles Linux, consultez [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md) (Création de clés SSH pour les machines virtuelles Linux dans Azure).

Pour plus d’informations sur l’utilisation de SSH à partir de Windows, consultez [comment toouse SSH clés avec Windows](ssh-from-windows.md).

