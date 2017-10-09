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
# <a name="create-an-internal-load-balancer-using-a-template"></a>Créer un équilibrage de charge interne à l’aide d’un modèle

> [!div class="op_single_selector"]
> * [Portail Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Modèle](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).  Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Déployer le modèle de hello à l’aide de cliquez sur toodeploy

Hello exemple de modèle disponible dans le référentiel de public hello utilise un fichier de paramètre contenant le scénario hello hello par défaut les valeurs utilisées toogenerate décrit ci-dessus. toodeploy ce modèle à l’aide de cliquez toodeploy, suivez [ce lien](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), cliquez sur **déployer tooAzure**, remplacez les valeurs de paramètre par défaut hello si nécessaire et suivez les instructions de hello dans le portail de hello.

## <a name="deploy-hello-template-by-using-powershell"></a>Déployer le modèle de hello à l’aide de PowerShell

modèle de hello toodeploy vous avez téléchargé à l’aide de PowerShell, suivez les étapes de hello ci-dessous.

1. Si vous n’avez jamais utilisé Azure PowerShell, consultez [comment tooInstall et configurer Azure PowerShell](/powershell/azure/overview) et suivez les instructions de hello tous les toohello de façon hello fin toosign dans Azure et sélectionnez votre abonnement.
2. Téléchargez le disque local du fichier tooyour de hello paramètres.
3. Modifier le fichier de hello et enregistrez-le.
4. Exécutez hello **New-AzureRmResourceGroupDeployment** toocreate d’applet de commande un groupe de ressources à l’aide de hello modèle.

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Déployer le modèle de hello à l’aide de hello CLI d’Azure

modèle de hello toodeploy à l’aide de hello CLI d’Azure, suivez les étapes de hello ci-dessous.

1. Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.
2. Exécutez hello **configuration azure mode** mode Manager tooResource commande tooswitch, comme indiqué ci-dessous.

    ```azurecli
    azure config mode arm
    ```

    Voici la sortie hello attendu pour la commande hello ci-dessus :

        info:    New mode is arm

3. Ouvrez le fichier de paramètres hello son contenu et sélectionnez Enregistrer tooa fichier sur votre ordinateur. Pour cet exemple, nous avons enregistré des fichiers de paramètres hello trop*parameters.json*.
4. Exécutez hello **créer de déploiement de groupe azure** commande toodeploy hello un équilibrage de charge interne à l’aide des paramètres et modèle de hello fichiers téléchargés et de modifier les propriétés. liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a>Étapes suivantes

[Configurer le mode de distribution d’équilibreur de charge à l’aide de l’affinité d’IP source](load-balancer-distribution-mode.md)

[Configuration des paramètres de délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)

