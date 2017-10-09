## <a name="understand-vm-reboots---maintenance-vs-downtime"></a>Comprendre les redémarrages des machines virtuelles : maintenance et temps d’arrêt
Il existe trois scénarios pouvant conduire toovirtual machine dans Azure qui est affectée : maintenance du matériel non planifié, le temps d’arrêt inattendus et une maintenance planifiée.

* **Événement de Maintenance matérielle non planifié** se produit lorsque hello plateforme Azure prévoit ce matériel hello ou n’importe quel ordinateur plateforme composant associé tooa physique, concerne toofail. Lors de la plateforme de hello prédit une défaillance, il émet un matériel non planifié maintenance événement tooreduce hello impact toohello ordinateurs virtuels hébergés sur ce matériel. Azure utilise la Migration dynamique technologie toomigrate Bonjour Machines virtuelles de hello échouent ordinateur physique intègre tooa de matériel. Migration dynamique est une machine virtuelle en conservant opération qu’uniquement les pauses hello ordinateur virtuel pendant une courte période. Mémoire, les fichiers ouverts et les connexions réseau sont conservées, mais les performances peuvent être réduites avant et/ou après l’événement de hello. Dans les cas où la Migration dynamique ne peut pas être utilisée, hello machine virtuelle est confrontés à temps d’arrêt inattendus, comme décrit ci-dessous.


* **Un temps d’arrêt inattendu** rarement se produit lorsque le matériel de hello ou infrastructure de hello physique sous-jacent de votre machine virtuelle a généré une erreur d’une certaine façon. Cela comprend les défaillances du réseau local, du disque local ou au niveau du rack. Lorsqu’un tel échec est détecté, hello plateforme Azure migre automatiquement (heals) ordinateur physique intègre votre machine virtuelle tooa. Au cours de la procédure de réparation de hello, machines virtuelles subir de temps morts (redémarrage) et une certaine perte de cas du lecteur temporaire de hello. Hello attaché du système d’exploitation et des disques de données sont toujours conservés. 

* **Planifié des événements de Maintenance** sont mises à jour périodiques effectuées par toohello Microsoft sous-jacent tooimprove de la plateforme Azure fiabilité, les performances et sécurité de l’infrastructure de plateforme hello vos machines virtuelles s’exécutent sur. La plupart de ces mises à jour se déroulent sans aucune incidence sur les machines virtuelles ou les services cloud (voir [Maintenance de conservation des machines virtuelles](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/preserving-maintenance)). Alors que hello plateforme Azure tente toouse Maintenance de conservation de machine virtuelle dans toutes les occasions possibles, sont rares lors de ces mises à jour nécessitent un redémarrage de votre ordinateur virtuel tooapply hello mises à jour requises toohello infrastructure sous-jacente. Dans ce cas, vous pouvez effectuer Maintenance planifiée d’Azure avec l’opération de redéploiement de la Maintenance en lançant la maintenance de hello pour leurs ordinateurs virtuels dans la fenêtre de temps approprié hello. Pour plus d’informations, consultez [Maintenance planifiée pour les machines virtuelles](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/planned-maintenance/).


impact de hello tooreduce de temps mort lié tooone ou plusieurs de ces événements, nous vous recommandons de hello suivant les meilleures pratiques de haute disponibilité pour vos ordinateurs virtuels :

* [Configuration de plusieurs machines virtuelles dans un groupe à haute disponibilité pour assurer la redondance]
* [Utilisation de disques gérés pour les machines virtuelles dans le groupe à haute disponibilité]
* [Utiliser les événements planifiés tooproactively réponse tooVM ayant un impact sur les événements] (https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-scheduled-events)
* [Configuration de chaque couche application dans des groupes à haute disponibilité séparés]
* [Combinaison de l’équilibrage de charge et des groupes à haute disponibilité]

