---
title: "aaaCommon fabricclient ne les exceptions levées | Documents Microsoft"
description: "Décrit les exceptions common hello et les erreurs qui peuvent être levées par hello FabricClient APIs lors de l’exécution des opérations de gestion des applications et du cluster."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: bb821313-b221-479f-b08e-36cf07e60a07
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 55bb556b25150524ebc28756eb1bd3e91dc37853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="common-exceptions-and-errors-when-working-with-hello-fabricclient-apis"></a>Exceptions et des erreurs lorsque vous travaillez avec hello FabricClient APIs courants
Hello [fabricclient ne](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) API Active cluster application administrateurs tooperform tâches d’administration et sur une application, un service ou un cluster Service Fabric. Par exemple, déploiement d’application, mise à niveau et la suppression, la vérification d’intégrité de hello un cluster ou un service de test. Les développeurs d’applications et les administrateurs de cluster peuvent utiliser des outils de toodevelop de fabricclient n’API de hello pour la gestion des applications et le cluster Service Fabric de hello.

Il existe de nombreux types d'opérations qui peuvent être effectuées à l'aide de FabricClient.  Chaque méthode peut lever des exceptions pour les erreurs en raison de tooincorrect entrée, des erreurs d’exécution ou des problèmes d’infrastructure temporaire.  Consultez toofind de documentation de référence hello API les exceptions levées par une méthode spécifique. Quelques exceptions peuvent cependant être levées par de nombreuses autres API [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient). Hello tableau suivant répertorie les exceptions hello qui sont communes à hello FabricClient APIs.

| Exception | Générée lorsque |
| --- |:--- |
| [System.Fabric.FabricObjectClosedException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricobjectclosedexception#System_Fabric_FabricObjectClosedException) |Hello [fabricclient ne](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) objet est dans un état fermé. Dispose de hello [fabricclient ne](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) de l’objet vous utilisez et instanciez un nouvel [fabricclient ne](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) objet. |
| [System.TimeoutException](https://docs.microsoft.com/dotnet/core/api/system.timeoutexception#System_TimeoutException) |Hello délai d’attente. [OperationTimedOut](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) est retourné lorsque l’opération de hello prend plus de MaxOperationTimeout toocomplete. |
| [System.UnauthorizedAccessException](https://docs.microsoft.com/dotnet/core/api/system.unauthorizedaccessexception#System_UnauthorizedAccessException) |Échec de la vérification d’accès Hello pour l’opération de hello. E_ACCESSDENIED est renvoyée. |
| [System.Fabric.FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException) |Une erreur d’exécution s’est produite lors de l’exécution d’opération de hello. Une des méthodes de fabricclient n’hello susceptibles de lever [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException), hello [ErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException_ErrorCode) propriété indique la raison exacte de l’exception de hello hello. Codes d’erreur sont définis dans hello [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) énumération. |
| [System.Fabric.FabricTransientException](https://docs.microsoft.com/dotnet/api/system.fabric.fabrictransientexception#System_Fabric_FabricTransientException) |opération de Hello a échoué en raison de la condition d’erreur transitoire tooa quelconque. Par exemple, une opération peut échouer si un quorum de réplicas est temporairement inaccessible. Exceptions transitoires correspondent toofailed les opérations qui peuvent être retentées. |

Certaines erreurs [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) courantes peuvent être retournées dans une exception [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException) :

| Erreur | Condition |
| --- |:--- |
| CommunicationError |Une erreur de communication a provoqué hello opération toofail, opération hello de nouvelle tentative. |
| InvalidCredentialType |type d’informations d’identification Hello n’est pas valide. |
| InvalidX509FindType |Hello X509FindType n’est pas valide. |
| InvalidX509StoreLocation |emplacement du magasin Hello X509 n’est pas valide. |
| InvalidX509StoreName |nom du magasin Hello X509 n’est pas valide. |
| InvalidX509Thumbprint |chaîne de l’empreinte numérique du certificat Hello X509 n’est pas valide. |
| InvalidProtectionLevel |niveau de protection Hello n’est pas valide. |
| InvalidX509Store |Impossible d’ouvrir le magasin de certificats Hello X509. |
| InvalidSubjectName |nom de l’objet Hello n’est pas valide. |
| InvalidAllowedCommonNameList |format de chaîne dans une liste nom commun de Hello n’est pas valide. Ce doit être une liste séparée par des virgules. |

