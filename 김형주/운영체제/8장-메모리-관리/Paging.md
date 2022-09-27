### Paging Example

![img](./page Example.png)

### Address Translation Architecture

![img](./Address Translation Architecture.png)

### Implementation of Page Table

- Page table은 main memory에 상주
- Page-table base register가 page table을 가리킴
- Page-table length register가 테이블 크기를 보관
- 모든 메모리 접근 연산에는 2번의 memory access 필요
- page table 접근 1번, 실제 data/instruction 접근 1번
- 속도 향상을 위해
  - associative register혹은 translation look-aside buffer
  - 라 불리는 고속의 lookup hardware cache 사용


### Paging Hardware with TLB

![img](./Paging Hardware with TLB.png)

### Two-Level Page Table

- Address-Translation Scheme

  - CPU는 다음 두 가지로 구성된 virtual address를 사용
    - Page number
      - page table의 index로 사용
      - 해당 index에는 그 페이지의 물리적 메모리 상의 base address가 저장됨

    - Page offset
      - base address와 더해져서 physical address가 구해짐

- Two-Level Paging Example

  - 현대의 컴퓨터는 address space가 매우 큰 프로그램 지원
    - 32bit address 사용시: 4G의 주소 공간
      - 각 page size가 4K 시 1M개의 page table entry 필요
      - 그러나 대부분의 프로그램은 4G의 주소 공간 중 지극히 일부분만 사용하므로 page table 공간이 심하게 낭비됨


  -> page table 자체를 page로 구성

  -> 사용되지 않는 주소 공간에 대한 outer page table의 엔트리 값은 NULL (대응하는 inner page table이 없음)

### Multilevel Paging and Performance

- Address space가 더 커지면 다단계 페이지 테이블 필요
- 각 단계의 페이지 테이블이 메모리에 존재하므로 logical address의 physical address 변환에 더 많은 메모리 접근 필요
- 캐쉬 메모리를 통해 메모리 접근 시간을 줄일 수 있음
- 4단계 페이지 테이블을 사용하는 경우
  - 메모리 접근 시간이 100ns, 캐쉬 메모리 접근 시간이 20ns이고 캐쉬 적중률이 98%인 경우
    - effective memory access time = 0.98 * 120 + 0.02 * 520 = 128 ns
    - 결과적으로 메모리 접근 시간을 28%만 down 시킴


### Valid (v)/ Invalid (i) Bit in a Page Table

![img](./Valid,Invalid Bit in a page Table.png)

### Memory Protection

- Page table의 각 entry 마다 아래의 bit을 둔다
  - Protection bit
    - page에 대한 접근 권한

  - Valid-invalid bit
    - valid는 해당 주소의 frame에 그 프로세스를 구성하는 유효한 내용이 있음을 뜻함(접근 허용)
    - invalid는 해당 주소의 frame에 유효한 내용이 없음을 뜻함 (접근 불허)
    - 


### Inverted Page Table

- page table이 매우 큰 이유

  - 모든 프로세스 별로 그 logical address에 대응하는 모든 페이지에 대해 page table entry가 존재
  - 대응하는 page가 메모리에 있든 아니든 간에 page table에는 entry로 존재

- Inverted page table

  - Page frame  하나당 page table에 하나의 entry를 둔 것
  - 각 page table entry는 각각의 물리적 메모리의 page frame이 담고 있는 내용 표시
  - 단점
    - 테이블 전체를 탐색해야 함
  - 조치
    - associative register 사용

  - Inverted Page Table Architecture

  ![img](./Inverted Page Table Architecture.png)

### Shared Page

- Shared code
  - Re-entrant Code
  - read-only로 하여 프로세스 간에 하나의 코드만 메모리에 올림
  - Shared code는 모든 프로세스의 logical address space에서 동일한 위치에 있어야 함
- Private code and data
  - 각 프로세스들은 독자적으로 메모리에 올림
  - Private data는 logical address space의 아무 곳에 와도 무방

- Shared Pages Example

![img](./Shared Pages Example.png)