---
title: "notifications d’alerte par courrier électronique d’aaaUse échelle actions toosend et webhook. | Microsoft Docs"
description: "Consultez Comment toouse échelle actions toocall web URL ou envoyer des notifications par courrier électronique dans le moniteur de Azure. "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a>Utiliser la mise à l’échelle actions toosend par courrier électronique et webhook des notifications d’alerte dans le moniteur de Azure
Cet article explique comment paramétrer des déclencheurs pour vous permettre d’appeler des URL web spécifiques ou d’envoyer des courriers électroniques en fonction d’actions de mise à l’échelle automatique dans Azure.  

## <a name="webhooks"></a>Webhooks
Webhooks permettent de systèmes de tooother tooroute hello Azure notifications d’alerte pour les notifications de post-traitement ou personnalisées. Par exemple, routage tooservices alerte hello qui peut gérer un entrant web demande toosend SMS, journal des bogues, notifier une équipe à l’aide de la conversation ou de services de messagerie, etc. hello webhook URI doit être un point de terminaison HTTP ou HTTPS valide.

## <a name="email"></a>Email
Adresse de messagerie valide tooany peut être envoyé à par courrier électronique. Les administrateurs et coadministrateurs d’abonnement hello sur lequel la règle de hello s’exécute également soient prévenus.

## <a name="cloud-services-and-web-apps"></a>Services cloud et applications web
Vous pouvez choisir de hello portail Azure pour les Services de cloud computing et des batteries de serveurs (applications Web).

* Choisissez hello **l’échelle** métrique.

![scale by (mise à l’échelle par)](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a>Jeux de mise à l’échelle de machine virtuelle
Pour des machines virtuelles plus récentes créées avec Resource Manager (groupes identiques de machines virtuelles), vous pouvez effectuer cette configuration à l’aide de l’API REST, de modèles Resource Manager, de PowerShell et de l’interface de ligne de commande (CLI). Aucune interface de portail n’est disponible pour l’instant.
Lorsque vous utilisez l’API REST de hello ou un modèle de gestionnaire de ressources, inclure l’élément de notifications de hello avec hello options suivantes.

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| Champ | Obligatoire ? | Description |
| --- | --- | --- |
| operation |yes |la valeur doit être « Scale » |
| sendToSubscriptionAdministrator |yes |la valeur doit être « true » ou « false » |
| sendToSubscriptionCoAdministrators |yes |la valeur doit être « true » ou « false » |
| customEmails |yes |la valeur peut être null ou un tableau de chaînes d’e-mails |
| Webhooks |yes |la valeur peut être null ou un Uri valide |
| serviceUri |yes |un URI https valide |
| properties |yes |la valeur doit être vide ( {} ) ou peut contenir des paires clé-valeur |

## <a name="authentication-in-webhooks"></a>Authentification dans des webhooks
Hello webhook peut s’authentifier à l’aide de l’authentification basée sur le jeton, où vous enregistrez hello webhook URI avec un ID de jeton en tant que paramètre de requête. Par exemple, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue

## <a name="autoscale-notification-webhook-payload-schema"></a>Schéma de la charge utile du webhook de notification de mise à l’échelle automatique
Lors de la notification de mise à l’échelle hello est générée, hello métadonnées suivante sont incluses dans la charge utile du webhook hello :

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| Champ | Obligatoire ? | Description |
| --- | --- | --- |
| status |yes |état Hello qui indique qu’une action de mise à l’échelle a été générée. |
| operation |yes |Pour une augmentation des instances, l’option est « augmenter la taille des instances » ; pour une diminution des instances, l’option est « Diminuer la taille des instances » |
| context |yes |contexte d’action de mise à l’échelle de Hello |
| timestamp |yes |Horodatage lors de l’action de mise à l’échelle hello a été déclenchée. |
| id |Oui |ID du Gestionnaire de ressources du paramètre de mise à l’échelle hello |
| name |Oui |nom de Hello du paramètre de mise à l’échelle hello |
| détails |Oui |Explication de l’action hello que nécessaire du service de mise à l’échelle hello et hello modifier dans le nombre d’instances hello |
| subscriptionId |Oui |ID d’abonnement de la ressource cible hello qui est mis à l’échelle |
| resourceGroupName |Oui |Nom de groupe de ressources de la ressource cible hello qui est mis à l’échelle |
| resourceName |Oui |Nom de ressource cible hello qui est mis à l’échelle |
| resourceType |Oui |Hello trois valeurs prises en charge : « microsoft.classiccompute/domainnames/slots/roles » - rôles de Service Cloud, « microsoft.compute/virtualmachinescalesets - « machines virtuelles identiques et « Microsoft.Web/serverfarms » - application Web |
| resourceId |Oui |ID du Gestionnaire de ressources de ressource cible hello qui est mis à l’échelle |
| portalLink |Oui |Page Résumé de lien vers le portail Azure toohello de ressource cible de hello |
| oldCapacity |Oui |Hello (ancienne) nombre d’instances actuelles lors de l’échelle automatique a effectué une action de mise à l’échelle |
| newCapacity |Oui |nouveau nombre d’instances Hello que mise à l’échelle à l’échelle les ressources hello trop|
| Propriétés |Non |facultatif. Jeu de paires < clé, valeur > (par exemple, Dictionary < String, String >). champ de propriétés Hello est facultatif. Dans une interface utilisateur personnalisée ou d’un workflow d’application en fonction de logique, vous pouvez entrer des clés et valeurs qui peuvent être passés à l’aide de la charge utile de hello. Une autre manière que les propriétés personnalisées toopass sauvegarder toohello sortants webhook appel est toouse hello webhook URI elle-même (en tant que paramètres de requête) |
