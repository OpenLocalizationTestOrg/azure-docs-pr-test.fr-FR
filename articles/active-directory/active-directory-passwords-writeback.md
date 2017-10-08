---
title: "Réinitialisation de mot de passe en libre-service Azure AD avec réécriture du mot de passe | Microsoft Docs"
description: "À l’aide d’Azure AD et Azure AD directory tooon local de se connecter toowriteback des mots de passe"
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
ms.openlocfilehash: 6a1dd964a51b4f3b5b0be303b722ab6deb4a6110
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="password-writeback-overview"></a>Vue d’ensemble de la réécriture du mot de passe

L’écriture différée de mot de passe permet de que vous les mots de passe toowrite tooconfigure AD Azure sauvegarder tooyou locale Active Directory. Il supprime hello besoin tooset des et gérer une solution de réinitialisation de mot de passe libre-service compliquée localement, et il fournit un moyen pratique de nuage pour votre tooreset utilisateurs leur mot de passe local où qu’ils soient. La réécriture du mot de passe est un composant [Azure Active Directory Connect](./connect/active-directory-aadconnect.md) qui peut être activé et utilisé par les abonnés actifs des [éditions Premium d’Azure Active Directory](active-directory-editions.md).

L’écriture différée de mot de passe fournit hello suivant de fonctionnalités

