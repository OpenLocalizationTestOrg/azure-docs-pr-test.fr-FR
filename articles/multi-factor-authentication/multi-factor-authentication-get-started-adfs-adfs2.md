---
title: aaaUse serveur Azure MFA avec AD FS 2.0 | Documents Microsoft
description: "Il s’agit de page d’authentification multifacteur Azure hello qui décrit comment tooget main d’Azure MFA et AD FS 2.0."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 96168849-241a-4499-a224-d829913caa7e
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 15011a94ca69dc6e51aa3edf74f5db6cd44d697a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-20"></a>Configurer le serveur Azure multi-Factor Authentication toowork avec AD FS 2.0
Cet article est pour les organisations qui sont fédérées avec Azure Active Directory et toosecure des ressources qui sont locales ou dans le cloud de hello. Protection de vos ressources, à l’aide de hello serveur Azure multi-Factor Authentication et configurez-le toowork avec AD FS afin que la vérification en deux étapes est déclenchée pour les points de terminaison de valeur élevée.

Cette documentation décrit l’utilisation de hello serveur Azure multi-Factor Authentication avec AD FS 2.0. Pour obtenir des informations sur AD FS, consultez [Sécurisez vos ressources cloud et locales à l’aide du serveur Azure Multi-Factor Authentication avec AD FS dans Windows Server 2012 R2](multi-factor-authentication-get-started-adfs-w2k12.md).

## <a name="secure-ad-fs-20-with-a-proxy"></a>Sécurisation d’AD FS 2.0 avec un proxy
toosecure AD FS 2.0 avec un proxy, installez hello serveur Azure multi-Factor Authentication sur le serveur de proxy hello AD FS.

### <a name="configure-iis-authentication"></a>Configuration de l’authentification IIS
1. Bonjour serveur Azure multi-Factor Authentication, cliquez sur hello **l’authentification IIS** icône dans le menu de gauche hello.
2. Cliquez sur hello **basée sur formulaire** onglet.
3. Cliquez sur **Add**.

   <center>![Configuration](./media/multi-factor-authentication-get-started-adfs-adfs2/setup1.png)</center>

