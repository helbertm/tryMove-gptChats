# Chat Migration Prompt

**Version 1.0**

This repository provides a structured **prompt** that extracts a complete,
machine‑readable snapshot of a ChatGPT or Custom GPT conversation so you can
migrate it to another environment with **zero loss of context**.

## Repository Layout

```
.
├── prompts/
│   └── migration_prompt_v1_0.txt   # Main extraction prompt
├── examples/
│   └── sample_response.yaml        # Fictitious example output
├── CHANGELOG.md
├── LICENSE
├── .gitignore
└── README.md
```

## Usage

1. Open the **original conversation** in ChatGPT / Custom GPT.  
2. Copy the contents of `prompts/migration_prompt_v1_0.txt`.  
3. Paste it into the message box and send it.  
4. The assistant will return a YAML block (multiple blocks if >100 k tokens).  
5. Copy that YAML into the *new* chat or Custom GPT knowledge base.

### Quick CLI Example

```bash
# macOS
pbcopy < prompts/migration_prompt_v1_0.txt
# Windows
type prompts\migration_prompt_v1_0.txt | clip
```

Then simply paste the prompt into the old chat.

## Example Output

See [`examples/sample_response.yaml`](examples/sample_response.yaml) for a
mock response showing the expected structure.


## Disclaimer on AI-Generated Output

This project relies on **generative AI**. Model outputs are *nondeterministic*—
the same prompt can yield slightly different YAML snapshots on different runs.
In practice the model may:

* Miss one or more files or media assets that were attached or generated.
* Return fewer than the requested 20 question–answer pairs, or summarise them
  differently.
* Truncate or omit sections when the conversation is large or close to the
  context‑window limit.
* Fill some fields with `null` when it is unsure.

For best fidelity **run the migration prompt at least twice** and manually review
the results:

1. Compare the YAML files side‑by‑side, especially the
   `files_and_media_assets_used` and `example_interactions` sections.
2. Merge or correct missing items before importing the snapshot into the new
   chat or Custom GPT.
3. Keep the original conversation open until you have verified the migrated
   copy behaves as expected.


## Contributing

Pull requests are welcome! Please:

1. Branch from `main`.  
2. Update `CHANGELOG.md` and bump `generator_prompt_version` in the prompt file.  
3. Open a PR with a clear description of the change.

## Best Practices

* **Semantic versioning**: `MAJOR.MINOR` (starting at **1.0**).  
* Document every prompt change in `CHANGELOG.md`.  
* Keep temporary files out of git (`.gitignore` already included).

## License

Released under the [MIT License](LICENSE).
