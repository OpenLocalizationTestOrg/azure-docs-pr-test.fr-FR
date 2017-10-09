---
title: "intégration de la passerelle de bureau avec l’extension d’Azure MFA NPS d’aaaRemote | Documents Microsoft"
description: "Cet article décrit l’intégration de votre infrastructure de passerelle Bureau à distance avec l’authentification Multifacteur Azure à l’aide d’extension du serveur NPS (Network Policy Server) hello pour Microsoft Azure."
services: active-directory
keywords: "Azure MFA, intégration de la passerelle des services Bureau à distance, Azure Active Directory, extension de serveur NPS"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: ae5f6864416582bd82b787005ca787988d23a813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#  <a name="integrate-your-remote-desktop-gateway-infrastructure-using-hello-network-policy-server-nps-extension-and-azure-ad"></a>Intégrer votre infrastructure de passerelle Bureau à distance à l’aide d’extension du serveur NPS (Network Policy Server) hello et Azure AD

Cet article fournit des détails pour l’intégration de votre infrastructure de passerelle Bureau à distance avec Azure multi-Factor Authentication (MFA) à l’aide d’extension du serveur NPS (Network Policy Server) hello pour Microsoft Azure. 

Hello extension du Service NPS (Network Policy Server) pour Azure permet de clients toosafeguard Authentication Dial-In Service RADIUS (Remote User) l’authentification du client à l’aide d’Azure's nuage [l’authentification multifacteur (MFA)](multi-factor-authentication.md). Cette solution fournit la vérification en deux étapes pour ajouter une deuxième couche de sécurité toouser connexions et transactions.

Cet article fournit des instructions détaillées pour l’intégration de l’infrastructure de serveur NPS hello avec l’authentification Multifacteur Azure à l’aide d’extension NPS hello pour Azure. Cela permet une vérification sécurisée pour les utilisateurs qui tentent de toolog sur tooa passerelle Bureau à distance. 

Hello stratégie réseau et les Services d’accès (NPS) permet aux entreprises de hello suivant de capacité toodo hello :
* Définir des emplacements centraux pour la gestion de hello et contrôle des demandes du réseau en spécifiant qui peut se connecter, les heures de la journée, les connexions sont autorisées, hello durée des connexions et le niveau de hello de sécurité que les clients doivent utiliser tooconnect et ainsi de suite. Plutôt que de spécifier ces stratégies sur chaque serveur VPN ou de passerelle des services Bureau à distance (RD), ces stratégies peuvent être spécifiées une seule fois dans un emplacement central. Hello protocole RADIUS fournit hello centralisée de l’authentification, l’autorisation et gestion des comptes (AAA). 
* Établir et appliquer les stratégies de contrôle d’intégrité de client de Protection d’accès réseau (NAP) qui détermine si les appareils sont autorisées sans restriction ou à accès restreint toonetwork ressources.
* Fournir un moyen tooenforce authentification et l’autorisation pour les commutateurs Ethernet et des points d’accès sans fil compatibles too802.1x accès.    

En règle générale, les organisations utiliser NPS (RADIUS) toosimplify et centraliser la gestion de hello du VPN des stratégies. Toutefois, de nombreuses organisations également NPS toosimplify et centraliser la gestion de hello de stratégies d’autorisation de connexion de bureau Bureau à distance (bureau à distance). 

Les organisations peuvent également intégrer NPS Azure MFA tooenhance sécurité et fournir un niveau élevé de compatibilité. Cela permet de s’assurer que les utilisateurs établir toolog de vérification en deux étapes sur toohello passerelle Bureau à distance. Pour toobe les utilisateurs autorisé à accéder, ils doivent fournir leur combinaison nom d’utilisateur/mot de passe avec les informations utilisateur de hello a dans leur contrôle. Ces informations doivent être approuvées et pas facilement dupliquées, comme un numéro de téléphone portable, numéro de téléphone fixe, une application sur un appareil mobile et autres.

Disponibilité toohello préalable de hello extension NPS pour Azure, les clients qui souhaitaient vérification en deux étapes tooimplement intégré NPS Azure MFA des environnements et avaient tooconfigure et mettre à jour un serveur distinct de l’authentification Multifacteur dans l’environnement local de hello en tant que documentées dans [passerelle Bureau à distance et le serveur Azure multi-Factor Authentication utilisant RADIUS](multi-factor-authentication-get-started-server-rdg.md).

disponibilité Hello d’extension NPS hello pour Azure offre désormais des organisations hello choix toodeploy une solution d’authentification Multifacteur local ou une nuage MFA solution toosecure RADIUS l’authentification du client.

