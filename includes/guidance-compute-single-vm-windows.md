Cet article présente un ensemble de pratiques éprouvées pour une machine virtuelle de Windows (machine virtuelle) en cours d’exécution sur Azure, le paiement de sécurité, la disponibilité, la facilité de gestion et une attention tooscalability.

> [!NOTE]
> Azure propose deux modèles de déploiement : [Azure Resource Manager][resource-manager-overview] et Azure Classic. Cet article utilise Resource Manager, solution recommandée par Microsoft pour les nouveaux déploiements.
>
>

Il est déconseillé d’utiliser une seule et même machine virtuelle pour les charges de travail stratégiques, car ce faisant, un seul point de défaillance est créé. Pour bénéficier d’une disponibilité plus élevée, vous devez déployer plusieurs machines virtuelles dans un [groupe à haute disponibilité][availability-set]. Pour plus d’informations, voir [Running multiple VMs on Azure (Exécution de plusieurs machines virtuelles sur Azure)][multi-vm].

## <a name="architecture-diagram"></a>Diagramme de l’architecture

Configuration d’une machine virtuelle dans Azure implique plus de parties que simplement hello machine virtuelle proprement dite. Il faut inclure les éléments de calcul, de mise en réseau et de stockage.

> Un document Visio qui inclut ce diagramme d’architecture est disponible en téléchargement à partir de hello [centre de téléchargement Microsoft][visio-download]. Ce diagramme est sur hello « Calcul - seule machine virtuelle » page.
>
>

![[0]][0]

* **Groupe de ressources.** Un [*groupe de ressources*][resource-manager-overview] est un conteneur qui héberge les ressources associées. Créer une ressource de ressources du groupe toohold hello pour cet ordinateur virtuel.
* **Machine virtuelle**. Vous pouvez configurer une machine virtuelle à partir d’une liste d’images publiées ou d’un fichier de disque dur virtuel (VHD) que vous téléchargez tooAzure stockage d’objets Blob.
* **Disque du système d’exploitation.** disque de Hello du système d’exploitation est un disque dur virtuel stocké dans [Azure Storage][azure-storage]. Cela signifie qu’il persiste même si l’ordinateur hôte de hello tombe en panne.
* **Disque temporaire** machine virtuelle Hello est créé avec un disque temporaire (hello `D:` lecteur sous Windows). Ce disque est stocké sur un lecteur physique sur l’ordinateur hôte de hello. Il *n’est pas* enregistré dans Stockage Azure et peut être supprimé lors des redémarrages ou d’autres événements de cycle de vie de la machine virtuelle. N’utilisez ce disque que pour des données temporaires, telles que des fichiers de pagination ou d’échange.
* **Disques de données.** Un [disque de données][data-disk] est un disque dur virtuel persistant utilisé pour les données d’application. Disques de données sont stockés dans le stockage Azure, comme disque de hello du système d’exploitation.
* **Réseau virtuel (VNet) et sous-réseau.** Chaque machine virtuelle dans Azure est déployée dans un réseau virtuel divisé en sous-réseaux.
* **Adresse IP publique.** Une adresse IP publique est toocommunicate nécessaire avec hello VM&mdash;par exemple sur le Bureau à distance (RDP).
* **Interfaces réseau (NIC)**. Hello NIC Active toocommunicate de machine virtuelle hello avec un réseau virtuel hello.
* **Groupe de sécurité réseau**. Hello [NSG] [ nsg] tooallow utilisé/deny de sous-réseau de toohello le trafic réseau. Vous pouvez associer un NSG à une carte réseau individuelle ou à un sous-réseau. Si vous l’associez à un sous-réseau, les règles du groupe de sécurité réseau hello s’appliquent VMs tooall dans ce sous-réseau.
* **Diagnostics.** Journalisation des diagnostics est cruciale pour la gestion et la résolution des problèmes de hello machine virtuelle.

## <a name="recommendations"></a>Recommandations

