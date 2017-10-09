
<!-- A-series, Av2-series, D-series, Dv2-series, DS-series*, DSv2-series* -->

- Hello série et les machines virtuelles de série Av2 peuvent être déployés sur une variété de types de matériel et les processeurs. taille de Hello est limitée, en fonction de matériel hello, les performances du processeur cohérent toooffer pour hello instance, quel que soit le matériel hello sur qu'il est déployé en cours d’exécution. toodetermine hello physique matériel sur lequel cette taille est déployée, requête hello virtuel du matériel à partir de hello Machine virtuelle.

- Machines virtuelles de série D sont conçues toorun les applications qui exigent une puissance de calcul et de performances de disque temporaire. Machines virtuelles de série D fournissent des processeurs plus rapides, un taux plus élevé de la mémoire de processeurs et un disque SSD (SSD) pour le disque temporaire de hello. Pour plus d’informations, consultez annonce de type hello sur hello Azure blog, [nouvelles tailles de Machine virtuelle de série D](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).

- Série Dv2, un toohello les fonctionnalités de la série D d’origine, un processeur plus puissant. Hello série Dv2 processeur est d’environ 35 % plus rapide que hello série D à l’UC. Il est basé sur hello dernière génération 2,4 GHz Intel Xeon® E5-2673 v3 (Haswell), processeur et avec hello 2.0 de la technologie Intel Turbo Boost, peuvent atteindre la too3.1 GHz. Hello Dv2 série a hello les mêmes configurations de mémoire et de disque comme hello série D.

- tailles de niveau de base Hello sont principalement pour les charges de travail de développement et les autres applications qui ne nécessitent pas équilibrage de charge, la mise à l’échelle automatique ou nécessitant beaucoup de mémoire ordinateurs virtuels. Pour savoir quelles sont les tailles de machines virtuelles les plus appropriées pour les applications de production, consultez (Tailles des machines virtuelles)[virtual-machines-size-specs.md] et pour des informations sur la tarification des machines virtuelles, consultez [Tarification des machines virtuelles Linux](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="dsv3-series"></a>Dsv3-series

ACU : 160-190

Les tailles de série Dsv3 sont basées sur hello 2,3 GHz Intel XEON® E5-2673 v4 (Broadwell) processeur peut atteindre 3.5GHz avec Intel Turbo Boost technologie 2.0 et utiliser un stockage premium. tailles de série Dsv3 Hello offrent une combinaison de processeurs, mémoire et le stockage temporaire pour la plupart des charges de travail de production.


| Taille             | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Disques de données max. | Débit de stockage temporaire et en cache max : E/S par seconde / Mbits/s (taille du cache en Gio) | Débit de disque maximal sans mise en cache : E/S / Mbits/s | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) |
|------------------|--------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------------------------|
| Standard_D2s_v3  | 2      | 8           | 16             | 4              | 4 000 / 32 (50)                                                       | 3 200 / 48                                | 2 / Modérée                                   |
| Standard_D4s_v3  | 4      | 16          | 32             | 8              | 8 000 / 64 (100)                                                      | 6 400 / 96                                | 2 / Modérée                                   |
| Standard_D8s_v3  | 8      | 32          | 64             | 16             | 16 000 / 128 (200)                                                    | 12 800 / 192                              | 4 / Élevée                                       |
| Standard_D16s_v3 | 16     | 64          | 128            | 32             | 32 000 / 256 (400)                                                    | 25 600 / 384                              | 8 / Élevée                                       |


## <a name="dv3-series"></a>Série Dv3

ACU : 160-190

Les tailles de série Dv3 sont basées sur hello 2,3 GHz Intel XEON® E5-2673 v4 (Broadwell) processeur afin d’obtenir 3.5GHz avec Intel Turbo Boost technologie 2.0. tailles de série Dv3 Hello offrent une combinaison de processeurs, mémoire et le stockage temporaire pour la plupart des charges de travail de production.

Le stockage sur disque de données est facturé séparément des machines virtuelles. les disques de stockage premium toouse, utiliser les tailles Dsv3 hello. Hello tarification et les paramètres de facturation pour Dsv3 tailles sont hello identique à celui de la série Dv3. 


