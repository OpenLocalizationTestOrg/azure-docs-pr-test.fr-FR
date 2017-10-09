---
title: aaaDeploy un conteneur Docker de cluster dans Azure | Documents Microsoft
description: "Déployer une solution de Kubernetes, contrôleur de domaine/système d’exploitation ou Docker Swarm dans le conteneur de Service Azure à l’aide de hello portail Azure ou un modèle de gestionnaire de ressources."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Mesos, Azure, dcos, swarm, kubernetes, azure container service, acs
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a><span data-ttu-id="68b9c-104">Déployer un conteneur Docker à l’aide de hello portail Azure de solution d’hébergement</span><span class="sxs-lookup"><span data-stu-id="68b9c-104">Deploy a Docker container hosting solution using hello Azure portal</span></span>



<span data-ttu-id="68b9c-105">Azure Container Service assure le déploiement rapide des principales solutions de mise en cluster et d’orchestration de containers open source.</span><span class="sxs-lookup"><span data-stu-id="68b9c-105">Azure Container Service provides rapid deployment of popular open-source container clustering and orchestration solutions.</span></span> <span data-ttu-id="68b9c-106">Ce document vous guide dans le processus de déploiement d’un cluster de Service de conteneur Azure à l’aide de hello portail Azure ou un modèle de démarrage rapide Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="68b9c-106">This document walks you through deploying an Azure Container Service cluster by using hello Azure portal or an Azure Resource Manager quickstart template.</span></span> 

