# utl-little-known-properties-of-macro-sysindex-mlogicnest-mprintnest
Little known properties of macro sysindex mlogicnest mprintnest
    %let pgm=utl-little-known-properties-of-macro-sysindex-mlogicnest-mprintnest;

    %stop_submission;

    Thanks for highlighting MLOGICNEST

    Little known properties of macro sysindex mlogicnest mprintnest


      CONTENTS

          1 sysindex print title only on first macro invocation
            This can be quite usefull to change the action on susequent macro calls

          2 mlogicnest display the nesting of macros
            by Ksharp profile
            https://communities.sas.com/t5/user/viewprofilepage/user-id/18408
    github              
    https://tinyurl.com/3y8863sd                                                                                    
    https://github.com/rogerjdeangelis/utl-little-known-properties-of-macro-sysindex-mlogicnest-mprintnest/tree/main
    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                 _           _                                                                                          */
    /*   ___ _   _ ___(_)_ __   __| | _____  __                                                                               */
    /*  / __| | | / __| | `_ \ / _` |/ _ \ \/ /                                                                               */
    /*  \__ \ |_| \__ \ | | | | (_| |  __/>  <                                                                                */
    /*  |___/\__, |___/_|_| |_|\__,_|\___/_/\_\                                                                               */
    /*       |___/                                                                                                            */
    /*                                                                                                                        */
    /*------------------------------------------------------------------------------------------------------------------------*/
    /*                                   |                                                |                                   */
    /*                    INPUT          |                           PROCESS              |            OUTPUT                 */
    /*                    =====          |                           =======              |            ======                 */
    /*                                   |                                                |                                   */
    /*                                   |                                                |                                   */
    /*  CLASS                            | I want the title to appear only on the first   | Title only appears on first call  */
    /*                                   | macro invocation of proc print;                |                                   */
    /*   NAME    SEX AGE  HEIGHT  WEIGHT |                                                | SUBSEQUENT PUPILS IN MY MATH      */
    /*                                   | Each time a macro is called the automatic      |                                   */
    /*  Alfred    M   14   69.0    112.5 | macro variable sysindex is increamented        |  NAME   SEX AGE HEIGHT WEIGHT     */
    /*  Alice     F   13   56.5     84.0 |                                                |                                   */
    /*  Barbara   F   13   65.3     98.0 | * YOU NEED THIS MACRO;                         | Alfred   M   14   69    112.5     */
    /*                                   | * IF YOU RERUN;                                |                                   */
    /*                                   | proc catalog cat=work.sasmacr et=macro;        |                                   */
    /*  data class;                      |    delete listob ;                             |                                   */
    /*    set sashelp.class(obs=3);      | run;quit;                                      |  NAME   SEX AGE HEIGHT WEIGHT     */
    /*  run;quit;                        |                                                |                                   */
    /*                                   | %macro listob(obs);                            | Alfred   M   14  69.0   112.5     */
    /*                                   |                                                | Alice    F   13  56.5    84.0     */
    /*                                   |    %put &=sysindex &=savinx;                   |                                   */
    /*                                   |                                                |                                   */
    /*                                   |   %if %eval((&sysindex-&savinx)> 1) %then %do; |                                   */
    /*                                   |     title;                                     |  NAME   SEX AGE HEIGHT WEIGHT     */
    /*                                   |     footnote;                                  |                                   */
    /*                                   |   %end;                                        | Alfred   M   14  69.0   112.5     */
    /*                                   |                                                | Alice    F   13  56.5    84.0     */
    /*                                   |   proc print data=sashelp.class(obs=&obs);     | Barbara  F   13  65.3    98.0     */
    /*                                   |   run;quit;                                    |                                   */
    /*                                   |                                                |                                   */
    /*                                   | %mend listob;                                  |                                   */
    /*                                   |                                                |                                   */
    /*                                   |                                                |                                   */
    /*                                   | title 'SUBSEQUENT PUPILS IN MY MATH CLASS';    |                                   */
    /*                                   | run;quit;                                      |                                   */
    /*                                   |                                                |                                   */
    /*                                   | options formdlim=' '; * output on one page;    |                                   */
    /*                                   |                                                |                                   */
    /*                                   | * GET CURRENT VALUE OF SYSINDEX;               |                                   */
    /*                                   | %let savinx=&sysindex;                         |                                   */
    /*                                   |                                                |                                   */
    /*                                   | * title will appearonly for this invocation;   |                                   */
    /*                                   | %listob(1);                                    |                                   */
    /*                                   | %listob(2);                                    |                                   */
    /*                                   | %listob(3);                                    |                                   */
    /*                                   |                                                |                                   */
    /*------------------------------------------------------------------------------------------------------------------------*/
    /*            _             _                      _                                                                      */
    /*  _ __ ___ | | ___   __ _(_) ___ _ __   ___  ___| |_                                                                    */
    /* | `_ ` _ \| |/ _ \ / _` | |/ __| `_ \ / _ \/ __| __|                                                                   */
    /* | | | | | | | (_) | (_| | | (__| | | |  __/\__ \ |_                                                                    */
    /* |_| |_| |_|_|\___/ \__, |_|\___|_| |_|\___||___/\__|                                                                   */
    /*                   |___/                                                                                                */
    /*                                                                                                                        */
    /*------------------------------------------------------------------------------------------------------------------------*/
    /*                                  |                                                |                                    */
    /*  INTERNAL INPUT IN MACRO         | options mprint mprintnest mlogic mlogicnest;   | SAS LOG (EDITED OUT BLANK LINES)   */
    /*                                  |                                                |                                    */
    /*                                  | %macro a;                                      | CHILD B MACRO CALLED               */
    /*                                  |   data _null_;                                 |                                    */
    /*                                  |     put 'hello A';                             | 180  %b                            */
    /*                                  |   run;                                         |                                    */
    /*                                  | %mend;                                         | MLOGIC(B):  Beginning execution.   */
    /*                                  |                                                |                                    */
    /*                                  | %macro b;                                      | MLOGIC(B.A):  Beginning execution. */
    /*                                  |                                                |                                    */
    /*                                  |   %a                                           | MPRINT(B.A):   data _null_;        */
    /*                                  |                                                | MPRINT(B.A):   put 'hello A';      */
    /*                                  |   data _null_;                                 | MPRINT(B.A):   run;                */
    /*                                  |     put 'hello B';                             |                                    */
    /*                                  |   run;                                         | hello A                            */
    /*                                  |                                                |                                    */
    /*                                  | %mend;                                         | MLOGIC(B.A):  Ending execution.    */
    /*                                  |                                                |                                    */
    /*                                  |                                                | CONTINING B EXECUTION (RJD added)  */
    /*                                  |                                                |                                    */
    /*                                  |                                                | MPRINT(B):   data _null_;          */
    /*                                  |                                                | MPRINT(B):   put 'hello B';        */
    /*                                  |                                                |                                    */
    /*                                  |                                                | MPRINT(B):   run;                  */
    /*                                  |                                                |                                    */
    /*                                  |                                                | hello B                            */
    /*                                  |                                                |                                    */
    /*                                  |                                                | MLOGIC(B):  Ending execution.      */
    /*                                  |                                                |                                    */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
