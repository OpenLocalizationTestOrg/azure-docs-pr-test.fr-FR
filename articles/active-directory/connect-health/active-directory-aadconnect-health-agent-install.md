---
title: "installation de se connecter l’Agent d’intégrité aaaAzure AD | Documents Microsoft"
description: "Il s’agit de page Azure AD Connect Health hello qui décrit l’installation de l’agent hello pour AD FS et de synchronisation."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 1cc8ae90-607d-4925-9c30-6770a4bd1b4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9019628ec1d4c477496e08910cfd668ed1933a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-agent-installation"></a>Installation de l'agent Azure AD Connect Health
Ce document vous guide dans l’installation et configuration des Agents d’intégrité de se connecter hello Azure AD. Vous pouvez télécharger les agents hello [ici](active-directory-aadconnect-health.md#download-and-install-azure-ad-connect-health-agent).

## <a name="requirements"></a>Configuration requise
Hello tableau suivant est une liste de conditions requises pour utiliser Azure AD Connect Health.

| Prérequis | Description |
| --- | --- |
| Azure AD Premium |Azure AD Connect Health est une fonctionnalité d’Azure AD Premium qui nécessite Azure AD Premium. </br></br>Pour plus d'informations, consultez la section [Prise en main d’Azure AD Premium](../active-directory-get-started-premium.md) </br>toostart une version d’évaluation gratuite de 30 jours, consultez [démarrer une version d’évaluation.](https://azure.microsoft.com/trial/get-started-active-directory/) |
| Vous devez être un global administrateur de votre tooget Azure AD en main Azure AD Connect Health |Par défaut, les seuls les administrateurs généraux de hello peuvent installer et configurer hello intégrité agents tooget démarré, portail hello d’accès et effectuer toutes les opérations dans Azure AD Connect Health. Pour plus d’informations, consultez l’article [Administration de votre annuaire Azure AD](../active-directory-administer.md). <br><br> À l’aide du contrôle d’accès basé sur rôle permet l’accès tooAzure AD Connect Health tooother aux utilisateurs de votre organisation. Pour plus d’informations, consultez [Contrôle d’accès en fonction du rôle pour Azure AD Connect Health.](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) </br></br>**Important :** hello compte utilisé lors de l’installation des agents de hello doit être un compte professionnel ou scolaire. Il ne peut pas s’agir d’un compte Microsoft. Pour plus d’informations, consultez [Inscription à Azure en tant qu’organisation](../sign-up-organization.md) |
| L’agent Azure AD Connect Health est installé sur chaque serveur cible | Azure AD Connect Health nécessite hello Agents d’intégrité toobe installé et configuré sur les données de serveurs cibles tooreceive hello et fournit des fonctionnalités de surveillance et Analytique hello </br></br>Par exemple, les données tooget à partir de votre infrastructure AD FS, l’agent de hello doivent être installées sur hello AD FS et des serveurs Proxy d’Application Web. De même, les données de tooget dans votre environnement local infrastructure de domaine Active Directory, l’agent de hello doit être installé sur les contrôleurs de domaine hello. </br></br> |
| Points de terminaison de connexion sortante toohello service Azure | Pendant l’installation et l’exécution, l’agent d’hello requiert des points de terminaison de connectivité tooAzure AD Connect Health service. Si la connectivité sortante est bloquée à l’aide de pare-feu, vérifiez que hello suivant les points de terminaison sont ajoutés toohello liste autorisée : </br></br><li>&#42;.blob.core.windows.net </li><li>&#42;.servicebus.windows.net - Port: 5671 </li><li>&#42;.adhybridhealth.azure.com/</li><li>https://management.azure.com </li><li>https://policykeyservice.dc.ad.msft.net/</li><li>https://login.windows.net</li><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li> |
|Connectivité sortante basée sur des adresses IP | Pour l’adresse IP adresse en fonction de filtrage sur les pare-feu, consultez toohello [plages d’adresses IP Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653).|
| L’inspection SSL pour le trafic sortant est filtrée ou désactivée | Hello agent opérations d’inscription étape ou les données de téléchargement peuvent échouer s’il existe inspection SSL ou arrêt pour le trafic sortant à la couche réseau hello. |
| Ports de pare-feu du serveur hello exécutant l’agent de hello. |l’agent Hello requiert hello suivant toobe ouvrir dans l’ordre pour toocommunicate d’agent hello avec les points de terminaison hello Azure AD Health service des ports de pare-feu.</br></br><li>Port TCP 443</li><li>Port TCP 5671</li> |
| Autoriser hello suivant des sites Web si la sécurité renforcée d’Internet Explorer est activée. |Si la sécurité renforcée d’Internet Explorer est activée, puis hello sites Web suivants doivent être autorisés sur serveur hello continu toohave hello agent est installé.</br></br><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li><li>https://login.windows.net</li><li>serveur de fédération Hello pour votre organisation approuvée par Azure Active Directory. Par exemple : https://sts.contoso.com</li> |
|Désactiver FIPS|FIPS n’est pas pris en charge par les agents Azure AD Connect Health.|

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-fs"></a>L’installation hello Agent Azure AD Connect Health pour AD FS
toostart hello d’installation de l’agent, double-cliquez sur le fichier .exe hello que vous avez téléchargé. Sur le premier écran de hello, cliquez sur Installer.

![Vérifier Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install1.png)

Une fois l’installation de hello est terminée, cliquez sur Configurer.

![Vérifier Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install2.png)

Cette opération lance un processus d’inscription de l’agent de hello PowerShell fenêtre tooinitiate. Lorsque vous y êtes invité, connectez-vous avec un compte Azure AD qui a l’enregistrement de l’agent tooperform accès. Par défaut hello compte d’administrateur général a accès.

![Vérifier Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install3.png)

Une fois que vous êtes connecté, PowerShell continue. Une fois terminée, vous pouvez fermer PowerShell et hello configuration est terminée.

À ce stade, hello agent services doivent être démarré automatiquement permettant hello agent téléchargement hello requis données toohello cloud service de manière sécurisée.

Si vous ne respectez pas tous les logiciels prérequis hello décrites dans les sections précédentes hello, avertissements apparaissent dans la fenêtre de PowerShell hello. Être vraiment toocomplete hello [exigences](active-directory-aadconnect-health-agent-install.md#requirements) avant d’installer l’agent de hello. Hello suivant capture d’écran est un exemple de ces erreurs.

![Vérifier Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install4.png)

tooverify hello agent a été installé, recherchez hello suivant des services sur le serveur de hello. Si vous terminé la configuration de hello, ils doivent déjà être en cours d’exécution. Dans le cas contraire, elles sont arrêtées jusqu'à ce que la configuration hello est terminée.

* Azure AD Connect Health AD FS Diagnostics Service
* Azure AD Connect Health AD FS Insights Service
* Azure AD Connect Health AD FS Monitoring Service

![Vérifier Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install5.png)

### <a name="agent-installation-on-windows-server-2008-r2-servers"></a>Installation de l’agent sur les serveurs Windows Server 2008 R2
Procédure pour les serveurs Windows Server 2008 R2 :

1. Assurez-vous que le serveur hello exécute au niveau de Service Pack 1 ou version ultérieure.
2. Désactivez la Configuration de sécurité renforcée pour l’installation de l’agent :
3. Installez Windows PowerShell 4.0 sur chacun des serveurs hello avant l’installation hello agent d’intégrité d’AD. tooinstall Windows PowerShell 4.0 :
   * Installer [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=40779) à l’aide de hello suivant le programme d’installation hors connexion de lien toodownload hello.
   * Installer PowerShell ISE (à partir des fonctionnalités de Windows)
   * Installer hello [Windows Management Framework 4.0.](https://www.microsoft.com/download/details.aspx?id=40855)
   * Installez Internet Explorer version 10 ou version ultérieure sur le serveur de hello. (Requis par hello Service d’intégrité tooauthenticate, à l’aide de vos informations d’identification d’administrateur Azure).
4. Pour plus d’informations sur l’installation de Windows PowerShell 4.0 sur Windows Server 2008 R2, consultez l’article de wiki hello [ici](http://social.technet.microsoft.com/wiki/contents/articles/20623.step-by-step-upgrading-the-powershell-version-4-on-2008-r2.aspx).

### <a name="enable-auditing-for-ad-fs"></a>Activer l’audit pour AD FS
> [!NOTE]
> Cette section s’applique uniquement à des serveurs de tooAD FS. Vous n’avez pas de le toofollow ces étapes sur les serveurs de Proxy d’Application hello Web.
>

Dans l’ordre pour hello Analytique de l’utilisation des fonctionnalités toogather et analyser les données, hello agent Azure AD Connect Health a besoin hello informations dans les journaux d’Audit de hello AD FS. Ces journaux ne sont pas activés par défaut. Hello utilisation suivant l’audit de procédures tooenable AD FS et toolocate hello AD FS, journaux, sur vos serveurs AD FS d’audit.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2008-r2"></a>tooenable l’audit pour AD FS sur Windows Server 2008 R2
1. Cliquez sur **Démarrer**, pointez trop**programmes**, pointez trop**outils d’administration**, puis cliquez sur **stratégie de sécurité locale**.
2. Accédez toohello **Security Settings\Local Policies\User Rights Management** dossier, puis double-cliquez sur Générer des audits de sécurité.
3. Sur hello **paramètre de sécurité locale** , vérifiez que le compte de service hello AD FS 2.0 est répertorié. Si elle n’est pas présente, cliquez sur **ajouter un utilisateur ou groupe** et ajoutez-le toohello liste, puis cliquez sur **OK**.
4. tooenable l’audit, ouvrez une invite de commandes avec des privilèges élevés et exécutez hello de commande suivante :<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable</code>
5. Fermez la stratégie de sécurité locale, puis ouvrez le composant logiciel enfichable Gestion des hello. hello tooopen le composant logiciel enfichable Gestion, cliquez sur **Démarrer**, pointez trop**programmes**, pointez trop**outils d’administration**, puis cliquez sur AD FS 2.0 Management.
6. Dans le volet Actions de hello, cliquez sur Modifier les propriétés de Service de fédération.
7. Bonjour **propriétés du Service de fédération** boîte de dialogue, cliquez sur hello **événements** onglet.
8. Sélectionnez hello **audits des succès** et **audits des échecs** cases à cocher.
9. Cliquez sur **OK**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2012-r2"></a>tooenable l’audit pour AD FS sur Windows Server 2012 R2
1. Ouvrez **stratégie de sécurité locale** en ouvrant **le Gestionnaire de serveur** sur l’écran d’accueil hello ou Gestionnaire de serveur dans la barre des tâches hello sur le bureau de hello, puis cliquez sur **outils/locales, stratégie de sécurité**.
2. Accédez toohello **Security Settings\Local Policies\User Rights Assignment** dossier, puis double-cliquez sur **générer des audits de sécurité**.
3. Sur hello **paramètre de sécurité locale** , vérifiez que le compte de service hello AD FS est répertorié. Si elle n’est pas présente, cliquez sur **ajouter un utilisateur ou groupe** et ajoutez-le toohello liste, puis cliquez sur **OK**.
4. tooenable l’audit, ouvrez une invite de commandes avec des privilèges élevés et exécutez hello de commande suivante : ```auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable```.
5. Fermer **stratégie de sécurité locale**, puis ouvrez hello **gestion AD FS** enfichable (dans le Gestionnaire de serveur, cliquez sur Outils, puis sélectionnez gestion AD FS).
6. Dans le volet Actions de hello, cliquez sur **modifier les propriétés de Service de fédération**.
7. Dans la boîte de dialogue Propriétés du Service de fédération hello, cliquez sur hello **événements** onglet.
8. Sélectionnez hello **audits des succès et les audits des échecs** cases à cocher, puis **OK**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2016"></a>tooenable l’audit pour AD FS sur Windows Server 2016
1. Ouvrez **stratégie de sécurité locale** en ouvrant **le Gestionnaire de serveur** sur l’écran d’accueil hello ou Gestionnaire de serveur dans la barre des tâches hello sur le bureau de hello, puis cliquez sur **outils/locales, stratégie de sécurité**.
2. Accédez toohello **Security Settings\Local Policies\User Rights Assignment** dossier, puis double-cliquez sur **générer des audits de sécurité**.
3. Sur hello **paramètre de sécurité locale** , vérifiez que le compte de service hello AD FS est répertorié. Si elle n’est pas présente, cliquez sur **ajouter un utilisateur ou groupe** et ajouter la liste toohello des comptes de service hello AD FS, puis cliquez sur **OK**.
4. tooenable l’audit, ouvrez une invite de commandes avec des privilèges élevés et exécutez hello de commande suivante :<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable.</code>
5. Fermer **stratégie de sécurité locale**, puis ouvrez hello **gestion AD FS** enfichable (dans le Gestionnaire de serveur, cliquez sur Outils, puis sélectionnez gestion AD FS).
6. Dans le volet Actions de hello, cliquez sur **modifier les propriétés de Service de fédération**.
7. Dans la boîte de dialogue Propriétés du Service de fédération hello, cliquez sur hello **événements** onglet.
8. Sélectionnez hello **audits des succès et les audits des échecs** cases à cocher, puis **OK**. Ceci doit être activé par défaut.
9. Ouvrez une fenêtre PowerShell et exécutez hello de commande suivante : ```Set-AdfsProperties -AuditLevel Verbose```.

Notez que le niveau d’audit « de base » est activé par défaut. En savoir plus sur hello [amélioration d’Audit de AD FS dans Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/auditing-enhancements-to-ad-fs-in-windows-server-2016)


#### <a name="toolocate-hello-ad-fs-audit-logs"></a>journaux d’audit de toolocate hello AD FS
1. Ouvrez l’ **Observateur d’événements**.
2. TooWindows journaux, sélectionnez **sécurité**.
3. Dans hello droit, cliquez sur **filtrer le journal actuel**.
4. Dans Source de l’événement, sélectionnez **Audit AD FS**.

![Journaux d’audit AD FS](./media/active-directory-aadconnect-health-requirements/adfsaudit.png)

> [!WARNING]
> Une stratégie de groupe peut désactiver l’audit AD FS. Si l’audit AD FS est désactivé, l’analyse de l’utilisation sur les activités de connexion n’est pas disponible. Assurez-vous de ne pas disposer de stratégie de groupe qui désactive l’audit AD FS.>
>


## <a name="installing-hello-azure-ad-connect-health-agent-for-sync"></a>L’installation d’agent d’Azure AD Connect Health hello pour la synchronisation
agent de Connect Health Hello Azure AD pour la synchronisation est installé automatiquement dans la build la plus récente d’Azure AD Connect hello. toouse Azure AD Connect pour la synchronisation, vous devez la version la plus récente hello toodownload d’Azure AD Connect et l’installer. Vous pouvez télécharger la version la plus récente hello [ici](http://www.microsoft.com/download/details.aspx?id=47594).

tooverify hello agent a été installé, recherchez hello suivant des services sur le serveur de hello. Si vous terminé la configuration de hello, ils doivent déjà être en cours d’exécution. Dans le cas contraire, elles sont arrêtées jusqu'à ce que la configuration hello est terminée.

* Azure AD Connect Health Sync Insights Service
* Azure AD Connect Health Sync Monitoring Service

![Vérifier Azure AD Connect Health pour la synchronisation](./media/active-directory-aadconnect-health-sync/services.png)

> [!NOTE]
> N'oubliez pas que l'utilisation d'Azure AD Connect Health requiert Azure AD Premium. Si vous n’avez pas d’Azure AD Premium, vous êtes configuration hello toocomplete Impossible hello portail Azure. Pour plus d’informations, consultez hello [page spécifications](active-directory-aadconnect-health-agent-install.md#requirements).
>
>

## <a name="manual-azure-ad-connect-health-for-sync-registration"></a>Enregistrement manuel d’Azure AD Connect Health pour la synchronisation
Si hello Azure AD Connect Health pour l’inscription de l’agent de synchronisation échoue après avoir correctement installé Azure AD Connect, vous pouvez utiliser hello suivant de commande PowerShell toomanually inscrire l’agent de hello.

> [!IMPORTANT]
> À l’aide de cette commande PowerShell est uniquement requis si l’inscription de l’agent de hello échoue après l’installation d’Azure AD Connect.
>
>

Hello PowerShell suivant, la commande est nécessaire uniquement lorsque l’enregistrement de l’agent d’intégrité hello échoue même après une installation réussie et une configuration d’Azure AD Connect. services d’Azure AD Connect Health Hello démarrera une fois que l’agent de hello a été correctement inscrit.

Vous pouvez manuellement inscrire l’agent de Connect Health hello Azure AD pour la synchronisation à l’aide de hello suivant de commande PowerShell :

`Register-AzureADConnectHealthSyncAgent -AttributeFiltering $false -StagingMode $false`

commande Hello prend après les paramètres :

* AttributeFiltering : $true (par défaut) - si Azure AD Connect n’est pas synchronisé ensemble d’attributs par défaut hello et a été personnalisé toouse un attribut filtré défini. Dans le cas contraire, c’est le paramètre $false qui s’applique.
* StagingMode : $false (par défaut) - si le serveur d’Azure AD Connect hello n’est pas la zone de transit mode, $true si hello serveur est configuré toobe dans le mode de mise en lots.

Lorsque vous y êtes invité pour l’authentification, vous devez utiliser hello du même compte d’administrateur général (tel que admin@domain.onmicrosoft.com) qui a été utilisé pour la configuration d’Azure AD Connect.

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-ds"></a>L’installation hello Agent Azure AD Connect Health pour AD DS
toostart hello d’installation de l’agent, double-cliquez sur le fichier .exe hello que vous avez téléchargé. Sur le premier écran de hello, cliquez sur Installer.

![Vérifier Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install1.png)

Une fois l’installation de hello est terminée, cliquez sur Configurer.

![Vérifier Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install2.png)

Une invite de commandes est lancée, suivie par certains éléments PowerShell qui exécutent Register-AzureADConnectHealthADDSAgent. Lorsque message toosign dans tooAzure, continuez et connectez-vous.

![Vérifier Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install3.png)

Une fois que vous êtes connecté, PowerShell continue. Une fois terminée, vous pouvez fermer PowerShell et hello configuration est terminée.

À ce stade, les services de hello doivent être démarrés automatiquement autorisant hello agent toomonitor et collecter des données. Si vous ne respectez pas tous les logiciels prérequis hello décrites dans les sections précédentes hello, avertissements apparaissent dans la fenêtre de PowerShell hello. Être vraiment toocomplete hello [exigences](active-directory-aadconnect-health-agent-install.md#requirements) avant d’installer l’agent de hello. Hello suivant capture d’écran est un exemple de ces erreurs.

![Vérifier Azure AD Connect Health pour AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install4.png)

tooverify hello agent a été installé, recherchez hello suivant des services sur le contrôleur de domaine hello.

* Azure AD Connect Health AD DS Insights Service
* Azure AD Connect Health AD DS Monitoring Service

Si vous terminé la configuration de hello, ces services doivent déjà être en cours d’exécution. Dans le cas contraire, elles sont arrêtées jusqu'à ce que la configuration hello est terminée.

![Vérifier Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install5.png)


### <a name="agent-registration-using-powershell"></a>Inscription de l’agent à l’aide de PowerShell
Après avoir installé hello approprié setup.exe de l’agent, vous pouvez effectuer l’étape de l’inscription de l’agent hello à l’aide de hello suivant les commandes PowerShell en fonction du rôle de hello. Ouvrez une fenêtre PowerShell et d’exécuter la commande appropriée de hello :

```
    Register-AzureADConnectHealthADFSAgent
    Register-AzureADConnectHealthADDSAgent
    Register-AzureADConnectHealthSyncAgent

```

Ces commandes acceptent « Credential » comme une inscription de hello toocomplete paramètre d’une manière non interactive ou sur un ordinateur Server Core.
* Hello d’informations d’identification peut être capturée dans une variable PowerShell qui est passée en tant que paramètre.
* Vous pouvez fournir n’importe quel ordinateur Azure AD Identity ayant des agents d’accès tooregister hello et n’a pas l’authentification Multifacteur activée.
* Par défaut, les administrateurs généraux ont accès enregistrement de l’agent tooperform. Vous pouvez également autoriser autres moins privilégié identités tooperform cette étape. En savoir plus sur le [Contrôle d’accès en fonction du rôle](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control).

```
    $cred = Get-Credential
    Register-AzureADConnectHealthADFSAgent -Credential $cred

```

## <a name="configure-azure-ad-connect-health-agents-toouse-http-proxy"></a>Configurer les Agents Azure AD Connect d’intégrité toouse HTTP Proxy
Vous pouvez configurer des Agents Azure AD Connect d’intégrité toowork avec un HTTP Proxy.

> [!NOTE]
> * À l’aide de « Netsh WinHttp set ProxyServerAddress » n’est pas prise en charge car l’agent de hello utilise les requêtes web System.Net toomake au lieu des Services HTTP Microsoft Windows.
> * Bonjour adresse de Http Proxy configuré est utilisé toopass via Https des messages chiffrés.
> * Les serveurs proxy authentifiés (à l’aide de HTTPBasic) ne sont pas pris en charge.
>
>

### <a name="change-health-agent-proxy-configuration"></a>Modification de la configuration du proxy d’un agent Health
Vous avez hello suivant options tooconfigure Azure AD Connect Health Agent toouse un HTTP Proxy.

> [!NOTE]
> Tous les services Azure AD Connect Health Agent doivent être redémarrés, par ordre de toobe de paramètres de proxy hello mis à jour. Exécutez hello de commande suivante :<br>
> Restart-Service AdHealth*
>
>

#### <a name="import-existing-proxy-settings"></a>Importation des paramètres de proxy existants
##### <a name="import-from-internet-explorer"></a>Importation à partir d'Internet Explorer
Paramètres du proxy Internet Explorer HTTP peuvent être importés, toobe utilisé par hello Agents Azure AD Connect d’intégrité. Sur chacun des serveurs hello exécutant l’agent d’intégrité hello, exécutez hello suivant de commande PowerShell :

    Set-AzureAdConnectHealthProxySettings -ImportFromInternetSettings

##### <a name="import-from-winhttp"></a>Importation à partir de WinHTTP
Paramètres de proxy WinHTTP peuvent être importés, toobe utilisé par hello Agents Azure AD Connect d’intégrité. Sur chacun des serveurs hello exécutant l’agent d’intégrité hello, exécutez hello suivant de commande PowerShell :

    Set-AzureAdConnectHealthProxySettings -ImportFromWinHttp

#### <a name="specify-proxy-addresses-manually"></a>Spécification manuelle des adresses du proxy
Vous pouvez spécifier manuellement un serveur proxy sur chacun des serveurs hello hello Agent d’intégrité, en cours d’exécution en exécutant hello suivant de commande PowerShell :

    Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress address:port

Exemple : *Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress myproxyserver: 443*

* « address » peut être un nom de serveur DNS pouvant être résolu ou une adresse IPv4
* "port" peut être omis. Dans ce cas, 443 est choisi comme port par défaut.

#### <a name="clear-existing-proxy-configuration"></a>Effacement de la configuration de proxy existante
Vous pouvez désactiver la configuration du proxy existant hello en exécutant hello de commande suivante :

    Set-AzureAdConnectHealthProxySettings -NoProxy


### <a name="read-current-proxy-settings"></a>Lecture des paramètres de proxy actuels
Vous pouvez lire hello actuellement configuré les paramètres de proxy en exécutant hello de commande suivante :

    Get-AzureAdConnectHealthProxySettings


## <a name="test-connectivity-tooazure-ad-connect-health-service"></a>Tester la connectivité tooAzure AD Service Connect Health
Il est possible que les problèmes peuvent survenir qui provoquent l’agent Azure AD Connect Health de hello toolose connectivité avec le service de hello Azure AD Connect Health. Cela inclut, entre autres, des problèmes réseau et des problèmes d’autorisation.

Si l’agent de hello est un service de toosend Impossible de données toohello Azure AD Connect Health pendant plus de deux heures, il est indiqué par hello suivant l’alerte dans le portail de hello : « les données de Service de contrôle d’intégrité ne sont pas de toodate. » Vous pouvez vérifier si hello affectée Azure AD Connect Health agent est le service de tooupload en mesure de données toohello Azure AD Connect Health en exécutant hello suivant de commande PowerShell :

    Test-AzureADConnectHealthConnectivity -Role ADFS

paramètre de rôle Hello prend actuellement hello valeurs suivantes :

* ADFS
* Synchronisation
* AJOUTE

Vous pouvez utiliser l’indicateur de - ShowResults hello dans hello commande tooview des journaux détaillés. Utilisez hello l’exemple suivant :

    Test-AzureADConnectHealthConnectivity -Role Sync -ShowResult

> [!NOTE]
> outil de connectivité toouse hello, vous devez premier enregistrement de l’agent terminée hello. Si vous n’êtes pas l’inscription de l’agent toocomplete en mesure de hello, assurez-vous que vous avez rempli toutes les hello [exigences](active-directory-aadconnect-health-agent-install.md#requirements) pour Azure AD Connect Health. Ce test de connectivité est effectué par défaut lors de l’inscription de l’agent.
>
>

## <a name="related-links"></a>Liens connexes
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Opérations Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Utilisation d’Azure AD Connect Health avec AD FS](active-directory-aadconnect-health-adfs.md)
* [Utilisation d'Azure AD Connect Health pour la synchronisation (en Anglais)](active-directory-aadconnect-health-sync.md)
* [Utilisation d’Azure AD Connect Health avec AD DS](active-directory-aadconnect-health-adds.md)
* [Forum Aux Questions (FAQ) Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Historique de publication des versions d’Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
