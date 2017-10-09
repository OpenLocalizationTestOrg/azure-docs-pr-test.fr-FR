---
title: "aaaHow tooget AppSource certifié pour Azure Active Directory | Documents Microsoft"
description: "Plus d’informations sur comment tooget votre application AppSource certifié pour Azure Active Directory."
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a>Comment tooget AppSource certifié pour Azure Active Directory
[Microsoft AppSource](https://appsource.microsoft.com/) est une destination pour l’entreprise aux utilisateurs toodiscover, essayez et gérer des applications de SaaS line-of-business (produits tooexisting Microsoft SaaS autonome SaaS et des modules complémentaires).

toolist une application SaaS sur AppSource autonome, votre application doit accepter l’authentification unique à partir des comptes d’une société ou d’une organisation qui dispose d’Azure Active Directory. processus de connexion Hello doit utiliser hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) ou [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocoles. L’intégration SAML n’est pas acceptée pour la certification AppSource.

## <a name="guides-and-code-samples"></a>Guides et exemples de code
Si vous souhaitez toolearn sur comment toointegrate connecter votre application avec Azure Active Directory à l’aide des ID d’ouverture, suivez nos guides et exemples Bonjour de code [guide du développeur Azure Active Directory](./active-directory-developers-guide.md#get-started "prise en main Azure AD pour les développeurs").

## <a name="multi-tenant-applications"></a>Applications multilocataires

Une application qui accepte les connexions des utilisateurs de toutes les entreprises ou organisations qui disposent d’Azure Active Directory sans qu’une instance, une configuration ou un déploiement distincts ne soient nécessaires est appelée une *application multilocataire*. AppSource recommande que les applications implémenter une architecture mutualisée tooenable hello *par simple clic* libérer l’expérience d’évaluation.

Dans l’ordre tooenable une architecture mutualisée sur votre application :
- Définissez `Multi-Tenanted` propriété trop`Yes` sur les informations d’inscription de votre application Bonjour [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (par défaut, les applications créées dans hello portail Azure sont configurées en tant que *àlocataireunique*)
- Mettre à jour votre toohello de demandes de code toosend '`common`« point de terminaison (mettre à jour le point de terminaison hello de *https://login.microsoftonline.com/ {yourtenant}* trop*https://login.microsoftonline.com/common*)
- Pour certaines plateformes, comme ASP.NET, vous devez également tooupdate tooaccept de votre code plusieurs émetteurs

Pour plus d’informations sur une architecture mutualisée, consultez : [comment toosign dans n’importe quel utilisateur Azure Active Directory (AD) à l’aide hello modèle d’application de l’architecture mutualisée](./active-directory-devhowto-multi-tenant-overview.md).

### <a name="single-tenant-applications"></a>Applications à locataire unique
Les applications qui acceptent uniquement les connexions des utilisateurs d’une instance Azure Active Directory définie sont appelées *applications à locataire unique*. Les utilisateurs externes (y compris les comptes d’entreprise ou école d’autres organisations ou compte personnel) peuvent se connecter dans l’application à locataire unique tooa après l’ajout de chaque utilisateur en tant que *compte invité* toohello Azure Active Directory de l’instance qui application Hello est inscrit. Vous pouvez ajouter des utilisateurs en tant qu’invité comptes tooan Azure Active Directory via hello [ *Azure AD B2B collaboration* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - et peut être effectuée [par programmation](../active-directory-b2b-code-samples.md). Lorsque vous ajoutez un utilisateur en tant qu’invité tooan de compte Azure Active Directory, un e-mail d’invitation est envoyé toohello utilisateur, d’invitation hello tooaccept en cliquant sur le lien hello dans l’e-mail d’invitation hello. Envoyé tooan des utilisateurs supplémentaires dans une organisation en invitant qui est également un membre de l’organisation partenaire de hello est non requis tooaccept un toosign invitation dans.

Les applications de locataire unique peuvent activer hello *Contact Me* expérience, mais si vous souhaitez tooenable hello par simple clic / libre expérience d’évaluation qui vous recommande de AppSource, activer une architecture mutualisée sur votre application à la place.


## <a name="appsource-trial-experiences"></a>Expérience d’essai gratuit AppSource

### <a name="free-trial-customer-led-trial-experience"></a>Essai gratuit (expérience d’essai gratuit menée par le client) 
Hello *orientée utilisateur la version d’évaluation* expérience hello AppSource recommandées car il offre une application de tooyour l’accès par simple clic. Vous trouverez ci-dessous une illustration de cette expérience :<br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li>Un utilisateur trouve votre application sur le site web AppSource.</li><li>Il sélectionne l’option « Essai gratuit ».</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li>AppSource redirige tooa d’utilisateur une URL de votre site web</li><li>Votre site web démarre hello <i>single-sign-on</i> processus automatiquement (sur le chargement de la page)</li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li>Utilisateur est redirigé tooMicrosoft connectez-vous page</li><li>L’utilisateur fournit un toosign des informations d’identification dans</li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li>L’utilisateur donne son consentement pour votre application.</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Ouverture de session se termine et l’utilisateur est redirigé tooyour arrière web site</li><li>Utilisateur démarre la version d’évaluation gratuite de hello</li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a>Me contacter (expérience d’essai gratuit menée par le partenaire)
Hello *expérience d’évaluation de partenaire* peut être utilisé lorsqu’un manuel ou une opération à long terme doit utilisateur de toohappen tooprovision hello / de l’entreprise : par exemple, votre application doit tooprovision des machines virtuelles, des instances de base de données, ou opérations qui prennent beaucoup toocomplete de temps. Dans ce cas, après l’utilisateur sélectionne hello *demande de version d’évaluation* bouton et remplit un formulaire, AppSource envoie hello de coordonnées de l’utilisateur. Lors de la réception de ces informations, puis configurer l’environnement de hello et envoyer à l’utilisateur de toohello hello des instructions sur la façon dont tooaccess hello expérience d’évaluation :<br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li>Un utilisateur trouve votre application sur le site web AppSource.</li><li>Il sélectionne l’option « Me contacter ».</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li>Il remplit un formulaire avec ses informations de contact.</li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td>Vous recevez les informations de l’utilisateur.</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td>Configurez l’environnement.</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td>Contactez l’utilisateur avec les informations relatives à l’essai gratuit.</td>
        </tr>
        </table><br/><br/>
        <ul><li>Vous recevez les informations de l’utilisateur et configurez l’instance d’essai gratuit.</li><li>Vous envoyez hello hyperlink tooaccess votre utilisateur toohello de l’application</li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li>Utilisateur accède à votre application et le complète hello single-sign-on processus</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li>L’utilisateur donne son consentement pour votre application.</li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Ouverture de session se termine et l’utilisateur est redirigé tooyour arrière web site</li><li>Utilisateur démarre la version d’évaluation gratuite de hello</li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a>Plus d’informations
Pour plus d’informations sur l’expérience d’évaluation de AppSource hello, consultez [cette vidéo](https://aka.ms/trialexperienceforwebapps). 
 
## <a name="next-steps"></a>Étapes suivantes

- Pour plus d’informations sur la création d’applications qui prennent en charge les connexions Azure Active Directory, consultez [Scénarios d’authentification pour Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios). 

- Pour plus d’informations sur comment toolist votre application SaaS dans AppSource, allez voir [AppSource informations sur le partenaire](https://appsource.microsoft.com/partners)


## <a name="get-support"></a>Obtenir de l’aide
Pour l’intégration d’Azure Active Directory, nous utilisons [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) avec prise en charge de hello Communauté tooprovide. 

Nous recommandons vivement de demander à vos questions sur la pile de dépassement de capacité et de parcourir toosee de problèmes existants si un utilisateur a demandé à votre question avant. Vérifiez que vos questions ou commentaires portent la mention `[azure-active-directory]`.

Utilisez hello suivant tooprovide des commentaires de la section commentaires et nous aider à affiner et mettre en forme notre contenu.

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->