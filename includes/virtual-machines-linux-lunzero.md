Lorsque vous ajoutez des disques de données tooa Linux VM, vous pouvez rencontrer des erreurs si un disque n’existe pas au numéro d’unité logique 0. Si vous ajoutez un disque manuellement à l’aide de hello `azure vm disk attach-new` commande et que vous spécifiez un numéro d’unité logique (`--lun`) au lieu de laisser hello toodetermine de plateforme Windows Azure hello LUN approprié, prenez soin qu’un disque existe déjà et qu’il existera au LUN 0. 

Envisagez de hello montrant un extrait de code de sortie hello à partir de l’exemple suivant `lsscsi`:

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

les disques de données Hello deux existent au LUN 0 et LUN 1 (première colonne de hello Bonjour `lsscsi` détails sur les sorties `[host:channel:target:lun]`). Les deux disques doivent être accessbile à partir de hello machine virtuelle. Si vous aviez spécifié manuellement de hello premier disque toobe est ajouté au LUN 1 et le deuxième disque de hello au LUN 2, vous pourrez voir pas disques hello correctement à partir de votre machine virtuelle.

> [!NOTE]
> Bonjour Azure `host` valeur est 5 dans ces exemples, mais cela peut varier en fonction de type hello de stockage que vous sélectionnez.
> 
> 

Ce comportement de disque n’est pas un problème d’Azure, mais de manière hello dans le hello Linux noyau suit les spécifications de SCSI hello. Lorsque le noyau Linux de hello analyse des périphériques attachés au bus SCSI hello, un appareil doit être présent au LUN 0 dans l’ordre pour hello toocontinue de système d’analyse pour les autres appareils. Par conséquent :

* Examinez la sortie hello de `lsscsi` après l’ajout d’un tooverify de disque de données que vous avez un disque au LUN 0.
* Si le disque ne s’affiche pas correctement dans votre machine virtuelle, vérifiez qu'un disque existe sur le LUN 0.

