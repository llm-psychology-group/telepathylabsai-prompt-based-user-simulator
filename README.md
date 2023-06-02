# In-Context Learning User Simulators for Task-Oriented Dialog Systems

This repo enhances **ConvLab-2** by incorporating the implementation of prompt-based user simulators using LLMs (among those, OpenAI's ChatGPT, HuggingFace-compatible LLMs like FLAN-T5). The user simulator selects relevant conversations as shots and generates interactive turn-by-turn conversations by interacting with a Convlab-2 dialog system on the MultiWOZ dataset.


For a comprehensive understanding of the implementation and evaluation process, please refer to the [paper]](https://arxiv.org/abs/2306.00774)

- [Installation](#installation)
- [Models](#models)
- [Run Experiments](#run-an-experiment)
- [Issues and Contributions](#issues-and-contributions)
- [How to cite this work](#how-to-cite-this-work)
- [License](#license)


## Installation

**IMPORTANT!!** We had to relax or force some requirements to make ConvLab2 work along with the most recent HF transformers library. Please make sure to follow the next steps.

1. Clone the repo:
  ```bash
  git clone https://github.com/silviatti/prompt-based-user-simulator.git

  cd prompt-based-user-simulator
  ```
2. **Create a virtual environment with python 3.7.9** (python 3.10.5 doesn't seem work, other versions may work as well)
3. Install the library via pip:
  ```bash
  pip install -e .
  ```
4. Unzip the file `train_corrected.json.zip`. This file will be used to retrieve the shots for building the prompt.
  ```bash
  cd data/multiwoz
  unzip train_corrected.json.zip
  ```

## Run an experiment

To run the experiments, just run 

```bash
python scripts/user_simulator_script.py
```

Run `python scripts/user_simulator_script.py --help` to see list of parameters. 
The script will run a specific number of dialogs with the defined dialog system and user simulator models.
The results are stored in the specified folder. The summary of the metrics is found in the `res.txt` file.

If you want to run it with a smaller GPU, you may want to use a smaller model `--model-id google/flan-t5-small`.


### Diversity of user and system utterances
```bash
python scripts/calculate_diversity.py --dataset_path data/multiwoz/train.json --data-key usr
```
will calculate various diversity metrics and save them to: `results/diversity/diversity_usr_data_multiwoz_train.json`


## Generative User Simulator Models
The framework supports different generative models for generating the user utterances. You can find them in `convlab2/nlg/generative_models`.
A generative model usually is a subclass of `convlab2/nlg/generative_models/user_simulator_generative_model.py`. 


### OpenAI Models
We currently support OpenAI's models through Azure API. You just need to specify your keys before running the models like this:
```bash
export OPENAI_API_BASE=https://azure-openai-something.openai.azure.com/
export OPENAI_API_KEY=your_key
```

### HuggingFace Models
We currently support HuggingFace models, which can be loaded via AutoModel interface. We also have model-specific definitions for FLAN-T5 and LLaMa models.


## Issues and contributions

You are welcome to create an issue if you want to request a feature, report a bug or ask a general question. We welcome contributions from community. See CONTRIBUTING.rst.

## Team

- Silvia Terragni <silvia.terragni@telepathy.ai>
- Modestas Filipavicius <modestas.filipavicius@telepathy.ai>
- Nghia Khau <nghia.khau@telepathy.ai>
- Bruna Guedes <bruna.guedes@telepathy.ai>
- André Manso <andre.manso@telepathy.ai>
- Roland Mathis <roland.mathis@telepathy.ai>


## Credits

A shout-out to the authors of [ConvLab-2](https://github.com/thu-coai/ConvLab-2) for building the framework from which we constructed the foundations of this work. 

## How to cite this work

Please cite:

```
@article{Terragni2023usersimulator,
  title={In-Context Learning User Simulators for Task-Oriented Dialog Systems},
  author={Silvia Terragni and Modestas Filipavicius and Nghia Khau and Bruna Guedes and André Manso and Roland Mathis},
  journal={ArXiv},
  year={2023},
  url="https://arxiv.org/abs/2306.00774",
  volume={abs/2306.00774}
}

@inproceedings{zhu2020convlab2,
    title={ConvLab-2: An Open-Source Toolkit for Building, Evaluating, and Diagnosing Dialogue Systems},
    author={Qi Zhu and Zheng Zhang and Yan Fang and Xiang Li and Ryuichi Takanobu and Jinchao Li and Baolin Peng and Jianfeng Gao and Xiaoyan Zhu and Minlie Huang},
    year={2020},
    booktitle={Proceedings of the 58th Annual Meeting of the Association for Computational Linguistics},
}

```

## License

Apache License 2.0
