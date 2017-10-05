---
title: "Gérer les alertes de sécurité dans le centre de sécurité Azure | Microsoft Docs"
description: "Ce document est conçu pour vous aider à utiliser les fonctionnalités du Centre de sécurité Azure pour gérer et résoudre les alertes de sécurité."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: 56fcfbfdbe15749132ba6a27861142fd564063c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-and-responding-to-security-alerts-in-azure-security-center"></a><span data-ttu-id="6049f-103">Gestion et résolution des alertes de sécurité dans le Centre de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="6049f-103">Managing and responding to security alerts in Azure Security Center</span></span>
<span data-ttu-id="6049f-104">Ce document est conçu pour vous aider à utiliser Azure Security Center afin de gérer et résoudre les alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="6049f-104">This document helps you use Azure Security Center to manage and respond to security alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="6049f-105">Pour activer la détection avancée, effectuez une mise à niveau vers Azure Security Center Standard.</span><span class="sxs-lookup"><span data-stu-id="6049f-105">To enable advanced detections, upgrade to Azure Security Center Standard.</span></span> <span data-ttu-id="6049f-106">Une version d’évaluation gratuite de 60 jours est disponible.</span><span class="sxs-lookup"><span data-stu-id="6049f-106">A free 60-day trial is available.</span></span> <span data-ttu-id="6049f-107">Pour mettre à niveau, sous [Stratégie de sécurité](security-center-policies.md), sélectionnez Niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="6049f-107">To upgrade, select Pricing Tier in the [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="6049f-108">Consultez [Tarification d’Azure Security Center](security-center-pricing.md) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="6049f-108">See [Azure Security Center pricing](security-center-pricing.md) to learn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="6049f-109">Que sont les alertes de sécurité ?</span><span class="sxs-lookup"><span data-stu-id="6049f-109">What are security alerts?</span></span>
<span data-ttu-id="6049f-110">Le Centre de sécurité collecte, analyse et intègre automatiquement les données de journaux provenant de vos ressources Azure, du réseau et des solutions partenaires connectées, telles que les solutions de protection des points de terminaison et des pare-feu, pour détecter les menaces réelles et réduire le nombre de faux positifs.</span><span class="sxs-lookup"><span data-stu-id="6049f-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect real threats and reduce false positives.</span></span> <span data-ttu-id="6049f-111">Une liste hiérarchisée d’alertes de sécurité est affichée dans le Centre de sécurité, ainsi que les informations nécessaires pour trouver rapidement la cause d’une attaque et des recommandations sur la façon d’y remédier.</span><span class="sxs-lookup"><span data-stu-id="6049f-111">A list of prioritized security alerts is shown in Security Center along with the information you need to quickly investigate the problem and recommendations for how to remediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="6049f-112">Pour plus d’informations sur le fonctionnement des fonctionnalités de détection de Security Center, consultez [Fonctionnalités de détection d’Azure Security Center](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="6049f-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="6049f-113">Gestion des alertes de sécurité</span><span class="sxs-lookup"><span data-stu-id="6049f-113">Managing security alerts</span></span>
<span data-ttu-id="6049f-114">Vous pouvez connaître vos alertes actuelles en consultant la vignette **Alertes de sécurité** .</span><span class="sxs-lookup"><span data-stu-id="6049f-114">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="6049f-115">Accédez au Portail Azure et suivez les étapes ci-après pour obtenir plus d’informations sur chaque alerte :</span><span class="sxs-lookup"><span data-stu-id="6049f-115">Open Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="6049f-116">La vignette **Alertes de sécurité** est affichée dans le tableau de bord Centre de sécurité.</span><span class="sxs-lookup"><span data-stu-id="6049f-116">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![Vignette Alertes de sécurité dans le Centre de sécurité](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="6049f-118">Cliquez sur la vignette pour ouvrir le panneau **Alertes de sécurité** , qui fournit des détails supplémentaires sur les alertes, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6049f-118">Click the tile to open the **Security alerts** blade that contains more details about the alerts as shown below.</span></span>

   ![Panneau Alertes de sécurité dans le Centre de sécurité](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="6049f-120">Les détails de chaque alerte sont affichés au bas du panneau.</span><span class="sxs-lookup"><span data-stu-id="6049f-120">In the bottom part of this blade are the details for each alert.</span></span> <span data-ttu-id="6049f-121">Pour les organiser à votre convenance, cliquez sur la colonne que vous voulez trier.</span><span class="sxs-lookup"><span data-stu-id="6049f-121">To sort, click the column that you want to sort by.</span></span> <span data-ttu-id="6049f-122">La définition de chaque colonne est indiquée ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6049f-122">The definition for each column is given below:</span></span>

* <span data-ttu-id="6049f-123">**Description** : brève explication de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="6049f-123">**Description**: A brief explanation of the alert.</span></span>
* <span data-ttu-id="6049f-124">**Nombre**: liste de toutes les alertes d’un type spécifique qui ont été détectées un jour précis.</span><span class="sxs-lookup"><span data-stu-id="6049f-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="6049f-125">**Détectée par**: service à l’origine du déclenchement de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="6049f-125">**Detected by**: The service that was responsible for triggering the alert.</span></span>
* <span data-ttu-id="6049f-126">**Date**: date à laquelle l’événement s’est produit.</span><span class="sxs-lookup"><span data-stu-id="6049f-126">**Date**: The date that the event occurred.</span></span>
* <span data-ttu-id="6049f-127">**État**: état actuel de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="6049f-127">**State**: The current state for that alert.</span></span> <span data-ttu-id="6049f-128">Il existe deux types d’état :</span><span class="sxs-lookup"><span data-stu-id="6049f-128">There are two types of states:</span></span>
  * <span data-ttu-id="6049f-129">**Active**: l’alerte de sécurité a été détectée.</span><span class="sxs-lookup"><span data-stu-id="6049f-129">**Active**: The security alert has been detected.</span></span>
* <span data-ttu-id="6049f-130">**Gravité**: niveau de gravité (élevé, moyen ou bas).</span><span class="sxs-lookup"><span data-stu-id="6049f-130">**Severity**: The severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="6049f-131">Filtrage des alertes</span><span class="sxs-lookup"><span data-stu-id="6049f-131">Filtering alerts</span></span>
<span data-ttu-id="6049f-132">Vous pouvez filtrer les alertes en fonction de la date, de l’état et du niveau de gravité.</span><span class="sxs-lookup"><span data-stu-id="6049f-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="6049f-133">Le filtrage des alertes peut être utile quand vous avez besoin de restreindre le nombre d’alertes de sécurité qui s’affichent.</span><span class="sxs-lookup"><span data-stu-id="6049f-133">Filtering alerts can be useful for scenarios where you need to narrow the scope of security alerts show.</span></span> <span data-ttu-id="6049f-134">Supposons que vous souhaitiez vérifier les alertes de sécurité qui se sont produites au cours des dernières 24 heures, car vous recherchez une violation de sécurité potentielle du système.</span><span class="sxs-lookup"><span data-stu-id="6049f-134">For example, you might you want to address security alerts that occurred in the last 24 hours because you are investigating a potential breach in the system.</span></span>

1. <span data-ttu-id="6049f-135">Cliquez sur **Filtrer** dans le panneau **Alertes de sécurité**.</span><span class="sxs-lookup"><span data-stu-id="6049f-135">Click **Filter** on the **Security Alerts** blade.</span></span> <span data-ttu-id="6049f-136">Dans le panneau **Filtrer** qui s’ouvre, vous pouvez sélectionner la date, l’état et les niveaux de gravité que vous souhaitez visualiser.</span><span class="sxs-lookup"><span data-stu-id="6049f-136">The **Filter** blade opens and you select the date, state, and severity values you wish to see.</span></span>

    ![Filtrage des alertes dans le Centre de sécurité](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-to-security-alerts"></a><span data-ttu-id="6049f-138">Répondre à des alertes de sécurité</span><span class="sxs-lookup"><span data-stu-id="6049f-138">Respond to security alerts</span></span>
<span data-ttu-id="6049f-139">Sélectionnez une alerte de sécurité pour en savoir plus sur les événements qui l’ont déclenchée et, le cas échéant, les étapes à suivre pour y remédier.</span><span class="sxs-lookup"><span data-stu-id="6049f-139">Select a security alert to learn more about the event(s) that triggered the alert and what, if any, steps you need to take to remediate an attack.</span></span> <span data-ttu-id="6049f-140">Les alertes de sécurité sont regroupées par type et date d’apparition.</span><span class="sxs-lookup"><span data-stu-id="6049f-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="6049f-141">Le fait de cliquer sur une alerte de sécurité ouvre un volet contenant une liste des alertes groupées.</span><span class="sxs-lookup"><span data-stu-id="6049f-141">Clicking a security alert will open a blade containing a list of the grouped alerts.</span></span>

![Répondre aux alertes de sécurité dans le centre de sécurité Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="6049f-143">Dans ce cas, les alertes qui ont été déclenchées concernent une activité suspecte utilisant le protocole RDP.</span><span class="sxs-lookup"><span data-stu-id="6049f-143">In this case, the alerts that were triggered refer to suspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="6049f-144">Les première, deuxième, troisième, quatrième et cinquième colonnes affichent respectivement les ressources qui ont été attaquées, le nombre de fois où la ressource a été attaquée, l’heure de l’attaque, l’état de l’alerte et le niveau de gravité de l’attaque.</span><span class="sxs-lookup"><span data-stu-id="6049f-144">The first column shows which resources were attacked; the second shows how many times the resource was attacked; the third shows the time of the attack; the fourth shows state of the alert; and the fifth shows the severity of the attack.</span></span> <span data-ttu-id="6049f-145">Après avoir examiné ces informations, cliquez sur la ressource qui a été attaquée. Un nouveau panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="6049f-145">After reviewing this information, click the resource that was attacked and a new blade will open.</span></span>

![Suggestions sur la façon de traiter les alertes de sécurité dans le centre de sécurité Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="6049f-147">Vous trouverez plus d’informations sur l’événement dans le champ **Description** de ce panneau.</span><span class="sxs-lookup"><span data-stu-id="6049f-147">In the **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="6049f-148">Ces informations permettent d’en savoir plus sur ce qui a déclenché l’alerte de sécurité, sur la ressource cible, sur l’adresse IP source (le cas échéant) et sur la manière de remédier au problème.</span><span class="sxs-lookup"><span data-stu-id="6049f-148">These additional details offer insight into what triggered the security alert, the target resource, when applicable the source IP address, and recommendations about how to remediate.</span></span>  <span data-ttu-id="6049f-149">Dans certains cas, l’adresse IP source sera vide (non disponible), car certains journaux d’événements Windows de la sécurité n’incluent pas l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="6049f-149">In some instances, the source IP address will be empty (not available) because not all Windows security events logs include the IP address.</span></span>

<span data-ttu-id="6049f-150">La correction suggérée par le Centre de sécurité dépend de l’alerte de sécurité.</span><span class="sxs-lookup"><span data-stu-id="6049f-150">The remediation suggested by Security Center will vary according to the security alert.</span></span> <span data-ttu-id="6049f-151">Dans certains cas, vous pouvez être amené à utiliser d’autres fonctionnalités Azure pour appliquer la correction recommandée.</span><span class="sxs-lookup"><span data-stu-id="6049f-151">In some cases, you may have to use other Azure capabilities to implement the recommended remediation.</span></span> <span data-ttu-id="6049f-152">Par exemple, pour cette attaque, la correction consiste à mettre sur liste noire l’adresse IP à l’origine de l’attaque à l’aide d’une règle de [liste de contrôle d’accès (ACL) réseau](../virtual-network/virtual-networks-acl.md) ou de [groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="6049f-152">For example, the remediation for this attack is to blacklist the IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="6049f-153">Pour plus d’informations sur les différents types d’alertes, consultez l’article [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md)(Alertes de sécurité par type dans Azure Security Center).</span><span class="sxs-lookup"><span data-stu-id="6049f-153">For more information on the different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="6049f-154">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6049f-154">See also</span></span>
<span data-ttu-id="6049f-155">Dans ce document, vous avez appris à configurer des stratégies de sécurité dans le Centre de sécurité.</span><span class="sxs-lookup"><span data-stu-id="6049f-155">In this document, you learned how to configure security policies in Security Center.</span></span> <span data-ttu-id="6049f-156">Pour plus d’informations sur le Centre de sécurité, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="6049f-156">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="6049f-157">Gestion des incidents de sécurité dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="6049f-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="6049f-158">Fonctionnalités de détection d’Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="6049f-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="6049f-159">Guide des opérations et de planification du Centre de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="6049f-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="6049f-160">[FAQ d’Azure Security Center](security-center-faq.md) : découvrez les réponses aux questions les plus souvent posées à propos de l’utilisation de ce service.</span><span class="sxs-lookup"><span data-stu-id="6049f-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="6049f-161">[Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.</span><span class="sxs-lookup"><span data-stu-id="6049f-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
