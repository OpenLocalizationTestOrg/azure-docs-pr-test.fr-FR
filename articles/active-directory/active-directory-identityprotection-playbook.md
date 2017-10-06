---
title: "manuel de la Protection d’identité Active Directory aaaAzure | Documents Microsoft"
description: "Découvrez comment Azure AD Identity Protection vous permet capacité hello toolimit une personne malveillante de tooexploit une identité compromise ou l’unité et toosecure une identité ou un périphérique qui a été précédemment toobe suspectée ou connu compromis."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestion d’applications, sécurité, risque, niveau de risque, vulnérabilité, stratégie de sécurité"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a>Manuel d’Azure Active Directory Identity Protection
Ce manuel vous aide à :

* Remplir les données dans l’environnement de Protection de l’identité de hello par des vulnérabilités et les événements à risque simulation
* Définir des stratégies d’accès conditionnel en fonction du risque et d’impact hello de ces stratégies de test

## <a name="simulating-risk-events"></a>Simulation des événements à risque
Cette section vous fournit les étapes pour simulation hello suivant les types d’événements risque :

* Connexions depuis des adresses IP anonymes (facile)
* Connexions depuis des emplacements non connus (moyen)
* Emplacements de tooatypical voyage impossible (difficiles)

Les autres événements à risque ne peuvent pas être simulés de manière sécurisée.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Connexions depuis des adresses IP anonymes
Ce type d’événement à risque signale les utilisateurs qui se sont connectés depuis une adresse IP ayant été identifiée comme l’adresse IP d’un proxy anonyme. Ces proxies sont utilisés par des personnes qui veulent toohide son leur adresse IP et peut être utilisé dans un but malveillant.

**toosimulate une sign-in à partir d’une adresse IP anonyme, effectuer hello suit**:

