---
title: "référentiels de Registre de conteneur aaaAzure | Documents Microsoft"
description: "Comment toouse les référentiels de Registre de conteneur Azure pour les images de Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="9d170-103">Référentiels Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="9d170-103">Azure container registry repositories</span></span>

<span data-ttu-id="9d170-104">Registre de conteneur Azure vous permet des images de conteneur toostore dans des référentiels.</span><span class="sxs-lookup"><span data-stu-id="9d170-104">Azure container registry allows you toostore container images in repositories.</span></span> <span data-ttu-id="9d170-105">En stockant les images dans des référentiels, vous pouvez créer des groupes d’images (ou une version de ces images) au sein d’environnements isolés.</span><span class="sxs-lookup"><span data-stu-id="9d170-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="9d170-106">Vous pouvez spécifier ces référentiels lorsque vous appuyez sur le Registre de tooyour d’images.</span><span class="sxs-lookup"><span data-stu-id="9d170-106">You can specify these repositories when you push images tooyour registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="9d170-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9d170-107">Prerequisites</span></span>
* <span data-ttu-id="9d170-108">**Azure Container Registry** : créez un Registre de conteneur dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9d170-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="9d170-109">Par exemple, utiliser hello [portail Azure](container-registry-get-started-portal.md) ou hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9d170-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="9d170-110">**Docker CLI** -tooset de votre ordinateur local en tant qu’un ordinateur hôte et l’accès hello Docker CLI commandes Docker, installez [moteur Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="9d170-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="9d170-111">**Extraire une image** - extraire une image à partir du Registre du Hub Docker publique hello marquer et poussez-le tooyour Registre.</span><span class="sxs-lookup"><span data-stu-id="9d170-111">**Pull an image** - Pull an image from hello public Docker Hub registry, tag it, and push it tooyour registry.</span></span> <span data-ttu-id="9d170-112">Pour obtenir des conseils sur la façon de push et pull des images, consultez [Registre privé de Push Docker image tooAzure](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9d170-112">For guidance on how push and pull images, see [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="9d170-113">Affichage des référentiels dans hello portail</span><span class="sxs-lookup"><span data-stu-id="9d170-113">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="9d170-114">Une fois que vous avez envoyée Registre de conteneur tooyour images, vous pouvez voir une liste de référentiels hello images hello Bonjour Azure portal d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="9d170-114">Once you have pushed images tooyour container registry, you can see a list of hello repositories hosting hello images in hello Azure portal.</span></span>

<span data-ttu-id="9d170-115">Si vous avez suivi les étapes de hello Bonjour [Registre privé de Push de Docker image tooAzure](container-registry-get-started-docker-cli.md) article, vous devez maintenant avoir une image Nginx dans le Registre de conteneur.</span><span class="sxs-lookup"><span data-stu-id="9d170-115">If you followed hello steps in hello [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="9d170-116">Dans le cadre d’instructions de hello, vous devez spécifié un espace de noms pour l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="9d170-116">As part of hello instructions, you should have specified a namespace for hello image.</span></span> <span data-ttu-id="9d170-117">Dans l’exemple hello ci-dessous, commande hello pousse le référentiel « exemples » toohello hello NGinx image :</span><span class="sxs-lookup"><span data-stu-id="9d170-117">In hello example below, hello command pushes hello NGinx image toohello "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="9d170-118">Azure Container Registry prend en charge les espaces de noms de référentiel à plusieurs niveaux.</span><span class="sxs-lookup"><span data-stu-id="9d170-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="9d170-119">Cette fonctionnalité permet de vous toogroup collections d’application spécifique d’images tooa connexes, ou une collection de développement de toospecific d’applications ou les équipes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="9d170-119">This feature enables you toogroup collections of images related tooa specific app, or a collection of apps toospecific development or operational teams.</span></span> <span data-ttu-id="9d170-120">tooread en savoir plus sur les référentiels dans les registres de conteneur, consultez [registres de conteneur privé Docker dans Azure](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="9d170-120">tooread more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="9d170-121">référentiels de Registre tooview hello conteneur :</span><span class="sxs-lookup"><span data-stu-id="9d170-121">tooview hello container registry repositories:</span></span>

1. <span data-ttu-id="9d170-122">Ouvrez une session dans toohello portail Azure</span><span class="sxs-lookup"><span data-stu-id="9d170-122">Log in toohello Azure portal</span></span>
2. <span data-ttu-id="9d170-123">Sur hello **Registre de conteneur Azure** panneau, Registre de select hello vous souhaitez tooinspect</span><span class="sxs-lookup"><span data-stu-id="9d170-123">On hello **Azure Container Registry** blade, select hello registry you wish tooinspect</span></span>
3. <span data-ttu-id="9d170-124">Dans le panneau de Registre hello, cliquez sur **référentiels** toosee une liste de tous les référentiels hello et leurs images.</span><span class="sxs-lookup"><span data-stu-id="9d170-124">In hello registry blade, click **Repositories** toosee a list of all hello repositories and their images</span></span>
4. <span data-ttu-id="9d170-125">(Facultatif) Sélectionnez un toosee les balises d’image spécifique</span><span class="sxs-lookup"><span data-stu-id="9d170-125">(Optional) Select a specific image toosee tags</span></span>

![Référentiels dans le portail de hello](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="9d170-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9d170-127">Next steps</span></span>
<span data-ttu-id="9d170-128">Maintenant que vous connaissez les principes de base hello, vous êtes prêt toostart à l’aide de votre Registre !</span><span class="sxs-lookup"><span data-stu-id="9d170-128">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="9d170-129">Par exemple, début du déploiement de conteneur images tooan [Service de conteneur Azure](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span><span class="sxs-lookup"><span data-stu-id="9d170-129">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
