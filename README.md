# CBT247
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. 
Due to amazing work by Alison Zhang and Jake Choi repos are no longer deleted.

```
//***FILE 247 is from Jim Marshall and Sam Golob and contains       *   FILE 247
//*           the "BRODCAST MANAGER" package of programs.  These    *   FILE 247
//*           programs are designed to eliminate the need for       *   FILE 247
//*           frequent SYNC's of the SYS1.BRODCAST dataset, and     *   FILE 247
//*           to give you control in displaying and deleting all    *   FILE 247
//*           user messages in the SYS1.BRODCAST dataset.           *   FILE 247
//*                                                                 *   FILE 247
//*           There are a great many utilities in this package.     *   FILE 247
//*           Users have contributed two front-ends so far.         *   FILE 247
//*                                                                 *   FILE 247
//*  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -  *   FILE 247
//*                                                                 *   FILE 247
//*     Important note:  A load module in TSO XMIT program for      *   FILE 247
//*           the vastly improved BDMSCAN program, which is part    *   FILE 247
//*           of the "Broadcast Master" commercial product from     *   FILE 247
//*           Sam Golob Systems Programming LLC, has been included  *   FILE 247
//*           as member BDMSCAN of this pds.  JCL to create a       *   FILE 247
//*           load library and run this program, has been included  *   FILE 247
//*           as member BDMSCAN$.  Try it.  You'll like it.         *   FILE 247
//*                                                                 *   FILE 247
//*           Full permission is granted from Sam Golob Systems     *   FILE 247
//*           Programming LLC, for anyone to run this copy of       *   FILE 247
//*           BDMSCAN anywhere.  No strings attached.               *   FILE 247
//*                                                                 *   FILE 247
//*  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -  *   FILE 247
//*                                                                 *   FILE 247
//*     I have just added an APF-authorized TSO command called      *   FILE 247
//*           BDMNNOTC which INSTANTLY changes the number of        *   FILE 247
//*           Global Notices records that are produced by the       *   FILE 247
//*           ACCOUNT/SYNC programs from IBM.  You just say         *   FILE 247
//*                                                                 *   FILE 247
//*                BDMNNOTC 200                                     *   FILE 247
//*                                                                 *   FILE 247
//*           and you can change the number of notices from 100     *   FILE 247
//*           (IBM's default) to 200 instantly, with no fuss and    *   FILE 247
//*           no IPL's and no zaps to IKJEFXSR/IKJEBLMT necessary.  *   FILE 247
//*                                                                 *   FILE 247
//*  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -  *   FILE 247
//*     Member $$BCMASM will assemble and link all BCM modules.     *   FILE 247
//*     Member $ASMSING will assemble and link one BCM module.      *   FILE 247
//*  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -  *   FILE 247
//*                                                                 *   FILE 247
//*  Improvements:                                                  *   FILE 247
//*                                                                 *   FILE 247
//*     1.  The userid ADD and userid DELETE programs, BCMUSADD     *   FILE 247
//*         and BCMUSDEL respectively, now use the TSO PUTLINE      *   FILE 247
//*         interface instead of TPUT, so you can get meaningful    *   FILE 247
//*         reports when you add or delete userids into the         *   FILE 247
//*         BRODCAST dataset using TSO-in-batch.                    *   FILE 247
//*                                                                 *   FILE 247
//*     2.  Three programs have been added to do direct writes      *   FILE 247
//*         to the NOTICES section of SYS1.BRODCAST or a copy       *   FILE 247
//*         of it.  BCMNLIST will list all active Notices messages  *   FILE 247
//*         in the allocated instance of SYS1.BRODCAST.  BCMNOTFY   *   FILE 247
//*         will create messages, delete messages or create blank   *   FILE 247
//*         messages in the NOTICES section of SYS1.BRODCAST or     *   FILE 247
//*         a copy of it.  To make those changes readable by        *   FILE 247
//*         LISTBC (which is the point), the BCMNUPD (authorized)   *   FILE 247
//*         TSO command sets a bit in the TSO Vector Table on,      *   FILE 247
//*         (this is the TSVTNCTU bit in TSVTFLG1) so anybody's     *   FILE 247
//*         execution of LISTBC will force an update to the         *   FILE 247
//*         incore Notices Table (only true for z/OS 1.3 MVS        *   FILE 247
//*         systems and later).                                     *   FILE 247
//*                                                                 *   FILE 247
//*         If the TSVTNCTU bit is on in a z/OS 1.2 or earlier      *   FILE 247
//*         MVS system, an OPER SEND ' ',SAVE command has to be     *   FILE 247
//*         executed, in order for the BRODCAST dataset to be       *   FILE 247
//*         re-read and the incore Notices table rewritten.         *   FILE 247
//*                                                                 *   FILE 247
//*         Members having names that begin with BCMN**** have      *   FILE 247
//*         to do with sending Broadcast Notify messages.  A few    *   FILE 247
//*         sample CLISTs are included to show how these programs   *   FILE 247
//*         can be deployed.  Lowercase messages can be sent with   *   FILE 247
//*         the BCMNOTFY program.  If you do this with a CLIST,     *   FILE 247
//*         you should specify CONTROL ASIS.                        *   FILE 247
//*                                                                 *   FILE 247
//*     3.  Full support for changing NOTICES records was added     *   FILE 247
//*         with the BCMNOTFY and BCMNUPD programs.  BCMNOTFY will  *   FILE 247
//*         add or delete messages, or replace a message line with  *   FILE 247
//*         (30) blanks.  BCMNUPD is an APF authorized TSO command  *   FILE 247
//*         which is necessary to flip a bit on, that tells LISTBC  *   FILE 247
//*         or OPER SEND, etc. (depending on TSO/E release) to      *   FILE 247
//*         update the incore Global Notices table that LISTBC      *   FILE 247
//*         reports the Notices from.  Our BCMNLIST program will    *   FILE 247
//*         read the Global Notices directly from SYS1.BRODCAST,    *   FILE 247
//*         but not from the incore Notices table that LISTBC       *   FILE 247
//*         reads.                                                  *   FILE 247
//*                                                                 *   FILE 247
//*     4.  Another way of handling NOTICES comes from Paul W.      *   FILE 247
//*         Lemons' BCEDIT package, which has been copied to this   *   FILE 247
//*         file from File 479.                                     *   FILE 247
//*                                                                 *   FILE 247
//*         BCEDIT** consists of 3 REXX execs that allow the        *   FILE 247
//*         administrator to ISPF-edit the global Broadcast         *   FILE 247
//*         Notices, and optionally, re-SEND them out               *   FILE 247
//*         conveniently, without having to format any OPERATOR     *   FILE 247
//*         SEND commands.  These execs do all the OPERATOR         *   FILE 247
//*         SENDs for you.  (Changed not to strip leading blanks.   *   FILE 247
//*         Old version is still available as BCEDIT@.  SG)         *   FILE 247
//*                                                                 *   FILE 247
//*         BCEDIT was fixed by Lionel Dyck to eliminate trouble    *   FILE 247
//*         arising from single quotes in the LISTBC messages.      *   FILE 247
//*         (Oct/2023)                                              *   FILE 247
//*                                                                 *   FILE 247
//*         Important note:  In order for the BCEDIT package to     *   FILE 247
//*         be able to issue the proper OPERATOR SEND commands on   *   FILE 247
//*         behalf of the TSO user, TSO CONSOLE authority has to    *   FILE 247
//*         have been turned on.  To make that job easier, an       *   FILE 247
//*         updated version of the authorized TSO command CPSCB     *   FILE 247
//*         has been included in this file.  Since CPSCB does not   *   FILE 247
//*         produce any TSO output when it has executed success-    *   FILE 247
//*         fully, its companion TSO command LPSCB (List the PSCB)  *   FILE 247
//*         has also been included in this file.  These two TSO     *   FILE 247
//*         commands are designed to be used together, with CPSCB   *   FILE 247
//*         doing the changing, and LPSCB doing the reporting.      *   FILE 247
//*                                                                 *   FILE 247
//*     5.  A new member $NOTICE was added, to give an example      *   FILE 247
//*         CLIST to update the BROADCAST Notices for all TSO       *   FILE 247
//*         users, if you can't get the CONSOLE authority for       *   FILE 247
//*         using the BCEDIT REXX.  Also see members BCMNCLxx       *   FILE 247
//*         and BCMNRXxx.                                           *   FILE 247
//*                                                                 *   FILE 247
//*     6.  The BCMLIST and BCMDEL programs have been expanded      *   FILE 247
//*         to display, or delete, only SOME of the broadcast       *   FILE 247
//*         messages for a userid, not necessary ALL of them.       *   FILE 247
//*                                                                 *   FILE 247
//*         You have full control, which messages are kept, and     *   FILE 247
//*         which are to be deleted, by using the two new optional  *   FILE 247
//*         keywords:  SKIP(nn) and MSGS(mm).                       *   FILE 247
//*                                                                 *   FILE 247
//*         If SKIP(nn) is coded, the first nn records are ignored  *   FILE 247
//*         in the list or delete operation for a userid's messages.*   FILE 247
//*                                                                 *   FILE 247
//*         If MSGS(mm) is coded, the next mm records are listed    *   FILE 247
//*         (if BCMLIST is used) or deleted (if BCMDEL is used.)    *   FILE 247
//*                                                                 *   FILE 247
//*         This gives you full control about which messages to     *   FILE 247
//*         list or delete -- which are kept, and which deleted.    *   FILE 247
//*                                                                 *   FILE 247
//*         Vinh Vu's BCMISPF ISPF interface has been modified      *   FILE 247
//*         to deal with the new SKIP(nn) and MSGS(mm) keywords.    *   FILE 247
//*                                                                 *   FILE 247
//*     7.  A new program, BCMXPORT, has been created from the      *   FILE 247
//*         BCMLIST program, with an additional output, designed    *   FILE 247
//*         to format existing messages into SEND (or BCMSEND)      *   FILE 247
//*         commands, so that they can be reloaded into a new       *   FILE 247
//*         SYS1.BRODCAST dataset.  This program is best run,       *   FILE 247
//*         with JCL, under TSO-in-batch.                           *   FILE 247
//*                                                                 *   FILE 247
//*         All the SEND (or BCMSEND) commands, can be executed     *   FILE 247
//*         as a CLIST, to reload the new SYS1.BRODCAST dataset.    *   FILE 247
//*                                                                 *   FILE 247
//*         Output is in VB-255 format and the commands are         *   FILE 247
//*         displaced 8 bytes to the right.                         *   FILE 247
//*                                                                 *   FILE 247
//*         BCMXPORT supports the new SKIP(nn) and MSGS(mm)         *   FILE 247
//*         keywords.                                               *   FILE 247
//*                                                                 *   FILE 247
//*     8.  John Kalinich sent in a REXX exec and a panel from a    *   FILE 247
//*         former colleague of his, Mark Reschke, which is a very  *   FILE 247
//*         nice way of formatting various kinds of SEND commands   *   FILE 247
//*         directly from a panel.  I have packaged this in a new   *   FILE 247
//*         member called SENDX.  (I changed the name from SEND,    *   FILE 247
//*         so as not to confuse with the TSO SEND command, if      *   FILE 247
//*         this REXX is not the default "SEND" at your site.       *   FILE 247
//*                                                                 *   FILE 247
//*  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -  *   FILE 247
//*                                                                 *   FILE 247
//*  FE 1 -   An ISPF interface for some of the utilities in        *   FILE 247
//*           this package, was written by Vinh Vu, and is          *   FILE 247
//*           included as member BCMISPFI.  This member is in       *   FILE 247
//*           PDSLOAD format (or IEBUPDTE SYSIN format), and        *   FILE 247
//*           it expands to produce a separate pds.  The            *   FILE 247
//*           identical package, in TSO XMIT format, is in          *   FILE 247
//*           member BCMISPF in this pds.                           *   FILE 247
//*                                                                 *   FILE 247
//*           Installation of Vinh Vu's package on each of your     *   FILE 247
//*           MVS LPARs, makes it very easy to do ongoing           *   FILE 247
//*           maintenance to SYS1.BRODCAST, to make sure it         *   FILE 247
//*           doesn't get full.  You need the BCMDEL, BCMLIST,      *   FILE 247
//*           and BCMUSERS load modules installed as well.          *   FILE 247
//*                                                                 *   FILE 247
//*  FE 2 -   Willy Jensen "WJensen" <mail@wjensen.com> also        *   FILE 247
//*           added a package (member WJMAINT) which allows         *   FILE 247
//*           deletion of all messages for an id that has           *   FILE 247
//*           greater than a certain amount of messages (e.g.       *   FILE 247
//*           if a user has more than 200 messages, then            *   FILE 247
//*           delete all the messages for that user).  This         *   FILE 247
//*           process works by "brute force".  A more delicate      *   FILE 247
//*           method of controlling deletion of messages, is        *   FILE 247
//*           made possible by the SKIP(nn) and MSGS(mm) operands   *   FILE 247
//*           of the BCMDEL program, and the use of the BCMISPF     *   FILE 247
//*           ISPF interface from Vinh Vu.                          *   FILE 247
//*                                                                 *   FILE 247
//*  FE 3 -   I wrote a crude ISPF interface (members CLISTS        *   FILE 247
//*           and PANELS), but Vinh Vu's interface is MUCH NICER,   *   FILE 247
//*           and I recommend using that interface only (member     *   FILE 247
//*           BCMISPF or member BCMISPFI).                          *   FILE 247
//*                                                                 *   FILE 247
//*  - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -  *   FILE 247
//*                                                                 *   FILE 247
//*           This package is now a full function set of utilities  *   FILE 247
//*           to manage, copy, export, or import SYS1.BRODCAST.     *   FILE 247
//*           (Of course, I'm thinking about adding a bit more...)  *   FILE 247
//*                                                                 *   FILE 247
//*           Questions, please call or write to:                   *   FILE 247
//*                                                                 *   FILE 247
//*             Sam Golob,  845-731-9031                            *   FILE 247
//*             P.O. Box 702, Pomona,  NY 10970                     *   FILE 247
//*                                                                 *   FILE 247
//*             email:   sbgolob@cbttape.org                        *   FILE 247
//*                                                                 *   FILE 247
//*   >>>>>   You can also move SYS1.BRODCAST to a different        *   FILE 247
//*   >>>>>   device type (e.g. 3380 to 3390) and/or expand it,     *   FILE 247
//*   >>>>>   without losing any notices or user messages.          *   FILE 247
//*                                                                 *   FILE 247
//*   >>>>>   And you can dump SYS1.BRODCAST into a transportable   *   FILE 247
//*   >>>>>   format, then restore it from the dump file.           *   FILE 247
//*                                                                 *   FILE 247
//*           All TSO commands in this package use the TSO          *   FILE 247
//*           PUTLINE interface, so their outputs can be written    *   FILE 247
//*           to SYSOUT and printed.  Therefore, they can be run    *   FILE 247
//*           using TSO-in-Batch.                                   *   FILE 247
//*                                                                 *   FILE 247
//*           There are programs in this package to display and     *   FILE 247
//*           delete any TSO user's messages, and to display the    *   FILE 247
//*           contents of the SYS1.BRODCAST dataset in general.     *   FILE 247
//*           Now, there's also a program to dump the entire        *   FILE 247
//*           contents of SYS1.BRODCAST into a flat file, for       *   FILE 247
//*           moving or sending to anywhere, and there are two      *   FILE 247
//*           programs for restoring this dumped file. Both pgms    *   FILE 247
//*           will adjust for device type changes.  One will just   *   FILE 247
//*           restore the dumped file back into a direct access     *   FILE 247
//*           dataset, and the other will expand the SYS1.BRODCAST  *   FILE 247
//*           copy, by adding more blank user message records.      *   FILE 247
//*                                                                 *   FILE 247
//*     - - - - - - - - - - - - - - - - - - - - - - - - - - - -     *   FILE 247
//*                                                                 *   FILE 247
//*     See new member @ZAP#NOT for a quick way of changing the     *   FILE 247
//*     default number of NOTICES records, which ACCOUNT SYNC       *   FILE 247
//*     will format in SYS1.BRODCAST .  Usually it's done by        *   FILE 247
//*     coding a usermod, using the IKJBCAST macro with the         *   FILE 247
//*     BCLMT=nnn operand.  Sample for that is in SYS1.SAMPLIB,     *   FILE 247
//*     member BCSTSMPE.  (That is the "long and orderly" way.)     *   FILE 247
//*                                                                 *   FILE 247
//*     - - - - - - - - - - - - - - - - - - - - - - - - - - - -     *   FILE 247
//*                                                                 *   FILE 247
//*     Programs Included - by name:                                *   FILE 247
//*                                                                 *   FILE 247
//*     BCMCLEAN  -  When LISTBC deletes a user message, it only    *   FILE 247
//*                  marks it as deleted, without clearing out old  *   FILE 247
//*                  message content from SYS1.BRODCAST.  BCMCLEAN  *   FILE 247
//*                  cleans & zeros out all deleted records, so if  *   FILE 247
//*                  you BROWSE or REVIEW (File 134) SYS1.BRODCAST, *   FILE 247
//*                  you'll really see how empty or full it is.     *   FILE 247
//*                                                                 *   FILE 247
//*                  Options: BCMCLEAN      - (no parameters)       *   FILE 247
//*                                           Cleans global and     *   FILE 247
//*                                           usrid records both.   *   FILE 247
//*                           BCMCLEAN N    - Cleans global         *   FILE 247
//*                                           notices records.      *   FILE 247
//*                           BCMCLEAN U or - Cleans all unused     *   FILE 247
//*                           BCMCLEAN M      userid records.       *   FILE 247
//*                                                                 *   FILE 247
//*     BCMDEL    -  TSO Command to display and delete any user's   *   FILE 247
//*                  messages, but it works directly on the         *   FILE 247
//*                  SYS1.BRODCAST dataset itself (or a copy) and   *   FILE 247
//*                  goes in, does the enqueues, and does all the   *   FILE 247
//*                  work directly.  Since it doesn't need LISTBC,  *   FILE 247
//*                  this command doesn't have to run authorized.   *   FILE 247
//*                  Can't work on Userlogs.  Only SYS1.BRODCAST.   *   FILE 247
//*                                                                 *   FILE 247
//*     BCMDIAG   -  Attempts to find "orphaned messages" which     *   FILE 247
//*                  are "officially valid" but which are not       *   FILE 247
//*                  part of a userid message chain.  Once found,   *   FILE 247
//*                  you                                            *   FILE 247
//*                                                                 *   FILE 247
//*                  Key byte of a null record is X'FF'.  First     *   FILE 247
//*                  data byte is "R" from CCHHR or TTR.            *   FILE 247
//*                                                                 *   FILE 247
//*     BCMDUMP   -  Works with BCMREST and BCMEXPND.  Dumps the    *   FILE 247
//*                  RECFM=DA SYS1.BRODCAST dataset into a RECFM=FB *   FILE 247
//*                  LRECL=130 dataset that can be moved anywhere.  *   FILE 247
//*                  BCMREST will reload this dump into a copy of   *   FILE 247
//*                  SYS1.BRODCAST, even across different device    *   FILE 247
//*                  types.  BCMEXPND will also do this, but it     *   FILE 247
//*                  will add blank userid messages to fill all     *   FILE 247
//*                  allocated primary extent space.  Therefore,    *   FILE 247
//*                  with BCMEXPND, you can enlarge SYS1.BRODCAST   *   FILE 247
//*                  without losing the messages.  Or you can move  *   FILE 247
//*                  it, to a different pack or even a different    *   FILE 247
//*                  system.                                        *   FILE 247
//*                                                                 *   FILE 247
//*     BCMEXPND  -  Works from a BCMDUMP RECFM=FB LRECL=130 dump   *   FILE 247
//*                  of SYS1.BRODCAST dataset, and will restore it, *   FILE 247
//*                  with all the messages and notices, to a copy   *   FILE 247
//*                  of SYS1.BRODCAST, that has been enlarged with  *   FILE 247
//*                  blank userid message records, to fit a bigger  *   FILE 247
//*                  allocated space.  Therefore, you can make      *   FILE 247
//*                  SYS1.BRODCAST bigger, without losing any       *   FILE 247
//*                  messages, and without doing an ACCOUNT SYNC.   *   FILE 247
//*                  Needs an IPL.  Compensates for different       *   FILE 247
//*                  device types.  (This may be the first time     *   FILE 247
//*                  in the history of OS and MVS that this could   *   FILE 247
//*                  be done.  I've never heard of another such     *   FILE 247
//*                  program.)                                      *   FILE 247
//*                                                                 *   FILE 247
//*     BCMREST   -  Does the same as BCMEXPND, but doesn't add     *   FILE 247
//*                  any new records.  Just restores the records    *   FILE 247
//*                  that were dumped.  Will compensate for         *   FILE 247
//*                  different disk device types.  You can move     *   FILE 247
//*                  SYS1.BRODCAST from a 3380 to a 3390, for       *   FILE 247
//*                  example, without losing any messages.          *   FILE 247
//*                                                                 *   FILE 247
//*     BCMLIST   -  TSO command, not authorized or restricted,     *   FILE 247
//*                  to list any user's (or all users') messages    *   FILE 247
//*                  in SYS1.BRODCAST.  Doesn't do Userlogs.        *   FILE 247
//*                  All the BCMLIS* programs can be invoked,       *   FILE 247
//*                  using a special userid name ALL$#@, which      *   FILE 247
//*                  will display information for all userids       *   FILE 247
//*                  defined to SYS1.BRODCAST.  All these BCMLIS*   *   FILE 247
//*                  commands can be run under TSO-in-Batch.        *   FILE 247
//*                                                                 *   FILE 247
//*     BCMLISY   -  Same as BCMLIST, but shows each message's      *   FILE 247
//*                  Relative Record Address.  (For diagnostic      *   FILE 247
//*                  purposes, to show the message chain.)          *   FILE 247
//*                                                                 *   FILE 247
//*     BCMLISX   -  Same as BCMLISY, but also shows entries for    *   FILE 247
//*                  users with no outstanding messages.  Can be    *   FILE 247
//*                  used (somewhat awkwardly) to display a list    *   FILE 247
//*                  of all defined userids in SYS1.BRODCAST.       *   FILE 247
//*                  For that purpose, use the BCMUSERS program.    *   FILE 247
//*                  This program is best used in TSO-in-Batch.     *   FILE 247
//*                                                                 *   FILE 247
//*     BCMNLIST  -  List NOTICES messages on the SYS1.BRODCAST     *   FILE 247
//*                  dataset, or a copy of it, in a format          *   FILE 247
//*                  similar to that produced by the "SEND LIST"    *   FILE 247
//*                  subcommand of the OPERATOR TSO command.        *   FILE 247
//*                  This command does not have to be authorized.   *   FILE 247
//*                                                                 *   FILE 247
//*     BCMNOTFY  -  Write NOTICES by message number to             *   FILE 247
//*                  SYS1.BRODCAST or a copy of it.  You can        *   FILE 247
//*                  write a new message to a given message number  *   FILE 247
//*                  without deleting the old message that was      *   FILE 247
//*                  there first.  You can delete a message from    *   FILE 247
//*                  a given number, or you can write a message     *   FILE 247
//*                  of blanks to a given number.  This command     *   FILE 247
//*                  does not have to be authorized.                *   FILE 247
//*                                                                 *   FILE 247
//*     BCMNUPD   -  Authorized TSO command, executed without       *   FILE 247
//*                  parameters, to update the bit in the TSO       *   FILE 247
//*                  Vector Table that forces a new copy of the     *   FILE 247
//*                  Incore Notices Table (that is read by LISTBC)  *   FILE 247
//*                  to be rewritten at the next LISTBC execution.  *   FILE 247
//*                  This makes all BCMNOTFY changes to the         *   FILE 247
//*                  BRODCAST dataset immediately readable by       *   FILE 247
//*                  LISTBC. (True for z/OS 1.3 and later.  See     *   FILE 247
//*                  comments in the BCMNHELP member for info       *   FILE 247
//*                  about setting this bit for z/OS 1.2 and        *   FILE 247
//*                  before.)                                       *   FILE 247
//*                                                                 *   FILE 247
//*     BCMSEND   -  This TSO command is sort of similar to a       *   FILE 247
//*                  TSO SEND command, except for some very         *   FILE 247
//*                  significant differences.  First, BCMSEND       *   FILE 247
//*                  only writes messsages to the BRODCAST dataset. *   FILE 247
//*                  It doesn't matter if the user is logged on.    *   FILE 247
//*                  Second, BCMSEND doesn't use the TSO parser.    *   FILE 247
//*                  Therefore, it doesn't "validity check" the     *   FILE 247
//*                  text of the message.  Everything that is in    *   FILE 247
//*                  the command buffer after 7 characters of the   *   FILE 247
//*                  userid, goes into the message--even hex data.  *   FILE 247
//*                  This is until the last non-blank character.    *   FILE 247
//*                  Third, you can use BCMSEND to write to a copy  *   FILE 247
//*                  of the SYS1.BRODCAST dataset, as well as to    *   FILE 247
//*                  the real one.  Just allocate the BRODCAST      *   FILE 247
//*                  ddname to the other dataset, not to the        *   FILE 247
//*                  cataloged SYS1.BRODCAST dataset.  You need     *   FILE 247
//*                  UPDATE authority to the BRODCAST dataset, to   *   FILE 247
//*                  use BCMSEND to write to it.                    *   FILE 247
//*                                                                 *   FILE 247
//*     BCMUSADD  -  Uses IBM's IKJIFRIF interface.  This is a      *   FILE 247
//*                  TSO command to add an arbitrary user name      *   FILE 247
//*                  as a userid in SYS1.BRODCAST.  This command    *   FILE 247
//*                  can be used in conjunction with BCMUSDEL.      *   FILE 247
//*                  Adding a userid with BCMUSADD has nothing      *   FILE 247
//*                  to do with either UADS or RACF.  But it        *   FILE 247
//*                  allows the system to SEND messages to this     *   FILE 247
//*                  arbitrary (up to 7 characters) name.           *   FILE 247
//*                  (Now uses the TSO PUTLINE interface and can    *   FILE 247
//*                  be run under TSO-in-batch or TSSO.)            *   FILE 247
//*                                                                 *   FILE 247
//*     BCMUSDEL  -  TSO command to delete an arbitrary TSO         *   FILE 247
//*                  userid record from SYS1.BRODCAST.  When the    *   FILE 247
//*                  userid is deleted, so are all its messages.    *   FILE 247
//*                  This command uses IBM's official IKJIFRIF      *   FILE 247
//*                  SYS1.BRODCAST interface.  Can be used to       *   FILE 247
//*                  clear all of a user's messages from SYS1.      *   FILE 247
//*                  BRODCAST without displaying them, but if you   *   FILE 247
//*                  want to keep the userid, you have to use       *   FILE 247
//*                  BCMUSADD afterwards, to add the id back.       *   FILE 247
//*                  (Now uses the TSO PUTLINE interface and can    *   FILE 247
//*                  be run under TSO-in-batch or TSSO.)            *   FILE 247
//*                                                                 *   FILE 247
//*     BCMSCAN   -  A modernization of the old BRODSCAN program    *   FILE 247
//*                  that is on this tape.  This is a batch program *   FILE 247
//*                  that does a general statistical survey of the  *   FILE 247
//*                  current state of the SYS1.BRODCAST dataset.    *   FILE 247
//*                  It displays all users who have outstanding     *   FILE 247
//*                  undelivered messages, and how many.  Therefore *   FILE 247
//*                  if SYS1.BRODCAST is full, or nearly so, you    *   FILE 247
//*                  run this program first, to determine which     *   FILE 247
//*                  userids are the culprits.                      *   FILE 247
//*                                                                 *   FILE 247
//*     BCMUSERS  -  TSO command to display all userids defined     *   FILE 247
//*                  to SYS1.BRODCAST.  This has nothing to do      *   FILE 247
//*                  with UADS or RACF.  Default is now to display  *   FILE 247
//*                  only users with outstanding messages.  If you  *   FILE 247
//*                  want to display all userids, use a parm of A   *   FILE 247
//*                  or ALL.                                        *   FILE 247
//*                                                                 *   FILE 247
//*                  If you use a parm of A, userids with           *   FILE 247
//*                  outstanding messages will be displayed with    *   FILE 247
//*                  2 extra lines.  One line shows the starting    *   FILE 247
//*                  and ending message pointer address in the      *   FILE 247
//*                  userid id record.  The other line shows the    *   FILE 247
//*                  number of outstanding messages for this        *   FILE 247
//*                  userid.                                        *   FILE 247
//*                                                                 *   FILE 247
//*     CPSCB and LPSCB  -  See note after BCEDIT comments above.   *   FILE 247
//*                                                                 *   FILE 247
//*     LSTB      -  A TSO command to list brodcast messages for    *   FILE 247
//*                  a userid (old program - disassembly)           *   FILE 247
//*                  Just submit to assemble.  Change load library. *   FILE 247
//*                  Does not delete the displayed messages.        *   FILE 247
//*                                                                 *   FILE 247
//*     MYID      -  A TSO command to display your own userid.      *   FILE 247
//*                  Uses the PSCBUSER field.  Written as a coding  *   FILE 247
//*                  exercise, but it's handy to use.  Fixed for    *   FILE 247
//*                  8-character userids, z/OS 2.3 and higher.      *   FILE 247
//*                                                                 *   FILE 247
//*     MYIDN     -  A PUTLINE'd version of MYID.  Not re-entrant.  *   FILE 247
//*                                                                 *   FILE 247
//*     MYIDP     -  A version of MYID which uses the TSO PUTLINE   *   FILE 247
//*                  interface and which can show output when run   *   FILE 247
//*                  under TSO-in-batch or TSSO.  Re-entrant.       *   FILE 247
//*                  Also shows system name, system FMID level,     *   FILE 247
//*                  the TSO user's ASID, the logon PROC name,      *   FILE 247
//*                  and the 4-digit machine type, you are running  *   FILE 247
//*                  on, plus the system residence pack and its     *   FILE 247
//*                  unit address.  Also shows the origin of the    *   FILE 247
//*                  TSO userid, UADS or the security system name.  *   FILE 247
//*                  it also shows your terminal id, and your       *   FILE 247
//*                  TSO prefix.                                    *   FILE 247
//*                                                                 *   FILE 247
//*     SYSTM     -  A TSO command to display what system you're    *   FILE 247
//*                  running on.  Also written as an exercise.      *   FILE 247
//*                  But also handy to have, so I'm making it       *   FILE 247
//*                  available here.                                *   FILE 247
//*                                                                 *   FILE 247
```
