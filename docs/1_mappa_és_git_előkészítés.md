1. mappaszerkezet
    ```
    todo-app
        |
        |
        +-backend
        |
        |         +-backend
        |         |
        +-docker--+-frontend
        |         |
        |         +-mysql
        |
        +-docs
        |
        |
        |
        +-frontend
    ```
2. git inicializálás
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

    #laravel futás közbeni file-ok
    backend/storage/*.key
    backend/logs/*.log
    backend/bootstrap/cache/*.php
    backend/public/hot
    backend/public/storage

    #szerkesztő file-jai
    .idea/
    .vscode/
    .DS_Store
    Thumbs.db
    *log
    ```
- .gitattributes
    ```
    * text=auto eol=lf

    *.png binary
    *.jpg binary
    *.jpeg binary
    *.gif binary
    *.ico binary
    *.wff binary
    *.woff2 binary
    ```
- git init; git status; git add .; git commit -m "message";
3. lokális repo feltöltése github-ra
- távoli repo létrehozása
- git branch -M main; git remote add origin link; git push -u origin main
4. ellenőrző parancsok
- git config user.name; git config user.email