---
title: "liste de compatibilité de fédération aaaAzure AD"
description: "Cette page a non-Microsoft fournisseurs d’identité qui peuvent être utilisé tooimplement l’authentification unique."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 22c8693e-8915-446d-b383-27e9587988ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: ac2f9ad324c8ca6b587b73ea465426ad6b074b03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-federation-compatibility-list"></a>Liste de compatibilité de fédération Azure AD
Azure Active Directory fournit l’authentification unique et une sécurité de l’accès aux applications améliorée pour Office 365 et d’autres ressources de Microsoft Online Services pour des implémentations hybrides et uniquement dans le cloud ne nécessitant aucune solution non-Microsoft. À l’instar de la plupart des services Microsoft Online, Office 365 est intégré à Azure Active Directory pour les services de répertoire, l’authentification et l’autorisation. Azure Active Directory fournit également des toothousands l’authentification uniques d’applications SaaS et localement les applications web. Consultez la galerie d’applications Azure Active Directory hello pour les applications SaaS pris en charge.

Pour les organisations ayant investi dans les solutions de fédération de non Microsoft, cette rubrique contient des conseils pour la configuration de l’authentification unique pour les utilisateurs de Windows Server Active Directory avec les services Microsoft Online services à l’aide de fournisseurs d’identité de non Microsoft à partir de hello « Azure Active Directory federation compatibilité liste » ci-dessous. 

