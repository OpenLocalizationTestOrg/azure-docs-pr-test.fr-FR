>[!NOTE]
>Pour les ressources qui ne sont pas fixes, vous pouvez demander hello quotas toobe est déclenché, en ouvrant un ticket de support. Faire **pas** créer des comptes Azure Media Services supplémentaires d’essayer tooobtain les limites supérieures.

| Ressource | Limite par défaut | 
| --- | --- | 
| Comptes AMS (Azure Media Services) dans un seul abonnement | 25 (fixe) |
| Unités réservées de média (RU) par compte AMS |25 (S1, S2)<br/>10 (S3) <sup>(1)</sup> | 
| Travaux par compte AMS | 50,000<sup>(2)</sup> |
| Tâches chaînées par travail | 30 (fixe) |
| Actifs par compte AMS | 1 000 000|
| Actifs par tâche | 50 |
| Actifs par travail | 100 |
| Localisateurs uniques associés à un actif à un moment donné | 5<sup>(4)</sup> |
| Canaux en direct par compte AMS  |5|
| Programmes dans un état Arrêté par canal  |50|
| Programmes en cours d’exécution par canal  |3|
| Points de terminaison de diffusion en continu en cours d’exécution par compte AMS|2|
| Unités de diffusion en continu par point de terminaison de diffusion en continu  |10 |
| Comptes de stockage | 1 000<sup>(5)</sup> (fixe) |
| Stratégies | 1,000,000<sup>(6)</sup> |
| Taille du fichier| Dans certains scénarios il existe une limite sur la taille de fichier maximale hello pris en charge pour le traitement dans Media Services. <sup>7</sup> |
  
<sup>1</sup> Les unités réservées S3 ne sont pas disponibles en Inde-Ouest. les limites RU maximales Hello réinitialisées si les clients hello change de type hello (par exemple, à partir de S2 tooS1). 

<sup>2</sup> Ce nombre comprend les travaux en file d’attente, terminés, actifs et annulés. Il n’inclut pas les travaux supprimés. Vous pouvez supprimer hello anciens travaux à l’aide de **IJob.Delete** ou hello **supprimer** requête HTTP.

À partir du 1er avril 2017, n’importe quel enregistrement de la tâche dans votre compte plu de 90 jours est automatiquement supprimé, ainsi que ses enregistrements de tâche associés, même si le nombre total de hello d’enregistrements est au-dessous du quota maximal de hello. Si vous avez besoin des informations de tâche/hello tooarchive, vous pouvez utiliser le code hello décrit [ici](../articles/media-services/media-services-dotnet-manage-entities.md).

<sup>3</sup> lors d’une demande en entités de travail toolist, un maximum de 1 000 est renvoyé par requête. Si vous devez suivre tookeep de toutes les soumises travaux, vous pouvez utiliser top/skip comme décrit dans [options de requête système OData](http://msdn.microsoft.com/library/gg309461.aspx).

<sup>4</sup> Les localisateurs ne sont pas conçus pour gérer le contrôle d’accès par utilisateur. toogive différents droits tooindividual les utilisateurs d’accès, utilisez les solutions de gestion des droits numériques (DRM). Pour plus d’informations, consultez [cette](../articles/media-services/media-services-content-protection-overview.md) section.

<sup>5</sup> comptes de stockage hello doivent provenir de hello même abonnement Azure.

<sup>6</sup> Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy). 

>[!NOTE]
> Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, etc.. Pour plus d’informations et un exemple, consultez [cette](../articles/media-services/media-services-dotnet-manage-entities.md#limit-access-policies) section.

<sup>7</sup>si vous téléchargez tooan contenu actif dans Azure Media Services avec tooprocess intention de hello avec un des processeurs multimédias de hello dans notre service (autrement dit, les encodeurs telles que des moteurs Media Encoder Standard et Workflow d’encodeur multimédia Premium ou l’analyse comme le détecteur de Face), puis vous devez connaître de contrainte hello sur la taille maximale hello. 

Depuis le 15 mai 2017, taille maximale de hello pris en charge pour un seul objet blob est to 195 - avec largers de fichier dépasse cette limite, votre tâche échoue. Nous travaillons un tooaddress correctif cette limite. En outre, hello contrainte sur la taille maximale de hello hello actif est comme suit.

| Types d’unités réservées de média | Taille maximale en entrée (Go)| 
| --- | --- | 
|S1 | 325|
|S2 | 640|
|S3 | 260|
