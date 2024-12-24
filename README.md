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

    
