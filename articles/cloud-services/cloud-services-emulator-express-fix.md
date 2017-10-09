---
title: "aaaSetup émulateur express toodebug des applications de Services de cloud computing dans Visual Studio | Documents Microsoft"
description: "Explique comment tooinstall hello tooenable redistribuable de C++ émulateur Express dans Visual Studio"
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
ms.openlocfilehash: 6fb506f0b1384f2e52310799eb5ae2a102d777bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="7b2ad-103">Utiliser l’émulateur Express une application de Services de cloud computing toodebug dans VS 2017</span><span class="sxs-lookup"><span data-stu-id="7b2ad-103">Use Emulator Express toodebug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="7b2ad-104">Cet article explique comment applications émulateur Express toouse toodebug Services de cloud computing dans VS 2017.</span><span class="sxs-lookup"><span data-stu-id="7b2ad-104">This article explains how toouse Emulator Express toodebug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="7b2ad-105">Contexte</span><span class="sxs-lookup"><span data-stu-id="7b2ad-105">Background context</span></span>
<span data-ttu-id="7b2ad-106">L’émulateur express est utilisé par défaut pour le débogage des rôles web et de travail des services cloud dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b2ad-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="7b2ad-107">Ce paramètre est spécifié dans la page de propriétés du projet de Services de cloud computing hello.</span><span class="sxs-lookup"><span data-stu-id="7b2ad-107">This setting is specified in hello Cloud Services project properties page.</span></span>

![Ouvrir les propriétés du projet][0]

![L’émulateur express est sélectionné par défaut][1]

<span data-ttu-id="7b2ad-110">Hello [Visual C++ Redistributable] [ Visual C++ Redistributable] pour Visual Studio est requis par l’émulateur express.</span><span class="sxs-lookup"><span data-stu-id="7b2ad-110">hello [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="7b2ad-111">Actuellement il n’est pas installé par hello la charge de travail Azure.</span><span class="sxs-lookup"><span data-stu-id="7b2ad-111">Currently it is not installed with hello Azure workload.</span></span> <span data-ttu-id="7b2ad-112">Fonction F5 les mouvements toodebug une application de Services de cloud computing, Visual Studio serait invite tooinstall ce composant et continuer le débogage.</span><span class="sxs-lookup"><span data-stu-id="7b2ad-112">Upon F5 gesture toodebug a Cloud Services applications, Visual Studio would prompt tooinstall this component and proceed with debugging.</span></span>

![Invite d’installation du redistribuable C++][2]

<span data-ttu-id="7b2ad-114">Cliquez sur Oui tooinstall de C++ Redistributable.</span><span class="sxs-lookup"><span data-stu-id="7b2ad-114">Click Yes tooinstall C++ Redistributable.</span></span>

![Installer le redistribuable C++][3]

<span data-ttu-id="7b2ad-116">Appuyez sur F5 à nouveau les sessions de débogage toolaunch.</span><span class="sxs-lookup"><span data-stu-id="7b2ad-116">Press F5 again toolaunch debugging sessions.</span></span>

![Démarrer le débogage][4]

![Débogage réussi][5]

> <span data-ttu-id="7b2ad-119">Remarque : l’installation du redistribuable Visual C++ n’est nécessaire qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="7b2ad-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="7b2ad-120">Si vous avez effectué une mise à niveau à partir d’une version antérieure du Kit de développement logiciel Azure et avez déjà installé l’émulateur express, vous ne rencontrerez pas ce problème.</span><span class="sxs-lookup"><span data-stu-id="7b2ad-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="7b2ad-121">Solution de contournement manuel</span><span class="sxs-lookup"><span data-stu-id="7b2ad-121">Manual workaround</span></span>
<span data-ttu-id="7b2ad-122">Vous pouvez également installer hello [Visual C++ Redistributable] [ Visual C++ Redistributable] manuellement et est appliquée même effet que la façon dont Visual Studio installée sur votre système.</span><span class="sxs-lookup"><span data-stu-id="7b2ad-122">You can also install hello [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="7b2ad-123">[VCRedist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="7b2ad-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="7b2ad-124">[VCRedist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="7b2ad-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b2ad-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7b2ad-125">Next Steps</span></span>
<span data-ttu-id="7b2ad-126">En savoir plus sur l’utilisation d’émulateur de calcul Azure toodebug vos applications de Services de cloud computing dans Visual Studio : [toorun d’à l’aide de l’émulateur Express et déboguer un service cloud sur un ordinateur local][Using Emulator Express toorun and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="7b2ad-126">Learn more about using Azure Computer Emulator toodebug your Cloud Services applications in Visual Studio: [Using Emulator Express toorun and debug a cloud service on a local machine][Using Emulator Express toorun and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express toorun and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
