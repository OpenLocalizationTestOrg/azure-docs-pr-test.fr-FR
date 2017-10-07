---
title: "Azure AD Connect : Expressions d’approvisionnement déclaratif | Microsoft Docs"
description: "Explique les expressions d’approvisionnement déclaratif hello."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: e3ea53c8-3801-4acf-a297-0fb9bb1bf11d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 516bcf1991c608d33aefc19551254d8b2bfc024f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning-expressions"></a>Azure AD Connect Sync : présentation des expressions d’approvisionnement déclaratif
Azure AD Connect sync s’appuie sur l’approvisionnement déclaratif introduit pour la première fois dans Forefront Identity Manager 2010. Il vous permet de tooimplement votre logique métier d’intégration complète d’identité sans hello besoin toowrite le code compilé.

Une partie essentielle de l’approvisionnement déclaratif est un langage d’expression hello utilisée dans le flux d’attributs. langage Hello utilisé est un sous-ensemble de Microsoft® Visual Basic pour Applications (VBA). Ce langage est utilisé dans Microsoft Office et les utilisateurs qui ont une certaine expérience de VBScript le reconnaîtront également. Hello langage d’Expression approvisionnement déclaratif utilise uniquement des fonctions et n’est pas un langage structuré. Il ne contient ni méthodes ni instructions. Les fonctions sont imbriquées à la place tooexpress du flux de programme.

Pour plus d’informations, consultez [toohello Visual Basic pour la référence du langage Applications pour Office 2013 d’accueil](https://msdn.microsoft.com/library/gg264383.aspx).

attributs de Hello sont fortement typées. Une fonction accepte uniquement les attributs du type correct de hello. Elle respecte également la casse. Les noms des fonctions et les noms des attributs doivent avoir une casse appropriée, sinon une erreur est levée.

## <a name="language-definitions-and-identifiers"></a>Définitions linguistiques et identificateurs
* Les fonctions ont un nom suivi d’arguments entre parenthèses : NomFonction (argument 1, argument N).
* Les attributs sont identifiés par des crochets : [NomAttribut]
* Les paramètres sont identifiés par des signes de pourcentage : %NomParamètre%
* Les constantes de chaîne sont placées entre guillemets : par exemple, "Contoso" (Remarque : vous devez utiliser des guillemets droits "" et non pas des guillemets courbes “”)
* Les valeurs numériques sont exprimées sans guillemets et attendu toobe décimal. Les valeurs hexadécimales sont précédées de &H. Par exemple, 98052, &HFF
* Les valeurs booléennes sont exprimées avec des constantes : True, False.
* Les constantes intégrées et les littéraux sont exprimés uniquement par leur nom : NULL, CRLF, IgnoreThisFlow

### <a name="functions"></a>Fonctions
Approvisionnement déclaratif utilise les valeurs d’attribut fonctions tooenable hello possibilité tootransform nombreux. Ces fonctions peuvent être imbriquées résultat hello à partir d’une fonction est passé dans la fonction de tooanother.

`Function1(Function2(Function3()))`

Vous trouverez la liste complète des fonctions Hello Bonjour [référence de fonction](active-directory-aadconnectsync-functions-reference.md).

### <a name="parameters"></a>Paramètres
Un paramètre est défini par un connecteur ou par un administrateur à l’aide de PowerShell. Les paramètres contiennent généralement des valeurs différentes de toosystem du système, par exemple le nom hello d’utilisateur de hello hello domaine se trouve dans. Vous pouvez les utiliser dans des flux d’attributs.

Hello connecteur Active Directory fourni hello paramètres suivants pour les règles de synchronisation entrantes :

| Nom du paramètre | Commentaire |
| --- | --- |
| Domain.Netbios |Le format du domaine de hello actuellement en cours d’importation, par exemple FABRIKAMSALES |
| Domain.FQDN |Format de nom de domaine complet du domaine de hello actuellement en cours d’importation, par exemple ventes.fabrikam.com |
| Domain.LDAP |Format LDAP du domaine de hello actuellement en cours d’importation, par exemple DC = sales, DC = fabrikam, DC = com |
| Forest.Netbios |Le format du nom forêt hello actuellement en cours d’importation, par exemple FABRIKAMCORP |
| Forest.FQDN |Format de nom de domaine complet du nom forêt hello actuellement en cours d’importation, par exemple fabrikam.com |
| Forest.LDAP |Format LDAP de hello nom de la forêt en cours d’importation, par exemple DC = fabrikam, DC = com |

système de Hello fournit hello après le paramètre, qui est identificateur hello de tooget utilisé Hello connecteur en cours d’exécution :  
`Connector.ID`

Voici un exemple qui remplit le domaine de l’attribut du métaverse hello avec le nom de netbios hello du domaine hello où se trouve hello utilisateur :  
`domain` <- `%Domain.Netbios%`

### <a name="operators"></a>Operators
Hello après les opérateurs peut être utilisé :

* **Opérateurs de comparaison** : &lt;, &lt;=, &lt;&gt;, =, &gt;, &gt;=
* **Mathématiques** : +, -, \*, -
* **Chaîne** : &amp; (concaténation)
* **Logiques** : &amp;&amp; (et), || (ou)
* **Ordre d’évaluation**: ( )

Les opérateurs sont évalué tooright gauche et ont des hello même priorité d’évaluation. Autrement dit, hello \* (multiplicateur) n’est pas évalué avant - (soustraction). 2\*(5 + 3) est identique à hello pas 2\*5 + 3. Hello crochets () sont utilisées l’évaluation hello toochange une commande gauche tooright l’ordre d’évaluation n’est pas appropriée.

## <a name="multi-valued-attributes"></a>Attributs à valeurs multiples
les fonctions Hello peuvent fonctionner sur les attributs à valeur unique et à valeurs multiples. Pour les attributs à valeurs multiples, fonction hello fonctionne sur toutes les valeurs et s’applique hello même fonction tooevery valeur.

Par exemple :  
`Trim([proxyAddresses])`Effectuer un ajustement de chaque valeur dans l’attribut proxyAddress de hello.  
`Word([proxyAddresses],1,"@") & "@contoso.com"`Pour chaque valeur avec une @-sign, remplacez le domaine hello avec @contoso.com.  
`IIF(InStr([proxyAddresses],"SIP:")=1,NULL,[proxyAddresses])`Recherchez hello adresse SIP et le supprimer à partir des valeurs de hello.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur le modèle de configuration hello dans [approvisionnement déclaratif compréhension](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Voir comment déclarative utilisé out-of-box dans la configuration se [présentation de la configuration par défaut hello](active-directory-aadconnectsync-understanding-default-configuration.md).
* Consultez la section Comment toomake une pratique modifier à l’aide de l’approvisionnement déclaratif dans [comment toomake un toohello de modification de configuration par défaut](active-directory-aadconnectsync-change-the-configuration.md).

**Rubriques de présentation**

* [Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)

**Rubriques de référence**

* [Azure AD Connect Sync : Référence aux fonctions](active-directory-aadconnectsync-functions-reference.md)

