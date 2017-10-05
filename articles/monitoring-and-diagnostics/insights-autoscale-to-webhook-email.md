---
title: "Utilisation d’actions de mise à l’échelle automatique pour envoyer des notifications d’alerte webhook et par courrier électronique. | Microsoft Docs"
description: "Découvrez comment utiliser des actions de mise à l’échelle automatique pour appeler des URL web ou envoyer des notifications par courrier électronique dans Azure Monitor. "
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
ms.openlocfilehash: 16caf14028494800e9259f0296c292b606d0210a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-autoscale-actions-to-send-email-and-webhook-alert-notifications-in-azure-monitor"></a>Utilisation d’actions de mise à l’échelle automatique pour envoyer des notifications d’alerte webhook et par courrier électronique dans Azure Moonitor
Cet article explique comment paramétrer des déclencheurs pour vous permettre d’appeler des URL web spécifiques ou d’envoyer des courriers électroniques en fonction d’actions de mise à l’échelle automatique dans Azure.  

## <a name="webhooks"></a>Webhooks
Les webhooks vous permettent d’acheminer les notifications d’alerte Azure vers d’autres systèmes afin qu’elles soient post-traitées ou personnalisées. À titre d’exemple, citons l’acheminement de l’alerte vers des services qui peuvent gérer une demande web entrante pour envoyer des SMS, consigner des bogues, informer une équipe par le biais de services de conversation ou de messagerie, etc. L’URI du webhook doit être un point de terminaison HTTP ou HTTPS valide.

## <a name="email"></a>Email
Un courrier électronique peut être envoyé à n’importe quelle adresse électronique valide. Les administrateurs et les coadministrateurs de l’abonnement dans lequel la règle est exécutée seront également avertis.

## <a name="cloud-services-and-web-apps"></a>Services cloud et applications web
Vous pouvez l’activer depuis le portail Azure pour les services cloud et les batteries de serveurs (applications web).

* Choisissez la métrique **scale by (mise à l’échelle par)** .

![scale by (mise à l’échelle par)](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a>Jeux de mise à l’échelle de machine virtuelle
Pour des machines virtuelles plus récentes créées avec Resource Manager (groupes identiques de machines virtuelles), vous pouvez effectuer cette configuration à l’aide de l’API REST, de modèles Resource Manager, de PowerShell et de l’interface de ligne de commande (CLI). Aucune interface de portail n’est disponible pour l’instant.
Lorsque vous utilisez l’API REST ou le modèle Resource Manager, incluez l’élément de notifications avec les options suivantes.

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
Le webhook peut s’authentifier en utilisant l’authentification par jeton, où vous enregistrez l’URI du webhook avec un ID de jeton comme paramètre de requête. Par exemple, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue

## <a name="autoscale-notification-webhook-payload-schema"></a>Schéma de la charge utile du webhook de notification de mise à l’échelle automatique
Lorsque la notification de mise à l’échelle automatique est générée, les métadonnées suivantes sont incluses dans la charge utile du webhook :

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' to capacity '2'",
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
| status |yes |L’état qui indique qu’une action de mise à l’échelle automatique a été générée. |
| operation |yes |Pour une augmentation des instances, l’option est « augmenter la taille des instances » ; pour une diminution des instances, l’option est « Diminuer la taille des instances » |
| context |yes |Le contexte de l’action de mise à l’échelle automatique |
| timestamp |yes |Horodatage du déclenchement de l’action de mise à l’échelle automatique. |
| id |yes |ID Resource Manager du paramètre de mise à l’échelle automatique |
| name |yes |Le nom du paramètre de mise à l’échelle automatique |
| détails |yes |Explication de l’action exécutée par le service de mise à l’échelle automatique et de la modification du nombre d’instances |
| subscriptionId |yes |ID d’abonnement de la ressource cible mise à l’échelle |
| nom_groupe_ressources |yes |Nom de groupe de ressources de la ressource cible mise à l’échelle |
| resourceName |yes |Nom de la ressource cible mise à l’échelle |
| resourceType |Oui |Trois valeurs sont prises en charge : « microsoft.classiccompute/domainnames/slots/roles » - Rôles de service cloud, « microsoft.compute/virtualmachinescalesets » - Jeux de mise à l’échelle de machine virtuelle et « Microsoft.Web/serverfarms » - Application Web |
| resourceId |yes |ID Resource Manager de la ressource cible mise à l’échelle |
| portalLink |yes |Lien du portail Azure vers la page de résumé de la ressource cible |
| oldCapacity |yes |Nombre d’instances (anciennes) actuel lors de l’exécution d’une action de mise à l’échelle par la mise à l’échelle automatique |
| newCapacity |yes |Le nouveau nombre d’instances auquel la mise à l’échelle automatique a mis la ressource à l’échelle |
| properties |Non |facultatif. Jeu de paires < clé, valeur > (par exemple, Dictionary < String, String >). Le champ properties est facultatif. Dans un flux de travail basé sur une application logique ou une interface utilisateur personnalisée, vous pouvez entrer des clés et des valeurs transmissibles par le biais de la charge utile. Une autre manière de transmettre des propriétés personnalisées au webhook sortant consiste à utiliser l’URI du webhook (sous la forme de paramètres de requête). |
