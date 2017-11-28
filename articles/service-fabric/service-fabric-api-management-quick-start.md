---
title: "aaaAzure Service Fabric avec le démarrage rapide de gestion des API | Documents Microsoft"
description: "Ce guide vous explique comment démarrer avec l’API de gestion et Azure Service Fabric tooquickly."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="384a1-103">Azure Service Fabric avec Gestion des API - Démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="384a1-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="384a1-104">Ce guide vous explique comment tooset jusqu'à la gestion des API Azure avec l’infrastructure de Service et configurer des votre première API opération toosend trafic tooback services en Service fabric.</span><span class="sxs-lookup"><span data-stu-id="384a1-104">This guide shows you how tooset up Azure API Management with Service Fabric and configure your first API operation toosend traffic tooback-end services in Service Fabric.</span></span> <span data-ttu-id="384a1-105">toolearn en savoir plus sur les scénarios de gestion des API Azure avec l’infrastructure de Service, consultez hello [vue d’ensemble](service-fabric-api-management-overview.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="384a1-105">toolearn more about Azure API Management scenarios with Service Fabric, see hello [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a><span data-ttu-id="384a1-106">Déployer tooAzure gestion des API et le Service Fabric</span><span class="sxs-lookup"><span data-stu-id="384a1-106">Deploy API Management and Service Fabric tooAzure</span></span>

<span data-ttu-id="384a1-107">première étape de Hello est toodeploy gestion des API et un tooAzure de cluster Service Fabric dans un réseau virtuel partagé.</span><span class="sxs-lookup"><span data-stu-id="384a1-107">hello first step is toodeploy API Management and a Service Fabric cluster tooAzure in a shared Virtual Network.</span></span> <span data-ttu-id="384a1-108">Cela permet de toocommunicate de gestion des API directement avec l’infrastructure de Service afin d’exécuter découverte de service, la résolution de partition de service et transférer le trafic directement tooany principal de service Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="384a1-108">This allows API Management toocommunicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly tooany backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="384a1-109">Topologie</span><span class="sxs-lookup"><span data-stu-id="384a1-109">Topology</span></span>

<span data-ttu-id="384a1-110">Ce guide déploie suivant de hello tooAzure de topologie dans lequel l’infrastructure de Service et de gestion des API se trouvent dans des sous-réseaux de hello même réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="384a1-110">This guide deploys hello following topology tooAzure in which API Management and Service Fabric are in subnets of hello same Virtual Network:</span></span>

 ![Légende de l’image][sf-apim-topology-overview]

<span data-ttu-id="384a1-112">tooget démarrer rapidement, les modèles du Gestionnaire de ressources sont fournis pour chaque étape du déploiement :</span><span class="sxs-lookup"><span data-stu-id="384a1-112">tooget started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="384a1-113">Topologie du réseau :</span><span class="sxs-lookup"><span data-stu-id="384a1-113">Network topology:</span></span>
    - <span data-ttu-id="384a1-114">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="384a1-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="384a1-115">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="384a1-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="384a1-116">Cluster Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="384a1-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="384a1-117">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="384a1-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="384a1-118">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="384a1-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="384a1-119">Gestion des API :</span><span class="sxs-lookup"><span data-stu-id="384a1-119">API Management:</span></span>
    - <span data-ttu-id="384a1-120">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="384a1-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="384a1-121">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="384a1-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-tooazure-and-select-your-subscription"></a><span data-ttu-id="384a1-122">Connectez-vous à tooAzure et sélectionnez votre abonnement</span><span class="sxs-lookup"><span data-stu-id="384a1-122">Sign in tooAzure and select your subscription</span></span>

