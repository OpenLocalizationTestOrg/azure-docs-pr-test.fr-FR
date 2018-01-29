---
title: "Utiliser l’émulateur express pour exécuter et déboguer un service cloud Azure sur un ordinateur local | Microsoft Docs"
description: "Utilisation de l’émulateur express pour exécuter et déboguer un service cloud sur une machine locale"
services: visual-studio-online
documentationcenter: n/a
author: mikejo
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: mikejo
ms.openlocfilehash: 9c258ad7de5e25b4b304f5e56d93abeff1187f71
ms.sourcegitcommit: b83781292640e82b5c172210c7190cf97fabb704
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2017
---
# <a name="using-emulator-express-to-run-and-debug-an-azure-cloud-service-on-a-local-machine"></a>Utiliser l’émulateur express pour exécuter et déboguer un service cloud Azure sur une machine locale
Avec l’émulateur express, vous testez et déboguez un service cloud sans avoir à exécuter Visual Studio en tant qu’administrateur. Vous pouvez définir les paramètres du projet pour utiliser l’émulateur express ou l’émulateur complet selon la configuration requise de votre service cloud. Pour plus d’informations sur l’émulateur complet, consultez [Exécuter une application Azure dans l’émulateur de calcul](storage/common/storage-use-emulator.md).

## <a name="using-emulator-express-in-visual-studio"></a>Utiliser l’émulateur express dans Visual Studio
Quand vous créez un projet Azure dans le Kit de développement logiciel (SDK) Azure 2.3 ou une version ultérieure, l’émulateur express est automatiquement utilisé. Dans le cas des projets existants créés à l’aide d’une version antérieure du Kit SDK Azure, suivez ces étapes pour sélectionner l’émulateur express :

1. Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.

1. Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le projet, puis, dans le menu contextuel, sélectionnez **Propriétés**.

1. Sur les pages de propriétés des projets, sélectionnez l’onglet **Web**.

    ![Propriétés pour un projet de service cloud Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. Sous **Serveur de développement local**, sélectionnez **l’option Utiliser IIS Express**.

1. Sous **Émulateur**, sélectionnez **Utiliser l’émulateur express**.
   
1. Pour lancer l’émulateur express, exécutez la commande suivante à l’invite de commande : 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Limitations de l’émulateur express
Les problèmes suivants sont des restrictions connues de l’émulateur express : 

- L’émulateur express n’est pas compatible avec le serveur web IIS.
- Votre service cloud peut contenir plusieurs rôles, mais chaque rôle est limité à une seule instance.
- Vous n’avez pas accès aux numéros de port inférieurs à 1 000. Si vous faites appel à un fournisseur d’authentification qui utilise habituellement un numéro de port inférieur à 1000, vous devrez peut-être remplacer cette valeur par un numéro de port supérieur à 1000.
- Les limitations qui s’appliquent à l’émulateur de calcul Azure s’appliquent aussi à l’émulateur express. Par exemple, il ne peut pas y avoir plus de 50 instances de rôle par déploiement. Pour plus d’informations sur l’émulateur de calcul Azure, consultez la page [Exécuter une application Azure dans l’émulateur de calcul](http://go.microsoft.com/fwlink/p/?LinkId=623050).

## <a name="next-steps"></a>Étapes suivantes
[Débogage des services cloud Azure](https://msdn.microsoft.com/library/azure/ee405479.aspx)
