## <a name="meaning-of-migration-of-iaas-resources-from-hello-classic-deployment-model-tooresource-manager"></a>Sens de la migration des ressources IaaS de tooResource de modèle de déploiement classique hello Manager
Avant de nous Explorez les détails de hello, examinons différence hello entre les opérations de données-plan et plan de gestion sur les ressources IaaS hello.

* *Plan de contrôle de la gestion* décrit les appels hello fournis dans le plan de contrôle de la gestion de hello ou hello API pour la modification des ressources. Par exemple, les opérations telles que la création d’une machine virtuelle, le redémarrage d’une machine virtuelle et la mise à jour d’un réseau virtuel avec un nouveau sous-réseau gérer hello ressources en cours d’exécution. Ils n’affectent pas directement les instances toohello connexion.
* *Plan de données* (application) décrit hello d’exécution d’application hello elle-même et nécessite une interaction avec les instances qui ne passent pas hello API Azure. Par exemple, l’accès à votre site web ou l’extraction de données à partir d’une instance de serveur SQL ou d’un serveur MongoDB en cours d’exécution sont considérés comme des interactions d’application ou de plan de données. Copie un objet blob à partir d’un compte de stockage et de l’accès à un tooRDP d’adresse IP publique ou de SSH dans la machine virtuelle de hello sont également plan de données. Ces opérations conservent l’application hello en cours d’exécution sur le calcul, de mise en réseau et de stockage.

Coulisses de hello, plan de données hello est hello même entre hello modèle de déploiement classique et pile Resource Manager. Pendant le processus de migration, nous convertir la représentation sous forme de hello de ressources hello toothat de modèle de déploiement de classique hello dans la pile du Gestionnaire de ressources hello. Par conséquent, vous devez toouse nouveaux outils, API, les kits de développement logiciel toomanage vos ressources dans la pile du Gestionnaire de ressources hello.

![Capture d’écran qui illustre la différence entre un plan de gestion/contrôle et le plan de données](../articles/virtual-machines/media/virtual-machines-windows-migration-classic-resource-manager/data-control-plane.png)


> [!NOTE]
> Dans certains scénarios de migration, hello s’arrête la plateforme Azure et désalloue redémarre vos machines virtuelles. Cela entraîne un bref temps d’arrêt du forfait de données.
>

## <a name="hello-migration-experience"></a>expérience de migration Hello
Avant de commencer, l’expérience de migration hello, suivant de hello est recommandé :

* Assurez-vous que les ressources hello que vous souhaitez toomigrate n’utilisent pas toutes les fonctionnalités prises en charge ou les configurations. Généralement, plateforme de hello détecte ces problèmes et génère une erreur.
* Si vous avez des machines virtuelles qui ne sont pas dans un réseau virtuel, ils seront arrêtés et désallouées comme partie de hello l’opération de préparation. Si vous ne souhaitez pas adresse IP publique de toolose hello, opération de préparation d’étudier de réservation d’adresse IP de hello avant le déclenchement de hello. Toutefois, si les machines virtuelles de hello sont dans un réseau virtuel, ils ne sont pas arrêtés et désallouées.
* Planifiez votre migration pendant tooaccommodate en dehors des heures pour les échecs inattendus peuvent se produire pendant la migration.
* Télécharger la configuration actuelle de hello de vos machines virtuelles à l’aide de PowerShell, les commandes de l’interface de ligne de commande (CLI) ou toomake API REST de validation après l’étape de préparation hello est terminée.
* Mettre à jour votre modèle de déploiement de gestionnaire de ressources à l’automation/Opérationnalisation scripts toohandle hello avant de commencer la migration de hello. Vous pouvez éventuellement effectuer les opérations GET lorsque les ressources hello sont hello préparé l’état.
* Évaluer les stratégies RBAC hello qui sont configurés sur les ressources IaaS classiques hello et planifier après la migration de hello.

flux de travail de migration Hello est comme suit

![Capture d’écran qui illustre le flux de travail de migration hello](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-workflow.png)

> [!NOTE]
> Toutes les opérations de hello décrites dans les sections suivantes de hello sont idempotent. Si vous avez un problème autre qu’une fonctionnalité non prise en charge ou une erreur de configuration, il est recommandé de relancer hello préparer, abandonner ou valider l’opération. Hello plateforme Azure essaie de recommencer hello.
>
>

