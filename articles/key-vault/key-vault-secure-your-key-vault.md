---
title: "votre clé de coffre aaaSecure | Documents Microsoft"
description: "Gérez les autorisations d’accès à un coffre de clés pour la gestion des clés et des secrets. Modèle d’autorisation et d’authentification pour le coffre de clés et comment toosecure votre clé de coffre"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e5b4e083-4a39-4410-8e3a-2832ad6db405
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 84f5fc18142a1ad89babbd11f4f65eca105afc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-key-vault"></a>Sécuriser votre coffre de clés
Azure Key Vault est un service cloud qui protège les clés et secrets de chiffrement (tels que les certificats, les chaînes de connexion et les mots de passe) de vos applications cloud. Étant donné que ces données sont sensibles et critiques, vous voulez les coffres de clé de tooyour accès toosecure afin que seules les applications et les utilisateurs peuvent accéder au coffre de clés. Cet article fournit une vue d’ensemble du modèle de coffre de clés d’accès, explique l’authentification et l’autorisation et décrit comment toosecure accès tookey coffre pour vos applications cloud avec un exemple.

## <a name="overview"></a>Vue d'ensemble
Coffre de clés tooa accès est contrôlé par deux interfaces distinctes : plan de la gestion et plan de données. Pour les deux plans d’autorisation et d’authentification appropriée est nécessaire pour un appelant (un utilisateur ou une application) peut obtenir tookey forte. L’authentification établit l’identité hello de l’appelant de hello, tandis que l’autorisation détermine quel appelant de hello operations est autorisée tooperform.

Pour l’authentification, le plan de gestion et le plan de données font tous deux appel à Azure Active Directory. Pour l’autorisation, le plan de gestion utilise le contrôle d’accès en fonction du rôle (RBAC), tandis que le plan de données s’appuie sur la stratégie d’accès au coffre de clés.

Voici une brève vue d’ensemble de rubriques hello :

