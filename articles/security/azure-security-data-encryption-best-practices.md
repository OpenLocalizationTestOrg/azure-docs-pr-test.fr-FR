---
title: "aaaData sécurité et meilleures pratiques de chiffrement | Documents Microsoft"
description: "Cet article détaille les meilleures pratiques en matière de chiffrement et de sécurité des données, à l’aide de capacités Azure intégrées."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 17ba67ad-e5cd-4a8f-b435-5218df753ca4
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: 5057c85ed3107921462a40045e716675ea41e4bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-security-and-encryption-best-practices"></a>Meilleures pratiques en matière de chiffrement et de sécurité des données - Azure
Une option de protection de toodata hello clés dans le cloud de hello est la gestion des comptes pour les états possibles de hello dans vos données susceptibles de se produire, et les contrôles sont disponibles pour cet état. À des fins de hello de données Azure sécurité chiffrement meilleures pratiques et recommandations de hello sera autour hello suivant des États de données :

* Au repos : cela inclut tous les objets de stockage, conteneurs et types d’informations présents de manière statique sur un support physique, qu’il s’agisse d’un disque magnétique ou d’un disque optique.
* En Transit : Lorsque données sont transférées entre des composants, des emplacements ou des programmes, tels que sur le réseau de hello, à travers un bus de service (à partir de local toocloud et vice versa, y compris les connexions hybrides tels que ExpressRoute), ou au cours d’une entrée/sortie processus, il est considéré comme étant en mouvement.

Dans cet article, nous aborderons différentes meilleures pratiques d’Azure en matière de chiffrement et de sécurité des données. Ces meilleures pratiques sont dérivés de notre expérience avec la sécurité des données Azure et de chiffrement et hello les expériences des clients comme vous.

Pour chaque meilleure pratique, nous allons détailler les éléments suivants :

* Les meilleures pratiques de hello est
* Raison pour laquelle vous souhaitez tooenable que les meilleures pratiques
* Ce que peut être le résultat de hello si vous ne parvenez pas la meilleure pratique de tooenable hello
* Meilleure pratique de toohello alternatives possibles
* Comment vous pouvez apprendre tooenable hello il est recommandé

Cet article de la sécurité des données Azure et les meilleures pratiques de chiffrement est basé sur un avis consensus et les capacités de la plateforme Azure et les ensembles de fonctionnalités, tels qu’ils existent au moment de hello que cet article a été écrit. Avis et les technologies changent au fil du temps et de cet article sera mis à jour sur un tooreflect régulièrement ces modifications.

Les meilleures pratiques en matière de chiffrement et de sécurité des données Azure qui sont abordées dans le cadre de cet article sont les suivantes :

* Application de l’authentification multifacteur via Azure Multi-Factor Authentication
* Utilisation du contrôle d’accès en fonction du rôle (RBAC)
* Chiffrement des machines virtuelles Azure
* Utilisation de modèles de sécurité matériels
* Gestion de stations de travail sécurisées
* Activation du chiffrement de données SQL
* Protection des données en transit
* Application du chiffrement des données au niveau fichier

## <a name="enforce-multi-factor-authentication"></a>Application de l’authentification multifacteur via Azure Multi-Factor Authentication
Hello première étape de l’accès aux données et de contrôle dans Microsoft Azure sont tooauthenticate hello. [Azure Multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md) est une méthode permettant de vérifier l’identité de l’utilisateur grâce à d’autres moyens que les seuls nom d’utilisateur et mot de passe. Cette méthode d’authentification permet toodata d’accès de sauvegarde et d’applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple.

En activant l’authentification Multifacteur Azure pour vos utilisateurs, vous ajoutez une deuxième couche de sécurité toouser connexions et transactions. Dans ce cas, une transaction peut accéder à un document situé sur un serveur de fichiers ou sur votre site SharePoint Online. L’authentification Multifacteur Azure permet également la probabilité de hello tooreduce informatique que les informations d’identification compromises aura les données d’accès tooorganization.

