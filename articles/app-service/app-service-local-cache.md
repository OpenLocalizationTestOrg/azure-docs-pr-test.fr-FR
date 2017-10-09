---
title: "vue d’ensemble de la mémoire Cache locale de Service d’application aaaAzure | Documents Microsoft"
description: "Cet article décrit comment tooenable, redimensionner et requête hello état de la fonctionnalité de Cache Local du Service application Azure hello"
services: app-service
documentationcenter: app-service
author: SyntaxC4
manager: yochayk
editor: 
tags: optional
keywords: 
ms.assetid: e34d405e-c5d4-46ad-9b26-2a1eda86ce80
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/04/2016
ms.author: cfowler
ms.openlocfilehash: 220331ac7e15352a434d63266701071024d868c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-local-cache-overview"></a>Présentation du cache local d’Azure App Service
Le contenu des applications web Azure est stocké sur Azure Storage et est exposé de manière durable en tant que partage de contenu. Cette conception est prévue toowork avec un large éventail d’applications et a hello suivant d’attributs :  

* contenu de Hello est partagé entre plusieurs instances de machine virtuelle (VM) de l’application web hello.
* contenu de Hello est durable et peut être modifié par les applications web en cours d’exécution.
* Fichiers journaux et les fichiers de données de diagnostic sont disponibles sous hello partagée dossier de contenu.
* Publication de nouveaux contenus directement des mises à jour hello dossier de contenu. Vous pouvez immédiatement hello d’affichage de contenu par le biais du site Web SCM hello et hello l’application web en cours d’exécution (généralement des technologies telles que ASP.NET lancer un redémarrage d’application web sur certains fichiers modifications tooget hello contenu le plus récent).

Tandis que de nombreuses applications web utilisent une seule ou la totalité de ces fonctionnalités, certaines autres ont uniquement besoin d’un magasin de contenu en lecture seule très performant à partir duquel elles peuvent s’exécuter avec une haute disponibilité. Ces applications peuvent tirer profit d’une instance de machine virtuelle sur un cache local spécifique.

fonctionnalité de Cache Local du Service application Azure Hello fournit une vue de rôle web de votre contenu. Ce contenu est un cache d’écriture avec rejet de votre contenu de stockage qui est créé de façon asynchrone au démarrage du site. Lorsque le cache de hello est prêt, site de hello est commuté toorun de contenu hello mis en cache. Les applications Web qui s’exécutent sur le Cache Local ont hello avantages suivants :

* Ils sont abri toolatencies qui se produisent lorsqu’ils accèdent à des contenus sur le stockage Azure.
* Elles sont mises à niveau abri toohello planifié ou à un temps mort planifié et toutes les autres problèmes avec le stockage Azure qui se produisent sur les serveurs qui font Office de partage de contenu hello.
* Ils ont moins de redémarrages application en raison de modifications de partage toostorage.

## <a name="how-local-cache-changes-hello-behavior-of-app-service"></a>Comment le Cache Local modifie le comportement hello du Service d’application
* le cache local Hello est une copie de hello /site /siteextensions dossiers et de l’application web hello. Il est créé sur une instance de machine virtuelle locale hello sur le démarrage de l’application web. Hello taille du cache local de hello par l’application web est limitée Mo too300 par défaut, mais vous pouvez l’augmenter les too2 go.
* le cache local Hello est en lecture-écriture. Toutefois, toutes les modifications seront ignorées lors hello web application déplace les ordinateurs virtuels ou obtient redémarrée. Vous ne devez pas utiliser le Cache Local pour les applications qui stockent des données critiques dans le magasin de contenu hello.
* Les applications Web peuvent continuer toowrite des fichiers journaux et les données de diagnostic, comme ils le font actuellement. Fichiers journaux et données, cependant, sont stockées localement sur hello machine virtuelle. Ils sont ensuite copiées régulièrement toohello magasin de contenu partagé. magasin de contenu partagé copie toohello Hello est un meilleur effort--permet de sauvegarder écriture pourrait être perdues en raison de pannes soudaines de tooa d’une instance de la machine virtuelle.
* Il existe une modification de la structure de dossiers hello hello LogFiles et des dossiers de données pour les applications web qui utilisent le Cache Local. Il existe désormais des sous-dossiers dans les dossiers de fichiers journaux et de données de stockage hello qui suivent le modèle de désignation hello de « identificateur » + horodatage. Chacun des sous-dossiers de hello correspond tooa instance d’ordinateur virtuel où l’application hello web est en cours d’exécution ou exécuté.  
* Publication modifications toohello l’application web par le biais de mécanismes de publication hello publiera toohello magasin de contenu partagé. Ceci est normal car nous souhaitons hello publié toobe contenu durable. toorefresh hello le cache local de l’application web de hello, il doit toobe redémarré. Cela sembler une étape excessive cycle de hello toomake transparente, consultez les informations de hello plus loin dans cet article.
* D:\Home pointera toohello le cache local. D:\Local continue pointant toohello machine virtuelle spécifique temporaire.
* affichage du contenu par défaut Hello du site SCM hello continue toobe qui Hello magasin de contenu partagé.

