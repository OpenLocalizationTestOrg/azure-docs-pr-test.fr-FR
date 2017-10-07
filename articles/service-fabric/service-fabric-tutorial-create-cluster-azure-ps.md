---
title: aaaCreate une infrastructure de Service de cluster dans Azure | Documents Microsoft
description: "Découvrez comment toocreate un Service Fabric de Linux ou Windows cluster dans Azure à l’aide de PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="02990-103">Créer un cluster sécurisé sur Azure à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="02990-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="02990-104">Ce didacticiel vous montre comment toocreate une infrastructure de Service de cluster (Windows ou Linux) en cours d’exécution dans Azure.</span><span class="sxs-lookup"><span data-stu-id="02990-104">This tutorial shows you how toocreate a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="02990-105">Lorsque vous avez terminé, vous disposez d’un cluster en cours d’exécution dans le cloud hello que vous pouvez déployer des applications.</span><span class="sxs-lookup"><span data-stu-id="02990-105">When you're finished, you have a cluster running in hello cloud that you can deploy applications to.</span></span>

<span data-ttu-id="02990-106">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="02990-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="02990-107">Création d’un cluster Service Fabric sécurisé dans Azure à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="02990-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="02990-108">Cluster hello sécurisé avec un certificat X.509</span><span class="sxs-lookup"><span data-stu-id="02990-108">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="02990-109">Connecter le cluster toohello à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="02990-109">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="02990-110">Supprimer un cluster</span><span class="sxs-lookup"><span data-stu-id="02990-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02990-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="02990-111">Prerequisites</span></span>
<span data-ttu-id="02990-112">Avant de commencer ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="02990-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="02990-113">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="02990-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="02990-114">Installer hello [module Service Fabric SDK et PowerShell](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="02990-114">Install hello [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="02990-115">Installer hello [Azure Powershell version 4.1 ou version ultérieure du module](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="02990-115">Install hello [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="02990-116">Hello procédure crée une version d’évaluation (seul ordinateur virtuel) à nœud unique cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="02990-116">hello following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="02990-117">cluster de Hello est sécurisé par un certificat auto-signé qui obtient créé en même temps que le cluster de hello et placé dans un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="02990-117">hello cluster is secured by a self-signed certificate that gets created along with hello cluster and then placed in a key vault.</span></span> <span data-ttu-id="02990-118">Les clusters à nœud unique ne peut pas être mis à l’échelle au-delà d’un ordinateur virtuel et les clusters d’aperçu ne peut pas être mis à niveau toonewer versions.</span><span class="sxs-lookup"><span data-stu-id="02990-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded toonewer versions.</span></span>

<span data-ttu-id="02990-119">coût toocalculate par l’exécution d’un cluster Service Fabric dans Azure utilisation hello [calculatrice de tarification Azure](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="02990-119">toocalculate cost incurred by running a Service Fabric cluster in Azure use hello [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="02990-120">Pour plus d’informations sur la création de clusters Service Fabric, consultez l’article [Créer un cluster Service Fabric à l’aide d’Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="02990-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-hello-cluster-using-azure-powershell"></a><span data-ttu-id="02990-121">Créer le cluster hello à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="02990-121">Create hello cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="02990-122">Télécharger une copie locale du modèle de gestionnaire de ressources Azure hello et fichier de paramètres hello de hello [modèle Azure Resource Manager pour le Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="02990-122">Download a local copy of hello Azure Resource Manager template and hello parameter file from hello [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="02990-123">*azuredeploy.JSON* est le modèle Azure Resource Manager hello qui définit un cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="02990-123">*azuredeploy.json* is hello Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="02990-124">*azuredeploy.Parameters.JSON* est un fichier de paramètres pour vous de déploiement de cluster toocustomize hello.</span><span class="sxs-lookup"><span data-stu-id="02990-124">*azuredeploy.parameters.json* is a parameters file for you toocustomize hello cluster deployment.</span></span>

2. <span data-ttu-id="02990-125">Personnaliser les paramètres Bonjour suivants de hello *azuredeploy.parameters.json* fichier de paramètres :</span><span class="sxs-lookup"><span data-stu-id="02990-125">Customize hello following parameters in hello *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="02990-126">Paramètre</span><span class="sxs-lookup"><span data-stu-id="02990-126">Parameter</span></span>       | <span data-ttu-id="02990-127">Description</span><span class="sxs-lookup"><span data-stu-id="02990-127">Description</span></span> | <span data-ttu-id="02990-128">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="02990-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="02990-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="02990-129">clusterLocation</span></span> | <span data-ttu-id="02990-130">cluster de hello Hello région Azure toowhich toodeploy.</span><span class="sxs-lookup"><span data-stu-id="02990-130">hello Azure region toowhich toodeploy hello cluster.</span></span> | <span data-ttu-id="02990-131">*par exemple, westeurope, eastasia, eastus*</span><span class="sxs-lookup"><span data-stu-id="02990-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="02990-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="02990-132">clusterName</span></span>     | <span data-ttu-id="02990-133">Nom du cluster de hello souhaité toocreate.</span><span class="sxs-lookup"><span data-stu-id="02990-133">Name of hello cluster you want toocreate.</span></span> | <span data-ttu-id="02990-134">*par exemple, bobs-sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="02990-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="02990-135">adminUsername</span><span class="sxs-lookup"><span data-stu-id="02990-135">adminUserName</span></span>   | <span data-ttu-id="02990-136">compte d’administrateur local Hello sur les ordinateurs virtuels du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="02990-136">hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="02990-137">*N’importe quel nom d’utilisateur Windows Server valide*</span><span class="sxs-lookup"><span data-stu-id="02990-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="02990-138">adminPassword</span><span class="sxs-lookup"><span data-stu-id="02990-138">adminPassword</span></span>   | <span data-ttu-id="02990-139">Mot de passe du compte d’administrateur local de hello sur les ordinateurs virtuels du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="02990-139">Password of hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="02990-140">*N’importe quel mot de passe Windows Server valide*</span><span class="sxs-lookup"><span data-stu-id="02990-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="02990-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="02990-141">clusterCodeVersion</span></span> | <span data-ttu-id="02990-142">toorun de version du Service Fabric Hello.</span><span class="sxs-lookup"><span data-stu-id="02990-142">hello Service Fabric version toorun.</span></span> <span data-ttu-id="02990-143">(255.255.X.255 sont des préversions).</span><span class="sxs-lookup"><span data-stu-id="02990-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="02990-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="02990-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="02990-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="02990-145">vmInstanceCount</span></span> | <span data-ttu-id="02990-146">nombre de Hello de machines virtuelles dans votre cluster (il peut être 1 ou 3-99).</span><span class="sxs-lookup"><span data-stu-id="02990-146">hello number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="02990-147">**1**</span><span class="sxs-lookup"><span data-stu-id="02990-147">**1**</span></span> | <span data-ttu-id="02990-148">*Pour un cluster de la version d’évaluation, spécifiez uniquement un ordinateur virtuel*</span><span class="sxs-lookup"><span data-stu-id="02990-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="02990-149">Ouvrez une console PowerShell, la connexion tooAzure et sélectionnez hello abonnement cluster de hello toodeploy dans :</span><span class="sxs-lookup"><span data-stu-id="02990-149">Open a PowerShell console, login tooAzure, and select hello subscription you want toodeploy hello cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="02990-150">Créez et chiffrer un mot de passe pour hello toobe de certificat utilisé par l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="02990-150">Create and encrypt a password for hello certificate toobe used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="02990-151">Créer des clusters de hello et son certificat en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="02990-151">Create hello cluster and its certificate by running hello following command:</span></span>

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   ><span data-ttu-id="02990-152">Hello `-CertificateSubjectName` paramètre doit s’aligner avec le paramètre clusterName hello spécifié dans le fichier de paramètres hello, ainsi que hello domaine lié toohello région Azure vous avez choisi, telles que : `clustername.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="02990-152">hello `-CertificateSubjectName` parameter should align with hello clusterName parameter specified in hello parameters file, as well as hello domain tied toohello Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="02990-153">Une fois la configuration de hello se termine, il génère des informations sur le cluster hello créé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="02990-153">Once hello configuration finishes, it outputs information about hello cluster created in Azure.</span></span> <span data-ttu-id="02990-154">Il copie également le répertoire hello cluster certificat toohello - CertificateOutputFolder sur le chemin d’accès hello spécifié pour ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="02990-154">It also copies hello cluster certificate toohello -CertificateOutputFolder directory on hello path you specified for this parameter.</span></span> <span data-ttu-id="02990-155">Vous avez besoin de ce certificat de tooaccess Service Fabric Explorer et la vue de contrôle d’intégrité hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="02990-155">You need this certificate tooaccess Service Fabric Explorer and view hello health of your cluster.</span></span>

<span data-ttu-id="02990-156">Prenez note de l’URL de hello pour votre cluster, ce qui peut être toohello similaire suivant URL : *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="02990-156">Take note of hello URL for your cluster, which may be similar toohello following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a><span data-ttu-id="02990-157">Modifier le certificat de hello et accéder au Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="02990-157">Modify hello certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="02990-158">Double-cliquez sur hello tooopen de certificat hello Assistant Importation de certificat.</span><span class="sxs-lookup"><span data-stu-id="02990-158">Double-click hello certificate tooopen hello Certificate Import Wizard.</span></span>

2. <span data-ttu-id="02990-159">Utiliser les paramètres par défaut, mais que toocheck hello **marquer cette clé comme exportable.**</span><span class="sxs-lookup"><span data-stu-id="02990-159">Use default settings, but make sure toocheck hello **Mark this key as exportable.**</span></span> <span data-ttu-id="02990-160">case à cocher, Bonjour **protection par clé privée** étape.</span><span class="sxs-lookup"><span data-stu-id="02990-160">check box, in hello **private key protection** step.</span></span> <span data-ttu-id="02990-161">Visual Studio a besoin de certificat de hello tooexport lors de la configuration de l’authentification de Registre de conteneur Azure tooService Cluster Fabric plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="02990-161">Visual Studio needs tooexport hello certificate when configuring Azure Container Registry tooService Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="02990-162">Vous pouvez maintenant ouvrir Service Fabric Explorer dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="02990-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="02990-163">toodo accédez donc toohello **ManagementEndpoint** URL pour votre cluster à l’aide d’un navigateur web et un certificat de hello select qui a été enregistré sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="02990-163">toodo so, navigate toohello **ManagementEndpoint** URL for your cluster using a web browser, and select hello certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="02990-164">Quand vous ouvrez Service Fabric Explorer, vous voyez une erreur de certificat, car vous utilisez un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="02990-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="02990-165">Dans Microsoft Edge, vous avez tooclick *détails* et puis hello *aller sur la page Web de toohello* lien.</span><span class="sxs-lookup"><span data-stu-id="02990-165">In Edge, you have tooclick *Details* and then hello *Go on toohello webpage* link.</span></span> <span data-ttu-id="02990-166">Dans Chrome, vous avez tooclick *avancé* et puis hello *continuer* lien.</span><span class="sxs-lookup"><span data-stu-id="02990-166">In Chrome, you have tooclick *Advanced* and then hello *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="02990-167">Si la création du cluster hello échoue, vous pouvez toujours exécuter à nouveau commande hello, qui met à jour des ressources hello déjà déployés.</span><span class="sxs-lookup"><span data-stu-id="02990-167">If hello cluster creation fails, you can always rerun hello command, which updates hello resources already deployed.</span></span> <span data-ttu-id="02990-168">Si un certificat a été créé dans le cadre du déploiement de hello a échoué, une est générée.</span><span class="sxs-lookup"><span data-stu-id="02990-168">If a certificate was created as part of hello failed deployment, a new one is generated.</span></span> <span data-ttu-id="02990-169">la création du cluster tootroubleshoot, consultez [créer un cluster Service Fabric à l’aide du Gestionnaire de ressources Azure](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="02990-169">tootroubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-toohello-secure-cluster"></a><span data-ttu-id="02990-170">Connecter le cluster sécurisée de toohello</span><span class="sxs-lookup"><span data-stu-id="02990-170">Connect toohello secure cluster</span></span>
<span data-ttu-id="02990-171">Se connecter à l’aide du module PowerShell de l’infrastructure de Service de hello installé avec hello SDK de l’infrastructure de Service de cluster de toohello.</span><span class="sxs-lookup"><span data-stu-id="02990-171">Connect toohello cluster using hello Service Fabric PowerShell module installed with hello Service Fabric SDK.</span></span>  <span data-ttu-id="02990-172">Tout d’abord, installez hello certificat dans hello personnel (My) magasin de l’utilisateur actuel de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="02990-172">First, install hello certificate into hello Personal (My) store of hello current user on your computer.</span></span>  <span data-ttu-id="02990-173">Exécutez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="02990-173">Run hello following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="02990-174">Vous êtes maintenant cluster sécurisée de tooyour tooconnect prêt.</span><span class="sxs-lookup"><span data-stu-id="02990-174">You are now ready tooconnect tooyour secure cluster.</span></span>

<span data-ttu-id="02990-175">Hello **Service Fabric** module PowerShell fournit de nombreuses applets de commande pour la gestion des clusters Service Fabric, les applications et services.</span><span class="sxs-lookup"><span data-stu-id="02990-175">hello **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="02990-176">Hello d’utilisation [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) applet de commande tooconnect toohello sécurisée cluster.</span><span class="sxs-lookup"><span data-stu-id="02990-176">Use hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello secure cluster.</span></span> <span data-ttu-id="02990-177">Hello empreinte numérique du certificat et les détails de connexion au point de terminaison sont trouvent dans la sortie de hello à partir d’une étape précédente.</span><span class="sxs-lookup"><span data-stu-id="02990-177">hello certificate thumbprint and connection endpoint details are found in hello output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="02990-178">Vérifiez que vous êtes connecté et le cluster de hello est sain à l’aide de hello [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="02990-178">Check that you are connected and hello cluster is healthy using hello [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="02990-179">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="02990-179">Clean up resources</span></span>

<span data-ttu-id="02990-180">Un cluster est composé d’autres ressources Windows Azure en outre toohello du cluster lui-même.</span><span class="sxs-lookup"><span data-stu-id="02990-180">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="02990-181">cluster de Hello la plus simple façon toodelete hello et toutes les ressources hello qu’elle consomme est le groupe de ressources toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="02990-181">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span>

<span data-ttu-id="02990-182">Connectez-vous à tooAzure et sélectionnez l’ID d’abonnement hello avec laquelle vous souhaitez le cluster de hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="02990-182">Log in tooAzure and select hello subscription ID with which you want tooremove hello cluster.</span></span>  <span data-ttu-id="02990-183">Vous pouvez trouver votre ID d’abonnement en vous connectant à toohello [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="02990-183">You can find your subscription ID by logging in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="02990-184">Supprimer le groupe de ressources hello et toutes les ressources de cluster hello à l’aide de hello [applet de commande Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="02990-184">Delete hello resource group and all hello cluster resources using hello [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="02990-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="02990-185">Next steps</span></span>
<span data-ttu-id="02990-186">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="02990-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="02990-187">Créer un cluster Service Fabric dans Azure</span><span class="sxs-lookup"><span data-stu-id="02990-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="02990-188">Cluster hello sécurisé avec un certificat X.509</span><span class="sxs-lookup"><span data-stu-id="02990-188">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="02990-189">Connecter le cluster toohello à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="02990-189">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="02990-190">Supprimer un cluster</span><span class="sxs-lookup"><span data-stu-id="02990-190">Remove a cluster</span></span>

<span data-ttu-id="02990-191">Ensuite, avancer toohello suivant toolearn didacticiel comment toodeploy une application existante.</span><span class="sxs-lookup"><span data-stu-id="02990-191">Next, advance toohello following tutorial toolearn how toodeploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="02990-192">Déployer une application .NET existante avec Docker Compose</span><span class="sxs-lookup"><span data-stu-id="02990-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)
