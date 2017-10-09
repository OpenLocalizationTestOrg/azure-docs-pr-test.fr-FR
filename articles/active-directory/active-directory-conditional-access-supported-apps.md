---
title: "aaaApplications et navigateurs qui utilisent des règles d’accès conditionnel dans Azure Active Directory | Documents Microsoft"
description: "Avec le contrôle d’accès conditionnel, Azure Active Directory vérifie pour des conditions spécifiques lors de l’authentification utilisateur de hello et tooallow accès à l’application."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 62349fba-3cc0-4ab5-babe-372b3389eff6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ca20853bb9f4b22d0b88ddd2f051d658e0d88cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="applications-and-browsers-that-use-conditional-access-rules-in-azure-active-directory"></a>Applications et navigateurs qui utilisent des règles d’accès conditionnel dans Azure Active Directory

Les règles d’accès conditionnel sont prises en charge dans les applications connectées à Azure Active Directory (Azure AD), les applications SaaS fédérées préintégrées, les applications qui utilisent l’authentification unique par mot de passe, les applications métier et les applications qui utilisent le proxy d’application Azure AD. Pour obtenir la liste détaillée des applications dans lesquelles vous pouvez utiliser l’accès conditionnel, consultez [Services activés avec accès conditionnel](active-directory-conditional-access-technical-reference.md). L’accès conditionnel fonctionne avec les applications mobiles et de bureau qui utilisent l’authentification moderne. Dans cet article, nous abordons le fonctionnement de l’accès conditionnel dans les applications mobiles et de bureau.

Vous pouvez utiliser les pages de connexion Azure AD dans les applications qui emploient l’authentification moderne. Avec une page de connexion, un utilisateur est invité à utiliser l’authentification multifacteur. Un message s’affiche si l’accès de l’utilisateur hello est bloquée. L’authentification moderne est requise pour tooauthenticate de périphérique hello avec Azure AD, afin que l’évaluation des stratégies d’accès conditionnel basés sur l’appareil.

Il est important tooknow les applications peuvent utiliser des règles d’accès conditionnel et hello étapes que vous devrez peut-être tootake toosecure autres points d’entrée application.

## <a name="applications-that-use-modern-authentication"></a>Applications qui utilisent l’authentification moderne
> [!NOTE]
> Si vous avez une stratégie d’accès conditionnel dans Azure AD qui a un équivalent dans Office 365, configurez les deux stratégies d’accès conditionnel. Cette situation concerne, par exemple, les stratégies d’accès tooconditional pour Exchange Online ou SharePoint Online.
>
>

Hello applications suivantes prennent en charge l’accès conditionnel pour Office 365 et d’autres applications de service de connexion AD Azure :


| Service cible| Plateforme| Application |
| --- | --- | --- |
| Tout service d’application Mes applications| Android et iOS| Stratégie MFA et d’emplacement pour les applications. Les stratégies basées sur les appareils ne sont pas prises en charge.|
| Service Application distante Azure| Windows 10, Windows 8.1, Windows 7, iOS, Android et MAC OS X| Application distante Azure|
| Dynamics CRM| Windows 10, Windows 8.1, Windows 7, iOS, Android| Application Dynamics CRM|
| Microsoft Teams| Windows 10, Windows 8.1, Windows 7, iOS, Android et MAC OS X| Services Microsoft Teams, soit tous les services qui prennent en charge Microsoft Teams et toutes ses applications clientes : Bureau Windows, MAC OS X, iOS, Android, WP et client web|
| Office 365 Exchange Online| Windows 10| Messagerie/Calendrier/Contacts, Outlook 2016, Outlook 2013 (avec authentification moderne), Skype Entreprise (avec authentification moderne)|
| Office 365 Exchange Online| Windows 8.1, Windows 7| Outlook 2016, Outlook 2013 (avec authentification moderne), Skype Entreprise (avec authentification moderne)|
| Office 365 Exchange Online| iOS| Application Outlook Mobile|
| Office 365 Exchange Online| Mac OS X| Outlook 2016 (Office pour Mac OS)|
| Office 365 SharePoint Online| Windows 10| Les applications Office 2016, les applications Office universel, Office 2013 (avec l’authentification moderne), client de synchronisation OneDrive (consultez [notes](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)), la prise en charge les groupes Office hello futures prévue, prise en charge des applications SharePoint vont hello future|
| Office 365 SharePoint Online| Windows 8.1, Windows 7| Applications Office 2016, Office 2013 (avec authentification moderne), client de synchronisation OneDrive (voir [notes](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))|
| Office 365 SharePoint Online| iOS, Android| Applications mobiles Office|
| Office 365 SharePoint Online| Mac OS X| Office 2016 pour Mac OS (Word, Excel, PowerPoint, OneNote uniquement). OneDrive pour la prise en charge de l’entreprise vont hello future|
| Office 365 Yammer| Windows 10, iOS, Android| Application Yammer Office|
| Service PowerBI| Windows 10, Windows 8.1, Windows 7 et iOS| Application PowerBI. application de Power BI Hello pour Android ne prend pas en charge l’accès conditionnel basé sur l’appareil.|
| Visual Studio Team Services| Windows 10, Windows 8.1, Windows 7, iOS, Android| Application Visual Studio Team Services|








## <a name="applications-that-do-not-use-modern-authentication"></a>Applications qui n’utilisent pas l’authentification moderne
Actuellement, vous devez utiliser les autres tooapps d’accès tooblock méthodes qui n’utilisent pas l’authentification moderne. Les règles d’accès pour les applications qui n’utilisent pas l’authentification moderne ne sont pas appliquées par l’accès conditionnel. Cela concerne principalement l’accès Exchange et SharePoint. La plupart des versions antérieures des applications utilisent d’anciens protocoles de contrôle d’accès.

