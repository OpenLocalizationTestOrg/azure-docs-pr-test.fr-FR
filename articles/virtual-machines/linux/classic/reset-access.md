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
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a><span data-ttu-id="61f79-103">Comment tooreset un mot de passe Linux VM ou clé SSH, corrigez la configuration SSH de hello et vérifier la cohérence des disques à l’aide de l’extension VMAccess hello</span><span class="sxs-lookup"><span data-stu-id="61f79-103">How tooreset a Linux VM password or SSH key, fix hello SSH configuration, and check disk consistency using hello VMAccess extension</span></span>
<span data-ttu-id="61f79-104">Impossible de se connecter virtuels tooa Linux sur Azure en raison d’un mot de passe oublié, une clé SSH (Secure Shell) incorrecte ou un problème de configuration de SSH hello, utilisez hello extension VMAccessForLinux avec un mot de passe hello CLI d’Azure tooreset hello ou clé SSH, corriger Hello configuration SSH et vérifier la cohérence des disques.</span><span class="sxs-lookup"><span data-stu-id="61f79-104">If you can't connect tooa Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with hello SSH configuration, use hello VMAccessForLinux extension with hello Azure CLI tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="61f79-105">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="61f79-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="61f79-106">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="61f79-106">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="61f79-107">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="61f79-107">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="61f79-108">Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="61f79-108">Learn how too[perform these steps using hello Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="61f79-109">Avec hello CLI d’Azure, vous utilisez hello **ensemble d’extension de machine virtuelle azure** commande à partir de vos commandes tooaccess de l’interface de ligne de commande (interpréteur de commandes, Terminal Server, invite de commandes).</span><span class="sxs-lookup"><span data-stu-id="61f79-109">With hello Azure CLI, you use hello **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) tooaccess commands.</span></span> <span data-ttu-id="61f79-110">Exécutez **azure help vm extension set** pour utiliser l’extension détaillée.</span><span class="sxs-lookup"><span data-stu-id="61f79-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="61f79-111">Avec hello CLI d’Azure, vous pouvez effectuer hello tâche suivantes :</span><span class="sxs-lookup"><span data-stu-id="61f79-111">With hello Azure CLI, you can do hello following tasks:</span></span>

