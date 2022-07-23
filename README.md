# GPT2_Japanese

## Huggingface Transformersのインストール
git clone https://github.com/huggingface/transformers -b v4.4.2

## ライブラリインストール
ほかにもライブラリ必要かも

動かない場合にはenv.txtのバージョン参照

pip3 install -e transformers

pip3 install datasets==1.2.1

pip3 install sentencepiece==0.1.91

pip3 install dill==0.3.4

## RTX3090 windows11 x64での環境

### driver install
GPUをPCにつなげてタスクマネージャーに表示された状態（GPUも電源入れる）でないとドライバをインストールできない

[ダウンロードページ](https://www.nvidia.co.jp/Download/index.aspx?lang=jp)

GeForce

GeForce RTX 30Series

GeForce RTX3090

Windows 11

Game Ready ドライバー(GRD)

japanese

### Cuda Toolkit 11.6 install
[ダウンロードページ](https://developer.nvidia.com/cuda-11-6-0-download-archive)

### CuDNN install
いらないかも？

[ダウンロードページ](https://developer.nvidia.com/rdp/cudnn-download)

環境変数を新規で追加

変数：CUDNN_PATH

値：C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.6

### Pytorch install
pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu116

### ./transformers/examples/language-modeling/run_clm.pyを編集
#### 追加
from transformers import T5Tokenizer
#### 変更
tokenizer = AutoTokenizer.from_pretrained(model_args.tokenizer_name, **tokenizer_kwargs)

　　↓

tokenizer = T5Tokenizer.from_pretrained(model_args.tokenizer_name, **tokenizer_kwargs)

tokenizer = AutoTokenizer.from_pretrained(model_args.model_name_or_path, **tokenizer_kwargs)

　　↓

tokenizer = T5Tokenizer.from_pretrained(model_args.model_name_or_path, **tokenizer_kwargs)

_______________________________________________________________________________________


## 学習コマンド
GPU使わないと結構時間かかる
GPU使う場合はtorchとcudaのバージョン、cuDNNのパス？等注意

python ./transformers/examples/language-modeling/run_clm.py\
    --model_name_or_path=rinna/japanese-gpt2-medium\
    --train_file=dataset/train.txt\
    --validation_file=dataset/train.txt\
    --do_train\
    --do_eval\
    --num_train_epochs=50\
    --save_steps=5000\
    --save_total_limit=3\
    --per_device_train_batch_size=2\
    --per_device_eval_batch_size=2\
    --output_dir=output/\
    --use_fast_tokenizer=False\
    --overwrite_output_dir=y



## 文章生成
test.ipynb
