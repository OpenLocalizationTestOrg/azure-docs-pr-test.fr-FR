---
title: "solution d’aaaOffice 365 Operations Management Suite (OMS) | Documents Microsoft"
description: "Cet article fournit des détails sur la configuration et l’utilisation de la solution hello Office 365 dans OMS.  Il inclut une description détaillée des enregistrements hello Office 365 créés dans le journal Analytique."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: a1507745251ff015abb785bae8352fea7cea0734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-solution-in-operations-management-suite-oms"></a>Solutions Office 365 dans Operations Management Suite (OMS)

![Logo Office 365](media/oms-solution-office-365/icon.png)

Hello Office 365 solution Operations Management Suite (OMS) vous permet de toomonitor votre environnement Office 365 dans le journal Analytique.  

- Surveiller les activités des utilisateurs sur des modèles d’utilisation tooanalyze vos comptes Office 365 ainsi que pour identifier des comportements. Par exemple, vous pouvez extraire les scénarios d’utilisation spécifiques, tels que les fichiers qui sont partagées en dehors de votre organisation ou les sites SharePoint les plus populaires de hello.
- Surveiller les modifications de configuration tootrack administrateur activités ou les opérations doté de privilèges élevés.
- Détectez et analysez le comportement des utilisateurs indésirables, qui peut être personnalisé pour les besoins de votre organisation.
- Présentation d’audit et de conformité. Par exemple, vous pouvez surveiller les opérations d’accès aux fichiers sur des fichiers confidentiels, qui peuvent vous aider avec les processus d’audit et de conformité hello.
- Effectuez le dépannage opérationnel à l’aide de la recherche OMS en haut des données d’activité Office 365 de votre organisation.

## <a name="prerequisites"></a>Composants requis
Hello Voici solution toothis préalable requis installés et configurés.

