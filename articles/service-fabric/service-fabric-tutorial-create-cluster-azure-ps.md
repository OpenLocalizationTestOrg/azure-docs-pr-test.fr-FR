---
title: "Créer un cluster Service Fabric dans Azure | Microsoft Docs"
description: "Découvrez comment créer un cluster Service Fabric Windows ou Linux dans Azure à l’aide de PowerShell."
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
ms.openlocfilehash: f62249417552b9cf840bfac3b94c27f63bd7064e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="c4a86-103">Créer un cluster sécurisé sur Azure à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4a86-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="c4a86-104">Ce didacticiel vous montre comment créer un cluster Service Fabric (Windows ou Linux) s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c4a86-104">This tutorial shows you how to create a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="c4a86-105">Lorsque vous avez terminé, vous disposez d’un cluster en cours d’exécution dans le cloud sur lequel vous pouvez déployer des applications.</span><span class="sxs-lookup"><span data-stu-id="c4a86-105">When you're finished, you have a cluster running in the cloud that you can deploy applications to.</span></span>

<span data-ttu-id="c4a86-106">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c4a86-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c4a86-107">Création d’un cluster Service Fabric sécurisé dans Azure à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4a86-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="c4a86-108">Sécuriser le cluster avec un certificat X.509</span><span class="sxs-lookup"><span data-stu-id="c4a86-108">Secure the cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="c4a86-109">Se connecter à un cluster à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4a86-109">Connect to the cluster using PowerShell</span></span>
> * <span data-ttu-id="c4a86-110">Supprimer un cluster</span><span class="sxs-lookup"><span data-stu-id="c4a86-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4a86-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c4a86-111">Prerequisites</span></span>
<span data-ttu-id="c4a86-112">Avant de commencer ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="c4a86-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="c4a86-113">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="c4a86-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="c4a86-114">Installez le [Kit de développement logiciel (SDK) Service Fabric et le module PowerShell](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c4a86-114">Install the [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="c4a86-115">Installez le [module Azure PowerShell, version 4.1 ou ultérieure](https://docs.microsoft.com/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c4a86-115">Install the [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="c4a86-116">La procédure suivante crée un cluster Service Fabric en préversion à nœud unique (machine virtuelle unique).</span><span class="sxs-lookup"><span data-stu-id="c4a86-116">The following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="c4a86-117">Le cluster est sécurisé par un certificat auto-signé, créé en même temps que le cluster et placé dans un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="c4a86-117">The cluster is secured by a self-signed certificate that gets created along with the cluster and then placed in a key vault.</span></span> <span data-ttu-id="c4a86-118">Les clusters à nœud unique ne peuvent pas être mis à l’échelle au-delà d’une machine virtuelle, et les clusters en préversion ne peuvent pas être mis à niveau vers une version plus récente.</span><span class="sxs-lookup"><span data-stu-id="c4a86-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded to newer versions.</span></span>

<span data-ttu-id="c4a86-119">Pour calculer le coût lié à l’exécution d’un cluster Service Fabric dans Azure, utilisez la [calculatrice de prix Azure](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="c4a86-119">To calculate cost incurred by running a Service Fabric cluster in Azure use the [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="c4a86-120">Pour plus d’informations sur la création de clusters Service Fabric, consultez l’article [Créer un cluster Service Fabric à l’aide d’Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c4a86-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-the-cluster-using-azure-powershell"></a><span data-ttu-id="c4a86-121">Créer le cluster à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4a86-121">Create the cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="c4a86-122">Téléchargez une copie locale du modèle Azure Resource Manager et le fichier de paramètres du [modèle Azure Resource Manager pour le référentiel GitHub de Service Fabric](https://aka.ms/securepreviewonelineclustertemplate).</span><span class="sxs-lookup"><span data-stu-id="c4a86-122">Download a local copy of the Azure Resource Manager template and the parameter file from the [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="c4a86-123">*azuredeploy.json* est le modèle Azure Resource Manager qui définit un cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4a86-123">*azuredeploy.json* is the Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="c4a86-124">*azuredeploy.parameters.json* est le fichier de paramètres permettant de personnaliser le déploiement du cluster.</span><span class="sxs-lookup"><span data-stu-id="c4a86-124">*azuredeploy.parameters.json* is a parameters file for you to customize the cluster deployment.</span></span>

2. <span data-ttu-id="c4a86-125">Personnalisez les paramètres suivants dans le fichier de paramètres *azuredeploy.parameters.json* :</span><span class="sxs-lookup"><span data-stu-id="c4a86-125">Customize the following parameters in the *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="c4a86-126">Paramètre</span><span class="sxs-lookup"><span data-stu-id="c4a86-126">Parameter</span></span>       | <span data-ttu-id="c4a86-127">Description</span><span class="sxs-lookup"><span data-stu-id="c4a86-127">Description</span></span> | <span data-ttu-id="c4a86-128">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="c4a86-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="c4a86-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="c4a86-129">clusterLocation</span></span> | <span data-ttu-id="c4a86-130">Région Azure dans laquelle déployer le cluster.</span><span class="sxs-lookup"><span data-stu-id="c4a86-130">The Azure region to which to deploy the cluster.</span></span> | <span data-ttu-id="c4a86-131">*par exemple, westeurope, eastasia, eastus*</span><span class="sxs-lookup"><span data-stu-id="c4a86-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="c4a86-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="c4a86-132">clusterName</span></span>     | <span data-ttu-id="c4a86-133">Nom du cluster que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="c4a86-133">Name of the cluster you want to create.</span></span> | <span data-ttu-id="c4a86-134">*par exemple, bobs-sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="c4a86-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="c4a86-135">adminUsername</span><span class="sxs-lookup"><span data-stu-id="c4a86-135">adminUserName</span></span>   | <span data-ttu-id="c4a86-136">Compte d’administrateur local sur les machines virtuelles du cluster.</span><span class="sxs-lookup"><span data-stu-id="c4a86-136">The local admin account on the cluster virtual machines.</span></span> | <span data-ttu-id="c4a86-137">*N’importe quel nom d’utilisateur Windows Server valide*</span><span class="sxs-lookup"><span data-stu-id="c4a86-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="c4a86-138">adminPassword</span><span class="sxs-lookup"><span data-stu-id="c4a86-138">adminPassword</span></span>   | <span data-ttu-id="c4a86-139">Mot de passe du compte d’administrateur local sur les machines virtuelles du cluster.</span><span class="sxs-lookup"><span data-stu-id="c4a86-139">Password of the local admin account on the cluster virtual machines.</span></span> | <span data-ttu-id="c4a86-140">*N’importe quel mot de passe Windows Server valide*</span><span class="sxs-lookup"><span data-stu-id="c4a86-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="c4a86-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="c4a86-141">clusterCodeVersion</span></span> | <span data-ttu-id="c4a86-142">Version de Service Fabric à exécuter.</span><span class="sxs-lookup"><span data-stu-id="c4a86-142">The Service Fabric version to run.</span></span> <span data-ttu-id="c4a86-143">(255.255.X.255 sont des préversions).</span><span class="sxs-lookup"><span data-stu-id="c4a86-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="c4a86-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="c4a86-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="c4a86-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="c4a86-145">vmInstanceCount</span></span> | <span data-ttu-id="c4a86-146">Nombre de machines virtuelles dans votre cluster (1 ou de 3 à 99).</span><span class="sxs-lookup"><span data-stu-id="c4a86-146">The number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="c4a86-147">**1**</span><span class="sxs-lookup"><span data-stu-id="c4a86-147">**1**</span></span> | <span data-ttu-id="c4a86-148">*Pour un cluster de la version d’évaluation, spécifiez uniquement un ordinateur virtuel*</span><span class="sxs-lookup"><span data-stu-id="c4a86-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="c4a86-149">Ouvrez une console PowerShell, connectez-vous à Azure et sélectionnez l’abonnement dans lequel vous souhaitez déployer le cluster :</span><span class="sxs-lookup"><span data-stu-id="c4a86-149">Open a PowerShell console, login to Azure, and select the subscription you want to deploy the cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="c4a86-150">Créez et chiffrez un mot de passe pour le certificat utilisé par Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4a86-150">Create and encrypt a password for the certificate to be used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="c4a86-151">Créez le cluster et son certificat en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c4a86-151">Create the cluster and its certificate by running the following command:</span></span>

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
   ><span data-ttu-id="c4a86-152">Le paramètre `-CertificateSubjectName` doit s’aligner sur le paramètre clusterName spécifié dans le fichier de paramètres, ainsi que sur le domaine lié à la région Azure que vous avez sélectionnée, par exemple : `clustername.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="c4a86-152">The `-CertificateSubjectName` parameter should align with the clusterName parameter specified in the parameters file, as well as the domain tied to the Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="c4a86-153">Une fois la configuration terminée, il génère des informations sur le cluster créé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c4a86-153">Once the configuration finishes, it outputs information about the cluster created in Azure.</span></span> <span data-ttu-id="c4a86-154">Il copie également le certificat de cluster dans le répertoire CertificateOutputFolder sur le chemin d’accès que vous avez spécifié pour ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="c4a86-154">It also copies the cluster certificate to the -CertificateOutputFolder directory on the path you specified for this parameter.</span></span> <span data-ttu-id="c4a86-155">Vous avez besoin de ce certificat pour accéder au Service Fabric Explorer et afficher l’intégrité de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="c4a86-155">You need this certificate to access Service Fabric Explorer and view the health of your cluster.</span></span>

<span data-ttu-id="c4a86-156">Prenez note de l’URL de votre cluster. Elle peut être semblable à l’URL suivante : *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="c4a86-156">Take note of the URL for your cluster, which may be similar to the following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-the-certificate--access-service-fabric-explorer"></a><span data-ttu-id="c4a86-157">Modifier le certificat et accéder à Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="c4a86-157">Modify the certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="c4a86-158">Double-cliquez sur le certificat pour ouvrir l’Assistant Importation de certificat.</span><span class="sxs-lookup"><span data-stu-id="c4a86-158">Double-click the certificate to open the Certificate Import Wizard.</span></span>

2. <span data-ttu-id="c4a86-159">Utilisez les paramètres par défaut, mais veillez à cocher la case **Marquer cette clé comme exportable**</span><span class="sxs-lookup"><span data-stu-id="c4a86-159">Use default settings, but make sure to check the **Mark this key as exportable.**</span></span> <span data-ttu-id="c4a86-160">à l’étape **Protection de clé privée**.</span><span class="sxs-lookup"><span data-stu-id="c4a86-160">check box, in the **private key protection** step.</span></span> <span data-ttu-id="c4a86-161">Visual Studio doit exporter le certificat pendant la configuration d’Azure Container Registry pour l’authentification de cluster Service Fabric plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c4a86-161">Visual Studio needs to export the certificate when configuring Azure Container Registry to Service Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="c4a86-162">Vous pouvez maintenant ouvrir Service Fabric Explorer dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="c4a86-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="c4a86-163">Pour ce faire, accédez à l’URL de **ManagementEndpoint** pour votre cluster à l’aide d’un navigateur web et sélectionnez le certificat qui a été enregistré sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c4a86-163">To do so, navigate to the **ManagementEndpoint** URL for your cluster using a web browser, and select the certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="c4a86-164">Quand vous ouvrez Service Fabric Explorer, vous voyez une erreur de certificat, car vous utilisez un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="c4a86-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="c4a86-165">Dans Edge, vous devez cliquer sur *Détails*, puis sur le lien *Atteindre la page web*.</span><span class="sxs-lookup"><span data-stu-id="c4a86-165">In Edge, you have to click *Details* and then the *Go on to the webpage* link.</span></span> <span data-ttu-id="c4a86-166">Dans Chrome, vous devez cliquer sur *Avancé*, puis sur le lien *proceed* (Continuer).</span><span class="sxs-lookup"><span data-stu-id="c4a86-166">In Chrome, you have to click *Advanced* and then the *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="c4a86-167">Si la création du cluster échoue, vous pouvez toujours réexécuter la commande et mettre ainsi à jour les ressources déjà déployées.</span><span class="sxs-lookup"><span data-stu-id="c4a86-167">If the cluster creation fails, you can always rerun the command, which updates the resources already deployed.</span></span> <span data-ttu-id="c4a86-168">Si un certificat a été créé dans le cadre du déploiement ayant échoué, un nouveau est généré.</span><span class="sxs-lookup"><span data-stu-id="c4a86-168">If a certificate was created as part of the failed deployment, a new one is generated.</span></span> <span data-ttu-id="c4a86-169">Pour résoudre les problèmes liés à la création du cluster, consultez l’article [Créer un cluster Service Fabric à l’aide d’Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c4a86-169">To troubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-to-the-secure-cluster"></a><span data-ttu-id="c4a86-170">Se connecter à un cluster sécurisé</span><span class="sxs-lookup"><span data-stu-id="c4a86-170">Connect to the secure cluster</span></span>
<span data-ttu-id="c4a86-171">Connectez-vous au cluster à l’aide du module Service Fabric PowerShell installé avec le Kit de développement logiciel (SDK) Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4a86-171">Connect to the cluster using the Service Fabric PowerShell module installed with the Service Fabric SDK.</span></span>  <span data-ttu-id="c4a86-172">Tout d’abord, installez le certificat dans le magasin personnel de l’utilisateur actuel sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c4a86-172">First, install the certificate into the Personal (My) store of the current user on your computer.</span></span>  <span data-ttu-id="c4a86-173">Exécutez la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="c4a86-173">Run the following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="c4a86-174">Vous êtes maintenant prêt à vous connecter à votre cluster sécurisé.</span><span class="sxs-lookup"><span data-stu-id="c4a86-174">You are now ready to connect to your secure cluster.</span></span>

<span data-ttu-id="c4a86-175">Le module **Service Fabric** PowerShell fournit de nombreuses cmdlets pour la gestion des services, applications et clusters Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4a86-175">The **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="c4a86-176">Pour vous connecter au cluster sécurisé, utilisez la cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster).</span><span class="sxs-lookup"><span data-stu-id="c4a86-176">Use the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet to connect to the secure cluster.</span></span> <span data-ttu-id="c4a86-177">Les détails du point de terminaison de connexion et de l’empreinte de certificat se trouvent dans la sortie d’une étape précédente.</span><span class="sxs-lookup"><span data-stu-id="c4a86-177">The certificate thumbprint and connection endpoint details are found in the output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="c4a86-178">Vérifiez que vous êtes connecté et que le cluster est sain à l’aide de la cmdlet [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="c4a86-178">Check that you are connected and the cluster is healthy using the [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="c4a86-179">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="c4a86-179">Clean up resources</span></span>

<span data-ttu-id="c4a86-180">Un cluster est composé d’autres ressources Azure en plus de la ressource de cluster elle-même.</span><span class="sxs-lookup"><span data-stu-id="c4a86-180">A cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="c4a86-181">Le plus simple pour supprimer le cluster et toutes les ressources qu’il consomme consiste à supprimer le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c4a86-181">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span>

<span data-ttu-id="c4a86-182">Connectez-vous à Azure et sélectionnez l’ID d’abonnement pour lequel vous souhaitez supprimer le cluster.</span><span class="sxs-lookup"><span data-stu-id="c4a86-182">Log in to Azure and select the subscription ID with which you want to remove the cluster.</span></span>  <span data-ttu-id="c4a86-183">Vous pouvez trouver votre ID d’abonnement en vous connectant au [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c4a86-183">You can find your subscription ID by logging in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="c4a86-184">Pour supprimer un groupe de ressources et toutes les ressources de cluster, utilisez la cmdlet [Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="c4a86-184">Delete the resource group and all the cluster resources using the [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="c4a86-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c4a86-185">Next steps</span></span>
<span data-ttu-id="c4a86-186">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="c4a86-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c4a86-187">Créer un cluster Service Fabric dans Azure</span><span class="sxs-lookup"><span data-stu-id="c4a86-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="c4a86-188">Sécuriser le cluster avec un certificat X.509</span><span class="sxs-lookup"><span data-stu-id="c4a86-188">Secure the cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="c4a86-189">Se connecter à un cluster à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4a86-189">Connect to the cluster using PowerShell</span></span>
> * <span data-ttu-id="c4a86-190">Supprimer un cluster</span><span class="sxs-lookup"><span data-stu-id="c4a86-190">Remove a cluster</span></span>

<span data-ttu-id="c4a86-191">Ensuite, passez au didacticiel suivant pour apprendre à déployer une application existante.</span><span class="sxs-lookup"><span data-stu-id="c4a86-191">Next, advance to the following tutorial to learn how to deploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="c4a86-192">Déployer une application .NET existante avec Docker Compose</span><span class="sxs-lookup"><span data-stu-id="c4a86-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)
