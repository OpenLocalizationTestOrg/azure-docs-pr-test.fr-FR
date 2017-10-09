---
title: "aaaBest pratiques et guide de dépannage pour les applications du nœud sur Azure Web Apps"
description: "Découvrez hello meilleures pratiques et les étapes de dépannage pour les applications du nœud sur Azure Web Apps."
services: app-service\web
documentationcenter: nodejs
author: ranjithr
manager: wadeh
editor: 
ms.assetid: 387ea217-7910-4468-8987-9a1022a99bef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 06/06/2016
ms.author: ranjithr
ms.openlocfilehash: 975898142a224f14df1091a46d16e9074d9e2831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-and-troubleshooting-guide-for-node-applications-on-azure-web-apps"></a>Meilleures pratiques et guide de dépannage pour les applications node sur Azure Web Apps
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Dans cet article, vous allez apprendre hello meilleures pratiques et les étapes de résolution [applications node](app-service-web-get-started-nodejs.md) en cours d’exécution sur les applications Web de Azure (avec [iisnode](https://github.com/azure/iisnode)).

> [!WARNING]
> Soyez vigilant lorsque vous appliquez ces étapes de dépannage sur votre site de production. Il est recommandé tootroubleshoot votre application sur une production non-programme d’installation par exemple votre emplacement intermédiaire et lorsque hello est résolu, remplacez votre emplacement intermédiaire avec votre emplacement de production.
> 
> 

## <a name="iisnode-configuration"></a>Configuration de IISNODE
Cela [fichier de schéma](https://github.com/Azure/iisnode/blob/master/src/config/iisnode_schema_x64.xml) montre tous les paramètres de hello qui peuvent être configurés pour iisnode. Certains paramètres de hello qui peuvent être utiles pour votre application sont :

* nodeProcessCountPerApplication
  
    Ce paramètre contrôle le nombre de hello de processus de nœud qui sont lancées par l’application IIS. La valeur par défaut est 1. Vous pouvez lancer autant de node.exe en tant que le nombre de cœurs de machine virtuelle en définissant cette too0. Valeur recommandée est 0 pour la plupart des applications, vous pouvez utiliser tous les cœurs de hello sur votre ordinateur. Node.exe est le seul thread pour un node.exe consommera un maximum de 1 core et tooget maximale des performances en dehors de votre application de nœud vous souhaiteriez tooutilize tous les cœurs.
* nodeProcessCommandLine
  
    Ce paramètre contrôle hello chemin toohello node.exe. Vous pouvez définir cette version de valeur toopoint tooyour node.exe.
* maxConcurrentRequestsPerProcess
  
    Ce paramètre contrôle le nombre maximal de hello de demandes simultanées envoyé par iisnode tooeach node.exe. Sur les applications Web d’azure, valeur par défaut de hello est infini. Vous n’aurez pas tooworry sur ce paramètre. En dehors d’azure WebApp, hello par défaut est 1024. Vous pourriez tooconfigure cela en fonction du nombre de requêtes votre application obtient et la vitesse à laquelle votre application traite chaque demande.
* maxNamedPipeConnectionRetry
  
    Ce paramètre contrôle le nombre maximal de hello d’iisnode effectuera une nouvelle tentative en connexion sur hello nommée requête de canal toosend hello sur toonode.exe. Ce paramètre conjointement avec namedPipeConnectionRetryDelay détermine hello un délai d’attente total de chaque demande dans iisnode. La valeur par défaut est 200 sur Azure Webapps. Délai total d’expiration en secondes = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1 000
* namedPipeConnectionRetryDelay
  
    Attend que ce paramètre contrôles hello quantité iisnode de temps (en ms) entre chaque nouvelle tentative toosend demande toonode.exe sur hello canal nommé. La valeur par défaut est 250 ms.
    Délai total d’expiration en secondes = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1 000
  
    Par défaut hello un délai d’attente total en iisnode sur les applications Web azure est 200 \* 250ms = 50 secondes.
* logDirectory
  
    Ce paramètre contrôle Active hello où iisnode enregistrera stdout/stderr. Valeur par défaut est iisnode, qui est relatif toohello script principal répertoire (où server.js principal est présent)
* debuggerExtensionDll
  
    Ce paramètre contrôle la version de node inspector qu’utilisera iisnode lors du débogage de votre application node. Actuellement iisnode-inspecteur-0.7.3.dll et iisnode-inspector.dll sont hello uniquement 2 valides pour ce paramètre. La valeur par défaut est iisnode-inspector 0.7.3.dll. version d’iisnode-inspecteur-0.7.3.dll utilise inspecteur-nœud-0.7.3 et websockets, vous devrez donc tooenable websockets sur votre toouse webapp azure cette version. Consultez <http://www.ranjithr.com/?p=98> pour plus d’informations sur comment tooconfigure iisnode toouse hello inspecteur de nœud de nouveau.
* flushResponse
  
    comportement par défaut de Hello d’IIS est qu’il met en mémoire tampon des données de réponse des too4MB avant de vider les ou fin hello de réponse de hello, selon ce qui se produit en premier. iisnode offre un paramètre toooverride ce comportement de configuration : tooflush un fragment du corps d’entité de réponse de hello dès qu’iisnode reçoit de node.exe, vous devez tooset hello iisnode/@flushResponse attribut dans web.config too'true':
  
    ```
    <configuration>    
        <system.webServer>    
            <!-- ... -->    
            <iisnode flushResponse="true" />    
        </system.webServer>    
    </configuration>
    ```
  
    L’activation de vidage de chaque fragment hello entité du corps de réponse ajoute une surcharge de performances qui réduit le débit du système de hello hello ~ 5 % (as of v0.1.13), donc il est mieux tooscope cette tooendpoints seul paramètre nécessitant une réponse de diffusion en continu (par exemple, à l’aide de hello <location> élément dans le fichier web.config de hello)
  
    Dans toothis d’ajout, de diffusion en continu des applications, vous devez responseBufferLimit de jeu tooalso de votre too0 Gestionnaire d’iisnode.
  
    ```
    <handlers>    
        <add name="iisnode" path="app.js" verb="\*" modules="iisnode" responseBufferLimit="0"/>    
    </handlers>
    ```
* watchedFiles
  
    Liste de fichiers séparés par des points-virgules dont les modifications feront l’objet d’une surveillance. Un fichier de tooa modification provoque hello application toorecycle. Chaque entrée se compose d’un nom de répertoire facultatif plus d’un nom de fichier requise relative toohello le répertoire où se trouve le point d’entrée principale de l’application hello sont. Les caractères génériques sont autorisés dans la partie de nom des fichiers de hello uniquement. La valeur par défaut est « \*. js;web.config ».
* recycleSignalEnabled
  
    La valeur par défaut est false. S’il est activé, votre application de nœud peut se connecter tooa de canal nommé (variable d’environnement IISNODE\_contrôle\_canal) et envoyer un message « recyclage ». Cela entraîne en douceur hello w3wp toorecycle.
* idlePageOutTimePeriod
  
    La valeur par défaut est 0, ce qui signifie que cette fonctionnalité est désactivée. Lorsque toosome valeur supérieure à 0, iisnode sera paginer de tous ses enfants traite toutes les millisecondes 'idlePageOutTimePeriod'. toounderstand page que des moyens, consultez toothis [documentation](https://msdn.microsoft.com/library/windows/desktop/ms682606.aspx). Ce paramètre est utile pour les applications qui consomment beaucoup de mémoire et souhaitez toopageout mémoire toodisk occasionnellement toofree de mémoire RAM.

> [!WARNING]
> Soyez prudent lors de l’activation hello suivant les paramètres de configuration sur les applications de production. Toonot est recommandé de les activer sur les applications de production en direct.
> 
> 

* debugHeaderEnabled
  
    valeur par défaut de Hello est false. Si défini tootrue, iisnode ajoutera une réponse iisnode-debug tooevery HTTP réponse d’en-tête HTTP qu’il envoie la valeur d’en-tête hello iisnode de débogage est une URL. Nombre d’éléments individuels d’informations de diagnostic permettre être collectées en examinant le fragment d’URL hello, mais une quantité une meilleure visualisation est obtenue en ouvrant hello URL dans le navigateur de hello.
* loggingEnabled
  
    Ce paramètre contrôle la journalisation de hello de stdout et stderr par iisnode. Iisnode sera capturer stdout/stderr à partir de processus de nœud qu'il lance et écrire Active toohello spécifiée dans le paramètre de « Répertoire_journal » hello. Une fois qu’il est activé, votre application doit écrire système de fichiers journaux toohello et selon la quantité de hello de journalisation effectuée par l’application hello, il peut y avoir en matière de performances.
* devErrorsEnabled
  
    La valeur par défaut est false. Lorsque la valeur tootrue, iisnode affiche le code d’état HTTP de hello et code d’erreur Win32 de votre navigateur. code de win32 Hello s’avérera utile dans certains types de problèmes de débogage.
* debuggingEnabled (ne pas activer ce paramètre sur un site de production en direct)
  
    Ce paramètre contrôle la fonctionnalité de débogage. iisnode est intégré à node-inspector. En activant ce paramètre, vous activez le débogage de votre application node. Une fois que ce paramètre est activé, iisnode sera mise en page hello nécessaires de nœud-inspecteur fichiers 'debuggerVirtualDir' répertoire hello premier débogage demande tooyour application node. Vous pouvez charger l’inspecteur de nœud de hello en envoyant une demande toohttp://yoursite/server.js/debug. Vous pouvez contrôler le segment d’URL hello débogage par le paramètre de 'debuggerPathSegment'. Par défaut, debuggerPathSegment=’debug’. Vous pouvez définir cette tooa GUID, par exemple pour qu’il soit plus difficile toobe découvert par d’autres.
  
    Consultez ce [lien](https://tomasz.janczuk.org/2011/11/debug-nodejs-applications-on-windows.html) pour plus d’informations sur le débogage.

## <a name="scenarios-and-recommendationstroubleshooting"></a>Scénarios et recommandations/résolution des pannes
### <a name="my-node-application-is-making-too-many-outbound-calls"></a>Mon application node émet trop d’appels sortants.
De nombreuses applications souhaiteriez toomake les connexions sortantes dans le cadre de leur fonctionnement normal. Par exemple, lorsqu’une demande arrive, votre application de nœud choix toocontact une API REST ailleurs et obtenir une demande d’information tooprocess hello. Vous pouvez toouse un agent de keep alive lors d’appels http ou https. Par exemple, vous pouvez utiliser module d’agentkeepalive hello que votre keep alive de l’agent lors de l’établissement de ces appels sortants. Cela permet de s’assurer que les sockets de hello sont réutilisés sur vos webapp azure VM et la surcharge de hello réduction de la création de nouveaux sockets pour chaque demande sortante. En outre, cela permet de s’assurer que vous utilisez moins de toomake sockets que nombreuses demandes sortantes et par conséquent, vous ne dépassez pas maxSockets hello qui sont alloués par machine virtuelle. Recommandation sur Azure WebApp serait tooset hello agentKeepAlive maxSockets valeur total tooa de 160 sockets par machine virtuelle. Cela signifie que si vous avez 4 node.exe s’exécutant sur hello machine virtuelle, vous souhaiteriez tooset hello agentKeepAlive maxSockets too40 par node.exe qui est de 160 total par machine virtuelle.

Exemple de configuration [d’agentKeepALive](https://www.npmjs.com/package/agentkeepalive) :

```
var keepaliveAgent = new Agent({    
    maxSockets: 40,    
    maxFreeSockets: 10,    
    timeout: 60000,    
    keepAliveTimeout: 300000    
});
```

Cet exemple suppose que 4 node.exe sont en cours d’exécution sur votre machine virtuelle. Si vous avez un nombre différent de node.exe s’exécutant sur hello machine virtuelle, vous aurez maxSockets de hello toomodify définir en conséquence.

### <a name="my-node-application-is-consuming-too-much-cpu"></a>Mon application node consomme trop de ressources processeur.
Azure Webapps vous enverra probablement une recommandation sur votre portail concernant le niveau de consommation processeur considéré comme élevé. Vous pouvez également le programme d’installation analyse toowatch pour certaines [métriques](web-sites-monitor.md). Lors de la vérification de l’utilisation de hello du processeur sur hello [tableau de bord de portail Azure](../application-insights/app-insights-web-monitor-performance.md), vérifiez les valeurs MAX de hello UC afin que vous n’attendez plus les valeurs de crête hello.
Dans les cas où vous pensez que votre application consomme trop de ressources processeur et vous ne pouvez pas expliquer pourquoi, vous devez tooprofile votre application de nœud.

### 
#### <a name="profiling-your-node-application-on-azure-webapps-with-v8-profiler"></a>Profilage de votre application node sur Azure Webapps à l’aide de V8-Profiler
Par exemple, vous permet de dire qu’application hello world que vous souhaitez tooprofile comme indiqué ci-dessous :

```
var http = require('http');    
function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    WriteConsoleLog();    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Accédez tooyour scm site https://yoursite.scm.azurewebsites.net/DebugConsole

Vous accéder à une invite de commandes, comme indiqué ci-dessous. Allez dans votre répertoire site/wwwroot.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_install_v8.png)

Exécuter les commandes hello « npm installer le Générateur de profils v8 »

Le programme v8-profiler et toutes ses dépendances devraient s’installer sous le répertoire node\_modules.
À présent, modifiez votre tooprofile server.js votre application.

```
var http = require('http');    
var profiler = require('v8-profiler');    
var fs = require('fs');

function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    profiler.startProfiling('HandleRequest');    
    WriteConsoleLog();    
    fs.writeFileSync('profile.cpuprofile', JSON.stringify(profiler.stopProfiling('HandleRequest')));    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Hello au-dessus de modifications sera fonction de WriteConsoleLog hello du profil, puis écrivez hello profil sortie too'profile.cpuprofile' fichier sous wwwroot du site. Une application tooyour de demande d’envoi. Vous verrez qu’un fichier « profile.cpuprofile » a été créé sous le répertoire wwwroot de votre site.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_profile.cpuprofile.png)

Télécharger ce fichier, et vous devrez tooopen ce fichier avec les outils F12 de Chrome. Appuyez sur F12 sur chrome, puis cliquez sur hello « Onglet Profils ». Cliquez sur le bouton « Load ». Sélectionnez le fichier profile.cpuprofile que vous venez de télécharger. Cliquez sur le profil hello que vous venez de charger.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/chrome_tools_view.png)

Vous verrez que 95 % des temps de hello a été consommée par WriteConsoleLog fonction comme indiqué ci-dessous. Cela vous indique également les numéros de ligne exacte de hello et les fichiers sources qui provoquent le problème de hello.

### <a name="my-node-application-is-consuming-too-much-memory"></a>Mon application node consomme trop de mémoire.
Azure Webapps vous enverra probablement une recommandation sur votre portail concernant le niveau de consommation de mémoire considéré comme élevé. Vous pouvez également le programme d’installation analyse toowatch pour certaines [métriques](web-sites-monitor.md). Lors de la vérification de l’utilisation de mémoire hello sur hello [tableau de bord de portail Azure](../application-insights/app-insights-web-monitor-performance.md), vérifiez les valeurs MAX hello pour la mémoire afin de ne pas manquer des valeurs de crête hello.

#### <a name="leak-detection-and-heap-diffing-for-nodejs"></a>Détection des fuites et procédure de heap diffing pour node.js
Vous pouvez utiliser [memwatch de nœud](https://github.com/lloyd/node-memwatch) toohelp identifient la mémoire des fuites.
Vous pouvez installer memwatch comme v8 Générateur de profils et de modifier que votre code toocapture et diff tas tooidentify hello fuites de mémoire dans votre application.

### <a name="my-nodeexes-are-getting-killed-randomly"></a>Mes fichiers node.exe sont arrêtés de façon aléatoire
Cette situation peut avoir diverses raisons :

1. Votre application lève des exceptions non interceptées : Veuillez cocher d:\\domestique\\LogFiles\\Application\\fichier errors.txt de journalisation pour plus d’informations hello sur hello une exception. Ce fichier contient la trace de la pile hello pour vous pouvez de résoudre votre application sur cette base.
2. Votre application consomme trop de mémoire, ce qui affecte le démarrage des autres processus. Si de mémoire virtuelle totale hello est too100 fermer %, votre node.exe a supprimées par hello processus manager toolet autres processus obtenir une chance toodo du travail. toofix, si votre application doit réellement toouse beaucoup de mémoire, veuillez l’échelle tooa ou assurez-vous que votre application n’est pas présente une fuite de mémoire virtuelle supérieure avec beaucoup plus de mémoire RAM.

### <a name="my-node-application-does-not-start"></a>Mon application node ne démarre pas
Si votre application renvoie des erreurs 500 au démarrage, plusieurs raisons peuvent expliquer ce phénomène :

1. Node.exe n’est pas présent à l’emplacement correct de hello. Vérifiez le paramètre nodeProcessCommandLine.
2. Fichier de script principal n’est pas présent à l’emplacement correct de hello. Web.config et assurez-vous que nom hello du fichier de script principal hello hello gestionnaires section correspondances hello principal fichier de script.
3. Configuration du fichier Web.config n’est pas correcte : Vérifiez les noms de paramètres hello/valeurs.
4. Démarrage à froid : votre application prend trop de temps toostartup. Si votre application met plus de (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1 000 secondes à démarrer, iisnode renvoie une erreur 500. Augmentez les valeurs de ces toomatch paramètres votre application démarrer iisnode tooprevent de temps à partir de ce délai et retourner hello 500 Erreur hello.

### <a name="my-node-application-crashed"></a>Mon application node a planté
Votre application lève des exceptions non interceptées : Veuillez cocher d:\\domestique\\LogFiles\\Application\\fichier errors.txt de journalisation pour plus d’informations hello sur hello une exception. Ce fichier contient la trace de la pile hello pour vous pouvez de résoudre votre application sur cette base.

### <a name="my-node-application-takes-too-much-time-toostartup-cold-start"></a>Mon application nœud prend trop de toostartup de temps (démarrage à froid)
Raison la plus courante est qu’un grand nombre de fichiers dans le nœud de hello application hello\_modules et hello application tentatives tooload la plupart de ces fichiers lors du démarrage. Par défaut, vos fichiers résidant sur le partage de réseau hello sur les applications Web Azure, le chargement des fichiers autant peut prendre un certain temps.
Certains toomake solutions cela plus rapide sont les suivantes :

1. Assurez-vous de qu'avoir une structure plate dépendance et pas de dépendances en double à l’aide de npm3 tooinstall vos modules.
2. Essayez toolazy charge votre nœud\_modules et tous les modules hello au démarrage de ne charge pas. Cela signifie que toorequire('module') d’appel hello doit être effectuée lorsque vous en avez réellement besoin au sein de la fonction hello vous essayez de module de hello toouse.
3. Azure Webapps offre une fonctionnalité dite de « cache local ». Cette fonctionnalité copie le contenu de votre hello réseau partage toohello disque hello machine virtuelle. Étant donné que les fichiers hello sont locaux, hello temps de chargement de nœud\_modules est beaucoup plus rapide. -Ce [documentation](../app-service/app-service-local-cache.md) explique comment toouse le Cache Local dans plus de détail.

## <a name="iisnode-http-status-and-substatus"></a>État et sous-état http IISNODE
Cela [fichier source](https://github.com/Azure/iisnode/blob/master/src/iisnode/cnodeconstants.h) répertorie tous les hello possibles d’état/sous-état combinaison iisnode peut retourner en cas d’erreur.

Activer FREB pour votre code d’erreur win32 application toosee hello (Vérifiez que vous activez FREB uniquement sur les sites de production non pour des raisons de performances.).

| État HTTP | Sous-état HTTP | Raison possible ? |
| --- | --- | --- |
| 500 |1 000 |Il a été un problème de la distribution hello demande tooIISNODE : Vérifiez si node.exe a été démarré. node.exe peut avoir été bloqué au démarrage. Vérifiez la configuration de votre fichier web.config afin d’identifier d’éventuelles erreurs. |
| 500 |1001 |-Win32Error 0 x 2 – application ne répond pas toohello URL. Réécriture d’URL de vérification des règles ou si votre application expresse définir des itinéraires correct hello. -Win32Error 0x6d – canal nommé est occupé : Node.exe n’accepte pas les requêtes, car le canal de hello est occupé. Vérifiez l’utilisation élevée du processeur. -Autres erreurs : vérifiez si node.exe a planté. |
| 500 |1002 |node.exe a planté : consultez l’arborescence des appels de procédure sous d:\\home\\LogFiles\\logging-errors.txt. |
| 500 |1003 |Configuration du canal problème : vous ne devez jamais voir cela, mais si vous le faites, hello nommé configuration du pipeline est incorrect. |
| 500 |1004-1018 |Une erreur s’est produite lors de l’envoi hello demande ou traitement de réponse hello à partir de node.exe. Vérifiez si node.exe a planté. Consultez l’arborescence des appels de procédure sous d:\\home\\LogFiles\\logging-errors.txt. |
| 503 |1 000 |N’est pas suffisant tooallocate mémoire plus les connexions de canaux nommés. Vérifiez pourquoi votre application consomme une grande quantité de mémoire. Vérifiez la valeur du paramètre maxConcurrentRequestsPerProcess. Si son n’est pas infinie et que vous avez un grand nombre de requêtes, augmenter cette valeur tooprevent cette erreur. |
| 503 |1001 |Demande n’a pas pu être distribué toonode.exe parce que le recyclage de l’application hello. Après que l’application hello a été recyclé, la demande doit être traitée normalement. |
| 503 |1002 |Code d’erreur win32 à cocher pour connaître la raison – demande n’a pas pu être distribué tooa node.exe. |
| 503 |1003 |Le canal nommé est trop occupé : vérifiez si nœud consomme beaucoup de ressources processeur |

NODE.exe contient un paramètre appelé NODE\_PENDING\_PIPE\_INSTANCES. Par défaut, cette valeur est définie sur 4 en dehors d’Azure Webapps. Cela signifie que node.exe peut uniquement accepter des demandes de 4 à la fois sur le canal nommé de hello. Sur les applications Web Azure, cette valeur est définie à too5000 et cette valeur doit être suffisante pour la plupart des applications de nœud en cours d’exécution sur les applications Web azure. Vous devez voir pas sur les applications Web azure 503.1003 parce que nous avons une valeur élevée pour hello nœud\_en attente\_canal\_INSTANCES.  |

## <a name="more-resources"></a>Autres ressources
Suivez ces liens de toolearn plus d’informations sur les applications node.js dans Azure App Service.

* [Prise en main des applications web Node.js dans Azure App Service](app-service-web-get-started-nodejs.md)
* [Comment toodebug un Node.js web application dans Azure App Service](web-sites-nodejs-debug.md)
* [Utilisation de modules Node.js avec des applications Azure](../nodejs-use-node-modules-azure-apps.md)
* [Azure App Service Web Apps : Node.js](https://blogs.msdn.microsoft.com/silverlining/2012/06/14/windows-azure-websites-node-js/)
* [Centre pour développeurs Node.js](../nodejs-use-node-modules-azure-apps.md)
* [Exploration hello Console de débogage Super Secret Kudu](https://azure.microsoft.com/documentation/videos/super-secret-kudu-debug-console-for-azure-web-sites/)

