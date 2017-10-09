# <a name="platform-supported-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources
Dans cet article, nous décrivons comment nous autorisons migration de l’infrastructure en tant qu’une ressource de service (IaaS) à partir de modèles de déploiement hello classique tooResource Manager. Pour en savoir plus, voir [Fonctionnalités et avantages d’Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md). Nous avons décrit en détail tooconnect ressources hello deux modèles de déploiement qui coexistent dans votre abonnement à l’aide de virtual réseau passerelles de site à site.

## <a name="goal-for-migration"></a>Objectif de la migration
Resource Manager autorise le déploiement d’applications complexes à l’aide de modèles, configure les machines virtuelles au moyen d’extensions de machines virtuelles et intègre la gestion des accès et le balisage. Azure Resource Manager inclut un déploiement extensible, en parallèle, de machines virtuelles dans des groupes à haute disponibilité. nouveau modèle de déploiement Hello fournit également la gestion du cycle de vie de calcul, réseau et stockage de l’indépendamment. Enfin, il existe un focus sur l’activation de la sécurité par défaut avec l’application hello des machines virtuelles dans un réseau virtuel.

Presque toutes les fonctionnalités de hello à partir du modèle de déploiement classique de hello sont pris en charge pour le calcul, réseau et de stockage sous Azure Resource Manager. toobenefit à partir de capacités de nouveau hello dans Azure Resource Manager, vous pouvez migrer existante des déploiements à partir du modèle de déploiement classique hello.

## <a name="supported-resources-for-migration"></a>Ressources prises en charge pour la migration
Ces ressources IaaS classiques sont prises en charge lors de la migration

* Machines virtuelles
* Groupes à haute disponibilité
* Services cloud
* Comptes de stockage
* Virtual Network
* Passerelles VPN
* Express Route passerelles _(Bonjour même abonnement que réseau virtuel uniquement)_
* Network Security Group 
* Tables de routage 
* IP réservées 

## <a name="supported-scopes-of-migration"></a>Étendues de migration prises en charge
Il existe 4 façons toocomplete la migration des ressources de calcul, réseau et de stockage. Les voici : 

* Migration de machines virtuelles (ne figurant PAS dans un réseau virtuel)
* Migration de machines virtuelles (dans un réseau virtuel)
* Migration des comptes de stockage
* Ressources non attachées (groupes de sécurité réseau, tables de routage et adresses IP réservées)

### <a name="migration-of-virtual-machines-not-in-a-virtual-network"></a>Migration de machines virtuelles (ne figurant PAS dans un réseau virtuel)
Dans le modèle de déploiement du Gestionnaire de ressources hello, la sécurité est appliquée pour vos applications par défaut. Toutes les machines virtuelles doivent toobe dans un réseau virtuel dans le modèle de gestionnaire de ressources hello. Hello redémarrage de la plateforme Azure (`Stop`, `Deallocate`, et `Start`) hello des machines virtuelles dans le cadre de la migration de hello. Vous avez deux options pour les réseaux virtuels hello hello des Machines virtuelles vont être migrés vers :

* Vous pouvez demander des hello plateforme toocreate un nouveau réseau virtuel et migration hello virtuels dans le réseau virtuel hello.
* Vous pouvez migrer des machines virtuelles de hello dans un réseau virtuel existant dans le Gestionnaire de ressources.

> [!NOTE]
> Dans cette portée de la migration, les deux hello des opérations de plan de gestion et opérations de données-plan hello ne soyez pas autorisées pendant une période de temps pendant la migration de hello.
>
>

### <a name="migration-of-virtual-machines-in-a-virtual-network"></a>Migration de machines virtuelles (dans un réseau virtuel)
Pour la plupart des configurations de machine virtuelle, migre uniquement les métadonnées hello entre les modèles de déploiement classique et le Gestionnaire de ressources hello. Hello sous-jacent de machines virtuelles s’exécutent sur hello même matériel, Bonjour même réseau et avec hello même stockage. opérations de gestion-plan Hello ne peuvent pas être autorisées pour une certaine période de temps pendant la migration de hello. Toutefois, le plan de données hello continue toowork. Autrement dit, vos applications en cours d’exécution sur des machines virtuelles (classiques) n’entraînent pas de temps d’arrêt pendant la migration de hello.

