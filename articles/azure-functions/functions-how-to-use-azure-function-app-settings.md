---
title: "aaaConfigure paramètres d’application Azure fonction | Documents Microsoft"
description: "Découvrez le fonctionnement des tooconfigure Azure sur les paramètres de l’application."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a>Comment toomanage une application hello portail Azure (fonction) 

Dans les fonctions d’Azure, une application de la fonction fournit le contexte de l’exécution de hello pour vos fonctions individuelles. Comportements d’application de fonction appliquent de fonctions de tooall hébergées par une application de la fonction donnée. Cette rubrique décrit comment tooconfigure et gérer vos applications de fonction Bonjour portail Azure.

toobegin, accédez toohello [portail Azure](http://portal.azure.com) et connectez-vous à tooyour compte Azure. Dans la barre de recherche hello haut hello du portail de hello, tapez nom hello de votre application de la fonction et sélectionnez-le dans la liste de hello. Après avoir sélectionné votre application de la fonction, vous voyez hello suivant page :

![Présentation de l’application Bonjour portail Azure (fonction)](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <a name="manage-app-service-settings"></a>Onglet Paramètres de Function App

![Présentation de l’application fonction Bonjour portail Azure.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

Hello **paramètres** onglet est où vous pouvez mettre à jour la version du runtime fonctions hello utilisée par votre application de la fonction. Il est également où vous gérer hello hôte clés utilisées toorestrict accès tooall fonctions HTTP hébergées par l’application de fonction hello.

Functions prend en charge les plans d’hébergement App Service et Consommation. Pour plus d’informations, consultez [choisissez plan de service correcte hello pour les fonctions d’Azure](functions-scale.md). Pour une meilleure prévisibilité dans le plan de la consommation de hello, fonctions vous permet de limiter l’utilisation de la plateforme en définissant un quota d’utilisation quotidienne, en secondes de gigaoctets. Une fois que le quota d’utilisation quotidienne hello est atteinte, application de fonction hello est arrêtée. Une application de la fonction s’est arrêtée suite à atteindre hello dépenses quota peut être réactivée à partir de hello même contexte que l’établissement de hello quotidiennement les dépenses quota. Consultez hello [fonctions Azure page de tarification](http://azure.microsoft.com/pricing/details/functions/) pour plus d’informations sur la facturation.   

## <a name="platform-features-tab"></a>Onglet Fonctionnalités de la plate-forme

![Onglet Fonctionnalités de la plate-forme de Function App.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

Les applications de fonction s’exécutent et sont conservées par la plateforme de Service d’applications Azure hello. Par conséquent, vos applications de fonction ont toomost d’accès de fonctionnalités hello du site web d’Azure core plateforme d’hébergement. Hello **fonctionnalités de plateforme** onglet est où vous avez accès hello nombreuses fonctionnalités de hello plateforme du Service d’applications que vous pouvez utiliser dans vos applications de fonction. 

> [!NOTE]
> Pas toutes les fonctionnalités de Service d’applications sont disponibles lorsqu’une application de la fonction s’exécute sur le plan d’hébergement hello consommation.

reste Hello de cette rubrique concentre sur hello suivant les fonctionnalités du Service de l’application hello portail Azure qui sont utiles pour les fonctions :

+ [Éditeur App Service](#editor)
+ [Paramètres de l’application](#settings) 
+ [Console](#console)
+ [Outils avancés (Kudu)](#kudu)
+ [Options de déploiement](#deployment)
+ [CORS](#cors)
+ [Authentification](#auth)
+ [Définition de l’API](#swagger)

Pour plus d’informations sur la façon toowork avec les paramètres du Service d’applications, consultez [configurer les paramètres de Service Azure App](../app-service-web/web-sites-configure.md).

### <a name="editor"></a>Éditeur App Service

| | |
|-|-|
| ![Éditeur App Service de Function App.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | Hello éditeur de Service de l’application est un éditeur avancé de portail que vous pouvez utiliser les fichiers de configuration JSON toomodify et les fichiers de code similaires. L’activation de cette option entraîne l’ouverture d’un onglet distinct du navigateur avec un éditeur de base. Cela vous permet de toointegrate avec hello Git référentiel, exécuter et déboguer le code et modifier les paramètres de l’application (fonction). Cet éditeur fournit un environnement de développement améliorée pour vos fonctions par rapport à un panneau de l’application hello par défaut (fonction).    |

![Hello éditeur de Service de l’application](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <a name="settings"></a>Paramètres de l’application

| | |
|-|-|
| ![Paramètres de l’application Function App.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | Hello du Service d’applications **paramètres de l’Application** lame est où vous configurer et gérez les versions du framework, le débogage distant, paramètres de l’application et les chaînes de connexion. Lorsque vous intégrez votre Function App avec d’autres services tiers et Azure, vous pouvez modifier ces paramètres ici. |

![Configurer les paramètres de l’application](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <a name="console"></a>Console

| | |
|-|-|
| ![Console d’application de fonction Bonjour portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | console de portail Hello est un outil de développement idéal lorsque vous préférez toointeract avec votre application de la fonction à partir de la ligne de commande hello. Les commandes courantes incluent la création de fichiers et de répertoires et la navigation, ainsi que l’exécution de scripts et de fichiers de commandes. |

![Console Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <a name="kudu"></a>Outils avancés (Kudu)

| | |
|-|-|
| ![Fonction application Kudu Bonjour portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | Hello outils avancés pour le Service d’application (également appelé Kudu) fournissent l’accès tooadvanced les fonctionnalités d’administration de votre application de la fonction. Dans Kudu, vous pouvez gérer les informations système, les paramètres d’application, les variables d’environnement, les extensions de site, les en-têtes HTTP et les variables de serveur. Vous pouvez également lancer **Kudu** en parcourant le point de terminaison SCM toohello pour votre application de la fonction, comme`https://<myfunctionapp>.scm.azurewebsites.net/` |

![Configurer Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><a name="deployment">Options de déploiement

| | |
|-|-|
| ![Options de déploiement d’application fonction Bonjour portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | Functions vous permet de développer votre code de fonctions sur votre machine locale. Vous pouvez ensuite charger votre tooAzure de projet d’application fonction locale. En outre de téléchargement FTP tootraditional, fonctions vous permet de déployer votre application de fonction utilisant des solutions d’intégration continue populaires, tels que GitHub, VSTS, Dropbox, Bitbucket et d’autres. Pour plus d’informations, consultez [Déploiement continu pour Azure Functions](functions-continuous-deployment.md). tooupload manuellement à l’aide de FTP ou Git local, vous devez également [configurer vos informations d’identification de déploiement](functions-continuous-deployment.md#credentials). |


### <a name="cors"></a>CORS

| | |
|-|-|
| ![Fonction application CORS Bonjour portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | l’exécution du code malveillant tooprevent dans vos services, les blocs de Service de l’application appelle tooyour fonction applications provenant de sources externes. Prend en charge les fonctions toolet (CORS) vous définissez une « liste » des autorisé d’origine à partir de laquelle vos fonctions peuvent accepter des demandes à distance du partage des ressources cross-origin.  |

![Configurer l’élément CORS de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <a name="auth"></a>Authentification

| | |
|-|-|
| ![Authentification d’application de fonction Bonjour portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | Lorsque les fonctions utilisent un déclencheur HTTP, vous pouvez exiger que les appels toofirst être authentifié. App Service prend en charge l’authentification Azure Active Directory et la connexion avec des fournisseurs sociaux tels que Facebook, Microsoft et Twitter. Pour plus d’informations sur la configuration de fournisseurs d’authentification spécifiques, consultez [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md) (Vue d’ensemble de l’authentification Azure App Service). |

![Configurer l’authentification pour une Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <a name="swagger"></a>Définition de l’API

| | |
|-|-|
| ![API d’application de fonction swagger définition Bonjour portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | Prend en charge les fonctions Swagger tooallow clients toomore consommer facilement vos fonctions déclenchés par HTTP. Pour plus d’informations sur la création de définitions d’API avec Swagger, consultez [Prise en main d’API Apps, d’ASP.NET et de Swagger dans Azure](../app-service-api/app-service-api-dotnet-get-started.md). Vous pouvez également utiliser les fonctions proxys toodefine une surface API unique pour plusieurs fonctions. Pour plus d’informations, consultez [Utilisation de Azure Functions Proxies (préversion)](functions-proxies.md). |

![Configurer l’API de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a>Étapes suivantes

+ [Configurer des applications web dans Azure App Service](../app-service-web/web-sites-configure.md)
+ [Déploiement continu pour Azure Functions](functions-continuous-deployment.md)



