---
title: "un modèle d’apprentissage automatique d’aaaRetrain | Documents Microsoft"
description: "Découvrez comment tooretrain un modèle et mise à jour hello Web service toouse hello qui vient d’être formé dans Azure Machine Learning."
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
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="e59c2-103">Reformer un modèle Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e59c2-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="e59c2-104">Dans le cadre du processus de hello d’une Opérationnalisation rapides des modèles d’apprentissage automatique dans Azure Machine Learning, votre modèle est formé et enregistré.</span><span class="sxs-lookup"><span data-stu-id="e59c2-104">As part of hello process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="e59c2-105">Vous utiliser toocreate un service Web predicative.</span><span class="sxs-lookup"><span data-stu-id="e59c2-105">You then use it toocreate a predicative Web service.</span></span> <span data-ttu-id="e59c2-106">Hello service Web peut ensuite être consommé dans les sites web, des tableaux de bord et des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="e59c2-106">hello Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="e59c2-107">Les modèles que vous créez à l’aide de Machine Learning ne sont généralement pas statiques.</span><span class="sxs-lookup"><span data-stu-id="e59c2-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="e59c2-108">Comme de nouvelles données sont disponibles ou lorsque le consommateur hello Hello API a son propre modèle de hello de données doit toobe reformé.</span><span class="sxs-lookup"><span data-stu-id="e59c2-108">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span> 

<span data-ttu-id="e59c2-109">Il peut être très fréquent d’avoir à effectuer à nouveau l’apprentissage du modèle.</span><span class="sxs-lookup"><span data-stu-id="e59c2-109">Retraining may occur frequently.</span></span> <span data-ttu-id="e59c2-110">Par programme avec la fonctionnalité de programmation API réapprentissage hello, recycler modèle hello utilisation hello API de réapprentissage et de mise à jour hello Web service avec des qui vient d’être formé hello.</span><span class="sxs-lookup"><span data-stu-id="e59c2-110">With hello Programmatic Retraining API feature, you can programmatically retrain hello model using hello Retraining APIs and update hello Web service with hello newly trained model.</span></span> 

<span data-ttu-id="e59c2-111">Ce document décrit les hello recyclage de processus et vous montre comment toouse hello réapprentissage des API.</span><span class="sxs-lookup"><span data-stu-id="e59c2-111">This document describes hello retraining process, and shows you how toouse hello Retraining APIs.</span></span>

## <a name="why-retrain-defining-hello-problem"></a><span data-ttu-id="e59c2-112">Pourquoi recycler : définition hello problème</span><span class="sxs-lookup"><span data-stu-id="e59c2-112">Why retrain: defining hello problem</span></span>
<span data-ttu-id="e59c2-113">Dans le cadre de l’apprentissage hello processus d’apprentissage, un modèle est formé à l’aide d’un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="e59c2-113">As part of hello machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="e59c2-114">Les modèles que vous créez à l’aide de Machine Learning ne sont généralement pas statiques.</span><span class="sxs-lookup"><span data-stu-id="e59c2-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="e59c2-115">Comme de nouvelles données sont disponibles ou lorsque le consommateur hello Hello API a son propre modèle de hello de données doit toobe reformé.</span><span class="sxs-lookup"><span data-stu-id="e59c2-115">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span>

