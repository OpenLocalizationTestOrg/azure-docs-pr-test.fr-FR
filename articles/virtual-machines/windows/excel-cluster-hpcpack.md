---
title: aaaHPC Pack de cluster pour Excel et SOA | Documents Microsoft
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
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="1425c-103">Prise en main de l’exécution de charges de travail Excel et SOA sur un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="1425c-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="1425c-104">Cet article explique comment toodeploy un Microsoft HPC Pack 2012 R2 de cluster sur des machines virtuelles à l’aide d’un modèle de démarrage rapide Azure, ou éventuellement un script de déploiement d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1425c-104">This article shows you how toodeploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="1425c-105">cluster de Hello utilise conçus des images de machine virtuelle de Azure Marketplace toorun Microsoft Excel ou de charges de travail architecture orientée services (SOA) avec HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="1425c-105">hello cluster uses Azure Marketplace VM images designed toorun Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="1425c-106">Vous pouvez utiliser hello toorun de cluster HPC d’Excel et des services SOA à partir d’un ordinateur de client local.</span><span class="sxs-lookup"><span data-stu-id="1425c-106">You can use hello cluster toorun Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="1425c-107">Hello Excel HPC services incluent le déchargement de classeur Excel et les fonctions définies par l’utilisateur Excel ou UDF.</span><span class="sxs-lookup"><span data-stu-id="1425c-107">hello Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="1425c-108">Cet article est basé sur les fonctionnalités, les modèles et les scripts pour HPC Pack 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="1425c-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="1425c-109">Ce scénario n’est pas pris en charge dans HPC Pack 2016 pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="1425c-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="1425c-110">À un niveau élevé, hello diagramme suivant montre hello HPC Pack cluster que vous créez.</span><span class="sxs-lookup"><span data-stu-id="1425c-110">At a high level, hello following diagram shows hello HPC Pack cluster you create.</span></span>

![Cluster HPC avec des nœuds exécutant des charges de travail Excel][scenario]

## <a name="prerequisites"></a><span data-ttu-id="1425c-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1425c-112">Prerequisites</span></span>
* <span data-ttu-id="1425c-113">**Ordinateur client** -vous besoin d’un cluster de toohello travaux clients basés sur Windows ordinateur toosubmit exemple Excel et SOA.</span><span class="sxs-lookup"><span data-stu-id="1425c-113">**Client computer** - You need a Windows-based client computer toosubmit sample Excel and SOA jobs toohello cluster.</span></span> <span data-ttu-id="1425c-114">Vous devez également un Bonjour de toorun de l’ordinateur Windows Azure PowerShell script de déploiement du cluster (si vous choisissez cette méthode de déploiement).</span><span class="sxs-lookup"><span data-stu-id="1425c-114">You also need a Windows computer toorun hello Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="1425c-115">**Abonnement Azure** : si vous n’en avez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="1425c-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="1425c-116">**Quota de cœurs** -vous devrez peut-être le quota de hello tooincrease de cœurs, surtout si vous déployez plusieurs nœuds de cluster avec des tailles de machine virtuelle multicœurs.</span><span class="sxs-lookup"><span data-stu-id="1425c-116">**Cores quota** - You might need tooincrease hello quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="1425c-117">Si vous utilisez un modèle de démarrage rapide Azure, le quota de cœurs hello dans le Gestionnaire de ressources est par région Azure.</span><span class="sxs-lookup"><span data-stu-id="1425c-117">If you are using an Azure quickstart template, hello cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="1425c-118">Dans ce cas, vous devrez peut-être quota de hello tooincrease dans une région spécifique.</span><span class="sxs-lookup"><span data-stu-id="1425c-118">In that case, you might need tooincrease hello quota in a specific region.</span></span> <span data-ttu-id="1425c-119">Consultez [Abonnement Azure et limites, quotas et contraintes du service](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="1425c-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="1425c-120">tooincrease un quota, [ouvrir une demande de support client en ligne](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) sans frais.</span><span class="sxs-lookup"><span data-stu-id="1425c-120">tooincrease a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="1425c-121">**Licence Microsoft Office** : si vous déployez des nœuds de calcul à l’aide d’une image de machine virtuelle HPC Pack 2012 R2 de la Place de marché avec Microsoft Excel, une version d’évaluation de Microsoft Excel Professionnel Plus 2013 est installée et valable pendant 30 jours.</span><span class="sxs-lookup"><span data-stu-id="1425c-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="1425c-122">Après la période d’évaluation hello, vous devez tooprovide une valide Microsoft Office licence tooactivate Excel toocontinue toorun les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="1425c-122">After hello evaluation period, you need tooprovide a valid Microsoft Office license tooactivate Excel toocontinue toorun workloads.</span></span> <span data-ttu-id="1425c-123">Consultez [Activation d’Excel](#excel-activation) plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="1425c-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="1425c-124">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="1425c-124">Step 1.</span></span> <span data-ttu-id="1425c-125">Configuration d’un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="1425c-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="1425c-126">Nous allons montrer deux tooset options cluster HPC Pack 2012 R2 de hello : première, à l’aide d’un modèle de démarrage rapide Azure et un hello portail Azure ; et, ensuite, à l’aide d’un script de déploiement d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1425c-126">We show two options tooset up hello HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and hello Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="1425c-127">Option 1.</span><span class="sxs-lookup"><span data-stu-id="1425c-127">Option 1.</span></span> <span data-ttu-id="1425c-128">Utilisation d’un modèle de démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="1425c-128">Use a quickstart template</span></span>
<span data-ttu-id="1425c-129">Utilisez un tooquickly de modèle de démarrage rapide Azure déployer un cluster HPC Pack dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1425c-129">Use an Azure quickstart template tooquickly deploy an HPC Pack cluster in hello Azure portal.</span></span> <span data-ttu-id="1425c-130">Lorsque vous ouvrez un modèle de hello dans le portail de hello, vous obtenez une interface utilisateur simple, où vous entrez des paramètres de hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="1425c-130">When you open hello template in hello portal, you get a simple UI where you enter hello settings for your cluster.</span></span> <span data-ttu-id="1425c-131">Voici les étapes hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-131">Here are hello steps.</span></span> 

