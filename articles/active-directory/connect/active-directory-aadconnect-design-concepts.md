---
title: "Azure AD Connect : principes de conception | Microsoft Docs"
description: "Cette rubrique détaille certains aspects de la conception de l’implémentation"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4114a6c0-f96a-493c-be74-1153666ce6c9
ms.service: active-directory
ms.custom: azure-ad-connect
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1e5d5c6a716ca653fb14fc059e8155124b433732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-design-concepts"></a>Principes de conception Azure AD Connect
Hello cette rubrique vise Zones toodescribe qui doivent être envisagés au cours de la conception de l’implémentation hello d’Azure AD Connect. Il s’agit d’une exploration approfondie de certains aspects. Ces concepts sont également décrits brièvement dans d’autres rubriques.

## <a name="sourceanchor"></a>sourceAnchor
attribut de sourceAnchor Hello est défini en tant que *un attribut immuable pendant la durée de vie hello d’un objet*. Il identifie de façon unique un objet comme étant hello même objet localement et dans Azure AD. attribut de Hello est également appelé **immutableId** et les noms de hello deux sont utilisés interchangeables.

word de Hello immuable, qui est « ne peut pas être modifiée », est important toothis rubrique. Étant donné que la valeur de cet attribut ne peut pas être modifiée une fois qu’elle a été définie, il est important toopick une conception qui prend en charge votre scénario.

attribut de Hello est utilisé pour hello les scénarios suivants :

* Quand un nouveau serveur de moteur de synchronisation est créé ou recréé après un scénario de récupération d’urgence, cet attribut lie les objets existants dans Azure AD à des objets locaux.
* Si vous passez d’un modèle d’identité synchronisé de tooa identité cloud uniquement, cet attribut permet aux objets « correspondance permanente » des objets existants dans Azure AD avec des objets locaux.
* Si vous utilisez la fédération, cet attribut avec hello **userPrincipalName** est utilisé dans hello revendication toouniquely identifier un utilisateur.

Cette rubrique aborde uniquement sourceAnchor en matière de toousers. Hello mêmes règles s’appliquent tooall les types d’objets, mais il est uniquement pour les utilisateurs que ce problème est généralement un problème.

### <a name="selecting-a-good-sourceanchor-attribute"></a>Sélection d’un attribut sourceAnchor approprié
valeur d’attribut Hello doit suivre hello suivant les règles :

* sa longueur doit être inférieure à 60 caractères
  * les caractères autres que a-z, A-Z ou 0-9 sont codés et comptabilisés comme 3 caractères
* elle ne doit pas contenir les caractères spéciaux suivants : &#92; ! # $ % & * + / = ? ^ &#96; { } | ~ < > ( ) ’ ; : , [ ] " @ _
* elle doit être globalement unique
* elle doit être une chaîne, un entier ou une valeur binaire
* elle ne doit pas être basée sur le nom de l’utilisateur, celui-ci est susceptible de changer
* elle ne doit pas respecter la casse et doit éviter les valeurs qui peuvent varier selon la casse
* Doit être attribué lors de la création d’objet de hello

Si hello sélectionné sourceAnchor n’est pas de type chaîne, puis apparaissent de Base64Encode de connexion AD Azure hello attribut valeur tooensure sans caractères spéciaux. Si vous utilisez un autre serveur de fédération à ADFS, assurez-vous que votre serveur peut également attribut de hello Base64Encode.

attribut de sourceAnchor Hello respecte la casse. La valeur « Durand » n’est pas hello identique à « Durand ». Mais vous ne devez pas avoir deux objets différents avec uniquement une différence de casse.

Si vous avez une seule forêt locale, puis attribut hello vous devez utiliser est **objectGUID**. Il s’agit également hello attribut utilisé lorsque vous utilisez les paramètres express dans Azure AD Connect et également hello attribut utilisé par la synchronisation d’annuaire.

Si vous avez plusieurs forêts et que vous ne déplacez pas les utilisateurs entre les forêts et domaines, puis **objectGUID** est un toouse bon attribut même dans ce cas.

Si vous déplacez des utilisateurs entre les forêts et domaines, vous devez trouver un attribut qui ne change pas, ou peut être déplacé avec les utilisateurs de hello pendant le déplacement de hello. Une approche recommandée est toointroduce un attribut synthétique. Un attribut qui peut contenir quelque chose qui ressemble à un GUID serait approprié. Lors de la création d’objet, un nouveau GUID est créé et affecté à un utilisateur de hello. Une règle de synchronisation personnalisés peut être créée dans toocreate de serveur de moteur de synchronisation hello cette valeur en fonction de hello **objectGUID** et mise à jour hello attribut sélectionné dans AD DS. Lorsque vous déplacez les objets hello, assurez-vous que tooalso copier le contenu de cette valeur hello.