* [<span data-ttu-id="61f79-112">Réinitialiser le mot de passe hello</span><span class="sxs-lookup"><span data-stu-id="61f79-112">Reset hello password</span></span>](#pwresetcli)
* [<span data-ttu-id="61f79-113">Réinitialiser la clé SSH hello</span><span class="sxs-lookup"><span data-stu-id="61f79-113">Reset hello SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="61f79-114">Réinitialisation de la clé hello hello et le mot de passe SSH</span><span class="sxs-lookup"><span data-stu-id="61f79-114">Reset hello password and hello SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="61f79-115">Création d’un nouveau compte utilisateur sudo</span><span class="sxs-lookup"><span data-stu-id="61f79-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="61f79-116">Réinitialiser la configuration SSH de hello</span><span class="sxs-lookup"><span data-stu-id="61f79-116">Reset hello SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="61f79-117">Suppression d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="61f79-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="61f79-118">Afficher l’état de hello Hello extension VMAccess</span><span class="sxs-lookup"><span data-stu-id="61f79-118">Display hello status of hello VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="61f79-119">Vérification de la cohérence des disques ajoutés</span><span class="sxs-lookup"><span data-stu-id="61f79-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="61f79-120">Réparation des disques ajoutées sur votre VM Linux</span><span class="sxs-lookup"><span data-stu-id="61f79-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="61f79-121">Composants requis</span><span class="sxs-lookup"><span data-stu-id="61f79-121">Prerequisites</span></span>
<span data-ttu-id="61f79-122">Vous devez suivant de hello toodo :</span><span class="sxs-lookup"><span data-stu-id="61f79-122">You will need toodo hello following:</span></span>

* <span data-ttu-id="61f79-123">Vous devez trop[installer hello CLI d’Azure](../../../cli-install-nodejs.md) et [connecter tooyour abonnement](../../../xplat-cli-connect.md) toouse Azure ressources associées à votre compte.</span><span class="sxs-lookup"><span data-stu-id="61f79-123">You will need too[install hello Azure CLI](../../../cli-install-nodejs.md) and [connect tooyour subscription](../../../xplat-cli-connect.md) toouse Azure resources associated with your account.</span></span>
* <span data-ttu-id="61f79-124">Ensemble hello mode approprié pour le modèle de déploiement classique hello en tapant hello à l’invite de commandes hello :</span><span class="sxs-lookup"><span data-stu-id="61f79-124">Set hello correct mode for hello classic deployment model by typing hello following at hello command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="61f79-125">Disposer d’un nouveau mot de passe ou d’un jeu de clés SSH, tooreset le des deux.</span><span class="sxs-lookup"><span data-stu-id="61f79-125">Have a new password or set of SSH keys, if you want tooreset either one.</span></span> <span data-ttu-id="61f79-126">Vous n’avez pas besoin ces si vous souhaitez que la configuration de SSH tooreset hello.</span><span class="sxs-lookup"><span data-stu-id="61f79-126">You don't need these if you want tooreset hello SSH configuration.</span></span>

## <span data-ttu-id="61f79-127"><a name="pwresetcli"></a>Réinitialiser le mot de passe hello</span><span class="sxs-lookup"><span data-stu-id="61f79-127"><a name="pwresetcli"></a>Reset hello password</span></span>
1. <span data-ttu-id="61f79-128">Sur votre ordinateur local, créez un fichier appelé PrivateConf.json avec ces lignes.</span><span class="sxs-lookup"><span data-stu-id="61f79-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="61f79-129">Remplacez **myUserName** et **myP@ssW0rd** par vos propres nom d’utilisateur et mot de passe, et définissez votre propre date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="61f79-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="61f79-130">Exécutez cette commande, en remplaçant le nom hello de votre machine virtuelle pour **myVM**.</span><span class="sxs-lookup"><span data-stu-id="61f79-130">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="61f79-131"><a name="sshkeyresetcli"></a>Réinitialiser la clé SSH hello</span><span class="sxs-lookup"><span data-stu-id="61f79-131"><a name="sshkeyresetcli"></a>Reset hello SSH key</span></span>
1. <span data-ttu-id="61f79-132">Créez un fichier appelé PrivateConf.json avec ces éléments.</span><span class="sxs-lookup"><span data-stu-id="61f79-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="61f79-133">Remplacez hello **myUserName** et **mySSHKey** valeurs avec vos propres informations.</span><span class="sxs-lookup"><span data-stu-id="61f79-133">Replace hello **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="61f79-134">Exécutez cette commande, en remplaçant le nom hello de votre machine virtuelle pour **myVM**.</span><span class="sxs-lookup"><span data-stu-id="61f79-134">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="61f79-135"><a name="resetbothcli"></a>Réinitialiser le mot de passe hello et la clé SSH hello</span><span class="sxs-lookup"><span data-stu-id="61f79-135"><a name="resetbothcli"></a>Reset both hello password and hello SSH key</span></span>
1. <span data-ttu-id="61f79-136">Créez un fichier appelé PrivateConf.json avec ces éléments.</span><span class="sxs-lookup"><span data-stu-id="61f79-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="61f79-137">Remplacez hello **myUserName**, **mySSHKey** et  **myP@ssW0rd**  valeurs avec vos propres informations.</span><span class="sxs-lookup"><span data-stu-id="61f79-137">Replace hello **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="61f79-138">Exécutez cette commande, en remplaçant le nom hello de votre machine virtuelle pour **myVM**.</span><span class="sxs-lookup"><span data-stu-id="61f79-138">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="61f79-139"><a name="createnewsudocli"></a>Création d’un nouveau compte utilisateur sudo</span><span class="sxs-lookup"><span data-stu-id="61f79-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="61f79-140">Si vous oubliez votre nom d’utilisateur, vous pouvez utiliser une autorité de sudo hello toocreate de VMAccess.</span><span class="sxs-lookup"><span data-stu-id="61f79-140">If you forget your user name, you can use VMAccess toocreate a new one with hello sudo authority.</span></span> <span data-ttu-id="61f79-141">Dans ce cas, hello nom d’utilisateur existant et un mot de passe ne sera pas modifié.</span><span class="sxs-lookup"><span data-stu-id="61f79-141">In this case, hello existing user name and password will not be modified.</span></span>

<span data-ttu-id="61f79-142">toocreate un nouvel utilisateur de sudo avec un accès de mot de passe, utiliser un script hello dans [le mot de passe réinitialisé hello](#pwresetcli) et spécifiez le nouveau nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="61f79-142">toocreate a new sudo user with password access, use hello script in [Reset hello password](#pwresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="61f79-143">toocreate un nouvel utilisateur de sudo avec accès de la clé SSH, utiliser un script hello dans [réinitialiser la clé SSH hello](#sshkeyresetcli) et spécifiez le nouveau nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="61f79-143">toocreate a new sudo user with SSH key access, use hello script in [Reset hello SSH key](#sshkeyresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="61f79-144">Vous pouvez également utiliser [réinitialiser le mot de passe hello et la clé SSH hello](#resetbothcli) toocreate un nouvel utilisateur avec mot de passe et accès de la clé SSH.</span><span class="sxs-lookup"><span data-stu-id="61f79-144">You can also use [Reset hello password and hello SSH key](#resetbothcli) toocreate a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="61f79-145"><a name="sshconfigresetcli"></a>Réinitialiser la configuration SSH de hello</span><span class="sxs-lookup"><span data-stu-id="61f79-145"><a name="sshconfigresetcli"></a>Reset hello SSH configuration</span></span>
<span data-ttu-id="61f79-146">Si la configuration de SSH hello est dans un état indésirable, vous risquez de perdre également accès toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="61f79-146">If hello SSH configuration is in an undesired state, you might also lose access toohello VM.</span></span> <span data-ttu-id="61f79-147">Vous pouvez utiliser l’état par défaut des tooits configuration hello hello VMAccess extension tooreset.</span><span class="sxs-lookup"><span data-stu-id="61f79-147">You can use hello VMAccess extension tooreset hello configuration tooits default state.</span></span> <span data-ttu-id="61f79-148">toodo par conséquent, vous devez simplement clé de « reset_ssh » tooset hello trop « True ».</span><span class="sxs-lookup"><span data-stu-id="61f79-148">toodo so, you just need tooset hello “reset_ssh” key too“True”.</span></span> <span data-ttu-id="61f79-149">extension de Hello sera redémarrer hello SSH serveur, ouvrez le port SSH hello sur votre machine virtuelle et réinitialiser les valeurs de toodefault configuration hello SSH.</span><span class="sxs-lookup"><span data-stu-id="61f79-149">hello extension will restart hello SSH server, open hello SSH port on your VM, and reset hello SSH configuration toodefault values.</span></span> <span data-ttu-id="61f79-150">compte d’utilisateur Hello (nom, un mot de passe ou les clés SSH) n’est pas remplacé.</span><span class="sxs-lookup"><span data-stu-id="61f79-150">hello user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="61f79-151">fichier de configuration Hello SSH réinitialisée se trouve dans /etc/ssh/sshd_config.</span><span class="sxs-lookup"><span data-stu-id="61f79-151">hello SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="61f79-152">Créez un fichier appelé PrivateConf.json avec ces éléments.</span><span class="sxs-lookup"><span data-stu-id="61f79-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="61f79-153">Exécutez cette commande, en remplaçant le nom hello de votre machine virtuelle pour **myVM**.</span><span class="sxs-lookup"><span data-stu-id="61f79-153">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="61f79-154"><a name="deletecli"></a>Suppression d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="61f79-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="61f79-155">Si vous voulez toodelete un compte d’utilisateur sans se connecter à toohello machine virtuelle directement, vous pouvez utiliser ce script.</span><span class="sxs-lookup"><span data-stu-id="61f79-155">If you want toodelete a user account without logging into toohello VM directly, you can use this script.</span></span>

1. <span data-ttu-id="61f79-156">Créez un fichier nommé PrivateConf.json avec ce contenu, en remplaçant tooremove de nom d’utilisateur hello pour **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="61f79-156">Create a file named PrivateConf.json with this content, substituting hello user name tooremove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="61f79-157">Exécutez cette commande, en remplaçant le nom hello de votre machine virtuelle pour **myVM**.</span><span class="sxs-lookup"><span data-stu-id="61f79-157">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="61f79-158"><a name="statuscli"></a>Afficher l’état de hello Hello extension VMAccess</span><span class="sxs-lookup"><span data-stu-id="61f79-158"><a name="statuscli"></a>Display hello status of hello VMAccess extension</span></span>
<span data-ttu-id="61f79-159">état de hello toodisplay Hello extension VMAccess, exécutez la commande.</span><span class="sxs-lookup"><span data-stu-id="61f79-159">toodisplay hello status of hello VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="61f79-160"><a name='checkdisk'></a>Vérification de la cohérence des disques ajoutés</span><span class="sxs-lookup"><span data-stu-id="61f79-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="61f79-161">fsck toorun sur tous les disques de votre machine virtuelle de Linux, vous devez suivant de hello toodo :</span><span class="sxs-lookup"><span data-stu-id="61f79-161">toorun fsck on all disks in your Linux virtual machine, you will need toodo hello following:</span></span>

1. <span data-ttu-id="61f79-162">Créez un fichier nommé PublicConf.json avec ces éléments.</span><span class="sxs-lookup"><span data-stu-id="61f79-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="61f79-163">Vérifier le disque prend une valeur booléenne pour si toocheck disques attaché à un ordinateur virtuel de tooyour ou non.</span><span class="sxs-lookup"><span data-stu-id="61f79-163">Check Disk takes a boolean for whether toocheck disks attached tooyour virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="61f79-164">Exécutez cette commande tooexecute, en remplaçant le nom hello de votre machine virtuelle pour **myVM**.</span><span class="sxs-lookup"><span data-stu-id="61f79-164">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="61f79-165"><a name='repairdisk'></a>Réparation de disques</span><span class="sxs-lookup"><span data-stu-id="61f79-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="61f79-166">toorepair les disques qui ne sont pas monter ou comportent des erreurs de configuration de montage, utilisent la configuration de monter l’extension tooreset hello hello VMAccess sur votre machine virtuelle de Linux.</span><span class="sxs-lookup"><span data-stu-id="61f79-166">toorepair disks that are not mounting or have mount configuration errors, use hello VMAccess extension tooreset hello mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="61f79-167">Puis remplacez nom hello du disque **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="61f79-167">Substituting hello name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="61f79-168">Créez un fichier nommé PublicConf.json avec ces éléments.</span><span class="sxs-lookup"><span data-stu-id="61f79-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="61f79-169">Exécutez cette commande tooexecute, en remplaçant le nom hello de votre machine virtuelle pour **myVM**.</span><span class="sxs-lookup"><span data-stu-id="61f79-169">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="61f79-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61f79-170">Next steps</span></span>
* <span data-ttu-id="61f79-171">Si vous souhaitez que les applets de commande Azure PowerShell toouse ou un mot de passe Azure Resource Manager modèles tooreset hello ou clé SSH, corrigez la configuration SSH de hello et vérifier la cohérence des disques, consultez hello [documentation d’extension VMAccess sur GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="61f79-171">If you want toouse Azure PowerShell cmdlets or Azure Resource Manager templates tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency, see hello [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="61f79-172">Vous pouvez également utiliser hello [portail Azure](https://portal.azure.com) mot de passe tooreset hello ou clé SSH d’un VM Linux déployés dans le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="61f79-172">You can also use hello [Azure portal](https://portal.azure.com) tooreset hello password or SSH key of a Linux VM deployed in hello classic deployment model.</span></span> <span data-ttu-id="61f79-173">Vous ne pouvez pas utiliser actuellement hello portail toothis un VM Linux déployés dans le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="61f79-173">You can't currently use hello portal do toothis for a Linux VM deployed in hello Resource Manager deployment model.</span></span>
* <span data-ttu-id="61f79-174">Consultez la page [À propos des extensions et des fonctionnalités des machines virtuelles](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour plus d’informations sur l’utilisation des extensions de machine virtuelle pour les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="61f79-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

