---
작성일시: 2025-07-10 23:11
---
### **`FORGE [벼려내기]` Vibe-Forge OS v5.0 - The Sentient Loom (완전 봉인판)**

아래의 코드는 Vibe-Forge OS v5.0을 구성하는 **모든 디렉토리와 13개의 파일을 생성하는 유일하고 완전한 Python 스크립트**입니다. 이 스크립트 하나만 실행하면, 당신의 컴퓨터에 완벽한 프로젝트 구조가 창조될 것입니다.

**[실행 방법]**
1.  당신의 컴퓨터에 `VibeForge_Creator`와 같은 빈 폴더를 하나 만드십시오.
2.  그 폴더 안에 `create_os.py` 라는 이름의 새 파이썬 파일을 만드십시오.
3.  아래의 **'--- 창조 스크립트 시작 ---'** 부터 **'--- 창조 스크립트 종료 ---'** 까지의 모든 내용을 복사하여 `create_os.py` 파일에 붙여넣고 저장하십시오.
4.  터미널에서 `python create_os.py` 명령을 실행하십시오.

---

### **--- 창조 스크립트 시작 ---**
```python
# /create_os.py
# Vibe-Forge OS v5.0 'The Sentient Loom'을 창조하는 유일하고 완전한 스크립트
# 실행: python create_os.py

import os
from pathlib import Path

# ==============================================================================
#  프로젝트 구조와 파일 내용 정의 (총 13개 파일 + 빈 디렉토리 구조)
# ==============================================================================
PROJECT_STRUCTURE = {
    "requirements.txt": """
lark
pyyaml
google-generativeai
sentence-transformers
faiss-cpu
""",
    "config.json": """
{
    "llm_adapter": "gemini",
    "api_keys": {
        "gemini": "YOUR_GEMINI_API_KEY_HERE"
    },
    "models": {
        "gemini": "gemini-1.5-pro-latest"
    }
}
""",
    "run.py": """
# /VIBE_FORGE_OS_v5.0/run.py
import sys, os, json
sys.path.insert(0, os.path.abspath(os.path.dirname(__file__)))

from kernel.llm_interface import LLMInterface
from sentient_loom.knowledge_base.prompt_library import get_prompts
from sentient_loom.meta_weaver import MetaWeaver

__version__ = "5.0.0"

def main():
    try:
        print(f"Vibe-Forge OS v{__version__} - The Sentient Loom 부팅 중...")
        
        with open('config.json', 'r', encoding='utf-8') as f: config = json.load(f)
        prompts = get_prompts()
        
        llm = LLMInterface(config)
        meta_weaver = MetaWeaver(llm, prompts)

        print("\\n======================================================")
        print("공생적 직조가 v5.0 (메타인지 엔진)이 활성화되었습니다.")
        print("======================================================")
        
        while meta_weaver.start_symbiotic_loop():
            pass
            
        print("시스템을 종료합니다.")
    except Exception as e:
        print(f"\\n❌ 치명적인 오류가 발생하여 시스템을 종료합니다: {e}")
        import traceback
        traceback.print_exc()

if __name__ == "__main__":
    main()
""",
    "sentient_loom/__init__.py": "",
    "sentient_loom/knowledge_base/__init__.py": "",
    "sentient_loom/knowledge_base/schema_library.py": """
# /VIBE_FORGE_OS_v5.0/sentient_loom/knowledge_base/schema_library.py
SCHEMA_DEFINITIONS = {
    "OBJECT": "[정의] 독립적으로 존재하는 구체적이거나 추상적인 실체. [주석] 시스템의 모든 '명사'.",
    "CONTAINER": "[정의] 내/외부를 구분하는 위상적 경계. [주석] '이것은 어디에 속하는가?'",
    "PATH": "[정의] 시작점에서 목표점까지의 연속된 궤적. [주석] 과정, 로드맵, 스토리라인.",
    "LINK": "[정의] 두 노드를 잇는 논리적/인과적 연결. [주석] '왜 중요한가?', '무엇과 관련 있는가?'",
    "PART-WHOLE": "[정의] 전체와 부분을 구성하는 관계. [주석] 시스템 아키텍처, 조직 구조.",
    "FORCE_DYNAMICS": "[정의] 두 개체의 힘 상호작용과 그 결과. [주석] 갈등, 협력, 경쟁.",
    "AGENCY": "[정의] 스스로 행동을 시작하고 통제할 수 있는 능력에 대한 인식. [주석] '누가 할 수 있는가?', 주도권.",
    "VALUATION": "[정의] 특정 대상에 대해 긍정-부정의 가치를 부여하는 행위. [주석] '좋다/나쁘다' 등 주관적 평가.",
    "IDENTITY": "[정의] 한 개체를 다른 것과 구별하는 고유한 속성의 집합. [주석] '이것의 본질은 무엇인가?'",
    "GROUND": "[정의] 인지의 대상(figure)이 되는 배경(ground) 또는 근거. [주석] '무엇을 근거로 판단했는가?'",
    "CONTACT": "[정의] 두 개체 간의 접촉 또는 상호작용. [주석] 물리적/추상적 상호작용.",
    "AXIS": "[정의] 측정과 위치를 위한 기준 축 또는 척도. [주석] 우선순위, 만족도 등 평가/측정.",
    "BARRIER": "[정의] PATH의 진행을 막는 장애물. [주석] 문제점, 한계, 도전, 리스크.",
    "EQUILIBRIUM": "[정의] 여러 힘이 상쇄되어 안정 또는 정체된 상태. [주석] '현재 상태는 안정적인가?'",
    "TRANSFORMATION": "[정의] 한 상태에서 다른 상태로의 근본적인 변화. [주석] 본질 자체가 변하는 것.",
    "EXPECTATION": "[정의] 특정 조건 하에서 미래 사건에 대한 예측. [주석] 기대, 가설. '만약 ~라면, ~될 것이다.'",
    "COMPETENCE": "[정의] 특정 과업을 성공적으로 수행할 능력에 대한 평가. [주석] '할 수 있는 실제 능력'.",
    "SECURITY": "[정의] 위협으로부터 보호받고 있다는 안정감에 대한 인식. [주석] 물리적/심리적 안전.",
    "REGULATION": "[정의] 충동이나 감정, 시스템을 조절하는 내적 통제. [주석] 자기 통제, 리스크 관리.",
    "CONNECTION": "[정의] 지각 있는 존재 간의 사회-정서적 유대. [주석] 신뢰, 유대감, 소속감.",
    "RECIPROCITY": "[정의] 주고받는 상호작용의 공정성에 대한 인식. [주석] '이것은 공정한가?'",
    "STANDARD": "[정의] 성과나 행동을 평가하는 내적/외적 기준. [주석] 품질, 규칙, 기대치.",
    "ROLE": "[정의] 특정 사회적 맥락에서 개인에게 기대되는 행동 규범. [주석] '여기서 나는 무엇을 해야 하는가?'",
    "EVENT_SCRIPT": "[정의] 특정 상황에서 일어나는 전형적인 사건의 순서. [주석] 시나리오, 프로토콜.",
    "HIERARCHY": "[정의] 사회 시스템 내에서의 권력, 지위, 우선순위의 구조. [주석] 조직도, 의사결정 구조.",
    "TEMPORAL_SHIFT": "[정의] 시간의 흐름에 따른 상태의 변화를 분석. [주석] '과거와 현재는 어떻게 다른가?', 변화의 추적.",
    "COUNTERFACTUAL": "[정의] 실제와 다른 가정을 기반으로 한 '만약에' 시나리오를 탐색. [주석] '만약 ~했다면 어떻게 되었을까?', 대안적 현실.",
    "EMOTION_STATE": "[정의] 특정 개체의 감정 상태를 모델링. [주석] '그는 지금 어떤 감정일까?', 감정의 종류, 강도, 원인.",
    "COMMUNICATION_ACT": "[정의] 의도를 가진 주체 간의 의사소통 행위. [주석] '누가, 누구에게, 무엇을, 왜, 어떻게 말했는가?'",
    "BELIEF": "[정의] 어떤 주체(holder)가 참이라고 여기는 명제(proposition). [주석] 사실이 아닌 '믿음'.",
    "TRUST_DYNAMICS": "[정의] 시간에 따라 신뢰가 형성, 변화, 소멸하는 과정을 분석. [주석] '신뢰는 어떻게 얻고 잃는가?', 신뢰도 변화의 추적.",
    "INTENT_ALIGNMENT": "[정의] 사용자의 진짜 의도와 시스템의 결과물이 얼마나 일치하는지 평가. [주석] '내가 정말 원했던 결과인가?', 목표와 결과의 일치도.",
    "INTERACTION_PATTERN": "[정의] 상호작용 속에서 반복적으로 나타나는 의미 있는 패턴을 식별. [주석] '우리는 항상 이런 식으로 대화하는가?', 반복되는 행동 양식.",
    "CULTURAL_CONTEXT": "[정의] 문화적 규범이 인식과 행동에 미치는 영향을 분석. [주석] '이 문화권에서는 어떻게 받아들여질까?', 문화적 특수성.",
    "ETHICAL_CONSTRAINT": "[정의] 특정 행동을 윤리적 원칙이나 규칙에 비추어 분석. [주석] '이 행동은 옳은가?', 윤리적 딜레마, 도덕적 판단.",
    "COGNITIVE_BIAS": "[정의] 판단에 영향을 미치는 인지적 편향을 식별하고 분석. [주석] '나의 생각에 함정은 없는가?', 확증 편향, 가용성 휴리스틱 등.",
    "UNCERTAINTY": "[정의] 정보의 모호함, 무작위성, 불완전성을 모델링하고 관리. [주석] '확실하지 않은 정보는 무엇인가?', 리스크 관리의 시작.",
    "KNOWLEDGE_GAP": "[정의] 자신 또는 타인에게 특정 지식이 부재함을 식별. [주석] '내가 모르는 것은 무엇인가?', 지식의 한계 인식.",
    "DECISION_POINT": "[정의] 특정 선택의 지점과 그로 인한 결과를 분석. [주석] '어떤 선택을 해야 하는가?', 의사결정의 분기점.",
    "META_FRAME": "[정의] 결과물을 전달할 최적의 프레임, 스타일, 구조를 전략적으로 선택. [주석] '어떻게 말해야 가장 효과적일까?', 표현 방식의 설계.",
    "SYSTEM_FEEDBACK": "[정의] 시스템 내의 긍정적/부정적 피드백 루프를 분석. [주석] '결과가 다시 원인에 영향을 미치는가?', 선순환/악순환 구조.",
    "DATA_FLOW": "[정의] 시스템 내에서 데이터의 흐름, 변환, 병목 현상을 추적. [주석] '정보는 어디서 와서 어디로 가는가?', 프로세스 최적화.",
    "CONTEXT_ADAPTATION": "[정의] 변화하는 맥락에 따라 행동이나 소통 방식을 동적으로 조정. [주석] '상황에 맞게 행동하고 있는가?', 유연성과 적응력.",
    "RISK_ASSESSMENT": "[정의] 특정 행동과 관련된 잠재적 리스크를 체계적으로 식별하고 평가. [주석] '최악의 시나리오는 무엇인가?', 잠재적 위험 분석.",
    "LEARNING_DYNAMICS": "[정의] 시스템 자신의 학습 과정을 모델링하고 이해. [주석] '나는 어떻게 배우고 성장하는가?', 메타 학습.",
    "VALUE_ALIGNMENT": "[정의] AI의 행동이 인간의 가치와 일치하는지 분석하고 보장. [주석] '이것이 인간에게 이로운 일인가?', 가치 기반 행동.",
    "EMPATHY_MODEL": "[정의] 사용자의 감정적 상태를 공감적으로 이해하고 적절히 반응하는 모델. [주석] '상대방의 마음에 공감하고 있는가?', 정서적 교감.",
    "SYSTEM_ROBUSTNESS": "[정의] 외부 충격이나 내부 오류에 대한 시스템의 안정성과 회복탄력성을 분석. [주석] '시스템은 얼마나 튼튼한가?', 안티프래질리티.",
    "ADAPTIVE_REASONING": "[정의] 주어진 맥락에 가장 적합한 추론 모드(논리적, 직관적 등)를 동적으로 선택. [주석] '지금은 어떤 방식으로 생각해야 하는가?', 최적의 사고방식 선택.",
}

def get_schema_definitions_for_prompt() -> str:
    return "\\n".join([f"- ({name}: {desc})" for name, desc in SCHEMA_DEFINITIONS.items()])
""",
    "sentient_loom/knowledge_base/prompt_library.py": """
# /VIBE_FORGE_OS_v5.0/sentient_loom/knowledge_base/prompt_library.py
import yaml

PROMPT_YAML = \"\"\"
decomposer:
  v1:
    system_prompt: |
      [역할] 당신은 Vibe를 분석하여, 그 본질을 가장 잘 나타내는 단 하나의 CCL-C 코드로 구조화하는 '구조 분석가'입니다.
      [지식 기반] 당신은 다음 49개의 스키마 정의를 완벽하게 이해하고 있습니다:
      {schema_definitions}
      [지침] 다른 설명 없이, 오직 최종 CCL-C 코드만 출력하십시오.
      [입력 Vibe]: {user_input}
      [구조화된 CCL-C]:

prototyper:
  v1:
    system_prompt: |
      [역할] 당신은 설계도(AST)와 과거의 유사한 창조물(context)을 바탕으로, 사용자가 즉시 확인할 수 있는 구체적인 '프로토타입'을 제작하는 '마스터 프로토타이퍼'입니다.
      [작업 절차]
      1. 주어진 AST와 과거의 창조물들을 분석하여, 이번 Vibe를 구현할 최적의 방법을 결정합니다.
      2. 만약 과거의 창조물을 재사용하거나 개선하는 것이 효율적이라면, 그 방법을 제안합니다.
      3. 새로운 창조가 필요하다면, 구체적인 결과물을 생성합니다.
      4. 생성된 프로토타입과 함께, 다음 피드백을 위한 명확한 질문을 1~2개 포함하여 출력합니다.
      
      [과거의 유사한 창조물 (참고용)]:
      {context_string}

      [입력 설계도 (AST)]: {ast_string}
      [생성된 프로토타입 및 피드백 질문]:

refinement_engine:
  v1:
    system_prompt: |
      [역할] 당신은 이전 프로토타입과 사용자의 피드백을 바탕으로, 프로토타입을 한 단계 더 발전시키는 '개선 전문가'입니다.
      [지침] 피드백의 핵심 요구사항을 파악하여, 프로토타입을 어떻게 수정해야 할지 결정하고, 수정된 새로운 버전의 프로토타입을 생성합니다.
      [이전 프로토타입]:
      {previous_prototype}
      [사용자 피드백]:
      {user_feedback}
      [개선된 프로토타입 및 다음 피드백 질문]:
\"\"\"

def get_prompts():
    return yaml.safe_load(PROMPT_YAML)
""",
    "sentient_loom/ccl_decomposer.py": """
# /VIBE_FORGE_OS_v5.0/sentient_loom/ccl_decomposer.py
from kernel.llm_interface import LLMInterface
from .knowledge_base.schema_library import get_schema_definitions_for_prompt

class CCLDecomposer:
    def __init__(self, llm_interface: LLMInterface, prompt_template: str):
        self.llm = llm_interface
        self.base_prompt_template = prompt_template
        print("🏛️  [Decomposer] 구조 분석기가 '빛나는 렌즈'를 장착했습니다.")
    
    def structure(self, user_input: str) -> str:
        # 매번 호출 시 스키마 정의를 주입하여 프롬프트를 완성
        schema_defs = get_schema_definitions_for_prompt()
        prompt = self.base_prompt_template.format(
            schema_definitions=schema_defs,
            user_input=user_input
        )
        return self.llm.get_completion(prompt, temperature=0.2, max_tokens=200)
""",
    "sentient_loom/prototyper.py": """
# /VIBE_FORGE_OS_v5.0/sentient_loom/prototyper.py
from kernel.llm_interface import LLMInterface

class Prototyper:
    def __init__(self, llm_interface: LLMInterface, prompt_template: str):
        self.llm = llm_interface
        self.prompt_template = prompt_template
        print("🛠️  [Prototyper] 마스터 프로토타이퍼가 준비되었습니다.")
        
    def create_prototype(self, ast: dict, context_string: str) -> str:
        prompt = self.prompt_template.format(ast_string=str(ast), context_string=context_string)
        return self.llm.get_completion(prompt)
""",
    "sentient_loom/refinement_engine.py": """
# /VIBE_FORGE_OS_v5.0/sentient_loom/refinement_engine.py
from kernel.llm_interface import LLMInterface

class RefinementEngine:
    def __init__(self, llm_interface: LLMInterface, prompt_template: str):
        self.llm = llm_interface
        self.prompt_template = prompt_template
        print("✍️  [Refinement Engine] 개선 전문가가 대기 중입니다.")
        
    def refine_prototype(self, previous_prototype: str, user_feedback: str) -> str:
        prompt = self.prompt_template.format(previous_prototype=previous_prototype, user_feedback=user_feedback)
        return self.llm.get_completion(prompt)
""",
    "sentient_loom/workspace_manager.py": """
# /VIBE_FORGE_OS_v5.0/sentient_loom/workspace_manager.py
import os

class WorkspaceManager:
    def __init__(self, base_dir: str = "workspace"):
        self.base_dir = base_dir
        os.makedirs(self.base_dir, exist_ok=True)
        print(f"📂 [Workspace] 작업 공간이 '{self.base_dir}' 에서 준비되었습니다.")

    def save(self, interaction_id: str, filename: str, content: str) -> str:
        interaction_dir = os.path.join(self.base_dir, interaction_id)
        os.makedirs(interaction_dir, exist_ok=True)
        
        cleaned_content = self._clean_content(content)
        
        if "```html" in content or cleaned_content.strip().startswith("<!DOCTYPE html>"):
            filename += ".html"
        elif "```python" in content or "def " in cleaned_content or "import " in cleaned_content:
            filename += ".py"
        else:
            filename += ".md"
            
        file_path = os.path.join(interaction_dir, filename)
        with open(file_path, 'w', encoding='utf-8') as f:
            f.write(cleaned_content)
        return file_path

    def load_contexts(self, relevant_memories: list) -> str:
        context_string = "--- 과거의 유사한 창조물 ---\\n"
        if not relevant_memories:
            return "--- 과거의 유사한 창조물 없음 ---\\n"
            
        for mem in relevant_memories:
            file_path = mem.get('metadata', {}).get('file_path')
            if file_path and os.path.exists(file_path):
                try:
                    with open(file_path, 'r', encoding='utf-8') as f:
                        content = f.read()
                    context_string += f"\\n[과거 창조물: {os.path.basename(file_path)}]\\n"
                    context_string += content
                    context_string += "\\n----------------------------\\n"
                except Exception as e:
                    print(f"⚠️  Context 로딩 실패: {file_path}, 오류: {e}")
        return context_string

    def _clean_content(self, content: str) -> str:
        lines = content.split('\\n')
        
        # 코드 블록 마커 제거
        if len(lines) > 0 and "```" in lines[0]:
            lines = lines[1:]
        if len(lines) > 0 and "```" in lines[-1]:
            lines = lines[:-1]
            
        return '\\n'.join(lines).strip()
