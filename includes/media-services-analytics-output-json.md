travail de Hello génère un fichier de sortie JSON qui contient des métadonnées sur les faces détectés et de suivi. les métadonnées Hello incluent les coordonnées indiquant l’emplacement de hello des faces, ainsi que de face ID numéro indiquant hello suivi de cette personne. Les numéros d’identification face sont tooreset susceptible d’engendrer des circonstances quand un visage de face hello est perdu ou superposée dans le cadre de hello, aboutissant à certaines personnes plusieurs ID lors de l’attribution.

Hello JSON inclut hello suivant des attributs de sortie :

| Élément | Description |
| --- | --- |
| version |Cela fait référence version toohello Hello vidéo API. |
| index | (S’applique tooAzure Media Redactor) définit l’index de frame hello d’événement en cours de hello. |
| échelle de temps |« Cycles » par seconde de la vidéo de hello. |
| Offset |Il s’agit de décalage de temps hello pour les horodatages. Cette valeur sera toujours 0 dans la version 1.0 des API vidéo. Cette valeur est susceptible d’être modifiée dans les scénarios pris en charge ultérieurement. |
| taux de trames |Images par seconde de hello vidéo. |
| fragments |les métadonnées Hello sont mémorisé en bloc dans différents segments appelés fragments. Chaque fragment contient des valeurs de début (start), de durée (duration), un numéro d’intervalle et des événements (event). |
| start |Hello heure de début du premier événement de hello dans 'ticks'. |
| duration |longueur de Hello du fragment hello, dans « cycles ». |
| interval |intervalle de salutation de chaque entrée d’événement dans le fragment de hello, dans « cycles ». |
| événements |Chaque événement contient des faces hello détecté et suivies pendant cette durée. Il s’agit d’un tableau de tableau d’événements. tableau d’externe Hello représente un intervalle de temps. tableau interne de Hello se compose de 0 ou plusieurs événements qui se sont produits à ce stade dans le temps. Un crochet vide signifie [] qu’aucun visage n’a été détecté. |
| id |ID de Hello de type hello est en cours de suivi. Ce nombre peut être modifié par inadvertance si un visage n’est plus détecté. Une personne donnée doit être hello même ID tout au long de hello vidéo global, mais il ne peut pas être garantie échéance toolimitations dans l’algorithme de détection hello (occlusion, etc.). |
| x, y |Hello haut à gauche X et Y des coordonnées de face hello englobant dans une échelle normalisée de too1.0 0.0. <br/>-X et Y coordonnées sont relatif toolandscape toujours, donc si vous avez un portrait vidéo (ou envers, dans le cas de hello d’e/s), vous aurez tootranspose hello coordonnées en conséquence. |
| largeur, hauteur |largeur de Hello et la hauteur de la face hello englobant dans une échelle normalisée de too1.0 0.0. |
| facesDetected |Il se trouve à la fin de hello de résultats JSON de hello et résume nombre hello des faces cet algorithme hello détecté au cours de hello vidéo. Étant donné que hello ID peut être réinitialisé par inadvertance si un visage devient non détecté (par exemple, face est mis hors écran, il semble absent), ce nombre peut toujours différent hello véritable nombre de faces dans la vidéo de hello. |

