# Salut, je suis Nephren 👋

🇬🇧 [English version](README.md)

Bonjour à tous ; hello everyone. Je développe des outils PowerShell pour Windows 11 — audits de sécurité, renforcement de la confidentialité, et maintenance système — pour ceux qui veulent savoir *exactement* ce qu'un script a touché sur leur machine, pas juste faire confiance parce que "ça a l'air d'avoir marché."

Chaque script ici suit les mêmes règles maison : un mode `-SelfTest` intégré qui valide la logique du script avant de le lancer pour de vrai, aucune auto-élévation silencieuse, et une signature de code là où la diffusion le justifie. Si un script te dit que ton système est sain, c'est parce qu'un seuil documenté l'a dit — pas une impression.

---

### 🧰 Ce qu'on trouve ici

| Repository | Ce que ça fait |
|---|---|
| 🌶️ [**SpicyCheck-v7.2**](https://github.com/NephVx2/SpicyCheck-v7.2) | Maintenance Windows 11 en une commande — diagnostic de santé à 16 points, nettoyage, réparation DISM/SFC/BCD bilingue FR/EN, optimisation disques, rapport HTML. Self-test à 36 assertions. |
| 🩺 [**Windows-Check-Security**](https://github.com/NephVx2/Windows-Check-Security) | Audit de sécurité Windows 11 en lecture seule — 22 sections (pare-feu, BitLocker, Defender, TLS, VBS, certificats...), score pondéré par catégorie, alertes de régression entre les runs. |
| 🧹 [**Windows-Preflight-Cleaner**](https://github.com/NephVx2/Windows-Preflight-Cleaner) | Script de maintenance autonome — 46+ caches système/applicatifs, logs, fichiers temporaires et WinSxS via DISM, purge DNS, corbeille. Mode simulation (dry-run) inclus. |
| 🔒 [**Harden-TLS**](https://github.com/NephVx2/Harden-TLS) | Ton PC accepte encore TLS 1.0, obsolète depuis 2021 — un script ferme cette porte définitivement, se vérifie lui-même avant de toucher à quoi que ce soit, et ne réécrit jamais ce qui est déjà corrigé. |
| 🛰️ [**Windows-Block-Telemetry**](https://github.com/NephVx2/Windows-Block-Telemetry) | Bloque la télémétrie de Microsoft, AMD, Adobe, Spotify, Brave, Firefox, Google, Discord, Steam et plus, triée par catégorie. |
| 🦁 [**Brave-debloat**](https://github.com/NephVx2/Brave-debloat) | Nettoyage interactif des options superflues de Brave pour renforcer sécurité et confidentialité. |
| 🧭 [**Toolbox-Commands**](https://github.com/NephVx2/Toolbox-Commands) | Une boîte à outils graphique accompagnée d'un catalogue de commandes séparé — à placer dans le même dossier pour lancer un large éventail de commandes Windows depuis une seule fenêtre. |

---

### 🛠️ Comment ces scripts sont construits

- **Self-testés** — la plupart des scripts embarquent un mode `-SelfTest` (ou équivalent) : des dizaines d'assertions internes qui confirment que les binaires, cmdlets et fonctions requis fonctionnent *avant* de toucher au système.
- **Score transparent** — les statuts de santé/sécurité reposent toujours sur un seuil documenté et explicite. Pas de boîte noire "fais-moi confiance."
- **Bilingue là où ça compte** — le français et l'anglais sont tous les deux traités sérieusement ; la logique de détection qui lit la sortie système (DISM, SFC...) est vérifiée dans les deux langues, pas seulement en anglais.
- **Signés** — les scripts sont signés numériquement via un certificat de signature de code personnel là où la diffusion le justifie.
- **Conscients des droits admin, pas avides d'admin** — les scripts qui ont besoin d'élévation l'exigent explicitement ; aucun ne s'auto-élève silencieusement.

---

### 📬 Me contacter

Un bug trouvé, ou un message Windows en français que mes scripts ne reconnaissent pas encore ? Ouvre une issue sur le repo concerné — c'est exactement le genre de retour qui améliore ces outils.

<sub>PowerShell · Windows 11 · Sécurité & Confidentialité · Self-testés, signés, bilingues.</sub>
