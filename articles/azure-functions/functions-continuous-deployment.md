---
title: "déploiement aaaContinuous pour les fonctions de Azure | Documents Microsoft"
description: "Utiliser les fonctionnalités de déploiement continu d’Azure App Service toopublish vos fonctions de Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a>Déploiement continu pour Azure Functions
Les fonctions Azure rend toodeploy facilement votre application de fonction à l’aide de l’intégration continue du Service d’applications. Functions s’intègre à BitBucket, Dropbox, GitHub et Visual Studio Team Services (VSTS). Ainsi, un flux de travail où le code de la fonction mises à jour apportée à l’aide d’un de ces tooAzure de déploiement de déclencheur de services intégrés. Si vous êtes nouvelles fonctions tooAzure, commencer par [vue d’ensemble des fonctions Azure](functions-overview.md).

Le déploiement continu est une option intéressante pour les projets auxquels plusieurs contributions fréquentes sont intégrées. Il vous permet également de conserver le contrôle de code source sur le code de vos fonctions. Hello sources de déploiement suivantes est actuellement prises en charge :

* [Bitbucket](https://bitbucket.org/)
* [Dropbox](https://www.dropbox.com/)
* Référentiel externe (Git ou Mercurial)
* [Référentiel Git local](../app-service-web/app-service-deploy-local-git.md)
* [GitHub](https://github.com)
* [OneDrive](https://onedrive.live.com/)
* [Visual Studio Team Services](https://www.visualstudio.com/team-services/)

Les déploiements sont configurés au cas par cas, selon les Function Apps. Après le déploiement continu est activé, code d’accès toofunction dans le portail de hello est défini trop*en lecture seule*.

## <a name="continuous-deployment-requirements"></a>Conditions requises pour le déploiement continu

Vous devez disposer de votre source de déploiement configurée et votre code de fonctions dans la source de déploiement hello avant de configurer le déploiement continu. Dans un déploiement d’application de fonction donnée, chaque fonction réside dans un sous-répertoire nommé, où le nom du répertoire hello est nom hello de fonction hello.  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a>Configurer un déploiement continu
Utilisez ce déploiement continu de procédure tooconfigure pour une application existante de la fonction. Les étapes suivantes présentent l’intégration avec un référentiel GitHub, mais des étapes similaires s’appliquent à Visual Studio Team Services ou à d’autres services de déploiement.

1. Dans votre application de la fonction Bonjour [portail Azure](https://portal.azure.com), cliquez sur **fonctionnalités de plateforme** et **options de déploiement**. 
   
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/setup-deployment.png)
 
2. Ensuite, dans hello **déploiements** cliquez sur le panneau **le programme d’installation**.
 
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. Bonjour **source du déploiement** panneau, cliquez sur **choisir les sources de**, puis renseignez les informations de hello pour votre source de déploiement choisie, cliquez sur **OK**.
   
    ![Choisir une source de déploiement](./media/functions-continuous-deployment/choose-deployment-source.png)

Après avoir configuré un déploiement continu, toutes les modifications de fichier dans votre source de déploiement sont copiés toohello fonction application et un déploiement de site complet est déclenché. site de Hello est redéployé lors de la mise à jour des fichiers de source de hello.

## <a name="deployment-options"></a>Options de déploiement

Hello Voici certains scénarios de déploiement classiques :

- [Créer un déploiement intermédiaire](#staging)
- [Déplacer le déploiement de toocontinuous fonctions existant](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a>Créer un déploiement intermédiaire

Function Apps ne prend pas encore en charge les emplacements de déploiement. Toutefois, vous pouvez tout de même gérer des déploiements intermédiaires et de production distincts à l’aide de l’intégration continue.

Hello tooconfigure de processus et de travail avec un déploiement intermédiaire se présente généralement comme suit :

1. Créez deux applications de fonction dans votre abonnement, un pour le code de production hello et un pour la mise en lots. 

2. Créez une source de déploiement, si vous n’en avez pas déjà. Cet exemple utilise [GitHub].

3. Pour votre application de fonction de production, les étapes de hello complète précédente **configurer le déploiement continu** et ensemble hello déploiement branche toohello de branche de maître du référentiel GitHub.
   
    ![Choisir une branche de déploiement](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. Répétez cette étape pour hello application de la fonction de mise en lots, mais choisissez hello intermédiaire à la place de branche dans votre référentiel GitHub. Si votre source de déploiement ne prend pas en charge la création de branches, utilisez un autre dossier.
    
5. Assurez-vous de mises à jour tooyour code Bonjour branche ou un dossier de mise en lots, puis vérifiez que ces modifications sont répercutées dans hello déploiement intermédiaire.

6. Après le test, fusionner des modifications à partir de hello branche de mise en lots dans la branche principale de hello. Cette application de fonction fusion déclencheurs déploiement toohello production. Si votre source de déploiement ne prend pas en charge les branches, remplacer les fichiers hello dans le dossier de production hello fichiers hello hello dossier intermédiaire.

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a>Déplacer le déploiement de toocontinuous fonctions existant
Lorsque vous disposez de fonctions existantes que vous avez créé et mis à jour dans le portail de hello, vous devez toodownload votre fonction des fichiers de code à l’aide de FTP ou hello référentiel Git local avant de pouvoir définir le déploiement continu comme décrit ci-dessus. Faire cela Bonjour les paramètres du Service d’applications pour votre application de la fonction. Une fois que vos fichiers sont téléchargés, vous pouvez les télécharger source du déploiement continu tooyour choisi.

> [!NOTE]
> Après avoir configuré l’intégration continue, vous ne seront plus en mesure de tooedit votre source de fichiers dans le portail de fonctions hello.

- [Comment configurer les informations d’identification de déploiement](#credentials)
- [Comment télécharger des fichiers via FTP](#downftp)
- [Comment : télécharger des fichiers à l’aide du référentiel Git hello](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a>Comment configurer les informations d’identification de déploiement
Avant de pouvoir télécharger des fichiers à partir de votre application de fonction avec FTP ou le référentiel Git, vous devez configurer votre site de hello tooaccess informations d’identification. Informations d’identification sont définies au niveau application à la fonction hello. Utilisez hello suit les informations d’identification du déploiement tooset étapes Bonjour portail Azure :

1. Dans votre application de la fonction Bonjour [portail Azure](https://portal.azure.com), cliquez sur **fonctionnalités de plateforme** et **informations d’identification de déploiement**.
   
    ![Définir les informations d’identification de déploiement local](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. Entrez un nom d’utilisateur et un mot de passe, puis cliquez sur **Enregistrer**. Vous pouvez désormais utiliser ces informations d’identification tooaccess votre application de la fonction à partir de FTP ou hello dépôt Git intégré.

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a>Comment télécharger des fichiers via le FTP

1. Dans votre application de la fonction Bonjour [portail Azure](https://portal.azure.com), cliquez sur **fonctionnalités de plateforme** et **propriétés**, puis copiez les valeurs hello pour **FTP/déploiement utilisateur**, **Nom de l’hôte FTP**, et **nom d’hôte FTPS**.  

    **Déploiement/FTP utilisateur** doit être entrée comme indiqué dans le portail hello, y compris le nom de l’application hello, tooprovide le contexte approprié pour le serveur de hello FTP.
   
    ![Obtenir vos informations de déploiement](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. À partir de votre client FTP, utilisez les informations de connexion hello collectées tooconnect tooyour application et télécharger des fichiers de source de hello pour vos fonctions.

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a>Comment télécharger des fichiers via le référentiel Git local

1. Dans votre application de la fonction Bonjour [portail Azure](https://portal.azure.com), cliquez sur **fonctionnalités de plateforme** et **options de déploiement**. 
   
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/setup-deployment.png)
 
2. Ensuite, dans hello **déploiements** cliquez sur le panneau **le programme d’installation**.
 
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. Bonjour **source du déploiement** panneau, cliquez sur **référentiel Git Local** puis cliquez sur **OK**.

3. Dans **fonctionnalités de plateforme**, cliquez sur **propriétés** et notez la valeur hello URL Git. 
   
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. Cloner le référentiel hello sur votre ordinateur local à l’aide d’une invite de commandes prenant en charge Git ou votre outil préféré de Git. commande de clone Git de Hello ressemble à ceci :
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. Récupérer les fichiers de votre clone de toohello fonction application sur votre ordinateur local, comme dans hello l’exemple suivant :
   
        git pull origin master
   
    Si nécessaire, fournissez vos [informations d’identification de déploiement configurées](#credentials).  

[GitHub]: https://github.com/
