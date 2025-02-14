
# Mesh file format

### OBJ (Wavefront OBJ)
+ 특징:
  + 텍스트 기반의 단순한 포맷
  + 정점, 텍스처 좌표, 법선, 면 정보를 저장
  + 재질 파일(.mtl)과 연계하여 재질 정보를 제공

### STL (Stereolithography)
+ 특징:
  + 주로 삼각형 메시로 구성
  + 텍스트 및 바이너리 형식 모두 지원
  + 색상, 텍스처 등의 추가 정보 없이 기하학 정보만 저장
### PLY (Polygon File Format or Stanford Triangle Format)
+ 특징:
  + 텍스트와 바이너리 형식 모두 지원
  + 정점, 면 외에도 각종 속성(예: 색상, 법선, 텍스처 좌표) 저장 가능

### OFF (Object File Format)
+ 특징:
  + 정점과 면 정보를 간결하게 표현
  + 주로 학술 및 연구 목적에서 사용

# Triangle Mesh
+ 정점(Vertex):
  + 삼각형의 각 꼭짓점을 정의하는 3차원 좌표 정보 (예: 𝑥,𝑦,𝑧)를 포함합니다.

+ 면(Face):
  + 세 개의 정점으로 구성된 삼각형으로, 모델의 표면을 구성합니다.

+ 모서리(Edge) (선택적):
  + 인접한 정점을 연결하는 선분으로, 일부 알고리즘에서만 명시적으로 사용됩니다.
'''
vertex1 = {x1, y1, z1}
vertex2 = {x2, y2, z2}
vertex3 = {x3, y3, z3}

face1 = {vertex1, vertex2, vertex3}
'''
