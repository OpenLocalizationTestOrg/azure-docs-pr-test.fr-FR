


Cet article répond à certaines questions courantes poser des utilisateurs sur les machines virtuelles créées avec le modèle de déploiement classique hello.

## <a name="can-i-migrate-my-vm-created-in-hello-classic-deployment-model-toohello-new-resource-manager-model"></a>Puis-je migrer mes machines virtuelles créées dans hello déploiement classique modèle toohello nouveau gestionnaire de ressources du modèle ?
Oui. Pour obtenir des instructions sur la façon de toomigrate, consultez :

* [Migrer à partir de tooAzure classique Gestionnaire de ressources à l’aide d’Azure PowerShell](../articles/virtual-machines/windows/migration-classic-resource-manager-ps.md).
* [Migrer à partir de tooAzure classique Gestionnaire de ressources à l’aide d’Azure CLI](../articles/virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md).

## <a name="what-can-i-run-on-an-azure-vm"></a>Qu’est-il possible d’exécuter sur une machine virtuelle Azure ?
Tous les abonnés peuvent exécuter des logiciels serveur sur une machine virtuelle Azure. Vous pouvez exécuter des versions récentes de Windows Server, ainsi que diverses distributions de Linux. Pour les détails de prise en charge, consultez les liens suivants :

