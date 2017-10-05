---
title: "Créer des clusters Hadoop avec des modèles – Azure HDInsight | Microsoft Docs"
description: "Apprenez à créer des clusters pour HDInsight avec des modèles Resource Manager."
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
ms.openlocfilehash: b2cdc954530daea2a641599c946ce3787149e762
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="d156b-103">Créer des clusters Hadoop dans HDInsight avec des modèles Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d156b-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="d156b-104">Vous trouverez dans cet article différentes façons de créer des clusters Azure HDInsight avec des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d156b-104">In this article, you learn several ways to create Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="d156b-105">Pour plus d’informations, consultez la page [Déploiement d’une application avec un modèle Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d156b-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="d156b-106">Pour découvrir d’autres outils et fonctions de création de clusters, cliquez sur le sélecteur d’onglets situé en haut de cette page, ou consultez la section relative aux [méthodes de création de clusters](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="d156b-106">To learn about other cluster creation tools and features, click the tab selector on the top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d156b-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d156b-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="d156b-108">Pour suivre les instructions de cet article, il vous faudra :</span><span class="sxs-lookup"><span data-stu-id="d156b-108">To follow the instructions in this article, you'll need:</span></span>

* <span data-ttu-id="d156b-109">Un [abonnement Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d156b-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="d156b-110">L’interface de ligne de commande Azure ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d156b-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="d156b-111">Modèles Microsoft Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d156b-111">Resource Manager templates</span></span>
<span data-ttu-id="d156b-112">Un modèle Resource Manager permet de créer les éléments suivants pour votre application en une seule opération coordonnée :</span><span class="sxs-lookup"><span data-stu-id="d156b-112">A Resource Manager template makes it easy to create the following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="d156b-113">des clusters HDInsight et les ressources dépendantes (par exemple, le compte de stockage par défaut) ;</span><span class="sxs-lookup"><span data-stu-id="d156b-113">HDInsight clusters and their dependent resources (such as the default storage account)</span></span>
* <span data-ttu-id="d156b-114">d’autres ressources (par exemple, Azure SQL Database pour utiliser Apache Sqoop).</span><span class="sxs-lookup"><span data-stu-id="d156b-114">Other resources (such as Azure SQL Database to use Apache Sqoop)</span></span>

<span data-ttu-id="d156b-115">Dans le modèle, vous définissez les ressources nécessaires à l’application.</span><span class="sxs-lookup"><span data-stu-id="d156b-115">In the template, you define the resources that are needed for the application.</span></span> <span data-ttu-id="d156b-116">Vous spécifiez également les paramètres de déploiement permettant d’entrer des valeurs pour différents environnements.</span><span class="sxs-lookup"><span data-stu-id="d156b-116">You also specify deployment parameters to input values for different environments.</span></span> <span data-ttu-id="d156b-117">Le modèle se compose d’un JSON et d’expressions permettant de construire des valeurs pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="d156b-117">The template consists of JSON and expressions that you use to construct values for your deployment.</span></span>

<span data-ttu-id="d156b-118">Pour accéder à des exemples de modèles HDInsight, consultez la page [Modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="d156b-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="d156b-119">Utilisez [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) interplateforme avec [l’extension Resource Manager](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) ou un éditeur de texte pour enregistrer le modèle dans un fichier sur votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="d156b-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with the [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor to save the template into a file on your workstation.</span></span> <span data-ttu-id="d156b-120">Vous pourrez apprendre à appeler le modèle avec différentes méthodes.</span><span class="sxs-lookup"><span data-stu-id="d156b-120">You learn how to call the template by using different methods.</span></span>

<span data-ttu-id="d156b-121">Pour plus d’informations sur les modèles Resource Manager, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="d156b-121">For more information about Resource Manager templates, see the following articles:</span></span>

* [<span data-ttu-id="d156b-122">Création de modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d156b-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="d156b-123">Déployer une application avec des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d156b-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="d156b-124">Génération de modèles</span><span class="sxs-lookup"><span data-stu-id="d156b-124">Generate templates</span></span>

<span data-ttu-id="d156b-125">Avec le Portail Azure, vous pouvez configurer toutes les propriétés d’un cluster, puis enregistrer le modèle avant de le déployer.</span><span class="sxs-lookup"><span data-stu-id="d156b-125">By using the Azure portal, you can configure all the properties of a cluster and then save the template before deploying it.</span></span> <span data-ttu-id="d156b-126">Vous pourrez ensuite réutiliser le modèle.</span><span class="sxs-lookup"><span data-stu-id="d156b-126">You can then reuse the template.</span></span>

<span data-ttu-id="d156b-127">**Pour générer un modèle avec le Portail Azure**</span><span class="sxs-lookup"><span data-stu-id="d156b-127">**To generate a template by using the Azure portal**</span></span>

1. <span data-ttu-id="d156b-128">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d156b-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d156b-129">Cliquez sur **Nouveau** dans le menu de gauche, puis sur **Intelligence + analyse** et sur **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d156b-129">Click **New** on the left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="d156b-130">Suivez les instructions pour entrer les propriétés.</span><span class="sxs-lookup"><span data-stu-id="d156b-130">Follow the instructions to enter properties.</span></span> <span data-ttu-id="d156b-131">Vous pouvez utiliser l’option **Création rapide** ou **Personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="d156b-131">You can use either the **Quick create** or the **Custom** option.</span></span>
4. <span data-ttu-id="d156b-132">Dans l’onglet **Résumé**, cliquez sur **Télécharger le modèle et les paramètres** :</span><span class="sxs-lookup"><span data-stu-id="d156b-132">On the **Summary** tab, click **Download template and parameters**:</span></span>

    ![Téléchargement de modèle Resource Manager pour la création de clusters Hadoop dans HDInsight](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="d156b-134">Une liste s’affiche, qui contient le fichier de modèle, le fichier de paramètres et les exemples de code utilisés pour déployer le modèle :</span><span class="sxs-lookup"><span data-stu-id="d156b-134">You see a list of the template file, parameters file, and code samples used to deploy the template:</span></span>

    ![Option de téléchargement de modèle Resource Manager pour la création de clusters Hadoop dans HDInsight](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="d156b-136">À ce stade, vous pouvez télécharger le modèle, l’enregistrer dans votre bibliothèque de modèles ou le déployer.</span><span class="sxs-lookup"><span data-stu-id="d156b-136">From here, you can download the template, save it to your template library, or deploy the template.</span></span>

    <span data-ttu-id="d156b-137">Pour accéder à un modèle de votre bibliothèque, cliquez sur **Plus de services** dans le menu de gauche, puis cliquez sur **Modèles** (sous la catégorie **Autres**).</span><span class="sxs-lookup"><span data-stu-id="d156b-137">To access a template in your library, click **More services** from the left menu, and then click **Templates** (under the **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="d156b-138">Le modèle et le fichier de paramètres doivent être utilisés ensemble.</span><span class="sxs-lookup"><span data-stu-id="d156b-138">The template and parameters file must be used together.</span></span> <span data-ttu-id="d156b-139">Sinon, vous obtiendrez peut-être des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="d156b-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="d156b-140">Par exemple, la valeur par défaut de la propriété **clusterKind** est toujours **hadoop**, quels que soient les éléments spécifiés avant de télécharger le modèle.</span><span class="sxs-lookup"><span data-stu-id="d156b-140">For example, the default **clusterKind** property value is always **hadoop**, despite what you specify before you download the template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="d156b-141">Déployer avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="d156b-141">Deploy with PowerShell</span></span>

<span data-ttu-id="d156b-142">Cette procédure crée un cluster Hadoop dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d156b-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="d156b-143">Enregistrez le fichier JSON dans [l’Annexe](#appx-a-arm-template) de votre poste de travail.</span><span class="sxs-lookup"><span data-stu-id="d156b-143">Save the JSON file in the [Appendix](#appx-a-arm-template) to your workstation.</span></span> <span data-ttu-id="d156b-144">Dans le script PowerShell, le nom de fichier est `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="d156b-144">In the PowerShell script, the file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="d156b-145">Définissez les paramètres et les variables, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d156b-145">Set the parameters and variables if needed.</span></span>
3. <span data-ttu-id="d156b-146">Exécutez le modèle avec le script PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="d156b-146">Run the template by using the following PowerShell script:</span></span>

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
        # Connect to Azure
        ####################################
        #region - Connect to Azure subscription
        Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and the dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="d156b-147">Le script PowerShell configure uniquement le nom du cluster.</span><span class="sxs-lookup"><span data-stu-id="d156b-147">The PowerShell script configures only the cluster name.</span></span> <span data-ttu-id="d156b-148">Le nom du compte de stockage est codé en dur dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="d156b-148">The storage account name is hard-coded in the template.</span></span> <span data-ttu-id="d156b-149">Vous êtes invité à entrer le mot de passe de l’utilisateur du cluster.</span><span class="sxs-lookup"><span data-stu-id="d156b-149">You are prompted to enter the cluster user password.</span></span> <span data-ttu-id="d156b-150">(Le nom d’utilisateur par défaut est **admin**.) Vous êtes également invité à entrer le mot de passe de l’utilisateur SSH.</span><span class="sxs-lookup"><span data-stu-id="d156b-150">(The default username is **admin**.) You are also prompted to enter the SSH user password.</span></span> <span data-ttu-id="d156b-151">(Le nom d’utilisateur SSH par défaut est **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="d156b-151">(The default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="d156b-152">Pour plus d’informations, consultez la rubrique [Déploiement avec PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="d156b-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="d156b-153">Déploiement avec la CLI</span><span class="sxs-lookup"><span data-stu-id="d156b-153">Deploy with CLI</span></span>
<span data-ttu-id="d156b-154">L’exemple suivant utilise l’interface de ligne de commande (CLI) Azure.</span><span class="sxs-lookup"><span data-stu-id="d156b-154">The following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="d156b-155">Il appelle un modèle Resource Manager pour créer un cluster, son compte de stockage dépendant et son conteneur :</span><span class="sxs-lookup"><span data-stu-id="d156b-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="d156b-156">Vous êtes invité à entrer :</span><span class="sxs-lookup"><span data-stu-id="d156b-156">You are prompted to enter:</span></span>
* <span data-ttu-id="d156b-157">le nom du cluster ;</span><span class="sxs-lookup"><span data-stu-id="d156b-157">The cluster name.</span></span>
* <span data-ttu-id="d156b-158">le mot de passe de l’utilisateur du cluster</span><span class="sxs-lookup"><span data-stu-id="d156b-158">The cluster user password.</span></span> <span data-ttu-id="d156b-159">(le nom d’utilisateur par défaut est **admin**) ;</span><span class="sxs-lookup"><span data-stu-id="d156b-159">(The default username is **admin**.)</span></span>
* <span data-ttu-id="d156b-160">le mot de passe de l’utilisateur SSH</span><span class="sxs-lookup"><span data-stu-id="d156b-160">The SSH user password.</span></span> <span data-ttu-id="d156b-161">(le nom d’utilisateur SSH par défaut est **sshuser**).</span><span class="sxs-lookup"><span data-stu-id="d156b-161">(The default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="d156b-162">Le code suivant fournit des paramètres inline :</span><span class="sxs-lookup"><span data-stu-id="d156b-162">The following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="d156b-163">Déployer avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="d156b-163">Deploy with the REST API</span></span>
<span data-ttu-id="d156b-164">Consultez [Déployer avec l’API REST](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="d156b-164">See [Deploy with the REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="d156b-165">Déployer avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d156b-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="d156b-166">Utilisez Visual Studio pour créer un projet de groupe de ressources et le déployer vers Azure par le biais de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d156b-166">Use Visual Studio to create a resource group project and deploy it to Azure through the user interface.</span></span> <span data-ttu-id="d156b-167">Vous sélectionnez le type de ressources à inclure dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="d156b-167">You select the type of resources to include in your project.</span></span> <span data-ttu-id="d156b-168">Ces ressources sont automatiquement ajoutées au modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d156b-168">Those resources are automatically added to the Resource Manager template.</span></span> <span data-ttu-id="d156b-169">Le projet fournit également un script PowerShell pour déployer le modèle.</span><span class="sxs-lookup"><span data-stu-id="d156b-169">The project also provides a PowerShell script to deploy the template.</span></span>

<span data-ttu-id="d156b-170">Pour une introduction à l’utilisation de Visual Studio avec les groupes de ressources, consultez [Création et déploiement de groupes de ressources Azure à l’aide de Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d156b-170">For an introduction to using Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="d156b-171">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="d156b-171">Troubleshoot</span></span>

<span data-ttu-id="d156b-172">Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="d156b-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d156b-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d156b-173">Next steps</span></span>
<span data-ttu-id="d156b-174">Cet article vous a présenté différentes méthodes pour créer un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d156b-174">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="d156b-175">Pour en savoir plus, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="d156b-175">To learn more, see the following articles:</span></span>

* <span data-ttu-id="d156b-176">Pour découvrir un exemple de déploiement de ressources par le biais de la bibliothèque cliente .NET, consultez la page [Déployer des ressources avec des bibliothèques .NET et un modèle](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d156b-176">For an example of deploying resources through the .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="d156b-177">Pour obtenir un exemple détaillé de déploiement d’une application, consultez [Approvisionner et déployer des microservices de manière prévisible dans Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="d156b-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="d156b-178">Pour obtenir des instructions sur le déploiement de votre solution dans différents environnements, consultez [Environnements de développement et de test dans Microsoft Azure](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="d156b-178">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="d156b-179">Pour en savoir plus sur les sections du modèle Azure Resource Manager, consultez [Création de modèles](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d156b-179">To learn about the sections of the Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d156b-180">Pour obtenir la liste des fonctions que vous pouvez utiliser dans un modèle Azure Resource Manager, voir [Fonctions des modèles](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="d156b-180">For a list of the functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-to-create-a-hadoop-cluster"></a><span data-ttu-id="d156b-181">Annexe : Modèle Resource Manager pour créer un cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="d156b-181">Appendix: Resource Manager template to create a Hadoop cluster</span></span>
<span data-ttu-id="d156b-182">Le modèle Azure Resource Manager suivant crée un cluster Hadoop basé sur Linux avec le compte de stockage Azure dépendant.</span><span class="sxs-lookup"><span data-stu-id="d156b-182">The following Azure Resource Manager template creates a Linux-based Hadoop cluster with the dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="d156b-183">Cet exemple inclut des informations de configuration pour le metastore Hive et le metastore Oozie.</span><span class="sxs-lookup"><span data-stu-id="d156b-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="d156b-184">Supprimez la section ou configurez la section avant d’utiliser le modèle.</span><span class="sxs-lookup"><span data-stu-id="d156b-184">Remove the section or configure the section before using the template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "The name of the HDInsight cluster to create."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used to remotely access the cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
            "description": "The location where all azure resources will be deployed."
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
            "description": "The type of the HDInsight cluster to create."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "The number of nodes in the HDInsight cluster."
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

## <a name="appendix-resource-manager-template-to-create-a-spark-cluster"></a><span data-ttu-id="d156b-185">Annexe : Modèle Resource Manager pour créer un cluster Spark</span><span class="sxs-lookup"><span data-stu-id="d156b-185">Appendix: Resource Manager template to create a Spark cluster</span></span>

<span data-ttu-id="d156b-186">Dans cette section contient un modèle Resource Manager que vous pouvez utiliser pour créer un cluster Spark HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d156b-186">This section provides a Resource Manager template that you can use to create an HDInsight Spark cluster.</span></span> <span data-ttu-id="d156b-187">Ce modèle inclut les configurations pour `spark-defaults` et `spark-thrift-sparkconf` (pour les clusters Spark 1.6) et `spark2-defaults` et `spark2-thrift-sparkconf` (pour les clusters Spark 2).</span><span class="sxs-lookup"><span data-stu-id="d156b-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="d156b-188">En outre, HDInsight calcule et définit des configurations telles que `spark.executor.instances`, `spark.executor.memory` et `spark.executor.cores` en fonction de la taille du cluster.</span><span class="sxs-lookup"><span data-stu-id="d156b-188">In addition to this, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on the cluster size.</span></span> 

<span data-ttu-id="d156b-189">Si vous définissez un paramètre d’une section au sein même du modèle, HDInsight ne calcule pas et ne définit pas les autres paramètres de cette même section.</span><span class="sxs-lookup"><span data-stu-id="d156b-189">If you set any one parameter in a section as part of the template itself, HDInsight does not calculate and set the other parameters of the same section.</span></span> <span data-ttu-id="d156b-190">Par exemple, le paramètre `spark.executor.instances` est dans la configuration `spark-defaults`.</span><span class="sxs-lookup"><span data-stu-id="d156b-190">For example, parameter `spark.executor.instances` is in the  `spark-defaults` configuration.</span></span> <span data-ttu-id="d156b-191">Si vous définissez un autre paramètre (par exemple, `spark.yarn.exector.memoryOverhead`) dans la configuration `spark-defaults`, HDInsight ne calcule pas et ne définit pas non plus le paramètre `spark.executor.instances`.</span><span class="sxs-lookup"><span data-stu-id="d156b-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in the `spark-defaults` configuration, HDInsight does not calculate and set the `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "The name of the HDInsight cluster to create."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "The location where all azure resources will be deployed."
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
                "description": "The number of nodes in the HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "The type of the HDInsight cluster to create."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used to remotely access the cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
