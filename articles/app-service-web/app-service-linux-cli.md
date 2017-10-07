---
title: "aaaManage l’application Web sur Linux à l’aide d’Azure CLI 2.0 | Documents Microsoft"
description: "Gérez l’application web sur Linux à l’aide d’Azure CLI."
keywords: azure app service, application web, cli, linux, oss
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a>Gérer l’application web sur Linux à l’aide d’Azure CLI

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

À l’aide des commandes hello dans cet article sont en mesure de toocreate et gérer une application Web sur Linux à l’aide d’Azure CLI 2.0.
Vous pouvez commencer à l’aide de la nouvelle version de hello Hello CLI de deux manières :

* [Installation d’Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) sur votre ordinateur.
* Utilisation d’[Azure Cloud Shell (version préliminaire)](../cloud-shell/overview.md)


## <a name="create-a-linux-app-service-plan"></a>Créer un plan App Service Linux

toocreate un Plan de Service d’application Linux, vous pouvez utiliser hello de commande suivante :

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a>Créer une application web de conteneur Docker personnalisé

toocreate une application web et configuration toorun conteneur Docker personnalisé, vous pouvez utiliser hello de commande suivante :

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a>Activer la journalisation de conteneur Docker hello

tooactivate hello journalisation du conteneur Docker, vous pouvez utiliser des hello de commande suivante :

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a>Modifier le conteneur Docker personnalisé de hello pour une application Web existante sur Linux d’application

toochange une application créée précédemment, à partir de hello Docker image tooa nouvelle image actuelle, vous pouvez utiliser hello de commande suivante :

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a>Utilisation d’images Docker d’un registre privé

Vous pouvez configurer des images de toouse votre application à partir d’un Registre privé. Vous devez tooprovide hello url pour votre Registre, le nom d’utilisateur et le mot de passe. Cela peut être obtenue à l’aide de hello de commande suivante :

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>Activer les déploiements continus d’images Docker personnalisées

Avec hello commande suivante, vous pouvez activer la fonctionnalité de CD hello et obtenir l’url du webhook hello. Cette url peut être utilisé tooconfigure vous référentiels docker Hub ou le Registre de conteneur Azure.

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a>Créer une application web sur l’application Linux à l’aide de l’une de nos infrastructures d’exécution intégrées

toocreate application Web PHP 5.6 sur application Linux, vous pouvez utiliser hello commande suivante.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a>Modifier la version de l’infrastructure pour une application web existante sur l’application Linux

toochange une application créée précédemment, à partir de tooNode.js de version de framework actuel hello 6.11, vous pouvez utiliser hello de commande suivante :

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a>Configurer des déploiements Git pour votre application web

tooset des déploiements Git pour votre application, vous pouvez utiliser hello de commande suivante :

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a>Étapes suivantes
* [Qu’est-ce qu’Azure Web App sur Linux ?](app-service-linux-intro.md)
* [Installation d’Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Azure Cloud Shell (version préliminaire)](../cloud-shell/overview.md)
* [Configurer des environnements intermédiaires dans Azure App Service](./web-sites-staged-publishing.md)
* [Déploiement continu avec l’application web Azure sur Linux](./app-service-linux-ci-cd.md)
