---
title: "Créer un équilibrage de charge accessible sur Internet à l’aide du modèle Azure | Microsoft Docs"
description: "Découvrez comment créer un équilibreur de charge accessible sur Internet dans Resource Manager à l’aide d’un modèle"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d829000e63515814b192f3f8256e3b8637bb3a34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="74d66-103">Création d’un équilibrage de charge accessible sur Internet à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="74d66-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="74d66-104">Portail</span><span class="sxs-lookup"><span data-stu-id="74d66-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="74d66-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="74d66-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="74d66-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="74d66-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="74d66-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="74d66-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="74d66-108">Cet article traite du modèle de déploiement de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="74d66-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="74d66-109">Vous pouvez également [découvrir comment créer un équilibreur de charge accessible sur Internet à l'aide du modèle de déploiement classique](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="74d66-109">You can also [Learn how to create an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="74d66-110">Déployer le modèle en un clic</span><span class="sxs-lookup"><span data-stu-id="74d66-110">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="74d66-111">L’exemple de modèle disponible dans le référentiel public utilise un fichier de paramètres contenant les valeurs par défaut utilisées pour générer le scénario décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="74d66-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="74d66-112">Pour déployer ce modèle en un clic, suivez [ce lien](http://go.microsoft.com/fwlink/?LinkId=544801), cliquez sur **Déployer dans Azure**, remplacez les valeurs de paramètre par défaut si nécessaire, puis suivez les instructions dans le portail.</span><span class="sxs-lookup"><span data-stu-id="74d66-112">To deploy this template using click to deploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="74d66-113">Déployer le modèle à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="74d66-113">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="74d66-114">Pour déployer le modèle téléchargé à l’aide de PowerShell, suivez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="74d66-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="74d66-115">Si vous n’avez jamais utilisé Azure PowerShell, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) et suivez les instructions jusqu’à la fin pour vous connecter à Azure et sélectionner votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="74d66-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="74d66-116">Pour créer un groupe de ressources à l'aide du modèle, exécutez l'applet de commande **New-AzureRmResourceGroupDeployment** .</span><span class="sxs-lookup"><span data-stu-id="74d66-116">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="74d66-117">Déployer le modèle à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="74d66-117">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="74d66-118">Pour déployer le modèle à l’aide de l’interface de ligne de commande Azure, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="74d66-118">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="74d66-119">Si vous n’avez jamais utilisé l’interface de ligne de commande Azure, consultez [Installation et configuration de l’interface de ligne de commande Azure](../cli-install-nodejs.md) et suivez les instructions jusqu’à l’étape vous invitant à sélectionner votre compte et votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="74d66-119">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="74d66-120">Exécutez la commande **azure config mode** pour passer en mode Resource Manager, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="74d66-120">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="74d66-121">Voici le résultat attendu pour la commande ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="74d66-121">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="74d66-122">Dans votre navigateur, accédez au [modèle de démarrage rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copiez le contenu du fichier json et collez-le dans un nouveau fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="74d66-122">From your browser, navigate to [the Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy the contents of the json file and paste into a new file in your computer.</span></span> <span data-ttu-id="74d66-123">Pour ce scénario, vous allez copier les valeurs ci-dessous dans un fichier nommé **C:\lb\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="74d66-123">For this scenario, you would be copying the values below to a file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="74d66-124">Exécutez l’applet de commande **azure group deployment create** pour déployer le nouvel équilibreur de charge à l’aide du modèle et des fichiers de paramètres que vous avez téléchargés et modifiés plus tôt.</span><span class="sxs-lookup"><span data-stu-id="74d66-124">Run the **azure group deployment create** cmdlet to deploy the new load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="74d66-125">La liste affichée après le résultat présente les différents paramètres utilisés.</span><span class="sxs-lookup"><span data-stu-id="74d66-125">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="74d66-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="74d66-126">Next steps</span></span>

[<span data-ttu-id="74d66-127">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="74d66-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="74d66-128">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="74d66-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="74d66-129">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="74d66-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
