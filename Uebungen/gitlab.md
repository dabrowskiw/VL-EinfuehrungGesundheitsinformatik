#Grundlagen

Clone:
```sh
git clone https://gitlab.com/dabrowskiw/htwgitexample.git
cd htwgitexample
```

Änderungen ansehen:
```sh
echo "Blub" >> README.md
git status
git diff README.md
```

Änderungen committen:
```sh
git commit README.md
git commit README.md -m "Mehr Punkte!"
```

Remotes überprüfen:
```sh
git remote
git remote -v
git remote -h
```

Branch überprüfen:
```sh
git branch
```

Push:
```sh
git push origin master
```

Credentials merken:
```sh
git config --global credential.helper store
```

Erkennen, dass das eine schlechte Idee ist:
```sh
cat ~/.git-credentials
rm ~/.git-credentials
```

Mit SSH clonen, um Sicherheit zu erhöhen:
```sh
cd ..
rm -rf htwgitexample
git clone git@gitlab.com:dabrowskiw/htwgitexample.git
```

Geht nicht, also erstmal keypair generieren:
```sh
ssh-keygen -t ed25519 -C "gitlab"
```

Key kopieren, unter Avatar rechts oben->Settings->SSH Keys einfügen: 
```sh
cat ~/.ssh/id_ed25519.pub | cut -d " " -f 1,2
```

Überprüfen, ob gitlab den key für die SSH-Verbindung nimmt:
```sh
ssh -T git@gitlab.com
```

Hurra, nochmal clonen:
```sh
git clone git@gitlab.com:dabrowskiw/htwgitexample.git
```

Noch ein paar Änderungen, und committen
```sh
echo "Und noch mehr Zeugs" >> README.md
git commit README.md -m "Änderungen..."
echo "Und noch vieeel mehr Zeugs" >> README.md
git commit README.md -m "Mehr Änderungen..."
```

Anschauen, was bisher mit README.md passiert ist:
```sh
git log README.md
```

Älteren Zustand (nicht gepusht) wiederherstellen:
```sh
git reset --hard <commit hash>
git log README.md
cat README.md
git push origin master
```

Git log ist auch im Web-Interface sichtbar: Repository->Commits

Älteren Zustand (gepusht) wiederherstellen:
```sh
git reset --hard <commit hash>
```

Und pushen:
```sh
git push origin master
git status
git push --force origin master
```

Problem: protected branch. Unportect in gitlab, dann geht es:
```sh
git push --force origin master
git log
```

Bevor man zu alten Commits zurückgeht, kann man sie sich auch anschauen (und eventuell Änderungen durchführen):
```sh
git checkout HEAD~2
cat README.md
git checkout master
git checkout HEAD~2
#README.md bearbeiten
git checkout master
#geht nicht
git stash
git checkout master
git stash list
git stash pop
#README.md bearbeiten, um Konflikte aufzulösen
git add README.md
git commit -m "Beispiel für stash"
git push
```

Saubere Alternative: Unerwünschte Änderungen in "toten Branch" legen, master zurückschieben
```sh
git branch dummeidee
git log
git push origin dummeidee
git checkout master
git reset --hard HEAD~2
git push --force origin master
```

In der Graph-Ansicht in gitlab sichtbar, aber noch klarer nach der nächsten Veränderung:
```sh
echo "Sooo viele neue Sachen" >> README.md
git commit README.md -m "Noch mehr Änderungen..."
git push origin master
```
