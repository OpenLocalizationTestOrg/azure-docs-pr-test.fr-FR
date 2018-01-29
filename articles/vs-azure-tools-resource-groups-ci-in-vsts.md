---
title: "Intégration continue dans Visual Studio Team Services à l’aide de projets Groupe de ressources Azure | Microsoft Docs"
description: "Décrit la configuration de l’intégration continue dans Visual Studio Team Services en utilisant des projets de déploiement Groupe de ressources Azure dans Visual Studio."
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
ms.openlocfilehash: e7d98ca3fa281a136595c37ed9b7e71de0cf7bff
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a>Intégration continue dans Visual Studio Team Services à l’aide de projets de déploiement de groupe de ressources Azure
Pour déployer un modèle Azure, vous devez effectuer les tâches en différentes étapes : Générer, Tester, Copier sur Azure (également appelé « gestion intermédiaire ») et Déployer le modèle. Il existe deux façons de déployer des modèles sur Visual Studio Team Services (VS Team Services). Les deux méthodes fournissent les mêmes résultats. Par conséquent, choisissez celle qui convient le mieux à votre flux de travail.

1. Ajoutez une opération unique à la définition de build qui exécute le script PowerShell inclus dans le projet de déploiement du groupe de ressources Azure (Deploy-AzureResourceGroup.ps1). Le script copie les artefacts et déploie ensuite le modèle.
2. Ajouter plusieurs étapes de build à Visual Studio Team Services, chacune effectuant une tâche intermédiaire.

Cet article présente les deux options. La première option a l’avantage d’utiliser le script utilisé par les développeurs dans Visual Studio et de garantir une cohérence tout au long du cycle de vie. La deuxième option est une alternative pratique au script intégré. Les deux procédures partent du principe que vous disposez déjà d’un projet de déploiement Visual Studio contrôlé dans Visual Studio Team Services.

## <a name="copy-artifacts-to-azure"></a>Copier des artefacts sur Azure
Quel que soit le scénario, si vous disposez de tous les artefacts nécessaires au déploiement du modèle, vous devez octroyer un accès à Azure Resource Manager. Ces artefacts peuvent inclure des fichiers tels que :

* des modèles imbriqués
* des scripts de configuration et DSC
* fichiers binaires d’application

