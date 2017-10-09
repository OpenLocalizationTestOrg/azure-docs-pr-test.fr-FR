---
title: aaaDeploying un nouveau service web dans Azure Machine Learning | Documents Microsoft
description: "flux de travail Hello du déploiement d’un ARM en fonction de service web"
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
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="b00ef-103">Déployer comme un nouveau service web</span><span class="sxs-lookup"><span data-stu-id="b00ef-103">Deploy a new web service</span></span>
<span data-ttu-id="b00ef-104">Fournit des services web basés sur Microsoft Azure Machine learning maintenant [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) permettant de nouvelles options de plan de facturation et déployer vos régions toomultiple du service web.</span><span class="sxs-lookup"><span data-stu-id="b00ef-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service toomultiple regions.</span></span>

<span data-ttu-id="b00ef-105">toodeploy de flux de travail général Hello un service web à l’aide des Services Web de Microsoft Azure Machine Learning est la suivante :</span><span class="sxs-lookup"><span data-stu-id="b00ef-105">hello general workflow toodeploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="b00ef-106">Créer une expérience prédictive</span><span class="sxs-lookup"><span data-stu-id="b00ef-106">Create a predictive experiment</span></span>
* <span data-ttu-id="b00ef-107">la déployer</span><span class="sxs-lookup"><span data-stu-id="b00ef-107">deploy it</span></span>
* <span data-ttu-id="b00ef-108">choisir son nom</span><span class="sxs-lookup"><span data-stu-id="b00ef-108">configure its name</span></span>
* <span data-ttu-id="b00ef-109">profil de facturation</span><span class="sxs-lookup"><span data-stu-id="b00ef-109">billing plan</span></span>
* <span data-ttu-id="b00ef-110">la tester</span><span class="sxs-lookup"><span data-stu-id="b00ef-110">test it</span></span>
* <span data-ttu-id="b00ef-111">l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="b00ef-111">consume it.</span></span>

<span data-ttu-id="b00ef-112">Hello graphique suivant illustre le flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="b00ef-112">hello following graphic illustrates hello workflow.</span></span>

