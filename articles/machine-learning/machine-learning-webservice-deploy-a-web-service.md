---
title: "Déploiement d’un nouveau service web dans Azure Machine Learning | Microsoft Docs"
description: "Flux de travail du déploiement d’un service web basé sur ARM"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: TRUE
ms.openlocfilehash: 1415709f9da2bb2cce859af9feb0ec15c1fa5801
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="a49ca-103">Déployer comme un nouveau service web</span><span class="sxs-lookup"><span data-stu-id="a49ca-103">Deploy a new web service</span></span>
<span data-ttu-id="a49ca-104">Microsoft Azure Machine Learning fournit désormais des services web basés sur [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) permettant de choisir de nouvelles options de plan de facturation et de déployer votre service web dans plusieurs régions.</span><span class="sxs-lookup"><span data-stu-id="a49ca-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service to multiple regions.</span></span>

<span data-ttu-id="a49ca-105">Le flux de travail général pour déployer un service web à l’aide des services web Microsoft Azure Machine Learning est le suivant :</span><span class="sxs-lookup"><span data-stu-id="a49ca-105">The general workflow to deploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="a49ca-106">Créer une expérience prédictive</span><span class="sxs-lookup"><span data-stu-id="a49ca-106">Create a predictive experiment</span></span>
* <span data-ttu-id="a49ca-107">la déployer</span><span class="sxs-lookup"><span data-stu-id="a49ca-107">deploy it</span></span>
* <span data-ttu-id="a49ca-108">choisir son nom</span><span class="sxs-lookup"><span data-stu-id="a49ca-108">configure its name</span></span>
* <span data-ttu-id="a49ca-109">profil de facturation</span><span class="sxs-lookup"><span data-stu-id="a49ca-109">billing plan</span></span>
* <span data-ttu-id="a49ca-110">la tester</span><span class="sxs-lookup"><span data-stu-id="a49ca-110">test it</span></span>
* <span data-ttu-id="a49ca-111">l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="a49ca-111">consume it.</span></span>

<span data-ttu-id="a49ca-112">La figure suivante illustre ce flux de travail.</span><span class="sxs-lookup"><span data-stu-id="a49ca-112">The following graphic illustrates the workflow.</span></span>