Hello conformément aux recommandations s’appliquent pour la plupart des scénarios. Suivez ces recommandations, sauf si vous avez un besoin spécifique qui vous oblige à les ignorer.

### <a name="vm-recommendations"></a>Recommandations pour les machines virtuelles

Azure propose de nombreuses tailles de machine virtuelle différente, mais nous vous recommandons de hello et GS-série DS prenant en charge de ces tailles de machine [stockage Premium][premium-storage]. Choisissez l’une de ces tailles de machine virtuelle, sauf si vous disposez d’une charge de travail spécialisée tel qu’un système de calcul hautes performances. Pour en savoir plus, consultez les [tailles des machines virtuelles][virtual-machine-sizes].

Si vous déplacez un tooAzure existant de la charge de travail, démarrer avec une taille de machine virtuelle hello tooyour de correspondance le plus proche hello serveurs locaux. Mesurer les performances de votre charge de travail réelle avec hello respecter tooCPU, la mémoire et les opérations d’entrées/sorties disque par seconde (IOPS), puis ajuster la taille de hello si nécessaire. Si vous avez besoin de plusieurs cartes réseau pour votre machine virtuelle, gardez à l’esprit que le nombre maximal de hello de cartes réseau est une fonction de hello [taille de machine virtuelle][vm-size-tables].   

Lorsque vous configurez hello machine virtuelle et autres ressources, vous devez spécifier une région. En règle générale, choisissez une région des utilisateurs internes tooyour le plus proche ou clients. Sachez toutefois que certaines tailles de machine virtuelle ne sont pas disponibles dans toutes les régions. Pour en savoir plus, voir les [services par région][services-by-region]. toosee une liste des tailles de machine virtuelle hello disponibles dans une région donnée, exécutez hello suivant de commande Azure de l’interface de ligne de commande (CLI) :

```
azure vm sizes --location <location>
```

Pour plus d’informations sur le choix d’une image de machine virtuelle publiée, consultez l’article [Parcourir et sélectionner des images de machines virtuelles Windows dans Azure avec l’interface CLI ou PowerShell][select-vm-image].

### <a name="disk-and-storage-recommendations"></a>Recommandations pour le disque et le stockage

Pour optimiser les performances d’E/S du disque, nous vous recommandons [Stockage Premium][premium-storage], qui stocke les données sur des disques SSD. Coût est basé sur la taille de hello du disque à allocation hello. Le nombre d’E/S par seconde et le débit dépendent également de la taille du disque. Lorsque vous approvisionnez un disque, vous devez donc tenir compte des trois facteurs : capacité, E/S par seconde et débit.

Créer des comptes de stockage Azure distincts pour chaque machine virtuelle toohold hello disques virtuels (VHD) dans tooavoid de commande en appuyant sur les limites d’IOPS hello pour les comptes de stockage.

Ajoutez un ou plusieurs disques de données. Lorsque vous créez un disque dur virtuel, il n’est pas formaté. Connectez-vous à un disque de hello tooformat hello VM. Si vous avez un grand nombre de disques de données, tenez compte des limites de d’e/s total hello hello du compte de stockage. Pour en savoir plus, voir les [limites du nombre de disques de machine virtuelle][vm-disk-limits].

Lorsque cela est possible, installez les applications sur un disque de données n’est pas le disque de système d’exploitation hello. Toutefois, certaines applications héritées peut-être composants tooinstall sur hello lecteur C:. Dans ce cas, vous pouvez [redimensionner hello du système d’exploitation disque] [ resize-os-disk] à l’aide de PowerShell.

Pour de meilleures performances, créez un compte de stockage distincts toohold les journaux de diagnostic. Un compte de stockage localement redondant (LRS) standard suffit pour les journaux de diagnostic.

### <a name="network-recommendations"></a>Recommandations pour le réseau

adresse IP publique de Hello peut être statique ou dynamique. valeur par défaut de Hello est dynamique.

