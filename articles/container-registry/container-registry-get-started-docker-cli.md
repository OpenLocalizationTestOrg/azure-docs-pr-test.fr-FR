---
title: "Transmission push de l’image Docker au Registre Azure privé | Microsoft Docs"
description: "Transmission et extraction des images Docker à un Registre de conteneur privé dans Azure à l’aide de l’interface de ligne de commande (CLI) Docker"
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
ms.openlocfilehash: 07d4d72e94eda02e8594dfddb0e911eb0e63012d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="push-your-first-image-to-a-private-docker-container-registry-using-the-docker-cli"></a><span data-ttu-id="10608-103">Transmission de votre première image vers un Registre de conteneur Docker privé à l’aide de l’interface de ligne de commande (CLI) Docker</span><span class="sxs-lookup"><span data-stu-id="10608-103">Push your first image to a private Docker container registry using the Docker CLI</span></span>
<span data-ttu-id="10608-104">Un Registre de conteneur Azure stocke et gère les images privées du conteneur [Docker](http://hub.docker.com), de la même manière que [Docker Hub](https://hub.docker.com/) stocke les images publiques du Docker.</span><span class="sxs-lookup"><span data-stu-id="10608-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar to the way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="10608-105">Vous pouvez utiliser [l’interface de ligne de commande Docker](https://docs.docker.com/engine/reference/commandline/cli/) (interface CLI Docker) pour la [connexion](https://docs.docker.com/engine/reference/commandline/login/), la [transmission](https://docs.docker.com/engine/reference/commandline/push/), [l’extraction](https://docs.docker.com/engine/reference/commandline/pull/) et d’autres opérations sur le Registre du conteneur.</span><span class="sxs-lookup"><span data-stu-id="10608-105">You use the [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="10608-106">Pour plus d’informations, notamment sur les concepts, voir la [page de présentation](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="10608-106">For more background and concepts, see [the overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="10608-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="10608-107">Prerequisites</span></span>
* <span data-ttu-id="10608-108">**Azure Container Registry** : créez un Registre de conteneur dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="10608-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="10608-109">Par exemple, utilisez le [portail Azure](container-registry-get-started-portal.md) ou [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="10608-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="10608-110">**Interface CLI Docker** : configurez votre ordinateur local comme un hôte Docker et accédez aux commandes de l’interface CLI Docker, installez le [moteur Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="10608-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-to-a-registry"></a><span data-ttu-id="10608-111">Se connecter à un Registre</span><span class="sxs-lookup"><span data-stu-id="10608-111">Log in to a registry</span></span>
<span data-ttu-id="10608-112">Exécutez `docker login` pour vous connecter à votre Registre de conteneur à l’aide de vos [informations d’identification du Registre](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="10608-112">Run `docker login` to log in to your container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="10608-113">L’exemple suivant transmet l’ID et le mot de passe d’un [principal du service](../active-directory/active-directory-application-objects.md) Azure Active Directory .</span><span class="sxs-lookup"><span data-stu-id="10608-113">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="10608-114">Par exemple, vous pouvez avoir affecté un principal du service à votre Registre pour un scénario d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="10608-114">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="10608-115">Veillez à spécifier le nom de Registre qualifié complet (en minuscules).</span><span class="sxs-lookup"><span data-stu-id="10608-115">Make sure to specify the fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="10608-116">Dans cet exemple, il s’agit de `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="10608-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-to-pull-and-push-an-image"></a><span data-ttu-id="10608-117">Étapes d’extraction et de transmission d’une image</span><span class="sxs-lookup"><span data-stu-id="10608-117">Steps to pull and push an image</span></span>
<span data-ttu-id="10608-118">L’exemple suivant télécharge l’image Nginx à partir du Registre Docker Hub public, la balise pour votre Registre de conteneur Azure privé, la transmet à votre Registre, puis l’extrait à nouveau.</span><span class="sxs-lookup"><span data-stu-id="10608-118">The follow example downloads the Nginx image from the public Docker Hub registry, tags it for your private Azure container registry, pushes it to your registry, then pulls it again.</span></span>

<span data-ttu-id="10608-119">**1. Extraire l’image officielle de Docker pour Nginx**</span><span class="sxs-lookup"><span data-stu-id="10608-119">**1. Pull the Docker official image for Nginx**</span></span>

<span data-ttu-id="10608-120">Tout d’abord, extrayez l’image Nginx publique de votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="10608-120">First pull the public Nginx image to your local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="10608-121">**2. Démarrer le conteneur Nginx**</span><span class="sxs-lookup"><span data-stu-id="10608-121">**2. Start the Nginx container**</span></span>

<span data-ttu-id="10608-122">La commande suivante démarre le conteneur Nginx local interactivement sur le port 8080, ce qui vous permet de voir le résultat depuis Nginx.</span><span class="sxs-lookup"><span data-stu-id="10608-122">The following command starts the local Nginx container interactively on port 8080, allowing you to see output from Nginx.</span></span> <span data-ttu-id="10608-123">Il supprime le conteneur en cours d’exécution une fois arrêté.</span><span class="sxs-lookup"><span data-stu-id="10608-123">It removes the running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="10608-124">Accédez à [http://localhost : 8080](http://localhost:8080) pour afficher le conteneur en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="10608-124">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span> <span data-ttu-id="10608-125">Vous voyez un écran semblable au suivant.</span><span class="sxs-lookup"><span data-stu-id="10608-125">You see a screen similar to the following one.</span></span>

![Nginx sur un ordinateur local](./media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="10608-127">Pour arrêter le conteneur en cours d’exécution, appuyez sur [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="10608-127">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="10608-128">**3. Créer un alias de l’image dans votre Registre**</span><span class="sxs-lookup"><span data-stu-id="10608-128">**3. Create an alias of the image in your registry**</span></span>

<span data-ttu-id="10608-129">La commande suivante crée un alias de l’image, avec un chemin d’accès qualifié complet à votre Registre.</span><span class="sxs-lookup"><span data-stu-id="10608-129">The following command creates an alias of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="10608-130">Cet exemple spécifie l’espace de noms `samples` pour éviter l’encombrement à la racine du Registre.</span><span class="sxs-lookup"><span data-stu-id="10608-130">This example specifies the `samples` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="10608-131">**4. Envoyer l’image vers votre Registre**</span><span class="sxs-lookup"><span data-stu-id="10608-131">**4. Push the image to your registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="10608-132">**5. Extraire l’image de votre Registre**</span><span class="sxs-lookup"><span data-stu-id="10608-132">**5. Pull the image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="10608-133">**6. Démarrer le conteneur Nginx à partir de votre Registre**</span><span class="sxs-lookup"><span data-stu-id="10608-133">**6. Start the Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="10608-134">Accédez à [http://localhost : 8080](http://localhost:8080) pour afficher le conteneur en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="10608-134">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span>

<span data-ttu-id="10608-135">Pour arrêter le conteneur en cours d’exécution, appuyez sur [CTRL] + [C].</span><span class="sxs-lookup"><span data-stu-id="10608-135">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="10608-136">**7. (Facultatif) Retirer l’image**</span><span class="sxs-lookup"><span data-stu-id="10608-136">**7. (Optional) Remove the image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="10608-137">Limites simultanées</span><span class="sxs-lookup"><span data-stu-id="10608-137">Concurrent Limits</span></span>
<span data-ttu-id="10608-138">Dans certains scénarios, l’exécution des appels simultanément peut générer des erreurs.</span><span class="sxs-lookup"><span data-stu-id="10608-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="10608-139">Le tableau suivant contient les limites des appels simultanés avec des opérations « Push » et « Pull » sur le Registre de conteneur Azure :</span><span class="sxs-lookup"><span data-stu-id="10608-139">The following table contains the limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="10608-140">Opération</span><span class="sxs-lookup"><span data-stu-id="10608-140">Operation</span></span>  | <span data-ttu-id="10608-141">Limite</span><span class="sxs-lookup"><span data-stu-id="10608-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="10608-142">PULL</span><span class="sxs-lookup"><span data-stu-id="10608-142">PULL</span></span>       | <span data-ttu-id="10608-143">Jusqu’à 10 opérations Pull simultanées par Registre</span><span class="sxs-lookup"><span data-stu-id="10608-143">Up to 10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="10608-144">PUSH</span><span class="sxs-lookup"><span data-stu-id="10608-144">PUSH</span></span>       | <span data-ttu-id="10608-145">Jusqu’à 5 opérations Push simultanées par Registre</span><span class="sxs-lookup"><span data-stu-id="10608-145">Up to 5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="10608-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="10608-146">Next steps</span></span>
<span data-ttu-id="10608-147">Maintenant que vous connaissez les principes de base, vous êtes prêt à utiliser votre Registre.</span><span class="sxs-lookup"><span data-stu-id="10608-147">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="10608-148">Par exemple, commencez à déployer les images du conteneur vers un cluster [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/).</span><span class="sxs-lookup"><span data-stu-id="10608-148">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
