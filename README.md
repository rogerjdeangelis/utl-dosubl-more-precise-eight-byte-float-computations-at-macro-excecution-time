# utl-dosubl-more-precise-eight-byte-float-computations-at-macro-excecution-time
More precise computations at macro excecution time  
    More precise computations at macro excecution time                                                                      
                                                                                                                            
    Providing macros with better precision                                                                                  
                                                                                                                            
    I need to perform these calulations at macro execution time                                                             
                                                                                                                            
    data;                                                                                                                   
       s=constant("EULER")  + 2;                                                                                            
       d=constant("PI") - s;                                                                                                
       put d=;                                                                                                              
    run;quit;                                                                                                               
                                                                                                                            
    github                                                                                                                  
    http://tinyurl.com/yyaoqs9f                                                                                             
    https://github.com/rogerjdeangelis/utl-dosubl-more-precise-eight-byte-float-computations-at-macro-excecution-time       
                                                                                                                            
    Inspired by SAS Forum                                                                                                   
    http://tinyurl.com/y4jwum9t                                                                                             
    https://communities.sas.com/t5/SAS-Programming/Passing-as-variable-to-a-macro-the-result-of-another-macro/m-p/550143    
                                                                                                                            
    *_                   _                                                                                                  
    (_)_ __  _ __  _   _| |_                                                                                                
    | | '_ \| '_ \| | | | __|                                                                                               
    | | | | | |_) | |_| | |_                                                                                                
    |_|_| |_| .__/ \__,_|\__|                                                                                               
            |_|                                                                                                             
    ;                                                                                                                       
                                                                                                                            
     %let num0=constant("PI");                                                                                              
     %let num1=constant("EULER");                                                                                           
     %let num2=2;                                                                                                           
                                                                                                                            
    *            _               _                                                                                          
      ___  _   _| |_ _ __  _   _| |_                                                                                        
     / _ \| | | | __| '_ \| | | | __|                                                                                       
    | (_) | |_| | |_| |_) | |_| | |_                                                                                        
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                       
                    |_|                                                                                                     
    ;                                                                                                                       
                                                                                                                            
    MYRESULT=0.56437698868826                                                                                               
                                                                                                                            
    *          _       _   _                                                                                                
     ___  ___ | |_   _| |_(_) ___  _ __                                                                                     
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                    
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                   
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                   
                                                                                                                            
    ;                                                                                                                       
                                                                                                                            
    %symdel mydiff num0 num1 num2 diff /nowarn;                                                                             
                                                                                                                            
    %macro calc(num0,num1,num2);                                                                                            
       %let rc=%sysfunc(dosubl('                                                                                            
          data _null_;                                                                                                      
              s=&num1 + &num2;                                                                                              
              d=&num0 - s;                                                                                                  
              lossless=put(d,hex16.);                                                                                       
              call symputx("diff",lossless);                                                                                
          run;quit;                                                                                                         
       '));                                                                                                                 
        &diff                                                                                                               
    %mend calc;                                                                                                             
                                                                                                                            
    %let myresult=%sysfunc(                                                                                                 
       inputn(%calc(constant("PI"),constant("EULER"),2),hex16.)                                                             
       );                                                                                                                   
                                                                                                                            
    %put &=myresult;                                                                                                        
                                                                                                                            
                                                                                                                            
