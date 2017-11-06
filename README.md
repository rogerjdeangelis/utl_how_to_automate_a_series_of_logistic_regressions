# utl_how_to_automate_a_series_of_logistic_regressions
How to use macro to create a series of logistic regressions

    ```  How to use macro to create a series of logistic regressions                                                                                                  ```
    ```                                                                                                                                                               ```
    ```    How to automate three logistic regressions                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```    INPUT                                                                                                                                                      ```
    ```    =====                                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```     WORK.HAVE total obs=4                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```      DEPENDENT_                                                                                                                                               ```
    ```          VAR       _123    _234    _341                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```           0         23      12       0                                                                                                                        ```
    ```           1         45      48       9                                                                                                                        ```
    ```           1          0      23       6                                                                                                                        ```
    ```           0         89      12      34                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```     WORKING CODE                                                                                                                                              ```
    ```     ============                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```      MAINLINE                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```          array vars[4] dependent_var _:;                                                                                                                      ```
    ```          do i=2 to dim(vars);                                                                                                                                 ```
    ```             call symputx('var',vname(vars[i]));                                                                                                               ```
    ```                                                                                                                                                               ```
    ```      SUBROUTINE (DODUBL)                                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```          proc logistic data=example;                                                                                                                          ```
    ```           model dependent_var = &var;                                                                                                                         ```
    ```          run;                                                                                                                                                 ```
    ```          %let ErrorText= &syserrortext;                                                                                                                       ```
    ```          %let ErrorCode= &syserr;                                                                                                                             ```
    ```                                                                                                                                                               ```
    ```      MAINLINE                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```          if  rc ne 0                                                                                                                                          ```
    ```              or ErrorCode ne "0" Then do;                                                                                                                     ```
    ```              Status        =  "Failed      ";                                                                                                                 ```
    ```          end;                                                                                                                                                 ```
    ```          else do;                                                                                                                                             ```
    ```             Status="Completed";                                                                                                                               ```
    ```          end;                                                                                                                                                 ```
    ```          output;                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```      OUTPUT                                                                                                                                                   ```
    ```      ======                                                                                                                                                   ```
    ```       WORK.LOG total obs=3                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```        STATUS      ERRORTEXT    ERRORCODE    VAR                                                                                                              ```
    ```                                                                                                                                                               ```
    ```       Completed                     0        _123                                                                                                             ```
    ```       Completed                     0        _234                                                                                                             ```
    ```       Completed                     0        _341                                                                                                             ```
    ```                                                                                                                                                               ```
    ```       NOTE: PROC LOGISTIC is modeling the probability that DEPENDENT_VAR=0. One way to change this to                                                         ```
    ```             model the probability that DEPENDENT_VAR=1 is to specify the response variable option                                                             ```
    ```             EVENT='1'.                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```       NOTE: PROC LOGISTIC is modeling the probability that DEPENDENT_VAR=0. One way to change this to                                                         ```
    ```             model the probability that DEPENDENT_VAR=1 is to specify the response variable option                                                             ```
    ```             EVENT='1'.                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```       NOTE: PROC LOGISTIC is modeling the probability that DEPENDENT_VAR=0. One way to change this to                                                         ```
    ```             model the probability that DEPENDENT_VAR=1 is to specify the response variable option                                                             ```
    ```             EVENT='1'.                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  https://goo.gl/5icoQh                                                                                                                                        ```
    ```  https://communities.sas.com/t5/Base-SAS-Programming/How-to-use-macro-to-create-a-series-of-logistic-regressions/m-p/410927                                   ```
    ```                                                                                                                                                               ```
    ```  *                _               _       _                                                                                                                   ```
    ```   _ __ ___   __ _| | _____     __| | __ _| |_ __ _                                                                                                            ```
    ```  | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |                                                                                                           ```
    ```  | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |                                                                                                           ```
    ```  |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  data have;                                                                                                                                                   ```
    ```    input dependent_var _123 _234 _341;                                                                                                                        ```
    ```  cards4;                                                                                                                                                      ```
    ```  0 23 12 0                                                                                                                                                    ```
    ```  1 45 48 9                                                                                                                                                    ```
    ```  1 0 23 6                                                                                                                                                     ```
    ```  0 89 15 34                                                                                                                                                   ```
    ```  0 13 15 7                                                                                                                                                    ```
    ```  1 41 48 4                                                                                                                                                    ```
    ```  1 1 25 3                                                                                                                                                     ```
    ```  1 19 11 39                                                                                                                                                   ```
    ```  ;;;;                                                                                                                                                         ```
    ```  run;                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```  %symdel var / nowarn;                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  data log (keep=var status errortext errorcode);                                                                                                              ```
    ```                                                                                                                                                               ```
    ```     retain                                                                                                                                                    ```
    ```       status errortext errorcode ;                                                                                                                            ```
    ```     length                                                                                                                                                    ```
    ```        ErrorText                                                                                                                                              ```
    ```        ErrorCode  $96;                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```     set have;                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```     array vars[4] dependent_var _:;                                                                                                                           ```
    ```     do i=2 to dim(vars);                                                                                                                                      ```
    ```       var=vname(vars[i]);                                                                                                                                     ```
    ```       call symputx('var',var);                                                                                                                                ```
    ```                                                                                                                                                               ```
    ```          rc=dosubl('                                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```             %let ErrorText= ;                                                                                                                                 ```
    ```             %let ErrorCode= ;                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```             proc logistic data=have;                                                                                                                          ```
    ```              model dependent_var = &var;                                                                                                                      ```
    ```             run;                                                                                                                                              ```
    ```             %let ErrorText= &syserrortext;                                                                                                                    ```
    ```             %let ErrorCode= &syserr;                                                                                                                          ```
    ```          ');                                                                                                                                                  ```
    ```                                                                                                                                                               ```
    ```       ErrorText  =  symget('ErrorText');                                                                                                                      ```
    ```       ErrorCode  =  symget('ErrorCode');                                                                                                                      ```
    ```                                                                                                                                                               ```
    ```       if  rc ne 0                                                                                                                                             ```
    ```           or ErrorCode ne "0" Then do;                                                                                                                        ```
    ```           Status        =  "Failed      ";                                                                                                                    ```
    ```       end;                                                                                                                                                    ```
    ```       else do;                                                                                                                                                ```
    ```          Status="Completed";                                                                                                                                  ```
    ```       end;                                                                                                                                                    ```
    ```       output;                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```     end;                                                                                                                                                      ```
    ```     stop;                                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```