<span data-ttu-id="e59c2-116">Dans ces scénarios, une API de programmation fournit un moyen pratique de tooallow vous ou hello consommateur de votre toocreate API un client qui peut, sur une base ponctuelle ou régulière, recycler modèle hello à l’aide de leurs propres données.</span><span class="sxs-lookup"><span data-stu-id="e59c2-116">In these scenarios, a programmatic API provides a convenient way tooallow you or hello consumer of your APIs toocreate a client that can, on a one-time or regular basis, retrain hello model using their own data.</span></span> <span data-ttu-id="e59c2-117">Ils peuvent évaluer les résultats de hello de recyclage puis hello Web service API toouse hello qui vient d’être formé de mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="e59c2-117">They can then evaluate hello results of retraining, and update hello Web service API toouse hello newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="e59c2-118">Si vous avez une expérience d’apprentissage existants et le service d’un site Web, vous souhaiterez toocheck out recyclage d’un site Web existant prédictive de service au lieu de suivant hello procédure pas à pas mentionnées dans hello suivant la section.</span><span class="sxs-lookup"><span data-stu-id="e59c2-118">If you have an existing Training Experiment and New Web service, you may want toocheck out Retrain an existing Predictive Web service instead of following hello walkthrough mentioned in hello following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="e59c2-119">Workflow de bout en bout</span><span class="sxs-lookup"><span data-stu-id="e59c2-119">End-to-end workflow</span></span>
<span data-ttu-id="e59c2-120">processus Hello implique hello suivant composants : expérience d’apprentissage A et une expérience prédictive publiées en tant qu’un service Web.</span><span class="sxs-lookup"><span data-stu-id="e59c2-120">hello process involves hello following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="e59c2-121">tooenable réapprentissage d’un modèle formé, hello expérience d’apprentissage doit être publiée en tant qu’un service Web avec la sortie de hello d’un modèle formé.</span><span class="sxs-lookup"><span data-stu-id="e59c2-121">tooenable retraining of a trained model, hello Training Experiment must be published as a Web service with hello output of a trained model.</span></span> <span data-ttu-id="e59c2-122">Ainsi, le modèle de toohello d’accès API à instruire de nouveau.</span><span class="sxs-lookup"><span data-stu-id="e59c2-122">This enables API access toohello model for retraining.</span></span> 

<span data-ttu-id="e59c2-123">Hello comme suit s’appliquent tooboth nouveau et classique des services Web :</span><span class="sxs-lookup"><span data-stu-id="e59c2-123">hello following steps apply tooboth New and Classic Web services:</span></span>

<span data-ttu-id="e59c2-124">Créer un service Web prédictif initial de hello :</span><span class="sxs-lookup"><span data-stu-id="e59c2-124">Create hello initial Predictive Web service:</span></span>

* <span data-ttu-id="e59c2-125">Créez une expérience d'apprentissage</span><span class="sxs-lookup"><span data-stu-id="e59c2-125">Create a training experiment</span></span>
* <span data-ttu-id="e59c2-126">Créez une expérience prédictive</span><span class="sxs-lookup"><span data-stu-id="e59c2-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="e59c2-127">Déployez un service web prédictif</span><span class="sxs-lookup"><span data-stu-id="e59c2-127">Deploy a predictive web service</span></span>

<span data-ttu-id="e59c2-128">Recycler le service Web de hello :</span><span class="sxs-lookup"><span data-stu-id="e59c2-128">Retrain hello Web service:</span></span>

* <span data-ttu-id="e59c2-129">Mettre à jour tooallow d’expérience de formation à instruire de nouveau</span><span class="sxs-lookup"><span data-stu-id="e59c2-129">Update training experiment tooallow for retraining</span></span>
* <span data-ttu-id="e59c2-130">Déployer hello recyclage du service web</span><span class="sxs-lookup"><span data-stu-id="e59c2-130">Deploy hello retraining web service</span></span>
* <span data-ttu-id="e59c2-131">Utiliser le modèle hello tooretrain hello Batch Execution Service code</span><span class="sxs-lookup"><span data-stu-id="e59c2-131">Use hello Batch Execution Service code tooretrain hello model</span></span>

