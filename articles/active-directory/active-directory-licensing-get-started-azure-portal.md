---
title: "aaaGet a démarré avec le Gestionnaire de licences dans Azure Active Directory | Documents Microsoft"
description: "Comment Azure Active Directory fonctionne de la licence, comment tooget démarrer avec les meilleures pratiques"
services: active-directory
keywords: Gestion des licences Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 268dab806b8b959790341d630a0355c6a43871d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="license-yourself-and-your-users-in-azure-active-directory"></a>Accorder une licence à vos utilisateurs et à vous-même dans Azure Active Directory

> [!div class="op_single_selector"]
> * [Instructions pour le portail Azure](active-directory-licensing-get-started-azure-portal.md)
> * [Obtenir des informations sur le portail Azure Classic](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) est une plateforme et une solution Microsoft de type IDaaS (Identity as a Service). Azure AD est proposé en différentes éditions de service :

* Azure Active Directory Free, disponible avec n’importe quel service Microsoft tel qu’Office 365, Dynamics, Microsoft Intune ou Azure. Azure AD ne génère aucun frais de consommation dans ce mode.

* Éditions Azure AD payantes telles que :
  - Enterprise Mobility + Security 
  - Azure AD Premium (P1 et P2)
  - Azure AD Standard
  - Azure Multi-Factor Authentication

À l’instar de nombreux services en ligne Microsoft, la plupart des versions Azure AD payantes sont fournies par le biais de droits par utilisateur, comme dans Office 365, Microsoft Intune et Azure AD. Dans ces cas, fournisseur de service hello est représenté par un ou plusieurs abonnements, et chaque abonnement inclut certaines licences prepurchased dans votre client. Les droits par utilisateur sont obtenus des manières suivantes :

* Attribution d’une licence 
* Création d’un lien entre l’utilisateur de hello et produit de hello.
* L’activation de composants du service pour l’utilisateur de hello hello.
* Consommation d’un des hello prépayé licences.