## <a name="configure-multiple-virtual-machines-in-an-availability-set-for-redundancy"></a>Configuration de plusieurs machines virtuelles dans un groupe à haute disponibilité pour assurer la redondance
application de tooyour tooprovide redondance, nous vous recommandons de groupe deux ou plusieurs machines virtuelles dans un ensemble de disponibilité. Cette configuration garantit que pendant un événement de maintenance planifiée ou non, au moins un ordinateur virtuel est disponible et répond aux hello 99,95 % contrat SLA Azure. Pour plus d’informations, consultez hello [SLA pour les Machines virtuelles](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Évitez de laisser une instance unique de machine virtuelle dans un groupe à haute disponibilité. Avec cette configuration, les machines virtuelles ne sont pas sous la garantie du SLA et connaissent des interruptions de service au cours des événements de maintenance planifiés, sauf lorsqu’une machine virtuelle unique utilise le [stockage Premium Azure](../articles/storage/common/storage-premium-storage.md). Pour les machines virtuelles uniques à l’aide du stockage premium, hello contrat SLA Azure s’applique.

Chaque ordinateur virtuel dans votre ensemble de disponibilité est attribué un **domaine de mise à jour** et un **domaine d’erreur** par hello sous-jacent de plateforme Azure. Pour un ensemble de disponibilité donné, cinq domaines de mise à jour non-configurables par l’utilisateur sont affectés par défaut (les déploiements de gestionnaire de ressources peuvent ensuite être des tooprovide accrue des domaines de mise à jour too20) tooindicate des groupes d’ordinateurs virtuels et le matériel physique sous-jacent qui peut être redémarré à hello même temps. Lorsque plus de cinq ordinateurs virtuels sont configurés dans un ensemble de disponibilité unique, les machines virtuelles sixième hello est placé dans hello même jour du domaine en tant que machine virtuelle de la première hello, hello septième Bonjour que même jour du domaine comme hello deuxième machine virtuelle et par conséquent sur. commande Hello de domaines de mise à jour en cours de redémarrage ne pouvez plus continuer séquentiellement pendant les maintenances, mais une mise à jour qu’un seul domaine est redémarré à la fois. Un domaine de mise à jour redémarré est donné toorecover de 30 minutes avant le lancée de la maintenance sur un domaine autre mise à jour.

Domaines d’erreur définissent groupe hello d’ordinateurs virtuels qui partagent un commun power source et le commutateur réseau. Par défaut, machines virtuelles de hello configurés au sein de votre jeu de disponibilité sont séparées à travers des domaines d’erreur toothree pour les déploiements de gestionnaire de ressources (deux domaines d’erreur pour classique). Alors que le placement de vos machines virtuelles dans un ensemble de disponibilité ne protège pas votre application à partir de système d’exploitation ou les erreurs spécifiques à l’application, il ne limite hello impact des défaillances de matériel physique potentielles, les pannes de réseau ou coupures de courant.

<!--Image reference-->
   ![Schéma conceptuel de hello mise à jour de domaine et erreur de configuration du domaine](./media/virtual-machines-common-manage-availability/ud-fd-configuration.png)

## <a name="use-managed-disks-for-vms-in-an-availability-set"></a>Utilisation de disques gérés pour les machines virtuelles dans le groupe à haute disponibilité
Si vous utilisez actuellement des machines virtuelles avec des disques non managées, nous recommandons vivement que vous [convertir des machines virtuelles dans le groupe à haute disponibilité des disques gérés toouse](../articles/virtual-machines/windows/convert-unmanaged-to-managed-disks.md).

[Des disques gérés par](../articles/virtual-machines/windows/managed-disks-overview.md) fournissent une meilleure fiabilité pour les groupes à haute disponibilité en veillant à ce que les disques de machines virtuelles dans un ensemble de disponibilité hello sont suffisamment isolé entre eux tooavoid des points de défaillance uniques. Cela en plaçant automatiquement les disques de hello dans des clusters de stockage différent. Si un cluster de stockage échoue en raison de l’erreur toohardware ou logicielle, seules les instances de machine virtuelle hello avec des disques sur ces marqueurs échouent.

![Domaines d’erreur des disques gérés](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> nombre de Hello de domaines d’erreur pour la haute disponibilité managé varie selon la région - deux ou trois par région. Hello tableau suivant indique le nombre de hello par région

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

Si vous envisagez de machines virtuelles de toouse avec [non managée disques](../articles/virtual-machines/windows/about-disks-and-vhds.md#types-of-disks), suivez les meilleures pratiques pour les comptes de stockage dans lequel les disques durs virtuels (VHD) d’ordinateurs virtuels sont stockés en tant que [objets BLOB de pages](https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs#about-page-blobs).

1. **Conserver tous les disques (système d’exploitation et données) sont associés à une machine virtuelle dans hello même compte de stockage**
2. **Hello de révision [limites](../articles/storage/common/storage-scalability-targets.md) nombre hello de disques non managés dans un compte de stockage** avant d’ajouter le compte de stockage de plusieurs disques durs virtuels tooa
3. **Utilisez un compte de stockage distinct pour chaque machine virtuelle d’un groupe à haute disponibilité.** Ne partagez pas les comptes de stockage avec plusieurs machines virtuelles dans hello même groupe à haute disponibilité. Il est acceptable pour les machines virtuelles sur différents comptes de stockage à haute disponibilité tooshare si au-dessus des meilleures pratiques sont respectées.

## <a name="configure-each-application-tier-into-separate-availability-sets"></a>Configuration de chaque couche application dans des groupes à haute disponibilité séparés
Si vos machines virtuelles sont tout presque identiques et servir hello même objectif de votre application, nous vous recommandons de configurer un groupe à haute disponibilité pour chaque niveau de votre application.  Si vous placez deux différents niveaux dans hello même groupe à haute disponibilité, tous les ordinateurs virtuels hello même couche application peut être redémarré à la fois. En configurant deux machines virtuelles ou plus dans un groupe à haute disponibilité par couche, vous vous assurez qu’au moins une machine de chaque couche reste disponible.

Par exemple, vous pouvez placer tous les ordinateurs virtuels hello dans les serveurs frontaux hello de votre application en cours d’exécution IIS, Apache, Nginx dans un ensemble de disponibilité unique. Assurez-vous que seuls les ordinateurs virtuels frontaux sont placées dans hello que même groupe à haute disponibilité. Assurez-vous également que seules les machines virtuelles de la couche de données sont placées dans leur propre groupe à haute disponibilité, au même titre que vos machines virtuelles répliquées SQL Server ou vos machines MySQL.

<!--Image reference-->
   ![Couches de l'application](./media/virtual-machines-common-manage-availability/application-tiers.png)

## <a name="combine-a-load-balancer-with-availability-sets"></a>Combinaison de l’équilibrage de charge et des groupes à haute disponibilité
Combiner hello [équilibrage de charge Azure](../articles/load-balancer/load-balancer-overview.md) avec une disponibilité définir tooget hello résilience la plupart des applications. Hello équilibrage de charge Azure distribue le trafic entre plusieurs machines virtuelles. Pour notre ordinateurs virtuels du niveau Standard, hello équilibrage de charge Azure est inclus. Pas de tous les niveaux d’ordinateur virtuel incluent hello équilibrage de charge Azure. Pour plus d’informations sur l’équilibrage de charge des machines virtuelles, consultez [Équilibrage de charge des machines virtuelles](../articles/virtual-machines/virtual-machines-linux-load-balance.md).

Si l’équilibrage de charge hello n’est pas configuré toobalance trafic entre plusieurs machines virtuelles, n’importe quel événement de maintenance planifiée affecte hello uniquement le trafic serveur machine virtuelle, à l’origine de la couche application tooyour panne. Placement des machines virtuelles de hello de même niveau sous hello même équilibreur de charge et disponibilité ensemble permet le trafic toobe en continu pris en charge par au moins une instance.


<!-- Link references -->
[Configuration de plusieurs machines virtuelles dans un groupe à haute disponibilité pour assurer la redondance]: #configure-multiple-virtual-machines-in-an-availability-set-for-redundancy
[Configuration de chaque couche application dans des groupes à haute disponibilité séparés]: #configure-each-application-tier-into-separate-availability-sets
[Combinaison de l’équilibrage de charge et des groupes à haute disponibilité]: #combine-a-load-balancer-with-availability-sets
[Avoid single instance virtual machines in availability sets]: #avoid-single-instance-virtual-machines-in-availability-sets
[Utilisation de disques gérés pour les machines virtuelles dans le groupe à haute disponibilité]: #use-managed-disks-for-vms-in-an-availability-set
