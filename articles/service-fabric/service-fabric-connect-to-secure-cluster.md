---
title: "aaaConnect en toute sécurité le cluster de Azure Service Fabric tooan | Documents Microsoft"
description: "Décrit comment tooauthenticate client accéder au cluster Service Fabric de tooa et toosecure la communication entre les clients et d’un cluster."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 759a539e-e5e6-4055-bff5-d38804656e10
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 1b6a87a1fefaddce2043c604ca53751157232170
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-cluster"></a>Connecter le cluster sécurisée de tooa

Lorsqu’un client connecte à nœud de cluster Service Fabric tooa, client de hello peut être établie à l’aide de la sécurité des certificats ou Azure Active Directory (AAD) une communication authentifiée et sécurisée. Cette authentification permet de s’assurer que seuls les utilisateurs autorisés peuvent accéder au cluster de hello et des applications déploiement et effectuent des tâches de gestion.  Certificat ou la sécurité AAD doit avoir été précédemment activée sur le cluster de hello lorsque hello cluster a été créé.  Pour plus d’informations sur les scénarios de sécurité des clusters, consultez [Sécurité des clusters](service-fabric-cluster-security.md). Si vous vous connectez le cluster tooa sécurisé avec des certificats [installer le certificat de client hello](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) sur ordinateur hello qui se connecte toohello cluster. 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a>Se connecter tooa cluster sécurisée à l’aide d’Azure Service Fabric CLI (sfctl)

Il n’y a cluster sécurisée tooa différentes façons tooconnect quelques à l’aide de hello Service Fabric CLI (sfctl). Lorsque vous utilisez un certificat client pour l’authentification, certificat hello détails doivent correspondre à un certificat déployé toohello les nœuds de cluster. Si votre certificat a des autorités de certification (CA), vous devez tooadditionally spécifier hello des autorités de certification de confiance.

Vous pouvez vous connecter à cluster tooa à l’aide de hello `sfctl cluster select` commande.

Les certificats clients peuvent être spécifiés de deux façons différentes : en tant que paire certificat/clé ou en tant que fichier .pem unique. Mot de passe protégé `pem` fichiers, vous serez invité à entrer le mot de passe tooenter hello automatiquement.

certificat de client hello toospecify qu’un fichier pem, spécifier le chemin d’accès du fichier hello Bonjour `--pem` argument. Par exemple :

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Fichiers pem de mot de passe protégé demande toorunning préalable de mot de passe n’importe quelle commande.

toospecify un certificat, la paire de clés utilisent hello `--cert` et `--key` arguments toospecify hello des chemins d’accès tooeach respectifs du fichier.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

Parfois, les certificats utilisés toosecure test ou développement clusters la validation de certificat échouent. toobypass certificat de vérification, spécifiez hello `--no-verify` option. Par exemple :

> [!WARNING]
> N’utilisez pas hello `no-verify` option lors de la connexion tooproduction Service Fabric clusters.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

En outre, vous pouvez spécifier toodirectories de chemins d’accès des certificats d’autorité de certification approuvées ou des certificats. toospecify ces chemins d’accès, utilisez hello `--ca` argument. Par exemple :

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

Une fois que vous vous connectez, vous devez être en mesure de trop[exécuter d’autres commandes sfctl](service-fabric-cli.md) toointeract avec cluster de hello.

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a>Connecter le cluster tooa à l’aide de PowerShell
Avant d’effectuer des opérations sur un cluster via PowerShell, tout d’abord établir un cluster de toohello de connexion. connexion du cluster Hello est utilisée pour toutes les commandes suivantes dans hello donné session PowerShell.

### <a name="connect-tooan-unsecure-cluster"></a>Se connecter tooan des clusters non sécurisés

tooan tooconnect non sécurisée de cluster, fournir hello cluster point de terminaison adresse toohello **Connect-ServiceFabricCluster** commande :

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Se connecter tooa cluster sécurisée à l’aide d’Azure Active Directory

