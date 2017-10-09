---
title: "développement de logiciels aaaAgile avec Azure App Service"
description: "Découvrez comment des applications de grande échelle de toocreate complexes avec Azure App Service d’une manière qui prend en charge le développement agile."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: c0fdb676-36a6-4738-925f-65b4835d187f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: a1c1c78cfff711774943b0235ed762f03f48fc6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="agile-software-development-with-azure-app-service"></a>Développement logiciel agile avec Azure App Service
Dans ce didacticiel, vous allez apprendre comment toocreate des applications complexes à grande échelle avec [Azure App Service](/azure/app-service/) d’une façon qui prend en charge [développement Agile](https://en.wikipedia.org/wiki/Agile_software_development). Il part du principe que vous savez comment trop[déployer des applications complexes comme prévu dans Azure](app-service-deploy-complex-application-predictably.md).

Limitations dans les processus techniques peuvent souvent constituer à elle de façon hello de réussite de l’implémentation des méthodologies agiles. Azure App Service avec des fonctionnalités telles que [publication continue](app-service-continuous-deployment.md), [environnements intermédiaires](web-sites-staged-publishing.md) (emplacements), et [analyse](web-sites-monitor.md), lorsqu’il est associé avec soin avec l’orchestration de hello et gestion du déploiement dans [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), peut être partie d’une solution idéale pour les développeurs qui adopter le développement agile.

Bonjour tableau suivant est une liste courte d’exigences associées au développement agile, et comment les services Azure permettent à chacun d’eux.

| Prérequis | Implémentation avec Azure |
| --- | --- |
| - Génération à chaque validation<br>- Génération automatique et rapide |Lorsqu’il est configuré avec le déploiement continu, Azure App Service peut générer les ressources en direct sur une branche de développement. Chaque fois que code est envoyé toohello branche, il est automatiquement généré et en cours d’exécution en direct dans Azure. |
| - Test automatique des générations |Charger les tests, les tests web, etc., peuvent être déployés avec le modèle de gestionnaire de ressources Azure hello. |
| - Effectuer des tests dans un clone de l’environnement de production |Les modèles de gestionnaire de ressources Azure peuvent être utilisé toocreate des clones de l’environnement de production Azure hello (y compris les paramètres de l’application, de modèles de chaînes de connexion, de mise à l’échelle, etc.) pour tester rapidement et de manière prévisible. |
| - Afficher aisément le résultat de la dernière génération |TooAzure de déploiement continu à partir d’un référentiel signifie que vous pouvez tester de nouveau code dans une application en temps réel immédiatement après avoir validé vos modifications. |
| -Valider branche principale de toohello tous les jours<br>- Automatiser le déploiement |Intégration continue d’une application de production avec la branche principale d’un référentiel déploie automatiquement chaque tooproduction de branche principale toohello validation et de fusion. |

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-do"></a>Procédure à suivre
Vous guide dans un workflow de développement test-étape de production typique dans l’ordre toopublish nouvelles modifications toohello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) exemple d’application, qui se compose de deux [les applications web](/services/app-service/web/), l’une est un serveur frontal (FE) et autre étant un principal de l’API Web (BE), Hello et un [base de données SQL](/services/sql-database/). Vous allez travailler avec hello suivant l’architecture de déploiement :

![](./media/app-service-agile-software-development/what-1-architecture.png)

image de hello tooput en mots :

* architecture de déploiement Hello est divisée en trois environnements distincts (ou [groupes de ressources](../azure-resource-manager/resource-group-overview.md) dans Azure), chacun avec son propre [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), [mise à l’échelle](web-sites-scale.md) paramètres, et la base de données SQL. 
* Chaque environnement peut être géré séparément. Il peut même être couvert par des abonnements différents.
* Intermédiaire et production sont implémentés en tant que les deux emplacements de hello même application de Service d’applications. branche principale de Hello est configuré pour l’intégration continue avec hello staging emplacement.
* Lorsqu’une branche de toomaster de validation est vérifiée sur hello staging emplacement (avec les données de production), hello vérifiées application intermédiaire est transférée dans l’emplacement de production hello [sans temps mort](web-sites-staged-publishing.md).

environnement de production et intermédiaire Hello est définie par modèle hello à [  *&lt;repository_root >*/ARMTemplates/ProdandStage.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/ProdAndStage.json).