### <a name="nested-templates-and-configuration-scripts"></a>Modèles imbriqués et les scripts de configuration
Lorsque vous utilisez les modèles fournis par Visual Studio (ou générés à l’aide d’extraits de code Visual Studio), le script PowerShell ne se contente pas de préparer les artefacts. Elle ajuste également l’URI correspondant aux différentes ressources de déploiement. Le script copie les artefacts vers un conteneur sécurisé dans Azure, crée un jeton SAP pour ce conteneur, puis transmet ces informations au déploiement du modèle. Consultez la section [Créer un modèle de déploiement](https://msdn.microsoft.com/library/azure/dn790564.aspx) pour en savoir plus sur les modèles imbriqués.  Quand vous utilisez des tâches dans Visual Studio Team Services, vous devez sélectionner les tâches appropriées pour votre déploiement de modèle et, si nécessaire, transmettre les valeurs de paramètre de l’étape intermédiaire au déploiement du modèle.

## <a name="set-up-continuous-deployment-in-vs-team-services"></a>Configurer le déploiement continu dans Visual Studio Team Services
Pour appeler le script PowerShell dans Visual Studio Team Services, vous devez mettre à jour votre définition de build. En bref, les étapes sont : 

1. la modification des définitions de build.
2. la définition de l’autorisation Azure dans Visual Studio Team Services.
3. l’ajout d’une étape de build d’Azure PowerShell faisant référence au script PowerShell dans le projet de déploiement de groupe de ressources Azure.
4. la définition de la valeur du paramètre *-ArtifactsStagingDirectory* pour qu’il fonctionne avec un projet créé dans Visual Studio Team Services.

### <a name="detailed-walkthrough-for-option-1"></a>Procédure pas à pas pour l’option 1
Les procédures suivantes vous guident lors des étapes nécessaires à la configuration d’un déploiement continu dans Visual Studio Team Services à l’aide d’une tâche unique qui exécute le script PowerShell dans votre projet. 

1. Modifiez votre définition de build de Visual Studio Team Services et ajoutez une étape de build Azure PowerShell. Choisissez la définition de build sous la catégorie **Définitions de build**, puis choisissez le lien **Modifier**.
   
   ![Modifier la définition de build][0]
2. Ajoutez une nouvelle étape **Azure PowerShell** à la définition de build, puis sélectionnez **Ajouter une étape de build…**. .
   
   ![Ajouter une étape de génération][1]
3. Choisissez la catégorie **Déployer une tâche**, sélectionnez la tâche **Azure PowerShell**, puis choisissez son bouton **Ajouter**.
   
   ![Ajouter des tâches][2]
4. Choisissez l’étape de build **Azure PowerShell** , puis renseignez ses valeurs.
   
   1. Si vous disposez déjà d’un point de terminaison de service Azure ajouté à Visual Studio Team Services, sélectionnez l’abonnement dans la zone de liste déroulante **Abonnement Azure**, puis passez à la section suivante. 
      
      Si vous n’avez pas de point de terminaison de service Azure dans Visual Studio Team Services, vous devez en ajouter un. Cette sous-section vous guide dans la procédure. Si votre compte Azure utilise un compte Microsoft (tel que Hotmail), vous devez procéder comme suit pour obtenir l’authentification d’un principal de service.
   2. Choisissez le lien **Gérer** en regard de la zone de liste déroulante **Abonnement Azure**.
      
      ![Gérer les abonnements Azure][3]
   3. Choisissez **Azure** dans la zone de liste déroulante **Nouveau point de terminaison de Service**.
      
      ![Nouveau point de terminaison de service][4]
   4. Dans la boîte de dialogue **Ajouter un abonnement Azure**, sélectionnez l’option **Principal du service**.
      
      ![Option du principal de service][5]
   5. Ajoutez les informations de votre abonnement Azure à la boîte de dialogue **Ajouter un abonnement Azure** . Vous devez fournir les éléments suivants :
      
      * ID d’abonnement
      * Nom d'abonnement
      * ID de principal de service
      * Clé de principal de service
      * ID client
   6. Ajout d’un nom de votre choix à la zone de nom **Abonnement** . Cette valeur apparaîtra plus tard dans la liste déroulante **Abonnement Azure** dans Visual Studio Team Services. 
   7. Si vous ne connaissez pas votre ID d’abonnement Azure, vous pouvez utiliser une des commandes suivantes pour le récupérer.
      
      Pour les scripts PowerShell, utilisez :
      
      `Get-AzureRmSubscription`
      
      Pour l’interface de ligne de commande Azure, consultez :
      
      `azure account show`
   8. Pour obtenir un ID de principal de service, une clé de principal de service et un ID client, suivez la procédure dans [Création de l’application Active Directory et du principal du service à l’aide du portail](resource-group-create-service-principal-portal.md) ou [Authentification d’un principal du service à l’aide d’Azure Resource Manager](resource-group-authenticate-service-principal.md).
   9. Ajoutez les valeurs de l’ID de principal du service, de la clé de principal du service et de l’ID de locataire dans la boîte de dialogue **Ajouter un abonnement Azure**, puis choisissez le bouton **OK**.
      
      Vous disposez désormais d’un Principal de service valide à utiliser pour exécuter le script Azure PowerShell.
5. Modifiez la définition de build, puis choisissez l’étape de build **Azure PowerShell** . Sélectionnez l’abonnement dans la zone de liste déroulante **Abonnement Azure** . (Si l’abonnement n’apparaît pas, choisissez le bouton **Actualiser** en regard du lien **gérer**.) 
   
   ![Configurer une tâche de génération Azure PowerShell][8]
6. Fournissez un chemin d’accès pour le script PowerShell Deploy-azureresourcegroup.ps1. Pour ce faire, cliquez sur les points de suspension (...) en regard de la zone **Chemin du script**, accédez au script Deploy-AzureResourceGroup.ps1 dans le dossier **Scripts** de votre projet, sélectionnez-le, puis cliquez sur le bouton **OK**.    
   
   ![Sélectionner le chemin d’accès au script][9]
7. Après avoir sélectionné le script, mettez à jour le chemin d’accès au script afin de l’exécuter depuis Build.StagingDirectory (répertoire dans lequel *ArtifactsLocation* est défini). Vous pouvez le faire en ajoutant « $(Build.StagingDirectory)/ » au début du chemin de script.
   
    ![Modifier le chemin d’accès au script][10]
8. Dans la zone **Arguments de script** , saisissez les paramètres suivants (sur une seule ligne). Lorsque vous exécutez le script dans Visual Studio, vous pouvez voir comment Visual Studio utilise les paramètres dans la fenêtre **Sortie** . Vous pouvez l’utiliser comme point de départ pour définir les valeurs de paramètre dans l’étape de build.
   
   | Paramètre | Description |
   | --- | --- |
   | -ResourceGroupLocation |Valeur de l’emplacement géographique où le groupe de ressources est localisé, par exemple **eastus** ou **« États-Unis de l'Est »**. (Ajouter des guillemets simples si le nom comporte un espace). Consultez les [Régions Azure](https://azure.microsoft.com/en-us/regions/) pour plus d’informations. |
   | -ResourceGroupName |Nom du groupe de ressources utilisé pour ce déploiement. |
   | -UploadArtifacts |Ce paramètre, quand il est présent, spécifie que les artefacts doivent être chargés vers Azure à partir du système local. Il vous suffit de définir ce commutateur si le déploiement de votre modèle requiert des artefacts supplémentaires pour les phases intermédiaires de l’utilisation du script PowerShell (tels que les scripts de configuration ou les modèles imbriqués). |
   | -StorageAccountName |Nom du compte de stockage utilisé pour les artefacts intermédiaires pour ce déploiement. Ce paramètre est utilisé uniquement si vous mettez en place des artefacts pour le déploiement. Si ce paramètre est fourni, un compte de stockage est créé si le script n’en a pas créé un au cours d’un déploiement précédent. Si le paramètre est spécifié, le compte de stockage doit déjà exister. |
   | -StorageAccountResourceGroupName |Nom du groupe de ressources contenant le compte de stockage. Ce paramètre est obligatoire uniquement si vous fournissez une valeur pour le paramètre StorageAccountName. |
   | -TemplateFile |Chemin d’accès vers le fichier modèle dans le projet de déploiement de groupe de ressources Azure. Pour améliorer la flexibilité, utilisez un chemin d’accès vers ce paramètre relatif à l’emplacement du script PowerShell au lieu d’un chemin d’accès absolu. |
   | -TemplateParametersFile |Chemin d’accès vers le fichier de paramètre dans le projet de déploiement de groupe de ressources Azure. Pour améliorer la flexibilité, utilisez un chemin d’accès vers ce paramètre relatif à l’emplacement du script PowerShell au lieu d’un chemin d’accès absolu. |
   | -ArtifactStagingDirectory |Ce paramètre indique au script PowerShell le dossier à partir duquel les fichiers binaires du projet doivent être copiés. Cette valeur remplace la valeur par défaut utilisée par le script PowerShell. Pour utiliser Visual Studio Team Services, définissez la valeur sur : - ArtifactStagingDirectory $(Build.StagingDirectory) |
   
   Voici un exemple d’arguments de script (ligne divisée pour une meilleure lisibilité) :
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   Lorsque vous avez terminé, la zone **Arguments de script** ressemble en principe à la liste suivante :
   
   ![Arguments de script][11]
9. Une fois que vous avez ajouté tous les éléments requis pour l’étape de build Azure PowerShell, choisissez le bouton **File d’attente** pour générer le projet. L’écran **Build** affiche la sortie du script PowerShell.

### <a name="detailed-walkthrough-for-option-2"></a>Procédure pas à pas pour l’option 2
Les procédures suivantes vous guident lors des étapes nécessaires à la configuration d’un déploiement continu dans Visual Studio Team Services à l’aide des tâches intégrées.

1. Modifiez votre définition de build Visual Studio Team Services pour ajouter deux nouvelles étapes de génération. Choisissez la définition de build sous la catégorie **Définitions de build**, puis choisissez le lien **Modifier**.
   
   ![Modifier la définition de build][12]
2. Ajoutez les nouvelles étapes de génération à la définition de build à l’aide du bouton **Ajouter une étape de génération...** .
   
   ![Ajouter une étape de génération][13]
3. Choisissez la catégorie de tâche **Déployer**, sélectionnez la tâche **Copie de fichiers Azure**, puis choisissez son bouton **Ajouter**.
   
   ![Ajouter la tâche Copie de fichiers Azure][14]
4. Choisissez la tâche **Déploiement de groupes de ressources Azure**, cliquez sur son bouton **Ajouter**, puis **fermez** le **Catalogue de tâches**.
   
   ![Ajouter une tâche Déploiement de groupes de ressources Azure][15]
5. Choisissez la tâche **Copie de fichiers Azure** et renseignez ses valeurs.
   
   Si vous disposez déjà d’un point de terminaison de service Azure ajouté à Visual Studio Team Services, sélectionnez l’abonnement dans la zone de liste déroulante **Abonnement Azure**. Si vous n’avez pas d’abonnement, consultez les instructions pour en configurer un dans Visual Studio Team Services décrites dans la section [Option 1](#detailed-walkthrough-for-option-1).
   
   * Source : entrez **$(Build.StagingDirectory)**.
   * Type de connexion Azure : sélectionnez **Azure Resource Manager**.
   * Abonnement Azure RM : sélectionnez l’abonnement pour le compte de stockage que vous souhaitez utiliser dans la zone de liste déroulante **Abonnement Azure**. Si l’abonnement n’apparaît pas, choisissez le bouton **Actualiser** en regard du lien **Gérer**.
   * Type de destination : sélectionnez **Objet blob Azure**.
   * Compte de stockage RM : sélectionnez le compte de stockage que vous souhaitez utiliser pour mettre en place des artefacts.
   * Nom du conteneur : entrez le nom du conteneur que vous souhaitez utiliser pour la préparation. Il peut s’agir d’un nom de conteneur valide quelconque, mais il doit être dédié à cette définition de build.
   
   Pour les valeurs de sortie :
   
   * URI du conteneur de stockage : entrez **artifactsLocation**
   * Jeton SAS du conteneur de stockage : entrez **artifactsLocationSasToken**
   
   ![Configurer la tâche Copie de fichiers Azure][16]
6. Choisissez l’étape de génération **Déploiement de groupes de ressources Azure**, puis renseignez ses valeurs.
   
   * Type de connexion Azure : sélectionnez **Azure Resource Manager**.
   * Abonnement Azure RM : sélectionnez l’abonnement pour le déploiement dans la zone de liste déroulante **Abonnement Azure**. Il s’agit généralement du même abonnement qu’à l’étape précédente.
   * Action : sélectionnez **Créer ou mettre à jour un groupe de ressources**.
   * Groupe de ressources : sélectionnez un groupe de ressources ou entrez le nom d’un nouveau groupe de ressources pour le déploiement.
   * Emplacement : sélectionnez l’emplacement du groupe de ressources.
   * Modèle : entrez le chemin d’accès et le nom du modèle à déployer en ajoutant le préfixe **$(Build.StagingDirectory)**, par exemple : **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**.
   * Paramètres du modèle : entrez le chemin d’accès et le nom des paramètres à utiliser en ajoutant le préfixe **$(Build.StagingDirectory)**, par exemple : **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**.
   * Remplacer les paramètres de modèle : entrez ou copiez et collez le code suivant :
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Configurer une tâche Déploiement de groupes de ressources Azure][17]
7. Une fois que vous avez ajouté tous les éléments requis, enregistrez la définition de build et choisissez **Mettre la nouvelle build en file d’attente** en haut.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur Azure Resource Manager et les groupes de ressources Azure, consultez l’article [Vue d’ensemble d’Azure Resource Manager](azure-resource-manager/resource-group-overview.md).

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
