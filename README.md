
# TP OAuth2 - Application Spring Boot avec Authentification Google


##  Description

Ce projet démontre l'intégration de l'authentification OAuth2 avec Spring Boot, permettant aux utilisateurs de se connecter via leur compte Google. L'application utilise le protocole OpenID Connect (OIDC) pour récupérer les informations du profil utilisateur.

##  Objectifs Pédagogiques

- Comprendre les principes du protocole OAuth2 et OpenID Connect
- Configurer une application Spring Boot en tant que client OAuth2
- Implémenter l'authentification avec Google OAuth2
- Extraire et afficher les informations du profil utilisateur
- Maîtriser le flux complet d'autorisation OAuth2

## Architecture

```
Application Spring Boot (Client OAuth2)
         ↓
    Google OAuth2 (Fournisseur d'identité)
         ↓
    Token d'accès + ID Token
         ↓
    Informations utilisateur (profil)
```

##  Structure du Projet

```
oauth2-client/
├── src/
│   └── main/
│       ├── java/
│       │   └── ma/
│       │       └── ens/
│       │           └── security/
│       │               ├── Oauth2ClientApplication.java
│       │               ├── config/
│       │               │   └── SecurityConfig.java
│       │               └── web/
│       │                   └── HomeController.java
│       └── resources/
│           ├── templates/
│           │   ├── index.html
│           │   └── profile.html
│           └── application.yml
├── pom.xml
└── README.md
```

##  Installation et Configuration

### Prérequis

- **Java 17** ou supérieur
- **Maven 3.6** ou supérieur
- **Compte Google** pour la configuration OAuth2

### 1. Cloner le projet

```bash
git clone <repository-url>
cd oauth2-client
```

### 2. Configuration Google OAuth2

#### Étape 1 : Créer un projet Google Cloud
1. Allez sur [Google Cloud Console](https://console.cloud.google.com/)
2. Créez un nouveau projet ou sélectionnez un existant
3. Activez l'API "Google Identity"

#### Étape 2 : Configurer l'écran de consentement OAuth
1. APIs & Services → OAuth consent screen
2. Type : "Externe"
3. Informations :
   - Nom de l'application : `TP OAuth2 Spring Boot`
   - Email de support : votre email
4. Ajoutez votre email comme "Test User"

#### Étape 3 : Créer les identifiants OAuth
1. APIs & Services → Credentials
2. Create Credentials → OAuth 2.0 Client IDs
3. Configuration :
   - Type d'application : "Application Web"
   - Nom : `spring-oauth2-client`
   - URI de redirection : `http://localhost:8080/login/oauth2/code/google`

#### Étape 4 : Récupérer les identifiants
Copiez le **Client ID** et **Client Secret** générés.

### 3. Configuration de l'application

Éditez le fichier `src/main/resources/application.yml` :

```yaml
server:
  port: 8080

spring:
  thymeleaf:
    cache: false
    
  security:
    oauth2:
      client:
        registration:
          google:
            client-id: votre-client-id.apps.googleusercontent.com
            client-secret: votre-client-secret
            scope:
              - openid
              - profile
              - email
```

### 4. Exécution

#### Avec Maven :
```bash
./mvnw spring-boot:run
```

#### Avec Java :
```bash
./mvnw clean package
java -jar target/oauth2-client-1.0.0.jar
```

#### Depuis IntelliJ IDEA :
- Ouvrez le projet dans IntelliJ
- Exécutez la classe `Oauth2ClientApplication`

## Utilisation

1. **Accédez à l'application** : http://localhost:8080
2. **Cliquez sur "Se connecter avec Google"**
3. **Authentifiez-vous** avec votre compte Google
4. **Autorisez l'application** à accéder à vos informations
5. **Visualisez votre profil** avec vos informations personnelles

## 🔧 Fonctionnalités

###  Implémentées
-  Authentification OAuth2 avec Google
-  Récupération du profil utilisateur (nom, email, photo)
-  Interface utilisateur responsive avec Bootstrap
-  Gestion de la déconnexion
-  Protection des routes avec Spring Security

###  Informations récupérées
- **Nom complet** de l'utilisateur
- **Adresse email**
- **Photo de profil**
- **Token d'identité** (JWT)

## Technologies Utilisées

- **Spring Boot 3.2.0** - Framework principal
- **Spring Security** - Authentification et autorisation
- **OAuth2 Client** - Intégration OAuth2
- **Thymeleaf** - Templates HTML
- **Bootstrap 5** - Interface utilisateur
- **Google OAuth2** - Fournisseur d'identité

##  Sécurité

- Validation automatique des tokens JWT par Spring Security
- Protection contre les attaques CSRF
- Gestion sécurisée des sessions
- Configuration des scopes minimaux requis

##  Dépannage

### Problèmes courants :

####  "Redirect URI mismatch"
**Solution** : Vérifiez que l'URI dans Google Cloud Console correspond exactement à :
```
http://localhost:8080/login/oauth2/code/google
```

####  "Application not verified"
**Solution** : Ajoutez votre email dans "Test users" de l'écran de consentement OAuth

####  Erreur 500 sur /profile
**Solution** : Vérifiez la syntaxe des templates Thymeleaf

####  Boucle de redirection
**Solution** : Vérifiez la configuration Spring Security dans `SecurityConfig.java`

### Logs de debug :

Activez les logs détaillés dans `application.yml` :
```yaml
logging:
  level:
    org.springframework.security: DEBUG
    ma.ens.security: DEBUG
```

## Concepts OAuth2 Expliqués

### Flux OAuth2 utilisé :
1. **Authorization Request** - Redirection vers Google
2. **User Consent** - Consentement de l'utilisateur
3. **Authorization Code** - Récupération du code
4. **Token Exchange** - Échange code contre tokens
5. **User Info** - Récupération du profil

### Tokens :
- **Access Token** : Accès aux ressources protégées
- **ID Token** (JWT) : Informations d'identité utilisateur

### Démonstration


<img width="955" height="431" alt="supr2" src="https://github.com/user-attachments/assets/8298bf2e-9c88-4ac4-8ccf-28e9e722217b" />



https://github.com/user-attachments/assets/08b3336e-93d0-4d3e-9bb8-235a157091ce




https://github.com/user-attachments/assets/d32d5f71-da25-4bcb-a05e-2cdc0b92f96c



##  Auteurs

- **AICHA BARAHOU** 






