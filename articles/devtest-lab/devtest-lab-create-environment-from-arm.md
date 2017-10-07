---
title: "aaaCreate les environnements de multi-VM et ressources PaaS avec les modèles Azure Resource Manager | Documents Microsoft"
description: "Découvrez comment toocreate les environnements de multi-VM et ressources PaaS dans Azure DevTest Labs à partir d’un modèle Azure Resource Manager"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: tarcher
ms.openlocfilehash: ab8628f6cb5a666435258efb93921ec69ad3a13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a>Créer des environnements de plusieurs machines virtuelles et des ressources PaaS avec les modèles Azure Resource Manager

Hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) vous permet de tooeasily [créer et ajouter un laboratoire tooa de machine virtuelle](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm). Cela fonctionne bien pour la création d’une machine virtuelle à la fois. Toutefois, si l’environnement de hello contient plusieurs ordinateurs virtuels, chaque machine virtuelle a toobe créée individuellement. Pour des scénarios tels que l’application Web à plusieurs niveaux ou une batterie de serveurs SharePoint, un mécanisme est tooallow nécessaire pour la création de hello de plusieurs machines virtuelles en une seule étape. À l’aide de modèles Azure Resource Manager, vous pouvez maintenant définir l’infrastructure de hello et la configuration de votre solution Windows Azure et à plusieurs reprises déployer plusieurs machines virtuelles dans un état cohérent. Cette fonctionnalité fournit hello avantages suivants :

- Les modèles Azure Resource Manager sont chargés directement à partir de votre dépôt de contrôle de code source (GitHub ou Team Services Git).
- Une fois configuré, vos utilisateurs peuvent créer un environnement en choisissant un modèle Azure Resource Manager à partir de hello portail Azure comme ils réalisables avec d’autres types de [bases de machine virtuelle](./devtest-lab-comparing-vm-base-image-types.md).
- Ressources PaaS Azure peuvent être configurées dans un environnement à partir d’un modèle Azure Resource Manager dans Ajout tooIaaS machines virtuelles.
- permet de suivre coût Hello des environnements lab hello dans Ajout tooindividual machines virtuelles créées par d’autres types de bases.
- Ressources de PaaS sont créés et apparaîtront dans le coût de suivi ; Toutefois, arrêt automatique de machine virtuelle ne s’applique pas les ressources tooPaaS.
- Les utilisateurs ont hello même contrôle de stratégie de machine virtuelle pour les environnements d’avoir des ordinateurs virtuels de lab-unique.

En savoir plus sur hello nombreux [avantages de l’utilisation de modèles de gestionnaire de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager) toodeploy, mettre à jour ou supprimer toutes vos ressources lab en une seule opération.

> [!NOTE]
> Lorsque vous utilisez un modèle de gestionnaire de ressources comme une base toocreate lab plusieurs machines virtuelles, il existe certaines différences tookeep n’oubliez pas que vous créiez Multi-machines virtuelles ou des machines virtuelles de l’unique. La rubrique « Utiliser un modèle Resource Manager de machine virtuelle » explique ces différences en détail.
>
>

## <a name="configure-azure-resource-manager-template-repositories"></a>Configurer les dépôts du modèle Azure Resource Manager

Comme une des meilleures pratiques de hello avec le code en tant qu’infrastructure et en tant que code de configuration, les modèles d’environnement doit être gérée dans le contrôle de code source. Azure DevTest Labs suit cette pratique et charge tous les modèles Azure Resource Manager directement à partir de vos dépôts GitHub ou VSTS Git. Par conséquent, les modèles de gestionnaire de ressources peuvent être utilisés le cycle de mise en production entier hello, à partir de hello test toohello environnement de production.

Il existe quelques règles toofollow tooorganize vos modèles Azure Resource Manager dans un référentiel :

- fichier de modèle principal Hello doit être nommé `azuredeploy.json`. 

    ![Fichiers de modèle Azure Resource Manager clés](./media/devtest-lab-create-environment-from-arm/master-template.png)

