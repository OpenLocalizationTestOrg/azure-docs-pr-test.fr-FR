---
title: aaaHow toodebug application web Node.js dans Azure App Service
description: "Découvrez comment toodebug un Node.js web application dans Azure App Service."
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a>Comment toodebug un Node.js web application dans Azure App Service
Azure fournit tooassist diagnostics intégrés avec le débogage des applications Node.js hébergées dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) les applications Web. Dans cet article, vous allez apprendre comment journalisation tooenable de stdout et stderr, afficher les informations d’erreur dans le navigateur de hello et comment toodownload et affichage des fichiers journaux.

Le diagnostic des applications Node.js hébergées sur Azure est fourni par [IISNode]. Alors que cet article décrit les paramètres les plus courants hello pour la collecte des informations de diagnostic, il ne fournit pas une référence complète pour l’utilisation des IISNode. Pour plus d’informations sur l’utilisation de IISNode, consultez hello [IISNode Readme] sur GitHub.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Activation de la journalisation
Par défaut, une application web App Service ne capture que les informations de diagnostic sur les déploiements, comme lorsque vous déployez une application Web à l’aide de Git. Cette information est utile si vous rencontrez un problème lors du déploiement, comme un échec lors de l'installation d'un module référencé dans **package.json**ou si vous utilisez un script de déploiement personnalisé.

tooenable hello journalisation de flux stdout et stderr, vous devez créer un **IISNode.yml** de fichiers à votre application Node.js racine hello et ajoutez hello qui suit :

    loggingEnabled: true

Cela permet la journalisation de stderr et stdout à partir de votre application Node.js hello.

Hello **IISNode.yml** fichier peut également être utilisé toocontrol si simplifié des erreurs ou des erreurs des développeurs sont renvoyées toohello navigateur lorsqu’une erreur se produit. erreurs des développeurs tooenable, ajouter hello suivant ligne toohello **IISNode.yml** fichier :

    devErrorsEnabled: true

Une fois cette option est activée, IISNode renvoie hello dernière 64 Ko, des informations envoyées toostderr au lieu d’une erreur conviviale tel que « une erreur interne s’est produite ».

> [!NOTE]
> DevErrorsEnabled est utile lors du diagnostic de problèmes au cours du développement, son activation dans un environnement de production peut entraîner des erreurs de développement envoyés tooend utilisateurs.
> 
> 

Si hello **IISNode.yml** fichier n’existe pas déjà dans votre application, vous devez redémarrer votre application web après la publication d’application hello mis à jour. Si vous modifiez simplement les paramètres dans un fichier **IISNode.yml** existant qui a été publié précédemment, aucun redémarrage n'est nécessaire.

> [!NOTE]
> Si votre application web a été créée à l’aide des outils de ligne de commande Azure hello ou des applets de commande PowerShell de Azure, une valeur par défaut **IISNode.yml** fichier est créé automatiquement.
> 
> 

toorestart hello web application, une application web de hello sélectionnez Bonjour [Azure Portal](https://portal.azure.com), puis cliquez sur **redémarrer** bouton :

![bouton redémarrer][restart-button]

Si les outils de ligne de commande Azure hello sont installés dans votre environnement de développement, vous pouvez utiliser hello suivant commande toorestart hello web app :

    azure site restart [sitename]

> [!NOTE]
> LoggingEnabled et devErrorsEnabled sont des options de configuration IISNode.yml hello couramment utilisé pour capturer des informations de diagnostic, IISNode.yml peut être utilisé tooconfigure diverses options pour votre environnement d’hébergement. Pour obtenir une liste complète des options de configuration hello, consultez hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) fichier.
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a>Accès aux journaux
Journaux de diagnostic sont accessibles de trois manières ; À l’aide de hello Transfer protocole FTP (File), télécharger une archive Zip, ou comme une mise à jour de flux de données du journal de hello (également appelé une fin). Téléchargement de l’archive Zip des fichiers journaux de hello hello ou la consultation des flux live de hello nécessitent outils de ligne de commande Azure hello. Elles peuvent être installées à l’aide de hello de commande suivante :

    npm install azure-cli -g

