
* Hello série M offre le nombre de processeurs plus élevé hello (des processeurs virtuels de too128) et la plus grande mémoire (too2.0 TiB) de toutes les machines virtuelles dans le cloud de hello.  Elle est idéale pour les très grandes bases de données ou d’autres applications qui bénéficient d’un nombre élevé de processeurs virtuels et de grandes quantités de mémoire.

* Série Dv2, série D, série G, et équivalents de DS/GS hello sont idéales pour les applications qui exigent des processeurs virtuels plus rapides, les meilleures performances de stockage temporaire, ou ont des demandes de mémoire supérieure.  Elles offrent une combinaison puissante pour de nombreuses applications professionnelles.

* Machines virtuelles de série D sont conçues toorun les applications qui exigent une puissance de calcul et de performances de disque temporaire. Ces machines virtuelles se caractérisent par des processeurs plus rapides, un rapport mémoire-processeur virtuel plus élevé et un disque SSD pour le stockage temporaire. Pour plus d’informations, consultez annonce de type hello sur hello Azure blog, [nouvelles tailles de Machine virtuelle de série D](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).

* Série Dv2, un toohello les fonctionnalités de la série D d’origine, un processeur plus puissant. Hello série Dv2 processeur est d’environ 35 % plus rapide que hello série D à l’UC. Il est basé sur hello dernière génération 2,4 GHz Intel Xeon® E5-2673 v3 (Haswell), processeur et avec hello 2.0 de la technologie Intel Turbo Boost, peuvent atteindre la too3.1 GHz. Hello Dv2 série a hello les mêmes configurations de mémoire et de disque comme hello série D.


## <a name="esv3-series"></a>Série ESv3

ACU : 160-190

Les instances de la série ESv3 sont basées sur hello 2,3 GHz Intel XEON® E5-2673 v4 (Broadwell) processeur peut atteindre 3.5GHz avec Intel Turbo Boost technologie 2.0 et utiliser un stockage premium. Les tailles des machines virtuelles de la série ESv3 sont idéales pour les applications d’entreprise nécessitant une mémoire importante.


| Taille             | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Disques de données max. | Débit de stockage temporaire et en cache max : E/S par seconde / Mbits/s (taille du cache en Gio) | Débit de disque maximal sans mise en cache : E/S / Mbits/s | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) |
|------------------|--------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------------------------|
| Standard_E2s_v3  | 2      | 16          | 32             | 4              | 4 000 / 32 (50)                                                       | 3 200 / 48                                | 2 / Modérée                                   |
| Standard_E4s_v3  | 4      | 32          | 64             | 8              | 8 000 / 64 (100)                                                      | 6 400 / 96                                | 2 / Modérée                                   |
| Standard_E8s_v3  | 8      | 64          | 128            | 16             | 16 000 / 128 (200)                                                    | 12 800 / 192                              | 4 / Élevée                                       |
| Standard_E16s_v3 | 16     | 128         | 256            | 32             | 32 000 / 256 (400)                                                    | 25 600 / 384                              | 8 / Élevée                                       |
| Standard_E32s_v3 | 32     | 256         | 512            | 32             | 64 000 / 512 (800)                                                    | 51 200 / 768                              | 8 / Extrêmement élevée                             |
| Standard_E64s_v3 | 64     | 432         | 864            | 32             | 128 000/1 024 (1 600)                                                   | 80 000 / 1 200                             | 8 / Extrêmement élevée                             |



## <a name="ev3-series"></a>Série Ev3

ACU : 160-190 

Les instances de la série Ev3 sont basées sur hello 2,3 GHz Intel XEON® E5-2673 v4 (Broadwell) processeur afin d’obtenir 3.5GHz avec Intel Turbo Boost technologie 2.0. Les tailles des machines virtuelles de la série ESv3 sont idéales pour les applications d’entreprise nécessitant une mémoire importante.

Le stockage sur disque de données est facturé séparément des machines virtuelles. toouse disques de stockage premium, utilisez des tailles de ESv3 hello. Hello tarification et les paramètres de facturation pour les tailles de ESv3 sont hello identique à celui de la série Ev3. 