Hello, suivant les configurations n’est pas pris en charge actuellement. Si la prise en charge est ajoutée dans hello future, certains ordinateurs virtuels dans cette configuration peuvent entraîner des temps d’arrêt (accédez à arrêter, libérer et redémarrer les opérations de machine virtuelle).

* Vous disposez de plus d’un groupe à haute disponibilité dans un seul service cloud.
* Vous disposez d’un ou de plusieurs groupes à haute disponibilité et de machines virtuelles ne figurant pas dans un groupe à haute disponibilité dans un seul service cloud.

> [!NOTE]
> Dans cette portée de la migration, plan de gestion hello ne peut pas autorisé pendant une période de temps pendant la migration de hello. Certaines configurations décrites ci-dessus entraînent un temps d’arrêt du forfait de données.
>
>

### <a name="storage-accounts-migration"></a>Migration des comptes de stockage
migration transparente de tooallow, vous pouvez déployer des machines virtuelles du Gestionnaire de ressources dans un compte de stockage classique. Cette fonctionnalité permet d’effectuer la migration des ressources de calcul et de réseau indépendamment des comptes de stockage. Une fois la migration sur vos Machines virtuelles et le réseau virtuel, vous devez toomigrate de votre processus de migration de stockage comptes toocomplete hello.

> [!NOTE]
> modèle de déploiement du Gestionnaire de ressources Hello ne concept hello des images de standard et des disques. Lorsque le compte de stockage hello est migrés, classiques des images et disques ne sont pas visibles dans la pile du Gestionnaire de ressources hello mais hello sauvegarde disques durs virtuels restent dans le compte de stockage hello.
>
>

### <a name="unattached-resources-network-security-groups-route-tables--reserved-ips"></a>Ressources non attachées (groupes de sécurité réseau, tables de routage et adresses IP réservées)
Groupes de sécurité réseau, les Tables d’itinéraires et des adresses IP réservées qui ne sont pas attachés tooany Machines virtuelles et des réseaux virtuels peuvent être migrés indépendamment.

<br>

## <a name="unsupported-features-and-configurations"></a>Fonctionnalités et configurations non prises en charge
À ce stade, nous ne gérons pas encore certaines fonctionnalités et configurations. Hello les sections suivantes décrire des nos recommandations autour d’elles.

### <a name="unsupported-features"></a>Fonctionnalités non prises en charge
Hello suivant les fonctionnalités n’est pas pris en charge actuellement. Vous pouvez éventuellement supprimer ces paramètres, migrer des machines virtuelles de hello et réactivez les paramètres hello dans le modèle de déploiement du Gestionnaire de ressources hello.

| Fournisseur de ressources | Fonctionnalité | Recommandation |
| --- | --- | --- |
| Calcul |Disques de machine virtuelle non associés. | objets BLOB de disque dur virtuel Hello derrière ces disques est obtenir migrés lors de la migration hello compte de stockage |
| Calcul |Images de machine virtuelle. | objets BLOB de disque dur virtuel Hello derrière ces disques est obtenir migrés lors de la migration hello compte de stockage |
| Réseau |Listes de contrôle d’accès de points de terminaison. | Supprimez les listes de contrôle d’accès des points de terminaison et réessayez la migration. |
| Réseau |Réseau virtuel doté d’une passerelle ExpressRoute et d’une passerelle VPN  | Supprimer hello passerelle VPN avant de commencer la migration, puis recréez les hello passerelle VPN une fois la migration est terminée. En savoir plus sur la [migration ExpressRoute](../articles/expressroute/expressroute-migration-classic-resource-manager.md).|
| Réseau |ExpressRoute avec des liens d’autorisation  | Supprimer la connexion de réseau hello ExpressRoute circuit toovirtaul avant de commencer la migration, puis recréez les connexions de hello une fois la migration est terminée. En savoir plus sur la [migration ExpressRoute](../articles/expressroute/expressroute-migration-classic-resource-manager.md). |
| Réseau |Application Gateway | Supprimer hello passerelle d’Application avant de commencer la migration, puis recréez les hello passerelle d’Application une fois la migration est terminée. |
| Réseau |Réseaux virtuels à l’aide de l’homologation de réseaux virtuels (VNet Peering). | Migrer le réseau virtuel tooResource Manager, puis d’homologues. Apprenez-en plus sur l’[Homologation de réseaux virtuels](../articles/virtual-network/virtual-network-peering-overview.md). | 

