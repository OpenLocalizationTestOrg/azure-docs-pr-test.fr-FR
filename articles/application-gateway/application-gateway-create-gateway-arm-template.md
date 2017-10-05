---
title: "Créer une passerelle Azure Application Gateway - modèles | Microsoft Docs"
description: "Cette page fournit des instructions pour la création d’une passerelle Azure Application Gateway à l’aide du modèle Azure Resource Manager"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 46cca89ccb5bd77d57fabc3e9027fcebd38da8e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-resource-manager-template"></a><span data-ttu-id="ebb3a-103">Création d’une passerelle d’application à l’aide du modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ebb3a-103">Create an application gateway by using the Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ebb3a-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="ebb3a-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="ebb3a-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ebb3a-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="ebb3a-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebb3a-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="ebb3a-107">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ebb3a-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="ebb3a-108">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="ebb3a-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="ebb3a-109">La passerelle Azure Application Gateway est un équilibreur de charge de couche 7.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="ebb3a-110">Elle assure l’exécution des requêtes HTTP de basculement et de routage des performances entre des serveurs locaux ou dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="ebb3a-111">Application Gateway offre de nombreuses fonctionnalités de contrôleur de livraison d’applications (ADC) : équilibrage de charge HTTP, affinité de session basée sur les cookies, déchargement SSL (Secure Sockets Layer), sondes d’intégrité personnalisées, prise en charge de plusieurs sites, etc.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="ebb3a-112">Pour obtenir une liste complète des fonctionnalités prises en charge, voir [Vue d’ensemble d’Application Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ebb3a-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="ebb3a-113">Cet article vous guidera dans le téléchargement et la modification d’un modèle Azure Resource Manager existant à partir de GitHub, et dans son déploiement à partir de GitHub, de PowerShell et de l’interface Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="ebb3a-114">Si vous déployez simplement le modèle Azure Resource Manager directement à partir de GitHub sans rien modifier, passez à la section Déployer un modèle à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-114">If you are simply deploying the Azure Resource Manager template directly from GitHub without any changes, skip to deploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="ebb3a-115">Scénario</span><span class="sxs-lookup"><span data-stu-id="ebb3a-115">Scenario</span></span>

<span data-ttu-id="ebb3a-116">Dans ce scénario, vous allez :</span><span class="sxs-lookup"><span data-stu-id="ebb3a-116">In this scenario you will:</span></span>

* <span data-ttu-id="ebb3a-117">créer une passerelle d’application avec le pare-feu d’applications web ;</span><span class="sxs-lookup"><span data-stu-id="ebb3a-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="ebb3a-118">créer un réseau virtuel nommé VirtualNetwork1 avec un bloc CIDR réservé de 10.0.0.0/16 ;</span><span class="sxs-lookup"><span data-stu-id="ebb3a-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="ebb3a-119">créer un sous-réseau appelé Appgatewaysubnet qui utilise 10.0.0.0/28 comme bloc CIDR ;</span><span class="sxs-lookup"><span data-stu-id="ebb3a-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="ebb3a-120">installer deux adresses IP terminales précédemment configurées pour les serveurs web pour lesquels vous souhaitez équilibrer la charge du trafic.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-120">Set up two previously configured back-end IPs for the web servers you want to load balance the traffic.</span></span> <span data-ttu-id="ebb3a-121">Dans cet exemple de modèle, nous allons utiliser les adresses IP terminales 10.0.1.10 et 10.0.1.11.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-121">In this template example, the back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="ebb3a-122">Ce sont les paramètres de ce modèle.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-122">Those settings are the parameters for this template.</span></span> <span data-ttu-id="ebb3a-123">Pour personnaliser le modèle, vous pouvez modifier les règles, l’écouteur, le protocole SSL et d’autres options en ouvrant le fichier azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-123">To customize the template, you can change rules, the listener, SSL, and other options in the azuredeploy.json file.</span></span>

![Scénario](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="ebb3a-125">Téléchargement et découverte du modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ebb3a-125">Download and understand the Azure Resource Manager template</span></span>

<span data-ttu-id="ebb3a-126">Vous pouvez télécharger le modèle Azure Resource Manager existant pour créer un réseau virtuel et deux sous-réseaux sur GitHub, apporter les modifications souhaitées, puis le réutiliser.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-126">You can download the existing Azure Resource Manager template to create a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="ebb3a-127">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ebb3a-127">To do so, use the following steps:</span></span>

1. <span data-ttu-id="ebb3a-128">Accédez à [Créer une passerelle d’application avec le pare-feu d’applications web activé](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="ebb3a-128">Navigate to [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="ebb3a-129">Cliquez sur **azuredeploy.json**, puis sur **RAW**.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="ebb3a-130">Enregistrez le fichier dans un dossier local sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-130">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="ebb3a-131">Si vous connaissez déjà les modèles Azure Resource Manager, passez à l’étape 7.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-131">If you are familiar with Azure Resource Manager templates, skip to step 7.</span></span>
1. <span data-ttu-id="ebb3a-132">Ouvrez le fichier que vous avez enregistré et consultez le contenu sous **parameters** à la ligne</span><span class="sxs-lookup"><span data-stu-id="ebb3a-132">Open the file that you saved and look at the contents under **parameters** in line</span></span>
1. <span data-ttu-id="ebb3a-133">Les paramètres du modèle Azure Resource Manager fournissent un espace réservé pour les valeurs à remplir lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="ebb3a-134">Paramètre</span><span class="sxs-lookup"><span data-stu-id="ebb3a-134">Parameter</span></span> | <span data-ttu-id="ebb3a-135">Description</span><span class="sxs-lookup"><span data-stu-id="ebb3a-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="ebb3a-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="ebb3a-136">**subnetPrefix**</span></span> |<span data-ttu-id="ebb3a-137">Bloc CIDR du sous-réseau de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-137">CIDR block for the application gateway subnet.</span></span> |
  | <span data-ttu-id="ebb3a-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="ebb3a-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="ebb3a-139">Taille de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-139">Size of the application gateway.</span></span>  <span data-ttu-id="ebb3a-140">Le pare-feu d’applications web autorise uniquement les tailles moyenne et grande.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="ebb3a-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="ebb3a-141">**backendIpaddress1**</span></span> |<span data-ttu-id="ebb3a-142">Adresse IP du premier serveur web.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-142">IP address of the first web server.</span></span> |
  | <span data-ttu-id="ebb3a-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="ebb3a-143">**backendIpaddress2**</span></span> |<span data-ttu-id="ebb3a-144">Adresse IP du deuxième serveur web.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-144">IP address of the second web server.</span></span> |
  | <span data-ttu-id="ebb3a-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="ebb3a-145">**wafEnabled**</span></span> | <span data-ttu-id="ebb3a-146">Permet de déterminer si le pare-feu d’applications web est activé.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-146">Setting to determine if WAF is enabled.</span></span>|
  | <span data-ttu-id="ebb3a-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="ebb3a-147">**wafMode**</span></span> | <span data-ttu-id="ebb3a-148">Mode du pare-feu d’applications web.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-148">Mode of the web application firewall.</span></span>  <span data-ttu-id="ebb3a-149">Les options disponibles sont **prévention** ou **détection**.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="ebb3a-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="ebb3a-150">**wafRuleSetType**</span></span> | <span data-ttu-id="ebb3a-151">Type de groupe de règles du pare-feu d’applications web.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="ebb3a-152">Actuellement, OWASP est la seule option prise en charge.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-152">Currently OWASP is the only supported option.</span></span> |
  | <span data-ttu-id="ebb3a-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="ebb3a-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="ebb3a-154">Version de groupe de règles.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-154">Ruleset version.</span></span> <span data-ttu-id="ebb3a-155">Les options prises en charge sont actuellement OWASP CRS 2.2.9 et 3.0.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-155">OWASP CRS 2.2.9 and 3.0 are currently the supported options.</span></span> |

1. <span data-ttu-id="ebb3a-156">Vérifiez le contenu sous **ressources** et notez les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="ebb3a-156">Check the content under **resources** and notice the following properties:</span></span>

   * <span data-ttu-id="ebb3a-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-157">**type**.</span></span> <span data-ttu-id="ebb3a-158">Type de ressource créée par le modèle.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-158">Type of resource being created by the template.</span></span> <span data-ttu-id="ebb3a-159">Dans ce cas, le type qui représente une passerelle d’application est `Microsoft.Network/applicationGateways`.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-159">In this case, the type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="ebb3a-160">**name**.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-160">**name**.</span></span> <span data-ttu-id="ebb3a-161">Nom de la ressource.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-161">Name for the resource.</span></span> <span data-ttu-id="ebb3a-162">Remarquez l’utilisation de `[parameters('applicationGatewayName')]`, qui signifie que le nom est fourni par vous ou un fichier de paramètres lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-162">Notice the use of `[parameters('applicationGatewayName')]`, which means that the name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="ebb3a-163">**properties**.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-163">**properties**.</span></span> <span data-ttu-id="ebb3a-164">Liste des propriétés de la ressource.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-164">List of properties for the resource.</span></span> <span data-ttu-id="ebb3a-165">Ce modèle utilise le réseau virtuel et une adresse IP publique lors de la création de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-165">This template uses the virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ebb3a-166">Pour plus d’informations sur les modèles, consultez [Référence sur les modèles Resource Manager](/templates/).</span><span class="sxs-lookup"><span data-stu-id="ebb3a-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="ebb3a-167">Revenez à [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-create/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="ebb3a-167">Navigate back to [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="ebb3a-168">Cliquez sur **azuredeploy-parameters.json**, puis sur **RAW**.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="ebb3a-169">Enregistrez le fichier dans un dossier local sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-169">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="ebb3a-170">Ouvrez le fichier que vous avez enregistré et modifiez les valeurs des paramètres.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-170">Open the file that you saved and edit the values for the parameters.</span></span> <span data-ttu-id="ebb3a-171">Utilisez les valeurs suivantes pour déployer la passerelle Application Gateway décrite dans notre scénario.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-171">Use the following values to deploy the application gateway described in our scenario.</span></span>

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. <span data-ttu-id="ebb3a-172">Enregistrez le fichier .</span><span class="sxs-lookup"><span data-stu-id="ebb3a-172">Save the file.</span></span> <span data-ttu-id="ebb3a-173">Vous pouvez tester le modèle JSON et le modèle de paramètres à l’aide des outils de validation JSON en ligne comme [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="ebb3a-173">You can test the JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-the-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="ebb3a-174">Déploiement du modèle Azure Resource Manager à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebb3a-174">Deploy the Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="ebb3a-175">Si vous n’avez jamais utilisé Azure PowerShell, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) et suivez les instructions pour vous connecter à Azure et sélectionner votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-175">If you have never used Azure PowerShell, visit: [How to install and configure Azure PowerShell](/powershell/azure/overview) and follow the instructions to sign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="ebb3a-176">Connexion à PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebb3a-176">Login to PowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="ebb3a-177">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-177">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="ebb3a-178">Vous êtes invité à vous authentifier à l’aide de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-178">You are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="ebb3a-179">Parmi vos abonnements Azure, choisissez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-179">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="ebb3a-180">Au besoin, créez un groupe de ressources à l’aide de l’applet de commande **New-AzureResourceGroup** .</span><span class="sxs-lookup"><span data-stu-id="ebb3a-180">If needed, create a resource group by using the **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="ebb3a-181">Dans l’exemple suivant, vous allez créer un groupe de ressources appelé AppgatewayRG dans les États-Unis de l’Est.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-181">In the following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="ebb3a-182">Exécutez l’applet de commande **New-AzureRmResourceGroupDeployment** pour déployer le nouveau réseau virtuel à l’aide du modèle précédent et des fichiers de paramètres que vous avez téléchargés et modifiés.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-182">Run the **New-AzureRmResourceGroupDeployment** cmdlet to deploy the new virtual network by using the preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-the-azure-cli"></a><span data-ttu-id="ebb3a-183">Déploiement du modèle Azure Resource Manager à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="ebb3a-183">Deploy the Azure Resource Manager template by using the Azure CLI</span></span>

<span data-ttu-id="ebb3a-184">Pour déployer le modèle Azure Resource Manager que vous avez téléchargé à l’aide de l’interface de ligne de commande Azure, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ebb3a-184">To deploy the Azure Resource Manager template you downloaded by using Azure CLI, follow the following steps:</span></span>

1. <span data-ttu-id="ebb3a-185">Si vous n’avez jamais utilisé l’interface de ligne de commande Azure, consultez [Installer et configurer l’interface de ligne de commande Azure](/cli/azure/install-azure-cli) et suivez les instructions jusqu’à l’étape où vous sélectionnez votre compte et votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-185">If you have never used Azure CLI, see [Install and configure the Azure CLI](/cli/azure/install-azure-cli) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="ebb3a-186">Au besoin, exécutez la commande `az group create` pour créer un groupe de ressources, comme illustré dans l’extrait de code suivant.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-186">If necessary, run the `az group create` command to create a resource group, as shown in the following code snippet.</span></span> <span data-ttu-id="ebb3a-187">Observez le résultat de la commande.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-187">Notice the output of the command.</span></span> <span data-ttu-id="ebb3a-188">La liste affichée après le résultat présente les différents paramètres utilisés.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-188">The list shown after the output explains the parameters used.</span></span> <span data-ttu-id="ebb3a-189">Pour plus d’informations sur les groupes de ressources, consultez la page [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ebb3a-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="ebb3a-190">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-190">**-n (or --name)**.</span></span> <span data-ttu-id="ebb3a-191">Nom du nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-191">Name for the new resource group.</span></span> <span data-ttu-id="ebb3a-192">Pour notre scénario, il s’agit de *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="ebb3a-193">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-193">**-l (or --location)**.</span></span> <span data-ttu-id="ebb3a-194">Région Azure où le nouveau groupe de ressources est créé.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-194">Azure region where the new resource group is created.</span></span> <span data-ttu-id="ebb3a-195">Pour notre scénario, il s’agit de *westus*.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="ebb3a-196">Exécutez l’applet de commande `az group deployment create` pour déployer le nouveau réseau virtuel à l’aide du modèle et des fichiers de paramètres que vous avez téléchargés et modifiés lors de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-196">Run the `az group deployment create` cmdlet to deploy the new virtual network by using the template and parameter files you downloaded and modified in the preceding step.</span></span> <span data-ttu-id="ebb3a-197">La liste affichée après le résultat présente les différents paramètres utilisés.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-197">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="ebb3a-198">Déploiement du modèle Azure Resource Manager à l’aide de la fonctionnalité « cliquer pour déployer »</span><span class="sxs-lookup"><span data-stu-id="ebb3a-198">Deploy the Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="ebb3a-199">La fonctionnalité « cliquer pour déployer » offre une autre manière d’utiliser les modèles ARM.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-199">Click-to-deploy is another way to use Azure Resource Manager templates.</span></span> <span data-ttu-id="ebb3a-200">C’est un moyen facile d’utiliser des modèles avec le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-200">It's an easy way to use templates with the Azure portal.</span></span>

1. <span data-ttu-id="ebb3a-201">Accédez à [Créer une passerelle d’application avec le pare-feu d’applications web](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="ebb3a-201">Go to [Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="ebb3a-202">Cliquez sur **Déployer dans Azure**.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-202">Click **Deploy to Azure**.</span></span>

    ![Déployer dans Azure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="ebb3a-204">Renseignez les paramètres du modèle de déploiement sur le portail, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-204">Fill out the parameters for the deployment template on the portal and click **OK**.</span></span>

    ![Paramètres](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="ebb3a-206">Sélectionnez **J’accepte les termes et conditions mentionnés ci-dessus**, puis cliquez sur **Acheter**.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-206">Select **I agree to the terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="ebb3a-207">Dans le panneau Déploiement personnalisé, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-207">On the Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-to-resource-manager-templates"></a><span data-ttu-id="ebb3a-208">Fournir des données de certificat aux modèles Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ebb3a-208">Providing certificate data to Resource Manager templates</span></span>

<span data-ttu-id="ebb3a-209">Si SSL est utilisé avec un modèle, le certificat doit être fourni dans une chaîne base64, et non chargé.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-209">When using SSL with a template, the certificate needs to be provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="ebb3a-210">Pour convertir un .pfx ou un .cer en chaîne base64, utilisez l’une des commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-210">To convert a .pfx or .cer to a base64 string use one of the following commands.</span></span> <span data-ttu-id="ebb3a-211">Les commandes ci-après convertissent le certificat en chaîne base64 qui pourra être fournie au modèle.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-211">The following commands convert the certificate to a base64 string, which can be provided to the template.</span></span> <span data-ttu-id="ebb3a-212">La sortie attendue est une chaîne qui peut être stockée dans une variable et collée dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="ebb3a-212">The expected output is a string that can be stored in a variable and pasted in the template.</span></span>

### <a name="macos"></a><span data-ttu-id="ebb3a-213">macOS</span><span class="sxs-lookup"><span data-stu-id="ebb3a-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="ebb3a-214">Windows</span><span class="sxs-lookup"><span data-stu-id="ebb3a-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="ebb3a-215">Supprimer toutes les ressources</span><span class="sxs-lookup"><span data-stu-id="ebb3a-215">Delete all resources</span></span>

<span data-ttu-id="ebb3a-216">Pour supprimer toutes les ressources créées dans cet article, effectuez l’une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ebb3a-216">To delete all resources created in this article, complete one of the following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="ebb3a-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebb3a-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="ebb3a-218">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="ebb3a-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="ebb3a-219">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ebb3a-219">Next steps</span></span>

<span data-ttu-id="ebb3a-220">Si vous souhaitez configurer le déchargement SSL, consultez la page [Configuration d’une passerelle Application Gateway pour le déchargement SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="ebb3a-220">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="ebb3a-221">Si vous voulez configurer une passerelle Application Gateway à utiliser avec l’équilibreur de charge interne, consultez la page [Création d’une passerelle Application Gateway avec un équilibrage de charge interne (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="ebb3a-221">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="ebb3a-222">Si vous souhaitez plus d’informations sur les options d’équilibrage de charge en général, visitez :</span><span class="sxs-lookup"><span data-stu-id="ebb3a-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="ebb3a-223">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="ebb3a-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="ebb3a-224">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="ebb3a-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

