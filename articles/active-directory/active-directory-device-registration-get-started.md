---
title: "aaaHow tooconfigure l’inscription automatique des périphériques joints au domaine de Windows avec Azure Active Directory | Documents Microsoft"
description: "Configurer votre tooregister d’appareils Windows joints automatiquement et silencieusement avec Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Prise en main du service Azure Active Directory Device Registration

L’inscription de périphérique Azure Active Directory est foundation hello pour les scénarios d’accès conditionnel basés sur l’appareil. Lorsqu’un appareil est inscrit, l’inscription de périphérique Azure Active Directory fournit appareil hello avec une identité qui est utilisé tooauthenticate hello périphérique lorsque hello utilisateur se connecte. Hello authentifié dispositif et attributs hello du périphérique de hello, peuvent ensuite être des stratégies d’accès conditionnel tooenforce utilisé pour les applications qui sont hébergées dans le cloud de hello et sur site.

Lorsqu’il est associé à une solution de management(MDM) des appareils mobiles tels que Microsoft Intune, les attributs d’appareil hello dans Azure Active Directory sont mis à jour avec des informations supplémentaires sur l’appareil de hello. Cela vous permet des règles d’accès conditionnel toocreate qui permettent d’accéder à partir d’appareils toomeet vos normes de conformité et de sécurité. Pour plus d’informations sur l’inscription d’appareils dans Microsoft Intune, consultez Inscrire des appareils pour la gestion dans Intune.
Les scénarios mis en œuvre par Azure Active Directory Device Registration incluent la prise en charge des appareils iOS, Android et Windows. Hello les scénarios individuels qui utilisent l’inscription d’Azure Active Directory pour appareils peuvent avoir une plateforme prise en charge et des exigences plus spécifiques. 

Ces scénarios sont les suivants :

- **Accès conditionnel pour les applications Office 365 avec Microsoft Intune :** administrateurs informatiques peuvent configurer l’accès conditionnel appareil stratégies toosecure ressources d’entreprise, tandis qu’à hello même moment, ce qui permet de travailleurs sur les appareils compatibles services de hello tooaccess. Pour plus d’informations, consultez la rubrique Stratégies d’accès conditionnel basées sur les appareils pour les services Office 365.

- **Tooapplications d’accès conditionnel qui sont hébergées en local :** vous pouvez utiliser les appareils inscrits avec des stratégies d’accès pour les applications qui sont configurées toouse AD FS avec Windows Server 2012 R2. Pour plus d’informations sur la configuration d’un accès conditionnel en local, consultez la rubrique [Configuration d'un accès conditionnel en local à l'aide du service d'inscription d'appareils Azure Active Directory](active-directory-device-registration-on-premises-setup.md).

## <a name="setting-up-azure-active-directory-device-registration"></a>Configuration du service Azure Active Directory Device Registration

l’inscription de périphérique toosetup, vous disposez de plusieurs options :

- Les appareils peuvent s’inscrire lorsque tooAzure jointes AD domaine. Pour plus d’informations sur cette rubrique, vous pouvez plus d’informations sur les paramètres de Azure AD Join et hello requis pour les utilisateurs domaine toojoin Azure AD.

- Les appareils peuvent être inscrits lorsque le travail ajouter des utilisateurs ou les comptes de l’école tooWindows sur un appareil personnel ou lorsque les appareils mobiles connectent tooa les ressources de travail nécessitant l’enregistrement. tooensure, vous devez activer l’inscription Azure Active Directory pour appareils dans hello portail Azure. 

- Les appareils peuvent être inscrits à l’aide d’une inscription automatique pour les ordinateurs traditionnels joints au domaine. tooensure, vous devez la première installation Azure AD Connect avant de continuer l’inscription automatique.

Pour obtenir des instructions plus récente, consultez [comment tooconfigure l’inscription automatique de Windows appartenant au domaine des appareils avec Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).  
Vous pouvez également examiner et activer ou désactiver les appareils inscrits via le portail d’administration de hello dans Azure Active Directory.

## <a name="enable-hello-azure-active-directory-device-registration-service"></a>Activer le service d’inscription de hello Azure Active Directory appareils

**hello tooenable service d’inscription de périphérique Azure Active Directory :**

1.  Se connecter toohello portail Microsoft Azure en tant qu’administrateur.

2.  Dans le volet gauche de hello, sélectionnez **Active Directory**.

3.  Sur l’onglet du répertoire hello, sélectionnez votre annuaire.

4.  Cliquez sur **Configurer**.

5.  Faites défiler trop**périphériques**.

6.  Sélectionnez TOUS pour LES UTILISATEURS PEUVENT INSCRIRE LEURS APPAREILS SUR AZURE AD.

7.  Sélectionnez le nombre maximal de hello de périphériques souhaités tooauthorize par l’utilisateur.

Hello l’inscription avec Microsoft Intune ou gestion des appareils mobiles pour Office 365 nécessite l’inscription de l’appareil. Si vous avez configuré l’un de ces services, **TOUS** est sélectionné et **AUCUN** est désactivé. Veuillez vous assurer qu’ils sont configurés correctement et la gestion des licences appropriées hello.

Par défaut, l’authentification à deux facteurs n’est pas activée pour le service de hello. Elle est toutefois recommandée lors de l’inscription d’un appareil.

- Avant de demander une authentification à deux facteurs pour ce service, vous devez configurer un fournisseur d’authentification à deux facteurs dans Azure Active Directory et configurer vos comptes d’utilisateur pour l’authentification multifacteur, consultez Ajout de l’authentification multifacteur tooAzure Active Directory

- Si vous utilisez les services AD FS avec Windows Server 2012 R2, vous devez configurer un module d’authentification à deux facteurs dans ces services. Pour plus d’informations, consultez la page Utilisation de Multi-Factor Authentication avec les services AD FS (Active Directory Federation Services).

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Afficher et gérer des objets appareil dans Azure Active Directory

À partir du portail d’administration Azure hello, vous pouvez afficher, bloquer et débloquer des appareils. Un appareil bloqué n’aura plus accès tooapplications qui sont tooallow configuré uniquement pour les appareils inscrits.

**tooview et gérer des objets appareil dans Azure Active Directory :**
 
1.  Ouvrez une session toohello portail Microsoft Azure en tant qu’administrateur.

2.  Dans le volet gauche de hello, sélectionnez **Active Directory**.

3.  Sélectionnez votre annuaire.

4.  Sélectionnez **Utilisateurs**. 

5.  Cliquez sur utilisateur hello pour lequel vous souhaitez que les appareils de hello toosee.

6.  Sélectionnez **Appareils**.

7.  Sélectionnez **Appareils inscrits**.

Vous pouvez à présent, passez en revue, bloquer ou débloquer des appareils inscrits de l’utilisateur hello.
Les appareils Windows 10 qui sont automatiquement inscrits et joint au domaine local n’apparaissent pas sous l’onglet utilisateurs de hello. Utilisez toofind de commande PowerShell de Get-MsolDevice hello tous les périphériques de votre entreprise. 


## <a name="next-steps"></a>Étapes suivantes

toosetup automatisée de l’inscription de périphérique, consultez [comment tooconfigure l’inscription automatique de Windows appartenant au domaine des appareils avec Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).


