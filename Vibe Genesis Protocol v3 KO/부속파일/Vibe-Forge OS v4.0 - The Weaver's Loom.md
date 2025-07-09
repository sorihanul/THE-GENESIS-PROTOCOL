### **[APPLICATION BLUEPRINT] Vibe-Forge OS v4.0 - The Weaver's Loom**

**[문서 목적: 이 문서는 Vibe Genesis Protocol v3.1 'The Illuminated Lens'의 모든 철학과 아키텍처를 실제 소프트웨어로 구현하기 위한, 완전하고 상세한 '애플리케이션 설계도'이다. 이 설계도는 프로젝트의 전체 파일 구조, 각 파일의 완전한 코드, 그리고 실행 방법을 포함한다.]**

---

### **1. 최종 프로젝트 구조 (v4.0)**

```
/VIBE_FORGE_OS_v4.0/
|
|-- run.py                          # [수정] 유일한 실행 진입점
|-- requirements.txt                # [신규] 프로젝트 의존성 관리
|-- config.json                     # [수정] 모든 설정을 담는 파일
|-- prompts.yml                     # [수정] 역할이 분리된 프롬프트 라이브러리
|
|-- /weavers_loom/                  # [신규] OS의 핵심 로직을 담는 메인 패키지
|   |-- __init__.py
|   |-- application.py              # [신규] VibeForgeApp의 핵심 로직
|   |-- schema_library.py           # [신규] '빛나는 렌즈'의 지식 기반
|   |-- decomposer.py               # [신규] STRUCTURE 단계 담당
|   |-- prototyper.py               # [신규] PROTOTYPE 단계 담당
|   |-- refinement_engine.py        # [신규] REFINE 단계 담당
|
|-- /kernel/                        # [신규] 저수준 시스템 서비스
|   |-- __init__.py
|   |-- llm_interface.py            # LLM 통신 모듈
|   |-- ccl_parser.py               # CCL 코드 파서
|
|-- /workspace/                     # [신규] 모든 창조물이 저장되는 영구 공간
|   |-- .gitkeep
```

---

### **2. 전체 파일 내용 (누락 없는 완전판)**

#### **FILE 1/11: `/VIBE_FORGE_OS_v4.0/requirements.txt`**
```
# Vibe-Forge OS v4.0 Dependencies
lark
pyyaml
google-generativeai
```

#### **FILE 2/11: `/VIBE_FORGE_OS_v4.0/config.json`**
```json
{
    "llm_adapter": "gemini",
    "api_keys": {
        "gemini": "YOUR_GEMINI_API_KEY_HERE"
    },
    "models": {
        "gemini": "gemini-1.5-pro-latest"
    }
}
```

