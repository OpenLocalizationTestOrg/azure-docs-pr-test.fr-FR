---
title: "Débogage d’une application web Node.js dans Azure Web Service"
description: "Apprenez à déboguer une application web Node.js dans Azure Web Service."
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
ms.openlocfilehash: 5e302a4c58a171d40e43a22c34c724e868019ec8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-debug-a-nodejs-web-app-in-azure-app-service"></a>Débogage d’une application web Node.js dans Azure Web Service
Azure fournit un outil de diagnostic intégré qui vous aide à déboguer les applications Node.js hébergées dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps. Cet article vous explique comment activer la journalisation de stdout et de stderr, comment afficher les informations sur l'erreur dans le navigateur et comment télécharger et afficher les fichiers journaux.

Le diagnostic des applications Node.js hébergées sur Azure est fourni par [IISNode]. Bien que les paramètres les plus courants pour la collecte des informations de diagnostic soient abordés, cet article ne fournit pas une référence complète sur l'utilisation de IISNode. Pour plus d'informations sur l'utilisation de IISNode, consultez le [fichier Lisez-moi IISNode] sur GitHub.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Activation de la journalisation
Par défaut, une application web App Service ne capture que les informations de diagnostic sur les déploiements, comme lorsque vous déployez une application Web à l’aide de Git. Cette information est utile si vous rencontrez un problème lors du déploiement, comme un échec lors de l'installation d'un module référencé dans **package.json**ou si vous utilisez un script de déploiement personnalisé.

Pour activer la journalisation des flux stdout et stderr, vous devez créer un fichier **IISNode.yml** à la racine de votre application Node.js et ajouter ce qui suit :

    loggingEnabled: true

Cela active la journalisation de stderr et stdout à partir de votre application Node.js.

Le fichier **IISNode.yml** peut également être utilisé pour contrôler si les erreurs conviviales ou les erreurs de développement sont renvoyées au navigateur lorsqu'un échec se produit. Pour activer les erreurs de développement, ajoutez la ligne suivante au fichier **IISNode.yml** :

    devErrorsEnabled: true

Une fois cette option activée, IISNode renvoie les derniers 64 Ko d'informations envoyées à stderr plutôt qu'une erreur conviviale comme « une erreur de serveur interne s'est produite ».

> [!NOTE]
> Bien que devErrorsEnabled soit utile pour diagnostiquer les problèmes lors du développement, l'activer dans un environnement de production peut entraîner l'envoi d'erreurs de développement aux utilisateurs finaux.
> 
> 

Si le fichier **IISNode.yml** n’existe pas dans votre application, vous devez redémarrer votre application Web après la publication de l’application mise à jour. Si vous modifiez simplement les paramètres dans un fichier **IISNode.yml** existant qui a été publié précédemment, aucun redémarrage n'est nécessaire.

> [!NOTE]
> Si votre application Web a été créée à l’aide des outils de ligne en commande Azure ou des applets de commande Azure PowerShell, un fichier **IISNode.yml** par défaut est automatiquement créé.
> 
> 

