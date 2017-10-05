---
title: "Reformer un modèle Machine Learning | Microsoft Docs"
description: "Apprenez à reformer un modèle et à mettre à jour le service web pour utiliser le modèle reformé dans Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: f86c2bc41dd7ff0bc31454a56b84d136dc7d026c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="24ce3-103">Reformer un modèle Machine Learning</span><span class="sxs-lookup"><span data-stu-id="24ce3-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="24ce3-104">Dans le cadre du processus de mise en œuvre opérationnelle des modèles d’apprentissage automatique d’Azure Machine Learning, votre modèle est entraîné et enregistré.</span><span class="sxs-lookup"><span data-stu-id="24ce3-104">As part of the process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="24ce3-105">Vous l’utilisez ensuite pour créer un service web prédictif.</span><span class="sxs-lookup"><span data-stu-id="24ce3-105">You then use it to create a predicative Web service.</span></span> <span data-ttu-id="24ce3-106">Le service web peut ensuite être utilisé dans des sites web, des tableaux de bord et des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="24ce3-106">The Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="24ce3-107">Les modèles que vous créez à l’aide de Machine Learning ne sont généralement pas statiques.</span><span class="sxs-lookup"><span data-stu-id="24ce3-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="24ce3-108">Lorsque de nouvelles données sont disponibles ou lorsque le consommateur de l’API a ses propres données, il faut effectuer à nouveau l’apprentissage du modèle.</span><span class="sxs-lookup"><span data-stu-id="24ce3-108">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span> 

<span data-ttu-id="24ce3-109">Il peut être très fréquent d’avoir à effectuer à nouveau l’apprentissage du modèle.</span><span class="sxs-lookup"><span data-stu-id="24ce3-109">Retraining may occur frequently.</span></span> <span data-ttu-id="24ce3-110">Avec la fonctionnalité d’API Programmatic Retraining, vous pouvez reformer le modèle par programmation à l’aide des API Retraining et mettre à jour le service web avec le modèle reformé.</span><span class="sxs-lookup"><span data-stu-id="24ce3-110">With the Programmatic Retraining API feature, you can programmatically retrain the model using the Retraining APIs and update the Web service with the newly trained model.</span></span> 

<span data-ttu-id="24ce3-111">Ce document décrit le processus de nouvel apprentissage et vous montre comment utiliser les API Retraining.</span><span class="sxs-lookup"><span data-stu-id="24ce3-111">This document describes the retraining process, and shows you how to use the Retraining APIs.</span></span>

## <a name="why-retrain-defining-the-problem"></a><span data-ttu-id="24ce3-112">Les raisons de la reformation : définition du problème</span><span class="sxs-lookup"><span data-stu-id="24ce3-112">Why retrain: defining the problem</span></span>
<span data-ttu-id="24ce3-113">Dans le cadre du processus de formation Machine Learning, un modèle est formé à l’aide d’un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="24ce3-113">As part of the machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="24ce3-114">Les modèles que vous créez à l’aide de Machine Learning ne sont généralement pas statiques.</span><span class="sxs-lookup"><span data-stu-id="24ce3-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="24ce3-115">Lorsque de nouvelles données sont disponibles ou lorsque le consommateur de l’API a ses propres données, il faut effectuer à nouveau l’apprentissage du modèle.</span><span class="sxs-lookup"><span data-stu-id="24ce3-115">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span>