### <a name="validate"></a>Valider
Hello valider l’opération est hello première étape dans le processus de migration hello. Hello cette étape vise état de hello tooanalyze des ressources hello vous souhaitez toomigrate dans le modèle de déploiement classique hello et que vous retournez réussite/échec si les ressources hello sont capables de migration.

Vous sélectionnez les réseaux virtuels hello ou un service cloud (s’il n’est pas dans un réseau virtuel) que vous souhaitez toovalidate pour la migration.

* Si les ressources hello ne sont pas capable de migration, hello plateforme Azure répertorie toutes les raisons de hello pourquoi il n'est pas pris en charge pour la migration.

#### <a name="checks-not-done-in-validate"></a>Vérifications non effectuées dans l’étape « Valider »

Valider les opération d’analyse uniquement état hello des ressources hello dans le modèle de déploiement classique hello. Il peut vérifier tous les échecs et les scénarios non pris en charge en raison des configurations toovarious dans le modèle de déploiement classique hello. Il n’est pas possible de toocheck pour tous les problèmes hello Azure Resource Manager pile peut imposer des ressources de hello pendant la migration. Ces problèmes sont vérifiées uniquement les ressources hello subir une transformation à l’étape suivante de hello de la migration, autrement dit, préparer. Hello ci-dessous répertorie tous les problèmes de hello non archivés à valider.


|Vérifications réseau non effectuées dans l’étape « Valider »|
|-|
|Un réseau virtuel ayant des passerelles ER et VPN|
|Connexion à la passerelle de réseau virtuel dans l’état déconnecté|
|Tous les circuits ER sont pile du Gestionnaire de ressources tooAzure pré-migrés|
|Quota de vérifications Azure Resource Manager des ressources réseau, à savoir : adresse IP publique statique, adresses IP publiques dynamiques, équilibreur de charge, groupes de sécurité réseau, tables de routage, interfaces réseau |
| Vérifier que toutes les règles d’équilibrage de charge sont valides sur le déploiement/réseau virtuel |
| Vérification pour les adresses IP privée en conflit entre les machines virtuelles l’arrêtées désallouées Bonjour même réseau virtuel |

### <a name="prepare"></a>Préparation
l’opération de préparation Hello est hello deuxième étape hello processus de migration. l’objectif Hello est transformation de hello toosimulate Hello les ressources IaaS de déploiement classique modèle tooResource Manager et de les présenter côte à côte vous toovisualize.

> [!NOTE] 
> Vos ressources classiques ne sont pas modifiées lors de cette étape. Il est donc un toorun étape sécurisée si vous testez la migration. 

Vous sélectionnez hello virtuel réseau ou hello service cloud (s’il n’est pas un réseau virtuel) que vous souhaitez tooprepare pour la migration.

* Si les ressources hello ne sont pas capable de migration, hello plateforme Azure arrête le processus de migration hello et répertorie le motif hello pourquoi hello préparer l’opération a échoué.
* Si la ressource de hello est capable de migration, hello plateforme Azure première verrouille les opérations de gestion-plan hello pour les ressources hello en cours de migration. Par exemple, vous n’êtes pas en mesure de tooadd un tooa de disque de données machine virtuelle en cours de migration.

Hello plateforme Azure démarre ensuite migration hello de métadonnées à partir de tooResource de modèle de déploiement classique Manager pour hello migration des ressources.

Une fois que hello préparer l’opération est terminée, vous pouvez hello de visualisation des ressources hello dans le modèle de déploiement classique et le Gestionnaire de ressources. Pour chaque service cloud dans le modèle de déploiement classique de hello, hello plateforme Azure crée un nom de groupe de ressources qui a hello modèle `cloud-service-name>-Migrated`.

> [!NOTE]
> Nom de hello tooselect possible du groupe de ressources créé pour les ressources migrées n’est pas (par exemple, «-migré »), mais une fois la migration terminée, vous pouvez utiliser Azure Resource Manager déplacement fonctionnalité toomove ressources tooany groupe de ressources que vous souhaitez. tooread plus d’informations sur cet voir [déplacer le groupe de ressources toonew ressources ou d’un abonnement](../articles/resource-group-move-resources.md)

Voici deux écrans qui montrent les résultats hello après une opération de préparation réussie. Premier écran montre un groupe de ressources qui contient le service de cloud hello d’origine. Deuxième écran montre hello nouveau »-migré « groupe de ressources qui contient les ressources Azure Resource Manager équivalentes hello.

![Capture d’écran illustrant le portail de service cloud classique](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-classic.png)

