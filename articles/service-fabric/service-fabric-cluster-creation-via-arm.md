---
title: "à partir d’un modèle de cluster aaaCreate un Azure Service Fabric | Documents Microsoft"
description: "Cet article décrit comment tooset d’une infrastructure sécurisée de Service de cluster dans Azure à l’aide du Gestionnaire de ressources Azure, Azure Key Vault et Azure Active Directory (Azure AD) pour l’authentification du client."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a>Créer un cluster Service Fabric à l’aide d’Azure Resource Manager
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Portail Azure](service-fabric-cluster-creation-via-portal.md)
>
>

Ce guide vous montre pas à pas comment configurer un cluster Azure Service Fabric sécurisé dans Azure à l’aide d’Azure Resource Manager. Nous accuser réception de que cet article hello est long. Néanmoins, sauf si vous connaissez déjà soigneusement le contenu hello, être toofollow que chaque étape avec soin.

guide de Hello couvre hello procédures suivantes :

* Configuration des certificats de tooupload coffre de clés Azure pour la sécurité de cluster et l’application
* Création d’un cluster sécurisé dans Azure à l’aide d’Azure Resource Manager
* Authentification des utilisateurs à l’aide d’Azure Active Directory (Azure AD) pour la gestion du cluster

Un cluster sécurisé est un cluster qui empêche les opérations de toomanagement tout accès non autorisé. Cela inclut le déploiement, la mise à niveau et suppression d’applications, services et données hello qu’ils contiennent. Un cluster non sécurisé est un cluster que toute personne peut se connecter tooat à tout moment et effectuer des opérations de gestion. Bien qu’il soit possible de toocreate un cluster non sécurisé, nous vous recommandons vivement de créer un cluster sécurisé à partir du début de hello. En effet, un cluster non sécurisé ne peut pas être sécurisé ultérieurement, ce qui implique la création d’un nouveau cluster.

