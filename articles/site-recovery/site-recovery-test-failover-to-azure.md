---
title: "tooAzure de basculement aaaTest en mode de récupération de Site | Documents Microsoft"
description: "En savoir plus sur l’exécution d’un test de basculement à partir de local tooAzure"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: fa0a93f409cc9f2c2c06c2d91c65971dc90c507f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="test--failover-tooazure-in-site-recovery"></a>Test de basculement tooAzure en mode de récupération de Site



Cet article fournit des informations et des instructions permettant d’effectuer un test de basculement ou d’un exercice de récupération d’urgence des ordinateurs virtuels et des serveurs physiques qui sont protégées par un Site Recovery en utilisant Azure comme site de récupération hello.

Valider des commentaires ou des questions au bas de hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Test de basculement est exécuté toovalidate votre stratégie de réplication ou effectuer un exercice de récupération d’urgence sans temps mort ni perte de données. Effectuant un test de basculement n’a aucune incidence sur la réplication en cours de hello ou sur votre environnement de production. Le test de basculement peut être effectué sur une machine virtuelle ou sur un [plan de récupération](site-recovery-create-recovery-plans.md). Lors du déclenchement d’un test de basculement, vous devez le test de toowhich toospecify hello réseau de machines virtuelles qui se connecte à. Une fois qu’un test de basculement est déclenché, vous pouvez suivre la progression dans hello **travaux** page.  


## <a name="supported-scenarios"></a>Scénarios pris en charge
Test de basculement est pris en charge dans tous les scénarios de déploiement autre que [tooAzure de site VMware hérité](site-recovery-vmware-to-azure-classic-legacy.md). Test de basculement n’est également pas prise en charge lors de la machine virtuelle a été basculée tooAzure.  


## <a name="run-a-test-failover"></a>Exécution d’un test de basculement
Cette procédure décrit comment toorun un test de basculement pour la récupération d’un plan. Vous pouvez également exécuter test de basculement pour un seul ordinateur à l’aide d’option appropriée de hello sur celui-ci.

![Test Failover](./media/site-recovery-test-failover-to-azure/TestFailover.png)


1. Sélectionnez **Plans de récupération** > *nom_planrécupération*. Cliquez sur **Test de basculement**.
1. Sélectionnez un **Point de récupération** toofailover à. Vous pouvez utiliser une des options suivantes de hello :
    1.  **Dernier traitement**: cette option bascule toutes les machines virtuelles hello plan toohello dernière récupération du point de récupération qui a déjà été traitée par le service de récupération de Site. Lorsque vous effectuez un test de basculement d’un ordinateur virtuel, la date et heure du dernier point de récupération traité hello est également affiché. Si vous effectuez le basculement d’un plan de récupération, vous pouvez atteindre l’ordinateur virtuel de tooindividual et observez **des Points de récupération la plus récente** vignette tooget ces informations. Aucun temps n’est consacré à tooprocess hello des données non traitées, cette option fournit une option de basculement faible RTO (objectif de temps de récupération).
    1.  **Dernière cohérentes au niveau application**: cette option bascule toutes les machines virtuelles hello plan toohello dernière application récupération cohérent du point de récupération qui a déjà été traitée par le service de récupération de Site. Lorsque vous effectuez un test de basculement d’un ordinateur virtuel, la date et heure du dernier point de récupération cohérents avec l’application hello est également affiché. Si vous effectuez le basculement d’un plan de récupération, vous pouvez atteindre l’ordinateur virtuel de tooindividual et observez **des Points de récupération la plus récente** vignette tooget ces informations.
    1.  **Dernière**: cette option traite tout d’abord toutes les données hello qui a été envoyé tooSite récupération service toocreate un point de récupération pour chaque ordinateur virtuel avant de les avoir basculé tooit. Cette option fournit hello plus bas RPO (Recovery Point Objective) en tant que hello virtuels créés après le basculement auront toutes les données hello qui a été répliquées tooSite le service de récupération lorsque hello basculement a été déclenchée.
    1.  **Latest multi-VM processed** (Dernier point multimachine virtuelle traité) : cette option est disponible uniquement pour les plans de récupération qui incluent au moins une machine virtuelle avec la cohérence multimachine virtuelle activée. Machines virtuelles qui font partie d’une réplication groupe basculement toohello dernière courantes multi-VM récupération cohérent du point. Autres machines virtuelles basculement tootheir dernier traité point de récupération.  
    1.  **Latest multi-VM app-consistent** (Dernier point d’application multimachine virtuelle cohérent) : cette option est disponible uniquement pour les plans de récupération qui incluent au moins une machine virtuelle avec la cohérence multimachine virtuelle activée. Machines virtuelles qui font partie d’une réplication de groupe basculement toohello commun multi-VM récupération cohérents avec les applications les plus récentes. Autres machines virtuelles basculement tootheir dernière cohérents avec les applications de points de récupération. 
    1.  **Personnalisé**: Si vous effectuez un test de basculement d’un ordinateur virtuel, vous pouvez ensuite utiliser ce point de récupération particulier option toofailover tooa.
