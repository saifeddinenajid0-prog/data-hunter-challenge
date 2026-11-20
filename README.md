# Data Hunter Challenge — Collecte de données Web

Ce projet collecte des données sur trois sources Web, avec trois méthodes d'extraction différentes, puis compare ces méthodes. Les jeux de données obtenus serviront de base à un projet de Data Mining.

> Projet réalisé dans le cadre d'un TD de **Data Mining**.
> Auteur·e : *Saifeddine Najid* 

## Missions

| # | Méthode | Source | Données extraites | Sortie |
|---|---|---|---|---|
| 1 | Scraping statique : `requests` + `BeautifulSoup` | [books.toscrape.com](https://books.toscrape.com/) | titre, prix, disponibilité, note (1–5) | `data/books.csv` |
| 2 | API REST : `requests` | [Open Library Search API](https://openlibrary.org/dev/docs/api/search) | titre, auteur(s), année de 1re publication, identifiant | `data/openlibrary.csv` |
| 3 | Scraping dynamique : `Selenium` | [quotes.toscrape.com/js](https://quotes.toscrape.com/js/) | citation, auteur, tags | `data/quotes.csv` |

## Points techniques

- **Pagination automatique** : le programme suit le lien *next* jusqu'au nombre de pages voulu.
- **Conversion en valeurs numériques** : `£51.77` devient `51.77` et la classe CSS `star-rating Three` devient `3`.
- **Paramètres de requête API** (`q`, `fields`, `limit`), **vérification du statut HTTP** et **gestion des champs manquants**.
- **Contenu généré par JavaScript** : `WebDriverWait` attend le chargement, `staleness_of` détecte le changement de page, et `try/finally` + `driver.quit()` ferment proprement le navigateur.
- **Audit qualité** des trois jeux (doublons, valeurs manquantes) et propositions de prétraitement.

## Comparaison des méthodes

| | Requests + BS4 | API REST | Selenium |
|---|---|---|---|
| Source | HTML statique | JSON | HTML généré par JS |
| Vitesse | Rapide | Très rapide | Lente |
| Robustesse | Moyenne | Élevée | Faible |
| Quand l'utiliser | Pages simples sans API | Dès qu'une API existe | Contenu dynamique, interactions |

## Lancer le projet

```bash
git clone https://github.com/saifeddinenajid0-prog/data-hunter-challenge.git
cd data-hunter-challenge
pip install -r requirements.txt
```

Ouvre ensuite `data_hunter_challenge.ipynb` dans VS Code ou Jupyter, puis exécute les cellules dans l'ordre.

La mission 3 nécessite **Firefox**. Le notebook utilise `geckodriver` s'il le trouve au chemin défini par `GECKODRIVER_PATH`. Sinon, Selenium Manager (Selenium ≥ 4.6) télécharge automatiquement le bon driver.

## Structure

```
data-hunter-challenge/
├── data_hunter_challenge.ipynb   # notebook des 3 missions + conclusion
├── data/
│   ├── books.csv
│   ├── openlibrary.csv
│   └── quotes.csv
├── requirements.txt
└── README.md
```

## Progression

- [x] Structure du projet
- [x] Mission 1 : scraping statique (books.csv)
- [x] Mission 2 : API Open Library (openlibrary.csv)
- [x] Mission 3 : scraping dynamique Selenium (quotes.csv)
- [ ] Audit qualité et conclusion
- [ ] Suite : prétraitement et premières analyses de Data Mining

## Stack

Python 3.12 · requests · BeautifulSoup4 · pandas · Selenium · Firefox/geckodriver · Jupyter