<span data-ttu-id="68b9c-107">Vous pouvez également déployer un cluster du Service de conteneur Azure à l’aide de hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) ou hello API de Service de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="68b9c-107">You can also deploy an Azure Container Service cluster by using hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="68b9c-108">Pour obtenir du contexte, consultez [Présentation d’Azure Container Service](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="68b9c-108">For background, see [Azure Container Service introduction](../container-service-intro.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="68b9c-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="68b9c-109">Prerequisites</span></span>

* <span data-ttu-id="68b9c-110">**Abonnement Azure** : si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="68b9c-110">**Azure subscription**: If you don't have one, sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> <span data-ttu-id="68b9c-111">Pour un cluster de plus grande taille, envisagez de souscrire un abonnement de paiement à l’utilisation ou d’autres options d’achat.</span><span class="sxs-lookup"><span data-stu-id="68b9c-111">For a larger cluster, consider a pay-as-you go subscription or other purchase options.</span></span>

    > [!NOTE]
    > <span data-ttu-id="68b9c-112">L’utilisation de votre abonnement Azure et [quotas ressources](../../azure-subscription-service-limits.md), telles que les quotas de cœurs, peut limiter la taille de hello du cluster hello vous déployez.</span><span class="sxs-lookup"><span data-stu-id="68b9c-112">Your Azure subscription usage and [resource quotas](../../azure-subscription-service-limits.md), such as cores quotas, can limit hello size of hello cluster you deploy.</span></span> <span data-ttu-id="68b9c-113">toorequest une augmentation du quota, ouvrir une [demande de support technique en ligne](../../azure-supportability/how-to-create-azure-support-request.md) sans frais.</span><span class="sxs-lookup"><span data-stu-id="68b9c-113">toorequest a quota increase, open an [online customer support request](../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
    >

* <span data-ttu-id="68b9c-114">**Clé publique SSH-RSA**: lors du déploiement via le portail de hello ou l’un des modèles de démarrage rapide Azure hello, vous devez clé publique de tooprovide hello pour l’authentification sur les ordinateurs virtuels du Service de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="68b9c-114">**SSH RSA public key**: When deploying through hello portal or one of hello Azure quickstart templates, you need tooprovide hello public key for authentication against Azure Container Service virtual machines.</span></span> <span data-ttu-id="68b9c-115">les clés RSA de Secure Shell (SSH) toocreate, consultez hello [OS X et Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../../virtual-machines/linux/ssh-from-windows.md) des conseils.</span><span class="sxs-lookup"><span data-stu-id="68b9c-115">toocreate Secure Shell (SSH) RSA keys, see hello [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md) guidance.</span></span> 

* <span data-ttu-id="68b9c-116">**ID client principal et le secret de service** (Kubernetes uniquement) : pour plus d’informations et des recommandations toocreate un principal du service Azure Active Directory, consultez [sur le principal du service pour un cluster Kubernetes hello](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="68b9c-116">**Service principal client ID and secret** (Kubernetes only): For more information and guidance toocreate an Azure Active Directory service principal, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>



## <a name="create-a-cluster-by-using-hello-azure-portal"></a><span data-ttu-id="68b9c-117">Créer un cluster à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="68b9c-117">Create a cluster by using hello Azure portal</span></span>
1. <span data-ttu-id="68b9c-118">Connexion toohello portail Azure, sélectionnez **nouveau**, puis recherchez hello Azure Marketplace pour **Service de conteneur Azure**.</span><span class="sxs-lookup"><span data-stu-id="68b9c-118">Sign in toohello Azure portal, select **New**, and search hello Azure Marketplace for **Azure Container Service**.</span></span>

    ![Azure Container Service dans Marketplace](./media/container-service-deployment/acs-portal1.png)  <br />

2. <span data-ttu-id="68b9c-120">Cliquez sur **Azure Container Service**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="68b9c-120">Click **Azure Container Service**, and click **Create**.</span></span>

3. <span data-ttu-id="68b9c-121">Sur hello **notions de base** panneau, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="68b9c-121">On hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="68b9c-122">**Orchestrator**: sélectionnez une des hello conteneur orchestrators toodeploy sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-122">**Orchestrator**: Select one of hello container orchestrators toodeploy on hello cluster.</span></span>
        * <span data-ttu-id="68b9c-123">**DC/OS**: déploie un cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="68b9c-123">**DC/OS**: Deploys a DC/OS cluster.</span></span>
        * <span data-ttu-id="68b9c-124">**Swarm**: déploie un cluster Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="68b9c-124">**Swarm**: Deploys a Docker Swarm cluster.</span></span>
        * <span data-ttu-id="68b9c-125">**Kubernetes** : déploie un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="68b9c-125">**Kubernetes**: Deploys a Kubernetes cluster.</span></span>
    * <span data-ttu-id="68b9c-126">**Abonnement**: sélectionnez un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="68b9c-126">**Subscription**: Select an Azure subscription.</span></span>
    * <span data-ttu-id="68b9c-127">**Groupe de ressources**: entrez le nom hello d’un nouveau groupe de ressources pour le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-127">**Resource group**: Enter hello name of a new resource group for hello deployment.</span></span>
    * <span data-ttu-id="68b9c-128">**Emplacement**: sélectionnez une région Azure pour le déploiement du Service de conteneur Azure hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-128">**Location**: Select an Azure region for hello Azure Container Service deployment.</span></span> <span data-ttu-id="68b9c-129">Pour connaître la disponibilité, consultez [Disponibilité des produits par région](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="68b9c-129">For availability, check [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
    
    ![Paramètres de base](./media/container-service-deployment/acs-portal3.png)  <br />
    
    <span data-ttu-id="68b9c-131">Cliquez sur **OK** lorsque vous êtes prêt tooproceed.</span><span class="sxs-lookup"><span data-stu-id="68b9c-131">Click **OK** when you're ready tooproceed.</span></span>

4. <span data-ttu-id="68b9c-132">Sur hello **maître configuration** panneau, entrez hello suivant les paramètres pour hello Linux maître ou les nœuds de cluster hello (certains paramètres sont spécifiques tooeach orchestrator) :</span><span class="sxs-lookup"><span data-stu-id="68b9c-132">On hello **Master configuration** blade, enter hello following settings for hello Linux master node or nodes in hello cluster (some settings are specific tooeach orchestrator):</span></span>

    * <span data-ttu-id="68b9c-133">**Nom DNS du contrôleur**: hello toocreate de préfixe utilisé un seul nom de domaine complet (FQDN) pour maître de hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-133">**Master DNS name**: hello prefix used toocreate a unique fully qualified domain name (FQDN) for hello master.</span></span> <span data-ttu-id="68b9c-134">Hello, le nom de domaine complet principal se présente sous forme de hello *préfixe*gestion*emplacement*. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="68b9c-134">hello master FQDN is of hello form *prefix*mgmt.*location*.cloudapp.azure.com.</span></span>
    * <span data-ttu-id="68b9c-135">**Nom d’utilisateur**: nom d’utilisateur hello pour un compte sur chaque hello Linux machines virtuelles hello cluster.</span><span class="sxs-lookup"><span data-stu-id="68b9c-135">**User name**: hello user name for an account on each of hello Linux virtual machines in hello cluster.</span></span>
    * <span data-ttu-id="68b9c-136">**Clé publique SSH-RSA**: ajouter hello toobe clé publique utilisée pour l’authentification sur les ordinateurs virtuels Linux hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-136">**SSH RSA public key**: Add hello public key toobe used for authentication against hello Linux virtual machines.</span></span> <span data-ttu-id="68b9c-137">Il est important que cette clé ne contient aucun saut de ligne, et il inclut hello `ssh-rsa` préfixe.</span><span class="sxs-lookup"><span data-stu-id="68b9c-137">It is important that this key contains no line breaks, and it includes hello `ssh-rsa` prefix.</span></span> <span data-ttu-id="68b9c-138">Hello `username@domain` suffixe est facultatif.</span><span class="sxs-lookup"><span data-stu-id="68b9c-138">hello `username@domain` postfix is optional.</span></span> <span data-ttu-id="68b9c-139">Hello clé doit ressembler à hello suivantes : **AAAAB3Nz ssh-rsa... <> …... UcyupgH azureuser@linuxvm** .</span><span class="sxs-lookup"><span data-stu-id="68b9c-139">hello key should look something like hello following: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span></span> 
    * <span data-ttu-id="68b9c-140">**Principal du service**: Si vous avez sélectionné orchestrator Kubernetes de hello, entrez un répertoire Azure Active Directory **ID de client principal de Service** (également appelé hello appId) et **clé secrète client principal du Service** (mot de passe).</span><span class="sxs-lookup"><span data-stu-id="68b9c-140">**Service principal**: If you selected hello Kubernetes orchestrator, enter an Azure Active Directory **Service principal client ID** (also called hello appId) and **Service principal client secret** (password).</span></span> <span data-ttu-id="68b9c-141">Pour plus d’informations, consultez [sur le principal du service pour un cluster Kubernetes hello](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="68b9c-141">For more information, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>
    * <span data-ttu-id="68b9c-142">**Maître nombre**: hello nombre de masques dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-142">**Master count**: hello number of masters in hello cluster.</span></span>
    * <span data-ttu-id="68b9c-143">**Diagnostics de machine virtuelle**: pour certains orchestrators, vous pouvez activer les diagnostics de machine virtuelle sur les maîtres hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-143">**VM diagnostics**: For some orchestrators, you can enable VM diagnostics on hello masters.</span></span>

    ![Configuration maître](./media/container-service-deployment/acs-portal4.png)  <br />

    <span data-ttu-id="68b9c-145">Cliquez sur **OK** lorsque vous êtes prêt tooproceed.</span><span class="sxs-lookup"><span data-stu-id="68b9c-145">Click **OK** when you're ready tooproceed.</span></span>

5. <span data-ttu-id="68b9c-146">Sur hello **configuration de l’Agent** panneau, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="68b9c-146">On hello **Agent configuration** blade, enter hello following information:</span></span>

    * <span data-ttu-id="68b9c-147">**Nombre d’agents**: pour Docker essaim et Kubernetes, cette valeur est le nombre initial de hello d’agents dans l’ensemble d’échelle de l’agent hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-147">**Agent count**: For Docker Swarm and Kubernetes, this value is hello initial number of agents in hello agent scale set.</span></span> <span data-ttu-id="68b9c-148">Pour le contrôleur de domaine/système d’exploitation, il est nombre initial de hello d’agents dans un ensemble d’échelle privé.</span><span class="sxs-lookup"><span data-stu-id="68b9c-148">For DC/OS, it is hello initial number of agents in a private scale set.</span></span> <span data-ttu-id="68b9c-149">En outre, un groupe identique public est créé pour DC/OS et contient un nombre prédéterminé d’agents.</span><span class="sxs-lookup"><span data-stu-id="68b9c-149">Additionally, a public scale set is created for DC/OS, which contains a predetermined number of agents.</span></span> <span data-ttu-id="68b9c-150">nombre d’agents dans cet ensemble d’échelle publique Hello est déterminé par nombre de hello de masques dans le cluster de hello : un agent public pour un maître et deux agents publics pour trois ou cinq formes de base.</span><span class="sxs-lookup"><span data-stu-id="68b9c-150">hello number of agents in this public scale set is determined by hello number of masters in hello cluster: one public agent for one master, and two public agents for three or five masters.</span></span>
    * <span data-ttu-id="68b9c-151">**Taille de machine virtuelle de l’agent**: hello taille des ordinateurs virtuels de l’agent hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-151">**Agent virtual machine size**: hello size of hello agent virtual machines.</span></span>
    * <span data-ttu-id="68b9c-152">**Système d’exploitation**: ce paramètre est actuellement disponible uniquement si vous avez sélectionné orchestrator Kubernetes de hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-152">**Operating system**: This setting is currently available only if you selected hello Kubernetes orchestrator.</span></span> <span data-ttu-id="68b9c-153">Choisissez une distribution Linux ou un toorun de système d’exploitation Windows Server sur les agents de hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-153">Choose either a Linux distribution or a Windows Server operating system toorun on hello agents.</span></span> <span data-ttu-id="68b9c-154">Ce paramètre détermine si votre cluster peut exécuter des applications de conteneur Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="68b9c-154">This setting determines whether your cluster can run Linux or Windows container apps.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="68b9c-155">La prise en charge de conteneur Windows est en version préliminaire pour les clusters Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="68b9c-155">Windows container support is in preview for Kubernetes clusters.</span></span> <span data-ttu-id="68b9c-156">Pour les clusters DC/OS et Swarm, seuls les agents Linux sont actuellement pris en charge dans Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="68b9c-156">On DC/OS and Swarm clusters, only Linux agents are currently supported in Azure Container Service.</span></span>

    * <span data-ttu-id="68b9c-157">**Informations d’identification de l’agent**: Si vous avez sélectionné le système d’exploitation de Windows hello, entrez un administrateur **nom d’utilisateur** et **mot de passe** pour l’agent hello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="68b9c-157">**Agent credentials**: If you selected hello Windows operating system, enter an administrator **User name** and **Password** for hello agent VMs.</span></span> 

    ![Configuration de l’agent](./media/container-service-deployment/acs-portal5.png)  <br />

    <span data-ttu-id="68b9c-159">Cliquez sur **OK** lorsque vous êtes prêt tooproceed.</span><span class="sxs-lookup"><span data-stu-id="68b9c-159">Click **OK** when you're ready tooproceed.</span></span>

6. <span data-ttu-id="68b9c-160">Cliquez sur **OK** une fois la validation du service terminée.</span><span class="sxs-lookup"><span data-stu-id="68b9c-160">After service validation finishes, click **OK**.</span></span>

    ![Validation](./media/container-service-deployment/acs-portal6.png)  <br />

7. <span data-ttu-id="68b9c-162">Passez en revue les termes du contrat de hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-162">Review hello terms.</span></span> <span data-ttu-id="68b9c-163">processus de déploiement toostart hello, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="68b9c-163">toostart hello deployment process, click **Create**.</span></span>

    <span data-ttu-id="68b9c-164">Si vous avez choisi toopin hello déploiement toohello portail Azure, vous pouvez voir l’état du déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-164">If you've elected toopin hello deployment toohello Azure portal, you can see hello deployment status.</span></span>

    ![état du déploiement](./media/container-service-deployment/acs-portal8.png)  <br />

<span data-ttu-id="68b9c-166">déploiement de Hello prend plusieurs minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="68b9c-166">hello deployment takes several minutes toocomplete.</span></span> <span data-ttu-id="68b9c-167">Ensuite, le cluster du Service de conteneur Azure hello est prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="68b9c-167">Then, hello Azure Container Service cluster is ready for use.</span></span>


## <a name="create-a-cluster-by-using-a-quickstart-template"></a><span data-ttu-id="68b9c-168">Créer un cluster à l’aide d’un modèle de démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="68b9c-168">Create a cluster by using a quickstart template</span></span>
<span data-ttu-id="68b9c-169">Les modèles de démarrage rapide Azure sont disponible toodeploy un cluster dans le conteneur de Service Azure.</span><span class="sxs-lookup"><span data-stu-id="68b9c-169">Azure quickstart templates are available toodeploy a cluster in Azure Container Service.</span></span> <span data-ttu-id="68b9c-170">Hello fourni des modèles de démarrage rapide peuvent être modifiée tooinclude configuration Azure supplémentaires ou avancés.</span><span class="sxs-lookup"><span data-stu-id="68b9c-170">hello provided quickstart templates can be modified tooinclude additional or advanced Azure configuration.</span></span> <span data-ttu-id="68b9c-171">toocreate un cluster du Service de conteneur Azure à l’aide d’un modèle de démarrage rapide Azure, vous devez un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="68b9c-171">toocreate an Azure Container Service cluster by using an Azure quickstart template, you need an Azure subscription.</span></span> <span data-ttu-id="68b9c-172">Si ce n’est pas le cas, inscrivez-vous dès aujourd’hui pour un [essai gratuit](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="68b9c-172">If you don't have one, then sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> 

<span data-ttu-id="68b9c-173">Suivez ces étapes toodeploy un cluster à l’aide d’un modèle et hello Azure CLI 2.0 (voir [instructions d’installation et](/cli/azure/install-az-cli2)).</span><span class="sxs-lookup"><span data-stu-id="68b9c-173">Follow these steps toodeploy a cluster using a template and hello Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span></span>

> [!NOTE] 
> <span data-ttu-id="68b9c-174">Si vous êtes sur un système Windows, vous pouvez utiliser un modèle à l’aide d’Azure PowerShell similaire toodeploy d’étapes.</span><span class="sxs-lookup"><span data-stu-id="68b9c-174">If you're on a Windows system, you can use similar steps toodeploy a template using Azure PowerShell.</span></span> <span data-ttu-id="68b9c-175">Consultez les étapes plus loin dans cette section.</span><span class="sxs-lookup"><span data-stu-id="68b9c-175">See steps later in this section.</span></span> <span data-ttu-id="68b9c-176">Vous pouvez également déployer un modèle de par Bonjour [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) ou d’autres méthodes.</span><span class="sxs-lookup"><span data-stu-id="68b9c-176">You can also deploy a template through hello [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) or other methods.</span></span>

1. <span data-ttu-id="68b9c-177">toodeploy un contrôleur de domaine/système d’exploitation, Docker Swarm ou Kubernetes du cluster, sélectionnez un des modèles de démarrage rapide disponible hello à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="68b9c-177">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="68b9c-178">Une liste partielle s’affiche.</span><span class="sxs-lookup"><span data-stu-id="68b9c-178">A partial list follows.</span></span> <span data-ttu-id="68b9c-179">Hello contrôleur de domaine/système d’exploitation et les modèles essaim sont hello même, à l’exception de sélection d’orchestrator hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="68b9c-179">hello DC/OS and Swarm templates are hello same, except for hello default orchestrator selection.</span></span>

    * [<span data-ttu-id="68b9c-180">Modèle DC/OS</span><span class="sxs-lookup"><span data-stu-id="68b9c-180">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="68b9c-181">Modèle Swarm</span><span class="sxs-lookup"><span data-stu-id="68b9c-181">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="68b9c-182">Modèle Kubernetes</span><span class="sxs-lookup"><span data-stu-id="68b9c-182">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="68b9c-183">Connectez-vous à tooyour compte Azure (`az login`) et assurez-vous que hello CLI d’Azure est connecté tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="68b9c-183">Log in tooyour Azure account (`az login`), and make sure that hello Azure CLI is connected tooyour Azure subscription.</span></span> <span data-ttu-id="68b9c-184">Vous pouvez voir l’abonnement de hello par défaut à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="68b9c-184">You can see hello default subscription by using hello following command:</span></span>

    ```azurecli
    az account show
    ```
    
    <span data-ttu-id="68b9c-185">Si vous avez plusieurs tooset d’abonnement et d’avoir un abonnement par défaut différent, exécutez `az account set --subscription` et spécifiez le nom ou ID d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-185">If you have more than one subscription and need tooset a different default subscription, run `az account set --subscription` and specify hello subscription ID or name.</span></span>

3. <span data-ttu-id="68b9c-186">Comme meilleure pratique, utilisez un groupe de ressources pour le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-186">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="68b9c-187">toocreate un groupe de ressources, utilisez hello `az group create` commande spécifie un nom de groupe de ressources et l’emplacement :</span><span class="sxs-lookup"><span data-stu-id="68b9c-187">toocreate a resource group, use hello `az group create` command specify a resource group name and location:</span></span> 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. <span data-ttu-id="68b9c-188">Créer un modèle requis hello de conteneur fichier JSON de paramètres.</span><span class="sxs-lookup"><span data-stu-id="68b9c-188">Create a JSON file containing hello required template parameters.</span></span> <span data-ttu-id="68b9c-189">Fichier de paramètres hello téléchargement nommé `azuredeploy.parameters.json` qui accompagne le modèle de Service de conteneur Azure hello `azuredeploy.json` dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="68b9c-189">Download hello parameters file named `azuredeploy.parameters.json` that accompanies hello Azure Container Service template `azuredeploy.json` in GitHub.</span></span> <span data-ttu-id="68b9c-190">Entrez les valeurs de paramètre requises pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="68b9c-190">Enter required parameter values for your cluster.</span></span> 

    <span data-ttu-id="68b9c-191">Par exemple, toouse hello [modèle de contrôleur de domaine/système d’exploitation](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), fournir des valeurs de paramètre pour `dnsNamePrefix` et `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="68b9c-191">For example, toouse hello [DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), supply parameter values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="68b9c-192">Consultez les descriptions de hello dans `azuredeploy.json` et options pour les autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="68b9c-192">See hello descriptions in `azuredeploy.json` and options for other parameters.</span></span>  
 

5. <span data-ttu-id="68b9c-193">Créer un cluster du Service de conteneur en transmettant le fichier de paramètres de déploiement hello avec hello suivant de commande, où :</span><span class="sxs-lookup"><span data-stu-id="68b9c-193">Create a Container Service cluster by passing hello deployment parameters file with hello following command, where:</span></span>

    * <span data-ttu-id="68b9c-194">**RESOURCE_GROUP** est le nom hello hello du groupe de ressources que vous avez créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-194">**RESOURCE_GROUP** is hello name of hello resource group that you created in hello previous step.</span></span>
    * <span data-ttu-id="68b9c-195">**DEPLOYMENT_NAME** (facultatif) est un nom que vous donnez toohello déploiement.</span><span class="sxs-lookup"><span data-stu-id="68b9c-195">**DEPLOYMENT_NAME** (optional) is a name you give toohello deployment.</span></span>
    * <span data-ttu-id="68b9c-196">**TEMPLATE_URI** est l’emplacement de hello du fichier de déploiement hello `azuredeploy.json`.</span><span class="sxs-lookup"><span data-stu-id="68b9c-196">**TEMPLATE_URI** is hello location of hello deployment file `azuredeploy.json`.</span></span> <span data-ttu-id="68b9c-197">Cet URI doit être le fichier brut hello, pas un toohello pointeur GitHub UI.</span><span class="sxs-lookup"><span data-stu-id="68b9c-197">This URI must be hello Raw file, not a pointer toohello GitHub UI.</span></span> <span data-ttu-id="68b9c-198">toofind cet URI, sélectionnez hello `azuredeploy.json` fichier dans GitHub, puis cliquez sur hello **Raw** bouton.</span><span class="sxs-lookup"><span data-stu-id="68b9c-198">toofind this URI, select hello `azuredeploy.json` file in GitHub, and click hello **Raw** button.</span></span>  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    <span data-ttu-id="68b9c-199">Vous pouvez également fournir des paramètres sous forme de chaîne au format JSON sur la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-199">You can also provide parameters as a JSON-formatted string on hello command line.</span></span> <span data-ttu-id="68b9c-200">Utilisez un commande similaire toohello qui suit :</span><span class="sxs-lookup"><span data-stu-id="68b9c-200">Use a command similar toohello following:</span></span>

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > <span data-ttu-id="68b9c-201">déploiement de Hello prend plusieurs minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="68b9c-201">hello deployment takes several minutes toocomplete.</span></span>
    > 

### <a name="equivalent-powershell-commands"></a><span data-ttu-id="68b9c-202">Commandes PowerShell équivalentes</span><span class="sxs-lookup"><span data-stu-id="68b9c-202">Equivalent PowerShell commands</span></span>
<span data-ttu-id="68b9c-203">Vous pouvez également déployer un modèle de cluster Azure Container Service avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="68b9c-203">You can also deploy an Azure Container Service cluster template with PowerShell.</span></span> <span data-ttu-id="68b9c-204">Ce document est basé sur la version 1.0 du hello [module Azure PowerShell](https://azure.microsoft.com/blog/azps-1-0/).</span><span class="sxs-lookup"><span data-stu-id="68b9c-204">This document is based on hello version 1.0 [Azure PowerShell module](https://azure.microsoft.com/blog/azps-1-0/).</span></span>

1. <span data-ttu-id="68b9c-205">toodeploy un contrôleur de domaine/système d’exploitation, Docker Swarm ou Kubernetes du cluster, sélectionnez un des modèles de démarrage rapide disponible hello à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="68b9c-205">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="68b9c-206">Une liste partielle s’affiche.</span><span class="sxs-lookup"><span data-stu-id="68b9c-206">A partial list follows.</span></span> <span data-ttu-id="68b9c-207">Notez que le hello contrôleur de domaine/système d’exploitation et les modèles essaim sont hello à identiques, à l’exception de hello de sélection d’orchestrator hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="68b9c-207">Note that hello DC/OS and Swarm templates are hello same, with hello exception of hello default orchestrator selection.</span></span>

    * [<span data-ttu-id="68b9c-208">Modèle DC/OS</span><span class="sxs-lookup"><span data-stu-id="68b9c-208">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="68b9c-209">Modèle Swarm</span><span class="sxs-lookup"><span data-stu-id="68b9c-209">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="68b9c-210">Modèle Kubernetes</span><span class="sxs-lookup"><span data-stu-id="68b9c-210">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="68b9c-211">Avant de créer un cluster dans votre abonnement Azure, vérifiez que votre session PowerShell a été signée dans tooAzure.</span><span class="sxs-lookup"><span data-stu-id="68b9c-211">Before creating a cluster in your Azure subscription, verify that your PowerShell session has been signed in tooAzure.</span></span> <span data-ttu-id="68b9c-212">Cela avec hello `Get-AzureRMSubscription` commande :</span><span class="sxs-lookup"><span data-stu-id="68b9c-212">You can do this with hello `Get-AzureRMSubscription` command:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="68b9c-213">Si vous devez toosign dans tooAzure, utilisez hello `Login-AzureRMAccount` commande :</span><span class="sxs-lookup"><span data-stu-id="68b9c-213">If you need toosign in tooAzure, use hello `Login-AzureRMAccount` command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

4. <span data-ttu-id="68b9c-214">Comme meilleure pratique, utilisez un groupe de ressources pour le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-214">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="68b9c-215">toocreate un groupe de ressources, utilisez hello `New-AzureRmResourceGroup` de commandes et spécifier une région de nom et la destination groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="68b9c-215">toocreate a resource group, use hello `New-AzureRmResourceGroup` command, and specify a resource group name and destination region:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. <span data-ttu-id="68b9c-216">Après avoir créé un groupe de ressources, vous pouvez créer votre cluster avec hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="68b9c-216">After you create a resource group, you can create your cluster with hello following command.</span></span> <span data-ttu-id="68b9c-217">Hello URI Hello souhaité template est spécifié avec hello `-TemplateUri` paramètre.</span><span class="sxs-lookup"><span data-stu-id="68b9c-217">hello URI of hello desired template is specified with hello `-TemplateUri` parameter.</span></span> <span data-ttu-id="68b9c-218">Lorsque vous exécutez cette commande, PowerShell vous invite à saisir les valeurs des paramètres de déploiement.</span><span class="sxs-lookup"><span data-stu-id="68b9c-218">When you run this command, PowerShell prompts you for deployment parameter values.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a><span data-ttu-id="68b9c-219">Indication des paramètres du modèle</span><span class="sxs-lookup"><span data-stu-id="68b9c-219">Provide template parameters</span></span>
<span data-ttu-id="68b9c-220">Si vous êtes familiarisé avec PowerShell, vous savez que vous pouvez passer en revue les paramètres disponibles de hello pour une applet de commande en tapant un signe moins (-) et en appuyant sur la touche TAB. hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-220">If you're familiar with PowerShell, you know that you can cycle through hello available parameters for a cmdlet by typing a minus sign (-) and then pressing hello TAB key.</span></span> <span data-ttu-id="68b9c-221">Cette fonctionnalité fonctionne également avec les paramètres que vous définissez dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="68b9c-221">This same functionality also works with parameters that you define in your template.</span></span> <span data-ttu-id="68b9c-222">Dès que vous tapez le nom du modèle hello, applet de commande hello extrait le modèle de hello, analyse hello paramètres et ajoute hello modèle paramètres toohello commande dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="68b9c-222">As soon as you type hello template name, hello cmdlet fetches hello template, parses hello parameters, and adds hello template parameters toohello command dynamically.</span></span> <span data-ttu-id="68b9c-223">Cela permet de valeurs de paramètre de modèle simple toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-223">This makes it easy toospecify hello template parameter values.</span></span> <span data-ttu-id="68b9c-224">Et, si vous oubliez d’une valeur de paramètre obligatoire, PowerShell vous invite à valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-224">And, if you forget a required parameter value, PowerShell prompts you for hello value.</span></span>

<span data-ttu-id="68b9c-225">Voici la commande hello complète, avec des paramètres inclus.</span><span class="sxs-lookup"><span data-stu-id="68b9c-225">Here is hello full command, with parameters included.</span></span> <span data-ttu-id="68b9c-226">Fournissez vos propres valeurs pour les noms des ressources de hello hello.</span><span class="sxs-lookup"><span data-stu-id="68b9c-226">Provide your own values for hello names of hello resources.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a><span data-ttu-id="68b9c-227">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="68b9c-227">Next steps</span></span>
<span data-ttu-id="68b9c-228">À présent que vous disposez d’un cluster opérationnel, consultez les documents suivants pour obtenir des informations supplémentaires concernant la connexion et la gestion du cluster :</span><span class="sxs-lookup"><span data-stu-id="68b9c-228">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="68b9c-229">Connecter le cluster du Service de conteneur Azure tooan</span><span class="sxs-lookup"><span data-stu-id="68b9c-229">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="68b9c-230">Gestion de conteneur via l’API REST</span><span class="sxs-lookup"><span data-stu-id="68b9c-230">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="68b9c-231">Gestion des conteneurs avec Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="68b9c-231">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="68b9c-232">Gestion des conteneurs avec Kubernetes</span><span class="sxs-lookup"><span data-stu-id="68b9c-232">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)
