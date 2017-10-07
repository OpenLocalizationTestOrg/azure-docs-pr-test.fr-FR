---
title: "Azure AD Connect : Présentation de l’approvisionnement déclaratif | Microsoft Docs"
description: "Explique hello configuration configuration modèle déclaratif dans Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: cfbb870d-be7d-47b3-ba01-9e78121f0067
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f11e078f0aafacf94d69f0726ae41629a8470336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning"></a>Azure AD Connect Sync : présentation de l’approvisionnement déclaratif
Cette rubrique explique le modèle de configuration hello dans Azure AD Connect. modèle de Hello est appelée approvisionnement déclaratif et il vous permet de toomake une modification de configuration avec la facilité. De nombreux éléments décrits dans cette rubrique sont des éléments avancés, non indispensables pour la plupart des scénarios clients.

## <a name="overview"></a>Vue d'ensemble
Approvisionnement déclaratif est le traitement des objets provenant d’un répertoire source connecté et détermine comment les attributs et les objets hello doivent être transformées à partir d’une source tooa cible. Traitement d’un objet dans un pipeline de synchronisation et le pipeline de hello est hello même pour les règles de trafic entrants et sortants. Règle de trafic entrant à partir un métaverse de toohello d’espace connecteur et règle de trafic sortant à partir de l’espace de connecteur tooa hello métaverse.

![Pipeline de synchronisation](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/sync1.png)  

pipeline de Hello a plusieurs modules. Chacun d’eux est responsable d’un concept de synchronisation des objets.

![Pipeline de synchronisation](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/pipeline.png)  

