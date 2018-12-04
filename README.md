# utl-using-infile-and-input-to-split-strings
Using infile and input to split strings.

    Using infile and input to split strings

    This may work for very long strings for instance 1tb strings.
    I am using a short string here for demonstration purposes.

    github
    https://tinyurl.com/yb25yzrr
    https://github.com/rogerjdeangelis/utl-using-infile-and-input-to-split-strings

    Related to
    SAS Forum
    https://tinyurl.com/yanxnqpg
    https://communities.sas.com/t5/SAS-Programming/Splitting-a-macro-variable-into-smaller-macro-variables/m-p/516976


    INPUT
    =====

    * The classic editor handles lines up to 384 chars. The string below is on one lne.;
    %let m=MACRO + Intercept [0.1921215597] + CHAR6 [0.3071353419] + CHAR9 [0.4431909076] + CHAR11 [0.2608270872] + CHAR783 [0.3223002876] + CHAR913 [0.3977991533] + CHAR741 [0.9413739214] + WOE_CHARX3 [0.278206];

    PROCESS
    =======

    data _null_;
      file "d:/txt/have.txt" lrecl=400; * max lrecl >1TB?;
      put "&m";
    run;quit;

    data want;
      infile  "d:/txt/have.txt" lrecl=384 dlm=" ";
      input @'+' char : $16. @@;
      if index(char,'CHAR')>0;
    run;quit;


    OUTPUT
    ======

    Up to 40 obs from WANT total obs=7

    Obs    CHAR

     1     CHAR6
     2     CHAR9
     3     CHAR11
     4     CHAR783
     5     CHAR913
     6     CHAR741
     7     WOE_CHARX3