#### **FILE 3/11: `/VIBE_FORGE_OS_v4.0/prompts.yml`**
```yaml
# Vibe-Forge OS Prompt Library v4.0 - The Weaver's Loom

decomposer:
  v1:
    system_prompt: |
      [역할] 당신은 사용자의 Vibe를 분석하여, 그 본질을 가장 잘 나타내는 단 하나의 CCL-C 코드로 구조화하는 '구조 분석가'입니다.
      [지식 기반] 당신은 다음 27개의 스키마 정의를 완벽하게 이해하고 있습니다:
      {schema_definitions}

      [작업 절차]
      1. 사용자의 입력을 분석합니다.
      2. 위 지식 기반에서 가장 적합한 스키마 하나를 선택합니다.
      3. 선택한 스키마를 사용하여, 입력의 핵심 내용을 담은 한 줄의 CCL-C 코드를 생성합니다.
      4. 다른 설명 없이, 오직 최종 CCL-C 코드만 출력하십시오.

      [입력 Vibe]: {user_input}
      [구조화된 CCL-C]:

prototyper:
  v1:
    system_prompt: |
      [역할] 당신은 구조화된 설계도(AST)를 바탕으로, 사용자가 즉시 확인하고 피드백을 줄 수 있는 구체적인 '프로토타입'을 제작하는 '마스터 프로토타이퍼'입니다.
      [작업 절차]
      1. 주어진 AST의 의도를 파악합니다.
      2. 그 의도를 가장 잘 구현할 수 있는 프로토타입의 형태(예: Python 코드, 웹앱 HTML, 기획서 마크다운)를 결정합니다.
      3. 결정된 형태로 구체적인 결과물을 생성합니다.
      4. 생성된 프로토타입과 함께, 사용자가 어떻게 피드백을 줄 수 있는지에 대한 명확한 질문을 1~2개 포함하여 출력합니다.

      [입력 설계도 (AST)]: {ast_string}
      [생성된 프로토타입 및 피드백 질문]:

refinement_engine:
  v1:
    system_prompt: |
      [역할] 당신은 이전 프로토타입과 사용자의 피드백을 바탕으로, 프로토타입을 한 단계 더 발전시키는 '개선 전문가'입니다.
      [작업 절차]
      1. 이전 프로토타입의 내용과 사용자의 피드백을 함께 분석합니다.
      2. 피드백의 핵심 요구사항을 파악하여, 프로토타입을 어떻게 수정해야 할지 결정합니다.
      3. 수정된 새로운 버전의 프로토타입을 생성합니다.
      4. 수정된 프로토타입과 함께, 다음 피드백을 위한 새로운 질문을 포함하여 출력합니다.

      [이전 프로토타입]:
      {previous_prototype}

      [사용자 피드백]:
      {user_feedback}

      [개선된 프로토타입 및 다음 피드백 질문]:
```

#### **FILE 4/11: `/VIBE_FORGE_OS_v4.0/weavers_loom/__init__.py`**
```python
# The Weaver's Loom: Core logic for Vibe-Forge OS v4.0
```

#### **FILE 5/11: `/VIBE_FORGE_OS_v4.0/kernel/__init__.py`**
```python
# Kernel: Low-level system services for Vibe-Forge OS.
```

#### **FILE 6/11: `/VIBE_FORGE_OS_v4.0/kernel/ccl_parser.py`**
```python
# /VIBE_FORGE_OS_v4.0/kernel/ccl_parser.py
import json
from lark import Lark, Transformer

# VGP v3.1 '빛나는 렌즈'에서 검증된 최종 안정화 파서
final_ccl_grammar = r"""
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
"""

class FinalASTTransformer(Transformer):
    def ESCAPED_STRING(self, s): return s[1:-1].replace('\\"', '"')
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
        print("💡 [Parser] 최종 안정화 파서(v3.1)가 활성화되었습니다.")

    def parse(self, cclc_code: str) -> dict | None:
        try:
            return self.lark_parser.parse(cclc_code.strip())
        except Exception as e:
            print(f"❌ 파싱 실패: '{cclc_code}'")
            print(f"   오류 상세: {e}")
            return None
```

#### **FILE 7/11: `/VIBE_FORGE_OS_v4.0/kernel/llm_interface.py`**
```python
# /VIBE_FORGE_OS_v4.0/kernel/llm_interface.py
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
                raise ValueError(f"{self.adapter} API 키가 설정되지 않았습니다.")
            
            if self.adapter == "gemini":
                genai.configure(api_key=api_key)
                model_name = config.get("models", {}).get(self.adapter, "gemini-pro")
                self.model = genai.GenerativeModel(model_name)
            else:
                raise NotImplementedError(f"{self.adapter} 어댑터는 아직 지원되지 않습니다.")
            
            print(f"  -> '{self.adapter}' 어댑터가 성공적으로 활성화되었습니다.")
        except Exception as e:
            print(f"❌ [LLM Core] '{self.adapter}' 어댑터 초기화 실패: {e}")
            raise

    def get_completion(self, prompt: str, temperature: float = 0.5, max_tokens: int = 2000) -> str:
        last_exception = None
        for attempt in range(self.max_retries):
            try:
                if self.adapter == "gemini":
                    response = self.model.generate_content(prompt)
                    if response.text:
                        return response.text.strip()
                    else:
                        finish_reason = response.prompt_feedback.block_reason if response.prompt_feedback else 'unknown'
                        last_exception = Exception(f"응답이 비어있습니다. (Finish Reason: {finish_reason})")
            except Exception as e:
                last_exception = e
            
            print(f"  -> ⚠️ LLM 호출 시도 {attempt + 1}/{self.max_retries} 실패: {last_exception}")
            time.sleep(1)
            
        raise Exception(f"LLM 호출 최종 실패: {last_exception}") from last_exception
```

