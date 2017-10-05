---
title: Partage de fichiers pour un cluster DC/OS Azure | Microsoft Docs
description: "Créer et monter un partage de fichiers sur un cluster DC/OS dans Azure Container Service"
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
ms.openlocfilehash: 549b52bfb0a0268f754da26c6a374b267861f6d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-mount-a-file-share-to-a-dcos-cluster"></a><span data-ttu-id="3a17f-104">Créer et monter un partage de fichiers sur un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="3a17f-104">Create and mount a file share to a DC/OS cluster</span></span>
<span data-ttu-id="3a17f-105">Ce didacticiel explique en détail comment créer un partage de fichiers dans Azure et comment le monter sur chaque agent et chaque maître du cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="3a17f-105">This tutorial details how to create a file share in Azure and mount it on each agent and master of the DC/OS cluster.</span></span> <span data-ttu-id="3a17f-106">La configuration d’un partage de fichiers facilite le partage de fichiers sur votre cluster, par exemple la configuration, l’accès, les journaux et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="3a17f-106">Setting up a file share makes it easier to share files across your cluster such as configuration, access, logs, and more.</span></span> <span data-ttu-id="3a17f-107">Dans ce didacticiel, les tâches suivantes sont effectuées :</span><span class="sxs-lookup"><span data-stu-id="3a17f-107">The following tasks are completed in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3a17f-108">Créer un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="3a17f-108">Create an Azure storage account</span></span>
> * <span data-ttu-id="3a17f-109">Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="3a17f-109">Create a file share</span></span>
> * <span data-ttu-id="3a17f-110">Montage du partage sur votre cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="3a17f-110">Mount the share in the DC/OS cluster</span></span>

<span data-ttu-id="3a17f-111">Vous avez besoin d’un cluster DC/OS ACS pour suivre les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="3a17f-111">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="3a17f-112">Le cas échéant, cet [exemple de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) peut en créer un pour vous.</span><span class="sxs-lookup"><span data-stu-id="3a17f-112">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="3a17f-113">Ce didacticiel requiert Azure CLI version 2.0.4 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3a17f-113">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3a17f-114">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="3a17f-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="3a17f-115">Si vous devez effectuer une mise à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3a17f-115">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a><span data-ttu-id="3a17f-116">Créer un partage de fichiers sur Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3a17f-116">Create a file share on Microsoft Azure</span></span>

<span data-ttu-id="3a17f-117">Avant d’utiliser un partage de fichiers Azure avec un cluster ACS DC/OS, vous devez créer le compte de stockage et le partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="3a17f-117">Before using an Azure file share with an ACS DC/OS cluster, the storage account and file share must be created.</span></span> <span data-ttu-id="3a17f-118">Exécutez le script suivant pour créer le stockage et le partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="3a17f-118">Run the following script to create the storage and file share.</span></span> <span data-ttu-id="3a17f-119">Mettez à jour les paramètres avec ceux de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="3a17f-119">Update the parameters with thoes from your environment.</span></span>

```azurecli-interactive
# Change these four parameters
DCOS_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
DCOS_PERS_RESOURCE_GROUP=myResourceGroup
DCOS_PERS_LOCATION=eastus
DCOS_PERS_SHARE_NAME=dcosshare

# Create the storage account with the parameters
az storage account create -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -l $DCOS_PERS_LOCATION --sku Standard_LRS

# Export the connection string as an environment variable, this is used when creating the Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $DCOS_PERS_STORAGE_ACCOUNT_NAME -g $DCOS_PERS_RESOURCE_GROUP -o tsv`

