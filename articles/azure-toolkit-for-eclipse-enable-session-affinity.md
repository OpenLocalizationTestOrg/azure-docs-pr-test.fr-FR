---
title: "à l’aide de l’affinité de Session aaaEnable hello boîte à outils Azure pour Eclipse"
description: "Découvrez comment l’affinité de session tooenable à l’aide hello boîte à outils Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a>Activer l'affinité de session
Dans la boîte à outils Azure pour Eclipse de hello, vous pouvez activer l’affinité de session HTTP, ou « sessions rémanentes » pour vos rôles. Hello image suivante montre hello **l’équilibrage de charge** fonctionnalité d’affinité de propriétés boîte de dialogue utilisée tooenable hello session :

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a>affinité de session tooenable pour votre rôle.
1. Sur le rôle hello dans l’Explorateur de projets d’Eclipse, cliquez **Azure**, puis cliquez sur **l’équilibrage de charge**.

2. Bonjour **propriétés de l’équilibrage de charge WorkerRole1** boîte de dialogue :

   a. Cochez **Activer l'affinité de session HTTP (sessions temporaires) pour ce rôle.**

   b. Pour **d’entrée de point de terminaison toouse**, sélectionnez un point de terminaison d’entrée toouse, par exemple, **http (public : 80, privé : 8080)**. Votre application doit utiliser ce point de terminaison en tant que point de terminaison HTTP. Vous pouvez activer plusieurs points de terminaison pour votre rôle, mais vous pouvez sélectionner qu’un seul d'entre eux toosupport sessions rémanentes.

   c. Régénérez votre application.

Une fois activée, si vous avez plusieurs instances de rôle, les demandes HTTP provenant d’un client particulier continuera gérées par hello même instance de rôle.

Hello boîte à outils Eclipse permet cela en installant un module IIS spécial appelé Application Request Routing (ARR) dans chacune de vos instances de rôle. ARR redirige l’instance de rôle appropriée de toohello de demandes HTTP. Hello toolkit reconfigure automatiquement le point de terminaison hello sélectionné afin que le trafic HTTP entrant de hello est premier toohello routé ARR logiciel. boîte à outils Hello crée également un nouveau point de terminaison interne votre serveur Java est configuré toolisten à. Qui est le point de terminaison hello utilisé par instance de rôle appropriée toohello le trafic HTTP de ARR tooreroute hello. De cette manière, chaque instance de rôle dans votre déploiement multi-instance sert de proxy inverse pour toutes les hello autres instances, en activant des sessions rémanentes.

## <a name="notes-about-session-affinity"></a>Remarques sur l'affinité de session
* Affinité de session ne fonctionne pas dans l’émulateur de calcul hello. Hello paramètres peuvent être appliquées dans l’émulateur de calcul hello sans interférer avec votre processus de génération ou de l’exécution de l’émulateur de calcul, mais la fonction hello elle-même ne fonctionne pas dans l’émulateur de calcul hello.

* L’activation de l’affinité de session entraîne une augmentation de la quantité hello d’espace disque pris en charge par votre déploiement dans Azure, comme des logiciels supplémentaires seront téléchargés et installés dans vos instances de rôle lorsque votre service est démarré en hello cloud Azure.

* Hello temps tooinitialize chaque rôle prend plus de temps.

* Un point de terminaison interne, toofunction comme un RE-routeur de trafic comme indiqué ci-dessus, est ajouté.


## <a name="see-also"></a>Voir aussi
[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]

[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Lors de l’installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse] 

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
