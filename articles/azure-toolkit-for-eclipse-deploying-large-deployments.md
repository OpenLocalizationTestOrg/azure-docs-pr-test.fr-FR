---
title: "aaaDeploying déploiements à grande échelle"
description: "Découvrez comment toodeploy déploiements à grande échelle à l’aide de hello boîte à outils Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a>Réalisation de déploiements volumineux
Si votre déploiement est trop grande toobe contenu dans le dossier approot de hello par défaut, vous pouvez utiliser une ressource de stockage local en tant que dossier racine de déploiement hello pour votre JDK et serveur d’applications.

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a>toouse une ressource de stockage local en tant que dossier racine de déploiement hello pour les déploiements à grandes échelle
1. Créez une ressource de stockage local. nom Hello de ressource de hello n’a pas d’importance. Ressources de stockage sont définies au niveau du rôle hello. Hello plus rapide moyen tooaccess hello stockage local configuration boîte de dialogue, à partir de laquelle vous pouvez créer une ressource de stockage local, est à l’aide de hello comme suit : rôle de hello avec le bouton droit dans hello **Explorateur de projets** vue (développez votre Nœud de projet Azure si vous ne voyez pas le rôle de hello), cliquez sur **Azure**, puis cliquez sur **stockage Local**. Au sein de hello **stockage Local** boîte de dialogue, cliquez sur **ajouter** toocreate une ressource de stockage local.

2. Ensemble hello souhaité taille tooat au moins 2 048 Mo (quoi que ce soit inférieure peut entraîner hello mêmes problèmes de taille de fichier que vous pouvez rencontrer dans approot de hello).

3. Vérifiez que **nettoyer le contenu de hello lorsque l’instance de rôle hello est recyclé** est vérifiée ; cela empêchera la logique de démarrage du déploiement hello d’entrer en conflit avec les fichiers existants dans la ressource de hello lorsque hello rôle instance est recyclée.

4. Vérifiez que hello **stockage variable environnement hello le chemin d’accès du répertoire de la ressource après le déploiement** a la valeur chaîne de toohello **DEPLOYROOT**. Votre boîte de dialogue de ressource de stockage local recherche similaire toohello suivant.

   ![][ic667943]

Vous pouvez également, si vous utilisez **DEPLOYROOT** comme hello *nom* de votre ressource locale et que vous ne modifiez pas le nom de variable de généré automatiquement l’environnement hello (qui sera défini trop **DEPLOYROOT_PATH** dans ce cas), qui doit s’exécuter pour votre application.

Vous trouverez des informations supplémentaires sur la création d’une ressource de stockage local dans [Propriétés de stockage local][Local storage properties].

## <a name="see-also"></a>Voir aussi
[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]

[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Lors de l’installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse] 

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
