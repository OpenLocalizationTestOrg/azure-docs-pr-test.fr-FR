---
title: "le Proxy d’Application d’aaaTroubleshoot | Documents Microsoft"
description: "Aborde comment tootroubleshoot les erreurs dans le Proxy d’Application Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 970caafb-40b8-483c-bb46-c8b032a4fb74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: d426708a2ee32da6674987b5794602ed984b06b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-proxy-problems-and-error-messages"></a>Résoudre les problèmes de proxy d’application et les messages d’erreur
Si les erreurs se produisent dans l’accès à une application publiée ou dans la publication d’applications, vérifiez hello suivant options toosee si le Proxy d’Application Microsoft Azure Active Directory fonctionne correctement :

* Windows hello ouvrez Services de la console et vérifiez que hello **Microsoft AAD Application Proxy Connector** service est activé et en cours d’exécution. Vous pouvez également toolook à la page de propriétés de service de Proxy d’Application de hello, comme indiqué dans hello suivant image :  
  ![Capture d’écran de la fenêtre Propriétés du connecteur de proxy d’application Microsoft AAD](./media/active-directory-application-proxy-troubleshoot/connectorproperties.png)
* Ouvrez l’Observateur d’événements et recherchez les événements du proxy d’application sous **Journaux des applications et des services** > **Microsoft** > **AadApplicationProxy** > **Connecteur** > **Admin**.
* Si nécessaire, des journaux plus détaillés sont disponibles par [sous tension hello des journaux de session du connecteur Proxy d’Application](application-proxy-understand-connectors.md#under-the-hood).

Pour plus d’informations sur l’outil de résolution des problèmes de hello Azure AD, consultez [résolution des problèmes de configuration requise réseau outil toovalidate](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/03/troubleshooting-tool-to-validate-connector-networking-prerequisites).

## <a name="hello-page-is-not-rendered-correctly"></a>page de Hello n’est pas rendu correctement
Vous pouvez rencontrer des problèmes d’affichage ou de fonctionnement de votre application sans recevoir de message d’erreur spécifique. Cela peut se produire si vous avez publié le chemin d’accès de l’article hello, mais application hello requiert le contenu qui existe en dehors de ce chemin d’accès.

Par exemple, si vous publiez hello chemin d’accès https://yourapp/app mais application hello appelle des images dans https://yourapp/media, elles ne sont pas rendues. Assurez-vous que vous publiez l’application hello utilisant hello plus haut niveau chemin d’accès tooinclude tout le contenu approprié. Dans le présent exemple, ce serait http://yourapp/.

Si vous modifiez votre contenu tooinclude référencé de chemin d’accès, mais vous devez tooland les utilisateurs sur un lien plus approfondie dans le chemin d’accès de hello, consultez hello billet de blog [lien de droite paramètre hello pour les applications du Proxy d’Application dans le volet d’accès hello Azure AD et les applications Office 365 Lanceur de](https://blogs.technet.microsoft.com/applicationproxyblog/2016/04/06/setting-the-right-link-for-application-proxy-applications-in-the-azure-ad-access-panel-and-office-365-app-launcher/).

## <a name="connector-errors"></a>Erreurs de connecteur

Hello d’utilisation [Azure AD Application Proxy Connector Ports Test outil](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que votre connecteur pouvez contacter le service de Proxy d’Application hello. Au minimum, assurez-vous que toutes les coches vertes la région du centre des États-Unis hello et tooyou le plus proche de la région de hello. En outre, un nombre plus élevé de coches vertes signifie une résilience accrue. 

Si l’inscription échoue pendant l’installation de l’Assistant Connecteur de hello, il existe deux façons raison hello tooview Échec de hello. Une recherche dans le journal des événements hello sous **Applications et Services Logs\Microsoft\AadApplicationProxy\Connector\Admin**, ou exécution hello suivant de commande Windows PowerShell :

    Get-EventLog application –source “Microsoft AAD Application Proxy Connector” –EntryType “Error” –Newest 1

Une fois que vous trouvez hello connecteur erreur du journal des événements hello, utilisez cette table de problème de hello de tooresolve erreurs courantes :

| Error | Étapes recommandées |
| ----- | ----------------- |
| Échoué de l’inscription du connecteur : Assurez-vous que vous avez activé le Proxy d’Application Bonjour portail de gestion Azure et que vous avez entré votre nom d’utilisateur Active Directory et le mot de passe correctement. Erreur : « Une ou plusieurs erreurs se sont produites. » | Si vous avez fermé la fenêtre de l’inscription de hello sans vous connecter tooAzure AD, réexécutez l’Assistant Connecteur de hello et inscrire hello connecteur. <br><br> Si la fenêtre d’inscription de hello s’ouvre et se ferme immédiatement sans vous autoriser toolog dans, vous obtiendrez probablement cette erreur. Cette erreur se produit quand il existe une erreur réseau sur votre système. Assurez-vous qu’il est possible de tooconnect à partir d’un site Web public de tooa de navigateur et que les ports de hello sont ouverts comme spécifié dans [conditions préalables du Proxy d’Application](active-directory-application-proxy-enable.md). |
| Erreur claire est présentée dans la fenêtre d’inscription de hello. Impossible de poursuivre | Si vous recevez cette erreur, et puis fenêtre hello se ferme, vous avez entré hello les nom d’utilisateur incorrect ou le mot de passe. Réessayez. |
| Échoué de l’inscription du connecteur : Assurez-vous que vous avez activé le Proxy d’Application Bonjour portail de gestion Azure et que vous avez entré votre nom d’utilisateur Active Directory et le mot de passe correctement. Erreur : ' AADSTS50059 : aucune information d’identification de client trouvé dans la demande soit hello ou impliquée par des fourni les informations d’identification et de recherche par service URI principal a échoué. | Vous essayez de toosign à l’aide d’un Account Microsoft et non à un domaine qui fait partie de l’ID d’organisation hello du répertoire de hello vous essayez de tooaccess. Assurez-vous que hello administrateur fait partie de hello même nom de domaine comme domaine du locataire hello, par exemple, si le domaine hello Azure AD est contoso.com, hello admin doit être admin@contoso.com. |
| Échec de la stratégie en cours d’exécution tooretrieve hello pour l’exécution de scripts PowerShell. | Si hello installation du connecteur échoue, vérifiez toomake assurer que la stratégie d’exécution PowerShell n’est pas désactivé. <br><br>1. Ouvrez hello éditeur de stratégie de groupe.<br>2. Accédez trop**Configuration ordinateur** > **modèles d’administration** > **composants Windows**  >   **Windows PowerShell** et double-cliquez sur **Turn on Script Execution**.<br>3. stratégie d’exécution hello peut être définie tooeither **pas configuré** ou **activé**. Si défini trop**activé**, assurez-vous que sous Options, hello stratégie d’exécution a la valeur tooeither **autoriser les scripts locaux et les scripts signés à distance** ou trop**autoriser tous les scripts**. |
| Échec de la configuration de hello toodownload connecteur. | certificat client du connecteur Hello, qui est utilisé pour l’authentification, a expiré. Cela peut également se produire si vous avez hello que connecteur installé derrière un proxy. Dans ce cas, hello connecteur ne peut pas accéder à Internet de hello et ne sera pas en mesure de tooprovide applications tooremote utilisateurs. Renouvelez l’approbation manuellement à l’aide de hello `Register-AppProxyConnector` applet de commande dans Windows PowerShell. Si votre connecteur est derrière un proxy, il est nécessaire de toogrant toohello connecteur comptes Internet « services réseau » et « système local ». Cela peut être accompli en accordant les accès toohello Proxy soit en définissant les toobypass hello proxy. |
| Échoué de l’inscription du connecteur : Vérifiez que vous êtes un administrateur Global de votre hello de tooregister connecteur Active Directory. Erreur : « la demande d’inscription hello a été refusée. » | alias Hello que vous essayez de toolog à l’aide n’est pas un administrateur de ce domaine. Votre connecteur est toujours installé pour le répertoire hello qui possède le domaine de l’utilisateur hello. Assurez-vous que compte d’administrateur hello avec que vous essayez de toosign a client toohello Azure AD d’autorisations globales. |

## <a name="kerberos-errors"></a>Erreurs Kerberos

Ce tableau présente les plus courants de hello les erreurs qui proviennent de Kerberos le programme d’installation et la configuration et inclut des suggestions de résolution.

| Error | Étapes recommandées |
| ----- | ----------------- |
| Échec de la stratégie en cours d’exécution tooretrieve hello pour l’exécution de scripts PowerShell. | Si hello installation du connecteur échoue, vérifiez toomake assurer que la stratégie d’exécution PowerShell n’est pas désactivé.<br><br>1. Ouvrez hello éditeur de stratégie de groupe.<br>2. Accédez trop**Configuration ordinateur** > **modèles d’administration** > **composants Windows**  >   **Windows PowerShell** et double-cliquez sur **Turn on Script Execution**.<br>3. stratégie d’exécution hello peut être définie tooeither **pas configuré** ou **activé**. Si défini trop**activé**, assurez-vous que sous Options, hello stratégie d’exécution a la valeur tooeither **autoriser les scripts locaux et les scripts signés à distance** ou trop**autoriser tous les scripts**. |
| 12008 - azure AD dépassé hello nombre maximal de l’authentification Kerberos autorisée tentatives toohello du serveur principal. | Cette erreur peut indiquer une configuration incorrecte entre Azure AD et hello principal serveur d’applications, ou un problème de configuration de date et l’heure sur les deux ordinateurs. serveur principal de Hello a refusé de ticket Kerberos de hello créée par Azure AD. Vérifiez qu’Azure AD et le serveur d’applications principal hello sont configurés correctement. Assurez-vous que la configuration de date et heure hello sur hello Azure AD et serveur d’applications principal hello sont synchronisées. |
| 13016 - azure AD ne peut pas récupérer de ticket Kerberos pour le compte d’utilisateur de hello étant donné qu’aucun UPN dans edge de hello jeton ou cookie d’accès hello. | Il existe un problème de configuration de STS hello. Corrigez hello revendication UPN configuration Bonjour STS. |
| 13019 - azure AD ne peut pas récupérer de ticket Kerberos pour le compte d’utilisateur de hello en raison de hello erreur d’API générale suivante. | Cet événement peut indiquer une configuration incorrecte entre Azure AD et serveur de contrôleur de domaine hello ou un problème de configuration de date et l’heure sur les deux ordinateurs. contrôleur de domaine Hello refusé le ticket Kerberos de hello créée par Azure AD. Vérifiez qu’Azure AD et serveur d’applications principal hello sont correctement configurés, particulièrement hello nom principal de service configuration. Vérifiez que hello Azure AD est joint à un domaine toohello même domaine que hello tooensure de contrôleur de domaine qui hello du contrôleur de domaine établit la relation d’approbation avec Azure AD. Assurez-vous que la configuration de date et heure hello sur hello Azure AD et contrôleur de domaine hello sont synchronisées. |
| 13020 - azure AD ne peut pas récupérer de ticket Kerberos pour le compte d’utilisateur de hello, car le SPN du serveur principal hello n’est pas défini. | Cet événement peut indiquer une configuration incorrecte entre Azure AD et serveur de contrôleur de domaine hello ou un problème de configuration de date et l’heure sur les deux ordinateurs. contrôleur de domaine Hello refusé le ticket Kerberos de hello créée par Azure AD. Vérifiez qu’Azure AD et serveur d’applications principal hello sont correctement configurés, particulièrement hello nom principal de service configuration. Vérifiez que hello Azure AD est joint à un domaine toohello même domaine que hello tooensure de contrôleur de domaine qui hello du contrôleur de domaine établit la relation d’approbation avec Azure AD. Assurez-vous que la configuration de date et heure hello sur hello Azure AD et contrôleur de domaine hello sont synchronisées. |
| 13022 - azure AD ne peut pas authentifier l’utilisateur de hello, car le serveur principal de hello répond tooKerberos les tentatives d’authentification avec une erreur HTTP 401. | Cet événement peut indiquer une configuration incorrecte entre Azure AD et hello principal serveur d’applications, ou un problème de configuration de date et l’heure sur les deux ordinateurs. serveur principal de Hello a refusé de ticket Kerberos de hello créée par Azure AD. Vérifiez qu’Azure AD et le serveur d’applications principal hello sont configurés correctement. Assurez-vous que la configuration de date et heure hello sur hello Azure AD et serveur d’applications principal hello sont synchronisées. |

## <a name="end-user-errors"></a>Erreurs de l’utilisateur final

Cette liste couvre les erreurs que vos utilisateurs finaux peuvent rencontrer quand ils essayez tooaccess hello application échouent. 

| Error | Étapes recommandées |
| ----- | ----------------- |
| site Web de Hello ne peut pas afficher la page de hello. | Votre utilisateur peut obtenir cette erreur lors de la tentative d’application de hello tooaccess que vous avez publiée si l’application hello est une application IWA. Hello défini SPN pour cette application peut être incorrecte. Pour les applications IWA, assurez-vous que ce nom principal de service configuré pour cette application hello est correct. |
| site Web de Hello ne peut pas afficher la page de hello. | Votre utilisateur peut obtenir cette erreur lors de la tentative d’application de hello tooaccess que vous avez publiée si l’application hello est une application OWA. Cela peut être dû à hello suivantes :<br><li>Hello défini SPN pour cette application est incorrecte. Assurez-vous que ce nom principal de service configuré pour cette application hello est correct.</li><li>utilisateur Hello qui a tenté d’application de hello tooaccess utilise un compte Microsoft plutôt que hello toosign compte d’entreprise approprié dans ou hello utilisateur est un utilisateur invité. Vérifiez que hello utilisateur se connecte en utilisant son compte d’entreprise que les correspondances hello domaine Hello publié l’application. Les utilisateurs d’un compte Microsoft et les invités ne peuvent pas accéder aux applications avec l’authentification Windows intégrée.</li><li>utilisateur Hello qui a tenté d’application de hello tooaccess n’est pas correctement défini pour cette application sur le côté local de hello. Assurez-vous que cet utilisateur dispose des autorisations appropriées hello tel que défini pour cette application principale sur l’ordinateur local de hello. |
| Cette application d’entreprise n’est pas accessible. Vous ne sont pas autorisés tooaccess cette application. Échec de l’autorisation. Assurez-vous que l’utilisateur tooassign hello avec application toothis d’accès. | Les utilisateurs peuvent obtenir cette erreur lors de la tentative d’application de hello tooaccess dans que vous avez publiée s’ils utilisent les comptes Microsoft au lieu de leur toosign compte d’entreprise. Les utilisateurs invités peuvent également obtenir cette erreur. Les utilisateurs d’un compte Microsoft et les invités ne peuvent pas accéder aux applications avec l’authentification Windows intégrée. Vérifiez que hello utilisateur se connecte en utilisant son compte d’entreprise que les correspondances hello domaine Hello publié l’application.<br><br>Vous n’avez ne peut-être pas affecté utilisateur hello pour cette application. Accédez toohello **Application** onglet et sous **utilisateurs et groupes**, affectez cet utilisateur ou une application toothis de groupe utilisateur. |
| Cette application d’entreprise n’est pas accessible pour l’instant. Réessayez plus tard... connecteur hello a expiré. | Les utilisateurs peuvent obtenir cette erreur lors de la tentative d’application de hello tooaccess que vous avez publiée s’ils ne sont pas définis correctement pour cette application sur le côté local de hello. Assurez-vous que les utilisateurs disposent des autorisations appropriées de hello tel que défini pour cette application principale sur l’ordinateur local de hello. |
| Cette application d’entreprise n’est pas accessible. Vous ne sont pas autorisés tooaccess cette application. Échec de l’autorisation. Assurez-vous que l’utilisateur hello possède une licence pour Azure Active Directory Premium ou Basic. | Les utilisateurs peuvent obtenir cette erreur lors de la tentative d’application de hello tooaccess que vous avez publiée s’ils n’ont pas été explicitement affectées avec une licence de base/Premium par l’administrateur de l’abonné hello. Accédez Active Directory de l’abonné toohello **licences** onglet et vous assurer que cet utilisateur ou ce groupe d’utilisateurs est attribué une licence Premium ou Basic. |

## <a name="my-error-wasnt-listed-here"></a>Mon erreur n’était pas répertoriée ici

Si vous rencontrez une erreur ou un problème avec le Proxy d’Application Azure AD qui n’est pas répertorié dans ce guide de dépannage, nous aimerions toohear à son sujet. Envoyer un courrier électronique tooour [équipe de commentaires](mailto:aadapfeedback@microsoft.com) avec les détails de hello de hello erreur vous s’est produite.

## <a name="see-also"></a>Voir aussi
* [Activation du proxy d’application Azure AD](active-directory-application-proxy-enable.md)
* [Publiez des applications avec le proxy d’application](active-directory-application-proxy-publish.md)
* [Activer l’authentification unique](active-directory-application-proxy-sso-using-kcd.md)
* [Activer l’accès conditionnel](active-directory-application-proxy-conditional-access.md)


<!--Image references-->
[1]: ./media/active-directory-application-proxy-troubleshoot/connectorproperties.png
[2]: ./media/active-directory-application-proxy-troubleshoot/sessionlog.png
