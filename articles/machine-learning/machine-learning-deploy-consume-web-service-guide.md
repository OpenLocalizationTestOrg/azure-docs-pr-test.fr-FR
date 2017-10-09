---
title: "Services web Azure Machine Learning : déploiement et consommation | Microsoft Docs"
description: "Ressources pour le déploiement et la consommation de services web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a>Services web Azure Machine Learning : déploiement et consommation
Vous pouvez utiliser des modèles et flux de travail de l’apprentissage automatique toodeploy Azure Machine Learning en tant que services web. Ces services web peuvent ensuite être utilisé toocall hello l’apprentissage automatique modèles à partir d’applications sur des prévisions hello Internet toodo en temps réel ou en mode batch. Les services web hello étant RESTful, vous pouvez les appeler à partir de différents langages de programmation et les plateformes, comme .NET et Java et d’applications, telles qu’Excel.

Hello les sections suivantes fournissent des liens toowalkthroughs, le code et documentation toohelp vous aider à démarrer.

## <a name="deploy-a-web-service"></a>Déployer un service web
### <a name="with-azure-machine-learning-studio"></a>Avec Azure Machine Learning Studio
Machine Learning Studio et du portail de Services Web de Microsoft Azure Machine Learning hello vous aider à déployer et gérer un service web sans écrire de code.

Hello liens suivants fournissent des informations générales sur la façon de toodeploy un nouveau service web :

* Pour obtenir une présentation toodeploy un nouveau service web qui est basé sur le Gestionnaire de ressources Azure, voir [déployer un nouveau service web](machine-learning-webservice-deploy-a-web-service.md).
* Pour une procédure pas à pas sur la façon toodeploy un service web, consultez [déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).
* Pour une procédure pas à pas complète sur la façon toocreate et déployer un service web, consultez [procédure pas à pas étape 1 : créer un espace de travail Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md).
* Pour des exemples spécifiques de déploiement d’un service web, consultez :

  * [Procédure pas à pas, étape 5 : Déployer le service web de Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md)
  * [Comment toodeploy un site web de service toomultiple régions](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a>Avec les API du fournisseur de ressources des services web (API Azure Resource Manager)
fournisseur de ressources Azure Machine Learning Hello pour les services web permet le déploiement et la gestion des services web à l’aide d’appels d’API REST. Pour plus de détails, consultez la référence [Service web Machine Learning (REST)](/rest/api/machinelearning/index).

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a>Avec des applets de commande PowerShell
Le fournisseur de ressources Azure Machine Learning pour les services web permet le déploiement et la gestion des services web au moyen d’applets de commande PowerShell.

applets de commande hello toouse, vous devez vous connecter tooyour compte Azure dans l’environnement PowerShell de hello à l’aide de hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) applet de commande. Si vous n’êtes pas familiarisé avec le fonctionnement des commandes toocall PowerShell qui sont basées sur le Gestionnaire de ressources, consultez [à l’aide de Azure PowerShell avec Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).

tooexport votre prédictive de faire des essais, d’utiliser [cet exemple de code](https://github.com/ritwik20/AzureML-WebServices). Après avoir créé le fichier .exe de hello à partir du code hello, vous pouvez taper :

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

Exécute l’application hello crée un modèle JSON du service web. toouse hello modèle toodeploy un service web, vous devez ajouter hello informations suivantes :

* Nom et clé du compte de stockage

    Vous pouvez obtenir le nom de compte de stockage hello et la clé à partir de deux hello [portail Azure](https://portal.azure.com/) ou hello [portail Azure classic](http://manage.windowsazure.com/).
* ID de plan d’engagement

    Vous pouvez obtenir l’ID de plan hello de hello [Azure Machine Learning Services Web](https://services.azureml.net) portail en vous connectant et en cliquant sur un nom de plan.

Ajoutez-les modèle JSON de toohello en tant qu’enfants de hello *propriétés* nœud hello de même niveau en tant que hello *MachineLearningWorkspace* nœud.

Voici un exemple :

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

Consultez hello suivant des articles et exemples de code pour plus d’informations :

* [Applets de commande Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) sur MSDN
* Exemple de [procédure pas à pas](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) sur GitHub

## <a name="consume-hello-web-services"></a>Utiliser les services web hello
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a>À partir de hello Azure Machine Learning Services interface utilisateur Web (test)
Vous pouvez tester votre service web à partir du portail de Services Web de Azure Machine Learning hello. Cela comprend le test du service de requête-réponse hello (RR) et des interfaces de service de l’exécution par lots (BES).

* [Déployer comme un nouveau service web](machine-learning-webservice-deploy-a-web-service.md)
* [Déploiement d’un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)
* [Procédure pas à pas, étape 5 : Déployer le service web de Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a>À partir d’Excel
Vous pouvez télécharger un modèle Excel qui utilise le service web de hello :

* [Utilisation d’un service web Microsoft Azure Machine Learning à partir de Microsoft Excel.](machine-learning-consuming-from-excel.md)
* [Complément Excel de services web Azure Machine Learning](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a>À partir d’un client basé sur REST
Les services web Azure Machine Learning sont des API RESTful. Vous pouvez utiliser ces API à partir de différentes plateformes, telles que .NET, Python, R, Java, hello de etc. **consommer** page de votre service web sur hello [portail de Services Web de Microsoft Azure Machine Learning](https://services.azureml.net) a exemple code qui peut vous aider à commencer. Pour plus d’informations, consultez [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).
