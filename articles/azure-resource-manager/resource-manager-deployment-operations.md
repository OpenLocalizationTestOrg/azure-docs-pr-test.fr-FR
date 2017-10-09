---
title: "aaaDeployment opérations avec Azure Resource Manager | Documents Microsoft"
description: "Décrit comment les opérations de déploiement d’Azure Resource Manager tooview avec hello portal, PowerShell, CLI d’Azure et les API REST."
services: azure-resource-manager,virtual-machines
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: infrastructure
ms.date: 01/13/2017
ms.author: tomfitz
ms.openlocfilehash: ba4823ca73caca83dfc07c99d736344ef8b7b54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a>Afficher les opérations de déploiement avec Azure Resource Manager


Vous pouvez afficher les opérations hello pour un déploiement via hello portail Azure. Vous serez peut-être plus vous souhaitez afficher les opérations de hello lorsque vous avez reçu une erreur lors du déploiement pour cet article se concentre sur l’affichage des opérations qui ont échoué. portail de Hello fournit une interface qui vous permet d’erreurs de hello tooeasily rechercher et déterminer les corrections éventuelles.

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a>Portail
opérations de déploiement toosee hello, utilisez hello comme suit :

1. Pour le groupe de ressources hello impliquée dans le déploiement de hello, notez l’état hello du dernier déploiement de hello. Vous pouvez sélectionner cette tooget état plus de détails.
   
    ![état du déploiement](./media/resource-manager-deployment-operations/deployment-status.png)
2. Vous consultez l’historique de déploiement récente hello. Sélectionnez le déploiement hello qui a échoué.
   
    ![état du déploiement](./media/resource-manager-deployment-operations/select-deployment.png)
3. Sélectionnez toosee de lien de hello expliquant pourquoi hello Échec du déploiement. Dans l’image hello ci-dessous, un enregistrement DNS hello n’est pas unique.  
   
    ![afficher le déploiement ayant échoué](./media/resource-manager-deployment-operations/view-error.png)
   
    Ce message d’erreur doit être suffisante pour vous toobegin résolution des problèmes. Toutefois, si vous avez besoin de plus d’informations sur les tâches ont été effectuées, vous pouvez afficher les opérations hello comme indiqué dans hello comme suit.
4. Vous pouvez afficher toutes les opérations de déploiement hello Bonjour **déploiement** panneau. Sélectionnez n’importe quel toosee opération plus de détails.
   
    ![afficher des opérations](./media/resource-manager-deployment-operations/view-operations.png)
   
    Dans ce cas, vous voyez que le compte de stockage hello et réseau virtuel à haute disponibilité ont été créés. Échec de l’adresse IP publique de Hello et autres ressources n’ont pas été tentées.
5. Vous pouvez afficher les événements pour le déploiement de hello en sélectionnant **événements**.
   
    ![visualiser les événements](./media/resource-manager-deployment-operations/view-events.png)
