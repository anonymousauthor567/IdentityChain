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
7. "HuggingFaceH4/starchat-beta
8. starcoder
9. starcoderplus
10. starcoderbase
11. starcoderbase-7b
12. starcoderbase-3b
13. starcoderbase-1b

Use [run_identity_chain.sh](./examples/run_identity_chain.sh) to run IdentityChain evaluation on a set of models.

Use [browse_results.py](./scripts/browse_results.py) to browse the results of IdentityChain evaluation.

Use [analyze_results.py](./scripts/analyze_results.py) to analyze the results of IdentityChain evaluation.

## Linting & Testing

We use a `Makefile` as a command registry:

- `make format`: autoformat  this library with `black`
- `make lint`: perform static analysis of this library with `black` and `flake8`
- `make annotate`: run type checking using `mypy`
- `make test`: run automated tests
- `make check`: check assets for packaging

Make sure that `make lint`, `make test`, and `make check` all pass locally before submitting a Pull Request.
