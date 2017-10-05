---
title: Exemple de script Azure CLI - Surveiller une application web avec les journaux de serveur web | Microsoft Docs
description: Exemple de script Azure CLI - Surveiller une application web avec les journaux de serveur web
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0887656f-611c-4627-8247-b5cded7cef60
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: df4ca5b1270ada849e231ad9608a5b1d2edda8be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="3d9ac-103">Surveiller une application web avec les journaux de serveur web</span><span class="sxs-lookup"><span data-stu-id="3d9ac-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="3d9ac-104">Dans ce scénario, vous créez un groupe de ressources, un plan App Service, une application web, et vous configurez l’application web afin d’activer les journaux de serveur web.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="3d9ac-105">Vous téléchargez ensuite les fichiers journaux pour révision.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-105">You will then download the log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3d9ac-106">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3d9ac-107">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="3d9ac-108">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3d9ac-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="3d9ac-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="3d9ac-109">Sample script</span></span>

<span data-ttu-id="3d9ac-110">[!code-azurecli-interactive[principal](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Surveiller les journaux")]</span><span class="sxs-lookup"><span data-stu-id="3d9ac-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="3d9ac-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="3d9ac-111">Script explanation</span></span>

<span data-ttu-id="3d9ac-112">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="3d9ac-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3d9ac-114">Commande</span><span class="sxs-lookup"><span data-stu-id="3d9ac-114">Command</span></span> | <span data-ttu-id="3d9ac-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="3d9ac-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3d9ac-116">az group create</span><span class="sxs-lookup"><span data-stu-id="3d9ac-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3d9ac-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3d9ac-118">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="3d9ac-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="3d9ac-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-119">Creates an App Service plan.</span></span> <span data-ttu-id="3d9ac-120">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="3d9ac-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="3d9ac-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="3d9ac-122">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="3d9ac-123">az webapp log config</span><span class="sxs-lookup"><span data-stu-id="3d9ac-123">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="3d9ac-124">Configure les journaux dans lesquels une application web Azure est conservée.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-124">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="3d9ac-125">az webapp log download</span><span class="sxs-lookup"><span data-stu-id="3d9ac-125">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="3d9ac-126">Télécharge les journaux d’une application web Azure sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="3d9ac-126">Downloads the logs of the an Azure web app to your local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3d9ac-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3d9ac-127">Next steps</span></span>

<span data-ttu-id="3d9ac-128">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3d9ac-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3d9ac-129">Vous trouverez des exemples supplémentaires de scripts CLI App Service dans la [documentation relative à Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3d9ac-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
