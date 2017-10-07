---
title: "services de cloud computing aaaOptions pour le débogage Azure | Documents Microsoft"
description: "Débogage des services cloud Azure"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/18/2017
ms.author: kraigb
ms.openlocfilehash: 8b7779ca33cfd82fd5fbccf229ea822c311bdea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-hello-various-ways-toodebug-an-azure-cloud-service"></a>En savoir plus hello différentes manières toodebug un service cloud Azure
Cet article fournit des liens toohello différentes façons toodebug un service cloud Azure. 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>Débogage d’un service cloud Azure dans Visual Studio
Vous pouvez enregistrer temps et l’argent à l’aide de toodebug d’émulateur de calcul Azure hello votre service cloud sur un ordinateur local. Déboguer un service localement avant de le déployer vous permet d’améliorer la fiabilité et les performances, tout en évitant les coûts de temps de calcul. Certaines erreurs peuvent toutefois se produire quand vous exécutez un service cloud directement dans Azure. Les erreurs qui se produisent uniquement lorsque vous exécutez un service cloud dans Azure peuvent être débogués en activant le débogage distant lorsque vous publiez votre service, puis en attachant l’instance de rôle du débogueur tooa hello. Pour plus d’informations, consultez [Déboguer votre service cloud sur votre ordinateur local](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer).

## <a name="using-azure-diagnostics"></a>Utilisation des diagnostics Azure 
Vous pouvez utiliser les Diagnostics Azure toolog obtenir des informations détaillées à partir de l’exécution de code dans des rôles, si les rôles hello sont en cours d’exécution dans l’environnement de développement hello ou dans Azure. Pour plus d’informations, consultez la page [Activation des diagnostics Azure dans Azure Cloud Services](http://go.microsoft.com/fwlink/p/?LinkId=400450).

## <a name="using-intellitrace"></a>Utilisation d’IntelliTrace 
Si vous utilisez des rôles de Visual Studio Enterprise toowrite ciblé .NET Framework 4.5, vous pouvez activer IntelliTrace au moment de hello que vous déployez un service cloud Azure depuis Visual Studio. IntelliTrace fournit un journal que vous pouvez utiliser avec Visual Studio toodebug votre application comme s’il s’exécutait dans Azure. Pour plus d’informations, consultez [Débogage d’un service cloud publié avec IntelliTrace et Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623016).

## <a name="remote-debugging"></a>Débogage à distance 
Vous pouvez activer le débogage distant sur vos services cloud au moment de hello lorsque vous déployez le service de cloud hello à partir de Visual Studio. Si vous choisissez tooenable pour un déploiement de débogage distant, les services de débogage distants sont installés sur des machines virtuelles hello qui s’exécutent chaque instance de rôle. Ces services, tels que `msvsmon.exe`, n’affectent pas les performances et n’entraînent pas de coûts supplémentaires. Pour plus d’informations, consultez [Déboguer un service cloud dans Azure](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure).

## <a name="next-steps"></a>Étapes suivantes
- [Débogage d’un service cloud Azure ou une machine virtuelle dans Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md) -en savoir plus de détails hello de services de cloud toodebug Azure.