- Si vous souhaitez que les valeurs de paramètre toouse définies dans un fichier de paramètres, le fichier de paramètres hello doit être nommé `azuredeploy.parameters.json`.
- Vous pouvez utiliser les paramètres hello `_artifactsLocation` et `_artifactsLocationSasToken` tooconstruct hello parametersLink valeur de l’URI, ce qui permet de DevTest Labs tooautomatically gérer les modèles imbriqués. Pour plus d’informations, consultez [How Azure DevTest Labs makes nested Resource Manager template deployments easier for testing environments](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/).
- Les métadonnées peuvent être description et nom d’affichage modèle défini toospecify hello. Ces métadonnées doivent être dans un fichier nommé `metadata.json`. Hello exemple de fichier de métadonnées suivant illustre comment toospecify hello afficher le nom et la description : 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of hello template>"
 
}
```

Hello suit guide par l’ajout d’un laboratoire de tooyour référentiel à l’aide de hello portail Azure. 

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
1. Dans liste hello labs, sélectionnez lab souhaité de hello.   
1. Dans le panneau de hello lab, sélectionnez **stratégies de Configuration et**.

    ![Configuration et stratégies](./media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. À partir de hello **stratégies de Configuration et** liste de paramètres, sélectionnez **référentiels**. Hello **référentiels** panneau répertorie les référentiels hello qui ont été ajoutés toohello lab. Un référentiel appelé `Public Repo` est généré automatiquement pour tous les ateliers pratiques et se connecte toohello [référentiel DevTest Labs GitHub](https://github.com/Azure/azure-devtestlab) qui contient plusieurs artefacts de machine virtuelle pour votre usage.

    ![Dépôt public](./media/devtest-lab-create-environment-from-arm/public-repo.png)

1. Sélectionnez **ajouter +** tooadd votre référentiel de modèle Azure Resource Manager.
1. Lorsque hello deuxième **référentiels** s’ouvre le panneau, entrez les informations nécessaires hello comme suit :
    - **Nom** -Entrez le nom de référentiel hello qui est utilisé dans le laboratoire de hello.
    - **URL de clone GIT** -Entrez l’URL de clone HTTPS GIT hello GitHub ou Visual Studio Team Services.  
    - **Branche** -entrez hello branche nom tooaccess vos définitions de modèle Azure Resource Manager. 
    - **Jeton d’accès personnel** -sert de jeton d’accès personnel hello toosecurely accéder à votre référentiel. sélectionner de votre jeton à partir de Visual Studio Team Services, tooget  **&lt;votrenom >> Mon profil > sécurité > jeton d’accès Public**. tooget votre jeton à partir de GitHub, sélectionnez votre avatar suivi en sélectionnant **Paramètres > jeton d’accès Public**. 
    - **Chemins d’accès du dossier** : l’un des champs d’entrée de hello deux, entrez les chemin d’accès du dossier hello qui commence par une barre oblique - / - et est tooyour relatif Git clone URI tooeither vos définitions d’artefact (premier champ d’entrée) ou votre modèle Azure Resource Manager définitions.   
    
        ![Dépôt public](./media/devtest-lab-create-environment-from-arm/repo-values.png)

1. Une fois que tous les champs hello requis sont entrés et passé la validation de hello, sélectionnez **enregistrer**.

section suivante de Hello vous guidera dans la création d’environnements à partir d’un modèle Azure Resource Manager.

## <a name="create-an-environment-from-an-azure-resource-manager-template"></a>Créer un environnement à partir d’un modèle Azure Resource Manager

Une fois qu’un référentiel de modèle Azure Resource Manager a été configuré dans le laboratoire de hello, vos utilisateurs lab peuvent créer un environnement à l’aide du portail Azure par hello comme suit :

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
1. Dans liste hello labs, sélectionnez lab souhaité de hello.   
1. Dans le panneau de hello lab, sélectionnez **ajouter +**.
1. Hello **choisir une base** panneau affiche les images de base hello vous pouvez utiliser avec les modèles Azure Resource Manager hello répertoriées en premier. Sélectionnez hello souhaité modèle Azure Resource Manager.

    ![Choisir une base](./media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. Sur hello **ajouter** panneau, entrez hello **nom de l’environnement** valeur. nom de l’environnement Hello est Nouveautés utilisateurs tooyour affichées dans le laboratoire de hello. champs d’entrée de Hello restants sont définies dans le modèle de gestionnaire de ressources Azure hello. Si les valeurs par défaut sont définis dans le modèle de hello ou hello `azuredeploy.parameter.json` fichier est présent, les valeurs par défaut sont affichées dans les champs d’entrée. Pour les paramètres de type *chaîne sécurisée*, vous pouvez utiliser des clés secrètes de hello stockées dans le lab hello [personnel magasin des secrets](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).

    ![Ajouter un panneau](./media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > Il existe plusieurs valeurs de paramètres, même quand elles sont spécifiées, qui sont affichées sous forme de valeurs vides. Par conséquent, si les utilisateurs affecter ces tooparameters de valeurs dans un modèle Azure Resource Manager, DevTest Labs n’affiche pas les valeurs hello ; au lieu de cela indiquant a des champs d’entrée vides dans lequel les utilisateurs du laboratoire hello doivent tooenter une valeur lors de la création d’environnement de hello.
    > 
    > - GEN-UNIQUE
    > - GEN-UNIQUE-[N]
    > - GEN-SSH-PUB-KEY
    > - GEN-PASSWORD 
 
1. Sélectionnez **ajouter** environnement de hello toocreate. environnement de Hello démarre immédiatement l’approvisionnement avec l’état hello affichage Bonjour **mes machines virtuelles** liste. Un groupe de ressources est automatiquement créé par hello lab tooprovision toutes les ressources hello définis dans le modèle de gestionnaire de ressources Azure hello.
1. Après la création de l’environnement de hello, sélectionnez l’environnement de hello Bonjour **mes machines virtuelles** liste panneau des groupe de ressources tooopen hello et parcourir toutes les ressources hello configurés dans l’environnement de hello.
    
    ![Liste Mes machines virtuelles](./media/devtest-lab-create-environment-from-arm/all-environment-resources.png)
   
   Vous pouvez également développer la liste de hello simplement tooview hello environnement d’ordinateurs virtuels qui sont configurés dans l’environnement de hello.
    
    ![Liste Mes machines virtuelles](./media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. Cliquez sur un des hello environnements tooview hello actions disponibles - telles que l’application des artefacts, attacher des disques de données, modification temps d’arrêt automatique et bien plus encore.

    ![Actions de l’environnement](./media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="next-steps"></a>Étapes suivantes
* Une fois qu’un ordinateur virtuel a été créé, vous pouvez vous connecter toohello machine virtuelle en sélectionnant **Connect** sur le panneau de la machine virtuelle hello.
* Afficher et gérer des ressources dans un environnement en sélectionnant l’environnement de hello Bonjour **mes machines virtuelles** liste dans votre laboratoire. 
* Explorer hello [modèles Azure Resource Manager à partir de la galerie de modèles de démarrage rapide d’Azure](https://github.com/Azure/azure-quickstart-templates)
