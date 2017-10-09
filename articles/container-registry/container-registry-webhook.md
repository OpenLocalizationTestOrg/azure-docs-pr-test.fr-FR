---
title: aaaAzure conteneur Registre webhooks | Documents Microsoft
description: Webhooks Azure Container Registry
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: Docker, Conteneurs, ACR
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="b6edb-104">Utilisation des webhooks Azure Container Registry - Portail Azure</span><span class="sxs-lookup"><span data-stu-id="b6edb-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="b6edb-105">Un Registre de conteneur Azure stocke et gère les images de conteneur Docker privés, comme toohello Hub d’ancrage stocke les images Docker publiques.</span><span class="sxs-lookup"><span data-stu-id="b6edb-105">An Azure container registry stores and manages private Docker container images, similar toohello way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="b6edb-106">Vous utilisez des webhooks tootrigger événements lorsque certaines actions sont exécutées dans un des référentiels de votre Registre.</span><span class="sxs-lookup"><span data-stu-id="b6edb-106">You use webhooks tootrigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="b6edb-107">Webhooks peut répondre tooevents au niveau du Registre hello ou elles peuvent être étendues vers le bas de balise du référentiel spécifique tooa.</span><span class="sxs-lookup"><span data-stu-id="b6edb-107">Webhooks can respond tooevents at hello registry level or they can be scoped down tooa specific repository tag.</span></span> 

