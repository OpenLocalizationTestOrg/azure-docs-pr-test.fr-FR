---
title: aaaAzure Forum aux questions sur le chiffrement de disque | Documents Microsoft
description: "Cet article fournit des réponses aux questions sur Microsoft Azure disque chiffrement pour Windows et les machines virtuelles IaaS Linux d’elles sonttrop."
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: 7188da52-5540-421d-bf45-d124dee74979
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: devtiw
ms.openlocfilehash: 17f084628ba4ef22e9d37dd3052ef10f8eb2cd7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-frequently-asked-questions-faq"></a>Forum aux questions sur Azure Disk Encryption

Ce FAQ répond aux questions sur Azure Disk Encryption pour les machines virtuelles IaaS Windows et Linux. Pour plus d’informations sur ce service, consultez la page [Chiffrement de disque Azure pour des machines virtuelles Windows et Linux IaaS](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

## <a name="general-questions"></a>Questions générales
**Q.** Dans quelles régions Azure Disk Encryption est-il en disponibilité générale ?

**R :** Le chiffrement Azure Disk Encryption pour les machines virtuelles IaaS Windows et Linux est en disponibilité générale dans toutes les régions publiques Azure.

**Q :** Avec quelles autres expériences utilisateur Azure Disk Encryption est-il disponible ?

**R :** Azure Disk Encryption (disponibilité générale) prend en charge les modèles Azure Resource Manager, Azure PowerShell et Azure CLI. Cela vous donne une grande flexibilité, car vous disposez de trois options différentes pour activer le chiffrement des disques sur vos machines virtuelles IaaS. Plus d’informations sur l’expérience utilisateur hello et des instructions pas à pas est disponible dans des expériences et des scénarios de déploiement du chiffrement de disque Azure hello.

**Q :** Combien coûte Azure Disk Encryption ?

**R :** Le chiffrement des disques de machines virtuelles avec Azure Disk Encryption est gratuit.

**Q :** Avec quels niveaux de machines virtuelles puis-je utiliser Azure Disk Encryption ?

**R :** Azure Disk Encryption est disponible uniquement sur les machines virtuelles de niveau standard, notamment avec les machines virtuelles IaaS séries [A, D, DS, G, GS, F](https://azure.microsoft.com/pricing/details/virtual-machines/), etc., incluant également les machines avec stockage Premium. Il n’est pas disponible sur les machines virtuelles de niveau de base.

**Q :** Quelles sont les distributions Linux prises en charge par Azure Disk Encryption ?

**R :** hello suivant les distributions Linux server et les versions est pris en charge le chiffrement des disques Azure :

| Distribution Linux | Version | Type de volume pris en charge pour le chiffrement|
| --- | --- |--- |
| Ubuntu | 16.04-DAILY-LTS | Disque de système d’exploitation et de données |
| Ubuntu | 14.04.5-DAILY-LTS | Disque de système d’exploitation et de données |
| RHEL | 7.3 | Disque de système d’exploitation et de données |
| RHEL | 7,2 | Disque de système d’exploitation et de données |
| RHEL | 6,8 | Disque de système d’exploitation et de données |
| RHEL | 6.7 | Disque de données |
| CentOS | 7.3 | Disque de système d’exploitation et de données |
| CentOS | 7.2n | Disque de système d’exploitation et de données |
| CentOS | 6.8 | Disque de système d’exploitation et de données |
| CentOS | 7.1 | Disque de données |
| CentOS | 7.0 | Disque de données |
| CentOS | 6.7 | Disque de données |
| CentOS | 6.6 | Disque de données |
| CentOS | 6.5 | Disque de données |
| openSUSE | 13.2 | Disque de données |
| SLES | 12 SP1 | Disque de données |
| SLES | Priority:12-SP1 | Disque de données |
| SLES | HPC 12 | Disque de données |
| SLES | Priority:11-SP4 | Disque de données |
| SLES | 11 SP4 | Disque de données |

**Q :** Comment puis-je commencer à utiliser Azure Disk Encryption ?

**R :** pour en savoir comment tooget démarrée par la lecture hello livre blanc de chiffrement de disque Azure situé [ici](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)

**Q :** Puis-je chiffrer des volumes de démarrage et de données avec Azure Disk Encryption ?

**R :** Oui, vous pouvez chiffrer des volumes de démarrage et de données pour les machines virtuelles IaaS Windows et Linux. Pour les machines virtuelles Windows, vous ne pouvez pas chiffrer les données de hello sans hello encrpting premier volume de système d’exploitation. Pour les machines virtuelles Linux, vous pouvez chiffrer tout d’abord le volume de données hello sans encryptinng hello volume du système d’exploitation. Une fois que vous avez chiffré le volume de hello du système d’exploitation pour Liux, la désactivation du chiffrement sur un volume du système d’exploitation pour les machines virtuelles IaaS Linux n’est pas pris en charge

**Q :** Azure Disk Encryption propose-t-il une fonctionnalité « BYOK » (apportez votre propre clé) ?

**R :** Oui, vous pouvez fournir vos propres clés de chiffrement à clé. Ces clés sont sauvegardés dans le coffre de clés Azure, qui est le magasin de clés hello pour le chiffrement du disque Azure. Pour plus d’informations sur la clé de chiffrement à clé hello prend en charge les scénarios, consultez les expériences et des scénarios de déploiement du chiffrement de disque Azure hello

**Q :** Puis-je utiliser une clé de chiffrement à clé créé par Azure ?

**R :** Oui, vous pouvez utiliser la clé de chiffrement d’Azure Key vault toogenerate pour une utilisation de chiffrement de disque Azure. Ces clés sont sauvegardés dans le coffre de clés Azure, qui est le magasin de clés hello pour le chiffrement du disque Azure. Pour plus d’informations sur la clé de chiffrement à clé hello prend en charge les scénarios, consultez les expériences et des scénarios de déploiement du chiffrement de disque Azure hello

**Q :** puis-je utiliser des clés de chiffrement local gestion de clés toosafeguard de service/HSM hello ?

**R :** vous ne pouvez pas utiliser les clés de chiffrement du gestion de clés toosafeguard de service/HSM hello hello localement avec le chiffrement de disque Azure. Vous pouvez uniquement utiliser des clés de chiffrement du service toosafeguard hello hello coffre de clés Azure. Pour plus d’informations sur la clé de chiffrement à clé hello prend en charge les scénarios, consultez les expériences et des scénarios de déploiement du chiffrement de disque Azure hello

**Q :** quels sont le chiffrement de disque Azure hello conditions préalables tooconfigure ?

**R :** hello application disque Azure chiffrement requise PowerShell script toocreate AAD, créer nouveau coffre de clés ou le programme d’installation de coffre de clés existant pour le disque chiffrement accès tooenable chiffrement et sauvegarde des secrets et la clé.  Pour plus d’informations sur la clé de chiffrement à clé hello prend en charge les scénarios, consultez les conditions préalables de chiffrement de disque Azure hello et des expériences et des scénarios de déploiement

**Q :** où puis-je obtenir plus d’informations sur la façon de toouse PowerShell pour la configuration de chiffrement de disque Azure ?

**R :** Vous pouvez consulter des articles très intéressants sur l’exécution de tâches Azure Disk Encryption de base, ainsi que des exemples de scénarios plus avancés. Pour les tâches de base hello, consultez Explorer [le chiffrement de disque Azure avec Azure PowerShell - partie 1](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/explore-azure-disk-encryption-with-azure-powershell/). Pour connaître les scénarios plus avancés, consultez le billet de blog en anglais [Azure Disk Encryption with Azure PowerShell – Part 2](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2/) (Explorer Azure Disk Encryption avec Azure PowerShell - Partie 2).

**Q :** Quelle version d’Azure PowerShell est prise en charge par Azure Disk Encryption ?

**R :** utiliser hello la dernière version du Kit de développement logiciel Azure PowerShell version tooconfigure chiffrement de disque Azure. Télécharger la version la plus récente de hello [Azure PowerShell](https://github.com/Azure/azure-powershell/releases). Azure Disk Encryption n’est PAS pris en charge par le Kit de développement logiciel (SDK) Azure PowerShell version 1.1.0.

> [!NOTE]
> Hello, extension d’Aperçu de chiffrement de disque Linux Azure est déconseillée. Pour plus d’informations, consultez toodocumentation [ici](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/12/deprecating-azure-disk-encryption-preview-extension-for-linux-iaas-vms/)

**Q :** Puis-je appliquer le chiffrement de disque Azure sur mon image Linux personnalisée ?

**R :** Vous ne pouvez pas appliquer le chiffrement de disque Azure sur votre image Linux personnalisée. Nous prenons en charge les images Linux de la galerie uniquement hello pour hello pris en charge les versions indiquées ci-dessus. Actuellement, nous ne prenons pas en charge les images Linux personnalisées.

**Q :** puis-je appliquer les mises à jour tooa Linux Red Hat VM à l’aide de la mise à jour Yum ?

**R :** Oui, vous pouvez appliquer une mise à jour ou un correctif sur une machine virtuelle Red Hat Linux en suivant les instructions décrites[ici](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/13/applying-updates-to-a-encrypted-azure-iaas-red-hat-vm-using-yum-update/)

**Q :** où puis-je accéder tooask question ou fournir des commentaires

**R :** vous permettent de poser des questions ou des commentaires sur le forum de chiffrement de disque Azure hello [ici](https://social.msdn.microsoft.com/Forums/home?forum=AzureDiskEncryption)

## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez appris plus hello plus fréquentes questions connexes tooAzure chiffrement de disque, pour plus d’informations sur ce service et de sa capacité à lire :

- [Appliquer le chiffrement de disque dans Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Chiffrement d’une machine virtuelle Azure](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Azure Data Encryption-at-Rest](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest) (Chiffrement des données Azure au repos)
