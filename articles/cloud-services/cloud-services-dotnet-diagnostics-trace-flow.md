---
title: flux de hello aaaTrace dans une Application de Services de Cloud avec Azure Diagnostics | Documents Microsoft
description: "Ajouter le traçage messages tooan Azure toohelp le débogage des applications, mesurer les performances, analyse, analyse du trafic et bien plus encore."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a>Flux de hello de trace d’une application de Services de Cloud avec Azure Diagnostics
Le suivi est un moyen pour vous toomonitor hello l’exécution de votre application pendant son exécution. Vous pouvez utiliser hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), et [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) toorecord des informations sur les erreurs de classes et exécution de l’application dans des journaux, des fichiers texte ou autres appareils pour une analyse ultérieure. Pour plus d’informations sur le suivi, consultez [Applications de suivi et instrumentation](https://msdn.microsoft.com/library/zs6s4h68.aspx).

## <a name="use-trace-statements-and-trace-switches"></a>Utilisez les instructions et commutateurs de suivi
Le traçage d’implémenter dans votre application de Services de cloud computing en ajoutant hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello configuration de l’application et apporté des appels tooSystem.Diagnostics.Trace ou à System.Diagnostics.Debug dans votre code de l’application. Utilisez un fichier configuration hello *app.config* pour les rôles de travail et hello *web.config* pour les rôles web. Lorsque vous créez un nouveau service hébergé à l’aide d’un modèle Visual Studio, les Diagnostics Azure est automatiquement ajouté toohello projet et hello DiagnosticMonitorTraceListener est ajouté le fichier de configuration approprié toohello pour les rôles hello que vous ajoutez.

Pour plus d’informations sur le placement des instructions de trace, consultez [Comment : ajouter des instructions de Trace tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).

En plaçant des [Commutateurs de suivi](https://msdn.microsoft.com/library/3at424ac.aspx) dans votre code, vous pouvez contrôler le traçage et son importance. Cela vous permet de surveiller l’état de hello de votre application dans un environnement de production. ce qui est particulièrement important dans une application qui utilise plusieurs composants s’exécutant sur plusieurs ordinateurs. Pour plus d’informations, consultez la rubrique [Procédure : configuration de commutateurs de trace](https://msdn.microsoft.com/library/t06xyy08.aspx).

## <a name="configure-hello-trace-listener-in-an-azure-application"></a>Configurer un écouteur de suivi hello dans une application Windows Azure
Trace, Debug et TraceSource, vous demander de configurer « écouteurs » toocollect et messages hello enregistrements qui sont envoyés. Les écouteurs recueillent, stockent et acheminent les messages de suivi. Elles indiquent hello suivi sortie tooan cible appropriée, telle qu’un journal, une fenêtre ou un fichier texte. Diagnostics Azure utilise hello [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) classe.

Avant d’effectuer hello suivant la procédure, vous devez initialiser hello moniteur de diagnostic Azure. toodo, consultez [activation des Diagnostics dans Microsoft Azure](cloud-services-dotnet-diagnostics.md).

Notez que si vous utilisez des modèles hello fournis par Visual Studio, hello configuration du port d’écoute hello est ajoutée automatiquement pour vous.

### <a name="add-a-trace-listener"></a>Ajouter un écouteur de suivi
1. Ouvrez le fichier web.config ou app.config de hello pour votre rôle.
2. Ajoutez hello fichier toohello de code suivant. Modifier hello Version attribut toouse hello numéro de version de l’assembly que vous référencez hello. version de l’assembly Hello ne change pas nécessairement avec chaque version de Windows Azure SDK sauf s’il existe des mises à jour tooit.
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > Assurez-vous que vous avez un toohello de référence de projet Microsoft.WindowsAzure.Diagnostics assembly. Numéro de version de mise à jour hello dans xml hello au-dessus de version de hello toomatch de hello référencé Microsoft.WindowsAzure.Diagnostics assembly.
   > 
   > 
3. Enregistrez le fichier de configuration hello.

Pour plus d’informations sur les écouteurs, consultez [Suivi des écouteurs](https://msdn.microsoft.com/library/4y5y10s7.aspx).

Après avoir terminé le port d’écoute hello étapes tooadd hello, vous pouvez ajouter le code de tooyour instructions de trace.

### <a name="tooadd-trace-statement-tooyour-code"></a>code de tooyour tooadd trace instruction
1. Ouvrez un fichier source pour votre application. Par exemple, hello <RoleName>fichier .cs pour le rôle de travail hello ou rôle web.
2. Ajoutez hello qui suit à l’aide d’instruction si elle n’a pas déjà été ajoutée :
    ```
        using System.Diagnostics;
    ```
3. Ajoutez les instructions Trace où vous souhaitez des informations de toocapture état hello de votre application. Vous pouvez utiliser une variété de sortie de hello tooformat méthodes Hello instruction de Trace. Pour plus d’informations, consultez [Comment : ajouter des instructions de Trace tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).
4. Enregistrez le fichier de source de hello.

