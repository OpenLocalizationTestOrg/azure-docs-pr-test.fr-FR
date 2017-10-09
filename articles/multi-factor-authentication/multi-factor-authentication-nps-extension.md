---
title: "fonctionnalités de l’authentification Multifacteur Azure aaaUse existantes NPS serveurs tooprovide | Documents Microsoft"
description: "Hello, extension de serveur de stratégie réseau pour l’authentification multifacteur Azure est une solution simple tooadd en deux étapes de nuage vericiation fonctionnalités tooyour infrastructure d’authentification existante."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: e9fc495b06873d45f06233f1aa618db9d94f8bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a>Intégrer votre infrastructure NPS existante dans Azure Multi-Factor Authentication

Hello extension serveur NPS (Network Policy Server) pour l’authentification Multifacteur Azure ajoute en cloud MFA fonctionnalités tooyour infrastructure d’authentification à l’aide de vos serveurs existants. Avec hello extension du serveur NPS, vous pouvez ajouter un appel téléphonique, message texte ou téléphone application Vérification tooyour existant flux d’authentification sans avoir tooinstall, configurer et gérer les nouveaux serveurs. 

Cette extension a été créée pour les organisations qui souhaitent des connexions VPN de tooprotect sans déploiement hello serveur Azure MFA. Hello extension du serveur NPS joue un adaptateur entre RADIUS et tooprovide de l’authentification Multifacteur Azure nuage un second facteur d’authentification pour les utilisateurs fédérés ou synchronisés.

Lorsque vous utilisez l’extension de serveur NPS hello pour Azure MFA, flux d’authentification hello inclut hello suivant des composants : 

1. **Serveur NAS/VPN** reçoit les demandes des clients VPN et les convertit en serveurs tooNPS de demandes RADIUS. 
2. **Serveur NPS** se connecte tooActive Active tooperform hello authentification principale pour hello demande RADIUS et, en cas de réussite, transmet les extensions hello demande tooany installé.  
3. **Extension de NPS** déclenche un tooAzure demande l’authentification Multifacteur pour l’authentification secondaire hello. Une fois que l’extension de hello reçoit la réponse de hello et si hello stimulation d’authentification Multifacteur réussit, il termine la demande d’authentification hello en fournissant un serveur NPS de hello avec des jetons de sécurité qui incluent une revendication d’authentification Multifacteur, émise par Azure STS.  
4. **L’authentification Multifacteur Azure** communique avec les détails de l’utilisateur Azure Active Directory tooretrieve hello et effectue l’authentification secondaire hello à l’aide d’un utilisateur de toohello vérification méthode configurée.

Hello suivant le diagramme illustre ce flux de demande d’authentification de niveau supérieur : 

