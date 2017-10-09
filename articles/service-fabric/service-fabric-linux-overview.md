---
title: aaaAzure Service Fabric sur Linux | Documents Microsoft
description: "Clusters service Fabric prend en charge Linux et Java, ce qui signifie que vous serez en mesure de toodeploy et héberger des applications de Service Fabric écrites en Java et c# sur Linux."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a>Service Fabric sur Linux
Aperçu de Hello du Service Fabric sur Linux vous permet de toobuild, déployer et gérer des applications hautement disponibles et hautement évolutives sur Linux comme vous le feriez sur Windows. les infrastructures de Service Fabric Hello (Services fiables et Reliable Actors) sont disponibles dans Java sur Linux en outre tooC # (.NET Core).  Vous pouvez également créer des [services exécutables invités](service-fabric-deploy-existing-app.md) via tous les langages ou frameworks. En outre, l’aperçu de hello prend également en charge des conteneurs Docker orchestrant ces opérations. Conteneurs docker peuvent exécuter des exécutables de l’invité ou les services de Service Fabric natives, qui utilisent des infrastructures de Service Fabric hello.

Service Fabric sur Linux est conceptuellement équivalent tooService Fabric sur Windows (à l’exception des caractéristiques du système d’exploitation et la prise en charge du langage de programmation). Par conséquent, la plupart de nos [documentation existante](http://aka.ms/servicefabricdocs) s’applique en vous permettant de vous familiariserez avec la technologie de hello.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a>Systèmes d’exploitation et langages de programmation pris en charge
Création de hello Hello limitée version préliminaire prend en charge du développement d’une case des clusters de plus toomulti-ordinateur des clusters dans Azure Ubuntu Server 16.04 en cours d’exécution. prend en charge de la version préliminaire Hello hello Reliable Actors et hello des infrastructures de Services sans état fiable en Java et c# dans Ajout tooguest exécutables et d’organiser des conteneurs Docker.  

> [!NOTE]
> Les infrastructures Reliable Collections ne sont pas encore prises en charge dans Linux. Les clusters seuls support ne sont pas pris en charge soit - qu’une seule zone et les clusters comportant plusieurs ordinateurs Azure Linux sont prises en charge dans l’aperçu de hello.
>
>


## <a name="supported-tooling"></a>Outils pris en charge
Aperçu de Hello prend en charge l’interaction avec le cluster hello via l’interface CLI de l’infrastructure de Service. Pour les développeurs Java, l’intégration avec Eclipse et Yeoman est assurée, la fonction Eclipse étant prise en charge sous Linux et OSX. Hello intégration de OSX utilise un VM Linux dans les coulisses de hello via vagrant. Pour les développeurs c#, l’intégration avec Yeoman est fournie toogenerate modèles d’application.

## <a name="next-steps"></a>Étapes suivantes

* Se familiariser avec hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) et [des Services fiables](service-fabric-reliable-services-introduction.md) infrastructures de programmation
* [Préparer votre environnement de développement sur Linux](service-fabric-get-started-linux.md)
* [Prepare your development environment on OSX (Préparer votre environnement de développement sur OSX)](service-fabric-get-started-mac.md)
* [Create your first Service Fabric Java application on Linux](service-fabric-create-your-first-linux-application-with-java.md)
* [Configurer l’intégration et le déploiement continus de Service Fabric avec Jenkins et GitHub](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [Différences entre Service Fabric Windows/Linux](service-fabric-linux-windows-differences.md)