![Capture d’écran qui affiche les ressources du portail Azure Resource Manager lors d’une opération de préparation](../articles/virtual-machines/windows/media/migration-classic-resource-manager/portal-arm.png)

Voici les coulisses vos ressources après l’achèvement de hello de phase de préparation. Notez que les ressources hello sont le plan de données hello est hello même. Elle est représentée dans le plan de gestion hello (modèle de déploiement classique) et plan de contrôle hello (Resource Manager).

![Coulisses de hello dans la phase de préparation](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-prepare.png)

> [!NOTE]
> Lors de cette phase de migration, les machines virtuelles qui ne font pas partie d’un réseau virtuel classique sont arrêtées et désallouées.
>

### <a name="check-manual-or-scripted"></a>Vérification (manuelle ou sur la base d’un script)
Dans l’étape de vérification hello, vous pouvez éventuellement utiliser configuration hello que vous avez téléchargé toovalidate antérieur que la migration hello est correcte. Vous pouvez également vous connecter toohello portail et sondages hello propriétés et ressources toovalidate que la migration des métadonnées semble correcte.

Si vous effectuez la migration d’un réseau virtuel, la majeure partie de la configuration des machines virtuelles n’est pas redémarrée. Pour les applications sur ces machines virtuelles, vous pouvez valider que l’application hello est toujours en cours d’exécution.

Vous pouvez tester votre analyse/automation et les scripts opérationnels toosee si hello machines virtuelles fonctionnent comme prévu et si vos scripts de mise à jour fonctionnent correctement. Seules les opérations GET sont prises en charge lorsque les ressources hello sont hello préparé l’état.

Il n’existe pas définir une fenêtre de temps avant laquelle vous avez besoin de la migration toocommit hello. Vous pouvez conserver les ressources en l’état pour la durée de votre choix. Toutefois, plan de gestion hello est verrouillée pour ces ressources jusqu'à ce que vous l’annulation ou la validez.

Si vous voyez les problèmes, vous pouvez toujours annuler la migration hello et modèle de déploiement classique toohello revenir en arrière. Une fois que vous revenez en arrière, hello plateforme Azure s’ouvre opérations de plan de gestion de hello sur les ressources de hello afin que vous puissiez reprendre les opérations normales sur ces machines virtuelles dans le modèle de déploiement classique hello.

### <a name="abort"></a>Abandon
Abandon est une étape facultative que vous pouvez utiliser toorevert votre modèle de déploiement classique de modifications toohello et arrêter la migration de hello. Cette opération supprime hello des métadonnées de gestionnaire de ressources pour vos ressources qui a été créé à l’étape de préparation précédente hello. 

![Coulisses de hello en phase d’abandon](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-abort.png)


> [!NOTE]
> Cette opération ne peut pas être exécutée une fois que vous avez avoir déclenché l’opération de validation hello.     
>

### <a name="commit"></a>Validation
Après avoir terminé la validation hello, vous pouvez valider la migration hello. Ressources n’apparaissent pas plus dans le modèle de déploiement classique et sont disponibles uniquement dans le modèle de déploiement du Gestionnaire de ressources hello. Hello ressources migrées peuvent être gérés uniquement dans le nouveau portail de hello.

> [!NOTE]
> Il s’agit d’une opération idempotente. En cas d’échec, il est recommandé que vous réessayez hello. S’il continue toofail, créez un ticket de support ou créer un forum post avec une balise ClassicIaaSMigration sur notre [Forum sur la machine virtuelle](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).
>
>

![Coulisses de hello en phase de validation](../articles/virtual-machines/windows/media/migration-classic-resource-manager/behind-the-scenes-commit.png)

## <a name="where-toobegin-migration"></a>Où toobegin migration ?

Voici un organigramme qui montre comment tooproceed avec la migration