![Flux de travail du déploiement d’un service web][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="b00ef-114">Déployer un service web à partir de Studio</span><span class="sxs-lookup"><span data-stu-id="b00ef-114">Deploy web service from Studio</span></span>
<span data-ttu-id="b00ef-115">toodeploy une expérience en tant qu’un nouveau service web.</span><span class="sxs-lookup"><span data-stu-id="b00ef-115">toodeploy an experiment as a new web service.</span></span> <span data-ttu-id="b00ef-116">Connectez-vous à hello Machine Learning Studio et créez un service web prédictif.</span><span class="sxs-lookup"><span data-stu-id="b00ef-116">Sign into hello Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="b00ef-117">**Remarque**: si vous avez déjà déployé une expérience en tant que service web classique, vous ne pouvez pas le déployer en tant que nouveau service web.</span><span class="sxs-lookup"><span data-stu-id="b00ef-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="b00ef-118">Cliquez sur **exécuter** bas hello hello expérimenter la zone de dessin, puis cliquez sur **déployer le Service Web** et **déployer le Service Web [nouveau]**.</span><span class="sxs-lookup"><span data-stu-id="b00ef-118">Click **Run** at hello bottom of hello experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="b00ef-119">page de déploiement de Hello du Gestionnaire de Service Web de Machine Learning hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="b00ef-119">hello deployment page of hello Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="b00ef-120">Page d’expérience de déploiement du Gestionnaire de service web Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b00ef-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="b00ef-121">Sur la page de déployer une expérience de hello, entrez un nom pour le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="b00ef-121">On hello Deploy Experiment page, enter a name for hello web service.</span></span>
<span data-ttu-id="b00ef-122">Sélectionnez un plan de tarification.</span><span class="sxs-lookup"><span data-stu-id="b00ef-122">Select a pricing plan.</span></span> <span data-ttu-id="b00ef-123">Si vous avez un plan de tarification existant, que vous pouvez le sélectionner, sinon vous devez créer un nouveau plan de prix pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="b00ef-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for hello service.</span></span> 

1. <span data-ttu-id="b00ef-124">Bonjour **Plan tarifaire** liste déroulante, sélectionnez un plan existant ou hello **sélectionnez Nouveau plan** option.</span><span class="sxs-lookup"><span data-stu-id="b00ef-124">In hello **Price Plan** drop down, select an existing plan or select hello **Select new plan** option.</span></span>
2. <span data-ttu-id="b00ef-125">Dans **le nom du Plan**, tapez un nom qui identifie le plan hello sur votre facture.</span><span class="sxs-lookup"><span data-stu-id="b00ef-125">In **Plan Name**, type a name that will identify hello plan on your bill.</span></span>
3. <span data-ttu-id="b00ef-126">Sélectionnez une des hello **niveaux de planification mensuelle**.</span><span class="sxs-lookup"><span data-stu-id="b00ef-126">Select one of hello **Monthly Plan Tiers**.</span></span> <span data-ttu-id="b00ef-127">Notez que les niveaux de plan hello par défaut toohello des plans pour votre région par défaut et votre service web est déployé toothat région.</span><span class="sxs-lookup"><span data-stu-id="b00ef-127">Note that hello plan tiers default toohello plans for your default region and your web service is deployed toothat region.</span></span>

<span data-ttu-id="b00ef-128">Cliquez sur **déployer** et de la page de démarrage rapide de hello pour votre service web s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="b00ef-128">Click **Deploy** and hello Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="b00ef-129">Page Démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="b00ef-129">Quickstart page</span></span>
<span data-ttu-id="b00ef-130">page de démarrage rapide du service web Hello vous donne accès et des conseils sur les tâches les plus courantes hello que vous allez effectuer après la création d’un nouveau service web.</span><span class="sxs-lookup"><span data-stu-id="b00ef-130">hello web service Quickstart page gives you access and guidance on hello most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="b00ef-131">À ce stade, vous pouvez facilement accéder à la fois hello **Test** page et **consommer** page.</span><span class="sxs-lookup"><span data-stu-id="b00ef-131">From here you can easily access both hello **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="b00ef-132">Test de votre service web</span><span class="sxs-lookup"><span data-stu-id="b00ef-132">Testing your web service</span></span>
<span data-ttu-id="b00ef-133">À partir de la page de démarrage rapide de hello, cliquez sur service web de Test, sous tâches courantes.</span><span class="sxs-lookup"><span data-stu-id="b00ef-133">From hello Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="b00ef-134">service de tootest hello web comme un Service de requête-réponse (RR) :</span><span class="sxs-lookup"><span data-stu-id="b00ef-134">tootest hello web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="b00ef-135">Cliquez sur **Test** sur la barre de menus hello.</span><span class="sxs-lookup"><span data-stu-id="b00ef-135">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="b00ef-136">Cliquez sur **Request-Response**(Requête-réponse).</span><span class="sxs-lookup"><span data-stu-id="b00ef-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="b00ef-137">Entrez les valeurs appropriées pour les colonnes d’entrée hello votre expérience.</span><span class="sxs-lookup"><span data-stu-id="b00ef-137">Enter appropriate values for hello input columns of your experiment.</span></span>
* <span data-ttu-id="b00ef-138">Cliquez sur Tester **requête-réponse**.</span><span class="sxs-lookup"><span data-stu-id="b00ef-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="b00ef-139">Résultat s’affiche sur la droite hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="b00ef-139">You results will display on hello right hand side of hello page.</span></span>

<span data-ttu-id="b00ef-140">tootest un service web de Service de l’exécution de lot (BES), vous allez utiliser un fichier CSV :</span><span class="sxs-lookup"><span data-stu-id="b00ef-140">tootest a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="b00ef-141">Cliquez sur **Test** sur la barre de menus hello.</span><span class="sxs-lookup"><span data-stu-id="b00ef-141">Click **Test** on hello menu bar.</span></span>
* <span data-ttu-id="b00ef-142">Cliquez sur **Lot**.</span><span class="sxs-lookup"><span data-stu-id="b00ef-142">Click **Batch**.</span></span>
* <span data-ttu-id="b00ef-143">Sous votre entrée, cliquez sur Parcourir et naviguez tooyour exemple de fichier de données.</span><span class="sxs-lookup"><span data-stu-id="b00ef-143">Under your input, click Browse and navigate tooyour sample data file.</span></span>
* <span data-ttu-id="b00ef-144">Cliquez sur **Test**.</span><span class="sxs-lookup"><span data-stu-id="b00ef-144">Click **Test**.</span></span>

<span data-ttu-id="b00ef-145">état de Hello de votre test s’affiche sous **tester des traitements par lots**.</span><span class="sxs-lookup"><span data-stu-id="b00ef-145">hello status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="b00ef-146">Utilisation de votre service web</span><span class="sxs-lookup"><span data-stu-id="b00ef-146">Consuming your Web Service</span></span>
<span data-ttu-id="b00ef-147">Lors de leur déploiement en tant que services web, les expériences Azure Machine Learning proposent une API REST, qui peut être exploitée par divers périphériques et plateformes.</span><span class="sxs-lookup"><span data-stu-id="b00ef-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="b00ef-148">Il s’agit, car des messages au format hello simple API REST accepte et répond avec JSON.</span><span class="sxs-lookup"><span data-stu-id="b00ef-148">This is because hello simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="b00ef-149">Hello portail d’Azure Machine Learning fournit du code qui peut être utilisé toocall hello web service R, c# et Python.</span><span class="sxs-lookup"><span data-stu-id="b00ef-149">hello Azure Machine Learning portal provides code that can be used toocall hello web service in R, C#, and Python.</span></span>

<span data-ttu-id="b00ef-150">Sur la page de consommation hello, vous pouvez rechercher :</span><span class="sxs-lookup"><span data-stu-id="b00ef-150">On hello Consuming page you can find:</span></span>

* <span data-ttu-id="b00ef-151">clé de l’API de Hello et URI pour la consommation de service web dans les applications.</span><span class="sxs-lookup"><span data-stu-id="b00ef-151">hello API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="b00ef-152">Tookick de modèles d’application web d’Excel et de démarrer votre consommation.</span><span class="sxs-lookup"><span data-stu-id="b00ef-152">Excel and web app templates tookick start your consumption process.</span></span>
* <span data-ttu-id="b00ef-153">Exemple de code dans c#, python et R tooget que vous avez démarré.</span><span class="sxs-lookup"><span data-stu-id="b00ef-153">Sample code in C#, python, and R tooget you started.</span></span>

<span data-ttu-id="b00ef-154">Pour plus d’informations sur l’utilisation des services web, consultez [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="b00ef-154">For more information on consuming web services, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b00ef-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b00ef-155">Next Steps</span></span>
<span data-ttu-id="b00ef-156">Pour plus d’informations sur l’utilisation des services web, consultez :</span><span class="sxs-lookup"><span data-stu-id="b00ef-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="b00ef-157">Comment tooconsume un service Web de Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b00ef-157">How tooconsume an Azure Machine Learning Web service</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="b00ef-158">Services web Azure Machine Learning : déploiement et consommation</span><span class="sxs-lookup"><span data-stu-id="b00ef-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