6. Voir tous les événements hello pour le déploiement de hello et de sélectionner n’importe quelle pour plus de détails. Notez que trop hello ID de corrélation. Cette valeur peut être utile lorsque vous travaillez avec le support technique tootroubleshoot un déploiement.
   
    ![voir les événements](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a>PowerShell
1. tooget hello état global d’un déploiement, utilisez hello **Get-AzureRmResourceGroupDeployment** commande. 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   Ou bien, vous pouvez filtrer les résultats de hello pour uniquement ces déploiements qui ont échoué.

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. Chaque déploiement comprend plusieurs opérations. Chaque opération représente une étape dans le processus de déploiement hello. toodiscover la cause du problème avec un déploiement, vous devez généralement toosee plus d’informations sur les opérations de déploiement hello. Vous pouvez voir État hello d’opérations hello avec **Get-AzureRmResourceGroupDeploymentOperation**.

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    Qui retourne plusieurs opérations à chacun d’eux Bonjour suivant le format :

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. tooget plus de détails sur les opérations ayant échoué, récupérer les propriétés de hello pour les opérations avec **n’a pas pu** état.

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    Qui retourne que tous les hello opérations ayant échoué avec chacun d’eux Bonjour suivant le format :

  ```powershell
  provisioningOperation : Create
  provisioningState     : Failed
  timestamp             : 2016-06-14T21:54:55.1468068Z
  duration              : PT3.1449887S
  trackingId            : f4ed72f8-4203-43dc-958a-15d041e8c233
  serviceRequestId      : a426f689-5d5a-448d-a2f0-9784d14c900a
  statusCode            : BadRequest
  statusMessage         : @{error=}
  targetResource        : @{id=/subscriptions/{guid}/resourceGroups/ExampleGroup/providers/
                          Microsoft.Network/publicIPAddresses/myPublicIP;
                          resourceType=Microsoft.Network/publicIPAddresses; resourceName=myPublicIP}
  ```

    Notez les %%ServiceRequestID%% hello et trackingId hello pour l’opération de hello. Hello %%ServiceRequestID%% peut être utile lorsque vous travaillez avec le support technique tootroubleshoot un déploiement. Vous utiliserez hello trackingId dans hello prochaine étape toofocus sur une opération particulière.
4. tooget hello message d’état d’une opération ayant échouée particulière, hello utilisez commande suivante :

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    Résultat :

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. Chaque opération de déploiement dans Azure inclut le contenu de la demande et de la réponse. contenu de la demande Hello est ce que vous avez envoyé tooAzure durant le déploiement (par exemple, créer une machine virtuelle, disque de système d’exploitation et d’autres ressources). contenu de la réponse Hello est envoyé par le Azure à partir de votre demande de déploiement. Au cours du déploiement, vous pouvez utiliser **DeploymentDebugLogLevel** toospecify habituellement qui hello requête et/ou de réponse sont conservés dans le journal de hello. 

  Vous obtenez ces informations à partir du journal de hello et l’enregistrer localement à l’aide de hello suivant de commandes PowerShell :

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a>Interface de ligne de commande Azure

1. Obtenir hello état global d’un déploiement avec hello **afficher de déploiement de groupe azure** commande.

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  Une des valeurs renvoyée de hello est hello **correlationId**. Cette valeur est utilisée tootrack les événements liés, et peut être utile dans les cas des tootroubleshoot de support technique un déploiement.

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. opérations de hello toosee pour un déploiement, utilisez :

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a>REST

1. Obtenir des informations sur un déploiement avec hello [obtenir des informations sur un déploiement de modèle](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) opération.

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    Dans la réponse de hello, notez en particulier hello **provisioningState**, **correlationId**, et **erreur** éléments. Hello **correlationId** sert tootrack les événements liés, et peut être utile dans les cas des tootroubleshoot de support technique un déploiement.

  ```json
  { 
    ...
    "properties": {
      "provisioningState":"Failed",
      "correlationId":"d5062e45-6e9f-4fd3-a0a0-6b2c56b15757",
      ...
      "error":{
        "code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see http://aka.ms/arm-debug for usage details.",
        "details":[{"code":"Conflict","message":"{\r\n  \"error\": {\r\n    \"message\": \"Conflict\",\r\n    \"code\": \"Conflict\"\r\n  }\r\n}"}]
      }  
    }
  }
  ```

2. Obtenir des informations sur les opérations de déploiement par hello [liste de toutes les opérations de déploiement de modèle](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) opération. 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    réponse de Hello inclut les informations de requête et/ou de réponse en fonction de ce que vous avez spécifié dans hello **debugSetting** propriété durant le déploiement.

  ```json
  {
    ...
    "properties": 
    {
      ...
      "request":{
        "content":{
          "location":"West US",
          "properties":{
            "accountType": "Standard_LRS"
          }
        }
      },
      "response":{
        "content":{
          "error":{
            "message":"Conflict","code":"Conflict"
          }
        }
      }
    }
  }
  ```


## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’aide sur la résolution des erreurs de déploiement particulier, consultez [résoudre les erreurs courantes lors du déploiement de ressources tooAzure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).
* les journaux toolearn sur l’utilisation d’activité hello toomonitor autres types d’actions, consultez [toomanage Azure des journaux d’activité de la vue ressources](resource-group-audit.md).
* reportez-vous à votre déploiement avant son exécution, toovalidate [déployer un groupe de ressources avec le modèle Azure Resource Manager](resource-group-template-deploy.md).

