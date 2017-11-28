---
title: Entonnoirs Azure Application Insights
description: "Apprenez à utiliser les entonnoirs pour découvrir de quelle façon les clients interagissent avec votre application."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: cfreeman
ms.openlocfilehash: 85f47daaaff8967eb83c330bab839023f128b486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="discover-how-customers-are-using-your-application-with-the-application-insights-funnels"></a><span data-ttu-id="2e464-103">Découvrez comment les clients utilisent votre application avec les entonnoirs Application Insights</span><span class="sxs-lookup"><span data-stu-id="2e464-103">Discover how customers are using your application with the Application Insights Funnels</span></span>

<span data-ttu-id="2e464-104">Comprendre l’expérience de vos utilisateurs est primordial pour votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="2e464-104">Understanding customer experience is of the utmost importance to your business.</span></span> <span data-ttu-id="2e464-105">Si votre application implique plusieurs étapes, vous devrez savoir si la plupart des clients vont au bout du processus, ou s’ils arrêtent celui-ci à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="2e464-105">If your application involves multiple stages, you will need to know if most customers are progressing through the entire process, or if they are ending the process at some point.</span></span> <span data-ttu-id="2e464-106">La progression via une série d’étapes dans une application web est appelée « entonnoir ».</span><span class="sxs-lookup"><span data-stu-id="2e464-106">The progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="2e464-107">Vous pouvez utiliser les entonnoirs Application Insights pour obtenir des informations sur vos utilisateurs et suivre les taux de conversion étape par étape.</span><span class="sxs-lookup"><span data-stu-id="2e464-107">You can use the Application Insights Funnels to gain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-the-funnels-blade"></a><span data-ttu-id="2e464-108">Prise en main du panneau Entonnoirs</span><span class="sxs-lookup"><span data-stu-id="2e464-108">Get started with the Funnels blade</span></span>
<span data-ttu-id="2e464-109">La meilleure façon d’en savoir plus sur les entonnoirs est de prendre un exemple.</span><span class="sxs-lookup"><span data-stu-id="2e464-109">The easiest way to learn about Funnels is to walk though an example.</span></span> <span data-ttu-id="2e464-110">Les illustrations suivantes montrent les étapes que les propriétaires d’entreprises de e-commerce devraient suivre pour apprendre de quelle façon leurs clients interagissent avec leur application web.</span><span class="sxs-lookup"><span data-stu-id="2e464-110">The following illustrations demonstrate the steps owners of an e-commerce business would take to learn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="2e464-111">Créer votre entonnoir</span><span class="sxs-lookup"><span data-stu-id="2e464-111">Create your funnel</span></span>
<span data-ttu-id="2e464-112">Avant de créer votre entonnoir, vous devez choisir la question à laquelle vous souhaitez répondre.</span><span class="sxs-lookup"><span data-stu-id="2e464-112">Before you create your funnel, you need to decide on the question you want to answer.</span></span> <span data-ttu-id="2e464-113">Par exemple, vous souhaiterez peut-être connaître le nombre de clients qui cliquent sur une publicité lorsqu’ils consultent votre page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="2e464-113">For example, you might want to know how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="2e464-114">Dans cet exemple, les propriétaires de la société Fabrikam Fiber souhaitent connaître le pourcentage de clients qui effectuent un achat après avoir ajouté des articles dans leur panier au cours du mois dernier.</span><span class="sxs-lookup"><span data-stu-id="2e464-114">In this example, the owners of the Fabrikam Fiber company want to know the percentage of customers who make a purchase after adding items to their shopping cart during the last month.</span></span>

<span data-ttu-id="2e464-115">Voici les étapes qu’ils suivent pour créer leur entonnoir.</span><span class="sxs-lookup"><span data-stu-id="2e464-115">Here are the steps they take to create their funnel.</span></span>

1. <span data-ttu-id="2e464-116">Cliquez sur le bouton Nouveau du panneau Entonnoirs.</span><span class="sxs-lookup"><span data-stu-id="2e464-116">Click the New button on the Funnels blade.</span></span>
1. <span data-ttu-id="2e464-117">Sélectionnez l’intervalle de temps « Mois dernier » dans la liste déroulante **Intervalle de temps**.</span><span class="sxs-lookup"><span data-stu-id="2e464-117">Select the time range of "Last month" from the **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="2e464-118">Sélectionnez l’événement **Product page** (Page du produit) dans la liste déroulante **Step 1** (Étape 1).</span><span class="sxs-lookup"><span data-stu-id="2e464-118">Select the **Product page** event from the **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="2e464-119">Sélectionnez l’événement **Add to shopping cart** (Ajouter au panier) dans la liste déroulante **Step 2** (Étape 2).</span><span class="sxs-lookup"><span data-stu-id="2e464-119">Select the **Add to shopping cart** event from the **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="2e464-120">Sélectionnez l’événement **Click purchase** (Cliquer sur Acheter) dans la liste déroulante **Step 3** (Étape 3).</span><span class="sxs-lookup"><span data-stu-id="2e464-120">Select the **Click purchase** event from the **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="2e464-121">Donnez un nom à l’entonnoir, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2e464-121">Add a name to the funnel and click **Save**.</span></span>

<span data-ttu-id="2e464-122">L’illustration suivante montre les données générées par le panneau Entonnoirs.</span><span class="sxs-lookup"><span data-stu-id="2e464-122">The following illustration demonstrates the data the Funnels blade generates.</span></span> <span data-ttu-id="2e464-123">À partir d’ici, les propriétaires de Fabrikam peuvent voir que pendant la semaine passée, 22,7 % des clients ayant ajouté un article à leur panier ont effectué un achat.</span><span class="sxs-lookup"><span data-stu-id="2e464-123">From here the Fabrikam owners can see that during the last week, 22.7% of their customers who added an item to their shopping cart completed the purchase.</span></span> <span data-ttu-id="2e464-124">Ils peuvent également voir que 1 % des clients ont cliqué sur une publicité avant de consulter la page du produit, et que 20 % des clients se sont déconnectés après avoir effectué leur achat.</span><span class="sxs-lookup"><span data-stu-id="2e464-124">They can also see that 1% of the customers clicked an advertisement before visiting the product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Panneau Entonnoirs avec des données](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="2e464-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e464-126">Next steps</span></span>
- <span data-ttu-id="2e464-127">En savoir plus sur [l’analyse de l’utilisation](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2e464-127">Learn more about [usage analysis](app-insights-usage-overview.md).</span></span> 
