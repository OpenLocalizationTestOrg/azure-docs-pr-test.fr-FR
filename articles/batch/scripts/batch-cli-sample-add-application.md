---
title: aaaAzure exemple de Script CLI - ajouter une Application de traitement par lots | Documents Microsoft
description: "Exemple de script Azure CLI - Ajout d’une application dans Batch"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a><span data-ttu-id="e99ee-103">Ajout d’applications tooAzure lot avec CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="e99ee-103">Adding applications tooAzure Batch with Azure CLI</span></span>

<span data-ttu-id="e99ee-104">Ce script montre comment tooset d’une application pour une utilisation avec un pool Azure Batch ou une tâche.</span><span class="sxs-lookup"><span data-stu-id="e99ee-104">This script demonstrates how tooset up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="e99ee-105">tooset d’une application, empaqueter votre fichier exécutable, avec toutes ses dépendances, dans un fichier .zip.</span><span class="sxs-lookup"><span data-stu-id="e99ee-105">tooset up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="e99ee-106">Dans ce fichier zip d’exécutable hello exemple fichier est appelé « Mon-application-exe.zip ».</span><span class="sxs-lookup"><span data-stu-id="e99ee-106">In this example hello executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e99ee-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e99ee-107">Prerequisites</span></span>

- <span data-ttu-id="e99ee-108">Installation hello CLI d’Azure à l’aide d’instructions hello de hello [guide d’installation Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), si vous n’avez pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="e99ee-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="e99ee-109">Créez un compte Azure si vous n’en avez pas.</span><span class="sxs-lookup"><span data-stu-id="e99ee-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="e99ee-110">Consultez [créer un compte de traitement par lots avec hello CLI d’Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) pour un exemple de script qui crée un compte.</span><span class="sxs-lookup"><span data-stu-id="e99ee-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="e99ee-111">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="e99ee-111">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a><span data-ttu-id="e99ee-112">Supprimer l’application</span><span class="sxs-lookup"><span data-stu-id="e99ee-112">Clean up application</span></span>

<span data-ttu-id="e99ee-113">Après avoir exécuté hello ci-dessus un exemple de script, exécuter hello suivant tooremove de commandes de l’application et tous ses packages d’application chargés.</span><span class="sxs-lookup"><span data-stu-id="e99ee-113">After you run hello above sample script, run hello following commands tooremove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="e99ee-114">Explication du script</span><span class="sxs-lookup"><span data-stu-id="e99ee-114">Script explanation</span></span>

<span data-ttu-id="e99ee-115">Ce script utilise hello suivant de commandes toocreate une application et le téléchargement d’un package d’application.</span><span class="sxs-lookup"><span data-stu-id="e99ee-115">This script uses hello following commands toocreate an application and upload an application package.</span></span>
<span data-ttu-id="e99ee-116">Chaque commande dans la table de hello lie documentation toocommand spécifique.</span><span class="sxs-lookup"><span data-stu-id="e99ee-116">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="e99ee-117">Commande</span><span class="sxs-lookup"><span data-stu-id="e99ee-117">Command</span></span> | <span data-ttu-id="e99ee-118">Remarques</span><span class="sxs-lookup"><span data-stu-id="e99ee-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e99ee-119">az batch application create</span><span class="sxs-lookup"><span data-stu-id="e99ee-119">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="e99ee-120">Crée une application.</span><span class="sxs-lookup"><span data-stu-id="e99ee-120">Creates an application.</span></span>  |
| [<span data-ttu-id="e99ee-121">az batch application set</span><span class="sxs-lookup"><span data-stu-id="e99ee-121">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="e99ee-122">Met à jour les propriétés d’une application.</span><span class="sxs-lookup"><span data-stu-id="e99ee-122">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="e99ee-123">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="e99ee-123">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="e99ee-124">Ajoute un toohello de package d’application spécifié application.</span><span class="sxs-lookup"><span data-stu-id="e99ee-124">Adds an application package toohello specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="e99ee-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e99ee-125">Next steps</span></span>

<span data-ttu-id="e99ee-126">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e99ee-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e99ee-127">Vous trouverez des exemples supplémentaires de script CLI de lot Bonjour [documentation d’Azure Batch CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e99ee-127">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
