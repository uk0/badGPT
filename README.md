## BadGPT


__未来将为云原生安全人员提供检测建议__

__用5美金训练一个简单能说中文的llama2-lora7b(8小时)__

* https://github.com/tloen/alpaca-lora.git


* https://huggingface.co/firshme/llama2-lora7b-trans_chinese_alpaca_data/tree/main

## conda

* sudo apt-get install git-lfs
* git lfs install
* pip install huggingface_hub

```bash

wget "https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh" -O ~/miniconda.sh

bash ~/miniconda.sh -b -p $HOME/miniconda
~/miniconda/bin/conda init $(echo $SHELL | awk -F '/' '{print $NF}')
echo 'Successfully installed miniconda...'
echo -n 'Conda version: '
~/miniconda/bin/conda --version
echo -e '\n'
exec bash

##install lfs
apt install git-lfs

conda create -n py39 python=3.9
conda activate py39
conda install pytorch torchvision torchaudio cudatoolkit=11.1 -c pytorch -c conda-forge
```


## generate.py (test)

python generate.py \
    --load_8bit \
    --base_model 'daryl149/llama-2-7b-chat-hf' \
    --lora_weights 'tloen/alpaca-lora-7b'


## download fle 

* https://github.com/LC1332/Chinese-alpaca-lora/blob/main/data/trans_chinese_alpaca_data.json?raw=true


## tools 

```bash

pip install nvitop

```

## train.py


```bash

python finetune.py \
    --base_model 'daryl149/llama-2-7b-chat-hf' \
    --data_path 'trans_chinese_alpaca_data.json' \
    --output_dir './lora-alpaca-zh'
```

### test


```bash
    python generate.py \
    --load_8bit \
    --base_model 'daryl149/llama-2-7b-chat-hf' \
    --lora_weights './lora-alpaca-zh'
```

### export 

```bash
BASE_MODEL=daryl149/llama-2-7b-chat-hf LORA_MODEL=lora-alpaca-zh HF_CHECKPOINT=hf_ckpt python export_hf_checkpoint.py

```

### save

```bash

git add .
git commit -m "add files"
git lfs migrate import --everything
git push 
```


###  训练使用 [vast](https://cloud.vast.ai/)