Hello dev et environnements de test sont définies par modèle hello à [  *&lt;repository_root >*/ARMTemplates/Dev.json](https://github.com/azure-appservice-samples/ToDoApp/blob/master/ARMTemplates/Dev.json).

Vous utiliserez également stratégie de création de branche hello classique, avec le code de déplacement à partir de la branche de développement hello branche de test toohello, puis toohello de branche principale (remontant en qualité, c’est le cas toospeak).

![](./media/app-service-agile-software-development/what-2-branches.png) 

## <a name="what-you-need"></a>Ce dont vous avez besoin
* Un compte Azure
* Un compte [GitHub](https://github.com/)
* Interpréteur de commandes GIT (installé avec [GitHub pour Windows](https://windows.github.com/))-permet de vous toorun à la fois hello Git et PowerShell des commandes hello même session 
* Dernières informations [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)
* Présentation de la base des hello suite d’outils :
  * Déploiement de modèles [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) (voir également [Déployer une application complexe de manière prévisible dans Microsoft Azure](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Vous avez besoin une toocomplete compte Azure ce didacticiel :
> 
> * Vous pouvez [ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/) -vous obtenez des crédits vous pouvez utiliser tootry à payer des services Azure et même après leur utilisation vous pouvez conserver le compte de hello et libérer de l’utilisation des services Azure, telles que les applications Web.
> * Vous pouvez [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) : votre abonnement Visual Studio vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants.
> 
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="set-up-your-production-environment"></a>Configurer votre environnement de production
> [!NOTE]
> script Hello automatiquement utilisé dans ce didacticiel configure la publication en continu à partir de votre référentiel GitHub. Cela nécessite que vos informations d’identification GitHub sont déjà stockées dans Azure, sinon hello basée sur un script de déploiement échoue lors de la tentative de paramètres de contrôle de code source tooconfigure pour les applications web hello. 
> 
> toostore informations d’identification de votre GitHub dans Azure, créez une application web Bonjour [portail Azure](https://portal.azure.com/) et [configurer le déploiement de GitHub](app-service-continuous-deployment.md). Vous ne devez toodo ce qu’une seule fois. 
> 
> 

Dans un scénario classique de DevOps, vous avez une application qui est en cours d’exécution en direct dans Azure, et vous souhaitez tooit de modifications toomake via la publication continue. Dans ce scénario, vous avez un modèle que vous toodeploy développés, testés et de hello environnement. Vous allez le configurer dans cette section.

1. Créer votre propre branchement de hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) référentiel. Pour plus d’informations sur la création de votre branchement, consultez [Branchement dans un référentiel](https://help.github.com/articles/fork-a-repo/). Une fois votre branchement créé, il est visible dans votre navigateur.
   
    ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Ouvrez une session Git Shell. Si vous n’avez pas encore Git Shell, installez [GitHub for Windows](https://windows.github.com/) .
3. Créer un clone local de votre branche en exécutant hello de commande suivante :

        git clone https://github.com/<your_fork>/ToDoApp.git 
4. Une fois que vous avez votre clone local, accédez trop*&lt;repository_root >*\ARMTemplates et exécution hello deploy.ps1 script comme suit :
   
        .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git
5. Lorsque vous y êtes invité, tapez Bonjour voulue nom d’utilisateur et mot de passe pour l’accès de la base de données.
   
   Vous devez voir hello mise en service de la progression de plusieurs ressources d’Azure. Lorsque le déploiement terminé, script de hello lance l’application hello dans le navigateur de hello et vous donne un signal sonore convivial.
   
    ![](./media/app-service-agile-software-development/production-2-app-in-browser.png)
   
   > [!TIP]
   > Examinons  *&lt;repository_root >*\ARMTemplates\Deploy.ps1, toosee comment il génère des ressources avec des ID uniques. Vous pouvez utiliser hello même approche toocreate clone de hello déploiement même sans vous préoccuper des noms de ressources en conflit.
   > 
   > 
6. De retour dans votre session Git Shell, exécutez :
   
        .\swap –Name ToDoApp<unique_string>master
   
    ![](./media/app-service-agile-software-development/production-4-swap.png)
7. Une fois le script de hello, revenez adresse du frontale toobrowse toohello (http://ToDoApp*&lt;unique_string >*master.azurewebsites.net/) toosee hello applications exécutent en production.
8. Connectez-vous à toohello [portail Azure](https://portal.azure.com/) et examiner ce qui est créé.
   
   Vous devez être en mesure de toosee deux les applications web Bonjour même groupe de ressources, avec hello `Api` suffixe de nom de hello. Si vous examinez l’affichage hello du groupe de ressources, vous consultez également hello de base de données SQL, server, hello plan App Service et emplacements intermédiaires de hello pour les applications web hello. Parcourir les différentes ressources hello et de les comparer avec  *&lt;repository_root >*toosee \ARMTemplates\ProdAndStage.json comment ils sont configurés dans le modèle de hello.
   
    ![](./media/app-service-agile-software-development/production-3-resource-group-view.png)

Vous avez maintenant configuré environnement de production hello. Ensuite, vous serez déclencher une nouvelle application toohello de mise à jour.

## <a name="create-dev-and-test-branches"></a>Créer des branches de développement et de test
Maintenant que vous avez une application complexe en cours d’exécution en production dans Azure, vous allez apporter une application tooyour de mise à jour en fonction de la méthodologie agile. Dans cette section, vous allez créer des branches de développement et de test que vous avez besoin des mises à jour de toomake hello requis hello.

1. Environnement de test hello d’abord créer. Dans votre session d’interpréteur de commandes Git, suivante d’exécution hello commandes environnement de hello toocreate pour une nouvelle branche appelée **NewUpdate**. 
   
        git checkout -b NewUpdate
        git push origin NewUpdate 
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch NewUpdate
2. Lorsque vous y êtes invité, tapez Bonjour voulue nom d’utilisateur et mot de passe pour l’accès de la base de données. 
   
   Lorsque le déploiement terminé, script de hello lance l’application hello dans le navigateur de hello et vous donne un signal sonore convivial. Vous disposez alors d’une nouvelle branche avec son propre environnement de test. Prendre un moment tooreview un peu plus sur cet environnement de test :
   
   * Vous pouvez le créer avec n’importe quel abonnement Azure. Cela signifie l’environnement de production hello peut être gérée séparément à partir de votre environnement de test.
   * Votre environnement de test s’exécute dans Azure.
   * Votre environnement de test est un environnement de production toohello identiques, à l’exception hello mise en lots des emplacements et hello mise à l’échelle des paramètres. Vous la connaissez, car elles sont les seules différences de hello entre ProdandStage.json et.JSON.
   * Vous pouvez gérer votre environnement de test dans son propre plan App Service avec un niveau de prix différent (par exemple, **Gratuit**).
   * La suppression de cet environnement de test est aussi simple que la suppression du groupe de ressources hello. Vous trouverez comment toodo cela [ultérieurement](#delete).
3. Allez sur toocreate une branche de développement en exécutant hello suivant de commandes :
   
        git checkout -b Dev
        git push origin Dev
        .\deploy.ps1 -TemplateFile .\Dev.json -RepoUrl https://github.com/<your_fork>/ToDoApp.git -Branch Dev
4. Lorsque vous y êtes invité, tapez Bonjour voulue nom d’utilisateur et mot de passe pour l’accès de la base de données. 
   
   Prendre un moment tooreview un peu plus sur cet environnement de développement : 
   
   * Votre environnement de développement a un environnement de test configuration toohello identiques car il est déployé à l’aide de hello même modèle.
   * Chaque environnement de développement peut être créé dans l’abonnement Azure hello du développeur, en laissant toobe d’environnement de test hello géré séparément.
   * Votre environnement de développement s’exécute dans Azure.
   * La suppression de hello dev environnement est aussi simple que la suppression du groupe de ressources hello. Vous trouverez comment toodo cela [ultérieurement](#delete).

> [!NOTE]
> Lorsque vous avez plusieurs développeurs travaillent sur la nouvelle mise à jour de hello, chacun d’eux peut facilement créer une branche et l’environnement de développement dédié avec hello comme suit :
> 
> 1. Créer leur propres branche du référentiel de hello dans GitHub (consultez [une branche dans un référentiel](https://help.github.com/articles/fork-a-repo/)).
> 2. Cloner le branchement hello sur leur ordinateur local
> 3. Exécutez hello même commandes toocreate leur propre environnement et la branche dev.
> 
> 

Lorsque vous avez terminé, votre branchement GitHub doit comporter trois branches :

![](./media/app-service-agile-software-development/test-1-github-view.png)

Vous devez disposer de six applications web (trois ensembles de deux applications) dans les trois groupes de ressources distincts :

![](./media/app-service-agile-software-development/test-2-all-webapps.png)

> [!NOTE]
> ProdandStage.json spécifie Bonjour production environnement toouse Bonjour **Standard** tarification, ce qui est approprié pour l’évolutivité de l’application de production hello.
> 
> 

## <a name="build-and-test-every-commit"></a>Générer et tester chaque validation
Bonjour les fichiers de modèle ProdAndStage.json et.JSON déjà spécifier les paramètres de contrôle de source de hello, qui par défaut définit la publication en continu pour l’application web de hello. Par conséquent, chaque branche de GitHub toohello validation déclenche un tooAzure de déploiement automatique de cette branche. Nous allons à présent découvrir le fonctionnement de votre configuration.

1. Assurez-vous que vous êtes dans la branche de développement hello du référentiel local de hello. toodo, exécution hello commande dans Git Shell suivante :
   
        git checkout Dev
2. Rendre couche d’interface utilisateur de l’application de toohello une modification en modifiant hello code toouse [Bootstrap](http://getbootstrap.com/components/) répertorie. Ouvrez  *&lt;repository_root >*\src\MultiChannelToDo.Web\index.cshtml et apportez hello après modification de la mise en surbrillance :
   
    ![](./media/app-service-agile-software-development/commit-1-changes.png)
   
    > [!NOTE]
    > Si vous ne pouvez pas lire hello image précédente : 
    > 
    > * Dans la ligne 18, modifiez `check-list` trop`list-group`.
    > * Dans la ligne 19, modifiez `class="check-list-item"` trop`class="list-group-item"`.
    > 
    > 
3. Enregistrez les modifications hello. Sauvegarder dans l’interpréteur de commandes Git, exécutez hello suivant de commandes :
   
        cd <repository_root>
        git add .
        git commit -m "changed toobootstrap style"
        git push origin Dev
   
   Ces commandes git sont similaires trop « vérification dans votre code » dans un autre système de contrôle de source, tel que TFS. Lorsque vous exécutez `git push`, validation de nouveau hello déclenche un tooAzure push de code automatique, les reconstructions puis hello application tooreflect hello modification dans l’environnement de développement hello.
4. tooverify cet environnement de développement de code push tooyour s’est produite, consultez la page d’application web de l’environnement de développement tooyour et examinez hello **déploiement** partie. Vous devez être en mesure de toosee votre dernière validation de message il.
   
    ![](./media/app-service-agile-software-development/commit-2-deployed.png)
5. À partir de là, cliquez sur **Parcourir** toosee hello nouvelle modification dans l’application en temps réel de hello dans Azure.
   
    ![](./media/app-service-agile-software-development/commit-3-webapp-in-browser.png)
   
   Il s’agit d’une application de toohello modification mineure. Toutefois, de nombreux heures modifications tooa complexes une application web ont des effets inattendus et indésirables. En cours de test de tooeasily en mesure de chaque validation dans les versions en direct permet de vous toocatch ces problèmes avant de les afficher par vos clients.

À ce stade, vous devez être familiarisé avec la réalisation de hello qui, en tant que développeur sur hello **NewUpdate** projet, vous pouvez créer un environnement de développement pour vous-même, puis générer chaque validation et tester chaque build.

## <a name="merge-code-into-test-environment"></a>Fusionner le code dans l’environnement de test
Lorsque vous êtes prêt toopush votre code à partir de développement branche tooNewUpdate branche, elle consiste à hello git standard :

1. Fusionner toutes les nouvelles tooNewUpdate de validations dans la branche de développement hello dans GitHub, tels que des validations créés par d’autres développeurs. Toute nouvelle validation sur GitHub déclenche un push de code et de la build dans l’environnement de développement hello. Vous pouvez vérifiez que votre code dans la branche Dev fonctionne toujours avec les éléments les plus récents à partir de la branche de NewUpdate hello.
2. Fusionnez toutes vos nouvelles validations entre la branche Dev et la branche NewUpdate dans GitHub. Cette action déclenche un push de code et de la build dans l’environnement de test hello. 

Notez à nouveau que parce que le déploiement continu est déjà configuré avec ces branches git, vous n’avez pas besoin tootake génère de toute autre action, comme l’intégration en cours d’exécution. Vous devez simplement des méthodes de contrôle de source standard tooperform à l’aide de git et Azure effectue tous les processus de génération hello pour vous.

Maintenant, nous allons push trop votre code**NewUpdate** branche. Dans l’interpréteur de commandes Git, exécutez hello suivant de commandes :

    git checkout NewUpdate
    git pull origin NewUpdate
    git merge Dev
    git push origin NewUpdate

Et voilà ! 

Page de l’application web accédez toohello pour votre toosee d’environnement de test de votre nouvelle validation (fusionnée dans NewUpdate branche) envoyées maintenant environnement de test toohello. Ensuite, cliquez sur **Parcourir** toosee qui hello changement de style est en cours d’exécution en direct dans Azure.

## <a name="deploy-update-tooproduction"></a>Déployer la mise à jour tooproduction
Environnement intermédiaire et de production en exécutant un push de code toohello n’êtes pas différente de ce que vous avez déjà fait lors de l’environnement de test de code toohello transmis en push. Cette opération est très simple. 

Dans l’interpréteur de commandes Git, exécutez hello suivant de commandes :

    git checkout master
    git pull origin master
    git merge NewUpdate
    git push origin master

N’oubliez pas que selon la façon hello environnement intermédiaire et de production de hello est défini dans ProdandStage.json, votre nouveau code est transmise toohello **intermédiaire** emplacement et il exécute. Par conséquent, si vous accédez à URL l’emplacement intermédiaire toohello, vous consultez hello nouveau code en cours d’exécution il. toodo, exécution hello suivant l’applet de commande de l’interpréteur de commandes Git.

    Start-Process -FilePath "http://ToDoApp<unique_string>master-Staging.azurewebsites.net"

Et maintenant, une fois que vous avez vérifié la mise à jour hello Bonjour staging emplacement, hello seule chose qui reste toodo est tooswap en production. Dans l’interpréteur de commandes Git, il suffit d’exécuter hello suivant les commandes :

    cd <repository_root>\ARMTemplates
    .\swap.ps1 -Name ToDoApp<unique_string>master

Félicitations ! Vous avez correctement publié une nouvelle application web mise à jour tooyour production. De plus, vous y êtes parvenu en créant aisément des environnements de développement et de test et en générant et en testant chaque validation. Ces étapes sont essentielles pour le développement logiciel agile.

<a name="delete"></a>

## <a name="delete-dev-and-test-environments"></a>Supprimer des environnements de développement et de test
Étant donné que vous avez conçu volontairement votre développement et groupes de ressources autonomes toobe environnements de test, il est facile toodelete les. toodelete hello ceux que vous avez créé dans ce didacticiel, les branches de GitHub hello et des artefacts Azure, exécutez simplement hello suivant les commandes dans l’interpréteur de commandes Git :

    git branch -d Dev
    git push origin :Dev
    git branch -d NewUpdate
    git push origin :NewUpdate
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>dev-group -Force -Verbose
    Remove-AzureRmResourceGroup -Name ToDoApp<unique_string>newupdate-group -Force -Verbose

## <a name="summary"></a>Résumé
Développement Agile est indispensable pour de nombreuses entreprises qui veulent tooadopt Azure en tant que leur plate-forme d’application. Dans ce didacticiel, vous avez appris comment toocreate et son réplicas exactes ou près de réplicas de hello environnement de production en toute simplicité, même pour les applications complexes. Vous avez également appris comment tooleverage traiter cette toocreate permet un développement qui peut générer et tester chaque validation simple dans Azure. Ce didacticiel vous a espère montré comment mieux utiliser Azure App Service et Azure Resource Manager toocreate ensemble une solution DevOps qui gère les méthodologies tooagile. À présent, vous pouvez tirer parti de ce scénario en recourant à des techniques DevOps avancées telles que le [test dans les environnements de production](app-service-web-test-in-production-get-start.md). Pour découvrir un scénario courant de test dans les environnements de production, consultez [Déploiement avec distribution d’une version d’évaluation (test bêta) dans Azure App Service](app-service-web-test-in-production-controlled-test-flight.md).

## <a name="more-resources"></a>Autres ressources
* [Déployer une application complexe de manière prévisible dans Microsoft Azure](app-service-deploy-complex-application-predictably.md)
* [Développement Agile en pratique : trucs et astuces pour le cycle de développement moderne](http://channel9.msdn.com/Events/Ignite/2015/BRK3707)
* [Stratégies de déploiement avancées pour les applications web Azure à l’aide des modèles Resource Manager](http://channel9.msdn.com/Events/Build/2015/2-620)
* [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - hello validateur JSON](http://jsonlint.com/)
* [ARMClient – configurer toosite de publication de GitHub](https://github.com/projectKudu/ARMClient/wiki/Setup-GitHub-publishing-to-Site)
* [Création de branches Git – Branchement et fusion basiques](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Blog de David Ebbo](http://blog.davidebbo.com/)
* [Azure PowerShell](/powershell/azure/overview)
* [Outils en ligne de commande multiplateforme Azure](../cli-install-nodejs.md)
* [Création ou modification des utilisateurs dans Azure AD](https://msdn.microsoft.com/library/azure/hh967632.aspx#BKMK_1)
* [Projet Wiki Kudu](https://github.com/projectkudu/kudu/wiki)

