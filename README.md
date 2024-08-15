# fastjet-examples

This is a collection of notebooks that have examples of jet physics algorithms, implemented using the pythia and fastjet python interfaces.

## Initial setup

The first time you check this out, you'll need to create a python virtual environment:

```
python -m venv jupyter.venv
```

Then, activate it and install the package dependencies:

```
source jupyter.venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
```

You'll need Pythia, and its python bindings. Following the instructions ...
https://pythia.org/latest-manual/PythonInterface.html

```
wget https://www.pythia.org/download/pythia83/pythia8312.tgz
tar -zxvf pythia8312.tgz
rm pythia8312.tgz
cd pythia8312/
./configure --with-python --with-gzip --with-mg5mes --with-openmp --with-lhapdf6=/users/mleblan6/work/crw-notebooks/LHAPDF-6.5.4_install/
make -j8
export PYTHONPATH=$(PREFIX_LIB):$PYTHONPATH 
```

`$(PREFIX_LIB)` should be the `lib/` directory within pythia that contains `pythia8.so`, for me this was `export PYTHONPATH=/users/mleblan6/work/crw-notebooks/pythia8312/lib/:$PYTHONPATH` on OSCAR.

You'll need to add that line to your `.bashrc`.

You can test and make sure everything is working so-far:

```
(jupyter.venv) [mleblan6@login010 crw-notebooks]$ python
Python 3.9.16 (main, Dec  8 2022, 00:00:00)
[GCC 11.3.1 20221121 (Red Hat 11.3.1-4)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import pythia8
>>> pythia = pythia8.Pythia("", False)
>>> settings = pythia.settings
>>> flags = settings.getFlagMap("")
>>> for key, val in settings.getFlagMap("").items(): print(key)
... [hit enter]
alpgen:setheavymasses
alpgen:setlightmasses
alpgen:setmlm
alpgen:setnjet
angantyr:glauberonly
angantyr:sdtest
[...]
```

Great!

## Starting a JupyterLab instance on OSCAR

Begin by going to this page: [https://ood.ccv.brown.edu/pun/sys/dashboard/batch_connect/sys/bc_ccv_jupyter_virtualenv/session_contexts/new](https://ood.ccv.brown.edu/pun/sys/dashboard/batch_connect/sys/bc_ccv_jupyter_virtualenv/session_contexts/new)

In the first box, you need to point at your python virtual environment on OSCAR. I enter the following:

```
/users/mleblan6/work/fastjet-examples/jupyter.venv/
```

You can select 'Jupter Lab' and leave the other fields at their default values. Adjust the number of cores, amount of memory and number of GPUs according to your session needs. Finally, specify the number of hours you would like the session to run for, and click 'Launch'!

When the session finally runs, you can access it through your browser from the next page or from the email notification.
