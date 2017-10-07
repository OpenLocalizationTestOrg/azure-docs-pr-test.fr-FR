---
title: "partage d’aaaFile pour le cluster de contrôleur de domaine/système d’exploitation Azure | Documents Microsoft"
description: "Créer et monter un partage tooa contrôleur de domaine/système d’exploitation de fichiers dans le Service de conteneur Azure"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Mesos, Azure, FileShare, cifs
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: d18090d414a3e00202ccde442ac9b865d74f1e34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a><span data-ttu-id="4e3f1-104">Créer et monter un cluster de contrôleur de domaine/système d’exploitation de tooa partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="4e3f1-104">Create and mount a file share tooa DC/OS cluster</span></span>
<span data-ttu-id="4e3f1-105">Ce didacticiel décrit en détail comment toocreate un fichier de partage dans Azure et l’installer sur chaque agent et le masque de hello cluster du contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-105">This tutorial details how toocreate a file share in Azure and mount it on each agent and master of hello DC/OS cluster.</span></span> <span data-ttu-id="4e3f1-106">Configuration d’un partage de fichiers rend plus facile tooshare fichiers sur votre cluster telles que la configuration, l’accès, les journaux et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-106">Setting up a file share makes it easier tooshare files across your cluster such as configuration, access, logs, and more.</span></span> <span data-ttu-id="4e3f1-107">Bonjour tâches suivantes est effectuée dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="4e3f1-107">hello following tasks are completed in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4e3f1-108">Création d'un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="4e3f1-108">Create an Azure storage account</span></span>
> * <span data-ttu-id="4e3f1-109">Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="4e3f1-109">Create a file share</span></span>
> * <span data-ttu-id="4e3f1-110">Monter le partage hello dans un cluster de contrôleur de domaine/système d’exploitation hello</span><span class="sxs-lookup"><span data-stu-id="4e3f1-110">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="4e3f1-111">Vous avez besoin d’un contrôleur de domaine/OS ACS hello toocomplete de cluster les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-111">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="4e3f1-112">Le cas échéant, cet [exemple de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) peut en créer un pour vous.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="4e3f1-113">Ce didacticiel requiert hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-113">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4e3f1-114">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4e3f1-115">Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4e3f1-115">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="4e3f1-116">Créer un partage de fichiers sur Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4e3f1-116">Create a file share on Microsoft Azure</span></span>

<span data-ttu-id="4e3f1-117">Avant d’utiliser un partage de fichiers Azure avec un cluster ACS contrôleur de domaine/système d’exploitation, le partage de fichier et de compte de stockage hello doit être créé.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-117">Before using an Azure file share with an ACS DC/OS cluster, hello storage account and file share must be created.</span></span> <span data-ttu-id="4e3f1-118">Exécutez hello suivant script toocreate hello stockage et le fichier partage.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-118">Run hello following script toocreate hello storage and file share.</span></span> <span data-ttu-id="4e3f1-119">Mettre à jour les paramètres hello spéciales à partir de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-119">Update hello parameters with thoes from your environment.</span></span>

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create hello storage account with hello parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-hello-share-in-your-cluster"></a><span data-ttu-id="4e3f1-120">Monter le partage hello dans votre cluster</span><span class="sxs-lookup"><span data-stu-id="4e3f1-120">Mount hello share in your cluster</span></span>

<span data-ttu-id="4e3f1-121">Ensuite, hello de partage de fichiers a besoin toobe monté sur chaque ordinateur virtuel à l’intérieur de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-121">Next, hello file share needs toobe mounted on every virtual machine inside your cluster.</span></span> <span data-ttu-id="4e3f1-122">Cette tâche est effectuée à l’aide de hello cifs outil/protocole.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-122">This task is completed using hello cifs tool/protocol.</span></span> <span data-ttu-id="4e3f1-123">opération de montage Hello peut être effectuée manuellement sur chaque nœud du cluster de hello, ou en exécutant un script sur chaque nœud de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-123">hello mount operation can be completed manually on each node of hello cluster, or by running a script against each node in hello cluster.</span></span>

<span data-ttu-id="4e3f1-124">Dans cet exemple, deux scripts sont exécutés, une toomount hello Azure partage de fichiers et une deuxième toorun ce script sur chaque nœud du cluster de contrôleur de domaine/système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-124">In this example, two scripts are run, one toomount hello Azure file share, and a second toorun this script on each node of hello DC/OS cluster.</span></span>

<span data-ttu-id="4e3f1-125">Tout d’abord, le nom de compte de stockage Windows Azure hello et la clé d’accès sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-125">First, hello Azure storage account name, and access key are needed.</span></span> <span data-ttu-id="4e3f1-126">Exécutez hello suivant de commandes tooget ces informations.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-126">Run hello following commands tooget this information.</span></span> <span data-ttu-id="4e3f1-127">Notez-les, car elles vont être utiles à une prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-127">Take note of each, these values are used in a later step.</span></span>

