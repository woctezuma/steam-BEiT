# Steam BEiT: match Steam Banners with Microsoft's BEiT

This repository contains Python code to retrieve Steam games with similar store banners, using [Microsoft's BEiT][hugging-face-doc].

Image similarity is assessed by the cosine similarity between image features encoded by BEiT.

![Similar vertical banners][wiki-cover]

## Model

BEiT is a Vision Transformer (ViT):
1. pre-trained with self-supervision (using patches, and "visual tokens" from [OpenAI's DALL-E][openai-dalle]) on ImageNet-21k,
2. then fine-tuned for classification on ImageNet-21k (14M images with ~21k classes),
3. finally fine-tuned for classification on ImageNet-1k (1.28M images with 1000 classes).

Pre-trained models are available at [HuggingFace][hugging-face-models], respectively as:
1. `microsoft/beit-base-patch16-224-pt22k`
2. `microsoft/beit-base-patch16-224-pt22k-ft22k`
3. `microsoft/beit-base-patch16-224`

Larger models are available by changing a keyword in their name: `large` (1.2 GB) instead of `base` (400 MB).

## Data

Data consists of **vertical** Steam banners (300x450 resolution), resized to 256x384 resolution.

This is performed with [`rom1504/img2dataset`][img2dataset-github].

## Usage

- To download image data, run [`download_steam_webdataset.ipynb`][download_steam_webdataset-notebook].
[![Open In Colab][colab-badge]][download_steam_webdataset-notebook]

Alternatively, you can find the data as `v0.1` in the ["Releases" section][github-releases] of this repository.

- To match images, run [`match_steam_banners_with_BEiT.ipynb`][match_steam_banners_with_BEiT-notebook].
[![Open In Colab][colab-badge]][match_steam_banners_with_BEiT-notebook]

## References

-   Microsoft's Bidirectional Encoder representation from Image Transformers (BEiT):
    - [Documentation][hugging-face-doc] and [model checkpoints][hugging-face-models] at HuggingFace
    - [Official Github repository][ms-beit-code]
    - [Bao, Hangbo, et al. *BEiT: BERT Pre-Training of Image Transformers*. arXiv 2021.][ms-beit-paper]
-   A generic repository to match images:
    - [`match-steam-banners`][banner-repository-generic]: retrieve games with similar banners,
-   My usage of Google's Big Transfer (BiT):
    - [`steam-BiT`][banner-repository-BiT]: retrieve games with similar banners, using Google's BiT,
-   My usage of Facebook's DINO:
    - [`steam-DINO`][banner-repository-DINO]: retrieve games with similar banners, using Facebook's DINO (resolution 224),
-   My usage of OpenAI's CLIP:
    - [`steam-CLIP`][banner-repository-CLIP]: retrieve games with similar banners, using OpenAI's CLIP (resolution 224),
    - [`steam-image-search`][natural-language-search]: retrieve games using natural language queries,
    - [`heroku-flask-api`][my-flask-API]: serve the matching results through an API built with Flask on Heroku.

<!-- Definitions -->

[wiki-cover]: <https://github.com/woctezuma/steam-BEiT/wiki/img/illustration.jpg>
[download_steam_webdataset-notebook]: <https://colab.research.google.com/github/woctezuma/steam-BiT/blob/main/download_steam_webdataset.ipynb>
[match_steam_banners_with_BEiT-notebook]: <https://colab.research.google.com/github/woctezuma/steam-BEiT/blob/main/match_steam_banners_with_BEiT.ipynb>

[openai-dalle]: <https://github.com/openai/dall-e>

[github-releases]: <https://github.com/woctezuma/steam-BiT/releases>
[img2dataset-github]: <https://github.com/rom1504/img2dataset>

[hugging-face-models]: <https://huggingface.co/models?filter=beit>
[hugging-face-doc]: <https://huggingface.co/transformers/master/model_doc/beit.html>
[ms-beit-code]: <https://github.com/microsoft/unilm/tree/master/beit>
[ms-beit-paper]: <https://arxiv.org/abs/2106.08254>

[banner-repository-generic]: <https://github.com/woctezuma/match-steam-banners>
[banner-repository-BiT]: <https://github.com/woctezuma/steam-BiT>
[banner-repository-DINO]: <https://github.com/woctezuma/steam-DINO>

[banner-repository-CLIP]: <https://github.com/woctezuma/steam-CLIP>
[natural-language-search]: <https://github.com/woctezuma/steam-image-search>
[my-flask-API]: <https://github.com/woctezuma/heroku-flask-api>

[colab-badge]: <https://colab.research.google.com/assets/colab-badge.svg>
