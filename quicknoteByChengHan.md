!!! 注意事項 !!!
用Lab GPU跑的話原先的 embedding_batch_size 會爆開 => 我有把他調成2跑過 可以順利執行
實際在跑時因為會有額外的one-shot prompt因此實際跑完的token數量一定不是我所記錄的


# Running Indexing & QA `reproduce/dataset`資料夾下的
dataset={dataset檔名}
ex: 
dataset=sample 
dataset=2wikimultihopqa
dataset=hotpotqa
dataset=musique
# Run OpenAI model
python main.py --dataset $dataset --llm_base_url https://api.openai.com/v1 --llm_name gpt-4o-mini --embedding_name nvidia/NV-Embed-v2

github https://github.com/OSU-NLP-Group/HippoRAG
HippoRAG 2-b31b1b"(https://arxiv.org/abs/2502.14802)
HippoRAG 1-b31b1b"(https://arxiv.org/abs/2405.14831)


`reproduce\dataset`: 實驗重現用的dataset (要其他的請至官網HugginFace )
`outputs\musique`: 轉換好三元組抽取結果的 "多跳問答資料集" (gpt-4o-mini"、"Llama-3.3-70B-Instruct")

# reproduce\dataset資料夾中
# 有_corpus：為offline Indexing的 建立 KG + Embeddings database用的檔案
# 沒有_corpus：的為提供 query 測試用資料（問題 + 正確答案 + 對應文件） 只是測試準確率使用!!


# 環境變數
export CUDA_VISIBLE_DEVICES=0,1
export VLLM_WORKER_MULTIPROC_METHOD=spawn
export HF_HOME=/datas/store162/chenghan/hf_home
export OPENAI_API_KEY=sk-FtWr6TPbLwCyq0uwGpYPQUDhIPiOEH1IcL-njESFqVT3BlbkFJxgam6aWocs3qaq-uD9J69EJ9GOrADz7BL_K4VklQwA 

### 此OPEN_API_KEY gpt-4o 每日上限為2,500,000 (250w個token)
`2wikimultihopqa_corpus`= 780,846 (78w個token)
`hotpotqa_corpus`= 1,534,427 (153w個token)
`musique_corpus`= 1,465,936 (146w個token)
`sample_corpus` = 382 (382個token)

# 目前已跑過的實驗 src.hipporag.HippoRAG:Evaluation results for retrieval:
sample : {'Recall@1': 0.0, 'Recall@2': 1.0, 'Recall@5': 1.0, 'Recall@10': 1.0, 'Recall@20': 1.0, 'Recall@30': 1.0, 'Recall@50': 1.0, 'Recall@100': 1.0, 'Recall@150': 1.0, 'Recall@200': 1.0}

2wikimultihopqa : {'ExactMatch': 0.601, 'F1': 0.6972} 

musique_corpus : 

sample_corpus : 