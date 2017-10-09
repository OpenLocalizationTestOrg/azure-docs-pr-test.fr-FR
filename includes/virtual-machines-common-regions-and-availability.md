# <a name="regions-and-availability-for-virtual-machines-in-azure"></a>Régions et disponibilité des machines virtuelles dans Azure
Azure fonctionne dans plusieurs centres de données monde hello. Ces centres de données sont regroupés dans des régions toogeographic, ce qui vous donne une grande souplesse dans le choix de l’emplacement toobuild vos applications. Il est important toounderstand comment et où vos machines virtuelles (VM) fonctionnent dans Azure, ainsi que les performances de toomaximize options, la disponibilité et la redondance. Cet article vous offre une vue d’ensemble de la disponibilité de hello et des fonctionnalités de redondance de Azure.

## <a name="what-are-azure-regions"></a>Que représentent les régions Azure ?
Vous créez des ressources Azure dans des régions géographiques définies comme « États-Unis de l'Ouest », « Europe du Nord » ou « Sud-Est asiatique ». Vous pouvez passer en revue hello [la liste des régions et leurs emplacements](https://azure.microsoft.com/regions/). Dans chaque région, plusieurs centres de données existent tooprovide pour la redondance et de disponibilité. Cette approche vous offre une grande souplesse lorsque vous concevez toomeet et les applications toocreate machines virtuelles plus proche tooyour utilisateurs tout juridique, conformité, ou que vous à des fins de taxe.

## <a name="special-azure-regions"></a>Régions Azure spéciales
Azure dispose de certaines régions spéciales que vous souhaitiez toouse lors de la création de vos applications à des fins juridiques ou de la conformité. Ces régions spéciales sont les suivantes :

