---
title: aaaCreate une infrastructure de Service de cluster dans Azure | Documents Microsoft
description: "Découvrez comment toocreate un Service Fabric de Linux ou Windows cluster dans Azure à l’aide de PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a>Créer un cluster sécurisé sur Azure à l’aide de PowerShell
Ce didacticiel vous montre comment toocreate une infrastructure de Service de cluster (Windows ou Linux) en cours d’exécution dans Azure. Lorsque vous avez terminé, vous disposez d’un cluster en cours d’exécution dans le cloud hello que vous pouvez déployer des applications.

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Création d’un cluster Service Fabric sécurisé dans Azure à l’aide de PowerShell
> * Cluster hello sécurisé avec un certificat X.509
> * Connecter le cluster toohello à l’aide de PowerShell
> * Supprimer un cluster

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel :
- Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- Installer hello [module Service Fabric SDK et PowerShell](service-fabric-get-started.md)
- Installer hello [Azure Powershell version 4.1 ou version ultérieure du module](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)

Hello procédure crée une version d’évaluation (seul ordinateur virtuel) à nœud unique cluster Service Fabric. cluster de Hello est sécurisé par un certificat auto-signé qui obtient créé en même temps que le cluster de hello et placé dans un coffre de clés. Les clusters à nœud unique ne peut pas être mis à l’échelle au-delà d’un ordinateur virtuel et les clusters d’aperçu ne peut pas être mis à niveau toonewer versions.

