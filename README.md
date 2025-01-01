
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

Ces corrections assurent une mise en page claire et des calculs précis. Si vous avez besoin de plus de détails ou d’un autre exemple, n’hésitez pas ! 😊

