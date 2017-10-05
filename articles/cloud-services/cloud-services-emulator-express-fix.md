---
title: "Configurer l’émulateur express pour déboguer des applications de service cloud dans Visual Studio | Microsoft Docs"
description: "Explique comment installer le redistribuable C++ pour activer l’émulateur express dans Visual Studio"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 22b20f7a-23f4-4f7f-b536-3bf1e01adcd1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 05d672dcb1335c617bb8d8cae43947bcd5e9ab3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-emulator-express-to-debug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="bc00b-103">Utiliser l’émulateur express pour déboguer des applications de service cloud dans VS 2017</span><span class="sxs-lookup"><span data-stu-id="bc00b-103">Use Emulator Express to debug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="bc00b-104">Cet article explique comment utiliser l’émulateur express pour déboguer des applications de service cloud dans VS 2017.</span><span class="sxs-lookup"><span data-stu-id="bc00b-104">This article explains how to use Emulator Express to debug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="bc00b-105">Contexte</span><span class="sxs-lookup"><span data-stu-id="bc00b-105">Background context</span></span>
<span data-ttu-id="bc00b-106">L’émulateur express est utilisé par défaut pour le débogage des rôles web et de travail des services cloud dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc00b-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="bc00b-107">Ce paramètre est spécifié dans la page de propriétés du projet de service cloud.</span><span class="sxs-lookup"><span data-stu-id="bc00b-107">This setting is specified in the Cloud Services project properties page.</span></span>

![Ouvrir les propriétés du projet][0]

![L’émulateur express est sélectionné par défaut][1]

<span data-ttu-id="bc00b-110">Le [Visual C++ Redistributable] [ Visual C++ Redistributable] pour Visual Studio est requis par l’émulateur express.</span><span class="sxs-lookup"><span data-stu-id="bc00b-110">The [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="bc00b-111">Il n’est actuellement pas installé avec la charge de travail Azure.</span><span class="sxs-lookup"><span data-stu-id="bc00b-111">Currently it is not installed with the Azure workload.</span></span> <span data-ttu-id="bc00b-112">En cas d’appui sur F5 pour déboguer une application de service cloud, Visual Studio invite à installer ce composant et à continuer le débogage.</span><span class="sxs-lookup"><span data-stu-id="bc00b-112">Upon F5 gesture to debug a Cloud Services applications, Visual Studio would prompt to install this component and proceed with debugging.</span></span>

![Invite d’installation du redistribuable C++][2]

<span data-ttu-id="bc00b-114">Cliquez sur Oui pour installer le redistribuable C++.</span><span class="sxs-lookup"><span data-stu-id="bc00b-114">Click Yes to install C++ Redistributable.</span></span>

![Installer le redistribuable C++][3]

<span data-ttu-id="bc00b-116">Appuyez de nouveau sur F5 pour lancer des sessions de débogage.</span><span class="sxs-lookup"><span data-stu-id="bc00b-116">Press F5 again to launch debugging sessions.</span></span>

![Démarrer le débogage][4]

![Débogage réussi][5]

> <span data-ttu-id="bc00b-119">Remarque : l’installation du redistribuable Visual C++ n’est nécessaire qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="bc00b-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="bc00b-120">Si vous avez effectué une mise à niveau à partir d’une version antérieure du Kit de développement logiciel Azure et avez déjà installé l’émulateur express, vous ne rencontrerez pas ce problème.</span><span class="sxs-lookup"><span data-stu-id="bc00b-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="bc00b-121">Solution de contournement manuel</span><span class="sxs-lookup"><span data-stu-id="bc00b-121">Manual workaround</span></span>
<span data-ttu-id="bc00b-122">Vous pouvez également installer le [Visual C++ Redistributable] [ Visual C++ Redistributable] manuellement et est appliquée même effet que la façon dont Visual Studio installée sur votre système.</span><span class="sxs-lookup"><span data-stu-id="bc00b-122">You can also install the [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="bc00b-123">[VCRedist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="bc00b-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="bc00b-124">[VCRedist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="bc00b-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc00b-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bc00b-125">Next Steps</span></span>
<span data-ttu-id="bc00b-126">En savoir plus sur l’utilisation d’émulateur de calcul Azure pour déboguer vos applications de Services de cloud computing dans Visual Studio : [à l’aide d’émulateur Express pour exécuter et déboguer un service cloud sur un ordinateur local][Using Emulator Express to run and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="bc00b-126">Learn more about using Azure Computer Emulator to debug your Cloud Services applications in Visual Studio: [Using Emulator Express to run and debug a cloud service on a local machine][Using Emulator Express to run and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express to run and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
