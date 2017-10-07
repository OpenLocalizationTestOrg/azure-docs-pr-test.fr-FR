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
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="a9aa3-103">Sécuriser un cluster autonome sur Windows à l’aide de certificats X.509</span><span class="sxs-lookup"><span data-stu-id="a9aa3-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="a9aa3-104">Cet article décrit comment les communications de hello toosecure entre hello différents nœuds du cluster Windows autonome, tooauthenticate les clients se connectant toothis cluster, à l’aide de certificats X.509 ainsi que comment.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-104">This article describes how toosecure hello communication between hello various nodes of your standalone Windows cluster, as well as how tooauthenticate clients connecting toothis cluster, using X.509 certificates.</span></span> <span data-ttu-id="a9aa3-105">Cela garantit que seuls les utilisateurs autorisés peuvent accéder à cluster de hello, hello des applications déployées et effectuer des tâches de gestion.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-105">This ensures that only authorized users can access hello cluster, hello deployed applications and perform management tasks.</span></span>  <span data-ttu-id="a9aa3-106">Sécurité de certificat doit être activée sur le cluster de hello lorsque hello cluster est créé.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-106">Certificate security should be enabled on hello cluster when hello cluster is created.</span></span>  

<span data-ttu-id="a9aa3-107">Pour en savoir plus sur la sécurité de cluster, telle que la sécurité nœud à nœud, la sécurité client à nœud et le contrôle d’accès en fonction du rôle, consultez [Scénarios de sécurité du cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="a9aa3-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="a9aa3-108">Quels sont les certificats requis ?</span><span class="sxs-lookup"><span data-stu-id="a9aa3-108">Which certificates will you need?</span></span>
<span data-ttu-id="a9aa3-109">toostart, [télécharger le package de cluster autonome hello](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone de nœuds hello dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-109">toostart with, [download hello standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone of hello nodes in your cluster.</span></span> <span data-ttu-id="a9aa3-110">Bonjour téléchargé le package, vous trouverez une **ClusterConfig.X509.MultiMachine.json** fichier.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-110">In hello downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="a9aa3-111">Ouvrez le fichier de hello et passez en revue la section hello pour **sécurité** sous hello **propriétés** section :</span><span class="sxs-lookup"><span data-stu-id="a9aa3-111">Open hello file and review hello section for **security** under hello **properties** section:</span></span>

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

<span data-ttu-id="a9aa3-112">Cette section décrit les certificats hello dont vous avez besoin pour la sécurisation de votre cluster de Windows autonome.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-112">This section describes hello certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="a9aa3-113">Si vous spécifiez un certificat de cluster, valeur hello **ClusterCredentialType** too_**X509**_. Si vous spécifiez un certificat de serveur pour les connexions externes, définissez hello **ServerCredentialType** trop_**X509**_. Mais pas obligatoire, nous vous recommandons toohave ces deux certificats pour un cluster correctement sécurisé. Si vous définissez ces valeurs trop*X509* vous devez également spécifier hello certificats correspondants ou Service Fabric lève une exception. Dans certains scénarios, vous pouvez souhaiter que toospecify hello _ClientCertificateThumbprints_ ou _ReverseProxyCertificate_. Dans ces scénarios, vous ne devez pas définir _ClusterCredentialType_ ou _ServerCredentialType_ too_X509_.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-113">If you are specifying a cluster certificate, set hello value of **ClusterCredentialType** too_**X509**_. If you are specifying server certificate for outside connections, set hello **ServerCredentialType** too_**X509**_. Although not mandatory, we recommend toohave both these certificates for a properly secured cluster. If you set these values too*X509* then you must also specify hello corresponding certificates or Service Fabric will throw an exception. In some scenarios, you may only want toospecify hello _ClientCertificateThumbprints_ or _ReverseProxyCertificate_. In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ too_X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="a9aa3-114">A [l’empreinte numérique](https://en.wikipedia.org/wiki/Public_key_fingerprint) est l’identité primaire de hello d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-114">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is hello primary identity of a certificate.</span></span> <span data-ttu-id="a9aa3-115">Lecture [comment empreinte tooretrieve d’un certificat](https://msdn.microsoft.com/library/ms734695.aspx) toofind out empreinte hello de certificats hello que vous créez.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-115">Read [How tooretrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) toofind out hello thumbprint of hello certificates that you create.</span></span>
> 
> 

<span data-ttu-id="a9aa3-116">Hello tableau ci-dessous répertorie les certificats hello dont vous aurez besoin de votre configuration de cluster :</span><span class="sxs-lookup"><span data-stu-id="a9aa3-116">hello following table lists hello certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="a9aa3-117">**Paramètre CertificateInformation**</span><span class="sxs-lookup"><span data-stu-id="a9aa3-117">**CertificateInformation Setting**</span></span> | <span data-ttu-id="a9aa3-118">**Description**</span><span class="sxs-lookup"><span data-stu-id="a9aa3-118">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="a9aa3-119">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="a9aa3-119">ClusterCertificate</span></span> |<span data-ttu-id="a9aa3-120">Recommandé pour l’environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-120">Recommended for test environment.</span></span> <span data-ttu-id="a9aa3-121">Ce certificat est la communication de hello toosecure requis entre les nœuds de hello sur un cluster.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-121">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="a9aa3-122">Vous pouvez utiliser deux certificats différents : un certificat principal et un certificat secondaire pour la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-122">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="a9aa3-123">Définir l’empreinte numérique hello du certificat principal de hello Bonjour **l’empreinte numérique** section et celle de hello secondaire Bonjour **ThumbprintSecondary** variables.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-123">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="a9aa3-124">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="a9aa3-124">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="a9aa3-125">Recommandé pour l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-125">Recommended for production environment.</span></span> <span data-ttu-id="a9aa3-126">Ce certificat est la communication de hello toosecure requis entre les nœuds de hello sur un cluster.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-126">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="a9aa3-127">Vous pouvez utiliser un ou deux noms communs de certificat de cluster.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-127">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="a9aa3-128">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="a9aa3-128">ServerCertificate</span></span> |<span data-ttu-id="a9aa3-129">Recommandé pour l’environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-129">Recommended for test environment.</span></span> <span data-ttu-id="a9aa3-130">Ce certificat est présenté toohello client quand il tente de tooconnect toothis cluster.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-130">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="a9aa3-131">Pour plus de commodité, vous pouvez choisir toouse hello même certificat pour *ClusterCertificate* et *ServerCertificate*.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-131">For convenience, you can choose toouse hello same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="a9aa3-132">Vous pouvez utiliser deux certificats de serveur différents : un certificat principal et un certificat secondaire pour la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-132">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="a9aa3-133">Définir l’empreinte numérique hello du certificat principal de hello Bonjour **l’empreinte numérique** section et celle de hello secondaire Bonjour **ThumbprintSecondary** variables.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-133">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="a9aa3-134">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="a9aa3-134">ServerCertificateCommonNames</span></span> |<span data-ttu-id="a9aa3-135">Recommandé pour l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-135">Recommended for production environment.</span></span> <span data-ttu-id="a9aa3-136">Ce certificat est présenté toohello client quand il tente de tooconnect toothis cluster.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-136">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="a9aa3-137">Pour plus de commodité, vous pouvez choisir toouse hello même certificat pour *ClusterCertificateCommonNames* et *ServerCertificateCommonNames*.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-137">For convenience, you can choose toouse hello same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="a9aa3-138">Vous pouvez utiliser un ou deux noms communs de certificat de serveur.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-138">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="a9aa3-139">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="a9aa3-139">ClientCertificateThumbprints</span></span> |<span data-ttu-id="a9aa3-140">Il s’agit d’un jeu de certificats que vous souhaitez tooinstall sur les clients de hello authentifié.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-140">This is a set of certificates that you want tooinstall on hello authenticated clients.</span></span> <span data-ttu-id="a9aa3-141">Vous pouvez avoir un nombre de certificats client différents installé sur les ordinateurs hello que vous souhaitez le cluster de toohello tooallow accès.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-141">You can have a number of different client certificates installed on hello machines that you want tooallow access toohello cluster.</span></span> <span data-ttu-id="a9aa3-142">Définir l’empreinte numérique hello de chaque certificat Bonjour **CertificateThumbprint** variable.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-142">Set hello thumbprint of each certificate in hello **CertificateThumbprint** variable.</span></span> <span data-ttu-id="a9aa3-143">Si vous définissez hello **IsAdmin** trop*true*, puis client hello avec ce certificat installé dessus faire administrateur des activités de gestion sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-143">If you set hello **IsAdmin** too*true*, then hello client with this certificate installed on it can do administrator management activities on hello cluster.</span></span> <span data-ttu-id="a9aa3-144">Si hello **IsAdmin** est *false*, client hello avec ce certificat ne pouvez effectuer les actions hello autorisées pour les droits d’accès utilisateur, généralement en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-144">If hello **IsAdmin** is *false*, hello client with this certificate can only perform hello actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="a9aa3-145">Pour plus d’informations sur les rôles, consultez [Contrôle d’accès en fonction du rôle (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="a9aa3-145">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="a9aa3-146">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="a9aa3-146">ClientCertificateCommonNames</span></span> |<span data-ttu-id="a9aa3-147">Définir hello commun le nom du certificat de client premier hello pour hello **CertificateCommonName**.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-147">Set hello common name of hello first client certificate for hello **CertificateCommonName**.</span></span> <span data-ttu-id="a9aa3-148">Hello **CertificateIssuerThumbprint** est l’empreinte numérique hello pour émetteur hello de ce certificat.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-148">hello **CertificateIssuerThumbprint** is hello thumbprint for hello issuer of this certificate.</span></span> <span data-ttu-id="a9aa3-149">Lecture [utilisation des certificats](https://msdn.microsoft.com/library/ms731899.aspx) tooknow plus d’informations sur les noms communs et de l’émetteur de hello.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-149">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) tooknow more about common names and hello issuer.</span></span> |
| <span data-ttu-id="a9aa3-150">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="a9aa3-150">ReverseProxyCertificate</span></span> |<span data-ttu-id="a9aa3-151">Recommandé pour l’environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-151">Recommended for test environment.</span></span> <span data-ttu-id="a9aa3-152">Il s’agit d’un certificat facultatif qui peut être spécifié si vous souhaitez toosecure votre [Proxy inverse](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="a9aa3-152">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="a9aa3-153">Assurez-vous que reverseProxyEndpointPort est défini dans nodeTypes, si vous utilisez ce certificat.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-153">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="a9aa3-154">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="a9aa3-154">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="a9aa3-155">Recommandé pour l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-155">Recommended for production environment.</span></span> <span data-ttu-id="a9aa3-156">Il s’agit d’un certificat facultatif qui peut être spécifié si vous souhaitez toosecure votre [Proxy inverse](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="a9aa3-156">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="a9aa3-157">Assurez-vous que reverseProxyEndpointPort est défini dans nodeTypes, si vous utilisez ce certificat.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-157">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="a9aa3-158">Voici exemple de configuration de cluster où les certificats de Cluster, serveur et Client hello ont été fournis.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-158">Here is example cluster configuration where hello Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="a9aa3-159">Notez que pour le cluster / serveur / reverseProxy certificats, l’empreinte numérique et le nom commun ne sont pas autorisés toobe configurés conjointement pour hello même type de certificat.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-159">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed toobe configured together for hello same cert type.</span></span>

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

## <a name="certificate-roll-over"></a><span data-ttu-id="a9aa3-160">Renouvellement d’un certificat</span><span class="sxs-lookup"><span data-stu-id="a9aa3-160">Certificate roll over</span></span>
<span data-ttu-id="a9aa3-161">Lorsque vous utilisez le nom commun du certificat au lieu de l’empreinte, le renouvellement de certificat ne requiert aucune mise à niveau de configuration de cluster.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-161">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="a9aa3-162">Si le certificat intervenant implique l’émetteur substituer, Veuillez conserver au moins 2 heures après l’installation du nouveau certificat de l’émetteur hello hello ancien émetteur de cert dans le magasin de certificats hello.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-162">If certificate roll over involves issuer roll over, please keep hello old issuer cert in hello cert store at least 2 hours after installing hello new issuer cert.</span></span>

## <a name="acquire-hello-x509-certificates"></a><span data-ttu-id="a9aa3-163">Obtenir des certificats X.509 hello</span><span class="sxs-lookup"><span data-stu-id="a9aa3-163">Acquire hello X.509 certificates</span></span>
<span data-ttu-id="a9aa3-164">communication toosecure au sein du cluster de hello, vous devez abord tooobtain des certificats X.509 pour vos nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-164">toosecure communication within hello cluster, you will first need tooobtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="a9aa3-165">En outre, toolimit connexion toothis cluster tooauthorized machines/utilisateurs, vous devez tooobtain et installer des certificats pour les ordinateurs clients hello.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-165">Additionally, toolimit connection toothis cluster tooauthorized machines/users, you will need tooobtain and install certificates for hello client machines.</span></span>

<span data-ttu-id="a9aa3-166">Pour les clusters qui exécutent des charges de travail de production, vous devez utiliser un [autorité de certification (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signés de cluster de hello de toosecure de certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-166">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate toosecure hello cluster.</span></span> <span data-ttu-id="a9aa3-167">Pour plus d’informations sur l’obtention de ces certificats, consultez trop[Comment : obtenir un certificat](http://msdn.microsoft.com/library/aa702761.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9aa3-167">For details on obtaining these certificates, go too[How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="a9aa3-168">Pour les clusters que vous utilisez à des fins de test, vous pouvez choisir toouse un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-168">For clusters that you use for test purposes, you can choose toouse a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="a9aa3-169">Facultatif : Créer un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="a9aa3-169">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="a9aa3-170">Une façon toocreate un certificat auto-signé qui peut être correctement sécurisé est toouse hello *CertSetup.ps1* script dans hello Service Fabric SDK dossier hello répertoire *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-170">One way toocreate a self-signed cert that can be secured correctly is toouse hello *CertSetup.ps1* script in hello Service Fabric SDK folder in hello directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="a9aa3-171">Modifier ce nom par défaut de fichier toochange hello du certificat de hello (recherchez hello valeur *CN = ServiceFabricDevClusterCert*).</span><span class="sxs-lookup"><span data-stu-id="a9aa3-171">Edit this file toochange hello default name of hello certificate (look for hello value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="a9aa3-172">Exécutez ce script en tant que `.\CertSetup.ps1 -Install`.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-172">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="a9aa3-173">Maintenant exporter le fichier PFX tooa du certificat hello avec un mot de passe protégé.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-173">Now export hello certificate tooa PFX file with a protected password.</span></span> <span data-ttu-id="a9aa3-174">Tout d’abord obtenir hello empreinte numérique du certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-174">First get hello thumbprint of hello certificate.</span></span> <span data-ttu-id="a9aa3-175">À partir de hello *Démarrer* menu, exécutez hello *gérer les certificats d’ordinateur*.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-175">From hello *Start* menu, run hello *Manage computer certificates*.</span></span> <span data-ttu-id="a9aa3-176">Accédez toohello **local\personnel** dossier et rechercher hello certificat que vous avez juste créé.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-176">Navigate toohello **Local Computer\Personal** folder and find hello certificate you just created.</span></span> <span data-ttu-id="a9aa3-177">Double-cliquez sur hello certificat tooopen il, sélectionnez hello *détails* onglet et faites défiler toohello *l’empreinte numérique* champ.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-177">Double-click hello certificate tooopen it, select hello *Details* tab and scroll down toohello *Thumbprint* field.</span></span> <span data-ttu-id="a9aa3-178">Copiez la valeur d’empreinte numérique hello dans la commande PowerShell de hello ci-dessous, après la suppression des espaces de hello.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-178">Copy hello thumbprint value into hello PowerShell command below, after removing hello spaces.</span></span>  <span data-ttu-id="a9aa3-179">Hello de modification `String` valeur tooa approprié de mot de passe sécurisé tooprotect et exécution hello suivant dans PowerShell :</span><span class="sxs-lookup"><span data-stu-id="a9aa3-179">Change hello `String` value tooa suitable secure password tooprotect it and run hello following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="a9aa3-180">Détails de hello toosee d’un certificat installé sur hello machine que vous pouvez exécuter hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="a9aa3-180">toosee hello details of a certificate installed on hello machine you can run hello following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="a9aa3-181">Ou bien, si vous avez un abonnement Azure, suivez la section de hello [ajouter des certificats tooKey coffre](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span><span class="sxs-lookup"><span data-stu-id="a9aa3-181">Alternatively, if you have an Azure subscription, follow hello section [Add certificates tooKey Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-hello-certificates"></a><span data-ttu-id="a9aa3-182">Installer des certificats de hello</span><span class="sxs-lookup"><span data-stu-id="a9aa3-182">Install hello certificates</span></span>
<span data-ttu-id="a9aa3-183">Une fois que vous avez ou les certificats, vous pouvez les installer sur les nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-183">Once you have certificate(s), you can install them on hello cluster nodes.</span></span> <span data-ttu-id="a9aa3-184">Vos nœuds doivent toohave hello plus récente de Windows PowerShell 3.x sur lesquels est installé.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-184">Your nodes need toohave hello latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="a9aa3-185">Vous devez toorepeat ces étapes sur chaque nœud, pour les certificats de Cluster et le serveur et tous les certificats secondaires.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-185">You will need toorepeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="a9aa3-186">Nœud de toohello pour les fichiers .pfx copie hello.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-186">Copy hello .pfx file(s) toohello node.</span></span>
2. <span data-ttu-id="a9aa3-187">Ouvrez une fenêtre PowerShell en tant qu’administrateur et entrez hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-187">Open a PowerShell window as an administrator and enter hello following commands.</span></span> <span data-ttu-id="a9aa3-188">Remplacez hello *$pswd* avec mot de passe hello que vous avez utilisé toocreate ce certificat.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-188">Replace hello *$pswd* with hello password that you used toocreate this certificate.</span></span> <span data-ttu-id="a9aa3-189">Remplacez hello *$PfxFilePath* avec le chemin complet de hello du nœud de hello .pfx toothis copié.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-189">Replace hello *$PfxFilePath* with hello full path of hello .pfx copied toothis node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="a9aa3-190">Maintenant définir le contrôle d’accès hello sur ce certificat afin que le processus de Service Fabric hello, qui s’exécute sous hello compte Service réseau, peut l’utiliser en exécutant le script suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-190">Now set hello access control on this certificate so that hello Service Fabric process, which runs under hello Network Service account, can use it by running hello following script.</span></span> <span data-ttu-id="a9aa3-191">Fournissez l’empreinte numérique hello hello certificat d’et « SERVICE réseau » pour le compte de service hello.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-191">Provide hello thumbprint of hello certificate and "NETWORK SERVICE" for hello service account.</span></span> <span data-ttu-id="a9aa3-192">Vous pouvez vérifier que hello ACL sur le certificat de hello sont corrects en ouvrant le certificat hello dans *Démarrer* > *gérer les certificats d’ordinateur* et en examinant *toutes les tâches*  >  *Gérer les clés privées*.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-192">You can check that hello ACLs on hello certificate are correct by opening hello certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
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
4. <span data-ttu-id="a9aa3-193">Répétez les étapes hello pour chaque certificat de serveur.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-193">Repeat hello steps above for each server certificate.</span></span> <span data-ttu-id="a9aa3-194">Vous pouvez également utiliser ces étapes tooinstall hello certificats clients sur des ordinateurs de hello que vous souhaitez le cluster de toohello tooallow accès.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-194">You can also use these steps tooinstall hello client certificates on hello machines that you want tooallow access toohello cluster.</span></span>

## <a name="create-hello-secure-cluster"></a><span data-ttu-id="a9aa3-195">Créer le cluster sécurisée de hello</span><span class="sxs-lookup"><span data-stu-id="a9aa3-195">Create hello secure cluster</span></span>
<span data-ttu-id="a9aa3-196">Après avoir configuré hello **sécurité** section Hello **ClusterConfig.X509.MultiMachine.json** fichier, vous pouvez passer trop[créez votre cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) tooconfigure de section Hello nœuds et créer le cluster de hello autonome.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-196">After configuring hello **security** section of hello **ClusterConfig.X509.MultiMachine.json** file, you can proceed too[Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section tooconfigure hello nodes and create hello standalone cluster.</span></span> <span data-ttu-id="a9aa3-197">N’oubliez pas de toouse hello **ClusterConfig.X509.MultiMachine.json** fichier lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-197">Remember toouse hello **ClusterConfig.X509.MultiMachine.json** file while creating hello cluster.</span></span> <span data-ttu-id="a9aa3-198">Par exemple, votre commande peut ressembler à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="a9aa3-198">For example, your command might look like hello following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="a9aa3-199">Une fois que vous avez hello sécurisé autonome Windows cluster en cours d’exécution et ont le programme d’installation Bonjour des clients authentifiés tooconnect tooit, suivez hello section [cluster sécurisée du tooa se connecter à l’aide de PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-199">Once you have hello secure standalone Windows cluster successfully running, and have setup hello authenticated clients tooconnect tooit, follow hello section [Connect tooa secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span></span> <span data-ttu-id="a9aa3-200">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a9aa3-200">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="a9aa3-201">Vous pouvez ensuite exécuter autres toowork de commandes PowerShell avec ce cluster.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-201">You can then run other PowerShell commands toowork with this cluster.</span></span> <span data-ttu-id="a9aa3-202">Par exemple, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow une liste de nœuds sur ce cluster sécurisé.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-202">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="a9aa3-203">cluster de hello tooremove, connecter nœud toohello sur cluster hello où vous avez téléchargé le package de Service Fabric hello, ouvrez une ligne de commande et accédez toohello dossier du package.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-203">tooremove hello cluster, connect toohello node on hello cluster where you downloaded hello Service Fabric package, open a command line and navigate toohello package folder.</span></span> <span data-ttu-id="a9aa3-204">Maintenant, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a9aa3-204">Now run hello following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="a9aa3-205">Configuration du certificat incorrect peut empêcher le prochaines évolutions et durant le déploiement de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-205">Incorrect certificate configuration may prevent hello cluster from coming up during deployment.</span></span> <span data-ttu-id="a9aa3-206">tooself-diagnostiquer les problèmes de sécurité, recherchez dans le groupe Observateur d’événements *journaux des Applications et Services* > *Microsoft Service Fabric*.</span><span class="sxs-lookup"><span data-stu-id="a9aa3-206">tooself-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

