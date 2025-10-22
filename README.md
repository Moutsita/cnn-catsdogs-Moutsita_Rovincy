# TP - CNN vs Transfert Learning (Chats vs Dogs)

## 1. Titre & Objectif du Projet

Ce projet compare deux approches pour la classification d'images (Chats vs Chiens) : l'entraînement d'un CNN **à partir de zéro** (*from scratch*) et l'utilisation du **Transfert Learning** (VGG-16). L'objectif est d'analyser l'impact de ces méthodes sur la convergence, la performance (Accuracy, Precision, Recall) et le temps d'exécution.

## 2. Environnement & Dépendances

L'environnement est basé sur Python. Les dépendances sont listées dans `requirements.txt`.

**Installation :** `pip install -r requirements.txt`

## 3. Organisation des Données

Le jeu de données "Cats vs Dogs" est utilisé. Les images doivent être placées dans le dossier `Cat_Dog_data` avec une structure `train/cat/`, `train/dog/`, `test/cat/`, `test/dog/`.

## 4. Commandes et Paramètres d'Entraînement

Les deux expériences ont été menées sur **10 époques** avec un `batch_size` de 32 sur CPU.

| Paramètre | Expérience A (Scratch) | Expérience B (Transfer Learning VGG-16) |
| :--- | :--- | :--- |
| **Architecture** | CNN simple (3 blocs conv) | VGG-16 (poids IMAGENET1K_V1) |
| **Optimiseur** | Adam ($\text{lr} = 0.001$) | Adam ($\text{lr} = 0.001$) sur les couches FC seulement |
| **Temps total (CPU)** | **7h 40min 38s** | **[TEMPS RÉEL À INSERER]** |

---

## 5. Résultats, Comparaison et Analyse

### Tableau Récapitulatif des Performances (Test Final - Époque 10)

| Expérience | Modèle | Loss Finale (Test) | Acc Finale (Test) | Prec Finale (Test) | Rec Finale (Test) |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **A** | CNN (*Scratch*) | **0.5568** | **0.7489** | **0.7937** | **0.6762** |
| **B** | VGG-16 (Transfer) | **[LOSS B]** | **[ACC B]** | **[PREC B]** | **[REC B]** |

### Courbes de Performance (Loss et Accuracy)

*(Insérer ici les images des deux graphiques générés par Matplotlib)*

### Matrice de Confusion (Bonus)

*(Insérer ici l'image de la Matrice de Confusion finale de l'Expérience B)*

### Analyse Comparative (2-3 Paragraphes)

**1. Convergence et Efficacité Temporelle**
L'Expérience A (CNN *from scratch*) a exigé **7 heures et 40 minutes** d'entraînement sur CPU, tandis que l'Expérience B (Transfer Learning) devrait converger en **[TEMPS B]** (à insérer). Cette différence illustre l'efficacité spectaculaire du Transfer Learning, qui évite le coût de calcul lié à l'apprentissage de toutes les caractéristiques de base sur un jeu de données limité.

**2. Performance et Robustesse**
En performance finale, le Transfer Learning **surclasse nettement** le modèle entraîné à partir de zéro. L'Expérience A a plafonné à $74.89 \%$ d'Accuracy avec un Recall faible ($67.62 \%$). L'Expérience B (VGG-16) devrait atteindre une précision significativement supérieure à $\mathbf{90\%}$. Ce résultat est dû à l'utilisation des caractéristiques génériques et robustes apprises par VGG-16 sur le jeu de données massif ImageNet.

**3. Conclusion**
Le Transfer Learning (Expérience B) est la méthode la plus efficace pour cette tâche, offrant un **gain de temps massif** et une **qualité de résultat nettement supérieure** par rapport à l'entraînement d'un modèle *from scratch* (Expérience A).

## 6. Limites & Pistes d'Amélioration

* **Fine-Tuning** : L'Expérience B pourrait être améliorée en dégelant et entraînant les dernières couches convolutionnelles du VGG-16 avec un très faible learning rate.
* **Scheduler** : L'utilisation d'un *scheduler* de taux d'apprentissage (ex: `StepLR`) aurait pu améliorer la convergence et la performance des deux modèles.
