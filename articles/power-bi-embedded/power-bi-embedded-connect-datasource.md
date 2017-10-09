---
title: "aaaMicrosoft Power BI Embedded - source de données tooa connexion"
description: Power BI Embedded, connecter des sources de toodata
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a><span data-ttu-id="14992-103">Connectez la source de données tooa</span><span class="sxs-lookup"><span data-stu-id="14992-103">Connect tooa data source</span></span>
<span data-ttu-id="14992-104">Avec **Power BI Embedded**, vous pouvez incorporer des rapports dans votre propore application.</span><span class="sxs-lookup"><span data-stu-id="14992-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="14992-105">Lorsque vous incorporez un rapport Power BI dans votre application, les rapports hello connecte toohello sous-jacente des données par **importation** une copie de données de hello ou par **connexion directe** à l’aide de source de données toohello  **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="14992-105">When you embed a Power BI report into your app, hello report connects toohello underlying data by **importing** a copy of hello data or by **connecting directly** toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="14992-106">Voici hello les différences entre l’utilisation de **importation** et **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="14992-106">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="14992-107">Importer</span><span class="sxs-lookup"><span data-stu-id="14992-107">Import</span></span> | <span data-ttu-id="14992-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="14992-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="14992-109">Tables, colonnes, *et données* sont importées ou copiées dans le jeu de données du rapport hello.</span><span class="sxs-lookup"><span data-stu-id="14992-109">Tables, columns, *and data* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="14992-110">toosee modifie les données sous-jacentes toohello s’est produite, vous devez actualiser ou importez, à nouveau un dataset complet, en cours.</span><span class="sxs-lookup"><span data-stu-id="14992-110">toosee changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="14992-111">Uniquement *tables et colonnes* sont importées ou copiées dans le jeu de données du rapport hello.</span><span class="sxs-lookup"><span data-stu-id="14992-111">Only *tables and columns* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="14992-112">Vous toujours Affichez les données les plus récentes hello.</span><span class="sxs-lookup"><span data-stu-id="14992-112">You always view hello most current data.</span></span> |

<span data-ttu-id="14992-113">Power BI Embedded vous permet d’utiliser DirectQuery avec des sources de données cloud mais pas des sources de données locales, pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="14992-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="14992-114">Hello passerelle de données locale n'est pas pris en charge avec Power BI incorporé pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="14992-114">hello On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="14992-115">Cela signifie que vous ne pouvez pas utiliser DirectQuery avec des sources de données locales.</span><span class="sxs-lookup"><span data-stu-id="14992-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="14992-116">Sources de données prises en charge</span><span class="sxs-lookup"><span data-stu-id="14992-116">Supported data sources</span></span>

<span data-ttu-id="14992-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="14992-117">**DirectQuery**</span></span>
* <span data-ttu-id="14992-118">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="14992-118">Azure SQL database</span></span>
* <span data-ttu-id="14992-119">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="14992-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="14992-120">**Importationation**</span><span class="sxs-lookup"><span data-stu-id="14992-120">**Import**</span></span>

<span data-ttu-id="14992-121">Vous pouvez importer à l’aide de toutes les sources de données disponibles hello dans Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="14992-121">You can import using all of hello available data sources within Power BI Desktop.</span></span> <span data-ttu-id="14992-122">Vous allez **pas** être en mesure de toorefresh ces données dans Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="14992-122">You will **not** be able toorefresh that data within Power BI Embedded.</span></span> <span data-ttu-id="14992-123">Vous devez les modifications tooupload tooyour PBIX tooPower BI incorporée du fichier.</span><span class="sxs-lookup"><span data-stu-id="14992-123">You will have tooupload changes tooyour PBIX file tooPower BI Embedded.</span></span> <span data-ttu-id="14992-124">Il s’agit en raison de la passerelle disponible de toono.</span><span class="sxs-lookup"><span data-stu-id="14992-124">This is due toono available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="14992-125">Avantages de l'utilisation de DirectQuery</span><span class="sxs-lookup"><span data-stu-id="14992-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="14992-126">Il existe deux grands avantages à utiliser **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="14992-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="14992-127">**DirectQuery** vous permet de créer des visualisations sur des jeux de données très volumineux, où il sinon serait irréalisable toofirst importation tous hello des données.</span><span class="sxs-lookup"><span data-stu-id="14992-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible toofirst import all of hello data.</span></span>
* <span data-ttu-id="14992-128">Modification des données sous-jacentes peuvent exiger une actualisation des données et pour certains rapports, hello doivent toodisplay les données actuelles nécessite des transferts de données volumineux, effectuer une nouvelle importation des données irréalisable.</span><span class="sxs-lookup"><span data-stu-id="14992-128">Underlying data changes can require a refresh of data, and for some reports, hello need toodisplay current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="14992-129">En revanche, les rapports **DirectQuery** utilisent toujours les données actuelles.</span><span class="sxs-lookup"><span data-stu-id="14992-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="14992-130">Limitations de DirectQuery</span><span class="sxs-lookup"><span data-stu-id="14992-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="14992-131">Il existe quelques limitations toousing **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="14992-131">There are a few limitations toousing **DirectQuery**:</span></span>

