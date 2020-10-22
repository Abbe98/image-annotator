# Image Annotator

Tool to run image annotation campaigns on Wikimedia Commons, created to gather data for machine learning tasks. This tool is based on [Wikidata Image Positions](https://github.com/lucaswerkmeister/tool-wd-image-positions) and licensed under AGPL-3.0. For the changes made see the git history.

## Local development setup

You can also run the tool locally, which is much more convenient for development.

```bash
git clone <repo>
cd tool-wd-image-positions
pipenv install
pipenv shell
export FLASK_APP=app.py
export FLASK_ENV=development
flask run
```

## Toolforge setup

On Wikimedia Toolforge, this tool runs under the `image-annotator` tool name. Source code resides in `~/www/python/src/`, a virtual environment is set up in `~/www/python/venv/`, logs end up in `~/uwsgi.log`.

Make sure to add / update `config.yaml`.

If the web service is not running for some reason, run the following command:
```bash
webservice --backend=kubernetes python3.7 start
```
If it’s acting up, try the same command with `restart` instead of `start`.

To update the service, run the following commands after becoming the tool account:
```bash
webservice --backend=kubernetes python3.7 shell
source ~/www/python/venv/bin/activate
cd ~/www/python/src
git fetch
git diff @ @{u} # inspect changes
git merge --ff-only @{u}
pip3 install -r requirements.txt
webservice --backend=kubernetes python restart
```

## License

The code in this repository is released under the AGPL v3, as provided in the `LICENSE` file.
