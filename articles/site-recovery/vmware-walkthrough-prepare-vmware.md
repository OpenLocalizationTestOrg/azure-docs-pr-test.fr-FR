---
title: "aaaPrepare VMware ressources locales pour tooAzure de réplication avec Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello pour répliquer les charges de travail en cours d’exécution sur les ordinateurs virtuels VMware tooAzure stockage"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 6aba0e89-ad7c-467e-9db2-cfb3bfe4c7d6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 09d81f15f6ee764135a62f5555e458c55fa30048
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-on-premises-vmware-replication-tooazure"></a>Étape 6 : Préparation de tooAzure de réplication locale VMware

Utilisez les instructions hello dans cette toointeract de serveurs VMware de l’article tooprepare local avec Azure Site Recovery et préparer des ordinateurs virtuels VMWare à l’installation du service mobilité de hello. agent de service de mobilité Hello doit être installé sur tous les ordinateurs virtuels de local que vous souhaitez tooreplicate tooAzure.

## <a name="prepare-for-automatic-discovery"></a>Préparation pour la détection automatique

Site Recovery détecte automatiquement les machines virtuelles s’exécutant sur des hôtes ESXi vSphere (avec ou sans serveur vCenter). Pour la détection automatique, les besoins de récupération de Site un hôtes tooaccess de compte et les serveurs :

1. toouse un compte dédié, créer un rôle (au niveau de vCenter hello, avec des autorisations hello décrites dans le tableau hello ci-dessous. Donnez-lui un nom, tel que **Azure_Site_Recovery**.
2. Ensuite, créez un utilisateur sur le serveur hôte/vCenter de vSphere hello et affecter hello rôle toohello utilisateur. Vous spécifiez ce compte d’utilisateur pendant le déploiement de Site Recovery.


### <a name="vmware-account-permissions"></a>Autorisations du compte VMware

Les besoins de récupération de site accès tooVMware hello processus serveur tooautomatically découvrir les machines virtuelles et pour le basculement et la restauration des machines virtuelles.

- **Migrer**: Si vous souhaitez uniquement toomigrate les ordinateurs virtuels VMware tooAzure, sans jamais les échoue de nouveau, vous pouvez utiliser un compte de VMware avec un rôle en lecture seule. Ce type de rôle peut exécuter le basculement mais ne peut pas arrêter les machines source protégées. Cela n’est pas nécessaire pour la migration.
- **Réplication/récupération**: Si vous souhaitez que le compte de hello toodeploy réplication complète (replicate, basculement, la restauration automatique) doit être toorun en mesure des opérations telles que la création et la suppression de disques, sous tension etc. de machines virtuelles.
- **Découverte automatique** : au moins un compte en lecture seule est nécessaire.


**Tâche** | **Nécessite un compte/rôle** | **Autorisations** | **Détails**
--- | --- | --- | ---
**Le serveur de processus découvre automatiquement les machines virtuelles VMware** | Vous devez disposer d’au moins un utilisateur en lecture seule | Objet de centre de données -> propager tooChild objet rôle = lecture seule | Utilisateur affecté au niveau du centre de données et a accès tooall hello objets dans le centre de données hello.<br/><br/> accès toorestrict, affecter hello **aucun accès** rôle avec hello **propager toochild** toohello des objets enfants (hôtes de vSphere, magasins de données, machines virtuelles et réseaux), l’objet.
**Type de basculement** | Vous devez disposer d’au moins un utilisateur en lecture seule | Objet de centre de données -> propager tooChild objet rôle = lecture seule | Utilisateur affecté au niveau du centre de données et a accès tooall hello objets dans le centre de données hello.<br/><br/> accès toorestrict, affecter hello **aucun accès** rôle avec hello **propager toochild** toohello (hôtes de vSphere, magasins de données, machines virtuelles et réseaux) des objets enfants de l’objet.<br/><br/> Utile à des fins de migration, mais pas pour la réplication complète, le basculement et la restauration automatique.
**Basculement et restauration automatique** | Nous vous suggérons de vous créez un rôle (Azure_Site_Recovery) avec les autorisations hello requis, puis affectez hello rôle tooa VMware utilisateur ou un groupe | Objet de centre de données -> propager tooChild objet rôle = Azure_Site_Recovery<br/><br/> Banque de données -> Allouer de l’espace, parcourir la banque de données, opérations de fichier de bas niveau, supprimer le fichier, mettre à jour les fichiers de machine virtuelle<br/><br/> Réseau -> Attribution de réseau<br/><br/> Ressource -> pool tooresource d’affecter un ordinateur virtuel, migrez la machine virtuelle hors tension, migrer sous tension sur la machine virtuelle<br/><br/> Tâches -> Créer une tâche, Mettre à jour une tâche<br/><br/> Machine virtuelle -> Configuration<br/><br/> Machine virtuelle -> Interagir -> répondre à la question, connexion d’appareil, configurer un support de CD, configurer une disquette, mettre hors tension, mettre sous tension, installation des outils VMware<br/><br/> Machine virtuelle -> Stock -> Créer, inscrire, désinscrire<br/><br/> Machine virtuelle -> Approvisionnement -> Autoriser le téléchargement de machines virtuelles, autoriser le chargement de fichiers de machine virtuelle<br/><br/> Machine virtuelle -> Instantanés -> Supprimer les instantanés | Utilisateur affecté au niveau du centre de données et a accès tooall hello objets dans le centre de données hello.<br/><br/> accès toorestrict, affecter hello **aucun accès** rôle avec hello **propager toochild** toohello des objets enfants (hôtes de vSphere, magasins de données, machines virtuelles et réseaux), l’objet.


## <a name="prepare-for-push-installation-of-hello-mobility-service"></a>Préparer l’installation push du service mobilité de hello

Hello service mobilité doit être installé sur tous les ordinateurs virtuels, vous souhaitez tooreplicate. Il existe plusieurs façons tooinstall hello du service de, y compris l’installation manuelle, une installation poussée du serveur de processus de récupération de Site hello et installation à l’aide de méthodes telles que System Center Configuration Manager.

Si vous souhaitez toouse poussée, vous devez tooprepare un compte que récupération de Site peut utiliser tooaccess hello machine virtuelle.

- Vous pouvez utiliser un compte local ou de domaine
- Pour Windows, si vous n’utilisez pas un compte de domaine, vous devez toodisable contrôle des accès utilisateur à distance sur l’ordinateur local de hello. toodo, Bonjour Enregistrer sous **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, ajouter l’entrée DWORD de hello **LocalAccountTokenFilterPolicy**, avec la valeur 1.
- Si vous souhaitez l’entrée de Registre tooadd hello pour Windows à partir d’une interface CLI, tapez :``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
- Pour Linux, hello doit être racine sur le serveur de Linux hello source.



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 7 : créer un coffre](vmware-walkthrough-create-vault.md)
