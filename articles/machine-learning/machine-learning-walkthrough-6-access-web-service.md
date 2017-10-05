---
title: "Étape 6 : Accéder au service web Machine Learning | Microsoft Docs"
description: "Étape 6 du guide pas à pas du développement d’une solution prédictive : accès à un service web actif Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d309f6c4749a80c81859b693a2bd5927e8fe0e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-6-access-the-azure-machine-learning-web-service"></a><span data-ttu-id="9a1bd-103">Étape de didacticiel pas à pas 6 : accéder au service web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9a1bd-103">Walkthrough Step 6: Access the Azure Machine Learning web service</span></span>

<span data-ttu-id="9a1bd-104">Voici la dernière étape de la procédure pas à pas [Développement d'une solution d'analyse prédictive dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="9a1bd-104">This is the last step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="9a1bd-105">Créer un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9a1bd-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="9a1bd-106">Télécharger des données existantes</span><span class="sxs-lookup"><span data-stu-id="9a1bd-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="9a1bd-107">Créer une expérience</span><span class="sxs-lookup"><span data-stu-id="9a1bd-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="9a1bd-108">Former et évaluer les modèles</span><span class="sxs-lookup"><span data-stu-id="9a1bd-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="9a1bd-109">Déployer le service web</span><span class="sxs-lookup"><span data-stu-id="9a1bd-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="9a1bd-110">**Accéder au service web**</span><span class="sxs-lookup"><span data-stu-id="9a1bd-110">**Access the Web service**</span></span>

- - -
<span data-ttu-id="9a1bd-111">Dans l'étape précédente de cette procédure pas à pas, nous avons déployé un service web qui utilise notre modèle prédictif de risque de crédit.</span><span class="sxs-lookup"><span data-stu-id="9a1bd-111">In the previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="9a1bd-112">Désormais, les utilisateurs peuvent lui envoyer des données et recevoir des résultats.</span><span class="sxs-lookup"><span data-stu-id="9a1bd-112">Now users are able to send data to it and receive results.</span></span> 

<span data-ttu-id="9a1bd-113">Il s’agit d’un service web Azure qui peut recevoir et renvoyer des données de deux manières à l’aide d’API REST :</span><span class="sxs-lookup"><span data-stu-id="9a1bd-113">The Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="9a1bd-114">**Demande/Réponse** : l'utilisateur envoie une ou plusieurs lignes de crédit au service en utilisant le protocole HTTP et le service répond avec un ou plusieurs jeux de résultats.</span><span class="sxs-lookup"><span data-stu-id="9a1bd-114">**Request/Response** - The user sends one or more rows of credit data to the service by using an HTTP protocol, and the service responds with one or more sets of results.</span></span>
* <span data-ttu-id="9a1bd-115">**Exécution en lots** : l'utilisateur stocke une ou plusieurs lignes de données de crédit dans le stockage d'objets blob Azure, puis envoie l'emplacement du stockage d'objets blob au service.</span><span class="sxs-lookup"><span data-stu-id="9a1bd-115">**Batch Execution** - The user stores one or more rows of credit data in an Azure blob and then sends the blob location to the service.</span></span> <span data-ttu-id="9a1bd-116">Le service évalue toutes les lignes de données dans l'objet blob d'entrée, enregistre les résultats dans un autre objet blob et renvoie l'URL de ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="9a1bd-116">The service scores all the rows of data in the input blob, stores the results in another blob, and returns the URL of that container.</span></span>  

<span data-ttu-id="9a1bd-117">Le moyen le plus rapide et le plus simple d’accéder à un service web classique est d’utiliser [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) ou [Modèle d’application Web Azure ML Batch Execution Service](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="9a1bd-117">The quickest and easiest way to access a Classic web service is through the [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="9a1bd-118">Ces modèles d'applications web peuvent générer une application Web personnalisée qui connaît les données d'entrée et les résultats attendus de votre service Web.</span><span class="sxs-lookup"><span data-stu-id="9a1bd-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="9a1bd-119">Il vous suffit de donner à l'application Web l'accès à votre service Web et aux données associées, et le modèle fait le reste.</span><span class="sxs-lookup"><span data-stu-id="9a1bd-119">All you need to do is provide access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="9a1bd-120">Pour plus d’informations sur les modèles d’applications web, consultez [Utilisation d’un service Web Microsoft Azure Machine Learning à l’aide d’un modèle d’application Web](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="9a1bd-120">For more information on using the web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="9a1bd-121">Vous pouvez également développer une application personnalisée pour accéder au service web à l'aide du code de démarrage fourni dans R, C# et les langages de programmation Python.</span><span class="sxs-lookup"><span data-stu-id="9a1bd-121">You can also develop a custom application to access the web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="9a1bd-122">Vous trouverez des détails complets dans [Utilisation d’un service web Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="9a1bd-122">You can find complete details in [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

