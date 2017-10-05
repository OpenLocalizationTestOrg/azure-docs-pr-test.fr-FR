Le travail génère un fichier de sortie JSON qui contient des métadonnées sur les visages détectés et suivis. Les métadonnées incluent des coordonnées indiquant l’emplacement des visages, mais aussi un numéro d’identification pour chaque visage, indiquant le suivi de cette personne. Les numéros d’identification des visages peuvent être réinitialisés dans des cas où le visage filmé de face sort de l’image ou si un élément vient se superposer ; certaines personnes peuvent ainsi se voir attribuer plusieurs identifiants.

Le fichier JSON de sortie contient les attributs suivants :

| Élément | Description |
| --- | --- |
| version |Cela vaut pour la version de l’API vidéo. |
| index | (S’applique uniquement à Azure Media Redactor) définit l’index d’image de l’événement actuel. |
| échelle de temps |« Cycles » par seconde de la vidéo. |
| Offset |Le décalage des horodatages. Cette valeur sera toujours 0 dans la version 1.0 des API vidéo. Cette valeur est susceptible d’être modifiée dans les scénarios pris en charge ultérieurement. |
| taux de trames |Images par seconde de la vidéo. |
| fragments |Les métadonnées sont mémorisées dans différents segments appelés fragments. Chaque fragment contient des valeurs de début (start), de durée (duration), un numéro d’intervalle et des événements (event). |
| start |L’heure de début du premier événement en « cycles ». |
| duration |La durée du fragment en « cycles ». |
| interval |L’intervalle de chaque entrée d’événement dans le fragment en « cycles ». |
| événements |Chaque événement contient les visages détectés et suivis pendant cette durée. Il s’agit d’un tableau de tableau d’événements. Le tableau externe représente un intervalle de temps. Le tableau interne se compose de 0 événement ou plus ayant eu lieu à ce moment précis. Un crochet vide signifie [] qu’aucun visage n’a été détecté. |
| id |L’ID du visage suivi. Ce nombre peut être modifié par inadvertance si un visage n’est plus détecté. Un individu donné devrait avoir le même ID tout au long de la vidéo, mais cela ne peut être garanti en raison des limitations de l’algorithme de détection (occlusion, etc.). |
| x, y |Les coordonnées du coin supérieur et gauche X et Y du cadre de limitation du visage sur une échelle normalisée de 0,0 à 1,0. <br/>-Les coordonnées X et Y sont toujours configurées selon un format paysage ; si la vidéo est en format portrait (ou à l’envers, dans le cas d’iOS), vous devrez transposer les coordonnées en conséquence. |
| largeur, hauteur |La largeur et la hauteur du cadre de limitation du visage sur une échelle normalisée de 0,0 à 1,0. |
| facesDetected |Cet élément se trouve à la fin des résultats JSON et résume le nombre de visages que l’algorithme a détectés au cours de la vidéo. Étant donné que les identifiants peuvent être réinitialisés par inadvertance si un visage n’est plus détecté (par exemple, un visage qui sort de l’image, qui regarde ailleurs), ce nombre peut ne pas refléter le nombre réel de visages dans la vidéo. |