## <a name="enable-local-cache-in-app-service"></a>Activer le cache local dans App Service
Configurez le cache local à l’aide d’une combinaison de paramètres d’application réservés. Vous pouvez configurer ces paramètres d’application à l’aide de hello méthodes suivantes :

* [Portail Azure](#Configure-Local-Cache-Portal)
* [Azure Resource Manager](#Configure-Local-Cache-ARM)

### <a name="configure-local-cache-by-using-hello-azure-portal"></a>Configurer le Cache Local à l’aide de hello portail Azure
<a name="Configure-Local-Cache-Portal"></a>

Activez le cache local pour chaque application web en utilisant ce paramètre d’application : `WEBSITE_LOCAL_CACHE_OPTION` = `Always`  

![Paramètres d’application du portail Azure : cache local](media/app-service-local-cache/app-service-local-cache-configure-portal.png)

### <a name="configure-local-cache-by-using-azure-resource-manager"></a>Configurer le cache local à l’aide d’Azure Resource Manager
<a name="Configure-Local-Cache-ARM"></a>

```

...

{
    "apiVersion": "2015-08-01",
    "type": "config",
    "name": "appsettings",
    "dependsOn": [
        "[resourceId('Microsoft.Web/sites/', variables('siteName'))]"
    ],

"properties": {
        "WEBSITE_LOCAL_CACHE_OPTION": "Always",
        "WEBSITE_LOCAL_CACHE_SIZEINMB": "300"
    }
}

...
```

## <a name="change-hello-size-setting-in-local-cache"></a>Modifier le paramètre de taille hello dans le Cache Local
Par défaut, taille de cache local hello est **300 Mo**. Cela inclut les /site hello et /siteextensions les dossiers qui sont copiés à partir de hello contenu magasin, ainsi que toute créées localement les dossiers des journaux et de données. tooincrease cette limite, utilisez le paramètre d’application hello `WEBSITE_LOCAL_CACHE_SIZEINMB`. Vous pouvez augmenter la taille de hello jusqu'à trop**2 Go** (2 000 Mo) par l’application web.

## <a name="best-practices-for-using-app-service-local-cache"></a>Bonnes pratiques pour utiliser le cache local d’App Service
Nous vous recommandons d’utiliser le Cache Local en conjonction avec hello [environnements de préproduction](../app-service-web/web-sites-staged-publishing.md) fonctionnalité.

* Ajouter hello *rémanentes* paramètre d’application `WEBSITE_LOCAL_CACHE_OPTION` avec la valeur de hello `Always` tooyour **Production** emplacement. Si vous utilisez `WEBSITE_LOCAL_CACHE_SIZEINMB`, également l’ajouter en tant que paramètre rémanentes tooyour Production slot.
* Créer un **intermédiaire** emplacement et l’emplacement intermédiaire de tooyour de publication. Vous ne définissez généralement pas hello emplacement toouse le Cache Local tooenable un cycle de vie de génération-déploiement-test transparente pour intermédiaires si vous bénéficiez des avantages de hello du Cache Local pour l’emplacement de production hello de mise en lots.
* Testez votre site par rapport à votre emplacement de préproduction.  
* Quand vous êtes prêt, lancez une [opération d’échange](../app-service-web/web-sites-staged-publishing.md#Swap) entre vos emplacements de préproduction et de production.  
* Paramètres rémanentes incluent les nom et emplacement de tooa répétitive. Par conséquent, lors de l’emplacement intermédiaire de hello obtient permuté en Production, elle hérite des paramètres de l’application hello le Cache Local. Hello échangés nouvellement Production emplacement sera exécuté sur le cache local hello après quelques minutes et s’être préparée dans le cadre de la préparation de l’emplacement après l’échange. Par conséquent, lors de l’échange d’emplacement hello est terminée, votre emplacement de Production s’exécute sur le cache local hello.

## <a name="frequently-asked-questions-faq"></a>Forum Aux Questions (FAQ)
### <a name="how-can-i-tell-if-local-cache-applies-toomy-web-app"></a>Comment puis-je savoir si le Cache Local s’applique à l’application web toomy ?
Si votre application web a besoin d’un magasin de contenu hautes performances, fiable, n’utilise pas les données critiques de hello magasin de contenu toowrite lors de l’exécution et est inférieure à 2 Go de taille totale, les réponses hello sont « Oui » ! tooget hello taille totale de vos dossiers /site et /siteextensions, vous pouvez utiliser l’extension de site hello « Utilisation du disque Azure Web Apps ».  

### <a name="how-can-i-tell-if-my-site-has-switched-toousing-local-cache"></a>Comment puis-je savoir si mon site a basculé toousing le Cache Local ?
Si vous utilisez la fonctionnalité de Cache locale hello avec les environnements de préproduction, opération de permutation hello s’achève pas tant que le Cache Local est préparée. toocheck si votre site est en cours d’exécution sur le Cache Local, vous pouvez vérifier variable d’environnement hello travail processus `WEBSITE_LOCALCACHE_READY`. Utilisez les instructions hello hello [variable d’environnement de processus de travail](https://github.com/projectkudu/kudu/wiki/Process-Threads-list-and-minidump-gcdump-diagsession#process-environment-variable) page tooaccess hello variable d’environnement de processus travail sur plusieurs instances.  

### <a name="i-just-published-new-changes-but-my-web-app-does-not-seem-toohave-them-why"></a>Vous venez de publier nouvelles modifications, mais mon application web ne semble pas toohave les. Pourquoi ?
Si votre application web utilise le Cache Local, vous devez toorestart votre site tooget hello dernières modifications. Ne souhaitez pas que site de production tooa toopublish modifications ? Consultez les options d’emplacement de hello dans la section des pratiques recommandées précédente hello.

### <a name="where-are-my-logs"></a>Où sont mes journaux ?
Avec le cache local, vos dossiers de données et de journaux se présentent un peu différemment. Toutefois, hello structure de votre reste sous-dossiers hello identiques, sauf que les sous-dossiers hello sont imbriqués sous un sous-dossier avec hello format « identificateur de machine virtuelle unique » + horodatage.

### <a name="i-have-local-cache-enabled-but-my-web-app-still-gets-restarted-why-is-that-i-thought-local-cache-helped-with-frequent-app-restarts"></a>J’ai activé le cache local, mais mon application web redémarre systématiquement. Pourquoi ? Je pensais que le cache local évitait les redémarrages d’application fréquents.
En effet, le cache local contribue à limiter les redémarrages d’application web liés au stockage. Toutefois, votre application web peut toujours subir un redémarrage pendant les mises à niveau de l’infrastructure planifiée de hello machine virtuelle. Hello globale redémarrages d’application que vous rencontrez avec le Cache Local activé doivent être moins.

### <a name="does-local-cache-exclude-any-directories-from-being-copied-toohello-faster-local-drive"></a>Ne le Cache Local exclure les répertoires d’être copiés toohello le disque local plus rapidement ?
Dans le cadre de l’étape hello qui copie le contenu du stockage hello n’importe quel dossier nommé référentiel sera exclu. Cela permet des scénarios où le contenu du site peut contenir un référentiel de contrôle de code source ne peut pas être nécessaire dans l’opération de tooday jour de l’application web hello. 
