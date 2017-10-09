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
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="8f8a8-103">Configuration avancée de la mise à l’échelle automatique à l’aide des modèles Resource Manager pour VM Scale Sets</span><span class="sxs-lookup"><span data-stu-id="8f8a8-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="8f8a8-104">Vous pouvez diminuer ou augmenter la taille des instances dans VM Scale Sets en fonction de certains seuils de métriques de performances, selon une planification périodique ou à une date donnée.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="8f8a8-105">Vous pouvez également configurer des e-mails et des webhooks de notification pour les actions de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="8f8a8-106">Cette procédure pas à pas présente un exemple de configuration de ces objets à l’aide d’un modèle Resource Manager sur un groupe de machines virtuelles identiques (VM Scale Set).</span><span class="sxs-lookup"><span data-stu-id="8f8a8-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="8f8a8-107">Pendant cette procédure pas à pas décrit les étapes de hello pour les jeux de mise à l’échelle de machine virtuelle, hello mêmes informations s’applique tooautoscaling [Services de cloud computing](https://azure.microsoft.com/services/cloud-services/), et [du Service d’applications - applications Web](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="8f8a8-107">While this walkthrough explains hello steps for VM Scale Sets, hello same information applies tooautoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="8f8a8-108">Pour une échelle simple entrée/sortie paramètre sur un ensemble d’échelle de machine virtuelle sur une mesure de performance simples tels que le processeur, reportez-vous à toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) et [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span><span class="sxs-lookup"><span data-stu-id="8f8a8-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="8f8a8-109">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="8f8a8-109">Walkthrough</span></span>
<span data-ttu-id="8f8a8-110">Dans cette procédure pas à pas, nous utilisons [Explorateur de ressources Azure](https://resources.azure.com/) tooconfigure et mise à jour le paramètre de mise à l’échelle hello pour un ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) tooconfigure and update hello autoscale setting for a scale set.</span></span> <span data-ttu-id="8f8a8-111">L’Explorateur de ressources Azure est un toomanage facilement les ressources Azure via le Gestionnaire de ressources des modèles.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-111">Azure Resource Explorer is an easy way toomanage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="8f8a8-112">Si vous ne le nouvel outil de l’Explorateur de ressources tooAzure, lisez [cette introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="8f8a8-112">If you are new tooAzure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="8f8a8-113">Déployez un nouveau groupe de machines virtuelles identiques avec un paramètre de mise à l’échelle automatique de base.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="8f8a8-114">Cet article utilise une hello de hello galerie de démarrage rapide Azure, une fenêtre a été mise à l’échelle est définie avec un modèle de base de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-114">This article uses hello one from hello Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="8f8a8-115">Échelle de Linux définit travail hello identique.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-115">Linux scale sets work hello same way.</span></span>
2. <span data-ttu-id="8f8a8-116">Après la création d’un ensemble d’échelle hello, accédez toohello échelle jeu de ressources à partir de l’Explorateur de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-116">After hello scale set is created, navigate toohello scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="8f8a8-117">Vous consultez suivant hello sous le nœud de Microsoft.Insights.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-117">You see hello following under Microsoft.Insights node.</span></span>

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="8f8a8-119">l’exécution du modèle Hello a créé un paramètre de mise à l’échelle par défaut avec le nom de hello **'autoscalewad'**.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-119">hello template execution has created a default autoscale setting with hello name **'autoscalewad'**.</span></span> <span data-ttu-id="8f8a8-120">Sur le côté droit de hello, vous pouvez afficher la définition complète de hello de ce paramètre de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-120">On hello right-hand side, you can view hello full definition of this autoscale setting.</span></span> <span data-ttu-id="8f8a8-121">Dans ce cas, le paramètre de mise à l’échelle par défaut hello est fourni avec une règle de montée en puissance parallèle et de mise à l’échelle de % en fonction du processeur.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-121">In this case, hello default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="8f8a8-122">Vous pouvez maintenant ajouter plus de profils et de règles basées sur la planification de hello ou des exigences spécifiques.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-122">You can now add more profiles and rules based on hello schedule or specific requirements.</span></span> <span data-ttu-id="8f8a8-123">Nous allons créer un paramètre de mise à l’échelle automatique avec trois profils.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="8f8a8-124">toounderstand profils et les règles de mise à l’échelle, passez en revue [mise à l’échelle les meilleures pratiques](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="8f8a8-124">toounderstand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="8f8a8-125">Profils et règles</span><span class="sxs-lookup"><span data-stu-id="8f8a8-125">Profiles & Rules</span></span> | <span data-ttu-id="8f8a8-126">Description</span><span class="sxs-lookup"><span data-stu-id="8f8a8-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="8f8a8-127">**Profil**</span><span class="sxs-lookup"><span data-stu-id="8f8a8-127">**Profile**</span></span> |<span data-ttu-id="8f8a8-128">**En fonction des métriques/performances**</span><span class="sxs-lookup"><span data-stu-id="8f8a8-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="8f8a8-129">Règle</span><span class="sxs-lookup"><span data-stu-id="8f8a8-129">Rule</span></span> |<span data-ttu-id="8f8a8-130">Nombre de messages de la file d’attente Service Bus > x</span><span class="sxs-lookup"><span data-stu-id="8f8a8-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="8f8a8-131">Règle</span><span class="sxs-lookup"><span data-stu-id="8f8a8-131">Rule</span></span> |<span data-ttu-id="8f8a8-132">Nombre de messages de la file d’attente Service Bus < y</span><span class="sxs-lookup"><span data-stu-id="8f8a8-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="8f8a8-133">Règle</span><span class="sxs-lookup"><span data-stu-id="8f8a8-133">Rule</span></span> |<span data-ttu-id="8f8a8-134">%UC > n</span><span class="sxs-lookup"><span data-stu-id="8f8a8-134">CPU% > n</span></span> |
    | <span data-ttu-id="8f8a8-135">Règle</span><span class="sxs-lookup"><span data-stu-id="8f8a8-135">Rule</span></span> |<span data-ttu-id="8f8a8-136">% UC, < p</span><span class="sxs-lookup"><span data-stu-id="8f8a8-136">CPU% < p</span></span> |
    | <span data-ttu-id="8f8a8-137">**Profil**</span><span class="sxs-lookup"><span data-stu-id="8f8a8-137">**Profile**</span></span> |<span data-ttu-id="8f8a8-138">**Heures dans la matinée, en semaine (aucune règle)**</span><span class="sxs-lookup"><span data-stu-id="8f8a8-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="8f8a8-139">**Profil**</span><span class="sxs-lookup"><span data-stu-id="8f8a8-139">**Profile**</span></span> |<span data-ttu-id="8f8a8-140">**Jour de lancement de produit (aucune règle)**</span><span class="sxs-lookup"><span data-stu-id="8f8a8-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="8f8a8-141">Voici un scénario de mise à l’échelle hypothétique que nous utiliserons pour cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="8f8a8-142">**Charge en fonction** -j’aimerais tooscale ou selon la charge de hello sur mon application hébergée sur mon set.* de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="8f8a8-142">**Load based** - I'd like tooscale out or in based on hello load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="8f8a8-143">**Taille de file d’attente de message** -utiliser une file d’attente du Bus de Service pour l’application de toomy de messages entrants hello.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-143">**Message Queue size** - I use a Service Bus Queue for hello incoming messages toomy application.</span></span> <span data-ttu-id="8f8a8-144">Utilisez de hello file d’attente messages et % de l’UC et de la configurer un tootrigger de profil par défaut une action de mise à l’échelle de nombre de messages ou de l’UC accès hello threshold.*</span><span class="sxs-lookup"><span data-stu-id="8f8a8-144">I use hello queue's message count and CPU% and configure a default profile tootrigger a scale action if either of message count or CPU hits hello threshold.*</span></span>
    * <span data-ttu-id="8f8a8-145">**Heure de la semaine et jour** -je voudrais un profil « heure du jour de hello' basé périodique hebdomadaire appelé « Jours ouvrables matin ».</span><span class="sxs-lookup"><span data-stu-id="8f8a8-145">**Time of week and day** - I want a weekly recurring 'time of hello day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="8f8a8-146">Selon les données d’historique, savoir qu’il est mieux toohave certain nombre d’ordinateurs virtuels instances toohandle le chargement de mon application au cours de cette time.*</span><span class="sxs-lookup"><span data-stu-id="8f8a8-146">Based on historical data, I know it is better toohave certain number of VM instances toohandle my application's load during this time.*</span></span>
    * <span data-ttu-id="8f8a8-147">**Dates particulières** : j’ai ajouté un profil « Jour de lancement de produit ».</span><span class="sxs-lookup"><span data-stu-id="8f8a8-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="8f8a8-148">Planifier l’avance des dates spécifiques afin de mon application est la charge de hello toohandle prêt en raison des annonces marketing et lorsqu’un nouveau produit mis en place hello application.*</span><span class="sxs-lookup"><span data-stu-id="8f8a8-148">I plan ahead for specific dates so my application is ready toohandle hello load due marketing announcements and when we put a new product in hello application.*</span></span>
    * <span data-ttu-id="8f8a8-149">*profils de deux derniers Hello peuvent également avoir des autres règles en fonction métriques de performances au sein de celles-ci. Dans ce cas, j’ai ne décidé pas les toohave un et à la place toorely sur les mesures de performance hello par défaut en fonction de règles. Les règles sont facultatives pour hello périodique et date en fonction des profils.*</span><span class="sxs-lookup"><span data-stu-id="8f8a8-149">*hello last two profiles can also have other performance metric based rules within them. In this case, I decided not toohave one and instead toorely on hello default performance metric based rules. Rules are optional for hello recurring and date-based profiles.*</span></span>

    <span data-ttu-id="8f8a8-150">Définition des priorités des profils de hello et des règles du moteur de mise à l’échelle sont également capturées dans hello [échelle meilleures pratiques](insights-autoscale-best-practices.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-150">Autoscale engine's prioritization of hello profiles and rules is also captured in hello [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="8f8a8-151">Pour obtenir une liste des métriques communément utilisées pour la mise à l’échelle, consultez [Métriques courantes pour la mise à l’échelle automatique d’Azure Insights](insights-autoscale-common-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="8f8a8-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="8f8a8-152">Vérifiez que vous êtes sur hello **en lecture/écriture** mode dans l’Explorateur de ressources</span><span class="sxs-lookup"><span data-stu-id="8f8a8-152">Make sure you are on hello **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, paramètre de mise à l’échelle automatique par défaut](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="8f8a8-154">Cliquez sur Modifier.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-154">Click Edit.</span></span> <span data-ttu-id="8f8a8-155">**Remplacez** élément les profils « hello » dans le paramètre de mise à l’échelle par hello configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="8f8a8-155">**Replace** hello 'profiles' element in autoscale setting with hello following configuration:</span></span>

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
    <span data-ttu-id="8f8a8-157">Pour les champs pris en charge et leurs valeurs, consultez la [documentation API REST de la mise à l’échelle automatique](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f8a8-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="8f8a8-158">Le paramètre de mise à l’échelle contient désormais hello trois profils expliqués précédemment.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-158">Now your autoscale setting contains hello three profiles explained previously.</span></span>

7. <span data-ttu-id="8f8a8-159">Pour finir, observez hello échelle **notification** section.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-159">Finally, look at hello Autoscale **notification** section.</span></span> <span data-ttu-id="8f8a8-160">Les notifications de mise à l’échelle permettent toodo trois choses lors d’une montée en puissance, ou dans l’action est déclenchée avec succès.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-160">Autoscale notifications allow you toodo three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="8f8a8-161">Avertir hello admin et les coadministrateurs de votre abonnement</span><span class="sxs-lookup"><span data-stu-id="8f8a8-161">Notify hello admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="8f8a8-162">Envoyer un e-mail à un ensemble d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="8f8a8-162">Email a set of users</span></span>
   - <span data-ttu-id="8f8a8-163">Déclencher un appel webhook.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-163">Trigger a webhook call.</span></span> <span data-ttu-id="8f8a8-164">Lorsqu’il est déclenché, ce webhook envoie des métadonnées sur la condition d’échelle hello et ensemble d’échelle de hello de ressource.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-164">When fired, this webhook sends metadata about hello autoscaling condition and hello scale set resource.</span></span> <span data-ttu-id="8f8a8-165">toolearn en savoir plus sur la charge utile de hello de webhook de l’échelle automatique, consultez [Webhook de configurer et de Notifications par courrier électronique pour la mise à l’échelle](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="8f8a8-165">toolearn more about hello payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="8f8a8-166">Ajouter hello après le remplacement de paramètre de mise à l’échelle toohello votre **notification** élément dont la valeur est null</span><span class="sxs-lookup"><span data-stu-id="8f8a8-166">Add hello following toohello Autoscale setting replacing your **notification** element whose value is null</span></span>

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

   <span data-ttu-id="8f8a8-167">Accès **Put** bouton dans le paramètre de mise à l’échelle de l’Explorateur de ressources tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-167">Hit **Put** button in Resource Explorer tooupdate hello autoscale setting.</span></span>

<span data-ttu-id="8f8a8-168">Vous avez de mises à jour un paramètre sur un tooinclude de jeu de mise à l’échelle de machine virtuelle plusieurs profils de mise à l’échelle d’échelle automatique et des notifications de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-168">You have updated an autoscale setting on a VM Scale set tooinclude multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f8a8-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8f8a8-169">Next Steps</span></span>
<span data-ttu-id="8f8a8-170">Utilisez ces informations supplémentaires sur l’échelle automatique de toolearn de liens.</span><span class="sxs-lookup"><span data-stu-id="8f8a8-170">Use these links toolearn more about autoscaling.</span></span>

[<span data-ttu-id="8f8a8-171">Dépanner la mise à l’échelle automatique avec des jeux de mise à l’échelle de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8f8a8-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="8f8a8-172">Métriques courantes pour la mise à l’échelle automatique d’Azure Insights</span><span class="sxs-lookup"><span data-stu-id="8f8a8-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="8f8a8-173">Meilleures pratiques pour la mise à l’échelle automatique d’Azure Insights</span><span class="sxs-lookup"><span data-stu-id="8f8a8-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="8f8a8-174">Gérer les paramètres de mise à l’échelle automatique à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f8a8-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="8f8a8-175">Gérer les paramètres de mise à l’échelle automatique à l’aide de la CLI</span><span class="sxs-lookup"><span data-stu-id="8f8a8-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="8f8a8-176">Utilisation d’actions de mise à l’échelle automatique pour envoyer des notifications d’alerte webhook et par courrier électronique dans Azure Insights</span><span class="sxs-lookup"><span data-stu-id="8f8a8-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
