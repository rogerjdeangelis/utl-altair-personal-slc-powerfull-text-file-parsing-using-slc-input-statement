# utl-altair-personal-slc-powerfull-text-file-parsing-using-slc-input-statement
Altair personal slc powerfull text file parsing using slc input statement
    %let pgm=utl-altair-personal-slc-powerfull-text-file-parsing-using-slc-input-statement;

    %stop_submission;

    Altair personal slc powerfull text file parsing using slc input statement

    Too long to post here, see github

    github
    https://github.com/rogerjdeangelis/utl-altair-personal-slc-powerfull-text-file-parsing-using-slc-input-statement

    For full text file (beware of non printable charaters in some text files, easy to remove)
    https://community.altair.com/discussion/38458
    https://community.altair.com/discussion/38458/altair-monarch-exercise-26-meditech-detail-trial-balance-vs-ap-transactions?utm_source=community-search&utm_medium=organic-search&utm_term=exercise

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    From the text file below extract Account and Debit and Credit and compute net (Credit-Debit)

    Altair SLC

    Obs         ACCOUNT         DASH     DEBIT      CREDIT       NET

     1     PATIENT SERVICES      -       5662.0     5580.00     -82.00
     2     MEDICAL EQUIPMENT     -      15841.3    25316.97    9475.67


    /*         _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| `_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    */

    &_init_;
    ods listing;
    data net ;
      infile datalines firstobs=13;
      input @'10.0000.' +8  account & $44. /
        @'------------  ------------' +(-1) dash $1. / @45 debit comma14.2  @58 credit comma14.2 @;
      net = credit - debit;
    cards4;
    DATE: 03/15/20 @ 0124           Example Health System GL *LIVE*
    USER: ABCDEFG                       DETAIL TRIAL BALANCE

                                             MAR 2020
                                               TRIAL

                            FROM ACCOUNT                  THRU ACCOUNT
                            10.0000.000000                10.0000.000015


    ACCOUNT
                JOURNAL    DATE     BCH ENTRY         DEBITS       CREDITS  DESCRIPTION

    10.0000.000001 - PATIENT SERVICES

                JE         02/15/20 3   1                           250.00  AP ACCR N-Z *DE *REV
                JE         02/15/20 5   1                         5,330.00  AP ACCR A-M *SB *REV
                AP         03/06/20 1   161           200.00                V# A000001 I# 256168 F#
                                                                            Vendor: MEDICAID
                AP         03/26/21 2   69          2,665.00                V# M000021 I# 458795 F#
                                                                            Vendor: ABC BUILDING & CO.
                AP         03/26/21 2   132            82.00                V# A000001 I# 145798 F#
                                                                            Vendor: MEDICAID
                JE         03/24/20 21  1           2,665.00                AP ACCR A-M *SB *REV
                                                ------------  ------------
                                                    5,662.00      5,580.00
    ---------------------------------------------------------------------------------------------------------------------------
    10.0000.000002 - MEDICAL EQUIPMENT

                MM         02/15/20 5   165        10,065.00                V# M000003 PO# 12345678   ACCRUAL
                                                                            Vendor: LAB CORP, INC.
                MM         02/15/20 5   79                        4,476.16  V# M000006 PO# 23475890   ACCRUAL
                                                                            Vendor: STRYKER
                MM         02/15/20 5   155                       6,986.00  V# M000007 PO# 24579822   ACCRUAL
                                                                            Vendor: MEDTRONIC
                MM         02/15/20 5   247                         489.67  V# M000012 PO# 24598783   ACCRUAL
                                                                            Vendor: DEF
                MM         02/15/20 5   370                         400.14  V# M000023 PO# 24578798   ACCRUAL
                                                                            Vendor: PHILIPS
                MM         02/15/20 5   679                         900.00  V# M000019 PO# 46519894   ACCRUAL
                                                                            Vendor: 3M
                MM         03/24/20 1   36          4,476.16                V# M000006 PO# 23475890   ACCRUAL
                                                                            Vendor: STRYKER
                MM         03/24/20 1   138           400.14                V# M000023 PO# 34589788   ACCRUAL
                                                                            Vendor: PHILIPS
                MM         03/24/20 1   259           900.00                V# M000019 PO# 48748738   ACCRUAL
                                                                            Vendor: 3M
                MM         03/24/20 1   68                       12,065.00  V# M000003 PO# 12345678   ACCRUAL
                                                                            Vendor: LAB CORP, INC.
                                                ------------  ------------
                                                   15,841.30     25,316.97
    ;;;;
    run;quit;

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    proc print data=net;
    run;quit;

    Altair SLC

    Obs         ACCOUNT         DASH     DEBIT      CREDIT

     1     PATIENT SERVICES      -       5662.0     5580.00
     2     MEDICAL EQUIPMENT     -      15841.3    25316.97

    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    98
    199       &_init_;
    200       ods listing;
    201       data net ;
    202         infile datalines firstobs=13;
    203         input @'10.0000.' +8  account & $44. /
    204           @'------------  ------------' +(-1) dash $1. / @45 debit comma14.2  @58 credit comma14.2 @;
    205         net = credit - debit;
    206       cards4;

    NOTE: Data set "WORK.net" has 2 observation(s) and 5 variable(s)
    NOTE: The data step took :
          real time : 0.004
          cpu time  : 0.015


    207       DATE: 03/15/20 @ 0124           Example Health System GL *LIVE*
    208       USER: ABCDEFG                       DETAIL TRIAL BALANCE
    209
    210                                                MAR 2020
    211                                                  TRIAL
    212
    213                               FROM ACCOUNT                  THRU ACCOUNT
    214                               10.0000.000000                10.0000.000015
    215
    216
    217       ACCOUNT
    218                   JOURNAL    DATE     BCH ENTRY         DEBITS       CREDITS  DESCRIPTION
    219
    220       10.0000.000001 - PATIENT SERVICES
    221
    222                   JE         02/15/20 3   1                           250.00  AP ACCR N-Z *DE *REV
    223                   JE         02/15/20 5   1                         5,330.00  AP ACCR A-M *SB *REV
    224                   AP         03/06/20 1   161           200.00                V# A000001 I# 256168 F#
    225                                                                               Vendor: MEDICAID
    226                   AP         03/26/21 2   69          2,665.00                V# M000021 I# 458795 F#
    227                                                                               Vendor: ABC BUILDING & CO.
    228                   AP         03/26/21 2   132            82.00                V# A000001 I# 145798 F#
    229                                                                               Vendor: MEDICAID
    230                   JE         03/24/20 21  1           2,665.00                AP ACCR A-M *SB *REV
    231                                                   ------------  ------------
    232                                                       5,662.00      5,580.00
    233       ---------------------------------------------------------------------------------------------------------------------------
    234       10.0000.000002 - MEDICAL EQUIPMENT
    235
    236                   MM         02/15/20 5   165        10,065.00                V# M000003 PO# 12345678   ACCRUAL
    237                                                                               Vendor: LAB CORP, INC.
    238                   MM         02/15/20 5   79                        4,476.16  V# M000006 PO# 23475890   ACCRUAL
    239                                                                               Vendor: STRYKER
    240                   MM         02/15/20 5   155                       6,986.00  V# M000007 PO# 24579822   ACCRUAL
    241                                                                               Vendor: MEDTRONIC
    242                   MM         02/15/20 5   247                         489.67  V# M000012 PO# 24598783   ACCRUAL
    243                                                                               Vendor: DEF
    244                   MM         02/15/20 5   370                         400.14  V# M000023 PO# 24578798   ACCRUAL
    245                                                                               Vendor: PHILIPS
    246                   MM         02/15/20 5   679                         900.00  V# M000019 PO# 46519894   ACCRUAL
    247                                                                               Vendor: 3M
    248                   MM         03/24/20 1   36          4,476.16                V# M000006 PO# 23475890   ACCRUAL
    249                                                                               Vendor: STRYKER
    250                   MM         03/24/20 1   138           400.14                V# M000023 PO# 34589788   ACCRUAL
    251                                                                               Vendor: PHILIPS
    252                   MM         03/24/20 1   259           900.00                V# M000019 PO# 48748738   ACCRUAL
    253                                                                               Vendor: 3M
    254                   MM         03/24/20 1   68                       12,065.00  V# M000003 PO# 12345678   ACCRUAL
    255                                                                               Vendor: LAB CORP, INC.
    256                                                   ------------  ------------
    257                                                      15,841.30     25,316.97
    258       ;;;;
    259       run;quit;
    260
    261
    262       proc print data=net;
    263       run;quit;
    NOTE: 2 observations were read from "WORK.net"
    NOTE: Procedure print step took :
          real time : 0.026
          cpu time  : 0.000


    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
