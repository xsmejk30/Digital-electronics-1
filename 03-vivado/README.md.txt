# Part One: Link to the reposiory
https://github.com/Simon-Roubal/Digital-electronics-1/tree/main/Labs/03-vivado
# Part Two: Table with connection of 16 slide switches and 16 LEDs on Nexys A7 board
| **Part** | **Pin** | **Active** |
| :-: | :-: | :-: |
| LED0 | H17 | High |
| LED1 | K15 | High |
| LED2 | J13 | High |
| LED3 | N14 | High |
| LED4 | R18 | High |
| LED5 | V17 | High |
| LED6 | U17 | High |
| LED7 | U16 | High |
| LED8 | V16 | High |
| LED9 | T15 | High |
| LED10 | U14 | High |
| LED11 | T16 | High |
| LED12 | V15 | High |
| LED13 | V14 | High |
| LED14 | V12 | High |
| LED15 | V11 | High |
| SW0 | J15 | - |
| SW1 | L16 | - |
| SW2 | M13 | - |
| SW3 | R15 | - |
| SW4 | R17 | - |
| SW5 | T18 | - |
| SW6 | U18 | - |
| SW7 | R13 | - |
| SW8 | T8 | - |
| SW9 | U8 | - |
| SW10 | R16 | - |
| SW11 | T13 | - |
| SW12 | H6 | - |
| SW13 | U12 | - |
| SW14 | U11 | - |
| SW15 | V10 | - |

# Part Three: Two-bit wide 4-to-1 multiplexer

## Listing of VHDL architecture

```vhdl
library ieee;
use ieee.std_logic_1164.all;

entity mux_2bit_4to1 is
    port(
        a_i           : in  std_logic_vector(2 - 1 downto 0);
        b_i           : in  std_logic_vector(2 - 1 downto 0);
        c_i           : in  std_logic_vector(2 - 1 downto 0);
        d_i           : in  std_logic_vector(2 - 1 downto 0);
        
        sel_i         : in  std_logic_vector(2 - 1 downto 0);

        f_o    :out std_logic_vector(2 - 1 downto 0)
    );
end entity mux_2bit_4to1;

architecture Behavioral of mux_2bit_4to1 is
begin
    f_o     <=  a_i when (sel_i="00")else
                b_i when (sel_i="01")else
                c_i when (sel_i="10")else
                d_i;

end architecture Behavioral;
```
## Listing of VHDL stimulus process from testbench file

```vhdl
library ieee;
use ieee.std_logic_1164.all;

entity tb_mux_2bit_4to1 is

end entity tb_mux_2bit_4to1;

architecture testbench of tb_mux_2bit_4to1 is

    -- Local signals
    signal s_a       : std_logic_vector(2 - 1 downto 0);
    signal s_b       : std_logic_vector(2 - 1 downto 0);
    signal s_c       : std_logic_vector(2 - 1 downto 0);
    signal s_d       : std_logic_vector(2 - 1 downto 0);
    signal s_sel     : std_logic_vector(2 - 1 downto 0);
    signal s_f       : std_logic_vector(2 - 1 downto 0);

begin
    uut_mux_2bit_4to1 : entity work.mux_2bit_4to1
        port map(
            a_i           => s_a,
            b_i           => s_b,
            c_i           => s_c,
            d_i           => s_d,
            sel_i         => s_sel,
            
            f_o           => s_f
        );

    p_stimulus : process
    begin
        -- Report a note at the begining of stimulus process
        report "Stimulus process started" severity note;

        s_d <= "00";s_c <= "00";s_b <= "00"; s_a <= "00";
        s_sel <= "00";  wait for 100 ns;
        
        s_d <= "10";s_c <= "01";s_b <= "01"; s_a <= "00";
        s_sel <= "00";  wait for 100 ns;
        
        s_d <= "10";s_c <= "01";s_b <= "01"; s_a <= "11";
        s_sel <= "00";  wait for 100 ns;
        
        s_d <= "10";s_c <= "01";s_b <= "01"; s_a <= "00";
        s_sel <= "01";  wait for 100 ns;
        
        s_d <= "10";s_c <= "01";s_b <= "11"; s_a <= "00";
        s_sel <= "01";  wait for 100 ns;
        
        s_sel <= "10";  wait for 100 ns;
        
        s_sel <= "11";  wait for 100 ns;

        -- Report a note at the end of stimulus process
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;

end architecture testbench;
```