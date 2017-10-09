---
title: "aaaLDAP l’authentification et le serveur Azure MFA | Documents Microsoft"
description: "Il s’agit de page d’authentification multifacteur Azure hello qui va vous aider à déployer l’authentification LDAP et le serveur Azure multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: e1a68568-53d1-4365-9e41-50925ad00869
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 17a26b57dbf6afa2fcfdb3d19c5b5ba2987a9f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ldap-authentication-and-azure-multi-factor-authentication-server"></a>Authentification LDAP et serveur Azure Multi-Factor Authentication
Par défaut, hello serveur Azure multi-Factor Authentication est configuré tooimport ou synchroniser des utilisateurs à partir d’Active Directory. Toutefois, il peut être configuré toobind toodifferent LDAP répertoires, tel qu’un annuaire ADAM ou un contrôleur de domaine Active Directory spécifique. Lorsque tooa connecté l’annuaire via LDAP, hello serveur Azure multi-Factor Authentication peut agir comme un authentifications tooperform de proxy LDAP. Il permet également de hello utiliser une liaison LDAP comme RADIUS cible, pour la pré-authentification des utilisateurs avec l’authentification IIS, ou pour l’authentification principale dans le portail de l’utilisateur l’authentification Multifacteur Azure hello.

toouse Azure multi-Factor Authentication comme un proxy LDAP, insérez hello serveur Azure multi-Factor Authentication entre un client LDAP hello (par exemple, équipement VPN, application) et le serveur d’annuaire LDAP hello. Hello serveur Azure multi-Factor Authentication doit être configuré toocommunicate avec les serveurs client hello et service d’annuaire LDAP hello. Dans cette configuration, hello serveur Azure multi-Factor Authentication accepte les demandes LDAP des serveurs clients et les applications et les transmet toohello cible LDAP Active server toovalidate hello informations d’identification principales. Si le service d’annuaire LDAP hello valide les informations d’identification principales hello, Azure multi-Factor Authentication effectue une vérification d’identité deuxième et envoie une réponse au client LDAP toohello précédent. l’authentification de la totalité de Hello réussit uniquement si l’authentification de serveur hello LDAP et vérification d’étape de la seconde hello réussissent.

## <a name="configure-ldap-authentication"></a>Configurer l’authentification LDAP
authentification LDAP tooconfigure, installation hello serveur Azure multi-Factor Authentication sur un serveur Windows. Utilisez hello procédure :

### <a name="add-an-ldap-client"></a>Ajouter un client LDAP

1. Bonjour serveur Azure multi-Factor Authentication, sélectionnez l’icône de l’authentification LDAP de hello dans le menu de gauche hello.
2. Vérifiez hello **activer l’authentification LDAP** case à cocher.

   ![Authentification LDAP](./media/multi-factor-authentication-get-started-server-ldap/ldap2.png)

3. Sous l’onglet de Clients hello, modifiez le port TCP hello et le port SSL si hello service Azure multi-Factor d’authentification LDAP doit lier toolisten ports toonon-standard pour les demandes LDAP.
4. Si vous envisagez toouse LDAPS de hello client toohello serveur Azure multi-Factor Authentication, un certificat SSL doit être installé sur hello même serveur en tant que serveur d’authentification Multifacteur. Cliquez sur **Parcourir** suivant toohello SSL cases de certificats et sélectionnez un toouse de certificat pour une connexion sécurisée hello.
5. Cliquez sur **Add**.
6. Dans la boîte de dialogue Ajouter un Client LDAP hello, entrez hello adresse IP du dispositif de hello, serveur ou application qui authentifie toohello serveur et un nom d’Application (facultatif). nom de l’Application Hello apparaît dans les rapports d’Azure multi-Factor Authentication et peut être affichée dans les messages d’authentification SMS ou application Mobile.
7. Vérifiez hello **une correspondance d’utilisateur exiger une authentification multifacteur Azure** zone si tous les utilisateurs ont été ou seront importés dans hello serveur et de vérification tootwo-étape de sujet. Si un nombre important d’utilisateurs n’ont pas encore été importé dans hello serveur et/ou est exempts de la vérification en deux étapes, laissez la zone de hello désactivée. Consultez le fichier d’aide de l’authentification Multifacteur serveur hello pour plus d’informations sur cette fonctionnalité.

Répétez ces étapes tooadd autres clients LDAP.

### <a name="configure-hello-ldap-directory-connection"></a>Configurer la connexion à l’annuaire LDAP hello

Lorsque hello Azure multi-Factor Authentication est configuré tooreceive les authentifications LDAP, il doit proxy ces toohello d’annuaire LDAP authentifications. Par conséquent, onglet de la cible de hello affiche uniquement une seule grisée option toouse une cible LDAP.

