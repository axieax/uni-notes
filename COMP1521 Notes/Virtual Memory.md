# Virtual Memory

All segments of address space (page) same size P

Page i holds address i*P .. (i + 1) * P

Translation of addresses can be implemented with an array - where each process has an array called the page table

Each array element contains the physical address in RAM of that page

For virtual address V, page_table[V / P] contains physical address of page

Address will be at offset V % P in both pages

So Physical address for V is page_table[V / P] + V % P

Make sure page number (V / P) is valid (less than page table size)

Address mapping if P == 2^n:

Page # gets mapped to a frame #, with same offset (bottom N bits)

Pages/frames are typically 4..256 KB in size, and each frame can hold one page of process adress space

Page fault - access to a page which is not loaded in RAM

Check for free fame - if no available, either suspend the requesting process until a page is freed, or replace one of the currently loaded/used pages (LRU - based on last access time)







