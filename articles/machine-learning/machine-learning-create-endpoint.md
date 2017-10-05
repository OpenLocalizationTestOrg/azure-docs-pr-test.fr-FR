---
title: "Création de points de terminaison de service web dans Machine Learning | Microsoft Docs"
description: "Création de points de terminaison de service web dans Azure Machine Learning"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 9f83ffc9cf7dbe37c1ce9980fd7f5b9133fe78f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="7c71e-103">Création de points de terminaison</span><span class="sxs-lookup"><span data-stu-id="7c71e-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="7c71e-104">Cette rubrique décrit les techniques applicables à un service web Machine Learning **classique**.</span><span class="sxs-lookup"><span data-stu-id="7c71e-104">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="7c71e-105">Lorsque vous créez des services web que vous vendez à vos clients, vous devez fournir à ceux-ci des modèles formés qui restent liés à l’expérience à partir de laquelle le service web a été créé.</span><span class="sxs-lookup"><span data-stu-id="7c71e-105">When you create Web services that you sell forward to your customers, you need to provide trained models to each customer that are still linked to the experiment from which the Web service was created.</span></span> <span data-ttu-id="7c71e-106">En outre, des mises à jour de l’expérience peuvent être appliquées de façon sélective à un point de terminaison, sans remplacer les personnalisations.</span><span class="sxs-lookup"><span data-stu-id="7c71e-106">In addition, any updates to the experiment should be applied selectively to an endpoint without overwriting the customizations.</span></span>

<span data-ttu-id="7c71e-107">À cette fin, le Azure Machine Learning vous permet de créer plusieurs points de terminaison pour un service web déployé.</span><span class="sxs-lookup"><span data-stu-id="7c71e-107">To accomplish this, Azure Machine Learning allows you to create multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="7c71e-108">Chaque point de terminaison du service web est adressé, limité et géré de façon indépendante.</span><span class="sxs-lookup"><span data-stu-id="7c71e-108">Each endpoint in the Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="7c71e-109">Chaque point de terminaison est une URL unique, et la clé d’autorisation que vous pouvez distribuer à vos clients.</span><span class="sxs-lookup"><span data-stu-id="7c71e-109">Each endpoint is a unique URL and authorization key that you can distribute to your customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-to-a-web-service"></a><span data-ttu-id="7c71e-110">Ajout de points de terminaison à un service web</span><span class="sxs-lookup"><span data-stu-id="7c71e-110">Adding endpoints to a Web service</span></span>
<span data-ttu-id="7c71e-111">Il existe trois façons d’ajouter un point de terminaison à un service web.</span><span class="sxs-lookup"><span data-stu-id="7c71e-111">There are three ways to add an endpoint to a Web service.</span></span>

* <span data-ttu-id="7c71e-112">Par programmation</span><span class="sxs-lookup"><span data-stu-id="7c71e-112">Programmatically</span></span>
* <span data-ttu-id="7c71e-113">Via le portail des services web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7c71e-113">Through the Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="7c71e-114">Via le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="7c71e-114">Though the Azure classic portal</span></span>

