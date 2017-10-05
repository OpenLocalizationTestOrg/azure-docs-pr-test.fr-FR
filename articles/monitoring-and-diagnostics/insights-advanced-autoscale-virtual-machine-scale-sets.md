---
title: "Mise à l’échelle automatique avancée à l’aide de Machines virtuelles Azure | Microsoft Docs"
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
ms.openlocfilehash: 80955535c8d863cd3d8d1b77e2ab8bc016b6d9f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="2be2b-103">Configuration avancée de la mise à l’échelle automatique à l’aide des modèles Resource Manager pour VM Scale Sets</span><span class="sxs-lookup"><span data-stu-id="2be2b-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="2be2b-104">Vous pouvez diminuer ou augmenter la taille des instances dans VM Scale Sets en fonction de certains seuils de métriques de performances, selon une planification périodique ou à une date donnée.</span><span class="sxs-lookup"><span data-stu-id="2be2b-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="2be2b-105">Vous pouvez également configurer des e-mails et des webhooks de notification pour les actions de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="2be2b-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="2be2b-106">Cette procédure pas à pas présente un exemple de configuration de ces objets à l’aide d’un modèle Resource Manager sur un groupe de machines virtuelles identiques (VM Scale Set).</span><span class="sxs-lookup"><span data-stu-id="2be2b-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="2be2b-107">Bien que cette procédure concerne plus spécifiquement jeux de mise à l’échelle de machines virtuelles, les mêmes informations s’appliquent pour la mise à l’échelle automatique des [services cloud](https://azure.microsoft.com/services/cloud-services/) et [d’App Service - Applications web](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="2be2b-107">While this walkthrough explains the steps for VM Scale Sets, the same information applies to autoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="2be2b-108">Pour utiliser un simple paramètre de mise à l’échelle (avec diminution ou augmentation de la taille des instances) sur un groupe de machines virtuelles identiques à partir d’une simple métrique de performances (par exemple, ressources processeur), reportez-vous à la documentation [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) et [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md)</span><span class="sxs-lookup"><span data-stu-id="2be2b-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer to the [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="2be2b-109">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="2be2b-109">Walkthrough</span></span>
<span data-ttu-id="2be2b-110">Dans cette procédure pas à pas, nous utilisons [Azure Resource Explorer](https://resources.azure.com/) pour configurer et mettre à jour le paramètre de mise à l’échelle automatique pour un groupe de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="2be2b-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) to configure and update the autoscale setting for a scale set.</span></span> <span data-ttu-id="2be2b-111">L’Explorateur de ressources Azure est un moyen simple de gérer des ressources Azure via des modèles Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2be2b-111">Azure Resource Explorer is an easy way to manage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="2be2b-112">Si vous débutez avec l’Explorateur de ressources Azure, lisez [cette introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="2be2b-112">If you are new to Azure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="2be2b-113">Déployez un nouveau groupe de machines virtuelles identiques avec un paramètre de mise à l’échelle automatique de base.</span><span class="sxs-lookup"><span data-stu-id="2be2b-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="2be2b-114">Cet article utilise celui de la galerie de démarrage rapide Azure, qui comporte un groupe de machines virtuelles identiques Windows avec un modèle de mise à l’échelle automatique de base.</span><span class="sxs-lookup"><span data-stu-id="2be2b-114">This article uses the one from the Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="2be2b-115">Les groupes de machines virtuelles identiques Linux fonctionnent de la même façon.</span><span class="sxs-lookup"><span data-stu-id="2be2b-115">Linux scale sets work the same way.</span></span>
2. <span data-ttu-id="2be2b-116">Une fois le groupe créé, accédez à la ressource du groupe à partir de l’Explorateur de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="2be2b-116">After the scale set is created, navigate to the scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="2be2b-117">Le code suivant apparaît sous le nœud Microsoft.Insights.</span><span class="sxs-lookup"><span data-stu-id="2be2b-117">You see the following under Microsoft.Insights node.</span></span>

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="2be2b-119">L’exécution du modèle a créé un paramètre de mise à l’échelle automatique par défaut portant le nom **'autoscalewad'**.</span><span class="sxs-lookup"><span data-stu-id="2be2b-119">The template execution has created a default autoscale setting with the name **'autoscalewad'**.</span></span> <span data-ttu-id="2be2b-120">Dans la partie droite, vous pouvez afficher la définition complète de ce paramètre de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="2be2b-120">On the right-hand side, you can view the full definition of this autoscale setting.</span></span> <span data-ttu-id="2be2b-121">Dans ce cas, le paramètre de mise à l’échelle par défaut est associé à une règle de diminution et d’augmentation de la taille des instances basé sur le % de processeur.</span><span class="sxs-lookup"><span data-stu-id="2be2b-121">In this case, the default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="2be2b-122">Vous pouvez maintenant ajouter d’autres profils et règles à partir d’un calendrier ou d’exigences spécifiques.</span><span class="sxs-lookup"><span data-stu-id="2be2b-122">You can now add more profiles and rules based on the schedule or specific requirements.</span></span> <span data-ttu-id="2be2b-123">Nous allons créer un paramètre de mise à l’échelle automatique avec trois profils.</span><span class="sxs-lookup"><span data-stu-id="2be2b-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="2be2b-124">Pour comprendre les profils et les règles de mise à l’échelle automatique, consultez [Meilleures pratiques pour la mise à l’échelle automatique d’Azure Insights](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="2be2b-124">To understand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="2be2b-125">Profils et règles</span><span class="sxs-lookup"><span data-stu-id="2be2b-125">Profiles & Rules</span></span> | <span data-ttu-id="2be2b-126">Description</span><span class="sxs-lookup"><span data-stu-id="2be2b-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="2be2b-127">**Profil**</span><span class="sxs-lookup"><span data-stu-id="2be2b-127">**Profile**</span></span> |<span data-ttu-id="2be2b-128">**En fonction des métriques/performances**</span><span class="sxs-lookup"><span data-stu-id="2be2b-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="2be2b-129">Règle</span><span class="sxs-lookup"><span data-stu-id="2be2b-129">Rule</span></span> |<span data-ttu-id="2be2b-130">Nombre de messages de la file d’attente Service Bus > x</span><span class="sxs-lookup"><span data-stu-id="2be2b-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="2be2b-131">Règle</span><span class="sxs-lookup"><span data-stu-id="2be2b-131">Rule</span></span> |<span data-ttu-id="2be2b-132">Nombre de messages de la file d’attente Service Bus < y</span><span class="sxs-lookup"><span data-stu-id="2be2b-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="2be2b-133">Règle</span><span class="sxs-lookup"><span data-stu-id="2be2b-133">Rule</span></span> |<span data-ttu-id="2be2b-134">%UC > n</span><span class="sxs-lookup"><span data-stu-id="2be2b-134">CPU% > n</span></span> |
    | <span data-ttu-id="2be2b-135">Règle</span><span class="sxs-lookup"><span data-stu-id="2be2b-135">Rule</span></span> |<span data-ttu-id="2be2b-136">% UC, < p</span><span class="sxs-lookup"><span data-stu-id="2be2b-136">CPU% < p</span></span> |
    | <span data-ttu-id="2be2b-137">**Profil**</span><span class="sxs-lookup"><span data-stu-id="2be2b-137">**Profile**</span></span> |<span data-ttu-id="2be2b-138">**Heures dans la matinée, en semaine (aucune règle)**</span><span class="sxs-lookup"><span data-stu-id="2be2b-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="2be2b-139">**Profil**</span><span class="sxs-lookup"><span data-stu-id="2be2b-139">**Profile**</span></span> |<span data-ttu-id="2be2b-140">**Jour de lancement de produit (aucune règle)**</span><span class="sxs-lookup"><span data-stu-id="2be2b-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="2be2b-141">Voici un scénario de mise à l’échelle hypothétique que nous utiliserons pour cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="2be2b-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="2be2b-142">**Selon la charge** : je souhaite diminuer ou augmenter la taille des instances en fonction de la charge de mon application hébergée sur mon groupe de machines virtuelles identiques.*</span><span class="sxs-lookup"><span data-stu-id="2be2b-142">**Load based** - I'd like to scale out or in based on the load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="2be2b-143">**Taille de la file d’attente** : j’utilise une file d’attente Service Bus pour les messages entrants dans mon application.</span><span class="sxs-lookup"><span data-stu-id="2be2b-143">**Message Queue size** - I use a Service Bus Queue for the incoming messages to my application.</span></span> <span data-ttu-id="2be2b-144">J’utilise le nombre de messages de la file d’attente et le % processeur, et je configure un profil par défaut pour déclencher une action de mise à l’échelle si le nombre de messages ou le % processeur atteint le seuil défini.*</span><span class="sxs-lookup"><span data-stu-id="2be2b-144">I use the queue's message count and CPU% and configure a default profile to trigger a scale action if either of message count or CPU hits the threshold.*</span></span>
    * <span data-ttu-id="2be2b-145">**Heure de la journée** : je souhaite définir un profil hebdomadaire basé sur « l’heure de la journée », appelé « Heures dans la matinée, en semaine ».</span><span class="sxs-lookup"><span data-stu-id="2be2b-145">**Time of week and day** - I want a weekly recurring 'time of the day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="2be2b-146">Au vu des données historiques, je sais qu’il est préférable d’avoir un certain nombre d’instances de machine virtuelle pour gérer la charge de mon application pendant cette période.*</span><span class="sxs-lookup"><span data-stu-id="2be2b-146">Based on historical data, I know it is better to have certain number of VM instances to handle my application's load during this time.*</span></span>
    * <span data-ttu-id="2be2b-147">**Dates particulières** : j’ai ajouté un profil « Jour de lancement de produit ».</span><span class="sxs-lookup"><span data-stu-id="2be2b-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="2be2b-148">Je planifie à l’avance des dates spécifiques afin que mon application soit prête à gérer la charge, en fonction des annonces marketing et des dates d’introduction de nouveaux produits dans l’application.*</span><span class="sxs-lookup"><span data-stu-id="2be2b-148">I plan ahead for specific dates so my application is ready to handle the load due marketing announcements and when we put a new product in the application.*</span></span>
    * <span data-ttu-id="2be2b-149">*Les deux derniers profils peuvent également contenir d’autres règles basées sur les métriques de performances. Dans mon cas, j’ai décidé de ne pas en utiliser et de me concentrer uniquement sur les règles basées sur les métriques de performances par défaut. Les règles sont facultatives pour les profils récurrents et les profils basés sur la date.*</span><span class="sxs-lookup"><span data-stu-id="2be2b-149">*The last two profiles can also have other performance metric based rules within them. In this case, I decided not to have one and instead to rely on the default performance metric based rules. Rules are optional for the recurring and date-based profiles.*</span></span>

    <span data-ttu-id="2be2b-150">La définition des priorités des profils et des règles du moteur de mise à l’échelle automatique est également décrite dans l’article [Meilleures pratiques pour la mise à l’échelle automatique d’Azure Insights](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="2be2b-150">Autoscale engine's prioritization of the profiles and rules is also captured in the [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="2be2b-151">Pour obtenir une liste des métriques communément utilisées pour la mise à l’échelle, consultez [Métriques courantes pour la mise à l’échelle automatique d’Azure Insights](insights-autoscale-common-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="2be2b-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="2be2b-152">Assurez-vous que vous utilisez l’Explorateur de ressources en mode **lecture/écriture**</span><span class="sxs-lookup"><span data-stu-id="2be2b-152">Make sure you are on the **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, paramètre de mise à l’échelle automatique par défaut](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="2be2b-154">Cliquez sur Modifier.</span><span class="sxs-lookup"><span data-stu-id="2be2b-154">Click Edit.</span></span> <span data-ttu-id="2be2b-155">**Remplacez** l’élément « profiles » dans le paramètre de mise à l’échelle automatique par la configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="2be2b-155">**Replace** the 'profiles' element in autoscale setting with the following configuration:</span></span>

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
    <span data-ttu-id="2be2b-157">Pour les champs pris en charge et leurs valeurs, consultez la [documentation API REST de la mise à l’échelle automatique](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="2be2b-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="2be2b-158">Votre paramètre de mise à l’échelle automatique contient à présent les trois profils expliqués précédemment.</span><span class="sxs-lookup"><span data-stu-id="2be2b-158">Now your autoscale setting contains the three profiles explained previously.</span></span>

7. <span data-ttu-id="2be2b-159">Examinons pour finir la section **notification** de la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="2be2b-159">Finally, look at the Autoscale **notification** section.</span></span> <span data-ttu-id="2be2b-160">Les notifications de mise à l’échelle automatique permettent de faire trois choses au moment du déclenchement d’une action de diminution ou d’augmentation de la taille des instances.</span><span class="sxs-lookup"><span data-stu-id="2be2b-160">Autoscale notifications allow you to do three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="2be2b-161">Avertir l’administrateur et les co-administrateurs de votre abonnement</span><span class="sxs-lookup"><span data-stu-id="2be2b-161">Notify the admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="2be2b-162">Envoyer un e-mail à un ensemble d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="2be2b-162">Email a set of users</span></span>
   - <span data-ttu-id="2be2b-163">Déclencher un appel webhook.</span><span class="sxs-lookup"><span data-stu-id="2be2b-163">Trigger a webhook call.</span></span> <span data-ttu-id="2be2b-164">Quand il est déclenché, ce webhook envoie les métadonnées relatives à la condition de mise à l’échelle automatique et à la ressource du groupe de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="2be2b-164">When fired, this webhook sends metadata about the autoscaling condition and the scale set resource.</span></span> <span data-ttu-id="2be2b-165">Pour plus d’informations sur la charge utile du webhook de mise à l’échelle automatique, consultez la page [Utilisation d’actions de mise à l’échelle automatique pour envoyer des notifications d’alerte webhook et par courrier électronique dans Azure Insights](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="2be2b-165">To learn more about the payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="2be2b-166">Ajoutez le code suivant au paramètre de mise à l’échelle automatique en remplaçant votre élément **notification** dont la valeur est null</span><span class="sxs-lookup"><span data-stu-id="2be2b-166">Add the following to the Autoscale setting replacing your **notification** element whose value is null</span></span>

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

   <span data-ttu-id="2be2b-167">Cliquez sur le bouton **Put** dans l’Explorateur de ressources pour mettre à jour le paramètre de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="2be2b-167">Hit **Put** button in Resource Explorer to update the autoscale setting.</span></span>

<span data-ttu-id="2be2b-168">Vous avez mis à jour un paramètre de mise à l’échelle automatique sur un groupe de machines virtuelles identiques pour inclure plusieurs profils de mise à l’échelle ainsi que des notifications de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="2be2b-168">You have updated an autoscale setting on a VM Scale set to include multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2be2b-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2be2b-169">Next Steps</span></span>
<span data-ttu-id="2be2b-170">Suivez ces liens pour en savoir plus sur la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="2be2b-170">Use these links to learn more about autoscaling.</span></span>

[<span data-ttu-id="2be2b-171">Dépanner la mise à l’échelle automatique avec des jeux de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="2be2b-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="2be2b-172">Métriques courantes pour la mise à l’échelle automatique d’Azure Insights</span><span class="sxs-lookup"><span data-stu-id="2be2b-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="2be2b-173">Meilleures pratiques pour la mise à l’échelle automatique d’Azure Insights</span><span class="sxs-lookup"><span data-stu-id="2be2b-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="2be2b-174">Gérer les paramètres de mise à l’échelle automatique à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="2be2b-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="2be2b-175">Gérer les paramètres de mise à l’échelle automatique à l’aide de la CLI</span><span class="sxs-lookup"><span data-stu-id="2be2b-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="2be2b-176">Utilisation d’actions de mise à l’échelle automatique pour envoyer des notifications d’alerte webhook et par courrier électronique dans Azure Insights</span><span class="sxs-lookup"><span data-stu-id="2be2b-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
