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
# <a name="container-security"></a>Sécurité du conteneur

L’infrastructure de service fournit un mécanisme pour les services à l’intérieur d’un conteneur de tooaccess un certificat est installé sur les nœuds hello dans un cluster Windows ou Linux (version 5.7 ou version ultérieure). En outre,Service Fabric prend également en charge les gMSA (comptes de service géré de groupe) pour les conteneurs Windows. 

## <a name="certificate-management-for-containers"></a>Gestion des certificats pour les conteneurs

Vous pouvez sécuriser vos services de conteneur en spécifiant un certificat. certificat de Hello doit être installé sur les nœuds de hello du cluster de hello. informations de certificat Hello sont fournies dans le manifeste de l’application hello sous hello `ContainerHostPolicies` balise sous la forme hello ci-dessous illustre d’extrait de code :

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

Lorsque vous démarrez l’application hello, hello runtime lit les certificats hello et génère un fichier PFX et un mot de passe pour chaque certificat. Ce fichier PFX et le mot de passe sont accessibles à l’intérieur du conteneur de hello à l’aide de hello suivant des variables d’environnement : 

* **Certificate_[CodePackageName]_[CertName]_PFX**
* **Certificate_[CodePackageName]_[CertName]_Password**

service de conteneur Hello ou un processus est chargé de l’importation du fichier PFX de hello dans le conteneur de hello. certificat de hello tooimport, vous pouvez utiliser `setupentrypoint.sh` scripts ou exécuté du code personnalisé dans le processus de conteneur hello. Exemple de code en c# pour l’importation hello PFX fichier suivante :

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
Ce certificat PFX peut être utilisé pour authentifier hello application ou service ou un commmunication sécurisée avec d’autres services.


## <a name="set-up-gmsa-for-windows-containers"></a>Configurer le gMSA pour les conteneurs Windows

tooset de service administré de groupe (groupe comptes de Service administré), un fichier de spécification des informations d’identification (`credspec`) est placé sur tous les nœuds de cluster de hello. fichier de Hello peut être copié sur tous les nœuds à l’aide d’une extension de machine virtuelle.  Hello `credspec` fichier doit contenir des informations de compte de service administré de groupe hello. Pour plus d’informations sur hello `credspec` de fichiers, consultez [les comptes de Service](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts). Spécification des informations d’identification Hello et hello `Hostname` balise sont spécifiés dans le manifeste de l’application hello. Hello `Hostname` balise doit correspondre au nom de compte de service administré de groupe hello hello s’exécute le conteneur sous.  Hello `Hostname` balise permet tooauthenticate de conteneur hello lui-même tooother des services de domaine hello à l’aide de l’authentification Kerberos.  Un exemple de spécification hello `Hostname` et hello `credspec` Bonjour manifeste d’application est indiqué dans hello suivant extrait de code :

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a>Étapes suivantes

* [Déployer un tooService de conteneur Windows Fabric sur Windows Server 2016](service-fabric-get-started-containers.md)
* [Déployer un tooService de conteneur Docker Fabric sur Linux](service-fabric-get-started-containers-linux.md)