* Source, l’objet de source de hello
* [Scope](#scope), recherche toutes les règles de synchronisation dans la portée
* [Join](#join), détermine la relation entre l’espace de connecteur et le métaverse
* [Transform](#transform), calcule comment les attributs doivent être transformés et flux
* [Precedence](#precedence), résout les contributions d’attribut conflictuelles
* Cible, l’objet cible de hello

## <a name="scope"></a>Scope
module de portée Hello est l’évaluation d’un objet et détermine les règles hello dans la portée et doivent être inclus dans le traitement de hello. En fonction des valeurs d’attributs hello sur l’objet de hello, règles de synchronisation différents sont toobe évaluée dans l’étendue. Par exemple, un utilisateur désactivé sans boîte aux lettres Exchange possède des règles différentes d’un utilisateur activé avec une boîte aux lettres.  
![Scope](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope1.png)  

étendue de Hello est définie en tant que groupes et des clauses. les clauses Hello sont à l’intérieur d’un groupe. Un opérateur logique AND est utilisé entre toutes les clauses d’un groupe. Par exemple, (department = IT AND country = Denmark). Un opérateur logique OR est utilisé entre les groupes.

![Scope](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope2.png)  
étendue Hello dans cette image doit être lu en tant que (department = IT et pays = Danemark) ou (pays = Suède). Si le groupe 1 ou 2 de groupe est évaluée tootrue, règle de hello est dans la portée.

module de portée Hello prend en charge hello opérations suivantes.

| Opération | Description |
| --- | --- |
| EQUAL, NOTEQUAL |Une comparaison de chaînes qui évalue si la valeur est égale toohello attribut de hello. Pour les attributs à valeurs multiples, consultez ISIN et ISNOTIN. |
| LESSTHAN, LESSTHAN_OR_EQUAL |Une comparaison de chaînes qui évalue si la valeur est par valeur hello dans l’attribut de hello. |
| CONTAINS, NOTCONTAINS |Une comparaison de chaînes qui évalue si la valeur se trouve quelque part dans la valeur dans l’attribut de hello. |
| STARTSWITH, NOTSTARTSWITH |Une comparaison de chaînes qui évalue si la valeur est exprimée en début de hello de valeur hello dans l’attribut de hello. |
| ENDSWITH, NOTENDSWITH |Une comparaison de chaînes qui évalue si la valeur est hello valeur de fin de hello dans l’attribut de hello. |
| GREATERTHAN, GREATERTHAN_OR_EQUAL |Une comparaison de chaînes qui évalue si la valeur est supérieure à la valeur hello dans l’attribut de hello. |
| ISNULL, ISNOTNULL |Évalue si hello attribut est absent de l’objet de hello. Si l’attribut de hello n’est pas présent et par conséquent null, la règle de hello est dans la portée. |
| ISIN, ISNOTIN |Évalue si la valeur de hello est présente dans l’attribut de hello défini. Cette opération est à valeurs multiples modification égal et de NOTEQUAL hello. attribut de Hello est supposée toobe un attribut à valeurs multiples et si la valeur de hello se trouve dans une des valeurs d’attribut hello, puis la règle de hello est dans la portée. |
| ISBITSET, ISNOTBITSET |Évalue si un bit particulier est défini. Par exemple, peut être utilisé tooevaluate bits hello dans userAccountControl toosee si un utilisateur est activé ou désactivé. |
| ISMEMBEROF, ISNOTMEMBEROF |valeur de Hello doit contenir un groupe de tooa nom unique dans l’espace de connecteur hello. Si l’objet de hello est membre du groupe hello spécifié, la règle de hello est dans la portée. |

## <a name="join"></a>Join
module de jointure Hello dans le pipeline de synchronisation hello est responsable de la recherche de relation hello entre hello dans la source de hello et un objet dans la cible de hello. Sur la règle de trafic entrant, cette relation serait un objet dans un espace de connecteur recherche un objet de relation de tooan hello métaverse.  
![Jointure entre cs et mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join1.png)  
Hello vise toosee s’il existe déjà un objet de métaverse hello, créé par un autre connecteur, elle doit être associée. Par exemple, dans une ressource de compte d’utilisateur à partir de la forêt de comptes hello hello doit être joint avec utilisateur hello à partir de la forêt de ressources hello.

Les jointures sont utilisés principalement sur les règles de trafic entrant toojoin connecteur espace objets ensemble toohello même objet de métaverse.

Hello jointures sont définies en tant qu’un ou plusieurs groupes. À l’intérieur d’un groupe, il existe des clauses. Un opérateur logique AND est utilisé entre toutes les clauses d’un groupe. Un opérateur logique OR est utilisé entre les groupes. groupes de Hello sont traités dans l’ordre de toobottom supérieur. Lorsqu’un groupe a trouvé exactement une correspondance avec un objet dans la cible de hello, aucune autre règle de jointure n’est évaluées. Si zéro ou plus d’un objet est trouvé, le traitement continue toohello au prochain groupe de règles. Pour cette raison, les règles de hello doivent être créés dans l’ordre de hello de plus explicite première et la plus probable à fin de hello.  
![Définition de jointure](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join2.png)  
jointures Hello dans cette image sont traités de toobottom supérieur. Pipeline de synchronisation hello première voit s’il existe une correspondance sur employeeID. Si ce n’est pas le cas, seconde hello voit si nom hello du compte peut être utilisé toojoin hello objets ensemble. Si tel n’est pas soit une correspondance, règle de troisième et dernière hello est une correspondance approximative plus à l’aide du nom d’utilisateur de hello.

Si toutes les règles de jointure ont été évaluées, et il n’est pas exactement une correspondance, hello **Type de lien** sur hello **Description** page est utilisée. Si cette option est définie trop**configurer**, un nouvel objet dans la cible de hello est alors créé.  
![Approvisionnement ou jointure](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join3.png)  

Un objet doit avoir une seule règle de synchronisation avec des règles de jointure dans la portée. S’il existe plusieurs règles de synchronisation dans lesquelles la jointure est définie, une erreur se produit. Priorité n’est pas utilisé tooresolve jointure conflits. Un objet doit avoir une règle de jointure dans la portée de tooflow attributs avec hello même sens entrant et sortant. Si vous avez besoin de tooflow toohello entrant et sortant des attributs même objet, vous devez avoir entrante et une règle de synchronisation sortants avec une jointure.

Jointure sortant a un comportement spécial quand il tente de tooprovision un espace de connecteur objet tooa cible. l’attribut Hello DN est toofirst utilisé, essayez une jointure de l’ordre inverse. S’il existe déjà un objet dans l’espace de connecteur hello cible avec hello même DN, hello objets sont joints.

module de jointure Hello est évaluée uniquement une fois que lorsqu’une nouvelle règle de synchronisation est dans l’étendue. Lorsqu’un objet est joint, il n’est pas disjonction même si les critères de jointure hello n’est plus remplie. Si vous voulez toodisjoin un objet, la règle de synchronisation hello qui joint les objets hello doit se trouver hors de portée.

### <a name="metaverse-delete"></a>Suppression du métaverse
Un objet de métaverse reste tant qu’il existe une règle de synchronisation dans la portée avec **Type de lien** défini trop**configurer** ou **StickyJoin**. Un StickyJoin est utilisé lorsqu’un connecteur n’est pas autorisé tooprovision un nouvel objet de métaverse de toohello, mais quand elle a joint, il doit être supprimé dans la source de hello avant la suppression d’objet de métaverse hello.

Lorsqu’un objet de métaverse est supprimé, tous les objets associés à une règle de synchronisation de trafic sortant marquée **Provision** sont marqués pour suppression.

## <a name="transformations"></a>Transformations
les transformations de Hello sont utilisée toodefine comment attributs doit être le flux à partir de hello source toohello cible. Hello flux peuvent avoir l’une des manières suivantes les hello **flux types**: Direct, une constante ou Expression. Un flux direct envoie la valeur de l’attribut telle quelle, sans transformation supplémentaire. Un Bonjour de jeux de valeur de constante de valeur spécifiée. Une expression utilise hello déclarative approvisionnement expression language tooexpress comment la transformation de hello doit être. Hello détails pour le langage d’expression hello se trouvent dans hello [présentation de langage d’expression approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) rubrique.

![Approvisionnement ou jointure](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/transformations1.png)  

Hello **appliquer une seule fois** case à cocher définit ce hello attribut doit être défini uniquement lors de l’objet de hello est initialement créé. Par exemple, cette configuration peut être utilisé tooset un mot de passe initial d’un nouvel objet utilisateur.

### <a name="merging-attribute-values"></a>Fusion de valeurs d’attribut
Flux d’attributs hello est un toodetermine paramètre si des attributs à valeurs multiples doivent être fusionnées à partir de plusieurs liens différents. la valeur par défaut Hello est **mise à jour**, ce qui indique que la règle de synchronisation hello avec la priorité la plus élevée doit win.

![Types de fusion](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/mergetype.png)  

Il existe également une option **Fusionner** et **MergeCaseInsensitive** (Fusion non sensible à la casse). Ces options vous permettent de toomerge des valeurs à partir de sources différentes. Par exemple, il peut être attribut de membre ou proxyAddresses de hello provenant de plusieurs forêts différentes toomerge utilisé. Lorsque vous utilisez cette option, tous les synchroniser les règles dans la portée pour un objet doit utiliser hello même type de fusion. Vous ne pouvez pas définir **Mettre à jour** à partir d’un connecteur et **Fusionner** à partir d’un autre connecteur. Si vous essayez, vous recevrez une erreur.

Hello la différence entre **fusion** et **MergeCaseInsensitive** est comment tooprocess dupliquer les valeurs d’attribut. moteur de synchronisation Hello permet de s’assurer que des valeurs en double ne sont pas insérées dans l’attribut cible de hello. Avec **MergeCaseInsensitive**, doublons au cas où ne vont ne pas toobe présent avec uniquement une différence. Par exemple, vous devez voir pas à la fois «SMTP:bob@contoso.com« et »smtp:bob@contoso.com» dans l’attribut cible de hello. **Fusion** examine uniquement les valeurs exactes de hello et plusieurs valeurs a uniquement une différence dans les cas peuvent être présents.

Hello option **remplacer** est hello identique **mise à jour**, mais il n’est pas utilisé.

### <a name="control-hello-attribute-flow-process"></a>Processus de flux de contrôle hello attribut
Lorsque plusieurs règles de synchronisation entrante sont configurés toocontribute toohello même attribut de métaverse, priorité est le gagnant hello toodetermine utilisé. la règle de synchronisation Hello avec la priorité la plus élevée (valeur numérique la plus basse) va valeur hello de toocontribute. Hello que même se produisent pour les règles de trafic sortant. la règle de synchronisation avec la priorité la plus élevée Hello wins et contribuer hello valeur toohello connectée active.

Dans certains cas, plutôt que contribuer à une valeur, la règle de synchronisation hello doit déterminer comment les autres règles doivent se comporter. Certains littéraux particuliers sont utilisés dans ce cas.

Pour les règles de synchronisation entrantes, hello littéral **NULL** peut être utilisé tooindicate que les flux hello ne dispose d’aucune toocontribute de valeur. Une autre règle avec une priorité inférieure peut transmettre sa valeur. Si aucune règle n’a contribué à une valeur, attribut de métaverse hello est supprimé. Pour une règle sortante, si **NULL** est la valeur finale de hello après le traitement de toutes les règles de synchronisation, puis de la valeur de hello est supprimée dans l’annuaire connecté de hello.

Hello littéral **AuthoritativeNull** ressemble trop**NULL** , mais avec une différence hello qu’aucune règle de priorité inférieur ne peut contribuer à une valeur.

Un flux d’attributs peut également utiliser le littéral **IgnoreThisFlow**. Il s’agit de tooNULL similaires dans les sens hello qu’il indique rien toocontribute. différence de Hello est qu’elle ne supprime pas une valeur déjà existante dans la cible de hello. C’est comme flux d’attribut hello n’a jamais été il.

Voici un exemple :

Dans *hors tooAD - utilisateur Exchange hybride* hello suit flux se trouve :  
`IIF([cloudSOAExchMailbox] = True,[cloudMSExchSafeSendersHash],IgnoreThisFlow)`  
Cette expression doit être lu en tant que : si la boîte aux lettres utilisateur de hello se trouve dans Azure AD, puis flux attribut hello tooAD d’Azure AD. Dans le cas contraire, ne sont pas acheminées tout retour tooActive active. Dans ce cas, il serait conserver la valeur hello dans AD.

### <a name="importedvalue"></a>ImportedValue
fonction de Hello ImportedValue est différente de celle de toutes les autres fonctions, car le nom de l’attribut hello doit être placé entre guillemets, plutôt que des crochets :  
`ImportedValue("proxyAddresses")`.

Généralement pendant la synchronisation un attribut utilise la valeur attendue de hello, même si elle n’a pas encore été exportée ou si une erreur a été reçue lors de l’exportation (« haut de la tour de hello »). Une synchronisation entrante part du principe qu’un attribut qui n’a pas encore atteint un annuaire connecté finira par l’atteindre. Dans certains cas, il est important de tooonly synchroniser une valeur qui a été confirmée par annuaire connecté de hello (« hologramme et tour d’importation de delta »).

Vous trouverez un exemple de cette fonction dans hello out-of-box règle de synchronisation *dans depuis AD-utilisateur courant à partir d’Exchange*. Dans Exchange hybride, valeur hello ajoutée par Exchange online doit uniquement être synchronisée lorsqu’il a été confirmé que la valeur de hello a été exportée correctement :  
`proxyAddresses` <- `RemoveDuplicates(Trim(ImportedValue("proxyAddresses")))`

## <a name="precedence"></a>Precedence
Lorsque vous essayez de plusieurs règles de synchronisation toocontribute hello même cible de toohello de valeur d’attribut, valeur de priorité hello est le gagnant hello toodetermine utilisé. règle Hello avec la priorité la plus élevée, plus petite valeur numérique, attribut de hello toocontribute un conflit est en cours.

![Types de fusion](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/precedence1.png)  

Ce classement peut être utilisé toodefine plus précise des flux pour un petit sous-ensemble des objets d’attribut. Par exemple, hello hors-de--règles prédéfinies vous assurer que des attributs à partir d’un compte activé (**User AccountEnabled**) ont une priorité d’autres comptes.

La précédence peut être définie entre les connecteurs. Qui permet tout d’abord des connecteurs avec meilleures valeurs toocontribute de données.

### <a name="multiple-objects-from-hello-same-connector-space"></a>Plusieurs objets à partir de hello même espace de connecteur
Si vous disposez de plusieurs objets Bonjour même connecteur espace toohello joint à un objet de métaverse même, priorité doit être ajustée. Si plusieurs objets sont dans la portée de hello même règle de synchronisation, puis le moteur de synchronisation hello n’est pas en mesure de toodetermine priorité. Il est ambigu quel objet de source doit contribuer hello valeur toohello métaverse. Cette configuration est signalée comme ambiguë même si les attributs de hello dans la source de hello ont hello même valeur.  
![Plusieurs objets joint toohello même objet mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple1.png)  

Pour ce scénario, vous devez toochange hello champ d’application de règles de synchronisation hello pour que les objets de source de hello aient des règles de synchronisation différent dans la portée. Cela vous permet de toodefine une priorité différente.  
![Plusieurs objets joint toohello même objet mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple2.png)  

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur le langage d’expression hello [compréhension des Expressions de l’approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Voir comment déclarative utilisé out-of-box dans la configuration se [présentation de la configuration par défaut hello](active-directory-aadconnectsync-understanding-default-configuration.md).
* Consultez la section Comment toomake une pratique modifier à l’aide de l’approvisionnement déclaratif dans [comment toomake un toohello de modification de configuration par défaut](active-directory-aadconnectsync-change-the-configuration.md).
* Continuer tooread fonctionnement des utilisateurs et des contacts dans [présentation des utilisateurs et Contacts](active-directory-aadconnectsync-understanding-users-and-contacts.md).

**Rubriques de présentation**

* [Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)

**Rubriques de référence**

* [Azure AD Connect Sync : Référence aux fonctions](active-directory-aadconnectsync-functions-reference.md)
