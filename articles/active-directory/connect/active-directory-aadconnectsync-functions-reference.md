---
title: "Azure AD Connect sync : Référence aux fonctions | Microsoft Docs"
description: "Référence d’expressions d’approvisionnement déclaratif dans Azure AD Connect Sync."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a>Azure AD Connect Sync : Référence aux fonctions
Dans Azure AD Connect, les fonctions sont utilisée toomanipulate une valeur d’attribut lors de la synchronisation.  
Hello syntaxe des fonctions de hello est exprimée à l’aide de hello suivant le format :  
`<output type> FunctionName(<input type> <position name>, ..)`

Si une fonction est surchargée et accepte plusieurs syntaxes, toutes les syntaxes valides sont répertoriées.  
les fonctions Hello sont fortement typées et elles vérifient que le type de hello passé dans le type de hello documentée de correspondances.  
Si le type de hello ne correspond pas, une erreur est générée.

types de Hello sont exprimées par hello selon la syntaxe :

* **bin** : binaire
* **bool** : booléen
* **dt** : date/heure UTC
* **enum** : énumération des constantes connues
* **EXP** – Expression, qui est attendu tooevaluate tooa booléen
* **mvbin** : binaire à valeurs multiples
* **mvstr** : chaîne à valeurs multiples
* **mvref** : référence à valeurs multiples
* **num** : numérique
* **ref** : référence
* **str** : chaîne
* **var** : variante de (quasiment) tout autre type
* **void** : ne retourne aucune valeur

Hello fonctions avec les types hello **mvbin**, **mvstr**, et **mvref** ne fonctionnent sur des attributs à valeurs multiples. Les fonctions avec **bin**, **str** et **ref** fonctionnent sur des attributs à valeur unique et à valeurs multiples.

