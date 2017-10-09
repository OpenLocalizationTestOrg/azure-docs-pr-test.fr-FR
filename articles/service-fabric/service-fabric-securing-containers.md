---
title: "aaaAzure sécurité conteneur de Service Fabric | Documents Microsoft"
description: En savoir plus toosecure maintenant les services de conteneur.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a><span data-ttu-id="5c162-103">Sécurité du conteneur</span><span class="sxs-lookup"><span data-stu-id="5c162-103">Container security</span></span>

<span data-ttu-id="5c162-104">L’infrastructure de service fournit un mécanisme pour les services à l’intérieur d’un conteneur de tooaccess un certificat est installé sur les nœuds hello dans un cluster Windows ou Linux (version 5.7 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="5c162-104">Service Fabric provides a mechanism for services inside a container tooaccess a certificate that is installed on hello nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="5c162-105">En outre,Service Fabric prend également en charge les gMSA (comptes de service géré de groupe) pour les conteneurs Windows.</span><span class="sxs-lookup"><span data-stu-id="5c162-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="5c162-106">Gestion des certificats pour les conteneurs</span><span class="sxs-lookup"><span data-stu-id="5c162-106">Certificate management for containers</span></span>

<span data-ttu-id="5c162-107">Vous pouvez sécuriser vos services de conteneur en spécifiant un certificat.</span><span class="sxs-lookup"><span data-stu-id="5c162-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="5c162-108">certificat de Hello doit être installé sur les nœuds de hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="5c162-108">hello certificate must be installed on hello nodes of hello cluster.</span></span> <span data-ttu-id="5c162-109">informations de certificat Hello sont fournies dans le manifeste de l’application hello sous hello `ContainerHostPolicies` balise sous la forme hello ci-dessous illustre d’extrait de code :</span><span class="sxs-lookup"><span data-stu-id="5c162-109">hello certificate information is provided in hello application manifest under hello `ContainerHostPolicies` tag as hello following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="5c162-110">Lorsque vous démarrez l’application hello, hello runtime lit les certificats hello et génère un fichier PFX et un mot de passe pour chaque certificat.</span><span class="sxs-lookup"><span data-stu-id="5c162-110">When starting hello application, hello runtime reads hello certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="5c162-111">Ce fichier PFX et le mot de passe sont accessibles à l’intérieur du conteneur de hello à l’aide de hello suivant des variables d’environnement :</span><span class="sxs-lookup"><span data-stu-id="5c162-111">This PFX file and password are accessible inside hello container using hello following environment variables:</span></span> 

* <span data-ttu-id="5c162-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span><span class="sxs-lookup"><span data-stu-id="5c162-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="5c162-113">**Certificate_[CodePackageName]_[CertName]_Password**</span><span class="sxs-lookup"><span data-stu-id="5c162-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="5c162-114">service de conteneur Hello ou un processus est chargé de l’importation du fichier PFX de hello dans le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="5c162-114">hello container service or process is responsible for importing hello PFX file into hello container.</span></span> <span data-ttu-id="5c162-115">certificat de hello tooimport, vous pouvez utiliser `setupentrypoint.sh` scripts ou exécuté du code personnalisé dans le processus de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="5c162-115">tooimport hello certificate, you can use `setupentrypoint.sh` scripts or executed custom code within hello container process.</span></span> <span data-ttu-id="5c162-116">Exemple de code en c# pour l’importation hello PFX fichier suivante :</span><span class="sxs-lookup"><span data-stu-id="5c162-116">Sample code in C# for importing hello PFX file follows:</span></span>

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
<span data-ttu-id="5c162-117">Ce certificat PFX peut être utilisé pour authentifier hello application ou service ou un commmunication sécurisée avec d’autres services.</span><span class="sxs-lookup"><span data-stu-id="5c162-117">This PFX certificate can be used for authenticate hello application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="5c162-118">Configurer le gMSA pour les conteneurs Windows</span><span class="sxs-lookup"><span data-stu-id="5c162-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="5c162-119">tooset de service administré de groupe (groupe comptes de Service administré), un fichier de spécification des informations d’identification (`credspec`) est placé sur tous les nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="5c162-119">tooset up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in hello cluster.</span></span> <span data-ttu-id="5c162-120">fichier de Hello peut être copié sur tous les nœuds à l’aide d’une extension de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5c162-120">hello file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="5c162-121">Hello `credspec` fichier doit contenir des informations de compte de service administré de groupe hello.</span><span class="sxs-lookup"><span data-stu-id="5c162-121">hello `credspec` file must contain hello gMSA account information.</span></span> <span data-ttu-id="5c162-122">Pour plus d’informations sur hello `credspec` de fichiers, consultez [les comptes de Service](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span><span class="sxs-lookup"><span data-stu-id="5c162-122">For more information on hello `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="5c162-123">Spécification des informations d’identification Hello et hello `Hostname` balise sont spécifiés dans le manifeste de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5c162-123">hello credential specification and hello `Hostname` tag are specified in hello application manifest.</span></span> <span data-ttu-id="5c162-124">Hello `Hostname` balise doit correspondre au nom de compte de service administré de groupe hello hello s’exécute le conteneur sous.</span><span class="sxs-lookup"><span data-stu-id="5c162-124">hello `Hostname` tag must match hello gMSA account name that hello container runs under.</span></span>  <span data-ttu-id="5c162-125">Hello `Hostname` balise permet tooauthenticate de conteneur hello lui-même tooother des services de domaine hello à l’aide de l’authentification Kerberos.</span><span class="sxs-lookup"><span data-stu-id="5c162-125">hello `Hostname` tag allows hello container tooauthenticate itself tooother services in hello domain using Kerberos authentication.</span></span>  <span data-ttu-id="5c162-126">Un exemple de spécification hello `Hostname` et hello `credspec` Bonjour manifeste d’application est indiqué dans hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="5c162-126">A sample for specifying hello `Hostname` and hello `credspec` in hello application manifest is shown in hello following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="5c162-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5c162-127">Next steps</span></span>

* [<span data-ttu-id="5c162-128">Déployer un tooService de conteneur Windows Fabric sur Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="5c162-128">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="5c162-129">Déployer un tooService de conteneur Docker Fabric sur Linux</span><span class="sxs-lookup"><span data-stu-id="5c162-129">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