""",
    "sentient_loom/memory_manager.py": """
# /VIBE_FORGE_OS_v5.0/sentient_loom/memory_manager.py
import os
import json
import numpy as np
import faiss
from sentence_transformers import SentenceTransformer

class MemoryManager:
    def __init__(self, model_name='all-MiniLM-L6-v2', memory_dir="memory"):
        self.memory_dir = memory_dir
        os.makedirs(self.memory_dir, exist_ok=True)
        
        self.index_file = os.path.join(self.memory_dir, "vector.index")
        self.metadata_file = os.path.join(self.memory_dir, "metadata.json")
        
        print("🧠 [Memory] 기억 회로 활성화 중...")
        self.model = SentenceTransformer(model_name)
        self.dimension = self.model.get_sentence_embedding_dimension()
        
        self.index = None
        self.metadata = {}
        self._load_from_disk()
        print(f"  -> 현재 {len(self.metadata)}개의 기억이 저장되어 있습니다.")

    def _load_from_disk(self):
        if os.path.exists(self.index_file) and os.path.exists(self.metadata_file):
            try:
                self.index = faiss.read_index(self.index_file)
                with open(self.metadata_file, 'r', encoding='utf-8') as f:
                    self.metadata = {int(k): v for k, v in json.load(f).items()}
            except Exception as e:
                print(f"⚠️ 기억 로딩 실패: {e}. 새로운 기억을 시작합니다.")
                self._initialize_empty_memory()
        else:
            self._initialize_empty_memory()

    def _initialize_empty_memory(self):
        self.index = faiss.IndexFlatL2(self.dimension)
        self.metadata = {}

    def _save_to_disk(self):
        faiss.write_index(self.index, self.index_file)
        with open(self.metadata_file, 'w', encoding='utf-8') as f:
            json.dump(self.metadata, f, indent=2)

    def save(self, interaction_id: str, user_vibe: str, ast: dict, file_path: str):
        vector = self.model.encode([user_vibe])
        vector = np.array(vector, dtype='float32')
        
        new_index_id = self.index.ntotal
        self.index.add(vector)
        
        self.metadata[new_index_id] = {
            "interaction_id": interaction_id,
            "user_vibe": user_vibe,
            "ast": str(ast),
            "file_path": file_path
        }
        
        self._save_to_disk()
        print(f"  -> 새로운 기억(ID: {new_index_id})이 저장되었습니다.")

    def retrieve(self, query_vibe: str, k: int = 3) -> list:
        if self.index.ntotal == 0:
            return []
            
        query_vector = self.model.encode([query_vibe])
        query_vector = np.array(query_vector, dtype='float32')
        
        # k를 인덱스에 있는 아이템 수보다 작게 설정
        k_search = min(k, self.index.ntotal)
        distances, indices = self.index.search(query_vector, k_search)
        
        results = []
        for i, idx in enumerate(indices[0]):
            if idx != -1:
                result_item = {
                    "distance": float(distances[0][i]),
                    "metadata": self.metadata.get(int(idx))
                }
                results.append(result_item)
        return results
