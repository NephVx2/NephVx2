# Salut, je suis Nephren 👋

🇬🇧 [English version](README.md)

Bonjour à tous ; hello everyone. Je développe des outils PowerShell pour Windows 11 — audits de sécurité, renforcement de la confidentialité, et maintenance système — pour ceux qui veulent savoir *exactement* ce qu'un script a touché sur leur machine, pas juste faire confiance parce que "ça a l'air d'avoir marché."

Chaque script ici suit les mêmes règles maison : un mode `-SelfTest` intégré qui valide la logique du script avant de le lancer pour de vrai, aucune auto-élévation silencieuse, et une signature de code là où la diffusion le justifie. Si un script te dit que ton système est sain, c'est parce qu'un seuil documenté l'a dit — pas une impression.

---

### 🧰 Ce qu'on trouve ici

| Repository | Ce que ça fait |
|---|---|
| 🌶️ [**SpicyCheck**](https://github.com/NephVx2/SpicyCheck) | Maintenance Windows 11 en une commande — diagnostic de santé à 16 points, nettoyage, réparation DISM/SFC/BCD bilingue FR/EN, optimisation disques, rapport HTML. Self-test à 36 assertions. |
| 🩺 [**Check-Security**](https://github.com/NephVx2/Check-Security) | Audit de sécurité Windows 11 en lecture seule — 22 sections (pare-feu, BitLocker, Defender, TLS/SCHANNEL, VBS, certificats...), score pondéré par catégorie, alertes de régression entre les runs, filtrable par section via `-Category`. Self-test à 48 assertions. |
| 🔒 [**Harden-TLS**](https://github.com/NephVx2/Harden-TLS) | Ton PC accepte encore TLS 1.0 et toute une pile de reliques de chiffrement des années 90 — un script ferme tout ça définitivement : protocoles, chiffrements, hachages, Diffie-Hellman, .NET Strong Crypto. Se vérifie lui-même avant de toucher à quoi que ce soit, annulation en un clic. Self-test à 17 assertions. |
| 🛰️ [**Block-Telemetry**](https://github.com/NephVx2/Block-Telemetry) | Bloque la télémétrie via le fichier hosts — 228 domaines, 15 catégories (Microsoft, Edge, Copilot, Adobe, Google, Brave et plus). Liste blanche codée en dur, mode simulation, vérificateur d'intégrité. Self-test à 8 assertions. |
| 🦁 [**Brave-Debloat**](https://github.com/NephVx2/Brave-Debloat) | Applique 53 stratégies de groupe Brave pour la confidentialité et la sécurité — sauvegarde/restauration, détection de conflits, rapport HTML. Self-test à 21 assertions. |
| 🧹 [**Windows-Preflight-Cleaner**](https://github.com/NephVx2/Windows-Preflight-Cleaner) | Script de maintenance autonome — 46+ caches système/applicatifs, logs, fichiers temporaires et WinSxS via DISM, purge DNS, corbeille. Mode simulation (dry-run) inclus. |
| 🧭 [**Toolbox-Commands**](https://github.com/NephVx2/Toolbox-Commands) | Accès en un clic à 145 commandes Windows réparties en 9 catégories — recherche, favoris, confirmation avant les commandes sensibles, self-test à 47 assertions. |

---

### 🎨 Aussi ici

Pas du PowerShell, mais un autre genre de projet perso :

- 🦅 [**fastfetch-ricing**](https://github.com/NephVx2/fastfetch-ricing) — une config Fastfetch pour terminaux Windows 11 / PowerShell compatibles Sixel, sections Hardware/Software/Session/Uptime, barres de progression, et un emplacement pour un logo personnalisé.
- 🎧 [**Spicetify-tui**](https://github.com/NephVx2/Spicetify-tui) — un thème Spicetify façon terminal pour Spotify, labels de panneaux, bannière ASCII, TokyoNight par défaut.

---

### 🛠️ Comment ces scripts sont construits

- **Self-testés** — la plupart des scripts embarquent un mode `-SelfTest` (ou équivalent) : des dizaines d'assertions internes qui confirment que les binaires, cmdlets et fonctions requis fonctionnent *avant* de toucher au système.
- **Score transparent** — les statuts de santé/sécurité reposent toujours sur un seuil documenté et explicite. Pas de boîte noire "fais-moi confiance."
- **Bilingue là où ça compte** — le français et l'anglais sont tous les deux traités sérieusement ; la logique de détection qui lit la sortie système (DISM, SFC...) est vérifiée dans les deux langues, pas seulement en anglais.
- **Signés là où c'est indiqué** — certains scripts portent un certificat de signature de code personnel auto-signé (vérifiable en bas du `.ps1`, présence d'un bloc `SIG # Begin signature block`) ; d'autres ne sont pas signés du tout. Dans les deux cas, voir ci-dessous ce que ça change concrètement au lancement.
- **Conscients des droits admin, pas avides d'admin** — les scripts qui ont besoin d'élévation l'exigent explicitement ; aucun ne s'auto-élève silencieusement.

---

### 🔓 Lancer un script téléchargé

N'importe quel `.ps1` téléchargé depuis ces repos sera marqué par Windows comme provenant de « la zone Internet » (le Mark of the Web). Sous la politique d'exécution courante `RemoteSigned`, cette marque bloque l'exécution du script — **qu'il soit signé ou non** :

- **Les scripts signés** ici utilisent un certificat personnel auto-signé. Sa racine de confiance n'est pas installée sur ta machine — contrairement à un certificat émis par une autorité de certification publique, il ne fera donc pas considérer le fichier comme provenant d'un « éditeur de confiance » par Windows. La signature prouve surtout que le fichier n'a pas été modifié après que je l'ai signé, pas que ta machine doit lui faire confiance par défaut.
- **Les scripts non signés** subissent le même blocage lié à la zone Internet, pour la raison plus simple qu'il n'y a même pas de certificat à essayer d'approuver.

La correction est identique dans les deux cas — choisis celle qui te convient :

```powershell
# Option A - retirer le marqueur "telecharge depuis Internet" (une seule fois, permanent)
Unblock-File .\nom-du-script.ps1

# Option B - contourner la politique pour un seul lancement, sans toucher au fichier
powershell -ExecutionPolicy Bypass -File .\nom-du-script.ps1
```

**Option C — sans PowerShell :** clic droit sur le fichier `.ps1` → *Propriétés* → dans l'onglet *Général*, coche **"Débloquer"** à côté de la mention de sécurité ("Ce fichier provient d'un autre ordinateur...") → *OK*. Ça fait exactement la même chose que `Unblock-File`, juste depuis l'explorateur de fichiers.

`Unblock-File` (ou la case ci-dessus) retire uniquement le marqueur sur ce fichier précis — ça ne modifie ni la politique d'exécution du système, ni aucun autre script. Lis un script avant de le débloquer et de le lancer, surtout en tant qu'Administrateur.

---

### 📬 Me contacter

Un bug trouvé, ou un message Windows en français que mes scripts ne reconnaissent pas encore ? Ouvre une issue sur le repo concerné — c'est exactement le genre de retour qui améliore ces outils.

<sub>PowerShell · Windows 11 · Sécurité & Confidentialité · Self-testés, signés, bilingues.</sub>
