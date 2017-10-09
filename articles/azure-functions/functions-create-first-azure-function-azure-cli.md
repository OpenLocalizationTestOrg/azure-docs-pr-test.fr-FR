---
title: "aaaCreate votre première fonction à partir de hello CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toocreate votre première Azure de fonction pour l’utilisation de l’exécution sans serveur hello CLI d’Azure."
services: functions
keywords: 
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 08/22/2017
ms.topic: hero-article
ms.service: functions
ms.custom: mvc
ms.devlang: azure-cli
manager: erikre
ms.openlocfilehash: 5feed0045d4998b88b0e1bb50996cb7bb42b0822
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-hello-azure-cli"></a><span data-ttu-id="87f91-103">Créer votre première fonction à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="87f91-103">Create your first function using hello Azure CLI</span></span>

<span data-ttu-id="87f91-104">Ce didacticiel de démarrage rapide décrit en détail le toouse Azure fonctions toocreate votre première fonction.</span><span class="sxs-lookup"><span data-stu-id="87f91-104">This quickstart tutorial walks through how toouse Azure Functions toocreate your first function.</span></span> <span data-ttu-id="87f91-105">Vous utilisez hello CLI d’Azure toocreate une application de fonction qui est hello sans infrastructure qui héberge votre fonction.</span><span class="sxs-lookup"><span data-stu-id="87f91-105">You use hello Azure CLI toocreate a function app, which is hello serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="87f91-106">code de fonction Hello lui-même est déployée à partir d’un dépôt d’exemples GitHub.</span><span class="sxs-lookup"><span data-stu-id="87f91-106">hello function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="87f91-107">Vous pouvez suivre les étapes de hello ci-dessous à l’aide d’un ordinateur Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="87f91-107">You can follow hello steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="87f91-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="87f91-108">Prerequisites</span></span> 

<span data-ttu-id="87f91-109">Avant d’exécuter cet exemple, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="87f91-109">Before running this sample, you must have hello following:</span></span>

