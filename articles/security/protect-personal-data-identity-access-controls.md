---
title: "les données personnelles aaaProtect avec des contrôles d’accès et des identités Azure | Documents Microsoft"
description: "À l’aide d’Azure toohelp de contrôles identités et des accès, vous protégez vos données personnelles"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a>Azure Active Directory et Multi-Factor Authentication : protéger les données personnelles avec des contrôles d’accès et d’identité

Cet article fournit des informations et des procédures que vous pouvez utiliser les données personnelles tooprotect via les services et les fonctionnalités de sécurité de l’authentification Azure Active Directory et de plusieurs facteurs.

## <a name="scenario"></a>Scénario

Une société de croisière volumineux en hello États-Unis, étend ses itinéraires de toooffer d’opérations dans hello Méditerranée, Adriatique et mer Baltique, ainsi que hello britanniques. toosupport ces efforts, elle a acquis plusieurs lignes croisière plus petits exercées en Italie, Allemagne, Danemark et hello Royaume-Uni 

la société de Hello utilise des données d’entreprise de Microsoft Azure toostore dans le cloud de hello. Ces dernières incluent des informations d’identification personnelle telles que les noms, les adresses, les numéros de téléphone et les informations de carte de crédit de sa base de clients globale. Il inclut également des informations de ressources humaines traditionnelles telles que les adresses et numéros de téléphone, numéros d’identification de taxe médicales plus d’informations sur les employés de la société dans tous les emplacements. ligne de croisière Hello gère également les bases de données volumineuses de membres du programme de récompense et fidélité qui inclut des informations personnelles tootrack des relations avec les clients en cours et passées.

Réseau de hello accès employés de l’entreprise à partir de sites distants et les agents de voyage société hello situés dans Bonjour tout le monde ont accès aux ressources de l’entreprise toosome.

## <a name="problem-statement"></a>Définition du problème

société de Hello doit protection hello des employés et les clients des données personnelles à partir des attaquants qui toouse compromis identités toogain accèdent. Ils doivent également vous assurer que toopersonal accès aux données par les utilisateurs légitimes sont limitées à ceux qui en ont besoin toodo leur travail.

## <a name="company-goal"></a>Objectif de l’entreprise

objectif de l’entreprise Hello est contrôlé tooensure qui accèdent aux données de toopersonal. Il est essentiel que les identités des utilisateurs à accéder à des données toopersonal soit protégé par l’authentification forte. Une stratégie de [privilège minimum] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) doit être appliquée afin que les utilisateurs légitimes ont seul niveau hello d’accès dont ils ont besoin et pas plus.

## <a name="solutions"></a>Solutions

Microsoft Azure fournit des outils de gestion des identités et des accès toohelp sociétés contrôler l’accès tooresources qui contiennent des données personnelles.

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) gère les identités et contrôle l’accès tooAzure ainsi que les autres localement et autres ressources de cloud, les données et les applications. [Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) aide les administrateurs Azure toominimize hello différents aux personnes qui ont accès toocertain plus d’informations, telles que les données personnelles. Il leur permet de toodiscover, restreindre et surveiller des identités privilégiées et leurs accès tooresources et tooassign temporaire, juste à temps (JIT) des droits d’administration tooeligible les utilisateurs. Il fournit également des informations sur les personnes dotées de privilèges Administrateur AAD.

Hello les activités liées à l’utilisation de AAD PIM incluent :

- Activation de Privileged Identity Management pour votre annuaire

- À l’aide des informations importantes Privileged Identity Management Administration du tableau de bord toosee un coup de œil

- Gestion des identités hello privilégié (administrateurs) en ajoutant ou supprimant le rôle d’administrateurs permanents ou éligibles tooeach

- Configurer les paramètres d’activation de rôle hello

- Activation des rôles

- Révision des activités de rôle

#### <a name="how-do-i-enable-aad-pim"></a>Comment activer AAD PIM ?

toostart à l’aide de PIM pour votre annuaire, hello suivant :