Une fois installé, les outils hello est accessible à l’aide de la commande hello 'azure'. outils de ligne de commande de Hello doit d’abord être configuré toouse votre abonnement Azure. Pour plus d’informations sur comment tooaccomplish cette tâche, consultez hello **comment toodownload et importation de paramètres de publication** section Hello [comment tooUse hello de ligne de commande de Windows Azure Tools](../xplat-cli-connect.md) l’article.

### <a name="ftp"></a>FTP
informations de diagnostic hello tooaccess via FTP, visitez hello [Azure Portal](https://portal.azure.com), sélectionnez votre application web, puis hello **tableau de bord**. Bonjour **liens rapides** section hello **journaux de DIAGNOSTIC FTP** et **journaux de DIAGNOSTIC FTPS** liens fournissent des journaux de toohello d’accès à l’aide du protocole de hello FTP.

> [!NOTE]
> Si vous n’avez pas précédemment configuré nom d’utilisateur et mot de passe pour le déploiement ou FTP, vous pouvez le faire à partir de hello **Quickstart** page de gestion en sélectionnant **configurer les informations d’identification de déploiement**.
> 
> 

Hello URL FTP retournées dans le tableau de bord hello concerne hello **LogFiles** répertoire qui contiendra hello suivant sous-répertoires :

* [Méthode de déploiement](web-sites-deploy.md) -si vous utilisez une méthode de déploiement tels que Git, un répertoire de même nom est créé et qu’il contienne des informations de hello liées toodeployments.
* nodejs : les informations stdout et stderr capturées à partir de toutes les instances de votre application (lorsque loggingEnabled est défini sur true).

### <a name="zip-archive"></a>Archive ZIP
toodownload une archive Zip des journaux de diagnostic hello, de hello utilisez commande suivante à partir des outils de ligne de commande Azure hello :

    azure site log download [sitename]

Cette commande télécharge un **diagnostics.zip** hello répertoire en cours. Cette archive contient hello suivant la structure de répertoires :

* deployments : un journal des informations concernant les déploiements de votre application
* LogFiles
  
  * [Méthode de déploiement](web-sites-deploy.md) -si vous utilisez une méthode de déploiement tels que Git, un répertoire de même nom est créé et qu’il contienne des informations de hello liées toodeployments.
  * nodejs : les informations stdout et stderr capturées à partir de toutes les instances de votre application (lorsque loggingEnabled est défini sur true).

### <a name="live-stream-tail"></a>Flux live (tail)
tooview un flux en direct des informations du journal de diagnostic, hello utilisez commande suivante à partir des outils de ligne de commande Azure hello :

    azure site log tail [sitename]

Cette méthode retourne un flux de données de journaux d’événements sont mis à jour lorsqu’elles se produisent sur le serveur de hello. Ce flux renvoie les informations de déploiement ainsi que les informations relatives à stdout et stderr (lorsque loggingEnabled est défini sur true).

<a id="nextsteps"></a>

## <a name="next-steps"></a>Étapes suivantes
Dans cet article vous avez appris comment tooenable et accès aux informations de diagnostic pour Azure. Alors que ces informations sont utiles dans les problèmes de présentation qui se produisent avec votre application, il peut pointer problème tooa avec un module que vous utilisez ou que la version de Node.js utilisé par l’application de Service Web Apps hello est différente de celle hello celui utilisé dans votre déploiement environnement.

Pour plus d'informations sur l'utilisation des modules sur Azure, consultez la page [Utilisation des modules Node.js avec les applications Azure](../nodejs-use-node-modules-azure-apps.md).

Pour plus d'informations sur la spécification d'une version Node.js de votre application, consultez la page [Spécification d'une version de Node.js dans une application Azure].

Pour plus d’informations, consultez également hello [centre de développement Node.js](/develop/nodejs/).

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[Spécification d'une version de Node.js dans une application Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