# Create the share
az storage share create -n $DCOS_PERS_SHARE_NAME
```

## <a name="mount-the-share-in-your-cluster"></a><span data-ttu-id="3a17f-120">Monter le partage sur votre cluster</span><span class="sxs-lookup"><span data-stu-id="3a17f-120">Mount the share in your cluster</span></span>

<span data-ttu-id="3a17f-121">Ensuite, le partage de fichiers doit être monté sur chaque machine virtuelle à l’intérieur de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="3a17f-121">Next, the file share needs to be mounted on every virtual machine inside your cluster.</span></span> <span data-ttu-id="3a17f-122">Cette tâche est effectuée à l’aide de l’outil/protocole cifs.</span><span class="sxs-lookup"><span data-stu-id="3a17f-122">This task is completed using the cifs tool/protocol.</span></span> <span data-ttu-id="3a17f-123">Vous pouvez effectuer manuellement cette opération de montage sur chaque nœud du cluster, ou exécuter un script sur chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="3a17f-123">The mount operation can be completed manually on each node of the cluster, or by running a script against each node in the cluster.</span></span>

<span data-ttu-id="3a17f-124">Dans cet exemple, deux scripts sont exécutés, l’un pour monter le partage de fichiers Azure, l’autre pour exécuter ce script sur chaque nœud du cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="3a17f-124">In this example, two scripts are run, one to mount the Azure file share, and a second to run this script on each node of the DC/OS cluster.</span></span>

<span data-ttu-id="3a17f-125">Tout d’abord, vous devez connaître le nom du compte de stockage Azure et la clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="3a17f-125">First, the Azure storage account name, and access key are needed.</span></span> <span data-ttu-id="3a17f-126">Pour récupérer ces informations, utilisez les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="3a17f-126">Run the following commands to get this information.</span></span> <span data-ttu-id="3a17f-127">Notez-les, car elles vont être utiles à une prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="3a17f-127">Take note of each, these values are used in a later step.</span></span>

<span data-ttu-id="3a17f-128">Nom du compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="3a17f-128">Storage account name:</span></span>

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

<span data-ttu-id="3a17f-129">Clé d’accès au compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="3a17f-129">Storage account access key:</span></span>

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

<span data-ttu-id="3a17f-130">Récupérez ensuite le nom de domaine complet du maître DC/OS et stockez-le dans une variable.</span><span class="sxs-lookup"><span data-stu-id="3a17f-130">Next, get the FQDN of the DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="3a17f-131">Copiez votre clé privée dans le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="3a17f-131">Copy your private key to the master node.</span></span> <span data-ttu-id="3a17f-132">Cette clé est nécessaire pour créer une connexion ssh avec tous les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="3a17f-132">This key is needed to create an ssh connection with all nodes in the cluster.</span></span> <span data-ttu-id="3a17f-133">Si une valeur non définie par défaut a été utilisée lors de la création du cluster, mettez à jour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3a17f-133">Update the user name if a non-default value was used when creating the cluster.</span></span> 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

<span data-ttu-id="3a17f-134">Connectez-vous par SSH au maître (ou premier maître) de votre cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="3a17f-134">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="3a17f-135">Si une valeur non définie par défaut a été utilisée lors de la création du cluster, mettez à jour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3a17f-135">Update the user name if a non-default value was used when creating the cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="3a17f-136">Créez un fichier nommé **cifsMount.sh** et copiez le contenu suivant dedans.</span><span class="sxs-lookup"><span data-stu-id="3a17f-136">Create a file named **cifsMount.sh**, and copy the following contents into it.</span></span> 

<span data-ttu-id="3a17f-137">Ce script est utilisé pour monter le partage de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="3a17f-137">This script is used to mount the Azure file share.</span></span> <span data-ttu-id="3a17f-138">Mettez à jour les variables `STORAGE_ACCT_NAME` et `ACCESS_KEY` avec les informations recueillies précédemment.</span><span class="sxs-lookup"><span data-stu-id="3a17f-138">Update the `STORAGE_ACCT_NAME` and `ACCESS_KEY` variables with the information collected earlier.</span></span>

```azurecli-interactive
#!/bin/bash

# Azure storage account name and access key
STORAGE_ACCT_NAME=mystorageaccount
ACCESS_KEY=mystorageaccountKey

# Install the cifs utils, should be already installed
sudo apt-get update && sudo apt-get -y install cifs-utils

# Create the local folder that will contain our share
if [ ! -d "/mnt/share/dcosshare" ]; then sudo mkdir -p "/mnt/share/dcosshare" ; fi

# Mount the share under the previous local folder created
sudo mount -t cifs //$STORAGE_ACCT_NAME.file.core.windows.net/dcosshare /mnt/share/dcosshare -o vers=3.0,username=$STORAGE_ACCT_NAME,password=$ACCESS_KEY,dir_mode=0777,file_mode=0777
```
<span data-ttu-id="3a17f-139">Créez un deuxième fichier nommé **getNodesRunScript.sh** et copiez le contenu suivant dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="3a17f-139">Create a second file named **getNodesRunScript.sh** and copy the following contents into the file.</span></span> 

<span data-ttu-id="3a17f-140">Ce script détecte tous les nœuds de cluster, puis exécute le script **cifsMount.sh** pour monter le partage de fichiers sur chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="3a17f-140">This script discovers all cluster nodes, and then runs the **cifsMount.sh** script to mount the file share on each.</span></span>

```azurecli-interactive
#!/bin/bash

# Install jq used for the next command
sudo apt-get install jq -y

# Get the IP address of each node using the mesos API and store it inside a file called nodes
curl http://leader.mesos:1050/system/health/v1/nodes | jq '.nodes[].host_ip' | sed 's/\"//g' | sed '/172/d' > nodes

# From the previous file created, run our script to mount our share on each node
cat nodes | while read line
do
  ssh `whoami`@$line -o StrictHostKeyChecking=no < ./cifsMount.sh
  done
```

<span data-ttu-id="3a17f-141">Exécutez le script pour monter le partage de fichiers Azure sur tous les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="3a17f-141">Run the script to mount the Azure file share on all nodes of the cluster.</span></span>

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

<span data-ttu-id="3a17f-142">Le partage de fichiers est désormais accessible sur `/mnt/share/dcosshare` dans chaque nœud du cluster.</span><span class="sxs-lookup"><span data-stu-id="3a17f-142">The file share is now accessible at `/mnt/share/dcosshare` on each node of the cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a17f-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3a17f-143">Next steps</span></span>

<span data-ttu-id="3a17f-144">Dans ce didacticiel, un partage de fichiers Azure a été rendu disponible sur un cluster DC/OS en suivant les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="3a17f-144">In this tutorial an Azure file share was made available to a DC/OS cluster using the steps:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3a17f-145">Créer un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="3a17f-145">Create an Azure storage account</span></span>
> * <span data-ttu-id="3a17f-146">Créer un partage de fichiers</span><span class="sxs-lookup"><span data-stu-id="3a17f-146">Create a file share</span></span>
> * <span data-ttu-id="3a17f-147">Monter le partage sur votre cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="3a17f-147">Mount the share in the DC/OS cluster</span></span>

<span data-ttu-id="3a17f-148">Passez au didacticiel suivant pour en savoir plus sur l’intégration d’un service Azure Container Registry avec DC/OS dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3a17f-148">Advance to the next tutorial to learn about integrating an Azure Container Registry with DC/OS in Azure.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="3a17f-149">Équilibrer la charge des applications</span><span class="sxs-lookup"><span data-stu-id="3a17f-149">Load balance applications</span></span>](container-service-dcos-acr.md)