1. tooconfigure hello connexion à l’annuaire LDAP, cliquez sur hello **intégration d’annuaire** icône.
2. Sur l’onglet Paramètres de hello, sélectionnez hello **utiliser la configuration LDAP spécifique** case d’option.
3. Sélectionnez **Modifier…**.
4. Dans la boîte de dialogue Modifier la Configuration LDAP hello, remplissez les champs de hello avec hello informations requises tooconnect toohello d’annuaire LDAP. Descriptions des champs de hello sont incluses dans le fichier d’aide hello serveur Azure multi-Factor Authentication.

    ![Intégration de répertoires](./media/multi-factor-authentication-get-started-server-ldap/ldap.png)

5. Test de connexion LDAP hello en cliquant sur hello **Test** bouton.
6. Si un test de connexion LDAP hello a réussi, cliquez sur hello **OK** bouton.
7. Cliquez sur hello **filtres** hello de l’onglet serveur est préconfiguré tooload conteneurs, groupes de sécurité et les utilisateurs à partir d’Active Directory. Si une liaison autre annuaire LDAP de tooa, vous devez probablement les filtres de hello tooedit affichés. Cliquez sur hello **aide** lien pour plus d’informations sur les filtres.
8. Cliquez sur hello **attributs** hello de l’onglet serveur est préconfiguré toomap des attributs à partir d’Active Directory.
9. Si vous effectuez une liaison tooa autre répertoire ou toochange hello préconfiguré mappages d’attributs LDAP, cliquez sur **modifier...**
10. Dans la boîte de dialogue Modifier les attributs hello, modifier les mappages d’attributs LDAP hello pour votre annuaire. Noms d’attribut peuvent être tapés ou sélectionnés en cliquant sur hello **...** champ de tooeach bouton suivant. Cliquez sur hello **aide** lien pour plus d’informations sur les attributs.
11. Cliquez sur hello **OK** bouton.
12. Cliquez sur hello **paramètres de la société** icône et sélectionnez hello **résolution de nom d’utilisateur** onglet.
13. Si vous vous connectez tooActive active à partir d’un serveur appartenant à un domaine, laissez hello **identificateurs de sécurité (SID) Windows de l’utilisation pour la correspondance des noms d’utilisateur** case d’option sélectionnée. Sinon, sélectionnez hello **attribut d’identificateur unique LDAP d’utilisation pour la correspondance des noms d’utilisateur** case d’option. 

Hello lorsque **attribut d’identificateur unique LDAP d’utilisation pour la correspondance des noms d’utilisateur** case d’option est sélectionnée, hello serveur Azure multi-Factor Authentication tente tooresolve chaque identificateur tooa de nom d’utilisateur dans l’annuaire LDAP de hello. Une recherche LDAP est effectuée sur le nom d’utilisateur de hello attributs définis dans hello intégration d’annuaire -> onglet attributs. Lorsqu’un utilisateur s’authentifie, nom d’utilisateur hello est résolu toohello d’identificateur unique dans l’annuaire LDAP de hello. Identificateur unique de Hello est utilisé pour l’utilisateur hello correspondant dans le fichier de données de l’authentification multifacteur Azure hello. Cela permet des comparaisons sans prise en compte de la casse et autorise les noms d’utilisateur longs et courts.

Après avoir effectué ces étapes, hello serveur MFA écoute les ports hello configuré pour les demandes d’accès LDAP de hello configuré les clients et agit comme un proxy pour les demandes d’annuaire LDAP de toohello pour l’authentification.

## <a name="configure-ldap-client"></a>Configurer un client LDAP
tooconfigure hello client LDAP, suivez les indications de hello :

* Configurez votre équipement, serveur ou tooauthenticate application via LDAP toohello serveur Azure multi-Factor Authentication comme s’il s’agissait de votre annuaire LDAP. Utilisez hello mêmes paramètres que vous utiliseriez normalement tooconnect directement tooyour annuaire LDAP, à l’exception du nom du serveur hello ou l’adresse IP, ce qui doit être celui de hello serveur Azure multi-Factor Authentication.
* Configurer hello LDAP délai too30-60 (secondes) afin qu’il soit temps toovalidate hello de l’utilisateur avec le service d’annuaire LDAP hello, effectuer une vérification à l’étape de la seconde hello, réception de la réponse et répondre de demande d’accès LDAP toohello.
* Si vous utilisez le protocole LDAPS, hello équipement ou le serveur qui effectue des requêtes LDAP hello doit approuver hello certificat SSL installé sur le serveur Azure multi-Factor Authentication de hello.

