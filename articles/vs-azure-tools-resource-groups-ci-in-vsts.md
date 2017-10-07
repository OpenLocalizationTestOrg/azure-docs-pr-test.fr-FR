---
title: "intégration aaaContinuous dans Visual Studio Team Services à l’aide de projets de groupe de ressources Azure | Documents Microsoft"
description: "Décrit comment les projets tooset créer une intégration continue dans Visual Studio Team Services à l’aide de déploiement de groupe de ressources Azure dans Visual Studio."
services: visual-studio-online
documentationcenter: na
author: mlearned
manager: erickson-doug
editor: 
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: 0fe4a4b8989ee323e8ef2206fa4ebed503025670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a>Intégration continue dans Visual Studio Team Services à l’aide de projets de déploiement de groupe de ressources Azure
toodeploy un modèle Azure, vous effectuez des tâches dans différents stades : créer, de Test, tooAzure de copie (également appelé « Étape intermédiaire ») et le modèle de déploiement. Il existe deux façons différentes toodeploy modèles tooVisual Studio Team Services (Visual Studio Team Services). Les deux méthodes fournissent hello mêmes résultats, appuyez sur hello qui répond le mieux à votre flux de travail.

1. Ajouter une définition de build tooyour seule étape qui exécute le script PowerShell hello qui est inclus dans le projet de déploiement de groupe de ressources Azure hello (Deploy-azureresourcegroup.ps1). script de Hello copie des artefacts et déploie ensuite le modèle de hello.
2. Ajouter plusieurs étapes de build à Visual Studio Team Services, chacune effectuant une tâche intermédiaire.

Cet article présente les deux options. option de première Hello a parti hello utilisant hello script utilisé par les développeurs dans Visual Studio et la spécification de cohérence tout au long du cycle de vie hello. Hello offre un script intégré toohello autre pratique. Les deux procédures partent du principe que vous disposez déjà d’un projet de déploiement Visual Studio contrôlé dans Visual Studio Team Services.

## <a name="copy-artifacts-tooazure"></a>Copiez les artefacts tooAzure
Quel que soit le scénario de hello, si vous disposez de tous les artefacts qui sont nécessaires pour le déploiement de modèle, vous devez donner toothem d’accès Azure Resource Manager. Ces artefacts peuvent inclure des fichiers tels que :

* des modèles imbriqués
* des scripts de configuration et DSC
* fichiers binaires d’application