## <a name="authentication-flow"></a>Flux d’authentification

Pour les utilisateurs toobe accordées à accéder aux ressources de toonetwork via une passerelle Bureau à distance, qu'ils doivent remplir les conditions de hello spécifiées dans une stratégie d’autorisation de connexion Bureau à distance (services Bureau à distance) et une stratégie d’autorisation de ressource Bureau à distance (RD RAP). Bureau à distance spécifier qui est autorisé tooconnect tooRD passerelles. Bureau à distance d spécifier les ressources réseau hello, tels que les ordinateurs de bureau à distance ou des applications à distance, que l’utilisateur hello est autorisé tooconnect toothrough hello passerelle Bureau à distance. 

Une passerelle Bureau à distance peut être configuré toouse un magasin de stratégies centrale pour le Bureau à distance. Stratégies de bureau à distance ne peut pas utiliser une stratégie centrale, car elles sont traitées sur hello passerelle Bureau à distance. Un exemple d’un toouse de passerelle Bureau à distance configuré un magasin de stratégies centrale pour le Bureau à distance est un serveur NPS tooanother client RADIUS qui sert de magasin de stratégie centralisée hello.

Lorsque hello extension NPS pour Azure est intégré à hello NPS et de passerelle Bureau à distance, les flux d’authentification réussie hello est la suivante :

1. serveur de passerelle Bureau à distance Hello reçoit une demande d’authentification à partir d’une ressource de tooa tooconnect utilisateur du Bureau à distance, par exemple une session Bureau à distance. Agissant comme un client RADIUS, serveur de passerelle Bureau à distance hello convertit le message de demande d’accès RADIUS tooa hello demande et envoie hello message toohello RADIUS NPS (server) sur lequel l’extension de serveur NPS hello est installée. 
2. Hello nom d’utilisateur et mot de passe est vérifiée dans Active Directory et hello utilisateur est authentifié.
3. Si tous les hello conditions comme spécifié dans hello de demande de connexion de serveur NPS et stratégies de réseau hello sont remplies (par exemple, l’heure du jour ou de groupe de restrictions d’appartenance), hello extension NPS déclenche une demande d’authentification secondaire avec l’authentification Multifacteur Azure. 
4. L’authentification Multifacteur Azure communique avec Azure AD, récupère les détails de l’utilisateur hello et effectue l’authentification secondaire hello à l’aide de la méthode hello configuré par l’utilisateur hello (message texte, application mobile et ainsi de suite). 
5. En cas de réussite de stimulation d’authentification Multifacteur de hello, Azure MFA communique extension NPS toohello hello résultat.
6. Hello serveur NPS où hello extension est installé envoie un message d’acceptation d’accès RADIUS pour le serveur de passerelle Bureau à distance toohello hello services Bureau à distance stratégie.
7. Hello utilisateur a accès toohello a demandé la ressource réseau via hello passerelle Bureau à distance.

## <a name="prerequisites"></a>Composants requis
Cette section détaille hello requise avant d’intégrer l’authentification Multifacteur Azure hello passerelle Bureau à distance. Avant de commencer, vous devez avoir hello suivant des conditions préalables en place.  

* Infrastructure des Services Bureau à distance (RDS)
* Licence Azure MFA
* Logiciel Windows Server
* Rôle des services de stratégie et d’accès réseau (NPS)
* Azure AD synchronisé avec AD local 
* ID du GUID Azure Active Directory

### <a name="remote-desktop-services-rds-infrastructure"></a>Infrastructure des Services Bureau à distance (RDS)
Vous devez disposer d’une infrastructure de Services Bureau à distance (RDS) de travail en place. Si vous le faites pas, vous pouvez rapidement créer cette infrastructure dans Azure utilisant hello de démarrage rapide modèle : [déploiement de créer la Collection de sessions de bureau à distance](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment). 

Si vous le souhaitez toomanually créer une infrastructure de services Bureau à distance sur site rapidement effectuer des tests, et suivez hello étapes toodeploy une. 
**En savoir plus** : [Déployer des services RDS avec le démarrage rapide Azure](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure) et [Déploiement de l’infrastructure RDS de base](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure). 

### <a name="licenses"></a>Licences
Une licence pour Azure MFA est obligatoire, disponible via un abonnement Azure AD Premium, Enterprise Mobility plus Security (EMS) ou MFA. Pour plus d’informations, consultez [comment tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md). À des fins de test, vous pouvez utiliser un abonnement d’évaluation.