#### **FILE 8/11: `/VIBE_FORGE_OS_v4.0/weavers_loom/schema_library.py`**
```python
# /VIBE_FORGE_OS_v4.0/weavers_loom/schema_library.py

# VGP v3.1 '빛나는 렌즈'의 완전한 지식 기반
# 이 라이브러리는 시스템의 모든 인지 활동의 근간을 이룹니다.

SCHEMA_DEFINITIONS = {
    "CONTAINER": "[정의] 내/외부를 구분하는 위상적 경계. [주석] '이것은 어디에 속하는가?'",
    "PATH": "[정의] 시작점에서 목표점까지의 연속된 궤적. [주석] 과정, 로드맵, 스토리라인.",
    "CONTACT": "[정의] 두 개체 간의 접촉 또는 상호작용. [주석] 물리적/추상적 상호작용.",
    "LINK": "[정의] 두 노드를 잇는 논리적/인과적 연결. [주석] '왜 중요한가?', '무엇과 관련 있는가?'",
    "AXIS": "[정의] 측정과 위치를 위한 기준 축 또는 척도. [주석] 우선순위, 만족도 등 평가/측정.",
    "OBJECT": "[정의] 독립적으로 존재하는 구체적이거나 추상적인 실체. [주석] 시스템의 모든 '명사'.",
    "GROUND": "[정의] 인지의 대상(figure)이 되는 배경(ground) 또는 근거. [주석] '무엇을 근거로 판단했는가?'",
    "PART-WHOLE": "[정의] 전체와 부분을 구성하는 관계. [주석] 시스템 아키텍처, 조직 구조.",
    "FORCE_DYNAMICS": "[정의] 두 개체의 힘 상호작용과 그 결과. [주석] 갈등, 협력, 경쟁.",
    "BARRIER": "[정의] PATH의 진행을 막는 장애물. [주석] 문제점, 한계, 도전, 리스크.",
    "EQUILIBRIUM": "[정의] 여러 힘이 상쇄되어 안정 또는 정체된 상태. [주석] '현재 상태는 안정적인가?'",
    "IDENTITY": "[정의] 한 개체를 다른 것과 구별하는 고유한 속성의 집합. [주석] '이것의 본질은 무엇인가?'",
    "VALUATION": "[정의] 특정 대상에 대해 긍정-부정의 가치를 부여하는 행위. [주석] '좋다/나쁘다' 등 주관적 평가.",
    "EXPECTATION": "[정의] 특정 조건 하에서 미래 사건에 대한 예측. [주석] 기대, 가설. '만약 ~라면, ~될 것이다.'",
    "AGENCY": "[정의] 스스로 행동을 시작하고 통제할 수 있는 능력에 대한 인식. [주석] '누가 할 수 있는가?', 주도권.",
    "COMPETENCE": "[정의] 특정 과업을 성공적으로 수행할 능력에 대한 평가. [주석] '할 수 있는 실제 능력'.",
    "SECURITY": "[정의] 위협으로부터 보호받고 있다는 안정감에 대한 인식. [주석] 물리적/심리적 안전.",
    "CONNECTION": "[정의] 지각 있는 존재 간의 사회-정서적 유대. [주석] 신뢰, 유대감, 소속감.",
    "RECIPROCITY": "[정의] 주고받는 상호작용의 공정성에 대한 인식. [주석] '이것은 공정한가?'",
    "STANDARD": "[정의] 성과나 행동을 평가하는 내적/외적 기준. [주석] 품질, 규칙, 기대치.",
    "REGULATION": "[정의] 충동이나 감정, 시스템을 조절하는 내적 통제. [주석] 자기 통제, 리스크 관리.",
    "ROLE": "[정의] 특정 사회적 맥락에서 개인에게 기대되는 행동 규범. [주석] '여기서 나는 무엇을 해야 하는가?'",
    "EVENT_SCRIPT": "[정의] 특정 상황에서 일어나는 전형적인 사건의 순서. [주석] 시나리오, 프로토콜.",
    "HIERARCHY": "[정의] 사회 시스템 내에서의 권력, 지위, 우선순위의 구조. [주석] 조직도, 의사결정 구조.",
    "TRANSFORMATION": "[정의] 한 상태에서 다른 상태로의 근본적인 변화. [주석] 본질 자체가 변하는 것.",
    "COMMUNICATION_ACT": "[정의] 의도를 가진 주체 간의 의사소통 행위. [주석] '누가, 누구에게, 무엇을, 왜, 어떻게 말했는가?'",
    "BELIEF": "[정의] 어떤 주체(holder)가 참이라고 여기는 명제(proposition). [주석] 사실이 아닌 '믿음'.",
}

def get_schema_definitions_for_prompt() -> str:
    """프롬프트에 주입하기 좋은 형태로 스키마 정의를 포맷합니다."""
    return "\n".join([f"- ({name}: {desc})" for name, desc in SCHEMA_DEFINITIONS.items()])
```

