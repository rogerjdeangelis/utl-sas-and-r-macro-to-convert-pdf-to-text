# utl-sas-and-r-macro-to-convert-pdf-to-text
SAS and r macro to convert pdf to text
    %let pgm=utl-sas-and-r-macro-to-convert-pdf-to-text;

    %stop_submission;

    SAS and r macro to convert pdf to text

    see github for documentation and complete code

    pdf input file
    https://tinyurl.com/4ke779bu
    https://github.com/rogerjdeangelis/utl-sas-and-r-macro-to-convert-pdf-to-text/blob/main/table.pdf

    github
    https://tinyurl.com/bdhrt8rk
    https://github.com/rogerjdeangelis/utl-sas-and-r-macro-to-convert-pdf-to-text

    PDF file
    https://tinyurl.com/4ke779bu

    CONVERT PDF TO TEXT

    %utl_pdftotext(
       inp=d:/pdf/table.pdf
      ,out=d:/txt/table.txt
      );

    SAMPLE OUTPUT

    SEX=F

    Obs AGE WEIGHT HEIGHT
      1     13   112    69
      2     13    84    56
      3     14    98    65
    SEX          294   190


    SEX=M

    Obs AGE WEIGHT HEIGHT
      4     14   102    62
      5     14   102    63
      6     12    83    57
    SEX          287   182
                 581   372

    RELATED REPOS ON END


    /**************************************************************************************************************************/
    /* INPUT                    | PROCESS                                           | OUTPUT                                  */
    /* =====                    | =======                                           | ======                                  */
    /*               H  W       | * CREATE PDF;                                     | PDF INPUT                               */
    /*               E  E       | -------------                                     | ---------                               */
    /*    N          I  I       |                                                   |                                         */
    /*    A    S  A  G  G       | %utlfkil(d:/pdf/table.pdf);                       |                                         */
    /*    M    E  G  H  H       |                                                   |                                         */
    /*    E    X  E  T  T       | ods pdf                                           | SEX=F                                   */
    /*                          |    file="d:/pdf/table.pdf"                        |                                         */
    /* Alice   F 13 69 112      |    style=journal;                                 | Obs    AGE WEIGHT HEIGHT                */
    /* Barbara F 13 56  84      |                                                   |   1     13   112    69                  */
    /* Carol   F 14 65  98      | ods pdf file="d:/pdf/table.pdf";                  |   2     13    84    56                  */
    /* Henry   M 14 62 102      | proc print                                        |   3     14    98    65                  */
    /* Alfred  M 14 63 102      |   data=class width=min;                           | SEX          294   190                  */
    /* James   M 12 57  83      |   by sex ;                                        |                                         */
    /*                          |   var age weight height;                          |                                         */
    /*                          |   sum weight height;                              | SEX=M                                   */
    /* options                  | run;quit;                                         |                                         */
    /*  validvarname=upcase;    | ods pdf close;                                    | Obs    AGE WEIGHT HEIGHT                */
    /* libname sd1 "d:/sd1";    |                                                   |   4     14   102    62                  */
    /* data sd1.have;           |                                                   |   5     14   102    63                  */
    /*   input                  | * CREATE TEXT FILE;                               |   6     12    83    57                  */
    /*     name$                | -------------------                               | SEX          287   182                  */
    /*     sex$ age             |                                                   |              581   372                  */
    /*     height               | title;                                            |                                         */
    /*     weight;              | footnote;                                         |                                         */
    /* cards4;                  | %symdel inp out / nowarn;                         |                                         */
    /* Alice   F 13 69 112      | %utlfkil(d:/txt/table.txt);                       |                                         */
    /* Barbara F 13 56 84       |                                                   |                                         */
    /* Carol   F 14 65 98       | %macro utl_pdftotext(inp,out)                     |                                         */
    /* Henry   M 14 62 102      |   / des="convert a pdf to text";                  |                                         */
    /* Alfred  M 14 63 102      |                                                   |                                         */
    /* James   M 12 57 83       |   %utl_submit_r64x("                              |                                         */
    /* ;;;;                     |     library(tm);                                  |                                         */
    /* run;quit;                |     library(pdftools);                            |                                         */
    /*                          |     file<-'&inp';                                 |                                         */
    /*                          |     Rpdf<-readPDF(                                |                                         */
    /*                          |       control=list(text='-layout'));              |                                         */
    /*                          |     corpus<-VCorpus(URISource(file),              |                                         */
    /*                          |     readerControl=list(reader=Rpdf));             |                                         */
    /*                          |     want<-content(content(corpus)[[1]]);          |                                         */
    /*                          |     write(want,file='&out');                      |                                         */
    /*                          |     lines<-unlist(strsplit(want,'\n'));           |                                         */
    /*                          |     non_empty_lines<-                             |                                         */
    /*                          |       lines[!grepl('^\\s*$',lines)];              |                                         */
    /*                          |     write(non_empty_lines                         |                                         */
    /*                          |       ,file='table.txt');                         |                                         */
    /*                          |   ");                                             |                                         */
    /*                          |                                                   |                                         */
    /*                          | %mend utl_pdftotext;                              |                                         */
    /*                          |                                                   |                                         */
    /*                          | %utl_pdftotext(                                   |                                         */
    /*                          |    inp=d:/pdf/table.pdf                           |                                         */
    /*                          |   ,out=d:/txt/table.txt                           |                                         */
    /*                          |   );                                              |                                         */
    /**************************************************************************************************************************/



    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options
     validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
      input
        name$
        sex$ age
        height
        weight;
    cards4;
    Alice   F 13 69 112
    Barbara F 13 56 84
    Carol   F 14 65 98
    Henry   M 14 62 102
    Alfred  M 14 63 102
    James   M 12 57 83
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*     NAME      SEX    AGE    HEIGHT    WEIGHT                                                                           */
    /*                                                                                                                        */
    /*   Alice       F      13      69        112                                                                             */
    /*   Barbara     F      13      56         84                                                                             */
    /*   Carol       F      14      65         98                                                                             */
    /*   Henry       M      14      62        102                                                                             */
    /*   Alfred      M      14      63        102                                                                             */
    /*   James       M      12      57         83                                                                             */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    * CREATE PDF;

    %utlfkil(d:/pdf/table.pdf);

    ods pdf
       file="d:/pdf/table.pdf"
       style=journal;

    ods pdf file="d:/pdf/table.pdf";
    proc print
      data=class width=min;
      by sex ;
      var age weight height;
      sum weight height;
    run;quit;
    ods pdf close;


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    * CREATE TEXT FILE;

    title;
    footnote;
    %symdel inp out / nowarn;
    %utlfkil(d:/txt/table.txt);

    %macro utl_pdftotext(inp,out)
      / des="convert a pdf to text";

      %utl_submit_r64x("
        library(tm);
        library(pdftools);
        file<-'&inp';
        Rpdf<-readPDF(
          control=list(text='-layout'));
        corpus<-VCorpus(URISource(file),
        readerControl=list(reader=Rpdf));
        want<-content(content(corpus)[[1]]);
        write(want,file='&out');
        lines<-unlist(strsplit(want,'\n'));
        non_empty_lines<-
          lines[!grepl('^\\s*$',lines)];
        write(non_empty_lines
          ,file='table.txt');
      ");

    %mend utl_pdftotext;

    %utl_pdftotext(
       inp=d:/pdf/table.pdf
      ,out=d:/txt/table.txt
      );

    /**************************************************************************************************************************/
    /* SEX=F                                                                                                                  */
    /*                                                                                                                        */
    /* Obs AGE WEIGHT HEIGHT                                                                                                  */
    /*   1     13   112    69                                                                                                 */
    /*   2     13    84    56                                                                                                 */
    /*   3     14    98    65                                                                                                 */
    /* SEX          294   190                                                                                                 */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* SEX=M                                                                                                                  */
    /*                                                                                                                        */
    /* Obs AGE WEIGHT HEIGHT                                                                                                  */
    /*   4     14   102    62                                                                                                 */
    /*   5     14   102    63                                                                                                 */
    /*   6     12    83    57                                                                                                 */
    /* SEX          287   182                                                                                                 */
    /*              581   372                                                                                                 */
    /**************************************************************************************************************************/

    RELATED REPOS
    =============

    https://github.com/rogerjdeangelis/utl-convert-pdf-to-text-using-python-and-r
    https://github.com/rogerjdeangelis/utl-create-a-pdf-excel-html-proc-report-with-greek-letters
    https://github.com/rogerjdeangelis/utl-create-a-simple-n-percent-clinical-table-in-r-sas-wps-python-output-pdf-rtf-xlsx-html-list
    https://github.com/rogerjdeangelis/utl-create-mutiple-pdf-files-from-one-table-dosubl-ods-newfile-option
    https://github.com/rogerjdeangelis/utl-creating-identical-pdf-and-powerpoint-slides
    https://github.com/rogerjdeangelis/utl-example-rtf-excel-and-pdf-reports-using-all-sas-provided-style-templates
    https://github.com/rogerjdeangelis/utl-fit-a-beta-pdf-using-sas-nlmixed-and-r-fitdistplus-package
    https://github.com/rogerjdeangelis/utl-forever-free-for-now-pdfgear-edit-split-combine-delete-pages-substitute-for-acrobat-pro
    https://github.com/rogerjdeangelis/utl-formatting-ai-seacrh-output-in-pdf-rtf-and-excel-format-perplexity-chatGPT-results
    https://github.com/rogerjdeangelis/utl-identical-side-by-side-text-and-graphics-in-pdf-and-powerpoint
    https://github.com/rogerjdeangelis/utl-mle-symbolic-solution-for-mu-and-sigma-of-normal-pdf-using-sympy
    https://github.com/rogerjdeangelis/utl-overlaying-histograms-and-scatterplots-in-powerpoint-pdf-and-jpeg
    https://github.com/rogerjdeangelis/utl-putting-a-frame-around-text-in-doc-rtf-and-pdf-ods-destinations-with-and-without-layout
    https://github.com/rogerjdeangelis/utl-r-one-liner-scatter-plot-with-densities-along-vertical-and-horizontal-axes-in-pdf-and-ppt
    https://github.com/rogerjdeangelis/utl-removing-unwanted-bookmarks-in-pdf-table-of-contents-toc
    https://github.com/rogerjdeangelis/utl-sas-ods-bidirectional-hyperlinked-table-of-contents-in-ods-pdf-html-and-excel
    https://github.com/rogerjdeangelis/utl-sas-ods-underlining-text-in-html-pdf-and-rtf
    https://github.com/rogerjdeangelis/utl-scraping-pdf-output-for-pdf-tables-and-lists
    https://github.com/rogerjdeangelis/utl-search-all-pdfs-for-an-arbitrary-word-in-mutuiple-pdf-file
    https://github.com/rogerjdeangelis/utl-side-by-side-proc-report-output-in-pdf-html-and-excel
    https://github.com/rogerjdeangelis/utl-simple-three-letter-commands-to-format-perplexity-AI-results-for-word-pdf-text-and-excel
    https://github.com/rogerjdeangelis/utl-sympy-exact-pdf-and-cdf-for-the-correlation-coefficient-given-bivariate-normals
    https://github.com/rogerjdeangelis/utl-using-beta-cdf-and-pdf-unitsquare-to-fit-non-linear-equations-and-simple-polynomials
    https://github.com/rogerjdeangelis/utl_combine_pdf_files_and_delete_pages_from_a_pdf_pyPDF_ghostscript
    https://github.com/rogerjdeangelis/utl_combining_all_pdf_files_in_a_directory
    https://github.com/rogerjdeangelis/utl_convert_pdf_tables_to_SAS_WPS_datasets
    https://github.com/rogerjdeangelis/utl_convert_pdf_tables_to_sas_tables
    https://github.com/rogerjdeangelis/utl_create-png-and-pdf-matrix-barcodes-with-embedded-url-links-r-language-graphics-plot
    https://github.com/rogerjdeangelis/utl_dropping-down-to-R-and-converting-pdfs-to-sas-tables-and-text
    https://github.com/rogerjdeangelis/utl_dropping-down-to-powershell-and-converting-doc-and-rtf-files-to-pdfs
    https://github.com/rogerjdeangelis/utl_ods_pdf_and_rtf_two_different_page_titles_on_the_same_page
    https://github.com/rogerjdeangelis/utl_pdf_graphics_top_40_a_sas_ods_graphics_look_at_chicago_public_schools_salaries_by_job
    https://github.com/rogerjdeangelis/utl_report_does_not_show_group_variable_across_new_pages_in_rtf_and_pdf

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
