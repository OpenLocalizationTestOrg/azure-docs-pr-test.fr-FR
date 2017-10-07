---
title: "aaaTroubleshooting hybride Azure Active Directory joint des périphériques de bas niveau | Documents Microsoft"
description: "Dépannez des appareils hybrides de bas niveau joints à Azure Active Directory."
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a>Dépanner des appareils hybrides de bas niveau joints à Azure Active Directory 

Cette rubrique est applicable toohello uniquement suivant des appareils : 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Pour Windows 10 ou Windows Server 2016, consultez la page [Dépanner des appareils hybrides Windows 10 et Windows Server 2016 joints à Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-current.md).

Cette rubrique suppose que vous avez [configuré hybride Azure Active Directory des appareils joints à un](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport les scénarios suivants :

- Accès conditionnel basé sur les appareils

- [Itinérance d’entreprise des paramètres](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello Entreprise](active-directory-azureadjoin-passport-deployment.md) 





Cette rubrique fournit des conseils sur la façon dont des problèmes potentiels de tooresolve de résolution des problèmes.  

**Bon à savoir :** 

- nombre maximal de Hello de périphériques par utilisateur est centré sur l’appareil. Par exemple, si *jdoe* et *jharnett* tooa connexion périphérique, un enregistrement distinct (DeviceID) est créé pour chacun d’eux Bonjour **utilisateur** onglet info.  

- l’inscription initiale de Hello / joindre des appareils est configuré tooperform une tentative d’ouverture de session ou verrouiller / déverrouiller. Un délai de cinq minutes peut être déclenché par une tâche du Planificateur de tâches. 

- Une réinstallation du système d’exploitation de hello ou une manuelle annuler l’inscription et réinscrivez peuvent créer une nouvelle inscription sur Azure AD et résultats dans plusieurs entrées sous l’onglet d’informations utilisateur hello dans hello portail Azure. 


## <a name="step-1-retrieve-hello-registration-status"></a>Étape 1 : Récupération de l’état de l’inscription de hello 

**état de l’inscription de hello tooverify :**  

1. Invite de commandes ouverte hello en tant qu’administrateur 

2. Saisissez `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

Cette commande affiche une boîte de dialogue qui vous offre plus de détails sur l’état de jointure hello.

![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a>Étape 2 : Évaluer l’état de jointure hello hybrides Azure AD 

Si la jointure de hello hybrides Azure AD n’a pas réussi, boîte de dialogue hello vous offre plus d’informations sur le problème hello qui s’est produite.

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
  
**causes les plus courantes Hello pour une jointure de Azure AD hybride ayant échoué sont :** 

- Votre ordinateur n’est pas sur le réseau interne de hello organisation ou un réseau privé virtuel sans connexion tooan locaux contrôleur de domaine Active Directory.

- Vous êtes connecté sur l’ordinateur tooyour avec un compte d’ordinateur local. 

- Problèmes de configuration du service : 

  - Hello serveur de fédération a été configuré toosupport **WIAORMULTIAUTHN**. 

  - Il n’existe aucun objet de Point de connexion qui pointe le nom de domaine vérifié tooyour dans Azure AD dans la forêt hello AD où appartient hello ordinateur.

  - Un utilisateur a atteint la limite de hello des périphériques. 

## <a name="next-steps"></a>Étapes suivantes

Pour toute question, consultez hello [Forum aux questions sur la gestion des appareils](device-management-faq.md)  
