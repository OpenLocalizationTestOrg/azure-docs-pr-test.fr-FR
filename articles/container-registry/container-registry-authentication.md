---
title: Authentification avec un Registre de conteneurs Azure | Microsoft Docs
description: "Connexion à un Registre de conteneurs Azure à l’aide d’un compte d’administrateur ou d’un principal du service Azure Active Directory"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: aa2a6bf3d7d9ec22020036851fc0f2bca37e31bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="ba375-103">S’authentifier avec un registre de conteneurs Docker</span><span class="sxs-lookup"><span data-stu-id="ba375-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="ba375-104">Pour utiliser des images de conteneur dans un Registre de conteneurs Azure, vous vous connectez à l’aide de la commande `docker login`.</span><span class="sxs-lookup"><span data-stu-id="ba375-104">To work with container images in an Azure container registry, you log in using the `docker login` command.</span></span> <span data-ttu-id="ba375-105">Vous pouvez vous connecter en utilisant un **[principal du service Azure Active Directory](../active-directory/active-directory-application-objects.md)** ou un **compte d’administrateur** spécifique à un registre.</span><span class="sxs-lookup"><span data-stu-id="ba375-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="ba375-106">Cet article fournit des détails sur ces identités.</span><span class="sxs-lookup"><span data-stu-id="ba375-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="ba375-107">Principal du service</span><span class="sxs-lookup"><span data-stu-id="ba375-107">Service principal</span></span>