concept de Hello de création de clusters sécurisés est hello identiques, qu’ils soient des clusters Windows ou Linux. Pour en savoir plus et accéder à des scripts d’assistance dédiés à la création de clusters Linux sécurisés, voir [Créer des clusters sécurisés sur Linux](#secure-linux-clusters).

## <a name="sign-in-tooyour-azure-account"></a>Se connecter tooyour compte Azure
Ce guide utilise [Azure PowerShell][azure-powershell]. Lorsque vous démarrez une nouvelle session PowerShell, connectez-vous à tooyour compte Azure, puis sélectionnez votre abonnement avant d’exécuter des commandes Azure.

La connexion tooyour compte Azure :

```powershell
Login-AzureRmAccount
```

Sélectionnez votre abonnement :

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a>Configurer un Key Vault
Cette section explique comment créer un Key Vault pour un cluster Service Fabric dans Azure et pour des applications Service Fabric. Pour un guide complet tooAzure le coffre de clés, consultez toohello [le coffre de clés mise en route][key-vault-get-started].

Service Fabric utilise toosecure de certificats X.509 un cluster et fournir des fonctionnalités de sécurité d’application. Vous utilisez des certificats de toomanage de coffre de clés pour les clusters Service Fabric dans Azure. Lorsqu’un cluster est déployé dans Azure, fournisseur de ressources Azure hello qui est chargé de créer des clusters Service Fabric extrait les certificats de coffre de clés et les installe sur les machines virtuelles du cluster hello.

Hello diagramme suivant illustre les relations hello entre Azure Key Vault, un cluster Service Fabric et le fournisseur de ressources Azure hello qui utilise les certificats stockés dans un coffre de clés lorsqu’il crée un cluster :

![Diagramme de l’installation de certificats][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Créer un groupe de ressources
première étape de Hello est toocreate un groupe de ressources spécifiquement pour votre coffre de clés. Nous vous recommandons de placer le coffre de clés hello dans son propre groupe de ressources. Cette action permet de supprimer des groupes ressources de calcul et de stockage hello, y compris le groupe de ressources hello qui contient votre cluster Service Fabric, sans perdre vos clés et les clés secrètes. groupe de ressources Hello qui contient votre coffre de clés _doit être Bonjour même région_ en tant que cluster hello qui l’utilise.

Si vous envisagez de clusters toodeploy dans plusieurs régions, nous vous suggérons de nom de groupe de ressources hello et coffre de clés hello d’une manière qui indique quelle région auquel il appartient.  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
sortie de Hello doit ressembler à ceci :

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a>Créer un coffre de clés dans le nouveau groupe de ressources hello
coffre de clés Hello _doit être activée pour le déploiement_ tooallow hello certificats de tooget de fournisseur de ressources de calcul à partir de celui-ci et l’installer sur les instances de machine virtuelle :

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

sortie de Hello doit ressembler à ceci :

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
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
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a>Utiliser un Key Vault existant

toouse un coffre de clés existant, vous _devez l’activer pour le déploiement_ tooallow hello certificats de tooget de fournisseur de ressources de calcul à partir de celui-ci et l’installer sur les nœuds de cluster :

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a>Ajouter le coffre de clés de certificats tooyour

Certificats sont utilisés dans les toosecure Service Fabric tooprovide l’authentification et chiffrement divers aspects d’un cluster et ses applications. Pour plus d’informations sur l’utilisation de certificats dans Service Fabric, consultez la page [Scénarios de sécurité d’un cluster Service Fabric][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Certificat de cluster et de serveur (obligatoire)
Ce certificat est requis toosecure un cluster et empêcher tout accès non autorisé tooit. Il assure la sécurité du cluster de deux manières :

* Authentification du cluster : authentifie la communication nœud à nœud pour la fédération du cluster. Seuls les nœuds qui peuvent prouver leur identité avec ce certificat peuvent être ajouté hello cluster.
* L’authentification du serveur : authentifie hello gestion des points de terminaison tooa gestion client de cluster, afin que hello gestion client sait qu’il communique avec le véritable toohello cluster. Ce certificat fournit également une connexion SSL pour hello API de gestion HTTPS et pour le Service Fabric Explorer via le protocole HTTPS.

tooserve ces fins, les certificats de hello doit respecter hello suivant les exigences :

* certificat de Hello doit contenir une clé privée.
* certificat de Hello doit être créé pour l’échange de clés, qui est exportable tooa fichier d’échange d’informations personnelles (.pfx).
* nom du sujet du certificat Hello doit correspondre au domaine hello que vous utilisez cluster Service Fabric de hello tooaccess. Cette mise en correspondance est requise tooprovide une connexion SSL pour les points de terminaison de gestion du cluster hello HTTPS et le Service Fabric Explorer. Vous ne pouvez pas obtenir un certificat SSL à partir d’une autorité de certification (CA) pour hello. cloudapp.azure.com domaine. Vous devez obtenir un nom de domaine personnalisé pour votre cluster. Lorsque vous demandez un certificat à partir d’une autorité de certification, hello nom du sujet du certificat doit correspondre au nom de domaine personnalisé hello que vous utilisez pour votre cluster.

### <a name="application-certificates-optional"></a>Certificats d’application (facultatif)
Un nombre quelconque de certificats supplémentaires peut être installé sur un cluster pour sécuriser une application. Avant de créer votre cluster, tenez compte des scénarios de sécurité hello qui nécessitent un toobe certificat installé sur les nœuds de hello, tel que :

* Le chiffrement et déchiffrement de valeurs de configuration d’application.
* Le chiffrement des données sur les nœuds lors de la réplication.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Mise en forme de certificats pour une utilisation par un fournisseur de ressources Azure
Vous pouvez ajouter et utiliser les fichiers de clé privée (.pfx) directement via votre Key Vault. Toutefois, le fournisseur de ressources de calcul Azure hello nécessite toobe clés stockée dans un format spécial de JavaScript Objet Notation (JSON). format de Hello inclut le fichier .pfx de hello comme un base 64-chaîne encodée au format et le mot de passe clé privée hello. tooaccommodate ces exigences, hello clés doivent être placés dans une chaîne JSON et ensuite stockées en tant que « clés secrètes » dans la clé de hello coffre.

toomake ce processus, un [module PowerShell est disponible sur GitHub][service-fabric-rp-helpers]. module de hello toouse, hello suivant :

1. Téléchargez hello intégralité du contenu du référentiel de hello dans un répertoire local.
2. Accédez toohello répertoire local.
2. Importez le module de ServiceFabricRPHelpers hello dans la fenêtre PowerShell :

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

Hello `Invoke-AddCertToKeyVault` commande dans ce module PowerShell met en forme une clé privée du certificat en une chaîne JSON et télécharge le coffre de clés toohello automatiquement. Utiliser le certificat de cluster hello commande tooadd hello et un coffre de clés toohello de certificats supplémentaires de l’application. Répétez cette étape pour tous les certificats supplémentaires que vous souhaitez tooinstall dans votre cluster.

#### <a name="uploading-an-existing-certificate"></a>Chargement d’un certificat existant

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

Si vous obtenez une erreur, par exemple hello celui présenté ici, cela signifie que vous disposez d’un conflit d’URL de ressource. conflit de hello tooresolve, modifier le nom de coffre de clés hello.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Une fois que la résolution du conflit de hello, sortie de hello doit ressembler à ceci :

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
>Vous devez hello trois précédent chaînes CertificateThumbprint, SourceVault et CertificateURL, tooset un tooobtain et un cluster Service Fabric sécurisée tous les certificats de l’application que vous pouvez utiliser pour la sécurité de l’application. Si vous n’enregistrez pas les chaînes de hello, il peut être difficile tooretrieve en interrogeant hello clé de coffre ultérieurement.

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a>Création d’un certificat auto-signé et de les télécharger toohello coffre de clés

Si vous avez déjà téléchargé votre coffre de clés de certificats toohello, ignorez cette étape. Cette étape est de générer un nouveau certificat auto-signé et de les télécharger tooyour coffre de clés. Une fois que vous modifiez les paramètres de hello Bonjour script suivant et exécutez, vous devez fournir un mot de passe du certificat.  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

Si vous obtenez une erreur, par exemple hello celui présenté ici, cela signifie que vous disposez d’un conflit d’URL de ressource. conflit de hello tooresolve, modifier le nom de coffre de clés hello, nom de groupe de routage et ainsi de suite.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Une fois que la résolution du conflit de hello, sortie de hello doit ressembler à ceci :

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
>Vous devez hello trois précédent chaînes CertificateThumbprint, SourceVault et CertificateURL, tooset un tooobtain et un cluster Service Fabric sécurisée tous les certificats de l’application que vous pouvez utiliser pour la sécurité de l’application. Si vous n’enregistrez pas les chaînes de hello, il peut être difficile tooretrieve en interrogeant hello clé de coffre ultérieurement.

 À ce stade, vous devez avoir hello suit les éléments en place :

* groupe de ressources du coffre de clés Hello.
* Bonjour coffre de clés et de son URL (appelé SourceVault Bonjour précédant la sortie PowerShell).
* certificat d’authentification serveur Hello cluster et son URL dans le coffre de clés hello.
* certificats d’application Hello et leurs URL dans le coffre de clés hello.


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a>Configuration d’Azure Active Directory pour l’authentification des clients

Azure AD permet aux organisations (appelés clients) toomanage utilisateur accès tooapplications. Ces dernières se composent d’applications avec une interface utilisateur de connexion web et d’applications avec une expérience client natif. Dans cet article, nous partons du principe que vous avez déjà créé un locataire. Si vous n’avez pas le cas, commencez par lire [comment tooget Azure Active Directory locataire][active-directory-howto-tenant].

Un cluster Service Fabric offre plusieurs tooits de points d’entrée des fonctionnalités de gestion, y compris hello basée sur le web [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] et [Visual Studio] [service-fabric-manage-application-in-visual-studio]. Par conséquent, vous créez le cluster de deux accès Azure AD applications toocontrol toohello, une application web et une application native.

toosimplify certaines des étapes de hello concernés par la configuration d’Azure AD avec un cluster Service Fabric, nous avons créé un ensemble de scripts Windows PowerShell.

> [!NOTE]
> Vous devez effectuer hello comme suit avant de créer le cluster de hello. Étant donné que les scripts hello attendent des points de terminaison et les noms de cluster, les valeurs hello doivent être planifiées et pas les valeurs que vous avez déjà créé.

1. [Télécharger les scripts hello] [ sf-aad-ps-script-download] tooyour ordinateur.
2. Avec le bouton hello fichier zip, sélectionnez **propriétés**, sélectionnez hello **Unblock** case à cocher, puis cliquez sur **appliquer**.
3. Extrayez le fichier zip de hello.
4. Exécutez `SetupApplications.ps1`et fournir hello TenantId, ClusterName et WebApplicationReplyUrl en tant que paramètres. Par exemple :

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    Vous pouvez trouver votre TenantId en exécutant la commande PowerShell de hello `Get-AzureSubscription`. L’exécution de cette commande affiche hello TenantId pour chaque abonnement.

    ClusterName est applications hello Azure AD tooprefix utilisés qui sont créées par le script de hello. Il n’a pas besoin nom du cluster actuel toomatch hello exactement. Il est prévu toomake uniquement il plus facile toomap Azure AD artefacts toohello Service Fabric cluster qu’ils sont utilisés avec.

    WebApplicationReplyUrl est hello par défaut point de terminaison Azure AD renvoie tooyour utilisateurs une fois qu’elles sont terminées la signature. Définissez ce point de terminaison en tant que point de terminaison de Service Fabric Explorer hello pour votre cluster, qui est par défaut :

    https://&lt;cluster_domain&gt;:19080/Explorer

    Vous êtes invité à toosign tooan compte disposant des privilèges d’administrateur pour le client de hello Azure AD. Après que vous être connecté, hello script crée les web hello et applications natives toorepresent votre cluster Service Fabric. Si vous examinez les applications du locataire hello Bonjour [portail Azure classic][azure-classic-portal], vous devez voir deux entrées :

   * *ClusterName*\_Cluster
   * *ClusterName*\_Client

   script de Hello imprime hello JSON requis par le modèle de gestionnaire de ressources Azure hello lorsque vous créez le cluster de hello dans la section suivante de hello, par conséquent, il est une fenêtre PowerShell de bonne idée tookeep hello ouvrir.

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a>Création d’un modèle Service Fabric Cluster Resource Manager
Dans cette section, hello génère de hello précédent des commandes PowerShell sont utilisés dans un modèle de gestionnaire de ressources du cluster Service Fabric.

Modèles de l’exemple de gestionnaire de ressources sont disponibles dans hello [la galerie de modèle de démarrage rapide Azure sur GitHub][azure-quickstart-templates]. Ces modèles peuvent être utilisés comme point de départ pour votre modèle de cluster.

### <a name="create-hello-resource-manager-template"></a>Créer le modèle de gestionnaire de ressources hello
Ce guide utilise hello [cluster sécurisée à 5 nœuds] [ service-fabric-secure-cluster-5-node-1-nodetype] exemple de modèle et les paramètres de modèle. Télécharger `azuredeploy.json` et `azuredeploy.parameters.json` tooyour ordinateur et ouvrez les deux fichiers dans votre éditeur de texte.

### <a name="add-certificates"></a>Ajout de certificats
Vous ajouter le modèle de gestionnaire de ressources du cluster certificats tooa en référençant le coffre de clés hello qui contient les clés de certificat hello. Nous vous recommandons de placer les valeurs hello coffre de clés dans un fichier de paramètres de modèle de gestionnaire de ressources. Cela conserve hello Gestionnaire de ressources du fichier de modèle réutilisables et de déploiement tooa spécifique de valeurs.

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a>Ajouter des qu'ensembles de l’échelle de machines virtuelles de tous les certificats toohello osProfile
Chaque certificat est installé dans un cluster de hello doit être configuré dans la section d’osProfile hello de ressource de jeu de mise à l’échelle hello (Microsoft.Compute/virtualMachineScaleSets). Cette action indique à hello fournisseur tooinstall hello du certificat de ressources sur les machines virtuelles de hello. Cette installation inclut le certificat de cluster hello et tous les certificats de sécurité d’application que vous envisagez de toouse pour vos applications :

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a>Configurer le certificat de cluster Service Fabric hello
certificat d’authentification Hello cluster doit être configuré dans les deux ressources de cluster Service Fabric hello (Microsoft.ServiceFabric/clusters) et hello extension Service Fabric pour l’échelle de machines virtuelles définit dans la ressource de jeu de mise à l’échelle hello machine virtuelle. Ce procédé permet tooconfigure de fournisseur de ressources de Service Fabric hello pour les utiliser pour l’authentification du cluster et serveur pour les points de terminaison de gestion.

##### <a name="virtual-machine-scale-set-resource"></a>Ressource des groupes de machines virtuelles identiques :
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a>Ressource Service Fabric :
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a>Insérer la configuration Azure AD
configuration de Hello Azure AD que vous avez créé précédemment peut être insérée directement dans votre modèle de gestionnaire de ressources. Toutefois, il est recommandé d’abord extraire les valeurs de hello dans un réutilisable de modèle de gestionnaire de ressources paramètres fichier tookeep hello et libres de déploiement tooa spécifique de valeurs.

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <a "configure-arm" ></a>Configuration des paramètres de modèle Resource Manager
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
Enfin, utilisez les valeurs de sortie de hello du coffre de clés hello et le fichier de paramètres de Azure AD PowerShell commandes toopopulate hello :

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
À ce stade, vous devez avoir hello suit les éléments en place :

* Groupe de ressources du Key Vault
  * Coffre de clés
  * Certificat d’authentification de serveur de clusters
  * Certificat de chiffrement de données
* Locataire Azure Active Directory
  * Application Azure AD pour la gestion basée sur le web et Service Fabric Explorer
  * Application Azure AD pour la gestion du client natif
  * Utilisateurs et rôles qui leur sont affectés
* Modèle Service Fabric Cluster Resource Manager
  * Certificats configurés par le biais du Key Vault
  * Configuration d’Azure Active Directory

Hello suivant schéma montre où interviennent les votre coffre de clés et de la configuration d’Azure AD dans votre modèle de gestionnaire de ressources.

![Mappage de dépendances de Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a>Créer le cluster de hello
Vous êtes maintenant cluster de hello toocreate prêt à l’aide de [déploiement de modèle de ressource Azure][resource-group-template-deploy].

#### <a name="test-it"></a>Testez-le
Utilisez hello suivant tootest de commande PowerShell de votre modèle de gestionnaire de ressources avec un fichier de paramètres :

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a>Déployez-le
Si le test de modèle de gestionnaire de ressources hello réussit, utilisez hello suivant toodeploy de commande PowerShell votre modèle de gestionnaire de ressources avec un fichier de paramètres :

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a>Affecter des utilisateurs tooroles
Après avoir créé hello applications toorepresent votre cluster, affecter vos utilisateurs des rôles toohello pris en charge par le Service Fabric : en lecture seule et administrateur. Vous pouvez attribuer des rôles de hello à l’aide de hello [portail Azure classic][azure-classic-portal].

1. Bonjour portail Azure, accédez à tooyour client, puis sélectionnez **Applications**.
2. Sélectionnez l’application web hello, qui porte un nom comme `myTestCluster_Cluster`.
3. Cliquez sur hello **utilisateurs** onglet.
4. Sélectionnez un tooassign d’utilisateur, puis cliquez sur hello **affecter** bouton bas hello écran hello.

    ![Les utilisateurs tooroles bouton affecter][assign-users-to-roles-button]
5. Sélectionnez hello rôle tooassign toohello utilisateur.

    ![Boîte de dialogue Affecter des utilisateurs][assign-users-to-roles-dialog]

> [!NOTE]
> Pour plus d’informations sur les rôles dans Service Fabric, consultez [Contrôle d’accès en fonction du rôle pour les clients de Service Fabric](service-fabric-cluster-security-roles.md).
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a>Créer des clusters sécurisés sur Linux
processus de hello toomake plus facile, nous avons fourni un [script du programme d’assistance](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux). Avant d’utiliser ce script d’assistance, assurez-vous que l’interface de ligne de commande Azure (CLI) est déjà installée, et qu’il se trouve dans votre chemin d’accès. Assurez-vous que le script de hello a tooexecute d’autorisations en exécutant `chmod +x cert_helper.py` après l’avoir téléchargé. première étape de Hello est toosign dans tooyour compte Azure à l’aide de CLI avec hello `azure login` commande. Une fois connectés tooyour compte Azure, utiliser un script d’assistance hello avec votre autorité de certification signé le certificat, en tant que hello ci-dessous illustre de commande :

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

paramètre d’IFichier - Hello peut prendre un fichier .pfx ou un fichier .pem comme entrée, avec le type de certificat hello (pfx ou pem ou ss s’il s’agit d’un certificat auto-signé).
paramètre -h Hello imprime texte d’aide hello.


Cette commande renvoie hello suivant trois chaînes en tant que sortie de hello :

* SourceVaultID, qui est l’ID de hello pour hello nouvelle KeyVault ResourceGroup il créé pour vous
* CertificateUrl pour accéder au certificat de hello
* CertificateThumbprint, qui est utilisée pour l’authentification.

Bonjour à l’exemple suivant montre comment toouse hello commande :

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
L’exécution de hello précédant donne de commande vous hello trois chaînes comme suit :

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

nom du sujet du certificat Hello doit correspondre au domaine hello que vous utilisez cluster Service Fabric de hello tooaccess. Cette correspondance est requise tooprovide une connexion SSL pour les points de terminaison de gestion du cluster hello HTTPS et le Service Fabric Explorer. Vous ne pouvez pas obtenir un certificat SSL à partir d’une autorité de certification pour hello `.cloudapp.azure.com` domaine. Vous devez obtenir un nom de domaine personnalisé pour votre cluster. Lorsque vous demandez un certificat à partir d’une autorité de certification, hello nom du sujet du certificat doit correspondre au nom de domaine personnalisé hello que vous utilisez pour votre cluster.

Ces noms de sujet sont entrées hello toocreate un cluster Service Fabric sécurisé (sans Azure AD), comme décrit dans [les paramètres de modèle de configurer le Gestionnaire de ressources](#configure-arm). Vous pouvez vous connecter à cluster sécurisée de toohello en suivant les instructions de hello pour [l’authentification client le cluster tooa accès](service-fabric-connect-to-secure-cluster.md). Les clusters Linux en version préliminaire ne prennent pas en charge l’authentification Azure AD. Vous pouvez attribuer des rôles d’administrateur et le client comme décrit dans hello [affecter des rôles toousers](#assign-roles) section. Lorsque vous spécifiez les rôles administrateur et le client pour un cluster de version d’évaluation de Linux, vous avez tooprovide empreintes numériques de certificat pour l’authentification. (Vous ne spécifiez aucun nom de sujet hello, car aucune validation de la chaîne ou de la révocation n’est effectuée dans cette version préliminaire.)

Si vous voulez toouse un certificat auto-signé pour le test, vous pouvez utiliser hello même toogenerate script un. Vous pouvez ensuite télécharger le coffre de clés tooyour certificat hello en fournissant l’indicateur de hello `ss` au lieu de fournir le nom de chemin d’accès et le certificat du certificat hello. Par exemple, consultez hello commande pour la création et téléchargement d’un certificat auto-signé suivante :

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
Cette commande retourne hello mêmes trois chaînes : SourceVault, CertificateUrl et CertificateThumbprint. Vous pouvez ensuite utiliser hello chaînes toocreate un cluster Linux sécurisé et un emplacement où le certificat auto-signé de hello est placé. Vous avez besoin de cluster de toohello tooconnect hello certificat auto-signé. Vous pouvez vous connecter à cluster sécurisée de toohello en suivant les instructions de hello pour [l’authentification client le cluster tooa accès](service-fabric-connect-to-secure-cluster.md).

nom du sujet du certificat Hello doit correspondre au domaine hello que vous utilisez cluster Service Fabric de hello tooaccess. Cette correspondance est requise tooprovide une connexion SSL pour les points de terminaison de gestion du cluster hello HTTPS et le Service Fabric Explorer. Vous ne pouvez pas obtenir un certificat SSL à partir d’une autorité de certification pour hello `.cloudapp.azure.com` domaine. Vous devez obtenir un nom de domaine personnalisé pour votre cluster. Lorsque vous demandez un certificat à partir d’une autorité de certification, hello nom du sujet du certificat doit correspondre au nom de domaine personnalisé hello que vous utilisez pour votre cluster.

Vous pouvez remplir les paramètres de hello à partir de script d’assistance hello hello portail Azure, comme décrit dans hello [créer un cluster Bonjour Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.

## <a name="next-steps"></a>Étapes suivantes
À ce stade, vous avez un cluster sécurisé avec l’authentification de gestion fournie par Azure Active Directory. Ensuite, [connecter tooyour cluster](service-fabric-connect-to-secure-cluster.md) et découvrez comment trop[gérer les secrets de l’application](service-fabric-application-secret-management.md).

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a>Résoudre les problèmes de configuration d’Azure Active Directory pour l’authentification des clients
Si vous rencontrez un problème pendant que vous configurez Azure AD pour l’authentification du client, passez en revue les solutions possibles hello dans cette section.

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a>Service Fabric Explorer invite tooselect un certificat
#### <a name="problem"></a>Problème
Après que vous être connecté avec succès tooAzure dans l’Explorateur de l’infrastructure de Service Active Directory, navigateur de hello retourne la page d’accueil toohello mais un message vous invite à entrer tooselect un certificat.

![Boîte de dialogue SFX de sélection d’un certificat][sfx-select-certificate-dialog]

#### <a name="reason"></a>Motif
utilisateur de Hello n’est pas affecté un rôle dans hello application de cluster Azure AD. Par conséquent, l’authentification Azure AD échoue sur le cluster Service Fabric. Service Fabric Explorer revient toocertificate authentification.

#### <a name="solution"></a>Solution
Suivez les instructions de hello pour la configuration d’Azure AD, puis attribuer des rôles d’utilisateur. En outre, nous vous recommandons de tension « Utilisateur d’application affectation tooaccess requis », en tant que `SetupApplications.ps1` est.

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a>Connexion avec PowerShell échoue avec une erreur : « hello spécifié des informations d’identification ne sont pas valides »
#### <a name="problem"></a>Problème
Lorsque vous utilisez PowerShell tooconnect toohello cluster en utilisant le mode de sécurité « AzureActiveDirectory », après vous être connecté avec succès tooAzure AD, la connexion de hello échoue avec une erreur : « hello spécifié informations d’identification ne sont pas valides. »

#### <a name="solution"></a>Solution
Cette solution est hello qu'identique hello précédant une.

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a>Lorsque vous vous connectez, Service Fabric Explorer renvoie un message d’échec : « AADSTS50011 »
#### <a name="problem"></a>Problème
Lorsque vous essayez de toosign dans tooAzure AD dans l’Explorateur de l’infrastructure de Service, page de hello retourne une erreur : « AADSTS50011 : hello adresse de réponse &lt;url&gt; ne correspondent pas aux adresses de réponse de hello configurés pour l’application hello : &lt;guid&gt;."

![L’adresse de réponse SFX ne correspond pas][sfx-reply-address-not-match]

#### <a name="reason"></a>Motif
application Hello cluster (web) qui représente le Service Fabric Explorer tente tooauthenticate auprès d’Azure AD, et dans le cadre de la demande de hello fournit des URL de retour de redirection hello. Mais hello URL n’est pas répertorié dans l’application hello Azure AD **URL de réponse** liste.

#### <a name="solution"></a>Solution
Sur hello **configurer** onglet Hello application (web) de cluster, ajoutez hello URL de Service Fabric Explorer toohello **URL de réponse** répertorier ou remplacez un des éléments hello dans la liste de hello. Lorsque vous avez terminé, enregistrez vos modifications.

![URL de réponse d’application web][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a>Connecter le cluster de hello en utilisant l’authentification Azure AD via PowerShell
tooconnect hello cluster Service Fabric, utilisez hello exemple de commande PowerShell suivant :

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

toolearn sur l’applet de commande Connect-ServiceFabricCluster de hello, consultez [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a>Puis-je réutiliser locataire hello même instance Azure AD dans plusieurs clusters ?
Oui. Mais n’oubliez pas d’application de cluster (web) tooyour tooadd hello URL de Service Fabric Explorer. Si vous ne le faites pas, Service Fabric Explorer ne fonctionnera pas.

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a>Pourquoi dois-je disposer d’un certificat de serveur lorsqu’Azure AD est activé ?
FabricClient et FabricGateway effectuent une authentification mutuelle. Lors de l’authentification Azure AD, intégration d’Azure AD fournit un client serveur toohello d’identité et certificat de serveur hello est utilisé tooverify hello identité du serveur. Pour plus d’informations sur les certificats Service Fabric, consultez [Certificats X.509 et Service Fabric][x509-certificates-and-service-fabric]

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