### <a name="nested-templates-and-configuration-scripts"></a>Modèles imbriqués et les scripts de configuration
Lorsque vous utilisez des modèles de hello fournis par Visual Studio (ou générée à l’aide des extraits de code Visual Studio), hello script PowerShell ne prépare pas uniquement les artefacts hello, il est également hello URI pour les ressources hello de différents déploiements. Hello script puis copie le conteneur de hello artefacts tooa sécurisé dans Azure, crée un jeton SAP pour ce conteneur et puis il transmet ces informations sur le déploiement d’un modèle toohello. Consultez [créer un modèle de déploiement](https://msdn.microsoft.com/library/azure/dn790564.aspx) toolearn savoir plus sur les modèles imbriqués.  Lorsque vous utilisez des tâches dans Visual Studio Team Services, vous devez sélectionner les tâches appropriées hello pour votre déploiement de modèle et si nécessaire, passer des valeurs de paramètre hello étape toohello modèle déploiement intermédiaire.

## <a name="set-up-continuous-deployment-in-vs-team-services"></a>Configurer le déploiement continu dans Visual Studio Team Services
toocall le script PowerShell hello dans Visual Studio Team Services, vous devez tooupdate votre définition de build. En bref, les étapes de hello sont : 

1. Modifier la définition de build hello.
2. la définition de l’autorisation Azure dans Visual Studio Team Services.
3. Ajoutez une étape de génération d’Azure PowerShell qui fait référence à script PowerShell de hello dans le projet de déploiement de groupe de ressources Azure hello.
4. La valeur hello Hello *- ArtifactsStagingDirectory* toowork de paramètre avec un projet créé dans Visual Studio Team Services.

### <a name="detailed-walkthrough-for-option-1"></a>Procédure pas à pas pour l’option 1
Hello procédures suivantes vous guident tout déploiement continu nécessaire tooconfigure étapes hello dans Visual Studio Team Services à l’aide d’une tâche qui exécute le script PowerShell de hello dans votre projet. 

1. Modifiez votre définition de build de Visual Studio Team Services et ajoutez une étape de build Azure PowerShell. Choisissez la définition de build hello sous hello **des définitions de Build** catégorie, puis choisissez hello **modifier** lien.
   
   ![Modifier la définition de build][0]
2. Ajouter un nouveau **Azure PowerShell** étape toohello build définition de build, puis choisissez hello **étape de génération ajouter...** .
   
   ![Ajouter une étape de génération][1]
3. Choisissez hello **tâche Deploy** catégorie, sélectionnez hello **Azure PowerShell** de tâches, puis son **ajouter** bouton.
   
   ![Ajouter des tâches][2]
4. Choisissez hello **Azure PowerShell** étape de génération et puis remplir ses valeurs.
   
   1. Si vous disposez déjà d’un point de terminaison de service Azure ajouté tooVS Team Services, choisissez un abonnement de hello Bonjour **abonnement Azure** zone de liste déroulante, puis ignorer toohello prochaine section. 
      
      Si vous n’avez pas un point de terminaison de service Azure dans Visual Studio Team Services, vous devez tooadd une. Cette sous-section vous guide tout au long des processus de hello. Si votre compte Azure utilise un compte Microsoft (tel que Hotmail), vous devez prendre hello suivant les étapes tooget un Principal du Service d’authentification.
   2. Choisissez hello **gérer** lien suivant toohello **abonnement Azure** zone de liste déroulante.
      
      ![Gérer les abonnements Azure][3]
   3. Choisissez **Azure** Bonjour **nouveau point de terminaison de Service** zone de liste déroulante.
      
      ![Nouveau point de terminaison de service][4]
   4. Bonjour **ajouter un abonnement Azure** boîte de dialogue, sélectionnez hello **Principal du Service** option.
      
      ![Option du principal de service][5]
   5. Ajouter votre toohello de plus d’informations d’abonnement Azure **ajouter un abonnement Azure** boîte de dialogue. Vous devez hello tooprovide éléments suivants :
      
      * ID d’abonnement
      * Nom d'abonnement
      * ID de principal de service
      * Clé de principal de service
      * ID client
   6. Ajouter un nom de votre choix de toohello **abonnement** zone Nom. Cette valeur s’affiche plus loin dans hello **abonnement Azure** liste déroulante dans Visual Studio Team Services. 
   7. Si vous ne connaissez pas votre ID d’abonnement Azure, vous pouvez utiliser une des hello suivant de commandes tooretrieve il.
      
      Pour les scripts PowerShell, utilisez :
      
      `Get-AzureRmSubscription`
      
      Pour l’interface de ligne de commande Azure, consultez :
      
      `azure account show`
   8. tooget un ID de Principal du Service, clé de Principal du Service et l’ID de locataire, suivez la procédure hello dans [application créer Active Directory et principal du service à l’aide du portail](resource-group-create-service-principal-portal.md) ou [l’authentification d’un principal de service avec Le Gestionnaire de ressources Azure](resource-group-authenticate-service-principal.md).
   9. Ajouter hello toohello de valeurs ID de Principal du Service, clé de Principal du Service et ID de client **ajouter un abonnement Azure** boîte de dialogue zone, puis choisissez hello **OK** bouton.
      
      Vous avez maintenant un Bonjour de toorun toouse de Principal du Service valide script Azure PowerShell.
5. Modifier la définition de build hello et choisissez hello **Azure PowerShell** étape de génération. Sélectionnez l’abonnement de hello Bonjour **abonnement Azure** zone de liste déroulante. (Si l’abonnement de hello n’apparaît pas, choisissez hello **Actualiser** hello suivant du bouton **gérer** lien.) 
   
   ![Configurer une tâche de génération Azure PowerShell][8]
6. Fournir un chemin d’accès de toohello script Deploy-azureresourcegroup.ps1 PowerShell. toodo, choisissez toohello suivant du bouton points de suspension (...) hello **chemin d’accès du Script** , accédez toohello Deploy-azureresourcegroup.ps1 PowerShell script hello **Scripts** dossier de votre projet, sélectionnez-le, puis choisissez hello **OK** bouton.    
   
   ![Sélectionnez le chemin d’accès tooscript][9]
7. Après avoir sélectionné le script de hello, mettre à jour hello chemin d’accès toohello script afin qu’il est exécuté à partir de hello Build.StagingDirectory (hello même répertoire que *ArtifactsLocation* a la valeur). Ce faire, vous pouvez ajouter « $(Build.StagingDirectory)/ « toohello début du chemin d’accès du script hello.
   
    ![Modifier le chemin d’accès tooscript][10]
8. Bonjour **Arguments de Script** , entrez hello suivant les paramètres (dans une seule ligne). Lorsque vous exécutez le script de hello dans Visual Studio, vous pouvez voir comment les utilisations VS hello paramètres Bonjour **sortie** fenêtre. Vous pouvez utiliser cela comme point de départ pour définir les valeurs de paramètre hello dans votre étape de génération.
   
   | Paramètre | Description |
   | --- | --- |
   | -ResourceGroupLocation |Hello valeur emplacement géographique où le groupe de ressources hello se trouve, telles que **eastus** ou **'États-Unis'**. (Ajouter des guillemets simples s’il existe un espace dans le nom de hello). Consultez les [Régions Azure](https://azure.microsoft.com/en-us/regions/) pour plus d’informations. |
   | -ResourceGroupName |nom Hello hello du groupe de ressources pour ce déploiement. |
   | -UploadArtifacts |Ce paramètre, lorsqu’il est présent, spécifie que les artefacts qui doivent toobe téléchargement tooAzure à partir du système local de hello. Vous ne devez tooset ce commutateur si votre déploiement de modèle requiert des artefacts supplémentaires que vous souhaitez toostage à l’aide du script PowerShell de hello (tels que les scripts de configuration ou les modèles imbriqués). |
   | -StorageAccountName |nom de Hello hello du compte de stockage utilisé toostage artefacts pour ce déploiement. Ce paramètre est utilisé uniquement si vous mettez en place des artefacts pour le déploiement. Si ce paramètre est fourni, un compte de stockage est créé si le script de hello n’a pas créé une au cours d’un déploiement précédent. Si le paramètre hello est spécifié, compte de stockage hello doit déjà exister. |
   | -StorageAccountResourceGroupName |nom Hello hello du groupe de ressources associé au compte de stockage hello. Ce paramètre est obligatoire uniquement si vous fournissez une valeur pour le paramètre de StorageAccountName hello. |
   | -TemplateFile |fichier de modèle toohello Hello chemin d’accès dans le projet de déploiement de groupe de ressources Azure hello. flexibilité de tooenhance, utilisez un chemin d’accès pour ce paramètre est l’emplacement relatif toohello Hello script PowerShell au lieu d’un chemin d’accès absolu. |
   | -TemplateParametersFile |fichier de paramètres toohello Hello chemin d’accès dans le projet de déploiement de groupe de ressources Azure hello. flexibilité de tooenhance, utilisez un chemin d’accès pour ce paramètre est l’emplacement relatif toohello Hello script PowerShell au lieu d’un chemin d’accès absolu. |
   | -ArtifactStagingDirectory |Ce paramètre permet de script PowerShell hello connaître le dossier de hello à partir duquel les fichiers binaires du projet hello doivent être copiés. Cette valeur remplace la valeur par défaut de hello utilisé par hello script PowerShell. Pour utiliser de Visual Studio Team Services, valeur hello : ArtifactStagingDirectory - $(Build.StagingDirectory) |
   
   Voici un exemple d’arguments de script (ligne divisée pour une meilleure lisibilité) :
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   Lorsque vous avez terminé, hello **Arguments de Script** zone devrait ressembler à hello suivant liste :
   
   ![Arguments de script][11]
9. Une fois que vous avez ajouté tous les hello toohello éléments requis Azure PowerShell étape de génération, choisissez hello **file d’attente** générer bouton toobuild hello projet. Hello **générer** écran montre la sortie de hello de hello script PowerShell.

### <a name="detailed-walkthrough-for-option-2"></a>Procédure pas à pas pour l’option 2
Hello procédures suivantes vous guident tout déploiement continu nécessaire tooconfigure étapes hello dans Visual Studio Team Services à l’aide de tâches intégrées de hello.

1. Modifier votre VS Team Services build définition tooadd deux nouvelles étapes de génération. Choisissez la définition de build hello sous hello **des définitions de Build** catégorie, puis choisissez hello **modifier** lien.
   
   ![Modifier la définition de build][12]
2. Étapes de génération hello ajouter nouvelle définition de build toohello hello **étape de génération ajouter...** .
   
   ![Ajouter une étape de génération][13]
3. Choisissez hello **déployer** catégorie de tâche, sélectionnez hello **Azure File Copy** de tâches, puis son **ajouter** bouton.
   
   ![Ajouter la tâche Copie de fichiers Azure][14]
4. Choisissez hello **déploiement de groupe de ressources Azure** de tâches, puis cliquez sur son **ajouter** bouton, puis **fermer** hello **tâche catalogue**.
   
   ![Ajouter une tâche Déploiement de groupes de ressources Azure][15]
5. Choisissez hello **Azure File Copy** remplir ses valeurs et de la tâche.
   
   Si vous disposez déjà d’un point de terminaison de service Azure ajouté tooVS Team Services, choisissez un abonnement de hello Bonjour **abonnement Azure** zone de liste déroulante. Si vous n’avez pas d’abonnement, consultez les instructions pour en configurer un dans Visual Studio Team Services décrites dans la section [Option 1](#detailed-walkthrough-for-option-1).
   
   * Source : entrez **$(Build.StagingDirectory)**.
   * Type de connexion Azure : sélectionnez **Azure Resource Manager**.
   * Abonnement RM Azure - abonnement hello sélectionnez hello compte de stockage souhaité toouse Bonjour **abonnement Azure** zone de liste déroulante. Si l’abonnement de hello n’apparaît pas, choisissez hello **Actualiser** hello suivant du bouton **gérer** lien.
   * Type de destination : sélectionnez **Objet blob Azure**.
   * Compte de stockage RM - sélectionner compte de stockage de hello vous aimeriez toouse pour les artefacts de mise en lots
   * Nom de conteneur - entrez hello nom du conteneur de hello vous aimeriez toouse pour la mise en lots ; Il peut être n’importe quel nom de conteneur valide, mais utiliser une définition de build toothis dédié
   
   Pour les valeurs de sortie hello :
   
   * URI du conteneur de stockage : entrez **artifactsLocation**
   * Jeton SAS du conteneur de stockage : entrez **artifactsLocationSasToken**
   
   ![Configurer la tâche Copie de fichiers Azure][16]
6. Choisissez hello **déploiement de groupe de ressources Azure** étape de génération et puis remplir ses valeurs.
   
   * Type de connexion Azure : sélectionnez **Azure Resource Manager**.
   * Abonnement RM Azure - abonnement sélectionnez hello pour le déploiement dans hello **abonnement Azure** zone de liste déroulante. Il s’agit généralement de hello même abonnement utilisé à l’étape précédente de hello
   * Action : sélectionnez **Créer ou mettre à jour un groupe de ressources**.
   * Groupe de ressources - sélectionner un groupe de ressources ou entrez le nom hello d’un nouveau groupe de ressources pour le déploiement de hello
   * Emplacement - emplacement sélectionnez hello pour le groupe de ressources hello
   * Modèle - Entrez le chemin d’accès de hello et de hello modèle toobe déployé ajoutant **$(Build.StagingDirectory)**, par exemple : **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**
   * Paramètres de modèle - Entrez le chemin d’accès de hello et de hello toobe de paramètres utilisé, ajoutant **$(Build.StagingDirectory)**, par exemple : **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**
   * Remplacer les paramètres de modèle : entrez ou copier- coller hello suivant de code :
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Configurer une tâche Déploiement de groupes de ressources Azure][17]
7. Une fois que vous avez ajouté tous les éléments requis de hello, enregistrer la définition de build hello et choisissez **nouvelle build en file d’attente** haut hello.

## <a name="next-steps"></a>Étapes suivantes
Lecture [vue d’ensemble du Gestionnaire de ressources Azure](azure-resource-manager/resource-group-overview.md) toolearn plus d’informations sur le Gestionnaire de ressources Azure et les groupes de ressources Azure.

[0]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png
[1]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png
[2]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png
[3]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png
[4]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png
[5]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png
[8]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png
[9]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png
[10]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png
[11]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png
[12]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png
[13]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png
[14]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png
[15]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png
[16]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png
[17]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png
