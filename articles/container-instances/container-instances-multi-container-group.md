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
# <a name="deploy-a-container-group"></a>Déployer un groupe de conteneurs

Les Instances du conteneur Azure prend en charge le déploiement de hello de plusieurs conteneurs sur un seul hôte à l’aide un *groupe conteneur*. Cela est utile lors de la création d’une annexe d’application pour la journalisation, la surveillance ou toute autre configuration dans laquelle un service a besoin d’un deuxième processus associé. 

Ce document décrit pas à pas une configuration simple d’annexe à plusieurs conteneurs à l’aide d’un modèle Azure Resource Manager.

## <a name="configure-hello-template"></a>Configurer le modèle de hello

Créez un fichier nommé `azuredeploy.json` et hello de copie suivante json dans celui-ci. 

Dans cet exemple, un groupe de conteneurs comprenant deux conteneurs et une adresse IP publique est défini. premier conteneur d’Hello du groupe de hello s’exécute une application exposés à internet. second conteneur Hello, annexe de hello, permet à une application de site web principal de toohello de demande HTTP via le réseau local du groupe hello. 

Cet exemple annexe peut être développé tootrigger une alerte si elle a reçu un code de réponse HTTP autre que 200 OK. 

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

toouse un registre d’image de conteneur privé, ajouter un document json d’objet toohello avec hello suivant le format.

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a>Déployer le modèle de hello

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

Déployer le modèle hello avec hello [créer de déploiement de groupe az](/cli/azure/group/deployment#create) commande.

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

Après quelques secondes, vous recevez une réponse initiale d’Azure. 

## <a name="view-deployment-state"></a>Afficher l’état du déploiement

état de hello tooview de déploiement hello, utilisez hello `az container show` commande. Cela retourne les adresse IP publique hello configuré sur le hello application est accessible.

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

Output:

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a>Consulter les journaux   

Afficher la sortie du journal d’un conteneur à l’aide de hello hello `az container logs` commande. Hello `--container-name` argument spécifie le conteneur de hello dans les journaux toopull. Dans cet exemple, le premier conteneur d’hello est spécifié. 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

Output:

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

les journaux de toosee hello pour le conteneur de voiture de côté hello, exécutez hello même commande spécification du nom de conteneur deuxième hello.

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

Output:

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

Comme vous pouvez le voir, les annexes hello sont d’effectuer régulièrement une application web principale de HTTP demande toohello via tooensure de réseau local du groupe hello qu’elle s’exécute.

## <a name="next-steps"></a>Étapes suivantes

Ce document couverte étapes hello nécessaires au déploiement d’un conteneur de plusieurs instance du conteneur Azure. Pour une fin tooend que rencontrer des Instances de conteneurs Azure, consultez le didacticiel d’Instances de conteneurs Azure hello.

> [!div class="nextstepaction"]
> [Didacticiel Azure Container Instances]: ./container-instances-tutorial-prepare-app.md