tooconnect tooa sécurisée qui utilise l’accès d’administrateur Azure Active Directory tooauthorize cluster, fournissez l’empreinte numérique du certificat hello cluster et cluster hello *AzureActiveDirectory* indicateur.  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Se connecter tooa cluster sécurisée à l’aide d’un certificat client
Exécution hello suivant de commande PowerShell de cluster tooa tooconnect sécurisé qui utilise l’accès d’administrateur client certificats tooauthorize. Fournir l’empreinte numérique du certificat hello cluster et l’empreinte numérique hello du certificat client hello qui dispose des autorisations pour la gestion de cluster. Détails du certificat Hello doivent correspondre à un certificat sur les nœuds de cluster hello.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

*ServerCertThumbprint* est l’empreinte numérique hello du certificat de serveur hello installé sur les nœuds de cluster hello. *FindValue* est l’empreinte numérique hello du certificat de client hello admin.
Lorsque les paramètres de hello sont renseignés, commande hello ressemble hello l’exemple suivant : 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a>Se connecter tooa cluster sécurisée à l’aide de Windows Active Directory
Si votre cluster autonome est déployé à l’aide de la sécurité d’Active Directory, connecter toohello cluster en ajoutant le commutateur hello « WindowsCredential ».

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a>Connecter le cluster tooa à l’aide de hello FabricClient APIs
Hello Service Fabric SDK fournit hello [fabricclient ne](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) classe pour la gestion de cluster. toouse hello fabricclient n’APIs, obtenir hello package NuGet de Microsoft.ServiceFabric.

### <a name="connect-tooan-unsecure-cluster"></a>Se connecter tooan des clusters non sécurisés

tooconnect tooa non sécurisé de cluster distant, créez une instance de fabricclient n’et fournir l’adresse du cluster hello :

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

Pour le code qui s’exécute à partir d’un cluster, par exemple, dans un Service fiable, créer un fabricclient ne *sans* spécifiant l’adresse du cluster hello. Fabricclient ne connecte la gestion locale des toohello code hello du nœud hello la passerelle est en cours d’exécution, ce qui évite un saut de réseau supplémentaire.

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Se connecter tooa cluster sécurisée à l’aide d’un certificat client

nœuds Hello dans un cluster de hello doivent avoir des certificats valides dont le nom commun ou nom DNS SAN s’affiche dans hello [RemoteCommonNames propriété](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) définie sur [fabricclient ne](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient). Ce processus permet une authentification mutuelle entre le client de hello et les nœuds de cluster hello.

```csharp
using System.Fabric;
using System.Security.Cryptography.X509Certificates;

string clientCertThumb = "71DE04467C9ED0544D021098BCD44C71E183414E";
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string CommonName = "www.clustername.westus.azure.com";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var xc = GetCredentials(clientCertThumb, serverCertThumb, CommonName);
var fc = new FabricClient(xc, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

static X509Credentials GetCredentials(string clientCertThumb, string serverCertThumb, string name)
{
    X509Credentials xc = new X509Credentials();
    xc.StoreLocation = StoreLocation.CurrentUser;
    xc.StoreName = "My";
    xc.FindType = X509FindType.FindByThumbprint;
    xc.FindValue = clientCertThumb;
    xc.RemoteCommonNames.Add(name);
    xc.RemoteCertThumbprints.Add(serverCertThumb);
    xc.ProtectionLevel = ProtectionLevel.EncryptAndSign;
    return xc;
}
```

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a>Se connecter tooa cluster sécurisée interactive à l’aide d’Azure Active Directory

Hello suivant l’exemple suivant utilise Azure Active Directory pour le certificat d’identité et de serveur pour l’identité du serveur.

Une fenêtre de dialogue s’ouvre automatiquement pour la connexion interactive lors de la connexion toohello cluster.

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}
```

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a>Se connecter tooa cluster sécurisée en mode non interactif à l’aide d’Azure Active Directory

Hello exemple suivant s’appuie sur Microsoft.IdentityModel.Clients.ActiveDirectory, Version : 2.19.208020213.

Pour plus d’informations sur l’acquisition d’un jeton AAD, consultez [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).

```csharp
string tenantId = "C15CFCEA-02C1-40DC-8466-FBD0EE0B05D2";
string clientApplicationId = "118473C2-7619-46E3-A8E4-6DA8D5F56E12";
string webApplicationId = "53E6948C-0897-4DA6-B26A-EE2A38A690B4";