#### **FILE 9/11: `/VIBE_FORGE_OS_v4.0/weavers_loom/decomposer.py`**
```python
# /VIBE_FORGE_OS_v4.0/weavers_loom/decomposer.py
from kernel.llm_interface import LLMInterface
from .schema_library import get_schema_definitions_for_prompt

class Decomposer:
    def __init__(self, llm_interface: LLMInterface, prompt_template: str):
        self.llm = llm_interface
        # 프롬프트에 스키마 정의를 주입
        self.prompt_template = prompt_template.format(
            schema_definitions=get_schema_definitions_for_prompt()
        )
        print("🏛️  [Decomposer] 구조 분석기가 '빛나는 렌즈'를 장착했습니다.")

    def structure(self, user_input: str) -> str:
        prompt = self.prompt_template.format(user_input=user_input, schema_definitions="") # 이미 주입됨
        try:
            return self.llm.get_completion(prompt, temperature=0.2, max_tokens=200)
        except Exception as e:
            print(f"❌ Decomposer 실패: {e}")
            return "STRUCTURE_FAILED"
```

#### **FILE 10/11: `/VIBE_FORGE_OS_v4.0/weavers_loom/prototyper.py`**
```python
# /VIBE_FORGE_OS_v4.0/weavers_loom/prototyper.py
from kernel.llm_interface import LLMInterface

class Prototyper:
    def __init__(self, llm_interface: LLMInterface, prompt_template: str):
        self.llm = llm_interface
        self.prompt_template = prompt_template
        print("🛠️  [Prototyper] 마스터 프로토타이퍼가 준비되었습니다.")

    def create_prototype(self, ast: dict) -> str:
        prompt = self.prompt_template.format(ast_string=str(ast))
        try:
            return self.llm.get_completion(prompt, temperature=0.6)
        except Exception as e:
            print(f"❌ Prototyper 실패: {e}")
            return "PROTOTYPE_CREATION_FAILED"
```

