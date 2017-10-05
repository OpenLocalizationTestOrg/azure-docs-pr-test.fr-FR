---
title: "Implémenter Oracle Data Guard sur une machine virtuelle Linux Azure | Documents Microsoft"
description: "Configurez et exécutez rapidement Oracle Data Guard dans votre environnement Azure."
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
ms.date: 05/10/2017
ms.author: rclaus
ms.openlocfilehash: fe8b635936c74c5154ec83d34160b9aae61c45e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="e689e-103">Implémenter Oracle Data Guard sur une machine virtuelle Linux Azure</span><span class="sxs-lookup"><span data-stu-id="e689e-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="e689e-104">L’interface de ligne de commande (CLI) Azure permet de créer et gérer des ressources Azure à partir de la ligne de commande ou dans les scripts.</span><span class="sxs-lookup"><span data-stu-id="e689e-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="e689e-105">Ce guide explique comment utiliser l’interface de ligne de commande Azure pour déployer une base de données Oracle 12c depuis une image de la galerie du Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e689e-105">This guide details using the Azure CLI to deploy an Oracle 12c Database from the Marketplace gallery image.</span></span> <span data-ttu-id="e689e-106">Une fois la base de données Oracle créée, ce document montre étape par étape comment installer et configurer Data Guard sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="e689e-106">Once the Oracle database is created, this document shows you step-by-step how to install and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="e689e-107">Avant de commencer, assurez-vous que l’interface de ligne de commande Azure est installée.</span><span class="sxs-lookup"><span data-stu-id="e689e-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="e689e-108">Pour plus d’informations, consultez le [Guide d’installation de l’interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e689e-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="e689e-109">Préparer l’environnement</span><span class="sxs-lookup"><span data-stu-id="e689e-109">Prepare the environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="e689e-110">Hypothèses</span><span class="sxs-lookup"><span data-stu-id="e689e-110">Assumptions</span></span>

<span data-ttu-id="e689e-111">Pour installer Oracle Data Guard, vous devez créer deux machines virtuelles Azure sur le même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="e689e-111">To perform the Oracle Data Guard install, you need to create two Azure VMs on the same availability set.</span></span> <span data-ttu-id="e689e-112">L’image Place de marché que vous utilisez pour créer la machine virtuelle est « Oracle:Oracle-Database-Ee:12.1.0.2:latest ».</span><span class="sxs-lookup"><span data-stu-id="e689e-112">The Marketplace image you use to create the VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="e689e-113">La machine virtuelle principale (myVM1) a une instance Oracle active.</span><span class="sxs-lookup"><span data-stu-id="e689e-113">The primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="e689e-114">Le machine virtuelle de secours (myVM2) dispose uniquement du logiciel Oracle installé.</span><span class="sxs-lookup"><span data-stu-id="e689e-114">The standby VM (myVM2) has the Oracle software installed only.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="e689e-115">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="e689e-115">Log in to Azure</span></span> 

<span data-ttu-id="e689e-116">Connectez-vous à votre abonnement Azure avec la commande [az login](/cli/azure/#login) et suivez les instructions à l’écran.</span><span class="sxs-lookup"><span data-stu-id="e689e-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="e689e-117">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="e689e-117">Create a resource group</span></span>

<span data-ttu-id="e689e-118">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e689e-118">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="e689e-119">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="e689e-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="e689e-120">L’exemple suivant crée un groupe de ressources nommé `myResourceGroup` à l’emplacement `westus`.</span><span class="sxs-lookup"><span data-stu-id="e689e-120">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="e689e-121">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="e689e-121">Create availability set</span></span>

<span data-ttu-id="e689e-122">Cette étape est facultative mais recommandée.</span><span class="sxs-lookup"><span data-stu-id="e689e-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="e689e-123">Pour plus d’informations, voir [Instructions pour les groupes à haute disponibilité Azure pour les machines virtuelles Windows](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="e689e-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="e689e-124">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="e689e-124">Create virtual machine</span></span>

<span data-ttu-id="e689e-125">Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e689e-125">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="e689e-126">L’exemple ci-après crée deux machines virtuelles nommées `myVM1` et `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="e689e-126">The following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="e689e-127">Crée les clés SSH si elles n’existent pas déjà dans un emplacement de clé par défaut.</span><span class="sxs-lookup"><span data-stu-id="e689e-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="e689e-128">Pour utiliser un ensemble spécifique de clés, utilisez l’option `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="e689e-128">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

<span data-ttu-id="e689e-129">Créer myVM1 (machine virtuelle principale)</span><span class="sxs-lookup"><span data-stu-id="e689e-129">Create myVM1 (primary)</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

<span data-ttu-id="e689e-130">Une fois la machine virtuelle créée, Azure CLI affiche des informations similaires à l’exemple suivant : prenez note de l’adresse IP publique `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="e689e-130">Once the VM has been created, the Azure CLI shows information similar to the following example: Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="e689e-131">Cette adresse est utilisée pour accéder à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e689e-131">This address is used to access the VM.</span></span>

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

<span data-ttu-id="e689e-132">Créer myVM2 (machine virtuelle secours)</span><span class="sxs-lookup"><span data-stu-id="e689e-132">Create myVM2 (standby)</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

<span data-ttu-id="e689e-133">Prenez note également de l’adresse IP publique `publicIpAddress` une fois celle-ci créée.</span><span class="sxs-lookup"><span data-stu-id="e689e-133">Take note of the `publicIpAddress` as well once it created.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="e689e-134">Ouvrir le port TCP pour la connectivité</span><span class="sxs-lookup"><span data-stu-id="e689e-134">Open the TCP port for connectivity</span></span>

<span data-ttu-id="e689e-135">L’étape consiste à configurer des points de terminaison externes qui permettent l’accès à distance à la base de données Oracle. Pour ce faire, exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="e689e-135">The step is to configure external endpoints, which allows accessing the Oracle DB remotely, you execute the following command.</span></span>

<span data-ttu-id="e689e-136">Ouvrir un port pour myVM1</span><span class="sxs-lookup"><span data-stu-id="e689e-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="e689e-137">Le résultat doit être semblable à la réponse suivante :</span><span class="sxs-lookup"><span data-stu-id="e689e-137">Result should look similar to the following response:</span></span>

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

<span data-ttu-id="e689e-138">Ouvrir un port pour myVM2</span><span class="sxs-lookup"><span data-stu-id="e689e-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-virtual-machine"></a><span data-ttu-id="e689e-139">Connexion à la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e689e-139">Connect to virtual machine</span></span>

<span data-ttu-id="e689e-140">Utilisez la commande suivante pour créer une session SSH avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e689e-140">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="e689e-141">Remplacez l’adresse IP par la valeur `publicIpAddress` de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e689e-141">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="e689e-142">Créer une base de données sur myVM1 (machine virtuelle principale)</span><span class="sxs-lookup"><span data-stu-id="e689e-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="e689e-143">Le logiciel Oracle est déjà installé sur l’image Place de marché, l’étape suivante consiste donc à installer la base de données.</span><span class="sxs-lookup"><span data-stu-id="e689e-143">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> <span data-ttu-id="e689e-144">La première étape s’exécute en tant que superutilisateur « oracle ».</span><span class="sxs-lookup"><span data-stu-id="e689e-144">the first step is running as the 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="e689e-145">Créer la base de données :</span><span class="sxs-lookup"><span data-stu-id="e689e-145">create the database:</span></span>

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
<span data-ttu-id="e689e-146">Les résultats doivent ressembler à la réponse suivante :</span><span class="sxs-lookup"><span data-stu-id="e689e-146">Outputs should look similar to the following response:</span></span>

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
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="e689e-147">Définir les variables ORACLE_SID et ORACLE_HOME</span><span class="sxs-lookup"><span data-stu-id="e689e-147">Set the ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="e689e-148">Si vous le souhaitez, vous pouvez ajouter ORACLE_HOME et ORACLE_SID au fichier .bashrc, de façon à ce que ces paramètres soient enregistrés pour des connexions futures.</span><span class="sxs-lookup"><span data-stu-id="e689e-148">Optionally, You can added ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="e689e-149">Configurations de Data Guard</span><span class="sxs-lookup"><span data-stu-id="e689e-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="e689e-150">Activer le mode de journalisation Archive sur myVM1 (machine virtuelle principale)</span><span class="sxs-lookup"><span data-stu-id="e689e-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="e689e-151">Activez la journalisation forcée et assurez-vous qu’au moins un fichier journal est présent.</span><span class="sxs-lookup"><span data-stu-id="e689e-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="e689e-152">Créez des journaux de rétablissement de secours.</span><span class="sxs-lookup"><span data-stu-id="e689e-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="e689e-153">Activez Flashback (qui effectuait la récupération beaucoup plus tôt) et définissez STANDBY_FILE_MANAGEMENT sur auto.</span><span class="sxs-lookup"><span data-stu-id="e689e-153">Turn on Flashback (which made the recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT to auto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="e689e-154">Configuration du service sur myVM1 (machine virtuelle principale)</span><span class="sxs-lookup"><span data-stu-id="e689e-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="e689e-155">Modifiez ou créez le fichier tnsnames.ora qui se trouve dans le dossier $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="e689e-155">Edit or create the tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="e689e-156">Ajoutez les entrées suivantes.</span><span class="sxs-lookup"><span data-stu-id="e689e-156">Add the following entries</span></span>

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

<span data-ttu-id="e689e-157">Modifiez ou créez le fichier listener.ora qui se trouve dans le dossier $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="e689e-157">Edit or create the listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="e689e-158">Ajoutez les entrées suivantes.</span><span class="sxs-lookup"><span data-stu-id="e689e-158">Add the following entries</span></span>

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

<span data-ttu-id="e689e-159">Démarrez l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="e689e-159">Start the listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="e689e-160">Configuration du service sur myVM2 (machine virtuelle de secours)</span><span class="sxs-lookup"><span data-stu-id="e689e-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="e689e-161">Modifiez ou créez le fichier tnsnames.ora qui se trouve dans le dossier $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="e689e-161">Edit or create the tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="e689e-162">Ajoutez les entrées suivantes.</span><span class="sxs-lookup"><span data-stu-id="e689e-162">Add the following entries</span></span>

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

<span data-ttu-id="e689e-163">Modifiez ou créez le fichier listener.ora qui se trouve dans le dossier $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="e689e-163">Edit or create the listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="e689e-164">Ajoutez les entrées suivantes.</span><span class="sxs-lookup"><span data-stu-id="e689e-164">Add the following entries</span></span>

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

<span data-ttu-id="e689e-165">Démarrez l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="e689e-165">Start the listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="e689e-166">Activez Data Guard Broker.</span><span class="sxs-lookup"><span data-stu-id="e689e-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-to-myvm2-standby"></a><span data-ttu-id="e689e-167">Restaurer la base de données sur myVM2 (machine virtuelle de secours)</span><span class="sxs-lookup"><span data-stu-id="e689e-167">Restore database to myVM2 (Standby)</span></span>

<span data-ttu-id="e689e-168">Créez un fichier de paramètres « /tmp/initcdb1_stby.ora » dont le contenu est le suivant.</span><span class="sxs-lookup"><span data-stu-id="e689e-168">Create a parameter file '/tmp/initcdb1_stby.ora' with the followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="e689e-169">Créez les dossiers.</span><span class="sxs-lookup"><span data-stu-id="e689e-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="e689e-170">Créez le fichier de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="e689e-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="e689e-171">Démarrez la base de données sur myVM2.</span><span class="sxs-lookup"><span data-stu-id="e689e-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="e689e-172">Restaurez la base de données avec l’utilitaire RMAN.</span><span class="sxs-lookup"><span data-stu-id="e689e-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="e689e-173">Exécutez les commandes suivantes dans RMAN.</span><span class="sxs-lookup"><span data-stu-id="e689e-173">Execute the following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="e689e-174">Activez Data Guard Broker.</span><span class="sxs-lookup"><span data-stu-id="e689e-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="e689e-175">Configurer Data Guard Broker sur myVM1 (machine virtuelle principale)</span><span class="sxs-lookup"><span data-stu-id="e689e-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="e689e-176">Démarrez le gestionnaire Data Guard et connectez-vous à l’aide de SYS et d’un mot de passe (sans utiliser d’authentification du système d’exploitation).</span><span class="sxs-lookup"><span data-stu-id="e689e-176">Start the Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="e689e-177">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e689e-177">Perform the followings</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="e689e-178">Examinez la configuration.</span><span class="sxs-lookup"><span data-stu-id="e689e-178">Review the configuration</span></span>
```bash
DGMGRL> SHOW CONFIGURATION;

Configuration - my_dg_config

  Protection Mode: MaxPerformance
  Members:
  cdb1      - Primary database
    cdb1_stby - Physical standby database

Fast-Start Failover: DISABLED

Configuration Status:
SUCCESS   (status updated 26 seconds ago)
```

<span data-ttu-id="e689e-179">Cela achève la configuration d’Oracle Data Guard.</span><span class="sxs-lookup"><span data-stu-id="e689e-179">This completed the Oracle Data Guard setup.</span></span> <span data-ttu-id="e689e-180">La section suivante montre comment tester la connectivité et basculement.</span><span class="sxs-lookup"><span data-stu-id="e689e-180">The next section shows you how to test the connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="e689e-181">Se connecter à la base de données à partir d’un ordinateur client</span><span class="sxs-lookup"><span data-stu-id="e689e-181">Connect database from client machine</span></span>

<span data-ttu-id="e689e-182">Mettez à jour ou créez le fichier tnsnames.ora sur votre ordinateur client qui est généralement situé dans $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="e689e-182">Update or create the tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="e689e-183">Remplacez l’adresse IP avec votre adresse IP publique `publicIpAddress` pour myVM1 et myVM2.</span><span class="sxs-lookup"><span data-stu-id="e689e-183">Replace the IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

```bash
cdb1=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM1 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1)
    )
  )

cdb1_stby=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM2 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1_stby)
    )
  )
```

<span data-ttu-id="e689e-184">Démarrez sqlplus.</span><span class="sxs-lookup"><span data-stu-id="e689e-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="e689e-185">Tester la configuration de Data Guard</span><span class="sxs-lookup"><span data-stu-id="e689e-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="e689e-186">Basculement de base de données vers myVM1 (machine virtuelle principale)</span><span class="sxs-lookup"><span data-stu-id="e689e-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="e689e-187">Pour basculer de la base de données primaire vers la base de données de secours (de cdb1 à cdb1_stby)</span><span class="sxs-lookup"><span data-stu-id="e689e-187">To switch from primary to standby (cdb1 to cdb1_stby)</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1_stby"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="e689e-188">Vous devriez à présent être en mesure de vous connecter à la base de données de secours.</span><span class="sxs-lookup"><span data-stu-id="e689e-188">You should now be able to connect to the standby database</span></span>

<span data-ttu-id="e689e-189">Démarrez sqlplus.</span><span class="sxs-lookup"><span data-stu-id="e689e-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="e689e-190">Re-basculement de base de données vers myVM2 (machine virtuelle de secours)</span><span class="sxs-lookup"><span data-stu-id="e689e-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="e689e-191">Pour re-basculer, exécutez ce qui suit sur myVM2.</span><span class="sxs-lookup"><span data-stu-id="e689e-191">To switch back, run the followings on myVM2</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="e689e-192">Une fois encore, vous devriez à présent pouvoir vous connecter à la base de données primaire.</span><span class="sxs-lookup"><span data-stu-id="e689e-192">Once again, You should now be able to connect to the primary database</span></span>

<span data-ttu-id="e689e-193">Démarrez sqlplus.</span><span class="sxs-lookup"><span data-stu-id="e689e-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="e689e-194">Cela achève l’installation et la configuration de Data Guard sur Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="e689e-194">This completed the installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="e689e-195">Suppression d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e689e-195">Delete virtual machine</span></span>

<span data-ttu-id="e689e-196">Lorsque vous n’en avez plus besoin, la commande suivante permet de supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="e689e-196">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="e689e-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e689e-197">Next steps</span></span>

[<span data-ttu-id="e689e-198">Didacticiel de création de machines virtuelles hautement disponibles</span><span class="sxs-lookup"><span data-stu-id="e689e-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="e689e-199">Découvrir des exemples de commande de déploiement de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e689e-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
