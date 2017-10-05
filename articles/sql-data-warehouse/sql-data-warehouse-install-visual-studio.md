---
title: "Installer Visual Studio et SSDT pour SQL Data Warehouse | Microsoft Docs"
description: "Installer les outils de développement Visual Studio et SSDT pour Azure SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: f7023b78c241a7bc8014276cd0bfa455165b42cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="7fdc4-103">Installer Visual Studio et SSDT pour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7fdc4-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="7fdc4-104">Pour développer des applications pour SQL Data Warehouse, nous recommandons l’utilisation de la version la plus récente de Visual Studio avec la dernière version de SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="7fdc4-104">To develop applications for SQL Data Warehouse, we recommend using the most recent version of Visual Studio with the most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="7fdc4-105">Visual Studio 2013 Update 5 avec SSDT est également pris en charge pour la compatibilité descendante.</span><span class="sxs-lookup"><span data-stu-id="7fdc4-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="7fdc4-106">L’utilisation de Visual Studio avec SSDT vous permettra d’utiliser l’Explorateur d’objets SQL Server pour explorer visuellement les tables, les vues, les procédures stockées et un plus grand nombre d’objets dans SQL Data Warehouse, ainsi que pour exécuter des requêtes.</span><span class="sxs-lookup"><span data-stu-id="7fdc4-106">Using Visual Studio with SSDT will allow you to use the SQL Server Object Explorer to visually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="7fdc4-107">SQL Data Warehouse ne prend pas actuellement en charge les projets de base de données Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7fdc4-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="7fdc4-108">Cette fonctionnalité sera ajoutée dans une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7fdc4-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="7fdc4-109">Étape 1 : Installer Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7fdc4-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="7fdc4-110">Suivez ces liens pour télécharger et installer Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7fdc4-110">Follow these links to download and install Visual Studio.</span></span> <span data-ttu-id="7fdc4-111">Si Visual Studio 2013 ou ultérieur est déjà installé sur votre machine, passez à l’étape 2 pour installer SSDT.</span><span class="sxs-lookup"><span data-stu-id="7fdc4-111">If you already have Visual Studio 2013 or later installed, you can skip to Step 2, install SSDT.</span></span>

1. <span data-ttu-id="7fdc4-112">[Téléchargez Visual Studio][].</span><span class="sxs-lookup"><span data-stu-id="7fdc4-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="7fdc4-113">Suivez le guide [d’installation de Visual Studio][Installing Visual Studio] sur MSDN et sélectionnez les configurations par défaut.</span><span class="sxs-lookup"><span data-stu-id="7fdc4-113">Follow the [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose the default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="7fdc4-114">Étape 2 : Installer SSDT</span><span class="sxs-lookup"><span data-stu-id="7fdc4-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="7fdc4-115">Pour installer SSDT pour Visual Studio, vérifiez simplement la présence d’une mise à jour SSDT dans Visual Studio en procédant comme suit.</span><span class="sxs-lookup"><span data-stu-id="7fdc4-115">To install SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="7fdc4-116">Dans Visual Studio, cliquez sur **Outils** / **Extensions et mises à jour...**</span><span class="sxs-lookup"><span data-stu-id="7fdc4-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="7fdc4-117"> / **Mises à jour**</span><span class="sxs-lookup"><span data-stu-id="7fdc4-117"> / **Updates**</span></span>
2. <span data-ttu-id="7fdc4-118">Sélectionnez **Mises à jour du produit** puis recherchez **Mise à jour Microsoft SQL Server pour les outils de base de données**.</span><span class="sxs-lookup"><span data-stu-id="7fdc4-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="7fdc4-119">Si aucune mise à jour n’est trouvée, vous devez avoir installé la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="7fdc4-119">If an update is not found, then you should have the latest version installed.</span></span>  <span data-ttu-id="7fdc4-120">Pour vérifier que SSDT est installé, cliquez sur **Aide** / **À propos de Microsoft Visual Studio** et recherchez SQL Server Data Tools dans la liste.</span><span class="sxs-lookup"><span data-stu-id="7fdc4-120">To confirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in the list.</span></span>  <span data-ttu-id="7fdc4-121">La dernière version de SSDT est 14.0.60525.0.</span><span class="sxs-lookup"><span data-stu-id="7fdc4-121">The latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="7fdc4-122">Si l’option d’installation n’est pas disponible à partir de Visual Studio, vous pouvez visiter la page [Téléchargement SSDT][SSDT Download] pour télécharger et installer SSDT manuellement.</span><span class="sxs-lookup"><span data-stu-id="7fdc4-122">If the option to install is not available from Visual Studio, alternatively you can visit the [SSDT Download][SSDT Download] page to download and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fdc4-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7fdc4-123">Next steps</span></span>
<span data-ttu-id="7fdc4-124">Maintenant que vous disposez de la dernière version de SSDT, vous êtes prêt à vous [connecter][connect] à SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7fdc4-124">Now that you have the latest version of SSDT, you are ready to [connect][connect] to your SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
<span data-ttu-id="7fdc4-125">[Téléchargez Visual Studio]: https://www.visualstudio.com/downloads/</span><span class="sxs-lookup"><span data-stu-id="7fdc4-125">[Download Visual Studio]: https://www.visualstudio.com/downloads/</span></span>
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
