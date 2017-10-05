---
title: Azure Container Instances - Groupe de conteneurs | Azure Docs
description: Azure Container Instances - Groupe de conteneurs
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 140f58582645ea32f77e901eb13364ed145bbecf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-container-group"></a><span data-ttu-id="6a787-103">Déployer un groupe de conteneurs</span><span class="sxs-lookup"><span data-stu-id="6a787-103">Deploy a container group</span></span>

<span data-ttu-id="6a787-104">Azure Container Instances prend en charge le déploiement de plusieurs conteneurs sur un seul hôte à l’aide d’un *groupe de conteneurs*.</span><span class="sxs-lookup"><span data-stu-id="6a787-104">Azure Container Instances support the deployment of multiple containers onto a single host using a *container group*.</span></span> <span data-ttu-id="6a787-105">Cela est utile lors de la création d’une annexe d’application pour la journalisation, la surveillance ou toute autre configuration dans laquelle un service a besoin d’un deuxième processus associé.</span><span class="sxs-lookup"><span data-stu-id="6a787-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span> 

<span data-ttu-id="6a787-106">Ce document décrit pas à pas une configuration simple d’annexe à plusieurs conteneurs à l’aide d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6a787-106">This document walks through running a simple multi-container sidecar configuration using an Azure Resource Manager template.</span></span>

## <a name="configure-the-template"></a><span data-ttu-id="6a787-107">Configurer le modèle</span><span class="sxs-lookup"><span data-stu-id="6a787-107">Configure the template</span></span>

<span data-ttu-id="6a787-108">Créez un fichier nommé `azuredeploy.json`, puis copiez-y le json suivant.</span><span class="sxs-lookup"><span data-stu-id="6a787-108">Create a file named `azuredeploy.json` and copy the following json into it.</span></span> 

<span data-ttu-id="6a787-109">Dans cet exemple, un groupe de conteneurs comprenant deux conteneurs et une adresse IP publique est défini.</span><span class="sxs-lookup"><span data-stu-id="6a787-109">In this sample, a container group with two containers and a public IP address is defined.</span></span> <span data-ttu-id="6a787-110">Le premier conteneur du groupe exécute une application accessible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="6a787-110">The first container of the group runs an internet facing application.</span></span> <span data-ttu-id="6a787-111">Le deuxième conteneur, l’annexe, adresse une requête HTTP à l’application web principale via le réseau local du groupe.</span><span class="sxs-lookup"><span data-stu-id="6a787-111">The second container, the sidecar, makes an HTTP request to the main web application via the group's local network.</span></span> 

<span data-ttu-id="6a787-112">Cet exemple d’annexe peut être étendu pour déclencher une alerte suite à la réception d’un code de réponse HTTP autre que 200 OK.</span><span class="sxs-lookup"><span data-stu-id="6a787-112">This sidecar example could be expanded to trigger an alert if it received an HTTP response code other than 200 OK.</span></span> 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
  },
  "variables": {
    "container1name": "aci-tutorial-app",
    "container1image": "microsoft/aci-helloworld:latest",
    "container2name": "aci-tutorial-sidecar",    
    "container2image": "microsoft/aci-tutorial-sidecar"
  },
    "resources": [
      {
        "name": "myContainerGroup",
        "type": "Microsoft.ContainerInstance/containerGroups",
        "apiVersion": "2017-08-01-preview",
        "location": "[resourceGroup().location]",
        "properties": {
          "containers": [
            {
              "name": "[variables('container1name')]",
              "properties": {
                "image": "[variables('container1image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                },
                "ports": [
                  {
                    "port": 80
                  }
                ]
              }
            },
            {
              "name": "[variables('container2name')]",
              "properties": {
                "image": "[variables('container2image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                }
              }
            }
          ],
          "osType": "Linux",
          "ipAddress": {
            "type": "Public",
            "ports": [
              {
                "protocol": "tcp",
                "port": "80"
              }
            ]
          }
        }
      }
    ],
    "outputs": {
      "containerIPv4Address": {
        "type": "string",
        "value": "[reference(resourceId('Microsoft.ContainerInstance/containerGroups/', 'myContainerGroup')).ipAddress.ip]"
      }
    }
  }
