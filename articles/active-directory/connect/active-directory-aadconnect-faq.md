---
title: "Azure Active Directory Connect : Forum Aux Questions | Microsoft Docs"
description: "Cette page comporte le Forum Aux Questions relatif à Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a>Forum Aux Questions sur Azure Active Directory Connect

## <a name="general-installation"></a>Installation générale
**Q : installation fonctionnera si hello un administrateur Global Azure AD a 2FA activé ?**  
Hello des générations à partir de février 2016, cela est pris en charge.

**Q : existe-t-il un moyen de tooinstall sans assistance Azure AD Connect ?**  
Il est uniquement pris en charge tooinstall Azure AD Connect à l’aide de l’Assistant installation hello. Une installation automatique et silencieuse n’est pas prise en charge.

**Q : Je possède une forêt dans laquelle un domaine ne peut pas être contacté. Comment installer Azure AD Connect ?**  
Hello des générations à partir de février 2016, cela est pris en charge.

**Q : hello travail de l’agent d’intégrité de domaine Active Directory sur server core ?**  
Oui. Après avoir installé l’agent de hello, vous pouvez terminer le processus de l’inscription de hello à l’aide de hello suivant l’applet de commande PowerShell : 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a>Réseau
**Q : je dispose d’un pare-feu, un périphérique réseau, ou quelque chose d’autre qui limite les connexions de durée maximale hello peut rester ouvert sur mon réseau. Quel doit être le seuil de délai côté client lors de l’utilisation d’Azure AD Connect ?**  
Tous les logiciels de mise en réseau, périphériques physiques ou tout autre élément hello durée maximale de connexions peuvent ouvrir doit utiliser un seuil d’au moins 5 minutes (300 secondes) pour la connectivité entre les limites hello serveur sur lequel hello Azure AD Connect client est installé et Azure Active Directory. Cela s’applique également des outils de synchronisation de Microsoft Identity tooall précédemment publiée.

**Q : Les domaines avec un nom en une seule partie sont-ils pris en charge ?**  
Non, Azure AD Connect ne prend pas en charge les forêts/domaines locaux utilisant des noms de domaine en une seule partie.

**Q : Les noms NetBios comportant un point sont-ils pris en charge ?**  
Non, Azure AD Connect ne prend pas en charge localement forêts/domaines où le nom NetBios hello contient un point «. » dans le nom de hello.

## <a name="federation"></a>Fédération
**Q : que faire si je reçois un message électronique qui me demande toorenew mon certificat Office 365**  
Utilisez les instructions de hello qui sont décrite dans hello [renouveler les certificats](active-directory-aadconnect-o365-certs.md) rubrique sur la façon dont toorenew hello certificat.

**Q : « Mettre à jour automatiquement la partie de confiance » est défini pour la partie de confiance Office 365. Dois-je tootake n’importe quelle action lorsque mon automatiquement le certificat de signature de jeton survole ?**  
Utilisez les instructions de hello qui sont décrite dans l’article de hello [renouveler les certificats](active-directory-aadconnect-o365-certs.md).

## <a name="environment"></a>Environnement
**Q : est-il pris en charge d’informatique toorename hello server après l’installation d’Azure AD Connect ?**  
Non. Modification du nom de serveur hello toonot de moteur de synchronisation de hello cause sera en mesure de tooconnect toohello base de données SQL et le service de hello ne sera pas en mesure de toostart.

## <a name="identity-data"></a>Données d’identité
**Q : attribut de nom UPN (userPrincipalName) hello dans Azure AD ne correspond pas à hello UPN de local - pourquoi ?**  
Reportez-vous aux articles suivants :

* [Les noms d’utilisateur ne correspondent pas dans Office 365, Azure ou Intune hello UPN local ou l’ID de connexion de remplacement](https://support.microsoft.com/en-us/kb/2523192)
* [Les modifications ne sont pas synchronisées par l’outil de synchronisation Azure Active Directory hello après avoir modifié hello UPN d’un toouse de compte d’utilisateur un autre domaine fédéré](https://support.microsoft.com/en-us/kb/2669550)

Vous pouvez également configurer Azure AD tooallow hello synchronisation moteur tooupdate hello userPrincipalName comme décrit dans [fonctionnalités de service de synchronisation Azure AD Connect](active-directory-aadconnectsyncservice-features.md).

**Q : est informatique pris en charge toosoft correspondance locale objets AD groupe/Contact avec les objets groupe contacter Azure Active Directory existants ?**  
Non, cela n’est pas pris en charge actuellement.

**Q : est-il informatique pris en charge toomanually définie ImmutableId attribut sur Azure AD groupe/Contact existant objets toohard établit une correspondance avec local tooon objets AD groupe/Contact ?**  
Non, cela n’est pas pris en charge actuellement.



## <a name="custom-configuration"></a>Configuration personnalisée
**Q : où se trouvent les applets de commande PowerShell hello pour Azure AD Connect documentée ?**  
Avec l’exception hello d’applets de commande hello sur ce site, autres applets de commande PowerShell trouvés dans Azure AD Connect ne sont pas pris en charge par le client.

**Q : puis-je utiliser la fonctionnalité « Importation de serveur d’exportation serveur » trouvée dans *Synchronization Service Manager* configuration toomove entre les serveurs ?**  
Non. Cette option ne récupérera pas tous les paramètres de configuration et ne doit pas être utilisée. À la place utilisez hello Assistant toocreate hello base de configuration sur le second serveur de hello et utiliser hello synchronisation règle éditeur toogenerate PowerShell scripts toomove toute règle personnalisée entre les serveurs. Consultez la section [Migration « Swing »](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).

**Q : les mots de passe peuvent être mis en cache pour la page de hello signe dans Azure et peut cela impossible, car il contient un élément input de mot de passe avec la saisie semi-automatique hello = attribut « false » ?**</br>
Actuellement, nous ne permettent pas de modification d’attributs HTML hello du champ de saisie du mot de passe hello, y compris la balise de la saisie semi-automatique hello. Nous travaillons actuellement sur une fonctionnalité qui permet de code Javascript personnalisé qui vous permettra de tooadd n’importe quel champ de mot de passe toohello attribut. Cette fonctionnalité devrait être accessible courant 2017.

**Q : sur hello Azure-page de connexion, les noms d’utilisateur pour les utilisateurs qui ont précédemment connecté sont affichés.  Est-il possible de désactiver ce comportement ?**</br>
Actuellement, nous ne permettent pas de modification d’attributs HTML hello de hello-page de connexion. Nous travaillons actuellement sur une fonctionnalité qui permet de code Javascript personnalisé qui vous permettra de tooadd n’importe quel champ de mot de passe toohello attribut. Cette fonctionnalité devrait être accessible courant 2017.

**Q : existe-t-il un moyen tooprevent sessions simultanées ?**</br>
Non.



## <a name="troubleshooting"></a>Résolution des problèmes
**Q : Comment puis-je obtenir de l’aide avec Azure AD Connect ?**

[Rechercher hello Base de connaissances Microsoft (KB)](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* Rechercher hello Base de connaissances Microsoft (KB) pour les problèmes de réparation toocommon solutions techniques sur la prise en charge d’Azure AD Connect.

[Forums Microsoft Azure Active Directory](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* Vous pouvez rechercher et Parcourir pour technical questions et réponses à partir de la Communauté de hello ou demandez à votre propre question en cliquant sur [ici](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).

[Service clientèle Azure AD Connect](https://manage.windowsazure.com/?getsupport=true)

* Utilisez cette prise en charge de tooget lien via hello portail Azure.

