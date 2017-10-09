---
title: "accès aaaReset sur l’utilisation de machines virtuelles de Azure Linux hello VMAccess Extension | Documents Microsoft"
description: "Réinitialisez l’accès sur les ordinateurs virtuels Linux de Azure à l’aide de hello VMAccess Extension."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a><span data-ttu-id="42b36-103">Gérer les utilisateurs, SSH et vérification ou de disquettes de réparation sur les machines virtuelles Azure Linux à l’aide de bienvenue de le VMAccess Extension avec hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="42b36-103">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="42b36-104">Cet article vous explique comment toouse hello Azure VMAcesss Extension toocheck ou réparer un disque, réinitialisez l’accès de l’utilisateur, gérer les comptes d’utilisateur ou réinitialiser la configuration de SSHD hello sur Linux.</span><span class="sxs-lookup"><span data-stu-id="42b36-104">This article shows you how toouse hello Azure VMAcesss Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSHD configuration on Linux.</span></span> <span data-ttu-id="42b36-105">article de Hello nécessite :</span><span class="sxs-lookup"><span data-stu-id="42b36-105">hello article requires:</span></span>

* <span data-ttu-id="42b36-106">un compte Azure ([obtenir un essai gratuit](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="42b36-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="42b36-107">Hello [CLI d’Azure](../../cli-install-nodejs.md) connecté `azure login`.</span><span class="sxs-lookup"><span data-stu-id="42b36-107">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="42b36-108">Hello CLI d’Azure *doit se trouver dans* mode Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="42b36-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="42b36-109">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="42b36-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="42b36-110">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="42b36-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="42b36-111">[Azure CLI 1.0](#quick-commands)– notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="42b36-111">[Azure CLI 1.0](#quick-commands)– our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="42b36-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="42b36-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="42b36-113">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="42b36-113">Quick commands</span></span>
<span data-ttu-id="42b36-114">Il existe deux façons toouse VMAccess sur vos machines virtuelles Linux :</span><span class="sxs-lookup"><span data-stu-id="42b36-114">There are two ways toouse VMAccess on your Linux VMs:</span></span>

* <span data-ttu-id="42b36-115">À l’aide de hello Azure CLI 1.0 et hello les paramètres requis.</span><span class="sxs-lookup"><span data-stu-id="42b36-115">Using hello Azure CLI 1.0 and hello required parameters.</span></span>
* <span data-ttu-id="42b36-116">À l’aide de fichiers JSON bruts que VMAccess traite et exploite.</span><span class="sxs-lookup"><span data-stu-id="42b36-116">Using raw JSON files that VMAccess processes and then act on.</span></span>

<span data-ttu-id="42b36-117">Section de commande rapide hello, nous allons toouse hello Azure CLI 1.0 `azure vm reset-access` (méthode).</span><span class="sxs-lookup"><span data-stu-id="42b36-117">For hello quick command section, we are going toouse hello Azure CLI 1.0 `azure vm reset-access` method.</span></span> <span data-ttu-id="42b36-118">Bonjour des exemples de commandes suivante, remplacez les valeurs de hello qui contiennent « exemple » avec des valeurs hello à partir de votre propre environnement.</span><span class="sxs-lookup"><span data-stu-id="42b36-118">In hello following command examples, replace hello values that contain "example" with hello values from your own environment.</span></span>

## <a name="create-a-resource-group-and-linux-vm"></a><span data-ttu-id="42b36-119">Création d'un groupe de ressources et d’une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="42b36-119">Create a Resource Group and Linux VM</span></span>
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a><span data-ttu-id="42b36-120">Création d’une machine virtuelle Debian</span><span class="sxs-lookup"><span data-stu-id="42b36-120">Create a Debian VM</span></span>
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a><span data-ttu-id="42b36-121">Réinitialisation du mot de passe racine</span><span class="sxs-lookup"><span data-stu-id="42b36-121">Reset root password</span></span>
<span data-ttu-id="42b36-122">mot de passe tooreset hello racine :</span><span class="sxs-lookup"><span data-stu-id="42b36-122">tooreset hello root password:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a><span data-ttu-id="42b36-123">Réinitialisation de la clé SSH</span><span class="sxs-lookup"><span data-stu-id="42b36-123">SSH key reset</span></span>
<span data-ttu-id="42b36-124">tooreset hello code SSH d’un utilisateur non racine :</span><span class="sxs-lookup"><span data-stu-id="42b36-124">tooreset hello SSH key of a non-root user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a><span data-ttu-id="42b36-125">Créer un utilisateur</span><span class="sxs-lookup"><span data-stu-id="42b36-125">Create a user</span></span>
<span data-ttu-id="42b36-126">toocreate un utilisateur :</span><span class="sxs-lookup"><span data-stu-id="42b36-126">toocreate a user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a><span data-ttu-id="42b36-127">Supprimer un utilisateur</span><span class="sxs-lookup"><span data-stu-id="42b36-127">Remove a user</span></span>
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a><span data-ttu-id="42b36-128">Réinitialiser SSHD</span><span class="sxs-lookup"><span data-stu-id="42b36-128">Reset SSHD</span></span>
<span data-ttu-id="42b36-129">configuration de SSHD tooreset hello :</span><span class="sxs-lookup"><span data-stu-id="42b36-129">tooreset hello SSHD configuration:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a><span data-ttu-id="42b36-130">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="42b36-130">Detailed walkthrough</span></span>
### <a name="vmaccess-defined"></a><span data-ttu-id="42b36-131">VMAccess défini :</span><span class="sxs-lookup"><span data-stu-id="42b36-131">VMAccess defined:</span></span>
<span data-ttu-id="42b36-132">disque Hello sur votre VM Linux affichant les erreurs.</span><span class="sxs-lookup"><span data-stu-id="42b36-132">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="42b36-133">Vous une certaine manière réinitialisez le mot de passe racine hello pour votre VM Linux ou accidentellement votre clé privée SSH.</span><span class="sxs-lookup"><span data-stu-id="42b36-133">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="42b36-134">Si cela se produisait dans jours hello de centre de données hello, vous devez toodrive il et puis ouvrez tooget KVM hello sur la console serveur hello.</span><span class="sxs-lookup"><span data-stu-id="42b36-134">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="42b36-135">Considérer hello extension VMAccess de Azure en tant que ce commutateur qui vous permet de tooaccess hello console tooreset accès tooLinux ou effectuez une maintenance au niveau du disque.</span><span class="sxs-lookup"><span data-stu-id="42b36-135">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="42b36-136">Pour hello plus procédure pas à pas, nous allons la forme longue de hello toouse de VMAccess, qui utilise des fichiers bruts JSON.</span><span class="sxs-lookup"><span data-stu-id="42b36-136">For hello detailed walkthrough, we are going toouse hello long form of VMAccess, which uses raw JSON files.</span></span>  <span data-ttu-id="42b36-137">Ces fichiers JSON VMAccess peuvent également être appelés à partir de modèles Azure.</span><span class="sxs-lookup"><span data-stu-id="42b36-137">These VMAccess JSON files can also be called from Azure templates.</span></span>

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a><span data-ttu-id="42b36-138">À l’aide de VMAccess toocheck ou la réparation du disque hello d’un VM Linux</span><span class="sxs-lookup"><span data-stu-id="42b36-138">Using VMAccess toocheck or repair hello disk of a Linux VM</span></span>
<span data-ttu-id="42b36-139">L’utilisation de VMAccess vous pouvez effectuer un fsck s’exécutent sur le disque hello sous votre VM Linux.</span><span class="sxs-lookup"><span data-stu-id="42b36-139">Using VMAccess you can do a fsck run on hello disk under your Linux VM.</span></span>  <span data-ttu-id="42b36-140">Vous pouvez également effectuer une vérification de disque et une réparation de disque à l’aide d’un VMAccess.</span><span class="sxs-lookup"><span data-stu-id="42b36-140">You can also do a disk check and a disk repair using a VMAccess.</span></span>

<span data-ttu-id="42b36-141">toocheck, puis sur Réparer hello disque utiliser ce script VMAccess :</span><span class="sxs-lookup"><span data-stu-id="42b36-141">toocheck, and then repair hello disk use this VMAccess script:</span></span>

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

<span data-ttu-id="42b36-142">Exécutez le script de VMAccess hello avec :</span><span class="sxs-lookup"><span data-stu-id="42b36-142">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a><span data-ttu-id="42b36-143">À l’aide de VMAccess tooreset utilisateur accès tooLinux</span><span class="sxs-lookup"><span data-stu-id="42b36-143">Using VMAccess tooreset user access tooLinux</span></span>
<span data-ttu-id="42b36-144">Si vous avez perdu l’accès tooroot sur votre VM Linux, vous pouvez lancer un VMAccess script tooreset hello mot de passe racine.</span><span class="sxs-lookup"><span data-stu-id="42b36-144">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset hello root password.</span></span>

<span data-ttu-id="42b36-145">mot de passe tooreset hello racine, utilisez ce script VMAccess :</span><span class="sxs-lookup"><span data-stu-id="42b36-145">tooreset hello root password, use this VMAccess script:</span></span>

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

<span data-ttu-id="42b36-146">Exécutez le script de VMAccess hello avec :</span><span class="sxs-lookup"><span data-stu-id="42b36-146">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

<span data-ttu-id="42b36-147">la clé SSH hello tooreset d’un utilisateur non racine, utilisez ce script VMAccess :</span><span class="sxs-lookup"><span data-stu-id="42b36-147">tooreset hello SSH key of a non-root user, use this VMAccess script:</span></span>

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

<span data-ttu-id="42b36-148">Exécutez le script de VMAccess hello avec :</span><span class="sxs-lookup"><span data-stu-id="42b36-148">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a><span data-ttu-id="42b36-149">À l’aide de comptes d’utilisateur toomanage VMAccess sur Linux</span><span class="sxs-lookup"><span data-stu-id="42b36-149">Using VMAccess toomanage user accounts on Linux</span></span>
<span data-ttu-id="42b36-150">VMAccess est un script Python qui peut être des utilisateurs toomanage utilisés sur votre Linux VM sans connexion et à l’aide du compte de racine sudo ou hello.</span><span class="sxs-lookup"><span data-stu-id="42b36-150">VMAccess is a Python script that can be used toomanage users on your Linux VM without logging in and using sudo or hello root account.</span></span>

<span data-ttu-id="42b36-151">toocreate un utilisateur, utilisez ce script VMAccess :</span><span class="sxs-lookup"><span data-stu-id="42b36-151">toocreate a user, use this VMAccess script:</span></span>

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="42b36-152">Exécutez le script de VMAccess hello avec :</span><span class="sxs-lookup"><span data-stu-id="42b36-152">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

<span data-ttu-id="42b36-153">toodelete un utilisateur, utilisez ce script VMAccess :</span><span class="sxs-lookup"><span data-stu-id="42b36-153">toodelete a user, use this VMAccess script:</span></span>

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

<span data-ttu-id="42b36-154">Exécutez le script de VMAccess hello avec :</span><span class="sxs-lookup"><span data-stu-id="42b36-154">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a><span data-ttu-id="42b36-155">À l’aide de la configuration de VMAccess tooreset hello SSHD</span><span class="sxs-lookup"><span data-stu-id="42b36-155">Using VMAccess tooreset hello SSHD configuration</span></span>
<span data-ttu-id="42b36-156">Si vous effectuez la configuration de modifications toohello SSHD de machines virtuelles Linux et la connexion SSH hello fermer avant de vérifier les modifications de hello, vous ne puissent pas SSH'ing dans.</span><span class="sxs-lookup"><span data-stu-id="42b36-156">If you make changes toohello Linux VMs SSHD configuration and close hello SSH connection before verifying hello changes, you may be prevented from SSH'ing back in.</span></span>  <span data-ttu-id="42b36-157">VMAccess peut être utilisé tooreset hello SSHD configuration arrière tooa bonne configuration sans être connecté en via SSH.</span><span class="sxs-lookup"><span data-stu-id="42b36-157">VMAccess can be used tooreset hello SSHD configuration back tooa known good configuration without being logged in over SSH.</span></span>

<span data-ttu-id="42b36-158">configuration de SSHD hello tooreset utiliser ce script de VMAccess :</span><span class="sxs-lookup"><span data-stu-id="42b36-158">tooreset hello SSHD configuration use this VMAccess script:</span></span>

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="42b36-159">Exécutez le script de VMAccess hello avec :</span><span class="sxs-lookup"><span data-stu-id="42b36-159">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a><span data-ttu-id="42b36-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="42b36-160">Next steps</span></span>
<span data-ttu-id="42b36-161">Mise à jour de Linux à l’aide des Extensions de VMAccess Azure est une méthode toomake change sur une VM Linux en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="42b36-161">Updating Linux using Azure VMAccess Extensions is one method toomake changes on a running Linux VM.</span></span>  <span data-ttu-id="42b36-162">Vous pouvez également utiliser des outils tels qu’init de cloud et les modèles Azure toomodify votre VM Linux au démarrage du système.</span><span class="sxs-lookup"><span data-stu-id="42b36-162">You can also use tools like cloud-init and Azure Templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="42b36-163">À propos des extensions et des fonctionnalités des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="42b36-163">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="42b36-164">Création de modèles Azure Resource Manager avec des extensions de machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="42b36-164">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="42b36-165">Lors de la création à l’aide de cloud-init toocustomize un VM Linux</span><span class="sxs-lookup"><span data-stu-id="42b36-165">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

