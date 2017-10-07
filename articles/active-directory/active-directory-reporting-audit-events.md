---
title: "événements de rapport d’audit aaaAzure Active Directory | Documents Microsoft"
description: "Événements audités disponibles pour l'affichage et le téléchargement à partir d'Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 307eedf7-05bc-448d-a84d-bead5a4c5770
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 4a84cce2be56bde006164abf10ad1e72ca6e99bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-report-events"></a>Événements de rapport d’audit d’Azure Active Directory
*Cette documentation fait partie de hello [Guide Azure Active Directory Reporting](active-directory-reporting-guide.md).*

Hello rapport de d’Audit Azure Active Directory permet aux clients d’identifier les actions privilégiées qui s’est produite dans leur annuaire Active Directory de Azure. Des actions privilégiées incluent des modifications d’élévation (par exemple, la création de rôle ou les réinitialisations de mot de passe), la modification des configurations de stratégie (par exemple des stratégies de mot de passe), ou la configuration de toodirectory de modifications (par exemple, modifications toodomain paramètres de fédération). Hello rapports fournissent un enregistrement d’audit de hello pour nom de l’événement hello, acteur hello qui a effectué l’action hello, les ressources de cible hello affectées par la modification de hello et hello date et heure (UTC). Les clients sont liste de hello tooretrieve en mesure d’événements d’audit pour leurs Azure Active Directory via hello [Azure Portal](https://portal.azure.com/), comme décrit dans [afficher vos journaux d’Audit](active-directory-reporting-azure-portal.md).

## <a name="list-of-audit-report-events"></a>Liste d'événements de rapport d'audit
<!--- audit event descriptions should be in hello past tense --->

| Événements | Description de l'événement |
| --- | --- |
| **Événements liés aux utilisateurs** | |
| Ajouter un utilisateur |Ajouter un répertoire toohello de l’utilisateur. |
| Supprimer l'utilisateur |Un utilisateur est supprimé à partir du répertoire de hello. |
| Définir les propriétés de licence |Définir les propriétés de licence hello pour un utilisateur dans le répertoire de hello. |
| Réinitialiser le mot de passe de l'utilisateur |Réinitialiser le mot de passe de hello pour un utilisateur dans le répertoire de hello. |
| Modifier le mot de passe de l'utilisateur |Modifié le mot de passe de hello pour un utilisateur dans le répertoire de hello. |
| Modifier la licence de l'utilisateur |Modifier une licence hello utilisateur tooa dans le répertoire de hello. toosee les licences ont été mis à jour, examinez à hello [utilisateur de mise à jour](#update-user-attributes) propriétés ci-dessous |
| Mettre à jour l'utilisateur |Mise à jour d’un utilisateur dans le répertoire de hello. [Voir ci-dessous](#update-user-attributes) les attributs qui peuvent être mis à jour. |
| Définir le mot de passe utilisateur |Définir propriété hello un toochange utilisateur son mot de passe de connexion. |
| Mettre à jour les informations d’identification de l’utilisateur |Le mot de passe utilisateur hello modifié |
| **Événements liés aux groupes** | |
| Ajouter un groupe |Créer un groupe dans le répertoire de hello. |
| Mettre à jour un groupe |Mise à jour d’un groupe dans le répertoire de hello. toosee les propriétés de groupe ont été mis à jour, consultez trop[auditée des propriétés de groupe](#update-group-attributes) dans la section hello ci-dessous |
| Supprimer un groupe |A supprimé un groupe à partir du répertoire de hello. |
| CreateGroupSettings |Création de paramètres de groupe. |
| UpdateGroupSettings |Mise à jour de paramètres de groupe. toosee les paramètres de groupe ont été mis à jour, consultez trop[auditée des propriétés de groupe](#update-group-attributes) dans la section hello ci-dessous |
| DeleteGroupSettings |Suppression de paramètres de groupe. |
| SetGroupLicense |Définition d’une licence de groupe. |
| SetGroupManagedBy |Définissez toobe groupe géré par l’utilisateur |
| AddGroupMember |Membre ajouté toogroup |
| RemoveGroupMember |Supprimer un membre d’un groupe |
| AddGroupOwner |Propriétaire ajouté toogroup |
| RemoveGroupOwner |Suppression d’un propriétaire de groupe. |
| **Événements liés aux applications** | |
| Ajouter un principal du service |Ajouter un répertoire toohello principal du service. |
| Supprimer le principal du service |Supprimer un principal de service à partir du répertoire de hello. |
| Ajouter les informations d'identification du principal du service |Principal du service tooa les informations d’identification ajoutées. |
| Supprimer les informations d'identification du principal du service |Suppression des informations d'identification d'un principal du service |
| Ajouter l'entrée de délégation |Créé un [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) dans le répertoire de hello. |
| Définir l'entrée de délégation |Mise à jour un [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) dans le répertoire de hello. |
| Supprimer l'entrée de délégation |Supprimer un [OAuth2PermissionGrant](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permissiongrant-entity) dans le répertoire de hello. |
| **Événements liés aux rôles** | |
| Ajouter le rôle membre tooRole |Ajouter un rôle d’annuaire utilisateur tooa. |
| Supprimer un membre du rôle |Suppression d'un utilisateur d'un rôle de répertoire |
| AddRoleDefinition |Ajout d’une définition de rôle. |
| UpdateRoleDefinition |Mise à jour d’une définition de rôle. toosee les paramètres de rôle ont été mis à jour, consultez trop[auditée de propriétés de définition de rôle](#update-role-definition-attributes) dans la section hello ci-dessous |
| DeleteRoleDefinition |Suppression d’une définition de rôle. |
| AddRoleAssignmentToRoleDefinition |Définition de toorole d’affectation de rôle ajouté. |
| RemoveRoleAssignmentFromRoleDefinition |Suppression d’une affectation de rôle d’une définition de rôle. |
| AddRoleFromTemplate |Ajout d’un rôle à partir d’un modèle. |
| UpdateRole |Mise à jour d’un rôle. |
| AddRoleScopeMemberToRole |Ajouté toorole de membre incluses dans l’étendue. |
| RemoveRoleScopedMemberFromRole |Suppression d’un membre inclus dans une étendue d’un rôle. |
| **Événements d’appareil (tous les nouveaux événements)** | |
| AddDevice |Ajout d’un appareil. |
| UpdateDevice |Mise à jour d’un appareil. toosee les propriétés de l’appareil ont été mis à jour, consultez trop[propriétés d’un périphérique contrôlé](#update-device-attributes) dans la section hello ci-dessous |
| DeleteDevice |Suppression d’un appareil. |
| AddDeviceConfiguration |Ajout d’une configuration d’appareil. |
| UpdateDeviceConfiguration |Mise à jour d’une configuration d’appareil. toosee les propriétés de configuration de périphérique ont été mis à jour, consultez trop[propriétés de configuration de périphérique contrôlé](#update-device-configuration-attributes) dans la section hello ci-dessous |
| DeleteDeviceConfiguration |Suppression d’une configuration d’appareil. |
| AddRegisteredOwner |Ajouté toodevice de propriétaire enregistré. |
| AddRegisteredUsers |Ajouté toodevice d’utilisateurs inscrits. |
| RemoveRegisteredOwner |Suppression du propriétaire enregistré d’un appareil. |
| RemoveRegisteredUsers |Suppression d’utilisateurs enregistrés d’un appareil. |
| RemoveDeviceCredentials |Suppression des informations d’identification d’un appareil. |
| **Événements B2B** | |
| Lot d’invitations chargé |Un administrateur a téléchargé un fichier contenant toobe invitations envoyée toopartner utilisateurs. |
| Lot d’invitations traité. |Un fichier contenant des invitations à participer à toopartner utilisateurs a été traité. |
| Invitation d’un utilisateur externe. |Un utilisateur externe a été invitée toohello active. |
| Utilisation de l’invitation d’un utilisateur externe. |Un utilisateur externe a échangé leur répertoire de toohello invitation. |
| Ajouter un utilisateur externe toogroup. |Groupe d’appartenance tooa dans le répertoire de hello a été affecté à un utilisateur externe. |
| Affecter un utilisateur externe tooapplication. |Application de tooan d’un accès direct a été affecté à un utilisateur externe. |
| Création d’un locataire viral. |Un client a été créé dans Azure AD en échange d’invitation hello. |
| Création d’un utilisateur viral. |Un utilisateur a été créé dans un client existant dans Azure AD en échange d’invitation hello. |
| **Unités administratives (tous les nouveaux événements)** | |
| AddAdministrativeUnit |Ajout d’une unité administrative. |
| UpdateAdministrativeUnit |Mise à jour d’une unité administrative. toosee les propriétés d’une unité d’administration ont été mis à jour, consultez trop[propriétés d’une unité Administrative auditée](#update-administrative-unit-attributes) dans la section hello ci-dessous |
| DeleteAdministrativeUnit |Suppression d’une unité administrative. |
| AddMemberToAdministrativeUnit |Ajouter l’unité tooadministrative de membre. |
| RemoveMemberFromAdministrativeUnit |Suppression d’un membre d’une unité administrative. |
| **Événements liés aux répertoires** | |
| Ajouter le partenaire toocompany |Ajouter un répertoire de toohello partenaire. |
| Supprimer le partenaire de l'entreprise |Supprimer un partenaire à partir du répertoire de hello. |
| DemotePartner |Rétrogradation d’un partenaire. |
| Ajouter le domaine toocompany |Ajouter un répertoire toohello de domaine. |
| Supprimer le domaine de l'entreprise |Supprimer un domaine à partir du répertoire de hello. |
| Mettre à jour le domaine |Mise à jour d’un domaine sur le répertoire de hello. toosee les propriétés du domaine ont été mis à jour, consultez trop[propriétés du domaine auditée](#update-domain-attributes) dans la section hello ci-dessous |
| Définir l'authentification de domaine |Modifié le paramètre de domaine par défaut hello pour entreprise de hello. |
| Définir les informations de contact d'entreprise |Définition des préférences de contact au niveau de l'entreprise Cela inclut les adresses de messagerie pour le marketing, ainsi que les notifications techniques à propos de Microsoft Online Services. |
| Définir les paramètres de fédération du domaine |Mise à jour des paramètres de fédération hello pour un domaine. |
| Vérifier le domaine |Vérifié un domaine sur le répertoire de hello. |
| Vérifier le domaine vérifié par courrier électronique |Vérifié un domaine sur le répertoire hello à l’aide de la vérification du courrier électronique. |
| Définir l'indicateur DirSyncEnabled de l'entreprise |Définir la propriété hello qui permet à un répertoire pour Azure AD Sync. |
| Définir la stratégie de mot de passe |Définition des contraintes de longueur et de caractères des mots de passe utilisateur |
| Définir les informations de l'entreprise |Informations au niveau de l’entreprise hello mis à jour Consultez hello [Get-MsolCompanyInformation](https://msdn.microsoft.com/library/azure/dn194126.aspx) applet de commande PowerShell pour plus de détails. |
| SetCompanyAllowedDataLocation |Définition d’un emplacement de données autorisé pour l’entreprise. |
| SetCompanyDirSyncEnabled |Définition de l’indicateur DirSyncEnabled de l’entreprise. |
| SetCompanyDirSyncFeature |Définition de la fonctionnalité DirSync. |
| SetCompanyInformation |Définition des informations de l’entreprise. |
| SetCompanyMultiNationalEnabled |Définition de l’activation de la fonctionnalité multinationale. |
| SetDirectoryFeatureOnTenant |Définition de la fonctionnalité d’annuaire sur un client. |
| SetTenantLicenseProperties |Définition des propriétés d’une licence client. |
| CreateCompanySettings |Création de paramètres d’entreprise. |
| UpdateCompanySettings |Mise à jour de paramètres d’entreprise. toosee les propriétés de la société ont été mis à jour, consultez trop[propriétés entreprise auditée](#update-company-attributes) dans la section hello ci-dessous |
| DeleteCompanySettings |Suppression de paramètres d’entreprise. |
| SetAccidentalDeletionThreshold |Définition d’un seuil de suppression accidentelle |
| SetRightsManagementProperties |Définition de propriétés Rights Management. |
| PurgeRightsManagementProperties |Vidage de propriétés Rights Management. |
| UpdateExternalSecrets |Mise à jour de clés secrètes externes. |
| **Événements de stratégie (tous les nouveaux événements)** | |
| AddPolicy |Ajout d’une stratégie. |
| UpdatePolicy |Mise à jour d’une stratégie. |
| DeletePolicy |Suppression d’une stratégie. |
| AddDefaultPolicyApplication |Ajouter la stratégie tooapplication. |
| AddDefaultPolicyServicePrincipal |Ajoutez stratégie tooservice principal. |
| RemoveDefaultPolicyApplication |Suppression d’une stratégie d’application. |
| RemoveDefaultPolicyServicePrincipal |Suppression d’une stratégie de principal du service. |
| RemovePolicyCredentials |Suppression des informations d’identification d’une stratégie. |

## <a name="audit-report-retention"></a>Rétention des rapports d’audit

Pour plus d’informations plus récentes hello sur la rétention, consultez [stratégies de rétention de rapport Azure Active Directory](active-directory-reporting-retention.md).


Pour les clients intéressés par le stockage aux événements d’audit pour les périodes de rétention plus longues, hello API Reporting peut être tooregularly utilisé extraire des événements d’audit dans un magasin de données distinct. Consultez [prise en main de hello API Reporting](active-directory-reporting-api-getting-started.md) pour plus d’informations.

## <a name="properties-included-with-each-audit-event"></a>Propriétés incluses dans chaque événement d'audit
| Propriété | Description |
| --- | --- |
| Date et heure |date de Hello et l’heure qui hello d’événement d’audit s’est produite |
| Acteur |utilisateur de Hello ou principal du service qui a exécuté hello action |
| Action |action Hello qui a été effectuée |
| Cible |utilisateur de Hello ou principal du service qui hello action a été effectuée sur |

## <a name="update-user-attributes"></a>Attributs de « Mettre à jour l’utilisateur »
événement d’audit de Hello « mise à jour utilisateur » inclut des informations supplémentaires sur les attributs utilisateur ont été mis à jour. Pour chaque attribut, les deux hello valeur précédente et hello nouvelle valeur est inclus.

| Attribut | Description |
| --- | --- |
| AccountEnabled |utilisateur de Hello peut se connecter. |
| AssignedLicense |Toutes les licences qui ont été attribuées toohello utilisateur. |
| AssignedPlan |Plans de service obtenue à partir des licences hello affecté toohello utilisateur. |
| LicenseAssignmentDetail |Pour plus d’informations sur les licences affectées toohello utilisateur. Par exemple, si basée sur le groupe de licences a été impliquée, cela inclut groupe hello accordé hello licence. |
| Mobile |téléphone mobile de l’utilisateur Hello. |
| OtherMail |Bonjour adresse de messagerie de secours de l’utilisateur. |
| OtherMobile |Bonjour téléphone mobile secondaire de l’utilisateur. |
| StrongAuthenticationMethod |Liste des méthodes de vérification configuré par l’utilisateur de hello pour l’authentification multifacteur, tel que le code d’appel vocal, SMS ou vérification à partir d’une application mobile. |
| StrongAuthenticationRequirement |Dans le cas où l'authentification multi-facteur est appliquée, activée ou désactivée pour cet utilisateur |
| StrongAuthenticationUserDetails |l’utilisateur Hello phone par courrier électronique et le numéro de téléphone numérique, autre adresse utilisée pour l’authentification multifacteur et la vérification de réinitialisation de mot de passe. |
| StrongAuthenticationPhoneAppDetail |Applications de détail forof phone inscrits tooperform 2FA connexion |
| TelephoneNumber |numéro de téléphone de l’utilisateur Hello. |
| AlternativeSecurityId |Un autre ID de sécurité pour l’objet de hello. |
| CreationType |Méthode de création d’utilisateur hello (soit par invitation ou virales). |
| InviteTicket |Liste des tickets d’invitation pour l’utilisateur de hello. |
| InviteReplyUrl |Liste des tooreply URL après l’acceptation de l’invitation. |
| InviteResources |Liste des ressources toowhich hello utilisateur a été invitée. |
| LastDirSyncTime |Heure de la dernière hello objet a été mis à jour en raison de la synchronisation à partir de hello ne faisant pas autorité (client, sur site) active. |
| MSExchRemoteRecipientType |Mappe les types de destinataires tooMSO. Consultez trop https://msdn.microsoft.com/library/microsoft.office.interop.outlook.recipient.type.aspx [types de destinataires MSO] pour les types de destinataires |
| PreferredDataLocation |Bonjour à l’emplacement par défaut pour l’utilisateur hello, du groupe, du contact, du dossier public, ou les données de l’appareil. |
| ProxyAddresses |adresse Hello par lequel un objet de destinataire d’Exchange Server est reconnu dans un système de messagerie étranger. |
| StsRefreshTokensValidFrom |Transmet les informations de révocation des jetons d’actualisation : tous les jetons d’actualisation STS émis avant ce moment sont considérés comme expirés. |
| UserPrincipalName |Hello UPN est un nom d’ouverture de session Internet pour un utilisateur. |
| UserState |État de l’utilisateur : PendingApproval/PendingAcceptance/Accepted/PendingVerification (Approbation en cours/Acceptation en cours/Accepté/Vérification en attente). |
| UserStateChangedOn |Horodatage de dernière modification tooUserState. Flux de travail du cycle de vie tootrigger utilisé. |
| UserType |Type d’utilisateur. Membre (0), invité (1), viral (2). |

## <a name="update-group-attributes"></a>Attributs de mise à jour d’un groupe
| Attribut | Description |
| --- | --- |
| Classification |classification de Hello pour un groupe unifié (IEA, IMA, etc.). |
| Description |Phrases descriptives contrôlable de visu sur l’objet de hello. |
| DisplayName |nom d’affichage Hello pour un objet |
| DirSyncEnabled |Indique si la synchronisation se produit à partir d’un annuaire faisant autorité (client, local). |
| GroupLicenseAssignment |Attribution de licence d’un groupe. |
| GroupType |Type de groupe. Unifié (0). |
| IsMembershipRuleLocked |Indique que hello MembershipRule propriété est définie par le service de gestion de groupes en libre-service hello et ne peut pas être modifié par les utilisateurs. Applicable toogroups uniquement où GroupType inclut GroupType.DynamicMembership |
| IsPublic |Indicateur tooindicate si le groupe de hello est publique/privée. |
| LastDirSyncTime |Heure de la dernière hello objet a été mis à jour suite à la synchronisation à partir de hello ne faisant pas autorité (sur site, le client) active. |
| Mail |Adresse e-mail principale |
| MailEnabled |Indique si ce groupe est doté d’une fonctionnalité de messagerie. |
| MailNickname |Moniker pour un objet de carnet d’adresses, en général partie hello de son nom de messagerie qui précède hello « @ » symbole. |
| MembershipRule |Une chaîne d’expression de critères de hello utilisé par toodetermine de service de gestion de groupes en libre-service hello les membres doivent appartenir toothis groupe. Voir également IsMembershipRuleLocked. Toogroups uniquement applicable lorsque GroupType inclut GroupType.DynamicMembership. |
| MembershipRuleProcessingState |Valeur enum définie par le service de gestion de groupes en libre-service hello définition du statut de hello de l’appartenance au traitement de ce groupe. Toogroups uniquement applicable lorsque GroupType inclut GroupType.DynamicMembership. |
| ProxyAddresses |adresse Hello par lequel un objet de destinataire d’Exchange Server est reconnu dans un système de messagerie étranger. |
| RenewedDateTime |Horodatage du renouvellement le plus récent d’un groupe. |
| SecurityEnabled |Indique si l’appartenance au groupe de hello peut-être influencer les décisions d’autorisation. |
| WellKnownObject |Qualifie un objet d’annuaire selon un ensemble prédéfini d’objets. |

## <a name="update-device-attributes"></a>Attributs de mise à jour d’un appareil
| Attribut | Description |
| --- | --- |
| AccountEnabled |Indique si un principal de sécurité peut s’authentifier. |
| CloudAccountEnabled |Indique si un principal de sécurité peut s’authentifier. Écrits par InTune lorsque l’appareil de hello est masterisé sur site. |
| CloudDeviceOSType |Type de périphérique hello selon hello du système d’exploitation par exemple, Windows RT, iOS. Si la valeur par un service cloud (par exemple, Windows Intune), cet attribut devient faisant autorité dans le répertoire de hello pour DeviceOSType. |
| CloudDeviceOSVersion |Version de hello du système d’exploitation. Si la valeur par un service cloud (par exemple, Windows Intune), cet attribut devient faisant autorité dans le répertoire de hello pour DeviceOSVersion. |
| CloudDisplayName |Valeur d’un attribut LDAP hello displayName. Si la valeur par un service cloud (par exemple, Windows Intune), cet attribut devient faisant autorité dans le répertoire de hello pour displayName. |
| CloudCreated |Indique si l’objet de hello a été créé par les services cloud. |
| CompliantUntil |Indique jusqu’à quand l’appareil est jugé conforme. |
| DeviceMetadata |Métadonnées personnalisées pour les appareils hello |
| DeviceObjectVersion |Cet attribut est la version du schéma utilisé tooidentify hello du périphérique de hello. |
| DeviceOSType |Type de périphérique hello selon hello du système d’exploitation par exemple, Windows RT, iOS. Écrit par hello Service d’inscription et prévue toobe mis à jour par hello service de gestion de gestion des appareils mobiles ou STS clair service de gestion. |
| DeviceOSVersion |Version de hello du système d’exploitation. Écrit par hello Service d’inscription et prévue toobe mis à jour par hello service de gestion de gestion des appareils mobiles ou STS clair service de gestion. |
| DevicePhysicalIds |Attribut à valeurs multiples destiné toostore les identificateurs de l’unité physique de hello. Ceux-ci peuvent inclure des ID de BIOS, des empreintes de TPM, des ID matériels spécifiques, etc. |
| DirSyncEnabled |Indique si la synchronisation se produit à partir d’un annuaire faisant autorité (client, local). |
| DisplayName |nom d’affichage Hello pour un objet |
| IsCompliant |Cet attribut est l’état gestion des appareils mobiles utilisés toomanage hello du périphérique de hello. |
| IsManaged |Cet attribut est utilisé appareil de hello tooindicate est géré par un cloud MDM. |
| LastDirSyncTime |Heure de la dernière hello objet a été mis à jour en raison de la synchronisation à partir de hello ne faisant pas autorité (sur site, le client) active. |

## <a name="update-device-configuration-attributes"></a>Attributs de mise à jour d’une configuration d’appareil
| Attribut | Description |
| --- | --- |
| MaximumRegistrationInactivityPeriod |nombre maximal de Hello de jours pendant lesquels un appareil peut être inactif avant d’être considérée pour la suppression. |
| RegistrationQuota |Stratégie utilisée toolimit hello quantité, pour les inscriptions d’appareils autorisée pour un seul utilisateur. |

## <a name="update-service-principal-configuration-attributes"></a>Attributs de mise à jour d’une configuration de principal du service
| Attribut | Description |
| --- | --- |
| AccountEnabled |Indique si un principal de sécurité peut s’authentifier. |
| AppPrincipalId |Identité externe, définie par une application, pour un principal de sécurité. |
| DisplayName |nom d’affichage Hello pour un objet |
| ServicePrincipalName |Un nom principal de service, qui contient « nom/authority » où nom indique une valeur de classe d’application et autorité contienne au moins nom d’hôte [ : port] ou « nom » qui spécifie un identificateur de principal du service hello. |

## <a name="update-app-attributes"></a>Attributs de mise à jour d’une application
| Attribut | Description |
| --- | --- |
| AppAddress |ensemble de Hello d’adresses (URL de redirection) assignés tooa principal du service. |
| AppId |ID d’application de hello application |
| AppIdentifierUri |Application URI, qui identifie l’application hello.  Il est généralement l’accès URL de l’application hello. |
| AppLogoUrl |url de Hello pour l’image du logo application hello stockée dans un réseau CDN. |
| AvailableToOtherTenants |Application hello true est une application mutualisée (peuvent être utilisés à d’autres locataires). |
| DisplayName |nom d’affichage Hello pour un nom d’Application |
| Entitlement |Liste des droits de l’application. |
| ExternalUserAccountDelegationsAllowed |Indicateur spécifiant si application de ressources est approuvée et peut créer des entrées de délégation pour des comptes d’utilisateur externes. |
| GroupMembershipClaims |stratégie de revendications de l’appartenance de groupe de Hello. |
| PublicClient |True si le client de hello ne peut pas garder secret (autrement dit, un client non confidentielle dans OAuth2.0) |
| RecordConsentConditions |Termes du contrat de types de conditions de consentement, tel que défini par hello : aucun (0), SilentConsentForPartnerManagedApp(1). Cette valeur sera exposée dans le schéma de l’API Graph hello et ne peut être ensemble/modifié par les administrateurs de clients. |
| RequiredResourceAccess |Contenu XML d’une valeur de hello RequiredResourceAccess propriété. |
| WebApp |S’il est défini sur true, cet attribut indique que cette application est une application web. |
| WwwHomepage |page Web de la principale Hello. |

## <a name="update-role-attributes"></a>Attributs de mise à jour d’un rôle
| Attribut | Description |
| --- | --- |
| AppAddress |ensemble de Hello d’adresses (URL de redirection) assignés tooa principal du service. |
| BelongsToFirstLoginObjectSet |Si la valeur est true, indique que cet objet appartienne ensemble toohello de connexion de tooenable requis d’objets de hello premier administrateur d’un nouveau locataire. |
| Builtin |Indique si durée de vie d’un objet de hello est détenue par le système de hello. |
| Description |Phrases descriptives contrôlable de visu sur l’objet de hello. |
| DisplayName |nom d’affichage Hello pour un objet |
| MailNickname |Moniker pour un objet de carnet d’adresses, en général partie hello de son nom de messagerie qui précède hello « @ » symbole. |
| RoleDisabled |Indique si le rôle de hello doit être ignorée à des fins de vérifications d’accès. |
| RoleTemplateId |Identité du modèle de rôle hello. |
| ServiceInfo |Les informations qui peuvent être consommées par MOAC et/ou d’autres instances de service de configuration spécifiques au service (Hello identiques ou différents types de service). |
| TaskSetScopeReference |Identifie un ensemble de tâches et un ensemble d’étendues associées à un rôle ou un modèle de rôle. |
| ValidationError |Informations publiées par un service fédéré décrivant une erreur non temporaire, spécifique au service en ce qui concerne les propriétés hello ou un lien à partir d’un tooresolve d’action d’administrateur objet. |
| WellKnownObject |Qualifie un objet d’annuaire selon un ensemble prédéfini d’objets. |

## <a name="update-role-definition-attributes"></a>Attributs de mise à jour d’une définition de rôle
| Attribut | Description |
| --- | --- |
| AssignableScopes |Collection d’étendues d’autorisation qui peuvent être référencées lors de l’affectation de cette entité de sécurité tooa RoleDefinition. |
| DisplayName |nom d’affichage Hello pour un objet |
| GrantedPermissions |Autorisations accordées par cette définition de rôle. |

## <a name="update-administrative-unit-attributes"></a>Attributs de mise à jour d’une unité administrative
| Attribut | Description |
| --- | --- |
| Description |Cette propriété est mise à jour lorsque vous modifiez la description de hello d’une unité administrative. |
| DisplayName |Cette propriété est mise à jour lorsque vous modifiez le nom hello d’une unité administrative. |

## <a name="update-company-attributes"></a>Attributs de mise à jour de paramètres d’entreprise
| Attribut | Description |
| --- | --- |
| AllowedDataLocation |Un emplacement dans le hello utilisateurs de l’entreprise sont autorisés à toobe configuré. |
| AuthorizedServiceInstance |Noms des instances de service toowhich un plan peuvent être déployés. |
| DirSyncEnabled |Indique si la synchronisation se produit à partir d’un annuaire faisant autorité (client, local). |
| DirSyncStatus |Indique si la synchronisation des objets de carnet d’adresse dans ce contexte client se produit à partir d’un autorité (client, sur site) Active ; une extension de la propriété DirSyncEnabled sur les objets de la société de hello. |
| DirSyncFeatures |Bit indicateur tookeep effectuer le suivi de l’ensemble de fonctionnalités de synchronisation d’annuaire activés et désactivés pour le client de hello. |
| DirectoryFeatures |Fonctionnalités d’annuaire activées ou désactivées. |
| DirSyncConfiguration |Contient tous les clients en cours DirSync configuration toohello spécifique. |
| DisplayName |nom d’affichage Hello pour un objet |
| IsMnc |Indicateur booléen ensemble trop « true » si hello entreprise est activée pour la fonctionnalité d’entreprise multinationale hello. |
| ObjectSettings |Collection de portée toohello applique des paramètres d’objet de hello. |
| PartnerCommerceUrl |Site de commerce du partenaire URL toohello. |
| PartnerHelpUrl |Site d’aide du partenaire URL toohello. |
| PartnerSupportEmail |Adresse de messagerie du partenaire URL toohello prise en charge. |
| PartnerSupportTelephone |Téléphone du support technique du partenaire URL toohello. |
| PartnerSupportUrl |Site du support technique du partenaire URL toohello. |
| StrongAuthenticationDetails |Informations relatives à tooStrongAuthentication. |
| StrongAuthenticationPolicy |Stratégie de l’authentification forte pour l’entreprise hello. |
| TechnicalNotificationMail |Courrier électronique adresse toonotify problèmes techniques concernant tooa entreprise. |
| TelephoneNumber |Numéros de téléphone qui sont conformes aux hello E.123 de recommandation ITU. |
| TenantType |type Hello d’un locataire. Si cette valeur n’est pas spécifiée, le client de hello est une société. Sinon, les valeurs possibles sont : MicrosoftSupport (0), SyndicatePartner (1), BreadthPartner (2) BreadthPartnerDelegatedAdmin (3) ResellerPartnerDelegatedAdmin (4) ValueAddedResellerPartnerDelegatedAdmin (5). |
| VerifiedDomain |Un jeu de noms de domaine DNS lié tooa entreprise. |

## <a name="update-domain-attributes"></a>Attributs de mise à jour de domaine
| Attribut | Description |
| --- | --- |
| Fonctionnalités |Bits indicateurs décrivant hello fonctionnalités de hello domaine, le cas échéant. |
| Default |Indique si le domaine de hello est par défaut hello ; par exemple, hello suffixe par défaut UserPrincipalName lorsqu’un administrateur crée un nouvel utilisateur dans MOAC. |
| Initial |Indique si le domaine de hello est domaine initial de hello pour entreprise de hello, alloué par OCP. domaine initial de Hello est un sous-domaine unique d’un domaine Microsoft Online ; e.g.contoso3.microsoftonline.com. |
| LiveType |Type de hello Windows Live espace de noms correspondant, le cas échéant. |
| Nom |Identificateur de point de terminaison hello. |
| PasswordNotificationWindowDays |nombre de Hello de jours avant l’expiration de mot de passe utilisateur de hello est averti. |
| PasswordValidityPeriodDays |Bonjour le nombre de jours pendant lesquels qu'un mot de passe est correct pour avant qu’elle doit être modifiée. |

Les enregistrements d'audit sont un contrôle requis pour de nombreuses réglementations de conformité. Pour les clients à l’aide de hello rapport Azure Active Directory auditer toomeet leurs réglementations de conformité, il est recommandé que le client hello envoyer une copie de cette rubrique d’aide avec la copie de hello du client hello exporté le rapport d’audit toohelp expliquent les rapports hello Détails. Si hello qu’aux réglementations de conformité toounderstand hello répondant Azure actuellement, diriger hello auditeur toohello [page conformité](https://azure.microsoft.com/support/trust-center/compliance/) Hello Microsoft Azure Trust Center.

