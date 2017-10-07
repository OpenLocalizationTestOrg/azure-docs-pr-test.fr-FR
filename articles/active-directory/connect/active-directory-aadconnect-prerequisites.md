---
title: "Azure AD Connect : Conditions préalables et matériel | Microsoft Docs"
description: "Cette rubrique décrit les composants requis pour hello et hello configuration matérielle requise pour Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 91b88fda-bca6-49a8-898f-8d906a661f07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2ec8b5da9440c92e8f9d6702d5e5e20de952b588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-for-azure-ad-connect"></a>Conditions préalables pour Azure AD Connect
Cette rubrique décrit les conditions préalables hello et hello configuration matérielle requise pour Azure AD Connect.

## <a name="before-you-install-azure-ad-connect"></a>Avant d’installer Azure AD Connect
Avant d’installer Azure AD Connect, voici ce dont vous avez besoin.

### <a name="azure-ad"></a>Azure AD
* Un abonnement Azure ou un [abonnement d’évaluation Azure](https://azure.microsoft.com/pricing/free-trial/). Cet abonnement n’est requis pour accéder aux hello portail Azure et non à l’aide d’Azure AD Connect. Si vous utilisez PowerShell ou Office 365, puis il est inutile une toouse d’abonnement Azure Azure AD Connect. Si vous avez une licence Office 365, vous pouvez également utiliser le portail de hello Office 365. Avec une licence Office 365 payante, vous pouvez également obtenir dans hello portail Azure à partir du portail de hello Office 365.
  * Vous pouvez également utiliser hello [portail Azure](https://portal.azure.com). Ce portail ne nécessite aucune licence Azure Active Directory.
* [Ajouter et vérifier le domaine de hello](../active-directory-domains-add-azure-portal.md) vous prévoyez toouse dans Azure AD. Par exemple, si vous prévoyez toouse contoso.com pour vos utilisateurs, veillez à ce domaine a été vérifié et vous n’utilisez pas de domaine par défaut de contoso.onmicrosoft.com hello uniquement.
* Un client Azure AD prend en charge 50 000 objets par défaut. Lorsque vous vérifiez votre domaine, limite de hello est accrue too300k objets. Si vous avez besoin de davantage d’objets dans Azure AD, vous devez tooopen une prise en charge toohave cas hello augmenter encore davantage. Si vous avez besoin de plus de 500 000 objets, si vous avez besoin d’une licence comme Office 365, Azure AD Standard, Azure AD Premium ou Enterprise Mobility Suite.

### <a name="prepare-your-on-premises-data"></a>Préparez vos données locales
* Utilisez [IdFix](https://support.office.com/article/Install-and-run-the-Office-365-IdFix-tool-f4bd2439-3e41-4169-99f6-3fabdfa326ac) tooidentify des erreurs telles que les doublons et les problèmes de mise en forme dans votre annuaire avant de pouvoir synchroniser tooAzure AD et Office 365.
* Vérifiez [les fonctionnalités de synchronisation facultatives que vous pouvez activer dans Azure AD](active-directory-aadconnectsyncservice-features.md) et évaluez quelles fonctionnalités vous devez activer.

### <a name="on-premises-active-directory"></a>Active Directory local
* Hello AD schéma version et la forêt niveau fonctionnel doit être Windows Server 2003 ou version ultérieure. les contrôleurs de domaine Hello peuvent exécuter n’importe quelle version tant que les conditions requises au niveau hello schéma et de forêt sont remplies.
* Si vous envisagez de fonctionnalité de hello toouse **l’écriture différée de mot de passe**, hello les contrôleurs de domaine doit être Windows Server 2008 (avec le dernier SP) ou version ultérieure. Si vos contrôleurs de domaine sont sur 2008 (version antérieure à R2), vous devez également appliquer le [correctif logiciel KB2386717](http://support.microsoft.com/kb/2386717).
* contrôleur de domaine Hello utilisé par Azure AD doit être accessible en écriture. Il s’agit de **ne pas pris en charge** toouse un RODC (contrôleur de domaine en lecture seule) et l’Azure AD Connect ne suit pas les redirections d’écriture.
* Il s’agit de **ne pas pris en charge** toouse forêts/domaines locaux à l’aide de SLD (domaines en une seule).
* Il s’agit de **ne pas pris en charge** toouse forêts/domaines locaux à l’aide de « en pointillés » (nom contient un point «. ») Noms NetBios.
* Il est recommandé de trop[activer la Corbeille Active Directory de hello](active-directory-aadconnectsync-recycle-bin.md).

### <a name="azure-ad-connect-server"></a>Serveur Azure AD Connect
* Impossible d’installer Azure AD Connect sur Small Business Server ou Windows Server Essentials. serveur de Hello doit utiliser Windows Server standard ou supérieure.
* serveur de se connecter de Hello Azure AD doit avoir une interface utilisateur graphique complet installée. Il s’agit de **ne pas pris en charge** tooinstall sur server core.
* Azure Active Directory Connect doit être installé sur Windows Server 2008 ou version ultérieure. Ce serveur peut être un contrôleur de domaine ou un serveur membre lorsque vous utilisez la configuration rapide. Si vous utilisez des paramètres personnalisés, serveur de hello peut également être autonome et n’a pas de toobe tooa joint à un domaine.
* Si vous installez Azure AD Connect sur Windows Server 2008 ou Windows Server 2008 R2, puis apportez que tooapply hello derniers correctifs logiciels à partir de Windows Update. installation de Hello n’est pas en mesure de toostart avec un serveur non corrigé.
* Si vous envisagez de fonctionnalité de hello toouse **synchronisation de mot de passe**, serveur de se connecter hello Azure AD doit être sur Windows Server 2008 R2 SP1 ou version ultérieure.
* Si vous envisagez de toouse un **compte de service administré de groupe**, serveur de se connecter hello Azure AD doit être Windows Server 2012 ou version ultérieure.
* Bonjour Azure AD Connect serveur doit avoir [.NET Framework 4.5.1](#component-prerequisites) ou version ultérieure et [Microsoft PowerShell 3.0](#component-prerequisites) ou version ultérieure.
* serveur d’Azure AD Connect Hello ne doit pas avoir de stratégie de groupe de la Transcription PowerShell activée.
* Si Active Directory Federation Services est déployé, les serveurs hello dans lequel sont installés les services AD FS ou Proxy d’Application Web doivent être Windows Server 2012 R2 ou version ultérieure. [gestion à distance de Windows](#windows-remote-management) doit être activée sur ces serveurs pour l’installation à distance.
* Si Active Directory Federation Services est déployé, vous avez besoin de [certificats SSL](#ssl-certificate-requirements).
* Si Active Directory Federation Services est en cours de déploiement, il vous suffit de tooconfigure [la résolution de noms](#name-resolution-for-federation-servers).
* Si vos administrateurs généraux ont l’authentification Multifacteur activée, puis hello URL **https://secure.aadcdn.microsoftonline-p.com** doit être dans la liste des sites de confiance hello. Vous êtes tooadd invité à cette liste de sites de confiance toohello site lorsque vous êtes invité à entrer une stimulation d’authentification Multifacteur et il n’a pas été ajouté avant. Vous pouvez utiliser Internet Explorer tooadd il tooyour des sites de confiance.

### <a name="sql-server-used-by-azure-ad-connect"></a>SQL Server utilisé par Azure AD Connect
* Azure AD Connect requiert une données d’identité de base de données SQL Server toostore. Par défaut, une base de données SQL Server 2012 Express LocalDB (version légère de SQL Server Express) est installée. SQL Server Express a une limite de taille de 10 Go qui vous permet de toomanage les objets environ 100 000. Si vous avez besoin de toomanage un volume plus important d’objets d’annuaire, vous devez toopoint hello Assistant tooa différents d’installation de SQL Server.
* Si vous utilisez un serveur SQL Server distinct, ces conditions s’appliquent :
  * Azure AD Connect prend en charge toutes les versions de Microsoft SQL Server à partir de SQL Server 2008 (avec le dernier Service Pack) tooSQL Server 2016 SP1. La Base de données SQL Microsoft Azure n’est **pas prise en charge** comme base de données.
  * Vous devez utiliser un classement SQL qui ne respecte pas la casse. Ces classements sont identifiés par un \_CI_ dans leur nom. Il s’agit de **ne pas pris en charge** toouse un classement qui respecte la casse, identifié par \_CS_ dans leur nom.
  * Vous ne pouvez avoir qu’un seul moteur de synchronisation par instance SQL. Il s’agit de **ne pas pris en charge** tooshare SQL de l’instance avec le service de synchronisation FIM/MIM, DirSync ou Azure AD Sync.

### <a name="accounts"></a>Comptes
* Un compte d’administrateur général de Azure AD pour le client hello Azure AD que toointegrate avec vous le souhaitez. Ce compte doit être un **compte scolaire ou d’organisation** et non d’un **compte Microsoft**.
* Si vous utilisez la configuration rapide ou effectuez une mise à niveau depuis DirSync, vous devez disposer d’un compte d’administrateur d’entreprise pour votre annuaire Active Directory local.
* [Comptes dans Active Directory](active-directory-aadconnect-accounts-permissions.md) si vous utilisez le chemin d’installation de hello des paramètres personnalisés.

### <a name="connectivity"></a>Connectivité
* serveur de se connecter Hello Azure AD a besoin de résolution DNS pour l’intranet et internet. Hello serveur DNS doit être en mesure de tooresolve tooyour locales des noms Active Directory et hello points de terminaison Azure AD.
* Si vous disposez de pare-feu sur votre Intranet et que vous avez besoin de ports tooopen entre les serveurs de se connecter de hello Azure AD et de vos contrôleurs de domaine, puis consultez [Ports de connexion Azure AD](active-directory-aadconnect-ports.md) pour plus d’informations.
* Si votre limite de pare-feu ou proxy d’URL est accessible, hello puis documentées dans les URL [plages d’adresses IP et des URL d’Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) doit être ouvert.
  * Si vous utilisez hello Cloud Microsoft en Allemagne ou hello cloud de Microsoft Azure Government, puis consultez [considérations relatives à des instances de service de synchronisation Azure AD Connect](active-directory-aadconnect-instances.md) des URL.
* Azure AD Connect est par défaut à l’aide de TLS 1.0 toocommunicate avec Azure AD. Vous pouvez modifier cette tooTLS 1.2 en suivant les étapes de hello dans [activer TLS 1.2 pour Azure AD Connect](#enable-tls-12-for-azure-ad-connect).
* Si vous utilisez un proxy sortant pour la connexion Internet de toohello, hello suivant paramètre Bonjour **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config** fichier doit être ajouté pour l’Assistant installation Bonjour Azure AD Connect synchronisation toobe tooconnect en mesure de toohello Internet et Azure AD. Ce texte doit être saisi en bas hello du fichier de hello. Dans ce code, &lt;PROXYADRESS&gt; représente hello nom d’hôte ou adresse IP proxy réel.

```
    <system.net>
        <defaultProxy>
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Si votre serveur proxy requiert une authentification, puis hello [compte de service](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) doit se trouver dans hello domaine et que vous devez utiliser hello personnalisé paramètres installation chemin toospecify un [le compte de service personnalisé](active-directory-aadconnect-get-started-custom.md#install-required-components). Vous devez également un toomachine.config modification différente. Cette modification dans le fichier machine.config, moteur d’installation hello Assistant et synchronisation répondre tooauthentication demandes à partir du serveur de proxy hello. Dans toutes les pages de l’Assistant installation, à l’exclusion de hello **configurer** hello signé à l’utilisateur de la page informations d’identification sont utilisées. Sur hello **configurer** page à fin hello de l’Assistant installation de hello, contexte de hello est commuté toohello [compte de service](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) qui a été créé par vous. section de machine.config Hello doit ressembler à ceci.

```
    <system.net>
        <defaultProxy enabled="true" useDefaultCredentials="true">
            <proxy
            usesystemdefault="true"
            proxyaddress="http://<PROXYADDRESS>:<PROXYPORT>"
            bypassonlocal="true"
            />
        </defaultProxy>
    </system.net>
```

* Lorsque Azure AD Connect envoie un tooAzure de demande web Active Directory dans le cadre de la synchronisation d’annuaires, Azure AD peut s’avérer too5 minutes toorespond. Il est courant pour la configuration du délai d’inactivité de connexion proxy serveurs toohave. Vérifiez que hello a été configuré tooat moins de 6 minutes ou plus.

Pour plus d’informations, consultez MSDN sur hello [proxy élément par défaut](https://msdn.microsoft.com/library/kd3cf2ex.aspx).  
Pour plus d’informations lorsque vous avez des problèmes de connectivité, consultez [Résoudre les problèmes de connectivité liés à Azure AD Connect](active-directory-aadconnect-troubleshoot-connectivity.md).

### <a name="other"></a>Autres
* Facultatif : Une test utilisateur tooverify synchronisation du compte.

## <a name="component-prerequisites"></a>Configuration requise pour les composants
### <a name="powershell-and-net-framework"></a>PowerShell et le .Net Framework
Azure AD Connect repose sur Microsoft PowerShell et le .NET Framework 4.5.1. Cette version ou une version ultérieure doit être installée sur votre serveur. Selon votre version de Windows Server, procédez comme hello suivant :

* Windows Server 2012 R2
  * Microsoft PowerShell est installé par défaut. Aucune action n’est requise.
  * Les versions .NET Framework 4.5.1 et ultérieures sont offertes par le biais de Windows Update. Assurez-vous que vous avez installé hello dernières mises à jour tooWindows Server Bonjour le panneau de configuration.
* Windows Server 2008 R2 et Windows Server 2012
  * version la plus récente de Microsoft PowerShell Hello est disponible dans **Windows Management Framework 4.0**, disponible sur [Microsoft Download Center](http://www.microsoft.com/downloads).
  * .NET Framework 4.5.1 et les versions ultérieures sont disponibles dans le [Centre de téléchargement Microsoft](http://www.microsoft.com/downloads).
* Windows Server 2008
  * version Hello plus récentes prises en charge de PowerShell est disponible dans **Windows Management Framework 3.0**, disponible sur [Microsoft Download Center](http://www.microsoft.com/downloads).
  * .NET Framework 4.5.1 et les versions ultérieures sont disponibles dans le [Centre de téléchargement Microsoft](http://www.microsoft.com/downloads).

### <a name="enable-tls-12-for-azure-ad-connect"></a>Activer TLS 1.2 pour Azure AD Connect
Azure AD Connect est à l’aide de TLS 1.0 par défaut pour le chiffrement des communications hello entre le serveur du moteur de synchronisation hello et Azure AD. Vous pouvez le modifier en configurant .net applications toouse TLS 1.2 par défaut sur le serveur de hello. Vous trouverez plus d’informations sur TLS 1.2 dans [l’Avis de sécurité Microsoft 2960358](https://technet.microsoft.com/security/advisory/2960358).

1. TLS 1.2 ne peut pas être activé sur Windows Server 2008. Vous avez besoin de Windows Server 2008 R2 ou version ultérieure. Vérifiez que vous possédez correctif .net 4.5.1 hello pour votre système d’exploitation, consultez [2960358 avis de sécurité Microsoft](https://technet.microsoft.com/security/advisory/2960358). Il est possible que cette version du correctif ou une version ultérieure soit déjà installée sur votre serveur.
2. Si vous utilisez Windows Server 2008 R2, vérifiez que TLS 1.2 est activé. Sur le serveur Windows Server 2012 et les versions ultérieures, TLS 1.2 doit déjà être activé.
   ```
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2]
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault"=dword:00000000 "Enabled"=dword:00000001
   ```
3. Pour tous les systèmes d’exploitation, définir cette clé de Registre et redémarrez le serveur de hello.
   ```
   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319
   "SchUseStrongCrypto"=dword:00000001
   ```
4. Si vous souhaitez également tooenable TLS 1.2 entre le serveur du moteur de synchronisation hello et un serveur SQL distant, puis vérifiez que vous disposez des versions hello requis installées pour [prise en charge de TLS 1.2 pour Microsoft SQL Server](https://support.microsoft.com/kb/3135244).

## <a name="prerequisites-for-federation-installation-and-configuration"></a>Configuration requise pour l'installation et la configuration de la fédération
### <a name="windows-remote-management"></a>gestion à distance de Windows
Lorsque vous utilisez Azure AD Connect toodeploy Active Directory Federation Services ou hello Proxy d’Application Web, vérifiez ces exigences :

* Si le serveur cible de hello est joint au domaine, puis vérifiez que l’option gérés à distance de Windows est activé
  * Dans une fenêtre de commandes PSH avec élévation de privilèges, utilisez la commande `Enable-PSRemoting –force`
* Si le serveur cible hello est WAP ordinateur faisant partie d’un domaine, il y a quelques exigences supplémentaires
  * Sur hello cible ordinateur (WAP) :
    * Assurez-vous de hello winrm (Windows Remote Management / WS-Management) service est en cours d’exécution via le composant logiciel enfichable Services hello
    * Dans une fenêtre de commandes PSH avec élévation de privilèges, utilisez la commande `Enable-PSRemoting –force`
  * Sur l’ordinateur hello sur quel hello Assistant est en cours d’exécution (si l’ordinateur cible hello est non-domaine le domaine joint ou non approuvé) :
    * Dans une fenêtre de commande avec élévation de privilèges PSH, utilisez la commande hello`Set-Item WSMan:\localhost\Client\TrustedHosts –Value <DMZServerFQDN> -Force –Concatenate`
    * Dans le Gestionnaire de serveur :
      * Ajouter un réseau de périmètre WAP hôte toomachine pool (Gestionnaire de serveur -> Gérer -> ajouter des serveurs... onglet utiliser DNS)
      * Onglet Gestionnaire de serveur tous les serveurs : cliquez avec le bouton droit sur le serveur WAP et cliquez sur gérer en tant que..., entrez les informations d’identification locales (pas le domaine) pour l’ordinateur WAP hello
      * toovalidate PSH la connectivité à distance, dans l’onglet du Gestionnaire de serveur tous les serveurs de hello : cliquez avec le bouton droit sur le serveur WAP et choisissez Windows PowerShell. Doit s’ouvrir une session à distance de PSH tooensure à distance PowerShell sessions peuvent être établies.

### <a name="ssl-certificate-requirements"></a>Configuration requise des certificats SSL
* Il est fortement recommandé toouse hello même certificat SSL sur tous les nœuds de votre batterie AD FS et tous les serveurs de proxy d’Application Web.
* certificat de Hello doit être un X509 certificat.
* Vous pouvez utiliser un certificat auto-signé sur les serveurs de fédération dans un environnement de laboratoire de test. Toutefois, pour un environnement de production, nous vous recommandons d’obtenir hello certificat à partir d’une autorité de certification publique.
  * Si vous utilisez un certificat qui n’est pas approuvé publiquement, vérifiez que hello installé sur chaque serveur Proxy d’Application Web est approuvé sur serveur local hello et sur tous les serveurs de fédération
* identité Hello du certificat de hello doit correspondre au nom de service de fédération hello (par exemple, sts.contoso.com).
  * l’identité Hello est une extension autre nom (SAN) de sujet du type dNSName ou, s’il n’y a pas d’entrées SAN, le nom du sujet hello spécifié comme un nom commun.  
  * Plusieurs entrées SAN peuvent être présentes dans le certificat hello, fourni un d’eux correspond au nom de service de fédération de hello.
  * Si vous envisagez de jonction de toouse, un SAN supplémentaire est nécessaire avec la valeur de hello **enterpriseregistration.** suivi d’un suffixe de nom d’utilisateur Principal (UPN) de hello de votre organisation, par exemple, **enterpriseregistration.contoso.com**.
* Les certificats basés sur les clés CNG (CryptoAPI Next Generation) et les fournisseurs de stockage de clés ne sont pas pris en charge. Cela signifie que vous devez utiliser un certificat basé sur un fournisseur de services de chiffrement et non sur un fournisseur de stockage de clés.
* Les certificats utilisant des caractères génériques sont pris en charge.

### <a name="name-resolution-for-federation-servers"></a>Résolution de noms pour les serveurs de fédération
* Configurer les enregistrements DNS pour hello nom de service de fédération AD FS (par exemple sts.contoso.com) pour hello intranet (votre serveur DNS interne) et hello extranet (DNS public via votre bureau d’enregistrement de domaine). Enregistrement de DNS intranet hello, assurez-vous d’utiliser un enregistrements et non les enregistrements CNAME. Cela est nécessaire pour toowork de l’authentification windows correctement à partir de votre ordinateur joint à un domaine.
* Si vous déployez plusieurs serveurs ADFS ou serveur Proxy d’Application Web, puis vérifiez que vous avez configuré votre équilibreur de charge et que les enregistrements DNS hello pour la fédération des hello AD FS du service de nom (par exemple sts.contoso.com) point toohello l’équilibrage de charge.
* Pour toowork de l’authentification intégrée windows pour les applications de navigateur à l’aide d’Internet Explorer sur votre intranet, assurez-vous que le nom du service de fédération AD FS (par exemple sts.contoso.com) hello est ajouté toohello zone de l’intranet dans Internet Explorer. Cela peut être contrôlé via la stratégie de groupe et tooall déployé votre domaine joint les ordinateurs.

## <a name="azure-ad-connect-supporting-components"></a>Composants de prise en charge d’Azure AD Connect
Hello Voici une liste des composants Azure AD Connect s’installe sur le serveur hello où Azure AD Connect est installé. Cette liste est destinée à une installation Express de base. Si vous choisissez un autre serveur SQL Server toouse sur hello installer la page des services de synchronisation, puis SQL Express LocalDB n’est pas installée localement.

* Azure AD Connect Health
* Assistant de connexion Microsoft Online Services pour les professionnels de l’informatique (installé, mais sans dépendance)
* Utilitaires de ligne de commande Microsoft SQL Server 2012
* Base de données locale Microsoft SQL Server 2012 Express
* Client natif Microsoft SQL Server 2012
* Package de redistribution Microsoft Visual C++ 2013

## <a name="hardware-requirements-for-azure-ad-connect"></a>Configuration matérielle requise pour Azure AD Connect
tableau Hello ci-dessous montre hello configuration minimale requise pour ordinateur de synchronisation Azure AD Connect hello.

| Nombre d’objets dans Active Directory | UC | Mémoire | Taille du disque dur |
| --- | --- | --- | --- |
| Moins de 10 000 |1,6 GHz |4 Go |70 Go |
| Entre 10 000 et 50 000 |1,6 GHz |4 Go |70 Go |
| Entre 50 000 et 100 000 |1,6 GHz |16 Go |100 Go |
| Pour les objets de 100 000 ou plus, version complète de hello de SQL Server est requise | | | |
| Entre 100 000 et 300 000 |1,6 GHz |32 Go |300 Go |
| Entre 300 000 et 600 000 |1,6 GHz |32 Go |450 Go |
| Plus de 600 000 |1,6 GHz |32 Go |500 Go |

Hello configuration minimale requise pour les ordinateurs exécutant les services AD FS ou serveurs d’applications Web est suivant de hello :

* Processeur : double cœur 1,6 GHz ou supérieur
* MÉMOIRE : 2 Go ou plus
* Machine virtuelle Azure : configuration A2 ou supérieure

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
