---
title: "Azure AD Connect Sync : Présentation des utilisateurs et des contacts | Microsoft Docs"
description: "Décrit les utilisateurs et les contacts dans Azure AD Connect Sync."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d204647-213a-4519-bd62-49563c421602
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: 4d80648c53a2981eb2626338913ed2282423f183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-users-and-contacts"></a>Azure AD Connect Sync : Présentation des utilisateurs et des contacts
Il existe plusieurs raisons pour lesquelles vous pouvez avoir plusieurs forêts Active Directory et il existe plusieurs topologies de déploiement différentes. Parmi les modèles courants, citons les déploiements de ressources de comptes et les forêts avec liste d’adresses globale synchronisées après fusion et acquisition. Mais même s’il existe des modèles pures, les modèles hybrides sont également courants. configuration par défaut de Hello dans la synchronisation Azure AD Connect n’assume pas un modèle particulier, mais en fonction de la correspondance d’utilisateur a été sélectionné dans le guide d’installation Bonjour, des comportements différents peuvent être observées.

Dans cette rubrique, nous verrons comment se comporte la configuration par défaut de hello dans certaines topologies. Nous allons examiner la configuration de hello et hello Éditeur des règles de synchronisation peut être toolook utilisé lors de la configuration de hello.

Il existe quelques règles générales de configuration hello suppose :

* Quelle que soit l’ordre dans nous importer à partir de la source de hello annuaires Active Directory, lequel résultat final de hello doit toujours être hello même.
* Un compte actif fournira toujours des informations de connexion, y compris **userPrincipalName** et **sourceAnchor**.
* Un compte désactivé contribue à userPrincipalName et sourceAnchor, sauf s’il est une boîte aux lettres liée, s’il n’existe aucun toobe compte actif trouvé.
* Un compte avec une boîte aux lettres liée ne sera jamais utilisé pour userPrincipalName et sourceAnchor. On part du principe qu’un compte actif sera trouvé ultérieurement.
* Un objet de contact peut être tooAzure configuré AD sous la forme d’un contact ou un utilisateur. Vous ne saurez s’il s’agit de l’un ou de l’autre qu’une fois que toutes les forêts Active Directory sources auront été traitées.

## <a name="contacts"></a>Contacts
Avoir des contacts représentant un utilisateur dans une autre forêt est courant après une fusion et acquisition où une solution GALSync joue le rôle de pont entre plusieurs forêts Exchange. objet de contact Hello est toujours joint de hello connecteur espace toohello métaverse à l’aide de l’attribut de messagerie hello. S’il existe déjà un objet contact ou utilisateur avec hello même adresse de messagerie, les objets hello sont joints entre eux. Cette option est configurée dans la règle de hello **dans depuis AD-jointure de Contact**. Il existe également une règle nommée **dans depuis AD-Contact courant** avec un attribut de métaverse flux toohello **sourceObjectType** avec la constante de hello **Contact**. Cette règle a une priorité très basse, donc si un objet utilisateur est toohello joints à un même objet de métaverse, puis la règle de hello **dans depuis AD-utilisateur courant** contribuera attribut toothis de hello valeur utilisateur. Avec cette règle, cet attribut aura la valeur de hello Contact si aucun utilisateur n’a pas été joint et hello valeur User si au moins un utilisateur a été trouvé.

Pour la configuration d’un tooAzure d’objet Active Directory, hello règle de trafic sortant **Out tooAAD : jointure de Contact** crée un objet de contact si hello attribut du métaverse **sourceObjectType** est défini trop**contactez** . Si cet attribut est défini trop**utilisateur**, puis les règles hello **hors tooAAD – User Join** crée un objet utilisateur à la place.
Il est possible qu’un objet est promu de Contact tooUser lorsque plusieurs annuaires Active Directory de source sont importés et synchronisés.

Par exemple, dans une topologie GALSync nous sera trouver des objets contact pour tout le monde dans hello seconde forêt quand nous importerons la première forêt de hello. Cela s’effectuera les nouveaux objets contacts Bonjour connecteur AAD. Lorsque plus tard, nous importer et synchroniser la seconde forêt de hello, nous recherche hello utilisateurs réels et les attacher toohello les objets du métaverse existants. Puis nous supprimer l’objet de contact hello dans AAD et créer un nouvel objet utilisateur à la place.

Si vous avez une topologie où les utilisateurs sont représentés en tant que contacts, veillez à que sélectionner les utilisateurs toomatch sur l’attribut de messagerie hello hello guide d’installation. Si vous sélectionnez une autre option, vous aurez une configuration dépendant de l’ordre. Objets de contact seront toujours joints à l’attribut de messagerie hello, mais les objets utilisateur ne seront joints à l’attribut de messagerie hello que si cette option a été sélectionnée dans le guide d’installation hello. Vous pourriez puis finir avec deux objets différents dans le métaverse hello avec hello même attribut de messagerie si l’objet de contact hello a été importé avant l’objet utilisateur de hello. Au cours de l’exportation tooAzure AD, une erreur est levée. Ce comportement est normal et indique des données incorrectes ou cette topologie hello n’a pas été correctement identifiée lors de l’installation de hello.

## <a name="disabled-accounts"></a>Comptes désactivés
Comptes désactivés sont également synchronisés tooAzure AD. Comptes désactivés sont des ressources communes toorepresent dans Exchange, par exemple des salles de conférence. exception de Hello concerne les utilisateurs ayant une boîte aux lettres liée ; comme mentionné précédemment, ces configure jamais un tooAzure de compte Active Directory.

hypothèse de Hello est que si un compte d’utilisateur désactivé est trouvé, nous ne trouverons pas un autre compte actif plus tard et l’objet hello est approvisionné tooAzure AD avec hello userPrincipalName et sourceAnchor trouvés. Dans le cas, un autre compte actif joindra toohello même objet de métaverse, puis ses userPrincipalName et sourceAnchor sera utilisé.

## <a name="changing-sourceanchor"></a>Changement de l’attribut sourceAnchor
Lorsqu’un objet a été exporté tooAzure AD, puis il n’est pas autorisée toochange hello sourceAnchor plus. Lorsque les objets hello a été attribut du métaverse hello exportée **cloudSourceAnchor** est définie avec hello **sourceAnchor** valeur acceptée par Azure AD. Si **sourceAnchor** est modifié et ne correspond pas à **cloudSourceAnchor**, règle de hello **hors tooAAD – User Join** lèvera une erreur de hello **attribut sourceAnchor a changé**. Dans ce cas, la configuration de hello ou les données doivent être corrigées par conséquent hello même sourceAnchor est présent dans le métaverse hello à nouveau avant de l’objet de hello peut être de nouveau synchronisé.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Azure AD Connect Sync : personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)