> [!TIP]
> <span data-ttu-id="1425c-132">Si vous le souhaitez, utilisez un [modèle Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) qui crée un cluster similaire spécialement pour les charges de travail Excel.</span><span class="sxs-lookup"><span data-stu-id="1425c-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="1425c-133">étapes de Hello est légèrement différentes des options suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-133">hello steps differ slightly from hello following.</span></span>
> 
> 

1. <span data-ttu-id="1425c-134">Visitez hello [page modèle de création d’un Cluster HPC sur GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="1425c-134">Visit hello [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="1425c-135">Si vous le souhaitez, passez en revue les informations sur le modèle de hello et le code source de hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-135">If you want, review information about hello template and hello source code.</span></span>
2. <span data-ttu-id="1425c-136">Cliquez sur **déployer tooAzure** toostart un déploiement avec le modèle hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1425c-136">Click **Deploy tooAzure** toostart a deployment with hello template in hello Azure portal.</span></span>
   
   ![Déployer le modèle tooAzure][github]
3. <span data-ttu-id="1425c-138">Dans le portail de hello, suivez ces étapes tooenter hello les paramètres pour le modèle de cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-138">In hello portal, follow these steps tooenter hello parameters for hello HPC cluster template.</span></span>
   
   <span data-ttu-id="1425c-139">a.</span><span class="sxs-lookup"><span data-stu-id="1425c-139">a.</span></span> <span data-ttu-id="1425c-140">Sur hello **paramètres** page, entrez ou modifiez les valeurs des paramètres du modèle hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-140">On hello **Parameters** page, enter or modify values for hello template parameters.</span></span> <span data-ttu-id="1425c-141">(Cliquez sur le paramètre suivant tooeach hello icône pour les informations d’aide.) Exemples de valeurs sont affichés dans hello suivant l’écran.</span><span class="sxs-lookup"><span data-stu-id="1425c-141">(Click hello icon next tooeach setting for help information.) Sample values are shown in hello following screen.</span></span> <span data-ttu-id="1425c-142">Cet exemple crée un cluster nommé *hpc01* Bonjour *hpc.local* domaine constitué d’un nœud principal et 2 nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="1425c-142">This example creates a cluster named *hpc01* in hello *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="1425c-143">les nœuds de calcul Hello sont créés à partir d’une image de machine virtuelle HPC Pack qui inclut Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="1425c-143">hello compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Saisie des paramètres][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="1425c-145">machine virtuelle est créée automatiquement à partir de hello du nœud principal Hello [dernière image Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) de HPC Pack 2012 R2 sur Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="1425c-145">hello head node VM is created automatically from hello [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="1425c-146">Actuellement, les images hello sont basée sur HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="1425c-146">Currently hello image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="1425c-147">Machines virtuelles de nœud de calcul sont créés à partir de la dernière image de hello de famille de nœud de calcul hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="1425c-147">Compute node VMs are created from hello latest image of hello selected compute node family.</span></span> <span data-ttu-id="1425c-148">Sélectionnez hello **ComputeNodeWithExcel** option pour hello dernière HPC Pack calcul nœud image qui inclut une version d’évaluation de Microsoft Excel Professionnel Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="1425c-148">Select hello **ComputeNodeWithExcel** option for hello latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="1425c-149">toodeploy un cluster pour les sessions SOA générales ou pour le déchargement de l’UDF d’Excel, choisissez hello **ComputeNode** option (sans Excel installé).</span><span class="sxs-lookup"><span data-stu-id="1425c-149">toodeploy a cluster for general SOA sessions or for Excel UDF offloading, choose hello **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="1425c-150">b.</span><span class="sxs-lookup"><span data-stu-id="1425c-150">b.</span></span> <span data-ttu-id="1425c-151">Choisissez un abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-151">Choose hello subscription.</span></span>
   
   <span data-ttu-id="1425c-152">c.</span><span class="sxs-lookup"><span data-stu-id="1425c-152">c.</span></span> <span data-ttu-id="1425c-153">Créer un groupe de ressources de cluster de hello, tel que *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="1425c-153">Create a resource group for hello cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="1425c-154">d.</span><span class="sxs-lookup"><span data-stu-id="1425c-154">d.</span></span> <span data-ttu-id="1425c-155">Choisissez un emplacement pour le groupe de ressources hello, tels que du centre des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="1425c-155">Choose a location for hello resource group, such as Central US.</span></span>
   
   <span data-ttu-id="1425c-156">e.</span><span class="sxs-lookup"><span data-stu-id="1425c-156">e.</span></span> <span data-ttu-id="1425c-157">Sur hello **juridiques** , lisez les termes du contrat de hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-157">On hello **Legal terms** page, review hello terms.</span></span> <span data-ttu-id="1425c-158">Si vous les acceptez, cliquez sur **Acheter**.</span><span class="sxs-lookup"><span data-stu-id="1425c-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="1425c-159">Ensuite, lorsque vous avez terminé la définition des valeurs hello pour le modèle de hello, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="1425c-159">Then, when you are finished setting hello values for hello template, click **Create**.</span></span>
4. <span data-ttu-id="1425c-160">Lorsque le déploiement de hello se termine (il prend généralement environ 30 minutes), exporter le fichier de certificat de cluster hello hello nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="1425c-160">When hello deployment completes (it typically takes around 30 minutes), export hello cluster certificate file from hello cluster head node.</span></span> <span data-ttu-id="1425c-161">Dans une étape ultérieure, vous importez ce certificat public sur hello ordinateur tooprovide hello côté serveur, l’authentification du client pour la liaison HTTP sécurisée.</span><span class="sxs-lookup"><span data-stu-id="1425c-161">In a later step, you import this public certificate on hello client computer tooprovide hello server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="1425c-162">a.</span><span class="sxs-lookup"><span data-stu-id="1425c-162">a.</span></span> <span data-ttu-id="1425c-163">Bonjour portail Azure, accédez à toohello du tableau de bord, nœud de tête hello sélectionnez, puis cliquez sur **Connect** haut hello hello tooconnect de page à l’aide du Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="1425c-163">In hello Azure portal, go toohello dashboard, select hello head node, and click **Connect** at hello top of hello page tooconnect using Remote Desktop.</span></span>
   
    <!-- ![Connect toohello head node][connect] -->
   
   <span data-ttu-id="1425c-164">b.</span><span class="sxs-lookup"><span data-stu-id="1425c-164">b.</span></span> <span data-ttu-id="1425c-165">Utilisez les procédures standard dans le Gestionnaire de certificats tooexport hello du nœud principal certificat (situé sous Cert : \LocalMachine\My) sans la clé privée de hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-165">Use standard procedures in Certificate Manager tooexport hello head node certificate (located under Cert:\LocalMachine\My) without hello private key.</span></span> <span data-ttu-id="1425c-166">Dans cet exemple, exportez *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="1425c-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Exporter le certificat de hello][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="1425c-168">Option 2.</span><span class="sxs-lookup"><span data-stu-id="1425c-168">Option 2.</span></span> <span data-ttu-id="1425c-169">Utilisez le script de déploiement de IaaS de HPC Pack hello</span><span class="sxs-lookup"><span data-stu-id="1425c-169">Use hello HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="1425c-170">Hello script de déploiement IaaS de HPC Pack fournit une autre façon polyvalente toodeploy un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="1425c-170">hello HPC Pack IaaS deployment script provides another versatile way toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="1425c-171">Il crée un cluster dans le modèle de déploiement classique de hello, tandis que le modèle de hello utilise le modèle de déploiement du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-171">It creates a cluster in hello classic deployment model, whereas hello template uses hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="1425c-172">En outre, le script de hello est compatible avec un abonnement dans hello Global Azure ou le service en Chine d’Azure.</span><span class="sxs-lookup"><span data-stu-id="1425c-172">Also, hello script is compatible with a subscription in either hello Azure Global or Azure China service.</span></span>

<span data-ttu-id="1425c-173">**Autres composants requis**</span><span class="sxs-lookup"><span data-stu-id="1425c-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="1425c-174">**Azure PowerShell** - [installez et configurez Azure PowerShell](/powershell/azure/overview) (version 0.8.10 ou ultérieure) sur votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="1425c-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="1425c-175">**Script de déploiement IaaS de HPC Pack** - Téléchargez et décompressez hello dernière version de script hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="1425c-175">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="1425c-176">Vérifier la version de hello du script de hello en exécutant `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="1425c-176">Check hello version of hello script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="1425c-177">Cet article est basé sur la version 4.5.0 ou ultérieure de script de hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-177">This article is based on version 4.5.0 or later of hello script.</span></span>

<span data-ttu-id="1425c-178">**Créer le fichier de configuration hello**</span><span class="sxs-lookup"><span data-stu-id="1425c-178">**Create hello configuration file**</span></span>

 <span data-ttu-id="1425c-179">Hello script de déploiement IaaS de HPC Pack utilise un fichier de configuration XML comme entrée qui décrit l’infrastructure de cluster HPC de hello hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-179">hello HPC Pack IaaS deployment script uses an XML configuration file as input that describes hello infrastructure of hello HPC cluster.</span></span> <span data-ttu-id="1425c-180">toodeploy un cluster constitué d’un nœud principal et 18 nœuds créés à partir de l’image de nœud de calcul hello qui inclut Microsoft Excel, remplacez les valeurs pour votre environnement en hello suivant l’exemple de fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="1425c-180">toodeploy a cluster consisting of a head node and 18 compute nodes created from hello compute node image that includes Microsoft Excel, substitute values for your environment into hello following sample configuration file.</span></span> <span data-ttu-id="1425c-181">Pour plus d’informations sur le fichier de configuration hello, consultez fichier Manual.rtf de hello dans le dossier de scripts hello et [créer un cluster HPC avec hello script de déploiement IaaS de HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1425c-181">For more information about hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="1425c-182">**Remarques sur le fichier de configuration hello**</span><span class="sxs-lookup"><span data-stu-id="1425c-182">**Notes about hello configuration file**</span></span>

* <span data-ttu-id="1425c-183">Hello **VMName** de nœud principal de hello **doit** être même hello comme hello **ServiceName**, ou les travaux SOA échouent toorun.</span><span class="sxs-lookup"><span data-stu-id="1425c-183">hello **VMName** of hello head node **MUST** be hello same as hello **ServiceName**, or SOA jobs fail toorun.</span></span>
* <span data-ttu-id="1425c-184">Veillez à spécifier **EnableWebPortal** afin que hello certificat du nœud principal est généré et exporté.</span><span class="sxs-lookup"><span data-stu-id="1425c-184">Make sure you specify **EnableWebPortal** so that hello head node certificate is generated and exported.</span></span>
* <span data-ttu-id="1425c-185">fichier de Hello spécifie un script PowerShell de post-configuration PostConfig.ps1 qui s’exécute sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-185">hello file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on hello head node.</span></span> <span data-ttu-id="1425c-186">Hello script de l’exemple suivant configure la chaîne de connexion de stockage Windows Azure hello, supprime le rôle de nœud de calcul hello à partir du nœud principal hello et affiche tous les nœuds en ligne lorsqu’ils sont déployés.</span><span class="sxs-lookup"><span data-stu-id="1425c-186">hello following sample script configures hello Azure storage connection string, removes hello compute node role from hello head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
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

<span data-ttu-id="1425c-187">**Exécutez le script de hello**</span><span class="sxs-lookup"><span data-stu-id="1425c-187">**Run hello script**</span></span>

1. <span data-ttu-id="1425c-188">Ouvrez la console PowerShell de hello sur l’ordinateur client de hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1425c-188">Open hello PowerShell console on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="1425c-189">Modifier le dossier de scripts Active toohello (E:\IaaSClusterScript dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="1425c-189">Change directory toohello script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="1425c-190">cluster de HPC Pack hello toodeploy, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="1425c-190">toodeploy hello HPC Pack cluster, run hello following command.</span></span> <span data-ttu-id="1425c-191">Cet exemple suppose que ce fichier de configuration hello se trouve dans E:\HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="1425c-191">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="1425c-192">Hello script de déploiement de HPC Pack s’exécute pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="1425c-192">hello HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="1425c-193">Une chose du script hello est tooexport et télécharger le certificat de cluster hello et l’enregistrer dans le dossier Documents de l’utilisateur actuel hello sur l’ordinateur client de hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-193">One thing hello script does is tooexport and download hello cluster certificate and save it in hello current user’s Documents folder on hello client computer.</span></span> <span data-ttu-id="1425c-194">script de Hello génère un similaire toohello suivante du message.</span><span class="sxs-lookup"><span data-stu-id="1425c-194">hello script generates a message similar toohello following.</span></span> <span data-ttu-id="1425c-195">Dans une étape suivante, vous importez les certificats hello dans le magasin de certificats approprié hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-195">In a following step, you import hello certificate in hello appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="1425c-196">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="1425c-196">Step 2.</span></span> <span data-ttu-id="1425c-197">Déchargement de classeurs Excel et exécution d’UDF à partir d'un client local</span><span class="sxs-lookup"><span data-stu-id="1425c-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="1425c-198">Activation d’Excel</span><span class="sxs-lookup"><span data-stu-id="1425c-198">Excel activation</span></span>
<span data-ttu-id="1425c-199">Lorsque vous utilisez hello image ComputeNodeWithExcel VM pour les charges de production, vous devez tooprovide une valide Microsoft Office licence clé tooactivate Excel sur les nœuds de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-199">When using hello ComputeNodeWithExcel VM image for production workloads, you need tooprovide a valid Microsoft Office license key tooactivate Excel on hello compute nodes.</span></span> <span data-ttu-id="1425c-200">Sinon, version d’évaluation de hello d’Excel expire après 30 jours, et exécute des classeurs Excel échouent avec hello COMException (0x800AC472).</span><span class="sxs-lookup"><span data-stu-id="1425c-200">Otherwise, hello evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with hello COMException (0x800AC472).</span></span> 

<span data-ttu-id="1425c-201">Vous pouvez réarmer Excel 30 jours de la période d’évaluation : ouvrez une session sur le nœud principal de toohello et clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` sur Excel tous les nœuds via HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="1425c-201">You can rearm Excel for another 30 days of evaluation time: Log on toohello head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="1425c-202">Vous pouvez rallonger la période d’évaluation 2 fois au maximum.</span><span class="sxs-lookup"><span data-stu-id="1425c-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="1425c-203">Ensuite, vous devez fournir une clé de licence Office valide.</span><span class="sxs-lookup"><span data-stu-id="1425c-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="1425c-204">Hello Office Professionnel Plus 2013 est installé sur l’image de machine virtuelle hello est une édition en volume avec une clé de licence Volume générique (GVLK).</span><span class="sxs-lookup"><span data-stu-id="1425c-204">hello Office Professional Plus 2013 installed on hello VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="1425c-205">Vous pouvez l’activer par le biais du service de gestion de clés (KMS), de l’activation basée sur Active Directory (AD-BA) ou d’une clé d’activation multiple (MAK).</span><span class="sxs-lookup"><span data-stu-id="1425c-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="1425c-206">toouse KMS/AD-BA, utiliser un serveur KMS existant ou en configurer une autre à l’aide de hello Volume License Pack pour Microsoft Office 2013.</span><span class="sxs-lookup"><span data-stu-id="1425c-206">toouse KMS/AD-BA, use an existing KMS server or set up a new one by using hello Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="1425c-207">(Si vous le souhaitez, configurer hello serveur sur le nœud principal de hello.) Activez ensuite la clé d’hôte KMS hello via hello Internet ou par téléphone.</span><span class="sxs-lookup"><span data-stu-id="1425c-207">(If you want to, set up hello server on hello head node.) Then, activate hello KMS host key via hello Internet or telephone.</span></span> <span data-ttu-id="1425c-208">Puis clusrun `ospp.vbs` tooset hello port et le serveur KMS et activer Office sur tous les nœuds de calcul Excel hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-208">Then clusrun `ospp.vbs` tooset hello KMS server and port and activate Office on all hello Excel compute nodes.</span></span> 

    * <span data-ttu-id="1425c-209">toouse MAK, première clusrun `ospp.vbs` tooinput hello clé et puis activer tous les nœuds de calcul Excel hello via hello Internet ou par téléphone.</span><span class="sxs-lookup"><span data-stu-id="1425c-209">toouse MAK, first clusrun `ospp.vbs` tooinput hello key and then activate all hello Excel compute nodes via hello Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="1425c-210">Les clés de produit commercialisées pour Office Professionnel Plus 2013 ne peuvent pas être utilisées avec cette image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1425c-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="1425c-211">Si vous disposez de clés valides et d’un support d’installation pour des éditions Office ou Excel autres que cette édition en volume Office Professionnel Plus 2013 (édition de volume), vous pouvez également les utiliser.</span><span class="sxs-lookup"><span data-stu-id="1425c-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="1425c-212">Tout d’abord désinstaller cette édition en volume et installer l’édition hello dont vous disposez.</span><span class="sxs-lookup"><span data-stu-id="1425c-212">First uninstall this volume edition and install hello edition that you have.</span></span> <span data-ttu-id="1425c-213">Hello réinstallé Excel de nœud de calcul peut être capturé en tant qu’un personnalisé toouse d’image de machine virtuelle dans un déploiement à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="1425c-213">hello reinstalled Excel compute node can be captured as a customized VM image toouse in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="1425c-214">Déchargement de classeurs Excel</span><span class="sxs-lookup"><span data-stu-id="1425c-214">Offload Excel workbooks</span></span>
<span data-ttu-id="1425c-215">Suivez ces toooffload étapes un classeur Excel afin qu’il s’exécute sur un cluster HPC Pack hello dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1425c-215">Follow these steps toooffload an Excel workbook so that it runs on hello HPC Pack cluster in Azure.</span></span> <span data-ttu-id="1425c-216">toodo, vous devez avoir Excel 2010 ou 2013 est déjà installé sur l’ordinateur client de hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-216">toodo this, you must have Excel 2010 or 2013 already installed on hello client computer.</span></span>

1. <span data-ttu-id="1425c-217">Utilisez une des options de hello dans l’étape 1 toodeploy un cluster HPC Pack avec hello Excel image de nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="1425c-217">Use one of hello options in Step 1 toodeploy an HPC Pack cluster with hello Excel compute node image.</span></span> <span data-ttu-id="1425c-218">Obtenir le fichier de certificat de cluster hello (.cer) et nom d’utilisateur du cluster et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1425c-218">Obtain hello cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="1425c-219">Sur l’ordinateur client de hello, importez le certificat de cluster de hello sous Cert : \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="1425c-219">On hello client computer, import hello cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="1425c-220">Assurez-vous qu'Excel est installé.</span><span class="sxs-lookup"><span data-stu-id="1425c-220">Make sure Excel is installed.</span></span> <span data-ttu-id="1425c-221">Créer un fichier Excel.exe.config avec hello suivant contenu dans hello même dossier que Excel.exe sur l’ordinateur client de hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-221">Create an Excel.exe.config file with hello following contents in hello same folder as Excel.exe on hello client computer.</span></span> <span data-ttu-id="1425c-222">Cette étape garantit que hello complément HPC Pack 2012 R2 Excel COM est chargé avec succès.</span><span class="sxs-lookup"><span data-stu-id="1425c-222">This step ensures that hello HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="1425c-223">Configurer le cluster HPC Pack de hello client toosubmit travaux toohello.</span><span class="sxs-lookup"><span data-stu-id="1425c-223">Set up hello client toosubmit jobs toohello HPC Pack cluster.</span></span> <span data-ttu-id="1425c-224">Une option consiste à hello toodownload complète [installation de HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49922) et installer hello HPC Pack client.</span><span class="sxs-lookup"><span data-stu-id="1425c-224">One option is toodownload hello full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install hello HPC Pack client.</span></span> <span data-ttu-id="1425c-225">Vous pouvez également télécharger et installer hello [les utilitaires clients HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) et hello approprié Visual C++ 2010 redistributable pour votre ordinateur ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="1425c-225">Alternatively, download and install hello [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and hello appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="1425c-226">Dans cet exemple, nous utilisons un exemple de classeur Excel nommé ConvertiblePricing_Complete.xlsb.</span><span class="sxs-lookup"><span data-stu-id="1425c-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="1425c-227">Vous pouvez le télécharger [ici](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="1425c-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="1425c-228">Copiez le dossier de travail hello Excel classeur tooa tels que D:\Excel\Run.</span><span class="sxs-lookup"><span data-stu-id="1425c-228">Copy hello Excel workbook tooa working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="1425c-229">Ouvrez le classeur Excel de hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-229">Open hello Excel workbook.</span></span> <span data-ttu-id="1425c-230">Sur hello **développer** du ruban, cliquez sur **compléments COM** et confirmez que hello HPC Pack Excel complément est chargé avec succès.</span><span class="sxs-lookup"><span data-stu-id="1425c-230">On hello **Develop** ribbon, click **COM Add-Ins** and confirm that hello HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![Complément Excel pour HPC Pack][addin]
8. <span data-ttu-id="1425c-232">Lignes de commentaires modifier hello VBA macro HPCControlMacros dans Excel en modifiant hello comme indiqué dans le script suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-232">Edit hello VBA macro HPCControlMacros in Excel by changing hello commented lines as shown in hello following script.</span></span> <span data-ttu-id="1425c-233">Remplacez les valeurs par celles appropriées pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="1425c-233">Substitute appropriate values for your environment.</span></span>
   
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
9. <span data-ttu-id="1425c-235">Copiez hello Excel classeur tooan téléchargement répertoire tel que D:\Excel\Upload.</span><span class="sxs-lookup"><span data-stu-id="1425c-235">Copy hello Excel workbook tooan upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="1425c-236">Ce répertoire est spécifié dans la constante de HPC_DependsFiles hello dans la macro VBA de hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-236">This directory is specified in hello HPC_DependsFiles constant in hello VBA macro.</span></span>
10. <span data-ttu-id="1425c-237">classeur de hello toorun sur cluster hello dans Azure, cliquez sur hello **Cluster** bouton sur la feuille de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-237">toorun hello workbook on hello cluster in Azure, click hello **Cluster** button on hello worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="1425c-238">Exécution d’UDF Excel</span><span class="sxs-lookup"><span data-stu-id="1425c-238">Run Excel UDFs</span></span>
<span data-ttu-id="1425c-239">toorun Excel UDF, suivez hello étapes précédentes tooset de 1 à 3 d’ordinateur du client hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-239">toorun Excel UDFs, follow hello preceding steps 1 – 3 tooset up hello client computer.</span></span> <span data-ttu-id="1425c-240">Pour Excel UDF, vous n’avez pas besoin toohave hello Excel application installée sur les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="1425c-240">For Excel UDFs, you don't need toohave hello Excel application installed on compute nodes.</span></span> <span data-ttu-id="1425c-241">Par conséquent, lors de la création de votre cluster de nœuds de calcul, vous pouvez choisir une image de nœud de calcul normal au lieu de hello calcul image de nœud avec Excel.</span><span class="sxs-lookup"><span data-stu-id="1425c-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of hello compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="1425c-242">Il existe une limite de 34 caractères Bonjour Excel 2010 et de la boîte de dialogue de connecteur de cluster 2013.</span><span class="sxs-lookup"><span data-stu-id="1425c-242">There is a 34 character limit in hello Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="1425c-243">Vous utilisez ce cluster hello toospecify boîte dialogue qui s’exécute hello UDF.</span><span class="sxs-lookup"><span data-stu-id="1425c-243">You use this dialog box toospecify hello cluster that runs hello UDFs.</span></span> <span data-ttu-id="1425c-244">Si le nom de cluster complet hello est plus long (par exemple, hpcexcelhn01.southeastasia.cloudapp.azure.com), il ne tient pas dans la boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-244">If hello full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in hello dialog box.</span></span> <span data-ttu-id="1425c-245">Bonjour solution de contournement est tooset une variable de l’échelle de l’ordinateur comme *CCP_IAASHN* avec la valeur hello du nom de cluster long hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-245">hello workaround is tooset a machine-wide variable such as *CCP_IAASHN* with hello value of hello long cluster name.</span></span> <span data-ttu-id="1425c-246">Ensuite, entrez *CCP_IAASHN %* dans la boîte de dialogue hello en tant que nom de nœud principal de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-246">Then, enter *%CCP_IAASHN%* in hello dialog box as hello cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="1425c-247">Une fois le cluster de hello est déployé, poursuivre hello suivant les étapes toorun intégré exemple Excel UDF.</span><span class="sxs-lookup"><span data-stu-id="1425c-247">After hello cluster is successfully deployed, continue with hello following steps toorun a sample built-in Excel UDF.</span></span> <span data-ttu-id="1425c-248">Pour des UDF Excel personnalisées, consultez ces [ressources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLL et les déployer sur un cluster IaaS de hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLLs and deploy them on hello IaaS cluster.</span></span>

1. <span data-ttu-id="1425c-249">Ouvrez un nouveau classeur Excel.</span><span class="sxs-lookup"><span data-stu-id="1425c-249">Open a new Excel workbook.</span></span> <span data-ttu-id="1425c-250">Sur hello **développer** du ruban, cliquez sur **compléments**. Puis, dans la boîte de dialogue hello, cliquez sur **Parcourir**, accédez toohello %CCP_HOME%Bin\XLL32 dossier et sélectionnez l’exemple hello ClusterUDF32.xll.</span><span class="sxs-lookup"><span data-stu-id="1425c-250">On hello **Develop** ribbon, click **Add-Ins**. Then, in hello dialog box, click **Browse**, navigate toohello %CCP_HOME%Bin\XLL32 folder, and select hello sample ClusterUDF32.xll.</span></span> <span data-ttu-id="1425c-251">Si hello ClusterUDF32 n’existe pas sur l’ordinateur client de hello, copiez-le à partir du dossier %CCP_HOME%Bin\XLL32 hello sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-251">If hello ClusterUDF32 doesn't exist on hello client machine, copy it from hello %CCP_HOME%Bin\XLL32 folder on hello head node.</span></span>
   
   ![Sélectionnez hello UDF][udf]
2. <span data-ttu-id="1425c-253">Cliquez sur **Fichier** > **Options** > **Avancé**.</span><span class="sxs-lookup"><span data-stu-id="1425c-253">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="1425c-254">Sous **formules**, vérifiez **autoriser toorun de fonctions XLL définies par l’utilisateur à un cluster de calcul**.</span><span class="sxs-lookup"><span data-stu-id="1425c-254">Under **Formulas**, check **Allow user-defined XLL functions toorun a compute cluster**.</span></span> <span data-ttu-id="1425c-255">Puis cliquez sur **Options** et entrez le nom du cluster complète hello dans **nom de nœud principal de Cluster**.</span><span class="sxs-lookup"><span data-stu-id="1425c-255">Then click **Options** and enter hello full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="1425c-256">(Comme indiqué précédemment cette zone d’entrée étant limité too34 caractères, un nom de cluster long peut ne pas correspond.</span><span class="sxs-lookup"><span data-stu-id="1425c-256">(As noted previously this input box is limited too34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="1425c-257">Vous pouvez utiliser des variables au niveau de la machine ici pour les noms de cluster longs.)</span><span class="sxs-lookup"><span data-stu-id="1425c-257">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Configurer hello UDF][options]
3. <span data-ttu-id="1425c-259">toorun hello calcul UDF sur le cluster de hello, cliquez sur la cellule hello avec la valeur =XllGetComputerNameC() et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="1425c-259">toorun hello UDF calculation on hello cluster, click hello cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="1425c-260">fonction Hello extrait simplement le nom hello du nœud de calcul hello sur quel hello UDF s’exécute.</span><span class="sxs-lookup"><span data-stu-id="1425c-260">hello function simply retrieves hello name of hello compute node on which hello UDF runs.</span></span> <span data-ttu-id="1425c-261">Pourquoi exécuter tout d’abord, une boîte de dialogue informations d’identification demande hello nom d’utilisateur et mot de passe tooconnect toohello cluster IaaS.</span><span class="sxs-lookup"><span data-stu-id="1425c-261">For hello first run, a credentials dialog box prompts for hello username and password tooconnect toohello IaaS cluster.</span></span>
   
   ![Exécution de l’UDF][run]
   
   <span data-ttu-id="1425c-263">Lorsqu’il existe de nombreuses cellules toocalculate, appuyez sur Ctrl-Maj-Alt + de calcul de hello toorun F9 sur toutes les cellules.</span><span class="sxs-lookup"><span data-stu-id="1425c-263">When there are many cells toocalculate, press Alt-Shift-Ctrl + F9 toorun hello calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="1425c-264">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="1425c-264">Step 3.</span></span> <span data-ttu-id="1425c-265">Exécution d’une charge de travail SOA depuis un client local</span><span class="sxs-lookup"><span data-stu-id="1425c-265">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="1425c-266">les applications SOA générales toorun sur un cluster IaaS HPC Pack de hello, utilisez d’abord une des méthodes de hello dans un cluster de hello toodeploy étape 1.</span><span class="sxs-lookup"><span data-stu-id="1425c-266">toorun general SOA applications on hello HPC Pack IaaS cluster, first use one of hello methods in Step 1 toodeploy hello cluster.</span></span> <span data-ttu-id="1425c-267">Spécifiez une image de nœud de calcul générique dans ce cas, étant donné que vous n’avez pas besoin d’Excel sur les nœuds de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-267">Specify a generic compute node image in this case, because you do not need Excel on hello compute nodes.</span></span> <span data-ttu-id="1425c-268">Puis, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="1425c-268">Then follow these steps.</span></span>

1. <span data-ttu-id="1425c-269">Après avoir récupéré le certificat de cluster hello, vous devez l’importer sur l’ordinateur client de hello sous Cert : \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="1425c-269">After retrieving hello cluster certificate, import it on hello client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="1425c-270">Installer hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) et [les utilitaires clients HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="1425c-270">Install hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="1425c-271">Ces outils vous toodevelop et exécutent des applications clientes SOA.</span><span class="sxs-lookup"><span data-stu-id="1425c-271">These tools enable you toodevelop and run SOA client applications.</span></span>
3. <span data-ttu-id="1425c-272">Télécharger hello HelloWorldR2 [exemple de code](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="1425c-272">Download hello HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="1425c-273">Ouvrez hello HelloWorldR2.sln dans Visual Studio 2010 ou 2012.</span><span class="sxs-lookup"><span data-stu-id="1425c-273">Open hello HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="1425c-274">(Cet exemple n’est pas compatible actuellement avec les versions plus récentes de Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="1425c-274">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="1425c-275">Générez le projet EchoService de hello tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="1425c-275">Build hello EchoService project first.</span></span> <span data-ttu-id="1425c-276">Ensuite, déployez le cluster IaaS de hello service toohello Bonjour même façon que vous déployez tooan local cluster.</span><span class="sxs-lookup"><span data-stu-id="1425c-276">Then, deploy hello service toohello IaaS cluster in hello same way you deploy tooan on-premises cluster.</span></span> <span data-ttu-id="1425c-277">Pour des instructions détaillées, consultez hello Lisezmoi.doc dans HelloWordR2.</span><span class="sxs-lookup"><span data-stu-id="1425c-277">For detailed steps, see hello Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="1425c-278">Modifier et générer hello HellWorldR2 et autres projets, comme décrit dans hello suivant la section toogenerate hello SOA les applications clientes qui s’exécutent sur un cluster IaaS Azure.</span><span class="sxs-lookup"><span data-stu-id="1425c-278">Modify and build hello HellWorldR2 and other projects as described in hello following section toogenerate hello SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="1425c-279">Utilisation de la liaison HTTP avec la file d'attente de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="1425c-279">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="1425c-280">liaison Http de toouse avec une file d’attente de stockage Azure, apporter quelques modifications toohello exemple de code.</span><span class="sxs-lookup"><span data-stu-id="1425c-280">toouse Http binding with an Azure storage queue, make a few changes toohello sample code.</span></span>

* <span data-ttu-id="1425c-281">Nom de cluster hello mise à jour.</span><span class="sxs-lookup"><span data-stu-id="1425c-281">Update hello cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="1425c-282">Si vous le souhaitez, utilisez la valeur par défaut de hello TransportScheme dans SessionStartInfo ou définir explicitement tooHttp.</span><span class="sxs-lookup"><span data-stu-id="1425c-282">Optionally, use hello default TransportScheme in SessionStartInfo or explicitly set it tooHttp.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="1425c-283">Utilisez la liaison par défaut pour hello BrokerClient.</span><span class="sxs-lookup"><span data-stu-id="1425c-283">Use default binding for hello BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="1425c-284">Ou définies explicitement à l’aide de hello basicHttpBinding.</span><span class="sxs-lookup"><span data-stu-id="1425c-284">Or set explicitly using hello basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="1425c-285">Vous pouvez également définir hello UseAzureQueue indicateur tootrue dans SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="1425c-285">Optionally, set hello UseAzureQueue flag tootrue in SessionStartInfo.</span></span> <span data-ttu-id="1425c-286">Si ce n’est pas le cas, ensemble, elle est définie tootrue par défaut lors de nom de cluster hello possède des suffixes de domaine Azure et hello TransportScheme est Http.</span><span class="sxs-lookup"><span data-stu-id="1425c-286">If not set, it will be set tootrue by default when hello cluster name has Azure domain suffixes and hello TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="1425c-287">Utilisation de la liaison HTTP sans la file d'attente de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="1425c-287">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="1425c-288">liaison Http de toouse sans une file d’attente de stockage Azure, explicitement ensemble hello UseAzureQueue indicateur toofalse Bonjour SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="1425c-288">toouse Http binding without an Azure storage queue, explicitly set hello UseAzureQueue flag toofalse in hello SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="1425c-289">Utilisation de la liaison NetTcp</span><span class="sxs-lookup"><span data-stu-id="1425c-289">Use NetTcp binding</span></span>
<span data-ttu-id="1425c-290">toouse NetTcp liaison, configuration de hello est cluster local de tooan similaire tooconnecting.</span><span class="sxs-lookup"><span data-stu-id="1425c-290">toouse NetTcp binding, hello configuration is similar tooconnecting tooan on-premises cluster.</span></span> <span data-ttu-id="1425c-291">Vous devez tooopen quelques points de terminaison sur la machine virtuelle du nœud principal hello.</span><span class="sxs-lookup"><span data-stu-id="1425c-291">You need tooopen a few endpoints on hello head node VM.</span></span> <span data-ttu-id="1425c-292">Si vous avez utilisé le cluster de hello IaaS HPC Pack déploiement script toocreate hello, par exemple, jeu de points de terminaison hello dans hello portail Azure comme suit.</span><span class="sxs-lookup"><span data-stu-id="1425c-292">If you used hello HPC Pack IaaS deployment script toocreate hello cluster, for example, set hello endpoints in hello Azure portal as follows.</span></span>

1. <span data-ttu-id="1425c-293">Arrêter hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1425c-293">Stop hello VM.</span></span>
2. <span data-ttu-id="1425c-294">Ajouter des ports TCP hello 9090, 9087, 9091, 9094 pour hello Session, service Broker, service Broker de traitement et de services de données, respectivement</span><span class="sxs-lookup"><span data-stu-id="1425c-294">Add hello TCP ports 9090, 9087, 9091, 9094 for hello Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Configuration des points de terminaison][endpoint-new-portal]
3. <span data-ttu-id="1425c-296">Démarrez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1425c-296">Start hello VM.</span></span>

<span data-ttu-id="1425c-297">Hello application cliente SOA ne nécessite aucune modification à l’exception de la modification hello principal toohello IaaS cluster nom complet.</span><span class="sxs-lookup"><span data-stu-id="1425c-297">hello SOA client application requires no changes except altering hello head name toohello IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1425c-298">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1425c-298">Next steps</span></span>
* <span data-ttu-id="1425c-299">Consultez [ces ressources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) pour plus d'informations sur l'exécution de charges de travail Excel avec HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="1425c-299">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="1425c-300">Consultez [Gestion des Services SOA dans Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) pour plus d'informations sur le déploiement et la gestion des services SOA avec HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="1425c-300">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

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
