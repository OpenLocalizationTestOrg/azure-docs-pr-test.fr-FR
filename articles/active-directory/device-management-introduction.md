---
title: gestion de toodevice aaaIntroduction dans Azure Active Directory | Documents Microsoft
description: "Découvrez comment la gestion des appareils peut vous aider à tooget contrôler les appareils hello qui accèdent à des ressources dans votre environnement."
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
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a>Gestion de toodevice introduction dans Azure Active Directory

Dans un monde mobile en premier, privilégie le cloud, Azure Active Directory (Azure AD) permet de toodevices de l’authentification unique, les applications et services à partir de n’importe quel endroit. Avec la prolifération de hello de périphériques - y compris votre propre appareil BYOD (Bring), les professionnels de l’informatique sont confrontés à deux objectifs différents :

- Permettre aux toobe des utilisateurs finaux hello productif où et quand
- Protéger les ressources d’entreprise de hello à tout moment

Par le biais des appareils, vos utilisateurs accèdent tooyour des ressources d’entreprise. tooprotect vos ressources d’entreprise, comme un administrateur, vous voulez contrôler toohave ces appareils. Cela vous permet de toomake sûr que vos utilisateurs sont l’accès à vos ressources à partir de périphériques qui répondent à vos normes de conformité et de sécurité. 

Gestion des appareils est également foundation hello pour [accès conditionnel basés sur le périphérique](active-directory-conditional-access-policy-connected-applications.md). Avec un accès conditionnel basé sur un appareil, vous pouvez vous assurer qu’accès tooresources dans votre environnement est possible seulement avec les appareils de confiance.   

Cette rubrique explique comment fonctionne la gestion des appareils dans Azure Active Directory.

## <a name="getting-devices-under-hello-control-of-azure-ad"></a>Mise en route d’appareils sous contrôle de code hello d’Azure AD

tooget un appareil sous contrôle de code hello d’Azure AD, vous avez deux options :

- Inscription 
- Jonction

**L’enregistrement** un tooAzure appareil AD permet de vous toomanage les identités d’un appareil. Lorsqu’un appareil est inscrit, inscription des appareils Azure AD fournit appareil hello avec une identité qui est utilisé tooauthenticate hello périphérique lorsqu’un utilisateur se connecte en tooAzure AD. Vous pouvez utiliser hello identité tooenable ou désactiver un périphérique.

Lorsqu’il est associé à une solution de management(MDM) des appareils mobiles tels que Microsoft Intune, les attributs d’appareil hello dans Azure AD sont mises à jour des informations supplémentaires sur l’appareil de hello. Cela vous permet des règles d’accès conditionnel toocreate qui permettent d’accéder à partir d’appareils toomeet vos normes de conformité et de sécurité. Pour plus d’informations sur l’inscription d’appareils dans Microsoft Intune, consultez Inscrire des appareils pour la gestion dans Intune.

**Jointure** un appareil est une extension de tooregistering un appareil. Cela signifie que, il vous offre tous les avantages de hello de l’inscription d’un appareil et toothis de plus, il modifie également l’état local de hello d’un périphérique. La modification d’état local de hello permet à votre périphérique dans toosign tooa des utilisateurs à l’aide d’une organisation compte professionnel ou scolaire au lieu d’un compte personnel.

## <a name="azure-ad-registered-devices"></a>Appareils inscrits sur Azure AD   

Bonjour Azure AD inscrit les appareils vise tooprovide vous avec prise en charge pour hello **propre appareil BYOD (Bring Your)** scénario. Dans ce scénario, un utilisateur peut accéder aux ressources contrôlées Azure Active Directory de votre organisation à l’aide d’un appareil personnel.  

![Appareils inscrits sur Azure AD](./media/device-management-introduction/03.png)

accès de Hello est basé sur un compte professionnel ou scolaire qui a été saisi sur l’appareil de hello.  
Par exemple, Windows 10 permet aux utilisateurs tooadd un travail ou scolaire compte tooa ordinateur personnel, une tablette ou téléphone.  
Lorsqu’un utilisateur a ajouté un travail ou un compte scolaire, un périphérique de hello est inscrit auprès d’Azure AD et éventuellement inscrits dans le système de gestion des appareils mobiles hello que votre organisation a configuré. Les utilisateurs de votre organisation peuvent ajouter un travail ou scolaire appareil personnel de compte tooa pour des raisons pratiques :

- Lors de l’accès à une application de travail pour hello pour la première fois
- Manuellement via hello **paramètres** menu dans les cas de hello de Windows 10 

Vous pouvez configurer les appareils inscrits sur Azure AD pour Windows 10, iOS, Android et macOS.

## <a name="azure-ad-joined-devices"></a>Appareils joints Azure AD

Hello vise des périphériques d’Azure AD joint toosimplify :

- Les déploiements Windows des appareils professionnels 
- Accès aux applications tooorganizational et les ressources à partir de n’importe quel appareil Windows

![Appareils inscrits sur Azure AD](./media/device-management-introduction/02.png)


