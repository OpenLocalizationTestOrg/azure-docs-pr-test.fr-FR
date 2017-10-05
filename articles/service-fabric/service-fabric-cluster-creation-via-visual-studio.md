---
title: "Configuration d’un cluster Service Fabric à l’aide de Visual Studio | Microsoft Docs"
description: "Décrit comment configurer un cluster Service Fabric à l’aide d’un modèle Azure Resource Manager créé par un projet de groupe de ressources Azure dans Visual Studio"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: c43145b96cdbdfaa7e1893e50d027321fe4c0510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="cc933-103">Configuration d’un cluster Service Fabric à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cc933-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="cc933-104">Cet article décrit comment configurer un cluster Azure Service Fabric à l’aide de Visual Studio et d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cc933-104">This article describes how to set up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="cc933-105">Nous utiliserons un projet du groupe de ressources Azure Visual Studio pour créer le modèle.</span><span class="sxs-lookup"><span data-stu-id="cc933-105">We will use a Visual Studio Azure resource group project to create the template.</span></span> <span data-ttu-id="cc933-106">Une fois le modèle créé, il peut être déployé directement vers Azure à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cc933-106">After the template has been created, it can be deployed directly to Azure from Visual Studio.</span></span> <span data-ttu-id="cc933-107">Il peut également être utilisé à partir d’un script ou dans le cadre de la fonctionnalité d’intégration continue (CI).</span><span class="sxs-lookup"><span data-stu-id="cc933-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="cc933-108">Création d’un modèle de cluster Service Fabric à l’aide d’un projet de groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="cc933-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="cc933-109">Pour commencer, ouvrez Visual Studio et créez un projet de groupe de ressources Azure (disponible dans le dossier **Cloud** ) :</span><span class="sxs-lookup"><span data-stu-id="cc933-109">To get started, open Visual Studio and create an Azure resource group project (it is available in the **Cloud** folder):</span></span>

![Boîte de dialogue Nouveau projet avec le projet du groupe de ressources Azure sélectionné][1]

