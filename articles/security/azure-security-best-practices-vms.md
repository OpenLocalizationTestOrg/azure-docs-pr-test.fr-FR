---
title: "meilleures pratiques de la sécurité de machine virtuelle aaaAzure | Documents Microsoft"
description: "Cet article fournit un éventail de sécurité meilleures pratiques toobe est utilisé dans les machines virtuelles situées dans Azure."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 5e757abe-16f6-41d5-b1be-e647100036d8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: b03bcc75fde6d49897f9a7f6f15aec87456edd0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-vm-security"></a>Meilleures pratiques pour la sécurité des machines virtuelles Azure

Dans la plupart des infrastructures en tant que scénarios un service (IaaS), [machines virtuelles (VM) Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/) est le calcul de charge de travail principale hello pour les organisations qui utilisent le cloud. Cela est particulièrement évident dans [scénarios hybrides](https://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) où les entreprises que vous souhaitez tooslowly migrer cloud toohello de charges de travail. Dans de tels scénarios, suivez hello [considérations de sécurité générales pour IaaS](https://social.technet.microsoft.com/wiki/contents/articles/3808.security-considerations-for-infrastructure-as-a-service-iaas.aspx)et appliquer sécurité meilleures pratiques tooall vos machines virtuelles.

Cet article décrit différentes meilleures pratiques de sécurité qui sont le résultat de nos expériences ou de celles de nos clients avec les machines virtuelles.

meilleures pratiques de Hello sont basées sur un consensus d’avis, et qu’ils fonctionnent avec les capacités de plateforme Azure actuelles et jeux de fonctionnalités. Étant donné que les avis et technologies peuvent changer au fil du temps, nous prévoyons de tooupdate cet article régulièrement tooreflect ces modifications.

Pour chaque meilleure pratique, l’article de hello explique :

* Quelles hello est préférable.
* Pourquoi il est une bonne idée tooenable il.
* Comment vous pouvez apprendre tooenable il.
* Ce qui peut se produire si vous ne parvenez pas tooenable il.
* Les alternatives possibles toohello meilleure pratique.

article de Hello examine hello suivant les meilleures pratiques de sécurité des ordinateurs virtuels :

* Authentification des machines virtuelles et contrôle d’accès à celles-ci
* Disponibilité des machines virtuelles et accès au réseau
* Protéger les données au repos sur les machines virtuelles Azure à l’aide du chiffrement
* Gérer les sauvegardes des machines virtuelles
* Gérer l’état de sécurité des machines virtuelles
* Analyser les performances des machines virtuelles

## <a name="vm-authentication-and-access-control"></a>Authentification des machines virtuelles et contrôle d’accès à celles-ci

Hello première étape pour protéger votre machine virtuelle est tooensure que seuls les utilisateurs autorisés sont en mesure de tooset des nouvelles machines virtuelles. Vous pouvez utiliser [Azure Resource Manager stratégies](../azure-resource-manager/resource-manager-policy.md) tooestablish des conventions pour les ressources de votre organisation, créer des stratégies personnalisées et appliquer ces stratégies tooresources, telles que [les groupes de ressources](../azure-resource-manager/resource-group-overview.md).

Machines virtuelles qui font partie de groupe de ressources tooa naturellement héritent de ses stratégies. Bien que nous recommandons cette approche toomanaging VM, vous pouvez également stratégies de machine virtuelle tooindividual contrôle d’accès à l’aide de [contrôle d’accès basé sur un rôle (RBAC)](../active-directory/role-based-access-control-configure.md).

Lorsque vous activez des stratégies du Gestionnaire de ressources et accès de machine virtuelle toocontrol RBAC, vous aider à améliorer la sécurité globale de machine virtuelle. Nous vous recommandons de consolider les machines virtuelles avec hello du cycle de vie de même dans hello même groupe de ressources. Les groupes de ressources vous aident à déployer et surveiller vos ressources, tout en compilant leur coût. tooenable utilisateurs tooaccess et configurer des ordinateurs virtuels, utilisez un [approche de privilège minimum](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models). Et lorsque vous affectez des privilèges toousers, planifiez hello toouse suivant des rôles Azure intégrés :

- [Machine virtuelle collaborateur](../active-directory/role-based-access-built-in-roles.md#virtual-machine-contributor): peut gérer des ordinateurs virtuels, mais pas hello virtuel toowhich compte de stockage ou réseau qu’ils sont connectés.
- [Classique collaborateur de Machine virtuelle](../active-directory/role-based-access-built-in-roles.md#classic-virtual-machine-contributor): peut gérer des machines virtuelles créées à l’aide de modèle de déploiement classique de hello, mais pas hello virtuel réseau ou stockage compte toowhich hello machines virtuelles sont connectées.
- [Gestionnaire de sécurité](../active-directory/role-based-access-built-in-roles.md#security-manager) : peut gérer les composants de sécurité, les stratégies de sécurité et les machines virtuelles.
- [Utilisateur de DevTest Labs](../active-directory/role-based-access-built-in-roles.md#devtest-labs-user) : peut tout afficher et connecter, démarrer, redémarrer et arrêter les machines virtuelles.

Ne partagez pas les comptes ou les mots de passe entre plusieurs administrateurs, et ne réutilisez pas les mots de passe dans plusieurs comptes d’utilisateur ou services, notamment pour les médias sociaux ou d’autres activités non administratives. Dans l’idéal, vous devez utiliser [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooset de modèles de vos machines virtuelles en toute sécurité. À l’aide de cette approche, vous pouvez renforcer votre choix de déploiement et appliquer les paramètres de sécurité tout au long du déploiement de hello.

Les organisations qui n’appliquent aucun contrôle d’accès aux données grâce aux fonctionnalités telles que RBAC risquent d’octroyer plus de privilèges que nécessaire à leurs utilisateurs. Données de toocertain accès utilisateur inappropriée peuvent compromettre directement ces données.

## <a name="vm-availability-and-network-access"></a>Disponibilité des machines virtuelles et accès au réseau

Si votre machine virtuelle exécute des applications critiques nécessitant toohave haute disponibilité, nous vous recommandons vivement d’utiliser plusieurs machines virtuelles. Pour augmenter la disponibilité, créez au moins deux machines virtuelles Bonjour [à haute disponibilité](../virtual-machines/windows/tutorial-availability-sets.md).

[L’équilibrage de charge Azure](../load-balancer/load-balancer-overview.md) requiert également qu’équilibrage de la charge de machines virtuelles appartiennent toohello même groupe à haute disponibilité. Si ces ordinateurs virtuels doivent être accessibles à partir de hello Internet, vous devez configurer un [équilibrage de charge connecté à Internet](../load-balancer/load-balancer-internet-overview.md).

Lorsque les machines virtuelles sont exposé toohello Internet, il est important que vous avez [contrôler le flux de trafic réseau avec des groupes de sécurité réseau (NSG)](../virtual-network/virtual-networks-nsg.md). Étant donné que les groupes de sécurité réseau peuvent être appliqués toosubnets, vous pouvez réduire nombre hello de groupes de sécurité réseau par vos ressources de regroupement par sous-réseau et l’application sous-réseaux toohello de groupes de sécurité réseau. intention de Hello est toocreate une couche d’isolement réseau, ce que vous pouvez faire en configurant correctement hello [sécurité réseau](../best-practices-network-security.md) fonctionnalités dans Azure.

Vous pouvez également utiliser la fonctionnalité de machine virtuelle (JIT) à l’accès juste-à-temps hello de toocontrol Azure Security Center qui a accès à distance tooa ordinateur virtuel spécifique et pendant combien de temps.

Les organisations qui n’appliquent des restrictions d’accès réseau sont des machines virtuelles de tooInternet côté exposé risques toosecurity, tel qu’une attaque en Force Brute protocole RDP (Remote Desktop).

## <a name="protect-data-at-rest-in-your-vms-by-enforcing-encryption"></a>Protéger les données au repos sur les machines virtuelles Azure à l’aide du chiffrement

Le [chiffrement des données au repos](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) est une étape obligatoire vers la confidentialité, la conformité et la souveraineté des données. [Le chiffrement des disques Azure](../security/azure-security-disk-encryption.md) Active tooencrypt des administrateurs informatiques Windows et les disques de machine virtuelle IaaS de Linux. Chiffrement de disque combine les fonctionnalités de BitLocker de Windows hello normalisées et hello Linux dm-crypt fonctionnalité tooprovide le chiffrement de volume pour hello du système d’exploitation et des disques de données hello.

Vous pouvez appliquer le chiffrement de disque toohelp protéger votre toomeet données exigences conformité et de sécurité de votre organisation. Votre organisation doit prendre en compte l’utilisation du chiffrement toohelp atténuer les risques liés à l’accès aux données toounauthorized connexes. Nous vous recommandons également de chiffrer de vos lecteurs avant d’écrire des données sensibles toothem.

Être tooencrypt que votre tooprotect de volumes de données de machine virtuelle les au repos dans votre compte de stockage Azure. Protéger les clés de chiffrement hello et la clé secrète à l’aide de [Azure Key Vault](https://azure.microsoft.com/en-us/documentation/articles/key-vault-whatis/).

Les organisations qui n’appliquent pas de chiffrement des données sont plus les problèmes d’intégrité toodata exposé. Par exemple, utilisateurs non autorisés ou non fiables peuvent voler des données de comptes compromis ou obtenir toodata contre tout accès codé dans ClearFormat. Outre prise sur ces risques, toocomply avec les réglementations du secteur, les sociétés doivent prouver qu’ils exercent diligence et à l’aide de sécurité correct contrôle tooenhance leur sécurité des données.

toolearn en savoir plus sur le chiffrement de disque, consultez [chiffrement de disque Azure pour Windows et les machines virtuelles IaaS Linux](azure-security-disk-encryption.md).


## <a name="manage-your-vm-updates"></a>Gérer les sauvegardes des machines virtuelles

Machines virtuelles Azure, comme toutes les locaux machines virtuelles, sont prévu toobe gérées par l’utilisateur, Azure ne push toothem de mises à jour de Windows. Toutefois, vous êtes encouragé tooleave paramètre de mise à jour Windows automatique hello activé. Une autre option consiste à toodeploy [Windows Server Update Services (WSUS)](https://technet.microsoft.com/windowsserver/bb332157.aspx) ou un autre produit appropriée de gestion des mises à jour sur une autre machine virtuelle ou sur site. WSUS et Windows Update maintiennent les machines virtuelles à jour. Nous vous recommandons également d’utiliser une analyse tooverify produit qui sont toutes vos machines virtuelles IaaS de toodate.

Parmi les images fournies par Azure sont hello tooinclude régulièrement mis à jour la plus récente round mises à jour Windows. Toutefois, il n’existe aucune garantie que les images hello sera en cours au moment du déploiement. Un léger décalage (de quelques semaines au maximum) après la diffusion des mises à jour est possible. Rechercher et installer toutes les mises à jour de Windows doivent être hello première étape de chaque déploiement. Cette mesure est tooapply particulièrement important lorsque vous déployez des images provenant de vous ou votre propre bibliothèque. Les images qui sont fournies dans le cadre de hello Azure Marketplace sont automatiquement mises à jour par défaut.

Les organisations qui n’appliquent les stratégies de mise à jour de logiciels sont plus exposés toothreats qui exploitent les vulnérabilités connues, précédemment fixes. Outre risquer de ces menaces, toocomply avec les réglementations du secteur, les sociétés doivent prouver qu’ils exercent diligence et toohelp des contrôles de sécurité appropriées à l’aide de garantir la sécurité de hello de leur charge de travail situé dans le cloud de hello.

Il est important tooemphasize que les meilleures pratiques pour les centres de données traditionnels mise à jour logicielle et IaaS Azure présentent de nombreuses similitudes. Par conséquent, nous recommandons que vous évaluez votre tooinclude de stratégies de mise à jour de machines virtuelles logiciel actuel.

## <a name="manage-your-vm-security-posture"></a>Gérer l’état de sécurité des machines virtuelles

Les menaces sont en constante évolution et la protection de vos ordinateurs virtuels nécessite une capacité d’analyse de riches qui peuvent rapidement détecter les menaces, empêcher les accès non autorisé tooyour ressources, déclenchent des alertes et réduire les faux positifs. posture de sécurité Hello pour une telle charge de travail comprend tous les aspects de sécurité de hello machine virtuelle, à partir de l’accès au réseau de mise à jour de gestion toosecure.

posture de sécurité hello toomonitor votre [Windows](../security-center/security-center-virtual-machine.md) et [les machines virtuelles Linux](../security-center/security-center-linux-virtual-machine.md), utilisez [Azure Security Center](../security-center/security-center-intro.md). Dans le centre de sécurité Azure, protégez vos machines virtuelles en tirant parti de hello suivant des fonctions :

* Appliquer les paramètres de sécurité du système d’exploitation avec les règles de configuration recommandées
* Rechercher et télécharger les mises à jour critiques et les mises à jour de sécurité qui peuvent être manquantes
* Mettre en œuvre les recommandations de protection contre les logiciels malveillants
* Valider le chiffrement des disques
* Évaluer et corriger les vulnérabilités
* Détecter les menaces

Security Center peut surveiller activement les menaces qui sont identifiées sous **Alertes de sécurité**. Les menaces corrélées sont regroupées dans la vue **Incident de sécurité**.

toounderstand comment le centre de sécurité peuvent vous aider à identifier les menaces potentielles dans vos machines virtuelles situées dans Azure, regardez hello suivant vidéo :

<iframe src="https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Security-Center-in-Incident-Response/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

Les organisations qui n’appliquent pas une méthode de sécurité renforcée pour leurs ordinateurs virtuels restent sans se préoccuper de tentatives potentielles par des utilisateurs non autorisés de contrôles de sécurité toocircumvent établie.

## <a name="monitor-vm-performance"></a>Analyser les performances des machines virtuelles

Parfois, une machine virtuelle consomme trop de ressources, ce qui peut poser problème. Tooservice toute interruption, ce qui viole le principe de sécurité hello de disponibilité peuvent provoquer des problèmes de performances avec une machine virtuelle. Pour cette raison, il est impératif toomonitor vmaccess pas uniquement réactive, lorsqu’un problème se produit, mais également proactive, par rapport aux performances de ligne de base de fonctionnement normal.

En analysant les [fichiers journaux de diagnostic Azure](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/), vous pouvez surveiller les ressources de vos machines virtuelles et identifier les problèmes potentiels susceptibles de nuire à la disponibilité et aux performances. Hello Extension des Diagnostics Azure fournit des fonctionnalités d’analyse et de diagnostics sur des machines virtuelles basées sur Windows. Vous pouvez activer ces fonctionnalités en incluant l’extension de hello dans le cadre de hello [modèle Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md).

Vous pouvez également utiliser [moniteur Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) toogain visibilité de contrôle d’intégrité de votre ressource.

Les organisations qui ne pas surveiller les performances de la machine virtuelle sont toodetermine impossible si certaines modifications dans les modèles de performances sont normal ou anormal. Si hello VM consomme davantage de ressources que la normale, ce type d’anomalie peut indiquer une attaque potentielle à partir d’une ressource externe ou un processus compromis en cours d’exécution dans hello machine virtuelle.
