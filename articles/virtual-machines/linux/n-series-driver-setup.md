---
title: "le programme d’installation d’aaaAzure N-series pilote pour Linux | Documents Microsoft"
description: "Comment tooset les pilotes NVIDIA GPU pour les machines virtuelles de série N Linux en cours d’exécution dans Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d91695d0-64b9-4e6b-84bd-18401eaecdde
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7db1b3859f9075c6d9f0319f39418946ea08743f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="62ba2-103">Installer les pilotes GPU NVIDIA sur les machines virtuelles série N exécutant Linux</span><span class="sxs-lookup"><span data-stu-id="62ba2-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="62ba2-104">avantage tootake hello GPU des fonctionnalités de N-series Azure installation ordinateurs virtuels exécutant Linux, prise en charge des pilotes de graphiques NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="62ba2-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="62ba2-105">Cet article vous offre des étapes de configuration de pilote lorsque vous avez déployé une machine virtuelle de série N.</span><span class="sxs-lookup"><span data-stu-id="62ba2-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="62ba2-106">Des informations de configuration du pilote sont également disponibles pour [les machines virtuelles Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62ba2-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="62ba2-107">Pour plus d’informations sur les spécifications, les capacités de stockage et les disques des machines virtuelles série N, consultez l’article [Tailles de machine virtuelle Linux GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62ba2-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="62ba2-108">Installer les pilotes GRID pour les machines virtuelles NV</span><span class="sxs-lookup"><span data-stu-id="62ba2-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="62ba2-109">pilotes de NVIDIA grille tooinstall sur des machines virtuelles NV, rendre un tooeach de connexion SSH VM et suivez les étapes de hello pour votre distribution Linux.</span><span class="sxs-lookup"><span data-stu-id="62ba2-109">tooinstall NVIDIA GRID drivers on NV VMs, make an SSH connection tooeach VM and follow hello steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="62ba2-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="62ba2-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="62ba2-111">Exécutez hello `lspci` commande.</span><span class="sxs-lookup"><span data-stu-id="62ba2-111">Run hello `lspci` command.</span></span> <span data-ttu-id="62ba2-112">Vérifiez que la carte de hello NVIDIA M60 ou cartes sont visibles en tant que périphériques PCI.</span><span class="sxs-lookup"><span data-stu-id="62ba2-112">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="62ba2-113">Installez les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="62ba2-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="62ba2-114">Désactiver les pilotes de noyau Nouveau hello, qui est incompatible avec le pilote NVIDIA hello.</span><span class="sxs-lookup"><span data-stu-id="62ba2-114">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="62ba2-115">(Utilisez uniquement pilote NVIDIA hello sur des machines virtuelles de NV.) toodo, créez un fichier dans `/etc/modprobe.d `nommé `nouveau.conf` avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="62ba2-115">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="62ba2-116">Redémarrez hello machine virtuelle et vous reconnecter.</span><span class="sxs-lookup"><span data-stu-id="62ba2-116">Reboot hello VM and reconnect.</span></span> <span data-ttu-id="62ba2-117">Quittez le serveur X :</span><span class="sxs-lookup"><span data-stu-id="62ba2-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="62ba2-118">Téléchargez et installez le pilote de grille hello :</span><span class="sxs-lookup"><span data-stu-id="62ba2-118">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="62ba2-119">Lorsque vous êtes invité à confirmer toorun hello nvidia-xconfig utilitaire tooupdate votre fichier de configuration de X, sélectionnez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="62ba2-119">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="62ba2-120">Une fois l’installation terminée, copiez /etc/nvidia/gridd.conf.template tooa nouveau fichier gridd.conf à l’emplacement etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="62ba2-120">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="62ba2-121">Ajouter hello suivant trop`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="62ba2-121">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="62ba2-122">Redémarrez hello machine virtuelle et poursuivre l’installation de hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="62ba2-122">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="62ba2-123">Basé sur CentOS 7.3 ou Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="62ba2-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="62ba2-124">Mettre à jour le noyau de hello et DKMS.</span><span class="sxs-lookup"><span data-stu-id="62ba2-124">Update hello kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="62ba2-125">Désactiver les pilotes de noyau Nouveau hello, qui est incompatible avec le pilote NVIDIA hello.</span><span class="sxs-lookup"><span data-stu-id="62ba2-125">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="62ba2-126">(Utilisez uniquement pilote NVIDIA hello sur des machines virtuelles de NV.) toodo, créez un fichier dans `/etc/modprobe.d `nommé `nouveau.conf` avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="62ba2-126">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="62ba2-127">Redémarrez hello machine virtuelle, vous reconnecter et installer hello les derniers Services d’intégration Linux pour Hyper-v :</span><span class="sxs-lookup"><span data-stu-id="62ba2-127">Reboot hello VM, reconnect, and install hello latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="62ba2-128">Reconnecter toohello machine virtuelle et exécutez hello `lspci` commande.</span><span class="sxs-lookup"><span data-stu-id="62ba2-128">Reconnect toohello VM and run hello `lspci` command.</span></span> <span data-ttu-id="62ba2-129">Vérifiez que la carte de hello NVIDIA M60 ou cartes sont visibles en tant que périphériques PCI.</span><span class="sxs-lookup"><span data-stu-id="62ba2-129">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="62ba2-130">Téléchargez et installez le pilote de grille hello :</span><span class="sxs-lookup"><span data-stu-id="62ba2-130">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="62ba2-131">Lorsque vous êtes invité à confirmer toorun hello nvidia-xconfig utilitaire tooupdate votre fichier de configuration de X, sélectionnez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="62ba2-131">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="62ba2-132">Une fois l’installation terminée, copiez /etc/nvidia/gridd.conf.template tooa nouveau fichier gridd.conf à l’emplacement etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="62ba2-132">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="62ba2-133">Ajouter hello suivant trop`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="62ba2-133">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="62ba2-134">Redémarrez hello machine virtuelle et poursuivre l’installation de hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="62ba2-134">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="62ba2-135">Vérification de l’installation du pilote</span><span class="sxs-lookup"><span data-stu-id="62ba2-135">Verify driver installation</span></span>