* **Gouvernement des États-Unis - Virginie** et **Gouvernement des États-Unis - Iowa**
  * Instance physique et logique d’Azure isolée du réseau pour les administrations et les partenaires des États-Unis, gérée par un personnel autorisé aux États-Unis. Inclut des certifications de conformité supplémentaires comme [FedRAMP](https://www.microsoft.com/en-us/TrustCenter/Compliance/FedRAMP) et [DISA](https://www.microsoft.com/en-us/TrustCenter/Compliance/DISA). En savoir plus sur [Azure Government](https://azure.microsoft.com/features/gov/).
* **Est de la Chine** et **Nord de la Chine**
  * Ces régions sont disponibles via un unique partenariat entre Microsoft et 21Vianet, par laquelle Microsoft ne gère pas directement les centres de données hello. En savoir plus sur [Microsoft Azure en Chine](http://www.windowsazure.cn/).
* **Centre de l’Allemagne** et **Nord-Est de l’Allemagne**
  * Ces régions sont disponibles via un modèle de tiers de confiance par laquelle les données client restent en Allemagne sous contrôle de T-Systems, une société Deutsche Telekom, agissant en tant que tiers de confiance hello allemand de données.

## <a name="region-pairs"></a>Paires de régions
Chaque région Azure est associée à une autre région de hello même geography (par exemple, États-Unis, Europe ou en Asie). Cette approche permet la réplication hello de ressources, comme le stockage de la machine virtuelle, par une secteur géographique qui doit réduire la probabilité hello de catastrophes naturelles, troubles civils, pannes de courant ou les pannes de réseau physique qui affectent les deux régions à la fois. Les paires de régions offrent les avantages supplémentaires suivants :

* Dans l’événement hello d’une panne Azure plus large, une région est hiérarchisée hors chaque paire toohelp réduire toorestore de temps hello pour les applications. 
* Mises à jour Azure planifiées sont annulées des régions de toopaired un à un temps mort toominimize de temps et des risques de panne d’application.
* Tooreside dans hello des données poursuit même geography en tant que sa paire (à l’exception de Brésil Sud) à des fins de taxes et de la loi mise en œuvre juridiction.

Voici quelques exemples de paires de régions :

| Primaire | Secondaire |
|:--- |:--- |
| Ouest des États-Unis |Est des États-Unis |
| Europe du Nord |Europe de l'Ouest |
| Asie du Sud-Est |Est de l'Asie |

Vous pouvez voir hello complète [la liste des options régionales paires ici](../articles/best-practices-availability-paired-regions.md#what-are-paired-regions).

## <a name="feature-availability"></a>Disponibilité des fonctionnalités
Certains services ou fonctionnalités des machines virtuelles ne sont disponibles que dans certaines régions, par exemple des tailles de machines virtuelles ou des types de stockage spécifiques. Il existe également certains services Azure globales qui ne nécessitent pas tooselect une région particulière, tel que [Azure Active Directory](../articles/active-directory/active-directory-whatis.md), [Traffic Manager](../articles/traffic-manager/traffic-manager-overview.md), ou [Azure DNS](../articles/dns/dns-overview.md). tooassist vous lorsque vous concevez votre environnement d’application, vous pouvez vérifier hello [disponibilité des services Azure dans chaque région](https://azure.microsoft.com/regions/#services). 

## <a name="storage-availability"></a>Disponibilité du stockage
Présentation des zones géographiques différentes et des régions Azure devient important lorsque vous considérez hello options de réplication de stockage disponible. Selon le type de stockage hello, vous disposez des options de réplication différent.

**Azure Managed Disks**
* Stockage localement redondant (LRS)
  * Réplique vos données trois fois au sein d’une région de hello dans lequel vous avez créé votre compte de stockage.

**Disques basés sur un compte de stockage**
* Stockage localement redondant (LRS)
  * Réplique vos données trois fois au sein d’une région de hello dans lequel vous avez créé votre compte de stockage.
* Stockage redondant dans une zone (ZRS)
  * Réplique vos données trois fois sur deux installations toothree, dans un ou deux régions.
* Stockage géo-redondant (GRS)
  * Réplique vos données tooa région secondaire des centaines de miles en dehors de la région principale de hello.
* Stockage géo-redondant avec accès en lecture (RA-GRS)
  * Réplique votre région secondaire tooa de données, comme avec GRS, mais fournit également des données de toohello d’accès en lecture seule dans l’emplacement secondaire de hello.

Hello tableau suivant fournit une vue d’ensemble rapide des différences de hello entre les types de réplication de stockage hello :

| Stratégie de réplication | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Les données sont répliquées entre plusieurs installations. |Non |Oui |Oui |Oui |
| Données peuvent être lues à partir de l’emplacement secondaire de hello et à partir de l’emplacement principal de hello. |Non |Non |Non |Oui |
| Nombre de copies de données conservées sur des nœuds distincts. |3 |3 |6 |6 |

Vous pouvez en savoir plus sur les [options de réplication de stockage Azure ici](../articles/storage/common/storage-redundancy.md). Pour plus d’informations sur les disques gérés, consultez [Vue d’ensemble d’Azure Managed Disks](../articles/virtual-machines/windows/managed-disks-overview.md).

### <a name="storage-costs"></a>Coûts de stockage
Les prix varient selon le type de stockage hello et la disponibilité que vous sélectionnez.

**Azure Managed Disks**
* Les disques gérés Premium s’appuient sur des disques SSD et les disques gérés Standard sur des disques à rotation classique. Premium et Standard de disques gérés sont facturés en fonction de la capacité de hello configuré pour le disque de hello.

**Disques non gérés**
* Stockage Premium est soutenu par Solid-State lecteurs (SSD) et est facturé en fonction de la capacité de hello du disque de hello.
* Stockage standard est soutenu par les disques à rotation régulière et est facturé en fonction de la capacité de hello en cours d’utilisation et souhaité de disponibilité du stockage.
  * Pour RA-GRS, il existe un transfert de données de géo-réplication des frais supplémentaires pour la bande passante hello de réplication qui tooanother données région Azure.

Consultez [tarification du stockage Azure](https://azure.microsoft.com/pricing/details/storage/) pour plus d’informations sur les options de disponibilité et de hello différents types de stockage de la tarification.

## <a name="availability-sets"></a>Groupes à haute disponibilité
Un ensemble de disponibilité est un regroupement logique d’ordinateurs virtuels qui permet à Azure toounderstand comment votre application est générée tooprovide pour la redondance et de disponibilité. Il est recommandé que deux ou plusieurs ordinateurs virtuels sont créés dans un tooprovide de jeu de disponibilité pour un hello hautement disponible de l’application et toomeet [99,95 % contrat SLA Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/). Lorsqu’une seule machine virtuelle utilise [stockage Azure Premium](../articles/storage/common/storage-premium-storage.md), hello contrat SLA Azure s’applique pour les événements de maintenance non planifiés. 

Un ensemble de disponibilité est composé de deux regroupements supplémentaires qui protègent contre les défaillances matérielles et autorisent les mises à jour toosafely être appliqué - (groupes) de domaines d’erreur et mettre à jour des domaines (domaines d’erreur).

![Schéma conceptuel de hello mise à jour de domaine et erreur de configuration du domaine](./media/virtual-machines-common-regions-and-availability/ud-fd-configuration.png)

Vous pouvez en savoir plus sur comment toomanage hello disponibilité de [les machines virtuelles Linux](../articles/virtual-machines/linux/manage-availability.md) ou [les machines virtuelles Windows](../articles/virtual-machines/windows/manage-availability.md).

### <a name="fault-domains"></a>Domaines d'erreur
Un domaine d’erreur est un groupe logique de matériel sous-jacent qui partagent une même source d’alimentation et de commutateur de réseau, même rack tooa dans un centre de données local. Lorsque vous créez des machines virtuelles au sein d’un ensemble de disponibilité, hello plateforme Azure distribue automatiquement vos machines virtuelles dans ces domaines d’erreur. Cette approche limite hello impact des défaillances de matériel physique potentielles, les pannes de réseau ou coupures de courant.

### <a name="update-domains"></a>Domaines de mise à jour
Un domaine de mise à jour est un groupe logique de matériel sous-jacent qui peut subir une maintenance ou a redémarré hello même temps. Lorsque vous créez des machines virtuelles au sein d’un ensemble de disponibilité, hello plateforme Azure distribue automatiquement vos machines virtuelles entre ces domaines de mise à jour. Cette approche garantit qu’au moins une instance de votre application reste toujours en cours d’exécution comme la plateforme Azure hello subit une maintenance périodique. commande Hello de domaines de mise à jour en cours de redémarrage ne pouvez plus continuer séquentiellement pendant les maintenances, mais une mise à jour qu’un seul domaine est redémarré à la fois.

### <a name="managed-disk-fault-domains"></a>Domaines d’erreur des disques gérés
Les machines virtuelles faisant appel à des [disques gérés Azure](../articles/virtual-machines/windows/faq-for-disks.md) sont alignées sur les domaines d’erreur des disques gérés lorsqu’un groupe à haute disponibilité géré est utilisé. Cet alignement garantit que tous les hello managés disques attaché tooa machine virtuelle se trouvent dans hello même domaine d’erreur de disque géré. Seules des machines virtuelles avec des disques gérés peuvent être créées dans un groupe à haute disponibilité géré. nombre de Hello de domaines de défaillance de disque géré varie par région - deux ou trois domaines d’erreur de disque géré par région.

![Domaines d’erreur des disques gérés](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> nombre de Hello de domaines d’erreur pour la haute disponibilité managé varie selon la région - deux ou trois par région. Hello tableau suivant indique le nombre de hello par région

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez maintenant démarrer toouse ces disponibilité et redondance des fonctionnalités toobuild votre environnement Azure. Pour en savoir plus sur les meilleures pratiques, consultez la rubrique relative aux [meilleures pratiques Azure en matière de disponibilité](../articles/best-practices-availability-checklist.md).

