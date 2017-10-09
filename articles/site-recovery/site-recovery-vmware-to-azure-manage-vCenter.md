---
title: " Gérer un serveur VMware vCenter dans Azure Site Recovery | Microsoft Docs"
description: "Cet article explique comment ajouter et gérer VMware vCenter dans Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 5be995f137d0c0efaf3050b5366a107098cae15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-vmware-vcenter-server-in-azure-site-recovery"></a>Gérer un serveur VMware vCenter dans Azure Site Recovery
Cet article traite de hello diverses opérations de récupération de Site qui peuvent être effectuées sur un serveur VMware vCenter.

## <a name="prerequisites"></a>Composants requis

**Prise en charge du serveur VMware vCenter et de l’hôte VMware vSphere ESX** | **Détails** |
|--- | --- |
|**Serveurs VMware locaux** | Un ou plusieurs serveurs VMware vSphere exécutant la version 6.0, 5.5, 5.1 avec les dernières mises à jour. Les serveurs doivent se trouver dans le même réseau que le serveur de configuration hello (ou un serveur de processus distinct) de hello.<br/><br/> Nous vous recommandons un vCenter server toomanage hôtes, exécutant 6.0 ou 5.5 avec les dernières mises à jour de hello. Seules les fonctionnalités disponibles dans la version 5.5 sont prises en charge lorsque du déploiement de la version 6.0.|

## <a name="prepare-an-account-for-automatic-discovery"></a>Préparer un compte pour la découverte automatique
Les besoins de récupération de site accès tooVMware hello processus serveur tooautomatically découvrir les ordinateurs virtuels et pour le basculement et la restauration des machines virtuelles.

* **Migrer**: Si vous souhaitez uniquement toomigrate tooAzure de machines virtuelles VMware, sans jamais les échoue de nouveau, vous pouvez utiliser un compte de VMware avec un rôle en lecture seule. Ce type de rôle peut exécuter le basculement mais ne peut pas arrêter les machines source protégées. Cela n’est pas nécessaire pour la migration.
* **Réplication/récupération**: Si vous souhaitez que le compte de hello toodeploy réplication complète (replicate, basculement, la restauration automatique) doit être toorun en mesure des opérations telles que la création et la suppression de disques, la mise sous tension sur l’ordinateur virtuel.
* **Découverte automatique** : au moins un compte en lecture seule est nécessaire.


|**Tâches :** | **Nécessite un compte/rôle** | **Autorisations** | **Détails**|
|--- | --- | --- | ---|
|**Le serveur de processus découvre automatiquement les machines virtuelles VMware** | Vous devez disposer d’au moins un utilisateur en lecture seule | Objet de centre de données -> propager tooChild objet rôle = lecture seule | Utilisateur affecté au niveau du centre de données et a accès tooall hello objets dans le centre de données hello.<br/><br/> accès toorestrict, affecter hello **aucun accès** rôle avec hello **propager toochild** objet, telles que les objets enfants toohello (hôtes de vSphere, magasins de données, machines virtuelles et réseaux).|
|**Type de basculement** | Vous devez disposer d’au moins un utilisateur en lecture seule | Objet de centre de données -> propager tooChild objet rôle = lecture seule | Utilisateur affecté au niveau du centre de données et a accès tooall hello objets dans le centre de données hello.<br/><br/> accès toorestrict, affecter hello **aucun accès** rôle avec hello **propager toochild** toohello (hôtes de vSphere, magasins de données, machines virtuelles et réseaux) des objets enfants de l’objet.<br/><br/> Utile à des fins de migration, mais pas pour la réplication complète, le basculement et la restauration automatique.|
|**Basculement et restauration automatique** | Nous vous suggérons de vous créez un rôle (AzureSiteRecoveryRole) avec les autorisations hello requis, puis affectez hello rôle tooa VMware utilisateur ou un groupe | Objet de centre de données -> propager tooChild objet rôle = AzureSiteRecoveryRole<br/><br/> Banque de données -> Allouer de l’espace, parcourir la banque de données, opérations de fichier de bas niveau, supprimer le fichier, mettre à jour les fichiers de machine virtuelle<br/><br/> Réseau -> Attribution de réseau<br/><br/> Ressource -> pool tooresource d’affecter un ordinateur virtuel, migrez la machine virtuelle hors tension, migrer sous tension sur la machine virtuelle<br/><br/> Tâches -> Créer une tâche, Mettre à jour une tâche<br/><br/> Machine virtuelle -> Configuration<br/><br/> Machine virtuelle -> Interagir -> répondre à la question, connexion d’appareil, configurer un support de CD, configurer une disquette, mettre hors tension, mettre sous tension, installation des outils VMware<br/><br/> Machine virtuelle -> Stock -> Créer, inscrire, désinscrire<br/><br/> Machine virtuelle -> Approvisionnement -> Autoriser le téléchargement de machines virtuelles, autoriser le chargement de fichiers de machine virtuelle<br/><br/> Machine virtuelle -> Instantanés -> Supprimer les instantanés | Utilisateur affecté au niveau du centre de données et a accès tooall hello objets dans le centre de données hello.<br/><br/> accès toorestrict, affecter hello **aucun accès** rôle avec hello **propager toochild** objet, telles que les objets enfants toohello (hôtes de vSphere, magasins de données, machines virtuelles et réseaux).|

