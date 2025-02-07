# Intégration Paystack avec Django

## 🚀 Introduction

Ce projet fournit une implémentation complète de l'intégration Paystack dans une application Django, offrant une API RESTful robuste pour gérer les transactions de paiement.

## 📋 Prérequis

- Python 3.8+
- Django 3.2+
- Django Rest Framework
- Requests library

## 🔧 Installation

### 1. Cloner le dépôt

```bash
git clone https://votre-repository.git
cd votre-projet
```

### 2. Créer un environnement virtuel

```bash
python -m venv venv
source venv/bin/activate  # Sur Windows: venv\Scripts\activate
```

### 3. Installer les dépendances

```bash
pip install -r requirements.txt
```

### 4. Configuration

#### Variables d'environnement

Créez un fichier `.env` à la racine du projet :

```env
PAYSTACK_SECRET_KEY=your_paystack_secret_key
PAYSTACK_PUBLIC_KEY=your_paystack_public_key
PAYSTACK_CALLBACK_URL=https://votre-site.com/payment/callback
```

#### Configuration Django

Dans `settings.py`, ajoutez :

```python
INSTALLED_APPS = [
    ...
    'rest_framework',
    'votre_app_paystack',
]

PAYSTACK_SECRET_KEY = os.getenv('PAYSTACK_SECRET_KEY')
PAYSTACK_PUBLIC_KEY = os.getenv('PAYSTACK_PUBLIC_KEY')
PAYSTACK_CALLBACK_URL = os.getenv('PAYSTACK_CALLBACK_URL')
```

## 🛠 Fonctionnalités

- Initialisation de transactions
- Vérification de paiements
- Remboursements
- Gestion des transactions
- Persistance des données

## 📘 Utilisation

### Initialiser une Transaction

```python
from votre_app.views import PaystackTransactionViewSet

# Via API REST
POST /transactions/initialize/
{
    "amount": 50000,  # 500.00 naira
    "email": "client@example.com"
}

# Dans le code
paystack_service = PaystackService()
transaction = paystack_service.initialize_transaction(
    amount=50000, 
    email='client@example.com'
)
```

### Vérifier une Transaction

```python
# Via API REST
POST /transactions/verify/
{
    "reference": "TXN-référence-unique"
}

# Dans le code
result = paystack_service.verify_transaction(reference)
```

### Remboursement

```python
# Via API REST
POST /transactions/refund/
{
    "reference": "TXN-référence-unique"
}

# Dans le code
refund_result = paystack_service.refund_transaction(reference)
```

## 🔒 Sécurité

- Utilisation de variables d'environnement
- Gestion des exceptions
- Logging des erreurs
- Validation des données

## 📊 Modèle de Transaction

Le modèle `Transaction` offre les statuts suivants :
- `pending`: Transaction en attente
- `initialized`: Transaction initialisée
- `successful`: Paiement réussi
- `failed`: Paiement échoué
- `refunded`: Transaction remboursée

## 🧪 Tests

```bash
python manage.py test votre_app_paystack
```

## 🔗 Webhooks

Pour implémenter les webhooks Paystack :
1. Créez une vue pour gérer les événements
2. Validez la signature Paystack
3. Traitez les différents types d'événements

## 🚧 Limitations

- Nécessite un compte Paystack actif
- Dépend de la disponibilité de l'API Paystack

## 🤝 Contributions

Les contributions sont les bienvenues ! Merci de suivre ces étapes :
1. Fork du dépôt
2. Créez une branche de fonctionnalité
3. Commitez vos modifications
4. Poussez et créez une Pull Request

## 📜 Licence

Aucune

## 📞 Support

En cas de problèmes :
- Vérifiez la documentation Paystack
- Consultez les issues du dépôt
- Contactez le mainteneur du projet