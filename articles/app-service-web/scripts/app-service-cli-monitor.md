---
title: aaaAzure exemple de Script CLI - analyser une application web avec les journaux du serveur web | Documents Microsoft
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
ms.openlocfilehash: 012b800c03af77387bed3d098fae3c96d82aee29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="946d8-103">Surveiller une application web avec les journaux de serveur web</span><span class="sxs-lookup"><span data-stu-id="946d8-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="946d8-104">Dans ce scénario, vous créez un groupe de ressources, le plan de service d’application, l’application web et configurer les journaux du serveur web tooenable hello web app.</span><span class="sxs-lookup"><span data-stu-id="946d8-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="946d8-105">Vous télécharge alors les fichiers de journaux hello pour révision.</span><span class="sxs-lookup"><span data-stu-id="946d8-105">You will then download hello log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="946d8-106">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="946d8-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="946d8-107">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="946d8-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="946d8-108">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="946d8-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="946d8-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="946d8-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="946d8-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="946d8-110">Script explanation</span></span>

<span data-ttu-id="946d8-111">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="946d8-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="946d8-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="946d8-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="946d8-113">Commande</span><span class="sxs-lookup"><span data-stu-id="946d8-113">Command</span></span> | <span data-ttu-id="946d8-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="946d8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="946d8-115">az group create</span><span class="sxs-lookup"><span data-stu-id="946d8-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="946d8-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="946d8-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="946d8-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="946d8-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="946d8-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="946d8-118">Creates an App Service plan.</span></span> <span data-ttu-id="946d8-119">Cela équivaut à une batterie de serveurs pour votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="946d8-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="946d8-120">az webapp create</span><span class="sxs-lookup"><span data-stu-id="946d8-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="946d8-121">Crée une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="946d8-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="946d8-122">az webapp log config</span><span class="sxs-lookup"><span data-stu-id="946d8-122">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="946d8-123">Configure les journaux dans lesquels une application web Azure est conservée.</span><span class="sxs-lookup"><span data-stu-id="946d8-123">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="946d8-124">az webapp log download</span><span class="sxs-lookup"><span data-stu-id="946d8-124">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="946d8-125">Téléchargements hello consigne de hello un ordinateur local du tooyour d’application web Azure.</span><span class="sxs-lookup"><span data-stu-id="946d8-125">Downloads hello logs of hello an Azure web app tooyour local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="946d8-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="946d8-126">Next steps</span></span>

<span data-ttu-id="946d8-127">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="946d8-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="946d8-128">Vous trouverez des exemples de script CLI de Service d’application supplémentaires Bonjour [documentation d’Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="946d8-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
