### Context
오늘은 LangChain의 핵심 구성 요소(Prompt Templates, ChatModels, Chains)를 학습하고 LCEL(LangChain Expression Language)을 활용하여 텍스트 요약 체인을 복습했습니다. LangChain은 복잡한 LLM(Large Language Model) 기반 애플리케이션을 구축하기 위한 프레임워크입니다.

### Core
**Prompt Templates & ChatModels**: 
```python
from langchain.prompts import PromptTemplate

prompt = PromptTemplate(
    input_variables=["input_text"],
    template="Summarize the following: {input_text}"
)

# ChatModel usage example
chat_model = ChatModel.from_pretrained("model-name")
response = chat_model.generate(prompt("Long text to summarize..."))
```
프롬프트 템플릿과 챗 모델을 결합하여 일관된 응답을 생성합니다.

**LCEL 파이프라인**:
```python
from langchain.lcel import Pipe

data_pipe = Pipe().add_nodes([
    LoadDataNode(),
    SummaryNode(),
    OutputNode()
])
result = data_pipe.run(input_data)
```
LCEL(Pipe 연산자)를 이용하여 데이터 흐름을 선언적으로 관리합니다.

### Insight
LangChain V0.3과 V1.0+의 주요 차이점은 **유연성**과 **안정성**입니다. 
- **V0.3**까지는 클래스 기반의 레거시 체인으로 인해 복잡한 상속 구조를 필요로 했습니다. 
- **V1.0+**에서는 LCEL 기반의 선언적 설계로 전환되었습니다. 이는 파이프라인의 가독성을 높이고 유지보수를 용이하게 합니다.
- First-class streaming 지원으로 스트리밍 구현의 복잡성을 줄였습니다. 

이러한 변화는 LangChain이 단순한 라이브러리를 넘어 커스텀 체인 조립을 지원하는 프레임워크로 진화했음을 나타냅니다.

**출처:** [LangChain Official Documentation](https://docs.langchain.com/)