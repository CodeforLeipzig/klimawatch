Sind die kommunalen Klimaschutzbemühungen (noch) im Plan?
Wir möchten eine einfach zu verstehende Homepage erstellen, welche diese Frage beantwortet.

Dazu wollen wir geplante Emissionsminderungsziele mit tatsächlichen Emissionsdaten
verknüpfen und für möglichst viele Kommunen Deutschland anzeigen.
Darüber hinaus wollen den Status einzelner Module von kommunalen
Klimaschutzkonzepten visualisieren.
Außerdem möchten wir die Ausbauziele der erneuerbaren Energien visualisieren.

[![Diskussion im Chat](https://img.shields.io/matrix/klimawatch:matrix.allmende.io?server_fqdn=matrix.allmende.io&label=Diskussion%20im%20Chat&style=for-the-badge)](https://matrix.to/#/#klimawatch:matrix.allmende.io)

# Wie kann ich die Daten meiner Kommune visualisieren?

In nur zwei Schritten: Du sammelst die Daten, wir visualisieren sie für Dich!
Hier gibt es [eine detaillierte Anleitung dazu](https://codeformuenster.org/klimawatch/hugo/anleitung).
Wer diesen Text hier liest: Wir freuen uns über [einen Pull Request](https://github.com/codeformuenster/klimawatch/pulls)!
Dann gerne

- mit der entsprechenden CSV-Datei (s. Anleitung) in den Ordner `data`
- den dazugehörigen Quellenangaben als README.md in den Ordner `docs/DEINEKOMMUNE`
- ggf. die mit dem Python-Skript automatisch erstellten Dateien:
    - `hugo/layouts/shortcodes/paris_DEINEKOMMUNE.html`
    - `hugo/layouts/data/you_draw_it_DEINEKOMMUNE_paris_data.json`
- ggf. die manuell angepasste Datei `content/kommunen/DEINEKOMMUNE.md` (gerne an `content/kommunen/template.md` orientieren)

Quellen nicht vergessen! Danke!

# Technisches

## Generierung der Grafiken:

Folgendes wurde alles mit `python3` getetest.
Benötigte Pakete installieren:

### Mit Conda

```
conda env create -f environment.yml
conda activate klimawatch
```
### Direkt mit pip

```
pip install plotly pandas numpy scipy --user
```

### Dann Plots generieren:

```
python generate_plots.py [kommune]
```

Dazu muss eine Datei mit dem Namen `kommune.csv` im Ordner `data` liegen.
Diese Datei sollte wie
[in der Anleitung beschrieben](https://codeformuenster.org/klimawatch/hugo/anleitung)
erstellt worden sein.
Wenn alles erfolgreich war, sollten

- eine Datei mit dem Namen `paris_[kommune].html`
  im Ordner `hugo/layouts/shortcodes/` und
- eine Datei `you_draw_it_[kommune]_paris_data.json` mit dem
  verbleibendem Parisbudget im Ordner `hugo/data/`

erstellt worden sein.

## Webseite bauen

Die Webseite wird mit dem static-site-generator `hugo` erstellt.
Deshalb, falls noch nicht geschehen, [`hugo` installieren](https://gohugo.io/)

Dann in den Ordner `hugo` gehen und mit

```
hugo server
```

`hugo` starten.
Nun sollte man mit einem Browser unter [localhost:1313](http://localhost:1313)
eine lokale Kopie der Webseite erreichen können.
Jede Änderung der zugrunde liegenden Dateien sollte live gezeigt werden.

### Inhalte der Webseite

Alle Content-Seiten werden als Markdown-Dateien verwaltet,
[hier findet sich eine Kurzreferenz](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

Für jede Kommune braucht man eine `content/kommunen/<kommune>.md` Datei.
Für eine neue Kommune bietet es sich an die Datei `content/kommunen/template.md`
zu kopieren und für die neue Kommune anzupassen.

Für übergreifende Seiten siehe die Beispielseiten `content/anleitung.md` oder `content/paris-limits.md`.
Die Dateien im Ordner `content/sections` erscheinen auf der Startseite als Sections.
Die Datei `content/_index.md` ist die Startseite.

### Layout

In der Datei `config.toml` gibt es viele Einstellungen,
unter anderem auch Farbeinstellungen, die dringend verbessert werden müssten.
Im Ordner `themes/assets` finden sich viele CSS-Einstellungen.

### Deployment

Das Deployment der Webseite läuft über github-pages. Dafür wird der Branch
`gh-pages` genutzt.
Das Skript `deploy_site.sh` erledigt alles, um eine neue Version zu deployen:
Es wird mit dem Aufruf `hugo` eine statische Seite im Ordner `public` gebaut,
dann werden diese Dateien in den `gh-pages`-Branch geschoben.

# Rechtliches

Der Quelltext dieses Projekts ist lizenziert unter der Apache 2.0 Lizenz:

```
Copyright 2019 Klimawatch Contributors

Licensed under the Apache License, Version 2.0 (the "License");
you may not use these files except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

Für die beigefügte Programmbibliothek `hugo/static/js/d3v4.js` gilt folgende Lizenzbedingung:

```
Copyright 2010-2017 Mike Bostock
All rights reserved.

Redistribution and use in source and binary forms, with or without modification,
are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this
  list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright notice,
  this list of conditions and the following disclaimer in the documentation
  and/or other materials provided with the distribution.

* Neither the name of the author nor the names of contributors may be used to
  endorse or promote products derived from this software without specific prior
  written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR
ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON
ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```