- Abonnement à Office 365 organisationnel.
- Informations d’identification pour un compte d’utilisateur qui est un administrateur global.
- tooreceive les données d’audit, vous devez [configurer l’audit](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&rs=en-US&ad=US#PickTab=Before_you_begin) dans votre abonnement Office 365.  Notez que [l’audit de boîte aux lettres](https://technet.microsoft.com/library/dn879651.aspx) est configuré séparément.  Vous pouvez toujours installer la solution de hello et collecter d’autres données si l’audit n’est pas configuré.
 


## <a name="management-packs"></a>Packs d’administration
Cette solution n’installe aucun pack d’administration dans les groupes d’administration connectés.
  

## <a name="configuration"></a>Configuration
Une fois que vous [ajouter hello Office 365 solution tooyour abonnement](../log-analytics/log-analytics-add-solutions.md), vous avez tooconnect il tooyour abonnement Office 365.

1. Ajouter tooyour de solution de gestion des alertes hello espace de travail OMS à l’aide du processus de hello décrit dans [ajouter des solutions](../log-analytics/log-analytics-add-solutions.md).
2. Accédez trop**paramètres** dans portail OMS : hello.
3. Sous **Sources connectées**, sélectionnez **Office 365**.
4. Cliquez sur **Connecter Office 365**.<br>![Connectez-vous à Office 365](media/oms-solution-office-365/configure.png)
5. Connectez-vous tooOffice 365 avec un compte qui est un administrateur Global pour votre abonnement. 
6. abonnement de Hello s’afficheront avec les charges de travail hello la surveillance des solutions de hello.<br>![Connectez-vous à Office 365](media/oms-solution-office-365/connected.png) 


## <a name="data-collection"></a>Collecte des données
### <a name="supported-agents"></a>Agents pris en charge
Hello solution Office 365 ne récupérer les données de n’importe quelle hello [agents OMS](../log-analytics/log-analytics-data-sources.md).  Il récupère les données directement à partir d’Office 365.

### <a name="collection-frequency"></a>Fréquence de collecte
Office 365 envoie un [webhook notification](https://msdn.microsoft.com/office-365/office-365-management-activity-api-reference#receiving-notifications) avec des données détaillées tooLog Analytique chaque fois qu’un enregistrement est créé.

## <a name="using-hello-solution"></a>À l’aide de la solution de hello
Lorsque vous ajoutez d’espace de travail OMS hello Office 365 solution tooyour, hello **Office 365** vignette sera ajoutée tooyour du tableau de bord OMS. Cette vignette affiche un nombre et une représentation graphique du nombre de hello d’ordinateurs dans votre environnement et leur conformité de mise à jour.<br><br>
![Vignette du résumé Office 365](media/oms-solution-office-365/tile.png)  

Cliquez sur hello **Office 365** vignette tooopen hello **Office 365** tableau de bord.

![Tableau de bord Office 365](media/oms-solution-office-365/dashboard.png)  

tableau de bord Hello inclut des colonnes de hello Bonjour tableau suivant. Chaque colonne répertorie hello top 10 alertes en faisant correspondre le nombre que les critères de la colonne pour hello spécifié plage étendue et d’heure. Vous pouvez exécuter une recherche de journal qui fournit l’intégralité de la liste hello en cliquant sur voir en bas de hello de colonne de hello ou en cliquant sur en-tête de colonne hello.

| Colonne | Description |
|:--|:--|
| Opérations | Fournit des informations sur hello les utilisateurs à partir de vos abonnements Office 365 analysés de tous les actifs. Vous serez également le nombre de hello toosee en mesure d’activités qui se produisent au fil du temps.
| Microsoft Exchange | Montre la répartition hello des activités d’Exchange Server telles que l’autorisation d’ajouter-Mailbox ou Set-Mailbox. |
| SharePoint | Affiche les activités supérieur hello aux utilisateurs d’effectuer sur les documents de SharePoint. Quand vous explorez à partir de cette vignette, page de recherche hello affiche les détails de hello de ces activités, telles que le document cible de hello et l’emplacement de hello de cette activité. Par exemple, pour un événement d’accéder au fichier, vous sera en mesure de toosee hello document qui est accessible, son nom de compte associé et une adresse IP. |
| Azure Active Directory | Inclut les activités utilisateur supérieures, telles que la réinitialisation du mot de passe utilisateur et les tentatives de connexion. Quand vous explorez, vous serez toosee en mesure de hello des détails sur ces activités comme hello état de résultat. Ceci est particulièrement utile si vous souhaitez toomonitor les activités suspectes sur votre Azure Active Directory. |




## <a name="log-analytics-records"></a>Enregistrements Log Analytics

Tous les enregistrements créés dans l’espace de travail hello Analytique de journal par les solutions hello Office 365 ont une **Type** de **OfficeActivity**.  Hello **OfficeWorkload** propriété détermine quel enregistrement hello du service Office 365 fait référence trop Exchange, AzureActiveDirectory, SharePoint ou OneDrive.  Hello **RecordType** propriété spécifie le type hello de l’opération.  propriétés de Hello varient pour chaque type d’opération et sont affichées dans les tableaux hello ci-dessous.

### <a name="common-properties"></a>Propriétés communes
Hello propriétés suivantes est des enregistrements communs tooall Office 365.

| Propriété | Description |
|:--- |:--- |
| Type | *OfficeActivity* |
| ClientIP | adresse IP de Hello du périphérique hello utilisé lors de l’activité hello a été enregistrée. adresse IP de Hello s’affiche au format d’adresse IPv4 ou IPv6. |
| OfficeWorkload | Service Office 365 hello enregistrement fait référence à.<br><br>AzureActiveDirectory<br>Microsoft Exchange<br>SharePoint|
| Opération | nom Hello d’activité utilisateur ou administrateur de hello.  |
| OrganizationId | Hello GUID pour le client Office 365 de votre organisation. Cette valeur sera toujours être hello même pour votre organisation, quel que soit le service hello Office 365 dans lequel elle se de produit. |
| RecordType | Type d’opération effectuée. |
| ResultStatus | Indique si l’action hello (propriété de l’opération spécifiée dans hello) a réussi ou non. Les valeurs possibles sont Réussie, Partiellement réussie ou Échec. Pour les activités d’administration Exchange, valeur de hello est la valeur True ou False. |
| UserId | Hello UPN (nom d’utilisateur Principal) de l’utilisateur hello qui a effectué l’action hello qui a entraîné hello enregistrement ; par exemple, my_name@my_domain_name. Notez que les enregistrements pour l’activité exécutée par les comptes système (tels que SHAREPOINT\system ou NTAUTHORITY\SYSTEM) sont également inclus. | 
| UserKey | Un autre ID pour l’utilisateur hello identifié Bonjour propriété UserId.  Par exemple, cette propriété est remplie avec l’ID unique de hello passport (PUID) pour les événements exécutés par les utilisateurs dans SharePoint, OneDrive entreprise et Exchange. Cette propriété peut également spécifier hello même valeur que hello propriété UserID pour les événements qui se produisent dans des événements et autres services effectuée par les comptes système|
| UserType | type Hello de l’utilisateur qui a effectué l’opération de hello.<br><br>Admin<br>Application<br>DcAdmin<br>Standard <br>Réservé<br>ServicePrincipal<br>System |


### <a name="azure-active-directory-base"></a>Base Azure Active Directory
Hello propriétés suivantes est des enregistrements d’Azure Active Directory tooall communs.

| Propriété | Description |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectory |
| AzureActiveDirectory_EventType | type de Hello d’événement de Azure AD. |
| ExtendedProperties | Hello des propriétés étendues d’événement de hello Azure AD. |


### <a name="azure-active-directory-account-logon"></a>Connexion au compte Azure Active Directory
Ces enregistrements sont créés lorsqu’un utilisateur Active Directory tente de toolog sur.

| Propriété | Description |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectoryAccountLogon |
| Application | application Hello qui déclenche l’événement de connexion de compte hello, telles que Office 15. |
| Client | Plus d’informations sur les clients hello périphérique, le périphérique du système d’exploitation et navigateur de périphérique qui a été utilisé pour hello d’événement de connexion de compte hello. |
| LoginStatus | Cette propriété est directement issue de OrgIdLogon.LoginStatus. mappage de Hello différents intéressant d’échecs de connexion peut être effectué par les algorithmes de génération d’alertes. |
| UserDomain | Hello d’informations d’identité du client (TII). | 


### <a name="azure-active-directory"></a>Azure Active Directory
Ces enregistrements sont créés lors de la modification ou ajouts apportés tooAzure les objets Active Directory.

| Propriété | Description |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectory |
| AADTarget | utilisateur de Hello action hello (identifiée par hello propriété Operation) a été effectuée sur. |
| Acteur | utilisateur de Hello ou principal du service qui a exécuté hello action. |
| ActorContextId | Hello GUID de l’organisation hello hello acteur appartient. |
| ActorIpAddress | Bonjour adresseIP d’acteur au format d’adresse IPV4 ou IPV6. |
| InterSystemsId | Hello GUID qui effectuent le suivi des actions de hello entre les composants de service de hello Office 365. |
| IntraSystemId |   Hello GUID généré par l’action de hello tootrack Azure Active Directory. |
| SupportTicketId | client de Hello prend en charge les ID de ticket pour l’action de hello dans les situations de « agir-nom-de ». |
| TargetContextId | Hello GUID de l’organisation hello hello ciblé utilisateur appartient. |


### <a name="data-center-security"></a>Sécurité du centre de données
Ces enregistrements sont créés à partir des données d’audit de sécurité du centre de données.  

| Propriété | Description |
|:--- |:--- |
| EffectiveOrganization | nom Hello du client, hello dont hello élévation/applet de commande a été ciblé sur. |
| ElevationApprovedTime | horodateur de Hello pour lorsque l’élévation hello a été approuvée. |
| ElevationApprover | nom Hello d’un gestionnaire de Microsoft. |
| ElevationDuration | Durée Hello pour le hello élévation était active. |
| ElevationRequestId |  Identificateur unique pour la demande d’élévation hello. |
| ElevationRole | élévation de hello Hello rôle a été demandée. |
| ElevationTime | Hello heure de début de l’élévation hello. |
| start_time | Hello heure de début de l’exécution de hello applet de commande. |


### <a name="exchange-admin"></a>Administrateur Exchange
Ces enregistrements sont créés lorsque des modifications sont apportées tooExchange configuration.

| Propriété | Description |
|:--- |:--- |
| OfficeWorkload | Microsoft Exchange |
| RecordType     | ExchangeAdmin |
| ExternalAccess |  Spécifie si l’applet de commande hello a été exécuté par un utilisateur dans votre organisation, par le personnel du centre de données Microsoft ou un compte de service du centre de données, ou par un administrateur délégué. valeur de Hello False indique que cette applet de commande hello a été exécuté par une personne dans votre organisation. valeur de Hello True indique que cette applet de commande hello a été exécutée par le personnel du centre de données, un compte de service du centre de données ou un administrateur délégué. |
| ModifiedObjectResolvedName |  Il s’agit de nom convivial hello d’objet hello qui a été modifié par l’applet de commande hello. Cette opération est enregistrée uniquement si l’applet de commande hello modifie l’objet de hello. |
| OrganizationName | nom Hello du client de hello. |
| OriginatingServer | nom Hello du serveur hello quels hello applet de commande a été exécutée. |
| Paramètres | nom de Hello et valeur pour tous les paramètres qui ont été utilisés avec l’applet de commande hello identifié dans hello propriété Operations. |


### <a name="exchange-mailbox"></a>Boîte aux lettres Exchange
Ces enregistrements sont créés lorsque des ajouts ou des modifications sont apportées tooExchange des boîtes aux lettres.

| Propriété | Description |
|:--- |:--- |
| OfficeWorkload | Microsoft Exchange |
| RecordType     | ExchangeItem |
| ClientInfoString | Informations sur le client de messagerie hello qui a été utilisé tooperform hello opération, comme une version du navigateur, la version d’Outlook et l’appareil mobile. |
| Client_IPAddress | adresse IP de Hello du périphérique hello utilisé lors de l’opération de hello a été enregistrée. adresse IP de Hello s’affiche au format d’adresse IPv4 ou IPv6. |
| ClientMachineName | nom de l’ordinateur Hello qui héberge le client Outlook de hello. |
| ClientProcessName | client de messagerie Hello qui a été de boîte aux lettres de hello tooaccess utilisé. |
| ClientVersion | version Hello hello du client de messagerie. |
| InternalLogonType | Réservé à un usage interne. |
| Logon_Type | Indique le type hello d’utilisateur accessibles de boîte aux lettres hello effectué hello qui a été enregistré. |
| LogonUserDisplayName |    nom convivial de Hello d’utilisateur hello qui a effectué l’opération de hello. |
| LogonUserSid | Hello SID de l’utilisateur de hello qui a effectué l’opération de hello. |
| MailboxGuid | Hello Exchange des GUID de boîte aux lettres hello qui a accédé. |
| MailboxOwnerMasterAccountSid | SID de compte principal du compte du propriétaire de boîte aux lettres. |
| MailboxOwnerSid | Hello SID du propriétaire de boîte aux lettres hello. |
| MailboxOwnerUPN | adresse de messagerie Hello de personne hello possède une boîte aux lettres hello qui a accédé. |


### <a name="exchange-mailbox-audit"></a>Audit de la boîte aux lettres Exchange
Ces enregistrements sont créés lors de la création d’une entrée d’audit de boîte aux lettres.

| Propriété | Description |
|:--- |:--- |
| OfficeWorkload | Microsoft Exchange |
| RecordType     | ExchangeItem |
| Item | Représente l’élément hello sur quel hello opération a été exécutée | 
| SendAsUserMailboxGuid | Hello Exchange des GUID de boîte aux lettres hello qui était accessible e-mail toosend comme. |
| SendAsUserSmtp | Adresse SMTP de l’utilisateur hello est empruntée. |
| SendonBehalfOfUserMailboxGuid | Hello Exchange des GUID de boîte aux lettres hello qui était accessible toosend des messages de la part de. |
| SendOnBehalfOfUserSmtp | Adresse SMTP de l’utilisateur hello sur le compte duquel hello par courrier électronique est envoyé. |


### <a name="exchange-mailbox-audit-group"></a>Groupe d’audit de la boîte aux lettres Exchange
Ces enregistrements sont créés lorsque des ajouts ou des modifications sont apportées tooExchange groupes.

| Propriété | Description |
|:--- |:--- |
| OfficeWorkload | Microsoft Exchange |
| OfficeWorkload | ExchangeItemGroup |
| AffectedItems | Informations sur chaque élément de groupe de hello. |
| CrossMailboxOperations | Indique si les opération hello plusieurs boîtes aux lettres. |
| DestMailboxId | Définie uniquement si le paramètre de CrossMailboxOperations hello a la valeur True. Spécifie la boîte aux lettres cible hello GUID. |
| DestMailboxOwnerMasterAccountSid | Définie uniquement si le paramètre de CrossMailboxOperations hello a la valeur True. Spécifie les hello SID pour hello master le SID du compte du propriétaire de boîte aux lettres cible hello. |
| DestMailboxOwnerSid | Définie uniquement si le paramètre de CrossMailboxOperations hello a la valeur True. Spécifie les hello SID de boîte aux lettres de hello cible. |
| DestMailboxOwnerUPN | Définie uniquement si le paramètre de CrossMailboxOperations hello a la valeur True. Spécifie les hello UPN du propriétaire de hello de boîte aux lettres de hello cible. |
| DestFolder | dossier de destination Hello, pour les opérations de déplacement. |
| Dossier | dossier Hello où se trouve un groupe d’éléments. |
| Dossiers |     Informations sur les dossiers de source de hello impliqués dans une opération ; par exemple, si les dossiers sont sélectionnés, puis supprimés. |


### <a name="sharepoint-base"></a>SharePoint Base
Ces propriétés sont des enregistrements de SharePoint tooall communs.

| Propriété | Description |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| EventSource | Identifie qu’un événement s’est produit dans SharePoint. Les valeurs possibles sont ObjectModel ou SharePoint. |
| itemType | type de Hello d’objet qui a été accédé ou modifié. Consultez table ItemType de hello pour plus d’informations sur les types d’objets hello. |
| MachineDomainInfo | Informations sur les opérations de synchronisation de terminal. Ces informations sont signalées uniquement s’il est présent dans la demande de hello. |
| MachineId |   Informations sur les opérations de synchronisation de terminal. Ces informations sont signalées uniquement s’il est présent dans la demande de hello. |
| Site_ | Hello GUID du site hello où se trouve hello fichier ou un dossier accédé par l’utilisateur de hello. |
| Source_Name | entité Hello qui a déclenché hello audité l’opération. Les valeurs possibles sont ObjectModel ou SharePoint. |
| UserAgent | Informations sur le client ou le navigateur de l’utilisateur hello. Ces informations sont fournies par le client de hello ou un navigateur. |


### <a name="sharepoint-schema"></a>Schéma de SharePoint
Ces enregistrements sont créés lorsque des modifications de configuration sont apportées tooSharePoint.

| Propriété | Description |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| CustomEvent | Chaîne facultative pour les événements personnalisés. |
| Event_Data |  Charge facultative pour les événements personnalisés. |
| ModifiedProperties | propriété de Hello est incluse pour les événements d’administration, telles que l’ajout d’un utilisateur en tant que membre d’un site ou un groupe administrateur de collection de sites. propriété de Hello inclut le nom hello de propriété hello qui a été modifiée (par exemple, groupe d’administration de Site hello), hello nouvelle valeur de hello a modifié la propriété (telle hello l’utilisateur qui a été ajouté en tant qu’un administrateur de site) et la valeur précédente hello hello modifié l’objet. |


### <a name="sharepoint-file-operations"></a>Opérations sur les fichiers SharePoint
Ces enregistrements sont créés dans les opérations de toofile de réponse dans SharePoint.

| Propriété | Description |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePointFileOperation |
| DestinationFileExtension | extension de fichier Hello d’un fichier qui est copié ou déplacé. Cette propriété s’affiche uniquement pour les événements FileCopied et FileMoved. |
| DestinationFileName | nom Hello du fichier hello qui est copié ou déplacé. Cette propriété s’affiche uniquement pour les événements FileCopied et FileMoved. |
| DestinationRelativeUrl | URL de Hello hello du dossier de destination dans lequel un fichier est copié ou déplacé. combinaison de Hello de valeurs hello pour les paramètres SiteURL DestinationRelativeURL et DestinationFileName est hello identique à la valeur hello pour la propriété ObjectID hello, qui est le nom de chemin d’accès complet de hello pour le fichier hello qui a été copié. Cette propriété s’affiche uniquement pour les événements FileCopied et FileMoved. |
| SharingType | type Hello des autorisations qui ont été affectées toohello utilisateur qui hello de ressource de partage a été partagé avec. Cet utilisateur est identifié par le paramètre de UserSharedWith hello. |
| Site_Url | Hello l’URL du site hello où se trouve hello fichier ou un dossier accédé par l’utilisateur de hello. |
| SourceFileExtension | extension de fichier Hello du fichier hello qui est accessible par l’utilisateur de hello. Cette propriété est vide si l’objet hello qui a accédé est un dossier. |
| SourceFileName |  nom de Hello du fichier de hello ou un dossier accédé par l’utilisateur de hello. |
| SourceRelativeUrl | Hello l’URL du dossier hello qui contient le fichier hello accédé par l’utilisateur de hello. combinaison de Hello de valeurs hello pour les paramètres de SiteURL SourceRelativeURL et SourceFileName hello est hello identique à la valeur hello pour la propriété ObjectID hello, qui est le nom de chemin d’accès complet hello pour le fichier hello accessible par l’utilisateur de hello. |
| UserSharedWith |  utilisateur de Hello une ressource a été partagée avec. |




## <a name="sample-log-searches"></a>Exemples de recherches dans les journaux
Hello tableau suivant fournit des exemples des recherches de journaux pour les enregistrements de mise à jour collectées par cette solution.

| Interroger | Description |
| --- | --- |
|Nombre de toutes les opérations de hello sur votre abonnement Office 365 |`Type = OfficeActivity | measure count() by Operation` |
|Utilisation des sites SharePoint|' Type = OfficeActivity OfficeWorkload = sharepoint | measure count() as Count by SiteUrl | sort Count asc`|
|Opérations d’accès de fichier par type d’utilisateur|`Type=OfficeActivity OfficeWorkload=sharepoint Operation=FileAccessed | measure count() by UserType`|
|Recherche avec un mot clé spécifique|`Type=OfficeActivity OfficeWorkload=azureactivedirectory "MyTest"`|
|Analyser des actions externes sur Exchange|`Type=OfficeActivity OfficeWorkload=exchange ExternalAccess = true`|



## <a name="troubleshooting"></a>Résolution des problèmes

Si votre solution Office 365 ne recueille pas les données comme prévu, vérifiez son état dans le portail OMS hello **paramètres** -> **Sources connectées** -> **Office 365** . Hello tableau suivant décrit chaque état.

| État | Description |
|:--|:--|
| Actif | Hello abonnement Office 365 est actif et la charge de travail hello est correctement connecté tooyour espace de travail OMS. |
| Pending | Hello abonnement Office 365 est activé, mais la charge de travail hello n’est pas encore connecté tooyour espace de travail OMS avec succès. Hello première que connexion d’abonnement de hello Office 365, toutes les charges de travail hello sera à cet état jusqu'à ce qu’ils sont correctement connectés. Patientez 24 heures pour tous les tooActive de tooswitch hello les charges de travail. |
| Inactif | Hello abonnement Office 365 est dans un état inactif. Vérifiez votre page d’administrateur d’Office 365 pour plus d’informations. Après avoir activé votre abonnement Office 365, supprimer la liaison à partir de votre espace de travail OMS et le lier à nouveau toostart recevoir des données. |



## <a name="next-steps"></a>Étapes suivantes
* Utiliser des recherches de journaux dans [Analytique de journal](../log-analytics/log-analytics-log-searches.md) tooview détaillé les données de mise à jour.
* [Créer vos propres tableaux de bord](../log-analytics/log-analytics-dashboards.md) toodisplay vos requêtes de recherche favoris Office 365.
* [Créer des alertes](../log-analytics/log-analytics-alerts.md) toobe informé de manière proactive des activités d’Office 365 importantes.  
