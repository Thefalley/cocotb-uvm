# cocotb-uvm

## install dependences debian 13.0

sudo apt-get update
sudo apt-get install -y \
  build-essential git make python3 python3-venv python3-pip \
  verilator iverilog gtkwave

### Verify version
verilator --version
iverilog -V
gtkwave --version
python3 --version


## Create virtual enviroment

python3 -m venv .venv
source .venv/bin/activate
python -m pip install -U pip setuptools wheel
pip install -r requirements.txt

### Verify

cocotb-config --version
python -c "import pyuvm, cocotb; print('ok')"
python -c "import cocotbext.axi; print('axi ok')"
verilator --version

## Estructura de proyecto

tu-proyecto/
├─ rtl/
│  ├─ axil_regfile.sv
│  └─ axis_incr.sv
├─ sim/
│  ├─ Makefile
│  ├─ test_axil.py
│  └─ test_axis.py
└─ requirements.txt

## Ejecutar test make

cd sim
make TOPLEVEL=axil_regfile MODULE=test_axil SIM=verilator
make TOPLEVEL=axis_incr MODULE=test_axis SIM=verilator

## Ver Ondas

gtkwave sim_build/obj_dir/Vaxil_regfile.fst &
# o para el otro DUT
gtkwave sim_build/obj_dir/Vaxis_incr.fst &


## Ejecuta regresiones con pytest

pytest -q

## Congelar versiones exactas del entorno

pip freeze > requirements.lock.txt

### Reproducir el entorno

pip install -r requirements.lock.txt