1. Se connecter toohello portail Azure en tant qu’administrateur général de votre annuaire.

2. Si votre organisation a plusieurs répertoires, sélectionnez votre nom d’utilisateur dans le coin supérieur droit hello Hello portail Azure. Sélectionnez le répertoire hello où vous allez utiliser Azure AD Privileged Identity Management.

3. Sélectionnez **davantage de services** et utiliser hello **filtre** toosearch de zone de texte pour Azure AD Privileged Identity Management.

4. Vérifiez **code confidentiel toodashboard** puis cliquez sur **créer**. Hello application de Privileged Identity Management s’ouvre.

Une fois Azure AD Privileged Identity Management est configuré, vous voyez Panneau de navigation hello lorsque vous ouvrez l’application hello.

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

Pour plus d’informations et pour obtenir des instructions sur la mise en route avec AAD PIM, consultez [Commencer à utiliser Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)

### <a name="azure-role-based-access-control"></a>Contrôle d’accès en fonction du rôle Azure

[Role-Based Access Control de Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) permet de gérer tooAzure d’accéder aux ressources en activant hello octroi d’accès basé sur le rôle d’utilisateur hello administrateurs Azure. Vous pouvez séparer les tâches au sein d’une équipe et accorder uniquement hello quantité toousers d’accès, les groupes et les applications dont ils ont besoin tooperform leur travail.

Accès en fonction du rôle peuvent être accordé toousers à l’aide de hello portail Azure, les outils de ligne de commande Azure ou les API de gestion Azure.

