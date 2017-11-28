---
title: "Sécurité de conteneurs Azure Service Fabric | Microsoft Docs"
description: "En savoir plus sur les services de conteneurs sécurisés."
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
ms.openlocfilehash: 75faca1e827a0eca6b97adcb2e1c6ca72b3364d6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="container-security"></a><span data-ttu-id="b50cf-103">Sécurité du conteneur</span><span class="sxs-lookup"><span data-stu-id="b50cf-103">Container security</span></span>

<span data-ttu-id="b50cf-104">Service Fabric fournit un mécanisme pour les services à l’intérieur d’un conteneur pour accéder à un certificat installé sur les nœuds dans un cluster Windows ou Linux (version 5.7 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="b50cf-104">Service Fabric provides a mechanism for services inside a container to access a certificate that is installed on the nodes in a Windows or Linux cluster (version 5.7 or higher).</span></span> <span data-ttu-id="b50cf-105">En outre,Service Fabric prend également en charge les gMSA (comptes de service géré de groupe) pour les conteneurs Windows.</span><span class="sxs-lookup"><span data-stu-id="b50cf-105">In addition, Service Fabric also supports gMSA (group Managed Service Accounts) for Windows containers.</span></span> 

## <a name="certificate-management-for-containers"></a><span data-ttu-id="b50cf-106">Gestion des certificats pour les conteneurs</span><span class="sxs-lookup"><span data-stu-id="b50cf-106">Certificate management for containers</span></span>

<span data-ttu-id="b50cf-107">Vous pouvez sécuriser vos services de conteneur en spécifiant un certificat.</span><span class="sxs-lookup"><span data-stu-id="b50cf-107">You can secure your container services by specifying a certificate.</span></span> <span data-ttu-id="b50cf-108">Le certificat doit être installé sur les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="b50cf-108">The certificate must be installed on the nodes of the cluster.</span></span> <span data-ttu-id="b50cf-109">Les informations de certificat sont fournies dans le manifeste d’application avec la balise `ContainerHostPolicies` comme le montre l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="b50cf-109">The certificate information is provided in the application manifest under the `ContainerHostPolicies` tag as the following snippet shows:</span></span>

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

<span data-ttu-id="b50cf-110">Lors du démarrage de l’application, le runtime lit les certificats et génère un fichier PFX ainsi qu’un mot de passe pour chaque certificat.</span><span class="sxs-lookup"><span data-stu-id="b50cf-110">When starting the application, the runtime reads the certificates and generates a PFX file and password for each certificate.</span></span> <span data-ttu-id="b50cf-111">Ce fichier PFX et le mot de passe sont accessibles à l’intérieur du conteneur à l’aide des variables d’environnement suivantes :</span><span class="sxs-lookup"><span data-stu-id="b50cf-111">This PFX file and password are accessible inside the container using the following environment variables:</span></span> 

* <span data-ttu-id="b50cf-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span><span class="sxs-lookup"><span data-stu-id="b50cf-112">**Certificate_[CodePackageName]_[CertName]_PFX**</span></span>
* <span data-ttu-id="b50cf-113">**Certificate_[CodePackageName]_[CertName]_Password**</span><span class="sxs-lookup"><span data-stu-id="b50cf-113">**Certificate_[CodePackageName]_[CertName]_Password**</span></span>

<span data-ttu-id="b50cf-114">Le service de conteneur ou le processus est responsable de l’importation du fichier PFX vers le conteneur.</span><span class="sxs-lookup"><span data-stu-id="b50cf-114">The container service or process is responsible for importing the PFX file into the container.</span></span> <span data-ttu-id="b50cf-115">Pour importer le certificat, vous pouvez utiliser les scripts `setupentrypoint.sh` ou exécuter un code personnalisé dans le processus de conteneur.</span><span class="sxs-lookup"><span data-stu-id="b50cf-115">To import the certificate, you can use `setupentrypoint.sh` scripts or executed custom code within the container process.</span></span> <span data-ttu-id="b50cf-116">L’exemple de code en C# qui importe le fichier PFX est le suivant :</span><span class="sxs-lookup"><span data-stu-id="b50cf-116">Sample code in C# for importing the PFX file follows:</span></span>

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
<span data-ttu-id="b50cf-117">Ce certificat PFX peut être utilisé pour authentifier l’application ou le service ou la communication sécurisée avec d’autres services.</span><span class="sxs-lookup"><span data-stu-id="b50cf-117">This PFX certificate can be used for authenticate the application or service or secure commmunication with other services.</span></span>


## <a name="set-up-gmsa-for-windows-containers"></a><span data-ttu-id="b50cf-118">Configurer le gMSA pour les conteneurs Windows</span><span class="sxs-lookup"><span data-stu-id="b50cf-118">Set up gMSA for Windows containers</span></span>

<span data-ttu-id="b50cf-119">Pour configurer un gMSA (compte de service géré de groupe), un fichier de spécification des informations d’identification (`credspec`) est placé sur tous les nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="b50cf-119">To set up gMSA (group Managed Service Accounts), a credential specification file (`credspec`) is placed on all nodes in the cluster.</span></span> <span data-ttu-id="b50cf-120">Le fichier peut être copié sur tous les nœuds à l’aide d’une extension de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b50cf-120">The file can be copied on all nodes using a VM extension.</span></span>  <span data-ttu-id="b50cf-121">Le fichier `credspec` doit contenir les informations de compte gMSA.</span><span class="sxs-lookup"><span data-stu-id="b50cf-121">The `credspec` file must contain the gMSA account information.</span></span> <span data-ttu-id="b50cf-122">Pour plus d’informations sur le fichier `credspec`, consultez la page [Comptes de service](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span><span class="sxs-lookup"><span data-stu-id="b50cf-122">For more information on the `credspec` file, see [Service Accounts](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts).</span></span> <span data-ttu-id="b50cf-123">La spécification d’informations d’identification et la balise `Hostname` sont spécifiées dans le manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="b50cf-123">The credential specification and the `Hostname` tag are specified in the application manifest.</span></span> <span data-ttu-id="b50cf-124">La balise `Hostname` doit correspondre au nom de compte gMSA dans lequel le conteneur s’exécute.</span><span class="sxs-lookup"><span data-stu-id="b50cf-124">The `Hostname` tag must match the gMSA account name that the container runs under.</span></span>  <span data-ttu-id="b50cf-125">La balise `Hostname` permet au conteneur de s’authentifier auprès d’autres services dans le domaine à l’aide de l’authentification Kerberos.</span><span class="sxs-lookup"><span data-stu-id="b50cf-125">The `Hostname` tag allows the container to authenticate itself to other services in the domain using Kerberos authentication.</span></span>  <span data-ttu-id="b50cf-126">Un exemple de spécification des balises `Hostname` et `credspec` du manifeste d’application est indiqué dans l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="b50cf-126">A sample for specifying the `Hostname` and the `credspec` in the application manifest is shown in the following snippet:</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="b50cf-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b50cf-127">Next steps</span></span>

* [<span data-ttu-id="b50cf-128">Déployer un conteneur Windows sur Service Fabric sous Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b50cf-128">Deploy a Windows container to Service Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="b50cf-129">Déployer un conteneur Docker sur Service Fabric sous Linux</span><span class="sxs-lookup"><span data-stu-id="b50cf-129">Deploy a Docker container to Service Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
