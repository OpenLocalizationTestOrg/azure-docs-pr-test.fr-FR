---
title: "utilisateurs d’Azure Active Directory aaaLicense Bonjour portail classique Azure | Documents Microsoft"
description: "Description du contrat de licence Microsoft Azure Active Directory, comment il fonctionne, comment tooget démarrer et meilleures pratiques, y compris Office 365, Microsoft Intune, Azure Active Directory Premium et les éditions de base"
services: active-directory
keywords: Gestion des licences Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d769e8c6-7581-43f5-a3b4-de4b1dca2344
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;H1Hack27Feb2017
ms.openlocfilehash: 4d5f244cbee2ae37a30976f70b5d4f21c3516d90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-azure-active-directory-licensing-in-hello-azure-classic-portal"></a>Ce qui est de licence Bonjour portail Azure classic Microsoft Azure Active Directory ?

> [!div class="op_single_selector"]
> * [Obtenir des instructions pour le portail Azure](active-directory-licensing-get-started-azure-portal.md)
> * [Informations sur le portail Azure Classic](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) est une plateforme et une solution Microsoft de type IDaaS (Identity as a Service). Azure AD est proposé dans de nombreuses techniques et des versions allant de Azure AD gratuit, qui est disponible avec tous les services Microsoft tels qu’Office 365, Dynamics, Microsoft Intune et Azure (Azure AD ne génère pas les tous les frais de consommation dans ce mode,) tooAzure AD payé les versions Enterprise Mobility Suite (EMS), Azure AD Premium et Basic, ainsi que d’Azure multi-Factor Authentication (MFA). À l’instar de nombreux services en ligne Microsoft, la plupart des versions Azure AD payantes sont fournies par le biais de droits par utilisateur, comme dans Office 365, Microsoft Intune et Azure AD. Dans ces cas, fournisseur de service hello est représenté par un ou plusieurs abonnements, et chaque abonnement comprend un nombre préalable à l’achat de licences de votre client. Droits d’utilisateur sont réalisées via une attribution de licence, création d’un lien entre l’utilisateur de hello et produit hello, l’activation des composants du service pour l’utilisateur de hello, hello et consommant une Hello prépayé licences.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article. Pour la tooassign les rôles d’administrateur dans Azure AD de hello admin center, consultez [licence vous-même et vos utilisateurs dans Azure AD](active-directory-licensing-get-started-azure-portal.md).