[Authentification à l’aide d’Azure Active Directory](#authentication-using-azure-active-directory) -cette section explique comment un appelant s’authentifie avec Azure Active Directory tooaccess un coffre de clés via un plan de la gestion et plan de données. 

[Plan de gestion et plan de données](#management-plane-and-data-plane) : le plan de gestion et le plan de données sont deux plans d’accès utilisés pour accéder à votre coffre de clés. Chaque plan d’accès prend en charge des opérations spécifiques. Cette section décrit les points de terminaison hello accès, la prise en charge des opérations et accéder à la méthode de contrôle utilisée par chaque plan. 

[Contrôle d’accès de plan de gestion](#management-plane-access-control) : dans cette section, nous allons examiner les opérations de plan toomanagement à l’aide du contrôle d’accès en fonction du rôle d’accès.

[Contrôle d’accès aux données plan](#data-plane-access-control) -cette section décrit la façon dont les données de toocontrol toouse coffre de clés accès stratégie plan accès.

[Exemple](#example) -cet exemple décrit comment toosetup contrôle d’accès pour votre coffre de clés tooallow trois différentes équipes (équipe de sécurité, les développeurs/opérateurs et auditeurs) tooperform toodevelop de tâches spécifiques, gérer et surveiller une application dans Azure .

## <a name="authentication-using-azure-active-directory"></a>Authentification à l’aide d’Azure Active Directory
Lorsque vous créez un coffre de clés dans un abonnement Azure, il est automatiquement associé au locataire Azure Active Directory de l’abonnement hello. Tous les appelants (utilisateurs et applications) doivent être enregistré dans cette tooaccess client ce coffre de clés. Une application ou un utilisateur doit s’authentifier avec le coffre de clés Azure Active Directory tooaccess. Cela s’applique le plan de gestion de tooboth et plan de données access. Dans les deux cas, une application peut accéder au coffre de clés de deux manières :

* **Accès de l’utilisateur et de l’application** : concerne généralement les applications qui accèdent au coffre de clés pour le compte d’un utilisateur connecté. Azure PowerShell et le portail Azure sont des exemples de ce type d’accès. Il existe deux façons toogrant accès toousers : unidirectionnel est toogrant accès toousers afin qu’ils peuvent accéder au coffre de clés à partir de n’importe quelle application et hello autrement toogrant un coffre de tookey d’accès utilisateur uniquement lorsqu’ils utilisent une application spécifique (tooas auxquels l’identité composée). 
* **accès uniquement par l’application** - pour les applications qu’exécuter les services du démon, tâches en arrière-plan a l’identité de l’application hello etc. accéder toohello clé de coffre.

Dans les deux types d’applications, application hello s’authentifie auprès d’Azure Active Directory à l’aide de hello [prise en charge des méthodes d’authentification](../active-directory/active-directory-authentication-scenarios.md) et acquiert un jeton. Méthode d’authentification utilisée dépend du type d’application hello. Application hello utilise ce jeton puis envoie le coffre de tookey demande API REST. En cas de hello d’accès Gestion plan sont routées via le point de terminaison Azure Resource Manager. Lors de l’accès aux données, les applications hello communique directement tooa point de terminaison de coffre de clés. Afficher plus de détails sur hello [flux d’authentification entier](../active-directory/active-directory-protocols-oauth-code.md). 

nom de la ressource Hello pour lequel application hello demande un jeton est différent selon qu’application hello est accédez à Gestion plan ou un plan de données. Par conséquent, nom de la ressource hello est soit gestion plan ou données plan point de terminaison décrite dans la table hello dans une section ultérieure, en fonction de hello environnement Azure.

Ayant un mécanisme unique pour l’authentification tooboth le plan de gestion et de données a ses propres avantages :

* Les organisations peuvent contrôler de manière centralisée accès coffres de clé tooall dans leur organisation.
* Si un utilisateur quitte, ils instantanément perdent l’accès tooall les coffres de clé dans l’organisation de hello
* Les organisations peuvent personnaliser l’authentification via des options de hello dans Azure Active Directory (par exemple, ce qui permet l’authentification multifacteur pour renforcer la sécurité)

## <a name="management-plane-and-data-plane"></a>Plan de gestion et plan de données
Azure Key Vault est un service Azure disponible via le modèle de déploiement Azure Resource Manager. Lorsque vous créez un coffre de clés, vous obtenez un conteneur virtuel à l’intérieur duquel vous pouvez créer d’autres objets tels que des clés, des secrets et des certificats. Puis vous accéder à votre coffre de clés à l’aide de la gestion des données et le plan plan tooperform des opérations spécifiques. Interface de gestion de plan est utilisé toomanage votre clé de coffre lui-même, telles que la création, la suppression, la mise à jour des attributs de coffre de clés et la définition de stratégies d’accès pour le plan de données. Interface de plan de données est utilisé tooadd, supprimer, modifier et utiliser les certificats stockés dans votre coffre de clés, les secrets et les clés de hello.

Hello plan et les données de plan des interfaces de gestion sont accessibles via différents points de terminaison (voir tableau). Hello deuxième colonne hello tableau décrit les noms DNS hello pour ces points de terminaison dans différents environnements Azure. Hello troisième colonne décrit les opérations hello que vous pouvez effectuer à partir de chaque plan d’accès. Chaque plan d’accès présente également son propre mécanisme de contrôle d’accès : pour le plan de gestion, le contrôle d’accès est défini à l’aide du contrôle d’accès en fonction du rôle (RBAC) Azure Resource Manager, tandis que pour le plan de données, il est défini à l’aide de la stratégie d’accès au coffre de clés.

| Plan d’accès | Points de terminaison d’accès | Opérations | Mécanisme de contrôle d’accès |
| --- | --- | --- | --- |
| Plan de gestion |**Mondial :**<br> management.azure.com:443<br><br> **Azure China :**<br> management.chinacloudapi.cn:443<br><br> **Azure US Government :**<br> management.usgovcloudapi.net:443<br><br> **Azure Germany :**<br> management.microsoftazure.de:443 |Créer/lire/mettre à jour/supprimer un coffre de clés <br> Définir des stratégies d’accès pour un coffre de clés<br>Définir des balises pour un coffre de clés |Contrôle d’accès en fonction du rôle (RBAC) Azure Resource Manager |
| Plan de données |**Mondial :**<br> &lt;nom du coffre&gt;.vault.azure.net:443<br><br> **Azure China :**<br> &lt;nom du coffre&gt;.vault.azure.cn:443<br><br> **Azure US Government :**<br> &lt;nom du coffre&gt;.vault.usgovcloudapi.net:443<br><br> **Azure Germany :**<br> &lt;nom du coffre&gt;.vault.microsoftazure.de:443 |Pour les clés : Decrypt, Encrypt, UnwrapKey, WrapKey, Verify, Sign, Get, List, Update, Create, Import, Delete, Backup, Restore<br><br> Pour les secrets : Get, List, Set, Delete |Stratégie d’accès au coffre de clés |

Hello Gestion plan et les données de plan des contrôles d’accès fonctionnent indépendamment. Par exemple, si vous souhaitez toogrant une application access toouse les clés dans un coffre de clés, vous devez uniquement des autorisations d’accès du plan de données toogrant à l’aide de stratégies d’accès de coffre de clés et aucun accès de plan de gestion n’est nécessaire pour cette application. Et à l’inverse, si vous souhaitez un toobe utilisateur en mesure de tooread coffre des balises et des propriétés, mais ne dispose pas des accès tookeys, secrets ou des certificats, vous pouvez accorder à cet utilisateur, accès « lecture » à l’aide de RBAC et aucun plan de toodata d’accès est requis.

## <a name="management-plane-access-control"></a>Contrôle d’accès au plan de gestion
plan de gestion Hello se compose d’opérations qui affectent le coffre de clés hello lui-même. Par exemple, vous pouvez créer ou supprimer un coffre de clés. Vous pouvez obtenir la liste des coffres d’un abonnement. Vous pouvez récupérer les propriétés de coffre de clés (par exemple, la référence (SKU), les balises) et définir des stratégies d’accès qui contrôlent les utilisateurs hello et les applications qui peuvent accéder aux clés et les clés secrètes dans le coffre de clés hello de coffre de clés. Le contrôle d’accès au plan de gestion utilise la fonctionnalité RBAC. Consultez la liste complète des opérations de coffre de clés qui peuvent être effectuées via le plan de gestion dans la table hello dans la précédente section hello. 

### <a name="role-based-access-control-rbac"></a>Contrôle d’accès en fonction du rôle (RBAC)
À chaque abonnement Azure correspond un annuaire Azure Active Directory. Les utilisateurs, des groupes et des applications à partir de ce répertoire peuvent être accordées à accéder aux toomanage ressources hello abonnement Azure qui utilisent le modèle de déploiement du Gestionnaire de ressources Azure hello. Ce type de contrôle d’accès est référencé tooas contrôle d’accès en fonction du rôle (RBAC). toomanage cela accéder, vous pouvez utiliser hello [portail Azure](https://portal.azure.com/), hello [outils CLI d’Azure](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), ou hello [API REST de gestionnaire de ressources Azure](https://msdn.microsoft.com/library/azure/dn906885.aspx).

Avec le modèle de gestionnaire de ressources Azure hello, créer votre coffre de clés dans une ressource groupe et contrôle d’accès toohello Gestion plan de ce coffre de clés à l’aide d’Azure Active Directory. Par exemple, vous pouvez accorder des utilisateurs ou un coffres de clé de toomanage possibilité de groupe dans un groupe de ressources spécifique.

Vous pouvez accorder l’accès toousers, des groupes et des applications à une étendue spécifique en attribuant des rôles RBAC appropriés. Par exemple, toogrant accéder aux clés coffres tooa utilisateur toomanage vous devez attribuer un rôle prédéfini 'coffre de clés collaborateur' utilisateur toothis à une étendue spécifique. étendue de Hello dans ce cas serait un abonnement, un groupe de ressources ou simplement un coffre de clés spécifique. Un rôle affecté au niveau de l’abonnement s’applique tooall les groupes de ressources et des ressources de cet abonnement. Un rôle affecté au niveau de groupe de ressources s’applique tooall des ressources dans ce groupe de ressources. Un rôle attribué pour une ressource spécifique s’applique uniquement à des ressources de toothat. Il existe plusieurs rôles prédéfinis (consultez [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md)), et si hello des rôles prédéfinis ne tiennent pas vos besoins, vous pouvez également définir vos propres rôles.

> [!IMPORTANT]
> Notez que si un utilisateur a un plan de gestion de coffre de clés collaborateur autorisations (RBAC) tooa, elle peut s’accorder plan toodata d’accès, en définissant la stratégie d’accès de coffre de clés, qui contrôle le plan de toodata d’accès. Par conséquent, il est recommandé de contrôler tootightly 'Collaborateur' accès tooyour coffres de clé tooensure seules personnes autorisées peuvent accéder et gérer votre coffres de clé, les clés, les secrets et les certificats.
> 
> 

## <a name="data-plane-access-control"></a>Contrôle d’accès au plan de données
plan de données de coffre de clés Hello se compose d’opérations qui affectent les objets hello dans un coffre de clés, telles que des clés, des secrets et des certificats.  Cela inclut les opérations liées aux clés (création, importation, mise à jour, énumération, sauvegarde et restauration de clés, par exemple), les opérations de chiffrement (signature, vérification, chiffrement, déchiffrement, encapsulage, désencapsulage, etc.), ainsi que la définition de balises et d’autres attributs pour les clés. De même, pour les secrets, le plan de données comprend les opérations get, set, list et delete.

L’accès au plan de données est octroyé en définissant des stratégies d’accès pour un coffre de clés. Un utilisateur, groupe ou une application doit avoir des autorisations de collaborateur (RBAC) pour le plan de gestion un coffre de clés toobe tooset en mesure de politiques d’accès pour ce coffre de clés. Un utilisateur, un groupe ou une application peut être accordée à accès tooperform des opérations spécifiques pour les clés ou les clés secrètes dans un coffre de clés. Coffre de clés prise en charge des entrées de stratégie d’accès too16 pour un coffre de clés. Créer un groupe de sécurité Azure Active Directory et ajouter les utilisateurs toothat groupe toogrant données plan accès tooseveral utilisateurs tooa coffre de clés.

### <a name="key-vault-access-policies"></a>Stratégies d’accès à un coffre de clés
Stratégies d’accès de coffre de clés accordent séparément des certificats, des secrets et des autorisations tookeys. Par exemple, vous pouvez donner un tooonly les clés d’accès utilisateur, mais pas d’autorisations pour les clés secrètes. Toutefois, les clés de tooaccess autorisations ou des clés secrètes ou des certificats sont au niveau du coffre hello. En d’autres termes, la stratégie d’accès à un coffre de clés ne prend pas en charge les autorisations de niveau objet. Vous pouvez utiliser [portail Azure](https://portal.azure.com/), hello [outils CLI d’Azure](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), ou hello [coffre de clés API REST de gestion](https://msdn.microsoft.com/library/azure/mt620024.aspx) tooset les stratégies d’accès pour un coffre de clés.

> [!IMPORTANT]
> Notez que les stratégies d’accès de coffre de clés s’appliquent au niveau du coffre hello. Par exemple, lorsqu’un utilisateur dispose de clés toocreate et suppression d’autorisation, elle peut effectuer les opérations sur toutes les clés dans ce coffre de clés.
> 
> 

## <a name="example"></a>Exemple
Supposons que vous développiez une application qui utilise un certificat pour SSL, le stockage Azure pour stocker des données et une clé RSA 2 048 bits pour les opérations de signature. Supposons que cette application s’exécute dans une machine virtuelle (ou un groupe de machines virtuelles identiques). Vous pouvez utiliser un toostore de coffre de clés que tous hello secrets de l’application et utiliser coffre de clés toostore hello amorçage un certificat qui est utilisé par tooauthenticate d’application hello avec Azure Active Directory.

Par conséquent, Voici un résumé de tous les toobe de clés et les secrets hello stockés dans un coffre de clés.

* **Certificat SSL** : utilisé pour le protocole SSL
* **Clé de stockage** -utilisé tooget accès tooStorage compte
* **Clé RSA 2 048 bits** : utilisée pour les opérations de signature
* **Certificat d’amorçage** -utilisé tooauthenticate tooAzure Active Directory, clé de stockage tooget accès tookey coffre toofetch hello et utiliser une clé RSA hello pour la signature.

Maintenant nous allons répondre aux hello utilisateurs de gérer, déployer et l’audit de cette application. Nous utiliserons trois rôles dans cet exemple.

* **L’équipe de sécurité** - il s’agit généralement de personnel informatique de hello 'bureau de hello responsable de la sécurité (sécurité directeur)', ou équivalent, responsable hello appropriée garde de secrets tels que les certificats SSL, les clés RSA utilisés pour la signature, les chaînes de connexion pour bases de données, les clés de compte de stockage.
* **Les développeurs/opérateurs** -il s’agit hello absents développement cette application, puis la déployer dans Azure. En règle générale, ne font pas partie de l’équipe de sécurité hello et par conséquent, ils ne doivent pas avoir accès tooany des données sensibles, telles que les certificats SSL, les clés RSA, mais application hello qu'ils déploient doit avoir accès toothose.
* **Auditeurs** -il s’agit généralement d’un ensemble différent de personnes, isolés des développeurs de hello et général du personnel informatique. Leur responsabilité est tooreview utilisation et maintenance des certificats, des clés, etc. et assurer la conformité aux normes de sécurité des données. 

Il existe un rôle plus étendue de hello en dehors de cette application, mais applique toobe ici mentionné, et qui serait un abonnement de hello (ou groupe de ressources) administrateur. Administrateur de l’abonnement définit des autorisations d’accès initial pour l’équipe de sécurité hello. Ici, nous supposons qu’administrateur d’abonnement hello a accordé l’accès toohello team tooa ressource groupe de sécurité dans lequel tous les hello des ressources nécessaires pour ce résident de l’application.

Maintenant nous allons voir quelles actions exécutées par chaque rôle de contexte hello de cette application.

* **Équipe de sécurité**
  * Création de coffres de clés
  * Activation de la journalisation de coffre de clés
  * Ajout de clés/secrets
  * Création d’une sauvegarde des clés pour la récupération d’urgence
  * Définir l’accès de coffre de clés stratégie toogrant autorisations toousers et applications tooperform des opérations spécifiques
  * Déploiement périodique de clés/secrets
* **Développeurs/opérateurs**
  * Obtenir des références toobootstrap et certificats SSL (empreintes numériques), clé de stockage (secret URI) et la signature de clé (clé URI) à partir de l’équipe de sécurité
  * Développement et déploiement d’une application qui accède aux clés et aux secrets par programmation
* **Auditeurs**
  * Passez en revue l’utilisation des journaux tooconfirm clé/secret utilisation et la conformité aux normes de sécurité des données

Maintenant nous allons voir forte tookey quelles autorisations sont requises par chaque rôle (et l’application hello) tooperform leurs tâches affectées. 

| Rôle d’utilisateur | Autorisations de plan de gestion | Autorisations de plan de données |
| --- | --- | --- |
| Équipe de sécurité |Collaborateur de coffre de clés |Clés : sauvegarde, création, suppression, obtention, importation, énumération, restauration <br> Secrets : toutes |
| Développeurs/opérateurs |coffre de clés déployer autorisation afin que les machines virtuelles de hello ils déploient peuvent extraire les secrets hello coffre de clés |Aucun |
| Auditeurs |Aucune |Clés : énumération<br>Secrets : énumération |
| Application |Aucune |Clés : énumération<br>Secrets : obtention |

> [!NOTE]
> Auditeurs doivent autorisation de liste de clés et les secrets afin qu’ils peuvent inspecter des attributs pour les clés et les secrets ne sont pas émis dans les journaux de hello, telles que les balises, les dates d’activation et d’expiration.
> 
> 

Outre le coffre de tookey d’autorisation, les trois rôles également besoin d’accès tooother ressources. Par exemple, toobe en mesure de toodeploy machines virtuelles (ou Web applications etc.). Les développeurs/opérateurs également besoin des types de ressources 'Collaborateur' accès toothose. Auditeurs avoir besoin de compte de stockage toohello accès en lecture sur lequel sont enregistrés les journaux de coffre de clés hello.

Étant donné que le coffre de clés tooyour accès concerne la sécurisation des focus hello de cet article, nous uniquement illustrent les parties pertinentes hello se rapportant toothis rubrique et ignorer les détails concernant le déploiement des certificats, l’accès aux clés et les secrets par programmation etc.. qui ont déjà été traités ailleurs. Déploiement de certificats stockés dans le coffre de clés tooVMs est traité dans un [billet de blog](https://blogs.technet.microsoft.com/kv/2016/09/14/updated-deploy-certificates-to-vms-from-customer-managed-key-vault/)et il est [exemple de code](https://www.microsoft.com/download/details.aspx?id=45343) disponibles qui illustre comment toouse amorçage certificat tooauthenticate tooAzure AD tooget tookey forte.

La plupart des autorisations d’accès hello peut être accordée à l’aide du portail Azure, mais vous devrez peut-être hello du tooachieve toouse Azure PowerShell (ou CLI d’Azure) des autorisations granulaires toogrant de résultat souhaité. 

Partons du principe Hello suivant des extraits de code PowerShell :

* administrateur d’Azure Active Directory Hello a créé des groupes de sécurité qui représentent les hello trois rôles, à savoir que Contoso équipe de sécurité, Contoso application Devops, Contoso application Auditors. administrateur de Hello a également ajouté des groupes de toohello les utilisateurs qu'auxquels ils appartiennent.
* **ContosoAppRG** est groupe de ressources hello où se trouvent toutes les ressources de hello. **contosologstorage** hello journaux sont stockées. 
* Coffre de clés **ContosoKeyVault** et compte de stockage utilisé pour les journaux de coffre de clés **contosologstorage** doit être Bonjour même emplacement

Premier administrateur de l’abonnement hello affecte coffre contributeur de la clé et l’équipe de sécurité de toohello rôles administrateur de l’accès utilisateur. Cela hello sécurité team toomanage accès tooother les ressources et gérer les coffres de clé dans le groupe de ressources hello ContosoAppRG.

```
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "key vault Contributor" -ResourceGroupName ContosoAppRG
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "User Access Administrator" -ResourceGroupName ContosoAppRG
```

Hello script suivant illustre comment l’équipe de sécurité hello peut créer un coffre de clés, le programme d’installation de journalisation et définir des autorisations d’accès pour les autres rôles et l’application hello. 

```
# Create key vault and enable logging
$sa = Get-AzureRmStorageAccount -ResourceGroup ContosoAppRG -Name contosologstorage
$kv = New-AzureRmKeyVault -VaultName ContosoKeyVault -ResourceGroup ContosoAppRG -SKU premium -Location 'westus' -EnabledForDeployment
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

# Data plane permissions for Security team
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -PermissionsToKeys backup,create,delete,get,import,list,restore -PermissionsToSecrets all

# Management plane permissions for Dev/ops
# Create a new role from an existing role
$devopsrole = Get-AzureRmRoleDefinition -Name "Virtual Machine Contributor"
$devopsrole.Id = $null
$devopsrole.Name = "Contoso App Devops"
$devopsrole.Description = "Can deploy VMs that need secrets from key vault"
$devopsrole.AssignableScopes = @("/subscriptions/<SUBSCRIPTION-GUID>")

# Add permission for dev/ops so they can deploy VMs that have secrets deployed from key vaults
$devopsrole.Actions.Add("Microsoft.KeyVault/vaults/deploy/action")
New-AzureRmRoleDefinition -Role $devopsrole

# Assign this newly defined role tooDev ops security group
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Devops')[0].Id -RoleDefinitionName "Contoso App Devops" -ResourceGroupName ContosoAppRG

# Data plane permissions for Auditors
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Auditors')[0].Id -PermissionsToKeys list -PermissionsToSecrets list
```

rôle personnalisé de Hello défini, il est uniquement l’abonnement peut être assigné toohello où le groupe de ressources ContosoAppRG hello est créé. Si hello mêmes rôles personnalisés seront utilisés pour d’autres projets dans d’autres abonnements, sa portée peut avoir plusieurs abonnements sont ajoutés.

attribution de rôles personnalisés Hello pour les développeurs/opérateurs hello pour obtenir l’autorisation « déployer/action » hello est un groupe de ressources toohello étendue. Ainsi uniquement hello VMs créé dans le groupe de ressources hello 'ContosoAppRG' obtenez les secrets hello (certificat SSL et certificat d’amorçage). Les ordinateurs virtuels qu’un membre de l’équipe de développement/ops crée dans un autre groupe de ressources ne sera pas en mesure de tooget ces clés secrètes même si connaît le secret hello URI.

Cet exemple illustre un scénario simple. Scénarios réels peuvent être plus complexes et vous devrez peut-être tooadjust autorisations tooyour coffre de clés en fonction de vos besoins. Par exemple, dans notre exemple, nous supposons que l’équipe de sécurité fournit la clé de hello et références secrets (URI et les empreintes numériques) qui tooreference de besoin les développeurs/opérateurs équipe dans leurs applications. Par conséquent, n’est nécessaire aux développeurs de toogrant/opérateurs tout accès de plan de données. Notez également que cet exemple se focalise sur la sécurisation de votre coffre de clés. Similaire doit être envisagé toosecure [vos machines virtuelles](https://azure.microsoft.com/services/virtual-machines/security/), [comptes de stockage](../storage/common/storage-security-guide.md) et d’autres ressources Azure trop.

> [!NOTE]
> Remarque : cet exemple montre comment l’accès au coffre de clés sera verrouillé en production. les développeurs de Hello doivent avoir leur propre abonnement ou le groupe de ressources où ils ont toomanage de toutes les autorisations leurs archivages, les machines virtuelles et les compte de stockage où ils développent application hello.
> 
> 

## <a name="resources"></a>Ressources
* [Contrôle d’accès en fonction du rôle Azure Active Directory](../active-directory/role-based-access-control-configure.md)
  
  Cet article explique hello de contrôle d’accès basé sur un rôle Active Directory de Azure et de son fonctionnement.
* [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md)
  
  Cet article explique les hello rôles intégrés disponibles dans RBAC.
* [Présentation du déploiement de Resource Manager et du déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md)
  
  Cet article explique le déploiement du Gestionnaire de ressources hello et modèles de déploiement classique et explique les avantages de hello de l’utilisation de groupes de gestion de ressources et les ressources hello
* [Gestion du contrôle d’accès en fonction du rôle (RBAC) avec Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  
  Cet article explique comment toomanage basée sur le rôle de contrôle d’accès avec Azure PowerShell
* [Gestion du contrôle d’accès en fonction du rôle avec l’API REST de hello](../active-directory/role-based-access-control-manage-access-rest.md)
  
  Cet article explique comment toouse hello API REST toomanage RBAC.
* [Role-Based Access Control for Microsoft Azure from Ignite (Contrôle d’accès en fonction du rôle pour Microsoft Azure)](https://channel9.msdn.com/events/Ignite/2015/BRK2707)
  
  Il s’agit d’un lien de tooa vidéo sur Channel 9 à partir de la conférence de Ignite 2015 MS hello. Dans cette session, ils parlent accéder aux fonctionnalités de gestion et création de rapports dans Azure et Explorer les meilleures pratiques pour la sécurisation de l’accès tooAzure les abonnements à l’aide d’Azure Active Directory.
* [Autoriser les applications tooweb à l’aide d’OAuth 2.0 et Azure Active Directory](../active-directory/active-directory-protocols-oauth-code.md)
  
  Cet article décrit le flux OAuth 2.0 complet pour l’authentification auprès d’Azure Active Directory.
* [API REST de gestion de coffre de clés](https://msdn.microsoft.com/library/azure/mt620024.aspx)
  
  Ce document est référence hello pour toomanage d’API REST hello votre clé de coffre par programme, notamment en définissant la stratégie d’accès au coffre de clés.
* [API REST de coffre de clés](https://msdn.microsoft.com/library/azure/dn903609.aspx)
  
  Coffre de tookey lien documentation de référence API REST.
* [Contrôle d’accès aux clés](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_KeyAccessControl)
  
  Lien tooSecret accès contrôle documentation de référence.
* [Contrôle d’accès aux secrets](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_SecretAccessControl)
  
  Lien tooKey accès contrôle documentation de référence.
* [Définition](https://msdn.microsoft.com/library/mt603625.aspx) et [suppression](https://msdn.microsoft.com/library/mt619427.aspx) de la stratégie d’accès au coffre de clés à l’aide de PowerShell
  
  Documentation de tooreference de liens pour la stratégie d’accès PowerShell applets de commande toomanage coffre de clés.

## <a name="next-steps"></a>Étapes suivantes
Pour un didacticiel de prise en main destiné aux administrateurs, consultez la page [Prise en main d’Azure Key Vault](key-vault-get-started.md).

Pour plus d’informations sur l’utilisation de la journalisation du coffre de clés, consultez [Journalisation d’Azure Key Vault](key-vault-logging.md).

Pour plus d’informations sur l’utilisation des clés et des secrets avec un coffre de clés Azure, consultez la page [À propos des clés et des clés secrètes](https://msdn.microsoft.com/library/azure/dn903623.aspx).

Si vous avez des questions sur le coffre de clés, visitez hello [coffre de clés Azure Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)

