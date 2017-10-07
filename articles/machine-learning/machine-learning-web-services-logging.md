---
title: aaaLogging pour les services web Machine Learning | Documents Microsoft
description: "Découvrez comment les services web tooenable la journalisation pour l’apprentissage. Journalisation fournit des informations supplémentaires toohelp dépanner hello API."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="41a5f-104">Activation de la journalisation pour les services Web de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="41a5f-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="41a5f-105">Ce document fournit des informations sur hello journalisation capacité de services web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="41a5f-105">This document provides information on hello logging capability of Machine Learning web services.</span></span> <span data-ttu-id="41a5f-106">Journalisation fournit des informations supplémentaires, au-delà d’un numéro d’erreur et un message, qui peut vous aider à résoudre les problèmes de votre toohello d’appels API de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="41a5f-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls toohello Machine Learning APIs.</span></span>  

## <a name="how-tooenable-logging-for-a-web-service"></a><span data-ttu-id="41a5f-107">Comment tooenable la journalisation pour un service Web</span><span class="sxs-lookup"><span data-stu-id="41a5f-107">How tooenable logging for a Web service</span></span>

<span data-ttu-id="41a5f-108">Vous activez la journalisation dans hello [Azure Machine Learning Services Web](https://services.azureml.net) portail.</span><span class="sxs-lookup"><span data-stu-id="41a5f-108">You enable logging from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="41a5f-109">Connectez-vous au portail de Services Web de Azure Machine Learning toohello à [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="41a5f-109">Sign in toohello Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="41a5f-110">Pour un service web standard, vous pouvez également obtenir toohello portail en cliquant sur **nouvelle expérience de Services Web** sur la page des Services Web de Machine Learning hello dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="41a5f-110">For a Classic web service, you can also get toohello portal by clicking **New Web Services Experience** on hello Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Lien Nouvelle expérience de services web](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="41a5f-112">Dans la barre de menus supérieure hello, cliquez sur **Services Web** pour un nouveau service web, ou cliquez sur **classique des Services Web** pour un classique de service web.</span><span class="sxs-lookup"><span data-stu-id="41a5f-112">On hello top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Sélectionner les services web nouveaux ou classiques](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="41a5f-114">Pour un service web, cliquez sur le nom du service web hello.</span><span class="sxs-lookup"><span data-stu-id="41a5f-114">For a New web service, click hello web service name.</span></span> <span data-ttu-id="41a5f-115">Pour un service web standard, cliquez sur le nom du service web hello, puis cliquez sur la page suivante de hello point de terminaison approprié hello.</span><span class="sxs-lookup"><span data-stu-id="41a5f-115">For a Classic web service, click hello web service name and then on hello next page click hello appropriate endpoint.</span></span>

4. <span data-ttu-id="41a5f-116">Dans la barre de menus supérieure hello, cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="41a5f-116">On hello top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="41a5f-117">Ensemble hello **activer la journalisation** option trop*erreur* (toolog les erreurs uniquement) ou *tous les* (pour la journalisation complète).</span><span class="sxs-lookup"><span data-stu-id="41a5f-117">Set hello **Enable Logging** option too*Error* (toolog only errors) or *All* (for full logging).</span></span>

   ![Sélectionner le niveau de journalisation](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="41a5f-119">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="41a5f-119">Click **Save**.</span></span>

7. <span data-ttu-id="41a5f-120">Pour les services web standard créer hello **ml-diagnostics** conteneur.</span><span class="sxs-lookup"><span data-stu-id="41a5f-120">For Classic web services, create hello **ml-diagnostics** container.</span></span>

   <span data-ttu-id="41a5f-121">Tous les journaux de service web sont conservés dans un conteneur d’objets blob nommé **ml-diagnostics** hello compte de stockage associé au service web de hello.</span><span class="sxs-lookup"><span data-stu-id="41a5f-121">All web service logs are kept in a blob container named **ml-diagnostics** in hello storage account associated with hello web service.</span></span> <span data-ttu-id="41a5f-122">Pour les nouveaux services web, ce conteneur est créé hello lors du premier qu'accès de service web de hello.</span><span class="sxs-lookup"><span data-stu-id="41a5f-122">For New web services, this container is created hello first time you access hello web service.</span></span> <span data-ttu-id="41a5f-123">Pour les services web standard, vous avez besoin de conteneur de hello toocreate s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="41a5f-123">For Classic web services, you need toocreate hello container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="41a5f-124">Bonjour [portail Azure](https://portal.azure.com), accédez toohello compte de stockage associé au service web de hello.</span><span class="sxs-lookup"><span data-stu-id="41a5f-124">In hello [Azure portal](https://portal.azure.com), go toohello storage account associated with hello web service.</span></span>

   2. <span data-ttu-id="41a5f-125">Sous **Service Blob**, cliquez sur **Conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="41a5f-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="41a5f-126">Si le conteneur de hello **ml-diagnostics** n’existe pas, cliquez sur **+ conteneur**, donnez à hello conteneur hello nom « ml-diagnostics » et sélectionnez hello **type d’accès** en tant que « Blob ».</span><span class="sxs-lookup"><span data-stu-id="41a5f-126">If hello container **ml-diagnostics** doesn't exist, click **+Container**, give hello container hello name "ml-diagnostics", and select hello **Access type** as "Blob".</span></span> <span data-ttu-id="41a5f-127">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="41a5f-127">Click **OK**.</span></span>

      ![Sélectionner le niveau de journalisation](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="41a5f-129">Pour un service web classique, hello Web Services du tableau de bord dans Machine Learning Studio dotée d’un commutateur de tooenable la journalisation.</span><span class="sxs-lookup"><span data-stu-id="41a5f-129">For a Classic web service, hello Web Services Dashboard in Machine Learning Studio also has a switch tooenable logging.</span></span> <span data-ttu-id="41a5f-130">Toutefois, étant donné que la journalisation est gérée via le portail de Services Web hello, vous devez tooenable journalisation via le portail hello comme décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="41a5f-130">However, because logging is now managed through hello Web Services portal, you need tooenable logging through hello portal as described in this article.</span></span> <span data-ttu-id="41a5f-131">Si vous déjà activé l’enregistrement dans Studio, puis dans le portail de Services Web de hello, désactiver la journalisation, puis réactivez-la.</span><span class="sxs-lookup"><span data-stu-id="41a5f-131">If you already enabled logging in Studio, then in hello Web Services Portal, disable logging and enable it again.</span></span>


## <a name="hello-effects-of-enabling-logging"></a><span data-ttu-id="41a5f-132">effets Hello d’activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="41a5f-132">hello effects of enabling logging</span></span>
<span data-ttu-id="41a5f-133">Lorsque la journalisation est activée, les erreurs à partir du point de terminaison de service hello web et diagnostics de hello sont enregistrés dans hello **ml-diagnostics** conteneur d’objets blob dans le compte de stockage Azure de hello lié avec l’espace de travail de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="41a5f-133">When logging is enabled, hello diagnostics and errors from hello web service endpoint are logged in hello **ml-diagnostics** blob container in hello Azure Storage Account linked with hello user’s workspace.</span></span> <span data-ttu-id="41a5f-134">Ce conteneur conserve toutes les informations de diagnostics de hello pour tous les postes clients hello web service pour tous les espaces de travail hello associés à ce compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="41a5f-134">This container holds all hello diagnostics information for all hello web service endpoints for all hello workspaces associated with this storage account.</span></span>

<span data-ttu-id="41a5f-135">Hello journaux peuvent être affichés à l’aide de hello plusieurs outils tooexplore à disposition un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="41a5f-135">hello logs can be viewed using any of hello several tools available tooexplore an Azure Storage Account.</span></span> <span data-ttu-id="41a5f-136">Hello plus simple peut être le compte de stockage toohello toonavigate hello portail Azure, cliquez sur **conteneurs**, puis cliquez sur le conteneur de hello **ml-diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="41a5f-136">hello easiest may be toonavigate toohello storage account in hello Azure portal, click **Containers**, and then click hello container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="41a5f-137">Journaliser les informations détaillées sur l’objet blob</span><span class="sxs-lookup"><span data-stu-id="41a5f-137">Log blob detail information</span></span>
<span data-ttu-id="41a5f-138">Chaque objet blob dans le conteneur de hello conserve des informations de diagnostics hello pour un seul de hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="41a5f-138">Each blob in hello container holds hello diagnostics information for exactly one of hello following actions:</span></span>

* <span data-ttu-id="41a5f-139">L’exécution de la méthode hello lot en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="41a5f-139">An execution of hello Batch-Execution method</span></span>  
* <span data-ttu-id="41a5f-140">L’exécution de la méthode hello demande-réponse</span><span class="sxs-lookup"><span data-stu-id="41a5f-140">An execution of hello Request-Response method</span></span>  
* <span data-ttu-id="41a5f-141">l’initialisation d'un conteneur de requête-réponse</span><span class="sxs-lookup"><span data-stu-id="41a5f-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="41a5f-142">nom Hello de chaque objet blob a un préfixe de hello suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="41a5f-142">hello name of each blob has a prefix of hello following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="41a5f-143">Où _type journal_ est une des valeurs suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="41a5f-143">Where _Log type_ is one of hello following values:</span></span>  

* <span data-ttu-id="41a5f-144">lot</span><span class="sxs-lookup"><span data-stu-id="41a5f-144">batch</span></span>  
* <span data-ttu-id="41a5f-145">score/requests</span><span class="sxs-lookup"><span data-stu-id="41a5f-145">score/requests</span></span>  
* <span data-ttu-id="41a5f-146">score/init</span><span class="sxs-lookup"><span data-stu-id="41a5f-146">score/init</span></span>  

