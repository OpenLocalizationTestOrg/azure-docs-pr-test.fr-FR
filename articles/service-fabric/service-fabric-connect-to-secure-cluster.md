---
title: "Connexion sécurisée à un cluster Azure Service Fabric | Microsoft Docs"
description: "Décrit comment authentifier l’accès client à un cluster Service Fabric et comment sécuriser les communications entre les clients et un cluster."
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
ms.openlocfilehash: d6a13ceb8ccd9207ecacc166247535d496d5dec7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="2a26f-103">Se connecter à un cluster sécurisé</span><span class="sxs-lookup"><span data-stu-id="2a26f-103">Connect to a secure cluster</span></span>

<span data-ttu-id="2a26f-104">Lorsqu’un client se connecte à un nœud de cluster Service Fabric, il peut être authentifié et une communication sécurisée peut être établie à l’aide de la sécurité par certificat ou d’Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="2a26f-104">When a client connects to a Service Fabric cluster node, the client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="2a26f-105">Cette authentification garantit que seuls les utilisateurs autorisés puissent accéder au cluster et aux applications déployées, et effectuer des tâches de gestion.</span><span class="sxs-lookup"><span data-stu-id="2a26f-105">This authentication ensures that only authorized users can access the cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="2a26f-106">La sécurité par certificat ou AAD doit avoir été précédemment activé sur le cluster à sa création.</span><span class="sxs-lookup"><span data-stu-id="2a26f-106">Certificate or AAD security must have been previously enabled on the cluster when the cluster was created.</span></span>  <span data-ttu-id="2a26f-107">Pour plus d’informations sur les scénarios de sécurité des clusters, consultez [Sécurité des clusters](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="2a26f-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="2a26f-108">Si vous vous connectez à un cluster sécurisé avec des certificats, [configurez le certificat client](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) sur l’ordinateur qui se connecte au cluster.</span><span class="sxs-lookup"><span data-stu-id="2a26f-108">If you are connecting to a cluster secured with certificates, [set up the client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on the computer that connects to the cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-to-a-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="2a26f-109">Se connecter à un cluster sécurisé à l’aide de l’interface CLI Azure Service Fabric (sfctl)</span><span class="sxs-lookup"><span data-stu-id="2a26f-109">Connect to a secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="2a26f-110">Il existe différentes manières de se connecter à un cluster sécurisé à l’aide de l’interface CLI Service Fabric (sfctl).</span><span class="sxs-lookup"><span data-stu-id="2a26f-110">There are a few different ways to connect to a secure cluster using the Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="2a26f-111">Lorsque vous utilisez un certificat client pour l’authentification, les détails du certificat doivent correspondre à un certificat déployé sur les nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="2a26f-111">When using a client certificate for authentication, the certificate details must match a certificate deployed to the cluster nodes.</span></span> <span data-ttu-id="2a26f-112">Si votre certificat dispose d’autorités de certification, vous devez également spécifier les autorités de certification approuvées.</span><span class="sxs-lookup"><span data-stu-id="2a26f-112">If your certificate has Certificate Authorities (CAs), you need to additionally specify the trusted CAs.</span></span>

<span data-ttu-id="2a26f-113">Vous pouvez vous connecter à un cluster à l’aide de la commande `sfctl cluster select`.</span><span class="sxs-lookup"><span data-stu-id="2a26f-113">You can connect to a cluster using the `sfctl cluster select` command.</span></span>

<span data-ttu-id="2a26f-114">Les certificats clients peuvent être spécifiés de deux façons différentes : en tant que paire certificat/clé ou en tant que fichier .pem unique.</span><span class="sxs-lookup"><span data-stu-id="2a26f-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="2a26f-115">Pour les fichiers `pem` protégés par mot de passe, vous serez automatiquement invité à entrer le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="2a26f-115">For password protected `pem` files, you will be prompted automatically to enter the password.</span></span>

<span data-ttu-id="2a26f-116">Pour spécifier le certificat client en tant que fichier .pem, spécifiez le chemin d’accès de fichier dans l’argument `--pem`.</span><span class="sxs-lookup"><span data-stu-id="2a26f-116">To specify the client certificate as a pem file, specify the file path in the `--pem` argument.</span></span> <span data-ttu-id="2a26f-117">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2a26f-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="2a26f-118">Les fichiers .pem protégés par mot de passe demanderont un mot de passe avant d’exécuter une commande.</span><span class="sxs-lookup"><span data-stu-id="2a26f-118">Password protected pem files will prompt for password prior to running any command.</span></span>

<span data-ttu-id="2a26f-119">Pour spécifier un certificat, la paire de clés utilise les arguments `--cert` et `--key` afin de spécifier les chemins d’accès de fichier vers chaque fichier respectif.</span><span class="sxs-lookup"><span data-stu-id="2a26f-119">To specify a cert, key pair use the `--cert` and `--key` arguments to specify the file paths to each respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="2a26f-120">Il arrive que les certificats utilisés pour sécuriser les clusters de test ou de développement ne parviennent pas à valider le certificat.</span><span class="sxs-lookup"><span data-stu-id="2a26f-120">Sometimes certificates used to secure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="2a26f-121">Pour ignorer la vérification du certificat, spécifiez l’option `--no-verify`.</span><span class="sxs-lookup"><span data-stu-id="2a26f-121">To bypass certificate verification, specify the `--no-verify` option.</span></span> <span data-ttu-id="2a26f-122">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2a26f-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="2a26f-123">N’utilisez pas l’option `no-verify` lorsque vous vous connectez aux clusters Service Fabric de production.</span><span class="sxs-lookup"><span data-stu-id="2a26f-123">Do not use the `no-verify` option when connecting to production Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="2a26f-124">En outre, vous pouvez spécifier des chemins d’accès aux répertoires de certificats d’autorité de certification approuvées, ou à des certificats individuels.</span><span class="sxs-lookup"><span data-stu-id="2a26f-124">In addition, you can specify paths to directories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="2a26f-125">Pour spécifier ces chemins d’accès, utilisez l’argument `--ca`.</span><span class="sxs-lookup"><span data-stu-id="2a26f-125">To specify these paths, use the `--ca` argument.</span></span> <span data-ttu-id="2a26f-126">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2a26f-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="2a26f-127">Une fois connecté, vous pouvez normalement [exécuter d’autres commandes sfctl](service-fabric-cli.md) pour interagir avec le cluster.</span><span class="sxs-lookup"><span data-stu-id="2a26f-127">After you connect, you should be able to [run other sfctl commands](service-fabric-cli.md) to interact with the cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-to-a-cluster-using-powershell"></a><span data-ttu-id="2a26f-128">Se connecter à un cluster à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a26f-128">Connect to a cluster using PowerShell</span></span>
<span data-ttu-id="2a26f-129">Avant d’effectuer des opérations sur un cluster par le biais de PowerShell, établissez tout d’abord une connexion au cluster.</span><span class="sxs-lookup"><span data-stu-id="2a26f-129">Before you perform operations on a cluster through PowerShell, first establish a connection to the cluster.</span></span> <span data-ttu-id="2a26f-130">La connexion au cluster est utilisée pour toutes les commandes suivantes dans la session PowerShell donnée.</span><span class="sxs-lookup"><span data-stu-id="2a26f-130">The cluster connection is used for all subsequent commands in the given PowerShell session.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="2a26f-131">Se connecter à un cluster non sécurisé</span><span class="sxs-lookup"><span data-stu-id="2a26f-131">Connect to an unsecure cluster</span></span>

<span data-ttu-id="2a26f-132">Pour vous connecter à un cluster non sécurisé, fournissez l’adresse de point de terminaison de cluster à la commande **Connect-ServiceFabricCluster** :</span><span class="sxs-lookup"><span data-stu-id="2a26f-132">To connect to an unsecure cluster, provide the cluster endpoint address to the **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="2a26f-133">Se connecter à un cluster sécurisé à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a26f-133">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="2a26f-134">Pour vous connecter à un cluster sécurisé qui utilise Azure Active Directory pour autoriser un accès administrateur de cluster, fournissez l’empreinte de certificat du cluster et utilisez l’indicateur *AzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="2a26f-134">To connect to a secure cluster that uses Azure Active Directory to authorize cluster administrator access, provide the cluster certificate thumbprint and use the *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="2a26f-135">Se connecter à un cluster sécurisé à l’aide d’un certificat client</span><span class="sxs-lookup"><span data-stu-id="2a26f-135">Connect to a secure cluster using a client certificate</span></span>
<span data-ttu-id="2a26f-136">Exécutez la commande PowerShell suivante pour vous connecter à un cluster sécurisé qui utilise des certificats clients pour autoriser l’accès administrateur.</span><span class="sxs-lookup"><span data-stu-id="2a26f-136">Run the following PowerShell command to connect to a secure cluster that uses client certificates to authorize administrator access.</span></span> <span data-ttu-id="2a26f-137">Fournissez l’empreinte de certificat du cluster et l’empreinte numérique du certificat client qui dispose des autorisations pour la gestion de cluster.</span><span class="sxs-lookup"><span data-stu-id="2a26f-137">Provide the cluster certificate thumbprint and the thumbprint of the client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="2a26f-138">Les détails du certificat doivent correspondre à un certificat sur les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="2a26f-138">The certificate details must match a certificate on the cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="2a26f-139">*ServerCertThumbprint* est l’empreinte du certificat du serveur installé sur les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="2a26f-139">*ServerCertThumbprint* is the thumbprint of the server certificate installed on the cluster nodes.</span></span> <span data-ttu-id="2a26f-140">*FindValue* est l’empreinte du certificat du client administrateur.</span><span class="sxs-lookup"><span data-stu-id="2a26f-140">*FindValue* is the thumbprint of the admin client certificate.</span></span>
<span data-ttu-id="2a26f-141">Lorsque les paramètres sont renseignés, la commande ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="2a26f-141">When the parameters are filled in, the command looks like the following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-to-a-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="2a26f-142">Connexion à un cluster sécurisé à l’aide de Windows Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a26f-142">Connect to a secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="2a26f-143">Si votre cluster autonome est déployé à l’aide de la sécurité d’Active Directory, connectez-vous au cluster en ajoutant le commutateur « WindowsCredential ».</span><span class="sxs-lookup"><span data-stu-id="2a26f-143">If your standalone cluster is deployed using AD security, connect to the cluster by appending the switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-to-a-cluster-using-the-fabricclient-apis"></a><span data-ttu-id="2a26f-144">Se connecter à un cluster à l’aide des API FabricClient</span><span class="sxs-lookup"><span data-stu-id="2a26f-144">Connect to a cluster using the FabricClient APIs</span></span>
<span data-ttu-id="2a26f-145">Le Kit de développement logiciel (SDK) Service Fabric fournit la classe [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) pour la gestion de cluster.</span><span class="sxs-lookup"><span data-stu-id="2a26f-145">The Service Fabric SDK provides the [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="2a26f-146">Pour utiliser les API FabricClient, obtenez le package NuGet Microsoft.ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="2a26f-146">To use the FabricClient APIs, get the Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="2a26f-147">Se connecter à un cluster non sécurisé</span><span class="sxs-lookup"><span data-stu-id="2a26f-147">Connect to an unsecure cluster</span></span>

<span data-ttu-id="2a26f-148">Pour vous connecter à un cluster à distance non sécurisé, créez une instance de FabricClient et fournissez l’adresse du cluster :</span><span class="sxs-lookup"><span data-stu-id="2a26f-148">To connect to a remote unsecured cluster, create a FabricClient instance and provide the cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="2a26f-149">Pour un code qui s’exécute à partir d’un cluster, par exemple dans un Reliable Service, créez un élément FabricClient *sans* spécifier l’adresse du cluster.</span><span class="sxs-lookup"><span data-stu-id="2a26f-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying the cluster address.</span></span> <span data-ttu-id="2a26f-150">FabricClient se connecte à la passerelle de gestion locale sur le nœud sur lequel le code est en cours d’exécution, évitant ainsi un tronçon réseau supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="2a26f-150">FabricClient connects to the local management gateway on the node the code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="2a26f-151">Se connecter à un cluster sécurisé à l’aide d’un certificat client</span><span class="sxs-lookup"><span data-stu-id="2a26f-151">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="2a26f-152">Les nœuds du cluster doivent présenter des certificats valides, dont le nom commun ou le nom DNS dans le SAN s’affichent dans la [propriété RemoteCommonNames](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) définie sur [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="2a26f-152">The nodes in the cluster must have valid certificates whose common name or DNS name in SAN appears in the [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="2a26f-153">Ce processus permet une authentification mutuelle entre le client et les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="2a26f-153">Following this process enables mutual authentication between the client and the cluster nodes.</span></span>

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

### <a name="connect-to-a-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="2a26f-154">Se connecter à un cluster sécurisé de manière interactive à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a26f-154">Connect to a secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="2a26f-155">L’exemple suivant utilise Azure Active Directory pour l’identité du client et le certificat de serveur pour l’identité du serveur.</span><span class="sxs-lookup"><span data-stu-id="2a26f-155">The following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="2a26f-156">Une fenêtre de connexion interactive s’ouvre automatiquement une fois la connexion au cluster établie.</span><span class="sxs-lookup"><span data-stu-id="2a26f-156">A dialog window automatically pops up for interactive sign-in upon connecting to the cluster.</span></span>

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

### <a name="connect-to-a-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="2a26f-157">Se connecter à un cluster sécurisé de manière non interactive à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a26f-157">Connect to a secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="2a26f-158">L’exemple suivant est basé sur Microsoft.IdentityModel.Clients.ActiveDirectory, version 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="2a26f-158">The following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="2a26f-159">Pour plus d’informations sur l’acquisition d’un jeton AAD, consultez [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="2a26f-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

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

### <a name="connect-to-a-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="2a26f-160">Se connecter à un cluster sécurisé sans connaissance préalable des métadonnées à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a26f-160">Connect to a secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="2a26f-161">L’exemple suivant utilise une procédure d’acquisition de jeton non interactive, mais vous pouvez suivre la même approche pour créer une expérience d’acquisition de jeton interactive personnalisée.</span><span class="sxs-lookup"><span data-stu-id="2a26f-161">The following example uses non-interactive token acquisition, but the same approach can be used to build a custom interactive token acquisition experience.</span></span> <span data-ttu-id="2a26f-162">Les métadonnées Azure Active Directory nécessaires à l’acquisition d’un jeton sont lues à partir de la configuration du cluster.</span><span class="sxs-lookup"><span data-stu-id="2a26f-162">The Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

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

## <a name="connect-to-a-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="2a26f-163">Se connecter à un cluster sécurisé à l’aide de Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="2a26f-163">Connect to a secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="2a26f-164">Pour atteindre [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) pour un cluster donné, dirigez votre navigateur vers :</span><span class="sxs-lookup"><span data-stu-id="2a26f-164">To reach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="2a26f-165">L'URL complète est également disponible dans le volet des éléments essentiels du cluster dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2a26f-165">The full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="2a26f-166">Se connecter à un cluster sécurisé à l’aide d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a26f-166">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="2a26f-167">Pour vous connecter à un cluster sécurisé avec AAD, dirigez votre navigateur vers :</span><span class="sxs-lookup"><span data-stu-id="2a26f-167">To connect to a cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="2a26f-168">Vous êtes automatiquement invité à ouvrir une session avec AAD.</span><span class="sxs-lookup"><span data-stu-id="2a26f-168">You are automatically be prompted to log in with AAD.</span></span>

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="2a26f-169">Se connecter à un cluster sécurisé à l’aide d’un certificat client</span><span class="sxs-lookup"><span data-stu-id="2a26f-169">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="2a26f-170">Pour vous connecter à un cluster sécurisé avec des certificats, pointez votre navigateur sur :</span><span class="sxs-lookup"><span data-stu-id="2a26f-170">To connect to a cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="2a26f-171">Vous êtes automatiquement invité à sélectionner un certificat client.</span><span class="sxs-lookup"><span data-stu-id="2a26f-171">You are automatically be prompted to select a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-the-remote-computer"></a><span data-ttu-id="2a26f-172">Configurer un certificat client sur l’ordinateur distant</span><span class="sxs-lookup"><span data-stu-id="2a26f-172">Set up a client certificate on the remote computer</span></span>
<span data-ttu-id="2a26f-173">Au moins deux certificats devraient être utilisés pour sécuriser le cluster, un pour le certificat du cluster et du serveur, et un autre pour l’accès client.</span><span class="sxs-lookup"><span data-stu-id="2a26f-173">At least two certificates should be used for securing the cluster, one for the cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="2a26f-174">Nous vous recommandons d’utiliser également des certificats secondaires supplémentaires et des certificats d’accès client.</span><span class="sxs-lookup"><span data-stu-id="2a26f-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="2a26f-175">Pour sécuriser la communication entre un client et un nœud de cluster à l’aide de la sécurité par certificat, vous devez d’abord obtenir et installer le certificat client.</span><span class="sxs-lookup"><span data-stu-id="2a26f-175">To secure the communication between a client and a cluster node using certificate security, you first need to obtain and install the client certificate.</span></span> <span data-ttu-id="2a26f-176">Ce certificat peut être installé dans le magasin personnel de l’ordinateur local ou de l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="2a26f-176">The certificate can be installed into the Personal (My) store of the local computer or the current user.</span></span>  <span data-ttu-id="2a26f-177">Vous avez également besoin de l’empreinte numérique du certificat du serveur afin que le client puisse authentifier le cluster.</span><span class="sxs-lookup"><span data-stu-id="2a26f-177">You also need the thumbprint of the server certificate so that the client can authenticate the cluster.</span></span>

<span data-ttu-id="2a26f-178">Exécutez l’applet de commande PowerShell suivante pour configurer le certificat client sur l’ordinateur à partir duquel vous accédez au cluster.</span><span class="sxs-lookup"><span data-stu-id="2a26f-178">Run the following PowerShell cmdlet to set up the client certificate on the computer from which you access the cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="2a26f-179">S’il s’agit d’un certificat auto-signé, vous devez l’importer dans le magasin de « personnes autorisées » de votre ordinateur avant de pouvoir l’utiliser pour vous connecter à un cluster sécurisé.</span><span class="sxs-lookup"><span data-stu-id="2a26f-179">If it is a self-signed certificate, you need to import it to your machine's "trusted people" store before you can use this certificate to connect to a secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="2a26f-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2a26f-180">Next steps</span></span>

* [<span data-ttu-id="2a26f-181">Processus de mise à niveau du cluster Service Fabric et attentes à votre égard</span><span class="sxs-lookup"><span data-stu-id="2a26f-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="2a26f-182">Gestion de vos applications Service Fabric dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2a26f-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="2a26f-183">Présentation du modèle d’intégrité de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2a26f-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="2a26f-184">Sécurité des applications et RunAs</span><span class="sxs-lookup"><span data-stu-id="2a26f-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="2a26f-185">Bien démarrer avec l’interface de ligne de commande Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2a26f-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