* Réserve un [adresse IP statique] [ static-ip] si vous avez besoin d’une adresse IP fixe qui ne changera pas &mdash; , par exemple, si vous avez besoin de toocreate un un enregistrement dans DNS ou devez hello liste sécurisée ajouté tooa toobe d’adresses IP.
* Vous pouvez également créer un nom de domaine complet (FQDN) pour l’adresse IP de hello. Vous pouvez inscrire un [enregistrement CNAME] [ cname-record] dans DNS qui pointe toohello nom de domaine complet. Pour plus d’informations, consultez [créer un nom de domaine complet dans le portail Azure de hello][fqdn].

Tous les groupes de sécurité réseau contiennent un ensemble de [règles par défaut][nsg-default-rules], notamment une règle qui bloque tout le trafic Internet entrant. les règles par défaut Hello ne peut pas être supprimés, mais les autres règles peuvent les remplacer. tooenable le trafic Internet, créer des règles qui autorisent le trafic entrant toospecific ports &mdash; , par exemple, le port 80 pour HTTP.  

tooenable RDP, ajoutez une règle de groupe de sécurité réseau qui autorise le trafic entrant tooTCP le port 3389.

## <a name="scalability-considerations"></a>Considérations relatives à l’extensibilité

Vous pouvez faire évoluer une machine virtuelle vers le haut ou vers le bas en [la modification de taille de machine virtuelle hello](../articles/virtual-machines/windows/sizes.md). tooscale out placés horizontalement, deux ou plusieurs machines virtuelles dans un groupe à haute disponibilité derrière un équilibreur de charge. Pour plus d’informations, voir [Exécution de plusieurs machines virtuelles sur Azure pour l’évolutivité et la disponibilité][multi-vm].

## <a name="availability-considerations"></a>Considérations relatives à la disponibilité

Pour bénéficier d’une disponibilité plus élevée, vous devez déployer plusieurs machines virtuelles dans un groupe à haute disponibilité. Cela fournit également un [contrat de niveau de service][vm-sla] (SLA) supérieur.

Votre machine virtuelle peut être affectée par la [maintenance planifiée][planned-maintenance] ou la [maintenance non planifiée][manage-vm-availability]. Vous pouvez utiliser [VM redémarrer journaux] [ reboot-logs] toodetermine si une machine virtuelle redémarrer a été provoquée par une maintenance planifiée.

Les disques durs virtuels sont stockés dans [Stockage Azure][azure-storage], lequel est répliqué à des fins de durabilité et de disponibilité.

tooprotect contre la perte accidentelle de données pendant les opérations normales (par exemple, en raison d’une erreur de l’utilisateur), vous devez également implémenter des sauvegardes dans le temps, à l’aide de [instantanés d’objets blob] [ blob-snapshot] ou un autre outil.

## <a name="manageability-considerations"></a>Considérations relatives à la facilité de gestion

**Groupes de ressources.** Fortement couplés de ressources que hello partage du cycle de vie de même dans hello même [groupe de ressources][resource-manager-overview]. Groupes de ressources vous toodeploy et le moniteur de ressources en tant que groupe et restaurer des coûts par groupe de ressources de facturation. Vous pouvez également supprimer des ressources dans un ensemble, ce qui est très utile pour les déploiements de test. Nommez les ressources de façon explicite. Qui rend plus facile toolocate une ressource spécifique et comprendre son rôle. Voir [Conventions d’affectation de noms recommandées pour les ressources Azure][naming conventions].

**VM diagnostics.** Permet la surveillance et le diagnostic, avec notamment des indicateurs d’intégrité de base, des journaux d’infrastructure de diagnostic et des [diagnostics de démarrage][boot-diagnostics]. Les diagnostics de démarrage peuvent vous aider à identifier un problème de démarrage si votre machine virtuelle refuse de démarrer. Pour en savoir plus, voir [Activation de la surveillance et des diagnostics][enable-monitoring]. Hello d’utilisation [collecte des journaux Azure] [ log-collector] extension toocollect plateforme Azure se connecte et les télécharger tooAzure stockage.   

