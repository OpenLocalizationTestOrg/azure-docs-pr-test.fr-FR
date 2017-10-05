---
title: Journalisation pour les services web Machine Learning | Microsoft Docs
description: "Découvrez comment activer la journalisation pour les services Web de Machine Learning. La journalisation fournit des informations supplémentaires pour vous aider à résoudre les problèmes des API."
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
ms.openlocfilehash: 7d0b2db01427430d6b0a317cdfefc265dd4b06e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="77b35-104">Activation de la journalisation pour les services Web de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="77b35-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="77b35-105">Ce document fournit des informations sur la fonctionnalité de journalisation des services web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="77b35-105">This document provides information on the logging capability of Machine Learning web services.</span></span> <span data-ttu-id="77b35-106">La journalisation fournit des informations supplémentaires, au-delà d’un numéro et d’un message d’erreur, qui peuvent vous aider à résoudre des problèmes liés à vos appels aux API Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="77b35-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls to the Machine Learning APIs.</span></span>  

## <a name="how-to-enable-logging-for-a-web-service"></a><span data-ttu-id="77b35-107">Comment activer la journalisation pour un service web</span><span class="sxs-lookup"><span data-stu-id="77b35-107">How to enable logging for a Web service</span></span>

<span data-ttu-id="77b35-108">Vous activez la journalisation à partir du portail des [services web Azure Machine Learning](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="77b35-108">You enable logging from the [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="77b35-109">Connectez-vous au portail des services web Azure Machine Learning à l’adresse [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="77b35-109">Sign in to the Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="77b35-110">Pour un service web classique, vous pouvez également accéder au portail en cliquant sur **Nouvelle expérience de services web** dans la page des services web Machine Learning dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="77b35-110">For a Classic web service, you can also get to the portal by clicking **New Web Services Experience** on the Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Lien Nouvelle expérience de services web](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="77b35-112">Dans la barre de menus supérieure, cliquez sur **Services web** pour un nouveau service web, ou sur **Services web classiques** pour un service web classique.</span><span class="sxs-lookup"><span data-stu-id="77b35-112">On the top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Sélectionner les services web nouveaux ou classiques](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="77b35-114">Pour un nouveau service web, cliquez sur son nom.</span><span class="sxs-lookup"><span data-stu-id="77b35-114">For a New web service, click the web service name.</span></span> <span data-ttu-id="77b35-115">Pour un service web classique, cliquez sur son nom, puis, dans la page suivante, sur le point de terminaison approprié.</span><span class="sxs-lookup"><span data-stu-id="77b35-115">For a Classic web service, click the web service name and then on the next page click the appropriate endpoint.</span></span>

4. <span data-ttu-id="77b35-116">Dans la barre de menus supérieure, cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="77b35-116">On the top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="77b35-117">Définissez l’option **Activer la journalisation** sur *Erreur* (pour journaliser uniquement les erreurs) ou sur *Tout* (pour une journalisation complète).</span><span class="sxs-lookup"><span data-stu-id="77b35-117">Set the **Enable Logging** option to *Error* (to log only errors) or *All* (for full logging).</span></span>

   ![Sélectionner le niveau de journalisation](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="77b35-119">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="77b35-119">Click **Save**.</span></span>

7. <span data-ttu-id="77b35-120">Pour les services web classiques, créez le conteneur **ml-diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="77b35-120">For Classic web services, create the **ml-diagnostics** container.</span></span>

   <span data-ttu-id="77b35-121">Tous les journaux du service web sont conservés dans un conteneur d’objets blob nommé **ml-diagnostics** dans le compte de stockage associé au service web.</span><span class="sxs-lookup"><span data-stu-id="77b35-121">All web service logs are kept in a blob container named **ml-diagnostics** in the storage account associated with the web service.</span></span> <span data-ttu-id="77b35-122">Pour les nouveaux services web, ce conteneur est créé la première fois que vous accédez au service.</span><span class="sxs-lookup"><span data-stu-id="77b35-122">For New web services, this container is created the first time you access the web service.</span></span> <span data-ttu-id="77b35-123">Pour les services web classiques, vous devez créer le conteneur s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="77b35-123">For Classic web services, you need to create the container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="77b35-124">Dans le [portail Azure](https://portal.azure.com), accédez au compte de stockage associé au service web.</span><span class="sxs-lookup"><span data-stu-id="77b35-124">In the [Azure portal](https://portal.azure.com), go to the storage account associated with the web service.</span></span>

   2. <span data-ttu-id="77b35-125">Sous **Service Blob**, cliquez sur **Conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="77b35-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="77b35-126">Si le conteneur **ml-diagnostics** n’existe pas, cliquez sur **+Conteneur**, nommez le conteneur « ml-diagnostics », puis sélectionnez le **Type d’accès** « Blob ».</span><span class="sxs-lookup"><span data-stu-id="77b35-126">If the container **ml-diagnostics** doesn't exist, click **+Container**, give the container the name "ml-diagnostics", and select the **Access type** as "Blob".</span></span> <span data-ttu-id="77b35-127">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="77b35-127">Click **OK**.</span></span>

      ![Sélectionner le niveau de journalisation](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="77b35-129">Pour un service web classique, le tableau de bord Services Web dans Machine Learning Studio comprend également un commutateur pour activer la journalisation.</span><span class="sxs-lookup"><span data-stu-id="77b35-129">For a Classic web service, the Web Services Dashboard in Machine Learning Studio also has a switch to enable logging.</span></span> <span data-ttu-id="77b35-130">Toutefois, la journalisation étant désormais gérée via le portail Services Web, vous devez l’activer via celui-ci, comme décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="77b35-130">However, because logging is now managed through the Web Services portal, you need to enable logging through the portal as described in this article.</span></span> <span data-ttu-id="77b35-131">Si vous déjà activé l’enregistrement dans Studio, puis dans le portail Services Web, désactiver, puis réactivez la journalisation.</span><span class="sxs-lookup"><span data-stu-id="77b35-131">If you already enabled logging in Studio, then in the Web Services Portal, disable logging and enable it again.</span></span>


## <a name="the-effects-of-enabling-logging"></a><span data-ttu-id="77b35-132">Effets de l’activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="77b35-132">The effects of enabling logging</span></span>
<span data-ttu-id="77b35-133">Lorsque la journalisation est activée, les diagnostics et erreurs du point de terminaison du service web sont journalisés dans le conteneur d’objets blob **ml-diagnostics** dans le compte de Stockage Azure lié à l’espace de travail de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="77b35-133">When logging is enabled, the diagnostics and errors from the web service endpoint are logged in the **ml-diagnostics** blob container in the Azure Storage Account linked with the user’s workspace.</span></span> <span data-ttu-id="77b35-134">Ce conteneur contient toutes les informations de diagnostic pour tous les points de terminaison de service web pour tous les espaces de travail associés à ce compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="77b35-134">This container holds all the diagnostics information for all the web service endpoints for all the workspaces associated with this storage account.</span></span>

<span data-ttu-id="77b35-135">Les journaux peuvent être consultés à l’aide de plusieurs outils servant à « explorer » un compte de Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="77b35-135">The logs can be viewed using any of the several tools available to explore an Azure Storage Account.</span></span> <span data-ttu-id="77b35-136">Le plus simple peut être d’accéder au compte de stockage dans le portail Azure, de cliquer sur **Conteneurs**, puis sur le conteneur **ml-diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="77b35-136">The easiest may be to navigate to the storage account in the Azure portal, click **Containers**, and then click the container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="77b35-137">Journaliser les informations détaillées sur l’objet blob</span><span class="sxs-lookup"><span data-stu-id="77b35-137">Log blob detail information</span></span>
<span data-ttu-id="77b35-138">Chaque objet blob dans le conteneur conserve les informations de diagnostic pour une et une seule des actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="77b35-138">Each blob in the container holds the diagnostics information for exactly one of the following actions:</span></span>

* <span data-ttu-id="77b35-139">une exécution de la méthode de traitement par lot</span><span class="sxs-lookup"><span data-stu-id="77b35-139">An execution of the Batch-Execution method</span></span>  
* <span data-ttu-id="77b35-140">une exécution de la méthode de requête-réponse</span><span class="sxs-lookup"><span data-stu-id="77b35-140">An execution of the Request-Response method</span></span>  
* <span data-ttu-id="77b35-141">l’initialisation d'un conteneur de requête-réponse</span><span class="sxs-lookup"><span data-stu-id="77b35-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="77b35-142">Le nom de chaque objet blob a un préfixe sous la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="77b35-142">The name of each blob has a prefix of the following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="77b35-143">Où _Type de journal_ est l’une des valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="77b35-143">Where _Log type_ is one of the following values:</span></span>  

* <span data-ttu-id="77b35-144">lot</span><span class="sxs-lookup"><span data-stu-id="77b35-144">batch</span></span>  
* <span data-ttu-id="77b35-145">score/requests</span><span class="sxs-lookup"><span data-stu-id="77b35-145">score/requests</span></span>  
* <span data-ttu-id="77b35-146">score/init</span><span class="sxs-lookup"><span data-stu-id="77b35-146">score/init</span></span>  

