# IdentityChain

## Installation

Create and Activate a Conda Environment.

   ``` bash
   conda create -n idchain python=3.10
   conda activate idchain
   ```

Clone this Repository to your Local Environment.

   ``` bash
   git clone https://github.com/anonymousauthor567/IdentityChain.git
   ```

Install the Library with all Dependencies.

   ``` bash
   cd IdentityChain
   make develop
   ```

## Usage

See [run_identity_chain_openai.py](./examples/run_identity_chain_openai.py) for an example of how to use IdentityChain to evaluate OpenAI models.

See [run_identity_chain_huggingface.py](./examples/run_identity_chain_huggingface.py) for an example of how to use IdentityChain to evaluate HuggingFace open-source models, including:

1. CodeLlama-7b-Instruct-hf
2. CodeLlama-13b-Instruct-hf
3. CodeLlama-34b-Instruct-hf
4. CodeLlama-7b-hf
5. CodeLlama-13b-hf
6. CodeLlama-34b-hf
7. HuggingFaceH4/starchat-beta
8. starcoder
9. starcoderplus
10. starcoderbase
11. starcoderbase-7b
12. starcoderbase-3b
13. starcoderbase-1b

Use [run_identity_chain.sh](./examples/run_identity_chain.sh) to execute scripts [run_identity_chain_openai.py](./examples/run_identity_chain_openai.py) or [run_identity_chain_huggingface.py](./examples/run_identity_chain_huggingface.py), which conducts several IdentityChain evaluation in a batch. Make sure that you:

1. Modify `export CUDA_VISIBLE_DEVICES=0` to specify the GPU device you want to use locally.
2. Modify `export HF_HOME=YOUR_OWN_PATH/huggingface` to specify your own huggingface home path, where the open-source models will be cached.
3. Modify `export IDENTITY_CHAIN_HOME=YOUR_OWN_PATH/IdentityChain` to your own IdentityChain home path.
4. Modify other parameters in the script for your own needs.

Then run the script:

``` bash
cd examples
bash run_identity_chain.sh
```

This script will create a temporary folder `tmp` under your IdentityChain home path, and store the results of IdentityChain evaluation in this folder, which will be a `jsonl` file. For example, `tmp/starcoderbase-1b/IDChain_starcoderbase-1b_tmp0.0g_len5_pb_all_m_v1_EvalPlus-Mini-v0.1.6_reformatted.jsonl`.

Use [analyze_results.py](./scripts/analyze_results.py) to analyze the results of IdentityChain evaluation. It will geneartes an `xlsx` file, which contains the following information:

1. The SC (Self-Consistency) and SSC (Strong Self-Consistency) scores of the model at each self-iteration step. Note that SSC_0 is just Pass@1.
2. The aggregated TOM score (also BLEU and CodeBLEU) information at each step for the following 4 types of resulsts: Pass-Pass, Pass-Fail, Fail-Fail, Fail-Pass.
3. The TOM score (also BLEU and CodeBLEU) trajectory at each self-iteration step for each sample in the eavluation set.
4. The raw test case outputs at each self-iteration step.

``` bash
cd ../scripts
python analyze_results.py --input_path ../tmp/starcoderbase-1b/IDChain_starcoderbase-1b_tmp0.0g_len5_pb_all_m_v1_EvalPlus-Mini-v0.1.6_reformatted.jsonl --chain_length 5
```

The analyzed results will give you a sense of the model's overall performance, and the TOM score trajectory will help you pinpoint the exact step where the model makes a mistake.

Use [browse_results.py](./scripts/browse_results.py) to browse the results of IdentityChain evaluation. You can use this script to manually examine and study the mistakes made by the model for specific samples.

``` bash
cd ../scripts
python browse_results.py --input_path ../tmp/starcoderbase-1b/IDChain_starcoderbase-1b_tmp0.0g_len5_pb_all_m_v1_EvalPlus-Mini-v0.1.6_reformatted.jsonl --chain_length 5 --start 0
```

## Linting & Testing

We use a `Makefile` as a command registry:

- `make format`: autoformat  this library with `black`
- `make lint`: perform static analysis of this library with `black` and `flake8`
- `make annotate`: run type checking using `mypy`
- `make test`: run automated tests
- `make check`: check assets for packaging

Make sure that `make lint`, `make test`, and `make check` all pass locally before submitting a Pull Request.
