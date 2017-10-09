---
title: aaaAuthenticate avec un Registre de conteneur Azure | Documents Microsoft
description: "Comment toolog dans le Registre de conteneur Azure tooan à l’aide d’Azure Active Directory service principal ou un compte d’administrateur"
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
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="6af5e-103">S’authentifier avec un registre de conteneurs Docker</span><span class="sxs-lookup"><span data-stu-id="6af5e-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="6af5e-104">toowork avec les images de conteneur dans un Registre de conteneur Azure, vous vous connectez à l’aide de hello `docker login` commande.</span><span class="sxs-lookup"><span data-stu-id="6af5e-104">toowork with container images in an Azure container registry, you log in using hello `docker login` command.</span></span> <span data-ttu-id="6af5e-105">Vous pouvez vous connecter en utilisant un **[principal du service Azure Active Directory](../active-directory/active-directory-application-objects.md)** ou un **compte d’administrateur** spécifique à un registre.</span><span class="sxs-lookup"><span data-stu-id="6af5e-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="6af5e-106">Cet article fournit des détails sur ces identités.</span><span class="sxs-lookup"><span data-stu-id="6af5e-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="6af5e-107">Principal du service</span><span class="sxs-lookup"><span data-stu-id="6af5e-107">Service principal</span></span>

