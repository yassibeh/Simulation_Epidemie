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

### **Rôles des pompiers**
1. **Décontamination :**
   - Les pompiers peuvent décontaminer les **citoyens** et les **lieux**.
   - **Règles :**
     - Chaque citoyen présent voit son niveau de contamination diminuer de **20%** par tour.
     - Une fois les citoyens décontaminés, le pompier diminue le niveau de contamination du lieu de **20%** par tour.
     - Priorité : **Citoyens d’abord**, lieu ensuite.
     - Le pompier utilise **1/10 de la capacité de son pulvérisateur par tour**.
     - ### **Règle du pulvérisateur**
        - Chaque pompier dispose d’un **pulvérisateur** avec une **capacité maximale** (par exemple, 1000 unités).
        - À chaque tour, un pompier peut utiliser **jusqu’à 1/10 de cette capacité totale**, soit **10% de la capacité totale**.
        - Chaque unité utilisée sert à décontaminer soit :
          - Les citoyens présents sur la case.
          - Le lieu (après avoir décontaminé les citoyens).
     - ### **Formule pour la consommation**
        1. Capacité totale initiale : \( \text{Capacité\_totale} \).
        2. Limite par tour : \( \text{Limite\_tour} = \text{Capacité\_totale} \times 0.1 \).
        
        - À chaque tour :
        - Si   Consommation_citoyens+Consommation_lieu≤Limite_tourConsommation_citoyens+Consommation_lieu≤Limite_tour, tout est traité.
        - Sinon, la décontamination est partielle (priorité aux citoyens).

2. **Brûler les corps :**
   - Dès qu’un pompier entre sur une case, tous les cadavres présents sont brûlés en **1 tour**.

3. **Protection contre la contamination :**
   - La tenue de protection du pompier limite l’augmentation de sa contamination :
     - Le pompier est contaminé **10 fois moins vite** par le niveau de contamination du lieu.
   - Le pompier est protégé contre la contamination d’autres citoyens :
     - **70% des cas** : Le virus d’un citoyen contaminé ne traverse pas la tenue.

---

### **Étapes clés à traduire en code**
#### 1. Décontamination des citoyens
- Parcourir la liste des citoyens présents sur la case.
- Réduire leur niveau de contamination de **20%** :
  \[
  C_{\text{citoyen\_nouveau}} = C_{\text{citoyen}} \times 0.8
  \]
- Réduire la capacité du pulvérisateur de **10%** par tour.

#### 2. Décontamination du lieu
- Une fois les citoyens décontaminés, réduire la contamination du lieu de **20%** :
  \[
  C_{\text{lieu\_nouveau}} = C_{\text{lieu}} \times 0.8
  \]

#### 3. Brûler les corps
- Réinitialiser le compteur de cadavres à **0** pour la case.

#### 4. Gestion de la contamination du pompier
- **Contamination par le lieu :**
  - L’augmentation est réduite par un facteur de 10 :
    \[
    C_{\text{pompier\_nouveau}} += C_{\text{lieu}} \times 0.002
    \]
- **Contamination par les citoyens :**
  - Tirer un nombre aléatoire entre 0 et 1.
  - Si ce nombre est supérieur à **0.3** (donc 70% de protection), le pompier n’est pas contaminé.

---


---

### **Rôles et comportements des médecins**
1. **Gestion des pochettes de soins :**
   - En début de partie :
     - **5 pochettes de soins** si le médecin est hors de l’hôpital.
     - **10 pochettes de soins** si le médecin est dans un hôpital.
   - En entrant dans un hôpital, un médecin reçoit **10 pochettes supplémentaires**.

2. **Soins des malades :**
   - Un médecin peut **soigner un seul malade par jour.**
   - Il soigne toujours **le citoyen le plus malade** (avec le niveau de contamination le plus élevé) sur sa case.
   - S’il se trouve dans un hôpital, il n’a pas besoin d’utiliser de pochette pour soigner.

3. **Auto-soin :**
   - Si le médecin est malade, il ne peut soigner personne.
   - Si le médecin est malade depuis **moins de 10 jours**, il peut s’auto-soigner en utilisant une pochette de soins.
   - Au-delà de **10 jours**, il est trop faible pour s’auto-soigner.

4. **Retour à l’hôpital :**
   - Un médecin qui quitte un hôpital ne peut y retourner avant **au moins 2 jours.**


### **Exemple concret** :
#### Situation :
- 3 citoyens sur une case :
  - Citoyen 1 : Contamination = 80%, malade.
  - Citoyen 2 : Contamination = 60%, malade.
  - Citoyen 3 : Contamination = 50%, en bonne santé.
- Le médecin :
  - Hors de l’hôpital.
  - Dispose de 5 pochettes de soins.

#### **Étapes du tour :**
1. Le médecin cherche le citoyen le plus malade :
   - Citoyen 1 (80%) est prioritaire.

2. Le médecin utilise une pochette pour soigner Citoyen 1 :
   - Citoyen 1 est guéri (contamination = 0).
   - Nombre de pochettes restantes : 4.

3. Si le médecin est malade depuis moins de 10 jours, il peut s’auto-soigner en consommant une pochette.

Settings

journaliste.note
pompiers .note
medecin.note
pulvérisateur.note
Untitled document 9.note
Untitled document 7.note
Untitled document 8.note
Untitled document 6.note
Untitled document 5.note
Untitled document 4.note
Untitled document 3.note
lettre de motivation_version canva.note
lettre de motivation.note
remarque cv .note
Projets_lunix_embarqués.note
Hobbies.note
Cv _version 2.note
cv_complet.note
langue et hobbies etc.note
Profil&interet.note

        Formations_final.note

Notes
Saved just now

Selection deleted
---
### **Rôles et responsabilités des journalistes**
1. **Transmission de dépêches à chaque tour :**
   - Les dépêches incluent des informations sur :
     - **Nombre de citoyens en bonne santé** (priorité : 6).
     - **Nombre de malades** (priorité : 7).
     - **Nombre de cadavres** (priorité : 8).
     - **Nombre de corps brûlés** (priorité : 9).
     - **Niveau moyen de contamination de la ville** (priorité : 5).
     - **Taux de contamination personnel** du journaliste (priorité : 1).

2. **Récupération des données :**
   - Les journalistes accèdent à ces informations via une **structure de mémoire partagée**.

3. **Priorité des informations :**
   - Les dépêches sont transmises selon un ordre de priorité.
   - Une file de messages unique est utilisée pour envoyer ces données.

---

standard
Rôles et responsabilités des journalistes

    Transmission de dépêches à chaque tour :
        Les dépêches incluent des informations sur :
            Nombre de citoyens en bonne santé (priorité : 6).
            Nombre de malades (priorité : 7).
            Nombre de cadavres (priorité : 8).
            Nombre de corps brûlés (priorité : 9).
            Niveau moyen de contamination de la ville (priorité : 5).
            Taux de contamination personnel du journaliste (priorité : 1).
    Récupération des données :
        Les journalistes accèdent à ces informations via une structure de mémoire partagée.
    Priorité des informations :
        Les dépêches sont transmises selon un ordre de priorité.
        Une file de messages unique est utilisée pour envoyer ces données.




    