* **Retour d’informations immédiat** : l’écriture différée de mot de passe est une opération synchrone. Vos utilisateurs sont informés immédiatement si leur mot de passe n’a pas respecté la stratégie ou a été toobe n’a pas pu réinitialiser ou modifié pour une raison quelconque.
* **Prend en charge la réinitialisation des mots de passe des utilisateurs à l’aide des services AD FS ou autres technologies de fédération** -l’écriture différée de mot de passe, tant que hello comptes des utilisateurs fédérés sont synchronisés dans votre locataire Azure AD, elles sont en mesure de toomanage leurs AD local mots de passe du cloud de hello.
* **Prend en charge la réinitialisation des mots de passe pour les utilisateurs à l’aide de [synchronisation du hachage de mot de passe](./connect/active-directory-aadconnectsync-implement-password-synchronization.md)**  : quand un service de réinitialisation du mot de passe hello détecte qu’un compte d’utilisateur synchronisé est activé pour la synchronisation du hachage de mot de passe, nous avons réinitialisé à la fois ce compte en local et le mot de passe de cloud computing simultanément.
* **Prend en charge la modification des mots de passe à partir de hello accéder au panneau de configuration et Office 365** : quand fédéré ou mot de passe synchronisé utilisateurs arrivé toochange leurs mots de passe a expiré ou non, nous écrivons ces environnement précédent tooyour AD local de mots de passe.
* **Prend en charge l’écriture différée des mots de passe lorsqu’un administrateur les réinitialise à partir de hello portail Azure** - lorsqu’un administrateur réinitialise le mot de passe d’un utilisateur Bonjour [portail Azure](https://portal.azure.com)si cet utilisateur est fédéré ou mot de passe synchronisé, nous mettrons hello mot de passe hello admin sélectionne sur votre AD local, ainsi. Il est actuellement pas pris en charge dans hello portail d’administration Office.
* **Applique votre site sur les stratégies de mot de passe Active Directory** : quand un utilisateur réinitialise son mot de passe, nous assurer qu’il répond à votre site avant de le valider toothat active par une stratégie AD. Cela comprend l’historique, la complexité, l’âge, les filtres de mot de passe et toute autre restriction de mot de passe que vous avez définie dans votre annuaire Active Directory local.
* **Ne nécessite pas les règles de pare-feu entrantes** -l’écriture différée de mot de passe utilise un relais Service Bus de Azure comme un canal de communication sous-jacent, ce qui signifie que que vous n’avez pas tooopen de ports entrants sur votre pare-feu pour toowork de cette fonctionnalité.
* **Aucune prise en charge pour les comptes d’utilisateur qui existent dans des groupes protégés dans votre annuaire Active Directory local.** : pour plus d’informations sur les groupes protégés, consultez la page [Comptes et groupes protégés dans Active Directory](https://technet.microsoft.com/library/dn535499.aspx).

## <a name="how-password-writeback-works"></a>Fonctionnement de la réécriture du mot de passe

Lors de la synchronisation d’un hachage de mot de passe ou fédéré utilisateur proviennent de tooreset ou modifier leur mot de passe dans le cloud de hello, hello suivante se produit :

1. Nous vérifions toosee le type d’utilisateur de hello de mot de passe.
    * Si nous constatons que le mot de passe hello est géré localement
        * Nous vérifions si hello dans le service d’écriture différée est activé et en cours d’exécution, s’il s’agit, nous laissons utilisateur de hello continuer
        * Si service d’écriture différée hello n’est pas actif, nous signalons à hello utilisateur que son mot de passe ne peut pas être réinitialisée maintenant
2. Ensuite, utilisateur de hello transmet les portails d’authentification appropriés hello et atteint l’écran de hello réinitialisation du mot de passe.
3. Hello l’utilisateur sélectionne un nouveau mot de passe et il confirme.
4. Lorsque vous cliquez sur Envoyer, nous chiffrons le mot de passe en texte clair hello avec une clé symétrique qui a été créée au cours du processus d’installation de l’écriture différée hello.
5. Après avoir chiffré le mot de passe hello, nous l’inclure dans une charge utile qui est envoyée via un relais HTTPS canal tooyour spécifiques du client service bus (que nous configurons également pour vous pendant le processus d’installation de l’écriture différée hello). Ce relais est protégé par un mot de passe généré de manière aléatoire, connu uniquement de votre installation locale.
6. Une fois que le message de salutation a atteint service bus, hello point de terminaison de réinitialisation du mot de passe automatiquement réveille et découvre qu’une demande de réinitialisation en attente.
7. Hello service recherche alors utilisateur de hello en question en utilisant l’attribut d’ancrage cloud hello. Pour cette toosucceed recherche :

    * objet d’utilisateur Hello doit exister dans hello espace de connecteur AD
    * Hello utilisateur objet doit être lié toohello correspondante MV
    * objet d’utilisateur Hello doit être lié toohello objet de connecteur AAD correspondant.
    * Hello lien à partir d’Active Directory connector objet tooMV doit avoir règle de synchronisation hello `Microsoft.InfromADUserAccountEnabled.xxx` sur le lien de hello. <br> <br>
    Lors de l’appel de hello proviennent cloud de hello, moteur de synchronisation hello utilise hello toolook d’attribut cloudAnchor d’objet d’espace de connecteur AAD hello, suit hello lien précédent toohello MV objet, puis retour toohello AD objet lien de hello. Car il peut y avoir plusieurs objets Active Directory (plusieurs forêts) pour le même utilisateur, le moteur de synchronisation hello s’appuie sur hello de hello `Microsoft.InfromADUserAccountEnabled.xxx` hello toopick de lien corrigez une.

    > [!Note]
    > À la suite de cette logique, Azure AD Connect doit être en mesure de toocommunicate avec hello émulateur PDC pour toowork de l’écriture différée de mot de passe. Si vous devez manuellement tooenable, Azure AD Connect toohello émulateur PDC peuvent se connecter en cliquant sur hello **propriétés** de connecteur de synchronisation Active Directory hello, puis en sélectionnant **configurer les partitions d’annuaire**. À partir de là, recherchez hello **les paramètres de connexion de contrôleur de domaine** section et case hello intitulée **utiliser uniquement les contrôleurs de domaine par défaut**. Même si hello préféré de que contrôleur de domaine n’est pas un émulateur de contrôleur de domaine principal, Azure AD Connect va tenter de tooconnect toohello contrôleur de domaine principal pour l’écriture différée de mot de passe.

8. Une fois que le compte d’utilisateur hello est trouvé, nous tentons de mot de passe tooreset hello directement dans la forêt Active Directory appropriée hello.
9. Si l’opération de définition du mot de passe hello réussit, nous signalons à hello utilisateur que son mot de passe a été modifié.
    > [!NOTE]
    > Dans les cas de hello lorsque hello mot de passe utilisateur est synchronisé tooAzure AD à l’aide de la synchronisation de mot de passe, il est probable que la stratégie de mot de passe d’on-premises hello est inférieure à celle de la stratégie de mot de passe de cloud hello. Dans ce cas, nous applique toujours toute stratégie d’on-premises hello est et d’autoriser un mot de passe hachage hachage synchronisation toosynchronize hello ce mot de passe. Cela garantit que votre stratégie locale est appliquée dans le cloud de hello, sans que si vous utilisez tooprovide de fédération ou de la synchronisation de mot de passe sur l’authentification unique.

10. Si le mot de passe de hello défini l’opération échoue, nous renvoyer hello erreur toohello utilisateur et laissons réessayer.
    * opération de Hello peut échouer en raison des éléments suivants de hello
        * Hello service est arrêté
        * mot de passe Hello qu’ils ont sélectionné ne répondait pas aux stratégies de l’organisation
        * Impossible de trouver les utilisateur hello Bonjour AD local

    Nous avons spécifique à un message pour la plupart de ces cas et indiquer à l’utilisateur de hello leur problème de hello tooresolve.

## <a name="configuring-password-writeback"></a>Configuration de la réécriture du mot de passe

Nous vous recommandons d’utiliser fonctionnalité de mise à jour automatique hello de [Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md) si vous souhaitez que l’écriture différée de mot de passe toouse.

DirSync et Azure AD Sync ne sont plus prises en charge des moyens de l’activation de l’article hello de l’écriture différée de mot de passe [mise à niveau de DirSync et Azure AD Sync](connect/active-directory-aadconnect-dirsync-deprecated.md) a plus d’informations toohelp, avec votre transition.

Hello étapes suivantes supposent que vous avez déjà configuré Azure AD Connect dans votre environnement à l’aide de hello [Express](./connect/active-directory-aadconnect-get-started-express.md) ou [personnalisé](./connect/active-directory-aadconnect-get-started-custom.md) paramètres.

1. tooconfigure et activer l’écriture différée de mot de passe se connecter tooyour Azure AD Connect server et démarrer hello **Azure AD Connect** Assistant de configuration.
2. Écran d’accueil hello sur **configurer**.
3. Hello supplémentaires sur les tâches de l’écran cliquez sur **personnaliser les options de synchronisation** , puis **suivant**.
4. Sur l’écran tooAzure AD de se connecter hello, entrez une information d’identification d’administrateur Global et choisissez **suivant**.
5. Sur hello connecter vos répertoires et le domaine et unité d’organisation de filtrage des écrans que vous pouvez choisir **suivant**.
6. Sur l’écran de fonctionnalités facultatives hello hello case à cocher ensuite trop**l’écriture différée de mot de passe** et cliquez sur **suivant**.
   ![Activation de l’écriture différée du mot de passe dans Azure AD Connect][Writeback]
7. Écran de prêt tooconfigure hello sur **configurer** et attendez hello processus toocomplete.
8. Lorsque Configuration terminée s’affiche, vous pouvez cliquer sur **Quitter**

## <a name="licensing-requirements-for-password-writeback"></a>Conditions de licence pour la réécriture du mot de passe

Pour plus d’informations concernant les licence, consultez les rubrique hello [licences nécessaires pour l’écriture différée de mot de passe](active-directory-passwords-licensing.md#licenses-required-for-password-writeback) ou hello suit les sites

* [Site de tarification d’Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Secure Productive Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

### <a name="on-premises-authentication-modes-supported-for-password-writeback"></a>Modes d’authentification locale pris en charge pour la réécriture du mot de passe

L’écriture différée de mot de passe fonctionne pour hello les types de mot de passe d’utilisateur suivants :

* **Utilisateurs cloud uniquement** : l’écriture différée du mot de passe ne s’applique pas dans cette situation, faute de mot de passe local
* **Utilisateurs dont le mode passe est synchronisé** : réécriture du mot de passe prise en charge
* **Utilisateurs fédérés** : réécriture du mot de passe prise en charge
* **Utilisateurs à authentification directe** : réécriture du mot de passe prise en charge

### <a name="user-and-admin-operations-supported-for-password-writeback"></a>Opérations de l’utilisateur et de l’administrateur prises en charge pour la réécriture du mot de passe

Les mots de passe mis à jour dans tous les hello suivant situations :

* **Opérations de l’utilisateur final prises en charge**
  * Toute modification volontaire en libre-service du mot de passe de l’utilisateur final
  * Toute modification forcée en libre-service du mot de passe de l’utilisateur final (par exemple, expiration du mot de passe)
  * Réinitialisation de n’importe quel mot de passe libre-service par l’utilisateur provenant de hello [portail de réinitialisation de mot de passe](https://passwordreset.microsoftonline.com)
* **Opérations de l’administrateur final prises en charge**
  * Toute modification volontaire en libre-service du mot de passe de l’administrateur
  * Toute modification forcée en libre-service du mot de passe de l’administrateur (par exemple, expiration du mot de passe)
  * N’importe quel mot de passe libre-service administrateur réinitialiser provenant de hello [portail de réinitialisation de mot de passe](https://passwordreset.microsoftonline.com)
  * N’importe quel mot de passe par l’administrateur de l’utilisateur final réinitialiser à partir de hello [portail Azure classic](https://manage.windowsazure.com)
  * N’importe quel mot de passe par l’administrateur de l’utilisateur final réinitialiser à partir de hello [portail Azure](https://portal.azure.com)

### <a name="user-and-admin-operations-not-supported-for-password-writeback"></a>Opérations de l’utilisateur et de l’administrateur non prises en charge pour la réécriture du mot de passe

Les mots de passe sont **pas** écrit dans des hello suivant situations :

* **Opérations de l’utilisateur final non prises en charge**
  * N’importe quel utilisateur final réinitialiser leur mot de passe à l’aide de PowerShell v1, v2 ou hello API Azure AD Graph
* **Opérations de l’administrateur non prises en charge**
  * N’importe quel mot de passe par l’administrateur de l’utilisateur final réinitialiser à partir de hello [portail de gestion Office](https://portal.office.com)
  * Réinitialise à partir de PowerShell v1, v2, de n’importe quel mot de passe par l’administrateur de l’utilisateur final ou hello API Azure AD Graph

Pendant que nous travaillons tooremove ces limitations, nous n’avons pas une chronologie spécifique, que nous pouvons partager encore.

## <a name="password-writeback-security-model"></a>Modèle de sécurité de la réécriture du mot de passe

La réécriture du mot de passe est un service hautement sécurisé.  tooensure que vos informations sont protégées, nous activons un modèle à 4 niveaux de sécurité qui est décrite ci-dessous.

* **Relais de Service Bus propre au client**
  * Lorsque vous configurez le service de hello, nous configurons un locataire-relais service bus spécifique qui est protégé par un mot de passe fort généré de manière aléatoire que Microsoft a jamais accès.
* **Clé de chiffrement de mot de passe forte et verrouillée**
  * Après la création de relais hello service bus, nous créer une clé symétrique forte, nous utilisons le mot de passe tooencrypt hello car elle provient d’acheminement hello. Cette clé se trouve uniquement dans le magasin des secrets de votre société dans le cloud hello, qui est fortement verrouillé et auditée, tout comme n’importe quel mot de passe dans le répertoire de hello.
* **TLS standard du secteur**
  1. Lorsqu’un mot de passe réinitialiser ou modifier opération se produit dans le cloud de hello, nous prendre le mot de passe en texte clair hello et chiffrer avec votre clé publique.
  2. Nous placer que dans un message HTTPS, ce qui est envoyé via un canal chiffré à l’aide de relais de Microsoft SSL certificats tooyour service bus.
  3. Une fois que message de type hello arrive dans Service Bus, votre agent local sort de veille des et s’authentifie à l’aide du Bus tooService hello mot de passe fort qui a été généré précédemment.
  4. Agent de local récupère le message chiffré de hello, déchiffre à l’aide de la clé privée de hello que nous avons générée.
  5. L’agent de local tente alors de mot de passe tooset hello via hello API SetPassword AD DS.
     * Cette étape est ce que nous permet de tooenforce votre AD local stratégie de mot de passe (complexité, âge, historique, filtres, etc.) dans le cloud de hello.
* **Stratégies d’expiration de message** 
  * Si le message de type hello se situe dans le Bus des services, car votre service local est arrêté, il sera de délai d’attente et supprimé après plusieurs minutes tooincrease encore davantage la sécurité.

### <a name="password-writeback-encryption-details"></a>Informations détaillées sur le chiffrement de la réécriture du mot de passe

les étapes de chiffrement Hello traverse une demande de réinitialisation de mot de passe lorsqu’un utilisateur soumet, avant son arrivée dans votre environnement local, la fiabilité tooensure maximale et la sécurité sont décrites ci-dessous.

* **Étape 1 : chiffrement de mot de passe avec la clé RSA 2048 bits** - une fois qu’un utilisateur soumet un toobe de mot de passe mis à jour tooon local, tout d’abord, hello soumis un mot de passe proprement dit est chiffré avec une clé RSA de 2 048 bits.
* **Étape 2 : chiffrement au niveau du Package avec AES-GCM** - puis hello ensemble du package (mot de passe + métadonnées requises) est chiffré à l’aide d’AES-GCM. Cela empêche toute personne ayant un canal d’accès direct toohello sous-jacent ServiceBus de consultation/falsifier contenu de hello.
* **Étape 3 : toutes les communications se produit sur TLS / SSL** -toutes les communications hello avec ServiceBus se produit dans un canal SSL/TLS. Cela protège le contenu de hello de tiers 3e non autorisés.
* **Substitution de clé automatique tous les six mois** - automatiquement tous les 6 mois, ou chaque fois que l’écriture différée de mot de passe est désactivée / activée de nouveau sur Azure AD Connect, nous substitution toutes ces clés tooensure maximale de service de sécurité et sécurité.

### <a name="password-writeback-bandwidth-usage"></a>Utilisation de la bande passante de la réécriture du mot de passe

L’écriture différée de mot de passe est un service de faible bande passante qui envoie des demandes de sauvegarder l’agent local de toohello uniquement sous hello suivant les circonstances :

1. Deux messages sont envoyés lors de l’activation ou désactivation de fonctionnalité hello via Azure AD Connect.
2. Un message est envoyé une fois toutes les cinq minutes comme une pulsation du service pour tant que service de hello est en cours d’exécution.
3. Deux messages sont envoyés chaque fois qu’un nouveau mot de passe est envoyé
    * Premier message, comme une opération de hello tooperform demande
    * Deuxième message qui contient le résultat de hello d’opération de hello et est envoyé en hello suivant circonstances :
        * Chaque fois qu’un nouveau mot de passe est soumis pendant une réinitialisation de mot de passe libre-service par l’utilisateur.
        * Chaque fois qu’un nouveau mot de passe est soumis pendant une opération de modification de mot de passe par l’utilisateur.
        * Chaque fois qu’un nouveau mot de passe est soumis au cours d’un mot de passe utilisateur d’initialisée par l’administrateur réinitialisé (à partir des portails admin Azure hello uniquement).

#### <a name="message-size-and-bandwidth-considerations"></a>Considérations relatives à la taille des messages et à la bande passante

Hello taille de chaque message de type hello décrite ci-dessus est généralement inférieure à 1 Ko, même sous des charges extrêmes, le service de l’écriture différée de mot de passe hello lui-même utilise quelques kilobits par seconde de la bande passante. Dans la mesure où chaque message est envoyé en temps réel, uniquement lorsque requis par une opération de mise à jour du mot de passe, car la taille des messages hello est si petit, utilisation de la bande passante hello de fonction d’écriture différée hello est effectivement toohave trop petite tout impact mesurable réel.

## <a name="next-steps"></a>Étapes suivantes

Hello suivant liens fournit des informations supplémentaires concernant le mot de passe réinitialisé à l’aide d’Azure AD

* [**Démarrage rapide**](active-directory-passwords-getting-started.md) : soyez rapidement opérationnel avec la gestion des mots de passe en libre-service d’Azure AD. 
* [**Licences**](active-directory-passwords-licensing.md) : configurez vos licences Azure AD.
* [**Données** ](active-directory-passwords-data.md) : comprendre les données de hello est nécessaire et comment il est utilisé pour la gestion de mot de passe
* [**Déploiement** ](active-directory-passwords-best-practices.md) -planifier et déployer des utilisateurs de tooyour SSPR hello d’aide est disponible ici
* [**Personnaliser** ](active-directory-passwords-customize.md) -personnaliser hello apparence Hello SSPR expérience pour votre entreprise.
* [**Stratégie**](active-directory-passwords-policy.md) : comprenez et définissez les stratégies de mot de passe d’Azure AD
* [**Rapports**](active-directory-passwords-reporting.md) : découvrez si, quand et où vos utilisateurs accèdent aux fonctionnalités de réinitialisation de mot de passe en libre-service
* [**Présentation approfondie technique** ](active-directory-passwords-how-it-works.md) -accédez derrière hello RIDEAU toounderstand son fonctionnement
* [**Forum Aux Questions (FAQ)**](active-directory-passwords-faq.md) : Comment ? Pourquoi ? Quoi ? Où ? Qui ? Quand ? -Réponses tooquestions vous souhaitiez toujours tooask
* [**Résoudre les problèmes** ](active-directory-passwords-troubleshoot.md) -en savoir comment tooresolve commun problèmes que nous pouvons voir avec SSPR

[Writeback]: ./media/active-directory-passwords-writeback/enablepasswordwriteback.png "Activation de la réécriture du mot de passe dans Azure AD Connect"
