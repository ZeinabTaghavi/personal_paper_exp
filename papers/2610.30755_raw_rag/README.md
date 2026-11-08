# Is Complex Agentic Memory Always Needed? Naive RAG Is Stronger Than We Thought

Paper: [arXiv:2610.30755v1](https://arxiv.org/abs/2610.30755)  
Authors: Zhengye Bao, Shengtao Zhang, Haokai Zhang, Shiqi Lou, Muning Wen, and Minnan Luo (2026)  
Official code: [Litmeb/RAW-RAG](https://github.com/Litmeb/RAW-RAG) (MIT license)

## Classification

This is a **methodological paper**, not a new-dataset paper. It evaluates a deliberately simple long-term-memory baseline, RAW-RAG, on LoCoMo, LongMemEval, MEME, MemoryAgentBench, and (in the appendix) PersonaMem-v2.

## Method in one paragraph

RAW-RAG preserves timestamped conversation history as raw text instead of extracting or mutating memory records. The paper splits history into 256-token windows with 32-token overlap, retrieves the 128 nearest windows by dense cosine similarity, reranks them with a cross-encoder, and gives the best 15 to a reader LLM. Selected windows can be expanded back to complete source turns. The central result is that this carefully configured baseline is competitive with, and often stronger than, more elaborate agentic-memory systems on the evaluated tasks.

## Availability

The official implementation and experiment configurations are public. The repository expects LoCoMo, LongMemEval-S, and MEME files to be placed in its data directory; it downloads MemoryAgentBench automatically. Full paper reproduction also requires configured embedding, reranking, reader, and judge services. The optional PersonaMem-v2 experiment requires separately prepared benchmark and chat-history files.

The paper does not define a single new dataset schema. `examples.json` is therefore a clearly marked **synthetic** conversation in a minimal source-preserving format: conversation ID, timestamped messages, a question, and an expected answer. It is only for demonstrating the method.

## Colab demo

`demo.ipynb` implements the paper's essential retrieval path:

1. load the local synthetic JSON record (or use an embedded fallback in Colab);
2. serialize timestamped raw turns without summarizing or mutating them;
3. create overlapping token windows linked to their source turns;
4. retrieve candidates with a small local dense embedding model;
5. rerank candidates with a small local cross-encoder;
6. expand selected windows to complete turns and assemble a reader-ready prompt.

The notebook uses `sentence-transformers/all-MiniLM-L6-v2` and `cross-encoder/ms-marco-MiniLM-L6-v2`, with smaller retrieval depths and 64-token windows so it runs comfortably on a Colab CPU. These are transparent substitutions for the paper's production configurations (for example, Qwen3-Embedding-4B plus Qwen3-Reranker-4B, or hosted embedding/reranking services). It does not reproduce the benchmark scores and does not call a reader LLM.

## Run

Open `demo.ipynb` in Google Colab and run all cells. Internet access is needed once to install `sentence-transformers` and download the two small public models. No API key is required.
