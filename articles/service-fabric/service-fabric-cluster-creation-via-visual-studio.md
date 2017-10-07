---
title: "aaaSetting configuration d’un cluster Service Fabric à l’aide de Visual Studio | Documents Microsoft"
description: "Décrit comment tooset d’une infrastructure de Service de cluster à l’aide du modèle Azure Resource Manager créé par un projet de groupe de ressources Azure dans Visual Studio"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a>Configuration d’un cluster Service Fabric à l’aide de Visual Studio
Cet article décrit comment tooset d’un Service Azure Fabric de cluster à l’aide de Visual Studio et un modèle Azure Resource Manager. Nous allons utiliser un modèle de Visual Studio Azure ressource groupe projet toocreate hello. Une fois le modèle de hello a été créé, il peut être déployé directement tooAzure à partir de Visual Studio. Il peut également être utilisé à partir d’un script ou dans le cadre de la fonctionnalité d’intégration continue (CI).

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a>Création d’un modèle de cluster Service Fabric à l’aide d’un projet de groupe de ressources Azure
tooget a démarré, ouvrez Visual Studio et créez un projet de groupe de ressources Azure (il est disponible dans hello **Cloud** dossier) :

![Boîte de dialogue Nouveau projet avec le projet du groupe de ressources Azure sélectionné][1]

Vous pouvez créer une solution Visual Studio pour ce projet ou solution existante de tooan l’ajouter.