<span data-ttu-id="384a1-123">Ce guide utilise [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="384a1-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="384a1-124">Lorsque vous démarrez une nouvelle session PowerShell, connectez-vous à tooyour compte Azure, puis sélectionnez votre abonnement avant d’exécuter des commandes Azure.</span><span class="sxs-lookup"><span data-stu-id="384a1-124">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="384a1-125">La connexion tooyour compte Azure :</span><span class="sxs-lookup"><span data-stu-id="384a1-125">Sign in tooyour Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="384a1-126">Sélectionnez votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="384a1-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="384a1-127">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="384a1-127">Create a resource group</span></span>

<span data-ttu-id="384a1-128">Créez un groupe de ressources pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="384a1-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="384a1-129">Attribuez-lui un nom et un emplacement.</span><span class="sxs-lookup"><span data-stu-id="384a1-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a><span data-ttu-id="384a1-130">Déployer la topologie du réseau hello</span><span class="sxs-lookup"><span data-stu-id="384a1-130">Deploy hello network topology</span></span>

<span data-ttu-id="384a1-131">Hello première étape consiste tooset des toowhich de topologie réseau hello gestion des API et cluster Service Fabric de hello sera déployé.</span><span class="sxs-lookup"><span data-stu-id="384a1-131">hello first step is tooset up hello network topology toowhich API Management and hello Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="384a1-132">Hello [network.json] [ network-arm] modèle du Gestionnaire de ressources est toocreate configuré un réseau virtuel (VNET) avec deux sous-réseaux et les deux groupes de sécurité réseau (NSG).</span><span class="sxs-lookup"><span data-stu-id="384a1-132">hello [network.json][network-arm] Resource Manager template is configured toocreate a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="384a1-133">Hello [network.parameters.json] [ network-parameters-arm] fichier de paramètres contient des noms de hello des sous-réseaux de hello et des groupes de sécurité réseau gestion des API et l’infrastructure de Service seront déployé.</span><span class="sxs-lookup"><span data-stu-id="384a1-133">hello [network.parameters.json][network-parameters-arm] parameters file contains hello names of hello subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="384a1-134">Dans ce guide, les valeurs de paramètre hello n’avez pas besoin toobe modifié.</span><span class="sxs-lookup"><span data-stu-id="384a1-134">For this guide, hello parameter values do not need toobe changed.</span></span> <span data-ttu-id="384a1-135">modèles de gestion des API et le Gestionnaire de ressources de l’infrastructure de Service Hello utilisent ces valeurs, afin de s’ils sont modifiés ici, vous devez modifier dans hello en conséquence les autres modèles de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="384a1-135">hello API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in hello other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="384a1-136">Vous pouvez télécharger hello suivant du fichier de modèle et les paramètres du Gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="384a1-136">Download hello following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="384a1-137">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="384a1-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="384a1-138">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="384a1-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="384a1-139">Utilisez hello suivant PowerShell commande toodeploy hello Gestionnaire de ressources du modèle de fichiers et de paramètres pour le programme d’installation de hello réseau :</span><span class="sxs-lookup"><span data-stu-id="384a1-139">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for hello network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a><span data-ttu-id="384a1-140">Déployer le cluster Service Fabric de hello</span><span class="sxs-lookup"><span data-stu-id="384a1-140">Deploy hello Service Fabric cluster</span></span>

<span data-ttu-id="384a1-141">Une fois que les ressources du réseau hello ont terminé le déploiement, étape suivante de hello est toodeploy un toohello de cluster Service Fabric réseau virtuel dans un sous-réseau de hello et désigné par groupe de sécurité réseau pour le cluster Service Fabric de hello.</span><span class="sxs-lookup"><span data-stu-id="384a1-141">Once hello network resources have finished deploying, hello next step is toodeploy a Service Fabric cluster toohello VNET in hello subnet and NSG designated for hello Service Fabric cluster.</span></span> <span data-ttu-id="384a1-142">Pour ce didacticiel, modèle de gestionnaire de ressources de l’infrastructure de Service hello est préconfigurée de manière toouse les noms de hello hello réseau virtuel, sous-réseau et groupe de sécurité réseau que vous avez configurée à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="384a1-142">For this tutorial, hello Service Fabric Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

<span data-ttu-id="384a1-143">modèle de gestionnaire de ressources de cluster de Service Fabric Hello est toocreate configuré un cluster sécurisé avec la sécurité du certificat.</span><span class="sxs-lookup"><span data-stu-id="384a1-143">hello Service Fabric cluster Resource Manager template is configured toocreate a secure cluster with certificate security.</span></span> <span data-ttu-id="384a1-144">certificat de Hello est communication de nœud à nœud toosecure utilisé pour votre cluster et le cluster Service Fabric de toomanage utilisateur accès tooyour.</span><span class="sxs-lookup"><span data-stu-id="384a1-144">hello certificate is used toosecure node-to-node communication for your cluster and toomanage user access tooyour Service Fabric cluster.</span></span> <span data-ttu-id="384a1-145">Gestion des API utilise cette hello tooaccess de certificat l’infrastructure de Service d’affectation de noms de Service pour la découverte de service.</span><span class="sxs-lookup"><span data-stu-id="384a1-145">API Management uses this certificate tooaccess  hello Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="384a1-146">Cette étape nécessite de disposer d’un certificat de sécurité du cluster dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="384a1-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="384a1-147">Pour plus d’informations sur la configuration d’un cluster sécurisé avec le coffre de clés, consultez [ce guide sur la création d’un cluster dans Azure à l’aide de Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="384a1-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="384a1-148">Vous pouvez ajouter l’authentification Azure Active Directory dans Ajout toohello certificat est utilisé pour l’accès au cluster.</span><span class="sxs-lookup"><span data-stu-id="384a1-148">You may add Azure Active Directory authentication in addition toohello certificate used for cluster access.</span></span> <span data-ttu-id="384a1-149">Azure Active Directory est hello recommandé cluster Service Fabric de façon toomanage utilisateur accès tooyour, mais n’est pas nécessaire toocomplete ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="384a1-149">Azure Active Directory is hello recommended way toomanage user access tooyour Service Fabric cluster, but is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="384a1-150">Un certificat est requis dans les deux cas pour la sécurité nœud à nœud du cluster et pour l’authentification de Gestion des API Azure, qui ne prend pas actuellement en charge l’authentification avec Azure Active Directory pour un principal de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="384a1-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="384a1-151">Vous pouvez télécharger hello suivant du fichier de modèle et les paramètres du Gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="384a1-151">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="384a1-152">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="384a1-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="384a1-153">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="384a1-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="384a1-154">Renseignez les paramètres vide hello hello `cluster.parameters.json` fichier pour votre déploiement, y compris hello [les informations de coffre de clés](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) pour votre certificat de cluster.</span><span class="sxs-lookup"><span data-stu-id="384a1-154">Fill in hello empty parameters in hello `cluster.parameters.json` file for your deployment, including hello [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="384a1-155">Utilisez hello suivant PowerShell commande toodeploy hello Gestionnaire de ressources du modèle et le paramètre fichiers toocreate hello cluster Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="384a1-155">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files toocreate hello Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="384a1-156">Déploiement de Gestion des API</span><span class="sxs-lookup"><span data-stu-id="384a1-156">Deploy API Management</span></span>

<span data-ttu-id="384a1-157">Enfin, déployez toohello de gestion des API réseau virtuel dans un sous-réseau de hello et NSG désigné pour la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="384a1-157">Finally, deploy API Management toohello VNET in hello subnet and NSG designated for API Management.</span></span> <span data-ttu-id="384a1-158">Il est inutile toowait pour toofinish de déploiement de cluster de Service Fabric hello avant de déployer la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="384a1-158">You do not need toowait for hello Service Fabric cluster deployment toofinish before deploying API Management.</span></span> 

<span data-ttu-id="384a1-159">Pour ce didacticiel, modèle de gestionnaire de ressources de gestion des API hello est préconfigurée de manière toouse les noms de hello hello réseau virtuel, sous-réseau et groupe de sécurité réseau que vous avez configurée à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="384a1-159">For this tutorial, hello API Management Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

 1. <span data-ttu-id="384a1-160">Vous pouvez télécharger hello suivant du fichier de modèle et les paramètres du Gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="384a1-160">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="384a1-161">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="384a1-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="384a1-162">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="384a1-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="384a1-163">Renseignez les paramètres vide hello hello `apim.parameters.json` pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="384a1-163">Fill in hello empty parameters in hello `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="384a1-164">Utilisez hello suivant PowerShell commande toodeploy hello Gestionnaire de ressources du modèle de fichiers et de paramètres pour la gestion des API :</span><span class="sxs-lookup"><span data-stu-id="384a1-164">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="384a1-165">Configuration de Gestion des API</span><span class="sxs-lookup"><span data-stu-id="384a1-165">Configure API Management</span></span>

<span data-ttu-id="384a1-166">Une fois Gestion des API et le cluster Fabric Service déployés, vous pouvez configurer un principal de Service Fabric dans Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="384a1-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="384a1-167">Cela vous permet de toocreate une stratégie de service principaux qui envoie le cluster Service Fabric de tooyour le trafic.</span><span class="sxs-lookup"><span data-stu-id="384a1-167">This allows you toocreate a backend service policy that sends traffic tooyour Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="384a1-168">Sécurité de Gestion des API</span><span class="sxs-lookup"><span data-stu-id="384a1-168">API Management Security</span></span>

<span data-ttu-id="384a1-169">tooconfigure hello Service Fabric principal, vous devez tout d’abord les paramètres de sécurité de gestion des API tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="384a1-169">tooconfigure hello Service Fabric backend, you first need tooconfigure API Management security settings.</span></span> <span data-ttu-id="384a1-170">les paramètres de sécurité tooconfigure, accédez tooyour API de service de gestion Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="384a1-170">tooconfigure security settings, go tooyour API Management service in hello Azure portal.</span></span>

#### <a name="enable-hello-api-management-rest-api"></a><span data-ttu-id="384a1-171">Activer l’API REST de gestion des API de hello</span><span class="sxs-lookup"><span data-stu-id="384a1-171">Enable hello API Management REST API</span></span>

<span data-ttu-id="384a1-172">Hello API REST de gestion des API est actuellement hello seule façon tooconfigure un service principal.</span><span class="sxs-lookup"><span data-stu-id="384a1-172">hello API Management REST API is currently hello only way tooconfigure a backend service.</span></span> <span data-ttu-id="384a1-173">première étape de Hello est tooenable hello API REST de gestion des API et sécuriser.</span><span class="sxs-lookup"><span data-stu-id="384a1-173">hello first step is tooenable hello API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="384a1-174">Dans le service de gestion des API de hello, sélectionnez **gestion des API - version préliminaire** sous **sécurité**.</span><span class="sxs-lookup"><span data-stu-id="384a1-174">In hello API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="384a1-175">Vérifiez hello **API REST de gestion des API activer** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="384a1-175">Check hello **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="384a1-176">Notez hello URL d’API de gestion - il s’agit des URL de hello, nous allons utiliser tooset ultérieure des principaux de Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="384a1-176">Note hello Management API URL - this is hello URL we'll use later tooset up hello Service Fabric backend</span></span>
 4. <span data-ttu-id="384a1-177">Générer un **jeton d’accès** en sélectionnant une date d’expiration et une clé, puis cliquez sur hello **générer** bouton bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="384a1-177">Generate an **access Token** by selecting an expiry date and a key, then click hello **Generate** button toward hello bottom of hello page.</span></span>
 5. <span data-ttu-id="384a1-178">Hello de copie **jeton d’accès** et enregistrez-le - nous les utiliserons Bonjour comme suit.</span><span class="sxs-lookup"><span data-stu-id="384a1-178">Copy hello **access token** and save it - we'll use this in hello following steps.</span></span> <span data-ttu-id="384a1-179">Notez que cela est différent de hello des clés primaires et secondaires.</span><span class="sxs-lookup"><span data-stu-id="384a1-179">Note this is different from hello primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="384a1-180">Chargement d’un certificat client Service Fabric</span><span class="sxs-lookup"><span data-stu-id="384a1-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="384a1-181">Gestion des API doivent s’authentifier avec votre cluster Service Fabric pour la découverte de service à l’aide d’un certificat client qui a cluster tooyour d’accès.</span><span class="sxs-lookup"><span data-stu-id="384a1-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access tooyour cluster.</span></span> <span data-ttu-id="384a1-182">Par souci de simplicité, ce didacticiel utilise hello même certificat spécifié lors de la création du cluster Service Fabric hello, qui par défaut peut être utilisé tooaccess votre cluster.</span><span class="sxs-lookup"><span data-stu-id="384a1-182">For simplicity, this tutorial uses hello same certificate specified when creating hello Service Fabric cluster, which by default can be used tooaccess your cluster.</span></span>

 1. <span data-ttu-id="384a1-183">Dans le service de gestion des API de hello, sélectionnez **certificats clients - version préliminaire** sous **sécurité**.</span><span class="sxs-lookup"><span data-stu-id="384a1-183">In hello API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="384a1-184">Cliquez sur hello **+ ajouter** bouton</span><span class="sxs-lookup"><span data-stu-id="384a1-184">Click hello **+ Add** button</span></span>
 2. <span data-ttu-id="384a1-185">Sélectionnez hello fichier de clé privée (.pfx) du certificat de cluster hello que vous avez spécifié lors de la création de votre cluster Service Fabric, lui donner un nom et mot de passe clé privée hello.</span><span class="sxs-lookup"><span data-stu-id="384a1-185">Select hello private key file (.pfx) of hello cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide hello private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="384a1-186">Ce didacticiel utilise hello même certificat pour la sécurité de client d’authentification et du cluster de nœud à l’autre.</span><span class="sxs-lookup"><span data-stu-id="384a1-186">This tutorial uses hello same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="384a1-187">Vous pouvez utiliser un certificat client distinct si vous avez un tooaccess configuré votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="384a1-187">You may use a separate client certificate if you have one configured tooaccess your Service Fabric cluster.</span></span>

### <a name="configure-hello-backend"></a><span data-ttu-id="384a1-188">Configurer hello principal</span><span class="sxs-lookup"><span data-stu-id="384a1-188">Configure hello backend</span></span>

<span data-ttu-id="384a1-189">Maintenant que la sécurité de la gestion des API est configurée, vous pouvez configurer les principaux de Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="384a1-189">Now that API Management security is configured, you can configure hello Service Fabric backend.</span></span> <span data-ttu-id="384a1-190">Pour les serveurs principaux de Service Fabric, cluster Service Fabric de hello est hello principal, plutôt que d’un service de l’infrastructure de Service spécifique.</span><span class="sxs-lookup"><span data-stu-id="384a1-190">For Service Fabric backends, hello Service Fabric cluster is hello backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="384a1-191">Cela permet à un toomore tooroute de stratégie unique à un service de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="384a1-191">This allows a single policy tooroute toomore than one service in hello cluster.</span></span>

<span data-ttu-id="384a1-192">Cette étape nécessite le jeton d’accès hello que précédemment générés et hello empreinte numérique de votre certificat de cluster que vous avez téléchargé tooAPI Management à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="384a1-192">This step requires hello access token you generated earlier and hello thumbprint for your cluster certificate you uploaded tooAPI Management in hello previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="384a1-193">Si vous avez utilisé un certificat client distinct à l’étape précédente de hello pour la gestion des API, vous devez l’empreinte numérique hello du certificat client hello empreinte de certificat du cluster addition toohello dans cette étape.</span><span class="sxs-lookup"><span data-stu-id="384a1-193">If you used a separate client certificate in hello previous step for API Management, you need hello thumbprint for hello client certificate in addition toohello cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="384a1-194">Envoyer hello suivant toohello de demande HTTP PUT URL d’API de gestion des API notées précédemment lors de l’activation du service principal de hello API REST de gestion des API tooconfigure hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="384a1-194">Send hello following HTTP PUT request toohello API Management API URL you noted earlier when enabling hello API Management REST API tooconfigure hello Service Fabric backend service.</span></span> <span data-ttu-id="384a1-195">Vous devez voir une `HTTP 201 Created` réponse lors de la commande hello réussit.</span><span class="sxs-lookup"><span data-stu-id="384a1-195">You should see an `HTTP 201 Created` response when hello command succeeds.</span></span> <span data-ttu-id="384a1-196">Pour plus d’informations sur chaque champ, consultez Gestion des API de hello [documentation de référence des API de service principal](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span><span class="sxs-lookup"><span data-stu-id="384a1-196">For more information on each field, see hello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="384a1-197">Commande HTTP et URL :</span><span class="sxs-lookup"><span data-stu-id="384a1-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="384a1-198">En-têtes de requête :</span><span class="sxs-lookup"><span data-stu-id="384a1-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="384a1-199">Corps de la requête :</span><span class="sxs-lookup"><span data-stu-id="384a1-199">Request body:</span></span>
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

<span data-ttu-id="384a1-200">Hello **url** paramètre ici est un nom qualifié complet de service d’un service dans votre cluster de toutes les demandes sont routés par défaut de tooby si aucun nom de service n’est spécifié dans une stratégie de serveur principal.</span><span class="sxs-lookup"><span data-stu-id="384a1-200">hello **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed tooby default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="384a1-201">Vous pouvez utiliser un nom de service factice, tel que « fabric : / faux/service » si vous ne comptez pas toohave un service de secours.</span><span class="sxs-lookup"><span data-stu-id="384a1-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend toohave a fallback service.</span></span>

<span data-ttu-id="384a1-202">Consultez toohello gestion des API [documentation de référence des API de service principal](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) pour plus d’informations sur chaque champ.</span><span class="sxs-lookup"><span data-stu-id="384a1-202">Refer toohello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="384a1-203">Exemple</span><span class="sxs-lookup"><span data-stu-id="384a1-203">Example</span></span>

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="384a1-204">Déploiement d’un service principal de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="384a1-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="384a1-205">Maintenant que vous avez hello que service Fabric est configuré comme un tooAPI principal Management, vous pouvez créer des stratégies du serveur principal pour votre API qui envoient le trafic services de Service Fabric tooyour.</span><span class="sxs-lookup"><span data-stu-id="384a1-205">Now that you have hello Service Fabric configured as a backend tooAPI Management, you can author backend policies for your APIs that send traffic tooyour Service Fabric services.</span></span> <span data-ttu-id="384a1-206">Mais tout d’abord vous avez besoin d’un service en cours d’exécution dans les demandes de tooaccept Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="384a1-206">But first you need a service running in Service Fabric tooaccept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="384a1-207">Création d’un service Service Fabric avec un point de terminaison HTTP</span><span class="sxs-lookup"><span data-stu-id="384a1-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="384a1-208">Pour ce didacticiel, nous allons créer une base Service sans état ASP.NET Core fiable à l’aide du modèle de projet Web API hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="384a1-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using hello default Web API project template.</span></span> <span data-ttu-id="384a1-209">Vous créerez ainsi un point de terminaison HTTP pour votre service, que vous exposerez via Gestion des API Azure :</span><span class="sxs-lookup"><span data-stu-id="384a1-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="384a1-210">Commencez par [configurer votre environnement de développement pour le développement d’ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span><span class="sxs-lookup"><span data-stu-id="384a1-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="384a1-211">Une fois votre environnement de développement configuré, démarrez Visual Studio en tant qu’administrateur et créez un service ASP.NET Core :</span><span class="sxs-lookup"><span data-stu-id="384a1-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="384a1-212">Dans Visual Studio, sélectionnez Fichier -> Nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="384a1-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="384a1-213">Sélectionnez le modèle d’Application Service Fabric hello dans le Cloud et nommez-le **« ApiApplication »**.</span><span class="sxs-lookup"><span data-stu-id="384a1-213">Select hello Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="384a1-214">Sélectionnez hello modèle de service ASP.NET Core et projet de hello nom **« WebApiService »**.</span><span class="sxs-lookup"><span data-stu-id="384a1-214">Select hello ASP.NET Core service template and name hello project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="384a1-215">Sélectionnez le modèle de projet hello Web API ASP.NET Core 1.1.</span><span class="sxs-lookup"><span data-stu-id="384a1-215">Select hello Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="384a1-216">Une fois que le projet de hello est créé, ouvrez `PackageRoot\ServiceManifest.xml` et supprimer hello `Port` attribut à partir de la configuration de ressource de point de terminaison hello :</span><span class="sxs-lookup"><span data-stu-id="384a1-216">Once hello project is created, open `PackageRoot\ServiceManifest.xml` and remove hello `Port` attribute from hello endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="384a1-217">Cela permet à Service Fabric toospecify un port de manière dynamique à partir de la plage de ports d’application hello, qui nous ouverts via hello groupe de sécurité réseau dans le modèle de gestionnaire de ressources de cluster hello, en autorisant le trafic tooflow tooit à partir de la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="384a1-217">This allows Service Fabric toospecify a port dynamically from hello application port range, which we opened through hello Network Security Group in hello cluster Resource Manager template, allowing traffic tooflow tooit from API Management.</span></span>
 
 6. <span data-ttu-id="384a1-218">Appuyez sur F5 dans Visual Studio tooverify hello web API est disponible localement.</span><span class="sxs-lookup"><span data-stu-id="384a1-218">Press F5 in Visual Studio tooverify hello web API is available locally.</span></span> 

    <span data-ttu-id="384a1-219">Ouvrez l’Explorateur de l’infrastructure de Service et Descendre instance spécifique de tooa Hello ASP.NET toosee hello adresse de base hello service principal est à l’écoute sur.</span><span class="sxs-lookup"><span data-stu-id="384a1-219">Open Service Fabric Explorer and drill down tooa specific instance of hello ASP.NET Core service toosee hello base address hello service is listening on.</span></span> <span data-ttu-id="384a1-220">Ajouter `/api/values` toohello adresse de base et ouvrez-le dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="384a1-220">Add `/api/values` toohello base address and open it in a browser.</span></span> <span data-ttu-id="384a1-221">Cela appelle hello méthode Get sur hello ValuesController dans le modèle d’API Web hello.</span><span class="sxs-lookup"><span data-stu-id="384a1-221">This invokes hello Get method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="384a1-222">Il renvoie la réponse par défaut hello qui est fourni par le modèle de hello, un tableau JSON qui contient deux chaînes :</span><span class="sxs-lookup"><span data-stu-id="384a1-222">It returns hello default response that is provided by hello template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="384a1-223">Il s’agit de point de terminaison hello vous expose via l’API de gestion dans Azure.</span><span class="sxs-lookup"><span data-stu-id="384a1-223">This is hello endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="384a1-224">Enfin, déployez un cluster tooyour hello application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="384a1-224">Finally, deploy hello application tooyour cluster in Azure.</span></span> <span data-ttu-id="384a1-225">[À l’aide de Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), cliquez sur le projet d’Application hello et sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="384a1-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click hello Application project and select **Publish**.</span></span> <span data-ttu-id="384a1-226">Fournissez votre point de terminaison de cluster (par exemple, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello application tooyour l’infrastructure de Service de cluster dans Azure.</span><span class="sxs-lookup"><span data-stu-id="384a1-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello application tooyour Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="384a1-227">Un service ASP.NET Core sans état nommé `fabric:/ApiApplication/WebApiService` doit maintenant s’exécuter dans votre cluster Service Fabric dans Azure.</span><span class="sxs-lookup"><span data-stu-id="384a1-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="384a1-228">Création d’une opération d’API</span><span class="sxs-lookup"><span data-stu-id="384a1-228">Create an API operation</span></span>

<span data-ttu-id="384a1-229">Maintenant, nous sommes prêt toocreate une opération de gestion des API qui toocommunicate d’utilisation des clients externes avec hello service sans état de ASP.NET Core en cours d’exécution dans le cluster Service Fabric de hello.</span><span class="sxs-lookup"><span data-stu-id="384a1-229">Now we're ready toocreate an operation in API Management that external clients use toocommunicate with hello ASP.NET Core stateless service running in hello Service Fabric cluster.</span></span>

 1. <span data-ttu-id="384a1-230">Connectez-vous à toohello portail Azure et accédez de déploiement du service Gestion des API tooyour.</span><span class="sxs-lookup"><span data-stu-id="384a1-230">Log in toohello Azure portal and navigate tooyour API Management service deployment.</span></span>
 2. <span data-ttu-id="384a1-231">Dans le panneau de service de gestion des API hello, sélectionnez **API - version préliminaire**</span><span class="sxs-lookup"><span data-stu-id="384a1-231">In hello API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="384a1-232">Ajouter une nouvelle API en cliquant sur hello **API vide** boîte et remplissez la boîte de dialogue hello :</span><span class="sxs-lookup"><span data-stu-id="384a1-232">Add a new API by clicking hello **Blank API** box and filling out hello dialog box:</span></span>

     - <span data-ttu-id="384a1-233">**URL du service Web** : pour les principaux de Service Fabric, cette valeur d’URL n’est pas utilisée.</span><span class="sxs-lookup"><span data-stu-id="384a1-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="384a1-234">Vous pouvez placer n’importe quelle valeur ici.</span><span class="sxs-lookup"><span data-stu-id="384a1-234">You can put any value here.</span></span> <span data-ttu-id="384a1-235">Pour ce didacticiel, utilisez : `http://servicefabric`.</span><span class="sxs-lookup"><span data-stu-id="384a1-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="384a1-236">**Nom** : entrez un nom pour votre API.</span><span class="sxs-lookup"><span data-stu-id="384a1-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="384a1-237">Pour ce didacticiel, utilisez `Service Fabric App`.</span><span class="sxs-lookup"><span data-stu-id="384a1-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="384a1-238">**Modèle d’URL** : sélectionnez HTTP, HTTPS ou les deux.</span><span class="sxs-lookup"><span data-stu-id="384a1-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="384a1-239">Pour ce didacticiel, utilisez `both`.</span><span class="sxs-lookup"><span data-stu-id="384a1-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="384a1-240">**API URL Suffix** (Suffixe d’URL d’API) : spécifiez un suffixe pour notre API.</span><span class="sxs-lookup"><span data-stu-id="384a1-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="384a1-241">Pour ce didacticiel, utilisez `myapp`.</span><span class="sxs-lookup"><span data-stu-id="384a1-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="384a1-242">Une fois hello API est créé, cliquez sur **+ de l’opération d’ajout de** tooadd une API frontale opération.</span><span class="sxs-lookup"><span data-stu-id="384a1-242">Once hello API is created, click **+ Add operation** tooadd a front-end API operation.</span></span> <span data-ttu-id="384a1-243">Renseignez les valeurs hello :</span><span class="sxs-lookup"><span data-stu-id="384a1-243">Fill out hello values:</span></span>
    
     - <span data-ttu-id="384a1-244">**URL**: sélectionnez `GET` et fournir un chemin d’accès URL hello API.</span><span class="sxs-lookup"><span data-stu-id="384a1-244">**URL**: Select `GET` and provide a URL path for hello API.</span></span> <span data-ttu-id="384a1-245">Pour ce didacticiel, utilisez `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="384a1-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="384a1-246">Par défaut, le chemin d’accès de hello URL spécifié ici est le chemin d’accès des URL hello envoyé service de l’infrastructure de Service principal toohello.</span><span class="sxs-lookup"><span data-stu-id="384a1-246">By default, hello URL path specified here is hello URL path sent toohello backend Service Fabric service.</span></span> <span data-ttu-id="384a1-247">Si vous utilisez hello même chemin d’URL ici que votre service utilise, dans ce cas `/api/values`, puis hello fonctionne sans modification supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="384a1-247">If you use hello same URL path here that your service uses, in this case `/api/values`, then hello operation works without further modification.</span></span> <span data-ttu-id="384a1-248">Vous pouvez également spécifier un chemin d’URL ici est différent du chemin d’accès de l’URL hello utilisé par votre service principal de service de l’infrastructure de Service, dans ce cas, vous devez également toospecify besoin de réécrire d’un chemin d’accès de votre stratégie de l’opération ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="384a1-248">You may also specify a URL path here that is different from hello URL path used by your backend Service Fabric service, in which case you will also need toospecify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="384a1-249">**Nom d’affichage**: fournir un nom pour l’API de hello.</span><span class="sxs-lookup"><span data-stu-id="384a1-249">**Display name**: Provide any name for hello API.</span></span> <span data-ttu-id="384a1-250">Pour ce didacticiel, utilisez `Values`.</span><span class="sxs-lookup"><span data-stu-id="384a1-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="384a1-251">Configuration d’une stratégie de principal</span><span class="sxs-lookup"><span data-stu-id="384a1-251">Configure a backend policy</span></span>

<span data-ttu-id="384a1-252">stratégie de serveur principal Hello lie l’ensemble.</span><span class="sxs-lookup"><span data-stu-id="384a1-252">hello backend policy ties everything together.</span></span> <span data-ttu-id="384a1-253">Il s’agit dans laquelle vous configurez hello principal Service Fabric toowhich du service sont routées.</span><span class="sxs-lookup"><span data-stu-id="384a1-253">This is where you configure hello backend Service Fabric service toowhich requests are routed.</span></span> <span data-ttu-id="384a1-254">Vous pouvez appliquer cette opération de l’API tooany stratégie.</span><span class="sxs-lookup"><span data-stu-id="384a1-254">You can apply this policy tooany API operation.</span></span> <span data-ttu-id="384a1-255">Hello [configuration principale d’un Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) fournit suivant de hello demande des contrôles de routage :</span><span class="sxs-lookup"><span data-stu-id="384a1-255">hello [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides hello following request routing controls:</span></span> 
 - <span data-ttu-id="384a1-256">Sélection de l’instance de service en spécifiant un nom d’instance d’un service Service Fabric, soit codé en dur (par exemple, `"fabric:/myapp/myservice"`) ou généré à partir de la demande de hello HTTP (par exemple, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="384a1-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from hello HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="384a1-257">Résolution de partition en générant une clé de partition à l’aide d’un modèle de partitionnement de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="384a1-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="384a1-258">Sélection de réplica pour les services avec état.</span><span class="sxs-lookup"><span data-stu-id="384a1-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="384a1-259">Résolution recommencez les conditions qui permettent de conditions de hello toospecify pour résoudre à nouveau un emplacement de service et le renvoi d’une demande.</span><span class="sxs-lookup"><span data-stu-id="384a1-259">Resolution retry conditions that allow you toospecify hello conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="384a1-260">Pour ce didacticiel, créez une stratégie de serveur principal qui route les requêtes directement toohello service sans état de ASP.NET Core déployé précédemment :</span><span class="sxs-lookup"><span data-stu-id="384a1-260">For this tutorial, create a backend policy that routes requests directly toohello ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="384a1-261">Sélectionner et modifier hello **entrants stratégies** pour hello `Values` opération en cliquant sur icône de modification hello, puis en sélectionnant **mode Code**.</span><span class="sxs-lookup"><span data-stu-id="384a1-261">Select and edit hello **inbound policies** for hello `Values` operation by clicking hello edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="384a1-262">Dans l’éditeur de code hello stratégie, ajoutez un `set-backend-service` stratégie sous entrant stratégies, comme indiqué ici et cliquez sur hello **enregistrer** bouton :</span><span class="sxs-lookup"><span data-stu-id="384a1-262">In hello policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click hello **Save** button:</span></span>
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

<span data-ttu-id="384a1-263">Pour un ensemble d’attributs de stratégie principal de l’infrastructure de Service, consultez toohello [documentation principale de gestion des API](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span><span class="sxs-lookup"><span data-stu-id="384a1-263">For a full set of Service Fabric back-end policy attributes, refer toohello [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-hello-api-tooa-product"></a><span data-ttu-id="384a1-264">Ajouter hello API tooa produit.</span><span class="sxs-lookup"><span data-stu-id="384a1-264">Add hello API tooa product.</span></span> 

<span data-ttu-id="384a1-265">Avant de pouvoir appeler les API hello, il doit être ajouté produit tooa où vous pouvez accorder l’accès toousers.</span><span class="sxs-lookup"><span data-stu-id="384a1-265">Before you can call hello API, it must be added tooa product where you can grant access toousers.</span></span> 

 1. <span data-ttu-id="384a1-266">Dans le service de gestion des API de hello, sélectionnez **produits - version préliminaire**.</span><span class="sxs-lookup"><span data-stu-id="384a1-266">In hello API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="384a1-267">Par défaut, Gestion des API fournit deux produits : Starter et Unlimited.</span><span class="sxs-lookup"><span data-stu-id="384a1-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="384a1-268">Sélectionnez illimitées hello.</span><span class="sxs-lookup"><span data-stu-id="384a1-268">Select hello Unlimited product.</span></span>
 3. <span data-ttu-id="384a1-269">Sélectionnez les API.</span><span class="sxs-lookup"><span data-stu-id="384a1-269">Select APIs.</span></span>
 4. <span data-ttu-id="384a1-270">Cliquez sur hello **+ ajouter** bouton.</span><span class="sxs-lookup"><span data-stu-id="384a1-270">Click hello **+ Add** button.</span></span>
 5. <span data-ttu-id="384a1-271">Sélectionnez hello `Service Fabric App` API vous créés dans les étapes précédentes hello et cliquez sur hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="384a1-271">Select hello `Service Fabric App` API you created in hello previous steps and click hello **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="384a1-272">Testez-le</span><span class="sxs-lookup"><span data-stu-id="384a1-272">Test it</span></span>

<span data-ttu-id="384a1-273">Vous pouvez maintenant essayer d’envoi d’un service principal de tooyour demande dans l’infrastructure de Service via la gestion de l’API directement à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="384a1-273">You can now try sending a request tooyour back-end service in Service Fabric through API Management directly from hello Azure portal.</span></span>

 1. <span data-ttu-id="384a1-274">Dans le service de gestion des API de hello, sélectionnez **API - version préliminaire**.</span><span class="sxs-lookup"><span data-stu-id="384a1-274">In hello API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="384a1-275">Bonjour `Service Fabric App` API que vous avez créé dans les étapes précédentes hello, sélectionnez hello **Test** onglet.</span><span class="sxs-lookup"><span data-stu-id="384a1-275">In hello `Service Fabric App` API you created in hello previous steps, select hello **Test** tab.</span></span>
 3. <span data-ttu-id="384a1-276">Cliquez sur hello **envoyer** bouton toosend un service de test demande toohello principal.</span><span class="sxs-lookup"><span data-stu-id="384a1-276">Click hello **Send** button toosend a test request toohello backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="384a1-277">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="384a1-277">Next steps</span></span>

<span data-ttu-id="384a1-278">À ce stade, vous devez disposer d’une configuration de base avec Service Fabric et Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="384a1-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="384a1-279">Ce didacticiel utilise l’authentification de base utilisateur basée sur certificat pour votre tooget de cluster Service Fabric que vous permettent de rapidement.</span><span class="sxs-lookup"><span data-stu-id="384a1-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster tooget you set up quickly.</span></span> <span data-ttu-id="384a1-280">Une authentification utilisateur plus avancée de votre cluster Service Fabric est préférable avec [l’authentification Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span><span class="sxs-lookup"><span data-stu-id="384a1-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="384a1-281">Ensuite, [créer et configurer des paramètres de produits avancés dans Gestion des API Azure](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare votre application pour le trafic du monde réel.</span><span class="sxs-lookup"><span data-stu-id="384a1-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare your application for real world traffic.</span></span>

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
