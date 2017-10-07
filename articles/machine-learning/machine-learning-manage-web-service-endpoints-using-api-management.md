---
title: "aaaLearn comment toomanage AzureML web services à l’aide de la gestion des API | Documents Microsoft"
description: "Un guide indiquant comment toomanage AzureML web services à l’aide de la gestion des API."
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
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a><span data-ttu-id="681e6-104">Découvrez comment toomanage AzureML web services à l’aide de la gestion des API</span><span class="sxs-lookup"><span data-stu-id="681e6-104">Learn how toomanage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="681e6-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="681e6-105">Overview</span></span>
<span data-ttu-id="681e6-106">Ce guide vous explique comment démarrer tooquickly à l’aide de gestion des API toomanage vos services web de AzureML.</span><span class="sxs-lookup"><span data-stu-id="681e6-106">This guide shows you how tooquickly get started using API Management toomanage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="681e6-107">Qu’est-ce que Gestion des API Azure ?</span><span class="sxs-lookup"><span data-stu-id="681e6-107">What is Azure API Management?</span></span>
<span data-ttu-id="681e6-108">Gestion des API Azure est un service Azure qui vous permet de gérer vos points de terminaison d’API REST en définissant l’accès utilisateur, la limitation d’utilisation et la surveillance du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="681e6-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="681e6-109">Cliquez [ici](https://azure.microsoft.com/services/api-management/) pour plus d’informations sur Gestion des API Azure.</span><span class="sxs-lookup"><span data-stu-id="681e6-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="681e6-110">Cliquez sur [ici](../api-management/api-management-get-started.md) pour obtenir un guide sur comment tooget démarrer avec la gestion des API Azure.</span><span class="sxs-lookup"><span data-stu-id="681e6-110">Click [here](../api-management/api-management-get-started.md) for a guide on how tooget started with Azure API Management.</span></span> <span data-ttu-id="681e6-111">Cet autre guide, sur lequel ce guide est basé, couvre plus de rubriques, notamment les configurations de notification, la tarification, la gestion des réponses, l’authentification des utilisateurs, la création de produits, les abonnements pour développeur et le tableau de bord d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="681e6-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="681e6-112">Présentation d’AzureML</span><span class="sxs-lookup"><span data-stu-id="681e6-112">What is AzureML?</span></span>
<span data-ttu-id="681e6-113">AzureML est un service Azure pour l’apprentissage qui vous permet de tooeasily build, déployer et partager des solutions d’analytique avancée.</span><span class="sxs-lookup"><span data-stu-id="681e6-113">AzureML is an Azure service for machine learning that enables you tooeasily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="681e6-114">Cliquez [ici](https://azure.microsoft.com/services/machine-learning/) pour plus d’informations sur AzureML.</span><span class="sxs-lookup"><span data-stu-id="681e6-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="681e6-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="681e6-115">Prerequisites</span></span>
<span data-ttu-id="681e6-116">toocomplete ce guide, vous devez :</span><span class="sxs-lookup"><span data-stu-id="681e6-116">toocomplete this guide, you need:</span></span>

* <span data-ttu-id="681e6-117">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="681e6-117">An Azure account.</span></span> <span data-ttu-id="681e6-118">Si vous n’avez pas un compte Azure, cliquez sur [ici](https://azure.microsoft.com/pricing/free-trial/) pour plus d’informations sur la façon de toocreate un compte d’évaluation gratuit.</span><span class="sxs-lookup"><span data-stu-id="681e6-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="681e6-119">Un compte AzureML.</span><span class="sxs-lookup"><span data-stu-id="681e6-119">An AzureML account.</span></span> <span data-ttu-id="681e6-120">Si vous n’avez pas un compte AzureML, cliquez sur [ici](https://studio.azureml.net/) pour plus d’informations sur la façon de toocreate un compte d’évaluation gratuit.</span><span class="sxs-lookup"><span data-stu-id="681e6-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="681e6-121">espace de travail Hello, service et api_key pour une expérience AzureML déployée comme un service web.</span><span class="sxs-lookup"><span data-stu-id="681e6-121">hello workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="681e6-122">Cliquez sur [ici](machine-learning-create-experiment.md) pour plus d’informations sur comment toocreate un AzureML faire des essais.</span><span class="sxs-lookup"><span data-stu-id="681e6-122">Click [here](machine-learning-create-experiment.md) for details on how toocreate an AzureML experiment.</span></span> <span data-ttu-id="681e6-123">Cliquez sur [ici](machine-learning-publish-a-machine-learning-web-service.md) pour plus d’informations sur comment toodeploy un AzureML faire des essais en tant qu’un service web.</span><span class="sxs-lookup"><span data-stu-id="681e6-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how toodeploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="681e6-124">Ou bien, l’annexe A comporte des instructions pour toocreate et test d’un simple AzureML tester et déploiement en tant que service web.</span><span class="sxs-lookup"><span data-stu-id="681e6-124">Alternately, Appendix A has instructions for how toocreate and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="681e6-125">Création d'une instance Gestion des API</span><span class="sxs-lookup"><span data-stu-id="681e6-125">Create an API Management instance</span></span>
<span data-ttu-id="681e6-126">Vous trouverez ci-dessous les étapes hello pour à l’aide de la gestion des API toomanage votre service web de AzureML.</span><span class="sxs-lookup"><span data-stu-id="681e6-126">Below are hello steps for using API Management toomanage your AzureML web service.</span></span> <span data-ttu-id="681e6-127">Créez d’abord une instance de service.</span><span class="sxs-lookup"><span data-stu-id="681e6-127">First create a service instance.</span></span> <span data-ttu-id="681e6-128">Connectez-vous à toohello [portail classique](https://manage.windowsazure.com/) et cliquez sur **nouveau** > **des Services d’application** > **gestion des API**  >  **Créer**.</span><span class="sxs-lookup"><span data-stu-id="681e6-128">Log in toohello [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="681e6-130">Spécifiez une **URL** unique.</span><span class="sxs-lookup"><span data-stu-id="681e6-130">Specify a unique **URL**.</span></span> <span data-ttu-id="681e6-131">Ce guide utilise **demoazureml** – vous devez toochoose quelque chose d’autre.</span><span class="sxs-lookup"><span data-stu-id="681e6-131">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="681e6-132">Choisissez hello souhaité **abonnement** et **région** pour votre instance de service.</span><span class="sxs-lookup"><span data-stu-id="681e6-132">Choose hello desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="681e6-133">Après avoir effectué vos sélections, cliquez sur le bouton suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="681e6-133">After making your selections, click hello next button.</span></span>

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="681e6-135">Spécifiez une valeur pour hello **nom de l’organisation**.</span><span class="sxs-lookup"><span data-stu-id="681e6-135">Specify a value for hello **Organization Name**.</span></span> <span data-ttu-id="681e6-136">Ce guide utilise **demoazureml** – vous devez toochoose quelque chose d’autre.</span><span class="sxs-lookup"><span data-stu-id="681e6-136">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="681e6-137">Entrez votre adresse de messagerie dans hello **e-mail administrateur** champ.</span><span class="sxs-lookup"><span data-stu-id="681e6-137">Enter your email address in hello **administrator e-mail** field.</span></span> <span data-ttu-id="681e6-138">Cette adresse de messagerie est utilisée pour les notifications de hello système de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="681e6-138">This email address is used for notifications from hello API Management system.</span></span>

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="681e6-140">Cliquez sur toocreate de case à cocher hello votre instance de service.</span><span class="sxs-lookup"><span data-stu-id="681e6-140">Click hello check box toocreate your service instance.</span></span> <span data-ttu-id="681e6-141">*Elle occupe minutes toothirty pour une nouvelle toobe de service créé*.</span><span class="sxs-lookup"><span data-stu-id="681e6-141">*It takes up toothirty minutes for a new service toobe created*.</span></span>

## <a name="create-hello-api"></a><span data-ttu-id="681e6-142">Créer des API de hello</span><span class="sxs-lookup"><span data-stu-id="681e6-142">Create hello API</span></span>
<span data-ttu-id="681e6-143">Une fois créé, l’instance de service hello hello prochaine étape consiste toocreate hello API.</span><span class="sxs-lookup"><span data-stu-id="681e6-143">Once hello service instance is created, hello next step is toocreate hello API.</span></span> <span data-ttu-id="681e6-144">Une API se compose d’un ensemble d’opérations pouvant être appelées à partir d’une application cliente.</span><span class="sxs-lookup"><span data-stu-id="681e6-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="681e6-145">Opérations d’API sont traitées tooexisting des services web.</span><span class="sxs-lookup"><span data-stu-id="681e6-145">API operations are proxied tooexisting web services.</span></span> <span data-ttu-id="681e6-146">Ce guide crée des API qui toohello proxy des services web AzureML RRS et BES existants.</span><span class="sxs-lookup"><span data-stu-id="681e6-146">This guide creates APIs that proxy toohello existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="681e6-147">API est créés et configurés à partir du portail de publication d’API hello, qui est accessible via le portail classique Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="681e6-147">APIs are created and configured from hello API publisher portal, which is accessed through hello Azure Classic Portal.</span></span> <span data-ttu-id="681e6-148">tooreach hello sélectionnez portail, du serveur de publication de votre instance de service.</span><span class="sxs-lookup"><span data-stu-id="681e6-148">tooreach hello publisher portal, select your service instance.</span></span>

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="681e6-150">Cliquez sur **gérer** Bonjour portail classique Azure pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="681e6-150">Click **Manage** in hello Azure Classic Portal for your API Management service.</span></span>

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="681e6-152">Cliquez sur **API** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **ajouter les API**.</span><span class="sxs-lookup"><span data-stu-id="681e6-152">Click **APIs** from hello **API Management** menu on hello left, and then click **Add API**.</span></span>

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="681e6-154">Type **AzureML démonstration API** comme hello **nom de l’API Web**.</span><span class="sxs-lookup"><span data-stu-id="681e6-154">Type **AzureML Demo API** as hello **Web API name**.</span></span> <span data-ttu-id="681e6-155">Type **https://ussouthcentral.services.azureml.net** comme hello **URL du service Web**.</span><span class="sxs-lookup"><span data-stu-id="681e6-155">Type **https://ussouthcentral.services.azureml.net** as hello **Web service URL**.</span></span> <span data-ttu-id="681e6-156">Type **azureml-demo** comme hello **suffixe d’URL d’API Web**.</span><span class="sxs-lookup"><span data-stu-id="681e6-156">Type **azureml-demo** as hello **Web API URL suffix**.</span></span> <span data-ttu-id="681e6-157">Vérifiez **HTTPS** comme hello **URL d’API Web** schéma.</span><span class="sxs-lookup"><span data-stu-id="681e6-157">Check **HTTPS** as hello **Web API URL** scheme.</span></span> <span data-ttu-id="681e6-158">Sélectionnez **Starter** comme **produit**.</span><span class="sxs-lookup"><span data-stu-id="681e6-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="681e6-159">Lorsque vous avez terminé, cliquez sur **enregistrer** toocreate hello API.</span><span class="sxs-lookup"><span data-stu-id="681e6-159">When finished, click **Save** toocreate hello API.</span></span>

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a><span data-ttu-id="681e6-161">Ajouter des opérations de hello</span><span class="sxs-lookup"><span data-stu-id="681e6-161">Add hello operations</span></span>
<span data-ttu-id="681e6-162">Cliquez sur **l’opération d’ajout** tooadd operations toothis API.</span><span class="sxs-lookup"><span data-stu-id="681e6-162">Click **Add operation** tooadd operations toothis API.</span></span>

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="681e6-164">Hello **nouvelle opération** fenêtre s’affiche et hello **Signature** est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="681e6-164">hello **New operation** window will be displayed and hello **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="681e6-165">Ajout d’une opération RRS</span><span class="sxs-lookup"><span data-stu-id="681e6-165">Add RRS Operation</span></span>
<span data-ttu-id="681e6-166">Tout d’abord créer une opération de service de AzureML RRS de hello.</span><span class="sxs-lookup"><span data-stu-id="681e6-166">First create an operation for hello AzureML RRS service.</span></span> <span data-ttu-id="681e6-167">Sélectionnez **POST** comme hello **verbe HTTP**.</span><span class="sxs-lookup"><span data-stu-id="681e6-167">Select **POST** as hello **HTTP verb**.</span></span> <span data-ttu-id="681e6-168">Type **/workspaces/ {espace de travail} /services/ {service} / exécuter ? api-version = {apiversion} & détails = {détails}** comme hello **modèle d’URL**.</span><span class="sxs-lookup"><span data-stu-id="681e6-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as hello **URL template**.</span></span> <span data-ttu-id="681e6-169">Type **RR exécuter** comme hello **nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="681e6-169">Type **RRS Execute** as hello **Display name**.</span></span>

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="681e6-171">Cliquez sur **réponses** > **ajouter** sur hello gauche et sélectionnez **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="681e6-171">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="681e6-172">Cliquez sur **enregistrer** toosave cette opération.</span><span class="sxs-lookup"><span data-stu-id="681e6-172">Click **Save** toosave this operation.</span></span>

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="681e6-174">Ajout d’opérations BES</span><span class="sxs-lookup"><span data-stu-id="681e6-174">Add BES Operations</span></span>
<span data-ttu-id="681e6-175">Captures d’écran ne sont pas incluses pour hello les opérations BES lorsqu’ils sont toothose très similaire pour l’ajout d’opération de RR hello.</span><span class="sxs-lookup"><span data-stu-id="681e6-175">Screenshots are not included for hello BES operations as they are very similar toothose for adding hello RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="681e6-176">Envoi (et non démarrage) d’un travail d’exécution de lot</span><span class="sxs-lookup"><span data-stu-id="681e6-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="681e6-177">Cliquez sur **l’opération d’ajout** tooadd hello AzureML BES opération toohello API.</span><span class="sxs-lookup"><span data-stu-id="681e6-177">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="681e6-178">Sélectionnez **POST** pour hello **verbe HTTP**.</span><span class="sxs-lookup"><span data-stu-id="681e6-178">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="681e6-179">Type **/workspaces/ {espace de travail} /services/ {service} / travaux ? api-version = {apiversion}** pour hello **modèle d’URL**.</span><span class="sxs-lookup"><span data-stu-id="681e6-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="681e6-180">Type **BES soumettre** pour hello **nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="681e6-180">Type **BES Submit** for hello **Display name**.</span></span> <span data-ttu-id="681e6-181">Cliquez sur **réponses** > **ajouter** sur hello gauche et sélectionnez **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="681e6-181">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="681e6-182">Cliquez sur **enregistrer** toosave cette opération.</span><span class="sxs-lookup"><span data-stu-id="681e6-182">Click **Save** toosave this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="681e6-183">Démarrage d’une tâche d’exécution de lot</span><span class="sxs-lookup"><span data-stu-id="681e6-183">Start a Batch Execution job</span></span>
<span data-ttu-id="681e6-184">Cliquez sur **l’opération d’ajout** tooadd hello AzureML BES opération toohello API.</span><span class="sxs-lookup"><span data-stu-id="681e6-184">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="681e6-185">Sélectionnez **POST** pour hello **verbe HTTP**.</span><span class="sxs-lookup"><span data-stu-id="681e6-185">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="681e6-186">Type **/workspaces/ {espace de travail} /services/ {service} /jobs/ {jobid} / démarrer ? api-version = {apiversion}** pour hello **modèle d’URL**.</span><span class="sxs-lookup"><span data-stu-id="681e6-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="681e6-187">Type **BES Démarrer** pour hello **nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="681e6-187">Type **BES Start** for hello **Display name**.</span></span> <span data-ttu-id="681e6-188">Cliquez sur **réponses** > **ajouter** sur hello gauche et sélectionnez **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="681e6-188">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="681e6-189">Cliquez sur **enregistrer** toosave cette opération.</span><span class="sxs-lookup"><span data-stu-id="681e6-189">Click **Save** toosave this operation.</span></span>

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="681e6-190">Obtenir l’état de hello ou le résultat d’une tâche d’exécution de lot</span><span class="sxs-lookup"><span data-stu-id="681e6-190">Get hello status or result of a Batch Execution job</span></span>
<span data-ttu-id="681e6-191">Cliquez sur **l’opération d’ajout** tooadd hello AzureML BES opération toohello API.</span><span class="sxs-lookup"><span data-stu-id="681e6-191">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="681e6-192">Sélectionnez **obtenir** pour hello **verbe HTTP**.</span><span class="sxs-lookup"><span data-stu-id="681e6-192">Select **GET** for hello **HTTP verb**.</span></span> <span data-ttu-id="681e6-193">Type **/workspaces/ {espace de travail} /services/ {service} /jobs/ {jobid} ? api-version = {apiversion}** pour hello **modèle d’URL**.</span><span class="sxs-lookup"><span data-stu-id="681e6-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="681e6-194">Type **BES état** pour hello **nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="681e6-194">Type **BES Status** for hello **Display name**.</span></span> <span data-ttu-id="681e6-195">Cliquez sur **réponses** > **ajouter** sur hello gauche et sélectionnez **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="681e6-195">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="681e6-196">Cliquez sur **enregistrer** toosave cette opération.</span><span class="sxs-lookup"><span data-stu-id="681e6-196">Click **Save** toosave this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="681e6-197">Suppression d’une tâche d’exécution de lot</span><span class="sxs-lookup"><span data-stu-id="681e6-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="681e6-198">Cliquez sur **l’opération d’ajout** tooadd hello AzureML BES opération toohello API.</span><span class="sxs-lookup"><span data-stu-id="681e6-198">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="681e6-199">Sélectionnez **supprimer** pour hello **verbe HTTP**.</span><span class="sxs-lookup"><span data-stu-id="681e6-199">Select **DELETE** for hello **HTTP verb**.</span></span> <span data-ttu-id="681e6-200">Type **/workspaces/ {espace de travail} /services/ {service} /jobs/ {jobid} ? api-version = {apiversion}** pour hello **modèle d’URL**.</span><span class="sxs-lookup"><span data-stu-id="681e6-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="681e6-201">Type **BES supprimer** pour hello **nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="681e6-201">Type **BES Delete** for hello **Display name**.</span></span> <span data-ttu-id="681e6-202">Cliquez sur **réponses** > **ajouter** sur hello gauche et sélectionnez **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="681e6-202">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="681e6-203">Cliquez sur **enregistrer** toosave cette opération.</span><span class="sxs-lookup"><span data-stu-id="681e6-203">Click **Save** toosave this operation.</span></span>

## <a name="call-an-operation-from-hello-developer-portal"></a><span data-ttu-id="681e6-204">Appeler une opération de hello portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="681e6-204">Call an operation from hello Developer Portal</span></span>
<span data-ttu-id="681e6-205">Opérations peuvent être appelées directement depuis le portail des développeurs hello, qui fournit un moyen pratique de tooview et tester le fonctionnement d’une API hello.</span><span class="sxs-lookup"><span data-stu-id="681e6-205">Operations can be called directly from hello Developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="681e6-206">Dans cette étape du guide, vous appelez hello **RR exécuter** méthode qui a été ajouté toohello **AzureML démonstration API**.</span><span class="sxs-lookup"><span data-stu-id="681e6-206">In this guide step you will call hello **RRS Execute** method that was added toohello **AzureML Demo API**.</span></span> <span data-ttu-id="681e6-207">Cliquez sur **portail des développeurs** à partir du menu de hello en hello haut à droite de hello portail classique.</span><span class="sxs-lookup"><span data-stu-id="681e6-207">Click **Developer portal** from hello menu at hello top right of hello Classic Portal.</span></span>

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="681e6-209">Cliquez sur **API** dans le menu du haut hello, puis cliquez sur **AzureML démonstration API** opérations de hello toosee disponibles.</span><span class="sxs-lookup"><span data-stu-id="681e6-209">Click **APIs** from hello top menu, and then click **AzureML Demo API** toosee hello operations available.</span></span>

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="681e6-211">Sélectionnez **RR exécuter** pour l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="681e6-211">Select **RRS Execute** for hello operation.</span></span> <span data-ttu-id="681e6-212">Cliquez sur **Essayer**.</span><span class="sxs-lookup"><span data-stu-id="681e6-212">Click **Try It**.</span></span>

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="681e6-214">Pour les paramètres de requête, tapez votre **espace de travail**, **service**, **2.0** pour hello **apiversion**, et **true**pour hello **détails**.</span><span class="sxs-lookup"><span data-stu-id="681e6-214">For Request parameters, type your **workspace**,  **service**, **2.0** for hello **apiversion**, and  **true** for hello **details**.</span></span> <span data-ttu-id="681e6-215">Vous pouvez trouver votre **espace de travail** et **service** dans le tableau de bord hello AzureML web service (consultez **tester un service web de hello** dans l’annexe A).</span><span class="sxs-lookup"><span data-stu-id="681e6-215">You can find your **workspace** and **service** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="681e6-216">Pour les en-têtes de requête, cliquez sur **Ajouter en-tête** et tapez **Content-Type** et **application/json**, puis cliquez sur **Ajouter en-tête** et tapez **Autorisation** et **Porteur<YOUR AZUREML SERVICE API-KEY>**.</span><span class="sxs-lookup"><span data-stu-id="681e6-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="681e6-217">Vous pouvez trouver votre **clé api** dans le tableau de bord hello AzureML web service (consultez **tester un service web de hello** dans l’annexe A).</span><span class="sxs-lookup"><span data-stu-id="681e6-217">You can find your **api key** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="681e6-218">Type **{« Entrées » : {« entrée1 » : {« ColumnNames » : « Valeurs » [« Col2 »] : [[« Ceci est une bonne journée »]]}}, « GlobalParameters » : {}}** hello corps de requête.</span><span class="sxs-lookup"><span data-stu-id="681e6-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for hello request body.</span></span>

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="681e6-220">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="681e6-220">Click **Send**.</span></span>

![Envoyer](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="681e6-222">Une fois une opération est appelée, le portail des développeurs hello affiche hello **URL demandée** à partir du service principal de hello, hello **état de la réponse**, hello **les en-têtes de réponse**, et n’importe quel **contenu de la réponse**.</span><span class="sxs-lookup"><span data-stu-id="681e6-222">After an operation is invoked, hello developer portal displays hello **Requested URL** from hello back-end service, hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="681e6-224">Annexe A - Création et test d’un service web AzureML simple</span><span class="sxs-lookup"><span data-stu-id="681e6-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-hello-experiment"></a><span data-ttu-id="681e6-225">Création d’expérience de hello</span><span class="sxs-lookup"><span data-stu-id="681e6-225">Creating hello experiment</span></span>
<span data-ttu-id="681e6-226">Vous trouverez ci-dessous les étapes de hello pour la création d’une expérience simple de AzureML et de les déployer comme un service web.</span><span class="sxs-lookup"><span data-stu-id="681e6-226">Below are hello steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="681e6-227">Hello web service prend comme entrée une colonne de texte arbitraire et retourne un jeu de fonctionnalités représentées en tant qu’entiers.</span><span class="sxs-lookup"><span data-stu-id="681e6-227">hello web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="681e6-228">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="681e6-228">For example:</span></span>

| <span data-ttu-id="681e6-229">Texte</span><span class="sxs-lookup"><span data-stu-id="681e6-229">Text</span></span> | <span data-ttu-id="681e6-230">Texte haché</span><span class="sxs-lookup"><span data-stu-id="681e6-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="681e6-231">C’est une belle journée</span><span class="sxs-lookup"><span data-stu-id="681e6-231">This is a good day</span></span> |<span data-ttu-id="681e6-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="681e6-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="681e6-233">Tout d’abord, à l’aide d’un navigateur de votre choix, accédez à : [https://studio.azureml.net/](https://studio.azureml.net/) et entrez votre toolog des informations d’identification dans.</span><span class="sxs-lookup"><span data-stu-id="681e6-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials toolog in.</span></span> <span data-ttu-id="681e6-234">Ensuite, créez une nouvelle expérience vide.</span><span class="sxs-lookup"><span data-stu-id="681e6-234">Next, create a new blank experiment.</span></span>

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="681e6-236">Renommez-le trop**SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="681e6-236">Rename it too**SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="681e6-237">Développez **Datasets enregistrés** et faites glisser **Critiques de livres d’Amazon** sur votre expérimentation.</span><span class="sxs-lookup"><span data-stu-id="681e6-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="681e6-239">Développez **Transformation des données** et **Manipulation** et faites glisser **Sélectionner des colonnes dans le jeu de données** sur votre expérimentation.</span><span class="sxs-lookup"><span data-stu-id="681e6-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="681e6-240">Se connecter **critiques à partir d’Amazon** trop**sélectionner les colonnes dans le jeu de données**.</span><span class="sxs-lookup"><span data-stu-id="681e6-240">Connect **Book Reviews from Amazon** too**Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="681e6-242">Cliquez sur **Sélectionner des colonnes dans le jeu de données**, puis sur **Exécuter le sélecteur de colonne** et sélectionnez **Col2**.</span><span class="sxs-lookup"><span data-stu-id="681e6-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="681e6-243">Cliquez sur hello coche tooapply ces modifications.</span><span class="sxs-lookup"><span data-stu-id="681e6-243">Click hello checkmark tooapply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="681e6-245">Développez **texte Analytique** et faites glisser **Feature Hashing** sur l’expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="681e6-245">Expand **Text Analytics** and drag **Feature Hashing** onto hello experiment.</span></span> <span data-ttu-id="681e6-246">Se connecter **sélectionner les colonnes dans le jeu de données** trop**Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="681e6-246">Connect **Select Columns in Dataset** too**Feature Hashing**.</span></span>

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="681e6-248">Type **3** pour hello **taille de bit hachage**.</span><span class="sxs-lookup"><span data-stu-id="681e6-248">Type **3** for hello **Hashing bitsize**.</span></span> <span data-ttu-id="681e6-249">Cela crée 8 (23) colonnes.</span><span class="sxs-lookup"><span data-stu-id="681e6-249">This will create 8 (23) columns.</span></span>

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="681e6-251">À ce stade, vous souhaiterez peut-être tooclick **exécuter** expérience de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="681e6-251">At this point, you may want tooclick **Run** tootest hello experiment.</span></span>

![Exécuter](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="681e6-253">Création d’un service web</span><span class="sxs-lookup"><span data-stu-id="681e6-253">Create a web service</span></span>
<span data-ttu-id="681e6-254">Maintenant, créez un service web.</span><span class="sxs-lookup"><span data-stu-id="681e6-254">Now create a web service.</span></span> <span data-ttu-id="681e6-255">Développez **Service Web** et faites glisser **Entrée** sur votre expérimentation.</span><span class="sxs-lookup"><span data-stu-id="681e6-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="681e6-256">Se connecter **entrée** trop**Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="681e6-256">Connect **Input** too**Feature Hashing**.</span></span> <span data-ttu-id="681e6-257">Faites également glisser **Sortie** sur votre expérience.</span><span class="sxs-lookup"><span data-stu-id="681e6-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="681e6-258">Se connecter **sortie** trop**Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="681e6-258">Connect **Output** too**Feature Hashing**.</span></span>

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="681e6-260">Cliquez sur **Publier le service Web**.</span><span class="sxs-lookup"><span data-stu-id="681e6-260">Click **Publish web service**.</span></span>

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="681e6-262">Cliquez sur **Oui** expérience de hello toopublish.</span><span class="sxs-lookup"><span data-stu-id="681e6-262">Click **Yes** toopublish hello experiment.</span></span>

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a><span data-ttu-id="681e6-264">Tester un service web de hello</span><span class="sxs-lookup"><span data-stu-id="681e6-264">Test hello web service</span></span>
<span data-ttu-id="681e6-265">Un service web AzureML se compose de points de terminaison RRS (service de requête/réponse) et BES (service d’exécution de lot).</span><span class="sxs-lookup"><span data-stu-id="681e6-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="681e6-266">RSS est conçu pour l’exécution synchrone.</span><span class="sxs-lookup"><span data-stu-id="681e6-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="681e6-267">BES est conçu pour l’exécution de tâches asynchrone.</span><span class="sxs-lookup"><span data-stu-id="681e6-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="681e6-268">tootest votre site web de service avec une source de Python hello exemple ci-dessous, vous devrez peut-être toodownload et installation Bonjour Azure SDK pour Python (voir : [comment tooinstall Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="681e6-268">tootest your web service with hello sample Python source below, you may need toodownload and install hello Azure SDK for Python (see: [How tooinstall Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="681e6-269">Vous devez également hello **espace de travail**, **service**, et **api_key** de votre expérience pour la source d’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="681e6-269">You will also need hello **workspace**, **service**, and **api_key** of your experiment for hello sample source below.</span></span> <span data-ttu-id="681e6-270">Vous pouvez trouver l’espace de travail hello et le service en cliquant sur **demande/réponse** ou **l’exécution par lots** pour votre expérience dans le tableau de bord hello web service.</span><span class="sxs-lookup"><span data-stu-id="681e6-270">You can find hello workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in hello web service dashboard.</span></span>

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="681e6-272">Vous pouvez trouver hello **api_key** en cliquant sur votre expérience dans le tableau de bord hello web service.</span><span class="sxs-lookup"><span data-stu-id="681e6-272">You can find hello **api_key** by clicking your experiment in hello web service dashboard.</span></span>

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="681e6-274">Test du point de terminaison RRS</span><span class="sxs-lookup"><span data-stu-id="681e6-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="681e6-275">Bouton de test</span><span class="sxs-lookup"><span data-stu-id="681e6-275">Test button</span></span>
<span data-ttu-id="681e6-276">Un point de terminaison facilement tootest hello RR est tooclick **Test** sur le tableau de bord hello web service.</span><span class="sxs-lookup"><span data-stu-id="681e6-276">An easy way tootest hello RRS endpoint is tooclick **Test** on hello web service dashboard.</span></span>

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="681e6-278">Tapez **C’est une belle journée** en **col2**.</span><span class="sxs-lookup"><span data-stu-id="681e6-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="681e6-279">Cliquez sur hello coche.</span><span class="sxs-lookup"><span data-stu-id="681e6-279">Click hello checkmark.</span></span>

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="681e6-281">Le résultat suivant doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="681e6-281">You will see something like</span></span>

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="681e6-283">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="681e6-283">Sample Code</span></span>
<span data-ttu-id="681e6-284">Une autre façon tootest vos enregistrements de ressources est à partir de votre code client.</span><span class="sxs-lookup"><span data-stu-id="681e6-284">Another way tootest your RRS is from your client code.</span></span> <span data-ttu-id="681e6-285">Si vous cliquez sur **demande/réponse** sur hello du tableau de bord et défilement toohello bas, vous verrez les exemples de code pour c#, Python et R. Vous verrez également la syntaxe hello de hello RR demande, y compris les URI de demande hello, en-têtes et corps.</span><span class="sxs-lookup"><span data-stu-id="681e6-285">If you click **Request/response** on hello dashboard and scroll toohello bottom, you will see sample code for C#, Python, and R. You will also see hello syntax of hello RRS request, including hello request URI, headers, and body.</span></span>

<span data-ttu-id="681e6-286">Ce guide fournit un exemple Python opérationnel.</span><span class="sxs-lookup"><span data-stu-id="681e6-286">This guide shows a working Python example.</span></span> <span data-ttu-id="681e6-287">Vous devez toomodify avec hello **espace de travail**, **service**, et **api_key** de votre expérience.</span><span class="sxs-lookup"><span data-stu-id="681e6-287">You will need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span>

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
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="681e6-288">Test du point de terminaison BES</span><span class="sxs-lookup"><span data-stu-id="681e6-288">Test BES endpoint</span></span>
<span data-ttu-id="681e6-289">Cliquez sur **l’exécution du lot** sur hello du tableau de bord et défilement toohello bas.</span><span class="sxs-lookup"><span data-stu-id="681e6-289">Click **Batch execution** on hello dashboard and scroll toohello bottom.</span></span> <span data-ttu-id="681e6-290">Vous verrez un exemple de code pour c#, Python et R. Vous verrez également syntaxe hello de hello BES demandes toosubmit un travail, démarrer une tâche, obtenir le statut de hello ou les résultats d’une tâche et supprimer un travail.</span><span class="sxs-lookup"><span data-stu-id="681e6-290">You will see sample code for C#, Python, and R. You will also see hello syntax of hello BES requests toosubmit a job, start a job, get hello status or results of a job, and delete a job.</span></span>

<span data-ttu-id="681e6-291">Ce guide fournit un exemple Python opérationnel.</span><span class="sxs-lookup"><span data-stu-id="681e6-291">This guide shows a working Python example.</span></span> <span data-ttu-id="681e6-292">Vous devez toomodify avec hello **espace de travail**, **service**, et **api_key** de votre expérience.</span><span class="sxs-lookup"><span data-stu-id="681e6-292">You need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="681e6-293">En outre, vous devez toomodify hello **nom de compte de stockage**, **clé de compte de stockage**, et **nom de conteneur de stockage**.</span><span class="sxs-lookup"><span data-stu-id="681e6-293">Additionally, you need toomodify hello **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="681e6-294">Enfin, vous aurez besoin d’emplacement de hello toomodify Hello **fichier d’entrée** et l’emplacement de hello Hello **fichier de sortie**.</span><span class="sxs-lookup"><span data-stu-id="681e6-294">Lastly, you will need toomodify hello location of hello **input file** and hello location of hello **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
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
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
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