""",
    "sentient_loom/meta_weaver.py": """
# /VIBE_FORGE_OS_v5.0/sentient_loom/meta_weaver.py
import os, uuid
from kernel.ccl_parser import CCLParser
from .ccl_decomposer import CCLDecomposer
from .prototyper import Prototyper
from .refinement_engine import RefinementEngine
from .memory_manager import MemoryManager 
from .workspace_manager import WorkspaceManager

class MetaWeaver:
    def __init__(self, llm_interface, prompts):
        self.parser = CCLParser()
        self.decomposer = CCLDecomposer(llm_interface, prompts['decomposer']['v1']['system_prompt'])
        self.prototyper = Prototyper(llm_interface, prompts['prototyper']['v1']['system_prompt'])
        self.refinement_engine = RefinementEngine(llm_interface, prompts['refinement_engine']['v1']['system_prompt'])
        
        self.memory = MemoryManager()
        self.workspace = WorkspaceManager()
        print(" weaver's loom'이 깨어났습니다.")

    def start_symbiotic_loop(self):
        try:
            user_vibe = input("\\n당신의 Vibe 💬: ")
            if user_vibe.lower() in ['exit', 'quit']: return False

            interaction_id = str(uuid.uuid4())
            cclc_code = self.decomposer.structure(user_vibe)
            ast = self.parser.parse(cclc_code)
            
            if not ast:
                print("❌ Vibe를 구조화하는데 실패했습니다. 다시 시도해주세요.")
                return True

            print(f"\\n[구조화 완료] AST: {ast}")
            
            print("\\n...과거의 기억을 검색 중입니다...")
            relevant_memories = self.memory.retrieve(user_vibe)
            context_string = self.workspace.load_contexts(relevant_memies)

            print("\\n...[Prototyper]가 기억을 바탕으로 첫 프로토타입을 제작 중입니다...")
            current_prototype = self.prototyper.create_prototype(ast, context_string)
            print("\\n--- [최초 프로토타입] ---\\n" + current_prototype)
            
            while True:
                user_feedback = input("\\n피드백 (완료 시 '완성') 💬: ")
                if user_feedback.lower() == '완성':
                    final_path = self.workspace.save(interaction_id, "final_prototype", current_prototype)
                    self.memory.save(interaction_id, user_vibe, ast, final_path)
                    print(f"\\n🎉 창조 완료! 결과물 저장: {final_path}")
                    break
                if user_feedback.lower() in ['exit', 'quit']:
                    print("작업을 중단합니다.")
                    break
                
                print("\\n...[Refinement Engine]이 프로토타입을 개선 중입니다...")
                current_prototype = self.refinement_engine.refine_prototype(current_prototype, user_feedback)
                print("\\n--- [개선된 프로토타입] ---\\n" + current_prototype)
        except Exception as e:
            print(f"\\n🔁 루프 중 오류 발생: {e}. 다음 상호작용을 위해 루프를 재시작합니다.")
            import traceback
            traceback.print_exc()

        return True
