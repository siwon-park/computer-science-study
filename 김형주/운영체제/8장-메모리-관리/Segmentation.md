### Segmentation Architecture

- Logical address는 다음의 두 가지로 구성 <segment-number, offset>
- segment table
  - each table entry has
    - base-starting physical address of the segment
    - limit-length of the segment

- Segment-table base register
  - 물리적 메모리에서의 segment table의 위치

- Segment-table length register
  - 프로그램이 사용하는 segment의 수


### Segmentation Hardware

![img](./Segmentation Hardware.png)

### Example of Segmetation

![img](./Example of Segmetation.png)

### Sharing of Segments

![img](./Sharing of Segments.png)

### Segmentation with Paging

- pure segmentation과의 차이점
  - segment-table entry가 segment의 base address를 가지고 있는 것이 아니라 segment를 구성하는 page table의 base address를 가지고 있음