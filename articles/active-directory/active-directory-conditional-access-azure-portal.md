---
title: "aaaAzure Active Directory un accès conditionnel | Documents Microsoft"
description: "Utilisez le contrôle d’accès conditionnel dans Azure Active Directory toocheck pour des conditions spécifiques lors de l’authentification pour accès tooapplications."
services: active-directory
keywords: "tooapps d’accès conditionnel, l’accès conditionnel avec Azure AD, sécuriser l’accès aux ressources toocompany, les stratégies d’accès conditionnel"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 9fa8a5c3e514c032fbe3aa56f33d759485a018c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-azure-active-directory"></a>Accès conditionnel dans Azure Active Directory

Dans un monde mobile en premier, privilégie le cloud, Azure Active Directory permet toodevices de l’authentification unique, les applications et services à partir de n’importe quel endroit. Avec la prolifération de hello des appareils (y compris BYOD), travaillent sur des réseaux d’entreprise et 3ème partie SaaS applications, les professionnels de l’informatique sont confrontées à deux objectifs différents :

- Permettre aux toobe des utilisateurs finaux hello productif où et quand
- Protéger les ressources d’entreprise de hello à tout moment

tooimprove productivité, Azure Active Directory fournit à vos utilisateurs avec un large éventail d’options tooaccess vos ressources d’entreprise. Gestion des accès aux applications Azure Active Directory vous permet de tooensure que seul *hello bonnes personnes* peuvent accéder à vos applications. Que se passe-t-il si vous voulez toohave plus contrôler comment les personnes appropriées hello accédez à vos ressources sous certaines conditions ? Que se passe-t-il si vous avez même conditions sous lequel vous voulez tooblock accès toocertain applications même pour hello *avec le bouton droit personnes*? Par exemple, il peut être OK pour vous si aux personnes hello accédez à certaines applications à partir d’un réseau approuvé ; Toutefois, vous pouvez les tooaccess ces applications à partir d’un réseau, que vous ne faites pas confiance. L’accès conditionnel apporte une réponse à ces questions.

Accès conditionnel est une fonctionnalité d’Azure Active Directory qui vous permet de contrôles tooenforce tooapps d’accès hello dans votre environnement en fonction des conditions spécifiques. Avec des contrôles, vous pouvez lier l’accès de toohello des exigences supplémentaires ou vous pouvez la bloquer. implémentation de Hello de l’accès conditionnel est basée sur des stratégies. Une approche basée sur des stratégies simplifie votre expérience de configuration, car il suit moyen hello que vous réfléchissez à vos exigences d’accès.  

En règle générale, vous définissez vos exigences d’accès à l’aide des instructions qui sont basées sur hello modèle :

![Contrôle](./media/active-directory-conditional-access-azure-portal/10.png)

Lorsque vous remplacez les deux occurrences de hello de «*cela*» avec les informations du monde réel, vous avez un exemple pour une instruction de stratégie qui semble tooyou familier :

*Lors du prestataires de service sont tooaccess nos applications de cloud à partir de réseaux qui ne sont pas approuvés, puis bloquer l’accès.*

instruction de stratégie Hello ci-dessus met en surbrillance power hello d’accès conditionnel. Pendant que vous pouvez activer sous-traitants toobasically accéder à vos applications cloud (**qui**), avec un accès conditionnel, vous pouvez également définir des conditions dans le hello accès est possible (**comment**).

Dans le contexte de hello d’accès conditionnel Azure Active Directory

- « **When this happens** » est une **instruction de condition**
- « **Then do this** » est un **contrôle**

![Contrôle](./media/active-directory-conditional-access-azure-portal/11.png)

combinaison de Hello d’une instruction de condition avec vos contrôles représente une stratégie d’accès conditionnel.

![Contrôle](./media/active-directory-conditional-access-azure-portal/12.png)


## <a name="controls"></a>Commandes

Dans une stratégie d’accès conditionnel, les contrôles définissent l’action à effectuer lorsqu’une instruction de condition est remplie.  
Grâce aux contrôles, vous pouvez bloquer ou autoriser l’accès avec des exigences supplémentaires.
Lorsque vous configurez une stratégie qui autorise l’accès, vous devez tooselect au moins une exigence.   

