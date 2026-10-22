## Scripts

<!-- create venv -->
python3 -m venv .venv 

<!-- activate it -->
source .venv/bin/activate
pip install -r requirements.txt

<!-- Checking if all the requirements have been installed -->
pip list

## Requirement.txt
AI / LLM
openai
langchain-openai

Agent
langgraph
langgraph-checkpoint
langsmith

RAG
langchain-community
langchain-huggingface
sentence-transformers

向量数据库
faiss-cpu
pinecone
langchain-pinecone

数据分析
pandas
scikit-learn

深度学习
torch

SQL 数据库
SQLAlchemy
pyodbc

文档处理
pypdf
openpyxl

配置管理
python-dotenv
pydantic-settings
 
前端界面
streamlit
altair