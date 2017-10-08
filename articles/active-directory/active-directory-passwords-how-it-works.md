---
title: "Découverte approfondie : réinitialisation du mot de passe libre-service Azure AD | Microsoft Docs"
description: "Découverte approfondie de la réinitialisation du mot de passe libre-service Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 618c5908-5bf6-4f0d-bf88-5168dfb28a88
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: c177192bbe69d179a25d174b06a0813ec28e2615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-password-reset-in-azure-ad-deep-dive"></a>Découverte approfondie de la réinitialisation de mot de passe libre-service dans Azure AD

Comment fonctionne la réinitialisation de mot de passe libre-service ? Que signifie cette option dans l’interface hello ? Continuer à lire toofind plus d’informations sur le mot de passe libre-service Azure AD réinitialiser.

## <a name="how-does-hello-password-reset-portal-work"></a>Comment le mot de passe hello réinitialise travail portail

Lorsqu’un utilisateur navigue toohello portail de réinitialisation du mot de passe, un flux de travail est lancé toodetermine :

   * La page de hello doit être localisée ?
   * Compte d’utilisateur hello n’est valide ?
   * L’organisation utilisateur de hello appartient à ?
   * Où hello mot de passe est géré ?
   * Est la fonctionnalité de hello hello utilisateur sous licence toouse ?


Lire les étapes hello ci-dessous toolearn sur la logique de hello derrière la page de réinitialisation de mot de passe hello.

1. Cliquent hello ne peut pas accéder au lien avec votre compte ou passe directement trop[https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com).
2. Basé sur hello de paramètres régionaux de navigateur hello expérience est rendue dans la langue appropriée de hello. expérience de réinitialisation de mot de passe Hello est localisé dans hello les mêmes langues que Office 365 prend en charge.
3. L’utilisateur entre un ID utilisateur et passe un test CAPTCHA.
4. Azure AD vérifie si l’utilisateur de hello est en mesure de toouse cette fonctionnalité de manière hello suivante :
   * Vérifie que l’utilisateur hello dispose de cette fonctionnalité est activée et une licence Azure AD.
     * Si l’utilisateur de hello n’a pas cette fonctionnalité est activée ou une licence attribuée, hello l’utilisateur est invité toocontact tooreset de leur administrateur leur mot de passe.
   * Vérifie que l’utilisateur hello possède les données de stimulation droite hello définies sur leur compte en fonction de la stratégie de l’administrateur.
     * Si la stratégie ne nécessite qu’une demande d’accès, il est garantie que l’utilisateur hello a hello défini données appropriées pour au moins un des défis de hello activés par la stratégie de l’administrateur hello.
       * Si l’utilisateur de hello n’est pas configuré, puis hello utilisateur est toocontact conseillée leur tooreset administrateur leur mot de passe.
     * Si la stratégie de hello exige deux tests, il est garantie que l’utilisateur hello a hello défini données appropriées pour au moins deux des défis hello activés par la stratégie de l’administrateur hello.
       * Si les utilisateurs hello ne sont pas configuré, puis nous hello utilisateur est toocontact conseillée leur tooreset administrateur leur mot de passe.
   * Vérifie si le mot de passe de l’utilisateur hello est géré localement (fédérés ou synchronisés avec hachage du mot de passe).
     * Si l’écriture différée est déployée et hello mot de passe utilisateur est géré localement, l’utilisateur de hello est autorisée à tooproceed tooauthenticate et réinitialiser leur mot de passe.
     * Si l’écriture différée n’est pas déployée hello mot de passe utilisateur est géré localement, puis hello utilisateur est invité toocontact tooreset de leur administrateur leur mot de passe.
5. S’il est déterminé que l’utilisateur hello est en mesure de toosuccessfully réinitialiser leur mot de passe, puis l’utilisateur de hello est guidé hello les processus de réinitialisation.

## <a name="authentication-methods"></a>Méthodes d’authentification

