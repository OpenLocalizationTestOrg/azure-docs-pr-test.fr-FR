---
title: "aaaCreate une fonction d’Azure qui se connecte tooan Azure Storage | Documents Microsoft"
description: "Le Script CLI Azure exemple : création d’une fonction d’Azure qui se connecte tooan stockage Azure"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: a51a2c17149478eb2d3d0d4034400ed00cd8416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="85547-103">Intégrer Function App à un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="85547-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="85547-104">Cet exemple de script crée une Function App et un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="85547-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="85547-105">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="85547-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="85547-106">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="85547-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="85547-107">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="85547-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="85547-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="85547-108">Sample script</span></span>

<span data-ttu-id="85547-109">Cet exemple crée une application de la fonction d’Azure et ajoute le paramètre d’application hello stockage connexion chaîne tooan.</span><span class="sxs-lookup"><span data-stu-id="85547-109">This sample creates an Azure Function app and adds hello storage connection string tooan app setting.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]


## <a name="clean-up-deployment"></a><span data-ttu-id="85547-110">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="85547-110">Clean up deployment</span></span>

<span data-ttu-id="85547-111">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello, application de Service d’applications et toutes les ressources :</span><span class="sxs-lookup"><span data-stu-id="85547-111">After hello script sample has been run, hello following command can be used tooremove hello resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="85547-112">Explication du script</span><span class="sxs-lookup"><span data-stu-id="85547-112">Script explanation</span></span>

<span data-ttu-id="85547-113">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="85547-113">This script uses hello following commands.</span></span> <span data-ttu-id="85547-114">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="85547-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="85547-115">Commande</span><span class="sxs-lookup"><span data-stu-id="85547-115">Command</span></span> | <span data-ttu-id="85547-116">Remarques</span><span class="sxs-lookup"><span data-stu-id="85547-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="85547-117">az login</span><span class="sxs-lookup"><span data-stu-id="85547-117">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="85547-118">TooAzure de connexion.</span><span class="sxs-lookup"><span data-stu-id="85547-118">Login tooAzure.</span></span> |
| [<span data-ttu-id="85547-119">az group create</span><span class="sxs-lookup"><span data-stu-id="85547-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="85547-120">Crée un groupe de ressources avec un emplacement.</span><span class="sxs-lookup"><span data-stu-id="85547-120">Create a resource group with location</span></span> |
| [<span data-ttu-id="85547-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="85547-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="85547-122">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="85547-122">Create a storage account</span></span> |
| [<span data-ttu-id="85547-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="85547-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="85547-124">Crée une Function App.</span><span class="sxs-lookup"><span data-stu-id="85547-124">Create a new function app</span></span> |
| [<span data-ttu-id="85547-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="85547-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="85547-126">Nettoyer</span><span class="sxs-lookup"><span data-stu-id="85547-126">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="85547-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="85547-127">Next steps</span></span>

<span data-ttu-id="85547-128">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="85547-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="85547-129">Vous trouverez des exemples supplémentaires de script CLI de fonctions Azure Bonjour [documentation Azure fonctions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="85547-129">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