![Diagramme du flux d’authentification](./media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a>Planifier votre déploiement

Hello, extension de serveur NPS gère automatiquement la redondance, vous n’avez pas besoin d’une configuration spéciale.

Vous pouvez créer autant de serveurs NPS compatibles avec Azure MFA que vous le souhaitez. Si vous installez plusieurs serveurs, vous devez utiliser un certificat client différent pour chacun d'entre eux. La création d’un certificat pour chaque serveur signifie que vous pouvez mettre à jour chaque certificat individuellement et que vous n’avez pas à craindre une interruption de service sur tous vos serveurs.

Serveurs VPN acheminent les demandes d’authentification, de sorte qu’ils toobe prenant en charge de nouveaux serveurs NPS d’activation de l’authentification Multifacteur Azure hello.

## <a name="prerequisites"></a>Composants requis

Hello, extension de serveur NPS est censée toowork avec votre infrastructure existante. Assurez-vous que vous avez hello suivant des conditions préalables avant de commencer.

### <a name="licenses"></a>Licences

Hello Extension NPS pour Azure MFA est disponible toocustomers avec [licences pour Azure multi-Factor Authentication](multi-factor-authentication.md) (inclus avec Azure AD Premium, EMS ou d’un abonnement de l’authentification Multifacteur).

### <a name="software"></a>Logiciel

Windows Server 2008 R2 SP1 ou version ultérieure.

### <a name="libraries"></a>Bibliothèques

Ces bibliothèques sont installés automatiquement avec l’extension de hello.
-   [Visual C++ Redistributable Packages pour Visual Studio 2013 (X64)](https://www.microsoft.com/download/details.aspx?id=40784)
-   [Module Microsoft Azure Active Directory pour Windows PowerShell version 1.1.166.0](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a>Azure Active Directory

Tout le monde à l’aide hello NPS extension doit être synchronisé tooAzure Active Directory à l’aide d’Azure AD Connect et doit être inscrit pour l’authentification Multifacteur.

Lorsque vous installez les extensions hello, vous devez hello directory administration et l’ID d’informations d’identification pour votre locataire Azure AD. Vous pouvez trouver votre ID de répertoire Bonjour [portail Azure](https://portal.azure.com). Connectez-vous en tant qu’administrateur, sélectionnez hello **Azure Active Directory** icône sur hello gauche, puis sélectionnez **propriétés**. Hello copie GUID Bonjour **ID de répertoire** boîte et l’enregistrer. Vous utilisez ce GUID en tant qu’ID de client hello lorsque vous installez hello extension du serveur NPS.

![Identification de votre ID de répertoire dans les propriétés Azure Active Directory](./media/multi-factor-authentication-nps-extension/find-directory-id.png)

## <a name="prepare-your-environment"></a>Préparation de votre environnement

Avant d’installer des extensions NPS hello, vous souhaitez tooprepare vous environnement toohandle hello le trafic d’authentification.

### <a name="enable-hello-nps-role-on-a-domain-joined-server"></a>Activer le rôle de serveur NPS hello sur un serveur appartenant à un domaine

serveur NPS de Hello connecte tooAzure Active Directory et authentifie les demandes d’authentification Multifacteur hello. Choisissez un serveur pour ce rôle. Nous vous recommandons de choisir un serveur qui ne gère pas les demandes provenant d’autres services, étant donné que hello extension NPS lève des erreurs pour toutes les demandes qui ne sont pas RADIUS.

1. Sur votre serveur, ouvrez hello **Assistant Ajouter des rôles et fonctionnalités** de hello menu du Gestionnaire de serveur Quickstart.
2. Choisissez **Installation basée sur un rôle ou une fonctionnalité** pour votre type d’installation.
3. Sélectionnez hello **stratégie de réseau et les Services d’accès** rôle de serveur. Une fenêtre peut s’afficher tooinform des fonctionnalités requises toorun ce rôle.
4. Continuez l’Assistant de hello jusqu'à ce que la page de Confirmation hello. Sélectionnez **Installer**.

Maintenant que vous avez un serveur désigné pour NPS, vous devez également configurer ce serveur toohandle demandes RADIUS à partir de hello solution VPN.

### <a name="configure-your-vpn-solution-toocommunicate-with-hello-nps-server"></a>Configurer votre toocommunicate de solution VPN avec le serveur NPS de hello

En fonction de la solution VPN que vous utilisez, hello tooconfigure étapes varient de votre stratégie d’authentification RADIUS. Configurer ce serveur de stratégie toopoint tooyour RADIUS NPS.

### <a name="sync-domain-users-toohello-cloud"></a>Synchronisation domaine utilisateurs toohello cloud

Cette étape peut être déjà terminée sur votre client, mais il est bon contrôle toodouble que Azure AD Connect a récemment synchronisé de vos bases de données.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’administrateur.
2. Sélectionnez **Azure Active Directory** > **Connexion Azure AD**
3. Vérifiez que votre état de synchronisation est **Activée** et que la dernière synchronisation a eu lieu il y a moins d’une heure.

Si vous devez tookick hors tension d’un nouveau cycle de synchronisation, nous hello d’instructions de [synchronisation Azure AD Connect : planificateur](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).

### <a name="determine-which-authentication-methods-your-users-can-use"></a>Déterminer les méthodes d’authentification que vos utilisateurs peuvent employer

Il existe deux facteurs qui affectent les méthodes d’authentification disponibles avec un déploiement d’extension NPS :

1. algorithme de chiffrement de mot de passe Hello utilisé entre un client RADIUS hello (VPN, Netscaler server, ou autres) et les serveurs NPS hello.
   - **PAP** prend en charge toutes les méthodes d’authentification hello d’Azure MFA dans le cloud de hello : appel téléphonique, message texte à sens unique, notification d’application mobile et code de vérification des applications mobiles.
   - **CHAPv2** et **EAP** prennent en charge l’appel téléphonique et la notification d’application mobile.
2. Hello d’entrée des méthodes qui hello application cliente (VPN, Netscaler server, ou autres) peut gérer. Par exemple, client VPN de hello a d’autres moyens tooallow hello utilisateur tootype dans un code de vérification à partir d’un texte ou d’une application mobile ?

Lorsque vous déployez des extensions NPS hello, utilisez ces tooevaluate facteurs quelles méthodes sont disponibles pour vos utilisateurs. Si votre client RADIUS prend en charge PAP, mais hello UX ne dispose pas des champs d’entrée pour un code de vérification, appel téléphonique et notification d’application mobile sont deux options de prise en charge hello.

Vous pouvez [désactiver les méthodes d’authentification non prises en charge](multi-factor-authentication-whats-next.md#selectable-verification-methods) dans Azure.

### <a name="enable-users-for-mfa"></a>Autoriser des utilisateurs à utiliser MFA

Avant de déployer d’extension NPS hello complète, vous devez tooenable l’authentification Multifacteur pour les utilisateurs de hello que vous souhaitez vérification en deux étapes de tooperform. Plus immédiatement, extension de hello tootest comme vous le déployer, vous avez besoin d’au moins un test compte est entièrement inscrit pour l’authentification multifacteur.

Utilisez ces tooget étapes démarré par un compte de test :
1. Connectez-vous trop[https://aka.ms/mfasetup](https://aka.ms/mfasetup) avec un compte de test. 
2. Suivez tooset des invites hello une méthode de vérification.
3. Créez une stratégie d’accès conditionnel ou [modifier l’état utilisateur hello](multi-factor-authentication-get-started-user-states.md) vérification en deux étapes de toorequire pour le compte de test hello. 

Vos utilisateurs également doivent toofollow tooenroll de ces étapes pour s’authentifier avec l’extension de serveur NPS hello.

## <a name="install-hello-nps-extension"></a>Installation de l’extension de serveur NPS hello

> [!IMPORTANT]
> Installer l’extension de serveur NPS hello sur un serveur autre que le point d’accès VPN hello.

### <a name="download-and-install-hello-nps-extension-for-azure-mfa"></a>Téléchargez et installez l’extension de serveur NPS hello pour Azure MFA

1.  [Télécharger hello NPS Extension](https://aka.ms/npsmfa) de hello Microsoft Download Center.
2.  Copiez toohello binaire de hello serveur NPS vous souhaitez tooconfigure.
3.  Exécutez *setup.exe* et suivez les instructions d’installation hello. Si vous rencontrez des erreurs, vérifiez que hello deux bibliothèques à partir de la section Configuration requise de hello ont été correctement installés.

### <a name="run-hello-powershell-script"></a>Exécutez le script PowerShell de hello

programme d’installation Hello crée un script PowerShell à cet emplacement : `C:\Program Files\Microsoft\AzureMfa\Config` (où C:\ représente le lecteur d’installation). Ce script PowerShell effectue hello suivant des actions :

-   Vous pouvez créer un certificat auto-signé.
-   Associer la clé publique de hello hello toohello du service de certificats principal sur Azure AD.
-   Magasin de certificats de hello dans le magasin de certificats ordinateur local hello.
-   TooNetwork de clé privée du certificat toohello accorder l’accès utilisateur.
-   Redémarrez hello NPS.

Sauf si vous souhaitez toouse vos propres certificats (au lieu de hello des certificats auto-signés qui hello PowerShell script génère), exécutez hello PowerShell Script installation de hello toocomplete. Si vous installez l’extension de hello sur plusieurs serveurs, chacun d’eux doit avoir son propre certificat.

1. Exécutez Windows PowerShell en tant qu’administrateur.
2. Remplacez les répertoires.

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. Exécuter script PowerShell de hello créé par le programme d’installation hello.

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. PowerShell vous invite à entrer votre ID client. Utilisez hello GUID ID de répertoire que vous avez copié à partir de hello portail Azure dans la section conditions préalables de hello.
5. Connectez-vous tooAzure AD en tant qu’administrateur.
6. PowerShell n’affiche un message de réussite lorsque hello script est terminé.  

Répétez ces étapes sur tous les serveurs NPS supplémentaires que vous souhaitez tooset pour l’équilibrage de charge.

>[!NOTE]
>Si vous utilisez vos propres certificats au lieu de générer des certificats avec hello script PowerShell, assurez-vous qu’ils aligneront convention d’affectation de noms du serveur NPS toohello. nom de l’objet Hello doit être **CN =\<TenantID\>, unité d’organisation = Microsoft NPS Extension**. 

## <a name="configure-your-nps-extension"></a>Configurer votre extension NPS

Cette section comprend des considérations relatives à la conception ainsi que des suggestions visant à garantir la réussite des déploiements d’extension NPS.

### <a name="configuration-limitations"></a>Limites de configuration

- Hello extension NPS pour l’authentification Multifacteur Azure n’inclut pas les outils toomigrate utilisateurs et les paramètres de cloud de toohello serveur MFA. Pour cette raison, nous vous suggérons d’à l’aide d’extension de hello pour les nouveaux déploiements, plutôt que de déploiement existant. Si vous utilisez l’extension de hello sur un déploiement existant, vos utilisateurs ont accès preuve tooperform toopopulate à nouveau leur MFA détails dans le cloud de hello.  
- Hello, extension de serveur NPS utilise hello UPN de hello locale utilisateur hello tooidentify à Active directory sur Azure MFA pour effectuer l’extension de hello hello AUTH secondaire peut être configuré toouse un autre identificateur comme autre connexion ID ou Active Directory personnalisé champ autre que UPN. Consultez [configuration des options avancées pour hello extension du serveur NPS pour l’authentification multifacteur](multi-factor-authentication-advanced-vpn-configurations.md) pour plus d’informations.
- Tous les protocoles de chiffrement ne prennent pas en charge toutes les méthodes de vérification.
   - **PAP** prend en charge l’appel téléphonique, le message texte à sens unique, la notification de l’application mobile et le code de vérification de l’application mobile
   - **CHAPv2** et **EAP** prennent en charge l’appel téléphonique et la notification d’application mobile

### <a name="control-radius-clients-that-require-mfa"></a>Contrôler les clients RADIUS nécessitant l’authentification MFA

Une fois que vous activez l’authentification Multifacteur pour un client RADIUS à l’aide de hello NPS Extension, toutes les authentifications pour ce client sont tooperform obligatoire l’authentification Multifacteur. Si vous souhaitez tooenable l’authentification Multifacteur pour certains clients RADIUS, mais pas d’autres, vous pouvez configurer deux serveurs NPS et installer l’extension de hello sur un seul d'entre eux. Configurer des clients RADIUS que vous voulez toorequire MFA toosend demandes toohello serveur NPS configuré avec l’extension de hello et tout autre serveur NPS RADIUS clients toohello ne pas configuré avec l’extension de hello.

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a>Anticiper la présence d’utilisateurs qui ne sont pas inscrits pour l’authentification MFA

Si vous avez des utilisateurs qui ne sont pas inscrits pour l’authentification Multifacteur, vous pouvez déterminer ce qui se passe quand ils tentent de tooauthenticate. Utilisez le paramètre de Registre hello *REQUIRE_USER_MATCH* dans le chemin d’accès du Registre hello *HKLM\Software\Microsoft\AzureMFA* comportement des fonctionnalités toocontrol hello. Ce paramètre ne dispose que d’une seule option de configuration :

| Clé | Valeur | Default |
| --- | ----- | ------- |
| REQUIRE_USER_MATCH | TRUE/FALSE | Pas définie (tooTRUE équivalent) |

Hello l’objectif de ce paramètre est toodetermine le toodo quand un utilisateur n’est pas inscrit pour l’authentification Multifacteur. Lorsque la clé de hello n’existe pas, n’est pas définie ou a la valeur tooTRUE, utilisateur de hello n’est pas inscrit, puis les extension hello échoue stimulation d’authentification Multifacteur hello. Lorsque hello clé a la valeur tooFALSE et utilisateur de hello n’est pas inscrit, l’authentification s’effectue sans effectuer l’authentification Multifacteur.

Vous pouvez choisir toocreate cette clé et valeur tooFALSE alors que vos utilisateurs sont l’intégration, et peut ne pas tous être inscrit pour l’authentification Multifacteur Azure encore. Toutefois, étant donné que la clé du paramètre hello permet aux utilisateurs qui ne sont pas inscrits pour toosign l’authentification Multifacteur dans, vous devez supprimer cette clé avant le cours tooproduction.

## <a name="troubleshooting"></a>Résolution des problèmes

### <a name="how-do-i-verify-that-hello-client-cert-is-installed-as-expected"></a>Comment vérifier que ce certificat de client hello est installé comme prévu ?

Recherchez les hello un certificat auto-signé créé par le programme d’installation de hello dans le magasin de certificats hello et que la clé privée de hello a des autorisations accordées toouser **SERVICE réseau**. certificat de Hello a un nom de sujet de **CN \<tenantid\>, unité d’organisation = Extension Microsoft de NPS**

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-toomy-tenant-in-azure-active-directory"></a>Comment puis-je vérifier que mon certificat client est client toomy associé dans Azure Active Directory ?

Ouvrir une invite de commandes PowerShell et exécution hello suivant les commandes :

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

Ces commandes impriment tous les certificats hello associer votre instance de hello extension du serveur NPS dans votre session PowerShell à votre client. Recherchez votre certificat, exportez votre certificat client en tant que « X.509(.cer) codé en Base 64 » fichier sans clé privée de hello et comparez-le avec liste hello à partir de PowerShell.

Valide-à partir d’et valide-jusqu'à ce que les horodateurs, qui sont dans un format lisible, peut être utilisé toofilter out misfits évidents si la commande hello retourne plus d’un certificat.

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a>Pourquoi mes demandes échouent-elles avec une erreur de jeton ADAL ?

Cette erreur peut être due tooone plusieurs raisons. Utilisez ces étapes toohelp résoudre les problèmes :

1. Redémarrez votre serveur NPS.
2. Vérifiez que le certificat client est installé comme prévu.
3. Vérifiez que le certificat hello est associé à votre client sur Azure AD.
4. Vérifiez que https://login.microsoftonline.com/ est accessible à partir du serveur hello extension de hello en cours d’exécution.

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-hello-user-is-not-found"></a>Pourquoi l’authentification échoue avec une erreur dans les journaux HTTP indiquant que l’utilisateur hello n’est pas trouvé ?

Vérifiez qu’Active Directory Connect est en cours d’exécution et que l’utilisateur hello est présent dans Windows Active Directory et Azure Active Directory.

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a>Pourquoi existe-t-il des erreurs de connexion HTTP dans les journaux pour tous mes échecs d’authentification ?

Vérifiez que https://adnotifications.windowsazure.com est accessible à partir du serveur hello extension NPS hello en cours d’exécution.


## <a name="next-steps"></a>Étapes suivantes

- Configurer d’autres ID de connexion, ou configurer une liste d’exceptions pour les adresses IP qui ne doivent pas effectuer de vérification en deux étapes en [configuration des options avancées pour hello extension du serveur NPS pour l’authentification multifacteur](nps-extension-advanced-configuration.md)

- [Résoudre les messages d’erreur de hello extension du serveur NPS pour Azure multi-Factor Authentication](multi-factor-authentication-nps-errors.md)
