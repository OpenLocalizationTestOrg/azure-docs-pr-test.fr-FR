---
title: "points de terminaison du service aaaCreating Web dans l’apprentissage | Documents Microsoft"
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
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="606e4-103">Création de points de terminaison</span><span class="sxs-lookup"><span data-stu-id="606e4-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="606e4-104">Cette rubrique décrit les techniques des tooa applicable **classique** service Machine Learning Web.</span><span class="sxs-lookup"><span data-stu-id="606e4-104">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="606e4-105">Lorsque vous créez des services Web qui vendent des clients de tooyour vers l’avant, vous devez tooprovide modèles formés tooeach client expérience toohello toujours lié à partir de quels hello Web service a été créé.</span><span class="sxs-lookup"><span data-stu-id="606e4-105">When you create Web services that you sell forward tooyour customers, you need tooprovide trained models tooeach customer that are still linked toohello experiment from which hello Web service was created.</span></span> <span data-ttu-id="606e4-106">En outre, les mises à jour toohello expérience doit-elle être appliquent de manière sélective tooan le point de terminaison sans remplacer les personnalisations hello.</span><span class="sxs-lookup"><span data-stu-id="606e4-106">In addition, any updates toohello experiment should be applied selectively tooan endpoint without overwriting hello customizations.</span></span>

<span data-ttu-id="606e4-107">tooaccomplish, Azure Machine Learning vous permet de toocreate plusieurs points de terminaison pour un service Web déployé.</span><span class="sxs-lookup"><span data-stu-id="606e4-107">tooaccomplish this, Azure Machine Learning allows you toocreate multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="606e4-108">Chaque point de terminaison de service Web de hello est indépendamment adressé limitée et géré.</span><span class="sxs-lookup"><span data-stu-id="606e4-108">Each endpoint in hello Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="606e4-109">Chaque point de terminaison est une clé unique d’URL et d’autorisation que vous pouvez distribuer tooyour clients.</span><span class="sxs-lookup"><span data-stu-id="606e4-109">Each endpoint is a unique URL and authorization key that you can distribute tooyour customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a><span data-ttu-id="606e4-110">Ajout de service Web de tooa points de terminaison</span><span class="sxs-lookup"><span data-stu-id="606e4-110">Adding endpoints tooa Web service</span></span>
<span data-ttu-id="606e4-111">Il existe trois façons tooadd un tooa de point de terminaison service Web.</span><span class="sxs-lookup"><span data-stu-id="606e4-111">There are three ways tooadd an endpoint tooa Web service.</span></span>

* <span data-ttu-id="606e4-112">Par programmation</span><span class="sxs-lookup"><span data-stu-id="606e4-112">Programmatically</span></span>
* <span data-ttu-id="606e4-113">Via le portail de Services Web de Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="606e4-113">Through hello Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="606e4-114">Bien que hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="606e4-114">Though hello Azure classic portal</span></span>

<span data-ttu-id="606e4-115">Une fois que le point de terminaison hello est créé, vous pouvez consommer via les API synchrones, lot API et feuilles de calcul excel.</span><span class="sxs-lookup"><span data-stu-id="606e4-115">Once hello endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="606e4-116">En outre tooadding les points de terminaison via cette interface utilisateur, vous pouvez également utiliser hello API de gestion de point de terminaison tooprogrammatically ajouter des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="606e4-116">In addition tooadding endpoints through this UI, you can also use hello Endpoint Management APIs tooprogrammatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="606e4-117">Si vous avez ajouté des points de terminaison supplémentaires toohello service Web, vous ne pouvez pas supprimer le point de terminaison par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="606e4-117">If you have added additional endpoints toohello Web service, you cannot delete hello default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="606e4-118">Ajout d’un point de terminaison par programme</span><span class="sxs-lookup"><span data-stu-id="606e4-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="606e4-119">Vous pouvez ajouter un point de terminaison tooyour Web service par programme hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) exemple de code.</span><span class="sxs-lookup"><span data-stu-id="606e4-119">You can add an endpoint tooyour Web service programmatically using hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="606e4-120">Ajout d’un point de terminaison à l’aide du portail de Services Web de Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="606e4-120">Adding an endpoint using hello Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="606e4-121">Dans Machine Learning Studio, sur la colonne du volet de navigation gauche hello, cliquez sur les Services Web.</span><span class="sxs-lookup"><span data-stu-id="606e4-121">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="606e4-122">Au bas de hello du tableau de bord de service Web hello, cliquez sur **gérer les points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="606e4-122">At hello bottom of hello Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="606e4-123">portail de Services Web de Azure Machine Learning Hello ouvre la page de points de terminaison de toohello pourquoi le service Web.</span><span class="sxs-lookup"><span data-stu-id="606e4-123">hello Azure Machine Learning Web Services portal opens toohello endpoints page for hello Web service.</span></span>
3. <span data-ttu-id="606e4-124">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="606e4-124">Click **New**.</span></span>
4. <span data-ttu-id="606e4-125">Tapez un nom et une description pour le nouveau point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="606e4-125">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="606e4-126">Les noms de point de terminaison doivent compter au maximum 24 caractères, et doivent être composés de lettres minuscules ou de chiffres.</span><span class="sxs-lookup"><span data-stu-id="606e4-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="606e4-127">Sélectionnez le niveau de journalisation hello et indique si les exemples de données sont activées.</span><span class="sxs-lookup"><span data-stu-id="606e4-127">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="606e4-128">Pour plus d’informations sur la journalisation, voir [Activation de la journalisation pour les services web Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="606e4-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a><span data-ttu-id="606e4-129">Ajout d’un point de terminaison à l’aide de hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="606e4-129">Adding an endpoint using hello Azure classic portal</span></span>
1. <span data-ttu-id="606e4-130">Connectez-vous à toohello [portail Azure classic](http://manage.windowsazure.com), cliquez sur **Machine Learning** dans la colonne de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="606e4-130">Sign in toohello [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in hello left column.</span></span> <span data-ttu-id="606e4-131">Cliquez sur espace de travail hello qui contient le service Web de hello qui vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="606e4-131">Click hello workspace which contains hello Web service in which you are interested.</span></span>
   
    ![Accédez tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="606e4-133">Cliquez sur **Services web**.</span><span class="sxs-lookup"><span data-stu-id="606e4-133">Click **Web Services**.</span></span>
   
    ![Accédez tooWeb services](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="606e4-135">Cliquez sur le service Web de hello vous intéresse dans la liste de hello toosee de points de terminaison disponibles.</span><span class="sxs-lookup"><span data-stu-id="606e4-135">Click hello Web service you're interested in toosee hello list of available endpoints.</span></span>
   
    ![Accédez tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="606e4-137">Au bas de hello de page de hello, cliquez sur **ajouter le point de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="606e4-137">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="606e4-138">Tapez un nom et une description, vérifiez qu’aucun autre point de terminaison avec le même nom dans ce service Web de hello.</span><span class="sxs-lookup"><span data-stu-id="606e4-138">Type a name and description, ensure there are no other endpoints with hello same name in this Web service.</span></span> <span data-ttu-id="606e4-139">Laissez le niveau de limitation de bande passante de hello avec sa valeur par défaut, sauf si vous avez des spécifications spéciales.</span><span class="sxs-lookup"><span data-stu-id="606e4-139">Leave hello throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="606e4-140">toolearn en savoir plus sur la limitation, consultez [API points de terminaison de mise à l’échelle](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="606e4-140">toolearn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Création d’un point de terminaison](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="606e4-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="606e4-142">Next Steps</span></span>
<span data-ttu-id="606e4-143">[Comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="606e4-143">[How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

