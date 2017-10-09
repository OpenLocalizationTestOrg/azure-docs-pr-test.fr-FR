---
title: "aaaAzure FAQ sur la gestion Active Directory périphérique | Documents Microsoft"
description: FAQ sur la gestion des appareils Azure Active Directory.
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
ms.openlocfilehash: 000eb6a930187e13cb24cf628793afd06813be23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-device-management-faq"></a>FAQ sur la gestion des appareils Azure Active Directory

**Q : j’inscrit les appareils hello récemment. Pourquoi ne peux pas voir les périphériques hello sous Mes infos utilisateur Bonjour portail Azure ?**

**R :** les appareils Windows 10 qui sont joints à un domaine avec l’inscription automatique ne s’affichent pas sous les informations d’utilisateur hello.
Vous devez toouse PowerShell toosee tous les appareils. 

Uniquement hello périphériques suivants sont répertoriés sous les informations d’utilisateur hello :

- Tous les appareils personnels qui ne sont pas joints à une entreprise 
- Tous les appareils non Windows 10 / Windows Server 2016 
- Tous les appareils non Windows 

---

**Q : Pourquoi ne puis-je pas voir tous les appareils hello inscrits dans Azure Active Directory Bonjour portail Azure ?** 

**R :** , il n’existe actuellement aucune toosee de façon tous les appareils inscrits Bonjour portail Azure. Vous pouvez utiliser Azure PowerShell toofind tous les appareils. Pour plus d’informations, consultez hello [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) applet de commande.

--- 

**Q : comment savoir quel état de l’inscription de périphérique hello du client de hello est ?**

**R :** dépend de l’état de l’inscription de périphérique hello :

- Quel périphérique hello est
- de la manière dont il a été inscrit ; 
- Les informations relatives à tooit. 
 

---

**Q : Pourquoi est un périphérique que j’ai supprimé Bonjour Azure portal ou à l’aide de Windows PowerShell toujours répertoriés comme inscrit ?**

**R :** Il s’agit du comportement par défaut. Appareil de Hello n’auront pas accès tooresources dans le cloud de hello. Si vous voulez tooremove hello périphérique et inscrivez de nouveau, une action manuelle doit être toobe effectuée sur le périphérique de hello. 

Pour Windows 10 et Windows Server 2016 sur site AD et joints à un domaine :

1.  Ouvrez l’invite de commandes hello en tant qu’administrateur.

2.  Saisissez `dsregcmd.exe /debug /leave`

3.  Se déconnecter et se dans la tâche planifiée tootrigger hello qui inscrit le périphérique de hello à nouveau. 

Pour les autres plateformes Windows sur site AD et jointes à un domaine :

1.  Ouvrez l’invite de commandes hello en tant qu’administrateur.
2.  Saisissez `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.
3.  Saisissez `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.

---

**Q : Pourquoi le portail Azure affiche-t-il des entrées d’appareils dupliquées ?**

**R :**

-   Pour Windows 10 et Windows Server 2016, s’ils sont des tentatives répétées toounjoin et joignez de nouveau hello même appareil, il peut y avoir des entrées en double. 

-   Si vous avez utilisé Ajouter compte professionnel ou scolaire, chaque utilisateur de windows qui utilise Ajouter compte professionnel ou scolaire créera un nouvel enregistrement d’appareil avec hello même nom de périphérique.

-   Autres plates-formes Windows local AD appartenant au domaine à l’aide de l’inscription automatique créera un nouvel enregistrement d’appareil avec hello même nom de périphérique pour chaque utilisateur de domaine qui se connecte à un périphérique de hello. 

-   Un ordinateur AADJ qui a été réinitialisé, réinstallé et nouveau en souscrivant hello même nom, apparaîtront en tant qu’un autre enregistrement hello même nom de périphérique.

---

**Q : Pourquoi peut un utilisateur encore accéder aux ressources d’un appareil, que j’ai désactivé Bonjour portail Azure ?**

**R :** peut prendre jusqu'à une heure tooan pour un toobe revoke appliqué.

>[!Note] 
>Pour les appareils perdus, nous vous recommandons de réinitialisation hello tooensure de périphérique que les utilisateurs ne peut pas accéder à des appareils de hello. Pour plus d’informations, consultez [Inscrire des appareils pour la gestion dans Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune). 


---

**Q : Pourquoi mes utilisateurs voient-ils s’afficher « Vous ne pouvez pas accéder à cet emplacement à partir d’ici » ?**

**R :** si vous avez configuré certain toorequire de règles d’accès conditionnel un état de périphérique spécifique et les appareils hello ne répond pas aux critères de hello, les utilisateurs sont bloquées et ce message s’affiche. Veuillez évaluer les règles de hello et assurez-vous de cet appareil hello est en mesure de toomeet hello critères tooavoid ce message.

---


**Q : je consultez enregistrement d’appareil hello sous les informations d’utilisateur hello Bonjour portail Azure et que vous pouvez voir l’état de hello tel qu’enregistré sur le client de hello. Ma configuration est-elle correcte pour l’utilisation de l’accès conditionnel ?**

**R :** enregistrement d’appareil hello (deviceID) et son état sur hello portail Azure doivent correspondre à des clients de hello et répondent à tous les critères d’évaluation pour l’accès conditionnel. Pour plus d’informations, consultez [Bien démarrer avec le service Azure Active Directory Device Registration](active-directory-device-registration.md).

---

**Q : je reçois un message « nom d’utilisateur ou mot de passe est incorrect » pour un périphérique j’ai viennent de rejoindre tooAzure AD ?**

**R :** Les raisons les plus courantes sont les suivantes :

- Vos informations d’identification ne sont plus valides.

- Votre ordinateur est toocommunicate impossible avec Azure Active Directory. Vérifiez les éventuels problèmes de connectivité réseau.

- Bonjour Azure AD Join conditions préalables n’ont pas été respectées. Veuillez vous assurer que vous avez suivi les étapes de hello pour [extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join](active-directory-azureadjoin-overview.md).  

- Connexions fédérées nécessite votre toosupport de serveur de fédération un point de terminaison WS-Trust active. 

---

**Q : Pourquoi hello « Désolé... une erreur s’est produite ! « boîte de dialogue lors de le ne joignez pas mon ordinateur ?**

**R :** Cela résulte de la configuration de l’inscription Azure Active Directory avec Intune. Pour plus d’informations, consultez [Configurer la gestion des appareils Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).  

---

**Q : Pourquoi mon toojoin tentative un PC échouer même si je n’ai reçu aucune information d’erreur ?**

**R :** une cause possible est que l’utilisateur hello est enregistré dans le périphérique toohello à l’aide du compte d’administrateur intégré hello. Créez un autre compte local avant d’utiliser le programme d’installation de Azure Active Directory Join toocomplete hello. 

---

**Q : où puis-je trouver des instructions d’inscription automatique pour le programme d’installation Bonjour ?**

**R :** pour obtenir des instructions détaillées, consultez [comment tooconfigure l’inscription automatique de Windows appartenant au domaine des appareils avec Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

---

**Q : où puis-je trouver dépannage plus d’informations sur l’inscription automatique hello ?**

**R :** Pour obtenir des informations de résolution des problèmes, consultez :

- [Résolution des problèmes d’enregistrement automatique du domaine joint ordinateurs tooAzure AD – Windows 10 et Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)

- [Résolution des problèmes d’enregistrement automatique du domaine joint tooAzure d’ordinateurs Active Directory pour les clients de bas niveau de Windows](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