<span data-ttu-id="4e3f1-128">Nom du compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="4e3f1-128">Storage account name:</span></span>

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

<span data-ttu-id="4e3f1-129">Clé d’accès au compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="4e3f1-129">Storage account access key:</span></span>

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

<span data-ttu-id="4e3f1-130">Ensuite, obtenez hello hello DC/OS maître et le stocker dans une variable de nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-130">Next, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="4e3f1-131">Copiez votre nœud principal toohello de clé privée.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-131">Copy your private key toohello master node.</span></span> <span data-ttu-id="4e3f1-132">Cette clé est nécessaire toocreate un ssh connexion avec tous les nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-132">This key is needed toocreate an ssh connection with all nodes in hello cluster.</span></span> <span data-ttu-id="4e3f1-133">Modifiez le nom d’utilisateur de hello si une valeur par défaut a été utilisée lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-133">Update hello user name if a non-default value was used when creating hello cluster.</span></span> 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

<span data-ttu-id="4e3f1-134">Créez une connexion SSH avec hello masque (ou de hello première) de votre cluster basé sur le système d’exploitation contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-134">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="4e3f1-135">Modifiez le nom d’utilisateur de hello si une valeur par défaut a été utilisée lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-135">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="4e3f1-136">Créez un fichier nommé **cifsMount.sh**, et en hello de copie suivant contenu dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-136">Create a file named **cifsMount.sh**, and copy hello following contents into it.</span></span> 

<span data-ttu-id="4e3f1-137">Ce script est un partage de fichiers Azure hello toomount utilisé.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-137">This script is used toomount hello Azure file share.</span></span> <span data-ttu-id="4e3f1-138">Hello de mise à jour `STORAGE_ACCT_NAME` et `ACCESS_KEY` variables avec des informations de hello recueillies précédemment.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-138">Update hello `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with hello information collected earlier.</span></span>

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install hello cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create hello local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount hello share under hello previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
<span data-ttu-id="4e3f1-139">Créez un deuxième fichier nommé **getNodesRunScript.sh** et hello de copie suivant contenu dans le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-139">Create a second file named **getNodesRunScript.sh** and copy hello following contents into hello file.</span></span> 

<span data-ttu-id="4e3f1-140">Ce script détecte tous les nœuds de cluster, puis exécute hello **cifsMount.sh** partage de fichiers de script toomount hello sur chacun.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-140">This script discovers all cluster nodes, and then runs hello **cifsMount.sh** script toomount hello file share on each.</span></span>

```azurecli-interactive
#!/bin/bash

# Install jq used for hello next command
sudo apt-get install jq -y

# Get hello IP address of each node using hello mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From hello previous file created, run our script toomount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

<span data-ttu-id="4e3f1-141">Partage de fichiers Azure hello hello exécution script toomount sur tous les nœuds du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-141">Run hello script toomount hello Azure file share on all nodes of hello cluster.</span></span>

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

<span data-ttu-id="4e3f1-142">Hello partage de fichiers est désormais accessible à `/mnt/share/dcosshare` sur chaque nœud du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-142">hello file share is now accessible at `/mnt/share/dcosshare` on each node of hello cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e3f1-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e3f1-143">Next steps</span></span>

<span data-ttu-id="4e3f1-144">Dans ce didacticiel Azure partage de fichiers a été faite tooa disponible cluster de contrôleur de domaine/système d’exploitation à l’aide des étapes de hello :</span><span class="sxs-lookup"><span data-stu-id="4e3f1-144">In this tutorial an Azure file share was made available tooa DC/OS cluster using hello steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4e3f1-145">Création d'un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="4e3f1-145">Create an Azure storage account</span></span>
> * <span data-ttu-id="4e3f1-146">Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="4e3f1-146">Create a file share</span></span>
> * <span data-ttu-id="4e3f1-147">Monter le partage hello dans un cluster de contrôleur de domaine/système d’exploitation hello</span><span class="sxs-lookup"><span data-stu-id="4e3f1-147">Mount hello share in hello DC/OS cluster</span></span>

<span data-ttu-id="4e3f1-148">Avance toohello toolearn de didacticiel suivant sur l’intégration d’un Registre de conteneur Azure avec contrôleur de domaine/système d’exploitation dans Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3f1-148">Advance toohello next tutorial toolearn about integrating an Azure Container Registry with DC/OS in Azure.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="4e3f1-149">Équilibrer la charge des applications</span><span class="sxs-lookup"><span data-stu-id="4e3f1-149">Load balance applications</span></span>](container-service-dcos-acr.md)