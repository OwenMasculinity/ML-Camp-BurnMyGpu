# Title Trigger - All titles you want
Google ML Camp-燃烧我的GPU-项目

![demo](./images/demo.png)
## Progress

* Tag Classification
- [x] (Pipeline) Training code
- [x] (Pipeline) Test code
- [x] (Pipeline) Inference API
- [x] (Model) PoolLSTM
- [x] (Model) RCNN+
- [x] (Model) Bert

* Keywords Extraction
- [x] (Pipeline) Test code
- [x] (Pipeline) Inference API

* Abstractive Summarization
- [x] (Pipeline) Training code
- [x] (Pipeline) Test code
- [x] (Pipeline) Inference API
- [x] (Model) Seq2seq+Attn
- [x] (Model) Effective Pointer generator

* Text Style Transfering
- [x] (Pipeline) Training code
- [x] (Pipeline) Test code

* Demo
- [x] Basic Layout
- [x] Attention Visualization


## Usage
### 1. Download the code and install
```bash
$ git@github.com:OwenMasculinity/ML-Camp-BurnMyGpu.git
$ python setup.py install
```

### 2. API
#### 2.1 Keywords Extraction
```python
from titletrigger.api import extract_keywords

content = "国务院总理李克强21日下午在中南海紫光阁会见中印边界问题印方特别代表"
extract_keywords(content, K=3)
```
#### 2.2 Extractive Summarization
```python

from titletrigger.api import ext_summarize
content = "国务院总理李克强21日下午在中南海紫光阁会见中印边界问题印方特别代表xxxx"

ext_headline = " ".join(ext_summarize([content])[0])
```

#### 2.3 Tag classification
```python
import sys
from titletrigger.api import tag_classify
sys.path.append('titletrigger/textclf')
clf_model_path = "YOU_MODEL_PATH"
clf_model_file = load_model(clf_model_path)
content = "国务院总理李克强21日下午在中南海紫光阁会见中印边界问题印方特别代表xxxx"
tag = tag_classify([content], clf_model_file)
```
pre-trained models can be downloaded in this [link](https://drive.google.com/open?id=1173TiJ4X_-2L5c43BdHG1kNA9svqeEOf)

#### 2.4 Abstractive classification
```python
import sys
from titletrigger.api import abs_summarize
sys.path.append('titletrigger/textsum')
clf_model_path = "YOU_MODEL_PATH"
content = "国务院总理李克强21日下午在中南海紫光阁会见中印边界问题印方特别代表xxxx"
result_dict = abs_summarize([content_list], sum_model_file)
tag = tag_classify(content_list, clf_model_file)
```
pre-trained models can be downloaded in this [link](https://drive.google.com/open?id=1svxKPlIHusm2ZzaLmUCP5KLwc8kWrH_C)

#### 2.5 Text Style Transfer
```python
from titletrigger.api import style_transfer
content = "国务院总理李克强21日下午在中南海紫光阁会见中印边界问题印方特别代表xxxx"
transferred_text = style_transfer(content)
```

### 3. Training
#### 3.1 Tag Classification
Downloading data from this [link](https://www.kaggle.com/noxmoon/chinese-official-daily-news-since-2016)
split it into ```train.csv```, ```valid.csv```, ```test.csv``` 
move them into titletrigger/textclf/data/chinese_news
```bash
$ cd titletrigger/textclf
$ ls data/chinese_news
train.csv
valid.csv
test.csv
$ python train.py -config conifg/config_rcnn.json
```
#### 3.2 Abstractive Summarization
move data splits into titletrigger/textclf/data/chinese_news
```bash
$ cd titletrigger/textclf
$ ls data/chinese_news
train.csv
valid.csv
test.csv
$ python train.py -config conifg/config_copynet.json
```

### 4. Demo
First open a httpserver
```bash
$ cd website
$ python -m http.server 8000
```
Open http://localhost:8000/demo.html in your browser
