---
title: "Développer des assemblys U-SQL pour des travaux Azure Data Lake Analytics | Microsoft Docs"
description: "Apprenez à développer des assemblys pour les utiliser et les réutiliser dans des travaux Data Lake Analytics. "
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/30/2016
ms.author: jejiang
ms.openlocfilehash: c49f80f8dcd330d7f46726241e7178351b9cc28f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="ba6d7-103">Développer des assemblys U-SQL pour des travaux Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ba6d7-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="ba6d7-104">Apprenez à convertir des fichiers code-behind and assemblys pour les utiliser et les réutiliser dans des travaux Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-104">Learn how to turn code-behind into assemblies to be used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="ba6d7-105">U-SQL permet d’ajouter facilement votre propre code personnalisé dans les langages .Net, tels que C#, VB.Net ou F#.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-105">U-SQL makes it easy to add your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="ba6d7-106">Vous pouvez même déployer votre propre runtime pour prendre en charge d’autres langages.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-106">You can even deploy your own runtime to support other languages.</span></span>

<span data-ttu-id="ba6d7-107">Le moyen le plus simple d’utiliser un code personnalisé consiste à se servir des outils Data Lake pour les capacités de code-behind de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-107">The easiest way to use custom code is to use the Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="ba6d7-108">Pour plus d’informations, consultez le [didacticiel : Développer des scripts U-SQL avec les outils Data Lake pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ba6d7-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="ba6d7-109">Il existe quelques inconvénients à l’utilisation de code-behind :</span><span class="sxs-lookup"><span data-stu-id="ba6d7-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="ba6d7-110">Le code source est chargé à chaque envoi de script.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-110">The source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="ba6d7-111">Le fichier code-behind ne peut pas être partagé avec d’autres tâches.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="ba6d7-112">Pour remédier à ces inconvénients, vous pouvez convertir le code-behind en assemblys et inscrire les assemblys dans le catalogue Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-112">To address these drawbacks, you can turn code-behind into assemblies, and register the assemblies to the Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba6d7-113">Prérequis</span><span class="sxs-lookup"><span data-stu-id="ba6d7-113">Prerequisites</span></span>
* <span data-ttu-id="ba6d7-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 Update 4 ou Visual Studio 2012 avec Visual C++ installé</span><span class="sxs-lookup"><span data-stu-id="ba6d7-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="ba6d7-115">Le kit SDK Microsoft Azure pour .NET version 2.5 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="ba6d7-116">Installez-le à l’aide de Web Platform Installer ou du programme d’installation de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ba6d7-116">Install it using the Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="ba6d7-117">Un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="ba6d7-118">Consultez l’article [Prise en main d’Azure Data Lake Analytics à l’aide du Portail Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ba6d7-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="ba6d7-119">Parcourez le didacticiel [Prise en main d’Azure Data Lake Analytics avec U-SQL Studio](data-lake-analytics-u-sql-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="ba6d7-119">Go through the [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="ba6d7-120">Connexion à Azure.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-120">Connect to Azure.</span></span>
* <span data-ttu-id="ba6d7-121">Téléchargez la source de données, consultez [Prise en main d’Azure Data Lake Analytics avec U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ba6d7-121">Upload the source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="ba6d7-122">Développement d’assemblys pour U-SQL</span><span class="sxs-lookup"><span data-stu-id="ba6d7-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="ba6d7-123">**Pour créer et soumettre un travail U-SQL**</span><span class="sxs-lookup"><span data-stu-id="ba6d7-123">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="ba6d7-124">Dans le menu **Fichier**, cliquez sur **Nouveau**, puis sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-124">From the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="ba6d7-125">Développez **Installé**, **Modèles**, **Azure Data Lake**, **U-SQL (ADLA)**, sélectionnez le modèle **Bibliothèque de classes (pour application U-SQL)**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select the **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="ba6d7-126">Écrivez votre code dans le fichier Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="ba6d7-127">Voici un exemple de code.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-127">The following is a code sample.</span></span>

        using Microsoft.Analytics.Interfaces;

        namespace USQLApplication_codebehind
        {
            [SqlUserDefinedProcessor]
            public class MyProcessor : IProcessor
            {
                public override IRow Process(IRow input, IUpdatableRow output)
                {
                    output.Set(0, input.Get<string>(0));
                    output.Set(0, input.Get<string>(0));
                    return output.AsReadOnly();
                }
            }
        }
4. <span data-ttu-id="ba6d7-128">Cliquez sur le menu **Générer**, puis sur **Générer la solution** pour créer la dll.</span><span class="sxs-lookup"><span data-stu-id="ba6d7-128">Click the **Build** menu, and then click **Build Solution** to create the dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="ba6d7-129">Inscription d’assemblys</span><span class="sxs-lookup"><span data-stu-id="ba6d7-129">Register assemblies</span></span>

<span data-ttu-id="ba6d7-130">Consultez [Utilisation du catalogue Data Lake Analytics (U-SQL)](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="ba6d7-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-the-assemblies"></a><span data-ttu-id="ba6d7-131">Utilisation des assemblys</span><span class="sxs-lookup"><span data-stu-id="ba6d7-131">Use the assemblies</span></span>

<span data-ttu-id="ba6d7-132">Consultez la page [Utilisation d’Azure Data Lake Tools pour Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="ba6d7-132">See [Use the Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ba6d7-133">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ba6d7-133">See also</span></span>
* [<span data-ttu-id="ba6d7-134">Prise en main de Data Lake Analytics à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba6d7-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="ba6d7-135">Prise en main de Data Lake Analytics à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="ba6d7-135">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="ba6d7-136">Utiliser les outils Data Lake pour Visual Studio pour le développement d’applications U-SQL</span><span class="sxs-lookup"><span data-stu-id="ba6d7-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="ba6d7-137">Utilisation du catalogue Data Lake Analytics (U-SQL)</span><span class="sxs-lookup"><span data-stu-id="ba6d7-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="ba6d7-138">Utilisation d’Azure Data Lake Tools pour Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ba6d7-138">Use the Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)