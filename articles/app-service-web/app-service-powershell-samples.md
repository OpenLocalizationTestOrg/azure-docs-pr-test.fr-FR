---
title: Exemples Azure PowerShell - App Service | Microsoft Docs
description: Exemples Azure PowerShell - App Service
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: b48d1137-8c04-46e0-b430-101e07d7e470
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 3254fdd57cfcd170f22374c1e3b058e6081d8e8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples"></a><span data-ttu-id="d1196-103">Exemples Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1196-103">Azure PowerShell Samples</span></span>

<span data-ttu-id="d1196-104">Le tableau suivant contient des liens vers des scripts Bash créés à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1196-104">The following table includes links to bash scripts built using the Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="d1196-105">**Créer une application**</span><span class="sxs-lookup"><span data-stu-id="d1196-105">**Create app**</span></span>||
| [<span data-ttu-id="d1196-106">Créer une application web avec un déploiement à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="d1196-106">Create a web app with deployment from GitHub</span></span>](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="d1196-107">Crée une application web Azure qui extrait le code à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="d1196-107">Creates an Azure web app which pulls code from GitHub.</span></span> |
| [<span data-ttu-id="d1196-108">Créer une application web avec un déploiement continu à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="d1196-108">Create a web app with continuous deployment from GitHub</span></span>](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="d1196-109">Crée une application web Azure qui déploie du code en continu à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="d1196-109">Creates an Azure web app which continuously deploys code from GitHub.</span></span> |
| [<span data-ttu-id="d1196-110">Créer une application web et déployer du code avec FTP</span><span class="sxs-lookup"><span data-stu-id="d1196-110">Create a web app and deploy code with FTP</span></span>](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="d1196-111">Crée une application web Azure et télécharge des fichiers à partir d’un répertoire local via FTP.</span><span class="sxs-lookup"><span data-stu-id="d1196-111">Creates an Azure web app and upload files from a local directory using FTP.</span></span> |
| [<span data-ttu-id="d1196-112">Créer une application web et déployer le code à partir d’un référentiel Git</span><span class="sxs-lookup"><span data-stu-id="d1196-112">Create a web app and deploy code from a local Git repository</span></span>](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="d1196-113">Crée une application web Azure et configure la transmission de code de type push à partir d’un référentiel Git local.</span><span class="sxs-lookup"><span data-stu-id="d1196-113">Creates an Azure web app and configures code push from a local Git repository.</span></span> |
| [<span data-ttu-id="d1196-114">Créer une application web et déployer le code dans un environnement intermédiaire</span><span class="sxs-lookup"><span data-stu-id="d1196-114">Create a web app and deploy code to a staging environment</span></span>](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="d1196-115">Crée une application web Azure avec un emplacement de déploiement pour les modifications de code intermédiaires.</span><span class="sxs-lookup"><span data-stu-id="d1196-115">Creates an Azure web app with a deployment slot for staging code changes.</span></span> |
|<span data-ttu-id="d1196-116">**Configurer l’application**</span><span class="sxs-lookup"><span data-stu-id="d1196-116">**Configure app**</span></span>||
| [<span data-ttu-id="d1196-117">Mapper un domaine personnalisé à une application web</span><span class="sxs-lookup"><span data-stu-id="d1196-117">Map a custom domain to a web app</span></span>](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="d1196-118">Crée une application web Azure et mappe un nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="d1196-118">Creates an Azure web app and maps a custom domain name to it.</span></span> |
| [<span data-ttu-id="d1196-119">Lier un certificat SSL personnalisé à une application web</span><span class="sxs-lookup"><span data-stu-id="d1196-119">Bind a custom SSL certificate to a web app</span></span>](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="d1196-120">Crée une application web Azure et lie le certificat SSL d’un nom de domaine personnalisé à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="d1196-120">Creates an Azure web app and binds the SSL certificate of a custom domain name to it.</span></span> |
|<span data-ttu-id="d1196-121">**Mettre à l’échelle une application**</span><span class="sxs-lookup"><span data-stu-id="d1196-121">**Scale app**</span></span>||
| [<span data-ttu-id="d1196-122">Mettre à l’échelle une application web manuellement</span><span class="sxs-lookup"><span data-stu-id="d1196-122">Scale a web app manually</span></span>](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="d1196-123">Crée une application web Azure et la met à l’échelle entre 2 instances.</span><span class="sxs-lookup"><span data-stu-id="d1196-123">Creates an Azure web app and scales it across 2 instances.</span></span> |
| [<span data-ttu-id="d1196-124">Mettre à l’échelle une application web dans le monde entier avec une architecture haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="d1196-124">Scale a web app worldwide with a high-availability architecture</span></span>](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="d1196-125">Crée deux applications web Azure dans deux régions géographiques différentes et les rend disponibles par le biais d’un point de terminaison unique à l’aide d’Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="d1196-125">Creates two Azure web apps in two different geographical regions and makes them available through a single endpoint using Azure Traffic Manager.</span></span> |
|<span data-ttu-id="d1196-126">**Connecter l’application aux ressources**</span><span class="sxs-lookup"><span data-stu-id="d1196-126">**Connect app to resources**</span></span>||
| [<span data-ttu-id="d1196-127">Connecter une application web à une instance SQL Database</span><span class="sxs-lookup"><span data-stu-id="d1196-127">Connect a web app to a SQL Database</span></span>](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="d1196-128">Crée une application web Azure et une instance SQL Database, puis ajoute la chaîne de connexion de base de données aux paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="d1196-128">Creates an Azure web app and a SQL database, then adds the database connection string to the app settings.</span></span> |
| [<span data-ttu-id="d1196-129">Connecter une application web à un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="d1196-129">Connect a web app to a storage account</span></span>](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="d1196-130">Crée une application web Azure et un compte de stockage, puis ajoute la chaîne de connexion de stockage aux paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="d1196-130">Creates an Azure web app and a storage account, then adds the storage connection string to the app settings.</span></span> |
|<span data-ttu-id="d1196-131">**Surveiller l’application**</span><span class="sxs-lookup"><span data-stu-id="d1196-131">**Monitor app**</span></span>||
| [<span data-ttu-id="d1196-132">Analyser une application web avec les journaux de serveur web</span><span class="sxs-lookup"><span data-stu-id="d1196-132">Monitor a web app with web server logs</span></span>](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="d1196-133">Crée une application web Azure, active sa journalisation et télécharge les journaux sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="d1196-133">Creates an Azure web app, enables logging for it, and downloads the logs to your local machine.</span></span> |
| | |
