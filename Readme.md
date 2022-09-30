# Setup Local Working Environnement

## create a virtual env
```bash
virtualenv venv
```

Where `venv` is the name of your local virtual env

## activate it
```bash
. venv/bin/activate
```

## install python librairies
```bash
pip install -r  requirements.txt
```

# Run your Fast API server

## in your local working env
```bash
gunicorn -w 3 -k uvicorn.workers.UvicornWorker app_ex:app
```

Then access to the `status` page with your browser to check your API is running, on : http://127.0.0.1:8000/status
If you can read `{"status":"running"}` in your browser, everything is fine :D

# How to push your code on github

## What you should NEVER do
* upload files directly on github.com

## What you want to do from now on
1. on your computer, with your shell (or terminal), move to the directory (ie `cd ~/FastAPI_4`),
2. check the git branch you are working on : `git status`,
3. if your are on `main` or `master`, you should create a new branch to work on : `git checkout -b my_new_feat_branch`, where `my_new_feat_branch` is an explicit name for what you aim to do,
4. now you are a the new branch, start updating or creating everything is needed,
5. add your files in your next commit : `git add FILES`, where `FILES` is the name of the file to commit. Do it for every new or updated file,
6. commit your changes : `git commit -m "explicit description on the change"`
7. then push the commit on the working branch : `git push`

    Please note you can link your heroku instance on your working branch.

8. When your working branch is clean, create a Pull Request in github, describe the changes, then use the big green button 'rebase and merge' to merge the working branch in `main` or `master` branch.
9. Delete your working branch from github and from your computer.

This workflow is usefull to keep your `main` branch healthy, and not polute it with working-in-progress updates. You can easily rollback, or other contributors can easily fork a healthy code.
