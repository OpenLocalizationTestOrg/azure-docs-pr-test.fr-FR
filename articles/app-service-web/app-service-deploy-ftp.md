---
title: "aaaDeploy votre tooAzure d’application du Service d’applications à l’aide de FTP/S | Documents Microsoft"
description: "Découvrez comment toodeploy votre tooAzure d’application du Service d’applications à l’aide de FTP ou FTPS."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a>Déployer votre tooAzure d’application du Service d’applications à l’aide de FTP/S

Cet article vous montre comment toouse FTP ou FTPS toodeploy votre application web, un principal de l’application mobile ou une application API trop[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).

point de terminaison Hello FTP/S pour votre application est déjà active. Aucune configuration n’est un déploiement de FTP/S tooenable nécessaire.

> [!IMPORTANT]
> Nous prenons en permanence des étapes tooimprove sécurité de la plateforme Microsoft Azure. Dans le cadre de cet effort continu, une mise à niveau des Applications Web est prévue pour les régions d’Allemagne centrale et d’Allemagne du nord-est. Au cours de cette, applications Web seront désactivation utilisez hello du protocole FTP en texte brut pour les déploiements. Nos clients tooour de recommandation est tooFTPS tooswitch pour les déploiements. Nous n’attendent pas de n’importe quel service de tooyour interruption pendant cette mise à niveau qui est prévue pour le 9/5. Nous vous remercions du soutien apporté à cet effort.

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a>Étape 1 : définir les informations d’identification du déploiement

serveur de hello FTP tooaccess pour votre application, vous devez tout d’abord d’informations d’identification de déploiement. 

tooset ou réinitialiser vos informations d’identification de déploiement, consultez [informations d’identification du déploiement Azure App Service](app-service-deployment-credentials.md). Ce didacticiel montre l’utilisation hello d’informations d’identification au niveau de l’utilisateur.

## <a name="step-2-get-ftp-connection-information"></a>Étape 2 : obtenir les informations de connexion FTP

1. Bonjour [portail Azure](https://portal.azure.com), ouvrez votre application [panneau des ressources](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Sélectionnez **vue d’ensemble** dans le menu de gauche hello, puis notez les valeurs hello pour **utilisateur FTP/déploiement**, **nom d’hôte FTP**, et **nom d’hôte FTPS**. 

    ![Informations de connexion FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > Hello **utilisateur FTP/déploiement** valeur utilisateur tel qu’affiché par hello portail Azure, y compris le nom de l’application hello dans l’ordre tooprovide bon contexte hello FTP serveur.
    > Vous pouvez trouver hello les mêmes informations lorsque vous sélectionnez **propriétés** dans le menu de gauche hello. 
    >
    > En outre, le mot de passe de déploiement hello n’est jamais affichée. Si vous oubliez votre mot de passe de déploiement, revenez trop[étape 1](#step1) et réinitialiser votre mot de passe de déploiement.
    >
    >

## <a name="step-3-deploy-files-tooazure"></a>Étape 3 : Déployer des fichiers tooAzure

1. À partir de votre client FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc.), utilisez les informations de connexion hello collectées tooconnect tooyour application.
3. Copier vos fichiers et leur toohello de structure de répertoire correspondant [ **/site/wwwroot** active](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) dans Azure (ou hello **/site/wwwroot/App_Data/tâches/** répertoire pour Les tâches Web).
4. Application de l’application de navigation tooyour URL tooverify hello s’exécute correctement. 

> [!NOTE] 
> Contrairement aux [déploiements Git](app-service-deploy-local-git.md), déploiement FTP ne prend pas en charge hello suivant automatisations de déploiement : 
>
> - restauration de dépendances (par exemple, des automatisations NuGet, NPM, PIP et Composer)
> - compilation de fichiers binaires .NET
> - génération du fichier web.config (dont voici un [exemple Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))
> 
> Vous devez restaurer, créer, générer ces fichiers requis manuellement sur votre ordinateur local et les déployer avec votre application.
>
>

## <a name="next-steps"></a>Étapes suivantes

Pour les scénarios de déploiement plus avancées, essayez [déploiement tooAzure avec Git](app-service-deploy-local-git.md). Déploiement GIT tooAzure permet le contrôle de version, la restauration des packages, MSBuild et bien plus encore.

## <a name="more-resources"></a>Autres ressources

* [Créer une application Web PHP-MySQL dans Azure App Service et la déployer à l’aide de FTP](web-sites-php-mysql-deploy-use-ftp.md).
* [Informations d’identification du déploiement d’Azure App Service](app-service-deploy-ftp.md)
