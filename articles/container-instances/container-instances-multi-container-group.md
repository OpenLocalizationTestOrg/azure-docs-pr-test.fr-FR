---
title: aaaAzure conteneur Instances - groupe conteneur multi | Documentation Azure
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
ms.openlocfilehash: 976f578cd2a9bf7f05ab97f24662139bb72062ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-group"></a><span data-ttu-id="a0146-103">Déployer un groupe de conteneurs</span><span class="sxs-lookup"><span data-stu-id="a0146-103">Deploy a container group</span></span>

<span data-ttu-id="a0146-104">Les Instances du conteneur Azure prend en charge le déploiement de hello de plusieurs conteneurs sur un seul hôte à l’aide un *groupe conteneur*.</span><span class="sxs-lookup"><span data-stu-id="a0146-104">Azure Container Instances support hello deployment of multiple containers onto a single host using a *container group*.</span></span> <span data-ttu-id="a0146-105">Cela est utile lors de la création d’une annexe d’application pour la journalisation, la surveillance ou toute autre configuration dans laquelle un service a besoin d’un deuxième processus associé.</span><span class="sxs-lookup"><span data-stu-id="a0146-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span> 

<span data-ttu-id="a0146-106">Ce document décrit pas à pas une configuration simple d’annexe à plusieurs conteneurs à l’aide d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a0146-106">This document walks through running a simple multi-container sidecar configuration using an Azure Resource Manager template.</span></span>

## <a name="configure-hello-template"></a><span data-ttu-id="a0146-107">Configurer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="a0146-107">Configure hello template</span></span>

<span data-ttu-id="a0146-108">Créez un fichier nommé `azuredeploy.json` et hello de copie suivante json dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="a0146-108">Create a file named `azuredeploy.json` and copy hello following json into it.</span></span> 

<span data-ttu-id="a0146-109">Dans cet exemple, un groupe de conteneurs comprenant deux conteneurs et une adresse IP publique est défini.</span><span class="sxs-lookup"><span data-stu-id="a0146-109">In this sample, a container group with two containers and a public IP address is defined.</span></span> <span data-ttu-id="a0146-110">premier conteneur d’Hello du groupe de hello s’exécute une application exposés à internet.</span><span class="sxs-lookup"><span data-stu-id="a0146-110">hello first container of hello group runs an internet facing application.</span></span> <span data-ttu-id="a0146-111">second conteneur Hello, annexe de hello, permet à une application de site web principal de toohello de demande HTTP via le réseau local du groupe hello.</span><span class="sxs-lookup"><span data-stu-id="a0146-111">hello second container, hello sidecar, makes an HTTP request toohello main web application via hello group's local network.</span></span> 

<span data-ttu-id="a0146-112">Cet exemple annexe peut être développé tootrigger une alerte si elle a reçu un code de réponse HTTP autre que 200 OK.</span><span class="sxs-lookup"><span data-stu-id="a0146-112">This sidecar example could be expanded tootrigger an alert if it received an HTTP response code other than 200 OK.</span></span> 

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

<span data-ttu-id="a0146-113">toouse un registre d’image de conteneur privé, ajouter un document json d’objet toohello avec hello suivant le format.</span><span class="sxs-lookup"><span data-stu-id="a0146-113">toouse a private container image registry, add an object toohello json document with hello following format.</span></span>

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a><span data-ttu-id="a0146-114">Déployer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="a0146-114">Deploy hello template</span></span>

<span data-ttu-id="a0146-115">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="a0146-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="a0146-116">Déployer le modèle hello avec hello [créer de déploiement de groupe az](/cli/azure/group/deployment#create) commande.</span><span class="sxs-lookup"><span data-stu-id="a0146-116">Deploy hello template with hello [az group deployment create](/cli/azure/group/deployment#create) command.</span></span>

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="a0146-117">Après quelques secondes, vous recevez une réponse initiale d’Azure.</span><span class="sxs-lookup"><span data-stu-id="a0146-117">Within a few seconds, you will receive an initial response from Azure.</span></span> 

## <a name="view-deployment-state"></a><span data-ttu-id="a0146-118">Afficher l’état du déploiement</span><span class="sxs-lookup"><span data-stu-id="a0146-118">View deployment state</span></span>

<span data-ttu-id="a0146-119">état de hello tooview de déploiement hello, utilisez hello `az container show` commande.</span><span class="sxs-lookup"><span data-stu-id="a0146-119">tooview hello state of hello deployment, use hello `az container show` command.</span></span> <span data-ttu-id="a0146-120">Cela retourne les adresse IP publique hello configuré sur le hello application est accessible.</span><span class="sxs-lookup"><span data-stu-id="a0146-120">This returns hello provisioned public IP address over which hello application can be accessed.</span></span>

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

<span data-ttu-id="a0146-121">Output:</span><span class="sxs-lookup"><span data-stu-id="a0146-121">Output:</span></span>

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="a0146-122">Consulter les journaux</span><span class="sxs-lookup"><span data-stu-id="a0146-122">View logs</span></span>   

<span data-ttu-id="a0146-123">Afficher la sortie du journal d’un conteneur à l’aide de hello hello `az container logs` commande.</span><span class="sxs-lookup"><span data-stu-id="a0146-123">View hello log output of a container using hello `az container logs` command.</span></span> <span data-ttu-id="a0146-124">Hello `--container-name` argument spécifie le conteneur de hello dans les journaux toopull.</span><span class="sxs-lookup"><span data-stu-id="a0146-124">hello `--container-name` argument specifies hello container from which toopull logs.</span></span> <span data-ttu-id="a0146-125">Dans cet exemple, le premier conteneur d’hello est spécifié.</span><span class="sxs-lookup"><span data-stu-id="a0146-125">In this example, hello first container is specified.</span></span> 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

<span data-ttu-id="a0146-126">Output:</span><span class="sxs-lookup"><span data-stu-id="a0146-126">Output:</span></span>

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="a0146-127">les journaux de toosee hello pour le conteneur de voiture de côté hello, exécutez hello même commande spécification du nom de conteneur deuxième hello.</span><span class="sxs-lookup"><span data-stu-id="a0146-127">toosee hello logs for hello side-car container, run hello same command specifying hello second container name.</span></span>

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

<span data-ttu-id="a0146-128">Output:</span><span class="sxs-lookup"><span data-stu-id="a0146-128">Output:</span></span>

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

<span data-ttu-id="a0146-129">Comme vous pouvez le voir, les annexes hello sont d’effectuer régulièrement une application web principale de HTTP demande toohello via tooensure de réseau local du groupe hello qu’elle s’exécute.</span><span class="sxs-lookup"><span data-stu-id="a0146-129">As you can see, hello sidecar is periodically making an HTTP request toohello main web application via hello group's local network tooensure that it is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0146-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0146-130">Next steps</span></span>

<span data-ttu-id="a0146-131">Ce document couverte étapes hello nécessaires au déploiement d’un conteneur de plusieurs instance du conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="a0146-131">This document covered hello steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="a0146-132">Pour une fin tooend que rencontrer des Instances de conteneurs Azure, consultez le didacticiel d’Instances de conteneurs Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a0146-132">For an end tooend Azure Container Instances experience, see hello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="a0146-133">[Didacticiel Azure Container Instances]: ./container-instances-tutorial-prepare-app.md</span><span class="sxs-lookup"><span data-stu-id="a0146-133">[Azure Container Instances tutorial]: ./container-instances-tutorial-prepare-app.md</span></span>
