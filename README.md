# simple-devcontainer

Ein minimaler Devcontainer für die Arbeit mit agentenorientierten CLI-Tools in einer sauberen Ubuntu-Umgebung.

## Inhalt

Der Container basiert auf:

```text
mcr.microsoft.com/devcontainers/base:ubuntu
```

Beim Erstellen des Containers werden installiert:

- Node.js 24.x
- `@anthropic-ai/claude-code`
- `@openai/codex`
- Google Antigravity CLI

Außerdem wird der globale npm-Prefix auf `~/.npm-global` gesetzt und der `PATH` in der Shell erweitert:

```bash
export PATH=$HOME/.local/bin:$HOME/.npm-global/bin:$PATH
```

## Verwendung

Repository in VS Code oder einem anderen Dev-Containers-kompatiblen Editor öffnen und den Container neu bauen.

In VS Code:

1. Repository-Ordner öffnen.
2. `Dev Containers: Reopen in Container` ausführen.
3. Warten, bis das `postCreateCommand` abgeschlossen ist.

Beispiel per CLI:

```bash
code .
```

Danach in VS Code den Befehl `Dev Containers: Reopen in Container` ausführen.

Nach dem Container-Build sollten die installierten CLIs im Terminal verfügbar sein.

Versionen prüfen:

```bash
codex --version
claude --version
agy --version
```

## CLIs starten

Codex starten:

```bash
codex
```

Claude Code starten:

```bash
claude
```

Google Antigravity CLI starten:

```bash
agy
```

## Lokale private Repositories

Wenn private oder nur lokal benötigte Repositories innerhalb des Working Trees eines öffentlichen Repositories liegen sollen, sollten sie nicht als Submodule angelegt werden, solange sie nicht sichtbar sein sollen.

Stattdessen kann der lokale Ordner in `.git/info/exclude` des öffentlichen Repositories eingetragen werden:

```gitignore
/local-folder/
```

Beispiel:

```bash
printf "\n/local-folder/\n" >> .git/info/exclude
git clone git@github.com:example/private-repo.git local-folder
```

Diese Regel wird nicht committed und gilt nur für den aktuellen Clone. Das verschachtelte Repository kann innen normal mit Git genutzt werden, während das öffentliche Repository weder den Ordner noch dessen Remote-URL oder Inhalte trackt.

Nach dem Eintrag sollte der Status des öffentlichen Repositories geprüft werden:

```bash
git status --short
```

Der lokale Ordner sollte dort nicht auftauchen.
