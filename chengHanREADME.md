dataset=sample
dataset=2wikimultihopqa
dataset=hotpotqa
dataset=musique

# Run OpenAI model
python main.py --dataset $dataset --llm_base_url https://api.openai.com/v1 --llm_name gpt-4o-mini --embedding_name nvidia/NV-Embed-v2

# Run ollama 
OLLAMA_HOST=0.0.0.0:11434 /datas/store162/chenghan/ollama/bin/ollama serve <!-- 提供服務 -->
/datas/store162/chenghan/ollama/bin/ollama run llama3.1 <!-- 選定model: llama3.1 or 其他但得額外下載 -->


# HippoRAG 論文/git 網址
github https://github.com/OSU-NLP-Group/HippoRAG
HippoRAG 2-b31b1b"(https://arxiv.org/abs/2502.14802)
HippoRAG 1-b31b1b"(https://arxiv.org/abs/2405.14831)

# reproduce\dataset資料夾中
# 有_corpus：為offline Indexing的 建立 KG + Embeddings database用的檔案
# 沒有_corpus：的為提供 query 測試用資料（問題 + 正確答案 + 對應文件） 只是測試準確率使用!!


# 環境變數
export CUDA_VISIBLE_DEVICES=0,1
export VLLM_WORKER_MULTIPROC_METHOD=spawn
export HF_HOME=/datas/store162/chenghan/hf_home
export OPENAI_API_KEY=sk-FtWr6TPbLwCyq0uwGpYPQUDhIPiOEH1IcL-njESFqVT3BlbkFJxgam6aWocs3qaq-uD9J69EJ9GOrADz7BL_K4VklQwA


