---
title: "aaaGet démarrée avec l’échelle automatique par métrique personnalisée dans Azure | Documents Microsoft"
description: "Découvrez comment tooscale votre ressource en fonction de la métrique personnalisée dans Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="8b9ac-103">Prise en main de la mise à l’échelle automatique par métrique personnalisée dans Azure</span><span class="sxs-lookup"><span data-stu-id="8b9ac-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="8b9ac-104">Cet article décrit comment tooscale votre ressource par une métrique personnalisée dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-104">This article describes how tooscale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="8b9ac-105">Azure à l’échelle automatique analyse s’applique uniquement tooVirtual jeux de mise à l’échelle de Machine (mise), services de cloud computing, les plans de service d’application et les environnements app service.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="8b9ac-106">Prise en main</span><span class="sxs-lookup"><span data-stu-id="8b9ac-106">Lets get started</span></span>
<span data-ttu-id="8b9ac-107">Cet article suppose que vous disposez d’une application web avec Application Insights déjà configuré.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="8b9ac-108">Si vous ne l’avez pas encore fait, vous pouvez [configurer Application Insights pour votre site web ASP.NET][1]</span><span class="sxs-lookup"><span data-stu-id="8b9ac-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="8b9ac-109">Ouvrez le [portail Azure][2]</span><span class="sxs-lookup"><span data-stu-id="8b9ac-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="8b9ac-110">Cliquez sur l’icône Azure dans le volet de navigation gauche hello.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-110">Click on Azure Monitor icon in hello left navigation pane.</span></span>
  <span data-ttu-id="8b9ac-111">![Lancer Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="8b9ac-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="8b9ac-112">Cliquez sur l’échelle automatique de la définition de toutes les ressources hello pour l’automatiquement mise à l’échelle est applicable, ainsi que son état actuel de la mise à l’échelle tooview ![découvrir à l’échelle automatique dans le moniteur de Azure][4]</span><span class="sxs-lookup"><span data-stu-id="8b9ac-112">Click on Autoscale setting tooview all hello resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="8b9ac-113">Ouvrir le panneau 'd’échelle automatique' dans le moniteur de Azure et sélectionnez une ressource tooscale</span><span class="sxs-lookup"><span data-stu-id="8b9ac-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want tooscale</span></span>
> <span data-ttu-id="8b9ac-114">Remarque : des étapes de hello ci-dessous utilisent un plan de service d’application associé à une application web qui a des aperçus d’application configurés.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-114">Note: hello steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="8b9ac-115">Dans le panneau de configuration hello mise à l’échelle pour la ressource de hello, notez que le nombre d’instances actuelles hello est 1.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-115">In hello scale setting blade for hello resource, notice that hello current instance count is 1.</span></span> <span data-ttu-id="8b9ac-116">Cliquez sur « Activer la mise à l’échelle automatique ».</span><span class="sxs-lookup"><span data-stu-id="8b9ac-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="8b9ac-117">![Paramètre d’échelle pour la nouvelle application web][5]</span><span class="sxs-lookup"><span data-stu-id="8b9ac-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="8b9ac-118">Fournissez un nom pour le paramètre d’échelle hello et hello cliquez sur « Ajouter une règle ».</span><span class="sxs-lookup"><span data-stu-id="8b9ac-118">Provide a name for hello scale setting, and hello click on "Add a rule".</span></span> <span data-ttu-id="8b9ac-119">Notez que les options de règle de mise à l’échelle de hello qui s’ouvre dans la partie droite de hello, un volet de contexte.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-119">Notice hello scale rule options that opens as a context pane in hello right hand side.</span></span> <span data-ttu-id="8b9ac-120">Par défaut, il définit tooscale d’option hello votre instance compter à 1 si percetage de processeur hello de ressource de hello est supérieure à 70 %.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-120">By default, it sets hello option tooscale your instance count by 1 if hello CPU percetage of hello resource exceeds 70%.</span></span> <span data-ttu-id="8b9ac-121">Modifier la source de métrique hello haut hello trop « Application Insights », sélectionnez hello la ressource application insights dans hello 'Resource' dropdown et métrique personnalisée de hello puis basé sur lequel vous souhaitez tooscale.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-121">Change hello metric source at hello top too"Application Insights", select hello app insights resource in hello 'Resource' dropdown and then select hello custom metric based on which you want tooscale.</span></span>
  <span data-ttu-id="8b9ac-122">![Mettre à l’échelle par métrique personnalisée][6]</span><span class="sxs-lookup"><span data-stu-id="8b9ac-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="8b9ac-123">Étape toohello similaire ci-dessus, ajouter une règle de mise à l’échelle qui est ajustée dans et diminuer le nombre de montée en puissance hello par 1 si la métrique personnalisée de hello est au-dessous du seuil.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-123">Similar toohello step above, add a scale rule that will scale in and decrease hello scale count by 1 if hello custom metric is below a threshold.</span></span>
  <span data-ttu-id="8b9ac-124">![Mise à l’échelle en fonction du processeur][7]</span><span class="sxs-lookup"><span data-stu-id="8b9ac-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="8b9ac-125">Définissez hello instance de limites.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-125">Set hello you instance limits.</span></span> <span data-ttu-id="8b9ac-126">Par exemple, si vous souhaitez tooscale entre des instances de 2 à 5 selon les fluctuations de métrique personnalisée hello, définissez 'minimale' trop '2', 'maximum' trop '5' et 'default' trop « 2 »</span><span class="sxs-lookup"><span data-stu-id="8b9ac-126">For example, if you want tooscale between 2-5 instances depending on hello custom metric fluctuations, set 'minimum' too'2', 'maximum' too'5' and 'default' too'2'</span></span>
> <span data-ttu-id="8b9ac-127">Remarque : au cas où il existe un problème de lecture des métriques de ressources hello et capacité actuelle de hello est inférieures à la capacité par défaut de hello, puis disponibilité de hello tooensure de ressource de hello, mise à l’échelle évoluera toohello dont la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-127">Note: In case there is a problem reading hello resource metrics and hello current capacity is below hello default capacity, then tooensure hello availability of hello resource, Autoscale will scale out toohello default value.</span></span> <span data-ttu-id="8b9ac-128">Si la propriété capacity hello est déjà supérieur à la capacité par défaut, la mise à l’échelle n’évolue pas dans.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-128">If hello current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="8b9ac-129">Cliquez sur « Enregistrer »</span><span class="sxs-lookup"><span data-stu-id="8b9ac-129">Click on 'Save'</span></span>

<span data-ttu-id="8b9ac-130">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="8b9ac-130">Congratulations.</span></span> <span data-ttu-id="8b9ac-131">Vous pouvez maintenant correctement créé votre échelle définissant tooauto mise à l’échelle votre application web basée sur une mesure personnalisée.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-131">You now now succesfully created your scale setting tooauto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="8b9ac-132">Remarque : hello la même procédure est applicable tooget un rôle de service cloud ou de mise en route.</span><span class="sxs-lookup"><span data-stu-id="8b9ac-132">Note: hello same steps are applicable tooget started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