| Taille            | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Disques de données max. | Débit de stockage temporaire local max : E/S par seconde / Mbits/s de lecture / Mbits/s d’écriture | Cartes réseau (max)/Bande passante réseau |
|-----------------|-----------|-------------|----------------|----------------|----------------------------------------------------------|------------------------------|
| Standard_E2_v3  | 2         | 16          | 50             | 4              | 3000/46/23                                               | 2 / Modérée                 |
| Standard_E4_v3  | 4         | 32          | 100            | 8              | 6000/93/46                                               | 2 / Modérée                 |
| Standard_E8_v3  | 8         | 64          | 200            | 16             | 12000/187/93                                             | 4 / Élevée                     |
| Standard_E16_v3 | 16        | 128         | 400            | 32             | 24000/375/187                                            | 8 / Élevée                     |
| Standard_E32_v3 | 32        | 256         | 800            | 32             | 48000/750/375                                            | 8 / Extrêmement élevée           |
| Standard_E64_v3 | 64        | 432         | 1 600           | 32             | 96000/1000/500                                           | 8 / Extrêmement élevée           |


## <a name="m-series"></a>Série M*

ACU : 160-180

| Taille            | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Disques de données max. | Débit de stockage temporaire et en cache max : E/S par seconde / Mbits/s (taille du cache en Gio) | Débit de disque maximal sans mise en cache : E/S / Mbits/s | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) |
|-----------------|------|-------------|----------------|----------------|-----------------------------------------------------------------------|-------------------------------------------|------------------------------|
| Standard_M64ms  | 64   | 1792        | 2 048           | 32             | 80,000 / 800 (6348)       | 40 000 / 1 000                            | 8 / 16 000          |
| Standard_M128s** | 128  | 2 048        | 4096           | 64             | 160,000 / 1,600 (12,696) | 80 000 / 2 000                            | 8 / 25 000          |



*Machines virtuelles de série M dotées de la technologie Hyper-Threading d’Intel®

** Plus de 64 processeurs virtuels nécessitent un des systèmes d’exploitation invités pris en charge suivants : Windows Server 2016, Ubuntu 16.04 LTS, SLES 12 SP2 et Red Hat Enterprise Linux ou CentOS 7.3 avec LIS 4.2.1 

<br>

## <a name="gs-series"></a>Série GS*

ACU : 180 - 240

| Taille | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Disques de données max. | Débit de stockage temporaire et en cache max : E/S par seconde / Mbits/s (taille du cache en Gio) | Débit de disque maximal sans mise en cache : E/S / Mbits/s | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_GS1 |2 |28 |56 |4 |10 000 / 100 (264) |5 000 / 125 |2 / 2 000 |
| Standard_GS2 |4 |56 |112 |8 |20 000 / 200 (528) |10 000 / 250 |2 / 4 000 |
| Standard_GS3 |8 |112 |224 |16 |40 000 / 400 (1 056) |20 000 / 500 |4 / 8 000 |
| Standard_GS4 |16 |224 |448 |32 |80 000 / 800 (2 112) |40 000 / 1 000 |8 / 6 000 à 16000 &#8224; |
| Standard_GS5** |32 |448 |896 |64 |160 000 / 1 600 (4 224) |80 000 / 2 000 |8 / 20 000 |

* hello maximale débit de disque (e/s ou Mbits/s) possible avec une série GS machine virtuelle peut être limité par le nombre de hello, taille et entrelacements de hello attachée ou les disques. Pour plus d’informations, consultez l’article [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../articles/storage/common/storage-premium-storage.md). 

** Instance est isolé toohardware tooa dédié seul client.


<br>

## <a name="g-series"></a>Série G

ACU : 180 - 240

| Taille         | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Débit de stockage temporaire local max : E/S par seconde / Mbits/s de lecture / Mbits/s d’écriture | Disques de données max / débit : E/S par seconde | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_G1  | 2         | 28          | 384            | 6000 / 93 / 46                                           | 4 / 4 x 500                       | 2 / 2 000                     |
| Standard_G2  | 4         | 56          | 768            | 12000 / 187 / 93                                         | 8 / 8 x 500                       | 2 / 4 000                     |
| Standard_G3  | 8         | 112         | 1 536          | 24000 / 375 / 187                                        | 16 / 16 x 500                     | 4 / 8 000                |
| Standard_G4  | 16        | 224         | 3 072          | 48000 / 750 / 375                                        | 32 / 32 x 500                     | 8 / 6 000 à 16000 &#8224;          |
| Standard_G5* | 32        | 448         | 6 144          | 96000 / 1500 / 750                                       | 64 / 64 x 500                     | 8 / 20 000           |

* Instance est isolé toohardware tooa dédié seul client.
<br>


## <a name="dsv2-series"></a>Séries DSv2*

ACU : 210-250

