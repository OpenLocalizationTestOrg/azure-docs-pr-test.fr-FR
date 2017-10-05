---
title: "Déployer OpenShift Origin sur Azure | Microsoft Docs"
description: "Découvrez comment déployer OpenShift Origin sur des machines virtuelles Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: e03da05625e440eab29ccc28a2343d3433fc7607
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-openshift-origin-to-azure-virtual-machines"></a><span data-ttu-id="d437e-103">Déployer OpenShift Origin sur des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="d437e-103">Deploy OpenShift Origin to Azure Virtual Machines</span></span> 

<span data-ttu-id="d437e-104">[OpenShift Origin](https://www.openshift.org/) est une plateforme de conteneurs open source basée sur [Kubernetes](https://kubernetes.io/).</span><span class="sxs-lookup"><span data-stu-id="d437e-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="d437e-105">Elle simplifie le processus de déploiement, de mise à l’échelle et d’exploitation d’applications mutualisées.</span><span class="sxs-lookup"><span data-stu-id="d437e-105">It simplifies the process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="d437e-106">Ce guide décrit comment déployer OpenShift Origin sur des machines virtuelles Azure à l’aide de l’interface de ligne de commande (CLI) Azure et de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d437e-106">This guide describes how to deploy OpenShift Origin on Azure Virtual Machines using the Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="d437e-107">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d437e-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d437e-108">Créer un Key Vault pour gérer les clés SSH pour le cluster OpenShift.</span><span class="sxs-lookup"><span data-stu-id="d437e-108">Create a KeyVault to manage SSH keys for the OpenShift cluster.</span></span>
> * <span data-ttu-id="d437e-109">Déployer un cluster OpenShift sur les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="d437e-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="d437e-110">Installer et configurer l’interface [CLI OpenShift](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) pour gérer le cluster.</span><span class="sxs-lookup"><span data-stu-id="d437e-110">Install and configure the [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) to manage the cluster.</span></span>
> * <span data-ttu-id="d437e-111">Personnaliser le déploiement OpenShift.</span><span class="sxs-lookup"><span data-stu-id="d437e-111">Customize the OpenShift deployment.</span></span>

<span data-ttu-id="d437e-112">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="d437e-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="d437e-113">Ce démarrage rapide requiert la version 2.0.8 ou ultérieure de l’interface Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d437e-113">This quick start requires the Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="d437e-114">Pour connaître la version de l’interface, exécutez `az --version`.</span><span class="sxs-lookup"><span data-stu-id="d437e-114">To find the version, run `az --version`.</span></span> <span data-ttu-id="d437e-115">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d437e-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="d437e-116">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="d437e-116">Log in to Azure</span></span> 
<span data-ttu-id="d437e-117">Connectez-vous à votre abonnement Azure avec la commande [az login](/cli/azure/#login) et suivez les instructions à l’écran ou cliquez sur **Essayer** pour utiliser Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="d437e-117">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions or click **Try it** to use Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="d437e-118">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="d437e-118">Create a resource group</span></span>

<span data-ttu-id="d437e-119">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d437e-119">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d437e-120">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="d437e-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="d437e-121">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *eastus*.</span><span class="sxs-lookup"><span data-stu-id="d437e-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="d437e-122">Créer un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="d437e-122">Create a Key Vault</span></span>
<span data-ttu-id="d437e-123">Créez un Key Vault pour stocker les clés SSH pour le cluster avec la commande [az keyvault create](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="d437e-123">Create a KeyVault to store the SSH keys for the cluster with the [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="d437e-124">Création d’une clé SSH</span><span class="sxs-lookup"><span data-stu-id="d437e-124">Create an SSH key</span></span> 
<span data-ttu-id="d437e-125">Une clé SSH est nécessaire pour sécuriser l’accès au cluster OpenShift Origin.</span><span class="sxs-lookup"><span data-stu-id="d437e-125">An SSH key is needed to secure access to the OpenShift Origin cluster.</span></span> <span data-ttu-id="d437e-126">Créez une paire de clés SSH à l’aide de la commande `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="d437e-126">Create an SSH key-pair using the `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="d437e-127">La paire de clés SSH créée ne doit pas présenter de phrase secrète.</span><span class="sxs-lookup"><span data-stu-id="d437e-127">The SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="d437e-128">Pour plus d’informations sur les clés SSH sur Windows, consultez [Utilisation de clés SSH avec Windows sur Azure](/azure/virtual-machines/linux/ssh-from-windows).</span><span class="sxs-lookup"><span data-stu-id="d437e-128">For more information on SSH keys on Windows, [How to create SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="d437e-129">Stocker la clé privée SSH dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="d437e-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="d437e-130">Le déploiement OpenShift utilise la clé SSH que vous avez créée pour sécuriser l’accès au maître OpenShift.</span><span class="sxs-lookup"><span data-stu-id="d437e-130">The OpenShift deployment uses the SSH key you created to secure access to the OpenShift master.</span></span> <span data-ttu-id="d437e-131">Pour permettre au déploiement de récupérer la clé SSH en toute sécurité, stockez la clé dans Key Vault à l’aide de la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="d437e-131">To enable the deployment to securely retrieve the SSH key, store the key in Key Vault using the following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="d437e-132">Activé pour le déploiement de modèle</span><span class="sxs-lookup"><span data-stu-id="d437e-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="d437e-133">Créer un principal du service</span><span class="sxs-lookup"><span data-stu-id="d437e-133">Create a service principal</span></span> 
<span data-ttu-id="d437e-134">OpenShift communique avec Azure à l’aide d’un nom d’utilisateur et d’un mot de passe ou d’un principal de service.</span><span class="sxs-lookup"><span data-stu-id="d437e-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="d437e-135">Un principal de service Azure est une identité de sécurité que vous pouvez utiliser avec des applications, des services et des outils d’automatisation comme OpenShift.</span><span class="sxs-lookup"><span data-stu-id="d437e-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="d437e-136">Vous contrôlez et définissez les opérations que le principal du service est autorisé à effectuer dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d437e-136">You control and define the permissions as to what operations the service principal can perform in Azure.</span></span> <span data-ttu-id="d437e-137">Pour renforcer la sécurité par rapport à la simple saisie d’un nom d’utilisateur et d’un mot de passe, cet exemple crée un principal de service de base.</span><span class="sxs-lookup"><span data-stu-id="d437e-137">To improve security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="d437e-138">Créez un principal de service avec la commande [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) et affichez les informations d’identification requises par OpenShift :</span><span class="sxs-lookup"><span data-stu-id="d437e-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output the credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="d437e-139">Prenez note de la propriété appId renvoyée par la commande.</span><span class="sxs-lookup"><span data-stu-id="d437e-139">Take note of the appId property returned from the command.</span></span>
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > <span data-ttu-id="d437e-140">Ne créez pas un mot de passe non sécurisé.</span><span class="sxs-lookup"><span data-stu-id="d437e-140">Don't create an insecure password.</span></span>  <span data-ttu-id="d437e-141">Suivez les conseils en matière de [Stratégies et restrictions de mot de passe dans Azure Active Directory](/azure/active-directory/active-directory-passwords-policy).</span><span class="sxs-lookup"><span data-stu-id="d437e-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="d437e-142">Pour plus d’informations sur les principaux de service, consultez [Créer un principal du service avec Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d437e-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-the-openshift-origin-template"></a><span data-ttu-id="d437e-143">Déployer le modèle OpenShift Origin</span><span class="sxs-lookup"><span data-stu-id="d437e-143">Deploy the OpenShift Origin template</span></span>
<span data-ttu-id="d437e-144">Vous allez maintenant déployer OpenShift Origin à l’aide d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d437e-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="d437e-145">La commande suivante requiert la version 2.0.8 ou ultérieure de l’interface Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d437e-145">The following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="d437e-146">Pour vérifier la version de l’interface Azure CLI, exécutez la commande `az --version`.</span><span class="sxs-lookup"><span data-stu-id="d437e-146">You can verify the az CLI version with the `az --version` command.</span></span> <span data-ttu-id="d437e-147">Pour mettre à jour l’interface, consultez [Installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d437e-147">To update the CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="d437e-148">Utilisez la valeur de `appId` du principal de service créé précédemment pour le paramètre `aadClientId`.</span><span class="sxs-lookup"><span data-stu-id="d437e-148">Use the `appId` value from the service principal you created earlier for the `aadClientId` parameter.</span></span>

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
<span data-ttu-id="d437e-149">Le déploiement peut prendre jusqu’à 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="d437e-149">The deployment may take up to 20 minutes to complete.</span></span> <span data-ttu-id="d437e-150">L’URL de la console OpenShift et le nom DNS du maître OpenShift est affiché sur le terminal à l’issue du déploiement.</span><span class="sxs-lookup"><span data-stu-id="d437e-150">The URL of the OpenShift console and DNS name of the OpenShift master is printed to the terminal when the deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-to-the-openshift-cluster"></a><span data-ttu-id="d437e-151">Se connecter au cluster OpenShift</span><span class="sxs-lookup"><span data-stu-id="d437e-151">Connect to the OpenShift cluster</span></span>
<span data-ttu-id="d437e-152">Une fois le déploiement terminé, connectez-vous à la console OpenShift dans un navigateur à l’aide de la valeur de `OpenShift Console Uri`.</span><span class="sxs-lookup"><span data-stu-id="d437e-152">When the deployment completes, connect to the OpenShift console using the browser using the `OpenShift Console Uri`.</span></span> <span data-ttu-id="d437e-153">Vous avez également la possibilité de vous connecter au maître OpenShift à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d437e-153">Alternatively, you can connect to the OpenShift master using the following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="d437e-154">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="d437e-154">Clean up resources</span></span>
<span data-ttu-id="d437e-155">Lorsque vous n’en avez plus besoin, vous pouvez utiliser la commande [az group delete](/cli/azure/group#delete) pour supprimer le groupe de ressources, le cluster OpenShift et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="d437e-155">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="d437e-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d437e-156">Next steps</span></span>

<span data-ttu-id="d437e-157">Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d437e-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="d437e-158">Créer un Key Vault pour gérer les clés SSH pour le cluster OpenShift.</span><span class="sxs-lookup"><span data-stu-id="d437e-158">Create a KeyVault to manage SSH keys for the OpenShift cluster.</span></span>
> * <span data-ttu-id="d437e-159">Déployer un cluster OpenShift sur les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="d437e-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="d437e-160">Installer et configurer l’interface [CLI OpenShift](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) pour gérer le cluster.</span><span class="sxs-lookup"><span data-stu-id="d437e-160">Install and configure the [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) to manage the cluster.</span></span>

<span data-ttu-id="d437e-161">Maintenant que le cluster OpenShift Origin est déployé,</span><span class="sxs-lookup"><span data-stu-id="d437e-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="d437e-162">vous pouvez suivre les didacticiels OpenShift pour découvrir comment déployer votre première application et utiliser les outils OpenShift.</span><span class="sxs-lookup"><span data-stu-id="d437e-162">You can follow OpenShift tutorials to learn how to deploy your first application and use the OpenShift tools.</span></span> <span data-ttu-id="d437e-163">Pour commencer, consultez [Prise en main d’OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html).</span><span class="sxs-lookup"><span data-stu-id="d437e-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) to get started.</span></span> 
