---
title: aaaPush Docker image tooprivate Registre Azure | Documents Microsoft
description: "Push et pull Docker Registre de conteneur privé tooa images dans Azure à l’aide de hello Docker CLI"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a81a6f4bfcb23642a89ac7631348d40e2f4911a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="push-your-first-image-tooa-private-docker-container-registry-using-hello-docker-cli"></a><span data-ttu-id="6728f-103">Push de votre première image tooa privé Docker Registre de conteneur à l’aide de hello Docker CLI</span><span class="sxs-lookup"><span data-stu-id="6728f-103">Push your first image tooa private Docker container registry using hello Docker CLI</span></span>
<span data-ttu-id="6728f-104">Un Registre de conteneur Azure stocke et gère des privé [Docker](http://hub.docker.com) les images de conteneur, toohello similaire moyen [Hub d’ancrage](https://hub.docker.com/) stocke les images Docker publiques.</span><span class="sxs-lookup"><span data-stu-id="6728f-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar toohello way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="6728f-105">Vous utilisez hello [Interface de ligne de commande Docker](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) pour [connexion](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [extraction](https://docs.docker.com/engine/reference/commandline/pull/)et d’autres opérations sur le conteneur Registre.</span><span class="sxs-lookup"><span data-stu-id="6728f-105">You use hello [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="6728f-106">Pour plus d’informations et des concepts, consultez [hello vue d’ensemble](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="6728f-106">For more background and concepts, see [hello overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="6728f-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6728f-107">Prerequisites</span></span>
* <span data-ttu-id="6728f-108">**Azure Container Registry** : créez un Registre de conteneur dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="6728f-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="6728f-109">Par exemple, utiliser hello [portail Azure](container-registry-get-started-portal.md) ou hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6728f-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="6728f-110">**Docker CLI** -tooset de votre ordinateur local en tant qu’un ordinateur hôte et l’accès hello Docker CLI commandes Docker, installez [moteur Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="6728f-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-tooa-registry"></a><span data-ttu-id="6728f-111">Ouvrez une session dans le Registre de tooa</span><span class="sxs-lookup"><span data-stu-id="6728f-111">Log in tooa registry</span></span>
<span data-ttu-id="6728f-112">Exécutez `docker login` toolog dans le Registre de conteneur tooyour avec votre [informations d’identification du Registre](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6728f-112">Run `docker login` toolog in tooyour container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="6728f-113">Hello exemple suivant passe hello ID et mot de passe d’Azure Active Directory [principal du service](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="6728f-113">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="6728f-114">Par exemple, vous avez peut-être affectés un Registre tooyour principal de service pour un scénario d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="6728f-114">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="6728f-115">Rend le nom de Registre complet de hello de que toospecify (tout en minuscules).</span><span class="sxs-lookup"><span data-stu-id="6728f-115">Make sure toospecify hello fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="6728f-116">Dans cet exemple, il s’agit de `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="6728f-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-toopull-and-push-an-image"></a><span data-ttu-id="6728f-117">Étapes toopull et transmettez une image</span><span class="sxs-lookup"><span data-stu-id="6728f-117">Steps toopull and push an image</span></span>
<span data-ttu-id="6728f-118">Hello suivre exemple téléchargements hello image Nginx à partir du Registre du Hub Docker publique hello, balises pour le Registre de votre conteneur Azure privée, il transmet tooyour Registre, puis il extrait à nouveau.</span><span class="sxs-lookup"><span data-stu-id="6728f-118">hello follow example downloads hello Nginx image from hello public Docker Hub registry, tags it for your private Azure container registry, pushes it tooyour registry, then pulls it again.</span></span>

<span data-ttu-id="6728f-119">**1. Extraire l’image officiel du Docker hello pour Nginx**</span><span class="sxs-lookup"><span data-stu-id="6728f-119">**1. Pull hello Docker official image for Nginx**</span></span>

<span data-ttu-id="6728f-120">Première extraction hello publique Nginx image tooyour ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="6728f-120">First pull hello public Nginx image tooyour local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="6728f-121">**2. Démarrez le conteneur de Nginx hello**</span><span class="sxs-lookup"><span data-stu-id="6728f-121">**2. Start hello Nginx container**</span></span>

<span data-ttu-id="6728f-122">Hello commande suivante démarre les conteneur Nginx local hello interactivement sur le port 8080, ce qui permet de sortie de toosee de Nginx.</span><span class="sxs-lookup"><span data-stu-id="6728f-122">hello following command starts hello local Nginx container interactively on port 8080, allowing you toosee output from Nginx.</span></span> <span data-ttu-id="6728f-123">Il supprime hello conteneur une fois arrêté en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6728f-123">It removes hello running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="6728f-124">Parcourir trop[http://localhost : 8080](http://localhost:8080) hello tooview conteneur en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6728f-124">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span> <span data-ttu-id="6728f-125">Vous voyez un toohello similaire écran suivant un.</span><span class="sxs-lookup"><span data-stu-id="6728f-125">You see a screen similar toohello following one.</span></span>

![Nginx sur un ordinateur local](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="6728f-127">toostop hello conteneur en cours d’exécution, appuyez sur [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="6728f-127">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="6728f-128">**3. Créer un alias de l’image de hello dans votre Registre.**</span><span class="sxs-lookup"><span data-stu-id="6728f-128">**3. Create an alias of hello image in your registry**</span></span>

<span data-ttu-id="6728f-129">Hello commande suivante crée un alias de l’image de hello, avec un Registre tooyour de chemin d’accès qualifié complet.</span><span class="sxs-lookup"><span data-stu-id="6728f-129">hello following command creates an alias of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="6728f-130">Cet exemple spécifie hello `samples` encombrement de l’espace de noms tooavoid dans la racine du Registre de hello hello.</span><span class="sxs-lookup"><span data-stu-id="6728f-130">This example specifies hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="6728f-131">**4. Push hello image tooyour Registre**</span><span class="sxs-lookup"><span data-stu-id="6728f-131">**4. Push hello image tooyour registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="6728f-132">**5. Image de hello par extraction de données à partir de votre Registre.**</span><span class="sxs-lookup"><span data-stu-id="6728f-132">**5. Pull hello image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="6728f-133">**6. Démarrer le conteneur de Nginx hello du Registre**</span><span class="sxs-lookup"><span data-stu-id="6728f-133">**6. Start hello Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="6728f-134">Parcourir trop[http://localhost : 8080](http://localhost:8080) hello tooview conteneur en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6728f-134">Browse too[http://localhost:8080](http://localhost:8080) tooview hello running container.</span></span>

<span data-ttu-id="6728f-135">toostop hello conteneur en cours d’exécution, appuyez sur [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="6728f-135">toostop hello running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="6728f-136">**7. (Facultatif) Supprimer une image de hello**</span><span class="sxs-lookup"><span data-stu-id="6728f-136">**7. (Optional) Remove hello image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="6728f-137">Limites simultanées</span><span class="sxs-lookup"><span data-stu-id="6728f-137">Concurrent Limits</span></span>
<span data-ttu-id="6728f-138">Dans certains scénarios, l’exécution des appels simultanément peut générer des erreurs.</span><span class="sxs-lookup"><span data-stu-id="6728f-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="6728f-139">Hello tableau suivant contient les limites de hello d’appels simultanés avec des opérations « Émission » et « Collecte » sur le Registre de conteneur Azure :</span><span class="sxs-lookup"><span data-stu-id="6728f-139">hello following table contains hello limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="6728f-140">Opération</span><span class="sxs-lookup"><span data-stu-id="6728f-140">Operation</span></span>  | <span data-ttu-id="6728f-141">Limite</span><span class="sxs-lookup"><span data-stu-id="6728f-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="6728f-142">PULL</span><span class="sxs-lookup"><span data-stu-id="6728f-142">PULL</span></span>       | <span data-ttu-id="6728f-143">Des too10 simultanées extrait par le Registre</span><span class="sxs-lookup"><span data-stu-id="6728f-143">Up too10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="6728f-144">PUSH</span><span class="sxs-lookup"><span data-stu-id="6728f-144">PUSH</span></span>       | <span data-ttu-id="6728f-145">Des too5 simultanées exécute un push par le Registre</span><span class="sxs-lookup"><span data-stu-id="6728f-145">Up too5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6728f-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6728f-146">Next steps</span></span>
<span data-ttu-id="6728f-147">Maintenant que vous connaissez les principes de base hello, vous êtes prêt toostart à l’aide de votre Registre !</span><span class="sxs-lookup"><span data-stu-id="6728f-147">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="6728f-148">Par exemple, début du déploiement de conteneur images tooan [Service de conteneur Azure](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span><span class="sxs-lookup"><span data-stu-id="6728f-148">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