![Capture d’écran qui illustre les étapes de migration hello](../articles/virtual-machines/windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="translation-of-classic-deployment-model-tooazure-resource-manager-resources"></a>Traduction de ressources de gestionnaire de ressources de tooAzure de modèle de déploiement classique
Vous trouverez un modèle de déploiement classique hello et les représentations sous forme de gestionnaire de ressources des ressources de hello Bonjour tableau suivant. D’autres fonctionnalités et ressources ne sont pas prises en charge actuellement.

| Représentation Classic | Représentation Resource Manager | Remarques détaillées |
| --- | --- | --- |
| Nom du service cloud |Nom DNS |Pendant la migration, un nouveau groupe de ressources est créé pour chaque service cloud avec le modèle de désignation hello `<cloudservicename>-migrated`. Ce groupe de ressources contient toutes vos ressources. nom du service cloud Hello devient un nom DNS associé avec l’adresse IP publique de hello. |
| Machine virtuelle |Machine virtuelle |Les propriétés spécifiques à la machine virtuelle sont inchangées après la migration. Certaines informations osProfile, comme le nom de l’ordinateur ne sont pas stockées dans le modèle de déploiement classique hello et restent vides après la migration. |
| Ressources de disque attachés tooVM |Implicite de disques attachés tooVM |Les disques ne sont pas modélisées en tant que ressources de niveau supérieur dans le modèle de déploiement du Gestionnaire de ressources hello. Ils sont migrés en tant que disques implicites sous hello machine virtuelle. Seuls les disques qui sont attachés tooa machine virtuelle sont pris en charge actuellement. Machines virtuelles du Gestionnaire de ressources peuvent désormais utiliser des comptes de stockage classiques, qui permet de migrer facilement des hello disques toobe sans les mises à jour. |
| Extensions de machine virtuelle |Extensions de machine virtuelle |Toutes les extensions de ressource hello, à l’exception des extensions XML, sont migrées à partir du modèle de déploiement classique hello. |
| Certificats de machine virtuelle |Certificats dans Azure Key Vault |Si un service cloud contient les certificats de service, un nouveau coffre de clés Azure par le service cloud et déplace les certificats hello dans le coffre de clés hello. machines virtuelles de Hello sont tooreference mis à jour les certificats hello hello coffre de clés. <br><br> **Remarque :** ne supprimez pas hello keyvault car cela peut provoquer hello VM toogo dans un état d’échec. Nous travaillons sur l’amélioration des éléments dans le service principal hello afin que les coffres de clé peut être supprimés en toute sécurité ou déplacées avec hello VM tooa un nouvel abonnement. |
| Configuration WinRM |Configuration WinRM sous osProfile |Configuration de la gestion à distance est déplacée de Windows sans le modifier, dans le cadre de la migration de hello. |
| Propriété de groupe à haute disponibilité |Ressource de groupe à haute disponibilité | Spécification de l’ensemble de disponibilité a une propriété sur hello machine virtuelle dans le modèle de déploiement classique hello. Haute disponibilité deviennent une ressource de niveau supérieur dans le cadre de la migration de hello. Hello configurations suivantes ne sont pas compatibles : plusieurs groupes à haute disponibilité par le service cloud ou à haute disponibilité d’un ou plusieurs en même temps que les machines virtuelles qui ne sont pas dans un groupe à haute disponibilité dans un service cloud. |
| Configuration réseau sur une machine virtuelle |Interface réseau principale |Configuration du réseau sur une machine virtuelle est représentée en tant que ressource d’interface réseau principale hello après la migration. Pour les machines virtuelles qui ne sont pas dans un réseau virtuel, l’adresse IP interne hello change pendant la migration. |
| Plusieurs interfaces réseau sur une machine virtuelle |Interfaces réseau |Si un ordinateur virtuel possède plusieurs interfaces réseau associées, chaque interface réseau devient une ressource de niveau supérieur dans le cadre de la migration de hello dans le modèle de déploiement du Gestionnaire de ressources hello, ainsi que toutes les propriétés de hello. |
| Jeux de points de terminaison soumis à l’équilibrage de charge |Équilibrage de charge |Dans le modèle de déploiement classique de hello, plateforme de hello attribué un équilibrage de charge implicite pour chaque service cloud. Pendant la migration, une nouvelle ressource d’équilibrage de charge est créée, et ensemble de point de terminaison de l’équilibrage de charge hello devient règles d’équilibrage de charge. |
| Règles NAT entrantes |Règles NAT entrantes |Des points de terminaison d’entrée définis sur hello machine virtuelle sont des règles de traduction d’adresse réseau tooinbound converti sous un équilibreur de charge hello pendant la migration de hello. |
| Adresse IP virtuelle |Adresse IP publique avec nom DNS |l’adresse IP virtuelle Hello devient une adresse IP publique et est associé à équilibrage de charge hello. Une adresse IP virtuelle peut être migrée uniquement s’il existe un point de terminaison d’entrée affecté tooit. |
| Réseau virtuel |Réseau virtuel |réseau virtuel de Hello est migré, avec toutes ses propriétés, modèle de déploiement du Gestionnaire de ressources toohello. Un groupe de ressources est créé avec le nom de hello `-migrated`. |
| IP réservées |Adresse IP publique avec méthode d’allocation statique |Adresses IP réservées associée à équilibrage de charge hello sont migrés en même temps que la migration du service de cloud computing hello ou ordinateur virtuel de hello hello. La migration d’adresses IP réservées non associées n’est pas prise en charge actuellement. |
| Adresse IP publique par machine virtuelle |Adresse IP publique avec méthode d’allocation dynamique |Hello adresse IP publique associée hello que machine virtuelle est convertie en une ressource d’adresse IP publique avec hello allocation méthode set toostatic. |
| Groupes de sécurité réseau |Groupes de sécurité réseau |Les groupes de sécurité réseau associés à un sous-réseau sont clonés en tant que partie du modèle de déploiement hello migration toohello Gestionnaire de ressources. Hello NSG dans le modèle de déploiement classique hello n’est pas supprimé lors de la migration de hello. Toutefois, les opérations de plan de gestion de hello pour hello groupe de sécurité réseau sont bloquées lors de la migration de hello est en cours d’exécution. |
| Serveurs DNS |Serveurs DNS |Serveurs DNS associé à un réseau virtuel ou hello ordinateurs virtuels sont migrés en tant que partie de hello correspondant migration de ressources, ainsi que toutes les propriétés de hello. |
| Itinéraires définis par l’utilisateur (UDR) |Itinéraires définis par l’utilisateur (UDR) |Itinéraires définis par l’utilisateur associés à un sous-réseau sont clonés en tant que partie du modèle de déploiement hello migration toohello Gestionnaire de ressources. Hello UDR dans le modèle de déploiement classique hello n’est pas supprimé lors de la migration de hello. opérations de gestion-plan Hello pour hello UDR sont bloquées lors de la migration de hello est en cours d’exécution. |
| Propriété de transfert IP sur la configuration réseau d’une machine virtuelle |Transfert de propriété sur hello carte réseau IP |propriété du transfert IP Hello sur une machine virtuelle est propriété converti tooa sur l’interface de réseau hello pendant la migration de hello. |
| Équilibreur de charge avec plusieurs adresses IP |Équilibreur de charge avec plusieurs ressources d’adresses IP publiques |Chaque adresse IP publique associée à équilibrage de charge hello est la ressource IP publique tooa converti et équilibrage de charge hello après la migration. |
| Noms DNS internes sur hello machine virtuelle |Noms DNS internes sur hello NIC |Pendant la migration, les suffixes DNS internes hello pour les machines virtuelles de hello sont migrés tooa propriété en lecture seule nommée « InternalDomainNameSuffix » sur hello carte réseau. suffixe de Hello reste inchangé après la migration et résolution de la machine virtuelle doit continuer toowork comme précédemment. |
| Passerelle de réseau virtuel |Passerelle de réseau virtuel |Les propriétés de la passerelle de réseau virtuel sont inchangées après la migration. Hello VIP associé hello passerelle ne modifie pas le soit. |
| Site de réseau local |Passerelle de réseau local |Propriétés du site réseau local sont migrés tooa inchangée nouvelle ressource appelée passerelle de réseau Local. Ceci représente les préfixes d’adresse locale et l’adresse IP de la passerelle distante. |
| Références de connexions |Connexion |Les références de connectivité entre la passerelle et le site de réseau local dans la configuration réseau sont représentées par une ressource nouvellement créée appelée Connexion dans Resource Manager après la migration. Toutes les propriétés de référence de connectivité dans les fichiers de configuration de réseau sont copiés toohello inchangée nouvellement créé la ressource de connexion. Connectivité de tooVNet de réseau virtuel dans classique est obtenue en créant des tunnels IPsec deux sites de réseau toolocal représentant hello des réseaux virtuels. Il s’agit transformé tooVnet2Vnet connexion type dans le modèle de gestionnaire de ressources sans nécessiter de passerelles de réseau local. |

## <a name="changes-tooyour-automation-and-tooling-after-migration"></a>Modifications tooyour automation et outils après la migration
Dans le cadre de la migration de vos ressources à partir du modèle de déploiement du Gestionnaire de ressources de toohello hello classique déploiement modèle, vous avez tooupdate votre automatisation existante ou un tooensure outils qu’il remplisse toujours toowork après la migration de hello.