### <a name="grant-controls"></a>Contrôles d’octroi
mise en œuvre actuelle Hello d’Azure Active Directory vous permet de hello tooconfigure suivant les exigences de contrôle d’allocation :

![Contrôle](./media/active-directory-conditional-access-azure-portal/05.png)

- **Multi-factor Authentication** - Grâce à l’authentification multifacteur, vous pouvez appliquer une authentification renforcée. En tant que fournisseur, vous pouvez combiner Azure Multi-Factor Authentication ou une authentification multifacteur locale, avec AD FS (Active Directory Federation Services). À l’aide de l’authentification multifacteur permet de protéger des ressources soit accessible par un utilisateur non autorisé peut avoir accédé toohello les informations d’identification d’un utilisateur valide.

- **Périphérique compatible** -vous pouvez définir des stratégies d’accès conditionnel au niveau du périphérique hello. Vous pouvez configurer une stratégie tooonly activer les ordinateurs qui sont conformes ou les périphériques mobiles qui sont inscrits dans un tooaccess de gestion des appareils mobiles, les ressources de votre organisation. Par exemple, vous pourrez utiliser la conformité des appareils Intune toocheck et puis signaler tooAzure AD pour l’application lors de l’utilisateur de hello tente tooaccess une application. Pour obtenir des instructions détaillées sur comment les applications tooprotect toouse Intune et les données, consultez [protéger les données avec Microsoft Intune et les applications](https://docs.microsoft.com/intune-classic/deploy-use/protect-apps-and-data-with-microsoft-intune). Vous pouvez également utiliser protection des données tooenforce Intune pour les appareils perdus ou volés. Pour plus d’informations, consultez [Protection de vos données avec effacement complet ou sélectif à l’aide de Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

- **APPAREIL joint à un domaine** – vous pouvez exiger hello appareils vous avez utilisé tooconnect tooAzure Active Directory toobe appartenant au domaine tooyour locale Active Directory (AD). Cette stratégie s’applique tooWindows bureaux, ordinateurs portables et tablettes de l’entreprise. 

Si vous avez sélectionné plusieurs contrôles, vous pouvez également indiquer si tous ces contrôles sont requis lors du traitement de votre stratégie.

![Contrôle](./media/active-directory-conditional-access-azure-portal/06.png)

### <a name="session-controls"></a>Contrôles de session
Les contrôles de session permettent de limiter l’expérience dans une application cloud. contrôles de session Hello sont appliquées par les applications cloud et s’appuient sur des informations supplémentaires fournies par l’application de toohello Azure AD sur la session de hello.

![Contrôle](./media/active-directory-conditional-access-azure-portal/session-control-pic.png)

#### <a name="use-app-enforced-restrictions"></a>Utiliser les restrictions appliquées par l’application
Vous pouvez utiliser cette application contrôle toorequire Azure AD toopass hello appareil informations toohello cloud. Cela permet de savoir si l’utilisateur de hello provient d’un périphérique conforme ou joint à un domaine hello cloud application. Ce contrôle n’est actuellement prise en charge uniquement avec SharePoint en tant qu’application de cloud hello. SharePoint utilise hello appareil informations tooprovide que les utilisateurs une expérience limitée ou complète en fonction de l’état de l’appareil hello.
toolearn en savoir plus sur comment toorequire limitée à l’accès à SharePoint, accédez [ici](https://aka.ms/spolimitedaccessdocs).

## <a name="condition-statement"></a>Instruction de condition

section précédente de Hello vous a présenté toosupported options tooblock ou restreindre l’accès des ressources de tooyour sous forme de contrôles. Dans une stratégie d’accès conditionnel, vous définissez les critères de hello nécessitant toobe remplie pour votre toobe contrôles appliqué sous forme d’une instruction de condition.  

Vous pouvez inclure hello suivant affectations dans votre instruction de condition :

![Contrôle](./media/active-directory-conditional-access-azure-portal/07.png)


- **Qui** -dans de nombreux cas, vous souhaitez que vos contrôles toobe appliqué tooa groupe d’utilisateurs spécifique. Dans une instruction de condition, vous pouvez définir cet ensemble en sélectionnant des utilisateurs de hello et groupes d’à que votre stratégie s’applique. Au besoin, vous pouvez également exclure explicitement un ensemble d’utilisateurs de votre stratégie en les exemptant.  
En sélectionnant des utilisateurs et des groupes, vous définissez étendue hello de votre stratégie s’applique à des utilisateurs.    

    ![Contrôle](./media/active-directory-conditional-access-azure-portal/08.png)



- **Quoi** - En général, certaines applications qui s’exécutent dans votre environnement requièrent une protection supérieure à d’autres. Cela affecte, par exemple, les applications qui ont accès aux données de toosensitive.
En sélectionnant les applications cloud, vous définissez étendue hello des applications cloud que votre stratégie s’applique. Au besoin, vous pouvez également exclure explicitement un ensemble d’applications de votre stratégie.

    ![Contrôle](./media/active-directory-conditional-access-azure-portal/09.png)


- **Comment** - tant que les applications d’accès tooyour est effectuée dans des conditions que vous pouvez contrôler, il n’y a peut n’être aucun nécessaire pour imposer des contrôles supplémentaires sur comment vos applications cloud sont accessibles par vos utilisateurs. Toutefois, aspect peut différer si les applications cloud accès tooyour est effectuée, par exemple, à partir des réseaux non approuvés ou des appareils qui ne sont pas conformes. Dans une instruction de condition, vous pouvez définir certaines conditions d’accès qui ont des exigences supplémentaires pour le mode d’accès tooyour applications.

    ![Conditions](./media/active-directory-conditional-access-azure-portal/21.png)


## <a name="conditions"></a>Conditions

Dans l’implémentation actuelle de hello d’Azure Active Directory, vous pouvez définir des conditions pour hello suivant de zones :

- Risque à la connexion
- Plateformes d’appareils
- Emplacements
- Applications clientes

![Conditions](./media/active-directory-conditional-access-azure-portal/21.png)

### <a name="sign-in-risk"></a>Risque à la connexion

Un risque pour la connexion est un objet qui est utilisé par la probabilité de hello tootrack Azure Active Directory qu’une tentative de connexion n’a pas été effectuée par le propriétaire légitime de hello d’un compte d’utilisateur. Dans cet objet, probabilité hello (haute, moyenne ou faible) est stockée sous forme d’un attribut appelé [niveau de risque de connexion](active-directory-reporting-risk-events.md#risk-level). Cet objet est généré lors de la connexion d’un utilisateur si des risques de connexion ont été détectés par Azure Active Directory. Pour en savoir plus, voir [Connexions risquées](active-directory-identityprotection.md#risky-sign-ins).  
Vous pouvez utiliser le niveau de connexion risque de hello calculée comme condition dans une stratégie d’accès conditionnel. 

![Conditions](./media/active-directory-conditional-access-azure-portal/22.png)

### <a name="device-platforms"></a>Plateformes d’appareils

plateforme d’appareil Hello est caractérisée par le système d’exploitation hello qui s’exécute sur votre appareil :

- Android
- iOS
- Windows Phone
- Windows
- Mac OS (préversion). 

![Conditions](./media/active-directory-conditional-access-azure-portal/02.png)

Vous pouvez définir des plateformes d’appareils hello qui sont inclus, ainsi que les plateformes d’appareils qui sont exclus d’une stratégie.  
plateformes d’appareils toouse dans la stratégie de hello, première modification hello bascules configurer trop**Oui**, puis sélectionnez tous ou périphérique plateformes hello stratégie s’applique à. Si vous sélectionnez les plateformes d’appareils individuels, stratégie de hello a uniquement un impact sur ces plateformes. Dans ce cas, les plateformes de tooother pris en charge les connexions ne sont pas affectées par la stratégie de hello.


### <a name="locations"></a>Emplacements

Hello emplacement est identifié par son adresse IP du client de hello hello, vous avez utilisé tooconnect tooAzure Active Directory. Cette condition requiert que vous toobe familière **emplacements nommés** et **MFA d’adresses IP approuvées**.  

**Emplacements nommés** est une fonctionnalité d’Azure Active Directory qui vous permet de plages d’adresses IP toolabel approuvé dans votre organisation. Dans votre environnement, vous pouvez utiliser les emplacements nommés dans le contexte de hello de détection hello de [risque d’événements](active-directory-reporting-risk-events.md) , ainsi que l’accès conditionnel. Pour plus d’informations sur la configuration des emplacements nommés dans Azure Active Directory, consultez [Emplacements nommés dans Azure Active Directory](active-directory-named-locations.md).

nombre de Hello des emplacements, que vous pouvez configurer est limité en taille hello d’objets connexes de hello dans Azure AD. Vous pouvez configurer les éléments suivants :
 
 - Un emplacement nommé avec des plages d’adresses IP too500
 - Un maximum de 60 sites (aperçu) nommés avec une plage d’adresses IP affectées tooeach d'entre eux 


**L’authentification Multifacteur d’adresses IP approuvées** est une fonctionnalité de l’authentification multifacteur qui vous permet de plages d’adresses IP toodefine approuvé représentant intranet local de votre organisation. Lorsque vous configurez des conditions d’un emplacement, des adresses IP approuvées vous permet de toodistinguish entre les connexions effectuées à partir de réseau de votre organisation et tous les autres emplacements. Pour plus d’informations, consultez [Adresses IP approuvées](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).  



Vous pouvez soit inclure tous les emplacements ou toutes les adresses IP approuvées, soit exclure toutes les adresses IP approuvées.

![Conditions](./media/active-directory-conditional-access-azure-portal/03.png)


### <a name="client-app"></a>Application cliente

application cliente de Hello peut être sur une application hello niveau générique (navigateur web, application mobile, client de bureau) vous avez utilisé tooconnect tooAzure Active Directory ou vous pouvez sélectionner spécifiquement Exchange Active Sync.  
Authentification hérité fait référence à tooclients à l’aide de l’authentification de base telles que les clients Office plus anciens qui n’utilisent pas l’authentification moderne. Pour l’instant, l’accès conditionnel ne fonctionne pas avec l’authentification héritée.

![Conditions](./media/active-directory-conditional-access-azure-portal/04.png)


## <a name="common-scenarios"></a>Scénarios courants

### <a name="requiring-multi-factor-authentication-for-apps"></a>Exiger l’authentification multifacteur pour les applications

De nombreux environnements disposent d’applications nécessitant un niveau de protection supérieur hello d’autres.
C’est, par exemple, les cas de hello pour les applications qui ont accès aux données de toosensitive.
Si vous souhaitez tooadd une autre couche de protection toothese applications, vous pouvez configurer une stratégie d’accès conditionnel qui requiert l’authentification multifacteur lorsque les utilisateurs accèdent à ces applications.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Exiger l’authentification multifacteur pour l’accès à partir de réseaux non approuvés

Ce scénario est le scénario précédent de toohello similaire, car elle ajoute la configuration requise pour l’authentification multifacteur.
Toutefois, hello principale différence est condition hello pour cette spécification.  
Lors de focus hello du scénario précédent de hello est sur les applications avec des données access toosensitve, hello ce scénario se concentre sur des emplacements approuvés.  
En d’autres termes, l’authentification multifacteur peut être requise si un utilisateur accède à une application à partir d’un réseau que vous n’avez pas approuvé.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Seuls les appareils approuvés ont accès aux services Office 365

Si vous utilisez Intune dans votre environnement, vous pouvez commencer immédiatement à l’aide d’interface de stratégie d’accès conditionnel hello Bonjour console Azure.

De nombreux clients Intune utilisent tooensure d’accès conditionnel qu’uniquement les appareils de confiance peuvent accéder aux services Office 365. Cela signifie que les appareils mobiles sont inscrits avec Intune et répondre aux exigences de stratégie de conformité, et que les PC Windows appartiennent à un domaine local de tooan jointes. Une amélioration importante est que vous n’avez pas tooset hello même stratégie pour chacun des services de hello Office 365.  Lorsque vous créez une nouvelle stratégie, configurez hello Cloud applications tooinclude chaque des applications hello O365 que vous souhaitez tooprotect avec l’accès conditionnel.

## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez tooknow tooconfigure une stratégie d’accès conditionnel, voir [prise en main avec un accès conditionnel dans Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

Si vous êtes prêt tooconfigure des stratégies d’accès conditionnel pour votre environnement, consultez hello [meilleures pratiques pour l’accès conditionnel dans Azure Active Directory](active-directory-conditional-access-best-practices.md). 
