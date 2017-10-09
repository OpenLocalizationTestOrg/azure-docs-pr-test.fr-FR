---
title: "Registre de conteneur de Docker privé aaaCreate - CLI d’Azure | Documents Microsoft"
description: "Commencer à créer et gérer des registres de conteneur Docker privés avec hello Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a><span data-ttu-id="46ad6-103">Créer un Registre de conteneur Docker privé à l’aide de hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="46ad6-103">Create a private Docker container registry using hello Azure CLI 2.0</span></span>
<span data-ttu-id="46ad6-104">Utiliser les commandes hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate un Registre de conteneur et de gérer ses paramètres de votre ordinateur Linux, Mac ou Windows.</span><span class="sxs-lookup"><span data-stu-id="46ad6-104">Use commands in hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate a container registry and manage its settings from your Linux, Mac, or Windows computer.</span></span> <span data-ttu-id="46ad6-105">Vous pouvez également créer et gérer des registres de conteneur à l’aide de hello [portail Azure](container-registry-get-started-portal.md) ou par programme avec hello Registre de conteneur [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="46ad6-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="46ad6-106">Pour des informations et des concepts, consultez [hello vue d’ensemble](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="46ad6-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="46ad6-107">Aide sur les commandes CLI de Registre de conteneur (`az acr` commandes), passez hello `-h` commande tooany de paramètre.</span><span class="sxs-lookup"><span data-stu-id="46ad6-107">For help on Container Registry CLI commands (`az acr` commands), pass hello `-h` parameter tooany command.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="46ad6-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="46ad6-108">Prerequisites</span></span>
* <span data-ttu-id="46ad6-109">**Azure CLI 2.0**: tooinstall et prise en main hello CLI 2.0, consultez hello [des instructions d’installation](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="46ad6-109">**Azure CLI 2.0**: tooinstall and get started with hello CLI 2.0, see hello [installation instructions](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="46ad6-110">Connectez-vous à tooyour abonnement Azure en exécutant `az login`.</span><span class="sxs-lookup"><span data-stu-id="46ad6-110">Log in tooyour Azure subscription by running `az login`.</span></span> <span data-ttu-id="46ad6-111">Pour plus d’informations, consultez [prise en main hello CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="46ad6-111">For more information, see [Get started with hello CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="46ad6-112">**Groupe de ressources** : créez un [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups) avant de créer un registre de conteneur, ou utilisez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="46ad6-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="46ad6-113">Assurez-vous que le groupe de ressources hello est dans un emplacement où le service de Registre de conteneur de hello est [disponible](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="46ad6-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="46ad6-114">un groupe de ressources à l’aide de toocreate hello CLI 2.0, consultez [hello référence CLI 2.0](/cli/azure/group).</span><span class="sxs-lookup"><span data-stu-id="46ad6-114">toocreate a resource group using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/group).</span></span>
* <span data-ttu-id="46ad6-115">**Compte de stockage** (facultatif) : créez un Azure standard [compte de stockage](../storage/common/storage-introduction.md) tooback Registre de conteneur hello Bonjour même emplacement.</span><span class="sxs-lookup"><span data-stu-id="46ad6-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="46ad6-116">Si vous ne spécifiez pas un compte de stockage lors de la création d’un Registre avec `az acr create`, commande hello crée une pour vous.</span><span class="sxs-lookup"><span data-stu-id="46ad6-116">If you don't specify a storage account when creating a registry with `az acr create`, hello command creates one for you.</span></span> <span data-ttu-id="46ad6-117">un stockage compte à l’aide de toocreate hello CLI 2.0, consultez [hello référence CLI 2.0](/cli/azure/storage/account).</span><span class="sxs-lookup"><span data-stu-id="46ad6-117">toocreate a storage account using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/storage/account).</span></span> <span data-ttu-id="46ad6-118">Pour l’instant, l’offre Stockage Premium n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="46ad6-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="46ad6-119">**Principal du service** (facultatif) : lorsque vous créez un Registre par hello CLI, par défaut il n'est pas configuré pour l’accès.</span><span class="sxs-lookup"><span data-stu-id="46ad6-119">**Service principal** (optional): When you create a registry with hello CLI, by default it is not set up for access.</span></span> <span data-ttu-id="46ad6-120">Selon vos besoins, vous pouvez affecter un Registre tooa principal de service Azure Active Directory existant (ou créer et affecter une autre), ou activer le compte d’utilisateur admin du Registre hello.</span><span class="sxs-lookup"><span data-stu-id="46ad6-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry (or create and assign a new one), or enable hello registry's admin user account.</span></span> <span data-ttu-id="46ad6-121">Consultez les sections hello plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="46ad6-121">See hello sections later in this article.</span></span> <span data-ttu-id="46ad6-122">Pour plus d’informations sur l’accès au Registre, consultez [authentifier avec le Registre de conteneur hello](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="46ad6-122">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="46ad6-123">Créer un registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="46ad6-123">Create a container registry</span></span>
<span data-ttu-id="46ad6-124">Exécutez hello `az acr create` commande toocreate un Registre de conteneur.</span><span class="sxs-lookup"><span data-stu-id="46ad6-124">Run hello `az acr create` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="46ad6-125">Lorsque vous créez un registre, spécifiez un nom de domaine global unique de niveau supérieur, contenant uniquement des chiffres et des lettres.</span><span class="sxs-lookup"><span data-stu-id="46ad6-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="46ad6-126">nom de Registre Hello dans les exemples hello est `myRegistry1`, mais remplacer par un nom unique de votre choix.</span><span class="sxs-lookup"><span data-stu-id="46ad6-126">hello registry name in hello examples is `myRegistry1`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="46ad6-127">Hello utilise hello Registre de conteneur toocreate minimal de paramètres de commande suivante `myRegistry1` dans le groupe de ressources hello `myResourceGroup`et à l’aide de hello *base* référence (SKU) :</span><span class="sxs-lookup"><span data-stu-id="46ad6-127">hello following command uses hello minimal parameters toocreate container registry `myRegistry1` in hello resource group `myResourceGroup`, and using hello *Basic* sku:</span></span>

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* <span data-ttu-id="46ad6-128">`--storage-account-name` est facultatif.</span><span class="sxs-lookup"><span data-stu-id="46ad6-128">`--storage-account-name` is optional.</span></span> <span data-ttu-id="46ad6-129">Si ce n’est pas spécifié, un compte de stockage est créé avec un nom composé du nom de Registre hello et un horodatage dans hello spécifié le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="46ad6-129">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

<span data-ttu-id="46ad6-130">Lors de la création de Registre de hello, sortie de hello est similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="46ad6-130">When hello registry is created, hello output is similar toohello following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


<span data-ttu-id="46ad6-131">Notez les poins suivants :</span><span class="sxs-lookup"><span data-stu-id="46ad6-131">Take special note:</span></span>

* <span data-ttu-id="46ad6-132">`id`-Identificateur de Registre hello dans votre abonnement, vous avez besoin si vous souhaitez tooassign un principal de service.</span><span class="sxs-lookup"><span data-stu-id="46ad6-132">`id` - Identifier for hello registry in your subscription, which you need if you want tooassign a service principal.</span></span>
* <span data-ttu-id="46ad6-133">`loginServer`-nom complet de hello vous spécifiez trop[connecter toohello Registre](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="46ad6-133">`loginServer` - hello fully qualified name you specify too[log in toohello registry](container-registry-authentication.md).</span></span> <span data-ttu-id="46ad6-134">Dans cet exemple, le nom de hello est `myregistry1.exp.azurecr.io` (tout en minuscules).</span><span class="sxs-lookup"><span data-stu-id="46ad6-134">In this example, hello name is `myregistry1.exp.azurecr.io` (all lowercase).</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="46ad6-135">Affecter un principal de service</span><span class="sxs-lookup"><span data-stu-id="46ad6-135">Assign a service principal</span></span>
<span data-ttu-id="46ad6-136">Utilisez tooassign des commandes CLI 2.0 un Registre tooa principal du service Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="46ad6-136">Use CLI 2.0 commands tooassign an Azure Active Directory service principal tooa registry.</span></span> <span data-ttu-id="46ad6-137">Hello principal du service dans ces exemples se voit attribuer hello propriétaire du rôle, mais vous pouvez affecter [autres rôles](../active-directory/role-based-access-control-configure.md) si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="46ad6-137">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a><span data-ttu-id="46ad6-138">Créer un principal de service et assigner le Registre de toohello d’accès</span><span class="sxs-lookup"><span data-stu-id="46ad6-138">Create a service principal and assign access toohello registry</span></span>
<span data-ttu-id="46ad6-139">Bonjour la commande suivante, un principal de service est affecté identificateur Registre propriétaire du rôle accès toohello passé avec hello `--scopes` paramètre.</span><span class="sxs-lookup"><span data-stu-id="46ad6-139">In hello following command, a new service principal is assigned Owner role access toohello registry identifier passed with hello `--scopes` parameter.</span></span> <span data-ttu-id="46ad6-140">Spécifiez un mot de passe fort avec hello `--password` paramètre.</span><span class="sxs-lookup"><span data-stu-id="46ad6-140">Specify a strong password with hello `--password` parameter.</span></span>

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a><span data-ttu-id="46ad6-141">Affecter un principal de service existant</span><span class="sxs-lookup"><span data-stu-id="46ad6-141">Assign an existing service principal</span></span>
<span data-ttu-id="46ad6-142">Si vous disposez d’un principal de service déjà et que vous souhaitez tooassign il propriétaire du rôle accès toohello exécution de Registre, un toohello similaire commande exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="46ad6-142">If you already have a service principal and want tooassign it Owner role access toohello registry, run a command similar toohello following example.</span></span> <span data-ttu-id="46ad6-143">Vous passez l’ID d’application principal de service hello à l’aide de hello `--assignee` paramètre :</span><span class="sxs-lookup"><span data-stu-id="46ad6-143">You pass hello service principal app ID using hello `--assignee` parameter:</span></span>

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a><span data-ttu-id="46ad6-144">Gérer les informations d’identification de l’administrateur</span><span class="sxs-lookup"><span data-stu-id="46ad6-144">Manage admin credentials</span></span>
<span data-ttu-id="46ad6-145">Un compte d’administrateur est automatiquement créé pour chaque registre de conteneur et est désactivé par défaut.</span><span class="sxs-lookup"><span data-stu-id="46ad6-145">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="46ad6-146">Hello suivant illustrent les exemples `az acr` toomanage hello admin informations d’identification pour le Registre de votre conteneur de commandes CLI.</span><span class="sxs-lookup"><span data-stu-id="46ad6-146">hello following examples show `az acr` CLI commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="46ad6-147">Obtenir les informations d’identification de l’utilisateur Admin</span><span class="sxs-lookup"><span data-stu-id="46ad6-147">Obtain admin user credentials</span></span>
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="46ad6-148">Activer l’utilisateur Admin pour un registre existant</span><span class="sxs-lookup"><span data-stu-id="46ad6-148">Enable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="46ad6-149">Désactiver l’utilisateur Admin pour un registre existant</span><span class="sxs-lookup"><span data-stu-id="46ad6-149">Disable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a><span data-ttu-id="46ad6-150">Répertorier les images et les balises</span><span class="sxs-lookup"><span data-stu-id="46ad6-150">List images and tags</span></span>
<span data-ttu-id="46ad6-151">Hello d’utilisation `az acr` commandes CLI de balises dans un référentiel et des images de hello tooquery.</span><span class="sxs-lookup"><span data-stu-id="46ad6-151">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="46ad6-152">Actuellement, Registre de conteneur ne prend pas en charge hello `docker search` tooquery de commande pour les images et les balises.</span><span class="sxs-lookup"><span data-stu-id="46ad6-152">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>


### <a name="list-repositories"></a><span data-ttu-id="46ad6-153">Répertorier les référentiels</span><span class="sxs-lookup"><span data-stu-id="46ad6-153">List repositories</span></span>
<span data-ttu-id="46ad6-154">Hello exemple suivant répertorie les référentiels hello dans un Registre, au format JSON (JavaScript Object Notation) :</span><span class="sxs-lookup"><span data-stu-id="46ad6-154">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="46ad6-155">Répertorier les balises</span><span class="sxs-lookup"><span data-stu-id="46ad6-155">List tags</span></span>
<span data-ttu-id="46ad6-156">Hello exemple suivant répertorie les balises hello sur hello **exemples/nginx** référentiel, au format JSON :</span><span class="sxs-lookup"><span data-stu-id="46ad6-156">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="46ad6-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="46ad6-157">Next steps</span></span>
* [<span data-ttu-id="46ad6-158">Push de votre première image à l’aide de hello Docker CLI</span><span class="sxs-lookup"><span data-stu-id="46ad6-158">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
