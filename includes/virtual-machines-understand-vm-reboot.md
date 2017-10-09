Machines virtuelles (VM) Azure peut parfois redémarrage sans raison apparente, sans preuve de votre ayant initialisé l’opération de redémarrage hello. Cet article répertorie les actions de hello et les événements qui peuvent entraîner des machines virtuelles tooreboot et fournissent un aperçu de comment tooavoid inattendue redémarrer des problèmes ou de réduire l’impact de hello de tels problèmes.

## <a name="configure-hello-vms-for-high-availability"></a>Configurer des machines virtuelles de hello pour la haute disponibilité
Hello meilleure manière tooprotect une application qui s’exécute sur Azure par rapport à la machine virtuelle redémarre et le temps mort tooconfigure hello machines virtuelles pour la haute disponibilité.

tooprovide ce niveau de l’application tooyour de redondance, nous vous recommandons de groupe deux ou plusieurs des ordinateurs virtuels dans un ensemble de disponibilité. Cette configuration garantit que, pendant un événement de maintenance planifiée ou non, au moins une machine virtuelle est disponible et répond aux hello 99,95 % [contrat SLA Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_5/).

Pour plus d’informations sur les groupes à haute disponibilité, consultez hello suivant des articles :

- [Gérer la disponibilité hello de machines virtuelles](../articles/virtual-machines/windows/manage-availability.md)
- [Configurer la disponibilité des machines virtuelles](../articles/virtual-machines/windows/classic/configure-availability.md)

## <a name="resource-health-information"></a>Informations sur Resource Health 
L’intégrité des ressources Azure est un service qui expose l’intégrité des ressources Azure hello et fournit des instructions pour résoudre des problèmes. Dans un environnement de cloud où il n’est pas possible toodirectly des serveurs d’accès ou les éléments d’infrastructure, hello l’intégrité des ressources vise temps hello tooreduce consacré à la résolution des problèmes. En particulier, hello vise tooreduce hello temps que la détermination de si racine hello de problème de hello trouve dans une application hello ou un événement à l’intérieur de hello plateforme Azure. Pour plus d’informations, consultez la section [Understand and use Resource Health](../articles/resource-health/resource-health-overview.md) (Comprendre et utiliser Resource Health).

## <a name="actions-and-events-that-can-cause-hello-vm-tooreboot"></a>Actions et les événements qui peuvent provoquer hello tooreboot de machine virtuelle

### <a name="planned-maintenance"></a>Maintenance planifiée
Microsoft Azure effectue périodiquement des mises à jour sur la sécurité de l’infrastructure hôte hello sous-jacente aux machines virtuelles, les performances et la fiabilité de hello globe tooimprove hello. Nombre de ces mises à jour sont exécutées sans impact sur les machines virtuelles ou les services cloud, y compris les mises à jour de préservation de la mémoire.

Toutefois, certaines mises à jour nécessitent un redémarrage. Dans ce cas, hello machines virtuelles sont arrêtées pendant que nous correctif infrastructure de hello et ensuite les machines virtuelles de hello sont redémarrées.

toounderstand les maintenances Azure est et comment il peut affecter la disponibilité de hello de vos ordinateurs virtuels Linux, voir les articles de hello répertoriées ici. les articles de Hello fournissent des informations sur les processus de maintenance planifiée par Azure hello et comment tooschedule planifiées maintenance toofurther réduisent l’impact de hello.

- [Maintenance planifiée des machines virtuelles dans Azure](../articles/virtual-machines/windows/planned-maintenance.md)
- [Comment tooschedule les maintenances planifiées sur des machines virtuelles Azure](../articles/virtual-machines/windows/classic/planned-maintenance-schedule.md)

### <a name="memory-preserving-updates"></a>Mises à jour de préservation de la mémoire   
Pour cette classe de mises à jour dans Microsoft Azure, les utilisateurs ne constatent aucun impact sur leurs machines virtuelles en cours d’exécution. La plupart de ces mises à jour sont toocomponents ou des services qui peuvent être mis à jour sans interférer avec hello instance en cours d’exécution. Certaines sont mises à jour de plateforme infrastructure sur le système d’exploitation hôte hello peuvent être appliquées sans avoir à redémarrer hello machines virtuelles.

Ces mises à jour de préservation de la mémoire sont réalisées avec la technologie qui permet la migration en direct. Lorsqu’il est mis à jour, hello VM est placé dans un *suspendu* état. Cet état conserve la mémoire hello dans la mémoire RAM tandis que le système d’exploitation hôte sous-jacent de hello reçoit des correctifs et mises à jour nécessaires de hello. Hello machine virtuelle est repris dans les 30 secondes en pause. Après avoir hello reprise de la machine virtuelle, son horloge est automatiquement synchronisé.

