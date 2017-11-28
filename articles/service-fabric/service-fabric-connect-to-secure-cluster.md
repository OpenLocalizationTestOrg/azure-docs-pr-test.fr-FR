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
# <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="a2276-103">Connecter le cluster sécurisée de tooa</span><span class="sxs-lookup"><span data-stu-id="a2276-103">Connect tooa secure cluster</span></span>

<span data-ttu-id="a2276-104">Lorsqu’un client connecte à nœud de cluster Service Fabric tooa, client de hello peut être établie à l’aide de la sécurité des certificats ou Azure Active Directory (AAD) une communication authentifiée et sécurisée.</span><span class="sxs-lookup"><span data-stu-id="a2276-104">When a client connects tooa Service Fabric cluster node, hello client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="a2276-105">Cette authentification permet de s’assurer que seuls les utilisateurs autorisés peuvent accéder au cluster de hello et des applications déploiement et effectuent des tâches de gestion.</span><span class="sxs-lookup"><span data-stu-id="a2276-105">This authentication ensures that only authorized users can access hello cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="a2276-106">Certificat ou la sécurité AAD doit avoir été précédemment activée sur le cluster de hello lorsque hello cluster a été créé.</span><span class="sxs-lookup"><span data-stu-id="a2276-106">Certificate or AAD security must have been previously enabled on hello cluster when hello cluster was created.</span></span>  <span data-ttu-id="a2276-107">Pour plus d’informations sur les scénarios de sécurité des clusters, consultez [Sécurité des clusters](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="a2276-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="a2276-108">Si vous vous connectez le cluster tooa sécurisé avec des certificats [installer le certificat de client hello](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) sur ordinateur hello qui se connecte toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="a2276-108">If you are connecting tooa cluster secured with certificates, [set up hello client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on hello computer that connects toohello cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="a2276-109">Se connecter tooa cluster sécurisée à l’aide d’Azure Service Fabric CLI (sfctl)</span><span class="sxs-lookup"><span data-stu-id="a2276-109">Connect tooa secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="a2276-110">Il n’y a cluster sécurisée tooa différentes façons tooconnect quelques à l’aide de hello Service Fabric CLI (sfctl).</span><span class="sxs-lookup"><span data-stu-id="a2276-110">There are a few different ways tooconnect tooa secure cluster using hello Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="a2276-111">Lorsque vous utilisez un certificat client pour l’authentification, certificat hello détails doivent correspondre à un certificat déployé toohello les nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="a2276-111">When using a client certificate for authentication, hello certificate details must match a certificate deployed toohello cluster nodes.</span></span> <span data-ttu-id="a2276-112">Si votre certificat a des autorités de certification (CA), vous devez tooadditionally spécifier hello des autorités de certification de confiance.</span><span class="sxs-lookup"><span data-stu-id="a2276-112">If your certificate has Certificate Authorities (CAs), you need tooadditionally specify hello trusted CAs.</span></span>

<span data-ttu-id="a2276-113">Vous pouvez vous connecter à cluster tooa à l’aide de hello `sfctl cluster select` commande.</span><span class="sxs-lookup"><span data-stu-id="a2276-113">You can connect tooa cluster using hello `sfctl cluster select` command.</span></span>

<span data-ttu-id="a2276-114">Les certificats clients peuvent être spécifiés de deux façons différentes : en tant que paire certificat/clé ou en tant que fichier .pem unique.</span><span class="sxs-lookup"><span data-stu-id="a2276-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="a2276-115">Mot de passe protégé `pem` fichiers, vous serez invité à entrer le mot de passe tooenter hello automatiquement.</span><span class="sxs-lookup"><span data-stu-id="a2276-115">For password protected `pem` files, you will be prompted automatically tooenter hello password.</span></span>

<span data-ttu-id="a2276-116">certificat de client hello toospecify qu’un fichier pem, spécifier le chemin d’accès du fichier hello Bonjour `--pem` argument.</span><span class="sxs-lookup"><span data-stu-id="a2276-116">toospecify hello client certificate as a pem file, specify hello file path in hello `--pem` argument.</span></span> <span data-ttu-id="a2276-117">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a2276-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="a2276-118">Fichiers pem de mot de passe protégé demande toorunning préalable de mot de passe n’importe quelle commande.</span><span class="sxs-lookup"><span data-stu-id="a2276-118">Password protected pem files will prompt for password prior toorunning any command.</span></span>

<span data-ttu-id="a2276-119">toospecify un certificat, la paire de clés utilisent hello `--cert` et `--key` arguments toospecify hello des chemins d’accès tooeach respectifs du fichier.</span><span class="sxs-lookup"><span data-stu-id="a2276-119">toospecify a cert, key pair use hello `--cert` and `--key` arguments toospecify hello file paths tooeach respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="a2276-120">Parfois, les certificats utilisés toosecure test ou développement clusters la validation de certificat échouent.</span><span class="sxs-lookup"><span data-stu-id="a2276-120">Sometimes certificates used toosecure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="a2276-121">toobypass certificat de vérification, spécifiez hello `--no-verify` option.</span><span class="sxs-lookup"><span data-stu-id="a2276-121">toobypass certificate verification, specify hello `--no-verify` option.</span></span> <span data-ttu-id="a2276-122">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a2276-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="a2276-123">N’utilisez pas hello `no-verify` option lors de la connexion tooproduction Service Fabric clusters.</span><span class="sxs-lookup"><span data-stu-id="a2276-123">Do not use hello `no-verify` option when connecting tooproduction Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="a2276-124">En outre, vous pouvez spécifier toodirectories de chemins d’accès des certificats d’autorité de certification approuvées ou des certificats.</span><span class="sxs-lookup"><span data-stu-id="a2276-124">In addition, you can specify paths toodirectories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="a2276-125">toospecify ces chemins d’accès, utilisez hello `--ca` argument.</span><span class="sxs-lookup"><span data-stu-id="a2276-125">toospecify these paths, use hello `--ca` argument.</span></span> <span data-ttu-id="a2276-126">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a2276-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="a2276-127">Une fois que vous vous connectez, vous devez être en mesure de trop[exécuter d’autres commandes sfctl](service-fabric-cli.md) toointeract avec cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a2276-127">After you connect, you should be able too[run other sfctl commands](service-fabric-cli.md) toointeract with hello cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a><span data-ttu-id="a2276-128">Connecter le cluster tooa à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2276-128">Connect tooa cluster using PowerShell</span></span>
<span data-ttu-id="a2276-129">Avant d’effectuer des opérations sur un cluster via PowerShell, tout d’abord établir un cluster de toohello de connexion.</span><span class="sxs-lookup"><span data-stu-id="a2276-129">Before you perform operations on a cluster through PowerShell, first establish a connection toohello cluster.</span></span> <span data-ttu-id="a2276-130">connexion du cluster Hello est utilisée pour toutes les commandes suivantes dans hello donné session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2276-130">hello cluster connection is used for all subsequent commands in hello given PowerShell session.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="a2276-131">Se connecter tooan des clusters non sécurisés</span><span class="sxs-lookup"><span data-stu-id="a2276-131">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="a2276-132">tooan tooconnect non sécurisée de cluster, fournir hello cluster point de terminaison adresse toohello **Connect-ServiceFabricCluster** commande :</span><span class="sxs-lookup"><span data-stu-id="a2276-132">tooconnect tooan unsecure cluster, provide hello cluster endpoint address toohello **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="a2276-133">Se connecter tooa cluster sécurisée à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2276-133">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="a2276-134">tooconnect tooa sécurisée qui utilise l’accès d’administrateur Azure Active Directory tooauthorize cluster, fournissez l’empreinte numérique du certificat hello cluster et cluster hello *AzureActiveDirectory* indicateur.</span><span class="sxs-lookup"><span data-stu-id="a2276-134">tooconnect tooa secure cluster that uses Azure Active Directory tooauthorize cluster administrator access, provide hello cluster certificate thumbprint and use hello *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="a2276-135">Se connecter tooa cluster sécurisée à l’aide d’un certificat client</span><span class="sxs-lookup"><span data-stu-id="a2276-135">Connect tooa secure cluster using a client certificate</span></span>
<span data-ttu-id="a2276-136">Exécution hello suivant de commande PowerShell de cluster tooa tooconnect sécurisé qui utilise l’accès d’administrateur client certificats tooauthorize.</span><span class="sxs-lookup"><span data-stu-id="a2276-136">Run hello following PowerShell command tooconnect tooa secure cluster that uses client certificates tooauthorize administrator access.</span></span> <span data-ttu-id="a2276-137">Fournir l’empreinte numérique du certificat hello cluster et l’empreinte numérique hello du certificat client hello qui dispose des autorisations pour la gestion de cluster.</span><span class="sxs-lookup"><span data-stu-id="a2276-137">Provide hello cluster certificate thumbprint and hello thumbprint of hello client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="a2276-138">Détails du certificat Hello doivent correspondre à un certificat sur les nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a2276-138">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="a2276-139">*ServerCertThumbprint* est l’empreinte numérique hello du certificat de serveur hello installé sur les nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a2276-139">*ServerCertThumbprint* is hello thumbprint of hello server certificate installed on hello cluster nodes.</span></span> <span data-ttu-id="a2276-140">*FindValue* est l’empreinte numérique hello du certificat de client hello admin.</span><span class="sxs-lookup"><span data-stu-id="a2276-140">*FindValue* is hello thumbprint of hello admin client certificate.</span></span>
<span data-ttu-id="a2276-141">Lorsque les paramètres de hello sont renseignés, commande hello ressemble hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="a2276-141">When hello parameters are filled in, hello command looks like hello following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="a2276-142">Se connecter tooa cluster sécurisée à l’aide de Windows Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2276-142">Connect tooa secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="a2276-143">Si votre cluster autonome est déployé à l’aide de la sécurité d’Active Directory, connecter toohello cluster en ajoutant le commutateur hello « WindowsCredential ».</span><span class="sxs-lookup"><span data-stu-id="a2276-143">If your standalone cluster is deployed using AD security, connect toohello cluster by appending hello switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a><span data-ttu-id="a2276-144">Connecter le cluster tooa à l’aide de hello FabricClient APIs</span><span class="sxs-lookup"><span data-stu-id="a2276-144">Connect tooa cluster using hello FabricClient APIs</span></span>
<span data-ttu-id="a2276-145">Hello Service Fabric SDK fournit hello [fabricclient ne](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) classe pour la gestion de cluster.</span><span class="sxs-lookup"><span data-stu-id="a2276-145">hello Service Fabric SDK provides hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="a2276-146">toouse hello fabricclient n’APIs, obtenir hello package NuGet de Microsoft.ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="a2276-146">toouse hello FabricClient APIs, get hello Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="a2276-147">Se connecter tooan des clusters non sécurisés</span><span class="sxs-lookup"><span data-stu-id="a2276-147">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="a2276-148">tooconnect tooa non sécurisé de cluster distant, créez une instance de fabricclient n’et fournir l’adresse du cluster hello :</span><span class="sxs-lookup"><span data-stu-id="a2276-148">tooconnect tooa remote unsecured cluster, create a FabricClient instance and provide hello cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="a2276-149">Pour le code qui s’exécute à partir d’un cluster, par exemple, dans un Service fiable, créer un fabricclient ne *sans* spécifiant l’adresse du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a2276-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying hello cluster address.</span></span> <span data-ttu-id="a2276-150">Fabricclient ne connecte la gestion locale des toohello code hello du nœud hello la passerelle est en cours d’exécution, ce qui évite un saut de réseau supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="a2276-150">FabricClient connects toohello local management gateway on hello node hello code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="a2276-151">Se connecter tooa cluster sécurisée à l’aide d’un certificat client</span><span class="sxs-lookup"><span data-stu-id="a2276-151">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="a2276-152">nœuds Hello dans un cluster de hello doivent avoir des certificats valides dont le nom commun ou nom DNS SAN s’affiche dans hello [RemoteCommonNames propriété](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) définie sur [fabricclient ne](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="a2276-152">hello nodes in hello cluster must have valid certificates whose common name or DNS name in SAN appears in hello [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="a2276-153">Ce processus permet une authentification mutuelle entre le client de hello et les nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a2276-153">Following this process enables mutual authentication between hello client and hello cluster nodes.</span></span>

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

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="a2276-154">Se connecter tooa cluster sécurisée interactive à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2276-154">Connect tooa secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="a2276-155">Hello suivant l’exemple suivant utilise Azure Active Directory pour le certificat d’identité et de serveur pour l’identité du serveur.</span><span class="sxs-lookup"><span data-stu-id="a2276-155">hello following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="a2276-156">Une fenêtre de dialogue s’ouvre automatiquement pour la connexion interactive lors de la connexion toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="a2276-156">A dialog window automatically pops up for interactive sign-in upon connecting toohello cluster.</span></span>

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

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="a2276-157">Se connecter tooa cluster sécurisée en mode non interactif à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2276-157">Connect tooa secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="a2276-158">Hello exemple suivant s’appuie sur Microsoft.IdentityModel.Clients.ActiveDirectory, Version : 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="a2276-158">hello following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="a2276-159">Pour plus d’informations sur l’acquisition d’un jeton AAD, consultez [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2276-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

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

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="a2276-160">Connecter le cluster sécurisée de tooa sans connaissance préalable de métadonnées à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2276-160">Connect tooa secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="a2276-161">Hello exemple suivant utilise une acquisition de jeton non interactif, mais hello même approche peut être utilisé toobuild une expérience de l’acquisition de jeton interactif personnalisé.</span><span class="sxs-lookup"><span data-stu-id="a2276-161">hello following example uses non-interactive token acquisition, but hello same approach can be used toobuild a custom interactive token acquisition experience.</span></span> <span data-ttu-id="a2276-162">métadonnées d’Azure Active Directory Hello nécessaire pour l’acquisition de jeton sont lu à partir de la configuration du cluster.</span><span class="sxs-lookup"><span data-stu-id="a2276-162">hello Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

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

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="a2276-163">Se connecter tooa cluster sécurisée à l’aide du Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="a2276-163">Connect tooa secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="a2276-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) pour un cluster donné, pointez votre navigateur sur :</span><span class="sxs-lookup"><span data-stu-id="a2276-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="a2276-165">URL complète de Hello est également disponible dans hello cluster essentials volet Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a2276-165">hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="a2276-166">Se connecter tooa cluster sécurisée à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2276-166">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="a2276-167">tooconnect tooa cluster qui est sécurisée avec AAD, pointez votre navigateur sur :</span><span class="sxs-lookup"><span data-stu-id="a2276-167">tooconnect tooa cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="a2276-168">Vous sont automatiquement être invité à toolog avec AAD.</span><span class="sxs-lookup"><span data-stu-id="a2276-168">You are automatically be prompted toolog in with AAD.</span></span>

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="a2276-169">Se connecter tooa cluster sécurisée à l’aide d’un certificat client</span><span class="sxs-lookup"><span data-stu-id="a2276-169">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="a2276-170">cluster tooa tooconnect sécurisé avec des certificats, pointez votre navigateur sur :</span><span class="sxs-lookup"><span data-stu-id="a2276-170">tooconnect tooa cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="a2276-171">Vous sont automatiquement être invité à tooselect un certificat client.</span><span class="sxs-lookup"><span data-stu-id="a2276-171">You are automatically be prompted tooselect a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a><span data-ttu-id="a2276-172">Configurer un certificat client sur l’ordinateur distant de hello</span><span class="sxs-lookup"><span data-stu-id="a2276-172">Set up a client certificate on hello remote computer</span></span>
<span data-ttu-id="a2276-173">Au moins deux certificats doivent être utilisés pour sécuriser le cluster de hello, une pour le certificat de cluster et serveur hello et l’autre pour l’accès client.</span><span class="sxs-lookup"><span data-stu-id="a2276-173">At least two certificates should be used for securing hello cluster, one for hello cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="a2276-174">Nous vous recommandons d’utiliser également des certificats secondaires supplémentaires et des certificats d’accès client.</span><span class="sxs-lookup"><span data-stu-id="a2276-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="a2276-175">sécurité de certificat de communication de hello toosecure entre un client et un nœud de cluster à l’aide, vous devez tooobtain et installez le certificat de client hello le.</span><span class="sxs-lookup"><span data-stu-id="a2276-175">toosecure hello communication between a client and a cluster node using certificate security, you first need tooobtain and install hello client certificate.</span></span> <span data-ttu-id="a2276-176">certificat de Hello peut être installé dans hello (My) magasin personnel de l’ordinateur local de hello ou l’utilisateur actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="a2276-176">hello certificate can be installed into hello Personal (My) store of hello local computer or hello current user.</span></span>  <span data-ttu-id="a2276-177">Vous devez également l’empreinte numérique hello hello du certificat de serveur afin que hello client peut s’authentifier cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a2276-177">You also need hello thumbprint of hello server certificate so that hello client can authenticate hello cluster.</span></span>

<span data-ttu-id="a2276-178">Exécutez hello suivant tooset d’applet de commande PowerShell de certificat de client hello sur ordinateur hello à partir de laquelle vous accéder au cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a2276-178">Run hello following PowerShell cmdlet tooset up hello client certificate on hello computer from which you access hello cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="a2276-179">S’il s’agit d’un certificat auto-signé, vous devez tooimport il « personnes de confiance « tooyour de l’ordinateur stocker avant de pouvoir utiliser ce cluster sécurisée de certificat tooconnect tooa.</span><span class="sxs-lookup"><span data-stu-id="a2276-179">If it is a self-signed certificate, you need tooimport it tooyour machine's "trusted people" store before you can use this certificate tooconnect tooa secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="a2276-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a2276-180">Next steps</span></span>

* [<span data-ttu-id="a2276-181">Processus de mise à niveau du cluster Service Fabric et attentes à votre égard</span><span class="sxs-lookup"><span data-stu-id="a2276-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="a2276-182">Gestion de vos applications Service Fabric dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a2276-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="a2276-183">Présentation du modèle d’intégrité de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a2276-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="a2276-184">Sécurité des applications et RunAs</span><span class="sxs-lookup"><span data-stu-id="a2276-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="a2276-185">Prise en main de l’interface de ligne de commande Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a2276-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
