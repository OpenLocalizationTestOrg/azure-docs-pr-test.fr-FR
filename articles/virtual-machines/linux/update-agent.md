---
title: "aaaUpdate hello Azure Linux Agent à partir de GitHub | Documents Microsoft"
description: "Découvrez comment tooupdate Azure Linux Agent pour votre VM Linux dans la version la plus récente à partir de GitHub toohello Azure"
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
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a><span data-ttu-id="21dfe-103">Comment tooupdate hello Azure Linux Agent sur un ordinateur virtuel</span><span class="sxs-lookup"><span data-stu-id="21dfe-103">How tooupdate hello Azure Linux Agent on a VM</span></span>

<span data-ttu-id="21dfe-104">tooupdate votre [Linux Agent Azure](https://github.com/Azure/WALinuxAgent) sur un Linux VM dans Azure, vous devez déjà disposer :</span><span class="sxs-lookup"><span data-stu-id="21dfe-104">tooupdate your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="21dfe-105">Une machine virtuelle Linux en cours d'exécution dans Azure.</span><span class="sxs-lookup"><span data-stu-id="21dfe-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="21dfe-106">Une connexion de toothat Linux VM à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="21dfe-106">A connection toothat Linux VM using SSH.</span></span>

<span data-ttu-id="21dfe-107">Vous devez toujours vérifier tout d’abord d’un package dans le référentiel de distribution de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="21dfe-107">You should always check for a package in hello Linux distro repository first.</span></span> <span data-ttu-id="21dfe-108">Il est possible de package hello disponible peut être pas la version la plus récente hello, toutefois, l’activation de mise à jour automatique garantit hello Linux Agent sera toujours obtenir les dernières mises à jour de hello.</span><span class="sxs-lookup"><span data-stu-id="21dfe-108">It is possible hello package available may not be hello latest version, however, enabling autoupdate will ensure hello Linux Agent will always get hello latest update.</span></span> <span data-ttu-id="21dfe-109">Si vous avez des problèmes d’installation à partir des gestionnaires de packages hello, vous devez rechercher la prise en charge à partir du fournisseur de distributeur hello.</span><span class="sxs-lookup"><span data-stu-id="21dfe-109">Should you have issues installing from hello package managers, you should seek support from hello distro vendor.</span></span>

## <a name="updating-hello-azure-linux-agent"></a><span data-ttu-id="21dfe-110">Mise à jour hello Linux Agent Azure</span><span class="sxs-lookup"><span data-stu-id="21dfe-110">Updating hello Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="21dfe-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="21dfe-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="21dfe-112">Vérifier votre version actuelle du package</span><span class="sxs-lookup"><span data-stu-id="21dfe-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="21dfe-113">Mettre à jour le cache du package</span><span class="sxs-lookup"><span data-stu-id="21dfe-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="21dfe-114">Installez la dernière version de package hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-114">Install hello latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="21dfe-115">Vérifier que la mise à jour automatique est activée</span><span class="sxs-lookup"><span data-stu-id="21dfe-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="21dfe-116">Vérifiez tout d’abord, toosee s’il est activé :</span><span class="sxs-lookup"><span data-stu-id="21dfe-116">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="21dfe-117">Recherchez « AutoUpdate.Enabled ».</span><span class="sxs-lookup"><span data-stu-id="21dfe-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="21dfe-118">Si vous voyez cette sortie, cela signifie qu’elle est activée :</span><span class="sxs-lookup"><span data-stu-id="21dfe-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="21dfe-119">tooenable exécuter :</span><span class="sxs-lookup"><span data-stu-id="21dfe-119">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="21dfe-120">Redémarrez le service de waagent hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-120">Restart hello waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="21dfe-121">Redémarrer l’agent pour 14.04</span><span class="sxs-lookup"><span data-stu-id="21dfe-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="21dfe-122">Redémarrer l’agent pour 16.04 / 17.04</span><span class="sxs-lookup"><span data-stu-id="21dfe-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="21dfe-123">Debian</span><span class="sxs-lookup"><span data-stu-id="21dfe-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="21dfe-124">Debian 7 « Wheezy »</span><span class="sxs-lookup"><span data-stu-id="21dfe-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="21dfe-125">Vérifier votre version actuelle du package</span><span class="sxs-lookup"><span data-stu-id="21dfe-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="21dfe-126">Mettre à jour le cache du package</span><span class="sxs-lookup"><span data-stu-id="21dfe-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="21dfe-127">Installez la dernière version de package hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-127">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="21dfe-128">Activer la mise à jour automatique de l’agent</span><span class="sxs-lookup"><span data-stu-id="21dfe-128">Enable agent auto update</span></span>
<span data-ttu-id="21dfe-129">Cette version de Debian n’a pas de version supérieure ou égale à 2.0.16. Par conséquent, AutoUpdate n’est pas disponible pour elle.</span><span class="sxs-lookup"><span data-stu-id="21dfe-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="21dfe-130">sortie de Hello de hello au-dessus de commande vous indiquera si le package de hello est à jour.</span><span class="sxs-lookup"><span data-stu-id="21dfe-130">hello output from hello above command will show you if hello package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="21dfe-131">Debian 8 « Jessie » / Debian 9 « Stretch »</span><span class="sxs-lookup"><span data-stu-id="21dfe-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="21dfe-132">Vérifier votre version actuelle du package</span><span class="sxs-lookup"><span data-stu-id="21dfe-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="21dfe-133">Mettre à jour le cache du package</span><span class="sxs-lookup"><span data-stu-id="21dfe-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="21dfe-134">Installez la dernière version de package hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-134">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="21dfe-135">Vérifier que la mise à jour automatique est activée</span><span class="sxs-lookup"><span data-stu-id="21dfe-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="21dfe-136">Vérifiez tout d’abord, toosee s’il est activé :</span><span class="sxs-lookup"><span data-stu-id="21dfe-136">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="21dfe-137">Recherchez « AutoUpdate.Enabled ».</span><span class="sxs-lookup"><span data-stu-id="21dfe-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="21dfe-138">Si vous voyez cette sortie, cela signifie qu’elle est activée :</span><span class="sxs-lookup"><span data-stu-id="21dfe-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="21dfe-139">tooenable exécuter :</span><span class="sxs-lookup"><span data-stu-id="21dfe-139">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="21dfe-140">Redémarrez le service de waagent hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-140">Restart hello waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="21dfe-141">Redhat / CentOS</span><span class="sxs-lookup"><span data-stu-id="21dfe-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="21dfe-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="21dfe-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="21dfe-143">Vérifier votre version actuelle du package</span><span class="sxs-lookup"><span data-stu-id="21dfe-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="21dfe-144">Vérifier les mises à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="21dfe-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="21dfe-145">Installez la dernière version de package hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-145">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="21dfe-146">Vérifier que la mise à jour automatique est activée</span><span class="sxs-lookup"><span data-stu-id="21dfe-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="21dfe-147">Vérifiez tout d’abord, toosee s’il est activé :</span><span class="sxs-lookup"><span data-stu-id="21dfe-147">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="21dfe-148">Recherchez « AutoUpdate.Enabled ».</span><span class="sxs-lookup"><span data-stu-id="21dfe-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="21dfe-149">Si vous voyez cette sortie, cela signifie qu’elle est activée :</span><span class="sxs-lookup"><span data-stu-id="21dfe-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="21dfe-150">tooenable exécuter :</span><span class="sxs-lookup"><span data-stu-id="21dfe-150">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="21dfe-151">Redémarrez le service de waagent hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-151">Restart hello waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="21dfe-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="21dfe-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="21dfe-153">Vérifier votre version actuelle du package</span><span class="sxs-lookup"><span data-stu-id="21dfe-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="21dfe-154">Vérifier les mises à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="21dfe-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="21dfe-155">Installez la dernière version de package hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-155">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="21dfe-156">Vérifier que la mise à jour automatique est activée</span><span class="sxs-lookup"><span data-stu-id="21dfe-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="21dfe-157">Vérifiez tout d’abord, toosee s’il est activé :</span><span class="sxs-lookup"><span data-stu-id="21dfe-157">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="21dfe-158">Recherchez « AutoUpdate.Enabled ».</span><span class="sxs-lookup"><span data-stu-id="21dfe-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="21dfe-159">Si vous voyez cette sortie, cela signifie qu’elle est activée :</span><span class="sxs-lookup"><span data-stu-id="21dfe-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="21dfe-160">tooenable exécuter :</span><span class="sxs-lookup"><span data-stu-id="21dfe-160">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="21dfe-161">Redémarrez le service de waagent hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-161">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="21dfe-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="21dfe-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="21dfe-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="21dfe-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="21dfe-164">Vérifier votre version actuelle du package</span><span class="sxs-lookup"><span data-stu-id="21dfe-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="21dfe-165">Vérifier les mises à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="21dfe-165">Check available updates</span></span>

<span data-ttu-id="21dfe-166">Hello au-dessus de sortie vous indique si le package de hello est de toodate.</span><span class="sxs-lookup"><span data-stu-id="21dfe-166">hello above output will show you if hello package is up toodate.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="21dfe-167">Installez la dernière version de package hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-167">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="21dfe-168">Vérifier que la mise à jour automatique est activée</span><span class="sxs-lookup"><span data-stu-id="21dfe-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="21dfe-169">Vérifiez tout d’abord, toosee s’il est activé :</span><span class="sxs-lookup"><span data-stu-id="21dfe-169">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="21dfe-170">Recherchez « AutoUpdate.Enabled ».</span><span class="sxs-lookup"><span data-stu-id="21dfe-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="21dfe-171">Si vous voyez cette sortie, cela signifie qu’elle est activée :</span><span class="sxs-lookup"><span data-stu-id="21dfe-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="21dfe-172">tooenable exécuter :</span><span class="sxs-lookup"><span data-stu-id="21dfe-172">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="21dfe-173">Redémarrez le service de waagent hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-173">Restart hello waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="21dfe-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="21dfe-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="21dfe-175">Vérifier votre version actuelle du package</span><span class="sxs-lookup"><span data-stu-id="21dfe-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="21dfe-176">Vérifier les mises à jour disponibles</span><span class="sxs-lookup"><span data-stu-id="21dfe-176">Check available updates</span></span>

<span data-ttu-id="21dfe-177">Dans la sortie de hello de hello ci-dessus, cela vous indiquera si le package de hello est à jour.</span><span class="sxs-lookup"><span data-stu-id="21dfe-177">In hello output from hello above, this will show you if hello package is upto date.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="21dfe-178">Installez la dernière version de package hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-178">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="21dfe-179">Vérifier que la mise à jour automatique est activée</span><span class="sxs-lookup"><span data-stu-id="21dfe-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="21dfe-180">Vérifiez tout d’abord, toosee s’il est activé :</span><span class="sxs-lookup"><span data-stu-id="21dfe-180">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="21dfe-181">Recherchez « AutoUpdate.Enabled ».</span><span class="sxs-lookup"><span data-stu-id="21dfe-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="21dfe-182">Si vous voyez cette sortie, cela signifie qu’elle est activée :</span><span class="sxs-lookup"><span data-stu-id="21dfe-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="21dfe-183">tooenable exécuter :</span><span class="sxs-lookup"><span data-stu-id="21dfe-183">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="21dfe-184">Redémarrez le service de waagent hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-184">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="21dfe-185">Oracle 6 et 7</span><span class="sxs-lookup"><span data-stu-id="21dfe-185">Oracle 6 and 7</span></span>

<span data-ttu-id="21dfe-186">Pour Oracle Linux, assurez-vous que hello `Addons` référentiel est activé.</span><span class="sxs-lookup"><span data-stu-id="21dfe-186">For Oracle Linux, make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="21dfe-187">Choisissez le fichier de hello tooedit `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) ou `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) et remplacez-la par hello `enabled=0` trop`enabled=1` sous **[ol6_addons]** ou **[ol7_addons]** Dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="21dfe-187">Choose tooedit hello file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="21dfe-188">Ensuite, tooinstall hello version la plus récente de hello Azure Linux Agent, type :</span><span class="sxs-lookup"><span data-stu-id="21dfe-188">Then, tooinstall hello latest version of hello Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="21dfe-189">Si vous ne trouvez pas référentiel de module complémentaire hello vous pouvez simplement ajouter ces lignes à fin hello de votre fichier .repo selon la version d’Oracle Linux tooyour :</span><span class="sxs-lookup"><span data-stu-id="21dfe-189">If you don't find hello add-on repository you can simply add these lines at hello end of your .repo file according tooyour Oracle Linux release:</span></span>

