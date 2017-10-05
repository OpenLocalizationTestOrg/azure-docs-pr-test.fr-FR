---
title: "Exemple de script Azure CLI - Ajout d’une application dans Batch | Microsoft Docs"
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
ms.openlocfilehash: 5d057eaf32867aedc95d58c5185e2be1f9385ec0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="adding-applications-to-azure-batch-with-azure-cli"></a><span data-ttu-id="612c0-103">Ajout d’applications dans Azure Batch avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="612c0-103">Adding applications to Azure Batch with Azure CLI</span></span>

<span data-ttu-id="612c0-104">Ce script explique comment configurer une application à utiliser avec une tâche ou un pool Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="612c0-104">This script demonstrates how to set up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="612c0-105">Pour configurer cette application, placez votre fichier exécutable et toutes ses éventuelles dépendances dans un fichier .zip.</span><span class="sxs-lookup"><span data-stu-id="612c0-105">To set up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="612c0-106">Dans cet exemple, le fichier .zip est appelé « my-application-exe.zip ».</span><span class="sxs-lookup"><span data-stu-id="612c0-106">In this example the executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="612c0-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="612c0-107">Prerequisites</span></span>

- <span data-ttu-id="612c0-108">Installez Azure CLI en suivant les instructions fournies dans le [Guide d’installation d’Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="612c0-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="612c0-109">Créez un compte Azure si vous n’en avez pas.</span><span class="sxs-lookup"><span data-stu-id="612c0-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="612c0-110">Pour un exemple de script qui crée un compte, voir [Créer un compte Batch avec Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account).</span><span class="sxs-lookup"><span data-stu-id="612c0-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="612c0-111">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="612c0-111">Sample script</span></span>

<span data-ttu-id="612c0-112">[!code-azurecli[principal](../../../cli_scripts/batch/add-application/add-application.sh "Ajouter une application")]</span><span class="sxs-lookup"><span data-stu-id="612c0-112">[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]</span></span>

## <a name="clean-up-application"></a><span data-ttu-id="612c0-113">Supprimer l’application</span><span class="sxs-lookup"><span data-stu-id="612c0-113">Clean up application</span></span>

<span data-ttu-id="612c0-114">Une fois l’exemple de script ci-dessus exécuté, lancez les commandes suivantes pour supprimer l’application et tous les packages associés qui ont été chargés.</span><span class="sxs-lookup"><span data-stu-id="612c0-114">After you run the above sample script, run the following commands to remove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="612c0-115">Explication du script</span><span class="sxs-lookup"><span data-stu-id="612c0-115">Script explanation</span></span>

<span data-ttu-id="612c0-116">Ce script utilise les commandes suivantes pour créer une application et charger un package d’application.</span><span class="sxs-lookup"><span data-stu-id="612c0-116">This script uses the following commands to create an application and upload an application package.</span></span>
<span data-ttu-id="612c0-117">Chaque commande de la table renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="612c0-117">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="612c0-118">Commande</span><span class="sxs-lookup"><span data-stu-id="612c0-118">Command</span></span> | <span data-ttu-id="612c0-119">Remarques</span><span class="sxs-lookup"><span data-stu-id="612c0-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="612c0-120">az batch application create</span><span class="sxs-lookup"><span data-stu-id="612c0-120">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="612c0-121">Crée une application.</span><span class="sxs-lookup"><span data-stu-id="612c0-121">Creates an application.</span></span>  |
| [<span data-ttu-id="612c0-122">az batch application set</span><span class="sxs-lookup"><span data-stu-id="612c0-122">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="612c0-123">Met à jour les propriétés d’une application.</span><span class="sxs-lookup"><span data-stu-id="612c0-123">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="612c0-124">az batch application package create</span><span class="sxs-lookup"><span data-stu-id="612c0-124">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="612c0-125">Ajoute un package d’application à l’application spécifiée.</span><span class="sxs-lookup"><span data-stu-id="612c0-125">Adds an application package to the specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="612c0-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="612c0-126">Next steps</span></span>

<span data-ttu-id="612c0-127">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="612c0-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="612c0-128">Vous trouverez des exemples supplémentaires de scripts CLI Batch dans la [documentation relative à la CLI Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="612c0-128">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
