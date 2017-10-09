---
title: "aaaConsume un Service de Web Machine Learning à partir d’Excel | Documents Microsoft"
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
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="77dd7-103">Utilisation d’un service web Microsoft Azure Machine Learning à partir de Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="77dd7-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="77dd7-104">Azure Machine Learning Studio rend toocall facilement les services web directement à partir d’Excel sans hello besoin toowrite n’importe quel code.</span><span class="sxs-lookup"><span data-stu-id="77dd7-104">Azure Machine Learning Studio makes it easy toocall web services directly from Excel without hello need toowrite any code.</span></span>

<span data-ttu-id="77dd7-105">Si vous utilisez Excel 2013 (ou version ultérieure) ou Excel Online, nous vous recommandons d’utiliser hello Excel [complément Excel](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="77dd7-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use hello Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="77dd7-106">Étapes</span><span class="sxs-lookup"><span data-stu-id="77dd7-106">Steps</span></span>
<span data-ttu-id="77dd7-107">Publiez un service web.</span><span class="sxs-lookup"><span data-stu-id="77dd7-107">Publish a web service.</span></span> <span data-ttu-id="77dd7-108">[Cette page](machine-learning-walkthrough-5-publish-web-service.md) explique comment toodo il.</span><span class="sxs-lookup"><span data-stu-id="77dd7-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how toodo it.</span></span> <span data-ttu-id="77dd7-109">Fonctionnalité de classeur Excel hello est actuellement uniquement pris en charge pour les services de demande/réponse qui ont une seule sortie (autrement dit, une étiquette de score unique).</span><span class="sxs-lookup"><span data-stu-id="77dd7-109">Currently hello Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="77dd7-110">Une fois que vous avez un service web, cliquez sur hello **SERVICES WEB** section sur la gauche hello de studio de hello et sélectionnez hello web service tooconsume à partir d’Excel.</span><span class="sxs-lookup"><span data-stu-id="77dd7-110">Once you have a web service, click on hello **WEB SERVICES** section on hello left of hello studio, and then select hello web service tooconsume from Excel.</span></span>

<span data-ttu-id="77dd7-111">**Service web classique**</span><span class="sxs-lookup"><span data-stu-id="77dd7-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="77dd7-112">Sur hello **tableau de bord** onglet service web de hello est une ligne pour hello **demande/réponse** service.</span><span class="sxs-lookup"><span data-stu-id="77dd7-112">On hello **DASHBOARD** tab for hello web service is a row for hello **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="77dd7-113">Si ce service dispose d’une sortie unique, vous devez voir hello **télécharger un classeur Excel** lien de la ligne.</span><span class="sxs-lookup"><span data-stu-id="77dd7-113">If this service had a single output, you should see hello **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="77dd7-114">Cliquez sur **Télécharger un classeur Excel**.</span><span class="sxs-lookup"><span data-stu-id="77dd7-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="77dd7-115">**Nouveau service web**</span><span class="sxs-lookup"><span data-stu-id="77dd7-115">**New Web Service**</span></span>

1. <span data-ttu-id="77dd7-116">Dans le portail du Service Web de Azure Machine Learning hello, sélectionnez **consommer**.</span><span class="sxs-lookup"><span data-stu-id="77dd7-116">In hello Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="77dd7-117">Hello consommer dans la page hello **options de la consommation de service Web** , cliquez sur icône Excel de hello.</span><span class="sxs-lookup"><span data-stu-id="77dd7-117">On hello Consume page, in hello **Web service consumption options** section, click hello Excel icon.</span></span>

<span data-ttu-id="77dd7-118">**À l’aide du classeur de hello**</span><span class="sxs-lookup"><span data-stu-id="77dd7-118">**Using hello workbook**</span></span>

1. <span data-ttu-id="77dd7-119">Classeur de hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="77dd7-119">Open hello workbook.</span></span>
2. <span data-ttu-id="77dd7-120">Un avertissement de sécurité s’affiche ; Cliquez sur hello **activer la modification** bouton.</span><span class="sxs-lookup"><span data-stu-id="77dd7-120">A Security Warning appears; click on hello **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="77dd7-121">Un avertissement de sécurité apparaît.</span><span class="sxs-lookup"><span data-stu-id="77dd7-121">A Security Warning appears.</span></span> <span data-ttu-id="77dd7-122">Cliquez sur hello **activer le contenu** bouton toorun macros de votre feuille de calcul.</span><span class="sxs-lookup"><span data-stu-id="77dd7-122">Click on hello **Enable Content** button toorun macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="77dd7-123">Une fois les macros activées, une table est générée.</span><span class="sxs-lookup"><span data-stu-id="77dd7-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="77dd7-124">Les colonnes en bleu sont requises en tant qu’entrée dans hello service web d’enregistrements de ressources, ou **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="77dd7-124">Columns in blue are required as input into hello RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="77dd7-125">Notez la sortie hello Hello service RR **valeurs prédites** en vert.</span><span class="sxs-lookup"><span data-stu-id="77dd7-125">Note hello output of hello RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="77dd7-126">Lorsque toutes les colonnes d’une ligne donnée sont remplis, hello classeur automatiquement appelle hello API de calcul de score et affiche hello résultats évalué.</span><span class="sxs-lookup"><span data-stu-id="77dd7-126">When all columns for a given row are filled, hello workbook automatically calls hello scoring API, and displays hello scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="77dd7-127">tooscore plus d’une ligne, remplissage hello deuxième ligne avec des données et hello prévisible de valeurs sont produites.</span><span class="sxs-lookup"><span data-stu-id="77dd7-127">tooscore more than one row, fill hello second row with data and hello predicted values are produced.</span></span> <span data-ttu-id="77dd7-128">Vous pouvez même coller plusieurs lignes à la fois.</span><span class="sxs-lookup"><span data-stu-id="77dd7-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="77dd7-129">Vous pouvez utiliser une des fonctionnalités d’Excel hello (graphiques, mappage de l’alimentation, conditionnelle mise en forme, etc.) avec hello prédit les valeurs toohelp visualiser les données de hello.</span><span class="sxs-lookup"><span data-stu-id="77dd7-129">You can use any of hello Excel features (graphs, power map, conditional formatting, etc.) with hello predicted values toohelp visualize hello data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="77dd7-130">Partage de votre classeur</span><span class="sxs-lookup"><span data-stu-id="77dd7-130">Sharing your workbook</span></span>
<span data-ttu-id="77dd7-131">Pour hello macros toowork, votre clé API doit être la partie de la feuille de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="77dd7-131">For hello macros toowork, your API Key must be part of hello spreadsheet.</span></span> <span data-ttu-id="77dd7-132">Cela signifie que vous devez partager le classeur de hello uniquement avec les entités/personnes de que confiance.</span><span class="sxs-lookup"><span data-stu-id="77dd7-132">That means that you should share hello workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="77dd7-133">Mises à jour automatiques</span><span class="sxs-lookup"><span data-stu-id="77dd7-133">Automatic updates</span></span>
<span data-ttu-id="77dd7-134">Un appel RRS est initié dans les deux cas suivants :</span><span class="sxs-lookup"><span data-stu-id="77dd7-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="77dd7-135">Hello la première fois une ligne a contenu dans toutes ses **paramètres**</span><span class="sxs-lookup"><span data-stu-id="77dd7-135">hello first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="77dd7-136">Chaque fois qu’un des hello **paramètres** modifications d’une ligne qui a toutes ses **paramètres** entré.</span><span class="sxs-lookup"><span data-stu-id="77dd7-136">Any time any of hello **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
