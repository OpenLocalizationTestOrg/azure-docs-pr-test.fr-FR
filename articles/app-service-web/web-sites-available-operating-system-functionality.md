---
title: "fonctionnalités du système aaaOperating sur Azure App Service"
description: "En savoir plus sur les applications API sur Azure App Service hello du système d’exploitation des fonctionnalités disponibles tooweb applications et les serveurs principaux de l’application mobile"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 39d5514f-0139-453a-b52e-4a1c06d8d914
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 695188c48102b10ece326fba8d50a5f55b03b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="operating-system-functionality-on-azure-app-service"></a>Fonctionnalités de système d’exploitation sur Azure App Service
Cet article décrit hello de ligne de base système d’exploitation des fonctionnalités communes qui sont disponible tooall les applications en cours d’exécution [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Ces fonctionnalités englobent notamment l'accès aux fichiers, l'accès réseau et l'accès au registre, ainsi que les journaux et événements de diagnostic. 

<a id="tiers"></a>

## <a name="app-service-plan-tiers"></a>Niveaux des plans App Service
App Service exécute les applications des clients dans un environnement d’hébergement mutualisé. Applications déployées dans hello **libre** et **Shared** niveaux de s’exécuter dans le processus de travail sur des ordinateurs virtuels partagés lors des applications déployées dans hello **Standard** et  **Premium** niveaux s’exécutent sur l’ou les ordinateurs virtuels dédiés spécifiquement pour les applications de hello associées à un seul client.

Étant donné que le Service d’applications prend en charge une expérience transparente entre les différents niveaux de mise à l’échelle, la configuration de sécurité hello appliquée pour hello de reste les applications de Service d’applications même. Cela garantit que les applications ne soudainement se comportent différemment, tombe en panne de façon inattendue, lorsque le plan de Service d’application bascule d’une couche tooanother.

<a id="developmentframeworks"></a>

## <a name="development-frameworks"></a>Infrastructures de développement
Tarification niveaux contrôle hello quantité des ressources de calcul (processeur, le stockage sur disque, mémoire et sortie de réseau) du Service d’applications tooapps disponibles. Toutefois, étendue hello tooapps disponible de la fonctionnalité de framework reste hello qu'identique, indépendamment de hello niveaux de mise à l’échelle.

App Service prend en charge différentes infrastructures de développement, telles qu’ASP.NET, ASP classique, node.js, PHP et Python (toutes exécutées en tant qu’extensions sous IIS). Dans l’ordre toosimplify et normaliser la configuration de la sécurité, les applications de Service d’applications s’exécutent généralement hello différentes infrastructures de développement avec leurs paramètres par défaut. Une approche tooconfiguring applications aurait pu la surface d’exposition de toocustomize hello API et des fonctionnalités pour chaque infrastructure de développement individuels. L’approche retenue pour App Service est plus générale puisqu’elle offre une base commune de fonctionnalités de système d’exploitation, quelle que soit l’infrastructure de développement d’une application.

Hello sections suivantes résument les types généraux de hello des applications de Service de système d’exploitation fonctionnalité tooApp disponibles.

<a id="FileAccess"></a>

## <a name="file-access"></a>Accès aux fichiers
Différents lecteurs sont disponibles dans App Service, notamment les lecteurs locaux et les lecteurs réseau.

<a id="LocalDrives"></a>

### <a name="local-drives"></a>Lecteurs locaux
Fondamentalement, du Service d’applications est un service qui s’exécute sur l’infrastructure de hello Azure PaaS (plateforme en tant que service). Un résultat, les lecteurs locaux hello qui sont « associé » tooa virtual machine hello même rôle de travail disponible tooany types lecteur exécutent dans Azure. Cela inclut un lecteur de système d’exploitation (hello lecteur D:\), un lecteur de l’application qui contient des fichiers cspkg Package Azure utilisés exclusivement par le Service d’applications (et toocustomers inaccessible) et un lecteur de le « utilisateur » (hello lecteur C:\), dont la taille varie selon la taille de hello Hello machine virtuelle.

<a id="NetworkDrives"></a>

### <a name="network-drives-aka-unc-shares"></a>Lecteurs réseau (partages UNC)
Un des aspects d’unique hello du Service d’application qui simplifie la maintenance et le déploiement d’applications est que tous les contenus de l’utilisateur sont stocké sur un ensemble de partages UNC. Ce modèle mappe très bien toohello le modèle commun de stockage de contenu utilisé par web local qui héberge les environnements qui disposent de plusieurs serveurs à charge équilibrée. 

App Service intègre un certain nombre de partages UNC créés dans chaque centre de données. Pourcentage du contenu de l’utilisateur hello pour tous les clients dans chaque centre de données est alloué tooeach un partage UNC. En outre, tout contenu de fichier hello pour l’abonnement d’un client unique est toujours placé sur hello partage UNC même. 

Notez que, en raison de services de cloud computing toohow fonctionne, changer au fil du temps d’ordinateur virtuel hello spécifique chargé d’héberger un partage UNC. Il est garanti que les partages UNC seront montés par différentes machines virtuelles, comme ils sont mis en haut et bas pendant hello cloud opérations normales. Pour cette raison, les applications doivent jamais des hypothèses codé en dur que les informations de l’ordinateur dans un chemin d’accès de fichier UNC hello resteront stables au fil du temps. Au lieu de cela, ils doivent utiliser hello pratique *faux* chemin d’accès absolu **D:\home\site** qui fournit des services d’application. Ce chemin d’accès absolu faux fournit une méthode de portable, indépendant d’application et d’utilisateur pour les applications de tooone de référence. À l’aide de **D:\home\site**, un peut transférer des fichiers partagés à partir de l’application tooapp sans avoir à tooconfigure un nouveau chemin d’accès absolu pour chaque transfert.

<a id="TypesOfFileAccess"></a>

### <a name="types-of-file-access-granted-tooan-app"></a>Types d’accès au fichier accordées tooan application
L’abonnement de chaque client comporte une structure de répertoires réservée sur un partage UNC spécifique dans un centre de données. Un client peut avoir plusieurs applications créées au sein d’un centre de données spécifique, de sorte que tous les répertoires hello appartenant abonnement du client unique tooa sont créés sur hello même partage UNC. partage de Hello peut-être inclure des répertoires, tels que ceux de contenu, erreur et les journaux de diagnostic et les versions antérieures de l’application hello créé par le contrôle de code source. Comme prévu, les répertoires d’application d’un client sont disponibles pour l’accès en lecture et écriture à l’exécution par le code de l’application de l’application hello.

Sur hello lecteurs locaux attaché toohello virtual machine qui exécute une application, un bloc d’espace sur le lecteur C:\ pour le stockage local temporaire spécifique à l’application de hello réserves de ressources de Service d’applications. Bien qu’une application a accès en lecture/écriture intégral tooits propre temporaire local, le stockage qui n’est pas vraiment toobe prévue utilisée directement par le code de l’application hello. Au lieu de cela, hello vise tooprovide stockage des fichiers temporaires pour les infrastructures d’applications IIS et web. Service d’applications limite également la quantité de hello de stockage local temporaire disponible tooeach application tooprevent différentes applications de consommer une quantité excessive de stockage de fichier local.

Hello le répertoire des fichiers ASP.NET temporaires sont de deux exemples d’application Service l'utilisation du stockage local temporaire et répertoire hello pour IIS dans des fichiers compressés. Hello système de compilation ASP.NET utilise le répertoire de « Fichiers ASP.NET temporaires » hello comme emplacement de cache de compilation temporaire. IIS utilise réponse de sortie toostore compressé hello « IIS fichiers compressés temporaires ». Ces deux types de fichiers d’utilisation (ainsi que d’autres utilisateurs) sont remappés dans le stockage local temporaire tooper l’application de Service d’applications. Ce nouveau mappage préserve les fonctionnalités.

Chaque application de Service de l’application s’exécute comme une identité de processus de travail de faibles unique aléatoire appelée hello « application pool identity », décrit plus loin ici : [http://www.iis.net/learn/manage/configuring-security/application-pool-identities ](http://www.iis.net/learn/manage/configuring-security/application-pool-identities). Code de l’application utilise cette identité pour le lecteur de système d’exploitation toohello accès en lecture seule de base (hello lecteur D:\). Le code d'application peut ainsi dresser la liste les structures de répertoires communes et lire les fichiers communs sur le lecteur du système d'exploitation. Bien que cela peut apparaître toobe un niveau assez large d’accès, hello les mêmes répertoires et fichiers sont accessibles lorsque vous déployez un rôle de travail dans Azure service hébergé et lire le contenu du lecteur hello. 

<a name="multipleinstances"></a>

### <a name="file-access-across-multiple-instances"></a>Accès aux fichiers sur plusieurs instances
répertoire de base Hello contienne le contenu d’une application, et tooit peut écrire du code de l’application. Si une application s’exécute sur plusieurs instances, répertoire hello est partagé entre toutes les instances afin que toutes les instances voir hello même répertoire. Par conséquent, par exemple, si une application enregistre le répertoire toohello les fichiers téléchargés, ces fichiers sont des instances de tooall immédiatement disponible. 

<a id="NetworkAccess"></a>

## <a name="network-access"></a>Accès réseau
Code de l’application peut utiliser TCP/IP et toomake de protocoles basé sur UDP sortant réseau connexions tooInternet accessible points de terminaison qui exposent des services externes. Les applications peuvent utiliser ces mêmes tooservices tooconnect de protocoles dans Azure &#151; par exemple, en établissant des tooSQL des connexions HTTPS de base de données.

Il existe également une fonctionnalité limitée pour les applications tooestablish un bouclage local connexion et disposez d’une application écoute sur ce socket de bouclage locale. Cette fonctionnalité existe tooenable principalement les applications qui écoutent sur les sockets de bouclage locale dans le cadre de leurs fonctionnalités. Notez que chaque application voit une connexion de bouclage « private ». l’application « A » ne peut pas écouter le socket de bouclage local tooa établie par l’application « B ».

Les canaux nommés sont également pris en charge en tant que mécanisme de communication inter-processus (IPC) entre différents processus qui exécutent collectivement une application. Par exemple, module de IIS FastCGI hello repose sur les canaux nommés toocoordinate hello des processus individuels qui s’exécutent pages PHP.

<a id="Code"></a>

## <a name="code-execution-processes-and-memory"></a>Exécution de code, processus et mémoire
Comme mentionné précédemment, les applications sont exécutées dans des processus de travail à faibles privilèges qui utilisent une identité de pool d’applications aléatoire. Code de l’application a un espace de mémoire toohello accès associé aux processus de travail hello, ainsi que tous les processus enfants qui peuvent être générées par le processus CGI ou d’autres applications. Toutefois, une application ne peut pas accéder à la mémoire de hello ou les données d’une autre application même s’il est sur hello même machine virtuelle.

Les applications peuvent exécuter des scripts ou des pages créés avec des infrastructures de développement Web prises en charge. Service d’applications ne configurer des modes de toomore limité de paramètres web framework. Par exemple, les applications ASP.NET s’exécutant sur le Service d’applications exécutent en mode de confiance « complet » comme mode de confiance tooa exécutée plus restreinte. Les infrastructures Web, y compris les classic ASP et ASP.NET, peuvent appeler des composants COM dans le processus (mais pas la sortie des composants COM de processus) comme ADO (ActiveX Data Objects) qui sont inscrits par défaut sur le système d’exploitation de Windows hello.

Les applications peuvent générer et exécuter un code arbitraire. Il n’est autorisée pour un choses de toodo application générer une interface de commande ou exécuter un script PowerShell. Toutefois, même si les processus et du code arbitraire peuvent être générés à partir d’une application, programmes exécutables et les scripts sont alors restreintes toohello privilèges accordés toohello parent pool d’applications. Par exemple, d’une application peut créer un fichier exécutable qui effectue un appel HTTP sortant, mais que le même fichier exécutable ne peut pas essayer d’adresse toounbind hello d’un ordinateur virtuel à partir de sa carte réseau. Appel réseau sortant est autorisée code à privilèges toolow, mais essayez tooreconfigure des paramètres de réseau sur un ordinateur virtuel nécessite des privilèges d’administrateur.

<a id="Diagnostics"></a>

## <a name="diagnostics-logs-and-events"></a>Journaux et événements de diagnostic
Informations du journal sont un autre jeu de données que certaines applications tenter tooaccess. Hello toocode disponible de journal d’informations en cours d’exécution dans le Service d’applications inclut un diagnostic et de consigner les informations générées par une application qui est également aisément accessible toohello application. 

Par exemple, les journaux W3C HTTP générés par une application active sont disponibles sur un répertoire de journal dans le réseau de hello emplacement du partage créé pour l’application hello ou disponibles dans le stockage blob si un client a configuré la journalisation W3C toostorage. Cette dernière option de Hello permet de grandes quantités de toobe journaux collecté sans risque hello de dépassement des limites de stockage de fichier hello associés à un partage réseau.

De la même manière, les diagnostics en temps réel des informations à partir d’applications .NET peuvent également être enregistrées à l’aide de hello .NET suivi infrastructure et de diagnostics avec les options toowrite hello partage réseau l’application hello trace informations tooeither ou vous pouvez également tooa stockage d’objets blob emplacement.

Zones de diagnostics journalisation et de suivi qui ne sont pas tooapps disponibles sont les événements ETW de Windows et les journaux des événements Windows courants (par exemple, système, Application et sécurité journaux des événements). Étant donné que les informations de suivi ETW peuvent être visibles, événements de l’échelle de l’ordinateur (avec droite hello ACL), accès en lecture et écriture du tooETW sont bloquées. Les développeurs peuvent remarquer cette API appelle tooread et écriture des événements ETW et journaux des événements Windows courantes apparaissent toowork, mais c’est parce que le Service d’applications est « émulant « hello appels afin qu’ils semblent toosucceed. En réalité, le code de l’application hello n’a aucune donnée d’événement toothis accès.

<a id="RegistryAccess"></a>

## <a name="registry-access"></a>Accès au registre
Les applications ont accès en lecture seule toomuch (mais pas toutes) du Registre hello de machine virtuelle de hello s’exécutent sur. Dans la pratique, cela signifie que les clés de Registre qui permettent l’accès en lecture seule toohello groupe local des utilisateurs sont accessibles par les applications. Une zone du Registre hello qui n’est actuellement pas pris en charge pour l’accès en lecture ou écriture est hello HKEY\_actuel\_ruche de l’utilisateur.

Registre de toohello d’accès en écriture est bloqué, y compris les clés de Registre d’accès tooany par l’utilisateur. Du point de vue de l’application hello, accès en écriture toohello Registre doit jamais se reposer Bonjour environnement Azure dans la mesure où les applications peuvent (et font) migrées entre les différentes machines virtuelles. Hello uniquement accessible en écriture le stockage persistant qui peut créer de dépendances par une application est la structure de répertoire de contenu par application hello stocké sur hello Qu'app Service UNC partage. 

## <a name="more-information"></a>Plus d’informations

[Bac à sable de l’application Web Azure](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox) -hello la plupart des informations à jour sur l’environnement d’exécution hello du Service d’application. Cette page est gérée directement par hello équipe de développement du Service d’applications.

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 


