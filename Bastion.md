# Mise en place d'un bastion pour votre infrastructure

Les bastions permettent de centraliser la sécurité réseau via des connexions SSH. Ils vérifient les identifiants des utilisateurs et des appareils, et autorisent l’accès uniquement aux utilisateurs figurant sur des **listes d’autorisation**.

---

## Comparatif des solutions

| Solution    | Zero Trust | MFA  | RBAC | Audit | Multi-protocole | Complexité |
|-------------|------------|------|------|-------|-----------------|------------|
| Teleport    | ✅         | ✅   | ✅   | ✅    | ✅              | Moyenne    |
| Guacamole   | ❌         | ❌   | ✅   | ✅    | ✅              | Élevée     |

---

## **Teleport**

### ✅ Avantages
- **Zero Trust** : Authentification forte (MFA, certificats courts).
- **RBAC** : Contrôle d’accès granulaire (rôles, permissions).
- **Audit complet** : Enregistrement des sessions SSH et des commandes.
- **Multi-protocole** : SSH, Kubernetes, bases de données, applications web.
- **Intégration** : Compatible avec GitHub, GitLab, OIDC, LDAP.
- **Open-source** : Version gratuite complète (option entreprise payante).

### ❌ Inconvénients
- Courbe d’apprentissage pour la configuration initiale.
- Nécessite un serveur dédié pour le cluster Teleport.

---

## **Guacamole**

### ✅ Avantages
- **Accès multi-protocole** : SSH, RDP, VNC via un navigateur web.
- **Centralisation** : Interface unique pour gérer tous les accès.
- **Logs et audit** : Enregistrement des sessions.
- **Open-source** : Sous licence Apache 2.0.

### ❌ Inconvénients
- Configuration complexe (nécessite Tomcat, MySQL/PostgreSQL).
- Moins sécurisé que Teleport (pas de MFA natif, dépend de la configuration du reverse proxy).

---

## **Choix final : Teleport**
J’ai préféré choisir Teleport car cette solution me paraît plus sécurisée, surtout si elle doit être proposée à des clients. Elle est plus adaptée pour répondre aux exigences de l’ANSSI et de l’ISO 27001, ce qui constitue un gage de qualité pour nos infrastructures.
