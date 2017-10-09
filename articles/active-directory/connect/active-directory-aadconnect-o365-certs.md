---
title: renouvellement aaaCertificate pour les utilisateurs Office 365 et Azure AD | Documents Microsoft
description: "Cet article explique les 365 utilisateurs tooOffice comment tooresolve problèmes avec des courriers électroniques qui les informer de renouvellement d’un certificat."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 543b7dc1-ccc9-407f-85a1-a9944c0ba1be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b9b309e06949dc5488cd628650be413f366ed347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="renew-federation-certificates-for-office-365-and-azure-active-directory"></a>Renouvellement des certificats de fédération pour Office 365 et Azure Active Directory
## <a name="overview"></a>Vue d'ensemble
Pour la fédération réussie entre Azure Active Directory (Azure AD) et les Services de fédération Active Directory (AD FS), les certificats de hello utilisés par AD FS toosign sécurité jetons tooAzure AD doivent correspondre à ce qui est configuré dans Azure AD. Une incompatibilité peut provoquer des toobroken approbation. Azure AD garantit la synchronisation de ces informations lorsque vous déployez AD FS et le proxy d’application web (pour l’accès extranet).

Cet article fournit les toomanage des informations supplémentaires vous vos certificats de signature de jetons et maintenir synchronisés avec Azure AD, Bonjour suivant le cas :

* Vous ne déployez pas hello Proxy d’Application Web, et par conséquent, les métadonnées de fédération hello ne sont pas disponible dans hello extranet.
* Vous n’utilisez pas la configuration par défaut de hello d’AD FS pour les certificats de signature de jetons.
* Vous utilisez un fournisseur d’identité tiers.

## <a name="default-configuration-of-ad-fs-for-token-signing-certificates"></a>Configuration par défaut d’AD FS pour les certificats de signature de jetons
certificats de déchiffrement de jeton et de signature de jetons Hello sont généralement des certificats auto-signés et sont adaptés pour un an. Par défaut, AD FS inclut un processus de renouvellement automatique appelé **AutoCertificateRollover**. Si vous utilisez AD FS 2.0 ou une version ultérieure, Office 365 et Azure AD mettent automatiquement à jour votre certificat avant qu’il n’arrive à expiration.

