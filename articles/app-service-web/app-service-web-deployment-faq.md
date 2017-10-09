---
title: aaaDeployment FAQ pour les applications web Azure | Documents Microsoft
description: "Obtenir elles sonttrop des réponses aux questions sur le déploiement pour la fonctionnalité d’applications Web hello de Service d’applications Azure."
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
ms.openlocfilehash: 566e1d7028e678f9679200f436118d27dfb07079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-faqs-for-web-apps-in-azure"></a>Forum aux questions sur le déploiement de Web Apps dans Azure

Cet article a elles sonttrop des réponses aux questions (FAQ) sur les problèmes de déploiement pour hello [fonctionnalité des applications Web d’Azure App Service](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-am-just-getting-started-with-app-service-web-apps-how-do-i-publish-my-code"></a>Je découvre App Service Web Apps. Comment publier mon code ?

Voici quelques options pour la publication de votre code d’application web :

*   Effectuer un déploiement à l’aide de Visual Studio. Si vous avez des solutions de Visual Studio hello, cliquez sur le projet d’application web hello et sélectionnez **publier**.
*   Déployez à l’aide d’un client FTP. Bonjour portail Azure, téléchargement hello publier le profil pour l’application hello web que vous souhaitez que toodeploy votre code. Ensuite, téléchargez hello fichiers too\site\wwwroot à l’aide de hello même publier des informations d’identification de profil FTP.

Pour plus d’informations, consultez [déployer votre application de tooApp Service](web-sites-deploy.md).

## <a name="i-see-an-error-message-when-i-try-toodeploy-from-visual-studio-how-do-i-resolve-this"></a>Je vois un message d’erreur lors de le toodeploy à partir de Visual Studio. Comment résoudre ce problème ?

Si vous voyez hello message suivant, vous utilisez peut-être une ancienne version du Kit de développement logiciel de hello : « erreur lors du déploiement pour la ressource 'YourResourceName' dans le groupe de ressources 'YourResourceGroup' : MissingRegistrationForLocation : abonnement de hello n’est pas inscrit pour Hello type de ressource « components » dans l’emplacement de hello « Du centre des États-Unis ». Réinscrivez pour ce fournisseur dans un emplacement de toothis accès ordre toohave. » 

tooresolve cette erreur, la mise à niveau toohello [dernière version du SDK](https://azure.microsoft.com/downloads/). Si vous voyez ce message et que vous avez hello la dernière version du SDK, envoyez une demande de prise en charge.

## <a name="how-do-i-deploy-an-aspnet-application-from-visual-studio-tooapp-service"></a>Comment pour déployer une application ASP.NET à partir de Visual Studio tooApp Service ?
<a id="deployasp"></a>

didacticiel de Hello [créer votre première application de web ASP.NET dans Azure dans les cinq minutes](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) vous montre comment toodeploy ASP.NET web application web application tooa du Service d’applications à l’aide de Visual Studio 2015.

## <a name="what-are-hello-different-types-of-deployment-credentials"></a>Quelles sont les hello différents types d’informations d’identification de déploiement ?

App Service prend en charge deux types d’informations d’identification pour le déploiement Git local et le déploiement FTP/S. Pour plus d’informations sur la façon de voir des informations d’identification de déploiement tooconfigure [configurer les informations d’identification de déploiement pour le Service d’applications](app-service-deployment-credentials.md).

## <a name="what-is-hello-file-or-directory-structure-of-my-app-service-web-app"></a>Qu’est la structure de fichier ou répertoire hello de mon application web de Service d’applications ?

Pour plus d’informations sur la structure des fichiers de votre application de Service de l’application hello, consultez [structure du fichier dans Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).

## <a name="how-do-i-resolve-ftp-error-550---there-is-not-enough-space-on-hello-disk-when-i-try-tooftp-my-files"></a>Comment résoudre « Erreur FTP 550 - il n’y n'est pas suffisamment d’espace sur le disque de hello » lorsque vous essayez tooFTP mes fichiers ?

Si vous voyez ce message, il est probable que vous exécutez dans un quota de disque dans le plan de service hello pour votre application web. Vous devrez peut-être tooscale des tooa niveau de service plus élevé en fonction de vos besoins en espace disque. Pour plus d’informations sur les plans de tarification et les limites de ressources, voir [Tarification de App Service](https://azure.microsoft.com/pricing/details/app-service/).

## <a name="how-do-i-set-up-continuous-deployment-for-my-app-service-web-app"></a>Comment configurer un déploiement continu pour mon application web App Service ?

Vous pouvez configurer un déploiement continu à partir de plusieurs ressources, dont Visual Studio Team Services, OneDrive, GitHub, Bitbucket, Dropbox et d’autres référentiels Git. Ces options sont disponibles dans le portail de hello. [Déploiement continu tooApp Service](app-service-continuous-deployment.md) utile didacticiel explique comment tooset configuration du déploiement continu.

## <a name="how-do-i-troubleshoot-issues-with-continuous-deployment-from-github-and-bitbucket"></a>Comment résoudre les problèmes de déploiement continu à partir de GitHub et de Bitbucket ?

Pour approfondir les problèmes liés à un déploiement continu à partir de GitHub ou de Bitbucket, voir [Analyse du déploiement continu](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment).

## <a name="i-cant-ftp-toomy-site-and-publish-my-code-how-do-i-resolve-this"></a>Je ne peux pas me toomy site FTP et publier mon code. Comment résoudre ce problème ?

problèmes de tooresolve FTP :

1. Vérifiez que vous entrez des informations d’identification et le nom d’hôte correct hello. Pour plus d’informations sur les différents types d’informations d’identification et toouse, voir [informations d’identification de déploiement](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).
2. Vérifiez que les ports de hello FTP ne sont pas bloqués par un pare-feu. les ports Hello doivent les paramètres suivants :
    * Port de connexion de contrôle FTP : 21
    * Port de connexion de contrôle FTP : 989, 10001-10300

## <a name="how-do-i-publish-my-code-tooapp-service"></a>Comment publier mon tooApp code Service ?

Hello démarrage rapide d’Azure est conçue toohelp vous déployez votre application à l’aide de la pile de déploiement hello et la méthode de votre choix. toouse hello démarrage rapide, Bonjour portail Azure, accédez trop**paramètres** > **déploiement d’applications**.

## <a name="why-does-my-app-sometimes-restart-after-deployment-tooapp-service"></a>Pourquoi mon application parfois redémarre après déploiement tooApp Service ?

toolearn sur les circonstances hello sous lequel un déploiement d’application peut entraîner un redémarrage, consultez [déploiement par rapport aux problèmes d’exécution](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts"). Comme décrit dans l’article de hello, du Service d’applications déploie dossier de fichiers toohello wwwroot. Il ne redémarre jamais directement votre application.

## <a name="how-do-i-integrate-visual-studio-team-services-code-with-app-service"></a>Comment intégrer le code de Visual Studio Team Services avec App Service ?

Vous disposez de deux options pour l’utilisation d’un déploiement continu avec Visual Studio Team Services :

*   Utiliser un projet Git. Se connecter via le Service d’applications à l’aide des options de déploiement hello pour ce référentiel.
*   Utiliser un projet Team Foundation Version Control (TFVC). Déployer à l’aide de l’agent de build hello pour le Service d’applications.

Le déploiement de code en continu pour ces deux options dépend des flux de travail de développeur et des procédures de vérification existants. Pour plus d’informations, voir les articles suivants : 

*   [Implémenter un déploiement continu de votre application de tooan site Web Azure](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)
*   [Définir un compte Visual Studio Team Services afin qu’il peut déployer l’application de web tooa](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)

## <a name="how-do-i-use-ftp-or-ftps-toodeploy-my-app-tooapp-service"></a>Comment utiliser FTP ou FTPS toodeploy mon tooApp app Service ?

Pour plus d’informations sur l’utilisation de FTP ou FTPS toodeploy votre tooApp d’application web Service, consultez [déployer votre tooApp app Service à l’aide de FTP/S](app-service-deploy-ftp.md).