Si la réinitialisation de mot de passe libre-service (SSPR) est activé, vous devez sélectionner au moins un des hello options pour les méthodes d’authentification suivantes. Nous vous recommandons vivement de choisir au moins deux méthodes d’authentification pour offrir davantage de flexibilité à vos utilisateurs.

* Email
* Téléphone mobile
* Téléphone de bureau
* Questions de sécurité

### <a name="what-fields-are-used-in-hello-directory-for-authentication-data"></a>Quels champs sont utilisés dans le répertoire de hello pour les données d’authentification

* Téléphone de bureau correspond tooOffice téléphone
    * Les utilisateurs sont tooset impossible dans ce champ s’il doit être défini par un administrateur
* Téléphone portable correspond tooeither téléphone d’authentification (non visible publiquement) ou d’un téléphone Mobile (visible publiquement)
    * service de Hello recherche d’abord téléphone d’authentification, puis revient tooMobile Phone si n’est pas présent
* Autre adresse de messagerie correspond tooeither E-mail d’authentification (non visible publiquement) ou l’autre adresse de messagerie
    * service de Hello recherche d’abord E-mail d’authentification, puis échoue tooAlternate différé par courrier électronique

Par défaut, seuls les attributs de cloud hello téléphone de bureau et téléphone portable sont synchronisés tooyour annuaire du cloud à partir de votre annuaire local pour les données d’authentification.

Les utilisateurs peuvent uniquement réinitialiser leur mot de passe s’ils ont des données présentes dans les méthodes d’authentification hello qu’administrateur hello a activé et nécessite.

