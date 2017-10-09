---
title: aaaAzure Application Insights Entonnoirs
description: "Découvrez comment vous pouvez utiliser les Entonnoirs toodiscover comment les clients interagissent avec votre application."
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
ms.openlocfilehash: 3a90cfd11cb193e303136504df44008ffd04a290
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="discover-how-customers-are-using-your-application-with-hello-application-insights-funnels"></a><span data-ttu-id="4372d-103">Découvrez comment les clients utilisent votre application avec Application Insights Entonnoirs de hello</span><span class="sxs-lookup"><span data-stu-id="4372d-103">Discover how customers are using your application with hello Application Insights Funnels</span></span>

<span data-ttu-id="4372d-104">Expérience de présentation est d’entreprise de tooyour hello plus haute importance.</span><span class="sxs-lookup"><span data-stu-id="4372d-104">Understanding customer experience is of hello utmost importance tooyour business.</span></span> <span data-ttu-id="4372d-105">Si votre application implique plusieurs étapes, vous devez tooknow si la progression de la plupart des clients via l’ensemble du processus hello, ou si elles sont se terminant par processus hello à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="4372d-105">If your application involves multiple stages, you will need tooknow if most customers are progressing through hello entire process, or if they are ending hello process at some point.</span></span> <span data-ttu-id="4372d-106">progression Hello via une série d’étapes dans une application web est appelée un « entonnoir ».</span><span class="sxs-lookup"><span data-stu-id="4372d-106">hello progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="4372d-107">Vous pouvez utiliser hello Application Insights Entonnoirs toogain vue d’ensemble de vos utilisateurs et les taux de conversion pas à pas de moniteur.</span><span class="sxs-lookup"><span data-stu-id="4372d-107">You can use hello Application Insights Funnels toogain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-hello-funnels-blade"></a><span data-ttu-id="4372d-108">Prise en main Panneau d’Entonnoirs hello</span><span class="sxs-lookup"><span data-stu-id="4372d-108">Get started with hello Funnels blade</span></span>
<span data-ttu-id="4372d-109">Hello toolearn de façon plus simple sur Entonnoirs est toowalk si un exemple.</span><span class="sxs-lookup"><span data-stu-id="4372d-109">hello easiest way toolearn about Funnels is toowalk though an example.</span></span> <span data-ttu-id="4372d-110">Hello illustrations suivantes montrent les propriétaires d’étapes hello d’une entreprise de commerce électronique prendrait toolearn comment leurs clients interagissent avec l’application web.</span><span class="sxs-lookup"><span data-stu-id="4372d-110">hello following illustrations demonstrate hello steps owners of an e-commerce business would take toolearn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="4372d-111">Créer votre entonnoir</span><span class="sxs-lookup"><span data-stu-id="4372d-111">Create your funnel</span></span>
<span data-ttu-id="4372d-112">Avant de créer votre en entonnoir, vous devez toodecide sur la question de hello souhaité tooanswer.</span><span class="sxs-lookup"><span data-stu-id="4372d-112">Before you create your funnel, you need toodecide on hello question you want tooanswer.</span></span> <span data-ttu-id="4372d-113">Par exemple, vous pourriez tooknow le nombre de clients affichage de votre page d’accueil, cliquez sur une publication.</span><span class="sxs-lookup"><span data-stu-id="4372d-113">For example, you might want tooknow how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="4372d-114">Dans cet exemple, les propriétaires de hello Hello entreprise de Fabrikam Fiber veulent pourcentage de hello tooknow de clients fassent un achat après l’ajout de tootheir éléments panier d’achat pendant hello du mois précédent.</span><span class="sxs-lookup"><span data-stu-id="4372d-114">In this example, hello owners of hello Fabrikam Fiber company want tooknow hello percentage of customers who make a purchase after adding items tootheir shopping cart during hello last month.</span></span>

<span data-ttu-id="4372d-115">Voici les étapes hello informerons toocreate leur en entonnoir.</span><span class="sxs-lookup"><span data-stu-id="4372d-115">Here are hello steps they take toocreate their funnel.</span></span>

1. <span data-ttu-id="4372d-116">Sur le bouton Nouveau hello Panneau d’Entonnoirs hello.</span><span class="sxs-lookup"><span data-stu-id="4372d-116">Click hello New button on hello Funnels blade.</span></span>
1. <span data-ttu-id="4372d-117">Sélectionnez plage de temps hello de « Mois » à partir de hello **période** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="4372d-117">Select hello time range of "Last month" from hello **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="4372d-118">Sélectionnez hello **page produit** événement hello **étape 1** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="4372d-118">Select hello **Product page** event from hello **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="4372d-119">Sélectionnez hello **ajouter tooshopping panier** événement hello **étape 2** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="4372d-119">Select hello **Add tooshopping cart** event from hello **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="4372d-120">Sélectionnez hello **cliquez sur acheter** événement hello **étape 3** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="4372d-120">Select hello **Click purchase** event from hello **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="4372d-121">Ajouter un graphique en entonnoir toohello de nom, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4372d-121">Add a name toohello funnel and click **Save**.</span></span>

<span data-ttu-id="4372d-122">Hello l’illustration suivante montre lame Entonnoirs hello hello génère.</span><span class="sxs-lookup"><span data-stu-id="4372d-122">hello following illustration demonstrates hello data hello Funnels blade generates.</span></span> <span data-ttu-id="4372d-123">À partir d’ici hello Fabrikam propriétaires peuvent voir que pendant la dernière semaine de hello, % 22.7 des clients qui l’a ajouté un élément tootheir d’achat panier achat de hello terminée.</span><span class="sxs-lookup"><span data-stu-id="4372d-123">From here hello Fabrikam owners can see that during hello last week, 22.7% of their customers who added an item tootheir shopping cart completed hello purchase.</span></span> <span data-ttu-id="4372d-124">Ils peuvent également voir que 1 % des clients de hello cliqué une publication avant la visite de page du produit hello et 20 % des clients déconnectés après avoir effectué leur achat.</span><span class="sxs-lookup"><span data-stu-id="4372d-124">They can also see that 1% of hello customers clicked an advertisement before visiting hello product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Panneau Entonnoirs avec des données](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="4372d-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4372d-126">Next steps</span></span>
- <span data-ttu-id="4372d-127">En savoir plus sur [l’analyse de l’utilisation](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4372d-127">Learn more about [usage analysis](app-insights-usage-overview.md).</span></span> 
