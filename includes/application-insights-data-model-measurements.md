Collection des mesures personnalisées. Utilisez cette tooreport collection nommée de mesure associé avec un élément de données de télémétrie hello. Les cas d’utilisation classiques sont :
- taille de Hello de charge utile de télémétrie des dépendances
- nombre de Hello d’éléments de file d’attente traités par la demande de télémétrie
- temps que le client a duré toocomplete hello étape de fin de l’étape Assistant télémétrie des événements.

Vous pouvez interroger les [mesures personnalisées](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) dans l’analyse des applications :

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > Mesures personnalisées sont associés avec l’élément de données de télémétrie hello qu'auquel ils appartiennent. Ils sont toosampling d’objet avec l’élément de données de télémétrie hello contenant ces mesures. une mesure dont la valeur est indépendante des autres types de données de télémétrie, utilisation de tootrack [télémétrie des métriques](../articles/application-insights/app-insights-api-custom-events-metrics.md).

Longueur maximale de clé  : 150
