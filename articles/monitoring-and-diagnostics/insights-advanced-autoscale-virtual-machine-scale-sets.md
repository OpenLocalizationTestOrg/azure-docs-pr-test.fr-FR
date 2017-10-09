---
title: "aaaAdvanced mise à l’échelle à l’aide de Machines virtuelles Azure | Documents Microsoft"
description: "Utilisez Resource Manager et VM Scale Sets avec plusieurs règles et profils qui envoient un e-mail et appellent les URL webhook avec des actions de mise à l’échelle."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a>Configuration avancée de la mise à l’échelle automatique à l’aide des modèles Resource Manager pour VM Scale Sets
Vous pouvez diminuer ou augmenter la taille des instances dans VM Scale Sets en fonction de certains seuils de métriques de performances, selon une planification périodique ou à une date donnée. Vous pouvez également configurer des e-mails et des webhooks de notification pour les actions de mise à l’échelle. Cette procédure pas à pas présente un exemple de configuration de ces objets à l’aide d’un modèle Resource Manager sur un groupe de machines virtuelles identiques (VM Scale Set).

> [!NOTE]
> Pendant cette procédure pas à pas décrit les étapes de hello pour les jeux de mise à l’échelle de machine virtuelle, hello mêmes informations s’applique tooautoscaling [Services de cloud computing](https://azure.microsoft.com/services/cloud-services/), et [du Service d’applications - applications Web](https://azure.microsoft.com/services/app-service/web/).
> Pour une échelle simple entrée/sortie paramètre sur un ensemble d’échelle de machine virtuelle sur une mesure de performance simples tels que le processeur, reportez-vous à toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) et [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents
>
>

## <a name="walkthrough"></a>Procédure pas à pas
Dans cette procédure pas à pas, nous utilisons [Explorateur de ressources Azure](https://resources.azure.com/) tooconfigure et mise à jour le paramètre de mise à l’échelle hello pour un ensemble d’échelle. L’Explorateur de ressources Azure est un toomanage facilement les ressources Azure via le Gestionnaire de ressources des modèles. Si vous ne le nouvel outil de l’Explorateur de ressources tooAzure, lisez [cette introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).

1. Déployez un nouveau groupe de machines virtuelles identiques avec un paramètre de mise à l’échelle automatique de base. Cet article utilise une hello de hello galerie de démarrage rapide Azure, une fenêtre a été mise à l’échelle est définie avec un modèle de base de mise à l’échelle. Échelle de Linux définit travail hello identique.
2. Après la création d’un ensemble d’échelle hello, accédez toohello échelle jeu de ressources à partir de l’Explorateur de ressources Azure. Vous consultez suivant hello sous le nœud de Microsoft.Insights.

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    l’exécution du modèle Hello a créé un paramètre de mise à l’échelle par défaut avec le nom de hello **'autoscalewad'**. Sur le côté droit de hello, vous pouvez afficher la définition complète de hello de ce paramètre de mise à l’échelle. Dans ce cas, le paramètre de mise à l’échelle par défaut hello est fourni avec une règle de montée en puissance parallèle et de mise à l’échelle de % en fonction du processeur.  

3. Vous pouvez maintenant ajouter plus de profils et de règles basées sur la planification de hello ou des exigences spécifiques. Nous allons créer un paramètre de mise à l’échelle automatique avec trois profils. toounderstand profils et les règles de mise à l’échelle, passez en revue [mise à l’échelle les meilleures pratiques](insights-autoscale-best-practices.md).  

    | Profils et règles | Description |
    |--- | --- |
    | **Profil** |**En fonction des métriques/performances** |
    | Règle |Nombre de messages de la file d’attente Service Bus > x |
    | Règle |Nombre de messages de la file d’attente Service Bus < y |
    | Règle |%UC > n |
    | Règle |% UC, < p |
    | **Profil** |**Heures dans la matinée, en semaine (aucune règle)** |
    | **Profil** |**Jour de lancement de produit (aucune règle)** |

4. Voici un scénario de mise à l’échelle hypothétique que nous utiliserons pour cette procédure pas à pas.

    * **Charge en fonction** -j’aimerais tooscale ou selon la charge de hello sur mon application hébergée sur mon set.* de mise à l’échelle
    * **Taille de file d’attente de message** -utiliser une file d’attente du Bus de Service pour l’application de toomy de messages entrants hello. Utilisez de hello file d’attente messages et % de l’UC et de la configurer un tootrigger de profil par défaut une action de mise à l’échelle de nombre de messages ou de l’UC accès hello threshold.*
    * **Heure de la semaine et jour** -je voudrais un profil « heure du jour de hello' basé périodique hebdomadaire appelé « Jours ouvrables matin ». Selon les données d’historique, savoir qu’il est mieux toohave certain nombre d’ordinateurs virtuels instances toohandle le chargement de mon application au cours de cette time.*
    * **Dates particulières** : j’ai ajouté un profil « Jour de lancement de produit ». Planifier l’avance des dates spécifiques afin de mon application est la charge de hello toohandle prêt en raison des annonces marketing et lorsqu’un nouveau produit mis en place hello application.*
    * *profils de deux derniers Hello peuvent également avoir des autres règles en fonction métriques de performances au sein de celles-ci. Dans ce cas, j’ai ne décidé pas les toohave un et à la place toorely sur les mesures de performance hello par défaut en fonction de règles. Les règles sont facultatives pour hello périodique et date en fonction des profils.*

    Définition des priorités des profils de hello et des règles du moteur de mise à l’échelle sont également capturées dans hello [échelle meilleures pratiques](insights-autoscale-best-practices.md) l’article.
    Pour obtenir une liste des métriques communément utilisées pour la mise à l’échelle, consultez [Métriques courantes pour la mise à l’échelle automatique d’Azure Insights](insights-autoscale-common-metrics.md)

5. Vérifiez que vous êtes sur hello **en lecture/écriture** mode dans l’Explorateur de ressources

    ![Autoscalewad, paramètre de mise à l’échelle automatique par défaut](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. Cliquez sur Modifier. **Remplacez** élément les profils « hello » dans le paramètre de mise à l’échelle par hello configuration suivante :

    ![profils](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    Pour les champs pris en charge et leurs valeurs, consultez la [documentation API REST de la mise à l’échelle automatique](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx). Le paramètre de mise à l’échelle contient désormais hello trois profils expliqués précédemment.

7. Pour finir, observez hello échelle **notification** section. Les notifications de mise à l’échelle permettent toodo trois choses lors d’une montée en puissance, ou dans l’action est déclenchée avec succès.
   - Avertir hello admin et les coadministrateurs de votre abonnement
   - Envoyer un e-mail à un ensemble d’utilisateurs
   - Déclencher un appel webhook. Lorsqu’il est déclenché, ce webhook envoie des métadonnées sur la condition d’échelle hello et ensemble d’échelle de hello de ressource. toolearn en savoir plus sur la charge utile de hello de webhook de l’échelle automatique, consultez [Webhook de configurer et de Notifications par courrier électronique pour la mise à l’échelle](insights-autoscale-to-webhook-email.md).

   Ajouter hello après le remplacement de paramètre de mise à l’échelle toohello votre **notification** élément dont la valeur est null

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
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

   Accès **Put** bouton dans le paramètre de mise à l’échelle de l’Explorateur de ressources tooupdate hello.

Vous avez de mises à jour un paramètre sur un tooinclude de jeu de mise à l’échelle de machine virtuelle plusieurs profils de mise à l’échelle d’échelle automatique et des notifications de mise à l’échelle.

## <a name="next-steps"></a>Étapes suivantes
Utilisez ces informations supplémentaires sur l’échelle automatique de toolearn de liens.

[Dépanner la mise à l’échelle automatique avec des jeux de mise à l’échelle de machine virtuelle](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[Métriques courantes pour la mise à l’échelle automatique d’Azure Insights](insights-autoscale-common-metrics.md)

[Meilleures pratiques pour la mise à l’échelle automatique d’Azure Insights](insights-autoscale-best-practices.md)

[Gérer les paramètres de mise à l’échelle automatique à l’aide de PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[Gérer les paramètres de mise à l’échelle automatique à l’aide de la CLI](insights-cli-samples.md#autoscale)

[Utilisation d’actions de mise à l’échelle automatique pour envoyer des notifications d’alerte webhook et par courrier électronique dans Azure Insights](insights-autoscale-to-webhook-email.md)
