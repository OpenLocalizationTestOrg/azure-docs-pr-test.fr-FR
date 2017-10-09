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
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a><span data-ttu-id="930d1-103">Installer et configurer le Bureau à distance tooconnect tooa Linux VM dans Azure</span><span class="sxs-lookup"><span data-stu-id="930d1-103">Install and configure Remote Desktop tooconnect tooa Linux VM in Azure</span></span>
<span data-ttu-id="930d1-104">Linux machines virtuelles (VM) dans Azure sont généralement gérées à partir de la ligne de commande hello à l’aide d’une connexion SSH (secure shell).</span><span class="sxs-lookup"><span data-stu-id="930d1-104">Linux virtual machines (VMs) in Azure are usually managed from hello command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="930d1-105">Lors de la nouvelle tooLinux, ou pour des scénarios de dépannage rapides, utilisez hello du Bureau à distance peut être plus facile.</span><span class="sxs-lookup"><span data-stu-id="930d1-105">When new tooLinux, or for quick troubleshooting scenarios, hello use of remote desktop may be easier.</span></span> <span data-ttu-id="930d1-106">Cet article détails comment tooinstall et configurer un environnement de bureau ([xfce](https://www.xfce.org)) et le Bureau à distance ([xrdp](http://www.xrdp.org)) pour votre VM Linux à l’aide du modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="930d1-106">This article details how tooinstall and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using hello Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="930d1-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="930d1-107">Prerequisites</span></span>
<span data-ttu-id="930d1-108">Cet article requiert une machine virtuelle Linux existante dans Azure.</span><span class="sxs-lookup"><span data-stu-id="930d1-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="930d1-109">Si vous devez toocreate une machine virtuelle, utilisez une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="930d1-109">If you need toocreate a VM, use one of hello following methods:</span></span>

- <span data-ttu-id="930d1-110">Hello [Azure CLI 2.0](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="930d1-110">hello [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="930d1-111">Hello [portail Azure](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="930d1-111">hello [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="930d1-112">Installation d’un environnement de bureau sur votre machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="930d1-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="930d1-113">La plupart des machines virtuelles Linux dans Azure n’ont pas d’environnement de bureau installé par défaut.</span><span class="sxs-lookup"><span data-stu-id="930d1-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="930d1-114">Les machines virtuelles Linux sont généralement gérées à l’aide des connexions SSH plutôt que d’un environnement de bureau.</span><span class="sxs-lookup"><span data-stu-id="930d1-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="930d1-115">Il existe divers environnements de bureau sous Linux que vous pouvez choisir.</span><span class="sxs-lookup"><span data-stu-id="930d1-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="930d1-116">Selon votre choix de l’environnement de bureau, il peut consommer un Go too2 d’espace disque et prendre tooinstall de minutes 5 too10 et configurer tous les packages hello requis.</span><span class="sxs-lookup"><span data-stu-id="930d1-116">Depending on your choice of desktop environment, it may consume one too2 GB of disk space, and take 5 too10 minutes tooinstall and configure all hello required packages.</span></span>

<span data-ttu-id="930d1-117">exemple Hello installe légère de hello [xfce4](https://www.xfce.org/) environnement de bureau sur une VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="930d1-117">hello following example installs hello lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="930d1-118">Pour les autres distributions varier légèrement en fonction des commandes (utilisez `yum` tooinstall sur Red Hat Enterprise Linux et configurer un approprié `selinux` des règles ou utilisez `zypper` tooinstall sur SUSE, par exemple).</span><span class="sxs-lookup"><span data-stu-id="930d1-118">Commands for other distributions vary slightly (use `yum` tooinstall on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` tooinstall on SUSE, for example).</span></span>

<span data-ttu-id="930d1-119">Tout d’abord, SSH tooyour une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="930d1-119">First, SSH tooyour VM.</span></span> <span data-ttu-id="930d1-120">Hello exemple suivant connecte toohello ordinateur virtuel nommé *myvm.westus.cloudapp.azure.com* avec le nom d’utilisateur hello de *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="930d1-120">hello following example connects toohello VM named *myvm.westus.cloudapp.azure.com* with hello username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="930d1-121">Si vous utilisez des fenêtres et plus d’informations sur l’utilisation de SSH, consultez [comment toouse SSH clés avec Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="930d1-121">If you are using Windows and need more information on using SSH, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="930d1-122">Ensuite, installez xfce en utilisant `apt` comme suit :</span><span class="sxs-lookup"><span data-stu-id="930d1-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="930d1-123">Installation et configuration d’un serveur de bureau à distance</span><span class="sxs-lookup"><span data-stu-id="930d1-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="930d1-124">Maintenant que vous avez un environnement de bureau installé, configurez un toolisten des services Bureau à distance pour les connexions entrantes.</span><span class="sxs-lookup"><span data-stu-id="930d1-124">Now that you have a desktop environment installed, configure a remote desktop service toolisten for incoming connections.</span></span> <span data-ttu-id="930d1-125">[xrdp](http://xrdp.org) est un serveur RDP (Remote Desktop Protocol) open source qui est disponible sur la plupart des distributions Linux et fonctionne bien avec xfce.</span><span class="sxs-lookup"><span data-stu-id="930d1-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="930d1-126">Installez xrdp sur votre machine virtuelle Ubuntu comme suit :</span><span class="sxs-lookup"><span data-stu-id="930d1-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="930d1-127">Indiquez xrdp le toouse de l’environnement de bureau lorsque vous démarrez votre session.</span><span class="sxs-lookup"><span data-stu-id="930d1-127">Tell xrdp what desktop environment toouse when you start your session.</span></span> <span data-ttu-id="930d1-128">Configurer xrdp toouse xfce en tant que votre environnement de bureau comme suit :</span><span class="sxs-lookup"><span data-stu-id="930d1-128">Configure xrdp toouse xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="930d1-129">Redémarrez le service de xrdp de hello pour effet de tootake hello modifications comme suit :</span><span class="sxs-lookup"><span data-stu-id="930d1-129">Restart hello xrdp service for hello changes tootake effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="930d1-130">Définition d’un mot de passe de compte d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="930d1-130">Set a local user account password</span></span>
<span data-ttu-id="930d1-131">Si vous avez créé un mot de passe pour votre compte d’utilisateur lorsque vous avez créé votre machine virtuelle, ignorez cette étape.</span><span class="sxs-lookup"><span data-stu-id="930d1-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="930d1-132">Si vous utilisez l’authentification par clé SSH et n’avez pas un mot de passe du compte local défini, spécifiez un mot de passe avant d’utiliser xrdp toolog dans tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="930d1-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp toolog in tooyour VM.</span></span> <span data-ttu-id="930d1-133">xrdp ne peut pas accepter de clés SSH pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="930d1-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="930d1-134">exemple Hello spécifie un mot de passe pour le compte d’utilisateur hello *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="930d1-134">hello following example specifies a password for hello user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="930d1-135">En spécifiant un mot de passe ne pas mettre à jour vos connexions de mot de passe SSHD configuration toopermit si elle ne l’est pas.</span><span class="sxs-lookup"><span data-stu-id="930d1-135">Specifying a password does not update your SSHD configuration toopermit password logins if it currently does not.</span></span> <span data-ttu-id="930d1-136">Du point de vue de la sécurité, vous pouvez souhaitez tooconnect tooyour machine virtuelle avec un tunnel SSH à l’aide de l’authentification basée sur la clé, puis connectez tooxrdp.</span><span class="sxs-lookup"><span data-stu-id="930d1-136">From a security perspective, you may wish tooconnect tooyour VM with an SSH tunnel using key-based authentication and then connect tooxrdp.</span></span> <span data-ttu-id="930d1-137">Dans ce cas, ignorez hello suivant l’étape sur la création d’une sécurité groupe règle tooallow à distance bureau le trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="930d1-137">If so, skip hello following step on creating a network security group rule tooallow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="930d1-138">Création d’une règle de groupe de sécurité réseau pour le trafic du Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="930d1-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="930d1-139">tooallow Bureau à distance le trafic tooreach votre VM Linux, une règle de groupe de sécurité réseau doit les toobe créé qui permet à TCP sur port les tooreach 3389 votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="930d1-139">tooallow Remote Desktop traffic tooreach your Linux VM, a network security group rule needs toobe created that allows TCP on port 3389 tooreach your VM.</span></span> <span data-ttu-id="930d1-140">Pour plus d’informations sur les règles de groupe de sécurité réseau, consultez [Présentation du groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="930d1-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="930d1-141">Vous pouvez également [utilisez hello toocreate portail Azure une règle de groupe de sécurité réseau](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="930d1-141">You can also [use hello Azure portal toocreate a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="930d1-142">Hello exemples suivants créent une règle de groupe de sécurité réseau avec [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create) nommé *myNetworkSecurityGroupRule* trop*autoriser* le trafic sur *tcp* port *3389*.</span><span class="sxs-lookup"><span data-stu-id="930d1-142">hello following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* too*allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="930d1-143">Connexion de votre machine virtuelle Linux à un client Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="930d1-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="930d1-144">Ouvrez votre client Bureau à distance local et connecter toohello adresse ou le nom DNS de votre VM Linux.</span><span class="sxs-lookup"><span data-stu-id="930d1-144">Open your local remote desktop client and connect toohello IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="930d1-145">Entrez le nom d’utilisateur de hello hello compte d’utilisateur sur votre machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="930d1-145">Enter hello username and password for hello user account on your VM as follows:</span></span>

![Se connecter tooxrdp à l’aide de votre client Bureau à distance](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="930d1-147">Une fois l’authentification, l’environnement de bureau xfce hello est chargées et Rechercher similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="930d1-147">After authenticating, hello xfce desktop environment will load and look similar toohello following example:</span></span>

![Environnement de bureau xfce via xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="930d1-149">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="930d1-149">Troubleshoot</span></span>
<span data-ttu-id="930d1-150">Si vous ne pouvez pas vous connecter tooyour VM Linux à l’aide d’un client Bureau à distance, utilisez `netstat` sur votre tooverify Linux VM que votre machine virtuelle écoute pour les connexions RDP comme suit :</span><span class="sxs-lookup"><span data-stu-id="930d1-150">If you cannot connect tooyour Linux VM using a Remote Desktop client, use `netstat` on your Linux VM tooverify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="930d1-151">Hello suivant montre l’exemple hello machine virtuelle à l’écoute sur le port TCP 3389 comme prévu :</span><span class="sxs-lookup"><span data-stu-id="930d1-151">hello following example shows hello VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="930d1-152">Si le service de xrdp hello n’est pas à l’écoute, sur un VM Ubuntu redémarrez hello service comme suit :</span><span class="sxs-lookup"><span data-stu-id="930d1-152">If hello xrdp service is not listening, on an Ubuntu VM restart hello service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="930d1-153">Examen des journaux dans */var/log*Thug sur votre Ubuntu VM pour obtenir des indications en tant que service de hello toowhy ne répond pas.</span><span class="sxs-lookup"><span data-stu-id="930d1-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as toowhy hello service may not be responding.</span></span> <span data-ttu-id="930d1-154">Vous pouvez également surveiller hello syslog pendant un tooview de la tentative de connexion Bureau à distance des erreurs :</span><span class="sxs-lookup"><span data-stu-id="930d1-154">You can also monitor hello syslog during a remote desktop connection attempt tooview any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="930d1-155">Autres distributions de Linux telles que Red Hat Enterprise Linux et SUSE peut-être tooreview d’emplacements de fichier journal et les services de toorestart de différentes façons.</span><span class="sxs-lookup"><span data-stu-id="930d1-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways toorestart services and alternate log file locations tooreview.</span></span>

<span data-ttu-id="930d1-156">Si vous ne recevez pas de réponse dans votre client Bureau à distance et que vous ne voyez pas tous les événements dans le journal système hello, cela indique que le trafic de bureau à distance ne peut pas atteindre hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="930d1-156">If you do not receive any response in your remote desktop client and do not see any events in hello system log, this behavior indicates that remote desktop traffic cannot reach hello VM.</span></span> <span data-ttu-id="930d1-157">Passez en revue votre tooensure règles du groupe de sécurité de réseau que vous disposez d’une règle de toopermit TCP sur le port 3389.</span><span class="sxs-lookup"><span data-stu-id="930d1-157">Review your network security group rules tooensure that you have a rule toopermit TCP on port 3389.</span></span> <span data-ttu-id="930d1-158">Pour plus d’informations, consultez [Résoudre les problèmes de connectivité des applications sur une machine virtuelle Linux Azure](../windows/troubleshoot-app-connection.md).</span><span class="sxs-lookup"><span data-stu-id="930d1-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="930d1-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="930d1-159">Next steps</span></span>
<span data-ttu-id="930d1-160">Pour plus d’informations sur la création et l’utilisation de clés SSH avec les machines virtuelles Linux, consultez [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md) (Création de clés SSH pour les machines virtuelles Linux dans Azure).</span><span class="sxs-lookup"><span data-stu-id="930d1-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="930d1-161">Pour plus d’informations sur l’utilisation de SSH à partir de Windows, consultez [comment toouse SSH clés avec Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="930d1-161">For information on using SSH from Windows, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

