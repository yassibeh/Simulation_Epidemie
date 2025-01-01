
# **Simulation Épidémie**

Les citoyens se déplacent dans une ville représentée par une grille de 7x7 cases. Ils peuvent être des médecins, des pompiers, des journalistes ou des citoyens ordinaires.

---

## **Rôles des citoyens :**

1. **Pompiers :**
    - Décontaminent les lieux et les citoyens.
    - Brûlent les corps pour réduire les risques de contamination.
2. **Médecins :**
    - Soignent les maladies dues à la contamination.
    - Peuvent s’auto-soigner s’ils possèdent des pochettes de soins.
3. **Journalistes :**
    - Rapportent des informations sur la contamination et les décès à une agence de presse.
4. **Citoyens ordinaires :**
    - Se déplacent, peuvent être contaminés ou tomber malades.

---

## **Types de lieux et capacités :**

- **Maison :** Capacité maximale de 6 citoyens.
- **Caserne :** Capacité maximale de 8 citoyens.
- **Hôpital :** Capacité maximale de 12 citoyens.
- **Terrain vague :** Capacité maximale de 16 citoyens.

---

## **Contamination initiale :**

1. Seuls les **terrains vagues** peuvent être contaminés au départ.
2. Parmi eux, **10% ont un niveau de contamination compris entre 20% et 40%.**
3. Les autres lieux (maisons, casernes, hôpitaux) sont initialement propres.

---

## **Déplacement des citoyens :**

1. Les citoyens se déplacent aléatoirement :
    - **60% des cas :** Le citoyen reste sur la même case.
    - **40% des cas :** Le citoyen se déplace vers une case voisine.
2. **Effets du déplacement :**
    - **Si le citoyen reste sur la même case :**
        - Son niveau de contamination augmente de **5% du niveau de contamination de la case**.
    - **Si le citoyen se déplace vers une autre case :**
        - Son niveau de contamination augmente de **2% du niveau de contamination de la nouvelle case**.
        - La case voit son niveau de contamination augmenter de **1% du niveau de contamination du citoyen entrant**.
3. **Cas particuliers :**
    - **Caserne :** Niveau de contamination toujours nul.
    - **Hôpital :** L'augmentation de contamination est divisée par **4** grâce aux conditions d’hygiène.

---

## **Exemple pratique :**

1. Un citoyen avec un niveau de contamination de **50%** entre sur une case avec une contamination de **10%**.
    - La contamination de la case augmente de :
        - $1\% \times 50 = 0,5\%$.
        - Nouveau niveau de contamination de la case : **10,5%**.
    - La contamination du citoyen augmente de :
        - $2\% \times 10 = 0,2\%$.
        - Nouveau niveau de contamination du citoyen : **50,2%**.

---

## **Santé et maladie des citoyens :**

1. **Probabilité de tomber malade :**
    - Égale au niveau de contamination d’un citoyen (exemple : 70% de contamination = 70% de probabilité).
2. **Décès après 5 jours de maladie :**
    - À partir du 5ᵉ jour, probabilité de décès : **5% par jour.**
    - Ce risque est réduit de moitié si un médecin est présent sur la même case.

---

## **Propagation de la contamination entre citoyens :**

1. **Si un malade ou un cadavre est présent sur une case :**
    - **10% de chance** de contaminer les citoyens présents.
    - **1% de chance** de contaminer les citoyens des terrains vagues voisins.
2. **Effet sur les citoyens infectés :**
    - Leur niveau de contamination augmente de **1%** par contamination.

---

## **Règles spécifiques des lieux :**

### **1. Terrains vagues :**

- Les terrains vagues peuvent contaminer leurs voisins sous certaines conditions :
    - La contamination se propage uniquement si le niveau de contamination du terrain vague est **supérieur** à celui du voisin.
    - La probabilité de propagation dépend de la direction :
        - **Est, Sud-Est :** 25%.
        - **Nord-Est :** 20%.
        - **Nord, Sud :** 15%.
        - **Ouest, Nord-Ouest, Sud-Ouest :** 3%.


#### **Exemple :**

- Terrain vague A (70%) et terrain vague B (50%) sont voisins.
    - Probabilité de propagation d'A vers B (Est) : 25%.
    - Si la propagation a lieu :
        - Différence de contamination : $70 - 50 = 20\%$.
        - Augmentation de B : Par exemple, $10\% \times 20 = 2\%$.
        - Nouveau niveau de B : **52%**.

