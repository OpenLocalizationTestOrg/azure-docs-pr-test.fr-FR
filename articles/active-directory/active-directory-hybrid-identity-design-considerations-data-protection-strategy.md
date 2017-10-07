---
title: "Considérations de conception pour les identités hybrides aaaAzure Active Directory - définir la stratégie de protection des données | Documents Microsoft"
description: "Vous allez définir la stratégie de protection des données hello pour hybride identité solution toomeet hello besoins de votre entreprise que vous avez définie."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e76fd1f4-340a-492a-84d9-e05f3b7cc396
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 8fd7ab364a09de3b60293a4a1cbb6e0fa4a3295d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="define-data-protection-strategy-for-your-hybrid-identity-solution"></a>Définir la stratégie de protection des données pour votre solution d’identités hybrides
Dans cette tâche, vous allez définir la stratégie de protection des données hello pour hybride identité solution toomeet hello besoins de votre entreprise que vous avez définie dans :

* [Déterminer les exigences de protection des données](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)
* [Déterminer les exigences de gestion de contenu](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)
* [Déterminer les exigences de contrôle d’accès](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)
* [Déterminer les exigences de réponse aux incidents](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="define-data-protection-options"></a>Définir les options de protection des données
Comme expliqué dans la section [Déterminer les exigences de synchronisation de répertoire](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md), Microsoft Azure AD peut se synchroniser avec vos services de domaine Active Directory (AD DS) situés en local. Cette intégration permet aux organisations tooleverage Azure AD tooverify de l’utilisateur quand ils essaient tooaccess des ressources d’entreprise. Cela est possible pour les deux scénarios : données rest localement et dans le cloud de hello.  Toodata d’accès dans Azure AD nécessite l’authentification des utilisateurs via un service de jeton de sécurité (STS).

Une fois authentifié, hello utilisateur principaux (UPN) est en lecture à partir du jeton d’authentification hello et hello répliquées des partitions et conteneur correspondant toohello domaine de l’utilisateur est déterminée. Pour plus d’informations sur l’existence de l’utilisateur hello, état activé et rôle sont utilisés par toodetermine de système d’autorisation hello si hello accès demandé toohello cible client n’est autorisé pour cet utilisateur dans cette session. Certaines actions autorisées (en particulier, créer utilisateur, réinitialisation de mot de passe) créer une piste d’audit qui peut être utilisée par un client efforts de conformité toomanage administrateur ou d’enquêtes.

Déplacement des données à partir de votre centre de données local dans le stockage Azure via une connexion Internet ne peuvent pas toujours être possibles en raison de toodata volume, la disponibilité de la bande passante ou autres considérations. Hello [Service d’importation/exportation Azure Storage](../storage/common/storage-import-export-service.md) constitue une option basée sur le matériel pour placer/la récupération des volumes importants de données dans le stockage blob. Il vous permet de toosend [chiffré par BitLocker](https://technet.microsoft.com/library/dn306081#BKMK_BL2012R2) directement tooan centre de données Azure où les opérateurs cloud téléchargera le compte de stockage tooyour hello contenu, ou ils peuvent télécharger votre tooyour de données Azure lecteurs tooreturn des lecteurs de disque dur tooyou. Seuls les disques chiffrées sont acceptées pour ce processus (à l’aide d’une clé BitLocker générée par hello service pendant l’installation de tâche hello). clé de BitLocker Hello est fournie tooAzure séparément, et offrir ainsi hors bande partage de clé.

Étant donné que les données en transit peuvent avoir lieu dans différents scénarios, est également tooknow pertinentes que Microsoft Azure utilise [mise en réseau virtuelle](https://azure.microsoft.com/documentation/services/virtual-network/) trafic tooisolate clients à partir d’une autre, utilisant des mesures comme niveau hôte et invité les pare-feu, le filtrage des paquets IP, le blocage des ports et les points de terminaison HTTPS. Toutefois, la plupart des communications internes d’Azure, y compris d’infrastructure à infrastructure et d’infrastructure à client (en local), sont également chiffrées. Un autre scénario important est communications hello dans les centres de données Azure ; Microsoft gère tooassure réseaux aucune machine virtuelle peut emprunter l’identité ou espionner sur l’adresse IP de hello d’un autre. Le protocole TLS/SSL est utilisé lors de l’accès de stockage Azure ou les bases de données SQL, ou lors de la connexion des Services de tooCloud. Dans ce cas, administrateur de client hello est responsable de l’obtention d’un certificat TLS/SSL et de les déployer une infrastructure cliente tootheir. Le trafic de données le déplacement de Machines virtuelles dans hello même déploiement ou entre les clients dans un déploiement unique via le réseau virtuel Microsoft Azure peut être protégé via des protocoles de communication chiffrée tels que HTTPS, SSL/TLS ou d’autres utilisateurs.

Selon la façon dont vous avez répondu aux questions hello dans [déterminer les exigences de protection des données](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md), vous devez être en mesure de toodetermine comment vous souhaitez que tooprotect vos données et solution d’identité hybride hello vous aidera à qui. tableau de Hello présente des options hello pris en charge par Azure qui sont disponibles pour chaque scénario de protection des données.

| Option de protection des données | Au repos dans le cloud de hello | Au repos en local | En transit |
| --- | --- | --- | --- |
| Chiffrement de lecteur BitLocker |X |X | |
| Bases de données SQL Server tooencrypt |X |X | |
| Chiffrement de machine virtuelle à machine virtuelle | | |X |
| SSL/TLS | | |X |
| VPN | | |X |

> [!NOTE]
> Lecture [conformité par fonctionnalité](https://azure.microsoft.com/support/trust-center/services/) à [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) tooknow plus d’informations sur les certifications de hello chaque service Azure est conforme.
> Étant donné que les options de hello pour la protection de données utilisent une approche multicouche, comparaison entre ces options ne sont pas applicables pour cette tâche. Assurez-vous que tirant parti de toutes les options disponibles pour chaque état des données hello.
>
>

## <a name="define-content-management-options"></a>Définir les options de gestion de contenu
L’un des avantages de l’utilisation d’Azure AD toomanage une infrastructure d’identité hybride sont que les processus hello sont complètement transparente du point de vue de l’utilisateur final de hello. utilisateur de Hello va tenter de tooaccess une ressource partagée, hello ressource requiert une authentification, hello disposera toosend un tooAzure de demande d’authentification AD dans l’ordre tooobtain hello jeton et accéder aux ressources de hello. Ce processus se déroule intégralement en arrière-plan, sans intervention de l’utilisateur. Il est également possible de toogrant autorisation tooa [groupe](active-directory-manage-groups.md#getting-started-with-access-management) d’utilisateurs dans l’ordre tooallow les tooperform certaines des actions courantes.

Les organisations préoccupées par la confidentialité des données requièrent généralement la classification des données pour leur solution. Si leur infrastructure locale actuelle est déjà utilisé par la classification des données, il est possible tooleverage Azure AD en tant que référentiel principal de hello pour l’identité de l’utilisateur. Le [kit de classification des données](https://msdn.microsoft.com/library/Hh204743.aspx) pour Windows Server 2012 R2 est un outil commun utilisé en local pour la classification des données. Cet outil peut aider à tooidentify, classifier et protéger les données sur les serveurs de fichiers dans votre cloud privé. Il est également possible de tooleverage hello [Classification automatique des fichiers](https://technet.microsoft.com/library/hh831672.aspx) dans Windows Server 2012 tooaccomplish cela.

Si votre organisation n’est pas la classification des données en place, mais a besoin des fichiers sensibles tooprotect sans ajouter de nouveaux serveurs locaux, ils peuvent utiliser Microsoft [Service Azure Rights Management](https://technet.microsoft.com/library/JJ585026.aspx).  Azure RMS utilise le chiffrement, d’identité et d’autorisation toohelp stratégies sécurisée vos fichiers et les messages électroniques, et il fonctionne sur plusieurs appareils, les téléphones, tablettes et PC. Étant donné que Azure RMS est un service cloud, il est inutile tooexplicitly configurer des approbations avec d’autres organisations pouvoir partager du contenu protégé avec eux. Si les organisations disposent déjà d’Office 365 ou d’un répertoire Azure AD, la collaboration entre les organisations est automatiquement prise en charge. Vous pouvez également synchroniser uniquement les attributs de répertoire hello qu’Azure RMS doit toosupport une identité commune pour vos comptes Active Directory local, à l’aide d’Azure Active Directory Synchronization Services (AAD Sync) ou Azure AD Connect.

Une partie essentielle de la gestion de contenu est toounderstand qui accède à la ressource, par conséquent, une fonctionnalité de journalisation enrichies est importante pour la solution de gestion des identités hello. Azure AD fournit des journaux sur plus de 30 jours, incluant les fonctionnalités suivantes :

* Modifications apportées à l’appartenance au rôle (ex : utilisateur ajouté le rôle d’administrateur tooGlobal)
* Mises à jour des informations d’identification (p. ex., modifications de mot de passe)
* Gestion de domaine (p. ex., vérification d’un domaine personnalisé, suppression d’un domaine)
* Ajout ou suppression d’applications
* Gestion des utilisateurs (p. ex., ajout, suppression, mise à jour d’un utilisateur)
* Ajout ou suppression de licences

> [!NOTE]
> Lecture [de sécurité de Microsoft Azure et de gestion du journal d’Audit](http://download.microsoft.com/download/B/6/C/B6C0A98B-D34A-417C-826E-3EA28CDFC9DD/AzureSecurityandAuditLogManagement_11132014.pdf) tooknow plus d’informations sur les fonctionnalités de journalisation dans Azure.
> Selon la façon dont vous avez répondu aux questions hello dans [déterminer les besoins de gestion de contenu](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md), vous devez être en mesure de toodetermine comment vous souhaitez que hello toobe contenu géré dans votre solution d’identité hybride. Alors que toutes les options sont exposées dans le tableau 6 sont compatibles avec d’intégration à Azure AD, il est important toodefine qui convient le mieux à vos besoins.
>
>

| Options de gestion de contenu | Avantages | Inconvénients |
| --- | --- | --- |
| Centralisation en local (Active Directory Rights Management Server) |Contrôle total sur l’infrastructure de serveur hello responsable de la classification des données de salutation <br> Fonction intégrée dans Windows Server, sans licence ou abonnement supplémentaire <br> Peut être intégré à Active AD dans un scénario hybride <br> Prise en charge des fonctionnalités de gestion des droits relatifs à l’information (IRM) dans Microsoft Online Services par exemple Exchange Online, SharePoint Online et Office 365 <br> Prise en charge des produits serveur Microsoft locaux, par exemple Exchange Server, SharePoint Server et des serveurs de fichiers exécutant Windows Server et l’infrastructure de classification des fichiers (ICF) |Une version ultérieure, maintenance (conserver les mises à jour, configuration et mises à niveau potentielles), depuis informatique possède hello serveur <br> Requiert une infrastructure de serveurs locale<br> N’exploite pas les fonctionnalités Azure en mode natif |
| Centralisé dans hello cloud (Azure RMS) |Plus facile toomanage comparée toohello solution locale <br> Peut être intégré à Active DS dans un scénario hybride <br>  Entièrement intégré dans Azure AD <br> Ne nécessite pas un serveur local dans le service de commande toodeploy hello <br> Prise en charge des produits serveur Microsoft locaux, par exemple Exchange Server, SharePoint Server et des serveurs de fichiers exécutant Windows Server et l’infrastructure de classification des fichiers (ICF) <br> Le service informatique peut contrôler complètement les clés de ses clients grâce à la fonctionnalité BYOK |Votre organisation doit posséder un abonnement au cloud prenant en charge RMS  <br> Votre organisation doit disposer d’une authentification d’utilisateur Azure AD directory toosupport pour RMS |
| Hybride (Azure RMS intégré à Active Directory Rights Management Server en local) |Ce scénario s’accumule avantages hello de, centralisée localement et dans le cloud de hello. |Votre organisation doit posséder un abonnement au cloud prenant en charge RMS  <br> Votre organisation doit disposer d’une authentification d’utilisateur Azure AD directory toosupport pour RMS, <br> Requiert une connexion entre le service cloud Azure et l’infrastructure locale |

## <a name="define-access-control-options"></a>Définir les options de contrôle d’accès
En tirant parti de l’authentification de hello, autorisation et contrôle d’accès fonctionnalités disponibles dans Azure AD, vous serez en mesure de tooenable votre toouse entreprise un référentiel central identité tout en autorisant les utilisateurs et les partenaires toouse-session unique (SSO) comme indiqué dans hello figure ci-dessous :

![](./media/hybrid-id-design-considerations/centralized-management.png)

Gestion centralisée et intégration complète avec d’autres répertoires

Azure Active Directory offre des toothousands l’authentification uniques d’applications SaaS et localement les applications web. Veuillez lire hello [liste de compatibilité de fédération Azure Active Directory : fournisseurs d’identité tiers qui peuvent être utilisé tooimplement l’authentification unique](https://msdn.microsoft.com/library/azure/jj679342.aspx) article pour plus d’informations sur hello tiers SSO qui ont été testés par Microsoft. Cette fonctionnalité permet l’organisation tooimplement un éventail de scénarios de B2B tout en conservant le contrôle de gestion des identités et des accès hello. Toutefois, au cours de hello B2B, processus de conception est méthode d’authentification hello toounderstand important qui sera utilisé par les partenaires hello et valide si cette méthode est prise en charge par Azure. Voici les méthodes actuellement prises en charge par Azure AD :

* SAML (Security Assertion Markup Language)
* OAuth
* Kerberos
* Jetons
* Certificats

> [!NOTE]
> lire [protocoles d’authentification Azure Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx) tooknow plus d’informations sur chaque protocole et de ses fonctionnalités dans Azure.
>
>

À l’aide de prise en charge hello Azure AD, permet aux applications commerciale hello même facile Mobile Services d’authentification expérience tooallow employés toosign dans leurs applications mobiles avec leurs informations d’identification Active Directory d’entreprise. Avec cette fonctionnalité, Azure AD est pris en charge comme fournisseur d’identité dans les Services mobiles en même temps que par hello autres fournisseurs d’identité déjà prennent en charge (qui incluent Accounts Microsoft, Facebook ID, ID de Google et Twitter des ID). Si hello local utilise hello des informations d’identification de l’utilisateur située dans les services AD DS hello entreprise des applications, l’accès de hello de partenaires et les utilisateurs provenant hello cloud doit être transparent. Vous pouvez gérer l’utilisateur l’accès conditionnel contrôle too(cloud-based) applications web, API web, Microsoft cloud services, les applications SaaS 3e partie et les applications clientes (mobile) native et présentent les avantages de hello de sécurité, l’audit, de rapports tout en un sur place. Toutefois, il est recommandé toovalidate cela dans un environnement hors production ou avec une quantité limitée d’utilisateurs.

> [!TIP]
> Il est importante toomention que Azure AD n’a pas de stratégie de groupe que les services AD DS a. Dans stratégie tooenforce des commandes pour les appareils, vous devez une solution de gestion des appareils mobiles tels que [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx).
>
>

Une fois que l’utilisateur de hello est authentifié à l’aide d’Azure AD, il est important de niveau de hello tooevaluate d’accès hello utilisateur il aura. Hello niveau d’accès hello utilisateur aura sur une ressource peuvent varier, Azure AD peut ajouter une couche de sécurité supplémentaire par contrôle toosome d’accéder aux ressources, vous devez également garder à l’esprit que les ressources hello lui-même peuvent avoir également sa propre liste de contrôle d’accès séparément, telles que le contrôle d’accès hello pour les fichiers situés dans un serveur de fichiers. figure Hello ci-dessous résume les niveaux hello du contrôle d’accès que vous pouvez avoir dans un scénario hybride :

![](./media/hybrid-id-design-considerations/accesscontrol.png)

Chaque interaction dans le diagramme hello a montré dans la Figure X représente un scénario de contrôle d’accès qui peut être couverts par Azure AD. Une description de chaque scénario est disponible ci-dessous :

1. Tooapplications accès conditionnelles qui sont hébergées en local : vous pouvez utiliser les appareils inscrits avec des stratégies d’accès pour les applications qui sont configurées toouse AD FS avec Windows Server 2012 R2. Pour plus d’informations sur la configuration d’un accès conditionnel en local, consultez la rubrique [Configuration d'un accès conditionnel en local à l'aide du service d'inscription d'appareils Azure Active Directory](active-directory-conditional-access.md).

2. Toohello de contrôle d’accès au portail Azure : Azure vous permet également de portail de toohello contrôle l’accès à l’aide du contrôle d’accès basé sur un rôle (RBAC)). Cette méthode permet de hello entreprise toorestrict hello quantité opérations procéder à un individu Bonjour portail Azure. En utilisant le portail de toohello d’accès RBAC toocontrol, les administrateurs informatiques peuvent déléguer l’accès à l’aide de hello suivant des approches de gestion des accès :

* Attribution de rôle de groupe : vous pouvez affecter l’accès à des groupes de tooAzure AD qui peuvent être synchronisés à partir de votre Active Directory local. Cela vous permet de tooleverage hello investissements de votre organisation dans les outils et processus de gestion des groupes. Vous pouvez également utiliser la fonctionnalité de gestion déléguée des groupes hello d’Azure AD Premium.
* Exploitez générée dans les rôles dans Azure : vous pouvez utiliser trois rôles : tooensure propriétaire, collaborateur et lecteur, que les utilisateurs et groupes ont des autorisations toodo uniquement hello les tâches dont ils ont besoin toodo leurs travaux.
* Un accès granulaire tooresources : vous pouvez affecter des rôles toousers et des groupes pour un abonnement spécifique, groupe de ressources ou une ressource individuelle Azure tel qu’un site Web ou d’une base de données. De cette façon, vous pouvez garantir que les utilisateurs ont accéder aux ressources de hello tooall que dont ils ont besoin et aucun tooresources accès qu’ils toomanage n’avez pas besoin.

> [!NOTE]
> Si vous créez des applications et que vous souhaitez le contrôle d’accès toocustomize hello pour eux, il est également possible toouse les rôles d’Application Azure AD pour l’autorisation. Passez en revue cette [WebApp-RoleClaims-DotNet exemple](https://github.com/AzureADSamples/WebApp-RoleClaims-DotNet) sur la façon de toobuild toouse de votre application cette fonctionnalité.
>
>

3. Accès conditionnel pour les applications Office 365 avec Microsoft Intune : administrateurs informatiques peuvent configurer l’accès conditionnel appareil stratégies toosecure ressources d’entreprise, tandis qu’à hello même moment, ce qui permet de travailleurs sur hello tooaccess de périphériques compatibles Services. Pour plus d’informations, consultez la rubrique [Stratégies d’accès conditionnel basées sur les appareils pour les services Office 365](active-directory-conditional-access-device-policies.md).

4. Accès conditionnel pour les applications Saas : [cette fonctionnalité](http://blogs.technet.com/b/ad/archive/2015/06/25/azure-ad-conditional-access-preview-update-more-apps-and-blocking-access-for-users-not-at-work.aspx) vous permet d’accéder de tooblock de capacité de hello pour les utilisateurs et de règles d’accès de l’authentification multifacteur par application de tooconfigure pas sur un réseau approuvé. Vous pouvez appliquer hello l’authentification multifacteur règles tooall les utilisateurs qui sont assignés toohello application, ou uniquement pour les utilisateurs au sein de spécifié les groupes de sécurité. Les utilisateurs peuvent être exclus de spécification de l’authentification multifacteur hello si elles accèdent à hello application à partir d’une adresse IP qu’à l’intérieur de hello réseau de l’organisation.

Étant donné que les options de hello pour le contrôle d’accès utilisent une approche multicouche, comparaison entre ces options ne sont pas applicables pour cette tâche. Assurez-vous que tirant parti de toutes les options disponibles pour chaque scénario nécessitant le tooyour toocontrol accéder aux ressources.

## <a name="define-incident-response-options"></a>Définir les options de réponse aux incidents
Azure AD peut aider tooidentity informatique potentielle des risques de sécurité d’environnement hello de surveillance de l’activité de l’utilisateur, service informatique peut tirer parti d’Azure AD Access et les rapports d’utilisation capacité toogain consulter hello intégrité et la sécurité de répertoire de votre organisation. Avec cette information, un administrateur informatique peut déterminer plus précisément où peut se trouver des risques de sécurité afin qu’ils peuvent planifier en conséquence toomitigate ces risques.  [Abonnement Azure AD Premium](active-directory-get-started-premium.md) possède un ensemble de rapports de sécurité qui peut activer informatique tooobtain ces informations. Les [rapports Azure AD](active-directory-view-access-usage-reports.md) sont classés comme indiqué ci-dessous :

* **Rapports d’anomalies**: contiennent des événements que nous avons trouvé toobe anormale de connexion. Notre objectif est toomake vous prenant en charge de cette activité et vous toobe toomake en mesure de déterminer si un événement est suspect.
* **Rapports d’application intégrée**: fournissent des indications sur l’utilisation des applications du cloud au sein de votre société. Azure Active Directory permet d’intégrer des milliers d'applications du cloud.
* **Rapports d’erreurs**: indiquent des erreurs qui peuvent se produire lors de la configuration des applications tooexternal de comptes.
* **Rapports spécifiques à l’utilisateur**: affichent les données d’activité relatives aux appareils/connexions d’un utilisateur spécifique.
* **Journaux d’activité**: contiennent un enregistrement de tous les événements audités dans hello des dernières 24 heures, des 7 derniers jours ou 30 jours, ainsi que les modifications d’activité de groupe et activité d’inscription et de réinitialisation de mot de passe de la dernière.

> [!TIP]
> Un autre rapport qui peut également aider à hello équipe de réponse aux incidents sur un incident est hello [utilisateur avec les informations d’identification fuitées](http://blogs.technet.com/b/ad/archive/2015/06/15/azure-active-directory-premium-reporting-now-detects-leaked-credentials.aspx) rapport.  Ce rapport couvre toutes les correspondances entre cette liste d’informations d’identification volées et votre client.
>
>

Les autres rapports intégrés importants dans Azure AD qui peuvent être utilisés lors d’une investigation de réponse aux incidents sont les suivants :

* **Activité de réinitialisation de mot de passe**: fournir des indications sur la réinitialisation de mot de passe est la rapidité utilisée dans l’organisation de hello hello admin.
* **Activité d’enregistrement de réinitialisation de mot de passe**: fournit des indications sur les utilisateurs qui ont enregistré leurs méthodes pour la réinitialisation de mot de passe, et sur les méthodes qu’ils ont sélectionnées.
* **Activité de groupe**: fournit un historique de groupe de modifications toohello (ex : les utilisateurs ajoutés ou supprimés) qui ont été lancée dans le volet d’accès de hello.

En outre toohello core reporting fonctionnalité disponible dans Azure AD Premium qui peuvent être exploitées lors d’un processus d’examen de réponse aux incidents, service informatique peut également tirer parti des informations tooobtain de rapport d’Audit tel que :

* Modifications apportées à l’appartenance au rôle (ex : utilisateur ajouté le rôle d’administrateur tooGlobal)
* Mises à jour des informations d’identification (p. ex., modifications de mot de passe)
* Gestion de domaine (p. ex., vérification d’un domaine personnalisé, suppression d’un domaine)
* Ajout ou suppression d’applications
* Gestion des utilisateurs (p. ex., ajout, suppression, mise à jour d’un utilisateur)
* Ajout ou suppression de licences

Étant donné que les options de hello réponse aux incidents utilisent une approche multicouche, comparaison entre ces options ne sont pas applicables pour cette tâche. Assurez-vous que vous tire parti des toutes les options disponibles pour chaque scénario nécessitant la fonctionnalité de création de rapports Azure AD toouse dans le cadre du processus de réponse aux incidents de votre entreprise.

## <a name="next-steps"></a>Étapes suivantes
[Déterminer les tâches de gestion des identités hybrides](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)

## <a name="see-also"></a>Voir aussi
[Présentation des considérations relatives à la conception](active-directory-hybrid-identity-design-considerations-overview.md)
