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
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a>Utiliser l’émulateur Express une application de Services de cloud computing toodebug dans VS 2017
Cet article explique comment applications émulateur Express toouse toodebug Services de cloud computing dans VS 2017.

## <a name="background-context"></a>Contexte
L’émulateur express est utilisé par défaut pour le débogage des rôles web et de travail des services cloud dans Visual Studio. Ce paramètre est spécifié dans la page de propriétés du projet de Services de cloud computing hello.

![Ouvrir les propriétés du projet][0]

![L’émulateur express est sélectionné par défaut][1]

Hello [Visual C++ Redistributable] [ Visual C++ Redistributable] pour Visual Studio est requis par l’émulateur express. Actuellement il n’est pas installé par hello la charge de travail Azure. Fonction F5 les mouvements toodebug une application de Services de cloud computing, Visual Studio serait invite tooinstall ce composant et continuer le débogage.

![Invite d’installation du redistribuable C++][2]

Cliquez sur Oui tooinstall de C++ Redistributable.

![Installer le redistribuable C++][3]

Appuyez sur F5 à nouveau les sessions de débogage toolaunch.

![Démarrer le débogage][4]

![Débogage réussi][5]

> Remarque : l’installation du redistribuable Visual C++ n’est nécessaire qu’une seule fois. Si vous avez effectué une mise à niveau à partir d’une version antérieure du Kit de développement logiciel Azure et avez déjà installé l’émulateur express, vous ne rencontrerez pas ce problème.
> 
> 

## <a name="manual-workaround"></a>Solution de contournement manuel
Vous pouvez également installer hello [Visual C++ Redistributable] [ Visual C++ Redistributable] manuellement et est appliquée même effet que la façon dont Visual Studio installée sur votre système.

[VCRedist_x86.exe][vcredist_x86.exe]

[VCRedist_x64.exe][vcredist_x64.exe]

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur l’utilisation d’émulateur de calcul Azure toodebug vos applications de Services de cloud computing dans Visual Studio : [toorun d’à l’aide de l’émulateur Express et déboguer un service cloud sur un ordinateur local][Using Emulator Express toorun and debug a cloud service on a local machine]

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
