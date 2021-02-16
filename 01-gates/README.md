# Labs 01-Gates
## Part One: Link to the repository
Link:
| **c** | **b** |**a** | **f(c,b,a)** |
| :-: | :-: | :-: | :-: |
| 0 | 0 | 0 | 1 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 0 |

Part Three: Verification of De Morgan's laws
Link to EDA
code:
```vhdl
architecture dataflow of gates is
begin
    f_o      <= (((not b_i) and a_i) or ((not c_i) and (not b_i)));
    fnand_o  <= ((a_i nand (not b_i)) nand ((not b_i) nand (not c_i)));
    fnor_o   <= ((a_i nor (not c_i)) nor b_i);
end architecture dataflow;
```
screen: 
## Part Three: Verification of Distributive laws
### Link to EDA:
```vhdl
architecture dataflow of gates is
begin
    f1_o  <= (x_i and (not x_i));
    f2_o  <= (x_i or (not x_i));
    f3_o  <= (x_i or  x_i  or  x_i  or  x_i);
    f4_o  <= (x_i and  x_i  and  x_i  and x_i);
    f11_o <= ((x_i and  y_i) or (x_i and  z_i));
    f12_o <= (x_i and (y_i or z_i));
    f21_o <= (((x_i or y_i) and (x_i or z_i)));
    f22_o <= (x_i or (y_i and  z_i));
end architecture dataflow;
```
screen:
