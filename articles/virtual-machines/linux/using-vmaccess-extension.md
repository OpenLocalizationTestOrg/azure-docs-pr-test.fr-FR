---
title: "aaaReset accès tooan machine virtuelle de Azure Linux | Documents Microsoft"
description: "Comment toomanage accès aux utilisateurs et réinitialiser sur l’utilisation de machines virtuelles Linux hello VMAccess Extension et hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/04/2017
ms.author: danlep
ms.openlocfilehash: 2f8db01b9fac20bf547d8b1926e5c0b3c5d18280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a><span data-ttu-id="5f7ba-103">Gérer les utilisateurs, SSH et vérification ou la réparation des disques sur l’utilisation de machines virtuelles Linux hello VMAccess Extension avec hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5f7ba-103">Manage users, SSH, and check or repair disks on Linux VMs using hello VMAccess Extension with hello Azure CLI 2.0</span></span>
<span data-ttu-id="5f7ba-104">disque Hello sur votre VM Linux affichant les erreurs.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-104">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="5f7ba-105">Vous une certaine manière réinitialisez le mot de passe racine hello pour votre VM Linux ou accidentellement votre clé privée SSH.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-105">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="5f7ba-106">Si cela se produisait dans jours hello de centre de données hello, vous devez toodrive il et puis ouvrez tooget KVM hello sur la console serveur hello.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-106">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="5f7ba-107">Considérer hello extension VMAccess de Azure en tant que ce commutateur qui vous permet de tooaccess hello console tooreset accès tooLinux ou effectuez une maintenance au niveau du disque.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-107">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="5f7ba-108">Cet article vous explique comment toouse hello Azure de le VMAccess Extension toocheck ou réparer un disque, réinitialisez l’accès de l’utilisateur, gérer les comptes d’utilisateur ou réinitialiser la configuration SSH de hello sur Linux.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-108">This article shows you how toouse hello Azure VMAccess Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSH configuration on Linux.</span></span> <span data-ttu-id="5f7ba-109">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5f7ba-109">You can also perform these steps with hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-toouse-hello-vmaccess-extension"></a><span data-ttu-id="5f7ba-110">Méthodes toouse hello VMAccess Extension</span><span class="sxs-lookup"><span data-stu-id="5f7ba-110">Ways toouse hello VMAccess Extension</span></span>
<span data-ttu-id="5f7ba-111">Il existe deux manières que vous pouvez utiliser hello VMAccess Extension sur vos machines virtuelles Linux :</span><span class="sxs-lookup"><span data-stu-id="5f7ba-111">There are two ways that you can use hello VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="5f7ba-112">Utilisez hello Azure CLI 2.0 et les paramètres de hello requis.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-112">Use hello Azure CLI 2.0 and hello required parameters.</span></span>
* <span data-ttu-id="5f7ba-113">[Utilisez le JSON brut fichiers ce processus de le VMAccess Extension hello](#use-json-files-and-the-vmaccess-extension) et ensuite agir sur.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-113">[Use raw JSON files that hello VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="5f7ba-114">Hello suivant l’utilisation d’exemples [utilisateur de machine virtuelle az](/cli/azure/vm/user) commandes.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-114">hello following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="5f7ba-115">tooperform ces étapes, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="5f7ba-115">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="5f7ba-116">Réinitialisation d’une clé SSH</span><span class="sxs-lookup"><span data-stu-id="5f7ba-116">Reset SSH key</span></span>
<span data-ttu-id="5f7ba-117">Hello exemple suivant réinitialise la clé SSH hello pour l’utilisateur de hello `azureuser` sur hello ordinateur virtuel nommé `myVM`:</span><span class="sxs-lookup"><span data-stu-id="5f7ba-117">hello following example resets hello SSH key for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="5f7ba-118">Réinitialiser le mot de passe</span><span class="sxs-lookup"><span data-stu-id="5f7ba-118">Reset password</span></span>
<span data-ttu-id="5f7ba-119">Hello exemple suivant réinitialise hello de mot de passe pour l’utilisateur de hello `azureuser` sur hello ordinateur virtuel nommé `myVM`:</span><span class="sxs-lookup"><span data-stu-id="5f7ba-119">hello following example resets hello password for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="5f7ba-120">Redémarrer SSH</span><span class="sxs-lookup"><span data-stu-id="5f7ba-120">Restart SSH</span></span>
<span data-ttu-id="5f7ba-121">exemple Hello redémarre démon SSH hello et réinitialise hello des valeurs de toodefault configuration SSH sur un ordinateur virtuel nommé `myVM`:</span><span class="sxs-lookup"><span data-stu-id="5f7ba-121">hello following example restarts hello SSH daemon and resets hello SSH configuration toodefault values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="5f7ba-122">Créer un utilisateur</span><span class="sxs-lookup"><span data-stu-id="5f7ba-122">Create a user</span></span>
<span data-ttu-id="5f7ba-123">Hello exemple suivant crée un utilisateur nommé `myNewUser` à l’aide d’une clé SSH pour l’authentification sur hello ordinateur virtuel nommé `myVM`:</span><span class="sxs-lookup"><span data-stu-id="5f7ba-123">hello following example creates a user named `myNewUser` using an SSH key for authentication on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="5f7ba-124">Supprimer un utilisateur</span><span class="sxs-lookup"><span data-stu-id="5f7ba-124">Delete a user</span></span>
<span data-ttu-id="5f7ba-125">Hello exemple suivant supprime un utilisateur nommé `myNewUser` sur hello ordinateur virtuel nommé `myVM`:</span><span class="sxs-lookup"><span data-stu-id="5f7ba-125">hello following example deletes a user named `myNewUser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a><span data-ttu-id="5f7ba-126">Utiliser des fichiers au format JSON et hello VMAccess Extension</span><span class="sxs-lookup"><span data-stu-id="5f7ba-126">Use JSON files and hello VMAccess Extension</span></span>
<span data-ttu-id="5f7ba-127">Hello suivant exemples utiliser des fichiers bruts JSON.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-127">hello following examples use raw JSON files.</span></span> <span data-ttu-id="5f7ba-128">Utilisez [az vm extension ensemble](/cli/azure/vm/extension#set) toothen appeler vos fichiers JSON.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-128">Use [az vm extension set](/cli/azure/vm/extension#set) toothen call your JSON files.</span></span> <span data-ttu-id="5f7ba-129">Ces fichiers JSON peuvent également être appelés à partir de modèles Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="5f7ba-130">Réinitialisation de l’accès utilisateur</span><span class="sxs-lookup"><span data-stu-id="5f7ba-130">Reset user access</span></span>
<span data-ttu-id="5f7ba-131">Si vous avez perdu l’accès tooroot sur votre VM Linux, vous pouvez lancer une tooreset de script VMAccess clé SSH ou le mot de passe d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-131">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset a user's SSH key or password.</span></span>

<span data-ttu-id="5f7ba-132">tooreset hello la clé publique SSH d’un utilisateur, créez un fichier nommé `reset_ssh_key.json` et ajouter des paramètres dans hello suivant le format.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-132">tooreset hello SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in hello following format.</span></span> <span data-ttu-id="5f7ba-133">Remplacez par vos propres valeurs hello `username` et `ssh_key` paramètres :</span><span class="sxs-lookup"><span data-stu-id="5f7ba-133">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="5f7ba-134">Exécutez le script de VMAccess hello avec :</span><span class="sxs-lookup"><span data-stu-id="5f7ba-134">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="5f7ba-135">tooreset un mot de passe utilisateur, créez un fichier nommé `reset_user_password.json` et ajouter des paramètres dans hello suivant le format.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-135">tooreset a user password, create a file named `reset_user_password.json` and add settings in hello following format.</span></span> <span data-ttu-id="5f7ba-136">Remplacez par vos propres valeurs hello `username` et `password` paramètres :</span><span class="sxs-lookup"><span data-stu-id="5f7ba-136">Substitute your own values for hello `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="5f7ba-137">Exécutez le script de VMAccess hello avec :</span><span class="sxs-lookup"><span data-stu-id="5f7ba-137">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="5f7ba-138">Redémarrer SSH</span><span class="sxs-lookup"><span data-stu-id="5f7ba-138">Restart SSH</span></span>
<span data-ttu-id="5f7ba-139">toorestart hello démon SSH et réinitialiser les valeurs de toodefault configuration hello SSH, créez un fichier nommé `reset_sshd.json`.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-139">toorestart hello SSH daemon and reset hello SSH configuration toodefault values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="5f7ba-140">Ajoutez hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="5f7ba-140">Add hello following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="5f7ba-141">Exécutez le script de VMAccess hello avec :</span><span class="sxs-lookup"><span data-stu-id="5f7ba-141">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="5f7ba-142">Gestion des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="5f7ba-142">Manage users</span></span>

<span data-ttu-id="5f7ba-143">toocreate un utilisateur qui utilise une clé SSH pour l’authentification, créez un fichier nommé `create_new_user.json` et ajouter des paramètres dans hello suivant le format.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-143">toocreate a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in hello following format.</span></span> <span data-ttu-id="5f7ba-144">Remplacez par vos propres valeurs hello `username` et `ssh_key` paramètres :</span><span class="sxs-lookup"><span data-stu-id="5f7ba-144">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="5f7ba-145">Exécutez le script de VMAccess hello avec :</span><span class="sxs-lookup"><span data-stu-id="5f7ba-145">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="5f7ba-146">toodelete un utilisateur, créez un fichier nommé `delete_user.json` et ajoutez hello suivant le contenu.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-146">toodelete a user, create a file named `delete_user.json` and add hello following content.</span></span> <span data-ttu-id="5f7ba-147">Remplacez par votre propre valeur pour hello `remove_user` paramètre :</span><span class="sxs-lookup"><span data-stu-id="5f7ba-147">Substitute your own value for hello `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="5f7ba-148">Exécutez le script de VMAccess hello avec :</span><span class="sxs-lookup"><span data-stu-id="5f7ba-148">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a><span data-ttu-id="5f7ba-149">Vérifiez ou réparez hello disque</span><span class="sxs-lookup"><span data-stu-id="5f7ba-149">Check or repair hello disk</span></span>
<span data-ttu-id="5f7ba-150">L’utilisation de VMAccess vous pouvez également vérifier et réparer un disque que vous avez ajouté toohello Linux VM.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-150">Using VMAccess you can also check and repair a disk that you added toohello Linux VM.</span></span>

<span data-ttu-id="5f7ba-151">toocheck, puis hello disquette, créez un fichier nommé `disk_check_repair.json` et ajouter des paramètres dans hello suivant le format.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-151">toocheck and then repair hello disk, create a file named `disk_check_repair.json` and add settings in hello following format.</span></span> <span data-ttu-id="5f7ba-152">Remplacez par votre propre valeur pour nom hello de `repair_disk`:</span><span class="sxs-lookup"><span data-stu-id="5f7ba-152">Substitute your own value for hello name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="5f7ba-153">Exécutez le script de VMAccess hello avec :</span><span class="sxs-lookup"><span data-stu-id="5f7ba-153">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="5f7ba-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5f7ba-154">Next steps</span></span>
<span data-ttu-id="5f7ba-155">Mise à jour de Linux à l’aide de hello le VMAccess Extension Azure est une méthode toomake change sur une VM Linux en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-155">Updating Linux using hello Azure VMAccess Extension is one method toomake changes on a running Linux VM.</span></span> <span data-ttu-id="5f7ba-156">Vous pouvez également utiliser des outils tels que le cloud-init et toomodify de modèles Azure Resource Manager votre VM Linux au démarrage du système.</span><span class="sxs-lookup"><span data-stu-id="5f7ba-156">You can also use tools like cloud-init and Azure Resource Manager templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="5f7ba-157">Extensions et fonctionnalités de machine virtuelle pour Linux</span><span class="sxs-lookup"><span data-stu-id="5f7ba-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="5f7ba-158">Création de modèles Azure Resource Manager avec des extensions de machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="5f7ba-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="5f7ba-159">Lors de la création à l’aide de cloud-init toocustomize un VM Linux</span><span class="sxs-lookup"><span data-stu-id="5f7ba-159">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md)