---

### **2. Casernes :**

1. **Accès :**
    - Seuls les pompiers peuvent entrer librement.
    - Les citoyens ordinaires ne peuvent entrer que si un pompier est présent.
2. **Décontamination :**
    - Réduction de contamination de **20% par tour** pour les citoyens présents.
    - En **5 tours maximum**, un citoyen est complètement décontaminé.

#### **Exemple :**

- Un citoyen avec une contamination de **50%** entre dans une caserne.
    - Au 1ᵉʳ tour : $50 \times 0.8 = 40\%$.
    - Au 2ᵉ tour : $40 \times 0.8 = 32\%$.

3. **Équipement :**
    - Les pompiers reçoivent un pulvérisateur à 1000% de capacité.
    - Les citoyens reçoivent un appareil pour mesurer la contamination.

---

### **3. Hôpitaux :**

1. **Accès :**
    - Seuls les malades, les médecins et les pompiers peuvent entrer.
2. **Effets sur les malades :**
    - Réduction du risque de mortalité (divisé par 4).
    - Réduction de contamination de **10% par tour**, mais pas en dessous du niveau de contamination de l’hôpital.
3. **Capacité :**
    - Limite de 12 citoyens.
    - Une fois guéris, les citoyens doivent quitter l’hôpital après **2 tours.**

---

## **Simulation simplifiée :**

### **Situation :**

- **Case A :** Terrain vague contaminé à 30%.
- **Case B :** Terrain vague contaminé à 10%.
- **Citoyen 1 :** Contamination 20%.


### **Tour 1 :**

1. Citoyen 1 se déplace de la case A à la case B.
    - Contamination de la case B augmente de $1\% \times 20 = 0,2\%$.
    - Nouvelle contamination de B : $10 + 0,2 = 10,2\%$.
    - Contamination du citoyen augmente de $2\% \times 10,2 = 0,204\%$.
    - Nouvelle contamination du citoyen : $20 + 0,204 = 20,204\%$.

---
### **Détails de l'implémentation - Initialisation et Simulation**

Cette partie décrit les éléments essentiels de la simulation, notamment la configuration initiale de la ville et l'organisation du simulateur en programmes distincts. Voici une explication détaillée de chaque aspect :

---

### **3.1 Initialisation**

#### **Configuration de la ville**

1. **Dimensions :**
    - La ville est une grille de **7x7 cases**, soit un total de 49 cases.
2. **Répartition des types de cases :**
    - **Hôpital :**
        - Placé au **centre de la grille**, c’est-à-dire en position (3,3) si les indices commencent à 0.
        - Il sert à soigner les citoyens malades.
    - **Caserne :**
        - Deux casernes sont placées :
            - Une au **nord-est**, par exemple en position (0,6).
            - Une au **sud-ouest**, par exemple en position (6,0).
            - Elles servent à décontaminer les citoyens et à brûler les cadavres.
    - **Maisons :**
        - Il y a **12 maisons** réparties aléatoirement sur les cases restantes.
        - Les maisons peuvent accueillir jusqu’à 6 citoyens chacune.
    - **Terrains vagues :**
        - Les **34 cases restantes** sont des terrains vagues.
        - Ces terrains peuvent être contaminés et transmettre la contamination.

---

#### **Répartition des citoyens**

1. **Population totale :**
    - La simulation commence avec **37 citoyens** :
        - **4 médecins** : Soignent les malades et réduisent leur risque de décès.
        - **6 pompiers** : Décontaminent les lieux et brûlent les corps.
        - **25 citoyens ordinaires**.
2. **Placement initial :**
    - Tous les citoyens doivent être positionnés sur les cases de la ville.
    - **Contraintes spécifiques :**
        - Au moins **1 médecin** doit être placé sur l’hôpital dès le début.
        - Chaque caserne doit avoir **au moins 1 pompier**.
        - Les autres citoyens sont répartis aléatoirement sur les cases restantes.

---

#### **Journalistes**

- Il y a **2 journalistes**.
- Ils utilisent un **canal de communication unique** (file de messages) pour transmettre des dépêches à une agence de presse.

---

#### **Durée de la simulation**