* <span data-ttu-id="14992-132">Toutes les tables doivent provenir d'une même base de données.</span><span class="sxs-lookup"><span data-stu-id="14992-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="14992-133">Si la requête de hello est trop complexe, une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="14992-133">If hello query is overly complex, an error will occur.</span></span> <span data-ttu-id="14992-134">Erreur de hello tooremedy, vous devez refactoriser les requête hello afin qu’il soit moins complexe.</span><span class="sxs-lookup"><span data-stu-id="14992-134">tooremedy hello error you must refactor hello query so it is less complex.</span></span> <span data-ttu-id="14992-135">Si la requête de hello doit être complexe, vous devez tooimport les données de salutation au lieu d’utiliser **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="14992-135">If hello query must be complex, you will need tooimport hello data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="14992-136">Filtrage de la relation est limité tooa direction à sens unique, plutôt que les deux sens.</span><span class="sxs-lookup"><span data-stu-id="14992-136">Relationship filtering is limited tooa single direction, rather than both directions.</span></span>
* <span data-ttu-id="14992-137">Vous ne pouvez pas modifier le type de données hello d’une colonne.</span><span class="sxs-lookup"><span data-stu-id="14992-137">You cannot change hello data type of a column.</span></span>
* <span data-ttu-id="14992-138">Par défaut, les limitations s’appliquent aux expressions DAX autorisées dans les mesures.</span><span class="sxs-lookup"><span data-stu-id="14992-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="14992-139">Voir [DirectQuery et mesures](#measures).</span><span class="sxs-lookup"><span data-stu-id="14992-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="14992-140">DirectQuery et mesures</span><span class="sxs-lookup"><span data-stu-id="14992-140">DirectQuery and measures</span></span>
<span data-ttu-id="14992-141">requêtes tooensure envoyés toohello source de données sous-jacente des performances acceptables, les limitations sont imposées aux mesures.</span><span class="sxs-lookup"><span data-stu-id="14992-141">tooensure queries sent toohello underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="14992-142">Lorsque vous utilisez **Power BI Desktop**avancées les utilisateurs peuvent choisir toobypass cette limitation en choisissant **fichier > Options et paramètres > Options**.</span><span class="sxs-lookup"><span data-stu-id="14992-142">When using **Power BI Desktop**, advanced users can choose toobypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="14992-143">Bonjour **Options** boîte de dialogue, choisissez **DirectQuery**, puis sélectionnez l’option de hello **autoriser des mesures sans restriction en mode DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="14992-143">In hello **Options** dialog, choose **DirectQuery**, and select hello option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="14992-144">Lorsque cette option est sélectionnée, toute expression DAX valide pour une mesure peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="14992-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="14992-145">Les utilisateurs doivent connaître ; Toutefois, que certaines expressions qui fonctionnent très bien lors de l’importation de données de salutation peut entraîner des requêtes très lentes toohello principal dans la source **DirectQuery** mode.</span><span class="sxs-lookup"><span data-stu-id="14992-145">Users must be aware; however, that some expressions that perform very well when hello data is imported may result in very slow queries toohello backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="14992-146">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="14992-146">See Also</span></span>
* [<span data-ttu-id="14992-147">Prise en main de Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="14992-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="14992-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="14992-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="14992-149">Des questions ?</span><span class="sxs-lookup"><span data-stu-id="14992-149">More questions?</span></span> [<span data-ttu-id="14992-150">Essayez de hello Communauté Power BI</span><span class="sxs-lookup"><span data-stu-id="14992-150">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

