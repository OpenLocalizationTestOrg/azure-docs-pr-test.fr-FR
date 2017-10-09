<!--author=alkohli last changed: 12/15/15-->

| Identificateur de la limite | Limite | Commentaires |
| --- | --- | --- |
| Nombre maximal d'informations d'identification du compte de stockage |64 | |
| Nombre maximal de conteneurs de volumes |64 | |
| Nombre maximal de volumes |255 | |
| Nombre maximal de planifications par modèle de bande passante |168 |Une planification pour toutes les heures, tous les jours de semaine de hello (24 * 7). |
| Taille maximale d'un volume à plusieurs niveaux sur les appareils physiques |64 To pour 8100 et 8600 |8100 et 8600 sont des appareils physiques. |
| Taille maximale d'un volume à plusieurs niveaux sur les appareils virtuels dans Azure |30 To pour 8010  <br></br> 64 To pour 8020 |8010 et 8020 sont des appareils virtuels dans Azure qui utilisent le stockage Standard et Premium respectivement. |
| Taille maximale d'un volume épinglé localement sur les appareils physiques |9 To pour 8100  <br></br> 24 To pour 8600 |8100 et 8600 sont des appareils physiques. |
| Nombre maximal de connexions iSCSI |512 | |
| Nombre maximal de connexions iSCSI à partir d'initiateurs |512 | |
| Nombre maximal d'enregistrements de contrôle d'accès par appareil |64 | |
| Nombre maximal de volumes par stratégie de sauvegarde |24 | |
| Nombre maximal de sauvegardes conservées par stratégie de sauvegarde |64 | |
| Nombre maximal de planifications par stratégie de sauvegarde |10 | |
| Nombre maximal d'instantanés de n'importe quel type pouvant être conservés par volume |256 |Cela inclut les instantanés locaux et les instantanés cloud. |
| Nombre maximal d'instantanés pouvant être présents dans n'importe quel appareil |10 000 | |
| Nombre maximal de volumes pouvant être traités en parallèle pour sauvegarder, restaurer ou cloner |16 |<ul><li>S’il existe plus de 16 volumes, ils sont traités séquentiellement à mesure que des emplacements se libèrent.</li><li>De nouvelles sauvegardes de cloné ou un volume hiérarchisé restauré ne peut pas se produire jusqu'à ce que hello est terminée. Toutefois, pour un volume local, les sauvegardes sont autorisées après que hello volume est en ligne.</li></ul> |
| Temps de récupération d'un clone et d'une restauration pour les volumes à plusieurs niveaux |< 2 minutes |<ul><li>volume de Hello est rendue disponible dans les 2 minutes d’opération de restauration ou de clonage, quelle que soit la taille du volume hello.</li><li>performances du volume Hello pourront être initialement inférieures à la normale, comme la plupart des données de hello et les métadonnées se trouvent toujours dans le cloud de hello. Les performances peuvent augmenter en tant que flux de données à partir de l’appareil StorSimple hello cloud toohello.</li><li>Hello temps total toodownload métadonnées dépendent hello alloué la taille du volume. Métadonnées sont automatiquement placées dans appareil hello en arrière-plan hello au taux de hello de 5 minutes par To de données de volume alloué. Cette vitesse est affectée par le cloud de toohello de la bande passante Internet.</li><li>Hello restauration ou l’opération de clonage est terminée quand toutes les métadonnées hello sont sur le périphérique de hello.</li><li>Opérations de sauvegarde ne peut pas être effectuées jusqu'à ce que la restauration de hello ou opération de clonage est terminée. |
| Temps de récupération d'une restauration pour les volumes épinglés localement |< 2 minutes |<ul><li>volume de Hello est rendue disponible dans les 2 minutes hello d’opération de restauration, quelle que soit la taille du volume hello.</li><li>performances du volume Hello pourront être initialement inférieures à la normale, comme la plupart des données de hello et les métadonnées se trouvent toujours dans le cloud de hello. Les performances peuvent augmenter en tant que flux de données à partir de l’appareil StorSimple hello cloud toohello.</li><li>Hello temps total toodownload métadonnées dépendent hello alloué la taille du volume. Métadonnées sont automatiquement placées dans appareil hello en arrière-plan hello au taux de hello de 5 minutes par To de données de volume alloué. Cette vitesse est affectée par le cloud de toohello de la bande passante Internet.</li><li>Contrairement aux volumes hiérarchisés, dans les cas de hello de volumes attachés localement, les données de volume hello sont également téléchargées localement sur l’appareil de hello. opération de restauration Hello est terminée lorsque toutes les données de volume hello a été placée toohello appareil.</li><li>opérations de restauration Hello peut s’avérer longues et hello total toocomplete hello restauration dépend de la taille de hello du volume de local hello configuré, votre bande passante Internet et des hello des données sur l’appareil de hello existantes. Opérations de sauvegarde sur le volume de hello attaché localement sont autorisées pendant que l’opération de restauration hello est en cours d’exécution. |
| Disponibilité de la restauration légère |Dernier basculement | |
| Débit maximal du client en lecture/écriture (quand il est traité depuis le niveau SSD de hello) * |920/720 Mo/s avec une seule interface réseau de 10 Gigabit Ethernet |Les too2x avec MPIO et deux interfaces réseau. |
| Débit maximal du client en lecture/écriture (quand il est traité à partir de la couche de disque dur hello) * |120/250 Mo/s | |
| Débit maximal du client en lecture/écriture (quand il est traité depuis le niveau cloud hello) * |11/41 Mo/s |Le débit de lecture dépend de si les clients génèrent et conservent une profondeur de file d’attente d’E/S suffisante. |

&#42; Le débit maximal par type d’E/S a été mesuré avec des scénarios de lecture et d’écriture de 100 pour cent. Le débit réel peut être inférieur et varie en fonction du mélange d’E/S et des conditions réseau.

