# CoNLL-to-Hugging-Face-JSON

This repository contains a Jupyter notebook that converts CoNLL format data to JSON format compatible with Hugging Face datasets ready to train your custom model. It's designed to prepare Named Entity Recognition (NER) datasets for use with Hugging Face's transformers library and other deep learning models.

## Features

1. **Two Mapping Options:**
   - Auto Mapping: Automatically identifies unique entity labels and assigns numeric IDs.
   - Custom Mapping: Allows user-defined label-to-ID mappings.

2. **Preserves NER Tag Structure:**
   - Maintains standard NER tag formats like B-Org, I-Org, etc.

3. **Generates Mapping File:**
   - Creates a separate text file with a JSON-like representation of the label mapping.

4. **Flexible Input Handling:**
   - Processes CoNLL format files, handling various NER tag schemes.

5. **Detailed Output:**
   - Provides statistics on processed sentences and tag distributions.

6. **Error Handling:**
   - Warns about unknown tags in custom mapping mode and defaults to 'O' (Outside) tag.

## Usage

### 1. Auto Mapping

Use this when you want the script to automatically assign numeric IDs to your NER tags.

```python
conll_to_json(input_file, output_file, class_mapping_file)
```

Example:
```python
conll_to_json(r'path/to/your/conll_file.conll', 'dataset_auto.json', 'tag_mapping_auto.txt')
```

### 2. Custom Mapping

Use this when you have a predefined mapping of NER tags to numeric IDs.

```python
conll_to_json(input_file, output_file, class_mapping_file, custom_mapping=custom_map)
```

Example:
```python
custom_map = {
    0: 'O',
    1: 'B-Address',
    2: 'I-Address',
    # ... other mappings ...
}

conll_to_json(r'path/to/your/conll_file.conll', 'dataset_custom.json', 'tag_mapping_custom.txt', custom_mapping=custom_map)
```

## Input Format

The script expects CoNLL format input files. Each line should contain token information, with the NER tag in the fourth column. Sentences are separated by blank lines.

Example:
```
John B-PER
Doe I-PER
lives O
in O
New B-LOC
York I-LOC
. O

She O
works O
for O
Apple B-ORG
Inc. I-ORG
```

## Output

1. **JSON File**: Contains the processed data in the following format:
   ```json
   {"id": "0", "tokens": ["John", "Doe", "lives", "in", "New", "York", "."], "ner_tags": [1, 2, 0, 0, 3, 4, 0]}
   {"id": "1", "tokens": ["She", "works", "for", "Apple", "Inc."], "ner_tags": [0, 0, 0, 5, 6]}
   ```

2. **Mapping File**: A text file containing the tag-to-ID mapping:
   ```python
   tag_mapping = {
       0: 'O',
       1: 'B-PER',
       2: 'I-PER',
       3: 'B-LOC',
       4: 'I-LOC',
       5: 'B-ORG',
       6: 'I-ORG',
   }
   ```

## Requirements

- Python 3.x
- Jupyter Notebook
- Required Python libraries: `json`, `collections`

## Installation

1. Clone this repository:
   ```
   git clone https://github.com/SakibAhmedShuva/CoNLL-to-Hugging-Face-JSON.git
   ```
2. Navigate to the repository directory:
   ```
   cd CoNLL-to-Hugging-Face-JSON
   ```
3. Open the Jupyter notebook:
   ```
   jupyter notebook conll2huggingface_json.ipynb
   ```

## Contributing

Contributions to improve the script or add new features are welcome. Please feel free to submit a pull request or open an issue for any bugs or feature requests.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
