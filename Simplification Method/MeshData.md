
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
```
vertex1 = {x1, y1, z1}
vertex2 = {x2, y2, z2}
vertex3 = {x3, y3, z3}

face1 = {vertex1, vertex2, vertex3}
```
# Half Edge
+ 정의
  + 메시의 각 edge를 두 개의 반쪽(half-edge)로 나누어 표현
  + 각 hale-edge는 방향(orientation)을 가지며 다음과 같은 정보를 저장함
    ```
    Origin Vertex: half-edge의 시작 정점.
    Twin Half-Edge: 같은 모서리를 공유하는, 반대 방향의 half-edge.
    Incident Face: half-edge가 속한 면(대부분 왼쪽 면으로 정의).
    Next Half-Edge: 해당 면의 경계를 따라 다음에 오는 half-edge.
    (선택적) Prev Half-Edge: 이전 half-edge (구현에 따라 포함될 수 있음).

    struct Vertex;
    struct Face;
    struct HalfEdge;

    // 정점(Vertex) 구조체: 3차원 좌표와 하나의 반모서리 포인터를 포함합니다.
    struct Vertex {
        float x, y, z;            // 정점의 좌표
        HalfEdge* outgoing;       // 이 정점에서 나가는 반모서리 (임의의 하나)
    };
    
    // 면(Face) 구조체: 면에 인접한 반모서리를 가리킵니다.
    struct Face {
        HalfEdge* halfEdge;       // 이 면을 구성하는 반모서리 중 하나
    };
    
    // Half-Edge 구조체: 메시의 연결 관계를 정의합니다.
    struct HalfEdge {
        Vertex* origin;           // 시작 정점
        HalfEdge* twin;           // 반대 방향의 twin 반모서리 (인접 면에 속함)
        Face* incidentFace;       // 이 반모서리가 속한 면
        HalfEdge* next;           // 면의 경계상 다음 반모서리 (반시계 방향)
    };
    
    /// Mesh 구조체: 메시의 모든 구성 요소를 저장합니다.
    struct Mesh {
        std::vector<Vertex> vertices;
        std::vector<HalfEdge> halfEdges;
        std::vector<Face> faces;
    };```

+ 장점
  + Vertex, Edge, Face를 빠르게 탐색 가능
    + 한 정점에 인접한 모든 면이나, 한 면의 경계에 있는 정점을 쉽게 접근 가능
  + 동적으로 메시 수정 가능
    + 메시의 추가, 삭제, 분할, 병합등의 연산에 효율적
    + 국소적인 변경이 전체 구조에 큰 영향을 주지 않음
   
+ 단점
  + 오버헤드 증가
  + non-manifold, non-orientable 모델에서는 사용하기 힘듬            
