---
title: "aaaCreate l’infrastructure de Service de cluster Bonjour portail Azure | Documents Microsoft"
description: "Cet article décrit comment tooset configuration d’un cluster Service Fabric sécurisé à l’aide d’Azure hello portail Azure et Azure Key Vault."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a>Créer un cluster Service Fabric dans Azure à l’aide de hello portail Azure
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Portail Azure](service-fabric-cluster-creation-via-portal.md)
> 
> 

Il s’agit d’un guide pas à pas qui vous guide tout au long des étapes de hello de configuration d’un cluster Service Fabric sécurisé dans Azure à l’aide de hello portail Azure. Ce guide vous guide tout au long de hello comme suit :

* Configurer les clés de toomanage de coffre de clés pour la sécurité du cluster.
* Créez un cluster sécurisé dans Azure via hello portail Azure.
* authentification d’administrateurs à l’aide de certificat.

> [!NOTE]
> Pour accéder à des options de sécurité plus avancées, telles que l’authentification des utilisateurs avec Azure Active Directory et la configuration de certificats pour la sécurité des applications, [créez votre cluster à l’aide d’Azure Resource Manager][create-cluster-arm].
> 
> 

Un cluster sécurisé est un cluster qui empêche les opérations de toomanagement tout accès non autorisé, qui inclut le déploiement, la mise à niveau et la suppression des applications, services et données hello qu’ils contiennent. Un cluster non sécurisé est un cluster que toute personne peut se connecter tooat à tout moment et effectuer des opérations de gestion. Bien qu’il soit possible de toocreate un cluster non sécurisé, il est **hautement recommandé toocreate un cluster sécurisé**. Un cluster non sécurisé **ne peut pas être sécurisé ultérieurement** , ce qui implique la création d’un nouveau cluster.