| Taille            | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Disques de données max. | Débit de stockage temporaire local max : E/S par seconde / Mbits/s de lecture / Mbits/s d’écriture | Cartes réseau (max)/Bande passante réseau |
|-----------------|-----------|-------------|----------------|----------------|----------------------------------------------------------|------------------------------|
| Standard_D2_v3  | 2         | 8           | 50             | 4              | 3000/46/23                                               | 2 / Modérée                 |
| Standard_D4_v3  | 4         | 16          | 100            | 8              | 6000/93/46                                               | 2 / Modérée                 |
| Standard_D8_v3  | 8         | 32          | 200            | 16             | 12000/187/93                                             | 4 / Élevée                     |
| Standard_D16_v3 | 16        | 64          | 400            | 32             | 24000/375/187                                            | 8 / Élevée                     |


## <a name="dsv2-series"></a>Séries DSv2

ACU : 210-250

| Taille | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Disques de données max. | Débit de stockage temporaire et en cache max : E/S par seconde / Mbits/s (taille du cache en Gio) | Débit de disque maximal sans mise en cache : E/S / Mbits/s | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS1_v2 |1 |3,5 |7 |2 |4 000 / 32 (43) |3 200 / 48 |2 / 750 |
| Standard_DS2_v2 |2 |7 |14 |4 |8 000 / 64 (86) |6 400 / 96 |2 / 1 500 |
| Standard_DS3_v2 |4 |14 |28 |8 |16 000 / 128 (172) |12 800 / 192 |4 / 3 000 |
| Standard_DS4_v2 |8 |28 |56 |16 |32 000 / 256 (344) |25 600 / 384 |8 / 6 000 |
| Standard_DS5_v2 |16 |56 |112 |32 |64 000 / 512 (688) |51 200 / 768 |8 / 6 000 à 12 000 &#8224;|



## <a name="dv2-series"></a>Série Dv2

ACU : 210-250

| Taille              | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Débit de stockage temporaire local max : E/S par seconde / Mbits/s de lecture / Mbits/s d’écriture | Disques de données max / débit : E/S par seconde | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) |
|-------------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D1_v2    | 1         | 3,5         | 50             | 3000 / 46 / 23                                           | 2 / 2 x 500                         | 2 / 750                 |
| Standard_D2_v2    | 2         | 7           | 100            | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1 500                     |
| Standard_D3_v2    | 4         | 14          | 200            | 12000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 3 000                     |
| Standard_D4_v2    | 8         | 28          | 400            | 24000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 6 000                     |
| Standard_D5_v2    | 16        | 56          | 800            | 48000 / 750 / 375                                        | 32 / 32 x 500                       | 8 / 6 000 à 12 000 &#8224;          |


<br>

## <a name="ds-series"></a>Série DS

ACU : 160

| Taille | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Disques de données max. | Débit de stockage temporaire et en cache max : E/S par seconde / Mbits/s (taille du cache en Gio) | Débit de disque maximal sans mise en cache : E/S / Mbits/s | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS1 |1 |3,5 |7 |2 |4 000 / 32 (43) |3 200 / 32 |2 / 500 |
| Standard_DS2 |2 |7 |14 |4 |8 000 / 64 (86) |6 400 / 64 |2 / 1 000 |
| Standard_DS3 |4 |14 |28 |8 |16 000 / 128 (172) |12 800 / 128 |4 / 2 000 |
| Standard_DS4 |8 |28 |56 |16 |32 000 / 256 (344) |25 600 / 256 |8 / 4 000 |

<br>

## <a name="d-series"></a>Série D 

ACU : 160

| Taille         | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Débit de stockage temporaire local max : E/S par seconde / Mbits/s de lecture / Mbits/s d’écriture | Disques de données max / débit : E/S par seconde | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| D1 standard  | 1         | 3,5         | 50             | 3000 / 46 / 23                                           | 2 / 2 x 500                         | 2 / 500                 |
| D2 standard  | 2         | 7           | 100            | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1 000                     |
| D3 standard  | 4         | 14          | 200            | 12000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 2 000                     |
| D4 standard  | 8         | 28          | 400            | 24000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 4 000                     |