1. Sélectionnez un **réseau virtuel Azure**: fournir un réseau virtuel Azure dans lequel les machines virtuelles de test hello serait créés. Machines virtuelles de test toocreate dans un sous-réseau portent le même nom de tentatives de récupération de site et à l’aide de hello même adresse IP que celle fournie dans **de calcul et réseau** paramètres d’ordinateur virtuel de hello. Si le sous-réseau de même nom n’est pas disponible dans hello réseau virtuel Azure fourni pour le test de basculement, puis l’ordinateur virtuel de test est créé dans le premier sous-réseau de hello par ordre alphabétique. Si la même adresse IP n’est pas disponible dans le sous-réseau de hello, l’ordinateur virtuel Obtient une autre adresse IP disponible dans le sous-réseau de hello. Pour plus d’informations, consultez [cette section](#creating-a-network-for-test-failover).
1. Si vous êtes basculement tooAzure et le chiffrement des données est activé dans **clé de chiffrement** certificat hello select qui a été émis lorsque vous avez activé le chiffrement des données pendant l’installation du fournisseur. Vous pouvez ignorer cette étape si vous n’avez pas activé le chiffrement sur l’ordinateur virtuel de hello.
1. Suivre la progression du basculement sur hello **travaux** onglet. Vous devez être machine de réplication en mesure de toosee hello test Bonjour portail Azure.
1. tooinitiate une connexion RDP sur l’ordinateur virtuel de hello, vous devez trop[ajouter une adresse ip publique](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine) sur hello interface réseau de hello a échoué sur l’ordinateur virtuel. Si vous basculez sur l’ordinateur virtuel de classique tooa, alors vous devez trop[ajouter un point de terminaison](../virtual-machines/windows/classic/setup-endpoints.md) sur le port 3389
1. Une fois que vous avez terminé, cliquez sur **basculement de test de nettoyage** sur le plan de récupération hello. Dans **Notes** enregistrer toutes les observations associées au test de basculement hello. Cette opération supprime hello virtuels qui ont été créés pendant le test de basculement.


> [!TIP]
> Machines virtuelles de test toocreate dans un sous-réseau portent le même nom de tentatives de récupération de site et à l’aide de hello même adresse IP que celle fournie dans **de calcul et réseau** paramètres d’ordinateur virtuel de hello. Si le sous-réseau de même nom n’est pas disponible dans hello réseau virtuel Azure fourni pour le test de basculement, puis l’ordinateur virtuel de test est créé dans le premier sous-réseau de hello par ordre alphabétique. Si hello cible IP fait partie de hello choisi sous-réseau, récupération de site tente de machine virtuelle toocreate hello test de basculement à l’aide de hello cible IP. Si hello cible IP ne fait pas partie de hello choisi sous-réseau ordinateur virtuel de test de basculement est créé à l’aide d’une adresse IP disponible dans hello choisi de sous-réseau.
>
>

## <a name="test-failover-job"></a>Tâche du test de basculement

![Test Failover](./media/site-recovery-test-failover-to-azure/TestFailoverJob.png)

Le déclenchement d’un test basculement implique les étapes suivantes :

1. Vérification des conditions requises : cette étape s’assure que toutes les conditions requises pour le basculement sont satisfaites.
1. Basculement : Cette étape traite les données de hello et rend prêt afin qu’une machine virtuelle Azure peut être créée à partir d’elle. Si vous avez choisi **dernière** point de récupération, cette étape crée un point de récupération à partir des données hello qui a été envoyées toohello service.
1. Démarrer : Cette étape crée une machine virtuelle Azure à l’aide de données de hello traitées à l’étape précédente de hello.

## <a name="time-taken-for-failover"></a>Durée du basculement

Dans certains cas, le basculement d’ordinateurs virtuels nécessite une étape supplémentaire intermédiaire qui prend généralement environ 8 toocomplete de minutes too10. Il s’agit des cas suivants :

* Ordinateurs virtuels VMware utilisant une version de hello service mobilité antérieurs à 9.8
* Serveurs physiques
* Machines virtuelles VMware Linux
* Machines virtuelles Hyper-V protégées en tant que serveurs physiques
* Machines virtuelles où les pilotes suivants ne sont pas présents en tant que pilotes de démarrage
    * storvsc
    * vmbus
    * storflt
    * intelide
    * atapi
* Machines virtuelles VMware qui n’ont pas de service DHCP activé, que vous utilisiez des adresses IP statiques ou DHCP

Bonjour tous les autres cas cette étape intermédiaire n’est pas obligatoire et durée hello pour le basculement hello est nettement plus faible.


## <a name="creating-a-network-for-test-failover"></a>Création d’un réseau pour le test de basculement
Il est recommandé que lorsque vous effectuez un test de basculement vous choisissez un réseau isolé de votre réseau de site de récupération de production que vous avez fourni dans **de calcul et réseau** paramètres de machine virtuelle de hello. Lorsque vous créez un réseau virtuel Azure, celui-ci est par défaut isolé des autres réseaux. Ce réseau doit reproduire votre réseau de production :

1. Réseau de test doit avoir le même nombre de sous-réseaux que celle de votre réseau de production et avec le même nom que celles de sous-réseaux hello dans votre réseau de production de hello.
1. Réseau de test doit utiliser hello même plage IP que celle de votre réseau de production.
1. Hello de mise à jour DNS de hello réseau de Test comme hello IP que vous avez donné en tant que cible IP pour l’ordinateur de virtuel hello DNS sous **de calcul et réseau** paramètres. Consultez la rubrique [Considérations en matière de test de basculement](site-recovery-active-directory.md#test-failover-considerations) pour plus de détails.


## <a name="test-failover-tooa-production-network-on-recovery-site"></a>Réseau de production de tooa de basculement de test sur le site de récupération
Il est recommandé que lorsque vous effectuez un test de basculement vous choisissez un réseau qui est différent de votre réseau de site de récupération de production que vous avez fourni dans **de calcul et réseau** paramètres de machine virtuelle de hello. Mais si vous voulez vraiment la connectivité de réseau tooend toovalidate fin dans un échec sur l’ordinateur virtuel, notez hello les points suivants :

1. Vérifiez que hello l’ordinateur virtuel principal est arrêtée lorsque vous effectuez un test de basculement hello. Si vous ne le faites pas, il y aura deux machines virtuelles avec hello même identité en cours d’exécution dans hello du même réseau à hello simultanément et qui peut entraîner des conséquences tooundesired.
1. Les modifications que vous apportez sur des machines virtuelles de hello test de basculement sont perdues lorsque vous les machines virtuelles de nettoyage hello test de basculement. Ces modifications ne seront pas répliquées toohello précédent l’ordinateur virtuel principal.
1. Cette méthode de tests conduit tooa les temps d’arrêt de votre application de production. Les utilisateurs de l’application hello doivent être posées toonot utiliser hello application lors de la récupération d’urgence de hello permet d’accéder est en cours d’exécution.  



## <a name="prepare-active-directory-and-dns"></a>Préparer Active Directory et DNS
toorun un test de basculement pour tester l’application, vous avez besoin une copie de l’environnement Active Directory de production hello dans votre environnement de test. Consultez la rubrique [Considérations en matière de test de basculement](site-recovery-active-directory.md#test-failover-considerations) pour plus de détails.

## <a name="prepare-tooconnect-tooazure-vms-after-failover"></a>Préparer des ordinateurs virtuels de tooAzure tooconnect après le basculement

Si vous souhaitez tooconnect tooAzure machines virtuelles à l’aide du protocole RDP après le basculement, assurez-vous que vous hello actions résumées dans le tableau de hello.

**Type de basculement** | **Emplacement** | **Actions**
--- | --- | ---
**Machine virtuelle Azure exécutant Windows** | Sur la machine locale, avant le basculement | tooaccess hello Azure VM sur hello internet, activer RDP, assurez-vous que TCP et les règles UDP sont ajoutées pour hello **Public**, et que RDP n’est autorisée dans **pare-feu Windows** > **autorisé Applications**, pour tous les profils.<br/><br/> activer RDP sur l’ordinateur de hello tooaccess via une connexion site à site et s’assurer que RDP est autorisé dans hello **pare-feu Windows** -> **autorisée des applications et fonctionnalités** pour  **Domaine et privés** réseaux.<br/><br/>  Assurez-vous que la stratégie de réseau SAN du système d’exploitation de hello est définie trop**OnlineAll**. [En savoir plus](https://support.microsoft.com/kb/3031135).<br/><br/> Assurez-vous qu’il n’y a aucune mise à jour de Windows en attente sur l’ordinateur virtuel de hello lorsque vous déclenchez un basculement. Mise à jour de Windows peut démarrer lorsque vous basculement et si vous ne serez pas en mesure de toologin toohello virtual machine jusqu'à la fin de la mise à jour de hello. <br/><br/>
**Machine virtuelle Azure exécutant Windows** | Sur la machine virtuelle Azure après le basculement | Pour un ordinateur virtuel classique, [ajouter un point de terminaison public](../virtual-machines/windows/classic/setup-endpoints.md) pourquoi le protocole RDP (port 3389)<br/><br/>  Pour une machine virtuelle Resource Manager, [ajoutez une adresse IP publique](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine).<br/><br/> Hello des règles de groupe de sécurité réseau sur hello a échoué sur une machine virtuelle, et le port tooallow entrant connexions toohello RDP doivent hello toowhich sous-réseau Azure qu’il est connecté.<br/><br/> Pour un ordinateur virtuel du Gestionnaire de ressources, vous pouvez vérifier **diagnostics de démarrage** toolook à une capture d’écran de l’ordinateur virtuel de hello<br/><br/> Si vous ne pouvez pas vous connecter, vérifiez que hello machine virtuelle est en cours d’exécution, puis consultez ces [des conseils de dépannage](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).<br/><br/>
**Machine virtuelle Azure exécutant Linux** | Sur la machine locale, avant le basculement | Vérifier que service Secure Shell sur hello Azure VM hello toostart automatiquement au démarrage du système.<br/><br/> Vérifiez que les règles de pare-feu autorisent un tooit de connexion SSH.
**Machine virtuelle Azure exécutant Linux** | Machine virtuelle Azure après le basculement | Hello des règles de groupe de sécurité réseau sur hello a échoué sur une machine virtuelle, et le port tooallow entrant connexions toohello SSH doivent hello toowhich sous-réseau Azure qu’il est connecté.<br/><br/> Pour un ordinateur virtuel classique, [ajouter un point de terminaison public](../virtual-machines/windows/classic/setup-endpoints.md) doit être créé, tooallow des connexions entrantes sur le port SSH (port TCP 22 par défaut) de hello.<br/><br/> Pour une machine virtuelle Resource Manager, [ajoutez une adresse IP publique](site-recovery-monitoring-and-troubleshooting.md#adding-a-public-ip-on-a-resource-manager-virtual-machine).<br/><br/> Pour un ordinateur virtuel du Gestionnaire de ressources, vous pouvez vérifier **diagnostics de démarrage** toolook à une capture d’écran de l’ordinateur virtuel de hello<br/><br/>



## <a name="next-steps"></a>Étapes suivantes
Une fois que votre tentative de test de basculement a réussi, vous pouvez essayer d’effectuer un [basculement](site-recovery-failover.md).
