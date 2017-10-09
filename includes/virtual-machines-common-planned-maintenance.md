Azure effectue périodiquement des mises à jour tooimprove hello fiabilité, les performances et sécurité de l’infrastructure d’hôte hello pour les ordinateurs virtuels. Ces mises à jour de plage à partir de la mise à jour corrective de composants logiciels Bonjour hébergeant l’environnement (par exemple, le système d’exploitation, hyperviseur et divers agents déployés sur l’ordinateur hôte de hello), la mise à niveau des composants réseau, toohardware mise hors service. majorité Hello de ces mises à jour sont effectuées sans toutes toohello hébergé impact sur les machines virtuelles. Cependant, il existe des cas où les mises à jour ont un impact :

- Si la maintenance de hello ne nécessite pas de redémarrage, Azure utilise hello toopause de migration sur place machine virtuelle lors de l’hôte de hello est mise à jour.

- Si la maintenance requiert un redémarrage, vous obtenez un avis lors de la planification de maintenance de hello. Dans ce cas, vous allez également recevoir une fenêtre de temps où vous pouvez commencer la maintenance de hello vous-même, à un moment qui vous convient.

Cette page décrit comment Microsoft Azure exécute les deux types de maintenance. Pour plus d’informations sur les événements non planifiés (interruptions), consultez disponibilité hello de gérer des machines virtuelles pour [Windows] (.. / articles/virtual-machines/windows/manage-availability.md) ou [Linux](../articles/virtual-machines/linux/manage-availability.md).

Hello d’applications s’exécutant sur une machine virtuelle peut collectent des informations sur les mises à jour à venir à l’aide de Service de métadonnées Azure pour [Windows](../articles/virtual-machines/windows/instance-metadata-service.md) ou [Linux] (.. / articles/virtual-machines/linux/instance-metadata-service.md).

## <a name="in-place-vm-migration"></a>Migration sur place d’une machine virtuelle

Lorsque les mises à jour ne nécessitent pas un redémarrage complet, une migration dynamique sur place est utilisée. Au cours de la mise à jour hello hello virtual machine est suspendue pendant environ 30 secondes, en conservant mémoire hello dans la mémoire RAM, tandis que hello environnement d’hébergement applique les correctifs et mises à jour nécessaires de hello. Hello ordinateur virtuel est ensuite redémarré et que l’horloge de l’ordinateur virtuel de hello hello est automatiquement synchronisé.

Pour les machines virtuelles dans des groupes à haute disponibilité, les domaines de mise à jour sont mis à jour un par un. Tous les ordinateurs virtuels dans un domaine de mise à jour (ID) sont en pause, mis à jour et puis redémarrés avant la maintenance planifiée se déplace sur toohello UD suivant.

Certaines applications peuvent être affectées par ces types de mises à jour. Les applications qui effectuent le traitement, comme la diffusion multimédia en continu ou le transcodage ou un débit élevé, les scénarios de mise en réseau des événements en temps réel ne peuvent pas être conçue tootolerate une pause deuxième 30. <!-- sooooo, what should they do? --> 


## <a name="maintenance-requiring-a-reboot"></a>Maintenance nécessitant un redémarrage

Quand les machines virtuelles doivent toobe redémarré pour la maintenance planifiée, vous êtes averti à l’avance. Maintenance planifiée comprend deux phases : hello libre-service de fenêtre et une fenêtre de maintenance planifiée.

Hello **libre-service de fenêtre** vous permet de déclencher une maintenance hello sur vos machines virtuelles. Pendant ce temps, vous pouvez interroger chaque toosee VM leur état et vérifier le résultat de hello de votre dernière demande de maintenance.

Lorsque vous démarrez libre-service de maintenance, votre machine virtuelle est nœud déplacé tooa qui a déjà été mis à jour et donne sur toute sa puissance. Étant donné que hello machine virtuelle a redémarré, disque temporaire de hello est perdu et les adresses IP dynamiques associés à interface réseau virtuelle sont mis à jour.

Si vous démarrez libre-service de maintenance et il existe une erreur pendant le processus de hello, hello opération est arrêtée, hello VM n’est pas mis à jour et il est également supprimé à partir de l’itération de maintenance hello planifié. Vous être contacté en une date ultérieure, avec une planification et proposé une nouvelle opportunité toodo libre-service de maintenance. 

Lors de la fenêtre de libre-service hello est passée, hello **fenêtre de maintenance planifiée** commence. Pendant cette période, vous pouvez tout de même interroger hello fenêtre de maintenance, mais n’est plus maintenance de hello toostart en mesure de vous-même.

## <a name="availability-considerations-during-planned-maintenance"></a>Considérations relatives à la disponibilité lors de la maintenance planifiée 

Si vous décidez toowait jusqu'à ce que hello planifié la fenêtre de maintenance, il existe quelques tooconsider choses pour maintenir la disponibilité le plus élevée de hello de vos machines virtuelles. 

### <a name="paired-regions"></a>Régions jumelées

Chaque région Azure est associée à une autre région de hello même geography, ensemble, ils apporter une paire régionale. Pendant les maintenances, Azure met à jour uniquement des machines virtuelles dans une région d’une paire de région de hello. Par exemple, lors de la mise à jour hello ordinateurs virtuels de l’Amérique du Nord, Azure ne mettra pas à jour les Machines virtuelles dans l’Amérique du Sud à hello même temps. Toutefois, autres régions comme Europe du Nord peut être en cours de maintenance à hello même temps que les États-Unis. Comprendre le fonctionnement des paires régionales peut vous aider à mieux répartir vos machines virtuelles entre les régions. Pour en savoir plus, consultez [Paires régionales Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="availability-sets-and-scale-sets"></a>Groupes à haute disponibilité et groupes identiques

Lors du déploiement d’une charge de travail sur des machines virtuelles Azure, vous pouvez créer des machines virtuelles de hello dans une application de tooyour disponibilité ensemble tooprovide haute disponibilité. Ceci vous garantit qu’au moins une des machines virtuelles sera disponible pendant une panne ou un événement de maintenance.

Au sein d’un ensemble de disponibilité, des ordinateurs virtuels individuels sont réparties sur les domaines de mise à jour too20 (domaines d’erreur). Lors de la maintenance planifiée, un seul domaine de mise à jour est affecté à un moment donné. N’oubliez pas que commande hello de domaines de mise à jour un impact sur ne pas nécessairement se produit séquentiellement. 

Machines virtuelles identiques sont une ressource de calcul Azure qui vous permet de toodeploy et gérer un ensemble de machines virtuelles identiques en tant qu’une seule ressource. ensemble d’échelle Hello est déployé automatiquement sur les domaines de mise à jour, telles que des machines virtuelles dans un ensemble de disponibilité. Comme pour les groupes à haute disponibilité, un seul domaine de mise à jour n’est impacté à la fois dans des groupes identiques.

Pour plus d’informations sur la configuration de vos ordinateurs virtuels pour la haute disponibilité, consultez disponibilité hello de gérer vos machines virtuelles pour Windows (.. / articles/virtual-machines/windows/manage-availability.md) ou [Linux](../articles/virtual-machines/linux/manage-availability.md).