Ces objectifs sont effectuées en fournissant aux utilisateurs une expérience de libre-service pour l’obtention de travail des appareils sous contrôle de code hello d’Azure AD.  
**Azure AD Join** est destiné aux organisations axées en priorité ou uniquement sur le cloud. Ce sont généralement les petites et moyennes entreprises qui ne possèdent pas d’infrastructure Windows Server Active Directory en local. 

Implémentation des appareils Azure AD joint offre hello avantages suivants :

- **Single-Sign-On (SSO)** tooyour Azure managed services et applications SaaS. Vos utilisateurs ne voient pas les invites d’authentification supplémentaires lorsqu’ils accèdent aux ressources de travail. Hello fonctionnalité SSO est même lorsqu’ils ne sont pas connectés toohello réseau de domaine disponible.

- **L’itinérance compatible avec l’entreprise** des paramètres utilisateur sur les appareils joints. Les utilisateurs ne doivent tooconnect un paramètres toosee de compte (par exemple, Hotmail) Microsoft pour les appareils.

- **Accès tooWindows Store Pro** à l’aide du compte Active Directory. Les utilisateurs peuvent choisir à partir d’un inventaire des applications présélectionnée par l’organisation de hello.

- **Windows Hello** prise en charge pour les ressources toowork un accès sécurisé et pratique.

- **Restriction d’accès** tooapps à partir d’uniquement les périphériques qui répondent à la stratégie de conformité.

Bien qu’Azure AD Join soit principalement conçu pour les organisations qui ne disposent pas d’une infrastructure Windows Server Active Directory locale, vous pouvez également l’utiliser dans les scénarios où :

- Vous ne pouvez pas utiliser une jointure de domaine local, par exemple, si vous avez besoin de tooget des appareils mobiles tels que les tablettes et téléphones sous contrôle de code.

- Vos utilisateurs doivent principalement tooaccess Office 365 ou autres applications SaaS intégrées à Azure AD.

- Vous voulez toomanage un groupe d’utilisateurs dans Azure AD et non dans Active Directory. Par exemple, cela peut concerner tooseasonal employés, prestataires de service ou les étudiants.

- Vous souhaitez tooprovide jointure tooworkers de fonctionnalités dans les succursales distantes avec l’infrastructure locale limitée.

Vous pouvez configurer des appareils joints Azure AD pour les appareils Windows 10.


## <a name="hybrid-azure-ad-joined-devices"></a>Appareils joints Azure AD hybrides

Pour plus de dix ans, de nombreuses organisations utilisent hello domaine jointure tootheir locale Active Directory tooenable :

- INFORMATIQUE départements toomanage travail des appareils à partir d’un emplacement central.

- Toosign d’utilisateurs dans les appareils tootheir avec leur annuaire Active Directory de travail ou d’établissement scolaire. 

En règle générale, les organisations avec un encombrement local s’appuient sur les appareils tooprovision méthodes de création d’images, et qu’ils utilisent souvent **System Center Configuration Manager (SCCM)** ou **(GP) de la stratégie de groupe** toomanage les.

Si votre environnement comporte un site local encombrement d’Active Directory et que vous également tirent parti de fonctionnalités hello fournies par Azure Active Directory, vous pouvez implémenter hybrides Azure AD joint périphériques. Il s’agit des appareils qui sont à la fois, jointes tooyour locaux Active Directory et Azure Active Directory.

![Appareils inscrits sur Azure AD](./media/device-management-introduction/01.png)


Vous devez utiliser des appareils joints Azure AD hybrides si :

- Vous avez Win32 applications déployées toothese périphériques qui utilisent NTLM / Kerberos.

- Vous avez besoin de stratégie de groupe ou SCCM / appareils de toomanage DCM.

- Vous souhaitez que les appareils de la tooconfigure toocontinue toouse de solutions d’acquisition d’images pour vos employés.

Vous pouvez configurer des appareils joints Azure AD hybrides pour Windows 10 et des appareils de bas niveau comme Windows 8 et Windows 7.

## <a name="summary"></a>Résumé

La gestion des périphériques dans Azure AD vous permet de : 

- Simplifier les processus hello consistant à placer les appareils sous contrôle de code hello d’Azure AD

- Fournir à vos utilisateurs avec les ressources de cloud toouse facilement accès tooyour d’une organisation

En règle générale, vous devez utiliser :

- Les appareils inscrits sur Azure AD pour les appareils personnels

- Appareils joints à Azure AD pour les appareils qui ne sont pas joints à un tooan AD local 

- Appareils joints à hybrides Azure AD pour les appareils qui sont joints à un tooan AD local     




## <a name="next-steps"></a>Étapes suivantes

- tooget une vue d’ensemble de comment appareil toomanage dans hello Azure portail, consultez [la gestion des appareils à l’aide de hello portail Azure](device-management-azure-portal.md)

- toolearn en savoir plus sur l’accès conditionnel basé sur un appareil, consultez [configurer des stratégies d’accès conditionnel basés sur le périphérique Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).

- appareils de Azure AD joint toosetup hybride, consultez [comment tooconfigure hybride Azure Active Directory appareils joints à un](device-management-hybrid-azuread-joined-devices-setup.md).


