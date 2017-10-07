---
title: "rôles d’administrateur aaaAssigning dans Azure Active Directory | Documents Microsoft"
description: "Un rôle d’administrateur peut être utilisé toocreate ou modifier des utilisateurs, attribuer des rôles administratifs, réinitialiser les mots de passe utilisateur, gérer les licences utilisateur ou gérer les domaines. Un utilisateur qui est affecté à un rôle d’administrateur a hello mêmes autorisations sur tous les toowhich de services de cloud computing votre organisation est abonnée."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7fc27e8e-b55f-4194-9b8f-2e95705fb731
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.reviewer: Vince.Smith
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: b96350c7264e6ad3620272e015ed9756b512dc4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assigning-administrator-roles-in-azure-active-directory"></a>Attribution de rôles d’administrateur dans Azure Active Directory
> [!div class="op_single_selector"]
> * [portail Azure]()
> * [portail Azure Classic](active-directory-assign-admin-roles.md)
>
>

Utilisez Azure Active Directory (Azure AD) toodesignate distincts pour les administrateurs pour différentes fonctions. Ces administrateurs peuvent accéder aux fonctionnalités sélectionnées dans hello portail Azure ou le portail Azure classic et, en fonction de leur rôle, sera être en mesure de toocreate ou modifier des utilisateurs, attribuer des rôles d’administrateur tooothers, réinitialiser les mots de passe utilisateur, gérer les licences utilisateur et gérer domaines, entre autres choses. Un utilisateur qui est affecté à un rôle d’administrateur aura hello des mêmes autorisations dans l’ensemble de toowhich de services de cloud hello votre organisation est abonnée, que vous affectiez le rôle hello dans le portail hello Office 365, ou Bonjour portail Azure classic ou à l’aide de module Hello Azure AD pour PowerShell de Microsoft.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article. Pour la tooassign les rôles d’administrateur dans Azure AD de hello admin center, consultez [attribution de rôles d’administrateur dans Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md).


Hello suivant des rôles d’administrateur est disponible :

* **Administrateur de facturation**: effectue les achats, gère les abonnements ainsi que les tickets de support et surveille l’état des services.