| Taille | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Disques de données max. | Débit de stockage temporaire et en cache max : E/S par seconde / Mbits/s (taille du cache en Gio) | Débit de disque maximal sans mise en cache : E/S / Mbits/s | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS11_v2 |2 |14 |28 |4 |8 000 / 64 (72) |6 400 / 96 |2 / 1 500 |
| Standard_DS12_v2 |4 |28 |56 |8 |16 000 / 128 (144) |12 800 / 192 |4 / 3 000 |
| Standard_DS13_v2 |8 |56 |112 |16 |32 000 / 256 (288) |25 600 / 384 |8 / 6 000 |
| Standard_DS14_v2 |16 |112 |224 |32 |64 000 / 512 (576) |51 200 / 768 |8 / 6 000 à 12 000 &#8224; |
| Standard_DS15_v2** |20 |140 |280 |40 |80 000 / 640 (720) |64 000 / 960 |8 / 20 000***

* hello maximale débit de disque (e/s ou Mbits/s) possible avec une série de DSv2 machine virtuelle peut être limité par le nombre de hello, taille et entrelacements de hello attachée ou les disques.  Pour plus d’informations, consultez l’article [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../articles/storage/common/storage-premium-storage.md).

** Instance est un nœud isolé que garantit que votre machine virtuelle est hello uniquement les ordinateurs virtuels sur notre nœud processeurs Intel Haswell.

***25 000 Mbits/s avec mise en réseau accélérée.

<br>

## <a name="dv2-series"></a>Série Dv2

ACU : 210-250

| Taille              | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Débit de stockage temporaire local max : E/S par seconde / Mbits/s de lecture / Mbits/s d’écriture | Disques de données max / débit : E/S par seconde | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) |
|-------------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_D11_v2   | 2         | 14          | 100            | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1 500                     |
| Standard_D12_v2   | 4         | 28          | 200            | 12000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 3 000                     |
| Standard_D13_v2   | 8         | 56          | 400            | 24000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 6 000                     |
| Standard_D14_v2   | 16        | 112         | 800            | 48000 / 750 / 375                                        | 32 / 32 x 500                       | 8 / 6 000 à 12 000 &#8224;          |
| Standard_D15_v2* | 20        | 140         | 1 000          | 60000 / 937 / 468                                        | 40 / 40 x 500                       | 8 / 20000** |

* Instance est un nœud isolé que garantit que votre machine virtuelle est hello uniquement les ordinateurs virtuels sur notre nœud processeurs Intel Haswell.

**25 000 Mbits/s avec mise en réseau accélérée.

<br>

## <a name="ds-series"></a>Séries DS*

ACU : 160

| Taille | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Disques de données max. | Débit de stockage temporaire et en cache max : E/S par seconde / Mbits/s (taille du cache en Gio) | Débit de disque maximal sans mise en cache : E/S / Mbits/s | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS11 |2 |14 |28 |4 |8 000 / 64 (72) |6 400 / 64 |2 / 1 000 |
| Standard_DS12 |4 |28 |56 |8 |16 000 / 128 (144) |12 800 / 128 |4 / 2 000 |
| Standard_DS13 |8 |56 |112 |16 |32 000 / 256 (288) |25 600 / 256 |8 / 4 000 |
| Standard_DS14 |16 |112 |224 |32 |64 000 / 512 (576) |51 200 / 512 |8 / 6000 - 8000 &#8224; |

* hello maximale débit de disque (e/s ou Mbits/s) possible avec une machine virtuelle de la série DS peut-être être limité par nombre de hello, taille et entrelacements de hello attachée ou les disques.  Pour plus d’informations, consultez l’article [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../articles/storage/common/storage-premium-storage.md).


## <a name="d-series"></a>Série D

ACU : 160

| Taille         | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Débit de stockage temporaire local max : E/S par seconde / Mbits/s de lecture / Mbits/s d’écriture | Disques de données max / débit : E/S par seconde | Nombre max de cartes réseau / Performance réseau attendue (Mbits/s) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| D11 standard | 2         | 14          | 100            | 6000 / 93 / 46                                           | 4 / 4 x 500                         | 2 / 1 000                     |
| D12 standard | 4         | 28          | 200            | 12000 / 187 / 93                                         | 8 / 8 x 500                         | 4 / 2 000                     |
| D13 standard | 8         | 56          | 400            | 24000 / 375 / 187                                        | 16 / 16 x 500                       | 8 / 4 000                     |
| D14 standard | 16        | 112         | 800            | 48000 / 750 / 375                                        | 32 / 32 x 500                       | 8 / 6000 - 8000 &#8224;                |

<br>