<span data-ttu-id="b6edb-108">Pour plus d’informations et des concepts, consultez hello [vue d’ensemble](./container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="b6edb-108">For more background and concepts, see hello [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6edb-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b6edb-109">Prerequisites</span></span> 

- <span data-ttu-id="b6edb-110">Registre managé de conteneurs Azure: créez un registre de conteneurs managé dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="b6edb-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="b6edb-111">Par exemple, utilisez hello portail Azure ou hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="b6edb-111">For example, use hello Azure portal or hello Azure CLI 2.0.</span></span> 
- <span data-ttu-id="b6edb-112">Docker CLI - tooset de votre ordinateur local en tant qu’un ordinateur hôte et l’accès hello Docker CLI commandes Docker, installez le moteur Docker.</span><span class="sxs-lookup"><span data-stu-id="b6edb-112">Docker CLI - tooset up your local computer as a Docker host and access hello Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="b6edb-113">Créer un portail Azure webhook</span><span class="sxs-lookup"><span data-stu-id="b6edb-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="b6edb-114">Connectez-vous à toohello portail Azure et accédez de Registre toohello dans lequel vous souhaitez toocreate webhooks.</span><span class="sxs-lookup"><span data-stu-id="b6edb-114">Log in toohello Azure portal and navigate toohello registry in which you want toocreate webhooks.</span></span> 

2. <span data-ttu-id="b6edb-115">Dans le panneau de conteneur hello, sélectionnez l’onglet de « Webhooks » de hello.</span><span class="sxs-lookup"><span data-stu-id="b6edb-115">In hello container blade, select hello "Webhooks" tab.</span></span> 

3. <span data-ttu-id="b6edb-116">Sélectionnez « Ajouter » à partir de la barre d’outils du panneau hello webhook.</span><span class="sxs-lookup"><span data-stu-id="b6edb-116">Select "Add" from hello webhook blade toolbar.</span></span> 

4. <span data-ttu-id="b6edb-117">Hello complète *créer le Webhook* formulaire avec hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6edb-117">Complete hello *Create Webhook* form with hello following information:</span></span>

| <span data-ttu-id="b6edb-118">Valeur</span><span class="sxs-lookup"><span data-stu-id="b6edb-118">Value</span></span> | <span data-ttu-id="b6edb-119">Description</span><span class="sxs-lookup"><span data-stu-id="b6edb-119">Description</span></span> |
|---|---|
| <span data-ttu-id="b6edb-120">Nom</span><span class="sxs-lookup"><span data-stu-id="b6edb-120">Name</span></span> | <span data-ttu-id="b6edb-121">Hello nom toogive toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="b6edb-121">hello name you want toogive toohello webhook.</span></span> <span data-ttu-id="b6edb-122">Il ne peut contenir que des lettres minuscules et des chiffres et avoir de 5 à 50 caractères.</span><span class="sxs-lookup"><span data-stu-id="b6edb-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="b6edb-123">URI de service</span><span class="sxs-lookup"><span data-stu-id="b6edb-123">Service URI</span></span> | <span data-ttu-id="b6edb-124">Hello URI où hello webhook doit envoyer des notifications de publication.</span><span class="sxs-lookup"><span data-stu-id="b6edb-124">hello URI where hello webhook should send POST notifications.</span></span> |
| <span data-ttu-id="b6edb-125">En-têtes personnalisés</span><span class="sxs-lookup"><span data-stu-id="b6edb-125">Custom headers</span></span> | <span data-ttu-id="b6edb-126">En-têtes toopass en même temps que la demande POST de hello.</span><span class="sxs-lookup"><span data-stu-id="b6edb-126">Headers you want toopass along with hello POST request.</span></span> <span data-ttu-id="b6edb-127">Ils doivent être au format « clé : valeur ».</span><span class="sxs-lookup"><span data-stu-id="b6edb-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="b6edb-128">Actions de déclencheur</span><span class="sxs-lookup"><span data-stu-id="b6edb-128">Trigger actions</span></span> | <span data-ttu-id="b6edb-129">Actions qui déclenchent hello webhook.</span><span class="sxs-lookup"><span data-stu-id="b6edb-129">Actions that trigger hello webhook.</span></span> <span data-ttu-id="b6edb-130">Actuellement, webhooks peut être déclenchée par push et/ou supprimer actions tooan image.</span><span class="sxs-lookup"><span data-stu-id="b6edb-130">Currently webhooks can be triggered by push and/or delete actions tooan image.</span></span> |
| <span data-ttu-id="b6edb-131">État</span><span class="sxs-lookup"><span data-stu-id="b6edb-131">Status</span></span> | <span data-ttu-id="b6edb-132">état Hello du webhook hello après sa création.</span><span class="sxs-lookup"><span data-stu-id="b6edb-132">hello status for hello webhook after it's created.</span></span> <span data-ttu-id="b6edb-133">Il est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="b6edb-133">It's enabled by default.</span></span> |
| <span data-ttu-id="b6edb-134">Scope</span><span class="sxs-lookup"><span data-stu-id="b6edb-134">Scope</span></span> | <span data-ttu-id="b6edb-135">étendue Hello qui fonctionne de webhook hello.</span><span class="sxs-lookup"><span data-stu-id="b6edb-135">hello scope at which hello webhook works.</span></span> <span data-ttu-id="b6edb-136">Étendue de hello est par défaut pour tous les événements dans le Registre de hello.</span><span class="sxs-lookup"><span data-stu-id="b6edb-136">By default hello scope is for all events in hello registry.</span></span> <span data-ttu-id="b6edb-137">Il peut être spécifié pour un référentiel ou d’une balise à l’aide du format de hello « référentiel : balise ».</span><span class="sxs-lookup"><span data-stu-id="b6edb-137">It can be specified for a repository or a tag by using hello format "repository: tag".</span></span> |

<span data-ttu-id="b6edb-138">Exemple de formulaire webhook :</span><span class="sxs-lookup"><span data-stu-id="b6edb-138">Example webhook form:</span></span>

![Interface utilisateur DC/OS](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="b6edb-140">Créer un webhook avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b6edb-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="b6edb-141">un webhook à l’aide de toocreate hello CLI d’Azure, utilisez hello [az acr webhook créer](/cli/azure/acr/webhook#create) commande.</span><span class="sxs-lookup"><span data-stu-id="b6edb-141">toocreate a webhook using hello Azure CLI, use hello [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="b6edb-142">Tester un webhook</span><span class="sxs-lookup"><span data-stu-id="b6edb-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="b6edb-143">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="b6edb-143">Azure portal</span></span>

<span data-ttu-id="b6edb-144">Webhook de hello toousing préalable sur le conteneur de l’image par émission de données et supprimer des actions, il peut être testé à l’aide de hello **Ping** bouton.</span><span class="sxs-lookup"><span data-stu-id="b6edb-144">Prior toousing hello webhook on container image push and delete actions, it can be tested using hello **Ping** button.</span></span> <span data-ttu-id="b6edb-145">Lorsqu’il est utilisé, hello Ping envoie qu'un toohello de la demande post générique spécifié de point de terminaison et les journaux de réponse hello.</span><span class="sxs-lookup"><span data-stu-id="b6edb-145">When used, hello Ping sends a generic post request toohello specified endpoint and logs hello response.</span></span> <span data-ttu-id="b6edb-146">Cela s’avère utile tooverify qui hello webhook a été configuré correctement.</span><span class="sxs-lookup"><span data-stu-id="b6edb-146">This is helpful tooverify that hello webhook has been set up correctly.</span></span>

1. <span data-ttu-id="b6edb-147">Sélectionnez webhook hello souhaité tootest.</span><span class="sxs-lookup"><span data-stu-id="b6edb-147">Select hello webhook you want tootest.</span></span> 
2. <span data-ttu-id="b6edb-148">Dans la barre d’outils supérieure hello, sélectionnez l’action de « Ping » de hello.</span><span class="sxs-lookup"><span data-stu-id="b6edb-148">In hello top toolbar, select hello "Ping" action.</span></span> 
3. <span data-ttu-id="b6edb-149">Demande de vérification de hello et de réponse.</span><span class="sxs-lookup"><span data-stu-id="b6edb-149">Check hello request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="b6edb-150">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="b6edb-150">Azure CLI</span></span>

<span data-ttu-id="b6edb-151">tootest un webhook ACR avec hello CLI d’Azure, utilisez hello [ping de webhook az acr](/cli/azure/acr/webhook#ping) commande.</span><span class="sxs-lookup"><span data-stu-id="b6edb-151">tootest an ACR webhook with hello Azure CLI, use hello [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="b6edb-152">résultats de hello toosee, utilisez hello [az acr webhook événements de la liste](/cli/azure/acr/webhook#list-events) commande.</span><span class="sxs-lookup"><span data-stu-id="b6edb-152">toosee hello results, use hello [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="b6edb-153">Supprimer un webhook</span><span class="sxs-lookup"><span data-stu-id="b6edb-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="b6edb-154">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="b6edb-154">Azure portal</span></span>

<span data-ttu-id="b6edb-155">Chaque webhook peut être supprimé en sélectionnant hello webhook, puis le bouton Supprimer hello hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b6edb-155">Each webhook can be deleted by selecting hello webhook and then hello delete button on hello Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="b6edb-156">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="b6edb-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```