* **Administrateur de conformité**: les utilisateurs disposant de ce rôle disposent des autorisations de gestion dans hello Office 365 sécurité & de centre de conformité et de centre d’administration Exchange. Pour plus d’informations, consultez l’article [À propos des rôles d’administrateur Office 365](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Administrateur de l’accès conditionnel**: les utilisateurs disposant de ce rôle ont des paramètres de l’accès conditionnel de hello capacité toomanage Azure Active Directory.

* **Administrateur de Service CRM**: les utilisateurs avec ce rôle ont des autorisations globales dans Microsoft CRM Online, lorsque le service de hello est présent, ainsi que de hello capacité toomanage des tickets de support et surveiller l’intégrité du service. Plus d’informations sur les [Rôles d’administrateur dans Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Administrateurs de l’appareil**: utilisateurs avec ce rôle de devenir des administrateurs d’ordinateur local sur tous les appareils Windows 10 qui sont jointe tooAzure Active Directory. Ils n’ont pas d’objets de périphériques hello capacité toomanage dans Azure Active Directory.

* **Lecteurs d’annuaire**: il s’agit d’un rôle hérité tooapplications toobe attribué qui ne prennent pas en charge hello [infrastructure de consentement](active-directory-integrating-applications.md). Il ne doit pas être attribuée aux utilisateurs de tooany.

* **Comptes de synchronisation de répertoire**: n’utilisez pas cela. Ce rôle est automatiquement attribué toohello Azure AD Connect service et pas prévu et pris en charge pour toute autre utilisation.

* **Répertoire Writers**: il s’agit d’un rôle hérité tooapplications toobe attribué qui ne prennent pas en charge hello [infrastructure de consentement](active-directory-integrating-applications.md). Il ne doit pas être attribuée aux utilisateurs de tooany.

* **Administrateur de Service Exchange**: les utilisateurs avec ce rôle ont des autorisations globales dans Microsoft Exchange Online, lorsque le service hello est présent. Plus d’informations sur les [Rôles d’administrateur dans Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Administrateur général / administrateur de la société**: les utilisateurs disposant de ce rôle ont des fonctionnalités d’administration de l’accès tooall dans Azure Active Directory, ainsi que tooAzure fédérée Active Directory, comme Exchange Online, SharePoint Online, des services et Skype pour entreprises en ligne. personne Hello qui s’inscrit pour le client d’Azure Active Directory hello devient un administrateur global. Seuls les administrateurs généraux peuvent affecter d’autres rôles d’administrateur. Une entreprise peut comprendre plusieurs administrateurs généraux. Les administrateurs généraux peuvent réinitialiser le mot de passe de hello pour tous les utilisateurs et tous les autres administrateurs.

  > [!NOTE]
  > Dans l’API Microsoft Graph, l’API Azure AD Graph et Azure AD PowerShell, ce rôle est identifié comme « Administrateur de l’entreprise ». Il est « Administrateur général » Bonjour [portail Azure](https://portal.azure.com).
  >
  >

* **Émetteur de l’invitation invité**: les utilisateurs de ce rôle peuvent gérer invitations d’utilisateur invité de Azure Active Directory B2B lorsque hello « Membres peuvent inviter » utilisateur est défini tooNo. Plus d’informations sur la collaboration B2B à [sur la version préliminaire de hello Azure AD B2B collaboration](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b). Il n’inclut pas d’autres autorisations.

* **Administrateur du Service Intune**: les utilisateurs avec ce rôle ont des autorisations globales dans Microsoft Intune Online, lorsque le service hello est présent. En outre, ce rôle contient les utilisateurs toomanage de capacité hello et des périphériques dans la stratégie de tooassociate de commande, ainsi que créer et gérer des groupes.

* **Administrateur de la boîte aux lettres** : ce rôle n’est utilisé que dans le cadre de la prise en charge de la messagerie Exchange Online sur les appareils RIM Blackberry. Si votre organisation n’utilise pas la messagerie Exchange Online sur les appareils RIM Blackberry, n’employez pas ce rôle.

* **Support de niveau 1 de partenaire** : ne pas utiliser. Ce rôle a été déconseillé et sera supprimé d’Azure AD Bonjour futures. Il s’adresse à un petit nombre de partenaires revendeurs Microsoft et n’est pas destiné à une utilisation générale.

* **Support de niveau 2 de partenaire** : ne pas utiliser. Ce rôle a été déconseillé et sera supprimé d’Azure AD Bonjour futures. Il s’adresse à un petit nombre de partenaires revendeurs Microsoft et n’est pas destiné à une utilisation générale.

* **Administrateur de mots de passe/Administrateur du support technique** : les utilisateurs dotés de ce rôle peuvent réinitialiser les mots de passe, gérer les demandes de service et surveiller l’état des services. Les administrateurs de mots de passe peuvent réinitialiser uniquement les mots de passe des utilisateurs et des autres administrateurs de mots de passe.

  > [!NOTE]
  > Dans l’API Microsoft Graph, l’API Azure AD Graph et Azure AD PowerShell, ce rôle est identifié comme « Administrateur Helpdesk ». Il est « mot de passe administrateur » Bonjour [portail Azure](https://portal.azure.com/).
  >
  >
  
* **Administrateur de Service Power BI**: les utilisateurs avec ce rôle ont des autorisations globales dans Microsoft Power BI, lorsque le service de hello est présent, ainsi que de hello capacité toomanage des tickets de support et surveiller l’intégrité du service. Plus d’informations sur les [Rôles d’administrateur dans Office 365](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d?ui=en-US&rs=en-001&ad=US).

* **Administrateur de rôle privilégié** : les utilisateurs disposant de ce rôle peuvent gérer les attributions de rôles dans Azure Active Directory, ainsi que dans Azure AD Privileged Identity Management. En outre, ce rôle permet de gérer tous les aspects de Privileged Identity Management.

* **Administrateur de sécurité**: les utilisateurs avec ce rôle ont toutes les autorisations en lecture seule de hello de rôle de lecteur hello sécurité, ainsi que la configuration de toomanage hello possibilité pour les services liés à la sécurité : Protection d’identité Azure Active Directory, Azure Protection des informations, Privileged Identity Management, Office 365 sécurité et centre de conformité. Plus d’informations sur les autorisations d’Office 365 est disponible à l’adresse [autorisations dans Office 365 sécurité Bonjour centre de conformité](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

* **Lecteur de sécurité**: les utilisateurs disposant de ce rôle ont accès en lecture seule global, y compris toutes les informations dans Azure Active Directory, la Protection d’identité, Privileged Identity Management, ainsi que hello capacité tooread Azure Active Directory connectez-vous les rapports et les journaux d’audit. rôle de Hello accorde également l’autorisation en lecture seule dans Office 365 sécurité & centre de conformité. Plus d’informations sur les autorisations d’Office 365 est disponible à l’adresse [autorisations dans Office 365 sécurité Bonjour centre de conformité](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

* **Administrateur de service prend en charge**: les utilisateurs disposant de ce rôle peuvent ouvrir des demandes de support auprès de Microsoft pour les services Azure et Office 365 et vues hello centre de tableau de bord et le message de service de hello portail Azure et le portail d’administration d’Office 365. Plus d’informations sur les [Rôles d’administrateur dans Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Administrateur de Service SharePoint**: les utilisateurs avec ce rôle ont des autorisations globales dans Microsoft SharePoint Online, lorsque le service de hello est présent, ainsi que de hello capacité toomanage des tickets de support et surveiller l’intégrité du service. Plus d’informations sur les [Rôles d’administrateur dans Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Skype pour entreprises / administrateur de Service Lync**: les utilisateurs disposant de ce rôle ont des autorisations globales dans Skype Microsoft pour les entreprises, lorsque le service hello est présent, ainsient que gérer les attributs d’utilisateur Skype spécifiques dans Azure Active Directory. En outre, cette tickets de support toomanage de capacité de rôle accorde hello et l’analyse de service d’intégrité. Plus d’informations sur les [Rôles d’administrateur dans Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

  > [!NOTE]
  > Dans l’API Microsoft Graph, l’API Azure AD Graph et Azure AD PowerShell, ce rôle est identifié comme « Administrateur des services Lync ». Il est « Skype pour administrateur du Service métier » Bonjour [portail Azure](https://portal.azure.com/).
  >
  >

* **Administrateur des comptes d’utilisateur** : les utilisateurs disposant de ce rôle peuvent créer et gérer tous les aspects relatifs aux utilisateurs et groupes. En outre, ce rôle inclut des tickets de support toomanage hello capacité et les analyses d’intégrité du service. Quelques restrictions s’appliquent. Par exemple, ce rôle n’autorise pas la suppression d’un administrateur général. En outre, bien qu’il autorise la modification des mots de passe des utilisateurs non administrateurs, il n’autorise pas la modification des mots de passe des administrateurs généraux ou des autres administrateurs privilégiés.

## <a name="administrator-permissions"></a>Autorisations des administrateurs

### <a name="billing-administrator"></a>Administrateur de facturation

| Peut | Ne peut pas |
| --- | --- |
|<p>Afficher les informations sur la société et les utilisateurs</p><p>Gérer les tickets de support Office</p><p>Effectuer des opérations de facturation et d’achat pour des produits Office</p> |<p>Réinitialiser les mots de passe utilisateur</p><p>Créer et gérer des vues utilisateur</p><p>Créer, modifier et supprimer des utilisateurs et groupes, et gérer les licences utilisateur</p><p>Gérer des domaines</p><p>Modifier les informations de l’entreprise</p><p>Déléguer des rôles d’administrateur tooothers</p><p>Utiliser la synchronisation de répertoires</p><p>Afficher les journaux d’audit</p>|

### <a name="conditional-access-administrator"></a>Administrateur de l’accès conditionnel
| Peut | Ne peut pas |
| --- | --- |
|<p>Afficher les informations sur la société et les utilisateurs</p><p>Gérer les paramètres d’accès conditionnel</p> |<p>Réinitialiser les mots de passe utilisateur</p><p>Créer et gérer des vues utilisateur</p><p>Créer, modifier et supprimer des utilisateurs et groupes, et gérer les licences utilisateur</p><p>Gérer des domaines</p><p>Modifier les informations de l’entreprise</p><p>Déléguer des rôles d’administrateur tooothers</p><p>Utiliser la synchronisation de répertoires</p><p>Afficher les journaux d’audit</p>|

### <a name="global-administrator"></a>Administrateur général
| Peut | Ne peut pas |
| --- | --- |
|<p>Afficher les informations sur la société et les utilisateurs</p><p>Gérer les tickets de support Office</p><p>Effectuer des opérations de facturation et d’achat pour des produits Office</p><p>Réinitialiser les mots de passe utilisateur</p><p>Réinitialiser les mots de passe de l’autre administrateur</p><p>Créer et gérer des vues utilisateur</p><p>Créer, modifier et supprimer des utilisateurs et groupes, et gérer les licences utilisateur</p><p>Gérer des domaines</p><p>Modifier les informations de l’entreprise</p><p>Déléguer des rôles d’administrateur tooothers</p><p>Utiliser la synchronisation de répertoires</p><p>Activer ou désactiver l’authentification multifacteur</p><p>Afficher les journaux d’audit</p> |<p>N/A</p>|

### <a name="password-administrator"></a>Administrateur de mots de passe
| Peut | Ne peut pas |
| --- | --- |
| <p>Afficher les informations sur la société et les utilisateurs</p><p>Gérer les tickets de support Office</p><p>Réinitialiser les mots de passe utilisateur</p> <p>Réinitialiser les mots de passe de l’autre administrateur</p>|<p>Effectuer des opérations de facturation et d’achat pour des produits Office</p><p>Créer et gérer des vues utilisateur</p><p>Créer, modifier et supprimer des utilisateurs et groupes, et gérer les licences utilisateur</p><p>Gérer des domaines</p><p>Modifier les informations de l’entreprise</p><p>Déléguer des rôles d’administrateur tooothers</p><p>Utiliser la synchronisation de répertoires</p><p>Afficher des rapports</p>|

### <a name="service-administrator"></a>Administrateur de services fédérés
| Peut | Ne peut pas |
| --- | --- |
| <p>Afficher les informations sur la société et les utilisateurs</p><p>Gérer les tickets de support Office</p> |<p>Réinitialiser les mots de passe utilisateur</p><p>Effectuer des opérations de facturation et d’achat pour des produits Office</p><p>Créer et gérer des vues utilisateur</p><p>Créer, modifier et supprimer des utilisateurs et groupes, et gérer les licences utilisateur</p><p>Gérer des domaines</p><p>Modifier les informations de l’entreprise</p><p>Déléguer des rôles d’administrateur tooothers</p><p>Utiliser la synchronisation de répertoires</p><p>Afficher les journaux d’audit</p> |

### <a name="user-administrator"></a>Administrateur d’utilisateurs
| Peut | Ne peut pas |
| --- | --- |
| <p>Afficher les informations sur la société et les utilisateurs</p><p>Gérer les tickets de support Office</p><p>Réinitialisez les mots de passe utilisateur, avec certaines limitations.</p><p>Réinitialiser les mots de passe de l’autre administrateur</p><p>Réinitialiser les mots de passe des autres utilisateurs</p><p>Créer et gérer des vues utilisateur</p><p>Créer, modifier et supprimer des utilisateurs et groupes, et gérer les licences utilisateur, avec des restrictions. Il lui est impossible de supprimer un administrateur général ou de créer d’autres administrateurs.</p> |<p>Effectuer des opérations de facturation et d’achat pour des produits Office</p><p>Gérer des domaines</p><p>Modifier les informations de l’entreprise</p><p>Déléguer des rôles d’administrateur tooothers</p><p>Utiliser la synchronisation de répertoires</p><p>Activer ou désactiver l’authentification multifacteur</p><p>Afficher les journaux d’audit</p> |

### <a name="security-reader"></a>Lecteur de sécurité
| Dans | Peut |
| --- | --- |
| Identity Protection Center |Lire tous les rapports de sécurité et informations de paramètres pour les fonctionnalités de sécurité<ul><li>Anti-spam<li>Chiffrement<li>Prévention contre la perte de données<li>Anti-programme malveillant<li>Détection avancée des menaces<li>Anti-hameçonnage<li>Règles du flux de messagerie |
| Privileged Identity Management |<p>Contient des informations de tooall d’accès en lecture seule signalées dans Azure AD PIM : stratégies et des rapports pour les attributions de rôle Azure AD, sécurité passe en revue et Bonjour futures lire toopolicy accéder à des données et des rapports pour les scénarios en dehors de l’attribution de rôle Azure AD.<p>**Ne peut pas** s’inscrire à Azure AD PIM ou rendre tout tooit de modifications. Dans le portail de PIM ou via PowerShell, qui fait partie de ce rôle peut activer des rôles supplémentaires (par exemple, administrateur général ou administrateur du rôle privilégié), si l’utilisateur de hello est un candidat pour eux. |
| <p>Monitor Office 365 Service Health</p><p>Centre de sécurité et conformité Office 365</p> |<ul><li>Lire et gérer les alertes<li>Lire les stratégies de sécurité<li>Lire les informations sur les menaces, Cloud App Discovery et Mise en quarantaine dans Recherche et enquêtes<li>Lecture de tous les rapports |

### <a name="security-administrator"></a>Security Administrator
| Dans | Peut |
| --- | --- |
| Identity Protection Center |<ul><li>Toutes les autorisations du rôle de sécurité Reader hello.<li>En outre, hello tooperform de capacité de toutes les opérations IPC à l’exception de la réinitialisation des mots de passe. |
| Privileged Identity Management |<ul><li>Toutes les autorisations du rôle de sécurité Reader hello.<li>**Ne peut pas** gérer les appartenances aux rôles Azure AD ou les paramètres. |
| <p>Monitor Office 365 Service Health</p><p>Centre de sécurité et conformité Office 365 |<ul><li>Toutes les autorisations du rôle de sécurité Reader hello.<li>Tous les paramètres configurables dans la fonctionnalité d’Advanced Threat Protection hello (de la protection contre les programmes malveillants et virus, configuration d’URL malveillante, suivi de l’URL, etc.). |

## <a name="details-about-hello-global-administrator-role"></a>Plus d’informations sur le rôle d’administrateur général hello
administrateur général de Hello possède des fonctionnalités d’administration de l’accès tooall. Par défaut, personne hello s’inscrit à un abonnement Azure rôle hello administrateur global pour le répertoire de hello. Seuls les administrateurs généraux peuvent affecter d’autres rôles d’administrateur.

### <a name="tooadd-a-colleague-as-a-global-administrator"></a>tooadd un collègue en tant qu’administrateur général

1. Connectez-vous à toohello [centre d’administration d’Azure Active Directory](https://aad.portal.azure.com) avec un compte qui est un administrateur global pour l’annuaire de locataire hello.

   ![Ouvrez le Centre d’administration Azure Active Directory](./media/active-directory-assign-admin-roles/active-directory-admin-center.png)

2. Sélectionnez **Utilisateurs et groupes&gt; Tous les utilisateurs**

3. Recherchez hello utilisateur vous souhaitez toodesignate en tant qu’un administrateur global et que vous ouvrez le panneau hello pour cet utilisateur.

4. Dans le panneau d’utilisateur hello, sélectionnez **rôle d’annuaire**.
 
5. Dans le panneau de rôle d’annuaire hello, sélectionnez hello **administrateur Global** rôle et l’enregistrer.

## <a name="assign-or-remove-administrator-roles"></a>Attribution ou suppression de rôles d’administrateur
toolearn utilisateur de tooa tooassign rôles d’administrateur dans Azure Active Directory, voir [affecter un utilisateur tooadministrator des rôles dans Azure Active Directory](active-directory-users-assign-role-azure-portal.md).

## <a name="deprecated-roles"></a>Rôles déconseillés

Hello suivant rôles ne doit pas être utilisée. Ils été déconseillée et sera supprimée d’Azure AD Bonjour futures.

* Administrateur de licences ad hoc
* Créateur d’utilisateur vérifié par e-mail
* Jonction d’appareils
* Gestionnaires d’appareils
* Utilisateurs d’appareils
* Jonction d’appareils d’espace de travail

## <a name="next-steps"></a>Étapes suivantes
* toolearn savoir plus sur les administrateurs de toochange pour un abonnement Azure, voir [comment tooadd ou modifier les rôles administrateur Azure](../billing-add-change-azure-subscription-administrator.md)
* toolearn en savoir plus sur la façon dont l’accès aux ressources est contrôlé dans Microsoft Azure, consultez [présentation de l’accès aux ressources dans Azure](active-directory-understanding-resource-access.md)
* Pour plus d’informations sur la façon dont Azure Active Directory est lié tooyour abonnement Azure, consultez [les abonnements Azure sont associés à Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* [Gestion des utilisateurs](active-directory-create-users.md)
* [Gestion des mots de passe](active-directory-manage-passwords.md)
* [Gestion des groupes](active-directory-manage-groups.md)
