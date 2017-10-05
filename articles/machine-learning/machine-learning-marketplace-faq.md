---
title: "(obsolète) Forum aux questions : publication et utilisation d’applications Machine Learning sur Azure Marketplace | Microsoft Docs"
description: "(obsolète) Forum aux questions sur la publication d’applications Machine Learning dans Azure Marketplace"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a4631dfeb2f817b3a3c612a8f6af48398e4f2ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-the-azure-marketplace-faq"></a><span data-ttu-id="b2ad1-103">(obsolète) Publication et utilisation d’applications Machine Learning sur Azure Marketplace : forum aux questions</span><span class="sxs-lookup"><span data-stu-id="b2ad1-103">(deprecated) Publishing and using Machine Learning apps in the Azure Marketplace: FAQ</span></span>

> [!NOTE]
> <span data-ttu-id="b2ad1-104">DataMarket et Data Services vont être mis hors service et les abonnements existants seront annulés à compter du 31/03/2017.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="b2ad1-105">Par conséquent, cet article deviendra obsolète.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="b2ad1-106">Vous pouvez aussi publier vos expériences d’apprentissage Machine Learning dans la [galerie Cortana Intelligence](https://gallery.cortanaintelligence.com/) pour les partager avec la communauté spécialiste des données.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-106">As an alternative, you can publish your Machine Learning experiments to the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for the benefit of the data science community.</span></span> <span data-ttu-id="b2ad1-107">Pour plus d’informations, consultez [Partager et découvrir des solutions dans la galerie Cortana Intelligence](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="b2ad1-107">For more information, see [Share and discover resources in the Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>


## <a name="questions-about-consuming-from-marketplace"></a><span data-ttu-id="b2ad1-108">Questions relatives à la consommation à partir de Marketplace</span><span class="sxs-lookup"><span data-stu-id="b2ad1-108">Questions about consuming from Marketplace</span></span>
<span data-ttu-id="b2ad1-109">**1. Le message d’erreur suivant apparaît une fois que j’ai saisi l’entrée pour le service web. Pourquoi ai-je cette erreur ?**</span><span class="sxs-lookup"><span data-stu-id="b2ad1-109">**1. Why do I get the following error message after I enter input for the web service:**</span></span>

<span data-ttu-id="b2ad1-110">**La demande a provoqué une erreur de temporisation ou une erreur sur le serveur principal. Notre équipe étudie en ce moment ce problème. Nous sommes désolés pour ce désagrément. (500)**</span><span class="sxs-lookup"><span data-stu-id="b2ad1-110">**The request resulted in a back-end time out or back-end error. The team is investigating the issue. We are sorry for the inconvenience. (500)**</span></span>

<span data-ttu-id="b2ad1-111">Vos paramètres d'entrée peuvent ne pas être conformes au format requis pour le service web spécifique.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-111">Your input parameter(s) may not conform to the required format for the specific web service.</span></span> <span data-ttu-id="b2ad1-112">Consultez le lien correspondant dans la documentation afin de rechercher le format correct pour les paramètres d'entrée et les limitations de ce service web.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-112">Please refer to the corresponding documentation link to find the correct format for input parameters and the limitations of this web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="b2ad1-113">**2. Si je copie le lien de l’API du service web que je vois sur la page « Explorer ce jeu de données » et que je le colle dans une autre fenêtre du navigateur, quelles informations d’identification dois-je utiliser pour accéder aux résultats et comment puis-je les afficher ?**</span><span class="sxs-lookup"><span data-stu-id="b2ad1-113">**2. If I copy the API link for the web service that I see on the "Explore this dataset" page and paste it into another browser window, what credentials should I use to access the results, and how do I see them?**</span></span>

<span data-ttu-id="b2ad1-114">Vous devez utiliser votre compte Marketplace en tant que nom d'utilisateur et la clé de compte principal comme mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-114">You should use your Marketplace account as the username and the primary account key as the password.</span></span> <span data-ttu-id="b2ad1-115">La clé de compte principal se trouve sur la page **Explorer ce jeu de données** sous la description du service web (cliquez sur le bouton **Afficher**).</span><span class="sxs-lookup"><span data-stu-id="b2ad1-115">The primary account key can be found on the **Explore this dataset** page under the description of the web service (click the **show** button).</span></span> <span data-ttu-id="b2ad1-116">Le résultat peut s’afficher dans le navigateur ou être disponible en téléchargement, en fonction du navigateur que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-116">The result may display in the browser or it may be available to  download, depending on which browser you are using.</span></span>

<span data-ttu-id="b2ad1-117">**3. Le message d’erreur suivant apparaît une fois que j’ai saisi l’entrée pour le service web sur la page « Explorer ce jeu de données ». Pourquoi ai-je cette erreur ?**</span><span class="sxs-lookup"><span data-stu-id="b2ad1-117">**3. Why do I get the following error message after I enter the input for the web service on the "Explore this dataset" page:**</span></span> 

<span data-ttu-id="b2ad1-118">**Une erreur inattendue s’est produite pendant le traitement de votre demande. Réessayez.**</span><span class="sxs-lookup"><span data-stu-id="b2ad1-118">**An unexpected error occurred while processing your request. Please try again.**</span></span>

<span data-ttu-id="b2ad1-119">Un ou plusieurs paramètres d’entrée de votre service web peuvent avoir dépassé la limite de longueur lors de la consommation du service web sur la page **Explorer ce jeu de données** de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-119">One or more input parameters of your web service may have exceeded the length limit when consuming the web service on the marketplace **Explore this dataset** page.</span></span> <span data-ttu-id="b2ad1-120">Les services peuvent être appelés avec une longueur d’entrée supérieure à l’aide de méthodes HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-120">The services can be called with a longer input length by using HTTP POST methods.</span></span> <span data-ttu-id="b2ad1-121">Pour obtenir des exemples, consultez la page [Exemples de solutions utilisant R sur Machine Learning et publiées sur Marketplace](machine-learning-r-csharp-web-service-examples.md).</span><span class="sxs-lookup"><span data-stu-id="b2ad1-121">For examples, see [Sample solutions using R on Machine Learning and published to Marketplace](machine-learning-r-csharp-web-service-examples.md).</span></span>

<span data-ttu-id="b2ad1-122">**4. Pourquoi l’onglet « EXPLORATEUR D’API » du magasin du portail Azure Classic est-il vide ?**</span><span class="sxs-lookup"><span data-stu-id="b2ad1-122">**4. Why do I not see anything in the "API EXPLORER" tab int the Store in the Azure Classic Portal?**</span></span> 

<span data-ttu-id="b2ad1-123">Il s’agit d’un problème connu sur Marketplace du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-123">This is a known issue with the Azure Classic Portal Marketplace.</span></span> <span data-ttu-id="b2ad1-124">Notre équipe travaille en ce moment à la résolution de ce problème.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-124">The team is working to resolve this issue.</span></span> 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a><span data-ttu-id="b2ad1-125">Questions relatives à la publication à partir d’Azure Machine Learning sur Marketplace</span><span class="sxs-lookup"><span data-stu-id="b2ad1-125">Questions about publishing from Azure Machine Learning on Marketplace</span></span>
<span data-ttu-id="b2ad1-126">**1. Pourquoi mes transactions de logos ou d’images ne s’actualisent-elles pas pour mon service web ?**</span><span class="sxs-lookup"><span data-stu-id="b2ad1-126">**1. Why are my transactions of logos or images not refreshing for my web service?**</span></span> 

<span data-ttu-id="b2ad1-127">Les logos et images sont mis en cache sur le portail de publication et cela peut prendre jusqu’à 10 jours avant que le nouveau logo ou la nouvelle image ne soit mis(e) à jour sur le portail.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-127">Logos and images are cached in the publishing portal, and it may take up to 10 days for the new logo or image to update on the portal.</span></span>

<span data-ttu-id="b2ad1-128">**2. Pourquoi l’onglet « Détail » de mon service web sur Marketplace affiche-t-il un message d’erreur ?**</span><span class="sxs-lookup"><span data-stu-id="b2ad1-128">**2. Why is the “Detail" tab of my web service on Marketplace showing an error message?**</span></span>

<span data-ttu-id="b2ad1-129">Un problème connu se produit sur Marketplace lorsque l’utilisateur se connecte à Azure Machine Learning pour obtenir des détails sur un service.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-129">There is a known Marketplace issue when connecting to Azure Machine Learning for service details.</span></span> <span data-ttu-id="b2ad1-130">Notre équipe travaille en ce moment à la résolution de ce problème.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-130">The team is working to resolve this issue.</span></span>

<span data-ttu-id="b2ad1-131">**3. Pourquoi l’exemple de code R dans les services web d’Azure Machine Learning ne permet-il pas de consommer les services web dans Marketplace ?**</span><span class="sxs-lookup"><span data-stu-id="b2ad1-131">**3. Why does the R sample code in the Azure Machine Learning web services not work for consuming the web services in Marketplace?**</span></span>

<span data-ttu-id="b2ad1-132">Les systèmes d’authentification sont différents lorsque vous vous connectez aux services web Azure Machine Learning directement ou lorsque vous vous y connectez via le Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-132">The authentication systems are different when connecting to Azure Machine Learning web services directly compared to connecting to these web services through the Marketplace.</span></span> <span data-ttu-id="b2ad1-133">Les services du Marketplace sont des services OData qui peuvent être appelés avec les méthodes GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-133">The services in Marketplace are OData services, and they can be called with GET or POST methods.</span></span> 

<span data-ttu-id="b2ad1-134">**4. Pourquoi les liens de support de mes offres de service web ne sont-ils pas correctement mis à jour pour certaines de mes offres ?**</span><span class="sxs-lookup"><span data-stu-id="b2ad1-134">**4. Why are the support links of my web service offers not updating correctly for some of my offers?**</span></span>

<span data-ttu-id="b2ad1-135">Les liens de support sont globaux par éditeur, non par offre.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-135">The support links are global per publisher, not per offer.</span></span> 

<span data-ttu-id="b2ad1-136">**5. Comment puis-je publier un service web avec le mode de saisie de lot sur Marketplace ?**</span><span class="sxs-lookup"><span data-stu-id="b2ad1-136">**5. How do I publish a web service with batch input mode in Marketplace?**</span></span>

<span data-ttu-id="b2ad1-137">Le mode de saisie de lot n'est actuellement pas pris en charge dans les services web Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-137">The batch input mode is currently not supported in Marketplace web services.</span></span>

<span data-ttu-id="b2ad1-138">**6. Qui dois-je contacter pour obtenir de l’aide si j’ai des questions sur la tâche d’éditeur de données ou si je rencontre des problèmes lors de la publication ?**</span><span class="sxs-lookup"><span data-stu-id="b2ad1-138">**6. Who should I contact to get help if I have questions about becoming a data publisher, or if I have issues during publishing?**</span></span>

<span data-ttu-id="b2ad1-139">Veuillez contacter l’équipe Azure Marketplace à l’adresse <mailto:datamarketbd@microsoft.com> pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="b2ad1-139">Please contact the Azure Marketplace team at <mailto:datamarketbd@microsoft.com> for more information.</span></span>