<span data-ttu-id="e59c2-132">Pour une procédure pas à pas de hello étapes précédentes, consultez [recycler l’apprentissage des modèles par programme](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="e59c2-132">For a walkthrough of hello preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="e59c2-133">toodeploy un nouveau service web, vous devez disposer des autorisations suffisantes dans hello abonnement toowhich vous déployez le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="e59c2-133">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="e59c2-134">Pour plus d’informations, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="e59c2-134">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="e59c2-135">Si vous avez déployé un service web classique :</span><span class="sxs-lookup"><span data-stu-id="e59c2-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="e59c2-136">Créer un nouveau point de terminaison de service Web prédictif de hello</span><span class="sxs-lookup"><span data-stu-id="e59c2-136">Create a new Endpoint on hello Predictive Web service</span></span>
* <span data-ttu-id="e59c2-137">Obtenir l’URL de correctif hello et le code</span><span class="sxs-lookup"><span data-stu-id="e59c2-137">Get hello PATCH URL and code</span></span>
* <span data-ttu-id="e59c2-138">Utilisez Bonjour de correctif logiciel des URL toopoint Bonjour nouveau point de terminaison à hello reformés modèle</span><span class="sxs-lookup"><span data-stu-id="e59c2-138">Use hello PATCH URL toopoint hello new Endpoint at hello retrained model</span></span> 

<span data-ttu-id="e59c2-139">Pour une procédure pas à pas de hello étapes précédentes, consultez [recycler un service Web classique](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e59c2-139">For a walkthrough of hello preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="e59c2-140">Si vous rencontrez des difficultés de recyclage d’un service Web classique, consultez [dépannage hello recyclage d’un service Web classique de Azure Machine Learning](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="e59c2-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting hello retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="e59c2-141">Si vous avez déployé un nouveau service web :</span><span class="sxs-lookup"><span data-stu-id="e59c2-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="e59c2-142">Connectez-vous à tooyour compte de gestionnaire de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="e59c2-142">Sign in tooyour Azure Resource Manager account</span></span>
* <span data-ttu-id="e59c2-143">Obtenir la définition du service Web hello</span><span class="sxs-lookup"><span data-stu-id="e59c2-143">Get hello Web service definition</span></span>
* <span data-ttu-id="e59c2-144">Exportation hello définition du Service Web en tant que JSON</span><span class="sxs-lookup"><span data-stu-id="e59c2-144">Export hello Web Service Definition as JSON</span></span>
* <span data-ttu-id="e59c2-145">Mettre à jour hello référence toohello `ilearner` blob Bonjour JSON</span><span class="sxs-lookup"><span data-stu-id="e59c2-145">Update hello reference toohello `ilearner` blob in hello JSON</span></span>
* <span data-ttu-id="e59c2-146">Importer des hello JSON dans une définition de Service Web</span><span class="sxs-lookup"><span data-stu-id="e59c2-146">Import hello JSON into a Web Service Definition</span></span>
* <span data-ttu-id="e59c2-147">Mettre à jour de service Web de hello avec la nouvelle définition de Service Web</span><span class="sxs-lookup"><span data-stu-id="e59c2-147">Update hello Web service with new Web Service Definition</span></span>

<span data-ttu-id="e59c2-148">Pour une procédure pas à pas de hello étapes précédentes, consultez [recycler un service d’un site Web à l’aide des applets de commande PowerShell de gestion de Machine Learning hello](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e59c2-148">For a walkthrough of hello preceding steps, see [Retrain a New Web service using hello Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="e59c2-149">processus de Hello pour configurer le recyclage d’un service Web classique comprend hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e59c2-149">hello process for setting up retraining for a Classic Web service involves hello following steps:</span></span>

![Présentation du processus de nouvel apprentissage.][1]

<span data-ttu-id="e59c2-151">processus Hello pour configurer le recyclage d’un service d’un site Web implique hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e59c2-151">hello process for setting up retraining for a New Web service involves hello following steps:</span></span>

![Présentation du processus de nouvel apprentissage.][7]

## <a name="other-resources"></a><span data-ttu-id="e59c2-153">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="e59c2-153">Other Resources</span></span>
* [<span data-ttu-id="e59c2-154">Reformation et mise à jour de modèles Microsoft Azure Machine Learning avec Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e59c2-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span></span>](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [<span data-ttu-id="e59c2-155">Créer de nombreux modèles Machine Learning et points de terminaison de service web à partir d’une expérience à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e59c2-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="e59c2-156">Hello [agréés réapprentissage des API à l’aide de modèles](https://www.youtube.com/watch?v=wwjglA8xllg) vidéo vous montre comment les modèles de Machine Learning tooretrain créés dans Azure Machine Learning à l’aide de hello PowerShell et API de recyclage.</span><span class="sxs-lookup"><span data-stu-id="e59c2-156">hello [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how tooretrain Machine Learning models created in Azure Machine Learning using hello Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

