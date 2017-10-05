---
title: "Créer une fonction Azure qui se connecte à un Stockage Azure | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer une fonction Azure qui se connecte à un Stockage Azure"
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
ms.openlocfilehash: 36dbc2c181c9991a27163e3194800f63c6c0e01e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="c175f-103">Intégrer Function App à un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="c175f-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="c175f-104">Cet exemple de script crée une Function App et un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c175f-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c175f-105">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0 ou une version ultérieure pour poursuivre la procédure décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="c175f-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c175f-106">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="c175f-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="c175f-107">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c175f-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c175f-108">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="c175f-108">Sample script</span></span>

<span data-ttu-id="c175f-109">Cet exemple crée une Function App Azure et ajoute la chaîne de connexion de stockage à un paramètre d’application.</span><span class="sxs-lookup"><span data-stu-id="c175f-109">This sample creates an Azure Function app and adds the storage connection string to an app setting.</span></span>

<span data-ttu-id="c175f-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Intégrer Function App à un compte de stockage Azure")]</span><span class="sxs-lookup"><span data-stu-id="c175f-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="c175f-111">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="c175f-111">Clean up deployment</span></span>

<span data-ttu-id="c175f-112">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources, l’application App Service et toutes les ressources associées :</span><span class="sxs-lookup"><span data-stu-id="c175f-112">After the script sample has been run, the following command can be used to remove the resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c175f-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="c175f-113">Script explanation</span></span>

<span data-ttu-id="c175f-114">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="c175f-114">This script uses the following commands.</span></span> <span data-ttu-id="c175f-115">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="c175f-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c175f-116">Commande</span><span class="sxs-lookup"><span data-stu-id="c175f-116">Command</span></span> | <span data-ttu-id="c175f-117">Remarques</span><span class="sxs-lookup"><span data-stu-id="c175f-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c175f-118">az login</span><span class="sxs-lookup"><span data-stu-id="c175f-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="c175f-119">Connexion à Azure.</span><span class="sxs-lookup"><span data-stu-id="c175f-119">Login to Azure.</span></span> |
| [<span data-ttu-id="c175f-120">az group create</span><span class="sxs-lookup"><span data-stu-id="c175f-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c175f-121">Crée un groupe de ressources avec un emplacement.</span><span class="sxs-lookup"><span data-stu-id="c175f-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="c175f-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="c175f-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="c175f-123">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c175f-123">Create a storage account</span></span> |
| [<span data-ttu-id="c175f-124">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="c175f-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="c175f-125">Crée une Function App.</span><span class="sxs-lookup"><span data-stu-id="c175f-125">Create a new function app</span></span> |
| [<span data-ttu-id="c175f-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="c175f-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="c175f-127">Nettoyer</span><span class="sxs-lookup"><span data-stu-id="c175f-127">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c175f-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c175f-128">Next steps</span></span>

<span data-ttu-id="c175f-129">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c175f-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c175f-130">Vous trouverez des exemples supplémentaires de scripts CLI Azure Functions dans la [documentation d’Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c175f-130">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
