---
title: aaaConfigure un projet de service cloud Azure avec Visual Studio | Documents Microsoft
description: "Découvrez comment tooconfigure Azure cloud projet de service dans Visual Studio, selon vos spécifications pour ce projet."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a>Configurer un projet de service cloud Azure avec Visual Studio
Vous pouvez configurer un projet de service cloud Azure selon vos spécifications pour ce projet. Vous pouvez définir des propriétés de projet hello pour hello suivant des catégories :

- **Publier un tooAzure de service cloud** -vous pouvez définir un toomake propriété sûr qu’un tooAzure de déployé le service cloud existant n’est pas supprimé par inadvertance.
- **Exécuter ou déboguer un service cloud sur l’ordinateur local de hello** -vous pouvez sélectionner un toouse de configuration de service et indiquer si vous souhaitez que l’émulateur de stockage Azure toostart hello.
- **Valider un package de service cloud lors de sa création** -vous pouvez décider tootreat tous les avertissements comme des erreurs afin que vous pouvez vous assurer de ce package de service cloud hello déploie sans problème. 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a>Étapes tooconfigure un projet de service cloud Azure
1. Ouvrir ou créer un projet de service cloud dans Visual Studio

1. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello et, dans le menu contextuel de hello, sélectionnez **propriétés**.
   
1. Dans la page de propriétés du projet hello, sélectionnez hello **développement** onglet.

    ![Menu des propriétés du projet](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. Définissez **demander confirmation avant de supprimer un déploiement existant** trop**True**. Ce paramètre permet de tooensure vous ne supprimez accidentellement un déploiement existant dans Azure

1. Sélectionnez hello souhaité **configuration du Service** tooindicate la configuration de service que vous souhaitez toouse lorsque vous exécutez ou déboguez votre service cloud localement. Pour plus d’informations sur la façon de toomodify une configuration de service pour un rôle, consultez [tooconfigure les rôles de hello pour Azure cloud service avec Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).

1. Définissez **émulateur de stockage Azure de démarrer** trop**True** toostart l’émulateur de stockage Azure hello lorsque vous exécutez ou déboguez votre service cloud localement.

1. Définissez **considérer les avertissements comme des erreurs** trop**True** toomake que vous ne pouvez pas publier s’il existe des erreurs de validation de package.

1. Définissez **utiliser des ports du projet web** trop**True** toomake sûr que votre rôle web utilise hello même port à chaque démarrage local dans IIS Express.

1. Dans la barre d’outils de Visual Studio hello, sélectionnez **enregistrer**.

## <a name="next-steps"></a>Étapes suivantes
- [Configurer un projet Azure à l'aide de plusieurs configurations de service](vs-azure-tools-multiple-services-project-configurations.md)