Par exemple : Si vous mettre en œuvre l’authentification Multifacteur Azure pour vos utilisateurs et configurez toouse un appel téléphonique ou un message texte en tant que vérification, si les informations d’identification de l’utilisateur hello sont compromise, les intrus hello ne sera pas être en mesure de tooaccess n’importe quelle ressource, car il n’a pas de téléphone de d’accès toouser. Les organisations qui n’ajoutent pas de cette couche supplémentaire de protection de l’identité sont plus exposées pour une attaque par vol d’informations d’identification, ce qui peut entraîner des toodata compromis.

Une solution pour les organisations qui souhaitent utiliser le contrôle de l’authentification tookeep hello locale est toouse [serveur Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), également appelée authentification Multifacteur localement. À l’aide de cette méthode, vous serez toujours en mesure de tooenforce une authentification multifacteur, tout en conservant l’authentification Multifacteur hello/server sur site.

Pour plus d’informations sur l’authentification Multifacteur Azure, lisez l’article de hello [prise en main d’Azure multi-Factor Authentication dans le cloud de hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

## <a name="use-role-based-access-control-rbac"></a>Utilisation du contrôle d’accès en fonction du rôle (RBAC)
Restreindre l’accès en fonction de hello [devez tooknow](https://en.wikipedia.org/wiki/Need_to_know) et [moindre privilège](https://en.wikipedia.org/wiki/Principle_of_least_privilege) principes de sécurité. Il est impératif pour les organisations qui souhaitent utiliser les stratégies de sécurité tooenforce pour accéder aux données. Azure contrôle d’accès en fonction du rôle (RBAC) peut être utilisé tooassign autorisations toousers, des groupes et des applications au niveau d’une certaine étendue. Hello portée d’une attribution de rôle peut être un abonnement, un groupe de ressources ou une seule ressource.

Vous pouvez tirer parti de [rôles RBAC intégrés](../active-directory/role-based-access-built-in-roles.md) dans Azure tooassign privilèges toousers. Envisagez d’utiliser *collaborateur de compte de stockage* pour les opérateurs cloud que vous avez besoin de comptes de stockage toomanage et *collaborateur de compte de stockage classique* comptes de stockage classiques toomanage de rôle. Pour les opérateurs cloud nécessitant des machines virtuelles de toomanage et compte de stockage, envisagez de les ajouter trop*contributeur de l’ordinateur virtuel* rôle.

Les organisations qui n’appliquent aucun contrôle d’accès aux données via des fonctionnalités telles que RBAC risquent d’octroyer plus de privilèges que nécessaire à leurs utilisateurs. Cela peut entraîner des toodata compromis par certains utilisateurs ayant accès toodata qui ne doivent pas sont en premier lieu de hello.

Vous pouvez en savoir plus sur Azure RBAC en lisant l’article de hello [du contrôle d’accès](../active-directory/role-based-access-control-configure.md).

## <a name="encrypt-azure-virtual-machines"></a>Chiffrement des machines virtuelles Azure
Pour de nombreuses organisations, le [chiffrement des données au repos](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) est une étape obligatoire du processus de gestion de la confidentialité, de la conformité et de la souveraineté des données. Le chiffrement des disques Azure permet tooencrypt des administrateurs informatiques Windows et les disques de Linux IaaS Machine virtuelle (VM). Le chiffrement des disques Azure s’appuie sur la fonctionnalité standard BitLocker hello industrie de Windows et fonctionnalité d’exploration de données-Crypt hello du chiffrement de volume tooprovide Linux pour hello du système d’exploitation et des disques de données hello.

Vous pouvez tirer parti de chiffrement de disque Azure toohelp protéger et sauvegarder votre toomeet données exigences conformité et de sécurité de votre organisation. Les organisations doivent également envisager d’utiliser le chiffrement toohelp atténuer les risques liés à l’accès aux données toounauthorized connexes. Il est également recommandé de chiffrer les lecteurs toowriting préalable des données sensibles toothem.

Les volumes de données de votre machine virtuelle et le volume de démarrage, assurez-vous que tooencrypt données de commandes tooprotect au repos dans votre compte de stockage Azure. Protéger les clés de chiffrement hello et les secrets en tirant parti [Azure Key Vault](../key-vault/key-vault-whatis.md).

Pour vos serveurs Windows locaux, tenez compte des hello suivant les meilleures pratiques de chiffrement :

* Utilisez [BitLocker](https://technet.microsoft.com/library/dn306081.aspx) pour le chiffrement des données.
* Stockez les informations de récupération dans AD DS.
* S’il existe un problème que les clés BitLocker ont été compromises, nous vous recommandons de mettre en forme hello lecteur tooremove toutes les instances de métadonnées de BitLocker hello de lecteur de hello ou que vous avez déchiffrement et chiffrement le lecteur hello à nouveau.

Les organisations qui n’appliquent pas de chiffrement des données sont probablement toobe exposée toodata des problèmes d’intégrité, tels que des utilisateurs malveillants ou non fiables vol de données et compromis comptes obtenir toodata tout accès non autorisé dans un format clair. Outre ces risques, sociétés qui disposent de toocomply avec les réglementations du secteur, doivent prouver qu’ils sont preuve de diligence et sont à l’aide de contrôles sécurité correct hello tooenhance la sécurité des données.

Vous pouvez en savoir plus sur chiffrement de disque Azure en lisant l’article de hello [chiffrement de disque Azure pour Windows et les machines virtuelles IaaS Linux](azure-security-disk-encryption.md).

## <a name="use-hardware-security-modules"></a>Utilisation de modèles de sécurité matériels
Les solutions de chiffrement utilisent des données tooencrypt de clés secrètes. Pour cette raison, il est vital que ces clés soient stockées de manière appropriée. Gestion des clés devient partie intégrante de la protection des données, comme il s’agit des clés secrètes toostore optimisées qui sont des données de tooencrypt utilisé.

Chiffrement de disque Azure utilise [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) toohelp vous contrôler et gérer des clés de chiffrement de disque et des clés secrètes dans votre abonnement de coffre de clés, tout en garantissant que toutes les données de disques de machine virtuelle hello sont chiffrées au repos dans votre Azure stockage. Vous devez utiliser des clés de tooaudit de coffre de clés Azure et d’utilisation des stratégies.

Il existe de nombreuses toonot connexes des risques ayant des contrôles de sécurité appropriés dans place tooprotect hello clés secrètes qui ont été utilisé tooencrypt vos données. Si des personnes malveillantes ont accès les clés secrètes toohello, ils seront en mesure de toodecrypt les données de salutation et susceptibles d’avoir accès tooconfidential informations.

Vous pouvez en savoir plus sur les recommandations générales concernant la gestion des certificats dans Azure en lisant l’article de hello [gestion des certificats dans Azure : choses à faire et](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/).

Pour en savoir plus sur Azure Key Vault, consultez [Prise en main d’Azure Key Vault](../key-vault/key-vault-get-started.md).

## <a name="manage-with-secure-workstations"></a>Gestion de stations de travail sécurisées
Hello grande majorité des utilisateurs finaux de hello attaques cible hello, depuis le point de terminaison hello devient l’un des points principaux de hello d’attaque. Si un attaquant compromet un point de terminaison hello, il peut exploiter les données de tooorganization accès de l’utilisateur hello informations d’identification toogain. La plupart des attaques de point de terminaison sont parti tootake en mesure de faits hello que les utilisateurs finaux sont des administrateurs dans leurs stations de travail locales.

Vous pouvez réduire ces risques en utilisant une station de travail de gestion sécurisée. Nous vous recommandons d’utiliser un [stations de travail de l’accès privilégié (privilégiées)](https://technet.microsoft.com/library/mt634654.aspx) surface d’attaque tooreduce hello dans les stations de travail. Ces stations de travail de gestion sécurisées peuvent vous aider à limiter certaines attaques, afin d’optimiser la sécurité de vos données. Assurez-vous que toouse privilégiées tooharden et verrou vers le bas de votre station de travail. Il s’agit d’un garanties de haute sécurité tooprovide étape importante pour les comptes sensibles, tâches et la protection des données.

Absence de protection de point de terminaison peut risque de compromettre vos données, assurez-vous que tooenforce stratégies de sécurité sur tous les périphériques qui sont des données tooconsume utilisé, quel que soit l’emplacement des données hello (cloud ou local).

Vous pouvez en savoir plus sur les privilèges d’accès station de travail en lisant l’article de hello [sécurisation de l’accès privilégié](https://technet.microsoft.com/library/mt631194.aspx).

## <a name="enable-sql-data-encryption"></a>Activation du chiffrement de données SQL
[Le chiffrement transparent des données de la base de données SQL Azure](https://msdn.microsoft.com/library/dn948096.aspx) (TDE) protège contre les menaces hello d’activités malveillantes en effectuant le chiffrement en temps réel et déchiffrement de base de données hello, les sauvegardes associées, et les fichiers journaux des transactions au repos sans exiger des modifications toohello application.  Stockage hello d’une base de données entière est chiffré à l’aide d’une clé de chiffrement de base de données hello appelée de clé symétrique.

Même lorsque le stockage dans son intégralité hello est chiffré, il est très important tooalso chiffrer votre base de données. Il s’agit d’une implémentation de hello approche défense en profondeur pour la protection des données. Si vous utilisez [base de données SQL Azure](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx) et souhaitez tooprotect les données sensibles telles que la carte de crédit ou les numéros de sécurité sociale, vous pouvez chiffrer les bases de données à la norme FIPS 140-2 validé 256 bits le chiffrement AES qui répond aux exigences de hello de nombreuses normes (par exemple, HIPAA, PCI).

Il est important toounderstand que les fichiers liés trop[extension du pool de mémoires tampons](https://msdn.microsoft.com/library/dn133176.aspx) (BPE) ne sont pas chiffrés lorsqu’une base de données est chiffrée à l’aide du chiffrement transparent des données. Vous devez utiliser les outils de chiffrement au niveau du système de fichiers tels que BitLocker ou hello [système de fichiers EFS](https://technet.microsoft.com/library/cc700811.aspx) (Encrypting File System) pour BPE les fichiers associés.

Depuis un utilisateur autorisé comme un administrateur de sécurité ou un administrateur de base de données peut accéder aux données de hello même si la base de données hello est chiffré avec chiffrement transparent des données, vous devez également suivre les recommandations hello ci-dessous :

* Authentification SQL au niveau de base de données hello
* Authentification Azure AD à l’aide des rôles RBAC.
* Les applications et les utilisateurs doivent utiliser des tooauthenticate de comptes distincts. Cette façon, vous pouvez limiter les autorisations hello accordées toousers et des applications et réduire les risques de hello d’activités malveillantes
* Implémenter la sécurité au niveau de la base de données à l’aide des rôles de base de données fixe (par exemple, db_datareader ou db_datawriter), ou vous pouvez créer des rôles personnalisés pour votre application de toogrant objets de base de données tooselected autorisations explicites

Les organisations qui n’appliquent aucun chiffrement au niveau de la base de données peuvent être plus vulnérables aux attaques susceptibles de compromettre les données des bases de données SQL.

Vous pouvez en savoir plus sur le chiffrement TDE de SQL, lisez l’article de hello [chiffrement Transparent des données avec Azure SQL Database](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx).

## <a name="protect-data-in-transit"></a>Protection des données en transit
La protection des données en transit doit être un aspect essentiel de votre stratégie de protection des données. Étant donné que les données allez déplacer dans les deux sens à partir de nombreux emplacements, recommandation générale de hello est toujours utiliser des données de tooexchange protocoles SSL/TLS sur les différents sites. Dans certains cas, vous souhaiterez peut-être canal de communication entière tooisolate hello entre vos locaux et le cloud infrastructure à l’aide d’un réseau privé virtuel (VPN).

Pour les données qui transitent entre votre infrastructure locale et Azure, vous devez envisager le recours aux dispositifs de protection appropriés, comme HTTPS ou VPN.

Pour les organisations qui ont besoin d’accéder toosecure à partir de plusieurs tooAzure locaux de stations de travail, utilisez [VPN de site à site Azure](../vpn-gateway/vpn-gateway-site-to-site-create.md).

Pour les organisations qui ont besoin d’accéder toosecure à partir d’une station de travail trouve tooAzure local, utilisez [Point-to-Site VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md).

Les jeux de données volumineux peuvent être transmis par le biais d’une liaison réseau étendu haut débit dédiée, comme [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Si vous choisissez toouse ExpressRoute, vous pouvez également chiffrer les données de salutation à l’aide de niveau application hello [SSL/TLS](https://support.microsoft.com/kb/257591) ou d’autres protocoles pour une protection supplémentaire.

Si vous interagissez avec le stockage Azure via hello portail Azure, toutes les transactions se produisent via HTTPS. [API REST de stockage](https://msdn.microsoft.com/library/azure/dd179355.aspx) via le protocole HTTPS peut également être utilisé toointeract avec [Azure Storage](https://azure.microsoft.com/services/storage/) et [base de données SQL Azure](https://azure.microsoft.com/services/sql-database/).

Les organisations qui échouent tooprotect des données en transit sont plus vulnérables pour [man in the middle attaques](https://technet.microsoft.com/library/gg195821.aspx), [espionnage](https://technet.microsoft.com/library/gg195641.aspx) et le piratage de session. Ces attaques peuvent être hello première étape de pouvoir accéder aux données de tooconfidential.

Vous pouvez en savoir plus sur option Azure VPN en lisant l’article de hello [planification et conception pour la passerelle VPN](../vpn-gateway/vpn-gateway-plan-design.md).

## <a name="enforce-file-level-data-encryption"></a>Application du chiffrement des données au niveau fichier
Une autre couche de protection qui peut augmenter hello niveau de sécurité pour vos données est le chiffrement du fichier hello lui-même, quelle que soit l’emplacement du fichier hello.

[Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) toohelp de stratégies de chiffrement, d’identité et d’autorisation utilise sécuriser vos fichiers et les messages électroniques. Azure RMS peut fonctionner sur plusieurs appareils (téléphones, tablettes et PC), en protégeant les données au sein de votre organisation et en dehors de cette dernière. Cette fonctionnalité est possible, car Azure RMS ajoute un niveau de protection reste avec les données de salutation, même quand celles-ci quittent les limites de votre organisation.

Lorsque vous utilisez Azure RMS tooprotect vos fichiers, vous utilisez le chiffrement standard avec prise en charge complète de [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html). Lorsque vous exploitez Azure RMS pour la protection des données, vous disposez d’assurance de hello protection de hello est conservé avec le fichier de hello, même si elle est copiée toostorage qui n’est pas sous contrôle de code hello du service informatique, tel qu’un service de stockage cloud. Hello même se produit pour les fichiers partagés par courrier électronique, hello est protégé en tant qu’un message électronique de tooan pièce jointe, avec des instructions comment tooopen hello protégés pièce jointe.

Lors de la planification pour l’adoption d’Azure RMS, nous recommandons suivant de hello :

* Installer hello [application de partage RMS](https://technet.microsoft.com/library/dn339006.aspx). Cette application s’intègre avec les applications Office en installant un complément Office, afin que les utilisateurs puissent directement protéger leurs fichiers, en toute simplicité.
* Configurer des applications et services toosupport Azure RMS
* Créez des [modèles personnalisés](https://technet.microsoft.com/library/dn642472.aspx) qui reflètent les besoins de votre entreprise (exemple : un modèle portant sur des données ultra-secrètes, qui doit être appliqué à tous les e-mails ultra-secrets).

Les organisations qui sont faibles sur [classification des données](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) et la protection des fichiers peut-être être plus vulnérables toodata fuite. Sans protection de fichiers appropriées, les organisations ne tooobtain en mesure de gagner en visibilité, surveiller les abus et empêcher tout accès malveillant toofiles.

Vous pouvez en savoir plus sur Azure RMS, lisez l’article de hello [prise en main d’Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).
