Une machine virtuelle Azure prend en charge l'attachement d'un certain nombre de disques de données. Pour des performances optimales, vous devez toolimit hello de disques très utilisées associé toohello machine virtuelle tooavoid possible la limitation. Si tous les disques ne sont pas très utilisés à hello simultanément, compte de stockage hello peut prendre en charge un plus grand nombre de disques.

* **Pour les disques Azure géré :** limite du nombre de disques de managé est régionale et également varie selon le type de stockage hello. Hello par défaut et également le nombre maximal hello est 10 000 par abonnement, par région et par type de stockage. Par exemple, vous pouvez créer jusqu'à too10, 000 standard gérés disques ainsi que 10 000 premium gérés disques dans un abonnement et dans une région. 

    Géré instantanés et les Images sont comptées par rapport à hello que limiter des disques gérés.

* **Pour les comptes de stockage standard :** un compte de stockage standard a un taux de demandes total maximal de 20 000 opérations d'E/S par seconde. Hello total IOPS sur tous vos disques de machine virtuelle dans un compte de stockage standard ne doit pas dépasser cette limite.
  
    Vous pouvez calculer à peu près de nombre hello de disques très utilisées pris en charge par un compte de stockage standard unique en fonction de la limite du taux de demande hello. Par exemple, pour un machine virtuelle, le niveau de base hello nombre maximal d’intensive des disques est environ 66 (20 000/300 IOPS par disque), et pour une machine virtuelle niveau Standard, il est environ 40 (20 000/500 IOPS par disque), comme indiqué dans le tableau hello ci-dessous. 
* **Pour les comptes de stockage premium :** un compte de stockage premium a un débit total maximum de 50 Gbits/s. débit total de Hello dans l’ensemble de vos disques de machine virtuelle ne doit pas dépasser cette limite.

