---
title: "aaaCreate Hadoop clusters à l’aide de modèles - Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toocreate clusters pour HDInsight à l’aide de modèles de gestionnaire de ressources"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="e8869-103">Créer des clusters Hadoop dans HDInsight avec des modèles Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8869-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="e8869-104">Dans cet article, vous découvrez plusieurs façons toocreate Azure HDInsight clusters avec des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e8869-104">In this article, you learn several ways toocreate Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="e8869-105">Pour plus d’informations, consultez la page [Déploiement d’une application avec un modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e8869-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="e8869-106">toolearn sur d’autres outils de création de cluster et les fonctionnalités, cliquez sur le sélecteur de tabulations hello haut hello de cette page ou de voir [méthodes de création de Cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="e8869-106">toolearn about other cluster creation tools and features, click hello tab selector on hello top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8869-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e8869-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="e8869-108">obtenir des instructions toofollow hello dans cet article, vous devez :</span><span class="sxs-lookup"><span data-stu-id="e8869-108">toofollow hello instructions in this article, you'll need:</span></span>

* <span data-ttu-id="e8869-109">Un [abonnement Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e8869-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e8869-110">L’interface de ligne de commande Azure ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8869-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="e8869-111">Modèles Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8869-111">Resource Manager templates</span></span>
<span data-ttu-id="e8869-112">Un modèle de gestionnaire de ressources facilite hello toocreate facile pour votre application dans une opération unique de coordonnées :</span><span class="sxs-lookup"><span data-stu-id="e8869-112">A Resource Manager template makes it easy toocreate hello following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="e8869-113">Clusters HDInsight et leurs ressources dépendantes (par exemple, le compte de stockage par défaut hello)</span><span class="sxs-lookup"><span data-stu-id="e8869-113">HDInsight clusters and their dependent resources (such as hello default storage account)</span></span>
* <span data-ttu-id="e8869-114">Autres ressources (telles que la base de données SQL Azure toouse Apache Sqoop)</span><span class="sxs-lookup"><span data-stu-id="e8869-114">Other resources (such as Azure SQL Database toouse Apache Sqoop)</span></span>

<span data-ttu-id="e8869-115">Dans le modèle de hello, vous définissez des ressources hello qui sont nécessaires pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="e8869-115">In hello template, you define hello resources that are needed for hello application.</span></span> <span data-ttu-id="e8869-116">Vous également spécifiez des valeurs de tooinput de paramètres de déploiement pour les différents environnements.</span><span class="sxs-lookup"><span data-stu-id="e8869-116">You also specify deployment parameters tooinput values for different environments.</span></span> <span data-ttu-id="e8869-117">modèle de Hello se compose de JSON et les expressions que vous utilisez des valeurs de tooconstruct pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="e8869-117">hello template consists of JSON and expressions that you use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="e8869-118">Pour accéder à des exemples de modèles HDInsight, consultez la page [Modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="e8869-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="e8869-119">Utilisez inter-plateformes [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) avec hello [extension du Gestionnaire de ressources](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) ou un modèle de hello texte éditeur toosave dans un fichier sur votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="e8869-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with hello [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor toosave hello template into a file on your workstation.</span></span> <span data-ttu-id="e8869-120">Vous allez apprendre comment toocall hello modèle à l’aide de différentes méthodes.</span><span class="sxs-lookup"><span data-stu-id="e8869-120">You learn how toocall hello template by using different methods.</span></span>

<span data-ttu-id="e8869-121">Pour plus d’informations sur les modèles de gestionnaire de ressources, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="e8869-121">For more information about Resource Manager templates, see hello following articles:</span></span>

* [<span data-ttu-id="e8869-122">Création de modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8869-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="e8869-123">Déployer une application avec des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8869-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="e8869-124">Génération de modèles</span><span class="sxs-lookup"><span data-stu-id="e8869-124">Generate templates</span></span>

<span data-ttu-id="e8869-125">À l’aide de hello portail Azure, vous pouvez configurer toutes les propriétés de hello d’un cluster et puis enregistrez le modèle de hello avant de le déployer.</span><span class="sxs-lookup"><span data-stu-id="e8869-125">By using hello Azure portal, you can configure all hello properties of a cluster and then save hello template before deploying it.</span></span> <span data-ttu-id="e8869-126">Vous pouvez réutiliser les modèles hello.</span><span class="sxs-lookup"><span data-stu-id="e8869-126">You can then reuse hello template.</span></span>

<span data-ttu-id="e8869-127">**toogenerate un modèle à l’aide de hello portail Azure**</span><span class="sxs-lookup"><span data-stu-id="e8869-127">**toogenerate a template by using hello Azure portal**</span></span>

1. <span data-ttu-id="e8869-128">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e8869-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e8869-129">Cliquez sur **nouveau** sur menu gauche hello **Intelligence + analytique**, puis cliquez sur **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e8869-129">Click **New** on hello left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="e8869-130">Suivre les propriétés de tooenter instructions hello.</span><span class="sxs-lookup"><span data-stu-id="e8869-130">Follow hello instructions tooenter properties.</span></span> <span data-ttu-id="e8869-131">Vous pouvez utiliser soit hello **création rapide** ou hello **personnalisé** option.</span><span class="sxs-lookup"><span data-stu-id="e8869-131">You can use either hello **Quick create** or hello **Custom** option.</span></span>
4. <span data-ttu-id="e8869-132">Sur hello **Résumé** , cliquez sur **télécharger le modèle et les paramètres**:</span><span class="sxs-lookup"><span data-stu-id="e8869-132">On hello **Summary** tab, click **Download template and parameters**:</span></span>

    ![Téléchargement de modèle Resource Manager pour la création de clusters Hadoop dans HDInsight](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="e8869-134">Vous consultez une liste des fichiers de modèle hello, fichier de paramètres et le modèle de code échantillons utilisés toodeploy hello :</span><span class="sxs-lookup"><span data-stu-id="e8869-134">You see a list of hello template file, parameters file, and code samples used toodeploy hello template:</span></span>

    ![Option de téléchargement de modèle Resource Manager pour la création de clusters Hadoop dans HDInsight](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="e8869-136">À ce stade, vous pouvez télécharger le modèle de hello, enregistrer la bibliothèque de modèles tooyour ou déployer le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="e8869-136">From here, you can download hello template, save it tooyour template library, or deploy hello template.</span></span>

    <span data-ttu-id="e8869-137">tooaccess un modèle dans votre bibliothèque, cliquez sur **davantage de services** dans le menu de gauche hello, puis cliquez sur **modèles** (sous hello **autres** catégorie).</span><span class="sxs-lookup"><span data-stu-id="e8869-137">tooaccess a template in your library, click **More services** from hello left menu, and then click **Templates** (under hello **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="e8869-138">fichier de modèle et les paramètres Hello doit être utilisé ensemble.</span><span class="sxs-lookup"><span data-stu-id="e8869-138">hello template and parameters file must be used together.</span></span> <span data-ttu-id="e8869-139">Sinon, vous obtiendrez peut-être des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="e8869-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="e8869-140">Par exemple, hello par défaut **clusterKind** valeur de propriété est toujours **hadoop**, malgré ce que vous spécifiez avant de télécharger le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="e8869-140">For example, hello default **clusterKind** property value is always **hadoop**, despite what you specify before you download hello template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="e8869-141">Déployer avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8869-141">Deploy with PowerShell</span></span>

<span data-ttu-id="e8869-142">Cette procédure crée un cluster Hadoop dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8869-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="e8869-143">Enregistrez le fichier JSON de hello Bonjour [annexe](#appx-a-arm-template) tooyour de station de travail.</span><span class="sxs-lookup"><span data-stu-id="e8869-143">Save hello JSON file in hello [Appendix](#appx-a-arm-template) tooyour workstation.</span></span> <span data-ttu-id="e8869-144">Bonjour script PowerShell, nom du fichier hello est `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="e8869-144">In hello PowerShell script, hello file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="e8869-145">Définir des variables et paramètres de hello si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e8869-145">Set hello parameters and variables if needed.</span></span>
3. <span data-ttu-id="e8869-146">Modèle de hello exécution à l’aide de hello PowerShell script suivant :</span><span class="sxs-lookup"><span data-stu-id="e8869-146">Run hello template by using hello following PowerShell script:</span></span>

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="e8869-147">Hello script PowerShell configure uniquement le nom de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e8869-147">hello PowerShell script configures only hello cluster name.</span></span> <span data-ttu-id="e8869-148">nom de compte de stockage Hello est codé en dur dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="e8869-148">hello storage account name is hard-coded in hello template.</span></span> <span data-ttu-id="e8869-149">Vous êtes invité à tooenter hello cluster mot de passe.</span><span class="sxs-lookup"><span data-stu-id="e8869-149">You are prompted tooenter hello cluster user password.</span></span> <span data-ttu-id="e8869-150">(nom d’utilisateur par défaut de hello est **admin**.) Vous êtes également invité à tooenter hello SSH mot de passe.</span><span class="sxs-lookup"><span data-stu-id="e8869-150">(hello default username is **admin**.) You are also prompted tooenter hello SSH user password.</span></span> <span data-ttu-id="e8869-151">(le nom d’utilisateur SSH hello par défaut est **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="e8869-151">(hello default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="e8869-152">Pour plus d’informations, consultez la rubrique [Déploiement avec PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="e8869-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="e8869-153">Déploiement avec la CLI</span><span class="sxs-lookup"><span data-stu-id="e8869-153">Deploy with CLI</span></span>
<span data-ttu-id="e8869-154">Hello suivant l’exemple utilise Azure interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="e8869-154">hello following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="e8869-155">Il appelle un modèle Resource Manager pour créer un cluster, son compte de stockage dépendant et son conteneur :</span><span class="sxs-lookup"><span data-stu-id="e8869-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="e8869-156">Vous êtes invité à tooenter :</span><span class="sxs-lookup"><span data-stu-id="e8869-156">You are prompted tooenter:</span></span>
* <span data-ttu-id="e8869-157">nom du cluster Hello.</span><span class="sxs-lookup"><span data-stu-id="e8869-157">hello cluster name.</span></span>
* <span data-ttu-id="e8869-158">mot de passe utilisateur de cluster Hello.</span><span class="sxs-lookup"><span data-stu-id="e8869-158">hello cluster user password.</span></span> <span data-ttu-id="e8869-159">(nom d’utilisateur par défaut de hello est **admin**.)</span><span class="sxs-lookup"><span data-stu-id="e8869-159">(hello default username is **admin**.)</span></span>
* <span data-ttu-id="e8869-160">mot de passe utilisateur SSH Hello.</span><span class="sxs-lookup"><span data-stu-id="e8869-160">hello SSH user password.</span></span> <span data-ttu-id="e8869-161">(le nom d’utilisateur SSH hello par défaut est **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="e8869-161">(hello default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="e8869-162">Hello suivant le code fournit des paramètres inclus :</span><span class="sxs-lookup"><span data-stu-id="e8869-162">hello following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="e8869-163">Déployer avec hello API REST</span><span class="sxs-lookup"><span data-stu-id="e8869-163">Deploy with hello REST API</span></span>
<span data-ttu-id="e8869-164">Consultez [déployer avec l’API REST de hello](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="e8869-164">See [Deploy with hello REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="e8869-165">Déployer avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e8869-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="e8869-166">Utilisez Visual Studio toocreate un projet de groupe de ressources et de déploiement tooAzure via l’interface utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="e8869-166">Use Visual Studio toocreate a resource group project and deploy it tooAzure through hello user interface.</span></span> <span data-ttu-id="e8869-167">Vous sélectionnez le type hello de tooinclude de ressources dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="e8869-167">You select hello type of resources tooinclude in your project.</span></span> <span data-ttu-id="e8869-168">Ces ressources sont automatiquement ajoutés toohello Gestionnaire de ressources du modèle.</span><span class="sxs-lookup"><span data-stu-id="e8869-168">Those resources are automatically added toohello Resource Manager template.</span></span> <span data-ttu-id="e8869-169">projet de Hello fournit également un modèle de hello de toodeploy de script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e8869-169">hello project also provides a PowerShell script toodeploy hello template.</span></span>

<span data-ttu-id="e8869-170">Pour une introduction toousing Visual Studio avec des groupes de ressources, consultez [création et déploiement des groupes de ressources Azure via Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e8869-170">For an introduction toousing Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="e8869-171">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="e8869-171">Troubleshoot</span></span>

<span data-ttu-id="e8869-172">Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="e8869-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8869-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e8869-173">Next steps</span></span>
<span data-ttu-id="e8869-174">Dans cet article, vous avez appris plusieurs façons toocreate un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e8869-174">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="e8869-175">toolearn, voir hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="e8869-175">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="e8869-176">Pour obtenir un exemple de déploiement de ressources via la bibliothèque cliente .NET hello, consultez [déployer des ressources à l’aide de bibliothèques .NET et un modèle](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8869-176">For an example of deploying resources through hello .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="e8869-177">Pour obtenir un exemple détaillé de déploiement d’une application, consultez [Approvisionner et déployer des microservices de manière prévisible dans Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="e8869-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="e8869-178">Pour obtenir des conseils sur le déploiement de vos environnements toodifferent de solution, consultez [environnements de développement et de test dans Microsoft Azure](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="e8869-178">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="e8869-179">toolearn sur les sections hello du modèle du Gestionnaire de ressources Azure hello, consultez [création de modèles](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e8869-179">toolearn about hello sections of hello Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e8869-180">Pour obtenir la liste des fonctions hello vous pouvez utiliser dans un modèle Azure Resource Manager, consultez [fonctions de modèle](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="e8869-180">For a list of hello functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a><span data-ttu-id="e8869-181">Annexe : Gestionnaire de ressources du modèle toocreate un cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="e8869-181">Appendix: Resource Manager template toocreate a Hadoop cluster</span></span>
<span data-ttu-id="e8869-182">Hello modèle Azure Resource Manager suivant crée un cluster Hadoop basé sur Linux avec un compte de stockage Azure dépendants hello.</span><span class="sxs-lookup"><span data-stu-id="e8869-182">hello following Azure Resource Manager template creates a Linux-based Hadoop cluster with hello dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="e8869-183">Cet exemple inclut des informations de configuration pour le metastore Hive et le metastore Oozie.</span><span class="sxs-lookup"><span data-stu-id="e8869-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="e8869-184">Supprimer la section de hello ou configurer la section de hello avant d’utiliser le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="e8869-184">Remove hello section or configure hello section before using hello template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a><span data-ttu-id="e8869-185">Annexe : Gestionnaire de ressources du modèle toocreate un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="e8869-185">Appendix: Resource Manager template toocreate a Spark cluster</span></span>

<span data-ttu-id="e8869-186">Cette section fournit un modèle de gestionnaire de ressources que vous pouvez utiliser toocreate un cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="e8869-186">This section provides a Resource Manager template that you can use toocreate an HDInsight Spark cluster.</span></span> <span data-ttu-id="e8869-187">Ce modèle inclut les configurations pour `spark-defaults` et `spark-thrift-sparkconf` (pour les clusters Spark 1.6) et `spark2-defaults` et `spark2-thrift-sparkconf` (pour les clusters Spark 2).</span><span class="sxs-lookup"><span data-stu-id="e8869-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="e8869-188">En outre toothis, HDInsight calcule et définit des configurations telles que `spark.executor.instances`, `spark.executor.memory`, et `spark.executor.cores` selon la taille de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e8869-188">In addition toothis, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on hello cluster size.</span></span> 

<span data-ttu-id="e8869-189">Si vous définissez un paramètre dans une section en tant que partie du modèle hello lui-même, HDInsight ne calculer et définir des autres paramètres de hello hello même section.</span><span class="sxs-lookup"><span data-stu-id="e8869-189">If you set any one parameter in a section as part of hello template itself, HDInsight does not calculate and set hello other parameters of hello same section.</span></span> <span data-ttu-id="e8869-190">Par exemple, le paramètre `spark.executor.instances` est Bonjour `spark-defaults` configuration.</span><span class="sxs-lookup"><span data-stu-id="e8869-190">For example, parameter `spark.executor.instances` is in hello  `spark-defaults` configuration.</span></span> <span data-ttu-id="e8869-191">Si vous définissez un autre paramètre (par exemple, `spark.yarn.exector.memoryOverhead`) Bonjour `spark-defaults` configuration, HDInsight ne pas calculer et définir hello `spark.executor.instances` également le paramètre.</span><span class="sxs-lookup"><span data-stu-id="e8869-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in hello `spark-defaults` configuration, HDInsight does not calculate and set hello `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
