# Tải dữ liệu arguana và chuyển đổi thành định dạng phù hợp
python preprocess_TR2016.py --input arguana --output arguana_kilt.jsonl

# Tạo bảng nhắc đến và cây tiền tố
python preprocess_mention_dicts.py --input arguana_kilt.jsonl --output mention_dict.pkl
python preprocess_tries.py --mention_dict mention_dict.pkl --output trie.pkl

# Tạo dữ liệu huấn luyện cho mGENRE
python preprocess_mgenre.py --input arguana_kilt.jsonl --mention_dict mention_dict.pkl --output train_data.jsonl

# Tiền xử lý với Fairseq
bash preprocess_fairseq.sh train_data.jsonl bin

# Cập nhật đường dẫn dataset trong train.sh
# Ví dụ: DATASET="path/to/arguana/bin"

# Chạy huấn luyện
bash train.sh
