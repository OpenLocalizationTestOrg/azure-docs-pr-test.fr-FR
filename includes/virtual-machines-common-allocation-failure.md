
Si votre problème Azure n’est pas abordé dans cet article, visitez hello [forums Azure sur MSDN et le débordement de pile](https://azure.microsoft.com/support/forums/). Vous pouvez publier votre problème sur ces forums ou too@AzureSupport sur Twitter. En outre, vous pouvez entrer une demande de support Azure en sélectionnant **obtenir un support technique** sur hello [prise en charge Azure](https://azure.microsoft.com/support/options/) site.

## <a name="general-troubleshooting-steps"></a>Étapes de dépannage générales
### <a name="troubleshoot-common-allocation-failures-in-hello-classic-deployment-model"></a>Résoudre les échecs d’allocation de courants dans le modèle de déploiement classique de hello
Ces étapes peuvent aider à résoudre de nombreux échecs d’allocation survenant au niveau des machines virtuelles :

* Redimensionnez la taille de machine virtuelle de l’autre tooa hello machine virtuelle.<br>
    Cliquez sur **Parcourir tout** > **Machines virtuelles (classiques)** > votre machine virtuelle > **Paramètres** > **Taille**. Pour des instructions détaillées, consultez [redimensionnement de la machine virtuelle de hello](https://msdn.microsoft.com/library/dn168976.aspx).
* Supprimer toutes les machines virtuelles à partir du service de cloud computing hello et recréer les machines virtuelles.<br>
    Cliquez sur **Parcourir tout** > **Machines virtuelles (classiques)** > votre machine virtuelle > **Supprimer**. Ensuite, cliquez sur **Nouveau** > **Calcul** > [image de la machine virtuelle].

### <a name="troubleshoot-common-allocation-failures-in-hello-azure-resource-manager-deployment-model"></a>Résoudre les échecs d’allocation de courants dans le modèle de déploiement du Gestionnaire de ressources Azure hello
Ces étapes peuvent aider à résoudre de nombreux échecs d’allocation survenant au niveau des machines virtuelles :

* Arrêter (désallouer) toutes les machines virtuelles dans hello disponibilité même définir, puis redémarrez chacun d’eux.<br>
    toostop : cliquez sur **groupes de ressources** > votre groupe de ressources > **ressources** > votre jeu de disponibilité > **virtuels** > votre machine virtuelle >  **Arrêter**.
  
    Une fois que tous les ordinateurs virtuels est arrêté, sélectionnez hello première machine virtuelle et cliquez sur **Démarrer**.

## <a name="background-information"></a>Informations contextuelles
### <a name="how-allocation-works"></a>Fonctionnement de l’allocation
serveurs Hello dans les centres de données Azure sont partitionnés en clusters. En règle générale, une demande d’allocation est tentée dans plusieurs clusters, mais il est possible que certaines contraintes à partir de la demande d’allocation hello force la demande de hello tooattempt hello plateforme Azure dans un seul cluster. Dans cet article, nous l’appellerons toothis en tant que « cluster tooa épinglés. » Le diagramme 1 ci-dessous illustre les cas de hello d’une allocation normale est tentée dans plusieurs clusters. Figure 2 illustre les cas de hello d’une allocation qui a épinglé tooCluster 2 car il s’agit où hello existant du Cloud Service CS_1 haute disponibilité est hébergé.
![Schéma d’allocation](./media/virtual-machines-common-allocation-failure/Allocation1.png)

### <a name="why-allocation-failures-happen"></a>Raisons des échecs d’une allocation
Lorsqu’une demande d’allocation est épinglé tooa cluster, il existe un risque plus élevé d’échec toofind libérer des ressources, car le pool de ressources disponibles hello est plus petite. En outre, si votre demande d’allocation est épinglé tooa cluster, mais de type hello de ressource que vous avez demandée n’est pas pris en charge par ce cluster, votre demande échoue même si le cluster de hello a libérer des ressources. Diagramme 3 ci-dessous illustre les cas de hello où une allocation en attente échoue parce que le cluster de candidat uniquement hello n’a pas de libérer des ressources. Figure 4 illustre les cas de hello où une allocation en attente échoue parce que le cluster de candidat hello uniquement ne prend pas en charge hello demandé la taille de machine virtuelle, même si le cluster de hello a libérer des ressources.

![Échec d’allocation épinglée](./media/virtual-machines-common-allocation-failure/Allocation2.png)

## <a name="detailed-troubleshoot-steps-specific-allocation-failure-scenarios-in-hello-classic-deployment-model"></a>Détaillées dépanner des scénarios d’échec d’allocation spécifiques comme suit dans le modèle de déploiement classique de hello
Voici les scénarios courants d’allocation qui provoquent une toobe de demande d’allocation épinglée. Nous aborderons chaque scénario ultérieurement dans cet article.

* Redimensionner une machine virtuelle ou ajouter des machines virtuelles ou service cloud existant de rôle instances tooan
* Redémarrer des machines virtuelles partiellement arrêtées (désallouées)
* Redémarrer des machines virtuelles complètement arrêtées (désallouées)
* Déploiements en environnement intermédiaire ou de production (PaaS uniquement)
* Groupe d’affinités (proximité entre la machine virtuelle et le service)
* Réseau virtuel par groupe d’affinités

Lorsque vous recevez une erreur d’allocation, voir si un des scénarios hello décrites tooyour erreur d’application. Utilisez l’erreur d’allocation hello retourné par scénario correspondant du hello tooidentify plateforme Azure hello. Si votre demande est mis en attente, en supprimer certains hello épingle contraintes tooopen vos clusters demande toomore, augmentant ainsi les chances de succès de l’allocation d’hello.

En règle générale, tant que l’erreur de hello n’indique pas « hello demandé une taille de machine virtuelle n’est pas pris en charge », vous pouvez toujours réessayer ultérieurement, suffisamment de ressources ait été libérée dans hello cluster tooaccommodate votre demande. Si hello problème que hello demandé de taille de machine virtuelle n’est pas pris en charge, essayez une autre taille de machine virtuelle. Dans le cas contraire, hello seule option consiste à hello tooremove épinglage de contrainte.

Deux scénarios d’échec courants sont des groupes de tooaffinity connexes. Bonjour précédentes, un groupe d’affinités étaient utilisées tooprovide proximité tooVMs/service instances, ou tooenable utilisé hello la création d’un réseau virtuel. Avec l’introduction de hello de réseaux virtuels régionaux, groupes d’affinités ne sont plus requis toocreate un réseau virtuel. Avec la réduction de hello de latence du réseau dans l’infrastructure Azure, recommandation hello toouse les groupes d’affinités pour la proximité de la machine virtuelle/service a changé.

Diagramme 5 ci-dessous présente taxonomie hello de scénarios d’allocation hello (épinglé).
![Taxonomie d’une allocation épinglée](./media/virtual-machines-common-allocation-failure/Allocation3.png)

> [!NOTE]
> erreur Hello figurent dans chaque scénario d’allocation est une forme abrégée. Consultez toohello [recherche de chaîne d’erreur](#Error string lookup) pour les chaînes d’erreur détaillé.
> 
> 

## <a name="allocation-scenario-resize-a-vm-or-add-vms-or-role-instances-tooan-existing-cloud-service"></a>Scénario d’allocation : redimensionner une machine virtuelle ou d’ajouter les instances de rôle ou machines virtuelles tooan le service cloud existant
**Erreur**

Upgrade_VMSizeNotSupported ou GeneralError

**Cause de l’épinglage au cluster**

Une demande tooresize une machine virtuelle ou ajouter un ordinateur virtuel ou un service cloud existant rôle instance tooan a toobe émise au cluster d’origine hello qui héberge le service de cloud computing hello. Création d’un service cloud permet toofind de plateforme Windows Azure hello un autre cluster prend en charge la taille de machine virtuelle hello que vous avez demandées ou libérer des ressources.

**Solution de contournement**

Si l’erreur de hello est Upgrade_VMSizeNotSupported *, essayez une autre taille de machine virtuelle. Si une taille différente de la machine virtuelle n’est pas une option, mais s’il est acceptable toouse une autre adresse IP virtuelle (VIP), créez un nouveau toohost de service cloud hello du nouvel ordinateur virtuel et ajoutez les hello nouveau cloud service toohello réseau virtuel régional où hello des machines virtuelles existantes sont en cours d’exécution. Si votre service cloud existant n’utilise pas un réseau virtuel régional, vous pouvez toujours créer un réseau virtuel pour le nouveau service de cloud hello et puis connectez votre [réseau virtuel toohello nouveau réseau virtuel existant](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Pour plus d’informations, consultez [Réseaux virtuels régionaux](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Si l’erreur de hello est GeneralError *, il est probable que type hello de ressource (par exemple, une taille de machine virtuelle particulière) est pris en charge par cluster de hello, mais le cluster de hello n’a pas de libérer des ressources au moment de hello. Toohello similaires au-dessus de scénario, ajouter des ressources de calcul hello souhaité dans la création d’un nouveau service cloud (Notez le nouveau service de cloud hello a toouse une adresse IP virtuelle à l’autre) et utiliser un tooconnect de réseau virtuel régional vos services cloud.

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Scénario d’allocation : redémarrer des machines virtuelles partiellement arrêtées (désallouées)
**Erreur**

GeneralError*

**Cause de l’épinglage au cluster**

Une désallocation partielle signifie que vous avez arrêté (désalloué) une ou plusieurs machines virtuelles, mais pas toutes, dans un service cloud. Lorsque vous arrêtez (Désallouez) une machine virtuelle, hello associé les ressources sont libérées. Le redémarrage de cette machine virtuelle constitue donc une nouvelle demande d’allocation. Le redémarrage des machines virtuelles dans un service cloud partiellement libérée est équivalent tooadding service cloud existant de machines virtuelles tooan. demande d’allocation Hello a toobe émise au cluster d’origine hello qui héberge le service de cloud computing hello. Création d’un autre service cloud permet toofind de plateforme Windows Azure hello un autre cluster qui a des ressources gratuites ou prend en charge la taille de machine virtuelle hello que vous avez demandé.

**Solution de contournement**

S’il est acceptable toouse une autre adresse IP virtuelle delete hello arrêtée (désallouées) de machines virtuelles (mais conserver les disques hello associé) et ajouter hello machines virtuelles via un autre service cloud. Utilisez un réseau virtuel régional de tooconnect vos services cloud :

* Si votre service cloud existant utilise un réseau virtuel régional, ajoutez simplement hello nouveau cloud service toohello même réseau virtuel.
* Si votre service cloud existant n’utilise pas un réseau virtuel régional, créez un réseau virtuel pour le nouveau service de cloud hello, puis [connecter votre réseau virtuel toohello nouveau réseau virtuel](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Pour plus d’informations, consultez [Réseaux virtuels régionaux](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

## <a name="allocation-scenario-restart-fully-stopped-deallocated-vms"></a>Scénario d’allocation : redémarrer des machines virtuelles complètement arrêtées (désallouées)
**Erreur**

GeneralError*

**Cause de l’épinglage au cluster**

Une désallocation complète signifie que vous avez arrêté (désalloué) toutes les machines virtuelles d’un service cloud. Bonjour toorestart de demandes d’allocation ces machines virtuelles ont toobe émise au cluster d’origine hello qui héberge le service de cloud computing hello. Création d’un service cloud permet toofind de plateforme Windows Azure hello un autre cluster prend en charge la taille de machine virtuelle hello que vous avez demandées ou libérer des ressources.

**Solution de contournement**

S’il est acceptable toouse une adresse IP virtuelle à l’autre, hello delete d’origine arrêtée (désallouées) de machines virtuelles (mais conserver les disques hello associé) et supprimer le service de cloud correspondant hello (calcul hello associé ressources déjà publiées que lorsque vous avez arrêté (désalloué) Hello machines virtuelles). Créer un nouveau tooadd Bonjour de cloud service machines virtuelles précédent.

## <a name="allocation-scenario-stagingproduction-deployments-platform-as-a-service-only"></a>Scénario d’allocation : déploiements en environnement intermédiaire ou de production (PaaS uniquement)
**Erreur**

New_General* ou New_VMSizeNotSupported*

**Cause de l’épinglage au cluster**

Hello mise en lots de déploiement et le déploiement de production hello d’un service cloud est hébergé dans hello même cluster. Lorsque vous ajoutez le deuxième déploiement de hello, demande d’allocation hello correspondant sera tentée Bonjour même cluster héberge hello premier déploiement.

**Solution de contournement**

Supprimer le premier déploiement de hello et service de cloud d’origine hello et redéployer le service de cloud computing hello. Cette action peut se retrouver premier déploiement de hello dans un cluster qui a des deux déploiements suffisamment toofit de libérer des ressources ou dans un cluster qui prend en charge des tailles de machine virtuelle hello que vous avez demandé.

## <a name="allocation-scenario-affinity-group-vmservice-proximity"></a>Scénario d’allocation : groupe d’affinités (proximité entre la machine virtuelle et le service)
**Erreur**

New_General* ou New_VMSizeNotSupported*

**Cause de l’épinglage au cluster**

N’importe quelle ressource de calcul attribué tooan le groupe d’affinités est liée tooone cluster. Nouvelles demandes de ressources de calcul dans ce groupe d’affinités sont essayés dans hello où se trouvent les ressources existantes hello du même cluster. Cela est vrai si hello nouvelles ressources sont créées via un service cloud ou via un service cloud existant.

**Solution de contournement**

Si un groupe d’affinités n’est pas nécessaire, n’utilisez pas de groupe d’affinités ou regroupez vos ressources de calcul dans plusieurs groupes d’affinités.

## <a name="allocation-scenario-affinity-group-based-virtual-network"></a>Scénario d’allocation : réseau virtuel par groupe d’affinités
**Erreur**

New_General* ou New_VMSizeNotSupported*

**Cause de l’épinglage au cluster**

Avant l’introduction des réseaux virtuels régionaux, vous étiez tooassociate requis un réseau virtuel avec un groupe d’affinités. Par conséquent, les ressources de calcul placées dans un groupe d’affinités sont liés par hello les mêmes contraintes comme décrit dans hello « scénario de répartition : le groupe d’affinités (proximité de la machine virtuelle/service) » ci-dessus. ressources de calcul Hello sont liés tooone cluster.

**Solution de contournement**

Si vous n’avez pas besoin d’un groupe d’affinités, créez un réseau virtuel régional pour hello nouvelles ressources que vous souhaitez ajouter, puis [connecter votre réseau virtuel toohello nouveau réseau virtuel](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Pour plus d’informations, consultez [Réseaux virtuels régionaux](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Vous pouvez également [migrer votre réseau virtuel régional basée sur le groupe d’affinités de réseau virtuel tooa](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), puis ajoutez de nouveau les ressources hello souhaité.

## <a name="detailed-troubleshooting-steps-specific-allocation-failure-scenarios-in-hello-azure-resource-manager-deployment-model"></a>Scénarios d’échec d’allocation spécifiques comme suit dans le modèle de déploiement du Gestionnaire de ressources Azure hello de dépannage détaillées
Voici les scénarios courants d’allocation qui provoquent une toobe de demande d’allocation épinglée. Nous aborderons chaque scénario ultérieurement dans cet article.

* Redimensionner une machine virtuelle ou ajouter des machines virtuelles ou service cloud existant de rôle instances tooan
* Redémarrer des machines virtuelles partiellement arrêtées (désallouées)
* Redémarrer des machines virtuelles complètement arrêtées (désallouées)

Lorsque vous recevez une erreur d’allocation, voir si un des scénarios hello décrites tooyour erreur d’application. Utilisez l’erreur d’allocation hello retourné par scénario correspondant du hello tooidentify plateforme Azure hello. Si votre demande est épinglé tooan les cluster existant, en supprimer certains hello épingle contraintes tooopen vos clusters demande toomore, augmentant ainsi les chances de succès de l’allocation d’hello.

En règle générale, tant que l’erreur de hello n’indique pas « hello demandé une taille de machine virtuelle n’est pas pris en charge », vous pouvez toujours réessayer ultérieurement, suffisamment de ressources ait été libérée dans hello cluster tooaccommodate votre demande. Si hello problème que hello demandé de taille de machine virtuelle n’est pas pris en charge, voir ci-dessous pour les solutions de contournement.

## <a name="allocation-scenario-resize-a-vm-or-add-vms-tooan-existing-availability-set"></a>Scénario d’allocation : redimensionner une machine virtuelle ou ajouter des machines virtuelles tooan à haute disponibilité existant
**Erreur**

Upgrade_VMSizeNotSupported* ou GeneralError*

**Cause de l’épinglage au cluster**

Une demande tooresize une machine virtuelle ou ajouter un tooan de machine virtuelle existante à haute disponibilité a toobe émise au cluster d’origine hello qui héberge le groupe à haute disponibilité existant hello. Création d’un ensemble de disponibilité permet toofind de plateforme Windows Azure hello un autre cluster prend en charge la taille de machine virtuelle hello que vous avez demandées ou libérer des ressources.

**Solution de contournement**

Si l’erreur de hello est Upgrade_VMSizeNotSupported *, essayez une autre taille de machine virtuelle. Si l’utilisation d’une autre taille de machine virtuelle n’est pas une option, arrêtez tous les ordinateurs virtuels dans le groupe à haute disponibilité hello. Vous pouvez ensuite modifier la taille de machine virtuelle hello qui alloue hello VM tooa cluster qui prend en charge hello hello souhaité de taille de machine virtuelle.

Si l’erreur de hello est GeneralError *, il est probable que type hello de ressource (par exemple, une taille de machine virtuelle particulière) est pris en charge par cluster de hello, mais le cluster de hello n’a pas de libérer des ressources au moment de hello. Si hello machine virtuelle peut faire partie d’un ensemble différent de disponibilité, créer une machine virtuelle dans un ensemble différent de disponibilité (Bonjour même région). Ce nouvel ordinateur virtuel peut ensuite être ajouté à toohello même réseau virtuel.  

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Scénario d’allocation : redémarrer des machines virtuelles partiellement arrêtées (désallouées)
**Erreur**

GeneralError*

**Cause de l’épinglage au cluster**

Une désallocation partielle signifie que vous avez arrêté (désalloué) une ou plusieurs machines virtuelles, mais pas toutes, dans un groupe à haute disponibilité. Lorsque vous arrêtez (Désallouez) une machine virtuelle, hello associé les ressources sont libérées. Le redémarrage de cette machine virtuelle constitue donc une nouvelle demande d’allocation. Le redémarrage des machines virtuelles dans un ensemble de disponibilité partiellement libérée est équivalent tooadding disponibilité de machines virtuelles tooan existante définie. demande d’allocation Hello a toobe émise au cluster d’origine hello qui héberge le groupe à haute disponibilité existant hello.

**Solution de contournement**

Arrêtez tous les ordinateurs virtuels hello groupe à haute disponibilité avant le redémarrage hello premier. Vous pourrez ainsi effectuer une nouvelle tentative d’allocation et sélectionner un nouveau cluster ayant une capacité disponible.

## <a name="allocation-scenario-restart-fully-stopped-deallocated"></a>Scénario d’allocation : redémarrer des machines virtuelles complètement arrêtées (désallouées)
**Erreur**

GeneralError*

**Cause de l’épinglage au cluster**

Une désallocation complète signifie que vous avez arrêté (désalloué) toutes les machines virtuelles d’un groupe à haute disponibilité. demande d’allocation Hello toorestart ces machines virtuelles cible tous les clusters qui prennent en charge hello taille souhaitée.

**Solution de contournement**

Sélectionnez un nouveau tooallocate de taille de machine virtuelle. Si cette opération ne fonctionne pas, réessayez ultérieurement.

## <a name="error-string-lookup"></a>Recherche de chaîne d’erreur
**New_VMSizeNotSupported***

« hello VM taille (ou une combinaison de tailles de machine virtuelle) requis par ce déploiement ne peut pas être configuré en raison de contraintes de demande toodeployment. Si possible, essayez de relâcher les contraintes telles que les liaisons de réseau virtuel, déploiement de service tooa hébergé sans aucun autre déploiement qu’il contient et le déploiement de l’affinité de différents tooa groupe ou sans groupe d’affinités, ou essayez tooa autre région. »

**New_General***

« L’allocation a échoué ; contraintes toosatisfy impossible dans la demande. Hello nouveau déploiement de service demandée n’est liée tooan affinité du groupe, ou elle cible un réseau virtuel ou il existe un déploiement sous ce service hébergé. Chacune de ces conditions contraint hello nouveau déploiement toospecific Azure ressources. Veuillez réessayer plus tard ou essayez de réduire la taille de machine virtuelle hello ou le nombre d’instances de rôle. Ou bien, si possible, supprimez les contraintes susmentionnés hello ou essayez de déployer tooa autre région. »

**Upgrade_VMSizeNotSupported***

« Déploiement de hello tooupgrade impossible. Hello demandé la taille de machine virtuelle XXX n’est peut-être pas disponible dans les ressources hello prenant en charge le déploiement existant de hello. Réessayez plus tard, utilisez une autre taille de machine virtuelle ou diminuez le nombre d’instances de rôle, ou créez un déploiement dans un service hébergé, avec une liaison à un nouveau groupe d’affinités ou sans liaison de groupe d’affinités. »

**GeneralError***

« serveur de hello a rencontré une erreur interne. Veuillez réessayer la demande de hello ». Ou « Échec tooproduce une allocation pour le service de hello. »

