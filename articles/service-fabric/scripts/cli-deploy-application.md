---
title: "aaaAzure exemple de déploiement de Script Service Fabric CLI"
description: "Déployer un cluster d’Azure Service Fabric tooan application à l’aide de hello CLI d’Azure Service Fabric"
services: service-fabric
documentationcenter: 
author: Thraka
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Déployer un cluster de Service Fabric application tooa

Cet exemple de script copie d’un magasin d’image application package tooa cluster enregistre le type de l’application hello dans un cluster de hello et crée une instance d’application à partir du type d’application hello. Tous les services par défaut sont également créés à ce stade.

Si nécessaire, installez hello [Service Fabric CLI](../service-fabric-cli.md).

## <a name="sample-script"></a>Exemple de script

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement

Lorsque vous avez terminé, hello [supprimer](cli-remove-application.md) script peut être utilisé tooremove hello application. script de suppression Hello supprime l’instance de l’application hello annule l’inscription du type de l’application hello et supprime le package d’application hello du magasin d’images.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations, consultez hello [documentation relative à Service Fabric CLI](../service-fabric-cli.md).

Vous trouverez des exemples supplémentaires de Service Fabric CLI pour Azure Service Fabric Bonjour [exemples de Service Fabric CLI](../samples-cli.md).