4. variables de nom d’utilisateur, mot de passe et domaine toodetect automatiquement, entrez les URL de connexion hello (par exemple, https://sso.contoso.com/adfs/ls) dans la boîte de dialogue hello du site Web basé sur des formulaires et cliquez sur **OK**.
5. Vérifiez hello **une correspondance d’utilisateur exiger une authentification multifacteur Azure** zone si tous les utilisateurs ont été ou seront importés dans hello serveur et de vérification tootwo-étape de sujet. Si un nombre important d’utilisateurs n’ont pas encore été importé dans hello serveur et/ou est exempté de la vérification en deux étapes, laissez la zone de hello désactivée.
6. Si les variables de page hello ne peut pas être détectées automatiquement, cliquez sur hello **spécifier manuellement...** bouton dans la boîte de dialogue hello du site Web basé sur des formulaires.
7. Dans la boîte de dialogue Ajouter un site Web hello, entrez la page de connexion hello URL toohello AD FS dans le champ URL de soumission de hello (par exemple, https://sso.contoso.com/adfs/ls) et entrez un nom d’Application (facultatif). nom de l’Application Hello apparaît dans les rapports d’Azure multi-Factor Authentication et peut être affichée dans les messages d’authentification SMS ou application Mobile.
8. Définir le format de la demande hello trop**POST ou GET**.
9. Entrez une variable de nom d’utilisateur hello (ctl00$ ContentPlaceHolder1$ UsernameTextBox) et un mot de passe (ctl00$ ContentPlaceHolder1$ PasswordTextBox). Si votre page de connexion basée sur formulaire affiche une zone de texte domaine, entrez la variable de domaine hello également. noms de hello toofind des zones d’entrée de hello sur la page de connexion hello, page de connexion toohello accédez dans un navigateur web, avec le bouton droit sur la page de hello et sélectionnez **afficher la Source**.
10. Vérifiez hello **une correspondance d’utilisateur exiger une authentification multifacteur Azure** zone si tous les utilisateurs ont été ou seront importés dans hello serveur et de vérification tootwo-étape de sujet. Si un nombre important d’utilisateurs n’ont pas encore été importé dans hello serveur et/ou est exempté de la vérification en deux étapes, laissez la zone de hello désactivée.
    <center>![Configuration](./media/multi-factor-authentication-get-started-adfs-adfs2/manual.png)</center>
11. Cliquez sur **Avancé...** tooreview paramètres avancé. Vous pouvez notamment :

    - Sélectionner un fichier de page de refus personnalisé
    - Site Web toohello cache les authentifications réussies à l’aide de cookies
    - Sélectionnez comment tooauthenticate hello les informations d’identification principales

12. Étant donné que le serveur de proxy hello AD FS n’est pas susceptible toobe joints à un domaine de toohello, vous pouvez utiliser le contrôleur de domaine LDAP tooconnect tooyour pour l’authentification préalable et l’importation de l’utilisateur. Dans la boîte de dialogue hello basé sur site, cliquez sur hello **l’authentification principale** onglet et sélectionnez **de la liaison LDAP** pour hello type d’authentification de l’authentification préalable.
13. Lorsque vous avez terminé, cliquez sur **OK** boîte de dialogue Ajouter un site Web tooreturn toohello.
14. Cliquez sur **OK** boîte de dialogue tooclose hello.
15. Une fois hello URL et les variables de page ont été détectés ou entrés, affichent les données du site Web de hello Bonjour basée sur formulaire le panneau de configuration.
16. Cliquez sur hello **Module natif** onglet et sélectionnez hello serveur du site Web hello proxy de hello AD FS est en cours d’exécution sous (comme « Site Web par défaut »), ou hello AD FS proxy application (par exemple, « ls » sous « adfs ») tooenable hello plug-in à hello IIS niveau souhaité.
17. Cliquez sur hello **l’authentification d’activer IIS** zone haut hello écran hello.

l’authentification IIS Hello est maintenant activée.

### <a name="configure-directory-integration"></a>Configuration de l’intégration d’annuaire
Vous avez activé l’authentification IIS, mais tooperform hello pré-authentification tooyour Active Directory (AD) via LDAP, vous devez configurer hello contrôleur de domaine de toohello de connexion LDAP.

1. Cliquez sur hello **intégration d’annuaire** icône.
2. Sur l’onglet Paramètres de hello, sélectionnez hello **utiliser la configuration LDAP spécifique** case d’option.

   <center>![Configuration](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap1.png)</center>

3. Cliquez sur **Modifier**.
4. Dans la boîte de dialogue Modifier la Configuration LDAP hello, remplissez les champs de hello avec le contrôleur de domaine toohello AD hello informations tooconnect requis. Descriptions des champs de hello sont incluses dans le fichier d’aide hello serveur Azure multi-Factor Authentication.
5. Test de connexion LDAP hello en cliquant sur hello **Test** bouton.

   <center>![Configuration](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap2.png)</center>

6. Si le test de connexion LDAP hello a réussi, cliquez sur **OK**.

### <a name="configure-company-settings"></a>Configuration des paramètres de la société
1. Ensuite, cliquez sur hello **paramètres de la société** icône et sélectionnez hello **résolution de nom d’utilisateur** onglet.
2. Sélectionnez hello **attribut d’identificateur unique LDAP d’utilisation pour la correspondance des noms d’utilisateur** case d’option.
3. Si les utilisateurs entrent leur nom d’utilisateur au format « DOMAINE\nom_utilisateur », hello Server a besoin de domaine de hello toobe toostrip en mesure de désactiver le nom d’utilisateur hello lorsqu’il crée la requête LDAP de hello. Ceci peut être effectué via un paramètre du registre.
4. Ouvrez l’Éditeur du Registre hello et accédez tooHKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Positive réseaux/PhoneFactor sur un serveur 64 bits. Si vous utilisez un serveur 32 bits, prendre hello « Wow6432Node » en dehors du chemin d’accès hello. Créer une valeur DWORD appelée « UsernameCxz_stripPrefixDomain » de clé de Registre et définir hello valeur too1. Azure multi-Factor Authentication sécurise désormais les proxy hello AD FS.

Assurez-vous que les utilisateurs ont été importés à partir d’Active Directory dans hello serveur. Consultez hello [section d’adresses IP approuvées](#trusted-ips) si vous souhaitez que toowhitelist les adresses IP internes afin que la vérification en deux étapes n’est pas requise pour se connecter à un site Web de toohello à partir de ces emplacements.

<center>![Configuration](./media/multi-factor-authentication-get-started-adfs-adfs2/reg.png)</center>

## <a name="ad-fs-20-direct-without-a-proxy"></a>AD FS 2.0 Direct sans proxy
Vous pouvez sécuriser ADFS lorsque le proxy de hello AD FS n’est pas utilisé. Installer hello serveur Azure multi-Factor Authentication sur le serveur de hello AD FS et configurer hello serveur par hello suivant les étapes :

1. Au sein de hello serveur Azure multi-Factor Authentication, cliquez sur hello **l’authentification IIS** icône dans le menu de gauche hello.
2. Cliquez sur hello **HTTP** onglet.
3. Cliquez sur **Add**.
4. Dans la boîte de dialogue Ajouter une URL de Base hello, entrez les URL de hello hello du site Web AD FS sur lequel l’authentification HTTP est exécutée (par exemple, https://sso.domain.com/adfs/ls/auth/integrated) dans le champ URL de Base de hello. Ensuite, entrez un nom d’application (facultatif). nom de l’Application Hello apparaît dans les rapports d’Azure multi-Factor Authentication et peut être affichée dans les messages d’authentification SMS ou application Mobile.
5. Si vous le souhaitez, ajustez le délai d’inactivité de hello et au Maximum les heures de session.
6. Vérifiez hello **une correspondance d’utilisateur exiger une authentification multifacteur Azure** zone si tous les utilisateurs ont été ou seront importés dans hello serveur et de vérification tootwo-étape de sujet. Si un nombre important d’utilisateurs n’ont pas encore été importé dans hello serveur et/ou est exempté de la vérification en deux étapes, laissez la zone de hello désactivée.
7. La case hello cookie du cache si vous le souhaitez.

   <center>![Configuration](./media/multi-factor-authentication-get-started-adfs-adfs2/noproxy.png)</center>

8. Cliquez sur **OK**.
9. Cliquez sur hello **Module natif** onglet et sélectionnez hello serveur, hello site Web (comme « Site Web par défaut ») ou tooenable hello plug-in à hello IIS de hello AD FS application (par exemple, « ls » sous « adfs ») de niveau souhaité.
10. Cliquez sur hello **l’authentification d’activer IIS** zone haut hello écran hello.

Le proxy AD FS est désormais protégé par le serveur Azure Multi-Factor Authentication.

Assurez-vous que les utilisateurs ont été importés à partir d’Active Directory dans hello serveur. Consultez hello des adresses IP approuvées section si vous souhaitez que les IP interne toowhitelist adresses afin que la vérification en deux étapes n’est pas requise pour se connecter à un site Web de toohello à partir de ces emplacements.

## <a name="trusted-ips"></a>Adresses IP approuvées
Adresses IP approuvées permettent aux utilisateurs toobypass Azure multi-Factor Authentication pour les demandes de site Web provenant d’adresses IP ou des sous-réseaux spécifiques. Par exemple, vous souhaiterez tooexempt des utilisateurs à partir de la vérification en deux étapes lorsqu’ils se connectent à partir d’office de hello. Pour ce faire, vous spécifiez hello office sous-réseau en tant qu’une adresse IP approuvée.

### <a name="tooconfigure-trusted-ips"></a>tooconfigure d’adresses IP approuvées
1. Dans la section authentification IIS de hello, cliquez sur hello **des adresses IP approuvées** onglet.
2. Cliquez sur hello **ajouter...** .
3. Lors de la boîte de dialogue Ajouter des adresses IP approuvées hello s’affiche, sélectionnez une des hello **adresse IP unique**, **plage d’adresses IP**, ou **sous-réseau** cases d’option.
4. Entrez l’adresse IP de hello, plage d’adresses IP ou sous-réseau qui doit être dans la liste approuvée. Si vous entrez un sous-réseau, sélectionnez hello hello approprié de masque de réseau et cliquez sur **OK** bouton. Hello approuvé QU'IP a été ajouté.

<center>![Configuration](./media/multi-factor-authentication-get-started-adfs-adfs2/trusted.png)</center>
