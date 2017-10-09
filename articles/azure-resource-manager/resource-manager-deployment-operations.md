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
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="8b9f1-103">Afficher les opérations de déploiement avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8b9f1-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="8b9f1-104">Vous pouvez afficher les opérations hello pour un déploiement via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-104">You can view hello operations for a deployment through hello Azure portal.</span></span> <span data-ttu-id="8b9f1-105">Vous serez peut-être plus vous souhaitez afficher les opérations de hello lorsque vous avez reçu une erreur lors du déploiement pour cet article se concentre sur l’affichage des opérations qui ont échoué.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-105">You may be most interested in viewing hello operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="8b9f1-106">portail de Hello fournit une interface qui vous permet d’erreurs de hello tooeasily rechercher et déterminer les corrections éventuelles.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-106">hello portal provides an interface that enables you tooeasily find hello errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="8b9f1-107">Portail</span><span class="sxs-lookup"><span data-stu-id="8b9f1-107">Portal</span></span>
<span data-ttu-id="8b9f1-108">opérations de déploiement toosee hello, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8b9f1-108">toosee hello deployment operations, use hello following steps:</span></span>

1. <span data-ttu-id="8b9f1-109">Pour le groupe de ressources hello impliquée dans le déploiement de hello, notez l’état hello du dernier déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-109">For hello resource group involved in hello deployment, notice hello status of hello last deployment.</span></span> <span data-ttu-id="8b9f1-110">Vous pouvez sélectionner cette tooget état plus de détails.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-110">You can select this status tooget more details.</span></span>
   
    ![état du déploiement](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="8b9f1-112">Vous consultez l’historique de déploiement récente hello.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-112">You see hello recent deployment history.</span></span> <span data-ttu-id="8b9f1-113">Sélectionnez le déploiement hello qui a échoué.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-113">Select hello deployment that failed.</span></span>
   
    ![état du déploiement](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="8b9f1-115">Sélectionnez toosee de lien de hello expliquant pourquoi hello Échec du déploiement.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-115">Select hello link toosee a description of why hello deployment failed.</span></span> <span data-ttu-id="8b9f1-116">Dans l’image hello ci-dessous, un enregistrement DNS hello n’est pas unique.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-116">In hello image below, hello DNS record is not unique.</span></span>  
   
    ![afficher le déploiement ayant échoué](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="8b9f1-118">Ce message d’erreur doit être suffisante pour vous toobegin résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-118">This error message should be enough for you toobegin troubleshooting.</span></span> <span data-ttu-id="8b9f1-119">Toutefois, si vous avez besoin de plus d’informations sur les tâches ont été effectuées, vous pouvez afficher les opérations hello comme indiqué dans hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-119">However, if you need more details about which tasks were completed, you can view hello operations as shown in hello following steps.</span></span>
4. <span data-ttu-id="8b9f1-120">Vous pouvez afficher toutes les opérations de déploiement hello Bonjour **déploiement** panneau.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-120">You can view all hello deployment operations in hello **Deployment** blade.</span></span> <span data-ttu-id="8b9f1-121">Sélectionnez n’importe quel toosee opération plus de détails.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-121">Select any operation toosee more details.</span></span>
   
    ![afficher des opérations](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="8b9f1-123">Dans ce cas, vous voyez que le compte de stockage hello et réseau virtuel à haute disponibilité ont été créés.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-123">In this case, you see that hello storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="8b9f1-124">Échec de l’adresse IP publique de Hello et autres ressources n’ont pas été tentées.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-124">hello public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="8b9f1-125">Vous pouvez afficher les événements pour le déploiement de hello en sélectionnant **événements**.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-125">You can view events for hello deployment by selecting **Events**.</span></span>
   
    ![visualiser les événements](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="8b9f1-127">Voir tous les événements hello pour le déploiement de hello et de sélectionner n’importe quelle pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-127">You see all hello events for hello deployment and select any one for more details.</span></span> <span data-ttu-id="8b9f1-128">Notez que trop hello ID de corrélation.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-128">Notice too hello correlation IDs.</span></span> <span data-ttu-id="8b9f1-129">Cette valeur peut être utile lorsque vous travaillez avec le support technique tootroubleshoot un déploiement.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-129">This value can be helpful when working with technical support tootroubleshoot a deployment.</span></span>
   
    ![voir les événements](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="8b9f1-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b9f1-131">PowerShell</span></span>
1. <span data-ttu-id="8b9f1-132">tooget hello état global d’un déploiement, utilisez hello **Get-AzureRmResourceGroupDeployment** commande.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-132">tooget hello overall status of a deployment, use hello **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="8b9f1-133">Ou bien, vous pouvez filtrer les résultats de hello pour uniquement ces déploiements qui ont échoué.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-133">Or, you can filter hello results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="8b9f1-134">Chaque déploiement comprend plusieurs opérations.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="8b9f1-135">Chaque opération représente une étape dans le processus de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-135">Each operation represents a step in hello deployment process.</span></span> <span data-ttu-id="8b9f1-136">toodiscover la cause du problème avec un déploiement, vous devez généralement toosee plus d’informations sur les opérations de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-136">toodiscover what went wrong with a deployment, you usually need toosee details about hello deployment operations.</span></span> <span data-ttu-id="8b9f1-137">Vous pouvez voir État hello d’opérations hello avec **Get-AzureRmResourceGroupDeploymentOperation**.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-137">You can see hello status of hello operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="8b9f1-138">Qui retourne plusieurs opérations à chacun d’eux Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="8b9f1-138">Which returns multiple operations with each one in hello following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="8b9f1-139">tooget plus de détails sur les opérations ayant échoué, récupérer les propriétés de hello pour les opérations avec **n’a pas pu** état.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-139">tooget more details about failed operations, retrieve hello properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="8b9f1-140">Qui retourne que tous les hello opérations ayant échoué avec chacun d’eux Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="8b9f1-140">Which returns all hello failed operations with each one in hello following format:</span></span>

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

    <span data-ttu-id="8b9f1-141">Notez les %%ServiceRequestID%% hello et trackingId hello pour l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-141">Note hello serviceRequestId and hello trackingId for hello operation.</span></span> <span data-ttu-id="8b9f1-142">Hello %%ServiceRequestID%% peut être utile lorsque vous travaillez avec le support technique tootroubleshoot un déploiement.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-142">hello serviceRequestId can be helpful when working with technical support tootroubleshoot a deployment.</span></span> <span data-ttu-id="8b9f1-143">Vous utiliserez hello trackingId dans hello prochaine étape toofocus sur une opération particulière.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-143">You will use hello trackingId in hello next step toofocus on a particular operation.</span></span>
4. <span data-ttu-id="8b9f1-144">tooget hello message d’état d’une opération ayant échouée particulière, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8b9f1-144">tooget hello status message of a particular failed operation, use hello following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="8b9f1-145">Résultat :</span><span class="sxs-lookup"><span data-stu-id="8b9f1-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="8b9f1-146">Chaque opération de déploiement dans Azure inclut le contenu de la demande et de la réponse.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="8b9f1-147">contenu de la demande Hello est ce que vous avez envoyé tooAzure durant le déploiement (par exemple, créer une machine virtuelle, disque de système d’exploitation et d’autres ressources).</span><span class="sxs-lookup"><span data-stu-id="8b9f1-147">hello request content is what you sent tooAzure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="8b9f1-148">contenu de la réponse Hello est envoyé par le Azure à partir de votre demande de déploiement.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-148">hello response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="8b9f1-149">Au cours du déploiement, vous pouvez utiliser **DeploymentDebugLogLevel** toospecify habituellement qui hello requête et/ou de réponse sont conservés dans le journal de hello.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter toospecify that hello request and/or response are retained in hello log.</span></span> 

  <span data-ttu-id="8b9f1-150">Vous obtenez ces informations à partir du journal de hello et l’enregistrer localement à l’aide de hello suivant de commandes PowerShell :</span><span class="sxs-lookup"><span data-stu-id="8b9f1-150">You get that information from hello log, and save it locally by using hello following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="8b9f1-151">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="8b9f1-151">Azure CLI</span></span>

1. <span data-ttu-id="8b9f1-152">Obtenir hello état global d’un déploiement avec hello **afficher de déploiement de groupe azure** commande.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-152">Get hello overall status of a deployment with hello **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="8b9f1-153">Une des valeurs renvoyée de hello est hello **correlationId**.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-153">One of hello returned values is hello **correlationId**.</span></span> <span data-ttu-id="8b9f1-154">Cette valeur est utilisée tootrack les événements liés, et peut être utile dans les cas des tootroubleshoot de support technique un déploiement.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-154">This value is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="8b9f1-155">opérations de hello toosee pour un déploiement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="8b9f1-155">toosee hello operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="8b9f1-156">REST</span><span class="sxs-lookup"><span data-stu-id="8b9f1-156">REST</span></span>

1. <span data-ttu-id="8b9f1-157">Obtenir des informations sur un déploiement avec hello [obtenir des informations sur un déploiement de modèle](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) opération.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-157">Get information about a deployment with hello [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="8b9f1-158">Dans la réponse de hello, notez en particulier hello **provisioningState**, **correlationId**, et **erreur** éléments.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-158">In hello response, note in particular hello **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="8b9f1-159">Hello **correlationId** sert tootrack les événements liés, et peut être utile dans les cas des tootroubleshoot de support technique un déploiement.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-159">hello **correlationId** is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

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

2. <span data-ttu-id="8b9f1-160">Obtenir des informations sur les opérations de déploiement par hello [liste de toutes les opérations de déploiement de modèle](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) opération.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-160">Get information about deployment operations with hello [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="8b9f1-161">réponse de Hello inclut les informations de requête et/ou de réponse en fonction de ce que vous avez spécifié dans hello **debugSetting** propriété durant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="8b9f1-161">hello response includes request and/or response information based on what you specified in hello **debugSetting** property during deployment.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="8b9f1-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8b9f1-162">Next steps</span></span>
* <span data-ttu-id="8b9f1-163">Pour plus d’aide sur la résolution des erreurs de déploiement particulier, consultez [résoudre les erreurs courantes lors du déploiement de ressources tooAzure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="8b9f1-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="8b9f1-164">les journaux toolearn sur l’utilisation d’activité hello toomonitor autres types d’actions, consultez [toomanage Azure des journaux d’activité de la vue ressources](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="8b9f1-164">toolearn about using hello activity logs toomonitor other types of actions, see [View activity logs toomanage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="8b9f1-165">reportez-vous à votre déploiement avant son exécution, toovalidate [déployer un groupe de ressources avec le modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8b9f1-165">toovalidate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

