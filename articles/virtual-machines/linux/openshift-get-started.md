---
title: aaaDeploy OpenShift origine tooAzure | Documents Microsoft
description: "Découvrez les machines virtuelles de toodeploy OpenShift origine tooAzure."
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
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a><span data-ttu-id="13032-103">Déployer OpenShift origine tooAzure Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="13032-103">Deploy OpenShift Origin tooAzure Virtual Machines</span></span> 

<span data-ttu-id="13032-104">[OpenShift Origin](https://www.openshift.org/) est une plateforme de conteneurs open source basée sur [Kubernetes](https://kubernetes.io/).</span><span class="sxs-lookup"><span data-stu-id="13032-104">[OpenShift Origin](https://www.openshift.org/) is an open source container platform built on [Kubernetes](https://kubernetes.io/).</span></span> <span data-ttu-id="13032-105">Il simplifie hello déploiement, mise à l’échelle et l’exploitation des applications mutualisées.</span><span class="sxs-lookup"><span data-stu-id="13032-105">It simplifies hello process of deploying, scaling, and operating multi-tenant applications.</span></span> 

<span data-ttu-id="13032-106">Ce guide décrit comment toodeploy OpenShift origine sur l’utilisation de Machines virtuelles Azure hello CLI d’Azure et les modèles du Gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="13032-106">This guide describes how toodeploy OpenShift Origin on Azure Virtual Machines using hello Azure CLI and Azure Resource Manager Templates.</span></span> <span data-ttu-id="13032-107">Ce didacticiel vous explique comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="13032-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="13032-108">Créer un toomanage KeyVault clés SSH pour le cluster de OpenShift hello.</span><span class="sxs-lookup"><span data-stu-id="13032-108">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="13032-109">Déployer un cluster OpenShift sur les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="13032-109">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="13032-110">Installer et configurer hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) cluster hello de toomanage.</span><span class="sxs-lookup"><span data-stu-id="13032-110">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>
> * <span data-ttu-id="13032-111">Personnalisez le déploiement de OpenShift hello.</span><span class="sxs-lookup"><span data-stu-id="13032-111">Customize hello OpenShift deployment.</span></span>

<span data-ttu-id="13032-112">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="13032-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="13032-113">Ce démarrage rapide nécessite hello CLI d’Azure version 2.0.8 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="13032-113">This quick start requires hello Azure CLI version 2.0.8 or later.</span></span> <span data-ttu-id="13032-114">version de hello toofind, exécutez `az --version`.</span><span class="sxs-lookup"><span data-stu-id="13032-114">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="13032-115">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="13032-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="13032-116">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="13032-116">Log in tooAzure</span></span> 
<span data-ttu-id="13032-117">Connectez-vous tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran ou cliquez sur **essayez-la** toouse Shell de Cloud.</span><span class="sxs-lookup"><span data-stu-id="13032-117">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions or click **Try it** toouse Cloud Shell.</span></span>

```azurecli 
az login
```
## <a name="create-a-resource-group"></a><span data-ttu-id="13032-118">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="13032-118">Create a resource group</span></span>

<span data-ttu-id="13032-119">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="13032-119">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="13032-120">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="13032-120">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="13032-121">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.</span><span class="sxs-lookup"><span data-stu-id="13032-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="13032-122">Créer un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="13032-122">Create a Key Vault</span></span>
<span data-ttu-id="13032-123">Créer des clés SSH pour le cluster de hello un Bonjour de toostore KeyVault avec hello [az keyvault créer](/cli/azure/keyvault#create) commande.</span><span class="sxs-lookup"><span data-stu-id="13032-123">Create a KeyVault toostore hello SSH keys for hello cluster with hello [az keyvault create](/cli/azure/keyvault#create) command.</span></span>  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a><span data-ttu-id="13032-124">Création d’une clé SSH</span><span class="sxs-lookup"><span data-stu-id="13032-124">Create an SSH key</span></span> 
<span data-ttu-id="13032-125">Une clé SSH n’est nécessaire toosecure accès toohello cluster d’origine de OpenShift.</span><span class="sxs-lookup"><span data-stu-id="13032-125">An SSH key is needed toosecure access toohello OpenShift Origin cluster.</span></span> <span data-ttu-id="13032-126">Créer une paire de clés SSH à l’aide de hello `ssh-keygen` commande.</span><span class="sxs-lookup"><span data-stu-id="13032-126">Create an SSH key-pair using hello `ssh-keygen` command.</span></span> 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> <span data-ttu-id="13032-127">Hello paire de clés SSH vous créez ne doit pas avoir un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="13032-127">hello SSH key pair you create must not have a passphrase.</span></span>

<span data-ttu-id="13032-128">Pour plus d’informations sur les clés SSH sur Windows, [comment toocreate SSH clés sur Windows](/azure/virtual-machines/linux/ssh-from-windows).</span><span class="sxs-lookup"><span data-stu-id="13032-128">For more information on SSH keys on Windows, [How toocreate SSH keys on Windows](/azure/virtual-machines/linux/ssh-from-windows).</span></span>

## <a name="store-ssh-private-key-in-key-vault"></a><span data-ttu-id="13032-129">Stocker la clé privée SSH dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="13032-129">Store SSH private key in Key Vault</span></span>
<span data-ttu-id="13032-130">Hello OpenShift déploiement utilise la clé SSH hello vous avez créé à l’accès toosecure toohello OpenShift master.</span><span class="sxs-lookup"><span data-stu-id="13032-130">hello OpenShift deployment uses hello SSH key you created toosecure access toohello OpenShift master.</span></span> <span data-ttu-id="13032-131">tooenable hello déploiement toosecurely de récupérer la clé SSH hello, stocker la clé de hello dans le coffre de clés à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="13032-131">tooenable hello deployment toosecurely retrieve hello SSH key, store hello key in Key Vault using hello following command.</span></span>

# <a name="enabled-for-template-deployment"></a><span data-ttu-id="13032-132">Activé pour le déploiement de modèle</span><span class="sxs-lookup"><span data-stu-id="13032-132">Enabled for template deployment</span></span>
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a><span data-ttu-id="13032-133">Créer un principal du service</span><span class="sxs-lookup"><span data-stu-id="13032-133">Create a service principal</span></span> 
<span data-ttu-id="13032-134">OpenShift communique avec Azure à l’aide d’un nom d’utilisateur et d’un mot de passe ou d’un principal de service.</span><span class="sxs-lookup"><span data-stu-id="13032-134">OpenShift communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="13032-135">Un principal de service Azure est une identité de sécurité que vous pouvez utiliser avec des applications, des services et des outils d’automatisation comme OpenShift.</span><span class="sxs-lookup"><span data-stu-id="13032-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like OpenShift.</span></span> <span data-ttu-id="13032-136">Contrôler et de définir des autorisations de hello comme principal du service hello toowhat opérations réalisables dans Azure.</span><span class="sxs-lookup"><span data-stu-id="13032-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="13032-137">sécurité tooimprove simplement en fournissant un nom d’utilisateur et un mot de passe, cet exemple crée un service de base principale.</span><span class="sxs-lookup"><span data-stu-id="13032-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="13032-138">Créer un service principal avec [az ad sp créer-de-rbac](/cli/azure/ad/sp#create-for-rbac) et informations d’identification de hello sortie OpenShift doit :</span><span class="sxs-lookup"><span data-stu-id="13032-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that OpenShift needs:</span></span>

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
<span data-ttu-id="13032-139">Prenez note de la propriété d’appId hello retournée à partir de la commande hello.</span><span class="sxs-lookup"><span data-stu-id="13032-139">Take note of hello appId property returned from hello command.</span></span>
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
 > <span data-ttu-id="13032-140">Ne créez pas un mot de passe non sécurisé.</span><span class="sxs-lookup"><span data-stu-id="13032-140">Don't create an insecure password.</span></span>  <span data-ttu-id="13032-141">Suivez les conseils en matière de [Stratégies et restrictions de mot de passe dans Azure Active Directory](/azure/active-directory/active-directory-passwords-policy).</span><span class="sxs-lookup"><span data-stu-id="13032-141">Follow the [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) guidance.</span></span>

<span data-ttu-id="13032-142">Pour plus d’informations sur les principaux de service, consultez [Créer un principal du service avec Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="13032-142">For more information on service principals, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

## <a name="deploy-hello-openshift-origin-template"></a><span data-ttu-id="13032-143">Déployer hello modèle d’origine de OpenShift</span><span class="sxs-lookup"><span data-stu-id="13032-143">Deploy hello OpenShift Origin template</span></span>
<span data-ttu-id="13032-144">Vous allez maintenant déployer OpenShift Origin à l’aide d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="13032-144">Next deploy OpenShift Origin using an Azure Resource Manager template.</span></span> 

> [!NOTE] 
> <span data-ttu-id="13032-145">commande suivante Hello requiert az CLI 2.0.8 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="13032-145">hello following command requires az CLI 2.0.8 or later.</span></span> <span data-ttu-id="13032-146">Vous pouvez vérifier hello az CLI version avec hello `az --version` commande.</span><span class="sxs-lookup"><span data-stu-id="13032-146">You can verify hello az CLI version with hello `az --version` command.</span></span> <span data-ttu-id="13032-147">tooupdate hello version CLI, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="13032-147">tooupdate hello CLI version, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="13032-148">Hello d’utilisation `appId` valeur à partir de principal du service hello créé précédemment pour hello `aadClientId` paramètre.</span><span class="sxs-lookup"><span data-stu-id="13032-148">Use hello `appId` value from hello service principal you created earlier for hello `aadClientId` parameter.</span></span>

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
<span data-ttu-id="13032-149">déploiement de Hello peut prendre jusqu'à too20 minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="13032-149">hello deployment may take up too20 minutes toocomplete.</span></span> <span data-ttu-id="13032-150">Hello URL de console de OpenShift hello et le nom DNS de hello OpenShift maître est imprimé toohello terminal lorsque hello déploiement est terminé.</span><span class="sxs-lookup"><span data-stu-id="13032-150">hello URL of hello OpenShift console and DNS name of hello OpenShift master is printed toohello terminal when hello deployment completes.</span></span>

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a><span data-ttu-id="13032-151">Se connecter toohello OpenShift cluster</span><span class="sxs-lookup"><span data-stu-id="13032-151">Connect toohello OpenShift cluster</span></span>
<span data-ttu-id="13032-152">Lorsque hello déploiement terminé, connecter la console de OpenShift toohello à l’aide du navigateur hello à l’aide de hello `OpenShift Console Uri`.</span><span class="sxs-lookup"><span data-stu-id="13032-152">When hello deployment completes, connect toohello OpenShift console using hello browser using hello `OpenShift Console Uri`.</span></span> <span data-ttu-id="13032-153">Ou bien, vous pouvez vous connecter principale de OpenShift toohello à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="13032-153">Alternatively, you can connect toohello OpenShift master using hello following command.</span></span>

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a><span data-ttu-id="13032-154">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="13032-154">Clean up resources</span></span>
<span data-ttu-id="13032-155">Lorsque vous n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, OpenShift cluster et toutes les ressources de la commande.</span><span class="sxs-lookup"><span data-stu-id="13032-155">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, OpenShift cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="13032-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="13032-156">Next steps</span></span>

<span data-ttu-id="13032-157">Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="13032-157">In this tutorial, learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="13032-158">Créer un toomanage KeyVault clés SSH pour le cluster de OpenShift hello.</span><span class="sxs-lookup"><span data-stu-id="13032-158">Create a KeyVault toomanage SSH keys for hello OpenShift cluster.</span></span>
> * <span data-ttu-id="13032-159">Déployer un cluster OpenShift sur les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="13032-159">Deploy an OpenShift cluster on Azure VMs.</span></span> 
> * <span data-ttu-id="13032-160">Installer et configurer hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) cluster hello de toomanage.</span><span class="sxs-lookup"><span data-stu-id="13032-160">Install and configure hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage hello cluster.</span></span>

<span data-ttu-id="13032-161">Maintenant que le cluster OpenShift Origin est déployé,</span><span class="sxs-lookup"><span data-stu-id="13032-161">Now that OpenShift Origin cluster is deployed.</span></span> <span data-ttu-id="13032-162">Vous pouvez suivre comment OpenShift didacticiels toolearn toodeploy votre première application et utilisez hello OpenShift outils.</span><span class="sxs-lookup"><span data-stu-id="13032-162">You can follow OpenShift tutorials toolearn how toodeploy your first application and use hello OpenShift tools.</span></span> <span data-ttu-id="13032-163">Consultez [prise en main d’origine de OpenShift](https://docs.openshift.org/latest/getting_started/index.html) tooget a démarré.</span><span class="sxs-lookup"><span data-stu-id="13032-163">See [Getting Started with OpenShift Origin](https://docs.openshift.org/latest/getting_started/index.html) tooget started.</span></span> 