<span data-ttu-id="6af5e-108">Vous pouvez [affecter un principal de service](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour Registre et l’utiliser pour l’authentification de base Docker.</span><span class="sxs-lookup"><span data-stu-id="6af5e-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="6af5e-109">L’utilisation d’un principal du service est recommandée dans la plupart des scénarios.</span><span class="sxs-lookup"><span data-stu-id="6af5e-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="6af5e-110">Fournir l’ID de l’application hello et le mot de passe toohello principal du service hello `docker login` de commande, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6af5e-110">Provide hello app ID and password of hello service principal toohello `docker login` command, as shown in hello following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="6af5e-111">Une fois connecté, Docker met en cache les informations d’identification de hello, vous n’avez pas besoin d’identifiant d’application tooremember hello.</span><span class="sxs-lookup"><span data-stu-id="6af5e-111">Once logged in, Docker caches hello credentials, so you don't need tooremember hello app ID.</span></span>

> [!TIP]
> <span data-ttu-id="6af5e-112">Si vous le souhaitez, vous pouvez régénérer le mot de passe hello d’un principal de service en exécutant hello `az ad sp reset-credentials` commande.</span><span class="sxs-lookup"><span data-stu-id="6af5e-112">If you want, you can regenerate hello password of a service principal by running hello `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="6af5e-113">Autoriser les principaux du service [accès en fonction du rôle](../active-directory/role-based-access-control-configure.md) tooa Registre.</span><span class="sxs-lookup"><span data-stu-id="6af5e-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) tooa registry.</span></span> <span data-ttu-id="6af5e-114">Les rôles disponibles sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="6af5e-114">Available roles are:</span></span>
  * <span data-ttu-id="6af5e-115">Lecteur (extraction).</span><span class="sxs-lookup"><span data-stu-id="6af5e-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="6af5e-116">Contributeur (extraction et envoi).</span><span class="sxs-lookup"><span data-stu-id="6af5e-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="6af5e-117">Propriétaire (par extraction de données, par envoi de données et affecter des rôles utilisateurs tooother).</span><span class="sxs-lookup"><span data-stu-id="6af5e-117">Owner (pull, push, and assign roles tooother users).</span></span>

<span data-ttu-id="6af5e-118">L’accès anonyme n’est pas disponible sur les registres de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="6af5e-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="6af5e-119">Pour des images publiques, vous pouvez utiliser [Docker Hub](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="6af5e-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="6af5e-120">Vous pouvez affecter plusieurs principaux de service de Registre tooa, ce qui vous permet d’accéder toodefine pour différents utilisateurs ou les applications.</span><span class="sxs-lookup"><span data-stu-id="6af5e-120">You can assign multiple service principals tooa registry, which allows you toodefine access for different users or applications.</span></span> <span data-ttu-id="6af5e-121">Principaux de service permettent également de Registre tooa connectivité « sans affichage » développeur ou DevOps scénarios hello exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6af5e-121">Service principals also enable "headless" connectivity tooa registry in developer or DevOps scenarios such as hello following examples:</span></span>

  * <span data-ttu-id="6af5e-122">Déploiements de conteneur à partir d’un système de tooorchestration de Registre, y compris le contrôleur de domaine/système d’exploitation, Docker Swarm et Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6af5e-122">Container deployments from a registry tooorchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="6af5e-123">Vous pouvez également extraire toorelated de registres de conteneur des services Azure tels que [Service de conteneur](../container-service/index.yml), [du Service d’applications](../app-service/index.md), [lot](../batch/index.md), [Service Fabric](/azure/service-fabric/)et d’autres.</span><span class="sxs-lookup"><span data-stu-id="6af5e-123">You can also pull container registries toorelated Azure services such as [Container Service](../container-service/index.yml), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="6af5e-124">Continue intégration et le déploiement des solutions (tels que Visual Studio Team Services ou Jenkins) qui génèrent des images de conteneur et de les transmettre tooa Registre.</span><span class="sxs-lookup"><span data-stu-id="6af5e-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them tooa registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="6af5e-125">Compte d’administrateur</span><span class="sxs-lookup"><span data-stu-id="6af5e-125">Admin account</span></span>
<span data-ttu-id="6af5e-126">Un compte d’administrateur est créé automatiquement pour chaque registre que vous créez.</span><span class="sxs-lookup"><span data-stu-id="6af5e-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="6af5e-127">Compte de hello est désactivé par défaut, mais vous pouvez l’activer et gérer les informations d’identification hello, par exemple via hello [portal](container-registry-get-started-portal.md#manage-registry-settings) ou à l’aide de hello [Azure CLI 2.0 commandes](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="6af5e-127">By default hello account is disabled, but you can enable it and manage hello credentials, for example through hello [portal](container-registry-get-started-portal.md#manage-registry-settings) or using hello [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="6af5e-128">Chaque compte d’administrateur reçoit deux mots de passe qui peuvent être régénérés.</span><span class="sxs-lookup"><span data-stu-id="6af5e-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="6af5e-129">deux mots de passe Hello permettent de Registre de toohello toomaintain connexions en utilisant un mot de passe pendant la régénération de hello autre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="6af5e-129">hello two passwords allow you toomaintain connections toohello registry by using one password while you regenerate hello other password.</span></span> <span data-ttu-id="6af5e-130">Si le compte de hello est activé, vous pouvez passer le nom d’utilisateur hello et soit toohello de mot de passe `docker login` commande de Registre toohello de l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="6af5e-130">If hello account is enabled, you can pass hello user name and either password toohello `docker login` command for basic authentication toohello registry.</span></span> <span data-ttu-id="6af5e-131">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6af5e-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="6af5e-132">compte d’administrateur Hello est conçu pour un seul utilisateur tooaccess hello du Registre, principalement à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="6af5e-132">hello admin account is designed for a single user tooaccess hello registry, mainly for test purposes.</span></span> <span data-ttu-id="6af5e-133">Il est recommandé pas les informations d’identification du compte de l’administrateur tooshare hello parmi d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6af5e-133">It is not recommended tooshare hello admin account credentials among other users.</span></span> <span data-ttu-id="6af5e-134">Tous les utilisateurs apparaissent sous la forme d’un Registre de toohello utilisateur unique.</span><span class="sxs-lookup"><span data-stu-id="6af5e-134">All users appear as a single user toohello registry.</span></span> <span data-ttu-id="6af5e-135">La modification ou la désactivation de ce compte désactive l’accès au Registre pour tous les utilisateurs qui utilisent des informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="6af5e-135">Changing or disabling this account disables registry access for all users who use hello credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="6af5e-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6af5e-136">Next steps</span></span>
* <span data-ttu-id="6af5e-137">[Push de votre première image à l’aide de hello Docker CLI](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6af5e-137">[Push your first image using hello Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="6af5e-138">Pour plus d’informations sur l’authentification dans l’aperçu du Registre de conteneur hello, consultez hello [billet de blog](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="6af5e-138">For more information about authentication in hello Container Registry preview, see hello [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
