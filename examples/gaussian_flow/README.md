Gaussian-Flow
---

Dependencies installtion must follow [this version](https://pointrix-project.github.io/pointrix/get_started/installation.html):

```bash
mamba create -n pointrix python=3.9
mamba activate pointrix
mamba install pytorch==2.1.1 torchvision==0.16.1 pytorch-cuda=12.1 -c pytorch -c nvidia

# do gaussian flow branch please.
pip install -r requirements.txt
pip install -e .

cd msplat
pip install .

python -m pip install git+https://github.com/Linyou/polyfourier.git

# ~Optional~ Mandatory for gaussian_flow You can also install gsplat or diff-gaussian-rasterization,
pip install gsplat
git clone https://github.com/graphdeco-inria/diff-gaussian-rasterization.git
cd diff-gaussian-rasterization
python setup.py install
pip install .
```

I will soon update a conda environment for easily installing all dependencies once I get used with the framework.

1. Dnerf dataset [download link](https://www.dropbox.com/scl/fi/cdcmkufncwcikk1dzbgb4/data.zip?rlkey=n5m21i84v2b2xk6h7qgiu8nkg&e=1&dl=0)
2. Extract the zip file and copy the path of `lego` folder.
3. Run the following command to train the model in this relative path `examples/gaussian_flow`:
    ```bash
    python launch.py --config dnerf.yaml trainer.datapipeline.dataset.data_path=/home/qingwen/data/data/lego/
    ```
4. If you want to test the model, run the following command with above model path printed in the terminal:
    ```bash
    python launch.py --config dnerf.yaml trainer.training=False trainer.datapipeline.dataset.data_path=/home/kin/data/dnerf/lego trainer.test_model_path=/home/kin/workspace/pointrix/examples/gaussian_flow/wandb/gf_tes/dnerf-lego@20250330-223143/chkpnt101.pth
    ```

## Other issues

1. `glm/glm.hpp: No such file or directory`, ref [gaussian-splatting/issues/645](https://github.com/graphdeco-inria/gaussian-splatting/issues/645#issuecomment-2230834319). Solution:
    ```bash
    sudo apt-get install libglm-dev
    ```
