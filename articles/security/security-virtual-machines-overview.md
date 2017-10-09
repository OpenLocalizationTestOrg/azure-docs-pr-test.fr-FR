---
title: "les fonctionnalités de sécurité aaaAzure utilisées avec les machines virtuelles | Documents Microsoft"
description: " Vue d’ensemble des fonctionnalités de sécurité Azure hello principales peuvent être utilisés avec les machines virtuelles. Fournissent des machines virtuelles Azure hello flexibilité de la virtualisation sans avoir toobuy et de mettre à jour le matériel physique hello qui s’exécute hello machine virtuelle. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 467b2c83-0352-4e9d-9788-c77fb400fe54
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: terrylan
ms.openlocfilehash: 1a1b9f02bd82a2655f4e2e5d9f9ce7a6671f63fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-security-overview"></a>Vue d’ensemble de la sécurité des machines virtuelles Azure
Azure Virtual Machines vous permet de déployer un large éventail de solutions de calcul de façon agile. Avec la prise en charge de Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP et Azure BizTalk Services, vous pouvez déployer des charges de travail et des langages variés sur la plupart des systèmes d’exploitation.

Une offre de machine virtuelle Azure hello flexibilité de la virtualisation sans avoir toobuy et de maintenir un matériel physique hello qui exécute hello virtual machine.  Vous pouvez générer et déployer vos applications avec assurance hello que vos données sont protégées et sécurisé dans nos centres de données hautement sécurisée.

Avec Azure, vous pouvez créer des solutions sécurisées et conformes qui :

* protègent vos machines virtuelles contre les virus et logiciels malveillants
* chiffrent vos données sensibles
* sécurisent le trafic réseau
* identifient et détectent les menaces
* respectent les exigences en matière de conformité

Hello cet article vise tooprovide une vue d’ensemble de fonctionnalités de sécurité Azure hello principales qui peut être utilisé avec des machines virtuelles. Nous fournissons également des liens tooarticles qui fournissent des détails de chaque fonctionnalité afin d’en savoir plus.  

Hello core Machine virtuelle Azure sécurité fonctionnalités toobe abordées dans cet article :

* Logiciel anti-programme malveillant
* Module de sécurité matériel
* Chiffrement du disque de machine virtuelle
* Sauvegarde de machine virtuelle
* Azure Site Recovery
* Réseau virtuel
* Gestion des stratégies de sécurité et création de rapports
* Conformité

## <a name="antimalware"></a>Logiciel anti-programme malveillant
Avec Azure, vous pouvez utiliser les logiciels anti-programme malveillant à partir des fournisseurs de sécurité telles que Microsoft, Symantec, Trend Micro et Kaspersky tooprotect vos machines virtuelles à partir de fichiers malveillants, de logiciels de publicité et d’autres menaces. Consultez hello en savoir plus section ci-dessous toofind articles sur les solutions de partenaire.

Microsoft Antimalware pour Azure Cloud Services et Virtual Machines offre une fonctionnalité de protection en temps réel qui permet d’identifier et de supprimer les virus, logiciels espions et autres logiciels malveillants.  Microsoft Antimalware fournit des alertes configurables vous avertissant lorsque connu tooinstall de tentatives de logiciels malveillants ou indésirables lui-même ou s’exécuter sur vos systèmes Azure.

Microsoft Antimalware est une solution d’agent unique pour les applications et les environnements de locataire, toorun conçue en arrière-plan hello sans intervention humaine. Vous pouvez déployer la protection en fonction des besoins de hello de votre application les charges de travail, avec une base sécurisée par défaut ou une configuration personnalisée, y compris les logiciels anti-programme malveillant d’analyse avancée.

Lorsque vous déployez et activez Microsoft Antimalware, hello suivant des fonctions de base est disponible :

* Protection en temps réel - surveille l’activité dans les Services de cloud computing et Machines virtuelles toodetect et bloc contre les programmes malveillants de l’exécution.
* Une analyse planifiée - effectue périodiquement ciblé analyse toodetect contre les programmes malveillants, y compris les programmes en cours d’exécution.
* Correction de logiciels malveillants : prend automatiquement des mesures sur les programmes malveillants détectés, notamment la suppression ou la mise en quarantaine des fichiers malveillants et le nettoyage des entrées de registre malveillantes.
* Mises à jour de signature - automatiquement installe hello protection signatures (définitions de virus) tooensure la protection plus récente est à jour selon une fréquence prédéterminée.
* Met à jour du moteur du logiciel anti-programme malveillant : automatiquement les mises à jour hello Microsoft Antimalware engine.
* Met à jour de logiciel anti-programme malveillant plateforme – automatiquement les mises à jour hello Microsoft Antimalware plateforme.
* Protection active - fournit des métadonnées de télémétrie tooAzure sur menaces détectées et ressources suspectes tooensure réponse et permet de signature synchrones en temps réel livraison rapide via hello Microsoft Active Protection système (MAPS).
* Exemples de création de rapports : fournit et exemples de rapports toohello Microsoft Antimalware service toohelp affiner le service de hello et la résolution des problèmes de l’activer.
* Exclusions – permet de tooconfigure les administrateurs de service d’application et de certains fichiers, des processus et lecteurs tooexclude de protection et de numérisation pour des raisons de performances et autres.
* Collecte d’événements de logiciel anti-programme malveillant - enregistre l’intégrité du service hello contre les logiciels malveillants, les activités suspectes et les actions de mise à jour effectuées dans le journal des événements système d’exploitation hello et les collecte dans le compte de stockage Azure hello client.

