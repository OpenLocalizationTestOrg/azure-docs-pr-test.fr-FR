---
title: "Configuration du pilote série N Azure pour Linux | Microsoft Docs"
description: "Procédure de configuration des pilotes GPU NVIDIA pour les machines virtuelles série N exécutant Linux dans Azure"
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
ms.openlocfilehash: bdeb4d5ca1d9ff4d7dfd0961690412dd7530572a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="c45c3-103">Installer les pilotes GPU NVIDIA sur les machines virtuelles série N exécutant Linux</span><span class="sxs-lookup"><span data-stu-id="c45c3-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="c45c3-104">Pour tirer parti des fonctionnalités GPU de machines virtuelles série N Azure exécutant Linux, installez des pilotes graphiques NVIDIA pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c45c3-104">To take advantage of the GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="c45c3-105">Cet article vous offre des étapes de configuration de pilote lorsque vous avez déployé une machine virtuelle de série N.</span><span class="sxs-lookup"><span data-stu-id="c45c3-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="c45c3-106">Des informations de configuration du pilote sont également disponibles pour [les machines virtuelles Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c45c3-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="c45c3-107">Pour plus d’informations sur les spécifications, les capacités de stockage et les disques des machines virtuelles série N, consultez l’article [Tailles de machine virtuelle Linux GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c45c3-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="c45c3-108">Installer les pilotes GRID pour les machines virtuelles NV</span><span class="sxs-lookup"><span data-stu-id="c45c3-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="c45c3-109">Pour installer les pilotes GRID NVIDIA sur des machines virtuelles NV, établissez une connexion SSH à chaque machine virtuelle et suivez les étapes de votre distribution Linux.</span><span class="sxs-lookup"><span data-stu-id="c45c3-109">To install NVIDIA GRID drivers on NV VMs, make an SSH connection to each VM and follow the steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="c45c3-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="c45c3-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="c45c3-111">Exécutez la commande `lspci`.</span><span class="sxs-lookup"><span data-stu-id="c45c3-111">Run the `lspci` command.</span></span> <span data-ttu-id="c45c3-112">Vérifiez que la ou les cartes NVIDIA M60 sont visibles en tant que périphériques PCI.</span><span class="sxs-lookup"><span data-stu-id="c45c3-112">Verify that the NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="c45c3-113">Installez les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="c45c3-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="c45c3-114">Désactivez le pilote du noyau Nouveau, qui n’est pas compatible avec le pilote NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="c45c3-114">Disable the Nouveau kernel driver, which is incompatible with the NVIDIA driver.</span></span> <span data-ttu-id="c45c3-115">(Utilisez uniquement le pilote NVIDIA sur les machines virtuelles NV.) Pour ce faire, créez un fichier `/etc/modprobe.d `nommé `nouveau.conf` avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="c45c3-115">(Only use the NVIDIA driver on NV VMs.) To do this, create a file in `/etc/modprobe.d `named `nouveau.conf` with the following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="c45c3-116">Redémarrez la machine virtuelle et reconnectez-vous.</span><span class="sxs-lookup"><span data-stu-id="c45c3-116">Reboot the VM and reconnect.</span></span> <span data-ttu-id="c45c3-117">Quittez le serveur X :</span><span class="sxs-lookup"><span data-stu-id="c45c3-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="c45c3-118">Téléchargez et installez le pilote GRID :</span><span class="sxs-lookup"><span data-stu-id="c45c3-118">Download and install the GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="c45c3-119">Lorsque vous êtes invité à indiquer si vous souhaitez exécuter l’utilitaire nvidia-xconfig pour mettre à jour votre fichier de configuration X, sélectionnez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="c45c3-119">When you're asked whether you want to run the nvidia-xconfig utility to update your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="c45c3-120">Une fois l’installation terminée, copiez /etc/nvidia/gridd.conf.template sur un nouveau fichier gridd.conf dà l’emplacement etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="c45c3-120">After installation completes, copy /etc/nvidia/gridd.conf.template to a new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="c45c3-121">Ajoutez la ligne suivante à `/etc/nvidia/gridd.conf` :</span><span class="sxs-lookup"><span data-stu-id="c45c3-121">Add the following to `/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="c45c3-122">Redémarrez la machine virtuelle et vérifiez l’installation.</span><span class="sxs-lookup"><span data-stu-id="c45c3-122">Reboot the VM and proceed to verify the installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="c45c3-123">Basé sur CentOS 7.3 ou Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="c45c3-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="c45c3-124">Mettez à jour le noyau et DKMS.</span><span class="sxs-lookup"><span data-stu-id="c45c3-124">Update the kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="c45c3-125">Désactivez le pilote du noyau Nouveau, qui n’est pas compatible avec le pilote NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="c45c3-125">Disable the Nouveau kernel driver, which is incompatible with the NVIDIA driver.</span></span> <span data-ttu-id="c45c3-126">(Utilisez uniquement le pilote NVIDIA sur les machines virtuelles NV.) Pour ce faire, créez un fichier `/etc/modprobe.d `nommé `nouveau.conf` avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="c45c3-126">(Only use the NVIDIA driver on NV VMs.) To do this, create a file in `/etc/modprobe.d `named `nouveau.conf` with the following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="c45c3-127">Redémarrez la machine virtuelle, reconnectez-vous et installez les derniers services d’intégration Linux pour Hyper-V :</span><span class="sxs-lookup"><span data-stu-id="c45c3-127">Reboot the VM, reconnect, and install the latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="c45c3-128">Reconnectez-vous à la machine virtuelle et exécutez la commande `lspci`.</span><span class="sxs-lookup"><span data-stu-id="c45c3-128">Reconnect to the VM and run the `lspci` command.</span></span> <span data-ttu-id="c45c3-129">Vérifiez que la ou les cartes NVIDIA M60 sont visibles en tant que périphériques PCI.</span><span class="sxs-lookup"><span data-stu-id="c45c3-129">Verify that the NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="c45c3-130">Téléchargez et installez le pilote GRID :</span><span class="sxs-lookup"><span data-stu-id="c45c3-130">Download and install the GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="c45c3-131">Lorsque vous êtes invité à indiquer si vous souhaitez exécuter l’utilitaire nvidia-xconfig pour mettre à jour votre fichier de configuration X, sélectionnez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="c45c3-131">When you're asked whether you want to run the nvidia-xconfig utility to update your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="c45c3-132">Une fois l’installation terminée, copiez /etc/nvidia/gridd.conf.template sur un nouveau fichier gridd.conf dà l’emplacement etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="c45c3-132">After installation completes, copy /etc/nvidia/gridd.conf.template to a new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="c45c3-133">Ajoutez la ligne suivante à `/etc/nvidia/gridd.conf` :</span><span class="sxs-lookup"><span data-stu-id="c45c3-133">Add the following to `/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="c45c3-134">Redémarrez la machine virtuelle et vérifiez l’installation.</span><span class="sxs-lookup"><span data-stu-id="c45c3-134">Reboot the VM and proceed to verify the installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="c45c3-135">Vérification de l’installation du pilote</span><span class="sxs-lookup"><span data-stu-id="c45c3-135">Verify driver installation</span></span>


<span data-ttu-id="c45c3-136">Pour interroger l’état de l’appareil GPU, connectez-vous par SSH à la machine virtuelle et exécutez l’utilitaire de ligne de commande [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) installé avec le pilote.</span><span class="sxs-lookup"><span data-stu-id="c45c3-136">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

<span data-ttu-id="c45c3-137">Une sortie similaire à ce qui suit s’affiche :</span><span class="sxs-lookup"><span data-stu-id="c45c3-137">Output similar to the following appears:</span></span>

![État de l’appareil NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="c45c3-139">Serveur X11</span><span class="sxs-lookup"><span data-stu-id="c45c3-139">X11 server</span></span>
<span data-ttu-id="c45c3-140">Si vous avez besoin d’un serveur X11 pour les connexions à distance vers une machine virtuelle NV, [x11vnc](http://www.karlrunge.com/x11vnc/) est recommandé, car il permet l’accélération matérielle des graphiques.</span><span class="sxs-lookup"><span data-stu-id="c45c3-140">If you need an X11 server for remote connections to an NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="c45c3-141">Le BusID de l’appareil M60 doit être ajouté manuellement au fichier xconfig (`etc/X11/xorg.conf` sur Ubuntu 16.04 LTS, `/etc/X11/XF86config` sur CentOS 7.3 ou Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="c45c3-141">The BusID of the M60 device must be manually added to the xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="c45c3-142">Ajoutez une section `"Device"` similaire à la suivante :</span><span class="sxs-lookup"><span data-stu-id="c45c3-142">Add a `"Device"` section similar to the following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="c45c3-143">En outre, mettez à jour votre section `"Screen"` pour utiliser cet appareil.</span><span class="sxs-lookup"><span data-stu-id="c45c3-143">Additionally, update your `"Screen"` section to use this device.</span></span>
 
<span data-ttu-id="c45c3-144">Vous trouverez le BusID en exécutant</span><span class="sxs-lookup"><span data-stu-id="c45c3-144">The BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="c45c3-145">Le BusID peut changer lorsqu’une machine virtuelle est réaffectée ou redémarrée.</span><span class="sxs-lookup"><span data-stu-id="c45c3-145">The BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="c45c3-146">Par conséquent, il peut être judicieux d’utiliser un script pour mettre à jour le BusID dans la configuration X11 lors du redémarrage d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c45c3-146">Therefore, you may want to use a script to update the BusID in the X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="c45c3-147">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c45c3-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed to ${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="c45c3-148">Ce fichier peut être appelé en tant que racine au démarrage en créant une entrée pour lui dans `/etc/rc.d/rc3.d`.</span><span class="sxs-lookup"><span data-stu-id="c45c3-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="c45c3-149">Installer des pilotes CUDA pour des machines virtuelles NC</span><span class="sxs-lookup"><span data-stu-id="c45c3-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="c45c3-150">Voici les étapes pour installer les pilotes NVIDIA sur des machines virtuelles Linux NC à partir du kit d’outils CUDA NVIDIA 8.0.</span><span class="sxs-lookup"><span data-stu-id="c45c3-150">Here are steps to install NVIDIA drivers on Linux NC VMs from the NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="c45c3-151">Les développeurs C et C++ peuvent éventuellement installer le kit d’outils complet pour créer des applications avec accélération GPU.</span><span class="sxs-lookup"><span data-stu-id="c45c3-151">C and C++ developers can optionally install the full Toolkit to build GPU-accelerated applications.</span></span> <span data-ttu-id="c45c3-152">Pour plus d’informations, consultez le [Guide d’installation de CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="c45c3-152">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="c45c3-153">Les liens de téléchargement de pilotes CUDA fournis ici sont à jour au moment de la publication.</span><span class="sxs-lookup"><span data-stu-id="c45c3-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="c45c3-154">Pour les pilotes CUDA les plus récents, visitez le site web de [NVIDIA](http://www.nvidia.com/).</span><span class="sxs-lookup"><span data-stu-id="c45c3-154">For the latest CUDA drivers, visit the [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="c45c3-155">Pour installer le kit d’outils CUDA, établissez une connexion SSH à chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c45c3-155">To install CUDA Toolkit, make an SSH connection to each VM.</span></span> <span data-ttu-id="c45c3-156">Pour vérifier que le système dispose d’un GPU compatible CUDA, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c45c3-156">To verify that the system has a CUDA-capable GPU, run the following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="c45c3-157">Vous verrez une sortie similaire à l’exemple suivant (illustrant une carte K80 Tesla NVIDIA) :</span><span class="sxs-lookup"><span data-stu-id="c45c3-157">You will see output similar to the following example (showing an NVIDIA Tesla K80 card):</span></span>

![Sortie de commande Ispci](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="c45c3-159">Ensuite, exécutez les commandes d’installation spécifiques de votre distribution.</span><span class="sxs-lookup"><span data-stu-id="c45c3-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="c45c3-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="c45c3-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="c45c3-161">Téléchargez et installez les pilotes CUDA.</span><span class="sxs-lookup"><span data-stu-id="c45c3-161">Download and install the CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="c45c3-162">L’installation peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="c45c3-162">The installation can take several minutes.</span></span>

2. <span data-ttu-id="c45c3-163">Pour éventuellement installer le kit d’outils CUDA complet, saisissez :</span><span class="sxs-lookup"><span data-stu-id="c45c3-163">To optionally install the complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="c45c3-164">Redémarrez la machine virtuelle et vérifiez l’installation.</span><span class="sxs-lookup"><span data-stu-id="c45c3-164">Reboot the VM and proceed to verify the installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="c45c3-165">Basé sur CentOS 7.3 ou Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="c45c3-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="c45c3-166">Obtenez les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="c45c3-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="c45c3-167">Reconnectez-vous à la machine virtuelle et installez les derniers services d’intégration Linux pour Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="c45c3-167">Reconnect to the VM and install the latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c45c3-168">Si vous avez installé une image HPC basée sur CentOS sur une machine virtuelle NC24r, passez à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="c45c3-168">If you installed a CentOS-based HPC image on an NC24r VM, skip to Step 3.</span></span> <span data-ttu-id="c45c3-169">Étant donné que les pilotes RDMA Azure et les services d’intégration Linux sont préinstallés dans l’image, LIS ne doit pas être mis à niveau et les mises à jour du noyau sont désactivées par défaut.</span><span class="sxs-lookup"><span data-stu-id="c45c3-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in the image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="c45c3-170">Reconnectez-vous à la machine virtuelle et continuez l’installation avec les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c45c3-170">Reconnect to the VM and continue installation with the following commands:</span></span>

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

  <span data-ttu-id="c45c3-171">L’installation peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="c45c3-171">The installation can take several minutes.</span></span> 

4. <span data-ttu-id="c45c3-172">Pour éventuellement installer le kit d’outils CUDA complet, saisissez :</span><span class="sxs-lookup"><span data-stu-id="c45c3-172">To optionally install the complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="c45c3-173">Redémarrez la machine virtuelle et vérifiez l’installation.</span><span class="sxs-lookup"><span data-stu-id="c45c3-173">Reboot the VM and proceed to verify the installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="c45c3-174">Vérification de l’installation du pilote</span><span class="sxs-lookup"><span data-stu-id="c45c3-174">Verify driver installation</span></span>


<span data-ttu-id="c45c3-175">Pour interroger l’état de l’appareil GPU, connectez-vous par SSH à la machine virtuelle et exécutez l’utilitaire de ligne de commande [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) installé avec le pilote.</span><span class="sxs-lookup"><span data-stu-id="c45c3-175">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

<span data-ttu-id="c45c3-176">Une sortie similaire à ce qui suit s’affiche :</span><span class="sxs-lookup"><span data-stu-id="c45c3-176">Output similar to the following appears:</span></span>

![État de l’appareil NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="c45c3-178">Mises à jour de pilote CUDA</span><span class="sxs-lookup"><span data-stu-id="c45c3-178">CUDA driver updates</span></span>

<span data-ttu-id="c45c3-179">Nous vous recommandons de régulièrement mettre à jour les pilotes CUDA après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="c45c3-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="c45c3-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="c45c3-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="c45c3-181">Basé sur CentOS 7.3 ou Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="c45c3-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="c45c3-182">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="c45c3-182">Troubleshooting</span></span>

* <span data-ttu-id="c45c3-183">Il existe un problème connu avec les pilotes CUDA sur les machines virtuelles Azure de série N exécutant le noyau Linux 4.4.0-75 sur Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="c45c3-183">There is a known issue with CUDA drivers on Azure N-series VMs running the 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="c45c3-184">Si vous effectuez une mise à niveau à partir d’une version antérieure du noyau, procédez à la mise à niveau vers la version 4.4.0-77 du noyau au minimum.</span><span class="sxs-lookup"><span data-stu-id="c45c3-184">If you are upgrading from an earlier kernel version, upgrade to at least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="c45c3-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c45c3-185">Next steps</span></span>

* <span data-ttu-id="c45c3-186">Pour plus d’informations sur les GPU NVIDIA sur les machines virtuelles série N, consultez :</span><span class="sxs-lookup"><span data-stu-id="c45c3-186">For more information about the NVIDIA GPUs on the N-series VMs, see:</span></span>
    * <span data-ttu-id="c45c3-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (pour les machines virtuelles NC Azure)</span><span class="sxs-lookup"><span data-stu-id="c45c3-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="c45c3-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (pour les machines virtuelles NV Azure)</span><span class="sxs-lookup"><span data-stu-id="c45c3-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="c45c3-189">Pour capturer une image Linux VM avec vos pilotes NVIDIA installés, consultez [Généraliser et capturer une machine virtuelle Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c45c3-189">To capture a Linux VM image with your installed NVIDIA drivers, see [How to generalize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
