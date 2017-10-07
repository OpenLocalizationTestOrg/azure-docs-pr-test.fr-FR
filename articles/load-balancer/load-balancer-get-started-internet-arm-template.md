---
title: "équilibrage de charge aaaCreate une côté Internet - modèle Azure | Documents Microsoft"
description: "Découvrez comment toocreate une connecté à Internet l’équilibrage de charge dans le Gestionnaire de ressources à l’aide d’un modèle"
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
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="77298-103">Création d’un équilibrage de charge accessible sur Internet à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="77298-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="77298-104">Portail</span><span class="sxs-lookup"><span data-stu-id="77298-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="77298-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="77298-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="77298-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="77298-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="77298-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="77298-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="77298-108">Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="77298-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="77298-109">Vous pouvez également [apprendre comment toocreate une connecté à Internet à l’aide du modèle de déploiement classique de l’équilibrage de charge](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="77298-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="77298-110">Déployer le modèle de hello à l’aide de cliquez sur toodeploy</span><span class="sxs-lookup"><span data-stu-id="77298-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="77298-111">Hello exemple de modèle disponible dans le référentiel de public hello utilise un fichier de paramètre contenant le scénario hello hello par défaut les valeurs utilisées toogenerate décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="77298-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="77298-112">toodeploy ce modèle à l’aide de cliquez toodeploy, suivez [ce lien](http://go.microsoft.com/fwlink/?LinkId=544801), cliquez sur **déployer tooAzure**, remplacez les valeurs de paramètre par défaut hello si nécessaire et suivez les instructions de hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="77298-112">toodeploy this template using click toodeploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="77298-113">Déployer le modèle de hello à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="77298-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="77298-114">modèle de hello toodeploy vous avez téléchargé à l’aide de PowerShell, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="77298-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="77298-115">Si vous n’avez jamais utilisé Azure PowerShell, consultez [comment tooInstall et configurer Azure PowerShell](/powershell/azure/overview) et suivez les instructions de hello tous les toohello de façon hello fin toosign dans Azure et sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="77298-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="77298-116">Exécutez hello **New-AzureRmResourceGroupDeployment** toocreate d’applet de commande un groupe de ressources à l’aide de hello modèle.</span><span class="sxs-lookup"><span data-stu-id="77298-116">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="77298-117">Déployer le modèle de hello à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="77298-117">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="77298-118">modèle de hello toodeploy à l’aide de hello CLI d’Azure, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="77298-118">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="77298-119">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="77298-119">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="77298-120">Exécutez hello **configuration azure mode** mode Manager tooResource commande tooswitch, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="77298-120">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="77298-121">Voici la sortie hello attendu pour la commande hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="77298-121">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="77298-122">À partir de votre navigateur, accédez trop[hello Quickstart modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copiez hello du contenu du fichier json de hello et collez dans un nouveau fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="77298-122">From your browser, navigate too[hello Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy hello contents of hello json file and paste into a new file in your computer.</span></span> <span data-ttu-id="77298-123">Pour ce scénario, vous serez copie les valeurs hello ci-dessous fichier tooa nommé **c:\lb\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="77298-123">For this scenario, you would be copying hello values below tooa file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="77298-124">Exécutez hello **créer de déploiement de groupe azure** applet de commande toodeploy hello un équilibrage de charge à l’aide des paramètres et modèle de hello fichiers téléchargés et de modifier les propriétés.</span><span class="sxs-lookup"><span data-stu-id="77298-124">Run hello **azure group deployment create** cmdlet toodeploy hello new load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="77298-125">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="77298-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="77298-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="77298-126">Next steps</span></span>

[<span data-ttu-id="77298-127">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="77298-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="77298-128">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="77298-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="77298-129">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="77298-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
