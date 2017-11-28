---
title: Cluster HPC Pack pour Excel et SOA | Microsoft Docs
description: "Prise en main de l’exécution de charges de travail Excel et SOA à grande échelle sur un cluster HPC Pack dans Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 63babd94fdab15217cfb0757e4cd6efe458a628d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="60be7-103">Prise en main de l’exécution de charges de travail Excel et SOA sur un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="60be7-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="60be7-104">Cet article vous montre comment déployer un cluster Microsoft HPC Pack 2012 R2 dans des machines virtuelles Azure à l’aide d’un modèle de démarrage rapide Azure ou éventuellement d’un script de déploiement Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60be7-104">This article shows you how to deploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="60be7-105">Le cluster utilise des images de machine virtuelle Azure Marketplace conçues pour exécuter des charges de travail d’architecture orientée services (SOA) ou Microsoft Excel avec HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="60be7-105">The cluster uses Azure Marketplace VM images designed to run Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="60be7-106">Vous pouvez utiliser le cluster pour exécuter des services Excel HPC et SOA à partir d’un ordinateur client local.</span><span class="sxs-lookup"><span data-stu-id="60be7-106">You can use the cluster to run Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="60be7-107">Les services Excel HPC incluent le déchargement de classeurs Excel et les fonctions Excel définies par l'utilisateur (UDF).</span><span class="sxs-lookup"><span data-stu-id="60be7-107">The Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="60be7-108">Cet article est basé sur les fonctionnalités, les modèles et les scripts pour HPC Pack 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="60be7-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="60be7-109">Ce scénario n’est pas pris en charge dans HPC Pack 2016 pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="60be7-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="60be7-110">Le diagramme général suivant montre le cluster HPC Pack que vous créez.</span><span class="sxs-lookup"><span data-stu-id="60be7-110">At a high level, the following diagram shows the HPC Pack cluster you create.</span></span>

![Cluster HPC avec des nœuds exécutant des charges de travail Excel][scenario]

## <a name="prerequisites"></a><span data-ttu-id="60be7-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="60be7-112">Prerequisites</span></span>
* <span data-ttu-id="60be7-113">**Ordinateur client** : vous avez besoin d’un ordinateur client Windows pour envoyer des exemples de tâches Excel et SOA au cluster.</span><span class="sxs-lookup"><span data-stu-id="60be7-113">**Client computer** - You need a Windows-based client computer to submit sample Excel and SOA jobs to the cluster.</span></span> <span data-ttu-id="60be7-114">Vous avez également besoin d’un ordinateur Windows pour exécuter le script de déploiement de cluster Azure PowerShell (si vous choisissez cette méthode de déploiement).</span><span class="sxs-lookup"><span data-stu-id="60be7-114">You also need a Windows computer to run the Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="60be7-115">**Abonnement Azure** : si vous n’en avez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="60be7-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="60be7-116">**Quota de cœurs** : vous devez peut-être augmenter le quota de cœurs, en particulier si vous déployez plusieurs nœuds de cluster avec des tailles de machines virtuelles multiprocesseurs.</span><span class="sxs-lookup"><span data-stu-id="60be7-116">**Cores quota** - You might need to increase the quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="60be7-117">Si vous utilisez un modèle de démarrage rapide Azure, le quota de cœurs dans le Resource Manager est défini par région Azure.</span><span class="sxs-lookup"><span data-stu-id="60be7-117">If you are using an Azure quickstart template, the cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="60be7-118">Dans ce cas, vous devrez peut-être augmenter le quota d’une région spécifique.</span><span class="sxs-lookup"><span data-stu-id="60be7-118">In that case, you might need to increase the quota in a specific region.</span></span> <span data-ttu-id="60be7-119">Consultez [Abonnement Azure et limites, quotas et contraintes du service](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="60be7-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="60be7-120">Pour augmenter un quota, [ouvrez une demande de service clientèle en ligne](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) gratuitement.</span><span class="sxs-lookup"><span data-stu-id="60be7-120">To increase a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="60be7-121">**Licence Microsoft Office** : si vous déployez des nœuds de calcul à l’aide d’une image de machine virtuelle HPC Pack 2012 R2 de la Place de marché avec Microsoft Excel, une version d’évaluation de Microsoft Excel Professionnel Plus 2013 est installée et valable pendant 30 jours.</span><span class="sxs-lookup"><span data-stu-id="60be7-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="60be7-122">À la fin de la période d’évaluation, vous devez fournir une licence valide de Microsoft Office pour activer Excel et continuer à exécuter les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="60be7-122">After the evaluation period, you need to provide a valid Microsoft Office license to activate Excel to continue to run workloads.</span></span> <span data-ttu-id="60be7-123">Consultez [Activation d’Excel](#excel-activation) plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="60be7-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="60be7-124">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="60be7-124">Step 1.</span></span> <span data-ttu-id="60be7-125">Configuration d’un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="60be7-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="60be7-126">Nous allons vous montrer deux options de configuration du cluster HPC Pack 2012 R2 : tout d’abord à l’aide d’un modèle de démarrage rapide Azure et du portail Azure et ensuite à l’aide d’un script de déploiement Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60be7-126">We show two options to set up the HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and the Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="60be7-127">Option 1.</span><span class="sxs-lookup"><span data-stu-id="60be7-127">Option 1.</span></span> <span data-ttu-id="60be7-128">Utilisation d’un modèle de démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="60be7-128">Use a quickstart template</span></span>
<span data-ttu-id="60be7-129">Utilisez un modèle de démarrage rapide Azure pour déployer rapidement un cluster HPC Pack dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="60be7-129">Use an Azure quickstart template to quickly deploy an HPC Pack cluster in the Azure portal.</span></span> <span data-ttu-id="60be7-130">Lorsque vous ouvrez le modèle dans le portail, vous obtenez une interface utilisateur simple vous permettant de saisir les paramètres pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="60be7-130">When you open the template in the portal, you get a simple UI where you enter the settings for your cluster.</span></span> <span data-ttu-id="60be7-131">Voici la procédure à suivre.</span><span class="sxs-lookup"><span data-stu-id="60be7-131">Here are the steps.</span></span> 

