---
title: "aaaMount stockage de fichier Azure sur les machines virtuelles Linux à l’aide de SMB avec Azure CLI 1.0 | Documents Microsoft"
description: "Comment toomount stockage de fichier Azure sur les machines virtuelles Linux à l’aide de SMB"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="320dc-103">Montage du Stockage Fichier Azure sur les machines virtuelles Linux à l’aide de SMB avec Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="320dc-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="320dc-104">Cet article explique comment toomount stockage de fichier Azure sur un VM Linux à l’aide de hello les protocole Server Message Block (SMB).</span><span class="sxs-lookup"><span data-stu-id="320dc-104">This article shows how toomount Azure File storage on a Linux VM by using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="320dc-105">Stockage de fichiers offre des partages de fichiers dans le cloud hello via le protocole SMB standard hello.</span><span class="sxs-lookup"><span data-stu-id="320dc-105">File storage offers file shares in hello cloud via hello standard SMB protocol.</span></span> <span data-ttu-id="320dc-106">spécifications de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="320dc-106">hello requirements are:</span></span>

* <span data-ttu-id="320dc-107">un [compte Azure](https://azure.microsoft.com/pricing/free-trial/) ;</span><span class="sxs-lookup"><span data-stu-id="320dc-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* <span data-ttu-id="320dc-108">[des fichiers de clés SSH (Secure Shell) publiques et privées](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="320dc-108">[Secure Shell (SSH) public and private key files](mac-create-ssh-keys.md)</span></span>

## <a name="cli-versions-toouse"></a><span data-ttu-id="320dc-109">Toouse des versions CLI</span><span class="sxs-lookup"><span data-stu-id="320dc-109">CLI versions toouse</span></span>
<span data-ttu-id="320dc-110">Vous pouvez exécuter la tâche hello en utilisant l’une de hello versions de l’interface de ligne de commande (CLI) suivantes :</span><span class="sxs-lookup"><span data-stu-id="320dc-110">You can complete hello task by using one of hello following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="320dc-111">[Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="320dc-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="320dc-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="320dc-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="320dc-113">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="320dc-113">Quick commands</span></span>
<span data-ttu-id="320dc-114">tâche de hello tooaccomplish rapidement, les étapes hello dans cette section.</span><span class="sxs-lookup"><span data-stu-id="320dc-114">tooaccomplish hello task quickly, follow hello steps in this section.</span></span> <span data-ttu-id="320dc-115">Pour plus d’informations et le contexte, commencent à hello [« Détaillée »](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span><span class="sxs-lookup"><span data-stu-id="320dc-115">For more detailed information and context, begin at hello ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="320dc-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="320dc-116">Prerequisites</span></span>
* <span data-ttu-id="320dc-117">un groupe de ressources ;</span><span class="sxs-lookup"><span data-stu-id="320dc-117">A resource group</span></span>
* <span data-ttu-id="320dc-118">Un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="320dc-118">An Azure virtual network</span></span>
* <span data-ttu-id="320dc-119">Un groupe de sécurité réseau avec une connexion SSH entrante.</span><span class="sxs-lookup"><span data-stu-id="320dc-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="320dc-120">Un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="320dc-120">A subnet</span></span>
* <span data-ttu-id="320dc-121">Un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="320dc-121">An Azure storage account</span></span>
* <span data-ttu-id="320dc-122">Des clés de compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="320dc-122">Azure storage account keys</span></span>
* <span data-ttu-id="320dc-123">Un partage de stockage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="320dc-123">An Azure File storage share</span></span>
* <span data-ttu-id="320dc-124">Une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="320dc-124">A Linux VM</span></span>

<span data-ttu-id="320dc-125">Remplacez les exemples par vos propres paramètres.</span><span class="sxs-lookup"><span data-stu-id="320dc-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="320dc-126">Créez un répertoire de montage local de hello</span><span class="sxs-lookup"><span data-stu-id="320dc-126">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="320dc-127">Monter le point de montage hello fichier stockage SMB partage toohello</span><span class="sxs-lookup"><span data-stu-id="320dc-127">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="320dc-128">Conserver le montage de hello après un redémarrage</span><span class="sxs-lookup"><span data-stu-id="320dc-128">Persist hello mount after a reboot</span></span>
<span data-ttu-id="320dc-129">Ajouter hello suivant ligne trop`/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="320dc-129">Add hello following line too`/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="320dc-130">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="320dc-130">Detailed walkthrough</span></span>

<span data-ttu-id="320dc-131">Stockage de fichiers offre des partages de fichiers dans le cloud de hello qui utilisent le protocole SMB standard de hello.</span><span class="sxs-lookup"><span data-stu-id="320dc-131">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="320dc-132">Avec la version la plus récente hello de stockage de fichiers, vous pouvez également monter un partage de fichiers à partir de n’importe quel système d’exploitation qui prend en charge SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="320dc-132">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="320dc-133">Lorsque vous utilisez un montage SMB sur Linux, vous obtenez sauvegardes tooa robustes et permanente d’archivage emplacement de stockage qui est pris en charge par un contrat SLA.</span><span class="sxs-lookup"><span data-stu-id="320dc-133">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="320dc-134">Déplacement des fichiers à partir d’un montage SMB tooan machine virtuelle qui est hébergé sur le stockage de fichiers est qu'un excellent moyen toodebug se connecte.</span><span class="sxs-lookup"><span data-stu-id="320dc-134">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="320dc-135">C’est parce que hello partage SMB même peut être monté localement tooyour Mac, Linux ou Windows station de travail.</span><span class="sxs-lookup"><span data-stu-id="320dc-135">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="320dc-136">SMB n’est pas la meilleure solution pour Linux de diffusion en continu de hello ou de journaux des applications en temps réel, car hello protocole SMB n’est pas généré toohandle ces droits journalisation lourde.</span><span class="sxs-lookup"><span data-stu-id="320dc-136">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="320dc-137">Un outil de couche de journalisation unifié et dédié comme Fluentd resprésente un meilleur choix que SMB pour collecter la sortie de journalisation d’applications et Linux.</span><span class="sxs-lookup"><span data-stu-id="320dc-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="320dc-138">Pour cette procédure pas à pas détaillées, nous créer les conditions préalables à hello nécessaires toofirst création du partage de stockage de fichier hello et puis montez via SMB sur un VM Linux.</span><span class="sxs-lookup"><span data-stu-id="320dc-138">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="320dc-139">Créer un compte de stockage Azure à l’aide de hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="320dc-139">Create an Azure storage account by using hello following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="320dc-140">Afficher les clés de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="320dc-140">Show hello storage account keys.</span></span>

    <span data-ttu-id="320dc-141">Lorsque vous créez un compte de stockage, les clés de compte hello sont créés dans les paires afin qu’ils peuvent être pivotées sans aucune interruption de service.</span><span class="sxs-lookup"><span data-stu-id="320dc-141">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="320dc-142">Lorsque vous basculez toohello deuxième clé de la paire de hello, vous créez une nouvelle paire de clés.</span><span class="sxs-lookup"><span data-stu-id="320dc-142">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="320dc-143">Nouvelles clés de compte de stockage sont toujours créés par paires, s’assurer que vous disposez toujours au moins un tooswitch prêt clé stockage inutilisé à.</span><span class="sxs-lookup"><span data-stu-id="320dc-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready tooswitch to.</span></span> <span data-ttu-id="320dc-144">clés de compte de stockage tooshow hello, utilisez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="320dc-144">tooshow hello storage account keys, use hello following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="320dc-145">Création du partage de stockage de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="320dc-145">Create hello File storage share.</span></span>

    <span data-ttu-id="320dc-146">partage de fichiers de stockage Hello contient le partage SMB hello.</span><span class="sxs-lookup"><span data-stu-id="320dc-146">hello File storage share contains hello SMB share.</span></span> <span data-ttu-id="320dc-147">quota de Hello est toujours exprimée en gigaoctets (Go).</span><span class="sxs-lookup"><span data-stu-id="320dc-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="320dc-148">toocreate hello du partage de fichiers de stockage, utilisez les hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="320dc-148">toocreate hello File storage share, use hello following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="320dc-149">Créer le répertoire de point de montage hello.</span><span class="sxs-lookup"><span data-stu-id="320dc-149">Create hello mount-point directory.</span></span>

    <span data-ttu-id="320dc-150">Vous devez créer un répertoire local dans hello toomount hello Linux fichier système partage SMB.</span><span class="sxs-lookup"><span data-stu-id="320dc-150">You must create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="320dc-151">Rien écrire ou lire à partir du répertoire de montage local hello est transféré toohello partage SMB qui est hébergé sur le stockage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="320dc-151">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="320dc-152">répertoire de hello toocreate, hello utilisation suivante du code :</span><span class="sxs-lookup"><span data-stu-id="320dc-152">toocreate hello directory, use hello following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="320dc-153">Montez hello partage SMB à l’aide de hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="320dc-153">Mount hello SMB share by using hello following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="320dc-154">Hello SMB de montage de redémarrages de persistance.</span><span class="sxs-lookup"><span data-stu-id="320dc-154">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="320dc-155">Lorsque vous redémarrez hello Linux VM, hello monté partage SMB est démonté lors de l’arrêt.</span><span class="sxs-lookup"><span data-stu-id="320dc-155">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="320dc-156">tooremount le partage SMB hello au démarrage du système, vous devez ajouter une ligne de toohello/etc/fstab Linux.</span><span class="sxs-lookup"><span data-stu-id="320dc-156">tooremount hello SMB share on boot, you must add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="320dc-157">Linux utilise hello fstab fichier toolist hello systèmes de fichiers qu’il doit toomount pendant le processus de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="320dc-157">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="320dc-158">Ajouter le partage SMB hello garantit que ce partage de stockage de fichier hello est un système de fichiers monté définitivement pour hello Linux VM.</span><span class="sxs-lookup"><span data-stu-id="320dc-158">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="320dc-159">Hello fichier stockage SMB partage tooa nouvel ordinateur virtuel est possible d’ajouter lorsque vous utilisez init-cloud.</span><span class="sxs-lookup"><span data-stu-id="320dc-159">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="320dc-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="320dc-160">Next steps</span></span>

- [<span data-ttu-id="320dc-161">Lors de la création à l’aide de cloud-init toocustomize un VM Linux</span><span class="sxs-lookup"><span data-stu-id="320dc-161">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="320dc-162">Ajouter un tooa de disque Linux VM</span><span class="sxs-lookup"><span data-stu-id="320dc-162">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="320dc-163">Chiffrer les disques sur un VM Linux à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="320dc-163">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
