---
title: "ressources aaaDeploy avec l’API REST et modèle | Documents Microsoft"
description: "Utilisez le Gestionnaire de ressources Azure et les REST API du Gestionnaire de ressources toodeploy une tooAzure de ressources. ressources de Hello sont définies dans un modèle de gestionnaire de ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a>Déployer des ressources à l’aide de modèles Resource Manager et de l’API REST Resource Manager
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Interface de ligne de commande Azure](resource-group-template-deploy-cli.md)
> * [Portail](resource-group-template-deploy-portal.md)
> * [API REST](resource-group-template-deploy-rest.md)
> 
> 

Cet article explique comment toouse hello REST API du Gestionnaire de ressources avec le Gestionnaire de ressources modèles toodeploy, tooAzure de vos ressources.  

> [!TIP]
> Pour obtenir de l’aide dans le débogage d’une erreur pendant le déploiement, consultez :
> 
> * [Afficher les opérations de déploiement](resource-manager-deployment-operations.md) toolearn sur l’obtention des informations qui vous permet de corriger votre erreur
> * [Résoudre les erreurs courantes lors du déploiement de ressources tooAzure avec Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn comment les erreurs de déploiement courantes tooresolve
> 
> 

Votre modèle peut être un fichier local ou un fichier externe disponible par le biais d’un URI. Lorsque votre modèle se trouve dans un compte de stockage, vous pouvez restreindre le modèle de toohello access et fournir un jeton de signature (SAS) d’accès partagé au cours du déploiement.

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a>Déployer avec hello API REST
1. Définissez [des en-têtes et des paramètres communs](https://docs.microsoft.com/rest/api/index), y compris des jetons d’authentification.
2. Si vous n’avez pas de groupe de ressources, créez-en un. Fournissez votre ID d’abonnement, le nom de hello du nouveau groupe de ressources hello et l’emplacement que vous avez besoin pour votre solution. Pour plus d’informations, consultez [Créer un groupe de ressources](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. Valider votre déploiement avant son exécution en exécutant hello [valider un déploiement de modèle](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) opération. Lorsque vous testez le déploiement de hello, spécifiez les paramètres exactement comme vous le feriez lors de l’exécution du déploiement hello (illustrée dans l’étape suivante de hello).
4. Créez un déploiement. Fournissez votre ID d’abonnement, hello nom hello du groupe de ressources, hello nom du déploiement de hello et un modèle de tooyour de lien. Pour plus d’informations sur le fichier de modèle hello, consultez [fichier de paramètres](#parameter-file). Pour plus d’informations sur l’API REST de hello toocreate un groupe de ressources, consultez [créer un déploiement de modèle](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate). Hello d’avis **mode** est défini trop**incrémentiel**. toorun un déploiement complet, définissez **mode** trop**Complete**. Soyez prudent lorsque le mode hello complète que vous pouvez supprimer par inadvertance des ressources qui ne sont pas dans votre modèle.
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      Si vous souhaitez toolog contenu de la réponse, le contenu de la demande ou les deux, inclure **debugSetting** dans la demande hello.
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      Vous pouvez configurer votre toouse de compte de stockage un jeton de signature (SAS) d’accès partagé. Pour plus d’informations, consultez [Délégation de l’accès avec une signature d’accès partagé](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).
5. Obtenir l’état de hello de déploiement de modèle hello. Pour plus d’informations, consultez [Obtenir des informations sur le déploiement d’un modèle](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a>Fichier de paramètres

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur la gestion des opérations asynchrones de REST, consultez [le suivi des opérations asynchrones Azure](resource-manager-async-operations.md).
* Pour obtenir un exemple de déploiement de ressources via la bibliothèque cliente .NET hello, consultez [déployer des ressources à l’aide de bibliothèques .NET et un modèle](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* paramètres de toodefine dans le modèle, consultez [création de modèles](resource-group-authoring-templates.md#parameters).
* Pour obtenir des conseils sur le déploiement de vos environnements toodifferent de solution, consultez [environnements de développement et de test dans Microsoft Azure](solution-dev-test-environments.md).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

