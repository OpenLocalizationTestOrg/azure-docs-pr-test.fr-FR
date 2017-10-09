---
title: principal aaaService pour Azure Kubernetes cluster | Documents Microsoft
description: "Créer et gérer un principal de service Azure Active Directory pour un cluster Kubernetes dans Azure Container Service"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="3dbb6-103">Configurer un principal de service Azure Active Directory pour un cluster Kubernetes dans Container Service</span><span class="sxs-lookup"><span data-stu-id="3dbb6-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="3dbb6-104">Dans le conteneur de Service Azure, un cluster Kubernetes nécessite un [principal du service Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) toointeract avec les API d’Azure.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) toointeract with Azure APIs.</span></span> <span data-ttu-id="3dbb6-105">Hello principal du service est nécessaire toodynamically gérer les ressources telles que [itinéraires définis par l’utilisateur](../../virtual-network/virtual-networks-udr-overview.md) et hello [équilibrage de charge de couche 4 Azure](../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3dbb6-105">hello service principal is needed toodynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and hello [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="3dbb6-106">Cet article explique tooset différentes options d’un service principal pour votre cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-106">This article shows different options tooset up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="3dbb6-107">Par exemple, si vous avez installé et configuré hello [Azure CLI 2.0](/cli/azure/install-az-cli2), vous pouvez exécuter hello [ `az acs create` ](/cli/azure/acs#create) commande toocreate hello Kubernetes cluster et hello principal du service à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-107">For example, if you installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster and hello service principal at hello same time.</span></span>


## <a name="requirements-for-hello-service-principal"></a><span data-ttu-id="3dbb6-108">Configuration requise pour le principal du service hello</span><span class="sxs-lookup"><span data-stu-id="3dbb6-108">Requirements for hello service principal</span></span>

<span data-ttu-id="3dbb6-109">Vous pouvez utiliser un principal de service Azure AD existant que répond aux hello suivant les exigences ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-109">You can use an existing Azure AD service principal that meets hello following requirements, or create a new one.</span></span>

* <span data-ttu-id="3dbb6-110">**Étendue**: groupe de ressources hello dans l’abonnement de hello utilisés cluster de Kubernetes toodeploy hello ou (moins de manière restrictive) abonnement de hello cluster hello de toodeploy.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-110">**Scope**: hello resource group in hello subscription used toodeploy hello Kubernetes cluster, or (less restrictively) hello subscription used toodeploy hello cluster.</span></span>

* <span data-ttu-id="3dbb6-111">**Rôle** : **Collaborateur**</span><span class="sxs-lookup"><span data-stu-id="3dbb6-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="3dbb6-112">**Clé secrète client** : doit être un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="3dbb6-113">Actuellement, vous ne pouvez pas utiliser de principal du service configuré pour l’authentification par certificat.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="3dbb6-114">toocreate un principal de service, vous devez disposer des autorisations tooregister une application avec votre locataire Azure AD et le rôle de tooa tooassign hello application dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-114">toocreate a service principal, you must have permissions tooregister an application with your Azure AD tenant, and tooassign hello application tooa role in your subscription.</span></span> <span data-ttu-id="3dbb6-115">toosee si vous avez les autorisations requises de hello, [archiver hello Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="3dbb6-115">toosee if you have hello required permissions, [check in hello Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="3dbb6-116">Option 1 : créer un principal de service dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3dbb6-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="3dbb6-117">Si vous voulez toocreate un principal du service Azure AD avant de déployer votre cluster Kubernetes, Azure fournit plusieurs méthodes.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-117">If you want toocreate an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="3dbb6-118">Hello suivant des exemples de commandes vous indiquent comment toodo avec hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3dbb6-118">hello following example commands show you how toodo this with hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="3dbb6-119">Vous pouvez également créer un service principal à l’aide de [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), ou d’autres méthodes.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="3dbb6-120">La sortie est similaire toohello suivante (présentée ici rédigé) :</span><span class="sxs-lookup"><span data-stu-id="3dbb6-120">Output is similar toohello following (shown here redacted):</span></span>

![Créer un principal du service](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="3dbb6-122">Mise en surbrillance sont hello **ID client** (`appId`) et hello **clé secrète client** (`password`) que vous utilisez en tant que paramètres de principal de service pour le déploiement de cluster.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-122">Highlighted are hello **client ID** (`appId`) and hello **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a><span data-ttu-id="3dbb6-123">Spécifiez le principal du service lors de la création du cluster de Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="3dbb6-123">Specify service principal when creating hello Kubernetes cluster</span></span>

<span data-ttu-id="3dbb6-124">Fournir hello **ID client** (également appelé hello `appId`, pour l’ID de l’Application) et **clé secrète client** (`password`) d’un service existant principal en tant que paramètres lorsque vous créez hello Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-124">Provide hello **client ID** (also called hello `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create hello Kubernetes cluster.</span></span> <span data-ttu-id="3dbb6-125">Assurez-vous que le principal du service hello répond aux exigences de hello en hello à partir de cet article.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-125">Make sure hello service principal meets hello requirements at hello beginning this article.</span></span>

<span data-ttu-id="3dbb6-126">Vous pouvez spécifier ces paramètres lors du déploiement de cluster de Kubernetes hello à l’aide de hello [Azure Interface de ligne de commande (CLI) 2.0](container-service-kubernetes-walkthrough.md), [portail Azure](../dcos-swarm/container-service-deployment.md), ou d’autres méthodes.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-126">You can specify these parameters when deploying hello Kubernetes cluster using hello [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="3dbb6-127">Lorsque vous spécifiez hello **ID client**, être vraiment toouse hello `appId`, pas hello `ObjectId`, de principal du service hello.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-127">When specifying hello **client ID**, be sure toouse hello `appId`, not hello `ObjectId`, of hello service principal.</span></span>
>

<span data-ttu-id="3dbb6-128">Hello suivant montre une façon toopass paramètres hello avec hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-128">hello following example shows one way toopass hello parameters with hello Azure CLI 2.0.</span></span> <span data-ttu-id="3dbb6-129">Cet exemple utilise hello [Kubernetes quickstart modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="3dbb6-129">This example uses hello [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="3dbb6-130">[Télécharger](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) fichier de paramètres de modèle hello `azuredeploy.parameters.json` à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) hello template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="3dbb6-131">service de hello toospecify principal, entrez les valeurs de `servicePrincipalClientId` et `servicePrincipalClientSecret` dans le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-131">toospecify hello service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in hello file.</span></span> <span data-ttu-id="3dbb6-132">(Vous devez également tooprovide vos propres valeurs pour `dnsNamePrefix` et `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-132">(You also need tooprovide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="3dbb6-133">Hello ce dernier est cluster hello de hello SSH tooaccess de clé publique). Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-133">hello latter is hello SSH public key tooaccess hello cluster.) Save hello file.</span></span>

    ![Transmettez les paramètres du principal du service](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="3dbb6-135">Exécution hello commande suivante, en utilisant `--parameters` tooset hello chemin d’accès toohello azuredeploy.parameters.json fichier.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-135">Run hello following command, using `--parameters` tooset hello path toohello azuredeploy.parameters.json file.</span></span> <span data-ttu-id="3dbb6-136">Cette commande déploie cluster hello dans un groupe de ressources que vous créez appelée `myResourceGroup` dans la région ouest des États-Unis hello.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-136">This command deploys hello cluster in a resource group you create called `myResourceGroup` in hello West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a><span data-ttu-id="3dbb6-137">Option 2 : Générer un principal de service lors de la création de cluster hello avec`az acs create`</span><span class="sxs-lookup"><span data-stu-id="3dbb6-137">Option 2: Generate a service principal when creating hello cluster with `az acs create`</span></span>

<span data-ttu-id="3dbb6-138">Si vous exécutez hello [ `az acs create` ](/cli/azure/acs#create) toocreate de commande hello Kubernetes cluster, vous avez un principal de service hello option toogenerate automatiquement.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-138">If you run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster, you have hello option toogenerate a service principal automatically.</span></span>

<span data-ttu-id="3dbb6-139">Comme avec d’autres options de création de clusters Kubernetes, vous pouvez spécifier des paramètres pour un principal du service existant lorsque vous exécutez `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="3dbb6-140">Toutefois, lorsque vous omettez ces paramètres, hello CLI d’Azure crée un automatiquement pour une utilisation avec le Service de conteneur.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-140">However, when you omit these parameters, hello Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="3dbb6-141">Cela s’effectue en toute transparence au cours du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-141">This takes place transparently during hello deployment.</span></span> 

<span data-ttu-id="3dbb6-142">Hello commande suivante crée un cluster Kubernetes et génère des clés SSH et les informations d’identification du principal de service :</span><span class="sxs-lookup"><span data-stu-id="3dbb6-142">hello following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="3dbb6-143">Si votre compte ne dispose pas hello Azure AD et abonnement autorisations toocreate un principal de service, commande hello génère une erreur similaire trop`Insufficient privileges toocomplete hello operation.`</span><span class="sxs-lookup"><span data-stu-id="3dbb6-143">If your account doesn't have hello Azure AD and subscription permissions toocreate a service principal, hello command generates an error similar too`Insufficient privileges toocomplete hello operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="3dbb6-144">Considérations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3dbb6-144">Additional considerations</span></span>

* <span data-ttu-id="3dbb6-145">Si vous n’avez toocreate d’autorisations à un principal de service dans votre abonnement, vous devrez peut-être tooask votre annuaire Azure AD ou abonnement administrateur tooassign hello des autorisations nécessaires ou demandez-lui un toouse principal de service avec le Service de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-145">If you don't have permissions toocreate a service principal in your subscription, you might need tooask your Azure AD or subscription administrator tooassign hello necessary permissions, or ask them for a service principal toouse with Azure Container Service.</span></span> 

* <span data-ttu-id="3dbb6-146">principal du service Hello pour Kubernetes fait partie de la configuration de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-146">hello service principal for Kubernetes is a part of hello cluster configuration.</span></span> <span data-ttu-id="3dbb6-147">Toutefois, n’utilisez pas cluster hello de hello identité toodeploy.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-147">However, don't use hello identity toodeploy hello cluster.</span></span>

* <span data-ttu-id="3dbb6-148">Chaque principal de service est associé à une application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="3dbb6-149">Hello principal du service pour un cluster Kubernetes peut être associé à n’importe quel Azure valide nom de l’application Active Directory (par exemple : `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="3dbb6-149">hello service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="3dbb6-150">URL de Hello pour une application hello n’a pas un point de terminaison réel toobe.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-150">hello URL for hello application doesn't have toobe a real endpoint.</span></span>

* <span data-ttu-id="3dbb6-151">Lorsque vous spécifiez principal du service hello **ID Client**, vous pouvez utiliser la valeur hello hello `appId` (comme indiqué dans cet article) ou principal du service correspondant hello `name` (par exemple,`https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="3dbb6-151">When specifying hello service principal **Client ID**, you can use hello value of hello `appId` (as shown in this article) or hello corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="3dbb6-152">Sur le maître de hello et de machines virtuelles dans un cluster de Kubernetes hello, hello service principal sont stockées dans hello fichier /etc/kubernetes/azure.json.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-152">On hello master and agent VMs in hello Kubernetes cluster, hello service principal credentials are stored in hello file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="3dbb6-153">Lorsque vous utilisez hello `az acs create` commande principal du service toogenerate hello automatiquement, les informations d’identification de principal hello service sont écrites toohello fichier ~/.azure/acsServicePrincipal.json sur l’ordinateur de hello utilisé toorun hello.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-153">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal credentials are written toohello file ~/.azure/acsServicePrincipal.json on hello machine used toorun hello command.</span></span> 

* <span data-ttu-id="3dbb6-154">Lorsque vous utilisez hello `az acs create` commande principal du service toogenerate hello automatiquement, le principal du service hello peut également authentifier avec un [Registre de conteneur Azure](../../container-registry/container-registry-intro.md) créées Bonjour même abonnement.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-154">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in hello same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="3dbb6-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3dbb6-155">Next steps</span></span>

* <span data-ttu-id="3dbb6-156">[Prise en main de Kubernetes](container-service-kubernetes-walkthrough.md) dans votre cluster de service de conteneur.</span><span class="sxs-lookup"><span data-stu-id="3dbb6-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="3dbb6-157">tootroubleshoot hello principal du service pour Kubernetes, consultez hello [documentation du moteur de ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="3dbb6-157">tootroubleshoot hello service principal for Kubernetes, see hello [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


