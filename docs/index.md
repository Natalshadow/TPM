# TPM — Trusted Platform Module

## Définition

Le **TPM** (*Trusted Platform Module*, ou **module de plateforme sécurisée**) est un composant de sécurité conçu pour fournir des fonctions cryptographiques et protéger certaines informations sensibles d'un ordinateur.

Il permet notamment de générer et de protéger des clés cryptographiques, de vérifier certains éléments de l'intégrité du système au démarrage et de fournir une base matérielle de confiance au système d'exploitation.

Le TPM est aujourd'hui principalement utilisé sous la forme **TPM 2.0** sur les ordinateurs modernes.

Il existe trois types de TPM: discret, intégré ou firmware, ce qui affecte le terme UEFI.

---

## À quoi sert un TPM ?

Le TPM peut être utilisé pour plusieurs fonctions de sécurité :

* protéger des clés cryptographiques ;
* stocker de manière sécurisée certaines informations d'authentification ;
* participer au chiffrement du disque avec **BitLocker** ;
* participer à l'authentification avec **Windows Hello** ;
* mesurer certains éléments du processus de démarrage ;
* contribuer à l'établissement d'une chaîne de confiance lors du démarrage du système.

L'idée générale est de disposer d'un composant matériel ou intégré à la plateforme qui puisse effectuer certaines opérations de sécurité sans avoir à exposer directement les clés protégées au système d'exploitation.

---

## Comment fonctionne le TPM ?

Le TPM dispose de capacités cryptographiques et d'un espace de stockage sécurisé.

Il peut notamment :

1. générer des clés cryptographiques ;
2. protéger certaines clés contre une extraction directe ;
3. effectuer des opérations cryptographiques ;
4. enregistrer des mesures liées au démarrage du système ;
5. fournir des informations permettant à certains mécanismes de sécurité de vérifier l'état de la plateforme.

Le TPM n'est donc pas un simple espace de stockage. Il peut effectuer lui-même certaines opérations cryptographiques et contrôler l'utilisation des informations qu'il protège.

---

## TPM et démarrage du système

Le TPM peut participer au **Measured Boot** (*démarrage mesuré*).

Lors du démarrage, différents éléments du système peuvent être mesurés, par exemple certains composants du processus de démarrage.

Ces mesures sont enregistrées dans des registres appelés **PCR** (*Platform Configuration Registers*).

L'objectif est de pouvoir conserver une trace cryptographique de l'état de la plateforme au cours du démarrage.

Cela peut ensuite être utilisé par d'autres mécanismes de sécurité pour déterminer si la plateforme se trouve dans un état attendu.

!!! note

```
Le TPM ne remplace pas le BIOS/UEFI et ne démarre pas lui-même l'ordinateur. Il fournit des fonctions de sécurité utilisées par la plateforme et le système d'exploitation.
```

---


## TPM 2.0

Le **TPM 2.0** est la version actuellement utilisée par les systèmes modernes.

Windows 11 impose notamment la présence d'un TPM 2.0 parmi ses exigences matérielles.



---

## TPM ≠ Secure Boot

Le TPM et le **Secure Boot** sont deux mécanismes différents qui peuvent fonctionner ensemble.

| Mécanisme       | Rôle principal                                                             |
| --------------- | -------------------------------------------------------------------------- |
| **TPM**         | Protection de clés et fonctions cryptographiques, mesures de la plateforme |
| **Secure Boot** | Vérification de la signature des composants autorisés à démarrer           |
| **BitLocker**   | Chiffrement des données                                                    |
| **UEFI**        | Firmware chargé avant le système d'exploitation                            |

### Exemple

Lors du démarrage d'un PC Windows :

```text
UEFI
  │
  ├── Secure Boot
  │     └── Vérifie les composants de démarrage
  │
  └── TPM
        └── Protège des informations cryptographiques
              et enregistre certaines mesures
                    │
                    ▼
             Windows
                    │
                    ▼
              BitLocker
```

Ces mécanismes ont donc des rôles différents mais complémentaires.



## Exemple concret

Prenons un ordinateur portable professionnel équipé d'un TPM 2.0.

Un utilisateur active **BitLocker** sur son disque système.

Le scénario simplifié peut être représenté ainsi :

```text
          Démarrage du PC
                 │
                 ▼
              UEFI
                 │
                 ├── Secure Boot
                 │
                 ▼
                TPM
                 │
        Vérification des mesures
                 │
                 ▼
       Protection des clés BitLocker
                 │
                 ▼
              Windows
```

Le TPM contribue ainsi à empêcher qu'une clé protégée soit simplement récupérée et utilisée ailleurs dans certaines situations.

---



## En résumé

Le **TPM (Trusted Platform Module)** est un composant de sécurité permettant notamment de :

* protéger des clés cryptographiques ;
* effectuer certaines opérations cryptographiques ;
* participer à la mesure du processus de démarrage ;
* protéger des informations utilisées par BitLocker ;
* participer à l'authentification avec Windows Hello ;
* fournir une base matérielle de confiance pour certaines fonctions de sécurité.

Le TPM constitue donc **une brique de sécurité de la plateforme**, et non une solution de sécurité complète à lui seul.

---

## Sources

* [Microsoft Learn — Vue d'ensemble du module de plateforme sécurisée (TPM)](https://learn.microsoft.com/fr-fr/windows/security/hardware-security/tpm/trusted-platform-module-overview)
* [Microsoft Learn — Utilisation du TPM par Windows](https://learn.microsoft.com/fr-fr/windows/security/hardware-security/tpm/how-windows-uses-the-tpm)
* [Microsoft Support — Qu'est-ce qu'un TPM ?](https://support.microsoft.com/fr-fr/windows/qu-est-ce-qu-un-tpm-7f4f7f2f-5f9e-4f5b-9f0f-5f6f4c8c4f8d)
