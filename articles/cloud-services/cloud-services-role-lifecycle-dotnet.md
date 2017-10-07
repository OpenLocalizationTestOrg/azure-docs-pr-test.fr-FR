---
title: "événements de cycle de vie de Service Cloud aaaHandle | Documents Microsoft"
description: "Explique comment utiliser des méthodes de cycle de vie hello d’un rôle de Service de cloud computing dans .NET"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 39b30acd-57b9-48b7-a7c4-40ea3430e451
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: cc0ccc5f055b965202b6e081a6ab72ad5d39b034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-lifecycle-of-a-web-or-worker-role-in-net"></a>Personnaliser hello du cycle de vie d’un rôle Web ou de travail dans .NET
Lorsque vous créez un rôle de travail, vous étendez hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) classe qui fournit des méthodes pour vous toooverride qui vous permettre de répondre à des événements de toolifecycle. Pour les rôles web, cette classe est facultative, vous devez l’utiliser dans les événements toolifecycle toorespond.

## <a name="extend-hello-roleentrypoint-class"></a>Étendre la classe RoleEntryPoint de hello
Hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) classe inclut des méthodes qui sont appelées par Azure lorsqu’elle **démarre**, **exécute**, ou **arrête** un rôle web ou de travail. Vous pouvez éventuellement substituer ces l’initialisation toomanage méthodes, séquences d’arrêt ou thread d’exécution hello du rôle de hello. 

Lors de l’extension **RoleEntryPoint**, vous devez être conscient de hello suit les comportements des méthodes de hello :

* Hello [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) et [OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) méthodes retournent une valeur booléenne, il est possible de tooreturn **false** à partir de ces méthodes.
  
   Si votre code renvoie **false**, processus de rôle hello se termine soudainement, sans exécuter une séquence d’arrêt peut avoir. En règle générale, vous devez éviter de retourner **false** de hello **OnStart** (méthode).
* Une exception non interceptée dans la surcharge d'une méthode **RoleEntryPoint** est traitée comme une exception non gérée.
  
   Si une exception se produit dans une des méthodes de cycle de vie hello, Azure déclenche hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) événement, et ensuite les processus hello sont terminée. Une fois mis hors connexion, votre rôle sera redémarré par Azure. Lorsqu’une exception non gérée se produit, hello [arrêt](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx) événement n’est pas déclenché et hello **OnStop** méthode n’est pas appelée.

Si votre rôle ne démarre pas ou est recyclé entre hello l’initialisation, occupés et arrêt des États, votre code peut lever une exception non gérée dans un des événements de cycle de vie hello que chaque rôle de hello temps redémarre. Dans ce cas, utilisez hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) événement toodetermine hello la cause de l’exception de hello et gérer de façon appropriée. Votre rôle peut également retourner hello [exécuter](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) (méthode), ce qui amène hello rôle toorestart. Pour plus d’informations sur les États de déploiement, consultez [tooRecycle de problèmes qui Cause rôles](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

> [!NOTE]
> Si vous utilisez hello **Azure Tools pour Microsoft Visual Studio** toodevelop votre application, des modèles de projet hello rôle étendent automatiquement hello **RoleEntryPoint** classe pour vous, Bonjour *WebRole.cs* et *WorkerRole.cs* fichiers.
> 
> 

## <a name="onstart-method"></a>Méthode OnStart
Hello **OnStart** méthode est appelée lorsque votre instance de rôle est remise en ligne par Azure. Pendant l’exécution de hello code OnStart, l’instance de rôle hello est marqué comme **occupé** et aucun trafic externe ne sera tooit dirigé par l’équilibrage de charge hello. Vous pouvez substituer cet méthode tooperform du travail d’initialisation, telles que la mise en œuvre des gestionnaires d’événements et le démarrage [Azure Diagnostics](cloud-services-how-to-monitor.md).

Si **OnStart** retourne **true**, hello instance est correctement initialisée et Azure appelle hello **RoleEntryPoint.Run** (méthode). Si **OnStart** retourne **false**, rôle de hello se termine immédiatement, sans exécuter les séquences d’arrêt planifié.

Hello suivant exemple de code montre comment toooverride hello **OnStart** (méthode). Cette méthode configure et démarre un moniteur de diagnostic lors de l’instance de rôle hello démarre et définit un transfert de la journalisation de compte de stockage de données tooa :

```csharp
public override bool OnStart()
{
    var config = DiagnosticMonitor.GetDefaultInitialConfiguration();

    config.DiagnosticInfrastructureLogs.ScheduledTransferLogLevelFilter = LogLevel.Error;
    config.DiagnosticInfrastructureLogs.ScheduledTransferPeriod = TimeSpan.FromMinutes(5);

    DiagnosticMonitor.Start("DiagnosticsConnectionString", config);

    return true;
}
```

## <a name="onstop-method"></a>Méthode OnStop
Hello **OnStop** méthode est appelée après qu’une instance de rôle a été mises hors connexion par Azure et avant l’arrêt du processus hello. Vous pouvez remplacer ce code toocall de méthode requis pour votre toocleanly d’instance de rôle arrêté.

> [!IMPORTANT]
> Le code s’exécutant dans hello **OnStop** méthode a une durée limitée de toofinish lorsqu’elle est appelée pour des raisons autres qu’un arrêt initié par l’utilisateur. Une fois cette durée écoulée, processus de hello se termine, donc vous devez vous assurer que le code Bonjour **OnStop** méthode peut s’exécuter rapidement ou qu’il peut ne pas en cours d’exécution toocompletion. Hello **OnStop** méthode est appelée après hello **arrêt** événement est déclenché.
> 
> 

## <a name="run-method"></a>Méthode Run
Vous pouvez remplacer hello **exécuter** méthode tooimplement un thread d’exécution longue pour votre instance de rôle.

Substitution de hello **exécuter** méthode n’est pas requise ; l’implémentation par défaut de hello démarre un thread qui se met en veille indéfiniment. Si vous ne substituez pas hello **exécuter** méthode, votre code sera bloqué indéfiniment. Si hello **exécuter** méthode est retournée, rôle de hello est automatiquement normalement recyclé ; en d’autres termes, Azure déclenche hello **arrêt** hello d’événements et les appels **OnStop** méthode afin que vos séquences d’arrêt puissent être exécutées avant que le rôle de hello est mis hors connexion.

### <a name="implementing-hello-aspnet-lifecycle-methods-for-a-web-role"></a>Implémentation des méthodes de cycle de vie ASP.NET hello pour un rôle web
Vous pouvez utiliser les méthodes de cycle de vie ASP.NET hello, en outre toothose fournie par hello **RoleEntryPoint** toomanage des séquences d’initialisation et d’arrêt pour un rôle web, de classe. Cela peut être utile à des fins de compatibilité si vous déplacez un tooAzure d’application ASP.NET existante. méthodes de cycle de vie ASP.NET Hello sont appelées à partir de hello **RoleEntryPoint** méthodes. Hello **Application\_Démarrer** méthode est appelée après hello **RoleEntryPoint.OnStart** fin de la méthode. Hello **Application\_fin** méthode est appelée avant hello **RoleEntryPoint.OnStop** méthode est appelée.

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment trop[créer un package de service cloud](cloud-services-model-and-package.md).

