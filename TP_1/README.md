# TP_1 : Étude de Cas : Entreprise XYZ

## Tpoplogie proposée:

```
---
config:
  theme: neo
  layout: fixed
  look: neo
---
flowchart TD
 subgraph Internet["Internet"]
        FW["Firewall / ISP"]
  end
 subgraph Datacenter["Datacenter"]
        R1["Routeur Cœur 1"]
        R2["Routeur Cœur 2"]
        SWC1["Switch Cœur 1"]
        SWC2["Switch Cœur 2"]
  end
 subgraph Distribution["Distribution"]
        SWD1B1["Switch Distribution Bât. 1 - A"]
        SWD2B1["Switch Distribution Bât. 1 - B"]
        SWD1B2["Switch Distribution Bât. 2 - A"]
        SWD2B2["Switch Distribution Bât. 2 - B"]
  end
 subgraph s1["Accès_Bât_1"]
        SWA1E1["Switch Accès Étage 1 - Bât. 1"]
        SWA2E2["Switch Accès Étage 2 - Bât. 1"]
  end
 subgraph s2["Accès_Bât_2"]
        SWA3E1["Switch Accès Étage 1 - Bât. 2"]
        SWA4E2["Switch Accès Étage 2 - Bât. 2"]
  end
    FW --> R1 & R2
    R1 --> SWC1 & SWC2
    R2 --> SWC1 & SWC2
    SWC1 --> SWD1B1 & SWD1B2 & SWD2B1 & SWD2B2
    SWC2 --> SWD1B1 & SWD1B2 & SWD2B1 & SWD2B2
    SWD1B1 --> SWA1E1 & SWA2E2
    SWD2B1 --> SWA1E1 & SWA2E2
    SWD1B2 --> SWA3E1 & SWA4E2
    SWD2B2 --> SWA4E2 & SWA3E1
```

## Description topologie

### Datacenter/core

Le datacenter abrite :

    Deux routeurs cœur (R1, R2) : gèrent le routage inter-sites, les politiques globales, et la redondance.

    Deux switches cœur (SWC1, SWC2) : assurent le transit rapide des données vers les couches Distribution. Ils sont reliés en double liaison aux routeurs, garantissant une tolérance aux pannes.

### Couche Distribution (par bâtiment)

Chaque bâtiment dispose de deux switches de distribution :

    Bâtiment 1 : SWD1B1 et SWD2B1

    Bâtiment 2 : SWD1B2 et SWD2B2

### Couche Accès (par étage)

Chaque étage de chaque bâtiment est équipé d’un switch d’accès :

    Bâtiment 1 :

        SWA1E1 (Étage 1)

        SWA2E2 (Étage 2)

    Bâtiment 2 :

        SWA3E1 (Étage 1)

        SWA4E2 (Étage 2)

L'infrastructure a été pensée pour :

    Ajouter facilement de nouveaux bâtiments en étendant les couches Distribution et Accès.

    Étendre les services via de nouveaux VLANs ou routage dynamique (OSPF, BGP).

    Supporter l’agrégation de liens et l’évolution vers des interfaces 10/40 GbE au besoin.

    Rajouter SW si besoin dans les étages/batiments
