---
title: "Azure AD Connect : Résoudre les problèmes de connectivité | Microsoft Docs"
description: "Explique comment des erreurs de connectivité de tootroubleshoot avec Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 3aa41bb5-6fcb-49da-9747-e7a3bd780e64
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 60d6b7c4ad8a3ab907c20e598ec9443f115df287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connectivity-issues-with-azure-ad-connect"></a>Résoudre les problèmes de connectivité liés à Azure AD Connect
Cet article explique le fonctionne de la connectivité entre Azure AD Connect et Azure AD et comment les problèmes de connectivité de tootroubleshoot. Ces problèmes sont probablement toobe vu dans un environnement avec un serveur proxy.

## <a name="troubleshoot-connectivity-issues-in-hello-installation-wizard"></a>Résoudre les problèmes de connectivité dans l’Assistant installation Bonjour
Azure AD Connect est à l’aide de l’authentification moderne (à l’aide de la bibliothèque ADAL de hello) pour l’authentification. l’Assistant installation Hello et le moteur de synchronisation hello approprié nécessitent toobe machine.config correctement configuré, car ces deux est des applications .NET.

Dans cet article, nous montrons comment Fabrikam connecte tooAzure AD via son proxy. serveur de proxy Hello est nommé fabrikamproxy et utilise le port 8080.

