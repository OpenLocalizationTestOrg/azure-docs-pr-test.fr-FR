---
title: aaaWorking avec Modules Node.js
description: "Découvrez comment toowork avec modules Node.js lors de l’utilisation du Service d’applications Azure ou les Services de cloud computing."
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c0e6cd3d-932d-433e-b72d-e513e23b4eb6
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 926358b7eb80a659dbc1015686b06a30d8c9b8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-nodejs-modules-with-azure-applications"></a>Utilisation de modules Node.js avec des applications Azure
Ce document fournit des instructions sur l'utilisation de modules Node.js avec des applications hébergées sur Azure. Il vous explique comment vous assurer que votre application utilise une version spécifique d'un module et vous présente l'utilisation de modules natifs avec Azure.

Si vous êtes déjà familiarisé avec l’utilisation de modules Node.js, **package.json** et **shrinkwrap.json de npm** fichiers, hello informations suivantes fournit un résumé de ce qui est décrite dans cet article :

* Azure App Service comprend les fichiers **package.json** et **npm-shrinkwrap.json** et peut installer des modules basés sur les entrées de ces fichiers.

* Les Services de cloud computing Azure attendre tous les modules toobe installé sur l’environnement de développement hello et hello **nœud\_modules** toobe répertoire inclus dans le cadre du package de déploiement hello. Elle est prise en charge tooenable possibles pour l’installation des modules à l’aide **package.json** ou **shrinkwrap.json de npm** fichiers sur les Services de Cloud ; Toutefois, cette configuration nécessite une personnalisation de valeur par défaut de hello scripts utilisés par les projets de Service Cloud. Pour obtenir un exemple de procédure tooconfigure cet environnement, consultez [Azure démarrage tâche toorun npm installer tooavoid déploiement des modules de nœud](https://github.com/woloski/nodeonazure-blog/blob/master/articles/startup-task-to-run-npm-in-azure.markdown)

> [!NOTE]
> Machines virtuelles ne sont pas abordés dans cet article, comme l’expérience de déploiement hello dans une machine virtuelle dépend du système d’exploitation de hello hébergé par hello Machine virtuelle.
> 
> 

## <a name="nodejs-modules"></a>Modules Node.js
Les modules sont des packages JavaScript chargeables qui fournissent une fonctionnalité spécifique à votre application. Les modules sont généralement installés à l’aide de hello **npm** de ligne de commande d’outils, toutefois, certains modules (par exemple, le module http du hello) sont fournies en tant que partie du package de Node.js hello core.

Lorsque les modules sont installés, ils sont stockés dans hello **nœud\_modules** répertoire au niveau racine hello de votre structure de répertoire d’application. Chaque module dans hello **nœud\_modules** répertoire maintient son propre **nœud\_modules** répertoire qui contient tous les modules qu’il dépend, et ce comportement se répète. pour chaque module tous les moyen hello la chaîne de dépendance hello. Cet environnement permet à chaque toohave module installé ses propres exigences de version pour les modules de hello qu'il dépend, toutefois cela peut entraîner une structure de répertoires volumineux.

Déploiement hello **nœud\_modules** répertoire comme partie de votre application augmente la taille de hello du déploiement hello lors de la comparaison de toousing un **package.json** ou  **npm-shrinkwrap.json** fichier ; Toutefois, il ne garantit que les versions hello de modules hello utilisés en production sont même hello sous forme de modules hello utilisés dans le développement.

### <a name="native-modules"></a>Modules natifs
Alors que la plupart des modules sont simplement des fichiers JavaScript en texte brut, certains modules sont des images binaires propres à des plateformes. Ces modules sont compilés au moment de l'installation, en général à l'aide de Python et node-gyp. Étant donné que les Services de cloud computing Azure reposent sur hello **nœud\_modules** dossier dans le cadre de l’application hello, n’importe quel module natif inclus comme partie des modules de hello installé doit fonctionner dans un service cloud tant qu’il était en cours de déploiement installé et compilé sur un système de développement Windows.

Azure App Service ne prend pas en charge tous les modules natifs et risque de ne pas pouvoir les compiler si des prérequis spécifiques sont requis. Alors que certains modules populaires tels que MongoDB ont des dépendances natives facultatives et fonctionnent correctement sans celles-ci, deux solutions se sont avérées opérationnelles avec presque tous les modules natifs disponibles à ce jour :

* Exécutez **npm installer** sur un ordinateur Windows qui a des composants requis de tous les hello native du module. Ensuite, déployez hello créé **nœud\_modules** dossier dans le cadre de hello application tooAzure du Service d’applications.

  * Avant de compiler, vérifiez que votre installation de Node.js locale a architecture correspondante et version de hello est aussi proche que possible toohello celui utilisé dans Azure (les valeurs actuelles hello peuvent être vérifiées sur le runtime à partir des propriétés **process.arch**et **process.version**).

* Azure App Service peut être configuré tooexecute un interpréteur de commandes personnalisé ou des scripts de shell pendant le déploiement, ce qui vous donne hello des commandes personnalisées opportunité tooexecute et de configurer précisément hello moyen **npm installer** est en cours d’exécution. Pour une vidéo montrant comment tooconfigure cet environnement, consultez [des Scripts de déploiement de site Web personnalisé avec Kudu].

### <a name="using-a-packagejson-file"></a>Utilisation du fichier package.json
Hello **package.json** fichier est un moyen toospecify hello niveau supérieur dépendances de votre application nécessite hello plateforme d’hébergement permettant d’installer les dépendances hello, au lieu de vous obliger tooinclude hello **nœud \_packages** dossier dans le cadre du déploiement de hello. Une fois l’application hello a été déployée, hello **npm installer** commande est utilisée tooparse hello **package.json** de fichiers et d’installer toutes les dépendances de hello répertoriés.

Pendant le développement, vous pouvez utiliser hello **--enregistrer**, **--save-dev**, ou **--save-facultatif** paramètres lors de l’installation des modules tooadd une entrée pour hello module tooyour **package.json** fichier automatiquement. Pour plus d'informations, consultez la page [npm-install](https://docs.npmjs.com/cli/install).

Un problème potentiel avec hello **package.json** fichier est qu’il indique uniquement version hello pour les dépendances de niveau supérieur. Chaque module installé peut ou ne pouvez pas spécifier de version hello de modules hello qu'il dépend, et il est possible que vous risquez par une chaîne de dépendance différente que hello celui utilisé dans le développement.

> [!NOTE]
> Lors du déploiement tooAzure Service d’application, si votre <b>package.json</b> fichier fait référence à un module natif, vous pouvez voir un toohello similaire erreur lors de la publication d’application hello à l’aide de Git suivantes : exemple :
> 
> npm ERR! module-name@0.6.0 install: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp configure build"' failed with 1
> 
> 

### <a name="using-a-npm-shrinkwrapjson-file"></a>Utilisation d'un fichier npm-shrinkwrap.json
Hello **npm-shrinkwrap.json** fichier est une tentative de tooaddress hello module des limitations de versioning de hello **package.json** fichier. Lors de hello **package.json** fichier inclut uniquement les versions pour les modules de niveau supérieur hello, hello **npm-shrinkwrap.json** fichier contient hello la configuration requise pour la chaîne de dépendance hello complet du module.

Lorsque votre application est prête pour la production, vous pouvez verrouiller la configuration requise et créer un **npm-shrinkwrap.json** fichier à l’aide de hello **npm film** commande. Cette commande utilise les versions hello actuellement installées dans hello **nœud\_modules** dossier et enregistrer ces toohello versions **npm-shrinkwrap.json** fichier. Une fois l’application hello a été déployé toohello environnement d’hébergement, hello **npm installer** commande est utilisée tooparse hello **npm-shrinkwrap.json** de fichiers et d’installer toutes les dépendances de hello répertoriés. Pour plus d’informations, consultez [npm-shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap).

> [!NOTE]
> Lors du déploiement tooAzure Service d’application, si votre <b>npm-shrinkwrap.json</b> fichier fait référence à un module natif, vous pouvez voir un toohello similaire erreur lors de la publication d’application hello à l’aide de Git suivantes : exemple :
> 
> npm ERR! module-name@0.6.0 install: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp configure build"' failed with 1
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous comprenez comment les modules Node.js toouse avec Azure, découvrez comment trop[spécifier hello Node.js version], [générer et déployer une application web de Node.js](app-service-web/app-service-web-get-started-nodejs.md), et [comment toouse hello Azure de ligne de commande Interface pour Mac et Linux].

Pour plus d’informations, consultez hello [centre de développement Node.js](/nodejs/azure/).

[spécifier hello Node.js version]: nodejs-specify-node-version-azure-apps.md
[comment toouse hello Azure de ligne de commande Interface pour Mac et Linux]:cli-install-nodejs.md
[des Scripts de déploiement de site Web personnalisé avec Kudu]: https://channel9.msdn.com/Shows/Azure-Friday/Custom-Web-Site-Deployment-Scripts-with-Kudu-with-David-Ebbo