### <a name="control-access-in-office-365-sharepoint-online"></a>Contrôle d’accès dans Office 365 SharePoint Online
Vous pouvez désactiver des protocoles hérités pour l’accès SharePoint à l’aide d’applet de commande hello SPOTenant de jeu. Utilisez cette applet de commande tooprevent des clients Office qui utilisent des protocoles de l’authentification moderne non d’accéder aux ressources SharePoint Online.

**Exemple de commande** :`Set-SPOTenant -LegacyAuthProtocolsEnabled $false`

### <a name="control-access-in-office-365-exchange-online"></a>Contrôle d’accès dans Office 365 Exchange Online
Exchange propose deux catégories principales de protocoles. Passez en revue les options suivantes de hello, puis sélectionnez Stratégie hello qui convient à votre organisation.

* **Exchange ActiveSync**. Par défaut, les stratégies d’accès conditionnel pour l’authentification multifacteur et d’emplacement ne sont pas appliquées pour Exchange ActiveSync. Vous devez tooprotect, accéder aux services toothese en configurant la stratégie Exchange ActiveSync directement ou en bloquant Exchange ActiveSync à l’aide de règles de Services de fédération Active Directory (AD FS).
* **Protocoles hérités**. Vous pouvez bloquer les protocoles hérités avec AD FS. Cela empêche les clients Office tooolder accès, telles qu’Office 2013 sans l’authentification moderne activée et les versions antérieures de Microsoft Office.

### <a name="use-ad-fs-tooblock-legacy-protocol"></a>Utiliser protocole hérité de tooblock AD FS
Vous pouvez utiliser hello suivant l’exemple d’émission règles tooblock hérités de protocole d’accès d’autorisation au niveau de hello AD FS. Choisissez parmi deux configurations courantes.

#### <a name="option-1-allow-exchange-activesync-and-allow-legacy-apps-but-only-on-hello-intranet"></a>Option 1 : Permettre à Exchange ActiveSync et autoriser des applications héritées, mais uniquement sur l’intranet de hello
En appliquant hello suivant trois règles toohello AD FS confiance approbation pour la plateforme d’identité Microsoft Office 365, le trafic Exchange ActiveSync, et navigateur et le trafic d’authentification moderne, avoir accès. Les applications héritées sont bloquées hello extranet.

##### <a name="rule-1"></a>Règle 1
    @RuleName = "Allow all intranet traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-2"></a>Règle 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-3"></a>Règle 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

#### <a name="option-2-allow-exchange-activesync-and-block-legacy-apps"></a>Option 2 : autoriser Exchange ActiveSync et bloquer les applications héritées
En appliquant hello suivant trois règles toohello AD FS confiance approbation pour la plateforme d’identité Microsoft Office 365, le trafic Exchange ActiveSync, et navigateur et le trafic d’authentification moderne, avoir accès. Les applications héritées ne pourront accéder à aucun emplacement.

##### <a name="rule-1"></a>Règle 1
    @RuleName = "Allow all intranet traffic only for browser and modern authentication clients"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-2"></a>Règle 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-3"></a>Règle 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


## <a name="supported-browsers-for-device-based-policies"></a>Navigateurs pris en charge pour les stratégies basées sur les appareils 

Vous pouvez uniquement accéder pour vérifier les stratégies basées sur les appareils pour la conformité de l’appareil et la jonction de domaine lorsque Azure AD peut identifier et authentifier les appareils hello. Lors de la plupart des contrôles, tels que l’emplacement et le travail de l’authentification Multifacteur sur la plupart des appareils et navigateurs, les stratégies de périphérique exigent de version de hello du système d’exploitation et les navigateurs répertoriés ci-dessous. L’accès est bloqué pour les utilisateurs sur les navigateurs non pris en charge ou des systèmes d’exploitation de hello quand une stratégie de périphérique est en place. 

| SE                     | Navigateurs                 | Support     |
| :--                    | :--                      | :-:         |
| Win 10                 | IE, Edge                 | ![Vérification][1] |
| Win 10                 | Chrome                   | VERSION PRÉLIMINAIRE     |
| Win 8/8.1            | IE, Chrome               | ![Vérification][1] |
| Win 7                  | IE, Chrome               | ![Vérification][1] |
| iOS                    | Safari                   | ![Vérification][1] |
| Android                | Chrome                   | ![Vérification][1] |
| Windows Phone          | IE, Edge                 | ![Vérification][1] |
| Windows Server 2016    | IE, Edge                 | ![Vérification][1] |
| Windows Server 2016    | Chrome                   | Bientôt disponible |
| Windows Server 2012 R2 | IE, Chrome               | ![Vérification][1] |
| Windows Server 2008 R2 | IE, Chrome               | ![Vérification][1] |
| Mac OS                 | Safari                   | ![Vérification][1] |
| Mac OS                 | Chrome                   | Bientôt disponible |

> [!NOTE]
> Pour la prise en charge de Chrome, vous devez utiliser la mise à jour de Windows 10 créateurs et installer une extension hello trouvé [ici](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji).
>
>

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations, consultez [Accès conditionnel dans Azure Active Directory](active-directory-conditional-access.md)




<!--Image references-->
[1]: ./media/active-directory-conditional-access-supported-apps/ic195031.png