- La simulation dure **100 tours**, où chaque tour correspond à un jour.
- Un **générateur aléatoire** est utilisé pour :
    - Placer les maisons et les citoyens au début.
    - Déterminer les mouvements aléatoires des citoyens pendant la simulation.

---

#### **Illustration - Exemple de répartition**

Voici un exemple de la disposition de la ville (Figure 1 mentionnée dans le texte) :

```
T  T  T  T  T  T  C
T  M  T  T  T  M  T
T  T  M  T  M  T  T
T  T  T  H  T  T  T
T  T  M  T  M  T  T
M  T  T  T  T  T  T
C  T  T  T  T  T  T
```

**Légende :**

- **T :** Terrain vague.
- **H :** Hôpital.
- **C :** Caserne.
- **M :** Maison.

---

### **3.2 Implémentation du simulateur**

#### **Structure globale du simulateur**

Le simulateur est composé de **quatre programmes distincts**, chacun ayant une responsabilité spécifique et communiquant entre eux via des ressources partagées.

---

#### **1. Programme "epidemic_sim"**

- **Responsabilités :**
    - Gérer la ville et l’état des citoyens.
    - Créer et gérer une **mémoire partagée** contenant des structures de données pour :
        - La disposition de la ville (cases, types de lieux, etc.).
        - L’état des citoyens (sains, malades, décédés, etc.).
    - Recevoir des signaux du programme "timer" pour indiquer la fin d’un tour.
    - Mettre à jour le fichier `evolution.txt` à chaque tour, qui contient :
        - Nombre de citoyens sains.
        - Nombre de malades.
        - Nombre de décès.
        - Nombre de cadavres brûlés.
    - Après 100 tours, envoyer un signal de fin à tous les autres programmes.
- **Interaction avec les autres programmes :**
    - Utilise des **tubes nommés** ou des **signaux** pour échanger des informations avec "citizen_manager" et "press_agency".
    - Génère le fichier `evolution.txt`, utilisé pour afficher les résultats avec Gnuplot.

---

#### **2. Programme "citizen_manager"**

- **Responsabilités :**
    - Gérer tous les **threads citoyens** (médecins, pompiers, citoyens ordinaires, journalistes).
    - Accéder à la mémoire partagée pour :
        - Obtenir les niveaux de contamination des cases.
        - Mettre à jour l’état des citoyens à chaque tour.
    - Simuler les actions des citoyens :
        - Déplacements.
        - Contaminations.
        - Soins et décontaminations.

---

#### **3. Programme "press_agency"**

- **Responsabilités :**
    - Jouer le rôle de l’agence de presse.
    - Recevoir les **dépêches des journalistes** via une **file de messages**.
    - Afficher les informations reçues en continu, avec certaines règles :
        - Dépêches sur la santé des journalistes affichées uniquement si leur contamination > **80%**.
        - Nombre de cadavres et corps brûlés réduit de **35%** avant affichage.
        - Nombre de citoyens contaminés et malades réduit de **10%** avant affichage.

---

#### **4. Programme "timer"**

- **Responsabilités :**
    - Définir la durée d’un tour (entre **1 et 5 secondes**).
    - Envoyer un signal au programme "epidemic_sim" pour indiquer la fin d’un tour.

---

### **Résumé des interactions**

1. **"epidemic_sim" :** Gère la simulation globale et stocke les données dans `evolution.txt`.
2. **"citizen_manager" :** Coordonne les citoyens et met à jour leur état.
3. **"press_agency" :** Traite les dépêches des journalistes et affiche les informations.
4. **"timer" :** Cadence la simulation en indiquant la fin des tours.

---

### **Exemple de fonctionnement :**

#### **Initialisation :**

1. **Hôpital** placé au centre, casernes au nord-est et sud-ouest.
2. **4 médecins** (dont 1 sur l’hôpital), **6 pompiers** (répartis entre les casernes), **25 citoyens ordinaires**.
3. Journalistes prêts à transmettre des dépêches.

#### **Premier tour :**

1. "timer" déclenche la fin du tour après 3 secondes.
2. "citizen_manager" :
    - Déplace les citoyens.
    - Met à jour les états (contamination, santé).
3. "epidemic_sim" met à jour `evolution.txt`.
4. "press_agency" affiche les dépêches.

---