![Flux de travail du déploiement d’un service web][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="a49ca-114">Déployer un service web à partir de Studio</span><span class="sxs-lookup"><span data-stu-id="a49ca-114">Deploy web service from Studio</span></span>
<span data-ttu-id="a49ca-115">Pour déployer une expérience en tant que nouveau service web.</span><span class="sxs-lookup"><span data-stu-id="a49ca-115">To deploy an experiment as a new web service.</span></span> <span data-ttu-id="a49ca-116">Connectez-vous à Machine Learning Studio et créez un nouveau service web prédictif.</span><span class="sxs-lookup"><span data-stu-id="a49ca-116">Sign into the Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="a49ca-117">**Remarque**: si vous avez déjà déployé une expérience en tant que service web classique, vous ne pouvez pas le déployer en tant que nouveau service web.</span><span class="sxs-lookup"><span data-stu-id="a49ca-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="a49ca-118">Cliquez sur **Exécuter** en bas du canevas de l’expérience, puis sur **Déployer le service web** et **Déployer le service web [nouveau]**.</span><span class="sxs-lookup"><span data-stu-id="a49ca-118">Click **Run** at the bottom of the experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="a49ca-119">La page de déploiement du Gestionnaire de service web Machine Learning s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="a49ca-119">The deployment page of the Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="a49ca-120">Page d’expérience de déploiement du Gestionnaire de service web Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a49ca-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="a49ca-121">Sur la page de l’expérience de déploiement, entrez le nom du service web.</span><span class="sxs-lookup"><span data-stu-id="a49ca-121">On the Deploy Experiment page, enter a name for the web service.</span></span>
<span data-ttu-id="a49ca-122">Sélectionnez un plan de tarification.</span><span class="sxs-lookup"><span data-stu-id="a49ca-122">Select a pricing plan.</span></span> <span data-ttu-id="a49ca-123">Si vous disposez d’un plan de tarification existant, vous pouvez le sélectionner. Sinon, vous devez créer un nouveau plan de tarification pour le service.</span><span class="sxs-lookup"><span data-stu-id="a49ca-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for the service.</span></span> 

1. <span data-ttu-id="a49ca-124">Dans la liste déroulante **Plan tarifaire**, sélectionnez un plan existant ou choisissez l’option **Select new plan** (Sélectionner un nouveau plan).</span><span class="sxs-lookup"><span data-stu-id="a49ca-124">In the **Price Plan** drop down, select an existing plan or select the **Select new plan** option.</span></span>
2. <span data-ttu-id="a49ca-125">Dans **Plan Name**, (Nom du plan), tapez un nom qui identifiera le plan sur votre facture.</span><span class="sxs-lookup"><span data-stu-id="a49ca-125">In **Plan Name**, type a name that will identify the plan on your bill.</span></span>
3. <span data-ttu-id="a49ca-126">Sélectionnez un des **niveaux de plans mensuels**.</span><span class="sxs-lookup"><span data-stu-id="a49ca-126">Select one of the **Monthly Plan Tiers**.</span></span> <span data-ttu-id="a49ca-127">Notez que les niveaux de plan s’appliquent par défaut aux plans de votre région et que votre service web est déployé dans cette région.</span><span class="sxs-lookup"><span data-stu-id="a49ca-127">Note that the plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

<span data-ttu-id="a49ca-128">Cliquez sur **Déployer** pour ouvrir la page Démarrage rapide de votre service web.</span><span class="sxs-lookup"><span data-stu-id="a49ca-128">Click **Deploy** and the Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="a49ca-129">Page Démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="a49ca-129">Quickstart page</span></span>
<span data-ttu-id="a49ca-130">La page Démarrage rapide du service web vous donne accès et vous fournit des conseils sur les tâches les plus courantes que vous allez effectuer après la création d’un nouveau service web.</span><span class="sxs-lookup"><span data-stu-id="a49ca-130">The web service Quickstart page gives you access and guidance on the most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="a49ca-131">À partir de là, vous pouvez facilement accéder à la fois à la page **Test** et à la page **Utiliser**.</span><span class="sxs-lookup"><span data-stu-id="a49ca-131">From here you can easily access both the **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="a49ca-132">Test de votre service web</span><span class="sxs-lookup"><span data-stu-id="a49ca-132">Testing your web service</span></span>
<span data-ttu-id="a49ca-133">Dans la page Démarrage rapide, cliquez sur Tester le service web dans la section sur les tâches courantes.</span><span class="sxs-lookup"><span data-stu-id="a49ca-133">From the Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="a49ca-134">Pour tester le service web en tant que service de requête-réponse (RRS) :</span><span class="sxs-lookup"><span data-stu-id="a49ca-134">To test the web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="a49ca-135">Cliquez sur **Test** dans la barre de menus.</span><span class="sxs-lookup"><span data-stu-id="a49ca-135">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="a49ca-136">Cliquez sur **Request-Response**(Requête-réponse).</span><span class="sxs-lookup"><span data-stu-id="a49ca-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="a49ca-137">Entrez les valeurs appropriées pour les colonnes d’entrée de votre expérience.</span><span class="sxs-lookup"><span data-stu-id="a49ca-137">Enter appropriate values for the input columns of your experiment.</span></span>
* <span data-ttu-id="a49ca-138">Cliquez sur Tester **requête-réponse**.</span><span class="sxs-lookup"><span data-stu-id="a49ca-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="a49ca-139">Vos résultats apparaîtront sur le côté droit de la page.</span><span class="sxs-lookup"><span data-stu-id="a49ca-139">You results will display on the right hand side of the page.</span></span>

<span data-ttu-id="a49ca-140">Pour tester un service web d’exécution de lots (BES), vous utiliserez un fichier CSV :</span><span class="sxs-lookup"><span data-stu-id="a49ca-140">To test a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="a49ca-141">Cliquez sur **Test** dans la barre de menus.</span><span class="sxs-lookup"><span data-stu-id="a49ca-141">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="a49ca-142">Cliquez sur **Lot**.</span><span class="sxs-lookup"><span data-stu-id="a49ca-142">Click **Batch**.</span></span>
* <span data-ttu-id="a49ca-143">Sous votre entrée, cliquez sur Parcourir et accédez à votre fichier de données d’exemple.</span><span class="sxs-lookup"><span data-stu-id="a49ca-143">Under your input, click Browse and navigate to your sample data file.</span></span>
* <span data-ttu-id="a49ca-144">Cliquez sur **Test**.</span><span class="sxs-lookup"><span data-stu-id="a49ca-144">Click **Test**.</span></span>

<span data-ttu-id="a49ca-145">L’état de votre test s’affiche sous **Test Batch Jobs**(Tâches de test de traitement par lots).</span><span class="sxs-lookup"><span data-stu-id="a49ca-145">The status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="a49ca-146">Utilisation de votre service web</span><span class="sxs-lookup"><span data-stu-id="a49ca-146">Consuming your Web Service</span></span>
<span data-ttu-id="a49ca-147">Lors de leur déploiement en tant que services web, les expériences Azure Machine Learning proposent une API REST, qui peut être exploitée par divers périphériques et plateformes.</span><span class="sxs-lookup"><span data-stu-id="a49ca-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="a49ca-148">En effet, l’API REST, très simple, accepte et répond au moyen de messages présentant le format JSON.</span><span class="sxs-lookup"><span data-stu-id="a49ca-148">This is because the simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="a49ca-149">Le portail Microsoft Azure Machine Learning propose du code que vous pouvez utiliser pour appeler le service web, en R, C# et Python.</span><span class="sxs-lookup"><span data-stu-id="a49ca-149">The Azure Machine Learning portal provides code that can be used to call the web service in R, C#, and Python.</span></span>

<span data-ttu-id="a49ca-150">Sur la page d’utilisation, vous trouverez :</span><span class="sxs-lookup"><span data-stu-id="a49ca-150">On the Consuming page you can find:</span></span>

* <span data-ttu-id="a49ca-151">La clé API et l’URI pour utiliser le service web dans les applications.</span><span class="sxs-lookup"><span data-stu-id="a49ca-151">The API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="a49ca-152">Des modèles d’application web et Excel pour démarrer le processus d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="a49ca-152">Excel and web app templates to kick start your consumption process.</span></span>
* <span data-ttu-id="a49ca-153">Un exemple de code en langage C#, python et R pour commencer.</span><span class="sxs-lookup"><span data-stu-id="a49ca-153">Sample code in C#, python, and R to get you started.</span></span>

<span data-ttu-id="a49ca-154">Pour plus d’informations sur l’utilisation de services web, voir [Utilisation d’un service web Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="a49ca-154">For more information on consuming web services, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a49ca-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a49ca-155">Next Steps</span></span>
<span data-ttu-id="a49ca-156">Pour plus d’informations sur l’utilisation des services web, consultez :</span><span class="sxs-lookup"><span data-stu-id="a49ca-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="a49ca-157">Utilisation d’un service web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a49ca-157">How to consume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="a49ca-158">Services web Azure Machine Learning : déploiement et consommation</span><span class="sxs-lookup"><span data-stu-id="a49ca-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
