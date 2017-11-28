---
title: "Étape 6 : Accéder au service de Machine Learning Web hello | Documents Microsoft"
description: "Étape 6 de hello développer la procédure pas à pas une solution prédictive : accéder à un service Web de Azure Machine Learning actif."
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
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a><span data-ttu-id="02347-103">Étape 6 de la procédure pas à pas : Service web de Azure Machine Learning hello accéder à</span><span class="sxs-lookup"><span data-stu-id="02347-103">Walkthrough Step 6: Access hello Azure Machine Learning web service</span></span>

<span data-ttu-id="02347-104">C’est hello dernière étape de la procédure pas à pas de hello, [développer une solution prédictive analytique dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="02347-104">This is hello last step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="02347-105">Créer un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="02347-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="02347-106">Télécharger des données existantes</span><span class="sxs-lookup"><span data-stu-id="02347-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="02347-107">Créer une expérience</span><span class="sxs-lookup"><span data-stu-id="02347-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="02347-108">L’apprentissage et évaluer des modèles de hello</span><span class="sxs-lookup"><span data-stu-id="02347-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="02347-109">Déployer le service Web de hello</span><span class="sxs-lookup"><span data-stu-id="02347-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="02347-110">**Accéder au service Web de hello**</span><span class="sxs-lookup"><span data-stu-id="02347-110">**Access hello Web service**</span></span>

- - -
<span data-ttu-id="02347-111">À l’étape précédente de hello dans cette procédure pas à pas, nous avons déployé un service web qui utilise de notre modèle de prévision de risque de crédit.</span><span class="sxs-lookup"><span data-stu-id="02347-111">In hello previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="02347-112">Désormais, les utilisateurs sont en mesure de toosend données tooit et recevoir les résultats.</span><span class="sxs-lookup"><span data-stu-id="02347-112">Now users are able toosend data tooit and receive results.</span></span> 

<span data-ttu-id="02347-113">Hello service Web est un service web Azure qui peut recevoir et retourner des données à l’aide des API REST de deux manières :</span><span class="sxs-lookup"><span data-stu-id="02347-113">hello Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="02347-114">**Demande/réponse** - utilisateur de hello envoie un ou plusieurs lignes de toohello de données de crédit de service à l’aide d’un protocole HTTP et hello répond de service avec un ou plusieurs jeux de résultats.</span><span class="sxs-lookup"><span data-stu-id="02347-114">**Request/Response** - hello user sends one or more rows of credit data toohello service by using an HTTP protocol, and hello service responds with one or more sets of results.</span></span>
* <span data-ttu-id="02347-115">**L’exécution du lot** - utilisateur de hello stocke une ou plusieurs lignes de données de crédit dans Azure d’objets blob et envoie ensuite le service de toohello emplacement hello blob.</span><span class="sxs-lookup"><span data-stu-id="02347-115">**Batch Execution** - hello user stores one or more rows of credit data in an Azure blob and then sends hello blob location toohello service.</span></span> <span data-ttu-id="02347-116">les scores de service Hello dans que tous hello des lignes de données Bonjour blob d’entrée, magasins hello aboutit à un autre objet blob et retourne hello URL de ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="02347-116">hello service scores all hello rows of data in hello input blob, stores hello results in another blob, and returns hello URL of that container.</span></span>  

<span data-ttu-id="02347-117">Hello tooaccess moyen le plus rapide et plus simple est d’un service web de classique via hello [l’application Web Azure ML avec requête-réponse Service](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) ou [modèle d’application Azure ML lot l’exécution du Service Web](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="02347-117">hello quickest and easiest way tooaccess a Classic web service is through hello [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="02347-118">Ces modèles d'applications web peuvent générer une application Web personnalisée qui connaît les données d'entrée et les résultats attendus de votre service Web.</span><span class="sxs-lookup"><span data-stu-id="02347-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="02347-119">Vous toodo suffit de fournir des données et accès tooyour web service et le modèle de hello hello rest.</span><span class="sxs-lookup"><span data-stu-id="02347-119">All you need toodo is provide access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="02347-120">Pour plus d’informations sur l’utilisation de modèles d’application web hello, consultez [consommer un service Web de Azure Machine Learning avec un modèle d’application web](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="02347-120">For more information on using hello web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="02347-121">Vous pouvez également développer tooaccess hello web service d’application personnalisé à l’aide de code de démarrage fourni pour vous dans R, c# et langages de programmation Python.</span><span class="sxs-lookup"><span data-stu-id="02347-121">You can also develop a custom application tooaccess hello web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="02347-122">Vous trouverez plus de détails dans [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="02347-122">You can find complete details in [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

