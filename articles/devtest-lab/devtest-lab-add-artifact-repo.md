---
title: "aaaAdd un laboratoire de tooa du référentiel Git dans Azure DevTest Labs | Documents Microsoft"
description: "Ajouter un dépôt GitHub ou Visual Studio Team Services Git pour vos sources d’artefacts personnalisés dans Azure DevTest Labs"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 01b459f7-eaf2-45a8-b4b5-2c0a821b33c8
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: tarcher
ms.openlocfilehash: e590559ffb2d497e39823e35c3f66974f42f13c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-git-repository-toostore-custom-artifacts-and-azure-resource-manager-templates"></a>Ajouter un artefacts de personnalisée toostore de référentiel Git et les modèles Azure Resource Manager

Si vous souhaitez trop[créer des artefacts personnalisés](devtest-lab-artifact-author.md) pour hello machines virtuelles dans votre laboratoire, ou [utiliser Azure Resource Manager modèles toocreate un environnement de test personnalisée](devtest-lab-create-environment-from-arm.md), vous devez également ajouter un tooinclude de référentiel Git privé les artefacts Hello ou modèles Azure Resource Manager créés par votre équipe. référentiel de Hello peut être hébergé sur [GitHub](https://github.com) ou sur [Visual Studio Team Services (VSTS)](https://visualstudio.com).

Nous avons fourni un [référentiel Github d’artefacts](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts) que vous pouvez déployer tel quel ou personnaliser pour vos laboratoires. Lorsque vous personnalisez ou créez un artefact, vous pouvez les stocker dans un référentiel public de hello : vous devez créer votre propre référentiel privé. 

Lorsque vous créez une machine virtuelle, vous pouvez enregistrer le modèle de gestionnaire de ressources Azure hello, personnalisez-le si vous le souhaitez et réutilisez-la ultérieure tooeasily créer davantage d’ordinateurs virtuels. Vous devez créer votre propre toostore dépôt privé vos modèles Azure Resource Manager.  

* toolearn toocreate un référentiel GitHub, voir [GitHub Bootcamp](https://help.github.com/categories/bootcamp/).
* toolearn toocreate un projet Team Services avec un référentiel Git, voir [connecter tooVisual Studio Team Services](https://www.visualstudio.com/get-started/setup/connect-to-visual-studio-online).

Hello capture d’écran suivante montre un exemple de la façon dont un référentiel contenant des artefacts peut se présenter dans GitHub :  
![Exemple de dépôt d’artefacts GitHub](./media/devtest-lab-add-repo/devtestlab-github-artifact-repo-home.png)

## <a name="get-hello-repository-information-and-credentials"></a>Obtenir des informations d’identification et les informations de référentiel hello
tooadd un laboratoire tooyour de référentiel, vous devez d’abord obtenir certaines informations de votre référentiel. Hello les sections suivantes vous guide tout au long de l’obtention de ces informations pour les référentiels hébergé sur GitHub et Visual Studio Team Services.

### <a name="get-hello-github-repository-clone-url-and-personal-access-token"></a>Obtenir un jeton URL de clonage du référentiel GitHub hello et d’accès personnel
URL du clone de référentiel tooget hello GitHub et le jeton d’accès personnel, procédez comme suit :

1. Parcourez la page d’accueil toohello du référentiel GitHub hello qui contient l’artefact de hello ou des définitions de modèle Azure Resource Manager.
2. Sélectionnez **Cloner ou télécharger**.
3. Hello de hello sélectionnez bouton toocopy **url de clone HTTPS** toohello Presse-papiers et enregistrez l’URL de hello pour une utilisation ultérieure.
4. Sélectionnez l’image du profil hello dans le coin supérieur droit de hello de GitHub, puis sélectionnez **paramètres**.
5. Bonjour **paramètres personnels** menu hello à gauche, sélectionnez **jetons d’accès personnels**.
6. Sélectionnez **Générer un nouveau jeton**.
7. Sur hello **nouveau jeton d’accès personnel** , entrez un **jeton description**, accepter les éléments par défaut de hello Bonjour **sélectionnez étendues**, puis choisissez **générer Jeton**.
8. Enregistrer le jeton de hello généré que vous en avez besoin plus tard.
9. Vous pouvez à présent fermer GitHub.   
10. Continuer toohello [se connecter à votre référentiel de toohello lab](#connect-your-lab-to-the-repository) section.

### <a name="get-hello-visual-studio-team-services-repository-clone-url-and-personal-access-token"></a>Obtenir un jeton URL de clonage du référentiel hello Visual Studio Team Services et d’accès personnel
URL du clone de référentiel tooget hello Visual Studio Team Services et le jeton d’accès personnel, procédez comme suit :

1. Ouvrez hello page d’accueil de votre collection d’équipe (par exemple, `https://contoso-web-team.visualstudio.com`), puis sélectionnez votre projet.
2. Sur la page d’accueil hello projet, sélectionnez **Code**.
3. URL du clone hello tooview, sur le projet de hello **Code** page, sélectionnez **Clone**.
4. Enregistrez hello URL que vous avez besoin plus tard dans ce didacticiel.
5. toocreate un jeton d’accès personnel, sélectionnez **mon profil** à partir du menu déroulant de hello utilisateur compte.
6. Sur la page d’informations de profil hello, sélectionnez **sécurité**.
7. Sur hello **sécurité** onglet, sélectionnez **ajouter**.
8. Bonjour **créer un jeton d’accès personnel** page :

   * Entrez un **Description** pour le jeton de hello.
   * Sélectionnez **180 jours** de hello **expire dans** liste.
   * Choisissez **tous les comptes accessibles** de hello **comptes** liste.
   * Choisissez hello **toutes les étendues** option.
   * Sélectionnez **Créer le jeton**.
9. Lorsque vous avez terminé, le nouveau jeton d’hello s’affiche dans hello **des jetons d’accès personnel** liste. Sélectionnez **copier le jeton**, puis enregistrez la valeur de jeton hello pour une utilisation ultérieure.
10. Continuer toohello [se connecter à votre référentiel de toohello lab](#connect-your-lab-to-the-repository) section.

## <a name="connect-your-lab-toohello-repository"></a>Se connecter à votre référentiel de toohello lab
1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
3. Dans liste hello labs, sélectionnez lab souhaité de hello.   
4. Dans le volet gauche de hello, sélectionnez **stratégies de Configuration et**.
5. Sur du laboratoire hello **stratégies de Configuration et** zone, sélectionnez **référentiels**.
6. Sur hello **référentiels** zone, sélectionnez **+ ajouter**.

    ![Bouton Ajouter un référentiel](./media/devtest-lab-add-repo/devtestlab-add-repo.png)
7. Sur hello deuxième **référentiels** , spécifiez hello informations suivantes :

   * **Nom** -Entrez un nom pour le référentiel de hello.
   * **Url de Clone GIT** -Entrez l’URL du clone hello Git HTTPS que vous avez copiée précédemment à partir de GitHub ou Visual Studio Team Services.
   * **Branche** -entrez hello branche tooget vos définitions.
   * **Jeton d’accès personnel** -Entrez le jeton d’accès personnel hello obtenu précédemment à partir de GitHub ou Visual Studio Team Services.
   * **Chemins d’accès du dossier** -Entrez au moins un dossier chemin d’accès relatif toohello clone URL qui contient votre objet ou des définitions de modèle Azure Resource Manager. Lorsque vous spécifiez un sous-répertoire, assurez-vous que tooinclude hello barre oblique dans un chemin d’accès du dossier hello.

     ![Zone Référentiels](./media/devtest-lab-add-repo/devtestlab-repo-blade.png)
8. Sélectionnez **Enregistrer**.

## <a name="next-steps"></a>Étapes suivantes
Après avoir créé votre référentiel Git privé, faire une ou les deux éléments suivants de hello, selon vos besoins :
* Magasin de votre [artefacts personnalisés](devtest-lab-artifact-author.md), qui vous permet de toocreate ultérieur nouvelles machines virtuelles.
* [Créer des environnements de multi-VM et PaaS ressources avec des modèles Azure Resource Manager](devtest-lab-create-environment-from-arm.md) puis à stocker les modèles hello dans votre référentiel privé.

Lorsque vous créez une machine virtuelle, vous pouvez vérifier que les artefacts hello ou les modèles sont ajoutés référentiel Git de tooyour. Elles sont disponibles immédiatement dans la liste de hello des artefacts ou des modèles, avec le nom hello de votre référentiel privé illustré dans la colonne hello qui spécifie la source de hello. 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="related-blog-posts"></a>Billets de blog connexes
* [Comment tootroubleshoot échec des artefacts dans Azure DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md)
* [Joindre un domaine Active Directory à l’aide d’un modèle de gestionnaire de ressources dans Azure DevTest Labs de tooexisting machine virtuelle](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)
