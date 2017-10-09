
>[!NOTE]
>Log Analytics s’appelait auparavant Operational Insights.
>
>

Hello suivant limites s’appliquent tooLog des ressources d’Analytique par abonnement :

| Ressource | Limite par défaut | Commentaires
| --- | --- | --- |
| Nombre d’espaces de travail gratuits par abonnement | 10 | Cette limite ne peut pas être augmentée. |
| Nombre d’espaces de travail payants par abonnement | N/A | Vous êtes limité par le nombre de hello des ressources au sein d’un groupe de ressources et nombre de groupes de ressources par abonnement | 


Hello suivant limites s’appliquent à espace de travail tooeach Analytique de journal :

|  | Gratuit | Standard | Premium | Standalone | OMS |
| --- | --- | --- | --- | --- | --- |
| Volume de données collecté par jour |500 MO<sup>1</sup> |Aucun |Aucun | Aucun | Aucun
| Période de rétention des données |7 jours |1 mois |12 mois | 1 mois<sup>2</sup> | 1 mois <sup>2</sup>|

<sup>1</sup> lorsque les clients atteignent leur limite de transfert de données quotidienne 500 Mo, analyse des données s’arrête et reprend au début de hello de hello le jour suivant. Les journées sont basées sur l’heure UTC.

<sup>2</sup> période de rétention des données hello pour hello autonome et des plans de tarification d’OMS peut être accrue too730 jours.

| Catégorie | Limites | Commentaires
| --- | --- | --- |
| API du collecteur de données | La taille maximale d’une publication est de 30 Mo<br>La taille maximale des valeurs de champ est de 32 Ko | Fractionner les volumes plus importants en plusieurs publications<br>Les champs de plus de 32 Ko de champs sont tronqués. |
| API de recherche | 5 000 enregistrements renvoyés pour des données non agrégées<br>500 000 enregistrements pour des données agrégées | Les données agrégées sont une recherche qui inclut hello `measure` commande
 
