---
title: Principal du service de cluster Azure Kubernetes | Microsoft Docs
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
ms.openlocfilehash: 37171b4e69ad7d8c41ca8e7475c33ce70379f484
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="a0935-103">Configurer un principal de service Azure Active Directory pour un cluster Kubernetes dans Container Service</span><span class="sxs-lookup"><span data-stu-id="a0935-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="a0935-104">Dans Azure Container Service, un cluster Kubernetes nécessite un [principal de service Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) pour interagir avec des API Azure.</span><span class="sxs-lookup"><span data-stu-id="a0935-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) to interact with Azure APIs.</span></span> <span data-ttu-id="a0935-105">Le principal de service est nécessaire pour gérer dynamiquement des ressources telles que des [itinéraires définis par l’utilisateur](../../virtual-network/virtual-networks-udr-overview.md) et [Azure Load Balancer de couche 4](../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0935-105">The service principal is needed to dynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and the [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="a0935-106">Cet article indique les différentes options permettant de configurer un principal de service pour votre cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="a0935-106">This article shows different options to set up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="a0935-107">Par exemple, si vous avez installé et configuré [Azure CLI 2.0](/cli/azure/install-az-cli2), vous pouvez exécuter la commande [`az acs create`](/cli/azure/acs#create) pour créer le cluster Kubernetes et le principal du service en même temps.</span><span class="sxs-lookup"><span data-stu-id="a0935-107">For example, if you installed and set up the [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run the [`az acs create`](/cli/azure/acs#create) command to create the Kubernetes cluster and the service principal at the same time.</span></span>


## <a name="requirements-for-the-service-principal"></a><span data-ttu-id="a0935-108">Configuration requise pour le principal du service</span><span class="sxs-lookup"><span data-stu-id="a0935-108">Requirements for the service principal</span></span>

<span data-ttu-id="a0935-109">Vous pouvez utiliser un principal de service Azure AD existant qui répond aux exigences ci-dessous ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="a0935-109">You can use an existing Azure AD service principal that meets the following requirements, or create a new one.</span></span>

* <span data-ttu-id="a0935-110">**Étendue** : groupe de ressources de l’abonnement utilisé pour déployer le cluster Kubernetes ou abonnement utilisé pour déployer le cluster (de façon moins restrictive).</span><span class="sxs-lookup"><span data-stu-id="a0935-110">**Scope**: the resource group in the subscription used to deploy the Kubernetes cluster, or (less restrictively) the subscription used to deploy the cluster.</span></span>

* <span data-ttu-id="a0935-111">**Rôle** : **Collaborateur**</span><span class="sxs-lookup"><span data-stu-id="a0935-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="a0935-112">**Clé secrète client** : doit être un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a0935-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="a0935-113">Actuellement, vous ne pouvez pas utiliser de principal du service configuré pour l’authentification par certificat.</span><span class="sxs-lookup"><span data-stu-id="a0935-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a0935-114">Pour créer un principal de service, vous devez disposer des autorisations suffisantes pour inscrire une application auprès de votre client Azure AD et l’affecter à un rôle dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="a0935-114">To create a service principal, you must have permissions to register an application with your Azure AD tenant, and to assign the application to a role in your subscription.</span></span> <span data-ttu-id="a0935-115">Si voir si vous disposez des autorisations requises, [procédez à une vérification dans le portail](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="a0935-115">To see if you have the required permissions, [check in the Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="a0935-116">Option 1 : créer un principal de service dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0935-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="a0935-117">Si vous souhaitez créer un principal de service Azure AD avant de déployer votre cluster Kubernetes, Azure propose plusieurs méthodes.</span><span class="sxs-lookup"><span data-stu-id="a0935-117">If you want to create an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="a0935-118">L’exemple de commande suivant vous montre comment procéder avec [l’Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a0935-118">The following example commands show you how to do this with the [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="a0935-119">Vous pouvez également créer un principal de service à l’aide [d’Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), du [portail](../../azure-resource-manager/resource-group-create-service-principal-portal.md) ou d’autres méthodes.</span><span class="sxs-lookup"><span data-stu-id="a0935-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), the [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="a0935-120">Le résultat est semblable à ce qui suit (illustré ici de manière rédigée) :</span><span class="sxs-lookup"><span data-stu-id="a0935-120">Output is similar to the following (shown here redacted):</span></span>

![Créer un principal du service](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="a0935-122">**L’ID client** (`appId`) et la **clé secrète client** (`password`) que vous utilisez en tant que paramètres du principal du service pour le déploiement du cluster sont mis en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="a0935-122">Highlighted are the **client ID** (`appId`) and the **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-the-kubernetes-cluster"></a><span data-ttu-id="a0935-123">Spécifier un principal de service lors de la création du cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a0935-123">Specify service principal when creating the Kubernetes cluster</span></span>

<span data-ttu-id="a0935-124">Fournissez **l’ID client** (également appelé `appId`, pour l’ID de l’application) et la **clé secrète client** (`password`) d’un principal du service existant en tant que paramètres lors de la création du cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="a0935-124">Provide the **client ID** (also called the `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create the Kubernetes cluster.</span></span> <span data-ttu-id="a0935-125">Veillez à que le principal de service réponde aux exigences indiquées au début cet article.</span><span class="sxs-lookup"><span data-stu-id="a0935-125">Make sure the service principal meets the requirements at the beginning this article.</span></span>

<span data-ttu-id="a0935-126">Vous pouvez spécifier ces paramètres lors du déploiement du cluster Kubernetes à l’aide [d’Azure CLI 2.0](container-service-kubernetes-walkthrough.md), du [portail Azure](../dcos-swarm/container-service-deployment.md) ou d’autres méthodes.</span><span class="sxs-lookup"><span data-stu-id="a0935-126">You can specify these parameters when deploying the Kubernetes cluster using the [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="a0935-127">Lorsque vous spécifiez **l’ID client**, veillez à utiliser l’`appId`, et non l’`ObjectId`, du principal du service.</span><span class="sxs-lookup"><span data-stu-id="a0935-127">When specifying the **client ID**, be sure to use the `appId`, not the `ObjectId`, of the service principal.</span></span>
>

<span data-ttu-id="a0935-128">L’exemple suivant illustre une manière de transmettre les paramètres avec Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a0935-128">The following example shows one way to pass the parameters with the Azure CLI 2.0.</span></span> <span data-ttu-id="a0935-129">Cet exemple utilise le [modèle de démarrage rapide Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="a0935-129">This example uses the [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="a0935-130">[Téléchargez](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) le fichier de paramètres de modèle `azuredeploy.parameters.json` à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="a0935-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) the template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="a0935-131">Pour spécifier le principal du service, entrez les valeurs pour `servicePrincipalClientId` et `servicePrincipalClientSecret` dans le fichier</span><span class="sxs-lookup"><span data-stu-id="a0935-131">To specify the service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in the file.</span></span> <span data-ttu-id="a0935-132">(vous devez également fournir vos propres valeurs pour `dnsNamePrefix` et `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="a0935-132">(You also need to provide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="a0935-133">La clé en question est la clé publique SSH pour accéder au cluster). Enregistrez le fichier .</span><span class="sxs-lookup"><span data-stu-id="a0935-133">The latter is the SSH public key to access the cluster.) Save the file.</span></span>

    ![Transmettez les paramètres du principal du service](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="a0935-135">Exécutez la commande suivante à l’aide de `--parameters` pour définir le chemin d’accès au fichier azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="a0935-135">Run the following command, using `--parameters` to set the path to the azuredeploy.parameters.json file.</span></span> <span data-ttu-id="a0935-136">Cette commande déploie le cluster dans un groupe de ressources que vous créez appelé `myResourceGroup` dans la région États-Unis de l’Ouest.</span><span class="sxs-lookup"><span data-stu-id="a0935-136">This command deploys the cluster in a resource group you create called `myResourceGroup` in the West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-the-cluster-with-az-acs-create"></a><span data-ttu-id="a0935-137">Option 2 : générer un principal de service lors de la création du cluster avec `az acs create`</span><span class="sxs-lookup"><span data-stu-id="a0935-137">Option 2: Generate a service principal when creating the cluster with `az acs create`</span></span>

<span data-ttu-id="a0935-138">Si vous exécutez la commande [`az acs create`](/cli/azure/acs#create) pour créer le cluster Kubernetes, vous pouvez générer un principal de service automatiquement.</span><span class="sxs-lookup"><span data-stu-id="a0935-138">If you run the [`az acs create`](/cli/azure/acs#create) command to create the Kubernetes cluster, you have the option to generate a service principal automatically.</span></span>

<span data-ttu-id="a0935-139">Comme avec d’autres options de création de clusters Kubernetes, vous pouvez spécifier des paramètres pour un principal du service existant lorsque vous exécutez `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="a0935-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="a0935-140">Toutefois, si vous omettez ces paramètres, Azure CLI en crée un automatiquement à utiliser avec Container Service.</span><span class="sxs-lookup"><span data-stu-id="a0935-140">However, when you omit these parameters, the Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="a0935-141">Cette procédure est réalisée en toute transparence au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="a0935-141">This takes place transparently during the deployment.</span></span> 

<span data-ttu-id="a0935-142">La commande suivante crée un cluster Kubernetes et génère des clés SSH et des informations d’identification du principal du service :</span><span class="sxs-lookup"><span data-stu-id="a0935-142">The following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="a0935-143">Si votre compte ne dispose pas des autorisations Azure AD ni des autorisations d’abonnement pour créer un principal de service, la commande génère une erreur semblable à `Insufficient privileges to complete the operation.`</span><span class="sxs-lookup"><span data-stu-id="a0935-143">If your account doesn't have the Azure AD and subscription permissions to create a service principal, the command generates an error similar to `Insufficient privileges to complete the operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="a0935-144">Considérations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a0935-144">Additional considerations</span></span>

* <span data-ttu-id="a0935-145">Si vous ne disposez pas des autorisations pour créer un principal de service dans votre abonnement, vous devrez peut-être demander à votre administrateur Azure AD ou à l’administrateur de votre abonnement de vous attribuer les autorisations nécessaires ou de créer un principal de service à utiliser avec Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="a0935-145">If you don't have permissions to create a service principal in your subscription, you might need to ask your Azure AD or subscription administrator to assign the necessary permissions, or ask them for a service principal to use with Azure Container Service.</span></span> 

* <span data-ttu-id="a0935-146">Le principal de service pour Kubernetes fait partie de la configuration du cluster.</span><span class="sxs-lookup"><span data-stu-id="a0935-146">The service principal for Kubernetes is a part of the cluster configuration.</span></span> <span data-ttu-id="a0935-147">Toutefois, n’utilisez pas l’identité pour déployer le cluster.</span><span class="sxs-lookup"><span data-stu-id="a0935-147">However, don't use the identity to deploy the cluster.</span></span>

* <span data-ttu-id="a0935-148">Chaque principal de service est associé à une application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0935-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="a0935-149">Le principal de service pour un cluster Kubernetes peut être associé à tout nom d’application Azure AD valide (par exemple : `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="a0935-149">The service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="a0935-150">L’URL de l’application ne doit pas être un point de terminaison réel.</span><span class="sxs-lookup"><span data-stu-id="a0935-150">The URL for the application doesn't have to be a real endpoint.</span></span>

* <span data-ttu-id="a0935-151">Lorsque vous spécifiez **l’ID Client** du principal de service, vous pouvez utiliser la valeur de `appId` (comme indiqué dans cet article) ou le principal de service correspondant `name` (par exemple, `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="a0935-151">When specifying the service principal **Client ID**, you can use the value of the `appId` (as shown in this article) or the corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="a0935-152">Sur les machines virtuelles principales et d’agent du cluster Kubernetes, les informations d’identification du principal de service sont stockées dans le fichier /etc/kubernetes/azure.json.</span><span class="sxs-lookup"><span data-stu-id="a0935-152">On the master and agent VMs in the Kubernetes cluster, the service principal credentials are stored in the file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="a0935-153">Si vous utilisez la commande `az acs create` pour générer automatiquement le principal de service, les informations d’identification du principal de service sont écrites dans le fichier ~/.azure/acsServicePrincipal.json sur la machine utilisée pour exécuter la commande.</span><span class="sxs-lookup"><span data-stu-id="a0935-153">When you use the `az acs create` command to generate the service principal automatically, the service principal credentials are written to the file ~/.azure/acsServicePrincipal.json on the machine used to run the command.</span></span> 

* <span data-ttu-id="a0935-154">Si vous utilisez la commande `az acs create` pour générer automatiquement le principal de service, ce dernier peut également s’authentifier auprès d’un registre [Azure Container Registry](../../container-registry/container-registry-intro.md) créé dans le même abonnement.</span><span class="sxs-lookup"><span data-stu-id="a0935-154">When you use the `az acs create` command to generate the service principal automatically, the service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in the same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="a0935-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0935-155">Next steps</span></span>

* <span data-ttu-id="a0935-156">[Prise en main de Kubernetes](container-service-kubernetes-walkthrough.md) dans votre cluster de service de conteneur.</span><span class="sxs-lookup"><span data-stu-id="a0935-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="a0935-157">Pour résoudre les problèmes du principal de service pour Kubernetes, consultez la [documentation du moteur ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="a0935-157">To troubleshoot the service principal for Kubernetes, see the [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