Pour redémarrer l’application web, sélectionnez-la dans le [portail Azure](https://portal.azure.com), puis cliquez sur le bouton **REDÉMARRER** :

![bouton redémarrer][restart-button]

Si les outils en ligne de commande Azure sont installés dans votre environnement de développement, vous pouvez utiliser la commande suivante pour redémarrer l’application web :

    azure site restart [sitename]

> [!NOTE]
> Bien que loggingEnabled et devErrorsEnabled soient les options de configuration IISNode.yml les plus fréquemment utilisées pour la capture des informations de diagnostic, IISNode.yml peut être utilisé pour configurer diverses options pour votre environnement d'hébergement. Pour une liste complète des options de configuration, consultez le fichier [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml).
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a>Accès aux journaux
Il existe trois manières d'accéder aux journaux de diagnostic : à l'aide du protocole FTP, en téléchargeant une archive ZIP ou via un flux live mis à jour du journal (également appelé « tail »). Le téléchargement de l'archive ZIP des fichiers journaux ou l'affichage du flux live requièrent les outils en ligne de commande Azure, que vous pouvez installer à l'aide de la commande suivante :

    npm install azure-cli -g

Une fois installés, ils sont accessibles à l'aide de la commande « azure ». Les outils en ligne de commande doivent d’abord être configurés pour utiliser votre abonnement Azure. Pour plus d'informations sur la réalisation de cette tâche, consultez la section **Téléchargement et importation des paramètres de publication** de l'article [Utilisation des outils en ligne de commande Azure](../xplat-cli-connect.md) .

### <a name="ftp"></a>FTP
Pour accéder aux informations de diagnostic via FTP, visitez le [portail Azure](https://portal.azure.com), sélectionnez votre application web, puis sélectionnez le **TABLEAU DE BORD**. Dans la section **liens rapides**, les liens **Journaux de diagnostic FTP** et **Journaux de diagnostic FTPS** permettent d’accéder aux journaux à l’aide du protocole FTP.

> [!NOTE]
> Si vous n’avez pas encore configuré un nom d’utilisateur et un mot de passe pour le FTP ou le déploiement, vous pouvez le faire sur la page de gestion **Démarrage rapide**, en sélectionnant **Configurer les informations d’identification du déploiement**.
> 
> 

L'URL FTP renvoyée dans le tableau de bord concerne le répertoire **LogFiles** , qui contient les sous-répertoires suivants :

* [Méthode de déploiement](web-sites-deploy.md) : si vous utilisez une méthode de déploiement comme Git, un répertoire de même nom est créé et contient les informations relatives aux déploiements.
* nodejs : les informations stdout et stderr capturées à partir de toutes les instances de votre application (lorsque loggingEnabled est défini sur true).

### <a name="zip-archive"></a>Archive ZIP
Pour télécharger une archive ZIP des journaux de diagnostic, utilisez la commande suivante à partir des outils en ligne de commande Azure :

    azure site log download [sitename]

Cela télécharge un fichier **diagnostics.zip** dans le répertoire actuel. Cette archive contient la structure de répertoires suivante :

* deployments : un journal des informations concernant les déploiements de votre application
* LogFiles
  
  * [Méthode de déploiement](web-sites-deploy.md) : si vous utilisez une méthode de déploiement comme Git, un répertoire de même nom est créé et contient les informations relatives aux déploiements.
  * nodejs : les informations stdout et stderr capturées à partir de toutes les instances de votre application (lorsque loggingEnabled est défini sur true).

### <a name="live-stream-tail"></a>Flux live (tail)
Pour afficher un flux live des informations du journal de diagnostic, utilisez la commande suivante à partir des outils en ligne de commande Azure :

    azure site log tail [sitename]

Cela renvoie un flux d'événements de journal qui sont mis à jour lorsqu'ils se produisent sur le serveur. Ce flux renvoie les informations de déploiement ainsi que les informations relatives à stdout et stderr (lorsque loggingEnabled est défini sur true).

<a id="nextsteps"></a>

## <a name="next-steps"></a>Étapes suivantes
Cet article vous a montré comment activer les informations de diagnostic pour Azure et comment y accéder. Bien que ces informations soient utiles pour comprendre les problèmes qui surviennent avec votre application, elles peuvent signaler un problème avec un module que vous utilisez ou la version de Node.js utilisée par App Services Web Apps qui est différente de celle utilisée dans votre environnement de déploiement.

Pour plus d'informations sur l'utilisation des modules sur Azure, consultez la page [Utilisation des modules Node.js avec les applications Azure](../nodejs-use-node-modules-azure-apps.md).

Pour plus d'informations sur la spécification d'une version Node.js de votre application, consultez la page [Spécification d'une version de Node.js dans une application Azure].

Pour plus d'informations, consultez aussi le [Centre pour développeurs Node.js](/develop/nodejs/).

## <a name="whats-changed"></a>Changements apportés
* Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[fichier Lisez-moi IISNode]: https://github.com/tjanczuk/iisnode#readme
[How to Use The Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[Spécification d'une version de Node.js dans une application Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

