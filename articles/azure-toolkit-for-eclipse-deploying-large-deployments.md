---
title: "Réalisation de déploiements volumineux"
description: "Découvrez comment déployer des déploiements volumineux à l’aide de la Boîte à outils Azure pour Eclipse."
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
ms.openlocfilehash: e12e379e2b6727653e2377b1760c3745596a1e9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploying-large-deployments"></a>Réalisation de déploiements volumineux
Si votre déploiement est trop volumineux pour être contenu dans le dossier approot par défaut, vous pouvez utiliser une ressource de stockage local comme dossier racine de déploiement pour votre JDK et serveur d’applications.

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a>Pour utiliser une ressource de stockage local comme dossier racine de déploiement pour les déploiements à grande échelle
1. Créez une ressource de stockage local. Le nom de la ressource n’a pas d’importance. Les ressources de stockage sont définies au niveau du rôle. Pour accéder à la boîte de dialogue de configuration du stockage local, à partir de laquelle vous pouvez créer une ressource de stockage local, le plus rapide est de procéder comme suit : cliquez avec le bouton droit sur le rôle dans la vue **Explorateur de projets** (développez le nœud de votre projet Azure si le rôle n’est pas visible), cliquez sur **Azure**, puis sur **Stockage Local**. Dans la boîte de dialogue **Stockage Local**, cliquez sur **Ajouter** pour créer une ressource de stockage local.

2. Définissez une taille d’au moins 2 048 Mo (une valeur inférieure peut provoquer les mêmes problèmes de taille de fichier que ceux que vous rencontreriez dans approot).

3. Vérifiez que l’option **Nettoyer le contenu lorsque l’instance de rôle est recyclée** est activée. Elle empêchera la logique de démarrage du déploiement d’entrer en conflit avec les fichiers existants dans la ressource lors du recyclage de l’instance de rôle.

4. Assurez-vous que **Variable d’environnement stockant le chemin d’accès au répertoire de la ressource après le déploiement** a la valeur **DEPLOYROOT**. La boîte de dialogue de ressource de stockage local doit avoir l’aspect suivant.

   ![][ic667943]

En guise d’alternative, si vous utilisez **DEPLOYROOT** comme *nom* de votre ressource locale et que vous ne modifiez pas le nom de variable d’environnement généré automatiquement (à savoir, ici, **DEPLOYROOT_PATH**), cela fonctionnera également pour votre application.

Vous trouverez des informations supplémentaires sur la création d’une ressource de stockage local dans [Propriétés de stockage local][Local storage properties].

## <a name="see-also"></a>Voir aussi
[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]

[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Installation du kit de ressources Azure pour Eclipse][Installing the Azure Toolkit for Eclipse] 

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
