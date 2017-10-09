---
title: "assemblys aaaDevelop U-SQL pour les travaux de l’Analytique de LAC de données Azure | Documents Microsoft"
description: "Découvrez comment toodevelop assemblys toobe utilisé et réutilisées dans les données de LAC Analytique travaux. "
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
ms.openlocfilehash: 86dd17b25e0967306ed36bb5b7f3178d9409d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-assemblies-for-azure-data-lake-analytics-jobs"></a><span data-ttu-id="5eaaa-103">Développer des assemblys U-SQL pour des travaux Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="5eaaa-103">Develop U-SQL assemblies for Azure Data Lake Analytics jobs</span></span>
<span data-ttu-id="5eaaa-104">Découvrez comment tooturn code-behind dans les assemblys toobe utilisé et réutilisées dans les travaux Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-104">Learn how tooturn code-behind into assemblies toobe used and reused in Data Lake Analytics jobs.</span></span> 

<span data-ttu-id="5eaaa-105">U-SQL rend facile tooadd votre propre code dans les langages .net, tels que c#, VB.Net ou F #.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-105">U-SQL makes it easy tooadd your own custom code in .Net languages, such as C#, VB.Net or F#.</span></span> <span data-ttu-id="5eaaa-106">Vous pouvez même déployer votre propre toosupport runtime autres langages.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-106">You can even deploy your own runtime toosupport other languages.</span></span>

<span data-ttu-id="5eaaa-107">code personnalisé Hello plus simple façon toouse est toouse hello Data Lake Tools pour les fonctions de code-behind de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-107">hello easiest way toouse custom code is toouse hello Data Lake Tools for Visual Studio’s code-behind capabilities.</span></span> <span data-ttu-id="5eaaa-108">Pour plus d’informations, consultez le [didacticiel : Développer des scripts U-SQL avec les outils Data Lake pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5eaaa-108">For more information, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="5eaaa-109">Il existe quelques inconvénients à l’utilisation de code-behind :</span><span class="sxs-lookup"><span data-stu-id="5eaaa-109">There are a few drawbacks of using code-behind:</span></span>

- <span data-ttu-id="5eaaa-110">code source de Hello obtient téléchargé pour chaque demande de script.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-110">hello source code gets uploaded for every script submission.</span></span>
- <span data-ttu-id="5eaaa-111">Le fichier code-behind ne peut pas être partagé avec d’autres tâches.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-111">code-behind cannot be shared with other jobs.</span></span>

<span data-ttu-id="5eaaa-112">tooaddress ces inconvénients, vous pouvez activer le code-behind dans des assemblys et inscrire le catalogue de hello assemblys toohello Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-112">tooaddress these drawbacks, you can turn code-behind into assemblies, and register hello assemblies toohello Data Lake Analytics catalog.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5eaaa-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5eaaa-113">Prerequisites</span></span>
* <span data-ttu-id="5eaaa-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 Update 4 ou Visual Studio 2012 avec Visual C++ installé</span><span class="sxs-lookup"><span data-stu-id="5eaaa-114">Visual Studio 2017, Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012 with Visual C++ Installed</span></span>
* <span data-ttu-id="5eaaa-115">Le kit SDK Microsoft Azure pour .NET version 2.5 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-115">Microsoft Azure SDK for .NET version 2.5 or above.</span></span>  <span data-ttu-id="5eaaa-116">Installer à l’aide du programme d’installation de plateforme hello Web ou le programme d’installation de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5eaaa-116">Install it using hello Web platform installer or Visual Studio Installer</span></span>
* <span data-ttu-id="5eaaa-117">Un compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-117">A Data Lake Analytics account.</span></span>  <span data-ttu-id="5eaaa-118">Consultez l’article [Prise en main d’Azure Data Lake Analytics à l’aide du Portail Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5eaaa-118">See [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="5eaaa-119">Passez en revue hello [prise en main Azure Data Lake Analytique U-SQL Studio](data-lake-analytics-u-sql-get-started.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-119">Go through hello [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md) tutorial.</span></span>
* <span data-ttu-id="5eaaa-120">Se connecter tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-120">Connect tooAzure.</span></span>
* <span data-ttu-id="5eaaa-121">Télécharger des données de sources de hello, consultez [prise en main Azure Data Lake Analytique U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5eaaa-121">Upload hello source data, see [Get started with Azure Data Lake Analytics U-SQL Studio](data-lake-analytics-u-sql-get-started.md).</span></span> 

## <a name="develop-assemblies-for-u-sql"></a><span data-ttu-id="5eaaa-122">Développement d’assemblys pour U-SQL</span><span class="sxs-lookup"><span data-stu-id="5eaaa-122">Develop assemblies for U-SQL</span></span>

<span data-ttu-id="5eaaa-123">**toocreate et soumettre un travail U-SQL**</span><span class="sxs-lookup"><span data-stu-id="5eaaa-123">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="5eaaa-124">À partir de hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-124">From hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="5eaaa-125">Développez **installé**, **modèles**, **Azure Data Lake**, **U-SQL(ADLA)**, sélectionnez hello **bibliothèque de classes (pour U-SQL Application)** modèle, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-125">Expand **Installed**, **Templates**, **Azure Data Lake**, **U-SQL(ADLA)**, select hello **Class Library (For U-SQL Application)** template, and then click **OK**.</span></span>
3. <span data-ttu-id="5eaaa-126">Écrivez votre code dans le fichier Class1.cs.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-126">Write your code in Class1.cs.</span></span>  <span data-ttu-id="5eaaa-127">Hello Voici un exemple de code.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-127">hello following is a code sample.</span></span>

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
4. <span data-ttu-id="5eaaa-128">Cliquez sur hello **générer** menu, puis sur **générer la Solution** toocreate hello dll.</span><span class="sxs-lookup"><span data-stu-id="5eaaa-128">Click hello **Build** menu, and then click **Build Solution** toocreate hello dll.</span></span>

## <a name="register-assemblies"></a><span data-ttu-id="5eaaa-129">Inscription d’assemblys</span><span class="sxs-lookup"><span data-stu-id="5eaaa-129">Register assemblies</span></span>

<span data-ttu-id="5eaaa-130">Consultez [Utilisation du catalogue Data Lake Analytics (U-SQL)](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="5eaaa-130">See [Use Data Lake Analytics(U-SQL) catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>


## <a name="use-hello-assemblies"></a><span data-ttu-id="5eaaa-131">Utiliser des assemblys hello</span><span class="sxs-lookup"><span data-stu-id="5eaaa-131">Use hello assemblies</span></span>

<span data-ttu-id="5eaaa-132">Consultez [utiliser hello Azure Data Lake Tools pour Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="5eaaa-132">See [Use hello Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="5eaaa-133">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5eaaa-133">See also</span></span>
* [<span data-ttu-id="5eaaa-134">Prise en main de Data Lake Analytics à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="5eaaa-134">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="5eaaa-135">Prise en main Analytique lac de données à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5eaaa-135">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="5eaaa-136">Utiliser les outils Data Lake pour Visual Studio pour le développement d’applications U-SQL</span><span class="sxs-lookup"><span data-stu-id="5eaaa-136">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="5eaaa-137">Utilisation du catalogue Data Lake Analytics (U-SQL)</span><span class="sxs-lookup"><span data-stu-id="5eaaa-137">Use Data Lake Analytics(U-SQL) catalog</span></span>](data-lake-analytics-use-u-sql-catalog.md)
* [<span data-ttu-id="5eaaa-138">Utilisez hello Azure Data Lake Tools pour Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5eaaa-138">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
