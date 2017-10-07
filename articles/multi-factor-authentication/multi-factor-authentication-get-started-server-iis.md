---
title: "aaaIIS l’authentification et le serveur Azure MFA | Documents Microsoft"
description: "Il s’agit de page d’authentification multifacteur Azure hello qui va vous aider à déployer l’authentification IIS et le serveur Azure multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d1bf1c8a-2c10-4ae6-9f4b-75f0c3df43eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017,it-pro
ms.openlocfilehash: 74bd39c2644e2bca0880baea3824cad4c9215111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-iis-web-apps"></a>Configuration d’un serveur Azure Multi-Factor Authentication pour les applications web IIS

Utiliser la section authentification IIS de hello de hello serveur Azure multi-Factor Authentication (MFA) tooenable et configurer l’authentification IIS pour l’intégration avec les applications web Microsoft IIS. Hello serveur Azure MFA installe un plug-in qui peut filtrer les demandes effectuées toohello IIS web server tooadd Azure multi-Factor Authentication. Hello plug-in IIS prend en charge l’authentification par formulaire et l’authentification Windows HTTP intégrée. Adresses IP peuvent également être configuré tooexempt les adresses IP internes à partir de l’authentification à deux facteurs de confiance.

![Authentification IIS](./media/multi-factor-authentication-get-started-server-iis/iis.png)

## <a name="using-form-based-iis-authentication-with-azure-multi-factor-authentication-server"></a>Utilisation de l'authentification IIS basée sur le formulaire avec le serveur Azure Multi-Factor Authentication
toosecure un IIS application qui utilise l’authentification basée sur le formulaire web, installez hello serveur Azure multi-Factor Authentication sur le serveur web hello IIS et configurer hello serveur par hello procédure :

