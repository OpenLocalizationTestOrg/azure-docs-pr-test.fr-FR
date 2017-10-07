---
title: les journaux aaaStreaming et console
description: Vue d'ensemble des journaux et de la console de diffusion en continu
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a>Journaux de diffusion en continu et hello Console
## <a name="streaming-logs"></a>Journaux en continu
Hello **portail Azure** fournit une visionneuse du journal en continu intégrée qui vous permet d’afficher les événements de suivi à partir de votre **du Service d’applications** applications en temps réel.  

La configuration de cette fonction se fait en quelques étapes simples :

* Écriture des suivis dans votre code
* Activation des **journaux de diagnostic** pour votre application
* Flux de hello vue à partir d’intégrées de hello **journaux de diffusion en continu** UI Bonjour **portail Azure**.

### <a name="how-toowrite-traces-in-your-code"></a>Comment toowrite effectue le suivi dans votre code
L'écriture des suivis dans votre code est simple.  En c#, il est aussi simple que l’écriture hello suivant de code :

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

Hello classe Trace réside dans l’espace de noms System.Diagnostics hello.

Dans une application node.js, vous pouvez écrire ce code tooachieve hello même résultat :

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a>Comment tooenable et vue hello des journaux de diffusion en continu
![][BrowseSitesScreenshot] Les diagnostics sont activés par application. Commencez par parcourir le site de toohello que vous aimeriez tooenable cette fonctionnalité.  

![][DiagnosticsLogs]À partir du menu Paramètres, faites défiler la liste toohello **analyse** section, puis cliquez sur **(1) des journaux de Diagnostic**. Puis **(2) activer** **journalisation des applications (système de fichiers)** ou **journalisation des applications (blob)** hello **niveau** option vous permet de modifier hello niveau de gravité de traces toocapture. Si vous essayez simplement tooget familiarisé avec la fonctionnalité de hello, définissez le niveau de hello trop**Verbose** tooensure toutes vos instructions de trace sont collectées.

Cliquez sur **enregistrer** haut hello Panneau de hello et que vous êtes prêt tooview journaux.

> [!NOTE]
> Bonjour supérieur Bonjour **au niveau de gravité** hello davantage de ressources sont consommé toolog et hello plus traces produites. Assurez-vous que **au niveau de gravité** est toohello configuré un niveau de détail approprié pour une production ou les sites à trafic important. 
> 
> 

![][StreamingLogsScreenshot]tooview hello **journaux de diffusion en continu** dans hello portail Azure, cliquez sur **flux du journal (1)** également dans hello **analyse** section du menu Paramètres de hello. Si votre application écrit activement les instructions de trace, vous devez les voir Bonjour **de diffusion en continu (2) connecte à l’interface utilisateur** quasiment en temps réel.

## <a name="console"></a>Console
Hello **portail Azure** fournit à l’application de console accès tooyour. Vous pouvez explorer le système de fichiers de l’application et exécuter les scripts powershell/cmd. Vous sont liés par hello autorisations mêmes définies en tant que code de votre application en cours d’exécution lors de l’exécution de commandes de la console. Répertoires de tooprotected Access ou des scripts en cours d’exécution qui nécessitent des autorisations élevées est bloquée.  

![][ConsoleScreenshot]À partir du menu Paramètres, faites défiler la liste trop**outils de développement** section, puis cliquez sur **Console (1)** et hello **(2) console** toohello droite s’ouvre l’interface utilisateur.

tooget familiarisé avec hello **console**, essayez les commandes de base telles que :

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