[Essayez Azure AD Premium maintenant.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

> [!NOTE]
> Portail d’administration Azure AD fait partie de hello portail Azure classic. Alors que l’utilisation d’Azure AD ne nécessite pas l’achat d’Azure, l’accès à ce portail requiert un abonnement Azure actif ou un [abonnement à la version d’évaluation d’Azure](https://azure.microsoft.com/pricing/free-trial/).
>
>

Pour découvrir une présentation détaillée des fonctionnalités des services Azure AD, consultez l’article [Qu’est-ce qu’Azure Active Directory ?](active-directory-whatis.md).
[En savoir plus sur les niveaux de service Azure AD](https://azure.microsoft.com/support/legal/sla/)

> [!NOTE]
> Les abonnements Azure paiement sont différents : alors qu’également représentés dans votre annuaire, ces abonnements permettre la création de ressources Azure et de les mapper tooyour mode de paiement. Dans ce cas il n’existe aucun nombre de licences associés à hello abonnement. Association d’utilisateurs avec abonnement hello, ressources d’abonnement toomanaging utilisateurs hello accès, est obtenue en leur octroyant toooperate d’autorisations sur les ressources Azure mappés toohello abonnement.
>
>

## <a name="how-does-azure-ad-licensing-work"></a>Comment la gestion des licences Azure AD fonctionne-t-elle ?
Les services Azure AD basés sur des licences (sur des droits) reposent sur l’activation d’un abonnement dans votre annuaire/client de service Azure AD. Une fois que l’abonnement hello est active des fonctionnalités de service hello peuvent être gérées par des administrateurs de service d’annuaire et utilisées par les utilisateurs sous licence.

Lorsque vous achetez ou activez Enterprise Mobility Suite, Azure AD Premium ou Azure AD Basic, votre annuaire est mis à jour avec abonnement hello, y compris sa période de validité et prépayé des licences. Vos informations d’abonnement, notamment l’état, les événements du cycle de vie suivant et nombre hello de licences attribuées ou disponibles est disponible via hello portail classique Azure sous l’onglet des licences pour un annuaire spécifique hello hello. Cela est également toobest place toomanage les affectations de licence.

Chaque abonnement se compose d’un ou plusieurs plans de service, chaque hello mappage inclus le niveau fonctionnel du type de service hello ; par exemple, Azure AD, l’authentification Multifacteur Azure, Microsoft Intune, Exchange Online ou SharePoint Online. La gestion des licences Azure AD ne nécessite AUCUNE gestion au niveau des plans de services. Cela est différent à partir d’Office 365, qui s’appuie sur cette configuration avancée mode toomanage access tooincluded services. Azure AD s’appuie sur dans la configuration du service, les fonctionnalités tooenable et gérer des autorisations individuelles.

En règle générale, les informations d’abonnement Azure AD sont gérées via hello portail Azure classic, sous l’onglet des licences pour un annuaire spécifique hello hello. Les abonnements AD Azure, avec l’exception hello d’Azure AD Premium, ne s’affichent pas dans le portail Office de hello.

> [!IMPORTANT]
> Azure Active Directory Premium et Basic, ainsi que les abonnements Enterprise Mobility Suite, sont tootheir confiné configuré/locataire d’annuaire. Abonnements ne peut pas être partagés entre les répertoires ou les utilisateurs tooentitle utilisés dans d’autres répertoires. Déplacement d’un abonnement entre les annuaires est possible, mais nécessite l’envoi d’un ticket de support ou l’annulation de rachat dans les cas de hello d’achats directs.
>
> Lors de l’achat d’Azure AD ou Enterprise Mobility Suite via une licence en Volume Activation de l’abonnement se produit automatiquement lorsque le contrat de hello inclut les autres services Microsoft Online services, par exemple, Office 365.
>
>

Payé fonctionnalités Azure AD transversales span hello du répertoire de hello. Voici quelques exemples :

* Affectation basée sur le groupe tooapplications, qui est activées sous l’application spécifique de hello que vous gérez.
* Avancées et les fonctionnalités de gestion de groupes en libre-service sont disponibles sous configuration de l’annuaire hello ou dans un groupe spécifique de hello.
* Rapports de sécurité Premium sont sur l’onglet Création de rapports de hello
* Détection des applications cloud s’affiche dans hello portail Azure sous l’identité.

### <a name="assigning-licenses"></a>Attribution de licences
Obtention d’un abonnement est qu'il suffit donc tooconfigure payé des fonctionnalités, à l’aide des fonctionnalités payée Azure AD nécessite distribution individuals droit toohello de licences. En règle générale, tout utilisateur qui doit avoir tooor d’accès qui est gérée via une annonce Azure payé fonctionnalité doit avoir une licence. L’attribution d’une licence est un mappage entre un utilisateur et un service acheté, comme Azure AD Premium, Azure AD Standard ou Enterprise Mobility Suite.

La gestion des utilisateurs de votre annuaire qui doivent disposer d’une licence est simple. Il est possible en assignant des règles d’affectation via le portail d’administration Azure AD hello tooa groupe toocreate ou en assignant des licences directement toohello bonnes personnes via un portail, PowerShell ou des API. Lorsque vous affectez le groupe de licences tooa, tous les membres du groupe sont affectés à une licence. Si les utilisateurs sont ajoutés ou supprimés du groupe de hello, elles seront licence hello attribué ou supprimés. L’affectation du groupe peut utiliser n’importe quel tooyou disponibles de gestion de groupe et est cohérente avec l’affectation basée sur le groupe tooapplications. À l’aide de cette approche, vous pouvez configurer des règles de telle sorte que tous les utilisateurs dans votre annuaire sont automatiquement affectés, assurez-vous que tout le monde avec le titre de travail approprié hello possède une licence ou même déléguer gestionnaires de tooother de décision de hello de hello entreprise.

Avec l’attribution de licence basée sur un groupe, tout utilisateur manquant un emplacement d’utilisation héritera de répertoire hello lors de l’attribution. Cet emplacement peut être modifié par l’administrateur de hello à tout moment. Dans les cas où hello automatisée a échoué en raison de l’attribution tooerror, les informations d’utilisateur hello sous que le type de licence reflètent cet état.

## <a name="getting-started-with-azure-ad-licensing"></a>Prise en main de la gestion des licences Azure AD
Prise en main d’Azure AD est facile ; Vous pouvez toujours créer votre annuaire dans le cadre de l’inscription gratuite tooa Azure. [En savoir plus sur l’inscription en tant qu’organisation](sign-up-organization.md). suivant de Hello peut vous aider à vous assurer que votre annuaire est mieux aligné avec d’autres services Microsoft vous pouvez consommer ou que vous prévoyez de tooconsume et vos objectifs de l’obtention du service de hello.

Voici quelques meilleures pratiques :

* Si vous utilisez déjà l’un des services d’organisation de Microsoft, vous disposez déjà d’un annuaire Azure AD. Dans ce cas, vous devez continuer toouse hello même répertoire pour d’autres services, afin que la gestion des identités core, y compris l’approvisionnement et hybrides SSO, peut être utilisée dans les services de hello. Vos utilisateurs bénéficient d’une ouverture de session unique et bénéficieront de fonctionnalités plus riches entre les services hello. Par conséquent, si vous décidez de toobuy une annonce Azure payé service pour votre personnel, nous vous recommandons d’utiliser hello même répertoire toodo cela.
* Si vous envisagez de toouse Azure AD pour un ensemble différent d’utilisateurs (clients, partenaires et ainsi de suite), ou si vous souhaitez que les services tooevaluate Azure AD et que vous souhaitez toodo qui en isolement de votre service de production, ou si vous cherchez toosetup un environnement de bac à sable pour vos services, nous vous recommandons de tout d’abord créer un nouveau répertoire via le portail classique Azure Azure de hello. [En savoir plus sur la création d’un annuaire Azure AD Bonjour portail Azure classic](active-directory-licensing-directory-independence.md). Hello nouveau répertoire sera créé avec votre compte en tant qu’un utilisateur externe avec des autorisations d’administrateur général. Lorsque vous vous connectez dans toohello Azure classic portail avec ce compte, vous être en mesure de toosee ce répertoire et accéder à toutes les tâches d’administration active. Nous vous recommandons de créer un compte local avec les privilèges appropriés toomanage autres services Microsoft (celles qui sont pas accessibles via le portail Azure classic de hello). [En savoir plus sur la création de comptes d'utilisateurs dans Azure AD](active-directory-create-users.md).

> [!NOTE]
> Azure AD prend en charge les « utilisateurs externes », qui correspondent aux comptes d’utilisateurs d’une instance Azure AD qui ont été créés à l’aide d’un compte Microsoft (MSA) ou d’une identité Azure AD à partir d’un autre annuaire. Pendant que nous sont occupés à étendre cette fonctionnalité dans tous les services d’organisation de Microsoft, dès maintenant ces comptes ne sont pas pris en charge dans des expériences de services hello ; par exemple, portail d’administration hello Office 365 ne prend pas en charge ces utilisateurs. Par conséquent, des utilisateurs externes aux comptes Microsoft Impossible de portail d’administration en mesure de tooaccess hello Office 365, tandis que les utilisateurs externes à partir d’autres annuaires Azure AD seront ignorées. Dans ce dernier cas de hello, compte local seul utilisateur hello, hello Azure AD ou Office 365 directory où hello utilisateur a été initialement créé, étaient accessibles via ces expériences.
>
>

Comme indiqué précédemment, Azure AD existe en différentes versions payantes. Ces versions présentent de légères différences sur le plan de leur disponibilité d’achat :

| Produit | Contrat Entreprise/Licence en volume | Ouverts | CSP | Droits d’utilisation MPN | Achat direct | Version d’évaluation |
| --- | --- | --- | --- | --- | --- | --- |
| Enterprise Mobility Suite |X |X |X |X | |X |
| Azure AD Premium |X |X |X | |X |X |
| Azure AD Standard |X |X |X |X |<br /> |<br /> |

### <a name="select-one-or-more-license-trials"></a>Sélectionner une ou plusieurs versions d’évaluation avec licences
 Dans tous les cas, vous pouvez activer un abonnement d’évaluation Azure AD Premium ou Enterprise Mobility Suite en sélectionnant la version d’évaluation spécifiques hello souhaité dans l’onglet des licences hello dans votre annuaire. Chaque version d’évaluation contient un abonnement de 30 jours avec 100 licences.

![Plans de licence de version d’évaluation Azure Active Directory](./media/active-directory-licensing-what-is/trial_plans.png)

![Plans de licence de version d’évaluation Enterprise Mobility Suite](./media/active-directory-licensing-what-is/EMS_trial_plan.png)

![Plans de licence de version d’évaluation actifs](./media/active-directory-licensing-what-is/active_license_trials.png)

### <a name="assign-licenses"></a>Attribuer des licences
Une fois l’abonnement de hello est actif, vous devez attribuer une licence tooyourself et actualiser hello tooensure de navigateur vous voyez toutes les fonctionnalités de votre. étape suivante Hello est tooassign licences utilisateurs toohello doivent tooaccess ou être incluses dans payant fonctionnalités Azure AD. Comme mentionné ci-dessus dans « Affectation des licences, « hello meilleure manière toodo cela est tooidentify hello groupe représentant l’audience de hello souhaité et affectez-le toohello licence ; de cette façon, les utilisateurs qui sont ajoutés ou supprimés du groupe de hello pendant son cycle de vie recevront tooor supprimé de la licence de hello.

tooassign un tooa un groupe de licences ou utilisateurs individuels, sélectionnez hello régime de licences vous comme tooassign et cliquez sur **affecter** sur la barre de commandes hello.

![Plans de licence de version d’évaluation actifs](./media/active-directory-licensing-what-is/assign_licenses.png)

Une fois dans hello affectation boîte de dialogue pour le plan sélectionné hello, vous pouvez sélectionner des utilisateurs et en les ajoutant toohello **affecter** colonne hello droite. Vous pouvez parcourir la liste des utilisateurs hello ou recherchez des personnes spécifiques à l’aide de la recherche de hello verre sur hello haut à droite de la grille d’utilisateur hello. groupes de tooassign, sélectionnez « Groupes » dans hello **afficher** menu puis cliquez sur le bouton de vérification hello sur hello toorefresh droite hello affectations qui sont affichés.

![Attribution des licences toogroups](./media/active-directory-licensing-what-is/assign_licenses_to_groups.png)

Vous pouvez maintenant rechercher ou parcourir les groupes et ajoutez-les toohello **affecter** colonne Bonjour identique. Vous pouvez utiliser ces tooassign une combinaison des groupes et utilisateurs en une seule opération. toocomplete hello du processus d’attribution, cliquez sur le bouton de vérification hello dans hello coin inférieur droit de la page de hello.

![Message de progression de l’attribution de licence](./media/active-directory-licensing-what-is/license_assignment_progress_message.png)

Lorsqu’un groupe est affecté, ses membres héritent des licences hello dans les 30 minutes, mais généralement de 1 à 2 minutes.

Lors de l’attribution des licences Azure AD, des erreurs d’attribution peuvent se produire, mais restent relativement rares. Les erreurs d’attribution se limitent aux problèmes suivants :

* Conflit d’affectation - lorsqu’un utilisateur a été précédemment attribué une licence qui n’est pas compatible avec licence en cours de hello. Dans ce cas, l’affectation de licence de nouveau hello nécessitera suppression hello précédent.
* Les licences disponibles dépassées - lorsque nombre hello d’utilisateurs dans les groupes assignés dépasse les licences disponibles, état d’attribution des utilisateurs hello reflètent un tooassign échec en raison de toomissing licences.

### <a name="view-assigned-licenses"></a>Visualiser les licences attribuées
Une vue de synthèse de licences attribuées, y compris les événements de cycle de vie abonnement disponible, attribué et suivant sont affichés sur hello **licences** onglet.

![Afficher le numéro de hello de licences attribuées](./media/active-directory-licensing-what-is/view_assigned_licenses.png)

L’accès à un plan de licence permet de visualiser une liste détaillée des utilisateurs et groupes attribués, comprenant l’état d’attribution et le chemin d’accès (attribution directe ou héritée d’un ou de plusieurs groupes).

![Affichage détaillé des licences attribuées pour un plan de licence](./media/active-directory-licensing-what-is/assigned_licenses_detail.png)

La suppression de licences se révèle tout aussi simple que l’attribution de licences. Si l’utilisateur de hello est directement attribué ou pour un groupe attribué, vous pouvez supprimer la licence de hello en sélectionnant le type de licence hello, en sélectionnant **supprimer**, l’ajout d’utilisateur de hello ou liste de suppression de groupe toohello et confirmer l’action de hello. Ou bien, vous pouvez ouvrir un type de licence, sélectionnez hello utilisateur ou groupe spécifique, puis appuyez sur **supprimer** sur la barre de commandes hello. tooend l’héritage d’un utilisateur d’une licence à partir d’un groupe, il vous suffit supprimez hello utilisateur hello groupe.

### <a name="extending-trials"></a>Extension des versions d’évaluation
Les extensions d’évaluation pour les clients sont disponibles en libre-service via le portail de hello Office 365. Un administrateur client peut naviguer toohello [portail Office](https://portal.office.com/#Billing) (accès dépend des autorisations pour le portail Office de hello) et sélectionnez votre version d’évaluation d’Azure AD Premium. Cliquez sur hello **étendre évaluation** et suivez les instructions de hello. Vous devez tooenter une carte de crédit, mais il ne sera pas débitée.

![Extension d’une version d’évaluation de licence dans le portail Office de hello](./media/active-directory-licensing-what-is/extend_license_trial.png)

Les clients peuvent également demander une extension de version d’évaluation en envoyant une demande de support. Un administrateur client peut naviguer toohello Office 365 portal [page de prise en charge](http://aka.ms/extendAADtrial) (accès dépend des autorisations pour la page de support Office hello). Sur cette page, sélectionnez « Abonnements et versions d’évaluation » sous Fonctionnalités, et « Questions de version d’évaluation » sous Symptôme. Enfin, entrez les informations sur les circonstances hello

![Extension d’une version d’évaluation avec licences à l’aide d’une demande de support](./media/active-directory-licensing-what-is/alternate_office_aad_trial_extension.png)

## <a name="next-steps"></a>Étapes suivantes
Maintenant, vous pouvez être prêt tooconfigure et utiliser certaines fonctionnalités d’Azure AD Premium.

* [Réinitialisation de mot de passe en libre service](active-directory-manage-passwords.md)
* [Gestion des groupes en libre service](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Tooapplications d’affectation de groupe](active-directory-manage-groups.md)
* [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Achat direct de licences Azure AD Premium](http://aka.ms/buyaadp)
