        OOYacc is an Object Oriented version of standard Berkeley Yacc v1.9. 
        =====================================================================
  

Advantages over other Yacc's (Bison etc)
----------------------------------------

-A Complete object oriented Parser. 
-Parser can have as many instances. All of them can run concurrently. 
-The parser stack is a private member of the Parser instance. 
-Each parser is reenterent. One can abort from the parser and can resume from the previous state. 
-Is very usefull in concurrent or parallel text parsing using the same grammer. 
  
Differences  over  berkeley  Yacc
=================================
Always generate the header file y.tab.h.  The switch -d  is not  valid. 
The  yacc stack YYSTYPE  is a private data type of the parser class. 
It generates a parser class named  yyParser. 
The function YYSTYPE* getLVal()  is used to retrieve the  yacc stack. 

Using  the OOYACC
==================
The Header File format and usage
#ifndef <file Prefix)_OOYACC_H  // the default file prefix is y 
#define <fiel prefix>_OOYACC_H  // File prefixes are usefull when you have more than one grammar 
.... 
.... 
typedef union{ 
.... 
.... 
} YYSTYPE; // redefine YYSTYPE if using multiple grammars 
class <symbol prefix>Parser{   //  The default symbol prefix is yy. User defined prefixes 
                               //  are useful when having more than one 
                               //  parser class. 
  private: 
    int yydebug; 
    int yynerrs; 
    int yyerrflag; 
    int yychar; 
    short *yyssp; 
    YYSTYPE *yyvsp; 
    YYSTYPE yyval; 
    YYSTYPE yylval; 
    short yyss[YYSTACKSIZE]; 
    YYSTYPE yyvs[YYSTACKSIZE]; 
    int yym,yyn,yystate; 
    char* yys; 
  public: 
    yyParser();            // default constructor of the parser. 
    int yyparse();         // the parser function 
    YYSTYPE* getLVal();    // function to retrieve the top of parser stack 
}; 

