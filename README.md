# NLLB-200-distilled-350M-en-ko
---
library_name: transformers
license: cc-by-nc-4.0
datasets:
- allenai/nllb
- facebook/flores
language:
- ko
- en
metrics:
- chrf
pipeline_tag: translation
---

# NLLB-200 Distilled-350M_en2ko

The NLLB-200 model showed outstanding performance in translation task and contributed to solving problems with low-resource languages.
Despite their efforts, it is still hard to run 600M or more than 1B model for those who have not enough computing environment.
So I made much smaller model that expertized translaing English to Korean. you can also run it with cpu (No mixed-precision, No Quantization). 



## Model

- Model: model is based on NLLB-200 600M
  - **Parameters: 350,537,728 (350M)**
  - **Encoder layers: 12 -> 3**
  - **Decoder layers: 12 -> 3**
  - FFN dimension: 4096 (same)
  - Embed dimension: 1024 (same)
  - Vocab size: 256206 (same)

- Licnese: CC-BY-NC

## Data

- Training Data: [NLLB dataset](https://huggingface.co/datasets/allenai/nllb)
- Evaluation Data: [Flores-200 dataset](https://huggingface.co/datasets/facebook/flores)

## Metric

- CPU: Intel (R) Xeon(R) CPU @ 2.20GHz (16 cores)
- GPU: NVIDIA L4 24GB



|                        | #Params | chrF(++) | GPU Inference time (s) | CPU Inference time (s) |
| ---------------------- | ------- | -------- | ---------------------- | ---------------------- |
| NLLB-200 3.3B          | 3.3B    | 34.3     | 0.98 s                 | 4.65 s                 |
| NLLB-200 1.3B          | 1.3B    | 32.1     | 0.89 s                 | 2.46 s                 |
| NLLB-200 600M          | 600M    | 32       | 0.43 s                 | 1.52 s                 |
| NLLB-200 350M (*ours*) | 350M    | 24.6     | 0.24 s                 | 1.43 s                 |


## Usage

```python
from transformers import AutoTokenizer, AutoModelForSeq2SeqLM

model = AutoModelForSeq2SeqLM.from_pretrained('dhtocks/nllb-200-distilled-350M_en-ko', forced_bos_token_id=256098)
tokenizer = AutoTokenizer.from_pretrained('dhtocks/nllb-200-distilled-350M_en-ko', src_lang='eng_Latn', tgt_lang='kor_Hang')

inputs = tokenizer('[YOUR_INPUT]', return_tensors="pt")
output = model.generate(**inputs)
print(tokenizer.decode(output[0]))
```

## Citation
```bibtex
@misc{,
  title={NLLB-200 distilled_350M_en-ko},
  author={Saechan Oh},
  year={2024}
}
```