```

<span data-ttu-id="6a787-113">Pour utiliser un registre d’image conteneur privé, ajoutez au document json un objet du format suivant.</span><span class="sxs-lookup"><span data-stu-id="6a787-113">To use a private container image registry, add an object to the json document with the following format.</span></span>

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-the-template"></a><span data-ttu-id="6a787-114">Déployer le modèle</span><span class="sxs-lookup"><span data-stu-id="6a787-114">Deploy the template</span></span>

<span data-ttu-id="6a787-115">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="6a787-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="6a787-116">Déployez ensuite le modèle avec la commande [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="6a787-116">Deploy the template with the [az group deployment create](/cli/azure/group/deployment#create) command.</span></span>

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="6a787-117">Après quelques secondes, vous recevez une réponse initiale d’Azure.</span><span class="sxs-lookup"><span data-stu-id="6a787-117">Within a few seconds, you will receive an initial response from Azure.</span></span> 

## <a name="view-deployment-state"></a><span data-ttu-id="6a787-118">Afficher l’état du déploiement</span><span class="sxs-lookup"><span data-stu-id="6a787-118">View deployment state</span></span>

<span data-ttu-id="6a787-119">Pour afficher l’état du déploiement, utilisez la commande `az container show`.</span><span class="sxs-lookup"><span data-stu-id="6a787-119">To view the state of the deployment, use the `az container show` command.</span></span> <span data-ttu-id="6a787-120">Celle-ci retourne l’adresse IP publique approvisionnée via laquelle l’application est accessible.</span><span class="sxs-lookup"><span data-stu-id="6a787-120">This returns the provisioned public IP address over which the application can be accessed.</span></span>

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

<span data-ttu-id="6a787-121">Sortie :</span><span class="sxs-lookup"><span data-stu-id="6a787-121">Output:</span></span>

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="6a787-122">Consulter les journaux</span><span class="sxs-lookup"><span data-stu-id="6a787-122">View logs</span></span>   

<span data-ttu-id="6a787-123">Consultez la sortie du journal d’un conteneur à l’aide de la commande `az container logs`.</span><span class="sxs-lookup"><span data-stu-id="6a787-123">View the log output of a container using the `az container logs` command.</span></span> <span data-ttu-id="6a787-124">L’argument `--container-name` spécifie le conteneur à partir duquel extraire les journaux.</span><span class="sxs-lookup"><span data-stu-id="6a787-124">The `--container-name` argument specifies the container from which to pull logs.</span></span> <span data-ttu-id="6a787-125">Dans cet exemple, le premier conteneur est spécifié.</span><span class="sxs-lookup"><span data-stu-id="6a787-125">In this example, the first container is specified.</span></span> 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

<span data-ttu-id="6a787-126">Sortie :</span><span class="sxs-lookup"><span data-stu-id="6a787-126">Output:</span></span>

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="6a787-127">Pour afficher les journaux du conteneur annexe, exécutez la même commande, en spécifiant le nom du deuxième conteneur.</span><span class="sxs-lookup"><span data-stu-id="6a787-127">To see the logs for the side-car container, run the same command specifying the second container name.</span></span>

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

<span data-ttu-id="6a787-128">Sortie :</span><span class="sxs-lookup"><span data-stu-id="6a787-128">Output:</span></span>

```bash
Every 3.0s: curl -I http://localhost                                                                                                                       Mon Jul 17 11:27:36 2017

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0  0  1663    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Length: 1663
Content-Type: text/html; charset=utf-8
Last-Modified: Sun, 16 Jul 2017 02:08:22 GMT
Date: Mon, 17 Jul 2017 18:27:36 GMT
```

<span data-ttu-id="6a787-129">Comme vous pouvez le voir, l’annexe envoie régulièrement une requête HTTP à l’application web principale via le réseau local du groupe pour s’assurer qu’il fonctionne.</span><span class="sxs-lookup"><span data-stu-id="6a787-129">As you can see, the sidecar is periodically making an HTTP request to the main web application via the group's local network to ensure that it is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a787-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6a787-130">Next steps</span></span>

<span data-ttu-id="6a787-131">Ce document a couvert les étapes nécessaires pour le déploiement d’une instance de conteneur Azure à plusieurs conteneurs.</span><span class="sxs-lookup"><span data-stu-id="6a787-131">This document covered the steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="6a787-132">Pour une expérience d’Azure Container Instances de bout en bout, voir le didacticiel d’Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="6a787-132">For an end to end Azure Container Instances experience, see the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="6a787-133">[Didacticiel Azure Container Instances]: ./container-instances-tutorial-prepare-app.md</span><span class="sxs-lookup"><span data-stu-id="6a787-133">[Azure Container Instances tutorial]: ./container-instances-tutorial-prepare-app.md</span></span>
