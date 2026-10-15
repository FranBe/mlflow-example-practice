# Example MLflow project

This is a fork from the Mlflow base example(official).
I used the repo beacuse I wanted to practice a little with running experiments using a previous project in GitHub.

## Some considerations

### Environment
It's obvious that if you are going to use MLflow, you need to have it installed in your system or in a virtual environment.

The example uses *conda* for environment creation and administration, a few instructions:

Creating environment from *yaml* file:

```bash
conda env create -f conda.yml
```

In this tutorial, the environment it's called...tutorial. You can check this out with:

```bash
conda env list
```
Environment activation:

```bash
conda activate tutorial
```
In case that you already have the file, and you made changes on it:

```bash
conda env update --file conda.yml --prune
```


### MLflow

Now, you can use mlflow...but, if you do it normally, using this:

```bash
mlflow run https://github.com/mlflow/mlflow-example.git -P alpha=0.5   
```

**Attention!**  
You'll find that MLflow obtains de GitHub repo, and uses conda, automcatically, downloading dependencies and preparing the environment. But, as you can notice, download all the libraries needed again, when have them installed in your own previuos virtual environment. In fact, MLflow will create a temp folder in */tmp* with all the data needed for the project.
That is normal behavior, but you can change it just using another parameter: *--env-manager=local*
So, the command would be now:

```bash
mlflow run https://github.com/mlflow/mlflow-example.git -P alpha=0.5 -P l1_ratio=0.3 --env-manager=local 
```

With this, the application will be able to reuse your local environment without the need to create a new one.  
Also, as you can see, I added another parameter inside the command (listed in *MLproject* file)

The rest is already known:

```bash
mlflow ui 
```
Notice that because the original code in *train.py* file doesn't specify a database uri or an experiment name, for example, the mlflow mode is the default, in wich creates a *mlruns* folder with the experiments, models, artifacts,... It doesn't use a database in Sqlite or PostgreSQL, for exmaple.

Accesing to the apllication graphical interface is as easy as entering the following URL into the web browser:

http://127.0.0.1:5000


#### Models

I kept the mlruns folder in the git repository, just for having the experiment and model history, even though it contains some dummy tests...

