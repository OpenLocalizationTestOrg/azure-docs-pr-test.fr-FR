---
title: "aaaAzure exemple de Script CLI - créez un compte Batch | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer un compte Batch"
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a><span data-ttu-id="6337d-103">Créer un compte de traitement par lots avec hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="6337d-103">Create a Batch account with hello Azure CLI</span></span>

<span data-ttu-id="6337d-104">Ce script crée un compte Azure Batch et montre comment différentes propriétés du compte de hello peuvent être interrogées et mis à jour.</span><span class="sxs-lookup"><span data-stu-id="6337d-104">This script creates an Azure Batch account and shows how various properties of hello account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6337d-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6337d-105">Prerequisites</span></span>

<span data-ttu-id="6337d-106">Installation hello CLI d’Azure à l’aide d’instructions hello de hello [guide d’installation Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), si vous n’avez pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="6337d-106">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="6337d-107">Exemple de script de compte Batch</span><span class="sxs-lookup"><span data-stu-id="6337d-107">Batch account sample script</span></span>

<span data-ttu-id="6337d-108">Lorsque vous créez un compte de traitement par lots, par défaut ses nœuds de calcul sont attribuées en interne par hello service Batch.</span><span class="sxs-lookup"><span data-stu-id="6337d-108">When you create a Batch account, by default its compute nodes are assigned internally by hello Batch service.</span></span> <span data-ttu-id="6337d-109">Nœuds de calcul alloué sera le quota de sujet tooa distinct et compte de hello peut être authentifié via les informations d’identification de clé partagée ou un jeton de répertoire Active de Azure.</span><span class="sxs-lookup"><span data-stu-id="6337d-109">Allocated compute nodes will be subject tooa separate core quota and hello account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="6337d-110">Compte Batch utilisant un exemple de script d’abonnement</span><span class="sxs-lookup"><span data-stu-id="6337d-110">Batch account using user subscription sample script</span></span>

<span data-ttu-id="6337d-111">Vous pouvez également choisir de toohave lot créer ses nœuds de calcul dans votre propre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6337d-111">You can also opt toohave Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="6337d-112">Comptes qui allouent de calcul nœuds à votre abonnement doivent être authentifiées via un jeton d’Azure Active Directory et les nœuds de calcul hello alloués seront comptabilisée dans le quota de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="6337d-112">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and hello compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="6337d-113">toocreate un compte dans ce mode, un doit spécifier une référence de coffre de clés lors de la création du compte de hello.</span><span class="sxs-lookup"><span data-stu-id="6337d-113">toocreate an account in this mode, one must specify a Key Vault reference when creating hello account.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6337d-114">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="6337d-114">Clean up deployment</span></span>

<span data-ttu-id="6337d-115">Une fois que vous exécutez Hello au-dessus des exemples de scripts, exécutez hello suivant commande tooremove le groupe de ressources et toutes les ressources (y compris les comptes de lots, comptes de stockage Azure et les coffres de clés Azure).</span><span class="sxs-lookup"><span data-stu-id="6337d-115">After you run either of hello above sample scripts, run hello following command tooremove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6337d-116">Explication du script</span><span class="sxs-lookup"><span data-stu-id="6337d-116">Script explanation</span></span>

<span data-ttu-id="6337d-117">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, du compte Batch et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="6337d-117">This script uses hello following commands toocreate a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="6337d-118">Chaque commande dans la table de hello lie documentation toocommand spécifique.</span><span class="sxs-lookup"><span data-stu-id="6337d-118">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="6337d-119">Commande</span><span class="sxs-lookup"><span data-stu-id="6337d-119">Command</span></span> | <span data-ttu-id="6337d-120">Remarques</span><span class="sxs-lookup"><span data-stu-id="6337d-120">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6337d-121">az group create</span><span class="sxs-lookup"><span data-stu-id="6337d-121">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6337d-122">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="6337d-122">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6337d-123">az batch account create</span><span class="sxs-lookup"><span data-stu-id="6337d-123">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="6337d-124">Crée un compte de traitement par lots hello.</span><span class="sxs-lookup"><span data-stu-id="6337d-124">Creates hello Batch account.</span></span>  |
| [<span data-ttu-id="6337d-125">az batch account set</span><span class="sxs-lookup"><span data-stu-id="6337d-125">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="6337d-126">Met à jour les propriétés de hello compte Batch.</span><span class="sxs-lookup"><span data-stu-id="6337d-126">Updates properties of hello Batch account.</span></span>  |
| [<span data-ttu-id="6337d-127">az batch account show</span><span class="sxs-lookup"><span data-stu-id="6337d-127">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="6337d-128">Récupère les détails de hello spécifié du compte Batch.</span><span class="sxs-lookup"><span data-stu-id="6337d-128">Retrieves details of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="6337d-129">az batch account keys list</span><span class="sxs-lookup"><span data-stu-id="6337d-129">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="6337d-130">Récupère les clés d’accès hello Hello spécifié du compte Batch.</span><span class="sxs-lookup"><span data-stu-id="6337d-130">Retrieves hello access keys of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="6337d-131">az batch account login</span><span class="sxs-lookup"><span data-stu-id="6337d-131">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="6337d-132">S’authentifie avec hello spécifié pour l’interaction de CLI davantage le compte Batch.</span><span class="sxs-lookup"><span data-stu-id="6337d-132">Authenticates against hello specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="6337d-133">az storage account create</span><span class="sxs-lookup"><span data-stu-id="6337d-133">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="6337d-134">Crée un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6337d-134">Creates a storage account.</span></span> |
| [<span data-ttu-id="6337d-135">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="6337d-135">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="6337d-136">Crée un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="6337d-136">Creates a key vault.</span></span> |
| [<span data-ttu-id="6337d-137">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="6337d-137">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="6337d-138">Mettre à jour la stratégie de sécurité hello de coffre de clés spécifié hello.</span><span class="sxs-lookup"><span data-stu-id="6337d-138">Update hello security policy of hello specified key vault.</span></span> |
| [<span data-ttu-id="6337d-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="6337d-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="6337d-140">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="6337d-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6337d-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6337d-141">Next steps</span></span>

<span data-ttu-id="6337d-142">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6337d-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6337d-143">Vous trouverez des exemples supplémentaires de script CLI de lot Bonjour [documentation d’Azure Batch CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6337d-143">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
