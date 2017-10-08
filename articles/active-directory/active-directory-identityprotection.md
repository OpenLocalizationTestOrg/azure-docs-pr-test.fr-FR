---
title: aaaAzure Active Directory Identity Protection | Documents Microsoft
description: "Découvrez comment Azure AD Identity Protection vous permet capacité hello toolimit une personne malveillante de tooexploit une identité compromise ou l’unité et toosecure une identité ou un périphérique qui a été précédemment toobe suspectée ou connu compromis."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestion d’applications, sécurité, risque, niveau de risque, vulnérabilité, stratégie de sécurité"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection

Azure Active Directory Identity Protection est une fonctionnalité d’édition hello Azure AD Premium P2 qui vous permet de :

- Détecter les vulnérabilités potentielles qui affectent les identités de votre organisation

- Configurer des actions suspectes de réponses automatiques toodetected qui sont les identités de l’organisation tooyour connexes  

- Examiner les incidents suspects et prendre les mesures appropriées tooresolve les   


## <a name="getting-started"></a>Prise en main

Microsoft sécurise les identités basées sur le cloud depuis plus de dix ans. Avec la Protection d’identité Azure Active Directory, dans votre environnement, vous pouvez utiliser hello mêmes systèmes de protection Microsoft utilise des identités toosecure.

Hello grande majorité des prennent des failles de sécurité placer lorsque des personnes malveillantes accèdent environnement tooan d’accès par le vol d’identité d’un utilisateur. Années de hello, des personnes malveillantes sont devenues plus efficaces en tirant parti des violations de tiers et d’utilisation des attaques d’hameçonnage sophistiquées. Dès qu’une personne malveillante accès aux comptes d’utilisateur doté de privilèges faibles tooeven, il est relativement facile pour les ressources d’entreprise tooimportant toogain accès via un mouvement latéral.

Par conséquent, vous devez :

- Protéger toutes les identités, quel que soit leur niveau de privilège

- Empêcher proactivement le détournement des identités compromises

Détecter les identités compromises n’est pas chose aisée. Azure Active Directory utilise des algorithmes d’apprentissage automatique adaptative et anomalies de toodetect heuristique et les incidents suspects qui indiquent potentiellement compromis des identités. Protection de l’identité à l’aide de ces données, génère des rapports et les alertes qui permettent de vous hello de tooevaluate a détecté des problèmes et atténuation appropriés ou les actions de mise à jour.

Mais Azure Active Directory Identity Protection est bien plus qu’un outil de surveillance et de création de rapports. tooprotect identités de votre organisation, vous pouvez configurer des stratégies basées sur les risques qui répondent automatiquement toodetected problèmes lorsqu’un niveau de risque spécifié a été atteint. Ces stratégies, en outre tooother conditionnel accéder aux contrôles fournis par Azure Active Directory et EMS, pouvez bloquer automatiquement ou initier des actions de mise à jour ADAPTATIF, y compris les réinitialisations de mot de passe et la mise en œuvre l’authentification multifacteur.


#### <a name="identity-protection-capabilities"></a>Fonctionnalités d’Identity Protection

**Détection des vulnérabilités et des comptes à risque :**  

* Fournir des recommandations personnalisées tooimprove globale posture de sécurité en mettant en surbrillance les vulnérabilités
* Calcul des niveaux de risque à la connexion
* Calcul du niveau de risque des utilisateurs


**Examen des événements à risque :**

* Envoi de notifications pour les événements à risque
* Examen des événements à risque à l’aide d’informations contextuelles et pertinentes
* En fournissant des workflows de base tootrack enquêtes
* Fournissant un accès facile tooremediation des actions telles que la réinitialisation de mot de passe

**Stratégies d’accès conditionnel en fonction des risques :**

* Stratégie toomitigate risquées connexions par le blocage des connexions ou exigeant l’authentification multifacteur.
* Stratégie tooblock ou des comptes d’utilisateur présente des risques sécurisé
* Stratégie toorequire utilisateurs tooregister pour l’authentification multifacteur



## <a name="identity-protection-roles"></a>Rôles de protection des identités (Identity Protection)

