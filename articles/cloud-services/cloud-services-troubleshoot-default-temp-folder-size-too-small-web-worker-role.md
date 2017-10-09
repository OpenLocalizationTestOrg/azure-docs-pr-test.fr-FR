---
title: "taille du dossier TEMP aaaDefault est trop petite pour un rôle | Documents Microsoft"
description: "Un rôle de service cloud a une quantité limitée d’espace pour le dossier temporaire hello. Cet article fournit des suggestions sur la façon de tooavoid manque d’espace."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f2af8dd-2012-4b36-9dd5-19bf6a67e47d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 307dc20f3264e29d122a6616be0028d2ec1282c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a>La taille par défaut du dossier TEMP est trop petite pour un rôle web/de travail de service cloud
la valeur par défaut Hello répertoire temporaire d’un rôle web ou de travail du service cloud a une taille maximale de 100 Mo, ce qui peut devenir complète à un moment donné. Cet article décrit comment tooavoid manque d’espace pour le répertoire temporaire de hello.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a>Pourquoi l’espace devient-il insuffisant ?
Hello standard Windows variables d’environnement TEMP et TMP sont toocode disponible qui est en cours d’exécution dans votre application. TEMP et TMP point tooa répertoire unique qui a une taille maximale de 100 Mo. Toutes les données stockées dans ce répertoire ne sont pas conservées lors du cycle de vie hello du service de cloud hello ; Si les instances de rôle hello dans un service cloud sont recyclées, répertoire de hello est nettoyé.

## <a name="suggestion-toofix-hello-problem"></a>Problème de suggestion toofix hello
Implémentez l’une des hello suivant alternatives :

* Configurez une ressource de stockage local et accédez-y directement au lieu d’utiliser TEMP ou TMP. tooaccess une ressource de stockage local à partir de code qui s’exécute au sein de votre application, l’appel hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) (méthode).
* Configurez une ressource de stockage local et pointez hello TEMP et TMP répertoires toopoint toohello chemin d’accès de ressource de stockage local hello. Cette modification doit être effectuée dans hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) (méthode).

Hello exemple de code suivant montre comment toomodify hello répertoires cibles pour TEMP et TMP à partir de la méthode OnStart de hello :

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // hello local resource declaration must have been added toothe
            // service definition file for hello role named WorkerRole1:
            //
            // <LocalResources>
            //    <LocalStorage name="CustomTempLocalStore"
            //                  cleanOnRoleRecycle="false"
            //                  sizeInMB="1024" />
            // </LocalResources>

            string customTempLocalResourcePath =
            RoleEnvironment.GetLocalResource("CustomTempLocalStore").RootPath;
            Environment.SetEnvironmentVariable("TMP", customTempLocalResourcePath);
            Environment.SetEnvironmentVariable("TEMP", customTempLocalResourcePath);

            // hello rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a>Étapes suivantes
Lire un blog décrivant [comment tooincrease hello taille du dossier temporaire de ASP.NET rôle Web Azure de hello](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).

Affichez plus d’ [articles de résolution des problèmes](/?tag=top-support-issue&product=cloud-services) liés aux services cloud.

toolearn comment les problèmes de rôle du service cloud tootroubleshoot à l’aide de données de diagnostic d’ordinateur PaaS Azure, afficher [série du blog de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
