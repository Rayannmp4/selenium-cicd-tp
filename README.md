# TP Selenium & CI/CD – Automatisation des Tests Web

## Structure du projet

### 1. Application web

### Application : Calculatrice Simple en HTML/CSS/JS

Addition, Soustraction, Multiplication, Division (gère division par zéro)

### 2. Tests automatisés avec Selenium
   
#### Installation des dépendances

Dans tests/requirements.txt :
```
selenium==4.15.0
pytest==7.4.3
pytest-html==4.1.1
webdriver-manager==4.0.1
```

Pour installer : 
```pip install -r requirements.txt```

cd tests
```python -m pytest test_selenium.py -v --html=report.html --self-contained-html```

### 3. CI/CD avec GitHub Actions
Fichier .github/workflows/ci-cd.yml :

```jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.9'
      - name: Install Chrome
        run: |
          sudo apt-get update
          sudo apt-get install -y google-chrome-stable
      - name: Install dependencies
        run: |
          cd tests
          pip install -r requirements.txt
      - name: Run Selenium Tests
        env:
          CI: true
        run: |
          cd tests
          python -m pytest test_selenium.py -v --html=../test-report.html --self-contained-html
      - name: Upload test results
        uses: actions/upload-artifact@v3
        if: always()
        with:
          name: test-results
          path: test-report.html
```
#### Auteur :
#### Rayann
#### TP Selenium & CI/CD - 2025
  

