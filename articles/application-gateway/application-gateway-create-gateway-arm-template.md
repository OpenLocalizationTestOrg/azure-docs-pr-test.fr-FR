---
title: "aaaCreate une passerelle d’Application Azure - modèles | Documents Microsoft"
description: "Cette page fournit des instructions toocreate une passerelle d’application Windows Azure à l’aide du modèle de gestionnaire de ressources Azure hello"
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
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a><span data-ttu-id="2455f-103">Créer une passerelle d’application à l’aide du modèle de gestionnaire de ressources Azure hello</span><span class="sxs-lookup"><span data-stu-id="2455f-103">Create an application gateway by using hello Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2455f-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="2455f-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="2455f-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2455f-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="2455f-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="2455f-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="2455f-107">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2455f-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="2455f-108">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="2455f-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="2455f-109">La passerelle Azure Application Gateway est un équilibreur de charge de couche 7.</span><span class="sxs-lookup"><span data-stu-id="2455f-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="2455f-110">Il fournit de basculement et le routage des performances des requêtes HTTP entre différents serveurs, qu’ils soient sur le cloud de hello ou localement.</span><span class="sxs-lookup"><span data-stu-id="2455f-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="2455f-111">Application Gateway offre de nombreuses fonctionnalités de contrôleur de livraison d’applications (ADC) : équilibrage de charge HTTP, affinité de session basée sur les cookies, déchargement SSL (Secure Sockets Layer), sondes d’intégrité personnalisées, prise en charge de plusieurs sites, etc.</span><span class="sxs-lookup"><span data-stu-id="2455f-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="2455f-112">toofind une liste complète des fonctionnalités prises en charge, visitez [vue d’ensemble de la passerelle d’Application](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="2455f-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="2455f-113">Cet article vous guide par le biais du téléchargement et modification d’un modèle Azure Resource Manager existant à partir de GitHub et le déploiement de modèle hello à partir de GitHub, PowerShell et hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="2455f-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="2455f-114">Si vous déployez simplement modèle du Gestionnaire de ressources Azure hello directement à partir de GitHub sans aucune modification, ignorez toodeploy un modèle à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="2455f-114">If you are simply deploying hello Azure Resource Manager template directly from GitHub without any changes, skip toodeploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="2455f-115">Scénario</span><span class="sxs-lookup"><span data-stu-id="2455f-115">Scenario</span></span>

<span data-ttu-id="2455f-116">Dans ce scénario, vous allez :</span><span class="sxs-lookup"><span data-stu-id="2455f-116">In this scenario you will:</span></span>

* <span data-ttu-id="2455f-117">créer une passerelle d’application avec le pare-feu d’applications web ;</span><span class="sxs-lookup"><span data-stu-id="2455f-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="2455f-118">créer un réseau virtuel nommé VirtualNetwork1 avec un bloc CIDR réservé de 10.0.0.0/16 ;</span><span class="sxs-lookup"><span data-stu-id="2455f-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="2455f-119">créer un sous-réseau appelé Appgatewaysubnet qui utilise 10.0.0.0/28 comme bloc CIDR ;</span><span class="sxs-lookup"><span data-stu-id="2455f-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="2455f-120">Configurer deux adresses IP principale précédemment configurés pour les serveurs web hello souhaité tooload équilibrer hello du trafic.</span><span class="sxs-lookup"><span data-stu-id="2455f-120">Set up two previously configured back-end IPs for hello web servers you want tooload balance hello traffic.</span></span> <span data-ttu-id="2455f-121">Dans cet exemple de modèle, hello principal des adresses IP sont 10.0.1.10 et 10.0.1.11.</span><span class="sxs-lookup"><span data-stu-id="2455f-121">In this template example, hello back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="2455f-122">Ces paramètres sont des paramètres de hello pour ce modèle.</span><span class="sxs-lookup"><span data-stu-id="2455f-122">Those settings are hello parameters for this template.</span></span> <span data-ttu-id="2455f-123">toocustomize modèle de hello, vous pouvez modifier les règles, port d’écoute hello, SSL et autres options dans le fichier de azuredeploy.json hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-123">toocustomize hello template, you can change rules, hello listener, SSL, and other options in hello azuredeploy.json file.</span></span>

![Scénario](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="2455f-125">Télécharger et de comprendre le modèle de gestionnaire de ressources Azure hello</span><span class="sxs-lookup"><span data-stu-id="2455f-125">Download and understand hello Azure Resource Manager template</span></span>

<span data-ttu-id="2455f-126">Vous pouvez télécharger hello existant Azure Resource Manager modèle toocreate un réseau virtuel et deux sous-réseaux à partir de GitHub, apporter des modifications que vous souhaitez et la réutiliser.</span><span class="sxs-lookup"><span data-stu-id="2455f-126">You can download hello existing Azure Resource Manager template toocreate a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="2455f-127">toodo utilisez donc hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2455f-127">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="2455f-128">Accédez trop[créer une Application passerelle avec pare-feu d’applications web activé](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="2455f-128">Navigate too[Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="2455f-129">Cliquez sur **azuredeploy.json**, puis sur **RAW**.</span><span class="sxs-lookup"><span data-stu-id="2455f-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="2455f-130">Enregistrez le dossier local de hello fichier tooa sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2455f-130">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="2455f-131">Si vous êtes familiarisé avec les modèles Azure Resource Manager, ignorez toostep 7.</span><span class="sxs-lookup"><span data-stu-id="2455f-131">If you are familiar with Azure Resource Manager templates, skip toostep 7.</span></span>
1. <span data-ttu-id="2455f-132">Ouvrez le fichier hello que vous avez enregistré et examinez le contenu de hello sous **paramètres** en ligne</span><span class="sxs-lookup"><span data-stu-id="2455f-132">Open hello file that you saved and look at hello contents under **parameters** in line</span></span>
1. <span data-ttu-id="2455f-133">Les paramètres du modèle Azure Resource Manager fournissent un espace réservé pour les valeurs à remplir lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="2455f-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="2455f-134">Paramètre</span><span class="sxs-lookup"><span data-stu-id="2455f-134">Parameter</span></span> | <span data-ttu-id="2455f-135">Description</span><span class="sxs-lookup"><span data-stu-id="2455f-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="2455f-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="2455f-136">**subnetPrefix**</span></span> |<span data-ttu-id="2455f-137">Bloc CIDR pour le sous-réseau de passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-137">CIDR block for hello application gateway subnet.</span></span> |
  | <span data-ttu-id="2455f-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="2455f-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="2455f-139">Taille de la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-139">Size of hello application gateway.</span></span>  <span data-ttu-id="2455f-140">Le pare-feu d’applications web autorise uniquement les tailles moyenne et grande.</span><span class="sxs-lookup"><span data-stu-id="2455f-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="2455f-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="2455f-141">**backendIpaddress1**</span></span> |<span data-ttu-id="2455f-142">Adresse IP du premier serveur web de hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-142">IP address of hello first web server.</span></span> |
  | <span data-ttu-id="2455f-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="2455f-143">**backendIpaddress2**</span></span> |<span data-ttu-id="2455f-144">Adresse IP du serveur web de la deuxième hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-144">IP address of hello second web server.</span></span> |
  | <span data-ttu-id="2455f-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="2455f-145">**wafEnabled**</span></span> | <span data-ttu-id="2455f-146">La définition de toodetermine WAF est activé.</span><span class="sxs-lookup"><span data-stu-id="2455f-146">Setting toodetermine if WAF is enabled.</span></span>|
  | <span data-ttu-id="2455f-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="2455f-147">**wafMode**</span></span> | <span data-ttu-id="2455f-148">Mode de pare-feu d’applications web hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-148">Mode of hello web application firewall.</span></span>  <span data-ttu-id="2455f-149">Les options disponibles sont **prévention** ou **détection**.</span><span class="sxs-lookup"><span data-stu-id="2455f-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="2455f-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="2455f-150">**wafRuleSetType**</span></span> | <span data-ttu-id="2455f-151">Type de groupe de règles du pare-feu d’applications web.</span><span class="sxs-lookup"><span data-stu-id="2455f-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="2455f-152">Actuellement OWASP avoir est hello pris en charge uniquement les option.</span><span class="sxs-lookup"><span data-stu-id="2455f-152">Currently OWASP is hello only supported option.</span></span> |
  | <span data-ttu-id="2455f-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="2455f-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="2455f-154">Version de groupe de règles.</span><span class="sxs-lookup"><span data-stu-id="2455f-154">Ruleset version.</span></span> <span data-ttu-id="2455f-155">Options de hello pris en charge sont actuellement OWASP CRS 2.2.9 et 3.0.</span><span class="sxs-lookup"><span data-stu-id="2455f-155">OWASP CRS 2.2.9 and 3.0 are currently hello supported options.</span></span> |

1. <span data-ttu-id="2455f-156">Vérifiez le contenu de hello sous **ressources** et avis hello les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="2455f-156">Check hello content under **resources** and notice hello following properties:</span></span>

   * <span data-ttu-id="2455f-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="2455f-157">**type**.</span></span> <span data-ttu-id="2455f-158">Type de ressource en cours de création par le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-158">Type of resource being created by hello template.</span></span> <span data-ttu-id="2455f-159">Dans ce cas, le type de hello est `Microsoft.Network/applicationGateways`, qui représente une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2455f-159">In this case, hello type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="2455f-160">**name**.</span><span class="sxs-lookup"><span data-stu-id="2455f-160">**name**.</span></span> <span data-ttu-id="2455f-161">Nom de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-161">Name for hello resource.</span></span> <span data-ttu-id="2455f-162">Utilisation de hello avis de `[parameters('applicationGatewayName')]`, ce qui signifie que ce nom hello est fourni en tant qu’entrée par vous ou par un fichier de paramètres au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="2455f-162">Notice hello use of `[parameters('applicationGatewayName')]`, which means that hello name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="2455f-163">**properties**.</span><span class="sxs-lookup"><span data-stu-id="2455f-163">**properties**.</span></span> <span data-ttu-id="2455f-164">Liste de propriétés pour la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-164">List of properties for hello resource.</span></span> <span data-ttu-id="2455f-165">Ce modèle utilise un réseau virtuel de hello et l’adresse IP publique lors de la création de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2455f-165">This template uses hello virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2455f-166">Pour plus d’informations sur les modèles, consultez [Référence sur les modèles Resource Manager](/templates/).</span><span class="sxs-lookup"><span data-stu-id="2455f-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="2455f-167">Naviguer vers l’arrière trop[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="2455f-167">Navigate back too[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="2455f-168">Cliquez sur **azuredeploy-parameters.json**, puis sur **RAW**.</span><span class="sxs-lookup"><span data-stu-id="2455f-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="2455f-169">Enregistrez le dossier local de hello fichier tooa sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2455f-169">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="2455f-170">Ouvrir le fichier hello que vous avez enregistré et modifier les valeurs hello pour les paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-170">Open hello file that you saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="2455f-171">Utilisez hello suivant la passerelle d’application hello toodeploy valeurs décrite dans notre scénario.</span><span class="sxs-lookup"><span data-stu-id="2455f-171">Use hello following values toodeploy hello application gateway described in our scenario.</span></span>

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

1. <span data-ttu-id="2455f-172">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-172">Save hello file.</span></span> <span data-ttu-id="2455f-173">Vous pouvez tester le modèle JSON hello et modèle de paramètre à l’aide des outils de validation JSON en ligne comme [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="2455f-173">You can test hello JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="2455f-174">Déployer le modèle de hello Azure Resource Manager à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="2455f-174">Deploy hello Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="2455f-175">Si vous n’avez jamais utilisé Azure PowerShell, visitez : [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) et suivez hello instructions toosign dans Azure et sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="2455f-175">If you have never used Azure PowerShell, visit: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions toosign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="2455f-176">Connexion tooPowerShell</span><span class="sxs-lookup"><span data-stu-id="2455f-176">Login tooPowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="2455f-177">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-177">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="2455f-178">Vous êtes invité à tooauthenticate avec vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="2455f-178">You are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="2455f-179">Choisissez parmi vos toouse abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="2455f-179">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="2455f-180">Si nécessaire, créez un groupe de ressources à l’aide de hello **New-AzureResourceGroup** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="2455f-180">If needed, create a resource group by using hello **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="2455f-181">Bonjour l’exemple suivant, vous créez un groupe de ressources appelé AppgatewayRG dans l’emplacement de l’est des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="2455f-181">In hello following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="2455f-182">Exécutez hello **New-AzureRmResourceGroupDeployment** applet de commande toodeploy hello nouveau réseau virtuel à l’aide de hello précédant les fichiers de modèle et les paramètres vous avez téléchargé et modifié.</span><span class="sxs-lookup"><span data-stu-id="2455f-182">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toodeploy hello new virtual network by using hello preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a><span data-ttu-id="2455f-183">Déploiement de modèle de gestionnaire de ressources Azure hello à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="2455f-183">Deploy hello Azure Resource Manager template by using hello Azure CLI</span></span>

<span data-ttu-id="2455f-184">modèle de gestionnaire de ressources Azure hello toodeploy vous avez téléchargé à l’aide de CLI d’Azure, suivez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2455f-184">toodeploy hello Azure Resource Manager template you downloaded by using Azure CLI, follow hello following steps:</span></span>

1. <span data-ttu-id="2455f-185">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](/cli/azure/install-azure-cli) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="2455f-185">If you have never used Azure CLI, see [Install and configure hello Azure CLI](/cli/azure/install-azure-cli) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="2455f-186">Si nécessaire, hello exécution `az group create` commande toocreate un groupe de ressources, comme indiqué dans hello suivant extrait de code.</span><span class="sxs-lookup"><span data-stu-id="2455f-186">If necessary, run hello `az group create` command toocreate a resource group, as shown in hello following code snippet.</span></span> <span data-ttu-id="2455f-187">Notez la sortie hello de commande hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-187">Notice hello output of hello command.</span></span> <span data-ttu-id="2455f-188">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="2455f-188">hello list shown after hello output explains hello parameters used.</span></span> <span data-ttu-id="2455f-189">Pour plus d’informations sur les groupes de ressources, consultez la page [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2455f-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="2455f-190">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="2455f-190">**-n (or --name)**.</span></span> <span data-ttu-id="2455f-191">Nom du nouveau groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-191">Name for hello new resource group.</span></span> <span data-ttu-id="2455f-192">Pour notre scénario, il s’agit de *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="2455f-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="2455f-193">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="2455f-193">**-l (or --location)**.</span></span> <span data-ttu-id="2455f-194">Région Azure où le nouveau groupe de ressources hello est créé.</span><span class="sxs-lookup"><span data-stu-id="2455f-194">Azure region where hello new resource group is created.</span></span> <span data-ttu-id="2455f-195">Pour notre scénario, il s’agit de *westus*.</span><span class="sxs-lookup"><span data-stu-id="2455f-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="2455f-196">Exécutez hello `az group deployment create` applet de commande toodeploy hello nouveau réseau virtuel à l’aide des paramètres et modèle de hello fichiers vous téléchargé et modifié dans hello précédant l’étape.</span><span class="sxs-lookup"><span data-stu-id="2455f-196">Run hello `az group deployment create` cmdlet toodeploy hello new virtual network by using hello template and parameter files you downloaded and modified in hello preceding step.</span></span> <span data-ttu-id="2455f-197">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="2455f-197">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="2455f-198">Déployer le modèle de gestionnaire de ressources Azure de hello à l’aide de clic sur le déploiement</span><span class="sxs-lookup"><span data-stu-id="2455f-198">Deploy hello Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="2455f-199">Cliquez sur le déploiement est un autre moyen toouse modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2455f-199">Click-to-deploy is another way toouse Azure Resource Manager templates.</span></span> <span data-ttu-id="2455f-200">Il s’agit de des modèles de toouse facilement avec hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2455f-200">It's an easy way toouse templates with hello Azure portal.</span></span>

1. <span data-ttu-id="2455f-201">Accédez trop[créer une passerelle d’application avec le pare-feu d’applications web](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="2455f-201">Go too[Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="2455f-202">Cliquez sur **déployer tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="2455f-202">Click **Deploy tooAzure**.</span></span>

    ![Déployer tooAzure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="2455f-204">Renseignez les paramètres hello hello modèle de déploiement sur le portail hello et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2455f-204">Fill out hello parameters for hello deployment template on hello portal and click **OK**.</span></span>

    ![Paramètres](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="2455f-206">Sélectionnez **J’accepte les conditions susmentionnées générales toohello** et cliquez sur **bon**.</span><span class="sxs-lookup"><span data-stu-id="2455f-206">Select **I agree toohello terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="2455f-207">Dans le panneau de déploiement personnalisée hello, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="2455f-207">On hello Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-tooresource-manager-templates"></a><span data-ttu-id="2455f-208">Fournissant des certificats données tooResource Gestionnaire de modèles</span><span class="sxs-lookup"><span data-stu-id="2455f-208">Providing certificate data tooResource Manager templates</span></span>

<span data-ttu-id="2455f-209">Lors de l’utilisation de SSL avec un modèle de certificat de hello doit toobe fourni dans une chaîne base64, au lieu d’en cours de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="2455f-209">When using SSL with a template, hello certificate needs toobe provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="2455f-210">tooconvert base64 tooa .pfx ou .cer chaîne utilisez hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="2455f-210">tooconvert a .pfx or .cer tooa base64 string use one of hello following commands.</span></span> <span data-ttu-id="2455f-211">Hello les commandes suivantes convertissent hello certificat tooa chaîne base64, qui peut être fourni toohello modèle.</span><span class="sxs-lookup"><span data-stu-id="2455f-211">hello following commands convert hello certificate tooa base64 string, which can be provided toohello template.</span></span> <span data-ttu-id="2455f-212">Hello attendu la sortie est une chaîne qui peut être stockée dans une variable et collée dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="2455f-212">hello expected output is a string that can be stored in a variable and pasted in hello template.</span></span>

### <a name="macos"></a><span data-ttu-id="2455f-213">macOS</span><span class="sxs-lookup"><span data-stu-id="2455f-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="2455f-214">Windows</span><span class="sxs-lookup"><span data-stu-id="2455f-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="2455f-215">Supprimer toutes les ressources</span><span class="sxs-lookup"><span data-stu-id="2455f-215">Delete all resources</span></span>

<span data-ttu-id="2455f-216">toodelete toutes les ressources créées dans cet article, effectuez l’une de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2455f-216">toodelete all resources created in this article, complete one of hello following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="2455f-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2455f-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="2455f-218">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="2455f-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="2455f-219">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2455f-219">Next steps</span></span>

<span data-ttu-id="2455f-220">Si vous souhaitez tooconfigure le déchargement SSL, visitez : [configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="2455f-220">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="2455f-221">Si vous voulez tooconfigure un toouse de passerelle d’application avec un équilibrage de charge interne, visitez : [créer une passerelle d’application avec un équilibreur de charge interne (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="2455f-221">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="2455f-222">Si vous souhaitez plus d’informations sur les options d’équilibrage de charge en général, visitez :</span><span class="sxs-lookup"><span data-stu-id="2455f-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="2455f-223">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="2455f-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="2455f-224">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="2455f-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