### <a name="renewal-notification-from-hello-office-365-portal-or-an-email"></a>Notification de renouvellement de portail de hello Office 365 ou un message électronique
> [!NOTE]
> Reportez-vous à votre certificat pour Office, si vous avez reçu un message électronique ou une notification de portail vous demandant de toorenew [gestion des modifications tootoken certificats de signature](#managecerts) toocheck si vous avez besoin de tootake n’importe quelle action. Microsoft a connaissance d’un éventuel problème pouvant conduire toonotifications pour le renouvellement du certificat est envoyé, même si aucune action n’est requise.
>
>

Azure Active Directory tente de métadonnées de fédération toomonitor hello et le jeton de hello de mise à jour de certificats de signature, comme indiqué par ces métadonnées. 30 jours avant l’expiration hello des certificats de signature de jeton de hello Azure AD vérifie si les nouveaux certificats sont disponibles en interrogeant les métadonnées de fédération hello.

* Si elle peut correctement interroger les métadonnées de fédération hello et récupérer les certificats nouveaux hello, aucune notification par courrier électronique ou un avertissement dans le portail de hello Office 365 n’est émise toohello utilisateur.
* Si elle ne peut pas extraire hello nouveau jeton certificats de signature, soit parce que les métadonnées de fédération hello ne sont pas accessible ou la substitution de certificat automatique n’est pas activée, Azure AD émet une notification par courrier électronique et un avertissement dans le portail de hello Office 365.

![Notification du portail Office 365](./media/active-directory-aadconnect-o365-certs/notification.png)

> [!IMPORTANT]
> Si vous utilisez AD FS, continuité des activités tooensure, vérifiez que vos serveurs possèdent hello après les mises à jour afin que les échecs d’authentification pour les problèmes connus n’apparaissent pas. Cela limite les problèmes connus du serveur proxy AD FS pour ce renouvellement ainsi que pour les périodes de renouvellement suivantes :
>
> Server 2012 R2 - [Windows Server : correctif cumulatif de mai 2014](http://support.microsoft.com/kb/2955164)
>
> Server 2008 R2 et 2012 [Échec de l’authentification par proxy dans Windows Server 2008 R2 SP1 ou dans Windows Server 2012](http://support.microsoft.com/kb/3094446)
>
>

## Vérifier si les certificats hello doivent toobe mis à jour<a name="managecerts"></a>
### <a name="step-1-check-hello-autocertificaterollover-state"></a>Étape 1 : Vérifier l’état de AutoCertificateRollover hello
Sur votre serveur AD FS, ouvrez Powershell. Vérifiez que hello AutoCertificateRollover a la valeur tooTrue.

    Get-Adfsproperties

![AutoCertificateRollover](./media/active-directory-aadconnect-o365-certs/autocertrollover.png)

>[!NOTE] 
>Si vous utilisez AD FS 2.0, commencez par exécuter Add-Pssnapin Microsoft.Adfs.Powershell.

### <a name="step-2-confirm-that-ad-fs-and-azure-ad-are-in-sync"></a>Étape 2 : vérifier que les services AD FS et Azure AD sont synchronisés
Sur votre serveur AD FS, ouvrir l’invite de commandes PowerShell Azure AD hello et se connecter tooAzure AD.

> [!NOTE]
> Vous pouvez télécharger Azure AD PowerShell [ici](https://technet.microsoft.com/library/jj151815.aspx).
>
>

    Connect-MsolService

Vérifiez les certificats hello configuré dans AD FS et les propriétés d’approbation de Azure AD pour hello de domaine spécifiant.

    Get-MsolFederationProperty -DomainName <domain.name> | FL Source, TokenSigningCertificate

![Get-MsolFederationProperty](./media/active-directory-aadconnect-o365-certs/certsync.png)

Si les empreintes numériques de hello dans les deux hello sorties correspondance, vos certificats sont synchronisés avec Azure AD.

### <a name="step-3-check-if-your-certificate-is-about-tooexpire"></a>Étape 3 : Vérifier si votre certificat est sur tooexpire
Dans la sortie de hello de Get-MsolFederationProperty ou Get-AdfsCertificate, recherchez date hello sous « Pas After ». Si la date de hello est inférieure à 30 jours, vous devez prendre la mesure.

| AutoCertificateRollover | Certificats synchronisés avec Azure AD | Les métadonnées de fédération sont accessibles publiquement | Validité | Action |
|:---:|:---:|:---:|:---:|:---:|
| Oui |Oui |Oui |- |Aucune action n'est nécessaire. Voir [Renouveler le certificat de signature de jetons automatiquement](#autorenew). |
| Oui |Non |- |Moins de 15 jours |Renouvelez immédiatement. Voir [Renouveler le certificat de signature de jetons manuellement](#manualrenew). |
| Non |- |- |Moins de 30 jours |Renouvelez immédiatement. Voir [Renouveler le certificat de signature de jetons manuellement](#manualrenew). |

\[-]  N’a pas d’importance

## Renouveler automatiquement des certificats de signature de jetons de hello (recommandé)<a name="autorenew"></a>
Vous n’avez pas besoin tooperform toutes les étapes manuelles si les deux éléments suivants de hello sont vraies :

* Vous avez déployé le Proxy d’Application Web, qui permet d’accéder aux métadonnées de fédération toohello de hello extranet.
* Vous utilisez la configuration par défaut de hello AD FS (AutoCertificateRollover est activé).

Vérifiez que hello suivant tooconfirm qui hello certificat peut être mis à jour automatiquement.

**1. tooTrue doit être définie à hello propriété d’AD FS AutoCertificateRollover.** Cela indique que AD FS génère automatiquement nouvelle signature de jetons et des certificats de déchiffrement de jeton, avant de hello ancien ceux expirent.

**2. métadonnées de fédération hello AD FS sont accessible publiquement.** Vérifiez que vos métadonnées de fédération sont accessible publiquement en naviguant toohello suivant l’URL à partir d’un ordinateur de hello internet public (sur le réseau d’entreprise hello) :

https://(votre_nom_FS)/federationmetadata/2007-06/federationmetadata.xml

où `(your_FS_name) `est remplacé par le nom d’hôte du service de fédération hello votre organisation utilise, tel que fs.contoso.com.  Si vous êtes en mesure de tooverify les deux de ces paramètres avec succès, vous n’avez pas toodo autre chose.  

Exemple : https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

## Renouveler manuellement le certificat de signature de jeton de hello<a name="manualrenew"></a>
Vous pouvez choisir toorenew certificats de signature de jeton hello manuellement. Par exemple, hello scénarios suivants fonctionnent mieux pour le renouvellement manuel :

* Les certificats de signature de jeton ne sont pas auto-signés. Hello plus souvent, cela est que votre organisation gère les certificats AD FS inscrits à partir d’une autorité de certification d’organisation.
* Sécurité du réseau n’autorise pas toobe de métadonnées de fédération hello publiquement disponible.

Dans ces scénarios, chaque fois que vous mettez à jour les certificats de signature de jeton de hello vous devez également mettre à jour votre domaine à Office 365 à l’aide de la commande PowerShell hello Update-MsolFederatedDomain.

### <a name="step-1-ensure-that-ad-fs-has-new-token-signing-certificates"></a>Étape 1 : s’assurer qu’AD FS dispose de nouveaux certificats de signature de jetons
**Configuration différente de la configuration par défaut**

Si vous utilisez une configuration par défaut des services AD FS (où **AutoCertificateRollover** est défini trop**False**), vous utilisez probablement les certificats personnalisés (ne pas auto-signé). Pour plus d’informations sur l’utilisation des certificats toorenew hello AD FS de signature de jetons, consultez [conseils pour les clients n’utilisez ne pas AD FS des certificats auto-signés](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert).

**Les métadonnées de fédération ne sont pas disponibles publiquement**

Hello d’autre part, si **AutoCertificateRollover** est défini trop**True**, mais les métadonnées de fédération ne sont pas accessible publiquement, d’abord vous assurer que les nouveaux certificats de signature de jeton ont été générées par Active Directory FS. Confirmez que nouveau jeton de signature des certificats par hello en prenant comme suit :

1. Vérifiez que vous êtes connecté sur le serveur de toohello principal AD FS.
2. Vérifier les certificats de signature actuelle hello dans AD FS en ouvrant une fenêtre de commande PowerShell et en cours d’exécution hello de commande suivante :

    PS C:\>Get-ADFSCertificate –CertificateType token-signing

   > [!NOTE]
   > Si vous utilisez AD FS 2.0, vous devez commencer par exécuter Add-Pssnapin Microsoft.Adfs.Powershell.
   >
   >
3. Examinez la sortie de la commande hello à tous les certificats répertoriés. Si AD FS a généré un nouveau certificat, vous devez voir deux certificats dans la sortie de hello : une pour le hello **IsPrimary** valeur est **True** et hello **NotAfter** date est dans les 5 jours et pour lequel **IsPrimary** est **False** et **NotAfter** est sur une année dans hello futures.
4. Si vous consultez un seul certificat et hello **NotAfter** date est comprise dans les 5 jours, vous devez toogenerate un nouveau certificat.
5. toogenerate un nouveau certificat, exécutez hello commande à une invite de commande PowerShell suivante : `PS C:\>Update-ADFSCertificate –CertificateType token-signing`.
6. Vérifier la mise à jour hello en exécutant la commande suivante à nouveau de hello : PS C:\>signature de jetons Get-ADFSCertificate – CertificateType

Deux certificats doivent apparaître maintenant, un d'entre eux possède un **NotAfter** date environ un an dans hello futures et pour quels hello **IsPrimary** valeur est **False**.

### <a name="step-2-update-hello-new-token-signing-certificates-for-hello-office-365-trust"></a>Étape 2 : Mettre à jour hello nouvelle signature de jetons des certificats de confiance de hello Office 365
Mettre à jour d’Office 365 avec hello nouveau jeton signature certificats toobe utilisée pour l’approbation de hello, comme suit.

1. Ouvrez hello Microsoft Azure Module Active Directory pour Windows PowerShell.
2. Exécutez la commande $cred=Get-Credential. Lorsque cette applet de commande vous demande des informations d’identification, tapez vos informations d’identification de compte administrateur de services cloud.
3. Exécutez la commande Connect-MsolService –Credential $cred. Cette applet de commande vous connecte toohello le service cloud. Création d’un contexte de connexion vous toohello le service cloud est requis avant d’exécuter une des autres applets de commande hello installé par l’outil de hello.
4. Si vous exécutez ces commandes sur un ordinateur qui n’est pas serveur de fédération principal hello AD FS, exécutez la cmdlet Set-MSOLAdfscontext-ordinateur <AD FS primary server>, où <AD FS primary server> est le nom de domaine complet interne hello du serveur de hello principal AD FS. Cette applet de commande crée un contexte qui vous connecte tooAD FS.
5. Exécutez Update-MSOLFederatedDomain –DomainName <domain>. Cette applet de commande met à jour les paramètres de hello d’AD FS dans le service de cloud computing hello et configure la relation d’approbation hello entre hello deux.

> [!NOTE]
> Si vous avez besoin de toosupport plusieurs domaines de premier niveau, par exemple contoso.com et fabrikam.com, vous devez utiliser hello **SupportMultipleDomain** commutateur avec les applets de commande. Pour plus d’informations, consultez [Prise en charge de plusieurs domaines de premier niveau](active-directory-aadconnect-multiple-domains.md).
>
>

## Réparer l’approbation Azure AD à l’aide d’Azure AD Connect <a name="connectrenew"></a>
Si vous avez configuré votre batterie de serveurs AD FS et la confiance Azure AD à l’aide d’Azure AD Connect, vous pouvez utiliser Azure AD Connect toodetect si vous avez besoin tootake toute action pour vos certificats de signature de jetons. Si vous avez besoin de certificats de hello toorenew, vous pouvez utiliser Azure AD Connect toodo donc.

Pour plus d’informations, consultez [réparation d’approbation de hello](active-directory-aadconnect-federation-management.md).
