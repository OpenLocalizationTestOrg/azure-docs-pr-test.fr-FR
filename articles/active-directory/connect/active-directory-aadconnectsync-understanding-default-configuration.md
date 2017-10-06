---
title: "Synchronisation Azure AD Connect : présentation de la configuration par défaut hello | Documents Microsoft"
description: "Cet article décrit la configuration par défaut de hello dans la synchronisation Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ed876f22-6892-4b9d-acbe-6a2d112f1cd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1cf95759af913cad8a1393839d3a836434e7c9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-default-configuration"></a>Synchronisation Azure AD Connect : présentation de la configuration par défaut hello
Cet article explique les règles de configuration d’out-of-box hello. Elle traite les règles hello et l’impact de ces règles de configuration de hello. Il vous guide également dans la configuration par défaut de hello de synchronisation Azure AD Connect. Hello vise que lecteur de hello comprenne le fonctionne du modèle de configuration hello, nommé approvisionnement déclaratif, dans un exemple réel. Cet article suppose que vous avez déjà installé et que vous configurez la synchronisation d’Azure AD Connect à l’aide de l’Assistant installation hello.

Détails de hello toounderstand du modèle de configuration hello, lire [approvisionnement déclaratif compréhension](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

## <a name="out-of-box-rules-from-on-premises-tooazure-ad"></a>Règles out-of-box local tooAzure AD
Hello expressions suivantes peuvent être trouvées dans la configuration d’out-of-box hello.

### <a name="user-out-of-box-rules"></a>Règles out-of-box d’utilisateur
Ces règles s’appliquent également de type d’objet iNetOrgPerson toohello.

Un objet utilisateur doit satisfaire hello suivant toobe synchronisé :

* Il doit disposer d’un sourceAnchor.
* Après avoir hello objet a été créé dans Azure AD, puis ancre source ne peut pas modifier. Si la valeur de hello est modifié localement, hello objet cesse synchronisation jusqu'à ce que hello sourceAnchor est modifié la valeur précédente de tooits précédent.
* Doit avoir hello accountEnabled (userAccountControl) attribut rempli. Avec un Active Directory local, cet attribut est toujours présent et renseigné.

Hello les objets utilisateur suivants est **pas** synchronisé tooAzure AD :

* `IsPresent([isCriticalSystemObject])`. Assurez-vous de nombreux objets d’out-of-box dans Active Directory, telles que compte d’administrateur intégré hello, ne sont pas synchronisées.
* `IsPresent([sAMAccountName]) = False`. Assurez-vous que les objets utilisateur sans l'attribut sAMAccountName ne sont pas synchronisés. Ce cas se produit pratiquement uniquement dans un domaine mis à niveau à partir d’un système NT4.
* `Left([sAMAccountName], 4) = "AAD_"`, `Left([sAMAccountName], 5) = "MSOL_"`. Ne pas synchroniser le compte de service hello utilisé par la synchronisation Azure AD Connect et ses versions antérieures.
* Ne synchronisez pas les comptes Exchange qui pourraient ne pas fonctionner dans Exchange Online.
  * `[sAMAccountName] = "SUPPORT_388945a0"`
  * `Left([mailNickname], 14) = "SystemMailbox{"`
  * `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`
  * `(Left([sAMAccountName], 4) = "CAS_" && (InStr([sAMAccountName], "}")> 0))`
* Ne synchronisez pas les objets qui pourraient ne pas fonctionner dans Exchange Online.
  `CBool(IIF(IsPresent([msExchRecipientTypeDetails]),BitAnd([msExchRecipientTypeDetails],&H21C07000) > 0,NULL))`  
  Ce masque de bits (& H21C07000) permet de filtrer les hello objets suivants :
  * Dossier public à extension messagerie
  * Boîte aux lettres de surveillance du système
  * Boîte aux lettres de base de données de boîtes aux lettres (Boîte aux lettres système)
  * Groupe de sécurité universel (ne s'applique pas à un utilisateur, mais est présent pour des raisons d'héritage)
  * Groupe non universel (ne s'applique pas à un utilisateur, mais est présent pour des raisons d'héritage)
  * Plan de boîte aux lettres
  * Boîte aux lettres de découverte
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Ne synchronisez aucun objet victime de réplication.

Hello, suivant les règles de l’attribut s’appliquent :

* `sourceAnchor <- IIF([msExchRecipientTypeDetails]=2,NULL,..)`. attribut de sourceAnchor Hello n’est pas obtenue à partir d’une boîte aux lettres liée. Il est supposé que si une boîte aux lettres liée a été trouvé, compte hello est joint plus tard.
* Lié à Exchange avec les attributs sont synchronisés uniquement si hello attribut **mailNickName** a une valeur.
* Lorsqu’il existe plusieurs forêts, les attributs sont consommés Bonjour suivant l’ordre :
  1. Attributs liés dans toosign (par exemple userPrincipalName) sont fournis à partir de la forêt hello avec un compte activé.
  2. Les attributs qui se trouvent dans une liste d’adresses globale Exchange (liste d’adresses globale) sont fournis à partir de la forêt hello avec une boîte aux lettres Exchange.
  3. Si aucune boîte aux lettres ne peut être trouvée, ces attributs peuvent provenir de n'importe quelle forêt.
  4. Échange connexes attributs (attributs techniques non visibles dans la liste d’adresses globale de hello) sont fournis à partir de la forêt de hello où `mailNickname ISNOTNULL`.
  5. S’il existe plusieurs forêts qui seraient répondent à une de ces règles, puis hello ordre de création (date/heure) de hello connecteurs (forêts) est utilisé toodetermine forêt qui fournit les attributs hello.

### <a name="contact-out-of-box-rules"></a>Règles out-of-box de contact
Un objet de contact doit satisfaire hello suivant toobe synchronisé :

* contact de Hello doit être à extension messagerie. Il est vérifié par hello suivant les règles :
  * `IsPresent([proxyAddresses]) = True)`. attribut proxyAddresses de Hello doit être rempli.
  * Vous trouverez une adresse de messagerie principale dans l’attribut proxyAddresses de hello ou hello mail. Hello la présence d’un @ est utilisé tooverify que le contenu de hello est une adresse de messagerie. Une de ces deux règles doit être évaluée tooTrue.
    * `(Contains([proxyAddresses], "SMTP:") > 0) && (InStr(Item([proxyAddresses], Contains([proxyAddresses], "SMTP:")), "@") > 0))`. Une entrée avec « SMTP : » et si elle existe, un @ est introuvable dans la chaîne de hello ?
    * `(IsPresent([mail]) = True && (InStr([mail], "@") > 0)`. Est hello attribut de messagerie rempli et s’il s’agit, pouvez un @ est introuvable dans la chaîne de hello ?

Hello objets contacts suivants est **pas** synchronisé tooAzure AD :

* `IsPresent([isCriticalSystemObject])`. Vérifiez qu’aucun objet contact marqué comme critique n’est synchronisé. Cet objet ne devrait pas avoir de configuration par défaut.
* `((InStr([displayName], "(MSOL)") > 0) && (CBool([msExchHideFromAddressLists])))`.
* `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`. Ces objets ne fonctionneraient pas avec Exchange Online.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Ne synchronisez aucun objet victime de réplication.

### <a name="group-out-of-box-rules"></a>Règles out-of-box de groupe
Un objet de groupe doit satisfaire hello suivant toobe synchronisé :

* Il doit compter moins de 50 000 membres. Ce nombre est le nombre de hello de membres de groupe de local hello.
  * S’il possède plus de membres avant la synchronisation démarre hello première fois, le groupe de hello n’est pas synchronisé.
  * Si la croissance nombre hello de membres à partir de lorsqu’il a été initialement créé, puis lorsqu’il atteint 50 000 membres que cesse de synchronisation jusqu'à ce que le nombre d’appartenance hello est inférieure à 50 000 à nouveau.
  * Remarque : nombre de 50 000 appartenance hello est également appliquée par Azure AD. Vous n’êtes pas en mesure de toosynchronize des groupes avec plus de membres même si vous modifiez ou supprimez cette règle.
* Si le groupe hello est un **groupe de Distribution**, il doit également être activé pour la messagerie. Consultez la page [Règles out-of-box de contact](#contact-out-of-box-rules) pour l’application de cette règle.

Bonjour, objets de groupe suivants est **pas** synchronisé tooAzure AD :

* `IsPresent([isCriticalSystemObject])`. Assurez-vous de nombreux objets d’out-of-box dans Active Directory, tels que du groupe Administrateurs intégrés de hello, ne sont pas synchronisées.
* `[sAMAccountName] = "MSOL_AD_Sync_RichCoexistence"`. Groupe hérité utilisé par DirSync.
* `BitAnd([msExchRecipientTypeDetails],&amp;H40000000)`. Groupe de rôles.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Ne synchronisez aucun objet victime de réplication.

### <a name="foreignsecurityprincipal-out-of-box-rules"></a>Règles out-of-box ForeignSecurityPrincipal
FSP est jointes trop « tout » (\*) objet hello métaverse. En réalité, cela se produit uniquement pour les utilisateurs et les groupes de sécurité. Cette configuration garantit que les appartenances inter-forêts sont correctement résolues et représentées dans Azure AD.

### <a name="computer-out-of-box-rules"></a>Règles out-of-box d’ordinateur
Un objet ordinateur doit satisfaire hello suivant toobe synchronisé :

* `userCertificate ISNOTNULL`. Seuls les objets ordinateur Windows 10 renseignent cet attribut. Tous les objets ordinateur avec une valeur de cet attribut sont synchronisés.

## <a name="understanding-hello-out-of-box-rules-scenario"></a>Présentation du scénario de règles d’out-of-box hello
Dans cet exemple, nous utilisons un déploiement comportant une forêt de comptes (A), une forêt de ressources (R) et un répertoire Azure AD.

![Vue d’ensemble avec description du scénario](./media/active-directory-aadconnectsync-understanding-default-configuration/scenario.png)

Dans cette configuration, il est supposé qu'est un compte activé dans la forêt de comptes hello et un compte désactivé dans la forêt de ressources hello avec une boîte aux lettres liée.

Notre objectif hello configuration par défaut est :

* Attributs liés dans toosign sont synchronisés à partir de la forêt hello avec compte de hello activée.
* Les attributs qui se trouvent dans hello Lag (liste d’adresses globale) sont synchronisés à partir de la forêt hello avec boîte aux lettres hello. Si aucune boîte aux lettres n’est trouvée, toute autre forêt est utilisée.
* Si une boîte aux lettres liée est trouvée, hello compte activé lié doit être présent pour hello objet toobe exporté tooAzure AD.

### <a name="synchronization-rule-editor"></a>Éditeur de règles de synchronisation
configuration de Hello peut être affichée et modifiée avec l’outil hello éditeur de règles de synchronisation (SRE) et un tooit raccourci se trouve dans le menu Démarrer de hello.

![Icône de l’Éditeur de règles de synchronisation](./media/active-directory-aadconnectsync-understanding-default-configuration/sre.png)

Hello SRE est un outil de kit de ressources, et il est installé avec la synchronisation Azure AD Connect. toostart en mesure de toobe, vous devez être membre du groupe ADSyncAdmins de hello. Lorsqu’il démarre, vous voyez quelque chose comme suit :

![Règles de synchronisation entrante](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

Dans ce volet, vous voyez toutes les règles de synchronisation créées pour votre configuration. Chaque ligne dans la table de hello est une règle de synchronisation. toohello gauche sous Rule Types, hello deux types différents sont répertoriés : entrant et sortant. Trafic entrant et sortant est à partir de la vue hello de hello métaverse. Vous êtes principalement continu toofocus sur hello dans cette vue d’ensemble de règles de trafic entrant. liste réelle à Hello de règles de synchronisation dépend de schéma de hello détecté dans Active Directory. Dans l’image hello ci-dessus, compte hello forêt (fabrikamonline.com) n’a pas de services, tels qu’Exchange et Lync et aucune règle de synchronisation créées pour ces services. Toutefois, dans la forêt de ressources hello (res.fabrikamonline.com) vous recherchez les règles de synchronisation pour ces services. contenu Hello de règles de hello est différent selon la version de hello détectée. Par exemple, dans un déploiement avec Exchange 2013, plus de flux d’attributs sont configurés que dans Exchange 2010/2007.

### <a name="synchronization-rule"></a>Règle de synchronisation
Une règle de synchronisation est un objet de configuration avec un jeu d’attributs qui circule quand une condition est remplie. Il est également utilisé toodescribe comment un objet dans un espace de connecteur est objet tooan connexes dans le métaverse hello, appelé **jointure** ou **correspond à**. les règles de synchronisation Hello ont une valeur de priorité indiquant comment elles rapportent tooeach autres. Une règle de synchronisation avec une valeur numérique inférieure a une priorité plus élevée et de conflit de flux d’attribut, wins de priorité plus élevées hello la résolution des conflits.

Par exemple, examinez hello règle de synchronisation **dans from AD – User AccountEnabled**. Sélectionnez cette ligne Bonjour SRE et **modifier**.

Étant donné que cette règle est une règle d’out-of-box, vous recevez un avertissement lorsque vous ouvrez la règle de hello. Vous ne devez pas apporter les [modifie les règles tooout-of-box](active-directory-aadconnectsync-best-practices-changing-default-configuration.md), de sorte que vous êtes invité à quelles sont vos intentions. Dans ce cas, vous souhaitez uniquement que tooview hello règle. Sélectionnez **Non**.

![Avertissement de règles de synchronisation](./media/active-directory-aadconnectsync-understanding-default-configuration/warningeditrule.png)

Une règle de synchronisation comporte quatre sections de configuration : Description, Filtre d’étendue, Règles de jointure et Transformations.

#### <a name="description"></a>Description
Hello première section fournit des informations de base telles que le nom et la description.

![Onglet Description dans l’Éditeur de règles de synchronisation ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruledescription.png)

Vous recherchez également des informations sur les système connecté, cette règle est liée, ce qui est l’objet de type Bonjour connecté système, à qu'elle s’applique et hello du type d’objet de métaverse. type d’objet de métaverse Hello est toujours indépendamment de la personne lorsque le type d’objet source hello est un utilisateur, iNetOrgPerson ou contact. type d’objet de métaverse Hello ne doit jamais changer, il est créé comme un type générique. Type de lien de Hello peut être définie tooJoin, StickyJoin ou Provision. Ce paramètre fonctionne avec la section Join Rules de hello et est traitée ultérieurement.

Vous pouvez également voir que cette règle de synchronisation est utilisée pour la synchronisation de mot de passe. Si un utilisateur est dans l’étendue de cette règle de synchronisation, un mot de passe hello est synchronisée à partir de toocloud local (en supposant que vous avez activé la fonctionnalité de synchronisation de mot de passe hello).

#### <a name="scoping-filter"></a>Filtre d’étendue
Hello section Scoping Filter est tooconfigure utilisé lorsqu’une règle de synchronisation doit s’appliquer. Étant donné que le nom hello Hello règle de synchronisation que vous examinez indique qu’il ne doit être appliquée pour les utilisateurs activés, l’étendue de hello est configuré dans ce attribut de hello AD **userAccountControl** doit avoir pas hello bit 2 défini. Lorsque le moteur de synchronisation hello recherche un utilisateur dans Active Directory, il s’applique cette synchronisation règle quand **userAccountControl** a la valeur toohello de valeur décimale 512 (utilisateur normal activé). Il ne s’applique pas les règles hello hello utilisateur a **userAccountControl** définir too514 (utilisateur normal désactivé).

![Onglet Étendue dans l’Éditeur de règles de synchronisation ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilter.png)

filtre d’étendue Hello possède des groupes et les Clauses qui peuvent être imbriqués. Toutes les clauses à l’intérieur d’un groupe doivent être satisfaites pour un tooapply de règle de synchronisation. Lorsque plusieurs groupes sont définis, au moins un groupe doit être satisfait pour hello règle tooapply. C’est-à-dire qu’une opération OR logique est évaluée entre les groupes et qu’une opération AND logique est évaluée à l’intérieur d’un groupe. Vous trouverez un exemple de cette configuration Bonjour règle de synchronisation sortants **hors tooAAD – Group Join**. Il existe plusieurs groupes de filtres de synchronisation, par exemple, un pour les groupes de sécurité (`securityEnabled EQUAL True`) et un autre pour les groupes de distribution (`securityEnabled EQUAL False`).

![Onglet Étendue dans l’Éditeur de règles de synchronisation ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilterout.png)

Cette règle est utilisée toodefine qui groupes doivent être approvisionné tooAzure AD. Groupes de distribution doivent être toobe extension messagerie synchronisé avec Azure AD, mais pour les groupes de sécurité, un message électronique n’est pas requis.

#### <a name="join-rules"></a>Règles de jointure
section de tiers Hello est tooconfigure utilisé interaction avec les objets dans l’espace de connecteur hello tooobjects hello métaverse. Hello règle que vous avez étudié précédemment n’a pas de configuration pour Join Rules, au lieu de cela vous sont toolook continue à **dans from AD – User Join**.

![Onglet Règles de jointure dans l’Éditeur de règles de synchronisation ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulejoinrules.png)

le contenu de la règle de jointure hello Hello dépend hello option sélectionnée dans l’Assistant installation Bonjour de correspondance. Pour une règle de trafic entrant, l’évaluation hello commence par un objet dans l’espace de connecteur source hello et chaque groupe de règles de jointure hello est évaluée dans la séquence. Si un objet source est évalué toomatch exactement un objet dans hello métaverse à l’aide d’une des règles de jointure hello, hello objets sont joints. Si toutes les règles ont été évaluées, et il n’existe aucune correspondance, hello Type de lien sur la page de description hello est utilisé. Si cette configuration est définie trop**configurer**, un nouvel objet est créé dans la cible de hello, hello métaverse. tooprovision un nouveau métaverse de toohello objet est également appelé trop**projet** un métaverse de toohello d’objet.

les règles de jointure Hello sont évaluées uniquement une fois. Lorsqu’un objet d’espace de connecteur et un objet de métaverse sont joints, ils restent tant que portée hello Hello règle de synchronisation est toujours satisfaite.

Lors de l’évaluation de plusieurs règles de synchronisation, une seule d’entre elles avec des règles de jointure définies doit être dans l’étendue. Si plusieurs règles de synchronisation avec des règles de jointure sont détectées pour un objet, une erreur est levée. Pour cette raison, il est recommandé de hello est toohave qu’une seule règle de synchronisation avec jointure définie quand plusieurs règles de synchronisation sont dans la portée d’un objet. Dans la configuration d’out-of-box hello pour la synchronisation Azure AD Connect, ces règles peuvent se trouve en regardant hello nom et recherchez ceux dont le mot de hello **joindre** à fin hello du nom de hello. Une règle de synchronisation sans aucune règle de jointure défini s’applique hello flux d’attributs à une autre règle de synchronisation de joindre les objets hello approvisionné un nouvel objet dans la cible de hello.

Si vous examinez l’image hello ci-dessus, vous pouvez voir cette règle hello tente toojoin **objectSID** avec **msExchMasterAccountSid** (Exchange) et **msRTCSIP-OriginatorSid** () Lync), qui est ce que nous attendions dans une topologie de forêt compte-ressource. Recherche de hello même règle sur toutes les forêts. hypothèse de Hello est que chaque forêt peut être un compte ou une ressource de forêt. Cette configuration fonctionne également si vous disposez de comptes qui se trouvent dans une forêt unique et n’ont pas de toobe joint.

#### <a name="transformations"></a>Transformations
section de transformation Hello définit tous les flux d’attributs applicables à objet cible de toohello hello objets sont joints et filtre d’étendue hello est satisfait. Si vous revenez en toohello **dans from AD – User AccountEnabled** règle de synchronisation, vous trouvez hello suivant transformations :

![Onglet Transformations dans l’Éditeur de règles de synchronisation ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruletransformations.png)

tooput cette configuration dans le contexte, dans un déploiement de forêt compte-ressource, il est attendu toofind un compte activé dans la forêt de comptes hello et un compte désactivé dans la ressource de hello forêt avec les paramètres Exchange et Lync. Hello règle de synchronisation que vous examinez contient les attributs hello requis pour la connexion et de ces attributs doit être le flux à partir de la forêt de hello dans lequel il existe un compte activé. Tous ces flux d’attributs sont regroupés dans une règle de synchronisation.

Une transformation peut avoir différents types : Constant, Direct et Expression.

* Un flux constant transmet toujours une valeur codée en dur. Dans les cas de hello ci-dessus, il définit toujours la valeur de hello **True** dans l’attribut du métaverse hello nommé **accountEnabled**.
* Un flux direct transite toujours attribut hello dans l’attribut de hello source toohello cible en tant que valeur hello-est.
* troisième type de flux Hello est Expression, permet d’effectuer les configurations plus complexes.

langage d’expression Hello est VBA (Visual Basic pour Applications), par conséquent, les personnes ayant une expérience de Microsoft Office ou VBScript reconnaîtra le format de hello. Les attributs sont placés entre crochets : [nom_attribut]. Noms d’attributs et les noms de fonctions respectent la casse, mais évalue les expressions de hello hello Éditeur des règles de synchronisation et génère un avertissement si l’expression de hello n’est pas valide. Toutes les expressions sont placées sur une seule ligne avec les fonctions imbriquées. alimentation de hello tooshow du langage de configuration hello, voici hello flux pour pwdLastSet, mais avec des commentaires supplémentaires insérés :

```
// If-then-else
IIF(
// (hello evaluation for IIF) Is hello attribute pwdLastSet present in AD?
IsPresent([pwdLastSet]),
// (hello True part of IIF) If it is, then from right tooleft, convert hello AD time format tooa .Net datetime, change it toohello time format used by Azure AD, and finally convert it tooa string.
CStr(FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")),
// (hello False part of IIF) Nothing toocontribute
NULL
)
```

Consultez [compréhension des Expressions de l’approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) pour plus d’informations sur le langage d’expression hello pour les flux d’attributs.

### <a name="precedence"></a>Precedence
Vous avez examiné certaines règles de synchronisation individuelles, mais hello règles fonctionnent ensemble dans la configuration de hello. Dans certains cas, une valeur d’attribut est obtenue à partir de plusieurs toohello de règles de synchronisation même attribut cible. Dans ce cas, la précédence d’attribut est toodetermine utilisé quel attribut wins. Par exemple, observez hello attribut sourceAnchor. Cet attribut est un toosign en mesure de toobe attribut important dans tooAzure AD. Vous pouvez trouver un flux d’attributs pour cet attribut dans deux règles de synchronisation différentes : **Entrant depuis AD – Utilisateur AccountEnabled** et **Entrant depuis AD – Utilisateur Common**. En raison de la priorité des règles tooSynchronization, attribut de sourceAnchor hello est obtenue à partir de forêt hello avec un compte activé tout d’abord lorsqu’il y a plusieurs objets joints toohello métaverse object. Si aucun compte activé, puis utilise de moteur de synchronisation hello hello règle de synchronisation fourre-tout **dans depuis AD-utilisateur courant**. Cette configuration garantit que même pour les comptes qui sont désactivés, il existe toujours un sourceAnchor.

![Règles de synchronisation entrante](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

priorité Hello pour les règles de synchronisation est définie dans les groupes par l’Assistant installation hello. Toutes les règles dans un groupe ont hello même nom, mais ils sont connectés toodifferent connecté répertoires. l’Assistant installation Hello donne la règle de hello **dans from AD – User Join** priorité la plus élevée et il effectue une itération sur tous les annuaires AD connectés. Ensuite, il continue avec hello autres groupes de règles dans un ordre prédéfini. À l’intérieur d’un groupe, les règles de hello sont ajoutées dans hello de commande hello que connecteurs ont été ajoutées dans l’Assistant de hello. Si un autre connecteur est ajouté via l’Assistant de hello, règles de synchronisation hello sont réorganisés et hello règles du nouveau connecteur sont insérées à la fin de chaque groupe.

### <a name="putting-it-all-together"></a>Exemple complet
Nous savons maintenant suffisamment sur les règles de synchronisation toobe toounderstand d’en mesure de fonctionne de la configuration de hello avec hello différentes règles de synchronisation. Si vous cherchez à un utilisateur et un hello attributs qui sont contribué toohello métaverse, les règles de hello sont appliquées dans hello suivant l’ordre :

| Nom | Commentaire |
|:--- |:--- |
| Entrant depuis AD – User Join |Règle pour joindre les objets de l’espace de connecteur avec métaverse. |
| Entrant depuis AD – Utilisateur AccountEnabled |Attributs requis pour la connexion tooAzure AD et Office 365. Nous voulons ces attributs à partir du compte de hello activée. |
| Entrant depuis AD – Utilisateur Common à partir d’Exchange |Attributs trouvés dans la liste d’adresses globale de hello. Nous supposons que la qualité des données hello est préférable de forêt hello où nous avons trouvé des boîtes aux lettres de l’utilisateur hello. |
| Entrant depuis AD – Utilisateur Common |Attributs trouvés dans la liste d’adresses globale de hello. Dans le cas où nous n’avons pas trouvé une boîte aux lettres, tout autre objet joint peut contribuer à valeur d’attribut hello. |
| Entrant depuis AD – Utilisateur Exchange |Existe seulement si Exchange a été détecté. Transfère tous les attributs Exchange d’infrastructure. |
| Entrant depuis AD – Utilisateur Lync |Existe seulement si Lync a été détecté. Transfère tous les attributs Lync d’infrastructure. |

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur le modèle de configuration hello dans [approvisionnement déclaratif compréhension](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* En savoir plus sur le langage d’expression hello [compréhension des Expressions de l’approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Continuer à lire le fonctionne de la configuration d’out-of-box hello dans [présentation des utilisateurs et des Contacts](active-directory-aadconnectsync-understanding-users-and-contacts.md)
* Consultez la section Comment toomake une pratique modifier à l’aide de l’approvisionnement déclaratif dans [comment toomake un toohello de modification de configuration par défaut](active-directory-aadconnectsync-change-the-configuration.md).

**Rubriques de présentation**

* [Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)

