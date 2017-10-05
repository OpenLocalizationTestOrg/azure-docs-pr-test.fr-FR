---
title: "Apprenez à gérer les services web AzureML à l’aide de la gestion des API | Microsoft Docs"
description: "Guide montrant comment gérer les services web AzureML à l’aide de la gestion des API"
keywords: apprentissage automatique,gestion des api
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 65eff3f4971f79886a840bb19bf76aaab48878de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="learn-how-to-manage-azureml-web-services-using-api-management"></a><span data-ttu-id="f823d-104">Gestion des services web AzureML à l’aide de Gestion des API</span><span class="sxs-lookup"><span data-stu-id="f823d-104">Learn how to manage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="f823d-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f823d-105">Overview</span></span>
<span data-ttu-id="f823d-106">Ce guide décrit la prise en main rapide de la gestion de vos services web AzureML grâce à Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="f823d-106">This guide shows you how to quickly get started using API Management to manage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="f823d-107">Qu’est-ce que Gestion des API Azure ?</span><span class="sxs-lookup"><span data-stu-id="f823d-107">What is Azure API Management?</span></span>
<span data-ttu-id="f823d-108">Gestion des API Azure est un service Azure qui vous permet de gérer vos points de terminaison d’API REST en définissant l’accès utilisateur, la limitation d’utilisation et la surveillance du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="f823d-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="f823d-109">Cliquez [ici](https://azure.microsoft.com/services/api-management/) pour plus d’informations sur Gestion des API Azure.</span><span class="sxs-lookup"><span data-stu-id="f823d-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="f823d-110">Cliquez [ici](../api-management/api-management-get-started.md) pour débuter avec Gestion des API Azure.</span><span class="sxs-lookup"><span data-stu-id="f823d-110">Click [here](../api-management/api-management-get-started.md) for a guide on how to get started with Azure API Management.</span></span> <span data-ttu-id="f823d-111">Cet autre guide, sur lequel ce guide est basé, couvre plus de rubriques, notamment les configurations de notification, la tarification, la gestion des réponses, l’authentification des utilisateurs, la création de produits, les abonnements pour développeur et le tableau de bord d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="f823d-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="f823d-112">Présentation d’AzureML</span><span class="sxs-lookup"><span data-stu-id="f823d-112">What is AzureML?</span></span>
<span data-ttu-id="f823d-113">AzureML est un service Azure d’apprentissage automatique qui vous permet de facilement générer, déployer et partager des solutions d’analyse avancée.</span><span class="sxs-lookup"><span data-stu-id="f823d-113">AzureML is an Azure service for machine learning that enables you to easily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="f823d-114">Cliquez [ici](https://azure.microsoft.com/services/machine-learning/) pour plus d’informations sur AzureML.</span><span class="sxs-lookup"><span data-stu-id="f823d-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f823d-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f823d-115">Prerequisites</span></span>
<span data-ttu-id="f823d-116">Pour utiliser ce guide, il vous faut :</span><span class="sxs-lookup"><span data-stu-id="f823d-116">To complete this guide, you need:</span></span>

* <span data-ttu-id="f823d-117">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="f823d-117">An Azure account.</span></span> <span data-ttu-id="f823d-118">Si vous n’avez pas de compte Azure, cliquez [ici](https://azure.microsoft.com/pricing/free-trial/) pour plus d’informations sur la création d’un compte d’essai gratuit.</span><span class="sxs-lookup"><span data-stu-id="f823d-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="f823d-119">Un compte AzureML.</span><span class="sxs-lookup"><span data-stu-id="f823d-119">An AzureML account.</span></span> <span data-ttu-id="f823d-120">Si vous n’avez pas de compte AzureML, cliquez [ici](https://studio.azureml.net/) pour plus d’informations sur la création d’un compte d’essai gratuit.</span><span class="sxs-lookup"><span data-stu-id="f823d-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="f823d-121">L’espace de travail, le service et l’api_key pour l’expérience AzureML déployés sous forme de service web.</span><span class="sxs-lookup"><span data-stu-id="f823d-121">The workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="f823d-122">Cliquez [ici](machine-learning-create-experiment.md) pour plus d’informations sur la création d’une expérience AzureML.</span><span class="sxs-lookup"><span data-stu-id="f823d-122">Click [here](machine-learning-create-experiment.md) for details on how to create an AzureML experiment.</span></span> <span data-ttu-id="f823d-123">Cliquez [ici](machine-learning-publish-a-machine-learning-web-service.md) pour plus d’informations sur le déploiement d’une expérience AzureML comme service web.</span><span class="sxs-lookup"><span data-stu-id="f823d-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how to deploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="f823d-124">L’annexe A contient également des instructions sur la façon de créer et de tester une expérience AzureML simple et de la déployer en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="f823d-124">Alternately, Appendix A has instructions for how to create and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="f823d-125">Création d'une instance Gestion des API</span><span class="sxs-lookup"><span data-stu-id="f823d-125">Create an API Management instance</span></span>
<span data-ttu-id="f823d-126">Vous trouverez ci-dessous les étapes d’utilisation de Gestion des API pour gérer votre service web AzureML.</span><span class="sxs-lookup"><span data-stu-id="f823d-126">Below are the steps for using API Management to manage your AzureML web service.</span></span> <span data-ttu-id="f823d-127">Créez d’abord une instance de service.</span><span class="sxs-lookup"><span data-stu-id="f823d-127">First create a service instance.</span></span> <span data-ttu-id="f823d-128">Connectez-vous au [portail Classic](https://manage.windowsazure.com/) et cliquez sur **Nouveau** > **App Services** > **Gestion des API** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f823d-128">Log in to the [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="f823d-130">Spécifiez une **URL** unique.</span><span class="sxs-lookup"><span data-stu-id="f823d-130">Specify a unique **URL**.</span></span> <span data-ttu-id="f823d-131">Ce guide utilise **demoazureml**. Vous devez choisir un nom différent.</span><span class="sxs-lookup"><span data-stu-id="f823d-131">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="f823d-132">Choisissez l’**abonnement** et la **région** souhaités pour votre instance de service.</span><span class="sxs-lookup"><span data-stu-id="f823d-132">Choose the desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="f823d-133">Une fois vos sélections effectuées, cliquez sur le bouton Suivant.</span><span class="sxs-lookup"><span data-stu-id="f823d-133">After making your selections, click the next button.</span></span>

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="f823d-135">Spécifiez une valeur pour le **nom de l’organisation**.</span><span class="sxs-lookup"><span data-stu-id="f823d-135">Specify a value for the **Organization Name**.</span></span> <span data-ttu-id="f823d-136">Ce guide utilise **demoazureml**. Vous devez choisir un nom différent.</span><span class="sxs-lookup"><span data-stu-id="f823d-136">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="f823d-137">Entrez votre adresse e-mail dans le champ **Adresse de messagerie de l’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="f823d-137">Enter your email address in the **administrator e-mail** field.</span></span> <span data-ttu-id="f823d-138">Cette adresse de messagerie est utilisée pour les notifications provenant du système Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="f823d-138">This email address is used for notifications from the API Management system.</span></span>

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="f823d-140">Cliquez sur la coche pour créer votre instance de service.</span><span class="sxs-lookup"><span data-stu-id="f823d-140">Click the check box to create your service instance.</span></span> <span data-ttu-id="f823d-141">*Jusqu’à trente minutes sont nécessaires pour créer un service*.</span><span class="sxs-lookup"><span data-stu-id="f823d-141">*It takes up to thirty minutes for a new service to be created*.</span></span>

## <a name="create-the-api"></a><span data-ttu-id="f823d-142">Création de l’API</span><span class="sxs-lookup"><span data-stu-id="f823d-142">Create the API</span></span>
<span data-ttu-id="f823d-143">Une fois l’instance de service créée, l’étape suivante consiste à créer une API.</span><span class="sxs-lookup"><span data-stu-id="f823d-143">Once the service instance is created, the next step is to create the API.</span></span> <span data-ttu-id="f823d-144">Une API se compose d’un ensemble d’opérations pouvant être appelées à partir d’une application cliente.</span><span class="sxs-lookup"><span data-stu-id="f823d-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="f823d-145">Les opérations de l’API sont transmises par proxy aux services web existants.</span><span class="sxs-lookup"><span data-stu-id="f823d-145">API operations are proxied to existing web services.</span></span> <span data-ttu-id="f823d-146">Ce guide crée des API comme proxy pour les services web AzureML RRS et BES existants.</span><span class="sxs-lookup"><span data-stu-id="f823d-146">This guide creates APIs that proxy to the existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="f823d-147">Les API sont créées et configurées à partir du portail des éditeurs d’API, accessible via le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="f823d-147">APIs are created and configured from the API publisher portal, which is accessed through the Azure Classic Portal.</span></span> <span data-ttu-id="f823d-148">Pour atteindre le portail des éditeurs, sélectionnez votre instance de service.</span><span class="sxs-lookup"><span data-stu-id="f823d-148">To reach the publisher portal, select your service instance.</span></span>

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="f823d-150">Cliquez sur **Gérer** dans le portail Azure Classic de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="f823d-150">Click **Manage** in the Azure Classic Portal for your API Management service.</span></span>

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="f823d-152">Cliquez sur **API** dans le menu **Gestion des API** à gauche, puis sur **Ajouter des API**.</span><span class="sxs-lookup"><span data-stu-id="f823d-152">Click **APIs** from the **API Management** menu on the left, and then click **Add API**.</span></span>

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="f823d-154">Tapez **API de démonstration AzureML** comme **nom de l’API web**.</span><span class="sxs-lookup"><span data-stu-id="f823d-154">Type **AzureML Demo API** as the **Web API name**.</span></span> <span data-ttu-id="f823d-155">Tapez **https://ussouthcentral.services.azureml.net** comme **URL du service web**.</span><span class="sxs-lookup"><span data-stu-id="f823d-155">Type **https://ussouthcentral.services.azureml.net** as the **Web service URL**.</span></span> <span data-ttu-id="f823d-156">Tapez **azureml-demo** comme **suffixe d’URL de l’API web**.</span><span class="sxs-lookup"><span data-stu-id="f823d-156">Type **azureml-demo** as the **Web API URL suffix**.</span></span> <span data-ttu-id="f823d-157">Cochez **HTTPS** comme schéma **d’URL de l’API web**.</span><span class="sxs-lookup"><span data-stu-id="f823d-157">Check **HTTPS** as the **Web API URL** scheme.</span></span> <span data-ttu-id="f823d-158">Sélectionnez **Starter** comme **produit**.</span><span class="sxs-lookup"><span data-stu-id="f823d-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="f823d-159">Quand vous avez terminé, cliquez sur **Enregistrer** pour créer l’API.</span><span class="sxs-lookup"><span data-stu-id="f823d-159">When finished, click **Save** to create the API.</span></span>

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-the-operations"></a><span data-ttu-id="f823d-161">Ajout des opérations</span><span class="sxs-lookup"><span data-stu-id="f823d-161">Add the operations</span></span>
<span data-ttu-id="f823d-162">Cliquez sur **Ajouter une opération** pour ajouter des opérations à l’API.</span><span class="sxs-lookup"><span data-stu-id="f823d-162">Click **Add operation** to add operations to this API.</span></span>

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="f823d-164">La fenêtre **Nouvelle opération** s’affiche et l’onglet **Signature** est sélectionné par défaut.</span><span class="sxs-lookup"><span data-stu-id="f823d-164">The **New operation** window will be displayed and the **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="f823d-165">Ajout d’une opération RRS</span><span class="sxs-lookup"><span data-stu-id="f823d-165">Add RRS Operation</span></span>
<span data-ttu-id="f823d-166">Créez une opération pour le service AzureML RRS.</span><span class="sxs-lookup"><span data-stu-id="f823d-166">First create an operation for the AzureML RRS service.</span></span> <span data-ttu-id="f823d-167">Sélectionnez **POST** comme **verbe HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f823d-167">Select **POST** as the **HTTP verb**.</span></span> <span data-ttu-id="f823d-168">Tapez **/workspaces/{espace de travail}/services/{service}/execute?api-version={versionapi}&details={détails}** comme **modèle d’URL**.</span><span class="sxs-lookup"><span data-stu-id="f823d-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as the **URL template**.</span></span> <span data-ttu-id="f823d-169">Tapez **Exécution RRS** comme **nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="f823d-169">Type **RRS Execute** as the **Display name**.</span></span>

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="f823d-171">Cliquez sur **Réponses** > **AJOUTER** sur la gauche et sélectionnez **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f823d-171">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="f823d-172">Cliquez sur **Enregistrer** pour enregistrer cette opération.</span><span class="sxs-lookup"><span data-stu-id="f823d-172">Click **Save** to save this operation.</span></span>

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="f823d-174">Ajout d’opérations BES</span><span class="sxs-lookup"><span data-stu-id="f823d-174">Add BES Operations</span></span>
<span data-ttu-id="f823d-175">Les captures d’écran ne sont pas incluses pour les opérations BES, car elles sont très similaires à celles de l’ajout de l’opération RRS.</span><span class="sxs-lookup"><span data-stu-id="f823d-175">Screenshots are not included for the BES operations as they are very similar to those for adding the RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="f823d-176">Envoi (et non démarrage) d’un travail d’exécution de lot</span><span class="sxs-lookup"><span data-stu-id="f823d-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="f823d-177">Cliquez sur **Ajouter une opération** pour ajouter l’opération BES AzureML à l’API.</span><span class="sxs-lookup"><span data-stu-id="f823d-177">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="f823d-178">Sélectionnez **POST** comme **verbe HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f823d-178">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="f823d-179">Tapez **/workspaces/{espace de travail}/services/{service}/jobs?api-version={versionapi}** comme **modèle d’URL**.</span><span class="sxs-lookup"><span data-stu-id="f823d-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="f823d-180">Tapez **Envoi BES** comme **nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="f823d-180">Type **BES Submit** for the **Display name**.</span></span> <span data-ttu-id="f823d-181">Cliquez sur **Réponses** > **AJOUTER** sur la gauche et sélectionnez **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f823d-181">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="f823d-182">Cliquez sur **Enregistrer** pour enregistrer cette opération.</span><span class="sxs-lookup"><span data-stu-id="f823d-182">Click **Save** to save this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="f823d-183">Démarrage d’une tâche d’exécution de lot</span><span class="sxs-lookup"><span data-stu-id="f823d-183">Start a Batch Execution job</span></span>
<span data-ttu-id="f823d-184">Cliquez sur **Ajouter une opération** pour ajouter l’opération BES AzureML à l’API.</span><span class="sxs-lookup"><span data-stu-id="f823d-184">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="f823d-185">Sélectionnez **POST** comme **verbe HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f823d-185">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="f823d-186">Tapez **/workspaces/{espace de travail}/services/{service}/jobs/{jobid}/start?api-version={versionapi}** comme **modèle d’URL**.</span><span class="sxs-lookup"><span data-stu-id="f823d-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="f823d-187">Tapez **Démarrage BES** comme **nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="f823d-187">Type **BES Start** for the **Display name**.</span></span> <span data-ttu-id="f823d-188">Cliquez sur **Réponses** > **AJOUTER** sur la gauche et sélectionnez **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f823d-188">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="f823d-189">Cliquez sur **Enregistrer** pour enregistrer cette opération.</span><span class="sxs-lookup"><span data-stu-id="f823d-189">Click **Save** to save this operation.</span></span>

### <a name="get-the-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="f823d-190">Obtention de l’état ou du résultat d’une tâche d’exécution de lot</span><span class="sxs-lookup"><span data-stu-id="f823d-190">Get the status or result of a Batch Execution job</span></span>
<span data-ttu-id="f823d-191">Cliquez sur **Ajouter une opération** pour ajouter l’opération BES AzureML à l’API.</span><span class="sxs-lookup"><span data-stu-id="f823d-191">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="f823d-192">Sélectionnez **GET** comme **verbe HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f823d-192">Select **GET** for the **HTTP verb**.</span></span> <span data-ttu-id="f823d-193">Tapez **/workspaces/{espace de travail}/services/{service}/jobs/{idjob}?api-version={versionapi}** comme **modèle d’URL**.</span><span class="sxs-lookup"><span data-stu-id="f823d-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="f823d-194">Tapez **État BES** comme **nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="f823d-194">Type **BES Status** for the **Display name**.</span></span> <span data-ttu-id="f823d-195">Cliquez sur **Réponses** > **AJOUTER** sur la gauche et sélectionnez **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f823d-195">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="f823d-196">Cliquez sur **Enregistrer** pour enregistrer cette opération.</span><span class="sxs-lookup"><span data-stu-id="f823d-196">Click **Save** to save this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="f823d-197">Suppression d’une tâche d’exécution de lot</span><span class="sxs-lookup"><span data-stu-id="f823d-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="f823d-198">Cliquez sur **Ajouter une opération** pour ajouter l’opération BES AzureML à l’API.</span><span class="sxs-lookup"><span data-stu-id="f823d-198">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="f823d-199">Sélectionnez **DELETE** comme **verbe HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f823d-199">Select **DELETE** for the **HTTP verb**.</span></span> <span data-ttu-id="f823d-200">Tapez **/workspaces/{espace de travail}/services/{service}/jobs/{idjob}?api-version={versionapi}** comme **modèle d’URL**.</span><span class="sxs-lookup"><span data-stu-id="f823d-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="f823d-201">Tapez **Suppression BES** comme **nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="f823d-201">Type **BES Delete** for the **Display name**.</span></span> <span data-ttu-id="f823d-202">Cliquez sur **Réponses** > **AJOUTER** sur la gauche et sélectionnez **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f823d-202">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="f823d-203">Cliquez sur **Enregistrer** pour enregistrer cette opération.</span><span class="sxs-lookup"><span data-stu-id="f823d-203">Click **Save** to save this operation.</span></span>

## <a name="call-an-operation-from-the-developer-portal"></a><span data-ttu-id="f823d-204">Appel d'une opération à partir du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="f823d-204">Call an operation from the Developer Portal</span></span>
<span data-ttu-id="f823d-205">Les opérations peuvent être directement appelées depuis le portail des développeurs, ce qui permet d'afficher et de tester les opérations d'une API.</span><span class="sxs-lookup"><span data-stu-id="f823d-205">Operations can be called directly from the Developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="f823d-206">Dans cette étape du guide, vous appelez la méthode **Exécution RRS** qui a été ajoutée à **l’API de démonstration AzureML**.</span><span class="sxs-lookup"><span data-stu-id="f823d-206">In this guide step you will call the **RRS Execute** method that was added to the **AzureML Demo API**.</span></span> <span data-ttu-id="f823d-207">Cliquez sur **Portail des développeurs** dans le menu en haut à droite du portail Classic.</span><span class="sxs-lookup"><span data-stu-id="f823d-207">Click **Developer portal** from the menu at the top right of the Classic Portal.</span></span>

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="f823d-209">Cliquez sur **API** dans le menu en haut, puis sur **API de démonstration AzureML** pour afficher les opérations disponibles.</span><span class="sxs-lookup"><span data-stu-id="f823d-209">Click **APIs** from the top menu, and then click **AzureML Demo API** to see the operations available.</span></span>

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="f823d-211">Sélectionnez **Exécution RRS** pour l’opération.</span><span class="sxs-lookup"><span data-stu-id="f823d-211">Select **RRS Execute** for the operation.</span></span> <span data-ttu-id="f823d-212">Cliquez sur **Essayer**.</span><span class="sxs-lookup"><span data-stu-id="f823d-212">Click **Try It**.</span></span>

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="f823d-214">Pour les paramètres de requête, tapez votre **espace de travail**, le **service**, **2.0** dans **versionapi** et **true** dans **Détails**.</span><span class="sxs-lookup"><span data-stu-id="f823d-214">For Request parameters, type your **workspace**,  **service**, **2.0** for the **apiversion**, and  **true** for the **details**.</span></span> <span data-ttu-id="f823d-215">Vous pouvez trouver vos **espace de travail** et **service** dans le tableau de bord du service web AzureML (voir **Test du service web** dans l’annexe A).</span><span class="sxs-lookup"><span data-stu-id="f823d-215">You can find your **workspace** and **service** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="f823d-216">Pour les en-têtes de requête, cliquez sur **Ajouter en-tête** et tapez **Content-Type** et **application/json**, puis cliquez sur **Ajouter en-tête** et tapez **Autorisation** et **Porteur<YOUR AZUREML SERVICE API-KEY>**.</span><span class="sxs-lookup"><span data-stu-id="f823d-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="f823d-217">Vous pouvez trouver votre **clé API** dans le tableau de bord du service web AzureML (voir **Test du service web** dans l’annexe A).</span><span class="sxs-lookup"><span data-stu-id="f823d-217">You can find your **api key** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="f823d-218">Tapez **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["C’est une belle journée"]]}}, "GlobalParameters": {}}** dans le corps de la requête.</span><span class="sxs-lookup"><span data-stu-id="f823d-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for the request body.</span></span>

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="f823d-220">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="f823d-220">Click **Send**.</span></span>

![Envoyer](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="f823d-222">Après l’appel d’une opération, le portail des développeurs affiche **l’URL requise** à partir du service principal, **l’état de la réponse**, les **en-têtes de la réponse** et tout **contenu de la réponse**.</span><span class="sxs-lookup"><span data-stu-id="f823d-222">After an operation is invoked, the developer portal displays the **Requested URL** from the back-end service, the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="f823d-224">Annexe A - Création et test d’un service web AzureML simple</span><span class="sxs-lookup"><span data-stu-id="f823d-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-the-experiment"></a><span data-ttu-id="f823d-225">Création de l’expérience</span><span class="sxs-lookup"><span data-stu-id="f823d-225">Creating the experiment</span></span>
<span data-ttu-id="f823d-226">Vous trouverez ci-dessous les étapes de création d’une expérience AzureML simple et de son déploiement comme service web.</span><span class="sxs-lookup"><span data-stu-id="f823d-226">Below are the steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="f823d-227">Le service web prend comme entrée une colonne de texte arbitraire et retourne un ensemble de fonctionnalités représentées sous forme d’entiers.</span><span class="sxs-lookup"><span data-stu-id="f823d-227">The web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="f823d-228">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f823d-228">For example:</span></span>

| <span data-ttu-id="f823d-229">Texte</span><span class="sxs-lookup"><span data-stu-id="f823d-229">Text</span></span> | <span data-ttu-id="f823d-230">Texte haché</span><span class="sxs-lookup"><span data-stu-id="f823d-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="f823d-231">C’est une belle journée</span><span class="sxs-lookup"><span data-stu-id="f823d-231">This is a good day</span></span> |<span data-ttu-id="f823d-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="f823d-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="f823d-233">Tout d’abord, à l’aide du navigateur de votre choix, accédez à [https://studio.azureml.net/](https://studio.azureml.net/) et entrez vos informations d’identification pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="f823d-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials to log in.</span></span> <span data-ttu-id="f823d-234">Ensuite, créez une nouvelle expérience vide.</span><span class="sxs-lookup"><span data-stu-id="f823d-234">Next, create a new blank experiment.</span></span>

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="f823d-236">Renommez-la **SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="f823d-236">Rename it to **SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="f823d-237">Développez **Datasets enregistrés** et faites glisser **Critiques de livres d’Amazon** sur votre expérimentation.</span><span class="sxs-lookup"><span data-stu-id="f823d-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="f823d-239">Développez **Transformation des données** et **Manipulation** et faites glisser **Sélectionner des colonnes dans le jeu de données** sur votre expérimentation.</span><span class="sxs-lookup"><span data-stu-id="f823d-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="f823d-240">Connectez **Critiques de livres d’Amazon** à **Sélectionner des colonnes dans le jeu de données**.</span><span class="sxs-lookup"><span data-stu-id="f823d-240">Connect **Book Reviews from Amazon** to **Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="f823d-242">Cliquez sur **Sélectionner des colonnes dans le jeu de données**, puis sur **Exécuter le sélecteur de colonne** et sélectionnez **Col2**.</span><span class="sxs-lookup"><span data-stu-id="f823d-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="f823d-243">Cliquez sur la coche pour appliquer ces modifications.</span><span class="sxs-lookup"><span data-stu-id="f823d-243">Click the checkmark to apply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="f823d-245">Développez **Analyse de texte** et faites glisser **Fonction de hachage** sur l’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="f823d-245">Expand **Text Analytics** and drag **Feature Hashing** onto the experiment.</span></span> <span data-ttu-id="f823d-246">Connectez **Sélectionner des colonnes dans le jeu de données** à **Fonction de hachage**.</span><span class="sxs-lookup"><span data-stu-id="f823d-246">Connect **Select Columns in Dataset** to **Feature Hashing**.</span></span>

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="f823d-248">Tapez **3** pour la **Taille de bits de hachage**.</span><span class="sxs-lookup"><span data-stu-id="f823d-248">Type **3** for the **Hashing bitsize**.</span></span> <span data-ttu-id="f823d-249">Cela crée 8 (23) colonnes.</span><span class="sxs-lookup"><span data-stu-id="f823d-249">This will create 8 (23) columns.</span></span>

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="f823d-251">À ce stade, vous pouvez cliquer sur **Exécuter** pour tester l’expérience.</span><span class="sxs-lookup"><span data-stu-id="f823d-251">At this point, you may want to click **Run** to test the experiment.</span></span>

![Exécuter](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="f823d-253">Création d’un service web</span><span class="sxs-lookup"><span data-stu-id="f823d-253">Create a web service</span></span>
<span data-ttu-id="f823d-254">Maintenant, créez un service web.</span><span class="sxs-lookup"><span data-stu-id="f823d-254">Now create a web service.</span></span> <span data-ttu-id="f823d-255">Développez **Service Web** et faites glisser **Entrée** sur votre expérimentation.</span><span class="sxs-lookup"><span data-stu-id="f823d-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="f823d-256">Connectez **Entrée** à **Fonction de hachage**.</span><span class="sxs-lookup"><span data-stu-id="f823d-256">Connect **Input** to **Feature Hashing**.</span></span> <span data-ttu-id="f823d-257">Faites également glisser **Sortie** sur votre expérience.</span><span class="sxs-lookup"><span data-stu-id="f823d-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="f823d-258">Connectez **Sortie** à **Fonction de hachage**.</span><span class="sxs-lookup"><span data-stu-id="f823d-258">Connect **Output** to **Feature Hashing**.</span></span>

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="f823d-260">Cliquez sur **Publier le service Web**.</span><span class="sxs-lookup"><span data-stu-id="f823d-260">Click **Publish web service**.</span></span>

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="f823d-262">Cliquez sur **Oui** pour publier l’expérience.</span><span class="sxs-lookup"><span data-stu-id="f823d-262">Click **Yes** to publish the experiment.</span></span>

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-the-web-service"></a><span data-ttu-id="f823d-264">Test du service web</span><span class="sxs-lookup"><span data-stu-id="f823d-264">Test the web service</span></span>
<span data-ttu-id="f823d-265">Un service web AzureML se compose de points de terminaison RRS (service de requête/réponse) et BES (service d’exécution de lot).</span><span class="sxs-lookup"><span data-stu-id="f823d-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="f823d-266">RSS est conçu pour l’exécution synchrone.</span><span class="sxs-lookup"><span data-stu-id="f823d-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="f823d-267">BES est conçu pour l’exécution de tâches asynchrone.</span><span class="sxs-lookup"><span data-stu-id="f823d-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="f823d-268">Pour tester un service web avec l’exemple de source Python ci-dessous, vous devrez peut-être télécharger et installer le Kit de développement logiciel (SDK) Microsoft Azure  pour Python (voir [Installation de Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="f823d-268">To test your web service with the sample Python source below, you may need to download and install the Azure SDK for Python (see: [How to install Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="f823d-269">Il vous faudra également **l’espace de travail**, le **service** et **l’api_key** de votre expérimentation pour l’exemple de source ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f823d-269">You will also need the **workspace**, **service**, and **api_key** of your experiment for the sample source below.</span></span> <span data-ttu-id="f823d-270">Vous pouvez trouver l’espace de travail et le service en cliquant sur **Requête/réponse** ou **Exécution de lot** pour votre expérimentation dans le tableau de bord de service web.</span><span class="sxs-lookup"><span data-stu-id="f823d-270">You can find the workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in the web service dashboard.</span></span>

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="f823d-272">Vous pouvez trouver **l’api_key** en cliquant sur votre expérimentation dans le tableau de bord de service web.</span><span class="sxs-lookup"><span data-stu-id="f823d-272">You can find the **api_key** by clicking your experiment in the web service dashboard.</span></span>

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="f823d-274">Test du point de terminaison RRS</span><span class="sxs-lookup"><span data-stu-id="f823d-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="f823d-275">Bouton de test</span><span class="sxs-lookup"><span data-stu-id="f823d-275">Test button</span></span>
<span data-ttu-id="f823d-276">Un moyen simple de tester le point de terminaison RRS consiste à cliquer sur **Test** sur le tableau de bord du service web.</span><span class="sxs-lookup"><span data-stu-id="f823d-276">An easy way to test the RRS endpoint is to click **Test** on the web service dashboard.</span></span>

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="f823d-278">Tapez **C’est une belle journée** en **col2**.</span><span class="sxs-lookup"><span data-stu-id="f823d-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="f823d-279">Cliquez sur la coche.</span><span class="sxs-lookup"><span data-stu-id="f823d-279">Click the checkmark.</span></span>

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="f823d-281">Le résultat suivant doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="f823d-281">You will see something like</span></span>

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="f823d-283">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="f823d-283">Sample Code</span></span>
<span data-ttu-id="f823d-284">Vous pouvez également tester votre RRS à partir de votre code client.</span><span class="sxs-lookup"><span data-stu-id="f823d-284">Another way to test your RRS is from your client code.</span></span> <span data-ttu-id="f823d-285">Si vous cliquez sur **Requête/réponse** sur le tableau de bord et faites défiler la liste vers le bas, vous trouverez des exemples de code pour C#, Python et R. Vous trouverez également la syntaxe de la requête RRS, y compris l’URI, les en-têtes et le corps de la requête.</span><span class="sxs-lookup"><span data-stu-id="f823d-285">If you click **Request/response** on the dashboard and scroll to the bottom, you will see sample code for C#, Python, and R. You will also see the syntax of the RRS request, including the request URI, headers, and body.</span></span>

<span data-ttu-id="f823d-286">Ce guide fournit un exemple Python opérationnel.</span><span class="sxs-lookup"><span data-stu-id="f823d-286">This guide shows a working Python example.</span></span> <span data-ttu-id="f823d-287">Vous devrez le modifier avec les **espace de travail**, **service** et **api_key** de votre expérimentation.</span><span class="sxs-lookup"><span data-stu-id="f823d-287">You will need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span>

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("The request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="f823d-288">Test du point de terminaison BES</span><span class="sxs-lookup"><span data-stu-id="f823d-288">Test BES endpoint</span></span>
<span data-ttu-id="f823d-289">Cliquez sur **Exécution de lot** sur le tableau de bord et faites défiler la liste vers le bas.</span><span class="sxs-lookup"><span data-stu-id="f823d-289">Click **Batch execution** on the dashboard and scroll to the bottom.</span></span> <span data-ttu-id="f823d-290">Vous trouverez des exemples de code pour C#, Python et R. Vous trouverez également la syntaxe des requêtes BES pour soumettre une tâche, démarrer une tâche, obtenir l’état ou les résultats d’une tâche et supprimer une tâche.</span><span class="sxs-lookup"><span data-stu-id="f823d-290">You will see sample code for C#, Python, and R. You will also see the syntax of the BES requests to submit a job, start a job, get the status or results of a job, and delete a job.</span></span>

<span data-ttu-id="f823d-291">Ce guide fournit un exemple Python opérationnel.</span><span class="sxs-lookup"><span data-stu-id="f823d-291">This guide shows a working Python example.</span></span> <span data-ttu-id="f823d-292">Vous devez le modifier avec les **espace de travail**, **service** et **api_key** de votre expérimentation.</span><span class="sxs-lookup"><span data-stu-id="f823d-292">You need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="f823d-293">En outre, vous devez modifier les **nom de compte de stockage**, **clé de compte de stockage** et **nom de conteneur de stockage**.</span><span class="sxs-lookup"><span data-stu-id="f823d-293">Additionally, you need to modify the **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="f823d-294">Enfin, vous devez modifier l’emplacement du **fichier d’entrée** et l’emplacement du **fichier de sortie**.</span><span class="sxs-lookup"><span data-stu-id="f823d-294">Lastly, you will need to modify the location of the **input file** and the location of the **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH THE API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH THE LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH THE LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("The request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading the result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written to the file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("The results for " + outputName + " are available at the following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "The results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading the input to blob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded the input to blob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting the job...")
    # submit the job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove the enclosing double-quotes
    print("Job ID: " + job_id)
    # start the job
    print("Starting the job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking the job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in the follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
