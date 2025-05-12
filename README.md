

# Multimode-RAG

![image](https://github.com/user-attachments/assets/54825b8f-6339-4079-9bb3-da9a50a8bf3e)





1. Extract text, tables, and images from PDF files using partitioning techniques and document structure analysis.
분할 기술과 문서 구조 분석을 사용하여 PDF 파일에서 텍스트, 표 및 이미지를 추출. PDF 낱장으로 분리후 -> 이미지(표, 차트)를 바운딩박스로 설정하여 크롭한후 저장 

2. Categorize extracted elements into text and tables based on their type.
추출된 요소를 유형에 따라 텍스트와 테이블로 분류

3. Generate summaries for text elements using LLM, optionally splitting long texts into manageable chunks.
LLM을 사용하여 텍스트 요소에 대한 요약을 생성하고 선택적으로 긴 텍스트를 관리 가능한 덩어리로 분할. 

4. Encode images as base64 strings and summarize them using an OpenAI Vision model.
이미지를 base64 문자열로 인코딩하고 Vision 모델을 사용하여 요약. LLaVA 또는 Qwen와 같은 모델을 사용해 이미지에서 요약을 생성.

5. Create a multi-vector retriever to index summaries and raw contents of text, tables, and images.
텍스트, 표, 이미지의 요약과 원시 콘텐츠를 색인화하는 다중 벡터 검색기를 생성. 이미지 자체를 llm에게 전달하기 보다는 이미지의 요약한 본을 만들어 텍스트와 함께 벡터 db에 저장 진행

6. Initialize a vector store using the Chroma vector store with OpenAI embeddings.
LLM 임베딩이 포함된 Chroma 벡터 저장소를 사용하여 벡터 저장소를 초기화

7. Construct a multi-modal RAG chain for processing user questions with both textual and visual context.
텍스트 및 시각적 컨텍스트를 모두 사용하여 사용자 질문을 처리하기 위한 다중 모드 RAG 체인을 구축

8. Retrieve relevant documents based on a user query using the multi-vector retriever.
다중 벡터 검색기를 사용하여 사용자 쿼리를 기반으로 관련 문서를 검색

9. Invoke the multi-modal RAG chain to generate a response to the user query.
다중 모드 RAG 체인을 호출하여 사용자 쿼리에 대한 응답을 생성


## 목표
1. 오픈소스만 구성된 RAG 파이프라인 구축
2. RTX 3090 or RTX 4090 환경
3. 추론능력


## method

1. Use a multimodal LLM (such as Deep Seek, Qwen 2.5 VL, exaone 3.5) to produce text summaries from images.
2. Embed and retrieve image summaries and texts chunks.
3. Pass image summaries and text chunks to a text LLM for answer synthesis.

## backend

- Use the [multi-vector retriever](https://python.langchain.com/docs/modules/data_connection/retrievers/multi_vector) with [Chroma](https://www.trychroma.com/) to store raw text (or tables) and images (in a docstore) along with their summaries (in a vectorstore) for retrieval. 
- Use Qwen 2.5-VL 7B for image summarization.
- Use Deepseek for final answer synthesis from join review of image summaries and texts (or tables).

## gpu
- RUNPOD (RTX 3090, RTX 4090)


## Stack

1. Vector DB
- Qdrant
- chroma(고려중.)

2. VLM
- Qwen 2.5 VL 13B

3. LLM
- deepseek r1-7b
- exaone 3.5

4. Chunking
- Docling

5 Embeding model
- bge m3 ko

6. Reranker model
- bge m3 Reranker

## Reference 

1. https://www.csdn.net/?spm=1001.2101.3001.4476
2. https://osguider.com/blog/
3. https://ai.gitcode.com/models?utm_source=highlight_word_gitcode