[Essayez Azure AD Premium maintenant.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

Pour obtenir une présentation détaillée des fonctionnalités des services Azure AD, consultez [Qu’est-ce qu’Azure Active Directory ?](active-directory-whatis.md). Pour plus d’informations, consultez la page [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/).

> [!NOTE]
> Les abonnements de paiement à l’utilisation Azure permettent la création de ressources Azure et les mappent tooyour de paiement. Il n’existe aucun nombre de licences associés à hello abonnement. Lorsque vous accordez qu'une toooperate d’autorisation utilisateur sur les ressources Azure mappé toohello abonnement, ils sont associés hello abonnement et peuvent gérer les ressources de l’abonnement.

## <a name="how-does-azure-active-directory-licensing-work"></a>Comment la gestion des licences Azure Active Directory fonctionne-t-elle ?

Les services Azure AD basés sur des licences reposent sur l’activation d’un abonnement dans votre locataire de service Azure AD. Une fois l’abonnement de hello est actif, des fonctionnalités de service hello sont gérées par des administrateurs Azure AD et utilisées par les utilisateurs sous licence.

### <a name="manage-subscription-information"></a>Gérer les informations d’abonnement

Lorsque vous achetez Enterprise Mobility + Security, Azure AD Premium ou Azure AD Basic, votre client est mis à jour avec abonnement hello, y compris sa période de validité et prépayé des licences. Vos informations d’abonnement, y compris nombre hello de licences attribuées ou disponibles, soient disponibles via hello portail Azure : sous **Azure Active Directory**, ouvrez hello **licences** vignette hello répertoire spécifique. Hello **licences** lame est également hello meilleures place toomanage les affectations de licence.

Chaque abonnement se compose d’un ou plusieurs plans de service, tels qu’Azure AD, Multi-Factor Authentication, Intune, Exchange Online ou SharePoint Online.  La gestion des licences Azure AD ne nécessite *aucune* gestion au niveau des plans de service. Office 365 est différent, car il s’appuie sur cette configuration avancée mode toomanage access tooincluded services. Azure AD s’appuie sur les fonctionnalités de tooenable en service de configuration et gérer des autorisations individuelles.

> [!IMPORTANT]
> Azure AD Premium, Azure AD Basic et Enterprise Mobility + abonnements de sécurité sont tootheir confiné configuré/locataire d’annuaire. Abonnements ne peut pas être partagés entre les répertoires ou les utilisateurs tooentitle utilisés dans d’autres répertoires. Le déplacement d’un abonnement entre annuaires est possible, mais nécessite l’envoi d’un ticket de support ou une annulation et un rachat pour les achats directs.
>
> Lorsque Azure AD ou Enterprise Mobility + Security achetée auprès d’un abonnement de licence en Volume, et lors de l’accord de hello inclut d’autres services Microsoft Online services (par exemple, Office 365), l’activation se produit automatiquement. 

### <a name="assign-licenses"></a>Attribuer des licences

Bien qu’obtention d’un abonnement est tous les tooconfigure payé des fonctionnalités, vous devez toujours distribuer des licences pour Azure AD payé toousers de fonctionnalités. Tout utilisateur qui doit avoir tooor d’accès qui est gérée via une annonce Azure payé fonctionnalité doit avoir une licence. L’attribution de licence est un mappage entre un utilisateur et un service acheté, comme Azure AD Premium, Azure AD Basic ou Enterprise Mobility + Security.


La gestion des utilisateurs de votre annuaire qui doivent disposer d’une licence nécessite les étapes suivantes : 

* Attribution de licences toogroups Bonjour [portail Azure](active-directory-licensing-whatis-azure-portal.md).
* Attribution de licences directement toousers via le portail de hello, PowerShell ou des API. 

Lorsque vous affectez un groupe de licences tooa, tous les membres du groupe sont affectés à une licence. Si les utilisateurs sont ajoutés ou supprimés du groupe de hello, licence hello est affectée ou supprimé. L’affectation du groupe peut utiliser n’importe quel tooyou disponibles de gestion de groupe, et il est cohérent avec l’affectation basée sur le groupe tooapplications.

Vous pouvez utiliser [attribution de licence basée sur le groupe](active-directory-licensing-whatis-azure-portal.md) tooset des règles telles que les éléments suivants de hello :
* Tous les utilisateurs de votre annuaire obtiennent automatiquement une licence
* Toute personne avec le titre de travail approprié hello Obtient une licence
* Vous pouvez déléguer des gestionnaires de tooother hello décision dans l’organisation de hello (à l’aide de [groupes en libre-service](active-directory-accessmanagement-self-service-group-management.md))

Pour obtenir une présentation détaillée de toogroups d’attribution de licence, y compris avancé des scénarios et Office 365, les scénarios de gestion de licences voir [attribuer des licences toousers par l’appartenance au groupe dans Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="get-started-with-azure-ad-licensing"></a>Bien démarrer avec la gestion des licences Azure AD

La prise en main d’Azure AD est simple. Vous pouvez toujours créer votre annuaire dans le cadre de l’inscription à une [évaluation gratuite d’Azure](https://azure.microsoft.com/offers/ms-azr-0044p/).

Hello meilleures pratiques suivantes peuvent aider à vous assurer que votre client est aligné avec d’autres services Microsoft que vous pouvez consommer et à vos objectifs de service de hello :

- Si vous utilisez déjà un des services d’organisation de hello auprès de Microsoft, vous avez déjà un locataire Azure AD. Il est hello toouse utile que même locataire pour d’autres services afin que core gestion des identités, y compris l’approvisionnement et hybrides-session unique (SSO), peuvent être utilisées dans les services de hello. Avec l’authentification unique, vos utilisateurs bénéficient de fonctionnalités enrichies de hello entre les services hello. Par conséquent, si vous décidez de toobuy un service payée d’Azure AD pour votre personnel, nous recommandons d’utiliser des hello même locataire à nouveau.

- Nous vous recommandons d’utiliser un nouveau locataire Bonjour portail Azure si vous envisagez de :
  - D’utiliser Azure AD pour un ensemble d’utilisateurs différent (par exemple des partenaires ou des clients)
  - D’évaluer les services Azure AD de manière isolée par rapport à votre service de production
  - De configurer un environnement de bac à sable pour vos services

  Hello nouveau répertoire est créé avec votre compte en tant qu’un utilisateur externe avec des autorisations d’administrateur général. Lorsque vous vous connectez dans toohello portail Azure avec ce compte, vous pouvez voir ce locataire et accéder à toutes les tâches d’administration.

> [!NOTE]
> Azure AD prend en charge les « utilisateurs invités », qui sont des comptes d’utilisateur d’un locataire Azure AD qui ont été créés par le biais d’un compte Microsoft ou d’une identité Azure AD d’un autre locataire. portail d’administration Hello Office 365 ne prend pas en charge ces utilisateurs. Les utilisateurs invités avec les comptes Microsoft ne sont pas portail d’administration en mesure de tooaccess hello Office 365, tandis que les utilisateurs invités à partir d’autres clients Azure AD sont ignorés. Dans ce dernier cas de hello, uniquement hello compte local de l’utilisateur, Bonjour Azure AD ou client Office 365 où hello utilisateur a été initialement créé, est accessible.

### <a name="select-one-or-more-license-trials"></a>Sélectionner une ou plusieurs versions d’évaluation avec licences

Vous pouvez activer un abonnement d’évaluation à Azure AD Premium ou à Enterprise Mobility + Security sous **Azure Active Directory** &gt; **Démarrage rapide**.

![Sélectionner une licence d’évaluation](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

Licences d’évaluation sont disponibles sur hello **licences** panneau.

### <a name="assign-licenses-toousers-and-groups"></a>Assigner des groupes et des licences toousers

Une fois l’abonnement de hello est actif, vous devez attribuer un tooyourself de licence. Actualisez hello tooensure de navigateur que vous voyez toutes les fonctionnalités de hello. étape suivante de Hello est tooassign licences toohello utilisateurs qui doivent accéder aux fonctionnalités de Azure AD toopaid. Comme décrit dans [attribuer des licences](#assign-licenses), une méthode simple tooassign licences est groupe de hello tooidentify représentant hello souhaité audience et affecter hello licence tooit. De cette façon, les utilisateurs qui sont ajoutés ou supprimés du groupe de hello pendant son cycle de vie sont affectés ou supprimés à partir de la licence de hello, respectivement.

> [!NOTE]
> Certains services Microsoft ne sont pas disponibles dans tous les emplacements. Tooa utilisateur peut être affectée à une licence, administrateur de hello devez spécifier hello **l’emplacement d’utilisation** propriété pour l’utilisateur de hello. Vous pouvez définir cette propriété sous **utilisateur** &gt; **profil** &gt; **paramètres** Bonjour portail Azure. Lorsque vous utilisez l’affectation du groupe de licences, emplacement hello du répertoire de hello hérite de n’importe quel utilisateur dont l’emplacement d’utilisation n’est pas spécifié.

tooassign une licence, sous **Azure Active Directory** &gt; **licences** &gt; **tous les produits**, sélectionnez un ou plusieurs produits, puis **Affecter** sur la barre de commandes hello.

![Sélectionnez un tooassign de licence](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

Vous pouvez utiliser hello **utilisateurs et groupes** toochoose panneau plusieurs utilisateurs ou groupes ou toodisable service plans dans le produit de hello. Utiliser zone de recherche hello toosearch supérieur pour les noms d’utilisateur et de groupe.

![Sélectionner un utilisateur ou un groupe pour l’attribution de licences](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

Lorsque vous affectez un groupe de tooa de licences, il peut prendre un certain temps avant que tous les utilisateurs héritent licence hello, en fonction du nombre de hello d’utilisateurs dans le groupe de hello. Vous pouvez vérifier le statut de traitement hello sur hello **groupe** panneau, sous hello **licences** vignette.

![Statut d’affectation de licence](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

Des erreurs d’affectation peuvent se produire lors de l’affectation des licences Azure AD, mais elles restent relativement rares lors de la gestion des produits Azure AD et Enterprise Mobility + Security. Les erreurs d’attribution se limitent aux problèmes suivants :
- Conflits d’attribution : quand un utilisateur a été affecté précédemment une licence qui n’est pas compatible avec licence en cours de hello. Dans ce cas, l’attribution de licence de nouveau hello requiert hello en cours de suppression.
- Dépassement de licences disponibles : lorsque nombre hello d’utilisateurs dans les groupes assignés dépasse les licences disponibles hello, état d’attribution d’un utilisateur reflète un tooassign échec en raison de toomissing licences.

#### <a name="azure-ad-b2b-collaboration-licensing"></a>Affectation de licences Azure Active Directory B2B Collaboration

B2B collaboration vous permet des utilisateurs invités de tooinvite à vos services de Azure AD client tooprovide accès tooAzure AD et les ressources Azure vous rendre disponible.  

Il n’existe aucun frais pour inviter les utilisateurs B2B et de les affecter l’application tooan dans Azure AD. Les applications too10 par invité utilisateur et des rapports de base 3 sont également gratuits pour les utilisateurs de collaboration B2B. Si votre utilisateur invité a aucune licence appropriée dans le locataire d’Azure AD du partenaire hello, ils allez disposer d’une licence dans le vôtre également.

Il n’est pas obligatoire, mais si vous souhaitez que les fonctionnalités de tooprovide accès toopaid Azure AD, les utilisateurs invités de B2B doivent disposer d’une licence avec des licences de Azure AD d’appropriées. Un locataire invitant à une annonce Azure payé licence permettre affecter des droits d’utilisateur B2B collaboration les utilisateurs d’invité tooan cinq supplémentaires invités toohello client. Pour plus d’informations et pour voir des scénarios, consultez le [Guide d’attribution de licences pour Azure Active Directory B2B Collaboration](active-directory-b2b-licensing.md).

### <a name="view-assigned-licenses"></a>Visualiser les licences attribuées

Un récapitulatif des licences attribuées et disponibles est disponible sous **Azure Active Directory** &gt; **Licences** &gt; **Tous les produits**.

![Afficher le récapitulatif des licences](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

Une liste détaillée des utilisateurs et groupes attribués est disponible quand vous sélectionnez un produit spécifique. Hello **utilisateurs sous licence** liste affiche tous les utilisateurs actuellement consomme une licence et que la licence de hello a été assignée directement toohello utilisateur ou si elle est héritée d’un groupe.

![Afficher le détail des licences](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

De même, hello **concédé sous licence de groupes** liste affiche tous les groupes de licences de toowhich ont été affectés. Sélectionnez un Bonjour tooopen utilisateur ou un groupe **licences** panneau, qui montre toutes les licences affectées toothat objet.

### <a name="remove-a-license"></a>Supprimer une licence

tooremove une licence, accédez toohello utilisateur ou un groupe et ouvrez hello **licences** vignette. Sélectionnez hello licence, puis cliquez sur **supprimer**.

![Supprimer une licence](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

Héritée par utilisateur hello à partir d’un groupe de licences ne peut pas être supprimées directement. Au lieu de cela, supprimez-le hello groupe hello à partir duquel ils héritent des licences de hello.

### <a name="extend-trials"></a>Prolonger des évaluations

Les extensions d’évaluation pour les clients sont disponibles en tant que libre service d’inscription via le portail de hello Office 365. Un administrateur client peut accéder portail Office de toohello (accès dépend des autorisations pour le portail Office de hello) et sélectionnez la version d’évaluation de hello Azure AD Premium. En cliquant sur hello **étendre évaluation** lien démarre le processus d’extension hello. Une carte de crédit est nécessaire, mais elle n’est pas débitée.

![Étendre une version d’évaluation Bonjour portail Azure](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur des scénarios avancés de gestion des licences via les groupes, consultez l’article de la hello [groupe d’affectation licences tooa](active-directory-licensing-group-assignment-azure-portal.md).

Voici des informations sur la façon tooconfigure et utiliser d’autres payée des fonctionnalités d’Azure AD :

* [Réinitialisation de mot de passe en libre service](active-directory-manage-passwords.md)
* [Gestion des groupes en libre service](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Achat direct de licences Azure AD Premium](http://aka.ms/buyaadp)