<span data-ttu-id="cc933-111">Vous pouvez créer une solution Visual Studio pour ce projet ou l’ajouter à une solution existante.</span><span class="sxs-lookup"><span data-stu-id="cc933-111">You can create a new Visual Studio solution for this project or add it to an existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="cc933-112">Si vous ne voyez pas le projet de groupe de ressources Azure sous le nœud Cloud, le Kit de développement logiciel (SDK) Azure n’est pas installé.</span><span class="sxs-lookup"><span data-stu-id="cc933-112">If you do not see the Azure resource group project under the Cloud node, you do not have the Azure SDK installed.</span></span> <span data-ttu-id="cc933-113">Lancez Web Platform Installer ([à installer maintenant](http://www.microsoft.com/web/downloads/platform.aspx) si ce n’est pas déjà fait), puis recherchez « Azure SDK pour .NET » et installez la version compatible avec votre version de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cc933-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install the version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="cc933-114">Une fois que vous avez cliqué sur le bouton OK, Visual Studio vous demande de sélectionner le modèle Resource Manager à créer :</span><span class="sxs-lookup"><span data-stu-id="cc933-114">After you hit the OK button, Visual Studio will ask you to select the Resource Manager template you want to create:</span></span>

![Boîte de dialogue Sélectionner le modèle Azure avec le modèle de cluster Service Fabric sélectionné][2]

<span data-ttu-id="cc933-116">Sélectionnez le modèle Service Fabric Cluster et cliquez à nouveau sur le bouton OK.</span><span class="sxs-lookup"><span data-stu-id="cc933-116">Select the Service Fabric Cluster template and hit the OK button again.</span></span> <span data-ttu-id="cc933-117">Le projet et le modèle Resource Manager sont maintenant créés.</span><span class="sxs-lookup"><span data-stu-id="cc933-117">The project and the Resource Manager template have now been created.</span></span>

## <a name="prepare-the-template-for-deployment"></a><span data-ttu-id="cc933-118">Préparation du modèle pour le déploiement</span><span class="sxs-lookup"><span data-stu-id="cc933-118">Prepare the template for deployment</span></span>
<span data-ttu-id="cc933-119">Avant de déployer le modèle pour créer le cluster, vous devez fournir les valeurs des paramètres obligatoires du modèle.</span><span class="sxs-lookup"><span data-stu-id="cc933-119">Before the template is deployed to create the cluster, you must provide values for the required template parameters.</span></span> <span data-ttu-id="cc933-120">Ces valeurs de paramètres sont lues à partir du fichier `ServiceFabricCluster.parameters.json`, qui se trouve dans le dossier `Templates` du projet de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="cc933-120">These parameter values are read from the `ServiceFabricCluster.parameters.json` file, which is in the `Templates` folder of the resource group project.</span></span> <span data-ttu-id="cc933-121">Ouvrez le fichier et spécifiez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="cc933-121">Open the file and provide the following values:</span></span>

| <span data-ttu-id="cc933-122">Nom du paramètre</span><span class="sxs-lookup"><span data-stu-id="cc933-122">Parameter name</span></span> | <span data-ttu-id="cc933-123">Description</span><span class="sxs-lookup"><span data-stu-id="cc933-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cc933-124">adminUsername</span><span class="sxs-lookup"><span data-stu-id="cc933-124">adminUserName</span></span> |<span data-ttu-id="cc933-125">Nom du compte de l’administrateur pour les machines Service Fabric (nœuds).</span><span class="sxs-lookup"><span data-stu-id="cc933-125">The name of the administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="cc933-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="cc933-126">certificateThumbprint</span></span> |<span data-ttu-id="cc933-127">Empreinte numérique du certificat qui sécurise le cluster.</span><span class="sxs-lookup"><span data-stu-id="cc933-127">The thumbprint of the certificate that secures the cluster.</span></span> |
| <span data-ttu-id="cc933-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="cc933-128">sourceVaultResourceId</span></span> |<span data-ttu-id="cc933-129">*ID de ressource* du coffre de clés où est stocké le certificat qui sécurise le cluster.</span><span class="sxs-lookup"><span data-stu-id="cc933-129">The *resource ID* of the key vault where the certificate that secures the cluster is stored.</span></span> |
| <span data-ttu-id="cc933-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="cc933-130">certificateUrlValue</span></span> |<span data-ttu-id="cc933-131">URL du certificat de sécurité du cluster.</span><span class="sxs-lookup"><span data-stu-id="cc933-131">The URL of the cluster security certificate.</span></span> |

<span data-ttu-id="cc933-132">Le modèle Resource Manager Service Fabric Visual Studio crée un cluster sécurisé, qui est protégé par un certificat.</span><span class="sxs-lookup"><span data-stu-id="cc933-132">The Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="cc933-133">Ce certificat est identifié par les trois derniers paramètres du modèle (`certificateThumbprint`, `sourceVaultValue` et `certificateUrlValue`) et doit être présent dans **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="cc933-133">This certificate is identified by the last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="cc933-134">Pour plus d’informations sur la création du certificat de sécurité du cluster, consultez l’article [Scénarios de sécurité d’un cluster Service Fabric](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) .</span><span class="sxs-lookup"><span data-stu-id="cc933-134">For more information on how to create the cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-the-cluster-name"></a><span data-ttu-id="cc933-135">Facultatif : modifier le nom du cluster</span><span class="sxs-lookup"><span data-stu-id="cc933-135">Optional: change the cluster name</span></span>
<span data-ttu-id="cc933-136">Chaque cluster Service Fabric dispose d’un nom.</span><span class="sxs-lookup"><span data-stu-id="cc933-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="cc933-137">Lors de la création d’un cluster Fabric dans Azure, le nom de cluster détermine (avec la région Azure) le nom du système DNS (Domain Name System) pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="cc933-137">When a Fabric cluster is created in Azure, cluster name determines (together with the Azure region) the Domain Name System (DNS) name for the cluster.</span></span> <span data-ttu-id="cc933-138">Par exemple, si vous nommez votre cluster `myBigCluster`, et que l’emplacement (région Azure) du groupe de ressources qui hébergera le nouveau cluster est États-Unis de l’Est, le nom DNS du cluster sera `myBigCluster.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="cc933-138">For example, if you name your cluster `myBigCluster`, and the location (Azure region) of the resource group that will host the new cluster is East US, the DNS name of the cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="cc933-139">Par défaut, le nom du cluster est généré automatiquement et rendu unique en associant un suffixe aléatoire à un préfixe « cluster ».</span><span class="sxs-lookup"><span data-stu-id="cc933-139">By default the cluster name is generated automatically and made unique by attaching a random suffix to a "cluster" prefix.</span></span> <span data-ttu-id="cc933-140">Cela permet d’utiliser très facilement le modèle comme un élément d’un système d’ **intégration continue** (CI).</span><span class="sxs-lookup"><span data-stu-id="cc933-140">This makes it very easy to use the template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="cc933-141">Si vous souhaitez utiliser un nom spécifique (qui a un sens pour vous) pour votre cluster, définissez la valeur de la variable `clusterName` dans le fichier de modèle Resource Manager (`ServiceFabricCluster.json`) avec le nom de votre choix.</span><span class="sxs-lookup"><span data-stu-id="cc933-141">If you want to use a specific name for your cluster, one that is meaningful to you, set the value of the `clusterName` variable in the Resource Manager template file (`ServiceFabricCluster.json`) to your chosen name.</span></span> <span data-ttu-id="cc933-142">Il s’agit de la première variable définie dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="cc933-142">It is the first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="cc933-143">Facultatif : ajout de ports d’application publics</span><span class="sxs-lookup"><span data-stu-id="cc933-143">Optional: add public application ports</span></span>
<span data-ttu-id="cc933-144">Vous pouvez également souhaiter modifier les ports d’application publics pour le cluster avant de le déployer.</span><span class="sxs-lookup"><span data-stu-id="cc933-144">You may also want to change the public application ports for the cluster before you deploy it.</span></span> <span data-ttu-id="cc933-145">Par défaut, le modèle ouvre seulement deux ports TCP publics (80 et 8081).</span><span class="sxs-lookup"><span data-stu-id="cc933-145">By default, the template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="cc933-146">Si vous avez besoin d’autres ports pour vos applications, modifiez la définition de l’équilibreur de charge Azure dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="cc933-146">If you need more for your applications, modify the Azure Load Balancer definition in the template.</span></span> <span data-ttu-id="cc933-147">La définition est stockée dans le fichier modèle principal (`ServiceFabricCluster.json`).</span><span class="sxs-lookup"><span data-stu-id="cc933-147">The definition is stored in the main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="cc933-148">Ouvrez ce fichier et recherchez `loadBalancedAppPort`.</span><span class="sxs-lookup"><span data-stu-id="cc933-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="cc933-149">Chaque port est associé à trois artefacts :</span><span class="sxs-lookup"><span data-stu-id="cc933-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="cc933-150">Une variable de modèle qui définit la valeur du port TCP pour le port :</span><span class="sxs-lookup"><span data-stu-id="cc933-150">A template variable that defines the TCP port value for the port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="cc933-151">Une *sonde* qui définit la fréquence et la durée pendant lesquelles l’équilibrage de charge Azure tente d’utiliser un nœud Service Fabric spécifique avant de basculer vers un autre.</span><span class="sxs-lookup"><span data-stu-id="cc933-151">A *probe* that defines how frequently and for how long the Azure load balancer attempts to use a specific Service Fabric node before failing over to another one.</span></span> <span data-ttu-id="cc933-152">Les sondes font partie de la ressource d’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="cc933-152">The probes are part of the Load Balancer resource.</span></span> <span data-ttu-id="cc933-153">Voici la définition de la sonde du premier port d’application par défaut :</span><span class="sxs-lookup"><span data-stu-id="cc933-153">Here is the probe definition for the first default application port:</span></span>
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. <span data-ttu-id="cc933-154">Une *règle d’équilibrage de charge* qui relie le port et la sonde, permettant ainsi un équilibrage de charge sur un ensemble de nœuds de cluster Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="cc933-154">A *load-balancing rule* that ties together the port and the probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   <span data-ttu-id="cc933-155">Si les applications que vous envisagez de déployer sur le cluster ont besoin de davantage de ports, vous pouvez les ajouter en créant des définitions de règle de sonde et d’équilibrage de charge supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="cc933-155">If the applications that you plan to deploy to the cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="cc933-156">Pour plus d’informations sur l’utilisation de l’équilibreur de charge Azure par le biais des modèles Resource Manager, consultez [Prise en main de la création d’un équilibreur de charge interne à l’aide d’un modèle](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="cc933-156">For more information on how to work with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-the-template-by-using-visual-studio"></a><span data-ttu-id="cc933-157">Déploiement du modèle à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cc933-157">Deploy the template by using Visual Studio</span></span>
<span data-ttu-id="cc933-158">Une fois que vous avez enregistré toutes les valeurs de paramètres requises dans le fichier`ServiceFabricCluster.param.dev.json` , vous êtes prêt à déployer le modèle et à créer votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cc933-158">After you have saved all the required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready to deploy the template and create your Service Fabric cluster.</span></span> <span data-ttu-id="cc933-159">Cliquez avec le bouton droit sur le projet de groupe de ressources dans l’Explorateur de solutions Visual Studio, puis sélectionnez **Déployer | Nouveau déploiement...**.</span><span class="sxs-lookup"><span data-stu-id="cc933-159">Right-click the resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**.</span></span> <span data-ttu-id="cc933-160">Si nécessaire, Visual Studio affiche la boîte de dialogue **Déployer vers le groupe de ressources**, vous demandant de vous authentifier auprès d’Azure :</span><span class="sxs-lookup"><span data-stu-id="cc933-160">If necessary, Visual Studio will show the **Deploy to Resource Group** dialog box, asking you to authenticate to Azure:</span></span>

![Boîte de dialogue Déployer vers le groupe de ressources][3]

<span data-ttu-id="cc933-162">La boîte de dialogue vous permet de choisir un groupe de ressources Resource Manager existant pour le cluster et vous permet d’en créer un.</span><span class="sxs-lookup"><span data-stu-id="cc933-162">The dialog box lets you choose an existing Resource Manager resource group for the cluster and gives you the option to create a new one.</span></span> <span data-ttu-id="cc933-163">Normalement, il est judicieux d’utiliser un groupe de ressources distinct pour un cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cc933-163">It normally makes sense to use a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="cc933-164">Quand vous cliquez sur le bouton Déployer, Visual Studio vous invite à confirmer les valeurs des paramètres du modèle.</span><span class="sxs-lookup"><span data-stu-id="cc933-164">After you hit the Deploy button, Visual Studio will prompt you to confirm the template parameter values.</span></span> <span data-ttu-id="cc933-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="cc933-165">Hit the **Save** button.</span></span> <span data-ttu-id="cc933-166">Un paramètre n’a pas une valeur persistante : le mot de passe du compte d’administrateur pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="cc933-166">One parameter does not have a persisted value: the administrative account password for the cluster.</span></span> <span data-ttu-id="cc933-167">Vous devez fournir une valeur de mot de passe quand Visual Studio vous en demande une.</span><span class="sxs-lookup"><span data-stu-id="cc933-167">You need to provide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="cc933-168">À partir d’Azure SDK 2.9, Visual Studio prend en charge la lecture des mots de passe depuis **Azure Key Vault** pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="cc933-168">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="cc933-169">Dans la boîte de dialogue de paramètres de modèle, notez que la zone de texte des paramètres `adminPassword` possède une petite icône de « clé » à droite.</span><span class="sxs-lookup"><span data-stu-id="cc933-169">In the template parameters dialog notice that the `adminPassword` parameter text box has a little "key" icon on the right.</span></span> <span data-ttu-id="cc933-170">Cette icône vous permet de sélectionner un secret de coffre de clés existant en tant que mot de passe d’administration du cluster.</span><span class="sxs-lookup"><span data-stu-id="cc933-170">This icon allows you to select an existing key vault secret as the administrative password for the cluster.</span></span> <span data-ttu-id="cc933-171">Assurez-vous simplement d’abord d’activer l’accès à Azure Resource Manager pour le déploiement du modèle dans les stratégies d’accès avancé de votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="cc933-171">Just make sure to first enable Azure Resource Manager access for template deployment in the Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="cc933-172">Vous pouvez surveiller la progression du processus de déploiement dans la fenêtre de sortie de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cc933-172">You can monitor the progress of the deployment process in the Visual Studio output window.</span></span> <span data-ttu-id="cc933-173">Une fois le déploiement de modèle terminé, votre nouveau cluster est prêt à utiliser.</span><span class="sxs-lookup"><span data-stu-id="cc933-173">Once the template deployment is completed, your new cluster is ready to use!</span></span>

> [!NOTE]
> <span data-ttu-id="cc933-174">Si PowerShell n’a jamais été utilisé pour administrer Azure à partir de l’ordinateur que vous utilisez actuellement, vous devez faire un peu de ménage.</span><span class="sxs-lookup"><span data-stu-id="cc933-174">If PowerShell was never used to administer Azure from the machine that you are using now, you need to do a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="cc933-175">Activez l’écriture de scripts PowerShell en exécutant la commande [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) .</span><span class="sxs-lookup"><span data-stu-id="cc933-175">Enable PowerShell scripting by running the [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="cc933-176">Pour les machines de développement, la stratégie « unrestricted » est généralement acceptable.</span><span class="sxs-lookup"><span data-stu-id="cc933-176">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="cc933-177">Décidez s’il faut autoriser la collecte de données de diagnostics à partir de commandes Azure PowerShell et exécutez [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) ou [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) au besoin.</span><span class="sxs-lookup"><span data-stu-id="cc933-177">Decide whether to allow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="cc933-178">Cela permet d'éviter les invites inutiles lors du déploiement du modèle.</span><span class="sxs-lookup"><span data-stu-id="cc933-178">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="cc933-179">Si des erreurs se produisent, accédez au [portail Azure](https://portal.azure.com/) et ouvrez le groupe de ressources utilisé pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="cc933-179">If there are any errors, go to the [Azure portal](https://portal.azure.com/) and open the resource group that you deployed to.</span></span> <span data-ttu-id="cc933-180">Cliquez sur **Tous les paramètres**, puis sur**Déploiements** dans le panneau Paramètres.</span><span class="sxs-lookup"><span data-stu-id="cc933-180">Click **All settings**, then click **Deployments** on the settings blade.</span></span> <span data-ttu-id="cc933-181">Un déploiement de groupe de ressources ayant échoué laisse des informations de diagnostic détaillées à cet endroit.</span><span class="sxs-lookup"><span data-stu-id="cc933-181">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="cc933-182">Les clusters Service Fabric nécessitent un certain nombre de nœuds actifs pour maintenir la disponibilité et préserver l’état. Cette situation est appelée « conservation du quorum ».</span><span class="sxs-lookup"><span data-stu-id="cc933-182">Service Fabric clusters require a certain number of nodes to be up to maintain availability and preserve state - referred to as "maintaining quorum."</span></span> <span data-ttu-id="cc933-183">Par conséquent, il est déconseillé d’arrêter tous les ordinateurs du cluster, sauf si vous avez d’abord effectué une [sauvegarde complète de votre état](service-fabric-reliable-services-backup-restore.md).</span><span class="sxs-lookup"><span data-stu-id="cc933-183">Therefore, it is not safe to shut down all of the machines in the cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="cc933-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cc933-184">Next steps</span></span>
* [<span data-ttu-id="cc933-185">En savoir plus sur la configuration de cluster Service Fabric à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="cc933-185">Learn about setting up Service Fabric cluster using the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="cc933-186">Apprenez à gérer et déployer des applications Service Fabric à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cc933-186">Learn how to manage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
