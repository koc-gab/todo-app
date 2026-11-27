1. mappa szerkezet
    ```
    |
    |-backend
    |-docker
    |   |
    |   |-backend
    |   |-frontend
    |   |-mysql
    |-docs
    |-frontend
    ```

2. git innicializálás
    - .gitignore
       ```
        #helyi környezet
        .env
        .env.*
        !.env.example

        #függőségek
        backend/vendor/
        frontend/node_modules/

        #build kimenet
        frontend/dist/

        #laravel futás közbeni fájlok
        backend/storage/*.key
        backend/storage/logs/*.log
        backend/bootstrap/cache/*.php
        backend/public/hot
        backend/public/storage

        #szerkesztő filejai
        .idea/
        .vscode/
        .DS_Store
        Thumbs.db
        *.log
        ```
    - .gitattributes
        ```
        * text=auto eol=lf

        *.png binarygit
        *.jpg binary
        *.jpeg binary
        *.gif binary
        *.ico binary
        *.woff binary
        *.woff2 binary
        ```
    - git init; git status; git add .; git commit -m "message"

3. lokális repo feltöltése githubra
    - git branch -M main
    - git remote add origin (github link)
    - ellenörző parancsok: git config user.name; git config user.email;
    - böngészős autentukáció elfogadása
    - git push -u origin main