# 🇳🇬 NaijaWeb

NaijaWeb is a web scraping project inspired by the [FineWeb paper](https://arxiv.org/abs/2406.17557) and the [WebText dataset](https://paperswithcode.com/dataset/webtext), including the [OpenWebText dataset](https://huggingface.co/datasets/Skylion007/openwebtext).

The scraping was performed on **Google Colab** due to its **free memory** and **easy integration with Google Drive**. Several notebooks (`clean_download_data.ipynb`, `clean_download_data_403.ipynb`, `download_webpages.ipynb`, `webscrape_403.ipynb`, and `webscrape_nairaland.ipynb`) were run across 9 different Colab notebooks (3 notebooks per Colab account) to expedite the process. All notebooks were linked to a single Google Drive folder: `/content/drive/MyDrive/nairaland_webtext`, where the files were saved.

The dataset is available on Hugging Face: [NaijaWeb Dataset](https://huggingface.co/datasets/saheedniyi/naijaweb).

## Notebooks and Process

### [webscrape_nairaland.ipynb](https://github.com/saheedniyi02/naijaweb/blob/main/webscrape_nairaland.ipynb)
This notebook scrapes and extracts posts from a specific **section** on [Nairaland](https://www.nairaland.com/). The script first collects all **post links** for each section and saves them to a pickle file. It then downloads the individual posts. Due to Colab's limited runtime, the process was distributed across 9 notebooks, where the long list of post links was split into smaller chunks to speed up the downloads.

### [extract_outboundlinks.ipynb](https://github.com/saheedniyi02/naijaweb/blob/main/extract_outboundlinks.ipynb)
This notebook extracts all outbound links from the downloaded posts, filters out certain domains, performs basic cleaning (removing full stops at the end of links and consecutive full stops), and saves the cleaned links to a CSV file.

### [download_webpages.ipynb](https://github.com/saheedniyi02/naijaweb/blob/main/download_webpages.ipynb)
This notebook downloads webpages from the outbound links extracted in the previous step. The links are downloaded in batches of 1,000 and saved as pickle files. This process was also run across 9 notebooks to save time.

### [clean_download_data.ipynb](https://github.com/saheedniyi02/naijaweb/blob/main/clean_download_data.ipynb)
This notebook uses [Trafilatura](https://trafilatura.readthedocs.io/en/latest/) (as inspired by the FineWeb paper) to extract and clean the downloaded webpages. Pages that returned a "403 Forbidden" response were saved for later handling.

### [webscrape_403.ipynb](https://github.com/saheedniyi02/naijaweb/blob/main/webscrape_403.ipynb)
This notebook redownloads webpages that initially returned a 403 error using [Cloudscraper](https://pypi.org/project/cloudscraper/).

### [clean_download_data_403.ipynb](https://github.com/saheedniyi02/naijaweb/blob/main/clean_download_data_403.ipynb)
This notebook extracts and cleans the data from the webpages that were redownloaded due to the 403 error.

### [fineweb_clean_data.ipynb](https://github.com/saheedniyi02/naijaweb/blob/main/fineweb_clean_data.ipynb)
This notebook applies the same cleaning process used on the FineWeb dataset, following these steps:
- 🔻 **FILTER**: 😈 URL filter
- 🔻 **FILTER**: 👯 Gopher repetition
- 🔻 **FILTER**: 🥇 Gopher quality
- 🔻 **FILTER**: ⛰ C4 quality
- 🔻 **FILTER**: 🍷 FineWeb quality
- 🔢 **TOKENIZER**: 📊 Counter
- 💽 **WRITER**: 🐿 Jsonl

### [PII_formatter.ipynb](https://github.com/saheedniyi02/naijaweb/blob/main/PII_formatter.ipynb)
This notebook removes Personally Identifiable Information (PII) such as emails and IP addresses from the dataset.

### [push_to_hub.ipynb](https://github.com/saheedniyi02/naijaweb/blob/main/push_to_hub.ipynb)
This notebook pushes the full dataset to Hugging Face and calculates the educational score of the dataset using the [FineWeb EDU classifier](https://huggingface.co/HuggingFaceFW/fineweb-edu-classifier). Note that the classifier's predictions may not be fully accurate due to the limited amount of Nigerian data the model was likely trained on.

### [extract_naijaweb_edu.ipynb](https://github.com/saheedniyi02/naijaweb/blob/main/extract_naijaweb_edu.ipynb)
This notebook detects the language of the documents and creates two subsets of the dataset: **[NaijaWeb EDU](https://huggingface.co/datasets/saheedniyi/naijaweb-edu)** and **[NaijaWeb EDU2](https://huggingface.co/datasets/saheedniyi/naijaweb-edu2)**, using the educational score. This is an attempt to recreate the FineWeb EDU dataset with Nigerian content.

---

If you find this project helpful, consider giving the repo a star. Thank you!
