## Week 2 Lab Report 

In this lab, I will be investigating the find command and it's command line options. 

# find
find is a terminal command that is used to find files and directories. It can also be used to find certain files in order to perform other operations on them.  

Command-line Options: 
- -type
    The -type option is used to search for files/directories based on their type. Specifically, -type d will search for directories and not files (the d after type stands for directories)

    Example 1: 
    '''
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % find technical -type d
    technical
    technical/government
    technical/government/About_LSC
    technical/government/Env_Prot_Agen
    technical/government/Alcohol_Problems
    technical/government/Gen_Account_Office
    technical/government/Post_Rate_Comm
    technical/government/Media
    technical/plos
    technical/biomed
    technical/911report
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % 
    '''
    This command (find technical -type d) looked at the technical directory and found+listed the technical directory and all of the directories contained within the technical directory. This command could be useful to understand what a directory contains and their specific paths. 

    Example 2: 
    '''
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % find technical -type d -name "government"
    technical/government
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % 
    '''
    The type d command option can also be used in conjunction with the name option to find directories. In this command, I asked the computer to find a directory within the technical directory who's name contained the word "government". There was only one directory that fit this specification, the government directory so it was listed out to the terminal. This could be useful to check/confirm whether a directory is actually where you think it is. 

    Example 3: 
    '''
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % find technical/government -type d
    technical/government
    technical/government/About_LSC
    technical/government/Env_Prot_Agen
    technical/government/Alcohol_Problems
    technical/government/Gen_Account_Office
    technical/government/Post_Rate_Comm
    technical/government/Media
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % 
    '''
    This command (find technical/government -type d) looked at the government directory and found+listed the government directory and all of the directories contained within the government directory. This command can be broken down into find (path) (option). This command could be useful to understand what a directory contains and their specific paths. 

- -maxdepth
    The -maxdepth option descends to at most the level that you specify to find files/directories. For example, -maxdepth 2 finds files/directories at the current directory and one sublevel down. 

    Example 1: 
    '''
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % find technical -maxdepth 1 -name "*.txt"
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % 
    '''
    This command is looking for files that end with .txt and are contained in the technical directories (not subdirectories within technical). This is because I wrote 1 after the -maxdepth option which asks the computer to only look at the current directory. 

    Example 2: 
    '''
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % find technical -maxdepth 2 -name "*.txt"
    technical/plos/journal.pbio.0030094.txt
    technical/plos/journal.pbio.0020046.txt
    technical/plos/pmed.0020028.txt
    technical/plos/journal.pbio.0020052.txt
    technical/plos/pmed.0020148.txt
    technical/plos/pmed.0020160.txt
    technical/plos/pmed.0010048.txt
    technical/plos/pmed.0010060.txt
    technical/plos/journal.pbio.0030137.txt
    technical/plos/journal.pbio.0030136.txt
    technical/plos/pmed.0010061.txt
    technical/plos/pmed.0010049.txt
    technical/plos/pmed.0020161.txt
    technical/plos/journal.pbio.0020127.txt
    technical/plos/pmed.0020149.txt
    technical/plos/journal.pbio.0020133.txt
    technical/plos/pmed.0020015.txt
    technical/plos/journal.pbio.0020053.txt
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % 
    '''
    (There were many more files than this but I could not include them all so I chose to include a select amount of files in this code block). This command is looking for files that end with .txt and are contained in the technical directory and the directories one level down from techincal (911report, biomed, plos, government). This is because I wrote 2 after the -maxdepth option which asks the computer to look at the current directory and directories one level down.

    Example 3: 
    '''
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % find technical -maxdepth 2 -name "journal*"
    technical/plos/journal.pbio.0030032.txt
    technical/plos/journal.pbio.0020354.txt
    technical/plos/journal.pbio.0020156.txt
    technical/plos/journal.pbio.0020140.txt
    technical/plos/journal.pbio.0020183.txt
    technical/plos/journal.pbio.0020430.txt
    technical/plos/journal.pbio.0020394.txt
    technical/plos/journal.pbio.0020431.txt
    technical/plos/journal.pbio.0020419.txt
    technical/plos/journal.pbio.0020169.txt
    technical/plos/journal.pbio.0020035.txt
    technical/plos/journal.pbio.0030024.txt
    technical/plos/journal.pbio.0020223.txt
    technical/plos/journal.pbio.0020019.txt
    technical/plos/journal.pbio.0020145.txt
    technical/plos/journal.pbio.0020353.txt
    technical/plos/journal.pbio.0020347.txt
    '''
    This command is looking for files that have journal in it and are contained in the technical directory and the directories one level down from techincal (911report, biomed, plos, government). This is because I wrote 2 after the -maxdepth option which asks the computer to look at the current directory and directories one level down.

- -delete 
    The delete command option deletes files/directories

    Example 1: 
    '''
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % find technical/plos -name "journal.pbio.0020001.txt" -delete
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % 
    '''
    This command looks for a file named "journal.pbio.0020001.txt" in the directory technical/plos and deletes it. This command is useful to delete specific files or files of a certain type. 

    Example 2: 
    '''
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % find technical -name "todelete"  -delete                       
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % 
    '''
    For this command I created a new directory within technical called "todelete". Then I types this command which  looks for a file/directory named "todelete" in the directory technical and deletes it. 

    Example 3: 
    '''
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % find technical/biomed -name "1468-6708-3-1.txt" -delete
    (base) siyona@Siyonas-MacBook-Air-3 skill-demo1 % 
    ''' 
    This command looks for a file named "1468-6708-3-1.txt" in the directory technical/biomed and deletes it. This command is useful to delete specific files/directories or files/directories of a certain type. 





