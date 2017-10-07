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
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a>Création d’un équilibrage de charge accessible sur Internet à l’aide d’un modèle

> [!div class="op_single_selector"]
> * [Portail](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Modèle](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello. Vous pouvez également [apprendre comment toocreate une connecté à Internet à l’aide du modèle de déploiement classique de l’équilibrage de charge](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Déployer le modèle de hello à l’aide de cliquez sur toodeploy

Hello exemple de modèle disponible dans le référentiel de public hello utilise un fichier de paramètre contenant le scénario hello hello par défaut les valeurs utilisées toogenerate décrit ci-dessus. toodeploy ce modèle à l’aide de cliquez toodeploy, suivez [ce lien](http://go.microsoft.com/fwlink/?LinkId=544801), cliquez sur **déployer tooAzure**, remplacez les valeurs de paramètre par défaut hello si nécessaire et suivez les instructions de hello dans le portail de hello.

## <a name="deploy-hello-template-by-using-powershell"></a>Déployer le modèle de hello à l’aide de PowerShell

modèle de hello toodeploy vous avez téléchargé à l’aide de PowerShell, suivez les étapes de hello ci-dessous.

1. Si vous n’avez jamais utilisé Azure PowerShell, consultez [comment tooInstall et configurer Azure PowerShell](/powershell/azure/overview) et suivez les instructions de hello tous les toohello de façon hello fin toosign dans Azure et sélectionnez votre abonnement.
2. Exécutez hello **New-AzureRmResourceGroupDeployment** toocreate d’applet de commande un groupe de ressources à l’aide de hello modèle.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
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

3. À partir de votre navigateur, accédez trop[hello Quickstart modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copiez hello du contenu du fichier json de hello et collez dans un nouveau fichier sur votre ordinateur. Pour ce scénario, vous serez copie les valeurs hello ci-dessous fichier tooa nommé **c:\lb\azuredeploy.parameters.json**.
4. Exécutez hello **créer de déploiement de groupe azure** applet de commande toodeploy hello un équilibrage de charge à l’aide des paramètres et modèle de hello fichiers téléchargés et de modifier les propriétés. liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a>Étapes suivantes

[Prise en main de la configuration d’un équilibrage de charge interne](load-balancer-get-started-ilb-arm-ps.md)

[Configuration d'un mode de distribution d'équilibrage de charge](load-balancer-distribution-mode.md)

[Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)
