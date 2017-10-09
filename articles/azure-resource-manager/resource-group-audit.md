---
title: "aaaView activités Windows Azure consigne les ressources toomonitor | Documents Microsoft"
description: "Utilisez hello activité enregistre les erreurs et les actions de l’utilisateur tooreview. Affiche le portail Azure, PowerShell, l’interface CLI Azure et REST."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a>Afficher l’activité enregistre les actions de tooaudit sur les ressources
Les journaux d’activité vous permettent de déterminer :

* les opérations effectuées sur les ressources hello dans votre abonnement
* qui a lancé une opération hello (bien que les opérations générées par un service principal ne retournent pas d’un utilisateur en tant que l’appelant de hello)
* Lorsque l’opération de hello s’est produite
* état Hello d’opération de hello
* les valeurs Hello d’autres propriétés qui peuvent vous aider à effectuer des recherches sur les opération hello

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

Vous pouvez récupérer des informations à partir des journaux d’activité hello via le portail hello, PowerShell, CLI d’Azure, API REST de Insights, ou [Insights .NET bibliothèque](https://www.nuget.org/packages/Microsoft.Azure.Insights/).

## <a name="portal"></a>Portail
1. journaux d’activité hello tooview via le portail de hello, sélectionnez **analyse**.
   
    ![sélectionner les journaux d’activité](./media/resource-group-audit/select-monitor.png)

   Ou, tooautomatically filtrer le journal d’activité hello pour une ressource particulière ou d’un groupe de ressources, sélectionnez **le journal d’activité** à partir de ce panneau des ressources. Notez que ce journal d’activité hello est filtré automatiquement par la ressource de hello sélectionné.
   
    ![filtrer par ressource](./media/resource-group-audit/filtered-by-resource.png)
2. Bonjour **le journal d’activité** panneau, vous voyez un résumé des dernières opérations.
   
    ![afficher des actions](./media/resource-group-audit/audit-summary.png)
3. nombre de hello toorestrict d’opérations affichée, sélectionnez différentes conditions. Par exemple, hello image suivante montre hello **Timespan** et **événement déclenché par** champs modifiés tooview hello mesures par un utilisateur particulier ou d’une application pour hello du mois passé. Sélectionnez **appliquer** tooview les résultats de hello de votre requête.
   
    ![définir des options de filtre](./media/resource-group-audit/set-filter.png)

4. Si vous avez besoin de requête de hello toorun plus tard, sélectionnez **enregistrer** et donnez un nom à des requêtes de hello.
   
    ![enregistrer la requête](./media/resource-group-audit/save-query.png)
5. tooquickly exécuter une requête, vous pouvez sélectionner une requêtes de hello intégrées, telles que de déploiement a échoué.

    ![sélectionner la requête](./media/resource-group-audit/select-quick-query.png)

   requête Hello définit automatiquement les valeurs de filtre hello requis.

    ![afficher les erreurs de déploiement](./media/resource-group-audit/view-failed-deployment.png)   

6. Sélectionnez une des hello operations toosee un résumé des événements de hello.

    ![afficher l’opération](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a>PowerShell
1. les entrées de journal tooretrieve, exécutez hello **Get-AzureRmLog** commande. Vous fournissez des paramètres supplémentaires toofilter hello liste d’entrées. Si vous ne spécifiez pas une heure de début et de fin, les entrées pour hello dernière heure sont retournées. Par exemple, les opérations de hello tooretrieve pour un groupe de ressources au cours de la dernière heure de hello exécutent :

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    Bonjour à l’exemple suivant montre comment l’activité de hello toouse du journal tooresearch les opérations effectuées pendant une durée spécifiée. Hello les dates de début et de fin sont spécifiées dans un format de date.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    Ou bien, vous pouvez utiliser les fonctions toospecify hello date plage de dates, par exemple hello 14 derniers jours.
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. En fonction de l’heure de début hello que vous spécifiez, les commandes précédentes hello peuvent retourner une longue liste des opérations de groupe de ressources hello. Vous pouvez filtrer les résultats de hello pour ce que vous recherchez en fournissant des critères de recherche. Par exemple, si vous essayez de tooresearch comment une application web a été arrêtée, vous pouvez exécuter hello de commande suivante :

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    Dans cet exemple, elle montre qu’une action d’arrêt a été effectuée par someone@contoso.com. 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. Vous pouvez rechercher des actions de hello effectuées par un utilisateur particulier, même pour un groupe de ressources qui n’existe plus.

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. Vous pouvez filtrer les résultats sur les opérations ayant échoué.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. Vous concentrer sur une erreur en examinant le message d’état hello pour cette entrée.
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    Résultat :
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a>Interface de ligne de commande Azure
* les entrées de journal tooretrieve, que vous exécutez hello **groupe azure journal afficher** commande.

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a>API REST
opérations de REST Hello pour travailler avec le journal d’activité hello font partie de hello [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx). les événements de journal d’activité tooretrieve, consultez [liste des événements de gestion hello dans un abonnement](https://msdn.microsoft.com/library/azure/dn931934.aspx).

## <a name="next-steps"></a>Étapes suivantes
* Journaux d’activité Azure sont utilisables avec Power BI toogain supérieur perspectives détaillées sur les actions hello dans votre abonnement. Consultez le billet de blog sur [l’affichage et l’analyse des journaux d’activité Azure dans Power BI](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).
* toolearn sur la définition des stratégies de sécurité, consultez [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).
* toolearn sur les commandes hello pour l’affichage des opérations de déploiement, consultez [afficher les opérations de déploiement](resource-manager-deployment-operations.md).
* toolearn tooprevent des suppressions sur une ressource pour tous les utilisateurs, voir [verrouiller les ressources avec Azure Resource Manager](resource-group-lock-resources.md).

