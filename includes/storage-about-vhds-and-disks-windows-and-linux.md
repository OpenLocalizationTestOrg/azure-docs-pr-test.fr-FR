
## <a name="about-vhds"></a>À propos des VHD

Hello disques durs virtuels utilisés dans Azure sont des fichiers .vhd stockés en tant qu’objets BLOB de pages dans un compte de stockage standard ou premium dans Azure. Pour des informations sur les objets blob de pages, consultez la page [Présentation des objets blob de blocs et des objets blob de pages](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs/). Pour plus d’informations sur le stockage Premium, consultez [High-performance premium storage and Azure VMs](../articles/storage/common/storage-premium-storage.md) (Stockage Premium hautes performances et machines virtuelles Azure).

Azure prend en charge hello format de disque dur virtuel de disque fixé. établit les format Hello fixée hello disque logique out linéairement dans le fichier de hello, donc ce décalage de disque X soit stocké au niveau du décalage de l’objet blob X. Un pied de page à fin hello d’objet blob de hello décrit les propriétés de hello Hello disque dur virtuel. Souvent, format fixe de hello gaspille de l’espace, car la plupart des disques ont de grandes plages inutilisées dans celles-ci. Toutefois, Azure stocke les fichiers .vhd dans un format épars, afin que vous bénéficiez des avantages de hello de deux hello fixe et disques dynamiques à hello même temps. Pour plus d’informations, consultez [Prise en main des disques durs virtuels](https://technet.microsoft.com/library/dd979539.aspx).

Tous les fichiers .vhd Azure que vous souhaitez toouse comme un disque de toocreate source ou les images sont en lecture seule. Lorsque vous créez un disque ou une image, Azure crée des copies de hello fichiers .vhd. Ces copies peuvent être en lecture seule ou lecture-écriture, selon la façon dont vous utilisez hello disque dur virtuel.

Lorsque vous créez une machine virtuelle à partir d’une image, Azure crée un disque de machine virtuelle hello qui est une copie du fichier de disque dur virtuel source hello. tooprotect contre la suppression accidentelle, Azure crée un bail sur tout fichier .vhd source qui a utilisé toocreate une image, un disque de système d’exploitation ou un disque de données.

Avant de pouvoir supprimer un fichier .vhd source, vous devez le bail de hello tooremove en supprimant hello disque ou l’image. toodelete un fichier .vhd qui est utilisé par un ordinateur virtuel comme un disque de système d’exploitation, vous pouvez supprimer hello machine virtuelle, disque de système d’exploitation hello et fichier .vhd de hello source à la fois par la suppression de machine virtuelle de hello et la suppression de tous les disques associés. Toutefois, la suppression d’un fichier .vhd qui constitue une source pour un disque de données requiert l’exécution de plusieurs étapes dans un ordre défini. Tout d’abord vous détachez le disque hello à partir de l’ordinateur virtuel de hello, puis supprimer hello disque, puis supprimez le fichier .vhd de hello.

> [!WARNING]
> Si vous supprimez un fichier .vhd source d’un stockage ou si vous supprimez votre compte de stockage, Microsoft ne pourra pas récupérer ces données pour vous.
> 

## <a name="types-of-disks"></a>Types de disques 

Les disques Azure sont conçus pour offrir une disponibilité de 99,999 %. Les disques Azure ont toujours fourni une durabilité de classe Entreprise pour les disques IaaS, avec un taux de défaillance annuel inégalé dans le secteur de zéro %.

Lorsque vous créez vos disques, vous avez le choix entre deux niveaux de performances : stockage Standard et stockage Premium. Deux types de disques, gérés et non gérés, sont également proposés pour l’un ou l’autre de ces niveaux de performances.


### <a name="standard-storage"></a>Stockage Standard 

Le stockage Standard s’appuie sur des disques durs et offre un stockage économique qui n’en est pas moins performant. Le stockage Standard peut être répliqué localement dans un centre de données ou être géoredondant avec des centres de données principal et secondaire. Pour plus d’informations sur la réplication du stockage, consultez [Réplication du stockage Azure](../articles/storage/common/storage-redundancy.md). 

Pour plus d’informations sur l’utilisation du stockage Standard avec des disques de machine virtuelle, consultez [Standard Storage and Disks](../articles/storage/common/storage-standard-storage.md) (Stockage Standard et disques).

### <a name="premium-storage"></a>Stockage Premium 

Le stockage Premium s’appuie sur des disques SSD afin d’assurer de hautes performances et une faible latence pour les machines virtuelles qui exécutent des charges de travail nécessitant de nombreuses E/S. Vous pouvez utiliser le stockage Premium avec les machines virtuelles Azure de série DS, DSv2, GS, Ls, ou FS. Pour plus d’informations, consultez [Stockage Premium](../articles/storage/common/storage-premium-storage.md).

### <a name="unmanaged-disks"></a>Disques non gérés

Les disques non managées sont type traditionnel de hello de disques qui ont été utilisés par les ordinateurs virtuels. Avec ces éléments, vous créez votre propre compte de stockage et spécifiez ce compte de stockage lorsque vous créez le disque de hello. Vous avez toomake que vous ne placez trop de disques hello même compte de stockage, car vous pourriez dépasser hello [objectifs d’évolutivité](../articles/storage/common/storage-scalability-targets.md) hello compte de stockage (20 000 e/s, par exemple), ce qui entraîne hello limitées de machines virtuelles. Avec des disques non managés, vous devez toofigure utiliser dont toomaximize hello utilise un ou plusieurs comptes tooget hello meilleures des performances de stockage en dehors de vos machines virtuelles.

### <a name="managed-disks"></a>Disques gérés 

Géré handles disques stockage de hello compte pour vous la création et la gestion en arrière-plan de hello et permet de s’assurer que vous n’avez pas tooworry sur les limites d’extensibilité hello hello du compte de stockage. Vous spécifiez simplement taille du disque hello et niveau de performance hello (Standard/Premium) et Azure crée et gère les disques de hello pour vous. Même lorsque vous ajoutez des disques ou évoluer hello machine virtuelle, vous n’avez tooworry sur le stockage hello utilisé. 

Vous pouvez également gérer vos images personnalisées dans un compte de stockage par région Azure et les utiliser toocreate des centaines d’ordinateurs virtuels dans hello même abonnement. Pour plus d’informations sur les disques gérés, consultez hello [vue d’ensemble de disques gérés](../articles/virtual-machines/windows/managed-disks-overview.md).

Nous vous recommandons d’utiliser des disques de Azure géré pour les nouvelles machines virtuelles, et convertir vos disques de toomanaged de disques non managé précédente, parti tootake Hello de nombreuses fonctionnalités disponibles dans les disques gérés.

### <a name="disk-comparison"></a>Comparaison des disques

Hello tableau suivant fournit une comparaison de Visual Studio Standard de la prime pour les deux managés et toohelp disques vous décidez quelles toouse.

|    | Disque Premium Azure | Disque Standard Azure |
|--- | ------------------ | ------------------- |
| Type de disque | SSD (Solid State Drive) | Disques durs  |
| Vue d'ensemble  | Stockage hautes performances et à faible latence sur disque SSD pour les machines virtuelles qui exécutent des charges de travail nécessitant de nombreuses E/S ou qui hébergent un environnement de production stratégique | Stockage économique sur disque dur pour les machines virtuelles utilisées à des fins de développement/test |
| Scénario  | Charges de travail de production et sensibles aux performances | Développement/test, non stratégique, <br>accès peu fréquent |
| Taille du disque | P4 : 32 Go (Disques gérés uniquement)<br>P6 : 64 Go (Disques gérés uniquement)<br>P10 : 128 Go<br>P20 : 512 Go<br>P30 : 1 024 Go<br>P40 : 2 048 GO<br>P50 : 4095 GO | Disques non gérés : 1 Go – 4 To (4095 GO) <br><br>Disques gérés :<br> S4 : 32 Go <br>S6 : 64 Go <br>S10 : 128 Go <br>S20 : 512 Go <br>S30 : 1 024 Go <br>S40 : 2 048 GO<br>S50 : 4095 GO| 
| Débit max. par disque | 250 Mo/s | 60 Mo/s | 
| Nb max. d’E/S par seconde par disque | 7 500 E/S PAR SECONDE | 500 E/S par seconde | 

