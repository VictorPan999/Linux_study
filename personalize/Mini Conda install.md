# Mini Conda install
###### tags: `Conda`
https://docs.conda.io/en/latest/miniconda.html

# Mini Conda command
update     :`conda update conda`
## Env management
env list   :`conda env list`
create env :`conda create —name myenv python=3.8`
remove env :`conda env remove -name`
open env   :`source activate`
close env  :`source deactive`

## Package management
package list:`conda list`
### Install package
#### Normal install
`conda install`
#### Install for datatable optuna lightgbm
`conda install -c conda-forge datatables`
optuna
lightgbm
#### Install sklearn
`Conda install -c intel scikit-learn`

package remove:`conda remove —name myenv numpy`