Hello CLI commande suivante permet de diagnostics :

```
azure vm enable-diag <resource-group> <vm-name>
```

**Arrêt d’une machine virtuelle.** Azure établit une distinction entre les états « arrêté » et « désalloué ». Vous êtes facturé quand hello état de la machine virtuelle est arrêtée, mais pas quand hello VM n’est pas libéré.

Utilisez hello suivant CLI commande toodeallocate une machine virtuelle :

```
azure vm deallocate <resource-group> <vm-name>
```

Bonjour portail Azure, hello **arrêter** bouton désalloue hello machine virtuelle. Toutefois, si vous arrêtez via hello du système d’exploitation lorsque vous êtes connecté, hello machine virtuelle est arrêtée, mais *pas* désallouées, donc vous serez facturé.

**Suppression d’une machine virtuelle.** Si vous supprimez une machine virtuelle, les disques durs virtuels hello ne sont pas supprimés. Cela signifie que vous pouvez supprimer en toute sécurité hello machine virtuelle sans perte de données. Toutefois, vous serez toujours facturé pour le stockage. toodelete hello disque dur virtuel, supprimez le fichier hello [stockage d’objets Blob][blob-storage].

tooprevent une suppression accidentelle, utilisez un [verrou de ressource] [ resource-lock] toolock hello ressource entière groupe ou un verrou des ressources, telles que hello machine virtuelle.

## <a name="security-considerations"></a>Considérations relatives à la sécurité

Utilisez [Azure Security Center] [ security-center] tooget une vue centralisée de l’état de la sécurité de vos ressources Azure hello. Centre de sécurité surveille les problèmes potentiels de sécurité et fournit une image complète de l’intégrité de la sécurité de votre déploiement hello. Le Centre de sécurité est configuré pour chaque abonnement Azure. Activez la collecte de données de sécurité comme décrit dans la section [Utiliser le Centre de sécurité]. Une fois la collecte de données activée, le Centre de sécurité analyse automatiquement les machines virtuelles créées dans le cadre de cet abonnement.

**Gestion des correctifs.** Si cette option est activée, le Centre de sécurité vérifie si des mises à jour critiques et de sécurité sont manquantes. Utilisez [les paramètres de stratégie de groupe] [ group-policy] mises à jour de hello VM tooenable automatique du système.

**Logiciel anti-programme malveillant.** Si cette option est activée, le Centre de sécurité vérifie si un logiciel anti-programme malveillant est installé. Vous pouvez également utiliser le logiciel anti-programme malveillant tooinstall à centre de sécurité à partir d’à l’intérieur de hello portail Azure.

**Opérations.** Utilisez [contrôle d’accès basé sur le rôle] [ rbac] (RBAC) toocontrol accès toohello Azure les ressources que vous déployez. RBAC vous permet d’attribuer des toomembers de rôles d’autorisation de votre équipe de DevOps. Par exemple, rôle de lecteur hello peut afficher les ressources Azure, mais pas créer, gérer ou les supprimer. Certains rôles sont des types de ressources Azure tooparticular spécifique. Par exemple, rôle de Machine virtuelle collaborateur hello peut redémarrer ou désallouer une machine virtuelle, réinitialiser le mot de passe administrateur hello, créer une machine virtuelle et ainsi de suite. D’autres [rôles RBAC intégrés][rbac-roles] peuvent être utiles dans cette architecture de référence, notamment [Utilisateur DevTest Lab][rbac-devtest] et [Collaborateur de réseau][rbac-network]. Toomultiple rôles peut être affecté à un utilisateur, et vous pouvez créer des rôles personnalisés pour d’autres autorisations affinées.

> [!NOTE]
> RBAC ne limite pas les actions hello réalisables par un utilisateur connecté à une machine virtuelle. Ces autorisations sont déterminées par le type de compte hello sur le système d’exploitation invité de hello.   
>
>

