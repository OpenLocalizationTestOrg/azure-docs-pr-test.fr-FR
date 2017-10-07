---
title: aaaInstall Visual Studio et SSDT pour SQL Data Warehouse | Documents Microsoft
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
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="57d4b-103">Installer Visual Studio et SSDT pour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="57d4b-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="57d4b-104">applications toodevelop pour SQL Data Warehouse, nous recommandons à l’aide de la version la plus récente de Visual Studio hello avec la version la plus récente de SQL Server Data Tools (SSDT) hello.</span><span class="sxs-lookup"><span data-stu-id="57d4b-104">toodevelop applications for SQL Data Warehouse, we recommend using hello most recent version of Visual Studio with hello most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="57d4b-105">Visual Studio 2013 Update 5 avec SSDT est également pris en charge pour la compatibilité descendante.</span><span class="sxs-lookup"><span data-stu-id="57d4b-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="57d4b-106">À l’aide de Visual Studio avec SSDT vous permettra de toouse hello Explorateur d’objets SQL Server toovisually Explorer les tables, vues, procédures stockées et beaucoup plus d’objets dans votre entrepôt de données SQL, ainsi que d’exécuter des requêtes.</span><span class="sxs-lookup"><span data-stu-id="57d4b-106">Using Visual Studio with SSDT will allow you toouse hello SQL Server Object Explorer toovisually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="57d4b-107">SQL Data Warehouse ne prend pas actuellement en charge les projets de base de données Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="57d4b-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="57d4b-108">Cette fonctionnalité sera ajoutée dans une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="57d4b-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="57d4b-109">Étape 1 : Installer Visual Studio</span><span class="sxs-lookup"><span data-stu-id="57d4b-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="57d4b-110">Suivez ces toodownload de liens et d’installer Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="57d4b-110">Follow these links toodownload and install Visual Studio.</span></span> <span data-ttu-id="57d4b-111">Si vous disposez déjà de Visual Studio 2013 ou version ultérieure est installé, vous pouvez ignorer tooStep 2, installez SSDT.</span><span class="sxs-lookup"><span data-stu-id="57d4b-111">If you already have Visual Studio 2013 or later installed, you can skip tooStep 2, install SSDT.</span></span>

1. <span data-ttu-id="57d4b-112">[Téléchargez Visual Studio][].</span><span class="sxs-lookup"><span data-stu-id="57d4b-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="57d4b-113">Suivez hello [installation de Visual Studio] [ Installing Visual Studio] guide sur MSDN et choisir la configuration par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="57d4b-113">Follow hello [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose hello default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="57d4b-114">Étape 2 : Installer SSDT</span><span class="sxs-lookup"><span data-stu-id="57d4b-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="57d4b-115">tooinstall SSDT pour Visual Studio Cochez simplement une mise à jour SSDT à partir de Visual Studio en suivant ces étapes.</span><span class="sxs-lookup"><span data-stu-id="57d4b-115">tooinstall SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="57d4b-116">Dans Visual Studio, cliquez sur **Outils** / **Extensions et mises à jour...**</span><span class="sxs-lookup"><span data-stu-id="57d4b-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="57d4b-117"> / **Mises à jour**</span><span class="sxs-lookup"><span data-stu-id="57d4b-117"> / **Updates**</span></span>
2. <span data-ttu-id="57d4b-118">Sélectionnez **Mises à jour du produit** puis recherchez **Mise à jour Microsoft SQL Server pour les outils de base de données**.</span><span class="sxs-lookup"><span data-stu-id="57d4b-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="57d4b-119">Si une mise à jour n’est trouvé, vous devez hello dernière version installée.</span><span class="sxs-lookup"><span data-stu-id="57d4b-119">If an update is not found, then you should have hello latest version installed.</span></span>  <span data-ttu-id="57d4b-120">tooconfirm SSDT est installé, cliquez sur **aide** / **sur Microsoft Visual Studio** et recherchez SQL Server Data Tools dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="57d4b-120">tooconfirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in hello list.</span></span>  <span data-ttu-id="57d4b-121">version la plus récente de SSDT Hello est 14.0.60525.0.</span><span class="sxs-lookup"><span data-stu-id="57d4b-121">hello latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="57d4b-122">Si hello option tooinstall n’est pas disponible à partir de Visual Studio, vous pouvez aussi visiter hello [de téléchargement SSDT] [ SSDT Download] page toodownload et installer SSDT manuellement.</span><span class="sxs-lookup"><span data-stu-id="57d4b-122">If hello option tooinstall is not available from Visual Studio, alternatively you can visit hello [SSDT Download][SSDT Download] page toodownload and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57d4b-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57d4b-123">Next steps</span></span>
<span data-ttu-id="57d4b-124">Maintenant que vous avez la version la plus récente de SSDT hello, vous êtes prêt trop[connecter] [ connect] tooyour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="57d4b-124">Now that you have hello latest version of SSDT, you are ready too[connect][connect] tooyour SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Téléchargez Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