<span data-ttu-id="7c71e-115">Une fois le point de terminaison créé, vous pouvez l’exploiter via des API synchrones, des API de lot et des feuilles de calcul Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="7c71e-115">Once the endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="7c71e-116">Outre l'ajout de points de terminaison via cette interface utilisateur, vous pouvez également utiliser les API de gestion de point de terminaison pour ajouter de manière programmée des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="7c71e-116">In addition to adding endpoints through this UI, you can also use the Endpoint Management APIs to programmatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="7c71e-117">Si vous avez ajouté des points de terminaison au service web, vous ne pouvez pas supprimer le point de terminaison par défaut.</span><span class="sxs-lookup"><span data-stu-id="7c71e-117">If you have added additional endpoints to the Web service, you cannot delete the default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="7c71e-118">Ajout d’un point de terminaison par programme</span><span class="sxs-lookup"><span data-stu-id="7c71e-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="7c71e-119">Vous pouvez ajouter un point de terminaison à votre service web par programme en utilisant l’exemple de code [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="7c71e-119">You can add an endpoint to your Web service programmatically using the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="7c71e-120">Ajout d’un point de terminaison à l’aide du portail des services web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7c71e-120">Adding an endpoint using the Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="7c71e-121">Dans Machine Learning Studio, dans la colonne de navigation de gauche, cliquez sur Services web.</span><span class="sxs-lookup"><span data-stu-id="7c71e-121">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="7c71e-122">En bas du tableau de bord du service web, cliquez sur **Gérer les points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="7c71e-122">At the bottom of the Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="7c71e-123">Le portail des services web Azure Machine Learning s’ouvre sur la page des points de terminaison pour le service web.</span><span class="sxs-lookup"><span data-stu-id="7c71e-123">The Azure Machine Learning Web Services portal opens to the endpoints page for the Web service.</span></span>
3. <span data-ttu-id="7c71e-124">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="7c71e-124">Click **New**.</span></span>
4. <span data-ttu-id="7c71e-125">Tapez un nom et une description pour le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="7c71e-125">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="7c71e-126">Les noms de point de terminaison doivent compter au maximum 24 caractères, et doivent être composés de lettres minuscules ou de chiffres.</span><span class="sxs-lookup"><span data-stu-id="7c71e-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="7c71e-127">Sélectionnez le niveau de journalisation et activez les exemples de données si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7c71e-127">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="7c71e-128">Pour plus d’informations sur la journalisation, voir [Activation de la journalisation pour les services web Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="7c71e-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-the-azure-classic-portal"></a><span data-ttu-id="7c71e-129">Ajout d’un point de terminaison via le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="7c71e-129">Adding an endpoint using the Azure classic portal</span></span>
1. <span data-ttu-id="7c71e-130">Connectez-vous au [portail Azure Classic](http://manage.windowsazure.com), puis cliquez sur **Machine Learning** dans la colonne de gauche.</span><span class="sxs-lookup"><span data-stu-id="7c71e-130">Sign in to the [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in the left column.</span></span> <span data-ttu-id="7c71e-131">Cliquez sur l’espace de travail contenant le service web qui vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="7c71e-131">Click the workspace which contains the Web service in which you are interested.</span></span>
   
    ![Accès à l’espace de travail](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="7c71e-133">Cliquez sur **Services web**.</span><span class="sxs-lookup"><span data-stu-id="7c71e-133">Click **Web Services**.</span></span>
   
    ![Accéder aux services web](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="7c71e-135">Cliquez sur le service web qui vous intéresse pour afficher la liste des points de terminaison disponibles.</span><span class="sxs-lookup"><span data-stu-id="7c71e-135">Click the Web service you're interested in to see the list of available endpoints.</span></span>
   
    ![Accès au point de terminaison](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="7c71e-137">En bas de la page, cliquez sur **Ajouter un point de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="7c71e-137">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="7c71e-138">Tapez un nom et une description, en vérifiant qu’il n’existe aucun point de terminaison du même nom dans ce service web.</span><span class="sxs-lookup"><span data-stu-id="7c71e-138">Type a name and description, ensure there are no other endpoints with the same name in this Web service.</span></span> <span data-ttu-id="7c71e-139">Conservez le niveau de limitation défini par défaut, sauf si vous avez des exigences particulières.</span><span class="sxs-lookup"><span data-stu-id="7c71e-139">Leave the throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="7c71e-140">Pour en savoir plus sur la limitation, voir [Mise à l’échelle de points de terminaison des API](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="7c71e-140">To learn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Création d’un point de terminaison](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="7c71e-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c71e-142">Next Steps</span></span>
<span data-ttu-id="7c71e-143">[Utilisation d’un service web Azure Machine Learning déployé à partir d’une expérience Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="7c71e-143">[How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