En raison de la période de courte pause hello, déploiement des mises à jour via ce mécanisme considérablement réduit l’impact de hello sur hello machines virtuelles. Toutefois, toutes les mises à jour ne peuvent être déployées de cette manière. 

Les mises à jour multi-instances (pour les machines virtuelles d’un groupe à haute disponibilité) se voient appliquer un seul domaine de mise à jour à la fois.

> [!NOTE]
> Les machines Linux dotées de versions anciennes de noyau sont affectées par une alerte sur le noyau au cours de cette méthode de mise à jour. tooavoid ce problème, la mise à jour tookernel version 3.10.0-327.10.1 ou version ultérieure. Pour plus d’informations, consultez [Une machine virtuelle Linux Azure sur un noyau 3.10 panique après une mise à niveau du nœud hôte](https://support.microsoft.com/help/3212236).     
    
### <a name="user-initiated-reboot-or-shutdown-actions"></a>Actions d’arrêt ou de redémarrage initiées par l’utilisateur
 
Si vous effectuez un redémarrage à partir de hello portail Azure, Azure PowerShell, une interface de ligne ou réinitialiser l’API, vous pouvez trouver des événements de hello Bonjour [journal des activités Azure](../articles/monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

Si vous effectuez l’action de hello système du hello machine virtuelle d’exploitation, vous trouverez les événements hello dans les journaux système hello.

D’autres scénarios qui entraînent généralement hello VM tooreboot sont plusieurs actions de modification de la configuration. Vous voyez normalement un message d’avertissement indiquant que l’exécution d’une action particulière entraîne un redémarrage de hello machine virtuelle. Des exemples des opérations de redimensionnement de machine virtuelle, modification hello de mot de passe du compte d’administration de hello et la définition d’une adresse IP statique.

### <a name="azure-security-center-and-windows-update"></a>Azure Security Center et Windows Update
Azure Security Center recherche quotidiennement les mises à jour manquantes du système d’exploitation sur les machines virtuelles Windows et Linux. Security Center récupère une liste des mises à jour de sécurité et critiques disponibles dans Windows Update ou WSUS (Windows Server Update Services), selon le service configuré sur les machines virtuelles Windows. Centre de sécurité vérifie également les mises à jour plus récentes de hello pour les systèmes Linux. S’il manque une mise à jour système sur votre machine virtuelle, Security Center vous recommande de l’appliquer. application Hello de ces mises à jour du système est contrôlée via hello centre de sécurité Bonjour portail Azure. L’application de certaines mises à jour peut nécessiter un redémarrage des machines virtuelles. Pour en savoir plus, consultez [Appliquer les mises à jour système dans Azure Security Center](../articles/security-center/security-center-apply-system-updates.md).

Comme les serveurs locaux, Azure n’enverra pas mises à jour à partir de Windows Update tooWindows machines virtuelles Azure, étant donné que ces ordinateurs sont prévu toobe géré par leurs utilisateurs. Toutefois, vous êtes encouragé tooleave paramètre de mise à jour Windows automatique hello activé. L’installation automatique des mises à jour à partir de Windows Update peut également entraîner des redémarrages toooccur après l’application des mises à jour hello. Pour plus d’informations, consultez [Windows Update : Forum Aux Questions](https://support.microsoft.com/help/12373/windows-update-faq).

### <a name="other-situations-affecting-hello-availability-of-your-vm"></a>Autres situations affecter la disponibilité de hello de votre machine virtuelle
Il existe des autres cas dans lequel Azure peut activement suspendre hello utilisation d’une machine virtuelle. Vous recevez les notifications par courrier électronique avant d’effectuer cette action, donc vous avez une chance tooresolve hello problèmes sous-jacents. Les violations de sécurité et l’expiration de hello de modes de paiement sont des exemples de problèmes qui affectent la disponibilité de la machine virtuelle.

### <a name="host-server-faults"></a>Erreurs du serveur hôte 
Hello machine virtuelle est hébergée sur un serveur physique qui est en cours d’exécution à l’intérieur d’un centre de données Azure. exécutions du serveur physique Hello un agent appelée hello Agent hôte dans Ajout tooa quelques autres composants Azure. Lorsque ces composants logiciels Azure sur le serveur physique de hello ne répondent plus, système de surveillance de hello déclenche un redémarrage hello hôte tooattempt de récupération du serveur. Hello machine virtuelle est généralement disponible dans les cinq minutes et continue toolive sur hello le même hôte que précédemment.

Erreurs de serveur sont généralement provoquées par une défaillance matérielle, par exemple défaillance hello d’un disque dur ou un disque SSD. Azure en permanence surveille ces occurrences, identifie les bogues hello et déploie les mises à jour après que l’atténuation de hello a été implémentée et testée.

Certaines erreurs de serveur hôte pouvant être toothat spécifique server, une situation de redémarrage de machine virtuelle répétée peut améliorer les redéployer manuellement les hello machine virtuelle tooanother hôte serveur. Cette opération peut être déclenchée à l’aide de hello **redéployer** proposée sur la page de détails hello Hello machine virtuelle, ou en arrêtant et redémarrant hello VM Bonjour portail Azure.

### <a name="auto-recovery"></a>Récupération automatique
Si le serveur hôte de hello ne peut pas redémarrer pour une raison quelconque, hello plateforme Azure lance un serveur hôte défectueux récupération automatique action tootake hello, la rotation pour un examen approfondi. 

Tous les ordinateurs virtuels sur cet hôte sont serveur hôte différent, sain de tooa automatiquement déplacé. Ce processus est généralement terminé dans les 15 minutes. toolearn en savoir plus sur le processus de récupération automatique hello, consultez [Auto-récupération des machines virtuelles](https://azure.microsoft.com/blog/service-healing-auto-recovery-of-virtual-machines).

### <a name="unplanned-maintenance"></a>Maintenance non planifiée
Dans de rares occasions, hello équipe Azure peut devez tooperform maintenance activités tooensure hello l’intégrité globale de hello plateforme Azure. Ce comportement peut affecter la disponibilité de la machine virtuelle, et il se produit généralement lorsque Bonjour même action de récupération automatique comme décrit précédemment.  

Non planifiés maintenances hello suivants :

- Défragmentation urgente de nœud
- Mises à jour du commutateur réseau urgente

### <a name="vm-crashes"></a>Incidents de machine virtuelle
Machines virtuelles peuvent redémarrer en raison de problèmes au sein de la machine virtuelle proprement dite de hello. charge de travail Hello ou un rôle qui s’exécute sur hello machine virtuelle peut déclencher une vérification de bogue hello système d’exploitation invité. Pour une aide pour déterminer la raison de hello de panne de hello, afficher les journaux système et application hello pour les machines virtuelles Windows et hello journaux série pour les machines virtuelles Linux.

### <a name="storage-related-forced-shutdowns"></a>Arrêt forcés relatifs au stockage
Machines virtuelles dans Azure reposent sur des disques virtuels pour le système d’exploitation et de stockage de données qui est hébergé sur l’infrastructure de stockage Azure hello. Chaque fois que la connectivité entre hello machine virtuelle et les disques virtuels hello associé ou disponibilité de hello est affectée pendant plus de 120 secondes, hello plateforme Azure effectue un arrêt forcé de hello tooavoid corruption des données dans les machines virtuelles. machines virtuelles de Hello sont sous tension automatiquement en une fois la connectivité de stockage a été restaurée. 

Durée Hello d’arrêt de hello peut être aussi courte que cinq minutes, mais peut être beaucoup plus longue. Hello Voici un des cas spécifiques hello associé liés au stockage des arrêts forcés : 

**Dépassement des limites d’E/S**

Machines virtuelles peuvent être temporairement arrêtés lorsque les demandes d’e/s sont constamment limitées parce que hello du volume des opérations d’e/s par seconde (IOPS) dépasse les limites de hello d’e/s de disque de hello. (Stockage sur disque standard est limité too500 IOPS.) toomitigate ce problème, utilisez l’agrégation de disques ou configurer l’espace de stockage hello invité hello machine virtuelle, en fonction de la charge de travail hello. Pour en savoir plus, consultez [Configuration de machines virtuelles Azure pour des performances de stockage optimales](http://blogs.msdn.com/b/mast/archive/2014/10/14/configuring-azure-virtual-machines-for-optimal-storage-performance.aspx).

Limites d’e/s plus importantes sont disponibles via le stockage Azure Premium avec des too80, 000 IOPS. Pour plus d’informations, consultez [Stockage Premium hautes performances](../articles/storage/common/storage-premium-storage.md).

### <a name="other-incidents"></a>Autres incidents
Dans de rares circonstances, un problème étendu peut affecter plusieurs serveurs dans un centre de données Azure. Si ce problème se produit, hello équipe Azure envoie des abonnements toohello affectée de notifications par courrier électronique. Vous pouvez vérifier hello [tableau de bord de l’intégrité du Service Azure](https://azure.microsoft.com/status/) et hello portail Azure pour l’état hello de pannes en cours et incidents passés.