+ <span data-ttu-id="87f91-110">Un compte [GitHub](https://github.com) actif.</span><span class="sxs-lookup"><span data-stu-id="87f91-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="87f91-111">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="87f91-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="87f91-112">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, cette rubrique requiert que vous exécutez hello CLI d’Azure version 2.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="87f91-112">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="87f91-113">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="87f91-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="87f91-114">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="87f91-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="87f91-115">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="87f91-115">Create a resource group</span></span>

<span data-ttu-id="87f91-116">Créer un groupe de ressources avec hello [az groupe créer](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="87f91-116">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="87f91-117">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure comme les Function Apps, les bases de données et les comptes de stockage sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="87f91-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="87f91-118">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="87f91-118">hello following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="87f91-119">Si vous n’utilisez pas Cloud Shell, vous devez d’abord vous connecter à l’aide de `az login`.</span><span class="sxs-lookup"><span data-stu-id="87f91-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="87f91-120">Création d'un compte Azure Storage</span><span class="sxs-lookup"><span data-stu-id="87f91-120">Create an Azure Storage account</span></span>

<span data-ttu-id="87f91-121">Fonctions utilise un état de toomaintain de compte de stockage Azure et d’autres informations sur vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="87f91-121">Functions uses an Azure Storage account toomaintain state and other information about your functions.</span></span> <span data-ttu-id="87f91-122">Créer un compte de stockage dans le groupe de ressources hello vous avez créé à l’aide de hello [créer de compte de stockage az](/cli/azure/storage/account#create) commande.</span><span class="sxs-lookup"><span data-stu-id="87f91-122">Create a storage account in hello resource group you created by using hello [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="87f91-123">Bonjour suivant de commande, remplacez par votre propre nom de compte de stockage global unique dans lequel vous consultez hello `<storage_name>` espace réservé.</span><span class="sxs-lookup"><span data-stu-id="87f91-123">In hello following command, substitute your own globally unique storage account name where you see hello `<storage_name>` placeholder.</span></span> <span data-ttu-id="87f91-124">Les noms des comptes de stockage doivent comporter entre 3 et 24 caractères, uniquement des lettres minuscules et des chiffres.</span><span class="sxs-lookup"><span data-stu-id="87f91-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="87f91-125">Après avoir créé le compte de stockage hello, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="87f91-125">After hello storage account has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "creationTime": "2017-04-15T17:14:39.320307+00:00",
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myresourcegroup/...",
  "kind": "Storage",
  "location": "westeurope",
  "name": "myfunctionappstorage",
  "primaryEndpoints": {
    "blob": "https://myfunctionappstorage.blob.core.windows.net/",
    "file": "https://myfunctionappstorage.file.core.windows.net/",
    "queue": "https://myfunctionappstorage.queue.core.windows.net/",
    "table": "https://myfunctionappstorage.table.core.windows.net/"
  },
     ....
    // Remaining output has been truncated for readability.
}
```

## <a name="create-a-function-app"></a><span data-ttu-id="87f91-126">Créer une Function App</span><span class="sxs-lookup"><span data-stu-id="87f91-126">Create a function app</span></span>

<span data-ttu-id="87f91-127">Vous devez disposer d’une application toohost hello exécution d’une fonction de vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="87f91-127">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="87f91-128">application de fonction Hello fournit un environnement d’exécution sans serveur de votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="87f91-128">hello function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="87f91-129">Elle vous permet de regrouper les fonctions en une unité logique pour faciliter la gestion, le déploiement et le partage des ressources.</span><span class="sxs-lookup"><span data-stu-id="87f91-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="87f91-130">Créer une application de la fonction à l’aide de hello [az functionapp créer](/cli/azure/functionapp#create) commande.</span><span class="sxs-lookup"><span data-stu-id="87f91-130">Create a function app by using hello [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="87f91-131">Bonjour suivant de commande, remplacez par votre propre nom de l’application une fonction unique dans lequel vous consultez hello `<app_name>` espace réservé et hello nom de compte de stockage pour `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="87f91-131">In hello following command, substitute your own unique function app name where you see hello `<app_name>` placeholder and hello storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="87f91-132">Hello `<app_name>` est utilisé comme domaine DNS par défaut hello pour application de fonction hello et c’est le cas hello nom doit toobe unique entre toutes les applications dans Azure.</span><span class="sxs-lookup"><span data-stu-id="87f91-132">hello `<app_name>` is used as hello default DNS domain for hello function app, and so hello name needs toobe unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="87f91-133">Par défaut, une application de la fonction est créée avec hello consommation plan d’hébergement, ce qui signifie que les ressources sont ajoutées dynamiquement comme requis par vos fonctions et que vous payez uniquement lors de l’exécutant des fonctions.</span><span class="sxs-lookup"><span data-stu-id="87f91-133">By default, a function app is created with hello Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="87f91-134">Pour plus d’informations, consultez [plan d’hébergement approprié choisir hello](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="87f91-134">For more information, see [Choose hello correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="87f91-135">Après que application de fonction hello a été créée, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="87f91-135">After hello function app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

<span data-ttu-id="87f91-136">Maintenant que vous avez une application de la fonction, vous pouvez déployer le code de fonction réelle hello de dépôt d’exemples hello GitHub.</span><span class="sxs-lookup"><span data-stu-id="87f91-136">Now that you have a function app, you can deploy hello actual function code from hello GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="87f91-137">Déployer votre code de fonction</span><span class="sxs-lookup"><span data-stu-id="87f91-137">Deploy your function code</span></span>  

<span data-ttu-id="87f91-138">Il existe plusieurs façons toocreate votre code de fonction dans votre nouvelle application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="87f91-138">There are several ways toocreate your function code in your new function app.</span></span> <span data-ttu-id="87f91-139">Cette rubrique connecte dépôt d’exemples tooa dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="87f91-139">This topic connects tooa sample repository in GitHub.</span></span> <span data-ttu-id="87f91-140">Comme avant, Bonjour suivant code remplacer hello `<app_name>` espace réservé nommé hello d’application de fonction hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="87f91-140">As before, in hello following code replace hello `<app_name>` placeholder with hello name of hello function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="87f91-141">Après le déploiement de hello source été définie, hello CLI d’Azure affiche des informations toohello similaire (les valeurs null sont supprimées pour une meilleure lisibilité) de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="87f91-141">After hello deployment source been set, hello Azure CLI shows information similar toohello following example (null values removed for readability):</span></span>

```json
{
  "branch": "master",
  "deploymentRollbackEnabled": false,
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myResourceGroup/...",
  "isManualIntegration": true,
  "isMercurial": false,
  "location": "West Europe",
  "name": "quickstart",
  "repoUrl": "https://github.com/Azure-Samples/functions-quickstart",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.Web/sites/sourcecontrols"
}
```

## <a name="test-hello-function"></a><span data-ttu-id="87f91-142">Fonction hello de test</span><span class="sxs-lookup"><span data-stu-id="87f91-142">Test hello function</span></span>

<span data-ttu-id="87f91-143">Utiliser cURL tootest hello déployé sur un ordinateur Mac ou Linux ou à l’aide d’un interpréteur de commandes sous Windows.</span><span class="sxs-lookup"><span data-stu-id="87f91-143">Use cURL tootest hello deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="87f91-144">Exécutez hello cURL commande, en remplaçant hello suivante `<app_name>` espace réservé nommé hello de votre application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="87f91-144">Execute hello following cURL command, replacing hello `<app_name>` placeholder with hello name of your function app.</span></span> <span data-ttu-id="87f91-145">Ajouter la chaîne de requête hello `&name=<yourname>` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="87f91-145">Append hello query string `&name=<yourname>` toohello URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Réponse de la fonction affichée dans un navigateur.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="87f91-147">Si vous n’avez pas cURL disponible dans votre ligne de commande, entrez hello même URL dans la zone Adresse hello de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="87f91-147">If you don't have cURL available in your command line, enter hello same URL in hello address of your web browser.</span></span> <span data-ttu-id="87f91-148">Là encore, remplacez hello `<app_name>` espace réservé nommé hello de votre application de la fonction et ajoute la chaîne de requête hello `&name=<yourname>` toohello URL et l’exécution de la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="87f91-148">Again, replace hello `<app_name>` placeholder with hello name of your function app, and append hello query string `&name=<yourname>` toohello URL and execute hello request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Réponse de la fonction affichée dans un navigateur.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="87f91-150">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="87f91-150">Clean up resources</span></span>

<span data-ttu-id="87f91-151">Les autres démarrages rapides de cette collection reposent sur ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="87f91-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="87f91-152">Si vous prévoyez toocontinue sur toowork Démarrages rapides suivants ou avec des didacticiels de hello, procédez de nettoyer les ressources hello créées dans ce démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="87f91-152">If you plan toocontinue on toowork with subsequent quickstarts or with hello tutorials, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="87f91-153">Si vous n’envisagez pas de toocontinue, utilisez hello suivant commande toodelete toutes les ressources créées par ce démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="87f91-153">If you do not plan toocontinue, use hello following command toodelete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="87f91-154">Quand vous y êtes invité, tapez `y`.</span><span class="sxs-lookup"><span data-stu-id="87f91-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87f91-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="87f91-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
