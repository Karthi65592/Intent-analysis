## Analyzing GPT-2 with TransformerLens

The `loading-gpt-2.ipynb` notebook explores the mechanistic interpretability of the `gpt2-small` model using the [TransformerLens](https://github.com/neelnanda-io/TransformerLens) library. It demonstrates how to inspect the internal representations of the model when reasoning about code security.

### Key Highlights:
* **Model Setup & Caching:** Loads the pre-trained `gpt2-small` model into a `HookedTransformer`. It uses `run_with_cache` to execute prompts and capture intermediate network activations, such as attention patterns (`pattern`), MLP outputs (`mlp_out`), and residual streams (`resid_post`).
* **Security Prompt Analysis:** Evaluates how the model processes a prompt requesting a secure login function. By caching the activations, we can peer into the layer-by-layer representations of the generated code context.
* **Logit Difference Evaluation:** Measures the model's ability to distinguish between secure and insecure code implementations. The notebook calculates the "Yes-No logit diff" to evaluate the model's response to:
  * A **clean** implementation that securely hashes passwords using `bcrypt`.
  * A **corrupted** implementation that insecurely stores passwords in plaintext.
* **TransformerBridge:** Demonstrates an alternative method to boot and run models while caching activations using `TransformerBridge`.
