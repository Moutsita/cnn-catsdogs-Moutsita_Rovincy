# TP - CNN vs Transfert Learning (Chats vs Dogs)

## 1. Titre & Objectif du Projet

Ce projet compare l'efficacité de l'entraînement d'un CNN **à partir de zéro** (Expérience A) et l'utilisation du **Transfert Learning avec VGG-16** (Expérience B) pour la classification d'images (Chats vs Chiens). L'objectif est d'analyser l'impact de ces méthodes sur la convergence, la performance (Accuracy, Precision, Recall) et le temps d'exécution sur GPU.

## 2. Environnement & Dépendances

Le projet a été exécuté sur un Notebook **Kaggle** avec **accélération GPU**. Les dépendances sont listées dans `requirements.txt`.

**Installation :** `pip install -r requirements.txt`

## 3. Organisation des Données

Le jeu de données "Cats vs Dogs" est utilisé. Les chemins ont été adaptés à la structure Kaggle (`/kaggle/input/dogs-vs-cats/`).

## 4. Commandes et Paramètres d'Entraînement

Les deux expériences ont été menées sur **10 époques** avec un `batch_size` de 32.

| Paramètre | Expérience A (Scratch) | Expérience B (Transfer Learning VGG-16) |
| :--- | :--- | :--- |
| **Architecture** | CNN simple (3 blocs conv) | VGG-16 (poids IMAGENET1K_V1) |
| **Optimiseur** | Adam ($\text{lr} = 0.001$) | Adam ($\text{lr} = 0.001$) sur les couches FC seulement |
| **Temps total (GPU)** | **13.5 minutes** | **68.5 minutes** |

---

## 5. Résultats, Comparaison et Analyse

### Tableau Récapitulatif des Performances (Test Final - Époque 10)

| Expérience | Modèle | Loss Finale (Test) | Acc Finale (Test) | Prec Finale (Test) | Rec Finale (Test) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **A** | CNN (*Scratch*) | **0.7877** | **0.7584** | **0.7584** | **0.7584** |
| **B** | VGG-16 (Transfer) | **0.1764** | **0.9328** | **0.9338** | **0.9318** |

### Courbes de Performance (Loss et Accuracy)

*(Insérer ici les images des deux graphiques générés par Matplotlib)* 

### Matrice de Confusion (Bonus)

*(Insérer ici l'image de la Matrice de Confusion finale de l'Expérience B)*

### Analyse Comparative (2-3 Paragraphes)

**1. Performance et Robustesse**
L'Expérience B (Transfer Learning) surpasse largement l'Expérience A. L'Expérience A a plafonné à **$75.84 \%$** d'Accuracy, indiquant que le modèle n'a pas réussi à extraire suffisamment de caractéristiques en 10 époques. En revanche, l'Expérience B a atteint une Accuracy de **$93.28 \%$** avec une Loss de seulement $0.1764$. Ce résultat confirme que les caractéristiques génériques apprises par VGG-16 sur ImageNet sont transférables et robustes pour la classification Chat/Chien, permettant un bond de performance de $\approx 17$ points d'Accuracy.

**2. Convergence et Efficacité Temporelle**
Bien que les deux expériences aient été lancées sur GPU, l'Expérience B a pris **cinq fois plus de temps** (68.5 min vs 13.5 min). Cela contredit le gain de temps typique du Transfer Learning sur CPU. **Cependant**, dans le contexte de notre TP initial, l'Expérience A sur **CPU prenait 7h 40min**, tandis que l'Expérience B est réalisable en environ une heure sur GPU. Le temps plus long de B sur GPU (par rapport à A sur GPU) est probablement dû à la complexité intrinsèque de VGG-16 et au plus grand nombre de paramètres dans les couches non gelées du classifieur que nous avons entraîné.

**3. Conclusion et Justification**
L'approche par Transfer Learning (Expérience B) est la plus efficace pour cette tâche, offrant une **qualité de résultat significativement supérieure** malgré le temps d'exécution plus long sur GPU. Les résultats valident la supériorité des modèles pré-entraînés, en particulier lorsque la performance est l'objectif principal.

## 6. Limites & Pistes d'Amélioration

* **Analyse du temps GPU :** Il serait pertinent d'analyser plus finement pourquoi VGG-16 a pris plus de temps que le petit CNN sur GPU.
* **Fine-Tuning** : Améliorer l'Expérience B en dégelant les dernières couches convolutionnelles du VGG-16 avec un très faible learning rate pour adapter davantage le modèle à la tâche.