Si les utilisateurs ne voulez pas que leur toobe numéro de téléphone mobile visible dans le répertoire de hello, seront quand même comme toouse il pour la réinitialisation du mot de passe, les administrateurs doivent remplir dans le répertoire de hello et utilisateur de hello doit ensuite remplir leurs **téléphone d’authentification**  attribut via hello [inscription portail de réinitialisation de mot de passe](http://aka.ms/ssprsetup). Les administrateurs peuvent voir ces informations dans le profil de l’utilisateur hello, mais il n’est pas publiée ailleurs. Si un compte d’administrateur Azure enregistre son numéro de téléphone d’authentification, il est rempli dans un champ de téléphone mobile hello et est visible.

### <a name="number-of-authentication-methods-required"></a>Nombre de méthodes d’authentification requises

Cette option détermine le nombre minimal de hello de méthodes d’authentification disponibles hello un utilisateur doit réussir tooreset ou déverrouiller son mot de passe et peut être définie tooeither 1 ou 2.

Les utilisateurs peuvent choisir toosupply plusieurs méthodes d’authentification si elles sont activées par l’administrateur de hello.

Si un utilisateur n’a pas de méthodes hello minimale requise enregistrés, ils voient une page d’erreur qui dirige les toorequest un tooreset administrateur leur mot de passe.

### <a name="how-secure-are-my-security-questions"></a>Sécuriser mes questions de sécurité

Si vous utilisez des questions de sécurité, nous vous recommandons les en cours d’utilisation par une autre méthode qu’ils puissent être moins sécurisées que d’autres méthodes, car certaines personnes peuvent connaître les réponses hello questions des utilisateurs tooanother.

> [!NOTE] 
> Les questions de sécurité sont stockées de manière privée et sécurisée sur un objet utilisateur dans le répertoire de hello et ne peuvent y répondre par les utilisateurs lors de l’inscription. Il n’existe aucun moyen pour un administrateur de tooread ou modifier un utilisateur questions ou les réponses.
>

### <a name="security-question-localization"></a>Localisation de la question de sécurité

Toutes les questions prédéfinies qui suivent sont traduites dans le jeu complet de hello des langues d’Office 365 en fonction de paramètres régionaux du navigateur de l’utilisateur hello.

* Dans quelle ville avez-vous rencontré votre premier(ère) époux/épouse ou compagnon/compagne ?
* Dans quelle ville vos parents se sont-ils rencontrés ?
* Dans quelle ville vit votre frère ou sœur le/la plus proche ?
* Dans quelle ville votre père est-il né ?
* Dans quelle ville était votre premier travail ?
* Dans quelle ville votre mère est-elle née ?
* Dans quelle ville étiez-vous pour le Nouvel an de l’année 2000 ?
* Qu’est le nom de votre professeur haute hello * école ?
* Quel est nom hello d’une université que vous avez appliqué toobut pas allé ?
* Qu’est le nom hello de hello emplacement dans lequel la réception de votre premier mariage ?
* Quel est le deuxième prénom de votre père ?
* Quel est votre aliment préféré ?
* Quels sont les nom et prénom de votre grand-mère maternelle ?
* Quel est le deuxième prénom de votre mère ?
* Quel est le mois et l’année de naissance de votre frère/sœur aîné(e) ? (par exemple, novembre 1985)
* Quel est le deuxième prénom de votre frère/sœur aîné(e) ?
* Quels sont les nom et prénom de votre grand-père paternel ?
* Quel est le deuxième prénom de votre frère/sœur cadet(te) ?
* Où avez-vous effectué votre dernière année de l’école primaire ?
* Ce qui a été hello tout d’abord les nom et prénom de votre meilleur ami ?
* Ce qui a été hello tout d’abord les nom et prénom de votre premier amoureux ?
* Quel était le nom de votre professeur hello ?
* Quels étaient la marque de hello et le modèle de votre première voiture ou Moto ?
* Quel était le nom hello de hello première école ?
* Quel était le nom hello d’hôpital hello dans lequel vous êtes né ?
* Quel était le nom hello de rue hello de votre première enfance ?
* Quel était le nom hello de votre héros d’enfance ?
* Quel était le nom hello de votre peluche préféré ?
* Quel était le nom hello de votre premier animal de compagnie ?
* Quel était votre surnom quand vous étiez enfant ?
* Quel était votre sport préféré au lycée ?
* Quel a été votre premier travail ?
* Ce qui ont été hello les quatre derniers chiffres de votre numéro de téléphone d’enfance ?
* Quand vous étiez jeune, que vouliez-vous toobe lorsque vous ont été développés ?
* Qui est hello plus célèbre que vous ayez jamais rencontrée ?

### <a name="custom-security-questions"></a>Questions de sécurité personnalisées

Les questions de sécurité personnalisées ne sont pas localisées pour tous les paramètres régionaux. Toutes les questions personnalisées sont affichent dans hello même langue, ils sont entrés dans l’interface utilisateur d’administration hello, même si les paramètres régionaux du navigateur de l’utilisateur hello sont différent. Si vous avez besoin de questions localisées, utilisez les questions hello prédéfinie.

longueur maximale de Hello d’une question de sécurité personnalisé est de 200 caractères.

### <a name="security-question-requirements"></a>Conditions relatives aux questions de sécurité

* La limite minimale du nombre de caractères par réponse est de 3 caractères.
* La limite maximale du nombre de caractères par réponse est de 40 caractères.
* Les utilisateurs ne peuvent pas répondre hello même question plusieurs fois
* Les utilisateurs ne peuvent pas fournir hello même répondre toomore à une question
* N’importe quel jeu de caractères peut être utilisé toodefine questions et réponses, y compris les caractères Unicode
* nombre Hello de questions définies doit être supérieur ou égal à nombre toohello de tooregister obligatoire de questions

## <a name="registration"></a>Inscription

### <a name="require-users-tooregister-when-signing-in"></a>Exiger des utilisateurs tooregister lors de la connexion

L’activation de cette option requiert un utilisateur qui est activé pour le mot de passe réinitialisé inscription de réinitialisation du mot de passe toocomplete hello si elles connecter tooapplications à l’aide de toosign Azure AD dans telles que celles qui suivent :

* Office 365
* Portail Azure
* Volet d'accès
* Applications fédérées
* Applications personnalisées utilisant Azure AD

La désactivation de cette fonctionnalité permettra toujours aux utilisateurs toomanually inscrire leurs informations de contact en vous rendant sur [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) ou en cliquant sur hello **inscrire pour la réinitialisation de mot de passe** lien sous hello onglet profil dans le volet d’accès hello.

> [!NOTE]
> Les utilisateurs peuvent fermer le portail d’inscription de réinitialisation du mot de passe hello en cliquant sur Annuler ou de fermeture de fenêtre hello, mais ils sont invités à chaque fois qu’ils se connecter jusqu'à ce qu’elles terminent l’inscription.
>

### <a name="number-of-days-before-users-are-asked-tooreconfirm-their-authentication-information"></a>Nombre de jours avant que les utilisateurs sont invités à tooreconfirm leurs informations d’authentification

Cette option détermine la période de temps entre la configuration et les informations d’authentification de reconfirmer hello et est uniquement disponible si vous activez hello **nécessitent tooregister des utilisateurs lors de la connexion** option.

Les valeurs valides sont 0-730 jours par 0 ce qui signifie de ne jamais demander aux utilisateurs tooreconfirm leurs informations d’authentification

## <a name="notifications"></a>Notifications

### <a name="notify-users-on-password-resets"></a>Notifier les utilisateurs lors des réinitialisations de mot de passe ?

Si cette option a la valeur tooyes, utilisateur hello qui réinitialise son mot de passe reçoit un message électronique pour les informer que leur mot de passe a été modifié via hello SSPR portail tootheir principal et les adresses courriel de secours sur le fichier dans Azure AD. Personne n’est informé de cet événement de réinitialisation.

### <a name="notify-all-admins-when-other-admins-reset-their-passwords"></a>Notifier tous les administrateurs quand d’autres administrateurs réinitialisent leur mot de passe ?

Si cette option a la valeur tooyes, puis **tous les administrateurs** recevoir une adresse de messagerie principale messagerie tootheir sur le fichier dans Azure AD pour les informer qu’un autre administrateur a changé son mot de passe à l’aide de SSPR.

Exemple : quatre administrateurs font partie d’un environnement. L’administrateur A réinitialise son mot de passe à l’aide de la réinitialisation du mot de passe libre-service. Les administrateurs B, C et D reçoivent un e-mail les informant de cet évènement.

## <a name="on-premises-integration"></a>Intégration locale

Si vous avez installé, configuré et activé Azure AD Connect, vous disposerez d’options supplémentaires pour les intégrations locales.

### <a name="write-back-passwords-tooyour-on-premises-directory"></a>Écriture différée des mots de passe tooyour des services locaux

Détermine si l’écriture différée de mot de passe est activée pour ce répertoire et, si c’est le cas, indique l’état hello du service de l’écriture différée local hello. Cela est utile si vous souhaitez tootemporarily désactiver hello l’écriture différée de mot de passe sans avoir à reconfigurer Azure AD Connect.

* Si hello basculer est tooyes de jeu, puis l’écriture différée est activée et fédérée et les utilisateurs synchronisé de hachage de mot de passe seront en mesure de tooreset leurs mots de passe.
* Si hello basculer est toono de jeu, puis l’écriture différée est désactivée et fédérée et les utilisateurs synchronisé de hachage de mot de passe ne sera pas en mesure de tooreset leurs mots de passe.

### <a name="allow-users-toounlock-accounts-without-resetting-their-password"></a>Autoriser les utilisateurs toounlock comptes sans réinitialiser leur mot de passe

Indique si les utilisateurs visitant le portail de réinitialisation du mot de passe hello doivent être toounlock d’option hello donné leur annuaire Active Directory local comptes sans réinitialiser leur mot de passe. Par défaut, Azure AD est toujours ouvrir des comptes lorsque vous effectuez une réinitialisation de mot de passe, ce paramètre vous permet de tooseparate ces deux opérations. 

* Si défini trop « Oui », les utilisateurs seront donnée hello option tooreset leur mot de passe et déverrouiller le compte de hello ou toounlock sans réinitialiser le mot de passe hello.
* Si la valeur trop « non », les utilisateurs seront en mesure de tooperform un compte et réinitialisation de mot de passe combiné opération de déverrouillage.

## <a name="network-requirements"></a>Configuration requise pour le réseau

### <a name="firewall-rules"></a>Règles de pare-feu

[URL et plages d’adresses IP Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

Pour Azure AD Connect version 1.1.443.0 et versions ultérieures, vous devez sortant suivant de toohello accès HTTPS
* passwordreset.microsoftonline.com
* servicebus.windows.net

Pour un accès plus granulaire, vous pouvez trouver la liste hello mis à jour de Microsoft Azure Datacenter plages d’adresses IP qui est mis à jour tous les mercredis et en suivant des hello effet lundi [ici](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="idle-connection-timeouts"></a>Délais d’expiration de connexion inactive

outil de connexion Hello Azure AD envoie les pings/KeepAlive périodique tooServiceBus points de terminaison tooensure que les connexions hello restent actifs. Outil de hello doit détecter le que trop de connexions sont en cours d’arrêt, elle augmentera automatiquement fréquence hello du point de terminaison toohello pings. Hello plus bas 'ping intervalles' supprime toois 1 ping toutes les 60 secondes, toutefois, il est fortement conseillé que proxys/pare-feu autorisent les connexions inactives toopersist au moins 2 à 3 minutes. *Pour les versions antérieures, nous suggérons 4 minutes ou plus.

## <a name="active-directory-permissions"></a>Autorisations Active Directory

Hello compte spécifié dans l’utilitaire hello Azure AD Connect doit avoir réinitialiser le mot de passe, modifier le mot de passe, des autorisations en écriture lockoutTime et des autorisations en écriture pwdLastSet, droits sur l’objet racine de hello d’étendus **chaque domaine** dans cette forêt **ou** sur l’utilisateur hello unités d’organisation vous souhaitez toobe dans l’étendue de SSPR.

Si vous n’êtes pas sûr quel hello compte ci-dessus fait référence, ouvrez configuration d’Azure Active Directory Connect hello l’interface utilisateur, et cliquez sur option de configuration hello vue actuelle. compte Hello que vous devez toois d’autorisation tooadd répertoriés sous « Répertoires synchronisé »

Définition de ces autorisations permet de compte de service Agent de gestion hello pour chaque mot de passe toomanage forêt pour le compte de comptes d’utilisateur au sein de cette forêt. **Si vous oubliez tooassign ces autorisations, puis, alors que l’écriture différée toobe correctement configuré, les utilisateurs rencontrent des erreurs lors de la tentative de toomanage leurs mots de passe local du cloud de hello.**

> [!NOTE]
> Elle peut prendre tooan heures ou plus pour ces autorisations tooreplicate tooall les objets dans votre annuaire.
>

tooset des autorisations appropriées de hello pour toooccur de l’écriture différée de mot de passe

1. Ouvrir des ordinateurs et utilisateurs Active Directory avec un compte qui dispose des autorisations d’administration de domaine approprié de hello
2. À partir du menu Affichage de hello, assurez-vous de que fonctionnalités avancées est activée
3. Dans le volet gauche de hello, objet hello qui représente la racine de hello du domaine de hello d’avec le bouton droit et choisissez Propriétés
    * Cliquez sur onglet de sécurité hello
    * Puis, cliquez sur Avancé.
4. À partir de l’onglet d’autorisations hello, cliquez sur Ajouter
5. Sélectionner un compte hello que les autorisations sont appliquées trop (à partir de programme d’installation d’Azure AD Connect)
6. Dans toodrop s’applique de hello zone de liste déroulante, sélectionnez les objets utilisateur descendants
7. Sous autorisations suivants de hello hello cases à cocher
    * Ne pas faire expirer le mot de passe
    * Réinitialiser le mot de passe
    * Modifier le mot de passe
    * Écrire lockoutTime
    * Écrire pwdLastSet
8. Cliquez sur Appliquer/OK via tooapply et fermer les boîtes de dialogue.

## <a name="how-does-password-reset-work-for-b2b-users"></a>Comment fonctionne la réinitialisation du mot de passe pour les utilisateurs B2B ?
La réinitialisation et la modification du mot de passe sont totalement compatibles avec toutes les configurations B2B.  Lisez ce qui suit pour hello trois explicite B2B cas pris en charge par la réinitialisation du mot de passe.

1. **Les utilisateurs à partir d’une organisation partenaire avec un locataire Azure AD** - si organisation hello vous s’associent avec un locataire Azure AD, nous **respectent les stratégies de réinitialisation de mot de passe sont activés dans ce locataire**. Pour un mot de passe réinitialisé toowork, hello partenaire organisation doit simplement toomake que Azure AD SSPR est activé, ce qui est sans frais supplémentaires pour les clients Office 365, et peut être activé en suivant les étapes hello notre [mise en route de la gestion de mot de passe ](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords) guide.
2. **Les utilisateurs qui souscrit à l’aide de [libre-service d’abonnement](active-directory-self-service-signup.md)**  - si l’organisation hello vous s’associent avec utilisé hello [libre-service d’abonnement](active-directory-self-service-signup.md) tooget de fonctionnalité à un client, nous leur permettre de réinitialisation de la adresse de messagerie Hello qu'ils inscrits.
3. **B2B utilisateurs** -les nouveaux utilisateurs B2B créés à l’aide hello nouvelle [les fonctionnalités Azure AD B2B](active-directory-b2b-what-is-azure-ad-b2b.md) sera également en mesure de tooreset leurs mots de passe avec messagerie hello ils enregistrés au cours du processus d’invitation hello.

tootest, accédez toohttp://passwordreset.microsoftonline.com avec l’un de ces utilisateurs partenaires. Tant que ces utilisateurs disposent d’une autre adresse de messagerie ou d’un e-mail d’authentification, la réinitialisation du mot de passe fonctionne comme prévu.

## <a name="next-steps"></a>Étapes suivantes

Hello suivant liens fournit des informations supplémentaires concernant le mot de passe réinitialisé à l’aide d’Azure AD

* [**Démarrage rapide**](active-directory-passwords-getting-started.md) : soyez rapidement opérationnel avec la gestion des mots de passe en libre-service d’Azure AD. 
* [**Licences**](active-directory-passwords-licensing.md) : configurez vos licences Azure AD.
* [**Données** ](active-directory-passwords-data.md) : comprendre les données de hello est nécessaire et comment il est utilisé pour la gestion de mot de passe
* [**Déploiement** ](active-directory-passwords-best-practices.md) -planifier et déployer des utilisateurs de tooyour SSPR hello d’aide est disponible ici
* [**Stratégie**](active-directory-passwords-policy.md) : comprenez et définissez les stratégies de mot de passe d’Azure AD
* [**Écriture différée de mot de passe**](active-directory-passwords-writeback.md) - fonctionnement de l’écriture différée de mot de passe avec votre annuaire local
* [**Personnaliser** ](active-directory-passwords-customize.md) -personnaliser hello apparence Hello SSPR expérience pour votre entreprise.
* [**Rapports**](active-directory-passwords-reporting.md) : découvrez si, quand et où vos utilisateurs accèdent aux fonctionnalités de réinitialisation de mot de passe en libre-service
* [**Forum Aux Questions (FAQ)**](active-directory-passwords-faq.md) - Comment ? Pourquoi ? Quoi ? Où ? Qui ? Quand ? -Réponses tooquestions vous souhaitiez toujours tooask
* [**Résoudre les problèmes** ](active-directory-passwords-troubleshoot.md) -en savoir comment tooresolve commun problèmes que nous pouvons voir avec SSPR