Nous devons toomake vraiment [ **machine.config** ](active-directory-aadconnect-prerequisites.md#connectivity) est correctement configuré.  
![machineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/machineconfig.png)

> [!NOTE]
> Dans certains blogs non Microsoft, il est documenté que les modifications doivent être apportées toomiiserver.exe.config à la place. Toutefois, ce fichier est remplacé à chaque mise à niveau même si elle fonctionne pendant l’installation initiale, système de hello cesse de fonctionner sur la première mise à niveau. Pour cette raison, hello est recommandé tooupdate machine.config à la place.
>
>

serveur de proxy Hello doit également disposer des URL hello requis ouverts. liste officielle de Hello est documenté dans [plages d’adresses IP et des URL d’Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

De ces URL, hello tableau suivant est hello toobe minimale de bare absolu en mesure de tooconnect tooAzure AD. Cette liste n’inclut pas de fonctionnalités facultatives, comme la réécriture du mot de passe ou Azure AD Connect Health. Il est documenté toohelp ici dans la résolution des problèmes pour la configuration initiale hello.

| URL | Port | Description |
| --- | --- | --- |
| mscrl.microsoft.com |HTTP/80 |Répertorie les toodownload utilisé CRL. |
| \*.verisign.com |HTTP/80 |Répertorie les toodownload utilisé CRL. |
| \*.entrust.com |HTTP/80 |Répertorie les CRL toodownload utilisé pour l’authentification Multifacteur. |
| \*.windows.net |HTTPS/443 |Toosign utilisé dans tooAzure AD. |
| secure.aadcdn.microsoftonline-p.com |HTTPS/443 |Utilisé pour MFA. |
| \**.microsoftonline.com |HTTPS/443 |Utilisé tooconfigure vos données d’importation/exportation et d’annuaire Azure AD. |

## <a name="errors-in-hello-wizard"></a>Erreurs dans l’Assistant de hello
l’Assistant installation Bonjour à l’aide de deux différents contextes de sécurité. Sur la page de hello **connecter tooAzure AD**, il est à l’aide de hello utilisateur actuellement connecté. Sur la page de hello **configurer**, il change toohello [compte exécutant le service hello pour le moteur de synchronisation hello](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account). S’il existe un problème, il apparaît probablement déjà au niveau de hello **connecter tooAzure AD** page Assistant hello étant donné que la configuration du proxy hello est globale.

Hello suivants est des erreurs les plus courantes de hello que vous pouvez rencontrer dans l’Assistant installation hello.

### <a name="hello-installation-wizard-has-not-been-correctly-configured"></a>l’Assistant installation Hello n’a pas été configuré correctement
Cette erreur apparaît lorsque l’Assistant hello lui-même ne peut pas atteindre le proxy de hello.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomachineconfig.png)

* Si vous voyez cette erreur, vérifiez que hello [machine.config](active-directory-aadconnect-prerequisites.md#connectivity) a été correctement configuré.
* Si qui semble correcte, suivez les étapes de hello dans [vérifier la connectivité de proxy](#verify-proxy-connectivity) toosee si le problème de hello se produit en dehors de l’Assistant hello également.

### <a name="a-microsoft-account-is-used"></a>Un compte Microsoft est utilisé
Si vous utilisez un **compte Microsoft** au lieu d’un compte **scolaire ou d’organisation**, vous voyez une erreur générique.  
![Un compte Microsoft est utilisé](./media/active-directory-aadconnect-troubleshoot-connectivity/unknownerror.png)

### <a name="hello-mfa-endpoint-cannot-be-reached"></a>point de terminaison de l’authentification Multifacteur Hello ne peut pas être atteint.
Cette erreur apparaît si hello point de terminaison **https://secure.aadcdn.microsoftonline-p.com** ne peut pas être atteint et votre administrateur général a l’authentification Multifacteur activée.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomicrosoftonlinep.png)

* Si vous voyez cette erreur, vérifiez ce point de terminaison hello **secure.aadcdn.microsoftonline-p.com** a été ajouté toohello proxy.

### <a name="hello-password-cannot-be-verified"></a>mot de passe Hello ne peut pas être vérifiée.
Si l’Assistant installation hello a réussi à se connecter tooAzure AD, mais hello mot de passe ne peut pas être vérifié que vous voyez cette erreur :  
![badpassword](./media/active-directory-aadconnect-troubleshoot-connectivity/badpassword.png)

* Est un mot de passe hello un mot de passe temporaire et doit être modifié ? Est il hello réellement mot de passe correct ? Essayez toosign dans toohttps://login.microsoftonline.com (sur un autre ordinateur que le serveur d’Azure AD Connect hello) et vérifiez le compte de hello est utilisable.

### <a name="verify-proxy-connectivity"></a>Vérifier la connectivité du proxy
tooverify si hello Azure AD Connect serveur dispose d’une connectivité réelle avec hello Proxy et Internet, utilisez certains toosee PowerShell si le proxy de hello autorise les demandes web ou non. À une invite PowerShell, exécutez `Invoke-WebRequest -Uri https://adminwebservice.microsoftonline.com/ProvisioningService.svc`. (Techniquement hello premier appel est toohttps://login.microsoftonline.com et cet URI fonctionne également, mais hello autres URI est toorespond plus rapide.)

PowerShell utilise la configuration de hello dans le proxy de machine.config toocontact hello. paramètres Hello dans winhttp/netsh ne devraient pas affecter ces applets de commande.

Si hello proxy est correctement configuré, vous devez obtenir un état de réussite : ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest200.png)

Si vous recevez **toohello tooconnect impossible à distance**, puis PowerShell tente un appel direct de toomake sans utiliser de proxy de hello ou DNS n’est pas correctement configuré. Vérifiez que hello **machine.config** fichier est correctement configuré.
![unabletoconnect](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequestunable.png)

Si le proxy de hello n’est pas correctement configuré, vous obtenez une erreur : ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest403.png)
![proxy407](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest407.png)

| Error | Texte d’erreur | Commentaire |
| --- | --- | --- |
| 403 |Interdit |proxy de Hello n’a pas été ouvert pour l’URL demandée de hello. Revoir la configuration du proxy hello et vérifiez que hello [URL](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) ont été ouverts. |
| 407 |Authentification proxy requise |serveur de proxy Hello requis une sign-in et aucun n’a été fourni. Si votre serveur proxy requiert une authentification, assurez-vous que toohave ce paramètre configuré dans le fichier machine.config de hello. Assurez-vous également que vous utilisez des comptes de domaine pour l’utilisateur hello exécutant l’Assistant de hello et pour le compte de service hello. |

## <a name="hello-communication-pattern-between-azure-ad-connect-and-azure-ad"></a>modèle de communication Hello entre Azure AD Connect et Azure AD
Si vous avez suivi l’ensemble des étapes précédentes et que vous ne pouvez toujours pas vous connecter, vous pouvez commencer à examiner les journaux du réseau. Cette section documente un modèle de connectivité réussi et normal. Il est également liste harengs rouge courantes qui peuvent être ignorées lors de la lecture des journaux de réseau hello.

* Il existe des appels toohttps://dc.services.visualstudio.com. Il n’est pas requis toohave que cette URL à ouvrir dans le proxy hello pour hello installation toosucceed et ces appels peut être ignorée.
* Vous consultez que la résolution dns répertorie toobe d’hôtes réel hello dans hello DNS nom espace nsatc.net et d’autres espaces de noms pas sous microsoftonline.com. Toutefois, il n’y a pas toutes les demandes de service web sur les noms de serveur réel hello et vous n’avez pas tooadd ces proxy toohello d’URL.
* provisioningapi adminwebservice de points de terminaison hello sont des points de terminaison de découverte et utilisé toouse de point de terminaison réel toofind hello. Ces points de terminaison diffèrent selon votre région.

### <a name="reference-proxy-logs"></a>Journaux de proxy de référence
Voici un vidage sur un proxy réel journal et hello page Assistant installation à partir de laquelle il a été effectuée (toohello entrées en double même point de terminaison ont été supprimés). Cette section peut être utilisée comme référence pour vos propres journaux de proxy et de réseau. points de terminaison Hello réelle peuvent être différentes dans votre environnement (en particulier les URL dans *italique*).

**Se connecter tooAzure AD**

| Temps | URL |
| --- | --- |
| 11/01/2016 8:31 |connect://login.microsoftonline.com:443 |
| 11/01/2016 8:31 |connect://adminwebservice.microsoftonline.com:443 |
| 11/01/2016 8:32 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 11/01/2016 8:32 |connect://login.microsoftonline.com:443 |
| 11/01/2016 8:33 |connect://provisioningapi.microsoftonline.com:443 |
| 11/01/2016 8:33 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**Configurer**

| Time | URL |
| --- | --- |
| 11/01/2016 8:43 |connect://login.microsoftonline.com:443 |
| 11/01/2016 8:43 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 11/01/2016 8:43 |connect://login.microsoftonline.com:443 |
| 11/01/2016 8:44 |connect://adminwebservice.microsoftonline.com:443 |
| 11/01/2016 8:44 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 11/01/2016 8:44 |connect://login.microsoftonline.com:443 |
| 11/01/2016 8:44 |connect://adminwebservice.microsoftonline.com:443 |
| 11/01/2016 8:44 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 11/01/2016 8:44 |connect://login.microsoftonline.com:443 |
| 11/01/2016 8:46 |connect://provisioningapi.microsoftonline.com:443 |
| 11/01/2016 8:46 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**Synchronisation initiale**

| Time | URL |
| --- | --- |
| 11/01/2016 8:48 |connect://login.windows.net:443 |
| 11/01/2016 8:49 |connect://adminwebservice.microsoftonline.com:443 |
| 11/01/2016 8:49 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 11/01/2016 8:49 |connect://*bba800-anchor*.microsoftonline.com:443 |

## <a name="authentication-errors"></a>Erreurs d’authentification
Cette section décrit les erreurs qui peuvent être retournées à partir de la bibliothèque ADAL (bibliothèque d’authentification hello utilisé par Azure AD Connect) et PowerShell. erreur Hello expliqué doit vous aider dans les étapes suivantes.

### <a name="invalid-grant"></a>Licence non valide
Nom d’utilisateur ou mot de passe non valide. Pour plus d’informations, consultez [Impossible de vérifier le mot de passe hello](#the-password-cannot-be-verified).

### <a name="unknown-user-type"></a>Type d’utilisateur inconnu
Votre annuaire Azure AD est introuvable ou n’a pas pu être résolu. Vous essayez peut-être de toologin avec un nom d’utilisateur dans un domaine non vérifié ?

### <a name="user-realm-discovery-failed"></a>Échec de la découverte de domaine d’utilisateur
Problèmes de configuration du réseau ou du proxy. réseau de Hello ne peut pas être atteint. Consultez [résoudre les problèmes de connectivité dans l’Assistant installation hello](#troubleshoot-connectivity-issues-in-the-installation-wizard).

### <a name="user-password-expired"></a>Mot de passe utilisateur expiré
Vos informations d’identification ont expiré. Modifiez votre mot de passe.

### <a name="authorizationfailure"></a>AuthorizationFailure
Problème inconnu.

### <a name="authentication-cancelled"></a>Authentification annulée
vérification de l’authentification multifacteur (MFA) Hello a été annulée.

### <a name="connecttomsonline"></a>ConnectToMSOnline
L’authentification a réussi, mais Azure AD PowerShell a un problème d’authentification.

### <a name="azurerolemissing"></a>AzureRoleMissing
L’authentification a réussi. Vous n’êtes pas administrateur global.

### <a name="privilegedidentitymanagement"></a>PrivilegedIdentityManagement
L’authentification a réussi. Privileged Identity Management a été activé et vous n’êtes actuellement pas administrateur global. Pour plus d’informations, consultez [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

### <a name="companyinfounavailable"></a>CompanyInfoUnavailable
L’authentification a réussi. Impossible de récupérer les informations de société à partir d’Azure AD.

### <a name="retrievedomains"></a>RetrieveDomains
L’authentification a réussi. Impossible de récupérer les informations de domaine à partir d’Azure AD.

### <a name="unexpected-exception"></a>Exception inattendue
Une erreur inattendue dans l’Assistant installation hello indiquées. Peut se produire si vous essayez de toouse un **Account Microsoft** plutôt qu’un **compte scolaire ou de l’organisation**.

## <a name="troubleshooting-steps-for-previous-releases"></a>Étapes de dépannage pour les versions précédentes.
Avec les versions en commençant par le numéro de build 1.1.105.0 (publiée février 2016), hello-assistant de connexion a été mis hors service. Configuration de cette section et hello ne doit plus être requise, mais est conservée en tant que référence.

Pour les hello unique dans l’assistant toowork, winhttp doit être configuré. Cette configuration peut être effectuée avec [**netsh**](active-directory-aadconnect-prerequisites.md#connectivity).  
![netsh](./media/active-directory-aadconnect-troubleshoot-connectivity/netsh.png)

### <a name="hello-sign-in-assistant-has-not-been-correctly-configured"></a>assistant de connexion Hello n’a pas été configuré correctement
Cette erreur apparaît lorsque hello-assistant de connexion ne peut pas atteindre le proxy de hello ou de proxy de hello n’autorise pas de demande de hello.
![nonetsh](./media/active-directory-aadconnect-troubleshoot-connectivity/nonetsh.png)

* Si vous voyez cette erreur, consultez configuration du proxy hello dans [netsh](active-directory-aadconnect-prerequisites.md#connectivity) et vérifiez qu’elle est correcte.
  ![netshshow](./media/active-directory-aadconnect-troubleshoot-connectivity/netshshow.png)
* Si qui semble correcte, suivez les étapes de hello dans [vérifier la connectivité de proxy](#verify-proxy-connectivity) toosee si le problème de hello se produit en dehors de l’Assistant hello également.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