## <a name="create-an-account-tooconnect-toovmware-vcenter-server-vmware-vsphere-exsi-host"></a>Créer un serveur compte tooconnect tooVMware vCenter / VMware vSphere EXSi hôte
1. Connexion en hello Configuration serveur et lancer hello cspsconfigtool.exe à l’aide du raccourci hello hello bureau.
2. Cliquez sur **ajouter un compte** sur hello **gérer le compte** onglet.

  ![add-account](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Détails du compte hello et cliquez sur OK tooadd hello compte. Hello compte doit pouvoir hello répertoriés dans hello [préparer un compte pour la découverte automatique](#prepare-an-account-for-automatic-discovery) section.

  >[!NOTE]
  Il prend environ 15 minutes pour toobe d’informations de compte hello synchronisation permanente avec le service de récupération de Site hello.


## <a name="associate-a-vmware-vcenter-vmware-vsphere-esx-host-add-vcenter"></a>Associer un serveur VMware vCenter/hôte VMware vSphere ESX (ajouter vCenter)
* On hello portail Azure, accédez trop*YourRecoveryServicesVault* > **Infrastructure Site Recovery** > **serveurs de Configuration**  >  *ConfigurationServer*
* Dans la page des détails du serveur de Configuration hello, cliquez sur Bonjour + vCenter bouton.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

## <a name="modify-credentials-used-tooconnect-toohello-vcenter-server-vsphere-esxi-host"></a>Modifier les informations d’identification utilisées tooconnect toohello vCenter server / vSphere ESXi hôte

1. Connexion en hello Configuration serveur et lancer hello cspsconfigtool.exe
2. Cliquez sur **ajouter un compte** sur hello **gérer le compte** onglet.

  ![add-account](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Fournir les informations du nouveau compte hello et cliquez sur OK tooadd hello compte. Hello compte doit pouvoir hello répertoriés dans hello [préparer un compte pour la découverte automatique](#prepare-an-account-for-automatic-discovery) section.
4. On hello portail Azure, accédez trop*YourRecoveryServicesVault* > **Infrastructure Site Recovery** > **serveurs de Configuration**  >  *ConfigurationServer*
5. Dans la page des détails du serveur de Configuration hello, cliquez sur hello **actualisation du serveur** bouton.
6. Une fois la tâche de serveur hello actualisation est terminée, sélectionnez hello vCenter Server tooopen hello vCenter page Résumé.
7. Sélectionnez hello récemment ajouté de compte Bonjour **compte de l’hôte serveur/vSphere vCenter** champ et cliquez sur hello **enregistrer** bouton.

  ![modify-account](./media/site-recovery-vmware-to-azure-manage-vcenter/modify-vcente-creds.png)

## <a name="delete-a-vcenter-in-azure-site-recovery"></a>Supprimer un serveur vCenter dans Azure Site Recovery
1. On hello portail Azure, accédez trop*YourRecoveryServicesVault* > **Infrastructure Site Recovery** > **serveurs de Configuration**  >  *ConfigurationServer*
2. Dans la page des détails du serveur de Configuration hello sélectionnez hello vCenter Server tooopen hello vCenter page Résumé.
3. Cliquez sur hello **supprimer** bouton toodelete hello vCenter

  ![delete-account](./media/site-recovery-vmware-to-azure-manage-vcenter/delete-vcenter.png)

> [!NOTE]
Si vous avez besoin de toomodify hello vCenter IP adresse/nom de domaine complet, détails du Port, vous devez toodelete hello du serveur vCenter et ajoutez à nouveau.
