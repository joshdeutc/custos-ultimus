# Custos Ultimus — Directives d'Action pour les Agents IA

Ce dépôt (**`custos-ultimus`**) est la variante dédiée administrée par Joshua (pour un appareil tiers / testée sur Samsung Galaxy A53 5G `RZCT30L9EGJ`), totalement isolée de **Custos Supremus** (`custos`) et de **Custos Studio** (`custos-studio`).

---

## 1. Identité & Isolation
* **Dépôt GitHub** : `github.com/joshdeutc/custos-ultimus`
* **Guardian (`:guardian`)** : `com.jo.custos.ultimus.guardian` (Device Owner — provisionnement : `adb shell dpm set-device-owner com.jo.custos.ultimus.guardian/com.jo.custos.guardian.GuardianAdminReceiver`)
* **Console UI (`:app`)** : `com.jo.custos.ultimus.app`
* **Clé de signature dédiée** : `micha-release.jks` (alias `micha-release`, Cold Storage sur clé USB externe uniquement, jamais stockée sur le PC ; configurée dans les secrets de l'environnement GitHub `production` de `joshdeutc/custos-ultimus`).
* **NE JAMAIS cibler le Pixel 8a (`100.104.70.72:5555`)** : ce dépôt cible uniquement les appareils de test (`RZCT30L9EGJ`) ou l'appareil cible dédié.

---

## 2. Sécurité & Invariants
1. **AUCUNE PORTE DÉROBÉE LOGICIELLE** : Pas de `REMOVE_OWNER`, pas de `clearDeviceOwnerApp`, pas de suppression de règles par ADB.
2. **ANTI-CONTOURNEMENT FACTORY RESET (Enterprise FRP)** : `FactoryResetProtectionPolicy` dans `GuardianEngine.kt` (`FRP_ADMIN_ACCOUNT_IDS`, 21-digit Google Gaia IDs) verrouille l'appareil sur le compte Google administrateur après toute réinitialisation, tout en préservant l'accès matériel au Recovery en cas de bootloop.
3. **IMMUNITÉ SYSTÈME ABSOLUE (Anti-Bootloop)** : Ne **JAMAIS** masquer (`setApplicationHidden`) ou suspendre (`setPackagesSuspended`) une application système (`FLAG_SYSTEM` / `FLAG_UPDATED_SYSTEM_APP`) ni `com.google.android.permissioncontroller`.
4. **CARAPACE & COUVRE-FEUX RÉSEAU** : Embarque toute la base `v1.27` (Carapace 3 s / 0 s au reboot, Couvre-feu Partage de connexion `@system:tethering`, Couvre-feu Internet total `@system:internet` via Always-On Blackhole VPN sans suspension d'app).
