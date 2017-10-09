---
title: aaaImplement Oracle Golden la porte sur une machine virtuelle Linux de Azure | Documents Microsoft
description: "Configurez et exécutez rapidement une base de données Oracle Golden Gate dans votre environnement Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="d7199-103">Implémenter Oracle Golden Gate sur une machine virtuelle Linux Azure</span><span class="sxs-lookup"><span data-stu-id="d7199-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="d7199-104">Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="d7199-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="d7199-105">Ce guide décrit en détail comment toouse hello CLI d’Azure toodeploy Oracle 12C de base de données à partir de l’image de la galerie Azure Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="d7199-105">This guide details how toouse hello Azure CLI toodeploy an Oracle 12c database from hello Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="d7199-106">Ce document explique comment toocreate, installer et configurer Oracle Golden porte sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="d7199-106">This document shows you step-by-step how toocreate, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="d7199-107">Avant de commencer, assurez-vous que hello que CLI d’Azure a été installé.</span><span class="sxs-lookup"><span data-stu-id="d7199-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="d7199-108">Pour plus d’informations, consultez le [Guide d’installation de l’interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d7199-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="d7199-109">Préparer l’environnement de hello</span><span class="sxs-lookup"><span data-stu-id="d7199-109">Prepare hello environment</span></span>

<span data-ttu-id="d7199-110">installation de Oracle Golden porte tooperform hello, vous devez toocreate deux machines virtuelles Azure hello même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="d7199-110">tooperform hello Oracle Golden Gate installation, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="d7199-111">image de Marketplace Hello vous utilisez toocreate hello machines virtuelles est **Oracle : Oracle-base de données-Ee:12.1.0.2:latest**.</span><span class="sxs-lookup"><span data-stu-id="d7199-111">hello Marketplace image you use toocreate hello VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="d7199-112">Également, vous devez toobe familiarisé avec Unix éditeur vi et que vous avez une connaissance élémentaire de x11 (X Windows).</span><span class="sxs-lookup"><span data-stu-id="d7199-112">You also need toobe familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="d7199-113">Hello Voici un résumé de la configuration de l’environnement hello :</span><span class="sxs-lookup"><span data-stu-id="d7199-113">hello following is a summary of hello environment configuration:</span></span>
> 
> |  | <span data-ttu-id="d7199-114">**Site principal**</span><span class="sxs-lookup"><span data-stu-id="d7199-114">**Primary site**</span></span> | <span data-ttu-id="d7199-115">**Site de réplication**</span><span class="sxs-lookup"><span data-stu-id="d7199-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="d7199-116">**Version d’Oracle**</span><span class="sxs-lookup"><span data-stu-id="d7199-116">**Oracle release**</span></span> |<span data-ttu-id="d7199-117">Oracle 12c Version 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="d7199-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="d7199-118">Oracle 12c Version 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="d7199-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="d7199-119">**Nom de la machine**</span><span class="sxs-lookup"><span data-stu-id="d7199-119">**Machine name**</span></span> |<span data-ttu-id="d7199-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="d7199-120">myVM1</span></span> |<span data-ttu-id="d7199-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="d7199-121">myVM2</span></span> |
> | <span data-ttu-id="d7199-122">**Système d’exploitation**</span><span class="sxs-lookup"><span data-stu-id="d7199-122">**Operating system**</span></span> |<span data-ttu-id="d7199-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="d7199-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="d7199-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="d7199-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="d7199-125">**SID Oracle**</span><span class="sxs-lookup"><span data-stu-id="d7199-125">**Oracle SID**</span></span> |<span data-ttu-id="d7199-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="d7199-126">CDB1</span></span> |<span data-ttu-id="d7199-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="d7199-127">CDB1</span></span> |
> | <span data-ttu-id="d7199-128">**Schéma de réplication**</span><span class="sxs-lookup"><span data-stu-id="d7199-128">**Replication schema**</span></span> |<span data-ttu-id="d7199-129">TEST</span><span class="sxs-lookup"><span data-stu-id="d7199-129">TEST</span></span>|<span data-ttu-id="d7199-130">TEST</span><span class="sxs-lookup"><span data-stu-id="d7199-130">TEST</span></span> |
> | <span data-ttu-id="d7199-131">**Propriétaire Golden Gate/réplication**</span><span class="sxs-lookup"><span data-stu-id="d7199-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="d7199-132">C##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="d7199-132">C##GGADMIN</span></span> |<span data-ttu-id="d7199-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="d7199-133">REPUSER</span></span> |
> | <span data-ttu-id="d7199-134">**Processus Golden Gate**</span><span class="sxs-lookup"><span data-stu-id="d7199-134">**Golden Gate process**</span></span> |<span data-ttu-id="d7199-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="d7199-135">EXTORA</span></span> |<span data-ttu-id="d7199-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="d7199-136">REPORA</span></span>|


### <a name="sign-in-tooazure"></a><span data-ttu-id="d7199-137">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="d7199-137">Sign in tooAzure</span></span> 

<span data-ttu-id="d7199-138">Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande.</span><span class="sxs-lookup"><span data-stu-id="d7199-138">Sign in tooyour Azure subscription with hello [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="d7199-139">Puis suivez hello à l’écran.</span><span class="sxs-lookup"><span data-stu-id="d7199-139">Then follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="d7199-140">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="d7199-140">Create a resource group</span></span>

<span data-ttu-id="d7199-141">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="d7199-141">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d7199-142">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et à partir duquel elles peuvent être gérées.</span><span class="sxs-lookup"><span data-stu-id="d7199-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="d7199-143">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westus` emplacement.</span><span class="sxs-lookup"><span data-stu-id="d7199-143">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="d7199-144">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="d7199-144">Create an availability set</span></span>

<span data-ttu-id="d7199-145">Hello suivant l’étape est facultative mais recommandée.</span><span class="sxs-lookup"><span data-stu-id="d7199-145">hello following step is optional but recommended.</span></span> <span data-ttu-id="d7199-146">Pour plus d’informations, consultez [Instructions pour les groupes à haute disponibilité Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="d7199-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="d7199-147">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d7199-147">Create a virtual machine</span></span>

<span data-ttu-id="d7199-148">Créer une machine virtuelle avec hello [az vm créer](/cli/azure/vm#create) commande.</span><span class="sxs-lookup"><span data-stu-id="d7199-148">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="d7199-149">Hello exemple suivant crée deux ordinateurs virtuels nommés `myVM1` et `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="d7199-149">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="d7199-150">Créez les clés SSH si elles n’existent pas déjà dans un emplacement de clé par défaut.</span><span class="sxs-lookup"><span data-stu-id="d7199-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="d7199-151">toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="d7199-151">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="d7199-152">Créez myVM1 (machine virtuelle principale) :</span><span class="sxs-lookup"><span data-stu-id="d7199-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="d7199-153">Après l’hello que machine virtuelle a été créé, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="d7199-153">After hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="d7199-154">(Notez hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="d7199-154">(Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="d7199-155">Cette adresse est utilisée tooaccess hello machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="d7199-155">This address is used tooaccess hello VM.)</span></span>

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="d7199-156">Créez myVM2 (machine virtuelle de réplication) :</span><span class="sxs-lookup"><span data-stu-id="d7199-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="d7199-157">Prenez note de hello `publicIpAddress` ainsi une fois qu’elle a été créée.</span><span class="sxs-lookup"><span data-stu-id="d7199-157">Take note of hello `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="d7199-158">Ouvrez le port TCP hello pour la connectivité</span><span class="sxs-lookup"><span data-stu-id="d7199-158">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="d7199-159">étape suivante de Hello est tooconfigure points de terminaison externes, qui permettent de base de données Oracle tooaccess hello à distance.</span><span class="sxs-lookup"><span data-stu-id="d7199-159">hello next step is tooconfigure external endpoints,  which enable you tooaccess hello Oracle database remotely.</span></span> <span data-ttu-id="d7199-160">tooconfigure hello points de terminaison externes, exécutez hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="d7199-160">tooconfigure hello external endpoints, run hello following commands.</span></span>

#### <a name="open-hello-port-for-myvm1"></a><span data-ttu-id="d7199-161">Ouvrez le port hello pour myVM1 :</span><span class="sxs-lookup"><span data-stu-id="d7199-161">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="d7199-162">les résultats de Hello doivent ressembler similaire toohello suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="d7199-162">hello results should look similar toohello following response:</span></span>

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

#### <a name="open-hello-port-for-myvm2"></a><span data-ttu-id="d7199-163">Ouvrez le port hello pour myVM2 :</span><span class="sxs-lookup"><span data-stu-id="d7199-163">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="d7199-164">Connecter l’ordinateur virtuel de toohello</span><span class="sxs-lookup"><span data-stu-id="d7199-164">Connect toohello virtual machine</span></span>

<span data-ttu-id="d7199-165">La commande suivante de hello utilisation toocreate une session SSH avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="d7199-165">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="d7199-166">Remplacer l’adresse IP de hello avec hello `publicIpAddress` de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d7199-166">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="d7199-167">Créer la base de données hello sur myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="d7199-167">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="d7199-168">Hello logiciels Oracle est déjà installé sur une image Marketplace hello, afin de l’étape suivante de hello est la base de données tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="d7199-168">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="d7199-169">Identification des logiciels de hello superutilisateur « oracle » de hello :</span><span class="sxs-lookup"><span data-stu-id="d7199-169">Run hello software as hello 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="d7199-170">Créer la base de données hello :</span><span class="sxs-lookup"><span data-stu-id="d7199-170">Create hello database:</span></span>

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
<span data-ttu-id="d7199-171">Sorties doivent être similaire toohello suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="d7199-171">Outputs should look similar toohello following response:</span></span>

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="d7199-172">Définir les variables ORACLE_SID et ORACLE_HOME hello.</span><span class="sxs-lookup"><span data-stu-id="d7199-172">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="d7199-173">Si vous le souhaitez, vous pouvez ajouter ORACLE_HOME et ORACLE_SID fichier .bashrc toohello, afin que ces paramètres sont enregistrés pour les futures connexions :</span><span class="sxs-lookup"><span data-stu-id="d7199-173">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="d7199-174">Démarrer l’écouteur d’Oracle</span><span class="sxs-lookup"><span data-stu-id="d7199-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a><span data-ttu-id="d7199-175">Créer la base de données hello sur myVM2 (réplication)</span><span class="sxs-lookup"><span data-stu-id="d7199-175">Create hello database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="d7199-176">Créer la base de données hello :</span><span class="sxs-lookup"><span data-stu-id="d7199-176">Create hello database:</span></span>

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
<span data-ttu-id="d7199-177">Définir les variables ORACLE_SID et ORACLE_HOME hello.</span><span class="sxs-lookup"><span data-stu-id="d7199-177">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="d7199-178">Si vous le souhaitez, vous pouvez ajouté ORACLE_HOME et ORACLE_SID toohello .bashrc de fichier, afin que ces paramètres sont enregistrés pour les futures connexions.</span><span class="sxs-lookup"><span data-stu-id="d7199-178">Optionally, you can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="d7199-179">Démarrer l’écouteur d’Oracle</span><span class="sxs-lookup"><span data-stu-id="d7199-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="d7199-180">Configurer Golden Gate</span><span class="sxs-lookup"><span data-stu-id="d7199-180">Configure Golden Gate</span></span> 
<span data-ttu-id="d7199-181">tooconfigure Golden porte, prendre des mesures de hello dans cette section.</span><span class="sxs-lookup"><span data-stu-id="d7199-181">tooconfigure Golden Gate, take hello steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="d7199-182">Activer le mode de journalisation d’archive sur myVM1 (machine virtuelle principale)</span><span class="sxs-lookup"><span data-stu-id="d7199-182">Enable archive log mode on myVM1 (primary)</span></span>

```bash
$ sqlplus / as sysdba
SQL> SELECT log_mode FROM v$database;

LOG_MODE
------------
NOARCHIVELOG

SQL> SHUTDOWN IMMEDIATE;
SQL> STARTUP MOUNT;
SQL> ALTER DATABASE ARCHIVELOG;
SQL> ALTER DATABASE OPEN;
```
<span data-ttu-id="d7199-183">Activez la journalisation forcée et assurez-vous qu’au moins un fichier journal est présent.</span><span class="sxs-lookup"><span data-stu-id="d7199-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="d7199-184">Télécharger le logiciel Golden Gate</span><span class="sxs-lookup"><span data-stu-id="d7199-184">Download Golden Gate software</span></span>
<span data-ttu-id="d7199-185">toodownload et préparer un logiciel Oracle Golden porte hello, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7199-185">toodownload and prepare hello Oracle Golden Gate software, complete hello following steps:</span></span>

1. <span data-ttu-id="d7199-186">Télécharger hello **fbo_ggs_Linux_x64_shiphome.zip** fichier hello [page de téléchargement Oracle Golden porte](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="d7199-186">Download hello **fbo_ggs_Linux_x64_shiphome.zip** file from hello [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="d7199-187">Sous hello télécharger titre **12.x.x.x GoldenGate Oracle pour Oracle Linux x86-64**, il doit y avoir un ensemble de toodownload de fichiers .zip.</span><span class="sxs-lookup"><span data-stu-id="d7199-187">Under hello download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files toodownload.</span></span>

2. <span data-ttu-id="d7199-188">Après avoir téléchargé hello .zip fichiers tooyour client ordinateur, utilisez Secure copie Protocol (SCP) toocopy hello fichiers tooyour machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="d7199-188">After you download hello .zip files tooyour client computer, use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="d7199-189">Déplacer hello .zip fichiers toohello **/ opt** dossier.</span><span class="sxs-lookup"><span data-stu-id="d7199-189">Move hello .zip files toohello **/opt** folder.</span></span> <span data-ttu-id="d7199-190">Puis modifiez le propriétaire hello des fichiers de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7199-190">Then change hello owner of hello files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="d7199-191">Décompresser les fichiers de hello (installation hello Linux décompresser utilitaire s’il n’est pas déjà installé) :</span><span class="sxs-lookup"><span data-stu-id="d7199-191">Unzip hello files (install hello Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="d7199-192">Changez l’autorisation :</span><span class="sxs-lookup"><span data-stu-id="d7199-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a><span data-ttu-id="d7199-193">Préparer le client de hello et de la machine virtuelle toorun x11 (pour les clients Windows uniquement)</span><span class="sxs-lookup"><span data-stu-id="d7199-193">Prepare hello client and VM toorun x11 (for Windows clients only)</span></span>
<span data-ttu-id="d7199-194">Il s’agit d’une étape facultative.</span><span class="sxs-lookup"><span data-stu-id="d7199-194">This is an optional step.</span></span> <span data-ttu-id="d7199-195">Vous pouvez l’ignorer si vous utilisez un client Linux ou si x11 est déjà configuré.</span><span class="sxs-lookup"><span data-stu-id="d7199-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="d7199-196">Vous pouvez télécharger PuTTY et Xming ordinateur Windows de tooyour :</span><span class="sxs-lookup"><span data-stu-id="d7199-196">Download PuTTY and Xming tooyour Windows computer:</span></span>

  * [<span data-ttu-id="d7199-197">Télécharger PuTTY</span><span class="sxs-lookup"><span data-stu-id="d7199-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="d7199-198">Télécharger Xming</span><span class="sxs-lookup"><span data-stu-id="d7199-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="d7199-199">Après avoir installé PuTTY, en hello PuTTY dossier (par exemple, C:\Program Files\PuTTY), exécutez puttygen.exe (Générateur de clé PuTTY).</span><span class="sxs-lookup"><span data-stu-id="d7199-199">After you install PuTTY, in hello PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="d7199-200">Dans PuTTY Key Generator :</span><span class="sxs-lookup"><span data-stu-id="d7199-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="d7199-201">toogenerate un Bonjour clé, sélectionnez **générer** bouton.</span><span class="sxs-lookup"><span data-stu-id="d7199-201">toogenerate a key, select hello **Generate** button.</span></span>
  - <span data-ttu-id="d7199-202">Copier le contenu de hello de clé de hello (**Ctrl + C**).</span><span class="sxs-lookup"><span data-stu-id="d7199-202">Copy hello contents of hello key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="d7199-203">Sélectionnez hello **clé privée d’enregistrement** bouton.</span><span class="sxs-lookup"><span data-stu-id="d7199-203">Select hello **Save private key** button.</span></span>
  - <span data-ttu-id="d7199-204">Ignorer l’avertissement hello qui s’affiche, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7199-204">Ignore hello warning that appears, and then select **OK**.</span></span>

    ![Capture d’écran de la page de générateur de clé PuTTY hello](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="d7199-206">Dans votre machine virtuelle, exécutez ces commandes :</span><span class="sxs-lookup"><span data-stu-id="d7199-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="d7199-207">Créez un fichier nommé **authorized_keys**.</span><span class="sxs-lookup"><span data-stu-id="d7199-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="d7199-208">Collez le contenu hello de clé de hello dans ce fichier, puis enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="d7199-208">Paste hello contents of hello key in this file, and then save hello file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d7199-209">clé de Hello doit contenir la chaîne de hello `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="d7199-209">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="d7199-210">En outre, le contenu hello de clé de hello doit être une seule ligne de texte.</span><span class="sxs-lookup"><span data-stu-id="d7199-210">Also, hello contents of hello key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="d7199-211">Démarrez PuTTY.</span><span class="sxs-lookup"><span data-stu-id="d7199-211">Start PuTTY.</span></span> <span data-ttu-id="d7199-212">Bonjour **catégorie** volet, sélectionnez **connexion** > **SSH** > **Auth**. Bonjour **fichier de clé privée pour l’authentification** , naviguez jusque toohello clé que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="d7199-212">In hello **Category** pane, select **Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

  ![Capture d’écran de la page Définir la clé privée de hello](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="d7199-214">Bonjour **catégorie** volet, sélectionnez **connexion** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="d7199-214">In hello **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="d7199-215">Puis sélectionnez hello **X11 d’activer le transfert** boîte.</span><span class="sxs-lookup"><span data-stu-id="d7199-215">Then select hello **Enable X11 forwarding** box.</span></span>

  ![Capture d’écran de la page d’activation X11 hello](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="d7199-217">Bonjour **catégorie** volet, accédez trop**Session**.</span><span class="sxs-lookup"><span data-stu-id="d7199-217">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="d7199-218">Entrez les informations sur l’hôte hello et sélectionnez **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="d7199-218">Enter hello host information, and then select **Open**.</span></span>

  ![Capture d’écran de la page de session hello](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="d7199-220">Installer le logiciel Golden Gate</span><span class="sxs-lookup"><span data-stu-id="d7199-220">Install Golden Gate software</span></span>

<span data-ttu-id="d7199-221">tooinstall Oracle Golden porte, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="d7199-221">tooinstall Oracle Golden Gate, complete hello following steps:</span></span>

1. <span data-ttu-id="d7199-222">Connectez-vous en tant qu’oracle.</span><span class="sxs-lookup"><span data-stu-id="d7199-222">Sign in as oracle.</span></span> <span data-ttu-id="d7199-223">(Vous devez être en mesure de toosign dans sans être invité à entrer un mot de passe.) Assurez-vous que Xming est en cours d’exécution avant de commencer l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="d7199-223">(You should be able toosign in without being prompted for a password.) Make sure that Xming is running before you begin hello installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="d7199-224">Sélectionnez « Oracle GoldenGate for Oracle Database 12c ».</span><span class="sxs-lookup"><span data-stu-id="d7199-224">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="d7199-225">Puis sélectionnez **suivant** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d7199-225">Then select **Next** toocontinue.</span></span>

  ![Capture d’écran de la page de sélectionner l’Installation de programme d’installation de hello](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="d7199-227">Modifier l’emplacement du logiciel hello.</span><span class="sxs-lookup"><span data-stu-id="d7199-227">Change hello software location.</span></span> <span data-ttu-id="d7199-228">Puis sélectionnez hello **démarrer le Gestionnaire de** zone, puis entrez l’emplacement de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="d7199-228">Then select  hello **Start Manager** box and enter hello database location.</span></span> <span data-ttu-id="d7199-229">Sélectionnez **suivant** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d7199-229">Select **Next** toocontinue.</span></span>

  ![Capture d’écran de la page Sélectionnez une Installation de hello](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="d7199-231">Basculez hello d’inventaire, puis **suivant** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d7199-231">Change hello inventory directory, and then select **Next** toocontinue.</span></span>

  ![Capture d’écran de la page Sélectionnez une Installation de hello](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="d7199-233">Sur hello **Résumé** écran, sélectionnez **installer** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="d7199-233">On hello **Summary** screen, select **Install** toocontinue.</span></span>

  ![Capture d’écran de la page de sélectionner l’Installation de programme d’installation de hello](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="d7199-235">Vous pouvez être invité à toorun un script en tant que « root ».</span><span class="sxs-lookup"><span data-stu-id="d7199-235">You might be prompted toorun a script as 'root'.</span></span> <span data-ttu-id="d7199-236">Dans ce cas, d’ouvrir une session distincte, ssh toohello machine virtuelle, sudo tooroot et puis exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="d7199-236">If so, open a separate session, ssh toohello VM, sudo tooroot, and then run hello script.</span></span> <span data-ttu-id="d7199-237">Sélectionnez **OK** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="d7199-237">Select **OK** continue.</span></span>

  ![Capture d’écran de la page Sélectionnez une Installation de hello](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="d7199-239">Lors de l’installation de hello est terminée, sélectionnez **fermer** processus de hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="d7199-239">When hello installation has finished, select **Close** toocomplete hello process.</span></span>

  ![Capture d’écran de la page Sélectionnez une Installation de hello](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="d7199-241">Configurer le service sur myVM1 (machine virtuelle principale)</span><span class="sxs-lookup"><span data-stu-id="d7199-241">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="d7199-242">Créer ou mettre à jour le fichier tnsnames.ora de hello :</span><span class="sxs-lookup"><span data-stu-id="d7199-242">Create or update hello tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="d7199-243">Permet de créer des comptes de propriétaire et utilisateur Golden porte de hello.</span><span class="sxs-lookup"><span data-stu-id="d7199-243">Create hello Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d7199-244">compte de propriétaire de Hello doit avoir le préfixe C ##.</span><span class="sxs-lookup"><span data-stu-id="d7199-244">hello owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="d7199-245">Créer un compte d’utilisateur test hello Golden porte :</span><span class="sxs-lookup"><span data-stu-id="d7199-245">Create hello Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="d7199-246">Configurer le fichier de paramètres d’extraction hello.</span><span class="sxs-lookup"><span data-stu-id="d7199-246">Configure hello extract parameter file.</span></span>

 <span data-ttu-id="d7199-247">Démarrer une interface de ligne hello porte finale (ggsci) :</span><span class="sxs-lookup"><span data-stu-id="d7199-247">Start hello Golden gate command-line interface (ggsci):</span></span>

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. <span data-ttu-id="d7199-248">Ajoutez hello suivant du fichier de paramètres d’extraction toohello (à l’aide des commandes de vi).</span><span class="sxs-lookup"><span data-stu-id="d7199-248">Add hello following toohello EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="d7199-249">Appuyez sur la touche ÉCHAP, ':wq!'</span><span class="sxs-lookup"><span data-stu-id="d7199-249">Press Esc key, ':wq!'</span></span> <span data-ttu-id="d7199-250">fichier de toosave.</span><span class="sxs-lookup"><span data-stu-id="d7199-250">toosave file.</span></span> 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. <span data-ttu-id="d7199-251">Extrait de registre--extrait intégré :</span><span class="sxs-lookup"><span data-stu-id="d7199-251">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="d7199-252">Configurer des points de contrôle d’extraction et démarrer l’extraction en temps réel :</span><span class="sxs-lookup"><span data-stu-id="d7199-252">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="d7199-253">Dans cette étape, vous trouver hello SCN, qui sera utilisée ultérieurement, dans une autre section de démarrage :</span><span class="sxs-lookup"><span data-stu-id="d7199-253">In this step, you find hello starting SCN, which will be used later, in a different section:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="d7199-254">Configurer le service sur myVM2 (machine virtuelle de réplication)</span><span class="sxs-lookup"><span data-stu-id="d7199-254">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="d7199-255">Créer ou mettre à jour le fichier tnsnames.ora de hello :</span><span class="sxs-lookup"><span data-stu-id="d7199-255">Create or update hello tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="d7199-256">Créez un compte de réplication :</span><span class="sxs-lookup"><span data-stu-id="d7199-256">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="d7199-257">Créez un compte d’utilisateur de test de Golden Gate :</span><span class="sxs-lookup"><span data-stu-id="d7199-257">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="d7199-258">Modifications de tooreplicate paramètre fichier REPLICAT :</span><span class="sxs-lookup"><span data-stu-id="d7199-258">REPLICAT parameter file tooreplicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="d7199-259">Contenu du fichier de paramètres REPORA :</span><span class="sxs-lookup"><span data-stu-id="d7199-259">Content of REPORA parameter file:</span></span>

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. <span data-ttu-id="d7199-260">Configurez un point de contrôle de réplication :</span><span class="sxs-lookup"><span data-stu-id="d7199-260">Set up a replicat checkpoint:</span></span>

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a><span data-ttu-id="d7199-261">Configurer la réplication hello (myVM1 et myVM2)</span><span class="sxs-lookup"><span data-stu-id="d7199-261">Set up hello replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="d7199-262">1. Configurer la réplication hello sur myVM2 (réplication)</span><span class="sxs-lookup"><span data-stu-id="d7199-262">1. Set up hello replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="d7199-263">Mettre à jour les fichiers hello avec les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="d7199-263">Update hello file with hello following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="d7199-264">Puis redémarrez le service Manager hello :</span><span class="sxs-lookup"><span data-stu-id="d7199-264">Then restart hello Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a><span data-ttu-id="d7199-265">2. Configurer la réplication hello sur myVM1 (principal)</span><span class="sxs-lookup"><span data-stu-id="d7199-265">2. Set up hello replication on myVM1 (primary)</span></span>

<span data-ttu-id="d7199-266">Démarrez la charge initiale hello et recherchez les erreurs :</span><span class="sxs-lookup"><span data-stu-id="d7199-266">Start hello initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="d7199-267">3. Configurer la réplication hello sur myVM2 (réplication)</span><span class="sxs-lookup"><span data-stu-id="d7199-267">3. Set up hello replication on myVM2 (replicate)</span></span>

<span data-ttu-id="d7199-268">Modifier hello numéro SCN avec le nombre de hello que vous avez obtenus avant :</span><span class="sxs-lookup"><span data-stu-id="d7199-268">Change hello SCN number with hello number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="d7199-269">la réplication Hello a commencé, et vous pouvez le tester en insérant de nouvelles tables de tooTEST d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="d7199-269">hello replication has begun, and you can test it by inserting new records tooTEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="d7199-270">Afficher l’état du travail et la résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="d7199-270">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="d7199-271">Afficher des rapports</span><span class="sxs-lookup"><span data-stu-id="d7199-271">View reports</span></span>
<span data-ttu-id="d7199-272">tooview signale myVM1, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="d7199-272">tooview reports on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="d7199-273">tooview signale myVM2, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="d7199-273">tooview reports on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="d7199-274">Afficher l’état et l’historique</span><span class="sxs-lookup"><span data-stu-id="d7199-274">View status and history</span></span>
<span data-ttu-id="d7199-275">tooview état et l’historique sur myVM1, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="d7199-275">tooview status and history on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="d7199-276">tooview état et l’historique sur myVM2, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="d7199-276">tooview status and history on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="d7199-277">Cela termine l’installation de hello et la configuration de Golden porte sur Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="d7199-277">This completes hello installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="d7199-278">Supprimer la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="d7199-278">Delete hello virtual machine</span></span>

<span data-ttu-id="d7199-279">Lorsqu’il n’est plus nécessaire, hello commande suivante peut être groupe de ressources utilisé tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="d7199-279">When it's no longer needed, hello following command can be used tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="d7199-280">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d7199-280">Next steps</span></span>

[<span data-ttu-id="d7199-281">Didacticiel de création de machines virtuelles hautement disponibles</span><span class="sxs-lookup"><span data-stu-id="d7199-281">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="d7199-282">Découvrir des exemples de commande de déploiement de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d7199-282">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
