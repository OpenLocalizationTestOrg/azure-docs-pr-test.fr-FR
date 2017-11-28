---
title: "Utilisation d’un service web Machine Learning à partir de Microsoft Excel | Microsoft Docs"
description: "Utilisation d’un service web Microsoft Azure Machine Learning à partir de Microsoft Excel."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: 9f1aac04d54221888ee9374317be339400dcf085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="c3980-103">Utilisation d’un service web Microsoft Azure Machine Learning à partir de Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="c3980-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="c3980-104">Microsoft Azure Machine Learning Studio permet d’appeler facilement des services web directement à partir de Microsoft Excel sans qu’il soit nécessaire d’écrire du code.</span><span class="sxs-lookup"><span data-stu-id="c3980-104">Azure Machine Learning Studio makes it easy to call web services directly from Excel without the need to write any code.</span></span>

<span data-ttu-id="c3980-105">Si vous utilisez Excel 2013 (ou une version ultérieure) ou Excel Online, nous vous recommandons d’utiliser la [macro complémentaire Excel](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="c3980-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use the Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="c3980-106">Étapes</span><span class="sxs-lookup"><span data-stu-id="c3980-106">Steps</span></span>
<span data-ttu-id="c3980-107">Publiez un service web.</span><span class="sxs-lookup"><span data-stu-id="c3980-107">Publish a web service.</span></span> <span data-ttu-id="c3980-108">[Cette page](machine-learning-walkthrough-5-publish-web-service.md) explique comment procéder.</span><span class="sxs-lookup"><span data-stu-id="c3980-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how to do it.</span></span> <span data-ttu-id="c3980-109">Actuellement, la fonctionnalité de classeur Excel est uniquement prise en charge pour les services de requête/réponse qui produisent une seule sortie (autrement dit, une étiquette de notation unique).</span><span class="sxs-lookup"><span data-stu-id="c3980-109">Currently the Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="c3980-110">Quand vous disposez d’un service web, cliquez sur la section **WEB SERVICES** située sur la partie gauche de Microsoft Azure Machine Learning Studio, puis sélectionnez le service web à utiliser à partir de Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="c3980-110">Once you have a web service, click on the **WEB SERVICES** section on the left of the studio, and then select the web service to consume from Excel.</span></span>

<span data-ttu-id="c3980-111">**Service web classique**</span><span class="sxs-lookup"><span data-stu-id="c3980-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="c3980-112">Sur l’onglet **TABLEAU DE BORD** du service web figure une ligne pour le service **REQUÊTE/RÉPONSE**.</span><span class="sxs-lookup"><span data-stu-id="c3980-112">On the **DASHBOARD** tab for the web service is a row for the **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="c3980-113">Si ce service produit une sortie unique, le lien **Télécharger un classeur Excel** doit apparaître sur cette ligne.</span><span class="sxs-lookup"><span data-stu-id="c3980-113">If this service had a single output, you should see the **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="c3980-114">Cliquez sur **Télécharger un classeur Excel**.</span><span class="sxs-lookup"><span data-stu-id="c3980-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="c3980-115">**Nouveau service web**</span><span class="sxs-lookup"><span data-stu-id="c3980-115">**New Web Service**</span></span>

1. <span data-ttu-id="c3980-116">Dans le portail Service web Azure Machine Learning, sélectionnez **Consommer**.</span><span class="sxs-lookup"><span data-stu-id="c3980-116">In the Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="c3980-117">Dans la page Consommer, dans les **options de consommation de service Web** cliquez sur l’icône Excel.</span><span class="sxs-lookup"><span data-stu-id="c3980-117">On the Consume page, in the **Web service consumption options** section, click the Excel icon.</span></span>

<span data-ttu-id="c3980-118">**Utilisation du classeur**</span><span class="sxs-lookup"><span data-stu-id="c3980-118">**Using the workbook**</span></span>

1. <span data-ttu-id="c3980-119">Ouvrez le classeur.</span><span class="sxs-lookup"><span data-stu-id="c3980-119">Open the workbook.</span></span>
2. <span data-ttu-id="c3980-120">Un avertissement de sécurité s’affiche. Cliquez sur le bouton **Activer la modification**.</span><span class="sxs-lookup"><span data-stu-id="c3980-120">A Security Warning appears; click on the **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="c3980-121">Un avertissement de sécurité apparaît.</span><span class="sxs-lookup"><span data-stu-id="c3980-121">A Security Warning appears.</span></span> <span data-ttu-id="c3980-122">Cliquez sur le bouton **Activer le contenu** pour pouvoir exécuter des macros sur votre feuille de calcul.</span><span class="sxs-lookup"><span data-stu-id="c3980-122">Click on the **Enable Content** button to run macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="c3980-123">Une fois les macros activées, une table est générée.</span><span class="sxs-lookup"><span data-stu-id="c3980-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="c3980-124">Les valeurs des colonnes en bleu sont requises en tant qu’entrées dans le service web RRS (Request/Response Service), ou en tant que **PARAMÈTRES**.</span><span class="sxs-lookup"><span data-stu-id="c3980-124">Columns in blue are required as input into the RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="c3980-125">Notez la sortie du service RRS, appelée **VALEURS PRÉDITES** et affichée en vert.</span><span class="sxs-lookup"><span data-stu-id="c3980-125">Note the output of the RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="c3980-126">Lorsque toutes les colonnes d’une ligne donnée sont remplies, le classeur appelle automatiquement l’API de notation et affiche les notes résultantes.</span><span class="sxs-lookup"><span data-stu-id="c3980-126">When all columns for a given row are filled, the workbook automatically calls the scoring API, and displays the scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="c3980-127">Pour noter plusieurs lignes, remplissez la deuxième ligne avec les données ; des valeurs prédites sont produites.</span><span class="sxs-lookup"><span data-stu-id="c3980-127">To score more than one row, fill the second row with data and the predicted values are produced.</span></span> <span data-ttu-id="c3980-128">Vous pouvez même coller plusieurs lignes à la fois.</span><span class="sxs-lookup"><span data-stu-id="c3980-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="c3980-129">Vous pouvez utiliser toutes les fonctionnalités de Microsoft Excel (graphiques, Power Map, mise en forme conditionnelle, etc.) avec les valeurs prédites pour visualiser les données.</span><span class="sxs-lookup"><span data-stu-id="c3980-129">You can use any of the Excel features (graphs, power map, conditional formatting, etc.) with the predicted values to help visualize the data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="c3980-130">Partage de votre classeur</span><span class="sxs-lookup"><span data-stu-id="c3980-130">Sharing your workbook</span></span>
<span data-ttu-id="c3980-131">Pour que les macros fonctionnent, votre Clé API doit faire partie de la feuille de calcul.</span><span class="sxs-lookup"><span data-stu-id="c3980-131">For the macros to work, your API Key must be part of the spreadsheet.</span></span> <span data-ttu-id="c3980-132">Cela signifie que vous devez uniquement partager le classeur avec des entités/personnes de confiance.</span><span class="sxs-lookup"><span data-stu-id="c3980-132">That means that you should share the workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="c3980-133">Mises à jour automatiques</span><span class="sxs-lookup"><span data-stu-id="c3980-133">Automatic updates</span></span>
<span data-ttu-id="c3980-134">Un appel RRS est initié dans les deux cas suivants :</span><span class="sxs-lookup"><span data-stu-id="c3980-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="c3980-135">la première fois que du contenu apparaît dans l’ensemble des **PARAMÈTRES**</span><span class="sxs-lookup"><span data-stu-id="c3980-135">The first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="c3980-136">chaque fois que l’un ou l’autre des **PARAMÈTRES** change dans une ligne dont l’ensemble des **PARAMÈTRES** a été entré.</span><span class="sxs-lookup"><span data-stu-id="c3980-136">Any time any of the **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