> [!NOTE]
> Si vous ne voyez pas le projet de groupe de ressources Azure hello sous le nœud de Cloud hello, vous n’avez pas hello Azure SDK est installé. Lancez Web Platform Installer ([installer maintenant](http://www.microsoft.com/web/downloads/platform.aspx) si vous n’avez pas déjà), puis recherchez « Azure SDK pour .NET » et installer la version hello qui est compatible avec votre version de Visual Studio.
> 
> 

Après avoir appuyé sur le bouton OK de hello, Visual Studio vous demandera tooselect hello Gestionnaire de ressources du modèle de toocreate :

![Boîte de dialogue Sélectionner le modèle Azure avec le modèle de cluster Service Fabric sélectionné][2]

Sélectionnez à nouveau le modèle de Cluster Service Fabric hello et le bouton de positionnement hello OK. projet de Hello et modèle du Gestionnaire de ressources hello ont été créés.

## <a name="prepare-hello-template-for-deployment"></a>Préparer un modèle de hello pour le déploiement
Avant cluster de hello toocreate déployé le modèle de hello, vous devez fournir des valeurs des paramètres du modèle hello requis. Ces valeurs de paramètres sont lus à partir de hello `ServiceFabricCluster.parameters.json` fichier, qui est Bonjour `Templates` dossier du projet de groupe de ressources hello. Ouvrir le fichier de hello et fournir hello valeurs suivantes :

| Nom du paramètre | Description |
| --- | --- |
| adminUsername |nom de Hello du compte d’administrateur hello pour les ordinateurs de l’infrastructure de Service (nœuds). |
| certificateThumbprint |Hello empreinte numérique du certificat hello qui sécurise le cluster de hello. |
| sourceVaultResourceId |Hello *ID de ressource* de coffre de clés hello où est stocké certificat hello qui sécurise le cluster de hello. |
| certificateUrlValue |URL de Hello hello cluster du certificat de sécurité. |

modèle de gestionnaire de ressources de Visual Studio Service Fabric Hello crée un cluster sécurisé qui est protégé par un certificat. Ce certificat est identifié par hello a trois paramètres de modèle (`certificateThumbprint`, `sourceVaultValue`, et `certificateUrlValue`), et il doit exister dans un **Azure Key Vault**. Pour plus d’informations sur la façon dont toocreate hello le certificat de sécurité de cluster, consultez [scénarios de sécurité du cluster Service Fabric](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) l’article.

## <a name="optional-change-hello-cluster-name"></a>Facultatif : Remplacez nom de cluster hello
Chaque cluster Service Fabric dispose d’un nom. Lors de la création d’un cluster de l’ensemble fibre optique dans Azure, le nom de cluster détermine (conjointement avec hello région Azure) nom du système DNS (Domain Name) hello pour le cluster de hello. Par exemple, si vous le nommez votre cluster `myBigCluster`et emplacement hello (région Azure) hello du groupe de ressources qui hébergera le nouveau cluster de hello est des États-Unis, nom DNS de hello du cluster de hello `myBigCluster.eastus.cloudapp.azure.com`.

Par défaut, nom du cluster hello est généré automatiquement et rendu unique en attachant un préfixe « cluster » du tooa suffixe aléatoire. Cela rend modèle de hello toouse très facilement en tant que partie d’un **intégration continue** système (CI). Si vous voulez toouse un nom spécifique pour votre cluster, qui est significatif tooyou, valeur hello hello `clusterName` variable dans le fichier de modèle de gestionnaire de ressources hello (`ServiceFabricCluster.json`) nom de tooyour choisi. Il est hello première variable définie dans ce fichier.

## <a name="optional-add-public-application-ports"></a>Facultatif : ajout de ports d’application publics
Vous pouvez également les ports publics application toochange hello pour le cluster de hello avant de le déployer. Par défaut, le modèle de hello ouvre deux ports TCP publics (80 et 8081). Si vous avez besoin pour vos applications, modifiez la définition d’équilibrage de charge Azure hello dans le modèle de hello. définition de Hello est stockée dans le fichier de modèle principal hello (`ServiceFabricCluster.json`). Ouvrez ce fichier et recherchez `loadBalancedAppPort`. Chaque port est associé à trois artefacts :

1. Une variable de modèle qui définit la valeur du port TCP hello pour le port de hello :
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. A *sonde* qui définit la fréquence et la durée pendant laquelle hello équilibrage de charge Azure tentatives tooanother une toouse un nœud de l’infrastructure de Service spécifique avant d’échouer. les sondes Hello font partie de hello ressource d’équilibrage de charge. Voici la définition de sonde hello pour le port de l’application hello première valeur par défaut :
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. A *règle d’équilibrage de charge* qui relie les ports hello et sonde hello, qui permet à équilibrage de charge entre un ensemble de nœuds de cluster Service Fabric :
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   Si les applications de hello que vous envisagez de toodeploy toohello cluster ont besoin de davantage de ports, vous pouvez les ajouter par la création de sonde supplémentaire et les définitions de règle de l’équilibrage de charge. Pour plus d’informations sur la façon de toowork avec équilibrage de charge Azure grâce aux modèles du Gestionnaire de ressources, consultez [prise en main la création d’un équilibreur de charge interne à l’aide d’un modèle](../load-balancer/load-balancer-get-started-ilb-arm-template.md).

## <a name="deploy-hello-template-by-using-visual-studio"></a>Déployer le modèle de hello à l’aide de Visual Studio
Après avoir enregistré toutes les hello des valeurs de paramètre obligatoires dans le`ServiceFabricCluster.param.dev.json` fichier, vous toodeploy prêt hello modèle et créez votre cluster Service Fabric. Cliquez sur le projet de groupe de ressources hello dans l’Explorateur de solutions Visual Studio et choisissez **déployer | Nouveau déploiement...** . Si la nécessaire, Visual Studio affiche hello **déployer tooResource groupe** boîte de dialogue vous demandant de tooauthenticate tooAzure :

![Déployer la boîte de dialogue groupe tooResource][3]

boîte de dialogue Hello vous permet de choisir un groupe de ressources existant Gestionnaire de ressources de cluster de hello et donne vous hello option toocreate un. Il est normalement sens toouse un groupe de ressources distinct pour un cluster Service Fabric.

Après avoir appuyé sur le bouton de déployer hello, Visual Studio vous invite valeurs de paramètre de modèle tooconfirm hello. Positionnement hello **enregistrer** bouton. Un paramètre n’a pas une valeur persistante : un mot de passe de compte d’administrateur de cluster de hello hello. Vous devez tooprovide une valeur de mot de passe lorsque Visual Studio vous invite à un.

> [!NOTE]
> À partir d’Azure SDK 2.9, Visual Studio prend en charge la lecture des mots de passe depuis **Azure Key Vault** pendant le déploiement. Dans la boîte de dialogue Paramètres de modèle hello, notez que hello `adminPassword` zone de texte de paramètre a une petite icône de « clé » sur hello droite. Cette icône vous permet de tooselect un secret de coffre de clés existant en tant que mot de passe d’administration hello pour le cluster de hello. Assurez-vous simplement que toofirst à activer l’accès Azure Resource Manager pour le déploiement de modèle dans hello avancée des stratégies d’accès de votre coffre de clés. 
> 
> 

Vous pouvez surveiller la progression hello du processus de déploiement hello dans la fenêtre de sortie de Visual Studio hello. Une fois le déploiement d’un modèle hello est terminé, votre nouveau cluster est prêt toouse !

> [!NOTE]
> Si PowerShell n’a jamais été utilisé tooadminister Azure à partir de l’ordinateur hello que vous utilisez, vous devez toodo maintenance un peu.
> 
> 1. Activer les scripts en exécutant hello PowerShell [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) commande. Pour les machines de développement, la stratégie « unrestricted » est généralement acceptable.
> 2. Décidez si collecte de données de diagnostic tooallow commandes Azure PowerShell, puis exécutez [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) ou [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) si nécessaire. Cela permet d'éviter les invites inutiles lors du déploiement du modèle.
> 
> 

S’il existe des erreurs, accédez à toohello [portail Azure](https://portal.azure.com/) et groupe de ressources hello ouverts que vous avez déployé à. Cliquez sur **tous les paramètres**, puis cliquez sur **déploiements** sur le panneau des paramètres hello. Un déploiement de groupe de ressources ayant échoué laisse des informations de diagnostic détaillées à cet endroit.

> [!NOTE]
> Clusters service Fabric nécessitent un certain nombre de toobe nœuds la disponibilité du toomaintain et conservent l’état - tooas référencé « gestion de quorum ». Par conséquent, il n’est pas sécurisé tooshut vers le bas de toutes les machines de hello du cluster de hello, sauf si vous avez tout d’abord exécuté un [une sauvegarde complète de l’état](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur la configuration de cluster Service Fabric à l’aide de hello portail Azure](service-fabric-cluster-creation-via-portal.md)
* [Découvrez comment toomanage et déployer des applications de Service Fabric à l’aide de Visual Studio](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