string token = GetAccessToken(
    tenantId,
    webApplicationId,
    clientApplicationId,
    "urn:ietf:wg:oauth:2.0:oob");

string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);
claimsCredentials.LocalClaims = token;

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(
    string tenantId,
    string resource,
    string clientId,
    string redirectUri)
{
    string authorityFormat = @"https://login.microsoftonline.com/{0}";
    string authority = string.Format(CultureInfo.InvariantCulture, authorityFormat, tenantId);
    var authContext = new AuthenticationContext(authority);

    var authResult = authContext.AcquireToken(
        resource,
        clientId,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a>Connecter le cluster sécurisée de tooa sans connaissance préalable de métadonnées à l’aide d’Azure Active Directory

Hello exemple suivant utilise une acquisition de jeton non interactif, mais hello même approche peut être utilisé toobuild une expérience de l’acquisition de jeton interactif personnalisé. métadonnées d’Azure Active Directory Hello nécessaire pour l’acquisition de jeton sont lu à partir de la configuration du cluster.

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

fc.ClaimsRetrieval += (o, e) =>
{
    return GetAccessToken(e.AzureActiveDirectoryMetadata);
};

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(AzureActiveDirectoryMetadata aad)
{
    var authContext = new AuthenticationContext(aad.Authority);

    var authResult = authContext.AcquireToken(
        aad.ClusterApplication,
        aad.ClientApplication,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

<a id="connectsecureclustersfx"></a>

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a>Se connecter tooa cluster sécurisée à l’aide du Service Fabric Explorer
tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) pour un cluster donné, pointez votre navigateur sur :

`http://<your-cluster-endpoint>:19080/Explorer`

URL complète de Hello est également disponible dans hello cluster essentials volet Hello portail Azure.

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Se connecter tooa cluster sécurisée à l’aide d’Azure Active Directory

tooconnect tooa cluster qui est sécurisée avec AAD, pointez votre navigateur sur :

`https://<your-cluster-endpoint>:19080/Explorer`

Vous sont automatiquement être invité à toolog avec AAD.

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Se connecter tooa cluster sécurisée à l’aide d’un certificat client

cluster tooa tooconnect sécurisé avec des certificats, pointez votre navigateur sur :

`https://<your-cluster-endpoint>:19080/Explorer`

Vous sont automatiquement être invité à tooselect un certificat client.

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a>Configurer un certificat client sur l’ordinateur distant de hello
Au moins deux certificats doivent être utilisés pour sécuriser le cluster de hello, une pour le certificat de cluster et serveur hello et l’autre pour l’accès client.  Nous vous recommandons d’utiliser également des certificats secondaires supplémentaires et des certificats d’accès client.  sécurité de certificat de communication de hello toosecure entre un client et un nœud de cluster à l’aide, vous devez tooobtain et installez le certificat de client hello le. certificat de Hello peut être installé dans hello (My) magasin personnel de l’ordinateur local de hello ou l’utilisateur actuel de hello.  Vous devez également l’empreinte numérique hello hello du certificat de serveur afin que hello client peut s’authentifier cluster de hello.

Exécutez hello suivant tooset d’applet de commande PowerShell de certificat de client hello sur ordinateur hello à partir de laquelle vous accéder au cluster de hello.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

S’il s’agit d’un certificat auto-signé, vous devez tooimport il « personnes de confiance « tooyour de l’ordinateur stocker avant de pouvoir utiliser ce cluster sécurisée de certificat tooconnect tooa.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a>Étapes suivantes

* [Processus de mise à niveau du cluster Service Fabric et attentes à votre égard](service-fabric-cluster-upgrade.md)
* [Gestion de vos applications Service Fabric dans Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Présentation du modèle d’intégrité de Service Fabric](service-fabric-health-introduction.md)
* [Sécurité des applications et RunAs](service-fabric-application-runas-security.md)
* [Prise en main de l’interface de ligne de commande Service Fabric](service-fabric-cli.md)
