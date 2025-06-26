# Danantara Topic Modeling

This project implements topic modeling using various techniques and libraries. It includes Jupyter notebooks for hands-on experimentation and analysis.

## Overview

The Danantara Topic Modeling project aims to explore and implement topic modeling techniques to extract insights from textual data. The project includes data preprocessing, model training, and evaluation steps.

## Project Structure

```
danantara-topic-modeling/
├── Notebooks/                                   # Jupyter notebooks and results
│   ├── indobertweet.ipynb                       # Main notebook for IndoBERTweet topic modeling
│   └── Result/
│       └── indobertopic/
│           └── min_cluster_size_50/
│               ├── topic_modeling_result.csv
│               ├── topic_keywords.csv
│               └── after_stopwords/
│                   └── topic_keywords.csv
├── requirements.txt                             # Lists the required Python packages
└── README.md                                    # Project documentation
```

## Installation

To set up the project, clone the repository and install the required dependencies:

```bash
git clone https://github.com/akhnafal-aban/danantara-topic-modeling.git
cd danantara-topic-modeling
pip install -r requirements.txt
```

## Requirements

Main dependencies used in the notebooks:

- numpy==1.21.0
- pandas==1.3.0
- scikit-learn==0.24.2
- nltk==3.6.3
- gensim==4.1.2
- matplotlib==3.4.2
- seaborn==0.11.2
- jupyter==1.0.0
- torch
- transformers
- emoji
- bertopic
- umap-learn
- hdbscan
- requests

> **Note:** Some packages (like `torch`, `transformers`, `bertopic`, `umap-learn`, `hdbscan`, `emoji`, `requests`) are used in the notebooks but may not be listed in `requirements.txt`. Please install them as needed:
>
> ```bash
> pip install torch transformers bertopic umap-learn hdbscan emoji requests
> ```

## Usage

1. Open the Jupyter notebook located in the `Notebooks` directory to start exploring the topic modeling implementation.
2. Follow the instructions within the notebook for data preprocessing, model training, and evaluation.

## Contributing

Contributions are welcome! Please feel free to submit a pull request or open an issue for any suggestions or improvements.

## License

This project is licensed under the MIT License. See the LICENSE file for more details.