<span data-ttu-id="21dfe-190">Pour les machines virtuelles Oracle Linux 6 :</span><span class="sxs-lookup"><span data-stu-id="21dfe-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="21dfe-191">Pour les machines virtuelles Oracle Linux 7 :</span><span class="sxs-lookup"><span data-stu-id="21dfe-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="21dfe-192">Tapez ensuite :</span><span class="sxs-lookup"><span data-stu-id="21dfe-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="21dfe-193">En général, cela est que nécessaire, mais si pour une raison quelconque vous devez tooinstall à partir de https://github.com directement, hello utilisation suivant les étapes.</span><span class="sxs-lookup"><span data-stu-id="21dfe-193">Typically this is all you need, but if for some reason you need tooinstall it from https://github.com directly, use hello following steps.</span></span>


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="21dfe-194">Mettre à jour hello Linux Agent lorsque aucun package de l’agent n’existe pour la distribution</span><span class="sxs-lookup"><span data-stu-id="21dfe-194">Update hello Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="21dfe-195">Installez wget (il existe des versions qui ne l’installation par défaut, tels que des versions Redhat, CentOS et Oracle Linux 6.4 et 6.5) en tapant `sudo yum install wget` sur la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="21dfe-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on hello command line.</span></span>

### <a name="1-download-hello-latest-version"></a><span data-ttu-id="21dfe-196">1. Télécharger la version la plus récente hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-196">1. Download hello latest version</span></span>
<span data-ttu-id="21dfe-197">Ouvrez [hello version de l’Agent de Linux Azure dans GitHub](https://github.com/Azure/WALinuxAgent/releases) dans une page web et découvrez le numéro de version plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="21dfe-197">Open [hello release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out hello latest version number.</span></span> <span data-ttu-id="21dfe-198">(Vous pouvez rechercher votre version actuelle en tapant `waagent --version`.)</span><span class="sxs-lookup"><span data-stu-id="21dfe-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="21dfe-199">Pour la version 2.2.x ou ultérieure, tapez :</span><span class="sxs-lookup"><span data-stu-id="21dfe-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="21dfe-200">Hello ligne suivante utilise version2.2.0 comme exemple :</span><span class="sxs-lookup"><span data-stu-id="21dfe-200">hello following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a><span data-ttu-id="21dfe-201">2. Installer hello Linux Agent Azure</span><span class="sxs-lookup"><span data-stu-id="21dfe-201">2. Install hello Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="21dfe-202">Pour la version 2.2.x, tapez :</span><span class="sxs-lookup"><span data-stu-id="21dfe-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="21dfe-203">Vous devrez peut-être le package de hello tooinstall `setuptools` premier--se [ici](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="21dfe-203">You may need tooinstall hello package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="21dfe-204">Exécutez ensuite la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="21dfe-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="21dfe-205">Vérifier que la mise à jour automatique est activée</span><span class="sxs-lookup"><span data-stu-id="21dfe-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="21dfe-206">Vérifiez tout d’abord, toosee s’il est activé :</span><span class="sxs-lookup"><span data-stu-id="21dfe-206">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="21dfe-207">Recherchez « AutoUpdate.Enabled ».</span><span class="sxs-lookup"><span data-stu-id="21dfe-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="21dfe-208">Si vous voyez cette sortie, cela signifie qu’elle est activée :</span><span class="sxs-lookup"><span data-stu-id="21dfe-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="21dfe-209">tooenable exécuter :</span><span class="sxs-lookup"><span data-stu-id="21dfe-209">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a><span data-ttu-id="21dfe-210">3. Redémarrez le service de waagent hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-210">3. Restart hello waagent service</span></span>
<span data-ttu-id="21dfe-211">Pour la plupart des versions de linux :</span><span class="sxs-lookup"><span data-stu-id="21dfe-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="21dfe-212">Pour Ubuntu, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="21dfe-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="21dfe-213">Pour CoreOS, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="21dfe-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a><span data-ttu-id="21dfe-214">4. Confirmer la version de le Linux Agent Azure hello</span><span class="sxs-lookup"><span data-stu-id="21dfe-214">4. Confirm hello Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="21dfe-215">Pour CoreOS, hello au-dessus de commande peuvent ne pas fonctionne.</span><span class="sxs-lookup"><span data-stu-id="21dfe-215">For CoreOS, hello above command may not work.</span></span>

<span data-ttu-id="21dfe-216">Vous verrez que hello Azure Linux Agent version a été mis à jour toohello nouvelle version.</span><span class="sxs-lookup"><span data-stu-id="21dfe-216">You will see that hello Azure Linux Agent version has been updated toohello new version.</span></span>

<span data-ttu-id="21dfe-217">Pour plus d’informations sur hello Linux Agent Azure, consultez [Lisezmoi de l’Agent Linux Azure](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="21dfe-217">For more information regarding hello Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>
