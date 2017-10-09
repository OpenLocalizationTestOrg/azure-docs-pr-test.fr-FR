Hello tableau suivant décrit chacun des hello principaux quotas, limites, valeurs par défaut et accélérateurs dans Azure Scheduler.

| Ressource | Description de la limite |
| --- | --- |
| **Taille du travail** |La taille maximale du travail est de 16 Ko. Si une commande PUT ou PATCH génère un travail qui dépasse ces limites, un code d'état 400 demande incorrecte est retourné. |
| **Taille d'URL de la requête** |Taille maximale des URL de demande hello est 2 048 caractères. |
| **Taille de l'en-tête d'agrégat** |La taille maximale de l'en-tête d'agrégat est de 4 096 caractères. |
| **Nombre d'en-têtes** |Le nombre maximal d'en-têtes est 50. |
| **Taille du corps** |La taille maximale du corps est 8 192 caractères. |
| **Période de récurrence** |La période de récurrence maximale est 18 mois. |
| **Heure de toostart** |Maximum « toostart heure » est 18 mois. |
| **Historique des travaux** |Le corps de réponse maximal stocké dans l'historique des travaux est 2 048 octets. |
| **Fréquence** |quota de fréquence maximal Hello par défaut est 1 heure dans une collection de travaux gratuite et 1 minute dans une collection de travaux standard. fréquence maximale de Hello est configurable sur un toobe de collection de travaux inférieur hello maximale. Tous les travaux dans la collection de tâches hello sont valeur hello limité sur la collection de tâches hello. Si vous essayez de toocreate un travail avec une fréquence supérieure à la fréquence maximale sur une collection de tâches hello hello la demande échoue avec un code d’état 409 conflit. |
| **Travaux** |quota maximal de travaux de valeur par défaut Hello est 5 travaux dans une collection de travaux gratuite et 50 dans une collection de travaux standard. nombre maximal de Hello de travaux est configurable sur une collection de travaux. Tous les travaux dans la collection de tâches hello sont valeur hello limité sur la collection de tâches hello. Si vous essayez de toocreate plus de travaux que le quota maximal des tâches de hello, puis demande de hello échoue avec un code d’état 409 conflit. |
| **Collections de travaux** |Le nombre maximal de collections de travaux par abonnement est de 200 000. |
| **Conservation de l'historique des travaux** |Historique des travaux est conservé pour les mois de too2 ou des toohello dernières exécutions de 1000. |
| **Conservation des travaux terminés et ayant généré une erreur** |Les travaux terminés et ayant généré une erreur sont conservés pendant 60 jours. |
| **Délai d'expiration** |Il existe un délai d’expiration de requête (non modifiable) statique de 60 secondes pour les actions HTTP. Pour les opérations en cours d’exécution plus longues, suivez les protocoles HTTP asynchrones ; par exemple, renvoyer un message 202 immédiatement, mais continuer à travailler dans l’arrière-plan de hello. |

