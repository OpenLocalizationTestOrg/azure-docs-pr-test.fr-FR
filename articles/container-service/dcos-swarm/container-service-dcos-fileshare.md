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
# <a name="create-and-mount-a-file-share-tooa-dcos-cluster"></a>Créer et monter un cluster de contrôleur de domaine/système d’exploitation de tooa partage de fichiers
Ce didacticiel décrit en détail comment toocreate un fichier de partage dans Azure et l’installer sur chaque agent et le masque de hello cluster du contrôleur de domaine/système d’exploitation. Configuration d’un partage de fichiers rend plus facile tooshare fichiers sur votre cluster telles que la configuration, l’accès, les journaux et bien plus encore. Bonjour tâches suivantes est effectuée dans ce didacticiel :

> [!div class="checklist"]
> * Création d'un compte de stockage Azure
> * Créer un partage de fichiers
> * Monter le partage hello dans un cluster de contrôleur de domaine/système d’exploitation hello

Vous avez besoin d’un contrôleur de domaine/OS ACS hello toocomplete de cluster les étapes de ce didacticiel. Le cas échéant, cet [exemple de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) peut en créer un pour vous.

Ce didacticiel requiert hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-file-share-on-microsoft-azure"></a>Créer un partage de fichiers sur Microsoft Azure

Avant d’utiliser un partage de fichiers Azure avec un cluster ACS contrôleur de domaine/système d’exploitation, le partage de fichier et de compte de stockage hello doit être créé. Exécutez hello suivant script toocreate hello stockage et le fichier partage. Mettre à jour les paramètres hello spéciales à partir de votre environnement.

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

## <a name="mount-hello-share-in-your-cluster"></a>Monter le partage hello dans votre cluster

Ensuite, hello de partage de fichiers a besoin toobe monté sur chaque ordinateur virtuel à l’intérieur de votre cluster. Cette tâche est effectuée à l’aide de hello cifs outil/protocole. opération de montage Hello peut être effectuée manuellement sur chaque nœud du cluster de hello, ou en exécutant un script sur chaque nœud de cluster de hello.

Dans cet exemple, deux scripts sont exécutés, une toomount hello Azure partage de fichiers et une deuxième toorun ce script sur chaque nœud du cluster de contrôleur de domaine/système d’exploitation hello.

Tout d’abord, le nom de compte de stockage Windows Azure hello et la clé d’accès sont nécessaires. Exécutez hello suivant de commandes tooget ces informations. Notez-les, car elles vont être utiles à une prochaine étape.

Nom du compte de stockage :

```azurecli-interactive
STORAGE_ACCT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCT
```

Clé d’accès au compte de stockage :

```azurecli-interactive
az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCT --query "[0].value" -o tsv
```

Ensuite, obtenez hello hello DC/OS maître et le stocker dans une variable de nom de domaine complet.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Copiez votre nœud principal toohello de clé privée. Cette clé est nécessaire toocreate un ssh connexion avec tous les nœuds de cluster de hello. Modifiez le nom d’utilisateur de hello si une valeur par défaut a été utilisée lors de la création du cluster de hello. 

```azurecli-interactive
scp ~/.ssh/id_rsa azureuser@$FQDN:~/.ssh
```

Créez une connexion SSH avec hello masque (ou de hello première) de votre cluster basé sur le système d’exploitation contrôleur de domaine. Modifiez le nom d’utilisateur de hello si une valeur par défaut a été utilisée lors de la création du cluster de hello.

```azurecli-interactive
ssh azureuser@$FQDN
```

Créez un fichier nommé **cifsMount.sh**, et en hello de copie suivant contenu dans celui-ci. 

Ce script est un partage de fichiers Azure hello toomount utilisé. Hello de mise à jour `STORAGE_ACCT_NAME` et `ACCESS_KEY` variables avec des informations de hello recueillies précédemment.

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
Créez un deuxième fichier nommé **getNodesRunScript.sh** et hello de copie suivant contenu dans le fichier de hello. 

Ce script détecte tous les nœuds de cluster, puis exécute hello **cifsMount.sh** partage de fichiers de script toomount hello sur chacun.

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

Partage de fichiers Azure hello hello exécution script toomount sur tous les nœuds du cluster de hello.

```azurecli-interactive
sh ./getNodesRunScript.sh
```  

Hello partage de fichiers est désormais accessible à `/mnt/share/dcosshare` sur chaque nœud du cluster de hello.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel Azure partage de fichiers a été faite tooa disponible cluster de contrôleur de domaine/système d’exploitation à l’aide des étapes de hello :

> [!div class="checklist"]
> * Création d'un compte de stockage Azure
> * Créer un partage de fichiers
> * Monter le partage hello dans un cluster de contrôleur de domaine/système d’exploitation hello

Avance toohello toolearn de didacticiel suivant sur l’intégration d’un Registre de conteneur Azure avec contrôleur de domaine/système d’exploitation dans Azure.  

> [!div class="nextstepaction"]
> [Équilibrer la charge des applications](container-service-dcos-acr.md)