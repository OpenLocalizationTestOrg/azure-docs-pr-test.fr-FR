---
title: "aaaLocal déploiement Git tooAzure du Service d’applications"
description: "Découvrez comment tooAzure tooenable local Git déploiement du Service d’applications."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a>TooAzure déploiement Git local du Service d’applications
Ce didacticiel vous montre comment toodeploy votre application trop[Azure App Service] à partir d’un référentiel Git sur votre ordinateur local. Service d’applications prend en charge cette approche avec hello **Git Local** option de déploiement dans hello [Azure Portal].  
Nombre de commandes Git de hello décrits dans cet article sont exécutées automatiquement lors de la création d’une application de Service d’applications à l’aide de hello [Interface de ligne de commande Azure] comme décrit [ici](app-service-web-get-started.md).

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez :

* Git. Vous pouvez télécharger le fichier binaire d’installation hello [ici](http://www.git-scm.com/downloads).  
* Connaissances élémentaires de Git.
* Un compte Microsoft Azure Si vous n’avez pas de compte, vous pouvez [vous inscrire pour un essai gratuit](https://azure.microsoft.com/pricing/free-trial) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.  
> 
> 

## <a name="Step1"></a>Étape 1 : création d’un référentiel local
Effectuer hello suivant de tâches toocreate un référentiel Git.

1. Lancez un outil de ligne de commande, comme **GitBash** (Windows) ou **Bash** (Unix Shell). Sur les systèmes OS X, vous pouvez accéder hello de ligne de commande via hello **Terminal** application.
2. Accédez répertoire toohello où toodeploy de contenu hello serait localisé.
3. Hello suivant commande tooinitialize un référentiel Git, utilisez :

```bash  
git init
```

## <a name="Step2"></a>Étape 2 : validation de votre contenu
App Service prend en charge des applications créées dans différents langages de programmation. 

1. Si votre référentiel contient déjà le contenu ignorer ce point et déplacer toopoint 2 ci-dessous. Si votre référentiel n'inclut pas encore de contenu, remplissez-le simplement avec un fichier .html statique comme suit : 
   
   * À l’aide d’un éditeur de texte, créez un nouveau fichier nommé **index.html** à racine hello du référentiel Git de hello
   * Ajouter hello après le texte comme contenu hello pour hello index.html fichier et enregistrez-le : *Hello Git !*
2. À partir de hello de ligne de commande, vérifiez que vous êtes sous racine hello de votre référentiel Git. Utilisez ensuite hello suivant du référentiel de commande tooadd fichiers tooyour :

```bash  
git add -A
```
3. Ensuite, la validation hello modifications toohello référentiel à l’aide de hello de commande suivante :

```bash  
git commit -m "Hello Azure App Service"
```  

## <a name="Step3"></a>Étape 3 : Activer hello référentiel d’application de Service d’applications
Effectuer hello suivant les étapes tooenable un référentiel Git pour votre application de Service d’applications.

1. Connectez-vous à toohello [Azure Portal].
2. Dans le panneau de votre application App Service, cliquez sur **Paramètres > Source du déploiement**. Cliquez successivement sur **Choisir une source**, **Référentiel Git local** et **OK**.  
   
    ![Référentiel Git local](./media/app-service-deploy-local-git/local_git_selection.png)
3. S’il s’agit de votre premier paramètre de temps un référentiel dans Azure, vous devez toocreate informations d’identification pour celle-ci. Vous allez utiliser les toolog dans hello référentiel Azure et publier des modifications à partir de votre référentiel Git local. Dans le panneau de votre application, cliquez sur **Paramètres > Informations d’identification du déploiement**, puis configurez le nom d’utilisateur et le mot de passe de votre déploiement. Quand vous avez terminé, cliquez sur **Enregistrer**.
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <a name="Step4"></a>Étape 4 : déploiement de votre projet
Utilisez hello suivant les étapes toopublish votre tooApp app Service à l’aide de Git Local.

1. Dans le panneau de votre application Bonjour portail Azure, cliquez sur **Paramètres > Propriétés** pour hello **URL Git**.
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    **URL GIT** est hello référence distante toodeploy toofrom votre référentiel local. Vous utiliserez cette URL de hello comme suit.
2. Hello de ligne de commande, vérifiez que vous êtes dans la racine de hello de votre référentiel Git local.
3. Utilisez `git remote` tooadd hello informations référence à distance répertorié dans **URL Git** à l’étape 1. Votre commande doit ressembler similaire toohello suivantes :
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > Hello **distant** commande ajoute un référentiel distant tooa de référence nommée. Dans cet exemple, une référence nommée « azure » est créée pour le référentiel de votre application web.
   > 
   > 
4. Push de votre contenu tooApp Service à l’aide de nouveau hello **azure** distant vous venez de créer.

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. Revenir en arrière application tooyour Bonjour portail Azure. Une entrée de journal de votre publication la plus récente doit être affichée dans hello **déploiements** panneau. 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. Cliquez sur hello **Parcourir** bouton haut hello hello tooverify à panneau de l’application hello contenu a été déployé. 

## <a name="Step5"></a>Résolution des problèmes
Hello Voici les erreurs ou des problèmes couramment rencontrés lors de l’utilisation de Git toopublish tooan application de Service de l’application dans Azure :

- - -
**Symptôme**: Impossible de tooaccess '[siteURL]' : Échec de tooconnect trop [scmAddress]

**Cause**: cette erreur peut se produire si l’application hello n’est pas en cours d’exécution.

**Résolution**: application hello de démarrage Bonjour portail Azure. Déploiement GIT ne fonctionne pas, sauf si l’application hello est en cours d’exécution. 

- - -
**Symptôme**: Impossible de résoudre l'hôte « nom_hôte »

**Cause**: cette erreur peut se produire si les informations d’adresse hello entré lors de la création hello 'azure' distant était incorrect.

**Résolution**: hello d’utilisation `git remote -v` commande toolist toutes les bases de données distantes, ainsi que les URL hello associé. Vérifiez que les URL hello hello 'azure' distant est correct. Si nécessaire, supprimez et recréez ce distant à l’aide de l’URL appropriée hello.

- - -
**Symptôme**: aucune référence en commun, ni spécifiée ; aucune action effectuée. Perhaps you should specify a branch such as 'master'.

**Cause**: cette erreur peut se produire si vous ne pas spécifier une branche lors de l’exécution d’une opération de diffusion de git et ont la valeur not set hello push.default utilisé par Git.

**Résolution**: effectuer l’opération hello push configuration de la branche maître hello. Par exemple :

```bash  
git push azure master
```
- - -
**Symptôme**: src refspec [nom_branche] ne correspond à aucun élément.

**Cause**: cette erreur peut se produire si vous essayez de branche de tooa toopush autres que master sur hello 'azure' à distance.

**Résolution**: effectuer l’opération hello push configuration de la branche maître hello. Par exemple :

```bash  
git push azure master
```
- - -
**Symptôme** : échec RPC ; résultat=22, Code HTTP = 502.

**Cause**: cette erreur peut se produire si vous essayez de toopush un référentiel git volumineux sur HTTPS.

**Résolution**: modifier la configuration git hello sur hello ordinateur local toomake hello post-mémoire tampon plus grande

```bash  
git config --global http.postBuffer 524288000
```
- - -
**Symptôme**: erreur - référentiel tooremote validée de modifications, mais votre application web ne pas mis à jour.

**Cause**: Cette erreur peut se produire si vous déployez une application Node.js contenant un fichier package.json spécifiant des modules obligatoires supplémentaires.

**Résolution**: Des messages supplémentaires contenant « npm ERR! doit être connecté toothis préalable erreur et peut fournir un contexte supplémentaire en cas d’échec hello. suivant de Hello est connues des causes de cette erreur et hello correspondant 'npm ERR !' » correspondant :

* **Fichier package.json incorrect**: npm ERR! Couldn’t read dependencies.
* **Native module that does not have a binary distribution for Windows**:
  
  * npm ERR! \`cmd "/c" "node-gyp rebuild"\` failed with 1
    
      OU
  * npm ERR! [modulename@version] preinstall: \`make || gmake\`

## <a name="additional-resources"></a>Ressources supplémentaires
* [Documentation Git](http://git-scm.com/documentation)
* [Documentation du projet Kudu](https://github.com/projectkudu/kudu/wiki)
* [TooAzure de déploiement d’un Service d’applications](app-service-continuous-deployment.md)
* [Comment toouse PowerShell pour Azure](/powershell/azure/overview)
* [Comment toouse hello Interface de ligne de commande de Azure](../cli-install-nodejs.md)

[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Azure Portal]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Interface de ligne de commande Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
