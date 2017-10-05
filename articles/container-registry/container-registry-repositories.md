---
title: "Créer des référentiels Azure Container Registry | Microsoft Docs"
description: "Utiliser des référentiels Azure Container Registry pour gérer des images Docker"
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
ms.openlocfilehash: 06b809c31cecef1714f60d04657eb74c611be8cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="7ecd1-103">Référentiels Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="7ecd1-103">Azure container registry repositories</span></span>

<span data-ttu-id="7ecd1-104">Un référentiel Azure Container Registry vous permet de stocker des images de conteneur.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-104">Azure container registry allows you to store container images in repositories.</span></span> <span data-ttu-id="7ecd1-105">En stockant les images dans des référentiels, vous pouvez créer des groupes d’images (ou une version de ces images) au sein d’environnements isolés.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="7ecd1-106">Vous pouvez spécifier ces référentiels lorsque vous envoyez des images à votre Registre via une transmission de type push.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-106">You can specify these repositories when you push images to your registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7ecd1-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7ecd1-107">Prerequisites</span></span>
* <span data-ttu-id="7ecd1-108">**Azure Container Registry** : créez un Registre de conteneur dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="7ecd1-109">Par exemple, utilisez le [portail Azure](container-registry-get-started-portal.md) ou [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7ecd1-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="7ecd1-110">**Interface CLI Docker** : configurez votre ordinateur local comme un hôte Docker et accédez aux commandes de l’interface CLI Docker, installez le [moteur Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="7ecd1-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="7ecd1-111">**Extraire une image** : extrayez une image à partir du Registre Docker Hub public, marquez-la et envoyez-la à votre Registre via une transmission de type push.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-111">**Pull an image** - Pull an image from the public Docker Hub registry, tag it, and push it to your registry.</span></span> <span data-ttu-id="7ecd1-112">Pour savoir comment envoyer des images via une transmission de type push et en extraire, voir [Transmission de votre première image vers un Registre de conteneur Docker privé à l’aide de l’interface de ligne de commande (CLI) Docker](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7ecd1-112">For guidance on how push and pull images, see [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="7ecd1-113">Affichage de référentiels dans le portail</span><span class="sxs-lookup"><span data-stu-id="7ecd1-113">Viewing repositories in the Portal</span></span>

<span data-ttu-id="7ecd1-114">Une fois que vous avez envoyé des images à votre Registre de conteneur via une transmission de type push, vous pouvez voir une liste des référentiels hébergeant les images dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-114">Once you have pushed images to your container registry, you can see a list of the repositories hosting the images in the Azure portal.</span></span>

<span data-ttu-id="7ecd1-115">Si vous avez suivi les étapes de l’article [Transmission de votre première image vers un Registre de conteneur Docker privé à l’aide de l’interface de ligne de commande (CLI) Docker](container-registry-get-started-docker-cli.md), vous devez maintenant voir apparaître une image Nginx dans le Registre de conteneur.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-115">If you followed the steps in the [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="7ecd1-116">Dans le cadre des instructions, vous avez dû spécifier un espace de noms pour l’image.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-116">As part of the instructions, you should have specified a namespace for the image.</span></span> <span data-ttu-id="7ecd1-117">Dans l’exemple ci-dessous, la commande envoie l’image Nginx via une transmission de type push, vers le référentiel « Samples » :</span><span class="sxs-lookup"><span data-stu-id="7ecd1-117">In the example below, the command pushes the NGinx image to the "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="7ecd1-118">Azure Container Registry prend en charge les espaces de noms de référentiel à plusieurs niveaux.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="7ecd1-119">Cette fonctionnalité vous permet de regrouper des collections d’images liées à une application spécifique, ou une collection d’applications à des équipes opérationnelles ou de développement spécifiques.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-119">This feature enables you to group collections of images related to a specific app, or a collection of apps to specific development or operational teams.</span></span> <span data-ttu-id="7ecd1-120">Pour en savoir plus sur les référentiels des Registres de conteneur, voir [Présentation des registres de conteneurs Docker privés](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="7ecd1-120">To read more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="7ecd1-121">Pour afficher les référentiels Azure Container Registry, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7ecd1-121">To view the container registry repositories:</span></span>

1. <span data-ttu-id="7ecd1-122">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-122">Log in to the Azure portal</span></span>
2. <span data-ttu-id="7ecd1-123">Sur le panneau **Azure Container Registry**, sélectionnez le Registre que vous souhaitez analyser.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-123">On the **Azure Container Registry** blade, select the registry you wish to inspect</span></span>
3. <span data-ttu-id="7ecd1-124">Sur le panneau de ce Registre, cliquez sur **Référentiels** pour afficher la liste de tous les référentiels et de leurs images.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-124">In the registry blade, click **Repositories** to see a list of all the repositories and their images</span></span>
4. <span data-ttu-id="7ecd1-125">(Facultatif) Sélectionnez une image spécifique pour afficher les balises.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-125">(Optional) Select a specific image to see tags</span></span>

![Affichage de référentiels dans le portail](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="7ecd1-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7ecd1-127">Next steps</span></span>
<span data-ttu-id="7ecd1-128">Maintenant que vous connaissez les principes de base, vous êtes prêt à utiliser votre Registre.</span><span class="sxs-lookup"><span data-stu-id="7ecd1-128">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="7ecd1-129">Par exemple, commencez à déployer les images du conteneur vers un cluster [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/).</span><span class="sxs-lookup"><span data-stu-id="7ecd1-129">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