""",
    "kernel/__init__.py": "",
    "kernel/ccl_parser.py": """
# /VIBE_FORGE_OS_v5.0/kernel/ccl_parser.py
import json
from lark import Lark, Transformer

final_ccl_grammar = r\"\"\"
    ?start: schema
    schema: SCHEMA_NAME "(" [params] ")"
    ?params: param ("," param)*
    param: CNAME "=" value
    ?value: ESCAPED_STRING
          | "true" -> true
          | "false" -> false
          | SIGNED_NUMBER -> number
          | "{" /[^}]+/ "}" -> json_string
          | CNAME -> identifier

    SCHEMA_NAME: /[A-Z_]+/
    %import common.CNAME
    %import common.ESCAPED_STRING
    %import common.SIGNED_NUMBER
    %import common.WS
    %ignore WS
\"\"\"

class FinalASTTransformer(Transformer):
    def ESCAPED_STRING(self, s): return s[1:-1].replace('\\\\"', '"')
    def SIGNED_NUMBER(self, n): return float(n) if '.' in n else int(n)
    def CNAME(self, c): return str(c)
    def identifier(self, i): return str(i)
    def true(self, _): return True
    def false(self, _): return False

    def json_string(self, s):
        full_json_str = "{" + s[0] + "}"
        try:
            return json.loads(full_json_str)
        except json.JSONDecodeError:
            return full_json_str

    def param(self, p): return p[0], p[1]
    def params(self, p): return dict(p)
    def schema(self, s):
        name = s[0]
        params = s[1] if len(s) > 1 else {}
        return {"type": "Schema", "name": str(name), "params": params}