• Pour les machines virtuelles Windows : [Prise en charge logicielle du serveur Microsoft pour les machines virtuelles Microsoft Azure](http://go.microsoft.com/fwlink/p/?LinkId=393550)

• Pour les machines virtuelles Linux : [Linux dans des distributions prises en charge par Azure](http://go.microsoft.com/fwlink/p/?LinkId=393551)

Pour les images de client Windows, certaines versions de Windows 7 et Windows 8.1 sont les abonnés Azure tooMSDN disponibles et les abonnés MSDN développement et de paiement à l’utilisation de Test, pour les tâches de développement et de test. Pour plus d’informations, notamment des instructions et des limitations, voir [Images de client Windows pour les abonnés MSDN](https://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/).

## <a name="why-are-affinity-groups-being-deprecated"></a>Pourquoi les groupes d’affinités sont-ils déconseillés ?
Les groupes d’affinités sont un concept hérité du regroupement géographique des déploiements de service cloud et des comptes de stockage d’un client dans Azure. Ils ont été fournies à l’origine de performances du réseau d’ordinateur virtuel en ordinateur virtuel tooimprove dans les conceptions de réseau Azure hello anticipée. Ils également pris en charge version initiale de hello de réseaux virtuels (réseaux virtuels), qui ont été limités tooa petit ensemble de matériel dans une région.

réseau de Azure actuel Hello dans une région est conçue afin que les groupes d’affinités ne sont plus nécessaires. Les réseaux virtuels sont également présents à l’échelon régional, de sorte qu’aucun groupe d’affinités n’est requis en cas d’utilisation d’un réseau virtuel. En raison des améliorations de toothese, nous ne recommandons plus aux clients d’utiliser les groupes d’affinités, car ils peuvent être limitée dans certains scénarios. À l’aide de groupes d’affinités inutilement associe votre matériel toospecific de machines virtuelles qui limite les choix hello de tailles de machine virtuelle tooyou disponible. Cela peut également générer des erreurs liées à toocapacity lorsque vous essayez de tooadd nouvelles machines virtuelles si un matériel spécifique hello associé avec le groupe d’affinités de hello est saturé.

Groupe d’affinités fonctionnalités est déjà déconseillé dans le modèle de déploiement du Gestionnaire de ressources Azure hello et hello portail Azure. Pour le portail Azure classic de hello, nous allons désapprouve prise en charge pour créer des groupes d’affinités et créer des ressources de stockage qui sont un groupe d’affinité tooan épinglés. Vous n’avez pas besoin toomodify des services cloud existants qui utilisent un groupe d’affinités. Toutefois, n’utilisez pas de groupes d’affinités pour les nouveaux services cloud, sauf instruction contraire de la part d’un spécialiste du support Azure.

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Quelle quantité de stockage puis-je utiliser avec une machine virtuelle ?
Chaque disque de données peut être jusqu'à too1 to. nombre de Hello de disques de données que vous pouvez utiliser dépend de la taille de hello de machine virtuelle de hello. Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Un compte de stockage Azure fournit le stockage de disque de système d’exploitation hello et les disques de données. Chaque disque est un fichier .vhd stocké sous la forme d’un objet blob de pages. Pour plus d’informations sur la tarification, voir [Tarification – Stockage](http://go.microsoft.com/fwlink/p/?LinkId=396819).

## <a name="which-virtual-hard-disk-types-can-i-use"></a>Quels types de disque dur virtuel puis-je utiliser ?
Azure prend uniquement en charge les disques durs virtuels fixes au format VHD. Si vous avez un VHDX que vous souhaitez toouse dans Azure, vous devez toofirst le convertir en utilisant le Gestionnaire Hyper-V ou hello [convert-VHD](http://go.microsoft.com/fwlink/p/?LinkId=393656) applet de commande. Après cela, utilisez [Add-AzureVHD](https://msdn.microsoft.com/library/azure/dn495173.aspx) hello de tooupload d’applet de commande (en mode de gestion des services) compte de stockage tooa de disque dur virtuel dans Azure afin de pouvoir l’utiliser avec des machines virtuelles.

* Pour obtenir des instructions de Linux, consultez [création et téléchargement d’un disque dur virtuel qui contient de système d’exploitation Linux hello](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
* Pour obtenir des instructions de Windows, consultez [création et téléchargement d’un disque dur virtuel de Windows Server de tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="are-these-virtual-machines-hello-same-as-hyper-v-virtual-machines"></a>Sont que Hello de ces machines virtuelles identiques en tant qu’ordinateurs virtuels Hyper-V ?
De nombreuses manières, elles sont similaires ordinateurs virtuels Hyper-V de « Génération 1 », mais ils ne sont pas exactement hello même. Les deux types fournissent un matériel virtualisé, et les disques durs virtuels hello au format VHD sont compatibles. Cela signifie que vous pouvez les déplacer entre Hyper-V et Azure. Les trois différences principales qui surprennent parfois les utilisateurs d’Hyper-V sont :

* Machine virtuelle de console accès tooa ne fournit pas Azure. Il n’existe aucun moyen de tooaccess une machine virtuelle jusqu'à ce qu’il est fait démarrage.
* La plupart des [tailles](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) de machines virtuelles Azure ne comportent qu’une seule carte réseau virtuelle, ce qui signifie qu’elles ne peuvent donc avoir qu’une seule adresse IP externe. (hello A8 et A9 tailles utilisent une deuxième carte réseau pour la communication de l’application entre des instances dans certains scénarios limités).
* Les machines virtuelles Azure ne prennent pas en charge les fonctionnalités des machines virtuelles Hyper-V de deuxième génération. Pour plus d’informations sur ces fonctionnalités, consultez les articles [Virtual Machine Specifications for Hyper-V](http://technet.microsoft.com/library/dn592184.aspx) (Spécifications des machines virtuelles pour Hyper-V) et [Vue d’ensemble de machines virtuelles de Génération 2](https://technet.microsoft.com/library/dn282285.aspx).

## <a name="can-these-virtual-machines-use-my-existing-on-premises-networking-infrastructure"></a>Ces machines virtuelles peuvent-elles utiliser mon infrastructure réseau existante locale ?
Pour les ordinateurs virtuels créés dans le modèle de déploiement classique de hello, vous pouvez utiliser tooextend de réseau virtuel Azure de votre infrastructure existante. approche de Hello ressemble à configurer une filiale. Vous pouvez configurer et gérer des réseaux privés virtuels (VPN) dans Azure ainsi les connecter en toute sécurité tooon local infrastructure informatique. Pour plus d’informations, voir [Présentation du réseau virtuel](../articles/virtual-network/virtual-networks-overview.md).

Vous devez toospecify hello réseau hello toowhen toobelong de machine virtuelle vous créez la machine virtuelle de hello. Vous ne pouvez pas joindre un ordinateur virtuel tooa réseau virtuel. Toutefois, vous pouvez contourner ce problème en détachant hello disque dur virtuel (VHD) à partir de l’ordinateur virtuel existant de hello et réutilisez-la toocreate un nouvel ordinateur virtuel avec la configuration de mise en réseau hello souhaité.

## <a name="how-can-i-access--my-virtual-machine"></a>Comment puis-je accéder à ma machine virtuelle ?
Vous devez tooestablish un toolog de connexion à distance sur l’ordinateur virtuel de toohello à l’aide de connexion Bureau à distance pour une machine virtuelle Windows ou un Secure Shell (SSH) pour un VM Linux. Pour obtenir des instructions, consultez les liens suivants :

* [Comment tooLog sur tooa Machine virtuelle exécutant Windows Server](../articles/virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Un maximum de 2 connexions simultanées sont prises en charge, sauf si le serveur de hello est configuré comme un hôte de session des Services Bureau à distance.  
* [Comment tooLog sur tooa Machine virtuelle exécutant Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Par défaut, SSH autorise un maximum de 10 connexions simultanées. Vous pouvez augmenter ce nombre en modifiant le fichier de configuration hello.

Si vous rencontrez des problèmes avec le Bureau à distance ou SSH, installer et utiliser hello [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) problème d’extension toohelp correctif hello.

Pour les machines virtuelles Windows, les options supplémentaires incluent :

* Dans hello portail Azure classic, recherche hello machine virtuelle, puis cliquez sur **réinitialiser l’accès à distance** à partir de la barre de commandes hello.
* Révision [tooa de connexions de résoudre les problèmes de bureau à distance basé sur Windows Azure Virtual Machine](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Utilisez la communication à distance de Windows PowerShell tooconnect toohello machine virtuelle, ou créer des points de terminaison supplémentaires pour les autres toohello tooconnect de ressources machine virtuelle. Pour plus d’informations, consultez [comment tooSet des points de terminaison tooa Machine virtuelle](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Si vous êtes familiarisé avec Hyper-V, vous risquez de rechercher les un tooVMConnect similaire d’outil. Azure n’offre pas un outil similaire car l’ordinateur virtuel de console accès tooa n’est pas pris en charge.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-for-windows-or-devsdb1-for-linux-toostore-data"></a>Puis-je utiliser des données de toostore hello disque temporaire (hello lecteur D: pour Windows ou/dev/sdb1 pour Linux) ?
Vous ne devez pas utiliser les données de toostore hello disque temporaire (hello lecteur D: par défaut pour Windows, ou/dev/sdb1 pour Linux). Ils ne permettent qu’un stockage temporaire, vous risqueriez donc de perdre des données sans pouvoir les récupérer. Cela peut se produire lors de la machine virtuelle de hello déplace tooa autre ordinateur hôte. Redimensionnement d’un ordinateur virtuel, la mise à jour hello hôte ou une défaillance matérielle sur l’ordinateur hôte de hello est certaines des raisons hello qu'une machine virtuelle peuvent se déplacer.

## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Comment puis-je modifier hello lettre de lecteur hello temporaire disque ?
Sur une machine virtuelle Windows, vous pouvez modifier la lettre de lecteur hello par déplacement du fichier page hello et en réaffectant les lettres de lecteur, mais vous devez toomake que vous hello étapes dans un ordre spécifique. Pour obtenir des instructions, consultez [modifier la lettre de lecteur hello du disque temporaire de Windows hello](../articles/virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="how-can-i-upgrade-hello-guest-operating-system"></a>Comment puis-je mettre à niveau hello de systèmes d’exploitation ?
Hello mise à niveau du terme signifie généralement tooa mobile plus récent de votre système d’exploitation, tout en restant sur hello même matériel. Pour les machines virtuelles Azure, hello le processus de passage tooa diffère d’une version plus récente pour Linux et Windows :

* Pour les machines virtuelles Linux, utilisez les outils de gestion de package hello et les procédures appropriées pour la distribution de hello.
* Pour une machine virtuelle Windows, vous avez besoin d’un serveur de hello de toomigrate à l’aide de quelque chose comme hello outils de Migration de Windows Server. N’essayez pas système d’exploitation invité de hello tooupgrade résidant sur Azure. Il n’est pas pris en charge en raison de risques hello de perdre l’accès toohello virtual machine. Si des problèmes se produisent pendant la mise à niveau hello, vous risquez de perdre hello capacité toostart un bureau à distance session et ne serait pas en mesure de tootroubleshoot des problèmes de hello.

Pour plus d’informations générales sur les outils hello et les processus pour la migration d’un serveur Windows, consultez [tooWindows migrer des rôles et fonctionnalités serveur](http://go.microsoft.com/fwlink/p/?LinkId=396940).

## <a name="whats-hello-default-user-name-and-password-on-hello-virtual-machine"></a>Qu’est le nom d’utilisateur par défaut hello et un mot de passe sur l’ordinateur virtuel de hello ?
images Hello fournies par Azure n’ont pas préconfiguré nom d’utilisateur et mot de passe. Lorsque vous créez la machine virtuelle à l’aide d’une de ces images, vous devez tooprovide un nom d’utilisateur et un mot de passe, que vous allez utiliser toolog sur l’ordinateur virtuel de toohello.

Si vous avez oublié le mot de passe ou nom d’utilisateur hello et que vous avez installé hello Agent de machine virtuelle, vous pouvez installer et utiliser hello [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) problème d’extension toofix hello.

Informations supplémentaires :

* Pour les images de Linux hello, si vous utilisez hello portail Azure classic, « azureuser » est fournie sous la forme d’un nom d’utilisateur par défaut, mais vous pouvez le modifier à l’aide de « À partir de la galerie » au lieu de « Création rapide » en tant que machine virtuelle de hello moyen toocreate hello. À l’aide de « À partir de la galerie » vous permet également de décider si toouse un mot de passe, une clé SSH ou les deux toolog dans. Hello compte d’utilisateur est un utilisateur non privilégié qui dispose d’un accès « sudo » toorun privilégié des commandes. compte de Hello « root » est désactivé.
* Pour les images de Windows, vous devez tooprovide un nom d’utilisateur et mot de passe lorsque vous créez hello machine virtuelle. compte de Hello est ajouté toohello groupe d’administrateurs.

## <a name="can-azure-run-anti-virus-on-my-virtual-machines"></a>Azure peut-il exécuter un antivirus sur mes machines virtuelles ?
Azure offre plusieurs options pour les solutions antiviruss, mais est de tooyou toomanage. Par exemple, vous devrez peut-être un abonnement distinct pour les logiciels anti-programme malveillant, et vous aurez besoin de toodecide pour toorun des analyses et installer les mises à jour. Vous pouvez ajouter une prise en charge d’antivirus avec une extension de machine virtuelle pour Microsoft Antimalware, Symantec Endpoint Protection ou TrendMicro Deep Security Agent lors de la création d’une machine virtuelle Windows ou à un moment ultérieur. Hello Symantec et TrendMicro extensions vous permettent d’utiliser une version d’évaluation gratuite de durée limitée ou un abonnement d’entreprise existante. Microsoft Antimalware est gratuit. Pour plus d'informations, consultez les rubriques :

* [Comment tooinstall et configurer Symantec Endpoint Protection sur une machine virtuelle Azure](http://go.microsoft.com/fwlink/p/?LinkId=404207)
* [Comment tooinstall et configurer Trend Micro Deep Security en tant que Service sur une machine virtuelle Azure](http://go.microsoft.com/fwlink/p/?LinkId=404206)
* [Déploiement de solutions anti-programmes malveillants sur des machines virtuelles Azure (en anglais)](https://azure.microsoft.com/blog/2014/05/13/deploying-antimalware-solutions-on-azure-virtual-machines/)

## <a name="what-are-my-options-for-backup-and-recovery"></a>Quelles sont les options disponibles en matière de sauvegarde et de récupération d’urgence ?
Azure Backup est disponible en version préliminaire dans certaines régions. Pour plus d’informations, voir [Sauvegarde des machines virtuelles Azure](../articles/backup/backup-azure-vms.md). D’autres solutions sont disponibles auprès de partenaires certifiés. toofind ce qui est actuellement disponible, recherchez hello Azure Marketplace.

Une autre option consiste à snapshots toouse hello de stockage d’objets blob. toodo, vous devez tooshut vers le bas hello machine virtuelle avant toute opération impliquant un instantané d’objet blob. Cela vous permet d’écritures de données en attente et place le système de fichiers hello dans un état cohérent.

## <a name="how-does-azure-charge-for-my-vm"></a>À quel mode de facturation ma machine virtuelle est-elle soumise dans Azure ?
Azure facture un prix de toutes les heures en fonction de la taille et le système d’exploitation de machine virtuelle hello. Pour les heures entamées, Azure facture uniquement pour les minutes hello d’utilisation. Si vous créez hello machine virtuelle avec une image de machine virtuelle contenant certains logiciels préinstallés, des coûts horaires logiciels supplémentaires peuvent s’appliquer. Azure facture séparément pour le stockage du hello machine virtuelle système d’exploitation et des disques de données. Le stockage sur disque temporaire est gratuit.

Vous êtes facturé quand hello état de la machine virtuelle est en cours d’exécution ou arrêté, mais vous n’êtes pas facturé quand hello état de la machine virtuelle est arrêtée (désallouée). tooput une machine virtuelle dans hello arrêté (désalloué) d’état, effectuez l’une des manières suivantes les hello :

* Arrêtez ou supprimez hello VM hello portail Azure classic.
* Utilisez hello Stop-AzureVM applet de commande, disponible dans le module Azure PowerShell de hello.
* Utiliser l’opération d’arrêt du rôle de hello Bonjour API REST Service Management et spécifiez StoppedDeallocated pour l’élément PostShutdownAction de hello.

Pour plus d’informations, voir [Tarification des machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="will-azure-reboot-my-vm-for-maintenance"></a>Dois-je m’attendre à ce qu’Azure redémarre ma machine virtuelle aux fins de maintenance ?
Azure redémarre parfois votre machine virtuelle dans le cadre des mises à jour de maintenance normales et planifiées dans hello centres de données Azure.

Des événements de maintenance non planifiés peuvent se produire quand Azure détecte un problème matériel sérieux qui affecte votre machine virtuelle. Pour les événements non planifiés, Azure migre hello tooa intègre hôte d’ordinateur virtuel et redémarre hello machine virtuelle automatiquement.

Pour n’importe quel ordinateur virtuel autonome (c'est-à-dire hello machine virtuelle ne fait pas partie d’un ensemble de disponibilité), Azure notifie administrateur de Service de l’abonnement hello par courrier électronique au moins une semaine avant la maintenance planifiée, car hello machines virtuelles peut être redémarrée au cours de la mise à jour hello. Applications qui s’exécutent sur des machines virtuelles de hello peut rencontrer des temps d’arrêt.

Vous pouvez également utiliser hello portail Azure classic ou le journal de redémarrage d’Azure PowerShell tooview hello lorsque le redémarrage de hello s’est produite en raison de la maintenance de tooplanned. Pour plus d’informations, voir [Affichage des journaux de redémarrage de machines virtuelles (en anglais)](https://azure.microsoft.com/blog/2015/04/01/viewing-vm-reboot-logs/).

tooprovide redondance, placer deux ou plus de la même façon configuré des ordinateurs virtuels dans hello même groupe à haute disponibilité. Cela contribue à garantir qu’au moins une machine virtuelle est disponible pendant la maintenance, planifiée ou non. Azure garantit certains niveaux de disponibilité des machines virtuelles pour cette configuration. Pour plus d’informations, consultez [gérer la disponibilité hello des machines virtuelles](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="additional-resources"></a>Ressources supplémentaires
[À propos de Machines virtuelles Azure](../articles/virtual-machines/virtual-machines-linux-about.md)

[Créer et gérer des ordinateurs virtuels Linux avec hello CLI d’Azure](../articles/virtual-machines/linux/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Créer et gérer des machines virtuelles Windows avec le module Azure PowerShell](../articles/virtual-machines/windows/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