### <a name="unsupported-configurations"></a>Configurations non prises en charge
Hello, suivant les configurations n’est pas pris en charge actuellement.

| Service | Configuration | Recommandation |
| --- | --- | --- |
| Gestionnaire de ressources |Contrôle d’accès en fonction du rôle (RBAC) pour les ressources Classic |Hello URI des ressources de hello est modifié après la migration, il est recommandé que vous envisagez de hello RBAC stratégie mises à jour nécessitant toohappen après la migration. |
| Calcul |Plusieurs sous-réseaux associés à une machine virtuelle |Mettre à jour hello sous-réseau configuration tooreference uniquement sous-réseaux. |
| Calcul |Machines virtuelles qui font partie du réseau virtuel de tooa mais n’avez pas un sous-réseau explicit affecté |Vous pouvez éventuellement supprimer hello machine virtuelle. |
| Calcul |Machines virtuelles dotées d’alertes et de stratégies de mise à l’échelle automatique |migration de Hello traverse et ces paramètres sont supprimés. Il est fortement recommandé que vous évaluez votre environnement avant de vous hello migration. Ou bien, vous pouvez reconfigurer les paramètres d’alerte hello après la migration. |
| Calcul |Extensions XML de machines virtuelles (BGInfo 1.*, débogueur Visual Studio, Web Deploy et débogage à distance) |Ce n’est pas pris en charge. Il est recommandé que vous supprimez ces extensions à partir de la migration de toocontinue hello des machines virtuelles, ou elles sont supprimées automatiquement durant le processus de migration hello. |
| Calcul |Diagnostics de démarrage avec le stockage Premium |Désactiver la fonctionnalité Diagnostics de démarrage pour hello machines virtuelles avant de poursuivre la migration. Vous pouvez réactiver les diagnostics de démarrage dans la pile du Gestionnaire de ressources hello après la migration de hello. En outre, les objets Blob utilisés pour la capture d’écran et les journaux de série doivent être supprimés afin que vous ne soyez plus facturé pour ces objets Blob. |
| Calcul |Services cloud contenant des rôles Web/de travail |Non pris en charge actuellement. |
| Réseau |Réseaux virtuels contenant des machines virtuelles et des rôles Web/de travail |Non pris en charge actuellement. |
| Azure App Service |Réseaux virtuels contenant des environnements App Service |Non pris en charge actuellement. |
| Azure HDInsight |Réseaux virtuels contenant des services HDInsight |Non pris en charge actuellement. |
| Services de cycle de vie Microsoft Dynamics |Réseaux virtuel contenant des machines virtuelles gérées par Dynamics Lifecycle Services |Non pris en charge actuellement. |
| Services de domaine Azure AD |Réseaux virtuels contenant des services de domaine Azure AD |Non pris en charge actuellement. |
| Azure RemoteApp |Réseaux virtuels contenant des déploiements Azure RemoteApp |Non pris en charge actuellement. |
| Gestion des API Azure |Réseaux virtuels contenant des déploiements Gestion des API Azure |Non pris en charge actuellement. toomigrate hello IaaS VNET, modifiez hello réseau virtuel de hello déploiement de gestion des API qui n’est pas une opération de temps d’arrêt. |
| Calcul |Extensions Azure Security Center avec un réseau virtuel disposant d’une passerelle VPN dans une connectivité en transit ou d’une passerelle ExpressRoute avec serveur DNS local |Centre de sécurité Azure installe les extensions sur vos Machines virtuelles de toomonitor leur sécurité automatiquement et déclencher des alertes. Ces extensions généralement installées automatiquement si hello stratégie du centre de sécurité Azure est activé sur les abonnement hello. La migration de la passerelle ExpressRoute n’est pas prise en charge actuellement et les passerelles VPN avec connectivité de transit perdent l’accès local. Vous supprimez ExpressRoute passerelle ou migration de passerelle VPN avec connectivité de transit, compte de stockage du tooVM internet access toobe perdue lors de la poursuite de la validation de la migration hello. migration de Hello ne va pas dans ce cas comme objet blob d’état agent hello invité ne peuvent pas être rempli. Il est recommandé toodisable stratégie Azure Security Center sur les abonnement hello 3 heures avant de procéder à la migration. |

