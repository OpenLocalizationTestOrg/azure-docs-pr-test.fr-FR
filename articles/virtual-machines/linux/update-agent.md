---
title: "Mettre à jour l’agent Linux Azure à partir de GitHub | Microsoft Docs"
description: "Découvrez comment mettre à jour l’agent Linux Azure pour votre machine virtuelle Linux dans Azure vers la dernière version à partir de GitHub"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: c79e37976a58ae5384b5856e0f7f258a773ef0fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-update-the-azure-linux-agent-on-a-vm"></a><span data-ttu-id="dfb25-103">Guide pratique pour mettre à jour l’agent Linux Azure sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="dfb25-103">How to update the Azure Linux Agent on a VM</span></span>

<span data-ttu-id="dfb25-104">Pour mettre à jour votre [agent Linux Azure](https://github.com/Azure/WALinuxAgent) sur une machine virtuelle Linux dans Azure vous devez déjà disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dfb25-104">To update your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="dfb25-105">Une machine virtuelle Linux en cours d'exécution dans Azure.</span><span class="sxs-lookup"><span data-stu-id="dfb25-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="dfb25-106">Une connexion à cette machine virtuelle Linux à l'aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="dfb25-106">A connection to that Linux VM using SSH.</span></span>

<span data-ttu-id="dfb25-107">Vous devez toujours d’abord vérifier s’il existe un package dans le référentiel de distribution Linux.</span><span class="sxs-lookup"><span data-stu-id="dfb25-107">You should always check for a package in the Linux distro repository first.</span></span> <span data-ttu-id="dfb25-108">Il est possible que le package disponible ne soit pas la dernière version. Toutefois, l’activation de la mise à jour automatique permet de s’assurer que l’agent Linux obtiendra toujours la mise à jour la plus récente.</span><span class="sxs-lookup"><span data-stu-id="dfb25-108">It is possible the package available may not be the latest version, however, enabling autoupdate will ensure the Linux Agent will always get the latest update.</span></span> <span data-ttu-id="dfb25-109">Si vous avez des problèmes d’installation à partir des gestionnaires de package, contactez l’éditeur de distribution pour obtenir de l’aide.</span><span class="sxs-lookup"><span data-stu-id="dfb25-109">Should you have issues installing from the package managers, you should seek support from the distro vendor.</span></span>

## <a name="updating-the-azure-linux-agent"></a><span data-ttu-id="dfb25-110">Mise à jour de l’agent Linux Azure</span><span class="sxs-lookup"><span data-stu-id="dfb25-110">Updating the Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="dfb25-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="dfb25-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="dfb25-112">Vérifier votre version actuelle du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="dfb25-113">Mettre à jour le cache du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="dfb25-114">Installer la dernière version du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-114">Install the latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="dfb25-115">Vérifier que la mise à jour automatique est activée</span><span class="sxs-lookup"><span data-stu-id="dfb25-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="dfb25-116">Tout d’abord, vérifiez si elle est activée :</span><span class="sxs-lookup"><span data-stu-id="dfb25-116">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="dfb25-117">Recherchez « AutoUpdate.Enabled ».</span><span class="sxs-lookup"><span data-stu-id="dfb25-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="dfb25-118">Si vous voyez cette sortie, cela signifie qu’elle est activée :</span><span class="sxs-lookup"><span data-stu-id="dfb25-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="dfb25-119">Pour l’activer, exécutez :</span><span class="sxs-lookup"><span data-stu-id="dfb25-119">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="dfb25-120">Redémarrer le service waagent</span><span class="sxs-lookup"><span data-stu-id="dfb25-120">Restart the waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="dfb25-121">Redémarrer l’agent pour 14.04</span><span class="sxs-lookup"><span data-stu-id="dfb25-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="dfb25-122">Redémarrer l’agent pour 16.04 / 17.04</span><span class="sxs-lookup"><span data-stu-id="dfb25-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="dfb25-123">Debian</span><span class="sxs-lookup"><span data-stu-id="dfb25-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="dfb25-124">Debian 7 « Wheezy »</span><span class="sxs-lookup"><span data-stu-id="dfb25-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="dfb25-125">Vérifier votre version actuelle du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="dfb25-126">Mettre à jour le cache du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="dfb25-127">Installer la dernière version du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-127">Install the latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="dfb25-128">Activer la mise à jour automatique de l’agent</span><span class="sxs-lookup"><span data-stu-id="dfb25-128">Enable agent auto update</span></span>
<span data-ttu-id="dfb25-129">Cette version de Debian n’a pas de version supérieure ou égale à 2.0.16. Par conséquent, AutoUpdate n’est pas disponible pour elle.</span><span class="sxs-lookup"><span data-stu-id="dfb25-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="dfb25-130">La sortie de la commande ci-dessus indique si le package est à jour.</span><span class="sxs-lookup"><span data-stu-id="dfb25-130">The output from the above command will show you if the package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="dfb25-131">Debian 8 « Jessie » / Debian 9 « Stretch »</span><span class="sxs-lookup"><span data-stu-id="dfb25-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="dfb25-132">Vérifier votre version actuelle du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="dfb25-133">Mettre à jour le cache du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="dfb25-134">Installer la dernière version du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-134">Install the latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="dfb25-135">Vérifier que la mise à jour automatique est activée</span><span class="sxs-lookup"><span data-stu-id="dfb25-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="dfb25-136">Tout d’abord, vérifiez si elle est activée :</span><span class="sxs-lookup"><span data-stu-id="dfb25-136">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="dfb25-137">Recherchez « AutoUpdate.Enabled ».</span><span class="sxs-lookup"><span data-stu-id="dfb25-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="dfb25-138">Si vous voyez cette sortie, cela signifie qu’elle est activée :</span><span class="sxs-lookup"><span data-stu-id="dfb25-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="dfb25-139">Pour l’activer, exécutez :</span><span class="sxs-lookup"><span data-stu-id="dfb25-139">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="dfb25-140">Redémarrer le service waagent</span><span class="sxs-lookup"><span data-stu-id="dfb25-140">Restart the waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="dfb25-141">Redhat / CentOS</span><span class="sxs-lookup"><span data-stu-id="dfb25-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="dfb25-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="dfb25-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="dfb25-143">Vérifier votre version actuelle du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="dfb25-144">Vérifier les mises à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="dfb25-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="dfb25-145">Installer la dernière version du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-145">Install the latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="dfb25-146">Vérifier que la mise à jour automatique est activée</span><span class="sxs-lookup"><span data-stu-id="dfb25-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="dfb25-147">Tout d’abord, vérifiez si elle est activée :</span><span class="sxs-lookup"><span data-stu-id="dfb25-147">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="dfb25-148">Recherchez « AutoUpdate.Enabled ».</span><span class="sxs-lookup"><span data-stu-id="dfb25-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="dfb25-149">Si vous voyez cette sortie, cela signifie qu’elle est activée :</span><span class="sxs-lookup"><span data-stu-id="dfb25-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="dfb25-150">Pour l’activer, exécutez :</span><span class="sxs-lookup"><span data-stu-id="dfb25-150">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="dfb25-151">Redémarrer le service waagent</span><span class="sxs-lookup"><span data-stu-id="dfb25-151">Restart the waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="dfb25-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="dfb25-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="dfb25-153">Vérifier votre version actuelle du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="dfb25-154">Vérifier les mises à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="dfb25-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="dfb25-155">Installer la dernière version du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-155">Install the latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="dfb25-156">Vérifier que la mise à jour automatique est activée</span><span class="sxs-lookup"><span data-stu-id="dfb25-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="dfb25-157">Tout d’abord, vérifiez si elle est activée :</span><span class="sxs-lookup"><span data-stu-id="dfb25-157">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="dfb25-158">Recherchez « AutoUpdate.Enabled ».</span><span class="sxs-lookup"><span data-stu-id="dfb25-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="dfb25-159">Si vous voyez cette sortie, cela signifie qu’elle est activée :</span><span class="sxs-lookup"><span data-stu-id="dfb25-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="dfb25-160">Pour l’activer, exécutez :</span><span class="sxs-lookup"><span data-stu-id="dfb25-160">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="dfb25-161">Redémarrer le service waagent</span><span class="sxs-lookup"><span data-stu-id="dfb25-161">Restart the waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="dfb25-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="dfb25-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="dfb25-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="dfb25-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="dfb25-164">Vérifier votre version actuelle du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="dfb25-165">Vérifier les mises à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="dfb25-165">Check available updates</span></span>

<span data-ttu-id="dfb25-166">La sortie ci-dessus indique si le package est à jour.</span><span class="sxs-lookup"><span data-stu-id="dfb25-166">The above output will show you if the package is up to date.</span></span>

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="dfb25-167">Installer la dernière version du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-167">Install the latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="dfb25-168">Vérifier que la mise à jour automatique est activée</span><span class="sxs-lookup"><span data-stu-id="dfb25-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="dfb25-169">Tout d’abord, vérifiez si elle est activée :</span><span class="sxs-lookup"><span data-stu-id="dfb25-169">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="dfb25-170">Recherchez « AutoUpdate.Enabled ».</span><span class="sxs-lookup"><span data-stu-id="dfb25-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="dfb25-171">Si vous voyez cette sortie, cela signifie qu’elle est activée :</span><span class="sxs-lookup"><span data-stu-id="dfb25-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="dfb25-172">Pour l’activer, exécutez :</span><span class="sxs-lookup"><span data-stu-id="dfb25-172">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="dfb25-173">Redémarrer le service waagent</span><span class="sxs-lookup"><span data-stu-id="dfb25-173">Restart the waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="dfb25-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="dfb25-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="dfb25-175">Vérifier votre version actuelle du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="dfb25-176">Vérifier les mises à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="dfb25-176">Check available updates</span></span>

<span data-ttu-id="dfb25-177">La sortie de la commande ci-dessus indique si le package est à jour.</span><span class="sxs-lookup"><span data-stu-id="dfb25-177">In the output from the above, this will show you if the package is upto date.</span></span>

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="dfb25-178">Installer la dernière version du package</span><span class="sxs-lookup"><span data-stu-id="dfb25-178">Install the latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="dfb25-179">Vérifier que la mise à jour automatique est activée</span><span class="sxs-lookup"><span data-stu-id="dfb25-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="dfb25-180">Tout d’abord, vérifiez si elle est activée :</span><span class="sxs-lookup"><span data-stu-id="dfb25-180">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="dfb25-181">Recherchez « AutoUpdate.Enabled ».</span><span class="sxs-lookup"><span data-stu-id="dfb25-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="dfb25-182">Si vous voyez cette sortie, cela signifie qu’elle est activée :</span><span class="sxs-lookup"><span data-stu-id="dfb25-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="dfb25-183">Pour l’activer, exécutez :</span><span class="sxs-lookup"><span data-stu-id="dfb25-183">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="dfb25-184">Redémarrer le service waagent</span><span class="sxs-lookup"><span data-stu-id="dfb25-184">Restart the waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="dfb25-185">Oracle 6 et 7</span><span class="sxs-lookup"><span data-stu-id="dfb25-185">Oracle 6 and 7</span></span>

<span data-ttu-id="dfb25-186">Pour Oracle Linux, assurez-vous que le référentiel `Addons` est activé.</span><span class="sxs-lookup"><span data-stu-id="dfb25-186">For Oracle Linux, make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="dfb25-187">Modifiez le fichier `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) ou `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), modifiez la ligne `enabled=0` en `enabled=1` sous **[ol6_addons]** ou **[ol7_addons]** dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="dfb25-187">Choose to edit the file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="dfb25-188">Puis, pour installer la dernière version de l'agent Linux Azure, tapez :</span><span class="sxs-lookup"><span data-stu-id="dfb25-188">Then, to install the latest version of the Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="dfb25-189">Si vous ne trouvez pas le référentiel de compléments, vous pouvez ajouter ces lignes à la fin de votre fichier .repo en fonction de votre version d’Oracle Linux :</span><span class="sxs-lookup"><span data-stu-id="dfb25-189">If you don't find the add-on repository you can simply add these lines at the end of your .repo file according to your Oracle Linux release:</span></span>

