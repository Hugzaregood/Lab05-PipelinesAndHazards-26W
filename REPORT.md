## Name: Nicholas Castellanos
## Email: ncast094@ucr.edu

## Section 1

A 15-cycle trace of the piplined CPU was tested while running the provided test program

| PC | Opcode | src1_addr | src1_out   | src2_addr | src_out    |dst_addr | dst_data   |
|---:|-------:|----------:|-----------:|----------:|-----------:|--------:|-----------:|
| 0  | 0x23   | 0         | 0x00000000 | 2         | 0x00000000 | 0       | 0x00000000 |
| 4  | 0x23   | 0         | 0x00000000 | 2         | 0x00000000 | 0       | 0x00000000 |
| 8  | 0x00   | 2         | 0x00000000 | 2         | 0x00000000 | 0       | 0x00000056 |
| 12 | 0x2B   | 0         | 0x00000000 | 3         | 0x00000000 | 2       | 0x00000056 |
| 16 | 0x00   | 3         | 0x00000000 | 2         | 0x00000056 | 2       | 0x00000056 |
| 20 | 0x08   | 3         | 0x00000000 | 5         | 0x00000000 | 3       | 0x00000000 |
| 24 | 0x00   | 5         | 0x00000000 | 3         | 0x00000000 | 3       | 0x00000084 |
| 28 | 0x00   | 6         | 0x00000000 | 2         | 0x00000056 | 4       | 0xFFFFFFAA |
| 32 | 0x00   | 6         | 0x00000000 | 2         | 0x00000056 | 5       | 0x0000000C |
| 36 | 0x00   | 5         | 0x0000000C | 4         | 0xFFFFFFAA | 6       | 0x00000000 |
| 40 | 0x04   | 5         | 0x0000000C | 0         | 0x00000000 | 7       | 0x00000056 |
| 44 | 0x23   | 0         | 0x00000000 | 8         | 0x00000000 | 8       | 0xFFFFFFA9 |
| 48 | 0x00   | 0         | 0x00000000 | 0         | 0x00000000 | 6       | 0x00000000 |
| 52 | 0x00   | 0         | 0x00000000 | 0         | 0x00000000 | 31      | 0x0000000C |
| 56 | 0x00   | 0         | 0x00000000 | 0         | 0x00000000 | 8       | 0x00000000 |

Opcode meanings:
  - 0x23 = `lw`
  - 0x2B = `sw`
  - 0x08 = `addi`
  - 0x04 = `beq`
  - 0x00 = `R-type`

## Section 2

A data hazard occurs between: 
`lw  $v0, 31($zero)` and 
`add $v1, $v0, $v0`.
The add reads `$v0` before the load writes to the new value causing the stale data to be used

A control hazard occurs when:
`beq $a2, $zero, -8`.
This allows incorrect instructions to enter the pipeline when the branch decision is resolved after the next instruction is fetched

## Section 3

`sll $zero, $zero, 0`
For this instruction it does nothing but only creates a single one-cycle delay. This would allow the load to complete before the add reads the 
register which prevents the data hazard
