## Send Emails through Python using SMTP server

### *Jupyter Notebook IDE is used to code and Sendgrid APIs used as a SMTP server*

## *Integration of the SMTP server through Sendgrid :*
<ul>
  <li>Create a account in Sendgrid and enter Email api. Choose SMTP relay.</li> <br>
  <code><img height = 200 src="https://github.com/ViduraErandika/Send-mails-through-Python/blob/main/images/choose.jpg"></code> <br>
  <li>Create an APIkey and copy the APIkey and password to python code and Verify Integration </li> <br>
  <code><img height = 200 src="https://github.com/ViduraErandika/Send-mails-through-Python/blob/main/images/intergration.jpg"></code> <br>  
</ul>

## *Update the python code in Jupyter Notebook :*

<ul>
  <li>Attach the CSV file which includes the destination mails.</li> <br> 
</ul>

```py
import pandas as pd
import numpy as np
import time
import sys
import os
import re

# sengrid smtplib protocols entered below
from smtplib import SMTP_SSL as SMTP       # this invokes the secure SMTP protocol (port 465, uses SSL)
# from smtplib import SMTP                  # use this for standard SMTP protocol   (port 25, no encryption)

# from email.MIMEText import MIMEText     # old version
from email.mime.text import MIMEText
from email.mime.image import MIMEImage
from email.mime.multipart import MIMEMultipart

log = pd.read_csv('/Users/vidur/Downloads/csv-test.csv', encoding='utf-8')    #enter your sending mails csv file HERE
```

<ul>
  <li>Update APIkey and password in followinf send_mail function.</li> <br> 
</ul>

``` py
def send_email(name,email,username,password,ref,i,teamname):
    SMTPserver = 'smtp.sendgrid.net'  #since i'm using sendgrid apis placed their SMTPserver here.
    sender =     'Test <***@uom.lk>'   # keyword <your sendgrid mail >
    destination = [email]            #sending destination
    print(i,end=" ")
    print(destination,end="")
    
    USERNAME = "apikey"               #set the sendgrid smtp api key and password here
    PASSWORD = "********************************************************"

    # typical values for text_subtype are plain, html, xml
    text_subtype = 'html'
    content="""\
            
            <p> Place Your Content here. </p>
    
    """ 
    subject="Email Subject here"

    try:
        msg = MIMEText(content, text_subtype)
        msg['Subject']=       subject
        msg['From']   = sender # some SMTP servers will do this automatically, not all

        conn = SMTP(SMTPserver)
        conn.set_debuglevel(False)
        conn.login(USERNAME, PASSWORD)
        try:
            conn.sendmail(sender, destination, msg.as_string())
        finally:
            print("*")
            conn.quit()
    except:
        failed.append(i)
        print("FAILED! - "+ str(destination))
```

<ul>
  <li>Run all the cells starting from 0.</li> <br> 
</ul>

### *Good Luck ❤*
