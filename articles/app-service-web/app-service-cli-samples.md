---
title: "aaaAzure CLI exemples - Service d’applications | Documents Microsoft"
description: "Exemples d’interface de ligne de commande - App Service"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: 53e6a15a-370a-48df-8618-c6737e26acec
ms.service: app-service
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: a943ccffb59c5d30a44cf1ce513fd2eac46101f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples"></a>Exemples d’interface de ligne de commande Azure

Hello tableau suivant inclut des liens toobash scripts créés à l’aide de hello CLI d’Azure.

| | |
|-|-|
|**Créer une application**||
| [Créer une application web et déployer le code à partir de GitHub](./scripts/app-service-cli-deploy-github.md?toc=%2fcli%2fazure%2ftoc.json)| Crée une application web Azure et déploie le code à partir d’un référentiel GitHub public. |
| [Créer une application web avec un déploiement continu à partir de GitHub](./scripts/app-service-cli-continuous-deployment-github.md?toc=%2fcli%2fazure%2ftoc.json)| Crée une application web Azure avec la publication continue à partir d’un référentiel GitHub dont vous êtes le propriétaire. |
| [Créer une application web et déployer le code à partir d’un référentiel Git](./scripts/app-service-cli-deploy-local-git.md?toc=%2fcli%2fazure%2ftoc.json) | Crée une application web Azure et configure la transmission de code de type push à partir d’un référentiel Git local. |
| [Créer une application web et de déployer tooa code environnement intermédiaire](./scripts/app-service-cli-deploy-staging-environment.md?toc=%2fcli%2fazure%2ftoc.json) | Crée une application web Azure avec un emplacement de déploiement pour les modifications de code intermédiaires. |
| [Créer une application web ASP.NET Core dans un conteneur Docker](./scripts/app-service-cli-linux-docker-aspnetcore.md?toc=%2fcli%2fazure%2ftoc.json)| Crée une application web Azure sur Linux et charge une image Docker à partir de Docker Hub. |
|**Configurer l’application**||
| [Mapper une domaine personnalisé tooa l’application web](./scripts/app-service-cli-configure-custom-domain.md?toc=%2fcli%2fazure%2ftoc.json)| Crée une application web Azure et mappe un tooit de nom de domaine personnalisé. |
| [Lier une application du web tooa de certificat SSL personnalisée](./scripts/app-service-cli-configure-ssl-certificate.md?toc=%2fcli%2fazure%2ftoc.json)| Crée une application web Azure et lie le certificat SSL de hello d’un tooit de nom de domaine personnalisé. |
|**Mettre à l’échelle une application**||
| [Mettre à l’échelle une application web manuellement](./scripts/app-service-cli-scale-manual.md?toc=%2fcli%2fazure%2ftoc.json) | Crée une application web Azure et la met à l’échelle entre 2 instances. |
| [Mettre à l’échelle une application web dans le monde entier avec une architecture haute disponibilité](./scripts/app-service-cli-scale-high-availability.md?toc=%2fcli%2fazure%2ftoc.json) | Crée deux applications web Azure dans deux régions géographiques différentes et les rend disponibles par le biais d’un point de terminaison unique à l’aide d’Azure Traffic Manager. |
|**Se connecter tooresources d’application**||
| [Se connecter à un tooa d’application web de la base de données SQL](./scripts/app-service-cli-app-service-sql.md?toc=%2fcli%2fazure%2ftoc.json)| Crée une application web Azure et une base de données SQL, puis ajoute les paramètres de l’application hello de base de données connexion chaîne toohello. |
| [Se connecter à un compte de stockage tooa application web](./scripts/app-service-cli-app-service-storage.md?toc=%2fcli%2fazure%2ftoc.json)| Crée une application web Azure et un compte de stockage, puis ajoute les paramètres de l’application hello stockage connexion chaîne toohello. |
| [Se connecter à un cache de redis tooa web app](./scripts/app-service-cli-app-service-redis.md?toc=%2fcli%2fazure%2ftoc.json) | Crée une application web Azure et un cache redis, puis ajoute les paramètres de l’application hello redis connexion détails toohello.) |
| [Se connecter à un tooCosmos d’application web DB](./scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json) | Crée une application web Azure et une base de données Cosmos, puis ajoute les paramètres de l’application hello Cosmos DB connexion détails toohello. |
|**Surveiller l’application**||
| [Analyser une application web avec les journaux de serveur web](./scripts/app-service-cli-monitor.md?toc=%2fcli%2fazure%2ftoc.json) | Crée une application web Azure, Active la journalisation pour elle et télécharge l’ordinateur local de hello journaux tooyour. |
| | |