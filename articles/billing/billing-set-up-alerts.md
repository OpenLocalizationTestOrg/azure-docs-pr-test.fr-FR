---
title: "aaaSet des alertes de facturation ou crédit pour les abonnements Azure | Documents Microsoft"
description: Describes how you can set up alerts on your Azure bill so you can avoid billing surprises.
keywords: "alerte de crédit, alerte de facturation"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="f242a-104">Configurer des alertes de facturation ou de crédit pour vos abonnements Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f242a-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="f242a-105">Si vous êtes hello Admin. compte pour un abonnement Azure, vous pouvez utiliser hello Azure facturation Service d’alerte facturation de toocreate personnalisé des alertes qui vous aident à surveillez et gérez l’activité de facturation pour vos comptes Azure.</span><span class="sxs-lookup"><span data-stu-id="f242a-105">If you’re hello Account Admin for an Azure subscription, you can use hello Azure Billing Alert Service toocreate customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="f242a-106">Ce service est en version préliminaire, donc vous devez tooenable il dans la page des fonctionnalités en version préliminaire hello tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="f242a-106">This service is in preview, so you need tooenable it in hello Preview Features page first.</span></span>

## <a name="set-hello-alert-threshold-and-email-recipients"></a><span data-ttu-id="f242a-107">Définir les destinataires de messagerie et le seuil d’alerte hello</span><span class="sxs-lookup"><span data-stu-id="f242a-107">Set hello alert threshold and email recipients</span></span>
1. <span data-ttu-id="f242a-108">Visitez [page des fonctionnalités en version préliminaire hello](https://account.windowsazure.com/PreviewFeatures) et activer **Service d’alerte de facturation**.</span><span class="sxs-lookup"><span data-stu-id="f242a-108">Visit [hello Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="f242a-109">Une fois que vous recevez un e-mail de confirmation hello que le service de facturation hello est activé pour votre abonnement, visitez [page des abonnements hello](https://account.windowsazure.com/Subscriptions) dans le portail du compte hello.</span><span class="sxs-lookup"><span data-stu-id="f242a-109">After you receive hello email confirmation that hello billing service is turned on for your subscription, visit [hello Subscriptions page](https://account.windowsazure.com/Subscriptions) in hello account portal.</span></span> <span data-ttu-id="f242a-110">Cliquez sur votre choix toomonitor, puis cliquez sur l’abonnement hello **alertes**.</span><span class="sxs-lookup"><span data-stu-id="f242a-110">Click hello subscription you want toomonitor, and then click **Alerts**.</span></span>

    ![Capture d’écran d’affichage d’abonnements hello du centre de compte Azure, des alertes en surbrillance][Image1]

2. <span data-ttu-id="f242a-112">Ensuite, cliquez sur **ajouter alertes** toocreate votre première application.</span><span class="sxs-lookup"><span data-stu-id="f242a-112">Next, click **Add Alert** toocreate your first one.</span></span> <span data-ttu-id="f242a-113">Vous pouvez définir un total de cinq alertes de facturation par abonnement, un seuil propre et tootwo les destinataires de courrier électronique pour chaque alerte.</span><span class="sxs-lookup"><span data-stu-id="f242a-113">You can set up a total of five billing alerts per subscription, with a different threshold and up tootwo email recipients for each alert.</span></span>

    ![Capture d’écran de hello affichage des alertes, où vous pouvez ajouter l’alerte][Image2]

3. <span data-ttu-id="f242a-115">Lorsque vous ajoutez une alerte, vous lui donnez un nom unique, choisissez un seuil de dépense, choisissez hello les adresses de messagerie où les alertes sont envoyées.</span><span class="sxs-lookup"><span data-stu-id="f242a-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose hello email addresses where alerts are sent.</span></span> <span data-ttu-id="f242a-116">Lorsque vous configurez le seuil de hello, vous pouvez choisir un **Total de facturation** ou un **du crédit** de hello **alerte pour** liste.</span><span class="sxs-lookup"><span data-stu-id="f242a-116">When setting up hello threshold, you can choose either a **Billing Total** or a **Monetary Credit** from hello **Alert For** list.</span></span> <span data-ttu-id="f242a-117">Pour un total de facturation, une alerte est envoyée lorsque les dépenses de l’abonnement de dépasse le seuil de hello.</span><span class="sxs-lookup"><span data-stu-id="f242a-117">For a billing total, an alert is sent when subscription spending exceeds hello threshold.</span></span> <span data-ttu-id="f242a-118">Pour un crédit monétaire, une alerte est envoyée lorsque les crédits monétaires descendent en dessous de la limite de hello.</span><span class="sxs-lookup"><span data-stu-id="f242a-118">For a monetary credit, an alert is sent when monetary credits drop below hello limit.</span></span> <span data-ttu-id="f242a-119">Les crédits monétaires s’appliquent généralement à tooFree des abonnements d’évaluation et de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f242a-119">Monetary credits usually apply tooFree Trial and Visual Studio subscriptions.</span></span>

    ![Capture d’écran d’affichage d’alerte Ajout hello, dans laquelle vous pouvez configurer les destinataires][Image3]

<span data-ttu-id="f242a-121">Azure prend en charge n’importe quelle adresse de messagerie, mais ne vérifiez que les adresses de messagerie hello fonctionne, vérifiez donc attentivement les fautes de frappe.</span><span class="sxs-lookup"><span data-stu-id="f242a-121">Azure supports any email address but doesn't verify that hello email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="f242a-122">Vérifier vos alertes</span><span class="sxs-lookup"><span data-stu-id="f242a-122">Check on your alerts</span></span>
<span data-ttu-id="f242a-123">Après avoir défini des alertes, hello centre des comptes les répertorie et indique combien de plus, vous pouvez configurer des.</span><span class="sxs-lookup"><span data-stu-id="f242a-123">After you set up alerts, hello Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="f242a-124">Pour chaque alerte, vous consultez hello limite de date et heure de qu'envoi, s’il s’agit d’une alerte pour un Total de facturation ou crédit monétaire et hello que permet de paramétrer.</span><span class="sxs-lookup"><span data-stu-id="f242a-124">For each alert, you see hello date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and hello limit you set up.</span></span> <span data-ttu-id="f242a-125">format de date et d’heure Hello est 24 heures heure universelle coordonnée (UTC) et la date de hello est aaaa-mm-jj format.</span><span class="sxs-lookup"><span data-stu-id="f242a-125">hello date and time format is 24-hour Universal Time Coordinate (UTC) and hello date is yyyy-mm-dd format.</span></span> <span data-ttu-id="f242a-126">Cliquez sur hello plus se connecter à une alerte dans hello liste tooedit ou hello-Corbeille toodelete il.</span><span class="sxs-lookup"><span data-stu-id="f242a-126">Click hello plus sign for an alert in hello list tooedit it, or click hello trash-can toodelete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="f242a-127">Alertes de facturation pour les clients Contrat Entreprise</span><span class="sxs-lookup"><span data-stu-id="f242a-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="f242a-128">Les clients Contrat Entreprise (EA) peuvent recevoir des alertes pour chaque département pour une inscription en définissant des quotas de dépense.</span><span class="sxs-lookup"><span data-stu-id="f242a-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="f242a-129">Consultez [Quotas de service de dépense](https://ea.azure.com/helpdocs/departmentSpendingQuotas) dans les tooget portail EA hello a démarré.</span><span class="sxs-lookup"><span data-stu-id="f242a-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in hello EA portal tooget started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="f242a-130">En savoir plus sur la gestion des coûts dans Azure</span><span class="sxs-lookup"><span data-stu-id="f242a-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="f242a-131">Estimer les coûts à l’aide de hello [calculatrice de prix](https://azure.microsoft.com/pricing/calculator/), [coût total de l’outil de calcul de la propriété](https://aka.ms/azure-tco-calculator), et lorsque vous ajoutez un service.</span><span class="sxs-lookup"><span data-stu-id="f242a-131">Estimate costs using hello [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="f242a-132">[Passez en revue régulièrement votre utilisation et vos coûts dans le portail Azure](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="f242a-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="f242a-133">Activez les [Recommandations de coûts du conseiller Azure](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="f242a-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="f242a-134">toolearn, voir [conseils sur la gestion des coûts Azure](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="f242a-134">toolearn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
