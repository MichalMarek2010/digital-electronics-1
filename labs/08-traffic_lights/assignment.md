# Lab 8: YOUR_FIRSTNAME LASTNAME

### Traffic light controller

1. Figure of state diagram:

   ![your figure](images/state1.jpg)

2. Listing of VHDL code of the completed process `p_traffic_fsm`. Always use syntax highlighting, meaningful comments, and follow VHDL guidelines:

```vhdl
     p_traffic_fsm : process(clk)
    begin
        if rising_edge(clk) then
            if (reset = '1') then   -- Synchronous reset
                s_state <= STOP1;   -- Set initial state
                s_cnt   <= c_ZERO;  -- Clear delay counter

            elsif (s_en = '1') then
                -- Every 250 ms, CASE checks the value of the s_state 
                -- variable and changes to the next state according 
                -- to the delay value.
                case s_state is

                    -- If the current state is STOP1, then wait 1 sec
                    -- and move to the next GO_WAIT state.
                    when STOP1 =>
                        -- Count up to c_DELAY_1SEC
                        if (s_cnt < c_DELAY_1SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            -- Move to the next state
                            s_state <= WEST_GO;
                            -- Reset local counter value
                            s_cnt <= c_ZERO;
                        end if;

                    when WEST_GO =>
                        -- WRITE OTHER STATES HERE
                        if (s_cnt < c_DELAY_4SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            -- Move to the next state
                            s_state <= WEST_WAIT;
                            -- Reset local counter value
                            s_cnt <= c_ZERO;
                        end if;
    
                    when WEST_WAIT =>
                        -- WRITE OTHER STATES HERE
                        if (s_cnt < c_DELAY_2SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            -- Move to the next state
                            s_state <= STOP2;
                            -- Reset local counter value
                            s_cnt <= c_ZERO;
                        end if;
                        
                    when STOP2 =>
                        -- WRITE OTHER STATES HERE
                        if (s_cnt < c_DELAY_1SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            -- Move to the next state
                            s_state <= SOUTH_GO;
                            -- Reset local counter value
                            s_cnt <= c_ZERO;
                        end if;
                        
                      when SOUTH_GO =>
                        -- WRITE OTHER STATES HERE
                        if (s_cnt < c_DELAY_4SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            -- Move to the next state
                            s_state <= SOUTH_WAIT;
                            -- Reset local counter value
                            s_cnt <= c_ZERO;
                        end if;
                      
                       when SOUTH_WAIT =>
                        -- WRITE OTHER STATES HERE
                        if (s_cnt < c_DELAY_2SEC) then
                            s_cnt <= s_cnt + 1;
                        else
                            -- Move to the next state
                            s_state <= STOP1;
                            -- Reset local counter value
                            s_cnt <= c_ZERO;
                        end if;
                        
                        
                    -- It is a good programming practice to use the 
                    -- OTHERS clause, even if all CASE choices have 
                    -- been made.
                    when others =>
                        s_state <= STOP1;
                        s_cnt   <= c_ZERO;
                end case;
            end if; -- Synchronous reset
        end if; -- Rising edge
    end process p_traffic_fsm;
```

3. Screenshot with simulated time waveforms. The full functionality of the entity must be verified. Always display all inputs and outputs (display the inputs at the top of the image, the outputs below them) at the appropriate time scale!

   ![your figure](images/sim.png)

### Smart controller

| **Current state** | **Direction South** | **Direction West** | **Delay** | **CAR sensor WEST/SOUTH** |
| :-- | :-: | :-: | :-: | :-: |
| STOP1      | red    | red | 1 sec | =>WEST_GO |
| WEST_GO    | red    | green | 4 sec | 10 or 00=>WEST_GO else =>WEST_WAIT |
| WEST_WAIT  | red    | yellow | 2 sec | =>STOP2 |
| STOP2      | red    | red | 1 sec | =>SOUTH_GO |
| SOUTH_GO   | green  | red | 4 sec | 01 or 00 =>SOUTH_GO else =>SOUTH_WAIT |
| SOUTH_WAIT | yellow | red | 2 sec | STOP1 |

### State diagram

1. State table for smart controller using two sensors and two traffic lights in three colors.
 
   ![your figure](images/state2.jpg)