<span data-ttu-id="24ce3-116">Dans ces scénarios, une API par programme offre un moyen pratique pour vous ou les utilisateurs de vos API de créer un client qui peut, à titre exceptionnel ou de manière régulière, reformer le modèle à l’aide de ses propres données.</span><span class="sxs-lookup"><span data-stu-id="24ce3-116">In these scenarios, a programmatic API provides a convenient way to allow you or the consumer of your APIs to create a client that can, on a one-time or regular basis, retrain the model using their own data.</span></span> <span data-ttu-id="24ce3-117">Il est alors possible d’évaluer les résultats de la reformation et de mettre à jour l’API du service web de sorte qu’elle utilise le modèle reformé.</span><span class="sxs-lookup"><span data-stu-id="24ce3-117">They can then evaluate the results of retraining, and update the Web service API to use the newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="24ce3-118">Si vous avez une expérience de formation existante et un nouveau service web, vous pouvez consulter la section Reformer un service web prédictif existant au lieu de suivre la procédure pas à pas décrite dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="24ce3-118">If you have an existing Training Experiment and New Web service, you may want to check out Retrain an existing Predictive Web service instead of following the walkthrough mentioned in the following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="24ce3-119">Workflow de bout en bout</span><span class="sxs-lookup"><span data-stu-id="24ce3-119">End-to-end workflow</span></span>
<span data-ttu-id="24ce3-120">Le processus implique les éléments suivants : une expérience de formation et une expérience prédictive publiées en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="24ce3-120">The process involves the following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="24ce3-121">Pour permettre la reformation d’un modèle, l’expérience de formation doit être publiée en tant que service web avec la sortie d’un modèle formé.</span><span class="sxs-lookup"><span data-stu-id="24ce3-121">To enable retraining of a trained model, the Training Experiment must be published as a Web service with the output of a trained model.</span></span> <span data-ttu-id="24ce3-122">Cela permet à l’API d’accéder au modèle en vue de la reformation.</span><span class="sxs-lookup"><span data-stu-id="24ce3-122">This enables API access to the model for retraining.</span></span> 

<span data-ttu-id="24ce3-123">Les étapes suivantes s’appliquent aux services web nouveaux et classiques :</span><span class="sxs-lookup"><span data-stu-id="24ce3-123">The following steps apply to both New and Classic Web services:</span></span>

<span data-ttu-id="24ce3-124">Créez le service web prédictif initial :</span><span class="sxs-lookup"><span data-stu-id="24ce3-124">Create the initial Predictive Web service:</span></span>

* <span data-ttu-id="24ce3-125">Créez une expérience d'apprentissage</span><span class="sxs-lookup"><span data-stu-id="24ce3-125">Create a training experiment</span></span>
* <span data-ttu-id="24ce3-126">Créez une expérience prédictive</span><span class="sxs-lookup"><span data-stu-id="24ce3-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="24ce3-127">Déployez un service web prédictif</span><span class="sxs-lookup"><span data-stu-id="24ce3-127">Deploy a predictive web service</span></span>

<span data-ttu-id="24ce3-128">Reformez le service web :</span><span class="sxs-lookup"><span data-stu-id="24ce3-128">Retrain the Web service:</span></span>

* <span data-ttu-id="24ce3-129">Mettez à jour l’expérience de formation pour permettre la reformation</span><span class="sxs-lookup"><span data-stu-id="24ce3-129">Update training experiment to allow for retraining</span></span>
* <span data-ttu-id="24ce3-130">Déployez le service web de reformation</span><span class="sxs-lookup"><span data-stu-id="24ce3-130">Deploy the retraining web service</span></span>
* <span data-ttu-id="24ce3-131">Utilisez le code de service d’exécution de lot pour reformer le modèle</span><span class="sxs-lookup"><span data-stu-id="24ce3-131">Use the Batch Execution Service code to retrain the model</span></span>