Une autre solution consiste à toopick un attribut existant, vous savez ne changent pas. **employeeID**est un des attributs couramment utilisés. Si vous envisagez d’un attribut qui contient des lettres, assurez-vous qu’il y a qu'aucun cas de hello chance (majuscules ou minuscules) ne peut changer pour la valeur de l’attribut hello. Les attributs incorrects qui ne doivent pas être utilisés sont ces attributs avec nom hello d’utilisateur de hello. Dans un mariage et divorce hello est toochange attendu, ce qui n’est pas autorisée pour cet attribut. C’est également une raison pour laquelle des attributs tels que **userPrincipalName**, **mail**, et **targetAddress** ne sont pas tooselect même possible dans l’installation de se connecter hello Azure AD Assistant. Ces attributs contiennent également hello « @ » caractères, ce qui n’est pas autorisée dans hello sourceAnchor.

### <a name="changing-hello-sourceanchor-attribute"></a>Modification d’attribut sourceAnchor hello
valeur de l’attribut sourceAnchor Hello ne peut pas être modifiée après la création de l’objet hello dans Azure AD et l’identité de hello est synchronisée.

Pour cette raison, hello suivant des restrictions s’appliquent tooAzure AD Connect :

* Hello sourceAnchor attribut peut uniquement être défini lors de l’installation initiale. Si vous réexécutez l’Assistant installation Bonjour, cette option est en lecture seule. Si vous devez toochange ce paramètre, vous devez désinstaller et réinstaller.
* Si vous installez un autre serveur d’Azure AD Connect, puis vous devez sélectionnez hello même attribut sourceAnchor précédemment utilisé. Si vous avez précédemment été à l’aide de DirSync et déplacer tooAzure AD vous connecter, vous devez utiliser **objectGUID** car il s’agit d’attribut hello utilisé par la synchronisation d’annuaire.
* Si la valeur hello sourceAnchor est modifiée une fois l’objet de hello a été exporté tooAzure AD, puis Azure AD Connect synchronisation génère une erreur et n’autorise pas plus de modifications sur cet objet avant de hello problème a été résolu et hello sourceAnchor est modifié en hello répertoire source.

