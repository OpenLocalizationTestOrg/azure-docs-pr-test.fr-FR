---
title: "attributs de clichés instantanés du service de synchronisation aaaAzure AD Connect | Documents Microsoft"
description: "Décrit le fonctionnement des attributs des clichés instantanés dans le service de synchronisation Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a>Attributs de clichés instantanés du service de synchronisation Azure AD Connect
La plupart des attributs sont représentés hello même façon dans Azure AD dans votre annuaire Active Directory local. Mais certains attributs ont une gestion spéciale et valeur d’attribut hello dans Azure AD peut être différente de celle se synchronise Azure AD Connect.

## <a name="introducing-shadow-attributes"></a>Présentation des attributs des clichés instantanés
Certains attributs ont deux représentations dans Azure AD. Valeur de local hello et une valeur calculée sont stockés. Ces attributs supplémentaires sont appelés attributs de clichés instantanés. sont des attributs les plus courants Hello deux où vous voyez ce comportement **userPrincipalName** et **proxyAddress**. modification de Hello dans les valeurs d’attribut se produit lorsque des valeurs de ces attributs représentant des domaines non vérifiés. Mais le moteur de synchronisation hello dans se connecter lit valeur hello dans l’attribut de clichés instantanés hello ainsi son point de vue, attribut de hello a été confirmée par Azure AD.

Vous ne voyez pas les attributs de clichés instantanés hello à l’aide de hello portail Azure ou avec PowerShell. Mais le concept hello de présentation vous aide à vous tootroubleshoot certains scénarios où l’attribut hello a des valeurs différentes sur site et dans le cloud de hello.

toobetter comprendre le comportement de hello, examinez cet exemple de Fabrikam :  
![Domaines](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
Ils ont plusieurs suffixes UPN dans leur Active Directory local, mais ils n’en ont vérifié qu’un.

### <a name="userprincipalname"></a>userPrincipalName
Un utilisateur a hello suivant de valeurs d’attribut dans un domaine non vérifié :

| Attribut | Valeur |
| --- | --- |
| userPrincipalName local | lee.sperry@fabrikam.com |
| shadowUserPrincipalName dans Azure AD | lee.sperry@fabrikam.com |
| userPrincipalName dans Azure AD | lee.sperry@fabrikam.onmicrosoft.com |

attribut userPrincipalName de Hello est la valeur hello qui se qu'affiche lors de l’utilisation de PowerShell.

Comme valeur d’attribut hello réel local est stocké dans Azure AD, lorsque vous vérifiez le domaine fabrikam.com de hello, AD Azure met à jour l’attribut userPrincipalName de hello valeur hello hello shadowUserPrincipalName. Vous n’avez pas de le toosynchronize les modifications à partir d’Azure AD Connect pour ces toobe valeurs mises à jour.

### <a name="proxyaddresses"></a>proxyAddresses
Hello même processus pour inclure uniquement des domaines vérifiés se produit également pour proxyAddresses, mais avec une logique supplémentaire. vérification de Hello pour les domaines vérifiés se produit uniquement pour les utilisateurs de boîte aux lettres. Un utilisateur ou un contact représentent un utilisateur dans une autre organisation Exchange et vous pouvez ajouter toutes les valeurs dans les objets toothese proxyAddresses.

Pour un utilisateur de boîte aux lettres, en local ou dans Exchange Online, seules les valeurs pour les domaines vérifiés s’affichent. Vous devriez voir quelque chose de semblable à ceci :

| Attribut | Valeur |
| --- | --- |
| proxyAddresses local | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| proxyAddresses dans Exchange Online | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

Dans ce cas **smtp:abbie.spencer@fabrikam.com** a été supprimée, car ce domaine n’a pas été vérifié. Mais Exchange a également ajouté **SIP:abbie.spencer@fabrikamonline.com**. Fabrikam n’a pas utilisé Lync/Skype en local, mais Azure AD et Exchange Online s’y préparent.

Cette logique pour proxyAddresses est référencé tooas **ProxyCalc**. ProxyCalc est appelé à chaque modification d’un utilisateur lorsque :

- utilisateur de Hello a été affecté à un plan de service qui inclut Exchange Online, même si l’utilisateur de hello n’était pas autorisée pour l’échange. Par exemple, si hello utilisateur est affecté hello Office E3 SKU, mais ne l’a été attribué SharePoint Online. Cela est vrai même si votre boîte aux lettres est toujours locale.
- Hello attribut msExchRecipientTypeDetails a une valeur.
- Vous apportez une modification tooproxyAddresses ou l’userPrincipalName.

ProxyCalc peut prendre quelques tooprocess temps une modification sur un utilisateur et n’est pas synchrone avec le processus d’exportation hello Azure AD Connect.

> [!NOTE]
> Hello ProxyCalc logique a quelques comportements supplémentaires pour des scénarios avancés ne pas documentés dans cette rubrique. Cette rubrique est fourni pour vous toounderstand hello comportement et ne documente pas toute la logique interne.

### <a name="quarantined-attribute-values"></a>Valeurs d’attribut en quarantaine
Les attributs de clichés instantanés sont également utilisés lorsque des valeurs d’attribut sont en double. Pour plus d’informations, consultez [Résilience d’attribut en double](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).

## <a name="see-also"></a>Voir aussi
* [Synchronisation d’Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