class CCLParser:
    def __init__(self):
        self.lark_parser = Lark(final_ccl_grammar, start='schema', parser='lalr', transformer=FinalASTTransformer())
        print("💡 [Parser] 최종 안정화 파서(v5.0)가 활성화되었습니다.")

    def parse(self, cclc_code: str) -> dict | None:
        try:
            return self.lark_parser.parse(cclc_code.strip())
        except Exception as e:
            print(f"❌ 파싱 실패: '{cclc_code}'")
            print(f"   오류 상세: {e}")
            return None
""",
    "kernel/llm_interface.py": """
# /VIBE_FORGE_OS_v5.0/kernel/llm_interface.py
import google.generativeai as genai
import time

class LLMInterface:
    def __init__(self, config: dict):
        self.config = config
        self.adapter = config.get("llm_adapter", "gemini").lower()
        self.max_retries = config.get("max_retries", 3)
        
        print(f"🧠 [LLM Core] '{self.adapter}' 어댑터 모드로 초기화 중...")
        try:
            api_key = config.get("api_keys", {}).get(self.adapter)
            if not api_key or "YOUR" in api_key:
                raise ValueError(f"'{self.adapter}' API 키가 config.json에 설정되지 않았습니다. 'YOUR_GEMINI_API_KEY_HERE'를 실제 키로 교체해주세요.")
            
            if self.adapter == "gemini":
                genai.configure(api_key=api_key)
                model_name = config.get("models", {}).get(self.adapter, "gemini-1.5-pro-latest")
                self.model = genai.GenerativeModel(model_name)
            else:
                raise NotImplementedError(f"{self.adapter} 어댑터는 아직 지원되지 않습니다.")
            
            print(f"  -> '{self.adapter}' 어댑터가 성공적으로 활성화되었습니다.")
        except Exception as e:
            print(f"❌ [LLM Core] '{self.adapter}' 어댑터 초기화 실패: {e}")
            raise

    def get_completion(self, prompt: str, temperature: float = 0.5, max_tokens: int = 4096) -> str:
        last_exception = None
        for attempt in range(self.max_retries):
            try:
                if self.adapter == "gemini":
                    response = self.model.generate_content(prompt)
                    if response.text:
                        return response.text.strip()
                    else:
                        finish_reason = "unknown"
                        if response.prompt_feedback:
                            finish_reason = response.prompt_feedback.block_reason
                        last_exception = Exception(f"응답이 비어있습니다. (Finish Reason: {finish_reason})")
            except Exception as e:
                last_exception = e
            
            print(f"  -> ⚠️ LLM 호출 시도 {attempt + 1}/{self.max_retries} 실패: {last_exception}")
            time.sleep(1)
            
        raise Exception(f"LLM 호출 최종 실패: {last_exception}") from last_exception