coût toocalculate par l’exécution d’un cluster Service Fabric dans Azure utilisation hello [calculatrice de tarification Azure](https://azure.microsoft.com/pricing/calculator/).
Pour plus d’informations sur la création de clusters Service Fabric, consultez l’article [Créer un cluster Service Fabric à l’aide d’Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

## <a name="create-hello-cluster-using-azure-powershell"></a>Créer le cluster hello à l’aide d’Azure PowerShell
1. Télécharger une copie locale du modèle de gestionnaire de ressources Azure hello et fichier de paramètres hello de hello [modèle Azure Resource Manager pour le Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) référentiel GitHub.  *azuredeploy.JSON* est le modèle Azure Resource Manager hello qui définit un cluster Service Fabric. *azuredeploy.Parameters.JSON* est un fichier de paramètres pour vous de déploiement de cluster toocustomize hello.

2. Personnaliser les paramètres Bonjour suivants de hello *azuredeploy.parameters.json* fichier de paramètres :

   | Paramètre       | Description | Valeur suggérée |
   | --------------- | ----------- | --------------- |
   | clusterLocation | cluster de hello Hello région Azure toowhich toodeploy. | *par exemple, westeurope, eastasia, eastus* |
   | clusterName     | Nom du cluster de hello souhaité toocreate. | *par exemple, bobs-sfpreviewcluster* |
   | adminUsername   | compte d’administrateur local Hello sur les ordinateurs virtuels du cluster hello. | *N’importe quel nom d’utilisateur Windows Server valide* |
   | adminPassword   | Mot de passe du compte d’administrateur local de hello sur les ordinateurs virtuels du cluster hello. | *N’importe quel mot de passe Windows Server valide* |
   | clusterCodeVersion | toorun de version du Service Fabric Hello. (255.255.X.255 sont des préversions). | **255.255.5718.255** |
   | vmInstanceCount | nombre de Hello de machines virtuelles dans votre cluster (il peut être 1 ou 3-99). | **1** | *Pour un cluster de la version d’évaluation, spécifiez uniquement un ordinateur virtuel* |

3. Ouvrez une console PowerShell, la connexion tooAzure et sélectionnez hello abonnement cluster de hello toodeploy dans :

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. Créez et chiffrer un mot de passe pour hello toobe de certificat utilisé par l’infrastructure de Service.

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. Créer des clusters de hello et son certificat en exécutant hello de commande suivante :

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   >Hello `-CertificateSubjectName` paramètre doit s’aligner avec le paramètre clusterName hello spécifié dans le fichier de paramètres hello, ainsi que hello domaine lié toohello région Azure vous avez choisi, telles que : `clustername.eastus.cloudapp.azure.com`.

Une fois la configuration de hello se termine, il génère des informations sur le cluster hello créé dans Azure. Il copie également le répertoire hello cluster certificat toohello - CertificateOutputFolder sur le chemin d’accès hello spécifié pour ce paramètre. Vous avez besoin de ce certificat de tooaccess Service Fabric Explorer et la vue de contrôle d’intégrité hello de votre cluster.

Prenez note de l’URL de hello pour votre cluster, ce qui peut être toohello similaire suivant URL : *https://mycluster.westeurope.cloudapp.azure.com:19080*

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a>Modifier le certificat de hello et accéder au Service Fabric Explorer ##

1. Double-cliquez sur hello tooopen de certificat hello Assistant Importation de certificat.

2. Utiliser les paramètres par défaut, mais que toocheck hello **marquer cette clé comme exportable.** case à cocher, Bonjour **protection par clé privée** étape. Visual Studio a besoin de certificat de hello tooexport lors de la configuration de l’authentification de Registre de conteneur Azure tooService Cluster Fabric plus loin dans ce didacticiel.

3. Vous pouvez maintenant ouvrir Service Fabric Explorer dans un navigateur. toodo accédez donc toohello **ManagementEndpoint** URL pour votre cluster à l’aide d’un navigateur web et un certificat de hello select qui a été enregistré sur votre ordinateur.

>[!NOTE]
>Quand vous ouvrez Service Fabric Explorer, vous voyez une erreur de certificat, car vous utilisez un certificat auto-signé. Dans Microsoft Edge, vous avez tooclick *détails* et puis hello *aller sur la page Web de toohello* lien. Dans Chrome, vous avez tooclick *avancé* et puis hello *continuer* lien.

>[!NOTE]
>Si la création du cluster hello échoue, vous pouvez toujours exécuter à nouveau commande hello, qui met à jour des ressources hello déjà déployés. Si un certificat a été créé dans le cadre du déploiement de hello a échoué, une est générée. la création du cluster tootroubleshoot, consultez [créer un cluster Service Fabric à l’aide du Gestionnaire de ressources Azure](service-fabric-cluster-creation-via-arm.md).

## <a name="connect-toohello-secure-cluster"></a>Connecter le cluster sécurisée de toohello
Se connecter à l’aide du module PowerShell de l’infrastructure de Service de hello installé avec hello SDK de l’infrastructure de Service de cluster de toohello.  Tout d’abord, installez hello certificat dans hello personnel (My) magasin de l’utilisateur actuel de hello sur votre ordinateur.  Exécutez hello suivant de commande PowerShell :

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

Vous êtes maintenant cluster sécurisée de tooyour tooconnect prêt.

Hello **Service Fabric** module PowerShell fournit de nombreuses applets de commande pour la gestion des clusters Service Fabric, les applications et services.  Hello d’utilisation [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) applet de commande tooconnect toohello sécurisée cluster. Hello empreinte numérique du certificat et les détails de connexion au point de terminaison sont trouvent dans la sortie de hello à partir d’une étape précédente.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Vérifiez que vous êtes connecté et le cluster de hello est sain à l’aide de hello [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) applet de commande.

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a>Supprimer des ressources

Un cluster est composé d’autres ressources Windows Azure en outre toohello du cluster lui-même. cluster de Hello la plus simple façon toodelete hello et toutes les ressources hello qu’elle consomme est le groupe de ressources toodelete hello.

Connectez-vous à tooAzure et sélectionnez l’ID d’abonnement hello avec laquelle vous souhaitez le cluster de hello tooremove.  Vous pouvez trouver votre ID d’abonnement en vous connectant à toohello [portail Azure](http://portal.azure.com). Supprimer le groupe de ressources hello et toutes les ressources de cluster hello à l’aide de hello [applet de commande Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Créer un cluster Service Fabric dans Azure
> * Cluster hello sécurisé avec un certificat X.509
> * Connecter le cluster toohello à l’aide de PowerShell
> * Supprimer un cluster

Ensuite, avancer toohello suivant toolearn didacticiel comment toodeploy une application existante.
> [!div class="nextstepaction"]
> [Déployer une application .NET existante avec Docker Compose](service-fabric-host-app-in-a-container.md)