<span data-ttu-id="62ba2-136">tooquery hello état du périphérique GPU, SSH toohello VM et exécution hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) utilitaire de ligne de commande installé avec le pilote de hello.</span><span class="sxs-lookup"><span data-stu-id="62ba2-136">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="62ba2-137">Suit toohello similaire de sortie s’affiche :</span><span class="sxs-lookup"><span data-stu-id="62ba2-137">Output similar toohello following appears:</span></span>

![État de l’appareil NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="62ba2-139">Serveur X11</span><span class="sxs-lookup"><span data-stu-id="62ba2-139">X11 server</span></span>
<span data-ttu-id="62ba2-140">Si vous avez besoin d’un X11 serveur pour les connexions à distance tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) est recommandée, car elle permet à l’accélération matérielle des graphiques.</span><span class="sxs-lookup"><span data-stu-id="62ba2-140">If you need an X11 server for remote connections tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="62ba2-141">Hello BusID du périphérique de hello M60 doit être ajoutée manuellement toohello xconfig fichier (`etc/X11/xorg.conf` sur Ubuntu 16.04 LTS, `/etc/X11/XF86config` sur CentOS 7.3 ou Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="62ba2-141">hello BusID of hello M60 device must be manually added toohello xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="62ba2-142">Ajouter un `"Device"` section similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="62ba2-142">Add a `"Device"` section similar toohello following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="62ba2-143">En outre, mettre à jour votre `"Screen"` section toouse cet appareil.</span><span class="sxs-lookup"><span data-stu-id="62ba2-143">Additionally, update your `"Screen"` section toouse this device.</span></span>
 
<span data-ttu-id="62ba2-144">Hello BusID accessibles en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="62ba2-144">hello BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="62ba2-145">Hello BusID peut changer lorsqu’une machine virtuelle obtient réaffectée ou redémarrée.</span><span class="sxs-lookup"><span data-stu-id="62ba2-145">hello BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="62ba2-146">Par conséquent, vous devrez toouse un Bonjour tooupdate de script BusID dans la configuration de hello X11 lors du redémarrage d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="62ba2-146">Therefore, you may want toouse a script tooupdate hello BusID in hello X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="62ba2-147">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="62ba2-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="62ba2-148">Ce fichier peut être appelé en tant que racine au démarrage en créant une entrée pour lui dans `/etc/rc.d/rc3.d`.</span><span class="sxs-lookup"><span data-stu-id="62ba2-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="62ba2-149">Installer des pilotes CUDA pour des machines virtuelles NC</span><span class="sxs-lookup"><span data-stu-id="62ba2-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="62ba2-150">Sont issues ici de pilotes NVIDIA tooinstall étapes sur les machines virtuelles Linux NC hello NVIDIA CUDA Toolkit 8.0.</span><span class="sxs-lookup"><span data-stu-id="62ba2-150">Here are steps tooinstall NVIDIA drivers on Linux NC VMs from hello NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="62ba2-151">Les développeurs C et C++ peuvent éventuellement installer des applications à accélération GPU de hello complètes Toolkit toobuild.</span><span class="sxs-lookup"><span data-stu-id="62ba2-151">C and C++ developers can optionally install hello full Toolkit toobuild GPU-accelerated applications.</span></span> <span data-ttu-id="62ba2-152">Pour plus d’informations, consultez hello [Guide d’Installation CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="62ba2-152">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="62ba2-153">Les liens de téléchargement de pilotes CUDA fournis ici sont à jour au moment de la publication.</span><span class="sxs-lookup"><span data-stu-id="62ba2-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="62ba2-154">Pour les derniers pilotes CUDA hello, visitez hello [NVIDIA](http://www.nvidia.com/) site Web.</span><span class="sxs-lookup"><span data-stu-id="62ba2-154">For hello latest CUDA drivers, visit hello [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="62ba2-155">tooinstall CUDA Toolkit, effectuez une tooeach de connexion SSH machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="62ba2-155">tooinstall CUDA Toolkit, make an SSH connection tooeach VM.</span></span> <span data-ttu-id="62ba2-156">tooverify qui hello système a un GPU compatible CUDA, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="62ba2-156">tooverify that hello system has a CUDA-capable GPU, run hello following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="62ba2-157">Vous verrez la sortie de toohello similaire (avec une carte NVIDIA Tesla K80) de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="62ba2-157">You will see output similar toohello following example (showing an NVIDIA Tesla K80 card):</span></span>

![Sortie de commande Ispci](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="62ba2-159">Ensuite, exécutez les commandes d’installation spécifiques de votre distribution.</span><span class="sxs-lookup"><span data-stu-id="62ba2-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="62ba2-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="62ba2-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="62ba2-161">Téléchargez et installez les pilotes CUDA hello.</span><span class="sxs-lookup"><span data-stu-id="62ba2-161">Download and install hello CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="62ba2-162">installation de Hello peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="62ba2-162">hello installation can take several minutes.</span></span>

2. <span data-ttu-id="62ba2-163">toooptionally installation hello complète CUDA toolkit, type :</span><span class="sxs-lookup"><span data-stu-id="62ba2-163">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="62ba2-164">Redémarrez hello machine virtuelle et poursuivre l’installation de hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="62ba2-164">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="62ba2-165">Basé sur CentOS 7.3 ou Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="62ba2-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="62ba2-166">Obtenez les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="62ba2-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="62ba2-167">Reconnecter toohello machine virtuelle et installer hello les derniers Services d’intégration Linux pour Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="62ba2-167">Reconnect toohello VM and install hello latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="62ba2-168">Si vous avez installé une image basée sur CentOS HPC sur une machine virtuelle NC24r, ignorez tooStep 3.</span><span class="sxs-lookup"><span data-stu-id="62ba2-168">If you installed a CentOS-based HPC image on an NC24r VM, skip tooStep 3.</span></span> <span data-ttu-id="62ba2-169">Étant donné que les pilotes RDMA Azure et les Services d’intégration Linux sont déjà installées dans hello image, LIS ne doit pas être mis à niveau et mises à jour du noyau sont désactivées par défaut.</span><span class="sxs-lookup"><span data-stu-id="62ba2-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in hello image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="62ba2-170">Reconnecter toohello machine virtuelle et poursuivre l’installation avec hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="62ba2-170">Reconnect toohello VM and continue installation with hello following commands:</span></span>

  ```bash
  sudo yum install kernel-devel

  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

  sudo yum install dkms

  CUDA_REPO_PKG=cuda-repo-rhel7-8.0.61-1.x86_64.rpm

  wget http://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/${CUDA_REPO_PKG} -O /tmp/${CUDA_REPO_PKG}

  sudo rpm -ivh /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo yum install cuda-drivers
  ```

  <span data-ttu-id="62ba2-171">installation de Hello peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="62ba2-171">hello installation can take several minutes.</span></span> 

4. <span data-ttu-id="62ba2-172">toooptionally installation hello complète CUDA toolkit, type :</span><span class="sxs-lookup"><span data-stu-id="62ba2-172">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="62ba2-173">Redémarrez hello machine virtuelle et poursuivre l’installation de hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="62ba2-173">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="62ba2-174">Vérification de l’installation du pilote</span><span class="sxs-lookup"><span data-stu-id="62ba2-174">Verify driver installation</span></span>


<span data-ttu-id="62ba2-175">tooquery hello état du périphérique GPU, SSH toohello VM et exécution hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) utilitaire de ligne de commande installé avec le pilote de hello.</span><span class="sxs-lookup"><span data-stu-id="62ba2-175">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="62ba2-176">Suit toohello similaire de sortie s’affiche :</span><span class="sxs-lookup"><span data-stu-id="62ba2-176">Output similar toohello following appears:</span></span>

![État de l’appareil NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="62ba2-178">Mises à jour de pilote CUDA</span><span class="sxs-lookup"><span data-stu-id="62ba2-178">CUDA driver updates</span></span>

<span data-ttu-id="62ba2-179">Nous vous recommandons de régulièrement mettre à jour les pilotes CUDA après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="62ba2-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="62ba2-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="62ba2-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="62ba2-181">Basé sur CentOS 7.3 ou Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="62ba2-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="62ba2-182">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="62ba2-182">Troubleshooting</span></span>

* <span data-ttu-id="62ba2-183">Il existe un problème connu avec les pilotes CUDA sur Azure série N machines virtuelles en cours d’exécution du noyau de Linux hello 4.4.0-75 sur Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="62ba2-183">There is a known issue with CUDA drivers on Azure N-series VMs running hello 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="62ba2-184">Si vous mettez à niveau à partir d’une version antérieure de noyau, mettre à niveau tooat moins 4.4.0-77 de version du noyau.</span><span class="sxs-lookup"><span data-stu-id="62ba2-184">If you are upgrading from an earlier kernel version, upgrade tooat least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="62ba2-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62ba2-185">Next steps</span></span>

* <span data-ttu-id="62ba2-186">Pour plus d’informations sur hello NVIDIA GPU sur hello machines virtuelles de série N, consultez :</span><span class="sxs-lookup"><span data-stu-id="62ba2-186">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="62ba2-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (pour les machines virtuelles NC Azure)</span><span class="sxs-lookup"><span data-stu-id="62ba2-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="62ba2-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (pour les machines virtuelles NV Azure)</span><span class="sxs-lookup"><span data-stu-id="62ba2-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="62ba2-189">toocapture une image Linux VM avec vos pilotes NVIDIA installés, consultez [comment toogeneralize et capturer une machine virtuelle Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62ba2-189">toocapture a Linux VM image with your installed NVIDIA drivers, see [How toogeneralize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