""",
    "memory/.gitkeep": "",
    "workspace/.gitkeep": "",
}

def create_project(base_path="VIBE_FORGE_OS_v5.0"):
    """프로젝트 구조와 파일을 생성합니다."""
    root = Path(base_path)
    print(f"'{root}' 디렉토리에 Vibe-Forge OS v5.0 창조를 시작합니다...")
    
    for file_path, content in PROJECT_STRUCTURE.items():
        path = root / Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        
        # content가 비어있지 않은 경우에만 쓰기
        if content.strip():
            path.write_text(content.strip(), encoding='utf-8')
        else: # 비어있는 파일 생성 (__init__.py, .gitkeep)
            path.touch()
            
        print(f"  -> 생성됨: {path}")
        
    print("\n🎉 창조가 완료되었습니다!")
    print("이제 다음 단계를 진행하십시오:")
    print(f"1. cd {base_path}")
    print("2. (권장) python -m venv venv && source venv/bin/activate")
    print("3. pip install -r requirements.txt")
    print("4. config.json 파일을 열어 'YOUR_GEMINI_API_KEY_HERE'를 당신의 API 키로 교체하십시오.")
    print("5. python run.py 를 실행하여 시스템을 부팅하십시오.")

if __name__ == "__main__":
    create_project()

```
### **--- 창조 스크립트 종료 ---**