![](./media/active-directory-aadconnect-federation-compatibility/oxford2.jpg)   
[Oxford Computer Group](http://oxfordcomputergroup.com/), organisme tiers, a testé, de la part de Microsoft, ces expériences d’authentification unique à l’aide de fournisseurs d’identité non-Microsoft par rapport à un ensemble de cas d’utilisation courants avec Azure Active Directory.

Pour plus d’informations sur la façon dont votre fournisseur d’identité tiers peut être répertorié ici, contactez Oxford Computer Groupe à l’adresse [idp@oxfordcomputergroup.com](mailto:idp@oxfordcomputergroup.com).

> [!IMPORTANT]
> Groupe d’ordinateurs Oxford testé uniquement les fonctionnalités de fédération hello de ces scénarios d’authentification unique. Groupe d’ordinateurs Oxford n’a pas effectué les tests de synchronisation de hello, l’authentification à deux facteurs, composants etc. de ces scénarios d’authentification unique.
> 
> Utilisation de connexion par un autre ID tooUPN n’est pas également testée dans ce programme.
> 
> 

* [Azure Active Directory](#azure-active-directory)
* [AuthAnvil Single Sign On 4.5](#authanvil-single-sign-on-45)
* [BIG-IP avec Access Policy Manager BIG-IP ver. 11.3x – 11.6x](#big-ip-with-access-policy-manager-big-ip-ver-113x--116x) 
* [BitGlass](#bitglass)
* [CA Secure Cloud](#ca-secure-cloud) 
* [CA SiteMinder 12.52](#ca-siteminder-1252-sp1-cumulative-release-4) 
* [Centrify](#centrify) 
* [Dell One Identity Cloud Access Manager v7.1](#dell-one-identity-cloud-access-manager-v71) 
* [Authentification composite DigitalPersona](#digitalpersona-composite-authentication)
* [IBM Tivoli Federated Identity Manager 6.2.2](#ibm-tivoli-federated-identity-manager-622) 
* [IceWall Federation Version 3.0](#icewall-federation-version-30) 
* [Memority](#memority)
* [NetIQ Access Manager 4.x](#netiq-access-manager-4x) 
* [Okta](#okta) 
* [OneLogin](#onelogin) 
* [Optimal IDM Virtual Identity Server Federation Services](#optimal-idm-virtual-identity-server-federation-services) 
* [PingFederate 6.11, 7.2, 8.x](#pingfederate-611-72-8x)
* [RadiantOne CFS 3.0](#radiantone-cfs-30) 
* [Sailpoint IdentityNow](#sailpoint-identitynow)
* [SecureAuth IdP 7.2.0](#secureauth-idp-720) 
* [Sign&amp;go 5.3](#signgo-53) 
* [Portail du service en ligne SoftBank Technology](#softbank)
* [VMware Workspace One](#vmware-workspace-one)



> [!IMPORTANT]
> Étant donné que ce sont des produits tiers, Microsoft ne fournit pas de prise en charge pour le déploiement de hello, configuration, dépannage, aux meilleures pratiques, etc. problèmes et questions concernant ces fournisseurs d’identité. Pour la prise en charge et des questions concernant ces fournisseurs d’identité, contactez directement le tiers hello pris en charge.
> 
> L’interopérabilité de ces fournisseurs d’identité tiers avec les services cloud Microsoft a uniquement été testée à l’aide des protocoles WS-Federation et WS-Trust. Test n’incluait pas à l’aide du protocole SAML de hello.
> 


## <a name="azure-active-directory"></a>Azure Active Directory

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification : 

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |Aucun |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |Aucun |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucun |
| Applications modernes utilisant ADAL (p. ex., Office 2016) |Pris en charge |Aucune |

Pour plus d’informations sur l’utilisation d’Azure Active Directory avec AD FS, consultez [Services AD FS (Active Directory Federation Services)](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).

Pour plus d’informations sur l’utilisation d’Azure Active Directory avec une synchronisation de mot de passe, consultez [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).

## <a name="authanvil-single-sign-on-45"></a>AuthAnvil Single Sign On 4.5

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique :

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations, consultez [AuthAnvil Single Sign On](https://help.scorpionsoft.com/entries/26538603-How-can-I-Configure-Single-Sign-On-for-Office-365-).


## <a name="big-ip-with-access-policy-manager-big-ip-ver-113x--116x"></a>BIG-IP avec Access Policy Manager BIG-IP ver. 11.3x – 11.6x

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique : 

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |Aucun |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Non pris en charge |Non pris en charge |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucun |

Pour plus d’informations sur BIG-IP Access Policy Manager, consultez [BIG-IP Access Policy Manager.](https://f5.com/products/modules/access-policy-manager) 

Pour obtenir des instructions de BIG-IP Access Policy Manager hello sur la tooconfigure télécharger cette tooyour d’expérience d’authentification unique STS tooprovide hello des utilisateurs Active Directory, hello pdf [BIG-IP](http://www.f5.com/pdf/deployment-guides/microsoft-office-365-idp-dg.pdf).

## <a name="bitglass"></a>BitGlass

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique :

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations sur BitGlass, consultez [BitGlass](http://www.bitglass.com).

## <a name="ca-secure-cloud"></a>CA Secure Cloud

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique :

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations sur CA Secure Cloud, consultez [CA Secure Cloud](http://www.ca.com/us/products/security-as-a-service.aspx).

## <a name="ca-siteminder-1252-sp1-cumulative-release-4"></a>CA SiteMinder 12.52 SP1 version cumulative 4

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique : 

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |Aucun |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |Aucun |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations sur CA SiteMinder, consultez [CA SiteMinder Federation](http://www.ca.com/us/products/ca-single-sign-on.html). 

## <a name="centrify"></a>Centrify

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique :

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |Aucun |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |Aucun |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Le contrôle d’accès des clients n’est pas pris en charge. |

Pour plus d’informations sur Centrify, consultez [Centrify](http://www.centrify.com/cloud/apps/single-sign-on-for-office-365.asp).

## <a name="dell-one-identity-cloud-access-manager-v71"></a>Dell One Identity Cloud Access Manager v7.1

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique :

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |Aucun |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |Aucun |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations sur Dell One Identity Cloud Access Manager, consultez [Dell One Identity Cloud Access Manager](http://software.dell.com/products/cloud-access-manager).

 Pour obtenir des instructions hello sur tooconfigure cette tooyour d’expérience d’authentification unique STS tooprovide hello utilisateurs Office 365, voir [configurer des utilisateurs Office 365](http://documents.software.dell.com/dell-one-identity-cloud-access-manager/7.1/how-to-configure-microsoft-office-365). 

## <a name="digitalpersona-composite-authentication"></a>Authentification composite DigitalPersona  

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique :

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge|
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge|
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations, consultez [DigitalPersona Composite Authentication](http://www.crossmatch.com/uploadedFiles/Support/Reference_Material/DigitalPersona-Office-365-Deployment-Guide.pdf).


## <a name="ibm-tivoli-federated-identity-manager-622"></a>IBM Tivoli Federated Identity Manager 6.2.2

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique : 

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |Aucun |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |Aucun |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations sur IBM Tivoli Federated Identity Manager, consultez [IBM Security Access Manager for Microsoft Applications](http://www-01.ibm.com/support/docview.wss?uid=swg24029517).

## <a name="icewall-federation-version-30"></a>IceWall Federation Version 3.0

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique :

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations sur IceWall Federation, consultez [IceWall Federation Version 3.0](http://h50146.www5.hp.com/products/software/security/icewall/eng/federation/) et [IceWall Federation - Office 365](http://h50146.www5.hp.com/products/software/security/icewall/federation/office365.html).

## <a name="memority"></a>Memority

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification : 

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |Aucun |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |Aucun |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations sur l’utilisation de Memority, consultez [Memority](http://www.memority.com).


## <a name="netiq-access-manager-4x"></a>NetIQ Access Manager 4.x

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique :

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |Aucun|
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |Aucun|
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations, consultez [NetIQ Access Manager](https://www.netiq.com/documentation/access-manager-43/admin/data/b65ogn0.html#b12iqp0m).

## <a name="okta"></a>Okta

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique : 

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |L’authentification Windows intégrée nécessite la configuration supplémentaire d’un serveur web et de l’application Okta. |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |Authentification Windows intégrée |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations sur Okta, consultez [Okta](https://www.okta.com/).

## <a name="onelogin"></a>OneLogin

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique : 

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |Authentification Windows intégrée |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |Authentification Windows intégrée |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations sur OneLogin, consultez [OneLogin](https://www.onelogin.com/).

## <a name="optimal-idm-virtual-identity-server-federation-services"></a>Optimal IDM Virtual Identity Server Federation Services

suivant de Hello est hello matrice de scénario prise en charge cette expérience d’authentification unique :

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |Aucun |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |Authentification Windows intégrée |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |

Pour plus d’informations sur le client Voir stratégies d’accès [tooOffice de limitation de l’accès 365 Services selon hello emplacement Hello Client](https://technet.microsoft.com/library/hh526961.aspx).





## <a name="pingfederate-611-72-8x"></a>PingFederate 6.11, 7.2, 8.x

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique :

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |Aucun |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |Aucun |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucun |

Pour hello obtenir des instructions sur comment tooconfigure ce STS tooprovide hello l’authentification unique sur expérience tooyour les utilisateurs Active Directory, consultez hello suivantes : 

- [PingFederate 6.11](http://go.microsoft.com/fwlink/?LinkID=266321)
- [PingFederate 7.2](http://documentation.pingidentity.com/display/PF72/PingFederate+7.2)
- [PingFederate 8.x](http://documentation.pingidentity.com/display/PFS/SSO+to+Office+365+Introduction)

## <a name="radiantone-cfs-30"></a>RadiantOne CFS 3.0

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique : 

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |Aucun |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |Authentification Windows intégrée |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations sur RadiantOne CFS, consultez [RadiantOne CFS](http://www.radiantlogic.com/products/radiantone-cfs/).

## <a name="sailpoint-identitynow"></a>Sailpoint IdentityNow

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique :

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations, consultez [Sailpoint IdentityNow](https://www.sailpoint.com/idaas-identity-as-a-service-identitynow/).

## <a name="secureauth-idp-720"></a>SecureAuth IdP 7.2.0

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique : 

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |Aucun |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |Aucun |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucun |

Pour plus d’informations sur SecureAuth, consultez [SecureAuth IdP](http://go.microsoft.com/?linkid=9845293).














## <a name="signgo-53"></a>Sign&go 5.3

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique :

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |Contrats Kerberos pris en charge |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |Aucun |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucun |

Sign&go 5.3 prend en charge l’authentification Kerberos via la configuration d’un contrat Kerberos.  Pour obtenir une assistance avec cette configuration, contactez Ilex ou la vue guide d’installation de hello [Sign & go](http://www.ilex-international.com/docs/sign&go_wsfederation_en.pdf)

## <a name="softbank-technology-online-service-gate"></a>Portail du service en ligne SoftBank Technology

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique :

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations sur Online Service Gate de SoftBank Technology, consultez [Softbank](https://www.softbanktech.jp/service/list/osg-pro-ent/).

## <a name="vmware-workspace-one"></a>VMware Workspace One

Hello Voici la matrice de prise en charge de scénario de hello pour cette expérience d’authentification unique :

| Client | Support | Exceptions |
| --- | --- | --- |
| Clients web (p. ex., Exchange Web Access et SharePoint Online) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge |
| Applications clientes riches (p. ex., Lync, abonnement Office, CRM) |Pris en charge |L’authentification Windows intégrée n’est pas prise en charge |
| Clients de messagerie riches (p. ex., Outlook et ActiveSync) |Pris en charge |Aucune |

Pour plus d’informations, consultez [VMware Workspace One](http://www.vmware.com/pdf/vidm-office365-saml.pdf).

