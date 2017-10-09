---
title: "vue d’ensemble d’aaaAzure Active Directory device registration | Documents Microsoft"
description: "L’inscription de périphérique Azure Active Directory est foundation hello pour les scénarios d’accès conditionnel basés sur l’appareil. Lorsqu’un appareil est inscrit, les dispositions de l’inscription de périphérique Azure Active Directory hello appareil avec une identité qui est utilisé tooauthenticate hello périphérique lorsque hello utilisateur se connecte."
services: active-directory
keywords: "enregistrement de l’appareil, activer l’enregistrement de l’appareil, enregistrement de l’appareil et MDM"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 1e92c1a2-01b8-4225-950b-373cd601b035
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: b9846e34fe873d271ebe71cbf8e70c6b4768885b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Prise en main du service Azure Active Directory Device Registration
L’inscription de périphérique Azure Active Directory est foundation hello pour les scénarios d’accès conditionnel basés sur l’appareil. Lorsqu’un appareil est inscrit, l’inscription de périphérique Azure Active Directory fournit appareil hello avec une identité qui est utilisé tooauthenticate hello périphérique lorsque hello utilisateur se connecte. Hello authentifié dispositif et attributs hello du périphérique de hello, peuvent ensuite être des stratégies d’accès conditionnel tooenforce utilisé pour les applications qui sont hébergées dans le cloud de hello et sur site.

Lorsqu’il est associé à une solution de management(MDM) des appareils mobiles tels que Microsoft Intune, les attributs d’appareil hello dans Azure Active Directory sont mis à jour avec des informations supplémentaires sur l’appareil de hello. Cela vous permet des règles d’accès conditionnel toocreate qui permettent d’accéder à partir d’appareils toomeet vos normes de conformité et de sécurité. Pour plus d’informations sur l’inscription d’appareils dans Microsoft Intune, consultez [Inscrire des appareils pour la gestion dans Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).

## <a name="scenarios-enabled-by-azure-active-directory-device-registration"></a>Scénarios permis par Azure Active Directory Device Registration
Azure Active Directory Device Registration prend en charge les appareils iOS, Android et Windows. Hello les scénarios individuels qui utilisent l’inscription de périphérique Azure AD peuvent avoir une plateforme prise en charge et des exigences plus spécifiques. Ces scénarios sont les suivants :

* **Tooapplications d’accès conditionnel qui sont hébergés sur site**: vous pouvez utiliser les appareils inscrits avec des stratégies d’accès pour les applications qui sont configurées toouse AD FS avec Windows Server 2012 R2. Pour plus d’informations sur la configuration d’un accès conditionnel en local, consultez la rubrique [Configuration d'un accès conditionnel en local à l'aide du service d'inscription d'appareils Azure Active Directory](active-directory-device-registration-on-premises-setup.md).
* **Accès conditionnel pour les applications Office 365 avec Microsoft Intune** : administrateurs informatiques peuvent configurer l’accès conditionnel appareil stratégies toosecure ressources d’entreprise, tandis qu’à hello même moment, ce qui permet de travailleurs sur les appareils compatibles services de hello tooaccess. Pour plus d’informations, consultez la rubrique [Stratégies d’accès conditionnel basées sur les appareils pour les services Office 365](active-directory-conditional-access-device-policies.md).

## <a name="setting-up-azure-active-directory-device-registration"></a>Configuration du service Azure Active Directory Device Registration
Vous avez besoin d’inscription de périphérique Azure AD tooenable Bonjour portail Azure afin que les appareils mobiles puissent détecter le service de hello en recherchant des enregistrements DNS connus. Vous devez configurer DNS de votre entreprise afin que les appareils Windows 10, Windows 8.1, Windows 7, Android et iOS peuvent découvrir et utiliser le service de hello.
Vous pouvez afficher et activer/désactiver les appareils inscrits via le portail d’administration de hello dans Azure Active Directory.

> [!NOTE]
> Pour obtenir des instructions plus récentes sur voir tooset d’inscription automatique, [comment toosetup l’enregistrement automatique du domaine Windows appareils joints à un avec Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).
> 
> 