## <a name="using-msds-consistencyguid-as-sourceanchor"></a>Utilisation de msDS-ConsistencyGuid en tant que sourceAnchor
Par défaut, Azure AD Connect (version 1.1.486.0 et antérieures) utilise objectGUID comme attribut de sourceAnchor hello. ObjectGUID est généré par le système. Vous ne pouvez pas spécifier sa valeur lors de la création d’objets Active Directory locaux. Comme expliqué dans la section [sourceAnchor](#sourceanchor), il existe des scénarios où vous avez besoin de la valeur sourceAnchor toospecify hello. Si les scénarios de hello sont tooyou applicable, vous devez utiliser un attribut AD configurable (par exemple, msDS-ConsistencyGuid) en tant qu’attribut de sourceAnchor hello.

Azure AD Connect (version 1.1.524.0 et après) autorise l’utiliser hello msDS-ConsistencyGuid comme attribut sourceAnchor. Lorsque vous utilisez cette fonctionnalité, Azure AD Connect configure automatiquement les règles de synchronisation hello pour :

1. Utilisez msDS-ConsistencyGuid en tant qu’attribut de sourceAnchor hello pour les objets utilisateur. ObjectGUID est utilisé pour d’autres types d’objets.

2. Pour toute donnée local utilisateur AD objet dont l’attribut msDS-ConsistencyGuid n’est pas rempli, Azure AD Connect écrit son attribut msDS-ConsistencyGuid d’objectGUID valeur toohello différé dans Active Directory local. Une fois que l’attribut msDS-ConsistencyGuid de hello est rempli, Azure AD Connect exporte ensuite hello objet tooAzure AD.

>[!NOTE]
> Une fois un local objet Active Directory est importé dans Azure AD Connect (c'est-à-dire, importé dans hello espace de connecteur Active Directory et projeté dans hello métaverse), vous ne pouvez pas modifier sa valeur sourceAnchor plus. la valeur sourceAnchor toospecify hello pour une fonction local AD d’objet, de configurer son attribut msDS-ConsistencyGuid avant leur importation dans Azure AD Connect.

### <a name="permission-required"></a>Autorisation requise
Pour cette fonctionnalité toowork, hello AD DS compte utilisé toosynchronize avec Active Directory local doit être accordé écriture autorisation toohello msDS-ConsistencyGuid attribut dans Active Directory local.

### <a name="how-tooenable-hello-consistencyguid-feature---new-installation"></a>Comment tooenable hello ConsistencyGuid fonctionnalité - nouvelle installation
Vous pouvez activer utiliser hello ConsistencyGuid comme sourceAnchor lors de l’installation de nouveau. Cette section décrit en détail l’installation rapide et l’installation personnalisée.

  >[!NOTE]
  > Seules les versions plus récentes d’Azure AD Connect (1.1.524.0 et après) prend en charge hello utiliser ConsistencyGuid comme sourceAnchor lors de l’installation de nouveau.

### <a name="how-tooenable-hello-consistencyguid-feature"></a>Comment tooenable hello ConsistencyGuid fonctionnalité
Actuellement, hello fonctionnalité peut uniquement être activée au cours de la nouvelle installation de Azure AD Connect.

#### <a name="express-installation"></a>Installation rapide
Lorsque vous installez Azure AD Connect avec le mode Express, Assistant d’Azure AD Connect hello détermine automatiquement toouse d’attribut hello publicité la plus appropriée en tant qu’attribut de sourceAnchor hello hello suivant logique à l’aide de :

* Tout d’abord, hello Azure AD Connect Assistant requêtes que votre attribut de hello AD Azure AD client tooretrieve utilisé comme hello attribut sourceAnchor dans l’installation de se connecter hello précédente Azure AD (le cas échéant). Si ces informations sont disponibles, Azure AD Connect utilise un attribut hello même AD.

  >[!NOTE]
  > Seules les versions plus récentes d’Azure AD Connect (1.1.524.0 et après) stocke des informations dans votre locataire Azure AD sur l’attribut sourceAnchor de hello utilisé durant l’installation. Les versions antérieures d’Azure AD Connect ne le font pas.

* Si plus d’informations sur l’attribut sourceAnchor de hello utilisé n’est pas disponibles, Assistant de hello vérifie état hello de l’attribut msDS-ConsistencyGuid de hello dans votre annuaire Active Directory local. Si l’attribut de hello n’est pas configurée sur n’importe quel objet dans le répertoire de hello, Assistant de hello utilise hello msDS-ConsistencyGuid en tant qu’attribut de sourceAnchor hello. Si l’attribut de hello est configuré sur un ou plusieurs objets dans le répertoire de hello, hello fermeture de l’Assistant attribut de hello est utilisé par d’autres applications et n’est pas approprié en tant qu’attribut sourceAnchor...

* Dans ce cas, Assistant de hello revient toousing objectGUID comme attribut de sourceAnchor hello.

* Une fois que l’attribut sourceAnchor de hello est décidé, Assistant de hello stocke les informations de hello dans votre locataire Azure AD. informations de Hello seront utilisées par une installation ultérieure d’Azure AD Connect.

Une fois l’installation d’Express terminée, Assistant de hello vous informe de l’attribut a été sélectionnée en tant qu’attribut d’ancre Source hello.

![L’Assistant informe concernant attribut AD choisi pour sourceAnchor](./media/active-directory-aadconnect-design-concepts/consistencyGuid-01.png)

#### <a name="custom-installation"></a>Installation personnalisée
Lorsque vous installez Azure AD Connect avec le mode personnalisé, Assistant d’Azure AD Connect hello fournit deux options lors de la configuration d’attribut sourceAnchor :

![Installation personnalisée - Configuration de sourceAnchor](./media/active-directory-aadconnect-design-concepts/consistencyGuid-02.png)

| Paramètre | Description |
| --- | --- |
| Laisser Azure gérer ancre source de hello pour moi | Sélectionnez cette option si vous souhaitez que les attributs de hello toopick Azure AD pour vous. Si vous sélectionnez cette option, Azure AD Connect, l’Assistant applique hello même [logique de sélection d’attribut sourceAnchor utilisée lors de l’installation d’Express](#express-installation). Installation de tooExpress similaire, hello Assistant vous informe l’attribut a été sélectionnée comme hello attribut d’ancre Source après la fin de l’installation personnalisée. |
| Un attribut spécifique | Sélectionnez cette option si vous le souhaitez toospecify un attribut Active Directory existant en tant qu’attribut de sourceAnchor hello. |

### <a name="how-tooenable-hello-consistencyguid-feature---existing-deployment"></a>Comment tooenable hello ConsistencyGuid - fonctionnalité de déploiement existant
Si vous avez un déploiement d’Azure AD Connect existant qui utilise en tant qu’attribut d’ancre Source hello objectGUID, vous pouvez activer cette toousing ConsistencyGuid à la place.

>[!NOTE]
> Seules les versions plus récentes d’Azure AD Connect (1.1.552.0 et après) prend en charge le basculement à partir de tooConsistencyGuid ObjectGuid en tant qu’attribut d’ancre Source hello.

tooswitch de tooConsistencyGuid objectGUID en tant qu’attribut d’ancre Source hello :

1. Démarrez l’Assistant de connexion hello Azure AD et cliquez sur **configurer** écran de tâches toogo toohello.

2. Sélectionnez hello **configurer l’ancre Source** option de tâches et cliquez sur **suivant**.

   ![Activer ConsistencyGuid pour un déploiement existant - Étape 2](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment01.png)

3. Entrez vos informations d’identification d’administrateur Azure AD et cliquez sur **Suivant**.

4. Assistant Azure AD Connect analyse état hello de l’attribut msDS-ConsistencyGuid de hello dans votre annuaire Active Directory local. Si l’attribut de hello n’est pas configurée sur n’importe quel objet Bonjour que répertoire, Azure AD Connect conclut qu’aucune autre application utilise actuellement les attributs hello et qu’il est sécurisé toouse elle en tant qu’attribut d’ancre Source hello. Cliquez sur **suivant** toocontinue.

   ![Activer ConsistencyGuid pour un déploiement existant - Étape 4](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment02.png)

5. Bonjour **tooConfigure prêt** , cliquez sur **configurer** modification de la configuration toomake hello.

   ![Activer ConsistencyGuid pour un déploiement existant - Étape 5](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment03.png)

6. Une fois que la fin de la configuration de hello, Assistant de hello indique que msDS-ConsistencyGuid est maintenant utilisé en tant qu’attribut d’ancre Source hello.

   ![Activer ConsistencyGuid pour un déploiement existant - Étape 6](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment04.png)

Lors de l’analyse de hello (étape 4), si l’attribut de hello est configuré sur un ou plusieurs objets dans le répertoire de hello, hello fermeture de l’Assistant attribut de hello est utilisé par une autre application et renvoie une erreur, comme illustré dans le diagramme hello ci-dessous. Si vous êtes certain que cet attribut hello n’est pas utilisé par les applications existantes, vous devez toocontact prise en charge pour plus d’informations sur la façon dont toosuppress hello erreur.

![Activer ConsistencyGuid pour un déploiement existant - Erreur](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeploymenterror.png)

### <a name="impact-on-ad-fs-or-third-party-federation-configuration"></a>Impact sur AD FS d’une configuration de fédération tierce
Si vous utilisez Azure AD Connect toomanage local déploiement AD FS, hello Azure AD Connect met automatiquement à jour l’attribut hello même AD toouse des règles de revendication de hello comme ancre source. Cela garantit que cette revendication d’ImmutableID hello générée par AD FS est cohérente avec hello sourceAnchor valeurs exporté tooAzure AD.

Si vous gérez des services AD FS en dehors d’Azure AD Connect ou si vous utilisez des serveurs de fédération de tiers pour l’authentification, vous devez manuellement mettre à jour les règles de revendication hello pour ImmutableID toobe revendication cohérente avec les valeurs de sourceAnchor hello exportée tooAzure AD en tant que décrit dans la section de l’article [modifier AD FS des règles de revendication](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#modclaims). Assistant de Hello renvoie hello suivant avertissement après l’installation :

![Configuration de fédération tierce](./media/active-directory-aadconnect-design-concepts/consistencyGuid-03.png)

### <a name="adding-new-directories-tooexisting-deployment"></a>Ajouter le nouveau déploiement répertoires tooexisting
Supposons que vous avez déployé Azure AD Connect avec hello ConsistencyGuid fonctionnalité est activée, et à présent vous aimeriez tooadd un autre déploiement de toohello active. Lorsque vous essayez de répertoire de hello tooadd, Assistant Azure AD Connect vérifie état hello de l’attribut mSDS-ConsistencyGuid de hello dans le répertoire de hello. Si l’attribut de hello est configuré sur un ou plusieurs objets dans le répertoire de hello, hello fermeture de l’Assistant attribut de hello est utilisé par d’autres applications et retourne une erreur, comme illustré dans le diagramme hello ci-dessous. Si vous êtes certain que cet attribut hello n’est pas utilisé par les applications existantes, vous devez toocontact prise en charge pour plus d’informations sur la façon dont toosuppress hello erreur.

![Ajouter le nouveau déploiement répertoires tooexisting](./media/active-directory-aadconnect-design-concepts/consistencyGuid-04.png)

## <a name="azure-ad-sign-in"></a>Authentification dans Azure AD
Lors de l’intégration de votre annuaire local avec Azure AD, il est important toounderstand comment les paramètres de synchronisation hello peuvent affecter la manière dont les utilisateurs hello s’authentifie. Azure AD utilise l’utilisateur de hello tooauthenticate userPrincipalName (UPN). Toutefois, lorsque vous synchronisez vos utilisateurs, vous devez choisir hello attribut toobe est utilisée pour la valeur userPrincipalName avec précaution.

### <a name="choosing-hello-attribute-for-userprincipalname"></a>Choix d’attribut hello pour userPrincipalName
Lorsque vous sélectionnez l’attribut hello pour fournir la valeur hello toobe UPN utilisé dans un Azure doit assurer.

* valeurs d’attribut Hello conformes toohello UPN syntaxe (RFC 822), qu'il doit être au format de hellousername@domain
* suffixe Hello dans tooone de correspondances de valeurs hello Hello vérifiées des domaines personnalisés dans Azure AD

Dans les paramètres express, hello supposé être un choix pour l’attribut de hello userPrincipalName. Si l’attribut userPrincipalName de hello ne contient pas de valeur de hello vous souhaitez que votre toosign utilisateurs dans tooAzure, puis vous devez choisir **Installation personnalisée**.

### <a name="custom-domain-state-and-upn"></a>État du domaine personnalisé et UPN
Il est important tooensure qu’il existe un domaine vérifié pour le suffixe UPN de hello.

John est un utilisateur de contoso.com. Vous souhaitez que John toouse hello local UPN john@contoso.com toosign dans tooAzure après avoir ont été synchronisées utilisateurs tooyour Azure AD directory contoso.onmicrosoft.com. toodo par conséquent, vous devez tooadd et vérifiez contoso.com en tant qu’un domaine personnalisé dans Azure AD avant de commencer la synchronisation des utilisateurs de hello. Si le suffixe UPN hello John, par exemple contoso.com, ne correspond pas à un domaine vérifié dans Azure AD, Azure AD remplace suffixe hello avec contoso.onmicrosoft.com.

### <a name="non-routable-on-premises-domains-and-upn-for-azure-ad"></a>Domaines locaux non routables et UPN pour Azure AD
Certaines organisations ont des domaines non routables, comme contoso.local, ou de simples domaines à étiquette unique, comme contoso. Vous n’êtes pas en mesure de tooverify un domaine non routable dans Azure AD. Azure AD Connect peut synchroniser tooonly un domaine vérifié dans Azure AD. Lorsque vous créez un répertoire Azure AD, il crée un domaine routable qui devient le domaine par défaut de votre Azure AD, par exemple contoso.onmicrosoft.com. Par conséquent, il devient nécessaire tooverify n’importe quel autre domaine routable dans un tel scénario au cas où vous ne souhaitez pas que le domaine toosync toohello par défaut onmicrosoft.com.

Lecture [ajouter votre tooAzure de nom de domaine personnalisé Active Directory](../active-directory-add-domain.md) pour plus d’informations sur l’ajout et la vérification de domaines.

Azure AD Connect détecte si vous exécutez un environnement de domaine non routable et vous avertit en temps utile si vous tentez de poursuivre la configuration rapide. Si vous opérez dans un domaine non routable, il est probable que l’UPN des utilisateurs de hello hello offrent de suffixes non routable. Par exemple, si vous exécutez sous contoso.local, Azure AD Connect suggère vous toouse des paramètres personnalisés au lieu d’utiliser les paramètres express. À l’aide de paramètres personnalisés, vous êtes attribut hello en mesure de toospecify qui doit être utilisé comme toosign UPN dans tooAzure une fois que les utilisateurs de hello sont synchronisé tooAzure AD.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