tooreset hello local mot de passe administrateur, exécutez hello `vm reset-access` commande CLI d’Azure.

```
azure vm reset-access -u <user> -p <new-password> <resource-group> <vm-name>
```

Utilisez [journaux d’audit] [ audit-logs] toosee mise en service des actions et autres événements de la machine virtuelle.

**Chiffrement des données.** Envisagez de [chiffrement de disque Azure] [ disk-encryption] si vous avez besoin tooencrypt hello du système d’exploitation et des disques de données.

## <a name="solution-deployment"></a>Déploiement de la solution

Un déploiement pour cette architecture de référence est disponible sur [GitHub][github-folder]. Il comprend un réseau virtuel, un groupe de sécurité réseau et une seule machine virtuelle. toodeploy hello architecture, procédez comme suit :

1. Cliquez avec le bouton droit sur bouton hello ci-dessous et sélectionnez soit « ouvrir le lien dans un nouvel onglet » ou « Ouvrir le lien dans une nouvelle fenêtre ».  
   [![Déployer tooAzure](../articles/guidance/media/blueprints/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Freference-architectures%2Fmaster%2Fguidance-compute-single-vm%2Fazuredeploy.json)
2. Une fois le lien de hello ouverts Bonjour portail Azure, vous devez entrer des valeurs pour certains des paramètres de hello :

   * Hello **groupe de ressources** nom est déjà défini dans le fichier de paramètres hello, sélectionnez **créer un nouveau** et entrez `ra-single-vm-rg` dans la zone de texte hello.
   * Région sélectionnez hello hello **emplacement** zone déroulante.
   * Ne modifiez pas hello **l’Uri racine modèle** ou hello **paramètre racine Uri** zones de texte.
   * Sélectionnez **windows** Bonjour **Type de système d’exploitation** zone déroulante.
   * Passez en revue les conditions générales hello, puis cliquez sur hello **J’accepte les termes du contrat de toohello et conditions susmentionnées** case à cocher.
   * Cliquez sur hello **achat** bouton.
3. Attendez que hello déploiement toocomplete.
4. fichiers de paramètres Hello incluent un nom d’utilisateur administrateur de codé en dur et le mot de passe, et il est fortement recommandé que vous modifiez immédiatement les deux. Cliquez sur hello ordinateur virtuel nommé `ra-single-vm0 `Bonjour portail Azure. Ensuite, cliquez sur **réinitialisation de mot de passe** Bonjour **prise en charge + dépannage** panneau. Sélectionnez **réinitialisation de mot de passe** Bonjour **Mode** zone de liste déroulante, puis sélectionnez un nouveau **nom d’utilisateur** et **mot de passe**. Cliquez sur hello **mise à jour** bouton toopersist hello nouveau nom d’utilisateur et mot de passe.

Pour plus d’informations sur les autres façons toodeploy cette architecture de référence, consultez le fichier Lisezmoi hello hello [machine virtuelle unique Guide][github-folder]] GitHub dossier.

## <a name="customize-hello-deployment"></a>Personnalisez le déploiement de hello
Si vous devez toochange hello déploiement toomatch à vos besoins, suivez les instructions de hello Bonjour [Lisez-moi][github-folder].

## <a name="next-steps"></a>Étapes suivantes
Pour augmenter la disponibilité, déployez au moins deux machines virtuelles derrière un équilibreur de charge. Pour plus d’informations, voir [Running multiple VMs on Azure (Exécution de plusieurs machines virtuelles sur Azure)][multi-vm].

<!-- links -->