Pour plus d’informations sur les concepts de base Azure RBAC, consultez [prise en main le contrôle d’accès en fonction du rôle Bonjour portail Azure.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a>Comment gérer le contrôle d’accès en fonction du rôle Azure avec PowerShell ?

Vous pouvez utiliser toomanage d’applets de commande PowerShell Azure RBAC, y compris hello les tâches de gestion suivantes :

- Répertorier les rôles

- Voir quel utilisateur a des autorisations d’accès

- Accorder l'accès

- Suppression d'accès

- Créer un rôle personnalisé

- Actions Get pour un fournisseur de ressources

- Modifier un rôle personnalisé

- Supprimer un rôle personnalisé

- Répertorier les rôles personnalisés

Pour obtenir des instructions sur toomanage RBAC Azure avec PowerShell, voir [en fonction du rôle de gérer l’accès avec Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).

### <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication

[L’authentification multifacteur Azure](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) est une solution de vérification en deux étapes qui vous aide à toodata d’accès de sauvegarde et les applications, tout en répondant à la demande de l’utilisateur pour un processus de connexion simple. Il fournit une authentification forte au moyen de diverses méthodes de vérification, notamment les appels téléphoniques, l’envoi de SMS ou la vérification sur l’application mobile.

l’authentification Multifacteur toodeploy Bonjour cloud Azure, vous devez toofirst l’activer et réactivez la vérification en deux étapes pour les utilisateurs.

#### <a name="how-do-i-enable-azure-toouse-mfa"></a>Comment faire pour activer toouse Azure MFA ?

Si vos utilisateurs disposent de licences qui incluent l’authentification multifacteur Azure, aucune n’est que vous avez besoin de tooturn toodo sur Azure MFA. Si ce n’est pas le cas, vous devez toocreate un fournisseur d’authentification multifacteur dans votre annuaire. toodo, procédez comme suit :

1. Sélectionnez **Active Directory** Bonjour portail Azure classic (connecté en tant qu’administrateur).

2. Sélectionnez **Fournisseurs Multi-Factor Authentication.**

3. Sélectionnez **Nouveau**, puis sous **App Services**, sélectionnez **Fournisseur d’authentification multifacteur.**

4. Sélectionnez **Création rapide.**

5. Renseignez le champ de nom hello et sélectionnez un modèle d’utilisation (par authentification ou par utilisateur activé).

6. Désignez un répertoire qui hello fournisseur d’authentification Multifacteur est associé.

7. Cliquez sur hello **créer** bouton.

![](media/protect-personal-data-identity-access-controls/quick-create.png)

Pour plus d’informations sur la façon de toomanage votre fournisseur d’authentification multifacteur, consultez [mise en route avec un fournisseur d’authentification multifacteur Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a>Comment activer la vérification en deux étapes pour les utilisateurs ?

Vous pouvez imposer la vérification en deux étapes pour toutes les connexions, ou vous pouvez créer de vérification en deux étapes de l’accès conditionnel stratégies toorequire uniquement lorsque des conditions spécifiques s’appliquent.

L’activation de l’authentification Multifacteur Azure en modifiant des États utilisateur est approche traditionnelle de hello pour exiger une vérification en deux étapes. Tous les utilisateurs de hello que vous activez hello vérification en deux étapes de même exigence tooperform chaque fois qu’ils se connectent. L’activation d’un utilisateur remplace toutes les stratégies d’accès conditionnel appliquées à cet utilisateur.

L’activation de l’authentification multifacteur Azure avec une stratégie d’accès conditionnel est une approche plus souple pour exiger une vérification en deux étapes. Vous pouvez créer des stratégies d’accès conditionnel qui s’appliquent toogroups, ainsi que des utilisateurs individuels. Vous pouvez appliquer davantage de restrictions aux groupes à haut risque par rapport aux groupes à faible risque, ou exiger la vérification en deux étapes uniquement pour les applications cloud à haut risque tout en ignorant celles à faible risque. Toutefois, l’accès conditionnel est une fonctionnalité payante d’Azure Active Directory.

tooenable l’authentification Multifacteur en modifiant l’état utilisateur, procédez comme hello suivant :

1. Se connecter toohello portail Azure en tant qu’administrateur.
2. Accédez trop**Azure Active Directory \> utilisateurs et groupes \> tous les utilisateurs**.
3. Sélectionnez **Multi-Factor Authentication**.
4. Rechercher un utilisateur hello que vous souhaitez tooenable pour Azure MFA. Vous devrez peut-être toochange hello vue haut hello.
5. Vérifiez hello boîte suivant toohello nom de l’utilisateur.
6. Sur la droite, sous étapes rapides de hello, choisissez **activer**.

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. Confirmez votre sélection dans la fenêtre contextuelle hello qui s’ouvre.  Les utilisateurs pour lesquels l’authentification Multifacteur a été activé demandera tooregister hello leur prochaine dans que connexion.

tooenable Azure MFA avec une stratégie d’accès conditionnel, hello suivant :

1. Se connecter toohello portail Azure en tant qu’administrateur.

2. Accédez trop**Azure Active Directory \> accès conditionnel**.

3. Sélectionnez **Nouvelle stratégie**.

4. Sous **Affectations**, sélectionnez **Utilisateurs et groupes**. Hello d’utilisation **Include** et **exclure** onglets toospecify quels utilisateurs et groupes qui est géré par la stratégie de hello.

5. Sous **Affectations**, sélectionnez **Applications cloud.** Choisissez trop**inclure toutes les applications cloud**.
6.  Sous **Contrôles d’accès**, sélectionnez **Accorder**. Choisissez **Exiger une authentification multifacteur**.
7.  Activer **activer la stratégie** trop**sur** , puis sélectionnez **enregistrer**.

Pour plus d’informations sur comment tooconfigure Azure MFA paramètres tooset des alertes de fraude, créer un contournement à usage unique, utiliser des messages vocaux personnalisés, configurer la mise en cache, spécifiez les adresses IP approuvées, créer des mots de passe d’application, activer la mémorisation de l’authentification Multifacteur pour les appareils auxquels les utilisateurs faites confiance, puis sélectionnez méthodes de vérification, consultez [configurer les paramètres d’authentification multifacteur Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)

## <a name="next-steps"></a>Étapes suivantes

- [Sécurisation de l’accès privilégié dans Azure AD](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [Forum aux questions sur Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [Résolution des problèmes de contrôle d’accès en fonction du rôle](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
