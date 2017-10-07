---
title: aaaCreate un serveur Jenkins sur Azure
description: "Installer Jenkins sur une machine virtuelle de Azure Linux à partir du modèle de solution Jenkins hello et générer un exemple d’application Java."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a>Créer un serveur Jenkins sur une machine virtuelle Linux de Azure à partir de hello portail Azure

Ce démarrage rapide montre comment tooinstall [Jenkins](https://jenkins.io) sur une machine virtuelle Ubuntu Linux avec les outils de hello et de plug-ins configurés toowork avec Azure. Lorsque vous avez terminé, vous disposez d’un serveur de Jenkins s’exécutant dans Azure qui génère un exemple d’application Java à partir de [Github](https://github.com).

## <a name="prerequisites"></a>Composants requis

* Un abonnement Azure
* TooSSH d’accès sur la ligne de commande de votre ordinateur (par exemple hello Bash shell ou [PuTTY](http://www.putty.org/))

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a>Créer hello Jenkins VM à partir du modèle de solution hello

Ouvrez hello [une image marketplace pour Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) dans votre navigateur web, puis sélectionnez **GET IT maintenant** à partir de la partie gauche de la page de hello hello. Hello révision prix et sélectionnez **continuer**, puis sélectionnez **créer** serveur Jenkins tooconfigure hello hello portail Azure. 
   
![Boîte de dialogue du Portail Azure](./media/install-jenkins-solution-template/ap-create.png)

Bonjour **configurer les paramètres de base** onglet, renseignez hello champs qui suivent :

![Configurer les paramètres de base](./media/install-jenkins-solution-template/ap-basic.png)

* Utilisez **Jenkins** comme **Nom**.
* Entrez un **Nom d’utilisateur**. nom d’utilisateur Hello doit répondre aux [aux exigences](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).
* Sélectionnez **mot de passe** comme hello **type d’authentification** et entrez un mot de passe. Hello le mot de passe doit contenir une lettre majuscule, un nombre et un caractère spécial.
* Utilisez **myJenkinsResourceGroup** pour hello **groupe de ressources**.
* Choisissez hello **États-Unis** [région Azure](https://azure.microsoft.com/regions/) de hello **emplacement** liste déroulante.

Sélectionnez **OK** tooproceed toohello **configurer des options supplémentaires** onglet. Entrez un nom unique de domaine nom tooidentify hello Jenkins et sélectionnez **OK**.

![Configurer des options supplémentaires](./media/install-jenkins-solution-template/ap-addtional.png)  

 Une fois la validation réussit, sélectionnez **OK** à partir de hello **Résumé** onglet. Enfin, sélectionnez **achat** toocreate hello Jenkins VM. Lorsque votre serveur est prêt, vous recevez une notification Bonjour portail Azure :   

![Notification Jenkins est prêt](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a>Se connecter tooJenkins

Accédez tooyour virtual machine (par exemple, http://jenkins2517454.eastus.cloudapp.azure.com/) dans votre navigateur web. console de Jenkins Hello n’est pas accessible via le protocole HTTP non sécurisé afin de vous trouverez des instructions sur la console de Jenkins hello page tooaccess hello en toute sécurité à partir de votre ordinateur à l’aide d’un tunnel SSH.

![Déverrouiller Jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

Configurer tunnel hello à l’aide de hello `ssh` commande page hello à partir de la ligne de commande hello, en remplaçant `username` avec le nom d’utilisateur d’administrateur de machine virtuelle hello choisi précédemment lors de la configuration d’ordinateur virtuel de hello à partir de modèle de solution hello de hello.

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

Une fois que vous avez démarré le tunnel de hello, accédez toohttp://localhost:8080 / sur votre ordinateur local. 

Obtenir le mot de passe initial de hello en exécutant hello commande dans la ligne de commande hello tout en étant connecté via SSH toohello Jenkins VM suivante.

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

Déverrouillage du tableau de bord Jenkins hello pour hello première fois à l’aide de ce mot de passe initial.

![Déverrouiller Jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

Sélectionnez **installer le plug-ins suggérées** sur hello page suivante, puis créez un Jenkins administrateur de l’utilisateur utilisées tooaccess hello Jenkins du tableau de bord.

![Jenkins est prêt à l’emploi](./media/install-jenkins-solution-template/jenkins-welcome.png)

Hello Jenkins serveur est maintenant prêt toobuild code.

## <a name="create-your-first-job"></a>Créer votre premier travail

Sélectionnez **créer de nouveaux travaux** à partir de la console de Jenkins hello, puis nommez-le **mySampleApp** et sélectionnez **projet Freestyle**, puis sélectionnez **OK**.

![Créer un travail](./media/install-jenkins-solution-template/jenkins-new-job.png) 

Sélectionnez hello **gestion du Code Source** onglet, activez **Git**, puis entrez hello suivant des URL dans **URL du référentiel** champ :`https://github.com/spring-guides/gs-spring-boot.git`

![Définir le référentiel Git de hello](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

Sélectionnez hello **générer** , puis sélectionnez **étape de génération ajouter**, **Gradle d’appel de script**. Sélectionnez **Utiliser Gradle Wrapper**, puis entrez `complete` dans l’**emplacement de Wrapper** et `build` pour **Tâches**.

![Utilisez hello Gradle wrapper toobuild](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

Sélectionnez **Avancé..** puis entrez `complete` Bonjour **racine générer un script** champ. Sélectionnez **Enregistrer**.

![Définir les paramètres avancés dans l’étape de génération de wrapper Gradle hello](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a>Générer du code de hello

Sélectionnez **générer maintenant** toocompile hello code et le package hello exemple d’application. Lorsque votre build est terminée, sélectionnez hello **espace de travail** lien pour le projet de hello.

![Parcourir le fichier toohello espace de travail tooget hello JAR à partir de la génération de hello](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

Accédez trop`complete/build/libs` et vérifiez que hello `gs-spring-boot-0.1.0.jar` existe-t-il tooverify que votre build a réussi. Votre Jenkins serveur est maintenant prêt à toobuild vos projets dans Azure.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Ajouter des machines virtuelles Azure en tant qu’agents Jenkins](jenkins-azure-vm-agents.md)
