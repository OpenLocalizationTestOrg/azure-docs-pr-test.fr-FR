---
title: "Rapport : réinitialisation de mot de passe en libre-service Azure AD | Microsoft Docs"
description: "Rapports sur les événements de réinitialisation de mot de passe en libre-service Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: af65b9be1e00c2819431694a5b0064b97b9e1867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-options-for-azure-ad-password-management"></a>Options de création de rapports pour la gestion des mots de passe Azure AD

Après le déploiement de nombreuses organisations souhaitent tooknow comment ou si SSPR est réellement utilisé. Azure AD fournit les fonctionnalités de création de rapports qui vous aident à tooanswer les questions en conserve des rapports et si vous possédez les licences appropriées, vous toocreate des requêtes personnalisées.

Hello suivantes peuvent répondre à certaines questions par les rapports qui existent dans hello [Azure portal] (https://portal.azure.com/).

> [!NOTE]
> Vous devez être [un administrateur global](active-directory-assign-admin-roles.md#assign-or-remove-administrator-roles) et devez opter pour ce toobe des données collectées pour le compte de votre organisation, par visite hello reporting onglet ou audit se connecte au moins une fois. Sans cela, les données ne sont pas collectées pour votre entreprise

* Combien de personnes se sont inscrites pour la réinitialisation des mots de passe ?
* Qui s’est inscrit pour la réinitialisation des mots de passe ?
* Quelles sont les données inscrites par ces personnes ?
* Combien de personnes réinitialiser leurs mots de passe Bonjour sept derniers jours ?
* Quels sont les utilisateurs des méthodes courantes de hello ou les administrateurs tooreset leurs mots de passe ?
* Quelles sont courantes de problèmes face aux utilisateurs ou administrateurs lors de la tentative de réinitialisation de mot de passe toouse ?
* Quels sont les administrateurs qui réinitialisent fréquemment leurs mots de passe ?
* Y a-t-il des activités suspectes en rapport avec la réinitialisation des mots de passe ?

## <a name="how-tooview-password-management-reports-in-hello-azure-portal"></a>La gestion des mots de passe tooview signale Bonjour portail Azure

Bonjour expérience du portail Azure, nous avons une méthode améliorée tooview mot de passe réinitialisation et mot de passe d’inscription activité de réinitialisation.  Suivez les étapes de hello ci-dessous toofind hello mot de passe réinitialisation et mot de passe d’inscription les événements de réinitialisation :

1. Accédez trop[**portal.azure.com**](https://portal.azure.com)
2. Cliquez sur hello **davantage de services** menu hello principal Azure portail navigation de gauche
3. Recherchez **Azure Active Directory** hello la liste des services et le sélectionner dans
4. Cliquez sur **utilisateurs et groupes** à partir du menu de navigation hello Azure Active Directory
5. Cliquez sur hello **les journaux d’Audit** élément de navigation à partir du menu de navigation des utilisateurs et groupes hello. Cela présente tous les événements d’audit de hello qui se produisent sur tous les utilisateurs de hello dans votre annuaire. Tous les hello mot de passe événements associés, ainsi, vous pouvez filtrer toosee de cette vue.
6. toofilter ce mot de passe de vue tooonly hello réinitialiser des événements connexes, cliquez sur hello **filtre** bouton en haut de hello du panneau des hello.
7. À partir de hello **filtre** menu, sélectionnez hello **catégorie** liste déroulante et modifiez-le toohello **gestion de mot de passe libre-service** type de catégorie.
8. Liste de hello filtre supplémentaire si vous le souhaitez en choisissant hello spécifiques **activité** vous intéressez

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>Comment les événements de gestion de mot de passe tooretrieve à partir de hello API Azure AD rapports et événements

Hello AD Azure API rapports et événements prend en charge de la récupération de toutes les informations de hello incluses dans les rapports de d’enregistrement réinitialisation du mot de passe et de réinitialisation des mots de passe. À l’aide de cette API, vous pouvez télécharger la réinitialisation de mot de passe individuelles et mot de passe réinitialisé les événements d’enregistrement pour l’intégration avec hello reporting technologie de votre choix.

### <a name="how-tooget-started-with-hello-reporting-api"></a>Comment tooget démarrer avec hello API de création de rapports

tooaccess ces données, vous devez toowrite une petite application ou script tooretrieve à partir de nos serveurs. [Découvrez comment tooget main hello API de création de rapports AD Azure](active-directory-reporting-api-getting-started.md).

Une fois que vous avez un script de travail, vous pouvez ensuite répondre tooexamine hello mot de passe d’inscription et de réinitialisation événements que vous pouvez récupérer toomeet vos scénarios.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): répertorie les colonnes hello disponibles pour les événements de réinitialisation de mot de passe
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): répertorie les colonnes hello disponibles pour les événements de l’inscription de réinitialisation de mot de passe

### <a name="reporting-api-data-retrieval-limitations"></a>Création de rapport sur les limitations de récupération des données API

Actuellement, hello rapports Azure AD et API d’événements récupère les trop**75 000 événements individuels** Hello [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) et [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) types , la répartition hello **30 derniers jours**.

Si vous avez besoin de tooretrieve ou stockez des données au-delà de cette fenêtre, nous vous suggérons de sa conservation dans une base de données externe et à l’aide des deltas hello hello API tooquery résultant. Notre recommandation est toobegin la récupération de ces données lorsque vous démarrez à l’aide de SSPR dans votre organisation, rendre persistant en externe et puis continuez deltas de hello tootrack à partir de ce point.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>Comment les événements d’enregistrement rapidement avec PowerShell de réinitialisation de mot de passe toodownload

En outre toousing Bonjour Azure AD API rapports et événements directement, vous pouvez également utiliser hello ci-dessous les événements de l’inscription de toorecent de script PowerShell dans votre annuaire. Cela est utile dans le cas toosee qui a inscrit récemment ou souhaitez tooensure que votre mot de passe réinitialisé déploiement se produit comme prévu.

* [Script PowerShell d’activité d’inscription SSPR Azure AD](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

### <a name="description-of-report-columns-in-azure-portal"></a>Description des colonnes du rapport dans le portail Azure

Hello liste suivante décrit chacune des colonnes du rapport hello en détail :

* **Utilisateur** – hello l’utilisateur ayant tenté d’effectuer un mot de passe réinitialisé opération d’inscription.
* **Rôle** – rôle hello d’utilisateur hello dans le répertoire de hello.
* **Date et heure** : hello date et heure de la tentative de hello.
* **Données inscrites** – l’inscription de réinitialisation quelles authentification données hello fourni par l’utilisateur au cours de mot de passe.

### <a name="description-of-report-values-in-azure-portal"></a>Description des valeurs du rapport dans le portail Azure

Hello tableau suivant décrit hello différentes valeurs autorisées pour chaque colonne :

| Colonne | Valeurs autorisées et leur signification |
| --- | --- |
| Données inscrites |**Autre adresse de messagerie** – utilisateur utilisé autre adresse de messagerie ou l’authentification par courrier électronique tooauthenticate<p><p>**Téléphone de bureau**– utilisateur utilisé office phone tooauthenticate<p>**Téléphone mobile** -utilisateur utilisé tooauthenticate de téléphone téléphone mobile ou de l’authentification<p>**Les Questions de sécurité** – tooauthenticate de questions de sécurité de l’utilisateur utilisées<p>**N’importe quelle combinaison de hello ci-dessus (par exemple, autre adresse de messagerie + téléphone portable)** – se produit lorsqu’une stratégie 2 porte est spécifiée et montre les deux méthodes hello utilisateur utilisé tooauthentication demande de réinitialisation de mot de passe. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>Activité dans le portail classique de hello de réinitialisation de mot de passe de vue

Ce rapport montre toutes les tentatives de réinitialisation de mot de passe qui se sont produites dans votre organisation.

* **Période max** : 30 jours
* **Nombre max de lignes** : 75 000
* **Téléchargeable**: Oui, via un fichier CSV

### <a name="description-of-report-columns-in-azure-classic-portal"></a>Description des colonnes du rapport dans le portail Azure Classic

Hello liste suivante décrit chacune des colonnes du rapport hello en détail :

1. **Utilisateur** – hello l’utilisateur ayant tenté d’effectuer un mot de passe réinitialisé opération (basée sur le champ d’ID d’utilisateur hello fourni lorsque l’utilisateur de hello prend tooreset un mot de passe).
2. **Rôle** – rôle hello d’utilisateur hello dans le répertoire de hello.
3. **Date et heure** : hello date et heure de la tentative de hello.
4. **Méthodes utilisé** : les méthodes d’authentification hello utilisateur utilisé pour cette opération de réinitialisation.
5. **Résultat** – opération de réinitialisation du résultat de hello de mot de passe hello.
6. **Détails** – hello les détails de la réinitialisation de mot de passe hello pourquoi a entraîné valeur hello il l’a fait.  Inclut également les étapes d’atténuation que vous pouvez adopter tooresolve une erreur inattendue.

### <a name="description-of-report-values-in-azure-classic-portal"></a>Description des valeurs du rapport dans le portail Azure Classic

Hello tableau suivant décrit hello différentes valeurs autorisées pour chaque colonne :

| Colonne | Valeurs autorisées et leur signification |
| --- | --- |
| Méthodes utilisées |**Autre adresse de messagerie** – utilisateur utilisé autre adresse de messagerie ou l’authentification par courrier électronique tooauthenticate<p>**Téléphone de bureau** – utilisateur utilisé office phone tooauthenticate<p>**Téléphone mobile** – utilisateur utilisé tooauthenticate de téléphone téléphone mobile ou de l’authentification<p>**Les Questions de sécurité** – tooauthenticate de questions de sécurité de l’utilisateur utilisées<p>**N’importe quelle combinaison de hello ci-dessus (par exemple, autre adresse de messagerie + téléphone portable)** – se produit lorsqu’une stratégie 2 porte est spécifiée et montre les deux méthodes hello utilisateur utilisé tooauthentication demande de réinitialisation de mot de passe. |
| Résultat |**Abandonné** : l’utilisateur a démarré la réinitialisation de mot de passe, puis s’est arrêté à mi-chemin sans terminer<p>**Bloqué** : compte d’utilisateur a été toouse a empêché le mot de passe réinitialisé en raison de la page de réinitialisation de mot de passe tooattempting toouse hello ou méthode de réinitialisation de mot de passe trop de fois dans une période de 24 heures<p>**Annulé** – utilisateur a démarré la réinitialisation de mot de passe, mais vous cliquez sur la session de hello toocancel cours de hello Annuler bouton <p>**Contacter l’administrateur** – utilisateur a un problème lors de sa session qu’il n’a pas pu résoudre, afin de l’utilisateur de la hello a cliqué sur le lien « Contactez votre administrateur » de hello au lieu de la fin de flux de réinitialisation de mot de passe hello<p>**Échec de** – utilisateur n’a pas pu tooreset un mot de passe, probablement parce que l’utilisateur de hello était pas configuré toouse hello fonctionnalité (par exemple, aucune licence, les informations d’authentification manquantes, mot de passe géré localement mais l’écriture différée est désactivée).<p>**Réussi** : la réinitialisation du mot de passe a réussi. |
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
| L’utilisateur a annulé avant de passer des méthodes d’authentification hello requis |Canceled |
| L’utilisateur a abandonné avant de soumettre un nouveau mot de passe |Canceled |
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

## <a name="self-service-password-management-activity-types"></a>Types d’activités de gestion des mots de passe en libre-service

Hello, les types d’activité suivants s’affichent dans hello **gestion de mot de passe libre-service** catégorie d’événement d’audit.  Une description pour chacun des éléments suivants.

* [**Bloqué à partir de la réinitialisation de mot de passe libre-service** ](#activity-type-blocked-from-self-service-password-reset) -indique un utilisateur a essayé de tooreset un mot de passe, utilisez un opérateur spécifique, ou valider un numéro de téléphone de plus de 5 fois total des dernières 24 heures.
* [**Modifier le mot de passe (libre-service)** ](#activity-type-change-password-self-service) -indique un utilisateur effectuée facultatives ou forcé (tooexpiry échéance) modification du mot de passe.
* [**Réinitialisation du mot de passe (admin)** ](#activity-type-reset-password-by-admin) -indique un administrateur a effectué un mot de passe réinitialisé pour le compte d’un utilisateur à partir de hello portail Azure.
* [**Réinitialisation de mot de passe (libre-service)** ](#activity-type-reset-password-self-service) -indique un utilisateur réinitialiser leur mot de passe à partir de hello [portail de réinitialisation du mot de passe Azure AD](https://passwordreset.microsoftonline.com).
* [**Mot de passe libre-service réinitialiser la progression des activités de flux** ](#activity-type-self-serve-password-reset-flow-activity-progress) -indique de chaque étape spécifique, un utilisateur parcoure (comme un mot de passe spécifiques de réinitialiser la porte d’authentification) dans le cadre d’un mot de passe hello réinitialisation des processus.
* [**Déverrouillage de compte d’utilisateur (libre-service)** ](#activity-type-unlock-user-account-self-service) -indique un utilisateur a été déverrouillée avec succès leur compte Active Directory sans réinitialiser leur mot de passe à partir de hello [portail de réinitialisation du mot de passe Azure AD](https://passwordreset.microsoftonline.com) à l’aide de Hello compte AD déverrouiller sans la fonctionnalité de réinitialisation.
* [**L’utilisateur a inscrit pour la réinitialisation du mot de passe libre-service** ](#activity-type-user-registered-for-self-service-password-reset) -indique un utilisateur a inscrit tous les tooreset en mesure de hello requis informations toobe leur mot de passe conformément aux hello actuellement spécifié de stratégie de réinitialisation du mot de passe client.

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
  * _Échec de_ -indique un échec de l’utilisateur toochange leur mot de passe. En cliquant sur hello ligne permet toosee hello **raison de l’état activité** toolearn catégorie plus d’informations sur la cause de l’échec de hello.
* **Activity Status Failure Reason** - (Motif de l’état d’activité Failure) 
  * _FuzzyPolicyViolationInvalidPassword_ -hello sélectionnés utilisateur un mot de passe a été automatiquement exclu (e) en raison des capacités d’interdit la détection de mot de passe de tooMicrosoft recherche toobe trop courant ou particulièrement faible.

### <a name="activity-type-reset-password-by-admin"></a>Type d’activité : Reset password (by admin) (Réinitialisation du mot de passe (par l’administrateur))

Hello suivant liste explique cette activité en détail :

* **Description de l’activité** – indique un administrateur a effectué un mot de passe réinitialisé pour le compte d’un utilisateur à partir de hello portail Azure.
* **Activité acteur** -administrateur hello qui a exécuté le mot de passe de hello réinitialisé pour le compte d’un autre utilisateur ou administrateur. Doit être un administrateur global, un administrateur de mot de passe, administrateur de l’utilisateur ou un administrateur du support technique.
* **Cible de l’activité** -utilisateur hello dont un mot de passe a été réinitialisé. Il peut s’agir d’un utilisateur final ou d’un autre administrateur.
* **États d’activité autorisés**
  * _Success_ : indique qu’un administrateur a correctement réinitialisé un mot de passe d’utilisateur
  * _Échec de_ -indique un échec de l’administrateur toochange un mot de passe. En cliquant sur hello ligne permet toosee hello **raison de l’état activité** toolearn catégorie plus d’informations sur la cause de l’échec de hello.

### <a name="activity-type-reset-password-self-service"></a>Type d’activité : Reset password (self-service) (Réinitialisation du mot de passe (libre-service))

Hello suivant liste explique cette activité en détail :

* **Description de l’activité** – indique un utilisateur réinitialiser leur mot de passe à partir de hello [portail de réinitialisation du mot de passe Azure AD](https://passwordreset.microsoftonline.com).
* **Activité acteur** -utilisateur hello réinitialiser leur mot de passe. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **Cible de l’activité** -utilisateur hello réinitialiser leur mot de passe. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **États d’activité autorisés**
  * _Success_ : indique qu’un utilisateur a correctement réinitialisé son propre mot de passe
  * _Échec de_ -indique un échec de l’utilisateur tooreset leur propre mot de passe. En cliquant sur hello ligne permet toosee hello **raison de l’état activité** toolearn catégorie plus d’informations sur la cause de l’échec de hello.
* **Activity Status Failure Reason** - (Motif de l’état d’activité Failure)
  * _FuzzyPolicyViolationInvalidPassword_ -administrateur de hello a sélectionné un mot de passe a été automatiquement exclu (e) en raison des capacités d’interdit la détection de mot de passe de tooMicrosoft recherche toobe trop courant ou particulièrement faible.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Type d’activité : Self serve password reset flow activity progress (Progression de l’activité du flux de réinitialisation du mot de passe en libre-service)

Hello suivant liste explique cette activité en détail :

* **Description de l’activité** – indique chaque étape spécifique, un utilisateur parcoure (comme un mot de passe spécifiques de réinitialiser la porte d’authentification) dans le cadre d’un mot de passe hello réinitialisation des processus.
* **Activité acteur** -hello l’utilisateur qui a effectué une partie de mot de passe hello réinitialisé flux. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **Cible de l’activité** -hello l’utilisateur qui a effectué une partie de mot de passe hello réinitialisé flux. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **États d’activité autorisés**
  * _Réussite_ -indique un utilisateur terminé avec succès une étape spécifique du flux de réinitialisation de mot de passe hello.
  * _Échec de_ -indique une étape spécifique d’un mot de passe hello réinitialisé flux a échoué. En cliquant sur hello ligne permet toosee hello **raison de l’état activité** toolearn catégorie plus d’informations sur la cause de l’échec de hello.
* **Motifs des états d’activité autorisés**
  * Voir le tableau ci-dessous pour [tous les motifs d’état d’activité de réinitialisation du mot de passe autorisés](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Type d’activité : Unlock user account (self-service) (Déverrouillage du compte d’utilisateur (libre-service))

Hello suivant liste explique cette activité en détail :

* **Description de l’activité** – indique un utilisateur a été déverrouillée avec succès leur compte Active Directory sans réinitialiser leur mot de passe à partir de hello [portail de réinitialisation du mot de passe Azure AD](https://passwordreset.microsoftonline.com) à l’aide du compte de hello AD déverrouiller sans réinitialiser fonctionnalité.
* **Activité acteur** -utilisateur hello déverrouillé leur compte sans réinitialiser leur mot de passe. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **Cible de l’activité** -utilisateur hello déverrouillé leur compte sans réinitialiser leur mot de passe. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **États d’activité autorisés**
  * _Success_ : indique qu’un utilisateur a correctement déverrouillé son propre compte
  * _Échec de_ -indique un échec de l’utilisateur toounlock leur compte. En cliquant sur hello ligne permet toosee hello **raison de l’état activité** toolearn catégorie plus d’informations sur la cause de l’échec de hello.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Type d’activité : User registered for self-service password reset (Utilisateur inscrit pour la réinitialisation du mot de passe libre-service)

Hello suivant liste explique cette activité en détail :

* **Description de l’activité** – indique un utilisateur a inscrit tous les tooreset en mesure de hello requis informations toobe leur mot de passe conformément aux hello actuellement spécifié de stratégie de réinitialisation du mot de passe client. 
* **Activité acteur** -utilisateur hello qui se sont inscrits pour la réinitialisation du mot de passe. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **Cible de l’activité** -utilisateur hello qui se sont inscrits pour la réinitialisation du mot de passe. Il peut s’agir d’un utilisateur final ou d’un administrateur.
* **États d’activité autorisés**
  * _Réussite_ -indique un utilisateur inscrit pour le mot de passe réinitialisé conformément à la stratégie actuelle hello. 
  * _Échec de_ -indique un tooregister utilisateur a échoué pour la réinitialisation du mot de passe. En cliquant sur hello ligne permet toosee hello **raison de l’état activité** toolearn catégorie plus d’informations sur la cause de l’échec de hello. Remarque : cela ne signifie pas un utilisateur est tooreset ne peut pas leur propre mot de passe simplement que qu’ils n’a pas terminé les processus d’inscription de hello. S’il existe des données non vérifiées sur leur compte est correcte (par exemple, un numéro de téléphone qui n’est pas validé), même si elles n’ont pas vérifié ce numéro de téléphone, ils peuvent encore l’utiliser tooreset leur mot de passe. Pour plus d’informations, consultez [Que se passe-t-il lorsqu’un utilisateur s’inscrit ?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="next-steps"></a>Étapes suivantes

Hello suivant liens fournit des informations supplémentaires concernant le mot de passe réinitialisé à l’aide d’Azure AD

* [Journaux d’audit de gestion de toouser raccourci](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit) - accédez directement de la gestion des utilisateurs du locataire tooyour les journaux d’audit
* [**Démarrage rapide**](active-directory-passwords-getting-started.md) : soyez rapidement opérationnel avec la gestion des mots de passe en libre-service d’Azure AD. 
* [**Licences**](active-directory-passwords-licensing.md) : configurez vos licences Azure AD.
* [**Données** ](active-directory-passwords-data.md) : comprendre les données de hello est nécessaire et comment il est utilisé pour la gestion de mot de passe
* [**Déploiement** ](active-directory-passwords-best-practices.md) -planifier et déployer des utilisateurs de tooyour SSPR hello d’aide est disponible ici
* [**Personnaliser** ](active-directory-passwords-customize.md) -personnaliser hello apparence Hello SSPR expérience pour votre entreprise.
* [**Présentation approfondie technique** ](active-directory-passwords-how-it-works.md) -accédez derrière hello RIDEAU toounderstand son fonctionnement
* [**Forum Aux Questions (FAQ)**](active-directory-passwords-faq.md) : Comment ? Pourquoi ? Quoi ? Où ? Qui ? Quand ? -Réponses tooquestions vous souhaitiez toujours tooask
* [**Résoudre les problèmes** ](active-directory-passwords-troubleshoot.md) -en savoir comment tooresolve commun problèmes que nous pouvons voir avec SSPR
* [**Stratégie**](active-directory-passwords-policy.md) : comprenez et définissez les stratégies de mot de passe d’Azure AD