## <a name="functions-reference"></a>Référence des fonctions
| Liste des fonctions |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| **Certificate** | | | | |
| [CertExtensionOids](#certextensionoids) |[CertFormat](#certformat) |[CertFriendlyName](#certfriendlyname) |[CertHashString](#certhashstring) | |
| [CertIssuer](#certissuer) |[CertIssuerDN](#certissuerdn) |[CertIssuerOid](#certissueroid) |[CertKeyAlgorithm](#certkeyalgorithm) | |
| [CertKeyAlgorithmParams](#certkeyalgorithmparams) |[CertNameInfo](#certnameinfo) |[CertNotAfter](#certnotafter) |[CertNotBefore](#certnotbefore) | |
| [CertPublicKeyOid](#certpublickeyoid) |[CertPublicKeyParametersOid](#certpublickeyparametersoid) |[CertSerialNumber](#certserialnumber) |[CertSignatureAlgorithmOid](#certsignaturealgorithmoid) | |
| [CertSubject](#certsubject) |[CertSubjectNameDN](#certsubjectnamedn) |[CertSubjectNameOid](#certsubjectnameoid) |[CertThumbprint](#certthumbprint) | |
[CertVersion](#certversion) |[IsCert](#iscert) | | | |
| **Conversion** | | | | |
| [CBool](#cbool) |[CDate](#cdate) |[CGuid](#cguid) |[ConvertFromBase64](#convertfrombase64) | |
| [ConvertToBase64](#converttobase64) |[ConvertFromUTF8Hex](#convertfromutf8hex) |[ConvertToUTF8Hex](#converttoutf8hex) |[CNum](#cnum) | |
| [CRef](#cref) |[CStr](#cstr) |[StringFromGuid](#StringFromGuid) |[StringFromSid](#stringfromsid) | |
| **Date / Heure** | | | | |
| [DateAdd](#dateadd) |[DateFromNum](#datefromnum) |[FormatDateTime](#formatdatetime) |[Now](#now) | |
| [NumFromDate](#numfromdate) | | | | |
| **Directory** | | | | |
| [DNComponent](#dncomponent) |[DNComponentRev](#dncomponentrev) |[EscapeDNComponent](#escapedncomponent) | | |
| **Evaluation** | | | | |
| [IsBitSet](#isbitset) |[IsDate](#isdate) |[IsEmpty](#isempty) |[IsGuid](#isguid) | |
| [IsNull](#isnull) |[IsNullOrEmpty](#isnullorempty) |[IsNumeric](#isnumeric) |[IsPresent](#ispresent) | |
| [IsString](#isstring) | | | | |
| **Mathématique** | | | | |
| [BitAnd](#bitand) |[BitOr](#bitor) |[RandomNum](#randomnum) | | |
| **Multi-valued** | | | | |
| [Contains](#contains) |[Count](#count) |[Item](#item) |[ItemOrNull](#itemornull) | |
| [Join](#join) |[RemoveDuplicates](#removeduplicates) |[Split](#split) | | |
| **Flux de programme** | | | | |
| [Error](#error) |[IIF](#iif) |[Sélection](#select) |[Switch](#switch) | |
| [Where](#where) |[With](#with) | | | |
| **Text** | | | | |
| [GUID](#guid) |[InStr](#instr) |[InStrRev](#instrrev) |[LCase](#lcase) | |
| [Left](#left) |[Len](#len) |[LTrim](#ltrim) |[Mid](#mid) | |
| [PadLeft](#padleft) |[PadRight](#padright) |[PCase](#pcase) |[Replace](#replace) | |
| [ReplaceChars](#replacechars) |[Right](#right) |[RTrim](#rtrim) |[Trim](#trim) | |
| [UCase](#ucase) |[Word](#word) | | | |

- - -
### <a name="bitand"></a>BitAnd
**Description :**  
Hello fonction BitAnd définit des bits spécifiés sur une valeur.

**Syntaxe :**  
`num BitAnd(num value1, num value2)`

* value1, value2 : valeurs numériques qui doivent être liées par AND.

**Remarques :**  
Cette fonction convertit les deux paramètres toohello binaire et définit un bit :

* 0 - si une ou les deux bits correspondants dans hello *masque* et *indicateur* sont 0
* 1 - si les deux bits correspondants de hello sont 1.

En d’autres termes, elle retourne 0 dans tous les cas sauf si les bits correspondants de hello des deux paramètres sont 1.

**Exemple :**  
`BitAnd(&HF, &HF7)`  
Retourne 7, car hexadécimale « F » et « F7 » prendre la valeur de toothis.

- - -
### <a name="bitor"></a>BitOr
**Description :**  
Hello fonction BitOr définit des bits spécifiés sur une valeur.

**Syntaxe :**  
`num BitOr(num value1, num value2)`

* value1, value2 : valeurs numériques qui doivent être liées par OR

**Remarques :**  
Cette fonction convertit les deux paramètres toohello binaire et définit un bit de too1 si une ou les deux bits correspondants hello masque et l’indicateur sont 1 et too0 si les deux bits correspondants de hello sont 0. En d’autres termes, elle retourne 1 dans tous les cas sauf si les bits correspondants de hello des deux paramètres égalent 0.

- - -
### <a name="cbool"></a>CBool
**Description :**  
Hello fonction CBool retourne qu'une valeur booléenne en fonction de l’expression de hello évaluée

**Syntaxe :**  
`bool CBool(exp Expression)`

**Remarques :**  
Si l’expression de hello évalue tooa différent de zéro, CBool retourne True, sinon elle retourne False.

**Exemple :**  
`CBool([attrib1] = [attrib2])`  

Retourne True si les deux attributs ont hello la même valeur.

- - -
### <a name="cdate"></a>CDate
**Description :**  
Hello fonction CDate retourne une valeur DateTime UTC à partir d’une chaîne. DateTime n’est pas un type d’attribut natif dans Sync, mais il est utilisé par certaines fonctions.

**Syntaxe :**  
`dt CDate(str value)`

* Valeur : chaîne comportant une date, une heure, et éventuellement, un fuseau horaire

**Remarques :**  
Hello retourné de chaîne est toujours en UTC.

**Exemple :**  
`CDate([employeeStartTime])`  
Retourne une valeur DateTime basée sur l’heure de début de l’employé hello

`CDate("2013-01-10 4:00 PM -8")`  
Renvoie une valeur DateTime représentant « 2013-01-11 12:00 AM ».








- - -
### <a name="certextensionoids"></a>CertExtensionOids
**Description :**  
Retourne hello Oid des valeurs de toutes les extensions critiques hello d’un objet de certificat.

**Syntaxe :**  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certformat"></a>CertFormat
**Description :**  
Retourne hello nom du format de hello de ce certificat X.509v3.

**Syntaxe :**  
`str CertFormat(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certfriendlyname"></a>CertFriendlyName
**Description :**  
Retourne hello associé alias pour un certificat.

**Syntaxe :**  
`str CertFriendlyName(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certhashstring"></a>CertHashString
**Description :**  
Retourne hello la valeur de hachage SHA1 pour le certificat X.509v3 de hello sous forme de chaîne hexadécimale.

**Syntaxe :**  
`str CertHashString(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certissuer"></a>CertIssuer
**Description :**  
Retourne hello nom de l’autorité de certification hello qui a émis le certificat x.509v.3 de hello.

**Syntaxe :**  
`str CertIssuer(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certissuerdn"></a>CertIssuerDN
**Description :**  
Retourne hello nom unique de l’émetteur du certificat hello.

**Syntaxe :**  
`str CertIssuerDN(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certissueroid"></a>CertIssuerOid
**Description :**  
Retourne hello Oid de l’émetteur du certificat hello.

**Syntaxe :**  
`str CertIssuerOid(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certkeyalgorithm"></a>CertKeyAlgorithm
**Description :**  
Retourne des informations d’algorithme de clé hello pour ce certificat x.509v.3 sous forme de chaîne.

**Syntaxe :**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certkeyalgorithmparams"></a>CertKeyAlgorithmParams
**Description :**  
Retourne les paramètres d’algorithme de clé hello du certificat x.509v.3 hello sous forme de chaîne hexadécimale.

**Syntaxe :**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certnameinfo"></a>CertNameInfo
**Description :**  
Retourne l’émetteur et l’objet de hello noms à partir d’un certificat.

**Syntaxe :**  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.
*   X509NameType : hello valeur X509NameType pour l’objet de hello.
*   includesIssuerName : nom de l’émetteur de hello tooinclude true ; Sinon, false.

- - -
### <a name="certnotafter"></a>CertNotAfter
**Description :**  
Retourne la date de hello en heure locale après laquelle un certificat n’est plus valide.

**Syntaxe :**  
`dt CertNotAfter(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certnotbefore"></a>CertNotBefore
**Description :**  
Retourne la date de hello en heure locale à laquelle un certificat devient valide.

**Syntaxe :**  
`dt CertNotBefore(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certpublickeyoid"></a>CertPublicKeyOid
**Description :**  
Retourne hello Oid de la clé publique hello du certificat x.509v.3 hello.

**Syntaxe :**  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certpublickeyparametersoid"></a>CertPublicKeyParametersOid
**Description :**  
Retourne hello Oid hello paramètres de clé publique pour le certificat X.509v3 de hello.

**Syntaxe :**  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certserialnumber"></a>CertSerialNumber
**Description :**  
Retourne le numéro de série hello du certificat X.509v3 de hello.

**Syntaxe :**  
`str CertSerialNumber(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certsignaturealgorithmoid"></a>CertSignatureAlgorithmOid
**Description :**  
Retourne hello Oid de l’algorithme de hello utilisé signature de hello toocreate d’un certificat.

**Syntaxe :**  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certsubject"></a>CertSubject
**Description :**  
Obtient hello nom unique du sujet d’un certificat.

**Syntaxe :**  
`str CertSubject(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certsubjectnamedn"></a>CertSubjectNameDN
**Description :**  
Retourne hello nom unique du sujet d’un certificat.

**Syntaxe :**  
`str CertSubjectNameDN(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certsubjectnameoid"></a>CertSubjectNameOid
**Description :**  
Retourne hello Oid de nom de l’objet hello à partir d’un certificat.

**Syntaxe :**  
`str CertSubjectNameOid(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certthumbprint"></a>CertThumbprint
**Description :**  
Hello retourne l’empreinte numérique d’un certificat.

**Syntaxe :**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="certversion"></a>CertVersion
**Description :**  
Retourne hello version du format d’un certificat X.509.

**Syntaxe :**  
`str CertThumbprint(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.

- - -
### <a name="cguid"></a>CGuid
**Description :**  
Hello fonction CGuid convertit la représentation sous forme de chaîne hello d’une représentation binaire de GUID tooits.

**Syntaxe :**  
`bin CGuid(str GUID)`

* Une chaîne rédigée au format suivant : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ou {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}

- - -
### <a name="contains"></a>Contains
**Description :**  
fonction de Hello Contains recherche une chaîne à l’intérieur d’un attribut à valeurs multiples

**Syntaxe :**  
`num Contains (mvstring attribute, str search)` - sensible à la casse  
`num Contains (mvstring attribute, str search, enum Casetype)`  
`num Contains (mvref attribute, str search)` - sensible à la casse

* attribut : hello attribut à valeurs multiples toosearch.
* recherche : chaîne toofind dans l’attribut de hello.
* Casetype : CaseInsensitive ou CaseSensitive.

Retourne les index dans l’attribut à valeurs multiples hello où la chaîne de hello a été trouvé. 0 est retourné si la chaîne de hello est introuvable.

**Remarques :**  
Pour les attributs de chaîne à valeurs multiples, hello recherche sous-chaînes dans les valeurs hello.  
Pour les attributs de référence, hello chaîne recherchée doit correspondre exactement hello valeur toobe est considérée comme une correspondance.

**Exemple :**  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
Si l’attribut proxyAddresses de hello possède une adresse de messagerie principale (indiqué en majuscules « SMTP : »), puis revenez attribut proxyAddress de hello, sinon renvoie une erreur.

- - -
### <a name="convertfrombase64"></a>ConvertFromBase64
**Description :**  
Hello ConvertFromBase64 fonction convertit hello spécifié chaîne régulière du tooa valeur codée en base64.

**Syntaxe :**  
`str ConvertFromBase64(str source)` - part du principe que l’encodage utilisé est Unicode  
`str ConvertFromBase64(str source, enum Encoding)`

* source : chaîne encodée Base64  
* En codage : Unicode, ASCII, UTF8

**Exemple**  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

Les deux exemples renvoient «*Hello world!*»

- - -
### <a name="convertfromutf8hex"></a>ConvertFromUTF8Hex
**Description :**  
Hello ConvertFromUTF8Hex fonction convertit hello spécifié la chaîne de tooa valeur encodée en UTF8 hexadécimal.

**Syntaxe :**  
`str ConvertFromUTF8Hex(str source)`

* source : chaîne encodée sur 2 octets UTF8

**Remarques :**  
Hello différence entre cette fonction et ConvertFromBase64([],UTF8) dans ce résultat hello est convivial pour l’attribut de nom unique hello.  
Ce format est utilisé par Azure Active Directory en tant que nom de domaine.

**Exemple :**  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
Renvoie «*Hello world!*».

- - -
### <a name="converttobase64"></a>ConvertToBase64
**Description :**  
Hello fonction ConvertToBase64 convertit une chaîne de tooa la chaîne Unicode en base64.  
Convertit la valeur hello d’un tableau d’entiers tooits équivalent représentation encodée en chiffres base 64.

**Syntaxe :**  
`str ConvertToBase64(str source)`

**Exemple :**  
`ConvertToBase64("Hello world!")`  
Renvoie « SABlAGwAbABvACAAdwBvAHIAbABkACEA ».

- - -
### <a name="converttoutf8hex"></a>ConvertToUTF8Hex
**Description :**  
Hello ConvertToUTF8Hex fonction convertit une chaîne de tooa les valeur encodée en UTF8 hexadécimal.

**Syntaxe :**  
`str ConvertToUTF8Hex(str source)`

**Remarques :**  
le format de sortie Hello de cette fonction est utilisé par Azure Active Directory en tant que format d’attribut DN.

**Exemple :**  
`ConvertToUTF8Hex("Hello world!")`  
Renvoie 48656C6C6F20776F726C6421.

- - -
### <a name="count"></a>Count
**Description :**  
Hello fonction Count retourne le nombre de hello d’éléments dans un attribut à valeurs multiples

**Syntaxe :**  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a>CNum
**Description :**  
Hello fonction CNum prend une chaîne et retourne un type de données numérique.

**Syntaxe :**  
`num CNum(str value)`

- - -
### <a name="cref"></a>CRef
**Description :**  
Convertit un attribut de chaîne de référence tooa

**Syntaxe :**  
`ref CRef(str value)`

**Exemple :**  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a>CStr
**Description :**  
Hello pour la fonction CStr convertit le type de données de chaîne de tooa.

**Syntaxe :**  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* valeur : peut être une valeur numérique, un attribut de référence ou une valeur booléenne.

**Exemple :**  
`CStr([dn])`  
Peut renvoyer « cn=Joe,dc=contoso,dc=com ».

- - -
### <a name="dateadd"></a>DateAdd
**Description :**  
Retourne une valeur Date contenant une toowhich date qu'un intervalle de temps spécifié a été ajouté.

**Syntaxe :**  
`dt DateAdd(str interval, num value, dt date)`

* intervalle : expression qui est l’intervalle de salutation pendant laquelle vous souhaitez que tooadd de chaîne. chaîne de Hello doit avoir une des valeurs suivantes de hello :
  * yyyy Année
  * q Trimestre
  * m Mois
  * y Jour de l’année
  * s Jour
  * w Jour de la semaine
  * ww Semaine
  * h Heure
  * n Minute
  * s Seconde
* valeur : hello du nombre d’unités que tooadd. Il peut être positif (dates tooget Bonjour futures) ou négatif (dates tooget Bonjour passées).
* date : DateTime représentant date toowhich hello intervalle est ajouté.

**Exemple :**  
`DateAdd("m", 3, CDate("2001-01-01"))`  
Ajoute 3 mois et renvoie une valeur DateTime représentant « 2001-04-01 ».

- - -
### <a name="datefromnum"></a>DateFromNum
**Description :**  
Hello les fonction DateFromNum convertit une valeur dans tooa de format de date du AD type DateTime.

**Syntaxe :**  
`dt DateFromNum(num value)`

**Exemple :**  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
Renvoie une valeur DateTime représentant 2012-01-01 23:00:00.

- - -
### <a name="dncomponent"></a>DNComponent
**Description :**  
Hello les fonction DNComponent retourne la valeur hello un composant DN spécifié à partir de la gauche.

**Syntaxe :**  
`str DNComponent(ref dn, num ComponentNumber)`

* nom unique : hello référence attribut toointerpret
* ComponentNumber : composant hello hello DN tooreturn

**Exemple :**  
`DNComponent([dn],1)`  
Si dn est « cn=Joe,ou=… », la fonction renvoie Joe.

- - -
### <a name="dncomponentrev"></a>DNComponentRev
**Description :**  
Hello DNComponentRev fonction retourne la valeur hello d’un composant DN spécifié à partir de la droite (fin hello).

**Syntaxe :**  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* nom unique : hello référence attribut toointerpret
* ComponentNumber - composant hello dans hello DN tooreturn
* Options : contrôleur de domaine – ignorer tous les composants avec « dc = »

**Exemple :**  
Si le nom de domaine est « cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com », alors  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
Renvoient US.

- - -
### <a name="error"></a>Error
**Description :**  
Hello fonction Error est utilisée tooreturn une erreur personnalisée.

**Syntaxe :**  
`void Error(str ErrorMessage)`

**Exemple :**  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
Si hello attribut accountName n’est pas présent, provoquent une erreur sur l’objet de hello.

- - -
### <a name="escapedncomponent"></a>EscapeDNComponent
**Description :**  
Hello fonction EscapeDNComponent prend un composant d’un nom unique et l’échappe afin qu’il peut être représentée dans l’annuaire LDAP.

**Syntaxe :**  
`str EscapeDNComponent(str value)`

**Exemple :**  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
Garantit que l’objet de hello peut être créé dans un annuaire LDAP même si l’attribut displayName de hello comporte des caractères qui doivent être échappés dans l’annuaire LDAP.

- - -
### <a name="formatdatetime"></a>FormatDateTime
**Description :**  
fonction FormatDateTime de Hello est utilisé tooformat une chaîne de tooa date/heure au format spécifié.

**Syntaxe :**  
`str FormatDateTime(dt value, str format)`

* valeur : une valeur au format de DateTime hello
* format : une chaîne représentant le tooconvert de format hello pour.

**Remarques :**  
Hello les valeurs possibles pour le format de hello se trouve ici : [Formats de Date/heure définis par l’utilisateur (fonction Format)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)

**Exemple :**  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
Renvoie comme résultat « 2007-12-25 ».

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
Peut donner comme résultat « 20140905081453.0Z ».

- - -
### <a name="guid"></a>GUID
**Description :**  
fonction de Hello GUID génère un nouveau GUID aléatoire.

**Syntaxe :**  
`str GUID()`

- - -
### <a name="iif"></a>IIF
**Description :**  
Hello fonction IIF renvoie l’un d’un ensemble de valeurs possibles selon une condition spécifiée.

**Syntaxe :**  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* condition : toute valeur ou expression qui peut être évaluée tootrue ou false.
* valueIfTrue : si la condition de hello a la valeur tootrue, hello a retourné la valeur.
* valueIfFalse : si la condition de hello a la valeur toofalse, hello a retourné la valeur.

**Exemple :**  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 Si l’utilisateur hello est intern, retourne l’alias hello d’un utilisateur avec « t- » ajouté toohello début, sinon retourne hello alias de l’utilisateur en l’état.

- - -
### <a name="instr"></a>InStr
**Description :**  
Hello fonction InStr hello première occurrence d’une sous-chaîne dans une chaîne

**Syntaxe :**  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* contrôle de chaîne : toobe recherchée de chaîne
* correspondance de chaîne : chaîne toobe trouvé
* Démarrer : démarrage de position toofind hello sous-chaîne
* compare : vbTextCompare ou vbBinaryCompare

**Remarques :**  
Position de hello retourne où la sous-chaîne de hello a été trouvée ou 0 si introuvable.

**Exemple :**  
`InStr("hello quick brown fox","quick")`  
Dans la liste too5

`InStr("repEated","e",3,vbBinaryCompare)`  
Prend la valeur too7

- - -
### <a name="instrrev"></a>InStrRev
**Description :**  
Hello fonction InStrRev trouve hello dernière occurrence d’une sous-chaîne dans une chaîne

**Syntaxe :**  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* contrôle de chaîne : toobe recherchée de chaîne
* correspondance de chaîne : chaîne toobe trouvé
* Démarrer : démarrage de position toofind hello sous-chaîne
* compare : vbTextCompare ou vbBinaryCompare

**Remarques :**  
Position de hello retourne où la sous-chaîne de hello a été trouvée ou 0 si introuvable.

**Exemple :**  
`InStrRev("abbcdbbbef","bb")`  
Renvoie 7.

- - -
### <a name="isbitset"></a>IsBitSet
**Description :**  
fonction de Hello IsBitSet teste si un bit est défini ou non.

**Syntaxe :**  
`bool IsBitSet(num value, num flag)`

* valeur : valeur numérique qui est évaluée. Flag : valeur numérique qui a hello bit toobe évaluée

**Exemple :**  
`IsBitSet(&HF,4)`  
Renvoie la valeur True, car le bit « 4 » est défini dans la valeur hexadécimale de hello « F »

- - -
### <a name="isdate"></a>IsDate
**Description :**  
Si l’expression de hello peut être évalue en un type DateTime, hello fonction IsDate prend la valeur tooTrue.

**Syntaxe :**  
`bool IsDate(var Expression)`

**Remarques :**  
Utilisé toodetermine si CDate() peut aboutir.

- - -
### <a name="iscert"></a>IsCert
**Description :**  
Retourne la valeur true si les données brutes hello peuvent être sérialisées en objet de certificat .NET X509Certificate2.

**Syntaxe :**  
`bool CertThumbprint(binary certificateRawData)`  
*   certificateRawData : représentation en tableau d’octets d’un certificat X.509. tableau d’octets Hello peut être codés en binaire (DER) ou des données encodées en Base64 X.509.
- - -
### <a name="isempty"></a>IsEmpty
**Description :**  
Si l’attribut de hello est présent dans hello CS ou MV mais prend la valeur tooan une chaîne vide, puis hello IsEmpty évalue tooTrue.

**Syntaxe :**  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a>IsGuid
**Description :**  
Si la chaîne de hello a pu être converti tooa GUID, fonction IsGuid prend hello évaluée tootrue.

**Syntaxe :**  
`bool IsGuid(str GUID)`

**Remarques :**  
Un GUID est défini en tant que chaîne en fonction de l’un de ces modèles : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}.

Utilisé toodetermine si la fonction CGuid() peut aboutir.

**Exemple :**  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
Si la valeur StrAttribute de hello a un format de GUID, renvoie une représentation binaire, sinon retourne une valeur Null.

- - -
### <a name="isnull"></a>IsNull
**Description :**  
Si hello expression tooNull, IsNull (fonction) hello retourne true.

**Syntaxe :**  
`bool IsNull(var Expression)`

**Remarques :**  
Pour un attribut, une valeur Null est exprimée par l’absence de hello d’attribut de hello.

**Exemple :**  
`IsNull([displayName])`  
Renvoie la valeur True si l’attribut de hello n’est pas présent dans hello CS ou MV.

- - -
### <a name="isnullorempty"></a>IsNullOrEmpty
**Description :**  
Si l’expression de hello est une chaîne null ou vide, fonction de hello IsNullOrEmpty retourne true.

**Syntaxe :**  
`bool IsNullOrEmpty(var Expression)`

**Remarques :**  
Pour un attribut, il évaluait tooTrue si l’attribut de hello est absent ou n’est présent, mais est une chaîne vide.  
inverse Hello de cette fonction s’appelle IsPresent.

**Exemple :**  
`IsNullOrEmpty([displayName])`  
Renvoie la valeur True si l’attribut de hello n’est pas présent ou est une chaîne vide dans hello CS ou MV.

- - -
### <a name="isnumeric"></a>IsNumeric
**Description :**  
Hello fonction IsNumeric retourne une valeur booléenne indiquant si une expression peut être évaluée comme un type de nombre.

**Syntaxe :**  
`bool IsNumeric(var Expression)`

**Remarques :**  
Utilisé toodetermine si CNum() peut être l’expression de hello tooparse réussie.

- - -
### <a name="isstring"></a>IsString
**Description :**  
Si l’expression de hello peut être évaluée tooa type chaîne, puis hello fonction IsString prend tooTrue.

**Syntaxe :**  
`bool IsString(var expression)`

**Remarques :**  
Utilisé toodetermine si CStr() peut être l’expression de hello tooparse réussie.

- - -
### <a name="ispresent"></a>IsPresent
**Description :**  
Si hello expression chaîne tooa qui n’est pas Null et n’est pas vide, puis hello IsPresent fonction retourne la valeur true.

**Syntaxe :**  
`bool IsPresent(var expression)`

**Remarques :**  
inverse Hello de cette fonction s’appelle IsNullOrEmpty.

**Exemple :**  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a>Item
**Description :**  
Hello fonction Item retourne un élément à partir d’un chaîne/attribut à valeurs multiples.

**Syntaxe :**  
`var Item(mvstr attribute, num index)`

* attribute : attribut à valeurs multiples
* index : élément de tooan d’index dans la chaîne à valeurs multiples hello.

**Remarques :**  
Hello fonction Item est utile avec hello fonction Contains comme fonction de ce dernier hello retourne tooan élément index du hello dans un attribut à valeurs multiples hello.

Génère une erreur si l’index est hors limites.

**Exemple :**  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
Retourne hello adresse de messagerie principale.

- - -
### <a name="itemornull"></a>ItemOrNull
**Description :**  
Hello fonction ItemOrNull retourne un élément à partir d’un chaîne/attribut à valeurs multiples.

**Syntaxe :**  
`var ItemOrNull(mvstr attribute, num index)`

* attribute : attribut à valeurs multiples
* index : élément de tooan d’index dans la chaîne à valeurs multiples hello.

**Remarques :**  
Hello fonction ItemOrNull est utile avec hello fonction Contains comme fonction de ce dernier hello retourne tooan élément index du hello dans un attribut à valeurs multiples hello.

Renvoie une valeur Null si l’index est hors limites.

- - -
### <a name="join"></a>Join
**Description :**  
fonction de jointure Hello prend une chaîne à valeurs multiples et retourne une chaîne à valeur unique avec séparateur spécifié inséré entre chaque élément.

**Syntaxe :**  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* attribut : attribut à valeurs multiples contenant des chaînes toobe joint.
* délimiteur : toute chaîne tooseparate utilisé les sous-chaînes de hello Bonjour a retourné une chaîne. Si omis, hello caractère espace (« ») est utilisé. Si le délimiteur est une chaîne de longueur nulle (" ») ou rien du tout, tous les éléments de liste de hello sont concaténés sans délimiteurs.

**Remarques**  
Il existe une parité entre hello jointure et des fonctions de fractionnement. Hello fonction Join prend un tableau de chaînes et les joint à l’aide d’une chaîne de délimiteur, tooreturn une chaîne unique. Hello fonction Split prend une chaîne et la sépare au niveau du délimiteur hello, tooreturn un tableau de chaînes. Toutefois, la principale différence est que Join peut concaténer des chaînes avec n’importe quelle chaîne de délimiteur, Split peut uniquement séparer des chaînes à l’aide d’un délimiteur de caractère unique.

**Exemple :**  
`Join([proxyAddresses],",")`  
Peut retourner : « SMTP:john.doe@contoso.com,smtp:jd@contoso.com »

- - -
### <a name="lcase"></a>LCase
**Description :**  
Hello fonction LCase convertit tous les caractères dans un cas de toolower de chaîne.

**Syntaxe :**  
`str LCase(str value)`

**Exemple :**  
`LCase("TeSt")`  
Renvoie « test ».

- - -
### <a name="left"></a>Left
**Description :**  
fonction gauche Hello retourne un nombre spécifié de caractères à partir de la gauche hello d’une chaîne.

**Syntaxe :**  
`str Left(str string, num NumChars)`

* chaîne : hello caractères tooreturn de chaîne à partir de
* NumChars : nombre identifiant le nombre hello de tooreturn de caractères à partir du début hello (gauche) de chaîne

**Remarques :**  
Chaîne contenant les caractères numChars première hello dans la chaîne :

* Si numChars = 0, retourne une chaîne vide.
* Si numChars < 0, retourne une chaîne d’entrée.
* Si la chaîne est null, retourne une chaîne vide.

Si la chaîne contient moins de caractères que le nombre de hello spécifié dans numChars, une chaîne de toostring identiques (c'est-à-dire, contenant tous les caractères dans le paramètre 1) est retournée.

**Exemple :**  
`Left("John Doe", 3)`  
Renvoie « Joh ».

- - -
### <a name="len"></a>Len
**Description :**  
Hello fonction Len renvoie le nombre de caractères dans une chaîne.

**Syntaxe :**  
`num Len(str value)`

**Exemple :**  
`Len("John Doe")`  
Renvoie 8.

- - -
### <a name="ltrim"></a>LTrim
**Description :**  
Hello fonction LTrim supprime les espaces de début d’une chaîne.

**Syntaxe :**  
`str LTrim(str value)`

**Exemple :**  
`LTrim(" Test ")`  
Renvoie « Test ».

- - -
### <a name="mid"></a>Mid
**Description :**  
Hello Mid, fonction retourne un nombre spécifié de caractères à partir d’une position spécifiée dans une chaîne.

**Syntaxe :**  
`str Mid(str string, num start, num NumChars)`

* chaîne : hello caractères tooreturn de chaîne à partir de
* Démarrer : nombre identifiant hello en caractères tooreturn de chaîne à partir de la position de début
* NumChars : nombre identifiant le nombre de hello de tooreturn de caractères à partir de la position dans la chaîne

**Remarques :**  
Renvoie numChars caractères à partir de la position de départ dans la chaîne.  
Chaîne contenant numChars caractères à partir de la position de départ dans la chaîne :

* Si numChars = 0, retourne une chaîne vide.
* Si numChars < 0, retourne une chaîne d’entrée.
* Si Démarrer > hello longueur de chaîne, retourne la chaîne d’entrée.
* Si start < = 0, retourne une chaîne d’entrée.
* Si la chaîne est null, retourne une chaîne vide.

S’il ne reste pas numChars caractères dans la chaîne à partir de la position de départ, autant de caractères que possible sont renvoyés.

**Exemple :**  
`Mid("John Doe", 3, 5)`  
Renvoie « hn Do ».

`Mid("John Doe", 6, 999)`  
Renvoie « Doe ».

- - -
### <a name="now"></a>Now
**Description :**  
Hello maintenant fonction retourne une valeur DateTime spécifiant hello date et l’heure, en fonction de tooyour date l’ordinateur et heure système.

**Syntaxe :**  
`dt Now()`

- - -
### <a name="numfromdate"></a>NumFromDate
**Description :**  
Hello fonction NumFromDate renvoie une date dans le format de date AD.

**Syntaxe :**  
`num NumFromDate(dt value)`

**Exemple :**  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
Renvoie 129699324000000000.

- - -
### <a name="padleft"></a>PadLeft
**Description :**  
Hello PadLeft fonction gauche remplit un tooa de chaîne spécifiée à l’aide d’un caractère de remplissage fourni de longueur.

**Syntaxe :**  
`str PadLeft(str string, num length, str padCharacter)`

* chaîne : hello toopad de chaîne.
* longueur : un nombre entier représentant hello souhaité de longueur de chaîne.
* padCharacter : chaîne composée d’un toouse caractère unique en tant que caractère de remplissage hello

**Remarques :**

* Si la longueur de chaîne hello est inférieure à la longueur, padCharacter est ajouté à plusieurs reprises toohello début (gauche) de la chaîne jusqu'à ce qu’il a un toolength égale longueur.
* PadCharacter peut être un caractère d’espacement, mais il ne peut pas s’agir de la valeur null.
* Si la longueur de chaîne hello est égal tooor supérieure à la longueur, la chaîne est retournée sans modification.
* Si la chaîne a une longueur supérieure à ou un toolength égal, un toostring identiques de chaîne est retournée.
* Si la longueur de chaîne hello est inférieure à la longueur, une nouvelle chaîne Hello souhaité longueur est retournée contenant string remplie avec un padCharacter.
* Si la chaîne est null, la fonction hello retourne une chaîne vide.

**Exemple :**  
`PadLeft("User", 10, "0")`  
Renvoie « 000000User ».

- - -
### <a name="padright"></a>PadRight
**Description :**  
Hello PadRight fonction droite remplit un tooa de chaîne spécifiée à l’aide d’un caractère de remplissage fourni de longueur.

**Syntaxe :**  
`str PadRight(str string, num length, str padCharacter)`

* chaîne : hello toopad de chaîne.
* longueur : un nombre entier représentant hello souhaité de longueur de chaîne.
* padCharacter : chaîne composée d’un toouse caractère unique en tant que caractère de remplissage hello

**Remarques :**

* Si la longueur de chaîne hello est inférieure à la longueur, padCharacter est ajouté à plusieurs reprises toohello fin (droite) de la chaîne jusqu'à ce qu’il a un toolength égale longueur.
* PadCharacter peut être un caractère d’espacement, mais il ne peut pas s’agir de la valeur null.
* Si la longueur de chaîne hello est égal tooor supérieure à la longueur, la chaîne est retournée sans modification.
* Si la chaîne a une longueur supérieure à ou un toolength égal, un toostring identiques de chaîne est retournée.
* Si la longueur de chaîne hello est inférieure à la longueur, une nouvelle chaîne Hello souhaité longueur est retournée contenant string remplie avec un padCharacter.
* Si la chaîne est null, la fonction hello retourne une chaîne vide.

**Exemple :**  
`PadRight("User", 10, "0")`  
Renvoie « User000000 ».

- - -
### <a name="pcase"></a>PCase
**Description :**  
Hello fonction PCase convertit hello premier caractère de chaque mot délimité par des espaces dans un cas de tooupper de chaîne, et tous les autres caractères sont converties en cas de toolower.

**Syntaxe :**  
`String PCase(string)`

**Remarques :**

* Cette fonction ne fournit pas actuellement une casse appropriée tooconvert un mot qui est entièrement en majuscule, par exemple un acronyme.

**Exemple :**  
`PCase("TEsT")`  
Renvoie « test ».

`PCase(LCase("TEST"))`  
Renvoie « Test ».

- - -
### <a name="randomnum"></a>RandomNum
**Description :**  
Hello fonction RandomNum retourne un nombre aléatoire entre un intervalle spécifié.

**Syntaxe :**  
`num RandomNum(num start, num end)`

* Démarrer : une identification hello inférieure limite de hello valeur aléatoire toogenerate
* fin : une identification hello supérieur limite de hello valeur aléatoire toogenerate

**Exemple :**  
`Random(100,999)`  
Peut renvoyer 734.

- - -
### <a name="removeduplicates"></a>RemoveDuplicates
**Description :**  
Hello fonction RemoveDuplicates prend une chaîne à valeurs multiples et assurez-vous que chaque valeur est unique.

**Syntaxe :**  
`mvstr RemoveDuplicates(mvstr attribute)`

**Exemple :**  
`RemoveDuplicates([proxyAddresses])`  
Renvoie un attribut proxyAddress expurgé duquel toutes les valeurs en double ont été supprimées.

- - -
### <a name="replace"></a>Replace
**Description :**  
Hello fonction Replace remplace toutes les occurrences d’une chaîne tooanother de chaîne.

**Syntaxe :**  
`str Replace(str string, str OldValue, str NewValue)`

* chaîne : les valeurs dans un tooreplace de chaîne.
* Ancienne valeur : tooreplace et toosearch de chaîne hello pour.
* NewValue : hello chaîne tooreplace à.

**Remarques :**  
fonction Hello reconnaît hello suivant monikers spéciaux suivants :

* \n – Nouvelle ligne
* \r – Retour chariot
* \t – Tabulation

**Exemple :**  
`Replace([address],"\r\n",", ")`  
Remplace CRLF par une virgule et un espace et peut entraîner une trop « One Microsoft Way, Redmond, WA, États-Unis »

- - -
### <a name="replacechars"></a>ReplaceChars
**Description :**  
Hello fonction ReplaceChars remplace toutes les occurrences des caractères trouvés dans hello chaîne ReplacePattern.

**Syntaxe :**  
`str ReplaceChars(str string, str ReplacePattern)`

* chaîne : un tooreplace de chaîne de caractères dans.
* ReplacePattern : une chaîne qui contient un dictionnaire avec tooreplace de caractères.

Hello format est {source1} : {cible1}, {source2} : {cible2}, {sourceN}, {Ciblen} où source est hello caractère toofind et cible hello chaîne tooreplace avec.

**Remarques :**

* fonction Hello prend chaque occurrence des sources définies et les remplace par les cibles hello.
* source de Hello doit être exactement un caractère (unicode).
* source de Hello ne peut pas être vide ni dépasser un caractère (erreur d’analyse).
* cible de Hello peut avoir plusieurs caractères, par exemple ö : oe, β : ss.
* cible de Hello peut être vide, indiquant que les caractères hello doivent être supprimés.
* source de Hello respecte la casse et doit être une correspondance exacte.
* Bonjour, (virgule) et : (deux-points) sont des caractères réservés et ne peut pas être remplacé à l’aide de cette fonction.
* Les espaces et autres caractères blancs Bonjour chaîne ReplacePattern sont ignorés.

**Exemple :**  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
Renvoie Raksmorgas.

`ReplaceChars("O’Neil",%ReplaceString%)`  
Retourne « ONeil », graduation hello est défini toobe supprimé.

- - -
### <a name="right"></a>Right
**Description :**  
fonction Hello retourne un nombre spécifié de caractères à partir de hello droite (fin) d’une chaîne.

**Syntaxe :**  
`str Right(str string, num NumChars)`

* chaîne : hello caractères tooreturn de chaîne à partir de
* NumChars : nombre identifiant le nombre de hello de tooreturn caractères de fin hello (à droite) de chaîne

**Remarques :**  
Les caractères NumChars sont retournées à partir de la dernière position de hello de chaîne.

Chaîne contenant les caractères numChars dernière hello dans la chaîne :

* Si numChars = 0, retourne une chaîne vide.
* Si numChars < 0, retourne une chaîne d’entrée.
* Si la chaîne est null, retourne une chaîne vide.

Si la chaîne contient moins de caractères hello nombre spécifié dans NumChars, une toostring identiques de chaîne est retournée.

**Exemple :**  
`Right("John Doe", 3)`  
Renvoie « Doe ».

- - -
### <a name="rtrim"></a>RTrim
**Description :**  
Hello RTrim (fonction) supprime les espaces de fin d’une chaîne.

**Syntaxe :**  
`str RTrim(str value)`

**Exemple :**  
`RTrim(" Test ")`  
Renvoie « Test ».

- - -
### <a name="select"></a>Sélectionnez
**Description :**  
Traite toutes les valeurs d’un attribut à valeurs multiples (ou la sortie d’une expression) selon la fonction spécifiée.

**Syntaxe :**  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* élément : représente un élément dans un attribut à valeurs multiples hello
* attribut : attribut à valeurs multiples hello
* expression : expression qui retourne une collection de valeurs
* condition : n’importe quelle fonction qui peut traiter un élément dans l’attribut de hello

**Exemples :**  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
Retourner toutes les valeurs hello dans donnez d’attribut à valeurs multiples hello après la suppression des traits d’union (-).

- - -
### <a name="split"></a>Split
**Description :**  
Hello fonction Split prend une chaîne séparée par un délimiteur et le rend une chaîne à valeurs multiples.

**Syntaxe :**  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* valeur : hello chaîne avec un tooseparate de caractère délimiteur.
* délimiteur : unique toobe de caractère utilisé comme séparateur de hello.
* limit : nombre maximal de valeurs qu’il est possible de renvoyer.

**Exemple :**  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
Retourne une chaîne à valeurs multiples comprenant 2 éléments utiles pour l’attribut proxyAddress de hello.

- - -
### <a name="stringfromguid"></a>StringFromGuid
**Description :**  
Hello fonction StringFromGuid prend un GUID binaire et il convertit la chaîne de tooa

**Syntaxe :**  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a>StringFromSid
**Description :**  
Hello les fonction StringFromSid convertit un tableau d’octets contenant la chaîne tooa d’identification de sécurité.

**Syntaxe :**  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a>Switch
**Description :**  
fonction Switch de Hello est tooreturn utilisé une valeur unique en fonction des conditions évaluées.

**Syntaxe :**  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* expr : expression de type Variant tooevaluate.
* valeur : valeur toobe retournée si l’expression correspondante hello est True.

**Remarques :**  
Hello argument de la fonction Switch liste se compose de paires d’expressions et de valeurs. expressions de Hello sont évaluées de gauche tooright et valeur hello associée hello première expression tooevaluate tooTrue est retournée. Si les parties hello ne sont pas correctement appariées, une erreur d’exécution se produit.

Par exemple, si expr1 est True, Switch renvoie la valeur1. Si expr-1 est False, mais expr-2 est True, Switch renvoie la valeur 2, et ainsi de suite.

Switch ne renvoie rien si :

* Aucune des expressions de hello ont la valeur True.
* première expression de True Hello possède une valeur correspondante qui a la valeur Null.

Switch évalue toutes les expressions, même si elle n’en renvoie qu’une. Pour cette raison, il est conseillé de surveiller les éventuels effets secondaires. Par exemple, si l’évaluation de hello d’une expression entraîne une division par zéro, une erreur se produit.

Valeur peut être également la fonction d’erreur hello, qui retourne une chaîne personnalisée.

**Exemple :**  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
Renvoie la langue de hello parlée dans certaines grandes villes, sinon retourne une erreur.

- - -
### <a name="trim"></a>Trim
**Description :**  
fonction Trim Hello supprime les espaces à gauche et blanc à partir d’une chaîne.

**Syntaxe :**  
`str Trim(str value)`  

**Exemple :**  
`Trim(" Test ")`  
Renvoie « test ».

`Trim([proxyAddresses])`  
Supprime les espaces à gauche et pour chaque valeur de l’attribut proxyAddress de hello.

- - -
### <a name="ucase"></a>UCase
**Description :**  
Hello fonction UCase convertit tous les caractères dans un cas de tooupper de chaîne.

**Syntaxe :**  
`str UCase(str string)`

**Exemple :**  
`UCase("TeSt")`  
Renvoie « test ».

- - -
### <a name="where"></a>Where

**Description :**  
Retourne un sous-ensemble de valeurs d’un attribut à valeurs multiples (ou la sortie d’une expression) en fonction de la condition.

**Syntaxe :**  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* élément : représente un élément dans un attribut à valeurs multiples hello
* attribut : attribut à valeurs multiples hello
* condition : toute expression qui peut être évaluée tootrue ou false
* expression : expression qui retourne une collection de valeurs

**Exemple :**  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
Retourner des valeurs de certificat hello dans userCertificate d’attribut à valeurs multiples hello qui ne sont pas expiré.

- - -
### <a name="with"></a>With
**Description :**  
Hello avec fonction fournit une toosimplify de façon à une expression complexe à l’aide d’une variable toorepresent une sous-expression qui apparaît une ou plusieurs fois dans une expression complexe de hello.

**Syntaxe**
`With(var variable, exp subExpression, exp complexExpression)` :  
* variable : représente hello sous-expression.
* subExpression : sous-expression représentée par une variable.
* complexExpression : expression complexe.

**Exemple :**  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
Fonctionnellement équivalent à :  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
Qui retourne uniquement les valeurs de certificat valide dans l’attribut userCertificate de hello.


- - -
### <a name="word"></a>Word
**Description :**  
Hello fonction Word renvoie un mot contenu dans la chaîne, en fonction des paramètres décrivant hello délimiteurs toouse et tooreturn nombre du mot hello.

**Syntaxe :**  
`str Word(str string, num WordNumber, str delimiters)`

* chaîne : hello chaîne tooreturn un mot.
* WordNumber : nombre identifiant le nombre de mots à renvoyer.
* délimiteurs : une chaîne représentant un ou plusieurs délimiteurs hello qui doivent être utilisés tooidentify mots

**Remarques :**  
Chaque chaîne de caractères dans une chaîne séparée par hello un des caractères hello dans les délimiteurs sont identifiés en tant que mots :

* Si number < 1, retourne une chaîne vide.
* Si string a la valeur null, renvoie une chaîne vide.

Si la chaîne contient moins de mots ou ne contient pas les mots identifiés par les séparateurs, une chaîne vide est renvoyée.

**Exemple :**  
`Word("hello quick brown fox",3," ")`  
Retourne « brown ».

`Word("This,string!has&many separators",3,",!&#")`  
Retourne « has ».

## <a name="additional-resources"></a>Ressources supplémentaires
* [Comprendre les expressions d’approvisionnement déclaratif](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [Azure AD Connect Sync : personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)