En savoir plus : reportez-vous à vos machines virtuelles, toolearn plus tooprotect de logiciel anti-programme malveillant :

* [Microsoft Antimalware pour Azure Cloud Services et les machines virtuelles](azure-security-antimalware.md)
* [Déploiement de solutions anti-programmes malveillants sur des machines virtuelles Azure (en anglais)](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [Comment tooinstall et configurer Trend Micro Deep Security en tant que Service sur une machine virtuelle Windows](../virtual-machines/windows/classic/install-trend.md)
* [Comment tooinstall et configurer Symantec Endpoint Protection sur une machine virtuelle Windows](../virtual-machines/windows/classic/install-symantec.md)
* [Solutions de sécurité Bonjour Azure Marketplace](https://azure.microsoft.com/marketplace/?term=security)

## <a name="hardware-security-module"></a>Module de sécurité matériel
Les protections par chiffrement et authentification peuvent être améliorées grâce à une meilleure clé de sécurité. Vous pouvez simplifier la gestion de hello et la sécurité de vos clés secrètes critiques et les clés en les stockant dans Azure Key Vault. Le coffre de clés fournit hello option toostore vos clés dans les normes de matériel sécurité certifiés tooFIPS de modules (HSM) 140-2 niveau 2. Vos clés de chiffrement SQL Server pour la sauvegarde ou le [chiffrement transparent des données](https://msdn.microsoft.com/library/bb934049.aspx) peuvent toutes être stockées dans Key Vault avec les clés ou secrets de vos applications. Autorisations et accéder aux éléments de toothese protégé sont gérées via [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).

En savoir plus :

* [Qu’est-ce qu’Azure Key Vault ?](../key-vault/key-vault-whatis.md)
* [Bien démarrer avec Azure Key Vault](../key-vault/key-vault-get-started.md)
* [Blog Azure Key Vault](https://blogs.technet.microsoft.com/kv/)

## <a name="virtual-machine-disk-encryption"></a>Chiffrement du disque de machine virtuelle
Azure Disk Encryption est une nouvelle fonctionnalité qui vous permet de chiffrer vos disques de machine virtuelle Windows et Linux Azure. Le chiffrement des disques Azure utilise la norme industrielle de hello [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) la fonctionnalité de Windows et hello [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt) fonctionnalité de chiffrement de volume tooprovide Linux pour hello du système d’exploitation et des disques de données hello.

solution de Hello est intégrée à Azure Key Vault toohelp contrôler et de gérer les clés de chiffrement de disque hello et des clés secrètes dans votre abonnement de coffre de clés, tout en garantissant que toutes les données de disques de machine virtuelle hello sont chiffrées au repos dans votre stockage Azure.

En savoir plus :

* [Azure Disk Encryption pour des machines virtuelles Windows et Linux IaaS](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)
* [Azure Disk Encryption pour les machines virtuelles Windows et Linux](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview-now-available/)
* [Chiffrement d’une machine virtuelle](../security-center/security-center-disk-encryption.md)

## <a name="virtual-machine-backup"></a>Sauvegarde de machine virtuelle
Sauvegarde Azure est une solution scalable qui protège les données de vos applications, sans aucun investissement en capital et avec des frais de fonctionnement minimaux. Les erreurs rencontrées par les applications peuvent endommager vos données et les erreurs humaines peuvent introduire des bogues dans vos applications. Avec Sauvegarde Azure, vos machines virtuelles exécutant Windows et Linux sont protégées.

En savoir plus :

* [Qu’est-ce que Sauvegarde Azure ?](../backup/backup-introduction-to-azure-backup.md)
* [Parcours d’apprentissage Sauvegarde Azure](https://azure.microsoft.com/documentation/learning-paths/backup/)
* [Service Sauvegarde Azure – Forum aux questions](../backup/backup-azure-backup-faq.md)

## <a name="azure-site-recovery"></a>Azure Site Recovery
Une partie importante de la stratégie de votre organisation BCDR est de savoir comment les charges de travail d’entreprise tookeep et applications des et en cours d’exécution lors de la planification et les arrêts se produisent. Azure Site Recovery aide à coordonner la réplication, le basculement et la récupération des charges de travail et des applications afin qu’elles soient disponibles à partir d’un site secondaire si votre site principal tombe en panne.

Site Recovery :

* **Simplifie votre stratégie de BCDR** : récupération de Site rend facile toohandle la réplication, le basculement et récupération de plusieurs charges de travail métier et d’applications à partir d’un emplacement unique. Site Recovery orchestre la réplication et le basculement, sans intercepter les données de vos applications ni posséder des informations à leur sujet.
* **Fournit une réplication flexible** : à l’aide de Site Recovery, vous pouvez répliquer des charges de travail s’exécutant sur des machines virtuelles Hyper-V et VMware, et des serveurs physiques Windows/Linux.
* **Prend en charge le basculement et la récupération** : récupération de Site fournit des exercices de récupération d’urgence toosupport basculements de test sans affecter les environnements de production. Vous pouvez également exécuter des basculements planifiés avec une perte de données zéro pour les interruptions attendues, ou des basculements non planifiés avec une perte de données minimale (en fonction de la fréquence de réplication) pour les incidents inattendus. Après le basculement, vous pouvez la restauration automatique tooyour les sites principaux. Site Recovery fournit des plans de récupération qui peuvent inclure des scripts et des classeurs Azure Automation afin que vous puissiez personnaliser le basculement et la récupération d’applications multiniveaux.
* **Élimine le centre de données secondaire** — vous pouvez répliquer site local secondaire de tooa ou tooAzure. À l’aide d’Azure comme destination de récupération d’urgence élimine hello coût et la complexité de la maintenance d’un site secondaire. Les données répliquées sont stockées dans Azure Storage.
* **S’intègre aux technologies existantes de continuité des activités et de récupération d’urgence** : Site Recovery collabore avec les fonctionnalités de continuité des activités et de récupération d’urgence d’autres applications. Par exemple, vous pouvez utiliser la récupération de Site tooprotect hello SQL Server back-end des charges de travail d’entreprise. Cela inclut la prise en charge native de SQL Server AlwaysOn toomanage hello basculement des groupes de disponibilité.

En savoir plus :

* [Qu’est-ce que le service Azure Site Recovery ?](../site-recovery/site-recovery-overview.md)
* [Comment Azure Site Recovery fonctionne-t-il ?](../site-recovery/site-recovery-components.md)
* [Quelles sont les charges de travail protégées par Azure Site Recovery ?](../site-recovery/site-recovery-workload.md)

## <a name="virtual-networking"></a>Réseau virtuel
Les machines virtuelles nécessitent une connectivité réseau. toosupport cette exigence, Azure nécessite toobe d’ordinateurs virtuels connecté tooan réseau virtuel Azure. Un réseau virtuel Azure est une construction logique reposant sur l’infrastructure du réseau Azure physique hello. Chaque réseau virtuel logique Azure est isolé des autres réseaux virtuels Azure. Cette isolation permet de s’assurer que le trafic réseau dans vos déploiements n’est pas accessible tooother les clients de Microsoft Azure.

En savoir plus :

* [Vue d’ensemble de la sécurité du réseau Azure](security-network-overview.md)
* [Présentation du réseau virtuel.](../virtual-network/virtual-networks-overview.md)
* [Fonctionnalités de mise en réseau et partenariats pour les scénarios d’entreprise](https://azure.microsoft.com/blog/networking-enterprise/)

## <a name="security-policy-management-and-reporting"></a>Gestion des stratégies de sécurité et création de rapports
Azure Security Center vous aide à empêcher, détecter et répondre toothreats et fournit le qu'augmentation de la visibilité et contrôler, sécurité hello de vos ressources Azure. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.

Le Centre de sécurité Azure vous permet d’optimiser et de surveiller la sécurité des machines virtuelles grâce aux opérations suivantes :

* Proposition de [recommandations de sécurité](../security-center/security-center-recommendations.md) sur la machine virtuelle, telles que l’application des mises à jour système, la configuration des points de terminaison ACL, l’activation des logiciels anti-programme malveillant, l’activation des groupes de sécurité réseau et l’application du chiffrement de disque.
* Analyse de l’état de hello de vos machines virtuelles

En savoir plus :

* [Introduction tooAzure centre de sécurité](../security-center/security-center-intro.md)
* [FAQ du Centre de sécurité Azure](../security-center/security-center-faq.md)
* [Opérations et planification du Centre de sécurité Azure](../security-center/security-center-planning-and-operations-guide.md)

## <a name="compliance"></a>Conformité
Azure Virtual Machines bénéficie des certifications FISMA, FedRAMP, HIPAA, PCI DSS Level 1 et de celles d’autres programmes majeurs de conformité. Cette certification facilite pour vos propres exigences de conformité des applications Azure toomeet et tooaddress de votre entreprise un large éventail des réglementations nationales et internationales.

En savoir plus :

* [Centre de gestion de la confidentialité Microsoft - Conformité](https://www.microsoft.com/TrustCenter/Compliance/default.aspx)
* [Cloud de confiance : sécurité, confidentialité et conformité dans Microsoft Azure](http://download.microsoft.com/download/1/6/0/160216AA-8445-480B-B60F-5C8EC8067FCA/WindowsAzure-SecurityPrivacyCompliance.pdf)
