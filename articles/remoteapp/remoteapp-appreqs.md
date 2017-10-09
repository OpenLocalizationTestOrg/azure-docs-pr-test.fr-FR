---
title: "configuration requise d’aaaApp pour Azure RemoteApp | Documents Microsoft"
description: En savoir plus sur les exigences hello pour les applications que vous souhaitez toouse dans Azure RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a>Configuration requise des applications
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Azure RemoteApp prend en charge la diffusion en continu des applications Windows 32 bits ou 64 bits à partir d’une image de Windows Server 2012 R2. La plupart des applications Windows 32 bits ou 64 bits existantes s’exécutent « tel quel » dans l’environnement Azure RemoteApp (Services Bureau à distance ou anciennement Services Terminal Server). Toutefois, il existe une différence entre s’exécuter et fonctionner correctement : certaines applications fonctionnent bien et correctement, d’autres non. Hello informations suivantes fournit des conseils pour le développement d’applications dans un environnement de Services Bureau à distance et de test de la compatibilité de tooensure.

Info : nous travaillons sur la création de quelques exemples d’applications fonctionnelles pour vous. Vous verrez de nouvelles rubriques décrivant l’utilisation de Microsoft Access, QuickBooks et App-V dans RemoteApp.

## <a name="requirements"></a>Configuration requise
Si ces trois conditions sont réunies, votre application s’exécutera correctement dans RemoteApp :

1. Les applications qui répondent à tous les [conditions de Certification des applications de bureau Windows](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) et respecter trop[des Services Bureau à distance, les instructions de programmation](https://msdn.microsoft.com/library/aa383490.aspx) aura une compatibilité complète avec RemoteApp.
2. Les applications doivent jamais stocker des données localement sur l’image de hello ou des instances de RemoteApp qui peuvent être perdues.  Après avoir créé une collection RemoteApp, les instances de hello sont clonés et sont sans état et ne doivent contenir que des applications. Stocker les données d’une source externe, ou dans le profil de l’utilisateur hello.
3. Les images personnalisées ne doivent jamais contenir de données pouvant être perdues.  

## <a name="testing-your-apps"></a>Test de vos applications
Utilisez ces applications de tootesting comme suit :

1. Installez Windows Server 2012 R2 et votre application
2. Activez le Bureau à distance
3. Créez deux comptes d’utilisateur, l’UtilisateurA et UserB, ajouter les deux groupes de sécurité utilisateur comptes toohello Bureau à distance.
4. Vérifier la compatibilité des session multiples en établissant des deux toohello de sessions Bureau à distance simultanées PC lors du lancement d’application hello.
5. Validation du comportement de l’application

## <a name="application-development-guidelines"></a>Conseils pour le développement d’applications
Utilisez hello suivant les instructions pour le développement d’applications pour RemoteApp.

### <a name="multiple-users"></a>Plusieurs utilisateurs
* L’installation d’une [application pour un seul utilisateur ](https://msdn.microsoft.com/library/aa380661.aspx)peut créer des problèmes dans un environnement multi-utilisateur.
* Les applications doivent [stockent des informations spécifiques à l’utilisateur](https://msdn.microsoft.com/library/aa383452.aspx) dans des emplacements spécifiques à l’utilisateur, séparément à partir des informations globales qui s’applique aux utilisateurs de tooall.
* RemoteApp utilise plusieurs [espaces de noms pour les objets de noyau](https://msdn.microsoft.com/library/aa382954.aspx); un espace de noms global est utilisé principalement par les services dans les applications client/serveur.
* Il n’est pas sécurisé tooassume qui hello nom d’ordinateur ou hello [adresse IP](https://msdn.microsoft.com/library/aa382942.aspx) toohello attribué ordinateur associés à un seul utilisateur, car plusieurs utilisateurs peuvent être connectés simultanément tooa hôte de Session Bureau à distance (la Session Bureau à distance Serveur hôte).

### <a name="performance"></a>Performances
* Désactiver [effets](https://msdn.microsoft.com/library/aa380822.aspx) avant d’ajouter votre tooRemoteApp d’application.
* disponibilité toomaximize du processeur pour tous les utilisateurs, soit désactiver [tâches en arrière-plan ](https://msdn.microsoft.com/library/aa380665.aspx) ou créer des tâches en arrière-plan efficace qui ne sont pas beaucoup de ressources.
* Paramétrez et équilibrez l’ [utilisation de threads](https://msdn.microsoft.com/library/aa383520.aspx) de l’application pour un environnement multi-utilisateur et multiprocesseur.
* toooptimize des performances, il est conseillé pour les applications trop[détecter](https://msdn.microsoft.com/library/aa380798.aspx) qui s’exécutent dans une session client.