### <a name="enable-azure-active-directory-device-registration-service"></a>Activer le service Azure Active Directory Device Registration
1. Se connecter toohello portail Microsoft Azure en tant qu’administrateur.
2. Dans le volet gauche de hello, sélectionnez **Active Directory**.
3. Sur hello **répertoire** , sélectionnez votre annuaire.
4. Sélectionnez hello **configurer** onglet.
5. Faites défiler la section toohello appelée **périphériques**.
6. Sélectionnez **TOUS** pour **LES UTILISATEURS PEUVENT JOINDRE DES APPAREILS À L’ESPACE DE TRAVAIL**.
7. Sélectionnez le nombre maximal de hello de périphériques souhaités tooauthorize par l’utilisateur.

> [!NOTE]
> L’inscription auprès de Microsoft Intune ou de Mobile Device Management pour Office 365 nécessite la jonction d’espace de travail. Si vous avez configuré un de ces services, tous est sélectionné et hello NONE bouton est désactivé.
> 
> 

Par défaut, l’authentification à deux facteurs n’est pas activée pour le service de hello. Elle est toutefois recommandée lors de l’inscription d’un appareil.

* Avant de demander une authentification à deux facteurs pour ce service, vous devez configurer un fournisseur d’authentification à deux facteurs dans Azure Active Directory et configurer vos comptes d’utilisateur pour l’authentification multifacteur, consultez [Ajout de multi-Factor TooAzure d’authentification Active Directory](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Si vous utilisez les services AD FS avec Windows Server 2012 R2, vous devez configurer un module d’authentification à deux facteurs dans ces services. Pour plus d’informations, consultez la page [Utilisation de Multi-Factor Authentication avec les services AD FS (Active Directory Federation Services)](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="configure-azure-active-directory-device-registration-discovery"></a>Configurer la détection du service Azure Active Directory Device Registration
Appareils Windows 7 et Windows 8.1 détecteront service d’inscription de périphérique hello en combinant le nom du compte d’utilisateur hello avec un nom de serveur d’inscription appareil connu.

Vous devez créer un enregistrement DNS CNAME qui pointe l’enregistrement de toohello A associé à votre service d’inscription de périphérique Azure Active Directory. Hello enregistrement CNAME doit utiliser enterpriseregistration de préfixe connu hello suivie suffixe UPN de hello utilisé par les comptes d’utilisateur hello dans votre organisation. Si votre organisation utilise plusieurs suffixes UPN, plusieurs enregistrements CNAME doivent être créés dans le DNS.

Par exemple, si vous utilisez deux suffixes UPN dans votre organisation nommés @contoso.com et @region.contoso.com, vous allez créer hello DNS les enregistrements suivants.

| Entrée | Type | Adresse |
| --- | --- | --- |
| enterpriseregistration.contoso.com |CNAME |enterpriseregistration.windows.net |
| enterpriseregistration.region.contoso.com |CNAME |enterpriseregistration.windows.net |

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Afficher et gérer des objets appareil dans Azure Active Directory
1. À partir du portail d’administration Azure hello, vous pouvez afficher, bloquer et débloquer des appareils. Un appareil bloqué n’aura plus accès tooapplications qui sont tooallow configuré uniquement pour les appareils inscrits.
2. Ouvrez une session toohello portail Microsoft Azure en tant qu’administrateur.
3. Dans le volet gauche de hello, sélectionnez **Active Directory**.
4. Sélectionnez votre annuaire.
5. Sélectionnez hello **utilisateurs** onglet. Puis sélectionnez un utilisateur tooview leurs appareils
6. Sélectionnez hello **périphériques** onglet.
7. Sélectionnez **les périphériques inscrits** de hello menu déroulant.
8. Ici, vous pouvez afficher, bloquer ou débloquer des appareils inscrits des utilisateurs hello.

## <a name="additional-topics"></a>Rubriques supplémentaires
Le service Azure Active Directory Device Registration vous permet d’inscrire vos appareils Windows 7 et Windows 8.1 joints à un domaine. Hello rubriques suivantes fournit plus d’informations sur les conditions préalables de hello et inscription d’appareils hello étapes tooconfigure requis sur les appareils Windows 7 et Windows 8.1.

* [Inscription automatique d’appareils auprès d’Azure Active Directory pour les appareils joints à un domaine Windows](active-directory-conditional-access-automatic-device-registration.md)
* [Inscription automatique auprès d’Azure Active Directory d’appareils Windows 10 joints à un domaine](active-directory-azureadjoin-devices-group-policy.md)

