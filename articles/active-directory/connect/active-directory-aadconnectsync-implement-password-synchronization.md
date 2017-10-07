---
title: synchronisation de mot de passe aaaImplement avec synchronisation Azure AD Connect | Documents Microsoft
description: Fournit des informations sur comment fonctionne de la synchronisation de mot de passe et tooset des.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 05f16c3e-9d23-45dc-afca-3d0fa9dbf501
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: a0401640f2a4d914419ee4446f923bb3a972389d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-password-synchronization-with-azure-ad-connect-sync"></a>Implémenter la synchronisation de mot de passe avec la synchronisation Azure AD Connect
Cet article fournit des informations que vous avez besoin toosynchronize vos mots de passe utilisateur depuis une local Active instance tooa basée sur le cloud Azure Active Directory (Azure AD) instance de l’annuaire.

## <a name="what-is-password-synchronization"></a>Qu'est-ce que la synchronisation de mot de passe ?
Hello la probabilité que vous êtes bloqué à partir de la réalisation de votre travail en raison d’un mot de passe oublié de tooa concerne toohello nombre de mots de passe différents, vous devez tooremember. Bonjour plusieurs mots de passe vous devez tooremember, hello supérieur hello probabilité tooforget une. Questions et des appels sur les réinitialisations de mot de passe et d’autres à la demande de problèmes liés au mot de passe hello la plupart des ressources de support technique.

Synchronisation de mot de passe est qu'une fonctionnalité utilisée toosynchronize mots de passe utilisateur d’une instance de tooa basée sur le cloud Azure AD instance locale Active Directory.
Utiliser cette fonctionnalité toosign dans les services de tooAzure AD comme Office 365, Microsoft Intune, CRM Online et les Services de domaine d’Active Directory Azure (Azure AD DS). Vous vous connectez toohello service à l’aide de hello même mot de passe toosign dans tooyour local instance Active Directory.

![Qu’est-ce qu’Azure AD Connect ?](./media/active-directory-aadconnectsync-implement-password-synchronization/arch1.png)

En réduisant le nombre de hello des mots de passe, vos utilisateurs doivent toojust toomaintain une. La synchronisation de mot de passe vous aide à :

* Améliorer la productivité de hello de vos utilisateurs.
* Réduire vos coûts de support technique.  

En outre, si vous décidez de toouse [fédération avec Active Directory Federation Services (ADFS)](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect), vous pouvez éventuellement définir la synchronisation de mot de passe de sauvegarde en cas d’échec de votre infrastructure AD FS.

Synchronisation de mot de passe est une fonctionnalité de synchronisation directory extension toohello implémentée par la synchronisation Azure AD Connect. synchronisation de mot de passe toouse dans votre environnement, vous devez :

* Installer Azure AD Connect.  
* Configurez la synchronisation d’annuaire entre votre instance Active Directory locale et votre instance Azure Active Directory.
* Activer la synchronisation de mot de passe.

Pour plus d’informations, consultez [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).

> [!NOTE]
> Pour plus d'informations sur les services de domaine Azure Active Directory configurés pour la synchronisation de mot de passe et FIPS, consultez « Synchronisation du mot de passe et FIPS » plus loin dans cet article.
>
>

## <a name="how-password-synchronization-works"></a>Fonctionnement de la synchronisation de mot de passe
Hello service de domaine Active Directory stocke les mots de passe sous forme de hello d’une représentation sous forme de valeur de hachage de mot de passe de l’utilisateur réel hello. Une valeur de hachage est le résultat d’une fonction mathématique unidirectionnelle (hello *algorithme de hachage*). Il n’existe aucun résultat de hello méthode toorevert d’une version de texte brut toohello fonction à sens unique d’un mot de passe. Vous ne pouvez pas utiliser un toosign de hachage de mot de passe dans le réseau local de tooyour.

votre mot de passe, la synchronisation Azure AD Connect extrait le hachage de mot de passe à partir de toosynchronize hello instance d’Active Directory local. Traitement de sécurité supplémentaire est appliqué toohello hachage de mot de passe avant qu’il soit synchronisé le service d’authentification Azure Active Directory toohello. Les mots de passe sont synchronisés pour chaque utilisateur et par ordre chronologique.

