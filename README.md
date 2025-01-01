# Simulation_Epidemie
Projet_simulation_Epidemie



Les citoyens se déplacent dans une ville représentée par une grille de 7x7 cases. Ils peuvent être des médecins, des pompiers, des journalistes ou des citoyens ordinaires.

- **Rôles :**
    - Les **pompiers** décontaminent les lieux et les citoyens.
    - Les **médecins** soignent les maladies dues à la contamination.
    - Les **journalistes** rapportent des informations sur la contamination et les décès à une agence de presse hors de la ville.
- **Types de cases et capacité :**
    - Maison : 6 citoyens.
    - Caserne : 8 citoyens.
    - Hôpital : 12 citoyens.
    - Terrain vague : 16 citoyens.
- **Contamination :**
    - Les terrains vagues sont les seuls initialement contaminés, avec 10% d’entre eux ayant un niveau de contamination entre 20% et 40%.

Chaque case a un niveau de contamination compris entre 0% et 100%.

Chaque lieu (case) a un niveau de contamination qui peut aller de 0% (pas de contamination) à 100% (contamination totale).

    Au départ (début de la simulation) :
        Seuls les terrains vagues peuvent être contaminés.
        Parmi tous les terrains vagues, seulement 10% d'entre eux ont un niveau de contamination supérieur à zéro.
        Ces terrains contaminés ont des niveaux de contamination compris entre 20% et 40%.
    En résumé, la majorité des terrains vagues ne sont pas contaminés au début, et parmi les contaminés, le niveau reste modéré (pas au maximum).
    
Voici un résumé structuré et détaillé, prêt à être traduit en code :

---

### **Déplacement des citoyens**
- Les citoyens peuvent se déplacer **aléatoirement** sur une grille.
  - **60% des cas :** Le citoyen reste sur la même case.
  - **40% des cas :** Le citoyen se déplace vers une case voisine (choisie aléatoirement parmi les 8 cases autour).
- Le **niveau de contamination d’un citoyen** est compris entre **0 (0%)** et **1 (100%)**.

---

### **Effets du déplacement sur la contamination**
1. **Si le citoyen reste sur la même case :**
   - Son niveau de contamination augmente de **5% du niveau actuel du lieu**.

2. **Si le citoyen se déplace vers une nouvelle case :**
   - Son niveau de contamination augmente de **2% du niveau de contamination du lieu cible**.
   - La case cible voit son niveau de contamination augmenter de **1% du niveau de contamination du citoyen**.
   - ### **Exemple pratique** : 
        1. Supposons qu’un citoyen a un niveau de contamination de **50%**.
        2. Il entre sur une case qui a actuellement un niveau de contamination de **10%**.
        3. La contamination de la case va augmenter de :
           \[
           1\% \times 50\% = 0,5\%
           \]
           - Nouveau niveau de contamination de la case = **10,5%**.


3. **Cas particuliers pour les lieux :**
   - **Caserne :** Niveau de contamination toujours nul.
   - **Hôpital :** L'augmentation de la contamination est divisée par **4** grâce aux conditions d’hygiène.

---

### **État de santé du citoyen**
1. **Probabilité de maladie :**
   - Un citoyen contaminé peut tomber malade.
   - La probabilité de tomber malade à chaque tour est **égale à son niveau de contamination**.

2. **Décès à partir du 5ᵉ jour de maladie :**
   - Probabilité de décès : **5% par jour au-delà du 5ᵉ jour**.
   - Ce risque est divisé par **2** si un médecin est présent sur la même case.

---

### **Propagation entre citoyens**
1. **Malade ou cadavre dans un lieu :**
   - **10% de chance** de contaminer les autres citoyens présents.
   - **1% de chance** de contaminer les citoyens des terrains vagues voisins.

2. **Effet de la contamination sur les citoyens infectés :**
   - Leur niveau de contamination augmente de **0.01**.

---


    
