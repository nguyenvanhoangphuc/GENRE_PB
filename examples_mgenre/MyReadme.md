## mGenre for fairseq
git clone --branch fixing_prefix_allowed_tokens_fn https://github.com/nicola-decao/fairseq
cd fairseq
pip install --editable ./

## Download Pretrained model 
fairseq_multilingual_entity_disambiguation bỏ trong thư mục models
lang_title2wikidataID-normalized_with_redirect.pkl bỏ trong thư mục data
titles_lang_all105_marisa_trie_with_redirect bỏ trong thư mục data

## mGENRE for transformers
Đoạn trên hướng dẫn cài đặt và sử dụng mGENRE (Multilingual Generative Entity Resolution), một mô hình cho phép giải quyết vấn đề phân giải thực thể (entity disambiguation) đa ngôn ngữ. Đây là mô hình được phát triển trên thư viện fairseq và cũng có thể chuyển đổi để dùng trên transformers.
```
git clone --branch fixing_prefix_allowed_tokens_fn https://github.com/nicola-decao/fairseq
cd fairseq
pip install --editable ./
```
Điều này sẽ cài đặt fairseq ở chế độ chỉnh sửa, cho phép thay đổi mã nguồn mà không cần cài đặt lại.

## Tải Trie và Định nghĩa Hàm Giới Hạn
Tải cây tiền tố (trie) và định nghĩa hàm để áp dụng giới hạn với entities trie. Trie giúp mGENRE tìm kiếm chính xác các thực thể liên quan trong một ngữ cảnh nhất định.
```
import pickle
from genre.trie import Trie, MarisaTrie

with open("../data/lang_title2wikidataID-normalized_with_redirect.pkl", "rb") as f:
    lang_title2wikidataID = pickle.load(f)
```
lang_title2wikidataID: Đoạn này tải bản đồ ánh xạ từ các tiêu đề Wikipedia (dựa trên ngôn ngữ) sang mã định danh trên Wikidata từ một tệp .pkl. Bản đồ này được sử dụng để tìm ra mã định danh Wikidata của thực thể sau khi mô hình sinh ra tiêu đề thực thể.

Input: 