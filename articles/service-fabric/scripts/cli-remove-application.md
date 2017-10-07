---
title: aaaAzure Service Fabric CLI Script supprimer (exemple)
description: "Supprimer une application à partir d’un cluster Azure Service Fabric à l’aide de hello CLI d’Azure Service Fabric"
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Supprimer une application d’un cluster Service Fabric

Cet exemple de script supprime une instance en cours d’exécution de l’application Service Fabric, annule l’inscription d’un type d’application et la version du cluster de hello.  Instance de l’application hello suppression supprime également hello toutes les instances de service associés à cette application en cours d’exécution. Ensuite, les fichiers de l’application hello sont supprimés à partir du magasin d’images hello. 

Si nécessaire, installez hello [Service Fabric CLI](../service-fabric-cli.md).

## <a name="sample-script"></a>Exemple de script

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations, consultez hello [documentation relative à Service Fabric CLI](../service-fabric-cli.md).

Vous trouverez des exemples supplémentaires de Service Fabric CLI pour Azure Service Fabric Bonjour [exemples de Service Fabric CLI](../samples-cli.md).