<br>


## <a name="av2-series"></a>Série Av2

ACU : 100

| Taille            | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Débit de stockage temporaire local max : E/S par seconde / Mbits/s de lecture / Mbits/s d’écriture | Disques de données max / débit : E/S par seconde | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) | 
|-----------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_A1_v2  | 1         | 2           | 10             | 1000 / 20 / 10                                           | 2 / 2 x 500               | 2 / 250                 |
| Standard_A2_v2  | 2         | 4           | 20             | 2000 / 40 / 20                                           | 4 / 4 x 500               | 2 / 500                 |
| Standard_A4_v2  | 4         | 8           | 40             | 4000 / 80 / 40                                           | 8 / 8 x 500               | 4 / 1 000                     |
| Standard_A8_v2  | 8         | 16          | 80             | 8000 / 160 / 80                                          | 16 / 16 x 500             | 8 / 2 000                     |
| Standard_A2m_v2 | 2         | 16          | 20             | 2000 / 40 / 20                                           | 4 / 4 x 500               | 2 / 500                 |
| Standard_A4m_v2 | 4         | 32          | 40             | 4000 / 80 / 40                                           | 8 / 8 x 500               | 4 / 1 000                     |
| Standard_A8m_v2 | 8         | 64          | 80             | 8000 / 160 / 80                                          | 16 / 16 x 500             | 8 / 2 000                     |

<br>

## <a name="a-series"></a>Série A

ACU : 50-100

| Taille | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (HDD) : Gio | Disques de données max. | Débit de disque de données max : E/S par seconde | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s)  |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A0* |1 |0,768 |20 |1 |1 x 500 |2 / 100 |
| Standard_A1 |1 |1,75 |70 |2 |2 x 500 |2 / 500  |
| Standard_A2 |2 |3,5 |135 |4 |4 x 500 |2 / 500 |
| Standard_A3 |4 |7 |285 |8 |8 x 500 |2 / 1 000 |
| Standard_A4 |8 |14 |605 |16 |16 x 500 |4 / 2 000 |
| Standard_A5 |2 |14 |135 |4 |4 x 500 |2 / 500 |
| Standard_A6 |4 |28 |285 |8 |8 x 500 |2 / 1 000 |
| Standard_A7 |8 |56 |605 |16 |16 x 500 |4 / 2 000 |
<br>

* hello taille A0 est trop sollicité sur du matériel physique de hello. Pour cette taille spécifique, les autres déploiements de client peuvent affecter les performances de hello de votre charge de travail en cours d’exécution. les performances relatives Hello sont décrite ci-dessous comme base hello attendu, variabilité approximative de sujet tooan de 15 pour cent.

### <a name="standard-a0---a4-using-cli-and-powershell"></a>Standard A0-A4 à l’aide de l’interface de ligne de commande et de Powershell
Dans le modèle de déploiement classique de hello, certains noms de taille de machine virtuelle sont légèrement différents dans l’interface CLI et PowerShell :

* Standard_A0 est ExtraSmall (Très petit) 
* Standard_A1 est Small (Petit)
* Standard_A2 est Medium (Moyen)
* Standard_A3 est Large (Grand)
* Standard_A4 est ExtraLarge (Très grand)

## <a name="basic-a"></a>De base A

|Taille - Taille\Nom | Processeurs virtuels |Mémoire|Cartes réseau (max)|Taille max. du disque temporaire |Bande passante disques de données (1 023 Go chacun)|Bande passante Nombre maximal d’opérations d’E/S par seconde (300 par disque)|
|---|---|---|---|---|---|---|
|0A0\Basic_A0|1|768 Mo|2| 20 Go|1|1 x 300|
|A1\Basic_A1|1|1,75 Go|2| 40 Go |2|2 x 300|
|A2\Basic_A2|2|3,5 Go|2| 60 Go|4|4 x 300|
|A3\Basic_A3|4|7 Go|2| 120 Go |8|8 x 300|
|A4\Basic_A4|8|14 Go|2| 240 Go |16|16 x 300|
