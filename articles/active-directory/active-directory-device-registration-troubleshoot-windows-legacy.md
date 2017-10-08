---
title: ordinateurs joints au aaaTroubleshooting hello-inscription automatique de domaine Azure AD pour les clients de bas niveau Windows | Documents Microsoft
description: "Résolution des problèmes d’inscription automatique hello de domaine Azure AD joint les ordinateurs pour les clients de bas niveau de Windows."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a>Résolution des problèmes d’enregistrement automatique du domaine joint tooAzure d’ordinateurs Active Directory pour les clients de bas niveau de Windows 

Cette rubrique est applicable toohello uniquement après les clients : 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Pour Windows 10 ou Windows Server 2016, consultez [résolution des problèmes d’enregistrement automatique du domaine joint ordinateurs tooAzure AD – Windows 10 et Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).

Cette rubrique suppose que vous avez configuré l’inscription automatique des appareils joints au domaine comme expliqué dans décrites dans [comment tooconfigure l’inscription automatique de Windows appartenant au domaine des appareils avec Azure Active Directory](active-directory-device-registration-get-started.md).
 
Cette rubrique fournit des conseils sur la façon dont des problèmes potentiels de tooresolve de résolution des problèmes.  
Toonote de certains éléments de résultats : 

- L’inscription de ces clients sur Azure AD est par utilisateur/appareil. Par exemple : Si jdoe et jharnett connecter toothis périphérique, un enregistrement distinct (DeviceID) est créé pour chacun de ces utilisateurs dans l’onglet info d’utilisateur hello.  

- L’inscription de ces clients en dehors de la zone de hello est tootry configuré à l’ouverture et de verrouiller/déverrouiller et il peut y avoir de délai de 5 minutes que cela est déclenché à l’aide d’une tâche du Planificateur de tâches. 

- Réinstallation du système d’exploitation de hello ou annuler l’inscription manuelle et réinscrire peut créer une nouvelle inscription sur Azure AD et entraîne plusieurs entrées sous l’onglet d’informations utilisateur hello Bonjour portail Azure. 


## <a name="step-1-retrieve-hello-registration-status"></a>Étape 1 : Récupération de l’état de l’inscription de hello 

**état de l’inscription de hello tooverify :**  

1. Invite de commandes ouverte hello en tant qu’administrateur 

2. Saisissez `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

Cette commande affiche une boîte de dialogue qui vous offre plus de détails sur l’état de jointure hello.

![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a>Étape 2 : Évaluer l’état de l’inscription de hello 

Si la jointure de hello n’a pas réussi, boîte de dialogue hello vous offre plus d’informations sur le problème hello qui s’est produite.

**les problèmes les plus courants Hello sont :**

- Une mauvaise configuration d’AD FS ou d’Azure AD

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- Vous n’êtes pas connecté en tant qu’utilisateur du domaine

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- Un quota a été atteint.

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- Hello service ne répond pas 

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

Vous trouverez également des informations d’état hello dans le journal des événements hello sous **Applications et Services Log\Microsoft-jonction**.
  
**causes les plus courantes Hello pour un échec d’inscription sont :** 

- Votre ordinateur n’est pas sur le réseau interne de hello organisation ou un réseau privé virtuel sans connexion tooan locaux contrôleur de domaine Active Directory.

- Vous êtes connecté sur l’ordinateur tooyour avec un compte d’ordinateur local. 

- Problèmes de configuration du service : 

  - Hello serveur de fédération a été configuré toosupport **WIAORMULTIAUTHN**. 

  - Il n’existe aucun objet de Point de connexion qui pointe le nom de domaine vérifié tooyour dans Azure AD dans la forêt hello AD où appartient hello ordinateur.

  - Un utilisateur a atteint la limite de hello des périphériques. Consultez Prise en main du service Azure Active Directory Device Registration.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations, consultez hello [Forum aux questions sur l’inscription automatique](active-directory-device-registration-faq.md) 
