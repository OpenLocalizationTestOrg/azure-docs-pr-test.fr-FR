---
title: "aaaAzure RemoteApp dépannage - échecs d’exécution et connexion d’Application | Documents Microsoft"
description: "Découvrez comment tootroubleshoot problèmes avec le démarrage et la connexion tooapplications dans Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e51d480c9d3fa1f2076f95b63c7a8cd2f6956a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a>Résoudre les problèmes liés à Azure RemoteApp : échecs de lancement et de connexion d’applications
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Les applications hébergées dans Azure RemoteApp peuvent échouer toolaunch pour différentes raisons. Cet article décrit les diverses raisons, les utilisateurs peuvent recevoir lorsque les messages d’erreur que vous essayez toolaunch applications. Il traite également des échecs de connexion. (Mais cet article ne décrit pas de problèmes lors de la signature dans le client d’Azure RemoteApp hello.)  

Lisez la suite pour plus d’informations sur les messages d’erreur courants en raison d’échecs de connexion et de lancement tooapp.

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a>Nous vous configurons... Réessayez dans 10 minutes.
Cette erreur signifie Qu'azure RemoteApp est l’évolution des besoins de capacité toomeet hello de vos utilisateurs. Dans l’arrière-plan de hello plusieurs instances de machine virtuelle de Azure RemoteApp sont créées besoins en capacité hello toohandle de vos utilisateurs. En général, cela prend environ cinq minutes mais peut prendre jusqu'à too10 minutes. Parfois, elle n’est pas assez rapide alors que vous avez besoin des ressources tout de suite. Par exemple un scénario de 9 : 00 où de nombreux utilisateurs doivent toouse votre application dans Azure RemoteAppn à hello même temps. Si cela produit tooyou nous pouvons activer **en mode de capacité** sur hello back-end. toodo ce ouvrir un ticket de Support de Azure. Être certain tooinclude votre ID d’abonnement dans la demande hello.  

![Nous vous configurons](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-tooyour-applications-please-re-launch-your-application"></a>Pu pas la reconnexion automatique tooyour applications. Veuillez relancer votre application
Ce message d’erreur est souvent si vous utilisez Azure RemoteApp et ensuite placez votre toosleep PC plu de 4 heures puis éveillé votre PC et hello Azure RemoteApp client tentative tooauto se reconnecter et délai d’attente a été dépassé.  Indiquer les utilisateurs toonavigate toohello arrière application et tenter de tooopen à partir de clients d’Azure RemoteApp hello.

![Pu pas la reconnexion automatique tooyour applications](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-hello-temp-profile"></a>Problèmes avec un profil temporaire de hello
Cette erreur se produit lorsque votre profil utilisateur (disque de profil utilisateur) a échoué toomount et d’utilisateur de hello a reçu un profil temporaire.  Les administrateurs doivent parcourir collection toohello Bonjour portail Azure et rendez-vous toohello **Sessions** onglet et essayez de trop**déconnexion** utilisateur de hello. Cela va forcer un journal complet de déconnecter la session d’utilisateur hello - puis disposez d’une application hello utilisateur tentative toolaunch à nouveau. En cas d’échec, contactez le support Azure.

## <a name="azure-remoteapp-has-stopped-working"></a>Azure RemoteApp a cessé de fonctionner
Ce message d’erreur signifie que les clients d’Azure RemoteApp hello rencontre un problème et doit toobe redémarré. Demander aux utilisateurs tooclose : sélectionnez **fermer le programme** , puis lancez à nouveau client d’Azure RemoteApp hello.  Si le problème de hello continue d’ouvrir et ticket de Support technique Azure.

![Azure RemoteApp a cessé de fonctionner](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-hello-connection-or-contact-your-system-administrator"></a>Une erreur s’est produite pendant que la connexion Bureau à distance accédait à la ressource. Tentatives de connexion de hello ou contactez votre administrateur système
Il s’agit d’un message d’erreur générique : contactez le support Azure pour que nous puissions examiner le problème. 

![Message Azure RemoteApp générique](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

