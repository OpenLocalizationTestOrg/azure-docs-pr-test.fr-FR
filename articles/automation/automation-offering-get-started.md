---
title: AAA prise en main Azure Automation | Documents Microsoft
description: "Cet article fournit une vue d’ensemble du service Azure Automation en passant en revue les détails de conception et d’implémentation hello Bonjour tooonboard de préparation de l’offre à partir d’Azure Marketplace."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 434e8ea28c55ff9bda1d2e46a7a6b8378a3baa0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation"></a>Prise en main d'Azure Automation

Ce guide de mise en route présente les principaux concepts connexes toohello déploiement d’Azure Automation. Si vous tooAutomation nouvelle dans Azure ou avez une expérience de logiciels System Center Orchestrator de flux de travail automation, ce guide vous aide à comprendre comment tooprepare et l’automatisation intégrée.  Ensuite, vous serez prêt toobegin procédures opérationnelles pour prendre en charge vos besoins d’automatisation de processus de développement. 


## <a name="automation-architecture-overview"></a>Présentation de l’architecture Automation

![Vue d’ensemble d’Azure Automation](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

Azure Automation est un logiciel en tant qu’une application de service (SaaS) qui fournit une architecture mutualisée évolutive et fiable, environnement tooautomate traite avec des runbooks et gérer tooWindows des modifications de configuration et les systèmes Linux à l’aide de la Configuration d’état souhaité (DSC) dans les services de cloud computing Azure, les autres ou sur site. Les entités contenues dans votre compte Automation, telles que les Runbooks, les ressources et les comptes d’identification, sont isolées des autres comptes Automation de votre abonnement et d’autres abonnements.  

Les Runbooks que vous exécutez dans Azure sont exécutés dans des bacs à sable Automation, qui sont hébergés sur les machines virtuelles PaaS Azure.  Les bacs à sable Automation permettent d’isoler les clients pour tous les aspects de l’exécution du Runbook : modules, stockage, mémoire, communication réseau, flux de travail, etc. Ce rôle est géré par le service de hello et n’est pas accessible à partir de votre compte Azure ou Azure Automation pour vous toocontrol.         

déploiement de hello tooautomate et gestion des ressources dans votre centre de données local ou d’autres services de cloud computing, après la création d’un compte Automation, vous pouvez désigner un ou plusieurs hello toorun de machines [travail de Runbook hybride (HRW)](automation-hybrid-runbook-worker.md) rôle.  Chaque HRW requiert hello Microsoft Management Agent avec un espace de travail de connexion tooa Analytique de journal et un compte Automation.  Analytique de journal est utilisé toobootstrap hello installation, de mettre à jour hello Microsoft Management Agent et surveiller la fonctionnalité hello Hello HRW.  remise Hello de procédures opérationnelles et hello toorun instruction que les sont effectuées par Azure Automation.

Vous pouvez déployer plusieurs HRW tooprovide disponibilité pour les procédures opérationnelles, travaux équilibre de charge et dans certains cas dédier les charges de travail particuliers pour les environnements.  Hello Microsoft Monitoring Agent sur hello HRW lance la communication avec hello service Automation via le port TCP 443, et il n’existe aucune exigence de pare-feu entrantes.  Une fois que vous avez runbook en cours d’exécution sur un HRW au sein de l’environnement de hello et que vous voulez que les tâches de gestion hello runbook tooperform par rapport à d’autres ordinateurs ou des services au sein de cet environnement, il peut être d’autres ports hello runbook a besoin d’accéder à.  Si vos stratégies de sécurité informatique n’autorisent pas les ordinateurs sur votre toohello de tooconnect réseau Internet, passez en revue l’article de hello [OMS passerelle](../log-analytics/log-analytics-oms-gateway.md), qui agit comme un proxy pour hello HRW toocollect état du travail et recevoir des informations de configuration à partir de votre compte Automation.

Procédures opérationnelles en cours d’exécution sur un HRW s’exécutent dans le contexte de hello du compte système local de hello sur l’ordinateur de hello, qui est hello recommandé de contexte de sécurité lors de l’exécution des actions d’administration sur l’ordinateur de Windows hello local. Si vous souhaitez que les tâches de toorun hello exécutables contre des ressources en dehors de l’ordinateur local de hello, vous devrez peut-être actifs des informations d’identification sécurisées toodefine Bonjour compte Automation que vous pouvez accéder à partir de runbook de hello et utiliser tooauthenticate avec les ressources externes hello. Vous pouvez utiliser [informations d’identification](automation-credentials.md), [certificat](automation-certificates.md), et [connexion](automation-connections.md) actifs dans votre runbook avec les applets de commande qui permettent d’informations d’identification toospecify afin de les authentifier.

Les configurations DSC stockées dans Azure Automation peuvent être appliquées directement tooAzure des machines virtuelles. Autres machines physiques et virtuelles peuvent demander des configurations de serveur de collecteur Azure Automation DSC hello.  Pour la gestion des configurations de vos systèmes sur site physiques ou virtuels Windows et Linux, vous n’avez pas besoin toodeploy infrastructure toosupport hello Automation DSC par extraction de données serveur quelconque, uniquement un accès Internet sortant à partir de chaque toobe système géré par Automation DSC , communiquent via le service OMS toohello TCP port 443.   

## <a name="prerequisites"></a>Composants requis

### <a name="automation-dsc"></a>Automation DSC
Azure Automation DSC peut être utilisé toomanage différents ordinateurs :

* Machines virtuelles Azure (classique) exécutant Windows ou Linux
* Machines virtuelles Azure exécutant Windows ou Linux
* Machines virtuelles Amazon Web Services (AWS) exécutant Windows ou Linux
* Ordinateurs physiques/virtuels Windows en local ou dans un cloud autre qu’Azure ou AWS
* Ordinateurs physiques/virtuels Linux en local ou dans un cloud autre qu’Azure ou AWS

Hello dernière version de WMF 5 doit être installée pour l’agent de DSC PowerShell hello pour toocommunicate en mesure de Windows toobe avec Azure Automation. version la plus récente de hello Hello [agent PowerShell DSC pour Linux](https://www.microsoft.com/en-us/download/details.aspx?id=49150) doit être installé pour toocommunicate en mesure de Linux toobe avec Azure Automation.

### <a name="hybrid-runbook-worker"></a>Runbook Worker hybride  
Lorsque vous désignez un runbook hybride de toorun ordinateur travaux, cet ordinateur doit disposer de hello :

* Windows Server 2012 ou version ultérieure
* Windows PowerShell 4.0 ou version ultérieure.  Nous vous recommandons d’installer Windows PowerShell 5.0 sur ordinateur hello pour garantir une fiabilité accrue. Vous pouvez télécharger la nouvelle version de hello de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=50395)
* Deux cœurs minimum
* De 4 Go de RAM minimum

### <a name="permissions-required-toocreate-automation-account"></a>Autorisations toocreate requis compte Automation
toocreate ou mise à jour un compte Automation, vous devez avoir hello suivant des privilèges spécifiques et des autorisations requises toocomplete de cette rubrique.   
 
* Dans l’ordre toocreate un compte Automation, votre compte d’utilisateur Active Directory doit être toobe tooa ajouté rôle rôle de propriétaire de toohello équivalent d’autorisations pour les ressources Microsoft.Automation comme indiqué dans l’article [contrôle d’accès basé sur un rôle dans Azure Automation ](automation-role-based-access-control.md).  
* Si les inscriptions d’application hello paramètre est défini trop**Oui**, les utilisateurs non administrateurs dans votre locataire Azure AD peuvent [inscrire des applications AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Si les inscriptions d’application hello paramètre est défini trop**non**, utilisateur hello effectuer cette action doit être un administrateur global dans Azure AD. 

Si vous n’êtes pas un membre d’instance d’Active Directory de l’abonnement hello avant que vous êtes ajouté toohello global administrateur ou le co-administrateur rôle d’abonnement de hello, vous êtes ajouté tooActive active en tant qu’invité. Dans ce cas, vous recevez un « vous n’avez pas toocreate autorisations... » avertissement sur hello **ajouter un compte Automation** panneau. Les utilisateurs qui ont été ajoutées toohello global administrateur ou le co-administrateur rôle tout d’abord peut être supprimé de l’instance d’Active Directory de l’abonnement hello et rajouté toomake les un utilisateur complète dans Active Directory. tooverify cette situation, hello **Azure Active Directory** volet Bonjour portail Azure, sélectionnez **utilisateurs et groupes**, sélectionnez **tous les utilisateurs** et, après avoir sélectionné hello utilisateur spécifique, sélectionnez **profil**. Hello valeur Hello **type utilisateur** attribut sous le profil de l’utilisateur hello doit être **invité**.

## <a name="authentication-planning"></a>Planification de l’authentification
Azure Automation vous permet de tâches tooautomate par rapport aux ressources dans Azure, sur site et avec d’autres fournisseurs cloud.  Dans l’ordre pour un tooperform runbook ses actions requises, il ressources doit être autorisations toosecurely accès hello doté d’autorisations minimales de hello nécessaires au sein de l’abonnement de hello.  

### <a name="what-is-an-automation-account"></a>Qu’est-ce qu’un compte Automation ? 
Toutes les tâches d’automatisation hello que vous effectuez par rapport à des ressources à l’aide des applets de commande Azure de hello dans Azure Automation s’authentifier à l’aide de l’authentification Azure Active Directory d’organisation identité basée sur les informations d’identification de tooAzure.  Un compte Automation est séparé hello compte vous utilisez toosign dans tooconfigure de portail toohello et ressources Azure.  Ressources d’automatisation inclus avec un compte sont les suivants de hello :

* **Certificats** : contient un certificat utilisé pour l’authentification à partir d’un runbook ou d’une configuration DSC ou permet d’en ajouter.
* **Connexions** -contient l’authentification et la configuration informations requises tooconnect tooan externe service ou une application à partir d’un runbook ou la configuration DSC.
* **Informations d’identification** -est un objet PSCredential qui contient les informations d’identification de sécurité comme un nom d’utilisateur et un mot de passe requis tooauthenticate à partir d’un runbook ou la configuration DSC.
* **Modules d’intégration** -sont des modules PowerShell inclus avec Azure Automation compte toomake d’utiliser les applets de commande dans les runbooks et les configurations DSC.
* **Planifications** : contient des planifications qui démarrent ou arrêtent un runbook à une heure spécifiée, y compris des fréquences récurrentes.
* **Variables** : contient les valeurs qui sont disponibles à partir d’un runbook ou d’une configuration DSC.
* **Les Configurations DSC** -sont des scripts PowerShell qui décrit comment tooconfigure une fonctionnalité du système d’exploitation ou la définition ou installer une application sur un ordinateur Windows ou Linux.  
* **Runbooks** : ensembles de tâches qui exécutent des processus automatisés dans Azure Automation sur la base de Windows PowerShell.    

ressources d’automatisation de Hello pour chaque compte Automation sont associées à une seule région Azure, mais les comptes Automation peuvent gérer toutes les ressources hello dans votre abonnement. Créer des comptes Automation dans des régions différentes si vous avez des stratégies qui requièrent des données et des ressources toobe tooa isolé une région spécifique.

> [!NOTE]
> Comptes Automation et les ressources de hello qu’ils contiennent qui sont créées dans hello portail Azure, ne sont pas accessibles dans hello portail Azure classic. Si vous souhaitez toomanage ces comptes ou leurs ressources avec Windows PowerShell, vous devez utiliser des modules du Gestionnaire de ressources Azure hello.
> 

Lorsque vous créez un compte Automation Bonjour portail Azure, vous créez automatiquement deux entités de l’authentification :

* Compte d’identification Azure. Ce compte crée un principal de service dans Azure Active Directory (Azure AD) et un certificat. Il assigne également hello collaborateur basée sur le rôle de contrôle d’accès (RBAC), qui gère les ressources de gestionnaire de ressources à l’aide de procédures opérationnelles.
* Compte d’identification Classic. Ce compte télécharge un certificat de gestion, qui est utilisé toomanage les ressources classiques à l’aide de procédures opérationnelles.

Contrôle d’accès basé sur les rôles est disponible avec toogrant Azure Resource Manager autorisé le compte d’utilisateur Azure AD actions tooan et exécuter en tant que compte et authentifier ce principal de service.  Lecture [contrôle d’accès basé sur le rôle dans l’article d’Azure Automation](automation-role-based-access-control.md) pour plus d’informations toohelp développer votre modèle pour la gestion des autorisations d’Automation.  

#### <a name="authentication-methods"></a>Méthodes d’authentification
Hello tableau suivant récapitule hello différentes méthodes d’authentification pour chaque environnement pris en charge par Azure Automation.

| Méthode | Environnement 
| --- | --- | 
| Compte d’identification Azure et compte d’identification Classic |Déploiement Azure Resource Manager et déploiement Classic |  
| Compte d’utilisateur Azure AD |Déploiement Azure Resource Manager et déploiement Classic |  
| Authentification Windows |Centre de données local ou un autre fournisseur de cloud à l’aide de hello Runbook Worker hybride |  
| Informations d’identification AWS |Amazon Web Services |  

Sous hello **comment to\Authentication et sécurité** section, prenez en charge les articles indiquant les étapes de la vue d’ensemble et l’implémentation tooconfigure l’authentification pour ces environnements, soit avec un existant ou nouveau compte que vous avez Dédiez pour cet environnement.  Pour hello Azure exécuter en tant qu’et classique compte d’identification, hello rubrique [mise à jour Automation exécuter en tant que compte](automation-create-runas-account.md) décrit comment tooupdate votre compte Automation existant avec hello exécuter en tant que comptes de portail de hello ou à l’aide de PowerShell si elle n’était pas initialement configurée avec un compte d’identification ou classique exécuter en tant que. Si vous souhaitez toocreate une identification classique compte d’identification avec un certificat émis par votre autorité de certification d’entreprise (CA), passez en revue cette toolearn article comment toocreate hello comptes à l’aide cette configuration.     
 
## <a name="network-planning"></a>Planification réseau
Pourquoi inscrire de tooand tooconnect Runbook Worker hybride avec Microsoft Operations Management Suite (OMS), il doit avoir le numéro de port toohello accès et hello URL décrites ci-dessous.  Il s’agit en outre toohello [ports et les URL nécessaires pour hello Microsoft Monitoring Agent](../log-analytics/log-analytics-windows-agents.md#network) tooconnect tooOMS. Si vous utilisez un serveur proxy pour la communication entre l’agent de hello et le service OMS de hello, vous devez tooensure que hello les ressources appropriées sont accessibles. Si vous utilisez un toohello d’accès toorestrict pare-feu Internet, vous devez avoir tooconfigure votre pare-feu toopermit accès.

informations de Hello ci-dessous port hello de liste et les URL qui sont requis pour toocommunicate de Runbook Worker hybride hello avec l’Automation.

* Port : seul TCP 443 est nécessaire pour l’accès Internet sortant
* URL globale : *.azure-automation.net

Si vous avez un compte Automation défini pour une région spécifique et que vous souhaitez toorestrict la communication avec ce centre de données régional, hello tableau suivant fournit un enregistrement DNS hello pour chaque région.

| **Région** | **Enregistrement DNS** |
| --- | --- |
| Centre-Sud des États-Unis |scus-jobruntimedata-prod-su1.azure-automation.net |
| Est des États-Unis 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| Centre-Ouest des États-Unis | wcus-jobruntimedata-prod-su1.azure-automation.net |
| Europe de l'Ouest |we-jobruntimedata-prod-su1.azure-automation.net |
| Europe du Nord |ne-jobruntimedata-prod-su1.azure-automation.net |
| Centre du Canada |cc-jobruntimedata-prod-su1.azure-automation.net |
| Asie du Sud-Est |sea-jobruntimedata-prod-su1.azure-automation.net |
| Inde centrale |cid-jobruntimedata-prod-su1.azure-automation.net |
| Est du Japon |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Sud-Est de l’Australie |ase-jobruntimedata-prod-su1.azure-automation.net |
| Sud du Royaume-Uni | uks-jobruntimedata-prod-su1.azure-automation.net |
| Gouvernement américain - Virginie | usge-jobruntimedata-prod-su1.azure-automation.us |

Pour obtenir la liste d’adresses IP au lieu de noms, téléchargez et lisez les hello [adresse IP du centre de données Azure](https://www.microsoft.com/download/details.aspx?id=41653) fichier xml à partir de hello Microsoft Download Center. 

> [!NOTE]
> Ce fichier contient hello plages d’adresses IP (y compris les plages de calcul, SQL et de stockage) utilisées dans hello centres de données Microsoft Azure. Un fichier mis à jour est validé hebdomadaire qui reflète les plages hello actuellement déployé et les plages d’IP toohello modifications à venir. Nouvelles plages figurant dans le fichier de hello pas servira dans les centres de données hello au moins une semaine. Veuillez télécharger hello nouveau code xml chaque semaine de fichiers et effectuer les modifications nécessaires hello sur votre site toocorrectly identifier les services qui s’exécutent dans Azure. Routage des utilisateurs Express peuvent Notez que ce fichier utilisé tooupdate hello annonce BGP d’espace Azure Bonjour première semaine de chaque mois. 
> 

## <a name="creating-an-automation-account"></a>Création d’un compte Automation

Il existe différentes façons de que créer un compte Automation Bonjour portail Azure.  Hello tableau suivant présente chaque type d’expérience de déploiement et les différences entre eux.  

|Méthode | Description |
|-------|-------------|
| Sélectionner un contrôle à partir de hello Marketplace & Automation | Une offre, qui crée un compte Automation et l’espace de travail OMS lié tooone dans hello même groupe de ressources et de région.  Intégration avec OMS également inclut des avantages hello d’Analytique de journal toomonitor et analyser les flux d’état et le travail de la tâche du runbook au fil du temps et utilisent des fonctionnalités avancées tooescalate ou étudier les problèmes. Hello offre également déploie des solutions hello de suivi des modifications et de gestion de la mise à jour, qui sont activées par défaut. |
| Sélectionnez l’Automation à partir de hello Marketplace | Crée un compte Automation dans un groupe de ressources nouvelles ou existantes qui n’est pas lié tooan espace de travail OMS et n’inclut pas toutes les solutions disponibles à partir de l’offre d’Automation & contrôle hello. Cela est une configuration de base qui vous présente tooAutomation et peut vous aider à apprendre comment toowrite runbooks, les configurations DSC et utilisez hello des fonctionnalités de service de hello. |
| Solutions de gestion sélectionnées | Si vous sélectionnez une solution –  **[gestion de la mise à jour](../operations-management-suite/oms-solution-update-management.md)**,  **[machines virtuelles de démarrage/arrêt pendant heures creuses](automation-solution-vm-management.md)**, ou  **[ Le suivi des modifications](../log-analytics/log-analytics-change-tracking.md)**  ils vous invite à tooselect une automatisation existante et l’espace de travail OMS ou offre vous hello toocreate option à la fois comme requis pour hello solution toobe est déployé dans votre abonnement. |

Cette rubrique vous guide lors de la création d’un espace de travail OMS et un compte Automation à l’offre d’intégration hello Automation & contrôle.  toocreate un compte Automation pour tester ou toopreview service hello, hello consultez l’article suivant autonome [créer le compte d’automatisation autonome](automation-create-standalone-account.md).  

### <a name="create-automation-account-integrated-with-oms"></a>Créer un compte Automation intégré à OMS
Hello recommandé tooonboard méthode Qu'automation est en sélectionnant l’offre d’Automation & contrôle hello de hello Marketplace.  Cela crée un compte d’automatisation et établit l’intégration avec un espace de travail OMS, y compris hello option tooinstall hello solutions de gestion qui sont disponibles avec l’offre de hello hello.  

1. Se connecter toohello portail Azure avec un compte qui est membre du rôle des administrateurs d’abonnements hello et coadministrateur de l’abonnement de hello.

2. Cliquez sur **Nouveau**.<br><br> ![Sélection de l’option Nouveau dans le portail Azure](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  

3. Recherchez **Automation** et puis Bonjour résultats de recherche sélectionnez **Automation & contrôle***.<br><br> ![Recherche et sélection d’Automation &amp; Control dans la Place de marché](media/automation-offering-get-started/automation-portal-martketplace-select-automationandcontrol.png).<br>   

4. Après avoir lu la description hello pour l’offre de hello, cliquez sur **créer**.  

5. Sur hello **Automation & contrôle** Panneau de paramètres, sélectionnez **espace de travail OMS**.  Sur hello **espaces de travail OMS** panneau, sélectionnez un toohello d’espace de travail lié OMS même abonnement Azure hello compte Automation est dans ou créer un espace de travail OMS.  Si vous n’avez pas un espace de travail OMS, sélectionnez **créer un nouvel espace de travail** et hello **espace de travail OMS** panneau, exécutez les opérations hello : 
   - Spécifiez un nom pour hello nouvelle **espace de travail OMS**.
   - Sélectionnez un **abonnement** toolink tooby en sélectionnant à partir de la liste déroulante de hello si la valeur par défaut hello sélectionnée n’est pas appropriée.
   - Pour **Groupe de ressources**, vous pouvez créer un groupe de ressources ou sélectionner un groupe de ressources existant.  
   - Sélectionnez un **emplacement**.  Actuellement les seuls emplacements hello disponibles sont **sud-est de l’Australie**, **États-Unis**, **Asie du Sud-est**, **ouest des États-Unis**et  **Europe de l’ouest**.
   - Sélectionner un **niveau de tarification**.  Hello est disponible dans deux niveaux : libre et de niveau par nœud (OMS).  niveau gratuit de Hello a une limite de quantité hello de données collectées quotidiennement, période de rétention et minutes de runtime de travail de runbook.  Hello par nœud (OMS) niveau n’a pas une limite de quantité hello de données collectées quotidiennement.  
   - Sélectionnez **Compte Automation**.  Si vous créez un nouvel espace de travail OMS, vous êtes invité tooalso créer un compte Automation est associé à hello nouvel espace de travail OMS spécifié précédemment, y compris votre abonnement Azure, le groupe de ressources et la région.  Vous pouvez sélectionner **créer un compte Automation** et hello **compte Automation** panneau, fournir hello suivantes : 
  - Bonjour **nom** , entrez le nom hello Hello compte Automation.

    Toutes les autres options sont automatiquement remplies en fonction de l’espace de travail OMS hello sélectionné et ces options ne peut pas être modifiées.  Un compte d’identification Azure est la méthode d’authentification par défaut hello pour offre de hello.  Une fois que vous cliquez sur **OK**, options de configuration hello sont validées et hello compte Automation est créé.  Vous pouvez suivre sa progression sous **Notifications** à partir du menu de hello. 

    Sinon, sélectionnez un compte d’identification Automation existant.  compte Hello sélectionné ne peut pas être déjà lié tooanother espace de travail OMS, dans le cas contraire, un message de notification est présenté dans le panneau de hello.  S’il est déjà lié, vous devez tooselect différents Automation compte d’identification ou créez un.

    Après avoir effectué les informations hello requises, cliquez sur **créer**.  informations de Hello sont vérifiées et hello compte Automation et exécuter en tant que les comptes sont créés.  Vous revenez toohello **espace de travail OMS** panneau automatiquement.  

6. Après avoir entré des informations de hello requis sur hello **espace de travail OMS** panneau, cliquez sur **créer**.  Alors que les informations de hello sont vérifiées et espace de travail hello est créé, vous pouvez suivre sa progression sous **Notifications** à partir du menu de hello.  Vous revenez toohello **ajouter la Solution** panneau.  

7. Sur hello **Automation & contrôle** Panneau de paramètres, confirmer la tooinstall hello recommandations présélectionnée. Si vous les désélectionnez, vous pourrez les installer séparément plus tard.  

8. Cliquez sur **créer** tooproceed avec d’intégration Automation et un espace de travail OMS. Tous les paramètres sont validés et il tente alors de hello toodeploy offre dans votre abonnement.  Ce processus peut prendre plusieurs secondes toocomplete et que vous pouvez suivre sa progression sous **Notifications** à partir du menu de hello. 

Une fois l’offre de hello intégrées, vous pouvez commencer à créer des solutions de gestion que vous avez activé procédures opérationnelles, le travail avec hello, déployez un [Runbook worker hybride](automation-hybrid-runbook-worker.md) rôle, ou commencer à travailler avec [Analytique de journal](https://docs.microsoft.com/azure/log-analytics) données toocollect générées par les ressources dans votre environnement cloud ou localement.   

## <a name="next-steps"></a>Étapes suivantes
* Vous pouvez confirmer que votre nouveau compte Automation s’authentifie auprès de ressources Azure en consultant [Test Azure Automation Run As account authentication](automation-verify-runas-authentication.md) (Test d’authentification du compte d’identification Azure Automation).
* tooget main de la création de runbooks, tout d’abord examiner hello [types de runbook Automation](automation-runbook-types.md) pris en charge et les considérations avant de commencer la création.