<span data-ttu-id="dfb25-190">Pour les machines virtuelles Oracle Linux 6 :</span><span class="sxs-lookup"><span data-stu-id="dfb25-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="dfb25-191">Pour les machines virtuelles Oracle Linux 7 :</span><span class="sxs-lookup"><span data-stu-id="dfb25-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="dfb25-192">Tapez ensuite :</span><span class="sxs-lookup"><span data-stu-id="dfb25-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="dfb25-193">Généralement, c’est tout ce qu’il vous est demandé de faire. Toutefois, si pour une raison quelconque vous devez l’installer directement à partir de https://github.com, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="dfb25-193">Typically this is all you need, but if for some reason you need to install it from https://github.com directly, use the following steps.</span></span>


## <a name="update-the-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="dfb25-194">Mettre à jour l’agent Linux quand il n’existe aucun package d’agent pour la distribution</span><span class="sxs-lookup"><span data-stu-id="dfb25-194">Update the Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="dfb25-195">Installez wget (certaines versions, telles que Redhat, CentOS et Oracle Linux versions 6.4 et 6.5, ne l’installent pas par défaut) en tapant `sudo yum install wget` sur la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="dfb25-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on the command line.</span></span>

### <a name="1-download-the-latest-version"></a><span data-ttu-id="dfb25-196">1. Téléchargez la dernière version</span><span class="sxs-lookup"><span data-stu-id="dfb25-196">1. Download the latest version</span></span>
<span data-ttu-id="dfb25-197">Ouvrez [la version de l’agent Linux Azure dans Github](https://github.com/Azure/WALinuxAgent/releases) dans une page web et cherchez le dernier numéro de version.</span><span class="sxs-lookup"><span data-stu-id="dfb25-197">Open [the release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out the latest version number.</span></span> <span data-ttu-id="dfb25-198">(Vous pouvez rechercher votre version actuelle en tapant `waagent --version`.)</span><span class="sxs-lookup"><span data-stu-id="dfb25-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="dfb25-199">Pour la version 2.2.x ou ultérieure, tapez :</span><span class="sxs-lookup"><span data-stu-id="dfb25-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="dfb25-200">La ligne suivante utilise la version 2.2.0 comme exemple :</span><span class="sxs-lookup"><span data-stu-id="dfb25-200">The following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-the-azure-linux-agent"></a><span data-ttu-id="dfb25-201">2. Installez l'agent Linux Azure.</span><span class="sxs-lookup"><span data-stu-id="dfb25-201">2. Install the Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="dfb25-202">Pour la version 2.2.x, tapez :</span><span class="sxs-lookup"><span data-stu-id="dfb25-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="dfb25-203">Vous devrez peut-être installer d’abord le package `setuptools`. Consultez [ces informations](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="dfb25-203">You may need to install the package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="dfb25-204">Exécutez ensuite la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="dfb25-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="dfb25-205">Vérifier que la mise à jour automatique est activée</span><span class="sxs-lookup"><span data-stu-id="dfb25-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="dfb25-206">Tout d’abord, vérifiez si elle est activée :</span><span class="sxs-lookup"><span data-stu-id="dfb25-206">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="dfb25-207">Recherchez « AutoUpdate.Enabled ».</span><span class="sxs-lookup"><span data-stu-id="dfb25-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="dfb25-208">Si vous voyez cette sortie, cela signifie qu’elle est activée :</span><span class="sxs-lookup"><span data-stu-id="dfb25-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="dfb25-209">Pour l’activer, exécutez :</span><span class="sxs-lookup"><span data-stu-id="dfb25-209">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-the-waagent-service"></a><span data-ttu-id="dfb25-210">3. Redémarrer le service waagent</span><span class="sxs-lookup"><span data-stu-id="dfb25-210">3. Restart the waagent service</span></span>
<span data-ttu-id="dfb25-211">Pour la plupart des versions de linux :</span><span class="sxs-lookup"><span data-stu-id="dfb25-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="dfb25-212">Pour Ubuntu, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dfb25-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="dfb25-213">Pour CoreOS, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dfb25-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-the-azure-linux-agent-version"></a><span data-ttu-id="dfb25-214">4. Confirmer la version de l'agent Linux Azure</span><span class="sxs-lookup"><span data-stu-id="dfb25-214">4. Confirm the Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="dfb25-215">Pour CoreOS, la commande ci-dessus peut ne pas fonctionner.</span><span class="sxs-lookup"><span data-stu-id="dfb25-215">For CoreOS, the above command may not work.</span></span>

<span data-ttu-id="dfb25-216">Vous verrez que la version de l'agent Linux Azure a été mise à jour vers la nouvelle version.</span><span class="sxs-lookup"><span data-stu-id="dfb25-216">You will see that the Azure Linux Agent version has been updated to the new version.</span></span>

<span data-ttu-id="dfb25-217">Pour plus d’informations sur l’agent Linux Azure, consultez le fichier [Lisezmoi de l’agent Linux Azure](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="dfb25-217">For more information regarding the Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>