flux de données réelles Hello du processus de synchronisation de mot de passe hello est similaire synchronisation toohello des données utilisateur telles que le nom d’affichage ou les adresses de messagerie. Toutefois, les mots de passe sont synchronisés plus fréquemment que la fenêtre de synchronisation d’annuaires standard hello pour d’autres attributs. processus de synchronisation de mot de passe Hello s’exécute toutes les 2 minutes. Vous ne pouvez pas modifier la fréquence hello de ce processus. Lorsque vous synchronisez un mot de passe, elle remplace le mot de passe de cloud computing existant hello.

Hello première fois que vous activez la fonctionnalité de synchronisation de mot de passe hello, il effectue une synchronisation initiale des mots de passe hello de tous les utilisateurs dans l’étendue. Vous ne peut pas définir explicitement un sous-ensemble des mots de passe utilisateur que vous souhaitez toosynchronize.

Lorsque vous modifiez un mot de passe local, hello mise à jour de mot de passe est synchronisé, plus souvent en quelques minutes.
fonctionnalité de synchronisation de mot de passe Hello tente automatiquement de tentatives de synchronisation a échoué. Si une erreur produit pendant une tentative toosynchronize un mot de passe, une erreur est consignée dans l’Observateur d’événements.

synchronisation Hello de mot de passe n’a aucun impact sur l’utilisateur hello qui est actuellement connecté.
Votre session de service cloud en cours n’est pas immédiatement affectée par une modification de mot de passe synchronisé qui se produit quand vous êtes connecté dans le service cloud tooa. Toutefois, lorsque le service cloud hello requiert tooauthenticate à nouveau, vous devez tooprovide votre nouveau mot de passe.

Un utilisateur doit entrer leurs informations d’identification d’entreprise un tooAzure tooauthenticate de deuxième temps AD, quelle que soit la qu’elles sont signées tootheir réseau d’entreprise. Ces modèle peut être réduite, toutefois, si l’utilisateur de hello sélectionne les hello maintenir la connexion dans la case à cocher (KMSI) au niveau de la connexion. Cette sélection définit un cookie de session qui ignore l’authentification pendant une courte période. Comportement KMSI peut être activé ou désactivé par l’administrateur d’Azure AD hello.

> [!NOTE]
> Synchronisation de mot de passe est uniquement pris en charge pour l’utilisateur de type hello objet dans Active Directory. Il n’est pas pris en charge pour le type d’objet iNetOrgPerson hello.

### <a name="detailed-description-of-how-password-synchronization-works"></a>Description détaillée du fonctionnement de la synchronisation des mots de passe
suivant de Hello décrit en détail comment fonctionne la synchronisation de mot de passe entre Active Directory et Azure AD.

![Flux de travail détaillé des mots de passe](./media/active-directory-aadconnectsync-implement-password-synchronization/arch3.png)