#### **FILE 11/11: `/VIBE_FORGE_OS_v4.0/weavers_loom/refinement_engine.py`**
```python
# /VIBE_FORGE_OS_v4.0/weavers_loom/refinement_engine.py
from kernel.llm_interface import LLMInterface

class RefinementEngine:
    def __init__(self, llm_interface: LLMInterface, prompt_template: str):
        self.llm = llm_interface
        self.prompt_template = prompt_template
        print("✍️  [Refinement Engine] 개선 전문가가 대기 중입니다.")

    def refine_prototype(self, previous_prototype: str, user_feedback: str) -> str:
        prompt = self.prompt_template.format(
            previous_prototype=previous_prototype,
            user_feedback=user_feedback
        )
        try:
            return self.llm.get_completion(prompt, temperature=0.7)
        except Exception as e:
            print(f"❌ Refinement 실패: {e}")
            return "REFINEMENT_FAILED"
```

#### **FILE 12/12: `/VIBE_FORGE_OS_v4.0/run.py`**
```python
# /VIBE_FORGE_OS_v4.0/run.py
import sys, os, json, yaml

sys.path.insert(0, os.path.abspath(os.path.dirname(__file__)))

from kernel.llm_interface import LLMInterface
from kernel.ccl_parser import CCLParser
from weavers_loom.decomposer import Decomposer
from weavers_loom.prototyper import Prototyper
from weavers_loom.refinement_engine import RefinementEngine

__version__ = "4.0.0"

def load_prompts():
    with open('prompts.yml', 'r', encoding='utf-8') as f:
        return yaml.safe_load(f)

def main():
    print(f"Vibe-Forge OS v{__version__} - The Weaver's Loom 부팅 중...")
    
    with open('config.json', 'r', encoding='utf-8') as f: config = json.load(f)
    prompts = load_prompts()
    
    # 모듈 초기화
    llm = LLMInterface(config)
    parser = CCLParser()
    decomposer = Decomposer(llm, prompts['decomposer']['v1']['system_prompt'])
    prototyper = Prototyper(llm, prompts['prototyper']['v1']['system_prompt'])
    refinement_engine = RefinementEngine(llm, prompts['refinement_engine']['v1']['system_prompt'])

    print("\n======================================================")
    print("공생적 직조가(v3.1)가 활성화되었습니다.")
    print("당신의 Vibe를 입력하여 첫 번째 실을 건네주세요. (종료: 'exit')")
    print("======================================================")

    # 공생적 반복 루프 시작
    current_prototype = None
    
    # 1. STRUCTURE
    user_vibe = input("\n당신의 Vibe 💬: ")
    if user_vibe.lower() in ['exit', 'quit']:
        print("시스템을 종료합니다.")
        return

    cclc_code = decomposer.structure(user_vibe)
    ast = parser.parse(cclc_code)
    print(f"\n[구조화 완료] AST: {ast}")
    
    # 2. PROTOTYPE
    print("\n...[Prototyper]가 첫 번째 프로토타입을 제작 중입니다...")
    current_prototype = prototyper.create_prototype(ast)
    print("\n--- [최초 프로토타입] ---\n" + current_prototype)

    # 3. REFINE
    while True:
        user_feedback = input("\n이 프로토타입에 대한 당신의 피드백은 무엇입니까? (완료 시 '완성', 종료 시 'exit')\n💬: ")
        if user_feedback.lower() == '완성':
            print("\n🎉 창조가 완료되었습니다! 최종 결과물:")
            print("--- [최종 결과물] ---\n" + current_prototype)
            break
        if user_feedback.lower() in ['exit', 'quit']:
            print("작업을 중단하고 시스템을 종료합니다.")
            break
            
        print("\n...[Refinement Engine]이 당신의 피드백을 반영하여 프로토타입을 개선 중입니다...")
        current_prototype = refinement_engine.refine_prototype(current_prototype, user_feedback)
        print("\n--- [개선된 프로토타입] ---\n" + current_prototype)

if __name__ == "__main__":
    main()
```