> [!TIP]
> <span data-ttu-id="60be7-132">Si vous le souhaitez, utilisez un [modèle Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) qui crée un cluster similaire spécialement pour les charges de travail Excel.</span><span class="sxs-lookup"><span data-stu-id="60be7-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="60be7-133">Les étapes sont légèrement différentes de celles qui suivent.</span><span class="sxs-lookup"><span data-stu-id="60be7-133">The steps differ slightly from the following.</span></span>
> 
> 

1. <span data-ttu-id="60be7-134">Consultez [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="60be7-134">Visit the [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="60be7-135">Si vous le souhaitez, examinez les informations sur le modèle et le code source.</span><span class="sxs-lookup"><span data-stu-id="60be7-135">If you want, review information about the template and the source code.</span></span>
2. <span data-ttu-id="60be7-136">Cliquez sur **Déployer vers Azure** pour lancer un déploiement avec le modèle dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="60be7-136">Click **Deploy to Azure** to start a deployment with the template in the Azure portal.</span></span>
   
   ![Modèle de déploiement vers Azure][github]
3. <span data-ttu-id="60be7-138">Dans le portail, procédez comme suit pour saisir les paramètres du modèle de cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="60be7-138">In the portal, follow these steps to enter the parameters for the HPC cluster template.</span></span>
   
   <span data-ttu-id="60be7-139">a.</span><span class="sxs-lookup"><span data-stu-id="60be7-139">a.</span></span> <span data-ttu-id="60be7-140">Sur la page **Paramètres**, saisissez ou modifiez les valeurs des paramètres du modèle.</span><span class="sxs-lookup"><span data-stu-id="60be7-140">On the **Parameters** page, enter or modify values for the template parameters.</span></span> <span data-ttu-id="60be7-141">(Cliquez sur l'icône en regard de chaque paramètre pour obtenir de l'aide.) Des exemples de valeurs sont affichés dans l'écran suivant.</span><span class="sxs-lookup"><span data-stu-id="60be7-141">(Click the icon next to each setting for help information.) Sample values are shown in the following screen.</span></span> <span data-ttu-id="60be7-142">Cet exemple crée un cluster nommé *hpc01* dans le domaine *hpc.local*, constitué d’un nœud principal et de 2 nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="60be7-142">This example creates a cluster named *hpc01* in the *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="60be7-143">Les nœuds de calcul sont créés à partir d'une image de machine virtuelle HPC Pack comprenant Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="60be7-143">The compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Saisie des paramètres][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="60be7-145">La machine virtuelle du nœud principal est créée automatiquement à partir de la [dernière image Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) de HPC Pack 2012 R2 sur Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="60be7-145">The head node VM is created automatically from the [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="60be7-146">Actuellement, l'image repose sur HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="60be7-146">Currently the image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="60be7-147">Les machines virtuelles du nœud de calcul sont créées à partir de la dernière image de la famille de nœuds de calcul sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="60be7-147">Compute node VMs are created from the latest image of the selected compute node family.</span></span> <span data-ttu-id="60be7-148">Sélectionnez l’option **ComputeNodeWithExcel** pour la dernière image de nœud de calcul HPC Pack comprenant une version d’évaluation de Microsoft Excel Professionnel Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="60be7-148">Select the **ComputeNodeWithExcel** option for the latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="60be7-149">Pour déployer un cluster pour les sessions SOA générales ou pour le déchargement Excel UDF, choisissez l'option **ComputeNode** (sans Excel installé).</span><span class="sxs-lookup"><span data-stu-id="60be7-149">To deploy a cluster for general SOA sessions or for Excel UDF offloading, choose the **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="60be7-150">b.</span><span class="sxs-lookup"><span data-stu-id="60be7-150">b.</span></span> <span data-ttu-id="60be7-151">Choisissez l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="60be7-151">Choose the subscription.</span></span>
   
   <span data-ttu-id="60be7-152">c.</span><span class="sxs-lookup"><span data-stu-id="60be7-152">c.</span></span> <span data-ttu-id="60be7-153">Créez un groupe de ressources pour le cluster, tel que *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="60be7-153">Create a resource group for the cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="60be7-154">d.</span><span class="sxs-lookup"><span data-stu-id="60be7-154">d.</span></span> <span data-ttu-id="60be7-155">Choisissez un emplacement pour le groupe de ressources, comme les États-Unis du Centre.</span><span class="sxs-lookup"><span data-stu-id="60be7-155">Choose a location for the resource group, such as Central US.</span></span>
   
   <span data-ttu-id="60be7-156">e.</span><span class="sxs-lookup"><span data-stu-id="60be7-156">e.</span></span> <span data-ttu-id="60be7-157">Lisez les conditions de la page **Mentions légales** .</span><span class="sxs-lookup"><span data-stu-id="60be7-157">On the **Legal terms** page, review the terms.</span></span> <span data-ttu-id="60be7-158">Si vous les acceptez, cliquez sur **Acheter**.</span><span class="sxs-lookup"><span data-stu-id="60be7-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="60be7-159">Une fois que vous avez défini les valeurs du modèle, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="60be7-159">Then, when you are finished setting the values for the template, click **Create**.</span></span>
4. <span data-ttu-id="60be7-160">Lorsque le déploiement est terminé (cela dure environ 30 minutes généralement), exportez le fichier de certificat de cluster depuis le nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="60be7-160">When the deployment completes (it typically takes around 30 minutes), export the cluster certificate file from the cluster head node.</span></span> <span data-ttu-id="60be7-161">Par la suite, vous importez ce certificat public sur l'ordinateur client pour fournir l'authentification côté serveur pour une liaison HTTP sécurisée.</span><span class="sxs-lookup"><span data-stu-id="60be7-161">In a later step, you import this public certificate on the client computer to provide the server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="60be7-162">a.</span><span class="sxs-lookup"><span data-stu-id="60be7-162">a.</span></span> <span data-ttu-id="60be7-163">Dans le portail Azure, accédez au tableau de bord, sélectionnez le nœud principal, puis cliquez sur **Connecter** en haut de la page pour vous connecter à l’aide du Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="60be7-163">In the Azure portal, go to the dashboard, select the head node, and click **Connect** at the top of the page to connect using Remote Desktop.</span></span>
   
    <!-- ![Connect to the head node][connect] -->
   
   <span data-ttu-id="60be7-164">b.</span><span class="sxs-lookup"><span data-stu-id="60be7-164">b.</span></span> <span data-ttu-id="60be7-165">Utilisez les procédures standard du Gestionnaire de certificat pour exporter le certificat du nœud principal (situé sous Cert:\LocalMachine\My) sans la clé privée.</span><span class="sxs-lookup"><span data-stu-id="60be7-165">Use standard procedures in Certificate Manager to export the head node certificate (located under Cert:\LocalMachine\My) without the private key.</span></span> <span data-ttu-id="60be7-166">Dans cet exemple, exportez *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="60be7-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Exportation du certificat][cert]

### <a name="option-2-use-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="60be7-168">Option 2.</span><span class="sxs-lookup"><span data-stu-id="60be7-168">Option 2.</span></span> <span data-ttu-id="60be7-169">Utilisation du script de déploiement du HPC Pack IaaS</span><span class="sxs-lookup"><span data-stu-id="60be7-169">Use the HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="60be7-170">Le script de déploiement du HPC Pack IaaS fournit une autre façon polyvalente de déployer un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="60be7-170">The HPC Pack IaaS deployment script provides another versatile way to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="60be7-171">Il crée un cluster dans le modèle de déploiement classique, tandis que le modèle utilise le modèle de déploiement d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="60be7-171">It creates a cluster in the classic deployment model, whereas the template uses the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="60be7-172">Le script est également compatible avec un abonnement dans le service Azure Global ou Azure China.</span><span class="sxs-lookup"><span data-stu-id="60be7-172">Also, the script is compatible with a subscription in either the Azure Global or Azure China service.</span></span>

<span data-ttu-id="60be7-173">**Autres composants requis**</span><span class="sxs-lookup"><span data-stu-id="60be7-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="60be7-174">**Azure PowerShell** - [installez et configurez Azure PowerShell](/powershell/azure/overview) (version 0.8.10 ou ultérieure) sur votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="60be7-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="60be7-175">**Script de déploiement de HPC Pack IaaS** : Téléchargez et décompressez la dernière version du script à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="60be7-175">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="60be7-176">Vérifiez la version du script en exécutant `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="60be7-176">Check the version of the script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="60be7-177">Cet article est basé sur la version 4.5.0 ou ultérieure du script.</span><span class="sxs-lookup"><span data-stu-id="60be7-177">This article is based on version 4.5.0 or later of the script.</span></span>

<span data-ttu-id="60be7-178">**Création du fichier de configuration**</span><span class="sxs-lookup"><span data-stu-id="60be7-178">**Create the configuration file**</span></span>

 <span data-ttu-id="60be7-179">Le script de déploiement de HPC Pack IaaS utilise un fichier de configuration XML comme entrée, qui décrit l’infrastructure du cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="60be7-179">The HPC Pack IaaS deployment script uses an XML configuration file as input that describes the infrastructure of the HPC cluster.</span></span> <span data-ttu-id="60be7-180">Pour déployer un cluster constitué d’un nœud principal et de 18 nœuds de calcul créés depuis l’image de nœuds de calcul comprenant Microsoft Excel, remplacez les valeurs par celles convenant à votre environnement dans l’exemple de fichier de configuration suivant.</span><span class="sxs-lookup"><span data-stu-id="60be7-180">To deploy a cluster consisting of a head node and 18 compute nodes created from the compute node image that includes Microsoft Excel, substitute values for your environment into the following sample configuration file.</span></span> <span data-ttu-id="60be7-181">Pour plus d’informations sur le fichier de configuration, consultez le fichier Manual.rtf dans le dossier de script et la rubrique [Créer un cluster HPC avec le script de déploiement HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60be7-181">For more information about the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="60be7-182">**Notes relatives au fichier de configuration**</span><span class="sxs-lookup"><span data-stu-id="60be7-182">**Notes about the configuration file**</span></span>

* <span data-ttu-id="60be7-183">Le **VMName** du nœud principal **DOIT** être identique au **ServiceName**, sinon l’exécution des tâches SOA échoue.</span><span class="sxs-lookup"><span data-stu-id="60be7-183">The **VMName** of the head node **MUST** be the same as the **ServiceName**, or SOA jobs fail to run.</span></span>
* <span data-ttu-id="60be7-184">Veillez à spécifier **EnableWebPortal** afin que le certificat du nœud principal soit généré et exporté.</span><span class="sxs-lookup"><span data-stu-id="60be7-184">Make sure you specify **EnableWebPortal** so that the head node certificate is generated and exported.</span></span>
* <span data-ttu-id="60be7-185">Le fichier spécifie un script PowerShell de post-configuration PostConfig.ps1 qui s’exécute sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="60be7-185">The file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on the head node.</span></span> <span data-ttu-id="60be7-186">L’exemple de script suivant configure la chaîne de connexion de stockage Azure, supprime le rôle de nœud de calcul à partir du nœud principal et affiche tous les nœuds en ligne lorsqu’ils sont déployés.</span><span class="sxs-lookup"><span data-stu-id="60be7-186">THe following sample script configures the Azure storage connection string, removes the compute node role from the head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add the HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set the Azure storage connection string for the cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove the compute node role for head node to make sure the Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in the deployment including the head node and compute nodes, which should match the number specified in the XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

<span data-ttu-id="60be7-187">**Exécutez le script**</span><span class="sxs-lookup"><span data-stu-id="60be7-187">**Run the script**</span></span>

1. <span data-ttu-id="60be7-188">Ouvrez la console PowerShell sur l’ordinateur client en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="60be7-188">Open the PowerShell console on the client computer as an administrator.</span></span>
2. <span data-ttu-id="60be7-189">Accédez au dossier de script (E:\IaaSClusterScript dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="60be7-189">Change directory to the script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="60be7-190">Exécutez la commande suivante pour déployer le cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="60be7-190">To deploy the HPC Pack cluster, run the following command.</span></span> <span data-ttu-id="60be7-191">Cet exemple part du principe que le fichier de configuration se trouve dans E:\HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="60be7-191">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="60be7-192">L’exécution du script de déploiement HPC Pack dure un certain temps.</span><span class="sxs-lookup"><span data-stu-id="60be7-192">The HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="60be7-193">Le script exporte et télécharge le certificat de cluster et l'enregistre dans le dossier Documents de l'utilisateur actuel sur l'ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="60be7-193">One thing the script does is to export and download the cluster certificate and save it in the current user’s Documents folder on the client computer.</span></span> <span data-ttu-id="60be7-194">Il script génère un message similaire à celui ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="60be7-194">The script generates a message similar to the following.</span></span> <span data-ttu-id="60be7-195">Vous allez maintenant importer le certificat dans le magasin de certificats approprié.</span><span class="sxs-lookup"><span data-stu-id="60be7-195">In a following step, you import the certificate in the appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import the following certificate in the Trusted Root Certification Authorities certificate store on the computer where you are submitting job or accessing the HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="60be7-196">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="60be7-196">Step 2.</span></span> <span data-ttu-id="60be7-197">Déchargement de classeurs Excel et exécution d’UDF à partir d'un client local</span><span class="sxs-lookup"><span data-stu-id="60be7-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="60be7-198">Activation d’Excel</span><span class="sxs-lookup"><span data-stu-id="60be7-198">Excel activation</span></span>
<span data-ttu-id="60be7-199">En cas d’utilisation d’une image de machine virtuelle ComputeNodeWithExcel pour les charges de travail de production, vous devez fournir une clé de licence Microsoft Office valide pour activer Excel sur les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="60be7-199">When using the ComputeNodeWithExcel VM image for production workloads, you need to provide a valid Microsoft Office license key to activate Excel on the compute nodes.</span></span> <span data-ttu-id="60be7-200">Sinon, la version d’évaluation d’Excel expire au bout de 30 jours et l’exécution des classeurs Excel échoue avec l’exception COMExeption (0x800AC472).</span><span class="sxs-lookup"><span data-stu-id="60be7-200">Otherwise, the evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with the COMException (0x800AC472).</span></span> 

<span data-ttu-id="60be7-201">Vous pouvez rallonger la période d’évaluation de 30 jours supplémentaires : ouvrez une session sur le nœud principal et exécutez la commande clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` sur tous les nœuds de calcul Excel par le biais de HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="60be7-201">You can rearm Excel for another 30 days of evaluation time: Log on to the head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="60be7-202">Vous pouvez rallonger la période d’évaluation 2 fois au maximum.</span><span class="sxs-lookup"><span data-stu-id="60be7-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="60be7-203">Ensuite, vous devez fournir une clé de licence Office valide.</span><span class="sxs-lookup"><span data-stu-id="60be7-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="60be7-204">La version d’Office Professionnel Plus 2013 installée sur l’image de machine virtuelle est une édition de volume avec une clé de licence de volume générique (GVLK).</span><span class="sxs-lookup"><span data-stu-id="60be7-204">The Office Professional Plus 2013 installed on the VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="60be7-205">Vous pouvez l’activer par le biais du service de gestion de clés (KMS), de l’activation basée sur Active Directory (AD-BA) ou d’une clé d’activation multiple (MAK).</span><span class="sxs-lookup"><span data-stu-id="60be7-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="60be7-206">Pour utiliser l’activation KMS/AD-BA, utilisez un serveur KMS existant ou configurez-en un à l’aide du pack de licences en volume Microsoft Office 2013.</span><span class="sxs-lookup"><span data-stu-id="60be7-206">To use KMS/AD-BA, use an existing KMS server or set up a new one by using the Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="60be7-207">(Si vous le souhaitez, configurez le serveur sur le nœud principal.) Activez ensuite la clé d’hôte KMS par Internet ou par téléphone.</span><span class="sxs-lookup"><span data-stu-id="60be7-207">(If you want to, set up the server on the head node.) Then, activate the KMS host key via the Internet or telephone.</span></span> <span data-ttu-id="60be7-208">Puis, exécutez la commande `ospp.vbs` pour définir le port et le serveur KMS et activer Office sur tous les nœuds de calcul Excel.</span><span class="sxs-lookup"><span data-stu-id="60be7-208">Then clusrun `ospp.vbs` to set the KMS server and port and activate Office on all the Excel compute nodes.</span></span> 

    * <span data-ttu-id="60be7-209">Pour utiliser une clé MAK, commencez par exécuter la commande clusrun `ospp.vbs` pour entrer la clé, puis activez tous les nœuds de calcul Excel par Internet ou par téléphone.</span><span class="sxs-lookup"><span data-stu-id="60be7-209">To use MAK, first clusrun `ospp.vbs` to input the key and then activate all the Excel compute nodes via the Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="60be7-210">Les clés de produit commercialisées pour Office Professionnel Plus 2013 ne peuvent pas être utilisées avec cette image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60be7-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="60be7-211">Si vous disposez de clés valides et d’un support d’installation pour des éditions Office ou Excel autres que cette édition en volume Office Professionnel Plus 2013 (édition de volume), vous pouvez également les utiliser.</span><span class="sxs-lookup"><span data-stu-id="60be7-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="60be7-212">Tout d’abord, désinstallez cette édition de volume et installez l’édition dont vous disposez.</span><span class="sxs-lookup"><span data-stu-id="60be7-212">First uninstall this volume edition and install the edition that you have.</span></span> <span data-ttu-id="60be7-213">Le nœud de calcul Excel réinstallé peut être capturé comme une image de machine virtuelle personnalisée à utiliser dans un déploiement à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="60be7-213">The reinstalled Excel compute node can be captured as a customized VM image to use in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="60be7-214">Déchargement de classeurs Excel</span><span class="sxs-lookup"><span data-stu-id="60be7-214">Offload Excel workbooks</span></span>
<span data-ttu-id="60be7-215">Suivez ces étapes pour décharger un classeur Excel afin qu’il s’exécute sur le cluster HPC Pack dans Azure.</span><span class="sxs-lookup"><span data-stu-id="60be7-215">Follow these steps to offload an Excel workbook so that it runs on the HPC Pack cluster in Azure.</span></span> <span data-ttu-id="60be7-216">Pour ce faire, Excel 2010 ou 2013 doit déjà être installé sur l'ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="60be7-216">To do this, you must have Excel 2010 or 2013 already installed on the client computer.</span></span>

1. <span data-ttu-id="60be7-217">Utilisez l’une des options de l'étape 1 pour déployer un cluster HPC Pack avec l’image de nœud de calcul Excel.</span><span class="sxs-lookup"><span data-stu-id="60be7-217">Use one of the options in Step 1 to deploy an HPC Pack cluster with the Excel compute node image.</span></span> <span data-ttu-id="60be7-218">Obtenez le fichier de certificat de cluster (.cer), le nom d'utilisateur et le mot de passe du cluster.</span><span class="sxs-lookup"><span data-stu-id="60be7-218">Obtain the cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="60be7-219">Sur l'ordinateur client, importez le certificat de cluster sous Cert:\CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="60be7-219">On the client computer, import the cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="60be7-220">Assurez-vous qu'Excel est installé.</span><span class="sxs-lookup"><span data-stu-id="60be7-220">Make sure Excel is installed.</span></span> <span data-ttu-id="60be7-221">Créez un fichier Excel.exe.config avec le contenu suivant dans le même dossier qu’Excel.exe sur l'ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="60be7-221">Create an Excel.exe.config file with the following contents in the same folder as Excel.exe on the client computer.</span></span> <span data-ttu-id="60be7-222">Cette étape garantit que le complément COM Excel de HPC Pack 2012 R2 est chargé avec succès.</span><span class="sxs-lookup"><span data-stu-id="60be7-222">This step ensures that the HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="60be7-223">Configurez le client de manière à soumettre des travaux au cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="60be7-223">Set up the client to submit jobs to the HPC Pack cluster.</span></span> <span data-ttu-id="60be7-224">Une option consiste à télécharger l’intégralité de [l’installation de HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49922) et à installer le client HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="60be7-224">One option is to download the full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install the HPC Pack client.</span></span> <span data-ttu-id="60be7-225">Vous pouvez également télécharger et installer les [utilitaires clients HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) et le redistributable Visual C++ 2010 adapté à votre ordinateur ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="60be7-225">Alternatively, download and install the [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and the appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="60be7-226">Dans cet exemple, nous utilisons un exemple de classeur Excel nommé ConvertiblePricing_Complete.xlsb.</span><span class="sxs-lookup"><span data-stu-id="60be7-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="60be7-227">Vous pouvez le télécharger [ici](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="60be7-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="60be7-228">Copiez le classeur Excel dans un dossier de travail comme D:\Excel\Run.</span><span class="sxs-lookup"><span data-stu-id="60be7-228">Copy the Excel workbook to a working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="60be7-229">Ouvrez le classeur Excel.</span><span class="sxs-lookup"><span data-stu-id="60be7-229">Open the Excel workbook.</span></span> <span data-ttu-id="60be7-230">Sur le ruban **Développer**, cliquez sur **Compléments COM** et confirmez que le complément COM Excel HPC Pack est chargé.</span><span class="sxs-lookup"><span data-stu-id="60be7-230">On the **Develop** ribbon, click **COM Add-Ins** and confirm that the HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![Complément Excel pour HPC Pack][addin]
8. <span data-ttu-id="60be7-232">Modifiez la macro VBA HPCControlMacros dans Excel en modifiant les lignes commentées, comme illustré dans le script suivant.</span><span class="sxs-lookup"><span data-stu-id="60be7-232">Edit the VBA macro HPCControlMacros in Excel by changing the commented lines as shown in the following script.</span></span> <span data-ttu-id="60be7-233">Remplacez les valeurs par celles appropriées pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="60be7-233">Substitute appropriate values for your environment.</span></span>
   
   ![Macro Excel pour HPC Pack][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. <span data-ttu-id="60be7-235">Copiez le classeur Excel dans un répertoire de téléchargement tel que D:\Excel\Upload.</span><span class="sxs-lookup"><span data-stu-id="60be7-235">Copy the Excel workbook to an upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="60be7-236">Ce répertoire est spécifié dans la constante HPC_DependsFiles dans la macro VBA.</span><span class="sxs-lookup"><span data-stu-id="60be7-236">This directory is specified in the HPC_DependsFiles constant in the VBA macro.</span></span>
10. <span data-ttu-id="60be7-237">Pour exécuter le classeur sur le cluster dans Azure, cliquez sur le bouton **Cluster** sur la feuille de calcul.</span><span class="sxs-lookup"><span data-stu-id="60be7-237">To run the workbook on the cluster in Azure, click the **Cluster** button on the worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="60be7-238">Exécution d’UDF Excel</span><span class="sxs-lookup"><span data-stu-id="60be7-238">Run Excel UDFs</span></span>
<span data-ttu-id="60be7-239">Pour exécuter des UDF Excel, suivez les étapes 1 à 3 précédentes pour configurer l'ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="60be7-239">To run Excel UDFs, follow the preceding steps 1 – 3 to set up the client computer.</span></span> <span data-ttu-id="60be7-240">Pour des UDF Excel, vous n’avez pas besoin d’installer l’application Excel sur les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="60be7-240">For Excel UDFs, you don't need to have the Excel application installed on compute nodes.</span></span> <span data-ttu-id="60be7-241">Par conséquent, lors de la création des nœuds de calcul de votre cluster, vous pouvez choisir une image de nœud de calcul normale au lieu de l’image de nœud de calcul Excel.</span><span class="sxs-lookup"><span data-stu-id="60be7-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of the compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="60be7-242">Il existe une limite de 34 caractères dans la boîte de dialogue de connecteur de cluster dans Excel 2010 et 2013.</span><span class="sxs-lookup"><span data-stu-id="60be7-242">There is a 34 character limit in the Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="60be7-243">Cette boîte de dialogue vous permet de spécifier le cluster qui exécute les UDF.</span><span class="sxs-lookup"><span data-stu-id="60be7-243">You use this dialog box to specify the cluster that runs the UDFs.</span></span> <span data-ttu-id="60be7-244">Si le nom de cluster complet est plus long (par exemple hpcexcelhn01.southeastasia.cloudapp.azure.com), il ne tient pas dans la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="60be7-244">If the full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in the dialog box.</span></span> <span data-ttu-id="60be7-245">La solution consiste à définir une variable à l’échelle de la machine (telle que *CCP_IAASHN*) avec la valeur du nom de cluster trop long.</span><span class="sxs-lookup"><span data-stu-id="60be7-245">The workaround is to set a machine-wide variable such as *CCP_IAASHN* with the value of the long cluster name.</span></span> <span data-ttu-id="60be7-246">Entrez ensuite *%CCP_IAASHN%* dans la boîte de dialogue en tant que le nom de nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="60be7-246">Then, enter *%CCP_IAASHN%* in the dialog box as the cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="60be7-247">Une fois le cluster déployé, poursuivez avec les étapes suivantes pour exécuter un exemple intégré d’UDF Excel.</span><span class="sxs-lookup"><span data-stu-id="60be7-247">After the cluster is successfully deployed, continue with the following steps to run a sample built-in Excel UDF.</span></span> <span data-ttu-id="60be7-248">Pour les UDF Excel personnalisées, consultez ces [ressources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) pour générer les XLL et les déployer sur le cluster IaaS.</span><span class="sxs-lookup"><span data-stu-id="60be7-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) to build the XLLs and deploy them on the IaaS cluster.</span></span>

1. <span data-ttu-id="60be7-249">Ouvrez un nouveau classeur Excel.</span><span class="sxs-lookup"><span data-stu-id="60be7-249">Open a new Excel workbook.</span></span> <span data-ttu-id="60be7-250">Dans le ruban **Développer**, cliquez sur **Compléments**.</span><span class="sxs-lookup"><span data-stu-id="60be7-250">On the **Develop** ribbon, click **Add-Ins**.</span></span> <span data-ttu-id="60be7-251">Puis, dans la boîte de dialogue, cliquez sur **Parcourir**, accédez au dossier %CCP_HOME%Bin\XLL32 et sélectionnez l’exemple ClusterUDF32.xll.</span><span class="sxs-lookup"><span data-stu-id="60be7-251">Then, in the dialog box, click **Browse**, navigate to the %CCP_HOME%Bin\XLL32 folder, and select the sample ClusterUDF32.xll.</span></span> <span data-ttu-id="60be7-252">Si le ClusterUDF32 n'existe pas sur la machine cliente, copiez-le à partir du dossier %CCP_HOME%Bin\XLL32 sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="60be7-252">If the ClusterUDF32 doesn't exist on the client machine, copy it from the %CCP_HOME%Bin\XLL32 folder on the head node.</span></span>
   
   ![Sélection de l'UDF][udf]
2. <span data-ttu-id="60be7-254">Cliquez sur **Fichier** > **Options** > **Avancé**.</span><span class="sxs-lookup"><span data-stu-id="60be7-254">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="60be7-255">Sous **Formules**, cochez l’option **Autoriser l’exécution de fonctions XLL définies par l’utilisateur sur un cluster de calcul**.</span><span class="sxs-lookup"><span data-stu-id="60be7-255">Under **Formulas**, check **Allow user-defined XLL functions to run a compute cluster**.</span></span> <span data-ttu-id="60be7-256">Puis cliquez sur **Options** et entrez le nom de cluster complet dans **Nom de nœud principal du cluster**.</span><span class="sxs-lookup"><span data-stu-id="60be7-256">Then click **Options** and enter the full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="60be7-257">(Comme indiqué précédemment, cette zone de saisie est limitée à 34 caractères, un nom de cluster plus long peut ne pas entrer.</span><span class="sxs-lookup"><span data-stu-id="60be7-257">(As noted previously this input box is limited to 34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="60be7-258">Vous pouvez utiliser des variables au niveau de la machine ici pour les noms de cluster longs.)</span><span class="sxs-lookup"><span data-stu-id="60be7-258">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Configuration de l’UDF][options]
3. <span data-ttu-id="60be7-260">Pour exécuter le calcul UDF sur le cluster, cliquez sur la cellule qui contient la valeur =XllGetComputerNameC() et appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="60be7-260">To run the UDF calculation on the cluster, click the cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="60be7-261">La fonction récupère simplement le nom du nœud de calcul sur lequel s'exécute l'UDF.</span><span class="sxs-lookup"><span data-stu-id="60be7-261">The function simply retrieves the name of the compute node on which the UDF runs.</span></span> <span data-ttu-id="60be7-262">Lors de la première exécution, une boîte de dialogue d’informations d'identification vous invite à entrer le nom d'utilisateur et un mot de passe pour vous connecter au cluster IaaS.</span><span class="sxs-lookup"><span data-stu-id="60be7-262">For the first run, a credentials dialog box prompts for the username and password to connect to the IaaS cluster.</span></span>
   
   ![Exécution de l’UDF][run]
   
   <span data-ttu-id="60be7-264">S’il faut calculer beaucoup de cellules, appuyez sur Alt-Maj-Ctrl + F9 pour exécuter le calcul sur toutes les cellules.</span><span class="sxs-lookup"><span data-stu-id="60be7-264">When there are many cells to calculate, press Alt-Shift-Ctrl + F9 to run the calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="60be7-265">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="60be7-265">Step 3.</span></span> <span data-ttu-id="60be7-266">Exécution d’une charge de travail SOA depuis un client local</span><span class="sxs-lookup"><span data-stu-id="60be7-266">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="60be7-267">Pour exécuter des applications SOA générales sur le cluster HPC Pack IaaS, utilisez tout d’abord l’une des méthodes de l’étape 1 pour déployer le cluster.</span><span class="sxs-lookup"><span data-stu-id="60be7-267">To run general SOA applications on the HPC Pack IaaS cluster, first use one of the methods in Step 1 to deploy the cluster.</span></span> <span data-ttu-id="60be7-268">Dans ce cas, spécifiez une image de nœud de calcul générique, car vous n’avez pas besoin d’Excel sur les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="60be7-268">Specify a generic compute node image in this case, because you do not need Excel on the compute nodes.</span></span> <span data-ttu-id="60be7-269">Puis, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="60be7-269">Then follow these steps.</span></span>

1. <span data-ttu-id="60be7-270">Après avoir récupéré le certificat du cluster, importez-le sur l'ordinateur client sous Cert:\CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="60be7-270">After retrieving the cluster certificate, import it on the client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="60be7-271">Installez le [Kit de développement logiciel (SDK) HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49921) et [les utilitaires clients HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="60be7-271">Install the [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="60be7-272">Ces outils vous permettent de développer et d’exécuter des applications clientes SOA.</span><span class="sxs-lookup"><span data-stu-id="60be7-272">These tools enable you to develop and run SOA client applications.</span></span>
3. <span data-ttu-id="60be7-273">Téléchargez [l’exemple de code](https://www.microsoft.com/download/details.aspx?id=41633)HelloWorldR2.</span><span class="sxs-lookup"><span data-stu-id="60be7-273">Download the HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="60be7-274">Ouvrez HelloWorldR2.sln dans Visual Studio 2010 ou 2012.</span><span class="sxs-lookup"><span data-stu-id="60be7-274">Open the HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="60be7-275">(Cet exemple n’est pas compatible actuellement avec les versions plus récentes de Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="60be7-275">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="60be7-276">Générez tout d’abord le projet EchoService.</span><span class="sxs-lookup"><span data-stu-id="60be7-276">Build the EchoService project first.</span></span> <span data-ttu-id="60be7-277">Déployez le service sur le cluster IaaS de la même manière que pour un déploiement sur un cluster local.</span><span class="sxs-lookup"><span data-stu-id="60be7-277">Then, deploy the service to the IaaS cluster in the same way you deploy to an on-premises cluster.</span></span> <span data-ttu-id="60be7-278">Pour des instructions détaillées, consultez le fichier Readme.doc dans HelloWordR2.</span><span class="sxs-lookup"><span data-stu-id="60be7-278">For detailed steps, see the Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="60be7-279">Modifiez et générez le code HellWorldR2 et d’autres projets comme décrit dans la section suivante pour générer les applications clientes SOA qui s’exécutent sur un cluster IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="60be7-279">Modify and build the HellWorldR2 and other projects as described in the following section to generate the SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="60be7-280">Utilisation de la liaison HTTP avec la file d'attente de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="60be7-280">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="60be7-281">Pour utiliser une liaison HTTP avec une file d'attente de stockage Azure, apportez quelques modifications à l'exemple de code.</span><span class="sxs-lookup"><span data-stu-id="60be7-281">To use Http binding with an Azure storage queue, make a few changes to the sample code.</span></span>

* <span data-ttu-id="60be7-282">Mettez le nom du cluster à jour.</span><span class="sxs-lookup"><span data-stu-id="60be7-282">Update the cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="60be7-283">Si vous le souhaitez, utilisez la valeur TransportScheme par défaut dans SessionStartInfo ou définissez-la explicitement sur HTTP.</span><span class="sxs-lookup"><span data-stu-id="60be7-283">Optionally, use the default TransportScheme in SessionStartInfo or explicitly set it to Http.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="60be7-284">Utilisez la liaison par défaut pour le BrokerClient.</span><span class="sxs-lookup"><span data-stu-id="60be7-284">Use default binding for the BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="60be7-285">Ou définissez-la explicitement à l'aide de basicHttpBinding.</span><span class="sxs-lookup"><span data-stu-id="60be7-285">Or set explicitly using the basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="60be7-286">Éventuellement, définissez l'indicateur UseAzureQueue sur true dans SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="60be7-286">Optionally, set the UseAzureQueue flag to true in SessionStartInfo.</span></span> <span data-ttu-id="60be7-287">S’il n’est pas défini, il est défini comme true par défaut lorsque le nom de cluster a des suffixes de domaine Azure et que le TransportScheme est HTTP.</span><span class="sxs-lookup"><span data-stu-id="60be7-287">If not set, it will be set to true by default when the cluster name has Azure domain suffixes and the TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="60be7-288">Utilisation de la liaison HTTP sans la file d'attente de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="60be7-288">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="60be7-289">Pour utiliser une liaison Http sans une file d’attente de stockage Azure, vous devez définir explicitement l’indicateur UseAzureQueue sur false dans SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="60be7-289">To use Http binding without an Azure storage queue, explicitly set the UseAzureQueue flag to false in the SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="60be7-290">Utilisation de la liaison NetTcp</span><span class="sxs-lookup"><span data-stu-id="60be7-290">Use NetTcp binding</span></span>
<span data-ttu-id="60be7-291">Pour utiliser une liaison NetTcp, la configuration est la même que pour se connecter à un cluster local.</span><span class="sxs-lookup"><span data-stu-id="60be7-291">To use NetTcp binding, the configuration is similar to connecting to an on-premises cluster.</span></span> <span data-ttu-id="60be7-292">Vous devez ouvrir quelques points de terminaison sur la machine virtuelle du nœud principal.</span><span class="sxs-lookup"><span data-stu-id="60be7-292">You need to open a few endpoints on the head node VM.</span></span> <span data-ttu-id="60be7-293">Si vous avez utilisé le script de déploiement HPC Pack IaaS pour créer le cluster, par exemple, définissez les points de terminaison dans le portail Azure comme suit.</span><span class="sxs-lookup"><span data-stu-id="60be7-293">If you used the HPC Pack IaaS deployment script to create the cluster, for example, set the endpoints in the Azure portal as follows.</span></span>

1. <span data-ttu-id="60be7-294">Arrêtez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60be7-294">Stop the VM.</span></span>
2. <span data-ttu-id="60be7-295">Ajoutez les ports TCP 9090, 9087, 9091 et 9094 pour les services Session, Broker, worker Broker et de données respectivement</span><span class="sxs-lookup"><span data-stu-id="60be7-295">Add the TCP ports 9090, 9087, 9091, 9094 for the Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Configuration des points de terminaison][endpoint-new-portal]
3. <span data-ttu-id="60be7-297">Démarrez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="60be7-297">Start the VM.</span></span>

<span data-ttu-id="60be7-298">L'application cliente SOA ne nécessite aucune modification à l'exception de la modification du nom principal en nom complet du cluster IaaS.</span><span class="sxs-lookup"><span data-stu-id="60be7-298">The SOA client application requires no changes except altering the head name to the IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60be7-299">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="60be7-299">Next steps</span></span>
* <span data-ttu-id="60be7-300">Consultez [ces ressources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) pour plus d'informations sur l'exécution de charges de travail Excel avec HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="60be7-300">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="60be7-301">Consultez [Gestion des Services SOA dans Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) pour plus d'informations sur le déploiement et la gestion des services SOA avec HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="60be7-301">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
