---
title: "Configurer des alertes de facturation ou de crédit pour vos abonnements Azure | Microsoft Docs"
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
ms.openlocfilehash: 7a1b579fdde831fdc3afa0a2aee4c24890216ed1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="09b48-104">Configurer des alertes de facturation ou de crédit pour vos abonnements Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="09b48-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="09b48-105">Si vous êtes l'administrateur de compte d'un abonnement Azure, vous pouvez utiliser le service d'alerte de facturation Azure pour créer des alertes de facturation personnalisées qui vous aident à surveiller et à gérer l'activité de facturation de vos comptes Azure.</span><span class="sxs-lookup"><span data-stu-id="09b48-105">If you’re the Account Admin for an Azure subscription, you can use the Azure Billing Alert Service to create customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="09b48-106">Ce service est disponible en version préliminaire. Vous devez l’activer d’abord dans la page Fonctionnalités préliminaires.</span><span class="sxs-lookup"><span data-stu-id="09b48-106">This service is in preview, so you need to enable it in the Preview Features page first.</span></span>

## <a name="set-the-alert-threshold-and-email-recipients"></a><span data-ttu-id="09b48-107">Définir le seuil d'alerte et les destinataires des messages électroniques</span><span class="sxs-lookup"><span data-stu-id="09b48-107">Set the alert threshold and email recipients</span></span>
1. <span data-ttu-id="09b48-108">Visitez [la page fonctionnalités préliminaires](https://account.windowsazure.com/PreviewFeatures) et activez le **service d’alerte de facturation**.</span><span class="sxs-lookup"><span data-stu-id="09b48-108">Visit [the Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="09b48-109">Lorsque vous aurez reçu par courrier électronique la confirmation que le service de facturation a été activé pour votre abonnement, rendez-vous sur la [page Abonnements](https://account.windowsazure.com/Subscriptions) du portail des comptes.</span><span class="sxs-lookup"><span data-stu-id="09b48-109">After you receive the email confirmation that the billing service is turned on for your subscription, visit [the Subscriptions page](https://account.windowsazure.com/Subscriptions) in the account portal.</span></span> <span data-ttu-id="09b48-110">Cliquez sur l’abonnement à surveiller, puis sur **Alertes**.</span><span class="sxs-lookup"><span data-stu-id="09b48-110">Click the subscription you want to monitor, and then click **Alerts**.</span></span>

    ![Capture d’écran de l’affichage des abonnements dans le Centre de comptes Azure, avec les alertes mises en surbrillance][Image1]

2. <span data-ttu-id="09b48-112">Ensuite, cliquez sur **Ajouter une alerte** pour créer votre première alerte.</span><span class="sxs-lookup"><span data-stu-id="09b48-112">Next, click **Add Alert** to create your first one.</span></span> <span data-ttu-id="09b48-113">Vous pouvez configurer un total de cinq alertes de facturation par abonnement avec un seuil distinct, et jusqu’à deux destinataires d’e-mail pour chaque alerte.</span><span class="sxs-lookup"><span data-stu-id="09b48-113">You can set up a total of five billing alerts per subscription, with a different threshold and up to two email recipients for each alert.</span></span>

    ![Capture d’écran de l’affichage des alertes dans lequel pouvez ajouter une alerte][Image2]

3. <span data-ttu-id="09b48-115">Quand vous ajoutez une alerte, vous lui donnez un nom unique, vous choisissez un seuil de dépenses, et vous choisissez également les e-mails auxquelles les alertes sont envoyées.</span><span class="sxs-lookup"><span data-stu-id="09b48-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose the email addresses where alerts are sent.</span></span> <span data-ttu-id="09b48-116">Quand vous configurez le seuil, vous pouvez choisir un **Total facturé** ou un **Crédit monétaire** dans la liste **Alerte pour**.</span><span class="sxs-lookup"><span data-stu-id="09b48-116">When setting up the threshold, you can choose either a **Billing Total** or a **Monetary Credit** from the **Alert For** list.</span></span> <span data-ttu-id="09b48-117">Pour un total facturé, une alerte est envoyée quand les dépenses d'abonnement dépassent le seuil.</span><span class="sxs-lookup"><span data-stu-id="09b48-117">For a billing total, an alert is sent when subscription spending exceeds the threshold.</span></span> <span data-ttu-id="09b48-118">Pour un crédit monétaire, une alerte est envoyée quand les crédits monétaires passent sous la limite.</span><span class="sxs-lookup"><span data-stu-id="09b48-118">For a monetary credit, an alert is sent when monetary credits drop below the limit.</span></span> <span data-ttu-id="09b48-119">Les crédits monétaires s’appliquent habituellement aux abonnements d’essai gratuit et Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="09b48-119">Monetary credits usually apply to Free Trial and Visual Studio subscriptions.</span></span>

    ![Capture d’écran de la vue d’ajout d’une alerte dans laquelle vous pouvez configurer les destinataires][Image3]

<span data-ttu-id="09b48-121">Azure prend en charge toutes les adresses e-mail mais ne vérifie pas si elles sont valides. Vous devez donc vous assurer qu'il n'y a aucune faute de frappe.</span><span class="sxs-lookup"><span data-stu-id="09b48-121">Azure supports any email address but doesn't verify that the email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="09b48-122">Vérifier vos alertes</span><span class="sxs-lookup"><span data-stu-id="09b48-122">Check on your alerts</span></span>
<span data-ttu-id="09b48-123">Une fois que vous avez configuré des alertes, le Centre des comptes les répertorie et vous montre le nombre d'alertes que vous pouvez encore configurer.</span><span class="sxs-lookup"><span data-stu-id="09b48-123">After you set up alerts, the Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="09b48-124">Pour chaque alerte, vous voyez la date et l'heure d'envoi, s'il s'agit d'une alerte relative au total facturé ou au crédit monétaire, ainsi que la limite que vous avez configurée.</span><span class="sxs-lookup"><span data-stu-id="09b48-124">For each alert, you see the date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and the limit you set up.</span></span> <span data-ttu-id="09b48-125">L'heure est au format 24 heures UTC (Universal Time Coordinate) et la date est au format aaaa-mm-jj.</span><span class="sxs-lookup"><span data-stu-id="09b48-125">The date and time format is 24-hour Universal Time Coordinate (UTC) and the date is yyyy-mm-dd format.</span></span> <span data-ttu-id="09b48-126">Cliquez sur le signe plus pour modifier une alerte listée, ou cliquez sur la poubelle pour la supprimer.</span><span class="sxs-lookup"><span data-stu-id="09b48-126">Click the plus sign for an alert in the list to edit it, or click the trash-can to delete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="09b48-127">Alertes de facturation pour les clients Contrat Entreprise</span><span class="sxs-lookup"><span data-stu-id="09b48-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="09b48-128">Les clients Contrat Entreprise (EA) peuvent recevoir des alertes pour chaque département pour une inscription en définissant des quotas de dépense.</span><span class="sxs-lookup"><span data-stu-id="09b48-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="09b48-129">Consultez les [quotas de dépense des départements](https://ea.azure.com/helpdocs/departmentSpendingQuotas) dans le portail EA pour commencer.</span><span class="sxs-lookup"><span data-stu-id="09b48-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in the EA portal to get started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="09b48-130">En savoir plus sur la gestion des coûts dans Azure</span><span class="sxs-lookup"><span data-stu-id="09b48-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="09b48-131">Estimez les coûts à l’aide de la [calculatrice de prix](https://azure.microsoft.com/pricing/calculator/) et de la [calculatrice du coût total de possession](https://aka.ms/azure-tco-calculator), également lorsque vous ajoutez un service.</span><span class="sxs-lookup"><span data-stu-id="09b48-131">Estimate costs using the [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="09b48-132">[Passez en revue régulièrement votre utilisation et vos coûts dans le portail Azure](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="09b48-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="09b48-133">Activez les [Recommandations de coûts du conseiller Azure](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="09b48-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="09b48-134">Pour plus d’informations, consultez [le guide de gestion des coûts Azure](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="09b48-134">To learn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
