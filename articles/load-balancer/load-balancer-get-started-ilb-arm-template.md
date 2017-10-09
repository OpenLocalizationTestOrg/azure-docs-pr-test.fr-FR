---
title: "aaaCreate un équilibreur de charge interne - modèle Azure | Documents Microsoft"
description: "Découvrez comment toocreate un interne l’équilibrage de charge à l’aide d’un modèle dans le Gestionnaire de ressources"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="82489-103">Créer un équilibrage de charge interne à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="82489-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="82489-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="82489-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="82489-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="82489-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="82489-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="82489-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="82489-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="82489-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="82489-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="82489-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="82489-109">Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="82489-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="82489-110">Déployer le modèle de hello à l’aide de cliquez sur toodeploy</span><span class="sxs-lookup"><span data-stu-id="82489-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="82489-111">Hello exemple de modèle disponible dans le référentiel de public hello utilise un fichier de paramètre contenant le scénario hello hello par défaut les valeurs utilisées toogenerate décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="82489-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="82489-112">toodeploy ce modèle à l’aide de cliquez toodeploy, suivez [ce lien](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), cliquez sur **déployer tooAzure**, remplacez les valeurs de paramètre par défaut hello si nécessaire et suivez les instructions de hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="82489-112">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="82489-113">Déployer le modèle de hello à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="82489-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="82489-114">modèle de hello toodeploy vous avez téléchargé à l’aide de PowerShell, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="82489-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="82489-115">Si vous n’avez jamais utilisé Azure PowerShell, consultez [comment tooInstall et configurer Azure PowerShell](/powershell/azure/overview) et suivez les instructions de hello tous les toohello de façon hello fin toosign dans Azure et sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="82489-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="82489-116">Téléchargez le disque local du fichier tooyour de hello paramètres.</span><span class="sxs-lookup"><span data-stu-id="82489-116">Download hello parameters file tooyour local disk.</span></span>
3. <span data-ttu-id="82489-117">Modifier le fichier de hello et enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="82489-117">Edit hello file and save it.</span></span>
4. <span data-ttu-id="82489-118">Exécutez hello **New-AzureRmResourceGroupDeployment** toocreate d’applet de commande un groupe de ressources à l’aide de hello modèle.</span><span class="sxs-lookup"><span data-stu-id="82489-118">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="82489-119">Déployer le modèle de hello à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="82489-119">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="82489-120">modèle de hello toodeploy à l’aide de hello CLI d’Azure, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="82489-120">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="82489-121">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="82489-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="82489-122">Exécutez hello **configuration azure mode** mode Manager tooResource commande tooswitch, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="82489-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="82489-123">Voici la sortie hello attendu pour la commande hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="82489-123">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="82489-124">Ouvrez le fichier de paramètres hello son contenu et sélectionnez Enregistrer tooa fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="82489-124">Open hello parameter file, select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="82489-125">Pour cet exemple, nous avons enregistré des fichiers de paramètres hello trop*parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="82489-125">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="82489-126">Exécutez hello **créer de déploiement de groupe azure** commande toodeploy hello un équilibrage de charge interne à l’aide des paramètres et modèle de hello fichiers téléchargés et de modifier les propriétés.</span><span class="sxs-lookup"><span data-stu-id="82489-126">Run hello **azure group deployment create** command toodeploy hello new internal load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="82489-127">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="82489-127">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="82489-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82489-128">Next steps</span></span>

[<span data-ttu-id="82489-129">Configurer le mode de distribution d’équilibreur de charge à l’aide de l’affinité d’IP source</span><span class="sxs-lookup"><span data-stu-id="82489-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="82489-130">Configuration des paramètres de délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="82489-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