1. Toutes les deux minutes, agent de synchronisation de mot de passe de hello sur le serveur de connexion hello AD demande des hachages de mot de passe stocké (l’attribut unicodePwd hello) à partir d’un contrôleur de domaine via hello standard [MS-DRSR](https://msdn.microsoft.com/library/cc228086.aspx) protocole de réplication utilisé toosynchronize données entre les contrôleurs de domaine. compte de service de Hello doit disposer de répliquer les modifications d’annuaire et les hachages de mot de passe répliquer Active toutes les modifications AD autorisations (par défaut sur l’installation) tooobtain hello.
2. Avant d’envoyer, hello DC chiffre le hachage de mot de passe hello MD4 à l’aide d’une clé qui est un [MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) hachage de clé de session RPC hello et d’un salt. Il envoie ensuite l’agent de synchronisation de mot de passe hello résultat toohello via RPC. Hello contrôleur de domaine passe également l’agent de synchronisation hello salt toohello en utilisant le protocole de réplication hello contrôleur de domaine, pour que l’agent de hello soient enveloppe de hello toodecrypt en mesure de.
3.  Agent de synchronisation de mot de passe hello après l’enveloppe chiffrée de hello, il utilise [MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx) et hello salt toogenerate toodecrypt clé hello reçu tooits arrière d’origine MD4 format de données. À aucun moment l’agent de synchronisation du mot de passe hello a accès toohello mot de passe. Hello utilisation de l’agent de synchronisation de mot de passe de MD5 est strictement pour la compatibilité de protocole de réplication avec hello contrôleur de domaine, et il est utilisé uniquement en local entre hello contrôleur de domaine et l’agent de synchronisation de mot de passe hello.
4.  agent de synchronisation de mot de passe Hello développe les octets de too64 de hachage de mot de passe binaire de 16 octets hello par la première conversion hello hachage tooa 32 octets chaîne hexadécimale, ensuite convertir cette chaîne dans le fichier binaire avec l’encodage UTF-16.
5.  agent de synchronisation de mot de passe Hello ajoute un salt, composé d’un salt de 10 octets, toofurther binaire de 64 octets toohello protéger hachage d’origine de hello.
6.  agent de synchronisation de mot de passe Hello puis combine le hachage de hello MD4 plus salt et les entrées qu’il en hello [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt) (fonction). 1000 itérations Hello [HMAC-SHA256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) algorithme de hachage à clé est utilisée. 
7.  agent de synchronisation de mot de passe Hello prend la valeur de hachage de 32 octets obtenue hello, concatène deux sel de salutation hello nombre de tooit d’itérations SHA256 (pour une utilisation par Azure AD), puis transmet la chaîne hello à partir d’Azure AD Connect tooAzure AD via le protocole SSL.</br> 
8.  Lorsqu’un utilisateur tente de toosign dans tooAzure AD et passe à leur mot de passe, le mot de passe hello sont exécutée via hello MD4 même + salt + PBKDF2 + HMAC-SHA256 processus. Si le hachage obtenu de hello correspond au hachage hello stocké dans Azure AD, hello a entré un mot de passe correct hello et est authentifié. 

>[!Note] 
>hachage MD4 d’origine de Hello n’est pas transmis tooAzure AD. Au lieu de cela, hello hachage SHA256 de hachage MD4 d’origine de hello est transmis. Par conséquent, si hachage hello stocké dans Azure AD est obtenu, il ne peut pas être utilisé dans une attaque pass-the-hash de local.

### <a name="how-password-synchronization-works-with-azure-active-directory-domain-services"></a>Fonctionnement de la synchronisation de mot de passe avec Azure Active Directory Domain Services
Vous pouvez également utiliser toosynchronize de fonctionnalité de synchronisation de mot de passe hello vos mots de passe local trop[Azure des Services de domaine Active Directory](../../active-directory-domain-services/active-directory-ds-overview.md). Dans ce scénario, instance d’Azure Active Directory Domain Services hello authentifie les utilisateurs dans le cloud de hello avec toutes les méthodes de hello disponibles dans votre instance d’Active Directory local. expérience de Hello de ce scénario est similaire toousing hello outil de Migration Active Directory (ADMT) dans un environnement sur site.

### <a name="security-considerations"></a>Considérations relatives à la sécurité
Lors de la synchronisation des mots de passe, version de votre mot de passe en texte brut hello n’est pas fonctionnalité de synchronisation de mot de passe toohello exposé, tooAzure AD ou l’un des services de hello associé.

Authentification de l’utilisateur a lieu auprès d’Azure AD, plutôt que par rapport à l’instance Active Directory de l’organisation hello. Si votre organisation a des problèmes sur les données de mot de passe dans un format en laissant hello local, considérez les faits hello que les données de mot de passe SHA256 stockées dans Azure AD--hello un hachage de hachage MD4 d’origine hello--est beaucoup plus sûre que ce qui est stocké dans Active Directory. En outre, étant donné que ce hachage SHA256 ne peut pas être déchiffré, il ne peut pas remettre en environnement Active Directory de l’organisation toohello et présenté sous la forme d’un mot de passe d’utilisateur valide dans une attaque pass-the-hash.





### <a name="password-policy-considerations"></a>Remarques sur les stratégies de mot de passe
Deux types de stratégies de mot de passe sont affectés par l’activation de la synchronisation de mot de passe :

* Stratégie de complexité de mot de passe
* Stratégie d’expiration de mot de passe

#### <a name="password-complexity-policy"></a>Stratégie de complexité de mot de passe  
Lorsque la synchronisation de mot de passe est activée, les stratégies de complexité de mot de passe hello dans votre instance d’Active Directory local remplacent la stratégie dans le cloud hello pour les utilisateurs synchronisés. Vous pouvez utiliser tous les mots de passe valides hello à partir de votre ordinateur local Active Directory instance tooaccess services Azure AD.

> [!NOTE]
> Les mots de passe pour les utilisateurs qui sont créés directement dans le cloud de hello existe toujours des stratégies de toopassword objet tel que défini dans le cloud de hello.

#### <a name="password-expiration-policy"></a>Stratégie d’expiration de mot de passe  
Si un utilisateur est dans la portée de hello de synchronisation de mot de passe, le mot de passe de compte hello cloud est défini trop*n’expirent jamais*.

Vous pouvez continuer toosign dans les services de cloud computing tooyour à l’aide d’un mot de passe synchronisé a expiré dans votre environnement local. La mise à jour de votre mot de passe cloud hello la prochaine fois que vous modifiez le mot de passe hello dans l’environnement local de hello.

#### <a name="account-expiration"></a>Expiration du compte
Si votre organisation utilise un attribut d’accountExpires hello dans le cadre de la gestion des comptes utilisateur, sachez que cet attribut n’est pas synchronisé tooAzure AD. Par conséquent, un compte Active Directory expiré dans un environnement configuré pour la synchronisation de mots de passe sera toujours actif dans Azure AD. Il est recommandé que si le compte de hello a expiré, une action de workflow doit déclencher un script PowerShell qui désactive le compte Azure AD de l’utilisateur hello. Inversement, lorsque le compte de hello est activée, instance d’Azure AD hello doit être activé.

### <a name="overwrite-synchronized-passwords"></a>Remplacement des mots de passe synchronisés
Un administrateur peut réinitialiser manuellement votre mot de passe à l’aide de Windows PowerShell.

Dans ce cas, votre mot de passe synchronisé substitue à nouveau mot de passe hello et toutes les stratégies de mot de passe définis dans le cloud de hello sont appliqués toohello le nouveau mot de passe.

Si vous modifiez à nouveau votre mot de passe local, hello le nouveau mot de passe est synchronisé toohello cloud, et il remplace le mot de passe hello mis à jour manuellement.

synchronisation Hello de mot de passe n’a aucun impact sur hello Azure utilisateur qui est connecté. Votre session de service cloud en cours n’est pas immédiatement affectée par une modification de mot de passe synchronisé qui se produit pendant que vous êtes connecté dans le service cloud tooa. KMSI étend la durée hello de cette différence. Hello cloud service exige que vous tooauthenticate à nouveau, vous devez tooprovide votre nouveau mot de passe.

### <a name="additional-advantages"></a>Autres avantages

- En règle générale, la synchronisation de mot de passe est tooimplement plus simple à un service de fédération. Il ne nécessite pas tous les serveurs supplémentaires et élimine la dépendance sur un tooauthenticate utilisateurs du service de fédération hautement disponible. 
- Synchronisation de mot de passe peut également être activée dans toofederation d’addition. Vous pouvez l’utiliser comme solution de secours si votre service de fédération connaît une défaillance.












## <a name="enable-password-synchronization"></a>Activer la synchronisation de mot de passe
Lorsque vous installez Azure AD Connect à l’aide de hello **paramètres Express** , synchronisation de mot de passe est automatiquement activée. Pour plus d’informations, voir [Prise en main d’Azure AD Connect avec la configuration rapide](active-directory-aadconnect-get-started-express.md).

Si vous utilisez des paramètres personnalisés lorsque vous installez Azure AD Connect, la synchronisation de mot de passe est disponible sur hello utilisateur-page de connexion. Pour plus d’informations, voir [Installation personnalisée d’Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

![Activation de la synchronisation de mot de passe](./media/active-directory-aadconnectsync-implement-password-synchronization/usersignin.png)

### <a name="password-synchronization-and-fips"></a>Synchronisation du mot de passe et FIPS
Si votre serveur a été verrouillé en fonction de tooFederal traitement Standard FIPS (Information), MD5 est désactivée.

**tooenable MD5 pour la synchronisation de mot de passe, effectuez hello comme suit :**

1. Accédez too%programfiles%\Azure AD Sync\Bin.
2. Ouvrez miiserver.exe.config.
3. Atteindre le nœud de configuration/runtime toohello à fin hello du fichier de hello.
4. Ajoutez hello suivant du nœud :`<enforceFIPSPolicy enabled="false"/>`
5. Enregistrez vos modifications.

Pour référence, cet extrait de code indique ce que vous devez obtenir :

```
    <configuration>
        <runtime>
            <enforceFIPSPolicy enabled="false"/>
        </runtime>
    </configuration>
```

Pour plus d'informations sur la sécurité et FIPS, consultez [Synchronisation, cryptage et conformité à la norme FIPS du mot de passe AAD](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/).

## <a name="troubleshoot-password-synchronization"></a>Résoudre les problèmes de synchronisation de mot de passe
Si vous avez des problèmes avec la synchronisation de mot de passe, consultez [Résolution des problèmes de synchronisation du mot de passe](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="next-steps"></a>Étapes suivantes
* [Azure AD Connect Sync : Personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)