1. Télécharger hello [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).
2. À l’aide de hello Tor Browser, accédez trop[https://myapps.microsoft.com](https://myapps.microsoft.com).   
3. Entrez les informations d’identification hello du compte hello tooappear Bonjour **-connexions à partir d’adresses IP anonymes** rapport.

Connectez-vous Hello apparaîtront sur le tableau de bord de Protection de l’identité hello dans les 5 minutes. 

### <a name="sign-ins-from-unfamiliar-locations"></a>Connexions depuis des emplacements non connus
Hello risque d’emplacements non connus est un mécanisme d’évaluation de connexion en temps réel qui prend en compte au-delà de l’authentification dans les emplacements (IP, la Latitude / Longitude et ASN) toodetermine des emplacements inhabituels / nouveau. système de Hello stocke IPs précédente, la Latitude / Longitude et homologations d’un utilisateur et considère que ces emplacements familiers toobe. Un emplacement de connexion est considéré comme inconnu si hello emplacement de connexion ne correspond pas à un des emplacements familier de hello existant.

Azure Active Directory Identity Protection :  

* présente une période d’apprentissage initiale de 14 jours, durant laquelle il ne signale pas les nouveaux emplacements en tant qu’emplacements non connus.
* ignore les connexions à partir de périphériques familières et emplacements des familier existant tooan géographiquement fermer.

les emplacements non connus toosimulate, vous avez toosign dans à partir d’un emplacement et un périphérique qui compte de hello n’a pas signé dans à partir d’avant. 

**toosimulate une sign-in à partir d’un emplacement inconnu, effectuer hello suit**:

1. Choisissez un compte qui présente un historique de connexion d’au moins 14 jours. 
2. Effectuez ensuite l’une ou l’autre de ces étapes :
   
   a. Lorsque vous utilisez un réseau privé virtuel, accédez trop[https://myapps.microsoft.com](https://myapps.microsoft.com) et entrez hello les informations d’identification du compte hello toosimulate hello risque événement.
   
   b. Demandez à une association dans un toosign autre emplacement à l’aide des informations d’identification du compte hello (non recommandées).

Connectez-vous Hello apparaîtront sur le tableau de bord de Protection de l’identité hello dans les 5 minutes.

### <a name="impossible-travel-tooatypical-location"></a>Voyage Impossible tooatypical emplacement
Simulation de condition de voyage impossible hello est difficile, car l’algorithme de hello utilise tooweed d’apprentissage machine des faux positifs comme voyage impossible à partir d’appareils familiers ou connexions à partir de réseaux privés virtuels qui sont utilisés par d’autres utilisateurs dans le répertoire de hello. En outre, algorithme de hello requiert un historique de connexion de 3 jours too14 pour l’utilisateur de hello avant le début de la génération d’événements à risque.

**toosimulate un emplacement tooatypical voyage impossible, effectuer hello suit**:

1. À l’aide de votre navigateur standard, accédez trop[https://myapps.microsoft.com](https://myapps.microsoft.com).  
2. Entrez les informations d’identification de hello de hello compte toogenerate un événement risque de voyage impossible pour.
3. Changez votre agent utilisateur. Vous pouvez changer l’agent utilisateur depuis les outils de développement dans Internet Explorer ou à l’aide d’un module complémentaire de sélecteur d’agents utilisateur dans Firefox ou Chrome.
4. Changez votre adresse IP. Vous pouvez changer votre adresse IP en utilisant un VPN, un module complémentaire Tor ou en créant une nouvelle machine au sein d’Azure dans un autre centre de données.
5. Connectez-vous trop[https://myapps.microsoft.com](https://myapps.microsoft.com) à l’aide de hello les mêmes informations d’identification en tant qu’avant et après quelques minutes après la hello précédente connexion.

Connectez-vous Hello s’afficheront dans le tableau de bord de Protection de l’identité hello dans les 2 à 4 heures.<br>
En raison de hello complexes d’apprentissage des modèles impliqués, il existe un risque qu’il n'est pas collectée.<br> Vous pouvez vouloir tooreplicate ces étapes pour plusieurs comptes Azure AD.

## <a name="simulating-vulnerabilities"></a>Simulation de vulnérabilités
Les vulnérabilités sont des points faibles exploitables par une personne malveillante au sein de votre environnement Azure AD. Actuellement, Azure AD Identity Protection présente trois types de vulnérabilités tirant parti d’autres fonctionnalités d’Azure AD. Ces vulnérabilités seront affichera sur le tableau de bord de Protection de l’identité hello automatiquement une fois que ces fonctionnalités sont définies.

* Azure AD [Multi-Factor Authentication ?](../multi-factor-authentication/multi-factor-authentication.md)
* Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).
* Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="user-compromise-risk"></a>Risque de compromission de l’utilisateur
**tootest risque de compromission d’utilisateur, effectuer hello suit**:

1. Connectez-vous trop[https://portal.azure.com](https://portal.azure.com) avec les informations d’identification d’administrateur général pour votre client.
2. Accédez trop**Identity Protection**. 
3. Sur hello principal **Azure AD Identity Protection** panneau, cliquez sur **paramètres**. 
4. Sur hello **paramètres du portail** panneau, sous **les règles de sécurité**, cliquez sur **risque de compromission d’utilisateur**. 
5. Sur hello **connectez-vous risque** panneau, activez **activer règle** hors tension, puis cliquez sur **enregistrer** paramètres.
6. Pour un compte d’utilisateur donné, simulez un événement à risque lié à des emplacements non connus ou à une adresse IP anonyme. Cela sera élever le niveau de risque d’utilisateur hello pour cet utilisateur trop**support**.
7. Patientez quelques minutes et vérifiez que le niveau de risque de votre utilisateur est défini sur **Moyen**.
8. Accédez toohello **paramètres du portail** panneau.
9. Sur hello **risque de compromission d’utilisateur** panneau, sous **activer règle**, sélectionnez **sur** . 
10. Sélectionnez une des options suivantes de hello :
    
    a. tooblock, sélectionnez **support** sous **bloc connectez-vous**.
    
    b. modification de mot de passe sécurisé tooenforce, sélectionnez **support** sous **exiger l’authentification multifacteur**.
11. Cliquez sur **Enregistrer**.
12. Vous pouvez maintenant tester l’accès conditionnel en fonction des risques en vous connectant à l’aide d’un compte d’utilisateur présentant un niveau de risque élevé. Si vous affectez la valeur moyenne risque hello, selon la configuration de hello de votre stratégie, votre connexion est soit bloquée ou si vous devez toochange votre mot de passe. 
    <br><br>
    ![Manuel de](./media/active-directory-identityprotection-playbook/201.png "manuel")
    <br>

## <a name="sign-in-risk"></a>Risque à la connexion
**tootest un signe de risque, procédez hello comme suit :**

1. Connectez-vous trop[https://portal.azure.com ](https://portal.azure.com) avec les informations d’identification d’administrateur général pour votre client.
2. Accédez trop**Identity Protection**.
3. Sur hello principal **Azure AD Identity Protection** panneau, cliquez sur **paramètres**. 
4. Sur hello **paramètres du portail** panneau, sous **les règles de sécurité**, cliquez sur **connectez-vous risque**.
5. Sur hello ** risque de se connecter ** panneau, sélectionnez **sur** sous **activer règle**. 
6. Sélectionnez une des options suivantes de hello :
   
   a. tooblock, sélectionnez **support** sous **bloc se connecter**
   
   b. modification de mot de passe sécurisé tooenforce, sélectionnez **support** sous **exiger l’authentification multifacteur**.
7. tooblock, sélectionnez moyenne sous le bloc de vous connecter.
8. l’authentification multifacteur tooenforce, sélectionnez **support** sous **exiger l’authentification multifacteur**.
9. Cliquez sur **Save**(Enregistrer).
10. Vous pouvez maintenant tester l’accès conditionnel en fonction du risque en simulant des emplacements inhabituels hello ou adresse IP anonyme risque événements car ils sont tous deux **support** risque d’événements.


![Manuel](./media/active-directory-identityprotection-playbook/200.png "Manuel")


## <a name="see-also"></a>Voir aussi
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