concepts de Hello sont hello même pour la création de clusters sécurisés, si les clusters hello sont des clusters Linux ou des clusters Windows. Pour en savoir plus et pour accéder à des scripts d’assistance dédiés à la création de clusters Linux sécurisés, voir [Créer des clusters sécurisés sur Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters). Hello paramètres obtenus par le script du programme d’assistance hello fourni peuvent être entrés directement dans le portail de hello comme décrit dans la section de hello [créer un cluster Bonjour Azure portal](#create-cluster-portal).

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure
Ce guide utilise [Azure PowerShell][azure-powershell]. Lorsque vous démarrez une nouvelle session PowerShell, connectez-vous tooyour compte Azure et sélectionnez votre abonnement avant l’exécution de commandes Azure.

Ouvrez une session dans le compte de tooyour azure :

```powershell
Login-AzureRmAccount
```

Sélectionnez votre abonnement :

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a>Configuration d’Azure Key Vault
Cette partie du guide de hello vous guide tout au long de la création d’un coffre de clés pour un cluster Service Fabric dans Azure et les applications de Service Fabric. Pour obtenir un guide complet sur le coffre de clés, consultez hello [le coffre de clés mise en route][key-vault-get-started].

Service Fabric utilise toosecure de certificats X.509 un cluster. Coffre de clés Azure est toomanage utilisé des certificats pour les clusters Service Fabric dans Azure. Lorsqu’un cluster est déployé dans Azure, le fournisseur de ressources Azure hello chargé de créer des clusters Service Fabric extrait les certificats de coffre de clés et les installe sur les machines virtuelles du cluster hello.

Hello diagramme suivant illustre les relations hello entre le coffre de clés, un cluster Service Fabric et le fournisseur de ressources Azure hello qui utilise les certificats stockés dans le coffre de clés lorsqu’il crée un cluster :

![Installation de certificats][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Créer un groupe de ressources
première étape de Hello est toocreate un nouveau groupe de ressources spécifiquement pour le coffre de clés. Placement de coffre de clés dans son propre groupe de ressources est recommandé afin que vous pouvez supprimer des groupes de ressources de calcul et de stockage - telles que le groupe de ressources hello qui a votre cluster Service Fabric - sans perdre vos clés et les clés secrètes. groupe de ressources Hello a votre coffre de clés doit être Bonjour même région que le cluster hello qui l’utilise.

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a>Création d'un coffre de clés
Créer un coffre de clés dans le nouveau groupe de ressources hello. Hello coffre de clés **doit être activée pour le déploiement** tooallow hello certificats de tooget de fournisseur de ressources de l’infrastructure de Service à partir de celui-ci et l’installer sur les nœuds de cluster :

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```

Si vous avez un coffre de clés existant, vous pouvez l’activer pour le déploiement à l’aide de l’interface de ligne de commande :

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a>Ajouter des certificats tooKey coffre
Certificats sont utilisés dans les toosecure Service Fabric tooprovide l’authentification et chiffrement divers aspects d’un cluster et ses applications. Pour plus d’informations sur l’utilisation de certificats dans Service Fabric, consultez la page [Scénarios de sécurité d’un cluster Service Fabric][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Certificat de cluster et de serveur (obligatoire)
Ce certificat est requis toosecure un cluster et empêcher tout accès non autorisé tooit. Il assure la sécurité du cluster de différentes manières :

* **Authentification du cluster :** authentifie la communication nœud à nœud pour la fédération du cluster. Seuls les nœuds qui peuvent prouver leur identité avec ce certificat peuvent être ajouté hello cluster.
* **L’authentification du serveur :** authentifie hello gestion des points de terminaison tooa gestion client de cluster, afin que hello gestion client sait qu’il communique avec le véritable toohello cluster. Ce certificat fournit également SSL pour hello API de gestion HTTPS et pour le Service Fabric Explorer via le protocole HTTPS.

tooserve ces fins, les certificats de hello doit respecter hello suivant les exigences :

* certificat de Hello doit contenir une clé privée.
* certificat de Hello doit être créé pour l’échange de clés, exportable tooa fichier d’échange d’informations personnelles (.pfx).
* Hello nom du sujet du certificat doit correspondre au cluster Service Fabric de hello domaine utilisé tooaccess hello. Cela est requis tooprovide SSL pour la gestion de points de terminaison HTTPS et le Service Fabric Explorer du cluster hello. Vous ne pouvez pas obtenir un certificat SSL à partir d’une autorité de certification (CA) pour hello `.cloudapp.azure.com` domaine. Vous devez obtenir un nom de domaine personnalisé pour votre cluster. Lorsque vous demandez un certificat à partir du nom du sujet du certificat de hello une autorité de certification doit correspondre au nom de domaine personnalisé hello utilisée pour votre cluster.

### <a name="client-authentication-certificates"></a>Authentification de certificat client
Les certificats client supplémentaires authentifient les administrateurs pour les tâches de gestion de cluster. Service Fabric dispose de deux niveaux d’accès : **admin** et **read-only user**. Au minimum, un seul certificat pour un accès administrateur doit être utilisé. Pour un accès de niveau utilisateur supplémentaire, un certificat distinct doit être fourni. Pour en savoir plus sur les rôles d’accès, consultez la page [Contrôle d’accès en fonction du rôle pour les clients de Service Fabric][service-fabric-cluster-security-roles].

Vous n’avez pas besoin de coffre tooupload Client d’authentification des certificats tooKey toowork avec Service Fabric. Ces certificats doivent uniquement toobe fourni toousers qui sont autorisés pour la gestion de cluster. 

> [!NOTE]
> Azure Active Directory est hello recommandé clients tooauthenticate de façon pour cluster des opérations de gestion. toouse Azure Active Directory, vous devez [créer un cluster à l’aide du Gestionnaire de ressources Azure][create-cluster-arm].
> 
> 

### <a name="application-certificates-optional"></a>Certificats d’application (facultatif)
Un nombre quelconque de certificats supplémentaires peut être installé sur un cluster pour sécuriser une application. Avant de créer votre cluster, tenez compte des scénarios de sécurité hello qui nécessitent un toobe certificat installé sur les nœuds de hello, tel que :

* Le chiffrement et déchiffrement de valeurs de configuration d’applications.
* Le chiffrement des données sur les nœuds lors de la réplication. 

Certificats d’application ne peut pas être configurés lors de la création d’un cluster via hello portail Azure. certificats d’application tooconfigure au moment le programme d’installation de cluster, vous devez [créer un cluster à l’aide du Gestionnaire de ressources Azure][create-cluster-arm]. Vous pouvez également ajouter le cluster de toohello certificats application après que qu’elle a été créée.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Mise en forme de certificats pour une utilisation par un fournisseur de ressources Azure
Des fichiers de clé privée (.pfx) peuvent être ajoutés et utilisés directement par le biais de Key Vault. Toutefois, le fournisseur de ressources Azure hello nécessite toobe clés stockée dans un format JSON spécial qui inclut .pfx hello comme base-64 codé en chaîne et hello privée clé mot de passe. tooaccommodate ces exigences, les clés doivent être placés dans une chaîne JSON et ensuite stockées en tant que *secrets* dans le coffre de clés.

est de toomake ce processus plus simple, un module PowerShell [disponible sur GitHub][service-fabric-rp-helpers]. Suivez ces module hello de toouse comme suit :

1. Téléchargez hello intégralité du contenu du référentiel de hello dans un répertoire local. 
2. Importez le module hello dans la fenêtre PowerShell :

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

Hello `Invoke-AddCertToKeyVault` commande dans ce module PowerShell met en forme une clé privée du certificat en une chaîne JSON et télécharge automatiquement les il tooKey coffre. Utiliser certificat de cluster tooadd hello et n’importe quel tooKey de certificats d’application supplémentaires coffre. Répétez cette étape pour tous les certificats supplémentaires que vous souhaitez tooinstall dans votre cluster.

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

Il s’agit de toutes les conditions préalables requises de coffre de clés hello pour la configuration d’un modèle de gestionnaire de ressources de cluster Service Fabric qui installe les certificats pour l’authentification de nœud, sécurité de point de terminaison de gestion et d’authentification et toute sécurité des applications supplémentaires fonctionnalités qui utilisent des certificats X.509. À ce stade, vous devez maintenant avoir hello après l’installation dans Azure :

* Groupe de ressources Key Vault
  * Key Vault
    * Certificat d’authentification de serveur de clusters

</a "create-cluster-portal" ></a>

## <a name="create-cluster-in-hello-azure-portal"></a>Créer un cluster Bonjour portail Azure
### <a name="search-for-hello-service-fabric-cluster-resource"></a>Rechercher des ressources de cluster Service Fabric
![Recherchez le modèle de cluster Service Fabric sur hello portail Azure.][SearchforServiceFabricClusterTemplate]

1. Connectez-vous à toohello [portail Azure][azure-portal].
2. Cliquez sur **nouveau** tooadd un nouveau modèle de ressource. Recherchez le modèle de Cluster Service Fabric hello Bonjour **Marketplace** sous **tout**.
3. Sélectionnez **Cluster Service Fabric** à partir de la liste de hello.
4. Accédez toohello **Cluster Service Fabric** panneau, cliquez sur **créer**,
5. Hello **cluster créer Service Fabric** panneau a hello suivant quatre étapes.

#### <a name="1-basics"></a>1. Concepts de base
![Capture d’écran de la création d’un groupe de ressources.][CreateRG]

Dans le panneau des principes de base hello, vous devez les détails de base de hello tooprovide pour votre cluster.

1. Entrez le nom hello de votre cluster.
2. Entrez un **nom d’utilisateur** et **mot de passe** Bureau à distance pour hello machines virtuelles.
3. Assurez-vous que tooselect hello **abonnement** que vous souhaitez votre toobe cluster déployé, surtout si vous avez plusieurs abonnements.
4. Créez un **groupe de ressources**. Il s’agit des meilleures toogive il hello même nom que le cluster de hello, dans la mesure où il vous aide à trouver une version ultérieure, en particulier lorsque vous essayez toomake modifications tooyour déploiement ou de supprimer votre cluster.
   
   > [!NOTE]
   > Vous pouvez décider toouse un groupe de ressources existant, mais il est une bonne approche en matière de toocreate un groupe de ressources. Il est ainsi facile toodelete clusters que vous n’avez pas besoin.
   > 
   > 
5. Sélectionnez hello **région** dans lequel vous souhaitez le cluster de hello toocreate. Vous devez utiliser hello même région que votre clé de coffre est dans.

#### <a name="2-cluster-configuration"></a>2. Configuration de clusters
![Création d’un type de nœud][CreateNodeType]

Configurez vos nœuds de cluster. Les types de nœud définissent les tailles de machine virtuelle hello, hello nombre de machines virtuelles et leurs propriétés. Votre cluster peut avoir plus d’un type de nœud, mais type de nœud principal hello (hello un premier que vous définissez sur le portail hello) doit avoir au moins cinq de machines virtuelles, car il s’agit de type de nœud hello où sont placés les services de système de Service Fabric. Ne configurez pas la zone **Propriétés de sélection élective** , car une propriété de sélection élective par défaut de « NodeTypeName » est ajoutée automatiquement.

> [!NOTE]
> Un scénario répandu si vous avez plusieurs types de nœuds est une application qui contient un service front-end et un service back-end. Vous souhaitez que service frontal de hello tooput sur des machines virtuelles la plus petites (tailles de machine virtuelle comme D2) avec toohello ouvrir de ports Internet, mais vous service de serveur principal tooput hello sur des machines virtuelles plus volumineux (avec des tailles de machine virtuelle, D4, D6, D15 et ainsi de suite) sans ouvrir de ports exposés à Internet.
> 
> 

1. Choisissez un nom pour votre type de nœud (1 too12 caractères contenant uniquement des lettres et chiffres).
2. Hello minimale **taille** de machines virtuelles de nœud principal de hello type est piloté par hello **durabilité** couche que vous choisissez pour le cluster de hello. valeur par défaut de Hello pour le niveau de durabilité hello est bronze. Pour plus d’informations sur la durabilité, consultez [comment toochoose hello l’infrastructure de Service de cluster la fiabilité et durabilité][service-fabric-cluster-capacity].
3. Sélectionnez la taille de machine virtuelle hello et le niveau tarifaire. Les machines virtuelles de série D ont des lecteurs de disques SSD et sont vivement recommandées pour les applications avec état. N’utilisez pas les références de machine virtuelle incluant des cœurs partiels ou présentant une capacité de disque disponible inférieure à 7 Go. 
4. Hello minimale **nombre** de machines virtuelles de nœud principal de hello type est piloté par hello **fiabilité** couche que vous choisissez. valeur par défaut de Hello pour le niveau de fiabilité hello est argent. Pour plus d’informations sur la fiabilité, consultez [comment toochoose hello l’infrastructure de Service de cluster la fiabilité et durabilité][service-fabric-cluster-capacity].
5. Choisissez un nombre hello d’ordinateurs virtuels pour le type de nœud hello. Vous pouvez augmenter ou diminuer nombre hello d’ordinateurs virtuels dans un type de nœud, ultérieurement, mais sur le type de nœud principal hello, hello minimale est pilotée par niveau de fiabilité hello que vous avez choisi. Les autres types de nœud peuvent avoir au moins 1 machine virtuelle.
6. Configurez des points de terminaison personnalisés. Ce champ vous permet de tooenter une liste séparée par des virgules des ports que vous souhaitez tooexpose via toohello d’équilibrage de charge Azure hello Internet public pour vos applications. Par exemple, si vous envisagez de toodeploy un cluster tooyour d’application web, entrez « 80 » ici trafic tooallow sur le port 80 dans votre cluster. Pour en savoir plus sur les points de terminaison, consultez la page [Communiquer avec des applications][service-fabric-connect-and-communicate-with-services].
7. Configurez les **diagnostics**du cluster. Par défaut, les diagnostics sont activés sur votre tooassist cluster avec la résolution des problèmes. Si vous souhaitez que les diagnostics de toodisable modifier hello **état** basculer trop**hors**. Nous vous recommandons de **ne pas** désactiver les diagnostics.
8. Sélectionnez hello mode que vous souhaitez que votre cluster de la valeur mise à niveau. Sélectionnez **automatique**, si vous souhaitez hello système tooautomatically récupère hello version la plus récente et que vous essayez de tooupgrade tooit de votre cluster. Définir le mode hello trop**manuel**, si vous souhaitez toochoose une version prise en charge.

> [!NOTE]
> Nous prenons uniquement en charge les clusters qui exécutent des versions prises en charge de Service Fabric. En sélectionnant hello **manuel** mode, vous tirez sur hello responsabilité tooupgrade version tooa pris en charge de votre cluster. Pour plus d’informations sur le mode de mise à niveau de Fabric hello consultez hello [document de service fabric-cluster-mise à niveau.][service-fabric-cluster-upgrade]
> 
> 

#### <a name="3-security"></a>3. Sécurité
![Capture d’écran des configurations de sécurité sur le portail Azure.][SecurityConfigs]

étape finale de Hello est cluster hello tooprovide certificat informations toosecure à l’aide de hello coffre de clés et certificats informations créé précédemment.

* Remplir les champs de certificat principal hello avec sortie hello obtenu à partir de téléchargement hello **certificat de cluster** à l’aide du coffre tooKey hello `Invoke-AddCertToKeyVault` commande PowerShell.

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* Vérifiez hello **configurer des paramètres avancés** zone tooenter les certificats clients pour **administrateur client** et **client en lecture seule**. Dans ces champs, entrez l’empreinte numérique hello de votre certificat de client d’administration et l’empreinte numérique hello de votre certificat client utilisateur en lecture seule, le cas échéant. Lorsque les administrateurs tentent tooconnect toohello cluster, elles sont accordées accès uniquement si elles ont un certificat avec une empreinte numérique qui correspond aux valeurs de l’empreinte numérique hello entré ici.  

#### <a name="4-summary"></a>4. Résumé
![Capture d’écran du tableau de démarrage hello affichage « Déploiement de Service Fabric Cluster ». ][Notifications]

la création du cluster toocomplete hello, cliquez sur **Résumé** des configurations de hello toosee que vous avez fournies, ou téléchargez hello modèle Azure Resource Manager que qui utilisé toodeploy votre cluster. Après avoir fourni les paramètres obligatoires hello, hello **OK** bouton devienne vert, et vous pouvez démarrer le processus de création de cluster hello en cliquant dessus.

Vous pouvez voir la progression de la création de hello dans les notifications de hello. (Cliquez sur l’icône de hello « cloche » près de barre d’état hello au niveau supérieur de hello à droite de votre écran.) Si vous avez cliqué sur **code confidentiel tooStartboard** lors de la création de cluster de hello, vous verrez **déploiement d’un Cluster Service Fabric** épinglé toohello **Démarrer** carte.

### <a name="view-your-cluster-status"></a>Afficher l’état de votre cluster
![Capture d’écran de détails du cluster dans le tableau de bord hello.][ClusterDashboard]

Une fois que votre cluster est créé, vous pouvez inspecter votre cluster dans le portail de hello :

1. Accédez trop**Parcourir** et cliquez sur **Service Fabric Clusters**.
2. Recherchez votre cluster et cliquez dessus.
3. Vous pouvez maintenant voir les détails de hello de votre cluster dans le tableau de bord hello, y compris le point de terminaison public du cluster hello et un lien de tooService Fabric Explorer.

Hello **nœud Moniteur** section sur le panneau de tableau de bord du cluster hello indique le nombre hello d’ordinateurs virtuels qui sont sains et non intègre. Vous trouverez plus de détails sur le contrôle d’intégrité du cluster hello à [introduction de modèle de contrôle d’intégrité de Service Fabric][service-fabric-health-introduction].

> [!NOTE]
> Clusters service Fabric nécessitent un certain nombre de toobe nœuds toujours toomaintain disponibilité et conservent l’état - tooas référencé « en conservant le quorum ». Clous, il n’est généralement pas tooshut sécurisé vers le bas de tous les ordinateurs dans un cluster de hello, sauf si vous avez tout d’abord exécuté un [une sauvegarde complète de votre état][service-fabric-reliable-services-backup-restore].
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a>Instance de tooa ensemble d’échelle de Machine virtuelle ou un nœud de cluster de connexion à distance
Chacun des hello NodeTypes vous spécifiez dans les résultats de cluster dans un ensemble de l’échelle de machines virtuelles mise en route de la configuration. Consultez [de connexion à distance instance d’ensemble d’échelle de Machine virtuelle tooa] [ remote-connect-to-a-vm-scale-set] pour plus d’informations.

## <a name="next-steps"></a>Étapes suivantes
À ce stade, vous avez un cluster sécurisé à l’aide de certificats pour l’authentification de la gestion. Ensuite, [connecter tooyour cluster](service-fabric-connect-to-secure-cluster.md) et découvrez comment trop[gérer les secrets de l’application](service-fabric-application-secret-management.md).  Découvrez également les [options de support de Service Fabric](service-fabric-support.md).

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
