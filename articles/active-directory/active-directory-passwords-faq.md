---
title: "Forum aux questions : réinitialisation du mot de passe en libre-service Azure AD | Microsoft Docs"
description: "Forum aux questions concernant la réinitialisation du mot de passe en libre-service Azure AD"
services: active-directory
keywords: "Gestion des mots de passe Active Directory, gestion des mots de passe, réinitialisation de mot de passe en libre-service Azure AD"
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
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a>Forum Aux Questions sur la gestion des mots de passe

Hello suivant est des questions fréquemment posées pour tous les éléments liés toopassword réinitialiser.

Si vous avez une question générale sur Azure AD et le mot de passe libre-service réinitialisation, ce qui reste sans réponse ici, vous pouvez demander Communauté de hello pour obtenir une assistance sur hello [les forums Azure Ad](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD). Les membres de la Communauté de hello inclure les ingénieurs, les chefs de produit, les MVP et autres professionnels de l’informatique.

Cette FAQ est divisée en hello les sections suivantes :

* [**Questions relatives à l’inscription à la réinitialisation du mot de passe**](#password-reset-registration)
* [**Questions relatives à la réinitialisation du mot de passe**](#password-reset)
* [**Questions relatives au changement du mot de passe**](#password-change)
* [**Questions relatives aux rapports de gestion des mots de passe**](#password-management-reports)
* [**Questions relatives à l’écriture différée du mot de passe**](#password-writeback)

## <a name="password-reset-registration"></a>Inscription à la réinitialisation de mot de passe
* **Q : Mes utilisateurs peuvent-ils inscrire leurs propres données de réinitialisation du mot de passe ?**

  > **R :** Oui, tant que la réinitialisation du mot de passe est activée et qu’ils sont concédés sous licence, ils peuvent accéder portail d’inscription de réinitialisation de mot de passe de toohello à http://aka.ms/ssprsetup tooregister leurs informations d’authentification. Les utilisateurs peuvent également inscrire en accédant volet d’accès toohello à http://myapps.microsoft.com, onglet hello du profil, puis sur hello Registre pour l’option de réinitialisation de mot de passe.
  >
  >
* **Q : Puis-je définir des données de réinitialisation de mot de passe pour le compte de mes utilisateurs ?**

  > **R :** Oui, vous pouvez le faire avec Azure AD Connect, PowerShell, hello [portail Azure](https://portal.azure.com), ou le portail d’administration Office hello. Pour plus d’informations, voir l’article hello [données utilisées par Azure AD libre-service mot de passe réinitialisé](active-directory-passwords-data.md).
  >
  >
* **Q : Puis-je synchroniser localement des données pour des questions de sécurité ?**

  > **R :** Ce n’est actuellement pas possible.
  >
  >
* **Q : Mes utilisateurs peuvent-ils inscrire des données pour que les autres utilisateurs ne puissent pas les voir ?**

  > **R :** Oui, lorsque les utilisateurs enregistrent des données à l’aide de hello portail de l’enregistrement de la réinitialisation du mot de passe, il est enregistré dans les champs d’authentification privés qui ne sont visibles que par les administrateurs globaux et hello de l’utilisateur.
    >
    > [!NOTE]
    > Si un **compte d’administrateur Azure** enregistre son numéro de téléphone d’authentification, il est également remplie dans le champ de téléphone mobile hello et est visible.
    >
  >
  >
* **Q : Mes utilisateurs doivent-ils toobe enregistré avant de pouvoir utiliser la réinitialisation de mot de passe ?**

  > **R :** non, si vous définissez suffisamment d’informations d’authentification de leur part, les utilisateurs n’ont pas tooregister. Mot de passe de réinitialisation, que vous avez correctement mis en forme des données stockées dans les champs appropriés de hello dans le répertoire de hello.
  >
  >
* **Q : puis-je synchroniser ou définir les champs téléphone d’authentification, E-mail d’authentification ou téléphone d’authentification secondaire hello pour le compte de mes utilisateurs ?**

  > **R :** Ce n’est actuellement pas possible.
  >
  >
* **Q : comment portail de l’enregistrement hello connaît le tooshow options Mes utilisateurs ?**

  > **R :** d’inscription portail de réinitialisation de mot de passe hello uniquement montre hello options que vous avez activées pour vos utilisateurs. Ces options sont trouvent sous hello section stratégie de réinitialisation de mot de passe utilisateur de l’onglet configurer de votre annuaire. Par exemple, cela signifie que si vous n’activez pas les questions de sécurité, puis les utilisateurs ne sont pas en mesure de tooregister pour cette option.
  >
  >
* **Q : Quand un utilisateur est-il considéré comme inscrit ?**

  > **R :** un utilisateur est considéré comme inscrit pour SSPR lorsqu’ils ont enregistrés au moins hello **nombre de tooreset requis de méthodes** que vous avez définie dans hello [portail Azure](https://portal.azure.com).
  >
  >
## <a name="password-reset"></a>Réinitialisation de mot de passe
* **Q : combien de temps dois-je attendre tooreceive un courrier électronique, SMS ou appel téléphonique de réinitialisation de mot de passe ?**

  > **R :** par courrier électronique, messages SMS et appels téléphoniques doivent arriver dans inférieurs à une minute, avec hello situant 5 à 20 secondes.
    >Si vous ne recevez pas de notification de hello dans ce laps de temps :
        > * Vérifiez votre dossier de courrier indésirable.
        > * Numéro hello ou adresse de messagerie utilisés est hello une souhaitées.
        > * Vérifiez que les données d’authentification hello dans le répertoire de hello sont correctement formatées.
                >     * Par exemple « +1 4255551234 » ou « user@contoso.com »
  >
  >
* **Q : Quelles langues sont prises en charge pour la réinitialisation de mot de passe ?**

  > **R :** hello d’interface utilisateur de réinitialisation de mot de passe, les messages SMS et voix appels sont localisés dans hello mêmes langues sont prises en charge dans Office 365.
  >
  >
* **Q : quelles parties de l’expérience de réinitialisation de mot de passe hello obtient marque lorsque je définis d’organisation dans mon annuaire de personnalisation de l’onglet Configurer ?**

  > **R :** portail de réinitialisation du mot de passe hello affiche le logo de votre organisation et vous permet de tooconfigure hello contactez votre administrateur lien toopoint tooa personnalisé adresse de messagerie ou URL. Tout message électronique envoyé par la réinitialisation du mot de passe inclut logo de votre organisation, de couleurs, de nom dans le corps hello de courrier électronique de hello et personnalisées à partir du nom.
  >
  >
* **Q : Comment puis-je pour informer les utilisateurs sur l’emplacement toogo tooreset leurs mots de passe ?**

  > **R :** vous pouvez envoyer votre toohttps://passwordreset.microsoftonline.com utilisateurs directement, ou vous pouvez leur demander de tooclick hello **ne peut pas accéder au lien avec votre compte** sur la page de connexion de n’importe quel professionnel ou scolaire. Vous pouvez également publier ces liens dans un utilisateur de facilement accessibles tooyour sur place.
  >
  >
* **Q : Puis-je utiliser cette page à partir d’un appareil mobile ?**

  > **R :** Oui, cette page fonctionne sur les appareils mobiles.
  >
  >
* **Q : Prenez-vous en charge le déverrouillage des comptes Active Directory locaux quand les utilisateurs réinitialisent leurs mots de passe ?**

  > **R :** oui, lorsqu’un utilisateur réinitialise son mot de passe et que l’écriture différée de mot de passe a été déployée à l’aide d’Azure AD Connect, ce compte d’utilisateur est déverrouillé automatiquement lorsqu’il réinitialise son mot de passe.
  >
  >
* **Q : Comment puis-je intégrer la réinitialisation de mot de passe directement dans l’expérience de connexion de Bureau de mes utilisateurs ?**

  > **R :** si vous êtes un client Azure AD Premium, vous pouvez installer le Gestionnaire d’identité Microsoft sans coût supplémentaire et déployer hello local mot de passe réinitialisation solution toomeet cette exigence.
  >
  >
* **Q : Puis-je définir des questions de sécurité différentes pour différents paramètres régionaux ?**

  > **R :** Ce n’est actuellement pas possible.
  >
  >
* **Q : combien de questions puis-je configurer pour l’option d’authentification hello Questions de sécurité ?**

  > **R :** vous pouvez configurer des questions de sécurité personnalisé too20 Bonjour [portail Azure](https://portal.azure.com).
  >
  >
* **Q : Quelle doit être la longueur des questions de sécurité ?**

  > **R :** Les questions de sécurité peuvent comprendre entre 3 et 200 caractères.
  >
  >
* **Q : combien de temps peuvent être réponses toosecurity questions ?**

  > **R :** réponses peuvent contenir 3 caractères too40.
  >
  >
* **Q : des réponses en double toosecurity questions rejetées ?**

  > **R :** Oui, nous rejetons les réponses en double toosecurity questions.
  >
  >
* **Q : mai un Registre utilisateur hello même question de sécurité plusieurs fois ?**

  > **R :** Non, une fois qu’un utilisateur a inscrit une question particulière, il ne peut plus inscrire cette même question une deuxième fois.
  >
  >
* **Q : est-il possible tooset une limite minimale des questions de sécurité pour l’inscription et la réinitialisation ?**

  > **R :** Oui, vous pouvez définir une limite pour l’inscription et une autre pour la réinitialisation. Vous pouvez poser entre 3 et 5 questions de sécurité pour l’inscription et entre 3 et 5 questions pour la réinitialisation.
  >
  >
* **Q : si un utilisateur a enregistré plus que hello le nombre maximal de tooreset requis de questions, comment les sont les questions de sécurité sélectionnées lors de la réinitialisation ?**

  > **R :** sécurité N questions sont sélectionnées au hasard nombre total de hello de questions auxquelles un utilisateur a inscrit, où N est hello **nombre de questions des tooreset requis**. Par exemple, si un utilisateur a enregistré 5 questions de sécurité, mais seulement 3 sont tooreset requis, 3 Hello 5 sont sélectionnées de manière aléatoire et présentées à la réinitialisation. Si hello utilisateur obtient les questions de toohello les réponses hello incorrect, processus de sélection de hello reproduit tooprevent martelage de question.
  >
  >
* **Q : Limitez-vous les tentatives de réinitialisation de mot de passe effectuées en un bref laps de temps ?**

  > **R :** Oui, il existe des fonctionnalités de sécurité intégrées tooprotect de réinitialisation de mot de passe d’une mauvaise utilisation. Les utilisateurs peuvent uniquement tenter 5 réinitialisations de mot de passe en une heure, après quoi leur compte est verrouillé pendant 24 heures. Ils peuvent uniquement essayer toovalidate un numéro de téléphone 5 fois au sein d’une heure avant d’être verrouillé pendant 24 heures. Les utilisateurs peuvent également tenter une même méthode d’authentification seulement 5 fois en une heure, après quoi leur compte est verrouillé pendant 24 heures.
  >
  >
* **Q : pour la durée pendant laquelle sont par courrier électronique hello et SMS code secret valide ?**

  > **R :** hello durée de vie de session pour la réinitialisation du mot de passe est de 105 minutes. À partir du début de hello Hello opération de réinitialisation de mot de passe, utilisateur de hello a 105 minutes tooreset leur mot de passe. Hello par courrier électronique et le code secret à usage unique de SMS ne sont pas valides après l’expiration de cette période.
  >
  >

## <a name="password-change"></a>Modification de mot de passe
* **Q : où les utilisateurs doivent accéder toochange leurs mots de passe ?**

  > **R :** les utilisateurs peuvent modifier leurs mots de passe n’importe où ils voient leur photo de profil ou d’une icône (comme dans le coin supérieur droit hello de leurs [Office 365](https://portal.office.com) ou [volet d’accès](https://myapps.microsoft.com) rencontre. Les utilisateurs peuvent modifier leurs mots de passe à partir de hello [page de profil de panneau d’accès](https://account.activedirectory.windowsazure.com/r#/profile). Les utilisateurs peuvent également être posées toochange leurs mots de passe automatiquement à l’écran de connexion hello Azure AD si leurs mots de passe ont expiré. Enfin, les utilisateurs peuvent naviguer toohello [portail de modification de mot de passe Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directement s’ils le souhaitent toochange leurs mots de passe.
  >
  >
* **Q : Mes utilisateurs notifiées Bonjour portail Office lors de l’expiration de leur mot de passe local ?**

  > **R :** cela est possible aujourd'hui si vous utilisez AD FS en suivant les instructions hello ici : [envoyer des revendications de stratégie de mot de passe avec ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396). Si vous utilisez la synchronisation de hachage de mot de passe, ces notifications ne sont pas prises en charge actuellement. C’est parce que nous ne pas synchroniser les stratégies de mot de passe du site, il est donc pas possible pour nous toocloud de notifications d’expiration toopost rencontre. Dans les deux cas, il est également possible trop[avertir les utilisateurs dont les mots de passe sont sur tooexpire à l’aide de PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).
  >
  >

## <a name="password-management-reports"></a>Rapports sur la gestion des mots de passe
* **Q : combien de temps faut-il pour tooshow données haut sur les rapports de gestion des mots de passe hello ?**

  > **R :** données doivent apparaître sur les rapports de gestion des mots de passe hello dans les 5 à 10 minutes. Il certaines instances peut prendre jusqu'à tooan heure tooappear.
  >
  >
* **Q : Comment puis-je filtrer les rapports de gestion des mots de passe hello ?**

  > **R :** vous pouvez filtrer les rapports de gestion des mots de passe hello en cliquant sur hello petite loupe toohello extrême droite des étiquettes de colonne hello, haut hello du rapport de hello. Si vous souhaitez toodo de filtrage plus précis, vous pouvez télécharger hello rapport tooexcel et créer un tableau croisé dynamique.
  >
  >
* **Q : quel est le nombre maximal de hello d’événements sont stockés dans les rapports de gestion des mots de passe hello ?**

  > **R :** des too75, 000 mot de passe réinitialisation ou mot de passe réinitialisation d’inscription événements est stockée dans les rapports de gestion de mot de passe hello, fractionnement sauvegarder too30 jours.  Nous travaillons tooexpand ce numéro tooinclude davantage d’événements.
  >
  >
* **Q : comment lointaine faire hello des rapports de gestion de mot de passe ?**

  > **R :** des rapports de gestion des mots de passe hello afficher les opérations qui se produisent au sein de hello 30 derniers jours. Pour l’instant, si vous devez tooarchive ces données, vous pouvez télécharger régulièrement des rapports de hello et les enregistrer dans un emplacement distinct.
  >
  >
* **Q : existe-t-il un nombre maximal de lignes qui peuvent s’afficher dans les rapports de gestion des mots de passe hello ?**

  > **R :** Oui, un maximum de 75 000 lignes peut-être apparaître sur l’un des rapports de gestion de mot de passe hello, si elles sont en cours indiquées dans hello téléchargées ou l’interface utilisateur.
  >
  >
* **Q : existe-t-il une tooaccess API hello mot de passe réinitialisation ou enregistrement données de rapports ?**

  > **R :** Oui, consultez hello suivants documentation toolearn comment vous pouvez accéder à un mot de passe hello réinitialiser les flux de données création de rapports.  [Découvrez comment tooaccess le mot de passe réinitialisé les événements de rapports par programme](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).
  >
  >

## <a name="password-writeback"></a>Réécriture du mot de passe
* **Q : comment fonctionne l’écriture différée de mot de passe de travail coulisses hello ?**

  > **R :** consultez [le fonctionnement de l’écriture différée de mot de passe](active-directory-passwords-writeback.md) pour une explication de ce qui se produit lorsque vous activez l’écriture différée de mot de passe et le flux des données via le système de hello dans votre environnement local.
  >
  >
* **Q : combien de temps l’écriture différée de mot de passe ne prend pas toowork ?  Y a-t-il un délai de synchronisation comme avec la synchronisation du hachage de mot de passe ?**

  > **R :** L’écriture différée du mot de passe est instantanée. Il s’agit d’un pipeline synchrone qui fonctionne différemment de la synchronisation du hachage de mot de passe. L’écriture différée de mot de passe permet aux utilisateurs tooget les commentaires en temps réel sur la réussite de leur mot de passe du hello réinitialiser ou modifier l’opération. temps moyen de Hello pour une écriture différée réussie d’un mot de passe est inférieure à 500 ms.
  >
  >
* **Q : Si mon compte local est désactivé, comment mon compte/accès cloud est-il affecté ?**

  > **R :** si votre ID local est désactivé, votre cloud ID ou d’y accéder seront également désactivée au prochain intervalle de synchronisation hello via la connexion à AAD par défaut de DECUBITUS Voici toutes les 30 minutes.
  >
  >
* **Q : si mon compte local est contraint par une stratégie de mot de passe Active Directory local, SSPR obéissent aux règles de cette stratégie lors de la modification du mot de passe hello ?**

  > **R :** Oui, SSPR s’appuie sur et à respecter hello local stratégie de mot de passe AD, y compris classique stratégie de mot de passe de domaine Active Directory, ainsi que toutes les stratégies de mot de passe affinée définies ciblés tooa donné utilisateur.
  >
  >
* **Q : Pour quels types de compte l’écriture différée du mot de passe fonctionne-t-elle ?**

  > **R :** L’écriture différée du mot de passe fonctionne pour les utilisateurs fédérés et ceux disposant de la synchronisation du hachage de mot de passe.
  >
  >
* **Q : L’écriture différée du mot de passe applique-t-elle les stratégies de mot de passe de mon domaine ?**

  > **R :** Oui, l’écriture différée du mot de passe applique l’âge du mot de passe, l’historique, la complexité, les filtres et toute autre restriction que vous pouvez mettre en place sur les mots de passe dans votre domaine local.
  >
  >
* **Q : L’écriture différée du mot de passe est-elle sécurisée ?  Comment puis-je être sûr de ne pas être piraté ?**

  > **R :** Oui, l’écriture différée du mot de passe est sécurisée. tooread en savoir plus sur les couches de hello quatre de sécurité implémenté par le service de l’écriture différée de mot de passe hello, extraire hello [modèle de sécurité de l’écriture différée de mot de passe](active-directory-passwords-writeback.md#password-writeback-security-model) section dans le fonctionnement de l’écriture différée de mot de passe.
  >
  >

## <a name="next-steps"></a>Étapes suivantes

Hello suivant liens fournit des informations supplémentaires concernant le mot de passe réinitialisé à l’aide d’Azure AD

* [**Démarrage rapide**](active-directory-passwords-getting-started.md) : soyez rapidement opérationnel avec la gestion des mots de passe en libre-service d’Azure AD. 
* [**Licences**](active-directory-passwords-licensing.md) : configurez vos licences Azure AD.
* [**Données** ](active-directory-passwords-data.md) : comprendre les données de hello est nécessaire et comment il est utilisé pour la gestion de mot de passe
* [**Déploiement** ](active-directory-passwords-best-practices.md) -planifier et déployer des utilisateurs de tooyour SSPR hello d’aide est disponible ici
* [**Personnaliser** ](active-directory-passwords-customize.md) -personnaliser hello apparence Hello SSPR expérience pour votre entreprise.
* [**Rapports**](active-directory-passwords-reporting.md) : découvrez si, quand et où vos utilisateurs accèdent aux fonctionnalités de réinitialisation de mot de passe en libre-service
* [**Stratégie**](active-directory-passwords-policy.md) : comprenez et définissez les stratégies de mot de passe d’Azure AD
* [**Écriture différée de mot de passe**](active-directory-passwords-writeback.md) - fonctionnement de l’écriture différée de mot de passe avec votre annuaire local
* [**Présentation approfondie technique** ](active-directory-passwords-how-it-works.md) -accédez derrière hello RIDEAU toounderstand son fonctionnement
* [**Résoudre les problèmes** ](active-directory-passwords-troubleshoot.md) -en savoir comment tooresolve commun problèmes que nous pouvons voir avec SSPR