activités de gestion hello tooload solde autour de votre implémentation de la Protection d’identité, vous pouvez attribuer plusieurs rôles. Azure AD Identity Protection prend en charge 3 rôles d’annuaire :

| Rôle                         | Peut                          | Ne peut pas
| :--                          | ---                                |  ---   |
| Administrateur général         | Accès complet tooIdentity Protection, intégrer Identity Protection| |
| Administrateur de sécurité       | Accès complet tooIdentity Protection | Onboard Identity Protection, réinitialiser les mots de passe pour un utilisateur |
| Lecteur de sécurité              | Accès seule tooIdentity Protection | Onboard Identity Protection, résoudre les utilisateurs, configurer les utilisateurs, réinitialiser les mots de passe |




Pour plus d’informations, voir [Attribution de rôles d’administrateur dans Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)



## <a name="detection"></a>Détection

### <a name="vulnerabilities"></a>Vulnérabilités

Azure Active Directory Identity Protection analyse votre configuration et détecte les vulnérabilités qui peuvent avoir un impact sur les identités de vos utilisateurs. Pour en savoir plus, consultez [Vulnérabilités détectées par Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).

### <a name="risk-events"></a>Événements à risque

Azure Active Directory utilise des algorithmes et des paramètres heuristiques toodetect suspecte que les actions associées tooyour identités des utilisateurs d’apprentissage adaptatif. système de Hello crée un enregistrement pour chaque action suspect détecté. Ces enregistrements sont également appelés événements à risque.  
Pour en savoir plus, consultez [Événements à risque dans Azure Active Directory](active-directory-identity-protection-risk-events.md).


## <a name="investigation"></a>Investigation
Votre parcours via la Protection d’identité commence généralement par le tableau de bord hello Identity Protection.

![Correction](./media/active-directory-identityprotection/1000.png "Correction")

tableau de bord Hello vous donne accès à :

* des rapports comme **Utilisateurs associés à un indicateur de risque**, **Événements à risque** et **Vulnérabilités** ;
* Paramètres de configuration hello de votre **des stratégies de sécurité**, **Notifications** et **l’inscription de l’authentification multifacteur**

Il est généralement votre point de départ pour l’enquête, qui est le processus hello de révision des activités de hello, les journaux et autres informations pertinentes associée tooa risque de toodecide d’événements si les étapes de mise à jour ou d’atténuation sont nécessaires, et comment l’identité de hello a été compromis et comprendre comment hello compromis identité a été utilisée.

