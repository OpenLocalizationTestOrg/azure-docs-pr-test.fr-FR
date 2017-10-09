---
title: aaaImplement Oracle Data Guard sur la machine virtuelle de Azure Linux | Documents Microsoft
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
ms.openlocfilehash: 101196b2f50dfca64d3eb1b4be56ff0c108693e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="bc395-103">Implémenter Oracle Data Guard sur une machine virtuelle Linux Azure</span><span class="sxs-lookup"><span data-stu-id="bc395-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="bc395-104">Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="bc395-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="bc395-105">Ce guide décrit en détail à l’aide de hello CLI d’Azure toodeploy Oracle 12C de base de données à partir de l’image de la galerie hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bc395-105">This guide details using hello Azure CLI toodeploy an Oracle 12c Database from hello Marketplace gallery image.</span></span> <span data-ttu-id="bc395-106">Une fois que la base de données Oracle hello est créé, ce document vous montre une procédure pas à pas tooinstall et configurer Data Guard sur la machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="bc395-106">Once hello Oracle database is created, this document shows you step-by-step how tooinstall and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="bc395-107">Avant de commencer, assurez-vous que hello que CLI d’Azure a été installé.</span><span class="sxs-lookup"><span data-stu-id="bc395-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="bc395-108">Pour plus d’informations, consultez le [Guide d’installation de l’interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bc395-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="bc395-109">Préparer l’environnement de hello</span><span class="sxs-lookup"><span data-stu-id="bc395-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="bc395-110">Hypothèses</span><span class="sxs-lookup"><span data-stu-id="bc395-110">Assumptions</span></span>

<span data-ttu-id="bc395-111">hello tooperform Oracle Data Guard installer, vous devez toocreate deux machines virtuelles Azure hello même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="bc395-111">tooperform hello Oracle Data Guard install, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="bc395-112">image de Marketplace Hello vous utilisez toocreate hello machines virtuelles est « Oracle : Oracle-base de données-Ee:12.1.0.2:latest ».</span><span class="sxs-lookup"><span data-stu-id="bc395-112">hello Marketplace image you use toocreate hello VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="bc395-113">Hello ordinateur virtuel principal (myVM1) a une instance Oracle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bc395-113">hello primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="bc395-114">Hello que machine virtuelle de secours (myVM2) dispose d’un hello Oracle logiciel uniquement.</span><span class="sxs-lookup"><span data-stu-id="bc395-114">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="bc395-115">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="bc395-115">Log in tooAzure</span></span> 

<span data-ttu-id="bc395-116">Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran.</span><span class="sxs-lookup"><span data-stu-id="bc395-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="bc395-117">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="bc395-117">Create a resource group</span></span>

<span data-ttu-id="bc395-118">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="bc395-118">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="bc395-119">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="bc395-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="bc395-120">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westus` emplacement.</span><span class="sxs-lookup"><span data-stu-id="bc395-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="bc395-121">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="bc395-121">Create availability set</span></span>

<span data-ttu-id="bc395-122">Cette étape est facultative mais recommandée.</span><span class="sxs-lookup"><span data-stu-id="bc395-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="bc395-123">Pour plus d’informations, voir [Instructions pour les groupes à haute disponibilité Azure pour les machines virtuelles Windows](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="bc395-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="bc395-124">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="bc395-124">Create virtual machine</span></span>

<span data-ttu-id="bc395-125">Créer une machine virtuelle avec hello [az vm créer](/cli/azure/vm#create) commande.</span><span class="sxs-lookup"><span data-stu-id="bc395-125">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="bc395-126">exemple Hello crée 2 ordinateurs virtuels nommés `myVM1` et `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="bc395-126">hello following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="bc395-127">Crée les clés SSH si elles n’existent pas déjà dans un emplacement de clé par défaut.</span><span class="sxs-lookup"><span data-stu-id="bc395-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="bc395-128">toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="bc395-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="bc395-129">Créer myVM1 (machine virtuelle principale)</span><span class="sxs-lookup"><span data-stu-id="bc395-129">Create myVM1 (primary)</span></span>
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

<span data-ttu-id="bc395-130">Une fois hello machine virtuelle a été créé, hello CLI d’Azure s’affiche des informations similaires toohello est l’exemple suivant : prenez note de hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="bc395-130">Once hello VM has been created, hello Azure CLI shows information similar toohello following example: Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="bc395-131">Cette adresse est utilisée tooaccess hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bc395-131">This address is used tooaccess hello VM.</span></span>

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

<span data-ttu-id="bc395-132">Créer myVM2 (machine virtuelle secours)</span><span class="sxs-lookup"><span data-stu-id="bc395-132">Create myVM2 (standby)</span></span>
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

<span data-ttu-id="bc395-133">Prenez note de hello `publicIpAddress` il créé ainsi qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="bc395-133">Take note of hello `publicIpAddress` as well once it created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="bc395-134">Ouvrez le port TCP hello pour la connectivité</span><span class="sxs-lookup"><span data-stu-id="bc395-134">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="bc395-135">étape de Hello est tooconfigure des points de terminaison externes, ce qui permet l’accès à distance de base de données Oracle de hello, vous exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="bc395-135">hello step is tooconfigure external endpoints, which allows accessing hello Oracle DB remotely, you execute hello following command.</span></span>

<span data-ttu-id="bc395-136">Ouvrir un port pour myVM1</span><span class="sxs-lookup"><span data-stu-id="bc395-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="bc395-137">Résultat doit être similaire toohello suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="bc395-137">Result should look similar toohello following response:</span></span>

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

<span data-ttu-id="bc395-138">Ouvrir un port pour myVM2</span><span class="sxs-lookup"><span data-stu-id="bc395-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toovirtual-machine"></a><span data-ttu-id="bc395-139">Connecter toovirtual machine</span><span class="sxs-lookup"><span data-stu-id="bc395-139">Connect toovirtual machine</span></span>

<span data-ttu-id="bc395-140">La commande suivante de hello utilisation toocreate une session SSH avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="bc395-140">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="bc395-141">Remplacer l’adresse IP de hello avec hello `publicIpAddress` de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bc395-141">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="bc395-142">Créer une base de données sur myVM1 (machine virtuelle principale)</span><span class="sxs-lookup"><span data-stu-id="bc395-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="bc395-143">Hello logiciels Oracle est déjà installé sur une image Marketplace hello, afin de l’étape suivante de hello est la base de données tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="bc395-143">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> <span data-ttu-id="bc395-144">première étape de Hello est en cours d’exécution en tant que super utilisateur de hello « oracle ».</span><span class="sxs-lookup"><span data-stu-id="bc395-144">hello first step is running as hello 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="bc395-145">Créer la base de données hello :</span><span class="sxs-lookup"><span data-stu-id="bc395-145">create hello database:</span></span>

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
<span data-ttu-id="bc395-146">Sorties doivent être similaire toohello suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="bc395-146">Outputs should look similar toohello following response:</span></span>

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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="bc395-147">Définir des variables ORACLE_SID et ORACLE_HOME hello</span><span class="sxs-lookup"><span data-stu-id="bc395-147">Set hello ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="bc395-148">Si vous le souhaitez, vous pouvez ajouté ORACLE_HOME et ORACLE_SID toohello .bashrc de fichier, afin que ces paramètres sont enregistrés pour les futures connexions.</span><span class="sxs-lookup"><span data-stu-id="bc395-148">Optionally, You can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="bc395-149">Configurations de Data Guard</span><span class="sxs-lookup"><span data-stu-id="bc395-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="bc395-150">Activer le mode de journalisation Archive sur myVM1 (machine virtuelle principale)</span><span class="sxs-lookup"><span data-stu-id="bc395-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="bc395-151">Activez la journalisation forcée et assurez-vous qu’au moins un fichier journal est présent.</span><span class="sxs-lookup"><span data-stu-id="bc395-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="bc395-152">Créez des journaux de rétablissement de secours.</span><span class="sxs-lookup"><span data-stu-id="bc395-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="bc395-153">Activer la restauration (ce qui rend la restauration de hello beaucoup plus tôt) et définissez STANDBY_FILE_MANAGEMENT tooauto</span><span class="sxs-lookup"><span data-stu-id="bc395-153">Turn on Flashback (which made hello recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT tooauto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="bc395-154">Configuration du service sur myVM1 (machine virtuelle principale)</span><span class="sxs-lookup"><span data-stu-id="bc395-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="bc395-155">Modifier ou créer le fichier tnsnames.ora hello, qui se trouve dans le dossier $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="bc395-155">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="bc395-156">Ajouter hello suivant des entrées</span><span class="sxs-lookup"><span data-stu-id="bc395-156">Add hello following entries</span></span>

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

<span data-ttu-id="bc395-157">Modifier ou créer le fichier listener.ora hello, qui se trouve dans le dossier $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="bc395-157">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="bc395-158">Ajouter hello suivant des entrées</span><span class="sxs-lookup"><span data-stu-id="bc395-158">Add hello following entries</span></span>

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

<span data-ttu-id="bc395-159">Démarrer l’écouteur de hello</span><span class="sxs-lookup"><span data-stu-id="bc395-159">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="bc395-160">Configuration du service sur myVM2 (machine virtuelle de secours)</span><span class="sxs-lookup"><span data-stu-id="bc395-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="bc395-161">Modifier ou créer le fichier tnsnames.ora hello, qui se trouve dans le dossier $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="bc395-161">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="bc395-162">Ajouter hello suivant des entrées</span><span class="sxs-lookup"><span data-stu-id="bc395-162">Add hello following entries</span></span>

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

<span data-ttu-id="bc395-163">Modifier ou créer le fichier listener.ora hello, qui se trouve dans le dossier $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="bc395-163">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="bc395-164">Ajouter hello suivant des entrées</span><span class="sxs-lookup"><span data-stu-id="bc395-164">Add hello following entries</span></span>

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

<span data-ttu-id="bc395-165">Démarrer l’écouteur de hello</span><span class="sxs-lookup"><span data-stu-id="bc395-165">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="bc395-166">Activez Data Guard Broker.</span><span class="sxs-lookup"><span data-stu-id="bc395-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-toomyvm2-standby"></a><span data-ttu-id="bc395-167">Restaurer la base de données toomyVM2 (secondaire)</span><span class="sxs-lookup"><span data-stu-id="bc395-167">Restore database toomyVM2 (Standby)</span></span>

<span data-ttu-id="bc395-168">Créer un fichier de paramètres ' / tmp/initcdb1_stby.ora' avec le contenu de ce qui suit hello</span><span class="sxs-lookup"><span data-stu-id="bc395-168">Create a parameter file '/tmp/initcdb1_stby.ora' with hello followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="bc395-169">Créez les dossiers.</span><span class="sxs-lookup"><span data-stu-id="bc395-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="bc395-170">Créez le fichier de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="bc395-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="bc395-171">Démarrez la base de données sur myVM2.</span><span class="sxs-lookup"><span data-stu-id="bc395-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="bc395-172">Restaurez la base de données avec l’utilitaire RMAN.</span><span class="sxs-lookup"><span data-stu-id="bc395-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="bc395-173">Exécutez hello suivant les commandes dans RMAN</span><span class="sxs-lookup"><span data-stu-id="bc395-173">Execute hello following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="bc395-174">Activez Data Guard Broker.</span><span class="sxs-lookup"><span data-stu-id="bc395-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="bc395-175">Configurer Data Guard Broker sur myVM1 (machine virtuelle principale)</span><span class="sxs-lookup"><span data-stu-id="bc395-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="bc395-176">Démarrez le gestionnaire hello Data Guard, à l’aide de SYS et le mot de passe (effectuez ne pas l’authentification du système d’exploitation).</span><span class="sxs-lookup"><span data-stu-id="bc395-176">Start hello Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="bc395-177">Effectuer ce qui suit hello</span><span class="sxs-lookup"><span data-stu-id="bc395-177">Perform hello followings</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="bc395-178">Revoir la configuration hello</span><span class="sxs-lookup"><span data-stu-id="bc395-178">Review hello configuration</span></span>
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

<span data-ttu-id="bc395-179">Le programme d’installation de hello Oracle Data Guard exécuter cette opération.</span><span class="sxs-lookup"><span data-stu-id="bc395-179">This completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="bc395-180">section suivante de Hello vous montre comment tootest hello de connectivité et de basculement</span><span class="sxs-lookup"><span data-stu-id="bc395-180">hello next section shows you how tootest hello connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="bc395-181">Se connecter à la base de données à partir d’un ordinateur client</span><span class="sxs-lookup"><span data-stu-id="bc395-181">Connect database from client machine</span></span>

<span data-ttu-id="bc395-182">Mettre à jour ou de créer le fichier tnsnames.ora de hello sur votre ordinateur client qui est généralement situé dans $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="bc395-182">Update or create hello tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="bc395-183">Remplacer l’adresse IP hello avec votre `publicIpAddress` pour myVM1 et myVM2</span><span class="sxs-lookup"><span data-stu-id="bc395-183">Replace hello IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

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

<span data-ttu-id="bc395-184">Démarrez sqlplus.</span><span class="sxs-lookup"><span data-stu-id="bc395-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="bc395-185">Tester la configuration de Data Guard</span><span class="sxs-lookup"><span data-stu-id="bc395-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="bc395-186">Basculement de base de données vers myVM1 (machine virtuelle principale)</span><span class="sxs-lookup"><span data-stu-id="bc395-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="bc395-187">tooswitch de toostandby principal (cdb1 toocdb1_stby)</span><span class="sxs-lookup"><span data-stu-id="bc395-187">tooswitch from primary toostandby (cdb1 toocdb1_stby)</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1_stby"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="bc395-188">Vous devez maintenant être en mesure de tooconnect toohello base de données en attente</span><span class="sxs-lookup"><span data-stu-id="bc395-188">You should now be able tooconnect toohello standby database</span></span>

<span data-ttu-id="bc395-189">Démarrez sqlplus.</span><span class="sxs-lookup"><span data-stu-id="bc395-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="bc395-190">Re-basculement de base de données vers myVM2 (machine virtuelle de secours)</span><span class="sxs-lookup"><span data-stu-id="bc395-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="bc395-191">tooswitch, exécutez ce qui suit hello sur myVM2</span><span class="sxs-lookup"><span data-stu-id="bc395-191">tooswitch back, run hello followings on myVM2</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="bc395-192">Une fois encore, vous devez maintenant être en mesure de tooconnect toohello base de données primaire</span><span class="sxs-lookup"><span data-stu-id="bc395-192">Once again, You should now be able tooconnect toohello primary database</span></span>

<span data-ttu-id="bc395-193">Démarrez sqlplus.</span><span class="sxs-lookup"><span data-stu-id="bc395-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="bc395-194">Cette opération effectuée hello et Configure Data Guard sur Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="bc395-194">This completed hello installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="bc395-195">Suppression d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bc395-195">Delete virtual machine</span></span>

<span data-ttu-id="bc395-196">Lorsque n’est plus nécessaire, hello commande suivante peut être utilisé tooremove hello groupe de ressources, machine virtuelle, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="bc395-196">When no longer needed, hello following command can be used tooremove hello Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="bc395-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bc395-197">Next steps</span></span>

[<span data-ttu-id="bc395-198">Didacticiel de création de machines virtuelles hautement disponibles</span><span class="sxs-lookup"><span data-stu-id="bc395-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="bc395-199">Découvrir des exemples de commande de déploiement de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bc395-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