### <a name="software"></a>Logiciel
Hello, extension de serveur NPS requiert Windows Server 2008 R2 SP1 ou version ultérieure avec le service de rôle NPS hello installé. Toutes les étapes de hello dans cette section ont été effectuées à l’aide de Windows Server 2016.

### <a name="network-policy-and-access-services-nps-role"></a>Rôle des services de stratégie et d’accès réseau (NPS)
Hello service de rôle NPS fournit le client et le serveur RADIUS de hello fonctionnalités, ainsi que de service de contrôle d’intégrité de la stratégie d’accès réseau. Ce rôle doit être installé sur au moins deux ordinateurs dans votre infrastructure : hello de passerelle Bureau à distance et un autre serveur membre ou contrôleur de domaine. Par défaut, le rôle de hello est déjà présent sur hello ordinateur configuré en tant que hello passerelle Bureau à distance.  Vous devez également installer au moins rôle NPS de hello sur un autre ordinateur, tel qu’un contrôleur de domaine ou un serveur membre.

Pour plus d’informations sur l’installation du rôle de serveur NPS hello de service Windows Server 2012 ou plus anciens, consultez [installer un serveur de stratégie de contrôle d’intégrité NAP](https://technet.microsoft.com/library/dd296890.aspx). Pour obtenir une description des meilleures pratiques pour NPS, y compris hello recommandation tooinstall NPS sur un contrôleur de domaine, consultez [meilleures pratiques pour NPS](https://technet.microsoft.com/library/cc771746).

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>Azure Active Directory synchronisé avec Active Directory local 
toouse hello extension serveur NPS local utilisateurs doivent être synchronisés avec Azure AD et activés pour l’authentification Multifacteur. Cette section part du principe que les utilisateurs locaux sont synchronisés avec Azure AD en utilisant AD Connect. Pour obtenir plus d’informations sur Azure AD Connect, consultez [Intégrer vos répertoires locaux avec Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md). 

### <a name="azure-active-directory-guid-id"></a>ID du GUID Azure Active Directory
tooinstall NPS, vous devez tooknow hello GUID de hello Azure AD. Vous trouverez ci-dessous des instructions pour la recherche hello GUID de hello Azure AD.

## <a name="configure-multi-factor-authentication"></a>Configurer l’authentification multifacteur 
Cette section fournit des instructions pour l’intégration d’Azure MFA avec hello passerelle Bureau à distance. En tant qu’administrateur, vous devez configurer le service de l’authentification Multifacteur Azure hello avant que les utilisateurs peuvent s’inscrire automatiquement leurs applications ou périphériques de plusieurs facteurs.

Suivez les étapes de hello dans [prise en main d’Azure multi-Factor Authentication dans le cloud de hello](multi-factor-authentication-get-started-cloud.md) tooenable l’authentification Multifacteur pour vos utilisateurs Azure AD. 

### <a name="configure-accounts-for-two-step-verification"></a>Configurer des comptes pour la vérification en deux étapes
Une fois qu’un compte a été activé pour l’authentification Multifacteur, vous ne pouvez pas vous connecter tooresources régie par hello stratégie d’authentification Multifacteur jusqu'à ce que vous avez correctement configuré un toouse appareil approuvé pour le second facteur d’authentification hello ont authentifié à l’aide de la vérification en deux étapes.

Suivez les étapes de hello dans [que signifie l’authentification multifacteur Azure pour moi ?](./end-user/multi-factor-authentication-end-user.md) toounderstand et configurer correctement vos appareils pour l’authentification Multifacteur avec votre compte d’utilisateur.

## <a name="install-and-configure-nps-extension"></a>Installer et configurer l’extension NPS
Cette section fournit des instructions pour la configuration des services Bureau à distance infrastructure toouse Azure MFA pour l’authentification du client avec hello passerelle Bureau à distance.

### <a name="acquire-azure-active-directory-guid-id"></a>Acquérir l’ID du GUID Azure Active Directory

Dans le cadre de la configuration de hello Hello extension du serveur NPS, vous devez identification d’administrateur de toosupply et l’ID de Azure AD hello pour votre locataire Azure AD. Hello suit vous montre comment ID de tooget hello locataire.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’administrateur global de hello Hello Azure locataire.
2. Bonjour barre de navigation gauche, sélectionnez hello **Azure Active Directory** icône.
3. Sélectionner **Propriétés**.
4. Dans le panneau des propriétés hello, en regard de hello ID de répertoire, cliquez sur hello **copie** icône, comme illustré ci-dessous, toocopy hello ID tooclipboard.

 ![Propriétés](./media/nps-extension-remote-desktop-gateway/image1.png)

### <a name="install-hello-nps-extension"></a>Installation de l’extension de serveur NPS hello
Installer l’extension NPS hello sur un serveur qui a hello stratégie réseau et le rôle de Services d’accès (NPS) est installé. Cela fonctionne comme serveur RADIUS de hello pour votre conception. 

>[!Important]
> Assurez-vous que vous n’installez pas d’extension NPS hello sur votre serveur de passerelle Bureau à distance.
> 

1. Télécharger hello [extension NPS](https://aka.ms/npsmfa). 
2. Copiez le serveur NPS toohello hello le programme d’installation le fichier exécutable (NpsExtnForAzureMfaInstaller.exe).
3. Sur le serveur NPS de hello, double-cliquez sur **NpsExtnForAzureMfaInstaller.exe**. À l’invite, cliquez sur **Exécuter**.
4. Bonjour NPS Extension pour la boîte de dialogue de l’authentification Multifacteur Azure, consultez hello le contrat de licence, vérifiez **J’accepte les conditions générales du contrat de licence toohello**, puis cliquez sur **installer**.
 
  ![Programme d’installation d’Azure MFA](./media/nps-extension-remote-desktop-gateway/image2.png)

5. Bonjour NPS Extension pour la boîte de dialogue de l’authentification Multifacteur Azure, cliquez sur Fermer. 

  ![Extension NPS pour Azure MFA](./media/nps-extension-remote-desktop-gateway/image3.png)

### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Configurer des certificats pour une utilisation avec l’extension de serveur NPS hello à l’aide d’un script PowerShell
Ensuite, vous devez tooconfigure certificats pour une utilisation par des communications sécurisées hello NPS extension tooensure et l’assurance. composants du serveur NPS Hello incluent un script Windows PowerShell qui configure un certificat auto-signé à utiliser avec le serveur NPS. 

script de Hello exécute hello suivant des actions :

* crée un certificat auto-signé
* Associe la clé publique du certificat tooservice de principal sur Azure AD
* Magasins hello certificat dans le magasin de l’ordinateur local hello
* Utilisateur de réseau toohello de clé privée du certificat toohello accorde l’accès
* redémarre le service de serveur de stratégie réseau

Si vous souhaitez toouse vos propres certificats, vous avez besoin de votre principal de service de certificat toohello tooassociate hello public sur Azure AD et ainsi de suite.

script de hello de toouse, fournir les extension hello avec vos informations d’identification Azure AD Admin et hello ID de locataire Azure AD que vous avez copiée précédemment. Exécutez le script de hello sur chaque serveur NPS où vous avez installé l’extension de serveur NPS hello. Puis la hello suivant :

1. Ouvrez une invite administrative Windows PowerShell.
2. À l’invite de commandes PowerShell hello, tapez **cd « c:\Program Files\Microsoft\AzureMfa\Config »**, puis appuyez sur **entrée**.
3. Tapez _.\AzureMfsNpsExtnConfigSetup.ps1_, puis appuyez sur **ENTRÉE**. script de Hello vérifie toosee si le module Azure Active Directory PowerShell hello est installé. Le cas contraire, script de hello installe le module de hello pour vous.

  ![Azure AD PowerShell](./media/nps-extension-remote-desktop-gateway/image4.png)
  
4. Une fois le script de hello vérifie l’installation de hello du module PowerShell de hello, il affiche la boîte de dialogue module Azure Active Directory PowerShell hello. Dans la boîte de dialogue hello, entrez vos informations d’identification d’administrateur d’Azure AD et un mot de passe, puis cliquez sur **connexion**.

  ![Ouvrez le compte Powershell](./media/nps-extension-remote-desktop-gateway/image5.png)

5. Lorsque vous y êtes invité, collez l’ID de client hello copiés précédemment toohello Presse-papiers, puis appuyez sur **entrée**.

  ![Entrez l’ID client](./media/nps-extension-remote-desktop-gateway/image6.png)

6. script de Hello crée un certificat auto-signé et effectue d’autres modifications de configuration. sortie de Hello doit être comme image hello indiqué ci-dessous.

  ![Certificat auto-signé](./media/nps-extension-remote-desktop-gateway/image7.png)

## <a name="configure-nps-components-on-remote-desktop-gateway"></a>Configurer les composants de serveur NPS sur la passerelle des services Bureau à distance
Dans cette section, vous configurez des stratégies d’autorisation des connexions hello passerelle Bureau à distance et autres paramètres de RADIUS.

flux d’authentification Hello requiert que les messages RADIUS être échangés entre hello passerelle Bureau à distance et hello serveur NPS où hello serveur NPS est installé. Cela signifie que vous devez configurer les paramètres des clients RADIUS sur la passerelle Bureau à distance et hello serveur NPS où hello NPS extension est installé. 

### <a name="configure-remote-desktop-gateway-connection-authorization-policies-toouse-central-store"></a>Configurer le magasin central toouse de stratégies d’autorisation passerelle Bureau à distance connexion
Stratégies d’autorisation de connexion Bureau à distance (bureau à distance) spécifient hello pour le serveur de passerelle Bureau à distance se connectant tooa. Les stratégies RD CAP peuvent être stockées localement (par défaut) ou être stockées dans un Store de stratégies RD CAP central qui exécute un serveur NPS. tooconfigure l’intégration d’Azure MFA avec les services Bureau à distance, vous avez besoin d’utiliser de hello toospecify d’un magasin central.

1. Sur le serveur de passerelle Bureau à distance hello, ouvrez **le Gestionnaire de serveur**. 
2. Cliquez sur hello, **outils**, point trop**Services Bureau à distance**, puis cliquez sur **Gestionnaire de passerelle Bureau à distance**.

  ![Services Bureau à distance](./media/nps-extension-remote-desktop-gateway/image8.png)

3. Dans le Gestionnaire de passerelle Bureau à distance de hello, cliquez sur  **\[nom du serveur\] (Local)**, puis cliquez sur **propriétés**.

  ![Nom du serveur](./media/nps-extension-remote-desktop-gateway/image9.png)

4. Dans la boîte de dialogue de propriétés hello, sélectionnez hello **services Bureau à distance** onglet magasin.
5. Sur l’onglet magasin de stratégies de bureau à distance de hello, sélectionnez **serveur Central exécutant NPS**. 
6. Bonjour **Entrez une adresse IP ou le nom de serveur hello NPS** champ, de type hello adresse IP ou serveur de nom de serveur hello où vous avez installé l’extension de serveur NPS hello.

  ![Entrez le nom ou l’adresse IP](./media/nps-extension-remote-desktop-gateway/image10.png)
  
7. Cliquez sur **Add**.
8. Bonjour **Secret partagé** boîte de dialogue, entrez un secret partagé, puis cliquez sur **OK**. Assurez-vous d’enregistrer ce secret partagé et de stocker les enregistrements de hello en toute sécurité.

 >[!NOTE]
 >Secret partagé est utilisé approbation tooestablish entre les clients et serveurs RADIUS de hello. Créer un mot de passe long et complexe.
 >

 ![Secret partagé](./media/nps-extension-remote-desktop-gateway/image11.png)

9. Cliquez sur **OK** boîte de dialogue tooclose hello.

### <a name="configure-radius-timeout-value-on-remote-desktop-gateway-nps"></a>Configurer la valeur de délai d’expiration RADIUS sur le serveur NPS de passerelle Bureau à distance
tooensure il est temps d’informations d’identification des utilisateurs toovalidate, effectuer une vérification en deux étapes, recevoir des réponses et répond tooRADIUS messages, il s’agit de la valeur du délai d’attente nécessaire tooadjust hello rayon.

1. Sur le serveur de passerelle Bureau à distance hello, dans le Gestionnaire de serveur, cliquez sur **outils**, puis cliquez sur **serveur NPS**. 
2. Bonjour **NPS (Local)** de la console, développez **Clients et serveurs RADIUS**, puis sélectionnez **serveur RADIUS distant**.

 ![Serveur RADIUS à distance](./media/nps-extension-remote-desktop-gateway/image12.png)

3. Dans le volet d’informations hello, double-cliquez sur **groupe de serveur de passerelle TS**.

 >[!NOTE]
 >Ce groupe de serveurs RADIUS a été créé lorsque vous avez configuré le serveur central de hello pour les stratégies du serveur NPS. Hello passerelle Bureau à distance transfère RADIUS messages toothis serveur ou groupe de serveurs, si elle est supérieure à un groupe de hello.
 >

4. Bonjour **propriétés de groupe de serveurs de passerelle TS** boîte de dialogue, adresse IP de hello select ou nom de hello du serveur NPS configuré de toostore Bureau à distance, puis cliquez sur **modifier**. 

 ![Groupe de serveurs de passerelle TS](./media/nps-extension-remote-desktop-gateway/image13.png)

5. Bonjour **modifier le serveur RADIUS** boîte de dialogue, sélectionnez hello **l’équilibrage de charge** onglet.
6. Bonjour **l’équilibrage de charge** onglet hello **nombre de secondes sans réponse avant que la requête est considérée comme supprimée** , modifiez la valeur par défaut de hello à partir de la valeur de 3 tooa entre 30 et 60 secondes.
7. Bonjour **nombre de secondes entre les demandes quand le serveur est identifié comme étant indisponible** , modifiez la valeur par défaut de hello de valeur de tooa de 30 secondes est égal tooor supérieure à la valeur hello spécifié à l’étape précédente de hello.

 ![Modifier le serveur RADIUS](./media/nps-extension-remote-desktop-gateway/image14.png)

8.  Cliquez sur OK à deux fois les boîtes de dialogue tooclose hello.

### <a name="verify-connection-request-policies"></a>Vérifiez les stratégies de demande de connexion 
Par défaut, lorsque vous configurez la passerelle Bureau à distance de hello toouse un magasin de stratégies central pour les stratégies d’autorisation de connexion, hello passerelle Bureau à distance est le serveur NPS toohello tooforward configuré CAP demandes. serveur NPS de Hello avec l’extension de l’authentification Multifacteur Azure hello installé, de demande d’accès RADIUS processus hello. Hello suit vous montre comment les stratégie de demande de connexion par défaut de hello tooverify. 

1. Sur hello passerelle Bureau à distance, dans la console NPS (Local) hello, développez **stratégies**, puis sélectionnez **stratégies de demande de connexion**.
2. Cliquez avec le bouton droit sur **Stratégies de demandes de connexion** et double cliquez sur **STRATÉGIE D’AUTORISATION DE PASSERELLE TS**.
3. Bonjour **propriétés de la stratégie d’autorisation de passerelle TS** boîte de dialogue, cliquez sur hello **paramètres** onglet.
4. Sur l’onglet **Paramètres**, sous Transfert de la demande de connexion, cliquez sur **Authentification**. Client RADIUS est configuré tooforward les demandes d’authentification.

 ![Paramètres d’authentification](./media/nps-extension-remote-desktop-gateway/image15.png)
 
5. Cliquez sur **Annuler**. 

## <a name="configure-nps-on-hello-server-where-hello-nps-extension-is-installed"></a>Configurer NPS sur le serveur hello où hello extension de serveur NPS est installé
serveur NPS Hello où extension NPS hello est installé doit toobe tooexchange en mesure de RADIUS messages avec le serveur NPS hello hello passerelle Bureau à distance. Ce message de tooenable exchange, vous devez disposer des composants de serveur NPS de hello tooconfigure sur serveur hello où hello service d’extension du serveur NPS est installé. 

### <a name="register-server-in-active-directory"></a>Enregistrer le serveur dans Active Directory
toofunction correctement dans ce scénario, le serveur NPS de hello doit toobe inscrit dans Active Directory.

1. Ouvrez le **Gestionnaire de serveur**.
2. Dans Gestionnaire de serveurs, cliquez sur **Outils** puis cliquez sur **Serveur de stratégie réseau**. 
3. Dans la console du serveur NPS hello, cliquez sur **NPS (Local)**, puis cliquez sur **inscrire un serveur dans Active Directory**. 
4. Cliquez deux fois sur **OK**.

 ![Enregistrement du serveur dans AD](./media/nps-extension-remote-desktop-gateway/image16.png)

5. Laissez la console de hello ouvert pour la procédure suivante de hello.

### <a name="create-and-configure-radius-client"></a>Créer et configurer un client RADIUS 
Hello passerelle Bureau à distance doit toobe configuré comme serveur RADIUS client toohello NPS. 

1. Sur serveur NPS de hello où hello extension de serveur NPS est installé, Bonjour **NPS (Local)** de la console, cliquez sur **Clients RADIUS** et cliquez sur **nouveau**.

 ![Nouveaux Clients RADIUS](./media/nps-extension-remote-desktop-gateway/image17.png)

2. Bonjour **client RADIUS nouvelle** boîte de dialogue zone, fournissez un nom convivial, tel que _passerelle_, et hello adresse IP ou nom DNS du serveur de passerelle Bureau à distance hello. 
3. Bonjour **secret partagé** et hello **confirmer le secret partagé** , saisissez hello même secret que celle utilisée précédemment.

 ![Nom et adresse](./media/nps-extension-remote-desktop-gateway/image18.png)

4. Cliquez sur **OK** boîte de dialogue tooclose hello RADIUS nouveau client.

### <a name="configure-network-policy"></a>Configurer la stratégie réseau
Rappel hello NPS serveur hello extension de l’authentification Multifacteur Azure est le magasin de stratégie centralisée désigné hello pour hello stratégie de l’autorisation de connexion (CAP). Par conséquent, vous devez tooimplement une extrémité de fin sur les demandes de connexions valide hello NPS serveur tooauthorize.  

1. Dans la console NPS (Local) hello, développez **stratégies**, puis cliquez sur **stratégies réseau**.
2. Avec le bouton droit **serveurs d’accès connexions tooother**, puis cliquez sur **Dupliquer stratégie**. 

 ![Dupliquer la stratégie](./media/nps-extension-remote-desktop-gateway/image19.png)

3. Avec le bouton droit **serveurs d’accès de copie de connexions tooother**, puis cliquez sur **propriétés**.

 ![Propriétés du réseau](./media/nps-extension-remote-desktop-gateway/image20.png)

4. Bonjour **serveurs d’accès de copie de connexions tooother** boîte de dialogue, dans le nom de la stratégie, entrez un nom approprié, tel que **RDG_CAP**. Cochez la case **Stratégie activée**, puis sélectionnez **Accorder l’accès**. Si vous le souhaitez, dans Type d’accès réseau, sélectionnez **Passerelle des services Bureau à distance** ou bien vous pouvez le laisser en tant que **Non spécifié**.

 ![Copie des connexions](./media/nps-extension-remote-desktop-gateway/image21.png)

5.  Cliquez sur hello **contraintes** et vérifiez **tooconnect de clients Autoriser sans négocier une méthode d’authentification**.

 ![Autoriser les clients tooconnect](./media/nps-extension-remote-desktop-gateway/image22.png)

6. Si vous le souhaitez, cliquez sur hello **Conditions** onglet et ajouter des conditions qui doivent être remplies pour hello connexion toobe autorisé, par exemple, l’appartenance à un groupe Windows spécifique.

 ![Conditions](./media/nps-extension-remote-desktop-gateway/image23.png)

7. Cliquez sur **OK**. Lorsque le message tooview hello rubrique d’aide correspondante, cliquez sur **non**.
8. Vérifiez que votre nouvelle stratégie est haut hello de liste hello, que la stratégie de hello est activé, et qu’il accorde un accès.

 ![Stratégies de réseau](./media/nps-extension-remote-desktop-gateway/image24.png)

## <a name="verify-configuration"></a>Vérifier la configuration
configuration de hello tooverify, vous devez toolog sur hello passerelle Bureau à distance avec un client RDP approprié. Être toouse qu’un compte qui est autorisé par les stratégies d’autorisation de connexion et est activé pour Azure MFA. 

Comme indiqué dans l’image hello ci-dessous, vous pouvez utiliser hello **accès Bureau à distance par le Web** page.

![Accès web au Bureau à distance](./media/nps-extension-remote-desktop-gateway/image25.png)

Lors de l’entrée avec succès vos informations d’identification pour l’authentification principale, boîte de dialogue de connexion de bureau à distance hello présente l’état de l’initialisation de la connexion à distance, comme indiqué ci-dessous. 

Si vous authentifiez correctement avec la méthode d’authentification secondaire hello que vous avez configuré précédemment dans l’authentification Multifacteur Azure, vous êtes connecté toohello ressource. Toutefois, si l’authentification secondaire hello n’a pas réussie, refusé accès tooresource. 

![Initier la connexion à distance](./media/nps-extension-remote-desktop-gateway/image26.png)

Dans l’exemple hello ci-dessous, hello authentificateur application sur un appareil Windows phone est l’authentification secondaire utilisé tooprovide hello.

![Comptes](./media/nps-extension-remote-desktop-gateway/image27.png)

Une fois que vous avez correctement authentifié à l’aide de la méthode d’authentification secondaire hello, vous êtes connecté à hello passerelle Bureau à distance comme d’habitude. Toutefois, car vous n’êtes toouse requis une méthode d’authentification secondaire à l’aide d’une application mobile sur un appareil de confiance, hello journal lors du processus est plus sûr qu’il serait dans le cas contraire.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>Afficher les journaux de l’Observateur d’événements pour les événements de connexion réussie
tooview hello réussie-événements de connexion dans les journaux de l’Observateur d’événements Windows hello, vous pouvez émettre hello suivant tooquery de commande Windows PowerShell hello Services Windows Terminal Server et les journaux de sécurité Windows.

tooquery réussie-événements de connexion dans les journaux des opérations hello passerelle _(événements\journaux et Services Logs\Microsoft\Windows\TerminalServices-Gateway\Operational_, utilisez hello suivant de commandes :

* _Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '300'} | FL 
* Cette commande affiche les événements de Windows qui montrent les utilisateur hello remplies les exigences de stratégie d’autorisation de ressource (RAP du Bureau à distance) et a été accordé l’accès.

![Afficher l’observateur d’événements](./media/nps-extension-remote-desktop-gateway/image28.png)

* _Get-WinEvent -Logname Microsoft-Windows-TerminalServices-Gateway/Operational_ | where {$_.ID -eq '200'} | FL
* Cette commande affiche les événements hello affichent lorsque l’utilisateur a satisfait exigences de stratégie d’autorisation de connexion.

![Autorisation de connexion](./media/nps-extension-remote-desktop-gateway/image29.png)

Vous pouvez également afficher ce journal et filtrer les ID d’événement, 300 et 200. événements d’ouverture de session réussie tooquery dans les journaux Observateur d’événements de sécurité hello, utilisez hello de commande suivante :

* _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL 
* Cette commande peut être exécutée sur un serveur NPS central de hello ou hello du serveur de passerelle Bureau à distance. 

![Événements de connexion réussie](./media/nps-extension-remote-desktop-gateway/image30.png)

Vous pouvez également afficher journal de sécurité hello ou hello stratégie réseau et accéder aux Services affichage personnalisé, comme indiqué ci-dessous :

![Services de stratégie et d’accès réseau](./media/nps-extension-remote-desktop-gateway/image31.png)

Sur serveur hello où vous avez installé les extensions du serveur NPS hello pour l’authentification Multifacteur Azure, vous trouverez des journaux de l’Observateur d’événements application extension toohello spécifique à _d’Application et de Services Logs\Microsoft\AzureMfa_. 

![Journaux d’application de l’observateur d’événements](./media/nps-extension-remote-desktop-gateway/image32.png)

## <a name="troubleshoot-guide"></a>Guide de résolution des problèmes

Si la configuration de hello ne fonctionne pas comme prévu, hello première place toostart tootroubleshoot est tooverify qui hello utilisateur toouse configuré Azure MFA. Avoir utilisateur de hello connecter toohello [portail Azure](https://portal.azure.com). Si les utilisateurs sont invités à une vérification secondaire et peuvent correctement s’authentifier, vous pouvez éliminer une configuration incorrecte d’Azure MFA.

Si l’authentification Multifacteur Azure fonctionne pour les utilisateurs de hello, vous devez examiner les journaux d’événements appropriés hello. Il s’agit notamment des journaux des événements de sécurité, la passerelle opérationnelle et l’authentification Multifacteur Azure hello qui sont décrites dans la section précédente de hello. 

Voici un exemple de sortie du journal de sécurité montrant un échec d’événement de connexion (ID d’événement 6273).

![Échec de l’événement de connexion](./media/nps-extension-remote-desktop-gateway/image33.png)

Est un événement associé à partir des journaux de hello AzureMFA indiquée ci-dessous :

![Journal Azure MFA](./media/nps-extension-remote-desktop-gateway/image34.png)

tooperform avancée résoudre les options, consultez hello NPS de base de données journal des fichiers de format où hello service NPS est installé. Ces fichiers journaux sont créés dans le dossier _%SystemRoot%\System32\Logs_ comme fichiers texte délimité par des virgules. 

Pour obtenir une description de ces fichiers journaux, consultez [Interpréter des fichiers journaux au format base de données de serveur NPS](https://technet.microsoft.com/library/cc771748.aspx). entrées Hello dans ces fichiers journaux peuvent être difficile toointerpret sans les importer dans une feuille de calcul ou une base de données. Vous pouvez rechercher plusieurs analyseurs IAS tooassist en ligne vous interpréter hello des fichiers journaux. 

Hello image ci-dessous montre sortie hello d’une telle téléchargeable [à contribution volontaire application](http://www.deepsoftware.com/iasviewer). 

![Application de logiciel à contribution volontaire](./media/nps-extension-remote-desktop-gateway/image35.png)

Enfin, pour obtenir des options de résolution des problèmes supplémentaires, vous pouvez utiliser un analyseur de protocoles, tel que [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx). 

l’image ci-dessous à partir de l’Analyseur de Message Microsoft Hello montre le trafic de réseau filtré sur le protocole RADIUS qui contient le nom d’utilisateur hello **Contoso\AliceC**.

![Microsoft Message Analyzer](./media/nps-extension-remote-desktop-gateway/image36.png)

## <a name="next-steps"></a>Étapes suivantes
[Comment tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md)

[Passerelle des services Bureau à distance et serveur Multi-Factor Authentication avec RADIUS](multi-factor-authentication-get-started-server-rdg.md)

[Intégrer vos répertoires locaux à Azure Active Directory](../active-directory/connect/active-directory-aadconnect.md)