Vous pouvez lier votre toohello d’activités enquête [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection envoie par courrier électronique.

Hello sections suivantes vous fournissent plus de détails et les étapes hello tooan connexes enquête.  


## <a name="risky-sign-ins"></a>Connexions risquées

Azure Active Directory détecte les [types d’événements à risque](active-directory-reporting-risk-events.md#risk-event-types) en temps réel et hors connexion. Chaque événement à risque qui a été détectée pour une connexion d’un utilisateur contribue tooa concept logique appelée connectez-vous présente des risques. Une connexion à présente des risques est un indicateur pour une tentative de connexion qui a ne peut-être pas été exécutée par le propriétaire légitime de hello d’un compte d’utilisateur.


### <a name="sign-in-risk-level"></a>Niveau de risque d’une connexion

Un niveau de risque de connexion est une indication (haute, moyenne ou faible) de probabilité de hello qu’une tentative de connexion n’a pas été effectuée par le propriétaire légitime de hello d’un compte d’utilisateur.

### <a name="mitigating-sign-in-risk-events"></a>Atténuation des événements à risque à la connexion

Une limitation est une action toolimit hello capacité un appareil sans restauration de l’état sans échec tooa hello identité ou un périphérique ou un attaquant tooexploit une identité compromise. Une atténuation ne résout pas les événements précédents connectez-vous risque associés hello identité ou d’appareil.

toomitigate risquée connexions automatiquement, vous pouvez configurer policicies de sécurité risque de connexion. À l’aide de ces stratégies, considèrent le niveau de risque de hello d’utilisateur de hello ou hello connectez-vous tooblock connexions risquées ou exiger l’authentification multifacteur de hello utilisateur tooperform. Ces actions peuvent empêcher un attaquant d’exploiter un endommagement de toocause d’identité et peuvent offrir une identité de hello toosecure heure.

### <a name="sign-in-risk-security-policy"></a>Stratégie de sécurité en matière de risque à la connexion
Une stratégie de connexion risque est une stratégie d’accès conditionnel qui prend la valeur hello risque tooa spécifique connectez-vous et applique les limitations de risques selon les règles et conditions prédéfinies.

![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1014.png "Stratégie en matière de risque à la connexion")

Azure AD Identity Protection vous permet de gérer l’atténuation hello de connexions présentant un risque en vous permettant de :

* Définir hello utilisateurs et groupes hello une stratégie s’applique à :

    ![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1015.png "Stratégie en matière de risque à la connexion")
* Définissez hello connectez-vous risque seuil (faible, moyen ou élevé) qui déclenche la stratégie de hello :

    ![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1016.png "Stratégie en matière de risque à la connexion")
* Ensemble hello contrôles toobe appliquée au moment de la stratégie de hello déclenche :  

    ![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1017.png "Stratégie en matière de risque à la connexion")
* Basculer hello de votre stratégie :

    ![Inscription à MFA](./media/active-directory-identityprotection/403.png "Inscription à MFA")
* Passez en revue et évaluer l’impact de hello d’une modification avant son activation :

    ![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1018.png "Stratégie en matière de risque à la connexion")

#### <a name="what-you-need-tooknow"></a>Vous devez tooknow
Vous pouvez configurer une authentification multifacteur toorequire de stratégie de sécurité risque de connexion :

![Stratégie en matière de risque à la connexion](./media/active-directory-identityprotection/1017.png "Stratégie en matière de risque à la connexion")

Toutefois, pour des raisons de sécurité, ce paramètre s’applique uniquement aux utilisateurs qui ont déjà été inscrits pour l’authentification multifacteur. Si l’authentification multifacteur de hello condition toorequire est respectée pour un utilisateur qui n’est pas encore inscrit pour l’authentification multifacteur, l’utilisateur de hello est bloquée.

Comme meilleure pratique, si vous souhaitez que l’authentification multifacteur de toorequire pour les connexions présentant un risque, vous devez :

1. Activer hello [stratégie d’inscription de l’authentification multifacteur](#multi-factor-authentication-registration-policy) pourquoi les utilisateurs affectés.
2. Nécessitent hello affectées toologin d’utilisateurs dans une session non risqué de tooperform une inscription de l’authentification Multifacteur

Suivre ces étapes permet de s’assurer que l’authentification multifacteur est requise pour une connexion à risque.

#### <a name="best-practices"></a>Meilleures pratiques
Choix d’un **haute** seuil réduit le nombre de hello de fois où une stratégie est déclenchée et réduit hello impact toousers.  

Toutefois, il exclut **faible** et **support** connexions signalées pour le risque d’une stratégie de hello, qui peut ne pas bloque un attaquant d’exploiter une identité compromise.

Lorsque le paramètre hello stratégie,

* Excluez les utilisateurs qui ne sont pas inscrits/ne peuvent pas s’inscrire à l’authentification multifacteur.
* Excluez les utilisateurs dans les paramètres régionaux où l’activation de la stratégie de hello n’est pas pratique (par exemple, aucun toohelpdesk accès)
* Exclure les utilisateurs qui sont susceptibles de toogenerate un grand nombre de faux positifs (les développeurs et aux analystes en sécurité)
* Utilisez un niveau de risque **Élevé** pendant le déploiement initial de la stratégie ou si vous devez minimiser la complexité pour les utilisateurs finaux.
* Utilisez un niveau de risque **Faible** si votre organisation nécessite une sécurité accrue. La sélection d’un niveau de risque **Faible** complique la connexion pour les utilisateurs, mais renforce la sécurité.

Hello recommandé par défaut pour la plupart des organisations est tooconfigure une règle pour un **support** seuil toostrike un compromis entre facilité d’utilisation et de sécurité.

stratégie de connexion risque Hello est :

* Le trafic tooall appliqués et les connexions à l’aide de l’authentification moderne.
* Tooapplications pas appliquées à l’aide des protocoles de sécurité plus anciens en désactivant le point de terminaison WS-Trust de hello à IDP hello fédéré, tel qu’AD FS.

Hello **événements à risque** page hello Identity Protection console répertorie tous les événements :

* auxquels cette stratégie a été appliquée ;
* Vous pouvez consulter l’activité hello et déterminer si action de hello a appropriées ou non

Pour une vue d’ensemble de hello liée à l’expérience utilisateur, consultez :

* [Récupération de connexion à risque](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [Connexion à risque bloquée](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [Expériences de connexion avec Azure AD Identity Protection](active-directory-identityprotection-flows.md)  

**boîte de dialogue configuration associés tooopen hello**:

- Sur hello **Azure AD Identity Protection** panneau, Bonjour **configurer** , cliquez sur **stratégie d’authentification risque**.

    ![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1014.png "Stratégie en matière de risque des utilisateurs")



## <a name="users-flagged-for-risk"></a>Utilisateurs associés à un indicateur de risque

Active tous les [risque d’événements](active-directory-identity-protection-risk-events.md) qui ont été détectés par Azure Active Directory pour un utilisateur contribuent tooa concept logique appelée risque de l’utilisateur. Un utilisateur signalé comme présentant un risque indique qu’un compte d’utilisateur est susceptible d’avoir été compromis.

![Utilisateurs associés à un indicateur de risque](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a>Niveau de risque d’un utilisateur

Un niveau de risque d’utilisateur est une indication (haute, moyenne ou faible) de probabilité de hello que hello l’identité d’utilisateur a été compromise. Il est calculé en fonction d’événements à risque hello utilisateur associés à l’identité d’un utilisateur.

Hello état d’un événement à risque est **Active** ou **fermé**. Uniquement les événements qui sont des risques **Active** contribuent le calcul du niveau de risque toohello utilisateur.

niveau de risque utilisateur Hello est calculé à l’aide de hello suivant entrées :

* Événements risque actif ayant un impact sur les utilisateurs hello
* Niveau de risque de ces événements
* Application ou non de mesures de correction

![Risques des utilisateurs](./media/active-directory-identityprotection/1031.png "Risques des utilisateurs")

Vous pouvez utiliser hello utilisateur risque niveaux toocreate stratégies d’accès conditionnel qui empêche les utilisateurs de risques de se connecter, ou forcer les toosecurely modifier leur mot de passe.

### <a name="closing-risk-events-manually"></a>Fermeture manuelle des événements à risque

Dans la plupart des cas, vous prendra correctives telles que les événements de risque de fermer tooautomatically de réinitialisation de mot de passe sécurisé. Toutefois, il se peut que cela ne soit pas toujours possible.  
C’est par exemple, les cas de hello, lorsque :

* un utilisateur avec des événements à risque actifs a été supprimé ;
* Une enquête révèle qu’un événement à signalé risque a été effectuer par un utilisateur légitime de hello

Étant donné que les événements à risque qui sont **Active** calcul du toohello utilisateur risque de contribuer, vous avez peut-être toomanually réduire un niveau de risque en fermant les événements à risque manuellement.  
Au cours de hello d’enquête, vous pouvez choisir tootake ces état de hello toochange actions d’un événement à risque des :

![Actions](./media/active-directory-identityprotection/34.png "Actions")

* **Résoudre** - si après avoir examiné un événement à risque, vous avez une action de mise à jour appropriées en dehors de la Protection d’identité, et si vous pensez que l’événement hello risque doit être considérée comme fermée, l’événement de hello marque comme résolu. Événements résolus définira tooClosed d’état de l’événement hello risque et événements risque de hello n’est plus contribuera toouser risque.
* **Marquer comme faux positif** : dans certains cas, il se peut qu’un événement à risque soit signalé à tort en tant que tel. Pour réduire nombre hello de telles occurrences en marquant l’événement à risque hello comme faux positifs. Cela permet de classification de hello tooimprove algorithmes d’événements similaires Bonjour future d’apprentissage hello. état Hello d’événements de faux positifs est trop**fermé** et ils ne seront plus prises toouser risque.
* **Ignorer** : Si vous n’avez pas pris aucune action de mise à jour, mais hello risque événement toobe est supprimé de la liste active de hello, vous pouvez marquer un événement à risque ignorer et état de l’événement hello va être fermée. Événements ignorés ne contribuent pas toouser risque. Cette option doit uniquement être utilisée dans des circonstances inhabituelles.
* **Réactiver** -risque d’événements qui ont été fermées manuellement (en choisissant **résoudre**, **faux positif**, ou **ignorer**) peuvent être réactivés, paramètre hello statut de l’événement différé trop**Active**. Événements à risque réactivé contribuent calcul du niveau de risque toohello utilisateur. Les événements à risque fermés à l’aide d’une mesure de correction (telle qu’une réinitialisation de mot de passe sécurisée) ne peuvent pas être réactivés.

**boîte de dialogue configuration associés tooopen hello**:

1. Sur hello **Azure AD Identity Protection** panneau, sous **examiner**, cliquez sur **risque d’événements**.

    ![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1002.png "Réinitialisation manuelle du mot de passe")
2. Bonjour **risque d’événements** , cliquez sur un risque.

    ![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1003.png "Réinitialisation manuelle du mot de passe")
3. Dans Panneau de risques hello, cliquez sur un utilisateur.

    ![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1004.png "Réinitialisation manuelle du mot de passe")

### <a name="closing-all-risk-events-for-a-user-manually"></a>Fermeture manuelle de tous les événements à risque pour un utilisateur
Au lieu de fermeture manuellement individuellement d’événements à risque pour un utilisateur, Azure Active Directory Identity Protection vous donne également une méthode tooclose tous les événements pour un utilisateur avec un seul clic.

![Actions](./media/active-directory-identityprotection/2222.png "Actions")

Lorsque vous cliquez sur **ignorer tous les événements**, tous les événements sont fermés et hello affectée utilisateur n’est plus exposés.

### <a name="remediating-user-risk-events"></a>Correction des événements à risque d’un utilisateur

Une mise à jour est une toosecure action une identité ou un périphérique qui a été précédemment ou suspecté toobe compromis. Une action de mise à jour restaure l’état sans échec tooa hello identité ou l’appareil et résout les événements précédents risque associés hello identité ou d’appareil.

événements à risque tooremediate utilisateur, vous pouvez :

* Effectuer un mot de passe sécurisé tooremediate utilisateur risque les événements de réinitialisation manuelle
* Configurer un toomitigate de stratégie de sécurité utilisateur risque ou de corriger automatiquement les événements à risque utilisateur
* Une nouvelle image de périphérique de hello infecté  

#### <a name="manual-secure-password-reset"></a>Réinitialisation manuelle et sécurisée du mot de passe
Une réinitialisation de mot de passe sécurisé est une mise à jour efficace pour de nombreux événements risque et lors de l’exécution, ferme ces événements à risque et automatiquement recalcule le niveau de risque hello utilisateur. Vous pouvez utiliser hello Identity Protection du tableau de bord tooinitiate un mot de passe réinitialisé pour un utilisateur présentant un risque.

boîte de dialogue associée Hello fournit deux méthodes différentes tooreset un mot de passe :

**Réinitialisation du mot de passe** : sélectionnez **nécessitent hello utilisateur tooreset leur mot de passe** tooallow hello récupération tooself utilisateur si l’utilisateur de hello a inscrit pour l’authentification multifacteur. Lors de l’utilisateur hello suivant signe, utilisateur de hello sera requis toosolve stimulation avec succès d’une authentification multifacteur et mot de passe de hello toochange puis, forcé. Cette option n’est pas disponible si le compte d’utilisateur hello n’est pas déjà inscrit de l’authentification multifacteur.

**Mot de passe temporaire** : sélectionnez **générer un mot de passe temporaire** tooimmediately invalider le mot de passe existant hello et créer un nouveau mot de passe temporaire pour l’utilisateur de hello. Envoyer hello nouveau mot de passe temporaire tooan autre adresse de messagerie pour l’utilisateur de hello ou un responsable de l’utilisateur toohello. Parce que le mot de passe hello est temporaire, utilisateur de hello sera un mot de passe hello toochange demandées lors de l’authentification.

![Stratégie](./media/active-directory-identityprotection/1005.png "Stratégie")

**boîte de dialogue configuration associés tooopen hello**:

1. Sur hello **Azure AD Identity Protection** panneau, cliquez sur **utilisateurs marqués pour risque**.

    ![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1006.png "Réinitialisation manuelle du mot de passe")
2. Dans la liste hello des utilisateurs, sélectionnez un utilisateur au moins un risque.

    ![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1007.png "Réinitialisation manuelle du mot de passe")
3. Dans le panneau d’utilisateur hello, cliquez sur **réinitialisation de mot de passe**.

    ![Réinitialisation manuelle du mot de passe](./media/active-directory-identityprotection/1008.png "Réinitialisation manuelle du mot de passe")

### <a name="user-risk-security-policy"></a>Stratégie de sécurité en matière de risque des utilisateurs
Une stratégie de sécurité utilisateur risque est une stratégie d’accès conditionnel qui prend la valeur hello risque tooa au niveau utilisateur et applique les actions de mise à jour et d’atténuation selon les règles et conditions prédéfinies.

![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1009.png "Stratégie en matière de risque des utilisateurs")

Azure AD Identity Protection vous permet de gérer l’atténuation de hello et mise à jour des utilisateurs marquées pour risque par ce qui vous permet :

* Définir hello utilisateurs et groupes hello une stratégie s’applique à :

    ![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1010.png "Stratégie en matière de risque des utilisateurs")
* Définissez hello utilisateur risque seuil (faible, moyen ou élevé) qui déclenche la stratégie de hello :

    ![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1011.png "Stratégie en matière de risque des utilisateurs")
* Ensemble hello contrôles toobe appliquée au moment de la stratégie de hello déclenche :

    ![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1012.png "Stratégie en matière de risque des utilisateurs")
* Basculer hello de votre stratégie :

    ![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/403.png "Inscription à MFA")
* Passez en revue et évaluer l’impact de hello d’une modification avant son activation :

    ![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1013.png "Stratégie en matière de risque des utilisateurs")

Choix d’un **haute** seuil réduit le nombre de hello de fois où une stratégie est déclenchée et réduit hello impact toousers.
Toutefois, il exclut **faible** et **support** utilisateurs signalées pour le risque d’une stratégie de hello, qui ne peut pas sécuriser les identités ou les appareils qui ont été précédemment ou suspectées toobe compromis.

Lorsque le paramètre hello stratégie,

* Exclure les utilisateurs qui sont susceptibles de toogenerate un grand nombre de faux positifs (les développeurs et aux analystes en sécurité)
* Excluez les utilisateurs dans les paramètres régionaux où l’activation de la stratégie de hello n’est pas pratique (par exemple, aucun toohelpdesk accès)
* Utilisez un niveau de risque **Élevé** pendant le déploiement initial de la stratégie ou si vous devez minimiser la complexité pour les utilisateurs finaux.
* Utilisez un niveau de risque **Faible** si votre organisation nécessite une sécurité accrue. La sélection d’un niveau de risque **Faible** complique la connexion pour les utilisateurs, mais renforce la sécurité.

Hello recommandé par défaut pour la plupart des organisations est tooconfigure une règle pour un **support** seuil toostrike un compromis entre facilité d’utilisation et de sécurité.

Pour une vue d’ensemble de hello liée à l’expérience utilisateur, consultez :

* [Flux de récupération de compte compromis](active-directory-identityprotection-flows.md#compromised-account-recovery).  
* [Flux de compte compromis bloqué](active-directory-identityprotection-flows.md#compromised-account-blocked).  

**boîte de dialogue configuration associés tooopen hello**:

- Sur hello **Azure AD Identity Protection** panneau, Bonjour **configurer** , cliquez sur **stratégie des risques utilisateur**.

    ![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1009.png "Stratégie en matière de risque des utilisateurs")

### <a name="mitigating-user-risk-events"></a>Atténuation des événements à risque d’un utilisateur
Les administrateurs peuvent définir un utilisateur risque sécurité stratégie tooblock utilisateurs lors de l’authentification en fonction du niveau de risque hello.

Le blocage d’une connexion :

* Empêche la génération de nouveaux événements de risque d’utilisateur pour l’utilisateur de hello affectée hello
* Permet aux administrateurs toomanually corriger les événements à risque hello affectant l’identité de l’utilisateur hello et restaurez-la état sécurisé de tooa



## <a name="multi-factor-authentication-registration-policy"></a>Stratégie d’inscription à l’authentification multifacteur
L’authentification multifacteur Azure est une méthode de vérification qui vous sont qui nécessite l’utilisation de hello de plus qu’un nom d’utilisateur et le mot de passe. Il fournit une deuxième couche de sécurité toouser connexions et transactions.  
Nous vous recommandons d’exiger l’authentification multifacteur d’Azure des connexions des utilisateurs pour les raisons suivantes :

* Elle fournit une authentification renforcée avec un éventail d’options de vérification simples.
* Joue un rôle clé dans la préparation de votre organisation tooprotect et récupérer à partir de compromission du compte

![Stratégie en matière de risque des utilisateurs](./media/active-directory-identityprotection/1019.png "Stratégie en matière de risque des utilisateurs")

Pour plus d’informations, consultez [Qu’est-ce qu’Azure Multi-Factor Authentication ?](../multi-factor-authentication/multi-factor-authentication.md)

Azure AD Identity Protection vous permet de gérer la sortie hello d’enregistrement de l’authentification multifacteur en configurant une stratégie qui vous permet de :

* Définir hello utilisateurs et groupes hello une stratégie s’applique à :

    ![Stratégie MFA](./media/active-directory-identityprotection/1020.png "Stratégie MFA")
* Ensemble hello contrôles toobe appliquée au moment de la stratégie de hello déclenche ::  

    ![Stratégie MFA](./media/active-directory-identityprotection/1021.png "Stratégie MFA")
* Basculer hello de votre stratégie :

    ![Stratégie MFA](./media/active-directory-identityprotection/403.png "Stratégie MFA")
* Afficher l’état de l’enregistrement actuel hello :

    ![Stratégie MFA](./media/active-directory-identityprotection/1022.png "Stratégie MFA")

Pour une vue d’ensemble de hello liée à l’expérience utilisateur, consultez :

* [Processus d’inscription à l’authentification multifacteur](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).  
* [Expériences de connexion avec Azure AD Identity Protection](active-directory-identityprotection-flows.md).  

**boîte de dialogue configuration associés tooopen hello**:

- Sur hello **Azure AD Identity Protection** panneau, Bonjour **configurer** , cliquez sur **l’enregistrement de l’authentification multifacteur**.

    ![Stratégie MFA](./media/active-directory-identityprotection/1019.png "Stratégie MFA")

## <a name="next-steps"></a>Étapes suivantes
* [Channel 9 : Azure AD and Identity Show: Identity Protection Preview (Émission sur Azure AD et l’identité : présentation d’Identity Protection)](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [Activer Azure Active Directory Identity Protection](active-directory-identityprotection-enable.md)

* [Vulnérabilités détectées par Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md)

* [Événements à risque dans Azure Active Directory](active-directory-identity-protection-risk-events.md)

* [Notifications d’Azure Active Directory Identity Protection](active-directory-identityprotection-notifications.md)

* [Manuel d’Azure Active Directory Identity Protection](active-directory-identityprotection-playbook.md)

* [Glossaire d’Azure Active Directory Identity Protection](active-directory-identityprotection-glossary.md)

* [Expériences de connexion avec Azure AD Identity Protection](active-directory-identityprotection-flows.md)

* [Azure Active Directory Identity Protection - comment toounblock utilisateurs](active-directory-identityprotection-unblock-howto.md)

* [Prise en main d’Azure Active Directory Identity Protection et de Microsoft Graph](active-directory-identityprotection-graph-getting-started.md)
