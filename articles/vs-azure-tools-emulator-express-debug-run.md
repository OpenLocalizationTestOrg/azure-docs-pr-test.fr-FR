---
title: "toorun d’émulateur Express aaaUsing et debug Azure cloud service sur un ordinateur local | Documents Microsoft"
description: "À l’aide de toorun d’émulateur Express et déboguer un service cloud sur un ordinateur local"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a>L’émulateur Express toorun et debug Azure cloud service sur un ordinateur local
Avec l’émulateur express, vous testez et déboguez un service cloud sans avoir à exécuter Visual Studio en tant qu’administrateur. Vous pouvez définir votre toouse de paramètres de projet à l’émulateur Express ou hello émulateur complet, selon les spécifications de hello de votre service cloud. Pour plus d’informations sur l’émulateur complet hello, consultez [exécuter une Application Azure dans l’émulateur de calcul de hello](storage/common/storage-use-emulator.md).

## <a name="using-emulator-express-in-visual-studio"></a>Utiliser l’émulateur express dans Visual Studio
Quand vous créez un projet Azure dans le Kit de développement logiciel (SDK) Azure 2.3 ou une version ultérieure, l’émulateur express est automatiquement utilisé. Pour les projets existants qui ont été créées avec une version antérieure de hello Azure SDK, utilisez hello suivant tooselect étapes émulateur Express :

1. Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.

1. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello et, dans le menu contextuel de hello, sélectionnez **propriétés**.

1. Dans les pages de propriétés de projets hello, sélectionnez hello **Web** onglet.

    ![Propriétés pour un projet de service cloud Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. Sous **Serveur de développement local**, sélectionnez **l’option Utiliser IIS Express**.

1. Sous **Émulateur**, sélectionnez **Utiliser l’émulateur express**.
   
1. toolaunch hello émulateur Express, exécutez hello commande à l’invite de commande suivante : 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Limitations de l’émulateur express
restrictions de l’émulateur Express est connue par Hello suivants : 

- L’émulateur express n’est pas compatible avec le serveur web IIS.
- Votre service cloud peut contenir plusieurs rôles, mais chaque rôle est limitée tooone instance.
- Vous n’avez pas accès aux numéros de port inférieurs à 1 000. Si vous utilisez un fournisseur d’authentification qui utilise généralement un port inférieur à 1000, vous devrez peut-être toochange ce numéro de port tooa valeur qui est supérieur à 1000.
- Les restrictions qui s’appliquent toohello émulateur de calcul Azure s’appliquent également à tooEmulator Express. Par exemple, il ne peut pas y avoir plus de 50 instances de rôle par déploiement. Pour plus d’informations sur hello émulateur de calcul Azure, consultez [exécuter une Application Azure dans l’émulateur de calcul de hello](http://go.microsoft.com/fwlink/p/?LinkId=623050).

## <a name="next-steps"></a>Étapes suivantes
[Débogage des services cloud Azure](https://msdn.microsoft.com/library/azure/ee405479.aspx)
