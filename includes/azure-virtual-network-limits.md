<a name="virtual-networking-limits-classic"></a>Les limites suivantes s’appliquent uniquement aux ressources de réseau gérées par le biais du modèle de déploiement classique par abonnement.

| Ressource | Limite par défaut | Limite maximale |
| --- | --- | --- |
| Réseaux virtuels |50 |100 |
| Sites de réseau local |20 |contacter le support technique |
| Serveurs DNS par réseau virtuel |20 |100 |
| Adresses IP privées par réseau virtuel |4096 |4096 |
| Flux TCP ou UDP simultanés par carte réseau de machine virtuelle ou instance de rôle |500K |500K |
| Groupes de sécurité réseau (NSG) |100 |200 |
| Règles de groupe de sécurité réseau par groupe de sécurité réseau |200 |400 |
| Tables d'itinéraires définis par l'utilisateur |100 |200 |
| Itinéraires définis par l'utilisateur par table d'itinéraire |100 |400 |
| Adresses IP publiques (dynamiques) |5 |contacter le support |
| Adresses IP publiques réservées |20 |contacter le support technique |
| Adresse IP virtuelle publique par déploiement |5 |contacter le support technique |
| Adresse IP virtuelle privée (ILB) par déploiement |1 |1 |
| Listes de contrôle d'accès (ACL) par point de terminaison |50 |50 |

#### <a name="azure-resource-manager-virtual-networking-limits"></a>Limites de mise en réseau – Azure Resource Manager
Les limites suivantes s’appliquent uniquement aux ressources de réseau gérées par le biais d’Azure Resource Manager par région et par abonnement.

| Ressource | Limite par défaut | Limite maximale |
| --- | --- | --- |
| Réseaux virtuels |50 |500 |
| Nombre de sous-réseaux par réseau virtuel |1 000 |contacter le support |
| Serveurs DNS par réseau virtuel |9 |25 |
| Adresses IP privées par réseau virtuel |4096 |8 192 |
| Adresses IP privées par interface réseau |50 |contacter le support technique |
| Flux TCP ou UDP simultanés par carte réseau de machine virtuelle ou instance de rôle |500K |500K |
| Interfaces réseau (NIC) |300 |10000 |
| Groupes de sécurité réseau (NSG) |100 |400 |
| Règles de groupe de sécurité réseau par groupe de sécurité réseau |200 |500 |
| Tables d'itinéraires définis par l'utilisateur |100 |200 |
| Itinéraires définis par l'utilisateur par table d'itinéraire |100 |400 |
| Adresses IP publiques (dynamiques) |60 |contacter le support technique |
| Adresses IP publiques (statiques) |20 |contacter le support technique |
| Équilibreurs de charge (accès interne et Internet) |100 |contacter le support technique |
| Règles d’équilibreur de charge par équilibreur de charge |150 |150 |
| Règles d’équilibreur de charge par configuration IP |299 |299 |
| Protocole Internet frontal public par équilibreur de charge |10 |30 |
| Protocole Internet frontal privé par équilibreur de charge |10 |contacter le support technique |
| Homologations VNet par réseau virtuel |10 |50 |
| Certificats racines point à site pour chaque passerelle VPN |20 |20 |
| Configurations IP secondaires par réseau virtuel |1 000 |contacter le support |

Pour accroître les limites par défaut, [contactez le support technique](../articles/azure-supportability/resource-manager-core-quotas-request.md ).

