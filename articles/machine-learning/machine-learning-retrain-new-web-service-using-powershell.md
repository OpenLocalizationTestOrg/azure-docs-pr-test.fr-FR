---
title: aaaRetrain un service web de nouveau Azure Machine Learning avec PowerShell | Documents Microsoft
description: "Découvrez comment tooprogrammatically recycler un modèle et une mise à jour hello web service toouse hello qui vient d’être formé dans Azure Machine Learning à l’aide des applets de commande PowerShell de gestion de Machine Learning hello."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a>Recycler un service web de base du nouveau gestionnaire de ressources à l’aide des applets de commande PowerShell de gestion de Machine Learning hello
Lorsque vous recycler un nouveau service web, vous mettez à jour hello web prédictif service définition tooreference hello nouveau modèle formé.  

## <a name="prerequisites"></a>Composants requis
Vous devez configurer une expérience de formation et une expérimentation prédictive comme indiqué dans [Reformer des modèles Machine Learning par programme](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> expérience de prédictive Hello doit être déployé comme une gestionnaire de ressources Azure (nouveau) en fonction du service web machine learning. toodeploy un nouveau service web, vous devez disposer des autorisations suffisantes dans hello abonnement toowhich vous déployez le service web de hello. Pour plus d’informations, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

Pour plus d’informations sur le déploiement de services web, consultez [Déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

Ce processus suppose que vous avez installé hello applets de commande Azure Machine Learning. Pour plus d’informations d’installation des applets de commande hello Machine Learning, consultez hello [applets de commande Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) référence sur MSDN.

Hello copié informations suivantes à partir de hello réapprentissage de sortie :

* BaseLocation
* RelativeLocation

étapes Hello sont :

1. Connectez-vous tooyour compte de gestionnaire de ressources Azure.
2. Obtenir la définition du service web hello
3. Exportation hello définition du Service Web en tant que JSON
4. Mise à jour hello toohello ilearner objet blob de référence Bonjour JSON.
5. Importer des hello JSON dans une définition de Service Web
6. Mettre à jour de service web de hello avec la nouvelle définition de Service Web

## <a name="sign-in-tooyour-azure-resource-manager-account"></a>Connectez-vous à tooyour compte de gestionnaire de ressources Azure
Vous devez tout d’abord vous connecter tooyour compte Azure dans l’environnement PowerShell de hello à l’aide de hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) applet de commande.

## <a name="get-hello-web-service-definition"></a>Obtenir hello définition du Service Web
Ensuite, obtenez hello Web Service en appelant hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) applet de commande. Hello définition du Service Web est une représentation interne du modèle formé de hello du service web de hello et n’est pas directement modifiable. Assurez-vous que vous récupérez hello définition du Service Web pour votre expérience prédictive et pas votre expérience d’apprentissage.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

nom de groupe ressource toodetermine hello d’un service web existant, exécutez hello applet de commande Get-AzureRmMlWebService sans aucun service web de paramètres toodisplay hello dans votre abonnement. Recherchez le service web de hello et observez son ID de service web. nom Hello hello du groupe de ressources est hello quatrième élément de hello ID, juste après hello *resourceGroups* élément. Dans l’exemple suivant de hello, nom de groupe de ressources hello est par défaut-MachineLearning-SouthCentralUS.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

Vous pouvez également toodetermine hello nom groupe de ressources d’un service web existant, le portail de Services Web de Microsoft Azure Machine Learning toohello d’ouverture de session. Sélectionnez le service web de hello. nom de groupe de ressources Hello est hello cinquième élément de hello les URL du service web de hello, juste après hello *resourceGroups* élément. Dans l’exemple suivant de hello, nom de groupe de ressources hello est par défaut-MachineLearning-SouthCentralUS.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a>Exportation hello définition du Service Web en tant que JSON
toomodify hello définition toohello formé modèle toouse Bonjour qui vient d’être formé, vous devez d’abord utiliser hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport de l’applet de commande il fichier de format tooa JSON.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a>Mise à jour hello toohello ilearner objet blob de référence Bonjour JSON.
Dans les ressources hello, recherchez hello [modèle formé], mise à jour hello *uri* valeur Bonjour *locationInfo* nœud avec hello URI d’objet blob de hello ilearner. URI Hello est généré en combinant hello *BaseLocation* et hello *RelativeLocation* à partir de la sortie hello Hello appel de reconversion BES. Cela met à jour hello chemin d’accès tooreference hello nouveau modèle formé.

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition"></a>Importer des hello JSON dans une définition de Service Web
Vous devez utiliser hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) applet de commande tooconvert hello modifié le fichier JSON dans une définition de Service Web que vous pouvez utiliser tooupdate hello définition du Service Web.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a>Mettre à jour de service web de hello avec la nouvelle définition de Service Web
Enfin, vous utilisez [AzureRmMlWebService de mise à jour](https://msdn.microsoft.com/library/azure/mt767922.aspx) applet de commande tooupdate hello définition du Service Web.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a>Résumé
À l’aide de la gestion des applets de commande PowerShell d’apprentissage Machine hello, vous pouvez mettre à jour hello le modèle formé d’un Service Web prédictive des scénarios tels que :

* Nouvel apprentissage périodique d’un modèle avec de nouvelles données.
* Distribution d’un modèle de toocustomers avec comme objectif hello leur permettant de former le modèle de hello à l’aide de leurs propres données.