1. Bonjour serveur Azure multi-Factor Authentication, cliquez sur l’icône de l’authentification IIS hello dans le menu de gauche hello.
2. Cliquez sur hello **basée sur formulaire** onglet.
3. Cliquez sur **Add**.
4. variables de nom d’utilisateur, mot de passe et domaine toodetect automatiquement, entrez hello URL de connexion (par exemple, https://localhost/contoso/auth/login.aspx) dans la boîte de dialogue hello du site Web basé sur des formulaires et cliquez sur **OK**.
5. Vérifiez hello **une correspondance d’utilisateur exiger une authentification multifacteur** zone si tous les utilisateurs ont été ou seront importés dans hello serveur et authentification toomulti-facteur de sujet. Si un nombre important d’utilisateurs n’ont pas encore été importé dans hello serveur et/ou est exempté de l’authentification multifacteur, laissez la zone de hello désactivée.
6. Si les variables de page hello ne peut pas être détectées automatiquement, cliquez sur **spécifier manuellement** dans la boîte de dialogue hello du site Web basé sur des formulaires.
7. Dans la boîte de dialogue Ajouter un site Web hello, entrez la page de connexion toohello hello URL dans le champ URL de soumission de hello et entrez un nom d’Application (facultatif). nom de l’Application Hello apparaît dans les rapports d’Azure multi-Factor Authentication et peut être affichée dans les messages d’authentification SMS ou application Mobile.
8. Sélectionnez le format de demande correct hello. Ce paramètre est défini trop**POST ou GET** pour la plupart des applications web.
9. Entrez la variable de nom d’utilisateur hello, variable de mot de passe et domaine (si elle apparaît sur la page de connexion hello). noms de hello toofind Hello d’entrée de zones, naviguez toohello page de connexion dans un navigateur web, avec le bouton droit sur la page de hello et sélectionnez **afficher la Source**.
10. Vérifiez hello **une correspondance d’utilisateur exiger une authentification multifacteur Azure** zone si tous les utilisateurs ont été ou seront importés dans hello serveur et authentification toomulti-facteur de sujet. Si un nombre important d’utilisateurs n’ont pas encore été importé dans hello serveur et/ou est exempté de l’authentification multifacteur, laissez la zone de hello désactivée.
11. Cliquez sur **avancé** tooreview les paramètres avancé, y compris :

  - Sélectionner un fichier de page de refus personnalisé
  - Cache les authentifications réussies toohello site Web pour une période de temps à l’aide de cookies
  - Déterminez si les informations d’identification tooauthenticate hello principal par rapport à un domaine Windows, annuaire LDAP. ou sur un serveur RADIUS.

12. Cliquez sur **OK** boîte de dialogue Ajouter un site Web tooreturn toohello.
13. Cliquez sur **OK**.
14. Une fois hello URL et les variables de page ont été détectés ou entrés, affichent les données du site Web de hello Bonjour basée sur formulaire le panneau de configuration.

## <a name="using-integrated-windows-authentication-with-azure-multi-factor-authentication-server"></a>Utilisation de l'authentification Windows intégrée avec le serveur Azure Multi-Factor Authentication
toosecure un IIS web application qui utilise l’authentification Windows HTTP intégrée, installez hello serveur Azure MFA sur le serveur web hello IIS, puis configurez hello serveur avec hello comme suit :

1. Bonjour serveur Azure multi-Factor Authentication, cliquez sur l’icône de l’authentification IIS hello dans le menu de gauche hello.
2. Cliquez sur hello **HTTP** onglet.
3. Cliquez sur **Add**.
4. Dans la boîte de dialogue Ajouter une URL de Base hello, entrez hello URL pour le site Web de hello où l’authentification HTTP est effectuée (par exemple, http://localhost/owa) et fournir un nom d’Application (facultatif). nom de l’Application Hello apparaît dans les rapports d’Azure multi-Factor Authentication et peut être affichée dans les messages d’authentification SMS ou application Mobile.
5. Ajuster délai d’inactivité de hello et au Maximum les heures de session si la valeur par défaut de hello n’est pas suffisant.
6. Vérifiez hello **une correspondance d’utilisateur exiger une authentification multifacteur** zone si tous les utilisateurs ont été ou seront importés dans hello serveur et authentification toomulti-facteur de sujet. Si un nombre important d’utilisateurs n’ont pas encore été importé dans hello serveur et/ou est exempté de l’authentification multifacteur, laissez la zone de hello désactivée.
7. Vérifiez hello **cache de Cookie** zone Si vous le souhaitez.
8. Cliquez sur **OK**.

## <a name="enable-iis-plug-ins-for-azure-multi-factor-authentication-server"></a>Activation des plug-ins IIS pour le serveur Azure Multi-Factor Authentication
Après avoir configuré hello basée sur formulaire ou de l’URL d’authentification HTTP et paramètres, sélectionnez hello emplacements où hello plug-ins IIS de l’authentification multifacteur Azure doit être chargé et activé dans IIS. Utilisez hello procédure :

1. Si vous exécutez IIS 6, cliquez sur hello **ISAPI** onglet. Site Web Sélectionnez hello hello d’application web est en cours d’exécution sous (par exemple, Site Web par défaut) tooenable hello ISAPI Azure multi-Factor Authentication filtre plug-in pour ce site.
2. Si vous exécutez IIS 7 ou version ultérieure, cliquez sur hello **Module natif** onglet. Sélectionnez hello serveur, sites Web ou applications tooenable hello plug-in IIS niveaux hello souhaité.
3. Cliquez sur hello **l’authentification d’activer IIS** zone haut hello écran hello. Azure multi-Factor Authentication sécurise désormais hello sélectionné IIS application. Assurez-vous que les utilisateurs ont été importés dans hello serveur.

## <a name="trusted-ips"></a>Adresses IP approuvées
Hello adresses IP approuvées permettent toobypass utilisateurs multi-Factor Authentication pour les demandes de site Web provenant d’adresses IP ou des sous-réseaux spécifiques. Par exemple, vous souhaiterez tooexempt des utilisateurs à partir de l’authentification multifacteur Azure pendant la connexion à partir d’office de hello. Pour ce faire, vous spécifiez hello office sous-réseau en tant qu’une adresse IP approuvée. tooconfigure d’adresses IP de confiance, utilisez hello procédure :

1. Dans la section authentification IIS de hello, cliquez sur hello **des adresses IP approuvées** onglet.
2. Cliquez sur **Add**.
3. Lors de la boîte de dialogue Ajouter des adresses IP approuvées hello s’affiche, sélectionnez hello **adresse IP unique**, **plage d’adresses IP**, ou **sous-réseau** case d’option.
4. Entrez l’adresse IP de hello, plage d’adresses IP ou sous-réseau qui doit être dans la liste approuvée. Si entrer un sous-réseau, un select hello approprié de masque de réseau et cliquez sur **OK**. liste blanche d’adresses Hello a maintenant été ajouté.