<span data-ttu-id="ba375-108">Vous pouvez [affecter un principal du service](container-registry-get-started-azure-cli.md#assign-a-service-principal) à votre registre et l’utiliser pour l’authentification Docker de base.</span><span class="sxs-lookup"><span data-stu-id="ba375-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) to your registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="ba375-109">L’utilisation d’un principal du service est recommandée dans la plupart des scénarios.</span><span class="sxs-lookup"><span data-stu-id="ba375-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="ba375-110">Fournissez le mot de passe et l’ID d’application du principal du service à la commande `docker login`, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ba375-110">Provide the app ID and password of the service principal to the `docker login` command, as shown in the following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="ba375-111">Une fois que vous êtes connecté, Docker met les informations d’identification en cache. Vous n’avez donc pas besoin de vous souvenir de l’ID d’application.</span><span class="sxs-lookup"><span data-stu-id="ba375-111">Once logged in, Docker caches the credentials, so you don't need to remember the app ID.</span></span>

> [!TIP]
> <span data-ttu-id="ba375-112">Si vous le souhaitez, vous pouvez régénérer le mot de passe d’un principal du service en exécutant la commande `az ad sp reset-credentials`.</span><span class="sxs-lookup"><span data-stu-id="ba375-112">If you want, you can regenerate the password of a service principal by running the `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="ba375-113">Les principaux du service autorisent [l’accès en fonction du rôle](../active-directory/role-based-access-control-configure.md) à un registre.</span><span class="sxs-lookup"><span data-stu-id="ba375-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) to a registry.</span></span> <span data-ttu-id="ba375-114">Les rôles disponibles sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="ba375-114">Available roles are:</span></span>
  * <span data-ttu-id="ba375-115">Lecteur (extraction).</span><span class="sxs-lookup"><span data-stu-id="ba375-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="ba375-116">Contributeur (extraction et envoi).</span><span class="sxs-lookup"><span data-stu-id="ba375-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="ba375-117">Propriétaire (extraction, envoi et attribution de rôles à d’autres utilisateurs).</span><span class="sxs-lookup"><span data-stu-id="ba375-117">Owner (pull, push, and assign roles to other users).</span></span>

<span data-ttu-id="ba375-118">L’accès anonyme n’est pas disponible sur les registres de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="ba375-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="ba375-119">Pour des images publiques, vous pouvez utiliser [Docker Hub](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="ba375-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="ba375-120">Vous pouvez affecter plusieurs principaux du service à un registre, ce qui vous permet de définir l’accès pour différents utilisateurs ou applications.</span><span class="sxs-lookup"><span data-stu-id="ba375-120">You can assign multiple service principals to a registry, which allows you to define access for different users or applications.</span></span> <span data-ttu-id="ba375-121">Les principaux du service activent également la connectivité « headless » (sans périphérique de contrôle) à un registre dans des scénarios de Développeur ou DevOps, tels que les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="ba375-121">Service principals also enable "headless" connectivity to a registry in developer or DevOps scenarios such as the following examples:</span></span>

  * <span data-ttu-id="ba375-122">Déploiements de conteneurs à partir d’un registre vers des systèmes d’orchestration, y compris DC/OS, Docker Swarm et Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="ba375-122">Container deployments from a registry to orchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="ba375-123">Vous pouvez également extraire des registres de conteneurs vers des services Azure connexes tels que [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/) et autres.</span><span class="sxs-lookup"><span data-stu-id="ba375-123">You can also pull container registries to related Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="ba375-124">Solutions d’intégration et de déploiement en continu (comme Visual Studio Team Services ou Jenkins) qui créent des images de conteneur et les envoient vers un registre.</span><span class="sxs-lookup"><span data-stu-id="ba375-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them to a registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="ba375-125">Compte d’administrateur</span><span class="sxs-lookup"><span data-stu-id="ba375-125">Admin account</span></span>
<span data-ttu-id="ba375-126">Un compte d’administrateur est créé automatiquement pour chaque registre que vous créez.</span><span class="sxs-lookup"><span data-stu-id="ba375-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="ba375-127">Le compte est désactivé par défaut, mais vous pouvez l’activer et gérer les informations d’identification, par exemple à l’aide du [portal](container-registry-get-started-portal.md#manage-registry-settings) ou des [commandes d’Azure CLI 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="ba375-127">By default the account is disabled, but you can enable it and manage the credentials, for example through the [portal](container-registry-get-started-portal.md#manage-registry-settings) or using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="ba375-128">Chaque compte d’administrateur reçoit deux mots de passe qui peuvent être régénérés.</span><span class="sxs-lookup"><span data-stu-id="ba375-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="ba375-129">Les deux mots de passe vous permettent de maintenir des connexions au Registre à en utilisant un mot de passe tandis que vous régénérez l’autre.</span><span class="sxs-lookup"><span data-stu-id="ba375-129">The two passwords allow you to maintain connections to the registry by using one password while you regenerate the other password.</span></span> <span data-ttu-id="ba375-130">Si le compte est activé, vous pouvez transmettre le nom d’utilisateur et chaque mot de passe à la commande `docker login` pour une authentification de base auprès du Registre.</span><span class="sxs-lookup"><span data-stu-id="ba375-130">If the account is enabled, you can pass the user name and either password to the `docker login` command for basic authentication to the registry.</span></span> <span data-ttu-id="ba375-131">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ba375-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="ba375-132">Le compte d’administrateur est conçu pour permettre à un seul utilisateur d’accéder au registre, principalement à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="ba375-132">The admin account is designed for a single user to access the registry, mainly for test purposes.</span></span> <span data-ttu-id="ba375-133">Il n’est pas recommandé de partager les informations d’identification du compte d’administrateur avec d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ba375-133">It is not recommended to share the admin account credentials among other users.</span></span> <span data-ttu-id="ba375-134">Tous les utilisateurs apparaissent sous la forme d’un seul utilisateur dans le registre.</span><span class="sxs-lookup"><span data-stu-id="ba375-134">All users appear as a single user to the registry.</span></span> <span data-ttu-id="ba375-135">La modification ou la désactivation de ce compte désactive l’accès au registre pour tous les utilisateurs qui utilisent les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="ba375-135">Changing or disabling this account disables registry access for all users who use the credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="ba375-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ba375-136">Next steps</span></span>
* <span data-ttu-id="ba375-137">[Transmettre votre première image à l’aide de l’interface de ligne de commande (CLI) Docker](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ba375-137">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="ba375-138">Pour plus d’informations sur l’authentification dans la version préliminaire du Registre de conteneurs, consultez le [billet de blog](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="ba375-138">For more information about authentication in the Container Registry preview, see the [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