[audit-logs]: https://azure.microsoft.com/en-us/blog/analyze-azure-audit-logs-in-powerbi-more/
[availability-set]:../articles/virtual-machines/windows/tutorial-availability-sets.md
[azure-cli]: /cli/azure/get-started-with-az-cli2
[azure-storage]: ../articles/storage/storage-introduction.md
[blob-snapshot]: ../articles/storage/storage-blob-snapshots.md
[blob-storage]: ../articles/storage/storage-introduction.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[cname-record]: https://en.wikipedia.org/wiki/CNAME_record
[data-disk]: ../articles/storage/storage-about-disks-and-vhds-windows.md
[disk-encryption]: ../articles/security/azure-security-disk-encryption.md
[enable-monitoring]: ../articles/monitoring-and-diagnostics/insights-how-to-use-diagnostics.md
[fqdn]:../articles/virtual-machines/windows/portal-create-fqdn.md
[github-folder]: http://github.com/mspnp/reference-architectures/tree/master/guidance-compute-single-vm
[group-policy]: https://technet.microsoft.com/en-us/library/dn595129.aspx
[log-collector]: https://azure.microsoft.com/en-us/blog/simplifying-virtual-machine-troubleshooting-using-azure-log-collector/
[manage-vm-availability]:../articles/virtual-machines/windows/manage-availability.md
[multi-vm]: ../articles/guidance/guidance-compute-multi-vm.md
[naming conventions]: ../articles/guidance/guidance-naming-conventions.md
[nsg]: ../articles/virtual-network/virtual-networks-nsg.md
[nsg-default-rules]: ../articles/virtual-network/virtual-networks-nsg.md#default-rules
[planned-maintenance]:../articles/virtual-machines/windows/planned-maintenance.md
[premium-storage]: ../articles/storage/storage-premium-storage.md
[rbac]: ../articles/active-directory/role-based-access-control-what-is.md
[rbac-roles]: ../articles/active-directory/role-based-access-built-in-roles.md
[rbac-devtest]: ../articles/active-directory/role-based-access-built-in-roles.md#devtest-labs-user
[rbac-network]: ../articles/active-directory/role-based-access-built-in-roles.md#network-contributor
[reboot-logs]: https://azure.microsoft.com/en-us/blog/viewing-vm-reboot-logs/
[resize-os-disk]:../articles/virtual-machines/windows/expand-os-disk.md
[Resize-VHD]: https://technet.microsoft.com/en-us/library/hh848535.aspx
[Resize virtual machines]: https://azure.microsoft.com/en-us/blog/resize-virtual-machines/
[resource-lock]: ../articles/resource-group-lock-resources.md
[resource-manager-overview]: ../articles/azure-resource-manager/resource-group-overview.md
[security-center]: https://azure.microsoft.com/en-us/services/security-center/
[select-vm-image]:../articles/virtual-machines/windows/cli-ps-findimage.md
[services-by-region]: https://azure.microsoft.com/en-us/regions/#services
[static-ip]: ../articles/virtual-network/virtual-networks-reserved-public-ip.md
[storage-account-limits]: ../articles/azure-subscription-service-limits.md#storage-limits
[storage-price]: https://azure.microsoft.com/pricing/details/storage/
[Utiliser le Centre de sécurité]: ../articles/security-center/security-center-get-started.md#use-security-center
[virtual-machine-sizes]: ../articles/virtual-machines/windows/sizes.md
[visio-download]: http://download.microsoft.com/download/1/5/6/1569703C-0A82-4A9C-8334-F13D0DF2F472/RAs.vsdx
[vm-disk-limits]: ../articles/azure-subscription-service-limits.md#virtual-machine-disk-limits
[vm-resize]:../articles/virtual-machines/linux/change-vm-size.md
[vm-sla]: https://azure.microsoft.com/support/legal/sla/virtual-machines
[vm-size-tables]: ../articles/virtual-machines/windows/sizes.md
[0]: ./media/guidance-blueprints/compute-single-vm.png "Architecture de machine virtuelle Windows unique dans Azure"
[readme]: https://github.com/mspnp/reference-architectures/blob/master/guidance-compute-single-vm
[blocks]: https://github.com/mspnp/template-building-blocks
