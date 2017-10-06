---
title: performances aaaApplication FAQ pour les applications web Azure | Documents Microsoft
description: "Obtenir elles sonttrop des réponses aux questions sur la disponibilité, les performances et les problèmes des applications dans la fonctionnalité d’applications Web hello du Service d’applications Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 7f2383743079e4c630fd548b0efd9993029afe11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-faqs-for-web-apps-in-azure"></a>FAQ sur les performances des applications web Azure dans Azure

Cet article a elles sonttrop des réponses aux questions (FAQ) sur les problèmes de performances des applications pour hello [fonctionnalité des applications Web d’Azure App Service](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-is-my-app-slow"></a>Pourquoi mon application est-elle lente ?

Plusieurs facteurs peuvent contribuer tooslow performances de l’application. Pour obtenir des étapes de dépannage détaillées, consultez [Résoudre les problèmes de lenteur d’une application web](app-service-web-troubleshoot-performance-degradation.md).

## <a name="how-do-i-troubleshoot-a-high-cpu-consumption-scenario"></a>Comment puis-je résoudre un problème de consommation excessive du processeur ?

Dans certaines situations de consommation excessive du processeur, votre application peut vraiment nécessiter davantage de ressources informatiques. Dans ce cas, envisagez la mise à l’échelle de niveau de service supérieur tooa afin de l’application hello obtienne toutes les ressources hello dont il a besoin. Dans d’autres cas, une consommation excessive du processeur peut être due à une boucle incorrecte ou à une méthode de codage. Obtenir un aperçu de ce qui déclenche une consommation excessive du processeur est un processus en deux parties. Créez d’abord un vidage de processus et ensuite analyser le vidage de processus hello. Pour plus d’informations, consultez [Capturer et analyser un fichier de vidage en cas de consommation excessive du processeur pour Web Apps](https://blogs.msdn.microsoft.com/asiatech/2016/01/20/how-to-capture-dump-when-intermittent-high-cpu-happens-on-azure-web-app/).

## <a name="how-do-i-troubleshoot-a-high-memory-consumption-scenario"></a>Comment résoudre les problèmes de consommation excessive de la mémoire ?

Dans certaines situations de consommation excessive de mémoire, votre application peut vraiment nécessiter davantage de ressources informatiques. Dans ce cas, envisagez la mise à l’échelle de niveau de service supérieur tooa afin de l’application hello obtienne toutes les ressources hello dont il a besoin. Parfois, un bogue dans le code hello peut entraîner une fuite de mémoire. Une pratique de codage peut également augmenter la consommation de mémoire. Obtenir un aperçu de ce qui déclenche une consommation excessive de mémoire est un processus en deux parties. Créez d’abord un vidage de processus et ensuite analyser le vidage de processus hello. Diagnostic d’incident à partir de hello Galerie d’extensions Azure Site peut effectuer efficacement ces deux étapes. Pour plus d’informations, consultez [Capturer et analyser un fichier de vidage en cas de consommation excessive intermittente de mémoire pour Web Apps](https://blogs.msdn.microsoft.com/asiatech/2016/02/02/how-to-capture-and-analyze-dump-for-intermittent-high-memory-on-azure-web-app/).

## <a name="how-do-i-automate-app-service-web-apps-by-using-powershell"></a>Comment automatiser les applications web App Service à l’aide de PowerShell ?

Vous pouvez utiliser toomanage d’applets de commande PowerShell et gérer des applications de Service d’applications web. Dans notre publication de blog [automatiser des applications web hébergées dans Azure App Service à l’aide de PowerShell](https://blogs.msdn.microsoft.com/puneetgupta/2016/03/21/automating-webapps-hosted-in-azure-app-service-through-powershell-arm-way/), nous allons décrire comment tooautomate toouse basée sur le Gestionnaire de ressources Azure de PowerShell applets de commande des tâches courantes. billet de blog Hello possède également un exemple de code pour diverses tâches de gestion des applications web. Pour des descriptions et la syntaxe de toutes les applets de commande des applications web App Service, consultez [AzureRM.Websites](https://docs.microsoft.com/powershell/module/azurerm.websites/?view=azurermps-4.0.0).

## <a name="how-do-i-view-my-web-apps-event-logs"></a>Comment afficher les journaux des événements de mon application web ?

les journaux d’événements de votre application web tooview :

1. Connectez-vous à tooyour [site Web de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. Dans le menu de hello, sélectionnez **Console de débogage** > **CMD**.
3. Sélectionnez hello **LogFiles** dossier.
4. journaux des événements tooview, sélectionnerez icône de crayon hello trop**eventlog.xml**.
5. journaux de hello toodownload, exécutez l’applet de commande PowerShell hello `Save-AzureWebSiteLog -Name webappname`.

## <a name="how-do-i-capture-a-user-mode-memory-dump-of-my-web-app"></a>Comment capturer un vidage de mémoire en mode utilisateur de mon application web ?

toocapture un vidage de mémoire en mode utilisateur de votre application web :

1. Connectez-vous à tooyour [site Web de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. Sélectionnez hello **Process Explorer** menu.
3. Avec le bouton hello **w3wp.exe** processus ou votre tâche Web.
4. Sélectionnez **Télécharger le vidage de mémoire** > **Vidage complet**.

## <a name="how-do-i-view-process-level-info-for-my-web-app"></a>Comment afficher les informations au niveau processus pour mon application web ?

Vous avez deux options pour afficher les informations au niveau processus pour votre application web :

*   Bonjour portail Azure :
    1. Ouvrez hello **Process Explorer** pour l’application web de hello.
    2. toosee hello plus d’informations, sélectionnez hello **w3wp.exe** processus.
*   Dans la console Kudu hello :
    1. Connectez-vous à tooyour [site Web de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
    2. Sélectionnez hello **Process Explorer** menu.
    3. Pourquoi **w3wp.exe** processus, sélectionnez **propriétés**.

## <a name="when-i-browse-toomy-app-i-see-error-403---this-web-app-is-stopped-how-do-i-resolve-this"></a>Lorsque vous parcourez toomy application, voir « Erreur 403 - cette application web est arrêtée. » Comment résoudre ce problème ?

Trois conditions peuvent provoquer cette erreur :

* l’application web Hello a atteint une limite de facturation et votre site a été désactivé.
* l’application Hello web a été arrêtée dans le portail de hello.
* l’application web Hello a atteint une limite de quota de ressources qui peut-être s’appliquer tooa gratuit ou partagé le plan de service mise à l’échelle.

toosee cause erreur de hello et problème de hello tooresolve, hello de suivre les étapes [les applications Web : « Erreur 403 : cette application web est arrêtée »](https://blogs.msdn.microsoft.com/waws/2016/01/05/azure-web-apps-error-403-this-web-app-is-stopped/).

## <a name="where-can-i-learn-more-about-quotas-and-limits-for-various-app-service-plans"></a>Où puis-je obtenir plus d’informations sur les quotas et les limites des différents plans App Service ?

Pour plus d’informations sur les quotas et les limites, consultez [Limites App Service](../azure-subscription-service-limits.md#app-service-limits). 

## <a name="how-do-i-decrease-hello-response-time-for-hello-first-request-after-idle-time"></a>Comment réduire les temps de réponse hello pour la première demande de hello après la durée d’inactivité

Par défaut, les applications web sont déchargées si elles restent inactives pendant un laps de temps défini. De cette manière, système de hello peut économiser les ressources. Hello inconvénient que hello réponse toohello première demande une fois l’application web hello déchargée est plus long, tooallow hello tooload d’application web et commencer le traitement des réponses. Dans les plans de service de base et Standard, vous pouvez activer hello **Always On** paramètre tookeep hello application est toujours chargée. Cela élimine le temps de chargement plus une fois l’application hello est inactive. toochange hello **Always On** paramètre :

1. Dans hello portail Azure, accédez à l’application web tooyour.
2. Sélectionnez **Paramètres de l'application**.
3. Pour **Always On**, sélectionnez **On**.

## <a name="how-do-i-turned-on-failed-request-tracing"></a>Comment activer le suivi des demandes ayant échoué ?

tooturn sur le suivi des demandes ayant échoué :

1. Dans hello portail Azure, accédez à l’application web tooyour.
3. Sélectionnez **Tous les paramètres** > **Journaux de diagnostic**.
4. Pour **Suivi des demandes ayant échoué**, sélectionnez **On**.
5. Sélectionnez **Enregistrer**.
6. Dans le panneau de l’application hello web, sélectionnez **outils**.
7. Sélectionnez **Visual Studio Online**.
8. Si le paramètre de hello n’est pas **sur**, sélectionnez **sur**.
9. Sélectionnez **Go**.
10. Sélectionnez **Web.config**.
11. Dans system.webServer, ajoutez cette configuration (toocapture une URL spécifique) :

    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*api*" />
    <add path="*api*">
    <traceAreas>
    <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
12. problèmes de performances lentes tootroubleshoot, ajoutez cette configuration (si hello capture demande prend plus de 30 secondes) :
    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*" />
    <add path="*">
    <traceAreas> <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions timeTaken="00:00:30" statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
13. hello de toodownload Échec de la trace des demandes, Bonjour [portal](https://portal.azure.com), accédez tooyour site.
15. Sélectionnez **Outils** > **Kudu** > **Go**.
18. Dans le menu de hello, sélectionnez **Console de débogage** > **CMD**.
19. Sélectionnez hello **LogFiles** le dossier et sélectionnez hello avec un nom qui commence par **W3SVC**.
20. fichier XML de hello toosee, icône de crayon hello select.

## <a name="i-see-hello-message-worker-process-requested-recycle-due-toopercent-memory-limit-how-do-i-address-this-issue"></a>Je vois le message de type hello « processus de travail a demandé le recyclage too'Percent échéance mémoire ' limite. » Comment pour résoudre ce problème ?

Hello disponible quantité maximale de mémoire pour un processus 32 bits (même sur un système d’exploitation de 64 bits) est de 2 Go. Par défaut, les processus de travail hello a la valeur too32 bits dans le Service d’application (pour la compatibilité avec les applications web héritées).

Songez à passer too64 des processus qui vous pouvez tirer parti de hello supplémentaire de mémoire disponible dans votre rôle traitement Web. Comme cette opération déclenche un redémarrage de l’application web, vous devez la planifier en conséquence.

Notez également qu’un environnement 64 bits nécessite un plan de service De base ou Standard. Les plans Gratuit et Partagé s’exécutent toujours dans un environnement 32 bits.

Pour plus d’informations, consultez [Configurer des applications web dans App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-configure).

## <a name="why-does-my-request-time-out-after-240-seconds"></a>Pourquoi ma demande expire-t-elle après 240 secondes ?

L’équilibrage de charge Azure comporte un paramètre de délai d’inactivité par défaut de quatre minutes. Il s’agit généralement d’un délai de réponse raisonnable pour une demande web. Si votre application web requiert un traitement en arrière-plan, nous vous recommandons d’utiliser des tâches Azure WebJob. application web Azure de Hello peut appeler des tâches Web et être avertie lorsque le traitement en arrière-plan est terminé. Vous pouvez choisir parmi plusieurs méthodes pour utiliser des tâches WebJob, y compris des files d’attente et des déclencheurs.

Les tâches WebJob sont conçues pour le traitement en arrière-plan. Vous pouvez effectuer autant de traitement en arrière-plan que vous le souhaitez dans une tâche WebJob. Pour plus d’informations sur les tâches WebJob, consultez [Exécuter des tâches en arrière-plan avec des tâches WebJob](https://docs.microsoft.com/azure/app-service-web/web-sites-create-web-jobs).

## <a name="aspnet-core-applications-that-are-hosted-in-app-service-sometimes-stop-responding-how-do-i-fix-this-issue"></a>Les applications ASP.NET Core hébergées dans App Service cessent parfais de répondre. Comment résoudre ce problème ?

Un problème connu avec une version [version de Kestrel](https://github.com/aspnet/KestrelHttpServer/issues/1182) peut entraîner une application ASP.NET Core 1.0 qui est hébergée dans le blocage du Service d’applications toointermittently. Vous pouvez également voir ce message : « hello spécifié l’Application CGI a rencontré un erreur hello serveur arrêté hello processus. »

Ce problème est résolu dans Kestrel version 1.0.2. Cette version est incluse dans hello mise à jour ASP.NET Core 1.0.3. tooresolve ce problème, assurez-vous que vous mettez à jour votre toouse de dépendances d’application Kestrel la version 1.0.2. Vous pouvez également utiliser une des deux solutions de contournement sont décrites dans le billet de blog hello [des performances lentes à ASP.NET Core 1.0 problèmes dans les applications de Service d’applications web](https://blogs.msdn.microsoft.com/waws/2016/12/11/asp-net-core-slow-perf-issues-on-azure-websites).


## <a name="i-cant-find-my-log-files-in-hello-file-structure-of-my-web-app-how-can-i-find-them"></a>Impossible de trouver mon fichiers journaux dans la structure de fichier hello de mon application web. Comment puis-je les trouver ?

Si vous utilisez la fonctionnalité de Cache locale hello du Service d’application, la structure de dossiers de hello Hello LogFiles et des dossiers de données pour votre instance de Service d’applications sont affectées. Lorsque le Cache Local est utilisé, les sous-dossiers sont créés dans le stockage hello LogFiles et des dossiers de données. utilisation de sous-dossiers Hello hello d’affectation de noms « unique identificateur de modèle » + horodatage. Chaque sous-dossier correspond tooa instance de machine virtuelle dans le hello application web est en cours d’exécution ou exécuté.

toodetermine si vous utilisez le Cache Local, vérifiez votre application de Service **paramètres de l’Application** onglet. Si le Cache Local est utilisé, de paramètre d’application hello `WEBSITE_LOCAL_CACHE_OPTION` est défini trop`Always`. Pour plus d’informations sur le Cache Local, consultez hello [vue d’ensemble de la mémoire Cache locale de Service d’application](https://docs.microsoft.com/azure/app-service/app-service-local-cache).

Si vous n’utilisez pas la fonctionnalité Cache local et que vous rencontrez ce problème, envoyez une demande de support.

## <a name="i-see-hello-message-an-attempt-was-made-tooaccess-a-socket-in-a-way-forbidden-by-its-access-permissions-how-do-i-resolve-this"></a>Je vois le message de type hello » une tentative a été effectuée tooaccess un socket de manière interdite par ses autorisations d’accès. » Comment résoudre ce problème ?

Cette erreur se produit généralement si les connexions TCP sortantes hello sur l’instance de machine virtuelle hello sont épuisées. Dans le Service d’application, les limites sont appliquées pour le nombre maximal de hello de connexions sortantes qui peut être effectuée pour chaque instance de machine virtuelle. Pour plus d’informations, consultez [Limites numériques entre les machines virtuelles](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#cross-vm-numerical-limits).

Cette erreur peut également se produire si vous essayez de tooaccess une adresse locale à partir de votre application. Pour plus d’informations, consultez [Demandes d’adresses locales](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#local-address-requests).

Pour plus d’informations sur les connexions sortantes dans votre application web, voir hello blog sur [sortantes des sites Web de connexions tooAzure](http://www.freekpaans.nl/2015/08/starving-outgoing-connections-on-windows-azure-web-sites/).

## <a name="how-do-i-use-visual-studio-tooremote-debug-my-app-service-web-app"></a>Comment utiliser débogage tooremote de Visual Studio mon application Service web d’application ?

Pour une procédure pas à pas détaillées qui vous montre comment toodebug votre application web à l’aide de Visual Studio, consultez [à distance déboguer votre application web de Service d’applications](https://blogs.msdn.microsoft.com/benjaminperkins/2016/09/22/remote-debug-your-azure-app-service-web-app/).
