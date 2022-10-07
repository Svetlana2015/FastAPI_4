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

# Deploy on Heroku

NOTE: the heroku app name below is `still-wildwood-24910`. 
*Take care of replacing it by the name of the app heroku created for you!*

## signup on

https://signup.heroku.com/

## install heroku cli

depends on platform : linux / macos / win

## log in

```bash
heroku login
```

Check for login confirmation
```
Logging in... done
Logged in as contact@neuralia.co
```

## create your app (after logged in)

create the app ONLY ONCE!

```bash
heroku apps:create --region eu 
```

## list your apps

```bash
heroku apps 

=== contact@neuralia.co Apps
still-wildwood-24910 (eu)
```

## setup aws credentials on heroku server 

SET THE NAME OF YOUR APP IN THE COMMAND LINE, to select where the credentials will be saved

https://devcenter.heroku.com/articles/s3

```bash
heroku config:set AWS_ACCESS_KEY_ID=MY-ACCESS-ID AWS_SECRET_ACCESS_KEY=MY-ACCESS-KEY --app=still-wildwood-24910
```

```
Setting AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY and restarting ⬢ still-wildwood-24910... done, v3
AWS_ACCESS_KEY_ID:     ******************
AWS_SECRET_ACCESS_KEY: *************************
```

## push your repo to heroku

check the app name on heroku remote

```bash
git remote -v
```

Be sure app name is the one in heroku repo url. If it is not, fix it

```bash
heroku git:remote -a still-wildwood-24910
```

```bash
git remote -v                                        ✔ 
heroku  https://git.heroku.com/still-wildwood-24910.git (fetch)
heroku  https://git.heroku.com/still-wildwood-24910.git (push)
origin  https://github.com/Svetlana2015/FastAPI_4.git (fetch)
origin  https://github.com/Svetlana2015/FastAPI_4.git (push)
```

then push you repo to `main` or `master`. Anyother branch won't be deployed.

```bash
git push heroku main
```

```bash
git push heroku main                                                              ✔  FastAPI_4  
Énumération des objets: 10, fait.
Décompte des objets: 100% (10/10), fait.
Compression par delta en utilisant jusqu'à 12 fils d'exécution
Compression des objets: 100% (9/9), fait.
Écriture des objets: 100% (10/10), 10.91 Kio | 1.09 Mio/s, fait.
Total 10 (delta 0), réutilisés 0 (delta 0), réutilisés du pack 0
remote: Compressing source files... done.
remote: Building source:
remote: 
remote: -----> Building on the Heroku-22 stack
remote: -----> Determining which buildpack to use for this app
remote: -----> Python app detected
remote: -----> Using Python version specified in runtime.txt
remote: -----> Installing python-3.10.7
remote: -----> Installing pip 22.2.2, setuptools 63.4.3 and wheel 0.37.1
remote: -----> Installing SQLite3
remote: -----> Installing requirements with pip
remote:        Collecting anyio==3.6.1
remote:          Downloading anyio-3.6.1-py3-none-any.whl (80 kB)
remote:        Collecting boto3==1.24.83
remote:          Downloading boto3-1.24.83-py3-none-any.whl (132 kB)
remote:        Collecting botocore==1.27.83
remote:          Downloading botocore-1.27.83-py3-none-any.whl (9.2 MB)
remote:        Collecting click==8.1.3
remote:          Downloading click-8.1.3-py3-none-any.whl (96 kB)
remote:        Collecting fastapi==0.78.0
remote:          Downloading fastapi-0.78.0-py3-none-any.whl (54 kB)
remote:        Collecting gunicorn==20.1.0
remote:          Downloading gunicorn-20.1.0-py3-none-any.whl (79 kB)
remote:        Collecting h11==0.14.0
remote:          Downloading h11-0.14.0-py3-none-any.whl (58 kB)
remote:        Collecting idna==3.4
remote:          Downloading idna-3.4-py3-none-any.whl (61 kB)
remote:        Collecting jmespath==1.0.1
remote:          Downloading jmespath-1.0.1-py3-none-any.whl (20 kB)
remote:        Collecting joblib==1.1.0
remote:          Downloading joblib-1.1.0-py2.py3-none-any.whl (306 kB)
remote:        Collecting numpy==1.21.5
remote:          Downloading numpy-1.21.5-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (15.9 MB)
remote:        Collecting pandas==1.4.2
remote:          Downloading pandas-1.4.2-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (11.7 MB)
remote:        Collecting pydantic==1.9.1
remote:          Downloading pydantic-1.9.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (12.0 MB)
remote:        Collecting python-dateutil==2.8.2
remote:          Downloading python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
remote:        Collecting pytz==2022.2.1
remote:          Downloading pytz-2022.2.1-py2.py3-none-any.whl (500 kB)
remote:        Collecting s3transfer==0.6.0
remote:          Downloading s3transfer-0.6.0-py3-none-any.whl (79 kB)
remote:        Collecting scikit-learn==1.1.1
remote:          Downloading scikit_learn-1.1.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (30.4 MB)
remote:        Collecting scipy==1.9.1
remote:          Downloading scipy-1.9.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (43.9 MB)
remote:        Collecting six==1.16.0
remote:          Downloading six-1.16.0-py2.py3-none-any.whl (11 kB)
remote:        Collecting sniffio==1.3.0
remote:          Downloading sniffio-1.3.0-py3-none-any.whl (10 kB)
remote:        Collecting starlette==0.19.1
remote:          Downloading starlette-0.19.1-py3-none-any.whl (63 kB)
remote:        Collecting threadpoolctl==3.1.0
remote:          Downloading threadpoolctl-3.1.0-py3-none-any.whl (14 kB)
remote:        Collecting typing_extensions==4.3.0
remote:          Downloading typing_extensions-4.3.0-py3-none-any.whl (25 kB)
remote:        Collecting urllib3==1.26.12
remote:          Downloading urllib3-1.26.12-py2.py3-none-any.whl (140 kB)
remote:        Collecting uvicorn==0.18.2
remote:          Downloading uvicorn-0.18.2-py3-none-any.whl (57 kB)
remote:        Installing collected packages: pytz, urllib3, typing_extensions, threadpoolctl, sniffio, six, numpy, joblib, jmespath, idna, h11, gunicorn, click, uvicorn, scipy, python-dateutil, pydantic, anyio, starlette, scikit-learn, pandas, botocore, s3transfer, fastapi, boto3
remote:        Successfully installed anyio-3.6.1 boto3-1.24.83 botocore-1.27.83 click-8.1.3 fastapi-0.78.0 gunicorn-20.1.0 h11-0.14.0 idna-3.4 jmespath-1.0.1 joblib-1.1.0 numpy-1.21.5 pandas-1.4.2 pydantic-1.9.1 python-dateutil-2.8.2 pytz-2022.2.1 s3transfer-0.6.0 scikit-learn-1.1.1 scipy-1.9.1 six-1.16.0 sniffio-1.3.0 starlette-0.19.1 threadpoolctl-3.1.0 typing_extensions-4.3.0 urllib3-1.26.12 uvicorn-0.18.2
remote: -----> Discovering process types
remote:        Procfile declares types -> web
remote: 
remote: -----> Compressing...
remote:        Done: 153.4M
remote: -----> Launching...
remote:        Released v4
remote:        https://still-wildwood-24910.herokuapp.com/ deployed to Heroku
remote: 
remote: Starting November 28th, 2022, free Heroku Dynos, free Heroku Postgres, and free Heroku Data for Redis® will no longer be available.
remote: 
remote: If you have apps using any of these resources, you must upgrade to paid plans by this date to ensure your apps continue to run and to retain your data. For students, we will announce a new program by the end of September. Learn more at https://blog.heroku.com/next-chapter
remote: 
remote: Verifying deploy... done.
To https://git.heroku.com/still-wildwood-24910.git
 * [new branch]      main -> main
```