<span data-ttu-id="24ce3-132">Pour une présentation détaillée des précédentes étapes, voir [Reformation des modèles Machine Learning par programme](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="24ce3-132">For a walkthrough of the preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="24ce3-133">Pour déployer un nouveau service web, vous devez disposer d’autorisations suffisantes dans l’abonnement dans lequel déployer le service web.</span><span class="sxs-lookup"><span data-stu-id="24ce3-133">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="24ce3-134">Pour en savoir plus, consultez la rubrique [Gérer un service web à l’aide du portail des services web Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="24ce3-134">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="24ce3-135">Si vous avez déployé un service web classique :</span><span class="sxs-lookup"><span data-stu-id="24ce3-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="24ce3-136">Créer un point de terminaison sur le service web prédictif</span><span class="sxs-lookup"><span data-stu-id="24ce3-136">Create a new Endpoint on the Predictive Web service</span></span>
* <span data-ttu-id="24ce3-137">Obtenez l’URL et le code du CORRECTIF</span><span class="sxs-lookup"><span data-stu-id="24ce3-137">Get the PATCH URL and code</span></span>
* <span data-ttu-id="24ce3-138">Utilisez l’URL du CORRECTIF pour faire pointer le nouveau point de terminaison sur le modèle reformé</span><span class="sxs-lookup"><span data-stu-id="24ce3-138">Use the PATCH URL to point the new Endpoint at the retrained model</span></span> 

<span data-ttu-id="24ce3-139">Pour une présentation détaillée des précédentes étapes, voir [Reformer un service web classique](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="24ce3-139">For a walkthrough of the preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="24ce3-140">Si vous rencontrez des difficultés pour reformer un service web classique, voir [Dépannage de la reformation d’un service web classique Azure Machine Learning](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="24ce3-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting the retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="24ce3-141">Si vous avez déployé un nouveau service web :</span><span class="sxs-lookup"><span data-stu-id="24ce3-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="24ce3-142">Connectez-vous à votre compte Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="24ce3-142">Sign in to your Azure Resource Manager account</span></span>
* <span data-ttu-id="24ce3-143">Obtenez la définition du service web</span><span class="sxs-lookup"><span data-stu-id="24ce3-143">Get the Web service definition</span></span>
* <span data-ttu-id="24ce3-144">Exportez la définition du service web au format JSON</span><span class="sxs-lookup"><span data-stu-id="24ce3-144">Export the Web Service Definition as JSON</span></span>
* <span data-ttu-id="24ce3-145">Mettez à jour la référence à l’objet blob `ilearner` dans le JSON</span><span class="sxs-lookup"><span data-stu-id="24ce3-145">Update the reference to the `ilearner` blob in the JSON</span></span>
* <span data-ttu-id="24ce3-146">Importez le JSON dans une définition du service web</span><span class="sxs-lookup"><span data-stu-id="24ce3-146">Import the JSON into a Web Service Definition</span></span>
* <span data-ttu-id="24ce3-147">Mettez à jour le service web avec la nouvelle définition du service web</span><span class="sxs-lookup"><span data-stu-id="24ce3-147">Update the Web service with new Web Service Definition</span></span>

<span data-ttu-id="24ce3-148">Pour une présentation détaillée des étapes précédentes, voir [Reformer un nouveau service web à l’aide des applets de commande PowerShell de gestion de Machine Learning](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="24ce3-148">For a walkthrough of the preceding steps, see [Retrain a New Web service using the Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="24ce3-149">Le processus de configuration de la reformation pour un service web classique implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="24ce3-149">The process for setting up retraining for a Classic Web service involves the following steps:</span></span>

![Présentation du processus de nouvel apprentissage.][1]

<span data-ttu-id="24ce3-151">Le processus de configuration de la reformation pour un nouveau service web implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="24ce3-151">The process for setting up retraining for a New Web service involves the following steps:</span></span>

![Présentation du processus de nouvel apprentissage.][7]

## <a name="other-resources"></a><span data-ttu-id="24ce3-153">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="24ce3-153">Other Resources</span></span>
* [<span data-ttu-id="24ce3-154">Reformation et mise à jour de modèles Microsoft Azure Machine Learning avec Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="24ce3-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span></span>](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [<span data-ttu-id="24ce3-155">Créer de nombreux modèles Machine Learning et points de terminaison de service web à partir d’une expérience à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="24ce3-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="24ce3-156">La vidéo [Modèles de reformation AML utilisant des API](https://www.youtube.com/watch?v=wwjglA8xllg) montre comment reformer des modèles Machine Learning créés dans Azure Machine Learning en utilisant les API de reformation et PowerShell.</span><span class="sxs-lookup"><span data-stu-id="24ce3-156">The [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how to retrain Machine Learning models created in Azure Machine Learning using the Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

