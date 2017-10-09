---
title: "aaaSet configuration d’un cluster Azure Service Fabric | Documents Microsoft"
description: "Démarrage rapide - Créer un cluster Service Fabric Windows ou Linux sur Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a>Créer votre premier cluster Service Fabric sur Azure
Un [cluster Service Fabric](service-fabric-deploy-anywhere.md) est un groupe de machines virtuelles ou physiques connectées au réseau, sur lequel vos microservices sont déployés et gérés. Ce démarrage rapide vous aide à toocreate un cluster de cinq nœuds, en cours d’exécution sur Windows ou Linux, via hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) ou [portail Azure](http://portal.azure.com) dans quelques minutes.  

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.


## <a name="use-hello-azure-portal"></a>Utilisez hello portail Azure

Connectez-vous toohello portail Azure à l’adresse [http://portal.azure.com](http://portal.azure.com).

### <a name="create-hello-cluster"></a>Créer le cluster de hello

1. Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.
2. Sélectionnez **de calcul** de hello **nouveau** panneau, puis sélectionnez **Cluster Service Fabric** de hello **de calcul** panneau.
3. Remplir hello Service Fabric **notions de base** formulaire. Pour **système d’exploitation**, sélectionnez version hello de Windows ou Linux que vous souhaitez hello toorun des nœuds de cluster. nom d’utilisateur Hello et le mot de passe entré ici est toolog utilisé dans la machine virtuelle de toohello. Pour **Groupe de ressources** créez-en un nouveau. Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont créées et gérées collectivement. Lorsque vous avez terminé, cliquez sur **OK**.

    ![Résultat de configuration du cluster][cluster-setup-basics]

4. Remplir hello **configuration de Cluster** formulaire.  Dans **Nombre de type de nœud**, mettez « 1 ».

5. Sélectionnez **le type de nœud 1 (principal)** et remplissez hello **configuration du type de nœud** formulaire.  Entrez un nom de type de nœud et définissez hello [le niveau de durabilité](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) trop « Bronze ».  Sélectionnez une taille de machine virtuelle.

    Taille de machine virtuelle hello, nombre d’ordinateurs virtuels, des points de terminaison personnalisés, définissent des types de nœuds et d’autres paramètres pour hello des machines virtuelles de ce type. Chaque type de nœud défini est configuré comme un ensemble d’échelle de machine virtuelle distincte, qui est utilisé toodeploy et les machines virtuelles gérées en tant qu’ensemble. Chaque type de nœud peut faire l’objet d’une montée ou descente en puissance de manière indépendante, avoir différents jeux de ports ouverts et présenter différentes métriques de capacité.  Hello premier ou principal, type de nœud est où les services de système de l’infrastructure de Service sont hébergés et doivent avoir cinq ou plusieurs machines virtuelles.

    Pour un déploiement de production, la [planification de la capacité](service-fabric-cluster-capacity.md) est une étape importante.  Pour ce guide de démarrage rapide, toutefois, vous n’exécutez pas d’applications. Vous pouvez donc sélectionner la taille de machine virtuelle *DS1_v2 Standard*.  Sélectionnez « Silver » pour hello [niveau de fiabilité](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) et une échelle de machine virtuelle initiale définie la capacité de 5.  

    Points de terminaison personnalisés ouvrent des ports dans l’équilibrage de charge Azure hello afin que vous pouvez vous connecter avec les applications qui s’exécutent sur le cluster de hello.  Entrez « 80, 8172 » tooopen les ports 80 et 8172.

    Ne pas vérifier hello **configurer des paramètres avancés** boîte, qui est utilisée pour la personnalisation de points de terminaison de la gestion de TCP/HTTP, plages de ports d’application, [les contraintes de placement](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), et [capacité propriétés](service-fabric-cluster-resource-manager-metrics.md).    

    Sélectionnez **OK**.

6. Bonjour **configuration de Cluster** écran, définissez **Diagnostics** trop**sur**.  Pour ce démarrage rapide, vous ne devez pas tooenter toute [définition de l’ensemble fibre optique](service-fabric-cluster-fabric-settings.md) propriétés.  Dans **la version de Fabric**, sélectionnez **automatique** mise à niveau en mode afin que Microsoft met automatiquement à jour la version de hello du code de l’ensemble fibre optique de hello exécution hello cluster.  Définir le mode hello trop**manuel** si vous souhaitez trop[choisir une version prise en charge](service-fabric-cluster-upgrade.md) tooupgrade à. 

    ![Configuration du type de nœud][node-type-config]

    Sélectionnez **OK**.

7. Remplir hello **sécurité** formulaire.  Pour ce guide de démarrage rapide, sélectionnez **Non sécurisé**.  Il est vivement recommandé de toocreate un cluster sécurisé pour les charges de production, toutefois, étant donné que toute personne peut anonymement connecter tooan des clusters non sécurisés et effectuer des opérations de gestion.  

    Certificats sont utilisés dans les toosecure Service Fabric tooprovide l’authentification et chiffrement divers aspects d’un cluster et ses applications. Pour plus d’informations sur l’utilisation de certificats dans Service Fabric, consultez la page [Scénarios de sécurité d’un cluster Service Fabric](service-fabric-cluster-security.md).  à l’aide d’Azure Active Directory ou tooset des certificats pour la sécurité de l’application, l’authentification utilisateur tooenable [créer un cluster à partir d’un modèle de gestionnaire de ressources](service-fabric-cluster-creation-via-arm.md).

    Sélectionnez **OK**.

8. Hello de révision résumé.  Si vous souhaitez que toodownload un modèle de gestionnaire de ressources généré à partir des paramètres de hello que vous avez entrées, sélectionnez **télécharger le modèle et les paramètres**.  Sélectionnez **créer** cluster hello de toocreate.

    Vous pouvez voir la progression de la création de hello dans les notifications de hello. (Cliquez sur l’icône de hello « cloche » près de barre d’état hello au niveau supérieur de hello à droite de votre écran.) Si vous avez cliqué sur **code confidentiel tooStartboard** lors de la création de cluster de hello, vous voyez **déploiement d’un Cluster Service Fabric** épinglé toohello **Démarrer** carte.

### <a name="view-cluster-status"></a>Afficher l’état du cluster
Une fois que votre cluster est créé, vous pouvez inspecter votre cluster Bonjour **vue d’ensemble** panneau dans le portail de hello. Vous pouvez maintenant voir les détails de hello de votre cluster dans le tableau de bord hello, y compris le point de terminaison public du cluster hello et un lien de tooService Fabric Explorer.

![État du cluster][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Visualiser le cluster hello à l’aide de l’Explorateur de Service Fabric
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) est un bon outil pour visualiser votre cluster et gérer les applications.  Service Fabric Explorer est un service qui s’exécute dans un cluster de hello.  Accéder à l’aide d’un navigateur web en cliquant sur hello **Service Fabric Explorer** lien du cluster de hello **vue d’ensemble** page hello portail.  Vous pouvez également entrer l’adresse de hello directement dans le navigateur de hello : [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)

tableau de bord Hello cluster fournit une vue d’ensemble de votre cluster, y compris un résumé de l’application et d’intégrité de nœud. affichage du nœud Hello montre la disposition physique de hello du cluster de hello. Vous pouvez identifier les applications ayant déployé du code sur un nœud donné.

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a>Connecter le cluster toohello à l’aide de PowerShell
Vérifiez que le cluster hello est en cours d’exécution en vous connectant à l’aide de PowerShell.  module ServiceFabric PowerShell Hello est installé avec hello [Service Fabric SDK](service-fabric-get-started.md).  Hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) applet de commande établit un cluster de toohello de connexion.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
Consultez [cluster sécurisée de se connecter tooa](service-fabric-connect-to-secure-cluster.md) pour obtenir des exemples de connexion tooa cluster. Après la connexion toohello cluster, utilisez hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay de l’applet de commande une liste de nœuds dans les informations de cluster et d’état hello pour chaque nœud. **HealthState** doit être à l’état *OK* pour chaque nœud.

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a>Supprimer le cluster de hello
Un cluster Service Fabric est constitué d’autres ressources Windows Azure en outre toohello du cluster lui-même. Toocompletely supprimer un cluster Service Fabric, vous devez également toodelete que tous hello il est constitué de ressources. cluster de Hello la plus simple façon toodelete hello et toutes les ressources hello qu’elle consomme est le groupe de ressources toodelete hello. Pour les autres toodelete comme un cluster ou un toodelete certaines ressources (mais pas toutes) hello dans un groupe de ressources, consultez [supprimer un cluster](service-fabric-cluster-delete.md)

Supprimer un groupe de ressources Bonjour portail Azure :
1. Accédez à cluster Service Fabric de toohello vous souhaitez toodelete.
2. Cliquez sur hello **groupe de ressources** nom sur la page d’essentials hello cluster.
3. Bonjour **Essentials du groupe de ressources** , cliquez sur **supprimer le groupe de ressources** et suivez les instructions de hello sur cette page toocomplete hello la suppression du groupe de ressources hello.
    ![Supprimer le groupe de ressources hello][cluster-delete]


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a>Utiliser Azure Powershell toodeploy un cluster sécurisé
1. Télécharger hello [Azure Powershell version 4.0 ou version ultérieure du module](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) sur votre ordinateur.

2. Ouvrez une fenêtre Windows PowerShell, hello exécuter commande suivante. 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    Vous devez voir s’afficher une sortie similaire toohello.

    ![liste ps][ps-list]

3. Connexion tooAzure et toowhich d’abonnement hello sélectionnez vous voulez toocreate hello cluster

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. Exécution hello suivant toonow de la commande Créer un cluster sécurisé. N’oubliez pas de paramètres de hello toocustomize. 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    commande Hello peut prendre de 10 minutes too30 minutes toocomplete, à fin hello de celle-ci, vous devez obtenir un suivante toohello similaire de sortie. sortie de Hello a plus d’informations sur le certificat hello, hello KeyVault où il a été téléchargé, et hello dossier local où le certificat de hello est copié. 

    ![Résultat PS][ps-out]

5. Copier l’intégralité de la sortie hello tooa fichier texte et enregistrez-le comme nous devons toorefer tooit. Prenez note de hello informations suivantes à partir de la sortie de hello. 

    - **CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx
    - **CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10
    - **ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080
    - **ClientConnectionEndpointPort** : 19000

### <a name="install-hello-certificate-on-your-local-machine"></a>Installer le certificat de hello sur votre ordinateur local
  
tooconnect toohello cluster, vous avez besoin tooinstall hello certificat dans le magasin personnel (My) de hello de l’utilisateur actuel hello. 

Exécutez hello suivant PowerShell

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

Vous êtes maintenant cluster sécurisée de tooyour tooconnect prêt.

### <a name="connect-tooa-secure-cluster"></a>Connecter le cluster sécurisée de tooa 

Exécutez hello suivant cluster sécurisée du tooa tooconnect commande PowerShell. Détails du certificat Hello doivent correspondre à un certificat qui a été utilisé tooset cluster de hello. 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


Hello suivant l’exemple affiche hello des paramètres completed : 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Exécutez hello suivant toocheck de commande que vous êtes connecté et le cluster de hello est sain.

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a>Publier votre cluster de tooyour des applications à partir de Visual Studio

Maintenant que vous avez configuré un cluster Azure, vous pouvez publier votre tooit d’applications à partir de Visual Studio en suivant hello [publier tooan cluster](service-fabric-publish-app-remote-cluster.md) document. 

### <a name="remove-hello-cluster"></a>Supprimer le cluster de hello
Un cluster est composé d’autres ressources Windows Azure en outre toohello du cluster lui-même. cluster de Hello la plus simple façon toodelete hello et toutes les ressources hello qu’elle consomme est le groupe de ressources toodelete hello. 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez configuré un cluster de développement, essayez suivante de hello :
* [Créer un cluster sécurisé dans le portail de hello](service-fabric-cluster-creation-via-portal.md)
* [Créer un cluster à partir d’un modèle](service-fabric-cluster-creation-via-arm.md) 
* [Déployer des applications à l’aide de PowerShell](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