DOUBLE CHECH `joblib` AND `scikit-learn` lib versions, download during install.

## check logs after deployement

```bash
heroku logs --tail
```

```bash
2022-10-07T18:30:35.694145+00:00 heroku[web.1]: Starting process with command `gunicorn -w 1 -k uvicorn.workers.UvicornWorker app_ex:app`
2022-10-07T18:30:36.876134+00:00 app[web.1]: [2022-10-07 18:30:36 +0000] [4] [INFO] Starting gunicorn 20.1.0
2022-10-07T18:30:36.876448+00:00 app[web.1]: [2022-10-07 18:30:36 +0000] [4] [INFO] Listening at: http://0.0.0.0:59418 (4)
2022-10-07T18:30:36.876504+00:00 app[web.1]: [2022-10-07 18:30:36 +0000] [4] [INFO] Using worker: uvicorn.workers.UvicornWorker
2022-10-07T18:30:36.879759+00:00 app[web.1]: [2022-10-07 18:30:36 +0000] [9] [INFO] Booting worker with pid: 9
2022-10-07T18:30:37.370088+00:00 heroku[web.1]: State changed from starting to up
2022-10-07T18:31:01.475064+00:00 app[web.1]: [2022-10-07 18:31:01 +0000] [9] [INFO] Started server process [9]
2022-10-07T18:31:01.475412+00:00 app[web.1]: [2022-10-07 18:31:01 +0000] [9] [INFO] Waiting for application startup.
2022-10-07T18:31:01.481737+00:00 app[web.1]: [2022-10-07 18:31:01 +0000] [9] [INFO] Application startup complete.
2022-10-07T18:31:05.567163+00:00 heroku[web.1]: Process running mem=691M(135.0%)
2022-10-07T18:31:05.570092+00:00 heroku[web.1]: Error R14 (Memory quota exceeded)
2022-10-07T18:30:53.000000+00:00 app[api]: Build succeeded
2022-10-07T18:31:27.945706+00:00 heroku[web.1]: Process running mem=691M(135.0%)
2022-10-07T18:31:27.974372+00:00 heroku[web.1]: Error R14 (Memory quota exceeded)
2022-10-07T18:31:27.814911+00:00 heroku[router]: at=info method=GET path="/" host=protected-journey-72403.herokuapp.com 
2022-10-07T18:31:48.428522+00:00 heroku[router]: at=info method=GET path="/status" host=protected-journey-72403.herokuapp.com request_id=63aebd13-3876-4a35-aa98-9c171b2ffea1 fwd="91.173.147.129" dyno=web.1 connect=0ms service=62ms status=200 bytes=164 protocol=https
```

This log tells us 
* it started with only one worker,
* but still near out of memory (Error R14 (Memory quota exceeded)),
* path="/status" respond with status code 200 (which is ok)

## destroy your app

```bash
heroku apps:destroy --app=still-wildwood-24910
```

## logout from heroku

```bash
heroku logout

Logging out... done
```
