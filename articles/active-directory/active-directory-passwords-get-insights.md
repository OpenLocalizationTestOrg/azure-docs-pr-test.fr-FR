---
title: "Obtention d’informations grâce aux rapports sur la gestion des mots de passe Azure AD | Microsoft Docs"
description: "Cet article décrit comment les rapports toouse tooget idée d’opérations de gestion de mot de passe de votre organisation."
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 1472b51d-53f4-4b0f-b1be-57f6fa88fa65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 90e0b8e621cdfe3e3a2f15df7b98115008855500
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-operational-insights-with-password-management-reports"></a>Comment les rapports tooget operational insights avec gestion de mot de passe
> [!IMPORTANT]
> **Rencontrez-vous des problèmes de connexion ?** Dans ce cas, [voici comment vous pouvez modifier et réinitialiser votre mot de passe](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
>
>

Cette section décrit comment vous pouvez utiliser Azure Active Directory tooview comment les utilisateurs sont à l’aide de réinitialisation de mot de passe et modifier dans votre organisation de rapports de gestion de mot de passe.

* [**Vue d’ensemble des rapports de gestion des mots de passe**](#overview-of-password-management-reports)
* [**Comment les rapports dans le nouveau portail de Azure hello gestion des mots de passe tooview**](#how-to-view-password-management-reports)
 * [Rôles d’annuaire autorisés tooread rapports](#directory-roles-allowed-to-read-reports)
* [**Libre service des types d’activité de gestion de mot de passe dans hello nouveau portail Azure.**](#self-service-password-management-activity-types)
 * [Blocage suite à la réinitialisation du mot de passe en libre-service](#activity-type-blocked-from-self-service-password-reset)
 * [Modification du mot de passe (libre-service)](#activity-type-change-password-self-service)
 * [Réinitialisation du mot de passe (par l’administrateur)](#activity-type-reset-password-by-admin)
 * [Modification du mot de passe (libre-service)](#activity-type-reset-password-self-service)
 * [Progression de l’activité du flux de réinitialisation du mot de passe en libre-service](#activity-type-self-serve-password-reset-flow-activity-progress)
 * [Déverrouillage du compte d’utilisateur (libre-service)](#activity-type-unlock-user-account-self-service)
 * [Utilisateur inscrit pour la réinitialisation du mot de passe en libre-service](#activity-type-user-registered-for-self-service-password-reset)
* [**Comment les événements de gestion de mot de passe tooretrieve à partir de hello API Azure AD rapports et événements**](#how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api)
 * [Création de rapport sur les limitations de récupération des données API](#reporting-api-data-retrieval-limitations)
* [**Comment les événements d’enregistrement rapidement avec PowerShell de réinitialisation de mot de passe toodownload**](#how-to-download-password-reset-registration-events-quickly-with-powershell)
* [**La gestion des mots de passe tooview signale dans le portail classique de hello**](#how-to-view-password-management-reports-in-the-classic-portal)
* [**Réinitialisation de vue activité d’inscription de votre organisation dans le portail classique de hello**](#view-password-reset-registration-activity-in-the-classic-portal)
* [**Activité de votre organisation dans le portail classique de hello de réinitialisation de mot de passe de vue**](#view-password-reset-activity-in-the-classic-portal)


## <a name="overview-of-password-management-reports"></a>Vue d’ensemble des rapports de gestion des mots de passe
Une fois que vous déployez la réinitialisation de mot de passe, une des étapes courantes hello est toosee comment il est utilisé dans votre organisation.  Par exemple, vous souhaiterez peut-être tooget insight dans la façon dont les utilisateurs s’inscrivent pour la réinitialisation du mot de passe ou combien de mot de passe réinitialise ont été effectuées hello quelques jours.  Voici quelques-unes des questions courantes hello que vous serez en mesure de tooanswer avec les rapports de gestion de mot de passe de hello qui existent dans hello [portail de gestion Azure](https://manage.windowsazure.com) aujourd'hui :

* Combien de personnes se sont inscrites pour la réinitialisation des mots de passe ?
* Qui s’est inscrit pour la réinitialisation des mots de passe ?
* Quelles sont les données inscrites par ces personnes ?
* Combien de personnes réinitialiser leurs mots de passe Bonjour ces 7 derniers jours ?
* Quels sont les utilisateurs des méthodes courantes de hello ou les administrateurs tooreset leurs mots de passe ?
* Quelles sont courantes de problèmes face aux utilisateurs ou administrateurs lors de la tentative de réinitialisation de mot de passe toouse ?
* Quels sont les administrateurs qui réinitialisent fréquemment leurs mots de passe ?
* Y a-t-il des activités suspectes en rapport avec la réinitialisation des mots de passe ?

## <a name="how-tooview-password-management-reports"></a>Comment les rapports de gestion de mot de passe tooview
Bonjour nouvelle [portail Azure](https://portal.azure.com) expérience, nous avoir une méthode améliorée pour le tooview mot de passe mot de passe et de réinitialisation réinitialisation d’inscription activité.  Suivez les étapes ci-dessous passe et de réinitialisation de mot de passe toofind hello hello réinitialiser les événements d’enregistrement Bonjour nouvelle [portail Azure](https://portal.azure.com):

1. Accédez trop[**portal.azure.com**](https://portal.azure.com)
2. Cliquez sur hello **davantage de services** menu de navigation de gauche hello principal portail Azure
3. Recherchez **Azure Active Directory** hello la liste des services et le sélectionner dans
4. Cliquez sur **utilisateurs et groupes** à partir du menu de navigation hello Azure Active Directory
5. Cliquez sur hello **les journaux d’Audit** élément de navigation à partir du menu de navigation des utilisateurs et groupes hello. Vous découvrirez tous hello se produise les événements d’audit par rapport à tous les utilisateurs de hello dans votre annuaire. Tous les hello mot de passe événements associés, ainsi, vous pouvez filtrer toosee de cette vue.
6. toofilter relatives de cette gestion de mot de passe d’affichage tooonly hello événements, cliquez sur hello **filtre** bouton en haut de hello du panneau des hello.
7. À partir de hello **filtre** menu, sélectionnez hello **catégorie** liste déroulante et modifiez-le toohello **gestion de mot de passe libre-service** type de catégorie.
8. Liste de hello filtre supplémentaire si vous le souhaitez en choisissant hello spécifiques **activité** vous intéressez
### <a name="direct-link-toouser-audit-blade"></a>Panneau de lien direct tooUser d’Audit
Si vous êtes connecté dans le portail de tooyour, Voici un panneau d’audit de lien direct toohello utilisateur où vous pouvez consulter ces événements :

* [Atteindre la vue de l’audit toouser gestion directement](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit)

### <a name="directory-roles-allowed-tooread-reports"></a>Rôles d’annuaire autorisé tooread rapports
Actuellement, hello rôles d’annuaire suivantes peuvent lire les rapports de gestion des mots de passe Azure AD dans le portail Azure classic de hello :

* Administrateur général

Avant d’être en mesure de tooread ces rapports, un administrateur global dans la société de hello doit avoir choisi de pour cette toobe données récupérée pour le compte d’organisation de hello en visitant hello reporting au moins une fois les journaux de tabulation ou d’audit. Sans cela, les données ne sont pas collectées pour votre entreprise.

tooread d’informations sur les rôles d’annuaire et qu’ils peuvent font, consultez [attribution de rôles d’administrateur dans Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-assign-admin-roles).

## <a name="self-service-password-management-activity-types"></a>Types d’activités de gestion des mots de passe en libre-service
Hello, les types d’activité suivants s’affichent dans hello **gestion de mot de passe libre-service** catégorie d’événement d’audit.  Ces types d’activité sont décrits ci-dessous.

* [**Bloqué à partir de la réinitialisation de mot de passe libre-service** ](#activity-type-blocked-from-self-service-password-reset) -indique un utilisateur a essayé de tooreset un mot de passe, utilisez un opérateur spécifique, ou valider un numéro de téléphone de plus de 5 fois total des dernières 24 heures.
* [**Modifier le mot de passe (libre-service)** ](#activity-type-change-password-self-service) -indique un utilisateur effectuée facultatives ou forcé (tooexpiry échéance) modification du mot de passe.
* [**Réinitialisation du mot de passe (admin)** ](#activity-type-reset-password-by-admin) -indique un administrateur a effectué un mot de passe réinitialisé pour le compte d’un utilisateur à partir de hello portail Azure.
* [**Réinitialisation de mot de passe (libre-service)** ](#activity-type-reset-password-self-service) -indique un utilisateur a été réinitialisé son mot de passe à partir de hello [portail de réinitialisation du mot de passe Azure AD](https://passwordreset.microsoftonline.com).
* [**Mot de passe libre-service réinitialiser la progression des activités de flux** ](#activity-type-self-serve-password-reset-flow-activity-progress) -indique de chaque étape spécifique, un utilisateur parcoure (comme un mot de passe spécifiques de réinitialiser la porte d’authentification) dans le cadre d’un mot de passe hello réinitialisation des processus.
* [**Déverrouillage de compte d’utilisateur (libre-service)** ](#activity-type-unlock-user-account-self-service) -indique un utilisateur a correctement déverrouillé son compte Active Directory sans réinitialiser son mot de passe à partir de hello [portail de réinitialisation du mot de passe Azure AD](https://passwordreset.microsoftonline.com) à l’aide de hello [déverrouillage de compte Active Directory sans réinitialiser](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) fonctionnalité.
* [**L’utilisateur a inscrit pour la réinitialisation du mot de passe libre-service** ](#activity-type-user-registered-for-self-service-password-reset) -indique un utilisateur a inscrit tous les tooreset en mesure de hello requis informations toobe son mot de passe respecte la stratégie de réinitialisation du mot de passe hello actuellement spécifié par le client.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>Type d’activité : Blocked from self-service password reset (Blocage suite à la réinitialisation du mot de passe en libre-service)
Hello suivant liste explique cette activité en détail :

* **Description de l’activité** – indique un utilisateur a tenté de tooreset un mot de passe, utilisez un opérateur spécifique ou valider un numéro de téléphone de plus de 5 fois total des dernières 24 heures.
* **Activité acteur** -utilisateur hello qui a été limitée à partir de l’exécution d’autres opérations de réinitialisation. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **Cible de l’activité** -utilisateur hello qui a été limitée à partir de l’exécution d’autres opérations de réinitialisation. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **États d’activité autorisés**
 * _Réussite_ -indique un utilisateur a été limité d’effectuer des réinitialisations supplémentaires, essayez les méthodes d’authentification supplémentaires, ou valider les numéros de téléphone supplémentaires pour hello pendant les 24 heures.
* **Activity Status Failure Reason** (Motif de l’état d’activité Failure) : non applicable

### <a name="activity-type-change-password-self-service"></a>Type d’activité : Change password (self-service) (Modification du mot de passe (libre-service))
Hello suivant liste explique cette activité en détail :

* **Description de l’activité** – indique un utilisateur effectuée facultatives ou forcé (tooexpiry échéance) modification du mot de passe.
* **Activité acteur** -utilisateur hello qui a modifié son mot de passe. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **Cible de l’activité** -utilisateur hello qui a modifié son mot de passe. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **États d’activité autorisés**
 * _Success_ : indique qu’un utilisateur a modifié son mot de passe avec succès
 * _Échec de_ -indique un échec de l’utilisateur toochange son mot de passe. En cliquant sur la ligne de hello vous permettra de toosee hello **raison de l’état activité** toolearn catégorie plus d’informations sur la cause de l’échec de hello.
* **Activity Status Failure Reason** - (Motif de l’état d’activité Failure)
 * _FuzzyPolicyViolationInvalidPassword_ -hello sélectionnés utilisateur un mot de passe qui a été automatiquement exclu (e) en raison des capacités d’interdit la détection de mot de passe de tooMicrosoft recherche toobe trop courant ou particulièrement faible.

### <a name="activity-type-reset-password-by-admin"></a>Type d’activité : Reset password (by admin) (Réinitialisation du mot de passe (par l’administrateur))
Hello suivant liste explique cette activité en détail :

* **Description de l’activité** – indique un administrateur a effectué un mot de passe réinitialisé pour le compte d’un utilisateur à partir de hello portail Azure.
* **Activité acteur** -administrateur hello qui a exécuté le mot de passe de hello réinitialisé pour le compte d’utilisateur final ou un administrateur. Doit être un administrateur global, un administrateur de mot de passe, administrateur de l’utilisateur ou un administrateur du support technique.
* **Cible de l’activité** -utilisateur hello dont un mot de passe a été réinitialisé. Il peut s’agir d’un utilisateur final ou d’un autre administrateur.
* **États d’activité autorisés**
 * _Success_ : indique qu’un administrateur a correctement réinitialisé un mot de passe d’utilisateur
 * _Échec de_ -indique un échec de l’administrateur toochange un mot de passe. En cliquant sur la ligne de hello vous permettra de toosee hello **raison de l’état activité** toolearn catégorie plus d’informations sur la cause de l’échec de hello.

### <a name="activity-type-reset-password-self-service"></a>Type d’activité : Reset password (self-service) (Réinitialisation du mot de passe (libre-service))
Hello suivant liste explique cette activité en détail :

* **Description de l’activité** – indique un utilisateur a été réinitialisé son mot de passe à partir de hello [portail de réinitialisation du mot de passe Azure AD](https://passwordreset.microsoftonline.com).
* **Activité acteur** -utilisateur hello réinitialiser son mot de passe. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **Cible de l’activité** -utilisateur hello réinitialiser son mot de passe. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **États d’activité autorisés**
 * _Success_ : indique qu’un utilisateur a correctement réinitialisé son propre mot de passe
 * _Échec de_ -indique un échec de l’utilisateur tooreset son propre mot de passe. En cliquant sur la ligne de hello vous permettra de toosee hello **raison de l’état activité** toolearn catégorie plus d’informations sur la cause de l’échec de hello.
* **Activity Status Failure Reason** - (Motif de l’état d’activité Failure)
 * _FuzzyPolicyViolationInvalidPassword_ -administrateur de hello a sélectionné un mot de passe qui a été automatiquement exclu (e) en raison des capacités d’interdit la détection de mot de passe de tooMicrosoft recherche toobe trop courant ou particulièrement faible.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Type d’activité : Self serve password reset flow activity progress (Progression de l’activité du flux de réinitialisation du mot de passe en libre-service)
Hello suivant liste explique cette activité en détail :

* **Description de l’activité** – indique chaque étape spécifique, un utilisateur parcoure (comme un mot de passe spécifiques de réinitialiser la porte d’authentification) dans le cadre d’un mot de passe hello réinitialisation des processus.
* **Activité acteur** -hello l’utilisateur qui a effectué une partie de mot de passe hello réinitialisé flux. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **Cible de l’activité** -hello l’utilisateur qui a effectué une partie de mot de passe hello réinitialisé flux. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **États d’activité autorisés**
 * _Réussite_ -indique un utilisateur terminé avec succès une étape spécifique du flux de réinitialisation de mot de passe hello.
 * _Échec de_ -indique une étape spécifique d’un mot de passe hello réinitialisé flux a échoué. En cliquant sur la ligne de hello vous permettra de toosee hello **raison de l’état activité** toolearn catégorie plus d’informations sur la cause de l’échec de hello.
* **Motifs des états d’activité autorisés**
 * Voir le tableau ci-dessous pour [tous les motifs d’état d’activité de réinitialisation du mot de passe autorisés](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Type d’activité : Unlock user account (self-service) (Déverrouillage du compte d’utilisateur (libre-service))
Hello suivant liste explique cette activité en détail :

* **Description de l’activité** – indique un utilisateur a correctement déverrouillé son compte Active Directory sans réinitialiser son mot de passe à partir de hello [portail de réinitialisation du mot de passe Azure AD](https://passwordreset.microsoftonline.com) à l’aide de hello [AD déverrouillage de compte sans réinitialiser](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) fonctionnalité.
* **Activité acteur** -utilisateur hello déverrouillé son compte sans réinitialiser leur mot de passe. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **Cible de l’activité** -utilisateur hello déverrouillé son compte sans réinitialiser leur mot de passe. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **États d’activité autorisés**
 * _Success_ : indique qu’un utilisateur a correctement déverrouillé son propre compte
 * _Échec de_ -indique un échec de l’utilisateur toounlock son compte. En cliquant sur la ligne de hello vous permettra de toosee hello **raison de l’état activité** toolearn catégorie plus d’informations sur la cause de l’échec de hello.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Type d’activité : User registered for self-service password reset (Utilisateur inscrit pour la réinitialisation du mot de passe libre-service)
Hello suivant liste explique cette activité en détail :

* **Description de l’activité** – indique un utilisateur a inscrit tous les tooreset en mesure de hello requis informations toobe son mot de passe respecte la stratégie de réinitialisation du mot de passe hello actuellement spécifié par le client.
* **Activité acteur** -utilisateur hello qui se sont inscrits pour la réinitialisation du mot de passe. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **Cible de l’activité** -utilisateur hello qui se sont inscrits pour la réinitialisation du mot de passe. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **États d’activité autorisés**
 * _Réussite_ -indique un utilisateur inscrit pour le mot de passe réinitialisé conformément à la stratégie actuelle hello.
 * _Échec de_ -indique un tooregister utilisateur a échoué pour la réinitialisation du mot de passe. En cliquant sur la ligne de hello vous permettra de toosee hello **raison de l’état activité** toolearn catégorie plus d’informations sur la cause de l’échec de hello. Remarque : cela ne signifie pas un utilisateur est tooreset n’a pas pu son propre mot de passe, simplement qu’il ou elle n’a pas terminé de processus d’inscription de hello. S’il existe des données non vérifiées sur leur compte est correcte (par exemple, un numéro de téléphone qui n’est pas validé), même si elles n’ont pas vérifié ce numéro de téléphone, ils peuvent encore l’utiliser tooreset leur mot de passe. Pour plus d’informations, consultez [Que se passe-t-il lorsqu’un utilisateur s’inscrit ?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>Comment les événements de gestion de mot de passe tooretrieve à partir de hello API Azure AD rapports et événements
Depuis août 2015, hello AD Azure API rapports et événements prend désormais en charge la récupération de toutes les informations de hello incluses dans les rapports par mot de passe hello réinitialisation et de mot de passe d’inscription de réinitialisation. À l’aide de cette API, vous pouvez télécharger la réinitialisation de mot de passe individuelles et mot de passe réinitialisé les événements d’enregistrement pour l’intégration avec hello technologiques de votre choce de création de rapports.

### <a name="how-tooget-started-with-hello-reporting-api"></a>Comment tooget démarrer avec hello API de création de rapports
tooaccess ces données, vous devez toowrite une petite application ou script tooretrieve à partir de nos serveurs. [Découvrez comment tooget main hello API de création de rapports AD Azure](active-directory-reporting-api-getting-started.md).

Une fois que vous avez un script de travail, vous pouvez ensuite répondre tooexamine hello mot de passe d’inscription et de réinitialisation événements que vous pouvez récupérer toomeet vos scénarios.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): répertorie les colonnes hello disponibles pour les événements de réinitialisation de mot de passe
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): répertorie les colonnes hello disponibles pour les événements de l’inscription de réinitialisation de mot de passe

### <a name="reporting-api-data-retrieval-limitations"></a>Création de rapport sur les limitations de récupération des données API
Actuellement, hello rapports Azure AD et API d’événements récupère les trop**75 000 événements individuels** Hello [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) et [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) types , la répartition hello **30 derniers jours**.

Si vous avez besoin de tooretrieve ou stockez des données au-delà de cette fenêtre, nous vous suggérons de sa conservation dans une base de données externe et à l’aide des deltas hello hello API tooquery résultant. Une meilleure pratique est toobegin la récupération de ces données lorsque vous démarrez votre mot de passe réinitialiser le processus d’inscription de votre organisation, rendre persistant en externe, puis continue deltas de hello tootrack à partir de ce point.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>Comment les événements d’enregistrement rapidement avec PowerShell de réinitialisation de mot de passe toodownload
En outre toousing Bonjour Azure AD API rapports et événements directement, vous pouvez également utiliser hello ci-dessous les événements de l’inscription de toorecent de script PowerShell dans votre annuaire. Cela est utile dans le cas toosee qui a inscrit récemment ou souhaitez tooensure que votre mot de passe réinitialisé déploiement se produit comme prévu.

* [Script PowerShell d’activité d’inscription SSPR Azure AD](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

## <a name="how-tooview-password-management-reports-in-hello-classic-portal"></a>La gestion des mots de passe tooview signale dans le portail classique de hello
rapports de gestion des mots de passe toofind hello, suivez les étapes de hello ci-dessous :

1. Cliquez sur hello **Active Directory** extension Bonjour [portail Azure classic](https://manage.windowsazure.com).
2. Sélectionnez votre annuaire à partir de la liste de hello qui s’affiche dans le portail de hello.
3. Cliquez sur hello **rapports** onglet.
4. Regardez sous hello **journaux d’activité** section.
5. Sélectionnez soit hello **activité de réinitialisation de mot de passe** rapport ou hello **activité de l’inscription de réinitialisation de mot de passe** rapport.

## <a name="view-password-reset-registration-activity-in-hello-classic-portal"></a>Réinitialisation de vue activité d’inscription dans le portail classique de hello
rapport d’activité d’enregistrement réinitialisation Hello mot de passe montre le que mot de passe toutes les inscriptions de réinitialisation qui se sont produites dans votre organisation.  Une inscription de réinitialisation de mot de passe s’affiche dans ce rapport pour tout utilisateur qui a été correctement inscrit les informations d’authentification au mot de passe hello portail d’inscription de réinitialisation ([http://aka.ms/ssprsetup](http://aka.ms/ssprsetup)).

* **Période max** : 30 jours
* **Nombre max de lignes** : 75 000
* **Téléchargeable**: Oui, via un fichier CSV

### <a name="description-of-report-columns"></a>Description des colonnes du rapport
Hello liste suivante décrit chacune des colonnes du rapport hello en détail :

* **Utilisateur** – hello l’utilisateur ayant tenté d’effectuer un mot de passe réinitialisé opération d’inscription.
* **Rôle** – rôle hello d’utilisateur hello dans le répertoire de hello.
* **Date et heure** : hello date et heure de la tentative de hello.
* **Données inscrites** – l’inscription de réinitialisation quelles authentification données hello fourni par l’utilisateur au cours de mot de passe.

### <a name="description-of-report-values"></a>Description des valeurs du rapport
Hello tableau suivant décrit hello différentes valeurs autorisées pour chaque colonne :

| Colonne | Valeurs autorisées et leur signification |
| --- | --- |
| Données inscrites |**Autre adresse de messagerie** – utilisateur utilisé autre adresse de messagerie ou l’authentification par courrier électronique tooauthenticate<p><p>**Téléphone de bureau**– utilisateur utilisé office phone tooauthenticate<p>**Téléphone mobile** -utilisateur utilisé tooauthenticate de téléphone téléphone mobile ou de l’authentification<p>**Les Questions de sécurité** – tooauthenticate de questions de sécurité de l’utilisateur utilisées<p>**N’importe quelle combinaison de hello ci-dessus (par exemple, autre adresse de messagerie + téléphone portable)** – se produit lorsqu’une stratégie 2 porte est spécifiée et montre les deux méthodes hello utilisateur utilisé tooauthentication demande de réinitialisation de son mot de passe. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>Activité dans le portail classique de hello de réinitialisation de mot de passe de vue
Ce rapport montre toutes les tentatives de réinitialisation de mot de passe qui se sont produites dans votre organisation.

* **Période max** : 30 jours
* **Nombre max de lignes** : 75 000
* **Téléchargeable**: Oui, via un fichier CSV

### <a name="description-of-report-columns"></a>Description des colonnes du rapport
Hello liste suivante décrit chacune des colonnes du rapport hello en détail :

1. **Utilisateur** – hello l’utilisateur ayant tenté d’effectuer un mot de passe réinitialisé opération (basée sur le champ d’ID d’utilisateur hello fourni lorsque l’utilisateur de hello prend tooreset un mot de passe).
2. **Rôle** – rôle hello d’utilisateur hello dans le répertoire de hello.
3. **Date et heure** : hello date et heure de la tentative de hello.
4. **Ou les méthodes utilisées** : les méthodes d’authentification hello utilisateur utilisé pour cette opération de réinitialisation.
5. **Résultat** – opération de réinitialisation du résultat final de hello du mot de passe hello.
6. **Détails** – hello les détails de la réinitialisation de mot de passe hello pourquoi a entraîné valeur hello il l’a fait.  Inclut également les étapes d’atténuation que vous pouvez adopter tooresolve une erreur inattendue.

### <a name="description-of-report-values"></a>Description des valeurs du rapport
Hello tableau suivant décrit hello différentes valeurs autorisées pour chaque colonne :

| Colonne | Valeurs autorisées et leur signification |
| --- | --- |
| Méthodes utilisées |**Autre adresse de messagerie** – utilisateur utilisé autre adresse de messagerie ou l’authentification par courrier électronique tooauthenticate<p>**Téléphone de bureau** – utilisateur utilisé office phone tooauthenticate<p>**Téléphone mobile** – utilisateur utilisé tooauthenticate de téléphone téléphone mobile ou de l’authentification<p>**Les Questions de sécurité** – tooauthenticate de questions de sécurité de l’utilisateur utilisées<p>**N’importe quelle combinaison de hello ci-dessus (par exemple, autre adresse de messagerie + téléphone portable)** – se produit lorsqu’une stratégie 2 porte est spécifiée et montre les deux méthodes hello utilisateur utilisé tooauthentication demande de réinitialisation de son mot de passe. |
| Résultat |**Abandonné** : l’utilisateur a démarré la réinitialisation de mot de passe, puis s’est arrêté à mi-chemin sans terminer<p>**Bloqué** : compte d’utilisateur a été toouse a empêché le mot de passe réinitialisé en raison de la page de réinitialisation de mot de passe tooattempting toouse hello ou méthode de réinitialisation de mot de passe trop de fois dans une période de 24 heures<p>**Annulé** – utilisateur a démarré la réinitialisation de mot de passe, mais vous cliquez sur la session de hello toocancel cours de hello Annuler bouton <p>**Contacter l’administrateur** – utilisateur a un problème lors de sa session qu’il n’a pas pu résoudre, afin de l’utilisateur de la hello a cliqué sur le lien « Contactez votre administrateur » de hello au lieu de la fin de flux de réinitialisation de mot de passe hello<p>**Échec de** – utilisateur n’a pas pu tooreset un mot de passe, probablement parce que l’utilisateur de hello était pas configuré toouse hello fonctionnalité (par exemple, aucune licence, pas les informations d’authentification, un mot de passe géré localement mais écriture différée n’est désactivée).<p>**Réussi** : la réinitialisation du mot de passe a réussi. |
| Détails |Voir le tableau ci-dessous |

### <a name="allowed-values-for-details-column"></a>Valeurs autorisées pour la colonne Détails
Vous trouverez ci-dessous la liste de hello de types de résultats que vous pouvez attendre lors de l’aide du mot de passe hello activité de réinitialisation :

| Détails | Type de résultat |
| --- | --- |
| Utilisateur a abandonné après avoir effectué l’option de vérification du courrier électronique hello |Abandonné |
| Utilisateur a abandonné après avoir effectué l’option de vérification par SMS hello mobile |Abandonné |
| Utilisateur a abandonné après avoir effectué l’option de vérification par appel vocal sur mobile hello |Abandonné |
| Utilisateur a abandonné après avoir effectué l’option de vérification par appel vocal hello office |Abandonné |
| Utilisateur a abandonné après avoir effectué l’option de questions de sécurité hello |Abandonné |
| L’utilisateur a abandonné après avoir entré son ID utilisateur. |Abandonné |
| Utilisateur a abandonné après avoir commencé l’option de vérification du courrier électronique hello |Abandonné |
| Utilisateur a abandonné après avoir commencé l’option de vérification par SMS hello mobile |Abandonné |
| Utilisateur a abandonné après avoir commencé l’option de vérification par appel vocal sur mobile hello |Abandonné |
| Utilisateur a abandonné après avoir commencé l’option de vérification par appel vocal hello office |Abandonné |
| Utilisateur a abandonné après avoir commencé l’option de questions de sécurité hello |Abandonné |
| L’utilisateur a abandonné avant de choisir un nouveau mot de passe. |Abandonné |
| L’utilisateur a abandonné lors du choix d’un nouveau mot de passe. |Abandonné |
| L’utilisateur a entré un trop grand nombre de codes de vérification par SMS non valides et est bloqué pour 24 heures. |Bloqué |
| L’utilisateur a tenté un trop grand nombre de fois la vérification de la voix par appel sur mobile et est bloqué pour 24 heures. |Bloqué |
| L’utilisateur a tenté un trop grand nombre de fois la vérification de la voix par appel au bureau et est bloqué pour 24 heures. |Bloqué |
| Utilisateur a tenté de questions de sécurité tooanswer trop de fois et qu’il est bloqué pour 24 heures |Bloqué |
| Utilisateur a tenté de tooverify un numéro de téléphone trop de fois et qu’il est bloqué pour 24 heures |Bloqué |
| L’utilisateur a abandonné avant de passer des méthodes d’authentification hello requis |Annulé |
| L’utilisateur a abandonné avant de soumettre un nouveau mot de passe. |Annulé |
| L’utilisateur a contacté un administrateur après avoir essayé l’option de vérification du courrier électronique hello |Administrateur contacté |
| L’utilisateur a contacté un administrateur après avoir essayé l’option de vérification par SMS hello mobile |Administrateur contacté |
| L’utilisateur a contacté un administrateur après avoir essayé l’option de vérification par appel vocal sur mobile hello |Administrateur contacté |
| L’utilisateur a contacté un administrateur après avoir essayé l’option de vérification par appel vocal hello office |Administrateur contacté |
| L’utilisateur a contacté un administrateur après avoir essayé l’option de vérification de question de sécurité hello |Administrateur contacté |
| La réinitialisation du mot de passe n’est pas activée pour cet utilisateur. Activer le mot de passe réinitialisé sous hello onglet tooresolve cette configuration |Échec |
| L’utilisateur n’a pas de licence. Vous pouvez ajouter un tooresolve d’utilisateur licence toohello cela |Échec |
| L’utilisateur a essayé de tooreset à partir d’un appareil sans cookies sont activés |Échec |
| Un nombre insuffisant de méthodes d’authentification sont définies pour le compte de l’utilisateur. Ajouter tooresolve des informations d’authentification |Échec |
| Le mot de passe de l’utilisateur est géré localement. Vous pouvez activer l’écriture différée de mot de passe tooresolve cette |Échec |
| Nous n’avons pas pu accéder au service de réinitialisation de votre mot de passe local. Vérifiez le journal des événements de votre ordinateur synchronisé. |Échec |
| Nous avons rencontré un problème lors de la réinitialisation de mot de passe local de l’utilisateur hello. Vérifiez le journal des événements de votre ordinateur synchronisé. |Échec |
| Cet utilisateur n’est pas membre du groupe utilisateurs de réinitialisation de mot de passe hello. Ajouter cette tooresolve de groupe utilisateur toothat. |Échec |
| La réinitialisation du mot de passe a été désactivée pour ce locataire. Consultez [ici](http://aka.ms/ssprtroubleshoot) tooresolve cela. |Échec |
| L’utilisateur a réinitialisé le mot de passe. |Réussi |

## <a name="next-steps"></a>Étapes suivantes
Voici les pages de documentation de réinitialisation de mot de passe Azure AD tooall liens Hello :

* **Rencontrez-vous des problèmes de connexion ?** Dans ce cas, [voici comment vous pouvez modifier et réinitialiser votre mot de passe](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
* [**Son fonctionnement** ](active-directory-passwords-how-it-works.md) -Découvrez hello six différents composants de service de hello et que chacun est
* [**Mise en route** ](active-directory-passwords-getting-started.md) -en savoir comment tooallow vous tooreset d’utilisateurs et modifier leurs mots de passe cloud ou local
* [**Personnaliser** ](active-directory-passwords-customize.md) - en savoir l’aspect que toocustomize hello & apparence et comportement de hello tooyour besoins du service
* [**Meilleures pratiques** ](active-directory-passwords-best-practices.md) -Découvrez comment tooquickly déployer et gérer efficacement les mots de passe de votre organisation
* [**Forum aux questions** ](active-directory-passwords-faq.md) -obtenir des réponses aux questions d’elles sonttrop
* [**Résolution des problèmes** ](active-directory-passwords-troubleshoot.md) -en savoir comment tooquickly résoudre les problèmes avec le service de hello
* [**En savoir plus** ](active-directory-passwords-learn-more.md) - accédez en profondeur des détails techniques hello de fonctionnement du service hello
