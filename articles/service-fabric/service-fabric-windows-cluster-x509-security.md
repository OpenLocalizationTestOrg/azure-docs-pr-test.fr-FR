---
title: "aaaSecure un Azure Service Fabric cluster sur Windows à l’aide de certificats | Documents Microsoft"
description: "Cet article décrit comment toosecure communication au sein de hello autonome ou privées de cluster ainsi qu’entre les clients et le cluster de hello."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: f0d411963615349a84edfc8125dec4ee5908f146
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a>Sécuriser un cluster autonome sur Windows à l’aide de certificats X.509
Cet article décrit comment les communications de hello toosecure entre hello différents nœuds du cluster Windows autonome, tooauthenticate les clients se connectant toothis cluster, à l’aide de certificats X.509 ainsi que comment. Cela garantit que seuls les utilisateurs autorisés peuvent accéder à cluster de hello, hello des applications déployées et effectuer des tâches de gestion.  Sécurité de certificat doit être activée sur le cluster de hello lorsque hello cluster est créé.  

Pour en savoir plus sur la sécurité de cluster, telle que la sécurité nœud à nœud, la sécurité client à nœud et le contrôle d’accès en fonction du rôle, consultez [Scénarios de sécurité du cluster](service-fabric-cluster-security.md).

## <a name="which-certificates-will-you-need"></a>Quels sont les certificats requis ?
toostart, [télécharger le package de cluster autonome hello](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone de nœuds hello dans votre cluster. Bonjour téléchargé le package, vous trouverez une **ClusterConfig.X509.MultiMachine.json** fichier. Ouvrez le fichier de hello et passez en revue la section hello pour **sécurité** sous hello **propriétés** section :

```JSON
"security": {
    "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

Cette section décrit les certificats hello dont vous avez besoin pour la sécurisation de votre cluster de Windows autonome. Si vous spécifiez un certificat de cluster, valeur hello **ClusterCredentialType** too_**X509**_. Si vous spécifiez un certificat de serveur pour les connexions externes, définissez hello **ServerCredentialType** trop_**X509**_. Mais pas obligatoire, nous vous recommandons toohave ces deux certificats pour un cluster correctement sécurisé. Si vous définissez ces valeurs trop*X509* vous devez également spécifier hello certificats correspondants ou Service Fabric lève une exception. Dans certains scénarios, vous pouvez souhaiter que toospecify hello _ClientCertificateThumbprints_ ou _ReverseProxyCertificate_. Dans ces scénarios, vous ne devez pas définir _ClusterCredentialType_ ou _ServerCredentialType_ too_X509_.


> [!NOTE]
> A [l’empreinte numérique](https://en.wikipedia.org/wiki/Public_key_fingerprint) est l’identité primaire de hello d’un certificat. Lecture [comment empreinte tooretrieve d’un certificat](https://msdn.microsoft.com/library/ms734695.aspx) toofind out empreinte hello de certificats hello que vous créez.
> 
> 

Hello tableau ci-dessous répertorie les certificats hello dont vous aurez besoin de votre configuration de cluster :

| **Paramètre CertificateInformation** | **Description** |
| --- | --- |
| ClusterCertificate |Recommandé pour l’environnement de test. Ce certificat est la communication de hello toosecure requis entre les nœuds de hello sur un cluster. Vous pouvez utiliser deux certificats différents : un certificat principal et un certificat secondaire pour la mise à niveau. Définir l’empreinte numérique hello du certificat principal de hello Bonjour **l’empreinte numérique** section et celle de hello secondaire Bonjour **ThumbprintSecondary** variables. |
| ClusterCertificateCommonNames |Recommandé pour l’environnement de production. Ce certificat est la communication de hello toosecure requis entre les nœuds de hello sur un cluster. Vous pouvez utiliser un ou deux noms communs de certificat de cluster. |
| ServerCertificate |Recommandé pour l’environnement de test. Ce certificat est présenté toohello client quand il tente de tooconnect toothis cluster. Pour plus de commodité, vous pouvez choisir toouse hello même certificat pour *ClusterCertificate* et *ServerCertificate*. Vous pouvez utiliser deux certificats de serveur différents : un certificat principal et un certificat secondaire pour la mise à niveau. Définir l’empreinte numérique hello du certificat principal de hello Bonjour **l’empreinte numérique** section et celle de hello secondaire Bonjour **ThumbprintSecondary** variables. |
| ServerCertificateCommonNames |Recommandé pour l’environnement de production. Ce certificat est présenté toohello client quand il tente de tooconnect toothis cluster. Pour plus de commodité, vous pouvez choisir toouse hello même certificat pour *ClusterCertificateCommonNames* et *ServerCertificateCommonNames*. Vous pouvez utiliser un ou deux noms communs de certificat de serveur. |
| ClientCertificateThumbprints |Il s’agit d’un jeu de certificats que vous souhaitez tooinstall sur les clients de hello authentifié. Vous pouvez avoir un nombre de certificats client différents installé sur les ordinateurs hello que vous souhaitez le cluster de toohello tooallow accès. Définir l’empreinte numérique hello de chaque certificat Bonjour **CertificateThumbprint** variable. Si vous définissez hello **IsAdmin** trop*true*, puis client hello avec ce certificat installé dessus faire administrateur des activités de gestion sur le cluster de hello. Si hello **IsAdmin** est *false*, client hello avec ce certificat ne pouvez effectuer les actions hello autorisées pour les droits d’accès utilisateur, généralement en lecture seule. Pour plus d’informations sur les rôles, consultez [Contrôle d’accès en fonction du rôle (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac) |
| ClientCertificateCommonNames |Définir hello commun le nom du certificat de client premier hello pour hello **CertificateCommonName**. Hello **CertificateIssuerThumbprint** est l’empreinte numérique hello pour émetteur hello de ce certificat. Lecture [utilisation des certificats](https://msdn.microsoft.com/library/ms731899.aspx) tooknow plus d’informations sur les noms communs et de l’émetteur de hello. |
| ReverseProxyCertificate |Recommandé pour l’environnement de test. Il s’agit d’un certificat facultatif qui peut être spécifié si vous souhaitez toosecure votre [Proxy inverse](service-fabric-reverseproxy.md). Assurez-vous que reverseProxyEndpointPort est défini dans nodeTypes, si vous utilisez ce certificat. |
| ReverseProxyCertificateCommonNames |Recommandé pour l’environnement de production. Il s’agit d’un certificat facultatif qui peut être spécifié si vous souhaitez toosecure votre [Proxy inverse](service-fabric-reverseproxy.md). Assurez-vous que reverseProxyEndpointPort est défini dans nodeTypes, si vous utilisez ce certificat. |

Voici exemple de configuration de cluster où les certificats de Cluster, serveur et Client hello ont été fournis. Notez que pour le cluster / serveur / reverseProxy certificats, l’empreinte numérique et le nom commun ne sont pas autorisés toobe configurés conjointement pour hello même type de certificat.

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace hello localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a>Renouvellement d’un certificat
Lorsque vous utilisez le nom commun du certificat au lieu de l’empreinte, le renouvellement de certificat ne requiert aucune mise à niveau de configuration de cluster.
Si le certificat intervenant implique l’émetteur substituer, Veuillez conserver au moins 2 heures après l’installation du nouveau certificat de l’émetteur hello hello ancien émetteur de cert dans le magasin de certificats hello.

## <a name="acquire-hello-x509-certificates"></a>Obtenir des certificats X.509 hello
communication toosecure au sein du cluster de hello, vous devez abord tooobtain des certificats X.509 pour vos nœuds de cluster. En outre, toolimit connexion toothis cluster tooauthorized machines/utilisateurs, vous devez tooobtain et installer des certificats pour les ordinateurs clients hello.

Pour les clusters qui exécutent des charges de travail de production, vous devez utiliser un [autorité de certification (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signés de cluster de hello de toosecure de certificat X.509. Pour plus d’informations sur l’obtention de ces certificats, consultez trop[Comment : obtenir un certificat](http://msdn.microsoft.com/library/aa702761.aspx).

Pour les clusters que vous utilisez à des fins de test, vous pouvez choisir toouse un certificat auto-signé.

## <a name="optional-create-a-self-signed-certificate"></a>Facultatif : Créer un certificat auto-signé
Une façon toocreate un certificat auto-signé qui peut être correctement sécurisé est toouse hello *CertSetup.ps1* script dans hello Service Fabric SDK dossier hello répertoire *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*. Modifier ce nom par défaut de fichier toochange hello du certificat de hello (recherchez hello valeur *CN = ServiceFabricDevClusterCert*). Exécutez ce script en tant que `.\CertSetup.ps1 -Install`.

Maintenant exporter le fichier PFX tooa du certificat hello avec un mot de passe protégé. Tout d’abord obtenir hello empreinte numérique du certificat de hello. À partir de hello *Démarrer* menu, exécutez hello *gérer les certificats d’ordinateur*. Accédez toohello **local\personnel** dossier et rechercher hello certificat que vous avez juste créé. Double-cliquez sur hello certificat tooopen il, sélectionnez hello *détails* onglet et faites défiler toohello *l’empreinte numérique* champ. Copiez la valeur d’empreinte numérique hello dans la commande PowerShell de hello ci-dessous, après la suppression des espaces de hello.  Hello de modification `String` valeur tooa approprié de mot de passe sécurisé tooprotect et exécution hello suivant dans PowerShell :

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

Détails de hello toosee d’un certificat installé sur hello machine que vous pouvez exécuter hello suivant de commande PowerShell :

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

Ou bien, si vous avez un abonnement Azure, suivez la section de hello [ajouter des certificats tooKey coffre](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).

## <a name="install-hello-certificates"></a>Installer des certificats de hello
Une fois que vous avez ou les certificats, vous pouvez les installer sur les nœuds de cluster hello. Vos nœuds doivent toohave hello plus récente de Windows PowerShell 3.x sur lesquels est installé. Vous devez toorepeat ces étapes sur chaque nœud, pour les certificats de Cluster et le serveur et tous les certificats secondaires.

1. Nœud de toohello pour les fichiers .pfx copie hello.
2. Ouvrez une fenêtre PowerShell en tant qu’administrateur et entrez hello suivant les commandes. Remplacez hello *$pswd* avec mot de passe hello que vous avez utilisé toocreate ce certificat. Remplacez hello *$PfxFilePath* avec le chemin complet de hello du nœud de hello .pfx toothis copié.
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. Maintenant définir le contrôle d’accès hello sur ce certificat afin que le processus de Service Fabric hello, qui s’exécute sous hello compte Service réseau, peut l’utiliser en exécutant le script suivant de hello. Fournissez l’empreinte numérique hello hello certificat d’et « SERVICE réseau » pour le compte de service hello. Vous pouvez vérifier que hello ACL sur le certificat de hello sont corrects en ouvrant le certificat hello dans *Démarrer* > *gérer les certificats d’ordinateur* et en examinant *toutes les tâches*  >  *Gérer les clés privées*.
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify hello user, hello permissions and hello permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of hello machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get hello current acl of hello private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add hello new ace toohello acl of hello private key
    $acl.SetAccessRule($accessRule)
   
    # Write back hello new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe hello access rights currently assigned toothis certificate.
    get-acl $keyFullPath| fl
    ```
4. Répétez les étapes hello pour chaque certificat de serveur. Vous pouvez également utiliser ces étapes tooinstall hello certificats clients sur des ordinateurs de hello que vous souhaitez le cluster de toohello tooallow accès.

## <a name="create-hello-secure-cluster"></a>Créer le cluster sécurisée de hello
Après avoir configuré hello **sécurité** section Hello **ClusterConfig.X509.MultiMachine.json** fichier, vous pouvez passer trop[créez votre cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) tooconfigure de section Hello nœuds et créer le cluster de hello autonome. N’oubliez pas de toouse hello **ClusterConfig.X509.MultiMachine.json** fichier lors de la création du cluster de hello. Par exemple, votre commande peut ressembler à hello suivantes :

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

Une fois que vous avez hello sécurisé autonome Windows cluster en cours d’exécution et ont le programme d’installation Bonjour des clients authentifiés tooconnect tooit, suivez hello section [cluster sécurisée du tooa se connecter à l’aide de PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit. Par exemple :

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

Vous pouvez ensuite exécuter autres toowork de commandes PowerShell avec ce cluster. Par exemple, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow une liste de nœuds sur ce cluster sécurisé.


cluster de hello tooremove, connecter nœud toohello sur cluster hello où vous avez téléchargé le package de Service Fabric hello, ouvrez une ligne de commande et accédez toohello dossier du package. Maintenant, exécutez hello de commande suivante :

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> Configuration du certificat incorrect peut empêcher le prochaines évolutions et durant le déploiement de cluster de hello. tooself-diagnostiquer les problèmes de sécurité, recherchez dans le groupe Observateur d’événements *journaux des Applications et Services* > *Microsoft Service Fabric*.
> 
> 

